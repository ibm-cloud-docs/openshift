---

copyright: 
  years: 2022, 2024
lastupdated: "2024-06-21"

keywords: kubernetes, openshift

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}


# Adding {{site.data.keyword.filestorage_vpc_short}} to apps
{: #storage-file-vpc-apps}

{{site.data.keyword.containerlong}} provides pre-defined storage classes that you can use to provision {{site.data.keyword.filestorage_vpc_short}}. Each storage class specifies the type of {{site.data.keyword.filestorage_vpc_short}} that you provision, including available size, IOPS, file system, and the retention policy. You can also create your own storage classes depending on your use case.
{: shortdesc}

The {{site.data.keyword.filestorage_vpc_short}} cluster add-on is available in Beta. 
{: beta} 

After you provision a specific type of storage by using a storage class, you can't change the type, or retention policy for the storage device. However, you can [change the size](/docs/openshift?topic=openshift-storage-file-vpc-apps#storage-file-vpc-expansion) and the [IOPS](/docs/vpc?topic=vpc-adjusting-share-iops&interface=ui) if you want to increase your storage capacity and performance. To change the type and retention policy for your storage, you must create a new storage instance and copy the data from the old storage instance to your new one.

Decide on a storage class. For more information, see the [storage class reference](/docs/openshift?topic=openshift-storage-file-vpc-sc-ref).

Review the following notes and considerations for {{site.data.keyword.filestorage_vpc_short}}.

- By default, {{site.data.keyword.filestorage_vpc_short}} cluster add-on provisions file shares in the `kube-<clusterID>` security group. This means pods can access file shares across nodes and zones.
- If you need the following features, you must [create your own storage class](/docs/openshift?topic=openshift-storage-file-vpc-apps#storage-file-vpc-custom-sc).
    - Your app needs to run as non-root.
    - Your cluster is in a different resource group from your VPC and subnet.
    - You need to limit file share access to pods on a given node or in a given zone.
    - You need to bring your own (BYOK) encryption using a KMS provider such as HPCS or Key Protect.
    - You need to manually specify the subnet or IP address of the [Virtual Network Interface (VNI)](/docs/vpc?topic=vpc-file-storage-vpc-about&interface=ui#fs-mount-granular-auth).



New security group rules have been introduced in versions 4.11 and later. These rule changes mean you must sync your security groups before you can use {{site.data.keyword.filestorage_vpc_short}}.
{: important}

If your cluster was initially created at version 4.11 or earlier, run the following commands to sync your security group settings.

1. Get the ID of the `kube-<clusterID>` security group.
    ```sh
    ibmcloud is sg kube-<cluster-id>  | grep ID
    ```
    {: pre}

1. Sync your security group settings.
    ```sh
    ibmcloud ks security-group sync -c <cluster ID> --security-group <ID>
    ```
    {: pre}


## Quick start for {{site.data.keyword.filestorage_vpc_short}}
{: #vpc-add-file-dynamic}

Create a persistent volume claim (PVC) to dynamically provision {{site.data.keyword.filestorage_vpc_short}} for your cluster. Dynamic provisioning automatically creates the matching persistent volume (PV) and orders the file share in your account.

1. [Access your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-access_cluster).

1. Review the pre-installed storage classes by running the following command. For more information, see the [storage class reference](/docs/openshift?topic=openshift-storage-file-vpc-sc-ref).
    ```shell
    oc get sc | grep vpc-file
    ```
    {: pre}

1. Save the following YAML to a file. This example creates a claim that is named `my-pvc` by using the `ibmc-vpc-file-min-iops` storage class with a gigabyte size of `10Gi`.

    ```yaml
    apiVersion: v1
    kind: PersistentVolumeClaim
    metadata:
      name: my-pvc # Enter a name for your PVC.
    spec:
      accessModes:
      - ReadWriteMany # The file share can be mounted on multiple nodes and pods.
      resources:
        requests:
          storage: 20Gi # Enter the size of the storage in gigabytes (Gi).
      storageClassName: ibmc-vpc-file-min-iops # Enter the name of the storage class that you want to use.
    ```
    {: codeblock}

1. Create the PVC.

    ```sh
    oc apply -f my-pvc.yaml
    ```
    {: pre}

1. Verify that your PVC is created and bound to the PV.

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
            image: busybox:1.28
            command: [ "sh", "-c", "sleep 1h" ]
            volumeMounts:
            - name: my-vol
              mountPath: /data/demo # Mount path for the application.
          volumes:
          - name: my-vol
            persistentVolumeClaim:
              claimName: my-pvc # Your PVC name.
    ```
    {: codeblock}
    
    `volumeMounts.mountPath`
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
    Containers:
      Mounts:
        /data/demo from my-vol (rw)
    Volumes:
    my-vol:
      Type:       PersistentVolumeClaim (a reference to a PersistentVolumeClaim in the same namespace)
      ClaimName:  my-pvc
      ReadOnly:   false
    ```
    {: screen}


1. **Optional**: After your pod is running, try [expanding your storage volume](#storage-file-vpc-expansion).


## Expanding a mounted volume
{: #storage-file-vpc-expansion}

To provision volumes that support expansion, you must use storage class that has `allowVolumeExpansion` set to `true`.

The {{site.data.keyword.filestorage_vpc_short}} cluster add-on supports expansion in both online and offline modes. However, expansion is only possible within the given [size and IOPs range of the {{site.data.keyword.filestorage_vpc_short}} profile](/docs/vpc?topic=vpc-file-storage-profiles&interface=ui#dp2-profile).
{: note}

1. Begin by deploying the [quick start example PVC and Deployment](#vpc-add-file-dynamic). 

1. After your PVC is mounted by an app pod, you can expand your volume by editing the value of the `spec.resources.requests.storage` field in your PVC. To expand your volume, edit your PVC and increase the value in the `spec.resources.requests.storage` field.

    ```sh
    kubectl edit pvc my-pvc
    ```
    {: pre}

    ```yaml
    spec:
      accessModes:
      - ReadWriteMany
      resources:
        requests:
          storage: 50Gi
    ```
    {: codeblock}

1. Save and close the PVC. Wait a few minutes for the volume to be expanded.

1. Verify that your volume is expanded.
    ```sh
    kubectl get pvc
    ```
    {: pre}

    Example output

    ```sh
    NAME     STATUS   VOLUME                                     CAPACITY   ACCESS MODES   STORAGECLASS        AGE
    my-pvc   Bound    pvc-25b6912e-75bf-41ca-b6b2-567fa4f9d245   50Gi       RWX            ibmc-vpc-file-min-iops   3m31s
    ```
    {: screen}


## Attaching existing file storage to an app
{: #vpc-add-file-static}

Create a persistent volume claim (PVC) to statically provision {{site.data.keyword.filestorage_vpc_short}} for your cluster. Static provisioning allows cluster administrators to make existing storage devices available to a cluster. 

1. Create a file share and target. For more information, see [Creating file shares and mount targets](/docs/vpc?topic=vpc-file-storage-create&interface=cli).

1. Before you can create a persistent volume (PV), retrieve the details about your file share.
    ```sh
    ibmcloud is shares
    ```
    {: pre}

1. Get the details of your share. Make a note of the mount targets.
    ```sh
    ibmcloud is share SHARE-ID
    ```
    {: pre}

    Example command.

    ```sh
    ibmcloud is share r134-bad98878-1f63-45d2-a3fd-60447094c2e6
    ```
    {: pre}

    Example output.

    ```sh
    ID                           r134-bad98878-1f63-45d2-a3fd-60447094c2e6   
    Name                         pvc-e7e005a9-e96b-41ad-9d6e-74650a9110a0   
    CRN                          crn:v1:staging:public:is:us-south-1:a/77f2bceddaeb577dcaddb4073fe82c1c::share:r134-bad98878-1f63-45d2-a3fd-60447094c2e6   
    Lifecycle state              stable   
    Access control mode          security_group   
    Zone                         us-south-1   
    Profile                      dp2   
    Size(GB)                     10   
    IOPS                         100   
    User Tags                    clusterid:cpjao3l20dl78jadqkd0,namespace:default,provisioner:vpc.file.csi.ibm.io,pv:pvc-e7e005a9-e96b-41ad-9d6e-74650a9110a0,pvc:pv-file,reclaimpolicy:delete,storageclass:custom-eni   
    Encryption                   provider_managed   
    Mount Targets                ID                                          Name      
                                r134-aa2aabb8-f616-47be-886b-99220852b728   pvc-e7e005a9-e96b-41ad-9d6e-74650a9110a0      
                                    
    Resource group               ID                                 Name      
                                300b9469ee8676f9a038ecdf408c1a9d   Default      
                                    
    Created                      2024-06-11T19:55:11+05:30   
    Replication role             none   
    Replication status           none   
    Replication status reasons   Status code   Status message      
    ```
    {: screen}

1. Get the `nfsServerPath`, also called the `Mount Path`. 
    ```sh
    ibmcloud is share-mount-target SHARE-ID SHARE-TARGET-ID
    ```
    {: pre}

    Example command.
    ```sh
    ibmcloud is share-mount-target  r134-bad98878-1f63-45d2-a3fd-60447094c2e6 r134-aa2aabb8-f616-47be-886b-99220852b728
    ```
    {: pre}

    Example output

    ```sh
    ID                          r134-aa2aabb8-f616-47be-886b-99220852b728   
    Name                        pvc-e7e005a9-e96b-41ad-9d6e-74650a9110a0   
    VPC                         ID                                          Name      
                                r134-f05922d4-d8ab-4f64-9a3d-82664b303bc1   vpc-public      
                                  
    Access control mode         security_group   
    Resource type               share_mount_target   
    Virtual network interface   ID                                          Name      
                                0716-6407fb4b-e962-49c4-8556-dc94f4574b4b   defective-chloride-huffy-gladly      
                                  
    Lifecycle state             stable   
    Mount path                  10.240.0.23:/89d8a454_f552_42bf_8374_4d31481edf4d   
    Transit Encryption          none   
    Created                     2024-06-11T19:55:12+05:30
    ```
    {: screen}

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
          nfsServerPath: NFS-SERVER-PATH
        driver: vpc.file.csi.ibm.io
        volumeHandle: FILE-SHARE-ID#SHARE-TARGET-ID
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

1. Create the deployment.
    ```sh
    oc apply -f testpod.yaml
    ```
    {: pre}

## Creating your own storage class
{: #storage-file-vpc-custom-sc}

Create your own customized storage class with the preferred settings for your {{site.data.keyword.filestorage_vpc_short}} instance. The following example uses the `dp2` [profile](https://cloud.ibm.com/docs/vpc?topic=vpc-file-storage-profiles&interface=ui#dp2-profile).


1. Create a storage class configuration file.

    ```yaml
    apiVersion: storage.k8s.io/v1
    kind: StorageClass
    metadata:
      name: ibmc-vpc-file-custom-sc
      labels:
        app.kubernetes.io/name: ibm-vpc-file-csi-driver
      annotations:
        version: v2.0
    provisioner: vpc.file.csi.ibm.io
    mountOptions:
      - hard
      - nfsvers=4.1
      - sec=sys
    parameters:
        profile: "dp2"
        billingType: "hourly" # hourly or monthly
        encrypted: "false"
        encryptionKey: "" # If encrypted is true, then a user must specify the CRK-CRN.
        resourceGroup: "" # By default resource group will be used from storage-secrete-store secret, User can override.
        isENIEnabled: "true" # VPC File Share VNI feature will be used by all PVCs created with this storage class.
        securityGroupIDs: "" # By default cluster security group i.e kube-<clusterID> will be used. User can provide their own comma separated SGs.
        subnetID: "" # User can provide subnetID in which the VNI will be created. Zone and region are mandatory for this. If not provided CSI driver will use the subnetID available in the cluster's VPC zone.
        region: "" # VPC CSI driver will select a region from cluster node's topology. The user can override this default.
        zone: "" # VPC CSI driver will select a region from cluster node's topology. The user can override this default.
        primaryIPID: "" # Existing ID of reserved IP from the same subnet as the file share zone. Zone and region are mandatory for this. SubnetID is not mandatory for this.
        primaryIPAddress: "" # IPAddress for VNI to be created in the respective subnet of the zone. Zone, region and subnetID are mandatory for this.
        tags: "" # User can add a list of tags "a, b, c" that will be used at the time of provisioning file share, by default CSI driver has its own tags.
        uid: "0" # The initial user identifier for the file share, by default its root.
        gid: "0" # The initial group identifier for the file share, by default its root.
        classVersion: "1"
    reclaimPolicy: "Delete"
    allowVolumeExpansion: true
    ```
    {: codeblock}

1. Create the customized storage class in your cluster.

    ```sh
    oc apply -f custom-storageclass.yaml
    ```
    {: pre}

1. Verify that your storage class is available in the cluster.

    ```sh
    oc get sc
    ```
    {: pre}

    Example output
    
    ```sh
    ibmc-vpc-file-custom-sc                       vpc.file.csi.ibm.io
    ```
    {: screen}




## Deploying an app that runs as non-root
{: #vpc-file-non-root-app}

1. Create your own storage class and specify the group ID or user ID that you want to use for your app.

    ```yaml
    apiVersion: storage.k8s.io/v1
    kind: StorageClass
    metadata:
      name: ibmc-vpc-file-custom-sc
      labels:
        app.kubernetes.io/name: ibm-vpc-file-csi-driver
      annotations:
        version: v2.0
    provisioner: vpc.file.csi.ibm.io
    mountOptions:
      - hard
      - nfsvers=4.1
      - sec=sys
    parameters:
        profile: "dp2"
        iops: "100"
        billingType: "hourly" # hourly or monthly
        encrypted: "false"
        uid: "3000" # The initial user identifier for the file share.
        gid: "1000" # The initial group identifier for the file share.
        classVersion: "1"
    reclaimPolicy: "Delete"
    allowVolumeExpansion: true
    ```
    {: codeblock}



1. Save the following YAML to a file called `my-pvc.yaml`.

    ```yaml
    apiVersion: v1
    kind: PersistentVolumeClaim
    metadata:
      name: my-pvc
    spec:
      accessModes:
      - ReadWriteMany
      resources:
        requests:
          storage: 10Gi
      storageClassName: ibmc-vpc-file-custom-sc
    ```
    {: codeblock}



1. Create the PVC.

    ```sh
    oc apply -f my-pvc.yaml
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
          claimName: my-pvc
    ``` 
    {: codeblock}

1. Verify the pod is running.
    ```sh
    oc get pods
    ```
    {: pre}




## Limiting file share access by worker pool, zone, or worker node
{: #storage-file-vpc-vni-setup}

The default behavior for {{site.data.keyword.filestorage_vpc_short}} cluster add-on is that pods on any node can access file shares. You can also apply more granular control over how pods access your file shares. For example, you might limit file share access to only pods on a specific node, in a specific zone, on a specific worker pool. Review the following scenarios for how you can configure pod access to your file shares.

If you use the following VNI features to limit pod access to your file shares, your app might not be highly available.

### Prerequisites
{: #storage-file-vpc-vni-prereqs}

To limit file share access by node, zone, or resource group, you must first create a custom VPC security group.

1. List your clusters and make a note of the cluster ID where you want to deploy file storage.
    ```sh
    ibmcloud ks cluster ls
    ```
    {: pre}

1. List your security groups and make a note of the ID `kube-<clusterID>` security group for your cluster. You need the security group ID later when adding security group rules.
    ```sh
    ibmcloud is sg 
    ```
    {: pre}

    Example output
    ```sh
    ID                                          Name                                             Rules   Targets   VPC       Resource group
    r006-4aaec88f-4986-4b7c-a737-401f7fef1555   kube-clusterID                       15      0         my-vpc   default
    ```
    {: pre}

1. Create a custom security group in the same VPC as your cluster. Your can use this security group to control access to your file shares by adding security group rules. 

    ```shell
    ibmcloud is security-group-create my-custom-security-group VPC-ID
    ```
    {: pre}

1. [Create your own storage class](#storage-file-vpc-custom-sc) and enter the ID of the custom security group you created earlier. All PVCs created from this storage class are in your custom security group.

1. Create a PVC that uses your own storage class.
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

1. After the PV binds to the PVC, get the PV details and make a note of the `nfsServerPath` value to find the VNI IP address.
    ```sh
    kubectl get pv pvc-XXXX -o yaml | grep nfsServerPath
    ```
    {: pre}

    Example output.

    ```sh
    nfsServerPath: XXX.XX.XX.XXX:/XX # VNI IP address
    ```
    {: screen}

### Limiting file share access to pods on one worker node
{: #storage-file-vpc-vni-one-worker}

1. Make sure you have [completed the prerequisites](#storage-file-vpc-vni-prereqs).

1. Add the following rule to the custom security group you created earlier.

    ```sh
    ibmcloud is sg-rulec CUSTOM-SG inbound tcp --port-min 111 --port-max 2049 --remote WORKER-IP
    ```
    {: pre}

1. Add the following rule to the `kube-clusterID` security group.
    ```sh
    ibmcloud is sg-rulec kube-<cluster-id> outbound tcp --port-min 111 --port-max 2049 --remote 10.240.0.10 # VNI IP
    ```
    {: pre}

1. Create a deployment that uses your PVC. Only pods that are deployed on the worker node that matches the rule that you created are able to mount or use the PVC. Pods deployed on other nodes are stuck in the container `creating` state. 
 

### Limiting file share access to pods on worker nodes in a single zone
{: #storage-file-vpc-vni-one-zone}

1. Make sure you have [completed the prerequisites](#storage-file-vpc-vni-prereqs).

1. Add the following rule to the custom security group you created earlier.

    ```sh
    ibmcloud is sg-rulec CUSTOM-SG inbound tcp --port-min 111 --port-max 2049 --remote 10.240.0.0/24 # zone subnet cidr range
    ```
    {: pre}

1. Add the following rule to the `kube-clusterID` security group. Specify the IP address of the virtual network interface (VNI).
    ```sh
    ibmcloud is sg-rulec kube-<cluster-ID> outbound tcp --port-min 111 --port-max 2049 --remote VNI-IP
    ```
    {: pre}


1. Create a deployment that uses your PVC. Only pods deployed in the zone that is listed in the previous rule can mount the PVC. Pods that are deployed in other zones cannot access the PVC and are stuck in the Container `creating` state.


### Limiting file share access to pods on worker nodes in a single worker pool
{: #storage-file-vpc-vni-one-pool}

1. Make sure you have [completed the prerequisites](#storage-file-vpc-vni-prereqs).

1. Create inbound rules for each subnet range

    ```sh
    ibmcloud is sg-rulec CUSTOM-SG inbound tcp --port-min 111 --port-max 2049 --remote 10.240.0.0/24 # zone 1 subnet cidr range
    ibmcloud is sg-rulec CUSTOM-SG inbound tcp --port-min 111 --port-max 2049 --remote 10.240.1.0/24 # zone 2 subnet cidr range
    ```
    {: pre}

1. Add the following rule to the `kube-clusterID` security group. Specify the IP address of the virtual network interface (VNI) as the remote or source.

    ```sh
    ibmcloud is sg-rulec kube-<cluster-ID> outbound tcp --port-min 111 --port-max 2049 --remote VNI-IP
    ```
    {: pre}

1. Deploy an app that uses the PVC you created earlier. Only pods on the worker pools indicated in the earlier rule can mount the PVC. Or, if you deploy your app in a daemonset, pods will only successfully deploy on worker nodes that you created security group rules for. Pods on worker pools that aren't in the specified worker pool fail with a `MountVolume.SetUp failed for volume "pvc-184b8c92-33ea-4874-b2ac-17665e53c060" : rpc error: code = DeadlineExceeded desc = context deadline exceeded` error.


### Limiting file share access to pods on worker nodes in multiple worker pools
{: #storage-file-vpc-vni-multiple-pools}

1. Make sure you have [completed the prerequisites](#storage-file-vpc-vni-prereqs).

1. Add the following rules to your custom security group. Specify the worker pools and the subnet CIDR ranges as the remote or source.

    ```sh
    ibmcloud is sg-rulec CUSTOM-SG inbound tcp --port-min 111 --port-max 2049 --remote 10.240.1.0/24 # worker pool 1, zone 1 subnet CIDR range
    ibmcloud is sg-rulec CUSTOM-SG inbound tcp --port-min 111 --port-max 2049 --remote 10.240.1.0/24 # worker pool 1, zone 2 subnet CIDR range
    ibmcloud is sg-rulec CUSTOM-SG inbound tcp --port-min 111 --port-max 2049 --remote 10.241.0.0/24 # worker pool 2, zone 1 subnet CIDR range
    ibmcloud is sg-rulec CUSTOM-SG inbound tcp --port-min 111 --port-max 2049 --remote 10.241.1.0/24 # worker pool 2, zone 2subnet CIDR range
    ibmcloud is sg-rulec CUSTOM-SG outbound tcp --port-min 111 --port-max 2049 --remote 10.240.1.7 # VNI-IP
    ```
    {: pre}

1. Add the following rule to the `kube-<clusterID>` security group. Specify the IP address of the virtual network interface (VNI) as the remote or source.

    ```sh
    ibmcloud is sg-rulec kube-<clusterID> outbound tcp --port-min 111 --port-max 2049 --remote 10.240.1.7 # VNI-IP
    ```
    {: pre}

1. Create a deployment that uses your PVC. Only pods deployed in the zone indicated in the rule can mount the PVC. Pods deployed on the restricted worker nodes are stuck in the Container `creating` state.



