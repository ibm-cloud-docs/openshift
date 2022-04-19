---

copyright: 
  years: 2014, 2022
lastupdated: "2022-04-19"

keywords: openshift

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}


# VPC clusters: Why can't my app connect via Ingress?
{: #vpc_ts_alb}
{: support}

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

2. {{site.data.keyword.redhat_openshift_notm}} version 4.4 or earlier only: [Allow traffic requests that are routed by the VPC load balancer to node ports on your worker nodes](/docs/openshift?topic=openshift-vpc-security-group).

3. Verify that the VPC load balancer for your routers exists. In the output, look for the VPC load balancer **Name** that starts with `kube-crtmgr-<cluster_ID>`. If you did not install the `infrastructure-service` plug-in, install it by running `ibmcloud plugin install infrastructure-service`.
    ```sh
    ibmcloud is load-balancers
    ```
    {: pre}

   -  If the VPC load balancer is not listed, it was deleted through the VPC console or the CLI. [Open an {{site.data.keyword.cloud_notm}} support case](https://cloud.ibm.com/unifiedsupport/cases/add) and include your cluster ID.

4.  If the load balancer exists, [view the VPC security groups that are attached to it](/docs/containers?topic=containers-vpc-security-group#vpc-sg-view). Ensure that you have not made any modifications to the `kube-<vpc-id>` security group, which is automatically applied to the VPC ALB when it is created. 
  - If you have modified the `kube-<vpc-id>` security group, set the original rules back in the security group. 
  - If you have removed the `kube-<vpc-id>` security group and replaced it with one or more security groups that you manage, ensure that inbound traffic to the ALB is allowed by the security groups you have set. Check that outbound traffic to the cluster workers is allowed to the nodeport range 30,000 - 32,767 on whichever protocols the ALB is using. 
  - If the VPC load balancer is listed and you have not modified the `kube-<vpc-id>` security group attached to it, the DNS entry might still be registering. When a VPC load balancer is created, the hostname is registered through a public DNS. Sometimes, it can take several minutes for this DNS entry to be replicated to the specific DNS that your client is using. You can either wait for the hostname to be registered in your DNS, or access the VPC load balancer directly by using one of its IP addresses. To find the VPC load balancer IP addresses, run `ibmcloud is lb <LB_ID>` and look for the **Public IPs** field. If after several minutes you can't reach the load balancer, it might be offline due to provisioning or connection issues. [Open an {{site.data.keyword.cloud_notm}} support case](https://cloud.ibm.com/unifiedsupport/cases/add). For the type, select **Technical**. For the category, select **Network** in the VPC section. In the description, include your cluster ID and the VPC load balancer ID.




