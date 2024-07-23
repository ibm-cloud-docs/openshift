---

copyright:
  years: 2023, 2024
lastupdated: "2024-07-23"


keywords: openshift, satellite, distributed cloud, on-prem, hybrid, images,

subcollection: openshift
content-type: tutorial
services: containers, cloud-object-storage
completion-time: 1h

---


{{site.data.keyword.attribute-definition-list}}

# Setting up the internal image registry for {{site.data.keyword.satelliteshort}} clusters
{: #satellite-clusters-registry}
{: toc-content-type="tutorial"}
{: toc-services="containers, cloud-object-storage"}
{: toc-completion-time="1h"}

[{{site.data.keyword.satelliteshort}}]{: tag-satellite}


By default, the internal registry does not run in your {{site.data.keyword.satelliteshort}} cluster because no backing storage is set up for the internal registry. Complete the following tutorial to configure the internal image registry in your {{site.data.keyword.satelliteshort}} cluster with {{site.data.keyword.cos_full_notm}} as the backing storage.
{: shortdesc}


This tutorial covers setting up the image registry by using {{site.data.keyword.cos_full_notm}}. However, you can also use non-persistent storage on the worker node. For more information, see [Storing images in the worker node empty directory](/docs/openshift?topic=openshift-registry#emptydir_internal_registry).
{: note}


## Create an {{site.data.keyword.cos_full_notm}} instance that meets the requirements
{: #sat-registry-cos-instance}
{: step}

1. In the {{site.data.keyword.cloud_notm}} console, navigate to the **Resources** menu and list your storage instances. 
2. Identify your {{site.data.keyword.cos_short}} instances and find the **Location** column. If an instance was created in {{site.data.keyword.cloud_notm}}, its location is listed as **Global**.
3. If you do not have a Global instance that meets the requirements, follow the steps to create one.
    1. From the {{site.data.keyword.cos_full_notm}}, click **Create Instance**.
    2. Under **Choose an Infrastructure**, select the **{{site.data.keyword.cloud_notm}}** option. 
    3. Select a pricing plan and a service name.
    4. Choose the resource group where your {{site.data.keyword.satelliteshort}} components are stored.
    5. Click **Create**. Note that it might take several minutes for your instance to provision.

## Create a bucket to use for your image registry
{: #sat-registry-bucket}
{: step}

Create a bucket to use when you set up your image registry. Your bucket must be configured with regional resiliency. For more information about creating a bucket, see [Setting up {{site.data.keyword.cos_full_notm}}](/docs/openshift?topic=openshift-storage-cos-understand).

1. Click on your {{site.data.keyword.cos_short}} instance.
2. Click **Create a bucket**.
3. Select the option to **Customize your bucket**.
4. Under **Resiliency**, select **Regional**.
5. From the **Location** drop down menu, choose the region that is closest to where your location is managed from. For example, if your location is managed from `wdc` (Washington, DC), choose the `us-east` region. To check where a {{site.data.keyword.satelliteshort}} location is managed from, run `ibmcloud sat location ls` in the CLI.
6. Under **Storage class**, select **Standard**.
7. Configure the remaining categories to your preferences.
8. Click **Create bucket**.
3. Create service credentials that enable your cluster to communicate with your {{site.data.keyword.cos_short}} instance.
1. In the navigation pane, click **Service credentials**, then click **New credential**.
2. Enter a name for the new credential.
3. From the drop down menu, choose the **Writer** role. 
4. Click **Advanced options**, then select the option to **Include HMAC Credential**.
5. Click **Add**.
6. In the **Service Credentials** table, expand your new credential. Note the `access_key_id` and the `secret_access_key_id`. Do not share these credentials with anyone. 
    Example credentials to save. 
    ```sh
    "cos_hmac_keys": {
        "access_key_id": "1111111a1111111a11aa1a111111111a11aa1a111a11a1a1",
        "secret_access_key": "222222b222222b22bb2b22222222b22bb2b222b22b2b2"
    }
    ```
    {: screen}

## Create a secret that contains your COS service credentials
{: #sat-registry-secret}
{: step}
        
In the CLI, create a secret with the service credentials you created and saved.

1. [Log in to your account. If applicable, target the appropriate resource group. Set the context for your cluster.](/docs/containers?topic=containers-access_cluster)
2. Create the secret.
    ```sh
    oc create secret generic image-registry-private-configuration-user --from-literal=REGISTRY_STORAGE_S3_ACCESSKEY=<access_key_id> --from-literal=REGISTRY_STORAGE_S3_SECRETKEY=<secret_access_key> --namespace openshift-image-registry
    ```
    {: pre}

## Update the {{site.data.keyword.redhat_openshift_notm}} Registry operator CRDs
{: #sat-registry-crds}
{: step}
        
1. Change the management state of the {{site.data.keyword.redhat_openshift_notm}} Register operator.
    ```sh
    oc patch configs.imageregistry.operator.openshift.io cluster --type merge --patch '{"spec":{"managementState":"Managed"}}'
    ```
    {: pre}
    
1. Edit the configuration storage attributes to store images in your {{site.data.keyword.cos_short}} bucket.
    1. Find and save your {{site.data.keyword.satelliteshort}} location's regional link endpoint. In the output, the endpoint is listed under the **Address** column.
        ```sh
        ibmcloud sat endpoint ls --location <location_name> | grep satellite-cosRegional
        ```
        {: pre}

        Example output
        ```sh
        ID                           Name                                              Destination Type   Address       
        cavvku1p1h1gcfgk1kn1_uwokw   satellite-cosRegional-cavvku1p1h1gcfgk1kn1        cloud              TLS   i11aa11a1a1a11a11-1a11a1aaa1a1a1a1a-c000.us-east.satellite.appdomian.cloud:11111 
        ```
        {: pre}
        
    1. Open the file editor in the CLI.
        ```sh
        oc edit configs.imageregistry.operator.openshift.io/cluster
        ```
        {: pre}
        
    1. Find the following section to edit. 
        ```yaml
        storage:
            emptyDir: {}
            managementState: Managed
        storageManaged: true
        ```
        {: codeblock}
        
    1. Replace `emptyDir: {}` with your bucket information and location endpoints.
        ```yaml
        s3:
          bucket: <bucket_name>
          region: <bucket_region>
          regionEndpoint: <location_link_endpoint>
          virtualHostedStyle: false
        ```
        {: codeblock}
        
        Example section after adding the bucket and location information.
        ```yaml
          storage:
            managementState: Managed
            s3:
              bucket: my_bucket
              region: us-east
              regionEndpoint: https://i11aa11a1a1a11a11-1a11a1aaa1a1a1a1a-c000.us-east.satellite.appdomian.cloud:11111
              virtualHostedStyle: false
          storageManaged: true
        ```
        {: codeblock}
        
    1. Save and apply the changes.

## Verify your changes
{: #sat-registry-verify}

Verify that the image registry was configured by checking for a pod that begins with `image-registry-` in the `openshift-image-registry` namespace. 

1. Run the following command.
    ```sh
    oc get pod -n openshift-image-registry
    ```
    {: pre}

1. Review the output and confirm that the registry pod is `Running`.

    Example output
    ```sh
    NAME                                               READY   STATUS      RESTARTS      AGE
    image-registry-63p54b8add-vkjju                    1/1      Running      0              16m
    ```
    {: screen}

