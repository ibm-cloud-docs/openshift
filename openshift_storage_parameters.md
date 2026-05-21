---

copyright:
  years: 2014, 2026
lastupdated: "2026-05-21"


keywords: openshift, openshift data foundation, openshift container storage, ocs

subcollection: openshift

---


{{site.data.keyword.attribute-definition-list}}



# OpenShift Data Foundation add-on parameter reference
{: #openshift_storage_parameters}

[Classic]{: tag-classic-inf} [VPC]{: tag-vpc}

Review the following parameter reference for the OpenShift Data Foundation cluster add-on.
{: shortdesc}

You can also find the add-on parameters in the [console](https://cloud.ibm.com/containers/cluster-management/clusters){: external} during add-on deployment, or by running the following command and specifying the add-on version you want to use.
{: tip}

```sh
ibmcloud oc cluster addon options --addon openshift-data-foundation --version VERSION
```
{: pre}


| Parameter | Description | Default | Editable after deployment |
| --- | --- | --- | --- |
| `name` | Specify a name for your resource that uses only lowercase letters, numbers, `-` or `.` | N/A | Yes |
| `odfDeploy` | Specify `true` to deploy the ODF resources such as storage classes, PVCs, and PVs when you enable the add-on. When set to `false`, only the add-on is deployed and you must then configure your ODF resources later via YAML configuration files. | `false` | Yes |
| `osdStorageClassName` | - [Classic]{: tag-classic-inf}: Specify `localblock`.  \n - [VPC]{: tag-vpc} Specify the name of the storage class that you want to use for your OSD devices. For multizone clusters, specify a metro storage class. For single zone clusters, Specify the name of the tiered storage class that you want to use. Example: `ibmc-vpc-block-10iops-tier`. | N/A | Yes |
| `osdSize` | Specify a size for your storage devices. Example: `512Gi`. The total storage capacity of your ODF cluster is equivalent to the `osdSize`  multiplied by the `numOfOsd`. | `512Gi` | Yes |
| `numOfOsd` | Specify the number of Object Storage Daemons (OSDs) to create. For multizone clusters, OpenShift Data Foundation creates three times the specified value to distribute OSDs across zones for high availability. For example, specifying `1` creates 3 OSDs. For single-zone clusters, the specified value is used directly. For example, specifying `1` creates 1 OSD. | `1` | Yes |
| `autoDiscoverDevices` | [Classic]{: tag-classic-inf} Specify `true` to automatically discover the available disks on your worker nodes.| `true` | Yes |
| `osdDevicePaths` | [Classic]{: tag-classic-inf} Specify a comma separated list of the device paths for the devices that you want to use for the OSD devices. The devices that you specify are used as your application storage in your configuration. Each device must have at least `100GiB` of space and must be unformatted and unmounted. The parameter format is `/dev/disk/by-id/<device-id>`. Example device path value for a partitioned device: `/dev/disk/by-id/scsi-0000000a00a00a00000a0aa000a00a0a0-part2`. If you specify more than one device path, be sure there are no spaces between each path. For example: `/dev/disk/by-id/scsi-1111111a11a11a11111a1aa111a11a1a1-part2`,`/dev/disk/by-id/scsi-0000000a00a00a00000a0aa000a00a0a0-part2`. | N/A | Yes |
| `billingType` | Specify a `billingType` of either `essentials` or `advanced` for your deployment. For more information about billing type, see [Feature support by billing type](/docs/openshift?topic=openshift-ocs-storage-prep&interface=cli#odf-essentials-vs-advanced). | `advanced` | Yes |
| `ocsUpgrade` | Specify `true` to upgrade the major version of your ODF deployment. | `false` | Yes |
| `workerPool` | Specify one of `workerPool` or `workerNodes`. Specify either the name or the ID of a worker pool to use for ODF.  Don't specify this option if you want to use all the worker nodes in your cluster. To retrieve your worker node name, run the **`ibmcloud oc worker ls -C CLUSTER`** command. | N/A | Yes |
| `workerNodes` | Specify one of `workerPool` or `workerNodes`. Specify the names of the worker nodes that you want to use for your ODF deployment. Don't specify this option if you want to use all the worker nodes in your cluster. To retrieve your worker node name, run the **`oc get nodes`** command. | N/A | Yes |
| `clusterEncryption` | **Optional**: Specify `true` to enable encryption. | `false` | No |
| `hpcsServiceName` | **Optional**: Specify the name of your {{site.data.keyword.hscrypto}} or {{site.data.keyword.keymanagementserviceshort}} instance. For example: `Hyper-Protect-Crypto-Services-eugb`. | `false` | Yes |
| `hpcsInstanceId` | **Optional**: Specify your {{site.data.keyword.hscrypto}} or {{site.data.keyword.keymanagementserviceshort}} instance ID. For example: `d11a1a43-aa0a-40a3-aaa9-5aaa63147aaa`. | N/A | Yes |
| `hpcsSecretName` | **Optional**: Specify the name of the secret that you created by using your {{site.data.keyword.hscrypto}} or {{site.data.keyword.keymanagementserviceshort}} credentials. For example: `ibm-hpcs-secret`. | N/A | Yes |
| `hpcsBaseUrl` | **Optional**: Specify the public or private endpoint of your {{site.data.keyword.hscrypto}} or {{site.data.keyword.keymanagementserviceshort}} instance. For example: `https://api.eu-gb.hs-crypto.cloud.ibm.com:8389`. | N/A | Yes |
| `hpcsTokenUrl` | **Optional**: Specify `https://iam.cloud.ibm.com/identity/token`. | N/A | Yes |
| `encryptionInTransit` | Specify `true` to enable in-transit encryption. Enabling in-transit encryption does not affect the existing mapped or mounted volumes. After a volume is mapped/mounted, it retains the encryption settings that were used when it was initially mounted. To change the encryption settings for existing volumes, they must be remounted again one-by-one. | `false` | No |
| `ignoreNoobaa` | Specify `true` if you do not want to deploy MultiCloud Object Gateway. | `true` | No |
| `disableNoobaaLB` | Specify `true` to disable to NooBaa public load balancer. | `false` | No |
| `taintNodes` | Specify `true` to taint the selected worker nodes so that only OpenShift Data Foundation pods can run on those nodes. Use this option only if you limit ODF to a subset of nodes in your cluster. | `false` | No |
| `addSingleReplicaPool` | Specify `true` to create a single replica pool without data replication, increasing the risk of data loss, data corruption, and potential system instability. | `false` | No |
| `useCephRBDAsDefaultStorageClass` | Set the Ceph RADOS block device (RBD) storage class as the default storage class in the cluster during the deployment of OpenShift Data Foundation. Make sure that you remove the existing default storage class before setting this parameter to `true`. | `false` | Yes |
| `enableNFS` | Enabling this feature allows you to export Network File System (NFS) data that can then be accessed internally or externally from the OpenShift cluster. | `false` | Yes |
| `resourceProfile` | Specify a resource profile based on the availability of resources during deployment. Select either `lean` which requires 24 CPUs and 72GiB memory, `balanced` which requires 30 CPUs and 72 GiB memory, or `performance` which requires 45 CPUs and 96 GiB memory. | `balanced` | Yes |
| `setDefaultStorageClassForVirtualization` | [4.21 and later]{: tag-cool-gray} If enabled, the RBD virtualization StorageClass is marked as the default for KubeVirt VM disks (persistent volumes) upon installation. | `false` | Yes |
| `enableAutomaticCapacityScaling` | [4.21 and later]{: tag-cool-gray} When enabled, the system continuously monitors storage utilization. Once used capacity reaches approximately 70% of the provisioned capacity, the system automatically adds additional raw storage capacity equivalent to the originally configured deployment size. | `false` | Yes |
| `clusterExpansionLimit` | [4.21 and later]{: tag-cool-gray} Defines the maximum cluster expansion limit in cloud storage. Automatic capacity scaling is suspended if this limit is exceeded. | `12Ti` | Yes |
| `enableAutomaticBackup` | [4.21 and later]{: tag-cool-gray} Enables automatic scheduled backups for the MultiCloud Object Gateway (NooBaa) metadata database. This feature is tightly coupled with the `ignoreNoobaa` configuration. It can only be enabled when MultiCloud Object Gateway is deployed (i.e., `ignoreNoobaa = false`). | `false` | Yes |
| `backupFrequency` | [4.21 and later]{: tag-cool-gray} This parameter defines the scheduling interval for automatic backups of the MultiCloud Object Gateway metadata database. Supported scheduling options follow standard cron-like presets: `@daily` (default), `@weekly`, `@monthly`. | `@daily` | Yes |
| `numOfBackupCopies` | [4.21 and later]{: tag-cool-gray} Specifies the number of automatic backup copies retained for the MultiCloud Object Gateway metadata database. | `5` | Yes |
{: caption="OpenShift Data Foundation add-on parameter reference" caption-side="bottom"}
