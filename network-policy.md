---

copyright: 
  years: 2014, 2026
lastupdated: "2026-09-30"


keywords: openshift

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}





# Controlling traffic with network policies
{: #network_policies}

[Classic clusters]{: tag-classic-inf}

This network policy information is specific to classic clusters. For VPC clusters, see [Understanding Secure by Default cluster VPC networking](/docs/openshift?topic=openshift-vpc-security-group-reference).
{: note}

Every {{site.data.keyword.openshiftlong}} cluster comes with a network plug-in called Calico. Default network policies secure the public network interface of every worker node in the cluster.
{: shortdesc}

Changing the Calico plug-in, components, or default Calico settings is not supported. For example, don't deploy a new Calico plug-in version, or modify the daemon sets or deployments for the Calico components, default `IPPool` resources, or Calico nodes. Instead, you can follow the documentation to [change the Calico MTU](/docs/openshift?topic=openshift-kernel#calico-mtu) or to [disable the port map plug-in for the Calico CNI](/docs/openshift?topic=openshift-kernel#calico-portmap) if necessary.
{: important}

You can use Calico and Kubernetes to create network policies for a cluster. With Kubernetes network policies, you can specify the network traffic that you want to allow or block to and from a pod within a cluster. To set more advanced network policies such as blocking inbound (ingress) traffic to network load balancer (NLB) services, use Calico network policies.

Kubernetes network policies
:   [Kubernetes network policies](https://kubernetes.io/docs/concepts/services-networking/network-policies/){: external} specify how pods can communicate with other pods and with external endpoints. Both incoming and outgoing network traffic is allowed or blocked based on protocol, port, and source or destination IP addresses. Traffic can also be filtered based on pod and namespace labels. You can apply Kubernetes network policies by using `oc` commands or the Kubernetes APIs.

Calico network policies
:   [Calico network policies](https://docs.tigera.io/calico/latest/reference/resources/networkpolicy){: external} are a superset of the Kubernetes network policies. Calico policies are applied using either the `oc` or `calicoctl` command line.  `oc` is preferred to avoid having to download calicoctl and keep it up to date. Calico policies add the following features.
    - Allow or block network traffic on specific network interfaces regardless of the Kubernetes pod source or destination IP address or CIDR.
    - Allow or block network traffic for pods across namespaces.
    - [Block inbound traffic to Kubernetes LoadBalancer or NodePort services](#block_ingress).


Calico enforces these policies, including any Kubernetes network policies, by setting up iptables rules that serve as a firewall for the worker node to define the characteristics that the network traffic must meet to be forwarded to the targeted resource.


## Default Calico network policies
{: #default_policy}
{: help}
{: support}

When a cluster with a public VLAN is created, a `HostEndpoint` resource with the `ibm.role: worker_public` label is created automatically for each worker node and its public network interface. This `HostEndpoint` causes all traffic to or from the public network interface to be dropped unless it is specifically allowed by a Calico policy that selects `ibm.role: worker_public` label.
{: shortdesc}

A `HostEndpoint` resource with the `ibm.role: worker_private` label is also created automatically for each worker node and its private network interface. A default `allow-all-private-default` policy is created so that all traffic is allowed to and from the private network interface. This `HostEndpoint` makes it easy for cluster users to further restrict private network traffic by creating Calico policies that select `ibm.role: worker_private` and have a lower order number than the `allow-all-private-default`.

These default Calico host policies allow all public outbound network traffic and allow public inbound traffic to specific cluster components, such as Kubernetes NodePort, LoadBalancer, and Ingress services. All private traffic is allowed by default by the `allow-all-private-default` policy. Any other inbound network traffic from the internet to your worker nodes that isn't specified in the default policies gets blocked. The default policies don't affect pod to pod traffic.

Don't remove the default policies from your cluster, because they are recreated on the next cluster master refresh or master update. If you want to further restrict traffic, apply lower order Calico policies to block the traffic. Be sure you fully understand what you are blocking, and that the cluster components do not need the traffic you want to block.
{: important}

Review the following default Calico host policies that are automatically applied to your cluster.

|Calico policy|Description|
|--- |--- |
|`allow-all-outbound`|Allows all outbound traffic on the public network.|
|`allow-all-private-default`| Allows all inbound and outbound traffic on the private network.|
|`allow-bigfix-port`|Allows incoming traffic on port 52311 to the BigFix app to allow necessary worker node updates.|
|`allow-icmp`|Allows incoming ICMP packets (pings).|
|`allow-node-port-dnat`|Allows incoming network load balancer (NLB), Ingress application load balancer (ALB), and NodePort service traffic to the pods that those services are exposing. Note: You don't need to specify the exposed ports because Kubernetes uses destination network address translation (DNAT) to forward the service requests to the correct pods. That forwarding takes place before the host endpoint policies are applied in iptables.|
|`allow-sys-mgmt`|Allows incoming connections for specific IBM Cloud infrastructure systems that are used to manage the worker nodes.|
|`allow-vrrp`|Allows VRRP packets, which monitor and move virtual IP addresses between worker nodes.|
{: caption="Default Calico host policies for each cluster" caption-side="bottom"}




## Viewing network policies
{: #view_policies}

View the details for default and any added network policies that are applied to your cluster.
{: shortdesc}

Before you begin, [install and configure the Calico CLI, and set the context for your cluster to run Calico commands](#cli_install).

1. View the Calico host endpoint.
    ```sh
    oc get hostendpoints.projectcalico.org -o yaml
    ```
    {: pre}

1. View all the Calico network policies that were created for the cluster. This list includes policies that might not apply to any pods or hosts yet. For a Calico policy to be enforced, a Kubernetes pod or Calico `HostEndpoint` must exist that matches the selector that in the Calico network policy.

    [Calico Network policies](https://docs.tigera.io/calico/latest/reference/resources/networkpolicy){: external} are scoped to specific namespaces:
    ```sh
    oc get networkpolicy.projectcalico.org --all-namespaces -o wide
    ```
    {: pre}

    [Kubernetes Network policies](https://kubernetes.io/docs/concepts/services-networking/network-policies/){: external} are also scoped to specific namespaces:
    ```sh
    oc get networkpolicies.networking.k8s.io --all-namespaces -o wide
    ```
    {: pre}

    [Calico Global network policies](https://docs.tigera.io/calico/latest/reference/resources/globalnetworkpolicy){: external} are not scoped to specific namespaces:
    ```sh
    oc get globalnetworkpolicies.projectcalico.org -o wide
    ```
    {: pre}

1. View details for a Calico network policy.
    ```sh
    oc get networkpolicies.projectcalico.org -o yaml <policy_name> --namespace <policy_namespace>
    ```
    {: pre}

1. View the details of all Calico global network policies for the cluster.
    ```sh
    oc get globalnetworkpolicies.projectcalico.org -o yaml
    ```
    {: pre}

1. View the details of all Kubernetes network policies for the cluster.
    ```sh
    oc get networkpolicies.networking.k8s.io --all-namespaces -o yaml
    ```
    {: pre}


## Adding network policies
{: #adding_network_policies}

Usually, the default policies don't require changes. Only advanced scenarios might require changes. If you find that you must make changes, you can create your own network policies.
{: shortdesc}

To create Kubernetes network policies, see the [Kubernetes network policy documentation](https://kubernetes.io/docs/concepts/services-networking/network-policies/){: external}.

To create Calico policies, use the following steps.

1. Define your Calico [network policy](https://docs.tigera.io/calico/latest/reference/resources/networkpolicy){: external} or [global network policy](https://docs.tigera.io/calico/latest/reference/resources/globalnetworkpolicy){: external} by creating a configuration script (`.yaml`) with Calico v3 policy syntax. These configuration files include the selectors that describe what pods, namespaces, or hosts that these policies apply to.

1. Apply the policies to the cluster.
    ```sh
    oc apply -f policy.yaml
    ```
    {: pre}
    
Calico and Kubernetes network policies only block new connections, they don't interrupt connections that existed before the policy was applied. After applying a new or changed policy, to test that it is working and not blocking more than it should, do the following:

1. Restart any pods that might be affected by the policy, or restart all pods in case you don't have your selector correct and it affects more than you think it will.

1. Run `ibmcloud ks cluster master refresh -c CLUSTER-ID` to restart your cluster master pods. This interrupts existing connections from kubelet and other components to the master and forces them to reconnect. This shows if the new and changed policies block any necessary connections to your master components.

1. Try to connect to {{site.data.keyword.openshiftshort}} console to ensure the policy changes don't block the connections needed by those components.



## Controlling inbound traffic to NLB or NodePort services
{: #block_ingress}

[By default](#default_policy), Kubernetes NodePort and LoadBalancer services make your app available on all public and private cluster interfaces. However, you can use Calico policies to block incoming traffic to your services based on traffic source or destination.
{: shortdesc}

Default Kubernetes and Calico policies are difficult to apply to protect Kubernetes NodePort and LoadBalancer services due to the DNAT iptables rules generated for these services. However, pre-DNAT policies prevent specified traffic from reaching your apps because they generate and apply iptables rules before Kubernetes uses regular DNAT to forward traffic to pods.

Some common uses for Calico pre-DNAT network policies:

- Block traffic to public node ports of a private network load balancer (NLB) service: An NLB service makes your app available over the NLB IP address and port and makes your app available over the service's node ports. Node ports are accessible on every IP address (public and private) for every node within the cluster.
- Block traffic to public node ports on clusters that are running [edge worker nodes](/docs/openshift?topic=openshift-edge#edge): Blocking node ports ensures that the edge worker nodes are the only worker nodes that handle incoming traffic.
- Block traffic from certain source IP addresses or CIDRs
- Allow traffic from only certain source IP addresses or CIDRs, and block all other traffic

To see how to allow or block source IP addresses, try the [Using Calico network policies to block traffic tutorial](/docs/openshift?topic=openshift-policy_tutorial#policy_tutorial).

## Example Calico policies to restrict public or private network traffic
{: #isolate_workers_public}

IBM provides a set of example [Calico public network policies](https://github.com/IBM-Cloud/kube-samples/tree/master/calico-policies/public-network-isolation) and [Calico private network policies](https://github.com/IBM-Cloud/kube-samples/tree/master/calico-policies/private-network-isolation) that further restrict public and private network traffic on cluster workers.
{: shortdesc}

These policies are not meant to block everything, nor do they necessarily meet any compliance requirements on their own. They are not actively supported by IBM and are just intended as one possible starting point and must be edited to meet your unique use cases. For more information, see the [README](https://github.com/IBM-Cloud/kube-samples/tree/master/calico-policies){: external}.
{: important}

IBM no longer recommends using the allow-egress-pods-public, allow-public-services-pods, allow-openshift-console, allow-kube-system-to-olm, allow-openshift-metrics, allow-egress-pods-private, or allow-private-services-pods sample policies in the [Applying public network policies](#calico-public) and [Applying private network policies](#isolate_workers) sections.  These policies controlled egress from all pods in the cluster.  To control traffic to and from pods IBM recommends using Kubernetes NetworkPolicy and targeting specific namespaces and pods instead of using these blanket policies that treat each pod the same.
{: important}

### Applying public network policies
{: #calico-public}

1. Clone the `IBM-Cloud/kube-samples` repository.

    ```sh
    git clone https://github.com/IBM-Cloud/kube-samples.git
    ```
    {: pre}

1. Change directories to the public policy directory for the region that your cluster is in. Example command for a cluster in US South:

    ```sh
    cd <filepath>/IBM-Cloud/kube-samples/calico-policies/public-network-isolation/us-south
    ```
    {: pre}

1. Review each policy for any changes you might need to make. For example, the `allow-ibm-ports-public.yaml` policy might need to be edited to specify the cluster's pod subnet, replacing the default `172.30.0.0/16` subnet. Also review these policies for any connections you might not want to allow.

1. Apply the public or private policies that you want to use.


    ```sh
    oc apply -f allow-ibm-ports-public.yaml
    oc apply -f allow-public-service-endpoint.yaml
    oc apply -f deny-all-outbound-public.yaml
    oc apply -f allow-konnectivity.yaml
    ```
    {: pre}

1. Optional: To allow your worker nodes to access other {{site.data.keyword.cloud_notm}} services over the public network, apply the `allow-public-services.yaml` policy. This policy allows access to the IP addresses for {{site.data.keyword.registrylong_notm}}, and if the services are available in the region, {{site.data.keyword.logs_full_notm}} and {{site.data.keyword.mon_full_notm}}. To access other {{site.data.keyword.cloud_notm}} services, you must manually add the subnets for those services to this policy.

    ```sh
    oc apply -f allow-public-services.yaml
    ```
    {: pre}

1. Verify that the Calico network policies are applied.

    ```sh
    oc get networkpolicies.projectcalico.org -o yaml -A
    ```
    {: pre}

1. Verify that the Calico global network policies are applied.

    ```sh
    oc get globalnetworkpolicies.projectcalico.org -o yaml
    ```
    {: pre}

1. Optional: If you do use policies that apply to pods in the cluster, test these well to ensure all your cluster functionality continues to work.  For example, if you use any in-cluster webhooks, ensure your policies allow these webhooks to make the required connections to the pods that implement the webhooks.  You also must allow traffic for any non-local services that extend the Kubernetes API. You can find these services by running `oc get apiservices`. Note that `default/openshift-apiserver` is included as a local service and does not require a network policy.


### Applying private network policies
{: #isolate_workers}

1. Clone the `IBM-Cloud/kube-samples` repository.

    ```sh
    git clone https://github.com/IBM-Cloud/kube-samples.git
    ```
    {: pre}

1. Go to the private policy directory for the region that your cluster is in. Example command for a cluster in US South:

    ```sh
    cd <filepath>/IBM-Cloud/kube-samples/calico-policies/private-network-isolation/us-south
    ```
    {: pre}

1. Review each policy for any changes you might need to make. For example, if you specified a custom subnet when you created your cluster that provides the private IP addresses for your pods, you must specify that CIDR instead of the `172.30.0.0/16` CIDR in the `allow-all-workers-private.yaml` policy.

1. Apply the policies.

    ```sh
    oc apply -f allow-all-workers-private.yaml
    oc apply -f allow-ibm-ports-private.yaml
    oc apply -f allow-icmp-private.yaml
    oc apply -f allow-private-service-endpoint.yaml
    oc apply -f allow-sys-mgmt-private.yaml
    oc apply -f deny-all-private-default.yaml
    ```
    {: pre}

1. Optional: To allow your workers to access {{site.data.keyword.registrylong_notm}} over the private network, apply the `allow-private-services.yaml` policy. To access other {{site.data.keyword.cloud_notm}} services that support private cloud service endpoints, you must manually add the subnets for those services to this policy.

    ```sh
    oc apply -f allow-private-services.yaml
    ```
    {: pre}

1. Optional: To expose your apps with private network load balancers (NLBs) or Ingress application load balancers (ALBs), you must open the VRRP protocol by applying the `allow-vrrp-private` policy.

    ```sh
    oc apply -f allow-vrrp-private.yaml
    ```
    {: pre}

    You can further control access to networking services by creating [Calico pre-DNAT policies](/docs/openshift?topic=openshift-network_policies#block_ingress). In the pre-DNAT policy, ensure that you use `selector: ibm.role=='worker_private'` to apply the policy to the workers' private host endpoints.
    {: tip}

1. Verify that the Calico network policies are applied.

    ```sh
    oc get networkpolicies.projectcalico.org -o yaml -A
    ```
    {: pre}

1. Verify that the Calico global network policies are applied.

    ```sh
    oc get globalnetworkpolicies.projectcalico.org -o yaml
    ```
    {: pre}

1. Optional: If you do use policies that apply to pods in the cluster, test these well to ensure all your cluster functionality continues to work.  For example, if you use any in-cluster webhooks, ensure your policies allow these webhooks to make the required connections to the pods that implement the webhooks.  You also must allow traffic for any non-local services that extend the Kubernetes API. You can find these services by running `oc get apiservices`. Note that `default/openshift-apiserver` is included as a local service and does not require a network policy.


## Controlling traffic between pods
{: #isolate_services}

Kubernetes policies protect pods from internal network traffic. You can create simple [Kubernetes network policies](/docs/openshift?topic=openshift-vpc-kube-policies) to isolate app microservices from each other within a namespace or across namespaces.

By default, any pod has access to any other pod in the cluster. Additionally, any pod has access to any services that are exposed by the pod network, such as a metrics service, the cluster DNS, the API server, or any services that you manually create in your cluster.





## Logging denied traffic
{: #log_denied}

To log denied traffic requests to certain pods in your cluster, you can create a Calico log network policy.
{: shortdesc}

When you set up network policies to limit traffic to app pods, traffic requests that are not permitted by these policies are denied and dropped. In some scenarios, you might want more information about denied traffic requests. For example, you might notice some unusual traffic that is continuously being denied by one of your network policies. To monitor the potential security threat, you can set up logging to record every time that the policy denies an attempted action on specified app pods.

This section shows you how to log traffic that is denied by a Kubernetes network policy. To log traffic that is denied by a Calico network policy, see [Lesson 5 of the Calico network policy tutorial](/docs/openshift?topic=openshift-policy_tutorial#lesson5).
{: tip}


1. Create or use an existing Kubernetes network policy that blocks or limits incoming traffic.

    1. Create a Kubernetes network policy. For example, to control traffic between pods, you might use the following example Kubernetes policy that is named `access-nginx` that limits access to an NGINX app. Incoming traffic to pods that are labeled "run=nginx" is allowed only from pods with the "run=access" label. All other incoming traffic to the "run=nginx" app pods is blocked.

        ```yaml
        kind: NetworkPolicy
       apiVersion: networking.k8s.io/v1
       metadata:
         name: access-nginx
       spec:
         podSelector:
           matchLabels:
             run: nginx
         ingress:
           - from:
             - podSelector:
                 matchLabels:
                   run: access
        ```
        {: codeblock}

    2. Apply the policy.

        ```sh
        oc apply -f <policy_name>.yaml
        ```
        {: pre}

2. To log all the traffic that is denied by the policy you created in the previous step, create a Calico NetworkPolicy named `log-denied-packets`. The following Calico policy uses the same pod selector as the example `access-nginx` Kubernetes policy described in step 1, however the syntax is slightly different since it is a Calico NetworkPolicy instead of a Kubernetes NetworkPolicy. Also, because all Kubernetes NetworkPolicy are evaluated by Calico as order `1000`, the order number `3000` is added to ensure it is evaluated after the Kubernetes NetworkPolicy. With these two policies in place, here is the result:

    * New connections coming in to the nginx pod are first evaluated against the Kubernetes NetworkPolicy (order `1000`). Connections coming from a pod with the `run=access` label are immediately accepted, meaning no other policies are evaluated.
    * If the connection is coming from a pod without the `run=access` label (or from anything that isn't a pod), that Kubernetes NetworkPolicy won't do anything and Calico next evaluates the `log-denied-packets` policy. This policy logs the packet to syslog on the worker the nginx pod is on.
    * Calico then checks for any other policies to apply to the connection, and since it doesn't find any, the packet is dropped. This is because any traffic to a pod with a policy that isn't explicitly allowed is dropped.

        ```yaml
        apiVersion: projectcalico.org/v3
        kind: NetworkPolicy
        metadata:
          name: log-denied-packets
        spec:
          types:
          - Ingress
          ingress:
          - action: Log
            destination: {}
            source: {}
          selector: projectcalico.org/orchestrator == 'k8s' && run == 'nginx'
          order: 3000
        ```
        {: codeblock}


    `types`
    :   This `Ingress` policy applies to all incoming traffic requests. The value `Ingress` is a general term for all incoming traffic, and does not refer to traffic only from the IBM Ingress ALB.
    `ingress`
    :   `action`: The `Log` action writes a log entry for any requests that match this policy to the `/var/log/syslog` path on the worker node. 
    :   `destination`: No destination is specified because the `selector` applies this policy to all pods with a certain label.
    :   `source`: This policy applies to requests from any source.
    
    `selector`
    :   The selector should target the same traffic as the original access-nginx Kubernetes NetworkPolicy. Since this is a Calico policy, you must include `projectcalico.org/orchestrator == 'k8s'` to indicate that it applies to all pods in the policy's namespace, in addition to the original `run == 'nginx'`.
    
    `order`
    :   Calico policies have orders that determine when they are applied to incoming request packets. Policies with lower orders, such as `1000`, are applied first. Policies with higher orders are applied after the lower-order policies. For example, a policy with a very high order, such as `3000`, is effectively applied last after all the lower-order policies have been applied. Incoming request packets go through the iptables rules chain and try to match rules from lower-order policies first. If a packet matches any rule, the packet is accepted. However, if a packet doesn't match any rule, it arrives at the last rule in the iptables rules chain with the highest order. To make sure that this policy is the last policy in the chain, use a much higher order, such as `3000`, than the policy you created in step 1. Note that Kubernetes NetworkPolicy are applied as order `1000`.



3. Apply the policy.

    ```sh
    oc apply -f log-denied-packets.yaml
    ```
    {: pre}

4. Generate log entries by sending requests that are not allowed by the policy that you created in step 1. For example, try to ping the pod that is protected by the network policy from a pod or an IP address that is not permitted.

5. Check for log entries that are written to the `/var/log/syslog` path. The DST (destination) or SRC (source) IP addresses in the log entry might be different than expected due to proxies, Network Address Translation (NAT), and other networking processes. The log entry looks similar to the following.

    ```sh
    Sep 5 14:34:40 <worker_hostname> kernel: [158271.044316] calico-packet: IN=eth1 OUT= MAC=08:00:27:d5:4e:57:0a:00:27:00:00:00:08:00 SRC=192.XXX.XX.X DST=192.XXX.XX.XX LEN=60 TOS=0x00 PREC=0x00 TTL=64 ID=52866 DF PROTO=TCP SPT=42962 DPT=22 WINDOW=29200 RES=0x00 SYN URGP=0
    ```
    {: screen}

6. Optional: Forward the logs from `/var/log/syslog` to [{{site.data.keyword.logs_full_notm}}](/docs/openshift?topic=openshift-health).
