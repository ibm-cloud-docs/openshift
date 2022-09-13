---

copyright:
  years: 2014, 2022
lastupdated: "2022-09-13"

keywords: kubernetes, openshift

subcollection: openshift

---


{{site.data.keyword.attribute-definition-list}}



# Deploying apps in OpenShift clusters
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

You can create apps through various methods in the {{site.data.keyword.redhat_openshift_notm}} console by using the **Developer** perspective. For more information, see the [{{site.data.keyword.redhat_openshift_notm}} documentation](https://docs.openshift.com/container-platform/4.9/applications/creating_applications/odc-creating-applications-using-developer-perspective.html){: external}.
{: shortdesc}

1. From the [{{site.data.keyword.redhat_openshift_notm}} clusters console](https://cloud.ibm.com/kubernetes/clusters?platformType=openshift){: external}, select your cluster.
2. Click **{{site.data.keyword.redhat_openshift_notm}} web console**.
3. From the perspective switcher, select **Developer**. The {{site.data.keyword.redhat_openshift_notm}} web console switches to the Developer perspective, and the menu now offers items such as **+Add**, **Topology**, and **Builds**.
4. Click **+Add**.
5. In the **Add** pane menu bar, select the **Project** that you want to create your app in from the drop-down list.
6. Click the method that you want to use to add your app, and follow the instructions. For example, click **From Git**.

### Deploying apps through the CLI
{: #deploy_apps_cli}

To create an app in your {{site.data.keyword.openshiftlong_notm}} cluster, use the `oc new-app` [command](https://docs.openshift.com/container-platform/4.9/cli_reference/openshift_cli/developer-cli-commands.html#new-app){: external}. For example, you might refer to a public GitHub repo, a public GitLab repo with a URL that ends in `.git`, or another local or remote repo. For more information, [try out the tutorial](/docs/openshift?topic=openshift-openshift_tutorial#openshift_deploy_app) and review the [{{site.data.keyword.redhat_openshift_notm}} documentation](https://docs.openshift.com/container-platform/4.9/applications/creating_applications/odc-creating-applications-using-developer-perspective.html){: external}.
{: shortdesc}

```sh
oc new-app --name <app_name> https://github.com/<path_to_app_repo> [--context-dir=<subdirectory>]
```
{: pre}

**What does the `new-app` command do?**

The `new-app` command creates a build configuration and app image from the source code, a deployment configuration to deploy the container to pods in your cluster, and a service to expose the app within the cluster. For more information about the build process and other sources besides Git, see the [{{site.data.keyword.redhat_openshift_notm}} documentation](https://docs.openshift.com/container-platform/4.9/applications/creating_applications/odc-creating-applications-using-developer-perspective.html){: external}.

## Deploying apps to specific worker nodes by using labels
{: #node_affinity}

When you deploy an app, the app pods indiscriminately deploy to various worker nodes in your cluster. Sometimes, you might want to restrict the worker nodes that the app pods to deploy to. For example, you might want app pods to deploy to only worker nodes in a certain worker pool because those worker nodes are on bare metal machines. To designate the worker nodes that app pods must deploy to, add an affinity rule to your app deployment.
{: shortdesc}

Before you begin
- [Access your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-access_cluster).
- Make sure that you are assigned a [service access role](/docs/openshift?topic=openshift-users#checking-perms) that grants the appropriate Kubernetes RBAC role so that you can work with Kubernetes resources in the {{site.data.keyword.redhat_openshift_notm}} project.
- **Optional**: [Set a label for the worker pool](/docs/openshift?topic=openshift-add_workers#worker_pool_labels) that you want to run the app on.

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
                        ibm-cloud.kubernetes.io/worker-version=1.23_1534
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

## Deploying an app on a GPU machine
{: #gpu_app}

If you have a [GPU machine type](/docs/openshift?topic=openshift-planning_worker_nodes#planning_worker_nodes), you can schedule mathematically intensive workloads onto the worker node. For example, you might run a 3D app that uses the Compute Unified Device Architecture (CUDA) platform to share the processing load across the GPU and CPU to increase performance.
{: shortdesc}

In the following steps, you learn how to deploy workloads that require the GPU. You can also deploy apps that don't need to process their workloads across both the GPU and CPU. After, you might find it useful to play around with mathematically intensive workloads such as the [TensorFlow](https://www.tensorflow.org/){: external} machine learning framework with [this Kubernetes demo](https://github.com/pachyderm/pachyderm/tree/master/examples/ml/tensorflow){: external}.


Before you begin
- Create a [cluster](/docs/openshift?topic=openshift-clusters#clusters_standard) or [worker pool](/docs/openshift?topic=openshift-add_workers#add_pool) that uses a GPU bare metal flavor. Keep in mind that setting up a bare metal machine can take more than one business day to complete.
- Make sure that you are assigned a [service access role](/docs/openshift?topic=openshift-users#checking-perms) that grants the appropriate Kubernetes RBAC role so that you can work with Kubernetes resources in the cluster.
- [Install the Node Feature Discovery and NVIDIA GPU operators for you cluster version](https://docs.nvidia.com/datacenter/cloud-native/gpu-operator/getting-started.html){: external}.

    You must use NVIDIA GPU operator version 1.3.1 or later. When you install the Node Feature Discovery operator, select the update channel that matches your {{site.data.keyword.redhat_openshift_notm}} cluster version. Do not install the operators through another method, such as a Helm chart.
    {: important}

- **Version 4.6 clusters**: Make sure that your worker nodes are updated to at least version `4.6.25_1541_openshift`. When you create an instance of the `ClusterPolicy` for the GPU operator, you must enter `450.80.02` for the **Driver Config** version.

To run a workload on a GPU machine,

1. Create a YAML file. In this example, a `Job` YAML manages batch-like workloads by making a short-lived pod that runs until the command that it is scheduled to complete successfully terminates.

    For GPU workloads, you must always provide the `resources: limits: nvidia.com/gpu` field in the YAML specification.
    {: note}

    ```yaml
    apiVersion: batch/v1
    kind: Job
    metadata:
      name: nvidia-smi
      labels:
        name: nvidia-smi
    spec:
      template:
        metadata:
          labels:
            name: nvidia-smi
        spec:
          containers:
          - name: nvidia-smi
            image: nvidia/cuda:9.1-base-ubuntu16.04
            command: [ "/usr/test/nvidia-smi" ]
            imagePullPolicy: IfNotPresent
            resources:
              limits:
                nvidia.com/gpu: 2
            volumeMounts:
            - mountPath: /usr/test
              name: nvidia0
          volumes:
            - name: nvidia0
              hostPath:
                path: /usr/bin
          restartPolicy: Never
    ```
    {: codeblock}
    
    | Component | Description |
    | ---- | ------- |
    | Metadata and label names | Enter a name and a label for the job, and use the same name in both the file's metadata and the `spec template` metadata. For example, `nvidia-smi`. |
    | `containers.image` | Provide the image that the container is a running instance of. In this example, the value is set to use the DockerHub CUDA image:`nvidia/cuda:9.1-base-ubuntu16.04`. |
    | `containers.command` | Specify a command to run in the container. In this example, the `[ "/usr/test/nvidia-smi" ]` command refers to a binary file that is on the GPU machine, so you must also set up a volume mount. |
    | `containers.imagePullPolicy` | To pull a new image only if the image is not currently on the worker node, specify `IfNotPresent`. |
    | `resources.limits` | For GPU machines, you must specify the resource limit. The Kubernetes [Device Plug-in](https://kubernetes.io/docs/concepts/extend-kubernetes/compute-storage-net/device-plugins/){: external} sets the default resource request to match the limit. \n * You must specify the key as `nvidia.com/gpu`. \n * Enter the whole number of GPUs that you request, such as `2`. Note that container pods don't share GPUs and GPUs can't be overcommitted. For example, if you have only 1 `mg1c.16x128` machine, then you have only 2 GPUs in that machine and can specify a maximum of `2`. |
    | `volumeMounts` | Name the volume that is mounted onto the container, such as `nvidia0`. Specify the `mountPath` on the container for the volume. In this example, the path `/usr/test` matches the path that is used in the job container command. |
    | `volumes` | Name the job volume, such as `nvidia0`. In the GPU worker node's `hostPath`, specify the volume's `path` on the host, in this example, `/usr/bin`. The container `mountPath` is mapped to the host volume `path`, which gives this job access to the NVIDIA binaries on the GPU worker node for the container command to run. |
    {: caption="Table 1. Understanding your YAML components" caption-side="top"}

2. Apply the YAML file. For example:

    ```sh
    oc apply -f nvidia-smi.yaml
    ```
    {: pre}

3. Check the job pod by filtering your pods by the `nvidia-sim` label. Verify that the **STATUS** is **Completed**.

    ```sh
    oc get pod -a -l 'name in (nvidia-sim)'
    ```
    {: pre}

    Example output

    ```sh
    NAME                  READY     STATUS      RESTARTS   AGE
    nvidia-smi-ppkd4      0/1       Completed   0          36s
    ```
    {: screen}

4. Describe the pod to see how the GPU device plug-in scheduled the pod.
    - In the `Limits` and `Requests` fields, see that the resource limit that you specified matches the request that the device plug-in automatically set.
    - In the events, verify that the pod is assigned to your GPU worker node.

        ```sh
        oc describe pod nvidia-smi-ppkd4
        ```
        {: pre}

        Example output
        ```sh
        NAME:           nvidia-smi-ppkd4
        Namespace:      default
        ...
        Limits:
            nvidia.com/gpu:  2
        Requests:
            nvidia.com/gpu:  2
        ...
        Events:
        Type    Reason                 Age   From                     Message
        ----    ------                 ----  ----                     -------
        Normal  Scheduled              1m    default-scheduler        Successfully assigned nvidia-smi-ppkd4 to 10.xxx.xx.xxx
        ...
        ```
        {: screen}

5. To verify that the job used the GPU to compute its workload, you can check the logs. The `[ "/usr/test/nvidia-smi" ]` command from the job queried the GPU device state on the GPU worker node.

    ```sh
    oc logs nvidia-sim-ppkd4
    ```
    {: pre}

    Example output

    ```sh
    +-----------------------------------------------------------------------------+
    | NVIDIA-SMI 390.12                 Driver Version: 390.12                    |
    |-------------------------------+----------------------+----------------------+
    | GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
    | Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
    |===============================+======================+======================|
    |   0  Tesla K80           Off  | 00000000:83:00.0 Off |                  Off |
    | N/A   37C    P0    57W / 149W |      0MiB / 12206MiB |      0%      Default |
    +-------------------------------+----------------------+----------------------+
    |   1  Tesla K80           Off  | 00000000:84:00.0 Off |                  Off |
    | N/A   32C    P0    63W / 149W |      0MiB / 12206MiB |      1%      Default |
    +-------------------------------+----------------------+----------------------+

    +-----------------------------------------------------------------------------+
    | Processes:                                                       GPU Memory |
    |  GPU       PID   Type   Process name                             Usage      |
    |=============================================================================|
    |  No running processes found                                                 |
    +-----------------------------------------------------------------------------+
    ```
    {: screen}

    In this example, you see that both GPUs were used to execute the job because both the GPUs were scheduled in the worker node. If the limit is set to 1, only 1 GPU is shown.

Now that you deployed a test GPU workload, you might want to set up your cluster to run a tool that relies on GPU processing, such as [IBM Maximo Visual Inspection](https://www.ibm.com/products/maximo/remote-monitoring){: external}.

## Deploying Cloud Paks, licensed software, and other integrations
{: #openshift_app_cloud_paks}

You can deploy IBM Cloud Paks&trade;, licensed software, and other 3rd party integrations to {{site.data.keyword.openshiftlong_notm}} clusters. You have various tools to deploy integrations, such as {{site.data.keyword.cloud_notm}} service binding, managed add-ons, Helm charts, and more. After you install an integration, follow that product's documentation for configuration settings and other instructions to integrate with your apps. For more information, see [Enhancing cluster capabilities with integrations](/docs/openshift?topic=openshift-supported_integrations).
{: shortdesc}

## Accessing the {{site.data.keyword.redhat_openshift_notm}} web console
{: #openshift_console}

You can use the {{site.data.keyword.redhat_openshift_notm}} console to manage your apps, deploy apps from the catalog, and access built-in functionality to help you operate your cluster. The {{site.data.keyword.redhat_openshift_notm}} console is deployed to your cluster by default, instead of the Kubernetes dashboard as in community Kubernetes clusters.
{: shortdesc}

For more information about the console, see the [{{site.data.keyword.redhat_openshift_notm}} documentation](https://docs.openshift.com/container-platform/4.9/web_console/web-console.html){: external}.

### {{site.data.keyword.redhat_openshift_notm}} console overview
{: #openshift_console4_overview}

1. From the [{{site.data.keyword.redhat_openshift_notm}} clusters console](https://cloud.ibm.com/kubernetes/clusters?platformType=openshift){: external}, select your {{site.data.keyword.redhat_openshift_notm}} cluster, then click **OpenShift web console**.
2. To work with your cluster in the CLI, click your profile **`IAM#user.name@email.com` > Copy Login Command**. Display and copy the `oc login` token command into your command line to authenticate by using the CLI.

You can explore the following areas of the {{site.data.keyword.redhat_openshift_notm}} web console.

Administrator perspective
:   The Administrator perspective is available from the side navigation menu perspective switcher. From the Administrator perspective, you can manage and set up the components that your team needs to run your apps, such as projects for your workloads, networking, and operators for integrating IBM, Red Hat, 3rd party, and custom services into the cluster. For more information, see [Viewing cluster information](http://docs.openshift.com/container-platform/4.9/web_console/using-dashboard-to-get-cluster-information.html){: external} in the {{site.data.keyword.redhat_openshift_notm}} documentation.

Developer perspective
:   The Developer perspective is available from the side navigation menu perspective switcher. From the Developer perspective, you can add apps to your cluster in a variety of ways, such as from Git repositories,container images, drag-and-drop or uploaded YAML files, operator catalogs, and more. The **Topology** view presents a unique way to visualize the workloads that run in a project and navigate their components from sidebars that aggregate related resources, including pods, services, routes, and metadata. For more information, see [Developer perspective](https://docs.openshift.com/container-platform/4.9/web_console/web-console-overview.html{: external} in the {{site.data.keyword.redhat_openshift_notm}} documentation. 







