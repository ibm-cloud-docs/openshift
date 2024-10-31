---

copyright: 
  years: 2024, 2024
lastupdated: "2024-10-30"

keywords: openshift, {{site.data.keyword.openshiftlong_notm}}, secure by default, {{site.data.keyword.openshiftlong_notm}}, outbound traffic protection, cluster create, quota, limitations

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why do I see DNS failures after adding a custom DNS resolver?
{: #ts-sbd-custom-dns}

[Virtual Private Cloud]{: tag-vpc}
[4.15 and later]{: tag-red}

You see DNS failures after creating a custom DNS resolver in your VPC where a 4.15 cluster already exists.
{: tsSymptoms}

In each of the following cases, syncing the `kube-<clusterID>` security group and replace the worker nodes as described in the following steps. Note that issue might not be seen immediately after the resolver is created and enabled in the VPC. DNS includes a cache which might resolve name lookup until a worker is replaced or restarted, or pods are restarted.  

- Adding or replacing a worker node to the cluster fails and `ibmcloud ks workers` shows a worker status similar to the following
    ```sh
    Infrastructure instance status is 'failed': Can't start instance because provisioning failed.
    ```
    {: screen}
 
- Running `oc get oc` you see an error similar to the following.
    ```sh
    dial tcp: lookup s3.direct.eu-de.cloud-object-storage.appdomain.cloud on 172.21.0.10:53: server misbehaving.
    ```
    {: screen}

- Restarting a worker results in and pods on that worker are in `Terminating` state, the OpenShift web console no longer opens, or Ingress is in `Critical` state.


If you have a custom DNS resolver enabled in your VPC before creating a 4.15 cluster, then {{site.data.keyword.openshiftlong_notm}} automatically adds rules to allow traffic through the DNS resolver IP addresses to your IBM Cloud managed security group (`kube-<clusterID>`).
{: tsCauses}

However, If you enable a custom DNS resolver on a VPC that already contains a 4.15 cluster, then those existing clusters lose access to DNS.

To correct this problem, allow access to the DNS resolvers on your existing clusters by syncing the `kube-<clusterID>` security group. Syncing the `kube-<clusterID>` security group adds rules that allow traffic through the DNS resolver IP addresses
{: tsResolve}

1. Find the security group ID of your `kube-<clusterID>` security group.

    ```sh
    ibmcloud is security-groups
    ```
    {: pre}

1. Sync the security group.

    ```sh
    ibmcloud oc security-group sync --cluster <clusterID> --security-group <security-group-ID>
    ```
    {: pre}

1. Replace the worker nodes in your cluster.
    ```sh
    ibmcloud oc worker replace --cluster <cluster_name_or_ID> --worker <worker_node_ID>
    ```
    {: pre}

1. If the issue persists, contact support. Open a [support case](/docs/account?topic=account-using-avatar). In the case details, be sure to include any relevant log files, error messages, or command outputs.


## Other scenarios
{: #sbd-dns-scenarios}

Error conditions that might be due to the combination of a custom DNS resolver in the VPC and 4.15 clusters in the same VPC.


### If the cluster is created after the DNS resolver is created
{: #sbd-dns-after}

If you create a 4.15 cluster after creating a custom DNS resolver and your worker do not enter a `Normal` or `Active` state, then the rules for the DNS custom resolver are not added to the `kube-<clusterID>` security group before they are needed by the logic that deploys the workers. 

1. List the details of the `kube-<clusterID>` security group to verify the custom DNS resolver IPs are added as targets in the security group.
    ```sh
    ibmcloud is sg kube-<clusterID>
    ```
    {: pre}

1. Replace the worker nodes in your cluster.
    ```sh
    ibmcloud oc worker replace --cluster <cluster_name_or_ID> --worker <worker_node_ID>
    ```
    {: pre}

1. If the issue persists, contact support. Open a [support case](/docs/account?topic=account-using-avatar). In the case details, be sure to include any relevant log files, error messages, or command outputs.
