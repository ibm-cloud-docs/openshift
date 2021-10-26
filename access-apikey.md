---

copyright: 
  years: 2014, 2021
lastupdated: "2021-10-26"

keywords: openshift, roks, rhoks, rhos

subcollection: openshift


---


{{site.data.keyword.attribute-definition-list}}


# Setting up API key credentials so the service can access the infrastructure and other cloud services
{: #access-creds}

To successfully provision and work with clusters, you must ensure that your {{site.data.keyword.cloud_notm}} account is correctly set up to access {{site.data.keyword.cloud_notm}} infrastructure and other {{site.data.keyword.cloud_notm}} services that you use in each resource group and region that your clusters are in.
{: shortdesc}

## Setting up the API key in most cases
{: #api_key_most_cases}
{: help}
{: support}

Your {{site.data.keyword.cloud_notm}} Pay-As-You-Go or Subscription account is already set up with access to {{site.data.keyword.cloud_notm}} infrastructure. To use this infrastructure in {{site.data.keyword.openshiftlong_notm}}, the **account owner** must make sure that an [API key](#api_key_about) is created with appropriate permissions for each region and resource group.
{: shortdesc}

The quickest way to set up the API key is to ask the account owner, who already has the required infrastructure permissions. However, the account owner might want to create a functional ID with all the required infrastructure permissions. Then, if the account owner is unavailable or changes, the API key owner remains the functional ID. Note that you cannot use a service ID to set the API key.
{: tip}

1. As the account owner, [invite a functional ID](/docs/account?topic=account-iamuserinv) to your {{site.data.keyword.cloud_notm}} account to use to set the API key infrastructure credentials, instead of a personal user.
2. [Assign the functional ID the correct permissions](#owner_permissions).
3. Log in as the functional ID.
    ```sh
    ibmcloud login
    ```
    {: pre}

4. Target the resource group where you want to set the API key. If you do not target a resource group, the API key is set for the default resource group. To list available resource groups, run `ibmcloud resource groups`.
    ```sh
    ibmcloud target -g <resource_group_name>
    ```
    {: pre}

5. Create an API key that impersonates your infrastructure permissions. {{site.data.keyword.openshiftlong_notm}} uses this API key to authenticate requests to manage infrastructure in the region and resource group. The previous API key for the region and resource group, if any, is deleted.
    ```sh
    ibmcloud oc api-key reset --region <region>
    ```
    {: pre}    

6. Verify that the API key is set up.
    ```sh
    ibmcloud oc api-key info --cluster <cluster_name_or_ID>
    ```
    {: pre}

7. Repeat these steps for each region and resource group that you want to create clusters in.

Now that the API key is set up for the region and resource group, you can [assign users {{site.data.keyword.cloud_notm}} IAM platform access roles](/docs/openshift?topic=openshift-users#checking-perms) to restrict what cluster infrastructure actions they can perform.


## Understanding other options than the API key
{: #api_key_other}

For different ways to access the IBM Cloud infrastructure portfolio, check out the following sections.
{: shortdesc}

* If you aren't sure whether your account already has access to the IBM Cloud infrastructure portfolio, see [Understanding access to the infrastructure portfolio](#understand_infra).
* If the account owner does not set the API key, [ensure that the user who sets the API key has the correct permissions](#owner_permissions).
* For more information about using your Pay-As-You-Go or Subscription account to set the API key, see [Accessing the infrastructure portfolio with your {{site.data.keyword.cloud_notm}} Pay-As-You-Go or Subscription account](#default_account).
* If you don't have a Pay-As-You-Go or Subscription account or need to use a different IBM Cloud infrastructure account, see [Accessing a different IBM Cloud infrastructure account](#credentials).


## Understanding how the API key works
{: #api_key_about}

{{site.data.keyword.openshiftlong_notm}} accesses the IBM Cloud infrastructure portfolio and other {{site.data.keyword.cloud_notm}} services that you use for your cluster by using an [API key](/docs/account?topic=account-manapikey). The API key impersonates, or stores the credentials of, a user with access to the infrastructure and other services. {{site.data.keyword.openshiftlong_notm}} uses the API key to order resources in the service, such as new worker nodes or VLANs in IBM Cloud infrastructure.
{: shortdesc}

**What is the API key used for?**

The API key is used to authorize underlying actions in the following {{site.data.keyword.cloud_notm}} services.
- **Infrastructure**, such as classic or VPC compute, networking, and storage resources for your cluster.
- **{{site.data.keyword.keymanagementserviceshort}}** or **{{site.data.keyword.hscrypto}}**, if you [enable a key management service provider](/docs/openshift?topic=openshift-encryption#kms) in your cluster.
- **{{site.data.keyword.cloudcerts_short}}**, for managing the Ingress certificates for your cluster.
- **{{site.data.keyword.registryshort}}**, for setting up default access to pull images from the registry to your cluster.
- **{{site.data.keyword.la_short}}**, if you [enable the logging service](/docs/containers?topic=containers-health).
- **{{site.data.keyword.mon_short}}**, if you [enable the monitoring service](/docs/containers?topic=containers-health).
- **{{site.data.keyword.at_short}}**, for sending audit events from your cluster.

**How many API keys do I need?**

You have a different API key for each region and resource group where you use {{site.data.keyword.openshiftlong_notm}}. To check if an API key is already set up for the region and resource group, run the following command.

```sh
ibmcloud oc api-key info --cluster <cluster_name_or_ID>
```
{: pre}

**How do I set up the API key?**

To enable all users to access the infrastructure portfolio or other services, the user whose credentials are stored in the [API key must have the correct permissions](#owner_permissions). Then, log in as the user or functional ID and perform the first admin action in a region and resource group or [reset the API key](#api_key_most_cases). For example, one of your admin users creates the first cluster in the `default` resource group in the `us-south` region. As a result, the {{site.data.keyword.cloud_notm}} IAM API key for this admin user is created in the account for this resource group and region.

**What permissions does the user who sets the API key need? How do I give the user these permissions?**

See [Permissions to create a cluster](/docs/openshift?topic=openshift-access_reference#cluster_create_permissions) and [Ensuring that the API key or infrastructure credentials owner has the correct permissions](#owner_permissions).

To check a user's permissions, review the access policies and access groups of the user in the [{{site.data.keyword.cloud_notm}} console](https://cloud.ibm.com/iam/users){: external}, or use the `ibmcloud iam user-policies <user>` command.

**If the API key is based on one user, how are other cluster users in the region and resource group affected?**

Other users within the region and resource group of the account share the API key for accessing the infrastructure and other services with {{site.data.keyword.openshiftlong_notm}} clusters. When users log in to the {{site.data.keyword.cloud_notm}} account, an {{site.data.keyword.cloud_notm}} IAM token that is based on the API key is generated for the CLI session and enables infrastructure-related commands to be run in a cluster.

To see the {{site.data.keyword.cloud_notm}} IAM token for a CLI session, you can run `ibmcloud iam oauth-tokens`. 
{: tip}

**If users have access to the portfolio through an {{site.data.keyword.cloud_notm}} IAM token, how do I limit which commands a user can run?**

After you set up access to the portfolio for users in your account, you can then control which infrastructure actions the users can perform by assigning the appropriate [platform access role](/docs/openshift?topic=openshift-users#checking-perms). By assigning {{site.data.keyword.cloud_notm}} IAM roles to users, they are limited in which commands they can run against a cluster. For example, because the API key owner has all the required infrastructure roles, all infrastructure-related commands can be run in a cluster. But, depending on the {{site.data.keyword.cloud_notm}} IAM role that is assigned to a user, the user can run only some of those infrastructure-related commands.

For example, if you want to create a cluster in a new region, make sure that the first cluster is created by a user with the **Super User** infrastructure role, such as the account owner. After verification, you can invite individual users or users in {{site.data.keyword.cloud_notm}} IAM access groups to that region by setting platform access policies for them in that region. A user with a **Viewer** platform access role isn't authorized to add a worker node. Therefore, the `worker-add` action fails, even though the API key has the correct infrastructure permissions. If you change the user's platform access role to **Operator**, the user is authorized to add a worker node. The `worker-add` action succeeds because the user is authorized and the API key is set correctly. You don't need to edit the user's IBM Cloud infrastructure permissions.

To audit the actions that users in your account run, you can use [{{site.data.keyword.cloudaccesstrailshort}}](/docs/containers?topic=containers-at_events) to view all cluster-related events.
{: tip}

**What if I don't want to assign the API key owner or credentials owner the Super User infrastructure role?**

For compliance, security, or billing reasons, you might not want to give the **Super User** infrastructure role to the user who sets the API key or whose credentials are set with the `ibmcloud oc credential set` command. However, if this user doesn't have the **Super User** role, then infrastructure-related actions, such as creating a cluster or reloading a worker node, can fail. Instead of using {{site.data.keyword.cloud_notm}} IAM platform access roles to control users' infrastructure access, you must [set specific IBM Cloud infrastructure permissions](#infra_access) for users.

**What happens if the user who set up the API key for a region and resource group leaves the company?**

If the user is leaving your organization, the {{site.data.keyword.cloud_notm}} account owner can remove that user's permissions. However, before you remove a user's specific access permissions or remove a user from your account completely, you must reset the API key with another user's infrastructure credentials. Otherwise, the other users in the account might lose access to the IBM Cloud infrastructure portal and infrastructure-related commands might fail. For more information, see [Removing user permissions](/docs/openshift?topic=openshift-users#removing).

Consider using a functional ID user for the API key owner instead of a personal user. In case the person leaves the team, the functional ID user remains the API key owner. Keep in mind that you cannot use a service ID to set the API key.

**How can I lock down my cluster if my API key becomes compromised?**

If an API key that is set for a region and resource group in your cluster is compromised, [delete it](/docs/account?topic=account-userapikey#delete_user_key) so that no further calls can be made by using the API key as authentication. For more information about securing access to the Kubernetes API server, see the [Kubernetes API server and etcd](/docs/openshift?topic=openshift-security#apiserver) security topic.

## Ensuring that the API key or infrastructure credentials owner has the correct permissions
{: #owner_permissions}

To ensure that all infrastructure-related actions can be successfully completed in the cluster, the user whose credentials you want to set for the API key must have the proper permissions. Consider using a functional ID user for the API key owner instead of a personal user. In case the person leaves the team, the functional ID user remains the API key owner. Note that you cannot use a service ID to set the API key.
{: shortdesc}

1. Log in to the [{{site.data.keyword.cloud_notm}} console](https://cloud.ibm.com/){: external}.

2. To make sure that all account-related actions can be successfully performed, verify that the user has the correct {{site.data.keyword.cloud_notm}} IAM platform access roles.
    1. From the menu bar, select **Manage > Access (IAM)**, and then click the **Users** page.
    2. Click the name of the user who you want to set the API key for or whose credentials you want to set for the API key, and then click the **Access policies** tab.
    3. [Assign the user](/docs/openshift?topic=openshift-users#checking-perms) the [minimum permissions that are needed to create and manage clusters](/docs/openshift?topic=openshift-access_reference#cluster_create_permissions).

3. To make sure that all infrastructure-related actions in your cluster can be successfully performed, verify that the user has the correct infrastructure access policies.
    1. From the menu bar, select **Manage > Access (IAM)**.
    2. Select the **Users** tab, click on the user. The required infrastructure permissions vary depending on what type of [cluster infrastructure provider](/docs/containers?topic=containers-infrastructure_providers) you use, classic or VPC.
        - For classic clusters
            1. In the **API keys** pane, verify that the user has a **Classic infrastructure API key**, or click **Create an IBM Cloud API key**. For more information, see [Managing classic infrastructure API keys](/docs/account?topic=account-classic_keys#classic_keys).
            2. Click the **Classic infrastructure** tab and then click the **Permissions** tab.
            3. If the user doesn't have each category checked, you can use the **Permission sets** drop-down list to assign the **Super User** role. Or you can expand each category and give the user the required [infrastructure permissions](/docs/openshift?topic=openshift-access_reference#infra).
        - For VPC clusters, assign the user the [**Administrator** platform access role for VPC Infrastructure](/docs/vpc?topic=vpc-iam-getting-started).


## Understanding access to the infrastructure portfolio
{: #understand_infra}

Determine whether your account has access to the IBM Cloud infrastructure portfolio and learn about how {{site.data.keyword.openshiftlong_notm}} uses the API key to access the portfolio.
{: shortdesc}

**Does the classic or VPC infrastructure provider for my cluster affect what access I need to the portfolio?**

Access to {{site.data.keyword.cloud_notm}} infrastructure works differently in classic and VPC clusters. Infrastructure resources for classic clusters are created in a separate {{site.data.keyword.cloud_notm}} infrastructure account. In most cases, your Pay-As-You-Go or Subscription account is linked to the {{site.data.keyword.cloud_notm}} infrastructure account so that account owners can access classic {{site.data.keyword.cloud_notm}} infrastructure automatically. To authorize other users to access classic compute, storage, and networking resources, you must assign [classic infrastructure roles](/docs/openshift?topic=openshift-access_reference#infra).

VPC infrastructure resources are integrated into IAM and as such, you must have the {{site.data.keyword.cloud_notm}} IAM **Administrator** platform access role to the [**VPC Infrastructure** service](/docs/vpc?topic=vpc-iam-getting-started) to create and list VPC resources.

For both [classic and VPC clusters](/docs/containers?topic=containers-infrastructure_providers), the credentials to access infrastructure resources are stored in an API key for the region and resource group of the cluster. To create and manage clusters after the infrastructure permissions are set, assign users IAM access roles to {{site.data.keyword.openshiftlong_notm}}.

Unlike classic, VPC does not support manually setting infrastructure credentials (`ibmcloud oc credential set`) to use another IBM Cloud infrastructure account to provision worker nodes. You must use your {{site.data.keyword.cloud_notm}} account's linked infrastructure account.
{: important}

**Does my account already have access to the IBM Cloud infrastructure portfolio?**

To access the IBM Cloud infrastructure portfolio, you use an {{site.data.keyword.cloud_notm}} Pay-As-You-Go or Subscription account. If you have a different type of account, view your options in the following list.

Lite accounts
: Lite accounts cannot provision clusters. To create a standard cluster, upgrade your Lite account to an {{site.data.keyword.cloud_notm}} [Pay-As-You-Go](/docs/account?topic=account-accounts#paygo) or [Subscription](/docs/account?topic=account-accounts#subscription-account) account.

Pay-As-You-Go
:   You can create standard clusters. Use an API key to set up infrastructure permissions for your clusters.

To use a different classic infrastructure account for classic clusters, [manually set {{site.data.keyword.cloud_notm}} infrastructure credentials for your {{site.data.keyword.cloud_notm}} account](/docs/openshift?topic=openshift-access-creds#credentials). You cannot set up your {{site.data.keyword.cloud_notm}} account to use the VPC infrastructure of a different account.
{: tip}

Subscription
:   Subscription accounts come with access to the infrastructure portfolio. You can create standard clusters. Use an API key to set up infrastructure permissions for your clusters. 

To use a different classic infrastructure account for classic clusters, [manually set](/docs/openshift?topic=openshift-access-creds#credentials) {{site.data.keyword.cloud_notm}} infrastructure credentials for your {{site.data.keyword.cloud_notm}} account. You cannot set up your {{site.data.keyword.cloud_notm}} account to use the VPC infrastructure of a different account.
{: tip}

IBM Cloud infrastructure accounts
:   If you have an IBM Cloud infrastructure without an {{site.data.keyword.cloud_notm}} account, create an {{site.data.keyword.cloud_notm}} [Pay-As-You-Go](/docs/account?topic=account-accounts#paygo) or [Subscription](/docs/account?topic=account-accounts#subscription-account) account. You have two separate IBM Cloud infrastructure accounts and billing. By default, your new {{site.data.keyword.cloud_notm}} account uses the new infrastructure account. To continue using the previous classic infrastructure account, manually set the credentials. You can manually set credentials for only classic clusters, not VPC clusters.


## Accessing the infrastructure portfolio with your {{site.data.keyword.cloud_notm}} Pay-As-You-Go or Subscription account
{: #default_account}

{{site.data.keyword.cloud_notm}} Pay-As-You-Go and Subscription accounts are automatically set up with an IBM Cloud infrastructure account that allows access to classic infrastructure resources. The API key that you set is used to order infrastructure resources from this infrastructure account, such as new worker nodes or VLANs.
{: shortdec}

You can find the current API key owner by running [`ibmcloud oc api-key info --cluster <cluster>`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_api_key_info). If you find that you need to update the API key that is stored for a region, you can do so by running the [`ibmcloud oc api-key reset --region <region>`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_api_key_reset) command. This command requires the {{site.data.keyword.openshiftlong_notm}} admin access policy and stores the API key of the user that executes this command in the account.

Be sure that you want to reset the key and understand the impact to your app. The key is used in several different places and can cause breaking changes if it's unnecessarily changed.
{: note}

**Before you begin**:
- If the account owner does not set up the API key, [ensure that the user who sets the API key has the correct permissions](#owner_permissions).
- Consider using a functional ID user for the API key owner instead of a personal user. In case the person leaves the team, the functional ID user remains the API key owner.
- [Access your {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-access_cluster).

To set up the API key to access the IBM Cloud infrastructure portfolio:

1. Create an API key for the region and resource group that the cluster is in.
    1. Log in to the command line with the user whose infrastructure permissions you want to use.
    2. Target the resource group where you want to set the API key. If you do not target a resource group, the API key is set for the default resource group.
        ```sh
        ibmcloud target -g <resource_group_name>
        ```
        {: pre}

    3. Set up the API key that has the user's permissions for the region.
        ```sh
        ibmcloud oc api-key reset --region <region>
        ```
        {: pre}    

    4. Verify that the API key is set up.
        ```sh
        ibmcloud oc api-key info --cluster <cluster_name_or_ID>
        ```
        {: pre}

2. [Create a cluster](/docs/containers?topic=containers-clusters). To create the cluster, the API key credentials that you set up for the region and resource group are used.


## Accessing a different classic infrastructure account
{: #credentials}

Instead of using the default linked IBM Cloud infrastructure account to order infrastructure for clusters within a region, you might want to use a different IBM Cloud infrastructure account that you already have. You can link this infrastructure account to your {{site.data.keyword.cloud_notm}} account by using the [`ibmcloud oc credential set`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_credentials_set) command. The IBM Cloud infrastructure credentials are used instead of the default Pay-As-You-Go or Subscription account's credentials that are stored for the region.
{: shortdesc}

You can manually set infrastructure credentials to a different account only for classic clusters, not for VPC clusters.
{: note}

The IBM Cloud infrastructure credentials that are set by the `ibmcloud oc credential set` command persist after your session ends. If you remove IBM Cloud infrastructure credentials that were manually set with the [`ibmcloud oc credential unset --region <region>`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_credentials_unset) command, the credentials of the Pay-As-You-Go or Subscription account are used instead. However, this change in infrastructure account credentials might cause [orphaned clusters](/docs/openshift?topic=openshift-worker_infra_errors#orphaned).
{: important}

**Before you begin**:
- If you are not using the account owner's credentials, [ensure that the user whose credentials you want to set for the API key has the correct permissions](#owner_permissions).
- [Access your {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-access_cluster).

To set infrastructure account credentials to access the IBM Cloud infrastructure portfolio:

1. Get the infrastructure account that you want to use to access the IBM Cloud infrastructure portfolio. You have different options that depend on your [current account type](#understand_infra).

2. Set the infrastructure API credentials with the user for the correct account.

    1. Get the user's infrastructure API credentials. Note that the credentials differ from the IBMid.

        1. From the [{{site.data.keyword.cloud_notm}}](https://cloud.ibm.com/){: external} console, select **Manage** > **Access (IAM)** > **Users** table and click the username.

        2. In the **API Keys** section, find or create a classic infrastructure API key.   

    2. Set the infrastructure API credentials to use.
        ```sh
        ibmcloud oc credential set --infrastructure-username <infrastructure_API_username> --infrastructure-api-key <infrastructure_API_authentication_key> --region <region>
        ```
        {: pre}

    3. Verify that the correct credentials are set.
        ```sh
        ibmcloud oc credential get --region <region>
        ```
        {: pre}

        Example output
        ```sh
        Infrastructure credentials for user name user@email.com set for resource group default.
        ```
        {: screen}

3. [Create a cluster](/docs/containers?topic=containers-clusters). To create the cluster, the infrastructure credentials that you set for the region and resource group are used.

4. Verify that your cluster uses the infrastructure account credentials that you set.
    1. Open the [{{site.data.keyword.cloud_notm}} clusters console](https://cloud.ibm.com/kubernetes/clusters){: external} and select your cluster. 
    2. In the Overview tab, look for an **Infrastructure User** field. 
    3. If you see that field, you do not use the default infrastructure credentials that come with your Pay-As-You-Go or Subscription account in this region. Instead, the region is set to use the different infrastructure account credentials that you set.


## Customizing classic infrastructure permissions
{: #infra_access}

When you assign the **Super User** infrastructure role to the admin or functional ID that sets the API key or whose infrastructure credentials are set, other users within the account share the API key or credentials for performing infrastructure actions. You can then control which infrastructure actions the users can perform by assigning the appropriate [{{site.data.keyword.cloud_notm}} IAM platform access role](/docs/openshift?topic=openshift-users#checking-perms). You don't need to edit the user's IBM Cloud infrastructure permissions.
{: shortdesc}

Classic infrastructure permissions apply only to classic clusters. For VPC clusters, see [Granting user permissions for VPC resources](/docs/vpc?topic=vpc-managing-user-permissions-for-vpc-resources).
{: note}

For compliance, security, or billing reasons, you might not want to give the **Super User** infrastructure role to the user who sets the API key or whose credentials are set with the `ibmcloud oc credential set` command. However, if this user doesn't have the **Super User** role, then infrastructure-related actions, such as creating a cluster or reloading a worker node, can fail. Instead of using {{site.data.keyword.cloud_notm}} IAM platform access roles to control users' infrastructure access, you must set specific IBM Cloud infrastructure permissions for users.

For example, if your account is not VRF-enabled, your IBM Cloud infrastructure account owner must turn on VLAN spanning. The account owner can also assign a user the **Network > Manage Network VLAN Spanning** permission so that the user can enable VLAN spanning. For more information, see [VLAN spanning for cross-VLAN communication](/docs/openshift?topic=openshift-subnets#basics_segmentation).

### Assigning infrastructure access through the console
{: #infra_console}

Classic infrastructure permissions apply only to classic clusters. For VPC clusters, see [Granting user permissions for VPC resources](/docs/vpc?topic=vpc-managing-user-permissions-for-vpc-resources).
{: note}

Before you begin:
- Make sure that you have the **Super User** role and all device access. You can't grant a user access that you don't have.
- Review the [required and suggested classic infrastructure permissions](/docs/openshift?topic=openshift-access_reference#infra) to know what to assign the personal user or functional ID.

To customize classic infrastructure permissions through the console:

1. Log in to the [{{site.data.keyword.cloud_notm}} console](https://cloud.ibm.com){: external}. From the menu bar, select **Manage > Access (IAM)**.
2. Click the **Users** page, and then click the name of the user that you want to set permissions for.
3. Click the **Classic infrastructure** tab, and then click the **Permissions** tab.
4. Customize the user's access. The permissions that users need depend on what infrastructure resources they need to use. You have two options for assigning access:
    - Use the **Permission sets** drop-down list to assign one of the following predefined roles. After selecting a role, click **Set**.
        - **View Only** gives the user permissions to view infrastructure details only.
        - **Basic User** gives the user some, but not all, infrastructure permissions.
        - **Super User** gives the user all infrastructure permissions.
    - Select individual permissions for each category. To review permissions that are needed to perform common tasks in {{site.data.keyword.openshiftlong_notm}}, see [User access permissions](/docs/openshift?topic=openshift-access_reference#infra).
5. Click **Save**.
6. In the **Device** tab, select the devices to grant access to.
    - In the **Select type** group, you can grant access to all bare metal, dedicated, and virtual servers so that users can work with all [flavors for worker nodes](/docs/openshift?topic=openshift-planning_worker_nodes#planning_worker_nodes).
    - In the **Enable future access** group, you can grant the user access to all future bare metal, dedicated, and virtual servers.
    - In the table of devices, make sure that the appropriate devices are selected.
7. To save your changes, click **Set**.
8. **Important**: If you are assigning permissions so that a user can manage clusters and worker nodes, you must assign the user access for working with support cases.
    1. Click the **Access policies** tab, and then click **Assign access**.
    2. Click the **Account management** card.
    3. Select **Support Center**.
    4. To allow the user to view, add, and edit support cases, select **Administrator**.
    5. Click **Assign**.

Downgrading permissions? The action can take a few minutes to complete.
{: tip}

### Assigning infrastructure access through the CLI
{: #infra_cli}

Classic infrastructure permissions apply only to classic clusters. For VPC clusters, see [Granting user permissions for VPC resources](/docs/vpc?topic=vpc-managing-user-permissions-for-vpc-resources).
{: note}

Before you begin:
* Make sure that you are the account owner or have **Super User** and all device access. You can't grant a user access that you don't have.
* Review the [required and suggested classic infrastructure permissions](/docs/openshift?topic=openshift-access_reference#infra).

To customize classic infrastructure permissions through the CLI:

1. Check whether the credentials for classic infrastructure access for {{site.data.keyword.openshiftlong_notm}} in the region and resource group have any missing required or suggested permissions.
    ```sh
    ibmcloud oc infra-permissions get --region <region>
    ```
    {: pre}

    Example output if classic infrastructure access is based on an API key.
    ```sh
    ...with infrastructure access set up by linked account API key.
    ```
    {: screen}

    Example output if classic infrastructure access is based on manually-set credentials.
    ```sh
    ...with infrastructure access set up by manually-set IaaS credentials.
    ```
    {: screen}

2. Get the user whose classic infrastructure credentials are used.
    - **API key**: Check the API key that is used for the region and resource group of the cluster. Note the **Name** and **Email** of the API key owner in the output of the following command.
        ```sh
        ibmcloud oc api-key info --cluster <cluster_name_or_ID>
        ```
        {: pre}

    - **Manually-set credentials**: Get the username in the output of the following command.    
        ```sh
        ibmcloud oc credential get --region <region>
        ```
        {: pre}

    Need to change the infrastructure credential owner? Check out the `ibmcloud oc api-key reset` [command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_api_key_reset) or the `ibmcloud oc credential set` [command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_credentials_set).
    {: tip}

3. List the users in your classic infrastructure account and note the **id** of the user whose credentials are set manually or by the API key.
    ```sh
    ibmcloud sl user list
    ```
    {: pre}

4. List the current classic infrastructure permissions that the user has. Note the **`KeyName`** of the permission that you want to change.
    ```sh
    ibmcloud sl user permissions <user_id>
    ```
    {: pre}

5. Edit the permission of the user. For the `--enable` flag, enter `true` to assign the permission or `false` to remove the permission.
    ```sh
    ibmcloud sl user permission-edit <user_id> --permission <permission_keyname> --enable (true|false)
    ```
    {: pre}

    To assign or remove user access to all permissions:
    ```sh
    ibmcloud sl user permission-edit <user_id> --permission ALL --enable (true|false)
    ```
    {: pre}

6. For individual required or suggested permissions, see the [Infrastructure roles](/docs/openshift?topic=openshift-access_reference#infra) table.




