---

copyright: 
  years: 2022, 2022
lastupdated: "2022-08-02"

keywords: openshift, block storage, snapshot

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}

# Setting up snapshots with {{site.data.keyword.block_storage_is_short}} 
{: #vpc-volume-snapshot}

{{site.data.keyword.block_storage_is_short}} volume snapshots provide you with a standardized way to copy a volume's contents at a particular point in time without creating an entirely new volume. For more information, see [How snapshots work](/docs/vpc?topic=vpc-snapshots-vpc-about).
{: shortdesc}

Supported infrastructure provider
:   VPC

Snapshot support is available in {{site.data.keyword.block_storage_is_short}} add-on version `5.0.0-beta` and later.  Version `5.0.0-beta` is available in Beta for allowlisted accounts only. [Contact support](/docs/containers?topic=containers-get-help) for information about how to get added to the allowlist. If you don't need snapshot support, follow the steps to use [{{site.data.keyword.block_storage_is_short}}](/docs/openshift?topic=openshift-vpc-block#vpc-block-add) in your cluster. After version `5.0.0` is released, version `5.0.0-beta` of the add-on becomes depreacted and Beta users must migrate to version `5.0.0`. Do not use the Beta version of the add-on unless you want to test snapshot support.
{: important}

## Enabling the {{site.data.keyword.block_storage_is_short}} add-on
{: #vpc-addon-enable}

1. [Log in to your account. If applicable, target the appropriate resource group. Set the context for your cluster.](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure)

1. Get the version number of the `vpc-block-csi-driver` add-on that is installed in your cluster.
    ```sh
    ibmcloud oc cluster addon ls --cluster CLUSTER
    ```
    {: pre}


1. If you have an add-on version earlier than `5.0.0-beta` of the {{site.data.keyword.block_storage_is_short}} add-on installed in your cluster, you must first disable the add-on and then enable version 5.0.0 or later. 
    ```sh
    ibmcloud oc cluster addon disable vpc-block-csi-driver  --cluster CLUSTER-ID
    ```
    {: pre}

    ```sh
    ibmcloud oc cluster addon enable vpc-block-csi-driver --version 5.0.0-beta --cluster CLUSTER-ID
    ```
    {: pre}

    Example output.
    ```sh
    Enabling add-on vpc-block-csi-driver(5.0.0-beta) for cluster CLUSTER-ID
    The add-on might take several minutes to deploy and become ready for use.
    ```
    {: screen}

1. Verify that the add-on state is `normal` and the status is `ready`.
    If you enabled the add-on, but the state is `critical`, then your account is not allowlisted. [Contact support](/docs/containers?topic=containers-get-help) for information about how to get added to the allowlist. Retry the steps to enable the add-on after your account is allowlisted.
    {: note}
    
    ```sh
    ibmcloud oc cluster addon ls --cluster CLUSTER-ID
    ```
    {: pre}

    ```sh
    Name                   Version                     Health State   Health Status   
    vpc-block-csi-driver   5.0.0-beta* (4.3 default)   normal         Addon Ready. For more info: http://ibm.biz/addon-state (H1500)   
    ```
    {: screen}

    
1. Verify that the driver pods are deployed and the status is `Running`.
    ```sh
    kubectl get pods -n kube-system | grep block
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

## Creating a deployment
{: #vpc-snapshot-deployment}

Create an example Persistent Volume Claim (PVC) and deploy a pod that references that claim. 
{: shortdesc}

1. Create a PVC that uses the following yaml. 

    ```yaml
    apiVersion: v1
    kind: PersistentVolumeClaim
    metadata:
        name: csi-block-pvc-custom
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
    kubectl create -f pvc.yaml
    ```
    {: pre}

1. Verify that the PVC is created and is in a `Bound` state.
    ```sh
    kubectl get pvc
    ```
    {: pre}

    ```sh
    NAME                   STATUS   VOLUME                                     CAPACITY   ACCESS MODES   STORAGECLASS                AGE
    csi-block-pvc-custom   Bound    pvc-0798b499-0b61-4f57-a184-4caeb7b9298d   10Gi       RWO            ibmc-vpc-block-5iops-tier   4m22s
    ```
    {: screen}

1. Create a YAML configuration file for a deployment that mounts the PVC that you created.  

    ```yaml
    apiVersion: apps/v1
    kind: Deployment
    metadata:
        name: testcustom
        labels:
            app: testcustom
    spec:
        replicas: 1
        selector:
            matchLabels:
            app: testcustom
        template:
            metadata:
                labels:
                    app: testcustom
            spec:
                containers:
                - image: nginx #image name which should be avilable within cluster
                  name: container-name # name of the container inside POD
                  volumeMounts:
                  - mountPath: /myvolumepath  # mount path for pvc from container
                    name: pvc-name # pvc name for this pod
                volumes:
                 - name: pvc-name  # volume resource name in this POD, user can choose any name as per kubernetes
                 persistentVolumeClaim:
                    claimName: csi-block-pvc-custom  # pvc name which was created by using claim.yaml file
    ```
    {: codeblock}

    ```sh
    kubectl create -f pod.yaml
    ```
    {: pre}

1. Verify that the pod is running in your cluster. 
    ```sh
    kubectl get pods
    ```
    {: pre}
    
    ```sh
    NAME                          READY   STATUS    RESTARTS   AGE
    testcustom-58dd7c89b6-8zdcl   1/1     Running   0          4m50s    
    ```
    {: screen}
   

1. Now that you have created the pod, log in to the pod and create a text file to use for the snapshot. 
    ```sh
    kubectl exec -it POD_NAME /bin/bash
    ```
    {: pre}

    Example output

    ```sh
    root@testcustom-58dd7c89b6-8zdcl:/# cd myvolumepath/
    root@testcustom-58dd7c89b6-8zdcl:/myvolumepath# echo "hi" > new.txt
    root@testcustom-58dd7c89b6-8zdcl:/myvolumepath# exit
    ```
    {: screen}


## Creating a volume snapshot
{: #vpc-create-snapshot}

After you create a deployment and a PVC, you can create the volume snapshot resources.

1. Verify your volume is in the `attached` state.

    ```sh
    oc get pvc
    ```
    {: pre}


1. Create a volume snapshot resource in your cluster by using the `vpc-block-snapshot` snapshot class that is deployed when you enabled the add-on. Save the following VolumeSnapshot configuration to a file called `snapvol.yaml`. 

    ```yaml
    apiVersion: snapshot.storage.k8s.io/v1
    kind: VolumeSnapshot
    metadata:
        name: vpc-block-snapshot
    spec:
        volumeSnapshotClassName: vpc-block-snapshot
        source:
            persistentVolumeClaimName: csi-block-pvc-custom
    ```
    {: codeblock}

    ```sh
    kubectl create -f snapvol.yaml
    ```
    {: pre}

1. Verify that the snapshot is created and ready to use.

    ```sh
    kubectl get volumesnapshots
    ```
    {: pre}
    
    Example output where `READYTOUSE` is `true`.
    ```sh
    NAME                            READYTOUSE   SOURCEPVC              SOURCESNAPSHOTCONTENT   RESTORESIZE   SNAPSHOTCLASS SNAPSHOTCONTENT                                    CREATIONTIME   AGE
    snapshot-csi-block-pvc-custom   true         csi-block-pvc-custom                           1Gi           snapshotclass   snapcontent-9c374fbf-43a6-48d6-afc5-e76e1ab7c12b   18h            18h
    ```
    {: screen}

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
            name: snapshot-csi-block-pvc-custom
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
    kubectl get pvc
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
            - image: nginx #image name which should be avilable within cluster
                name: container-name # name of the container inside POD
                volumeMounts:
                - mountPath: /myvolumepath  # mount path for pvc from container
                name: pvc-name # pvc name for this pod
            volumes:
            - name: pvc-name  # volume resource name in this POD, user can choose any name as per kubernetes
                persistentVolumeClaim:
                claimName: restore-pvc   # pvc name which was created by using claim.yaml file
    ```
    {: codeblock}

    ```sh
    kubectl create -f podtwo.yaml
    ```
    {: pre}

1. Verify that the pod is created.
    ```sh
    kubectl get pods
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
    kubectl exec -it POD_NAME /bin/bash
    root@POD_NAME :/# cd myvolumepath/
    root@POD_NAME :/myvolumepath# ls
    lost+found  new.txt
    root@POD_NAME :/myvolumepath# cat new.txt 
    ```
    {: pre}
    
    Example output.
    
    ```sh
    hi
    ```
    {: screen}
    
    
    
