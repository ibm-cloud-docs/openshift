---

copyright: 
  years: 2022, 2026
lastupdated: "2026-03-31"


keywords: openshift, block storage for vpc, snapshot, restore snapshot, create snapshot

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}



# Setting up snapshots with the {{site.data.keyword.block_storage_is_short}} cluster add-on
{: #vpc-volume-snapshot}

[Virtual Private Cloud]{: tag-vpc} 

{{site.data.keyword.block_storage_is_short}} volume snapshots provide you with a standardized way to copy a volume's contents at a particular point in time without creating an entirely new volume. For more information about snapshots, see [How snapshots work](/docs/vpc?topic=vpc-snapshots-vpc-about). For more information about {{site.data.keyword.block_storage_is_short}}, see [About {{site.data.keyword.block_storage_is_short}}](/docs/vpc?topic=vpc-block-storage-about).
{: shortdesc}


By default, the {{site.data.keyword.block_storage_is_short}} cluster add-on creates volumes and snapshots in the same VPC resource group where the cluster is deployed. However, starting with add-on version 5.2.46 and later, you can create snapshots in a different resource group by specifying the `resourceGroup` parameter in your `VolumeSnapshotClass`. For more information, see [Creating snapshots in a different resource group](#vpc-snapshot-different-rg).
{: important}


## Creating an app
{: #vpc-snapshot-deployment}

Create an example Persistent Volume Claim (PVC) and deploy a pod that references that claim. 
{: shortdesc}

1. [Log in to your account. If applicable, target the appropriate resource group. Set the context for your cluster.](/docs/containers?topic=containers-access_cluster)

1. Verify that the add-on state is `normal` and the status is `Ready`.
    
    ```sh
    ibmcloud oc cluster addon ls --cluster CLUSTER-ID
    ```
    {: pre}

    ```sh
    Name                   Version                     Health State   Health Status   
    vpc-block-csi-driver   5.2   normal         Addon Ready. For more info: http://ibm.biz/addon-state (H1500)   
    ```
    {: screen}
    
1. Verify that the driver pods are deployed and the status is `Running`.
    ```sh
    oc get pods -n kube-system | grep vpc-block-csi
    ```
    {: pre}
    
    Example output
    ```sh                    
    ibm-vpc-block-csi-controller-0                        7/7     Running   0          77s
    ibm-vpc-block-csi-node-56c85                          4/4     Running   0          77s
    ibm-vpc-block-csi-node-87j2t                          4/4     Running   0          77s
    ibm-vpc-block-csi-node-cmh2h                          4/4     Running   0          77s
    ```
    {: screen}

1. Create a PVC. 

    ```yaml
    apiVersion: v1
    kind: PersistentVolumeClaim
    metadata:
      name: csi-block-pvc
    spec:
      accessModes:
      - ReadWriteOnce
      resources:
        requests:
          storage: 10Gi
      storageClassName: ibmc-vpc-block-5iops-tier
    ```
    {: codeblock}

    ```sh
    oc create -f pvc.yaml
    ```
    {: pre}

1. Verify that the PVC is created and is in a `Bound` state.
    ```sh
    oc get pvc
    ```
    {: pre}

    ```sh
    NAME                   STATUS   VOLUME                                     CAPACITY   ACCESS MODES   STORAGECLASS                AGE
    csi-block-pvc   Bound    pvc-0798b499-0b61-4f57-a184-4caeb7b9298d   10Gi       RWO            ibmc-vpc-block-5iops-tier   4m22s
    ```
    {: screen}

1. Create a YAML configuration file for a deployment that mounts the PVC that you created.  

    ```yaml
    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: my-deployment
      labels:
        app: my-deployment
    spec:
      replicas: 1
      selector:
        matchLabels:
          app: my-deployment
      template:
        metadata:
          labels:
            app: my-deployment
        spec:
          containers:
          - image: nginx # Your containerized app image
            name: container-name 
            volumeMounts:
            - mountPath: /myvolumepath  # Mount path for PVC
              name: my-vol # Volume mount name
          volumes:
          - name: my-vol  # Volume resource name
            persistentVolumeClaim:
              claimName: csi-block-pvc  # The name of the PVC you created earlier
    ```
    {: codeblock}

    ```sh
    oc create -f pod.yaml
    ```
    {: pre}

1. Verify that the pod is running in your cluster. 
    ```sh
    oc get pods
    ```
    {: pre}
    
    ```sh
    NAME                          READY   STATUS    RESTARTS   AGE
    my-deployment-58dd7c89b6-8zdcl   1/1     Running   0          4m50s    
    ```
    {: screen}
   

1. Now that you have created the pod, log in to the pod and create a text file to use for the snapshot. 
    ```sh
    oc exec -it POD_NAME /bin/bash
    ```
    {: pre}

    Example output

    ```sh
    root@my-deployment-58dd7c89b6-8zdcl:/# cd myvolumepath/
    root@my-deployment-58dd7c89b6-8zdcl:/myvolumepath# echo "hi" > new.txt
    root@my-deployment-58dd7c89b6-8zdcl:/myvolumepath# exit
    ```
    {: screen}


## Creating a volume snapshot
{: #vpc-create-snapshot}

After you create a deployment and a PVC, you can create the volume snapshot resources. 

You can create snapshots only when a volume is attached to a pod.
{: note}

1. Make sure that you have **Share Snapshot Operator** permissions in IAM.

1. Create a volume snapshot resource in your cluster by using the `ibmc-vpcblock-snapshot` snapshot class that is deployed when you enabled the add-on. Save the following `VolumeSnapshot` configuration to a file called `snapvol.yaml`. 

    ```yaml
    apiVersion: snapshot.storage.k8s.io/v1
    kind: VolumeSnapshot
    metadata:
      name: snapshot-csi-block-pvc
    spec:
      volumeSnapshotClassName: ibmc-vpcblock-snapshot
      source:
        persistentVolumeClaimName: csi-block-pvc
    ```
    {: codeblock}

    ```sh
    oc create -f snapvol.yaml
    ```
    {: pre}

1. Verify that the snapshot is ready to use.

    ```sh
    oc get volumesnapshots
    ```
    {: pre}
    
    Example output where `READYTOUSE` is `true`:
    ```sh
    NAME                       READYTOUSE   SOURCEPVC       SOURCESNAPSHOTCONTENT   RESTORESIZE   SNAPSHOTCLASS           SNAPSHOTCONTENT                                    CREATIONTIME   AGE
    snapshot-csi-block-pvc     true         csi-block-pvc                           1Gi           ibmc-vpcblock-snapshot   snapcontent-9c374fbf-43a6-48d6-afc5-e76e1ab7c12b   18h            18h
    ```
    {: screen}


## Creating snapshots in a different resource group
{: #vpc-snapshot-different-rg}

Starting with {{site.data.keyword.block_storage_is_short}} cluster add-on version 5.2.46 and later, you can create volume snapshots in a resource group that is different from your cluster's resource group. This feature provides greater flexibility in resource organization, quota management, and access control.
{: shortdesc}


- **Version requirement**: This feature is supported only in add-on version 5.2.46 and later.
- **Default behavior**: If you don't specify a `resourceGroup` parameter or if you specify an empty string, snapshots are created in the cluster's resource group.


### Prerequisites
{: #vpc-snapshot-different-rg-prereqs}

Before you begin, make sure you have the following permissions in IAM:
- **VPC Infrastructure Services (is)**: Editor and Writer
- **Kubernetes Service (container-kubernetes)**: Operator
- **Resource Group**: Viewer for each resource group where you want to create snapshots

### Creating a custom VolumeSnapshotClass
{: #vpc-snapshot-custom-class}

To create snapshots in a different resource group, you must create a custom `VolumeSnapshotClass` that specifies the target resource group ID.

1. Get the resource group ID where you want to create the snapshot.
    ```sh
    ibmcloud resource groups
    ```
    {: pre}

1. Create a `VolumeSnapshotClass` configuration file. Save the following YAML to a file called `vpc-snap-custom-rg.yaml`. Replace `<RESOURCE_GROUP_ID>` with your target resource group ID.

    ```yaml
    apiVersion: snapshot.storage.k8s.io/v1
    kind: VolumeSnapshotClass
    metadata:
      name: vpc-snap-custom-rg
    driver: vpc.block.csi.ibm.io
    deletionPolicy: Delete
    parameters:
      resourceGroup: <RESOURCE_GROUP_ID>
    ```
    {: codeblock}

    The `resourceGroup` parameter must be the resource group ID, not the resource group name.
    {: important}

1. Create the `VolumeSnapshotClass` in your cluster.
    ```sh
    oc create -f vpc-snap-custom-rg.yaml
    ```
    {: pre}

1. Verify that the `VolumeSnapshotClass` is created.
    ```sh
    oc get volumesnapshotclass
    ```
    {: pre}

### Creating a snapshot with a custom resource group
{: #vpc-snapshot-create-custom-rg}

After you create the custom `VolumeSnapshotClass`, you can create snapshots that reference it.

1. Create a `VolumeSnapshot` configuration file that references your custom snapshot class. Save the following YAML to a file called `snapshot-custom-rg.yaml`.

    ```yaml
    apiVersion: snapshot.storage.k8s.io/v1
    kind: VolumeSnapshot
    metadata:
      name: snapshot-custom-rg
    spec:
      volumeSnapshotClassName: vpc-snap-custom-rg
      source:
        persistentVolumeClaimName: csi-block-pvc
    ```
    {: codeblock}

1. Create the snapshot.
    ```sh
    oc create -f snapshot-custom-rg.yaml
    ```
    {: pre}

1. Verify that the snapshot is ready to use.
    ```sh
    oc get volumesnapshots
    ```
    {: pre}

1. Verify that the snapshot was created in the target resource group by using the IBM Cloud CLI.
    ```sh
    ibmcloud target -g <RESOURCE_GROUP_NAME>
    ibmcloud is snapshots
    ```
    {: pre}


## Restoring from a volume snapshot
{: #vpc-restore-from-snapshot}

After you deploy the snapshot resources, you can restore data to a new volume by using the snapshot. Creating a PVC dynamically provisions a new volume with snapshot data.


1. Create a second PVC that references your volume snapshot. 
    ```yaml
    apiVersion: v1
    kind: PersistentVolumeClaim
    metadata:
      name: restore-pvc
    spec:
      storageClassName: ibmc-vpc-block-5iops-tier
      dataSource:
        name: snapshot-csi-block-pvc
        kind: VolumeSnapshot
        apiGroup: snapshot.storage.k8s.io
      accessModes:
        - ReadWriteOnce
      resources:
        requests:
          storage: 10Gi
    ```
    {: codeblock}

1. Verify that the PVC is created and is in a `Bound` state. 
    ```sh
    oc get pvc
    ```
    {: pre}

    ```sh
    NAME                   STATUS   VOLUME                                     CAPACITY   ACCESS MODES   STORAGECLASS                AGE
    restore-pvc            Bound    pvc-4ede7630-5a49-4bae-b34d-dc528acfb884   10Gi       RWO            ibmc-vpc-block-5iops-tier   18h
    ```
    {: screen}

1. Create a second YAML configuration file for a deployment that mounts the PVC that you created.
    ```yaml
    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: podtwo
      labels:
        app: podtwo
    spec:
      replicas: 1
      selector:
        matchLabels:
          app: podtwo
      template:
        metadata:
          labels:
            app: podtwo
        spec:
          containers:
          - image: nginx # Your containerized app image
            name: container-name
            volumeMounts:
            - mountPath: /myvolumepath  # Mount path for pvc from container
              name: my-vol # Volume mount name
          volumes:
          - name: my-vol  # Volume resource name
            persistentVolumeClaim:
              claimName: restore-pvc   # The name of the PVC that you created earlier
    ```
    {: codeblock}

    ```sh
    oc create -f podtwo.yaml
    ```
    {: pre}

1. Verify that the pod is created.
    ```sh
    oc get pods
    ```
    {: pre}
    
    
    ```sh
    NAME                          READY   STATUS    RESTARTS   AGE
    POD_NAME                      1/1     Running   0          30m
    POD2_NAME                     1/1     Running   0          46h
    ```
    {: screen}

1. Log in to the newly created pod and verify that the sample text file you created earlier is saved to the new pod. 
    ```sh
    oc exec -it POD_NAME /bin/bash
    root@POD_NAME :/# cd myvolumepath/
    root@POD_NAME :/myvolumepath# ls
    lost+found  new.txt
    root@POD_NAME :/myvolumepath# cat new.txt 
    ```
    {: pre}
    
    Example output
    
    ```sh
    hi
    ```
    {: screen}




## Turning off snapshots
{: #vpc-turn-off-snapshots}

By default, snapshot functionality is enabled when using the {{site.data.keyword.block_storage_is_short}}. This functionality can be turned off in the configmap `addon-vpc-block-csi-driver-configmap` in the `kube-system` namespace by changing the `IsSnapshotEnabled` to `false`. Note that with this change in the configmap, any snapshots that are created fail with the message:`CreateSnapshot functionality is disabled`.


1. Save the current configmap from your cluster to your local machine.
    ```sh
    oc get cm -n kube-system addon-vpc-block-csi-driver-configmap -o yaml >> snapshotconfigmap.yaml
    ```
    {: pre}

1. Edit the `IsSnapshotEnabled` parameter to `false`.

1. Save the file and apply your changes. 
    ```sh
    oc apply -f snapshotconfigmap.yaml
    ```
    {: pre}

## Next steps
{: #snapshot-next-steps}

Deploy the snapshot validation webhook to validate user input. For more information, see [Deploying the snapshot validation webhook](https://github.com/kubernetes-sigs/ibm-vpc-block-csi-driver/tree/master/deploy/kubernetes/snapshot/validation-webhook){: external}.


    
## Troubleshooting snapshots
{: #ts-snapshot-vpc-block-addon-next}

Review the following troubleshooting topics.

- [Why can't I create snapshots?](/docs/openshift?topic=openshift-ts-storage-snapshotfails).
- [Why can't I delete my `volumesnapshot` resources?](/docs/openshift?topic=openshift-ts-storage-volumesnapshotdelete)
