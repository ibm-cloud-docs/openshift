---

copyright:
  years: 2014, 2022
lastupdated: "2022-02-28"

keywords: openshift

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}

# Installing the {{site.data.keyword.cos_full_notm}} plug-in
{: #storage_cos_install}

Install the {{site.data.keyword.cos_full_notm}} plug-in with a Helm chart to set up pre-defined storage classes for {{site.data.keyword.cos_full_notm}}. You can use these storage classes to create a PVC to provision {{site.data.keyword.cos_full_notm}} for your apps.
{: shortdesc}

Looking for instructions for how to update or remove the {{site.data.keyword.cos_full_notm}} plug-in? See [Updating the plug-in](#update_cos_plugin) and [Removing the plug-in](#remove_cos_plugin).
{: tip}

The {{site.data.keyword.cos_full_notm}} plug-in requires at least 0.2 vCPU and 128 MB of memory.
{: note}

Before you begin: [Access your {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-access_cluster).

To install the `ibmc` Helm plug-in and the `ibm-object-storage-plugin`:

1. Make sure that your worker node applies the latest patch for your minor version to run your worker node with the latest security settings. The patch version also ensures that the root password on the worker node is renewed. 

    If you did not apply updates or reload your worker node within the last 90 days, your root password on the worker node expires and the installation of the storage plug-in might fail. 
    {: note}

    1. List the current patch version of your worker nodes.
        ```sh
        ibmcloud oc worker ls --cluster <cluster_name_or_ID>
        ```
        {: pre}

        Example output
        ```sh
        OK
        ID                                                  Public IP        Private IP     Machine Type           State    Status   Zone    Version
        kube-dal10-crb1a23b456789ac1b20b2nc1e12b345ab-w26   169.xx.xxx.xxx    10.xxx.xx.xxx   b3c.4x16.encrypted     normal   Ready    dal10   1.22.7_1523*
        ```
        {: screen}

        If your worker node does not apply the latest patch version, you see an asterisk (`*`) in the **Version** column of your CLI output.

    2. Review the [version changelog](/docs/containers?topic=containers-changelog) to find the changes that are in the latest patch version.

    3. Apply the latest patch version by reloading your worker node. Follow the instructions in the [ibmcloud oc worker reload command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_reload) to gracefully reschedule any running pods on your worker node before you reload your worker node. Note that during the reload, your worker node machine is updated with the latest image and data is deleted if not [stored outside the worker node](/docs/openshift?topic=openshift-storage_planning#persistent_storage_overview).
1. Review the changelog and verify support for your [cluster version and architecture](/docs/containers?topic=containers-cos_plugin_changelog).
2. [Follow the instructions](/docs/openshift?topic=openshift-helm#install_v3) to install the version 3 Helm client on your local machine.

    If you enabled [VRF](/docs/account?topic=account-vrf-service-endpoint#vrf) and [service endpoints](/docs/account?topic=account-vrf-service-endpoint#service-endpoint) in your {{site.data.keyword.cloud_notm}} account, you can use the private {{site.data.keyword.cloud_notm}} Helm repository to keep your image pull traffic on the private network. If you can't enable VRF or service endpoints in your account, use the public Helm repository.
    {: note}

3. Add the {{site.data.keyword.cloud_notm}} Helm repo to your cluster.

    ```sh
    helm repo add ibm-helm https://raw.githubusercontent.com/IBM/charts/master/repo/ibm-helm
    ```
    {: pre}

4. Update the Helm repo to retrieve the most recent version of all Helm charts in this repo.
    ```sh
    helm repo update
    ```
    {: pre}

5. If you installed the {{site.data.keyword.cos_full_notm}} Helm plug-in earlier, remove the `ibmc` plug-in.
    ```sh
    helm plugin uninstall ibmc
    ```
    {: pre}

6. Download the Helm charts and unpack the charts in your current directory.

    ```sh
    helm fetch --untar ibm-helm/ibm-object-storage-plugin
    ```
    {: pre}

    If the output shows `Error: failed to untar: a file or directory with the name ibm-object-storage-plugin already exists`, delete your `ibm-object-storage-plugin` directory and rerun the `helm fetch` command.
    {: tip}

7. If you use OS X or a Linux distribution, install the {{site.data.keyword.cos_full_notm}} Helm plug-in `ibmc`. The plug-in automatically retrieves your cluster location and to set the API endpoint for your {{site.data.keyword.cos_full_notm}} buckets in your storage classes. If you use Windows as your operating system, continue with the next step.
    1. Install the Helm plug-in.
        ```sh
        helm plugin install ./ibm-object-storage-plugin/helm-ibmc
        ```
        {: pre}

    2. Verify that the `ibmc` plug-in is installed successfully.
        ```sh
        helm ibmc --help
        ```
        {: pre}

        If the output shows the error `Error: fork/exec /home/iksadmin/.helm/plugins/helm-ibmc/ibmc.sh: permission denied`, run `chmod 755 /Users/<user_name>/Library/helm/plugins/helm-ibmc/ibmc.sh`. Then, rerun `helm ibmc --help`.
        {: tip}

        Example output

        ```sh
        helm version: v3.2.4+g0ad800e
        Install or upgrade Helm charts in IBM K8S Service(IKS) and IBM Cloud Private(ICP)
        Usage:
            helm ibmc [command]
        Available Commands:
            install           Install a Helm chart
            upgrade           Upgrade the release to a new version of the Helm chart
        Available Flags:
            -h, --help        (Optional) This text.
            -u, --update      (Optional) Update this plugin to the latest version
        Example Usage:
            Install: helm ibmc install ibm-object-storage-plugin ibm-helm/ibm-object-storage-plugin
            Upgrade: helm ibmc upgrade [RELEASE] ibm-helm/ibm-object-storage-plugin
        Note:
            1. It is always recommended to install latest version of ibm-object-storage-plugin chart.
            2. It is always recommended to have 'kubectl' client up-to-date.
        ```
        {: screen}

8. Optional: Limit the {{site.data.keyword.cos_full_notm}} plug-in to access only the Kubernetes secrets that hold your {{site.data.keyword.cos_full_notm}} service credentials. By default, the plug-in can access all Kubernetes secrets in your cluster.
    1. [Create your {{site.data.keyword.cos_full_notm}} service instance](/docs/openshift?topic=openshift-storage-cos-understand#create_cos_service).
    2. [Store your {{site.data.keyword.cos_full_notm}} service credentials in a Kubernetes secret](/docs/openshift?topic=openshift-storage-cos-understand#create_cos_secret)).
    3. From the `ibm-object-storage-plugin`, navigate to the `templates` directory and list available files.
        **OS X and Linux**

        ```sh
        cd templates && ls
        ```
        {: pre}

        **Windows**

        ```sh
        chdir templates && dir
        ```
        {: pre}

    4. Open the `provisioner-sa.yaml` file and look for the `ibmcloud-object-storage-secret-reader` `ClusterRole` definition.
    5. Add the name of the secret that you created earlier to the list of secrets that the plug-in is authorized to access in the `resourceNames` section.
        ```yaml
        kind: ClusterRole
        apiVersion: rbac.authorization.k8s.io/v1beta1
        metadata:
         name: ibmcloud-object-storage-secret-reader
        rules:
        - apiGroups: [""]
          resources: ["secrets"]
          resourceNames: ["<secret_name1>","<secret_name2>"]
          verbs: ["get"]
        ```
        {: codeblock}

    6. Save your changes and navigate to your working directory.


9. Install the `ibm-object-storage-plugin` in your cluster. When you install the plug-in, pre-defined storage classes are added to your cluster. If you completed the previous step for limiting the {{site.data.keyword.cos_full_notm}} plug-in to access only the Kubernetes secrets that hold your {{site.data.keyword.cos_full_notm}} service credentials and you are still targeting the `templates` directory, change directories to your working directory. **VPC clusters only**: To enable authorized IPs on VPC, set the `--set bucketAccessPolicy=true` flag.

Example `helm ibmc install` command for OS X and Linux.

```sh
helm ibmc install ibm-object-storage-plugin ibm-helm/ibm-object-storage-plugin --set license=true [--set bucketAccessPolicy=false]
```
{: pre}

Example `helm install` command for Windows.

```sh
helm install ibm-object-storage-plugin ./ibm-object-storage-plugin --set dcname="${DC_NAME}" --set provider="${CLUSTER_PROVIDER}" --set workerOS="${WORKER_OS}" --region="${REGION} --set platform="${PLATFORM}" --set license=true [--set bucketAccessPolicy=false]
```
{: pre}


`DC_NAME`
:   The cluster data center. To retrieve the data center, run `oc get cm cluster-info -n kube-system -o jsonpath="{.data.cluster-config\.json}{'\n'}"`. Store the data center value in an environment variable by running `SET DC_NAME=<datacenter>`. Optional: Set the environment variable in Windows PowerShell by running `$env:DC_NAME="<datacenter>"`.

`CLUSTER_PROVIDER`
:   The infrastructure provider. To retrieve this value, run `oc get nodes -o jsonpath="{.items[*].metadata.labels.ibm-cloud\.kubernetes\.io\/iaas-provider}{'\n'}"`. If the output from the previous step contains `softlayer`, then set the `CLUSTER_PROVIDER` to `"IBMC"`. If the output contains `gc`, `ng`, or `g2`, then set the `CLUSTER_PROVIDER` to `"IBMC-VPC"`. Store the infrastructure provider in an environment variable. For example: `SET CLUSTER_PROVIDER="IBMC-VPC"`.

`WORKER_OS` and `PLATFORM`
:   The operating system of the worker nodes. To retrieve these values, run `oc get nodes -o jsonpath="{.items[*].metadata.labels.ibm-cloud\.kubernetes\.io\/os}{'\n'}"`. Store the operating system of the worker nodes in an environment variable. For {{site.data.keyword.openshiftlong_notm}} clusters, run `SET WORKER_OS="redhat"` and `SET PLATFORM="openshift"`. 

`REGION`
:   The region of the worker nodes. To retrieve this value, run `oc get nodes -o yaml | grep 'ibm-cloud\.kubernetes\.io/region'`. Store the region of the worker nodes in an environment variable by running `SET REGION="< region>"`.

## Updating the {{site.data.keyword.cos_full_notm}} plug-in
{: #update_cos_plugin}

You can upgrade the existing {{site.data.keyword.cos_full_notm}} plug-in to the most recent version.
{: shortdesc}


1. Get the name of your {{site.data.keyword.cos_full_notm}} plug-in Helm release and the version of the plug-in in your cluster.

    ```sh
    helm ls -A | grep object
    ```
    {: pre}

    Example output

    ```sh
    NAME              NAMESPACE      REVISION    UPDATED                                   STATUS      CHART                                  APP VERSION               
    <release_name>  <namespace>     1           2020-02-13 16:05:58.599679 -0500 EST    deployed    ibm-object-storage-plugin-1.1.2        1.1.2
    ```
    {: screen}

1. Follow the steps in [Installing the {{site.data.keyword.cos_full_notm}} plug-in](/docs/containers?topic=containers-storage_cos_install) to install the latest version of the {{site.data.keyword.cos_full_notm}} plug-in.

1. Update the {{site.data.keyword.cloud_notm}} Helm repo to retrieve the most recent version of all Helm charts in this repo.

    ```sh
    helm repo update
    ```
    {: pre}

1. Update the {{site.data.keyword.cos_full_notm}} `ibmc` Helm plug-in to the most recent version.

    ```sh
    helm ibmc --update
    ```
    {: pre}

1. Install the most recent version of the `ibm-object-storage-plugin` for your operating system.

  Example `helm ibmc install` command for OS X and Linux.

    ```sh
    helm ibmc install ibm-object-storage-plugin ibm-helm/ibm-object-storage-plugin --set license=true [--set bucketAccessPolicy=false]
    ```
    {: pre}

  Example `helm install` command for Windows.

    ```sh
    helm install ibm-object-storage-plugin ./ibm-object-storage-plugin --set dcname="${DC_NAME}" --set provider="${CLUSTER_PROVIDER}" --set workerOS="${WORKER_OS}" --region="${REGION} --set platform="${PLATFORM}" --set license=true [--set bucketAccessPolicy=false]
    ```
    {: pre}

    `DC_NAME`
    :   The cluster data center. To retrieve the data center, run `oc get cm cluster-info -n kube-system -o jsonpath="{.data.cluster-config\.json}{'\n'}"`. Store the data center value in an environment variable by running `SET DC_NAME=<datacenter>`. Optional: Set the environment variable in Windows PowerShell by running `$env:DC_NAME="<datacenter>"`.

    `CLUSTER_PROVIDER`
    :   The infrastructure provider. To retrieve this value, run `oc get nodes -o jsonpath="{.items[*].metadata.labels.ibm-cloud\.kubernetes\.io\/iaas-provider}{'\n'}"`. If the output from the previous step contains `softlayer`, then set the `CLUSTER_PROVIDER` to `"IBMC"`. If the output contains `gc`, `ng`, or `g2`, then set the `CLUSTER_PROVIDER` to `"IBMC-VPC"`. Store the infrastructure provider in an environment variable. For example: `SET CLUSTER_PROVIDER="IBMC-VPC"`.

    `WORKER_OS` and `PLATFORM`
    :   The operating system of the worker nodes. To retrieve these values, run `oc get nodes -o jsonpath="{.items[*].metadata.labels.ibm-cloud\.kubernetes\.io\/os}{'\n'}"`. Store the operating system of the worker nodes in an environment variable. For {{site.data.keyword.openshiftlong_notm}} clusters, run `SET WORKER_OS="redhat"` and `SET PLATFORM="openshift"`. 

    `REGION`
    :   The region of the worker nodes. To retrieve this value, run `oc get nodes -o yaml | grep 'ibm-cloud\.kubernetes\.io/region'`. Store the region of the worker nodes in an environment variable by running `SET REGION="< region>"`. |

1. Verify that the `ibmcloud-object-storage-plugin` is successfully upgraded. The upgrade of the plug-in is successful when you see `deployment "ibmcloud-object-storage-plugin" successfully rolled out` in your CLI output.

    ```sh
    oc rollout status deployment/ibmcloud-object-storage-plugin -n ibm-object-s3fs
    ```
    {: pre}

1. Verify that the `ibmcloud-object-storage-driver` is successfully upgraded. The upgrade is successful when you see `daemon set "ibmcloud-object-storage-driver" successfully rolled out` in your CLI output.

    ```sh
    oc rollout status ds/ibmcloud-object-storage-driver -n ibm-object-s3fs
    ```
    {: pre}

1. Verify that the {{site.data.keyword.cos_full_notm}} pods are in a `Running` state.

    ```sh
    oc get pods -n <namespace> -o wide | grep object-storage
    ```
    {: pre}

If you're having trouble updating the {{site.data.keyword.cos_full_notm}} plug-in, see [Object storage: Installing the Object storage `ibmc` Helm plug-in fails](/docs/containers?topic=containers-cos_helm_fails) and [Object storage: Installing the {{site.data.keyword.cos_full_notm}} plug-in fails](/docs/containers?topic=containers-cos_plugin_fails).
{: tip}

## Removing the {{site.data.keyword.cos_full_notm}} plug-in
{: #remove_cos_plugin}

If you don't want to provision and use {{site.data.keyword.cos_full_notm}} in your cluster, you can uninstall the `ibm-object-storage-plugin` and the `ibmc` Helm plug-in.
{: shortdesc}

Removing the `ibmc` Helm plug-in or the `ibm-object-storage-plugin` doesn't remove existing PVCs, PVs, data. When you remove the `ibm-object-storage-plugin`, all the related pods and daemon sets are removed from your cluster. You can't provision new {{site.data.keyword.cos_full_notm}} for your cluster or use existing PVCs and PVs after you remove the plug-in, unless you configure your app to use the {{site.data.keyword.cos_full_notm}} API directly.
{: important}

Before you begin:

- [Access your {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-access_cluster).
- Make sure that you don't have any PVCs or PVs in your cluster that use {{site.data.keyword.cos_full_notm}}. To list all pods that mount a specific PVC, run `oc get pods --all-namespaces -o=jsonpath='{range .items[*]}{"\n"}{.metadata.name}{":\t"}{range .spec.volumes[*]}{.persistentVolumeClaim.claimName}{" "}{end}{end}' | grep "<pvc_name>"`.

To remove the `ibmc` Helm plug-in and the `ibm-object-storage-plugin`:

1. Get the name of your `ibm-object-storage-plugin` Helm installation.

    ```sh
    helm ls -A | grep ibm-object-storage-plugin
    ```
    {: pre}

    Example output

    ```sh
    NAME                         NAMESPACE    REVISION    UPDATED                                 STATUS      CHART                                  APP VERSION               
    ibm-object-storage-plugin    default      2           2020-04-01 08:46:01.403477 -0400 EDT    deployed    ibm-object-storage-plugin-1.1.4        1.1.4  
    ```
    {: screen}

2. Uninstall the `ibm-object-storage-plugin`.

    ```sh
    helm uninstall <release_name>
    ```
    {: pre}

    Example command for a release named `ibm-object-storage-plugin`.

    ```sh
    helm uninstall ibm-object-storage-plugin
    ```
    {: pre}

3. Verify that the `ibm-object-storage-plugin` pods are removed.

    ```sh
    oc get pod -n <namespace> | grep object-storage
    ```
    {: pre}

    The removal of the pods is successful if no pods are displayed in your CLI output. The removal of the storage classes is successful if no storage classes are displayed in your CLI output.

4. Verify that the storage classes are removed.

    ```sh
    oc get storageclasses | grep s3
    ```
    {: pre}

5. If you use OS X or a Linux distribution, remove the `ibmc` Helm plug-in. If you use Windows, this step is not required.

    1. Remove the `ibmc` Helm plug-in.

        ```sh
        helm plugin uninstall ibmc
        ```
        {: pre}

    2. Verify that the `ibmc` plug-in is removed. The `ibmc` plug-in is removed successfully if the `ibmc` plug-in is not listed in your CLI output.

        ```sh
        helm plugin list
        ```
        {: pre}

        Example output

        ```sh
        NAME    VERSION    DESCRIPTION
        ```
        {: screen}

## Deciding on the object storage configuration
{: #configure_cos}

{{site.data.keyword.openshiftlong_notm}} provides pre-defined storage classes that you can use to create buckets with a specific configuration.
{: shortdesc}

1. List available storage classes in {{site.data.keyword.openshiftlong_notm}}.

    ```sh
    oc get storageclasses | grep s3
    ```
    {: pre}

    Example output

    ```sh
    ibmc-s3fs-cold-cross-region            ibm.io/ibmc-s3fs   8m
    ibmc-s3fs-cold-regional                ibm.io/ibmc-s3fs   8m
    ibmc-s3fs-flex-cross-region            ibm.io/ibmc-s3fs   8m
    ibmc-s3fs-flex-perf-cross-region       ibm.io/ibmc-s3fs   8m
    ibmc-s3fs-flex-perf-regional           ibm.io/ibmc-s3fs   8m
    ibmc-s3fs-flex-regional                ibm.io/ibmc-s3fs   8m
    ibmc-s3fs-standard-cross-region        ibm.io/ibmc-s3fs   8m
    ibmc-s3fs-standard-perf-cross-region   ibm.io/ibmc-s3fs   8m
    ibmc-s3fs-standard-perf-regional       ibm.io/ibmc-s3fs   8m
    ibmc-s3fs-standard-regional            ibm.io/ibmc-s3fs   8m
    ibmc-s3fs-vault-cross-region           ibm.io/ibmc-s3fs   8m
    ibmc-s3fs-vault-regional               ibm.io/ibmc-s3fs   8m
    ```
    {: screen}

2. Choose a storage class that fits your data access requirements. The storage class determines the [pricing](https://cloud.ibm.com/objectstorage/create#pricing){: external} for storage capacity, read and write operations, and outbound bandwidth for a bucket. The option that is right for you is based on how frequently data is read and written to your service instance.
    - **Standard**: This option is used for hot data that is accessed frequently. Common use cases are web or mobile apps.
    - **Vault**: This option is used for workloads or cool data that are accessed infrequently, such as once a month or less. Common use cases are archives, short-term data retention, digital asset preservation, tape replacement, and disaster recovery.
    - **Cold**: This option is used for cold data that is rarely accessed (every 90 days or less), or inactive data. Common use cases are archives, long-term backups, historical data that you keep for compliance, or workloads and apps that are rarely accessed.
    - **Flex**: This option is used for workloads and data that don't follow a specific usage pattern, or that are too huge to determine or predict a usage pattern. **Tip:** Check out this [blog](https://www.ibm.com/blogs/cloud-archive/2017/03/interconnect-2017-changing-rules-storage/){: external} to learn how the Flex storage class works compared to traditional storage tiers.   

3. Decide on the level of resiliency for the data that is stored in your bucket.
    - **Cross-region**: With this option, your data is stored across three regions within a geolocation for highest availability. If you have workloads that are distributed across regions, requests are routed to the nearest regional endpoint. The API endpoint for the geolocation is automatically set by the `ibmc` Helm plug-in that you installed earlier based on the location that your cluster is in. For example, if your cluster is in `US South`, then your storage classes are configured to use the `US GEO` API endpoint for your buckets. For more information, see [Regions and endpoints](/docs/cloud-object-storage/basics?topic=cloud-object-storage-endpoints#endpoints).  
    - **Regional**: With this option, your data is replicated across multiple zones within one region. If you have workloads that are located in the same region, you see lower latency and better performance than in a cross-regional setup. The regional endpoint is automatically set by the `ibm` Helm plug-in that you installed earlier based on the location that your cluster is in. For example, if your cluster is in `US South`, then your storage classes were configured to use `US South` as the regional endpoint for your buckets. For more information, see [Regions and endpoints](/docs/cloud-object-storage/basics?topic=cloud-object-storage-endpoints#endpoints).

4. Review the detailed {{site.data.keyword.cos_full_notm}} bucket configuration for a storage class.

    ```sh
    oc describe storageclass <storageclass_name>
    ```
    {: pre}

    Example output

    ```sh
    Name:                  ibmc-s3fs-standard-cross-region
    IsDefaultClass:        No
    Annotations:           <none>
    Provisioner:           ibm.io/ibmc-s3fs
    Parameters:            ibm.io/chunk-size-mb=16,ibm.io/curl-debug=false,ibm.io/debug-level=warn,ibm.io/iam-endpoint=https://iam.bluemix.net,ibm.io/kernel-cache=true,ibm.io/multireq-max=20,ibm.io/object-store-endpoint=https://s3-api.dal-us-geo.objectstorage.service.networklayer.com,ibm.io/object-store-storage-class=us-standard,ibm.io/parallel-count=2,ibm.io/s3fs-fuse-retry-count=5,ibm.io/stat-cache-size=100000,ibm.io/tls-cipher-suite=AESGCM
    AllowVolumeExpansion:  <unset>
    MountOptions:          <none>
    ReclaimPolicy:         Delete
    VolumeBindingMode:     Immediate
    Events:                <none>
    ```
    {: screen}


    `ibm.io/chunk-size-mb`
    :   The size of a data chunk that is read from or written to {{site.data.keyword.cos_full_notm}} in megabytes. Storage classes with `perf` in their name are set up with 52 megabytes. Storage classes without `perf` in their name use 16 megabyte chunks. For example, if you want to read a file that is `1GB`, the plug-in reads this file in multiple 16 or 52-megabyte chunks.
    
    `ibm.io/curl-debug`
    :   Enable the logging of requests that are sent to the {{site.data.keyword.cos_full_notm}} service instance. If enabled, logs are sent to `syslog` and you can [forward the logs to an external logging server](/docs/containers?topic=containers-health#logging). By default, all storage classes are set to `false` to disable this logging feature.
    
    `ibm.io/debug-level`
    :   The logging level that is set by the {{site.data.keyword.cos_full_notm}} plug-in. All storage classes are set up with the `WARN` logging level.
    
    `ibm.io/iam-endpoint`
    :   The API endpoint for {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM). 
    
    `ibm.io/kernel-cache`
    :   Enable or disable the kernel buffer cache for the volume mount point. If enabled, data that is read from {{site.data.keyword.cos_full_notm}} is stored in the kernel cache to ensure fast read access to your data. If disabled, data is not cached and always read from {{site.data.keyword.cos_full_notm}}. Kernel cache is enabled for `standard` and `flex` storage classes, and disabled for `cold` and `vault` storage classes. 
    
    `ibm.io/multireq-max`
    :   The maximum number of parallel requests that can be sent to the {{site.data.keyword.cos_full_notm}} service instance to list files in a single directory. All storage classes are set up with a maximum of 20 parallel requests.
    
    `ibm.io/object-store-endpoint`
    :   The API endpoint to use to access the bucket in your {{site.data.keyword.cos_full_notm}} service instance. The endpoint is automatically set based on the region of your cluster. If you want to access an existing bucket that is located in a different region than the one where your cluster is in, you must [create a custom storage class](/docs/openshift?topic=openshift-kube_concepts#customized_storageclass) and use the API endpoint for your bucket.
    
    `ibm.io/object-store-storage-class`
    :   The name of the storage class.
    
    `ibm.io/parallel-count`
    :   The maximum number of parallel requests that can be sent to the {{site.data.keyword.cos_full_notm}} service instance for a single read or write operation. Storage classes with `perf` in their name are set up with a maximum of 20 parallel requests. Storage classes without `perf` are set up with two parallel requests by default.
    
    `ibm.io/s3fs-fuse-retry-count`
    :   The maximum number of retries for a read or write operation before the operation is considered unsuccessful. All storage classes are set up with a maximum of five retries.
    
    `ibm.io/stat-cache-size`
    :   The maximum number of records that are kept in the {{site.data.keyword.cos_full_notm}} metadata cache. Every record can take up to 0.5 kilobytes. All storage classes set the maximum number of records to 100000 by default.
    
    `ibm.io/tls-cipher-suite`
    :   The TLS cipher suite that must be used when a connection to {{site.data.keyword.cos_full_notm}} is established via the HTTPS endpoint. The value for the cipher suite must follow the [OpenSSL format](https://www.openssl.org/docs/man1.1.1/man1/ciphers.html){: external}. If your worker nodes run an Ubuntu operating system, your storage classes are set up to use the `AESGCM`cipher suite by default. For worker nodes that run a Red Hat operating system, the `ecdhe_rsa_aes_128_gcm_sha_256` cipher suite is used by default.


    For more information about each storage class, see the [storage class reference](/docs/containers?topic=containers-storage_cos_reference). If you want to change any of the pre-set values, create your own [customized storage class](/docs/openshift?topic=openshift-kube_concepts#customized_storageclass).
    {: tip}

5. Decide on a name for your bucket. The name of a bucket must be unique in {{site.data.keyword.cos_full_notm}}. You can also choose to automatically create a name for your bucket by the {{site.data.keyword.cos_full_notm}} plug-in. To organize data in a bucket, you can create subdirectories.

    The storage class that you chose earlier determines the pricing for the entire bucket. You can't define different storage classes for subdirectories. If you want to store data with different access requirements, consider creating multiple buckets by using multiple PVCs.
    {: note}

6. Choose if you want to keep your data and the bucket after the cluster or the persistent volume claim (PVC) is deleted. When you delete the PVC, the PV is always deleted. You can choose if you want to also automatically delete the data and the bucket when you delete the PVC. Your {{site.data.keyword.cos_full_notm}} service instance is independent from the retention policy that you select for your data and is never removed when you delete a PVC.

Now that you decided on the configuration that you want, you are ready to [create a PVC](/docs/containers?topic=containers-storage_cos_apps) to provision {{site.data.keyword.cos_full_notm}}.


## Verifying your installation
{: #cos-plugin verify}

Review the pod details to verify that the plug-in installation succeeded.
{: shortdesc}

1. Verify the installation succeeded by listing the driver pods.

    ```sh
    oc get pod --all-namespaces -o wide | grep object
    ```
    {: pre}

    Example output

    ```sh
    ibmcloud-object-storage-driver-9n8g8                              1/1       Running   0          2m
    ibmcloud-object-storage-plugin-7c774d484b-pcnnx                   1/1       Running   0          2m
    ```
    {: screen}

    The installation is successful when you see one `ibmcloud-object-storage-plugin` pod and one or more `ibmcloud-object-storage-driver` pods. The number of `ibmcloud-object-storage-driver` pods equals the number of worker nodes in your cluster. All pods must be in a `Running` state for the plug-in to function properly. If the pods fail, run `oc describe pod -n ibm-object-s3fs <pod_name>` to find the root cause for the failure.

1. Verify that the storage classes are created successfully.

    ```sh
    oc get storageclass | grep s3
    ```
    {: pre}

    Example output

    ```sh
    ibmc-s3fs-cold-cross-region            ibm.io/ibmc-s3fs   8m
    ibmc-s3fs-cold-regional                ibm.io/ibmc-s3fs   8m
    ibmc-s3fs-flex-cross-region            ibm.io/ibmc-s3fs   8m
    ibmc-s3fs-flex-perf-cross-region       ibm.io/ibmc-s3fs   8m
    ibmc-s3fs-flex-perf-regional           ibm.io/ibmc-s3fs   8m
    ibmc-s3fs-flex-regional                ibm.io/ibmc-s3fs   8m
    ibmc-s3fs-standard-cross-region        ibm.io/ibmc-s3fs   8m
    ibmc-s3fs-standard-perf-cross-region   ibm.io/ibmc-s3fs   8m
    ibmc-s3fs-standard-perf-regional       ibm.io/ibmc-s3fs   8m
    ibmc-s3fs-standard-regional            ibm.io/ibmc-s3fs   8m
    ibmc-s3fs-vault-cross-region           ibm.io/ibmc-s3fs   8m
    ibmc-s3fs-vault-regional               ibm.io/ibmc-s3fs   8m
    ```
    {: screen}

    If you want to set one of the {{site.data.keyword.cos_full_notm}} storage classes as your default storage class, run `oc patch storage class <storageclass> -p '{"metadata": {"annotations":{"storageclass.kubernetes.io/is-default-class":"true"}}}'`. Replace `<storageclass>` with the name of the {{site.data.keyword.cos_full_notm}} storage class.
    {: tip}

1. Follow the instructions to [add object storage to your apps](/docs/containers?topic=containers-storage_cos_apps).

If you're having trouble installing the {{site.data.keyword.cos_full_notm}} plug-in, see [Object storage: Installing the Object storage `ibmc` Helm plug-in fails](/docs/containers?topic=containers-cos_helm_fails) and [Object storage: Installing the {{site.data.keyword.cos_full_notm}} plug-in fails](/docs/containers?topic=containers-cos_plugin_fails).
{: tip}


