---

copyright:
  years: 2014, 2019
lastupdated: "2019-07-19"

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

# Troubleshooting OpenShift clusters
{: #openshift_troubleshoot}

Review some known issues or common error messages that you might encounter when you use Red Hat OpenShift on IBM Cloud clusters.
{: shortdesc}

For general cluster debugging, see the {{site.data.keyword.containerlong_notm}} docs.
* [Debugging your cluster](/docs/containers?topic=containers-cs_troubleshoot).
* [Clusters and worker nodes](/docs/containers?topic=containers-cs_troubleshoot_clusters).
* [Storage](/docs/containers?topic=containers-cs_troubleshoot_storage).
* [Logging and monitoring](/docs/containers?topic=containers-cs_troubleshoot_health).
* [Debugging Ingress](/docs/containers?topic=containers-cs_troubleshoot_debug_ingress).
* [Cluster networking](/docs/containers?topic=containers-cs_troubleshoot_network).

## Feedback and questions
{: #openshift_support}

During the beta, Red Hat OpenShift on IBM Cloud clusters are not covered by IBM Support nor Red Hat Support. Any support that is provided is to help you evaluate the product in preparation for its general availability.
{: important}

For any questions or feedback, post in Slack.
*   If you are an external user, post in the [#openshift ![External link icon](../icons/launch-glyph.svg "External link icon")](https://ibm-container-service.slack.com/messages/CKCJLJCH4) channel.
*   If you are an IBMer, use the [#iks-openshift-users ![External link icon](../icons/launch-glyph.svg "External link icon")](https://ibm-argonauts.slack.com/messages/CJH0UPN2D) channel.

If you do not use an IBMid for your {{site.data.keyword.cloud_notm}} account, [request an invitation](https://bxcs-slack-invite.mybluemix.net/) to this Slack.
{: tip}

## Missing permissions to create clusters
{: #rhoks_ts_cluster_permissions}

{: tsSymptoms}
You do not have permissions to create a cluster.

{: tsCauses}
To create an OpenShift cluster, you must have the same permissions as you need to create a native Kubernetes cluster. The required permissions include infrastructure credentials for the region and resource group and {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM) **Administrator** permissions.

{: tsResolve}
Review [Assigning cluster access](https://cloud.ibm.com/docs/containers?topic=containers-users) to learn how to set up infrastructure credentials for a region and resource group and how to assign users access through IAM.

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
The OpenVPN server could not be configured because the router IP address that is created for the network load balancer (NLB) could not be found. The router might not have been assigned an IP address because your cluster does not have a subnet with available portable IP addresses, or the Ingress setup did not complete.

{: tsResolve}

**Verify that your cluster has available subnets.**
1.  Check that your cluster has a **Subnet CIDR** for public and private subnets. If you set up a private VLAN-only cluster, you might only have a private subnet.
    ```
    oc cluster-get --cluster <cluster_name_or_ID> --showResources
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
    oc cluster-refresh --cluster <cluster_name_or_ID>
    ```
    {: pre}

**Verify that the Ingress setup completed successfully.**
1.  Check that the `ibm-cloud-provider-ip-*` pods for Ingress are in a **Running** status.
    ```
    oc get pods -n kube-system | grep alb
    ```
    {: pre}
2.  If a pod is not running, review the **Events** in the pod details to troubleshoot the issue further.
    ```
    oc describe pod -n kube-system <pod_name>
    ```
    {: pre}
3.  After you resolve the Ingress pod issue, refresh the master to restart the Ingress setup.
    ```
    oc cluster-refresh --cluster <cluster_name_or_ID>
    ```
    {: pre}

<br />


## OpenVPN server error due to NLB DNS
{: #rhoks_ts_openvpn_dns}

{: tsSymptoms}
Could not create a domain name service for the network load balancer ('oc nlb-dns-create') with the following error message:<ul>
<li><code>This action requires the Editor role for the cluster in IBM Cloud Container Service. Contact the IBM Cloud account administrator and request the required Identity and Access user role. (A0008)</code></li>
<li><code>The specified cluster could not be found. (A0006)</code></li>
<li><code>The input parameters in the request body are either incomplete or in the wrong format. Be sure to include all required parameters in your request in JSON format. (E0011)</code></li><ul>

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
    oc cluster-refresh --cluster <cluster_name_or_ID>
    ```
    {: pre}

<br />


## Cannot access registry console
{: #rhoks_ts_registry_console}

{: tsSymptoms}
Cannot access the local Docker registry console with the following error.
```
An authentication error occurred.
```
{: screen}

{: tsCauses}
OpenShift clusters that were created before 18 June 2019 did not set the registry console provider URL to the external cluster endpoint.

{: tsResolve}
Modify the registry console deployment so that you can access it externally.
1.  From the OpenShift **Application Console**, open the **default** namespace and then click **Applications > Deployments > registry-console**.
2.  In the **Environment** tab of the **registry-console** details page, find the **OPENSHIFT_OAUTH_PROVIDER_URL** field.
3.  In the **Value** field, add `-e` after the `c1` such as in `https://c1-e.eu-gb.containers.cloud.ibm.com:20399`.
4.  Click **Save**. Now, the registry console deployment can be accessed through the public API endpoint of the cluster master.
5.  From the **default** project navigation pane, click **Applications > Routes**. To open the registry console, click the **Hostname** value, such as `https://registry-console-default.<cluster_name>-<random_ID>.<region>.containers.appdomain.cloud`.

    For the beta, the registry console uses self-signed TLS certificates, so you must choose to proceed to get to the registry console. In Google Chrome, click **Advanced > Proceed to <cluster_master_URL>**. Other browsers have similar options. If you cannot proceed with this setting, try opening the URL in a private browser.
    {: note}

<br />


## `oc` or `kubectl` commands fail
{: #rhoks_ts_admin_config}

{: tsSymptoms}
When you try to run `oc` or `kubectl` commands, you see an error similar to the following.
```
No resources found.
Error from server (Forbidden): <resource> is forbidden: User "IAM#user@email.com" cannot list <resources> at the cluster scope: no RBAC policy matched
```
{: screen}

{: tsCauses}
You need to download the `admin` configuration files for your cluster in order to run commands that require the `cluster-admin` cluster role.

{: tsResolve}
Run `oc cluster-config --cluster <cluster_name_or_ID> --admin` and try again.

<br />


## Cannot use `calicoctl`
{: #rhoks_ts_calicoctl}

{: tsSymptoms}
When you try to use `calicoctl`, you get the following error.
```
Failed to create Calico API client: context deadline exceeded
```
{: screen}

{: tsCauses}
The Calico configuration file must be modified to update the `etcdEndpoint` field.

{: tsResolve}
Follow the instructions in the [Limitations topic](#openshift_limitations).

<br />


## Pods in `CrashLoopBackOff` status
{: #rhoks_ts_pods_crashloop}

{: tsSymptoms}
Your pods are in a `CrashLoopBackOff` status.

{: tsCauses}
When you try to deploy an app that works on native Kubernetes platforms, you might see this status or a related error message because OpenShift sets up stricter security settings by default than native Kubernetes.

{: tsResolve}
Make sure that you followed the docs that are linked in the [Limitations topic](#openshift_limitations).

<br />


## Cannot push or pull images from local machine to Docker registry
{: #rhoks_ts_docker_local}

{: tsSymptoms}
You cannot push or pull Docker images from your local machine to the cluster's built-in Docker registry.

{: tsCauses}
By default, the Docker registry is available internally within the cluster. You can build apps from remote directories such as GitHub or DockerHub by using the `oc new-app` command. Or, you can expose your Docker registry such as with a route or load balancer so that you can push and pull images from your local machine.

{: tsResolve}
Create a route for the `docker-registry` service in the `default` project. Include the `--hostname` flag so that you can give the registry a shorter domain name.

```
oc create route edge --service=docker-registry -n default --hostname <registry_domain_name>
```
{: pre}
