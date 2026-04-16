---

copyright:
  years: 2026, 2026

lastupdated: "2026-04-16"

keywords: openshift virtualization, hyperconverged, node placement, kubevirt, openshift-cnv

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why does the HyperConverged resource deployment fail?
{: #ts-virt-hyperconverged-deployment-fails}
{: troubleshoot}
{: support}

[Virtual Private Cloud]{: tag-vpc}
[4.17 and later]{: tag-red}
[Bare metal worker nodes only]{: tag-warm-gray}
[RHCOS only]{: tag-magenta}

You create the HyperConverged resource for OpenShift Virtualization, but the deployment does not complete successfully.
{: tsSymptoms}

The HyperConverged configuration might reference node labels or placement settings that do not match your cluster. {{site.data.keyword.openshiftlong_notm}} clusters require you to configure node placement explicitly for infrastructure components and VM workloads.
{: tsCauses}

To resolve the issue,
{: tsResolve}

 verify the node labels in your cluster and review the HyperConverged resource configuration.

1. Verify the node labels in your cluster.
   ```sh
   oc get nodes --show-labels
   ```
   {: pre}

2. Check the HyperConverged resource status.
   ```sh
   oc get hyperconverged -n openshift-cnv
   oc describe hyperconverged kubevirt-hyperconverged -n openshift-cnv
   ```
   {: pre}

3. Update the HyperConverged resource with node selectors that match your environment.
   ```sh
   oc edit hyperconverged kubevirt-hyperconverged -n openshift-cnv
   ```
   {: pre}

4. Review the HyperConverged operator logs.
   ```sh
   oc logs -n openshift-cnv -l name=hyperconverged-cluster-operator
   ```
   {: pre}

5. Review the node placement guidance in [Installing the OpenShift Virtualization Operator](/docs/openshift?topic=openshift-oc-virtualization#virt-install-node-placement) and update the `infra` and `workloads` placement settings as needed.
