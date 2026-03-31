---

copyright:
  years: 2022, 2026
lastupdated: "2026-03-31"


keywords: rhel, os, operating system, rhel 9, 418, migration, vpc, rhcos

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}



# Migrating NVIDIA GPU resources to RHCOS worker nodes
{: #rhcos-migrate-gpu}

[Virtual Private Cloud]{: tag-vpc}

Review the following steps about how to migrate your NVIDIA GPU operator resources from RHEL 8 GPU worker nodes to RHCOS worker nodes.

The NVIDIA GPU operator consists of the following resources:
- `gpu-feature-discovery`
- `nvidia-container-toolkit-daemonset`
- `nvidia-cuda-validator`
- `nvidia-dcgm`
- `nvidia-dcgm-exporter`
- `nvidia-device-plugin-daemonset`
- `nvidia-driver-daemonset`
- `nvidia-node-status-exporter`
- `nvidia-operator-validator`

The main component of interest is `nvidia-driver-daemonset`. This component is responsible for installing the GPU driver into the GPU worker node. These drivers are installed differently when targeting RHEL 8 versus RHCOS worker nodes.

**Official statement from NVIDIA GPU operator**: All worker nodes or node groups to run GPU workloads in the Kubernetes cluster must run the same operating system version to use the NVIDIA GPU Driver container. Alternatively, if you pre-install the NVIDIA GPU Driver on the nodes, then you can run different operating systems. For more information, see [Installing the NVIDIA GPU operator](https://docs.nvidia.com/datacenter/cloud-native/gpu-operator/latest/getting-started.html#installing-the-nvidia-gpu-operator){: external}.
{: note}

The NVIDIA GPU operator isn't capable of simultaneously managing driver installations on different worker node operating systems. This limitation means that if the GPU driver installation is solely managed by the NVIDIA GPU operator, then a full migration of the driver installation is required when changing worker node operating systems.
{: important}


Complete the following steps to migrate NVIDIA GPU operator driver installations from RHEL 8 to RHCOS worker nodes. This example specifically describes migration steps for the the following cluster configuration:

## Initial environment details
{: #env-details}

Review the details and notes for migrating an {{site.data.keyword.openshiftlong_notm}} version 4.17 on VPC with RHEL 8 worker nodes to version 4.18 with RHCOS worker nodes.

Version 4.18 supports only RHCOS and RHEL 9. However, the NVIDIA GPU operator does not support RHEL 9 operating system. Therefore, you must migrate to RHCOS when updating to 4.18.
{: note}

Before you begin, make sure the cluster meets the following requirements.

- A 4.17 VPC cluster with RHEL 8 worker nodes using NVIDIA GPU flavors.
- The NVIDIA GPU operator, ClusterPolicy, and operands are all installed and `Ready`.

1. Get the details of the `nvidia-gpu-operator`.
    ```sh
    oc get po -n nvidia-gpu-operator -o wide
    ```
    {: pre}

    Example output
    ```sh
    NAME                                       READY   STATUS      RESTARTS   AGE     IP               NODE          NOMINATED NODE   READINESS GATES
    gpu-feature-discovery-ng7zn                1/1     Running     0          6m6s    172.23.145.152   10.240.0.15   <none>           <none>
    gpu-operator-678b489684-7zgkq              1/1     Running     0          45h     172.23.145.135   10.240.0.15   <none>           <none>
    nvidia-container-toolkit-daemonset-j4dzs   1/1     Running     0          6m6s    172.23.145.143   10.240.0.15   <none>           <none>
    nvidia-cuda-validator-l44mz                0/1     Completed   0          2m28s   172.23.145.236   10.240.0.15   <none>           <none>
    nvidia-dcgm-7sfvn                          1/1     Running     0          6m7s    172.23.145.180   10.240.0.15   <none>           <none>
    nvidia-dcgm-exporter-s5k48                 1/1     Running     0          6m6s    172.23.145.172   10.240.0.15   <none>           <none>
    nvidia-device-plugin-daemonset-xhds2       1/1     Running     0          6m6s    172.23.145.191   10.240.0.15   <none>           <none>
    nvidia-driver-daemonset-mjqls              1/1     Running     0          7m1s    172.23.145.145   10.240.0.15   <none>           <none>
    nvidia-node-status-exporter-5kvs4          1/1     Running     0          7m16s   172.23.145.235   10.240.0.15   <none>           <none>
    nvidia-operator-validator-pz7wm            1/1     Running     0          6m7s    172.23.145.153   10.240.0.15   <none>           <none>
    ```
    {: screen}

1. Get the details of the `gpu-cluster-policy` and make sure it is `ready`.
    ```sh
    oc get clusterpolicies.nvidia.com gpu-cluster-policy
    ```
    {: pre}

    Example output
    ```sh
    NAME                 STATUS   AGE
    gpu-cluster-policy   ready    2025-03-07T03:07:00Z
    ```
    {: screen}

### Step 1: Update the cluster master
{: #step-1-update-master}

Run the following command to update the master.

```sh
ibmcloud oc cluster master update --cluster <clusterNameOrID> --version 4.18_openshift
```
{: pre}

At this point, don't upgrade workers nodes to 4.18. For now, keep your RHEL 8 workers on 4.17.


### Step 2: Create an RHCOS cluster worker pool
{: #step-2-create-workerpool}

1. Run the following command to create a RHCOS worker pool.

    ```sh
    ibmcloud oc worker-pool create vpc-gen2 \
        --cluster <clusterNameOrID> \
        --name <workerPoolName> \
        --flavor <workerNodeFlavor> \
        --size-per-zone <sizePerZoneCount> \
        --operating-system RHCOS
    ```
    {: pre}

Don't add zones to this RHCOS worker pool. There should be no workers in this worker pool.


### Step 3: Add worker pool labels to the RHCOS worker pool
{: #step-3-create-labels}

Add the following labels to your RHCOS worker pool.
- `nvidia.com/gpu.deploy.operands=false`. For more information, see [Preventing Installation of Operands on Some Nodes](https://docs.nvidia.com/datacenter/cloud-native/gpu-operator/latest/getting-started.html#preventing-installation-of-operands-on-some-nodes){: external}
- `nvidia.com/gpu.deploy.driver=false`. For more information, see [Preventing Installation of NVIDIA GPU Driver on Some Nodes](https://docs.nvidia.com/datacenter/cloud-native/gpu-operator/latest/getting-started.html#preventing-installation-of-nvidia-gpu-driver-on-some-nodes){: external}

Adding labels to the worker pool allows for node labels to exist before the worker nodes are available to cluster. This ensures that NVIDIA GPU resources are not automatically scheduled from the start. If NVIDA GPU resources are scheduled on worker nodes where drivers cannot be installed, it will degrade the status of the ClusterPolicy resource. Drivers cannot yet be installed on RHCOS worker nodes because the NVIDIA GPU operator is configured to use the RHEL 8 install method.

Run the following command to add labels to your worker pool.

```sh
ibmcloud oc worker-pool label set \
    --cluster <clusterNameOrID> \
    --worker-pool <workerPoolNameOrID> \
    --label nvidia.com/gpu.deploy.operands=false \
    --label nvidia.com/gpu.deploy.driver=false
```
{: pre}

### Step 4: Add RHCOS worker nodes to cluster
{: #step-4-add-nodes}

Add capacity to your cluster to allow for workload migration. Adding zones to the worker pool triggers the worker nodes to start provisioning and join the cluster. Note that the NVIDIA GPU resources are not deployed on the RHCOS worker nodes yet.

```sh
ibmcloud oc zone add vpc-gen2 \
    --cluster <clusterNameOrID> \
    --worker-pool <workerPoolNameOrID> \
    --subnet-id <vpcSubnetID> \
    --zone <vpcZone>
```
{: pre}

At this point, RHCOS worker nodes are available in the cluster to begin migration.

### Step 5: Change the driver installer on the RHEL 8 worker nodes to unmanaged
{: #step-5-unmanage-driver}

Add the `nvidia.com/gpu.deploy.driver=false` label to your RHEL 8 worker nodes. This label unschedules the existing driver installer pods from the RHEL 8 workers. The driver is not to be uninstalled. Other operands, including device plug-ins, remain on the RHEL 8 workers. The `ClusterPolicy` state remains ready. Since the driver is still installed and the device plug-in is running, GPU workloads continue to be functional.

1. Add the `nvidia.com/gpu.deploy.driver=false` to RHEL 8 worker nodes.

    To label an individual worker node:
    ```sh
    oc label nodes <nodeName> "nvidia.com/gpu.deploy.driver=false"
    ```
    {: pre}

    To label an entire worker pool:
    ```sh
    ibmcloud oc worker-pool label set \
        --cluster <clusterNameOrID> \
        --worker-pool <workerPoolNameOrID> \
        --label nvidia.com/gpu.deploy.driver=false
    ```
    {: pre}

1. List pods to confirm the labels.
    ```sh
    oc get po -n nvidia-gpu-operator -o wide
    ```
    {: pre}

    Example output
    ```sh
    NAME                                       READY   STATUS        RESTARTS   AGE     IP               NODE          NOMINATED NODE   READINESS GATES
    gpu-feature-discovery-ng7zn                1/1     Running       0          4h27m   172.23.145.152   10.240.0.15   <none>           <none>
    gpu-operator-678b489684-7zgkq              1/1     Running       0          2d2h    172.23.145.135   10.240.0.15   <none>           <none>
    nvidia-container-toolkit-daemonset-j4dzs   1/1     Running       0          4h27m   172.23.145.143   10.240.0.15   <none>           <none>
    nvidia-cuda-validator-l44mz                0/1     Completed     0          4h24m   172.23.145.236   10.240.0.15   <none>           <none>
    nvidia-dcgm-7sfvn                          1/1     Running       0          4h27m   172.23.145.180   10.240.0.15   <none>           <none>
    nvidia-dcgm-exporter-s5k48                 1/1     Running       0          4h27m   172.23.145.172   10.240.0.15   <none>           <none>
    nvidia-device-plugin-daemonset-xhds2       1/1     Running       0          4h27m   172.23.145.191   10.240.0.15   <none>           <none>
    nvidia-driver-daemonset-mjqls              1/1     Terminating   0          4h28m   172.23.145.145   10.240.0.15   <none>           <none>
    nvidia-node-status-exporter-5kvs4          1/1     Running       0          4h28m   172.23.145.235   10.240.0.15   <none>           <none>
    nvidia-operator-validator-pz7wm            1/1     Running       0          4h27m   172.23.145.153   10.240.0.15   <none>           <none>
    ```
    {: screen}

1. Confirm the `gpu-cluster-policy` is `ready`.
    ```sh
    oc get clusterpolicies.nvidia.com gpu-cluster-policy
    ```
    {: pre}

    Example output
    ```sh
    NAME                 STATUS   AGE
    gpu-cluster-policy   ready    2025-03-07T03:07:00Z
    ```
    {: pre}

### Step 6: Schedule driver installer and other operands to RHCOS worker nodes
{: #step-6-schedule-driver}

Add the `nvidia.com/gpu.deploy.driver=true` and `nvidia.com/gpu.deploy.operands=true` to your RHCOS workers.

Adding these labels attempts to schedule the driver installer, device plug-in, and other operands to the RHCOS worker nodes. Most pods are in the `init` state due to driver installer failing. Driver installer is failing because it is attempting to install the driver by using the RHEL 8 method.

Run the `label nodes` command to add labels.

To label an individual worker node:
```sh
oc label nodes <nodeName> "nvidia.com/gpu.deploy.driver=true"
oc label nodes <nodeName> "nvidia.com/gpu.deploy.operands=true"
```
{: pre}

To label an entire worker pool:
```sh
ibmcloud oc worker-pool label set \
    --cluster <clusterNameOrID> \
    --worker-pool <workerPoolNameOrID> \
    --label nvidia.com/gpu.deploy.driver=true
```
{: pre}

After adding the labels, continue to the next step.

### Step 7: Convert driver installer from RHEL 8 to RHCOS installation method
{: #step-7-convert-installation-method}

Delete `nvidia-driver-installer` DaemonSet. This DaemonSet is specific to RHEL 8 and is no longer needed. The GPU operator reconciles and detects that a RHCOS worker node is present in the cluster. The GPU operator re-creates the driver installer DaemonSet, but now with the RHCOS installation method based on OpenShift Driver Toolkit.

1. Delete `nvidia-driver-installer` DaemonSet. After deleting the DaemonSet, don't add or reload any of the RHEL 8 GPU workers.
    ```sh
    oc delete daemonset -n nvidia-gpu-operator nvidia-driver-installer
    ```
    {: pre}


1. List pods and confirm that the GPU driver is installed on the RHCOS worker nodes and the remaining operands are `ready`.

    ```sh
    oc get po -n nvidia-gpu-operator -o wide
    ```
    {: pre}

    Example output
    ```sh
    NAME                                                  READY   STATUS      RESTARTS      AGE     IP               NODE                                                     NOMINATED NODE   READINESS GATES
    gpu-feature-discovery-h4bhx                           1/1     Running     0             18m     172.23.137.119   test-coajphf20ooqeeg7u9dg-btsstagevpc-gx316x8-000239a8   <none>           <none>
    gpu-feature-discovery-ng7zn                           1/1     Running     0             4h58m   172.23.145.152   10.240.0.15                                              <none>           <none>
    gpu-operator-678b489684-7zgkq                         1/1     Running     0             2d2h    172.23.145.135   10.240.0.15                                              <none>           <none>
    nvidia-container-toolkit-daemonset-79j86              1/1     Running     0             18m     172.23.137.115   test-coajphf20ooqeeg7u9dg-btsstagevpc-gx316x8-000239a8   <none>           <none>
    nvidia-container-toolkit-daemonset-j4dzs              1/1     Running     0             4h58m   172.23.145.143   10.240.0.15                                              <none>           <none>
    nvidia-cuda-validator-l44mz                           0/1     Completed   0             4h55m   172.23.145.236   10.240.0.15                                              <none>           <none>
    nvidia-cuda-validator-xgscz                           0/1     Completed   0             15m     172.23.137.121   test-coajphf20ooqeeg7u9dg-btsstagevpc-gx316x8-000239a8   <none>           <none>
    nvidia-dcgm-7sfvn                                     1/1     Running     0             4h58m   172.23.145.180   10.240.0.15                                              <none>           <none>
    nvidia-dcgm-9rpnz                                     1/1     Running     0             18m     172.23.137.117   test-coajphf20ooqeeg7u9dg-btsstagevpc-gx316x8-000239a8   <none>           <none>
    nvidia-dcgm-exporter-s5k48                            1/1     Running     0             4h58m   172.23.145.172   10.240.0.15                                              <none>           <none>
    nvidia-dcgm-exporter-x8vlc                            1/1     Running     2 (14m ago)   18m     172.23.137.116   test-coajphf20ooqeeg7u9dg-btsstagevpc-gx316x8-000239a8   <none>           <none>
    nvidia-device-plugin-daemonset-7g5hz                  1/1     Running     0             18m     172.23.137.120   test-coajphf20ooqeeg7u9dg-btsstagevpc-gx316x8-000239a8   <none>           <none>
    nvidia-device-plugin-daemonset-xhds2                  1/1     Running     0             4h58m   172.23.145.191   10.240.0.15                                              <none>           <none>
    nvidia-driver-daemonset-416.94.202502260030-0-dkcmh   2/2     Running     0             19m     172.23.137.107   test-coajphf20ooqeeg7u9dg-btsstagevpc-gx316x8-000239a8   <none>           <none>
    nvidia-node-status-exporter-5kvs4                     1/1     Running     0             5h      172.23.145.235   10.240.0.15                                              <none>           <none>
    nvidia-node-status-exporter-94v9f                     1/1     Running     0             19m     172.23.137.110   test-coajphf20ooqeeg7u9dg-btsstagevpc-gx316x8-000239a8   <none>           <none>
    nvidia-operator-validator-4wk6z                       1/1     Running     0             18m     172.23.137.118   test-coajphf20ooqeeg7u9dg-btsstagevpc-gx316x8-000239a8   <none>           <none>
    nvidia-operator-validator-pz7wm                       1/1     Running     0             4h58m   172.23.145.153   10.240.0.15                                              <none>           <none>
    ```
    {: screen}

1. Confirm the `gpu-cluster-policy` is ready.
    ```sh
    oc get clusterpolicies.nvidia.com gpu-cluster-policy
    ```
    {: pre}

    Example output
    ```sh
    NAME                 STATUS   AGE
    gpu-cluster-policy   ready    2025-03-07T03:07:00Z
    ```
    {: screen}

1. Describe your nodes and confirm the allocatable GPUs.

    ```sh
    oc describe no
    ```
    {: pre}

    Example output
    ```sh
    ...
    Capacity:
    nvidia.com/gpu:     1
    ...
    Allocatable:
    nvidia.com/gpu:     1
    ```
    {: screen}

### Step 8: Migrate GPU-dependent workloads to your RHCOS worker nodes
{: #step-8-convert-migrate-workloads}

Now that RHCOS GPU worker nodes have the GPU driver installed and are ready for scheduling, migrate GPU-dependent workloads to the RHCOS worker nodes.

* Migrate per pod by cordoning node and deleting individual pods.
    ```sh
    oc adm cordon no/<nodeName>
    oc delete po -n <namespace> <podName>
    ```
    {: pre}

* Migrate per Node by draining nodes. For more information, see [Safely drain a node](https://kubernetes.io/docs/tasks/administer-cluster/safely-drain-node/){: external}.

* Migrate per worker pool by deleting your entire RHEL worker pool.
    ```sh
    ibmcloud oc worker-pool rm --cluster <clusterNameOrID> --worker-pool <workerPoolNameOrID>
    ```
    {: pre}

### Step 9: Remove labels from your RHCOS worker pool
{: #step-9-remove-labels}

Remove worker pool labels that you added in a previous step. This removal ensures that new RHCOS worker nodes provisioned afterward don't have these labels and the NVIDIA GPU components get automatically installed.

### Step 10: Scale down or delete RHEL 8 worker pool
{: #step-10-remove-rhel-pool}

At this point, migration of NVIDIA GPU driver is complete. You can scale down or delete your RHEL worker pools.

```sh
ibmcloud oc worker-pool rm --cluster <clusterNameOrID> --worker-pool <workerPoolNameOrID>
```
{: pre}
