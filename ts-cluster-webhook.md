---

copyright: 
  years: 2014, 2022
lastupdated: "2022-08-04"

keywords: openshift

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}



# Why do cluster operations fail due to a broken webhook?
{: #webhooks_update}
{: support}

Supported infrastructure providers
:   Classic
:   VPC


During a master operation such as updating your cluster version, the cluster had a broken webhook application.
{: tsSymptoms}

Now, master operations can't complete. You see an error similar to the following:

```sh
can't complete cluster master operations because the cluster has a broken webhook application. For more information, see the troubleshooting docs: 'https://ibm.biz/master_webhook'
```
{: screen}


Your cluster has configurable Kubernetes webhook resources, validating or mutating admission webhooks, that can intercept and modify requests from various services in the cluster to the API server in the cluster master.
{: tsCauses}

Because webhooks can change or reject requests, broken webhooks can impact the functionality of the cluster in various ways, such as preventing you from updating the master version or other maintenance operations. For more information, see the [Dynamic Admission Control](https://kubernetes.io/docs/reference/access-authn-authz/extensible-admission-controllers/){: external} in the Kubernetes documentation.

Potential causes for broken webhooks include:
*   The underlying resource that issues the request is missing or unhealthy, such as a Kubernetes service, endpoint, or pod.
*   The webhook is part of an add-on or other plug-in application that did not install correctly or is unhealthy.
*   Your cluster might have a networking connectivity issue that prevents the webhook from communicating with the Kubernetes API server in the cluster master.

Identify and restore the resource that causes the broken webhook.
{: tsResolve}

1. Create a test pod to get an error that identifies the broken webhook. The error message might have the name of the broken webhook. If the webhook test passes, then the failure may have been temporary and can be retried.
    ```sh
    oc run webhook-test --image registry.ng.bluemix.net/armada-master/pause:3.2 -n ibm-system
    ```
    {: pre}

    In the following example, the webhook is `trust.hooks.securityenforcement.admission.cloud.ibm.com`.
    ```sh
    Error from server (InternalError): Internal error occurred: failed calling webhook "trust.hooks.securityenforcementadmission.cloud.ibm.com": Post https://ibmcloud-image-enforcement.ibm-system.svc:443/mutating-pods?timeout=30s: dialtcp 172.21.xxx.xxx:443: connect: connection timed out
    ```
    {: screen}

2. Get the name of the broken webhook.
    *   If the error message has a broken webhook, replace `trust.hooks.securityenforcement.admission.cloud.ibm.com` with the broken webhook that you previously identified.
        ```sh
        oc get mutatingwebhookconfigurations,validatingwebhookconfigurations -o jsonpath='{.items[?(@.webhooks[*].name=="trust.hooks.securityenforcement.admission.cloud.ibm.com")].metadata.name}{"\n"}'
        ```
        {: pre}

        Example output
        ```sh
        image-admission-config
        ```
        {: pre}

    *   If the error does not have a broken webhook, list all the webhooks in your cluster and check their configurations in the following steps.
        ```sh
        oc get mutatingwebhookconfigurations,validatingwebhookconfigurations
        ```
        {: pre}  
            
3. Review the service and location details of the mutating or validating webhook configuration in the `clientConfig` section in the output of the following command. Replace `image-admission-config` with the name that you previously identified. If the webhook exists outside the cluster, contact the cluster owner to check the webhook status.
    ```sh
    oc get mutatingwebhookconfiguration image-admission-config -o yaml
    ```
    {: pre}

    ```sh
    oc get validatingwebhookconfigurations image-admission-config -o yaml
    ```
    {: pre}

    Example output

    ```sh
      clientConfig:
        caBundle: <redacted>
        service:
            name: <name>
            namespace: <namespace>
            path: /inject
            port: 443
    ```
    {: screen}

4. **Optional**: Back up the webhooks, especially if you don't know how to reinstall the webhook.
    ```sh
    oc get mutatingwebhookconfiguration <name> -o yaml > mutatingwebhook-backup.yaml
    ```
    {: pre}

    ```sh
    oc get validatingwebhookconfiguration <name> -o yaml > validatingwebhook-backup.yaml
    ```
    {: pre}

5. Check the status of the related service and pods for the webhook.
    1. Check the service **Type**, **Selector**, and **Endpoint** fields.
        ```sh
        oc describe service -n <namespace> <service_name>
        ```
        {: pre}

    2. If the service type is **ClusterIP**, check that the pod for OpenVPN ({{site.data.keyword.redhat_openshift_notm}} version 4.7 or earlier) or Konnectivity ({{site.data.keyword.redhat_openshift_notm}} version 4.8 or later) is in a **Running** status so that the webhook can connect securely to the Kubernetes API in the cluster master. If the pod is not healthy, check the pod events, logs, worker node health, and other components to troubleshoot.

        * {{site.data.keyword.redhat_openshift_notm}} version 4.8 or later: Check the Konnectivity agent pods.
            ```sh
            oc describe pods -n kube-system -l app=konnectivity-agent
            ```
            {: pre}

        * {{site.data.keyword.redhat_openshift_notm}} version 4.7 or earlier: Check the OpenVPN client pods.
            ```sh
            oc describe pods -n kube-system -l app=vpn
            ```
            {: pre}

    3. If the service does not have an endpoint, check the health of the backing resources, such as a deployment or pod. If the resource is not healthy, check the pod events, logs, worker node health, and other components to troubleshoot. For more information, see [Debugging app deployments](/docs/containers?topic=containers-debug_apps).
        ```sh
        oc get all -n my-service-namespace -l <key=value>
        ```
        {: pre}

    4. If the service does not have any backing resources, or if troubleshooting the pods does not resolve the issue, remove the webhook.
        ```sh
        oc delete mutatingwebhook <name>
        ```
        {: pre}

6. Retry the cluster master operation, such as updating the cluster.
7. If you still see the error, you might have worker node or network connectivity issues.
    *   [Worker node troubleshooting](/docs/containers?topic=containers-debug_worker_nodes).
    *   Make sure that the webhook can connect to the Kubernetes API server in the cluster master. For example, if you use Calico network policies, security groups, or some other type of firewall, set up your [classic](/docs/containers?topic=containers-firewall) or [VPC](/docs/containers?topic=containers-vpc-firewall) cluster with the appropriate access.
    *   If the webhook is managed by an add-on that you installed, uninstall the add-on. Common add-ons that cause webhook issues include the following:
        * [Portieris](/docs/openshift?topic=openshift-images#portieris-image-sec)
8. Re-create the webhook or reinstall the add-on.




