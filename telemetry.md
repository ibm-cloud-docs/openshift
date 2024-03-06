---

copyright: 
  years: 2024, 2024
lastupdated: "2024-03-06"


keywords: telemetry, remote health, remote monitoring, cluster data, health data

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}

# Telemetry for remote health monitoring
{: #telemetry}

Telemetry is a remote health monitoring feature that collects anonymized aggregated data about your cluster, such as the health of your components and the number and types of resources in use. If you have a public cluster that runs version 4.14 or later and was provisioned on or after 28 Feb 2024, you can elect to have your own Telemetry data visible in the Red Hat Hybrid Console under your Red Hat account for your use. For more information on Telemetry, such as the type of data collected, see [About Telemetry](https://access.redhat.com/documentation/en-us/openshift_container_platform/4.1/html/telemetry/about-telemetry){: external} in the {{site.data.keyword.redhat_openshift_notm}} documentation. 
{: shortdesc}


## Enabling Telemetry
{: #telemetry_enable}

To enable Telemetry, update your pull secret by adding your OpenShift access token to allow remote health reporting.  Note that Telemetry can only be enabled for public clusters that run version 4.14 or later and were provisioned on or after 28 Feb 2024. 



1. Log into the [{{site.data.keyword.redhat_openshift_notm}} console](https://console.redhat.com/openshift){: external}.
1. Navigate to **Downloads** > **Tokens > Pull Secret** and download the pull secret as a JSON file.

1. Get your current pull secret and store it in a JSON file. Consider naming the JSON file something like `pull-secret-original.json`.
    ```sh
    oc get secrets pull-secret -n openshift-config -o template='{{index .data ".dockerconfigjson"}}' | base64 -d > pull-secret-original.json
    ```
    {: pre}

1. [Access your cluster in the CLI](/docs/openshift?topic=openshift-access_cluster). 

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

1. For classic infrastructure, [reload all worker nodes in your cluster](/https://cloud.ibm.com/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_reload). For VPC infrastucture, [replace all worker nodes in your cluster](/docs/containers?topic=containers-kubernetes-service-cli#cli_worker_replace).

1. To verify that Telemetry is enabled in the cluster, open the [{{site.data.keyword.redhat_openshift_notm}} console](https://console.redhat.com/openshift){: external} and navigate to the **Clusters** page. If your cluster is listed, Telemetry is enabled.


## Disabling Telemetry
{: #oc_disable_telemetry_reports}

You can disable of Telemetry only in cluster versions 4.13 and earlier or cluster versions 4.14 that were created before 28 February 2024.

You might want to disable this remote health reporting to comply with privacy laws, organizational standards, or data governance practices. To disable, you must modify the global configuration for the cluster and reload all the worker nodes.

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

2. Follow the {{site.data.keyword.redhat_openshift_notm}} instructions to [update the global pull secret in the cluster to disable remote health reporting](https://docs.openshift.com/container-platform/4.13/support/remote_health_monitoring/opting-out-of-remote-health-reporting.html){: external}.
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


