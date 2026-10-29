---

copyright:
  years: 2026, 2026
lastupdated: "2026-10-29"

keywords: openshift, classic, vpc, migrate, create cluster, provision, createCluster

subcollection: openshift

content-type: howto

---

{{site.data.keyword.attribute-definition-list}}

# Create the VPC cluster
{: #vpc-migrate-create}

[Classic infrastructure]{: tag-classic-inf}

Provision the VPC cluster from the generated metadata. After creation, the migration service automatically begins migrating infrastructure resources — IAM policies, add-ons, and global resources — in the background.
{: shortdesc}

## Before you begin
{: #vpc-migrate-create-prereqs}

- Complete the [assess](/docs/openshift?topic=openshift-vpc-migrate-assess) and [plan](/docs/openshift?topic=openshift-vpc-migrate-plan) topics.
- Have any override values ready: VPC ID, subnet IDs per zone, cluster name, and worker pool flavors.
- [Access your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-access_cluster).

## Create the VPC cluster
{: #vpc-migrate-create-cluster}

### From the console
{: #vpc-migrate-create-ui}
{: ui}

1. In the migration wizard, navigate to the **Create** step in the left navigation panel.
2. Review the **Classic cluster** summary, which shows the cluster **Name**, **Cluster ID**, **Tag**, **Control plane** status, **Node status**, and **Ingress status**.
3. Click **Create VPC cluster**. This opens the standard **Create a cluster** page with the configuration pre-filled from your assessment:
   - The cluster name defaults to `<classic-name>-VPC`.
   - The infrastructure is set to **Virtual Private Cloud**.
   - Worker pool configuration is retained from the Classic cluster.
   - You select the VPC. If you do not select a VPC, a new VPC is created in the same region as your Classic cluster.
   - If a zone is missing a subnet, a warning banner prompts you to create one before proceeding.
4. Review the pre-filled settings. You can adjust the cluster name, VPC selection, subnet assignments, worker pool flavor, and other settings as needed.
5. Click **Create** in the cost summary panel to provision the VPC cluster.
6. After the cluster is provisioned, return to the migration wizard. The **VPC cluster** section updates with the new cluster's details. Click **Migrate workloads** to proceed.

### From the CLI
{: #vpc-migrate-create-cli}
{: cli}

1. Create the VPC cluster using the generated metadata defaults. Replace `CLASSIC_CLUSTER_ID` with your Classic cluster ID, `VPC_ID` with your VPC ID, and `ZONE=SUBNET_ID` with a zone and subnet pair.

   ```sh
   ibmcloud oc replatform cluster create --cluster-id CLASSIC_CLUSTER_ID --vpc-id VPC_ID --subnet-id ZONE=SUBNET_ID
   ```
   {: pre}

   Example output:
   ```text
   OK
   VPC cluster creation initiated. VPC cluster name: mig-my-classic-cluster
   VPC cluster ID: a1b2c3d4e5f6g7h8i9j0k1l2m3n4o5p6
   ```
   {: screen}

   To specify multiple zones, repeat `--subnet-id`. To override the cluster name, include `--name`:

   ```sh
   ibmcloud oc replatform cluster create --cluster-id CLASSIC_CLUSTER_ID \
     --vpc-id VPC_ID \
     --subnet-id us-south-1=SUBNET_ID_1 \
     --subnet-id us-south-2=SUBNET_ID_2 \
     --name mig-my-cluster
   ```
   {: pre}

   Example output:
   ```text
   OK
   VPC cluster creation initiated. VPC cluster name: mig-my-cluster
   VPC cluster ID: b2c3d4e5f6g7h8i9j0k1l2m3n4o5p6q7
   ```
   {: screen}

### From the API
{: #vpc-migrate-create-api}
{: api}

Call the `createCluster` mutation. To use the generated defaults, pass only the `clusterID`.

1. Submit the mutation:

   ```graphql
   mutation CreateCluster($input: createClusterInput!) {
     createCluster(input: $input) {
       message status region classicClusterID
     }
   }
   ```
   {: codeblock}

   **Minimal — use all generated defaults:**

   ```json
   {
     "input": { "clusterID": "CLASSIC_CLUSTER_ID" }
   }
   ```
   {: codeblock}

   **With overrides — custom name, subnets, and worker pool flavor:**

   ```json
   {
     "input": {
       "clusterID":       "CLASSIC_CLUSTER_ID",
       "vpcClusterName":  "mig-my-cluster",
       "vpcID":           "VPC_ID",
       "subnetIDs": {
         "us-south-1": "0717-subnet-aaa",
         "us-south-2": "0727-subnet-bbb"
       },
       "workerPoolOverrides": [
         { "name": "default", "flavor": "bx2.8x32" }
       ],
       "disableBRSWorkerpool": false
     }
   }
   ```
   {: codeblock}

   Valid values for `vpcClusterName` must start with a lowercase letter, use only `[a-z0-9-]`, end with a letter or digit, and be 32 characters or fewer.
   {: note}

   Example response:
   ```json
   {
     "data": {
       "createCluster": {
         "message": "VPC cluster creation initiated.",
         "status": "in_progress",
         "region": "us-south",
         "classicClusterID": "CLASSIC_CLUSTER_ID"
       }
     }
   }
   ```
   {: screen}

## Monitor cluster provisioning
{: #vpc-migrate-create-wait}

After the cluster creation is submitted, the VPC cluster is provisioning. Monitor the worker node status until all workers show a state of `normal`. If workers do not reach `normal` state after 30 minutes, run the following command to check the current worker state and status before consulting the [cluster state](/docs/openshift?topic=openshift-states-cluster) and [worker node state](/docs/openshift?topic=openshift-states-workers) reference topics:

```sh
ibmcloud oc worker get --cluster VPC_CLUSTER_NAME --worker WORKER_ID
```
{: pre}

Review the `State` and `Status` fields in the output. A state of `critical`, `unknown`, or `provision_failed` indicates a provisioning problem. See [Worker node states](/docs/openshift?topic=openshift-states-workers) for the resolution steps for each state.

After all workers reach `normal` state, the background infrastructure sub-operations begin automatically. For full monitoring instructions, retry guidance, and troubleshooting for those sub-operations, see [Monitor global resource migration](/docs/openshift?topic=openshift-vpc-migrate-global-resources).

### From the console
{: #vpc-migrate-create-wait-ui}
{: ui}

After clicking **Create**, the cluster creation flow redirects you to the new VPC cluster overview page. When the cluster is ready, a **What next?** banner appears. Do not proceed to the **Migrate** step until all four background sub-operations are complete. See [Monitor global resource migration](/docs/openshift?topic=openshift-vpc-migrate-global-resources) for details and troubleshooting.

### From the CLI
{: #vpc-migrate-create-wait-cli}
{: cli}

1. Run the following command periodically until all worker nodes show `State: normal` before proceeding to monitor the background sub-operations.

   ```sh
   ibmcloud oc workers --cluster VPC_CLUSTER_NAME
   ```
   {: pre}

   Example output:
   ```text
   ID                                                     State    Status   Zone         Version    IP              Flavor
   kube-a1b2c3d4-default-00000aaa-worker-0   normal   Ready    us-south-1   1.34.1_1601   10.240.0.4   bx2.8x32
   kube-a1b2c3d4-default-00000bbb-worker-0   normal   Ready    us-south-2   1.34.1_1601   10.240.64.4  bx2.8x32
   kube-a1b2c3d4-default-00000ccc-worker-0   normal   Ready    us-south-3   1.34.1_1601   10.240.128.4 bx2.8x32
   ```
   {: screen}

### From the API
{: #vpc-migrate-create-wait-api}
{: api}

After all workers reach `normal` state, proceed to monitor the background sub-operations. For the full polling query, retry guidance, and troubleshooting, see [Monitor global resource migration](/docs/openshift?topic=openshift-vpc-migrate-global-resources).

## Next steps
{: #vpc-migrate-create-next}

[Monitor global resource migration](/docs/openshift?topic=openshift-vpc-migrate-global-resources)
