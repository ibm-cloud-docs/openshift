---

copyright:
  years: 2014, 2021
lastupdated: "2021-04-14"

keywords: openshift, openshift container storage, ocs, vpc, roks

subcollection: openshift

---

{:DomainName: data-hd-keyref="APPDomain"}
{:DomainName: data-hd-keyref="DomainName"}
{:android: data-hd-operatingsystem="android"}
{:api: .ph data-hd-interface='api'}
{:apikey: data-credential-placeholder='apikey'}
{:app_key: data-hd-keyref="app_key"}
{:app_name: data-hd-keyref="app_name"}
{:app_secret: data-hd-keyref="app_secret"}
{:app_url: data-hd-keyref="app_url"}
{:authenticated-content: .authenticated-content}
{:beta: .beta}
{:c#: data-hd-programlang="c#"}
{:cli: .ph data-hd-interface='cli'}
{:codeblock: .codeblock}
{:curl: .ph data-hd-programlang='curl'}
{:deprecated: .deprecated}
{:dotnet-standard: .ph data-hd-programlang='dotnet-standard'}
{:download: .download}
{:external: target="_blank" .external}
{:faq: data-hd-content-type='faq'}
{:fuzzybunny: .ph data-hd-programlang='fuzzybunny'}
{:generic: data-hd-operatingsystem="generic"}
{:generic: data-hd-programlang="generic"}
{:gif: data-image-type='gif'}
{:go: .ph data-hd-programlang='go'}
{:help: data-hd-content-type='help'}
{:hide-dashboard: .hide-dashboard}
{:hide-in-docs: .hide-in-docs}
{:important: .important}
{:ios: data-hd-operatingsystem="ios"}
{:java: .ph data-hd-programlang='java'}
{:java: data-hd-programlang="java"}
{:javascript: .ph data-hd-programlang='javascript'}
{:javascript: data-hd-programlang="javascript"}
{:new_window: target="_blank"}
{:note .note}
{:note: .note}
{:objectc data-hd-programlang="objectc"}
{:org_name: data-hd-keyref="org_name"}
{:php: data-hd-programlang="php"}
{:pre: .pre}
{:preview: .preview}
{:python: .ph data-hd-programlang='python'}
{:python: data-hd-programlang="python"}
{:route: data-hd-keyref="route"}
{:row-headers: .row-headers}
{:ruby: .ph data-hd-programlang='ruby'}
{:ruby: data-hd-programlang="ruby"}
{:runtime: architecture="runtime"}
{:runtimeIcon: .runtimeIcon}
{:runtimeIconList: .runtimeIconList}
{:runtimeLink: .runtimeLink}
{:runtimeTitle: .runtimeTitle}
{:screen: .screen}
{:script: data-hd-video='script'}
{:service: architecture="service"}
{:service_instance_name: data-hd-keyref="service_instance_name"}
{:service_name: data-hd-keyref="service_name"}
{:shortdesc: .shortdesc}
{:space_name: data-hd-keyref="space_name"}
{:step: data-tutorial-type='step'}
{:subsection: outputclass="subsection"}
{:support: data-reuse='support'}
{:swift: .ph data-hd-programlang='swift'}
{:swift: data-hd-programlang="swift"}
{:table: .aria-labeledby="caption"}
{:term: .term}
{:tip: .tip}
{:tooling-url: data-tooling-url-placeholder='tooling-url'}
{:troubleshoot: data-hd-content-type='troubleshoot'}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:tsSymptoms: .tsSymptoms}
{:tutorial: data-hd-content-type='tutorial'}
{:ui: .ph data-hd-interface='ui'}
{:unity: .ph data-hd-programlang='unity'}
{:url: data-credential-placeholder='url'}
{:user_ID: data-hd-keyref="user_ID"}
{:vbnet: .ph data-hd-programlang='vb.net'}
{:video: .video}
 


