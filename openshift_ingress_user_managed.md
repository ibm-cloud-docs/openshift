---

copyright:
  years: 2014, 2019
lastupdated: "2019-10-30"

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

The IBM-provided Ingress application load balancers (ALBs) are based on NGINX controllers that you can configure by using [custom {{site.data.keyword.cloud_notm}} annotations](/docs/containers?topic=containers-ingress_annotation). Depending on what your app requires, you might want to configure your own custom Ingress controller. When you bring your own Ingress controller instead of using the IBM-provided Ingress ALB, you are responsible for supplying the controller image, maintaining the controller, updating the controller, and any security-related updates to keep your Ingress controller free from vulnerabilities. **Note**: Bringing your own Ingress controller is supported only for providing public external access to your apps and is not supported for providing private external access.

## Expose your Ingress controller by creating an NLB and a hostname
{: #user_managed_nlb}

Create a network load balancer (NLB) to expose your custom Ingress controller deployment, and then create a hostname for the NLB IP address.
{: shortdesc}

1. Get the configuration file for your Ingress controller ready. For example, you can use the [cloud-generic NGINX community Ingress controller ![External link icon](../icons/launch-glyph.svg "External link icon")](https://github.com/kubernetes/ingress-nginx/tree/master/deploy/cloud-generic). If you use the community controller, edit the `kustomization.yaml` file by following these steps.
  1. Replace the `namespace: ingress-nginx` with `namespace: kube-system`.
  2. In the `commonLabels` section, replace the `app.kubernetes.io/name: ingress-nginx` and `app.kubernetes.io/part-of: ingress-nginx` labels with one `app: ingress-nginx` label.

2. Deploy your own Ingress controller. For example, to use the cloud-generic NGINX community Ingress controller, run the following command.
    ```
    oc apply --kustomize . -n kube-system
    ```
    {: pre}

3. Define a load balancer to expose your custom Ingress deployment.
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
  https://<load_blanacer_host_name>/<app_path>
  ```
  {: codeblock}





