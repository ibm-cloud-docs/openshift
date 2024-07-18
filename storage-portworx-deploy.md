---

copyright: 
  years: 2014, 2024
lastupdated: "2024-07-18"


keywords: portworx, kubernetes, <containers>containers</containers><openshift>openshift</openshift>

subcollection: <containers>containers</containers><openshift>openshift</openshift>


---

{{site.data.keyword.attribute-definition-list}}

# Installing Portworx in your cluster
{: #storage_portworx_deploy}

Provision a Portworx service instance from the {{site.data.keyword.cloud_notm}} catalog. After you create the service instance, the latest Portworx enterprise edition (`px-enterprise`) is installed on your cluster by using Helm. In addition, [Stork](https://docs.portworx.com/portworx-enterprise/operations/operate-kubernetes/storage-operations/stork){: external} is also installed on your <containers>{{site.data.keyword.containerlong_notm}}</containers><openshift>{{site.data.keyword.openshiftlong_notm}}</openshift> cluster. Stork is the Portworx storage scheduler. With Stork, you can co-locate pods with their data and create and restore snapshots of Portworx volumes.
{: shortdesc}

Looking for instructions about how to update or remove Portworx? See [Updating Portworx](/docs/<containers>containers</containers><openshift>openshift</openshift>?topic=<containers>containers</containers><openshift>openshift</openshift>-storage_portworx_update) and [Removing Portworx](/docs/<containers>containers</containers><openshift>openshift</openshift>?topic=<containers>containers</containers><openshift>openshift</openshift>-storage_portworx_removing).
{: tip}

Before you begin:
- Make sure that you have the correct [permissions](/docs/<containers>containers</containers><openshift>openshift</openshift>?topic=<containers>containers</containers><openshift>openshift</openshift>-clusters) to create <containers>{{site.data.keyword.containerlong_notm}}</containers><openshift>{{site.data.keyword.openshiftlong_notm}}</openshift> clusters.

- [Create or use an existing cluster](/docs/<containers>containers</containers><openshift>openshift</openshift>?topic=<containers>containers</containers><openshift>openshift</openshift>-clusters).

- If you want to use non-SDS worker nodes in a classic cluster [add a block storage device to your worker node](/docs/<containers>containers</containers><openshift>openshift</openshift>?topic=<containers>containers</containers><openshift>openshift</openshift>-utilities#manual_block).

- Choose if you want to [use the internal Portworx key-value database (KVDB)](/docs/<containers>containers</containers><openshift>openshift</openshift>?topic=<containers>containers</containers><openshift>openshift</openshift>-storage_portworx_kv_store) or [create a Databases for etcd service instance](/docs/<containers>containers</containers><openshift>openshift</openshift>?topic=<containers>containers</containers><openshift>openshift</openshift>-storage_portworx_kv_store) to store the Portworx configuration and metadata.

- Decide whether you want to encrypt your Portworx volumes. To encrypt your volumes, you must [set up an {{site.data.keyword.keymanagementservicelong_notm}} or a {{site.data.keyword.hscrypto}} instance and store your service information in a Kubernetes secret](/docs/<containers>containers</containers><openshift>openshift</openshift>?topic=<containers>containers</containers><openshift>openshift</openshift>-storage_portworx_encryption).

- Make sure that you [copied the image pull secrets from the `default` to the `kube-system` <containers>namespace</containers><openshift>project</openshift>](/docs/<containers>containers</containers><openshift>openshift</openshift>?topic=<containers>containers</containers><openshift>openshift</openshift>-registry#copy_imagePullSecret) so that you can pull images from {{site.data.keyword.registryshort}}. Make sure that you [add the image pull secrets to the Kubernetes service account](/docs/<containers>containers</containers><openshift>openshift</openshift>?topic=<containers>containers</containers><openshift>openshift</openshift>-registry#store_imagePullSecret) of the `kube-system` <containers>namespace</containers><openshift>project</openshift>.

- Decide if you want to include your cluster in a Portworx disaster recovery configuration. For more information, see [Setting up disaster recovery with Portworx](/docs/<containers>containers</containers><openshift>openshift</openshift>?topic=<containers>containers</containers><openshift>openshift</openshift>-storage_portworx_recovery).

- If you attached a separate device for the Portworx journal, make sure that you retrieve the device path by running `lsblk` while logged into your worker node.

- If you attached a separate devices for the Portworx KVDB, make sure that you retrieve the device path by running `lsblk` while logged into your worker node.

- <containers>[Log in to your account. If applicable, target the appropriate resource group. Set the context for your cluster.](/docs/containers?topic=containers-access_cluster)</containers><openshift>[Access your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-access_cluster).</openshift>

To install Portworx:

1. Open the Portworx service from the [{{site.data.keyword.cloud_notm}} catalog](https://cloud.ibm.com/catalog/services/portworx-enterprise){: external} and complete the fields as follows:

    1. Select the region where your <containers>{{site.data.keyword.containerlong_notm}}</containers><openshift>{{site.data.keyword.openshiftlong_notm}}</openshift> cluster is located.
    
    1.  Review the Portworx pricing information.
    
    1. Enter a name for your Portworx service instance.
    
    1. Select the resource group that your cluster is in.
    
    1. In the **Tag** field, enter the name of the cluster where you want to install Portworx. After you create the Portworx service instance, you can't see the cluster that you installed Portworx into. To find the cluster more easily later, make sure that you enter the cluster name and any additional information as tags.
    
    1. Enter an {{site.data.keyword.cloud_notm}} API key to retrieve the list of clusters that you have access to. If you don't have an API key, see [Managing user API keys](/docs/account?topic=account-userapikey). After you enter the API key, the **Kubernetes or OpenShift cluster name** field appears.
    1. Enter a unique **Portworx cluster name**.
    1. In the **Cloud Drives** menu:
        1. Select **Use Cloud Drives** (VPC Clusters only) to dynamically provision {{site.data.keyword.block_storage_is_short}} for Portworx. After selecting **Use Cloud Drives**, select the **Storage class name** and the **Size** of the block storage drives that you want to provision.
        1. Select **Use Already Attached Drives** (Classic, VPC, or Satellite) to use the block storage that is already attached to your worker nodes. 
    1. From the **Portworx metadata key-value store** drop down, choose the type of key-value store that you want to use to store Portworx metadata. Select **Portworx KVDB** to automatically create a key-value store during the Portworx installation, or select **Databases for etcd** if you want to use an existing Databases for etcd instance. If you choose **Databases for etcd**, the **Etcd API endpoints** and **Etcd secret name** fields appear.
    1. **Namespace**: Enter the namespace where you want to deploy the Portworx resources.
    1. **Required for Databases for etcd only**: Enter the information of your Databases for etcd service instance.
        1. [Retrieve the etcd endpoint, and the name of the Kubernetes secret](/docs/<containers>containers</containers><openshift>openshift</openshift>?topic=<containers>containers</containers><openshift>openshift</openshift>-storage_portworx_kv_store) that you created for your Databases for etcd service instance.
        2. In the **Etcd API endpoints** field, enter the API endpoint of your Databases for etcd service instance that you retrieved earlier. Make sure to enter the endpoint in the format `etcd:<etcd_endpoint1>;etcd:<etcd_endpoint2>`. If you have more than one endpoint, include all endpoints and separate them with a semicolon (`;`).
        3. In the **Etcd secret name** field, enter the name of the Kubernetes secret that you created in your cluster to store the Databases for etcd service credentials.
    1. From the **Kubernetes or OpenShift cluster name** drop down list, select the cluster where you want to install Portworx. If your cluster is not listed, make sure that you select the correct {{site.data.keyword.cloud_notm}} region. If the region is correct, verify that you have the correct [permissions](/docs/<containers>containers</containers><openshift>openshift</openshift>?topic=<containers>containers</containers><openshift>openshift</openshift>-clusters) to view and work with your cluster. Make sure that you select a cluster that meets the [minimum hardware requirements for Portworx](https://docs.portworx.com/portworx-enterprise/platform/prerequisites){: external}.
    1. **Optional**: From the **Portworx secret store type** drop down list, choose the secret store type that you want to use to store the volume encryption key.
        - **Kubernetes Secret**: Choose this option if you want to store your own custom key to encrypt your volumes in a Kubernetes Secret in your cluster. The secret must not be present before you install Portworx. You can create the secret after you install Portworx. For more information, see the [Portworx documentation](https://docs.portworx.com/portworx-enterprise/operations/key-management/kubernetes-secrets){: external}.
        - **{{site.data.keyword.keymanagementservicelong_notm}}**: Choose this option if you want to use root keys in {{site.data.keyword.keymanagementservicelong_notm}} to encrypt your volumes. Make sure that you follow the [instructions](/docs/<containers>containers</containers><openshift>openshift</openshift>?topic=<containers>containers</containers><openshift>openshift</openshift>-storage_portworx_encryption) to create your {{site.data.keyword.keymanagementservicelong_notm}} service instance, and to store the credentials for how to access your service instance in a Kubernetes secret in the `portworx` <containers>namespace</containers><openshift>project</openshift> before you install Portworx.
    1. **Optional**: If you want to set up a journal device or KVDB devices, enter the device details in the **Advanced Options** field. Choose from the following options for journal devices.
        
        - Enter `j;auto` to allow Portworx to automatically create a 3 GB partition on one of your block storage devices to use for the journal.
        - Enter `j;</device/path>` to use a specific device for the journal. For example, enter `j;/dev/vde` to use the disk located at `/dev/vde`. To find the path of the device that you want to use for the journal, log in to a worker node and run `lsblk`.
        - Enter `kvdb_dev;<device path>` to specify the device where you want to store internal KVDB data. For example, `kvdb_dev;/dev/vdd`. To find the path of the device that you want to use, log in to a worker node and run `lsblk`. To use a specific device for KVDB data, you must have an available storage device of 3GB or on at least 3 worker nodes. The devices must also and on the same path on each worker node. For example: `/dev/vdd`.

1. Click **Create** to start the Portworx installation in your cluster. This process might take a few minutes to complete. The service details page opens with instructions for how to verify your Portworx installation, create a persistent volume claim (PVC), and mount the PVC to an app.
1. From the [{{site.data.keyword.cloud_notm}} resource list](https://cloud.ibm.com/resources){: external}, find the Portworx service that you created.
1. Review the **Status** column to see if the installation succeeded or failed. The status might take a few minutes to update.
1. If the **Status** changes to `Provision failure`, follow the [instructions](/docs/<containers>containers</containers><openshift>openshift</openshift>?topic=<containers>containers</containers><openshift>openshift</openshift>-debug-portworx) to start troubleshooting why your installation failed.
1. If the **Status** changes to `Provisioned`, verify that your Portworx installation completed successfully and that all your local disks were recognized and added to the Portworx storage layer.
    1. List the Portworx pods in the `kube-system` <containers>namespace</containers><openshift>project</openshift>. The installation is successful when you see one or more `portworx`, `stork`, and `stork-scheduler` pods. The number of pods equals the number of worker nodes that are in your Portworx cluster. All pods must be in a `Running` state.
        ```sh
        <containers>kubectl</containers><openshift>oc</openshift> get pods -n kube-system | grep 'portworx\|stork'
        ```
        {: pre}

        Example output
        ```sh
        portworx-594rw                          1/1       Running     0          20h
        portworx-rn6wk                          1/1       Running     0          20h
        portworx-rx9vf                          1/1       Running     0          20h
        stork-6b99cf5579-5q6x4                  1/1       Running     0          20h
        stork-6b99cf5579-slqlr                  1/1       Running     0          20h
        stork-6b99cf5579-vz9j4                  1/1       Running     0          20h
        stork-scheduler-7dd8799cc-bl75b         1/1       Running     0          20h
        stork-scheduler-7dd8799cc-j4rc9         1/1       Running     0          20h
        stork-scheduler-7dd8799cc-knjwt         1/1       Running     0          20h
        ```
        {: screen}

    2. Log in to one of your `portworx` pods and list the status of your Portworx cluster.
        ```sh
        <containers>kubectl</containers><openshift>oc</openshift> exec <portworx_pod> -it -n kube-system -- /opt/pwx/bin/pxctl status
        ```
        {: pre}

        Example output
        ```sh
        Status: PX is operational
        License: Trial (expires in 30 days)
        Node ID: 10.176.48.67
        IP: 10.176.48.67
        Local Storage Pool: 1 pool
        POOL    IO_PRIORITY    RAID_LEVEL    USABLE    USED    STATUS    ZONE    REGION
          0    LOW        raid0        20 GiB    3.0 GiB    Online    dal10    us-south
        Local Storage Devices: 1 device
        Device    Path                        Media Type        Size        Last-Scan
            0:1    /dev/mapper/3600a09803830445455244c4a38754c66    STORAGE_MEDIUM_MAGNETIC    20 GiB        17 Sep 18 20:36 UTC
                total                            -            20 GiB
        Cluster Summary
        Cluster ID: mycluster
            Cluster UUID: a0d287ba-be82-4aac-b81c-7e22ac49faf5
        Scheduler: kubernetes
        Nodes: 2 node(s) with storage (2 online), 1 node(s) without storage (1 online)
          IP        ID        StorageNode    Used    Capacity    Status    StorageStatus    Version        Kernel            OS
          10.184.58.11    10.184.58.11    Yes        3.0 GiB    20 GiB        Online    Up        1.5.0.0-bc1c580    4.4.0-133-generic    Ubuntu 20.04.5 LTS
          10.176.48.67    10.176.48.67    Yes        3.0 GiB    20 GiB        Online    Up (This node)    1.5.0.0-bc1c580    4.4.0-133-generic    Ubuntu 20.04.5 LTS
          10.176.48.83    10.176.48.83    No        0 B    0 B        Online    No Storage    1.5.0.0-bc1c580    4.4.0-133-generic    Ubuntu 20.04.5 LTS
        Global Storage Pool
          Total Used        :  6.0 GiB
          Total Capacity    :  40 GiB
        ```
        {: screen}

    3. Verify that all worker nodes that you wanted to include in your Portworx storage layer are included by reviewing the **StorageNode** column in the **Cluster Summary** section of your CLI output. Worker nodes that are in the storage layer are displayed with `Yes` in the **StorageNode** column.

        Because Portworx runs as a DaemonSet in your cluster, existing worker nodes are automatically inspected for raw block storage and added to the Portworx data layer when you deploy Portworx. If you add worker nodes to your cluster and add raw block storage to those workers, restart the Portworx pods on the new worker nodes so that your storage volumes are detected by the DaemonSet.
        {: note}

    4. Verify that each storage node is listed with the correct amount of raw block storage by reviewing the **Capacity** column in the **Cluster Summary** section of your CLI output.

    5. Review the Portworx I/O classification that was assigned to the disks that are part of the Portworx cluster. During the setup of your Portworx cluster, every disk is inspected to determine the performance profile of the device. The profile classification depends on how fast the network is that your worker node is connected to and the type of storage device that you have. Disks of SDS worker nodes are classified as `high`. If you manually attach disks to a virtual worker node, then these disks are classified as `low` due to the slower network speed that comes with virtual worker nodes.
        ```sh
        <containers>kubectl</containers><openshift>oc</openshift> exec -it <portworx_pod> -n kube-system -- /opt/pwx/bin/pxctl cluster provision-status
        ```
        {: pre}

        Example output
        
        ```sh
        NODE        NODE STATUS    POOL    POOL STATUS    IO_PRIORITY    SIZE    AVAILABLE    USED    PROVISIONED    RESERVEFACTOR    ZONE    REGION        RACK
        10.184.58.11    Up        0    Online        LOW        20 GiB    17 GiB        3.0 GiB    0 B        0        dal12    us-south    default
        10.176.48.67    Up        0    Online        LOW        20 GiB    17 GiB        3.0 GiB    0 B        0        dal10    us-south    default
        10.176.48.83    Up        0    Online        HIGH        3.5 TiB    3.5 TiB        10 GiB    0 B        0        dal10    us-south    default
        ```
        {: screen}



## Creating a Portworx volume
{: #add_portworx_storage}

Start creating Portworx volumes by using Kubernetes dynamic provisioning.
{: shortdesc}

1. List available storage classes in your cluster and check whether you can use an existing Portworx storage class that was set up during the Portworx installation. The pre-defined storage classes are optimized for database usage and to share data across pods.
    ```sh
    <containers>kubectl</containers><openshift>oc</openshift> get sc | grep portworx
    ```
    {: pre}

    To view the details of a storage class, run `<containers>kubectl</containers><openshift>oc</openshift> describe storageclass <storageclass_name>`.
    {: tip}

2. If you don't want to use an existing storage class, create a customized storage class. For a full list of supported options that you can specify in your storage class, see [Using Dynamic Provisioning](https://docs.portworx.com/portworx-enterprise/operations/operate-kubernetes/storage-operations/create-pvcs/dynamic-provisioning.html){: external}.
    1. Create a configuration file for your storage class.
        ```yaml
        kind: StorageClass
        apiVersion: storage.k8s.io/v1
        metadata:
          name: <storageclass_name>
        provisioner: kubernetes.io/portworx-volume
        parameters:
          repl: "<replication_factor>"
          secure: "<true_or_false>"
          priority_io: "<io_priority>"
          shared: "<true_or_false>"
        ```
        {: codeblock}

        `metadata.name`
        :   Enter a name for your storage class.
        
        `parameters.repl`
        :   Enter the number of replicas for your data that you want to store across different worker nodes. Allowed numbers are `1`,`2`, or `3`. For example, if you enter `3`, then your data is replicated across three different worker nodes in your Portworx cluster. To store your data highly available, use a multizone cluster and replicate your data across three worker nodes in different zones.
            You must have enough worker nodes to fulfill your replication requirement. For example, if you have two worker nodes, but you specify three replicas, then the creation of the PVC with this storage class fails.
            {: note}
        
        `parameters.secure`
        :   Specify whether you want to encrypt the data in your volume with {{site.data.keyword.keymanagementservicelong_notm}}. Choose between the following options.
            - `true`: Enter `true` to enable encryption for your Portworx volumes. To encrypt volumes, you must have an {{site.data.keyword.keymanagementservicelong_notm}} service instance and a Kubernetes secret that holds your customer root key. For more information about how to set up encryption for Portworx volumes, see [Encrypting your Portworx volumes](/docs/<containers>containers</containers><openshift>openshift</openshift>?topic=<containers>containers</containers><openshift>openshift</openshift>-storage_portworx_encryption). 
            - `false`: When you enter `false`, your Portworx volumes are not encrypted. If you don't specify this option, your Portworx volumes are not encrypted by default. You can choose to enable volume encryption in your PVC, even if you disabled encryption in your storage class. The setting that you make in the PVC take precedence over the settings in the storage class.

        `parameters.priority_io`
        :   Enter the Portworx I/O priority that you want to request for your data. Available options are `high`, `medium`, and `low`. During the setup of your Portworx cluster, every disk is inspected to determine the performance profile of the device. The profile classification depends on the network bandwidth of your worker node and the type of storage device. Disks of SDS worker nodes are classified as `high`. If you manually attach disks to a virtual worker node, then these disks are classified as `low` due to the slower network speed that comes with virtual worker nodes. 
        :   When you create a PVC with a storage class, the number of replicas that you specify in `parameters/repl` overrides the I/O priority. For example, when you specify three replicas that you want to store on high-speed disks, but you have only one worker node with a high-speed disk in your cluster, then your PVC creation still succeeds. Your data is replicated across both high and low speed disks.
        
        `parameters.shared`
        :   Define whether you want to allow multiple pods to access the same volume. Choose between the following options:
            - True: If you set this option to `true`, then you can access the same volume by multiple pods that are distributed across worker nodes in different zones.
            - False: If you set this option to `false`, you can access the volume from multiple pods only if the pods are deployed onto the worker node that attaches the physical disk that backs the volume. If your pod is deployed onto a different worker node, the pod can't access the volume.

    2. Create the storage class.
        ```sh
        <containers>kubectl</containers><openshift>oc</openshift> apply -f storageclass.yaml
        ```
        {: pre}

    3. Verify that the storage class is created.
        ```sh
        <containers>kubectl</containers><openshift>oc</openshift> get sc
        ```
        {: pre}

3. Create a persistent volume claim (PVC).
    1. Create a configuration file for your PVC.
        ```yaml
        kind: PersistentVolumeClaim
        apiVersion: v1
        metadata:
          name: mypvc
        spec:
          accessModes:
            - <access_mode>
          resources:
            requests:
              storage: <size>
          storageClassName: portworx-shared-sc
        ```
        {: codeblock}

        `metadata.name`
        :   Enter a name for your PVC, such as `mypvc`.
        
        `spec.accessModes`
        :   Enter the [Kubernetes access mode](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#access-modes){: external} that you want to use.
        
        `resources.requests.storage`
        :   Enter the amount of storage in gigabytes that you want to assign from your Portworx cluster. For example, to assign 2 gigabytes from your Portworx cluster, enter `2Gi`. The amount of storage that you can specify is limited by the amount of storage that is available in your Portworx cluster. If you specified a replication factor in your storage class higher than 1, then the amount of storage that you specify in your PVC is reserved on multiple worker nodes.
        
        `spec.storageClassName`
        :   Enter the name of the storage class that you chose or created earlier and that you want to use to provision your PV. The example YAML file uses the `portworx-shared-sc` storage class.

    2. Create your PVC.
        ```sh
        <containers>kubectl</containers><openshift>oc</openshift> apply -f pvc.yaml
        ```
        {: pre}

    3. Verify that your PVC is created and bound to a persistent volume (PV). This process might take a few minutes.
        ```sh
        <containers>kubectl</containers><openshift>oc</openshift> get pvc
        ```
        {: pre}

        

## Mounting the volume to your app
{: #mount_pvc}

To access the storage from your app, you must mount the PVC to your app.
{: shortdesc}

1. Create a configuration file for a deployment that mounts the PVC.

    For tips on how to deploy a stateful set with Portworx, see [StatefulSets]<containers>(https://docs.portworx.com/portworx-enterprise/operations/operate-kubernetes/application-install-with-kubernetes/cassandra){: external}</containers><openshift>(https://portworx.com/blog/cassandra-openshift-run-ha-cassandra-red-hat-openshift/){: external}</openshift>{: external}. The Portworx documentation also includes examples for how to deploy Cassandra, [Kafka](https://docs.portworx.com/portworx-enterprise/operations/operate-kubernetes/application-install-with-kubernetes/kafka-with-zookeeper){: external}, [ElasticSearch with Kibana](https://docs.portworx.com/portworx-enterprise/operations/operate-kubernetes/application-install-with-kubernetes/elastic-search-and-kibana){: external}, and [WordPress with MySQL](https://docs.portworx.com/portworx-enterprise/operations/operate-kubernetes/application-install-with-kubernetes/wordpress){: external}.
    {: tip}

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
          schedulerName: stork
          containers:
          - image: <image_name>
            name: <container_name>
          securityContext:
              fsGroup: <group_ID>
            volumeMounts:
            - name: <volume_name>
              mountPath: /<file_path>
          volumes:
          - name: <volume_name>
            persistentVolumeClaim:
              claimName: <pvc_name>
    ```
    {: codeblock}

    `metadata.labels.app`
    :   A label for the deployment.
    
    `spec.selector.matchLabels.app` and `spec.template.metadata.labels.app`
    :   A label for your app.
    
    `template.metadata.labels.app`
    :   A label for the deployment.
    
    `spec.schedulerName`
    :   Use [Stork](https://docs.portworx.com/portworx-enterprise/operations/operate-kubernetes/storage-operations/stork){: external} as the scheduler for your Portworx cluster. With Stork, you can co-locate pods with their data, provides seamless migration of pods in case of storage errors and makes it easier to create and restore snapshots of Portworx volumes.
    
    `spec.containers.image`
    :   The name of the image that you want to use. To list available images in your {{site.data.keyword.registrylong_notm}} account, run `ibmcloud cr image-list`.
    
    `spec.containers.name`
    :   The name of the container that you want to deploy to your cluster.
    
    `spec.containers.securityContext.fsGroup`
    :   Optional: To access your storage with a non-root user, specify the [security context](https://kubernetes.io/docs/tasks/configure-pod-container/security-context/){: external} for your pod and define the set of users that you want to grant access in the `fsGroup` section on your deployment YAML. For more information, see [Accessing Portworx volumes with a non-root user](https://docs.portworx.com/portworx-enterprise/operations/operate-kubernetes/storage-operations/create-pvcs/access-via-non-root-users){: external}.
    
    `spec.containers.volumeMounts.mountPath`
    :   The absolute path of the directory to where the volume is mounted inside the container. If you want to share a volume between different apps, you can specify [volume sub paths](https://kubernetes.io/docs/concepts/storage/volumes/#using-subpath){: external} for each of your apps.
    
    `spec.containers.volumeMounts.name`
    :   The name of the volume to mount to your pod.
    
    `volumes.name`
    :   The name of the volume to mount to your pod. Typically this name is the same as `volumeMounts/name`.
    
    `volumes.persistentVolumeClaim.claimName`
    :   The name of the PVC that binds the PV that you want to use.

2. Create your deployment.
    ```sh
    <containers>kubectl</containers><openshift>oc</openshift> apply -f deployment.yaml
    ```
    {: pre}

3. Verify that the PV is successfully mounted to your app.
    ```sh
    <containers>kubectl</containers><openshift>oc</openshift> describe deployment <deployment_name>
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

4. Verify that you can write data to your Portworx cluster.
    1. Log in to the pod that mounts your PV.
        ```sh
        <containers>kubectl</containers><openshift>oc</openshift> exec <pod_name> -it bash
        ```
        {: pre}

    2. Navigate to your volume mount path that you defined in your app deployment.
    3. Create a text file.
        ```sh
        echo "This is a test" > test.txt
        ```
        {: pre}

    4. Read the file that you created.
        ```sh
        cat test.txt
        ```
        {: pre}





