---

copyright:
  years: 2023, 2024
lastupdated: "2024-05-10"


keywords: openshift, openshift data foundation, openshift container storage, ocs, worker update, worker replace

subcollection: openshift


content-type: tutorial
services: openshift, vpc
account-plan: paid
completion-time: 60m

---



{{site.data.keyword.attribute-definition-list}}

# Updating or replacing VPC worker nodes that use OpenShift Data Foundation
{: #openshift-storage-update-vpc}
{: toc-content-type="tutorial"}
{: toc-services="openshift, vpc"}
{: toc-completion-time="60m"}

[Virtual Private Cloud]{: tag-vpc}


For VPC clusters with a storage solution such as OpenShift Data Foundation you must cordon, drain, and replace each worker node sequentially. If you deployed OpenShift Data Foundation to a subset of worker nodes in your cluster, then after you replace the worker node, you must then edit the `ocscluster` resource to include the new worker node.
{: shortdesc}

The following tutorial covers both major and minor updates and worker replacement.

[Major update]{: tag-red}
:   Complete the steps with this label to apply a major update; for example, if you are updating your worker nodes to a new major version, such as from `4.11` to `4.12` as well as OpenShift Data Foundation from `4.11` to `4.12`.

[Minor update]{: tag-blue}
:   Complete the steps with this label to apply a patch update, for example if you are updating from `4.12.15_1542_openshift` to `4.12.16_1544_openshift` while keeping OpenShift Data Foundation at version `4.12`. You must repeat these steps for each node you want to update.

[Worker replace]{: tag-green} 
:   Complete the steps with this label steps if you are replacing a worker node at the same patch version. You must repeat these steps for each node you want to replace.

Skipping versions during an upgrade, such as from 4.8 to 4.12 is not supported.
{: important}


[Log in to your account. If applicable, target the appropriate resource group. Set the context for your cluster.](/docs/containers?topic=containers-access_cluster)

Before updating your worker nodes, make sure to back up your app data. Also, plan to complete the following steps for one worker node at a time. Repeat the steps for each worker node that you want to update.
{: important}

## Update the cluster master
{: #update-cluster-master-vpc}
{: step}
 
[Major update]{: tag-red}


1. If you are updating your worker nodes to a new major version, such as from `4.11` to `4.12`, update the cluster master first. 
    ```sh
    ibmcloud oc cluster master update --cluster CLUSTER [--version MAJOR.MINOR.PATCH] [--force-update] [-f] [-q]
    ```
    {: pre}

    Example command:
    ```sh
    ibmcloud oc cluster master update --cluster mycluster --version 4.14.22 --force-update
    ```
    {: pre}
    
1. Wait until the master update finishes. 

## Determine which storage nodes you want to update or replace
{: #determine-storage-nodes-vpc}
{: step}

[Major update]{: tag-red} [Minor update]{: tag-blue} [Worker replace]{: tag-green}

1. List your worker nodes by using `oc get nodes` and determine which storage nodes you want to update.

    ```sh
    oc get nodes
    ```
    {: pre}
    
    Example output
        
    ```sh
    NAME           STATUS   ROLES           AGE    VERSION
    10.241.0.4     Ready    master,worker   106s   v1.21.6+4b61f94
    10.241.128.4   Ready    master,worker   22d    v1.21.6+bb8d50a
    10.241.64.4    Ready    master,worker   22d    v1.21.6+bb8d50a
    ```
    {: screen}

## Scale down OpenShift Data Foundation
{: #scale-down-odf-vpc}
{: step}

[Major update]{: tag-red} [Minor update]{: tag-blue} [Worker replace]{: tag-green}

1.  For each worker node that you found in the previous step, find the `rook-ceph-mon` and `rook-ceph-osd` deployments.
    ```sh
    oc get pods -n openshift-storage -o wide | grep -i <node_name>
    ```
    {: pre}
    
1. Scale down the deployments that you found in the previous step. 
    ```sh
    oc scale deployment rook-ceph-mon-c --replicas=0 -n openshift-storage
    ```
    {: pre}
    
    ```sh
    oc scale deployment rook-ceph-osd-2 --replicas=0 -n openshift-storage
    ```
    {: pre}

    ```sh
    oc scale deployment --selector=app=rook-ceph-crashcollector,node_name=NODE-NAME --replicas=0 -n openshift-storage
    ```
    {: pre}

    
## Cordon and drain the worker node
{: #cordon-drain-worker-node-vpc}
{: step}

[Major update]{: tag-red} [Minor update]{: tag-blue} [Worker replace]{: tag-green}

1.  Cordon the node. Cordoning the node prevents any pods from being scheduled on this node.
    ```sh
    oc adm cordon NODE_NAME
    ```
    {: pre}
    
    Example output
    
    ```sh
    node/10.241.0.4 cordoned
    ```
    {: screen}
    
1. Drain the node to remove all the pods. When you drain the worker node, the pods move to the other worker nodes ensuring there is no downtime. Draining also ensures that there is no disruption of the pod disruption budget. 
    ```sh
    oc adm drain NODE_NAME --force --delete-emptydir-data --ignore-daemonsets
    ```
    {: pre}
    
    Example output
    ```sh
    evicting pod "managed-storage-validation-webhooks-7fd79bc9f7-pdpv6"
    evicting pod "calico-kube-controllers-647dbbd685-fmrp9"
    evicting pod "certified-operators-2v852"
    evicting pod "csi-snapshot-controller-77fbf474df-47ddt"
    evicting pod "calico-typha-8574d89b8c-7f2cc"
    evicting pod "dns-operator-6d48cbff67-vrrsw"
    evicting pod "router-default-6fc798b98b-9m6kh"
    evicting pod "prometheus-adapter-5b77ffdd5f-hzqrp"
    evicting pod "alertmanager-main-1"
    evicting pod "prometheus-k8s-0"
    evicting pod "network-check-source-66c7fbb86-2r78z"
    ```
    {: screen}
    
1. Wait until draining finishes, then complete the following steps to replace the worker node. 

## Replace the worker node
{: #upgrade-worker-node-vpc}
{: step}

[Major update]{: tag-red} [Minor update]{: tag-blue} [Worker replace]{: tag-green}


1. List your worker nodes by using the `ibmcloud oc worker ls` command and find the worker node that you cordoned and drained in the previous step.
    ```sh
    ibmcloud oc worker ls -c CLUSTER
    ```
    {: pre}
    
    Example output
    ```sh
    ID                                                 Primary IP     Flavor     State    Status   Zone        Version   
    kube-c85ra07w091uv4nid9ug-vpcoc-default-000001c1   10.241.128.4   bx2.4x16   normal   Ready    us-east-3   4.8.29_1544_openshift*   
    kube-c85ra07w091uv4nid9ug-vpcoc-default-00000288   10.241.0.4     bx2.4x16   normal   Ready    us-east-1   4.8.29_1544_openshift*   
    kube-c85ra07w091uv4nid9ug-vpcoc-default-00000352   10.241.64.4    bx2.4x16   normal   Ready    us-east-2   4.8.29_1544_openshift*
    ```
    {: pre}


1.  Replace the worker node. 

    [Minor update]{: tag-blue} Example command to replace the worker node and apply the latest patch update.
    ```sh
    ibmcloud oc worker replace -c CLUSTER --worker kube-*** --update
    ```
    {: pre}

    [Worker replace]{: tag-green} Example command to replace the worker node without applying the latest patch update.
    ```sh
    ibmcloud oc worker replace -c CLUSTER --worker kube-***
    ```
    {: pre}
        
    Example output
    ```sh
    The replacement worker node is created in the same zone with the same flavor, but gets new public or private IP addresses. During the replacement, all pods might be rescheduled onto other worker nodes and data is deleted if not stored outside the pod. To avoid downtime, ensure that you have enough worker nodes to handle your workload while the selected worker nodes are being replaced.
    Replace worker node kube-c85ra07w091uv4nid9ug-cluster-default-00000288? [y/N]> y
    Deleting worker node kube-c85ra07w091uv4nid9ug-cluster-default-00000288 and creating a new worker node in cluster
    ```
    {: screen}
    
1. Wait for the replacement node to be provisioned and then list your worker nodes. Note that this process might take 20 minutes or more.
    ```sh
    oc get nodes
    ```
    {: pre}
    
    Example output
    
    ```sh
    NAME           STATUS   ROLES           AGE   VERSION
    10.241.0.4     Ready    master,worker   22d   v1.21.6+bb8d50a
    10.241.128.4   Ready    master,worker   22d   v1.21.6+bb8d50a
    10.241.64.4    Ready    master,worker   22d   v1.21.6+bb8d50a
    ```
    {: screen}

## Clean up the resources from the old node
{: #cleanup-os-storage-vpc}
{: step}

[Major update]{: tag-red} [Minor update]{: tag-blue} [Worker replace]{: tag-green}

1. Verify OSD pod has come up on the replaced node in a `running` state, if the pod is running, continue to [step 7](#add-storage-node-vpc). If the pod has failed, perform the following steps.

1. Navigate to the `openshift-storage` project.
    ```sh
    oc project openshift-storage
    ```
    {: pre}

1. Remove the failed OSD from the cluster. You can specify multiple failed OSDs if required:
    ```sh
    oc process -n openshift-storage ocs-osd-removal -p FAILED_OSD_IDS=<failed_osd_id> -p FORCE_OSD_REMOVAL=true | oc create -f -
    ```
    {: pre}
    
    The `FAILED_osd_id` value is the integer in the pod name immediately after the `rook-ceph-osd` prefix. The `FORCE_OSD_REMOVAL` value must be changed to `true` in clusters that have only three OSDs, or clusters with insufficient space to restore all three replicas of the data after the OSD is removed.
    {: note}

1. Verify that the OSD was removed successfully by checking the status of the `ocs-osd-removal-job` pod.
    ```sh
    oc get pod -l job-name=ocs-osd-removal-job -n openshift-storage
    ```
    {: pre}

1. Verify that the OSD removal is completed.
    ```sh
    oc logs -l job-name=ocs-osd-removal-job -n openshift-storage --tail=-1 | egrep -i 'completed removal'
    ```
    {: pre}

    Example output

    ```sh
    2023-03-10 06:50:04.501511 I | cephosd: completed removal of OSD 0
    ```
    {: screen}

## Add the new storage node
{: #add-storage-node-vpc}
{: step}

[Major update]{: tag-red} [Minor update]{: tag-blue} [Worker replace]{: tag-green}

1. If you limited your ODF deployment to a subset of worker nodes by specifying node names during installation, you must update the `ocscluster` CRD to include the new name. 
    If you did not limit your configuration to only certain worker nodes, you do not need to update the `ocscluster` CRD.
    {: important}
    
    ```sh
    oc edit ocscluster 
    ```
    {: pre}

    ```yaml
    apiVersion: ocs.ibm.io/v1
    kind: OcsCluster
    metadata:
    name: ocscluster-auto
    spec:
    . . .
    osdSize: 250Gi
    osdStorageClassName: ibmc-vpc-block-metro-10iops-tier
    workerNodes:
    - NODE-NAME # Example 10.248.128.42
    - NODE-NAME
    - NODE-NAME
    ```
    {: screen}

1. Wait for the OpenShift Data Foundation pods to deploy to the new worker. Verify the new persistent volumes are created and that all pods are in a `Running` state.
    ```sh
    oc get pv
    oc get ocscluster
    oc get pods -n openshift-storage
    ```
    {: pre}

1. Verify that all other required OpenShift Data Foundation pods are in Running state.
    ```sh
    oc get pod -n openshift-storage | grep mon
    ```
    {: pre}
    
    Example output:
    ```sh
    rook-ceph-mon-a-cd575c89b-b6k66         2/2     Running
    0          38m
    rook-ceph-mon-b-6776bc469b-tzzt8        2/2     Running
    0          38m
    rook-ceph-mon-d-5ff5d488b5-7v8xh        2/2     Running
    0          4m8s
    ```
    {: screen}

1. Verify that new OSD pods are running on the replacement node:
    ```sh
    oc get pods -o wide -n openshift-storage| egrep -i <new_node_name> | egrep osd
    ```
    {: pre}

    
    
## Update the OpenShift Data Foundation add-on
{: #update-ocs-add-on-vpc}
{: step}

[Major update]{: tag-red}


1. Check the existing version.
    ```sh
    ibmcloud oc cluster addon ls --cluster CLUSTER
    ```
    {: pre}

1. Update the add-on.
    ```sh
    ibmcloud oc cluster addon update openshift-data-foundation --cluster CLUSTER --version VERSION
    ```
    {: pre}

1. Verify the add-on is updated.
    ```sh
    ibmcloud oc cluster addon ls --cluster CLUSTER
    ```
    {: pre}

## Update your cluster resource
{: #update-ocs-resource-yaml-vpc}
{: step}

[Major update]{: tag-red}

1. Get the name of your `ocscluster` resource.
    ```sh
    oc get ocscluster
    ```
    {: pre}

    Example output
    ```sh
    NAME             AGE
    ocscluster-vpc   19d
    ```
    {: screen}

1. Run the following command to edit your `ocscluster` resource.
    ```sh
    oc edit ocscluster OCS-CLUSTER-NAME
    ```
    {: pre}

1. Set the `ocsUpgrade` parameter to `true`.
    ```yaml
    ...
    spec:
        billingType: hourly
    monSize: 20Gi
    monStorageClassName: ibmc-vpc-block-10iops-tier
    numOfOsd: 1
    ocsUpgrade: true
    osdSize: 250Gi
    osdStorageClassName: ibmc-vpc-block-10iops-tier
    status:
        storageClusterStatus: Decreasing the capacity not allowed
    ```
    {: codeblock}

1. Save and close the file.

1. Wait for the update to complete.

1. Verify that the `storagecluster` and `cephcluster` resources are both deployed correctly.

    ```sh
    oc get storagecluster -n openshift-storage
    NAME                 AGE   PHASE   EXTERNAL   CREATED AT             VERSION
    ocs-storagecluster   43h   Ready              2023-06-21T09:22:00Z   4.11.0
    ```
    {: screen}

    ```sh
    oc get cephcluster -n openshift-storage
    NAME                             DATADIRHOSTPATH   MONCOUNT   AGE   PHASE   MESSAGE                        HEALTH      EXTERNAL
    ocs-storagecluster-cephcluster   /var/lib/rook     3          43h   Ready   Cluster created successfully   HEALTH_OK   
    ```
    {: screen}

    ```sh
    oc get csv -n openshift-storage
    NAME                              DISPLAY                       VERSION   REPLACES                          PHASE
    mcg-operator.v4.11.8              NooBaa Operator               4.11.8    mcg-operator.v4.11.7              Succeeded
    ocs-operator.v4.11.8              OpenShift Container Storage   4.11.8    ocs-operator.v4.11.7              Succeeded
    odf-csi-addons-operator.v4.11.8   CSI Addons                    4.11.8    odf-csi-addons-operator.v4.11.7   Succeeded
    odf-operator.v4.11.8              OpenShift Data Foundation     4.11.8    odf-operator.v4.11.7              Succeeded
    ```
    {: screen}

 





