---

copyright: 
  years: 2014, 2024
lastupdated: "2024-07-18"


keywords: <containers>kubernetes, lb2.0, nlb</containers><openshift>openshift, lb2.0, nlb</openshift>

subcollection: <containers>containers</containers><openshift>openshift</openshift>


---

{{site.data.keyword.attribute-definition-list}}





# Classic: Setting up DSR load balancing with an NLB 2.0
{: #loadbalancer-v2}

Version 2.0 NLBs can be created in classic clusters only, and can't be created in VPC clusters. To load balance in VPC clusters, see [Exposing apps with load balancers for VPC](/docs/<containers>containers</containers><openshift>openshift</openshift>?topic=<containers>containers</containers><openshift>openshift</openshift>-vpc-lbaas).
{: note}

Expose a port and use a portable IP address for a Layer 4 network load balancer (NLB) to expose a containerized app. For more information about version 2.0 NLBs, see [Components and architecture of an NLB 2.0](/docs/<containers>containers</containers><openshift>openshift</openshift>?topic=<containers>containers</containers><openshift>openshift</openshift>-loadbalancer-about#planning_ipvs).
{: shortdesc}

## Prerequisites
{: #ipvs_provision}

You can't update an existing version 1.0 NLB to 2.0. You must create a new NLB 2.0. Note that you can run version 1.0 and 2.0 NLBs simultaneously in a cluster.<openshift> To use NLB 2.0, your cluster must run {{site.data.keyword.redhat_openshift_notm}} version 4.</openshift>
{: shortdesc}

Before you create an NLB 2.0, you must complete the following prerequisite steps.

1. To allow your NLB 2.0 to forward requests to app pods in multiple zones, open a support case to request capacity aggregation for your VLANs. This configuration setting does not cause any network disruptions or outages.
    1. Log in to the [{{site.data.keyword.cloud_notm}} console](https://cloud.ibm.com/).
    2. From the menu bar, click **Support**, click the **Manage cases** tab, and click **Create new case**.
    3. In the case fields, enter the following:
        Topic: Network - Provisioning
        Subtopic: Classic - VLAN
    4. Add the following information to the description: `Please set up the network to allow capacity aggregation on the public and private VLANs associated with my account. This is related to /docs/<containers>containers</containers><openshift>openshift</openshift>?topic=<containers>containers</containers><openshift>openshift</openshift>-loadbalancer-v2#ipvs_provision, and is needed so I can configure NLB v2.0 LoadBalancers in my Classic Kubernetes Cluster.`. Note that if you want to allow capacity aggregation on specific VLANs, such as the public VLANs for one cluster only, you can specify those VLAN IDs in the description.
    5. Click **Submit**.

2. Enable a [Virtual Router Function (VRF)](/docs/account?topic=account-vrf-service-endpoint&interface=ui) for your IBM Cloud infrastructure account. To enable VRF, see [Enabling VRF](/docs/account?topic=account-vrf-service-endpoint&interface=ui). To check whether a VRF is already enabled, use the `ibmcloud account show` command. If you can't or don't want to enable VRF, enable [VLAN spanning](/docs/vlans?topic=vlans-vlan-spanning#vlan-spanning). When a VRF or VLAN spanning is enabled, the NLB 2.0 can route packets to various subnets in the account.

3. If you use [Calico pre-DNAT network policies](/docs/<containers>containers</containers><openshift>openshift</openshift>?topic=<containers>containers</containers><openshift>openshift</openshift>-network_policies#block_ingress) to manage traffic to an NLB 2.0, you must add the `applyOnForward: true` and `doNotTrack: true` fields to and remove the `preDNAT: true` from the `spec` section in the policies. `applyOnForward: true` ensures that the Calico policy is applied to the traffic as it is encapsulated and forwarded. `doNotTrack: true` ensures that the worker nodes can use DSR to return a response packet directly to the client without needing the connection to be tracked. For example, if you use a Calico policy to allow traffic from only specific IP addresses to your NLB IP address, the policy looks similar to the following:
    ```yaml
    apiVersion: projectcalico.org/v3
    kind: GlobalNetworkPolicy
    metadata:
      name: allowlist
    spec:
      applyOnForward: true
      doNotTrack: true
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
    {: screen}

Next, you can follow the steps in [Setting up an NLB 2.0 in a multizone cluster](#ipvs_multi_zone_config) or [in a single-zone cluster](#ipvs_single_zone_config).



## Setting up an NLB 2.0 in a multizone cluster
{: #ipvs_multi_zone_config}

**Before you begin**:

* **Important**: Complete the [NLB 2.0 prerequisites](#ipvs_provision).
* To create public NLBs in multiple zones, at least one public VLAN must have portable subnets available in each zone. To create private NLBs in multiple zones, at least one private VLAN must have portable subnets available in each zone. You can add subnets by following the steps in [Configuring subnets for clusters](/docs/<containers>containers</containers><openshift>openshift</openshift>?topic=<containers>containers</containers><openshift>openshift</openshift>-subnets).
* Ensure that you have the [**Writer** or **Manager** {{site.data.keyword.cloud_notm}} IAM service access role](/docs/<containers>containers</containers><openshift>openshift</openshift>?topic=<containers>containers</containers><openshift>openshift</openshift>-iam-platform-access-roles) for the `default` namespace.
* Ensure you have the required number of worker nodes:
    * Classic clusters: If you restrict network traffic to edge worker nodes, ensure that at least two [edge worker nodes](/docs/<containers>containers</containers><openshift>openshift</openshift>?topic=<containers>containers</containers><openshift>openshift</openshift>-edge#edge) are enabled in each zone so that NLBs deploy uniformly.
* When cluster nodes are reloaded or when a cluster master update includes a new `keepalived` image,  the load balancer virtual IP is moved to the network interface of a new node. When this occurs, any long-lasting connections to your load balancer must be re-established. Consider including retry logic in your application so that attempts to re-establish the connection are made quickly.

To set up an NLB 2.0 in a multizone cluster:
1. [Deploy your app to the cluster](<containers>/docs/containers?topic=containers-deploy_app#app_cli</containers><openshift>/docs/<containers>containers</containers><openshift>openshift</openshift>?topic=<containers>containers</containers><openshift>openshift</openshift>-app</openshift>). Ensure that you add a label to your deployment in the metadata section of your configuration file. This custom label identifies all pods where your app runs to include them in the load balancing.

2. Create a load balancer service for the app that you want to expose to the public internet or a private network.
    1. Create a service configuration file that is named, for example, `myloadbalancer.yaml`.
    2. Define a load balancer service for the app that you want to expose. You can specify a zone, a VLAN, and an IP address.

        ```yaml
        apiVersion: v1
        kind: Service
        metadata:
          name: myloadbalancer
          annotations:
            service.kubernetes.io/ibm-load-balancer-cloud-provider-ip-type: <public_or_private>
            service.kubernetes.io/ibm-load-balancer-cloud-provider-zone: "<zone>"
            service.kubernetes.io/ibm-load-balancer-cloud-provider-vlan: "<vlan_id>"
            service.kubernetes.io/ibm-load-balancer-cloud-provider-enable-features: "ipvs"
            service.kubernetes.io/ibm-load-balancer-cloud-provider-ipvs-scheduler: "<algorithm>"
       spec:
         type: LoadBalancer
         selector:
           <selector_key>: <selector_value>
         ports:
          - protocol: TCP
            port: 8080
            targetPort: 8080 # Optional. By default, the `targetPort` is set to match the `port` value unless specified otherwise. 
         loadBalancerIP: <IP_address>
         externalTrafficPolicy: Local
        ```
        {: codeblock}

        `service.kubernetes.io/ibm-load-balancer-cloud-provider-ip-type:`
        :   Annotation to specify a `private` or `public` load balancer.


        `service.kubernetes.io/ibm-load-balancer-cloud-provider-zone:`
        :   Annotation to specify the zone that the load balancer service deploys to. To see zones, run `<containers>ibmcloud ks</containers><openshift>ibmcloud oc</openshift> zone ls`.


        `service.kubernetes.io/ibm-load-balancer-cloud-provider-vlan:`
        :   Annotation to specify a VLAN that the load balancer service deploys to. To see VLANs, run `<containers>ibmcloud ks</containers><openshift>ibmcloud oc</openshift> vlan ls --zone <zone>`.


        `service.kubernetes.io/ibm-load-balancer-cloud-provider-enable-features: "ipvs"`
        :   Annotation to specify a version 2.0 load balancer.


        `service.kubernetes.io/ibm-load-balancer-cloud-provider-ipvs-scheduler:`
        :   Optional: Annotation to specify the scheduling algorithm. Accepted values are `"rr"` for round-robin (default) or `"sh"` for Source Hashing. For more information, see [2.0: Scheduling algorithms](#scheduling).


        `selector`
        :   The label key (`<selector_key>`) and value (`<selector_value>`) that you used in the `spec.template.metadata.labels` section of your app deployment YAML.


        `port`
        :   The port that the service listens on.


        `loadBalancerIP`
        :   Optional: To create a private NLB or to use a specific portable IP address for a public NLB, specify the IP address that you want to use. The IP address must be in the zone and VLAN that you specify in the annotations. If you don't specify an IP address: If your cluster is on a public VLAN, a portable public IP address is used. Most clusters are on a public VLAN. If your cluster is on a private VLAN only, a portable private IP address is used.


        `externalTrafficPolicy: Local`
        :   Set to `Local`.


        Example configuration file to create an NLB 2.0 service in `dal12` that uses the round-robin scheduling algorithm:

        ```yaml
        apiVersion: v1
        kind: Service
        metadata:
          name: myloadbalancer
          annotations:
            service.kubernetes.io/ibm-load-balancer-cloud-provider-zone: "dal12"
            service.kubernetes.io/ibm-load-balancer-cloud-provider-enable-features: "ipvs"
            service.kubernetes.io/ibm-load-balancer-cloud-provider-ipvs-scheduler: "rr"
        spec:
          type: LoadBalancer
           selector:
             app: nginx
           ports:
            - protocol: TCP
              port: 8080
              targetPort: 8080 # Optional. By default, the `targetPort` is set to match the `port` value unless specified otherwise. 
           externalTrafficPolicy: Local
        ```
        {: codeblock}

    3. Optional: Make your NLB service available to only a limited range of IP addresses by specifying the IPs in the `spec.loadBalancerSourceRanges` field. `loadBalancerSourceRanges` is implemented by `kube-proxy` in your cluster via Iptables rules on worker nodes. For more information, see the [Kubernetes documentation](https://kubernetes.io/docs/concepts/services-networking/){: external}.

    4. Create the service in your cluster.

        ```sh
        <containers>kubectl</containers><openshift>oc</openshift> apply -f myloadbalancer.yaml
        ```
        {: pre}

3. Verify that the NLB service was created successfully. It might take a few minutes for the NLB service to be created properly and for the app to be available.

    ```sh
    <containers>kubectl</containers><openshift>oc</openshift> describe service myloadbalancer
    ```
    {: pre}

    Example CLI output:

    ```sh
    NAME:                   myloadbalancer
    Namespace:              default
    Labels:                 <none>
    Selector:               app=liberty
    Type:                   LoadBalancer
    Zone:                   dal10
    IP:                     172.21.xxx.xxx
    LoadBalancer Ingress:   169.xx.xxx.xxx
    Port:                   <unset> 8080/TCP
    NodePort:               <unset> 32040/TCP
    Endpoints:              172.30.xxx.xxx:8080
    Session Affinity:       None
    Events:
        FirstSeen    LastSeen    Count    From            SubObjectPath    Type     Reason                      Message
        ---------    --------    -----    ----            -------------    ----     ------                      -------
        10s            10s            1        {service-controller }      Normal CreatingLoadBalancer    Creating load balancer
        10s            10s            1        {service-controller }        Normal CreatedLoadBalancer    Created load balancer
    ```
    {: screen}

    The **LoadBalancer Ingress** IP address is the portable IP address that was assigned to your NLB service.

4. If you created a public NLB, access your app from the internet.
    1. Open your preferred web browser.
    2. Enter the portable public IP address of the NLB and port.

        ```sh
        http://169.xx.xxx.xxx:8080
        ```
        {: codeblock}

5. To achieve high availability, repeat the steps 2 - 4 to add an NLB 2.0 in each zone where you have app instances.

6. Optional: An NLB service also makes your app available over the service's NodePorts. [NodePorts](/docs/<containers>containers</containers><openshift>openshift</openshift>?topic=<containers>containers</containers><openshift>openshift</openshift>-nodeport) are accessible on every public and private IP address for every node within the cluster. To block traffic to NodePorts while you are using an NLB service, see [Controlling inbound traffic to network load balancer (NLB) or NodePort services](/docs/<containers>containers</containers><openshift>openshift</openshift>?topic=<containers>containers</containers><openshift>openshift</openshift>-network_policies#block_ingress).

Next, you can [register an NLB subdomain](/docs/<containers>containers</containers><openshift>openshift</openshift>?topic=<containers>containers</containers><openshift>openshift</openshift>-loadbalancer_hostname).


## Setting up an NLB 2.0 in a single-zone cluster
{: #ipvs_single_zone_config}

**Before you begin**:

* **Important**: Complete the [NLB 2.0 prerequisites](#ipvs_provision).
* You must have an available portable public or private IP address to assign to the NLB service. For more information, see [Configuring subnets for clusters](/docs/<containers>containers</containers><openshift>openshift</openshift>?topic=<containers>containers</containers><openshift>openshift</openshift>-subnets).
* Ensure that you have the [**Writer** or **Manager** {{site.data.keyword.cloud_notm}} IAM service access role](/docs/<containers>containers</containers><openshift>openshift</openshift>?topic=<containers>containers</containers><openshift>openshift</openshift>-iam-platform-access-roles) for the `default` namespace.
* When cluster nodes are reloaded or when a cluster master update includes a new `keepalived` image,  the load balancer virtual IP is moved to the network interface of a new node. When this occurs, any long-lasting connections to your load balancer must be re-established. Consider including retry logic in your application so that attempts to re-establish the connection are made quickly.

To create an NLB 2.0 service in a single-zone cluster:

1. [Deploy your app to the cluster](<containers>/docs/containers?topic=containers-deploy_app#app_cli</containers><openshift>/docs/<containers>containers</containers><openshift>openshift</openshift>?topic=<containers>containers</containers><openshift>openshift</openshift>-app</openshift>). Ensure that you add a label to your deployment in the metadata section of your configuration file. This label is needed to identify all pods where your app runs so that they are in the load balancing.
2. Create a load balancer service for the app that you want to expose to the public internet or a private network.
    1. Create a service configuration file that is named, for example, `myloadbalancer.yaml`.

    2. Define a load balancer 2.0 service for the app that you want to expose.
        ```yaml
        apiVersion: v1
        kind: Service
        metadata:
          name: myloadbalancer
          annotations:
            service.kubernetes.io/ibm-load-balancer-cloud-provider-ip-type: <public_or_private>
            service.kubernetes.io/ibm-load-balancer-cloud-provider-vlan: "<vlan_id>"
            service.kubernetes.io/ibm-load-balancer-cloud-provider-enable-features: "ipvs"
            service.kubernetes.io/ibm-load-balancer-cloud-provider-ipvs-scheduler: "<algorithm>"
        spec:
          type: LoadBalancer
          selector:
            <selector_key>: <selector_value>
          ports:
           - protocol: TCP
             port: 8080
             targetPort: 8080 # Optional. By default, the `targetPort` is set to match the `port` value unless specified otherwise. 
          loadBalancerIP: <IP_address>
          externalTrafficPolicy: Local
        ```
        {: codeblock}

        `service.kubernetes.io/ibm-load-balancer-cloud-provider-ip-type:`
        :   Annotation to specify a `private` or `public` load balancer.


        `service.kubernetes.io/ibm-load-balancer-cloud-provider-vlan:`
        :   Optional: Annotation to specify a VLAN that the load balancer service deploys to. To see VLANs, run `<containers>ibmcloud ks</containers><openshift>ibmcloud oc</openshift> vlan ls --zone <zone>`.


        `service.kubernetes.io/ibm-load-balancer-cloud-provider-enable-features: "ipvs"`
        :   Annotation to specify a load balancer 2.0.


        `service.kubernetes.io/ibm-load-balancer-cloud-provider-ipvs-scheduler:`
        :   Optional: Annotation to specify a scheduling algorithm. Accepted values are `"rr"` for round-robin (default) or `"sh"` for Source Hashing. For more information, see [2.0: Scheduling algorithms](#scheduling).


        `selector`
        :   The label key (<selector_key>) and value (<selector_value>) that you used in the `spec.template.metadata.labels` section of your app deployment YAML.


        `port`
        :   The port that the service listens on.


        `loadBalancerIP`
        :   Optional: To create a private NLB or to use a specific portable IP address for a public NLB, specify the IP address that you want to use. The IP address must be on the VLAN that you specify in the annotations. If you don't specify an IP address:
            - If your cluster is on a public VLAN, a portable public IP address is used. Most clusters are on a public VLAN.
            - If your cluster is on a private VLAN only, a portable private IP address is used.


        `externalTrafficPolicy: Local`
        :   Set to `Local`.

    3. Optional: Make your NLB service available to only a limited range of IP addresses by specifying the IPs in the `spec.loadBalancerSourceRanges` field. `loadBalancerSourceRanges` is implemented by `kube-proxy` in your cluster via Iptables rules on worker nodes. For more information, see the [Kubernetes documentation](https://kubernetes.io/docs/concepts/services-networking/){: external}.

    4. Create the service in your cluster.

        ```sh
        <containers>kubectl</containers><openshift>oc</openshift> apply -f myloadbalancer.yaml
        ```
        {: pre}

3. Verify that the NLB service was created successfully. It might take a few minutes for the service to be created and for the app to be available.

    ```sh
    <containers>kubectl</containers><openshift>oc</openshift> describe service myloadbalancer
    ```
    {: pre}

    Example CLI output:

    ```sh
    NAME:                   myloadbalancer
    Namespace:              default
    Labels:                 <none>
    Selector:               app=liberty
    Type:                   LoadBalancer
    Location:               dal10
    IP:                     172.21.xxx.xxx
    LoadBalancer Ingress:   169.xx.xxx.xxx
    Port:                   <unset> 8080/TCP
    NodePort:               <unset> 32040/TCP
    Endpoints:              172.30.xxx.xxx:8080
    Session Affinity:       None
    Events:
        FirstSeen    LastSeen    Count    From            SubObjectPath    Type     Reason                      Message
        ---------    --------    -----    ----            -------------    ----     ------                      -------
        10s            10s            1        {service-controller }      Normal CreatingLoadBalancer    Creating load balancer
        10s            10s            1        {service-controller }        Normal CreatedLoadBalancer    Created load balancer
    ```
    {: screen}

    The **LoadBalancer Ingress** IP address is the portable IP address that was assigned to your NLB service.

4. If you created a public NLB, access your app from the internet.
    1. Open your preferred web browser.
    2. Enter the portable public IP address of the NLB and port.

        ```sh
        http://169.xx.xxx.xxx:8080
        ```
        {: codeblock}

5. Optional: An NLB service also makes your app available over the service's NodePorts. [NodePorts](/docs/<containers>containers</containers><openshift>openshift</openshift>?topic=<containers>containers</containers><openshift>openshift</openshift>-nodeport) are accessible on every public and private IP address for every node within the cluster. To block traffic to NodePorts while you are using an NLB service, see [Controlling inbound traffic to network load balancer (NLB) or NodePort services](/docs/<containers>containers</containers><openshift>openshift</openshift>?topic=<containers>containers</containers><openshift>openshift</openshift>-network_policies#block_ingress).

Next, you can [register an NLB subdomain](/docs/<containers>containers</containers><openshift>openshift</openshift>?topic=<containers>containers</containers><openshift>openshift</openshift>-loadbalancer_hostname).



## Scheduling algorithms
{: #scheduling}

Scheduling algorithms determine how an NLB 2.0 assigns network connections to your app pods. As client requests arrive to your cluster, the NLB routes the request packets to worker nodes based on the scheduling algorithm. To use a scheduling algorithm, specify its `Keepalived` short name in the scheduler annotation of your NLB service configuration file: `service.kubernetes.io/ibm-load-balancer-cloud-provider-ipvs-scheduler: "rr"`. Check the following lists to see which scheduling algorithms are supported in <containers>{{site.data.keyword.containerlong_notm}}</containers><openshift>{{site.data.keyword.openshiftlong_notm}}</openshift>. If you don't specify a scheduling algorithm, the round-robin algorithm is used by default. For more information, see the [`Keepalived` documentation](https://www.keepalived.org/doc/scheduling_algorithms.html){: external}.


### Supported scheduling algorithms
{: #scheduling_supported}

Round Robin (`rr`)
:   The NLB cycles through the list of app pods when routing connections to worker nodes, treating each app pod equally. round-robin is the default scheduling algorithm for version 2.0 NLBs.

Source Hashing (`sh`)
:   The NLB generates a hash key based on the source IP address of the client request packet. The NLB then looks up the hash key in a statically assigned hash table, and routes the request to the app pod that handles hashes of that range. This algorithm ensures that requests from a particular client are always directed to the same app pod. Kubernetes uses Iptables rules, which cause requests to be sent to a random pod on the worker. To use this scheduling algorithm, you must ensure that no more than one pod of your app is deployed per worker node. For example, if each pod has the label `run=<app_name>`, add the following anti-affinity rule to the `spec` section of your app deployment:

```yaml
spec:
  affinity:
  podAntiAffinity:
    preferredDuringSchedulingIgnoredDuringExecution:
    - weight: 100
      podAffinityTerm:
        labelSelector:
          matchExpressions:
          - key: run
            operator: In
            values:
            - <APP_NAME>
        topologyKey: kubernetes.io/hostname
```
{: codeblock}


### Unsupported scheduling algorithms
{: #scheduling_unsupported}

Destination Hashing (`dh`)
:   The destination of the packet, which is the NLB IP address and port, is used to determine which worker node handles the incoming request. However, the IP address and port for NLBs in <containers>{{site.data.keyword.containerlong_notm}}</containers><openshift>{{site.data.keyword.openshiftlong_notm}}</openshift> don't change. The NLB is forced to keep the request within the same worker node that it is on, so only app pods on one worker handle all incoming requests.

Dynamic connection counting algorithms
:   The following algorithms depend on dynamic counting of connections between clients and NLBs. However, because direct service return (DSR) prevents NLB 2.0 pods from being in the return packet path, NLBs don't track established connections.
    - Least Connection (`lc`)
    - Locality-Based Least Connection (`lblc`)
    - Locality-Based Least Connection with Replication (`lblcr`)
    - Never Queue (`nq`)
    - Shortest Expected Delay (`seq`)

Weighted pod algorithms
:   The following algorithms depend on weighted app pods. However, in <containers>{{site.data.keyword.containerlong_notm}}</containers><openshift>{{site.data.keyword.openshiftlong_notm}}</openshift>, all app pods are assigned equal weight for load balancing.
    - Weighted Least Connection (`wlc`)
    - Weighted round-robin (`wrr`)



