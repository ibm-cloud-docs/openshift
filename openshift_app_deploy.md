---

copyright:
  years: 2014, 2025
lastupdated: "2025-05-28"


keywords: kubernetes, openshift

subcollection: openshift

---


{{site.data.keyword.attribute-definition-list}}





# Deploying apps in {{site.data.keyword.redhat_openshift_notm}} clusters
{: #deploy_app}

With {{site.data.keyword.openshiftlong}} clusters, you can deploy apps from a remote file or repository such as GitHub with a single command. Also, your clusters come with various built-in services that you can use to help operate your cluster.
{: shortdesc}

## Moving your apps to {{site.data.keyword.redhat_openshift_notm}}
{: #openshift_move_apps}

To create an app in your {{site.data.keyword.openshiftlong_notm}} cluster, you can use the {{site.data.keyword.redhat_openshift_notm}} console or CLI.
{: shortdesc}

Seeing errors when you deploy your app? {{site.data.keyword.redhat_openshift_notm}} has different default settings than community Kubernetes, such as stricter security context constraints. Review the [common scenarios where you might need to modify your apps](/docs/openshift?topic=openshift-plan_deploy#openshift_move_apps_scenarios) so that you can deploy them on {{site.data.keyword.redhat_openshift_notm}} clusters.
{: tip}

### Deploying apps through the console
{: #deploy_apps_ui}
{: ui}

You can create apps through various methods in the {{site.data.keyword.redhat_openshift_notm}} console by using the **Developer** perspective. For more information, see the [{{site.data.keyword.redhat_openshift_notm}} documentation](https://docs.openshift.com/container-platform/4.17/applications/creating_applications/odc-creating-applications-using-developer-perspective.html){: external}.
{: shortdesc}

1. From the [console](https://cloud.ibm.com/containers/cluster-management/clusters){: external}, select your cluster.
2. Click **{{site.data.keyword.redhat_openshift_notm}} web console**.
3. From the perspective switcher, select **Developer**. The {{site.data.keyword.redhat_openshift_notm}} web console switches to the Developer perspective, and the menu now offers items such as **+Add**, **Topology**, and **Builds**.
4. Click **+Add**.
5. In the **Add** pane menu bar, select the **Project** that you want to create your app in from the drop-down list.
6. Click the method that you want to use to add your app, and follow the instructions. For example, click **From Git**.

### Deploying apps through the CLI
{: #deploy_apps_cli}
{: cli}

To create an app in your {{site.data.keyword.openshiftlong_notm}} cluster, use the `oc new-app` [command](https://docs.openshift.com/container-platform/4.17/cli_reference/openshift_cli/developer-cli-commands.html#new-app){: external}. For example, you might refer to a public GitHub repo, a public GitLab repo with a URL that ends in `.git`, or another local or remote repo. For more information, [try out the tutorial](/docs/openshift?topic=openshift-openshift_tutorial#openshift_deploy_app) and review the [{{site.data.keyword.redhat_openshift_notm}} documentation](https://docs.openshift.com/container-platform/4.17/applications/creating_applications/odc-creating-applications-using-developer-perspective.html){: external}.
{: shortdesc}

```sh
oc new-app --name <app_name> https://github.com/<path_to_app_repo> [--context-dir=<subdirectory>]
```
{: pre}

What does the `new-app` command do?
:   The `new-app` command creates a build configuration and app image from the source code, a deployment configuration to deploy the container to pods in your cluster, and a service to expose the app within the cluster. For more information about the build process and other sources besides Git, see the [{{site.data.keyword.redhat_openshift_notm}} documentation](https://docs.openshift.com/container-platform/4.17/applications/creating_applications/odc-creating-applications-using-developer-perspective.html){: external}.

## Deploying apps to specific worker nodes by using labels
{: #node_affinity}

When you deploy an app, the app pods indiscriminately deploy to various worker nodes in your cluster. Sometimes, you might want to restrict the worker nodes that the app pods to deploy to. For example, you might want app pods to deploy to only worker nodes in a certain worker pool because those worker nodes are on bare metal machines. To designate the worker nodes that app pods must deploy to, add an affinity rule to your app deployment.
{: shortdesc}

Before you begin
- [Access your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-access_cluster).
- **Optional**: [Set a label for the worker pool](/docs/openshift?topic=openshift-worker-tag-label) that you want to run the app on.

To deploy apps to specific worker nodes,

1. Get the ID of the worker pool that you want to deploy app pods to.
    ```sh
    ibmcloud oc worker-pool ls --cluster <cluster_name_or_ID>
    ```
    {: pre}

2. List the worker nodes that are in the worker pool, and note one of the **Private IP** addresses.
    ```sh
    ibmcloud oc worker ls --cluster <cluster_name_or_ID> --worker-pool <worker_pool_name_or_ID>
    ```
    {: pre}

3. Describe the worker node. In the **Labels** output, note the worker pool ID label, `ibm-cloud.kubernetes.io/worker-pool-id`.

    The steps in this topic use a worker pool ID to deploy app pods only to worker nodes within that worker pool. To deploy app pods to specific worker nodes by using a different label, note this label instead. For example, to deploy app pods only to worker nodes on a specific private VLAN, use the `privateVLAN=` label.
    {: tip}

    ```sh
    oc describe node <worker_node_private_IP>
    ```
    {: pre}

    Example output

    ```sh
    NAME:               10.xxx.xx.xxx
    Roles:              <none>
    Labels:             arch=amd64
                        beta.kubernetes.io/arch=amd64
                        beta.kubernetes.io/instance-type=b3c.4x16.encrypted
                        beta.kubernetes.io/os=linux
                        failure-domain.beta.kubernetes.io/region=us-south
                        failure-domain.beta.kubernetes.io/zone=dal10
                        ibm-cloud.kubernetes.io/encrypted-docker-data=true
                        ibm-cloud.kubernetes.io/ha-worker=true
                        ibm-cloud.kubernetes.io/iaas-provider=softlayer
                        ibm-cloud.kubernetes.io/machine-type=b3c.4x16.encrypted
                        ibm-cloud.kubernetes.io/sgx-enabled=false
                        ibm-cloud.kubernetes.io/worker-pool-id=00a11aa1a11aa11a1111a1111aaa11aa-11a11a
                        ibm-cloud.kubernetes.io/worker-version=1.32_1534
                        kubernetes.io/hostname=10.xxx.xx.xxx
                        privateVLAN=1234567
                        publicVLAN=7654321
    Annotations:        node.alpha.kubernetes.io/ttl=0
    ...
    ```
    {: screen}

4. [Add an affinity rule](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/){: external} for the worker pool ID label to the app deployment.

    Example YAML

    ```yaml
    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: with-node-affinity
    spec:
      template:
        spec:
          affinity:
            nodeAffinity:
              requiredDuringSchedulingIgnoredDuringExecution:
                nodeSelectorTerms:
                - matchExpressions:
                  - key: ibm-cloud.kubernetes.io/worker-pool-id
                    operator: In
                    values:
                    - <worker_pool_ID>
    ...
    ```
    {: codeblock}

    In the **affinity** section of the example YAML, `ibm-cloud.kubernetes.io/worker-pool-id` is the `key` and `<worker_pool_ID>` is the `value`.

5. Apply the updated deployment configuration file.
    ```sh
    oc apply -f with-node-affinity.yaml
    ```
    {: pre}

6. Verify that the app pods deployed to the correct worker nodes.

    1. List the pods in your cluster.
        ```sh
        oc get pods -o wide
        ```
        {: pre}

        Example output
        ```sh
        NAME                   READY     STATUS              RESTARTS   AGE       IP               NODE
        cf-py-d7b7d94db-vp8pq  1/1       Running             0          15d       172.30.xxx.xxx   10.176.48.78
        ```
        {: screen}

    2. In the output, identify a pod for your app. Note the **NODE** private IP address of the worker node that the pod is on.

        In the previous example output, the app pod `cf-py-d7b7d94db-vp8pq` is on a worker node with the IP address `10.xxx.xx.xxx`.

    3. List the worker nodes in the worker pool that you designated in your app deployment.

        ```sh
        ibmcloud oc worker ls --cluster <cluster_name_or_ID> --worker-pool <worker_pool_name_or_ID>
        ```
        {: pre}

        Example output

        ```sh
        ID                                                 Public IP       Private IP     Machine Type      State    Status  Zone    Version
        kube-dal10-crb20b637238bb471f8b4b8b881bbb4962-w7   169.xx.xxx.xxx  10.176.48.78   b3c.4x16          normal   Ready   dal10   1.8.6_1504
        kube-dal10-crb20b637238bb471f8b4b8b881bbb4962-w8   169.xx.xxx.xxx  10.176.48.83   b3c.4x16          normal   Ready   dal10   1.8.6_1504
        kube-dal12-crb20b637238bb471f8b4b8b881bbb4962-w9   169.xx.xxx.xxx  10.176.48.69   b3c.4x16          normal   Ready   dal12   1.8.6_1504
        ```
        {: screen}

        If you created an app affinity rule based on another factor, get that value instead. For example, to verify that the app pod deployed to a worker node on a specific VLAN, view the VLAN that the worker node is on by running `ibmcloud oc worker get --cluster <cluster_name_or_ID> --worker <worker_ID>`.
        {: tip}

    4. In the output, verify that the worker node with the private IP address that you identified in the previous step is deployed in this worker pool.

## Deploying an app on an NVIDIA GPU machine
{: #gpu_app}

If you have a GPU machine type, you can speed up the processing time required for compute intensive workloads such as AI, machine learning, inferencing, and more.
{: shortdesc}




In the following steps, you learn how to deploy workloads that require the GPU. However, you can also deploy apps that don't need to process their workloads across both the GPU and CPU. 

You can also try mathematically intensive workloads such as the [TensorFlow](https://www.tensorflow.org/){: external} machine learning framework with [this Kubernetes demo](https://github.com/pachyderm/pachyderm/tree/master/examples/ml/tensorflow){: external}.
{: tip}

### Prerequisites
{: #gpu-prereqs}

Before you begin
- Create a [cluster](/docs/openshift?topic=openshift-clusters) or worker pool that uses a GPU flavor. Keep in mind that setting up a bare metal machine can take more than one business day to complete. For a list of available flavors, see the following links.
    - [Classic flavors](/docs/openshift?topic=openshift-classic-flavors)
    - [VPC flavors](/docs/openshift?topic=openshift-vpc-flavors)

- Make sure that you are assigned a [service access role](/docs/openshift?topic=openshift-iam-platform-access-roles) that grants the appropriate Kubernetes RBAC role so that you can work with Kubernetes resources in the cluster.



**Private only cluster limitations**: If you cluster doesn't have public network connectivity, you must allow public network connectivity or mirror images from external registries and image streams to `icr.io`. In the following example, the GPU app uses the OLM marketplace with image streams. This example does not work if your cluster can't access the NVIDIA registry (`nvcr.io`).

- [Install the NVIDIA GPU operator for your cluster version](https://docs.nvidia.com/datacenter/cloud-native/gpu-operator/getting-started.html#operator-install-guide){: external}.
- [Install the Node Feature Discovery and NVIDIA GPU operators for your cluster version](https://docs.nvidia.com/datacenter/cloud-native/gpu-operator/getting-started.html){: external}.

You must use NVIDIA GPU operator version 1.3.1 or later. When you install the Node Feature Discovery operator, select the update channel that matches your {{site.data.keyword.redhat_openshift_notm}} cluster version. Don't install the operators through another method, such as a Helm chart.
{: important}

If you experience issues installing the Node Feature Discovery Operator or the NVIDIA GPU Operator, [contact NVIDIA support for help](https://www.nvidia.com/en-us/support/){: external} or open an issue in the [NVIDIA GPU Operator repo](https://github.com/NVIDIA/gpu-operator/issues){: external}
{: note}
    


### Deploying a workload
{: #gpu-workload}

1. Create a YAML file. In this example, a `Job` YAML manages batch-like workloads by making a short-lived pod that runs until the command completes and successfully terminates.

    For GPU workloads, you must specify the `resources: limits: nvidia.com/gpu` field in the job YAML.
    {: note}

    ```yaml
    apiVersion: batch/v1
    kind: Job
    metadata:
      name: nvidia-devicequery
      labels:
        name: nvidia-devicequery
    spec:
      template:
        metadata:
          labels:
            name: nvidia-devicequery
        spec:
          containers:
          - name: nvidia-devicequery
            image: nvcr.io/nvidia/k8s/cuda-sample:devicequery-cuda11.7.1-ubuntu20.04
            imagePullPolicy: IfNotPresent
            resources:
              limits:
                nvidia.com/gpu: 2
          restartPolicy: Never
    ```
    {: codeblock}
    
    | Component | Description | 
    |--- | --- |
    | Metadata and label names | Enter a name and a label for the job, and use the same name in both the file's metadata and the `spec template` metadata. For example, `nvidia-devicequery`. |
    | `containers.image` | Provide the image that the container is a running instance of. In this example, the value is set to use the DockerHub CUDA device query image:`nvcr.io/nvidia/k8s/cuda-sample:devicequery-cuda11.7.1-ubuntu20.04`. |
    | `containers.imagePullPolicy` | To pull a new image only if the image is not currently on the worker node, specify `IfNotPresent`. |
    | `resources.limits` | For GPU machines, you must specify the resource limit. The Kubernetes [Device Plug-in](https://kubernetes.io/docs/concepts/extend-kubernetes/compute-storage-net/device-plugins/){: external} sets the default resource request to match the limit. \n * You must specify the key as `nvidia.com/gpu`. \n * Enter the whole number of GPUs that you request, such as `2`. Note that container pods don't share GPUs and GPUs can't be overcommitted. For example, if you have only 1 `mg1c.16x128` machine, then you have only 2 GPUs in that machine and can specify a maximum of `2`. |
    {: caption="Understanding your YAML components" caption-side="bottom"}

2. Apply the YAML file. For example:

    ```sh
    oc apply -f nvidia-devicequery.yaml
    ```
    {: pre}

3. Check the job pod by filtering your pods by the `nvidia-devicequery` label. Verify that the **STATUS** is **Completed**.

    ```sh
    oc get pod -A -l 'name in (nvidia-devicequery)'
    ```
    {: pre}

    Example output

    ```sh
    NAME                  READY     STATUS      RESTARTS   AGE
    nvidia-devicequery-ppkd4      0/1       Completed   0          36s
    ```
    {: screen}

4. Describe the pod to see how the GPU device plug-in scheduled the pod.
    - In the `Limits` and `Requests` fields, see that the resource limit that you specified matches the request that the device plug-in automatically set.
    - In the events, verify that the pod is assigned to your GPU worker node.

        ```sh
        oc describe pod nvidia-devicequery-ppkd4
        ```
        {: pre}

        Example output
        ```sh
        NAME:           nvidia-devicequery-ppkd4
        Namespace:      default
        ...
        Limits:
            nvidia.com/gpu:  1
        Requests:
            nvidia.com/gpu:  1
        ...
        Events:
        Type    Reason                 Age   From                     Message
        ----    ------                 ----  ----                     -------
        Normal  Scheduled              1m    default-scheduler        Successfully assigned nvidia-devicequery-ppkd4 to 10.xxx.xx.xxx
        ...
        ```
        {: screen}

5. To verify that the job used the GPU to compute its workload, you can check the logs.

    ```sh
    oc logs nvidia-devicequery-ppkd4
    ```
    {: pre}

    Example output

    ```sh
    /cuda-samples/sample Starting...
    
    CUDA Device Query (Runtime API) version (CUDART static linking)
    
    Detected 1 CUDA Capable device(s)
    
    Device 0: "Tesla P100-PCIE-16GB"
    CUDA Driver Version / Runtime Version          11.4 / 11.7
    CUDA Capability Major/Minor version number:    6.0
    Total amount of global memory:                 16281 MBytes (17071734784 bytes)
    (056) Multiprocessors, (064) CUDA Cores/MP:    3584 CUDA Cores
    GPU Max Clock rate:                            1329 MHz (1.33 GHz)
    Memory Clock rate:                             715 Mhz
    Memory Bus Width:                              4096-bit
    L2 Cache Size:                                 4194304 bytes
    Maximum Texture Dimension Size (x,y,z)         1D=(131072), 2D=(131072, 65536), 3D=(16384, 16384, 16384)
    Maximum Layered 1D Texture Size, (num) layers  1D=(32768), 2048 layers
    Maximum Layered 2D Texture Size, (num) layers  2D=(32768, 32768), 2048 layers
    Total amount of constant memory:               65536 bytes
    Total amount of shared memory per block:       49152 bytes
    Total shared memory per multiprocessor:        65536 bytes
    Total number of registers available per block: 65536
    Warp size:                                     32
    Maximum number of threads per multiprocessor:  2048
    Maximum number of threads per block:           1024
    Max dimension size of a thread block (x,y,z): (1024, 1024, 64)
    Max dimension size of a grid size    (x,y,z): (2147483647, 65535, 65535)
    Maximum memory pitch:                          2147483647 bytes
    Texture alignment:                             512 bytes
    Concurrent copy and kernel execution:          Yes with 2 copy engine(s)
    Run time limit on kernels:                     No
    Integrated GPU sharing Host Memory:            No
    Support host page-locked memory mapping:       Yes
    Alignment requirement for Surfaces:            Yes
    Device has ECC support:                        Enabled
    Device supports Unified Addressing (UVA):      Yes
    Device supports Managed Memory:                Yes
    Device supports Compute Preemption:            Yes
    Supports Cooperative Kernel Launch:            Yes
    Supports MultiDevice Co-op Kernel Launch:      Yes
    Device PCI Domain ID / Bus ID / location ID:   0 / 175 / 0
    Compute Mode:
    < Default (multiple host threads can use ::cudaSetDevice() with device simultaneously) >
    
    deviceQuery, CUDA Driver = CUDART, CUDA Driver Version = 11.4, CUDA Runtime Version = 11.7, NumDevs = 1
    Result = PASS
    ```
    {: screen}

    In this example, you see a GPU was used to execute the job because the GPU was scheduled in the worker node. If the limit is set to 2, only 2 GPUs are shown.

Now that you deployed a test GPU workload, you might want to set up your cluster to run a tool that relies on GPU processing, such as [IBM Maximo Visual Inspection](https://www.ibm.com/products/maximo/asset-performance-management){: external}.


    
## Deploying an app on an Intel AI Accelerator (Gaudi 3) machine
{: #intel-gpu-app}

Complete the following example to deploy Intel Gaudi’s PyTorch container image that a retreives a Gaudi device by using the `resource.limits` field. Before you begin, make sure your cluster meets the following requirements.

- Version 4.18 and later
- VPC clusters only
- RHCOS worker nodes only
- Intel Gaudi Base [operator v1.20.1 and later](https://catalog.redhat.com/software/container-stacks/detail/6683b2cce45daa25e36bddcb){: external}

For more information and examples, see the [Habana docs](https://docs.habana.ai/en/latest/){: external} and the [quickstart example](https://docs.habana.ai/en/latest/Quick_Start_Guides/Kubernetes_Quick_Start.html){: external}.
{: tip}



1. Copy the following example job configuration and save it as a file called `config.yaml`
    ```yaml
    apiVersion: batch/v1
    kind: Job
    metadata:
      name: habanalabs-gaudi-demo
    spec:
      template:
          spec:
            hostIPC: true
            restartPolicy: OnFailure
            containers:
              - name: habana-ai-base-container
                image: vault.habana.ai/gaudi-docker/1.21.0/ubuntu22.04/habanalabs/pytorch-installer-2.6.0:latest
                workingDir: /root
                command: ["hl-smi"]
                securityContext:
                  capabilities:
                      add: ["SYS_NICE"]
                resources:
                  limits:
                      habana.ai/gaudi: 8
                      memory: 409Gi
                      hugepages-2Mi: 9500Mi
    ```
    {: codeblock}

1. Apply the job in your cluster.
    ```sh
    oc apply -f config.yaml
    ```
    {: pre}

1. Wait for the pods to start, then verify the job completed.
    ```sh
    oc get po -n default
    ```
    {: pre}

    Example
    ```sh
    NAME                          READY   STATUS      RESTARTS   AGE
    habanalabs-gaudi-demo-kmdcp   0/1     Completed   0          2m32s
    ```
    {: screen}

1. Describe the job pod for more details.
    ```sh
    oc describe po habanalabs-gaudi-demo-kmdcp
    ```
    {: pre}

    ```sh
    Name:             habanalabs-gaudi-demo-kmdcp
    Namespace:        default
    Priority:         0
    Service Account:  default
    Node:             test-csrq76620trmo9r8j7u0-btsstagevpc-gaudi3s-00013059/10.180.0.83
    Start Time:       Tue, 27 May 2025 14:41:50 -0400
    Labels:           batch.kubernetes.io/controller-uid=c3b33c8a-5fef-4312-9d59-c8b13c03313a
                      batch.kubernetes.io/job-name=habanalabs-gaudi-demo
                      controller-uid=c3b33c8a-5fef-4312-9d59-c8b13c03313a
                      job-name=habanalabs-gaudi-demo
    Annotations:      cni.projectcalico.org/containerID: 7c883dfa9c681ee2c4128b1a5412d4dc181842d0de2a4b7b8019eefc06df37ca
                      cni.projectcalico.org/podIP: 
                      cni.projectcalico.org/podIPs: 
    Status:           Succeeded
    IP:               172.17.151.97
    IPs:
      IP:           172.17.151.97
    Controlled By:  Job/habanalabs-gaudi-demo
    Containers:
      habana-ai-base-container:
        Container ID:  cri-o://d75288e9b467f3f820e05e770bbc3d9a2b11cbf8155a54a129fc083d5d507571
        Image:         vault.habana.ai/gaudi-docker/1.21.0/ubuntu22.04/habanalabs/pytorch-installer-2.6.0:latest
        Image ID:      vault.habana.ai/gaudi-docker/1.21.0/ubuntu22.04/habanalabs/pytorch-installer-2.6.0@sha256:cd599626a8f4d1c3a7b354ccf4ef73e19196f09030d02261d4900bf3467a964c
        Port:          <none>
        Host Port:     <none>
        Command:
          hl-smi
        State:          Terminated
          Reason:       Completed
          Exit Code:    0
          Started:      Tue, 27 May 2025 14:41:53 -0400
          Finished:     Tue, 27 May 2025 14:41:54 -0400
        Ready:          False
        Restart Count:  0
        Limits:
          habana.ai/gaudi:  8
          hugepages-2Mi:    9500Mi
          memory:           409Gi
        Requests:
          habana.ai/gaudi:  8
          hugepages-2Mi:    9500Mi
          memory:           409Gi
        Environment:        <none>
        Mounts:
          /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-8vn42 (ro)
    Conditions:
      Type                        Status
      PodReadyToStartContainers   False 
      Initialized                 True 
      Ready                       False 
      ContainersReady             False 
      PodScheduled                True 
    Volumes:
      kube-api-access-8vn42:
        Type:                    Projected (a volume that contains injected data from multiple sources)
        TokenExpirationSeconds:  3607
        ConfigMapName:           kube-root-ca.crt
        ConfigMapOptional:       <nil>
        DownwardAPI:             true
        ConfigMapName:           openshift-service-ca.crt
        ConfigMapOptional:       <nil>
    QoS Class:                   Burstable
    Node-Selectors:              <none>
    Tolerations:                 node.kubernetes.io/memory-pressure:NoSchedule op=Exists
                                  node.kubernetes.io/not-ready:NoExecute op=Exists for 300s
                                  node.kubernetes.io/unreachable:NoExecute op=Exists for 300s
    Events:
      Type    Reason          Age   From               Message
      ----    ------          ----  ----               -------
      Normal  Scheduled       53s   default-scheduler  Successfully assigned default/habanalabs-gaudi-demo-kmdcp to test-csrq76620trmo9r8j7u0-btsstagevpc-gaudi3s-00013059
      Normal  AddedInterface  52s   multus             Add eth0 [172.17.151.97/32] from k8s-pod-network
      Normal  Pulling         52s   kubelet            Pulling image "vault.habana.ai/gaudi-docker/1.21.0/ubuntu22.04/habanalabs/pytorch-installer-2.6.0:latest"
      Normal  Pulled          50s   kubelet            Successfully pulled image "vault.habana.ai/gaudi-docker/1.21.0/ubuntu22.04/habanalabs/pytorch-installer-2.6.0:latest" in 2.146s (2.146s including waiting). Image size: 5188441181 bytes.
      Normal  Created         50s   kubelet            Created container: habana-ai-base-container
      Normal  Started         50s   kubelet            Started container habana-ai-base-container
    ```
    {: screen}

1. Get the pod logs to see the Gaudi device details.
    ```sh
    oc logs habanalabs-gaudi-demo-kmdcp
    ```
    {: pre}

    Example output    
    ```sh
    +-----------------------------------------------------------------------------+
    | HL-SMI Version:                              hl-1.21.0-fw-59.2.1.0          |
    | Driver Version:                                     1.20.1-366eb9c          |
    | Nic Driver Version:                                 1.20.1-213b09b          |
    |-------------------------------+----------------------+----------------------+
    | AIP  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncor-Events|
    | Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | AIP-Util  Compute M. |
    |===============================+======================+======================|
    |   0  HL-325L             N/A  | 0000:e9:00.0     N/A |                   0  |
    | N/A   36C   P0  228W /  900W  |   672MiB / 131072MiB |     0%            0% |
    |-------------------------------+----------------------+----------------------+
    |   1  HL-325L             N/A  | 0000:c1:00.0     N/A |                   0  |
    | N/A   37C   P0  226W /  900W  |   672MiB / 131072MiB |     0%            0% |
    |-------------------------------+----------------------+----------------------+
    |   2  HL-325L             N/A  | 0000:b7:00.0     N/A |                   0  |
    | N/A   36C   P0  225W /  900W  |   672MiB / 131072MiB |     0%            0% |
    |-------------------------------+----------------------+----------------------+
    |   3  HL-325L             N/A  | 0000:ad:00.0     N/A |                   0  |
    | N/A   40C   P0  228W /  900W  |   672MiB / 131072MiB |     0%            0% |
    |-------------------------------+----------------------+----------------------+
    |   4  HL-325L             N/A  | 0000:a3:00.0     N/A |                   0  |
    | N/A   36C   P0  228W /  900W  |   672MiB / 131072MiB |     0%            0% |
    |-------------------------------+----------------------+----------------------+
    |   5  HL-325L             N/A  | 0000:df:00.0     N/A |                   0  |
    | N/A   39C   P0  229W /  900W  |   672MiB / 131072MiB |     0%            0% |
    |-------------------------------+----------------------+----------------------+
    |   6  HL-325L             N/A  | 0000:d5:00.0     N/A |                   0  |
    | N/A   36C   P0  231W /  900W  |   672MiB / 131072MiB |     0%            0% |
    |-------------------------------+----------------------+----------------------+
    |   7  HL-325L             N/A  | 0000:cb:00.0     N/A |                   0  |
    | N/A   38C   P0  227W /  900W  |   672MiB / 131072MiB |     0%            0% |
    |-------------------------------+----------------------+----------------------+
    | Compute Processes:                                               AIP Memory |
    |  AIP       PID   Type   Process name                             Usage      |
    |=============================================================================|
    |   0        N/A   N/A    N/A                                      N/A        |
    |   1        N/A   N/A    N/A                                      N/A        |
    |   2        N/A   N/A    N/A                                      N/A        |
    |   3        N/A   N/A    N/A                                      N/A        |
    |   4        N/A   N/A    N/A                                      N/A        |
    |   5        N/A   N/A    N/A                                      N/A        |
    |   6        N/A   N/A    N/A                                      N/A        |
    |   7        N/A   N/A    N/A                                      N/A        |
    +=============================================================================+
    ```
    {: screen}


 