# Managing your OpenShift Container Storage deployment
{: #ocs-manage-deployment}

Review the following topics to manage your OpenShift Container Storage deployment.

## Expanding OCS in VPC clusters
{: ocs-vpc-expand-storage-cluster}

To expand your OCS storage cluster, you can [add worker nodes](#ocs-expand-vpc) to your cluster, or you can scale OCS by [increasing the `numOfOsd`](#ocs-vpc-scaling-osd).
{: shortdesc}

### Expanding OCS by adding worker nodes to your cluster
{: #ocs-vpc-add-worker-nodes}

To increase the storage capacity that is available to OpenShift Container Storage, add compatible worker nodes to your cluster.
{: shortdesc}

1. Expand the worker pool of the cluster that is used for OCS by [adding worker nodes](/docs/openshift?topic=openshift-add_worker nodes). Ensure that your worker nodes meet the [requirements for OCS](#ocs-storage-classic). If you deployed OCS on all of the worker nodes in your cluster, the OCS drivers are installed on the new worker nodes when they are added to your cluster.
2. If you deployed OCS on a subset of worker nodes in your cluster by specifying the `<worker-IP>` parameters in your `OcsCluster` custom resource, you can add the IP addresses of the new worker nodes to your OCS deployment by editing the custom resource definition.
  ```sh
  oc edit ocsluster ocscluster-vpc
  ```
  {: pre}
3. Save the `OcsCluster` custom resource file to reapply it to your cluster.

<br />

### Scaling OCS by increasing the `numOfOsd` in your CRD
{: #ocs-vpc-scaling-osd}

You can scale your OCS configuration by increasing the `numOfOsd` setting. When you increase the number of OSDs, OCS provisions that number of disks of the same `osdSize` capacity in GB in each of the worker nodes in your OCS cluster. However, the total storage that is available to your applications is equal to the number of worker nodes that are multiplied by the `osdSize` multiplied by the `numOfOsd`, and then divided by the replication factor, which is a constant of 3. 
{: shortdesc}

For example, if your OCS cluster has three worker nodes, you specify an `osdSize` of `150Gi`, and you set the `numOfOsd` to 4, then your storage totals are as follows.
  * **Total storage that is available for application use**: `osdSize` multiplied by `numOfOsd` and the number of worker nodes in the cluster, and divided by the replication factor of 3, or `(3 x 150Gi x 4) / 3 = 600Gi`.
  * **Total storage that is provisioned as disks in the cluster**: `osdSize` multiplied by `numOfOsd` and the number of worker nodes in the cluster, or `150Gi x 4 x 3 = 1800Gi`.


| Number of worker nodes | Initial `osdSize` | `numOfOsd` per worker node | Storage capacity available to applications | Total storage of provisioned disks |
| --- | --- | --- | --- | --- |
| 3 | 150Gi | 1 | 150Gi | 450Gi |
| 3 | 150Gi | 2 | 300Gi | 900Gi |
| 3 | 150Gi | 3 | 450Gi | 1350Gi |
| 3 | 150Gi | 4 | 600Gi | 1800Gi |
| 6 | 150Gi | 1 | 300Gi | 900Gi |
| 6 | 150Gi | 2 | 600Gi | 1800Gi |
| 6 | 150Gi | 3 | 900Gi | 2700Gi |
| 6 | 150Gi | 4 | 1200Gi | 3600Gi |
{: caption="Table 1. OpenShift Container Storage scaling." caption-side="top"}
{: summary="The rows are read from left to right. The first column is the number of worker nodes. The second column is the initial OSD size. The third column is the number of OSDs. The fourth column is the total storage capacity that is available to applications in the cluster. The fifth column is the total storage capacity of the provisioned disks."}

[Access your {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-access_cluster).

1. Get the name of your `OcsCluster` custom resource.
  ```sh
  oc get ocsluster
  ```
  {: pre}

1. Save your `OcsCluster` custom resource YAML file to your local machine as `ocsluster.yaml`.
  ```sh
  oc get ocsluster ocsluster-vpc -o yaml
  ```
  {: pre}

1. Increase the `numOfOsd` parameter and reapply the `ocscluster` CRD to your cluster.
  ```sh
  oc apply -f ocsluster.yaml
  ```
  {: pre}

1. Verify that the additional OSDs are created. 
  ```sh
  oc get pv
  ```
  {: pre}

<br />
## VPC: Updating the OCS operator from your CRD
{: #ocs-addon-up-vpc}

If you deployed OCS by using a CRD, you can update your OCS deployment by editing the `OcsCluster` custom resource in your cluster.
{: shortdesc}

[Access your {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-access_cluster).

1. Get the name of you OCS storage cluster
  ```sh
  oc get ocscluster
  ```
  {: pre} 

  **Example output**
  ```sh
  NAME             AGE
  ocscluster-vpc   19d
  ```
  {: screen}

1. Run the following command to edit your `OcsCluster`.
  ```sh
  oc edit ocscluster <ocs-cluster-name>
  ```
  {: pre}

1. Edit the ocscluster and set the `OcsUpgrade` parameter to `true`.
  ```yaml
  ...
  spec:
    billingType: hourly
    monSize: 20Gi
    monStorageClassName: ibmc-vpc-block-10iops-tier
    numOfOsd: 1
    ocsUpgrade: true
    osdSize: 100Gi
    osdStorageClassName: ibmc-vpc-block-10iops-tier
  status:
    storageClusterStatus: Decreasing the capacity not allowed
  ```
  {: codeblock}

1. Save and close the `OcsCluster` to reapply it to your cluster.


<br />

## Classic: Increasing storage capacity by adding worker nodes to your cluster
{: #ocs-add-worker-nodes-classic}

To increase the storage capacity that is available to OpenShift Container Storage, add compatible worker nodes to your cluster.
{: shortdesc}

[Access your {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-access_cluster).

1. Expand the worker pool of the cluster that is used for OCS by [adding SDS worker nodes](/docs/openshift?topic=openshift-add_worker nodes). Ensure that your worker nodes meet the [requirements for OCS](#ocs-storage-classic).
2. [Find the `by-id` of the local disks](#ocs-classic-get-devices) on your new worker nodes.
3. Add the `by-id` of the local disks to your `OcsCluster` custom resource definition.
  ```sh
  oc edit ocscluster ocscluster
  ```
  {: pre}
3. If you deployed OCS on a subset of worker nodes in your cluster by specifying the `<worker-IP>` parameters in your `OcsCluster` custom resource, add the IP addresses of the new worker nodes to your OCS deployment by editing the custom resource definition.
4. Save the `OcsCluster` custom resource file to reapply it to your cluster.

<br />

## Setting up backing stores by using the NooBaa CLI
{: #ocs-backing-store-setup}

After you deploy OCS, you can configure more backing stores in your OCS storage cluster. You can create a backing store by using any s3 compatible object store such as AWS or {{site.data.keyword.cos_full_notm}}.
{: shortdesc}

You can also create and manage your backing stores in the {{site.data.keyword.openshiftshort}} web console.
{: tip}

To add a backing store to your OCS storage cluster by using the NooBaa CLI:

[Access your {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-access_cluster).

1. Install the [NooBaa Operator CLI](https://github.com/noobaa/noobaa-operator){: external}.
1. Run the `noobaa backingstore create` command to see a list of supported backing store types.
  ```sh
  noobaa backingstore create
  ```
  {: pre}

  **Example output**
  ```sh
  Create backing store

  Available Commands:
    aws-s3               Create aws-s3 backing store
    azure-blob           Create azure-blob backing store
    google-cloud-storage Create google-cloud-storage backing store
    ibm-cos              Create ibm-cos backing store
    pv-pool              Create pv-pool backing store
    s3-compatible        Create s3-compatible backing store
  ```
  {: screen}

1. Get the details of the service that you want to use. If you want to set up an {{site.data.keyword.cos_full_notm}}, get your HMAC credentials. For more information, see [Using HMAC credentials](/docs/cloud-object-storage?topic=cloud-object-storage-uhc-hmac-credentials-main). The following example NooBaa command shows the configuration parameters that are required to create a backing store by using an {{site.data.keyword.cos_full_notm}} service instance.
  ```sh
  noobaa backingstore create ibm-cos <backing-store-name> -n openshift-storage --access-key=<access-key> --endpoint=<endpoint> --secret-key=<secret-key> --target-bucket<target-bucket>
  ```
  {: pre}

1. Get the details of your backing store.
  ```sh
  noobaa backingstore status <backing-store-name> -n openshift-storage
  ```
  {: pre}

<br />

## Removing OCS from your apps
{: #ocs-remove-apps-storage}

To remove OCS from your apps, you can delete your app or deployment and the corresponding PVCs.
{: shortdesc}

If you want to fully remove OCS and all of your data, you can [remove your OCS storage cluster](#ocs-remove-storage-cluster).
{: note}

1. List your PVCs and note the name of the PVC and the corresponding PV that you want to remove.
   ```sh
   oc get pvc
   ```
   {: pre}

2. Remove any pods that mount the PVC.
   1. List all the pods that currently mount the PVC that you want to delete. If no pods are returned, you do not have any pods that currently use your PVC.
      ```sh
      oc get pods --all-namespaces -o=jsonpath='{range .items[*]}{"\n"}{.metadata.name}{":\t"}{range .spec.volumes[*]}{.persistentVolumeClaim.claimName}{" "}{end}{end}' | grep "<pvc_name>"
      ```
      {: pre}

      Example output:
      ```
      app    ocs-storagecluster-cephfs
      ```
      {: screen}

   2. Remove the pod that uses the PVC. If the pod is part of a deployment, remove the deployment.
      ```sh
      oc delete pod <pod_name>
      ```
      {: pre}

      ```sh
      oc delete deployment <deployment_name>
      ```
      {: pre}

   3. Verify that the pod or the deployment is removed.
      ```sh
      oc get pods
      ```
      {: pre}

      ```sh
      oc get deployments
      ```
      {: pre}

3. **Optional** Delete the PVC. Deleting the PVC deletes your app data from the storage volume.
   ```sh
   oc delete pvc <pvc_name>
   ```
   {: pre}



## Removing your OCS storage cluster
{: #ocs-remove-storage-cluster}

Complete the following steps to remove the OCS resources from your cluster.
{: shortdesc}

The following steps result in data loss. Back up the data on your local volumes before you remove your OCS deployment.
{: important}

**What happens when I delete the OCS storage cluster?**

When you delete the `OcsCluster` custom resource from your cluster, the following resources are deleted. Additionally, any apps that require access to the data on your local volumes might experience downtime.
  - OCS driver pods.
  - The MON and OSD PVCs.
  - All data from your volumes. However, if you created PVCs by using the NooBaa storage class, and your apps wrote data to your backing store, the data in your backing store is not deleted.

1. Get the name of your `OcsCluster` custom resource.
  ```sh
  oc get ocscluster
  ```
  {: pre}

  **Example output for a custom resource called `ocscluster-vpc`.**
  ```sh
  NAME             AGE
  ocscluster-vpc   4s
  ```
  {: screen}

1. Delete your `OcsCluster` custom resource. Replace `<ocscluster_name>` with the name of your custom resource.
  ```
  oc delete ocsluster <ocscluster_name>
  ```
  {: pre}

  **Example command for an `OcsCluster` custom resource called `ocscluster-vpc`.**
  ```
  oc delete ocsluster ocscluster-vpc
  ```
  {: pre}

1. Delete any PVCs that you created.
  ```sh
  oc get pvc
  ```
  {: pre}

1. **Optional** If you do not want to reinstall OCS, you can [Remove the OCS add-on from your cluster](#ocs-addon-rm-vpc).

## Cleaning up your OCS deployment
{: #ocs-rm-cleanup-resources}

After you remove OCS from your apps, and remove your OCS storage cluster, you can clean up the remaining Kubernetes resources that were deployed with OCS.
{: shortdesc}

### VPC: Cleaning up OCS
{: #ocs-cleanup-vpc}

1. Clean up the remaining Kubernetes resources from your cluster. Save the following script in a file called `cleanup.sh` to your local machine.
  ```sh
  #!/bin/bash
  ocscluster_name=`oc get ocscluster | awk 'NR==2 {print $1}'`
  oc delete ocscluster --all --wait=false
  kubectl patch ocscluster/$ocscluster_name -p '{"metadata":{"finalizers":[]}}' --type=merge
  oc delete ns openshift-storage --wait=false
  sleep 20
  kubectl -n openshift-storage patch persistentvolumeclaim/db-noobaa-db-0 -p '{"metadata":{"finalizers":[]}}' --type=merge
  kubectl -n openshift-storage patch cephblockpool.ceph.rook.io/ocs-storagecluster-cephblockpool -p '{"metadata":{"finalizers":[]}}' --type=merge
  kubectl -n openshift-storage patch cephcluster.ceph.rook.io/ocs-storagecluster-cephcluster -p '{"metadata":{"finalizers":[]}}' --type=merge
  kubectl -n openshift-storage patch cephfilesystem.ceph.rook.io/ocs-storagecluster-cephfilesystem -p '{"metadata":{"finalizers":[]}}' --type=merge
  kubectl -n openshift-storage patch cephobjectstore.ceph.rook.io/ocs-storagecluster-cephobjectstore -p '{"metadata":{"finalizers":[]}}' --type=merge
  kubectl -n openshift-storage patch cephobjectstoreuser.ceph.rook.io/noobaa-ceph-objectstore-user -p '{"metadata":{"finalizers":[]}}' --type=merge
  kubectl -n openshift-storage patch cephobjectstoreuser.ceph.rook.io/ocs-storagecluster-cephobjectstoreuser -p '{"metadata":{"finalizers":[]}}' --type=merge
  kubectl -n openshift-storage patch NooBaa/noobaa -p '{"metadata":{"finalizers":[]}}' --type=merge
  kubectl -n openshift-storage patch backingstores.noobaa.io/noobaa-default-backing-store -p '{"metadata":{"finalizers":[]}}' --type=merge
  kubectl -n openshift-storage patch bucketclasses.noobaa.io/noobaa-default-bucket-class -p '{"metadata":{"finalizers":[]}}' --type=merge
  kubectl -n openshift-storage patch storagecluster.ocs.openshift.io/ocs-storagecluster -p '{"metadata":{"finalizers":[]}}' --type=merge
  sleep 20
  oc delete pods -n openshift-storage --all --force --grace-period=0
  sleep 20
  ```
  {: pre}

1. Run the `cleanup.sh` script.
  ```sh
  sh ./cleanup.sh
  ```
  {: pre}

### Classic: Cleaning up OCS
{: #ocs-cleanup-classic-resources}

1. Clean up the remaining Kubernetes resources from your cluster. Save the following script in a file called `cleanup.sh` to your local machine.
  ```sh
  #!/bin/bash
  ocscluster_name=`oc get ocscluster | awk 'NR==2 {print $1}'`
  oc delete ocscluster --all --wait=false
  kubectl patch ocscluster/$ocscluster_name -p '{"metadata":{"finalizers":[]}}' --type=merge
  oc delete ns openshift-storage --wait=false
  sleep 20
  kubectl -n openshift-storage patch persistentvolumeclaim/db-noobaa-db-0 -p '{"metadata":{"finalizers":[]}}' --type=merge
  kubectl -n openshift-storage patch cephblockpool.ceph.rook.io/ocs-storagecluster-cephblockpool -p '{"metadata":{"finalizers":[]}}' --type=merge
  kubectl -n openshift-storage patch cephcluster.ceph.rook.io/ocs-storagecluster-cephcluster -p '{"metadata":{"finalizers":[]}}' --type=merge
  kubectl -n openshift-storage patch cephfilesystem.ceph.rook.io/ocs-storagecluster-cephfilesystem -p '{"metadata":{"finalizers":[]}}' --type=merge
  kubectl -n openshift-storage patch cephobjectstore.ceph.rook.io/ocs-storagecluster-cephobjectstore -p '{"metadata":{"finalizers":[]}}' --type=merge
  kubectl -n openshift-storage patch cephobjectstoreuser.ceph.rook.io/noobaa-ceph-objectstore-user -p '{"metadata":{"finalizers":[]}}' --type=merge
  kubectl -n openshift-storage patch cephobjectstoreuser.ceph.rook.io/ocs-storagecluster-cephobjectstoreuser -p '{"metadata":{"finalizers":[]}}' --type=merge
  kubectl -n openshift-storage patch NooBaa/noobaa -p '{"metadata":{"finalizers":[]}}' --type=merge
  kubectl -n openshift-storage patch backingstores.noobaa.io/noobaa-default-backing-store -p '{"metadata":{"finalizers":[]}}' --type=merge
  kubectl -n openshift-storage patch bucketclasses.noobaa.io/noobaa-default-bucket-class -p '{"metadata":{"finalizers":[]}}' --type=merge
  kubectl -n openshift-storage patch storagecluster.ocs.openshift.io/ocs-storagecluster -p '{"metadata":{"finalizers":[]}}' --type=merge
  sleep 20
  oc delete pods -n openshift-storage --all --force --grace-period=0
  oc delete ns local-storage --wait=false
  sleep 20
  kubectl -n local-storage patch localvolume.local.storage.openshift.io/local-block -p '{"metadata":{"finalizers":[]}}' --type=merge
  kubectl -n local-storage patch localvolume.local.storage.openshift.io/local-file -p '{"metadata":{"finalizers":[]}}' --type=merge
  sleep 20
  oc delete pods -n local-storage --all --force --grace-period=0
  ```
  {: pre}

1. Run the `cleanup.sh` script.
  ```sh
  sh ./cleanup.sh
  ```
  {: pre}

1. After you run the cleanup script, log in to each worker node and run the following commands.
  1. Deploy a debug pod and run `chroot /host`.
    ```sh
    oc debug node/<node_name> -- chroot /host
    ```
    {: pre}

  1. Run the following command to remove any files or directories on the specified paths. Repeat this step for each worker node that you used in your OCS configuration.
    ```sh
    rm -rvf /var/lib/rook /mnt/local-storage
    ```
    {: codeblock}

    **Example output**:
    ```sh
    removed '/var/lib/rook/openshift-storage/log/ocs-deviceset-0-data-0-6fgp6/ceph-volume.log'
    removed directory: '/var/lib/rook/openshift-storage/log/ocs-deviceset-0-data-0-6fgp6'
    removed directory: '/var/lib/rook/openshift-storage/log'
    removed directory: '/var/lib/rook/openshift-storage/crash/posted'
    removed directory: '/var/lib/rook/openshift-storage/crash'
    removed '/var/lib/rook/openshift-storage/client.admin.keyring'
    removed '/var/lib/rook/openshift-storage/openshift-storage.config'
    removed directory: '/var/lib/rook/openshift-storage'
    removed directory: '/var/lib/rook'
    removed '/mnt/local-storage/localblock/nvme3n1'
    removed directory: '/mnt/local-storage/localblock'
    removed '/mnt/local-storage/localfile/nvme2n1'
    removed directory: '/mnt/local-storage/localfile'
    removed directory: '/mnt/local-storage'
    ```
    {: codeblock}

1. **Optional**: If you no longer want to use the local volumes that you used in your OCS configuration, you can delete them from the cluster. List the local PVs.
  ```sh
  oc get pv
  ```
  {: pre}

  **Example output**:
  ```sh
  local-pv-180cfc58   139Gi      RWO            Delete           Available           localfile               11m
  local-pv-67f21982   139Gi      RWO            Delete           Available           localfile               12m
  local-pv-80c5166    100Gi      RWO            Delete           Available           localblock              12m
  local-pv-9b049705   139Gi      RWO            Delete           Available           localfile               12m
  local-pv-b09e0279   100Gi      RWO            Delete           Available           localblock              12m
  local-pv-f798e570   100Gi      RWO            Delete           Available           localblock              12m
  ```
  {: screen}

1. Delete the local PVs.
  ```sh
  oc delete pv <pv_name> <pv_name> <pv_name>
  ```
  {: pre}

## Troubleshooting OCS
{: #ocs-troubleshooting-gather}

To gather the information that is needed to troubleshoot OCS, you can use the `oc adm must-gather` command and specify the OCS image. For more information, see [Gathering cluster data](https://docs.openshift.com/container-platform/4.5/support/gathering-cluster-data.html).
{: shortdesc}

You can use the Rook community toolbox to debug issues with your Ceph cluster. For more information, see the [Rook documentation](https://rook.io/docs/rook/v1.3/ceph-toolbox.html){: external}.
{:tip}




