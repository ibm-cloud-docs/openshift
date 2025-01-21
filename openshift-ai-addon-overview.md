---
copyright: 
  years: 2024, 2025
lastupdated: "2025-01-21"


keywords: openshift, {{site.data.keyword.openshiftlong_notm}}, ai, add-on

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}

# About the Red Hat OpenShift AI add-on
{: #ai-addon-about}

Use the OpenShift AI add-on to quickly deploy OpenShift AI in {{site.data.keyword.openshiftshort}}.

Red Hat OpenShift AI is a flexible, scalable artificial intelligence and machine learning platform that enables enterprises to create and deliver AI-enabled applications at scale across hybrid cloud environments. OpenShift AI enables data acquisition and preparation, model training and fine-tuning, model serving and model monitoring, and hardware acceleration. For more information on the features and benefits of OpenShift AI, see [What is Red Hat OpenShift AI?](https://www.redhat.com/en/technologies/cloud-computing/openshift/openshift-ai){: external}.


## What gets deployed when I install the OpenShift AI add-on?
{: #ai-addon-deployed}

Installing the add-on deploys the OpenShift AI operator, which is managed by IBM. You can choose to also install additional operators that are recommended for the use of certain OpenShift AI features, but are not managed by IBM. 

To avoid disruptions to your workload, make sure you understand [your responsibilities for managing and maintaining](#ai-addon-responsibility) the operators used for the OpenShift AI add-on. The OpenShift AI operator is managed by IBM, however any additional operators that you chose to include in the installation are not managed by IBM. You are responsible for managing and maintaining these additional operators.
{: important}

These following operators are recommended for the OpenShift AI add-on. If they are not already installed on your cluster, you can choose to include them in the add-on installation. Or, you can install them at anytime by using OperatorHub or by following the operator-specific installation steps. 

- [OpenShift Pipelines](https://docs.openshift.com/pipelines/1.16/about/about-pipelines.html){: external}
  - [Installing OpenShift Pipelines](https://docs.openshift.com/pipelines/1.16/install_config/installing-pipelines.html){: external}
- [Node Feature Discovery](https://docs.openshift.com/container-platform/4.16/hardware_enablement/psap-node-feature-discovery-operator.html){: external}
  - [Installing the Node Feature Discovery Operator](https://docs.openshift.com/container-platform/4.16/hardware_enablement/psap-node-feature-discovery-operator.html#installing-the-node-feature-discovery-operator_psap-node-feature-discovery-operator){: external}
- [NVIDIA GPU Operator](https://docs.nvidia.com/datacenter/cloud-native/gpu-operator/latest/index.html){: external}
  - [Installing the NVIDIA GPU Operator](https://docs.nvidia.com/datacenter/cloud-native/gpu-operator/latest/getting-started.html){: external}


## Who is responsible for managing the OpenShift AI add-on components and required operators?
{: #ai-addon-responsibility}

To avoid disruptions to your workload, it's important to understand your responsibilities for managing and maintaining the operators used for the OpenShift AI add-on.

### OpenShift AI operator
{: #responsible-IBM}

The OpenShift AI operator is managed and maintained by IBM and receives updates directly from the add-on. This means you receive a notification from IBM when an update becomes available and that IBM also provides a change log for these updates. This is the only installed operator that is managed by IBM.

IBM's responsibilities
:   - Providing security updates and notifications when updates are available. 
:   - Providing change log for updates, including CVEs and a description of changes included.
:   - Removing the operator when you uninstall the add-on. 

Your responsibilities
:   - Reviewing and understanding the changes included in each update.
:   - Depending on the update approval policy setting you specify when you install the add-on, you might need to manually approve the changes for the update to apply. For more information, see [How are OpenShift AI addon-on components updated?](#ai-addon-updatehow).

### Additional operators
{: #responsible-customer}

The OpenShift AI operator is the only installed operator that is managed by IBM. All additional operators used for the add-on are unmanaged, meaning that you are responsible for managing and maintaining these operators. IBM does not provide notifications when updates are available for these operators. 

If you already have these operators installed on your cluster before you install the OpenShift AI add-on, you can continue using your current management and updating strategy. 

IBM's responsibilities
:   - IBM is not responsible for managing, maintaining, or updating these additional operators. 

Your responsibilities
:   - Maintaining the health and functioning of each operator, including but not limited to updating, monitoring, recovery, and re-installation.
:   - Knowing when updates are available for each operator, what changes are included, and applying the updates. 
:   - Removing the operator when you uninstall the add-on. 


## How are OpenShift AI add-on components updated?
{: #ai-addon-updatehow}

Each operator used by the OpenShift AI add-on must be updated individually. The update process depends on whether the operator is managed by IBM or not managed by IBM. 

### Updating the OpenShift AI operator
{: #ai-addon-updatehow-managed}

The OpenShift AI operator is managed by IBM. Therefore IBM notifies you when updates are available for the operator and provides a change log. Updates for the OpenShift AI operator typically follow the same schedule of updates for the Red Hat OpenShift AI platform, so that if the OpenShift AI Platform releases a major, minor, or patch update, a corresponding update is made available for the operator. 

Depending on the approval policy you specify when you first install the add-on, you might need to review and approve the update plan before the update can be applied. 
If you specify the `Manual` approval policy, then you must manually approve most update plans. If you specify the `Automatic` approval policy, then you do not need to review any updates. In the case of minor or patch updates, only certain parts of the update might need to be reviewed. Additionally, the type of update determines how the update is applied. Major updates require you to run a command, but minor and patch updates are applied automatically (after you manually approve the plan, if required). For more detailed explanation, see [Updating the IBM-managed OpenShift AI operator](/docs/openshift?topic=openshift-ai-addon-manage#ai-addon-update). 

Version rollbacks are not supported. You cannot undo an update to the OpenShift AI operator. Take this into consideration and make sure you choose your update strategy carefully, especially if you choose the `Automatic` approval policy. 
{: important}

### Updating operators not managed by IBM
{: #ai-addon-updatehow-notmanaged}

You are responsible for updating all operators that are not managed by IBM. IBM does not notify you of available updates or provide support related to updates for these operators. Refer to the provider documentation for information on keeping these operators up to date. 


## What's next?
{: #ai-addon-ov-next}

Follow the steps to [install the OpenShift AI add-on](/docs/openshift?topic=openshift-ai-addon-install) using the CLI or UI. 


