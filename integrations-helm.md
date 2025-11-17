---

copyright: 
  years: 2014, 2025
lastupdated: "2025-11-17"


keywords: kubernetes, openshift

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}





# Adding services by using Helm charts
{: #helm}

You can add complex {{site.data.keyword.redhat_openshift_notm}} apps to your cluster by using Helm charts.
{: shortdesc}

In {{site.data.keyword.redhat_openshift_notm}} clusters that run version 4, use [Operators](/docs/openshift?topic=openshift-operators) instead of Helm charts. If you have custom Helm charts, you can create a [Helm-based Operator](https://docs.redhat.com/en/documentation/openshift_container_platform/4.7/html/operators/developing-operators){: external} instead.
{: tip}

## About Helm in {{site.data.keyword.openshiftlong_notm}}
{: #about-helm}

### What is Helm and how do I use it?
{: #what-is-helm}

[Helm](https://helm.sh){: external} is a Kubernetes package manager that uses Helm charts to define, install, and upgrade complex Kubernetes apps in your cluster. Helm charts package the specifications to generate YAML files for Kubernetes resources that build your app. These Kubernetes resources are automatically applied in your cluster and assigned a version by Helm. You can also use Helm to specify and package your own app and let Helm generate the YAML files for your Kubernetes resources.

### What Helm charts are supported in {{site.data.keyword.openshiftlong_notm}}?
{: #supported-charts}

For an overview of available Helm charts, see the [Helm charts catalog](https://cloud.ibm.com/kubernetes/helm){: external}.


## Installing Helm v3 in your cluster
{: #install_v3}

Set up Helm v3 and the {{site.data.keyword.cloud_notm}} Helm repositories in your cluster.
{: shortdesc}

Before you begin: [Log in to your account. If applicable, target the appropriate resource group. Set the context for your cluster.](/docs/containers?topic=containers-access_cluster)

1. Install the latest release of the version 3 [Helm CLI](https://github.com/helm/helm/releases){: external} on your local machine.

2. Add the {{site.data.keyword.cloud_notm}} Helm repositories to your Helm instance.

    If you enabled [VRF](/docs/account?topic=account-vrf-service-endpoint&interface=ui) and [service endpoints](/docs/account?topic=account-vrf-service-endpoint#service-endpoint) in your {{site.data.keyword.cloud_notm}} account, you can use the private {{site.data.keyword.cloud_notm}} Helm repository to keep your image pull traffic on the private network. If you can't enable VRF or service endpoints in your account, use the public registry domain: `helm repo add iks-charts https://icr.io/helm/iks-charts`.
    {: note}

    ```sh
    helm repo add iks-charts https://private.icr.io/helm/iks-charts
    ```
    {: pre}

3. Update the repos to retrieve the latest versions of all Helm charts.
    ```sh
    helm repo update
    ```
    {: pre}

4. List the Helm charts that are currently available in the {{site.data.keyword.cloud_notm}} repositories.
    ```sh
    helm search repo iks-charts
    ```
    {: pre}

    ```sh
    helm search repo ibm-charts
    ```
    {: pre}

    ```sh
    helm search repo ibm-community
    ```
    {: pre}

    ```sh
    helm search repo entitled
    ```
    {: pre}

    ```sh
    helm search repo ibm-helm
    ```
    {: pre}

5. Identify the Helm chart that you want to install and follow the instructions in the Helm chart `README` to install the Helm chart in your cluster.
