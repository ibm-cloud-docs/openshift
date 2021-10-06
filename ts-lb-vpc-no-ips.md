---

copyright: 
  years: 2014, 2021
lastupdated: "2021-10-06"

keywords: openshift, roks, rhoks, rhos

subcollection: openshift
content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}



# VPC clusters: Why does a Kubernetes `LoadBalancer` service fail with no IPs?
{: #vpc_no_lb}

**Infrastructure provider**: ![VPC infrastructure provider icon.](images/icon-vpc-2.svg) VPC

You exposed your app by creating a Kubernetes `LoadBalancer` service in your VPC cluster.
{: tsSymptoms}

When you run `oc describe svc <kubernetes_lb_service_name>`, you see a warning message in the **Events** section similar to one of the following:
```
The subnet with ID(s) '<subnet_id>' has insufficient available ipv4 addresses.
```
{: screen}

When you create a Kubernetes `LoadBalancer` service in your cluster, a VPC load balancer is automatically created in your VPC.
{: tsCauses}

The VPC load balancer puts a floating IP address for your Kubernetes `LoadBalancer` service behind a hostname that you can access your app through.

In VPC clusters, both worker nodes and services are assigned IP addresses from the same subnets. Traffic routing is enabled between subnets, so when all IP addresses in a subnet for a zone are used by worker nodes or services, you can still create new worker nodes or services in that zone because they use IP addresses from subnets in other zones. However, if all IP addresses on all subnets are in use, a new Kubernetes `LoadBalancer` service cannot be successfully provisioned.

After you create a VPC subnet, you cannot resize it or change its IP range.
{: tsResolve}

Instead, you must create a larger VPC subnet in one or more zones where you have worker nodes. Then you create a new worker pool using the larger subnets.

1. [Create a new VPC subnet](https://cloud.ibm.com/vpc/provision/network){: external} in the same VPC and in one or more zones where your cluster has worker nodes. Make sure that you create a subnet that can support both the number of worker nodes and services that you plan to create in your cluster. The default CIDR size of each VPC subnet is `/24`, which can support up to 253 worker nodes and services. To check your cluster's VPC and zones, run `ibmcloud oc cluster get --cluster <cluster_name_or_ID>`.

2. Create a new worker pool in your cluster.
    ```sh
    ibmcloud oc worker-pool create vpc-gen2 --name <name> --cluster <cluster_name_or_ID> --flavor <flavor> --size-per-zone <number_of_worker_nodes> --label <key>=<value>
    ```
    {: pre}

3. Using the ID for the larger subnets that you created in step 1, add the zones to the worker pool. Repeat the following command for each zone and subnet.
    ```sh
    ibmcloud oc zone add vpc-gen2 --zone <zone> --subnet-id <subnet_id> --cluster <cluster_name_or_ID> --worker-pool <worker_pool_name>
    ```
    {: pre}

4. After a few minutes, verify that your `LoadBalancer` service is successfully provisioned onto one of the new subnets. If the service is provisioned successfully, no `Warning` or `Error` events are displayed.
    ```sh
    oc describe svc <kubernetes_lb_service_name>
    ```
    {: pre}






