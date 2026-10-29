---

copyright:
  years: 2026, 2026
lastupdated: "2026-10-29"

keywords: openshift, classic, vpc, migrate, assess, inventory, metadata, generateVPCMetadata

subcollection: openshift

content-type: howto

---

{{site.data.keyword.attribute-definition-list}}

# Assess your Classic cluster
{: #vpc-migrate-assess}

[Classic infrastructure]{: tag-classic-inf}

Inspect your Classic cluster and generate the VPC metadata that drives the rest of the migration. The metadata captures your cluster's worker pools, subnets, add-ons, KMS configuration, and proposes equivalent VPC settings for each.
{: shortdesc}

## Before you begin
{: #vpc-migrate-assess-prereqs}

- You have at least the **Operator** (`containers-kubernetes.cluster.operate`) {{site.data.keyword.iamlong}} platform access role for {{site.data.keyword.openshiftlong_notm}} on the Classic cluster. See [Assigning cluster access](/docs/openshift?topic=openshift-iam-platform-access-roles).
- A Cloud Object Storage (COS) instance is provisioned in the same account. Metadata files (`{clusterID}_classic.json` and `{clusterID}_vpc.json`) are written to this instance.
- If your Classic cluster connects to on-premises networks using Classic VPN or Direct Link 1.0, plan to set up equivalent VPC connectivity before you start workload migration. See [Step 4: Plan private connectivity](/docs/openshift?topic=openshift-vpc-migrate-plan#vpc-migrate-plan-connectivity).
- [Access your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-access_cluster).

## Generate VPC metadata
{: #vpc-migrate-assess-generate}

### From the console
{: #vpc-migrate-assess-ui}
{: ui}

1. Open the migration wizard. Go to **Migration hub** > **Clusters** > **Eligible clusters** and click **Open wizard** for your Classic cluster. Alternatively, go to **Containers** > **Clusters** and select **Migrate to VPC** in the row actions.
2. On the **Assess** step, under **Assessment**, select your **Cloud Object Storage instance** from the dropdown. If you do not have a COS instance, click **Create +** to provision one.
3. Click **Assess configurations**. The button changes to a spinner with the message **Running assessment** while the metadata is being generated.
4. When the assessment completes, the status updates to **Assessment complete**. If the assessment fails, a banner displays the error — resolve the indicated IAM permissions issue and click **Assess configurations** again.
5. Review the **VPC cluster preview** panel. It shows the proposed values for **Infrastructure**, **Worker Pools**, **Private & Public Endpoint**, **Outbound traffic**, **CIDR (IP range)**, and **Resource group**.
6. Optionally, click **Compare clusters** to open a side-by-side comparison of your Classic cluster and the proposed VPC cluster configuration.
7. Before you create the VPC cluster, review [Plan your VPC environment](/docs/openshift?topic=openshift-vpc-migrate-plan).

### From the CLI
{: #vpc-migrate-assess-cli}
{: cli}

Run the following commands to generate and inspect the VPC metadata for your Classic cluster.

1. Generate the VPC metadata for your Classic cluster. Replace `CLUSTER_ID` with your Classic cluster ID and `COS_CRN` with the CRN of your COS instance.

   ```sh
   ibmcloud oc replatform cluster assess --cluster-id CLUSTER_ID --cos-instance-crn COS_CRN
   ```
   {: pre}

   When the command completes, the metadata files are written to your COS instance.

2. Review the generated VPC configuration. Replace `CLUSTER_ID` with your Classic cluster ID.

   ```sh
   ibmcloud oc replatform cluster get --cluster-id CLUSTER_ID
   ```
   {: pre}

   Example output:
   ```text
   VPC name:        mig-my-classic-cluster
   Region:          us-south
   Worker pools:
     default        bx2.4x16   2/zone   us-south-1, us-south-2
   Add-ons:
     cluster-autoscaler   1.2.1
   KMS instance CRN:  (none)
   ```
   {: screen}

   Confirm that the `region`, worker pool flavors, add-ons, and KMS settings match your expectations before you proceed.

### From the API
{: #vpc-migrate-assess-api}
{: api}

1. Call the `generateVPCMetadata` mutation. Replace `CLUSTER_ID` with your Classic cluster ID and `COS_INSTANCE_ID` with the ID from your COS instance CRN.

   ```graphql
   mutation GenerateMeta($input: GenerateVPCMetadataInput!) {
     generateVPCMetadata(input: $input) {
       classic {
         ID name region masterVersion numberOfWorkers
         workerZones state status EOS
       }
       vpcMeta {
         VPCID name region version type
         vpcSubnetIDs { key value }
         workerPools {
           name machineType sizePerZone operatingSystem zones
           secondaryStorageOption secondaryStorageSize
         }
         addOns { name version }
         disablePSE
         keyManagementService {
           desiredInstanceCRN desiredRootKeyID
         }
       }
     }
   }
   ```
   {: codeblock}

   ```json
   {
     "input": {
       "clusterID":      "CLUSTER_ID",
       "cosInstanceCRN": "crn:v1:bluemix:public:cloud-object-storage:global:a/ACCOUNT_ID:COS_INSTANCE_ID::"
     }
   }
   ```
   {: codeblock}

   Send the request:

   ```sh
   curl -X POST https://REGION.containers.cloud.ibm.com/graphql \
     -H "Authorization: Bearer $(ibmcloud iam oauth-tokens --output json | jq -r '.iam_token')" \
     -H "Content-Type: application/json" \
     -d '{"query":"mutation GenerateMeta($input:GenerateVPCMetadataInput!){generateVPCMetadata(input:$input){classic{ID name region masterVersion}vpcMeta{name region}}}","variables":{"input":{"clusterID":"CLUSTER_ID","cosInstanceCRN":"COS_CRN"}}}'
   ```
   {: pre}

   Example response:
   ```json
   {
     "data": {
       "generateVPCMetadata": {
         "classic": {
           "ID": "abc123xyz456",
           "name": "my-classic-cluster",
           "region": "us-south",
           "masterVersion": "1.34.1_1601"
         },
         "vpcMeta": {
           "name": "mig-my-classic-cluster",
           "region": "us-south"
         }
       }
     }
   }
   ```
   {: screen}

2. Query the generated VPC configuration and confirm that `region`, `workerPools`, `addOns`, and `keyManagementService` match your expectations. Replace `CLUSTER_ID` with your Classic cluster ID.

   ```graphql
   query GetVPCMeta($id: ID!) {
     node(id: $id) {
       id
       ... on KubernetesCluster {
         vpcMigration {
           vpcMeta {
             VPCID name region version
             vpcSubnetIDs { key value }
             workerPools {
               name machineType sizePerZone operatingSystem zones
             }
             addOns { name version }
             keyManagementService { desiredInstanceCRN desiredRootKeyID }
           }
         }
       }
     }
   }
   ```
   {: codeblock}

   ```json
   { "id": "CLUSTER_ID" }
   ```
   {: codeblock}

   Example response:
   ```json
   {
     "data": {
       "node": {
         "id": "abc123xyz456",
         "vpcMigration": {
           "vpcMeta": {
             "VPCID": "r006-1a2b3c4d-5e6f-7890-abcd-ef1234567890",
             "name": "mig-my-classic-cluster",
             "region": "us-south",
             "version": "1.34",
             "vpcSubnetIDs": [
               { "key": "us-south-1", "value": "0717-subnet-aaa" },
               { "key": "us-south-2", "value": "0727-subnet-bbb" }
             ],
             "workerPools": [
               {
                 "name": "default",
                 "machineType": "bx2.4x16",
                 "sizePerZone": 2,
                 "operatingSystem": "REDHAT_8_64",
                 "zones": ["us-south-1", "us-south-2"]
               }
             ],
             "addOns": [
               { "name": "cluster-autoscaler", "version": "1.2.1" }
             ],
             "keyManagementService": {
               "desiredInstanceCRN": "",
               "desiredRootKeyID": ""
             }
           }
         }
       }
     }
   }
   ```
   {: screen}

## Review add-on compatibility
{: #vpc-migrate-assess-addons}

The migration service automatically migrates supported add-ons to the VPC cluster. For the full add-on migration behavior table, see [Add-on migration behavior](/docs/openshift?topic=openshift-vpc-migrate-overview#vpc-migrate-overview-limitations-addons).

If your cluster has an add-on not listed in that table, treat it as not migrated and plan to re-enable it manually on the VPC cluster.
{: note}

### From the console
{: #vpc-migrate-assess-addons-ui}
{: ui}

After the assessment completes, the **VPC cluster preview** panel shows the **Worker Pools** count. To see the full list of add-ons detected on your Classic cluster, click **Compare clusters** and review the **Add-ons** section in the side-by-side comparison panel. Compare the add-ons listed against the [add-on migration behavior table](/docs/openshift?topic=openshift-vpc-migrate-overview#vpc-migrate-overview-limitations-addons).

### From the CLI
{: #vpc-migrate-assess-addons-cli}
{: cli}

1. List the add-ons installed on your Classic cluster:

   ```sh
   ibmcloud oc cluster addon ls --cluster CLUSTER
   ```
   {: pre}

   Example output:
   ```text
   Name                   Version   Health State   Health Status
   cluster-autoscaler     1.2.1     normal         Addon Ready
   image-key-synchronizer 4.16.0    normal         Addon Ready
   static-route           1.0.0     normal         Addon Ready
   ```
   {: screen}

2. Compare the installed add-ons against the [add-on migration behavior table](/docs/openshift?topic=openshift-vpc-migrate-overview#vpc-migrate-overview-limitations-addons).

### From the API
{: #vpc-migrate-assess-addons-api}
{: api}

The `generateVPCMetadata` response includes an `addOns` array in the `vpcMeta` object. Compare the add-ons listed in that response against the [add-on migration behavior table](/docs/openshift?topic=openshift-vpc-migrate-overview#vpc-migrate-overview-limitations-addons).

## Review persistent storage
{: #vpc-migrate-assess-storage}

Classic clusters use Classic Block Storage and Classic File Storage. VPC clusters use VPC Block Storage and VPC File Storage. Identify all PVCs now so that you can plan the storage class mappings before you proceed to the workload migration phase.

### From the console
{: #vpc-migrate-assess-storage-ui}
{: ui}

1. From the [{{site.data.keyword.cloud_notm}} console](https://cloud.ibm.com/containers/cluster-management/clusters){: external}, click your Classic cluster.
2. Click **Storage** in the left navigation menu.
3. Review the list of persistent volume claims. Note the **Storage class** for each PVC — you will map each Classic storage class to a VPC equivalent when you create the migration plan.

### From the CLI
{: #vpc-migrate-assess-storage-cli}
{: cli}

List all PVCs on your Classic cluster so that you can plan your storage class mappings before the Migrate step.

1. List all PVCs across namespaces. Note the storage class of each PVC — you will map each Classic storage class to a VPC equivalent in the Migrate step.

   ```sh
   oc get pvc --all-namespaces
   ```
   {: pre}

   Example output:
   ```text
   NAMESPACE    NAME              STATUS   VOLUME                                     CAPACITY   ACCESS MODES   STORAGECLASS        AGE
   production   my-block-pvc      Bound    pvc-a1b2c3d4-e5f6-7890-abcd-ef1234567890   20Gi       RWO            ibmc-block-gold     45d
   production   my-file-pvc       Bound    pvc-b2c3d4e5-f6a7-8901-bcde-f12345678901   10Gi       RWX            ibmc-file-silver    45d
   staging      app-data-pvc      Bound    pvc-c3d4e5f6-a7b8-9012-cdef-123456789012   50Gi       RWO            ibmc-block-bronze   12d
   ```
   {: screen}

The migration plan generated in [Migrate workloads](/docs/openshift?topic=openshift-vpc-migrate-workloads) provides the storage class mappings, which you can override per PVC.

### From the API
{: #vpc-migrate-assess-storage-api}
{: api}

List all PVCs on your Classic cluster so that you can plan your storage class mappings before calling `startWorkloadMigration`.

1. List all PVCs across namespaces on your Classic cluster. Note the storage class of each PVC — you will pass storage class mappings in the `startWorkloadMigration` mutation during the Migrate step.

   ```sh
   curl -X GET https://REGION.containers.cloud.ibm.com/v1/clusters/CLASSIC_CLUSTER_ID/config \
     -H "Authorization: Bearer $(ibmcloud iam oauth-tokens --output json | jq -r '.iam_token')"
   ```
   {: pre}

   Alternatively, query the cluster directly using `kubectl` with the retrieved kubeconfig:

   ```sh
   oc get pvc --all-namespaces --output json | jq '[.items[] | {namespace: .metadata.namespace, name: .metadata.name, storageClass: .spec.storageClassName, capacity: .spec.resources.requests.storage}]'
   ```
   {: pre}

   Example output:
   ```json
   [
     { "namespace": "production", "name": "my-block-pvc", "storageClass": "ibmc-block-gold",   "capacity": "20Gi" },
     { "namespace": "production", "name": "my-file-pvc",  "storageClass": "ibmc-file-silver",  "capacity": "10Gi" },
     { "namespace": "staging",    "name": "app-data-pvc", "storageClass": "ibmc-block-bronze",  "capacity": "50Gi" }
   ]
   ```
   {: screen}

The `createMigrationPlan` response includes proposed `storageClassNameMappings` for each PVC. You can override any mapping when calling `startWorkloadMigration`.

## Next steps
{: #vpc-migrate-assess-next}

[Plan your VPC environment](/docs/openshift?topic=openshift-vpc-migrate-plan)
