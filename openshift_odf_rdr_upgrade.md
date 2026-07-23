---

copyright:
  years: 2026
lastupdated: "2026-07-23"

keywords: openshift data foundation, ODF, disaster recovery, upgrade, ODF-DR, regional disaster recovery, RDR

subcollection: openshift

content-type: tutorial
services: openshift, vpc
account-plan: paid
completion-time: 2h

---


{{site.data.keyword.attribute-definition-list}}


# Upgrading your OpenShift Data Foundation Regional Disaster Recovery environment
{: #openshift_odf_rdr_upgrade}
{: toc-content-type="tutorial"}
{: toc-services="openshift, vpc"}
{: toc-completion-time="2h"}

[Virtual Private Cloud]{: tag-vpc}
[4.21 and later]{: tag-red}

Learn when and how to upgrade the components of your OpenShift Data Foundation (ODF) Regional Disaster Recovery (RDR) environment, including {{site.data.keyword.openshiftlong_notm}}, the Advanced Cluster Management (ACM) add-on, ODF, and the ODF-DR operator.
{: shortdesc}

## Before you begin
{: #odf-rdr-upgrade-before}

Upgrade your ODF-RDR environment when a new version of {{site.data.keyword.openshiftlong_notm}}, ACM, or ODF is available, or when any component is old or approaching deprecation. Failure to upgrade may result in future outages.

Wait until upgrade versions for all three components are available before you start. This reduces the overall upgrade effort.
{: tip}

## Upgrading the hub cluster
{: #odf-rdr-upgrade-roks-hub}
{: step}

[Hub cluster]{: tag-blue}

Upgrade both the control plane and worker nodes on the hub cluster before upgrading any add-ons.

1. Update the cluster master to the target version.
   ```sh
   ibmcloud oc cluster master update --cluster <cluster_name> --version <version>
   ```
   {: pre}

2. Wait a few minutes, then confirm that the master update is complete.
   ```sh
   ibmcloud oc cluster ls
   ```
   {: pre}

3. List the worker nodes and note the ID of each node to update.
   ```sh
   ibmcloud oc worker ls --cluster <cluster_name>
   ```
   {: pre}

4. Replace each worker node to update it to the same version as the master. Repeat for each worker node.
   ```sh
   ibmcloud oc worker replace --cluster <cluster_name> --worker <worker_node_id> --update
   ```
   {: pre}

5. Confirm that all worker nodes are running the target version and show a **Ready** status.
   ```sh
   ibmcloud oc worker ls --cluster <cluster_name>
   ```
   {: pre}

## Upgrading the managed clusters
{: #odf-rdr-upgrade-roks-spoke}
{: step}

[Managed cluster]{: tag-warm-gray}

Because the managed clusters run ODF, follow the ODF-aware node upgrade procedure, which covers both the {{site.data.keyword.openshiftlong_notm}} and ODF upgrades. For detailed instructions, see [Updating or replacing VPC worker nodes that use ODF](/docs/openshift?topic=openshift-openshift-storage-update-vpc&interface=ui).

## Upgrading ACM on the hub cluster
{: #odf-rdr-upgrade-acm}
{: step}

[Hub cluster]{: tag-blue}

After all clusters are running the target {{site.data.keyword.openshiftlong_notm}} version, upgrade the ACM add-on on the hub cluster.

1. Upgrade the ACM add-on to the target version. Replace `<cluster_id>` with your hub cluster ID and `<version>` with the target ACM version (for example, `2.16`).
   ```sh
   ibmcloud oc cluster addon update acm --cluster <cluster_id> --version <version>
   ```
   {: pre}

2. Confirm that the add-on updated successfully. In the output, verify the ACM add-on shows the target version.
   ```sh
   ibmcloud oc cluster addon ls --cluster <cluster_id>
   ```
   {: pre}

## Upgrading the ODF-DR operator on the hub cluster
{: #odf-rdr-upgrade-odf-dr}
{: step}

[Hub cluster]{: tag-blue}

After ODF is upgraded on all managed clusters, upgrade the ODF Multicluster Orchestrator Operator on the hub cluster.

1. Confirm the current subscription channel for the ODF Multicluster Orchestrator operator.
   ```sh
   oc get subscription odf-multicluster-orchestrator -n openshift-operators -o jsonpath='{.spec.channel}'
   ```
   {: pre}

2. Patch the subscription to the target channel. Replace `stable-4.21` with the target version channel.
   ```sh
   oc patch subscription odf-multicluster-orchestrator -n openshift-operators \
     --type merge -p '{"spec":{"channel":"stable-4.21"}}'
   ```
   {: pre}

3. Confirm that the install plan for the new version has been created and approved.
   ```sh
   oc get installplan -n openshift-operators
   ```
   {: pre}

4. Verify that the CSV for the target version shows `Succeeded` status.
   ```sh
   oc get csv -n openshift-operators | grep odf-multicluster
   ```
   {: pre}

5. Verify that the ODF Multicluster Orchestrator operator pods are running in the `openshift-operators` namespace.
   ```sh
   oc get pods -n openshift-operators | grep -i odf
   ```
   {: pre}

   Confirm that both `odf-multicluster-console` and `odfmo-controller-manager` pods show `Running` status.

6. Verify that the `DRPolicy` is validated after reconciliation.
   ```sh
   oc get drpolicy -A
   ```
   {: pre}

   Confirm that the `VALIDATED` column shows `True` for all policies. If not, run the following command to check the status conditions.
   ```sh
   oc describe drpolicy <drpolicy_name>
   ```
   {: pre}

7. Verify that the `MirrorPeer` has finished reconciling.
   ```sh
   oc get mirrorpeers -A
   ```
   {: pre}

   Confirm that the `Phase` shows `ExchangedSecret`. If it shows `ExchangingSecret`, verify Submariner connectivity before proceeding.

For more information, see [Installing ODF Multicluster Orchestrator](https://docs.redhat.com/en/documentation/red_hat_openshift_data_foundation/4.21/html-single/configuring_openshift_data_foundation_disaster_recovery_for_openshift_workloads/index#installing-odf-multicluster-orchestrator_mdr){: external} in the Red Hat documentation.

## Upgrading optional operators
{: #odf-rdr-upgrade-optional-operators}
{: step}

If your environment includes the following operators, upgrade them after the ODF-DR operator.

GitOps
:   For more information, see [GitOps overview](https://docs.redhat.com/en/documentation/red_hat_advanced_cluster_management_for_kubernetes/2.15/html/gitops/gitops-overview){: external} in the Red Hat documentation.

OADP
:   For more information, see [Introduction to OpenShift API for data protection](https://docs.redhat.com/en/documentation/openshift_container_platform/4.21/html/backup_and_restore/oadp-application-backup-and-restore#oadp-introduction){: external} in the Red Hat documentation.

## Next steps
{: #odf-rdr-upgrade-next}

After completing all upgrades, verify that the environment is healthy and that disaster recovery is functioning correctly. For detailed verification steps, see [Verifying your ODF Regional Disaster Recovery configuration](/docs/openshift?topic=openshift-openshift_odf_rdr_verify).
