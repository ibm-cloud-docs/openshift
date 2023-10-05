---

copyright: 
  years: 2022, 2023
lastupdated: "2023-10-05"

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
{: important}


Before you begin: [Access your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-access_cluster).

1. Decide on a storage class. For more information, see the [storage class reference](/docs/openshift?topic=openshift-storage-file-vpc-managing). If you don't find what you are looking for or if your app needs to run as non-root, consider creating your own customized storage class. To get started, check out the [customized storage class samples](/docs/openshift?topic=openshift-storage-file-vpc-managing#storage-file-vpc-custom-sc).

1. List available storage classes in {{site.data.keyword.openshiftlong_notm}}.

    ```sh
    oc get storageclasses | grep file
    ```
    {: pre}

    Example output
    ```sh
    NAME                                          TYPE            
    ibmc-vpc-file-10iops-tier                     vpc.file.csi.ibm.io
    ibmc-vpc-file-3iops-tier                      vpc.file.csi.ibm.io
    ibmc-vpc-file-5iops-tier                      vpc.file.csi.ibm.io
    ibmc-vpc-file-retain-10iops-tier              vpc.file.csi.ibm.io
    ibmc-vpc-file-retain-3iops-tier               vpc.file.csi.ibm.io
    ibmc-vpc-file-retain-5iops-tier               vpc.file.csi.ibm.io
    ibmc-vpc-file-retain-dp2                      vpc.file.csi.ibm.io
    ibmc-vpc-file-dp2                             vpc.file.csi.ibm.io
    ```
    {: screen}

1. Review the configuration of a storage class.

    ```sh
    oc describe storageclass <storageclass_name>
    ```
    {: pre}

  
1. Choose the file storage `type`, `IOPS`, `reclaim policy`, and `billing` that you want to use.


## Deploying an app that uses {{site.data.keyword.filestorage_vpc_short}} with dynamic provisioning
{: #vpc_add_file_dynamic}

Create a persistent volume claim (PVC) to dynamically provision {{site.data.keyword.filestorage_vpc_short}} for your cluster. Dynamic provisioning automatically creates the matching persistent volume (PV) and orders the file share in your account.


By default, file shares that are created by using dynamic provisioning with pre-installed storage classes are created with root permissions. If your app needs to run as not root, [create a custom storage class](/docs/openshift?topic=openshift-storage-file-vpc-managing#storage-file-vpc-custom-sc).
{: note}


1. Create a persistent volume claim (PVC) `.yaml` file. The following example creates a claim that is named `mypvc` by using the `ibmc-vpc-file-5iops-tier` storage class, billed `monthly`, with a gigabyte size of `10Gi`.

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
      storageClassName: ibmc-vpc-file-dp2
    ```
      {: codeblock}
    

    `name`
    :   Enter the name of the PVC.
    
    `accessMode`
    :   `ReadWriteMany`: The PVC can be mounted by multiple pods. All pods can read from and write to the volume.
    
    `storage`
    :   Enter the size of the {{site.data.keyword.filestorage_vpc_short}}, in gigabytes (Gi). After your storage is provisioned, you can't change the size of your {{site.data.keyword.filestorage_vpc_short}}. Make sure to specify a size that matches the amount of data that you want to store.
    
    `storageClassName`
    :   The name of the storage class that you want to use to provision {{site.data.keyword.filestorage_vpc_short}}. You can choose to use one of the [IBM-provided storage classes](/docs/openshift?topic=openshift-storage-file-vpc-sc-ref) or [create your own storage class](/docs/containers?topic=containers-storage-file-vpc-managing#storage-file-vpc-custom-sc). If you don't specify a storage class, the PV is created with the default storage class `ibmc-vpc-file-3iops-tier`.


1. Create the PVC.

    ```sh
    oc apply -f mypvc.yaml
    ```
    {: pre}

1. Verify that your PVC is created and bound to the PV. This process can take a few minutes.

    ```sh
    oc describe pvc mypvc
    ```
    {: pre}

    Example output

    ```sh
    Name:        mypvc
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
        3m        3m        1    {ibm.io/ibmc-vpc-file 31898035-3011-11e7-a6a4-7a08779efd33 }            Normal        Provisioning        External provisioner is provisioning volume for claim "default/my-persistent-volume-claim"
        3m        1m        10    {persistentvolume-controller }                            Normal        ExternalProvisioning    can't find provisioner "ibmc-vpc-file-retain-5iops-tier ", expecting that a volume for the claim is provisioned either manually or via external software
        1m        1m        1    {ibm.io/ibmc-vpc-file 31898035-3011-11e7-a6a4-7a08779efd33 }            Normal        ProvisioningSucceeded    Successfully provisioned volume pvc-0d787071-3a67-11e7-aafc-eef80dd2dea2

    ```
    {: screen}

1. Create a deployment `.yaml` file and reference the PVC that you created in the previous step.

    ```yaml
    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: <deployment_name>
      labels:
        app: <deployment_label>
    spec:
      selector:
        matchLabels:
          app: <app_name>
      template:
        metadata:
          labels:
            app: <app_name>
        spec:
          containers:
          - image: <image_name>
            name: <container_name>
            volumeMounts:
            - name: <volume_name>
              mountPath: /<file_path>
          volumes:
          - name: <volume_name>
            persistentVolumeClaim:
              claimName: PVC-NAME
    ```
    {: codeblock}

    `metadata.labels.app`
    :   In the metadata section, enter a label for the deployment.
     
    `matchLabels.app` and `labels.app`
    :   In the spec selector and template metadata sections, enter label for your app.
    
    `image`
    :   The name of the container image that you want to use. To list available images in your {{site.data.keyword.registrylong_notm}} account, run `ibmcloud cr image-list`.
    
    `spec.containers.name`
    :   The name of the container that you want to deploy to your cluster.
    
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
    oc apply -f <local_yaml_path>
    ```
    {: pre}

1. Verify that the PV is successfully mounted.

    ```sh
    oc describe deployment <deployment_name>
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




## Deploying an app that uses {{site.data.keyword.filestorage_vpc_short}} with static provisioning
{: #vpc_add_file_static}

Create a persistent volume claim (PVC) to statically provision {{site.data.keyword.filestorage_vpc_short}} for your cluster. Static provisioning allows cluster administrators to make existing storage devices available to a cluster. 

Before you can create a persistent volume (PV), you have to retrieve details about your file share.

1. Get the ID for your file share.
    ```sh
    ibmcloud is shares
    ```
    {: pre}

1. Get the `share-target`. 
    ```sh
    ibmcloud is share-targets SHARE-ID
    ```
    {: pre}

1. Get the `nfsServerPath`, also called the `Mount Path`. 
    ```sh
    ibmcloud is share-target SHARE-ID SHARE-TARGET-ID
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

1. To mount the storage to your deployment, create a configuration `.yaml` file and specify the PVC that binds the PV.
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
    oc apply -f pvc-static
    ```
    {: pre}

1. Attach your fileshare to the desired application pod. 
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








