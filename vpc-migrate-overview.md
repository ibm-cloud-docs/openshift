---

copyright:
  years: 2026, 2026
lastupdated: "2026-10-29"

keywords: openshift, classic, vpc, migrate, migration, overview, replatform, limitations, add-ons, version support, eligible clusters

subcollection: openshift

content-type: overview

---

{{site.data.keyword.attribute-definition-list}}

# Migrating from Classic to VPC
{: #vpc-migrate-overview}

[Classic infrastructure]{: tag-classic-inf}

Migrate your {{site.data.keyword.openshiftlong_notm}} workloads from Classic infrastructure to VPC to take advantage of improved security, networking flexibility, and better performance.
{: shortdesc}

## Why should I migrate from Classic to VPC?
{: #vpc-migrate-overview-why}
{: faq}

{{site.data.keyword.cloud_notm}} VPC is the next generation of cloud infrastructure. It builds on the foundation of Classic infrastructure to meet evolving workload demands, with greater flexibility, performance, connectivity, security, and control.

Classic infrastructure is a legacy compute platform. New Classic cluster creation is restricted on a per-region basis. Accounts that do not already have a Classic cluster in a region can no longer create new Classic clusters there. VPC is the strategic direction for new workloads. For more information, see [Classic cluster creation restrictions](/docs/openshift?topic=openshift-classic-create-restriction).

{{site.data.keyword.openshiftlong_notm}} runs natively on VPC, which gives your teams a secure, integrated foundation for modern containerized applications. When you migrate, your clusters gain the following benefits.

- Worker nodes run within your VPC subnets, which keeps your workloads private.
- VPC Application Load Balancers integrate with Kubernetes Ingress, which simplifies application delivery.
- Encrypted VPC Block Storage and snapshots protect and persist your data, and provision faster than Classic storage.
- VPC routing keeps cluster-to-cluster and service-to-service traffic private.
- Private cluster endpoints keep the API server off the public internet.
- Security groups and private endpoints strengthen your network security.
- A modern API simplifies infrastructure management.

## What do I need before I start?
{: #vpc-migrate-overview-prereqs}
{: faq}

Complete the following prerequisites before you open the migration wizard. Some of them take time to provision, so do not wait until you are in the middle of the wizard.

- Ensure that you have at least the **Operator** (`containers-kubernetes.cluster.operate`) {{site.data.keyword.iamlong}} platform access role for the {{site.data.keyword.containerlong_notm}} service on both the Classic cluster and the VPC cluster. See [Assigning cluster access](/docs/openshift?topic=openshift-iam-platform-access-roles).
- Ensure that your Classic cluster runs a supported version of Kubernetes or {{site.data.keyword.openshiftshort}}. If the version is at end of support, [update it first](/docs/openshift?topic=openshift-update).
- Install and update the {{site.data.keyword.cloud_notm}} CLI and the {{site.data.keyword.openshiftlong_notm}} plug-in. See [Installing the CLI](/docs/openshift?topic=openshift-cli-install).
- Provision an {{site.data.keyword.cos_full_notm}} (COS) instance in the same account. The migration service uses COS to store generated metadata and migration plans.
- Provision an {{site.data.keyword.cloud_notm}} Backup and Recovery Service (BRS) instance in the same resource group as your Classic cluster. BRS is the only supported method for migrating workload and storage data. You select the BRS instance during the workload migration step. See [Migrate workloads](/docs/openshift?topic=openshift-vpc-migrate-workloads#vpc-migrate-workloads-brs).
- If your Classic cluster connects to on-premises networks by using Classic VPN or Direct Link 1.0, set up the equivalent VPC connectivity before you start workload migration. The migration service does not migrate these connections. See [Plan private connectivity](/docs/openshift?topic=openshift-vpc-migrate-plan#vpc-migrate-plan-connectivity).
- Ensure that your Classic cluster is in a multizone region (MZR). If your cluster is in a single-zone region (SZR), see [Which clusters are eligible for migration?](#vpc-migrate-overview-limitations-cluster) before you continue.
- Verify that your account has enough quota for the VPC resources that the migration creates. Check all quotas in [VPC quotas](/docs/vpc?topic=vpc-quotas){: external}.

## Which clusters are eligible for migration?
{: #vpc-migrate-overview-limitations-cluster}
{: faq}

The migration wizard supports only some Classic clusters. Your cluster must meet all of the following requirements.

- It is a standard cluster. Free clusters and {{site.data.keyword.satelliteshort}} location clusters cannot be migrated.
- It runs a supported version of Kubernetes or {{site.data.keyword.openshiftshort}}.
- It is in a multizone region (MZR). If your cluster is in a single-zone region (SZR), you cannot use the migration wizard.

## What is migrated automatically and what is not?
{: #vpc-migrate-overview-limitations}
{: faq}

### Which add-ons are migrated?
{: #vpc-migrate-overview-limitations-addons}

The migration service migrates a subset of managed add-ons. You must re-enable the other add-ons on the VPC cluster after migration.

| Add-on | Migrated automatically? | What you need to do |
|--------|-------------------------|---------------------|
| `cluster-autoscaler` | Yes | No action required. |
| `image-key-synchronizer` | Yes | No action required. |
| `static-route` | Yes | No action required. |
| `alb-oauth-proxy` | No | Re-enable the add-on after migration and reconfigure your App ID credentials. Workloads that use the ALB OAuth Proxy do not function until you re-enable it. See [Enabling the ALB OAuth Proxy add-on](/docs/openshift?topic=openshift-cl-add-ons-alb-oauth-proxy). |
| `istio` | No | Re-enable the add-on after migration. Pods in Istio-managed namespaces might fail to start until you re-enable Istio and reapply the namespace label. See [Setting up Istio](/docs/openshift?topic=openshift-cl-add-ons-istio). |
{: caption="Add-on migration behavior for Kubernetes clusters" caption-side="bottom"}
{: class="simple-tab-table"}
{: tab-title="Kubernetes"}
{: tab-group="vpc-migrate-addons"}
{: #vpc-migrate-addons-k8s}

| Add-on | Migrated automatically? | What you need to do |
|--------|-------------------------|---------------------|
| `cluster-autoscaler` | Yes | No action required. |
| `image-key-synchronizer` | Yes | No action required. |
| `static-route` | Yes | No action required. |
| `openshift-data-foundation` | No | Install ODF on the VPC cluster before you start the workload migration step. See [VPC: Installing ODF](/docs/openshift?topic=openshift-deploy-odf-vpc). |
| `openshift-ai` | No | Reinstall the add-on after migration. OpenShift AI workloads that use cluster-local services are unavailable until you reinstall it. See [Setting up OpenShift AI](/docs/openshift?topic=openshift-cl-add-ons-openshift-ai). |
| `hpcs-router` | No | Re-enable the add-on by running the [`ibmcloud oc cluster addon enable hpcs-router`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-addon-enable-hpcs-router-cli) command, and update the instance bindings after migration. Workloads that rely on HPCS-managed secrets cannot retrieve keys until you do. |
{: caption="Add-on migration behavior for OpenShift clusters" caption-side="bottom"}
{: class="simple-tab-table"}
{: tab-title="OpenShift"}
{: tab-group="vpc-migrate-addons"}
{: #vpc-migrate-addons-openshift}

The `vpc-file-csi-driver` add-on is not present on Classic clusters. The migration tool enables it by default on the VPC cluster.
{: note}

### Which network policies are migrated?
{: #vpc-migrate-overview-limitations-networking}

The migration service does not migrate Global Network Policies (GNPs). Moving them to VPC security groups is your responsibility. To create equivalent allow rules in VPC, see [Controlling traffic with VPC security groups](/docs/vpc?topic=vpc-using-security-groups){: external}.

The migration service migrates only namespace-scoped network policies, as part of the workload migration step.

- Kubernetes network policies: Only policies that are created within a migrated namespace are migrated as is from the Classic cluster.
- Calico network policies: Only policies that are created within a migrated namespace are migrated as is from the Classic cluster.

NodePort services work on VPC, but the underlying implementation differs from Classic. Review any firewall or security group rules that target NodePort ranges.

### What happens to my storage?
{: #vpc-migrate-overview-limitations-storage}

The migration service provides the Classic-to-VPC storage class mappings. You can review them in the migration plan or in the console during the workload migration step. For more information, see [Classic-to-VPC concept mapping](/docs/openshift?topic=openshift-vpc-migrate-concept-map#vpc-migrate-concept-map-storage).

| Storage type | Migrated automatically? | What you need to do |
|--------------|-------------------------|---------------------|
| Classic Block Storage | Yes | No action required. PVC data is copied to new VPC Block Storage volumes by using BRS. Classic and VPC volumes exist at the same time. The Classic PVs and PVCs are not deleted until you delete the Classic cluster. |
| Classic File Storage (NFS) | Yes | No action required. PVC data is copied to new VPC File Storage volumes by using BRS. Classic File Storage for Classic is not supported on VPC — the migrated data is served from VPC File Storage. The Classic PVs and PVCs are not deleted until you delete the Classic cluster. |
| Object Storage (COS) | Not needed | Update any cluster-side credentials after migration. COS buckets are not cluster-specific. |
| Portworx and third-party storage | No | Install Portworx on the VPC cluster before you start the workload migration step. See [Installing Portworx in your cluster](/docs/openshift?topic=openshift-storage_portworx_deploy). |
| OpenShift Data Foundation (ODF) storage classes and PVCs (OpenShift clusters only) | No | Install ODF on the VPC cluster before you start the workload migration step. See [VPC: Installing ODF](/docs/openshift?topic=openshift-deploy-odf-vpc). |
{: caption="Storage migration behavior" caption-side="bottom"}

### What workload considerations should I know about?
{: #vpc-migrate-overview-limitations-workloads}

System namespaces
:   `kube-system`, `ibm-system`, `calico-system`, and other IBM-managed namespaces are excluded from workload migration automatically.

Stateful applications
:   A final data sync during cutover captures writes made after the initial migration. Plan a maintenance window for this sync. See [Cut over and validate](/docs/openshift?topic=openshift-vpc-migrate-cutover#vpc-migrate-cutover-sync).

Classic-specific annotations
:   Resources such as load balancers with Classic NLB annotations will be translated to VPC-supported equivalents. After migration, review the migration plan for any actionable notifications related to networking resources, such as LoadBalancer Services or Ingress objects, and perform the recommended actions accordingly.

Ingress subdomains
:   Classic and VPC clusters each have their own IBM-managed Ingress subdomain. After cutover, update the Ingress resources, application configuration, environment variables, and CI/CD pipelines that reference the Classic subdomain.

COS CSI add-on
:   If your cluster uses the legacy s3fs Flex driver, use BRS to migrate those namespaces before you migrate other workloads.

Global resources
:   The migration service automatically migrates the NodeLocal DNS Cache ConfigMap, the CoreDNS and DNS Operator configuration, the Kubernetes Metrics Server ConfigMap, the Ingress controller configuration, and MTU settings. For {{site.data.keyword.openshiftlong_notm}} clusters, it also migrates the cluster monitoring configuration, custom OLM operator subscriptions, and the global pull secret if you modified it. You do not need to re-create these resources.

Customer cluster-scoped resources
:   Custom cluster-scoped objects such as custom `ClusterRole`, `ClusterRoleBinding`, custom `SecurityContextConstraints`, `PriorityClass`, `CustomResourceDefinition`, and admission webhooks are not automatically migrated. You can export and apply them to your VPC cluster before migrating workloads. See [Migrating cluster-scoped resources](/docs/openshift?topic=openshift-vpc-migrate-workloads#vpc-migrate-workloads-cluster-scoped).

## How does the migration work?
{: #vpc-migrate-overview-how}
{: faq}

Migration is a phased, non-disruptive process. Your Classic cluster continues to run and serve traffic throughout. The migration service analyzes your Classic cluster, generates a VPC configuration, provisions a new VPC cluster, and automatically migrates global resources and IAM policies. It then guides you through migrating your workloads. You cut over traffic to the VPC cluster yourself.

You can open the migration wizard from the Migration hub or from the Containers page in the {{site.data.keyword.cloud_notm}} console. The wizard tracks your progress through each step in the left navigation panel. To open the wizard, see [Step 1: Open the migration wizard](/docs/openshift?topic=openshift-vpc-migrate-quickstart#vpc-migrate-quickstart-open).

For scripted or automated migrations, you can use the GraphQL API at `/graphql` with Bearer token authentication, or the ibmcloud oc CLI commands, instead of the wizard.

## What are the migration steps?
{: #vpc-migrate-overview-phases}
{: faq}

The migration wizard has two phases. In phase 1, you assess your Classic cluster, create the VPC cluster, and migrate your workloads. In phase 2, you cut over traffic to the VPC cluster. The steps in the following table match the steps in the migration wizard.

| Phase | Step | Topics | What happens |
|-------|------|--------|--------------|
| Phase 1 | Step 1: Assess | [Assess your Classic cluster](/docs/openshift?topic=openshift-vpc-migrate-assess) and [Plan your VPC environment](/docs/openshift?topic=openshift-vpc-migrate-plan) | Select a COS instance, run the assessment to generate VPC metadata, and review the proposed VPC cluster configuration. Use the Plan topic to adjust the configuration before you create the cluster. |
| Phase 1 | Step 2: Create | [Create the VPC cluster](/docs/openshift?topic=openshift-vpc-migrate-create) and [Monitor global resource migration](/docs/openshift?topic=openshift-vpc-migrate-global-resources) | Provision the VPC cluster from the generated metadata. Infrastructure migration for IAM policies, add-ons, and global resources starts automatically. The wizard shows a checkmark on this step when all background sub-operations are complete. |
| Phase 1 | Step 3: Migrate | [Migrate workloads](/docs/openshift?topic=openshift-vpc-migrate-workloads) | Choose a backup and recovery instance and create migration plans to move workloads to the VPC cluster, namespace by namespace. |
| Phase 2 | Cutover | [Cut over and validate](/docs/openshift?topic=openshift-vpc-migrate-cutover) | Redirect live traffic to the VPC cluster, validate your workloads, observe a stabilization period, and complete the finish migration checklist. |
{: caption="Classic-to-VPC migration phases and steps" caption-side="bottom"}

After you finish the wizard, [delete the Classic cluster](/docs/openshift?topic=openshift-vpc-migrate-decommission). Deleting the cluster is a manual process that is not part of the wizard.

## What happens to my IAM and access configuration?
{: #vpc-migrate-faq-iam}
{: faq}

IAM credentials, service IDs, and access groups are not cluster-specific, so migration does not affect them. Image pull secrets are migrated automatically during the workload migration step. The Classic infrastructure API key is not reused on VPC, so you must verify the IAM API key for VPC infrastructure separately. See [Assigning cluster access](/docs/openshift?topic=openshift-iam-platform-access-roles).

## How does BRS copy my data?
{: #vpc-migrate-faq-brs}
{: faq}

BRS copies PVC data from Classic Block and File storage to new VPC volumes. Classic and VPC volumes exist at the same time during migration. The migration service never deletes or unmounts your Classic storage. For more information about BRS, see [What is Backup and Recovery?](/docs/backup-recovery?topic=backup-recovery-about-baas){: external}.

## How do I cut over traffic and delete the Classic cluster?
{: #vpc-migrate-faq-cutover}
{: faq}

Cutting over traffic and deleting the Classic cluster are manual processes. The migration wizard does not do them for you.
{: important}

After all workloads run on the VPC cluster, you quiesce stateful writes, perform a final data sync, update your external DNS to point to the VPC cluster ALB addresses, and validate your applications. Keep the Classic cluster running for a stabilization period before you finish the wizard. When you click **Finish migration**, a checklist confirms that all cutover steps are complete. The wizard is complete after you confirm the checklist.

Deleting the Classic cluster is a separate step after the wizard. Deleting the Classic cluster removes all associated worker nodes, VLANs (if they are not shared), and load balancers, and it cannot be undone. See [Cut over and validate](/docs/openshift?topic=openshift-vpc-migrate-cutover) and [Deleting Classic clusters](/docs/openshift?topic=openshift-vpc-migrate-decommission).

## Is my Classic cluster affected while migration is in progress?
{: #vpc-migrate-faq-classic-impact}
{: faq}

Migration is non-disruptive. Your Classic cluster continues to run and serve traffic throughout. The only planned downtime is the final data sync during cutover, when stateful applications are temporarily quiesced to prevent data divergence. You control when that window occurs. The length of the window depends on your data volume.

You cannot stop a workload migration after it starts. If you encounter issues, do not delete the Classic cluster. It remains fully operational and continues to serve traffic. If cutover validation fails, roll back by pointing your DNS back to the Classic cluster ALB addresses.

## Does migration affect my pricing or license?
{: #vpc-migrate-faq-pricing}
{: faq}

You continue to pay for your Classic cluster and its worker nodes, load balancers, and storage until you delete it. After you create the VPC cluster, you also pay for its worker nodes and associated VPC resources. Both clusters run simultaneously during the migration period. Delete the Classic cluster as soon as you complete cutover and validation to avoid paying for both environments.

If you use {{site.data.keyword.cloud_notm}} Backup and Recovery Service (BRS) to migrate your storage data, BRS usage charges apply while the service is active. For pricing details, see [IBM Cloud Backup and Recovery pricing](https://cloud.ibm.com/backup-recovery/pricing){: external}. For general billing information, see the [BRS billing FAQ](/docs/backup-recovery?topic=backup-recovery-faq#baas-billing){: external}.

Migration does not affect your Red Hat OpenShift licenses. OpenShift license charges are tied to your worker node hours, not to the cluster itself, so the license transitions automatically when you move workloads to the VPC cluster.

## Next steps
{: #vpc-migrate-overview-next}

- To try the migration wizard, follow the [Migration wizard quickstart guide](/docs/openshift?topic=openshift-vpc-migrate-quickstart).
- To begin, [assess your Classic cluster](/docs/openshift?topic=openshift-vpc-migrate-assess) and generate the VPC configuration metadata.
- To find the VPC equivalent of a Classic concept, see [Classic-to-VPC concept mapping](/docs/openshift?topic=openshift-vpc-migrate-concept-map).
