---

copyright:
  years: 2014, 2019
lastupdated: "2019-11-19"

keywords: kubernetes, iks, oks, iro, openshift, red hat, red hat openshift, rhos, roks, rhoks

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
{:important: .important}
{:deprecated: .deprecated}
{:download: .download}
{:preview: .preview}
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}

# Tutorial: Creating a Red Hat OpenShift on IBM Cloud cluster
{: #openshift_tutorial}

With {{site.data.keyword.openshiftlong}}, you can create highly available clusters with virtual or bare metal worker nodes that come installed with the Red Hat OpenShift on IBM Cloud Container Platform orchestration software. You get all the [advantages of a managed offering](/docs/openshift?topic=openshift-cs_ov) for your cluster infrastructure environment, while using the [OpenShift tooling and catalog ![External link icon](../icons/launch-glyph.svg "External link icon")](https://docs.openshift.com/container-platform/3.11/welcome/index.html) that runs on Red Hat Enterprise Linux for your app deployments.
{: shortdesc}

OpenShift worker nodes are available for paid accounts and standard clusters only. Red Hat OpenShift on IBM Cloud supports OpenShift version 3.11 only, which includes Kubernetes version 1.11. The operating system is Red Hat Enterprise Linux 7.
{: note}


## Objectives
{: #openshift_objectives}

In the tutorial lessons, you create a standard Red Hat OpenShift on IBM Cloud cluster, open the OpenShift console, access built-in OpenShift components, deploy an app in an OpenShift project, and expose the app on an OpenShift route so that external users can access the service.
{: shortdesc}

<img src="/images/roks_tutorial.png" width="600" alt="OpenShift tutorial diagram" style="width:600px; border-style: none"/>

## Time required
{: #openshift_time}
45 minutes

## Audience
{: #openshift_audience}

This tutorial is for cluster administrators who want to learn how to create a Red Hat OpenShift on IBM Cloud cluster for the first time.
{: shortdesc}

## Prerequisites
{: #openshift_prereqs}

*   Ensure that you have the following {{site.data.keyword.cloud_notm}} IAM access policies.
    *   The [**Administrator** platform role](/docs/openshift?topic=openshift-users#platform) for {{site.data.keyword.containerlong_notm}}
    *   The [**Writer** or **Manager** service role](/docs/openshift?topic=openshift-users#platform) for {{site.data.keyword.containerlong_notm}}
    *   The [**Administrator** platform role](/docs/openshift?topic=openshift-users#platform) for {{site.data.keyword.registrylong_notm}}
*    Make sure that the [API key](/docs/openshift?topic=openshift-users#api_key) for the {{site.data.keyword.cloud_notm}} region and resource group is set up with the correct infrastructure permissions, **Super User**, or the [minimum roles](/docs/containers?topic=containers-access_reference#infra) to create a cluster.

<br />


## Lesson 1: Creating a Red Hat OpenShift on IBM Cloud cluster
{: #openshift_create_cluster}

Create a Red Hat OpenShift on IBM Cloud cluster. To learn about what components are set up when you create a cluster, see the [Service architecture](/docs/openshift?topic=openshift-service-arch). OpenShift is available for only standard clusters. You can learn more about the price of standard clusters in the [frequently asked questions](/docs/openshift?topic=openshift-faqs#charges).
{:shortdesc}

1.  Install the command-line tools.
    *   [Install the {{site.data.keyword.cloud_notm}} CLI (`ibmcloud`), {{site.data.keyword.containershort_notm}} plug-in (`ibmcloud oc`), and {{site.data.keyword.registryshort_notm}} plug-in (`ibmcloud cr`)](/docs/containers?topic=containers-cs_cli_install#cs_cli_install_steps).
    *   [Install the OpenShift Origin (`oc`) and Kubernetes (`kubectl`) CLIs](/docs/openshift?topic=openshift-openshift-cli#cli_oc).
2.  Log in to the account that you set up to create OpenShift clusters. Target the **us-east** or **eu-gb** region and the resource group. If you have a federated account, include the `--sso` flag.
    ```
    ibmcloud login -r (us-east|eu-gb) [-g default] [--sso]
    ```
    {: pre}
3.  Create a cluster with a unique name. The following command creates a cluster with three worker nodes that have four cores and 16 GB memory in Washington, DC. If you have existing VLANs that you want to use, get the VLAN IDs by running `ibmcloud oc vlan ls --zone <zone>`.
    ```
    ibmcloud oc cluster create classic --name my_openshift --location wdc04 --kube-version 3.11_openshift --machine-type b3c.4x16.encrypted  --workers 3 --public-vlan <public_VLAN_ID> --private-vlan <private_VLAN_ID>
    ```
    {: pre}
4.  List your cluster details. Review the cluster **State**, check the **Ingress Subdomain**, and note the **Master URL**.<p class="note">Your cluster creation might take some time to complete. After the cluster state shows **Normal**, the cluster network and load-balancing components take about 10 more minutes to deploy and update the cluster domain that you use for the OpenShift web console and other routes. Wait until the cluster is ready before continuing to the next step by checking that the **Ingress Subdomain** follows a pattern of `<cluster_name>.<region>.containers.appdomain.cloud`.</p>
    ```
    ibmcloud oc cluster get --cluster <cluster_name_or_ID>
    ```
    {: pre}
5.  Download the configuration files to connect to your cluster.
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
6.  In your browser, navigate to the address of your **Master URL** and append `/console`. For example, `https://c0.containers.cloud.ibm.com:23652/console`.
7.  From the OpenShift web console menu bar, click your profile **IAM#user.name@email.com > Copy Login Command**. Paste the copied `oc` login command into your terminal to authenticate via the CLI.<p class="tip">Save your cluster master URL to access the OpenShift console later. In future sessions, you can skip the `cluster config` step and copy the login command from the console instead.</p>
8.  Verify that the `oc` commands run properly with your cluster by checking the version.

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

    If you cannot perform operations that require Administrator permissions, such as listing all the worker nodes or pods in a cluster, download the TLS certificates and permission files for the cluster administrator by running the `ibmcloud oc cluster config --cluster <cluster_name_or_ID> --admin` command.
    {: tip}

<br />


## Lesson 2: Navigating the OpenShift console
{: #openshift_oc_console}

Red Hat OpenShift on IBM Cloud comes with built-in services that you can use to help operate your cluster, such as the OpenShift console.
{:shortdesc}

1.  From the [Red Hat OpenShift on IBM Cloud console ![External link icon](../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/kubernetes/clusters?platformType=openshift), select your OpenShift cluster, then click **OpenShift web console**.
2.  Explore the different areas of the OpenShift console by clicking the dropdown menu in the **OpenShift Container Platform** menu bar.
    * **Service Catalog**: Browse the catalog of built-in services that you can deploy on OpenShift. For example, if you already have an `node.js` app that is hosted in GitHub, you can click the **Languages** tab and deploy a **JavaScript** app. The **My Projects** pane provides a quick view of all the projects that you have access to, and clicking on a project takes you to the Application Console.
    * **Application Console**: For each project namespace that you have access to, you can manage and view logs for your OpenShift resources such as pods, services, routes, builds, images, or persistent volume claims. You can also add services from the catalog to the project.
    * **Cluster Console**: For cluster-wide administrators across all the projects in the cluster, you can manage projects, service accounts, RBAC roles and role bindings, and resource quotas. You can also see combined views of the status and events of the resources within the cluster.
3.  To continue working with your cluster in the terminal: From the Service Console or Application Console, click your profile **IAM#user.name@email.com > Copy Login Command**. Paste the copied `oc` login command into your terminal to authenticate via the CLI.

<br />


## Lesson 3: Deploying an app to your OpenShift cluster
{: #openshift_deploy_app}

With Red Hat OpenShift on IBM Cloud, you can create a new app and expose your app service via an OpenShift router for external users to use.
{: shortdesc}

If you took a break from the last lesson and started a new terminal, make sure that you log back in to your cluster. Open your OpenShift web console at `https://<master_URL>/console`. For example, `https://c0.containers.cloud.ibm.com:23652/console`. Then from the menu bar, click your profile **IAM#user.name@email.com > Copy Login Command** and paste the copied `oc` login command into your terminal to authenticate via the CLI.
{: tip}

1.  Create a project for your Hello World app. A project is an OpenShift version of a Kubernetes namespace with additional annotations.
    ```
    oc new-project hello-world
    ```
    {: pre}
2.  Build the sample app [from the source code ![External link icon](../icons/launch-glyph.svg "External link icon")](https://github.com/IBM/container-service-getting-started-wt). With the OpenShift `new-app` command, you can refer to a directory in a remote repository that contains the Dockerfile and app code to build your image. The command builds the image, stores the image in the local Docker registry, and creates the app deployment configurations (`dc`) and services (`svc`). For more information about creating new apps, [see the OpenShift docs ![External link icon](../icons/launch-glyph.svg "External link icon")](https://docs.openshift.com/container-platform/3.11/dev_guide/application_lifecycle/new_app.html).
    ```
    oc new-app --name hello-world https://github.com/IBM/container-service-getting-started-wt --context-dir="Lab 1"
    ```
    {: pre}
3.  Verify that the sample Hello World app components are created.
    1.  List the **hello-world** services and note the service name. Your app listens for traffic on these internal cluster IP addresses unless you create a route for the service so that the router can forward external traffic requests to the app.
        ```
        oc get svc -n hello-world
        ```
        {: pre}

        Example output:
        ```
        NAME          TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)    AGE
        hello-world   ClusterIP   172.21.xxx.xxx   <nones>       8080/TCP   31m
        ```
        {: screen}
    2.  List the pods. Pods with `build` in the name are jobs that **Completed** as part of the new app build process. Make sure that the **hello-world** pod status is **Running**.
        ```
        oc get pods -n hello-world
        ```
        {: pre}

        Example output:
        ```
        NAME                READY     STATUS             RESTARTS   AGE
        hello-world-9cv7d   1/1       Running            0          30m
        hello-world-build   0/1       Completed          0          31m
        ```
        {: screen}
4.  Set up a route so that you can publicly access the hello world service. By default, the hostname is in the format of `<service_name>-<namespace>.<cluster_name>-<random_ID>.<region>.containers.appdomain.cloud`. If you want to customize the hostname, include the `--hostname=<hostname>` flag. **Note**: The hostname that is assigned to your route is different than the Ingress subdomain that is assigned by default to your cluster. Your route does not use the Ingress subdomain.
    1.  Create a route for the **hello-world** service.
        ```
        oc create route edge --service=hello-world -n hello-world
        ```
        {: pre}
    2.  Get the route hostname address from the **Host/Port** output.
        ```
        oc get route -n hello-world
        ```
        {: pre}
        Example output:
        ```
        NAME          HOST/PORT                         PATH                                        SERVICES      PORT       TERMINATION   WILDCARD
        hello-world   hello-world-hello.world.<cluster_name>-<random_ID>.<region>.containers.appdomain.cloud    hello-world   8080-tcp   edge/Allow    None
        ```
        {: screen}
5.  Access your app. Be sure to append `https://` to your route hostname.
    ```
    curl https://hello-world-hello-world.<cluster_name>-<random_ID>.<region>.containers.appdomain.cloud
    ```
    {: pre}

    Example output:
    ```
    Hello world from hello-world-9cv7d! Your app is up and running in a cluster!
    ```
    {: screen}
6.  **Optional** To clean up the resources that you created in this lesson, you can use the labels that are assigned to each app.
    1.  List all the resources for each app in the `hello-world` project.
        ```
        oc get all -l app=hello-world -o name -n hello-world
        ```
        {: pre}
        Example output:
        ```
        pod/hello-world-1-dh2ff
        replicationcontroller/hello-world-1
        service/hello-world
        deploymentconfig.apps.openshift.io/hello-world
        buildconfig.build.openshift.io/hello-world
        build.build.openshift.io/hello-world-1
        imagestream.image.openshift.io/hello-world
        imagestream.image.openshift.io/node
        route.route.openshift.io/hello-world
        ```
        {: screen}
    2.  Delete all the resources that you created.
        ```
        oc delete all -l app=hello-world -n hello-world
        ```
        {: pre}



<br />


## What's next?
{: #openshift_next}

For more information about working with your apps and routing services, see the [OpenShift Developer Guide](https://docs.openshift.com/container-platform/3.11/dev_guide/index.html).

Install two popular {{site.data.keyword.containerlong_notm}} add-ons: [{{site.data.keyword.la_full_notm}}](/docs/openshift?topic=openshift-health#openshift_logdna) and [{{site.data.keyword.mon_full_notm}}](/docs/openshift?topic=openshift-health#openshift_sysdig).
