---

copyright:
  years: 2014, 2021
lastupdated: "2021-10-04"

keywords: openshift, roks, rhoks, rhos

subcollection: openshift
content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

  

# Why does no Ingress subdomain exist after cluster creation?
{: #ingress_subdomain}

**Infrastructure provider**:
* <img src="images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Classic
* <img src="images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> VPC


You create a cluster and run `ibmcloud oc cluster get --cluster <cluster>` to check its status. The cluster **State** is `normal`, but the **Ingress Subdomain** and **Ingress Secret** are not available.
{: tsSymptoms}


Even if the cluster is in a `normal` state, the Ingress subdomain and secret might still be in progress. The Ingress subdomain and secret creation follows a process that might take more than 15 minutes to complete:
{: tsCauses}

<img src="images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> **Classic clusters**:

1. When worker nodes are fully deployed and ready on the VLANs, a portable public and a portable private subnet for the VLANs are ordered.
2. After the portable subnet orders are successfully fulfilled, the `ibm-cloud-provider-vlan-ip-config` config map is updated with the portable public and portable private IP addresses.
3. When the `ibm-cloud-provider-vlan-ip-config` config map is updated, the router for the Ingress controller is triggered for creation.
4. A load balancer service that exposes the ALB or router is created and assigned an IP address.
5. The load balancer IP address is used to register the Ingress subdomain in Akamai. Akamai might have latency during the registration process.

If you create a classic cluster that is connected to private VLANs only, or if you create a free cluster, no Ingress subdomain or secret are created.
{: note}

<img src="images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> **VPC clusters**:

1. When you create a VPC cluster, one public and one private VPC load balancer are automatically created outside of your cluster in your VPC.
2. One public router per zone is triggered for creation.
3. A load balancer service that exposes the router is created and assigned a hostname.
4. The load balancer hostname is used to register the Ingress subdomain in Akamai. Akamai might have latency during the registration process.

Creating a cluster after deleting a cluster the same or similar name? See [No Ingress subdomain exists after you create clusters of the same or similar name](/docs/openshift?topic=openshift-cs_rate_limit) instead.
{: tip}


Typically, after the cluster is ready, the Ingress subdomain and secret are created after 15 minutes. If the Ingress subdomain and secret are still unavailable after your cluster is in a `normal` state for more than 15 minutes, you can check the progress of the creation process by following these steps:
{: tsResolve}

1. [Log in to your cluster](/docs/openshift?topic=openshift-access_cluster). Because the subdomain is not available, the {{site.data.keyword.openshiftshort}} console cannot open. Instead, you can set the cluster context with the `--admin` flag through the CLI.
    ```sh
    ibmcloud oc cluster config -c <cluster_name_or_ID> --admin
    ```
    {: pre}

2. Verify that the worker nodes have a **State** of `normal` and a **Status** of `Ready`. After you create the cluster, it can take up to 20 minutes for the worker nodes to be ready.
    ```sh
    ibmcloud oc worker ls -c <cluster_name_or_ID>
    ```
    {: pre}

    Example output

    ```sh
    ID                                                     Public IP         Private IP      Flavor              State     Status   Zone    Version
    kube-blrs3b1d0p0p2f7haq0g-mycluster-default-000001f7   169.xx.xxx.xxx    10.xxx.xx.xxx   u3c.2x4.encrypted   deployed   Ready    dal10   1.21.5
    ```
    {: screen}

3. Verify that the prerequisite steps for your ALB creation are completed.
    * <img src="images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> **Classic clusters**: Get the details of the `ibm-cloud-provider-vlan-ip-config` config map.
    ```sh
    oc describe cm ibm-cloud-provider-vlan-ip-config -n kube-system
    ```
    {: pre}

    * If the config map shows IP addresses, continue to the next step.
    * If the **Events** section shows a warning message similar to `ErrorSubnetLimitReached: There are already the maximum number of subnets permitted in this VLAN`, see the [VLAN capacity troubleshooting topic](/docs/openshift?topic=openshift-cs_subnet_limit_43).

    Example output of a config map populated with IP addresses:
    ```sh
    NAME:         ibm-cloud-provider-vlan-ip-config
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

    * <img src="images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> **VPC clusters**: Verify that the VPC load balancer for your routers exists. In the output, look for the VPC load balancer **Name** that starts with `kube-<cluster_ID>`. If you did not install the `infrastructure-service` plug-in, install it by running `ibmcloud plugin install infrastructure-service`.
    ```
    ibmcloud is load-balancers
    ```
    {: pre}

    <p class="note">Even though the VPC load balancer is listed, its DNS entry might still be registering. When a VPC load balancer is created, the hostname is registered through a public DNS. In some cases, it can take several minutes for this DNS entry to be replicated to the specific DNS that your client is using.</p>

4. Verify that the router for the Ingress controller is successfully created.
    1. Check whether a router deployment exists for your cluster.
        * If a router deployment is listed, continue to the next step.
        * If no router deployment is created after several minutes, [review ways to get help](/docs/openshift?topic=openshift-get-help).

        ```sh
        oc get deployment -n openshift-ingress
        ```
        {: pre}

        Example output
        ```sh
        NAME             READY   UP-TO-DATE   AVAILABLE   AGE
        router-default   2/2     2            2           26m
        ```
        {: screen}

    2. Check whether the router's load balancer service exists and is assigned a public external IP address (classic clusters) or a hostname (VPC clusters).
        * If a service that is named `router-default` is listed and is assigned an IP address (classic clusters) or a hostname (VPC clusters), continue to the next step.
        * If no `router-default` service is created after several minutes, [review ways to get help](/docs/openshift?topic=openshift-get-help).

        ```sh
        oc get svc -n openshift-ingress
        ```
        {: pre}

        Example output
        ```sh
        NAME                      TYPE           CLUSTER-IP      EXTERNAL-IP    PORT(S)                      AGE
        router-default            LoadBalancer   172.21.47.119   169.XX.XX.XX   80:31182/TCP,443:31154/TCP   27m
        router-internal-default   ClusterIP      172.21.51.30    <none>         80/TCP,443/TCP,1936/TCP      26m
        ```
        {: screen}

5. Check again whether the Ingress subdomain and secret are created. If they are not available, but you verified that all of the components in steps 1 - 3 exist, [review ways to get help](/docs/openshift?topic=openshift-get-help).
    ```sh
    ibmcloud oc cluster get -c <cluster_name_or_ID>
    ```
    {: pre}






