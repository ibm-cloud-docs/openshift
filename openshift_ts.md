---

copyright:
  years: 2014, 2019
lastupdated: "2019-11-06"

keywords: openshift, roks, rhoks, rhos

subcollection: openshift

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
{:external: target="_blank" .external}

# Troubleshooting OpenShift clusters
{: #openshift_troubleshoot}

Review some known issues or common error messages that you might encounter when you use {{site.data.keyword.openshiftlong}} clusters.
{: shortdesc}

For general cluster debugging, see the {{site.data.keyword.containerlong_notm}} docs:
* [Debugging your cluster](/docs/containers?topic=containers-cs_troubleshoot)
* [Clusters and worker nodes](/docs/containers?topic=containers-cs_troubleshoot_clusters)
* [Storage](/docs/openshift?topic=openshift-cs_troubleshoot_storage)
* [Logging and monitoring](/docs/containers?topic=containers-cs_troubleshoot_health)
* [Debugging Ingress](/docs/containers?topic=containers-cs_troubleshoot_debug_ingress)
* [Cluster networking](/docs/containers?topic=containers-cs_troubleshoot_network)

## Feedback, questions, and support
{: #openshift_support}

Review different ways to get help and support for your Red Hat OpenShift on IBM Cloud clusters. For any questions or feedback, post in Slack.
{: shortdesc}

**General ways to resolve issues**<br>
1. Keep your cluster environment up to date.
   * Check monthly for available security and operating system patches to [update your worker nodes](/docs/openshift?topic=openshift-update#worker_node).
   * [Update your cluster](/docs/openshift?topic=openshift-update#master) to the latest default version for [OpenShift](/docs/containers?topic=containers-cs_versions).
2. Make sure that your command line tools are up to date.
   * In the terminal, you are notified when updates to the `ibmcloud` CLI and plug-ins are available. Be sure to keep your CLI up-to-date so that you can use all available commands and flags.
   * Make sure that [your `kubectl` CLI](/docs/containers?topic=containers-cs_cli_install#kubectl) client matches the same Kubernetes version as your cluster server. [Kubernetes does not support ![External link icon](../icons/launch-glyph.svg "External link icon")](https://kubernetes.io/docs/setup/release/version-skew-policy/) `kubectl` client versions that are 2 or more versions apart from the server version (n +/- 2).

**Reviewing issues and status**<br>
1. To see whether {{site.data.keyword.cloud_notm}} is available, [check the {{site.data.keyword.cloud_notm}} status page ![External link icon](../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/status?selected=status).
2. Filter for the **Kubernetes Cluster** component.

**Feedback and questions**<br>
1. Post in the {{site.data.keyword.containerlong_notm}} Slack.
   *   If you are an external user, post in the [#openshift ![External link icon](../icons/launch-glyph.svg "External link icon")](https://ibm-container-service.slack.com/messages/CKCJLJCH4) channel.
   *   If you are an IBMer, use the [#iks-openshift-users ![External link icon](../icons/launch-glyph.svg "External link icon")](https://ibm-argonauts.slack.com/messages/CJH0UPN2D) channel.<p class="tip">If you do not use an IBMid for your {{site.data.keyword.cloud_notm}} account, [request an invitation](https://cloud.ibm.com/kubernetes/slack) to this Slack.</p>
2. Review forums such as OpenShift help, Stack Overflow, and IBM Developer to see whether other users ran into the same issue. When you use the forums to ask a question, tag your question so that it is seen by the {{site.data.keyword.cloud_notm}} development teams.
   * If you have technical questions about developing or deploying clusters or apps with {{site.data.keyword.containerlong_notm}}, post your question on [Stack Overflow ![External link icon](../icons/launch-glyph.svg "External link icon")](https://stackoverflow.com/questions/tagged/ibm-cloud+containers) and tag your question with `ibm-cloud`, `containers`, and `openshift`.
   * For questions about the service and getting started instructions, use the [IBM Developer Answers ![External link icon](../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/answers/topics/containers/?smartspace=bluemix) forum. Include the `ibm-cloud`, `containers`, and `openshift` tags.
   * See [Getting help](/docs/get-support?topic=get-support-getting-customer-support#using-avatar) for more details about using the forums.

**Getting help**<br>
1.  Contact IBM Support by opening a case. To learn about opening an IBM support case, or about support levels and case severities, see [Contacting support](/docs/get-support?topic=get-support-getting-customer-support).
2.  In your support case, for **Category**, select **Containers**.
3.  For the **Offering**, select your OpenShift cluster.<p class="tip">When you report an issue, include your cluster ID. To get your cluster ID, run `ibmcloud oc cluster ls`. You can also use the [{{site.data.keyword.containerlong_notm}} Diagnostics and Debug Tool](/docs/containers?topic=containers-cs_troubleshoot#debug_utility) to gather and export pertinent information from your cluster to share with IBM Support.</p>


## Missing permissions to create clusters
{: #rhoks_ts_cluster_permissions}

{: tsSymptoms}
You do not have permissions to create a cluster.

{: tsCauses}
To create an OpenShift cluster, you must have the same permissions as you need to create a community Kubernetes cluster. The required permissions include infrastructure credentials for the region and resource group and {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM) **Administrator** permissions.

{: tsResolve}
Review [Assigning cluster access](/docs/openshift?topic=openshift-users) to learn how to set up infrastructure credentials for a region and resource group and how to assign users access through IAM.

<br />


## No resources found
{: #rhoks_ts_not_found}

{: tsSymptoms}
When you are running an `oc` command such as `oc get nodes` or `oc get secrets`, you see an error message similar to the following.

```
No resources found.
```
{: screen}

{: tsCauses}
Your OpenShift token is expired. OpenShift token that are generated by using your {{site.data.keyword.cloud_notm}} IAM credentials expire in 24 hours.

{: tsResolve}
Re-authenticate with the OpenShift token by [copying the `oc login` command from the web console](/docs/openshift?topic=openshift-openshift_access_cluster#access_public_se) or [creating an API key](/docs/openshift?topic=openshift-openshift_access_cluster#access_api_key).

<br />


## Time out when trying to connect to a pod
{: #roks_timeout}

{: tsSymptoms}
You try to connect to a pod, such as logging in with `oc exec` or getting logs with `oc logs`. The pod is healthy, but you see an error message similar to the following.
```
Error from server: Get https://<10.xxx.xx.xxx>:<port>/<address>: dial tcp <10.xxx.xx.xxx>:<port>: connect: connection timed out
```
{: screen}

{: tsCauses}
The OpenVPN server is experiencing configuration issues that prevent accessing the pod from its internal address.

{: tsResolve}
Before you begin: [Access your OpenShift cluster](/docs/openshift?topic=openshift-openshift_access_cluster).

1.  Check if a cluster and worker node updates are available by viewing your cluster and worker node details in the console or a `cluster ls` or `worker ls` command. If so, [update your cluster and worker nodes to the latest version](/docs/openshift?topic=openshift-update).
2.  Restart the OpenVPN pod by deleting it. Another VPN pod is scheduled. When its **STATUS** is **Running**, try to connect the pod that you previously could not connect to.
    ```
    oc delete pod -n kube-system -l app=vpn
    ```
    {: pre}

<br />


## Missing the public `containers.appdomain.cloud` subdomain
{: #roks_ts_subdomain}

{: tsSymptoms}
When you expose an app through a router subdomain, you get a local subdomain instead of a public route, in the format: `<service_name>-<project_name>.router.default.svc.cluster.local`.

{: tsCauses}
After the cluster is created and enters a **normal** state, the router subdomain networking and load balancing components still take some time to deploy. If you expose your app before the networking components fully provision, or if the components experience an error, your apps can only be exposed internally with the default router's `svc.cluster.local` domain.

When the components fully provision, a public router subdomain is available for your apps, in the format `<cluster-name>-<accountID-hashed>-<ssll>.<region>.containers.appdomain.cloud`.

{: tsResolve}

1.  After you create a cluster, wait some time before you expose your apps, even after the cluster enters a **normal** state.
2.  Check the **Master Status**. If the **Master Status** is not **Ready**, [review its status](/docs/containers?topic=containers-cs_troubleshoot#debug_master) and follow any troubleshooting information to resolve the issue.   
    ```
    ibmcloud oc cluster get -c <cluster_name_or_ID>
    ```
    {: pre}
3.  Check that your cluster has public connectivity so that the networking components can talk to the master as they deploy.
    *  In the output of Step 2, check that your cluster has a **Public Service Endpoint URL**. If your cluster does not have a **Public Service Endpoint URL**, [enable it](/docs/openshift?topic=openshift-cs_network_cluster#set-up-public-se).
    *   Check that at least some of the worker nodes in your cluster have a **Public IP** address. If no worker node does, you must [set up public VLANs for at least one worker pool](/docs/openshift?topic=openshift-cs_network_cluster#change-vlans).
        ```
        ibmcloud oc workers -c <cluster_name_or_ID>
        ```
        {: pre}
4.  In the output of Step 2, check that the **Ingress Subdomain** is available. The Ingress components in your cluster must provision before the router components can be created. If the **Ingress Subdomain** and **Ingress Secret** are not available, see [No Ingress subdomain exists after cluster creation](/docs/containers?topic=containers-cs_troubleshoot_network#ingress_subdomain).
5.  Check that the **Hostname** of the router subdomain is in the format: `<cluster-name>-<accountID-hashed>-<ssll>.<region>.containers.appdomain.cloud`.
    ```
    ibmcloud oc nlb-dns ls -c <cluster_name_or_ID>
    ```
    {: pre}

    *  If after two hours of creating the cluster, the router subdomain is not updated, review the **Master Status** of the cluster again, and follow any troubleshooting steps to resolve the issue.

If the troubleshooting steps do not resolve the issue, see [Getting help](#openshift_support).

<br />


## OpenVPN server error due to ingress IP address for NLB
{: #rhoks_ts_openvpn_subnet}

{: tsSymptoms}
You see the following error message.
```
CAE003: Unable to determine the ingress IP address for the network load balancer.
```
{: screen}

{: tsCauses}
The OpenVPN server could not be configured because the router IP address that is created for the network load balancer (NLB) could not be found. The router might not have been assigned an IP address because your cluster does not have a subnet with available portable IP addresses, or the NLB setup did not complete.

{: tsResolve}

**Verify that your cluster has available subnets.**
1.  Check that your cluster has a **Subnet CIDR** for public and private subnets. If you set up a private VLAN-only cluster, you might have only a private subnet.
    ```
    ibmcloud oc cluster get --cluster <cluster_name_or_ID> --show-resources
    ```
    {: pre}

    Example output:
    ```
    Name:                           <cluster_name>   
    ...

    Subnet VLANs
    VLAN ID   Subnet CIDR        Public   User-managed   
    2345678   10.xxx.xx.xxx/29   false    false   
    2876543   169.xx.xxx.xxx/29  true     false
    ```
    {: screen}
2.  If the cluster does not have a subnet, [create a subnet for the cluster](/docs/containers?topic=containers-subnets#request) or [add an existing subnet from your account to the cluster](/docs/containers?topic=containers-subnets#add-existing).
3.  If the cluster does have a subnet, [check for available portable IP addresses](/docs/containers?topic=containers-subnets#review_ip) and if necessary, [add more portable IP address by adding a subnet](/docs/containers?topic=containers-subnets#adding_ips).
4.  Refresh the master to restart the OpenVPN setup so that it uses the available subnet.
    ```
    ibmcloud oc cluster master refresh --cluster <cluster_name_or_ID>
    ```
    {: pre}

**Verify that the NLB setup completed successfully.**
1.  Check that the `ibm-cloud-provider-ip-*` pods for the NLB are in a **Running** status.
    ```
    oc get pods -n ibm-system | grep ibm-cloud-provider-ip
    ```
    {: pre}
2.  If a pod is not running, review the **Events** in the pod details to troubleshoot the issue further.
    ```
    oc describe pod -n kube-system <pod_name>
    ```
    {: pre}
3.  After you resolve the NLB pod issue, refresh the master to restart the NLB setup.
    ```
    ibmcloud oc cluster master refresh --cluster <cluster_name_or_ID>
    ```
    {: pre}

<br />


## OpenVPN server error due to NLB DNS
{: #rhoks_ts_openvpn_dns}

{: tsSymptoms}
Could not create a domain name service for the network load balancer (`ibmcloud oc nlb-dns create`) with the following error message:<ul>
<li><code>This action requires the Editor role for the cluster in IBM Cloud Container Service. Contact the IBM Cloud account administrator and request the required Identity and Access user role. (A0008)</code></li>
<li><code>The specified cluster could not be found. (A0006)</code></li>
<li><code>The input parameters in the request body are either incomplete or in the wrong format. Be sure to include all required parameters in your request in JSON format. (E0011)</code></li></ul>

{: tsCauses}
The OpenVPN server could not be configured because a domain name service (DNS) was not created for the network load balancer (NLB).

{: tsResolve}
1.  Check that you have the correct permissions in {{site.data.keyword.cloud_notm}} IAM. If not, contact your account administrator to [assign you the appropriate IAM platform or service access role](/docs/containers?topic=containers-users#platform).
    ```
    ibmcloud iam user-policies <my_user_name@example.com>
    ```
    {: pre}
2.  For cluster not found or incorrect input parameter errors, continue to the next step.
3.  Refresh the master so that NLB DNS creation operation is retried.
    ```
    ibmcloud oc cluster master refresh --cluster <cluster_name_or_ID>
    ```
    {: pre}

<br />




## VPN server error due to infrastructure credentials
{: #rhoks_ts_openvpn_login}

{: tsSymptoms}
After you create or update a cluster, the master status returns a VPN server configuration error message similar to the following.
```
VPN server configuration update failed. IBM Cloud support has been notified and is working to resolve this issue.
```
{: screen}

{: tsCauses}
The infrastructure credentials that are associated with the resource group that the cluster is created in are missing (such as the API key owner is no longer part of the account) or missing required permissions.

{: tsResolve}
[Complete the troubleshooting guide](/docs/containers?topic=containers-cs_troubleshoot_clusters#cs_credentials) to check and update the infrastructure credentials that are used for the resource group.

<br />


## Missing projects or `oc` and `kubectl` commands fail
{: #rhoks_ts_admin_config}

{: tsSymptoms}
You do not see all the projects that you have access to. When you try to run `oc` or `kubectl` commands, you see an error similar to the following.
```
No resources found.
Error from server (Forbidden): <resource> is forbidden: User "IAM#user@email.com" cannot list <resources> at the cluster scope: no RBAC policy matched
```
{: screen}

{: tsCauses}
You need to download the `admin` configuration files for your cluster in order to run commands that require the `cluster-admin` cluster role.

{: tsResolve}
Run `ibmcloud oc cluster config --cluster <cluster_name_or_ID> --admin` and try again.

<br />


## Pods in `CrashLoopBackOff` status
{: #rhoks_ts_pods_crashloop}

{: tsSymptoms}
Your pods are in a `CrashLoopBackOff` status.

{: tsCauses}
When you try to deploy an app that works on community Kubernetes platforms, you might see this status or a related error message because OpenShift sets up stricter security settings by default than community Kubernetes.

{: tsResolve}
Make sure that you followed the docs in the [Moving your apps to OpenShift topic](/docs/openshift?topic=openshift-openshift_apps#openshift_move_apps).

<br />


## Cannot push or pull images from local machine to Docker registry
{: #rhoks_ts_docker_local}

{: tsSymptoms}
You cannot push or pull Docker images from your local machine to the cluster's built-in Docker registry.

{: tsCauses}
By default, the Docker registry is available internally within the cluster. You can build apps from remote directories such as GitHub or DockerHub by using the `oc new-app` command. Or, you can expose your Docker registry such as with a route or load balancer so that you can push and pull images from your local machine.

{: tsResolve}
Create a route for the `docker-registry` service in the `default` project. For more information, see [Setting up a secure external route for the internal registry](/docs/openshift?topic=openshift-openshift-images#route_internal_registry).

## Time out when pushing to the internal registry
{: #roks_timeout_docker}

{: tsSymptoms}
You try to push an image to the [internal registry](/docs/openshift?topic=openshift-openshift-images#openshift_internal_registry), but sporadically you see an error message similar to the following.
```
received unexpected HTTP status: 504 Gateway Time-out
```
{: screen}

{: tsCauses}
The default file storage device that provides the storage for the internal registry's images is initially set up with 2 IOPS and 20 GB of storage. When you push larger images, the device might time out because its IOPS is too low to support the image.

{: tsResolve}
[Change the size and IOPS of the existing file storage device](/docs/openshift?topic=openshift-file_storage#file_change_storage_configuration).

When you resize the volume in your IBM Cloud infrastructure account, the attached PVC description is not updated. Instead, you can log in to the `docker-registry` pod that uses the `registry-backing` PVC to verify that the volume is resized.
{: note}
