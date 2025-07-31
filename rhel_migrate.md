---

copyright:
  years: 2022, 2025
lastupdated: "2025-07-31"


keywords: rhel, os, operating system, rhcos, 418, migration

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}



# Migrating to a new operating system
{: #rhel_migrate}

[Classic]{: tag-classic-inf} [VPC]{: tag-vpc}

Complete the following steps to migrate your worker nodes to a new operating system.
{: shortdesc}


Beginning with cluster version 4.18, Red Hat Enterprise Linux CoreOS (RHCOS) is the default operating system and RHEL worker nodes are deprecated in this version. Support for RHEL worker nodes ends with the release of version 4.21. Migrate your clusters to use RHCOS worker nodes as soon as possible.
{: important}

| Milestone | Description |
| --- | --- |
| 4.18 release: {{site.data.keyword.openshift_418_release_date}} | Beginning with cluster version 4.18, Red Hat Enterprise Linux CoreOS (RHCOS) is the default operating system and RHEL worker nodes are deprecated in this version. RHEL workers are still available in version 4.18 only to complete the migration to RHCOS workers. |
| 4.21 release | Cluster version 4.21 supports only RHCOS worker nodes. Migrate your RHEL 9 worker nodes to RHCOS before updating to version 4.21. |
{: caption="RHEL deprecation timeline" caption-side="bottom"}

The steps to migrate to RHCOS are different based on your use case. Review the following links for steps that apply to your use case.

[Migrating worker nodes to RHCOS](#migrate-rhcos)
:   Follow theses steps for most uses cases.

[Migrating GPU worker nodes to RHCOS](#rhcos-migrate-gpu)
:   If you have GPU worker nodes, follow these steps to migrate to RHCOS.

Looking for Terraform steps? For more information, see this blog post for steps on how to migrate to RHCOS by using Terraform. TBD link
{: tip}

## Migrating worker nodes to RHCOS
{: #migrate-rhcos}

Complete the following steps to migrate your worker nodes to RHCOS.

To migrate to RHCOS, you must provision a new worker pool, then delete the previous RHEL worker pool. The new worker pool must reside in the same zone as the previous worker pool. 

### Step 1: Upgrade your cluster master
{: #upgrade-cluster-rhcos}

Run the following command to update the master.

```sh
ibmcloud ks cluster master update --cluster <clusterNameOrID> --version 4.18_openshift
```
{: pre}

### Step 2: Creating a new RHCOS worker pool
{: #create-pool-rhcos}

- Make sure to specify `RHCOS` as the `--operating-system` of the new pool.
- Make sure that the number of nodes specified with the `--size-per-zone` option matches the number of workers per zone for the RHEL worker pool. To list a worker pool's zones and the number of workers per zone, run `ibmcloud oc worker-pool get --worker-pool WORKER_POOL --cluster CLUSTER`.
- Make sure to include the `--entitlement ocp_entitled` option if you have a Cloud Pak entitlement.

1. Run the `ibmcloud oc worker-pool create` command to create a new worker pool.

    **VPC**: Example command to create a RHCOS worker pool. For more information about the `worker pool create vpc-gen2` command, see the [CLI reference](/docs/openshift?topic=openshift-kubernetes-service-cli#cli_worker_pool_create_vpc_gen2) for command details. [Adding worker nodes in VPC clusters](/docs/openshift?topic=openshift-add-workers-vpc).

    ```sh
    ibmcloud oc worker-pool create vpc-gen2 --name <worker_pool_name> --cluster <cluster_name_or_ID> --flavor <flavor> --size-per-zone <number_of_workers_per_zone> --operating-system RHCOS [--entitlement ocp_entitled]
    ```
    {: pre}
    
    **{{site.data.keyword.satelliteshort}}**: Example command to create a RHCOS worker pool. Note that for {{site.data.keyword.satelliteshort}} clusters, you must first [attach hosts to your location](/docs/satellite?topic=satellite-attach-hosts) before you can create a worker pool.
    
    ```sh
    ibmcloud oc worker-pool create satellite --cluster CLUSTER --host-label "os=RHCOS" --name NAME --size-per-zone SIZE --operating-system RHCOS --zone ZONE [--label LABEL]
    ```
    {: pre}


1. Verify that the worker pool is created and note the worker pool ID.

    ```sh
    ibmcloud oc worker-pool ls --cluster <cluster_name_or_ID>
    ```
    {: pre}

    Example output

    ```sh
    Name            ID                              Flavor                 OS              Workers 
    my_workerpool   aaaaa1a11a1aa1aaaaa111aa11      b3c.4x16.encrypted     REDHAT_8_64    0 
    ```
    {: screen}

1. Add one or more zones to your worker pool. When you add a zone, the number of worker nodes you specified with the `--size-per-zone` option are added to the zone. These worker nodes run the RHCOS operating system. It's recommended that the zones you add to the RHCOS worker pool match the zones added to the RHEL worker pool that you are replacing. To view the zones attached to a worker pool, run `ibmcloud oc worker-pool zones --worker-pool WORKER_POOL --cluster CLUSTER`. If you add zones that do not match those of RHEL worker pool, make sure your workloads will not be impacted by moving them to a new zone. Note that File or Block storage are not supported across zones. 


### Step 3: Add worker nodes to your RHCOS worker pool
{: #rhcos-add-worker-nodes}

See [Adding a zone to a worker pool in a VPC cluster](/docs/openshift?topic=openshift-add-workers-vpc#vpc_add_zone).



### Step 4: Migrate your workloads
{: #rhcos-migrate-workloads}

If you have software-defined storage (SDS) solutions like OpenShift Data Foundation or Portworx, update your storage configurations to include the new worker nodes and verify your workloads before removing your RHEL worker nodes.
{: important}

For more information about rescheduling workloads, see [Safely Drain a Node](https://kubernetes.io/docs/tasks/administer-cluster/safely-drain-node/){: external} in the Kubernetes docs or [Understanding how to evacuate pods on nodes](https://docs.openshift.com/container-platform/4.9/nodes/nodes/nodes-nodes-working.html){: external} in the {{site.data.keyword.redhat_openshift_notm}} docs.
{: tip}

* Migrate per pod by cordoning node and deleting individual pods.
    ```sh
    oc adm cordon no/<nodeName>
    oc delete po -n <namespace> <podName>
    ```
    {: pre}

* Migrate per Node by draining nodes. For more information, see [Safely drain a node](https://kubernetes.io/docs/tasks/administer-cluster/safely-drain-node/){: external}.

* Migrate per worker pool by deleting your entire RHEL worker pool.
    ```sh
    ibmcloud ks worker-pool rm --cluster <clusterNameOrID> --worker-pool <workerPoolNameOrID>
    ```
    {: pre}

### Step 5: Remove the RHEL worker nodes
{: #rm-rhel-pool}

Remove the worker pool that contains the RHEL workers. 

Consider scaling down your RHEL worker pool and keeping it for several days before you remove it. This way, you can easily scale the worker pool back up if your workload experiences disruptions during the migration process. When you have determined that your workload is stable and functions normally, you can safely remove the RHEL worker pool.
{: important}

1. List your worker pools and note the name of the worker pool you want to remove.
    ```sh
    ibmcloud oc worker-pool ls --cluster CLUSTER
    ```
    {: pre}

2. Run the command to remove the worker pool.
    ```sh
    ibmcloud oc worker-pool rm --worker-pool WORKER_POOL --cluster CLUSTER
    ```
    {: pre}

### Optional Step 5: Uninstall and reinstall the Object Storage plug-in
{: #rhel-rm-cos}

If you use the COS plug-in in your cluster, after migrating from RHEL to RHCOS, you must uninstall and reinstall it because the `kube-driver` path is different between the two operating systems. If this is not done, you may see an error similar to `Error: failed to mkdir /usr/libexec/kubernetes: mkdir /usr/libexec/kubernetes: read-only file system`.

* [Follow the steps to uninstall the COS plug-in](/docs/openshift?topic=openshift-storage_cos_install#remove_cos_plugin).

* [Resintall the plug-in](/docs/openshift?topic=openshift-storage_cos_install#remove_cos_plugin)

## Migrating NVIDIA GPU resources to RHCOS worker nodes
{: #rhcos-migrate-gpu}

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


- Migrating a {{site.data.keyword.openshiftlong_notm}} version 4.17 on VPC with RHEL 8 worker nodes to version 4.18 with RHCOS worker nodes.
- Version 4.17 does not support RHCOS worker nodes.
- Version 4.17 supports RHEL 8 and RHEL 9 (exclusions apply).
- Version 4.18 does not support RHEL 8 worker nodes.
- Version supports only RHCOS and RHEL 9.
- NVIDIA GPU operator does not support RHEL 9 operating system.


Complete the following steps to migrate NVIDIA GPU operator driver installations from RHEL 8 to RHCOS worker nodes. This example specifically describes migration steps for the the following cluster configuration:

### Initial environment details
{: #env-details}

- {{site.data.keyword.openshiftlong_notm}} 4.17 VPC cluster
- RHEL 8 worker nodes using NVIDIA GPU flavors
- NVIDIA GPU operator installed
- NVIDIA GPU operator's ClusterPolicy installed
- Operator, ClusterPolicy, and operands ready

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

Adding these labels attempts to schedule the driver installer, device plugin, and other operands to the RHCOS worker nodes. Most pods are in the `init` state due to driver installer failing. Driver installer is failing because it is attempting to install the driver by using the RHEL 8 method.

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



## Migrating to Red Hat Enterprise Linux 9
{: #migrate-rhel-9}

For RHEL 9, the `/tmp` directory is a separate partition that has the `nosuid`, `noexec`, and `nodev` options set. If your apps install to and run scripts or binaries under the `/tmp` directory, they might fail. Update your apps to use the `/var/tmp` directory instead of the `/tmp` directory to run temporary scripts or binaries.

The default `cgroup` implementation is `cgroup` v2. In RHEL 9, `cgroup` v1 isn't supported. Review the [Kubernetes migration documentation for `cgroup` v2](https://kubernetes.io/docs/concepts/architecture/cgroups/#migrating-to-cgroup-v2) and verify that your applications fully support `cgroup` v2. There are known issues with older versions of Java that may cause out of memory (OOM) issues for workloads.
{: important}

1. Review your worker pool operating systems to find which pools you need to migrate.
    ```sh
    ibmcloud ks worker-pools -c CLUSTER
    ```
    {: pre}

1. Specify the `RHEL_9_64` version for the worker pool. 

    ```sh
    ibmcloud oc worker-pool operating-system set --cluster CLUSTER --worker-pool POOL --operating-system RHEL_9_64
    ```
    {: pre}

1. Update each worker node in the worker pool by running the [`ibmcloud oc worker update`](/docs/containers?topic=containers-kubernetes-service-cli#cs_worker_update) for Classic clusters or [`ibmcloud oc worker replace`](/docs/containers?topic=containers-kubernetes-service-cli#cli_worker_replace) for VPC clusters. 

    Make sure you have enough worker nodes to support your workload while you update or replace the relevant worker nodes. For more information, see [Updating VPC worker nodes](/docs/containers?topic=containers-update&interface=ui#vpc_worker_node) or [Updating classic worker nodes](/docs/containers?topic=containers-update&interface=ui#worker_node).
    {: tip}

    Example command to update Classic worker nodes.

    ```sh
    ibmcloud oc worker update --cluster CLUSTER --worker WORKER1_ID [--worker WORKER2_ID] 
    ```
    {: pre}

    Example command to replace VPC worker nodes.

    ```sh
    ibmcloud oc worker replace --cluster CLUSTER --worker WORKER_ID
    ```
    {: pre}

1. Get the details for your worker pool and workers. In the output, verify that your worker nodes run the `RHEL_9_64` operating system.

    Get the details for a worker pool. 
    ```sh
    ibmcloud oc worker-pools -c CLUSTER
    ```
    {: pre}

    Get the details for a worker node. 
    ```sh
    ibmcloud oc worker get --cluster CLUSTER --worker WORKER_NODE_ID 
    ```
    {: pre}
