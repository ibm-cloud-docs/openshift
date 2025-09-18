---

copyright: 
  years: 2014, 2025
lastupdated: "2025-09-18"


keywords: openshift, {{site.data.keyword.openshiftlong_notm}}, support, get help

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}



# Contacting support
{: #get-help}

Still having issues with your cluster? Review different ways to get help and support for your {{site.data.keyword.openshiftlong_notm}} clusters. For any questions or feedback, post in Slack.
{: shortdesc}

Before you open a support case, gather relevant information about your cluster environment.
{: tip}

## Get your cluster details
{: #cluster-details}

1. Get your cluster details.

    ```sh
    ibmcloud oc cluster get -c <cluster_name_or_ID>
    ```
    {: pre}

2. If your issue involves worker nodes, get the worker node details.

    1. List all worker nodes in the cluster, and note the **ID** of any worker nodes with an unhealthy **State** or **Status**.
    
        ```sh
        ibmcloud oc worker ls -c <cluster_name_or_ID>
        ```
        {: pre}

    2. Get the details of the unhealthy worker node.
    
        ```sh
        ibmcloud oc worker get -w <worker_ID> -c <cluster_name_or_ID>
        ```
        {: pre}

3. For issues with resources within your cluster such as pods or services, log in to the cluster and use the Kubernetes API to get more information about them.

    You can also use the [{{site.data.keyword.containerlong_notm}} Diagnostics and Debug Tool](/docs/openshift?topic=openshift-debug-tool) to gather and export pertinent information to share with IBM Support.
    {: tip}



## Gather error logs and other information
{: #gather-logs}

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

Example commands to collect the logs from a given time.

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

1. Start a toolbox container, which includes the required binaries and plug-ins to run the `sosreport`.
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





## Open a support case
{: #support-case}

1. Contact IBM Support by [opening a case](https://cloud.ibm.com/unifiedsupport/cases/form){: external}.

1. For the **Problem type**, search for or select {{site.data.keyword.openshiftlong_notm}}.

1. For the **Case details**, provide a descriptive title and include the details that you previously gathered. From the **Resources**, you can also select the cluster that the issue is related to.

1. Be as specific as possible and include and architecture diagrams or supplemental materials that you think you could help IBM Support troubleshoot the issue.
