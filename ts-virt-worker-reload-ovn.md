---

copyright:
  years: 2026, 2026

lastupdated: "2026-05-06"

keywords: openshift virtualization, vni, worker reload, ovn, ovnkube, node-chassis-id, bare metal

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why does my worker node enter a critical state after reload with VNIs attached?
{: #ts-virt-worker-reload-ovn}
{: troubleshoot}
{: support}

[Virtual Private Cloud]{: tag-vpc}
[4.20 and later]{: tag-red}
[Bare metal worker nodes only]{: tag-warm-gray}
[RHCOS only]{: tag-magenta}
[OVN-Kubernetes CNI required]{: tag-blue}

When you reload a bare metal worker node that has Virtual Network Interfaces (VNIs) attached, the worker node enters a `critical` state and shows `Not Ready` status.
{: tsSymptoms}

When you check the worker node, you see the following issues:
- The `ovnkube-node` pod is in `CrashLoopBackOff` state
- The `ovnkube-controller` logs show an error similar to: `admission webhook "node.network-node-identity.openshift.io" denied the request: user: "system:ovn-node:..." is not allowed to set k8s.ovn.org/node-chassis-id on node`
- Network policies are not properly reconciled
- The Kubernetes API is unavailable from pods on the affected node

Starting with OpenShift 4.20, OVN enforces immutability on the `k8s.ovn.org/node-chassis-id` annotation. During a bare metal worker node reload operation, the node's chassis ID changes (stored in `/etc/openvswitch/system-id.conf`), but the old OVN annotations remain on the node object. When the `ovnkube-controller` pod attempts to set the new chassis ID, it is denied by the admission webhook because the annotation cannot be changed once set.
{: tsCauses}

To resolve this issue, manually remove the stale OVN annotations from the worker node after it is powered off during the reload operation.
{: tsResolve}

1. Initiate the worker node reload.
    ```sh
    ibmcloud ks worker reload --cluster <cluster_name_or_ID> --worker <worker_node_ID>
    ```
    {: pre}

2. Wait for the worker node to power off and enter the `Reloading` state. You can monitor the reload process by checking the worker node status.
    ```sh
    ibmcloud ks worker get --cluster <cluster_name_or_ID> --worker <worker_node_ID>
    ```
    {: pre}

3. After the worker node is powered off (or if the `ovnkube-node` pod is already crashing), remove the stale OVN annotations from the node. Replace `<NODE_NAME>` with your worker node name.
    ```sh
    NODE="<NODE_NAME>"; oc annotate node "$NODE" \
      k8s.ovn.org/host-cidrs- \
      k8s.ovn.org/l3-gateway-config- \
      k8s.ovn.org/node-chassis-id- \
      k8s.ovn.org/node-encap-ips- \
      k8s.ovn.org/node-id- \
      k8s.ovn.org/node-masquerade-subnet- \
      k8s.ovn.org/node-primary-ifaddr- \
      k8s.ovn.org/node-subnets- \
      k8s.ovn.org/node-transit-switch-port-ifaddr- \
      k8s.ovn.org/zone-name- \
      --overwrite
    ```
    {: pre}

    The timing is flexible - you can run this command after the node is powered off during the reload, or when the `ovnkube-node` pod is already crashing. You don't need to worry about precise timing beyond waiting for the shutdown to begin.
    {: tip}

4. Wait for the reload to complete. The worker node should return to a `Normal` state with `Ready` status.
    ```sh
    ibmcloud ks worker get --cluster <cluster_name_or_ID> --worker <worker_node_ID>
    ```
    {: pre}

5. Verify that the `ovnkube-node` pod is running successfully on the reloaded worker node.
    ```sh
    oc get pods -n openshift-ovn-kubernetes -o wide | grep <NODE_NAME>
    ```
    {: pre}

6. Verify that the worker node is ready and network connectivity is restored.
    ```sh
    oc get node <NODE_NAME>
    ```
    {: pre}

For more information about managing VNIs with OpenShift Virtualization, see [Managing virtual network interfaces for OpenShift Virtualization](/docs/openshift?topic=openshift-vni-virtualization).

## Related links
{: #ts-virt-worker-reload-ovn-related}

- [Red Hat Knowledge Base: ovnkube-controller goes in crashloopbackoff state](https://access.redhat.com/solutions/7103888){: external}
- [Red Hat Jira: OCPBUGS-49781](https://redhat.atlassian.net/browse/OCPBUGS-49781){: external}
- [Updating VPC worker nodes](/docs/openshift?topic=openshift-update#vpc_worker_node)
