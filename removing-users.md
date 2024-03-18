---

copyright: 
  years: 2022, 2024
lastupdated: "2024-03-15"


keywords: openshift, kubernetes, infrastructure, rbac, policy

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}


# Removing users
{: #removing-user-permissions}

If a user no longer needs specific access permissions, or if the user is leaving your organization, the {{site.data.keyword.cloud_notm}} account owner can remove that user's permissions.
{: shortdesc}

## Checking whether the user's credentials are used for infrastructure permissions
{: #removing_check_infra}

Before you remove a user's specific access permissions or remove a user from your account completely, ensure that the user's infrastructure credentials are not used to set the API key or for the `ibmcloud oc credential set` command. Otherwise, the other users in the account might lose access to the IBM Cloud infrastructure portal and infrastructure-related commands might fail.
{: shortdesc}

To avoid this issue for future users, consider using a functional ID user for the API key owner instead of a personal user. In case the person leaves the team, the functional ID user remains the API key owner.
{: tip}

1. Target your CLI context to a region and resource group where you have clusters.
    ```sh
    ibmcloud target -g <resource_group_name> -r <region>
    ```
    {: pre}

2. Check the owner of the API key or infrastructure credentials set for that region and resource group.
    ```sh
    ibmcloud oc api-key info --cluster <cluster_name_or_id>
    ```
    {: pre}

    ```sh
    ibmcloud oc credential get --region <region>
    ```
    {: pre}

3. **API key**: If the user's username is returned, use another user's credentials to set the API key.
    1. [Invite a functional ID user](/docs/account?topic=account-iamuserinv) to your {{site.data.keyword.cloud_notm}} account to use to set the API key infrastructure credentials, instead of a personal user. In case a person leaves the team, the functional ID user remains the API key owner.
    2. [Ensure that the functional ID user who sets the API key has the correct permissions](/docs/openshift?topic=openshift-iam-platform-access-roles).
    3. Log in as the functional ID.
        ```sh
        ibmcloud login
        ```
        {: pre}

    4. Change the infrastructure credentials to the functional ID user.
        ```sh
        ibmcloud oc api-key reset --region <region>
        ```
        {: pre}

    5. Refresh the clusters in the region to pick up on the new API key configuration.
        ```sh
        ibmcloud oc cluster master refresh -c <cluster_name_or_ID>
        ```
        {: pre}

4. **Infrastructure account**: If the user's username is returned as the owner of the infrastructure account, migrate your existing clusters to a different infrastructure account before removing the user. For each cluster that the user created, follow these steps:
    1. Check which infrastructure account the user used to provision the cluster.
        1. In the **Worker Nodes** tab, select a worker node and note its **ID**.
        2. Open the menu ![Menu icon](../icons/icon_hamburger.svg "Menu icon") and click **Classic Infrastructure**.
        3. From the infrastructure navigation pane, click **Devices > Device List**.
        4. Search for the worker node ID that you previously noted.
        5. If you don't find the worker node ID, the worker node is not provisioned into this infrastructure account. Switch to a different infrastructure account and try again.
    2. Determine what happens to the infrastructure account that the user used to provision the clusters after the user leaves.
        * If the user does not own the infrastructure account, then other users have access to this infrastructure account and it persists after the user leaves. You can continue to work with these clusters in your account. Make sure that at least one other user has the [**Administrator** platform access role](/docs/openshift?topic=openshift-iam-platform-access-roles) for the clusters.
        * If the user owns the infrastructure account, then the infrastructure account is deleted when the user leaves. You can't continue to work with these clusters. To prevent the cluster from becoming orphaned, the user must delete the clusters before the user leaves. If the user leaves but the clusters were not deleted, you must use the `ibmcloud oc credential set` command to change your infrastructure credentials to the account that the cluster worker nodes are provisioned in, and delete the cluster. For more information, see [Unable to modify or delete infrastructure in an orphaned cluster](/docs/openshift?topic=openshift-cluster_infra_errors).
5. Repeat these steps for each combination of resource groups and regions where you have clusters.


## Removing {{site.data.keyword.cloud_notm}} IAM platform permissions and the associated pre-defined RBAC permissions
{: #remove_iam_rbac}

1. Log in to the [{{site.data.keyword.cloud_notm}} console](https://cloud.ibm.com/){: external}. From the menu bar, select **Manage > Access (IAM)**.
2. Click the **Users** page, and then click the name of the user that you want to remove permissions from.
3. In the table entry for the user, click the **Actions menu** ![Action menu icon](../icons/action-menu-icon.svg "Action menu icon") **> Remove user**.
4. When {{site.data.keyword.cloud_notm}} IAM platform permissions are removed, the user's permissions are also automatically removed from the associated predefined RBAC roles. To update the RBAC roles with the changes, run `ibmcloud oc cluster config`. However, if you created [custom RBAC roles or cluster roles](#rbac), you must remove the user from the `.yaml` files for those RBAC role bindings or cluster role bindings. See steps to remove custom RBAC permissions in the next section.

### Removing custom RBAC permissions
{: #remove_custom_rbac}

If you don't need custom RBAC permissions anymore, you can remove them.

1. Open the `.yaml` file for the role binding or cluster role binding that you created.
2. In the `subjects` section, remove the section for the user.
3. Save the file.
4. Apply the changes in the role binding or cluster role binding resource in your cluster.
    ```sh
    oc apply -f my_role_binding.yaml
    ```
    {: pre}

