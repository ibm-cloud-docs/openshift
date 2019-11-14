---

copyright:
  years: 2014, 2019
lastupdated: "2019-11-14"

keywords: openshift, roks, rhoks, rhos, clusters

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

# Creating OpenShift clusters
{: #openshift-create-cluster}

Create a {{site.data.keyword.openshiftlong}} cluster.
{: shortdesc}

## Prerequisites
{: #openshift_cluster_prereqs}

To create OpenShift clusters, complete the following prerequisite steps.

1.  [Prepare your account to create clusters](/docs/containers?topic=containers-clusters#cluster_prepare). This step includes creating a billable account, setting up an API key with infrastructure permissions, making sure that you have Administrator access in {{site.data.keyword.cloud_notm}} IAM, planning resource groups, and setting up account networking.
2.  [Prepare to create clusters](/docs/containers?topic=containers-clusters#prepare_cluster_level). This step includes planning cluster setup, estimating costs, and if applicable, allowing network traffic through a firewall.<p class="note">OpenShift clusters are available [only as standard cluster, not free](/docs/openshift?topic=openshift-faqs#openshift_free).</p>
3.   [Install the {{site.data.keyword.cloud_notm}} and OpenShift CLIs](/docs/openshift?topic=openshift-openshift-cli).

<br />


## Creating a cluster with the console
{: #openshift_create_cluster_console}

Create a standard OpenShift cluster in the {{site.data.keyword.cloud_notm}} console.
{: shortdesc}

Before you begin, [complete the prerequisites](#openshift_cluster_prereqs).

1.  Create a cluster.
    1.  Log in to your [{{site.data.keyword.cloud_notm}} account ![External link icon](../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/).
    2.  From the hamburger menu ![hamburger menu icon](../icons/icon_hamburger.svg "hamburger menu icon"), select **OpenShift** and then click **Create cluster**.
    3.  Choose your cluster setup details and name.
    *   Fill out your cluster name, resource group, and tags.
    *   For the **Location**, set the **Geography**, and then select any of the six worldwide multizone **Metro** or single zone [locations](/docs/openshift?topic=openshift-regions-and-zones) to use for your **Worker zones**.
    *   For **Default worker pool**, choose an available flavor for your worker nodes. Red Hat OpenShift on IBM Cloud supports OpenShift version 3.11 only, which includes Kubernetes version 1.11. The operating system is Red Hat Enterprise Linux 7.
    1.  To finish, click **Create cluster**.<p class="note">Your cluster creation might take some time to complete. After the cluster state shows **Normal**, the cluster network and load-balancing components take about 10 more minutes to deploy and update the cluster domain that you use for the OpenShift web console and other routes. Wait until the cluster is ready before continuing to the next step by checking that the **Ingress subdomain** follows a pattern of `<cluster_name>.<region>.containers.appdomain.cloud`.<br><br>If your cluster does not reach a **deployed** state, check out the [Debugging clusters](/docs/containers?topic=containers-cs_troubleshoot) guide for help. For example, if your cluster is provisioned in an account that is protected by a firewall gateway appliance, you must [configure your firewall settings to allow outgoing traffic to the appropriate ports and IP addresses](/docs/openshift?topic=openshift-firewall).</p>
2.  From the cluster details page, click **OpenShift web console**. For more information about using the OpenShift console, see the [OpenShift docs ![External link icon](../icons/launch-glyph.svg "External link icon")](https://docs.openshift.com/container-platform/3.11/getting_started/developers_console.html).
3.  To continue working in the terminal: From the OpenShift web console menu bar, click your profile **IAM#user.name@email.com > Copy Login Command**. Paste the copied `oc` login command into your terminal to authenticate via the CLI.

<br />


## Creating a cluster with the CLI
{: #openshift_create_cluster_cli}

Create a standard OpenShift cluster by using the {{site.data.keyword.cloud_notm}} CLI.
{: shortdesc}

Before you begin, [complete the prerequisites](#openshift_cluster_prereqs).

1.  Log in to the account that you set up to create OpenShift clusters. Target the **us-east** or **eu-gb** region and the resource group. If you have a federated account, include the `--sso` flag.
    ```
    ibmcloud login -r (us-east|eu-gb) [-g default] [--sso]
    ```
    {: pre}
2.  Create a cluster.
    ```
    ibmcloud oc cluster create classic --name <name> --location <zone> --kube-version <openshift_version> --machine-type <worker_node_flavor> --workers <number_of_worker_nodes_per_zone> --public-vlan <public_VLAN_ID> --private-vlan <private_VLAN_ID>
    ```
    {: pre}

    Example command to create a cluster with three workers nodes that have four cores and 16 GB memory in Washington, DC:

    ```
    ibmcloud oc cluster create classic --name my_openshift --location wdc04 --kube-version 3.11_openshift --machine-type b3c.4x16.encrypted  --workers 3 --public-vlan <public_VLAN_ID> --private-vlan <private_VLAN_ID>
    ```
    {: pre}

    <table summary="The first row in the table spans both columns. The rest of the rows should be read left to right, with the command component in column one and the matching description in column two.">
    <caption>cluster create components</caption>
    <thead>
    <th colspan=2><img src="images/idea.png" alt="Idea icon"/> Understanding this command's components</th>
    </thead>
    <tbody>
    <tr>
    <td><code>cluster-create</code></td>
    <td>The command to create a classic infrastructure cluster in your {{site.data.keyword.cloud_notm}} account.</td>
    </tr>
    <tr>
    <td><code>--name <em>&lt;name&gt;</em></code></td>
    <td>Enter a name for your cluster. The name must start with a letter, can contain letters, numbers, and hyphens (-), and must be 35 characters or fewer. Use a name that is unique across {{site.data.keyword.cloud_notm}} regions.</td>
    </tr>
    <tr>
    <td><code>--location <em>&lt;zone&gt;</em></code></td>
    <td>Specify the zone where you want to create your cluster. For a list of supported zones, see [Single and multizone locations](/docs/openshift?topic=openshift-regions-and-zones#zones).</p></td>
    </tr>
    <tr>
      <td><code>--kube-version <em>&lt;openshift_version&gt;</em></code></td>
      <td>You must choose a supported OpenShift version. OpenShift versions include a Kubernetes version that differs from the Kubernetes versions that are available on community Kubernetes Ubuntu clusters. To list available OpenShift versions, run `ibmcloud oc versions`. To create a cluster with the latest the patch version, you can specify just the major and minor version, such as ` 3.11_openshift`.<br><br>Red Hat OpenShift on IBM Cloud supports OpenShift version 3.11 only, which includes Kubernetes version 1.11. The operating system is Red Hat Enterprise Linux 7.</td>
    </tr>
    <tr>
    <td><code>--machine-type <em>&lt;worker_node_flavor&gt;</em></code></td>
    <td>Choose a machine type, or flavor, for your worker nodes. You can deploy your worker nodes as virtual machines on shared or dedicated hardware, or as physical machines on bare metal. Available physical and virtual machines types vary by the zone in which you deploy the cluster. To list available flavors, run `ibmcloud oc flavors --zone <zone>`.</td>
    </tr>
    <tr>
    <td><code>--workers <em>&lt;number_of_worker_nodes_per_zone&gt;</em></code></td>
    <td>The number of worker nodes to include in the cluster. You might want to specify at least three worker nodes so that your cluster has enough resources to run the default components and for high availability. If the <code>--workers</code> option is not specified, one worker node is created.</td>
    </tr>
    <tr>
    <td><code>--public-vlan <em>&lt;public_vlan_id&gt;</em></code></td>
    <td>If you already have a public VLAN set up in your IBM Cloud infrastructure account for that zone, enter the ID of the public VLAN. To check available VLANs, run `ibmcloud oc vlan ls --zone <zone>`. <br><br>If you do not have a public VLAN in your account, do not specify this option. {{site.data.keyword.containerlong_notm}} automatically creates a public VLAN for you.</td>
    </tr>
    <tr>
    <td><code>--private-vlan <em>&lt;private_vlan_id&gt;</em></code></td>
    <td>If you already have a private VLAN set up in your IBM Cloud infrastructure account for that zone, enter the ID of the private VLAN. To check available VLANs, run `ibmcloud oc vlan ls --zone <zone>`. <br><br>If you do not have a private VLAN in your account, do not specify this option. {{site.data.keyword.containerlong_notm}} automatically creates a private VLAN for you.</td>
    </tr>
    </tbody></table>
3.  List your cluster details. Review the cluster **State**, check the **Ingress Subdomain**, and note the **Master URL**.<p class="note">Your cluster creation might take some time to complete. After the cluster state shows **Normal**, the cluster network and load-balancing components take about 10 more minutes to deploy and update the cluster domain that you use for the OpenShift web console and other routes. Wait until the cluster is ready before continuing to the next step by checking that the **Ingress Subdomain** follows a pattern of `<cluster_name>.<region>.containers.appdomain.cloud`.<br><br>Is your cluster not in a **deployed** state? Check out the [Debugging clusters](/docs/containers?topic=containers-cs_troubleshoot) guide for help. For example, if your cluster is provisioned in an account that is protected by a firewall gateway appliance, you must [configure your firewall settings to allow outgoing traffic to the appropriate ports and IP addresses](/docs/openshift?topic=openshift-firewall).</p>

    ```
    ibmcloud oc cluster get --cluster <cluster_name_or_ID>
    ```
    {: pre}

4.  Download the configuration files to connect to your cluster.
    ```
    ibmcloud oc cluster config --cluster <cluster_name_or_ID>
    ```
    {: pre}

    When the download of the configuration files is finished, a command is displayed that you can copy and paste to set the path to the local Kubernetes configuration file as an environment variable.

    Example for OS X:

    ```
    export KUBECONFIG=/Users/<user_name>/.bluemix/plugins/kubernetes-service/clusters/<cluster_name>/kube-config-<datacenter>-<cluster_name>.yml
    ```
    {: screen}
5.  In your browser, navigate to the address of your **Master URL** and append `/console`. For example, `https://c0.containers.cloud.ibm.com:23652/console`.
6.  From the OpenShift web console menu bar, click your profile **IAM#user.name@email.com > Copy Login Command**. Paste the copied `oc` login command into your terminal to authenticate via the CLI.<p class="tip">Save your cluster master URL to access the OpenShift console later. In future sessions, you can skip the `cluster config` step and copy the login command from the console instead.</p>
7.  Verify that the `oc` commands run properly with your cluster by checking the version.

    ```
    oc version
    ```
    {: pre}

    Example output:

    ```
    oc v3.11.0+0cbc58b
    kubernetes v1.11.0+d4cacc0
    features: Basic-Auth

    Server https://c0.containers.cloud.ibm.com:23652
    openshift v3.11.98
    kubernetes v1.11.0+d4cacc0
    ```
    {: screen}

<br />


## Next steps
{: #next_steps}

When the cluster is up and running, you can check out the following tasks:
- If you created the cluster in a multizone capable zone, [spread worker nodes by adding a zone to your cluster](/docs/openshift?topic=openshift-add_workers).
- [Deploy an app in your cluster](/docs/openshift?topic=openshift-openshift_apps).
- [Expose your apps with routes](/docs/openshift?topic=openshift-openshift_routes).
