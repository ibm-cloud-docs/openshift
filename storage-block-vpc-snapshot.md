---

copyright: 
  years: 2022, 2023
lastupdated: "2023-06-21"

keywords: openshift, block storage, snapshot

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}



# Setting up snapshots with the {{site.data.keyword.block_storage_is_short}} add-on
{: #vpc-volume-snapshot}

[Virtual Private Cloud]{: tag-vpc} 

{{site.data.keyword.block_storage_is_short}} volume snapshots provide you with a standardized way to copy a volume's contents at a particular point in time without creating an entirely new volume. For more information, see [How snapshots work](/docs/vpc?topic=vpc-snapshots-vpc-about).
{: shortdesc}

If you want to see an example scenario using snapshots to back up a WordPress app, see [Point in time backup and restore of a stateful application](https://w3.ibm.com/w3publisher/isl-cloud-platform/blogs/5ef8f200-0e27-11ed-a874-c7aca9398345){: example}.
{: tip}


    
Deploy the snapshot validation webhook to validate user input. For more information, see [Deploying the snapshot validation webhook](https://github.com/kubernetes-sigs/ibm-vpc-block-csi-driver/tree/master/deploy/kubernetes/snapshot/validation-webhook){: external}.
{: tip}


## Creating an app deployment
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
    vpc-block-csi-driver   5.0   normal         Addon Ready. For more info: http://ibm.biz/addon-state (H1500)   
    ```
    {: screen}
    
1. Verify that the driver pods are deployed and the status is `Running`.
    ```sh
    kubectl get pods -n kube-system | grep vpc-block-csi
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

1. Create a PVC that uses the following yaml. 

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
    my-deployment-58dd7c89b6-8zdcl   1/1     Running   0          4m50s    
    ```
    {: screen}
   

1. Now that you have created the pod, log in to the pod and create a text file to use for the snapshot. 
    ```sh
    kubectl exec -it POD_NAME /bin/bash
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

    ```sh
    kubectl create -f snapvol.yaml
    ```
    {: pre}

1. Verify that the snapshot is ready to use.

    ```sh
    kubectl get volumesnapshots
    ```
    {: pre}
    
    Example output where `READYTOUSE` is `true`.
    ```sh
    NAME                            READYTOUSE   SOURCEPVC              SOURCESNAPSHOTCONTENT   RESTORESIZE   SNAPSHOTCLASS SNAPSHOTCONTENT                                    CREATIONTIME   AGE
    ibmc-vpcblock-snapshot   true         csi-block-pvc                           1Gi           ibmc-vpcblock-snapshot   snapcontent-9c374fbf-43a6-48d6-afc5-e76e1ab7c12b   18h            18h
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
    
## Customizing snapshots
{: #vpc-customize-snapshot}

You can edit the add-on configmap for finer control your volume snapshots. First, make sure you have the latest configmap, then update the values based on your environment.

1. Save the current configmap from your cluster to your local machine.
    ```sh
    kubectl get cm -n kube-system addon-vpc-block-csi-driver-configmap -o yaml >> snapshotconfigmap.yaml
    ```
    {: pre}

1. Review the [configmap settings](#vpc-block-configmap-settings) and add any missing values to the `data` section.

1. Add any new parameters to your configmap. If you have previously customized the configmap, make sure to preserve your customizations when adding the new parameters. 

1. Save the file and apply your changes. 
    ```sh
    kubectl apply -f snapshotconfigmap.yaml
    ```
    {: pre}


### `addon-vpc-block-csi-driver-configmap` default settings
{: #vpc-block-configmap-settings}

```yaml
    data:
      IsVolumeSnapshotClassDefault: "true"
      IsStorageClassDefault: "true"
      AttachDetachMinRetryGAP: "3"              #Initial retry interval for checking Attach/Detach Status. Default 3 seconds
      AttachDetachMinRetryAttempt: "3"          #Number of attempts for AttachDetachMinRetryGAP. Default is 3 retries for 3 seconds retry gap.
      AttachDetachMaxRetryAttempt: "46"         #Total number of retries for for checking Attach/Detach Status. Default is 46 times i.e ~7 mins (3 secs * 3 times + 6 secs * 6 times + 10 secs * 10 times)
      AttacherWorkerThreads: "15"               #The number of goroutines for processing VolumeAttachments
      AttacherKubeAPIBurst: "10"                #The number of requests to the Kubernetes API server, exceeding the QPS, that can be sent at any given time
      AttacherKubeAPIQPS: "5.0"                 #The number of requests per second sent by a Kubernetes client to the Kubernetes API server.
      #Requested resources per container
      CSIDriverRegistrarCPURequest: "10m"       #container:csi-driver-registrar, resource-type: cpu-request
      CSIDriverRegistrarMemoryRequest: "20Mi"   #container:csi-driver-registrar,  resource-type: memory-request
      NodeDriverMemoryRequest: "30m"            #container:iks-vpc-block-node-driver, resource-type: cpu-request
      NodeDriverCPURequest: "75Mi"              #container:iks-vpc-block-node-driver, resource-type: memory-request
      LivenessProbeCPURequest: "5m"             #container:liveness-probe, resource-type: cpu-request
      LivenessProbeMemoryRequest: "10Mi"        #container:liveness-probe, resource-type: memory-request
      SecretSidecarCPURequest: "10m"            #container:storage-secret-sidecar, resource-type: cpu-request
      SecretSidecarMemoryRequest: "20Mi"        #container:storage-secret-sidecar, resource-type: memory-request
      CSIProvisionerCPURequest: "20m"           #container:csi-provisioner, resource-type: cpu-request
      CSIProvisionerMemoryRequest: "40Mi"       #container:csi-provisioner, resource-type: memory-request
      CSIAttacherCPURequest: "15m"              #container:csi-attacher, resource-type: cpu-request
      CSIAttacherMemoryRequest: "30Mi"          #container:csi-attacher, resource-type: memory-request
      CSIResizerCPURequest: "20m"               #container:csi-resizer, resource-type: cpu-request
      CSIResizerMemoryRequest: "40Mi"           #container:csi-resizer, resource-type: memory-request
      BlockDriverCPURequest: "75m"              #container:iks-vpc-block-driver, resource-type: cpu-request
      BlockDriverMemoryRequest: "150Mi"         #container:iks-vpc-block-driver, resource-type: memory-request
      CSISnapshotterCPURequest: "20m"           #container:csi-snapshotter, resource-type: cpu-request
      CSISnapshotterMemoryRequest: "40Mi"       #container:csi-snapshotter, resource-type: memory-request
      #Resource Limits per container
      CSIDriverRegistrarCPULimit: "40m"         #container:csi-driver-registrar, resource-type: cpu-limit
      CSIDriverRegistrarMemoryLimit: "80Mi"     #container:csi-driver-registrar, resource-type: memory-limit
      NodeDriverCPULimit: "120m"                #container:iks-vpc-block-node-driver, resource-type: cpu-limit
      NodeDriverMemoryLimit: "300Mi"            #container:iks-vpc-block-node-driver, resource-type: memory-limit
      LivenessProbeCPULimit: "20m"              #container:liveness-probe, resource-type: cpu-limit
      LivenessProbeMemoryLimit: "40Mi"          #container:liveness-probe, resource-type: memory-limit
      SecretSidecarCPULimit: "40m"              #container:storage-secret-sidecar, resource-type: cpu-limit
      SecretSidecarMemoryLimit: "80Mi"          #container:storage-secret-sidecar, resource-type: memory-limit
      CSIProvisionerCPULimit: "80m"             #container:csi-provisioner, resource-type: cpu-limit
      CSIProvisionerMemoryLimit: "160Mi"        #container:csi-provisioner, resource-type: memory-limit
      CSIAttacherCPULimits: "60m"               #container:csi-attacher, resource-type: cpu-limit
      CSIAttacherMemoryLimit: "120Mi"           #container:csi-attacher, resource-type: memory-limit
      CSIResizerCPULimit: "80m"                 #container:csi-resizer, resource-type: cpu-limit
      CSIResizerMemoryLimit: "160Mi"            #container:csi-resizer, resource-type: memory-limit
      BlockDriverCPULimit: "300m"               #container:iks-vpc-block-driver, resource-type: cpu-limit
      BlockDriverMemoryLimit: "600Mi"           #container:iks-vpc-block-driver, resource-type: memory-limit
      CSISnapshotterCPULimit: "80m"             #container:csi-snapshotter, resource-type: cpu-limit
      CSISnapshotterMemoryLimit: "160Mi"        #container:csi-snapshotter, resource-type: memory-limit
      CSISnapshotterRetryIntervalStart: "1s"    #container:csi-snapshotter, Initial retry interval of failed volume snapshot creation or deletion.
      CSISnapshotterRetryIntervalMax: "300s"    #container:csi-snapshotter, Maximum retry interval of failed volume snapshot creation or deletion.
      CSISidecarLogLevel: "5"                   #container:csi-snapshotter, glog/klog log level
      IsSnapshotEnabled : "true"		#container: iks-vpc-block-driver
      CustomSnapshotCreateDelay: "300"		#container: iks-vpc-block-driver
```
{: codeblock}



## Turning off snapshots
{: #vpc-turn-off-snapshots}

By default, snapshot functionality is enabled when using the {{site.data.keyword.block_storage_is_short}}. This functionality can be turned off in the configmap `addon-vpc-block-csi-driver-configmap` in the `kube-system` namespace by changing the `IsSnapshotEnabled` to `false`. Note that with this change in the configmap, any snapshots that are created fail with the message: "CreateSnapshot functionality is disabled." 


1. Save the current configmap from your cluster to your local machine.
    ```sh
    kubectl get cm -n kube-system addon-vpc-block-csi-driver-configmap -o yaml >> snapshotconfigmap.yaml
    ```
    {: pre}

1. Edit the `IsSnapshotEnabled` parameter to `false`.

1. Save the file and apply your changes. 
    ```sh
    kubectl apply -f snapshotconfigmap.yaml
    ```
    {: pre}

    
## Troubleshooting snapshots
{: #ts-snapshot-vpc-block-addon-next}

Review the following troubleshooting topics.

- [Why can't I create snapshots?](/docs/openshift?topic=openshift-ts-storage-snapshotfails).
- [Why can't I delete my `volumesnapshot` resources](/docs/openshift?topic=openshift-ts-storage-volumesnapshotdelete).
