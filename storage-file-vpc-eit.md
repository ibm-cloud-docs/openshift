---

copyright:
  years: 2026
lastupdated: "2026-08-03"


keywords: openshift, {{site.data.keyword.openshiftlong_notm}}, file, encryption, transit, EIT, stunnel, regional, RFS

subcollection: openshift
content-type: howto


---

{{site.data.keyword.attribute-definition-list}}


# Encryption in transit for {{site.data.keyword.filestorage_vpc_full_notm}}
{: #storage-file-vpc-eit}

[Virtual Private Cloud]{: tag-vpc}

Use encryption in transit (EIT) to protect data as it moves between your worker nodes and the {{site.data.keyword.filestorage_vpc_short}} service. This topic covers EIT for both zonal file shares that use the `dp2` profile and regional file shares that use the `rfs` profile.
{: shortdesc}

## Zonal file shares — Setting up encryption in transit
{: #vpc-file-dp2-eit}

If you choose to use encryption in transit, balance your security requirements with performance needs. Encrypting data in transit can affect performance because data must be encrypted and decrypted at the endpoints. For more information, see [VPC Encryption in Transit](/docs/vpc?topic=vpc-file-storage-vpc-about&interface=ui#fs-eit).



On RHCOS (CoreOS) worker nodes, EIT is not active until the node is rebooted after the operator installs the required packages. Plan for a rolling reboot when you enable EIT.
{: important}




- EIT is available for cluster versions 4.16 and later.
- By default, file shares are [encrypted at rest](/docs/vpc?topic=vpc-file-storage-vpc-about&interface=ui#FS-encryption) with IBM-managed encryption.
- To use EIT with Secure by Default clusters, you must add the following outbound rule to the `kube-<clusterID>` security group. This rule is added automatically for ROKS clusters at version 4.18 and later. For older cluster versions, add the rule manually.
    - **Protocol**: Any
    - **Source type**: Any
    - **Source**: `0.0.0.0/0`
    - **Destination**: `169.254.169.254`
- EIT is not available for statically provisioned volumes. To set up EIT, you must use dynamic provisioning.
- EIT packages are automatically updated in your cluster when EIT is enabled.
- Encrypting data in transit can affect performance. The impact depends on your workload characteristics. Workloads that perform synchronous writes or bypass VSI caching, such as databases, might see a substantial performance impact when EIT is enabled. To assess the impact, benchmark your workload with and without EIT.
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

1. In the configmap, set `ENABLE_EIT: "true"` and add worker pools where you want to enable EIT to the `EIT_ENABLED_WORKER_POOLS` field. For example: `"wp1,wp2"`. You can also set the `EIT_METADATA_RETRY_COUNT` and `EIT_METADATA_RETRY_INTERVAL` parameters to control retry behavior when fetching instance metadata.

    ```yaml
    apiVersion: v1
    data:
      EIT_ENABLED_WORKER_POOLS: "wp1,wp2" # Specify the worker pools where you want to enable EIT. If this field is blank, EIT is not enabled on any worker pools.
      ENABLE_EIT: "true"                   # Specify true/false
      EIT_METADATA_RETRY_COUNT: "3"        # Number of retries for fetching instance metadata before an error is returned
      EIT_METADATA_RETRY_INTERVAL: "30"    # Interval in seconds between each metadata fetch retry
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

1. After enabling EIT, save and close the configmap.

This step can take up to 5 minutes to complete as the operator installs EIT packages on the specified worker nodes.
{: note}

1. To verify EIT is enabled, review the events of the `file-csi-driver-status` configmap to confirm that EIT installation succeeded on each worker node. Look for `Package installation successful` events for each node in your specified worker pools.

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

1. If your worker pools contain RHCOS (CoreOS) nodes, drain and reboot each affected node to activate the EIT packages. EIT is not functional on RHCOS nodes until the node is rebooted. Draining the node first ensures that running workloads are rescheduled to other nodes before the reboot, avoiding impact to production apps.

    Drain the node to safely evict all running pods.

    ```sh
    oc drain <node-name> --ignore-daemonsets --delete-emptydir-data
    ```
    {: pre}

    Reboot the drained node.

    ```sh
    ibmcloud ks worker reboot --cluster CLUSTER_ID --worker WORKER_ID
    ```
    {: pre}

    After the node is back online and in `Ready` state, uncordon it to allow workloads to be scheduled on it again.

    ```sh
    oc uncordon <node-name>
    ```
    {: pre}

    

1. Select a pre-installed storage class that supports EIT or create your own storage class.

    * Create a PVC by using the `ibmc-vpc-file-eit` storage class.
    * Create your own storage class and set the `isEITEnabled` parameter to `true`.

1. Create a PVC that references the storage class you selected, then deploy an app that uses your PVC.

If you encounter issues with EIT after completing these steps, see the following troubleshooting topics:
- [Why do I see an `UnresponsiveMountHelperContainerUtility` error?](/docs/openshift?topic=openshift-ts-storage-vpc-file-eit-unresponsive)
- [Why do I see a `MetadataServiceNotEnabled` error?](/docs/openshift?topic=openshift-ts-storage-vpc-file-eit-metadata)
{: tip}

## Regional file shares — Setting up encryption in transit (Beta)
{: #vpc-file-rfs-eit}

Regional File Storage (RFS) with encryption in transit (EIT) provides secure, TLS-encrypted NFS connections for file shares across multiple availability zones within a region. The {{site.data.keyword.filestorage_vpc_short}} add-on automatically manages a stunnel sidecar on each worker node that wraps all NFS traffic in TLS 1.3 or higher, transparent to your applications.

For background on Regional File Storage, see [Regional file storage overview](/docs/vpc?topic=vpc-file-storage-vpc-about&interface=ui#regional-file-storage-overview).

RFS with EIT is available as Beta support only and is recommended for experimental use only. Do not use this feature in production workloads.
{: beta}

### How it works
{: #vpc-file-rfs-eit-how}

When you create a PVC with an RFS EIT storage class and a pod mounts it, the add-on automatically sets up an encrypted stunnel tunnel on the worker node and routes all NFS traffic through it. The encryption is transparent to your applications — they continue to use standard NFS mounts while all data in transit is protected with TLS 1.3 or higher.

The tunnel lifecycle is fully managed by the driver: it is created when a pod mounts the volume and torn down when the pod is deleted.

### Before you begin
{: #vpc-file-rfs-eit-prereqs}

- The {{site.data.keyword.filestorage_vpc_short}} add-on **version 2.0 or later** is installed on your cluster. For more information, see [Enabling the {{site.data.keyword.filestorage_vpc_full_notm}} cluster add-on](/docs/openshift?topic=openshift-storage-file-vpc-install).

### Limitations
{: #vpc-file-rfs-eit-limits}

Review the following limitations before you enable RFS EIT.

- **Maximum PVC mounts per node:** 300, one port per PVC from the port range 11300–11599, bound on `127.0.0.1`.
- **Port conflict for applications with `hostNetwork: true`:** Application pods that use `hostNetwork: true` and bind to `127.0.0.1` in the port range 11300–11599 may conflict with existing RFS EIT PVC mounts.
- All limitations that apply to [VPC File Storage](/docs/vpc?topic=vpc-file-storage-vpc-about#fs-limitations) also apply.

### Setting up encryption in transit for Regional File Storage
{: #vpc-file-rfs-eit-setup}

Complete the following steps to provision a regional file share with encryption in transit.

1. Create a storage class that specifies the `rfs` profile and sets `isEITEnabled: "true"`. Save the following YAML to a file called `rfs-eit-sc.yaml`.

    The following parameters are required for RFS EIT: `profile: "rfs"`, `isENIEnabled: "true"`, `isEITEnabled: "true"`, and `proto=tcp` in the mount options.
    {: note}

    ```yaml
    apiVersion: storage.k8s.io/v1
    kind: StorageClass
    metadata:
      name: ibmc-vpc-file-rfs-eit-custom
      labels:
        app.kubernetes.io/name: ibm-vpc-file-csi-driver
    provisioner: vpc.file.csi.ibm.io
    parameters:
      profile: "rfs"           # Regional File Storage profile
      billingType: "hourly"
      throughput: "1000"       # Bandwidth in MB/s (25–8192 MB/s for RFS profile)
      encrypted: "false"
      encryptionKey: ""        # Specify the CRK CRN if encrypted is true
      resourceGroup: ""        # Defaults to the resource group in the storage secret store
      isENIEnabled: "true"     # Required for RFS — enables ENI/VNI feature
      isEITEnabled: "true"     # Enables encryption in transit with stunnel
      securityGroupIDs: ""     # Defaults to the cluster security group kube-<clusterID>
      subnetID: ""             # Defaults to an available subnet in the cluster VPC
      region: ""               # Defaults to the region from the cluster node topology
      primaryIPID: ""          # Optional: existing reserved IP ID (region is required)
      primaryIPAddress: ""     # Optional: IP address for ENI/VNI (region and subnetID required)
      tags: ""
      uid: "0"
      gid: "0"
      classVersion: "1"
    mountOptions:
      - hard
      - nfsvers=4.1
      - sec=sys
      - proto=tcp              # Required for stunnel (encryption in transit)
    reclaimPolicy: "Delete"
    allowVolumeExpansion: true
    ```
    {: codeblock}

1. Apply the storage class.

    ```sh
    oc apply -f rfs-eit-sc.yaml
    ```
    {: pre}

1. Create a PVC that references the `ibmc-vpc-file-rfs-eit-custom` storage class. Save the following YAML to a file called `rfs-eit-pvc.yaml`.

    ```yaml
    apiVersion: v1
    kind: PersistentVolumeClaim
    metadata:
      name: my-rfs-eit-pvc
    spec:
      accessModes:
        - ReadWriteMany
      resources:
        requests:
          storage: 10Gi
      storageClassName: ibmc-vpc-file-rfs-eit-custom
    ```
    {: codeblock}

1. Apply the PVC.

    ```sh
    oc apply -f rfs-eit-pvc.yaml
    ```
    {: pre}

1. Create a pod that mounts the PVC. Save the following YAML to a file called `rfs-eit-pod.yaml`.

    ```yaml
    apiVersion: v1
    kind: Pod
    metadata:
      name: my-rfs-eit-app
    spec:
      containers:
      - name: app
        image: nginx:latest
        volumeMounts:
        - name: rfs-eit-storage
          mountPath: /data
      volumes:
      - name: rfs-eit-storage
        persistentVolumeClaim:
          claimName: my-rfs-eit-pvc
    ```
    {: codeblock}

1. Apply the pod.

    ```sh
    oc apply -f rfs-eit-pod.yaml
    ```
    {: pre}

### Verifying encryption in transit is active
{: #vpc-file-rfs-eit-verify}

After the pod starts, verify that the encryption in transit is working by checking the file share target. The mount target must show `Transit Encryption: stunnel` to confirm EIT is active.

1. Wait for the pod to reach `Running` state and the PVC to reach `Bound` status.

    ```sh
    oc get pod my-rfs-eit-app
    oc get pvc my-rfs-eit-pvc
    ```
    {: pre}

1. Get the file share ID and the mount target ID from the persistent volume.

    ```sh
    oc describe pv <pv-name> | grep -E "fileShareId|fileShareTargetId"
    ```
    {: pre}

    Note the `fileShareId` and `fileShareTargetId` values from the output. You will use them in the next step to verify EIT on the VPC side.

1. Verify that the file share mount target shows `stunnel` as the transit encryption method.

    ```sh
    ibmcloud is share-mount-target <file-share-id> <file-share-target-id> | grep "Transit Encryption"
    ```
    {: pre}

    Example output that confirms EIT is active:
    ```sh
    Transit Encryption          stunnel
    ```
    {: screen}

### Troubleshooting RFS EIT
{: #vpc-file-rfs-eit-ts}

For help with common RFS EIT errors, see [Troubleshooting Regional File Storage encryption in transit](/docs/openshift?topic=openshift-ts-storage-vpc-file-rfs-eit).

## Next steps
{: #storage-file-vpc-eit-next}

- [Managing {{site.data.keyword.filestorage_vpc_short}}](/docs/openshift?topic=openshift-storage-file-vpc-managing)
- [{{site.data.keyword.filestorage_vpc_short}} storage class reference](/docs/openshift?topic=openshift-storage-file-vpc-sc-ref)
- [Troubleshooting RFS EIT](/docs/openshift?topic=openshift-ts-storage-vpc-file-rfs-eit)
- [Why do I see an `UnresponsiveMountHelperContainerUtility` error?](/docs/openshift?topic=openshift-ts-storage-vpc-file-eit-unresponsive)
- [Why do I see a `MetadataServiceNotEnabled` error?](/docs/openshift?topic=openshift-ts-storage-vpc-file-eit-metadata)
