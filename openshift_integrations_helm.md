---

copyright:
  years: 2014, 2020
lastupdated: "2020-01-31"

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

## About Helm in Red Hat OpenShift on IBM Cloud
{: #about-helm}

### What is Helm and how do I use it?
{: #what-is-helm}

[Helm ![External link icon](../icons/launch-glyph.svg "External link icon")](https://helm.sh) is a Kubernetes package manager that uses Helm charts to define, install, and upgrade complex Kubernetes apps in your cluster. Helm charts package the specifications to generate YAML files for Kubernetes resources that build your app. These Kubernetes resources are automatically applied in your cluster and assigned a version by Helm. You can also use Helm to specify and package your own app and let Helm generate the YAML files for your Kubernetes resources.

### What Helm charts are supported in Red Hat OpenShift on IBM Cloud?
{: #supported-charts}

For an overview of available Helm charts, see the [Helm charts catalog ![External link icon](../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/kubernetes/helm). The Helm charts that are listed in this catalog are grouped as follows:

- **iks-charts**: Helm charts that are approved for Red Hat OpenShift on IBM Cloud. The name of this repo was changed from `ibm` to `iks-charts`.
- **ibm-charts**: Helm charts that are approved for Red Hat OpenShift on IBM Cloud and {{site.data.keyword.cloud_notm}} Private clusters.
- **ibm-community**: Helm charts that originated outside IBM, such as from [Red Hat OpenShift on IBM Cloud partners](/docs/openshift?topic=openshift-service-partners). These charts are supported and maintained by the community partners.
- **kubernetes**: Helm charts that are provided by the Kubernetes community and considered `stable` by the community governance. These charts are not verified to work in Red Hat OpenShift on IBM Cloud or {{site.data.keyword.cloud_notm}} Private clusters.
- **kubernetes-incubator**: Helm charts that are provided by the Kubernetes community and considered `incubator` by the community governance. These charts are not verified to work in Red Hat OpenShift on IBM Cloud or {{site.data.keyword.cloud_notm}} Private clusters.
- **entitled**: Helm charts of licensed software that you must purchase and for which you must set up cluster access with an entitlement key. For more information, see [Setting up a cluster to pull entitled software](/docs/openshift?topic=openshift-images#secret_entitled_software).

Helm charts from the **iks-charts**, **ibm-charts**, and, if licensed, **entitled** repositories are fully integrated into the {{site.data.keyword.cloud_notm}} support organization. If you have a question or an issue with using these Helm charts, you can use one of the Red Hat OpenShift on IBM Cloud support channels. For more information, see [Getting help and support](/docs/containers?topic=containers-cs_troubleshoot_clusters#clusters_getting_help).

### Do I install Helm v2 or v3?
{: #helm-v2-v3}

[Helm v3 was released on 13 November 2019](https://helm.sh/blog/helm-3-released/){:external}. Helm v3 provides several advantages over Helm v2. For example, the Helm server [Tiller is removed in Helm v3](https://helm.sh/docs/faq/#removal-of-tiller){: external}. You no longer need to set up a Tiller service account or initialize Helm with Tiller. Additionally, [chart release names are now scoped to namespaces](https://helm.sh/docs/faq/#release-names-are-now-scoped-to-the-namespace){: external} so that you can release one version of the same chart across several namespaces.

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

[Helm v3 was released on 13 November 2019](https://helm.sh/blog/helm-3-released/){:external}. In Helm v3, the Helm server Tiller is removed, among many other changes. Continue to use Helm with Tiller only if you have specific requirements to use Helm v2 in your cluster. Otherwise, migrate to Helm v3.
{: shortdesc}

1. Before you migrate, review the [list of changes between v2 and v3](https://helm.sh/docs/topics/v2_v3_migration/){: external} and the [v3 FAQs](https://helm.sh/docs/faq/){: external}.

2. Follow the [Helm v2 to v3 migration steps](https://helm.sh/blog/migrate-from-helm-v2-to-helm-v3/){: external}. These steps include installing the Helm v3 client, backing up Helm v2 data, using the [`helm-2to3` plug-in](https://github.com/helm/helm-2to3){: external} to migrate your Helm v2 configuration and releases, and cleaning up Helm v2 data and the v2 client.

3. Continue with step 2 in [Installing Helm v3 in your cluster](#install_v3) to add the {{site.data.keyword.cloud_notm}} Helm repositories to your Helm instance.

As you work with Helm charts, keep in mind the Helm v3 changes, such as the fact that [chart release names are now scoped to namespaces](https://helm.sh/docs/faq/#release-names-are-now-scoped-to-the-namespace){: external} and that several [Helm CLI commands are renamed](https://helm.sh/docs/faq/#cli-command-renames){: external}.

<br />


## Installing Helm v2 in your cluster
{: #install_v2}

[Helm v3 was released on 13 November 2019](https://helm.sh/blog/helm-3-released/){:external}. Helm v2 requires you to set up the Helm server, Tiller, which is removed in Helm v3. Because Tiller requires a specific service account due to security issues, install Helm v2 only if you have specific requirements to use Helm v2 in your cluster. Otherwise, [install the latest release of Helm v3](#install_v3).
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

### Installing Helm v2 in a private cluster
{: #private_v2}

Install Helm v2 in a cluster that does not have public access.
{: shortdesc}

To deploy Helm charts, you must install the Helm CLI on your local machine and install the Helm server Tiller in your cluster. The image for Tiller is stored in the public Google Container Registry. To access the image during the Tiller installation, your cluster must allow public network connectivity to the public Google Container Registry. Classic clusters that are connected to a public VLAN and VPC clusters with subnets that are configured with a public gateway can access the image and install Tiller. Private clusters that are protected with a custom firewall, or clusters that do not have public network connectivity, such as classic clusters that are connected to a private VLAN only, or VPC clusters with subnets that are not configured with a public gateway, do not allow access to the Tiller image. Instead, you can [pull the image to your local machine, tag it, and push the image to your namespace in {{site.data.keyword.registryshort_notm}}](#private_local_tiller). Or you can [install Helm charts without using Tiller](#private_install_without_tiller).

#### Pushing the Tiller image to your namespace in IBM Cloud Container Registry
{: #private_local_tiller}

You can pull the Tiller image to your local machine, push the image to your namespace in {{site.data.keyword.registryshort_notm}} and install Tiller in your private cluster by using the image in {{site.data.keyword.registryshort_notm}}.
{: shortdesc}

If you want to install a Helm chart without using Tiller, see [Private clusters: Installing Helm charts without using Tiller](#private_install_without_tiller).
{: tip}

Before you begin:
- Install Docker on your local machine. If you installed the [{{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cloud-cli-getting-started), Docker is already installed.
- [Install the {{site.data.keyword.registryshort_notm}} CLI plug-in and set up a namespace](/docs/Registry?topic=registry-getting-started#gs_registry_cli_install).
- To install Tiller with a Kubernetes service account and cluster role binding in the `tiller` project, make sure that you have the [`cluster-admin` role](/docs/openshift?topic=openshift-users#access_policies).

To install Tiller by using {{site.data.keyword.registryshort_notm}}:

1. Install the [Helm CLI](https://helm.sh/docs/using_helm/#installing-helm){: external} on your local machine.
2. Connect to your private classic cluster by using the {{site.data.keyword.cloud_notm}} infrastructure VPN tunnel that you set up, or to your VPC cluster by using the [VPC VPN service](/docs/vpc-on-classic-network?topic=vpc-on-classic-network---using-vpn-with-your-vpc).
3. [Find the version of Tiller ![External link icon](../icons/launch-glyph.svg "External link icon")](https://console.cloud.google.com/gcr/images/kubernetes-helm/GLOBAL/tiller?gcrImageListsize=30) that you want to install in your cluster. If you do not need a specific version, use the latest one. In the digest image row, click the vertical ellipsis action menu, and then click **Show Pull Command** to copy the pull command.
4. Pull the Tiller image from the public Google Container Registry to your local machine. Include the image tag that you copied in the previous step.
   ```
   docker pull <tiller_image>
   ```
   {: pre}

   Example output:
   ```
   docker pull gcr.io/kubernetes-helm/tiller:v2.13.0
   v2.13.0: Pulling from kubernetes-helm/tiller
   48ecbb6b270e: Pull complete
   d3fa0712c71b: Pull complete
   bf13a43b92e9: Pull complete
   b3f98be98675: Pull complete
   Digest: sha256:c4bf03bb67b3ae07e38e834f29dc7fd43f472f67cad3c078279ff1bbbb463aa6
   Status: Downloaded newer image for gcr.io/kubernetes-helm/tiller:v2.13.0
   ```
   {: screen}
5. [Tag the Tiller image](/docs/Registry?topic=registry-getting-started#gs_registry_images_pulling), then [push it to your namespace in {{site.data.keyword.registryshort_notm}}](/docs/Registry?topic=registry-getting-started#gs_registry_images_pushing).
6. To access the image in {{site.data.keyword.registryshort_notm}} from inside your cluster, [copy the image pull secret from the default project to the `tiller` project](/docs/openshift?topic=openshift-images#copy_imagePullSecret).
7. **Important**: To maintain cluster security, create a service account for Tiller in the `tiller` project and a Kubernetes RBAC cluster role binding for the `tiller-deploy` pod.
    1. [Get the Kubernetes service account and cluster role binding YAML file ![External link icon](../icons/launch-glyph.svg "External link icon")](https://raw.githubusercontent.com/IBM-Cloud/kube-samples/master/rbac/serviceaccount-tiller.yaml).
    2. Create the Kubernetes resources in your cluster.
       ```
       oc apply -f serviceaccount-tiller.yaml
       ```
       {: pre}

8. Install Tiller in your private cluster by using the image that you stored in your namespace in {{site.data.keyword.registryshort_notm}}.
   ```
   helm init --tiller-image <region>.icr.io/<mynamespace>/<myimage>:<tag> --service-account tiller
   ```
   {: pre}

9. Add the {{site.data.keyword.cloud_notm}} Helm repositories to your Helm instance.
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

10. Update the repos to retrieve the latest versions of all Helm charts.
    ```
    helm repo update
    ```
    {: pre}

11. List the Helm charts that are currently available in the {{site.data.keyword.cloud_notm}} repositories.
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

12. Identify the Helm chart that you want to install and follow the instructions in the Helm chart `README` to install the Helm chart in your cluster.

#### Installing Helm charts without using Tiller
{: #private_install_without_tiller}

If you don't want to install Tiller in your private cluster, you can manually create the Helm chart YAML files and apply them by using `oc` commands.
{: shortdesc}

The steps in this example show how to install Helm charts from the {{site.data.keyword.cloud_notm}} Helm chart repositories in your private cluster. If you want to install a Helm chart that is not stored in one of the {{site.data.keyword.cloud_notm}} Helm chart repositories, you must follow the instructions in this topic to create the YAML files for your Helm chart. In addition, you must download the Helm chart image from the public container registry, push it to your namespace in {{site.data.keyword.registryshort_notm}}, and update the `values.yaml` file to use the image in {{site.data.keyword.registryshort_notm}}.
{: note}

1. Install the <a href="https://helm.sh/docs/using_helm/#installing-helm" target="_blank">Helm CLI <img src="../icons/launch-glyph.svg" alt="External link icon"></a> on your local machine.
2. Connect to your private classic cluster by using the {{site.data.keyword.cloud_notm}} infrastructure VPN tunnel that you set up, or to your VPC cluster by using the [VPC VPN service](/docs/vpc-on-classic-network?topic=vpc-on-classic-network---using-vpn-with-your-vpc).
3. Add the {{site.data.keyword.cloud_notm}} Helm repositories to your Helm instance.
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

4. Update the repos to retrieve the latest versions of all Helm charts.
   ```
   helm repo update
   ```
   {: pre}

5. List the Helm charts that are currently available in the {{site.data.keyword.cloud_notm}} repositories.
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

6. Identify the Helm chart that you want to install, download the Helm chart to your local machine, and unpack the files of your Helm chart. The following example shows how to download the Helm chart for the cluster autoscaler version 1.0.3 and unpack the files in a `cluster-autoscaler` directory.
   ```
   helm fetch iks-charts/ibm-iks-cluster-autoscaler --untar --untardir ./cluster-autoscaler --version 1.0.3
   ```
   {: pre}

7. Navigate to the directory where you unpacked the Helm chart files.
   ```
   cd cluster-autoscaler
   ```
   {: pre}

8. Create an `output` directory for the YAML files that you generate by using the files in your Helm chart.
   ```
   mkdir output
   ```
   {: pre}

9. Open the `values.yaml` file and make any changes that are required by the Helm chart installation instructions.
   ```
   nano ibm-iks-cluster-autoscaler/values.yaml
   ```
   {: pre}

10. Use your local Helm installation to create all configuration YAML files for your Helm chart. The YAML files are stored in the `output` directory that you created earlier.
    ```
    helm template --values ./ibm-iks-cluster-autoscaler/values.yaml --output-dir ./output ./ibm-iks-cluster-autoscaler
    ```
    {: pre}

    Example output:
    ```
    wrote ./output/ibm-iks-cluster-autoscaler/templates/ca-configmap.yaml
    wrote ./output/ibm-iks-cluster-autoscaler/templates/ca-service-account-roles.yaml
    wrote ./output/ibm-iks-cluster-autoscaler/templates/ca-service.yaml
    wrote ./output/ibm-iks-cluster-autoscaler/templates/ca-deployment.yaml
    ```
    {: screen}

11. Deploy all YAML files to your private cluster.
    ```
    oc apply --recursive --filename ./output
    ```
   {: pre}

12. Optional: Remove all YAML files from the `output` directory.
    ```
    oc delete --recursive --filename ./output
    ```
    {: pre}

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
1.  Follow the instructions to install the Helm server Tiller for your [public](#public_helm_install) or [private](#private_local_tiller) cluster.
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

* View the available Helm charts that you can use in Red Hat OpenShift on IBM Cloud in the [Helm Charts Catalog](https://cloud.ibm.com/kubernetes/helm){:external}.
* Review the [list of changes between Helm v2 and v3](https://helm.sh/docs/topics/v2_v3_migration/){: external} and the [v3 FAQs](https://helm.sh/docs/faq/){: external}.
* Learn more about how you can [increase deployment velocity with Kubernetes Helm Charts](https://developer.ibm.com/recipes/tutorials/increase-deployment-velocity-with-kubernetes-helm-charts/){:external}.



