---

copyright: 
  years: 2024, 2024
lastupdated: "2024-07-23"


keywords: telemetry, remote health, remote monitoring, cluster data, health data

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}

# Telemetry for remote health monitoring
{: #telemetry}

Telemetry is a remote health monitoring feature that collects anonymized aggregated data about your cluster, such as the health of your components and the number and types of resources in use. If you have a public cluster that runs version 4.14 or later and was provisioned on or after 28 Feb 2024, you can elect to have your own Telemetry data visible in the Red Hat Hybrid Console under your Red Hat account for your use. For more information on Telemetry, such as the type of data collected, see [About Telemetry](https://docs.redhat.com/en/documentation/openshift_container_platform/4.1/html/telemetry/about-telemetry){: external} in the {{site.data.keyword.redhat_openshift_notm}} documentation. 
{: shortdesc}


## Enabling Telemetry
{: #telemetry_enable}

To enable Telemetry, update your pull secret by adding your OpenShift access token to allow remote health reporting. The exact steps to follow depend on your cluster version and when the cluster was created. If you are not sure if your cluster has Telemetry enabled already, see [Checking if Telemetry is enabled for a cluster](#telemetry_check).


**For version 4.13 or earlier, or version 4.14 clusters that were created before 29 Feb 2024**: If your cluster was created before 29 Feb 2024, [open a support ticket](/docs/openshift?topic=openshift-allowlist-request) and indicate that you want to enable Telemetry in your cluster. When the ticket is resolved, continue with the following steps. 

**For version 4.14 clusters created on or after 29 Feb 2024**: Continue with the following steps.

1. Log into the [{{site.data.keyword.redhat_openshift_notm}} console](https://console.redhat.com/openshift){: external}.
1. Navigate to **Downloads** > **Tokens > Pull Secret** and download the pull secret as a JSON file.

1. [Access your cluster in the CLI](/docs/openshift?topic=openshift-access_cluster).

1. Get your current pull secret and store it in a JSON file. Consider naming the JSON file something like `pull-secret-original.json`.
    ```sh
    oc get secrets pull-secret -n openshift-config -o template='{{index .data ".dockerconfigjson"}}' | base64 -d > pull-secret-original.json
    ```
    {: pre}

1. Append the downloaded JSON file to your existing pull secret and apply the changes to the cluster.
    ```sh
    oc set data secret/pull-secret -n openshift-config --from-file=.dockerconfigjson=./<downloaded-pull-secret-name>.json
    ```
    {: pre}

1. Verify that the existing pull secret is updated. Look for the `auths` section that contains the access token.
    ```sh
    oc get secret pull-secret -n openshift-config --output="jsonpath={.data.\.dockerconfigjson}" | base64 --decode
    ```
    {: pre}

    Example `auths` section.

    ```yaml
        {
    "auths": {
        "cloud.openshift.com": {
        "auth": "<your_token>",
        "email": "<email_address>"
        }
    }
    }
    ```
    {: codeblock}

1. For classic infrastructure, [reload all worker nodes in your cluster](/https://cloud.ibm.com/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_reload). For VPC infrastructure, [replace all worker nodes in your cluster](/docs/containers?topic=containers-kubernetes-service-cli#cli_worker_replace).

1. Open the [{{site.data.keyword.redhat_openshift_notm}} console](https://console.redhat.com/openshift){: external} and navigate to the **Clusters** page. Telemetry is enabled when your cluster type is `RHOIC`. Note that it might take a few minutes for the changes to reflect in the console. If you want to verify Telemetry enablement in the CLI, see [Checking if Telemetry is enabled for a cluster](#telemetry_check).


## Disabling Telemetry
{: #oc_disable_telemetry_reports}

You might want to disable this remote health reporting to comply with privacy laws, organizational standards, or data governance practices. To disable Telemetry, modify the global configuration for the cluster and reload all the worker nodes.

1. Check that the telemetry reporting pod runs in your cluster.
    ```sh
    oc get pods -n openshift-monitoring
    ```
    {: pre}

    Example output

    ```sh
    NAME                              READY   STATUS      RESTARTS   AGE
    telemeter-client-7cfd7cb85-lm9dt  3/3     Running     0          4d13h
    ...
    ```
    {: screen}

2. Follow the {{site.data.keyword.redhat_openshift_notm}} instructions to [update the global pull secret in the cluster to disable remote health reporting](https://docs.openshift.com/container-platform/4.15/support/remote_health_monitoring/opting-out-of-remote-health-reporting.html){: external}.
3. To pick up the global configuration changes, reload all the worker nodes in your cluster.
    1. Note the **ID** of the worker nodes in your cluster.
        ```sh
        ibmcloud oc worker ls -c <cluster_name_or_ID>
        ```
        {: pre}

    2. Reload each worker node. You can reload multiple worker nodes by including multiple `-w` options, but make sure to leave enough worker nodes running at the same time for your apps to avoid an outage.
        ```sh
        ibmcloud oc worker reload -c <cluster_name_or_ID> -w <workerID_1> -w <workerID_2>
        ```
        {: pre}

4. After the worker nodes are back in a healthy state, verify that the telemetry reporting pod no longer runs in your cluster.
    ```sh
    oc get pods -n openshift-monitoring
    ```
    {: pre}


## Checking if Telemetry is enabled for a cluster
{: #telemetry_check}

If you are not sure whether Telemetry is already enabled for a cluster, follow these steps to see if the Telemetry configuration is present in your cluster pull secret. If the configuration is present in the pull secret, Telemetry is enabled for the cluster.


1. In the CLI, set the context for your cluster and include the `--admin` option.

    ```sh
    ibmcloud oc cluster config -c CLUSTER-ID --admin
    ```
    {: pre}

2. Get the pull secret located in the `openshift-config` namespace. Note that this command extracts the data from the secret, base64 decodes it, and then outputs the info into a file. 
    ```sh
    oc get secrets pull-secret -n openshift-config -o template='{{index .data ".dockerconfigjson"}}' | base64 -d > pull-secret.json
    ```
    {: pre}

3. View the contents of the file. In the pull secret, look for the `cloud.openshift.com` authorization. If it exists, Telemetry is enabled on the cluster.

    ```sh
    cat pull-secret.json 
    ```
    {: pre}

    Example authorization in pull secret file. 

    ```yaml
    "auths": {
        "cloud.openshift.com": {
            "auth": "xyz123...",
            "email": "user@us.ibm.com"
        }
    ```
    {: screen}

