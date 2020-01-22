---

copyright:
  years: 2014, 2020
lastupdated: "2020-01-22"

keywords: openshift, roks, rhoks, rhos, oc

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


# Installing the OpenShift CLI
{: #openshift-cli}

You can use the {{site.data.keyword.openshiftlong}} command line interface (CLI) plug-in (`ibmcloud oc`) to create and manage your OpenShift cluster infrastructure, such as creating clusters and worker nodes. Then, you can use the OpenShift CLI (`oc`) to manage the resources within your OpenShift cluster, such as projects, pods, and deployments. To use the API, see [Setting up the API](/docs/openshift?topic=openshift-cs_api_install).

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
{: support}
{: help}

To view a local version of the OpenShift dashboard and to deploy apps into your Red Hat OpenShift on IBM Cloud clusters, install the OpenShift CLI (`oc`) and Kubernetes CLI (`kubectl`). For more information, see the [OpenShift docs](https://docs.openshift.com/container-platform/3.11/cli_reference/get_started_cli.html){: external}.
{: shortdesc}

Using both community Kubernetes and OpenShift clusters? Your clusters might run different versions of Kubernetes, such as 1.11 on OpenShift and 1.15.8 on Ubuntu. Make sure to use the `kubectl` binary file that matches the `+/- 1` [skew policy](https://kubernetes.io/docs/setup/release/version-skew-policy/){: external} for your cluster `major.minor` Kubernetes version.
{: note}

1.  Download the latest OpenShift CLI (`oc`) for your local operating system and OpenShift version. The current default OpenShift version is 3.11.

    *   [OpenShift Container Platform 3 `oc` download link](https://mirror.openshift.com/pub/openshift-v3/clients/){: external}

2.  [Download the Kubernetes CLI (`kubectl`)](/docs/containers?topic=containers-cs_cli_install#kubectl) for your OpenShift cluster. You might use different `kubectl` versions if you have community Kubernetes clusters that run other Kubernetes versions such as 1.16.5.

    *  For clusters that run OpenShift 3.11: Download at least version 1.13. Because `kubectl` versions 1.11 and 1.12 are no longer supported, the `kubectl` version that you use for your OpenShift 3.11, Kubernetes 1.11 cluster cannot meet the `+/- 1` [skew policy](https://kubernetes.io/docs/setup/release/version-skew-policy/){: external}. Instead, use at least `kubectl` version 1.13 to protect your cluster from Common Vulnerability and Exposures (CVEs) that might arise in unsupported versions.

    If you have multiple clusters that run different versions of Kubernetes, you can download separate `kubectl` binary files. Then, set up an alias in your local terminal profile to point to the separate binary files that match the version of `kubectl` your cluster needs.
    {: tip}

3.  If you use Mac OS or Linux, complete the following steps to add the binary files to your `PATH` system variable. If you use Windows, install the `oc` CLI in the same directory as the {{site.data.keyword.cloud_notm}} CLI. This setup saves you some file path changes when you run commands later.
    1.  Move the `oc` and `kubectl` executable files to the `/usr/local/bin` directory.
        ```
        mv /<filepath>/oc /usr/local/bin/oc
        ```
        {: pre}

        ```
        mv /<filepath>/kubectl /usr/local/bin/kubectl
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
4.  **Optional**: [Enable autocompletion for `kubectl` commands](https://kubernetes.io/docs/tasks/tools/install-kubectl/#enabling-shell-autocompletion){: external}. The steps vary depending on the shell that you use. You can repeat the steps to enable autocompletion for `oc` commands. For example, in bash on Linux, instead of `kubectl completion bash >/etc/bash_completion.d/kubectl`, you can run `oc completion bash >/etc/bash_completion.d/oc_completion`.

Next, start [Creating a Red Hat OpenShift on IBM Cloud cluster](/docs/openshift?topic=openshift-openshift_tutorial).

For more information about the OpenShift CLI, see the [`oc` commands docs](https://docs.openshift.com/container-platform/3.11/cli_reference/basic_cli_operations.html){: external}.
{: note}

<br />


## Using the Kubernetes web terminal in your web browser
{: #cli_web}

The Kubernetes web terminal allows you to use the {{site.data.keyword.cloud_notm}} CLI to manage your cluster directly from your web browser.
{: shortdesc}

You can use the Kubernetes web terminal for quick access and testing of your cluster. Do not use it for production workloads.
{: important}

If you use the cluster dashboard in the {{site.data.keyword.cloud_notm}} console to manage your clusters but want to quickly make more advanced configuration changes, you can now run CLI commands directly from your web browser in the Kubernetes web terminal. The Kubernetes Terminal is enabled with the base [{{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cloud-cli-getting-started){: external}, the {{site.data.keyword.containerlong_notm}} plug-in, and the {{site.data.keyword.registryshort_notm}} plug-in. Additionally, the terminal context is already set to the cluster that you are working with so that you can run Kubernetes `kubectl` commands to work with your cluster.

Any files that you download and edit locally, such as YAML files, are stored temporarily in Kubernetes Terminal and do not persist across sessions.
{: note}

To install and launch the Kubernetes web terminal:

1. In your [cluster dashboard](https://cloud.ibm.com/kubernetes/clusters){: external}, click the name of the cluster where you want to install the web terminal.
2.  From the upper right of the cluster detail page, click the **Web terminal** button.
3.  Click **Install**. It might take a few minutes for the terminal add-on to install.
4.  Click the **Web terminal** button again. The terminal opens in your browser.

Next time, you can launch the Kubernetes Terminal simply by clicking the **Web terminal** button.
