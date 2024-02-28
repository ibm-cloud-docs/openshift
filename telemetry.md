---

copyright: 
  years: 2024, 2024
lastupdated: "2024-02-28"


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



1. From the {{site.data.keyword.redhat_openshift_notm}} console, download a JSON file of the pull secret that allows remote health reporting.
    1. Log into the [{{site.data.keyword.redhat_openshift_notm}} console](https://console.redhat.com/openshift){: external}.
    2. Navigate to **Tokens > Pull Secret** and download the pull secret as a JSON file.

2. Get your current pull secret and store it in a JSON file. Consider naming the JSON file something like `pull-secret-original.json`.
    ```sh
    ibmcloud oc get secrets pull-secret -n openshift-config -o template='{{index .data ".dockerconfigjson"}}' | base64 -d > pull-secret-original.json
    ```
    {: pre}

3. [Access your cluster in the CLI](/docs/openshift?topic=openshift-access_cluster). 

4. Append the downloaded JSON file to your existing pull secret and apply the changes to the cluster.
    ```sh
    ibmcloud oc set data secret/pull-secret -n openshift-config --from-file=.dockerconfigjson=./<downloaded-pull-secret-name>.json
    ```
    {: pre}

5. Verify that the existing pull secret is updated. Look for the `auths` section that contains the access token.
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

6. For classic infrastructure, [repload all worker nodes in your cluster](/https://cloud.ibm.com/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_reload). For VPC infrastucture, [replace all worker nodes in your cluster](/docs/containers?topic=containers-kubernetes-service-cli#cli_worker_replace).

7. To verify that Telemetry is enabled in the cluster, open the [{{site.data.keyword.redhat_openshift_notm}} console](https://console.redhat.com/openshift){: external} and navigate to the **Clusters** page. If your cluster is listed, Telemetry is enabled. 


