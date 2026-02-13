---

copyright:
  years: 2025, 2026
lastupdated: "2026-02-13"


keywords: openshift, acm, advanced cluster management, manage cluster, management, addon, add-on, acm addon

subcollection: openshift

---


{{site.data.keyword.attribute-definition-list}}

# Setting up the Advanced Cluster Management add-on (select regions only)
{: #acm}

The Advanced Cluster Management (ACM) add-on provides a simplified way for customers to manage monitoring, workload placement, and security policies across multiple clusters.
{: shortdesc}

The Advanced Cluster Management add-on is available for select regions only.
{: important}

Installing ACM from OperatorHub is not supported for IBM Cloud clusters. To install ACM, follow the instructions on this page. 
{: important}

The cluster that you install ACM on is the **hub cluster**. During or after the installation, you can specify multiple **managed clusters** to manage with ACM.

## Before you begin
{: #before}

Review the following prerequisite steps and information before you install the ACM add-on.

1. Review the [ACM plan types](/docs/openshift?topic=openshift-acm-about&interface=ui#overviews) and decide which plan you want to use. Note that for ACM for Virtualization, it is recommended that your managed clusters run bare metal worker nodes. 
1. Make sure your clusters meet the following requirements.
    - Your **hub cluster** must be a VPC cluster with at least **3** worker nodes that run **RHCOS** and a minimum of **6 VCPU and 64GB RAM**. For high availability, make sure your cluster has at least one worker node per zone across 3 zones.
    - Each **managed cluster** must have at least **3** worker nodes that run **RHCOS** and a minimum of **6 VCPU and 64GB RAM**. 
    - In addition, if you want to use the **ACM for Virtualization** plan, it is recommended that you use **bare metal worker nodes**. For the **ACM for Kubernetes** plan, managed clusters can run either **bare metal nodes** or **VSIs**.
1. Review the [operators that are automatically installed](#auto-op}) by the ACM add-on and the [optional operators](#optional-op) that you can install as enhancements.
1. You must have the [Administrator platform access role and the Manager service access role](/docs/openshift?topic=openshift-iam-platform-access-roles) for the cluster in IBM Cloud Kubernetes Service. 
1. You must have a VPC cluster with at least 3 worker nodes. Each worker node must have a minimum of 4 CPUs and 16GB RAM. For high availability, make sure your cluster has at least one worker node per zone across 3 zones. 
1. [Create a trusted profile on your cluster to use for ACM](#trusted-prof).
1. For each cluster you want to manage with ACM, you must create a secret on the hub cluster with the managed cluster's access token and server URL. This step can be completed before or after installation.  See [Preparing secrets for ACM](#prep-secret). 
1. [Install or update the CLI](/docs/openshift?topic=openshift-cli-install).

## Create a trusted profile for ACM
{: #trust-prof}

Follow the steps to create a trusted profile to use for ACM.

1. Follow the steps to [create a trusted profile](/docs/account?topic=account-create-trusted-profile&interface=ui). In the **Conditions** for the profile, be sure to specify the following access.
    * Allow access when **Namespace** equals `kube-system`
    * Satellite Service Roles - Satellite Link Administrator, Reader
    * Kubernetes Service Roles - Manager, Editor
    * Billing Service Roles - Reader, Operator

1. After you create your trusted profile, copy the ID from the **Trusted profiles** page in the console.

1. Create the following secret by using the ID for the trusted profile. Save the following text and enter your credentials. You can follow the steps to create the secret manually or you can use the shell script to [automatically create the secret in your cluster](#odf-secret-create-truted-profile).

    ```txt
    IBMCLOUD_AUTHTYPE=pod-identity
    IBMCLOUD_PROFILEID=<TRUSTED-PROFILE-ID>
    ```
    {: codeblock}

1. Create a secret in your cluster that contains the credentials for the trusted profile. Save the following YAML to a file called `ibm-cloud-credentials.yaml`. In the `ibm-credentials.env:` field, enter the ID of trusted profile.

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

1. [Log in to your account. If applicable, target the appropriate resource group. Set the context for your cluster.](/docs/containers?topic=containers-access_cluster)

1. Create the secret in your cluster.
    
    ```sh
    kubectl apply -f ibm-cloud-credentials.yaml
    ```
    {: pre}

## Preparing secrets for ACM
{: #prep-secret}

For each cluster that you want to manage with ACM, you must create a secret on the hub cluster that includes the managed cluster's access token and server URL. 

If you want to import managed clusters during the ACM add-on installation process, complete these steps before you begin the installation. If you choose to create the secrets and import managed clusters after the add-on is installed on the hub cluster, you can do so by completing [additional steps](#after) with the CLI.  
{: important}

Complete the following steps for each cluster that you want to manage.

1. On the cluster that you want to manage with ACM, run the command to find the server URL. In the output, find and note the **Master URL** value. This is the server URL to reference in the secret. You also use this URL in the following steps. 

    ```sh
    ibmcloud oc cluster get -c <cluster_name_or_ID>
    ```
    {: pre}

    Example output.

    ```sh
    NAME:                           mycluster
    ID:                             1234567
    State:                          normal
    Created:                        2025-01-22T19:22:16+0000
    Location:                       dal10
    Master URL:                     https://c100-e.<region>.containers.cloud.ibm.com:<port>
    ...
    ```
    {: screen}

2. Get the token endpoint of the Red Hat OpenShift oauth server. Replace `<master_URL>` with the URL found in the previous step. Note that the value in the output is **not** the access token. 

    ```sh
    curl <master_URL>/.well-known/oauth-authorization-server | jq -r .token_endpoint
    ```
    {: pre}

    Example output.

    ```sh
    <token_endpoint>/oauth/token
    ```
    {: screen}


3. Log in to the cluster with the endpoint that you previously retrieved. Replace `<URL>` with the `<token_endpoint>` of the oauth server that you found in the previous step. In the output, find the `<access_token>` contained in the **Location response**. This is the access token to include in the secret. 

    Example curl request:

    ```sh
    curl -u 'apikey:<API_key>' -H "X-CSRF-Token: a" '<URL>/oauth/authorize?client_id=openshift-challenging-client&response_type=token' -vvv
    ```
    {: pre}

    Example output. The <access_token> is included in the Location response string. 

    ```sh
    < HTTP/1.1 302 Found
    < Cache-Control: no-cache, no-store, max-age=0, must-revalidate
    < Cache-Control: no-cache, no-store, max-age=0, must-revalidate
    < Expires: 0
    < Expires: Fri, 01 Jan 2030 00:00:00 GMT
    < Location: <token_endpoint>/oauth/token/implicit#access_token=<access_token>&expires_in=86400&scope=user%3Afull&token_type=Bearer
    ...
    ```
    {: screen}


4. On the hub cluster, create a secret that contains the cluster access token and server URL. For information on creating secrets, see [Working with secrets](https://kubernetes.io/docs/concepts/configuration/secret/){: external} in the Kubernetes documentation. 

    Example secret. 

    ```json
    apiVersion: v1
    kind: Secret
    metadata:
      name: <secret_name>
      namespace: <secret_namespace>  # The namespace that the secret is to be created in
    type: Opaque
    stringData:
      token: <access_token>
      server: <server_url>
    ```
    {: pre}



## Installing ACM from the UI
{: #install-ui}
{: ui}

Use the UI to install the ACM add-on and ACM operator to the hub cluster.

1. If you want to import one or more managed clusters to manage with ACM during the installation process, follow the steps in [Preparing secrets for ACM](#prep-secret) to create the required secret on the hub cluster. Save the secret name and namespace. You can also skip this step for now and complete it after the installation process, but additional CLI steps will be required. 

1. Log in to the {{site.data.keyword.cloud_notm}} console and navigate to your [Clusters](https://cloud.ibm.com/containers/cluster-management/clusters){: external} page. Click the cluster you want to install ACM on. 

1. From the cluster details page, find the **Add-ons** section. 

1. Under **Available to install**, find the **Red Hat Advanced Cluster Management** option and click **Install**.

1. On the installation page, select the ACM add-on version to install.

1. Choose which ACM plan you want to use: **ACM for Virtualization** or **ACM for Kubernetes**. You can upgrade from the **ACM for Virtualization** plan to **ACM for Kubernetes** plan at anytime, but note that the upgrade is permanent and cannot be reversed. 

1. Choose how you want to import managed clusters. To import clusters after the add-on is installed, select **Import from CLI**. If you created the required secrets on the hub cluster and you want to import managed clusters now, select **Import now**. 

    You can only use the UI to import managed clusters during the installation process. Once the ACM add-on is installed on the hub cluster, you must [use the CLI](#after) to import managed clusters.
    {: important}

    1. If you selected the **Import now** option, click **Import cluster** in the pop-up menu. 
    2. To import clusters that exist in the account, select the cluster and enter the secret name and namespace. Then, click **Next**.
    3. To import cross-account or external clusters, specify the cluster ID, the secret name, and secret namespace. Then, click **Import Cluster**.

1. Click **Create**.

1. Verify that the add-on is installed on your cluster. 
    1. Navigate to your OpenShift Web Console Multicluster Hub.
    2. From the drop down navigation menu, select **Fleet Management**.
    3. Find your Clusters list and check that your cluster is listed with the **Hub** control plane type. 

1. **Optional**: Review the [additional operators](#optional-op) you can install to enhance ACM features.


## Installing ACM from the CLI
{: #install-cli}
{: cli}

Use the CLI to install the ACM add-on on the hub cluster. 

1. Find the default version of the ACM add-on.

    ```sh
    ibmcloud oc cluster addon versions
    ```
    {: pre}

2. Review the ACM add-on options. In the command, specify the default version found in the previous step. Note any options you want to include when you install the add-on. 

    ```sh
    ibmcloud oc cluster addon options --addon acm --version <default_version>
    ```
    {: pre}

3. If you want to import clusters to be managed by the add-on, follow the steps in [Preparing secrets for ACM](#prep-secret) and save the cluster ID and the name and namespace of the secret you create on the hub cluster. You can also complete this process after the add-on is installed on the hub cluster, however additional steps are required to [import managed clusters after installation](#after). 

4. Run the command to enable the add-on. Be sure to specify the `billingPlan` and `isLicenseAccepted` parameters, as well as the optional `--managedClusters` parameter if you want to import clusters during the installation process.  

    ```sh
    ibmcloud oc ibmcloud oc cluster addon enable acm --cluster HUB_CLUSTER_ID 'managedClusters=["clusterid:CLUSTER_ID;secretname:SECRET_NAME;secretnamespace:SECRET_NAMESPACE;action:IMPORT"]' --param 'billingPlan=PLAN' --param 'isLicenseAccepted=BOOLEAN' --param 
    ```
    {: pre}

    Command parameters. See the example command below for an example of each parameter type. 

    `--cluster`
    :   Required. The ID of the hub cluster to install the ACM add-on to. 

    `--param 'managedClusters=["]`
    :   Optional. Include this parameter one or more times to import managed clusters during the add-on installation process. You can also complete this step later. For more information, see [Preparing secrets for ACM](#prep-secret).
    :   Specify the following values:
    :   - **clusterid**: The ID of the managed cluster to import.
    :   - **secretname**: The name of the secret you created on the hub cluster. This secret contains the credentials for the managed cluster.
    :   - **secretnamespace**: The namespace of the secret you created on the hub cluster. This secret contains the credentials for the managed cluster.
    :   - **action:IMPORT**: The parameter that specifies the IMPORT action for the managed cluster. 
    

    `--param 'billingPlan='`
    :   Required. The billing plan you want to select for ACM. Options include `KUBERNETES` for the **ACM for Kubernetes** plan or `VIRTUALIZATION` for the **ACM for Virtualization** plan. Note that you can later upgrade from **ACM for Virtualization** to **ACM for Kubernetes**, but the upgrade is permanent and cannot be reversed.

    `--param 'isLicenseAccepted='`
    :  Required. Specify `TRUE` to accept the license agreement for the selected billing plan. By accepting this license, you agree to the applicable terms and conditions and acknowledge your understanding of the services included in the selected plan. 

    Example command to install the ACM add-on with the **ACM for Virtualization** billing plan and import a managed cluster.

    ```sh
    ibmcloud ks cluster addon enable acm --cluster a5bcde982dfer2nwxq73 --param 'managedClusters=["clusterid:w7rthce34gfbq7ww12d3;secretname:managed-secret-1;secretnamespace:managed-ns1;action:Import"]' --param 'billingPlan=KUBERNETES' --param 'isLicenseAccepted=true'
    ```
    {: pre}

5. **Optional**: Review the [additional operators](#optional-op) you can install to enhance ACM features.




## ACM operators
{: #operators}

Review the operators that are automatically installed by the ACM add-on and the optional operators that you can install as enhancements.

### Automatically installed operators
{: #auto-op}

The following operators are automatically installed on either your hub cluster or managed clusters when you install the ACM add-on.

| Operator | Description |
|---|---|
| Advanced Cluster Management (ACM) Operator | Installed on the **hub cluster**. |
| MultiCluster Engine Operator | Installed on **managed clusters** by the ACM operator. |
{: caption="Automatically installed operators for ACM." caption-side="bottom"}


### Optional operators
{: #optional-op}

The following operators are optional and can be installed on either the hub cluster or managed clusters to enhance ACM features. Note that IBM is not responsible for managing these operators. 

You are responsible for managing these operators, including but not limited to updating, monitoring, recovery, and re-installation.
{: important}

| Operator | Description | Additional information |
|---|---|---|
| GitOps Operator | - Use to run Argo-cd Applications from the ACM console. \n - Install on the **hub cluster** and any **managed clusters**. | [GitOps overview](https://docs.redhat.com/en/documentation/red_hat_advanced_cluster_management_for_kubernetes/2.15/html/gitops/gitops-overview){: external} |
| Red Hat OpenShift Virtualization Operator | - Use to manage VM workloads alongside container workloads. \n - Install on **managed clusters**. \n - Available for bare metal clusters only (only applies to the managed cluster). | [Installing the OpenShift Virtualization Operator](https://cloud.ibm.com/docs/openshift?topic=openshift-oc-virtualization) |
{: caption="Optional operators for ACM." caption-side="bottom"}


## Adding, updating, or removing a managed cluster after ACM is deployed
{: #after}

To add or remove a managed cluster from an ACM instance, you must edit the `managedClusters` section of the ACM custom resource on the hub cluster.

1. Run the command to edit the ACM resource.

    ```sh
    oc edit acmhub <resource_name>
    ```
    {: pre}

2. In the `managedClusters` section of the resource, add the cluster ID, the cluster secret, the namespace for the secret, and the action you want to implement for the cluster. See the example below for formatting. For the action, specify `Import`, `Update`, or `Delete`. Note that to delete a cluster, you do not need the secret or the secret namespace. 

    The following example adds `cluster_id_1`, updates `cluster_id_2`, and deletes `cluster_id_3` from the ACM instance.

    ```json
    managedclusters:
      - clusterid: "cluster_id_1"
        secretname: "managed-secret-1"
        secretnamespace: "managed-namespace" # The namespace that the secret was created in
        action: "Import"
      - clusterid: "cluster_id_2"
        secretname: "managed-secret-2"
        secretnamespace: "managed-namespace-2" # The namespace that the secret was created in
      - clusterid: "cluster_id_3"
        action: "Delete"  
    ```
    {: screen}

3. Save and apply the changes.

## Upgrading the ACM version
{: #upgrade}

Run the command to upgrade the add-on to a new version. 

```sh
ibmcloud oc cluster addon update acm --cluster <cluster_id> --version <add-on_version>
```
{: pre}

To check that the add-on updated, list your cluster add-ons. In the output, look for the ACM add-on details.

```sh
ibmcloud oc cluster addon ls --cluster <cluster_id>
```
{: pre}


## Deleting the ACM add-on
{: #delete}

Follow the steps to delete the ACM add-on.

1. Delete the ACM resource from the hub cluster.

    ```sh
    oc delete acmhub <resource_name>
    ```
    {: pre}

2. After the resource is deleted, remove the ACM add-on. Specify the same cluster ID. 

    ```sh
    ibmcloud oc cluster addon disable acm -f --cluster <cluster_id>
    ```
    {: pre}




