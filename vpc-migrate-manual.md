---

copyright:
  years: 2026, 2026
lastupdated: "2026-10-29"

keywords: openshift, classic, vpc, migrate, migration, manual, single-zone

subcollection: openshift

content-type: howto

---

{{site.data.keyword.attribute-definition-list}}

# Migrating from Classic to VPC manually
{: #vpc-migrate-manual}

[Classic infrastructure]{: tag-classic-inf}

Migrate a Classic cluster to VPC without the migration wizard.
{: shortdesc}

Most customers use the [migration wizard](/docs/openshift?topic=openshift-vpc-migrate-overview) to migrate {{site.data.keyword.openshiftlong_notm}} clusters from Classic to VPC. Migrate manually only if you cannot or do not want to use the wizard. For example, the wizard does not support clusters in a single-zone region (SZR). To check whether your cluster is eligible for the wizard, see [Which clusters are eligible for migration?](/docs/openshift?topic=openshift-vpc-migrate-overview#vpc-migrate-overview-limitations-cluster)

In Phase 1, you plan and set up your VPC infrastructure: assess your Classic environment, create the VPC network, configure security groups, and provision the VPC cluster.

## Step 1: Assess your Classic environment
{: #vpc-migrate-manual-assess}

Inventory your Classic cluster resources before you create anything in VPC. Document the following:

- Worker node flavors, zone distribution, and node counts
- VLANs, subnets, and any on-premises connectivity (Classic VPN, Direct Link 1.0)
- Add-ons, operators, and any cluster-scoped resources (CRDs, ClusterRoles, webhooks)
- Storage classes and PVCs in use
- Load balancers and Ingress hostnames
- Image registry paths ({{site.data.keyword.registrylong_notm}} namespaces and any private registries)

Use this inventory to drive each subsequent step. Pay particular attention to resources that have no direct VPC equivalent, such as Classic VPN and Direct Link 1.0 connections, which you must replace with VPC equivalents before cutover.

## Step 2: Create a VPC environment
{: #vpc-migrate-manual-vpc-env}

Create the VPC networking infrastructure to mirror your Classic network topology.

1. Create a VPC in the same region as your Classic cluster.
2. Create one subnet per zone, sized to accommodate your worker nodes and future growth.
3. Create a VPE (Virtual Private Endpoint) gateway per zone for any IBM Cloud services your workloads use (for example, {{site.data.keyword.cos_full_notm}}, {{site.data.keyword.registrylong_notm}}).
4. If your Classic cluster connects to on-premises networks by using Classic VPN or Direct Link 1.0, set up the equivalent VPC connectivity now. The migration does not migrate these connections. See [Setting up VPC VPN](/docs/openshift?topic=openshift-vpn-onprem) or [Direct Link 2.0](/docs/dl).

## Step 3: Configure VPC security groups
{: #vpc-migrate-manual-sg}

Map your Classic network access controls to VPC security groups.

1. Review the inbound and outbound rules on your Classic worker node network interfaces.
2. Create VPC security groups that replicate the required rules.
3. Record the security group IDs — you supply them when you create the VPC cluster.

## Step 4: Create the VPC cluster
{: #vpc-migrate-manual-create}

Provision the VPC cluster to match your Classic cluster configuration.

1. Choose a worker node flavor that includes secondary storage if your Classic cluster uses local storage or if you plan to use {{site.data.keyword.cloud_notm}} Backup and Recovery Service (BRS) for data migration.
2. Enable **Outbound traffic protection** to match the Classic cluster default security posture.
3. Provide the security group mapping from Step 3.
4. Set the cluster name and resource group.
5. Create the cluster. Wait for all worker nodes to reach **Ready** state before continuing.

After the cluster is ready, export any custom `ClusterRole`, `ClusterRoleBinding`, `PriorityClass`, `CustomResourceDefinition`, and admission webhooks from the Classic cluster and apply them to the VPC cluster. See [Migrating cluster-scoped resources](/docs/openshift?topic=openshift-vpc-migrate-workloads#vpc-migrate-workloads-cluster-scoped).

In Phase 2, you deploy your applications to VPC, replicate data, set up load balancing, and cut over live traffic.

## Step 5: Set up your deployment and replicate data
{: #vpc-migrate-manual-deploy}

Move your workloads to the VPC cluster by using your CI/CD pipeline or by deploying manually.

If you use a CI/CD pipeline:

1. Update your pipeline to target the VPC cluster.
2. Verify that the pipeline sets up all required resources: storage classes, registry pull secrets, ConfigMaps, Secrets, and image registry paths.
3. Replicate data from Classic to VPC storage volumes using your chosen backup and recovery method. IBM recommends {{site.data.keyword.cloud_notm}} Backup and Recovery Service (BRS). For pricing information, see [IBM Cloud Backup and Recovery pricing](https://cloud.ibm.com/backup-recovery/pricing){: external}.
4. Run the pipeline and confirm all workloads deploy successfully.

If you deploy manually:

1. Configure storage classes on the VPC cluster to match what your applications expect.
2. Copy image registry paths and pull secrets from the Classic cluster to the VPC cluster.
3. Replicate PVC data from Classic volumes to VPC volumes using BRS or another backup method.
4. Apply all namespace-scoped Kubernetes resources (Deployments, Services, ConfigMaps, Secrets, PVCs) to the VPC cluster.
5. Confirm all pods reach **Running** state.

## Step 6: Configure load balancers
{: #vpc-migrate-manual-lb}

Recreate your Classic load balancer and Ingress configuration on VPC.

1. Review your Classic NodePort services, portable IP assignments, and Ingress rules.
2. Create equivalent VPC Application Load Balancers (ALBs) or Network Load Balancers (NLBs) for each service.
3. Enable and configure the VPC ALB for Ingress. Record the new VPC ALB hostnames and IP addresses — you need these for the DNS cutover step.

## Step 7: Validate and test
{: #vpc-migrate-manual-validate}

Before changing any external DNS, verify that your applications work correctly on the VPC cluster.

1. Update internal service-to-service calls to use VPC cluster endpoints.
2. Run functional, integration, and smoke tests against the VPC cluster endpoints directly.
3. Confirm storage volumes are populated and persistent data is intact.
4. Verify that all health checks, readiness probes, and liveness probes pass.

## Step 8: Update DNS and routing
{: #vpc-migrate-manual-dns}

Redirect external traffic to the VPC cluster.

1. Lower the TTL on your external DNS records at least 24 hours before the switchover.
2. When you are ready to cut over, update your external DNS records to point to the VPC ALB addresses recorded in Step 6.
3. Wait for DNS propagation and monitor for errors. Keep the Classic cluster running during propagation.

## Step 9: Cut over to VPC
{: #vpc-migrate-manual-cutover}

Perform the final data sync and complete the traffic switchover.

1. Quiesce stateful writes to your applications to prevent data divergence during the final sync.
2. Perform a final backup and restore cycle with your chosen backup method to capture any writes made after the initial data replication.
3. Confirm that the VPC cluster is serving all traffic and that no traffic is reaching the Classic cluster.

If cutover validation fails, roll back by pointing your external DNS back to the Classic cluster ALB addresses.

## Step 10: Monitor and optimize
{: #vpc-migrate-manual-monitor}

Observe the VPC cluster after cutover before deleting the Classic cluster.

1. Monitor application performance, error rates, and resource utilization for at least 24 to 48 hours.
2. Validate that autoscaling, alerts, and logging pipelines work as expected on VPC.
3. Resolve any issues while the Classic cluster is still available as a fallback.

## Next steps
{: #vpc-migrate-manual-next}

- Review the [Classic-to-VPC concept mapping](/docs/openshift?topic=openshift-vpc-migrate-concept-map) to find the VPC equivalent of each Classic resource.
- After your workloads run on VPC, [delete the Classic cluster](/docs/openshift?topic=openshift-vpc-migrate-decommission).
