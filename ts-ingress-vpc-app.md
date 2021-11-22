---

copyright: 
  years: 2014, 2021
lastupdated: "2021-11-22"

keywords: openshift

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}


# VPC clusters: Why can't my app connect via Ingress?
{: #vpc_ts_alb}

**Infrastructure provider**:
* ![VPC infrastructure provider icon.](images/icon-vpc-2.svg) VPC


You exposed your app by creating an Ingress resource for your app in your VPC cluster. When you tried to connect to your app by using the Ingress subdomain, the connection failed or timed out.
{: tsSymptoms}


When you create a VPC cluster, one public and one private VPC load balancer are automatically created outside of your cluster in your VPC.
{: tsCauses}

The VPC load balancer routes requests to the apps that the routers expose. Requests can't be routed to your app in the following situations:
    * A VPC security group is blocking incoming traffic to your worker nodes, including incoming requests to your app.
    * The VPC load balancer is offline, such as due to load balancer provisioning errors or VSI connection errors.
    * The VPC load balancer is deleted through the VPC console or the CLI.
    * The VPC load balancer's DNS entry is still registering.


Verify that no VPC security groups are blocking traffic to your cluster and that the VPC load balancer is available.
{: tsResolve}

1. Install the `infrastructure-service` plug-in. The prefix for running commands is `ibmcloud is`.
    ```sh
    ibmcloud plugin install infrastructure-service
    ```
    {: pre}

2. {{site.data.keyword.openshiftshort}} version 4.4 or earlier only: [Allow traffic requests that are routed by the VPC load balancer to node ports on your worker nodes](/docs/openshift?topic=openshift-vpc-network-policy#security_groups).

3. Verify that the VPC load balancer for your routers exists. In the output, look for the VPC load balancer **Name** that starts with `kube-crtmgr-<cluster_ID>`. If you did not install the `infrastructure-service` plug-in, install it by running `ibmcloud plugin install infrastructure-service`.
    ```sh
    ibmcloud is load-balancers
    ```
    {: pre}


If the VPC load balancer is not listed, it was deleted through the VPC console or the CLI. [Open an {{site.data.keyword.cloud_notm}} support case](https://cloud.ibm.com/unifiedsupport/cases/add) and include your cluster ID.

If the VPC load balancer is listed, its DNS entry might still be registering. When a VPC load balancer is created, the hostname is registered through a public DNS. In some cases, it can take several minutes for this DNS entry to be replicated to the specific DNS that your client is using. You can either wait for the hostname to be registered in your DNS, or access the VPC load balancer directly by using one of its IP addresses. To find the VPC load balancer IP addresses, run `ibmcloud is lb <LB_ID>` and look for the **Public IPs** field. If after several minutes you can't reach the load balancer, it might be offline due to provisioning or connection issues. [Open an {{site.data.keyword.cloud_notm}} support case](https://cloud.ibm.com/unifiedsupport/cases/add). For the type, select **Technical**. For the category, select **Network** in the VPC section. In the description, include your cluster ID and the VPC load balancer ID.




