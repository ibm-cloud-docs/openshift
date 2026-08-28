---

copyright:
  years: 2025, 2026
lastupdated: "2026-08-28"


keywords: openshift, acm, advanced cluster management, manage cluster, management, addon, add-on, acm addon

subcollection: openshift

---


{{site.data.keyword.attribute-definition-list}}

# Setting up the Advanced Cluster Management add-on
{: #acm}

The Advanced Cluster Management (ACM) add-on provides a simplified way for customers to manage monitoring, workload placement, and security policies across multiple clusters.
{: shortdesc}

Installing ACM from OperatorHub is not supported for IBM Cloud clusters. To install ACM, follow the instructions on this page.
{: important}

The cluster that you install ACM on is the **hub cluster**. During or after the installation, you can specify multiple **managed clusters** to manage with ACM.

## Before you begin
{: #before}

Review the following prerequisite steps and information before you install the ACM add-on.


1. Make sure that your clusters meet the following requirements.
    - Your **hub cluster** must be a VPC cluster with at least **3** worker nodes that run **RHCOS** and a minimum of **6 VCPU and 64GB RAM**. For high availability, make sure that your cluster has at least one worker node per zone across 3 zones.
    - Each **managed cluster** must have at least **3** worker nodes that run **RHCOS** and a minimum of **6 VCPU and 64GB RAM**. 
1. Review the [operators that are automatically installed](#auto-op) by the ACM add-on and the [optional operators](#optional-op) that you can install as enhancements.
1. You must have the [Administrator platform access role and the Manager service access role](/docs/openshift?topic=openshift-iam-platform-access-roles) for the cluster in IBM Cloud Kubernetes Service.
1. You must have a VPC cluster with at least 3 worker nodes. Each worker node must have a minimum of 4 CPUs and 16GB RAM. For high availability, make sure that your cluster has at least one worker node per zone across 3 zones.
1. [Create a trusted profile on your cluster to use for ACM](#trust-prof).
1. **Optional**: If you want to import managed clusters during the ACM add-on installation process, if you plan to import managed clusters using the CLI after installation, or if you plan to update a managed cluster's connection credentials later, you must create a secret on the hub cluster for each managed cluster. See [Preparing secrets for ACM](#prep-secret). This step is not required if you only plan to import managed clusters after installation using the OpenShift web console.
1. [Install or update the CLI](/docs/openshift?topic=openshift-cli-install).

## Create a trusted profile for ACM
{: #trust-prof}

Follow the steps to create a trusted profile to use for ACM and assign it to the hub cluster.

Once you add a trusted profile to a cluster, it cannot be removed and you cannot resume using an API key for your resources. Make sure that you follow these steps carefully to ensure that your trusted profile is set up correctly.
{: important}

### Create a trusted profile using the UI
{: #trust-prof-ui}
{: ui}

1. Follow the steps to [create a trusted profile](/docs/iam?topic=iam-create-trusted-profile&interface=ui). In the **Conditions** for the profile, be sure to specify the following access.
    * Compute resources: **Red Hat OpenShift**
    * All service resources
    * Allow access when **Namespace** equals `kube-system`
    * Kubernetes Service Roles - Manager, Editor

1. After you create your trusted profile, copy the ID from the **Trusted profiles** page in the console.

### Create a trusted profile using the CLI
{: #trust-prof-cli}
{: cli}

1. Create the trusted profile.
    ```sh
    ibmcloud iam trusted-profile-create acm-operator-profile
    ```
    {: pre}

1. Create the compute resource trust rule, scoped to the `kube-system` namespace on Red Hat OpenShift compute resources.
    ```sh
    ibmcloud iam trusted-profile-rule-create acm-operator-profile \
      --name kube-system-rule \
      --type Profile-CR \
      --conditions claim:namespace,operator:EQUALS,value:kube-system \
      --cr-type ROKS_SA
    ```
    {: pre}

1. Assign the IAM access policy to the profile. Replace `CLUSTER_ID` with your hub cluster ID.
    ```sh
    ibmcloud iam trusted-profile-policy-create acm-operator-profile \
      --roles Reader,Viewer,Operator,Editor \
      --service-name containers-kubernetes \
      --service-instance CLUSTER_ID
    ```
    {: pre}

### Set the trusted profile for the cluster
{: #trust-prof-set}

1. Retrieve the trusted profile ID.
    ```sh
    ibmcloud iam trusted-profiles
    ```
    {: pre}

1. Assign the trusted profile to the cluster.
    ```sh
    ibmcloud oc experimental trusted-profile set --cluster CLUSTER_NAME_OR_ID --trusted-profile TRUSTED_PROFILE_ID
    ```
    {: pre}

1. Verify that the trusted profile secret was created in the cluster. This command can take up to 10 minutes to complete. Wait for the secret to appear before proceeding to install the ACM add-on. If you proceed before the secret is created, the ACM add-on installation will fail.
    ```sh
    oc get secrets -n kube-system | grep ibm-cloud-credentials
    ```
    {: pre}

## Preparing secrets for ACM
{: #prep-secret}

Creating secrets for ACM is optional. You only need to complete this section if you want to import managed clusters during the ACM add-on installation process, if you plan to [import managed clusters after installation using the CLI](#import-cli), or if you plan to [update a managed cluster's connection credentials](#after) later.

If you plan to import managed clusters after installation using the OpenShift web console and do not need to update connection credentials later, you do not need to create secrets.
{: important}

For each cluster that you want to manage, complete the following steps on the hub cluster.

1. On the cluster that you want to manage with ACM, run the command to find the server URL. In the output, find and note the **Master URL** value. This is the server URL to reference in the secret. You also use this URL in the following steps.

    ```sh
    ibmcloud oc cluster get -c CLUSTER_NAME_OR_ID
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

2. Retrieve the base URL of the Red Hat OpenShift oauth server. Replace `MASTER_URL` with the URL found in the previous step. The command extracts the base URL without the `/oauth/token` suffix.

    ```sh
    curl -sS MASTER_URL/.well-known/oauth-authorization-server | jq -r .token_endpoint | sed 's#/oauth/token##'
    ```
    {: pre}

    Example output.

    ```sh
    https://c111-e.us-east.containers.cloud.ibm.com:31282
    ```
    {: screen}


3. Retrieve an access token using the endpoint retrieved in the previous step. Execute the following cURL command, replacing `URL` with the output from the previous step and `API_KEY` with your [IBM Cloud API key](https://cloud.ibm.com/iam/apikeys){: external}. In the output, find the `ACCESS_TOKEN` contained in the **Location response**. This is the access token to include in the secret.

    Example curl request:

    ```sh
    curl -u 'apikey:API_KEY' -H "X-CSRF-Token: a" 'URL/oauth/authorize?client_id=openshift-challenging-client&response_type=token' -vvv
    ```
    {: pre}

    Example output. The ACCESS_TOKEN is included in the Location response string.

    ```sh
    < HTTP/1.1 302 Found
    < Cache-Control: no-cache, no-store, max-age=0, must-revalidate
    < Cache-Control: no-cache, no-store, max-age=0, must-revalidate
    < Expires: 0
    < Expires: Fri, 01 Jan 2030 00:00:00 GMT
    < Location: TOKEN_ENDPOINT/oauth/token/implicit#access_token=ACCESS_TOKEN&expires_in=86400&scope=user%3Afull&token_type=Bearer
    ...
    ```
    {: screen}


4. On the hub cluster, create a secret that contains the cluster access token and server URL. For information on creating secrets, see [Working with secrets](https://kubernetes.io/docs/concepts/configuration/secret/){: external} in the Kubernetes documentation.

    Example secret.

    ```json
    apiVersion: v1
    kind: Secret
    metadata:
      name: SECRET_NAME
      namespace: SECRET_NAMESPACE  # The namespace that the secret is to be created in
    type: Opaque
    stringData:
      token: ACCESS_TOKEN
      server: SERVER_URL
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



1. Choose how you want to import managed clusters. To import clusters after the add-on is installed, select **Import from CLI**. If you created the required secrets on the hub cluster and you want to import managed clusters now, select **Import now**.

    You can only use the IBM Cloud UI to import managed clusters during the installation process. Once the ACM add-on is installed on the hub cluster, you can [use the CLI](#after) or the OpenShift web console to import managed clusters.
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
    ibmcloud oc cluster addon options --addon acm --version DEFAULT_VERSION
    ```
    {: pre}

3. If you want to import clusters to be managed by the add-on and, follow the steps in [Preparing secrets for ACM](#prep-secret) if you have not already done so. Be sure to save the cluster ID and the name and namespace of the secret you create on the hub cluster. You can also complete this process after the add-on is installed on the hub cluster, however additional steps are required to [import managed clusters after installation](#after).

4. Run the command to enable the add-on. Be sure to specify the `billingPlan` and `isLicenseAccepted` parameters, as well as the optional `--managedClusters` parameter if you want to import clusters during the installation process.

    ```sh
    ibmcloud oc cluster addon enable acm --cluster HUB_CLUSTER_ID --param 'managedClusters=["clusterid:CLUSTER_ID;secretname:SECRET_NAME;secretnamespace:SECRET_NAMESPACE;action:IMPORT"]' --param 'billingPlan=PLAN' --param 'isLicenseAccepted=BOOLEAN'
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
    :   Required. The billing plan you want to select for ACM. Specify `KUBERNETES` for the **ACM for Kubernetes** plan.

    `--param 'isLicenseAccepted='`
    :  Required. Specify `TRUE` to accept the license agreement for the selected billing plan. By accepting this license, you agree to the applicable terms and conditions and acknowledge your understanding of the services included in the selected plan. 
    
1. Verify that the add-on installed. It might take several minutes for the add-on to show in the following outputs.

    1. On the hub cluster, check that the `acmhub` resource is created.
        ```sh
        oc get acmhub
        ```
        {: pre}

        Example output.

        ```sh
            NAME       AGE
            acm-auto   1h
        ```
        {: screen}

    2. On the hub cluster, check the `acmhub` status.

        ```sh
        oc describe acmhubstatus
        ```
        {: pre}

        Example output.

        ```sh
        status
            phase: Ready
        ```
        {: screen}

5. **Optional**: Review the [additional operators](#optional-op) you can install to enhance ACM features.



## ACM operators
{: #acm-operators}

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
| Submariner | - Provides direct networking between two or more Kubernetes clusters in your environment. Required for [Regional Disaster Recovery with ODF](/docs/openshift?topic=openshift-openshift_odf_rdr_roks&interface=cli). \n - Install on **managed clusters**. | [Submariner](https://docs.redhat.com/en/documentation/red_hat_advanced_cluster_management_for_kubernetes/2.2/html/manage_cluster/submariner){: external} |
{: caption="Optional operators for ACM." caption-side="bottom"}

## Importing managed clusters after ACM is installed
{: #import}

You can import managed clusters after ACM is installed by using the OpenShift web console or the CLI. The console-based methods do not require a secret. The CLI method requires a [secret](#prep-secret).

All clusters managed by ACM must belong to a cluster set. You can create a new cluster set, or you can add clusters to the `Default` cluster set. If no cluster set is specified, managed clusters are added to the `Default` option.
{: tip}

### Importing a managed cluster by using a generated command
{: #import-generate}

Use the OpenShift web console to generate an import command, then run that command on the cluster you want to import.

1. Open the OpenShift web console for the ACM hub cluster.

2. From the **Fleet Management** perspective, click **Import cluster**.

3. Enter the **Name** of the cluster, select a **Cluster set** if applicable, and enter **Additional labels** if applicable.

4. For **Import mode**, select **Run import commands manually** and click **Next**.

5. Optionally select an automation template and click **Next**.

6. Review the details and click **Generate command**. Copy the command that is displayed.

7. Log in to the cluster you want to import and run the copied command with `kubectl` configured for that cluster.

### Importing a managed cluster by using the server URL and API token
{: #import-token-url}

Gather the API token and server URL for the cluster you want to import, then use the OpenShift web console to import the cluster.

1. Get the API token and server URL for the cluster you want to import.

    1. In the {{site.data.keyword.cloud_notm}} console, navigate to your [cluster list](https://cloud.ibm.com/containers/cluster-management/clusters){: external} and click the cluster you want to import.

    2. From the cluster details page, click **OpenShift web console**.

    3. Click the username menu, shown in the format `IAM#username`, then click **Copy login command**.

    4. Click **Display token**. Find the command that begins with `oc login` and save the API token (`sha256~XXXX`) and the server URL.

2. Open the OpenShift web console for the ACM hub cluster.

3. From the **Fleet Management** perspective, click **Import cluster**.

4. Enter the **Name** of the cluster, select a **Cluster set** if applicable, and enter **Additional labels** if applicable.

5. For **Import mode**, select **Enter your server URL and API token for the existing cluster**. Enter the server URL and API token that you retrieved, then click **Next**.

6. Optionally select an automation template and click **Next**.

7. Review the details and click **Import**.

### Importing a managed cluster by using the kubeconfig
{: #import-kubeconfig}

Gather the kubeconfig for the cluster you want to import, then use the OpenShift web console to import the cluster.

1. Get the kubeconfig for the cluster you want to import. From the IBM Cloud CLI, run the following command and save the output.

    ```sh
    ibmcloud ks cluster config --cluster CLUSTER_NAME --admin --output yaml
    ```
    {: pre}

2. Open the OpenShift web console for the ACM hub cluster.

3. From the **Fleet Management** perspective, click **Import cluster**.

4. Enter the **Name** of the cluster, select a **Cluster set** if applicable, and enter **Additional labels** if applicable.

5. For **Import mode**, select **Kubeconfig** and paste in the kubeconfig content that you retrieved, then click **Next**.

6. Optionally select an automation template and click **Next**.

7. Review the details and click **Import**.

### Import from Red Hat OpenShift Cluster Manager
{: #import-ocm}

The **Import from Red Hat OpenShift Cluster Manager** import mode is only supported for Red Hat OpenShift Service on AWS (ROSA) clusters and is not applicable for IBM Cloud clusters.

### Importing a managed cluster using the CLI
{: #import-cli}

The CLI import method requires you to have [created a secret](#prep-secret) for the managed cluster on the hub cluster.

To import a managed cluster using the CLI, edit the ACM resource to include the cluster to manage.

1. Run the command to edit the ACM resource.

    ```sh
    oc edit acmhub RESOURCE_NAME
    ```
    {: pre}

2. In the `managedClusters` section of the resource, add the cluster ID, the name of the cluster secret created for ACM, the namespace for the secret, and specify the `Import` action. The following example imports `CLUSTER_ID_1`.

    ```json
    managedclusters:
      - clusterid: "CLUSTER_ID_1"
        secretname: "SECRET_NAME"
        secretnamespace: "SECRET_NAMESPACE" # The namespace that the secret was created in
        action: "Import"
    ```
    {: screen}

3. Save and apply the changes.


## Updating or removing a managed cluster
{: #after}

To remove a managed cluster from an ACM instance, or to update ACM's connection credentials for a managed cluster (for example, after token rotation or a server URL change), you must edit the `managedClusters` section of the ACM custom resource on the hub cluster. The `Update` action refreshes the secret-based credentials that ACM uses to communicate with a managed cluster. This is not the same as upgrading the OpenShift version of a cluster.

Updating a managed cluster's connection credentials requires the [secret](#prep-secret) for that cluster.
{: note}

1. Run the command to edit the ACM resource.

    ```sh
    oc edit acmhub RESOURCE_NAME
    ```
    {: pre}

2. In the `managedClusters` section of the resource, add the cluster ID, the name of the cluster secret created for ACM, the namespace for the secret, and the action you want to implement for the cluster. See the example below for formatting. For the action, specify `Delete` or `Update`. Note that to delete a cluster, you do not need the secret or the secret namespace.

    The following example deletes `CLUSTER_ID_1` and updates `CLUSTER_ID_2`.

    ```json
    managedclusters:
      - clusterid: "CLUSTER_ID_1"
        action: "Delete"
      - clusterid: "CLUSTER_ID_2"
        secretname: "SECRET_NAME"
        secretnamespace: "SECRET_NAMESPACE" # The namespace that the secret was created in
        action: "Update"
    ```
    {: screen}

3. Save and apply the changes.

## Upgrading the ACM version
{: #upgrade}

Run the command to upgrade the add-on to a new version.

```sh
ibmcloud oc cluster addon update acm --cluster CLUSTER_ID --version ADD-ON_VERSION
```
{: pre}

To check that the add-on updated, list your cluster add-ons. In the output, look for the ACM add-on details.

```sh
ibmcloud oc cluster addon ls --cluster CLUSTER_ID
```
{: pre}


## Deleting the ACM add-on
{: #delete}

Follow the steps to delete the ACM add-on.

1. Delete the ACM resource from the hub cluster.

    ```sh
    oc delete acmhub RESOURCE_NAME
    ```
    {: pre}

2. After the resource is deleted, remove the ACM add-on. Specify the same cluster ID.

    ```sh
    ibmcloud oc cluster addon disable acm -f --cluster CLUSTER_ID
    ```
    {: pre}
