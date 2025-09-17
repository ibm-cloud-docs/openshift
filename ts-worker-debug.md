---

copyright: 
  years: 2014, 2025
lastupdated: "2025-09-17"


keywords: openshift, kubernetes, help, network, connectivity, {{site.data.keyword.openshiftlong_notm}}

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}


# Debugging worker nodes
{: #debug_worker_nodes}
{: troubleshoot}
{: support}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf}

Review the options to debug your worker nodes and find the root causes for failures.
{: shortdesc}


## Check worker node notifications and maintenance updates
{: #worker-debug-notifs}

Check the {{site.data.keyword.cloud_notm}} health and status dashboard for any notifications or maintenance updates that might be relevant to your worker nodes. These notifications or updates might help determine the cause of the worker node failures.

1. [Classic clusters]{: tag-classic-inf} Check the [health dashboard](https://cloud.ibm.com/gen1/infrastructure/health-dashboard){: external} for any {{site.data.keyword.cloud_notm}} emergency maintenance notifications that might affect classic worker nodes in your account. Depending on the nature of the maintenance notification, you might need to reboot or reload your worker nodes. 
1. Check the {{site.data.keyword.cloud_notm}} [status dashboard](https://cloud.ibm.com/status){: external} for any known problems that might affect your worker nodes or cluster. If any of the following components show an error status, that component might be the cause of your worker node disruptions. 
    - For all clusters, check the **Kubernetes Service** and **Container Registry** components.
    - For Red Hat OpenShift clusters, check the **Red Hat OpenShift on IBM Cloud** component.
    - For VPC clusters, check the **Virtual Private Cloud**, **Virtual Private Endpoint** and **Virtual Server for VPC** components.
    - For Classic clusters, check the **Classic Infrastructure Provisioning** and **Virtual Servers** components.


## Quick steps to resolve worker node issues
{: #worker-debug-quick}

If your worker node is not functioning as expected, you can follow these steps to update your cluster and command line tools or run diagnostic tests. If the issue persists, see [Debugging your worker node](#worker-debug-steps) for additional steps. 
{: shortdesc}

1. [Update your cluster and worker nodes to the latest version](/docs/openshift?topic=openshift-update#update).
2. [Update your command line tools](/docs/openshift?topic=openshift-cli-update).
3. [Run tests in the Diagnostics and Debug Tool add-on](/docs/openshift?topic=openshift-debug-tool). 


## Debugging your worker node
{: #worker-debug-steps}

### Step 1: Get the worker node state
{: #worker-debug-get-state}

If your cluster is in a **Critical**, **Delete failed**, or **Warning** state, or is stuck in the **Pending** state for a long time, review the state of your worker nodes.

```sh
ibmcloud oc worker ls --cluster <cluster_name_or_id>
```
{: pre}

### Step 2: Review the worker node state
{: #worker-debug-rev-state}

Review the **State** and **Status** field for every worker node in your CLI output.

For more information, see [Worker node states](/docs/openshift?topic=openshift-worker-node-state-reference).

### Step 3: Get the details for each worker node
{: #worker-debug-get-details}

Get the details for the worker node. If the details include an error message, review the list of [common error messages for worker nodes](/docs/openshift?topic=openshift-common_worker_nodes_issues) to learn how to resolve the problem.

```sh
ibmcloud oc worker get --cluster <cluster_name_or_id> --worker <worker_node_id>
```
{: pre}

### Step 4: Review the infrastructure provider for the worker node
{: #worker-debug-rev-infra}

Review the infrastructure environment to check for other reasons that might cause the worker node issues.
1. Check with your networking team to make sure that no recent maintenance, such as firewall or subnet updates, might impact the worker node connections.
2. Review [{{site.data.keyword.cloud_notm}}](https://cloud.ibm.com/status/){: external} for **{{site.data.keyword.openshiftlong_notm}}** and the underlying infrastructure provider, such as **Virtual Servers** for classic, **VPC** related components, or **{{site.data.keyword.satelliteshort}}**.
3. If you have access to the underlying infrastructure, such as classic **Virtual Servers**, review the details of the corresponding machines for the worker nodes.




### Step 5: Gather the logs and other details about your worker nodes
{: #worker-debug-must-gather}

### Running the `must-gather` command
{: #must-gather-oc}

The `oc adm must-gather` CLI command collects the information from your cluster for debugging issues. The must-gather tool collects resource definitions, service logs, and more. Note that audit logs are not collected as part of the default set of information to reduce the size of the files.

When you run `oc adm must-gather`, a new pod with a random name is created in a new project on the cluster. The data is collected on that pod and saved in a new directory that starts with `must-gather.local`.

Review the following example commands.

```sh
oc adm must-gather
```
{: pre}

Example command to collect data related to one or more specific features, use the `--image` argument with a specific image.

```sh
oc adm must-gather \
--image=registry.redhat.io/container-native-virtualization/cnv-must-gather-rhel9:v4.17.5
```
{: pre}

Example command to collect audit logs.

```sh
oc adm must-gather -- /usr/bin/gather_audit_logs
```
{: pre}


Example command to run must-gather in a specific namespace.
```sh
oc adm must-gather --run-namespace <namespace> \
--image=registry.redhat.io/container-native-virtualization/cnv-must-gather-rhel9:v4.17.5
```
{: pre}

Example commands to collect the logs from a given time frame.

```sh
oc adm must-gather --since=24h
```
{: pre}

```sh
oc adm must-gather --since-time=$(date -d '-24 hours' +%Y-%m-%dT%T.%9N%:z )
```
{: pre}

Example command to collect network logs.

```sh
oc adm must-gather -- gather_network_logs
```
{: pre}

For more examples and arguments run the following command

```sh
oc adm must-gather -h
```
{: pre}

Example command to create a compressed file from the must-gather directory.
```sh
tar cvaf must-gather.tar.gz must-gather.local.5421342344627712289/
```
{: pre}

Attach the compressed file to your support case.

### Gathering an SOS report
{: #sos-report-oc}

`sosreport` is a tool that collects configuration details, system information, and diagnostic data from Red Hat Enterprise Linux (RHEL) and Red Hat Enterprise Linux CoreOS (RHCOS) systems. It provides a standardized way to collect diagnostic information relating to a node, which can then be provided to support for issue diagnosis.

In some support interactions, support might ask you to collect a `sosreport` archive for a specific OpenShift Container Platform node. For example, it might be necessary to review system logs or other node-specific data that is not included within the output of `oc adm must-gather`.

The recommended way to generate a `sosreport` for an OpenShift Container Platform cluster node is through a debug pod.

[Access your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-access_cluster).

1. List your worker nodes.
    ```sh
    oc get nodes
    ```
    {: pre}

1.  Start a a debug session on the target node.
    ```sh
    oc debug node/node_name
    ```
    {: pre}

    To enter into a debug session on the target node that is tainted with the `NoExecute` effect, add a toleration to a temporary namespace, and start the debug pod in the temp namespace.
    {: note}

    ```sh
    oc new-project temp oc patch namespace temp --type=merge -p '{"metadata": {"annotations": { "scheduler.alpha.kubernetes.io/defaultTolerations": "[{\"operator\": \"Exists\"}]"}}}'
    ```
    {: pre}

    ```sh
    oc debug node/my-cluster-node
    ```
    {: pre}

1. Set `/host` as the root directory within the debug shell. The debug pod mounts the host’s root file system in `/host` within the pod. By changing the root directory to `/host`, you can run binaries contained in the host’s executable paths.
    ```sh
    chroot /host
    ```
    {: pre}

    OpenShift Container Platform cluster nodes running Red Hat Enterprise Linux CoreOS (RHCOS) are immutable and rely on Operators to apply cluster changes. Accessing cluster nodes by using SSH is not recommended. However, if the OpenShift Container Platform API is not available, or the kubelet is not properly functioning on the target node, oc operations might be impacted. In such situations, it is possible to access nodes using `ssh core@<node>.<cluster_name>.<base_domain>` instead.
    {: note}

1. Start a toolbox container, which includes the required binaries and plugins to run the `sosreport`.
    ```sh
    toolbox
    ```
    {: pre}


    If an existing toolbox pod is already running, the toolbox command outputs `'toolbox-' already exists. Trying to start….` Remove the running toolbox container with `podman rm toolbox-` and start a new toolbox container.
    {: note}

1. Run the `sos report` command and follow the prompts to collect troubleshooting data.
    ```sh
    sos report -k crio.all=on -k crio.logs=on -k podman.all=on -k podman.logs=on
    ```
    {: pre}
    
    Example command to include information on OVN-Kubernetes networking configurations from a node in your report.
    ```sh
    sos report --all-logs
    ```
    {: pre}

    The `sosreport` output provides the archive’s location and checksum. The following sample output references support case ID 01234567. The file path is outside of the `chroot` environment because the toolbox container mounts the host’s root directory at `/host`.
    ```sh
    Your sosreport has been generated and saved in:
    /host/var/tmp/sosreport-my-cluster-node-01234567-2020-05-28-eyjknxt.tar.xz
    The checksum is: 382ffc167510fd71b4f12a4f40b97a4e
    ```
    {: screen}

1. Output the `sosreport` to a file.

    The debug container mounts the host’s root directory at `/host`. Reference the absolute path from the debug container’s root directory, including `/host`, when specifying target files for concatenation.
    {: tip}

    ```sh
    oc debug node/my-cluster-node -- bash -c 'cat /host/var/tmp/sosreport-my-cluster-node-01234567-2020-05-28-eyjknxt.tar.xz' > /tmp/sosreport-my-cluster-node-01234567-2020-05-28-eyjknxt.tar.xz
    ```
    {: pre}

    OpenShift Container Platform cluster nodes running Red Hat Enterprise Linux CoreOS (RHCOS) are immutable and rely on Operators to apply cluster changes. Transferring a `sosreport` archive from a cluster node by using `scp` is not recommended. However, if the OpenShift Container Platform API is not available, or the kubelet is not properly functioning on the target node, `oc` operations might be impacted. In such situations, it is possible to copy a `sosreport` archive from a node by running `scp core@<node>.<cluster_name>.<base_domain>:<file_path> <local_path>`.
    {: note}

1. Upload the file to your support case.
