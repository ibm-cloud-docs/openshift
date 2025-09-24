---

copyright: 
  years: 2024, 2025
lastupdated: "2025-09-24"


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

## Considerations
{: #ai-consideration}

- To use all the capabilities provided by OpenShift AI, at least 1 GPU is recommended.
- Your cluster can have a mix of GPU and non-GPU nodes. However, if you use this configuration, make sure to deploy your app on a GPU node to leverage its resources.
- Beginning with version 2.19.0 of OpenShift AI Operator, KServe is available in either Advanced or Standard mode. By default, when you install KServe using the OpenShift AI using the IBM Cloud add-on, it is installed in Standard mode. If you want to use Advanced mode, you must complete the [optional steps](#ai-install-kserve) after installing the add-on.


## Before you begin
{: #ai-before}

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


## Step 1: Choose customization options 
{: #ai-custom-step}
{: cli}

You can enhance your Red Hat OpenShift AI projects by specifying different options to include with your add-on installation, such as data pipelines for building portable machine learning workflows or tools for managing and scaling your resources. You can also customize upgrade policies and deletion policies. 

Run the command to list all options. For descriptions of each available option, see [OpenShift AI customization options](#custom-options). If you do not include a specific option when you install the add-on, the default value applies. 

```sh
ibmcloud oc cluster addon options --addon openshift-ai
```
{: pre}

## Step 2: Review the recommended operators
{: #ai-ops-rec-cli}
{: cli}

You can choose to also install additional operators that are recommended for the use of certain OpenShift AI features. If they are not already installed on your cluster, you can choose to include them in the add-on installation. Or, you can install them at anytime by using OperatorHub or by following the operator-specific installation steps. To use these operators, you must [disable outbound traffic protection](/docs/openshift?topic=openshift-sbd-allow-outbound) for your cluster. 

You are responsible for managing these operators, including but not limited to updating, monitoring, recovery, and re-installation.
{: important}

The following operators are recommended. 
- [OpenShift Pipelines](https://docs.redhat.com/documentation/red_hat_openshift_pipelines/1.16/html/about_openshift_pipelines/index){: external}
    - [Installing OpenShift Pipelines](https://docs.redhat.com/documentation/red_hat_openshift_pipelines/1.16/html/installing_and_configuring/installing-pipelines){: external}
- [Node Feature Discovery](https://docs.redhat.com/documentation/openshift_container_platform/4.16/html/specialized_hardware_and_driver_enablement/psap-node-feature-discovery-operator){: external}
    - [Installing the Node Feature Discovery Operator](https://docs.redhat.com/documentation/openshift_container_platform/4.16/html/specialized_hardware_and_driver_enablement/psap-node-feature-discovery-operator#installing-the-node-feature-discovery-operator_psap-node-feature-discovery-operator){: external}
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

## Step 1: Review the recommended operators
{: #ai-ops-rec}
{: ui}

You can choose to also install additional operators that are recommended for the use of certain OpenShift AI features. If they are not already installed on your cluster, you can choose to include them in the add-on installation. Or, you can install them at anytime by using OperatorHub or by following the operator-specific installation steps. To use these operators, you must [disable outbound traffic protection](/docs/openshift?topic=openshift-sbd-allow-outbound) for your cluster. 

You are responsible for managing these operators, including but not limited to updating, monitoring, recovery, and re-installation.
{: important}

The following operators are recommended. 
- [OpenShift Pipelines](https://docs.redhat.com/documentation/red_hat_openshift_pipelines/1.16/html/about_openshift_pipelines/index){: external}
    - [Installing OpenShift Pipelines](https://docs.redhat.com/documentation/red_hat_openshift_pipelines/1.16/html/installing_and_configuring/installing-pipelines){: external}
- [Node Feature Discovery](https://docs.redhat.com/documentation/openshift_container_platform/4.16/html/specialized_hardware_and_driver_enablement/psap-node-feature-discovery-operator){: external}
    - [Installing the Node Feature Discovery Operator](https://docs.redhat.com/documentation/openshift_container_platform/4.16/html/specialized_hardware_and_driver_enablement/psap-node-feature-discovery-operator#installing-the-node-feature-discovery-operator_psap-node-feature-discovery-operator){: external}
- [NVIDIA GPU Operator](https://docs.nvidia.com/datacenter/cloud-native/gpu-operator/latest/index.html){: external}
    - [Installing the NVIDIA GPU Operator](https://docs.nvidia.com/datacenter/cloud-native/gpu-operator/latest/getting-started.html){: external}


Some of these operators might include additional customizations that you can choose to specify when you install the add-on. Review the list of [customizations available for the recommended operators](/docs/openshift?topic=openshift-ai-addon-install&interface=cli#ai-ops-rec-cli).

## Step 2: Install the add-on in the UI
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

Review the customization options available for the OpenShift AI add-on.

To include an option when you [install the OpenShift AI add-on with the CLI](/docs/openshift?topic=openshift-ai-addon-install&interface=cli#ai-install-cli), include the option with the `--parameter PARAM=VALUE` format when you run the `ibmcloud oc cluster addon enable openshift-ai`. For example, to install the add-on with the Data Science Pipelines option, specify `--parameter oaiDataSciencePipelines=Managed`.
{: cli}

To include an option when you [install the OpenShift AI add-on with the UI](/docs/openshift?topic=openshift-ai-addon-install&interface=ui#ai-install-ui), click to enable the option when prompted. 
{: ui}

| Customization | CLI Parameter | Description | CLI Values | Default value |
| ------------- | --------- | ----------- | ------ | ------------- |
| OpenShift AI approval policy | `oaiInstallPlanApproval` | Apply minor and patch updates automatically or manually. | `Automatic` or `Manual` |  `Automatic` |                   
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


## Customizations for recommended operators
{: #rec-ops-custom}

Review the [recommended operators](/docs/openshift?topic=openshift-ai-addon-install&interface=ui#ai-ops-rec) and the optional customizations you can include during installation. 

To include a customization for an operator when you [install the OpenShift AI add-on with the CLI](/docs/openshift?topic=openshift-ai-addon-install&interface=cli#ai-install-cli), include the option with the `--parameter PARAM=VALUE` format when you run the `ibmcloud oc cluster addon enable openshift-ai`. For example, to include the NVIDIA GPUDirect Storage customization for the NVIDIA operator, specify `--parameter nvidiaGpuDirectStorageEnabled=true`.
{: cli}

To include a customization for an operator when you [install the OpenShift AI add-on with the UI](/docs/openshift?topic=openshift-ai-addon-install&interface=ui#ai-install-ui), click to enable the option when prompted. 
{: ui}

| Customization | CLI Parameter | Description |  CLI Values | Default value |
| ------------- | --------- | ----------- | --------| ------------- |             
| NFD Deletion Policy | `nfdDeletePolicy` |  Retain or delete the operator if the OpenShift AI add-on is removed. | `Retain` or `Delete` | `Retain` |                               
| NVIDIA Deletion Policy | `nvidiaDeletePolicy` | Retain or delete the operator if the OpenShift AI add-on is removed. | `Retain` or `Delete` | `Retain` |                   
| NVIDIA Sandbox Workloads | `nvidiaSandboxWorkloads` | Enable management of additional operands required for sandbox workloads. | `true` (enabled) \n  `false` (disabled) | `true` (enabled) |             
| NVIDIA DCGM Hostengine Deployment | `nvidiaDcgmEnabled` | Enable deployment of the NVIDIA DCGM Hostengine as a separate pod. | `true` (enabled) \n `false` (disabled) | `true` (enabled) |                
| NVIDIA vGPU Manager | `nvidiaVgpuManagerEnabled` | Enable NVIDIA vGPU Manager. | `true` (enabled) \n `false` (disabled) | `true` (enabled) |         
| NVIDIA VFIO Manager | `nvidiaVfioManagerEnabled` | Enable VFIO Manager for configuration to deploy VFIO-PCI. | `true` (enabled) \n `false` (disabled) | `true` (enabled) |        
| NVIDIA Node Status Exporter | `nvidiaNodeStatusExporterEnabled` | Enable Node Status Exporter. | `true` (enabled) \n `false` (disabled) | `true` (enabled) |  
| NVIDIA Sandbox Device Plug-in | `nvidiaSandboxDevicePluginEnabled` | Enable NVIDIA Sandbox Device Plug-in. | `true` (enabled) \n `false` (disabled) | `true` (enabled) |
| NVIDA MIG Manager| `nvidiaMigManagerEnabled` |  Enable NVIDIA MIG Manager. | `true` (enabled) \n `false` (disabled) | `true` (enabled) |         
| NVIDIA vGPU Device Manager| `nvidiaVgpuDeviceManagerEnabled` | Enable NVIDIA vGPU Device Manager. | `true` (enabled) \n `false` (disabled) | `true` (enabled) | 
| NVIDIA GPUDirect Storage | `nvidiaGpuDirectStorageEnabled` | Enable GPUDirect Storage. | `true` (enabled) \n `false` (disabled) | `true` (enabled) |
| NVIDIA CUDA Testing | `nvidiaCudaTest` | Enable NVIDIA CUDA testing.  |`true` (enabled) \n `false` (disabled) | `false` (disabled) |   
| Pipeline Operator Deletion Policy| `pipelineDeletePolicy` | Retain or delete the operator if the OpenShift AI add-on is removed. | | `Retain` or `Delete` | `Retain` |            
{: caption="OpenShift AI add-on customizations options and CLI parameters for additional operators." caption-side="bottom"}


## What's next?
{: #ai-addon-install-next}

- See information on [managing the OpenShift AI add-on](/docs/openshift?topic=openshift-ai-addon-manage).
- Make sure you understand the [update process](/docs/openshift?topic=openshift-ai-addon-manage#ai-addon-update) for the OpenShift AI add-on.
