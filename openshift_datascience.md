---

copyright:
  years: 2023, 2024
lastupdated: "2024-02-23"


keywords: data science, AI, machine learning, AI modeling, modeling, GPUs, NVIDIA, node feature discovery, pipelines

subcollection: openshift

content-type: tutorial
services: openshift
account-plan: paid
completion-time: 60m

---

{{site.data.keyword.attribute-definition-list}}

# Installing Red Hat OpenShift AI
{: #datascience}
{: toc-content-type="tutorial"}
{: toc-services="openshift"}
{: toc-completion-time="60m"}

Red Hat OpenShift AI is an open hybrid AI and machine learning platform for gathering insights from data and building AI-enabled applications. It provides tools to rapidly develop, train, serve, and monitor machine learning models on site, in the public cloud, or at the edge. You can install Red Hat OpenShift AI and other necessary operators onto an existing Red Hat OpenShift cluster that is enabled with GPU-enhanced worker nodes. 
{: shortdesc}

The following steps refer to the Red Hat documentation. For more information see, [Installing OpenShift AI self-managed](https://access.redhat.com/documentation/en-us/red_hat_openshift_ai_self-managed/2-latest#installing-openshift-data-science-on-openshift-container-platform_install){: external}.
{: note}

## Before you begin
{: #datascience_before}


1. [Request access](/docs/openshift?topic=openshift-allowlist-request) to GPU worker nodes on VPC clusters, which are currently behind an allowlist. 

2. [Create a Red Hat OpenShift VPC cluster](/docs/openshift?topic=openshift-cluster-create-vpc-gen2&interface=ui) that runs on [bare metal GPU worker nodes](/docs/openshift?topic=openshift-planning_worker_nodes#bm) and has a public cloud service endpoint. If you choose to use a private cloud service endpoint, make sure you configure your cluster so that you can access the OpenShift web console. 

3. Make sure you can [access the your cluster through the OpenShift web console](/docs/openshift?topic=openshift-access_cluster#access_oc_console). 


## Optional. Install the Red Hat OpenShift Pipelines Operator
{: #datascience_pipelines}
{: step}

OpenShift AI supports data science pipelines. A pipeline is a collection of task resources that are arranged in a specific order of execution. By using Red Hat OpenShift AI with pipelines, you can standardize and automate the build and deployment of your data science models. For installation steps, see [Installing OpenShift Pipelines](https://docs.openshift.com/pipelines/1.12/install_config/installing-pipelines.html){: external} in the Red Hat documentation. 

## Install the OpenShift AI Operator
{: #datascience_install}
{: step}

You can install the OpenShift AI Operator to your cluster using the web console. See [Installing OpenShift AI self-managed](https://access.redhat.com/documentation/en-us/red_hat_openshift_ai_self-managed/2-latest#installing-openshift-data-science-on-openshift-container-platform_install){: external} for detailed installation steps and requirements.


## Install the Node Feature Discovery Operator
{: #datascience_node_feature_discovery}
{: step}

The Node Feature Discovery (NFD) Operator is a prerequisite for the NVIDIA GPU Operator, which is required to enable and use GPUs with OpenShift AI. Follow the steps in [Installing the Node Feature Discovery (NFD) Operator](https://docs.nvidia.com/datacenter/cloud-native/openshift/23.6.1/install-nfd.html){: external} in the NVIDIA documentation to install the operator using the Red Hat OperatorHub catalog in the OpenShift Container Platform web console. Make sure you follow all the instructions, including the step to create a Node Feature Discovery instance and the steps to verify the installation. 


## Install the NVIDIA GPU Operator
{: #datascience_nvidia_gpu}
{: step}

To ensure that your data scientists can use compute-heavy workloads in their models, you can enable graphics processing units (GPUs) in OpenShift AI. To enable GPUs on OpenShift, you must install the NVIDIA GPU Operator on the cluster. For installation steps, see [Installing the NVIDIA GPU Operator](https://docs.nvidia.com/datacenter/cloud-native/openshift/23.6.1/install-gpu-ocp.html#installing-the-nvidia-gpu-operator) in the NVIDIA documentation. Note that the [Node Feature Discovery Operator](#datascience_node_feature_discovery) must be installed before you can install the NVIDIA GPU operator.

To check that the GPU operator installation is successful, you can [run a sample GPU application](https://docs.nvidia.com/datacenter/cloud-native/openshift/23.6.1/install-gpu-ocp.html#running-a-sample-gpu-application){: external}.
{: tip}

## Check installed operators
{: #datascience_check}
{: step}

After you install the operators, check that they are visible in the OpenShift web console. 

1. In the IBM Cloud console, navigate to your clusters page. 
2. Click on the cluster. Then, click **OpenShift web console**.
3. In the side panel, click **Operators** > **Installed operators**.
4. Check that the following operators are installed with a status of `Succeeded`. The **Package Server**, which is automatically installed when the cluster is created, is also listed. 
    - NVIDIA GPU Operator
    - Node Feature Discovery Operator
    - Red Hat OpenShift Pipelines
    - Red Hat OpenShift AI


## What's next?
{: #datascience_next}

Now that you have OpenShift AI installed on your cluster, try one of the [Data Science learning paths](https://developers.redhat.com/learn/openshift-ai){: external}, run a sample AI workload on your cluster by following one of the [Red Hat OpenShift tutorials](https://developers.redhat.com/learn/openshift-ai){: external}, or try this tutorial on using [GPUs and a Jupyter notebook for AI or machine learning modeling](https://developers.redhat.com/learn/openshift-data-science/configure-jupyter-notebook-use-gpus-aiml-modeling){: external}. 








