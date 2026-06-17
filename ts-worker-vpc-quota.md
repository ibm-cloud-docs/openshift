---

copyright:
  years: 2026, 2026
lastupdated: "2026-06-17"

keywords: openshift, vpc quota, worker node, vcpu, memory, gpu, instance storage, optimized instance storage

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# VPC worker nodes fail to provision due to quota limits
{: #ts-worker-vpc-quota}
{: troubleshoot}
{: support}

[Virtual Private Cloud]{: tag-vpc}

When you try to create or add worker nodes to your VPC cluster, the worker nodes fail to provision and show an error related to quota limits.
{: shortdesc}

Your worker nodes are in a `provision_failed` state. When you run `ibmcloud oc worker get --cluster <cluster_name_or_id> --worker <worker_id>` or view the worker details in the console, you see an error message similar to the following example.
{: tsSymptoms}

```sh
The user account has insufficient infrastructure quota to provision the worker: A VSI with this profile (30720GB generic instance storage) will put user over quota. Allocated: 1013760GB, Quota: 983040GB
```
{: screen}

The error message indicates which resource quota has been exceeded (vCPU, memory, GPU, instance storage, or optimized instance storage) and provides details about your current allocation and quota limit.

VPC manages quotas for vCPU, memory, GPU, instance storage, and optimized instance storage resources on a per-account basis. When you provision VPC virtual server instance (VSI) worker nodes on public infrastructure, these resources count against your account's VPC quotas. If you reach your quota limit for any of these resources, worker node provisioning fails.
{: tsCauses}

This quota management currently applies only to VSI worker nodes on public infrastructure. Dedicated host and bare metal worker nodes are not subject to these VPC quotas, as {{site.data.keyword.openshiftlong_notm}} continues to manage quotas for those worker node types.

To resolve this issue, you need to increase your VPC quota for the affected resource.
{: tsResolve}

1. Check your current VPC quota usage to identify which resource limit you've reached. For more information about VPC quotas and how to view them, see [Quotas and service limits](/docs/vpc?topic=vpc-quotas){: external} and [Viewing VPC resource metrics](/docs/vpc?topic=vpc-vpc-quota-metrics){: external}.

2. Open a support case with VPC to request a quota increase for the affected resource (vCPU, memory, GPU, instance storage, or optimized instance storage).
   1. Go to the [IBM Cloud Support Center](https://cloud.ibm.com/unifiedsupport/supportcenter){: external}.
   2. Click **Create a case**.
   3. Select **VPC Infrastructure** as the offering.
   4. In your case description, specify:
      - The resource type for which you need a quota increase (vCPU, memory, GPU, instance storage, or optimized instance storage)
      - Your current quota limit
      - The new quota limit you're requesting
      - The reason for the increase (for example, "Need to provision additional worker nodes for my {{site.data.keyword.openshiftlong_notm}} cluster")

3. After your quota increase is approved and applied, retry provisioning your worker nodes.
   - For failed worker nodes, you can delete them and create new ones, or use the `ibmcloud oc worker replace` command to replace them.
   - For worker pools that failed to scale, the cluster autoscaler (if enabled on the worker pool) automatically retries provisioning after the quota is increased.
