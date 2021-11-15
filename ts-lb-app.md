---

copyright: 
  years: 2014, 2021
lastupdated: "2021-11-15"

keywords: openshift

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}


# Classic clusters: Why can't my app connect via a network load balancer (NLB) service?
{: #cs_loadbalancer_fails}

**Infrastructure provider**: ![Classic infrastructure provider icon.](images/icon-classic-2.svg) Classic

You exposed your app by creating an NLB service in your classic cluster.
{: tsSymptoms} 

When you tried to connect to your app by using the public IP address of the NLB, the connection failed or timed out.


Your NLB service might not be working properly for one of the following reasons:
{: tsCauses}

    - The cluster is a free cluster or a standard cluster with only one worker node.
    - The cluster is not fully deployed yet.
    - The configuration script for your NLB service includes errors.


Check that you set up a standard cluster that is fully deployed and has at least two worker nodes to ensure high availability for your NLB service.
{: tsResolve} 

1. List your worker nodes. In your CLI output, make sure that the **Status** of your worker nodes displays **Ready** and that the **Machine Type** shows a flavor other than **free**.


    ```sh
    ibmcloud oc worker ls --cluster <cluster_name_or_ID>
    ```
    {: pre}

2. For version 2.0 NLBs: Ensure that you complete the [NLB 2.0 prerequisites](/docs/openshift?topic=openshift-loadbalancer-v2#ipvs_provision).

3. Check the accuracy of the configuration file for your NLB service.
    * Version 2.0 NLBs:
        ```yaml
        apiVersion: v1
        kind: Service
        metadata:
          name: myservice
          annotations:
            service.kubernetes.io/ibm-load-balancer-cloud-provider-enable-features: "ipvs"
        spec:
          type: LoadBalancer
          selector:
            <selector_key>:<selector_value>
          ports:
           - protocol: TCP
             port: 8080
          externalTrafficPolicy: Local
        ```
        {: screen}

        1. Check that you defined **LoadBalancer** as the type for your service.
        2. Check that you included the `service.kubernetes.io/ibm-load-balancer-cloud-provider-enable-features: "ipvs"` annotation.
        3. In the `spec.selector` section of the LoadBalancer service, ensure that the `<selector_key>` and `<selector_value>` is the same as the key/value pair that you used in the `spec.template.metadata.labels` section of your deployment YAML. If labels do not match, the **Endpoints** section in your LoadBalancer service displays **<none>** and your app is not accessible from the internet.
        4. Check that you used the **port** that your app listens on.
        5. Check that you set `externalTrafficPolicy` to `Local`.

    * Version 1.0 NLBs:
        ```yaml
        apiVersion: v1
        kind: Service
        metadata:
          name: myservice
        spec:
          type: LoadBalancer
          selector:
            <selector_key>:<selector_value>
          ports:
           - protocol: TCP
             port: 8080
        ```
        {: screen}

        1. Check that you defined **LoadBalancer** as the type for your service.
        2. In the `spec.selector` section of the LoadBalancer service, ensure that the `<selector_key>` and `<selector_value>` is the same as the key/value pair that you used in the `spec.template.metadata.labels` section of your deployment YAML. If labels do not match, the **Endpoints** section in your LoadBalancer service displays **<none>** and your app is not accessible from the internet.
        3. Check that you used the **port** that your app listens on.

3. Check your NLB service and review the **Events** section to find potential errors.

    ```sh
    oc describe service <myservice>
    ```
    {: pre}

    Look for the following error messages:

    <ul><li><pre class="screen"><code>Clusters with one node must use services of type NodePort</code></pre></br>To use the NLB service, you must have a standard cluster with at least two worker nodes.</li>
    <li><pre class="screen"><code>No cloud provider IPs are available to fulfill the NLB service request. Add a portable subnet to the cluster and try again</code></pre></br>This error message indicates that no portable public IP addresses are left to be allocated to your NLB service. Refer to <a href="/docs/openshift?topic=openshift-subnets#subnets">Adding subnets to clusters</a> to find information about how to request portable public IP addresses for your cluster. After portable public IP addresses are available to the cluster, the NLB service is automatically created.</li>
    <li><pre class="screen"><code>Requested cloud provider IP &lt;cloud-provider-ip&gt; is not available. The following cloud provider IPs are available: &lt;available-cloud-provider-ips&gt;</code></pre></br>You defined a portable public IP address for your load balancer YAML by using the <strong><code>loadBalancerIP</code></strong> section, but this portable public IP address is not available in your portable public subnet. In the <strong><code>loadBalancerIP</code></strong> section your configuration script, remove the existing IP address and add one of the available portable public IP addresses. You can also remove the <strong><code>loadBalancerIP</code></strong> section from your script so that an available portable public IP address can be allocated automatically.</li>
    <li><pre class="screen"><code>No available nodes for NLB services</code></pre>You do not have enough worker nodes to deploy an NLB service. One reason might be that you deployed a standard cluster with more than one worker node, but the provisioning of the worker nodes failed.</li>
    <ol><li>List available worker nodes.</br><pre class="pre"><code>oc get nodes</code></pre></li>
    <li>If at least two available worker nodes are found, list the worker node details.</br><pre class="pre"><code>ibmcloud oc worker get --cluster &lt;cluster_name_or_ID&gt; --worker &lt;worker_ID&gt;</code></pre></li>
    <li>Make sure that the public and private VLAN IDs for the worker nodes that were returned by the <code>oc get nodes</code> and the <code>ibmcloud oc worker get</code> commands match.</li></ol></li></ul>

4. If you use a custom domain to connect to your NLB service, make sure that your custom domain is mapped to the public IP address of your NLB service.
    1. Find the public IP address of your NLB service.
        ```sh
        oc describe service <service_name> | grep "LoadBalancer Ingress"
        ```
        {: pre}

    2. Check that your custom domain is mapped to the portable public IP address of your NLB service in the Pointer record (PTR).




