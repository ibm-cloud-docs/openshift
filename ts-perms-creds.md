---

copyright: 
  years: 2014, 2024
lastupdated: "2024-08-20"


keywords: kubernetes, openshift, user permissions, infrastructure credentials

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Resolving permission and credential errors
{: #ts-perms-creds}


When you try to make changes to your cluster, such as creating or deleting worker nodes or other components, you receive an error message similar to one of the following examples. 
{: tsSymptoms}

```sh
The infrastructure authentication credentials are not authorized for the request.
```
{: screen}

```sh
We were unable to connect to your Softlayer account.
Creating a standard cluster requires that you have either a
Pay-As-You-Go account that is linked to an IBM Cloud infrastructure
account term or that you have used the Kubernetes service
CLI to set your Infrastructure API keys.
```
{: screen}

```sh
'Item' must be ordered with permission.
```
{: screen}

```sh
The worker node instance '<ID>' can't be found. Review '<provider>' infrastructure user permissions.
```
{: screen}

```sh
The worker node instance can't be found. Review '<provider>' infrastructure user permissions.
```
{: screen}

```sh
The worker node instance can't be identified. Review '<provider>' infrastructure user permissions.
```
{: screen}

```sh
The IAM token exchange request failed with the message: <message>
IAM token exchange request failed: <message>
```
{: screen}

```sh
The cluster could not be configured with the registry. Make sure that you have the Administrator role for Container Registry.
```
{: screen}


The infrastructure credentials that are set for the region and resource group are missing the appropriate [infrastructure permissions](/docs/openshift?topic=openshift-iam-platform-access-roles), or the credentials are not recognized.
{: tsCauses}

There are multiple reasons why this can occur. 

- You do not have the required infrastructure permissions. 

- The resource group and region are mismatched. 
    - Credentials and the IAM API key are set to a region and a resource group. The region is specified when you run the `ibmcloud oc credential set` command. The resource group applied is whichever resource group is targeted when you run this command. If you do not explicitly target a resource group with the [`ibmcloud target`](/docs/cli?topic=cli-ibmcloud_cli#ibmcloud_target) command before you run `ibmcloud oc credential set`, it is possible that the API key's resource group is not the one you expected, resulting is mismatched credentials that are not recognized. 

- Credentials were added to or removed from the cluster.
    - If you created a cluster with a linked [IBM Cloud infrastructure account](/docs/openshift?topic=openshift-classic-credentials) and then later added or removed  credentials with the `ibmcloud oc credential set` or `ibmcloud oc credential unset`, the credentials might not match the specifications for the linked account. This can result in the credentials being unrecognized. 

The account owner must set up the infrastructure account credentials properly. The credentials depend on what type of infrastructure account you are using.
{: tsResolve}

Before you begin, [Log in to your account. If applicable, target the appropriate resource group. Set the context for your cluster.](/docs/containers?topic=containers-access_cluster).

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

        For console and CLI commands to assign these permissions, see [Classic infrastructure roles](/docs/openshift?topic=openshift-iam-platform-access-roles).
        {: tip}

    2. Make sure that the [infrastructure credentials owner for the API key or the manually set account has the correct permissions](/docs/openshift?topic=openshift-iam-platform-access-roles).
        You can change the [API key](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_api_key_reset) or [manually set](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_credentials_set) infrastructure credentials owner for the region and resource group.
        {: note}
        
3. Try again to perform the infrastructure operation, such as deleting the cluster or worker node. If you still run into the permissions or credentials error, review these additional troubleshooting pages.
    1. If the worker node is not removed, review the [**State** and **Status** fields](/docs/openshift?topic=openshift-debug_worker_nodes) and the [common issues with worker nodes](/docs/openshift?topic=openshift-common_worker_nodes_issues) to continue debugging.
    1. If you manually set credentials and still can't see the cluster's worker nodes in your infrastructure account, you might check whether the [cluster is orphaned](#orphaned).

1. If the issue persists, gather the following information to submit to IBM Cloud support. Save the outputs from each command. Make sure that you have the correct resource group targeted with the `ibmcloud target -g <resource_group>` command. 

    1. API key info.

        ```sh
        ibmcloud ks api-key info --cluster <cluster_name_or_id>
        ```
        {: pre}
    
    1. Account details.

        ```sh
        ibmcloud target
        ```
        {: pre}
    
    1. Credential details for the expected region and resource group.

        ```sh
        ibmcloud oc credential get --region <region>
        ```
        {: pre}

    1. Infrastructure permissions details.

        ```sh
        ibmcloud oc infra-permissions get --region <region>
        ```
        {: pre}

1. [Open an issue with IBM Cloud support](/docs/openshift?topic=openshift-get-help. Be sure to include all the information and command outputs gathered in the previous step. 

## Invalid API key
{: #invalid_apikey}

[Classic infrastructure]{: tag-classic-inf}

When you try to complete an action that requires you to specify an API key, you get an error similar to the following. 
{: tsSymptoms}

```sh
Error: SoftLayer_Exception_User_Customer_Unauthorized: Invalid API key
```
{: screen}

Additionally, running the `ibmcloud ks api-key reset` command does not resolve the issue and the output of the `ibmcloud oc infra-permissions get` command does not indicate any problems with permissions. 

There are multiple reasons why this error can occur.
{: tsCauses}

- The action you are attempting requires you to specify a classic infrastructure API key rather than a Kubernetes API key. If a classic infrastructure API key is set for the region, it takes precedence over all other credentials. 

- The classic infrastructure API key you specified does not exist. It might have been deleted, or the API key owner might have left the organization. 

If you know the classic infrastructure API key, specify it. If you do not know the infrastructure API key or you think it might have been deleted, follow these steps.
{: tsResolve}

1. [Reset the classic infrastructure API key](/docs/containers?topic=containers-kubernetes-service-cli#cs_credentials_set).

    ```sh
    ibmcloud oc credential set classic --infrastructure-api-key API_KEY --infrastructure-username USERNAME --region REGION [-q]
    ```
    {: pre}

2. Run the command to [update the credential on the cluster](/docs/containers?topic=containers-kubernetes-service-cli#cs_api_key_reset). 

    ```sh
    ibmcloud oc api-key reset --region REGION [-q]
    ```
    {: pre}


3. Try again to complete the action. 




