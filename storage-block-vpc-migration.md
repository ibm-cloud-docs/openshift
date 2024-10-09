---

copyright: 
  years: 2024, 2024
lastupdated: "2024-10-09"


keywords: openshift, migration, block storage for vpc, snapshots

subcollection: openshift

content-type: tutorial
services: containers, vpc
account-plan: paid
completion-time: 2h

---

{{site.data.keyword.attribute-definition-list}}



# Migrating {{site.data.keyword.block_storage_is_short}} apps and data between IBM Cloud accounts
{: #storage-block-vpc-migration}
{: toc-content-type="tutorial"}
{: toc-services="containers, vpc"}
{: toc-completion-time="2h"}

[Virtual Private Cloud]{: tag-vpc}

In this tutorial, you'll migrate a {{site.data.keyword.block_storage_is_short}} app and snapshot data from an {{site.data.keyword.containerlong_notm}} cluster in one account, to a {{site.data.keyword.openshiftlong_notm}} cluster in a separate account.


## Prerequisites
{: #vpc-block-migration-prereqs}


[Account 1]{: tag-purple}

In Account 1, you must have the following.

* An {{site.data.keyword.containerlong_notm}} cluster.

* A app that uses {{site.data.keyword.block_storage_is_short}} and a snapshot of your app data. For more information, see [Setting up snapshots with the {{site.data.keyword.block_storage_is_short}} cluster add-on](/docs/openshift?topic=openshift-vpc-volume-snapshot#vpc-snapshot-deployment).


[Account 2]{: tag-teal}

In Account 2, the destination account to migrate to, you must have the following.

* A {{site.data.keyword.openshiftlong_notm}} cluster.

## Get your account IDs
{: #vpc-block-mig-account-IDs}
{: step}

[Account 1]{: tag-purple} [Account 2]{: tag-teal}


For each account, get your account IDs from the **Account settings** [page](https://cloud.ibm.com/account/settings){: external}.


## Set up your permissions
{: #vpc-block-mig-s2s}
{: step}

[Account 1]{: tag-purple}

In Account 1, from the [IAM authorizations page](https://cloud.ibm.com/iam/authorizations/grant){: external} give account to access to **Block Storage Snapshots for VPC**.

1. In the **Source account** panel, select **Specific account**, then enter the account ID of **Account 2**.
1. In the **Service** panel, select **VPC Infrastructure Services**.
1. In the **Resources** panel, select **Specific resources**, then select **Block Storage Snapshots for VPC**.
1. **Optional** You can also scope the authorization to a specific snapshot or a specific resource group by adding a condition.


[Account 2]{: tag-teal}

In Account 2, from the [IAM Users page](https://cloud.ibm.com/iam/users){: external}, give the user who is completing this tutorial the **Snapshot Remote Account Restorer** permissions.

1. Select the user that you want to assign the **Snapshot Remote Account Restorer** permissions to.
1. On the **Access tab**, click **Assign access**.
1. In the **Service** field, select **VPC Infrastructure Services**.
1. In the **Resources** field, select **Specific resources**, then select **Resource type** and **Block Storage Snapshots for VPC**.
1. In the **Roles and actions**, select **Snapshot Remote Account Restorer**.
1. Click **Add**, then **Assign** to finish assigning access.


## Optional: Deploy an app
{: #vpc-block-mig-deploy}
{: step}

[Account 1]{: tag-purple}

If you don't already have an app to migrate, you can deploy the following example app.

1. [Log in to your account. If applicable, target the appropriate resource group. Set the context for your cluster.](/docs/containers?topic=containers-access_cluster)

1. Verify that the add-on state is `normal` and the status is `Ready`.
    
    ```txt
    ibmcloud oc cluster addon ls --cluster CLUSTER-ID
    ```
    {: pre}

    ```txt
    Name                   Version                     Health State   Health Status   
    vpc-block-csi-driver   5.0   normal         Addon Ready. For more info: http://ibm.biz/addon-state (H1500)   
    ```
    {: screen}
    
1. Verify that the driver pods are deployed and the status is `Running`.
    ```txt
    oc get pods -n kube-system | grep vpc-block-csi
    ```
    {: pre}
    
    Example output
    ```txt                    
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

    ```txt
    oc create -f pvc.yaml
    ```
    {: pre}

1. Verify that the PVC is created and is in a `Bound` state.
    ```txt
    oc get pvc
    ```
    {: pre}

    ```txt
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

    ```txt
    oc create -f pod.yaml
    ```
    {: pre}

1. Verify that the pod is running in your cluster. 
    ```txt
    oc get pods
    ```
    {: pre}
    
    ```txt
    NAME                          READY   STATUS    RESTARTS   AGE
    my-deployment-58dd7c89b6-8zdcl   1/1     Running   0          4m50s    
    ```
    {: screen}
   

1. Now that you have created the pod, log in to the pod and create a text file to use for the snapshot. 
    ```txt
    oc exec -it POD_NAME /bin/bash
    ```
    {: pre}

    Example output

    ```txt
    root@my-deployment-58dd7c89b6-8zdcl:/# cd myvolumepath/
    root@my-deployment-58dd7c89b6-8zdcl:/myvolumepath# echo "hi" > new.txt
    root@my-deployment-58dd7c89b6-8zdcl:/myvolumepath# exit
    ```
    {: screen}

## Create a snapshot
{: #vpc-block-mig-snapshot}
{: step}

[Account 1]{: tag-purple}

After you create a deployment and a PVC, you can create the volume snapshot resources. 

You can creating snapshots only when a volume is attached to a pod.
{: note}


1. Create a volume snapshot resource in your cluster by using the `ibmc-vpcblock-snapshot` snapshot class that is deployed when you enabled the add-on. Save the following VolumeSnapshot configuration to a file called `snapvol.yaml`. 

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

    ```txt
    oc create -f snapvol.yaml
    ```
    {: pre}

1. Verify that the snapshot is ready to use and make a note of the `SNAPSHOTCONTENT`.

    ```txt
    oc get volumesnapshots
    ```
    {: pre}
    
    Example output where `READYTOUSE` is `true`.
    ```txt
    NAME                            READYTOUSE   SOURCEPVC              SOURCESNAPSHOTCONTENT   RESTORESIZE   SNAPSHOTCLASS SNAPSHOTCONTENT                                    CREATIONTIME   AGE
    ibmc-vpcblock-snapshot   true         csi-block-pvc                           1Gi           ibmc-vpcblock-snapshot   snapcontent-9c374fbf-43a6-48d6-afc5-e76e1ab7c12b   18h            18h
    ```
    {: screen}

## Get the details of your snapshot
{: #vpc-block-mig-snapshot-details}
{: step}

[Account 1]{: tag-purple}

1. Get the details of your `volumesnapshotcontent` by using the `SNAPSHOTCONTENT` you found in the previous step.

    ```sh
    oc describe volumesnapshotcontent snapcontent-9c374fbf-43a6-48d6-afc5-e76e1ab7c12b
    ```
    {: pre}

    Example output
    ```yaml
    Name:         snapcontent-995f295b-6036-4d67-ab03-bba8557a0884
    Namespace:    
    Labels:       <none>
    Annotations:  <none>
    API Version:  snapshot.storage.k8s.io/v1
    Kind:         VolumeSnapshotContent
    Metadata:
      Creation Timestamp:  2024-09-24T11:08:18Z
      Finalizers:
        snapshot.storage.kubernetes.io/volumesnapshotcontent-bound-protection
      Generation:  1
      Managed Fields:
        API Version:  snapshot.storage.k8s.io/v1
        Fields Type:  FieldsV1
        fieldsV1:
          f:metadata:
            f:finalizers:
              .:
              v:"snapshot.storage.kubernetes.io/volumesnapshotcontent-bound-protection":
          f:spec:
            .:
            f:deletionPolicy:
            f:driver:
            f:source:
              .:
              f:volumeHandle:
            f:sourceVolumeMode:
            f:volumeSnapshotClassName:
            f:volumeSnapshotRef:
        Manager:      snapshot-controller
        Operation:    Update
        Time:         2024-09-24T11:08:18Z
        API Version:  snapshot.storage.k8s.io/v1
        Fields Type:  FieldsV1
        fieldsV1:
          f:status:
            .:
            f:creationTime:
            f:readyToUse:
            f:restoreSize:
            f:snapshotHandle:
        Manager:         csi-snapshotter
        Operation:       Update
        Subresource:     status
        Time:            2024-09-24T11:08:43Z
      Resource Version:  1501448
      UID:               ad50aa42-8056-4264-9188-a13da3aaebca
    Spec:
      Deletion Policy:  Delete
      Driver:           vpc.block.csi.ibm.io
      Source:
        Volume Handle:             r134-c7e32d5b-3a42-4d3e-b5e9-772b84566eaf
      Source Volume Mode:          Filesystem
      Volume Snapshot Class Name:  ibmc-vpcblock-snapshot-delete
      Volume Snapshot Ref:
        API Version:       snapshot.storage.k8s.io/v1
        Kind:              VolumeSnapshot
        Name:              new-snapshot-with-crn
        Namespace:         default
        Resource Version:  1501308
        UID:               995f295b-6036-4d67-ab03-bba8557a0884
    Status:
      Creation Time:    1727176105000000000
      Ready To Use:     true
      Restore Size:     10737418240
      Snapshot Handle:  crn:v1:staging:public:is:us-south:a/1152aa1c1ec54274ac42b8ad8507c90c::snapshot:r134-12f0bdb5-21e6-4e6b-8b5c-ce9a1b378ec5
    Events:             <none>
    ```
    {: screen}

1. In the output, make a note of the `Snapshot Handle`. In this example, it is `crn:v1:staging:public:is:us-south:a/1152aa1c1ec54274ac42b8ad8507c90c::snapshot:r134-12f0bdb5-21e6-4e6b-8b5c-ce9a1b378ec5`.

## Restore the snapshot in Account 2
{: #vpc-block-mig-snapshot-restore}
{: step}

[Account 2]{: tag-teal}

1. [Access your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-access_cluster).

1. Create a `VolumeSnapshotContent` resource. Save the following configuration as a file called `volsnapcontent.yaml`.
    ```yaml
    apiVersion: snapshot.storage.k8s.io/v1
    kind: VolumeSnapshotContent
    metadata:
      name: crossaccount-snapshot-cnt
    spec:
      volumeSnapshotClassName: ibmc-vpcblock-snapshot-retain
      deletionPolicy: Retain
      driver: vpc.block.csi.ibm.io
      source:
        snapshotHandle: CRN # Enter the CRN of the snapshot you created earlier. For example crn:v1:public:is:us-south:a/8ee729d7f903db130b00257d91b6977f::snapshot:r134-64c3ad8e-786e-4f54-9b63-388615811ba6
      volumeSnapshotRef:
        name: crossaccount-snapshot
        namespace: default
    ```
    {: codeblock}

1. Create the `VolumeSnapshotContent` in your cluster.
    ```sh
    oc apply -f volsnapcontent.yaml
    ```
    {: pre}

    Example output
    ```txt
    volumesnapshot.snapshot.storage.k8s.io/crossaccount-snapshot created
    ```
    {: screen}

1. Create a `VolumeSnapshot`. Save the following configuration as a file called `volsnap.yaml`.
    ```yaml
    kind: VolumeSnapshot
    metadata:
      name: crossaccount-snapshot
      namespace: default
    spec:
      volumeSnapshotClassName: ibmc-vpcblock-snapshot-retain
      source:
        volumeSnapshotContentName: crossaccount-snapshot-cnt # Enter the name of the VolumeSnapshotContent that you created in the previous step.
    ```
    {: codeblock}

1. Create the `VolumeSnapshot` in your cluster.
    ```sh
    oc apply -f volsnap.yaml
    ```
    {: pre}


1. Create a PVC. Save the following configuration as a file called `pvc2.yaml`

    ```yaml
    apiVersion: v1
    kind: PersistentVolumeClaim
    metadata:
      name: restore-cross-pvc
    spec:
      storageClassName: ibmc-vpc-block-5iops-tier
      dataSource:
        name: crossaccount-snapshot
        kind: VolumeSnapshot
        apiGroup: snapshot.storage.k8s.io
      accessModes:
        - ReadWriteOnce
      resources:
        requests:
          storage: 10Gi
    ```
    {: codeblock}

1. Create the PVC in your cluster.
    ```sh
    oc apply -f pvc2.yaml
    ```
    {: pre}

## Redploy your app
{: #vpc-block-mig-snapshot-redeploy}
{: step}

[Account 2]{: tag-teal}

1. Copy the following example deployment and save it to a file called `dep2.yaml`.  

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
              claimName: restore-cross-pvc  # The name of the PVC you created earlier
    ```
    {: codeblock}

    ```txt
    oc create -f dep2.yaml
    ```
    {: pre}

1. Verify that the pod is running in your cluster. 
    ```txt
    oc get pods
    ```
    {: pre}
    
    ```txt
    NAME                          READY   STATUS    RESTARTS   AGE
    my-deployment-58dd7c89b6-8zdcl   1/1     Running   0          4m50s    
    ```
    {: screen}

## Continue migrating your snapshots and apps to Account 2
{: #vpc-block-mig-snapshot-next}
{: step}

[Account 2]{: tag-teal}

Repeat this tutorial for any additional snapshots and apps that you want to migrate across accounts.
