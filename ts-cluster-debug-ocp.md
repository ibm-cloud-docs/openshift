---

copyright:
  years: 2014, 2021
lastupdated: "2021-10-04"

keywords: openshift, roks, rhoks, rhos

subcollection: openshift
content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

  

# Debugging {{site.data.keyword.openshiftshort}} web console, OperatorHub, internal registry, and other components
{: #ocp-debug}

**Infrastructure provider**:
* <img src="images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Classic
* <img src="images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> VPC

{{site.data.keyword.openshiftshort}} clusters have many built-in components that work together to simplify the developer experience. For example, you can use the {{site.data.keyword.openshiftshort}} web console to manage and deploy your cluster workloads, or enable 3rd-party operators from the OperatorHub to enhance your cluster with a service mesh and other capabilities.  
{: shortdesc}

Commonly used components include the following. If these components fail, review the following debug steps.
* **{{site.data.keyword.openshiftshort}} web console** in the `openshift-console` project
* **OperatorHub** in the `openshift-marketplace` project
* **Internal registry** in the `openshift-image-registry` project

<img src="images/icon-version-43.png" alt="Version 4 icon" width="30" style="width:30px; border-style: none"/> Some components, such as the OperatorHub, are available only in clusters that run {{site.data.keyword.openshiftshort}} version 4, or run in different projects in version 3.11. You can still troubleshoot {{site.data.keyword.openshiftshort}} components in 3.11 clusters, but the project and resource names might vary.
{: note}

## Step 1: Check your account setup
{: #oc-debug-acct}

Check that your {{site.data.keyword.cloud_notm}} account is set up properly. Some common scenarios that can prevent the default components from running properly include the following:
* If your classic cluster has multiple zones, or if you have a VPC cluster, make sure that you enable [VRF or VLAN spanning](/docs/openshift?topic=openshift-subnets#basics_segmentation). To check if VRF is already enabled, run `ibmcloud account show`. To check if VLAN spanning is enabled, run `ibmcloud oc vlan-spanning get`.
* If some users in the account use a multifactor authentication (MFA) like [TOTP](/docs/account?topic=account-totp), make sure that you [enable MFA](/docs/account?topic=account-enablemfa) for all users in the {{site.data.keyword.cloud_notm}} account.

## Step 2: VPC: Check the public gateway
{: #oc-debug-pgw}

VPC clusters only, with public and private cloud service endpoints enabled: Check that a public gateway is enabled on each VPC subnet that your cluster is attached to. Public gateway are required for default components such as the web console and OperatorHub to use a secure, public connection to complete actions such as pulling images from remote, private registries.

1. Use the {{site.data.keyword.cloud_notm}} console or CLI to [ensure that a public gateway is enabled on each subnet](/docs/openshift?topic=openshift-vpc-subnets#create_vpc_subnet) that your cluster is attached to.
2. Restart the components for the **Developer catalog** in the web console.
    1. Edit the configmap for the samples operator.
        ```sh
        oc edit configs.samples.operator.openshift.io/cluster
        ```
        {: pre}

    2. Change the value of `managementState` from `Removed` to `Managed`.
    3. Save and close the config map. Your changes are automatically applied.

## Step 3: Check firewalls and network policies
{: #oc-debug-firewall}

Check any firewalls or network policies to verify that you do not block any ingress or egress traffic for the OperatorHub or other {{site.data.keyword.openshiftshort}} components.

* If you generated an {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM) allowlist by specifying which IP addresses have access to your cluster, you must [add the CIDRs of the {{site.data.keyword.openshiftlong_notm}} control plane for the zones in the region where your cluster is located to the allowlist](/docs/openshift?topic=openshift-firewall#iam_allowlist).
* Classic only: If you have a firewall, [open the required ports and IP addresses in your firewall](/docs/openshift?topic=openshift-firewall).
* VPC only: If you control traffic with VPC ACLs or security groups, make sure that you allow the minimum required [inbound and outbound rules](/docs/openshift?topic=openshift-firewall).


## Step 4: Check the cluster setup
{: #oc-debug-cluster-setup}

Check that your cluster is set up properly. If you just created your cluster, wait awhile for your cluster components to fully provision.
1. Get the details of your cluster.
    ```sh
    ibmcloud oc cluster get -c <cluster_name_or_ID>
    ```
    {: pre}

2. Review the output of the previous step to check the **Ingress Subdomain**.
    *  If your cluster does **not** have a subdomain, see [No Ingress subdomain exists after cluster creation](/docs/openshift?topic=openshift-ingress_subdomain).
    *  If your cluster does have a subdomain, continue to the next step.
3. Verify that your cluster runs the latest patch **Version**. If your cluster does not run the latest patch version, update the cluster and worker nodes.
    1. [Update the cluster master](/docs/openshift?topic=openshift-update#master) to the latest patch version for your cluster major and minor version.
        ```sh
        ibmcloud oc cluster master update -c <cluster_name_or_ID> --version <major.minor>_openshift-f
        ```
        {: pre}

    2. List your worker nodes.
        ```sh
        ibmcloud oc worker ls -c <cluster_name_or_ID>
        ```
        {: pre}

    3. [Update the worker nodes](/docs/openshift?topic=openshift-update#worker_node) to matchthe cluster master version.
        ```sh
        ibmcloud oc worker update -c <cluster_name_or_ID> -w <worker1_ID> -w <worker2_ID> -w<worker3_ID>
        ```
        {: pre}

4. Check the cluster **State**. If the state is not **normal**, see [Debugging clusters(#debug_clusters).
5. Check the **Master health**. If the state is not **normal**, see [Reviewing master health(#debug_master).
6. Check the worker nodes that the {{site.data.keyword.openshiftshort}} components might run on. If the state is not **normal**, see [Debugging worker nodes](/docs/containers?topic=containers-debug_worker_nodes).
    ```sh
    ibmcloud oc worker ls -c <cluster_name_or_ID>
    ```
    {: pre}

## Step 5: Log in to your cluster
{: #oc-debug-cluster-login}

[Log in to your cluster](/docs/openshift?topic=openshift-access_cluster). Note that if the {{site.data.keyword.openshiftshort}} web console does not work for you to get the login token, you can [access the cluster from the CLI](/docs/openshift?topic=openshift-access_cluster#access_oc_cli).

VPC only: If you enabled the private cloud service endpoint, you must be [connected to the private network through your VPC VPN connection](/docs/openshift?topic=openshift-access_cluster#vpc_private_se) to access the web console.
{: note}

## Step 6: Check the component pods
{: #oc-debug-pods}

Check the health of the {{site.data.keyword.openshiftshort}} component pods that do not work.
1. Check the status of the pod.
    ```sh
    oc get pods -n <project>
    ```
    {: pre}

2. If a pod is not in a **Running** status, describe the pod and check for the events. For example, you might see an error that the pod cannot be scheduled because of a lack of CPU or memory resources, which is common if you have a cluster with less than 3 worker nodes. [Resize your worker pool](/docs/openshift?topic=openshift-add_workers) and try again.
    ```sh
    oc describe pod -n <project> <pod>
    ```
    {: pre}

3. If you do not see any helpful information in the events section, check the pod logs for any error messages or other troubleshooting information.
    ```sh
    oc logs pod -n <project> <pod>
    ```
    {: pre}

4. Restart the pod and check if it reaches a **Running** status.
    ```sh
    oc delete pod -n <project> <pod>
    ```
    {: pre}

## Step 7: Check the system pods
{: #oc-debug-pods-system}

If the pods are healthy, check if other system pods are experiencing issues. Oftentimes to function properly, one component depends on another component to be healthy.

For example, the OperatorHub has a set of images that are stored in external registries such as `quay.io`. These images are pulled into the internal registry to use across the projects in your {{site.data.keyword.openshiftshort}} cluster. If any of the OperatorHub or internal registry components are not set up properly, such as due to lack of permissions or compute resources, the OperatorHub and catalog do not display.


1. Check for pending pods.
    ```sh
    oc get pods --all-namespaces | grep Pending
    ```
    {: pre}

2. Describe the pods and check for the **Events**.
    ```sh
    oc describe pod -n <project_name> <pod_name>
    ```
    {: pre}

    For example, some common messages that you might see from `openshift-image-registry` pods include:
    * A `Volume could not be created` error message because you created the cluster without the correct storage permission. {{site.data.keyword.openshiftlong_notm}} clusters come with a file storage device by default to store images for the system and other pods. Revise your [infrastructure permissions](/docs/openshift?topic=openshift-access_reference#infra) and restart the pod.
    * An `order will exceed maximum number of storage volumes allowed` error message because you have exceeded the combined quota of file and block storage devices that are allowed per account. [Remove unused storage devices](/docs/containers?topic=containers-file_storage#cleanup) or [increase your storage quota](/docs/BlockStorage?topic=BlockStorage-managingstoragelimits), and restart the pod.
    * A message that images cannot be stored because the file storage device is full. [Resize the storage device](/docs/openshift?topic=openshift-file_storage#file_change_storage_configuration) and restart the pod.
    * A `Pull image still failed due to error: unauthorized: authentication required` error message because the internal registry cannot pull images from an external registry. Check that [the image pull secrets](/docs/openshift?topic=openshift-registry#cluster_registry_auth) are set for the project and restart the pod.
3. Check the **Node** that the failing pods run on. If all the pods run on the same worker node, the worker node might have a network connectivity issue. Reload the worker node.
    ```sh
    ibmcloud oc worker reload -c <cluster_name_or_ID> -w <worker_node_ID>
    ```
    {: pre}

## Step 8: Check the OpenVPN
{: #oc-debug-openvpn}



Check that the OpenVPN in the cluster is set up properly.
1. Check that the OpenVPN pod is **Running**.
    ```sh
    oc get pods -n kube-system -l app=vpn
    ```
    {: pre}

2. Check the OpenVPN logs, and check for an `ERROR` message such as `WORKERIP:<port>`, such as`WORKERIP:10250`, that indicates that the VPN tunnel does not work.
    ```sh
    oc logs -n kube-system <vpn_pod> --tail 10
    ```
    {: pre}

3. If you see the worker IP error, check if worker-to-worker communication is broken. Log in to a `calico-node` pod in the `calico-system` project, and check for the same `WORKERIP:10250` error.
    ```sh
    oc exec -n calico-system <calico-node_pod> -- date
    ```
    {: pre}

4. If the worker-to-worker communication is broken, make sure that you enable [VRF or VLAN spanning](/docs/openshift?topic=openshift-subnets#basics_segmentation).
5. If you see a different error from either the OpenVPN or `calico-node` pod, restart the OpenVPN pod.
    ```sh
    oc delete pod -n kube-system <vpn_pod>
    ```
    {: pre}

6. If the OpenVPN still fails, check the worker node that the pod runs on.
    ```sh
    oc describe pod -n kube-system <vpn_pod> | grep "Node:"
    ```
    {: pre}

7. Cordon the worker node so that the OpenVPN pod is rescheduled to a different worker node.
    ```sh
    oc cordon <worker_node>
    ```
    {: pre}

8. Check the OpenVPN pod logs again. If the pod no longer has an error, the worker node might have a network connectivity issue. Reload the worker node.
    ```sh
    ibmcloud oc worker reload -c <cluster_name_or_ID> -w <worker_node_ID>
    ```
    {: pre}

## Step 9: Refresh the cluster master
{: #oc-debug-refresh-master}

Refresh the cluster master to set up the default {{site.data.keyword.openshiftshort}} components. After you refresh the cluster, wait a few minutes to allow the operation to complete.
```sh
ibmcloud oc cluster master refresh -c <cluster_name_or_ID>
```
{: pre}


## Step 10: Retry
{: #oc-debug-retry}

Try to use the {{site.data.keyword.openshiftshort}} component again.

If the error still exists, see [Feedback, questions, and support](/docs/openshift?topic=openshift-get-help).






