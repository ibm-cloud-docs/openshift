---

copyright:
  years: 2014, 2021
lastupdated: "2021-05-24"

keywords: openshift, roks, rhoks, rhos

subcollection: openshift
content-type: troubleshoot

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
{:terraform: .ph data-hd-interface='terraform'}
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
  

# Why does no Ingress subdomain exist after cluster creation?
{: #ingress_subdomain}

**Infrastructure provider**:
  * <img src="../images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Classic
  * <img src="../images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> VPC

{: tsSymptoms}
You create a cluster and run `ibmcloud oc cluster get --cluster <cluster>` to check its status. The cluster **State** is `normal`, but the **Ingress Subdomain** and **Ingress Secret** are not available.

{: tsCauses}
Even if the cluster is in a `normal` state, the Ingress subdomain and secret might still be in progress. The Ingress subdomain and secret creation follows a process that might take more than 15 minutes to complete:

<img src="../images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> **Classic clusters**:

1. When worker nodes are fully deployed and ready on the VLANs, a portable public and a portable private subnet for the VLANs are ordered.
2. After the portable subnet orders are successfully fulfilled, the `ibm-cloud-provider-vlan-ip-config` config map is updated with the portable public and portable private IP addresses.
3. When the `ibm-cloud-provider-vlan-ip-config` config map is updated, the public ALB (version 3.11 clusters) or router for the Ingress controller (version 4 clusters) is triggered for creation.
4. A load balancer service that exposes the ALB or router is created and assigned an IP address.
5. The load balancer IP address is used to register the Ingress subdomain in Cloudflare. Cloudflare might have latency during the registration process.

If you create a classic cluster that is connected to private VLANs only, or if you create a free cluster, no Ingress subdomain or secret are created.
{: note}

<img src="../images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> **VPC clusters** (version 4 only):

1. When you create a VPC cluster, one public and one private VPC load balancer are automatically created outside of your cluster in your VPC.
2. One public router per zone is triggered for creation.
3. A load balancer service that exposes the router is created and assigned a hostname.
4. The load balancer hostname is used to register the Ingress subdomain in Cloudflare. Cloudflare might have latency during the registration process.

Creating a cluster after deleting a cluster the same or similar name? See [No Ingress subdomain exists after you create clusters of the same or similar name](/docs/openshift?topic=openshift-cs_rate_limit) instead.
{: tip}

{: tsResolve}
Typically, after the cluster is ready, the Ingress subdomain and secret are created after 15 minutes. If the Ingress subdomain and secret are still unavailable after your cluster is in a `normal` state for more than 15 minutes, you can check the progress of the creation process by following these steps:

1.  [Log in to your cluster](/docs/openshift?topic=openshift-access_cluster). Because the subdomain is not available, the {{site.data.keyword.openshiftshort}} console cannot open. Instead, you can set the cluster context with the `--admin` flag through the CLI.
    ```
    ibmcloud oc cluster config -c <cluster_name_or_ID> --admin
    ```
    {: pre}
2. Verify that the worker nodes have a **State** of `normal` and a **Status** of `Ready`. After you create the cluster, it can take up to 20 minutes for the worker nodes to be ready.
   ```
   ibmcloud oc worker ls -c <cluster_name_or_ID>
   ```
   {: pre}

   Example output:
   ```
   ID                                                     Public IP         Private IP      Flavor              State     Status   Zone    Version
   kube-blrs3b1d0p0p2f7haq0g-mycluster-default-000001f7   169.xx.xxx.xxx    10.xxx.xx.xxx   u3c.2x4.encrypted   deployed   Ready    dal10   1.20.7
   ```
   {: screen}

3. Verify that the prerequisite steps for your ALB creation are completed.
  * <img src="../images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> **Classic clusters**: Get the details of the `ibm-cloud-provider-vlan-ip-config` config map.
    ```
    oc describe cm ibm-cloud-provider-vlan-ip-config -n kube-system
    ```
    {: pre}
    * If the config map shows IP addresses, continue to the next step.
    * If the **Events** section shows a warning message similar to `ErrorSubnetLimitReached: There are already the maximum number of subnets permitted in this VLAN`, see the [VLAN capacity troubleshooting topic](/docs/openshift?topic=openshift-cs_subnet_limit).

    Example output of a config map populated with IP addresses:
    ```
    Name:         ibm-cloud-provider-vlan-ip-config
    Namespace:    kube-system
    Labels:       <none>
    Annotations:  <none>

    Data
    ====
    reserved_public_vlan_id:
    ----

    vlanipmap.json:
    ----
    {
      "vlans": [
        {
          "id": "2234947",
          "subnets": [
            {
              "id": "2215454",
              "ips": [
                "10.XXX.XXX.XXX",
                "10.XXX.XXX.XXX",
                "10.XXX.XXX.XXX",
                "10.XXX.XXX.XXX",
                "10.XXX.XXX.XXX"
              ],
              "is_public": false,
              "is_byoip": false,
              "cidr": "10.XXX.XXX.X/29"
            }
          ],
          "zone": "dal10",
          "region": "us-south"
        },
        {
          "id": "2234945",
          "subnets": [
            {
              "id": "2219170",
              "ips": [
                "169.XX.XXX.XX",
                "169.XX.XXX.XX",
                "169.XX.XXX.XX",
                "169.XX.XXX.XX",
                "169.XX.XXX.XX"
              ],
              "is_public": true,
              "is_byoip": false,
              "cidr": "169.XX.XXX.X/29"
            }
          ],
          "zone": "dal10",
          "region": "us-south"
        }
      ],
      "vlan_errors": [],
      "reserved_ips": []
    }
    cluster_id:
    ----
    bmnj1b1d09lpvv3oof0g
    reserved_private_ip:
    ----

    reserved_private_vlan_id:
    ----

    reserved_public_ip:
    ----

    Events:  <none>
    ```
    {: screen}
  * <img src="../images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> **VPC clusters** (version 4 only): Verify that the VPC load balancer for your routers exists. In the output, look for the VPC load balancer **Name** that starts with `kube-<cluster_ID>`. If you did not install the `infrastructure-service` plug-in, install it by running `ibmcloud plugin install infrastructure-service`.
    ```
    ibmcloud is load-balancers
    ```
    {: pre}
    <p class="note">Even though the VPC load balancer is listed, its DNS entry might still be registering. When a VPC load balancer is created, the hostname is registered through a public DNS. In some cases, it can take several minutes for this DNS entry to be replicated to the specific DNS that your client is using.</p>

4. Verify that the router for the Ingress controller (version 4 clusters) or ALB (version 3.11 clusters) is successfully created.
  * **Version 4:**
    1. Check whether a router deployment exists for your cluster.
      * If a router deployment is listed, continue to the next step.
      * If no router deployment is created after several minutes, [review ways to get help](/docs/openshift?topic=openshift-get-help).

        ```
        oc get deployment -n openshift-ingress
        ```
        {: pre}

        Example output:
        ```
        NAME             READY   UP-TO-DATE   AVAILABLE   AGE
        router-default   2/2     2            2           26m
        ```
        {: screen}

    2. Check whether the router's load balancer service exists and is assigned a public external IP address (classic clusters) or a hostname (VPC clusters).
      * If a service that is named `router-default` is listed and is assigned an IP address (classic clusters) or a hostname (VPC clusters), continue to the next step.
      * If no `router-default` service is created after several minutes, [review ways to get help](/docs/openshift?topic=openshift-get-help).

        ```
        oc get svc -n openshift-ingress
        ```
        {: pre}

        Example output:
        ```
        NAME                      TYPE           CLUSTER-IP      EXTERNAL-IP    PORT(S)                      AGE
        router-default            LoadBalancer   172.21.47.119   169.XX.XX.XX   80:31182/TCP,443:31154/TCP   27m
        router-internal-default   ClusterIP      172.21.51.30    <none>         80/TCP,443/TCP,1936/TCP      26m
        ```
        {: screen}
  * **Version 3.11:**
    1. Check whether an ALB exists for your cluster and that the ALB has a public IP address assigned.
      * If a public ALB is listed and is assigned an IP address, continue to the next step.
      * If no ALBs are created after several minutes, [review ways to get help](/docs/openshift?topic=openshift-get-help).

        ```
        ibmcloud oc ingress alb ls -c <cluster_name_or_ID>
        ```
        {: pre}

        Example output:
        ```
        ALB ID                                Enabled   Status     Type      ALB IP          Zone    Build                          ALB VLAN ID   NLB Version
        private-crbmnj1b1d09lpvv3oof0g-alb1   false     disabled   private   -               dal10   ingress:2477/ingress-auth:992   2234947       2.0
        public-crbmnj1b1d09lpvv3oof0g-alb1    true      enabled    public    169.XX.XXX.XX   dal10   ingress:2477/ingress-auth:992   2234945       2.0
        ```
        {: screen}

    2. Check whether the `LoadBalancer` service that exposes the ALB exists and is assigned the same IP address as the public ALB.
      * If a `LoadBalancer` service is listed and is assigned an IP address, continue to the next step.
      * If no `LoadBalancer` services are created after several minutes, [review ways to get help](/docs/openshift?topic=openshift-get-help).

        ```
        kubectl get svc -n kube-system | grep LoadBalancer
        ```
        {: pre}

        Example output:
        ```
        public-crbmnj1b1d09lpvv3oof0g-alb1   LoadBalancer   172.21.XXX.XXX   169.XX.XXX.XX   80:30723/TCP,443:31241/TCP   1d
        ```
        {: screen}

5. Check again whether the Ingress subdomain and secret are created. If they are not available, but you verified that all of the components in steps 1 - 3 exist, [review ways to get help](/docs/openshift?topic=openshift-get-help).
  ```
  ibmcloud oc cluster get -c <cluster_name_or_ID>
  ```
  {: pre}
