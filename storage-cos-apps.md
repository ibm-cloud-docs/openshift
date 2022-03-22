---

copyright:
  years: 2014, 2022
lastupdated: "2022-03-22"

keywords: openshift

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}

# Adding object storage to apps
{: #storage_cos_apps}

Create a persistent volume claim (PVC) to provision {{site.data.keyword.cos_full_notm}} for your cluster.
{: shortdesc}

Depending on the settings that you choose in your PVC, you can provision {{site.data.keyword.cos_full_notm}} in the following ways:
- [Dynamic provisioning](/docs/openshift?topic=openshift-kube_concepts#dynamic_provisioning): When you create the PVC, the matching persistent volume (PV) and the bucket in your {{site.data.keyword.cos_full_notm}} service instance are automatically created.
- [Static provisioning](/docs/openshift?topic=openshift-kube_concepts#static_provisioning): You can reference an existing bucket in your {{site.data.keyword.cos_full_notm}} service instance in your PVC. When you create the PVC, only the matching PV is automatically created and linked to your existing bucket in {{site.data.keyword.cos_full_notm}}.

Before you begin:
- [Create and prepare your {{site.data.keyword.cos_full_notm}} service instance](/docs/openshift?topic=openshift-storage-cos-understand#create_cos_service).
- [Create a secret to store your {{site.data.keyword.cos_full_notm}} service credentials](/docs/openshift?topic=openshift-storage-cos-understand#create_cos_secret)).
- [Decide on the configuration for your {{site.data.keyword.cos_full_notm}}](/docs/openshift?topic=openshift-storage_cos_install#configure_cos).

To add {{site.data.keyword.cos_full_notm}} to your cluster:

1. Create a configuration file to define your persistent volume claim (PVC). If you add your [{{site.data.keyword.cos_full_notm}} credentials to the default storage classes](/docs/containers?topic=containers-storage_cos_install), you don't need to list your secret in the PVC.

    ```yaml
    kind: PersistentVolumeClaim
    apiVersion: v1
    metadata:
      name: <name> # Enter the name of the PVC.
      namespace: <namespace> # Enter the namespace where you want to create the PVC. The PVC must be created in the same namespace where you created the Kubernetes secret for your service credentials and where you want to run your pod.
      annotations:
        ibm.io/auto-create-bucket: "<true_or_false>"
        ibm.io/auto-delete-bucket: "<true_or_false>"
        ibm.io/bucket: "<bucket_name>"
        ibm.io/object-path: "<bucket_subdirectory>"
        ibm.io/secret-name: "<secret_name>"
        ibm.io/endpoint: "https://<s3fs_service_endpoint>"
        ibm.io/tls-cipher-suite: "default"
        ibm.io/secret-namespace: "<secret-namespace>" # By default, the COS plug-in searches for your secret in the same namespace where you create the PVC. If you created your secret in a namespace other than the namespace where you want to create your PVC, enter the namespace where you created your secret.
    spec:
      accessModes:
        - ReadWriteOnce
      resources:
        requests:
          storage: <size>
      storageClassName: <storage_class>
    ```
    {: codeblock}

    `ibm.io/auto-create-bucket`
    :   Choose between the following options. 
    :   `true`: When you create the PVC, the PV and the bucket in your {{site.data.keyword.cos_full_notm}} service instance are automatically created. Choose this option to create a new bucket in your {{site.data.keyword.cos_full_notm}} service instance. Note that the service credentials must have **Writer** permissions to automatically create the bucket.
    :   `false`: Choose this option if you want to access data in an existing bucket. When you create the PVC, the PV is automatically created and linked to the bucket that you specify in `ibm.io/bucket`.

    `ibm.io/auto-delete-bucket`
    :   Choose between the following options.
    :   `true`: Your data, the bucket, and the PV is automatically removed when you delete the PVC. Your {{site.data.keyword.cos_full_notm}} service instance remains and is not deleted. If you choose to set this option to `true`, then you must set `ibm.io/auto-create-bucket: true` and `ibm.io/bucket: ""` so that your bucket is automatically created with a name with the format `tmp-s3fs-xxxx`.
    :   `false`: When you delete the PVC, the PV is deleted automatically, but your data and the bucket in your {{site.data.keyword.cos_full_notm}} service instance remain. To access your data, you must create a new PVC with the name of your existing bucket.
    
    `ibm.io/bucket`
    :   Choose between the following options.
    :   If `ibm.io/auto-create-bucket` is set to `true`: Enter the name of the bucket that you want to create in {{site.data.keyword.cos_full_notm}}. If in addition `ibm.io/auto-delete-bucket` is set to `true`, you must leave this field blank to automatically assign your bucket a name with the format `tmp-s3fs-xxxx`. The name must be unique in {{site.data.keyword.cos_full_notm}}.
    :   If `ibm.io/auto-create-bucket` is set to `false`: Enter the name of the existing bucket that you want to access in the cluster. 
    
    `ibm.io/object-path`
    :   Optional: Enter the name of the existing subdirectory in your bucket that you want to mount. Use this option if you want to mount a subdirectory only and not the entire bucket. To mount a subdirectory, you must set `ibm.io/auto-create-bucket: "false"` and provide the name of the bucket in `ibm.io/bucket`.
    
    `ibm.io/secret-name`
    :   Enter the name of the secret that holds the {{site.data.keyword.cos_full_notm}} credentials that you created earlier. If you add your [{{site.data.keyword.cos_full_notm}} credentials](/docs/openshift?topic=openshift-storage-cos-understand#service_credentials) to the default storage classes, you must not list secret in the PVC.
    
    `ibm.io/endpoint`
    :   If you created your {{site.data.keyword.cos_full_notm}} service instance in a location that is different from your cluster, enter the private or public cloud service endpoint of your {{site.data.keyword.cos_full_notm}} service instance that you want to use. For more information and an overview of available service endpoints, see [Additional endpoint information](/docs/cloud-object-storage?topic=cloud-object-storage-advanced-endpoints). By default, the `ibmc` Helm plug-in automatically retrieves your cluster location and creates the storage classes by using the {{site.data.keyword.cos_full_notm}} private cloud service endpoint that matches your cluster location. If your classic cluster is in a multizone metro, such as `dal10`, the {{site.data.keyword.cos_full_notm}} private cloud service endpoint for the multizone metro, for example Dallas. To verify that the service endpoint in your storage classes matches the service endpoint of your service instance, run `oc describe storageclass < storageclassname>`. Make sure that you enter your service endpoint in the format `https://< s3fs_private_service_endpoint>` for private cloud service endpoints, or `http://< s3fs_public_service_endpoint>` for public cloud service endpoints. If the service endpoint in your storage class matches the service endpoint of your {{site.data.keyword.cos_full_notm}} service instance, don't include the `ibm.io/endpoint` option in your PVC YAML file. 
    
    `storage`
    :   In the spec resources requests section, enter a fictitious size for your {{site.data.keyword.cos_full_notm}} bucket in gigabytes. The size is required by Kubernetes, but not respected in {{site.data.keyword.cos_full_notm}}. You can enter any size that you want. The actual space that you use in {{site.data.keyword.cos_full_notm}} might be different and is billed based on the [pricing table](https://cloud.ibm.com/objectstorage/create#pricing){: external}.
    
    `storageClassName`
    :   Choose between the following options.
    :   If `ibm.io/auto-create-bucket: "true"`: Enter the storage class that you want to use for your new bucket.
    :   If `ibm.io/auto-create-bucket: "false"`: Enter the storage class that you used to create your existing bucket. 
    :   If you manually created the bucket in your {{site.data.keyword.cos_full_notm}} service instance or you can't remember the storage class that you used, find your service instance in the {{site.data.keyword.cloud_notm}} dashboard and review the **Class** and **Location** of your existing bucket. Then, use the appropriate [storage class](/docs/containers?topic=containers-storage_cos_reference).
        The {{site.data.keyword.cos_full_notm}} API endpoint that is set in your storage class is based on the region that your cluster is in. If you want to access a bucket that is located in a different region than the one where your cluster is in, you must create a [custom storage class](/docs/openshift?topic=openshift-kube_concepts#customized_storageclass) and use the appropriate API endpoint for your bucket.
        {: note}
        
    `secret-namespace`
    :   By default, the COS plug-in searches for your secret in the same namespace where you create the PVC. If you created your secret in a namespace other than the namespace where you want to create your PVC, enter the namespace where you created your secret.

1. Create the PVC in your cluster.

    ```sh
    oc apply -f filepath/pvc.yaml
    ```
    {: pre}

1. Verify that your PVC is created and bound to the PV.

    ```sh
    oc get pvc
    ```
    {: pre}

    Example output

    ```sh
    NAME                  STATUS    VOLUME                                     CAPACITY   ACCESS MODES   STORAGECLASS                     AGE
    s3fs-test-pvc         Bound     pvc-b38b30f9-1234-11e8-ad2b-t910456jbe12   8Gi        RWO            ibmc-s3fs-standard-cross-region  1h
    ```
    {: screen}

1. Optional: If you plan to access your data with a non-root user, or added files to an existing {{site.data.keyword.cos_full_notm}} bucket by using the console or the API directly, make sure that the [files have the correct permission](/docs/containers?topic=containers-cos_nonroot_access) assigned so that your app can successfully read and update the files as needed.

1. To mount the PV to your deployment, create a configuration `.yaml` file and specify the PVC that binds the PV. {: #cos_app_volume_mount}

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
            securityContext:
              runAsUser: <non_root_user>
            volumeMounts:
            - name: <volume_name>
              mountPath: /<file_path>
          volumes:
          - name: <volume_name>
            persistentVolumeClaim:
              claimName: <pvc_name>
    ```
    {: codeblock}

`app`
:   In the metadata section, enter label for the deployment.

`matchLabels.app` and `labels.app`
:   In the spec selector and in the spec template metadata sections, enter a label for your app.

`image`
:   The name of the container image that you want to use. To list available images in your {{site.data.keyword.registrylong_notm}} account, run `ibmcloud cr image-list`.

`name`
:   The name of the container that you want to deploy to your cluster.

`runAsUser`
:   In the spec containers security context section, you can optionally set the run as user value.

`mountPath`
:   In the spec containers volume mounts section, enter the absolute path of the directory to where the volume is mounted inside the container. If you want to share a volume between different apps, you can specify [volume sub paths](https://kubernetes.io/docs/concepts/storage/volumes/#using-subpath){: external} for each of your apps.

`volumeMounts.name`
:   In the spec containers volume mounts section, enter the name of the volume to mount to your pod.

`volumes.name`
:   In the volumes section, enter the name of the volume to mount to your pod. Typically this name is the same as `volumeMounts/name`.

`claimName`
:   In the volumes persistent volume claim section, enter the name of the PVC that binds the PV that you want to use.


## Creating a deployment 
{: #create-cos-deployment-steps}

After you create PVC and deployment configuration files, create the deployment in your cluster.
{: shortdesc}

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

1. Verify that you can write data to your {{site.data.keyword.cos_full_notm}} service instance by logging in to the app pod and writing data. Log in to the pod that mounts your PV.

    ```sh
    oc exec <pod_name> -it bash
    ```
    {: pre}

1. Navigate to your volume mount path that you defined in your app deployment.
1. Create a text file.

    ```sh
    echo "This is a test" > test.txt
    ```
    {: pre}

1. From the {{site.data.keyword.Bluemix}} dashboard, navigate to your {{site.data.keyword.cos_full_notm}} service instance.
1. From the menu, select **Buckets**.
1. Open your bucket, and verify that you can see the `test.txt` that you created.

    

## Using object storage in a stateful set
{: #cos_statefulset}

If you have a stateful app such as a database, you can create stateful sets that use {{site.data.keyword.cos_full_notm}} to store your app's data. Alternatively, you can use an {{site.data.keyword.cloud_notm}} database-as-a-service, such as {{site.data.keyword.cloudant_short_notm}} and store your data in the cloud.
{: shortdesc}

Before you begin:
- [Create and prepare your {{site.data.keyword.cos_full_notm}} service instance](/docs/openshift?topic=openshift-storage-cos-understand#create_cos_service).
- [Create a secret to store your {{site.data.keyword.cos_full_notm}} service credentials](/docs/openshift?topic=openshift-storage-cos-understand#create_cos_secret).
- [Decide on the configuration for your {{site.data.keyword.cos_full_notm}}](/docs/openshift?topic=openshift-storage_cos_install#configure_cos).

To deploy a stateful set that uses object storage:

1. Create a configuration file for your stateful set and the service that you use to expose the stateful set. The following examples show how to deploy NGINX as a stateful set with three replicas, each replica with a separate bucket or sharing the same bucket.

    Example to create a stateful set with three replicas, with each replica using a separate bucket.
    ```yaml
    apiVersion: v1
    kind: Service
    metadata:
      name: nginx-v01
      namespace: default
      labels:
        app: nginx-v01 # must match spec.template.metadata.labels and spec.selector.matchLabels in stateful set YAML
    spec:
      ports:
      - port: 80
        name: web
      clusterIP: None
      selector:
        app: nginx-v01 # must match spec.template.metadata.labels and spec.selector.matchLabels in stateful set YAML
    ---
    apiVersion: apps/v1
    kind: StatefulSet
    metadata:
      name: web-v01
      namespace: default
    spec:
      selector:
        matchLabels:
          app: nginx-v01 # must match spec.template.metadata.labels in stateful set YAML and metadata.labels in service YAML
      serviceName: "nginx-v01"
      replicas: 3
      template:
        metadata:
          labels:
            app: nginx-v01 # must match spec.selector.matchLabels in stateful set YAML and metadata.labels in service YAML
        spec:
          terminationGracePeriodSeconds: 10
          containers:
          - name: nginx
            image: k8s.gcr.io/nginx-slim:0.8
            ports:
            - containerPort: 80
              name: web
            volumeMounts:
            - name: mypvc
              mountPath: /usr/share/nginx/html
      volumeClaimTemplates:
      - metadata:
          name: mypvc
          annotations:
            ibm.io/auto-create-bucket: "true"
            ibm.io/auto-delete-bucket: "true"
            ibm.io/bucket: ""
            ibm.io/secret-name: mysecret
            volume.beta.kubernetes.io/storage-class: ibmc-s3fs-standard-perf-cross-region
            volume.beta.kubernetes.io/storage-provisioner: ibm.io/ibmc-s3fs
        spec:
          accessModes: [ "ReadWriteOnce" ]
          storageClassName: "ibmc-s3fs-standard-perf-cross-region"
          resources:
            requests:
              storage: 1Gi
    ```
    {: codeblock}

    Example to create a stateful set with three replicas that share the same bucket `mybucket`.
    ```yaml
    apiVersion: v1
    kind: Service
    metadata:
      name: nginx-v01
      namespace: default
      labels:
        app: nginx-v01 # must match spec.template.metadata.labels and spec.selector.matchLabels in stateful set YAML
    spec:
      ports:
      - port: 80
        name: web
      clusterIP: None
      selector:
        app: nginx-v01 # must match spec.template.metadata.labels and spec.selector.matchLabels in stateful set YAML
    ---
    apiVersion: apps/v1
    kind: StatefulSet
    metadata:
      name: web-v01
      namespace: default
    spec:
      selector:
        matchLabels:
          app: nginx-v01 # must match spec.template.metadata.labels in stateful set YAML and metadata.labels in service YAML
      serviceName: "nginx-v01"
      replicas: 3
      template:
        metadata:
          labels:
            app: nginx-v01 # must match spec.selector.matchLabels in stateful set YAML and metadata.labels in service YAML
        spec:
          terminationGracePeriodSeconds: 10
          containers:
          - name: nginx
            image: k8s.gcr.io/nginx-slim:0.8
            ports:
            - containerPort: 80
              name: web
            volumeMounts:
            - name: mypvc
              mountPath: /usr/share/nginx/html
      volumeClaimTemplates:
      - metadata:
          name: mypvc
          annotations:
            ibm.io/auto-create-bucket: "false"
            ibm.io/auto-delete-bucket: "false"
            ibm.io/bucket: mybucket
            ibm.io/secret-name: mysecret
            volume.beta.kubernetes.io/storage-class: ibmc-s3fs-standard-perf-cross-region
            volume.beta.kubernetes.io/storage-provisioner: ibm.io/ibmc-s3fs
        spec:
          accessModes: [ "ReadOnlyMany" ]
          storageClassName: "ibmc-s3fs-standard-perf-cross-region"
          resources:
            requests:
              storage: 1Gi
    ```
    {: codeblock}


`name`
:   Enter a name for your stateful set. The name that you enter is used to create the name for your PVC in the format: `<volume_name>-< statefulset_name>-<replica_number>`.

`serviceName`
:   Enter the name of the service that you want to use to expose your stateful set.

`replicas`
:   Enter the number of replicas for your stateful set.

`matchLabels`
:   In the spec selector match labels section, enter all labels that you want to include in your stateful set and your PVC. Labels that you include in the `volumeClaimTemplates` of your stateful set are not recognized by Kubernetes. Instead, you must define these labels in the `spec.selector.matchLabels` and `spec.template.metadata.labels` section of your stateful set YAML. To make sure that all your stateful set replicas are into the load balancing of your service, include the same label that you used in the `spec.selector` section of your service YAML.

`labels`
:   In the spec metadata labels section, enter the same labels that you added to the `spec.selector.matchLabels` section of your stateful set YAML.

`terminationGracePeriodSeconds`
:   Enter the number of seconds to give the `kubelet` to gracefully terminate the pod that runs your stateful set replica. For more information, see [Delete Pods](https://kubernetes.io/docs/tasks/run-application/force-delete-stateful-set-pod/#delete-pods).

`VolumeClaimTemplates.name`
:   In the spec volume claim templates metadata section, enter a name for your volume. Use the same name that you defined in the `spec.containers.volumeMount.name` section. The name that you enter here is used to create the name for your PVC in the format: `<volume_name>-<statefulset_name>-<replica_number>`.

`ibm.io/auto-create-bucket`
:   In the spec volume claim templates metadata section, set an annotation to configure how buckets are created. Choose between the following options: 
    - **true:** Choose this option to automatically create a bucket for each stateful set replica. Note that the service credentials must have **Writer** permissions to automatically create the bucket.
    - **false:** Choose this option if you want to share an existing bucket across your stateful set replicas. Make sure to define the name of the bucket in the `spec.volumeClaimTemplates.metadata.annotions.ibm.io/bucket` section of your stateful set YAML.

`ibm.io/auto-delete-bucket`
:   In the spec volume claim templates metadata section, set an annotation to configure how buckets are deleted. Choose between the following options: 
    - **true:** Your data, the bucket, and the PV is automatically removed when you delete the PVC. Your {{site.data.keyword.cos_full_notm}} service instance remains and is not deleted. If you choose to set this option to true, then you must set `ibm.io/auto-create-bucket: true` and `ibm.io/bucket: ""`so that your bucket is automatically created with a name with the format `tmp-s3fs-xxxx`.
    - **false:** When you delete the PVC, the PV is deleted automatically, but your data and the bucket in your {{site.data.keyword.cos_full_notm}} service instance remain. To access your data, you must create a new PVC with the name of your existing bucket.

`ibm.io/bucket`
:   In the spec volume claim templates metadata section, set an annotation for the bucket details. Choose between the following options:
    - If `ibm.io/auto-create-bucket` is set to **true**: Enter the name of the bucket that you want to create in {{site.data.keyword.cos_full_notm}}. If in addition `ibm.io/auto-delete-bucket` is set to `true`, you must leave this field blank to automatically assign your bucket a name with the format `tmp-s3fs-xxxx`. The name must be unique in {{site.data.keyword.cos_full_notm}}.
    - If `ibm.io/auto-create-bucket` is set to **false**: Enter the name of the existing bucket that you want to access in the cluster.

`ibm.io/secret-name`
:   In the spec volume claim templates metadata annotations section, enter the name of the secret that holds the {{site.data.keyword.cos_full_notm}} credentials that you created earlier. If you add your [{{site.data.keyword.cos_full_notm}} credentials](/docs/containers?topic=containers-storage_cos_install) to the default storage classes, you must not list the secret in the PVC.

`kubernetes.io/storage-class`
:   In the spec volume claim templates metadata annotations section, enter the storage class that you want to use. Choose between the following options:
    - If `ibm.io/auto-create-bucket: "true"`: Enter the storage class that you want to use for your new bucket.
    - If `ibm.io/auto-create-bucket: "false"`: Enter the storage class that you used to create your existing bucket.
    To list existing storage classes, run`oc get storageclasses | grep s3`. If you don't specify a storage class, the PVC is created with the default storage class that is set in your cluster. Make sure that the default storage class uses the `ibm.io/ibmc-s3fs` provisioner so that your stateful set is provisioned with object storage.

`storageClassName`
:   In the spec volume claim templates spec section, enter the same storage class that you entered in the `spec.volumeClaimTemplates.metadata.annotations.volume.beta.kubernetes.io/storage-class` section of your stateful set YAML.

`storage`
:   In the spec volume claim templates spec resource requests section, enter a fictitious size for your {{site.data.keyword.cos_full_notm}} bucket in gigabytes. The size is required by Kubernetes, but not respected in {{site.data.keyword.cos_full_notm}}. You can enter any size that you want. The actual space that you use in {{site.data.keyword.cos_full_notm}} might be different and is billed based on the [pricing table](https://cloud.ibm.com/objectstorage/create#pricing){: external}.