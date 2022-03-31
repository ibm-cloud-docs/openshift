---

copyright: 
  years: 2014, 2022
lastupdated: "2022-03-30"

keywords: openshift

subcollection: openshift

content-type: troubleshoot

---


{{site.data.keyword.attribute-definition-list}}


# What permissions do I need to manage storage and create PVCs?
{: #missing_permissions}
{: support}


**Infrastructure provider**:
* ![Classic infrastructure provider icon.](images/icon-classic-2.svg) Classic
* ![VPC infrastructure provider icon.](images/icon-vpc-2.svg) VPC


When you create a PVC, the PVC remains pending. When you run `oc describe pvc <pvc_name>`, you see an error message similar to the following:
{: tsSymptoms}

```sh
User doesn't have permissions to create or manage Storage
```
{: screen}


The IAM API key or the IBM Cloud infrastructure API key that is stored in the `storage-secret-store` Kubernetes secret of your cluster  does not have all the required permissions to provision persistent storage.
{: tsCauses}


1. Retrieve the IAM key or IBM Cloud infrastructure API key that is stored in the `storage-secret-store` Kubernetes secret of your cluster and verify that the correct API key is used.
{: tsResolve}

    ```sh
    oc get secret storage-secret-store -n kube-system -o yaml | grep slclient.toml: | awk '{print $2}' | base64 --decode
    ```
    {: pre}

    Example output

    ```sh
    [Bluemix]
    iam_url = "https://iam.bluemix.net"
    iam_client_id = "bx"
    iam_client_secret = "bx"
    iam_api_key = "<iam_api_key>"
    refresh_token = ""
    pay_tier = "paid"
    containers_api_route = "https://us-south.containers.bluemix.net"

    [Softlayer]
    encryption = true
    softlayer_username = ""
    softlayer_api_key = ""
    softlayer_endpoint_url = "https://api.softlayer.com/rest/v3"
    softlayer_iam_endpoint_url = "https://api.softlayer.com/mobile/v3"
    softlayer_datacenter = "dal10"
    ```
    {: screen}

    The IAM API key is listed in the `Bluemix.iam_api_key` section of your CLI output. If the `Softlayer.softlayer_api_key` is empty at the same time, then the IAM API key is used to determine your infrastructure permissions. The IAM API key is automatically set by the user who runs the first action that requires the IAM **Administrator** platform access role in a resource group and region. If a different API key is set in `Softlayer.softlayer_api_key`, then this key takes precedence over the IAM API key. The `Softlayer.softlayer_api_key` is set when a cluster admin runs the `ibmcloud oc credentials-set` command.

2. If you want to change the credentials, update the API key that is used.
    1. [Log in to your account. If applicable, target the appropriate resource group. Set the context for your cluster.](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure)
    2. To update the IAM API key, use the `ibmcloud oc api-key reset` [command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_api_key_reset). To update the IBM Cloud infrastructure key, use the `ibmcloud oc credential set` [command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_credentials_set).
    3. Wait about 10 - 15 minutes for the `storage-secret-store` Kubernetes secret to update, then verify that the key is updated.
        ```sh
        oc get secret storage-secret-store -n kube-system -o yaml | grep slclient.toml: | awk '{print $2}' | base64 --decode
        ```
        {: pre}

3. If the API key is correct, verify that the key has the correct permission to provision persistent storage.
    1. Contact the account owner to verify the permission of the API key.
    2. As the account owner, select **Manage** > **Access (IAM)** from the navigation in the {{site.data.keyword.cloud_notm}} console.
    3. Select **Users** and find the user whose API key you want to use.
    4. From the actions menu, select **Manage user details**.
    5. Go to the **Classic infrastructure** tab.
    6. Expand the **Account** category and verify that the **Add/ Upgrade Storage (Storage Layer)** permission is assigned.
    7. Expand the **Services** category and verify that the **Storage Manage** permission is assigned.
4. Remove the PVC that failed.
    ```sh
    oc delete pvc <pvc_name>
    ```
    {: pre}

5. Re-create the PVC.
    ```sh
    oc apply -f pvc.yaml
    ```
    {: pre}




