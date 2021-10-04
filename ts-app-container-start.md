---

copyright: 
  years: 2014, 2021
lastupdated: "2021-10-04"

keywords: openshift, roks, rhoks, rhos

subcollection: openshift
content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}



# Why don't my containers start?
{: #ts-app-container-start}


You notice one or more of the following issues:
{: tsSymptoms}

* Worker nodes are unable to create new pods. The pods deploy successfully to worker nodes, but the containers are stuck in the `ContainerCreating` state.
* When you run `oc describe pod <pod>` for a pod in the `ContainerCreating` state, you see an event similar to the following.

    ```sh
    Failed to create pod sandbox: rpc error: code = Unknown desc = failed to setup network for sandbox "XXX": failed to request 1 IPv4 addresses. IPAM allocated only 0
    ```
    {: screen}

* One or more of the `calico-node` pods fail to start on a worker node and are in the `CrashLoopBackOff` state. When you run `kubectl logs -n kube-system <calico-node_pod>`, the last lines of the logs contain the following message.

    ```sh
    Unable to autoassign an address - pools are likely exhausted. type="ipipTunnelAddress"
    ```
    {: screen}


If you do not see either of the IP address-related messages that are listed in the symptoms, your containers might not start because the registry quota was reached.
{: tsCauses}

If you see either of the IP address-related messages that are listed in the symptoms, your containers might not start because the IP Address Manager (IPAM) for the Calico plug-in incorrectly detects that all pod IP addresses in the cluster are in use. Because the Calico IPAM detects no available IP addresses, it does not assign IP addresses to new pods in the cluster, and pods cannot start.


## Fixing registry quota issues
{: #regitry-quota}
{: tsResolve}

**Infrastructure provider**:
* ![Classic infrastructure provider icon.](images/icon-classic-2.svg) Classic
* ![VPC infrastructure provider icon.](images/icon-vpc-2.svg) VPC

To fix registry quota issues, [free up storage in {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-registry_quota#registry_quota_freeup).
{: shortdesc}

## Fixing IP address issues
{: #calico-ips}

To fix IP address issues, release individual and blocks of IP addresses that were not cleanly removed from the Calico IPAM records so that they can be reused by pods in your cluster.
{: shortdesc}

**Infrastructure provider and versions**:
* ![Classic infrastructure provider icon.](images/icon-classic-2.svg) Classic
* ![VPC infrastructure provider icon.](images/icon-vpc-2.svg) VPC

Your cluster must run a [supported version](/docs/openshift?topic=openshift-openshift_versions#version_types). If you cluster runs a deprecated or unsupported version, first [update your cluster](/docs/containers?topic=containers-update).


### Step 1: Releasing individual IP addresses
{: #individual-ips}

First, check for and release individual IP addresses that were not cleanly removed from the Calico IPAM records so that they can be reused by pods in your cluster.
{: shortdesc}

1. Follow the steps in [Installing and configuring the Calico CLI](/docs/containers?topic=containers-network_policies#cli_install) to download version 3.18 or later of the `calicoctl` client, use the correct Calico configuration for your cluster, and verify that the Calico configuration is working correctly for your targeted cluster. Note that even if you cluster runs an older version of Calico, you can still use `calicoctl` version 3.18 to run the commands in the following steps.

2. Check for any IP addresses that are incorrectly detected as in use by the Calico IPAM.
    ```sh
    calicoctl ipam check
    ```
    {: pre}

3. In the output, look for the section that contains the line `Scanning for IPs that are allocated but not actually in use...`. If IP addresses are allocated in IPAM but are not actually in use, continue to the next step to release them. In this example output, 181 IP addresses can be released.

    ```sh
    ...
    Scanning for IPs that are allocated but not actually in use...
    Found 181 IPs that are allocated in IPAM but not actually in use.
    Scanning for IPs that are in use by a workload or node but not allocated in IPAM...
    Found 0 in-use IPs that are not in active IP pools.
    Found 0 in-use IPs that are in active IP pools but have no corresponding IPAM allocation.

    Check complete; found 181 problems.
    ```
    {: screen}

4. Release IP addresses from the Calico IPAM that were previously assigned to a pod endpoint. Note that after you lock the data store in the following steps, existing pods continue to run, but any pods that are created remain in the `ContainerCreating` state and cannot start until you unlock the data store. This data store lock ensures that the IPAM records are not modified while you release IP addresses. For more information, see the [Calico open source documentation](https://docs.projectcalico.org/reference/calicoctl/ipam/check){: external}.

    1. Lock the data store for the Calico IPAM records.
        ```sh
        calicoctl datastore migrate lock
        ```
        {: pre}

    2. Save the IPAM check results.
        ```sh
        calicoctl ipam check -o report.json
        ```
        {: pre}

    3. Release unused IP addresses. This process can run for up to 20 minutes depending on how many IP addresses must be released.
        ```sh
        calicoctl ipam release --from-report=report.json
        ```
        {: pre}

    4. Unlock the data store.
        ```sh
        calicoctl datastore migrate unlock
        ```
        {: pre}

    5. Verify that all unused IP addresses are released.
        ```sh
        calicoctl ipam check
        ```
        {: pre}

        Example output

        ```sh
        Check complete; found 0 problems.
        ```
        {: screen}

5. Optional: To verify that the data store was successfully unlocked and that IP addresses are now available for assignment, create a pod and check that it starts correctly.

    1. For example, create a simple NGNINX pod.
        ```sh
        oc run test --image=nginx --generator=run-pod/v1
        ```
        {: pre}

    2. Verify that the pod has an IP address and is running successfully.
        ```sh
        oc get po test
        ```
        {: pre}

    3. Delete the test pod.
        ```sh
        oc delete pod test
        ```
        {: pre}

6. Continue to the next section to check for unused IP address blocks.

### Step 2: Releasing IP address blocks
{: #releasing-individual-ips}

Next, check for and clean up entire blocks of IP addresses that are assigned to a worker node but are not used by that worker node.
{: shortdesc}

Occasionally, when a worker node is assigned a second or third block of IP addresses, entire blocks of IP addresses that the worker node previously used might later be completely unused. Additionally, when you remove or replace a worker node, the cleanup of the IP address block by the Calico IPAM might fail due to the lack of a worker node for the `calico-kube-controllers` to temporarily run on, or due to problems with the CNI plug-in or `containerd` runtime when the worker node is removed or replaced.

Ensuring that IP blocks are free is especially important for all classic clusters that run Kubernetes version 1.19 or later and all VPC clusters. In these clusters, the `strictAffinity` Calico setting is set to `true`, which forces a worker node to use IP addresses that are from its assigned IP blocks only, as opposed to using IP addresses from blocks that are assigned to other worker nodes. Over time, the blocks that are assigned to nodes but that are unused can accumulate until no more IP address blocks can be assigned to worker nodes.

1. Follow the steps to [release individual IP addresses](#individual-ips).

2. Choose whether to lock the data store for the Calico IPAM records.
    - If you lock the data store, existing pods continue to run, but any pods that are created remain in the `ContainerCreating` state and cannot start until you unlock the data store. This data store lock ensures that pods cannot be created after you check for unused blocks, but before you release the blocks.
    - If you do not lock the data store, you must immediately verify that no new pods used IP addresses from a released block that you deleted.
    ```sh
    calicoctl datastore migrate lock
    ```
    {: pre}

3. List the Calico IPAM records. In the output, look for blocks that have 0 `IPS IN USE`, which indicates that the block is not used by its assigned worker node.
    ```sh
    calicoctl ipam show --show-blocks
    ```
    {: pre}

    In this example output, the `172.24.10.64/26` block has no IP addresses in use.
    ```sh
    ...
    Block    | 172.24.10.64/26  |        64 | 0 (0%)     | 64 (100%)  |
    ...
    ```
    {: screen}

4. For each of these blocks, complete the following steps to release the block.

    1. Verify that no pods currently use an IP address from the block.
        ```sh
        oc get pods -A
        ```
        {: pre}

    2. Get the `BlockAffinity` for the block. Replace the periods and forward slash in the block with hyphens (-). For example, for the block `172.24.10.64/26`, the format for the following command is `172-24-10-64-26`.
        ```sh
        oc get blockaffinity | grep <block>
        ```
        {: pre}

    3. Delete the `BlockAffinity`.
        ```sh
        oc delete blockaffinity <block_affinity>
        ```
        {: pre}

    4. Get the `IPAMBlock` for the block. Replace the periods and forward slash in the block with hyphens (-). For example, for the block `172.24.10.64/26`, the format for the following command is `172-24-10-64-26`.
        ```sh
        oc get ipamblock | grep <block>
        ```
        {: pre}

    5. Delete the `IPAMBlock`.
        ```sh
        oc delete ipamblock <ipam_block>
        ```
        {: pre}

    6. If you did not lock the data store in step 2: Check that no pods were created directly before you deleted the `BlockAffinity` and `IPAMBlock`. If pods were created, you must delete the `BlockAffinity` and `IPAMBlock` for this block again. Then, delete any pods that use an IP address in this block by running `oc delete pod <pod>` so the pod is recreated with an IP address from a different block.
        ```sh
        oc get pods -A
        ```
        {: pre}

    7. Repeat these steps for any other blocks that that have 0 `IPS IN USE`.

5. If you locked the data store in step 2: Unlock the data store.
    ```sh
    calicoctl datastore migrate unlock
    ```
    {: pre}







