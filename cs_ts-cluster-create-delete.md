---

copyright: 
  years: 2014, 2021
lastupdated: "2021-10-08"

keywords: openshift, roks, rhoks, rhos

subcollection: openshift
content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}



# Why can't I create or delete clusters?
{: #cluster_infra_errors}
{: troubleshoot}
{: support}

You cannot perform infrastructure-related commands on your cluster, such as:
* Adding worker nodes in an existing cluster or when creating a new cluster
* Removing worker nodes
* Reloading or rebooting worker nodes
* Resizing worker pools
* Updating your cluster
* Deleting your cluster

Review the error messages in the following sections to troubleshoot infrastructure-related issues that are caused by [incorrect cluster permissions](#cs_credentials), [orphaned clusters in other infrastructure accounts](#orphaned), or [a time-based one-time passcode (TOTP) on the account](#cs_totp).

## Unable to create or delete worker nodes due to permission errors
{: #cs_credentials}


You cannot manage worker nodes for your cluster, and you receive an error message similar to one of the following.
{: tsSymptoms}

```sh
We were unable to connect to your IBM Cloud infrastructure account.
Creating a standard cluster requires that you have either a
Pay-As-You-Go account that is linked to an IBM Cloud infrastructure
account term or that you have used the {{site.data.keyword.containerlong_notm}}
CLI to set your {{site.data.keyword.cloud_notm}} Infrastructure API keys.
```
{: screen}

```sh
'Item' must be ordered with permission.
```
{: screen}

```sh
The worker node instance '<ID>' cannot be found. Review '<provider>' infrastructure user permissions.
```
{: screen}

```sh
The worker node instance cannot be found. Review '<provider>' infrastructure user permissions.
```
{: screen}

```sh
The worker node instance cannot be identified. Review '<provider>' infrastructure user permissions.
```
{: screen}

```sh
The IAM token exchange request failed with the message: <message>
IAM token exchange request failed: <message>
```
{: screen}

```sh
The cluster could not be configured with the registry. Make sure that you have the Administrator role for {{site.data.keyword.registrylong_notm}}.
```
{: screen}


The infrastructure credentials that are set for the region and resource group are missing the appropriate [infrastructure permissions](/docs/openshift?topic=openshift-access_reference#infra).
{: tsCauses}

The user's infrastructure permissions are most commonly stored as an [API key](/docs/openshift?topic=openshift-access-creds) for the region and resource group. More rarely, if you use a [different {{site.data.keyword.cloud_notm}} account type](/docs/openshift?topic=openshift-access-creds#understand_infra), you might have [set infrastructure credentials manually](/docs/openshift?topic=openshift-access-creds#credentials).



The account owner must set up the infrastructure account credentials properly. The credentials depend on what type of infrastructure account you are using.
{: tsResolve}

Before you begin, [Log in to your account. If applicable, target the appropriate resource group. Set the context for your cluster.](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure).

1. Identify what user credentials are used for the region and resource group's infrastructure permissions.
    1. Check the API key for a region and resource group of the cluster.
        ```sh
        ibmcloud oc api-key info --cluster <cluster_name_or_ID>
        ```
        {: pre}

        Example output
        ```sh
        Getting information about the API key owner for cluster <cluster_name>...
        OK
        Name                Email
        <user_name>         <name@email.com>
        ```
        {: screen}

    2. Check if the classic infrastructure account for the region and resource group is manually set to use a different IBM Cloud infrastructure account.
        ```sh
        ibmcloud oc credential get --region <us-south>
        ```
        {: pre}

        **Example output if credentials are set to use a different classic account**. In this case, the user's infrastructure credentials are used for the region and resource group that you targeted, even if a different user's credentials are stored in the API key that you retrieved in the previous step.
        ```sh
        OK
        Infrastructure credentials for user name <1234567_name@email.com> set for resource group <resource_group_name>.
        ```
        {: screen}

        **Example output if credentials are not set to use a different classic account**. In this case, the API key owner that you retrieved in the previous step has the infrastructure credentials that are used for the region and resource group.
        ```sh
        FAILED
        No credentials set for resource group <resource_group_name>.: The user credentials could not be found. (E0051)
        ```
        {: screen}

2. Validate the infrastructure permissions that the user has.
    1. List the suggested and required infrastructure permissions for the region and resource group.
        ```sh
        ibmcloud oc infra-permissions get --region <region>
        ```
        {: pre}

        For console and CLI commands to assign these permissions, see [Classic infrastructure roles](/docs/openshift?topic=openshift-access_reference#infra).
        {: tip}

    2. Make sure that the [infrastructure credentials owner for the API key or the manually-set account has the correct permissions](/docs/openshift?topic=openshift-access-creds#owner_permissions).
    3. If necessary, you can change the [API key](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_api_key_reset) or [manually-set](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_credentials_set) infrastructure credentials owner for the region and resource group.
3. Test that the changed permissions permit authorized users to perform infrastructure operations for the cluster.
    1. For example, you might try to a delete a worker node.
        ```sh
        ibmcloud oc worker rm --cluster <cluster_name_or_ID> --worker <worker_node_ID>
        ```
        {: pre}

    2. Check to see if the worker node is removed.
        ```sh
        ibmcloud oc worker get --cluster <cluster_name_or_ID> --worker <worker_node_ID>
        ```
        {: pre}

        Example output if the worker node removal is successful. The `worker get` operation fails because the worker node is deleted. The infrastructure permissions are correctly set up.
        ```sh
        FAILED
        The specified worker node could not be found. (E0011)
        ```
        {: screen}

    3. If the worker node is not removed, review that [**State** and **Status** fields](/docs/containers?topic=containers-debug_worker_nodes) and the [common issues with worker nodes](/docs/containers?topic=containers-common_worker_nodes_issues) to continue debugging.
    4. If you manually set credentials and still cannot see the cluster's worker nodes in your infrastructure account, you might check whether the [cluster is orphaned](#orphaned).

## Unable to create or delete worker nodes due to incorrect account error
{: #orphaned}

**Infrastructure provider**: ![Classic infrastructure provider icon.](images/icon-classic-2.svg) Classic


You cannot manage worker nodes for your cluster, or view the cluster worker nodes in your classic IBM Cloud infrastructure account. However, you can update and manage other clusters in the account.
{: tsSymptoms}

Further, you verified that you have the [proper infrastructure credentials](#cs_credentials).

You might receive an error message in your worker node status similar to the following.
```sh
incorrect account for worker - The 'classic' infrastructure user credentials changed and no longer match the worker node instance infrastructure account.
```
{: screen}


The cluster might be provisioned in a classic IBM Cloud infrastructure account that is no longer linked to your {{site.data.keyword.openshiftlong_notm}} account. The cluster is orphaned. Because the resources are in a different account, you do not have the infrastructure credentials to modify the resources.
{: tsCauses}

Consider the following example scenario to understand how clusters might become orphaned.
1. You have an {{site.data.keyword.cloud_notm}} Pay-As-You-Go account.
2. You create a cluster named `Cluster1`. The worker nodes and other infrastructure resources are provisioned into the infrastructure account that comes with your Pay-As-You-Go account.
3. Later, you find out that your team uses a legacy or shared classic IBM Cloud infrastructure account. You use the `ibmcloud oc credential set` command to change the IBM Cloud infrastructure credentials to use your team account.
4. You create another cluster named `Cluster2`. The worker nodes and other infrastructure resources are provisioned into the team infrastructure account.
5. You notice that `Cluster1` needs a worker node update, a worker node reload, or you just want to clean it up by deleting it. However, because `Cluster1` was provisioned into a different infrastructure account, you cannot modify its infrastructure resources. `Cluster1` is orphaned.
6. You follow the resolution steps in the following section, but do not set your infrastructure credentials back to your team account. You can delete `Cluster1`, but now `Cluster2` is orphaned.
7. You change your infrastructure credentials back to the team account that created `Cluster2`. Now, you no longer have an orphaned cluster!




Before you begin: Log in to the [{{site.data.keyword.openshiftshort}} clusters console](https://cloud.ibm.com/kubernetes/clusters?platformType=openshift){: external}. [Log in to your account. If applicable, target the appropriate resource group. Set the context for your cluster.](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure).
{: tsResolve}

1. Check which infrastructure account the region that your cluster is in currently uses to provision clusters. Replace `<region>` with the {{site.data.keyword.cloud_notm}} region that the cluster is in.
    ```sh
    ibmcloud oc credential get --region <region>
    ```
    {: pre}

    If you see a message similar to the following, then the account uses the default, linked infrastructure account.
    ```sh
    No credentials set for resource group <resource group>.: The user credentials could not be found.
    ```
    {: screen}

2. Check which infrastructure account was used to provision the cluster.
    1. In the **Worker Nodes** tab, select a worker node and note its **ID**.
    2. Open the menu ![Menu icon](../../icons/icon_hamburger.svg "Menu icon") and click **Classic Infrastructure**.
    3. From the infrastructure navigation pane, click **Devices > Device List**.
    4. Search for the worker node ID that you previously noted.
    5. If you do not find the worker node ID, the worker node is not provisioned into this infrastructure account. Switch to a different infrastructure account and try again.
3. Compare the infrastructure accounts.
    *   **If the worker nodes are in the linked infrastructure account**: Use the `ibmcloud oc credential unset` [command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_credentials_unset) to resume using the default infrastructure credentials that are linked with your Pay-As-You-Go account.
    *   **If the worker nodes are in a different infrastructure account**: Use the `ibmcloud oc credential set` [command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_credentials_set) to change your infrastructure credentials to the account that the cluster worker nodes are provisioned in, which you found in the previous step.

        If you no longer have access to the infrastructure credentials, you can open an {{site.data.keyword.cloud_notm}} support case to determine an email address for the administrator of the other infrastructure account. However, {{site.data.keyword.cloud_notm}} Support cannot remove the orphaned cluster for you, and you must contact the administrator of the other account to get the infrastructure credentials.
        {: note}

    *   **If the infrastructure accounts match**: Check the rest of the worker nodes in the cluster and see if any has a different infrastructure account. Make sure that you checked the worker nodes in the cluster that has the credentials issue. Review other [common infrastructure credential issues](/docs/containers?topic=containers-worker_infra_errors).
4. Now that the infrastructure credentials are updated, retry the blocked action, such as updating or deleting a worker node, and verify that the action succeeds.
5. If you have other clusters in the same region and resource that require the previous infrastructure credentials, repeat Step 3 to reset the infrastructure credentials to the previous account. Note that if you created clusters with a different infrastructure account than the account that you switch to, you might orphan those clusters.

    Tired of switching infrastructure accounts each time you need to perform a cluster or worker action? Consider re-creating all the clusters in the region and resource group in the same infrastructure account. Then, migrate your workloads and remove the old clusters from the different infrastructure account.
    {: note}

## Unable to create or delete worker nodes due to endpoints error
{: #vpe-ts}

**Infrastructure provider**: ![VPC infrastructure provider icon.](images/icon-vpc-2.svg) VPC {{site.data.keyword.openshiftshort}} version 4.6 or later


You cannot manage worker nodes for your cluster, and you receive an error message similar to one of the following.
{: tsSymptoms}

```sh
Worker deploy failed due to network communications failing to master or registry endpoints. Please verify your network setup is allowing traffic from this subnet then attempt a worker replace on this worker
```
{: screen}

```sh
Pending endpoint gateway creation
```
{: screen}


In clusters that run {{site.data.keyword.openshiftshort}} version 4.6 or later, worker nodes can communicate with the Kubernetes master through the cluster's virtual private endpoint (VPE).
{: tsCauses}

One VPE gateway resource is created per cluster in your VPC. If the VPE gateway for your cluster is not correctly created in your VPC, the VPE gateway is deleted from your VPC, or the IP address that is reserved for the VPE is deleted from your VPC subnet, worker nodes lose connectivity with the Kubernetes master.

Re-establish the VPE connection between your worker nodes and Kubernetes master.
{: tsResolve}

1. To check the VPE gateway for your cluster in the VPC infrastructure console, open the [Virtual private endpoint gateways for VPC dashboard](https://cloud.ibm.com/vpc-ext/network/endpointGateways){: external} and look for the VPE gateway in the format `iks-<cluster_ID>`.
    * If the gateway for your cluster is not listed, continue to the next step.
    * If the gateway for your cluster is listed but its status is not `Stable`, [open a support case](/docs/openshift?topic=openshift-get-help#help-support). In the case details, include the cluster ID.
    * If the gateway for your cluster is listed and its status is `Stable`, you might have firewall or security group rules that are blocking worker node communication to the cluster master. [Configure your security group rules to allow outgoing traffic to the appropriate ports and IP addresses](/docs/openshift?topic=openshift-vpc-network-policy#security_groups).

2. Refresh the cluster master. If the VPE gateway did not exist in your VPC, it is created, and connectivity to the reserved IP addresses on the subnets that your worker nodes are connected to is re-established. After you refresh the cluster, wait a few minutes to allow the operation to complete.
    ```sh
    ibmcloud oc cluster master refresh -c <cluster_name_or_ID>
    ```
    {: pre}

3. Verify that the VPE gateway for your cluster is created by opening the [Virtual private endpoint gateways for VPC dashboard](https://cloud.ibm.com/vpc-ext/network/endpointGateways){: external} and looking for the VPE gateway in the format `iks-<cluster_ID>`.

4. If you still cannot manage worker nodes after the cluster master is refreshed, replace the worker nodes that you cannot access.
    1. List all worker nodes in your cluster and note the **name** of the worker node that you want to replace.
        ```sh
        oc get nodes
        ```
        {: pre}

        The **name** that is returned in this command is the private IP address that is assigned to your worker node. You can find more information about your worker node when you run the `ibmcloud oc worker ls --cluster <cluster_name_or_ID>` command and look for the worker node with the same **Private IP** address.

    2. Replace the worker node. As part of the replace process, the pods that run on the worker node are drained and rescheduled onto remaining worker nodes in the cluster. The worker node is also cordoned, or marked as unavailable for future pod scheduling. Use the worker node ID that is returned from the `ibmcloud oc worker ls --cluster <cluster_name_or_ID>` command.
        ```sh
        ibmcloud oc worker replace --cluster <cluster_name_or_ID> --worker <worker_node_ID>
        ```
        {: pre}

    3. Verify that the worker node is replaced.
        ```sh
        ibmcloud oc worker ls --cluster <cluster_name_or_ID>
        ```
        {: pre}

## Unable to create or delete worker nodes due to paid account or one time password error
{: #cs_totp}

**Infrastructure provider**: ![Classic infrastructure provider icon.](images/icon-classic-2.svg) Classic


You cannot manage worker nodes for your cluster, and you receive an error message similar to one of the following.
{: tsSymptoms}

```sh
Unable to connect to the IBM Cloud account. Ensure that you have a paid account.
```
{: screen}

```sh
Cannot authenticate the infrastructure user: Time-based One Time Password authentication is required to log in with this user.
```
{: screen}


Your {{site.data.keyword.cloud_notm}} account uses its own automatically linked infrastructure through a Pay-as-you-Go account.
{: tsCauses}

However, the account administrator enabled the time-based one-time passcode (TOTP) option so that users are prompted for a time-based one-time passcode (TOTP) at login. This type of [multifactor authentication (MFA)](/docs/account?topic=account-types#account-based) is account-based, and affects all access to the account. TOTP MFA also affects the access that {{site.data.keyword.containerlong_notm}} requires to make calls to {{site.data.keyword.cloud_notm}} infrastructure. If TOTP is enabled for the account, you cannot create and manage clusters and worker nodes in {{site.data.keyword.containerlong_notm}}.


The {{site.data.keyword.cloud_notm}} account owner or an account administrator must either:
{: tsResolve}

* Disable TOTP for the account, and continue to use the automatically linked infrastructure credentials for {{site.data.keyword.containerlong_notm}}.
* Continue to use TOTP, but create an infrastructure API key that {{site.data.keyword.containerlong_notm}} can use to make direct calls to the {{site.data.keyword.cloud_notm}} infrastructure API.

**To disable TOTP MFA for the account:**
1. Log in to the [{{site.data.keyword.cloud_notm}} console](https://cloud.ibm.com/){: external}. From the menu bar, select **Manage > Access (IAM)**.
2. In the left navigation, click the **Settings** page.
3. Under **Multifactor authentication**, click **Edit**.
4. Select **None**, and click **Update**.

**To use TOTP MFA and create an infrastructure API key for {{site.data.keyword.containerlong_notm}}:**
1. From the [{{site.data.keyword.cloud_notm}}](https://cloud.ibm.com/){: external} console, select **Manage** > **Access (IAM)** > **Users** and click the name of the account owner. **Note**: If you do not use the account owner's credentials, first [ensure that the user whose credentials you use has the correct permissions](/docs/openshift?topic=openshift-access-creds#owner_permissions).
2. In the **API Keys** section, find or create a classic infrastructure API key.
3. Use the infrastructure API key to set the infrastructure API credentials for {{site.data.keyword.containerlong_notm}}. Repeat this command for each region where you create clusters.
    ```sh
    ibmcloud oc credential set classic --infrastructure-username <infrastructure_API_username> --infrastructure-api-key <infrastructure_API_authentication_key> --region <region>
    ```
    {: pre}

4. Verify that the correct credentials are set.
    ```sh
    ibmcloud oc credential get --region <region>
    ```
    {: pre}

    Example output

    ```sh
    Infrastructure credentials for user name user@email.com set for resource group default.
    ```
    {: screen}

5. To ensure that existing clusters use the updated infrastructure API credentials, run `ibmcloud oc api-key reset --region <region>` in each region where you have clusters.




