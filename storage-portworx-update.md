---

copyright: 
  years: 2014, 2023
lastupdated: "2023-08-03"

keywords: portworx, openshift

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}



# Updating Portworx in your cluster
{: #storage_portworx_update}

Beginning with version `2.12` Portworx uses an operator-based deployment model instead of the Helm based model use in version `2.11` and earlier. If you are updating from Portworx `2.11` to version `2.12`, follow the migration steps in the [Portworx documentation](https://docs.portworx.com/operations/operate-kubernetes/migrate-daemonset/){: external}.
{: important}


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

## Migrating Red Hat Enterprise Linux versions 
{: #px-rhel-migrate}

When you migrate from RHEL 7 to RHEL 8, follow the steps to update your [worker nodes](/docs/openshift?topic=openshift-rhel_migrate). 

[If you are re-attaching drives, you must attach raw {{site.data.keyword.block_storage_is_short}} to your worker nodes.](/docs/openshift?topic=openshift-utilities#vpc_api_attach).


If you are using cloud drives, you do not need to reattach storage to your worker nodes. 
{: important}

## Exploring other Portworx features
{: #features}


Using existing Portworx volumes
:   If you have an existing Portworx volume that you created manually or that was not automatically deleted when you deleted the PVC, you can statically provision the corresponding PV and PVC and use this volume with your app. For more information, see [Using existing volumes](https://docs.portworx.com/portworx-install-with-kubernetes/storage-operations/create-pvcs/using-preprovisioned-volumes/#using-the-portworx-volume){: external}.

Running stateful sets on Portworx
:   If you have a stateful app that you want to deploy as a stateful set into your cluster, you can set up your stateful set to use storage from your Portworx cluster. For more information, see [Create a MySQL StatefulSet](https://docs.portworx.com/portworx-install-with-kubernetes/application-install-with-kubernetes/cassandra/#create-a-mysql-statefulset){: external}.

Running your pods hyperconverged
:   You can configure your Portworx cluster to schedule pods on the same worker node where the pod's volume resides. This setup is also referred to as `hyperconverged` and can improve the data storage performance. For more information, see [Run pods on same host as a volume](https://docs.portworx.com/portworx-install-with-kubernetes/storage-operations/hyperconvergence/){: external}.

Creating snapshots of your Portworx volumes
:   You can save the current state of a volume and its data by creating a Portworx snapshot. Snapshots can be stored on your local Portworx cluster or in the Cloud. For more information, see [Create and use local snapshots](https://docs.portworx.com/portworx-install-with-kubernetes/storage-operations/create-snapshots/){: external}.

Monitoring and managing your Portworx cluster with Lighthouse
:   You can view the health of your Portworx cluster, including the number of available storage nodes, volumes and available capacity, and analyze your data in [Prometheus, Grafana, or Kibana](https://docs.portworx.com/install-with-other/operate-and-maintain/monitoring/){: external}.






