---

copyright:
  years: 2014, 2020
lastupdated: "2020-08-03"

keywords: openshift, roks, rhos, rhoks

subcollection: openshift

---

{:beta: .beta}
{:codeblock: .codeblock}
{:deprecated: .deprecated}
{:download: .download}
{:external: target="_blank" .external}
{:faq: data-hd-content-type='faq'}
{:gif: data-image-type='gif'}
{:help: data-hd-content-type='help'}
{:important: .important}
{:new_window: target="_blank"}
{:note: .note}
{:pre: .pre}
{:preview: .preview}
{:screen: .screen}
{:shortdesc: .shortdesc}
{:support: data-reuse='support'}
{:table: .aria-labeledby="caption"}
{:tip: .tip}
{:troubleshoot: data-hd-content-type='troubleshoot'}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:tsSymptoms: .tsSymptoms}
{:step: data-tutorial-type='step'}


# VPC: Exposing apps with VPC load balancers
{: #vpc-lbaas}

<img src="images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> VPC load balancers can be created for VPC clusters only, and cannot be created for classic clusters. To load balance in classic clusters, see [About NLBs](/docs/openshift?topic=openshift-loadbalancer-about).

Set up a Load Balancer for VPC to expose your app on the public or private network.
{: shortdesc}

## About VPC load balancing in Red Hat OpenShift on IBM Cloud
{: #lbaas_about}

When you create a Kubernetes `LoadBalancer` service for an app in your cluster, a layer 7 [Load Balancer for VPC](/docs/vpc?topic=vpc-load-balancers) is automatically created in your VPC outside of your cluster. The load balancer is multizonal and routes requests for your app through the private NodePorts that are automatically opened on your worker nodes.
{: shortdesc}

The VPC load balancer serves as the external entry point for incoming requests for the app.
* If you create a **public** Kubernetes `LoadBalancer` service, you can access your app from the internet through the hostname that is assigned by the VPC load balancer to the Kubernetes `LoadBalancer` service in the format `1234abcd-<region>.lb.appdomain.cloud`. Even though your worker nodes are connected to only a private VPC subnet, the VPC load balancer can receive and route public requests to the service that exposes your app. Note that no public gateway is required on your VPC subnet to allow public requests to your VPC load balancer. However, if your app must access a public URL, you must attach public gateways to the VPC subnets that your worker nodes are connected to.
* If you create a **private** Kubernetes `LoadBalancer` service, your app is accessible only to systems that are connected to your private subnets within the same region and VPC. If you are connected to your private VPC network, you can access your app through the hostname that is assigned by the VPC load balancer to the Kubernetes `LoadBalancer` service in the format `1234abcd-<region>.lb.appdomain.cloud`.

The following diagram illustrates how a user accesses an app from the internet through the VPC load balancer.

<img src="images/vpc_tutorial_lesson4_lb.png" width="800" alt="VPC load balancing for a cluster" style="width:600px; border-style: none"/>

A request to your app uses the hostname that is assigned to the Kubernetes `LoadBalancer` service by the VPC load balancer. The request is automatically forwarded by the VPC load balancer to one of the node ports on the worker, and further to the private IP address of the app pod. If app instances are deployed to multiple worker nodes in the cluster, the load balancer routes the requests between the app pods on various worker nodes. Additionally, if you have a multizone cluster, the VPC load balancer routes requests to worker nodes across all subnets and zones in your cluster.

<br />


## Setting up a Load Balancer for VPC
{: #setup_vpc_ks_vpc_lb}

Expose your app to the public or to the private network by setting up a Kubernetes `LoadBalancer` service in your cluster. When you expose your app, a Load Balancer for VPC that routes requests to your app is automatically created for you in your VPC outside of your cluster.
{: shortdesc}

**Before you begin**:
* Ensure that you have the [**Writer** or **Manager** {{site.data.keyword.cloud_notm}} IAM service role](/docs/openshift?topic=openshift-users#platform) for the `default` namespace.
* [Access your {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-access_cluster).
* VPC Gen 2 clusters: [Allow traffic requests that are routed by the VPC load balancer to node ports on your worker nodes](/docs/openshift?topic=openshift-vpc-network-policy#security_groups).

</br>**To enable your app to receive public or private requests:**
1.  [Deploy your app to the cluster](/docs/openshift?topic=openshift-openshift_apps). Ensure that you add a label in the metadata section of your deployment configuration file. This custom label identifies all pods where your app runs to include them in the load balancing.

2. Create a configuration YAML file for your Kubernetes `LoadBalancer` service and name the file `myloadbalancer.yaml`.
  ```yaml
  apiVersion: v1
  kind: Service
  metadata:
    name: myloadbalancer
    annotations:
      service.kubernetes.io/ibm-load-balancer-cloud-provider-ip-type: <public_or_private>
      service.kubernetes.io/ibm-load-balancer-cloud-provider-zone: "<zone>"
  spec:
    type: LoadBalancer
    selector:
      <selector_key>: <selector_value>
    ports:
     - name: http
       protocol: TCP
       port: 8080
       targetPort: 8080
     - name: https
       protocol: TCP
       port: 443
  ```
  {: codeblock}

  <table>
  <caption>Understanding the YAML file components</caption>
  <col width="25%">
  <thead>
  <th>Parameter</th>
  <th>Description</th>
  </thead>
  <tbody>
  <tr>
    <td>`service.kubernetes.io/ibm-load-balancer-cloud-provider-ip-type`</td>
    <td>Annotation to specify a service that accepts public or private requests. If you do not include this annotation, a public `LoadBalancer` is created.</td>
  </tr>
  <tr>
    <td>`service.kubernetes.io/ibm-load-balancer-cloud-provider-zone`</td>
    <td>Annotation to specify a VPC zone that your cluster is attached to. When you specify a zone in this annotation, two processes occur:<ul>
    <li>The VPC load balancer is deployed to the same subnet in that zone that your worker nodes are connected to.</li>
    <li>Only worker nodes in your cluster in this zone are configured to receive traffic from the VPC load balancer.</li><ul>
    To see zones, run `ibmcloud oc zone ls --provider vpc-gen2`.<p class="note">To place the load balancer in a specific zone, you must specify this annotation when you create the load balancer. If you later change this annotation to a different zone, the load balancer itself is not moved to the new zone. However, the load balancer is reconfigured to send traffic to only worker nodes in the new zone.</br></br>If you set the `dedicated: edge` label on worker nodes, then only edge nodes in the specified zone are configured to receive traffic. Edge nodes in other zones and non-edge nodes in the specified zone do not receive traffic from the load balancer.</p></td>
  </tr>
  <tr>
    <td>`selector`</td>
    <td>The label key (&lt;selector_key&gt;) and value (&lt;selector_value&gt;) that you used in the `spec.template.metadata.labels` section of your app deployment YAML. This custom label identifies all pods where your app runs to include them in the load balancing.</td>
  </tr>
  <tr>
    <td>`port`</td>
    <td>The port that the service listens on.</td>
  </tr>
  <tr>
    <td>`targetPort`</td>
    <td>The port to which the service directs traffic.</td>
  </tr>
  </tbody></table>

3. Create the Kubernetes `LoadBalancer` service in your cluster.
  ```
  oc apply -f myloadbalancer.yaml -n <namespace>
  ```
  {: pre}

4. Verify that the Kubernetes `LoadBalancer` service is created successfully in your cluster. When the service is created, the **LoadBalancer Ingress** field is populated with a hostname that is assigned by the VPC load balancer.

  **The VPC load balancer takes a few minutes to provision in your VPC.** You cannot access your app by using the hostname of your Kubernetes `LoadBalancer` service until the VPC load balancer is fully provisioned.
  {: note}
  ```
  oc describe svc myloadbalancer -n <namespace>
  ```
  {: pre}

  Example CLI output for a public `LoadBalancer` service:
  ```
  Name:                     myloadbalancer
  Namespace:                default
  Labels:                   <none>
  Annotations:              kubectl.kubernetes.io/last-applied-configuration:
                              {"apiVersion":"v1","kind":"Service","metadata":{"annotations":{"service.kubernetes.io/ibm-load-balancer-cloud-provider-ip-type":"public"},...
                            service.kubernetes.io/ibm-load-balancer-cloud-provider-ip-type: public
  Selector:                 run=webserver
  Type:                     LoadBalancer
  IP:                       172.21.106.166
  LoadBalancer Ingress:     1234abcd-us-south.lb.appdomain.cloud
  Port:                     <unset>  8080/TCP
  TargetPort:               8080/TCP
  NodePort:                 <unset>  30532/TCP
  Endpoints:
  Session Affinity:         None
  External Traffic Policy:  Cluster
  Events:
    Type    Reason                Age   From                Message
    ----    ------                ----  ----                -------
    Normal  EnsuringLoadBalancer  52s   service-controller  Ensuring load balancer
    Normal  EnsuredLoadBalancer   35s   service-controller  Ensured load balancer
  ```
  {: screen}

4. Verify that the VPC load balancer is created successfully in your VPC. In the output, verify that the VPC load balancer has an **Operating Status** of `online` and a **Provision Status** of `active`.

  The VPC load balancer name has a format `kube-<cluster_ID>-<kubernetes_lb_service_UID>`. To see your cluster ID, run `ibmcloud oc cluster get --cluster <cluster_name>`. To see the Kubernetes `LoadBalancer` service UID, run `oc get svc myloadbalancer -o yaml` and look for the **metadata.uid** field in the output. The dashes (-) are removed from the Kubernetes `LoadBalancer` service UID in the VPC load balancer name.
  {: tip}
  Do not rename any VPC load balancers that are created automatically for `LoadBalancer` services. If you rename a VPC load balancer, {{site.data.keyword.containerlong_notm}} automatically creates another VPC load balancer for the `LoadBalancer` service.
  {: important}
  ```
  ibmcloud is load-balancers
  ```
  {: pre}

  In the following example CLI output, the VPC load balancer that is named `kube-bh077ne10vqpekt0domg-046e0f754d624dca8b287a033d55f96e` is created for the Kubernetes `LoadBalancer` service:
  ```
  ID                                     Name                                                         Created          Host Name                                  Is Public   Listeners                               Operating Status   Pools                                   Private IPs              Provision Status   Public IPs                    Subnets                                Resource Group
  06496f64-a689-4693-ba23-320959b7b677   kube-bh077ne10vqpekt0domg-046e0f754d624dca8b287a033d55f96e   8 minutes ago    1234abcd-us-south.lb.appdomain.cloud       yes         95482dcf-6b9b-4c6a-be54-04d3c46cf017    online             717f2122-5431-403c-b21d-630a12fc3a5a    10.241.0.7,10.241.0.13   active             169.63.99.184,169.63.99.124   c6540331-1c1c-40f4-9c35-aa42a98fe0d9   00809211b934565df546a95f86160f62
  ```
  {: screen}

5. If you created a public `LoadBalancer` service, curl the hostname of the Kubernetes `LoadBalancer` service that is assigned by the VPC load balancer.
  Example:
  ```
  curl 06496f64-us-south.lb.appdomain.cloud:8080
  ```
  {: pre}

  Example output:
  ```
  Hello world from hello-world-deployment-5fd7787c79-sl9hn! Your app is up and running in a cluster!
  ```
  {: screen}

  If you created a private `LoadBalancer` service, you must be [connected to your private VPC network](/docs/vpc?topic=vpc-vpn-onprem-example) to curl the hostname.
  {: tip}

Do not delete the subnets that you attached to your cluster during cluster creation or when you add worker nodes in a zone. If you delete a VPC subnet that your cluster used, any load balancers that use IP addresses from the subnet might experience issues, and you might be unable to create new load balancers.
{: important}

<br />


## Registering a VPC load balancer hostname with a DNS subdomain
{: #vpc_lb_dns}

The VPC load balancer provides a default HTTP hostname in the format `1234abcd-<region>.lb.appdomain.cloud` through which you can access your app. However, if you want an SSL certificate for your app domain to support HTTPS, you can create an IBM-provided subdomain or bring your own custom domain. Note that in VPC clusters, you can create subdomains for both public and private VPC load balancers.
{: shortdesc}

After you create a DNS subdomain for a VPC load balancer hostname, you cannot use `nlb-dns health-monitor` commands to create a custom health check. Instead, the default VPC load balancer health check that is provided for the default VPC load balancer hostname is used. For more information, see the [VPC documentation](/docs/vpc?topic=vpc-load-balancers#health-checks).
{: note}

Before you begin:
* [Set up a VPC load balancer](#setup_vpc_ks_vpc_lb). Ensure that you define an HTTPS port in your Kubernetes `LoadBalancer` service that configures the VPC load balancer.
* To use the SSL certificate to access your app via HTTPS, your app must be able to terminate TLS connections.

1. Get the hostname for your VPC load balancer. In the output, look for the hostname in the **EXTERNAL-IP** column.
  ```
  oc get svc -o wide
  ```
  {: pre}

  Example output:
  ```
  NAME            TYPE           CLUSTER-IP       EXTERNAL-IP                            PORT(S)     AGE       SELECTOR
  ...
  webserver-lb    LoadBalancer   172.21.xxx.xxx   1234abcd-us-south.lb.appdomain.cloud   8080:30532/TCP     1d       run=webserver
  ```
  {: screen}

2. Create a DNS subdomain for the load balancer hostname.
  * **IBM-provided subdomain**: Use `nlb-dns` commands to generate a subdomain with an SSL certificate for the VPC load balancer hostname. {{site.data.keyword.cloud_notm}} takes care of generating and maintaining the wildcard SSL certificate for the subdomain for you.
    1. Create a DNS subdomain and SSL certificate.
        ```
        ibmcloud oc nlb-dns create vpc-gen2 --cluster <cluster_name_or_id> --lb-host <vpc_lb_hostname> --type (public|private)
        ```
        {: pre}

    2. Verify that the subdomain is created. For more information, see [Understanding the subdomain format](/docs/openshift?topic=openshift-loadbalancer_hostname#loadbalancer_hostname_format).
      ```
      ibmcloud oc nlb-dns ls --cluster <cluster_name_or_id>
      ```
      {: pre}

      Example output:
      ```
      Subdomain                                                                               Load Balancer Hostname                        Health Monitor   SSL Cert Status           SSL Cert Secret Name
      mycluster-a1b2cdef345678g9hi012j3kl4567890-0001.us-south.containers.appdomain.cloud     ["1234abcd-us-south.lb.appdomain.cloud"]      None             created                   <certificate>
      ```
      {: screen}

  * **Custom domain**: Provide your own custom domain and give it an alias by specifying the VPC load balancer hostname as a Canonical Name record (CNAME).
    1. Register a custom domain by working with your Domain Name Service (DNS) provider or [{{site.data.keyword.cloud_notm}} DNS](/docs/dns?topic=dns-getting-started).
    2. Define an alias for your custom domain by specifying the VPC load balancer hostname as a Canonical Name record (CNAME).

3. If you created a subdomain for a public VPC load balancer, open a web browser and enter the URL to access your app through the subdomain. If you created a subdomain for a private VPC load balancer, you must be [connected to your private VPC network](/docs/vpc?topic=vpc-vpn-onprem-example) to test access to your subdomain.

To use the SSL certificate to access your app via HTTPS, ensure that you defined an HTTPS port in your [Kubernetes `LoadBalancer` service](#setup_vpc_ks_vpc_lb). You can verify that requests are correctly routing through the HTTPS port by running `curl -v --insecure https://<domain>`. A connection error indicates that no HTTPS port is open on the service. Also, ensure that TLS connections can be terminated by your app. You can verify that your app terminates TLS properly by running `curl -v https://<domain>`. A certificate error indicates that your app is not properly terminating TLS connections.
{: tip}

<br />


## Limitations
{: #lbaas_limitations}

For more information about using load balancers for VPC, see the VPC docs for [public and private](/docs/vpc?topic=vpc-load-balancers#private-load-balancer) load balancers.
{: shortdesc}

* VPC load balancers do not currently support UDP.
* Private VPC load balancers do not accept all traffic, only RFC 1918 traffic.
* One VPC load balancer is created for each Kubernetes `LoadBalancer` service that you create, and it routes requests to that Kubernetes `LoadBalancer` service only. Across all of your VPC clusters in your VPC, a maximum of 20 VPC load balancers can be created.
* The VPC load balancer can route requests to pods that are deployed on a maximum of 50 worker nodes in a cluster. If your cluster has more than 50 worker nodes, create one load balancer per zone. In the YAML file for each load balancer, add the `service.kubernetes.io/ibm-load-balancer-cloud-provider-zone: "<zone>"` annotation. Each load balancer can forward requests to apps on the worker nodes in that zone only.
* When you define the configuration YAML file for a Kubernetes `LoadBalancer` service, the following annotations and settings are not supported:
    * `service.kubernetes.io/ibm-load-balancer-cloud-provider-vlan: "<vlan_id>"`
    * `service.kubernetes.io/ibm-load-balancer-cloud-provider-enable-features: "ipvs"`
    * `service.kubernetes.io/ibm-load-balancer-cloud-provider-ipvs-scheduler: "<algorithm>"`
    * `spec.loadBalancerIP`
    * `spec.loadBalancerSourceRanges`
    * The `externalTrafficPolicy: Local` setting is supported, but the setting does not preserve the source IP of the request.
* When you delete a VPC cluster, any VPC load balancers that were automatically created by Red Hat OpenShift on IBM Cloud for the Kubernetes `LoadBalancer` services in that cluster are also automatically deleted. However, any VPC load balancers that you manually created in your VPC are not deleted.
* You can register up to 128 subdomains for VPC load balancer hostnames. This limit can be lifted on request by opening a [support case](/docs/get-support?topic=get-support-getting-customer-support).




