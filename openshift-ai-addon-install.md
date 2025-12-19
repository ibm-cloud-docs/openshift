---

copyright: 
  years: 2024, 2025
lastupdated: "2025-12-19"


keywords: openshift, {{site.data.keyword.openshiftlong_notm}}, ai, add-on

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}



# Installing the Red Hat OpenShift AI add-on
{: #ai-addon-install}

Follow the steps to install the OpenShift AI add-on to an existing cluster. 

Want to deploy the OpenShift AI operator on a new cluster? Try the [OpenShift AI on IBM Cloud](https://cloud.ibm.com/catalog/7a4d68b4-cf8b-40cd-a3d1-f49aff526eb3/architecture/roks-rhoai-c24ae512-8b25-43d7-8fb3-4173c7e94472-global){: external} deployable architecture. 
{: tip}

## Minimum requirements
{: #ai-min}

Review the following considerations before setting up the add-on. 

- Review the [Supported cluster add-on versions](/docs/openshift?topic=openshift-supported-cluster-addon-versions) and determine which add-on version to install in your cluster.
- Your cluster must have at least 2 worker nodes. Each worker node must have a minimum of 8vCPU and 32GB memory.
- Your worker nodes must use the RHCOS operating system.
- You must allow outbound traffic from your cluster to install the required operators.

## Supported versions
{: #versions}

Review the supported OpenShift AI add-on versions and the corresponding [OpenShift AI](https://www.redhat.com/en/products/ai/openshift-ai){: external} and [{{site.data.keyword.openshiftshort}}](/docs/openshift?topic=openshift-openshift_versions) versions. 

| OpenShift AI add-on version | Red Hat OpenShift AI version |	Supported Red Hat OpenShift on IBM Cloud versions |
| --------------------------  | ---------------------------- | -------------------------------------------------- |
| 418 | 2.22 | 4.18, 4.19 |
| 417 | 2.22 | 4.17, 4.18 |
| 416 | 2.22 | 4.16, 4.17 | 
{: caption="Supported AI add-on versions and corresponding versions for Red Hat OpenShift AI and Red Hat OpenShift on IBM Cloud". caption-side="bottom"}

## Considerations
{: #ai-consideration}

- To use all the capabilities provided by OpenShift AI, at least 1 GPU is recommended.
- Your cluster can have a mix of GPU and non-GPU nodes. However, if you use this configuration, make sure to deploy your app on a GPU node to leverage its resources.
- Beginning with version 2.19.0 of OpenShift AI Operator, KServe is available in either Advanced or Standard mode. By default, when you install KServe using the OpenShift AI using the IBM Cloud add-on, it is installed in Standard mode. If you want to use Advanced mode, you must complete the [optional steps](#ai-install-kserve) after installing the add-on.


## Before you begin
{: #ai-before}
{: cli}

1. [Log in to your account. If applicable, target the appropriate resource group. Set the context for your cluster.](/docs/containers?topic=containers-access_cluster)

1. **Optional**: If you don't already have one, [create a VPC Public Gateway](/docs/vpc?topic=vpc-create-public-gateways).

1. If you want to use the [OpenShift Pipelines, Node Feature Discovery, or NVIDIA GPU operators](/docs/openshift?topic=openshift-ai-addon-install&interface=ui#ai-ops-rec) with the OpenShift AI add-on, you must disable outbound traffic protection. If you do not want to use those operators, skip this step. 

    Disabling outbound traffic protection permits all external network connections. See [Managing outbound traffic protection in VPC clusters](/docs/openshift?topic=openshift-sbd-allow-outbound) for more information.
    {: note}

    ```sh
    ibmcloud oc vpc outbound-traffic-protection disable --cluster CLUSTER
    ```
    {: pre}

1. Enable OperatorHub on your cluster.

    ```sh
    oc patch operatorhub cluster --type json -p '[{"op": "add", "path": "/spec/disableAllDefaultSources", "value": false}]' 
    ```
    {: pre}


## Before you begin
{: #ai-before-ui}
{: ui}

1. [Log in to your account. If applicable, target the appropriate resource group. Set the context for your cluster.](/docs/containers?topic=containers-access_cluster)

1. **Optional**: If you don't already have one, [create a VPC Public Gateway](/docs/vpc?topic=vpc-create-public-gateways).

1. If you want to use the [OpenShift Pipelines, Node Feature Discovery, or NVIDIA GPU operators](/docs/openshift?topic=openshift-ai-addon-install&interface=ui#ai-ops-rec) with the OpenShift AI add-on, you must disable outbound traffic protection. If you do not want to use those operators, skip this step. 

    Disabling outbound traffic protection permits all external network connections. See [Managing outbound traffic protection in VPC clusters](/docs/openshift?topic=openshift-sbd-allow-outbound) for more information.
    {: note}

    1. In the console, navigate to your [Clusters page](https://cloud.ibm.com/containers/cluster-management/clusters){: external} and click the relevant cluster.
    2. On the Overview page for the cluster, find the **Networking** section and select the **Outbound traffic protection disabled** option.

1. Enable OperatorHub on your cluster.

    ```sh
    oc patch operatorhub cluster --type json -p '[{"op": "add", "path": "/spec/disableAllDefaultSources", "value": false}]' 
    ```
    {: pre}


## Step 1: Choose customization options 
{: #ai-custom-step}


You can enhance your Red Hat OpenShift AI projects by specifying different options to include with your add-on installation, such as data pipelines for building portable machine learning workflows or tools for managing and scaling your resources. You can also customize upgrade policies and deletion policies. For descriptions of each available option, see [OpenShift AI customization options](#custom-options). If you do not include a specific option when you install the add-on, the default value applies. These options are managed by the Red Hat OpenShift AI platform. 

In the CLI, run the command to list all options. In the UI, these options are listed in the **Capabilities** section during installation. 

```sh
ibmcloud oc cluster addon options --addon openshift-ai
```
{: pre}

## Step 2: Review additional recommended operators
{: #ai-ops-rec-cli}
{: cli}

You can choose to also install additional operators that are recommended for the use of certain OpenShift AI features. If they are not already installed on your cluster, you can choose to include them in the add-on installation. Or, you can install them at anytime by using OperatorHub or by following the operator-specific installation steps. To use these operators, you must [disable outbound traffic protection](/docs/openshift?topic=openshift-sbd-allow-outbound) for your cluster. 

You are responsible for managing these operators, including but not limited to updating, monitoring, recovery, and re-installation.
{: important}

The following operators are recommended. 
- [OpenShift Pipelines](https://docs.redhat.com/documentation/red_hat_openshift_pipelines/1.16/html/about_openshift_pipelines/index){: external}
    - [Installing OpenShift Pipelines](https://docs.redhat.com/documentation/red_hat_openshift_pipelines/1.16/html/installing_and_configuring/installing-pipelines){: external}
- [Node Feature Discovery](https://docs.redhat.com/en/documentation/openshift_container_platform/4.16/html/specialized_hardware_and_driver_enablement/psap-node-feature-discovery-operator){: external}
    - [Installing the Node Feature Discovery Operator](https://docs.redhat.com/en/documentation/openshift_container_platform/4.16/html/specialized_hardware_and_driver_enablement/psap-node-feature-discovery-operator#installing-the-node-feature-discovery-operator_psap-node-feature-discovery-operator){: external}
- [NVIDIA GPU Operator](https://docs.nvidia.com/datacenter/cloud-native/gpu-operator/latest/index.html){: external}
    - [Installing the NVIDIA GPU Operator](https://docs.nvidia.com/datacenter/cloud-native/gpu-operator/latest/getting-started.html){: external}


Some of these operators might include additional customizations that you can choose to specify when you install the add-on. Review the list of [customizations available for the recommended operators](/docs/openshift?topic=openshift-ai-addon-install&interface=cli#ai-ops-rec-cli).

## Step 3: Install the add-on in the CLI
{: #ai-install-cli}
{: cli}

Run the command to install the Red Hat OpenShift AI add-on. Specify [customizations](/docs/openshift?topic=openshift-ai-addon-install&interface=cli#ai-ops-rec-cli) with the format `--parameter PARAM=VALUE`. For example, to include the Data Science Pipelines option, specify `--parameter oaiDataSciencePipelines=Managed`.

To include the recommended operators when installing the add-on with the CLI, specify the following options when you run the installation command.
- OpenShift Pipelines: `--parameter pipelineEnabled=true`
- Node Feature Discovery: `--parameter nfdEnabled=true`
- NVIDIA GPU Operator: `--parameter nvidiaEnabled=true`

For a list of available versions, see [Supported versions](#versions).


Installation command.

```sh
ibmcloud oc cluster addon enable openshift-ai --cluster CLUSTER [-f] [--param PARAM] [-q] [--version VERSION]
```
{: pre}

Example command to install the add-on with automatic minor and patch updates, CodeFlare, and KServe enabled.

```sh
ibmcloud oc cluster addon enable openshift-ai --cluster CLUSTER --param oaiInstallPlanApproval=Automatic --param oaiCodeflare=Managed --param oaiKserve=Managed
```
{: pre}

## Step 2: Review the additional recommended operators
{: #ai-ops-rec}
{: ui}

You can choose to also install additional operators that are recommended for the use of certain OpenShift AI features. If they are not already installed on your cluster, you can choose to include them in the add-on installation. Or, you can install them at anytime by using OperatorHub or by following the operator-specific installation steps. To use these operators, you must [disable outbound traffic protection](/docs/openshift?topic=openshift-sbd-allow-outbound) for your cluster. 

You are responsible for managing these operators, including but not limited to updating, monitoring, recovery, and re-installation.
{: important}

The following operators are recommended. 
- [OpenShift Pipelines](https://docs.redhat.com/documentation/red_hat_openshift_pipelines/1.16/html/about_openshift_pipelines/index){: external}
    - [Installing OpenShift Pipelines](https://docs.redhat.com/documentation/red_hat_openshift_pipelines/1.16/html/installing_and_configuring/installing-pipelines){: external}
- [Node Feature Discovery](https://docs.redhat.com/en/documentation/openshift_container_platform/4.16/html/specialized_hardware_and_driver_enablement/psap-node-feature-discovery-operator){: external}
    - [Installing the Node Feature Discovery Operator](https://docs.redhat.com/en/documentation/openshift_container_platform/4.16/html/specialized_hardware_and_driver_enablement/psap-node-feature-discovery-operator#installing-the-node-feature-discovery-operator_psap-node-feature-discovery-operator){: external}
- [NVIDIA GPU Operator](https://docs.nvidia.com/datacenter/cloud-native/gpu-operator/latest/index.html){: external}
    - [Installing the NVIDIA GPU Operator](https://docs.nvidia.com/datacenter/cloud-native/gpu-operator/latest/getting-started.html){: external}


Some of these operators might include additional customizations that you can choose to specify when you install the add-on. Review the list of [customizations available for the recommended operators](/docs/openshift?topic=openshift-ai-addon-install&interface=cli#ai-ops-rec-cli).

## Step 3: Install the add-on in the UI
{: #ai-install-ui}
{: ui}

Install the Red Hat OpenShift AI add-on with the UI. 

1. Navigate to your [cluster page](https://cloud.ibm.com/containers/cluster-management/clusters){: external} and click the relevant cluster. 

2. On the cluster details page, find the **Add-ons** section. Find the **Red Hat OpenShift AI** option and click **Install**.

3. In the **Capabilities** section, review the description of the available add-on customization options and enable the options you want to include with the installation. 

4. In the **Additional recommended operators** section, click to expand each operator and select the customization options you want to include. These additional operators and customizations are recommended for certain Red Hat OpenShift AI features. You can choose to install these options later by using OperatorHub or by following the operator-specific installation steps. 

    You are responsible for managing these operators, including but not limited to updating, monitoring, recovery, and re-installation.
    {: important}

5. Click **Install**.

## Step 4: Access the OpenShift AI dashboard
{: #ai-dashboard}

After you install the OpenShift AI add-on, you can access the [OpenShift AI dashboard](https://docs.redhat.com/en/documentation/red_hat_openshift_ai_cloud_service/1/html/getting_started_with_red_hat_openshift_ai_cloud_service/logging-in_get-started?extIdCarryOver=true&sc_cid=RHCTG0180000382536#viewing-installed-components_get-started){: external}. 

1. From your cluster overview page, click **OpenShift web console**.
2. From the **Application launcher** ![Application launcher](../icons/thumbnail.svg "Application launcher"), select the **Red Hat OpenShift AI** dashboard option. 
3. If prompted, click `Log in with OpenShift`.



## Optional: Setting up KServe in Advanced mode
{: #ai-install-kserve}

If you want to use KServe in Advanced mode, you must complete the following steps.

1. Install the OpenShift Serverless Operator from OperatorHub.
1. Install the OpenShift Service Mesh Operator from OperatorHub.
1. Set the service mesh management state to `Managed` in your Data Science Cluster Initialization CR.
    ```yaml
    serviceMesh:
        controlPlane:
            metricsCollection: Istio
            name: data-science-smcp
            namespace: istio-system
        managementState: Managed
    ```
    {: pre}

1. Set the KServe serving management state to `Managed` in your Data Science Cluster custom resource.
    ```yaml
    kserve:
        managementState: Managed
        serving:
          managementState: Managed
          name: knative-serving
    ```
    {: pre}

## OpenShift AI customization options
{: #custom-options}

Review the customization options available for the OpenShift AI add-on. These operators are managed by the Red Hat OpenShift AI platform. 

To include an option when you [install the OpenShift AI add-on with the CLI](/docs/openshift?topic=openshift-ai-addon-install&interface=cli#ai-install-cli), include the option with the `--parameter PARAM=VALUE` format when you run the `ibmcloud oc cluster addon enable openshift-ai`. For example, to install the add-on with the Data Science Pipelines option, specify `--parameter oaiDataSciencePipelines=Managed`.
{: cli}

To include an option when you [install the OpenShift AI add-on with the UI](/docs/openshift?topic=openshift-ai-addon-install&interface=ui#ai-install-ui), click to enable the option when prompted. These options are included in the **Capabilities** section. 
{: ui}

| Customization | CLI Parameter | Description | Values | Default value |
| ------------- | --------- | ----------- | ------ | ------------- |
| OpenShift AI platform minor and patch updates approval policy | `oaiInstallPlanApproval` | Apply minor and patch updates automatically or manually. | `Automatic` or `Manual` |  `Automatic` |                   
| OpenShift AI deletion policy | `oaiDeletePolicy` | Retain or delete any operators or components installed by the add-on if the add-on is removed. | `Retain` or `Delete` | `Retain` |         
| Open Data Hub Dashboard | `oaiDashboard` | Enable or disable the component. If enabled, it is managed by OpenShift AI platform. | `Managed` to enable \n`Removed` to disable | `Managed` (enabled) |           
| Kueue | `oaiKueue` | Enable or disable the component. If enabled, it is managed by OpenShift AI platform. | `Managed` to enable \n`Removed` to disable | `Managed` (enabled) |                                       
| CodeFlare | `oaiCodeflare` | Enable or disable the component. If enabled, it is managed by OpenShift AI platform. | `Managed` to enable \n`Removed` to disable | `Managed` (enabled) |                                  
| ModelMesh Serving | `oaiModelmeshserving` | Enable or disable the component. If enabled, it is managed by OpenShift AI platform. | `Managed` to enable \n`Removed` to disable | `Managed` (enabled) |                           
| Workbench | `oaiWorkbenches` | Enable or disable the component. If enabled, it is managed by OpenShift AI platform. | `Managed` to enable \n`Removed` to disable | `Managed` (enabled) |                                 
| Data Science Pipelines | `oaiDataSciencePipelines` | Enable or disable the component. If enabled, it is managed by OpenShift AI platform. | `Managed` to enable \n`Removed` to disable | `Managed` (enabled) |                         
| KServe | `oaiKserve` | Enable or disable the component. If enabled, it is managed by OpenShift AI platform. | `Managed` to enable \n`Removed` to disable | `Managed` (enabled) |                                       
| Ray | `oaiRay` | Enable or disable the component. If enabled, it is managed by OpenShift AI platform. | `Managed` to enable \n`Removed` to disable | `Managed` (enabled) | 
{: caption="OpenShift AI add-on customization options and CLI parameters." caption-side="bottom"}            


## Additional recommended operators
{: #rec-ops-custom}

Review the [recommended operators](/docs/openshift?topic=openshift-ai-addon-install&interface=ui#ai-ops-rec) and the optional customizations you can include during installation. You are responsible for managing these operators, including but not limited to updating, monitoring, recovery, and re-installation.

To include a customization for an operator when you [install the OpenShift AI add-on with the CLI](/docs/openshift?topic=openshift-ai-addon-install&interface=cli#ai-install-cli), include the option with the `--parameter PARAM=VALUE` format when you run the `ibmcloud oc cluster addon enable openshift-ai`. For example, to include the NVIDIA GPUDirect Storage customization for the NVIDIA operator, specify `--parameter nvidiaGpuDirectStorageEnabled=true`.
{: cli}

To include a customization for an operator when you [install the OpenShift AI add-on with the UI](/docs/openshift?topic=openshift-ai-addon-install&interface=ui#ai-install-ui), click to enable the option when prompted. Note that there are additional NVIDIA operators with default settings that can only be changed in the CLI, or by editing the ClusterPolicy.
{: ui}


| Customization | CLI Parameter | Description | Value | Default setting |
| ------------- | --------- | ----------- | --------| ------------- |             
| Node Feature Discovery deletion policy | `nfdDeletePolicy` |  Retain or delete the operator if the OpenShift AI add-on is removed. | `Retain` (default) or `Delete` | `Retain` |                               
| NVIDIA GPU Operator deletion policy | `nvidiaDeletePolicy` | Retain or delete the operator if the OpenShift AI add-on is removed. | `Retain` (default) or `Delete` | `Retain` |   
| NVIDIA CUDA post-installation testing | `nvidiaCudaTest` | Enable NVIDIA CUDA testing.  |`true` (enabled, default) \n `false` (disabled) | `false` (disabled) |   
| Pipeline Operator deletion policy| `pipelineDeletePolicy` | Retain or delete the operator if the OpenShift AI add-on is removed. | | `Retain` (default) or `Delete` | `Retain` |            
{: caption="OpenShift AI add-on customizations options for additional operators. These settings can be changed during installation in the CLI or UI." caption-side="bottom"}

The following NVIDIA GPU operators apply with the default settings. You can only change these settings during installation if you install the add-on with the CLI. After installation, you can change these settings, in either the UI or the CLI, by editing the ClusterPolicy. 

| Customization | CLI Parameter | Description |  CLI values | UI default setting | 
| ------------- | --------- | ----------- | --------| ------------- |   
| NVIDIA Sandbox Workloads | `nvidiaSandboxWorkloads` | Enable management of additional operands required for sandbox workloads. | `true` (enabled, default) \n  `false` (disabled) | `Enabled` |  
| NVIDIA vGPU Manager | `nvidiaVgpuManagerEnabled` | Enable NVIDIA vGPU Manager. | `true` (enabled, default) \n `false` (disabled) | `Enabled` |   
| NVIDIA GPUDirect Storage | `nvidiaGpuDirectStorageEnabled` | Enable GPUDirect Storage. | `true` (enabled, default) \n `false` (disabled) | `Enabled` |
| NVIDIA Node Status Exporter | `nvidiaNodeStatusExporterEnabled` | Enable Node Status Exporter. | `true` (enabled, default) \n `false` (disabled) | `Enabled` |
| NVIDIA Virtual Function I/O Manager | `nvidiaVfioManagerEnabled` | Enable VFIO Manager for configuration to deploy VFIO-PCI. | `true` (enabled, default) \n `false` (disabled) | `Enabled` |   
| NVIDIA Sandbox Device Plug-in | `nvidiaSandboxDevicePluginEnabled` | Enable NVIDIA Sandbox Device Plug-in. | `true` (enabled, default) \n `false` (disabled) | `Enabled` |
| NVIDA Multi Instance GPU Manager| `nvidiaMigManagerEnabled` |  Enable NVIDIA Multi Instance GPU Manager. | `true` (enabled, default) \n `false` (disabled) | `Enabled` |   
| NVIDIA Data Center GPU Manager Hostengine Deployment | `nvidiaDcgmEnabled` | Enable deployment of the NVIDIA Data Center GPU Manager Hostengine as a separate pod. | `true` (enabled, default) \n `false` (disabled) | `Enabled` |  
| NVIDIA vGPU Device Manager| `nvidiaVgpuDeviceManagerEnabled` | Enable NVIDIA vGPU Device Manager. | `true` (enabled, default) \n `false` (disabled) | `Enabled` |
{: caption="OpenShift AI add-on customizations options for additional operators. These settings can be changed during installation in the CLI only." caption-side="bottom"}

## What's next?
{: #ai-addon-install-next}

- Try out a [tutorial for using OpenShift AI for fraud detection](https://docs.redhat.com/en/documentation/red_hat_openshift_ai_self-managed/2.22/html/openshift_ai_tutorial_-_fraud_detection_example/index){: external}
- See information on [managing the OpenShift AI add-on](/docs/openshift?topic=openshift-ai-addon-manage).
- Make sure you understand the [update process](/docs/openshift?topic=openshift-ai-addon-manage#ai-addon-update) for the OpenShift AI add-on.
