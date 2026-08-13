---

copyright:
  years: 2026
lastupdated: "2026-08-13"

keywords: openshift, vpc file storage, capacity roundoff, fixed iops, dp2, storageclass, pvc

subcollection: openshift

content-type: howto

---

{{site.data.keyword.attribute-definition-list}}

# Enabling automatic capacity roundoff for fixed IOPS profiles
{: #storage-file-vpc-capacity-roundoff}

With the capacity roundoff feature of the IBM VPC File CSI Driver, you can allow the driver to automatically adjust a requested persistent volume claim (PVC) capacity when it is lower than the minimum supported capacity for the selected fixed IOPS profile. This eliminates the need to manually calculate minimum capacity values before provisioning file shares.
{: shortdesc}

## How capacity roundoff works
{: #storage-file-vpc-capacity-roundoff-overview}

During driver startup, the IBM VPC File CSI Driver fetches a supported capacity-to-IOPS catalog from IBM Global Catalog. The catalog is cached in memory and used for all subsequent provisioning requests. The following table describes driver behavior during PVC provisioning.

| Scenario | Driver behavior |
| --- | --- |
| Requested IOPS is supported and requested capacity is below the minimum | The driver rounds up the capacity to the minimum supported value and provisions the PVC. |
| Requested IOPS is supported and requested capacity meets the minimum | The PVC provisions at the requested capacity. |
| Requested IOPS is not supported | Provisioning fails with a validation error. For help resolving this error, see [Troubleshooting capacity roundoff](/docs/openshift?topic=openshift-ts-storage-vpc-file-capacity-roundoff). |
{: caption="Capacity roundoff provisioning behavior" caption-side="bottom"}

If Global Catalog is unreachable at driver startup, a warning is logged and capacity roundoff is unavailable. All other provisioning behavior continues as expected.
{: note}

## Prerequisites
{: #storage-file-vpc-capacity-roundoff-prereqs}

Before you enable capacity roundoff, the driver must be able to reach IBM Global Catalog. To allow access, configure a Virtual Private Endpoint Gateway (VPEG) in your VPC.

1. [Create a Virtual Private Endpoint Gateway](/docs/vpc?topic=vpc-about-vpe) in your VPC for the Global Resources Catalog service.

   When you create the VPEG, configure the following settings:
   - Under **Cloud services**, select **Global Resources Catalog**.
   - Under **Available endpoints**, select the endpoint with endpoint type `api` and URL `private.globalcatalog.cloud.ibm.com` or `*.private.globalcatalog.cloud.ibm.com`.

   Use the exact service names and URLs as shown in the IBM Cloud UI.
   {: note}

1. Verify that your cluster nodes can reach the Global Catalog private endpoint. Without connectivity, the driver logs a warning at startup, and capacity roundoff is unavailable. All other provisioning behavior continues as expected.

## Create a StorageClass with capacity roundoff enabled
{: #storage-file-vpc-capacity-roundoff-sc}

Capacity roundoff is an optional feature that is disabled by default and must be enabled per StorageClass. Existing StorageClasses are not affected.

This feature applies only to `dp2` profile StorageClasses that use fixed IOPS provisioning. It does not apply to `rfs` profile classes.
{: important}

1. Create a StorageClass configuration file that sets `allowCapacityRoundoffForIops: "true"` in the `parameters` section.

   The following example creates a StorageClass with a valid IOPS value and capacity roundoff enabled:

   ```yaml
   apiVersion: storage.k8s.io/v1
   kind: StorageClass
   metadata:
     name: ibmc-vpc-file-dp2-roundoff
     labels:
       app.kubernetes.io/name: ibm-vpc-file-csi-driver
   provisioner: vpc.file.csi.ibm.io
   allowVolumeExpansion: true
   reclaimPolicy: Delete
   mountOptions:
     - hard
     - nfsvers=4.1
     - sec=sys
   parameters:
     allowCapacityRoundoffForIops: "true"
     billingType: hourly
     classVersion: "1"
     encrypted: "false"
     encryptionKey: ""
     gid: "0"
     iops: "4700"
     isENIEnabled: "true"
     primaryIPAddress: ""
     primaryIPID: ""
     profile: dp2
     region: ""
     resourceGroup: ""
     securityGroupIDs: ""
     subnetID: ""
     tags: ""
     uid: "0"
     zone: ""
   volumeBindingMode: Immediate
   ```
   {: codeblock}

1. Apply the StorageClass to your cluster.

   ```sh
   oc apply -f ibmc-vpc-file-dp2-roundoff.yaml
   ```
   {: pre}

1. Verify that the StorageClass is available in your cluster. Look for the name you specified in the output.

   ```sh
   oc get sc
   ```
   {: pre}

## Provision a PVC with capacity roundoff
{: #storage-file-vpc-capacity-roundoff-pvc}

After you create your StorageClass, create a PVC that references it. The following examples show the two main provisioning scenarios.

### Scenario 1: Capacity is below the minimum and gets rounded up
{: #storage-file-vpc-capacity-roundoff-scenario-low}

In this example, the PVC requests 80 Gi of storage. Because 80 Gi is below the minimum supported capacity for 4700 IOPS, the driver automatically provisions the file share at the minimum supported capacity (100 Gi in this case).

1. Create a PVC configuration file.

   ```yaml
   apiVersion: v1
   kind: PersistentVolumeClaim
   metadata:
     name: my-roundoff-pvc
     namespace: default
   spec:
     accessModes:
       - ReadWriteMany
     resources:
       requests:
         storage: 80Gi
     storageClassName: ibmc-vpc-file-dp2-roundoff
   ```
   {: codeblock}

1. Apply the PVC.

   ```sh
   oc apply -f my-roundoff-pvc.yaml
   ```
   {: pre}

1. Check that the PVC is bound and note the `CAPACITY` field in the output. The capacity should reflect the rounded-up value, not the 80 Gi that was requested.

   ```sh
   oc get pvc my-roundoff-pvc
   ```
   {: pre}

   Example output:

   ```sh
   NAME              STATUS   VOLUME                                     CAPACITY   ACCESS MODES   STORAGECLASS                  AGE
   my-roundoff-pvc   Bound    pvc-91ff9a52-5004-4441-9611-be5410edbfe4   100Gi      RWX            ibmc-vpc-file-dp2-roundoff    30s
   ```
   {: screen}

   The `CAPACITY` value is `100Gi` even though `80Gi` was requested, which confirms that the driver rounded up to the minimum supported capacity.

### Scenario 2: Capacity meets the minimum and provisions as requested
{: #storage-file-vpc-capacity-roundoff-scenario-exact}

In this example, the PVC requests 200 Gi, which already satisfies the minimum supported capacity for 4700 IOPS. The driver provisions the file share at the requested capacity with no adjustment.

1. Create a PVC configuration file.

   ```yaml
   apiVersion: v1
   kind: PersistentVolumeClaim
   metadata:
     name: my-exact-pvc
     namespace: default
   spec:
     accessModes:
       - ReadWriteMany
     resources:
       requests:
         storage: 200Gi
     storageClassName: ibmc-vpc-file-dp2-roundoff
   ```
   {: codeblock}

1. Apply the PVC.

   ```sh
   oc apply -f my-exact-pvc.yaml
   ```
   {: pre}

1. Check that the PVC is bound. The `CAPACITY` field should show `200Gi`, confirming no adjustment was made.

   ```sh
   oc get pvc my-exact-pvc
   ```
   {: pre}

   Example output:

   ```sh
   NAME           STATUS   VOLUME                                     CAPACITY   ACCESS MODES   STORAGECLASS                  AGE
   my-exact-pvc   Bound    pvc-3528044b-b004-4077-b09f-c6cdf7000180   200Gi      RWX            ibmc-vpc-file-dp2-roundoff    24m
   ```
   {: screen}

## Next steps
{: #storage-file-vpc-capacity-roundoff-next}

- [Add {{site.data.keyword.filestorage_vpc_short}} to your apps](/docs/openshift?topic=openshift-storage-file-vpc-apps)
- [Review the storage class reference](/docs/openshift?topic=openshift-storage-file-vpc-sc-ref)
- [Manage your {{site.data.keyword.filestorage_vpc_short}} instances](/docs/openshift?topic=openshift-storage-file-vpc-managing)

## Related links
{: #storage-file-vpc-capacity-roundoff-links}

- [About Virtual Private Endpoint Gateways](/docs/vpc?topic=vpc-about-vpe)
- [{{site.data.keyword.filestorage_vpc_short}} `dp2` profiles](/docs/vpc?topic=vpc-file-storage-profiles&interface=ui#dp2-profile)
- [VPC File Storage CSI Driver add-on changelog](/docs/openshift?topic=openshift-cl-add-ons-vpc-file-csi-driver)
- [Troubleshooting: Why does my PVC stay in Pending status when using capacity roundoff?](/docs/openshift?topic=openshift-ts-storage-vpc-file-capacity-roundoff)
