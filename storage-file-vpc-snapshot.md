---

copyright: 
  years: 2025, 2025
lastupdated: "2025-12-11"


keywords: openshift, containers, file storage for vpc, snapshots, create snapshot

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}


# Setting up snapshots for {{site.data.keyword.filestorage_vpc_short}}
{: #vpc-volume-snapshot-file}

[Virtual Private Cloud]{: tag-vpc} 

{{site.data.keyword.filestorage_vpc_short}} volume snapshots provide you with a standardized way to copy a volume's contents at a particular point in time without creating an entirely new volume. Snapshots are supported for both zonal(dp2) and regional (rfs) based storage classes. For more information about snapshots, see [How snapshots work](/docs/vpc?topic=vpc-fs-snapshots-about). 
{: shortdesc}

For more information about {{site.data.keyword.filestorage_vpc_short}}, see [About {{site.data.keyword.filestorage_vpc_short}}](/docs/vpc?topic=vpc-file-storage-vpc-about).


Snapshots support for the {{site.data.keyword.filestorage_vpc_short}} add-on is currently in Beta.
{: beta}

If the PVC (file share) is deleted, then all the corresponding snapshots owned by the file share are deleted. In this case CSI volume snapshots remain, but the backend snapshots in VPC will not exists. Therefore, you must delete volumes by using `oc delete vs <snapshot-name>`.
{: note}

## Prerequisites
{: #snapshot-file-pre}

- Make sure you have the {{site.data.keyword.filestorage_vpc_short}} add-on installed in your cluster.
- Make sure you have **Share Snapshot Operator** [permissions in IAM](/docs/account?topic=account-iam-service-roles-actions#is.share-roles).


## Creating an app
{: #vpc-snapshot-deployment-file}

Create an example Persistent Volume Claim (PVC) and deploy a pod that references that claim. 
{: shortdesc}

1. [Log in to your account. If applicable, target the appropriate resource group. Set the context for your cluster.](/docs/containers?topic=containers-access_cluster)

1. Verify that the add-on state is `normal` and the status is `Ready`.
    
    ```sh
    ibmcloud oc cluster addon ls --cluster CLUSTER-ID
    ```
    {: pre}

    ```sh
    Name                    Version                     Health State   Health Status   
    vpc-file-csi-driver     2.0                         normal         Addon Ready. For more info: http://ibm.biz/addon-state (H1500)
    ```
    {: screen}
    
1. Verify that the driver pods are deployed and the status is `Running`.
    ```sh
    oc get pods -n kube-system | grep vpc-file-csi
    ```
    {: pre}
    
    Example output
    ```sh                    
    ibm-vpc-file-csi-controller-s34sw                    7/7     Running   0          77s
    ibm-vpc-file-csi-controller-7hdhd                    7/7     Running   0          77s
    ibm-vpc-file-csi-node-56c85                          4/4     Running   0          77s
    ibm-vpc-file-csi-node-87j2t                          4/4     Running   0          77s
    ibm-vpc-file-csi-node-cmh2h                          4/4     Running   0          77s
    ```
    {: screen}

1. Create a PVC. 

    ```yaml
    apiVersion: v1
    kind: PersistentVolumeClaim
    metadata:
      name: csi-file-pvc
    spec:
      accessModes:
      - ReadWriteMany
      resources:
        requests:
          storage: 10Gi
      storageClassName: ibmc-vpc-file-min-iops
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
    NAME           STATUS   VOLUME                                     CAPACITY   ACCESS MODES   STORAGECLASS             VOLUMEATTRIBUTESCLASS   AGE
    csi-file-pvc   Bound    pvc-9873bd7e-41a8-4234-a9bf-271b8ca7e4f9   10Gi       RWM          ibmc-vpc-file-min-iops   <unset>                 5
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
            claimName: csi-file-pvc  # The name of the PVC you created earlier

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
    oc exec -it POD_NAME -- /bin/bash
    ```
    {: pre}

    Example commands to create a new text file.

    ```sh
    root@my-deployment-58dd7c89b6-8zdcl:/# cd myvolumepath/
    root@my-deployment-58dd7c89b6-8zdcl:/myvolumepath# echo "hi" > new.txt
    root@my-deployment-58dd7c89b6-8zdcl:/myvolumepath# exit
    ```
    {: screen}


## Creating a volume snapshot
{: #vpc-create-snapshot}

After you create a deployment and a PVC, you can create the volume snapshots.

1. Make sure you have **Share Snapshot Operator** [permissions in IAM](/docs/account?topic=account-iam-service-roles-actions#is.share-roles).

1. Create a volume snapshot in your cluster by using the `ibmc-vpcfile-snapshot` snapshot class that is deployed when you enabled the add-on. Save the following VolumeSnapshot configuration to a file called `snapvol.yaml`. 

    ```yaml
    apiVersion: snapshot.storage.k8s.io/v1
    kind: VolumeSnapshot
    metadata:
      name: snapshot-csi-file-pvc
    spec:
      volumeSnapshotClassName: ibmc-vpcfile-snapshot-delete
      source:
        persistentVolumeClaimName: csi-file-pvc
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
    
    Example output where `READYTOUSE` is `true`.
    ```sh
    NAME                            READYTOUSE   SOURCEPVC              SOURCESNAPSHOTCONTENT   RESTORESIZE   SNAPSHOTCLASS SNAPSHOTCONTENT                                    CREATIONTIME   AGE
    ibmc-vpcfile-snapshot-delete   true         csi-file-pvc                           10Gi           ibmc-vpcfile-snapshot-delete   snapcontent-9c374fbf-43a6-48d6-afc5-e76e1ab7c12b   18h            18h
    ```
    {: screen}

## Restoring from a volume snapshot
{: #vpc-restore-from-snapshot}

After you deploy the volume snapshot, you can restore data to a new volume by using the snapshot. Creating a PVC dynamically provisions a new volume with snapshot data.


1. Create a second PVC that references your volume snapshot. 
    ```yaml
    apiVersion: v1
    kind: PersistentVolumeClaim
    metadata:
      name: restore-pvc
    spec:
      storageClassName: ibmc-vpc-file-min-iops
      dataSource:
        name: snapshot-csi-file-pvc
        kind: VolumeSnapshot
        apiGroup: snapshot.storage.k8s.io
      accessModes:
        - ReadWriteMany
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
    NAME           STATUS   VOLUME                                     CAPACITY   ACCESS MODES   STORAGECLASS             VOLUMEATTRIBUTESCLASS   AGE
    csi-file-pvc   Bound    pvc-9873bd7e-41a8-4234-a9bf-271b8ca7e4f9   10Gi       RWM            ibmc-vpc-file-min-iops   <unset>                 9m16s
    restore-pvc    Bound    pvc-04dc8d6c-ac75-48b1-989d-ed67deb35911   10Gi       RWM            ibmc-vpc-file-min-iops   <unset>                 116s
    ```
    {: screen}

1. Create a second YAML configuration file for a deployment that mounts the PVC that you created.
    ```yaml
    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: restore-pod
      labels:
        app: restore-pod
    spec:
      replicas: 1
      selector:
        matchLabels:
          app: restore-pod
      template:
        metadata:
          labels:
            app: restore-pod
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
    oc create -f restore-pod.yaml
    ```
    {: pre}

1. Verify that the pod is created.
    ```sh
    oc get pods
    ```
    {: pre}
    
    
    ```sh
    NAME                          READY   STATUS    RESTARTS   AGE
    restore-pod-1                      1/1     Running   0          30m
    pod-2                     1/1     Running   0          46h
    ```
    {: screen}

1. Log in to the newly created pod and verify that the sample text file you created earlier is saved to the new pod. 
    ```sh
    oc exec -it POD_NAME -- /bin/bash
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

## Restoring static snapshots
{: #file-static-snapshot-restore}

Complete the following steps to restore a static snapshot.

1. [Log in to your account. If applicable, target the appropriate resource group. Set the context for your cluster.](/docs/containers?topic=containers-access_cluster)

1. Get snapshot CRN using
    ```sh
    ibmcloud is share-snapshot <share-id> <share-snapshot-id> | grep CRN
    ```
    {: pre}

    Example output
    ```sh
    CRN  crn:v1:staging:public:is:us-south-3:a/77f2bceddaeb577dcaddb4073fe82c1c::share-snapshot:r134-1b3af00c-7a07-4ba7-b005-f6723c5b5e98/r134-164521b1-f5c1-4968-9605-a7aaa7e6cd2f
    ```
    {: pre}

1. Create a `VolumeSnapshotContent` resource. Save the following configuration as a file called `volsnapcontent.yaml`.

    ```yaml
    apiVersion: snapshot.storage.k8s.io/v1
    kind: VolumeSnapshotContent
    metadata:
      name: static-file-snapshot-cnt
    spec:
      volumeSnapshotClassName: ibmc-vpcfile-snapshot-retain
      deletionPolicy: Retain
      driver: vpc.file.csi.ibm.io
      source:
        snapshotHandle: crn:v1:staging:public:is:us-south-3:a/77f2bceddaeb577dcaddb4073fe82c1c::share-snapshot:r134-1b3af00c-7a07-4ba7-b005-f6723c5b5e98/r134-164521b1-f5c1-4968-9605-a7aaa7e6cd2f  # Enter the CRN of the snapshot you created earlier. For example crn:v1:public:is:us-south:a/8ee729d7f903db130b00257d91b6977f::snapshot:r134-64c3ad8e-786e-4f54-9b63-388615811ba6
      volumeSnapshotRef:
        name: static-file-snapshot
        namespace: default
    ```
    {: codeblock}

    ```sh
    oc apply -f volsnapcontent.yaml
    ```
    {: pre}

    Example output
    ```sh
    volumesnapshot.snapshot.storage.k8s.io/crossaccount-snapshot created
    ```
    {: screen}

1. Create a VolumeSnapshot. Save the following configuration as a file called volsnap.yaml.

    ```yaml
    apiVersion: snapshot.storage.k8s.io/v1
    kind: VolumeSnapshot
    metadata:
      name: static-file-snapshot
      namespace: default
    spec:
      volumeSnapshotClassName: ibmc-vpcfile-snapshot-retain
      source:
        volumeSnapshotContentName: static-file-snapshot-cnt # Enter the name of the VolumeSnapshotContent that you created in the previous step.
    ```
    {: codeblock}

    ```sh
    oc apply -f volsnap.yaml
    ```
    {: pre}

1. Create a PVC. Save the following configuration as a file called `pvc2.yaml`.

    ```yaml
    apiVersion: v1
    kind: PersistentVolumeClaim
    metadata:
      name: restore-static-pvc
    spec:
      storageClassName: ibmc-vpc-file-min-iops
      dataSource:
        name: static-file-snapshot
        kind: VolumeSnapshot
        apiGroup: snapshot.storage.k8s.io
      accessModes:
        - ReadWriteMany
       resources:
        requests:
          storage: 10Gi
    ```
    {: codeblock}

    ```sh
    oc apply -f pvc2.yaml
    ```
    {: pre}

    Redeploy your app.

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
              claimName: restore-static-pvc  # The name of the PVC you created earlier
    ```
    {: codeblock}

    ```sh
    oc create -f dep2.yaml
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

1. Log in to the newly created pod and verify that the sample text file you created earlier is saved to the new pod.
    ```sh
    root@my-deployment-static-768f64ffcf-h6qft:/# cd myvolumepath/
    root@my-deployment-static-768f64ffcf-h6qft:/myvolumepath# ls
    new.txt
    root@my-deployment-static-768f64ffcf-h6qft:/myvolumepath# cat new.txt 
    hi
    ```
    {: screen}

## Turning off snapshots
{: #vpc-turn-off-snapshots}

By default, snapshot functionality is enabled when using the {{site.data.keyword.filestorage_vpc_short}}. This functionality can be turned off in the configmap `addon-vpc-file-csi-driver-configmap` in the `kube-system` namespace by changing the `IsSnapshotEnabled` to `false`. Note that with this change in the configmap, any snapshots that are created fail with the message:`CreateSnapshot functionality is disabled`.


1. Save the current configmap from your cluster to your local machine.
    ```sh
    oc get cm -n kube-system addon-vpc-file-csi-driver-configmap -o yaml >> snapshotconfigmap.yaml
    ```
    {: pre}

1. Edit the `IS_SNAPSHOT_ENABLED` paramter to `false`.

    ```txt
    IS_SNAPSHOT_ENABLED:false
    ```
    {: codeblock}

1. Save the file and apply your changes. 
    ```sh
    oc apply -f snapshotconfigmap.yaml
    ```
    {: pre}
