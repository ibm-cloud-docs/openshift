---

copyright:
  years: 2014, 2021
lastupdated: "2021-05-26"

keywords: openshift, roks, rhoks, rhos

subcollection: openshift
content-type: troubleshoot

---

{:DomainName: data-hd-keyref="APPDomain"}
{:DomainName: data-hd-keyref="DomainName"}
{:android: data-hd-operatingsystem="android"}
{:api: .ph data-hd-interface='api'}
{:apikey: data-credential-placeholder='apikey'}
{:app_key: data-hd-keyref="app_key"}
{:app_name: data-hd-keyref="app_name"}
{:app_secret: data-hd-keyref="app_secret"}
{:app_url: data-hd-keyref="app_url"}
{:authenticated-content: .authenticated-content}
{:beta: .beta}
{:c#: data-hd-programlang="c#"}
{:cli: .ph data-hd-interface='cli'}
{:codeblock: .codeblock}
{:curl: .ph data-hd-programlang='curl'}
{:deprecated: .deprecated}
{:dotnet-standard: .ph data-hd-programlang='dotnet-standard'}
{:download: .download}
{:external: target="_blank" .external}
{:faq: data-hd-content-type='faq'}
{:fuzzybunny: .ph data-hd-programlang='fuzzybunny'}
{:generic: data-hd-operatingsystem="generic"}
{:generic: data-hd-programlang="generic"}
{:gif: data-image-type='gif'}
{:go: .ph data-hd-programlang='go'}
{:help: data-hd-content-type='help'}
{:hide-dashboard: .hide-dashboard}
{:hide-in-docs: .hide-in-docs}
{:important: .important}
{:ios: data-hd-operatingsystem="ios"}
{:java: .ph data-hd-programlang='java'}
{:java: data-hd-programlang="java"}
{:javascript: .ph data-hd-programlang='javascript'}
{:javascript: data-hd-programlang="javascript"}
{:new_window: target="_blank"}
{:note .note}
{:note: .note}
{:objectc data-hd-programlang="objectc"}
{:org_name: data-hd-keyref="org_name"}
{:php: data-hd-programlang="php"}
{:pre: .pre}
{:preview: .preview}
{:python: .ph data-hd-programlang='python'}
{:python: data-hd-programlang="python"}
{:route: data-hd-keyref="route"}
{:row-headers: .row-headers}
{:ruby: .ph data-hd-programlang='ruby'}
{:ruby: data-hd-programlang="ruby"}
{:runtime: architecture="runtime"}
{:runtimeIcon: .runtimeIcon}
{:runtimeIconList: .runtimeIconList}
{:runtimeLink: .runtimeLink}
{:runtimeTitle: .runtimeTitle}
{:screen: .screen}
{:script: data-hd-video='script'}
{:service: architecture="service"}
{:service_instance_name: data-hd-keyref="service_instance_name"}
{:service_name: data-hd-keyref="service_name"}
{:shortdesc: .shortdesc}
{:space_name: data-hd-keyref="space_name"}
{:step: data-tutorial-type='step'}
{:subsection: outputclass="subsection"}
{:support: data-reuse='support'}
{:swift: .ph data-hd-programlang='swift'}
{:swift: data-hd-programlang="swift"}
{:table: .aria-labeledby="caption"}
{:term: .term}
{:terraform: .ph data-hd-interface='terraform'}
{:tip: .tip}
{:tooling-url: data-tooling-url-placeholder='tooling-url'}
{:troubleshoot: data-hd-content-type='troubleshoot'}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:tsSymptoms: .tsSymptoms}
{:tutorial: data-hd-content-type='tutorial'}
{:ui: .ph data-hd-interface='ui'}
{:unity: .ph data-hd-programlang='unity'}
{:url: data-credential-placeholder='url'}
{:user_ID: data-hd-keyref="user_ID"}
{:vbnet: .ph data-hd-programlang='vb.net'}
{:video: .video}
  
  
# Why do cluster operations fail due to a broken webhook?
{: #webhooks_update}

**Infrastructure provider**:
  * <img src="../images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Classic
  * <img src="../images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> VPC

{: tsSymptoms}
During a master operation such as updating your cluster version, the cluster had a broken webhook application. Now, master operations cannot complete. You see an error similar to the following:

```
Cannot complete cluster master operations because the cluster has a broken webhook application. For more information, see the troubleshooting docs: 'https://ibm.biz/master_webhook'
```
{: screen}

{: tsCauses}
Your cluster has configurable Kubernetes webhook resources, validating or mutating admission webhooks, that can intercept and modify requests from various services in the cluster to the API server in the cluster master. Because webhooks can change or reject requests, broken webhooks can impact the functionality of the cluster in various ways, such as preventing you from updating the master version or other maintenance operations. For more information, see the [Dynamic Admission Control](https://kubernetes.io/docs/reference/access-authn-authz/extensible-admission-controllers/){: external} in the Kubernetes documentation.

Potential causes for broken webhooks include:
*   The underlying resource that issues the request is missing or unhealthy, such as a Kubernetes service, endpoint, or pod.
*   The webhook is part of an add-on or other plug-in application that did not install correctly or is unhealthy.
*   Your cluster might have a networking connectivity issue that prevents the webhook from communicating with the Kubernetes API server in the cluster master.

{: tsResolve}
Identify and restore the resource that causes the broken webhook.

1.  Create a test pod to get an error that identifies the broken webhook. The error message might have the name of the broken webhook.
    ```
    oc run webhook-test --generator=run-pod/v1 --image pause:latest
    ```
    {: pre}

    In the following example, the webhook is `trust.hooks.securityenforcement.admission.cloud.ibm.com`.
    ```
    Error from server (InternalError): Internal error occurred: failed calling webhook "trust.hooks.securityenforcementadmission.cloud.ibm.com": Post https://ibmcloud-image-enforcement.ibm-system.svc:443/mutating-pods?timeout=30s: dialtcp 172.21.xxx.xxx:443: connect: connection timed out
    ```
    {: screen}
2.  Get the name of the broken webhook.
    *   If the error message has a broken webhook, replace `trust.hooks.securityenforcement.admission.cloud.ibm.com` with the broken webhook that you previously identified.
        ```
        oc get mutatingwebhookconfigurations,validatingwebhookconfigurations -o jsonpath='{.items[?(@.webhooks[*].name=="trust.hooks.securityenforcement.admission.cloud.ibm.com")].metadata.name}{"\n"}'
        ```
        {: pre}

        Example output:
        ```
        image-admission-config
        ```
        {: pre}
    *   If the error does not have a broken webhook, list all the webhooks in your cluster and check their configurations in the following steps.
        ```
        oc get mutatingwebhookconfigurations,validatingwebhookconfigurations
        ```
        {: pre}   
3.  Review the service and location details of the mutating or validating webhook configuration in the `clientConfig` section in the output of the following command. Replace `image-admission-config` with the name that you previously identified. If the webhook exists outside the cluster, contact the cluster owner to check the webhook status.
    ```
    oc get mutatingwebhookconfiguration image-admission-config -o yaml
    ```
    {: pre}

    ```
    oc get validatingwebhookconfigurations image-admission-config -o yaml
    ```
    {: pre}

    Example output:
    ```
      clientConfig:
        caBundle: <redacted>
        service:
            name: <name>
            namespace: <namespace>
            path: /inject
            port: 443
    ```
    {: screen}
4.  **Optional**: Back up the webhooks, especially if you do not know how to reinstall the webhook.
    ```
    oc get mutatingwebhookconfiguration <name> -o yaml > mutatingwebhook-backup.yaml
    ```
    {: pre}

    ```
    oc get validatingwebhookconfiguration <name> -o yaml > validatingwebhook-backup.yaml
    ```
    {: pre}
5.  Check the status of the related service and pods for the webhook.
    1.  Check the service **Type**, **Selector**, and **Endpoint** fields.
        ```
        oc describe service -n <namespace> <service_name>
        ```
        {: pre}
    2.  If the service type is **ClusterIP**, check that the OpenVPN pod is in a **Running** status so that the webhook can connect securely to the Kubernetes API in the cluster master. If the pod is not healthy, check the pod events, logs, worker node health, and other components to troubleshoot. For more information, see [Debugging app deployments](/docs/openshift?topic=openshift-debug_apps).
        ```
        oc describe pods -n kube-system -l app=vpn
        ```
        {: pre}
    3.  If the service does not have an endpoint, check the health of the backing resources, such as a deployment or pod. If the resource is not healthy, check the pod events, logs, worker node health, and other components to troubleshoot. For more information, see [Debugging app deployments](/docs/openshift?topic=openshift-debug_apps).
        ```
        oc get all -n my-service-namespace -l <key=value>
        ```
        {: pre}
    4.  If the service does not have any backing resources, or if troubleshooting the pods does not resolve the issue, remove the webhook.
        ```
        oc delete mutatingwebhook <name>
        ```
        {: pre}
6.  Retry the cluster master operation, such as updating the cluster.
7.  If you still see the error, you might have worker node or network connectivity issues.
    *   [Worker node troubleshooting](/docs/openshift?topic=openshift-debug_worker_nodes.
    *   Make sure that the webhook can connect to the Kubernetes API server in the cluster master. For example, if you use Calico network policies, security groups, or some other type of firewall, set up your [classic](/docs/openshift?topic=openshift-firewall) or [VPC](/docs/openshift?topic=openshift-vpc-firewall) cluster with the appropriate access.
    *   If the webhook is managed by an add-on that you installed, uninstall the add-on. Common add-ons that cause webhook issues include the following:
        * [Portieris](/docs/openshift?topic=openshift-images#portieris-image-sec)
8.  Re-create the webhook or reinstall the add-on.
