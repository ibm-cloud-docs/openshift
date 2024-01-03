---

copyright: 
  years: 2023, 2024
lastupdated: "2024-01-03"


keywords: kubernetes, help, api key, security

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}


# How do I rotate the cluster API key in the event of a leak?
{: #ts-troubleshoot-api-key-leak}
{: support}

Your cluster security has been compromised due to an exposed API key.
{: tsSymptoms}

There can be many reasons why or how an API key leak occurs. After you rotate the key, plan to complete a thorough root cause analysis.
{: tsCauses}

To resolve the issue, rotate your cluster credentials.
{: tsResolve}

1. Use your cluster ID to find the IAM service ID for your cluster. Make a note of the service ID that begins with `cluster-CLUSTERID`.

    ```sh
    ibmcloud iam service-ids | grep CLUSTER-ID
    ```
    {: pre}

    Example output
    ```sh
    ServiceId-bc8cebd4-491e-4582-9a75-e93938004f79     cluster-ck0a5faw0bm3lnln95lg   ... ...
    ```
    {: pre}

1. Find the API keys associated with the service ID that you found in the previous step. In the following example, the API key used for {{site.data.keyword.registryshort}} is rotated.
    ```sh
    ibmcloud iam service-api-keys ServiceId-xxx-xxx
    Getting all API keys of xxx...
    OK
    ID                                            Name                           Description                                                          Created At              Last Updated            Locked
    ApiKey-79ed0b99-1ac9-4676-96be-8cbaa485fa74   cluster-ck9blho20n01rtorhqhg   API key created for cluster access to IBM Cloud Container Registry   2023-09-26T11:04+0000   2023-09-26T11:04+0000   false
    ```
    {: pre}

1. To generate a new key, delete the service API key.
    ```sh
    ibmcloud iam service-api-key-delete SERVICE_API_KEY_ID_OR_NAME SERVICE_ID_OR_NAME
    ```
    {: pre}

1. Run the **`ibmcloud ks cluster pull-secret apply`** [command](/docs/containers?topic=containers-kubernetes-service-cli#cs_cluster_pull_secret_apply). This command generates a new API key and updates the `all-icr-io` secret in the default namespace.
    ```sh
    ibmcloud ks cluster pull-secret apply --cluster CLUSTER
    ```
    {: pre}

1. Note that the new API key is generated immediately. However, the updated secret might take several minutes to populate.




