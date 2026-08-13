---

copyright:
  years: 2026
lastupdated: "2026-08-13"

keywords: openshift, vpc file storage, capacity roundoff, pvc pending, ProvisioningFailed, dp2, storageclass

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why does my PVC stay in Pending status when using capacity roundoff?
{: #ts-storage-vpc-file-capacity-roundoff}
{: troubleshoot}
{: support}

[Virtual Private Cloud]{: tag-vpc}

Your PVC stays in `Pending` status and you see a `ProvisioningFailed` warning event when using a StorageClass with `allowCapacityRoundoffForIops: "true"` enabled.
{: tsSymptoms}

One of the following conditions might be causing the failure:
{: tsCauses}

- The driver could not reach IBM Global Catalog at startup and the DP2 catalog was not loaded. Capacity roundoff requires the driver to fetch a supported capacity-to-IOPS catalog from Global Catalog during startup.
- The requested IOPS or capacity combination is not valid for the `dp2` profile.

Check the PVC events to identify the error message, then resolve the issue based on the following table.
{: tsResolve}

1. Run the following command and look for a `Warning` event with a `ProvisioningFailed` reason.

   ```sh
   oc describe pvc PVC_NAME
   ```
   {: pre}

1. Match the error message to the resolution in the following table.

| Error message in events | Cause | Resolution |
| --- | --- | --- |
| `capacity round-off is unavailable because the DP2 catalog could not be loaded during driver startup` | The driver could not reach Global Catalog at startup. | Verify that your Virtual Private Endpoint Gateway (VPEG) is configured correctly and that the driver can reach `private.globalcatalog.cloud.ibm.com`. Restart the driver pods after fixing connectivity. For setup instructions, see [Prerequisites](/docs/openshift?topic=openshift-storage-file-vpc-capacity-roundoff#storage-file-vpc-capacity-roundoff-prereqs). |
| `shares_profile_capacity_iops_invalid` | The requested IOPS or capacity combination is not valid for the `dp2` profile. | Check that the requested IOPS is within the [supported range for the `dp2` profile](/docs/vpc?topic=vpc-file-storage-profiles&interface=ui#dp2-profile) and that the requested capacity does not exceed the profile maximum. |
{: caption="Common capacity roundoff provisioning failures" caption-side="bottom"}
