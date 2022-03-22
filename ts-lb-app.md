---

copyright: 
  years: 2014, 2022
lastupdated: "2022-03-22"

keywords: openshift

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}


# Why can't my app connect via a network load balancer (NLB) service?
{: #cs_loadbalancer_fails}
{: support}

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

    * Version 2.0 NLBs
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
        3. In the `spec.selector` section of the LoadBalancer service, ensure that the `<selector_key>` and `<selector_value>` is the same as the key/value pair that you used in the `spec.template.metadata.labels` section of your deployment YAML. If labels don't match, the **Endpoints** section in your LoadBalancer service displays `<none>` and your app is not accessible from the internet.
        4. Check that you used the **port** that your app listens on.
        5. Check that you set `externalTrafficPolicy` to `Local`.

    * Version 1.0 NLBs
    
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
        2. In the `spec.selector` section of the LoadBalancer service, ensure that the `<selector_key>` and `<selector_value>` is the same as the key/value pair that you used in the `spec.template.metadata.labels` section of your deployment YAML. If labels don't match, the **Endpoints** section in your LoadBalancer service displays **<none>** and your app is not accessible from the internet.
        3. Check that you used the **port** that your app listens on.

4. Check your NLB service and review the **Events** section to find potential errors.

    ```sh
    oc describe service <myservice>
    ```
    {: pre}

    Look for the following error messages.

    Clusters with one node must use services of type NodePort
    :   To use the NLB service, you must have a standard cluster with at least two worker nodes.
    
    No cloud provider IPs are available to fulfill the NLB service request. Add a portable subnet to the cluster and try again.
    :   This error message indicates that no portable public IP addresses are left to be allocated to your NLB service. Refer to [Adding subnets to clusters](/docs/openshift?topic=openshift-subnets#subnets) to find information about how to request portable public IP addresses for your cluster. After portable public IP addresses are available to the cluster, the NLB service is automatically created.
    
    Requested cloud provider IP `<cloud-provider-ip>` is not available. The following cloud provider IPs are available: `<available-cloud-provider-ips>`
    :   You defined a portable public IP address for your load balancer YAML by using the `loadBalancerIP` section, but this portable public IP address is not available in your portable public subnet. In the `loadBalancerIP` section your configuration script, remove the existing IP address and add one of the available portable public IP addresses. You can also remove the `loadBalancerIP` section from your script so that an available portable public IP address can be allocated automatically.
    
    No available nodes for NLB services
    :   You don't have enough worker nodes to deploy an NLB service. One reason might be that you deployed a standard cluster with more than one worker node, but the provisioning of the worker nodes failed.
        1. List available worker nodes by running `oc get nodes`.
        2. If at least two available worker nodes are found, list the worker node details by running `ibmcloud oc worker get --cluster <cluster_name_or_ID> --worker <worker_ID>`.
        3. Make sure that the public and private VLAN IDs for the worker nodes that were returned by the `oc get nodes` and the `ibmcloud oc worker get` commands match.

5. If you use a custom domain to connect to your NLB service, make sure that your custom domain is mapped to the public IP address of your NLB service.
    1. Find the public IP address of your NLB service.
        ```sh
        oc describe service <service_name> | grep "LoadBalancer Ingress"
        ```
        {: pre}

    2. Check that your custom domain is mapped to the portable public IP address of your NLB service in the Pointer record (PTR).




