---

copyright: 
  years: 2014, 2025
lastupdated: "2025-11-21"


keywords: openshift, {{site.data.keyword.openshiftlong_notm}}, clusters, worker nodes, worker pools, tag, label

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}




# Tagging and labeling clusters and services
{: #worker-tag-label}

When you create a cluster, services or resources that are created and used by that cluster are tagged to indicate which cluster is using them. You can also manually tag {{site.data.keyword.openshiftlong_notm}} clusters to help manage your {{site.data.keyword.cloud_notm}} resources. For example, you might add `key:value` tags to your cluster and other cloud resources so that your billing department track resources, such as `costctr:1234`. Tags are visible account-wide. For more information, see [Working with tags](/docs/account?topic=account-tag).
{: shortdesc}



- Service tags added to services used by {{site.data.keyword.openshiftlong_notm}} are in the format `containers-kubernetes:cluster:CLUSTER-ID`.
- Service tags are added asynchronously after services are provisioned and can take some time to appear.
- Service tags cannot be modified or deleted by the customer only the service that creates them.
- User tags are added manually by users in the account.
- The following resources are tagged with {{site.data.keyword.openshiftlong_notm}} service tags.
	- Secondary storage volumes.

Tags are not the same thing as Kubernetes labels. [Kubernetes labels](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/){: external} are `key:value` pairs that can be used as selectors for the resources that are in your cluster, such as adding a label to worker pool to [deploy an app to only certain worker nodes](/docs/openshift?topic=openshift-deploy_app#node_affinity). Tags are an {{site.data.keyword.cloud_notm}} tool that you can use to filter your {{site.data.keyword.cloud_notm}} resources, such as clusters, storage devices, or {{site.data.keyword.watson}} services.
{: note}

Do not include personal information in your tags. Learn more about [securing your personal information](/docs/containers?topic=containers-security#pi) when you work with Kubernetes resources.
{: important}


## Finding {{site.data.keyword.BluSoftlayer_notm}} resources with service tags from a specific cluster
{: #finding-services-tags}

1. Get your cluster ID.
    ```sh
    ibmcloud oc cluster ls
    ```
    {: pre}

1. To find a list of services that were created or are being used by that cluster, run the following command.
    ```sh
    ibmcloud resource search 'service_tags:"containers-kubernetes:cluster:CLUSTER-ID"'
    ```
    {: pre}

    Example command.
    ```sh
    ibmcloud resource search 'service_tags:"containers-kubernetes:cluster:d4f0si2w06ftldhe3s80"'
    ```
    {: pre}		

## Manually adding user tags to clusters in the console
{: #add-tags-console}
{: ui}

1. Log in to the [{{site.data.keyword.cloud_notm}} clusters console](https://cloud.ibm.com/kubernetes/clusters){: external}.
1. Select a cluster with existing tags.
1. Next to the cluster name and status, click the **Edit tags** pencil icon. If your cluster does not have any existing tags, you don't have an **Edit tags** pencil icon. Instead, use the [resource list](/docs/account?topic=account-tag) or CLI.

1. Enter the tag that you want to add to your cluster. To assign a key-value pair, use a colon such as `costctr:1234`.


## Manually adding user tags to clusters by using the CLI
{: #add-tags-cli}
{: cli}

1. Log in to the [{{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-ibmcloud_cli#ibmcloud_login){: external}.
    ```sh
    ibmcloud login [--sso]
    ```
    {: pre}

1. [Tag your cluster](/docs/cli?topic=cli-ibmcloud_commands_resource#ibmcloud_resource_tag_attach). Replace the `--resource-name` with the name of your cluster. To list available clusters, run `ibmcloud oc cluster ls`. If you want to check your existing tags so as not to duplicate any, run `ibmcloud resource tags`.

    ```sh
    ibmcloud resource tag-attach --resource-name <cluster_name> --tag-names <tag1,tag2>
    ```
    {: pre}
    
    If you have more than one resource of the same name in your {{site.data.keyword.cloud_notm}} account, the error message lists the resource CRNs and details, and instructs you to try again with the `--resource-id`option.
    {: note}




## Manually adding labels to existing worker pools
{: #worker_pool_labels}

You can assign a worker pool a label when you create the worker pool, or later by following these steps. After a worker pool is labeled, all existing and subsequent worker nodes get this label. You might use labels to deploy specific workloads only to worker nodes in the worker pool, such as [edge nodes for load balancer network traffic](/docs/openshift?topic=openshift-edge).
{: shortdesc}

Do not include personal information in your labels. Learn more about [securing your personal information](/docs/containers?topic=containers-security#pi) when you work with Kubernetes resources.
{: important}

Before you begin: [Access your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-access_cluster).

1. List the worker pools in your cluster.
    ```sh
    ibmcloud oc worker-pool ls --cluster <cluster_name_or_ID>
    ```
    {: pre}

1. List the existing custom labels on worker nodes in the worker pool that you want to label.
    ```sh
    ibmcloud oc worker-pool get --cluster <cluster_name_or_ID> --worker-pool <pool>
    ```
    {: pre}

1. Label the worker pool with a `key=value` label. When you set a worker pool label, all the existing custom labels are replaced. To keep any existing custom labels on the worker pool, include those labels with this option.

    You can also rename an existing label by assigning the same key a new value. However, don't modify the worker pool or worker node labels that are provided by default because these labels are required for worker pools to function properly. Modify only custom labels that you previously added.
    {: important}

    ```sh
    ibmcloud oc worker-pool label set --cluster <cluster_name_or_ID> --worker-pool <worker_pool_name_or_ID> --label <key=value>
    ```
    {: pre}

    Example to set `<key>: <value>` as a new custom label in a worker pool with existing labels `team: DevOps` and `app: test`:
    ```sh
    ibmcloud oc worker-pool label set --cluster <cluster_name_or_ID> --worker-pool <worker_pool_name_or_ID> --label <key=value> --label team=DevOps --label app=test
    ```
    {: pre}

1. Verify that the worker pool and worker node have the `key=value` label that you assigned.
    *   To check worker pools:
        ```sh
        ibmcloud oc worker-pool get --cluster <cluster_name_or_ID> --worker-pool <worker_pool_name_or_ID>
        ```
        {: pre}

    *   To check worker nodes:
        1. List the worker nodes in the worker pool and note the **Private IP**.
            ```sh
            ibmcloud oc worker ls --cluster <cluster_name_or_ID> --worker-pool <worker_pool_name_or_ID>
            ```
            {: pre}

        1. Review the **Labels** field of the output.
            ```sh
            oc describe node <worker_node_private_IP>
            ```
            {: pre}

            Example output for an added label (`app=test`):
            ```sh
            Labels:   app=test
            arch=amd64
            ...
            ```
            {: screen}

            Example output for a removed label (the `app=test` label is gone):
            ```sh
            Labels:   arch=amd64
            ...
            ```
            {: screen}            

1. **Optional**: To remove an individual label from a worker pool, you can run the `ibmcloud oc worker-pool label set` command with only the custom labels that you want to keep. To remove all custom labels from a worker pool, you can run the `ibmcloud oc worker-pool label rm` command.

    Do not remove the worker pool and worker node labels that are provided by default because these labels are required for worker pools to function properly. Remove only custom labels that you previously added.
    {: important}

    Example to keep only the `team: DevOps` and `app: test` labels and remove all other custom labels from a worker pool:
    ```sh
    ibmcloud oc worker-pool label set --cluster <cluster_name_or_ID> --worker-pool <worker_pool_name_or_ID> --label team=DevOps --label app=test
    ```
    {: pre}

    Example to remove all custom label from a worker pool:
    ```sh
    ibmcloud oc worker-pool label rm --cluster <cluster_name_or_ID> --worker-pool <worker_pool_name_or_ID>
    ```
    {: pre}

After you label your worker pool, you can use the [label in your app deployments](/docs/openshift?topic=openshift-app#label) so that your workloads run on only these worker nodes, or [taints](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/){: external} to prevent deployments from running on these worker nodes.
