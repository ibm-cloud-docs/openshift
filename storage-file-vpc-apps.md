---

copyright: 
  years: 2022, 2024
lastupdated: "2024-03-28"


keywords: openshift

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}

# Adding {{site.data.keyword.filestorage_vpc_short}} to apps
{: #storage-file-vpc-apps}

{{site.data.keyword.containerlong}} provides pre-defined storage classes for {{site.data.keyword.filestorage_vpc_short}} that you can use to provision {{site.data.keyword.filestorage_vpc_short}} with a specific configuration.
{: shortdesc}

Every storage class specifies the type of {{site.data.keyword.filestorage_vpc_short}} that you provision, including available size, IOPS, file system, and the retention policy.  

After you provision a specific type of storage by using a storage class, you can't change the type, or retention policy for the storage device. However, you can [change the size and the IOPS](/docs/vpc?topic=vpc-file-storage-profiles#fs-tiers){: external} if you want to increase your storage capacity and performance. To change the type and retention policy for your storage, you must create a new storage instance and copy the data from the old storage instance to your new one.

Decide on a storage class. For more information, see the [storage class reference](/docs/openshift?topic=openshift-storage-file-vpc-managing).

New security group rules have been introduced in versions 4.11 and later. These rule changes mean you must sync your security groups before you can use {{site.data.keyword.filestorage_vpc_short}}.
{: important}

Run the following commands to sync your security group settings.


1. Get the ID of the `kube-<cluster-id>` security group.
    ```sh
    ibmcloud is sg kube-<cluster-id>  | grep ID
    ```
    {: pre}

1. Sync your security group settings.
    ```sh
    ibmcloud ks security-group sync -c <cluster ID> --security-group <ID>
    ```
    {: pre}

## Quick start for {{site.data.keyword.filestorage_vpc_short}} with dynamic provisioning
{: #vpc-add-file-dynamic}

Create a persistent volume claim (PVC) to dynamically provision {{site.data.keyword.filestorage_vpc_short}} for your cluster. Dynamic provisioning automatically creates the matching persistent volume (PV) and orders the file share in your account.

1. [Access your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-access_cluster).

1. Save the following code to a file called `my-pvc.yaml`. This code creates a claim that is named `my-pvc` by using the `ibmc-vpc-file-dp2` storage class, billed `monthly`, with a gigabyte size of `10Gi`.

    ```yaml
    apiVersion: v1
    kind: PersistentVolumeClaim
    metadata:
      name: my-pvc # Enter a name for your PVC.
    spec:
      accessModes:
      - ReadWriteMany # The PVC can be mounted by multiple pods. All pods can read from and write to the volume.
      resources:
        requests:
          storage: 10Gi # Enter the size of the storage in gigabytes (Gi).
      storageClassName: ibmc-vpc-file-dp2 # Enter the name of the storage class that you want to use.
    ```
      {: codeblock}

1. Create the PVC.

    ```sh
    oc apply -f my-pvc.yaml
    ```
    {: pre}

1. Verify that your PVC is created and bound to the PV. This process can take a few minutes.

    ```sh
    oc describe pvc my-pvc
    ```
    {: pre}

    Example output

    ```sh
    Name:        my-pvc
    Namespace:    default
    StorageClass:    ""
    Status:        Bound
    Volume:        pvc-0d787071-3a67-11e7-aafc-eef80dd2dea2
    Labels:        <none>
    Capacity:    20Gi
    Access Modes:    RWX
    Events:
        FirstSeen    LastSeen    Count    From                                SubObjectPath    Type        Reason            Message
        ---------    --------    -----    ----                                -------------    --------    ------            -------
        1m        1m        1    {ibm.io/ibmc-vpc-file 31898035-3011-11e7-a6a4-7a08779efd33 }            Normal        ProvisioningSucceeded    Successfully provisioned volume pvc-0d787071-3a67-11e7-aafc-eef80dd2dea2

    ```
    {: screen}

1. Save the following deployment configuration to file called `deployment.yaml` and reference the PVC that you created in the previous step.

    ```yaml
    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: my-deployment
      labels:
        app: my-deployment
    spec:
      selector:
        matchLabels:
          app: busybox
      template:
        metadata:
          labels:
            app: busybox
        spec:
          containers:
          - name: busybox
            image: busybox:1.28 # The name of the container image that you want to use. 
            command: [ "sh", "-c", "sleep 1h" ]
            volumeMounts:
            - name: my-vol
              mountPath: /data/demo
          volumes:
          - name: my-vol
            persistentVolumeClaim:
              claimName: my-pvc
    ```
    {: codeblock}
    
    `mountPath`
    :   In the container volume mounts section, enter the absolute path of the directory to where the volume is mounted inside the container. Data that is written to the mount path is stored under the `root` directory in your physical {{site.data.keyword.filestorage_vpc_short}} instance. If you want to share a volume between different apps, you can specify [volume sub paths](https://kubernetes.io/docs/concepts/storage/volumes/#using-subpath){: external} for each of your apps.
    
    `volumeMounts.name`
    :   In the container volume mounts section, enter the name of the volume to mount to your pod.
    
    `volume.name`
    :   In the volumes section, enter the name of the volume to mount to your pod. Typically this name is the same as 
    `volumeMounts.name`.
    
    `claimName`
    :   In the volumes persistent volume claim section, enter the name of the PVC that binds the PV that you want to use.

1. Create the deployment.

    ```sh
    oc apply -f deployment.yaml
    ```
    {: pre}

1. Verify that the PV is successfully mounted.

    ```sh
    oc describe deployment my-deployment
    ```
    {: pre}

    The mount point is in the **Volume Mounts** field and the volume is in the **Volumes** field.

    ```sh
    Volume Mounts:
        /var/run/secrets/kubernetes.io/serviceaccount from default-token-tqp61 (ro)
        /volumemount from myvol (rw)
    ...
    Volumes:
    myvol:
        Type:    PersistentVolumeClaim (a reference to a PersistentVolumeClaim in the same namespace)
        ClaimName:    mypvc
        ReadOnly:    false
    ```
    {: screen}


## Attaching existing file storage to an app
{: #vpc-add-file-static}

Create a persistent volume claim (PVC) to statically provision {{site.data.keyword.filestorage_vpc_short}} for your cluster. Static provisioning allows cluster administrators to make existing storage devices available to a cluster. 

Before you can create a persistent volume (PV), you have to retrieve details about your file share.

1. Get the ID for your file share.
    ```sh
    ibmcloud is shares
    ```
    {: pre}

1. Get the details of your share. Make a note of the mount targets.
    ```sh
    ibmcloud is share SHARE-ID
    ```
    {: pre}

1. Get the `nfsServerPath`, also called the `Mount Path`. 
    ```sh
    ibmcloud is share-mount-target SHARE-ID SHARE-TARGET-ID
    ```
    {: pre}

1. Create a PV configuration file called `static-file-share.yaml` that references your file share. 
    ```yaml
    apiVersion: v1
    kind: PersistentVolume
    metadata:
    name: static-file-share
    spec:
    mountOptions:
      - hard
      - nfsvers=4.1
      - sec=sys
    accessModes:
    - ReadWriteMany
    capacity:
      storage: 10Gi
    csi:
      volumeAttributes:
        nfsServerPath:  NFS-SERVER-PATH
      driver: vpc.file.csi.ibm.io
      volumeHandle: FILE-SHARE-ID:SHARE-TARGET-ID
    ```
    {: codeblock}

1. Create the PV.
    ```sh
    oc apply -f static-file-share.yaml
    ```
    {: pre}

1. Create a PVC.
    ```yaml
      apiVersion: v1
      kind: PersistentVolumeClaim
      metadata:
        name: pvc-static
      spec:
        accessModes:
        - ReadWriteMany
        resources:
          requests:
            storage: 10Gi
        storageClassName: "" #Leave the storage class blank.
    ```
    {: codeblock}

1. Create the PVC to bind your PV.
    ```sh
    oc apply -f pvc-static.yaml
    ```
    {: pre}

1. Create a deployment file name `testpod.yaml` to attach your fileshare to the desired application pod. 
    ```yaml
    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: testpod
      labels:
        app: testpod
    spec:
      securityContext:
        fsgroup: 0
      replicas: 1
      selector:
        matchLabels:
          app: testpod
      template:
        metadata:
          labels:
            app: testpod
        spec:
          containers:
          - image: IMAGE
            name: CONTAINER-NAME
            volumeMounts:
            - mountPath: /myvol  
              name: pvc-name 
          volumes:
          - name: pvc-name 
            persistentVolumeClaim:
              claimName: pvc-static # The name of the PVC that you created earlier
    ```
    {: codeblock}

    `spec.containers.image`
    :   The name of the container image that you want to use. To list available images in your {{site.data.keyword.registrylong_notm}} account, run `ibmcloud cr image-list`.
    
    `spec.containers.name`
    :   The name of the container that you want to deploy to your cluster.
    
    `spec.containers.volumeMounts.mountPath`
    :   Enter the absolute path of the directory to where the volume is mounted inside the container. Data that is written to the mount path is stored under the `root` directory in your physical {{site.data.keyword.filestorage_vpc_short}} instance. If you want to share a volume between different apps, you can specify [volume sub paths](https://kubernetes.io/docs/concepts/storage/volumes/#using-subpath){: external} for each of your apps.
    
    `volumeMounts.name`
    :   Enter the name of the volume to mount to your pod.
    
    `volume.name`
    :   Enter the name of the volume to mount to your pod. Typically this name is the same as 
    `volumeMounts.name`.
    
    `volumes.persistentVolumeClaim.claimName`
    :   Enter the name of the PVC that binds the PV that you want to use.

    `securityContext`
    :   Enter the `securityContext` that your app needs, for example `runAsUser` or `runAsGroup` that matches `uid` or `gid` of your file share. Note that `fsGroup: 0` is used in the example to provide root permissions. For more information about security context, see [Configure a Security Context for a Pod or Container](https://kubernetes.io/docs/tasks/configure-pod-container/security-context/){: external}.

1. Create the deployment.
    ```sh
    oc apply -f testpod.yaml
    ```
    {: pre}


## Deploying an app that runs as non-root
{: #vpc-file-non-root-app}

If your app needs to run as non-root, or if your cluster resource group is different than the VPC/Subnet resource group, you must create your own customized storage class. To get started, check out the [customized storage class samples](#storage-file-vpc-custom-sc).


You can run your app as non-root by first creating a custom storage class that contains the group ID (`gid`) or user ID (`uid`) that you want to use.

1. Create a custom storage class and specify the group ID (`gid`) or user ID (`uid`) that you want to use for your app.

    ```yaml
    apiVersion: storage.k8s.io/v1
    kind: StorageClass
    metadata:
        name: ibmc-vpc-file-dp-eni-default
    provisioner: vpc.file.csi.ibm.io
    mountOptions:
        - hard
        - nfsvers=4.1
        - sec=sys
    parameters:
        profile: "dp2"
        iops: "100" # Default IOPS.
        billingType: "hourly" # The default billing policy used.
        encrypted: "false" # By default, all PVC using this class will only be provider managed encrypted.
        gid: "3000" # The default is 0 which runs as root. You can optionally specify a non-root group ID.
        uid: "1000" # The default is 0 which runs as root. You can optionally specify a non-root user ID.
        classVersion: "1"
    reclaimPolicy: "Delete"
    allowVolumeExpansion: true
    ```
    {: codeblock}

1. Save the following code to a file called `my-pvc.yaml`. This code creates a claim that is named `my-pvc` by using the `ibmc-vpc-file-dp2` storage class, billed `monthly`, with a gigabyte size of `10Gi`.

    ```yaml
    apiVersion: v1
    kind: PersistentVolumeClaim
    metadata:
      name: my-pvc # Enter a name for your PVC.
    spec:
      accessModes:
      - ReadWriteMany # The PVC can be mounted by multiple pods. All pods can read from and write to the volume.
      resources:
        requests:
          storage: 10Gi # Enter the size of the storage in gigabytes (Gi). After your storage is provisioned, you can't change the size. Make sure to specify a size that matches the amount of data that you want to store.
      storageClassName: ibmc-vpc-file-dp-eni-default # Enter the name of the storage class that you want to use.
    ```
      {: codeblock}

1. Create the PVC.
    ```sh
    kubectl apply -f my-pvc.yaml
    ```
    {: pre}

1. Create a pod that mounts the PVC.

    ```yaml
    apiVersion: v1
    kind: Pod
    metadata:
      name: security-context-demo
    spec:
      securityContext:
        runAsUser: 1000
        runAsGroup: 3000
      volumes:
      - name: sec-ctx-vol
        emptyDir: {}
      containers:
      - name: sec-ctx-demo
        image: busybox:1.28
        command: [ "sh", "-c", "sleep 1h" ]
        volumeMounts:
        - name: sec-ctx-vol
          mountPath: /data/demo
        securityContext:
          allowPrivilegeEscalation: false
        persistentVolumeClaim:
          claimName: my-pvc # The name of the PVC that you created earlier
    ```
    {: codeblock}



## Creating a custom storage class
{: #storage-file-vpc-custom-sc}

Create your own customized storage class with the preferred settings for your {{site.data.keyword.filestorage_vpc_short}} instance.


1. Review the [Storage class reference](/docs/openshift?topic=openshift-storage-file-vpc-sc-ref) to determine the `profile` that you want to use for your storage class. 

    If you want to use a preinstalled storage class as a template, you can get the details of a storage class by using the `oc get sc STORAGECLASS -o yaml` command.
    {: tip}

2. Create a custom storage class configuration file.

    ```yaml
    apiVersion: storage.k8s.io/v1
    kind: StorageClass
    metadata:
        name: ibmc-vpc-file-dp-eni-default
    provisioner: vpc.file.csi.ibm.io
    mountOptions:
        - hard
        - nfsvers=4.1
        - sec=sys
    parameters:
        profile: "dp2" # The VPC Storage profile used.
        iops: "100" # Default IOPS.
        billingType: "hourly" # The default billing policy used.
        encrypted: "false" # By default, all PVC using this class will only be provider managed encrypted.
        gid: "0" # The default is 0 which runs as root. You can optionally specify a non-root group ID.
        uid: "0" # The default is 0 which runs as root. You can optionally specify a non-root user ID.
        encryptionKey: "" # If encrypted is true, then you must specify the CRN of the encryption key that you want to use from your associated KP/HPCS instance.
        resourceGroup: "" # By default, the cluster resource group is used. If your VPC or subnets are in a different resource group than the cluster, enter the VPC or subnet resource group here.
        region: "" # By default, the region will be populated from the worker node topology.
        zone: "" # By default, the storage vpc driver automatically selects a zone.
        tags: "" # A list of tags "a, b, c" that will be created when the volume is created.
        isENIEnabled: "true" # VPC File Share uses the VNI feature.
        securityGroupIDs: "" # Specify a comma-separated list of security group IDs.
        subnetID: "" # Specify the subnet ID in which the ENI/VNI is created. If not specified, the subnet used are the VPC subnets in the same zone of the cluster.
        zone: "" # By default, the storage VPC driver selects a zone. The user can override this default.
        primaryIPID: "" # Existing ID of reserved IP address from the same subnet as the file share zone. The subnet-id is not mandatory for this field.
        primaryIPAddress: "" # IP address for VNI to be created in the subnet of the zone. The subnetID parameter is also required for this field.
        classVersion: "1"
    reclaimPolicy: "Delete"
    allowVolumeExpansion: true
    ```
    {: codeblock}

3. Create the customized storage class in your cluster.

    ```sh
    oc apply -f custom-storageclass.yaml
    ```
    {: pre}

4. Verify that your storage class is available in the cluster.

    ```sh
    oc get storageclasses
    ```
    {: pre}

    Example output
    
    ```sh
    NAME                                          PROVISIONER
    ibmc-vpc-file-dp-eni-default                  vpc.file.csi.ibm.io
    ```
    {: screen}


## Limiting file share access by worker node, zone, or worker pool
{: #storage-file-vpc-vni-setup}

The default behavior for {{site.data.keyword.filestorage_vpc_short}} cluster add-on is that pods on a given node can access file shares.

In versions 1.2 of and later of the {{site.data.keyword.filestorage_vpc_short}} cluster add-on, you can control more granularly how pods access your file shares. For example, you might limit file share access to only pods on a specific node, in a specific zone, on a specific worker pool, or in a specific subnet. Review the following scenarios for how you can configure pod access to your file shares.

If you use VNI to limit pod access to your file shares, you will not have high availability as file share access and in case a subnet is down where the VNI is created, you will not have access to your file share which also impacts reading and writing to the file share.

### Prerequisites
{: #storage-file-vpc-vni-prereqs}

1. List your clusters and make a note of the cluster ID where you want to deploy file storage.
    ```sh
    ibmcloud ks cluster ls
    ```
    {: pre}

1. List your security groups and make a note of the ID `kube-cluster-ID` security for your cluster.
    ```sh
    ibmcloud is sg 
    ```
    {: pre}

    Example output
    ```sh
    ID                                          Name                                             Rules   Targets   VPC       Resource group
    r006-4aaec88f-4986-4b7c-a737-401f7fef1555   kube-cluster-ID                       15      0         my-vpc   default
    ```
    {: pre}

1. Create a custom security group in the same VPC as your cluster. This security group is used to control access to your file shares.

    ```sh
    ibmcloud is security-group-create my-custom-security-group VPC-ID
    ```
    {: pre}

1. [Create a custom storage class](#storage-file-vpc-custom-sc) and enter your custom security group ID. This security group is used for all PVCs (file shares) created from this custom storage class.

1. Create a PVC that uses your custom storage class.
    ```yaml
      apiVersion: v1
      kind: PersistentVolumeClaim
      metadata:
        name: pvc-custom-vni
      spec:
        accessModes:
        - ReadWriteMany
        resources:
          requests:
            storage: 10Gi
        storageClassName: "" # For example: my-custom-storage-class
    ```
    {: codeblock}

1. After the PV is bound to the PVC, get the PV details and make a note of the `nfsServerPath` value to find the VNI IP address.
    ```sh
    kubectl get pv pvc-XXXX -o yaml | grep nfsServerPath
    ```
    {: pre}

    Example output.
    ```yaml
    nfsServerPath: XXX.XX.XX.XXX:/XX # VNI IP address
    ```
    {: screen}

### Limiting file share access to pods on one worker node
{: #storage-file-vpc-vni-one-worker}

1. Add the following rule to the custom security group you created earlier.

    ```sh
    ibmcloud is sg-rulec CUSTOM-SG inbound tcp --port-min 111 --port-max 2049 --remote WORKER-IP
    ```
    {: pre}

1. Add the following rule to the `kube-cluster-ID` security group.
    ```sh
    ibmcloud is sg-rulec kube-<cluster-id> outbound tcp --port-min 111 --port-max 2049 --remote 10.240.0.10 # VNI IP
    ```

1. Create a deployment that uses your PVC. Only pods that are deployed on the worker node that matches the rule that you created are able to mount or use the PVC. Pods deployed on other nodes are stuck in the container `creating` state. 
 

### Limiting file share access to pods on worker nodes in a single zone
{: #storage-file-vpc-vni-one-zone}

1. Add the following rule to the custom security group you created earlier.

    ```sh
    ibmcloud is sg-rulec CUSTOM-SG inbound tcp --port-min 111 --port-max 2049 --remote 10.240.0.0/24 # zone subnet cidr range
    ```
    {: pre}

1. Add the following rule to the `kube-cluster-ID` security group.
    ```sh
    ibmcloud is sg-rulec kube-<cluster-ID> outbound tcp --port-min 111 --port-max 2049 --remote 10.240.1.7 # VNI IP
    ```


1. Create a deployment that uses your PVC. Only pods deployed in the zone that is listed in the previous rule can mount the PVC. Pods that are deployed in other zones cannot access the PVC and are stuck in the Container `creating` state.



### Limiting file share access to pods on worker nodes in a single worker pool
{: #storage-file-vpc-vni-one-pool}

1. Add the following rules to your custom security group.

    ```sh
    ibmcloud is sg-rulec CUSTOM-SG inbound tcp --port-min 111 --port-max 2049 --remote 10.240.0.0/24 # zone 1 subnet cidr range
    ibmcloud is sg-rulec CUSTOM-SG inbound tcp --port-min 111 --port-max 2049 --remote 10.240.1.0/24 # zone 2 subnet cidr range
    ```
    {: pre}

1. Add the following rule to the `kube-cluster-ID` security group.

    ```sh
    ibmcloud is sg-rulec kube-<cluster-ID> outbound tcp --port-min 111 --port-max 2049 --remote 10.240.1.7 # VNI IP
    ```
    {: pre}

1. Deploy an app that uses the PVC you created earlier. Only pods that are deployed on the worker pools indicated in the previous rule can mount the PVC. Or, if you deploy your app in a daemonset, pods will only successfully deploy on worker nodes that you created security group rules for. Pods on worker pools that are not in the specified worker pool will fail with a `MountVolume.SetUp failed for volume "pvc-184b8c92-33ea-4874-b2ac-17665e53c060" : rpc error: code = DeadlineExceeded desc = context deadline exceeded` error.


### Limiting file share access to pods on worker nodes in multiple worker pools
{: #storage-file-vpc-vni-multiple-pools}

1. Add the following rules to your custom SG.

    ```sh
    ibmcloud is sg-rulec CUSTOM-SG inbound tcp --port-min 111 --port-max 2049 --remote 10.240.1.0/24 # worker pool 1, zone 1 subnet CIDR range
    ibmcloud is sg-rulec CUSTOM-SG inbound tcp --port-min 111 --port-max 2049 --remote 10.240.1.0/24 # worker pool 1, zone 2 subnet CIDR range
    ibmcloud is sg-rulec CUSTOM-SG inbound tcp --port-min 111 --port-max 2049 --remote 10.241.0.0/24 # worker pool 2, zone 1 subnet CIDR ange
    ibmcloud is sg-rulec CUSTOM-SG inbound tcp --port-min 111 --port-max 2049 --remote 10.241.1.0/24 # worker pool 2, zone 2subnet CIDR ange
    ibmcloud is sg-rulec CUSTOM-SG outbound tcp --port-min 111 --port-max 2049 --remote 10.240.1.7 # VNI-IP
    ```
    {: pre}

1. Add the following rule to the `kube-cluster-ID` security group.

    ```sh
    ibmcloud is sg-rulec kube-<cluster-ID> outbound tcp --port-min 111 --port-max 2049 --remote 10.240.1.7 # VNI IP
    ```
    {: pre}

1. Create a deployment that uses your PVC. Only pods deployed in the zone indicated in the rule can mount the PVC. Pods deployed on the restricted worker nodes are stuck in the Container `creating` state.



