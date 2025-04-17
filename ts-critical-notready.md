---

copyright:
  years: 2023, 2025
lastupdated: "2025-04-17"


keywords: critical, not ready, notready, troubleshooting, worker node status, status

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}

# Troubleshooting worker nodes in `Critical` or `NotReady` state
{: #ts-critical-notready}

Cluster worker nodes go into a `Critical` or `NotReady` state when they stop communicating with the cluster master. When this occurs, your worker nodes are marked as `Critical` in the {{site.data.keyword.cloud_notm}} UI or when you run `ibmcloud oc worker` commands, and as `NotReady` in the Red Hat OpenShift dashboards and when you run `oc get nodes`. There are several reasons why communication stops between worker nodes and the cluster master. Follow these steps to troubleshoot worker nodes in these states. 
{: shortdesc}

Check the {{site.data.keyword.cloud_notm}} health and status dashboard for any notifications or maintenance updates that might be relevant to your worker nodes. These notifications or updates might help determine the cause of the worker node failures.
{: important}


## Check the common causes of worker node failures
{: #ts-critical-notready-common}

There are several reasons why communication stops between worker nodes and the cluster master. Check whether the following common issues are causing the disruption.

The worker was deleted, reloaded, updated, replaced, or rebooted
:   Worker nodes might temporarily show a `Critical` or `NotReady` state when they are deleted, reloaded, updated, or replaced. If any of these actions have been initiated on your worker node, whether manually or as part of an automation setup such as cluster autoscaler, wait until the actions are complete. Then, check the status of your worker nodes again. If any workers remain in the `Critical` or `NotReady` state, [reload](/docs/openshift?topic=openshift-kubernetes-service-cli&interface=ui#cs_worker_reload) or [replace](/docs/openshift?topic=openshift-kubernetes-service-cli&interface=ui#cli_worker_replace) the affected workers. 
:   If a worker node was reloaded or replaced and initially works correctly, but then after some time goes back into a `Critical` or `NotReady` state, then it is likely that some workload or component on the worker is causing the issue. See [Debugging worker nodes](/docs/openshift?topic=openshift-debug-kube-nodes) to isolate the problem workload.

A worker node might end up in a `Critical` or `NotReady` state if it was rebooted without first being cordoned and drained. If this is the case, waiting for the reboot to complete does not resolve the issue. [Reload](/docs/openshift?topic=openshift-kubernetes-service-cli&interface=ui#cs_worker_reload) or [replace](/docs/openshift?topic=openshift-kubernetes-service-cli&interface=ui#cli_worker_replace) the affected worker. If the issue persists, continue with the troubleshooting steps. 
{: note}

The worker node was unintentionally powered down
:   [Classic clusters]{: tag-classic-inf} In the [IBM Cloud console resource list](https://cloud.ibm.com/resources){: external}, worker nodes on classic infrastructure are classified as **compute resources**, or virtual machines. Sometimes a user might not realize that these resources function as cluster worker nodes, and might unintentionally power the worker nodes down. Worker nodes that are powered down might show up in the `Critical` or `NotReady` state. Ensure that the affected worker nodes are not powered down. 


## Troubleshooting steps
{: #ts-critical-notready-steps}

If your worker nodes remain in the `Critical` or `NotReady` state after addressing the [common causes](#ts-critical-notready-common), continue with the following troubleshooting steps.

If a worker node that you previously reloaded or replaced is in the `deploy_failed` or `provision_failed` state when you run `ibmcloud ks workers`, follow the steps in the [All worker nodes in a cluster are affected](#ts-critical-notready-steps-all) section, even if not all nodes are affected. If a different state is indicated, see [Worker node states](/docs/openshift?topic=openshift-worker-node-state-reference) for steps to troubleshoot the new worker. Do not replace or reload any additional worker nodes. 
{: tip}

### If one or some worker nodes are affected
{: #ts-critical-notready-steps-some}

If only some, but not all, of the worker nodes in your cluster are in a `Critical` or `NotReady` state, follow these steps to determine the cause of the disruption and resolve the issue. If the affected worker nodes are all from the same zone, subnet, or VLAN, continue to the next section.

1. Get the details of the specific node. 

    ```sh
    oc describe node <node-IP-address>
    ```
    {: pre}

2. In the output, check the **Conditions** section to determine if the node is experiencing any memory, disk or PID issues. This information might indicate that the node is running low on that type of resource. This situation might occur for one of the following reasons:
    - Memory or CPU exhaustion caused by a lack of proper requests and limits on your pods.
    - Worker disks are full, sometimes because of large pod logs or pod output to the node itself.
    - Slow memory leaks that build up over time, which can cause problems for workers that have not been updated in over a month.
    - Bugs and crashes that affect the Linux kernel.

3. If you are able to determine the cause of the issue from the information in the **Conditions** section, follow the steps in [Debugging worker nodes](/docs/openshift?topic=openshift-debug-kube-nodes) to isolate the problem workload.

4. If the previous steps do not solve the issue, [reload](/docs/openshift?topic=openshift-kubernetes-service-cli&interface=ui#cs_worker_reload) or [replace](/docs/openshift?topic=openshift-kubernetes-service-cli&interface=ui#cli_worker_replace) the affected workers one at a time. 

### If all worker nodes in a single zone, subnet, or VLAN are affected
{: #ts-critical-notready-steps-zone}

If all worker nodes in one zone, subnet, or VLAN are in a `Critical` or `NotReady` state, but all other worker nodes in the cluster are functioning normally, there might be an issue with a networking component. Follow the steps in [If all worker nodes in a cluster are affected](#ts-critical-notready-steps-all), especially to the steps regarding any networking components that might affect the zone, subnet or VLAN, such as firewall or gateway rules, ACLs or custom routes, or Calico and Kubernetes network policies.

If you checked your networking components and still cannot resolve the issue, [gather your worker node data](#ts-critical-notready-gather) and open a support ticket. 


### If all worker nodes in a cluster are affected 
{: #ts-critical-notready-steps-all}

If all the worker nodes in your cluster show `Critical`or `NotReady` at the same time, there might be a problem with either the cluster `apiserver` or the networking path between the workers and the `apiserver`. Follow these troubleshooting steps to determine the cause and resolve the issue.

Some steps are specific to a specialized area, such as networking or automation. Consult with the relevant administrator or team in your organization before completing these steps. 
{: note}

1. Check if there were any recent changes to your cluster, environment, or account that might impact your worker nodes. If so, revert the changes and then check the worker node status to determine if the changes caused the issue.
    - For classic clusters, check any firewall or gateway, such as Virtual Router Appliance, Vyatta, or Juniper that manages traffic for cluster workers. Look for changes or issues that might drop or redirect traffic from cluster workers. 
    - For VPC clusters, check if any changes were made to the default security group and ACLs on the VPC or the worker nodes. If any modifications were made, ensure that you are allowing all necessary traffic from the cluster worker nodes to the cluster master, container registry, and other critical services. For more information, see [Controlling Traffic with VPC Security Groups](/docs/openshift?topic=openshift-vpc-security-group&interface=ui) and [Controlling traffic with ACLs](/docs/openshift?topic=openshift-vpc-acls&interface=ui).
    - For VPC clusters, check any custom routing rules for changes that might be blocking traffic from the cluster `apiserver`.
    - Check any Calico or Kubernetes network policies that are applied to the cluster and make sure that they do not block traffic from the worker node to the cluster `apiservice`, container registry, or other critical services. 
1. Check if the applications, security, or monitoring components in your cluster are overloading the cluster `apiserver` with requests, which might cause disruptions for your worker nodes.
1. If you recently added any components to your cluster, remove them. If you made changes to any existing components in your cluster, revert the changes. Then, check the status of your worker nodes to see if the new components or changes were causing the issue. 
1. Check for changes on any cluster webhooks, which can disrupt `apiserver` requests or block a worker node's ability to connect with the `apiserver`. Check for webhooks that are rejecting requests. Run the following command to get a list of webhooks that are rejecting requests.

    ```sh
    kubectl get --raw /metrics | grep apiserver_admission_webhook_admission_duration_seconds
    ```
    {: pre}

1. Review the output for webhooks that have `rejected="true"` status.


1. Remove and regenerate any custom Docker pull secrets, which, if misconfigured, can prevent worker nodes from pulling images from Docker registries. 
    1. Run the `ibmcloud oc delete secret -n openshift pull-secret` and `ibmcloud oc delete secret -n openshift-config pull-secret` commands to delete the custom Docker pull secrets.
        ```sh
        ibmcloud oc delete secret -n openshift pull-secret
        ```
        {: pre}

        ```sh
        ibmcloud oc delete secret -n openshift-config pull-secret
        ```
        {: pre}

    1. Wait for the cluster to regenerate the custom Docker pull secrets. Any misconfigured components are no longer present in the regenerated pull secrets.
1. Check the status of your worker nodes. If they are in a `Normal` state, add back any deleted components and re-create any reverted changes, one by one, until you can determine which configuration or component caused the worker node disruption. 
1. If the issue is still not resolved, follow the steps to [gather your worker node data](#ts-critical-notready-gather) and open a support ticket. 


### If worker nodes switch between normal and critical states
{: #ts-critical-notready-steps-switch}

If your worker nodes switch between a `Normal` and `Critical` or `NotReady` state, check the following components for any issues or recent changes that might disrupt your worker nodes.


1. For classic clusters, check your firewalls or gateways. If there is a bandwidth limit or any type of malfunction, resolve the issue. Then, check your worker nodes again.
1. Check if the applications, security, or monitoring components in your cluster are overloading the cluster `apiserver` with requests, which might cause disruptions for your worker nodes.
1. If you recently added any components to your cluster, remove them. If you made changes to any existing components in your cluster, revert the changes. Then, check the status of your worker nodes to see whether the new components or changes were causing the issue. 
1. Check for changes on any cluster webhooks, which can disrupt `apiserver` requests or block a worker node's ability to connect with the `apiserver`. Check for webhooks that are rejecting requests. Run the following command to get a list of webhooks that are rejecting requests.

    ```sh
    kubectl get --raw /metrics | grep apiserver_admission_webhook_admission_duration_seconds
    ```
    {: pre}

1. Review the output for webhooks that have `rejected="true"` status.
1. If the issue is still not resolved, follow the steps to [gather your worker node data](#ts-critical-notready-gather) and open a support ticket. 


## Gathering data for a support case
{: #ts-critical-notready-gather}

If you are unable to resolve the issue with the troubleshooting steps, gather information about your worker nodes. Then, [open a support ticket](https://cloud.ibm.com/unifiedsupport/cases/form){: external} and include the worker node information you gathered.
{: shortdesc}

Before you open a support ticket, review the information and follow any troubleshooting steps in [Debugging worker nodes](/docs/openshift?topic=openshift-debug_worker_nodes), [Worker node states](/docs/openshift?topic=openshift-worker-node-state-reference), and [Troubleshooting worker nodes in `Critical` or `NotReady` state](#ts-critical-notready).
{: important}

If all worker nodes in a cluster, or in one region, subnet, or VLAN are affected, you can open an initial support ticket without gathering data. However, you might later be asked to gather the relevant data. If only one or some of your worker nodes are affected, you must gather the relevant data to include in your support ticket. 
{: note}


### Before you begin
{: #ts-critical-notready-gather-before}

Check the conditions of your worker nodes and cluster before you gather data.

1. Check the CPU and memory level of your nodes. If any node is over 80% in either CPU or memory usage, consider provisioning more nodes or reducing your workload. 

    ```sh
    oc top node 
    ```
    {: pre}

    Example output 

    ```sh
    NAME            CPU(cores)   CPU%   MEMORY(bytes)   MEMORY%   
    10.001.1.01     640m         16%    6194Mi          47%       
    10.002.2.02     2686m        68%    4024Mi          30%       
    10.003.3.03     2088m        53%    10735Mi         81%  
    ```
    {: screen}

1. Check for changes on any cluster webhooks, which can disrupt `apiserver` requests or block a worker node's ability to connect with the `apiserver`. Check for webhooks that are rejecting requests. Run the following command to get a list of webhooks that are rejecting requests.

    ```sh
    kubectl get --raw /metrics | grep apiserver_admission_webhook_admission_duration_seconds
    ```
    {: pre}

1. Review the output for webhooks that have `rejected="true"` status.

### Gathering data
{: #ts-critical-notready-gather-steps}

Follow the steps to gather the relevant worker node data.

1. Get the details of each node. Save the output details to include in your support ticket.

    ```sh
    oc describe node <node-ip-address>
    ```
    {: pre}

2. Run the [Diagnostics and Debug Tool](/docs/openshift?topic=openshift-debug-tool)  and the [OpenShift Diagnostics and Debug Tool](/docs/openshift?topic=openshift-debug-tool). Export the kube and network test results to a compressed file and save the file to include in your support ticket. If all workers in your cluster are affected, you can skip this step as the debug tools cannot work properly if all worker nodes are disrupted.

3. Show that there are no added mutating or validating webhooks remaining in your cluster by getting the webhook details. Save the command output to include in your support ticket. Note that the following mutating webhooks might remain and do not need to be deleted: `alertmanagerconfigs.openshift`, `managed-storage-validation-webhooks`, `multus.openshift.io`, `performance-addon-operator`, `prometheusrules.openshift.io`,`snapshot.storage.k8s.io`.

    ```sh
    kubectl get mutatingwebhookconfigurations
    ```
    {: pre}

    ```sh
    kubectl get validatingwebhookconfigurations
    ```
    {: pre}

4. [Classic clusters]{: tag-classic-inf}: Access the KVM console for one of the affected workers. Then, gather the relevant logs and output. 
    1. Follow the steps to access the [KVM console](/docs/virtual-servers?topic=virtual-servers-access-kvm-console).
    2. Gather and save the following logs. Review the logs for possible causes of the worker node disruption, such as a lack of memory or disk space, the disk entering read-only mode, and other issues.
        - /var/log/boot.log
        - /var/log/calico/cni/cni.log
        - /var/log/crio.log
        - /var/log/cron
        - /var/log/messages
        - /var/log/secure
        - /var/log/kubelet.log
    3.  Run the following commands and save the output to attach to the support ticket.
        - `ps -aux`                     # Dump running process
        - `df -H`                       # Dump disk usage information
        - `vmstat`                      # Dump memory usage information
        - `lshw`                        # Dump hardware information
        - `last -Fxn2 shutdown reboot`  # determine if last restart was graceful or not
        - `mount | grep -i "(ro"`       # to rule out disk read-only issue.  NOTE: `tmpfs` being `ro` is fine
        - `touch /this`                 # to rule out disk read-only issue
5. [Open a support ticket](https://cloud.ibm.com/unifiedsupport/cases/form){: external} and attach all the outputs saved in the previous steps.
