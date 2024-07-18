---

copyright: 
  years: 2014, 2024
lastupdated: "2024-07-18"


keywords: <containers>kubernetes, lb1.0, nlb</containers><openshift>openshift, lb2.0, nlb</openshift>

subcollection: <containers>containers</containers><openshift>openshift</openshift>


---

{{site.data.keyword.attribute-definition-list}}





# Classic: Setting up basic load balancing with an NLB 1.0
{: #loadbalancer}

Version 1.0 NLBs can be created in classic clusters only, and can't be created in VPC clusters. To load balance in VPC clusters, see [Exposing apps with load balancers for VPC](/docs/<containers>containers</containers><openshift>openshift</openshift>?topic=<containers>containers</containers><openshift>openshift</openshift>-vpc-lbaas).
{: note}

Expose a port and use a portable IP address for a Layer 4 network load balancer (NLB) to expose a containerized app. For information about version 1.0 NLBs, see [Components and architecture of an NLB 1.0](/docs/<containers>containers</containers><openshift>openshift</openshift>?topic=<containers>containers</containers><openshift>openshift</openshift>-loadbalancer-about#v1_planning).
{: shortdesc}

## Setting up an NLB 1.0 in a multizone cluster
{: #multi_zone_config}

**Before you begin**:
* To create public network load balancers (NLBs) in multiple zones, at least one public VLAN must have portable subnets available in each zone. To create private NLBs in multiple zones, at least one private VLAN must have portable subnets available in each zone. You can add subnets by following the steps in [Configuring subnets for clusters](/docs/<containers>containers</containers><openshift>openshift</openshift>?topic=<containers>containers</containers><openshift>openshift</openshift>-subnets).
* Enable a [Virtual Router Function (VRF)](/docs/account?topic=account-vrf-service-endpoint&interface=ui) for your IBM Cloud infrastructure account. To enable VRF, see [Enabling VRF](/docs/account?topic=account-vrf-service-endpoint&interface=ui). To check whether a VRF is already enabled, use the `ibmcloud account show` command. If you can't or don't want to enable VRF, enable [VLAN spanning](/docs/vlans?topic=vlans-vlan-spanning#vlan-spanning). When a VRF or VLAN spanning is enabled, the NLB 1.0 can route packets to various subnets in the account.
* Ensure you have the [**Writer** or **Manager** {{site.data.keyword.cloud_notm}} IAM service access role](/docs/<containers>containers</containers><openshift>openshift</openshift>?topic=<containers>containers</containers><openshift>openshift</openshift>-iam-platform-access-roles) for the `default` namespace.
* Ensure you have the required number of worker nodes:<containers>
    * Classic clusters:</containers> If you restrict network traffic to edge worker nodes, ensure that at least two [edge worker nodes](/docs/<containers>containers</containers><openshift>openshift</openshift>?topic=<containers>containers</containers><openshift>openshift</openshift>-edge#edge) are enabled in each zone so that NLBs deploy uniformly.
* When cluster nodes are reloaded or when a cluster master update includes a new `keepalived` image,  the load balancer virtual IP is moved to the network interface of a new node. When this occurs, any long-lasting connections to your load balancer must be re-established. Consider including retry logic in your application so that attempts to re-establish the connection are made quickly.

To set up an NLB 1.0 service in a multizone cluster:
1. [Deploy your app to the cluster](<containers>/docs/containers?topic=containers-deploy_app#app_cli</containers><openshift>/docs/<containers>containers</containers><openshift>openshift</openshift>?topic=<containers>containers</containers><openshift>openshift</openshift>-app</openshift>). Ensure that you add a label in the metadata section of your deployment configuration file. This custom label identifies all pods where your app runs to include them in the load balancing.

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
        spec:
          type: LoadBalancer
          selector:
            <selector_key>: <selector_value>
          ports:
           - protocol: TCP
             port: 8080
             targetPort: 8080 # Optional. By default, the `targetPort` is set to match the `port` value unless specified otherwise. 
          loadBalancerIP: <IP_address>
        ```
        {: codeblock}


        `service.kubernetes.io/ibm-load-balancer-cloud-provider-ip-type`
        :   Annotation to specify a `private` or `public` load balancer. If you don't specify this annotation and your worker nodes are connected to public VLANs, a public `LoadBalancer` service is created. If your worker nodes are connected to private VLANs only, a private `LoadBalancer` service is created.
        
        `service.kubernetes.io/ibm-load-balancer-cloud-provider-zone`
        :   Annotation to specify the zone that the load balancer service deploys to. To see zones, run `<containers>ibmcloud ks</containers><openshift>ibmcloud oc</openshift> zone ls`.
        
        `service.kubernetes.io/ibm-load-balancer-cloud-provider-vlan`
        :   Annotation to specify a VLAN that the load balancer service deploys to. To see VLANs, run `<containers>ibmcloud ks</containers><openshift>ibmcloud oc</openshift> vlan ls --zone <zone>`.
        
        `selector`
        :   The label key (`<selector_key>`) and value (`<selector_value>`) that you used in the `spec.template.metadata.labels` section of your app deployment YAML.
        
        `port`
        :   The port that the service listens on.
        
        `loadBalancerIP`
        :   Optional: To create a private load balancer or to use a specific portable IP address for a public load balancer, specify the IP address that you want to use. The IP address must be on the VLAN and zone that you specify in the annotations. If you don't specify an IP address:
        :   If your cluster is on a public VLAN, a portable public IP address is used. Most clusters are on a public VLAN.
        :   If your cluster is on a private VLAN only, a portable private IP address is used.

        Example configuration file to create a private NLB 1.0 service that uses a specified IP address on private VLAN `2234945` in `dal12`:

        ```yaml
        apiVersion: v1
        kind: Service
        metadata:
          name: myloadbalancer
          annotations:
            service.kubernetes.io/ibm-load-balancer-cloud-provider-ip-type: private
            service.kubernetes.io/ibm-load-balancer-cloud-provider-zone: "dal12"
            service.kubernetes.io/ibm-load-balancer-cloud-provider-vlan: "2234945"
        spec:
          type: LoadBalancer
          selector:
            app: nginx
          ports:
           - protocol: TCP
             port: 8080
             targetPort: 8080 # Optional. By default, the `targetPort` is set to match the `port` value unless specified otherwise. 
          loadBalancerIP: 172.21.xxx.xxx
        ```
        {: codeblock}

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

    In the output, the **LoadBalancer Ingress** IP address is the portable IP address that was assigned to your NLB service:

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

4. If you created a public NLB, access your app from the internet.
    1. Open your preferred web browser.
    2. Enter the portable public IP address of the NLB and port.

        ```sh
        http://169.xx.xxx.xxx:8080
        ```
        {: codeblock}

5. Repeat the steps 2 - 4 to add a version 1.0 NLB in each zone.

6. If you choose to [enable source IP preservation for an NLB 1.0](#lb_source_ip), ensure that app pods are scheduled onto the edge worker nodes by [adding edge node affinity to app pods](#lb_edge_nodes). App pods must be scheduled onto edge nodes to receive incoming requests.

7. Optional: A load balancer service also makes your app available over the service's NodePorts. [NodePorts](/docs/<containers>containers</containers><openshift>openshift</openshift>?topic=<containers>containers</containers><openshift>openshift</openshift>-nodeport) are accessible on every public and private IP address for every node within the cluster. To block traffic to NodePorts while you are using an NLB service, see [Controlling inbound traffic to network load balancer (NLB) or NodePort services](/docs/<containers>containers</containers><openshift>openshift</openshift>?topic=<containers>containers</containers><openshift>openshift</openshift>-network_policies#block_ingress).

Next, you can [register an NLB subdomain](/docs/<containers>containers</containers><openshift>openshift</openshift>?topic=<containers>containers</containers><openshift>openshift</openshift>-loadbalancer_hostname).



## Setting up an NLB 1.0 in a single-zone cluster
{: #lb_config}

**Before you begin**:
* You must have an available portable public or private IP address to assign to the network load balancer (NLB) service. For more information, see [Configuring subnets for clusters](/docs/<containers>containers</containers><openshift>openshift</openshift>?topic=<containers>containers</containers><openshift>openshift</openshift>-subnets).
* Ensure you have the [**Writer** or **Manager** {{site.data.keyword.cloud_notm}} IAM service access role](/docs/<containers>containers</containers><openshift>openshift</openshift>?topic=<containers>containers</containers><openshift>openshift</openshift>-iam-platform-access-roles) for the `default` namespace.
* When cluster nodes are reloaded or when a cluster master update includes a new `keepalived` image,  the load balancer virtual IP is moved to the network interface of a new node. When this occurs, any long-lasting connections to your load balancer must be re-established. Consider including retry logic in your application so that attempts to re-establish the connection are made quickly.

To create an NLB 1.0 service in a single-zone cluster:

1. [Deploy your app to the cluster](<containers>/docs/containers?topic=containers-deploy_app#app_cli</containers><openshift>/docs/<containers>containers</containers><openshift>openshift</openshift>?topic=<containers>containers</containers><openshift>openshift</openshift>-app</openshift>). Ensure that you add a label to your deployment in the metadata section of your configuration file. This label is needed to identify all pods where your app runs so that they are in the load balancing.
2. Create a load balancer service for the app that you want to expose to the public internet or a private network.
    1. Create a service configuration file that is named, for example, `myloadbalancer.yaml`.

    2. Define a load balancer service for the app that you want to expose.
        ```yaml
        apiVersion: v1
        kind: Service
        metadata:
          name: myloadbalancer
          annotations:
            service.kubernetes.io/ibm-load-balancer-cloud-provider-ip-type: <public_or_private>
            service.kubernetes.io/ibm-load-balancer-cloud-provider-vlan: "<vlan_id>"
        spec:
          type: LoadBalancer
          selector:
            <selector_key>: <selector_value>
          ports:
           - protocol: TCP
             port: 8080
             targetPort: 8080 # Optional. By default, the `targetPort` is set to match the `port` value unless specified otherwise. 
          loadBalancerIP: <IP_address>
        ```
        {: codeblock}

        `service.kubernetes.io/ibm-load-balancer-cloud-provider-ip-type:`
        :   Annotation to specify a `private` or `public` load balancer.
        `service.kubernetes.io/ibm-load-balancer-cloud-provider-vlan:`
        :   Annotation to specify a VLAN that the load balancer service deploys to. To see VLANs, run `<containers>ibmcloud ks</containers><openshift>ibmcloud oc</openshift> vlan ls --zone <zone>`.
        `selector`
        :   The label key (<selector_key>) and value (<selector_value>) that you used in the `spec.template.metadata.labels` section of your app deployment YAML.
        
        `port`
        :   The port that the service listens on.
        
        `loadBalancerIP`
        :   Optional: To create a private load balancer or to use a specific portable IP address for a public load balancer, specify the IP address that you want to use. The IP address must be on the VLAN that you specify in the annotations. If you don't specify an IP address:
        :   If your cluster is on a public VLAN, a portable public IP address is used. Most clusters are on a public VLAN.
        :   If your cluster is on a private VLAN only, a portable private IP address is used.

        Example configuration file to create a private NLB 1.0 service that uses a specified IP address on private VLAN `2234945`:

        ```yaml
        apiVersion: v1
        kind: Service
        metadata:
          name: myloadbalancer
          annotations:
            service.kubernetes.io/ibm-load-balancer-cloud-provider-ip-type: private
            service.kubernetes.io/ibm-load-balancer-cloud-provider-vlan: "2234945"
        spec:
          type: LoadBalancer
          selector:
            app: nginx
          ports:
           - protocol: TCP
             port: 8080
             targetPort: 8080 # Optional. By default, the `targetPort` is set to match the `port` value unless specified otherwise. 
          loadBalancerIP: 172.21.xxx.xxx
        ```
        {: codeblock}

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

5. If you choose to [enable source IP preservation for an NLB 1.0](#lb_source_ip), ensure that app pods are scheduled onto the edge worker nodes by [adding edge node affinity to app pods](#lb_edge_nodes). App pods must be scheduled onto edge nodes to receive incoming requests.

6. Optional: A load balancer service also makes your app available over the service's NodePorts. [NodePorts](/docs/<containers>containers</containers><openshift>openshift</openshift>?topic=<containers>containers</containers><openshift>openshift</openshift>-nodeport) are accessible on every public and private IP address for every node within the cluster. To block traffic to NodePorts while you are using an NLB service, see [Controlling inbound traffic to network load balancer (NLB) or NodePort services](/docs/<containers>containers</containers><openshift>openshift</openshift>?topic=<containers>containers</containers><openshift>openshift</openshift>-network_policies#block_ingress).

Next, you can [register an NLB subdomain](/docs/<containers>containers</containers><openshift>openshift</openshift>?topic=<containers>containers</containers><openshift>openshift</openshift>-loadbalancer_hostname#loadbalancer_hostname).



## Enabling source IP preservation
{: #lb_source_ip}

This feature is for version 1.0 network load balancers (NLBs) only. The source IP address of client requests is preserved by default in version 2.0 NLBs.
{: note}

When a client request to your app is sent to your cluster, a load balancer service pod receives the request. If no app pod exists on the same worker node as the load balancer service pod, the NLB forwards the request to a different worker node. The source IP address of the package is changed to the public IP address of the worker node where the load balancer service pod runs.
{: shortdesc}

To preserve the original source IP address of the client request, you can [enable source IP](https://kubernetes.io/docs/tasks/access-application-cluster/create-external-load-balancer/#preserving-the-client-source-ip){: external} for load balancer services. The TCP connection continues all the way to the app pods so that the app can see the actual source IP address of the initiator. Preserving the client’s IP is useful, for example, when app servers have to apply security and access-control policies.

After you enable the source IP, load balancer service pods must forward requests to app pods that are deployed to the same worker node only. Typically, load balancer service pods are also deployed to the worker nodes that the app pods are deployed to. However, some situations exist where the load balancer pods and app pods might not be scheduled onto the same worker node:

* You have edge nodes that are tainted so that only load balancer service pods can deploy to them. App pods are not permitted to deploy to those nodes.
* Your cluster is connected to multiple public or private VLANs, and your app pods might deploy to worker nodes that are connected only to one VLAN. Load balancer service pods might not deploy to those worker nodes because the NLB IP address is connected to a different VLAN than the worker nodes.

To force your app to deploy to specific worker nodes where load balancer service pods can also deploy to, you must add affinity rules and tolerations to your app deployment.

### Adding edge node affinity rules and tolerations
{: #lb_edge_nodes}

When you [label worker nodes as edge nodes](/docs/<containers>containers</containers><openshift>openshift</openshift>?topic=<containers>containers</containers><openshift>openshift</openshift>-edge#edge_nodes_nlb) and also [taint the edge nodes](/docs/<containers>containers</containers><openshift>openshift</openshift>?topic=<containers>containers</containers><openshift>openshift</openshift>-edge#edge_workloads), load balancer service pods deploy only to those edge nodes, and app pods can't deploy to edge nodes. When source IP is enabled for the NLB service, the load balancer pods on the edge nodes can't forward incoming requests to your app pods on other worker nodes.
{: shortdesc}

To force your app pods to deploy to edge nodes, add an edge node [affinity rule](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/){: external} and [toleration](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/){: external} to the app deployment.

Example deployment YAML file with edge node affinity and edge node toleration:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: with-node-affinity
spec:
  selector:
    matchLabels:
      <label_name>: <label_value>
  template:
    spec:
      affinity:
        nodeAffinity:
          requiredDuringSchedulingIgnoredDuringExecution:
            nodeSelectorTerms:
            - matchExpressions:
              - key: dedicated
                operator: In
                values:
                - edge
      tolerations:
        - key: dedicated
          value: edge
...
```
{: codeblock}

Both the **affinity** and **tolerations** sections have `dedicated` as the `key` and `edge` as the `value`.

### Adding affinity rules for multiple public or private VLANs
{: #edge_nodes_multiple_vlans}

When your cluster is connected to multiple public or private VLANs, your app pods might deploy to worker nodes that are connected only to one VLAN. If the NLB IP address is connected to a different VLAN than these worker nodes, load balancer service pods won't deploy to those worker nodes.
{: shortdesc}

When source IP is enabled, schedule app pods on worker nodes that are the same VLAN as the NLB's IP address by adding an affinity rule to the app deployment.

Before you begin: <containers>[Log in to your account. If applicable, target the appropriate resource group. Set the context for your cluster.](/docs/containers?topic=containers-access_cluster)</containers><openshift>[Access your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-access_cluster).</openshift>

1. Get the IP address of the NLB service. Look for the IP address in the **LoadBalancer Ingress** field.
    ```sh
    <containers>kubectl</containers><openshift>oc</openshift> describe service <loadbalancer_service_name>
    ```
    {: pre}

2. Retrieve the VLAN ID that your NLB service is connected to.

    1. List portable public VLANs for your cluster.
        ```sh
        <containers>ibmcloud ks</containers><openshift>ibmcloud oc</openshift> cluster get --cluster <cluster_name_or_ID> --show-resources
        ```
        {: pre}

        Example output
        ```sh
        ...

        Subnet VLANs
        VLAN ID   Subnet CIDR       Public   User-managed
        2234947   10.xxx.xx.xxx/29  false    false
        2234945   169.36.5.xxx/29   true     false
        ```
        {: screen}

    2. In the output under **Subnet VLANs**, look for the subnet CIDR that matches the NLB IP address that you retrieved earlier and note the VLAN ID.

        For example, if the NLB service IP address is `169.36.5.xxx`, the matching subnet in the example output of the previous step is `169.36.5.xxx/29`. The VLAN ID that the subnet is connected to is `2234945`.

3. [Add an affinity rule](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/){: external} to the app deployment for the VLAN ID that you noted in the previous step.

    For example, if you have multiple VLANs but want your app pods to deploy to worker nodes on the `2234945` public VLAN only:

    ```yaml
    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: with-node-affinity
    spec:
      selector:
        matchLabels:
          <label_name>: <label_value>
      template:
        spec:
          affinity:
            nodeAffinity:
              requiredDuringSchedulingIgnoredDuringExecution:
                nodeSelectorTerms:
                - matchExpressions:
                  - key: publicVLAN
                    operator: In
                    values:
                    - "2234945"
    ...
    ```
    {: codeblock}

    In the example YAML, the **affinity** section has `publicVLAN` as the `key` and `"2234945"` as the `value`.

4. Apply the updated deployment configuration file.
    ```sh
    <containers>kubectl</containers><openshift>oc</openshift> apply -f with-node-affinity.yaml
    ```
    {: pre}

5. Verify that the app pods deployed to worker nodes connected to the designated VLAN.

    1. List the pods in your cluster. Replace `<selector>` with the label that you used for the app.
        ```sh
        <containers>kubectl</containers><openshift>oc</openshift> get pods -o wide app=<selector>
        ```
        {: pre}

        Example output
        ```sh
        NAME                   READY     STATUS              RESTARTS   AGE       IP               NODE
        cf-py-d7b7d94db-vp8pq  1/1       Running             0          10d       172.30.xxx.xxx   10.176.48.78
        ```
        {: screen}

    2. In the output, identify a pod for your app. Note the **NODE** ID of the worker node that the pod is on.

        In the example output of the previous step, the app pod `cf-py-d7b7d94db-vp8pq` is on worker node `10.176.48.78`.

    3. List the details for the worker node.

        ```sh
        <containers>kubectl</containers><openshift>oc</openshift> describe node <worker_node_ID>
        ```
        {: pre}

        Example output

        ```sh
        NAME:                   10.xxx.xx.xxx
        Role:
        Labels:                 arch=amd64
        beta.kubernetes.io/arch=amd64
        beta.kubernetes.io/os=linux
        failure-domain.beta.kubernetes.io/region=us-south
        failure-domain.beta.kubernetes.io/zone=dal10
        ibm-cloud.kubernetes.io/encrypted-docker-data=true
        kubernetes.io/hostname=10.xxx.xx.xxx
        privateVLAN=2234945
        publicVLAN=2234967
        ...
        ```
        {: screen}

    4. In the **Labels** section of the output, verify that the public or private VLAN is the VLAN that you designated in previous steps.




