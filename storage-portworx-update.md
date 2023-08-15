---

copyright: 
  years: 2014, 2023
lastupdated: "2023-08-15"

keywords: portworx, openshift

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}



# Updating Portworx in your cluster
{: #storage_portworx_update}

Beginning with version `2.12` Portworx uses an operator-based deployment model instead of the Helm based model use in version `2.11` and earlier. If you are updating from Portworx `2.11` to version `2.12`, follow the migration steps in the [Portworx documentation](https://docs.portworx.com/operations/operate-kubernetes/migrate-daemonset/){: external}.
{: important}

Looking to update Portworx in a Classic cluster? For more information, see [Updating Classic worker nodes](/docs/openshift?topic=openshift-update&interface=ui#worker_node).


## VPC: Updating worker nodes with Portworx volumes
{: #portworx_vpc_up}

[Virtual Private Cloud]{: tag-vpc} 

When you update a worker node in a VPC cluster, the worker node is removed from your cluster and replaced with a new worker node. If Portworx volumes are attached to the worker node that you replaced, you must attach the volumes to the new worker node.
{: shortdesc}

Update only one worker node at a time. When the worker node update is complete, attach your {{site.data.keyword.block_storage_is_short}} and restart the Portworx pod.
{: important}


1. [Enter maintenance mode on the worker nodes that you want to update](https://docs.portworx.com/portworx-enterprise/operations/operate-kubernetes/troubleshooting/enter-maintenance-mode){: external}.

2. [Update your VPC worker nodes](/docs/containers?topic=containers-update#vpc_worker_node).

3. [Attach raw {{site.data.keyword.block_storage_is_short}} to your worker nodes](/docs/openshift?topic=openshift-utilities#vpc_api_attach).

4. Verify that your storage is attached by running the following command.
    ```sh
    oc get pv -o yaml | grep "attachstatus"
    ```
    {: pre}

5. Restart the Portworx pod on the new worker node.
    ```sh
    oc delete pod <portworx_pod> -n <portworx_namespace>
    ```
    {: pre}

6. Exit maintenance mode
    ```sh
    pxctl service maintenance --exit
    ```
    {: pre}

7. [Mount the volume to your app](/docs/openshift?topic=openshift-storage_portworx_deploy#mount_pvc).










