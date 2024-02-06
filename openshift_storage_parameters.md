---

copyright:
  years: 2014, 2024
lastupdated: "2024-02-06"


keywords: openshift, openshift data foundation, openshift container storage, ocs

subcollection: openshift

---


{{site.data.keyword.attribute-definition-list}}



# OpenShift Data Foundation add-on parameter reference
{: #openshift_storage_parameters}

[Classic]{: tag-classic-inf} [VPC]{: tag-vpc}

Review the following parameter reference for the OpenShift Data Foundation cluster add-on.
{: shortdesc}

You can also find the add-on parameters in the [{{site.data.keyword.redhat_openshift_notm}} clusters console](https://cloud.ibm.com/kubernetes/clusters?platformType=openshift){: external} during add-on deployment, or by running the following command and specifying the add-on version you want to use.
{: tip}

```sh
ibmcloud oc cluster addon options --addon openshift-data-foundation --version VERSION
```
{: pre}


| Parameter | Description | Default |
| --- | --- | --- |
| `name` | Specify a name for your resource that uses only lowercase letters, numbers, `-` or `.` | N/A |
| `odfDeploy` | Specify `true` to deploy the ODF resources such as storage classes, PVCs, and PVs when you enable the add-on. When set to `false`, only the add-on is deployed and you must then configure your ODF resources later via YAML configuration files. | `false` |
| `osdStorageClassName` | - [Classic]{: tag-classic-inf}: Specify `localblock`.  \n - [VPC]{: tag-vpc} Specify the name of the storage class that you want to use for your OSD devices. For **multizone clusters**, specify a metro storage class. For **single zone clusters**, Specify the name of the tiered storage class that you want to use. Example: `ibmc-vpc-block-10iops-tier`. | N/A |
| `osdSize` | Specify a size for your storage devices. Example: `250Gi`. The total storage capacity of your ODF cluster is equivalent to the `osdSize`  multiplied by the `numOfOsd`. | `250Gi` |
| `numOfOsd` | Specify the number of object storage daemons (OSDs) that you want to create. ODF creates three times the specified number. For example, if you Specify `1`, ODF creates 3 OSDs. | `1` |
| `osdDevicePaths` | [Classic]{: tag-classic-inf} Specify a comma separated list of the device paths for the devices that you want to use for the OSD devices. The devices that you specify are used as your application storage in your configuration. Each device must have at least `100GiB` of space and must be unformatted and unmounted. The parameter format is `/dev/disk/by-id/<device-id>`. Example device path value for a partitioned device: `/dev/disk/by-id/scsi-0000000a00a00a00000a0aa000a00a0a0-part2`. If you specify more than one device path, be sure there are no spaces between each path. For example: `/dev/disk/by-id/scsi-1111111a11a11a11111a1aa111a11a1a1-part2`,`/dev/disk/by-id/scsi-0000000a00a00a00000a0aa000a00a0a0-part2`. | N/A |
| `billingType` | Specify a `billingType` of either `essentials` or `advanced` for your OCS deployment. For more information about billing type, see [Feature support by billing type](/docs/openshift?topic=openshift-ocs-storage-prep&interface=cli#odf-essentials-vs-advanced). | `advanced` |
| `autoDiscoverDevices` | [Classic]{: tag-classic-inf} **Optional**: Specify `true` to automatically discover the available disks on your worker nodes.| `false` |
| `ocsUpgrade` | Specify `true` to upgrade the major version of your ODF deployment. | `false` |
| `workerNodes` | **Optional**: Specify the names of the worker nodes that you want to use for your ODF deployment. Don't specify this parameter if you want to use all the worker nodes in your cluster. To retrieve your worker node name, run the **`oc get nodes`** command. | N/A |
| `clusterEncryption` | Specify `true` to enable encryption. | `false` |
| `hpcsServiceName` | Specify the name of your {{site.data.keyword.hscrypto}} or {{site.data.keyword.keymanagementserviceshort}} instance. For example: `Hyper-Protect-Crypto-Services-eugb`. | `false` |
| `hpcsInstanceId` | Specify your {{site.data.keyword.hscrypto}} or {{site.data.keyword.keymanagementserviceshort}} instance ID. For example: `d11a1a43-aa0a-40a3-aaa9-5aaa63147aaa`. | N/A |
| `hpcsSecretName` | Specify the name of the secret that you created by using your {{site.data.keyword.hscrypto}} or {{site.data.keyword.keymanagementserviceshort}} credentials. For example: `ibm-hpcs-secret`. | N/A |
| `hpcsBaseUrl` | Specify the public or private endpoint of your {{site.data.keyword.hscrypto}} or {{site.data.keyword.keymanagementserviceshort}} instance. For example: `https://api.eu-gb.hs-crypto.cloud.ibm.com:8389`. | N/A |
| `hpcsTokenUrl` | Specify `https://iam.cloud.ibm.com/identity/token`. | N/A |
| `encryptionInTransit` | [4.13 and later]{: tag-cool-gray} Specify `true` to enable in-transit encryption. Enabling in-transit encryption does not affect the existing mapped or mounted volumes. After a volume is mapped/mounted, it retains the encryption settings that were used when it was initially mounted. To change the encryption settings for existing volumes, they must be remounted again one-by-one. | `false` |
| `ignore-noobaa` | [4.13 and later]{: tag-cool-gray} Specify `true` if you do not want to deploy MultiCloud Object Gateway. | `false` |
| `disableNoobaaLB` | [4.14 and later]{: tag-warm-gray} Specify `true` to disable to NooBaa public load balancer. | `false` |
| `taintNodes` | [4.14 and later]{: tag-warm-gray} Specify `true` to taint the selected worker nodes so that only OpenShift Data Foundation pods can run on those nodes. Use this option only if you limit ODF to a subset of nodes in your cluster. | `false` |
| `addSingleReplicaPool` | [4.14 and later]{: tag-warm-gray} Specify `true` to create a single replica pool without data replication, increasing the risk of data loss, data corruption, and potential system instability. | `false` |
| `prepareForDisasterRecovery` | [4.14 and later]{: tag-warm-gray} Specify `true` to set up the storage system for disaster recovery service with the essential configurations in place. This allows seamless implementation of disaster recovery strategies for your workloads. | `false` |
{: caption="OpenShift Data Foundation add-on parameter reference" caption-side="bottom"}


