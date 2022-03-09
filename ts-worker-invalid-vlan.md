---

copyright: 
  years: 2014, 2022
lastupdated: "2022-03-08"

keywords: openshift

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}


# Classic: Why can't I add worker nodes with an invalid VLAN ID?
{: #suspended}
{: support}

**Infrastructure provider**: ![Classic infrastructure provider icon.](images/icon-classic-2.svg) Classic


Your {{site.data.keyword.cloud_notm}} account was suspended, or all worker nodes in your cluster were deleted. After the account is reactivated, you can't add worker nodes when you try to resize or rebalance your worker pool. You see an error message similar to the following:
{: tsSymptoms}

```
SoftLayerAPIError(SoftLayer_Exception_Public): Could not obtain network VLAN with id #123456.
```
{: screen}


When an account is suspended, the worker nodes within the account are deleted. If a cluster has no worker nodes, IBM Cloud infrastructure reclaims the associated public and private VLANs. However, the cluster worker pool still has the previous VLAN IDs in its metadata and uses these unavailable IDs when you rebalance or resize the pool. The nodes fail to create because the VLANs are no longer associated with the cluster.
{: tsCauses}


You can [delete your existing worker pool](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_pool_rm), then [create a new worker pool](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_pool_create).
{: tsResolve}

Alternatively, you can keep your existing worker pool by ordering new VLANs and using these to create new worker nodes in the pool.

Before you begin: [Log in to your account. If applicable, target the appropriate resource group. Set the context for your cluster.](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure)

1. To get the zones that you need new VLAN IDs for, note the **Location** in the following command output. **Note**: If your cluster is a multizone, you need VLAN IDs for each zone.

    ```sh
    ibmcloud oc cluster ls
    ```
    {: pre}

2. Get a new private and public VLAN for each zone that your cluster is in by [contacting {{site.data.keyword.cloud_notm}} support](/docs/vlans?topic=vlans-ordering-premium-vlans#ordering-premium-vlans).

3. Note the new private and public VLAN IDs for each zone.

4. Note the name of your worker pools.

    ```sh
    ibmcloud oc worker-pool ls --cluster <cluster_name_or_ID>
    ```
    {: pre}

5. Use the `zone network-set` [command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_zone_network_set) to change the worker pool network metadata.

    ```sh
    ibmcloud oc zone network-set --zone <zone> --cluster <cluster_name_or_ID> -- worker-pool ls <worker-pool> --private-vlan <private_vlan_ID> --public-vlan <public_vlan_ID>
    ```
    {: pre}

6. **Multizone cluster only**: Repeat **Step 5** for each zone in your cluster.

7. Rebalance or resize your worker pool to add worker nodes that use the new VLAN IDs. For example:

    ```sh
    ibmcloud oc worker-pool resize --cluster <cluster_name_or_ID> --worker-pool <worker_pool> --size-per-zone <number_of_workers_per_zone>
    ```
    {: pre}

8. Verify that your worker nodes are created.

    ```sh
    ibmcloud oc worker ls --cluster <cluster_name_or_ID> --worker-pool <worker_pool>
    ```
    {: pre}






