---

copyright:
  years: 2024, 2025
lastupdated: "2025-07-28"


keywords: kubernetes, openshift, object storage add-in, cos

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}



# Installing the {{site.data.keyword.cos_full_notm}} cluster add-on
{: #storage-cos-install-addon}

The {{site.data.keyword.cos_full_notm}} cluster add-on is available in Beta for allowlisted accounts only. To get added to the allowlist, contact support. For more information, see [Requesting access to allowlisted features](/docs/openshift?topic=openshift-allowlist-request).
{: beta}

Prerequisites
- The {{site.data.keyword.cos_full_notm}} add-on requires at least 0.2 vCPU and 128 MB of memory.
- Set up a [{{site.data.keyword.cos_full_notm}} instance](/docs/openshift?topic=openshift-storage-cos-understand#create_cos_service).

## Understanding bucket creation and removal
{: #cos-addon-bucket-cd}


- You can use an existing bucket by specifying the bucket name in your PVC.
- If you provide a bucket name and that bucket doesn't exist, then a bucket with that name is created.
- If you don't provide a bucket name, then a bucket with the naming convention `temp-xxx` is created.
- Buckets are deleted based on reclaim policy defined in your storage class.
    - If `reclaimPolicy: Delete` is set, the bucket is deleted when the PVC is deleted.
    - If `reclaimPolicy: Retain` is set, the bucket is retained even after the PVC is deleted.


## Enabling the {{site.data.keyword.cos_full_notm}} add-on
{: #enable-cos-addon}


Before you begin: [Access your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-access_cluster).

1. List the add-ons and find the version you want to install.
    ```sh
    ibmcloud oc cluster addon versions
    ```
    {: pre}

    Example output
    ```sh                                                         
    OK
    Name                        Version            Supported Kubernetes Range   Supported OpenShift Range   Kubernetes Default   OpenShift Default
    ibm-object-csi-driver       1.0 (default)      >=1.30.0 <1.33.0             unsupported                 -                    -
    ibm-object-csi-driver       0.1                >=1.30.0 <1.33.0             >=4.15.0 <4.16.0            -                    -                  -                                    -
    ```
    {: screen}

1. Install the add-on.
    ```sh
    ibmcloud oc cluster addon enable ibm-object-csi-driver --cluster CLUSTER [--version VERSION]
    ```
    {: pre}

1. Verify the installation.
    ```sh
    ibmcloud oc cluster addon ls --cluster CLUSTER
    ```
    {: pre}

    ```sh
    OK
    Name                    Version   Health State   Health Status
    ibm-object-csi-driver   0.1       normal         Addon Ready. For more info: http://ibm.biz/addon-state (H1500)
    ```
    {: screen}

1. List the available storage classes.
    ```sh
    oc get sc | grep object
    ```
    {: pre}

    ```sh
    ibm-object-storage-smart-rclone             cos.s3.csi.ibm.io   Delete          Immediate           false                  17h
    ibm-object-storage-smart-rclone-retain      cos.s3.csi.ibm.io   Retain          Immediate           false                  17h
    ibm-object-storage-smart-s3fs               cos.s3.csi.ibm.io   Delete          Immediate           false                  17h
    ibm-object-storage-smart-s3fs-retain        cos.s3.csi.ibm.io   Retain          Immediate           false                  17h
    ibm-object-storage-standard-rclone          cos.s3.csi.ibm.io   Delete          Immediate           false                  17h
    ibm-object-storage-standard-rclone-retain   cos.s3.csi.ibm.io   Retain          Immediate           false                  17h
    ibm-object-storage-standard-s3fs            cos.s3.csi.ibm.io   Delete          Immediate           false                  17h
    ibm-object-storage-standard-s3fs-retain     cos.s3.csi.ibm.io   Retain          Immediate           false                  17h
    ```
    {: screen}

## Deploying an app that uses {{site.data.keyword.cos_full_notm}}
{: #cos-addon-app}


### Create a Kubernetes secret that contains your COS credentials.
{: #cos-addon-app-secret}

1. [Access your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-access_cluster).

1. Save the following configuration as a file called `secret.yaml`.

    - For **IAM credentials**, use a combination of `apiKey` and `serviceId` from Object Storage.
    - For **HMAC credentials**, use `accessKey` and `secretKey` from Object Storage.

    ```yaml
    apiVersion: v1
    kind: Secret
    type: cos-s3-csi-driver
    metadata:
        name: cos-secret-1 # Name your secret. This same name is used for the PVC in the following steps.
        namespace: <namespace> # Specify the namespace where you want to create the secret.
    data:
        bucketName: <base64-encoded-bucket-name>
        apiKey: <base64-encoded-COS-Service-Instance-API-key>
        serviceID: <base64-encoded-COS-service-ID>
        accessKey: <base64-encoded-HMAC-access-key>
        secretKey: <base64-encoded-HMAC-secret-key>
    stringData:
    # uid: "3000" # Optional: Provide a uid to run as non root user. This must match runAsUser in SecurityContext of pod spec.
    mountOptions: |
        # Review or update the following default s3fs mount options
        #max_stat_cache_size=100000
        #mp_umask=002
        #parallel_count=8  # value depends on the storage class used
        #sigv2
        #use_path_request_style
        #default_acl=private 
        #kernel_cache
        #multipart_size=62
        #retries=5
        #allow_other
        #max_dirty_data=51200
        
        # Review or update the following default rclone mount options
        #--allow-other=true
        #--daemon=true
        #acl=private 
        #upload_cutoff=256Mi 
        #chunk_size=64Mi 
        #upload_concurrency=20 
        #copy_cutoff=1Gi 
        #memory_pool_flush_time=30s 
        #disable_checksum=true 
        #bucket_acl=private 
        #max_upload_parts=64

    ```
    {: codeblock}

    mountOptions
    :    You can customize the mount options for either `s3fs` or `rclone` by editing the `mountOptions` in your secret. For more information, see the [s3fs mount options](https://github.com/IBM/ibm-object-csi-driver/blob/main/cos-csi-mounter/server/s3fs.go){: external} and the [rclone mount options](https://github.com/IBM/ibm-object-csi-driver/blob/main/cos-csi-mounter/server/rclone.go){: external}.

    Currently, the add-on is enabled to support a fixed set of mount options with proper validation for each mount option. If you want to use any other mount options that are not in the validation list, contact support to enable those options.
    {: note}



1. Encode the credentials that you retrieved in the previous section to base64. Repeat this command for each parameter.
    ```sh
    echo -n "<value>" | base64
    ```
    {: pre}

1. Update the configuration file with the base64 encoded values.

1. Create the secret.
    ```sh
    oc apply -f secret.yaml
    ```
    {: pre}


### Create a PVC
{: #cos-addon-app-pvc}

You can either use a single secret across multiple PVCs or one secret per PVC.

You can manage this behavior by using the following annotations in the PVC yaml. These annotations help the driver map the PVC to the correct secret.

```yaml
cos.csi.driver/secret: "<custom-secret>"
cos.csi.driver/secret-namespace: "<namespace>"
```
{: codeblock}

Make sure your secret, PVC, and pods are all in the same namespace
{: note}


Example PVC for a 1-to-1 secret to PVC mapping by giving your PVC the same name as the secret you created earlier.
```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: cos-secret-1 # Give your PVC the same name as the secret you created in the previous step.
  namespace: <namespace> # The namespace where you want to create the PVC.
spec:
  accessModes:
  - ReadWriteMany
  resources:
    requests:
      storage: 10Gi
  storageClassName: <storage_class_name> # The storage class you want to use.
```
{: codeblock}


Example PVC for using 1 secret to many PVCs by using annotations to specify the secret.
```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: cos-csi-pvc1
  namespace: <namespace> # The namespace where you want to create the PVC.
  annotations:
    cos.csi.driver/secret: "<custom-secret>" 
    cos.csi.driver/secret-namespace: "<namespace>"
spec:
  accessModes:
  - ReadWriteOnce
  resources:
    requests:
      storage: 256Mi
  storageClassName: <storage_class_name> # The storage class you want to use.
```
{: codeblock}

1. Choose one of the previous examples and customize it for your use case. For a list of storage classes, see the [Storage class reference](#cos-sc-ref-addon).

1. Create the PVC.
    ```sh
    oc apply -f pvc.yaml
    ```
    {: pre}

### Create a deployment
{: #cos-addon-app-dep}

1. Save the following configuration to a file called `dep.yaml`.

    ```yaml
    apiVersion: apps/v1
    kind: Deployment
    metadata:
    name: <name>
    labels:
        app: <name>
    spec:
    replicas: 1
    selector:
        matchLabels:
        app: <name>
    template:
        metadata:
        labels:
            app: <name>
        spec:
        containers:
        - name: app-frontend
            image: <image> # Enter your app image. 
            imagePullPolicy: IfNotPresent
            volumeMounts:
            - mountPath: <path_you_want_to_mount_the_volume_on> # For example `/dev`
            name: cos-csi-volume
        volumes:
        - name: cos-csi-volume
            persistentVolumeClaim:
            claimName: <pvc_name> # Enter the name of the PVC you created earlier.
    ```
    {: codeblock}

1. Create the deployment.
    ```sh
    oc apply -f dep.yaml
    ```
    {: pre}



## Disabling the {{site.data.keyword.cos_full_notm}} add-on
{: #disable-cos-addon}

1. Run the following command to disable the add-on.
    ```sh
     ibmcloud oc cluster addon disable ibm-object-csi-driver --cluster CLUSTER
     ```
     {: pre}

    Example output
     ```sh
    Data and resources that you created for the add-on might be deleted when the add-on is disabled. Continue? [y/N]> y
    Disabling add-on ibm-object-csi-driver for cluster XXX...
    OK
    ```
    {: screen}

1. Verify the add-on was removed.
    ```sh
    ibmcloud oc cluster addon ls --cluster CLUSTER
    ```
    {: pre}



## Migrating from the Helm plug-in to the cluster add-on
{: #cos-addon-migrate-helm}

1. [Access your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-access_cluster).

1. Get the details of your PVCs and select one to migrate.
    ```sh
    oc get pvc --all-namespaces -o custom-columns='NAMESPACE:.metadata.namespace,NAME:.metadata.name' | tail -n +2 | while read namespace pvc; do kubectl describe pvc "$pvc" -n "$namespace" | grep 'volume.kubernetes.io/storage-provisioner: ibm.io/ibmc-s3fs' > /dev/null ; if [ $? -eq 0 ]; then echo "PVC: $pvc in Namespace: $namespace uses ibm.io/ibmc-s3fs storage provisioner"; fi; done
    ```
    {: pre}

    Example output
    ```txt
    PVC: pvc-test in Namespace: default uses ibm.io/ibmc-s3fs storage provisioner
    ```
    {: screen}

1. Describe the PVC and get the bucket name.
    ```sh
    oc describe pvc <pvc_name> | grep ibm.io/bucket:
    ```
    {: pre}

    Example output
    ```txt
    ibm.io/bucket: test-s3
    ```
    {: screen}

1. Recreate your secret with the bucket name included.
    ```yaml
    apiVersion: v1
    kind: Secret
    type: cos-s3-csi-driver
    metadata:
        name: cos-secret-1 # Name your secret.
        namespace: <namespace> # Specify the namespace where you want to create the secret.
    data:
        bucketName: <base64-encoded-bucket-name>
        accessKey: <base64-encoded-HMAC-access-key>
        secretKey: <base64-encoded-HMAC-secret-key>
    stringData:
    # uid: "3000" # Optional: Provide a uid to run as non root user. This must match runAsUser in SecurityContext of pod spec.
    mountOptions: |
        key1=value1
        key2=value2
    ```
    {: codeblock}
    
1. Find the storage class that was used in your PVC.
    ```sh
    oc describe pvc <pvc_name> | grep StorageClass:
    ```
    {: pre}

    Example command for a PVC called `test-s3`.
    ```sh
    oc describe pvc test-s3 | grep StorageClass:
    ```
    {: pre}

    Example output
    ```txt
    StorageClass:  ibmc-s3fs-smart-perf-regional
    ```
    {: screen}

1. [Review the new storage classes](#cos-sc-ref-addon) that are available with the add-on and select a replacement class.
    * If you used a `flex` class, choose one of the new `smart` classes.
    * If you used a `standard` classes, choose one of the new `standard` classes.
    * The `cold` and `vault` classes are no longer available with the add-on; choose a `smart` or `standard` class instead.

1. Review the details of your PVC.
    ```sh
    oc describe pvc test-s3
    ```
    {: pre}

    Example output

    ```txt
    Name:          pvc-test
    Namespace:     default
    StorageClass:  ibmc-s3fs-smart-perf-regional
    Status:        Bound
    Volume:        pvc-c625474d-31f0-4929-bc3e-feace1fb42fb
    Labels:        <none>
    Annotations:   ibm.io/auto-create-bucket: true
                ibm.io/auto-delete-bucket: true
                ibm.io/bucket: bha-test-s23
                ibm.io/secret-name: satstoragesecret
                pv.kubernetes.io/bind-completed: yes
                pv.kubernetes.io/bound-by-controller: yes
                volume.beta.kubernetes.io/storage-provisioner: ibm.io/ibmc-s3fs
                volume.kubernetes.io/storage-provisioner: ibm.io/ibmc-s3fs
    Finalizers:    [kubernetes.io/pvc-protection]
    Capacity:      3Gi
    Access Modes:  RWO
    VolumeMode:    Filesystem
    Used By:       test-pod
    Events:        <none>
    ```
    {: screen}

1. Create a replacement PVC that uses a new storage class and references the secret you created earlier.
    ```yaml
    apiVersion: v1
    kind: PersistentVolumeClaim
    metadata:
    name: cos-csi-pvc1
    namespace: <namespace> # The namespace where you want to create the PVC.
    annotations:
        cos.csi.driver/secret: "cos-secret-1"  # Secret created in step 4
        cos.csi.driver/secret-namespace: "<secret_namespace>"
    spec:
    accessModes:
    - ReadWriteOnce
    resources:
        requests:
        storage: 256Mi
    storageClassName: <storage_class_name> # The storage class you picked based on old storage class mapping.
    ```
    {: codeblock}

1. Verify the PVC is `Bound`.
    ```sh
    oc get pvc
    ```
    {: pre}

1. Get the details of your app.
    ```sh
    oc get pods
    ```
    {: pre}

1. Scale down your app to zero.
    ```sh
    kubectl scale deployment --replicas=0 my-app
    ```
    {: pre}

1. Create a replacement deployment that references the PVC you created in the previous step.


1. After the new deployment is running, you can delete the old deployment.

1. Repeat these steps for each PVC that you want to migrate.



## {{site.data.keyword.cos_full_notm}} cluster add-on storage classes
{: #cos-sc-ref-addon}

| Name | Reclaim policy | Binding mode |
| --- | --- | --- |
| ibm-object-storage-smart-rclone | Delete | Immediate |
| ibm-object-storage-smart-rclone-retain | Retain | Immediate |
| ibm-object-storage-smart-s3fs | Delete | Immediate |
| ibm-object-storage-smart-s3fs-retain | Retain | Immediate |
| ibm-object-storage-standard-rclone | Delete | Immediate |
| ibm-object-storage-standard-rclone-retain | Retain | Immediate |
| ibm-object-storage-standard-s3fs |  Delete | Immediate |
| ibm-object-storage-standard-s3fs-retain | Retain | Immediate |
{: caption="COS cluster add-on storage classes." caption-side="bottom"}
