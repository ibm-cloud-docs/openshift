---

copyright:
  years: 2026, 2026
lastupdated: "2026-02-11"

keywords: openshift, networking, cni

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}


# Selecting a container network interface
{: #cni}

Review the following information for selecting a container network interface (CNI).
{: shortdesc}

In {{site.data.keyword.openshiftlong_notm}} version 4.20 and later, Calico is the default CNI, but clusters that use RHCOS worker nodes have the option of selecting Open Virtual Network (OVN) as their cluster CNI. 

Calico [Default]{: tag-warm-grey}
:   Calico is a single platform for networking, network security, and observability for any Kubernetes distribution in the cloud, on-premises, or at the edge. Whether you're just starting with Kubernetes or operating at scale, Calico's open source, enterprise, and cloud editions provide the networking, security, and observability you need. For more information, see [Calico documentation](https://docs.tigera.io/calico/latest/about/){: external}.

Open Virutal Network (OVN) [4.20 and later]{: tag-red} [RHCOS worker nodes only]{: tag-magenta}
:   Open Virtual Network (OVN) is an Open vSwitch-based software-defined networking (SDN) solution for supplying network services to instances. OVN provides platform-neutral support for the full OpenStack Networking API. With OVN, you can programatically connect groups of guest instances into private L2 and L3 networks. For more information, see the [Red Hat documentation](https://docs.redhat.com/en/documentation/red_hat_openstack_platform/13/html/networking_with_open_virtual_network/open_virtual_network_ovn){: external}

## Comparing Calico and OVN
{: #cni-compare}

Review the following table to compare the features and functionality of Calico and OVN.

If you plan to use OVN, you must ensure that your VPC subnets don't overlap with the additional subnets specified in the following table. If there is a subnet overlap, pod to pod networking will fail.
{: important}

| Component | Calico | OVN-Kubernetes |
| --- | --- | --- |
| Encapsulation | - IP in IP Protocol (not UDP or TCP)  \n - Encapsulates only pod to pod traffic from pods running on nodes that are in different subnets. | - Geneve: UDP Protocol on port 6081  \n - Encapsulates all pod to pod traffic |
| Default Cluster Network / Pod MTU | 1480 bytes (20 byte IPinIP header) by default. This can be changed. | 1400 bytes (100 byte Geneve header) by default. This can be changed. Daemonset needs to create NetworkManager file instead of just running `ip link set dev ens3 mtu`. You must also restart new worker nodes. |
| Pod IPAM | This is implemented by calico-ipam CNI and not by containers in the cluster. In use and free pod IPs and subnets are stored as Custom Resources in the cluster. Calico initially allocates each new node a /26 subnet (64 IPs, at least one typically used as tunl0 IP, rest are available for pods). If all IPs in a /26 are used, then Calico assigns a second /26 subnet to the node. You can use the `calicoctl ipam check` to see subnets assigned to each node. The `calico-ipam` CNI allocates pod IP to each new pod. | - Pod IPAM is handled by both the `ovnkube-control-plane` pod (`ovnkube-cluster-manager` container) in the control plane and by `ovnkube-node` pods in customer cluster (`ovnkube-controller` container).  \n - The `ovnkube-cluster-manager` container in the control plane watches for new nodes and llocates /24 pod subnet (256 IPs) to each new cluster node. Only a single /24 pod subnet is added, with no option to add a second one. It also allocates a join subnet IP to each new node.  \n - The `ovnkube-controller` container on each cluster node watches all k8s resources and allocates pod IP to each new pod. |
| Pod to pod routing | - Uses linux routes.  \n - Uses BGP to distribute routes.  \n - `tunl0` interface on each node for encapsulation. | - Open vSwitch (OVS) runs on each node and routes pod to pod traffic.  \n - OVN configures OVS flows to define pod to pod routing via Geneve.  \n - Many interfaces created such as: `ovs-system`, `genev_sys_6081`, `ovn-k8s-mp0`, `br-int`, `br-ex` |
| Kubernetes network policies | - Implemented by `calico-node` adding iptables rules.  \n - Logs network policy drops and/or allowed.  \n Requires extra Calico policies that use a “Log” action and some thought and planning on where/when to put these Log actions.  \n - Logs to `syslog` on the worker node, which can difficult to retrieve.  \n - Logs do not include what policy allowed the traffic. | - Implemented by OVS using ACLs on logical ports (not iptables).  \n - Logging network policy drops and/or allowed traffic is much easier by using annotations.  \n - Annotate the namespace(s) where you want to log policy activity, and if you want to log allows, denies, or both.  \ -n Logs are sent to file `/var/log/ovn/acl-audit-log.log` in the `ovnkube-node` pod.  \n - Configuration options exist to send these logs to other log targets.  \n - Logs include which policy allowed the traffic, but not which traffic denied it, because policies are allow-only.  \n - There must be at least one policy in place for allowed traffic to be logged. |
| Host network policies | Calico GlobalNetworkPolicies | None |
| Additional subnets | None | - **Join Subnet**: `100.64.0.0/16` (OpenShift default).  \n - **Masquerade subnet**: `169.254.64.0/18`. This is different from the OpenShift default of `169.254.0.0/17`. This difference is to avoid conflicting with the `169.254.2.0/24` IPs that are used for local registry haproxy.  \n - **Transit subnet**:`100.88.0.0/16` (OpenShift default). |
| APIserver watches | - `calico-typha` registers resource watches and acts as a proxy to `calico-node` pods to notify of changes.  \n - `calico-node` connects to one of the `calico-typha` pods and registers for notification of resource changes. | - The `ovnkube-cluster-manager` container in control plane watches for new nodes.  \n - The `ovnkube-controller` container on each cluster node watches for resources and translates them into OVN logical entries on nbdb. |
| CNI | The `calico` and `calico-ipam` CNI binaries are copied to each node by the `install-cni` initContainer on the `calico-node` pod. | The `ovnkube-node` pod’s `ovnkube-controller` container executes the CNI binary for add and delete calls. |
| Namespaces, pods, and deployments created | - `calico-apiserver` namespace  \n - `calico-apiserver` (deployment, 2 pods)  \n - `calico-system` namespace  \n - `calico-node` (each node)  \n - `calico-typha` (deployment, from 2 - 10 pods).  \n - `calico-kube-controllers` (1 node).  \n - `openshift-kube-proxy` namespace.  \n - `openshift-kube-proxy` (each node).  \n - `tigera-operator`.  \n - `tigera-operator` (deployment, 1 pod) | 
| Non-pod resources created |  The `calico` CNI binary, `calico-ipam` CNI binary, and various other CNI binaries are copied to each node by `install-cni` initContainer on `calico-node`. | - `openshift-ovn-kubernetes` namespace, `ovnkube-node` on each node with 8 containers, `ovnkube-controller` watches resources, allocates pod IPs, and translates resources into OVN logical entries in `nbdb`. Also handles CNI add and delete.  \n - `nbdb` stores logical entries.  \n - `northd` converts logical entries from `nbdb` to logical flows in `sbdb`.  \n - `sbdb` stores logical flows.  \n - `ovn-controller` converts logical flows in `sbdb` and programs OVS switch.  \n - `ovn-acl-logging`.  \n - `kube-rbac-proxy-node` protects node metrics so only authorized users can scrape them.  \n - `kube-rbac-proxy-ovn-metrics` protects OVN metrics so only authorized users can scrape them. |
| Connections between pods | - The `calico-node` pod initially connects to the kube apiserver via local haproxy in proxy pod listening on TCP 172.20.0.1:2040 to get `calico-typha` pod list.  \n - The `calico-node` pod connects to one of the `calico-typha` pods on TCP port 5473 to listen for cluster resource updates.  \n - The `calico-node` pod runs bird BGP daemon that connects in a full mesh to all other `calico-node` bird BGP daemons on TCP port 179.  \n - Pod to pod traffic happens directly for pods on nodes in the same subnet and protocol/port the pod is using and uses IPinIP with no port for encapsulated traffic. | - The `ovnkube-controller` container on each node connects to kube apiserver via local haproxy in proxy pod listening on TCP `172.20.0.1:2040` for resource watches.  \n - All pod to pod traffic happens over the Geneve tunnel on UDP port 6081.   - For more information, see [Configuring your firewall](https://docs.redhat.com/en/documentation/openshift_container_platform/4.20/html/installation_configuration/configuring-firewall){: external}. |
{: caption="Calico and OVN comparison table" caption-side="bottom"}







