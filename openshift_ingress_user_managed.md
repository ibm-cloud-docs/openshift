---

copyright:
  years: 2014, 2021
lastupdated: "2021-01-04"

keywords: openshift, roks, rhoks, rhos, nginx, iks multiple ingress controllers, byo controller

subcollection: openshift

---

{:DomainName: data-hd-keyref="APPDomain"}
{:DomainName: data-hd-keyref="DomainName"}
{:android: data-hd-operatingsystem="android"}
{:api: .ph data-hd-interface='api'}
{:apikey: data-credential-placeholder='apikey'}
{:app_key: data-hd-keyref="app_key"}
{:app_name: data-hd-keyref="app_name"}
{:app_secret: data-hd-keyref="app_secret"}
{:app_url: data-hd-keyref="app_url"}
{:authenticated-content: .authenticated-content}
{:beta: .beta}
{:c#: data-hd-programlang="c#"}
{:cli: .ph data-hd-interface='cli'}
{:codeblock: .codeblock}
{:curl: .ph data-hd-programlang='curl'}
{:deprecated: .deprecated}
{:dotnet-standard: .ph data-hd-programlang='dotnet-standard'}
{:download: .download}
{:external: target="_blank" .external}
{:faq: data-hd-content-type='faq'}
{:fuzzybunny: .ph data-hd-programlang='fuzzybunny'}
{:generic: data-hd-operatingsystem="generic"}
{:generic: data-hd-programlang="generic"}
{:gif: data-image-type='gif'}
{:go: .ph data-hd-programlang='go'}
{:help: data-hd-content-type='help'}
{:hide-dashboard: .hide-dashboard}
{:hide-in-docs: .hide-in-docs}
{:important: .important}
{:ios: data-hd-operatingsystem="ios"}
{:java: .ph data-hd-programlang='java'}
{:java: data-hd-programlang="java"}
{:javascript: .ph data-hd-programlang='javascript'}
{:javascript: data-hd-programlang="javascript"}
{:new_window: target="_blank"}
{:note .note}
{:note: .note}
{:objectc data-hd-programlang="objectc"}
{:org_name: data-hd-keyref="org_name"}
{:php: data-hd-programlang="php"}
{:pre: .pre}
{:preview: .preview}
{:python: .ph data-hd-programlang='python'}
{:python: data-hd-programlang="python"}
{:route: data-hd-keyref="route"}
{:row-headers: .row-headers}
{:ruby: .ph data-hd-programlang='ruby'}
{:ruby: data-hd-programlang="ruby"}
{:runtime: architecture="runtime"}
{:runtimeIcon: .runtimeIcon}
{:runtimeIconList: .runtimeIconList}
{:runtimeLink: .runtimeLink}
{:runtimeTitle: .runtimeTitle}
{:screen: .screen}
{:script: data-hd-video='script'}
{:service: architecture="service"}
{:service_instance_name: data-hd-keyref="service_instance_name"}
{:service_name: data-hd-keyref="service_name"}
{:shortdesc: .shortdesc}
{:space_name: data-hd-keyref="space_name"}
{:step: data-tutorial-type='step'}
{:subsection: outputclass="subsection"}
{:support: data-reuse='support'}
{:swift: .ph data-hd-programlang='swift'}
{:swift: data-hd-programlang="swift"}
{:table: .aria-labeledby="caption"}
{:term: .term}
{:tip: .tip}
{:tooling-url: data-tooling-url-placeholder='tooling-url'}
{:troubleshoot: data-hd-content-type='troubleshoot'}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:tsSymptoms: .tsSymptoms}
{:tutorial: data-hd-content-type='tutorial'}
{:ui: .ph data-hd-interface='ui'}
{:unity: .ph data-hd-programlang='unity'}
{:url: data-credential-placeholder='url'}
{:user_ID: data-hd-keyref="user_ID"}
{:vbnet: .ph data-hd-programlang='vb.net'}
{:video: .video}



