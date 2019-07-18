---

copyright:
  years: 2014, 2019
lastupdated: "2019-07-18"

keywords: openshift, roks, rhoks, rhos, oc

subcollection: containers

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

# Installing the Red Hat OpenShift Container Platform CLI
{: #openshift-cli}

You can use the {{site.data.keyword.containerlong_notm}} CLI alias for OpenShift (`ibmcloud oc`) to create and manage your OpenShift cluster infrastructure, such as creating clusters and worker nodes. You can use the OpenShift Origin CLI (`oc`) to manage the resources within your OpenShift cluster, such as projects, pods, and deployments. 

## Installing the IBM Cloud CLI and plug-ins
{: #cli_ibmcloud_oc}

See the topic in the [{{site.data.keyword.containerlong_notm}} docs](/docs/containers?topic=containers-cs_cli_install#cs_cli_install_steps) to install the following CLIs.
{: shortdesc}

* {{site.data.keyword.cloud_notm}} CLI (`{[bx]}`)
* {{site.data.keyword.containershort_notm}} plug-in (`ibmcloud oc` alias for OpenShift clusters)
* Container Registry plug-in (`{[bxcr]}`)

<br />


## Installing the OpenShift Origin CLI (`oc`)
{: #cli_oc}

[Red Hat OpenShift on IBM Cloud](/docs/containers?topic=containers-openshift_tutorial) is available as a beta to test out OpenShift clusters.
{: preview}

To view a local version of the OpenShift dashboard and to deploy apps into your Red Hat OpenShift on IBM Cloud clusters, install the OpenShift Origin CLI (`oc`). The `oc` CLI includes a matching version of the Kubernetes CLI (`kubectl`). For more information, see the [OpenShift docs ![External link icon](../icons/launch-glyph.svg "External link icon")](https://docs.openshift.com/container-platform/3.11/cli_reference/get_started_cli.html).
{: shortdesc}

Using both Red Hat OpenShift on IBM Cloud and Ubuntu native {{site.data.keyword.containershort_notm}} clusters? The `oc` CLI comes with both the `oc` and `kubectl` binaries, but your different clusters might run different versions of Kubernetes, such as 1.11 on OpenShift and 1.13.8 on Ubuntu. Make sure to use the `kubectl` binary that matches your cluster `major.minor` Kubernetes version.
{: note}

1.  [Download the OpenShift Origin CLI ![External link icon](../icons/launch-glyph.svg "External link icon")](https://www.okd.io/download.html) for your local operating system and OpenShift version. The current default OpenShift version is 3.11.

2.  If you use Mac OS or Linux, complete the following steps to add the binaries to your `PATH` system variable. If you use Windows, install the `oc` CLI in the same directory as the {{site.data.keyword.cloud_notm}} CLI. This setup saves you some file path changes when you run commands later.
    1.  Move the `oc` and `kubectl` executable files to the `/usr/local/bin` directory.
        ```
        mv /<filepath>/oc /usr/local/bin/oc && mv /<filepath>/kubectl /usr/local/bin/kubectl
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
3.  If you have clusters that run different versions of Kubernetes, such as an OpenShift cluster with version 1.11 and a native Kubernetes cluster with version 1.14.4, download each `kubectl` version binary file to a separate directory.
    1.  Delete the `kubectl` binary file that comes with the `oc` installation, because this `kubectl` version does not work with native Kubernetes clusters.
        ```
        rm /usr/local/bin/kubectl
        ```
        {: pre}
    2.  [Download separate `kubectl` binary files](#kubectl) that match the versions of your OpenShift and native Kubernetes clusters.
    3.  **Optional**: Set up an alias in your local terminal profile to point to separate binaries that match the version of `kubectl` your cluster needs.
4.  **Optional**: [Enable autocompletion for `kubectl` commands ![External link icon](../icons/launch-glyph.svg "External link icon")](https://kubernetes.io/docs/tasks/tools/install-kubectl/#enabling-shell-autocompletion). The steps vary depending on the shell that you use. You can repeat the steps to enable autocompletion for `oc` commands. For example in bash on Linux, instead of `kubectl completion bash >/etc/bash_completion.d/kubectl`, you can run `oc completion bash >/etc/bash_completion.d/oc_completion`.

Next, start [Creating a Red Hat OpenShift on IBM Cloud cluster (preview)](/docs/containers?topic=containers-openshift_tutorial).

For more information about the OpenShift Origin CLI, see the [`oc` commands docs ![External link icon](../icons/launch-glyph.svg "External link icon")](https://docs.openshift.com/container-platform/3.11/cli_reference/basic_cli_operations.html).
{: note}

<br />


## Accessing an OpenShift cluster from the terminal or automation tools
{: #openshift_cluster_login}

Red Hat OpenShift on IBM Cloud is integrated with {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM) so that you can authenticate users and services by using their IAM identities and authorize actions with access roles and policies. When you authenticate as a user through the OpenShift console, your IAM identity is used to generate an OpenShift login token that you can use to log in to the terminal. If you want to automate logging in to your cluster, you can create an IAM API key to use for the `oc login` command.
{:shortdesc}

**Before you begin**:
* [Install the `oc` CLI](#cli_oc).
* [Create an OpenShift cluster](/docs/openshift?topic=openshift-openshift-create-cluster).

**To log in to your cluster as a user through the terminal**:
1.  In the [{{site.data.keyword.containerlong_notm}} console ![External link icon](../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/kubernetes/clusters), click the cluster that you want to access.
2.  Click the **Access** tab and follow the instructions.

<br>
**To automate access to your cluster with an API key**:
1.  Create an {{site.data.keyword.cloud_notm}} API key.<p class="important">Save your API key in a secure location. You cannot retrieve the API key again. If you want to export the output to a file on your local machine, include the `--file <path>/<file_name>` flag.</p>
    ```
    ibmcloud iam api-key-create <name>
    ```
    {: pre}
2.  Get the **Master URL** of the cluster that you want to access. 
    ```
    ibmcloud ks cluster-get --cluster <cluster_name_or_ID>
    ```
    {: pre}
3.  Use the API key and cluster URL to log in to your OpenShift cluster. The user name (`-u`) is `apikey`, the password (`-p`) is your API key value, and the `--server` is the service endpoint URL of the cluster master.
    ```
    oc login -u apikey -p <API_key> --server=<master_URL>
    ```
    {: pre}
