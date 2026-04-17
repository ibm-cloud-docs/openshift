---

copyright:
  years: 2025, 2026
lastupdated: "2026-04-17"

keywords: openshift, virtualization, operator, hyperconverged, kubevirt

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}

# Installing the OpenShift Virtualization Operator
{: #oc-virtualization}

[Virtual Private Cloud]{: tag-vpc}
[4.17 and later]{: tag-red}
[Bare metal worker nodes only]{: tag-warm-gray}
[RHCOS only]{: tag-magenta}

After setting up storage for your cluster, install the OpenShift Virtualization Operator to enable virtual machine management capabilities.
{: shortdesc}

## Before you begin
{: #virt-install-prereqs}

Before you install the OpenShift Virtualization Operator, complete the following steps:

1. [Create a {{site.data.keyword.openshiftlong_notm}} cluster](/docs/openshift?topic=openshift-cluster-create-vpc-gen2) with the following requirements:
   - **Bare metal worker nodes**: Required for virtualization workloads
   - **RHCOS operating system**: Required (not RHEL)
   - **OVN-Kubernetes CNI**: Required for advanced networking features
   - **OpenShift 4.20 or later**: Required for full virtualization support
   - **Outbound traffic protection**: Must be disabled (can be set during cluster creation or disabled afterward)
   
   You can disable outbound traffic protection during cluster creation in the UI or CLI, or disable it after cluster creation using the command in step 3.
   {: tip}

2. [Set up storage for OpenShift Virtualization](/docs/openshift?topic=openshift-virt-storage-setup). Your cluster must have exactly one properly configured storage solution (either ODF or VPC File Storage).

3. If you didn't disable outbound traffic protection during cluster creation, disable it now.
   ```sh
   ibmcloud oc vpc outbound-traffic-protection disable -c <cluster-name>
   ```
   {: pre}
   
   This step is only needed if outbound traffic protection was not disabled during cluster creation.
   {: note}

4. Enable the default catalog sources.
   ```sh
   ibmcloud ks cluster config --admin -c <cluster-name>
   oc patch operatorhub cluster --type json -p '[{"op": "add", "path": "/spec/disableAllDefaultSources", "value": false}]'
   ```
   {: pre}

5. Verify the catalog sources are available.
   ```sh
   oc get catalogsource -n openshift-marketplace
   ```
   {: pre}

6. Confirm the OpenShift Virtualization package is available.
   ```sh
   oc get packagemanifests -n openshift-marketplace | grep kubevirt
   ```
   {: pre}

## Installing the OpenShift Virtualization Operator from the console
{: #virt-install-console}

1. Log in to the {{site.data.keyword.cloud_notm}} console and navigate to your cluster.

2. Click **OpenShift web console** to open the OpenShift console.

3. In the OpenShift console, navigate to **Ecosystem** > **OperatorHub** (or **Operators** > **OperatorHub** in earlier versions).

4. Search for **OpenShift Virtualization**.

5. Click the **OpenShift Virtualization** tile and then click **Install**.

6. On the Install Operator page, configure the following settings:
   - **Update channel**: Select the appropriate channel for your OpenShift version
   - **Installation mode**: All namespaces on the cluster (default)
   - **Installed Namespace**: openshift-cnv (default)
   - **Update approval**: Automatic (recommended)

7. Click **Install** to begin the installation.

8. Wait for the operator installation to complete. The status changes to **Succeeded** when ready.

## Installing the OpenShift Virtualization Operator from the CLI
{: #virt-install-cli}

1. Create a namespace for the OpenShift Virtualization Operator.
   ```sh
   oc create namespace openshift-cnv
   ```
   {: pre}

2. Create an OperatorGroup.
   ```yaml
   cat <<EOF | oc apply -f -
   apiVersion: operators.coreos.com/v1
   kind: OperatorGroup
   metadata:
     name: kubevirt-hyperconverged-group
     namespace: openshift-cnv
   spec:
     targetNamespaces:
     - openshift-cnv
   EOF
   ```
   {: codeblock}

3. Create a Subscription to install the operator.
   ```yaml
   cat <<EOF | oc apply -f -
   apiVersion: operators.coreos.com/v1alpha1
   kind: Subscription
   metadata:
     name: hco-operatorhub
     namespace: openshift-cnv
   spec:
     source: redhat-operators
     sourceNamespace: openshift-marketplace
     name: kubevirt-hyperconverged
     startingCSV: kubevirt-hyperconverged-operator.v4.20.8
     channel: "stable"
   EOF
   ```
   {: codeblock}

4. Verify the operator installation.
   ```sh
   oc get csv -n openshift-cnv
   ```
   {: pre}

   Wait until the `PHASE` column shows `Succeeded`.

## Creating the HyperConverged custom resource
{: #virt-install-hyperconverged}

After the operator is installed, create a HyperConverged custom resource to deploy the OpenShift Virtualization components.

### Understanding node placement
{: #virt-install-node-placement}

{{site.data.keyword.openshiftlong_notm}} clusters do not have nodes labeled as `master`. You must configure node placement policies to specify where virtualization components and VM workloads run.

#### Recommended configuration
{: #virt-install-node-placement-recommended}

- **Infrastructure components**: Deploy on VSI worker nodes for cost optimization
- **VM workloads**: Deploy on bare metal worker nodes for best performance

### Creating the HyperConverged CR from the console
{: #virt-install-hc-console}

1. In the OpenShift console, navigate to **Ecosystem** > **Installed Operators** (or **Operators** > **Installed Operators** in earlier versions).

2. Click **OpenShift Virtualization**.

3. Click the **HyperConverged** tab.

4. Click **Create HyperConverged**.

5. Configure node placement for infrastructure components:
   - Click **Infra** tab
   - Add node selectors or tolerations to target VSI nodes

6. Configure node placement for VM workloads:
   - Click **Workloads** tab
   - Add node selectors or tolerations to target bare metal nodes

7. Click **Create**.

### Creating the HyperConverged CR from the CLI
{: #virt-install-hc-cli}

Create a HyperConverged custom resource with the default configuration.

```yaml
cat <<EOF | oc apply -f -
apiVersion: hco.kubevirt.io/v1beta1
kind: HyperConverged
metadata:
  name: kubevirt-hyperconverged
  namespace: openshift-cnv
spec:
EOF
```
{: codeblock}

## Verifying the installation
{: #virt-install-verify}

1. Check the HyperConverged resource status.
   ```sh
   oc get hyperconverged -n openshift-cnv
   ```
   {: pre}

   Wait until the `PHASE` column shows `Deployed`.

2. Verify that virtualization pods are running.
   ```sh
   oc get pods -n openshift-cnv
   ```
   {: pre}

3. Check for the Virtualization menu in the OpenShift console.
   - Log in to the OpenShift console
   - Look for **Virtualization** in the main navigation menu

4. Verify storage profiles are created.
   ```sh
   oc get storageprofile
   ```
   {: pre}

5. If using VPC File Storage, configure storage profiles as described in [Setting up storage for OpenShift Virtualization](/docs/openshift?topic=openshift-virt-storage-setup#virt-storage-vpc-file-profiles).

## Troubleshooting installation issues
{: #virt-install-troubleshoot}

### HyperConverged resource fails to deploy
{: #virt-install-ts-hc-fail}

If the HyperConverged resource fails to deploy with node placement errors:

1. Check your node labels.
   ```sh
   oc get nodes --show-labels
   ```
   {: pre}

2. Update the HyperConverged CR with correct node selectors.
   ```sh
   oc edit hyperconverged kubevirt-hyperconverged -n openshift-cnv
   ```
   {: pre}

3. Review the HyperConverged operator logs.
   ```sh
   oc logs -n openshift-cnv -l name=hyperconverged-cluster-operator
   ```
   {: pre}

### Operator installation fails
{: #virt-install-ts-operator-fail}

If the operator installation fails:

1. Verify catalog sources are enabled.
   ```sh
   oc get catalogsource -n openshift-marketplace
   ```
   {: pre}

2. Check operator subscription status.
   ```sh
   oc get subscription -n openshift-cnv
   ```
   {: pre}

3. Review operator logs.
   ```sh
   oc logs -n openshift-cnv -l app=kubevirt-hyperconverged-operator
   ```
   {: pre}

## Next steps
{: #virt-install-next-steps}

After installing OpenShift Virtualization:

- [Create and manage virtual machines](https://docs.redhat.com/en/documentation/openshift_container_platform/4.20/html/virtualization/virtual-machines){: external}

- [Set up VM templates and images](https://docs.redhat.com/en/documentation/openshift_container_platform/4.20/html/virtualization/virtual-machines#virt-creating-vms-from-rh-images-overview){: external}

For complete installation instructions, see [Installing OpenShift Virtualization](https://docs.redhat.com/en/documentation/openshift_container_platform/4.20/html-single/virtualization/index#installing-virt){: external} in the Red Hat documentation.
