---

copyright:
  years: 2024, 2026
lastupdated: "2026-04-22"


keywords: kubernetes, openshift, object storage add-in, cos

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}



# Installing the {{site.data.keyword.cos_full_notm}} cluster add-on
{: #storage-cos-install-addon}


Prerequisites:
- The {{site.data.keyword.cos_full_notm}} add-on requires at least 0.3 vCPU and 360 MB of memory.
- The add-on is available for Red Hat CoreOS (RHCOS) and Ubuntu worker nodes. If your cluster has both RHEL and RHCOS nodes, then the add-on is deployed only on the RHCOS nodes.
- Set up an [{{site.data.keyword.cos_full_notm}} instance](/docs/openshift?topic=openshift-storage-cos-understand#create_cos_service).
- **Optional** If you plan to use bucket versioning, your service credentials must have **Manager** or **Writer** permissions to enable or disable bucket versioning on the bucket. For more information, see [Getting started with versioning](/docs/cloud-object-storage?topic=cloud-object-storage-versioning#versioning-getting-started).



## Understanding bucket creation and removal
{: #cos-addon-bucket-cd}


- You can use an existing bucket by specifying the bucket name in your PVC.
- If you provide a bucket name and that bucket doesn't exist, then a bucket with that name is created.
- If you don't provide a bucket name, then a bucket with the naming convention `temp-xxx` is created.
- Buckets are deleted based on reclaim policy defined in your storage class.
    - If `reclaimPolicy: Delete` is set, the bucket is deleted when the PVC is deleted.
    - If `reclaimPolicy: Retain` is set, the bucket is retained even after the PVC is deleted.


## Enabling the {{site.data.keyword.cos_full_notm}} add-on from the CLI
{: #enable-cos-addon}


Before you begin: [Access your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-access_cluster).

1. List the add-ons and find the version you want to install.
    ```sh
    ibmcloud oc cluster addon versions
    ```
    {: pre}

1. Review the add-on options.
    ```sh
    ibmcloud oc cluster addon options --addon ibm-object-csi-driver [--version VERSION]
    ```
    {: pre}

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
    ibm-object-csi-driver   1.0       normal         Addon Ready. For more info: http://ibm.biz/addon-state (H1500)
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

1. Save the following configuration as a file called `secret.yaml`. Provide either IAM credentials or HMAC, but not both.

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
        apiKey: <base64-encoded-COS-Service-Instance-apikey>
        serviceID: <base64-encoded-COS-resource_instance_id>
        accessKey: <base64-encoded-HMAC-access_key_id>
        secretKey: <base64-encoded-HMAC-secret_access_key>
        kp-root-key-crn: <CRN> # Key Protect or HPCS root key crn in base64 encoded format
    stringData:
        bucketName: <bucket-name> # Optional. If you don't provide a bucket name, a bucket with the naming convention s3fs-timestamp-xxx or rclone-timestamp-xxx is created.
        bucketVersioning: false # Bucket versioning is set to false by default. Set to true to enable bucket versioning. Set to false to disable versioning for a bucket where versioning is enabled.
    # uid: "3000" # Optional: Provide a uid to run as non root user. This must match runAsUser in SecurityContext of pod spec.
    mountOptions: |
        # Review or update the following default s3fs mount options
        #multipart_size=52
        #multireq_max=20
        #max_dirty_data=5120
        #parallel_count=20
        #max_stat_cache_size=100000
        #retries=5
        #kernel_cache
        
        # Review or update the following default rclone mount options
        #acl=private
        #bucket_acl=private
        #upload_cutoff=100Mi
        #chunk_size=16Mi
        #max_upload_parts=1000
        #upload_concurrency=8

    ```
    {: codeblock}

    `mountOptions`
    :   You can customize the mount options for either `s3fs` or `rclone` by editing the `mountOptions` in your secret. Align the options that you specify with the storage class that your PVC uses. To review the default values for a storage class, run `oc describe storageclass <storageclass_name>` or `oc describe storageclass <storageclass_name>`. For more information, see the [s3fs mount options](https://github.com/IBM/ibm-object-csi-driver/blob/main/cos-csi-mounter/server/s3fs.go){: external} and the [`rclone` mount options](https://github.com/IBM/ibm-object-csi-driver/blob/main/cos-csi-mounter/server/rclone.go){: external}.

    Currently, the add-on is enabled to support a fixed set of mount options with proper validation for each mount option. If you want to use any other mount options that are not in the validation list, contact support to enable those options.
    {: note}



1. Encode all the secret data parameters to base64.
    ```sh
    echo -n "<value>" | base64
    ```
    {: pre}

1. Update the `secret.yaml` with the base64 encoded values.

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
```
{: codeblock}

Make sure that your secret, PVC, and pods are all in the same namespace
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

The existing secrets, PVCs, and deployments are not deleted by disabling the add-on or by patch updates. There are no disruptions to existing customer workloads.
{: note}

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

1. Re-create your secret with the bucket name included.
    ```yaml
    apiVersion: v1
    kind: Secret
    type: cos-s3-csi-driver
    metadata:
        name: cos-secret-1 # Name your secret.
        namespace: <namespace> # Specify the namespace where you want to create the secret.
    data:
        accessKey: <base64-encoded-HMAC-access-key>
        secretKey: <base64-encoded-HMAC-secret-key>
    stringData:
        bucketName: <bucket-name>
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

The {{site.data.keyword.cos_full_notm}} cluster add-on provides storage classes for the `s3fs` and `rclone` mounters. Choose a storage class that fits your data access requirements. The storage class determines the bucket class, reclaim policy, and default mount behavior for the bucket that is created for your workload.

Standard
:   Use for hot data that you access frequently, such as data for web or mobile apps.

Smart
:   Use for workloads and data that do not follow a specific usage pattern, or when the usage pattern is difficult to predict.

| Name | Bucket class | Mounter | Reclaim policy | Binding mode |
| --- | --- | --- | --- | --- |
| ibm-object-storage-smart-rclone | Smart | `rclone` | Delete | Immediate |
| ibm-object-storage-smart-rclone-retain | Smart | `rclone` | Retain | Immediate |
| ibm-object-storage-smart-s3fs | Smart | `s3fs` | Delete | Immediate |
| ibm-object-storage-smart-s3fs-retain | Smart | `s3fs` | Retain | Immediate |
| ibm-object-storage-standard-rclone | Standard | `rclone` | Delete | Immediate |
| ibm-object-storage-standard-rclone-retain | Standard | `rclone` | Retain | Immediate |
| ibm-object-storage-standard-s3fs | Standard | `s3fs` | Delete | Immediate |
| ibm-object-storage-standard-s3fs-retain | Standard | `s3fs` | Retain | Immediate |
{: caption="COS cluster add-on storage classes" caption-side="bottom"}

To review the detailed bucket configuration for a storage class, run `oc describe storageclass <storageclass_name>` or `oc describe storageclass <storageclass_name>`.

### Storage class parameters
{: #cos-sc-ref-addon-params}

All cluster add-on storage classes include the following core parameters.

| Parameter | Description |
| --- | --- |
| `client` | Identifies the client type that the driver uses. The add-on storage classes use `awss3`. |
| `cosEndpoint` | Defines the {{site.data.keyword.cos_full_notm}} endpoint for the bucket region. |
| `csi.storage.k8s.io/node-publish-secret-name` | References the name of the secret that contains your {{site.data.keyword.cos_full_notm}} credentials. |
| `csi.storage.k8s.io/node-publish-secret-namespace` | References the namespace of the secret that contains your {{site.data.keyword.cos_full_notm}} credentials. |
| `locationConstraint` | Defines the bucket class and region, such as `au-syd-smart` or `au-syd-standard`. |
| `mounter` | Specifies whether the storage class uses the `s3fs` or `rclone` mounter. |
{: caption="Core parameters for COS cluster add-on storage classes" caption-side="bottom"}

### Default `s3fs` storage class mount options
{: #cos-sc-ref-addon-s3fs}

The `s3fs` storage classes use the following default mount options.

| Mount option | Description |
| --- | --- |
| `multipart_size=52` | Sets the part size, in MB, for each multipart request. |
| `multireq_max=20` | Sets the maximum number of parallel requests for listing objects. |
| `max_dirty_data=5120` | Flushes dirty data to S3 after a specified number of MB are written. The minimum supported value is `50`. A value of `-1` disables this behavior. |
| `parallel_count=20` | Sets the number of parallel requests for uploading large objects. `s3fs` uploads large objects by using multipart requests and sends requests in parallel. |
| `max_stat_cache_size=100000` | Sets the maximum number of entries in the stat cache and symbolic link cache. |
| `retries=5` | Sets the number of times to retry a failed S3 transaction. |
| `kernel_cache` | Enables the kernel buffer cache for the volume mount point. Data that is read from {{site.data.keyword.cos_full_notm}} is stored in the kernel cache to help provide faster read access. Kernel cache is enabled for the standard and smart `s3fs` storage classes. |
{: caption="Default mount options for COS add-on `s3fs` storage classes" caption-side="bottom"}

### Default `rclone` storage class mount options
{: #cos-sc-ref-addon-rclone}

The `rclone` storage classes use the following default mount options.

| Mount option | Description |
| --- | --- |
| `acl=private` | Ensures that uploaded objects are not publicly accessible. |
| `bucket_acl=private` | Sets the default ACL for buckets that `rclone` creates to `private`. |
| `upload_cutoff=100Mi` | Uploads files larger than `100 MiB` by using multipart upload. Smaller files are uploaded in a single request. |
| `chunk_size=16Mi` | Sets the size of each part in a multipart upload. |
| `max_upload_parts=1000` | Sets the maximum number of parts per multipart upload and indirectly caps the maximum supported file size with the configured `chunk_size`. With `chunk_size=16Mi`, the maximum file size is `16 GiB`. |
| `upload_concurrency=8` | Sets the number of parts that are uploaded in parallel during a multipart upload. |
{: caption="Default mount options for COS add-on `rclone` storage classes" caption-side="bottom"}
