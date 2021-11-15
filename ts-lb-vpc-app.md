---

copyright: 
  years: 2014, 2021
lastupdated: "2021-11-15"

keywords: openshift

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}


# VPC clusters: Why can't my app connect via load balancer?
{: #vpc_ts_lb}

**Infrastructure provider**: ![VPC infrastructure provider icon.](images/icon-vpc-2.svg) VPC

You exposed your app by creating a Kubernetes `LoadBalancer` service in your VPC cluster. When you try to connect to your app by using the hostname that is assigned to the Kubernetes `LoadBalancer`, the connection fails or times out.
{: tsSymptoms}

When you run `oc describe svc <kubernetes_lb_service_name>`, you might see a warning message similar to one of the following in the **Events** section:

```sh
The VPC load balancer that routes requests to this Kubernetes `LoadBalancer` service is offline.
```
{: screen}

```sh
The VPC load balancer that routes requests to this Kubernetes `LoadBalancer` service was deleted from your VPC.
```
{: screen}


When you create a Kubernetes `LoadBalancer` service in your cluster, a VPC load balancer is automatically created in your VPC. The VPC load balancer routes requests only to the app that the Kubernetes `LoadBalancer` service exposes.
{: tsCauses}

Requests cannot be routed to your app in the following situations:
* A VPC security group is blocking incoming traffic to your worker nodes, including incoming requests to your app.
* The VPC load balancer is offline, such as due to load balancer provisioning errors or VSI connection errors.
* The VPC load balancer is deleted through the VPC console or the CLI.
* The VPC load balancer's DNS entry is still registering.
* You reached the maximum number of VPC load balancers permitted per account. Check the [VPC quotas documentation](/docs/vpc?topic=vpc-quotas#load-balancer-quotas) for VPC resource quotas across all of your VPC clusters in your VPC.

Verify that no VPC security groups are blocking traffic to your cluster and that the VPC load balancer is available.
{: tsResolve}

1. {{site.data.keyword.openshiftshort}} version 4.4 or earlier only: [Allow traffic requests that are routed by the VPC load balancer to node ports on your worker nodes](/docs/openshift?topic=openshift-vpc-network-policy#security_groups).

2. Verify that the VPC load balancer for the Kubernetes `LoadBalancer` service exists. In the output, look for the VPC load balancer that is formatted `kube-<cluster_ID>-<kubernetes_lb_service_UID>`. You can get the Kubernetes `LoadBalancer` service UID by running `oc get svc <service_name> -o yaml`.
    ```sh
    ibmcloud is load-balancers
    ```
    {: pre}

- If the VPC load balancer is not listed, it does not exist for one of the following reasons:
    * You reached the maximum number of VPC load balancers permitted per account. Across all of your VPC clusters in your VPC, a maximum of 20 VPC load balancers can be created. One VPC load balancer is created for each Kubernetes `LoadBalancer` service that you create, and it routes requests to that Kubernetes `LoadBalancer` service only.
    * The VPC load balancer was deleted through the VPC console or the CLI. To re-create the VPC load balancer for your Kubernetes `LoadBalancer` service, restart the Kubernetes master by running `ibmcloud oc cluster master refresh --cluster <cluster_name_or_id>`.
    
    If you want to remove the load balancing setup for an app in your VPC cluster, delete the Kubernetes `LoadBalancer` service by running `oc delete svc <kubernetes_lb_service_name>`. The VPC load balancer that is associated with the Kubernetes `LoadBalancer` service is automatically deleted from your VPC.
    {: tip}
    
- If the VPC load balancer is listed, it might not be responsive for the following reasons:
    * Its DNS entry might still be registering. When a VPC load balancer is created, the hostname is registered through a public DNS. In some cases, it can take several minutes for this DNS entry to be replicated to the specific DNS that your client is using. You can either wait for the hostname to be registered in your DNS, or access the VPC load balancer directly by using one of its IP addresses. To find the VPC load balancer IP addresses, run `ibmcloud is lb <LB_ID>` and look for the **Public IPs** field.
    * If after several minutes you cannot reach the load balancer, it might be offline due to provisioning or connection issues. [Open an {{site.data.keyword.cloud_notm}} support case](https://cloud.ibm.com/unifiedsupport/cases/add). For the type, select **Technical**. For the category, select **Network** in the VPC section. In the description, include your cluster ID and the VPC load balancer ID.





