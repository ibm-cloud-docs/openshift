---

copyright:
  years: 2014, 2020
lastupdated: "2020-03-06"

keywords: openshift, roks, rhoks, rhos, nginx, iks multiple ingress controllers, byo controller

subcollection: openshift

---

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


# Bringing your own Ingress controller
{: #ingress-user_managed}

Bring your own Ingress controller to run on {{site.data.keyword.cloud_notm}} and leverage an IBM-provided hostname and TLS certificate.
{: shortdesc}

<img src="images/icon-version-311.png" alt="Version 3.11 icon" width="30" style="width:30px; border-style: none"/> This information is applicable for clusters that run OpenShift version 3.11 only. To learn about Ingress for OpenShift version 4.3 or later, see [About Ingress in OpenShift version 4.3 or later](/openshift?topic=openshift-ingress-about-roks4).
{: important}

In Red Hat OpenShift on IBM Cloud, IBM-provided application load balancers (ALBs) are based on a custom implementation of the NGINX Ingress controller. However, depending on what your app requires, you might want to configure your own custom Ingress controller instead of using the IBM-provided ALBs. For example, you might want to use the Istio `ingressgateway` load balancer service to control traffic for your cluster. When you bring your own Ingress controller, you are responsible for supplying the controller image, maintaining the controller, updating the controller, and any security-related updates to keep your Ingress controller free from vulnerabilities.

## Exposing your Ingress controller by creating an NLB and a hostname
{: #user_managed_nlb}

Create a network load balancer (NLB) to expose your custom Ingress controller deployment, and then create a hostname for the NLB IP address.
{: shortdesc}

In classic clusters, bringing your own Ingress controller is supported only for providing public external access to your apps and is not supported for providing private external access.
{: note}

1. Get the configuration file for your Ingress controller ready. For example, you can use the [cloud-generic NGINX community Ingress controller](https://raw.githubusercontent.com/kubernetes/ingress-nginx/nginx-0.30.0/deploy/static/mandatory.yaml){: external}. If you use the community controller, edit the `mandatory.yaml` file by following these steps.
  1. Replace all instances of `namespace: ingress-nginx` with `namespace: kube-system`.
  2. Replace all instances of the `app.kubernetes.io/name: ingress-nginx` and `app.kubernetes.io/part-of: ingress-nginx` labels with one `app: ingress-nginx` label.

2. Deploy your own Ingress controller. For example, to use the cloud-generic NGINX community Ingress controller, run the following command.
    ```
    oc apply -f mandatory.yaml -n kube-system
    ```
    {: pre}

3. Define a load balancer service to expose your custom Ingress deployment.
    ```yaml
    apiVersion: v1
    kind: Service
    metadata:
      name: ingress-nginx
    spec:
      type: LoadBalancer
      selector:
        app: ingress-nginx
      ports:
       - protocol: TCP
         port: 80
      externalTrafficPolicy: Cluster
    ```
    {: codeblock}

4. Create the service in your cluster.
  ```
  oc apply -f ingress-nginx.yaml -n kube-system
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

6. Register the load balancer IP address by creating a new DNS hostname or by using the existing Ingress subdomain for your cluster. If you plan to continue to use IBM-provided ALBs concurrently with your custom Ingress controller in one cluster, you must create a new DNS hostname.
  * Create a new DNS hostname:
      1. Register the NLB IP address with a DNS hostname.
        ```
        ibmcloud oc nlb-dns create classic --cluster <cluster_name_or_id> --ip <LB_IP>
        ```
        {: pre}
      2. Verify that the hostname is created.
        ```
        ibmcloud oc nlb-dns ls --cluster <cluster_name_or_id>
        ```
        {: pre}

        Example output:
        ```
        Hostname                                                                                IP(s)              Health Monitor   SSL Cert Status           SSL Cert Secret Name
        mycluster-a1b2cdef345678g9hi012j3kl4567890-0000.us-south.containers.appdomain.cloud     ["168.1.1.1"]      None             created                   <certificate>
        ```
        {: screen}
      3. Optional: [Enable health checks on the hostname by creating a health monitor](/docs/openshift?topic=openshift-loadbalancer_hostname#loadbalancer_hostname_monitor).
  * Use the existing Ingress subdomain for your cluster:
      1. Get the Ingress subdomain for your cluster.
        ```
        ibmcloud oc cluster get -c <cluster> | grep Ingress
        ```
        {: pre}

      2. Get the existing ALB IP addresses that are registered by default with the Ingress subdomain. In the output, look for the **IP(s)** that are registered for the Ingress subdomain for your cluster.
        ```
        ibmcloud oc nlb-dns ls -c <cluster>
        ```
        {: pre}

        Example output:
        ```
        Hostname                                                                               IP(s)                       Health Monitor   SSL Cert Status   SSL Cert Secret Name                               Secret Namespace
        mycluster-35366fb2d3d90fd50548180f69e7d12a-0000.us-south.containers.appdomain.cloud    169.XX.XX.X,169.XX.XXX.XX   enabled          created           mycluster                                          default
        ```
        {: screen}

      3. Remove the ALB IP addresses from the subdomain. If you have a multizone cluster, run this command for each ALB IP address.
        ```
        ibmcloud oc nlb-dns rm classic --cluster <cluster> --ip <ALB_IP> --nlb-host <Ingress_subdomain>
        ```
        {: pre}

      4. Add the IP address for your load balancer to the subdomain.
        ```
        ibmcloud oc nlb-dns add classic --cluster <cluster> --ip <load_balancer_IP> --nlb-host <Ingress_subdomain>
        ```
        {: pre}

      5. Verify that your load balancer is now registered with the Ingress subdomain.
        ```
        ibmcloud oc nlb-dns ls -c <cluster>
        ```
        {: pre}
7. Deploy any other resources that are required by your custom Ingress controller, such as the configmap. If you used the cloud-generic NGINX community Ingress controller in step 1, you can skip this step because the resources are already included in the `mandatory.yaml.` file.

8. Create Ingress resources for your apps. You can use the Kubernetes documentation to create [an Ingress resource file](https://kubernetes.io/docs/concepts/services-networking/ingress/){: external} and use [annotations](https://kubernetes.github.io/ingress-nginx/user-guide/nginx-configuration/annotations/){: external}.
  <p class="tip">If you continue to use IBM-provided ALBs concurrently with your custom Ingress controller in one cluster, you can create separate Ingress resources for your ALBs and custom controller. In the [Ingress resource that you create to apply to the IBM ALBs only](/docs/openshift?topic=openshift-ingress#ingress_expose_public), add the annotation <code>kubernetes.io/ingress.class: "iks-nginx"</code>.</p>

9. Access your app by using the subdomain you configured in step 6 and the path that your app listens on that you specified in the Ingress resource file.
  ```
  https://<host_name>/<app_path>
  ```
  {: codeblock}



