---

copyright:
  years: 2014, 2021
lastupdated: "2021-10-04"

keywords: openshift, roks, rhoks, rhos

subcollection: openshift
content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

  

# Debugging Ingress
{: #ingress-debug-roks4}
{: troubleshoot}
{: support}

**Infrastructure provider**:
* <img src="images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Classic
* <img src="images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> VPC


You exposed your app by creating an Ingress resource for your app in your cluster. However, when you try to connect to your app through the Ingress subdomain or the IP address of the Ingress controller's router, the connection fails or times out.
{: tsSymptoms}


The steps in the following sections can help you debug your Ingress setup.
{: tsResolve}

Before you begin, ensure you have the following [{{site.data.keyword.cloud_notm}} IAM access policies](/docs/openshift?topic=openshift-users) for {{site.data.keyword.containerlong_notm}}:
    - **Editor** or **Administrator** platform access role for the cluster
    - **Writer** or **Manager** service access role

Seeing an **Application is not available** page when you try to access your app's subdomain? [Check your app deployment and Ingress resource configuration](#app-debug-ingress-43). Seeing a **Connection timeout** page? [Check the health of the Ingress controller's router pods](#errors-43).
{: tip}

## Step 1: Check your app deployment and Ingress resource configuration
{: #app-debug-ingress-43}

Start by checking for errors in your app deployment and the Ingress resource deployment. Error messages in your deployments can help you find the root causes for failures and further debug your Ingress setup in the next sections.
{: shortdesc}

1. Before you debug Ingress, first check out [Debugging app deployments](/docs/openshift?topic=openshift-debug_apps). Ingress issues are often caused by underlying issues in your app deployment or in the `ClusterIP` service that exposes your app. For example, your app label and service selector might not match, or your app and service target ports might not match.

2. Check your Ingress resource deployment and look for warnings or error messages.
    ```sh
    oc describe ingress <ingress_resource_name>
    ```
    {: pre}

    In the **Events** section of the output, you might see warning messages about invalid values in your Ingress resource or in certain annotations that you used. Check the [Ingress resource configuration documentation](/docs/openshift?topic=openshift-ingress-roks4#ingress-roks4-public-3). For annotations, note that the {{site.data.keyword.containerlong_notm}} annotations (`ingress.bluemix.net/<annotation>`) and NGINX annotations (`nginx.ingress.kubernetes.io/<annotation>`) are not supported for the router or the Ingress resource in {{site.data.keyword.openshiftshort}} version 4. If you want to customize routing rules for apps in a cluster that runs {{site.data.keyword.openshiftshort}} version 4, you can use [route-specific HAProxy annotations](https://docs.openshift.com/container-platform/4.7/networking/routes/route-configuration.html#nw-route-specific-annotations_route-configuration){: external}, which are in the format `haproxy.router.openshift.io/<annotation>` or `router.openshift.io/<annotation>`.

    ```sh
    NAME:             myingress
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
    ```sh
    oc get ingress -o yaml
    ```
    {: pre}

    1. Ensure that you define a host in only one Ingress resource. If one host is defined in multiple Ingress resources, the Ingress controller might not forward traffic properly and you might experience errors.

    2. Check that the subdomain and TLS certificate are correct. To find the IBM provided Ingress subdomain and TLS certificate, run `ibmcloud oc cluster get --cluster <cluster_name_or_ID>`.

    3. Make sure that your app listens on the same path that is configured in the **path** section of your Ingress.

    4. Edit your resource configuration YAML as needed. When you close the editor, your changes are saved and automatically applied.
        ```sh
        oc edit ingress <myingressresource>
        ```
        {: pre}

## Step 2: Run Ingress tests in the Diagnostics and Debug Tool
{: #debug-tool-43}

Use the {{site.data.keyword.containerlong_notm}} Diagnostics and Debug Tool to run Ingress tests and gather pertinent Ingress information from your cluster. To use the debug tool, you can enable the add-on in your cluster.
{: shortdesc}

1. In the [{{site.data.keyword.openshiftshort}} clusters console](https://cloud.ibm.com/kubernetes/clusters?platformType=openshift){: external}, click the name of the cluster where you want to install the debug tool add-on.

2. Click the **Add-ons** tab.

3. On the Diagnostics and Debug Tool card, click **Install**.

4. In the dialog box, click **Install**. Note that it can take a few minutes for the add-on to be installed. <p class="tip">To resolve some common issues that you might encounter during the add-on deployment, see [Reviewing add-on state and statuses](/docs/openshift?topic=openshift-debug_addons).</p>

5. On the Diagnostics and Debug Tool card, click **Dashboard**.

5. In the debug tool dashboard, select the **ingress** group of tests. Some tests check for potential warnings, errors, or issues, and some tests only gather information that you can reference while you troubleshoot. For more information about the function of each test, click the information icon next to the test's name.

6. Click **Run**.

7. Check the results of each test.
    * If any test fails, click the information icon next to the test's name in the left-hand column for information about how to resolve the issue.
    * You can also use the results of tests that only gather information while you debug your Ingress service in the following sections.

## Step 3: Check the health of the Ingress controller's router
{: #errors-43}

Verify that the Ingress operator and the Ingress controller's router are healthy. Ingress controllers are managed by the Ingress operator. The router forwards requests to the pods for that app only according to the rules defined in the Ingress resource and implemented by the Ingress controller.
{: shortdesc}

1. Check the status of your Ingress operator pods.
    1. Get the Ingress operator pods that are running in your cluster.
        ```sh
        oc get pods -n openshift-ingress-operator
        ```
        {: pre}

    2. Make sure that all pods are running by checking the **STATUS** column.

    3. If a pod does not have a `Running` status, you can delete the pod to restart it.
        ```sh
        oc delete pod <pod> -n openshift-ingress-operator
        ```
        {: pre}

    4. Get the logs for the Ingress controller and look for error messages in the logs.
        ```sh
        oc logs deployments/ingress-operator -n openshift-ingress-operator -c ingress-operator
        ```
        {: pre}

2. Check the status and logs of your Ingress controller's router pods.
    1. Get the Ingress controller's router pods that are running in your cluster.
        ```sh
        oc get pods -n openshift-ingress
        ```
        {: pre}

    2. Make sure that all `router-default` pods and pods for routers in any other zone are running by checking the **STATUS** column. If you have a multizone cluster, note that the router service in the first zone where you have workers nodes is always named `router-default`, and router services in the zones that you subsequently add to your cluster have names such as `router-dal12`.

    3. If a pod does not have a `Running` status, you can delete the pod to restart it.
        ```sh
        oc delete pod <pod> -n openshift-ingress
        ```
        {: pre}

    4. Get the logs for each pod and look for error messages in the logs. 
        ```sh
        oc logs <pod> -n openshift-ingress
        ```
        {: pre}

3. Check for events and errors on each router service.
    1. List the services in the `openshift-ingress` namespace.
        ```sh
        oc get svc -n openshift-ingress
        ```
        {: pre}

        Example output for a multizone cluster with worker nodes in `dal10` and `dal13`:
        ```sh
        NAME                                         TYPE           CLUSTER-IP      EXTERNAL-IP    PORT(S)                      AGE
        router-dal13                                 LoadBalancer   172.21.47.119   169.XX.XX.XX   80:32318/TCP,443:30915/TCP   26d
        router-default                               LoadBalancer   172.21.47.119   169.XX.XX.XX   80:32637/TCP,443:31719/TCP   26d
        router-internal-default                      ClusterIP      172.21.51.30    <none>         80/TCP,443/TCP,1936/TCP      26d
        ```
        {: screen}

    2. Describe each router service and check for messages in the `Events` section of the output.
        ```sh
        oc describe svc router-default -n openshift-ingress
        ```
        {: pre}

        * For example, in VPC clusters, you might see an error message such as `The VPC load balancer that routes requests to this Kubernetes LoadBalancer service is offline`. For more information, see [VPC clusters: Why can't my app connect via load balancer?](/docs/openshift?topic=openshift-vpc_ts_lb).

## Step 4: Ping the Ingress subdomain and router public IP address
{: #ping-43}

Check the availability of the public IP addresses of the Ingress controller's routers and verify your subdomain mappings. Additionally, ensure that the {{site.data.keyword.openshiftshort}} control plane can access your routers to health check them.
{: shortdesc}

1. Verify that your router services are reachable by the router health check.
    * **Classic**: If you use Calico pre-DNAT network policies or another custom firewall to block incoming traffic to your cluster, you must allow inbound access on port 80 from the {{site.data.keyword.openshiftshort}} control plane and Akamai's IPv4 IP addresses to the IP addresses of your router services so that the {{site.data.keyword.openshiftshort}} control plane can check the health of your routers. For example, if you use Calico policies, [create a Calico pre-DNAT policy](/docs/openshift?topic=openshift-network_policies#isolate_workers) to allow inbound access to your routers from [Akamai's source IP addresses](https://github.com/IBM-Cloud/kube-samples/tree/master/akamai/gtm-liveness-test){: external} that are used to check the health of your routers on port 80 and the [control plane subnets for the region where your cluster is located](https://github.com/IBM-Cloud/kube-samples/tree/master/control-plane-ips){: external}. Continue to the next step to get the router service IP addresses.<p class="important">From 07 to 31 July 2021, the DNS provider is changed from Cloudflare to Akamai for all `containers.appdomain.cloud`, `containers.mybluemix.net`, and `containers.cloud.ibm.com` domains for all clusters in {{site.data.keyword.openshiftlong_notm}}. If you currently allow inbound traffic to your classic cluster from the Cloudflare source IP addresses, you must also allow inbound traffic from the [Akamai source IP addresses](https://github.com/IBM-Cloud/kube-samples/tree/master/akamai/gtm-liveness-test){: external} before 07 July. After the migration completes on 31 July, you can remove the Cloudflare IP address rules. For more information, see the [announcement](https://cloud.ibm.com/notifications?selected=1621697674798){: external}.</p>
    * **VPC**: If you set up [VPC security groups](/docs/openshift?topic=openshift-vpc-network-policy#security_groups) or [VPC access control lists (ACLs)](/docs/openshift?topic=openshift-vpc-network-policy#acls) to secure your cluster network, ensure that you create the rules to allow the necessary traffic from the {{site.data.keyword.openshiftshort}} control plane IP addresses. Alternatively, to allow the inbound traffic for router healthchecks, you can create one rule to allow all incoming traffic on port 80.

2. Get the external IP addresses that the router services are listening on. If you have a multizone cluster, note that the router service in the first zone where you have workers nodes is always named `router-default`, and router services in the zones that you subsequently add to your cluster have names such as `router-dal12`. In VPC clusters, the external IP addresses are behind a hostname that is assigned by the VPC load balancer, such as `aabb1122-us-south.lb.appdomain.cloud`.
    ```sh
    oc get svc -n openshift-ingress
    ```
    {: pre}

    Example output for a classic multizone cluster with worker nodes in `dal10` and `dal13`:
    ```sh
    NAME                                         TYPE           CLUSTER-IP      EXTERNAL-IP    PORT(S)                      AGE
    router-dal13                                 LoadBalancer   172.21.47.119   169.XX.XX.XX   80:32318/TCP,443:30915/TCP   26d
    router-default                               LoadBalancer   172.21.47.119   169.XX.XX.XX   80:32637/TCP,443:31719/TCP   26d
    router-internal-default                      ClusterIP      172.21.51.30    <none>         80/TCP,443/TCP,1936/TCP      26d
    ```
    {: screen}

    If a router has no external IP address (classic) or hostname (VPC), see [Version 4: Why doesn't the router for the Ingress controller deploy in a zone?](/docs/openshift?topic=openshift-cs_subnet_limit_43).
    {: note}

3. Check the health of your router pods (classic) or hostname (VPC).
    - Classic clusters: [Check the status of your router pods](#errors-43).
    - VPC clusters: Router services in multizone clusters are created with a `/healthz` path so that you can check the health of each service IP address. The following HTTP cURL command uses the `/healthz` path, which returns the `ok` status for a healthy IP.
    ```sh
    curl -X GET http://<router_svc_IP_or_hostname>/healthz -H "Host:router-default.<ingress_subdomain>"
    ```
    {: pre}

    If one or more of the IP addresses does not return `ok`, [check the status of your router pods](#errors-43).

4. Get the IBM-provided Ingress subdomain.
    ```sh
    ibmcloud oc cluster get --cluster <cluster_name_or_ID> | grep Ingress
    ```
    {: pre}

    Example output

    ```sh
    Ingress Subdomain:      mycluster-<hash>-0000.us-south.containers.appdomain.cloud
    Ingress Secret:         mycluster-<hash>-0000
    ```
    {: screen}

5. Ensure that the router IP address is registered with your cluster's IBM-provided Ingress subdomain. For example, in a multizone cluster, the public router IP in each zone where you have worker nodes must be registered under the same subdomain.
    ```
    host <ingress_subdomain>
    ```
    {: pre}

    Example output

    ```sh
    mycluster-<hash>-0000.us-south.containers.appdomain.cloud has address 169.XX.XX.XXX
    mycluster-<hash>-0000.us-south.containers.appdomain.cloud has address 169.XX.XXX.XX
    ```
    {: screen}

6. If you use a custom domain, verify that you used your DNS provider to map the custom domain to the IBM-provided subdomain or the router's public IP address.
    * **IBM-provided subdomain CNAME**: Check that your custom domain is mapped to the cluster's IBM-provided subdomain in the Canonical Name record (CNAME).
        ```
        host www.my-domain.com
        ```
        {: pre}

        Example output
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

        Example output
        ```
        www.my-domain.com has address 169.XX.XX.XXX
        www.my-domain.com has address 169.XX.XX.XXX
        ```
        {: screen}






