---

copyright:
  years: 2014, 2019
lastupdated: "2019-11-19"

keywords: openshift, roks, rhoks, rhos, nginx, iks multiple ingress controllers, byo controller

subcollection: openshift

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:download: .download}
{:preview: .preview}

# Bringing your own Ingress controller
{: #ingress-user_managed}

Bring your own Ingress controller to run on {{site.data.keyword.cloud_notm}} and leverage an IBM-provided hostname and TLS certificate.
{: shortdesc}

The IBM-provided Ingress application load balancers (ALBs) are based on NGINX controllers that you can configure by using [custom {{site.data.keyword.cloud_notm}} annotations](/docs/openshift?topic=openshift-ingress_annotation). Depending on what your app requires, you might want to configure your own custom Ingress controller. When you bring your own Ingress controller instead of using the IBM-provided Ingress ALB, you are responsible for supplying the controller image, maintaining the controller, updating the controller, and any security-related updates to keep your Ingress controller free from vulnerabilities.

## Classic clusters: Exposing your Ingress controller by creating an NLB and a hostname
{: #user_managed_nlb}

Create a network load balancer (NLB) to expose your custom Ingress controller deployment, and then create a hostname for the NLB IP address.
{: shortdesc}

In classic clusters, bringing your own Ingress controller is supported only for providing public external access to your apps and is not supported for providing private external access.
{: note}

1. Get the configuration file for your Ingress controller ready. For example, you can use the [cloud-generic NGINX community Ingress controller ![External link icon](../icons/launch-glyph.svg "External link icon")](https://github.com/kubernetes/ingress-nginx/tree/master/deploy/cloud-generic). If you use the community controller, edit the `kustomization.yaml` file by following these steps.
  1. Replace the `namespace: ingress-nginx` with `namespace: kube-system`.
  2. In the `commonLabels` section, replace the `app.kubernetes.io/name: ingress-nginx` and `app.kubernetes.io/part-of: ingress-nginx` labels with one `app: ingress-nginx` label.

2. Deploy your own Ingress controller. For example, to use the cloud-generic NGINX community Ingress controller, run the following command.
    ```
    oc apply --kustomize . -n kube-system
    ```
    {: pre}

3. Define a load balancer service to expose your custom Ingress deployment.
    ```
    apiVersion: v1
    kind: Service
    metadata:
      name: my-lb-svc
    spec:
      type: LoadBalancer
      selector:
        app: ingress-nginx
      ports:
       - protocol: TCP
         port: 8080
      externalTrafficPolicy: Local
    ```
    {: codeblock}

4. Create the service in your cluster.
    ```
    oc apply -f my-lb-svc.yaml
    ```
    {: pre}

5. Get the **EXTERNAL-IP** address for the load balancer.
    ```
    oc get svc my-lb-svc -n kube-system
    ```
    {: pre}

    In the following example output, the **EXTERNAL-IP** is `168.1.1.1`.
    ```
    NAME         TYPE           CLUSTER-IP       EXTERNAL-IP      PORT(S)            AGE
    my-lb-svc    LoadBalancer   172.21.xxx.xxx   168.1.1.1        80:30104/TCP       2m
    ```
    {: screen}

6. Register the load balancer IP address by creating a DNS hostname.
    ```
    ibmcloud oc nlb-dns create classic --cluster <cluster_name_or_id> --ip <LB_IP>
    ```
    {: pre}

7. Verify that the hostname is created.
  ```
  ibmcloud oc nlb-dns ls --cluster <cluster_name_or_id>
  ```
  {: pre}

  Example output:
  ```
  Hostname                                                                                IP(s)              Health Monitor   SSL Cert Status           SSL Cert Secret Name
  mycluster-a1b2cdef345678g9hi012j3kl4567890-0001.us-south.containers.appdomain.cloud     ["168.1.1.1"]      None             created                   <certificate>
  ```
  {: screen}

8. Optional: [Enable health checks on the hostname by creating a health monitor](/docs/openshift?topic=openshift-loadbalancer_hostname#loadbalancer_hostname_monitor).

9. Deploy any other resources that are required by your custom Ingress controller, such as the configmap.

10. Create Ingress resources for your apps. You can use the Kubernetes documentation to create [an Ingress resource file ![External link icon](../icons/launch-glyph.svg "External link icon")](https://kubernetes.io/docs/concepts/services-networking/ingress/) and use [annotations ![External link icon](../icons/launch-glyph.svg "External link icon")](https://kubernetes.github.io/ingress-nginx/user-guide/nginx-configuration/annotations/).
  <p class="tip">If you continue to use IBM-provided ALBs concurrently with your custom Ingress controller in one cluster, you can create separate Ingress resources for your ALBs and custom controller. In the [Ingress resource that you create to apply to the IBM ALBs only](/docs/openshift?topic=openshift-ingress#ingress_expose_public), add the annotation <code>kubernetes.io/ingress.class: "iks-nginx"</code>.</p>

11. Access your app by using the load balancer hostname that you found in step 7 and the path that your app listens on that you specified in the Ingress resource file.
  ```
  https://<load_balancer_host_name>/<app_path>
  ```
  {: codeblock}

## VPC clusters: Exposing your Ingress controller by creating a VPC load balancer and subdomain
{: #user_managed_vpc}

Expose your custom Ingress controller deployment to the public or to the private network by setting up a Kubernetes `LoadBalancer` service in your cluster. A VPC load balancer which routes requests to your app is automatically created for you in your VPC outside of your cluster.
{: shortdesc}

1. Get the configuration file for your Ingress controller ready. For example, you can use the [cloud-generic NGINX community Ingress controller ![External link icon](../icons/launch-glyph.svg "External link icon")](https://github.com/kubernetes/ingress-nginx/tree/master/deploy/cloud-generic). If you use the community controller, edit the `kustomization.yaml` file by following these steps.
  1. Replace the `namespace: ingress-nginx` with `namespace: kube-system`.
  2. In the `commonLabels` section, replace the `app.kubernetes.io/name: ingress-nginx` and `app.kubernetes.io/part-of: ingress-nginx` labels with one `app: ingress-nginx` label.

2. Deploy your own Ingress controller. For example, to use the cloud-generic NGINX community Ingress controller, run the following command.
    ```
    oc apply --kustomize . -n kube-system
    ```
    {: pre}

3. Define a Kubernetes `LoadBalancer` service to expose your custom Ingress deployment.
    ```
    apiVersion: v1
    kind: Service
    metadata:
      name: my-lb-svc
      annotations:
        service.kubernetes.io/ibm-load-balancer-cloud-provider-ip-type: <public_or_private>
    spec:
      type: LoadBalancer
      selector:
        app: ingress-nginx
      ports:
       - protocol: TCP
         port: 8080
    ```
    {: codeblock}

4. Create the Kubernetes `LoadBalancer` service in your cluster.
    ```
    oc apply -f my-lb-svc.yaml
    ```
    {: pre}

5. Verify that the Kubernetes `LoadBalancer` service is created successfully in your cluster. When the service is created, copy the hostname that is assigned by the VPC load balancer in the **LoadBalancer Ingress** field.

  **The VPC load balancer takes a few minutes to provision in your VPC.** You cannot access the hostname of your Kubernetes `LoadBalancer` service until the VPC load balancer is fully provisioned.
  {: note}
  ```
  oc describe svc myloadbalancer
  ```
  {: pre}

  In the following example output, the **LoadBalancer Ingress** hostname is `1234abcd-us-south.lb.appdomain.cloud`:
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

6. Create a DNS entry for the VPC load balancer hostname by creating a subdomain with an SSL certificate.
  ```
  ibmcloud oc nlb-dns create vpc-classic --cluster <cluster_name_or_id> --lb-host <vpc_lb_hostname> --type (public|private)
  ```
  {: pre}

7. Verify that the subdomain is created.
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

8. Deploy any other resources that are required by your custom Ingress controller, such as the configmap.

9. Create Ingress resources for your apps. You can use the Kubernetes documentation to create [an Ingress resource file ![External link icon](../icons/launch-glyph.svg "External link icon")](https://kubernetes.io/docs/concepts/services-networking/ingress/) and use [annotations ![External link icon](../icons/launch-glyph.svg "External link icon")](https://kubernetes.github.io/ingress-nginx/user-guide/nginx-configuration/annotations/).
  <p class="tip">If you continue to use IBM-provided ALBs concurrently with your custom Ingress controller in one cluster, you can create separate Ingress resources for your IBM ALBs and custom controller. In the [Ingress resource that you create to apply to the IBM ALBs only](/docs/openshift?topic=openshift-ingress#ingress_expose_public), add the annotation <code>kubernetes.io/ingress.class: "iks-nginx"</code>.</p>

10. Access your app by using the subdomain that you created in step 7 and the path that your app listens on that you specified in the Ingress resource file. If you created a subdomain for a private VPC load balancer, you must be [connected to your private VPC network](/docs/vpc-on-classic-network?topic=vpc-on-classic-network---using-vpn-with-your-vpc) to test access to your subdomain.
  ```
  https://<load_balancer_subdomain>/<app_path>
  ```
  {: codeblock}





