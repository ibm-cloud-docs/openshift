---

copyright:
  years: 2026, 2026

lastupdated: "2026-09-28"

keywords: port 443, control plane, firewall, network, ROKS 4.22, notice, change

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}

# Cluster control plane reachable over port 443 (ROKS 4.22+)
{: #notice-cp-port-443}

[Red Hat OpenShift on IBM Cloud]{: tag-red}

Starting with {{site.data.keyword.openshiftlong_notm}} version 4.22, the cluster control plane is reachable over port 443 in addition to the existing NodePort range (30000–32767). Review the following information to determine whether you need to take action before upgrading to version 4.22 or later.
{: shortdesc}

## What is changing
{: #notice-cp-port-443-what}

In version 4.22, the cluster control plane is exposed on **port 443** (HTTPS) using hostname-based routing. Previously, communication to the control plane used only the NodePort range (30000–32767).

Traffic is routed through four purpose-built hostnames. The `.api.` and `.oauth.` hostnames are available over both the public and private service endpoints. The `.tunnel.` and `.ignition.private.` hostnames are available over the **private service endpoint only**.

| Hostname pattern | Purpose | Endpoint availability |
| --- | --- | --- |
| `<cluster>.api.<region-domain>` | Kubernetes API server (`kubectl`, `oc`) | Public and private |
| `<cluster>.oauth.<region-domain>` | OAuth server (`oc login`, web console) | Public and private |
| `<cluster>.tunnel.<region-domain>` | Konnectivity tunnel (kubelet → API, pod exec/logs) | Private only |
| `<cluster>.ignition.private.<region-domain>` | RHCOS ignition endpoint for worker nodes | Private only |
{: caption="Port 443 hostnames for the cluster control plane" caption-side="bottom"}

In addition to `kubectl` and `oc` client traffic, this change affects worker-to-control-plane traffic. Worker nodes use port 443 for the kubelet API, Konnectivity, and RHCOS ignition — not only external client connections.

This change improves compatibility with standard enterprise networking environments and aligns with upstream OpenShift behavior.

## Who is affected
{: #notice-cp-port-443-who}

You might be affected if your environment includes any of the following:

- Custom firewall rules or security group rules that restrict outbound or inbound traffic on port 443
- Network ACLs (NACLs) in VPC environments that explicitly block port 443 traffic to or from the control plane
- Calico or Kubernetes network policies that restrict egress to the control plane IP range on specific ports
- On-premises or corporate network restrictions that block port 443 to IBM Cloud endpoints

Most environments already permit port 443 traffic and are **not affected** by this change.

## Required actions
{: #notice-cp-port-443-actions}

Before upgrading your cluster to version 4.22 or later, review and update your network configuration as needed.

1. **Check your firewall rules.** Ensure that port 443 (TCP) is permitted for outbound traffic to all four control plane hostnames. The hostnames follow the pattern `<cluster>.<purpose>.<region-domain>` and are listed in the cluster details in the {{site.data.keyword.cloud_notm}} console or via the `ibmcloud ks cluster get` command.

1. **Review VPC security groups.** If you use custom VPC security groups, verify that inbound and outbound rules allow TCP traffic on port 443 to and from the control plane.

1. **Review network ACLs.** If you use custom VPC network ACLs, ensure that port 443 is not blocked for traffic between worker nodes and the control plane.

1. **Review Calico and Kubernetes network policies.** If you have egress network policies that restrict traffic from worker nodes, ensure that port 443 is permitted to the control plane IP ranges.

1. **Review on-premises connectivity.** If your cluster worker nodes connect to the control plane over a VPN or {{site.data.keyword.dl_full_notm}} connection, ensure that port 443 is permitted across that connection.

## Verification
{: #notice-cp-port-443-verify}

After updating your network configuration, you can verify connectivity to the Kubernetes API server on port 443 by running the following command from a worker node or a pod in the cluster.

```sh
curl -k https://<cluster>.api.<region-domain>/healthz
```
{: pre}

A response of `ok` confirms that port 443 is reachable to the API server hostname.

## Getting help
{: #notice-cp-port-443-help}

If you have questions or encounter issues, open a support case in the [{{site.data.keyword.cloud_notm}} console](https://cloud.ibm.com/unifiedsupport/cases/add){: external} or contact your IBM account team.
