---

copyright: 
  years: 2014, 2022
lastupdated: "2022-03-23"

keywords: openshift

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}


# Controlling traffic with network policies on classic clusters
{: #network_policies}

![Classic infrastructure provider icon.](images/icon-classic-2.svg) This network policy information is specific to classic clusters. For network policy information for VPC clusters, see [Controlling traffic with VPC access control lists](/docs/containers?topic=containers-vpc-network-policy).
{: note}

Every {{site.data.keyword.openshiftlong}} cluster comes with a network plug-in called Calico. Default network policies secure the public network interface of every worker node in the cluster.
{: shortdesc}

You can use Calico and Kubernetes to create network policies for a cluster. With Kubernetes network policies, you can specify the network traffic that you want to allow or block to and from a pod within a cluster. To set more advanced network policies such as blocking inbound (ingress) traffic to network load balancer (NLB) services, use Calico network policies.

Kubernetes network policies
:   [Kubernetes network policies](https://kubernetes.io/docs/concepts/services-networking/network-policies/){: external} specify how pods can communicate with other pods and with external endpoints. Both incoming and outgoing network traffic is allowed or blocked based on protocol, port, and source or destination IP addresses. Traffic can also be filtered based on pod and namespace labels. You can apply Kubernetes network policies by using `oc` commands or the Kubernetes APIs. When you apply a Kubernetes network policy, it's automatically converted into a Calico network policy so that Calico can apply an `Iptables` rule. The Calico network policy name has the `knp.default` prefix. To update the policy in the future, update the Kubernetes policy, and the updates are automatically applied to the Calico network policy.

Calico network policies
:   [Calico network policies](https://projectcalico.docs.tigera.io/security/protect-hosts){: external} are a set of the Kubernetes network policies. You can apply Calico policies by using the `calicoctl` command line. Calico policies add the following features.
    - Allow or block network traffic on specific network interfaces regardless of the Kubernetes pod source or destination IP address or CIDR.
    - Allow or block network traffic for pods across namespaces.
    - [Block inbound traffic to Kubernetes LoadBalancer or NodePort services](#block_ingress).

Calico enforces these policies, including any Kubernetes network policies that are automatically converted to Calico policies, by setting up Linux Iptables rules on the Kubernetes worker nodes. Iptables rules serve as a firewall for the worker node to define the characteristics that the network traffic must meet to be forwarded to the targeted resource.

In OpenShift Container Platform version 4, Calico is based on the Kubernetes data-store driver. For more information, see the [Calico documentation](https://projectcalico.docs.tigera.io/getting-started/kubernetes/hardway/the-calico-datastore){: external}.


## Default Calico network policies
{: #default_policy}
{: help}
{: support}

When a cluster with a public VLAN is created, a `HostEndpoint` resource with the `ibm.role: worker_public` label is created automatically for each worker node and its public network interface. To protect the public network interface of a worker node, default Calico policies are applied to any host endpoint with the `ibm.role: worker_public` label.
{: shortdesc}

**Clusters that run {{site.data.keyword.redhat_openshift_notm}} version 4**: A `HostEndpoint` resource with the `ibm.role: worker_private` label is also created automatically for each worker node and its private network interface. To protect the private network interface of a worker node, default Calico policies are applied to any host endpoint with the `ibm.role: worker_private` label.

These default Calico host policies allow all outbound network traffic and allow inbound traffic to specific cluster components, such as Kubernetes NodePort, LoadBalancer, and Ingress services. Any other inbound network traffic from the internet to your worker nodes that isn't specified in the default policies gets blocked. The default policies don't affect pod to pod traffic.

Don't remove policies that apply to a host endpoint unless you fully understand the policy. Be sure that you don't need the traffic allowed by the policy.
{: important}

Review the following default Calico host policies that are automatically applied to your cluster.

|Calico policy|Description|
|--- |--- |
|`allow-all-outbound`|Allows all outbound traffic on the public network.|
|`allow-all-private-default`|In {{site.data.keyword.redhat_openshift_notm}} version 4 or later: Allows all inbound and outbound traffic on the private network.|
|`allow-bigfix-port`|Allows incoming traffic on port 52311 to the BigFix app to allow necessary worker node updates.|
|`allow-icmp`|Allows incoming ICMP packets (pings).|
|`allow-node-port-dnat`|Allows incoming network load balancer (NLB), Ingress application load balancer (ALB), and NodePort service traffic to the pods that those services are exposing. Note: You don't need to specify the exposed ports because Kubernetes uses destination network address translation (DNAT) to forward the service requests to the correct pods. That forwarding takes place before the host endpoint policies are applied in Iptables.|
|`allow-sys-mgmt`|Allows incoming connections for specific IBM Cloud infrastructure systems that are used to manage the worker nodes.|
|`allow-vrrp`|Allows VRRP packets, which monitor and move virtual IP addresses between worker nodes.|
{: caption="Default Calico host policies for each cluster"}
{: summary="The first row in the table spans both columns. Read the rest of the rows from left to right, with the Calico policy in column one and the description in column two."}



## Installing and configuring the Calico CLI
{: #cli_install}

To view, manage, and add Calico policies, install and configure the Calico CLI.
{: shortdesc}

1. Set the context for your cluster to run Calico commands.
  
    * {{site.data.keyword.redhat_openshift_notm}} version 4.6 and later:
    
        1. Download the `kubeconfig` configuration file for your cluster.
            ```sh
            ibmcloud oc cluster config --cluster <cluster_name_or_ID>
            ```
            {: pre}

        2. Set the `DATASTORE_TYPE` environment variable to `kubernetes`.
            ```sh
            export DATASTORE_TYPE=kubernetes
            ```
            {: pre}

2. If corporate network policies use proxies or firewalls to prevent access from your local system to public endpoints, [allow TCP access for Calico commands](/docs/openshift?topic=openshift-firewall#firewall).

3. Follow the steps to install the `calicoctl` command line tool.
    * Linux and OS X
        1. [Download the version of the Calico CLI that matches your operating system](https://github.com/projectcalico/calicoctl/releases){: external}. For OS X, you might need to manually allow the downloaded file to be opened and run by navigating to **System Preferences** > **Security & Privacy** > **General**.

        2. Move the file to the `/usr/local/bin` directory.
            ```sh
            mv <filepath>/<filename> /usr/local/bin/calicoctl
            ```
            {: pre}

        3. Make the file an executable file.
            ```sh
            chmod +x /usr/local/bin/calicoctl
            ```
            {: pre}

        4. Ensure there isn't an old Calico configuration file `calicoctl.cfg` in the `/etc/calico` directory. If the `/etc/calico/calicoctl.cfg` file exists, delete it.

    * Windows
        1. [Download the Calico CLI](https://github.com/projectcalico/calicoctl/releases){: external}. When you save the file, rename it to `calicoctl.exe` and save it in the same directory as the {{site.data.keyword.cloud_notm}} CLI. This setup saves you some file path changes when you run commands later.
  
        3. Set the `KUBECONFIG` environment variable to the network configuration file that you found in step 1.
        
            ```sh
            export KUBECONFIG=./.bluemix/plugins/container-service/clusters/<cluster_name>-<hash>/calicoctl.cfg
            ```
            {: pre}



4. Verify that the Calico configuration is working correctly.
    ```sh
    calicoctl get nodes
    ```
    {: pre}

    Example output

    ```sh
    NAME
    10.176.48.106
    10.176.48.107
    10.184.58.23
    10.184.58.42
    ...
    ```
    {: screen}

Changing the Calico plug-in, components, or default Calico settings is not supported. For example, don't deploy a new Calico plug-in version, or modify the daemon sets or deployments for the Calico components, default `IPPool` resources, or Calico nodes. Instead, you can follow the documentation to [change the Calico MTU](/docs/openshift?topic=openshift-kernel#calico-mtu) or to [disable the port map plug-in for the Calico CNI](/docs/openshift?topic=openshift-kernel#calico-portmap) if necessary.
{: important}



## Viewing network policies
{: #view_policies}

View the details for default and any added network policies that are applied to your cluster.
{: shortdesc}

Before you begin, [install and configure the Calico CLI, and set the context for your cluster to run Calico commands](#cli_install).

1. View the Calico host endpoint.
    ```sh
    calicoctl get hostendpoint -o yaml
    ```
    {: pre}

2. View all the Calico and Kubernetes network policies that were created for the cluster. This list includes policies that might not apply to any pods or hosts yet. For a network policy to be enforced, a Kubernetes resource must exist that matches the selector that in the Calico network policy.

    [Network policies](https://projectcalico.docs.tigera.io/reference/resources/networkpolicy){: external} are scoped to specific namespaces:
    ```sh
    calicoctl get NetworkPolicy --all-namespaces -o wide
    ```
    {: pre}

    [Global network policies](https://projectcalico.docs.tigera.io/reference/resources/globalnetworkpolicy){: external} are not scoped to specific namespaces:
    ```sh
    calicoctl get GlobalNetworkPolicy -o wide
    ```
    {: pre}

3. View details for a network policy.
    ```sh
    calicoctl get NetworkPolicy -o yaml <policy_name> --namespace <policy_namespace>
    ```
    {: pre}

4. View the details of all global network policies for the cluster.
    ```sh
    calicoctl get GlobalNetworkPolicy -o yaml
    ```
    {: pre}


## Adding network policies
{: #adding_network_policies}

Usually, the default policies don't require changes. Only advanced scenarios might require changes. If you find that you must make changes, you can create your own network policies.
{: shortdesc}

To create Kubernetes network policies, see the [Kubernetes network policy documentation](https://kubernetes.io/docs/concepts/services-networking/network-policies/){: external}.

To create Calico policies, use the following steps. Before you begin, [install and configure the Calico CLI, and set the context for your cluster to run Calico commands](#cli_install).

1. Define your Calico [network policy](https://projectcalico.docs.tigera.io/reference/resources/networkpolicy){: external} or [global network policy](https://projectcalico.docs.tigera.io/reference/resources/globalnetworkpolicy){: external} by creating a configuration script (`.yaml`) with Calico v3 policy syntax. These configuration files include the selectors that describe what pods, namespaces, or hosts that these policies apply to. See these [sample Calico policies](https://projectcalico.docs.tigera.io/security/tutorials/kubernetes-policy-advanced){: external} to help you create your own.

2. Apply the policies to the cluster. If you have a Windows system, include the `--config=<filepath>/calicoctl.cfg` flag.
    ```sh
    calicoctl apply -f policy.yaml [--config=<filepath>/calicoctl.cfg]
    ```
    {: pre}


## Controlling inbound traffic to NLB or NodePort services
{: #block_ingress}

[By default](#default_policy), Kubernetes NodePort and LoadBalancer services make your app available on all public and private cluster interfaces. However, you can use Calico policies to block incoming traffic to your services based on traffic source or destination.
{: shortdesc}

Default Kubernetes and Calico policies are difficult to apply to protecting Kubernetes NodePort and LoadBalancer services due to the DNAT Iptables rules generated for these services. However, pre-DNAT policies prevent specified traffic from reaching your apps because they generate and apply Iptables rules before Kubernetes uses regular DNAT to forward traffic to pods.

Some common uses for Calico pre-DNAT network policies:

- Block traffic to public node ports of a private network load balancer (NLB) service: An NLB service makes your app available over the NLB IP address and port and makes your app available over the service's node ports. Node ports are accessible on every IP address (public and private) for every node within the cluster.
- Block traffic to public node ports on clusters that are running [edge worker nodes](/docs/openshift?topic=openshift-edge#edge): Blocking node ports ensures that the edge worker nodes are the only worker nodes that handle incoming traffic.
- Block traffic from certain source IP addresses or CIDRs
- Allow traffic from only certain source IP addresses or CIDRs, and block all other traffic

To see how to allow or block source IP addresses, try the [Using Calico network policies to block traffic tutorial](/docs/containers?topic=containers-policy_tutorial#policy_tutorial). For more example Calico network policies that control traffic to and from your cluster, you can check out the [stars policy demo](https://projectcalico.docs.tigera.io/security/tutorials/kubernetes-policy-demo/kubernetes-demo){: external} and the [advanced network policy](https://projectcalico.docs.tigera.io/security/tutorials/kubernetes-policy-advanced){: external}.
{: tip}

Before you begin, [install and configure the Calico CLI, and set the context for your cluster to run Calico commands](#cli_install).

1. Define a Calico pre-DNAT network policy for ingress (inbound traffic) access to Kubernetes services.
    * Use [Calico v3 policy syntax](https://projectcalico.docs.tigera.io/reference/resources/networkpolicy){: external}.

        Example resource that blocks traffic to all public node ports

        ```yaml
        apiVersion: projectcalico.org/v3
        kind: GlobalNetworkPolicy
        metadata:
          name: deny-nodeports
        spec:
          applyOnForward: true
          preDNAT: true
          ingress:
          - action: Deny
            destination:
              ports:
              - 30000:32767
            protocol: TCP
            source: {}
          - action: Deny
            destination:
              ports:
              - 30000:32767
            protocol: UDP
            source: {}
          selector: ibm.role=='worker_public'
          order: 1100
          types:
          - Ingress
        ```
        {: codeblock}

        Example resource that allows traffic from only a specified source CIDR to an NLB 1.0

        ```yaml
        apiVersion: projectcalico.org/v3
        kind: GlobalNetworkPolicy
        metadata:
          name: allowlist
        spec:
          applyOnForward: true
          preDNAT: true
          ingress:
          - action: Allow
            destination:
              nets:
              - <loadbalancer_IP>/32
              ports:
              - 80
            protocol: TCP
            source:
              nets:
              - <client_address>/32
          selector: ibm.role=='worker_public'
          order: 500
          types:
          - Ingress
        ```
        {: codeblock}

2. Apply the Calico preDNAT network policy. If you use a Windows machine, include the `--config=<filepath>/calicoctl.cfg` flag. It takes about 1 minute for the policy changes to be applied throughout the cluster.

    ```sh
    calicoctl apply -f deny-nodeports.yaml [--config=<filepath>/calicoctl.cfg]
    ```
    {: pre}

3. Optional: In multizone clusters, a multizone load balancer (MZLB) health checks the Ingress application load balancers (ALBs) in each zone of your cluster and keeps the DNS lookup results updated based on these health checks. If you use pre-DNAT policies to block all incoming traffic to Ingress services, you must allow inbound access on port 80 to your ALBs from the [CIDRs of the region where your cluster is located](https://github.com/IBM-Cloud/kube-samples/tree/master/control-plane-ips){: external}, and for classic clusters only, [Akamai's source IP addresses](https://github.com/IBM-Cloud/kube-samples/tree/master/akamai/gtm-liveness-test){: external} so that the {{site.data.keyword.redhat_openshift_notm}} control plane can check the health of your routers. For steps on how to create a Calico pre-DNAT policy to allow these IP addresses, see Lesson 3 of the [Calico network policy tutorial](/docs/containers?topic=containers-policy_tutorial#lesson3).

## Isolating clusters on the public network
{: #isolate_workers_public}

You can isolate your cluster on the public network by applying [Calico public network policies](https://github.com/IBM-Cloud/kube-samples/tree/master/calico-policies/public-network-isolation){: external}.
{: shortdesc}

This set of Calico policies work in conjunction with the [default Calico policies](#default_policy) to block most public network traffic of a cluster while allowing communication that is necessary for the cluster to function to specific subnets. To see a list of the ports that are opened by these policies and a list of the policies that are included, see the [README for the Calico public network policies](https://github.com/IBM-Cloud/kube-samples/blob/master/calico-policies/public-network-isolation/README.md){: external}.

When you apply the egress pod policies that are in this policy set, only network traffic to the subnets and ports that are specified in the pod policies is permitted. All traffic to any subnets or ports that are not specified in the policies is blocked for all pods in all namespaces. Because only the ports and subnets that are necessary for the pods to function in {{site.data.keyword.containerlong_notm}} are specified in these policies, your pods can't send network traffic over the internet until you add or change the Calico policy to allow them to.
{: important}

Whenever new locations for {{site.data.keyword.openshiftlong_notm}} and other {{site.data.keyword.cloud_notm}} are enabled, the subnets for these locations are added to the Calico policies. Be sure to [watch the GitHub repository](https://github.com/IBM-Cloud/kube-samples/tree/master/calico-policies/public-network-isolation){: external} for any updates to these policies and keep your local isolation policies up-to-date.
{: note}

Before you begin, [install and configure the Calico CLI, and set the context for your cluster to run Calico commands](#cli_install).

1. Clone the `IBM-Cloud/kube-samples` repository.

    ```sh
    git clone https://github.com/IBM-Cloud/kube-samples.git
    ```
    {: pre}

2. Navigate to the public policy directory for the region that your cluster is in. Example command for a cluster in US South:

    ```sh
    cd <filepath>/IBM-Cloud/kube-samples/calico-policies/public-network-isolation/us-south
    ```
    {: pre}

3. Review each policy for any changes you might need to make. For example, if you specified a custom subnet when you created your cluster that provides the private IP addresses for your pods, you must specify that CIDR instead of the `172.30.0.0/16` CIDR in the `allow-ibm-ports-public.yaml` policy.

4. Apply the policies.

    ```sh
    calicoctl apply -f allow-egress-pods-public.yaml
    calicoctl apply -f allow-ibm-ports-public.yaml
    calicoctl apply -f allow-public-service-endpoint.yaml
    calicoctl apply -f deny-all-outbound-public.yaml
    calicoctl apply -f allow-openshift-console.yaml
    ```
    {: pre}

5. Optional: To allow your worker nodes to access other {{site.data.keyword.cloud_notm}} services over the public network, apply the `allow-public-services.yaml` and `allow-public-services-pods.yaml` policies. The policy allows access to the IP addresses for {{site.data.keyword.registrylong_notm}}, and if the services are available in the region, {{site.data.keyword.la_full_notm}} and {{site.data.keyword.mon_full_notm}}. To access other {{site.data.keyword.cloud_notm}} services, you must manually add the subnets for those services to this policy.

    ```sh
    calicoctl apply -f allow-public-services.yaml
    calicoctl apply -f allow-public-services-pods.yaml
    ```
    {: pre}

6. Verify that the policies are applied.

    ```sh
    calicoctl get GlobalNetworkPolicies -o yaml
    ```
    {: pre}

7. Optional: If you must allow traffic that is not specified by these policies, [create and apply Calico policies](#adding_network_policies) to allow this traffic. For example, if you use any in-cluster webhooks, you must add policies to ensure that the webhooks can make the required connections. You also must create policies for any non-local services that extend the Kubernetes API. You can find these services by running `oc get apiservices`. Note that `default/openshift-apiserver` is included as a local service and does not require a network policy.


## Isolating clusters on the private network
{: #isolate_workers}

You can isolate your cluster from other systems on the private network by applying [Calico private network policies](https://github.com/IBM-Cloud/kube-samples/tree/master/calico-policies/private-network-isolation/calico-v3){: external}.
{: shortdesc}

This set of Calico policies and host endpoints can isolate the private network traffic of a cluster from other resources in the account's private network, while allowing communication on the private network that is necessary for the cluster to function. For example, when you enable [VRF or VLAN spanning](/docs/openshift?topic=openshift-plan_basics#worker-worker) to allow worker nodes to communicate with each other on the private network, any instance that is connected to any of the private VLANs in the same {{site.data.keyword.cloud_notm}} account can communicate with your worker nodes.

To see a list of the ports that are opened by these policies and a list of the policies that are included, see the [README for the Calico private network policies](https://github.com/IBM-Cloud/kube-samples/blob/master/calico-policies/private-network-isolation/README.md){: external}.

When you apply the egress pod policies that are in this policy set, only network traffic to the subnets and ports that are specified in the pod policies is permitted. All traffic to any subnets or ports that are not specified in the policies is blocked for all pods in all namespaces. Because only the ports and subnets that are necessary for the pods to function in {{site.data.keyword.containerlong_notm}} are specified in these policies, your pods can't send network traffic over the private network until you add or change the Calico policy to allow them to.
{: important}

Whenever new locations for {{site.data.keyword.openshiftlong_notm}} and other {{site.data.keyword.cloud_notm}} are enabled, the subnets for these locations are added to the Calico policies. Be sure to [watch the GitHub repository](https://github.com/IBM-Cloud/kube-samples/tree/master/calico-policies/private-network-isolation){: external} for any updates to these policies and keep your local isolation policies up-to-date.
{: note}

Before you begin, [install and configure the Calico CLI, and set the context for your cluster to run Calico commands](#cli_install).

1. Clone the `IBM-Cloud/kube-samples` repository.

    ```sh
    git clone https://github.com/IBM-Cloud/kube-samples.git
    ```
    {: pre}

2. Go to the `calico-v3` private policy directory for the region that your cluster is in. Example command for a cluster in US South:

    ```sh
    cd <filepath>/IBM-Cloud/kube-samples/calico-policies/private-network-isolation/calico-v3/us-south
    ```
    {: pre}

3. Review each policy for any changes you might need to make. For example, if you specified a custom subnet when you created your cluster that provides the private IP addresses for your pods, you must specify that CIDR instead of the `172.30.0.0/16` CIDR in the `allow-all-workers-private.yaml` policy.

4. Apply the policies.

    ```sh
    calicoctl apply -f allow-all-workers-private.yaml
    calicoctl apply -f allow-egress-pods-private.yaml
    calicoctl apply -f allow-ibm-ports-private.yaml
    calicoctl apply -f allow-icmp-private.yaml
    calicoctl apply -f allow-private-service-endpoint.yaml
    calicoctl apply -f allow-sys-mgmt-private.yaml
    calicoctl apply -f deny-all-private-default.yaml
    ```
    {: pre}

5. **{{site.data.keyword.redhat_openshift_notm}} version 3.11 clusters only**: Set up private host endpoints for your worker nodes. When your worker nodes have private host endpoints, the policies that you apply can target the worker node private interface (eth0) and the pod network of a cluster.
    1. Open the `generic-privatehostendpoint.yaml` policy.
    2. Replace `<worker_name>` with the name of a worker node. Note that some worker nodes must follow a different naming structure for Calico policies. You must use the name that is returned when you run `calicoctl get nodes --config=<filepath>/calicoctl.cfg`.
    3. Replace `<worker-node-private-ip>` with the private IP address for the worker node. To see your worker nodes' private IP addresses, run `ibmcloud oc worker ls --cluster <my_cluster>`.
    4. For each worker node in your cluster, repeat these steps in a separate entry in the file. Note that each time you add a worker node to a cluster, you must update the host endpoints file with the new entries.
    5. Save the policy.
    6. Apply the policy.

        ```sh
        calicoctl apply -f generic-privatehostendpoint.yaml
        ```
        {: pre}

6. Optional: To allow your workers and pods to access {{site.data.keyword.registrylong_notm}} over the private network, apply the `allow-private-services.yaml` and `allow-private-services-pods.yaml` policies. To access other {{site.data.keyword.cloud_notm}} services that support private cloud service endpoints, you must manually add the subnets for those services to this policy.

    ```sh
    calicoctl apply -f allow-private-services.yaml
    calicoctl apply -f allow-private-services-pods.yaml
    ```
    {: pre}

7. Optional: To expose your apps with private network load balancers (NLBs) or Ingress application load balancers (ALBs), you must open the VRRP protocol by applying the `allow-vrrp-private` policy.

    ```sh
    calicoctl apply -f allow-vrrp-private.yaml
    ```
    {: pre}

    You can further control access to networking services by creating [Calico pre-DNAT policies](/docs/openshift?topic=openshift-network_policies#block_ingress). In the pre-DNAT policy, ensure that you use `selector: ibm.role=='worker_private'` to apply the policy to the workers' private host endpoints.
    {: tip}

8. Verify that the policies are applied.

    ```sh
    calicoctl get GlobalNetworkPolicies -o yaml
    ```
    {: pre}

9. Optional: If you must allow traffic that is not specified by these policies, [create and apply Calico policies](#adding_network_policies) to allow this traffic. For example, if you use any in-cluster webhooks, you must add policies to ensure that the webhooks can make the required connections. You also must create policies for any non-local services that extend the Kubernetes API. You can find these services by running `oc get apiservices`. Note that `default/openshift-apiserver` is included as a local service and does not require a network policy.


## Controlling traffic between pods
{: #isolate_services}

Kubernetes policies protect pods from internal network traffic. You can create simple [Kubernetes network policies](/docs/containers?topic=containers-vpc-kube-policies) to isolate app microservices from each other within a namespace or across namespaces.

By default, any pod has access to any other pod in the cluster. Additionally, any pod has access to any services that are exposed by the pod network, such as a metrics service, the cluster DNS, the API server, or any services that you manually create in your cluster.





## Logging denied traffic
{: #log_denied}

To log denied traffic requests to certain pods in your cluster, you can create a Calico log network policy.
{: shortdesc}

When you set up network policies to limit traffic to app pods, traffic requests that are not permitted by these policies are denied and dropped. In some scenarios, you might want more information about denied traffic requests. For example, you might notice some unusual traffic that is continuously being denied by one of your network policies. To monitor the potential security threat, you can set up logging to record every time that the policy denies an attempted action on specified app pods.

This section shows you how to log traffic that is denied by a Kubernetes network policy. To log traffic that is denied by a Calico network policy, see [Lesson 5 of the Calico network policy tutorial](/docs/containers?topic=containers-policy_tutorial#lesson5).
{: tip}

Before you begin, [install and configure the Calico CLI, and set the context for your cluster to run Calico commands](#cli_install).

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

    2. Apply the policy. The Kubernetes policy is automatically converted to a Calico `NetworkPolicy` so that Calico can apply it as `Iptables` rules. The Calico network policy name has the `knp.default` prefix. To update the policy in the future, update the Kubernetes policy and the updates are automatically applied to the Calico network policy.

        ```sh
        oc apply -f <policy_name>.yaml
        ```
        {: pre}

    3. Review the syntax of the automatically created Calico policy and copy the value of the `spec.selector` field. If you use a Windows machine, include the `--config=<filepath>/calicoctl.cfg` flag.
        ```sh
        calicoctl get policy -o yaml knp.default.<policy_name> [--config=<filepath>/calicoctl.cfg]
        ```
        {: pre}

        For example, after the Kubernetes policy is applied and converted to a Calico NetworkPolicy, the `access-nginx` policy has the following Calico v3 syntax. The `spec.selector` field has the value `projectcalico.org/orchestrator == 'k8s' && run == 'nginx'`.
        ```yaml
        apiVersion: projectcalico.org/v3
        kind: NetworkPolicy
        metadata:
          name: knp.default.access-nginx
        spec:
          ingress:
          - action: Allow
            destination: {}
            source:
              selector: projectcalico.org/orchestrator == 'k8s' && run == 'access'
          order: 1000
          selector: projectcalico.org/orchestrator == 'k8s' && run == 'nginx'
          types:
          - Ingress
        ```
        {: screen}

2. To log all the traffic that is denied by the policy you created in the previous step, create a Calico NetworkPolicy named `log-denied-packets`. For example, the following log policy uses the same pod selector as the example `access-nginx` Kubernetes policy described in step 1, which adds this policy to the Calico Iptables rule chain. By using a higher-order number, such as `3000`, you can ensure that this rule is added to the end of the Iptables rule chain. Any request packet from the `run=access`-labeled pod that matches the `access-nginx` policy rule is accepted by the `run=nginx`-labeled pods. However, when packets from any other source try to match the low-order `access-nginx` policy rule, they are denied. Those packets then try to match the high-order `log-denied-packets` policy rule. `log-denied-packets` logs any packets that arrive to it, so only packets that were denied by the `run=nginx`-labeled pods are logged. After the packets' attempts are logged, the packets are dropped.

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
    :   This `Ingress` policy applies to all incoming traffic requests. The value `Ingress` is a general term for all incoming traffic, and does not refer to traffic only from the IBM Ingress ALB. |
    `ingress`
    :   `action`: The `Log` action writes a log entry for any requests that match this policy to the `/var/log/syslog` path on the worker node. 
    :   `destination`: No destination is specified because the `selector` applies this policy to all pods with a certain label.
    :   `source`: This policy applies to requests from any source.
    
    `selector`
    :   Replace `<selector>` with the same selector in the `spec.selector` field that you used in your policy from step 1. For example, by using the selector `selector: projectcalico.org/orchestrator == 'k8s' && run == 'nginx'`, this policy's rule is added to the same Iptables chain as the `access-nginx` sample Kubernetes network policy rule in step 1. This policy applies only to incoming network traffic to pods that use the same selector label.
    
    `order`
    :   Calico policies have orders that determine when they are applied to incoming request packets. Policies with lower orders, such as `1000`, are applied first. Policies with higher orders are applied after the lower-order policies. For example, a policy with a very high order, such as `3000`, is effectively applied last after all the lower-order policies have been applied.</br></br>Incoming request packets go through the Iptables rules chain and try to match rules from lower-order policies first. If a packet matches any rule, the packet is accepted. However, if a packet doesn't match any rule, it arrives at the last rule in the Iptables rules chain with the highest order. To make sure that this policy is the last policy in the chain, use a much higher order, such as `3000`, than the policy you created in step 1. 


3. Apply the policy. If you use a Windows machine, include the `--config=<filepath>/calicoctl.cfg` flag.

    ```sh
    calicoctl apply -f log-denied-packets.yaml [--config=<filepath>/calicoctl.cfg]
    ```
    {: pre}

4. Generate log entries by sending requests that are not allowed by the policy that you created in step 1. For example, try to ping the pod that is protected by the network policy from a pod or an IP address that is not permitted.

5. Check for log entries that are written to the `/var/log/syslog` path. The DST (destination) or SRC (source) IP addresses in the log entry might be different than expected due to proxies, Network Address Translation (NAT), and other networking processes. The log entry looks similar to the following.

    ```sh
    Sep 5 14:34:40 <worker_hostname> kernel: [158271.044316] calico-packet: IN=eth1 OUT= MAC=08:00:27:d5:4e:57:0a:00:27:00:00:00:08:00 SRC=192.XXX.XX.X DST=192.XXX.XX.XX LEN=60 TOS=0x00 PREC=0x00 TTL=64 ID=52866 DF PROTO=TCP SPT=42962 DPT=22 WINDOW=29200 RES=0x00 SYN URGP=0
    ```
    {: screen}

6. Optional: Forward the logs from `/var/log/syslog` to [{{site.data.keyword.la_full}}](/docs/openshift?topic=openshift-health#openshift_logging).




