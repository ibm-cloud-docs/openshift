---

copyright:
  years: 2014, 2019
lastupdated: "2019-11-26"

keywords: openshift, roks, rhoks, rhos, oc

subcollection: openshift

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:note: .note}
{:download: .download}
{:preview: .preview} 



# Installing the OpenShift CLI
{: #openshift-cli}

You can use the {{site.data.keyword.openshiftlong}} command line interface (CLI) plug-in (`ibmcloud oc`) to create and manage your OpenShift cluster infrastructure, such as creating clusters and worker nodes. Then, you can use the OpenShift Origin CLI (`oc`) to manage the resources within your OpenShift cluster, such as projects, pods, and deployments. To use the API, see [Setting up the API](/docs/openshift?topic=openshift-cs_api_install).

## Installing the IBM Cloud CLI and plug-ins
{: #cli_ibmcloud_oc}

See the topic in the [{{site.data.keyword.containerlong_notm}} docs](/docs/containers?topic=containers-cs_cli_install#cs_cli_install_steps) to install the following CLIs.
{: shortdesc}

* {{site.data.keyword.cloud_notm}} CLI (`ibmcloud`)
* {{site.data.keyword.containershort_notm}} plug-in (`ibmcloud oc` alias for OpenShift clusters)
* Container Registry plug-in (`ibmcloud cr`)

<br />


## Installing the OpenShift Origin CLI (`oc`)
{: #cli_oc}

To view a local version of the OpenShift dashboard and to deploy apps into your Red Hat OpenShift on IBM Cloud clusters, install the OpenShift Origin CLI (`oc`). The `oc` CLI includes a matching version of the Kubernetes CLI (`kubectl`). For more information, see the [OpenShift docs ![External link icon](../icons/launch-glyph.svg "External link icon")](https://docs.openshift.com/container-platform/3.11/cli_reference/get_started_cli.html).
{: shortdesc}

Using both community Kubernetes and OpenShift clusters? The `oc` CLI comes with both the `oc` and `kubectl` binary files, but your clusters might run different versions of Kubernetes, such as 1.11 on OpenShift and 1.14.9 on Ubuntu. Make sure to use the `kubectl` binary file that matches the `+/- 1` [skew policy ![External link icon](../icons/launch-glyph.svg "External link icon")](https://kubernetes.io/docs/setup/release/version-skew-policy/) for your cluster `major.minor` Kubernetes version.
{: note}

1.  [Download the OpenShift Origin CLI ![External link icon](../icons/launch-glyph.svg "External link icon")](https://www.okd.io/download.html) for your local operating system and OpenShift version. The current default OpenShift version is 3.11.

2.  If you use Mac OS or Linux, complete the following steps to add the binary files to your `PATH` system variable. If you use Windows, install the `oc` CLI in the same directory as the {{site.data.keyword.cloud_notm}} CLI. This setup saves you some file path changes when you run commands later.
    1.  Move the `oc` and `kubectl` executable files to the `/usr/local/bin` directory.
        ```
        mv /<filepath>/oc /usr/local/bin/oc
        ```
        {: pre}

    2.  Make sure that `/usr/local/bin` is listed in your `PATH` system variable. The `PATH` variable contains all directories where your operating system can find executable files. The directories that are listed in the `PATH` variable serve different purposes. `/usr/local/bin` is used to store executable files for software that is not part of the operating system and that was manually installed by the system administrator.
        ```
        echo $PATH
        ```
        {: pre}
        Example CLI output:
        ```
        /usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin
        ```
        {: screen}
3.  If you have clusters that run different versions of Kubernetes, such as an OpenShift cluster with version 1.11 and a community Kubernetes cluster with version 1.16.3: Download each `kubectl` version binary file to a separate directory. Your `kubectl` version must match the `+/- 1` [skew policy ![External link icon](../icons/launch-glyph.svg "External link icon")](https://kubernetes.io/docs/setup/release/version-skew-policy/) for your cluster `major.minor` Kubernetes version.
    1.  Delete the `kubectl` binary file that comes with the `oc` installation because this `kubectl` version does not work with community Kubernetes clusters.
        ```
        rm /usr/local/bin/kubectl
        ```
        {: pre}
    2.  [Download separate `kubectl` binary files](/docs/containers?topic=containers-cs_cli_install#kubectl) for your OpenShift and community Kubernetes clusters.<p class="important">The `kubectl` version 1.11 CLI has a bug that yields errors when you use `kubectl` commands to interact with OpenShift-specific resources, such as security context constraints (`kubectl get scc`). If you plan to use `kubectl` instead of `oc` commands, download the `kubectl` version 1.12 CLI instead of the 1.11 CLI. The 1.12 CLI is still within the `+/- 1` skew policy for your 3.11 OpenShift clusters. The `oc` CLI does not have this bug, so you can run `oc get scc` without error.</p>
    3.  **Optional**: Set up an alias in your local terminal profile to point to separate binaries that match the version of `kubectl` your cluster needs.
4.  **Optional**: [Enable autocompletion for `kubectl` commands ![External link icon](../icons/launch-glyph.svg "External link icon")](https://kubernetes.io/docs/tasks/tools/install-kubectl/#enabling-shell-autocompletion). The steps vary depending on the shell that you use. You can repeat the steps to enable autocompletion for `oc` commands. For example, in bash on Linux, instead of `kubectl completion bash >/etc/bash_completion.d/kubectl`, you can run `oc completion bash >/etc/bash_completion.d/oc_completion`.

Next, start [Creating a Red Hat OpenShift on IBM Cloud cluster](/docs/openshift?topic=openshift-openshift_tutorial).

For more information about the OpenShift Origin CLI, see the [`oc` commands docs ![External link icon](../icons/launch-glyph.svg "External link icon")](https://docs.openshift.com/container-platform/3.11/cli_reference/basic_cli_operations.html).
{: note}

<br />


## Using the Kubernetes web terminal in your web browser
{: #cli_web}

The Kubernetes web terminal allows you to use the {{site.data.keyword.cloud_notm}} CLI to manage your cluster directly from your web browser.
{: shortdesc}

You can use the Kubernetes web terminal for quick access and testing of your cluster. Do not use it for production workloads.
{: important}

If you use the cluster dashboard in the {{site.data.keyword.cloud_notm}} console to manage your clusters but want to quickly make more advanced configuration changes, you can now run CLI commands directly from your web browser in the Kubernetes web terminal. The Kubernetes Terminal is enabled with the base [{{site.data.keyword.cloud_notm}} CLI ![External link icon](../icons/launch-glyph.svg "External link icon")](/docs/cli?topic=cloud-cli-getting-started), the {{site.data.keyword.containerlong_notm}} plug-in, and the {{site.data.keyword.registryshort_notm}} plug-in. Additionally, the terminal context is already set to the cluster that you are working with so that you can run Kubernetes `kubectl` commands to work with your cluster.

Any files that you download and edit locally, such as YAML files, are stored temporarily in Kubernetes Terminal and do not persist across sessions.
{: note}

To install and launch the Kubernetes web terminal:

1. In your [cluster dashboard ![External link icon](../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/kubernetes/clusters), click the name of the cluster where you want to install the web terminal.
2.  From the upper right of the cluster detail page, click the **Web terminal** button.
3.  Click **Install**. It might take a few minutes for the terminal add-on to install.
4.  Click the **Web terminal** button again. The terminal opens in your browser.

Next time, you can launch the Kubernetes Terminal simply by clicking the **Web terminal** button.
