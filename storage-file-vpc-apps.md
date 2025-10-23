---

copyright: 
  years: 2022, 2025
lastupdated: "2025-10-22"

keywords: kubernetes, openshift

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}


# Adding {{site.data.keyword.filestorage_vpc_short}} to apps
{: #storage-file-vpc-apps}

{{site.data.keyword.openshiftlong_notm}} provides pre-defined storage classes that you can use to provision {{site.data.keyword.filestorage_vpc_short}}. Each storage class specifies the type of {{site.data.keyword.filestorage_vpc_short}} that you provision, including available size, IOPS, file system, and the retention policy. You can also create your own storage classes depending on your use case.
{: shortdesc}

Review the following notes and considerations before continuing.


-  After you provision a specific type of storage by using a storage class, you can't change the type, or retention policy for the storage device. However, you can [change the size](/docs/openshift?topic=openshift-storage-file-vpc-apps#storage-file-vpc-expansion) and the [IOPS](/docs/vpc?topic=vpc-file-storage-adjusting-iops&interface=ui) if you want to increase your storage capacity and performance. To change the type and retention policy for your storage, you must create a new storage instance and copy the data from the old storage instance to your new one.
- If your cluster and VPC are in separate resource groups, then before you can provision file shares, you must create your own storage class and provide your VPC resource group ID under the `resourceGroup` section along with the `kube-<clusterID>` security group ID under `securityGroupIDs` section. To retrieve security group ID do the following. For more information, see [Creating your own storage class](/docs/openshift?topic=openshift-storage-file-vpc-apps#storage-file-vpc-custom-sc).
- New security group rules were introduced in cluster versions 4.11 and later. These rule changes mean that you must sync your security groups before you can use {{site.data.keyword.filestorage_vpc_short}}. For more information, see [Adding {{site.data.keyword.filestorage_vpc_short}} to apps](/docs/containers?topic=containers-storage-file-vpc-apps).
- New storage classes were added with version 2.0 of the add-on. You can no longer provision new file shares that use the older storage classes. Existing volumes that use the older storage classes continue to function, however you cannot expand the volumes that were created using the older classes. For more information, see the [Migrating to a new storage class](/docs/openshift?topic=openshift-storage-file-vpc-apps#storage-file-expansion-migration).
- Creating a PVC by using [StorageClassSecrets](https://kubernetes-csi.github.io/docs/secrets-and-credentials-storage-class.html){: external} is not supported.
- Make sure the user who creates the cluster has the Reader, Writer, and Operator permissions for VPC Infrastructure Services.
- Make sure you [set up a service authorization](/docs/vpc?topic=vpc-file-s2s-auth&interface=ui) from VPC Infrastructure to KMS/HPCS if you plan to use encryption on your file shares.
- By default, {{site.data.keyword.filestorage_vpc_short}} cluster add-on provisions file shares in the `kube-<clusterID>` security group. This means pods can access file shares across nodes and zones.
- If you are using context-based restrictions, make sure you configure your network zones and rules. For more information, see [Protecting Virtual Private Cloud (VPC) Infrastructure Services with context-based restrictions](/docs/vpc?topic=vpc-cbr&interface=ui).


New security group rules were introduced in versions 4.11 and later. These rule changes mean you must sync your security groups before you can use {{site.data.keyword.filestorage_vpc_short}}. If your cluster was initially created at version 4.11 or earlier, run the following commands to sync your security group settings.
{: important}


1. Get the ID of your cluster.
    ```sh
    ibmcloud oc cluster ls
    ```
    {: pre}

1. Get the ID of the `kube-<clusterID>` security group.
    ```sh
    ibmcloud is sg kube-<cluster-id>  | grep ID
    ```
    {: pre}

1. Sync the `kube-<clusterID>` security group by using the ID that you retrieved in the previous step.
    ```sh
    ibmcloud ks security-group sync -c <cluster ID> --security-group <ID>
    ```
    {: pre}


## Quick start for {{site.data.keyword.filestorage_vpc_short}}
{: #vpc-add-file-dynamic}

Create a persistent volume claim (PVC) to dynamically provision {{site.data.keyword.filestorage_vpc_short}} for your cluster. Dynamic provisioning automatically creates the matching persistent volume (PV) and orders the file share in your account.

1. [Access your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-access_cluster).

1. Review the pre-installed storage classes by running the following command. For more information, see the [storage class reference](/docs/openshift?topic=openshift-storage-file-vpc-sc-ref).
    ```sh
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

## Migrating to a new storage class
{: #storage-file-expansion-migration}

- New storage classes were added with version 2.0 of the add-on.
- You can no longer provision new file shares that use the older storage classes.
- Existing volumes that use the older storage classes continue to function, however you cannot expand the volumes that were created using the older classes.
- If you need the volume expansion feature, complete the following steps to migrate your apps to a newer storage class.
- If you don't need the volume expansion feature, you do not need to migrate and your PVCs continue to function as normal.
- The following steps cover manual migration.


1. Find the PVC you want to migrate and make a note of the both the PVC name and the associated PV name.
    ```sh
    oc get pvc
    ```
    {: pre}

1. Scale down your app that is using the PVC.

    ```sh
    oc scale deployment DEPLOYMENT --replicas 0
    ```
    {: pre}

2. Edit the PV object that your app is using to change reclaim policy to `Retain` and storage class to `ibmc-vpc-file-min-iops`. 

    ```sh
    kubectl edit pv PV
    ```
    {: pre}

    ```yaml
    spec:
      accessModes:
      - ReadWriteMany
      capacity:
        storage: 20Gi
      claimRef:
        apiVersion: v1
        kind: PersistentVolumeClaim
        name: <pvc-name>
        namespace: default
        ...
      persistentVolumeReclaimPolicy: Retain # Change delete to retain
      storageClassName: ibmc-vpc-file-min-iops # Enter a new storage class
      volumeMode: Filesystem
    ```
    {: codeblock}

3. Delete the existing PVC object.
    ```sh
    kubectl delete pvc PVC
    ```
    {: pre}

4. Edit the PV again and remove the `claimRef` section.

    ```sh
    kubectl edit pv PV
    ```
    {: pre}

    ```yaml
    spec:
      accessModes:
      - ReadWriteMany
      capacity:
        storage: 20Gi
      #claimRef:
        #apiVersion: v1
        #kind: PersistentVolumeClaim
        #name: <pvc-name>
        #namespace: default
        #resourceVersion: "381270"
        #uid: 4042f319-1233-4187-8549-8249a840a8dd
    ```
    {: codeblock}

5. Create a PVC that has the same name and same size as your previous PVC. This should be done one by one for all affected PVCs.

    ```sh
    apiVersion: v1
    kind: PersistentVolumeClaim
    metadata:
      name: <pvc-name>
    spec:
      accessModes:
      - ReadWriteMany
      resources:
        requests:
          storage: <size>Gi
      storageClassName: ibmc-vpc-file-min-iops
    ```
    {: codeblock}

6. Scale up your app which was using the PVC.

    ```sh
    k scale deployment DEPLOYMENT --replicas x
    ```
    {: pre}

7. To continue using volume expansion, see [Setting up volume expansion](#storage-file-vpc-expansion).



## Setting up volume expansion
{: #storage-file-vpc-expansion}

To provision volumes that support expansion, you must use storage class that has `allowVolumeExpansion` set to `true`.

The {{site.data.keyword.filestorage_vpc_short}} cluster add-on supports expansion in both online and offline modes. However, expansion is only possible within the given [size and IOPs range of the {{site.data.keyword.filestorage_vpc_short}} profile](/docs/vpc?topic=vpc-file-storage-profiles&interface=ui#dp2-profile).
{: note}

New storage classes were introduced with version 2.0. Volume expansion does not work for shares that use the storage classes from earlier versions of the add-on.
{: note}

### Before you begin
{: #before-vpc-file-expansion}

* To use volume expansion, make sure you [update your add-on to at least version 2.0](/docs/openshift?topic=openshift-storage-file-vpc-managing).

* Make sure your app is using one of the [latest storage classes](/docs/openshift?topic=openshift-storage-file-vpc-sc-ref). For migration steps, see [Migrating to a new storage class](#storage-file-expansion-migration)

* If you don't have a running app, begin by deploying the [quick start example PVC and Deployment](#vpc-add-file-dynamic). 

### Expanding a mounted volume
{: #vpc-file-volume-expansion}

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

1. Get your cluster ID.
    ```sh
    ibmcloud ks cluster ls
    ```
    {: pre}

1. Get the ID of your `kube-<clusterID>` security group.
    ```sh
    ibmcloud is sg kube-<cluster-id>  | grep ID
    ```
    {: pre}

1. Create a file share. For more information, see [Creating file shares and mount targets](/docs/vpc?topic=vpc-file-storage-create&interface=cli).

    ```sh
    ibmcloud is share-create --name my-file-share --zone us-south-2 --profile dp2 --size 1000 --iops 1000
    ```
    {: pre}

1. Create a share mount target and specify the `kube-<clusterID>` security group ID that you retrieved earlier in the `--vni-sgs` option.

    ```sh
    ibmcloud is share-mount-target-create my-file-share --subnet my-subnet --name NAME --vni-name my-share-vni-1  --vni-sgs kube-<cluster-id> --resource-group-name Default --vpc ID
    ```
    {: pre}

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

    Example output

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

1. Create a deployment file name `testpod.yaml` to attach your fileshare to an application pod.

    ```yaml
    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: testpod
      labels:
        app: testpod
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
          - name: pvc-name 
            persistentVolumeClaim:
              claimName: pvc-static # The name of the PVC that you created earlier
    ```
    {: codeblock}
    
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

You can create your own customized storage class with the preferred settings for your {{site.data.keyword.filestorage_vpc_short}} instance. 

If you need the following features, you must [create your own storage class](/docs/openshift?topic=openshift-storage-file-vpc-apps#storage-file-vpc-custom-sc).

- Your app needs to run as non-root.
- Your cluster is in a different resource group from your VPC and subnet.
- You need to limit file share access to pods on a given node or in a given zone.
- You need to bring your own (BYOK) encryption using a KMS provider such as HPCS or Key Protect.
- You need to manually specify the subnet or IP address of the [Virtual Network Interface (VNI)](/docs/vpc?topic=vpc-file-storage-vpc-about&interface=ui#fs-mount-granular-auth).
- You need more control over capacity and bandwidth. In this case, you can use the `rfs` profile. For more information, see [Regional file shares overview](/docs/vpc?topic=vpc-file-storage-profiles&interface=ui#rfs-profile).

If your cluster and VPC are not in the same resource group, you must specify the VPC resource group ID in the `resourceGroup` section and the `kube-<clusterID>` security group ID in the `securityGroupIDs` section. You can find the ID of the `kube-<clusterID>` security group by running `ibmcloud is sg kube-<cluster-id>  | grep ID`.
{: important}


1. Create a storage class configuration file. The following example uses the `dp2` [profile](/docs/vpc?topic=vpc-file-storage-profiles&interface=ui#dp2-profile).

    ```yaml
    apiVersion: storage.k8s.io/v1
    kind: StorageClass
    metadata:
      name: ibmc-vpc-file-custom-sc
      labels:
        app.kubernetes.io/name: ibm-vpc-file-csi-driver
    provisioner: vpc.file.csi.ibm.io
    mountOptions:
      - hard
      - nfsvers=4.1
      - sec=sys
    parameters:
        profile: "dp2" # or rfs
        billingType: "hourly" # hourly or monthly
        encrypted: "false"
        encryptionKey: "" # If encrypted is true, then a user must specify the CRK-CRN.
        resourceGroup: "" # Resource group ID. By default, the resource group of the cluster will be used from storage-secrete-store secret.
        isENIEnabled: "true" # VPC File Share VNI feature will be used by all PVCs created with this storage class.
        securityGroupIDs: "" # By default cluster security group i.e kube-<clusterID> will be used. User can provide their own comma separated SGs.
        subnetID: "" # User can provide subnetID in which the VNI will be created. Zone and region are mandatory for this. If not provided CSI driver will use the subnetID available in the cluster's VPC zone.
        region: "" # VPC CSI driver will select a region from cluster node's topology. The user can override this default.
        zone: "" # VPC CSI driver will select a region from cluster node's topology. The user can override this default.
        primaryIPID: "" # Existing ID of reserved IP from the same subnet as the file share zone. Zone and region are mandatory for this. SubnetID is not mandatory for this.
        primaryIPAddress: "" # IPAddress for VNI to be created in the subnet of the zone. Zone, region and subnetID are mandatory for this.
        iops: "" # Example: 100, this option is valid only for the dp2 profile.
        throughput: "" # Example: 2000, this option is valid only for the rfs profile
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


## Setting the default storage class
{: #vpc-file-set-default-sc}

- Changing the default storage class is only available for add-on version 2.0 or later.
- You can set the default storage class to one of the pre-installed {{site.data.keyword.filestorage_vpc_short}} classes or your own custom storage class. If you are using a custom storage class, make sure the provisioner is set to `vpc.file.csi.ibm.io`.
- If multiple storage classes are set as the default in a cluster, any of the default storage classes might be used. As a best practice, and to ensure the correct storage class is used, remove any existing default storage classes in the cluster before setting a new default class.


1. Edit the `addon-vpc-file-csi-driver-configmap` configmap and specify the storage class name in `SET_DEFAULT_STORAGE_CLASS` parameter.
    ```sh
    oc edit cm addon-vpc-file-csi-driver-configmap -n kube-system
    ```
    {: pre}

    Example output
    ```sh
    SET_DEFAULT_STORAGE_CLASS: "ibmc-vpc-file-eit"
    ```
    {: screen}

1. Verify the default is set correctly by describing the `file-csi-driver-status` configmap.
    ```sh
    oc describe cm file-csi-driver-status -n kube-system
    ```
    {: pre}


    Example output.
    ```sh
    events:
    ----
    - event: EnableVPCFileCSIDriver
      description: 'VPC File CSI Driver enable successful, DriverVersion: v2.0.6'
      timestamp: "2024-09-20 12:01:02"
    - event: Change default storage class request
      description: Successfully set 'ibmc-vpc-file-eit' as default storage class
      timestamp: "2024-09-20 12:01:36"
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
        runAsUser: 3000
        runAsGroup: 1000
      volumes:
      - name: sec-ctx-vol
        persistentVolumeClaim:
            claimName: my-pvc
      containers:
      - name: sec-ctx-demo
        image: busybox:1.28
        command: [ "sh", "-c", "sleep 1h" ]
        volumeMounts:
        - name: sec-ctx-vol
          mountPath: /data/demo
        securityContext:
          allowPrivilegeEscalation: false
    ```
    {: codeblock}

1. Verify the pod is running.

    ```sh
    oc get pods
    ```
    {: pre}


## Setting up KMS encryption for {{site.data.keyword.filestorage_vpc_short}}
{: #storage-file-kms}

Use a key management service (KMS) provider, such as {{site.data.keyword.keymanagementservicelong}} or {{site.data.keyword.hscrypto}}, to create a private root key that you use in your {{site.data.keyword.filestorage_vpc_short}} instance to encrypt data as it is written to storage. After you create the private root key, create your own storage class or a Kubernetes secret with your root key and then use this storage class or secret to provision your {{site.data.keyword.filestorage_vpc_short}} instance.
{: shortdesc}


1. Create an instance of the KMS provider that you want to use.
    - [{{site.data.keyword.keymanagementserviceshort}}](/docs/key-protect?topic=key-protect-provision#provision).
    - [{{site.data.keyword.hscrypto}}](https://cloud.ibm.com/catalog/services/hyper-protect-crypto-services){: external}.

1. Create a root key in your KMS instance.
    - [{{site.data.keyword.keymanagementserviceshort}} root key](/docs/key-protect?topic=key-protect-create-root-keys#create-root-keys).
    - [{{site.data.keyword.hscrypto}} root key](/docs/hs-crypto?topic=hs-crypto-create-root-keys). By default, the root key is created without an expiration date.

1. Complete the [prerequisites for customer-managed encryption](/docs/vpc?topic=vpc-vpc-encryption-planning#byok-encryption-prereqs) and authorize {{site.data.keyword.filestorage_vpc_short}} to access {{site.data.keyword.keymanagementservicelong}}. Make sure to give {{site.data.keyword.filestorage_vpc_short}} at least `Reader` access to your KMS instance.
    
1. Create a custom storage class and specify your KMS details.
    ```yaml
    apiVersion: storage.k8s.io/v1
    kind: StorageClass
    metadata:
      name: custom-sc-encrypted
      labels:
        app.kubernetes.io/name: ibm-vpc-file-csi-driver
    provisioner: vpc.file.csi.ibm.io
    mountOptions:
      - hard
      - nfsvers=4.1
      - sec=sys
    parameters:
        profile: "dp2"
        billingType: "hourly" # hourly or monthly
        encrypted: "true"
        encryptionKey: "" # Specify the root key CRN.
        resourceGroup: "" # Resource group ID. By default, the resource group of the cluster will be used from storage-secrete-store secret.
        isENIEnabled: "true" # VPC File Share VNI feature will be used by all PVCs created with this storage class.
        securityGroupIDs: "" # By default cluster security group i.e kube-<clusterID> will be used. User can provide their own comma separated SGs.
        subnetID: "" # User can provide subnetID in which the VNI will be created. Zone and region are mandatory for this. If not provided CSI driver will use the subnetID available in the cluster's VPC zone.
        region: "" # VPC CSI driver will select a region from cluster node's topology. The user can override this default.
        zone: "" # VPC CSI driver will select a region from cluster node's topology. The user can override this default.
        primaryIPID: "" # Existing ID of reserved IP from the same subnet as the file share zone. Zone and region are mandatory for this. SubnetID is not mandatory for this.
        primaryIPAddress: "" # IPAddress for VNI to be created in the subnet of the zone. Zone, region and subnetID are mandatory for this.
        tags: "" # User can add a list of tags "a, b, c" that will be used at the time of provisioning file share, by default CSI driver has its own tags.
        uid: "0" # The initial user identifier for the file share, by default its root.
        gid: "0" # The initial group identifier for the file share, by default its root.
        classVersion: "1"
    reclaimPolicy: "Delete"
    allowVolumeExpansion: true
    ```
    {: codeblock}

1. Create the storage class.
    ```txt
    oc apply -f encrypted-class.yaml
    ```
    {: pre}

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
      storageClassName: custom-sc-encrypted
    ```
    {: codeblock}

1. Create the PVC.

    ```sh
    oc apply -f my-pvc.yaml
    ```
    {: pre}

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
    :   In the volumes section, enter the name of the volume to mount to your pod. Typically this name is the same as `volumeMounts.name`.


1. Create the deployment.

    ```sh
    oc apply -f deployment.yaml
    ```
    {: pre}


## Setting up encryption in-transit (EIT)
{: #storage-file-vpc-eit}

Review the following information about EIT. If you choose to use encryption in-transit, you need to balance your requirements between performance and enhanced security. Encrypting data in-transit can have performance impacts due to the processing that is needed to encrypt and decrypt the data at the endpoints. For more information about encryption in-transit, see [VPC Encryption in Transit](/docs/vpc?topic=vpc-file-storage-vpc-about&interface=ui#fs-eit).

- EIT is available for cluster versions 4.16 and later.
- EIT is available only for RHCOS worker nodes.
- By default, file shares are [encrypted at rest](/docs/vpc?topic=vpc-file-storage-vpc-about&interface=ui#FS-encryption) with IBM-managed encryption. 
- To use EIT with Secure by Default clusters, you must add the following outbound rule to the `kube-<clusterID>` security group.
    - **Protocol**: Any
    - **Source type**: Any
    - **Source**: 0.0.0.0/0
    - **Destination** 169.254.169.254.
- EIT is not available for statically provisioned volumes. To set up EIT, you must use dynamic provisioning.
- EIT packages are automatically updated in your cluster when EIT is enabled.
- If you choose to use Encryption-in-transit, you need to balance your requirements between performance and enhanced security. Encrypting data in transit can have some performance impact due to the processing that is needed to encrypt and decrypt the data at the endpoints. The impact depends on the workload characteristics. Workloads that perform synchronous writes or bypass VSI caching, such as databases, might have a substantial performance impact when EIT is enabled. To determine EIT’s performance impact, benchmark your workload with and without EIT.
- Even without EIT, the data moves through a secure data center network. For more information about network security, see [Security in your VPC](/docs/vpc?topic=vpc-security-in-your-vpc) and [Protecting Virtual Private Cloud (VPC) Infrastructure Services with context-based restrictions](/docs/vpc?topic=vpc-cbr).

File Storage for VPC is considered to be a Financial Services Validated service only when encryption-in-transit is enabled. For more information, see [what is a Financial Services Validated service](/docs/framework-financial-services?topic=framework-financial-services-faqs-framework#financial-services-validated).
{: important}


Complete the following steps to set up encryption-in-transit (EIT) for file shares in your {{site.data.keyword.openshiftlong_notm}} cluster. Enabling EIT installs the required packages on your worker nodes.

1. Make a note of the worker pools in your cluster where you want to enable EIT.
1. Edit the `addon-vpc-file-csi-driver-configmap`.

    ```shell
    oc edit cm addon-vpc-file-csi-driver-configmap -n kube-system
    ```
    {: pre}


1. In the configmap, set `ENABLE_EIT:true` and add worker pools where you want to enable EIT to the `WORKER_POOLS_WITH_EIT`. For example: `"wp1, wp2"`.

    ```yaml
    apiVersion: v1
    data:
      EIT_ENABLED_WORKER_POOLS: "wp1,wp2" # Specify the worker pools where you want to enable EIT. If this field is blank, EIT is not enabled on any worker pools.
      ENABLE_EIT: "true"
    kind: ConfigMap
    metadata:
      creationTimestamp: "2024-06-18T09:45:48Z"
      labels:
        app.kubernetes.io/name: ibm-vpc-file-csi-driver
      name: addon-vpc-file-csi-driver-configmap
      namespace: kube-system
      ownerReferences:
      - apiVersion: csi.drivers.ibmcloud.io/v1
        blockOwnerDeletion: true
        controller: true
        kind: VPCFileCSIDriver
        name: ibm-vpc-file-csi-driver
        uid: d3c8bbcd-24fa-4203-9352-4ab7aa72a055
      resourceVersion: "1251777"
      uid: 5c9d6679-4135-458b-800d-217b34d27c75
    ```
    {: codeblock}

1. After enabling EIT, save and close the config map.

1. To verify EIT is enabled, review the events of the `file-csi-driver-status` config map.

    ```sh
    oc describe cm file-csi-driver-status -n kube-system
    ```
    {: pre}

    Example output

    ```yaml
    apiVersion: v1
    data:
      EIT_ENABLED_WORKER_NODES: |
        default:
        - 10.240.0.10
        - 10.240.0.8
      PACKAGE_DEPLOYER_VERSION: v1.0.0
      events: |
        - event: EnableVPCFileCSIDriver
          description: 'VPC File CSI Driver enable successful, DriverVersion: v2.0.3'
          timestamp: "2024-06-13 09:17:07"
        - event: EnableEITRequest
          description: 'Request received to enableEIT, workerPools: , check the file-csi-driver-status
            configmap for eit installation status on each node of each workerpool.'
          timestamp: "2024-06-13 09:17:31"
        - event: 'Enabling EIT on host: 10.240.0.10'
          description: 'Package installation successful on host: 10.240.0.10, workerpool: wp1'
          timestamp: "2024-06-13 09:17:48"
        - event: 'Enabling EIT on host: 10.240.0.8'
          description: 'Package installation successful on host: 10.240.0.8, workerpool: wp2'
          timestamp: "2024-06-13 09:17:48"
    ```
    {: codeblock}

1. Select a pre-installed storage class that supports EIT or create your own storage class.

    * Create a PVC by using either the `ibmc-vpc-file-eit` storage class.
    * Create your own storage class and set the `isEITenabled` parameter to `true`.

1. Create a PVC that references the storage class you selected, then deploy an app that uses your PVC.




## Limiting file share access by worker pool, zone, or worker node
{: #storage-file-vpc-vni-setup}

The default behavior for {{site.data.keyword.filestorage_vpc_short}} cluster add-on is that pods on any node can access file shares. You can also apply more granular control over how pods access your file shares. For example, you might limit file share access to only pods on a specific node, in a specific zone, on a specific worker pool. Review the following scenarios for how you can configure pod access to your file shares.

When a PVC is created, it creates one file share target per PVC and one VNI IP is reserved on that subnet in the zone. This means the max number of PVCs for VPC file storage depends on the available IP addresses on that subnet.
{: note}

If you use the following VNI features to limit pod access to your file shares, your app might not be highly available.

### Before you begin
{: #storage-file-vpc-vni-prereqs}

To limit file share access by node, zone, or resource group, you must first create a custom VPC security group.

1. List your clusters and make a note of the cluster ID where you want to deploy file storage.
    ```sh
    ibmcloud ks cluster ls
    ```
    {: pre}

1. Get your worker pool details.
    ```sh
    ibmcloud ks worker-pool ls --cluster <cluster>
    ```
    {: pre}
    
2. Get your subnet details.
    ```sh
    ibmcloud ks worker-pool get <worker-pool> --cluster <cluster> | grep -A 3 Subnets
    ```
    {: pre}

1. Get your subnet CIDRs. Repeat this step for each subnet. You use this CIDR range later.
    ```sh
    ibmcloud is subnet <subnet-id> | grep "IPv4 CIDR"
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

    Example output

    ```sh
    nfsServerPath: XXX.XX.XX.XXX:/XX # VNI IP address
    ```
    {: screen}

### Limiting file share access to pods on one worker node
{: #storage-file-vpc-vni-one-worker}

1. Make sure you have [completed the prerequisites](#storage-file-vpc-vni-prereqs).

1. Add the following rule to the custom security group you created earlier.

    ```sh
    ibmcloud is sg-rulec CUSTOM-SG inbound tcp --port-min 111 --port-max 2049 --remote 10.240.0.20 # Worker node IP
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
    ibmcloud is sg-rulec kube-<cluster-ID> outbound tcp --port-min 111 --port-max 2049 --remote 10.240.0.10 # VNI IP
    ```
    {: pre}


1. Create a deployment that uses your PVC. Only pods deployed in the zone that is listed in the previous rule can mount the PVC. Pods that are deployed in other zones cannot access the PVC and are stuck in the Container `creating` state.


### Limiting file share access to pods on worker nodes in a single worker pool
{: #storage-file-vpc-vni-one-pool}

1. Make sure you have [completed the prerequisites](#storage-file-vpc-vni-prereqs).

1. Create inbound rules for each worker pool subnet range.

    ```sh
    ibmcloud is sg-rulec CUSTOM-SG inbound tcp --port-min 111 --port-max 2049 --remote 10.240.0.0/24 # zone 1 subnet cidr range
    ibmcloud is sg-rulec CUSTOM-SG inbound tcp --port-min 111 --port-max 2049 --remote 10.240.1.0/24 # zone 2 subnet cidr range
    ```
    {: pre}

1. Add the following rule to the `kube-clusterID` security group. Specify the IP address of the virtual network interface (VNI) as the remote or source.

    ```sh
    ibmcloud is sg-rulec kube-<cluster-ID> outbound tcp --port-min 111 --port-max 2049 --remote 10.240.0.10 # VNI IP
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
    ```
    {: pre}

1. Add the following rule to the `kube-<clusterID>` security group. Specify the IP address of the virtual network interface (VNI) as the remote or source.

    ```sh
    ibmcloud is sg-rulec kube-<clusterID> outbound tcp --port-min 111 --port-max 2049 --remote 10.240.1.7 # VNI-IP
    ```
    {: pre}

1. Create a deployment that uses your PVC. Only pods deployed in the zone indicated in the rule can mount the PVC. Pods deployed on the restricted worker nodes are stuck in the Container `creating` state.
