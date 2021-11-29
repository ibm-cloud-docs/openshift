---

copyright:
  years: 2014, 2021
lastupdated: "2021-11-29"

keywords: openshift

subcollection: openshift
content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Classic clusters: Why doesn't the Ingress controller deploy in a zone?
{: #cs_subnet_limit_43}

**Infrastructure provider and version**:
* ![Classic infrastructure provider icon.](images/icon-classic-2.svg) Classic
* <img src="images/icon-version-43.png" alt="Version 4 icon" width="30" style="width:30px; border-style: none"/> {{site.data.keyword.openshiftshort}} version 4


When you run `oc get svc -n openshift-ingress`, one or more zones has no public Ingress controller.
{: tsSymptoms}

* No `router-default` service is deployed, or the service might not have an external IP address assigned. For example, in a single-zone cluster, you might see the following:
    ```sh
    NAME                                         TYPE           CLUSTER-IP      EXTERNAL-IP    PORT(S)                      AGE
    router-default                               LoadBalancer   172.21.47.119   <none>         80:32637/TCP,443:31719/TCP   26m
    router-internal-default                      ClusterIP      172.21.51.30    <none>         80/TCP,443/TCP,1936/TCP      26m
    ```
    {: screen}

* If you have a multizone cluster, one zone has no Ingress controller service. For example, in a multizone cluster that has worker nodes in `dal10`, `dal12`, and `dal13`, you might see a `router-default` service for `dal10` and a `router-dal12` for `dal12`, but no `router-dal13` for `dal13`. Note that the Ingress controller service in the first zone where you have workers nodes is always named `router-default`, and Ingress controller services in the zones that you subsequently add to your cluster have names such as `router-dal12`. You might also see that one zone has no Ingress controller service, but another zone has two or more Ingress controller services.
    ```sh
    NAME                                         TYPE           CLUSTER-IP      EXTERNAL-IP    PORT(S)                      AGE
    router-default                               LoadBalancer   172.21.47.119   169.XX.XX.XX   80:32637/TCP,443:31719/TCP   26m
    router-dal12                                 LoadBalancer   172.21.47.119   169.XX.XX.XX   80:32637/TCP,443:31719/TCP   26m
    router-internal-default                      ClusterIP      172.21.51.30    <none>         80/TCP,443/TCP,1936/TCP      26m
    ```
    {: screen}


Router services might not deploy for one of the following reasons:
{: tsCauses}

* **If no Ingress controller services are deployed or Ingress controller services are not assigned an external IP address**: In standard clusters, the first time that you create a cluster in a zone, a public VLAN and a private VLAN in that zone are automatically provisioned for you in your IBM Cloud infrastructure account. In that zone, 1 public portable subnet is requested on the public VLAN that you specify and 1 private portable subnet is requested on the private VLAN that you specify. For {{site.data.keyword.openshiftlong_notm}}, VLANs have a limit of 40 subnets. If the cluster's VLAN in a zone already reached that limit, the **Ingress Subdomain** fails to provision and the default public Ingress controller for the Ingress controller fails to provision. To view how many subnets a VLAN has, from the [IBM Cloud infrastructure console](https://cloud.ibm.com/classic?), select **Network** > **IP Management** > **VLANs**. Click the **VLAN Number** of the VLAN that you used to create your cluster. Review the **Subnets** section to see whether 40 or more subnets exist.

* **If one zone has no Ingress controller service**: When your Ingress controller services are created, they are automatically spread across the zones in your cluster. If the network for the first zone that your cluster was created with is not ready when the Ingress controller services are created, the Ingress controller service for that zone might be placed in a different zone. Two Ingress controller services might be created in one zone, and no Ingress controller service is created in the initial zone.

Resolve VLAN issues for Ingress controller services that have no IP address, or multizone Ingress controller service issues for zones with no Ingress controller services.
{: tsResolve}


## Resolving VLAN issues
{: #resolve_vlan}

To resolve VLAN issues for Ingress controller services that have no IP address:
{: shortdesc}

Option 1: If you need a new VLAN, order one by [contacting {{site.data.keyword.cloud_notm}} support](/docs/vlans?topic=vlans-ordering-premium-vlans#ordering-premium-vlans). Then, [create a cluster](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_cluster_create) that uses this new VLAN.

Option 2: If you have another VLAN that is available, you can [set up VLAN spanning](/docs/vlans?topic=vlans-vlan-spanning#vlan-spanning) in your existing cluster. To check if VLAN spanning is already enabled, use the `ibmcloud oc vlan spanning get --region <region>` [command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_vlan_spanning_get). Then, you can add new worker nodes to the cluster that use the other VLAN with available subnets. Create at least 2 worker nodes per zone. Now, IP addresses are available so that the Ingress controllers can automatically deploy.

Option 3: If you are not using all the subnets in the VLAN, you can reuse subnets on the VLAN by adding them to your cluster.
1. Check that the subnet that you want to use is available.
    <p class="note">The infrastructure account that you use might be shared across multiple {{site.data.keyword.cloud_notm}} accounts. In this case, even if you run the `ibmcloud oc subnets` command to see subnets with **Bound Clusters**, you can see information only for your clusters. Check with the infrastructure account owner to make sure that the subnets are available and not in use by any other account or team.</p>

2. Use the [`ibmcloud oc cluster subnet add` command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_cluster_subnet_add) to make an existing subnet available to your cluster.

3. Verify that the subnet was successfully created and added to your cluster. The subnet CIDR is listed in the **Subnet VLANs** section.
    ```sh
    ibmcloud oc cluster get --cluster <cluster_name> --show-resources
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

4. Verify that the portable IP addresses from the subnet that you added are used for the Ingress controller in your cluster. It might take several minutes for the services to use the portable IP addresses from the newly-added subnet.
    * **No Ingress subdomain**: Run `ibmcloud oc cluster get --cluster <cluster>` to verify that the **Ingress Subdomain** is populated.
    * **A Ingress controller does not deploy in a zone**: Run `oc get svc -n openshift-ingress` to verify that the missing Ingress controller is deployed with an external IP address.


## Resolving multizone Ingress controller service deployment issues
{: #resolve_mzr_router}

Create a Ingress controller service in the zone where a Ingress controller service did not deploy. If a duplicate Ingress controller service was initially created in a different zone, do **not** delete that Ingress controller service.
{: shortdesc}

1. Create a YAML for a Ingress controller service in the zone where a Ingress controller service did not deploy. Name the Ingress controller service `router-<zone>`.
    ```yaml
     apiVersion: v1
     kind: Service
     metadata:
       annotations:
         service.kubernetes.io/ibm-load-balancer-cloud-provider-ip-type: public
       finalizers:
       - service.kubernetes.io/load-balancer-cleanup
       labels:
         app: router
         ingresscontroller.operator.openshift.io/owning-ingresscontroller: default
         router: router-default
       name: router-<zone>
       namespace: openshift-ingress
     spec:
       externalTrafficPolicy: Cluster
       selector:
         ingresscontroller.operator.openshift.io/deployment-ingresscontroller: default
       sessionAffinity: None
       type: LoadBalancer
    ```
    {: codeblock}

2. Create the Ingress controller service in your cluster.
    ```sh
    oc create -f router-<zone>.yaml
    ```
    {: pre}

3. Verify that the Ingress controller service is created in the correct zone. In the output, get the **EXTERNAL IP** address.
    ```sh
    oc get svc router-<zone> -n openshift-ingress
    ```
    {: pre}

    Example output

    ```sh
    NAME                         TYPE           CLUSTER-IP       EXTERNAL-IP     PORT(S)                      AGE
    router-dal12                 LoadBalancer   172.21.57.132    169.XX.XX.XX    80/TCP,443/TCP,1940/TCP      3m
    ```
    {: screen}

4. Get the subdomain for your default Ingress controller. In the output, look for the subdomain formatted like `<cluster_name>-<random_hash>-0000.<region>.containers.appdomain.cloud`.
    ```sh
    ibmcloud oc nlb-dns ls -c <cluster_name_or_ID>
    ```
    {: pre}

5. Register the Ingress controller service's IP address with your Ingress controller's subdomain.
    ```sh
    ibmcloud oc nlb-dns add -c <cluster_name_or_ID> --ip <router_svc_ip> --nlb-host <router_subdomain>
    ```
    {: pre}






