---

copyright: 
  years: 2014, 2024
lastupdated: "2024-01-03"


keywords: openshift, continuous integration and delivery

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}


# Continuous integration and delivery for app development and deployment
{: #cicd}

With {{site.data.keyword.cloud_notm}} and other open source tools, you can set up continuous integration and delivery (CI/CD), version control, tool chains, and more to help automate app development and deployment.
{: shortdesc}

Continuous integration (CI) can help you detect errors early, ensure early system integration, and improve collaboration in your development process. Continuous delivery (CD) is a practice by which you build and deploy your software so that it can be released into production at any time. By automating your continuous integration and delivery processes through setting up CI/CD pipelines, you can achieve repeatability in code releases and greater predictability in delivery schedules.

Adopt a DevOps approach by using {{site.data.keyword.deliverypipelinelong}}, which includes open toolchains that automate the building and deployment of containerized apps.  

## Before you begin
{: #cicd_before}

Before you begin, make sure that you have at least the following permissions in {{site.data.keyword.cloud_notm}} IAM.

- **Editor** platform access role and **Writer** service access role to the **Kubernetes Service** cluster. For more information, see [User access permissions](/docs/openshift?topic=openshift-access_reference).
- **Viewer** platform access role to the resource group of the cluster where you want to create the toolchain.
- **Editor** platform access role to the **Toolchain** service (note that this service is separate than **Continuous Delivery**).

## Creating a toolchain with Delivery Pipeline
{: #cicd_toolchain}

Follow these steps to create a CI/CD pipeline with a toolchain. A toolchain is a set of tool integrations that support development, deployment, and operations tasks. When configuring the toolchain you can include and configure a Delivery Pipeline that is automatically created and triggered after the toolchain is created.

1. From the [{{site.data.keyword.redhat_openshift_notm}} clusters console](https://cloud.ibm.com/kubernetes/clusters?platformType=openshift){: external}, select the cluster for which you want to set up a continuous delivery pipeline.
2. Select the **DevOps** tab.
3. Click **Create a toolchain**.
4. Review the available toolchains. IBM provides pre-defined toolchains that you can use to deploy, test, and monitor Kubernetes-native apps or Helm charts. You can expand each toolchain to find an overview of the tools that are set up for you and to find the scripts in GitHub that are used to configure the toolchain in your cluster. If you know what tools you want to use, you can create your own toolchain.
5. Select the toolchain that you want to use and click **Create**.
6. Follow the directions in the console to configure your toolchain. Make sure to include the name of your cluster in your toolchain name so that you can easily find the toolchain that is associated with your cluster later. For more information, see [Creating toolchains](/docs/ContinuousDelivery?topic=ContinuousDelivery-toolchains_getting_started).
7. Select **Delivery Pipeline** to review the stages of your continuous integration and continuous delivery pipeline. After you create your toolchain, your pipeline is automatically kicked off and runs through the stages that you configured. Make sure that your stages run successfully and correct any errors.
8. Modify your toolchain. You can add more tools to your toolchain or change the stages of your delivery pipeline.
    1. From the [{{site.data.keyword.redhat_openshift_notm}} clusters console](https://cloud.ibm.com/kubernetes/clusters?platformType=openshift){: external}, select the cluster for which you want to set up a continuous delivery pipeline.
    2. Select the **DevOps** tab.
    3. Select the toolchain that you want to modify.



For a deep dive into the benefits and specifics of automating continuous integration and delivery, check out [Automate continuous integration](https://www.ibm.com/garage/method/practices/code/practice_continuous_integration){: external} and [Build and deploy by using continuous delivery](https://www.ibm.com/garage/method/practices/deliver/practice_continuous_delivery){: external} in the IBM Garage Methodology documentation.
{: tip}


## Other resources for automating your pipeline
{: #cicd-other}

Check out the following integrations and tools that you can use to automate your CI/CD pipeline. 

Codeship
:   You can use [Codeship](https://www.cloudbees.com/products/codeship){: external} for the continuous integration and delivery of containers. For more information, see [Using Codeship Pro To Deploy Workloads to {{site.data.keyword.containerlong_notm}}](https://www.ibm.com/cloud/blog/using-codeship-pro-deploy-workloads-ibm-container-service){: external}.

Grafeas
:   [Grafeas](https://grafeas.io){: external} is an open source CI/CD service that provides a common way for how to retrieve, store, and exchange metadata during the software supply chain process. For example, if you integrate Grafeas into your app build process, Grafeas can store information about the initiator of the build request, vulnerability scan results, and quality assurance sign-off so that you can make an informed decision if an app can be deployed to production. You can use this metadata in audits or to prove compliance for your software supply chain.

{{site.data.keyword.deliverypipelinelong}}
:   With your app configuration files organized in a source control management system such as Git, you can build your pipeline to test and deploy code to different environments, such as `test` and `prod`. {{site.data.keyword.contdelivery_full}} allows you to automate your app builds and container deployments to Kubernetes clusters by using a toolchain. You can also check out [this tutorial on Continuous Deployment to Kubernetes](/docs/solution-tutorials?topic=solution-tutorials-continuous-deployment-to-kubernetes#continuous-deployment-to-kubernetes).

Razee
:   [Razee](https://razee.io/){: external} is an open-source project that automates and manages the deployment of Kubernetes resources across clusters, environments, and cloud providers, and helps you to visualize deployment information for your resources so that you can monitor the rollout process and find deployment issues more quickly. For more information about Razee and how to set up Razee in your cluster to automate your deployment process, see the [Razee documentation](https://github.com/razee-io/Razee){: external}.



Kustomize
:   Use the Kubernetes project [Kustomize](https://github.com/kubernetes-sigs/kustomize){: external} to package your apps by both standardizing and customizing your deployments across multiple environments. Kustomize helps you write, customize, and reuse your Kubernetes resource YAML configurations. To get started, see [Packaging apps for reuse in multiple environments with Kustomize](/docs/openshift?topic=openshift-kustomize).
    
Operators
:   With operators, you can manage the lifecycle of the apps in your cluster, including third-party software and services that you integrate into your cluster from the [OperatorHub](https://operatorhub.io/){: external}. You can consistently install, update, and monitor system components by using operators or by making operators available to developers that work in specific projects or across projects. To set up operators, see [Using Operators in version 4 clusters](/docs/openshift?topic=openshift-operators#operators_4).

