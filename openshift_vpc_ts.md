---

copyright:
  years: 2014, 2019
lastupdated: "2019-10-30"

keywords: openshift, roks, rhoks, rhos, vpc

subcollection: containers

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
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}

# Troubleshooting VPC clusters
{: #vpc_troubleshoot}

Review some known issues or common error messages that you might encounter when you use VPC clusters.
{: shortdesc}

## Cannot connect to an app via load balancer
{: #vpc_ts_lb}

{: tsSymptoms}
You publicly exposed your app by creating a Kubernetes `LoadBalancer` service in your VPC cluster. When you try to connect to your app by using the hostname that is assigned to the Kubernetes `LoadBalancer`, the connection fails or times out.

When you run `kubectl describe svc <kubernetes_lb_service_name>`, you see a warning message similar to one of the following in the **Events** section:
```
The VPC load balancer that routes requests to this Kubernetes `LoadBalancer` service is offline.
```
{: screen}
```
The VPC load balancer that routes requests to this Kubernetes `LoadBalancer` service was deleted from your VPC.
```
{: screen}

{: tsCauses}
When you create a Kubernetes `LoadBalancer` service in your cluster, a VPC load balancer is automatically created in your VPC. The VPC load balancer routes requests only to the app that the Kubernetes `LoadBalancer` service exposes. Requests cannot be routed to your app in the following situations:
* The VPC load balancer is offline, such as due to load balancer provisioning errors or VSI connection errors.
* The VPC load balancer is deleted through the VPC console or the CLI.
* The VPC load balancer's DNS entry is still registering.

{: tsResolve}
Verify that the VPC load balancer for the Kubernetes `LoadBalancer` service exists. In the output, look for the VPC load balancer that is formatted `kube-<cluster_ID>-<kubernetes_lb_service_UID>`. You can get the Kubernetes `LoadBalancer` service UID by running `kubectl get svc <service_name> -o yaml`.
  ```
  ibmcloud is load-balancers
  ```
  {: pre}

* If the VPC load balancer is not listed, it was deleted through the VPC console or the CLI. To recreate the VPC load balancer for your Kubernetes `LoadBalancer` service, restart the Kubernetes master by running `ibmcloud oc cluster master refresh --cluster <cluster_name_or_id>`. <p class="tip">If you want to remove the load-balancing setup for an app in your VPC cluster, delete the Kubernetes `LoadBalancer` service by running `kubectl delete svc <kubernetes_lb_service_name>`. The VPC load balancer that is associated with the Kubernetes `LoadBalancer` service is automatically deleted from your VPC.</p>
* If the VPC load balancer is listed, its DNS entry might still be registering. When a VPC load balancer is created, the hostname is registered through a public DNS. In some cases, it can take several minutes for this DNS entry to be replicated to the specific DNS that your client is using. You can either wait for the hostname to be registered in your DNS, or access the VPC load balancer directly by using one of its IP addresses. To find the VPC load balancer IP addresses, look for the **Public IP** column in the output of `ibmcloud is load-balancers`. If after several minutes you cannot reach the load balancer, it might be offline due to provisioning or connection issues. [Open an {{site.data.keyword.cloud_notm}} support case](https://cloud.ibm.com/unifiedsupport/cases/add). For the type, select **Technical**. For the category, select **Network** in the VPC section. In the description, include your cluster ID and the VPC load balancer ID.

<br />


## Kubernetes `LoadBalancer` service fails because no IPs are available
{: #vpc_no_lb}

{: tsSymptoms}
You publicly exposed your app by creating a Kubernetes `LoadBalancer` service in your VPC cluster. When you run `kubectl describe svc <kubernetes_lb_service_name>`, you see a warning message in the **Events** section similar to one of the following:
```
The subnet with ID(s) '<subnet_id>' has insufficient available ipv4 addresses.
```
{: screen}

{: tsCauses}
When you create a Kubernetes `LoadBalancer` service in your cluster, a VPC load balancer is automatically created in your VPC. The VPC load balancer puts a floating IP address for your Kubernetes `LoadBalancer` service behind a hostname that you can access your app through.

In VPC clusters, both worker nodes and services are assigned IP addresses from the same subnets. Traffic routing is enabled between subnets, so when all IP addresses in a subnet for a zone are used by worker nodes or services, you can still create new worker nodes or services in that zone because they use IP addresses from subnets in other zones. However, if all IP addresses on all subnets are in use, a new Kubernetes `LoadBalancer` service cannot be successfully provisioned.

{: tsResolve}
After you create a VPC subnet, you cannot resize it or change its IP range. Instead, you must create a larger VPC subnet in one or more zones where you have worker nodes. Then you create a new worker pool using the larger subnets.

1. [Create a new VPC subnet ![External link icon](../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/vpc/provision/network) in the same VPC and in one or more zones where your cluster has worker nodes. Make sure that you create a subnet that can support both the number of worker nodes and services that you plan to create in your cluster. The default CIDR size of each VPC subnet is `/24`, which can support up to 253 worker nodes and services. To check your cluster's VPC and zones, run `ibmcloud oc cluster get --cluster <cluster_name_or_ID>`.

2. Create a new worker pool in your cluster.
   ```
   ibmcloud oc worker-pool create vpc-classic --name <worker_pool_name> --cluster <cluster_name_or_ID> --flavor <flavor> --vpc-id <VPC_ID> --size-per-zone <number_of_workers_per_zone>
   ```
   {: pre}

3. Using the ID for the larger subnets that you created in step 1, add the zones to the worker pool. Repeat the following command for each zone and subnet.
  ```
  ibmcloud oc zone add vpc-classic --zone <zone> --subnet-id <subnet_id> --cluster <cluster_name_or_ID> --worker-pool <worker_pool_name>
  ```
  {: pre}

4. After a few minutes, verify that your `LoadBalancer` service is successfully provisioned onto one of the new subnets. If the service is provisioned successfully, no `Warning` or `Error` events are displayed.
  ```
  kubectl describe svc <kubernetes_lb_service_name>
  ```
  {: pre}

<br />


## Cannot connect to an app via Ingress
{: #vpc_ts_alb}

{: tsSymptoms}
You publicly exposed your app by creating an Ingress resource for your app in your cluster. When you tried to connect to your app by using the subdomain of the Ingress application load balancer (ALB), the connection failed or timed out.

{: tsCauses}
When you create a VPC cluster, one public and one private VPC load balancer is automatically created outside of your cluster in your VPC. The VPC load balancer routes requests to the apps that the ALBs expose. Requests cannot be routed to your app in the following situations:
* The VPC load balancer is offline, such as due to load balancer provisioning errors or VSI connection errors.
* The VPC load balancer is deleted through the VPC console or the CLI.
* The VPC load balancer's DNS entry is still registering.

{: tsResolve}
Verify that the VPC load balancer for your ALBs exists. In the output, look for the VPC load balancer that has the same **Host Name** as your public or private ALBs. You can see the hostnames for your public and private ALBs by running `ibmcloud oc alb ls --cluster <cluster_name_or_ID>` and looking for the **Load Balancer Hostname** field.
  ```
  ibmcloud is load-balancers
  ```
  {: pre}

* If the VPC load balancer is not listed, it was deleted through the VPC console or the CLI. To recreate the VPC load balancer for your ALBs, disable all of the public or private ALBs that are assigned that VPC load balancer's hostname by running `ibmcloud oc alb configure vpc-classic --alb-id <ALB_ID> --disable` for each ALB. Then, re-enable those ALBs by running `ibmcloud oc alb configure vpc-classic --alb-id <ALB_ID> --enable` for each ALB. A new VPC load balancer for the ALBs takes a few minutes to provision in your VPC. You cannot access your app until the VPC load balancer for your ALBs is fully provisioned.
* If the VPC load balancer is listed, its DNS entry might still be registering. When a VPC load balancer is created, the hostname is registered through a public DNS. In some cases, it can take several minutes for this DNS entry to be replicated to the specific DNS that your client is using. You can either wait for the hostname to be registered in your DNS, or access the VPC load balancer directly by using one of its IP addresses. To find the VPC load balancer IP addresses, look for the **Public IP** column in the output of `ibmcloud is load-balancers`. If after several minutes you cannot reach the load balancer, it might be offline due to provisioning or connection issues. [Open an {{site.data.keyword.cloud_notm}} support case](https://cloud.ibm.com/unifiedsupport/cases/add). For the type, select **Technical**. For the category, select **Network** in the VPC section. In the description, include your cluster ID and the VPC load balancer ID.

## Getting help and support
{: #vpc_getting_help}

Still having issues with your cluster?
{: shortdesc}

-  In the terminal, you are notified when updates to the `ibmcloud` CLI and plug-ins are available. Be sure to keep your CLI up-to-date so that you can use all available commands and flags.
-   To see whether {{site.data.keyword.cloud_notm}} is available, [check the {{site.data.keyword.cloud_notm}} status page ![External link icon](../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/status?selected=status).
-   Post a question in the [{{site.data.keyword.containerlong_notm}} Slack ![External link icon](../icons/launch-glyph.svg "External link icon")](https://ibm-container-service.slack.com).
    If you are not using an IBM ID for your {{site.data.keyword.cloud_notm}} account, [request an invitation](https://cloud.ibm.com/kubernetes/slack) to this Slack.
    {: tip}
-   Review the forums to see whether other users ran into the same issue. When you use the forums to ask a question, tag your question so that it is seen by the {{site.data.keyword.cloud_notm}} development teams.
    -   If you have technical questions about developing or deploying clusters or apps with Red Hat OpenShift on IBM Cloud, post your question on [Stack Overflow ![External link icon](../icons/launch-glyph.svg "External link icon")](https://stackoverflow.com/questions/tagged/ibm-cloud+containers) and tag your question with `ibm-cloud`, `kubernetes`, and `containers`.
    -   For questions about the service and getting started instructions, use the [IBM Developer Answers ![External link icon](../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/answers/topics/containers/?smartspace=bluemix) forum. Include the `ibm-cloud` and `containers` tags.
    See [Getting help](/docs/get-support?topic=get-support-getting-customer-support#using-avatar) for more details about using the forums.
-   Contact IBM Support by opening a case. To learn about opening an IBM support case, or about support levels and case severities, see [Contacting support](/docs/get-support?topic=get-support-getting-customer-support).
When you report an issue, include your cluster ID. To get your cluster ID, run `ibmcloud oc cluster ls`. You can also use the [{{site.data.keyword.containerlong_notm}} Diagnostics and Debug Tool](/docs/containers?topic=containers-cs_troubleshoot#debug_utility) to gather and export pertinent information from your cluster to share with IBM Support.
{: tip}


