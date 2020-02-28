---

copyright:
  years: 2014, 2020
lastupdated: "2020-02-27"

keywords: openshift, roks, rhoks, rhos

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


# Ingress
{: #cs_troubleshoot_debug_ingress}

As you use {{site.data.keyword.openshiftlong}}, consider these techniques for general Ingress troubleshooting and debugging.
{: shortdesc}

<img src="images/icon-version-311.png" alt="Version 3.11 icon" width="30" style="width:30px; border-style: none"/> 3.11 clusters only: While you troubleshoot, you can use the [{{site.data.keyword.containerlong_notm}} Diagnostics and Debug Tool](/docs/openshift?topic=openshift-cs_troubleshoot#debug_utility) to run tests and gather pertinent Ingress information from your cluster.
{: tip}



## No Ingress subdomain exists after cluster creation
{: #ingress_subdomain}

{: tsSymptoms}
You create a cluster and run `ibmcloud oc cluster get --cluster <cluster>` to check its status. The cluster **State** is `normal`, but the **Ingress Subdomain** and **Ingress Secret** are not available.

{: tsCauses}
Even if the cluster is in a `normal` state, the Ingress subdomain and secret might still be in progress. The Ingress subdomain and secret creation follows a process that might take more than 15 minutes to complete:

1. When worker nodes are fully deployed and ready on the VLANs, a portable public and a portable private subnet for the VLANs are ordered.
2. After the portable subnet orders are successfully fulfilled, the `ibm-cloud-provider-vlan-ip-config` config map is updated with the portable public and portable private IP addresses.
3. When the `ibm-cloud-provider-vlan-ip-config` config map is updated, the public ALB (version 3.11 clusters) or router for the Ingress controller (version 4.3 or later clusters) is triggered for creation.
4. A load balancer service that exposes the ALB or router is created and assigned an IP address.
5. The load balancer IP address is used to register the Ingress subdomain in Cloudflare. Cloudflare might have latency during the registration process.

{: tsResolve}
Typically, after the cluster is ready, the Ingress subdomain and secret are created after 15 minutes. If the Ingress subdomain and secret are still unavailable after your cluster is in a `normal` state for more than 15 minutes, you can check the progress of the creation process by following these steps:

1.  [Log in to your cluster](/docs/openshift?topic=openshift-access_cluster). Because the subdomain is not available, the OpenShift console cannot open. Instead, you can set the cluster context with the `--admin` flag through the CLI.
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
   kube-blrs3b1d0p0p2f7haq0g-mycluster-default-000001f7   169.xx.xxx.xxx    10.xxx.xx.xxx   u3c.2x4.encrypted   deployed   Ready    dal10   1.15.10
   ```
   {: screen}

3. Get the details of the `ibm-cloud-provider-vlan-ip-config` config map.
  * If the config map shows IP addresses, continue to the next step.
  * If the **Events** section shows a warning message similar to `ErrorSubnetLimitReached: There are already the maximum number of subnets permitted in this VLAN`, see the [VLAN capacity troubleshooting topic](/docs/openshift?topic=openshift-cs_troubleshoot_debug_ingress#cs_subnet_limit).

    ```
    kubectl describe cm ibm-cloud-provider-vlan-ip-config -n kube-system
    ```
    {: pre}

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

4. Verify that the ALB (version 3.11 clusters) or router for the Ingress controller (version 4.3 or later clusters) is successfully created.
  * **Version 3.11 clusters:**
    1. Check whether an ALB exists for your cluster and that the ALB has a public IP address assigned.
      * If a public ALB is listed and is assigned an IP address, continue to the next step.
      * If no ALBs are created after several minutes, [contact us](#getting_help).

        ```
        ibmcloud oc alb ls -c <cluster_name_or_ID>
        ```
        {: pre}

        Example output:
        ```
        ALB ID                                Enabled   Status     Type      ALB IP          Zone    Build                          ALB VLAN ID   NLB Version
        private-crbmnj1b1d09lpvv3oof0g-alb1   false     disabled   private   -               dal10   ingress:584/ingress-auth:344   2234947       2.0
        public-crbmnj1b1d09lpvv3oof0g-alb1    true      enabled    public    169.XX.XXX.XX   dal10   ingress:584/ingress-auth:344   2234945       2.0
        ```
        {: screen}

    2. Check whether the `LoadBalancer` service that exposes the ALB exists and is assigned the same IP address as the public ALB.
      * If a `LoadBalancer` service is listed and is assigned an IP address, continue to the next step.
      * If no `LoadBalancer` services are created after several minutes, [contact us](#getting_help).

        ```
        kubectl get svc -n kube-system | grep LoadBalancer
        ```
        {: pre}

        Example output:
        ```
        public-crbmnj1b1d09lpvv3oof0g-alb1   LoadBalancer   172.21.XXX.XXX   169.XX.XXX.XX   80:30723/TCP,443:31241/TCP   1d
        ```
        {: screen}
  * **Version 4.3 and later clusters:**
    1. Check whether a router deployment exists for your cluster.
      * If a router deployment is listed, continue to the next step.
      * If no router deployment is created after several minutes, [contact us](#getting_help).

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

    2. Check whether the router's load balancer service exists and is assigned a public external IP address.
      * If a service that is named `router-default` is listed and is assigned an IP address, continue to the next step.
      * If no `router-default` service is created after several minutes, [contact us](#getting_help).

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

5. Check again whether the Ingress subdomain and secret are created. If they are not available, but you verified that all of the components in steps 1 - 3 exist, [contact us](#getting_help).
  ```
  ibmcloud oc cluster get -c <cluster_name_or_ID>
  ```
  {: pre}

<br />


## No Ingress subdomain exists after you create clusters of the same or similar name
{: #cs_rate_limit}

{: tsSymptoms}
You create and delete a cluster multiple times, such as for automation purposes, and you either use the same name for the cluster every time that you create it, or a name that is very similar to previous names that you used. When you run `ibmcloud oc cluster get --cluster <cluster>`, your cluster is in a `normal` state but no **Ingress Subdomain** or **Ingress Secret** are available.

{: tsCauses}
When you create and delete a cluster that uses the same name multiple times, the Ingress subdomain for that cluster in the format `<cluster_name>.<globally_unique_account_HASH>-0000.<region>.containers.appdomain.cloud` is registered and unregistered each time. The certificate for the subdomain is also generated and deleted each time. If you create and delete a cluster with the same name 5 times or more within 7 days, you might reach the Let's Encrypt [Duplicate Certificate rate limit](https://letsencrypt.org/docs/rate-limits/?origin_team=T4LT36D1N){: external}, because the same Ingress subdomain and certificate are registered every time that you create the cluster. Because very long cluster names are truncated to 24 characters in the Ingress subdomain for the cluster, you can also reach the rate limit if you use multiple cluster names that have the same first 24 characters.

{: tsResolve}
If you need to continue testing, you can change the name of the cluster so that when you create the new cluster a new, different Ingress subdomain and secret are registered.

<br />


## Cannot connect to an app via Ingress
{: #cs_ingress_fails}

{: tsSymptoms}
You publicly exposed your app by creating an Ingress resource for your app in your classic cluster. When you tried to connect to your app by using the public IP address or Ingress subdomain, the connection failed or timed out.

{: tsResolve}
First, check that your cluster is fully deployed and has at least 2 worker nodes available per zone to ensure high availability for your ALB (version 3.11 clusters) or router for the Ingress controller (version 4.3 or later clusters).
```
ibmcloud oc worker ls --cluster <cluster_name_or_ID>
```
{: pre}

In your CLI output, make sure that the **Status** of your worker nodes displays **Ready** and that the **Machine Type** shows a flavor other than **free**.

* If your standard cluster is fully deployed and has at least 2 worker nodes per zone, but no **Ingress Subdomain** is available, see [No Ingress subdomain exists after cluster creation](/docs/openshift?topic=openshift-cs_troubleshoot_debug_ingress#ingress_subdomain).
* For other issues, troubleshoot your Ingress setup by following the steps in [3.11 clusters: Debugging Ingress](#ingress-debug)or [4.3 clusters: Debugging Ingress](#ingress-debug-roks4).

Version 3.11 clusters: If you recently restarted your ALB pods or enabled an ALB, a [readiness check](/docs/openshift?topic=openshift-ingress-settings#readiness-check) prevents ALB pods from attempting to route traffic requests until all of the Ingress resource files are parsed. This readiness check prevents request loss and can take up to 5 minutes.
{: note}

<br />


## 4.3 clusters: Debugging Ingress
{: #ingress-debug-roks4}
{: troubleshoot}
{: support}

<img src="images/icon-version-43.png" alt="Version 4.3 icon" width="30" style="width:30px; border-style: none"/> This troubleshooting topic applies only to OpenShift clusters that run version 4.3. For 3.11 clusters, see [3.11 clusters: Debugging Ingress](#ingress-debug).
{: note}

{: tsSymptoms}
You publicly exposed your app by creating an Ingress resource for your app in your cluster. However, when you try to connect to your app through the Ingress subdomain or the IP address of the Ingress controller's router, the connection fails or times out.

{: tsResolve}
The steps in the following sections can help you debug your Ingress setup.

Before you begin, ensure you have the following [{{site.data.keyword.cloud_notm}} IAM access policies](/docs/openshift?topic=openshift-users#platform) for {{site.data.keyword.containerlong_notm}}:
  - **Editor** or **Administrator** platform role for the cluster
  - **Writer** or **Manager** service role

Seeing an **Application is not available** page when you try to access your app's subdomain? [Check your app deployment and Ingress resource configuration](#app-debug-ingress-43). Seeing a **Connection timeout** page? [Check the health of the Ingress controller's router pods](#errors-43).
{: tip}

### Step 1: Check your app deployment and Ingress resource configuration
{: #app-debug-ingress-43}

Start by checking for errors in your app deployment and the Ingress resource deployment. Error messages in your deployments can help you find the root causes for failures and further debug your Ingress setup in the next sections.
{: shortdesc}

1. Before you debug Ingress, first check out [Debugging app deployments](/docs/openshift?topic=openshift-cs_troubleshoot_app#debug_apps). Ingress issues are often caused by underlying issues in your app deployment or in the `ClusterIP` service that exposes your app. For example, your app label and service selector might not match, or your app and service target ports might not match.

2. Check your Ingress resource deployment and look for warnings or error messages.
    ```
    oc describe ingress <ingress_resource_name>
    ```
    {: pre}

    In the **Events** section of the output, you might see warning messages about invalid values in your Ingress resource or in certain annotations that you used. Check the [Ingress resource configuration documentation](/docs/openshift?topic=openshift-ingress#public_inside_4). For annotations, note that the {{site.data.keyword.containerlong_notm}} annotations (`ingress.bluemix.net/<annotation>`) and NGINX annotations (`nginx.ingress.kubernetes.io/<annotation>`) are not supported for the router or the Ingress resource in OpenShift version 4.3 and later. If you want to customize routing rules for apps in a cluster that runs OpenShift version 4.3 or later, you can use [HAProxy annotations for the OpenShift router](https://docs.openshift.com/container-platform/4.3/networking/routes/route-configuration.html#nw-route-specific-annotations_route-configuration){: external} that manages traffic for your app. These annotations are in the format `haproxy.router.openshift.io/<annotation>` or `router.openshift.io/<annotation>`. To add annotations to the router, run `oc edit svc router-default -n openshift-ingress`.

    ```
    Name:             myingress
    Namespace:        default
    Address:          169.xx.xxx.xxx,169.xx.xxx.xxx
    Default backend:  default-http-backend:80 (<none>)
    Rules:
      Host                                             Path  Backends
      ----                                             ----  --------
      mycluster-<hash>-0000.us-south.containers.appdomain.cloud
                                                       /tea      myservice1:80 (<none>)
                                                       /coffee   myservice2:80 (<none>)
    Annotations:
      custom-port:        protocol=http port=7490; protocol=https port=4431
      location-modifier:  modifier='~' serviceName=myservice1;modifier='^~' serviceName=myservice2
    Events:
      Type     Reason             Age   From                                Message
      ----     ------             ----  ----                                -------
      Warning  TLSSecretNotFound  1m    router-default-69d6f598f8-vn8tj     Failed to apply ingress resource.
      Warning  AnnotationError    2s    router-default-69d6f598f8-vn8tj     Failed to apply ingress.bluemix.net/custom-port annotation.
      Warning  TLSSecretNotFound  1m    router-dal10-y2d4359tf4-g4ar7       Failed to apply ingress resource.
      Warning  AnnotationError    2s    router-dal10-y2d4359tf4-g4ar7       Failed to apply ingress.bluemix.net/custom-port annotation.
    ```
    {: screen}

3. Check the Ingress resource configuration file.
    ```
    oc get ingress -o yaml
    ```
    {: pre}

    1. Ensure that you define a host in only one Ingress resource. If one host is defined in multiple Ingress resources, the Ingress controller might not forward traffic properly and you might experience errors.

    2. Check that the subdomain and TLS certificate are correct. To find the IBM provided Ingress subdomain and TLS certificate, run `ibmcloud oc cluster get --cluster <cluster_name_or_ID>`.

    3.  Make sure that your app listens on the same path that is configured in the **path** section of your Ingress. If your app is set up to listen on the root path, use `/` as the path. If incoming traffic to this path must be routed to a different path that your app listens on, use the [rewrite paths](/docs/openshift?topic=openshift-ingress_annotation#rewrite-path) annotation.

    4. Edit your resource configuration YAML as needed. When you close the editor, your changes are saved and automatically applied.
        ```
        oc edit ingress <myingressresource>
        ```
        {: pre}

### Step 2: Check the health of the Ingress controller's router
{: #errors-43}

Verify that the Ingress operator and the Ingress controller's router are healthy. Ingress controllers are managed by the Ingress operator. The router forwards requests to the pods for that app only according to the rules defined in the Ingress resource and implemented by the Ingress controller.
{: shortdesc}

1. Check the status of your Ingress operator pods.
    1. Get the Ingress operator pods that are running in your cluster.
        ```
        oc get pods -n openshift-ingress-operator
        ```
        {: pre}

    2. Make sure that all pods are running by checking the **STATUS** column.

    3. If a pod does not have a `Running` status, you can delete the pod to restart it.
        ```
        oc delete pod <pod> -n openshift-ingress-operator
        ```
        {: pre}

    4. Get the logs for the Ingress controller and look for error messages in the logs.
        ```
        oc logs deployments/ingress-operator --namespace=openshift-ingress-operator
        ```
        {: pre}

2. Check the status and logs of your Ingress controller's router pods.
    1. Get the Ingress controller's router pods that are running in your cluster.
        ```
        oc get pods -n openshift-ingress
        ```
        {: pre}

    2. Make sure that all `router-default` pods and pods for routers in any other zone are running by checking the **STATUS** column. If you have a multizone cluster, note that the router service in the first zone where you have workers nodes is always named `router-default`, and router services in the zones that you subsequently add to your cluster have names such as `router-dal12`.

    3. If a pod does not have a `Running` status, you can delete the pod to restart it.
        ```
        oc delete pod <pod> -n openshift-ingress
        ```
        {: pre}

    4. Get the logs for each pod and look for error messages in the logs. 
        ```
        oc logs <pod> -n openshift-ingress
        ```
        {: pre}

### Step 3: Ping the Ingress subdomain and router public IP address
{: #ping-43}

Check the availability of the public IP addresses of the Ingress controller's routers and verify your subdomain mappings.
{: shortdesc}

1. Get the external IP addresses that the router services are listening on. If you have a multizone cluster, note that the router service in the first zone where you have workers nodes is always named `router-default`, and router services in the zones that you subsequently add to your cluster have names such as `router-dal12`.
    ```
    oc get svc -n openshift-ingress
    ```
    {: pre}

    Example output for a multizone cluster with worker nodes in `dal10` and `dal13`:
    ```
    NAME                                         TYPE           CLUSTER-IP      EXTERNAL-IP    PORT(S)                      AGE
    router-dal13                                 LoadBalancer   172.21.47.119   169.XX.XX.XX   80:32318/TCP,443:30915/TCP   26d
    router-default                               LoadBalancer   172.21.47.119   169.XX.XX.XX   80:32637/TCP,443:31719/TCP   26d
    router-internal-default                      ClusterIP      172.21.51.30    <none>         80/TCP,443/TCP,1936/TCP      26d
    ```
    {: screen}

    If a router has no external IP address, see [4.3 clusters: Router for Ingress controller does not deploy](/docs/openshift?topic=openshift-cs_troubleshoot_debug_ingress#cs_subnet_limit_43).
    {: note}

2. Check the health of your router by pinging its IP address.
  * Single-zone clusters:
    ```
    ping <router_IP>
    ```
    {: pre}
    * If the CLI returns a timeout and you have a custom firewall that is protecting your worker nodes, make sure that you allow ICMP in your [firewall](/docs/openshift?topic=openshift-cs_troubleshoot#cs_firewall).
    * If you don't have a firewall or your firewall does not block the pings and the pings still timeout, [check the status of your router pods](#errors-43).
  * Multizone clusters: Router services in multizone clusters are created with a `/healthz` path so that you can check the health of each service IP address. The following HTTP cURL command uses the `/healthz` past, which is configured to return the `ok` status for a healthy IP.
    ```
    curl -X GET http://<router_svc_ip>/healthz -H "Host:router-default.<ingress_subdomain>"
    ```
    {: pre}
    If one or more of the IP addresses does not return `ok`, [check the status of your router pods](#errors-43).

3. Get the IBM-provided Ingress subdomain.
    ```
    ibmcloud oc cluster get --cluster <cluster_name_or_ID> | grep Ingress
    ```
    {: pre}

    Example output:
    ```
    Ingress Subdomain:      mycluster-<hash>-0000.us-south.containers.appdomain.cloud
    Ingress Secret:         mycluster-<hash>-0000
    ```
    {: screen}

4. Ensure that the router IP address is registered with your cluster's IBM-provided Ingress subdomain. For example, in a multizone cluster, the public router IP in each zone where you have worker nodes must be registered under the same subdomain.
    ```
    host <ingress_subdomain>
    ```
    {: pre}

    Example output:
    ```
    mycluster-<hash>-0000.us-south.containers.appdomain.cloud has address 169.XX.XX.XXX
    mycluster-<hash>-0000.us-south.containers.appdomain.cloud has address 169.XX.XXX.XX
    ```
    {: screen}

5. If you use a custom domain, verify that you used your DNS provider to map the custom domain to the IBM-provided subdomain or the router's public IP address.
    * **IBM-provided subdomain CNAME**: Check that your custom domain is mapped to the cluster's IBM-provided subdomain in the Canonical Name record (CNAME).
        ```
        host www.my-domain.com
        ```
        {: pre}

        Example output:
        ```
        www.my-domain.com is an alias for mycluster-<hash>-0000.us-south.containers.appdomain.cloud
        mycluster-<hash>-0000.us-south.containers.appdomain.cloud has address 169.XX.XX.XXX
        mycluster-<hash>-0000.us-south.containers.appdomain.cloud has address 169.XX.XX.XXX
        ```
        {: screen}

    * **Public IP address A record**: Check that your custom domain is mapped to the router's portable public IP address in the A record.
        ```
        host www.my-domain.com
        ```
        {: pre}

        Example output:
        ```
        www.my-domain.com has address 169.XX.XX.XXX
        www.my-domain.com has address 169.XX.XX.XXX
        ```
        {: screen}

<br />


## 4.3 clusters: Router for Ingress controller does not deploy in a zone
{: #cs_subnet_limit_43}

<img src="images/icon-version-43.png" alt="Version 4.3 icon" width="30" style="width:30px; border-style: none"/> This troubleshooting topic applies only to OpenShift clusters that run version 4.3.
{: note}

{: tsSymptoms}
When you run `oc get svc -n openshift-ingress`, one or more zones has no public router.
* No `router-default` service is deployed, or the service might not have an external IP address assigned. For example, in a single-zone cluster, you might see the following:
  ```
  NAME                                         TYPE           CLUSTER-IP      EXTERNAL-IP    PORT(S)                      AGE
  router-default                               LoadBalancer   172.21.47.119   <none>         80:32637/TCP,443:31719/TCP   26m
  router-internal-default                      ClusterIP      172.21.51.30    <none>         80/TCP,443/TCP,1936/TCP      26m
  ```
  {: screen}
* If you have a multizone cluster, one zone has no router service. For example, in a multizone cluster that has worker nodes in `dal10` and `dal12`, you might see a `router-default` service for `dal10`, but no `router-dal12` for `dal12`. Note that the router service in the first zone where you have workers nodes is always named `router-default`, and router services in the zones that you subsequently add to your cluster have names such as `router-dal12`.
  ```
  NAME                                         TYPE           CLUSTER-IP      EXTERNAL-IP    PORT(S)                      AGE
  router-default                               LoadBalancer   172.21.47.119   169.XX.XX.XX   80:32637/TCP,443:31719/TCP   26m
  router-internal-default                      ClusterIP      172.21.51.30    <none>         80/TCP,443/TCP,1936/TCP      26m
  ```
  {: screen}

{: tsCauses}
In standard clusters, the first time that you create a cluster in a zone, a public VLAN and a private VLAN in that zone are automatically provisioned for you in your IBM Cloud infrastructure account. In that zone, 1 public portable subnet is requested on the public VLAN that you specify and 1 private portable subnet is requested on the private VLAN that you specify. For Red Hat OpenShift on IBM Cloud, VLANs have a limit of 40 subnets. If the cluster's VLAN in a zone already reached that limit, the **Ingress Subdomain** fails to provision and the default public router for the Ingress controller fails to provision.

To view how many subnets a VLAN has:
1.  From the [IBM Cloud infrastructure console](https://cloud.ibm.com/classic?), select **Network** > **IP Management** > **VLANs**.
2.  Click the **VLAN Number** of the VLAN that you used to create your cluster. Review the **Subnets** section to see whether 40 or more subnets exist.

{: tsResolve}
Option 1: If you need a new VLAN, order one by [contacting {{site.data.keyword.cloud_notm}} support](/docs/vlans?topic=vlans-ordering-premium-vlans#ordering-premium-vlans). Then, [create a cluster](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_cluster_create) that uses this new VLAN.

Option 2: If you have another VLAN that is available, you can [set up VLAN spanning](/docs/vlans?topic=vlans-vlan-spanning#vlan-spanning) in your existing cluster. To check if VLAN spanning is already enabled, use the `ibmcloud oc vlan spanning get --region <region>` [command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_vlan_spanning_get). Then, you can add new worker nodes to the cluster that use the other VLAN with available subnets. Create at least 2 worker nodes per zone. Now, IP addresses are available so that the routers can automatically deploy.

Option 3: If you are not using all the subnets in the VLAN, you can reuse subnets on the VLAN by adding them to your cluster.
1. Check that the subnet that you want to use is available.
  <p class="note">The infrastructure account that you use might be shared across multiple {{site.data.keyword.cloud_notm}} accounts. In this case, even if you run the `ibmcloud oc subnets` command to see subnets with **Bound Clusters**, you can see information only for your clusters. Check with the infrastructure account owner to make sure that the subnets are available and not in use by any other account or team.</p>

2. Use the [`ibmcloud oc cluster subnet add` command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_cluster_subnet_add) to make an existing subnet available to your cluster.

3. Verify that the subnet was successfully created and added to your cluster. The subnet CIDR is listed in the **Subnet VLANs** section.
    ```
    ibmcloud oc cluster get --show-resources <cluster_name_or_ID>
    ```
    {: pre}

    In this example output, a second subnet was added to the `2234945` public VLAN:
    ```
    Subnet VLANs
    VLAN ID   Subnet CIDR          Public   User-managed
    2234947   10.xxx.xx.xxx/29     false    false
    2234945   169.xx.xxx.xxx/29    true     false
    2234945   169.xx.xxx.xxx/29    true     false
    ```
    {: screen}

4. Verify that the portable IP addresses from the subnet that you added are used for the router in your cluster. It might take several minutes for the services to use the portable IP addresses from the newly-added subnet.
  * **No Ingress subdomain**: Run `ibmcloud oc cluster get --cluster <cluster>` to verify that the **Ingress Subdomain** is populated.
  * **A router does not deploy in a zone**: Run `oc get svc -n openshift-ingress` to verify that the missing router is deployed with an external IP address.

<br />


## 3.11 clusters: Debugging Ingress
{: #ingress-debug}
{: troubleshoot}
{: support}


<img src="images/icon-version-311.png" alt="Version 3.11 icon" width="30" style="width:30px; border-style: none"/> This troubleshooting topic applies only to OpenShift clusters that run version 3.11. For 4.3 clusters, see [4.3 clusters: Debugging Ingress](#ingress-debug-roks4).
{: note}


{: tsSymptoms}
You publicly exposed your app by creating an Ingress resource for your app in your cluster. However, when you try to connect to your app through the Ingress subdomain or the ALBs' IP addresses, the connection fails or times out.

{: tsResolve}
The steps in the following sections can help you debug your Ingress setup.

Before you begin, ensure you have the following [{{site.data.keyword.cloud_notm}} IAM access policies](/docs/openshift?topic=openshift-users#platform) for {{site.data.keyword.containerlong_notm}}:
  - **Editor** or **Administrator** platform role for the cluster
  - **Writer** or **Manager** service role

### Step 1: Check your app deployment
{: #app-debug-ingress}

Before you debug Ingress, first check out [Debugging app deployments](/docs/openshift?topic=openshift-cs_troubleshoot_app#debug_apps).
{: shortdesc}

Ingress issues are often caused by underlying issues in your app deployment or in the `ClusterIP` service that exposes your app. For example, your app label and service selector might not match, or your app and service target ports might not match.

### Step 2: Run Ingress tests in the Diagnostics and Debug Tool
{: #debug-tool-ingress}

While you troubleshoot, you can use the {{site.data.keyword.containerlong_notm}} Diagnostics and Debug Tool to run Ingress tests and gather pertinent Ingress information from your cluster. To use the debug tool, you can enable the add-on in your cluster.
{: shortdesc}

1. In your [cluster dashboard](https://cloud.ibm.com/kubernetes/clusters?platformType=openshift){: external}, click the name of the cluster where you want to install the debug tool add-on.

2. Click the **Add-ons** tab.

3. On the Diagnostics and Debug Tool card, click **Install**.

4. In the dialog box, click **Install**. Note that it can take a few minutes for the add-on to be installed.

5. On the Diagnostics and Debug Tool card, click **Dashboard**.

5. In the debug tool dashboard, select the **ingress** group of tests. Some tests check for potential warnings, errors, or issues, and some tests only gather information that you can reference while you troubleshoot. For more information about the function of each test, click the information icon next to the test's name.

6. Click **Run**.

7. Check the results of each test.
  * If any test fails, click the information icon next to the test's name in the left-hand column for information about how to resolve the issue.
  * You can also use the results of tests that only gather information while you debug your Ingress service in the following sections.

### Step 3: Check for error messages in your Ingress deployment and the ALB pod logs
{: #errors}

Start by checking for error messages in the Ingress resource deployment events and ALB pod logs. These error messages can help you find the root causes for failures and further debug your Ingress setup in the next sections.
{: shortdesc}

1. Check your Ingress resource deployment and look for warnings or error messages.
    ```
    oc describe ingress <myingress>
    ```
    {: pre}

    In the **Events** section of the output, you might see warning messages about invalid values in your Ingress resource or in certain annotations that you used. Check the [Ingress resource configuration documentation](/docs/openshift?topic=openshift-ingress#public_inside_4) or the [annotations documentation](/docs/openshift?topic=openshift-ingress_annotation).

    ```
    Name:             myingress
    Namespace:        default
    Address:          169.xx.xxx.xxx,169.xx.xxx.xxx
    Default backend:  default-http-backend:80 (<none>)
    Rules:
      Host                                             Path  Backends
      ----                                             ----  --------
      mycluster-<hash>-0000.us-south.containers.appdomain.cloud
                                                       /tea      myservice1:80 (<none>)
                                                       /coffee   myservice2:80 (<none>)
    Annotations:
      custom-port:        protocol=http port=7490; protocol=https port=4431
      location-modifier:  modifier='~' serviceName=myservice1;modifier='^~' serviceName=myservice2
    Events:
      Type     Reason             Age   From                                                            Message
      ----     ------             ----  ----                                                            -------
      Normal   Success            1m    public-cr87c198fcf4bd458ca61402bb4c7e945a-alb1-258623678-gvf9n  Successfully applied ingress resource.
      Warning  TLSSecretNotFound  1m    public-cr87c198fcf4bd458ca61402bb4c7e945a-alb1-258623678-gvf9n  Failed to apply ingress resource.
      Normal   Success            59s   public-cr87c198fcf4bd458ca61402bb4c7e945a-alb1-258623678-gvf9n  Successfully applied ingress resource.
      Warning  AnnotationError    40s   public-cr87c198fcf4bd458ca61402bb4c7e945a-alb1-258623678-gvf9n  Failed to apply ingress.bluemix.net/custom-port annotation. Error annotation format error : One of the mandatory fields not valid/missing for annotation ingress.bluemix.net/custom-port
      Normal   Success            40s   public-cr87c198fcf4bd458ca61402bb4c7e945a-alb1-258623678-gvf9n  Successfully applied ingress resource.
      Warning  AnnotationError    2s    public-cr87c198fcf4bd458ca61402bb4c7e945a-alb1-258623678-gvf9n  Failed to apply ingress.bluemix.net/custom-port annotation. Invalid port 7490. Annotation cannot use ports 7481 - 7490
      Normal   Success            2s    public-cr87c198fcf4bd458ca61402bb4c7e945a-alb1-258623678-gvf9n  Successfully applied ingress resource.
    ```
    {: screen}
{: #check_pods}
2. Check the status of your ALB pods.
    1. Get the ALB pods that are running in your cluster.
        ```
        oc get pods -n kube-system | grep alb
        ```
        {: pre}

    2. Make sure that all pods are running by checking the **STATUS** column.

    3. If a pod does not have a `Running` status, you can disable and re-enable the ALB. In the following commands, replace `<ALB_ID>` with the ID of the pod's ALB. For example, if the pod that is not running has the name `public-crb2f60e9735254ac8b20b9c1e38b649a5-alb1-5d6d86fbbc-kxj6z`, the ALB ID is `public-crb2f60e9735254ac8b20b9c1e38b649a5-alb1`.

      When the pod restarts, a [readiness check](/docs/openshift?topic=openshift-ingress-settings#readiness-check) prevents the ALB pod from attempting to route traffic requests until all of the Ingress resource files are parsed. This readiness check prevents request loss and can take up to 5 minutes by default.
      {: note}
      * Classic clusters:
        ```
        ibmcloud oc alb configure classic --alb-id <ALB_ID> --disable
        ```
        {: pre}

        ```
        ibmcloud oc alb configure classic --alb-id <ALB_ID> --enable
        ```
        {: pre}
      * VPC clusters:
        ```
        ibmcloud oc alb configure vpc-classic --alb-id <ALB_ID> --disable
        ```
        {: pre}

        ```
        ibmcloud oc alb configure vpc-classic --alb-id <ALB_ID> --enable
        ```
        {: pre}

3. Check the logs for your ALB.
    1.  Get the IDs of the ALB pods that are running in your cluster.
        ```
        oc get pods -n kube-system | grep alb
        ```
        {: pre}

    3. Get the logs for the `nginx-ingress` container on each ALB pod.
        ```
        oc logs <ingress_pod_ID> nginx-ingress -n kube-system
        ```
        {: pre}

    4. Look for error messages in the ALB logs.

### Step 4: Ping the ALB subdomain and public IP addresses
{: #ping}

Check the availability of your Ingress subdomain and ALBs' public IP addresses.
{: shortdesc}

1. Get the IP addresses that your public ALBs are listening on.
    ```
    ibmcloud oc alb ls --cluster <cluster_name_or_ID>
    ```
    {: pre}

    Example output for a multizone cluster with worker nodes in `dal10` and `dal13`:

    ```
    ALB ID                                            Enabled   Status     Type      ALB IP          Zone    Build                          ALB VLAN ID   NLB Version
    private-cr24a9f2caf6554648836337d240064935-alb1   false     disabled   private   -               dal13   ingress:411/ingress-auth:315   2294021       -
    private-cr24a9f2caf6554648836337d240064935-alb2   false     disabled   private   -               dal10   ingress:411/ingress-auth:315   2234947       -
    public-cr24a9f2caf6554648836337d240064935-alb1    true      enabled    public    169.62.196.238  dal13   ingress:411/ingress-auth:315   2294019       -
    public-cr24a9f2caf6554648836337d240064935-alb2    true      enabled    public    169.46.52.222   dal10   ingress:411/ingress-auth:315   2234945       -
    ```
    {: screen}

    * If a public ALB has no IP address, see [Ingress ALB does not deploy in a zone](/docs/openshift?topic=openshift-cs_troubleshoot_debug_ingress#cs_subnet_limit).

2. Check the health of your ALB IPs.

    * For single zone cluster and multizone clusters: Ping the IP address of each public ALB to ensure that each ALB is able to successfully receive packets. If you are using private ALBs, you can ping their IP addresses only from the private network.
        ```
        ping <ALB_IP>
        ```
        {: pre}

        * If the CLI returns a timeout and you have a custom firewall that is protecting your worker nodes, make sure that you allow ICMP in your [firewall](/docs/openshift?topic=openshift-cs_troubleshoot#cs_firewall).
        * If you don't have a firewall or your firewall does not block the pings and the pings still timeout, [check the status of your ALB pods](#check_pods).

    * Multizone clusters only: You can use the MZLB health check to determine the status of your ALB IPs. For more information about the MZLB, see [Multizone load balancer (MZLB)](/docs/openshift?topic=openshift-ingress-about#ingress_components). The MZLB health check is available only for clusters that have the new Ingress subdomain in the format `<cluster_name>.<region_or_zone>.containers.appdomain.cloud`. If your cluster still uses the older format of `<cluster_name>.<region>.containers.mybluemix.net`, [convert your single zone cluster to multizone](/docs/openshift?topic=openshift-add_workers#add_zone). Your cluster is assigned a subdomain with the new format, but can also continue to use the older subdomain format. Alternatively, you can order a new cluster that is automatically assigned the new subdomain format.

    The following HTTP cURL command uses the `albhealth` host, which is configured by Red Hat OpenShift on IBM Cloud to return the `healthy` or `unhealthy` status for an ALB IP.
        ```
        curl -X GET http://169.62.196.238/ -H "Host: albhealth.mycluster-<hash>-0000.us-south.containers.appdomain.cloud"
        ```
        {: pre}

        Example output:
        ```
        healthy
        ```
        {: screen}
        If one or more of the IPs returns `unhealthy`, [check the status of your ALB pods](#check_pods).

3. Get the IBM-provided Ingress subdomain.
    ```
    ibmcloud oc cluster get --cluster <cluster_name_or_ID> | grep Ingress
    ```
    {: pre}

    Example output:
    ```
    Ingress Subdomain:      mycluster-<hash>-0000.us-south.containers.appdomain.cloud
    Ingress Secret:         mycluster-<hash>-0000
    ```
    {: screen}

4. Ensure that the IPs for each public ALB that you got in step 2 of this section are registered with your cluster's IBM-provided Ingress subdomain. For example, in a multizone cluster, the public ALB IP in each zone where you have worker nodes must be registered under the same subdomain.

    ```
    oc get ingress -o wide
    ```
    {: pre}

    Example output:
    ```
    NAME                HOSTS                                                    ADDRESS                        PORTS     AGE
    myingressresource   mycluster-<hash>-0000.us-south.containers.appdomain.cloud      169.46.52.222,169.62.196.238   80        1h
    ```
    {: screen}

### Step 5: Check your domain mappings and Ingress resource configuration
{: #ts_ingress_config}

1. If you use a custom domain, verify that you used your DNS provider to map the custom domain to the IBM-provided subdomain or the ALB's public IP address. Note that using a CNAME is preferred because IBM provides automatic health checks on the IBM subdomain and removes any failing IPs from the DNS response.
    * **IBM-provided subdomain CNAME**: Check that your custom domain is mapped to the cluster's IBM-provided subdomain in the Canonical Name record (CNAME).
        ```
        host www.my-domain.com
        ```
        {: pre}

        Example output:
        ```
        www.my-domain.com is an alias for mycluster-<hash>-0000.us-south.containers.appdomain.cloud
        mycluster-<hash>-0000.us-south.containers.appdomain.cloud has address 169.46.52.222
        mycluster-<hash>-0000.us-south.containers.appdomain.cloud has address 169.62.196.238
        ```
        {: screen}

    * **Public IP address A record**: Check that your custom domain is mapped to the ALB's portable public IP address in the A record. The IPs should match the public ALB IPs that you got in step 1 of the [previous section](#ping).
        ```
        host www.my-domain.com
        ```
        {: pre}

        Example output:
        ```
        www.my-domain.com has address 169.46.52.222
        www.my-domain.com has address 169.62.196.238
        ```
        {: screen}

2. Check the Ingress resource configuration files for your cluster.
    ```
    oc get ingress -o yaml
    ```
    {: pre}

    1. Ensure that you define a host in only one Ingress resource. If one host is defined in multiple Ingress resources, the ALB might not forward traffic properly and you might experience errors.

    2. Check that the subdomain and TLS certificate are correct. To find the IBM provided Ingress subdomain and TLS certificate, run `ibmcloud oc cluster get --cluster <cluster_name_or_ID>`.

    3.  Make sure that your app listens on the same path that is configured in the **path** section of your Ingress. If your app is set up to listen on the root path, use `/` as the path. If incoming traffic to this path must be routed to a different path that your app listens on, use the [rewrite paths](/docs/openshift?topic=openshift-ingress_annotation#rewrite-path) annotation.

    4. Edit your resource configuration YAML as needed. When you close the editor, your changes are saved and automatically applied.
        ```
        oc edit ingress <myingressresource>
        ```
        {: pre}

### Removing an ALB from DNS for debugging
{: #one_alb}

If you can't access your app through a specific ALB IP, you can temporarily remove the ALB from production by disabling its DNS registration. Then, you can use the ALB's IP address to run debugging tests on that ALB.

For example, say you have a multizone cluster in 2 zones, and the 2 public ALBs have IP addresses `169.46.52.222` and `169.62.196.238`. Although the health check is returning healthy for the second zone's ALB, your app isn't directly reachable through it. You decide to remove that ALB's IP address, `169.62.196.238`, from production for debugging. The first zone's ALB IP, `169.46.52.222`, is registered with your domain and continues to route traffic while you debug the second zone's ALB.

1. Get the name of the ALB with the unreachable IP address.
    ```
    ibmcloud oc alb ls --cluster <cluster_name> | grep <ALB_IP>
    ```
    {: pre}

    For example, the unreachable IP `169.62.196.238` belongs to the ALB `public-cr24a9f2caf6554648836337d240064935-alb1`:
    ```
    ALB ID                                            Enabled   Status     Type      ALB IP           Zone    Build                          ALB VLAN ID   NLB Version
    public-cr24a9f2caf6554648836337d240064935-alb1    false     disabled   private   169.62.196.238   dal13   ingress:411/ingress-auth:315   2294021       -
    ```
    {: screen}

2. Using the ALB name from the previous step, get the names of the ALB pods. The following command uses the example ALB name from the previous step:
    ```
    oc get pods -n kube-system | grep public-cr24a9f2caf6554648836337d240064935-alb1
    ```
    {: pre}

    Example output:
    ```
    public-cr24a9f2caf6554648836337d240064935-alb1-7f78686c9d-8rvtq   2/2       Running   0          24m
    public-cr24a9f2caf6554648836337d240064935-alb1-7f78686c9d-trqxc   2/2       Running   0          24m
    ```
    {: screen}

3. Disable the health check that runs for all ALB pods. Repeat these steps for each ALB pod that you got in the previous step. The example commands and output in these steps use the first pod, `public-cr24a9f2caf6554648836337d240064935-alb1-7f78686c9d-8rvtq`.
    1. Log in to the ALB pod and check the `server_name` line in the NGINX configuration file.
        ```
        oc exec -ti public-cr24a9f2caf6554648836337d240064935-alb1-7f78686c9d-8rvtq -n kube-system -c nginx-ingress -- grep server_name /etc/nginx/conf.d/kube-system-alb-health.conf
        ```
        {: pre}

        Example output that confirms the ALB pod is configured with the correct health check subdomain, `albhealth.<domain>`:
        ```
        server_name albhealth.mycluster-<hash>-0000.us-south.containers.appdomain.cloud;
        ```
        {: screen}

    2. To remove the IP by disabling the health check, insert `#` in front of the `server_name`. When the `albhealth.mycluster-<hash>-0000.us-south.containers.appdomain.cloud` virtual host is disabled for the ALB, the automated health check automatically removes the IP from the DNS response.
        ```
        oc exec -ti public-cr24a9f2caf6554648836337d240064935-alb1-7f78686c9d-8rvtq -n kube-system -c nginx-ingress -- sed -i -e 's*server_name*#server_name*g' /etc/nginx/conf.d/kube-system-alb-health.conf
        ```
        {: pre}

    3. Verify that the change was applied.
        ```
        oc exec -ti public-cr24a9f2caf6554648836337d240064935-alb1-7f78686c9d-8rvtq -n kube-system -c nginx-ingress -- grep server_name /etc/nginx/conf.d/kube-system-alb-health.conf
        ```
        {: pre}

        Example output:
        ```
        #server_name albhealth.mycluster-<hash>-0000.us-south.containers.appdomain.cloud
        ```
        {: screen}

    4. To remove the IP from the DNS registration, reload the NGINX configuration.
        ```
        oc exec -ti public-cr24a9f2caf6554648836337d240064935-alb1-7f78686c9d-8rvtq -n kube-system -c nginx-ingress -- nginx -s reload
        ```
        {: pre}

    5. Repeat these steps for each ALB pod.

4. Now, when you attempt to cURL the `albhealth` host to health check the ALB IP, the check fails.
    ```
    curl -X GET http://169.62.196.238/ -H "Host: albhealth.mycluster-<hash>-0000.us-south.containers.appdomain.cloud"
    ```
    {: pre}

    Output:
    ```
    <html>
        <head>
            <title>404 Not Found</title>
        </head>
        <body bgcolor="white"><center>
            <h1>404 Not Found</h1>
        </body>
    </html>
    ```
    {: screen}

5. Verify that the ALB IP address is removed from the DNS registration for your domain by checking the Cloudflare server. Note that the DNS registration might take a few minutes to update.
    ```
    host mycluster-<hash>-0000.us-south.containers.appdomain.cloud ada.ns.cloudflare.com
    ```
    {: pre}

    Example output that confirms that only the healthy ALB IP, `169.46.52.222`, remains in the DNS registration and that the unhealthy ALB IP, `169.62.196.238`, has been removed:
    ```
    mycluster-<hash>-0000.us-south.containers.appdomain.cloud has address 169.46.52.222
    ```
    {: screen}

6. Now that the ALB IP has been removed from production, you can run debugging tests against your app through it. To test communication to your app through this IP, you can run the following cURL command, replacing the example values with your own values:
    ```
    curl -X GET --resolve mycluster-<hash>-0000.us-south.containers.appdomain.cloud:443:169.62.196.238 https://mycluster-<hash>-0000.us-south.containers.appdomain.cloud/
    ```
    {: pre}

    * If everything is configured correctly, you get back the expected response from your app.
    * If you get an error in response, there might be an error in your app or in a configuration that applies only to this specific ALB. Check your app code, your [Ingress resource configuration files](/docs/openshift?topic=openshift-ingress#public_inside_4), or any other configurations you have applied to only this ALB.

7. After you finish debugging, restore the health check on the ALB pods. Repeat these steps for each ALB pod.
  1. Log in to the ALB pod and remove the `#` from the `server_name`.
    ```
    oc exec -ti <pod_name> -n kube-system -c nginx-ingress -- sed -i -e 's*#server_name*server_name*g' /etc/nginx/conf.d/kube-system-alb-health.conf
    ```
    {: pre}

  2. Reload the NGINX configuration so that the health check restoration is applied.
    ```
    oc exec -ti <pod_name> -n kube-system -c nginx-ingress -- nginx -s reload
    ```
    {: pre}

9. Now, when you cURL the `albhealth` host to health check the ALB IP, the check returns `healthy`.
    ```
    curl -X GET http://169.62.196.238/ -H "Host: albhealth.mycluster-<hash>-0000.us-south.containers.appdomain.cloud"
    ```
    {: pre}

10. Verify that the ALB IP address has been restored in the DNS registration for your domain by checking the Cloudflare server. Note that the DNS registration might take a few minutes to update.
    ```
    host mycluster-<hash>-0000.us-south.containers.appdomain.cloud ada.ns.cloudflare.com
    ```
    {: pre}

    Example output:
    ```
    mycluster-<hash>-0000.us-south.containers.appdomain.cloud has address 169.46.52.222
    mycluster-<hash>-0000.us-south.containers.appdomain.cloud has address 169.62.196.238
    ```
    {: screen}

<br />


## 3.11 clusters: Ingress application load balancer (ALB) secret issues
{: #cs_albsecret_fails}


<img src="images/icon-version-311.png" alt="Version 3.11 icon" width="30" style="width:30px; border-style: none"/> This troubleshooting topic applies only to OpenShift clusters that run version 3.11.
{: note}


{: tsSymptoms}
After you deploy an Ingress application load balancer (ALB) secret to your cluster by using the `ibmcloud oc alb cert deploy` command, the `Description` field is not updating with the secret name when you view your certificate in {{site.data.keyword.cloudcerts_full_notm}}.

When you list information about the ALB secret, the state says `*_failed`. For example, `create_failed`, `update_failed`, `delete_failed`.

List the ALB secret details (`ibmcloud ks alb cert get`) and view the ALB secret `status` to get more information on the reason for failure.

{: tsResolve}
Review the following reasons why the ALB secret might fail and the corresponding troubleshooting steps:

<table>
<caption>Troubleshooting Ingress application load balancer secrets</caption>
 <thead>
 <th>Why it's happening</th>
 <th>How to fix it</th>
 </thead>
 <tbody>
 <tr>
 <td>The owner of the cluster's API Key does not have the required access roles to download and update certificate data.</td>
 <td>Check with your account Administrator to assign the owner of the cluster's API Key, the following {{site.data.keyword.cloud_notm}} IAM roles:<ul><li>The **Manager** and **Writer** service roles for your {{site.data.keyword.cloudcerts_full_notm}} instance. For more information, see <a href="/docs/certificate-manager?topic=certificate-manager-managing-service-access-roles#managing-service-access-roles">Managing service access</a> for {{site.data.keyword.cloudcerts_short}}.</li><li>The <a href="/docs/containers?topic=containers-users#platform">**Administrator** platform role</a> for the cluster.</li></ul></td>
 </tr>
 <tr>
 <td>The certificate CRN provided at time of create, update, or remove does not belong to the same account as the cluster.</td>
 <td>Check that the certificate CRN you provided is imported to an instance of the {{site.data.keyword.cloudcerts_short}} service that is deployed in the same account as your cluster.</td>
 </tr>
 <tr>
 <td>The certificate CRN provided at time of create is incorrect.</td>
 <td><ol><li>Check the accuracy of the certificate CRN string you provide.</li><li>If the certificate CRN is found to be accurate, then try to update the secret: <code>ibmcloud oc alb cert deploy --update --cluster &lt;cluster_name_or_ID&gt; --secret-name &lt;secret_name&gt; --cert-crn &lt;certificate_CRN&gt;</code></li><li>If this command results in the <code>update_failed</code> status, then remove the secret: <code>ibmcloud oc alb cert rm --cluster &lt;cluster_name_or_ID&gt; --secret-name &lt;secret_name&gt;</code></li><li>Deploy the secret again: <code>ibmcloud oc alb cert deploy --cluster &lt;cluster_name_or_ID&gt; --secret-name &lt;secret_name&gt; --cert-crn &lt;certificate_CRN&gt;</code></li></ol></td>
 </tr>
 <tr>
 <td>The certificate CRN provided at time of update is incorrect.</td>
 <td><ol><li>Check the accuracy of the certificate CRN string you provide.</li><li>If the certificate CRN is found to be accurate, then remove the secret: <code>ibmcloud oc alb cert rm --cluster &lt;cluster_name_or_ID&gt; --secret-name &lt;secret_name&gt;</code></li><li>Deploy the secret again: <code>ibmcloud oc alb cert deploy --cluster &lt;cluster_name_or_ID&gt; --secret-name &lt;secret_name&gt; --cert-crn &lt;certificate_CRN&gt;</code></li><li>Try to update the secret: <code>ibmcloud oc alb cert deploy --update --cluster &lt;cluster_name_or_ID&gt; --secret-name &lt;secret_name&gt; --cert-crn &lt;certificate_CRN&gt;</code></li></ol></td>
 </tr>
 <tr>
 <td>The {{site.data.keyword.cloudcerts_long_notm}} service is experiencing downtime.</td>
 <td>Check that your {{site.data.keyword.cloudcerts_short}} service is up and running.</td>
 </tr>
 <tr>
 <td>Your imported secret has the same name as the IBM-provided Ingress secret.</td>
 <td>Rename your secret. You can check the name of the IBM-provided Ingress secret by running `ibmcloud oc cluster get --cluster <cluster_name_or_ID> | grep Ingress`.</td>
 </tr>
  <tr>
  <td>The description for the certificate is not updated with the secret name when you view the certificate in {{site.data.keyword.cloudcerts_full_notm}}.</td>
  <td>Check whether the length of the certificate description reached the <a href="/apidocs/certificate-manager#update-a-certificate-s-metadata">upper limit of 1024 characters</a>.</td>
  </tr>
 </tbody></table>

<br />


## 3.11 clusters: ALB does not deploy in a zone
{: #cs_subnet_limit}


<img src="images/icon-version-311.png" alt="Version 3.11 icon" width="30" style="width:30px; border-style: none"/> This troubleshooting topic applies only to OpenShift clusters that run version 3.11.
{: note}


{: tsSymptoms}
When you have a multizone cluster and run `ibmcloud oc alb ls --cluster <cluster>`, no ALB is deployed in a zone. For example, if you have worker nodes in 3 zones, you might see an output similar to the following in which a public ALB did not deploy to the third zone.
```
ALB ID                                            Enabled    Status     Type      ALB IP           Zone    Build                          ALB VLAN ID   NLB Version
private-cr96039a75fddb4ad1a09ced6699c88888-alb1   false      disabled   private   -                dal10   ingress:411/ingress-auth:315   2294021       -
private-cr96039a75fddb4ad1a09ced6699c88888-alb2   false      disabled   private   -                dal12   ingress:411/ingress-auth:315   2234947       -
private-cr96039a75fddb4ad1a09ced6699c88888-alb3   false      disabled   private   -                dal13   ingress:411/ingress-auth:315   2234943       -
public-cr96039a75fddb4ad1a09ced6699c88888-alb1    true       enabled    public    169.xx.xxx.xxx   dal10   ingress:411/ingress-auth:315   2294019       -
public-cr96039a75fddb4ad1a09ced6699c88888-alb2    true       enabled    public    169.xx.xxx.xxx   dal12   ingress:411/ingress-auth:315   2234945       -
```
{: screen}

{: tsCauses}
In standard clusters, the first time that you create a cluster in a zone, a public VLAN and a private VLAN in that zone are automatically provisioned for you in your IBM Cloud infrastructure account. In that zone, 1 public portable subnet is requested on the public VLAN that you specify and 1 private portable subnet is requested on the private VLAN that you specify. For Red Hat OpenShift on IBM Cloud, VLANs have a limit of 40 subnets. If the cluster's VLAN in a zone already reached that limit, the **Ingress Subdomain** fails to provision and the public Ingress ALB for that zone fails to provision.

To view how many subnets a VLAN has:
1.  From the [IBM Cloud infrastructure console](https://cloud.ibm.com/classic?), select **Network** > **IP Management** > **VLANs**.
2.  Click the **VLAN Number** of the VLAN that you used to create your cluster. Review the **Subnets** section to see whether 40 or more subnets exist.

{: tsResolve}
Option 1: If you need a new VLAN, order one by [contacting {{site.data.keyword.cloud_notm}} support](/docs/vlans?topic=vlans-ordering-premium-vlans#ordering-premium-vlans). Then, [create a cluster](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_cluster_create) that uses this new VLAN.

Option 2: If you have another VLAN that is available, you can [set up VLAN spanning](/docs/vlans?topic=vlans-vlan-spanning#vlan-spanning) in your existing cluster. After, you can add new worker nodes to the cluster that use the other VLAN with available subnets. To check if VLAN spanning is already enabled, use the `ibmcloud oc vlan spanning get --region <region>` [command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_vlan_spanning_get).

Option 3: If you are not using all the subnets in the VLAN, you can reuse subnets on the VLAN by adding them to your cluster.
1. Check that the subnet that you want to use is available.
  <p class="note">The infrastructure account that you use might be shared across multiple {{site.data.keyword.cloud_notm}} accounts. In this case, even if you run the `ibmcloud oc subnets` command to see subnets with **Bound Clusters**, you can see information only for your clusters. Check with the infrastructure account owner to make sure that the subnets are available and not in use by any other account or team.</p>

2. Use the [`ibmcloud oc cluster subnet add` command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_cluster_subnet_add) to make an existing subnet available to your cluster.

3. Verify that the subnet was successfully created and added to your cluster. The subnet CIDR is listed in the **Subnet VLANs** section.
    ```
    ibmcloud oc cluster get --show-resources <cluster_name_or_ID>
    ```
    {: pre}

    In this example output, a second subnet was added to the `2234945` public VLAN:
    ```
    Subnet VLANs
    VLAN ID   Subnet CIDR          Public   User-managed
    2234947   10.xxx.xx.xxx/29     false    false
    2234945   169.xx.xxx.xxx/29    true     false
    2234945   169.xx.xxx.xxx/29    true     false
    ```
    {: screen}

4. Verify that the portable IP addresses from the subnet that you added are used for the ALBs in your cluster. It might take several minutes for the services to use the portable IP addresses from the newly-added subnet.
  * **No Ingress subdomain**: Run `ibmcloud oc cluster get --cluster <cluster>` to verify that the **Ingress Subdomain** is populated.
  * **An ALB does not deploy in a zone**: Run `ibmcloud oc alb ls --cluster <cluster>` to verify that the missing ALB is deployed.

<br />


## 3.11 clusters: Source IP preservation fails when using tainted nodes
{: #cs_source_ip_fails}


<img src="images/icon-version-311.png" alt="Version 3.11 icon" width="30" style="width:30px; border-style: none"/> This troubleshooting topic applies only to OpenShift clusters that run version 3.11.
{: note}


{: tsSymptoms}
You enabled source IP preservation for an [Ingress ALB](/docs/openshift?topic=openshift-ingress-settings#preserve_source_ip) service by changing `externalTrafficPolicy` to `Local` in the service's configuration file. However, no traffic reaches the back-end service for your app.

{: tsCauses}
When you enable source IP preservation for Ingress ALB services, the source IP address of the client request is preserved. The service forwards traffic to app pods on the same worker node only to ensure that the request packet's IP address isn't changed. Typically, Ingress ALB service pods are deployed to the same worker nodes that the app pods are deployed to. However, some situations exist where the service pods and app pods might not be scheduled onto the same worker node. If you use [Kubernetes taints](https://kubernetes.io/docs/concepts/configuration/taint-and-toleration/){: external} on worker nodes, any pods that don't have a taint toleration are prevented from running on the tainted worker nodes. Source IP preservation might not be working based on the type of taint you used:

* **Edge node taints**: You [added the `dedicated=edge` label](/docs/openshift?topic=openshift-edge#edge_nodes) to two or more worker nodes on each public VLAN in your cluster to ensure that Ingress pods deploy to those worker nodes only. Then, you also [tainted those edge nodes](/docs/openshift?topic=openshift-edge#edge_workloads) to prevent any other workloads from running on edge nodes. However, you didn't add an edge node affinity rule and toleration to your app deployment. Your app pods can't be scheduled on the same tainted nodes as the service pods, and no traffic reaches the back-end service for your app.

* **Custom taints**: You used custom taints on several nodes so that only app pods with that taint toleration can deploy to those nodes. You added affinity rules and tolerations to the deployments of your app and Ingress service so that their pods deploy to only those nodes. However, `ibm-cloud-provider-ip` `keepalived` pods that are automatically created in the `ibm-system` namespace ensure that the ALB pods and the app pods are always scheduled onto the same worker node. These `keepalived` pods don't have the tolerations for the custom taints that you used. They can't be scheduled on the same tainted nodes that your app pods are running on, and no traffic reaches the back-end service for your app.

{: tsResolve}
Resolve the issue by choosing one of the following options:

* **Edge node taints**: To ensure that your ALB and app pods deploy to tainted edge nodes, [add edge node affinity rules and tolerations to your app deployment](/docs/openshift?topic=openshift-loadbalancer#lb_edge_nodes). Ingress ALB pods have these affinity rules and tolerations by default.

* **Custom taints**: Remove custom taints that the `keepalived` pods don't have tolerations for. Instead, you can [label worker nodes as edge nodes, and then taint those edge nodes](/docs/openshift?topic=openshift-edge).

If you complete one of the above options but the `keepalived` pods are still not scheduled, you can get more information about the `keepalived` pods:

1. Get the `keepalived` pods.
    ```
    oc get pods -n ibm-system
    ```
    {: pre}

2. In the output, look for `ibm-cloud-provider-ip` pods that have a **Status** of `Pending`. Example:
    ```
    ibm-cloud-provider-ip-169-61-XX-XX-55967b5b8c-7zv9t     0/1       Pending   0          2m        <none>          <none>
    ibm-cloud-provider-ip-169-61-XX-XX-55967b5b8c-8ptvg     0/1       Pending   0          2m        <none>          <none>
    ```
    {:screen}

3. Describe each `keepalived` pod and look for the **Events** section. Address any error or warning messages that are listed.
    ```
    oc describe pod ibm-cloud-provider-ip-169-61-XX-XX-55967b5b8c-7zv9t -n ibm-system
    ```
    {: pre}

<br />


## Connection via WebSocket closes after 60 seconds
{: #cs_ingress_websocket}

{: tsSymptoms}
Your Ingress service exposes an app that uses a WebSocket. However, the connection between a client and your WebSocket app closes when no traffic is sent between them for 60 seconds.

{: tsCauses}
The connection to your WebSocket app might drop after 60 seconds of inactivity for one of the following reasons:

* Your Internet connection has a proxy or firewall that doesn't tolerate long connections.
* A timeout in the ALB to the WebSocket app terminates the connection.

{: tsResolve}
To prevent the connection from closing after 60 seconds of inactivity:

1. If you connect to your WebSocket app through a proxy or firewall, make sure the proxy or firewall isn't configured to automatically terminate long connections.

2. To keep the connection alive, you can increase the value of the timeout or set up a heartbeat in your app.
<dl><dt>Change the timeout</dt>
<dd>Increase the value of the `proxy-read-timeout` in your ALB configuration. For example, to change the timeout from `60s` to a larger value like `300s`, add this [annotation](/docs/openshift?topic=openshift-ingress_annotation#connection) to your Ingress resource file: `ingress.bluemix.net/proxy-read-timeout: "serviceName=<service_name> timeout=300s"`. The timeout is changed for all public ALBs in your cluster.</dd>
<dt>Set up a heartbeat</dt>
<dd>If you don't want to change the ALB's default read timeout value, set up a heartbeat in your WebSocket app. When you set up a heartbeat protocol by using a framework like [WAMP ![External link icon](../icons/launch-glyph.svg "External link icon")](https://wamp-proto.org/), the app's upstream server periodically sends a "ping" message on a timed interval and the client responds with a "pong" message. Set the heartbeat interval to 58 seconds or less so that the "ping/pong" traffic keeps the connection open before the 60-second timeout is enforced.</dd></dl>

<br />


## Feedback, questions, and support
{: #getting_help}

Still having issues with your cluster? Review different ways to get help and support for your Red Hat OpenShift on IBM Cloud clusters. For any questions or feedback, post in Slack.
{: shortdesc}

**General ways to resolve issues**<br>
1. Keep your cluster environment up to date.
   * Check monthly for available security and operating system patches to [update your worker nodes](/docs/openshift?topic=openshift-update#worker_node).
   * [Update your cluster](/docs/openshift?topic=openshift-update#master) to the latest default version for [OpenShift](/docs/openshift?topic=openshift-openshift_versions).
2. Make sure that your command line tools are up to date.
   * In the terminal, you are notified when updates to the `ibmcloud` CLI and plug-ins are available. Be sure to keep your CLI up-to-date so that you can use all available commands and flags.
   * Make sure that [your `oc` CLI](/docs/openshift?topic=openshift-openshift-cli#kubectl) client matches the same Kubernetes version as your cluster server. [Kubernetes does not support](https://kubernetes.io/docs/setup/release/version-skew-policy/){: external} `oc` client versions that are 2 or more versions apart from the server version (n +/- 2).
<br>

**Reviewing issues and status**<br>
1. To see whether {{site.data.keyword.cloud_notm}} is available, [check the {{site.data.keyword.cloud_notm}} status page](https://cloud.ibm.com/status?selected=status){: external}.
2. Filter for the **Kubernetes Service** component.
<br>

**Feedback and questions**<br>
1. Post in the {{site.data.keyword.containershort}} Slack.
   * If you are an external user, post in the [#openshift](https://ibm-cloud-success.slack.com/messages/CKCJLJCH4){: external} channel.
   * If you are an IBMer, use the [#iks-openshift-users](https://ibm-argonauts.slack.com/messages/CJH0UPN2D){: external} channel.<p class="tip">If you do not use an IBMid for your {{site.data.keyword.cloud_notm}} account, [request an invitation](https://cloud.ibm.com/kubernetes/slack){: external} to this Slack.</p>
2. Review forums such as OpenShift help, Stack Overflow, and IBM Developer to see whether other users ran into the same issue. When you use the forums to ask a question, tag your question so that it is seen by the {{site.data.keyword.cloud_notm}} development teams.
   * If you have technical questions about developing or deploying clusters or apps with Red Hat OpenShift on IBM Cloud, post your question on [Stack Overflow](https://stackoverflow.com/questions/tagged/ibm-cloud+containers){: external} and tag your question with `ibm-cloud`, `containers`, and `openshift`.
   * For questions about the service and getting started instructions, use the [IBM Developer Answers](https://developer.ibm.com/answers/topics/containers/?smartspace=bluemix){: external} forum. Include the `ibm-cloud` and `containers` tags.
   * See [Getting help](/docs/get-support?topic=get-support-getting-customer-support#using-avatar) for more details about using the forums.
<br>

**Getting help**<br>
1.  Contact IBM Support by opening a case. To learn about opening an IBM support case, or about support levels and case severities, see [Contacting support](/docs/get-support?topic=get-support-getting-customer-support).
2.  In your support case, for **Category**, select **Containers**.
3.  For the **Offering**, select your OpenShift cluster.<p class="tip">When you report an issue, include your cluster ID. To get your cluster ID, run `ibmcloud oc cluster ls`. 3.11 clusters only: You can also use the [{{site.data.keyword.containerlong_notm}} Diagnostics and Debug Tool](/docs/openshift?topic=openshift-cs_troubleshoot#debug_utility) to gather and export pertinent information from your cluster to share with IBM Support.</p>