# Bringing your own Ingress controller
{: #ingress-user_managed}

Bring your own Ingress controller to run on {{site.data.keyword.cloud_notm}} and leverage an IBM-provided hostname and TLS certificate.
{: shortdesc}

<img src="images/icon-version-311.png" alt="Version 3.11 icon" width="30" style="width:30px; border-style: none"/> This information is applicable for clusters that run {{site.data.keyword.openshiftshort}} version 3.11 only. To learn about Ingress for {{site.data.keyword.openshiftshort}} version 4, see [About Ingress in {{site.data.keyword.openshiftshort}} version 4](/docs/openshift?topic=openshift-ingress-about-roks4).
{: important}

In {{site.data.keyword.openshiftlong_notm}}, application load balancers (ALBs) are created for you by default. However, depending on what your app requires, you might want to configure your own custom Ingress controller instead of using the IBM-provided ALBs. For example, you might want to use the Istio `ingressgateway` load balancer service to control traffic for your cluster. When you bring your own Ingress controller, you are responsible for supplying the controller image, maintaining the controller, updating the controller, and any security-related updates to keep your Ingress controller free from vulnerabilities.

If you choose to bring your own Ingress controller, IBM does not provide support for your Ingress deployment. You are responsible for configuring, updating, and managing your Ingress system. The following sections help you get started, but you are responsible for any changes that you must make to the steps.
{: important}

## Exposing your Ingress controller by creating an NLB and a hostname
{: #user_managed_nlb}

<img src="images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Create a network load balancer (NLB) to expose your custom Ingress controller deployment, and then create a hostname for the NLB IP address.
{: shortdesc}

In classic clusters, bringing your own Ingress controller is supported only for providing public external access to your apps and is not supported for providing private external access.
{: note}

1. Get the configuration file for your Ingress controller ready. For example, you can use the [cloud-generic NGINX community Ingress controller](https://github.com/kubernetes/ingress-nginx/blob/master/deploy/static/provider/cloud/deploy.yaml){: external}. If you use the community controller, edit the `deploy.yaml` file by following these steps.
  1. Replace all instances of `namespace: ingress-nginx` with `namespace: kube-system`.
  2. Replace all instances of the `app.kubernetes.io/name: ingress-nginx` and `app.kubernetes.io/instance: ingress-nginx` labels with one `app: ingress-nginx` label.

2. Deploy your own Ingress controller. For example, to use the cloud-generic NGINX community Ingress controller, run the following command.
    ```
    oc apply -f deploy.yaml -n kube-system
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
       - name: http
         protocol: TCP
         port: 80
       - name: https
         protocol: TCP
         port: 443
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
    oc get svc ingress-nginx -n kube-system
    ```
    {: pre}

    In the following example output, the **EXTERNAL-IP** is `168.1.1.1`.
    ```
    NAME             TYPE           CLUSTER-IP       EXTERNAL-IP      PORT(S)            AGE
    ingress-nginx    LoadBalancer   172.21.xxx.xxx   168.1.1.1        80:30104/TCP       2m
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
        ibmcloud oc nlb-dns add --cluster <cluster> --ip <load_balancer_IP> --nlb-host <Ingress_subdomain>
        ```
        {: pre}

      5. If you do not plan to continue to use IBM-provided ALBs concurrently with your custom Ingress controller:
          1. Get the ID of the ALBs.
            ```
            ibmcloud oc ingress alb ls --cluster <cluster-name>
            ```
            {: pre}

          2. Disable each ALB.
            ```
            ibmcloud oc ingress alb disable --alb <ALB_ID> -c <cluster_name_or_ID>
            ```
            {: pre}

      6. Verify that your load balancer is now registered with the Ingress subdomain.
        ```
        ibmcloud oc nlb-dns ls -c <cluster>
        ```
        {: pre}
7. Deploy any other resources that are required by your custom Ingress controller, such as the configmap. If you used the cloud-generic NGINX community Ingress controller in step 1, you can skip this step because the resources are already included in the `deploy.yaml` file.

8. Create Ingress resources for your apps. You can use the Kubernetes documentation to create [an Ingress resource file](https://kubernetes.io/docs/concepts/services-networking/ingress/){: external} and use [annotations](https://kubernetes.github.io/ingress-nginx/user-guide/nginx-configuration/annotations/){: external}.
  <p class="important">If you continue to use IBM-provided ALBs concurrently with your custom Ingress controller in one cluster, create separate Ingress resources for your ALBs and custom controller. In the [Ingress resource that you create to apply to the IBM ALBs only](/docs/openshift?topic=openshift-ingress#ingress_expose_public), you must add the annotation <code>kubernetes.io/ingress.class: "iks-nginx"</code>.</p>

9. Access your app by using the subdomain you configured in step 6 and the path that your app listens on that you specified in the Ingress resource file.
  ```
  https://<host_name>/<app_path>
  ```
  {: codeblock}


