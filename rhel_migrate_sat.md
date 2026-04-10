---

copyright:
  years: 2026, 2026
lastupdated: "2026-04-10"


keywords: rhel, os, operating system, rhcos, 418, migration, satellite

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}



# Migrating Satellite worker nodes to RHCOS
{: #rhel_migrate_sat}

[Satellite]{: tag-satellite}

Complete the following steps to migrate your Satellite worker nodes to RHCOS
{: shortdesc}


To migrate to RHCOS, you must provision a new worker pool, then delete the previous RHEL worker pool. The new worker pool must reside in the same zone as the previous worker pool. 

## Step 1: Upgrade your cluster master
{: #upgrade-cluster-rhcos}

Run the following command to update the master.

```sh
ibmcloud ks cluster master update --cluster <clusterNameOrID> --version 4.18_openshift
```
{: pre}

## Step 2: Creating a new RHCOS worker pool
{: #create-pool-rhcos}

- Make sure to specify `RHCOS` as the `--operating-system` of the new pool.
- Make sure that the number of nodes specified with the `--size-per-zone` option matches the number of workers per zone for the RHEL worker pool. To list a worker pool's zones and the number of workers per zone, run `ibmcloud oc worker-pool get --worker-pool WORKER_POOL --cluster CLUSTER`.
- Make sure to include the `--entitlement ocp_entitled` option if you have a Cloud Pak entitlement.

1. Run the `ibmcloud oc worker-pool create` command to create a new worker pool.

    
    Example command to create a RHCOS worker pool. Note that for {{site.data.keyword.satelliteshort}} clusters, you must first [attach hosts to your location](/docs/satellite?topic=satellite-attach-hosts) before you can create a worker pool.
    
    ```sh
    ibmcloud oc worker-pool create satellite --cluster CLUSTER --host-label "os=RHCOS" --name NAME --size-per-zone SIZE --operating-system RHCOS --zone ZONE [--label LABEL]
    ```
    {: pre}


1. Verify that the worker pool is created and note the worker pool ID.

    ```sh
    ibmcloud oc worker-pool ls --cluster <cluster_name_or_ID>
    ```
    {: pre}

    Example output

    ```sh
    Name            ID                              Flavor                 OS              Workers 
    my_workerpool   aaaaa1a11a1aa1aaaaa111aa11      b3c.4x16.encrypted     REDHAT_8_64    0 
    ```
    {: screen}

1. Add one or more zones to your worker pool. When you add a zone, the number of worker nodes you specified with the `--size-per-zone` option are added to the zone. These worker nodes run the RHCOS operating system. It's recommended that the zones you add to the RHCOS worker pool match the zones added to the RHEL worker pool that you are replacing. To view the zones attached to a worker pool, run `ibmcloud oc worker-pool zones --worker-pool WORKER_POOL --cluster CLUSTER`. If you add zones that do not match those of RHEL worker pool, make sure that your workloads will not be impacted by moving them to a new zone. Note that File or Block storage are not supported across zones. 


## Step 3: Add worker nodes to your RHCOS worker pool
{: #rhcos-add-worker-nodes}

See [Adding a zone to a worker pool in a VPC cluster](/docs/openshift?topic=openshift-add-workers-vpc#vpc_add_zone).



## Step 4: Migrate your workloads
{: #rhcos-migrate-workloads}

If you have software-defined storage (SDS) solutions like OpenShift Data Foundation or Portworx, update your storage configurations to include the new worker nodes and verify your workloads before removing your RHEL worker nodes.
{: important}

For more information about rescheduling workloads, see [Safely Drain a Node](https://kubernetes.io/docs/tasks/administer-cluster/safely-drain-node/){: external} in the Kubernetes docs or [Understanding how to evacuate pods on nodes](https://docs.redhat.com/en/documentation/openshift_container_platform/4.9/html/nodes/working-with-nodes#nodes-nodes-working){: external} in the {{site.data.keyword.redhat_openshift_notm}} docs.
{: tip}

* Migrate per pod by cordoning node and deleting individual pods.
    ```sh
    oc adm cordon no/<nodeName>
    oc delete po -n <namespace> <podName>
    ```
    {: pre}

* Migrate per Node by draining nodes. For more information, see [Safely drain a node](https://kubernetes.io/docs/tasks/administer-cluster/safely-drain-node/){: external}.

* Migrate per worker pool by deleting your entire RHEL worker pool.
    ```sh
    ibmcloud ks worker-pool rm --cluster <clusterNameOrID> --worker-pool <workerPoolNameOrID>
    ```
    {: pre}

## Step 5: Remove the RHEL worker nodes
{: #rm-rhel-pool}

Remove the worker pool that contains the RHEL workers. 

Consider scaling down your RHEL worker pool and keeping it for several days before you remove it. This way, you can easily scale the worker pool back up if your workload experiences disruptions during the migration process. When you have determined that your workload is stable and functions normally, you can safely remove the RHEL worker pool.
{: important}

1. List your worker pools and note the name of the worker pool you want to remove.
    ```sh
    ibmcloud oc worker-pool ls --cluster CLUSTER
    ```
    {: pre}

2. Run the command to remove the worker pool.
    ```sh
    ibmcloud oc worker-pool rm --worker-pool WORKER_POOL --cluster CLUSTER
    ```
    {: pre}

### Optional Step 5: Uninstall and reinstall the Object Storage plug-in
{: #rhel-rm-cos}

If you use the COS plug-in in your cluster, after migrating from RHEL to RHCOS, you must uninstall and reinstall it because the `kube-driver` path is different between the two operating systems. If this is not done, you may see an error similar to `Error: failed to mkdir /usr/libexec/kubernetes: mkdir /usr/libexec/kubernetes: read-only file system`.

* [Follow the steps to uninstall the COS plug-in](/docs/openshift?topic=openshift-storage_cos_install#remove_cos_plugin).

* [Reinstall the plug-in](/docs/openshift?topic=openshift-storage_cos_install#remove_cos_plugin)
