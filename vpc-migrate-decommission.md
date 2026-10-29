---

copyright:
  years: 2026, 2026
lastupdated: "2026-10-29"

keywords: openshift, classic, vpc, migrate, delete, remove, cluster

subcollection: openshift

content-type: howto

---

{{site.data.keyword.attribute-definition-list}}

# Deleting Classic clusters
{: #vpc-migrate-decommission}

[Classic infrastructure]{: tag-classic-inf}

After your workloads are running on VPC and traffic has been fully redirected, delete the Classic cluster to remove unused infrastructure.
{: shortdesc}

## Before you begin
{: #vpc-migrate-decommission-prereqs}

- All workloads are validated and running on the VPC cluster, DNS has been cut over, and the stabilization period has passed with no traffic or errors on the Classic cluster. See [Cut over and validate](/docs/openshift?topic=openshift-vpc-migrate-cutover).
- DNS TTLs have been restored to their original values.
- You have confirmed that no other Classic clusters in your account share VLANs with this cluster that you want to retain.
- [Access your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-access_cluster).

## Step 1: Verify no active traffic on the Classic cluster
{: #vpc-migrate-decommission-verify}

Before deleting, confirm the Classic cluster is no longer receiving traffic.

### From the console
{: #vpc-migrate-decommission-verify-ui}
{: ui}

1. From the [{{site.data.keyword.cloud_notm}} console](https://cloud.ibm.com/containers/cluster-management/clusters){: external}, click your Classic cluster.
2. Click **Kubernetes dashboard** and navigate to **Workloads** > **Pods**.
3. Confirm that no new pods are being created and that workload activity has stopped.

### From the CLI
{: #vpc-migrate-decommission-verify-cli}
{: cli}

1. Check for active pod restarts or events on the Classic cluster that would indicate ongoing traffic.

   ```sh
   oc get pods --all-namespaces --sort-by='.status.containerStatuses[0].restartCount'
   ```
   {: pre}

2. Confirm no new events are appearing on the Classic cluster.

   ```sh
   oc get events --all-namespaces --sort-by='.lastTimestamp' | tail -10
   ```
   {: pre}

## Step 2: Remove any remaining Classic-specific resources
{: #vpc-migrate-decommission-cleanup}

Before deleting the cluster, clean up any resources that were not migrated and are no longer needed.

- Cancel any Classic bare metal servers or virtual server instances that were attached to the cluster outside of the managed worker nodes.
- Review and delete any Classic load balancers that were created by Kubernetes `LoadBalancer` services, if they were not automatically cleaned up.
- If your cluster used Classic File Storage or Classic Block Storage PVCs that you do not want to retain, delete those PVCs before cluster deletion or they will become orphaned volumes.

Classic PVCs that are not deleted before cluster removal persist as orphaned volumes and continue to incur charges. Delete them explicitly if you do not plan to reuse them.
{: important}

## Step 3: Delete the Classic cluster
{: #vpc-migrate-decommission-delete}

### From the console
{: #vpc-migrate-decommission-delete-ui}
{: ui}

Deleting the cluster removes all associated worker nodes, VLANs (if not shared with other clusters), and load balancers. This action cannot be undone.
{: important}

1. From the [{{site.data.keyword.cloud_notm}} console](https://cloud.ibm.com/containers/cluster-management/clusters){: external}, click your Classic cluster.
2. Click **Actions** > **Delete**.
3. Select **Delete all attached storage** only if you want to permanently delete Classic persistent volumes along with the cluster.
4. Confirm by entering the cluster name and click **Delete**.

### From the CLI
{: #vpc-migrate-decommission-delete-cli}
{: cli}

Deleting the cluster removes the associated Classic infrastructure: worker nodes, VLANs (if not shared), and load balancers. Omit `--force-delete-storage` if you want to retain Classic storage volumes for manual cleanup.
{: important}

1. Delete the Classic cluster.

   ```sh
   ibmcloud oc cluster rm --cluster CLASSIC_CLUSTER_NAME --force-delete-storage
   ```
   {: pre}

   Example output:
   ```text
   Remove cluster? [kube-a1b2c3d4] (Y/n)> Y
   Removing cluster kube-a1b2c3d4...
   OK
   ```
   {: screen}

### From the API
{: #vpc-migrate-decommission-delete-api}
{: api}

Deleting the cluster removes all associated Classic infrastructure. Omit `deleteResources=true` if you want to retain Classic storage volumes.
{: important}

1. Delete the Classic cluster.

   ```sh
   curl -X DELETE "https://REGION.containers.cloud.ibm.com/v1/clusters/CLASSIC_CLUSTER_ID?deleteResources=true" \
     -H "Authorization: Bearer $(ibmcloud iam oauth-tokens --output json | jq -r '.iam_token')"
   ```
   {: pre}

   A `204 No Content` response confirms the deletion request was accepted. The cluster is removed asynchronously.

2. Confirm the cluster no longer appears in the cluster list.

   ```sh
   curl -X GET "https://REGION.containers.cloud.ibm.com/v1/clusters" \
     -H "Authorization: Bearer $(ibmcloud iam oauth-tokens --output json | jq -r '.iam_token')" \
     | jq '[.[] | select(.id == "CLASSIC_CLUSTER_ID")]'
   ```
   {: pre}

   An empty array `[]` confirms the cluster has been deleted.

## Next steps
{: #vpc-migrate-decommission-next}

Your migration is complete. To continue managing your new VPC cluster:

- [VPC cluster networking](/docs/openshift?topic=openshift-vpc-subnets)
- [Updating clusters, worker nodes, and cluster components](/docs/openshift?topic=openshift-update)
- [Securing your cluster](/docs/openshift?topic=openshift-security)
