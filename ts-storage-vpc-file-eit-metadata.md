---

copyright:
  years: 2026
lastupdated: "2026-08-04"


keywords: kubernetes, openshift

subcollection: openshift
content-type: troubleshoot


---

{{site.data.keyword.attribute-definition-list}}

# Why do I see a `MetadataServiceNotEnabled` error for {{site.data.keyword.filestorage_vpc_short}}?
{: #ts-storage-vpc-file-eit-metadata}

[Virtual Private Cloud]{: tag-vpc}

If your pod or PVC fails with a `MetadataServiceNotEnabled` error while using encryption in transit (EIT) with {{site.data.keyword.filestorage_vpc_short}}, use this topic to identify and resolve the cause.
{: shortdesc}

When you use encryption in transit (EIT) with {{site.data.keyword.filestorage_vpc_short}}, your pod or PVC fails with a `MetadataServiceNotEnabled` error.
{: tsSymptoms}

You see an error message similar to the following example in your pod events or describe output:

```sh
Code: MetadataServiceNotEnabled,
Description: Failed to mount target.,
Action: Metadata service might not be enabled for worker node.
  Make sure to use IKS>=1.30 or ROKS>=4.16 cluster.
```
{: screen}

This error means the EIT mount process tried to reach the instance metadata service at `169.254.169.254` but received no response. There are two independent root causes — check both.
{: tsCauses}

## Resolving the issue
{: #ts-storage-vpc-file-eit-metadata-resolve}

Check the following root causes.
{: tsResolve}

### Root cause A — Cluster version is too old
{: #ts-storage-vpc-file-eit-metadata-root-cause-a}

EIT requires ROKS version 4.16 or later. On older clusters, the metadata service endpoint is not available to workloads.

Check the current cluster version to confirm whether your cluster meets the minimum requirement. The output shows `Pending` or `normal` status and the Kubernetes version.

```sh
ibmcloud ks cluster get --cluster <cluster-id> | grep "Version"
```
{: pre}

**Resolution:** Upgrade the cluster to ROKS version 4.16 or later.

### Root cause B — Secure by Default cluster is missing the metadata outbound rule
{: #ts-storage-vpc-file-eit-metadata-root-cause-b}

For Secure by Default clusters, outbound traffic to `169.254.169.254` is blocked unless an explicit outbound rule is added to the `kube-<clusterID>` security group. Without this rule, the EIT process cannot reach the metadata service even on a supported cluster version.

This rule is added automatically for ROKS clusters at version 4.18 and later. For older cluster versions, add the rule manually.
{: note}

1. Check whether the outbound rule already exists. If the command returns a line containing `169.254.169.254`, the rule is present and this is not the cause.

    ```sh
    ibmcloud is sg kube-<cluster-id> | grep 169.254.169.254
    ```
    {: pre}

1. If the rule is absent, add it.

    ```sh
    ibmcloud is sg-rulec kube-<cluster-id> outbound \
      --protocol all \
      --remote 169.254.169.254
    ```
    {: pre}

    Alternatively, add the rule from the IBM Cloud UI under **VPC Infrastructure > Security groups > `kube-<clusterID>` > Outbound rules** with the following values:

    | Field | Value |
    |---|---|
    | Protocol | Any |
    | Source type | Any |
    | Source | `0.0.0.0/0` |
    | Destination | `169.254.169.254` |
    {: caption="Outbound rule values for metadata service access" caption-side="bottom"}

1. After adding the rule, retry the failing pod. No node reboot is required.

If the issue persists after both checks, [open a support ticket](/docs/get-support?topic=get-support-open-case) with the IBM Cloud Container Storage team.

## Related topics
{: #ts-storage-vpc-file-eit-metadata-related}

- [Setting up encryption in-transit (EIT)](/docs/openshift?topic=openshift-storage-file-vpc-apps#storage-file-vpc-apps-eit)
- [Why do I see an `UnresponsiveMountHelperContainerUtility` error?](/docs/openshift?topic=openshift-ts-storage-vpc-file-eit-unresponsive)
