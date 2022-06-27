---

copyright: 
  years: 2014, 2022
lastupdated: "2022-06-27"

keywords: openshift, block storage, pod identity, trusted profiles

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}

# Setting up trusted profiles for the {{site.data.keyword.block_storage_is_short}} add-on
{: #storage-block-vpc-trusted-profiles.md}

You can use trusted profiles to limit the access that running pods in your cluster have to other resources in your account or cluster. For more information about trusted profiles, see [Creating trusted profiles](/docs/account?topic=account-create-trusted-profile).
{: shortdesc}

Supported infrastructure provider
:   ![VPC](../icons/vpc.svg "VPC") VPC

## Enabling the {{site.data.keyword.block_storage_is_short}} add-on
{: #vpc-addon-enable-trusted}

1. [Log in to your account. If applicable, target the appropriate resource group. Set the context for your cluster.](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure)

1. Get the version number of the `vpc-block-csi-driver` add-on that is installed in your cluster.
    ```sh
    ibmcloud oc cluster addon ls --cluster CLUSTER
    ```
    {: pre}


1. If you have an add-on version earlier than 4.4 of the {{site.data.keyword.block_storage_is_short}} add-on installed in your cluster, you must first disable the add-on and then enable version 4.4 or later. 
    ```sh
    ibmcloud oc cluster addon disable vpc-block-csi-driver  --cluster CLUSTER-ID
    ```
    {: pre}

    ```sh
    ibmcloud oc cluster addon enable vpc-block-csi-driver --version 4.4 --cluster CLUSTER-ID
    ```
    {: pre}

    Example output.
    ```sh
    Enabling add-on vpc-block-csi-driver(4.4) for cluster CLUSTER-ID
    The add-on might take several minutes to deploy and become ready for use.
    ```
    {: screen}

1. Verify that the add-on state is `normal` and the status is `ready`.
    ```sh
    ibmcloud oc cluster addon ls --cluster CLUSTER-ID
    ```
    {: pre}

    ```sh
    Name                   Version                     Health State   Health Status   
    vpc-block-csi-driver   4.4 (4.3 default)   normal         Addon Ready. For more info: http://ibm.biz/addon-state (H1500)   
    ```
    {: screen}

    
1. Verify that the driver pods are deployed and the status is `Running`.
    ```sh
    kubectl get pods -n kube-system | grep block
    ```
    {: pre}
    
    Example output
    ```sh                    
    ibm-vpc-block-csi-controller-0                        7/7     Running   0          77s
    ibm-vpc-block-csi-node-56c85                          4/4     Running   0          77s
    ibm-vpc-block-csi-node-87j2t                          4/4     Running   0          77s
    ibm-vpc-block-csi-node-cmh2h                          4/4     Running   0          77s
    ```
    {: screen}


## Setting up trusted profiles
{: #vpc-block-setup-trusted}

1. Follow the steps to [create a trusted profile](/docs/account?topic=account-create-trusted-profile&interface=ui). In the **Conditions** for the profile, be sure to specify the following access.

    * Allow access when **Service account** equals `ibm-vpc-block-controller-sa`.
    * Allow acccess when **Namespace** equals `kube-system`.

    You can create the trusted profile for specific clusters or for all current and future clusters.
    {: note}
    
1. After you create your trusted profile, copy the ID from the **Trusted profiles** page in the console.

1. Create a secret in your cluster that contains the credentials for the trusted profile. You can create the secret by using the ID or API key for the trusted profile. Save the following YAML to a file called `ibm-cloud-credentials.yaml`. In the `ibm-credentials.env:` field, enter the base64 encoded API key or the ID of trusted profile.

    ```yaml
    apiVersion: v1
    data:
      ibm-credentials.env: # Trusted profile ID
    kind: Secret
    metadata:
      name: ibm-cloud-credentials
      namespace: kube-system
    type: Opaque
    ```
    {: codeblock}

1. [Log in to your account. If applicable, target the appropriate resource group. Set the context for your cluster.](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure)

1. Create the secret in your cluster.
    
    ```sh
    kubectl apply -f ibm-cloud-credentials.yaml
    ```
    {: pre}

1. Restart the driver pods by disabling and re-enabling the add-on.
    1. Disable the add-on. 
        ```sh
        ibmcloud oc cluster addon disable vpc-block-csi-driver
        ```
        {: pre}

    1. Re-enable the add-on.
        ```sh
        ibmcloud oc cluster addon enable vpc-block-csi-driver --cluster CLUSTER --version VERSION
        ```
        {: pre}
    
    
