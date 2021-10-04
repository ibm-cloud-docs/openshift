---

copyright: 
  years: 2014, 2021
lastupdated: "2021-10-04"

keywords: kubernetes, openshift, roks, rhoks, rhos

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}



# Adding services by using Helm charts
{: #helm}

You can add complex {{site.data.keyword.openshiftshort}} apps to your cluster by using Helm charts.
{: shortdesc}

In {{site.data.keyword.openshiftshort}} clusters that run version 4, use [Operators](/docs/openshift?topic=openshift-operators) instead of Helm charts. If you have custom Helm charts, you can create a [Helm-based Operator ![External link icon](../icons/launch-glyph.svg "External link icon")](https://docs.openshift.com/container-platform/4.7/operators/operator_sdk/) instead.
{: tip}

## About Helm in {{site.data.keyword.openshiftlong_notm}}
{: #about-helm}

### What is Helm and how do I use it?
{: #what-is-helm}

[Helm](https://helm.sh){: external} is a Kubernetes package manager that uses Helm charts to define, install, and upgrade complex Kubernetes apps in your cluster. Helm charts package the specifications to generate YAML files for Kubernetes resources that build your app. These Kubernetes resources are automatically applied in your cluster and assigned a version by Helm. You can also use Helm to specify and package your own app and let Helm generate the YAML files for your Kubernetes resources.

### What Helm charts are supported in {{site.data.keyword.openshiftlong_notm}}?
{: #supported-charts}

For an overview of available Helm charts, see the [Helm charts catalog](https://cloud.ibm.com/kubernetes/helm){: external}. The Helm charts that are listed in this catalog are grouped as follows:

- **iks-charts**: Helm charts that are approved for {{site.data.keyword.openshiftlong_notm}}. The name of this repo was changed from `ibm` to `iks-charts`.
- **ibm-charts**: Helm charts that are approved for {{site.data.keyword.openshiftlong_notm}} and {{site.data.keyword.cloud_notm}} Private clusters.
- **ibm-community**: Helm charts that originated outside IBM, such as from [{{site.data.keyword.openshiftlong_notm}} partners](/docs/containers?topic=containers-service-partners). These charts are supported and maintained by the community partners.
- **kubernetes**: Helm charts that are provided by the Kubernetes community and considered `stable` by the community governance. These charts are not verified to work in {{site.data.keyword.openshiftlong_notm}} or {{site.data.keyword.cloud_notm}} Private clusters.
- **kubernetes-incubator**: Helm charts that are provided by the Kubernetes community and considered `incubator` by the community governance. These charts are not verified to work in {{site.data.keyword.openshiftlong_notm}} or {{site.data.keyword.cloud_notm}} Private clusters.
- **entitled**: Helm charts of licensed software that you must purchase and for which you must set up cluster access with an entitlement key. For more information, see [Setting up a cluster to pull entitled software](/docs/containers?topic=containers-registry#secret_entitled_software).

Helm charts from the **iks-charts**, **ibm-charts**, and, if licensed, **entitled** repositories are fully integrated into the {{site.data.keyword.cloud_notm}} support organization. If you have a question or an issue with using these Helm charts, you can use one of the {{site.data.keyword.openshiftlong_notm}} support channels. For more information, see [Getting help and support](/docs/containers?topic=containers-get-help). [Install the latest release of Helm v3](#install_v3).



## Installing Helm v3 in your cluster
{: #install_v3}

Set up Helm v3 and the {{site.data.keyword.cloud_notm}} Helm repositories in your cluster.
{: shortdesc}

Before you begin: [Log in to your account. If applicable, target the appropriate resource group. Set the context for your cluster.](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure)

1. Install the latest release of the version 3 [Helm CLI](https://github.com/helm/helm/releases){: external} on your local machine.

2. Add the {{site.data.keyword.cloud_notm}} Helm repositories to your Helm instance.

    If you enabled [VRF](/docs/account?topic=account-vrf-service-endpoint#vrf) and [service endpoints](/docs/account?topic=account-vrf-service-endpoint#service-endpoint) in your {{site.data.keyword.cloud_notm}} account, you can use the private {{site.data.keyword.cloud_notm}} Helm repository to keep your image pull traffic on the private network. If you cannot enable VRF or service endpoints in your account, use the public registry domain: `helm repo add iks-charts https://icr.io/helm/iks-charts`.
    {: note}

    ```sh
    helm repo add iks-charts https://private.icr.io/helm/iks-charts
    ```
    {: pre}

    ```sh
    helm repo add ibm-charts https://raw.githubusercontent.com/IBM/charts/master/repo/stable
    ```
    {: pre}

    ```sh
    helm repo add ibm-community https://raw.githubusercontent.com/IBM/charts/master/repo/community
    ```
    {: pre}

    ```sh
    helm repo add entitled https://raw.githubusercontent.com/IBM/charts/master/repo/entitled
    ```
    {: pre}

    ```sh
    helm repo add ibm-helm https://raw.githubusercontent.com/IBM/charts/master/repo/ibm-helm
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




