---

copyright:
  years: 2026, 2026
lastupdated: "2026-06-01"

keywords: openshift, virtualization service, rovs, addon, openshift virtualization, hyperconverged, nmstate, node maintenance

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}

# Managing the OpenShift Virtualization add-on
{: #rovs-addon-virtualization}

[Virtual Private Cloud]{: tag-vpc}
[4.20 and later]{: tag-red}
[Bare metal worker nodes only]{: tag-warm-gray}
[RHCOS only]{: tag-magenta}

The `openshift-virtualization` add-on provides a one-click experience to set up the virtualization platform on Red Hat OpenShift on IBM Cloud for VPC with Satellite-enabled services (ROVS) clusters. This add-on is automatically enabled by default on all ROVS clusters.
{: shortdesc}

This service is currently available as a beta release. Access is controlled by an allowlist. During the beta period, only console-based cluster creation is supported.
{: beta}


## Understanding the OpenShift Virtualization add-on
{: #rovs-addon-virt-about}

The OpenShift Virtualization add-on orchestrates the deployment and management of the following operators to enable virtual machine capabilities in your ROVS cluster:

OpenShift Virtualization Operator (Hyperconverged)
:   Provides the core virtualization capabilities for running and managing virtual machines. For more information, see [Installing OpenShift Virtualization](https://docs.redhat.com/en/documentation/openshift_container_platform/4.20/html/virtualization/installing){: external}.

NMState Operator
:   Manages network configuration for virtual machines and nodes. For more information, see [About the Kubernetes NMState Operator](https://docs.redhat.com/en/documentation/openshift_container_platform/4.20/html/networking_operators/k8s-nmstate-about-the-k8s-nmstate-operator){: external}.

Node Maintenance Operator
:   Handles node maintenance operations for virtual machine workloads. For more information, see [Node Maintenance Operator](https://docs.redhat.com/en/documentation/workload_availability_for_red_hat_openshift/23.2/html-single/remediation_fencing_and_maintenance/index#node-maintenance-operator){: external}.

Installation of these operators from Red Hat OperatorHub is blocked on ROVS clusters. The add-on manages all operator installations and updates.
{: important}

## Add-on characteristics
{: #rovs-addon-virt-characteristics}

The OpenShift Virtualization add-on has the following characteristics:

Automatic enablement
:   The add-on is automatically enabled when you create a ROVS cluster. You cannot manually enable the add-on through the CLI or console.

Cannot be disabled
:   Disabling the add-on is not supported. The option is not available in the console, and attempting to disable it through the CLI results in an error.

No configuration options
:   The add-on has no user-configurable parameters.

Version binding
:   The add-on version is bound to the ROVS cluster version (for example, 4.20). The add-on supports the current minor version and the next minor version (n+1). For example, add-on version 4.20 can be used with ROVS versions 4.20 and 4.21.

Automatic patch updates
:   Patch updates are applied automatically to your cluster using the **Automatic Approval** strategy. IBM notifies you at least one week before production rollout with change details. All dependent operators are updated automatically if new versions exist in the mirrored operator catalog. The add-on uses the `stable` channel for all operator updates.

Manual version upgrades
:   To upgrade the add-on to a newer version (for example, from 4.19 to 4.20), you must first upgrade your ROVS cluster to the target version, then manually update the add-on version using the CLI command `ibmcloud ks cluster addon update openshift-virtualization --cluster <cluster_name_or_id> --version <version>`.

Update channel
:   The add-on uses the `stable` channel for updates, which provides Z-stream updates for bug fixes and security issues.

Version compatibility
:   Each add-on version supports the current ROVS version (n) and the next minor version (n+1). For example, add-on version 4.19 supports ROVS versions 4.19 and 4.20.

Custom catalog
:   A custom catalog with mirrored dependent operators is set up automatically during add-on enablement and is placed in the `openshift-marketplace` namespace.

## Installed resources
{: #rovs-addon-virt-resources}

When the add-on is enabled, the following resources are created:

Parent operator namespace
:   The `ibm-openshift-virt-operator` namespace contains all resources related to the parent operator, including a custom resource of type `ibmopenshiftvirtualizations.openshiftvirt.ibm.io`.

Custom catalog
:   The custom catalog is placed in the `openshift-marketplace` namespace.

Dependent operators
:   The parent operator acts as a meta operator and installs the following dependent operators during reconciliation:
    - OpenShift Virtualization (in the `openshift-cnv` namespace)
    - NMState (in the `openshift-nmstate` namespace)
    - Node Maintenance Operator (in the `openshift-operators` namespace)

## Viewing add-on information
{: #rovs-addon-virt-view}

If the feature flag is enabled for your account, you can view information about the OpenShift Virtualization add-on by using the CLI. If the feature flag is not enabled, use the console and cluster details to review add-on status instead.

### Listing installed add-ons
{: #rovs-addon-virt-list}

List all add-ons that are installed in your ROVS cluster.

```sh
ibmcloud ks cluster addon ls --cluster <cluster_name_or_id>
```
{: pre}

Example output:

```sh
Name                       Version   Health State   Health Status
ibm-storage-operator       1.0       normal         Addon Ready. For more info: http://ibm.biz/addon-state (H1500)
openshift-virtualization   4.20      normal         Addon Ready. For more info: http://ibm.biz/addon-state (H1500)
```
{: screen}

### Getting add-on details
{: #rovs-addon-virt-get}

If the feature flag is enabled for your account, get detailed information about the OpenShift Virtualization add-on.

```sh
ibmcloud ks cluster addon get --addon openshift-virtualization --cluster <cluster_name_or_id>
```
{: pre}

Example output:

```sh
name:            openshift-virtualization
Version:         4.20
Health State:    normal
Health Status:   Addon Ready. For more info: http://ibm.biz/addon-state (H1500)
```
{: screen}

### Listing available add-on versions
{: #rovs-addon-virt-versions}

If the feature flag is enabled for your account, list the available versions of the OpenShift Virtualization add-on.

```sh
ibmcloud ks cluster addon versions --addon openshift-virtualization
```
{: pre}

Example output:

```sh
Name                       Version   Supported Kubernetes Range   Supported OpenShift Range   Kubernetes Default   OpenShift Default
openshift-virtualization   4.19      unsupported                  >=4.19.0 <4.21.0            -                    >=4.19.0 <4.21.0
openshift-virtualization   4.20      unsupported                  >=4.20.0 <4.22.0            -                    >=4.20.0 <4.22.0
```
{: screen}

This output shows which ROVS versions are supported by each add-on version.

### Checking for configuration options
{: #rovs-addon-virt-options}

If the feature flag is enabled for your account, you can confirm that the OpenShift Virtualization add-on does not support configuration options.

```sh
ibmcloud ks cluster addon options --addon openshift-virtualization
```
{: pre}

Example output:

```sh
FAILED
No addon installation options are available for openshift-virtualization.
```
{: screen}

## Updating the add-on
{: #rovs-addon-virt-update}

The OpenShift Virtualization add-on supports two types of updates:

### Automatic patch updates
{: #rovs-addon-virt-patch-updates}

Patch updates (such as from 4.20.1 to 4.20.2) are applied automatically to all clusters. These updates include bug fixes and security patches. IBM provides at least one week advance notification before rolling out patch updates to production.

The automatic patch update process does the following:
1. Restarts the parent operator
2. Reconciles the catalog source
3. Updates all child operators based on the `stable` channel subscription

### Manual version upgrades
{: #rovs-addon-virt-version-upgrades}

To upgrade the OpenShift Virtualization add-on to a newer minor version (such as from 4.19 to 4.20), you must first upgrade your ROVS cluster to the target version. If the feature flag is not enabled for your account, contact IBM Support before you attempt the CLI update.

1. Upgrade your ROVS cluster to the target version. For more information, see [Updating clusters](/docs/openshift?topic=openshift-update).

2. After the cluster upgrade is complete, update the add-on to the matching version.

   ```sh
   ibmcloud ks cluster addon update openshift-virtualization --cluster <cluster_name_or_id> --version <version>
   ```
   {: pre}

   For example, to update to version 4.20:

   ```sh
   ibmcloud ks cluster addon update openshift-virtualization --cluster my-rovs-cluster --version 4.20
   ```
   {: pre}

It is highly recommended to update the add-on version to match your cluster version for optimal compatibility and support.
{: important}

## Disabling the add-on
{: #rovs-addon-virt-disable}

Disabling the OpenShift Virtualization add-on is not supported on ROVS clusters (Phase 1). The add-on is a core component of the Virtualization Service and cannot be removed. If the feature flag is enabled for your account and you attempt the CLI command, the command results in an error.

```sh
ibmcloud ks cluster addon disable openshift-virtualization --cluster <cluster_name_or_id>
```
{: pre}

Support for add-on uninstallation is planned for standard ROKS clusters in Phase 2.
{: note}

## Troubleshooting the add-on
{: #rovs-addon-virt-troubleshoot}

If you encounter issues with the OpenShift Virtualization add-on, gather the following information before opening a support case.

### Gathering add-on information
{: #rovs-addon-virt-gather-info}

Run the following commands to gather details about the OpenShift Virtualization add-on and its dependent operators.

1. Get the IBM OpenShift Virtualization custom resource.

   ```sh
   oc get ibmopenshiftvirtualizations.openshiftvirt.ibm.io -n ibm-openshift-virt-operator -o yaml
   ```
   {: pre}

2. List all resources in the parent operator namespace.

   ```sh
   oc get all -n ibm-openshift-virt-operator
   ```
   {: pre}

3. Check the OpenShift Virtualization operator status.

   ```sh
   oc get csv -n openshift-cnv
   ```
   {: pre}

4. Get the HyperConverged resource details.

   ```sh
   oc get hco -n openshift-cnv kubevirt-hyperconverged -o yaml
   ```
   {: pre}

5. List all resources in the OpenShift Virtualization namespace.

   ```sh
   oc get all -n openshift-cnv
   ```
   {: pre}

6. Check the NMState operator status.

   ```sh
   oc get csv -n openshift-nmstate
   ```
   {: pre}

7. List all resources in the NMState namespace.

   ```sh
   oc get all -n openshift-nmstate
   ```
   {: pre}

8. Get the NMState resource details.

   ```sh
   oc get nmstate nmstate -o yaml
   ```
   {: pre}

9. List NodeNetworkConfigurationPolicy resources.

   ```sh
   oc get nncp
   ```
   {: pre}

10. Check the Node Maintenance Operator status.

    ```sh
    oc get csv -n openshift-operators
    ```
    {: pre}

11. List all resources in the operators namespace.

    ```sh
    oc get all -n openshift-operators
    ```
    {: pre}

12. Check the custom catalog source.

    ```sh
    oc get catalogsource custom-redhat-operators-openshiftvirt -n openshift-marketplace
    ```
    {: pre}

13. List package manifests from the custom catalog.

    ```sh
    oc get packagemanifests -n openshift-marketplace | grep "Custom Redhat Operators for Openshift Virtualization"
    ```
    {: pre}

### Opening a support case
{: #rovs-addon-virt-support}

If your issue is not resolved, open a support case and include the output from the troubleshooting commands. For more information, see [Getting support](/docs/get-support).

## Next steps
{: #rovs-addon-virt-next}

- [Deploy your first virtual machine](/docs/openshift?topic=openshift-rovs-getting-started#rovs-gs-first-vm)
- [Learn about managing Virtualization Service clusters](/docs/openshift?topic=openshift-rovs-manage)
- [Explore OpenShift Virtualization documentation](https://docs.redhat.com/en/documentation/openshift_container_platform/4.20/html/virtualization){: external}
