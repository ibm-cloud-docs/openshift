---

copyright:
  years: 2014, 2020
lastupdated: "2020-02-17"

keywords: kubernetes, openshift, roks, rhoks, rhos

subcollection: openshift

---

{:codeblock: .codeblock}
{:deprecated: .deprecated}
{:download: .download}
{:external: target="_blank" .external}
{:faq: data-hd-content-type='faq'}
{:gif: data-image-type='gif'}
{:help: data-hd-content-type='help'}
{:important: .important}
{:new_window: target="_blank"}
{:note: .note}
{:pre: .pre}
{:preview: .preview}
{:screen: .screen}
{:shortdesc: .shortdesc}
{:support: data-reuse='support'}
{:table: .aria-labeledby="caption"}
{:tip: .tip}
{:troubleshoot: data-hd-content-type='troubleshoot'}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:tsSymptoms: .tsSymptoms}


# Adding services by using Helm charts
{: #helm}

You can add complex OpenShift apps to your cluster by using Helm charts.
{: shortdesc}

In OpenShift clusters that run version 4.3 or later, use [Operators](/docs/openshift?topic=openshift-operators) instead of Helm charts. If you have custom Helm charts, you can create a [Helm-based Operator ![External link icon](../icons/launch-glyph.svg "External link icon")](https://docs.openshift.com/container-platform/4.2/operators/operator_sdk/osdk-helm.html) instead.
{: tip}

## About Helm in Red Hat OpenShift on IBM Cloud
{: #about-helm}

### What is Helm and how do I use it?
{: #what-is-helm}

[Helm](https://helm.sh){: external} is a Kubernetes package manager that uses Helm charts to define, install, and upgrade complex Kubernetes apps in your cluster. Helm charts package the specifications to generate YAML files for Kubernetes resources that build your app. These Kubernetes resources are automatically applied in your cluster and assigned a version by Helm. You can also use Helm to specify and package your own app and let Helm generate the YAML files for your Kubernetes resources.

### What Helm charts are supported in Red Hat OpenShift on IBM Cloud?
{: #supported-charts}

For an overview of available Helm charts, see the [Helm charts catalog](https://cloud.ibm.com/kubernetes/helm){: external}. The Helm charts that are listed in this catalog are grouped as follows:

- **iks-charts**: Helm charts that are approved for Red Hat OpenShift on IBM Cloud. The name of this repo was changed from `ibm` to `iks-charts`.
- **ibm-charts**: Helm charts that are approved for Red Hat OpenShift on IBM Cloud and {{site.data.keyword.cloud_notm}} Private clusters.
- **ibm-community**: Helm charts that originated outside IBM, such as from [Red Hat OpenShift on IBM Cloud partners](/docs/openshift?topic=openshift-service-partners). These charts are supported and maintained by the community partners.
- **kubernetes**: Helm charts that are provided by the Kubernetes community and considered `stable` by the community governance. These charts are not verified to work in Red Hat OpenShift on IBM Cloud or {{site.data.keyword.cloud_notm}} Private clusters.
- **kubernetes-incubator**: Helm charts that are provided by the Kubernetes community and considered `incubator` by the community governance. These charts are not verified to work in Red Hat OpenShift on IBM Cloud or {{site.data.keyword.cloud_notm}} Private clusters.
- **entitled**: Helm charts of licensed software that you must purchase and for which you must set up cluster access with an entitlement key. For more information, see [Setting up a cluster to pull entitled software](/docs/openshift?topic=openshift-registry#secret_entitled_software).

Helm charts from the **iks-charts**, **ibm-charts**, and, if licensed, **entitled** repositories are fully integrated into the {{site.data.keyword.cloud_notm}} support organization. If you have a question or an issue with using these Helm charts, you can use one of the Red Hat OpenShift on IBM Cloud support channels. For more information, see [Getting help and support](/docs/containers?topic=containers-cs_troubleshoot_clusters#clusters_getting_help).

### Do I install Helm v2 or v3?
{: #helm-v2-v3}

[Helm v3 was released on 13 November 2019](https://helm.sh/blog/helm-3-released/){: external}. Helm v3 provides several advantages over Helm v2. For example, the Helm server [Tiller is removed in Helm v3](https://helm.sh/docs/faq/#removal-of-tiller){: external}. You no longer need to set up a Tiller service account or initialize Helm with Tiller. Additionally, [chart release names are now scoped to namespaces](https://helm.sh/docs/faq/#release-names-are-now-scoped-to-the-namespace){: external} so that you can release one version of the same chart across several namespaces.

[Install Helm v2](#install_v2) only if you have specific requirements to use Helm v2 in your cluster. Otherwise, [install the latest release of Helm v3](#install_v3). If you already installed Helm v2 in your cluster, you can [migrate from Helm v2 to v3](#migrate_v3).

<br />


## Installing Helm v3 in your cluster
{: #install_v3}

Set up Helm v3 and the {{site.data.keyword.cloud_notm}} Helm repositories in your cluster.
{: shortdesc}

Before you begin: [Log in to your account. If applicable, target the appropriate resource group. Set the context for your cluster.](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure)

1. Install the latest release of the version 3 [Helm CLI](https://github.com/helm/helm/releases){: external} on your local machine.

2. Add the {{site.data.keyword.cloud_notm}} Helm repositories to your Helm instance.
   ```
   helm repo add iks-charts https://icr.io/helm/iks-charts
   ```
   {: pre}

   ```
   helm repo add ibm-charts https://raw.githubusercontent.com/IBM/charts/master/repo/stable
   ```
   {: pre}

   ```
   helm repo add ibm-community https://raw.githubusercontent.com/IBM/charts/master/repo/community
   ```
   {: pre}

   ```
   helm repo add entitled https://raw.githubusercontent.com/IBM/charts/master/repo/entitled
   ```
   {: pre}

3. Update the repos to retrieve the latest versions of all Helm charts.
   ```
   helm repo update
   ```
   {: pre}

4. List the Helm charts that are currently available in the {{site.data.keyword.cloud_notm}} repositories.
   ```
   helm search repo iks-charts
   ```
   {: pre}

   ```
   helm search repo ibm-charts
   ```
   {: pre}

   ```
   helm search repo ibm-community
   ```
   {: pre}

   ```
   helm search repo entitled
   ```
   {: pre}

5. Identify the Helm chart that you want to install and follow the instructions in the Helm chart `README` to install the Helm chart in your cluster.

<br />


## Migrating from Helm v2 to v3
{: #migrate_v3}

[Helm v3 was released on 13 November 2019](https://helm.sh/blog/helm-3-released/){: external}. In Helm v3, the Helm server Tiller is removed, among many other changes. Continue to use Helm with Tiller only if you have specific requirements to use Helm v2 in your cluster. Otherwise, migrate to Helm v3.
{: shortdesc}

1. Before you migrate, review the [list of changes between v2 and v3](https://helm.sh/docs/topics/v2_v3_migration/){: external} and the [v3 FAQs](https://helm.sh/docs/faq/){: external}.

2. Follow the [Helm v2 to v3 migration steps](https://helm.sh/blog/migrate-from-helm-v2-to-helm-v3/){: external}. These steps include installing the Helm v3 client, backing up Helm v2 data, using the [`helm-2to3` plug-in](https://github.com/helm/helm-2to3){: external} to migrate your Helm v2 configuration and releases, and cleaning up Helm v2 data and the v2 client.

3. Continue with step 2 in [Installing Helm v3 in your cluster](#install_v3) to add the {{site.data.keyword.cloud_notm}} Helm repositories to your Helm instance.

As you work with Helm charts, keep in mind the Helm v3 changes, such as the fact that [chart release names are now scoped to namespaces](https://helm.sh/docs/faq/#release-names-are-now-scoped-to-the-namespace){: external} and that several [Helm CLI commands are renamed](https://helm.sh/docs/faq/#cli-command-renames){: external}.

<br />


## Installing Helm v2 in your cluster
{: #install_v2}

[Helm v3 was released on 13 November 2019](https://helm.sh/blog/helm-3-released/){: external}. Helm v2 requires you to set up the Helm server, Tiller, which is removed in Helm v3. Because Tiller requires a specific service account due to security issues, install Helm v2 only if you have specific requirements to use Helm v2 in your cluster. Otherwise, [install the latest release of Helm v3](#install_v3).
{: note}

### Setting up Helm v2 in a cluster with public access
{: #public_helm_install}

If you have a classic cluster that is connected to a public VLAN, or a VPC cluster with a subnet that is configured with a public gateway, you can install the Helm server Tiller by using the public image in the Google Container Registry.
{: shortdesc}

Before you begin:
- [Log in to your account. If applicable, target the appropriate resource group. Set the context for your cluster.](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure)
- To install Tiller with a Kubernetes service account and cluster role binding in the `tiller` project, make sure that you have the [`cluster-admin` role](/docs/openshift?topic=openshift-users#access_policies).

To install Helm in a cluster with public network access:

1. Install version 2.16.1 of the [Helm CLI](https://github.com/helm/helm/releases/tag/v2.16.1){: external} on your local machine.

2. Check whether you already installed Tiller with a Kubernetes service account in your cluster.
   ```
   oc get serviceaccount -n tiller
   ```
   {: pre}

   Example output if Tiller is installed:
   ```
   tiller      tiller                               1         189d
   ```
   {: screen}

   The example output includes the OpenShift project and name of the service account for Tiller. If Tiller is not installed with a service account in your cluster, no CLI output is returned.

3. **Important**: To maintain cluster security, set up Tiller with a service account and cluster role binding in your cluster.
   - **If Tiller is already installed with a service account:**
     1. Create a cluster role binding for the Tiller service account.
        ```
        oc create clusterrolebinding tiller --clusterrole=cluster-admin --serviceaccount=tiller:tiller -n tiller
        ```
        {: pre}

     2. Update Tiller. Replace `<tiller_service_account_name>` with the name of the Kubernetes service account for Tiller that you retrieved in the previous step.
        ```
        helm init --upgrade --service-account <tiller_service_account_name>
        ```
        {: pre}

     3. Verify that the `tiller-deploy` pod has a **Status** of `Running` in your cluster.
        ```
        oc get pods -n tiller -l app=helm
        ```
        {: pre}

        Example output:

        ```
        NAME                            READY     STATUS    RESTARTS   AGE
        tiller-deploy-352283156-nzbcm   1/1       Running   0          2m
        ```
        {: screen}

   - **If Tiller is not yet installed with a service account:**
     1.  As a cluster administrator, create a project for Tiller.
         ```
         oc adm new-project tiller
         ```
         {: pre}
     1. Create a Kubernetes service account and cluster role binding for Tiller in the `tiller` project of your cluster.
        ```
        oc create serviceaccount tiller -n tiller
        ```
        {: pre}

        ```
        oc create clusterrolebinding tiller --clusterrole=cluster-admin --serviceaccount=tiller:tiller -n tiller
        ```
        {: pre}

     2. Verify that the Tiller service account is created.
        ```
        oc get serviceaccount tiller -n tiller
        ```
        {: pre}

        Example output:
        ```
        NAME                                 SECRETS   AGE
        tiller                               1         2m
        ```
        {: screen}

     3. Initialize the Helm CLI and install Tiller in your cluster with the service account that you created.
        ```
        helm init --service-account tiller
        ```
        {: pre}

     4. Verify that the `tiller-deploy` pod has a **Status** of `Running` in your cluster.
        ```
        oc get pods -n tiller -l app=helm
        ```
        {: pre}

        Example output:
        ```
        NAME                            READY     STATUS    RESTARTS   AGE
        tiller-deploy-352283156-nzbcm   1/1       Running   0          2m
        ```
        {: screen}

4. Add the {{site.data.keyword.cloud_notm}} Helm repositories to your Helm instance.
   ```
   helm repo add iks-charts https://icr.io/helm/iks-charts
   ```
   {: pre}

   ```
   helm repo add ibm-charts https://raw.githubusercontent.com/IBM/charts/master/repo/stable
   ```
   {: pre}

   ```
   helm repo add ibm-community https://raw.githubusercontent.com/IBM/charts/master/repo/community
   ```
   {: pre}

   ```
   helm repo add entitled https://raw.githubusercontent.com/IBM/charts/master/repo/entitled
   ```
   {: pre}

5. Update the repos to retrieve the latest versions of all Helm charts.
   ```
   helm repo update
   ```
   {: pre}

6. List the Helm charts that are currently available in the {{site.data.keyword.cloud_notm}} repositories.
   ```
   helm search repo iks-charts
   ```
   {: pre}

   ```
   helm search repo ibm-charts
   ```
   {: pre}

   ```
   helm search repo ibm-community
   ```
   {: pre}

   ```
   helm search repo entitled
   ```
   {: pre}

7. Identify the Helm chart that you want to install and follow the instructions in the Helm chart `README` to install the Helm chart in your cluster.

### Installing Tiller with a different version than your cluster
{: #tiller_version}

By default, when you initiate Helm for your cluster, the version of Tiller matches the version of your cluster. For example, if you have a cluster that runs Kubernetes version 1.13, the Tiller version is 2.13. You can update your Tiller deployment to use a different version of the Tiller image. For more information, see the [Helm documentation ![External link icon](../icons/launch-glyph.svg "External link icon")](https://helm.sh/docs/install/).
{: shortdesc}

Some Helm charts might not be compatible with an older Tiller version. You see an error similar to the following:

```
Error: Chart incompatible with Tiller v2.11.0
```
{: screen}

To change your version of Tiller:
1.  Follow the instructions to install the Helm server Tiller [in your cluster](#public_helm_install).
2.  [Find the version of Tiller ![External link icon](../icons/launch-glyph.svg "External link icon")](https://console.cloud.google.com/gcr/images/kubernetes-helm/GLOBAL/tiller?gcrImageListsize=30) that is required by the Helm chart that you want to install. Hover over the digest image and click the **Copy full image name** icon.
3. Update your Tiller deployment to use the image that you previously copied.
   ```
   oc --namespace=tiller set image deployments/tiller-deploy tiller=<tiller_image>
   ```
   {: pre}

   Example command to change the Tiller image version to `2.12.3`:
   ```
   oc --namespace=tiller set image deployments/tiller-deploy tiller=gcr.io/kubernetes-helm/tiller@sha256:cab750b402d24dd7b24756858c31eae6a007cd0ee91ea802b3891e2e940d214d
   ```
   {: pre}
4. Confirm that the server version of Tiller that runs in your cluster is updated to the version that you set.
   ```
   helm version --server
   ```
   {: pre}

   Example output:
   ```
   Server: &version.Version{SemVer:"v2.12.3", GitCommit:"eecf22f77df5f65c823aacd2dbd30ae6c65f186e", GitTreeState:"clean"}
   ```
   {: screen}

## Related Helm links
{: #helm_links}

Review the following links to find additional Helm information.
{: shortdesc}

* View the available Helm charts that you can use in Red Hat OpenShift on IBM Cloud in the [Helm Charts Catalog](https://cloud.ibm.com/kubernetes/helm){: external}.
* Review the [list of changes between Helm v2 and v3](https://helm.sh/docs/topics/v2_v3_migration/){: external} and the [v3 FAQs](https://helm.sh/docs/faq/){: external}.
* Learn more about how you can [increase deployment velocity with Kubernetes Helm Charts](https://developer.ibm.com/recipes/tutorials/increase-deployment-velocity-with-kubernetes-helm-charts/){: external}.



