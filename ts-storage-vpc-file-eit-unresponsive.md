---

copyright: 
  years: 2024, 2026
lastupdated: "2026-08-12"


keywords: kubernetes, openshift

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}

# Why do I see an `UnresponsiveMountHelperContainerUtility` error for {{site.data.keyword.filestorage_vpc_short}}?
{: #ts-storage-vpc-file-eit-unresponsive}

[Virtual Private Cloud]{: tag-vpc}


Your app that uses encryption in-transit (EIT) with a zonal `dp2` profile {{site.data.keyword.filestorage_vpc_short}} fails with an `UnresponsiveMountHelperContainerUtility` error.
{: tsSymptoms}


Troubleshoot unresponsive VPC file storage systems with EIT (Encrypted In Transit).
{: shortdesc}

You see an error message similar to the following example:

```sh
Code: UnresponsiveMountHelperContainerUtility,
Description: Failed to mount target because unable to make connection to mount helper container service.,
BackendError: Failed to send EIT based request. Failed with error:
  Post "http://unix/api/mount": dial unix /var/lib/ibmshare.sock: connect: no such file or directory,
Action: Check if EIT is enabled from storage operator.
  Run command 'kubectl edit configmap addon-vpc-file-csi-driver-configmap -n kube-system'
  and set 'ENABLE_EIT' flag to 'true'.
```
{: screen}

Either EIT is not enabled on your worker pools, or your app pod is scheduled on a worker pool node where EIT is not enabled. One of the following conditions is true:
{: tsCauses}

- `ENABLE_EIT` is `false` or `EIT_ENABLED_WORKER_POOLS` is empty in the configmap.
- The worker pool that the pod is running on is not listed in `EIT_ENABLED_WORKER_POOLS`.
- On RHCOS worker nodes, the EIT packages are installed but the node has not been rebooted yet to activate them.
- On RHCOS worker nodes, a previous uninstall and reinstall cycle was performed without a reboot in between, leaving the package in a broken "already layered" state.

## Resolving the issue
{: #vpc-file-eit-resolve}

Complete the following steps to identify and resolve the cause.
{: tsResolve}

### Check which nodes have EIT enabled
{: #ts-storage-vpc-file-eit-unresponsive-check-nodes}

Review the `file-csi-driver-status` configmap to see which nodes have EIT packages installed and confirm the configuration is correct.

1. Describe the status configmap to see which nodes have EIT enabled. Look for the `EIT_ENABLED_WORKER_NODES` key, which lists worker pool names and the IP addresses of nodes where EIT installation is complete.

    ```sh
    oc describe cm file-csi-driver-status -n kube-system
    ```
    {: pre}

    Example output:
    ```sh
    EIT_ENABLED_WORKER_NODES:
    ----
    default:
    - 10.240.0.89
    - 10.240.0.87
    - 10.240.0.88
    ```
    {: screen}

    An empty value means no nodes have had EIT installed yet.

1. Verify that `ENABLE_EIT` is set to `true` and that the target worker pool is listed in `EIT_ENABLED_WORKER_POOLS`.

    ```sh
    oc describe cm addon-vpc-file-csi-driver-configmap -n kube-system
    ```
    {: pre}

### Confirm that your app pod is running on an EIT-enabled node
{: #ts-storage-vpc-file-eit-unresponsive-confirm-node}

List your pods to find out which node they are scheduled on, then cross-check against the list from the previous section.

1. List your pods and note the node IP address that each pod is running on.

    ```sh
    oc get pods -A -o wide
    ```
    {: pre}

1. Cross-check the node IP against the `EIT_ENABLED_WORKER_NODES` list from Step 1. If the pod is on a node that is not in that list, do one of the following:
    - Move the pod to an EIT-enabled node by using node selectors or affinity rules.
    - Add the worker pool that contains that node to `EIT_ENABLED_WORKER_POOLS` in the configmap, and wait for the operator to reconcile.

## OS-specific considerations
{: #ts-storage-vpc-file-eit-unresponsive-os}

The required packages are installed differently depending on the worker node operating system.

### Ubuntu and RHEL
{: #ts-storage-vpc-file-eit-unresponsive-ubuntu-rhel}

No reboot is required. The packages become active immediately after installation. If the node IP appears in `EIT_ENABLED_WORKER_NODES` and the pod is on that node, EIT should be functional. If the socket is still missing, check the storage operator pod logs for installation errors.

```sh
oc logs -n kube-system -l app=ibm-vpc-file-csi-operator --tail=100
```
{: pre}

### RHCOS / CoreOS
{: #ts-storage-vpc-file-eit-unresponsive-rhcos}

RHCOS is an immutable operating system. **The packages are not active until the node is rebooted**, even if the node IP already appears in `EIT_ENABLED_WORKER_NODES`.

#### Node shows as EIT-enabled but mount still fails
{: #ts-storage-vpc-file-eit-unresponsive-rhcos-mount-fails}

If the node IP is listed in `EIT_ENABLED_WORKER_NODES` but you still see the `UnresponsiveMountHelperContainerUtility` error, the node has not been rebooted since the packages were installed. The socket `/var/lib/ibmshare.sock` does not exist until after a reboot.

To confirm that a reboot is pending, run the following commands on the affected node:

1. Open a debug shell on the affected node by using the OpenShift CLI.

    ```sh
    oc debug node/<nodeName>
    ```
    {: pre}

1. Inside the debug shell, check whether EIT packages are staged but not yet active.

    ```sh
    chroot /host
    rpm-ostree status
    ```
    {: pre}

    In the output, look for a pending or staged layer that lists `mount-helper` and `mount-helper-container`. If the packages appear in a layer that is **not** marked `(booted)`, a reboot is required to activate them.

    Example output showing packages staged for the next boot:
    ```sh
    State: idle
    Deployments:
      ● ostree-unverified-registry:...
        ...
        LayeredPackages: mount-helper mount-helper-container
    
      ostree-unverified-registry:...  (booted)
        ...
    ```
    {: screen}

To resolve this, drain and reboot the affected RHCOS node to avoid impact to running workloads.

1. Find the worker IDs for the nodes listed in `EIT_ENABLED_WORKER_NODES` by matching their IP addresses.

    ```sh
    ibmcloud ks workers --cluster CLUSTER_ID
    ```
    {: pre}

1. Drain the node to safely evict all running pods before the reboot.

    ```sh
    oc drain <node-name> --ignore-daemonsets --delete-emptydir-data
    ```
    {: pre}

1. Reboot the drained node.

    ```sh
    ibmcloud ks worker reboot --cluster CLUSTER_ID --worker WORKER_ID
    ```
    {: pre}

1. After the node is back online and in `Ready` state, uncordon it to allow workloads to be scheduled on it again.

    ```sh
    oc uncordon <node-name>
    ```
    {: pre}

#### Install job fails with "already layered" error on RHCOS
{: #ts-storage-vpc-file-eit-unresponsive-rhcos-layered}

If you previously uninstalled EIT on an RHCOS worker pool and then re-enabled it without rebooting the node in between, the storage operator install job might fail with an error similar to:

```sh
error: Packages are already layered: mount-helper-<version>.rpm mount-helper-container-<version>.rpm
```
{: screen}

This happens because `rpm-ostree uninstall` only stages the removal. The packages are still present in the current boot layer until a reboot occurs. When the operator tries to run `rpm-ostree install` again, it sees the packages as already installed.

To resolve this:

1. Drain the node to safely evict all running pods before the reboot.

    ```sh
    oc drain <node-name> --ignore-daemonsets --delete-emptydir-data
    ```
    {: pre}

1. Reboot the RHCOS node to apply the pending uninstall.

    ```sh
    ibmcloud ks worker reboot --cluster CLUSTER_ID --worker WORKER_ID
    ```
    {: pre}

1. After the node is back online and in `Ready` state, uncordon it to allow workloads to be scheduled on it again.

    ```sh
    oc uncordon <node-name>
    ```
    {: pre}

1. After the node comes back online, the previously installed packages are gone. The storage operator automatically reinstalls them on the next reconciliation cycle, typically within a few minutes.

1. After the operator reports the node as EIT-enabled in `EIT_ENABLED_WORKER_NODES`, drain and reboot the node again to activate the newly installed packages, then uncordon it.

The complete cycle for RHCOS uninstall then reinstall is: reboot after uninstall → operator reinstalls → reboot again to activate.
{: note}

## New nodes added to an EIT-enabled worker pool
{: #ts-storage-vpc-file-eit-unresponsive-new-nodes}

When a new node joins a worker pool that is already listed in `EIT_ENABLED_WORKER_POOLS`, the storage operator automatically installs EIT packages on the new node during its next reconciliation cycle. No configmap update is required.

For RHCOS nodes, you must still drain and reboot the node after installation before EIT becomes active. Drain the node, reboot it, and then uncordon it to reduce impact to running workloads. Until the node is rebooted, any pod that uses an EIT-enabled PVC and is scheduled on that new node sees the same `UnresponsiveMountHelperContainerUtility` error. Ubuntu (IKS) and RHEL (ROKS) nodes do not require a reboot when a new node is added.
