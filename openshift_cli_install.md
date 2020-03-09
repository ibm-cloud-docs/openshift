---

copyright:
  years: 2014, 2020
lastupdated: "2020-03-09"

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
{: #cs_cli_install_steps}

Install the required CLIs to create and manage your OpenShift clusters in Red Hat OpenShift on IBM Cloud, and to deploy containerized apps to your cluster.
{:shortdesc}

This task includes the information for installing these CLIs and plug-ins:

* {{site.data.keyword.cloud_notm}} CLI (`ibmcloud`)
* Red Hat OpenShift on IBM Cloud plug-in (`ibmcloud oc` alias for OpenShift clusters)
* {{site.data.keyword.registrylong_notm}} plug-in (`ibmcloud cr`)

If you want to use the {{site.data.keyword.cloud_notm}} console instead, you can run CLI commands directly from your web browser in the [{{site.data.keyword.cloud-shell_notm}}](#cloud-shell).
{: tip}

<br>
To install the CLIs:

1.  Install the [{{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cloud-cli-getting-started#idt-prereq){: external}. This installation includes:
    -   The base {{site.data.keyword.cloud_notm}} CLI (`ibmcloud`).
    -   The Red Hat OpenShift on IBM Cloud plug-in (`ibmcloud oc`).
    -   {{site.data.keyword.registryshort_notm}} plug-in (`ibmcloud cr`). Use this plug-in to set up your own namespace in a multi-tenant, highly available, and scalable private image registry that is hosted by IBM, and to store and share Docker images with other users. Docker images are required to deploy containers into a cluster.
    -   The Kubernetes CLI (`kubectl`) that matches the default version: 1.16.7.<p class="note">After you install the {{site.data.keyword.cloud_notm}} CLI, you must [also install the `oc` CLI and the `kubectl` version that matches your cluster](/docs/openshift?topic=openshift-openshift-cli).</p>
    -   The Helm CLI (`helm`). You might use Helm as a package manager to install {{site.data.keyword.cloud_notm}} services and complex apps to your cluster via Helm charts. You must still [set up Helm](/docs/openshift?topic=openshift-helm) in each cluster where you want to use Helm.

    Plan to use the CLI often? Try [Enabling shell autocompletion for {{site.data.keyword.cloud_notm}} CLI (Linux/MacOS only)](/docs/cli/reference/ibmcloud?topic=cloud-cli-shell-autocomplete#shell-autocomplete-linux).
    {: tip}

2.  Log in to the {{site.data.keyword.cloud_notm}} CLI. Enter your {{site.data.keyword.cloud_notm}} credentials when prompted.
    ```
    ibmcloud login
    ```
    {: pre}

    If you have a federated ID, use `ibmcloud login --sso` to log in to the {{site.data.keyword.cloud_notm}} CLI. Enter your username and use the provided URL in your CLI output to retrieve your one-time passcode. You know you have a federated ID when the login fails without the `--sso` and succeeds with the `--sso` option.
    {: tip}

4.  Verify that the Red Hat OpenShift on IBM Cloud plug-in and {{site.data.keyword.registryshort_notm}} plug-in are installed correctly.
    ```
    ibmcloud plugin list
    ```
    {: pre}

    Example output:
    ```
    Listing installed plug-ins...

    Plugin Name                            Version   Status
    container-registry                     0.1.404
    container-service/kubernetes-service   0.4.66
    ```
    {: screen}

For reference information about these CLIs, see the documentation for those tools.

-   [`ibmcloud` commands](/docs/cli/reference/ibmcloud?topic=cloud-cli-ibmcloud_cli#ibmcloud_cli)
-   [`ibmcloud oc` commands](/docs/openshift?topic=openshift-kubernetes-service-cli)
-   [`ibmcloud cr` commands](/docs/Registry?topic=container-registry-cli-plugin-containerregcli)

<br />



## Installing the OpenShift Origin CLI (`oc`)
{: #cli_oc}
{: support}
{: help}

To view a local version of the OpenShift dashboard and to deploy apps into your Red Hat OpenShift on IBM Cloud clusters, install the OpenShift CLI (`oc`) and Kubernetes CLI (`kubectl`). For more information, see the [OpenShift docs](https://docs.openshift.com/container-platform/4.3/cli_reference/openshift_cli/getting-started-cli.html){: external}.
{: shortdesc}

Using both community Kubernetes and OpenShift clusters? Your clusters might run different versions of Kubernetes, such as 1.11 on OpenShift and 1.16.7 on Ubuntu. Make sure to use the `kubectl` binary file that matches the `+/- 1` [skew policy](https://kubernetes.io/docs/setup/release/version-skew-policy/){: external} for your cluster `major.minor` Kubernetes version.
{: note}

1.  Download the latest OpenShift CLI (`oc`) for your local operating system and OpenShift version. The current default OpenShift version is 3.11.

    *   [OpenShift Container Platform 3 `oc` download link](https://mirror.openshift.com/pub/openshift-v3/clients/){: external}
    *   [OpenShift Container Platform 4 `oc` download link](https://mirror.openshift.com/pub/openshift-v4/clients/oc/){: external}

2.  [Download the Kubernetes CLI (`kubectl`)](/docs/openshift?topic=openshift-cs_cli_install#kubectl) for your OpenShift cluster. You might use different `kubectl` versions if you have community Kubernetes clusters that run other Kubernetes versions such as 1.17.3.

    *  For clusters that run OpenShift 3.11: Download at least version 1.15. Because earlier `kubectl` versions are no longer supported, the `kubectl` version that you use for your OpenShift 3.11, Kubernetes 1.11 cluster cannot meet the `+/- 1` [skew policy](https://kubernetes.io/docs/setup/release/version-skew-policy/){: external}. Instead, use at least `kubectl` version 1.15 to protect your cluster from Common Vulnerability and Exposures (CVEs) that might arise in unsupported versions.
    * For clusters that run OpenShift 4.3: Download `kubectl` version 1.16.

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

For more information about the `oc` CLI, see the [OpenShift documentation](https://docs.openshift.com/container-platform/4.3/cli_reference/openshift_cli/getting-started-cli.html){: external}.
{: note}

<br />



## Updating the CLI
{: #cs_cli_upgrade}

Update the CLIs regularly to use new features.
{:shortdesc}

This task includes the information for updating the following CLIs:
-   {{site.data.keyword.cloud_notm}} CLI version 0.8.0 or later
-   Red Hat OpenShift on IBM Cloud plug-in
-   OpenShift CLI
-   {{site.data.keyword.registryshort_notm}} plug-in

<br>
To update the CLIs:

1.  Update the {{site.data.keyword.cloud_notm}} CLI. Download the [latest version](/docs/cli?topic=cloud-cli-getting-started){: external} and run the installer.

2. Log in to the {{site.data.keyword.cloud_notm}} CLI. Enter your {{site.data.keyword.cloud_notm}} credentials when prompted.

    ```
    ibmcloud login
    ```
    {: pre}

     If you have a federated ID, use `ibmcloud login --sso` to log in to the {{site.data.keyword.cloud_notm}} CLI. Enter your username and use the provided URL in your CLI output to retrieve your one-time passcode. You know you have a federated ID when the login fails without the `--sso` and succeeds with the `--sso` option.
     {: tip}

3.  Update the Red Hat OpenShift on IBM Cloud plug-in.
    1.  Install the update from the {{site.data.keyword.cloud_notm}} plug-in repository.

        ```
        ibmcloud plugin update kubernetes-service 
        ```
        {: pre}

    2.  Verify the plug-in installation by running the following command and checking the list of the plug-ins that are installed.

        ```
        ibmcloud plugin list
        ```
        {: pre}

        The Red Hat OpenShift on IBM Cloud plug-in is displayed in the results as `kubernetes-service`.

    3.  Initialize the CLI.

        ```
        ibmcloud oc init
        ```
        {: pre}

4.  [Update the OpenShift CLI](#cli_oc).

5.  Update the {{site.data.keyword.registryshort_notm}} plug-in.
    1.  Install the update from the {{site.data.keyword.cloud_notm}} plug-in repository.

        ```
        ibmcloud plugin update container-registry 
        ```
        {: pre}

    2.  Verify the plug-in installation by running the following command and checking the list of the plug-ins that are installed.

        ```
        ibmcloud plugin list
        ```
        {: pre}

        The registry plug-in is displayed in the results as `container-registry`.

<br />


## Uninstalling the CLI
{: #cs_cli_uninstall}

If you no longer need the CLI, you can uninstall it.
{:shortdesc}

This task includes the information for removing these CLIs:


-   Red Hat OpenShift on IBM Cloud plug-in
-   {{site.data.keyword.registryshort_notm}} plug-in

To uninstall the CLIs:

1.  Uninstall the Red Hat OpenShift on IBM Cloud plug-in.

    ```
    ibmcloud plugin uninstall kubernetes-service
    ```
    {: pre}

2.  Uninstall the {{site.data.keyword.registryshort_notm}} plug-in.

    ```
    ibmcloud plugin uninstall container-registry
    ```
    {: pre}

4.  Verify the plug-ins were uninstalled by running the following command and checking the list of the plug-ins that are installed.

    ```
    ibmcloud plugin list
    ```
    {: pre}

    The `kubernetes-service` and the `container-registry` plug-in are not displayed in the results.

5.  [Uninstall the {{site.data.keyword.cloud_notm}} CLI.](/docs/cli?topic=cloud-cli-uninstall-ibmcloud-cli)

6.  Uninstall the Kubernetes CLI.
    ```
    sudo rm /usr/local/bin/oc
    ```
    {: pre}

<br />


## Using the {{site.data.keyword.cloud-shell_notm}} in your web browser (beta)
{: #cloud-shell}

[{{site.data.keyword.cloud-shell_full}}](https://cloud.ibm.com/shell){: external} allows you to use the {{site.data.keyword.cloud_notm}} CLI and various CLI plug-ins to manage your cluster directly from your web browser.
{: shortdesc}

<img src="images/icon-beta-flair.png" alt="Beta icon" width="30" style="width:30px; border-style: none"/> The {{site.data.keyword.cloud-shell_notm}} is a beta feature that is subject to change. Do not use it for production workloads.
{: preview}

The {{site.data.keyword.cloud-shell_notm}} is enabled with several [plug-ins and tools](/docs/cloud-shell?topic=cloud-shell-plugins-tools), including the base {{site.data.keyword.cloud_notm}} CLI (`ibmcloud`), the {{site.data.keyword.containerlong_notm}} plug-in (`ibmcloud oc`), the {{site.data.keyword.registryshort_notm}} plug-in (`ibmcloud cr`), and the OpenShift CLI (`oc`).

While you use the {{site.data.keyword.cloud-shell_short}}, keep in mind the following limitations:
* You can open up to five concurrent sessions, which operate independently so you can work with different resources, regions, and accounts at once.
* Any files that you download and edit locally, such as YAML files, are stored temporarily in the {{site.data.keyword.cloud-shell_short}} and do not persist across sessions.
* {{site.data.keyword.cloud-shell_short}} has a usage quota that limits you to 4 hours of continuous use or up to 30 hours within a week.

To launch and use the {{site.data.keyword.cloud-shell_notm}}:

1. In the [{{site.data.keyword.cloud_notm}} console](https://cloud.ibm.com/){:external} menu bar, click the {{site.data.keyword.cloud-shell_short}} icon ![{{site.data.keyword.cloud-shell_notm}} icon](../icons/terminal-cloud-shell.svg).
2. A session starts and automatically logs you in to the {{site.data.keyword.cloud_notm}} CLI with your current account credentials.
3. Access your cluster by getting the `oc login` token.
  1.  In the [Red Hat OpenShift on IBM Cloud console](https://cloud.ibm.com/kubernetes/clusters?platformType=openshift){: external}, click the cluster that you want to access.
  2.  In the **Actions...** drop-down list, select **Connect via CLI**.
  3.  Follow the instructions.
  <p class="note">If you cannot or do not want to open the OpenShift console, you can set the cluster context with the `--admin` flag through the CLI.<p class="pre"><code>ibmcloud oc cluster config -c <cluster_name_or_ID> --admin</code></p></p>

