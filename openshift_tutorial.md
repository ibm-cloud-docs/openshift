---

copyright:
  years: 2014, 2021
lastupdated: "2021-03-05"

keywords: kubernetes, iks, oks, iro, openshift, red hat, red hat openshift, rhos, roks, rhoks

subcollection: openshift

content-type: tutorial
services: openshift
account-plan:
completion-time: 45m

---

{:DomainName: data-hd-keyref="APPDomain"}
{:DomainName: data-hd-keyref="DomainName"}
{:android: data-hd-operatingsystem="android"}
{:api: .ph data-hd-interface='api'}
{:apikey: data-credential-placeholder='apikey'}
{:app_key: data-hd-keyref="app_key"}
{:app_name: data-hd-keyref="app_name"}
{:app_secret: data-hd-keyref="app_secret"}
{:app_url: data-hd-keyref="app_url"}
{:authenticated-content: .authenticated-content}
{:beta: .beta}
{:c#: data-hd-programlang="c#"}
{:cli: .ph data-hd-interface='cli'}
{:codeblock: .codeblock}
{:curl: .ph data-hd-programlang='curl'}
{:deprecated: .deprecated}
{:dotnet-standard: .ph data-hd-programlang='dotnet-standard'}
{:download: .download}
{:external: target="_blank" .external}
{:faq: data-hd-content-type='faq'}
{:fuzzybunny: .ph data-hd-programlang='fuzzybunny'}
{:generic: data-hd-operatingsystem="generic"}
{:generic: data-hd-programlang="generic"}
{:gif: data-image-type='gif'}
{:go: .ph data-hd-programlang='go'}
{:help: data-hd-content-type='help'}
{:hide-dashboard: .hide-dashboard}
{:hide-in-docs: .hide-in-docs}
{:important: .important}
{:ios: data-hd-operatingsystem="ios"}
{:java: .ph data-hd-programlang='java'}
{:java: data-hd-programlang="java"}
{:javascript: .ph data-hd-programlang='javascript'}
{:javascript: data-hd-programlang="javascript"}
{:new_window: target="_blank"}
{:note .note}
{:note: .note}
{:objectc data-hd-programlang="objectc"}
{:org_name: data-hd-keyref="org_name"}
{:php: data-hd-programlang="php"}
{:pre: .pre}
{:preview: .preview}
{:python: .ph data-hd-programlang='python'}
{:python: data-hd-programlang="python"}
{:route: data-hd-keyref="route"}
{:row-headers: .row-headers}
{:ruby: .ph data-hd-programlang='ruby'}
{:ruby: data-hd-programlang="ruby"}
{:runtime: architecture="runtime"}
{:runtimeIcon: .runtimeIcon}
{:runtimeIconList: .runtimeIconList}
{:runtimeLink: .runtimeLink}
{:runtimeTitle: .runtimeTitle}
{:screen: .screen}
{:script: data-hd-video='script'}
{:service: architecture="service"}
{:service_instance_name: data-hd-keyref="service_instance_name"}
{:service_name: data-hd-keyref="service_name"}
{:shortdesc: .shortdesc}
{:space_name: data-hd-keyref="space_name"}
{:step: data-tutorial-type='step'}
{:subsection: outputclass="subsection"}
{:support: data-reuse='support'}
{:swift: .ph data-hd-programlang='swift'}
{:swift: data-hd-programlang="swift"}
{:table: .aria-labeledby="caption"}
{:term: .term}
{:tip: .tip}
{:tooling-url: data-tooling-url-placeholder='tooling-url'}
{:troubleshoot: data-hd-content-type='troubleshoot'}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:tsSymptoms: .tsSymptoms}
{:tutorial: data-hd-content-type='tutorial'}
{:ui: .ph data-hd-interface='ui'}
{:unity: .ph data-hd-programlang='unity'}
{:url: data-credential-placeholder='url'}
{:user_ID: data-hd-keyref="user_ID"}
{:vbnet: .ph data-hd-programlang='vb.net'}
{:video: .video}



# Creating {{site.data.keyword.openshiftlong_notm}} clusters
{: #openshift_tutorial}
{: toc-content-type="tutorial"}
{: toc-services="openshift"}
{: toc-completion-time="45m"}

Create a cluster with worker nodes that come installed with {{site.data.keyword.openshiftshort}} container orchestration platform.
{: shortdesc}

With {{site.data.keyword.openshiftlong}}, you can create highly available clusters with virtual or bare metal worker nodes that come installed with the {{site.data.keyword.openshiftlong_notm}} Container Platform orchestration software. You get all the [advantages of a managed offering](/docs/openshift?topic=openshift-cs_ov) for your cluster infrastructure environment, while using the [{{site.data.keyword.openshiftshort}} tooling and catalog](https://docs.openshift.com/container-platform/4.5/welcome/index.html){: external} that runs on Red Hat Enterprise Linux for your app deployments.

{{site.data.keyword.openshiftshort}} worker nodes are available for paid accounts and standard clusters only. In this tutorial, you create a cluster that runs version 4.6. The operating system is Red Hat Enterprise Linux 7.
{: note}

## Objectives
{: #openshift_objectives}

In the tutorial lessons, you create a standard {{site.data.keyword.openshiftlong_notm}} cluster, open the {{site.data.keyword.openshiftshort}} console, access built-in {{site.data.keyword.openshiftshort}} components, deploy an app in an {{site.data.keyword.openshiftshort}} project, and expose the app on an {{site.data.keyword.openshiftshort}} route so that external users can access the service.
{: shortdesc}

<img src="/images/roks_tutorial.png" width="600" alt="{{site.data.keyword.openshiftshort}} tutorial diagram" style="width:600px; border-style: none"/>

## Audience
{: #openshift_audience}

This tutorial is for cluster administrators who want to learn how to create a {{site.data.keyword.openshiftlong_notm}} cluster for the first time by using the CLI.
{: shortdesc}

## Prerequisites
{: #openshift_prereqs}

*   Ensure that you have the following {{site.data.keyword.cloud_notm}} IAM access policies.
    *   The [**Administrator** platform access role](/docs/openshift?topic=openshift-users#platform) for {{site.data.keyword.containerlong_notm}}
    *   The [**Writer** or **Manager** service access role](/docs/openshift?topic=openshift-users#platform) for {{site.data.keyword.containerlong_notm}}
    *   The [**Administrator** platform access role](/docs/openshift?topic=openshift-users#platform) for {{site.data.keyword.registrylong_notm}}
*   Make sure that the [API key](/docs/openshift?topic=openshift-users#api_key) for the {{site.data.keyword.cloud_notm}} region and resource group is set up with the correct infrastructure permissions, **Super User**, or the [minimum roles](/docs/openshift?topic=openshift-access_reference#infra) to create a cluster.

<br />

## Create a {{site.data.keyword.openshiftlong_notm}} cluster
{: #openshift_create_cluster}
{: step}

Create a {{site.data.keyword.openshiftlong_notm}} cluster. To learn about what components are set up when you create a cluster, see the [Service architecture](/docs/openshift?topic=openshift-service-arch#service-architecture). {{site.data.keyword.openshiftshort}} is available for only standard clusters. You can learn more about the price of standard clusters in the [frequently asked questions](/docs/openshift?topic=openshift-faqs#charges).
{: shortdesc}

1.  Install the command-line tools.
    *   [Install the {{site.data.keyword.cloud_notm}} CLI (`ibmcloud`), {{site.data.keyword.containershort_notm}} plug-in (`ibmcloud oc`), and {{site.data.keyword.registrylong_notm}} plug-in (`ibmcloud cr`)](/docs/containers?topic=containers-cs_cli_install#cs_cli_install_steps).
    *   [Install the {{site.data.keyword.openshiftshort}} (`oc`) and Kubernetes (`kubectl`) CLIs](/docs/openshift?topic=openshift-openshift-cli#cli_oc).
2.  Log in to the account and resource group where you want to create {{site.data.keyword.openshiftshort}} clusters. If you have a federated account, include the `--sso` flag.
    ```
    ibmcloud login [-g <resource_group>] [--sso]
    ```
    {: pre}
3.  Create a cluster with a unique name. The following command creates a version 4.6 cluster in Washington, DC with the minimum configuration of 2 worker nodes that have at least 4 cores and 16 GB memory so that default {{site.data.keyword.openshiftshort}} components can deploy. If you have existing VLANs that you want to use, get the VLAN IDs by running `ibmcloud oc vlan ls --zone <zone>`. For more information, see [Creating a standard classic cluster in the CLI](/docs/openshift?topic=openshift-clusters#clusters_cli_steps).
    ```
    ibmcloud oc cluster create classic --name my_openshift --location wdc04 --version 4.6_openshift --flavor b3c.4x16.encrypted  --workers 2 --public-vlan <public_VLAN_ID> --private-vlan <private_VLAN_ID> --public-service-endpoint
    ```
    {: pre}
4.  List your cluster details. Review the cluster **State**, check the **Ingress Subdomain**, and note the **Master URL**.<p class="note">Your cluster creation might take some time to complete. After the cluster state shows **Normal**, the cluster network and router components take about 10 more minutes to deploy and update the cluster domain that you use for the {{site.data.keyword.openshiftshort}} web console and other routes. Before you continue, wait until the cluster is ready by checking that the **Ingress Subdomain** follows a pattern of `<cluster_name>.<globally_unique_account_HASH>-0001.<region>.containers.appdomain.cloud`.</p>
    ```
    ibmcloud oc cluster get --cluster <cluster_name_or_ID>
    ```
    {: pre}
5.  Download and add the `kubeconfig` configuration file for your cluster to your existing `kubeconfig` in `~/.kube/config` or the last file in the `KUBECONFIG` environment variable.
    ```
    ibmcloud oc cluster config --cluster <cluster_name_or_ID>
    ```
    {: pre}
6.  In your browser, navigate to the address of your **Master URL** and append `/console`. For example, `https://c0.containers.cloud.ibm.com:23652/console`.
7.  From the {{site.data.keyword.openshiftshort}} web console menu bar, click your profile **IAM#user.name@email.com > Copy Login Command**. Display and copy the `oc login` token command into your command line to authenticate via the CLI.<p class="tip">Save your cluster master URL to access the {{site.data.keyword.openshiftshort}} console later. In future sessions, you can skip the `cluster config` step and copy the login command from the console instead.</p>
8.  Verify that the `oc` commands run properly with your cluster by checking the version.
    ```
    oc version
    ```
    {: pre}

    Example output:
    ```
    Client Version: v4.6.0
    Kubernetes Version: v1.19.2
    ```
    {: screen}

    If you cannot perform operations that require Administrator permissions, such as listing all the worker nodes or pods in a cluster, download the TLS certificates and permission files for the cluster administrator by running the `ibmcloud oc cluster config --cluster <cluster_name_or_ID> --admin` command.
    {: tip}

<br />

## Navigate the {{site.data.keyword.openshiftshort}} console
{: #openshift_oc_console}
{: step}

{{site.data.keyword.openshiftlong_notm}} comes with built-in services that you can use to help operate your cluster, such as the {{site.data.keyword.openshiftshort}} console.
{: shortdesc}

1.  From the [{{site.data.keyword.openshiftlong_notm}} console](https://cloud.ibm.com/kubernetes/clusters?platformType=openshift){: external}, select your {{site.data.keyword.openshiftshort}} cluster, then click **OpenShift web console**.
2.  Explore the different areas of the {{site.data.keyword.openshiftshort}} web console, as described in the following tabbed table.

    <table class="simple-tab-table" id="console1" tab-title="OCP 4" tab-group="console-version" aria-describedby="tableSummary-19ecbef4c01853826b42de82471b9035">
    <caption caption-side="top">
      <img src="images/icon-version-43.png" alt="Version 4 icon" width="30" style="width:30px; border-style: none"/> {{site.data.keyword.openshiftshort}} console overview<br>
      <span class="table-summary" id="tableSummary-19ecbef4c01853826b42de82471b9035">The rows are read from left to right. The area of the console is in the first column, the location in the console is in the second column, and the description of the console area in the third column. You can change between {{site.data.keyword.openshiftshort}} console versions by toggling the tabs at the beginning of the table.</span>
    </caption>
    <thead>
    <tr>
    <th>Area</th>
    <th>Location in console</th>
    <th>Description</th>
    </tr>
    </thead>
    <tbody>
    <tr>
    <td>Administrator perspective</td>
    <td>Side navigation menu perspective switcher.</td>
    <td>From the Administrator perspective, you can manage and set up the components that your team needs to run your apps, such as projects for your workloads, networking, and operators for integrating IBM, Red Hat, 3rd party, and custom services into the cluster. For more information, see [Viewing cluster information](http://docs.openshift.com/container-platform/4.5/web_console/using-dashboard-to-get-cluster-information.html){: external} in the {{site.data.keyword.openshiftshort}} documentation.</td>
    </tr>
    <tr>
    <td>Developer perspective</td>
    <td>Side navigation menu perspective switcher.</td>
    <td>From the Developer perspective, you can add apps to your cluster in a variety of ways, such as from Git repositories,container images, drag-and-drop or uploaded YAML files, operator catalogs, and more. The **Topology** view presents a unique way to visualize the workloads that run in a project and navigate their components from sidebars that aggregate related resources, including pods, services, routes, and metadata. For more information, see [Developer perspective](http://docs.openshift.com/container-platform/4.5/web_console/odc-about-developer-perspective.html){: external} in the {{site.data.keyword.openshiftshort}} documentation.</td>
    </tr>
    </tbody>
    </table>
    <table class="simple-tab-table" id="console2" tab-title="OCP 3" tab-group="console-version" aria-describedby="tableSummary-a4edc48da30a2a6943cabb6b3a128df4">
    <caption caption-side="top">
      <img src="images/icon-version-311.png" alt="Version 3.11 icon" width="30" style="width:30px; border-style: none"/> {{site.data.keyword.openshiftshort}} console overview<br>
      <span class="table-summary" id="tableSummary-a4edc48da30a2a6943cabb6b3a128df4">The rows are read from left to right. The area of the console is in the first column, the location in the console is in the second column, and the description of the console area in the third column. You can change between {{site.data.keyword.openshiftshort}} console versions by toggling the tabs at the beginning of the table.</span>
    </caption>
    <thead>
    <tr>
    <th>Area</th>
    <th>Location in console</th>
    <th>Description</th>
    </tr>
    </thead>
    <tbody>
    <tr>
    <td>Service Catalog</td>
    <td>Dropdown menu in the **OpenShift Container Platform** menu bar.</td>
    <td>Browse the catalog of built-in services that you can deploy on {{site.data.keyword.openshiftshort}}. For example, if you already have a `node.js` app that is hosted on GitHub, you can click the **Languages** tab and deploy a **JavaScript** app. The **My Projects** pane provides a quick view of all the projects that you have access to, and clicking on a project takes you to the Application Console. For more information, see the [{{site.data.keyword.openshiftshort}} Web Console Walkthrough](https://docs.openshift.com/container-platform/3.11/getting_started/developers_console.html){: external} in the {{site.data.keyword.openshiftshort}} documentation.</td>
    </tr>
    <tr>
    <td>Application Console</td>
    <td>Dropdown menu in the **OpenShift Container Platform** menu bar.</td>
    <td>For each project that you have access to, you can manage your {{site.data.keyword.openshiftshort}} resources such as pods, services, routes, builds, images or persistent volume claims. You can also view and analyze logs for these resources, or add services from the catalog to the project. For more information, see the [{{site.data.keyword.openshiftshort}} Web Console Walkthrough](https://docs.openshift.com/container-platform/3.11/getting_started/developers_console.html){: external} in the {{site.data.keyword.openshiftshort}} documentation.</td>
    </tr>
    <tr>
    <td>Cluster Console</td>
    <td>Dropdown menu in the **OpenShift Container Platform** menu bar.</td>
    <td>For cluster-wide administrators across all the projects in the cluster, you can manage projects, service accounts,RBAC roles, role bindings, and resource quotas. You can also see the status and events for resources within the cluster in a combined view. For more information, see the [{{site.data.keyword.openshiftshort}} Web Console Walkthrough](https://docs.openshift.com/container-platform/3.11/getting_started/developers_console.html){: external} in the {{site.data.keyword.openshiftshort}} documentation.</td>
    </tr>
    </tbody>
    </table><p></p>
3.  To work with your cluster in the CLI, click your profile **IAM#user.name@email.com > Copy Login Command**. Display and copy the `oc login` token command into your command line to authenticate via the CLI.

<br />

## Deploy an app to your {{site.data.keyword.openshiftshort}} cluster
{: #openshift_deploy_app}
{: step}

With {{site.data.keyword.openshiftlong_notm}}, you can create a new app and expose your app service via an {{site.data.keyword.openshiftshort}} router for external users to use.
{: shortdesc}

If you took a break from the last lesson and started a new command line, make sure that you log back in to your cluster. Open your {{site.data.keyword.openshiftshort}} web console at `https://<master_URL>/console`. For example, `https://c0.containers.cloud.ibm.com:23652/console`. Then from the menu bar, click your profile **IAM#user.name@email.com > Copy Login Command**. Display and copy the `oc login` token command into your command line to authenticate via the CLI.
{: tip}

1.  Create a project for your Hello World app. A project is an {{site.data.keyword.openshiftshort}} version of a Kubernetes namespace with additional annotations.
    ```
    oc new-project hello-world
    ```
    {: pre}
2.  Build the sample app [from the source code](https://github.com/IBM/container-service-getting-started-wt){: external}. With the {{site.data.keyword.openshiftshort}} `new-app` command, you can refer to a directory in a remote repository that contains the Dockerfile and app code to build your image. The command builds the image, stores the image in the local Docker registry, and creates the app deployment configurations (`dc`) and services (`svc`). For more information about creating new apps, [see the {{site.data.keyword.openshiftshort}} docs](http://docs.openshift.com/container-platform/4.5/applications/application_life_cycle_management/odc-creating-applications-using-developer-perspective.html){: external}.
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
        hello-world   ClusterIP   172.21.xxx.xxx   <none>       8080/TCP   31m
        ```
        {: screen}
    2.  List the pods. Pods with `build` in the name are jobs that **Completed** as part of the new app build process. Make sure that the **hello-world** pod status is **Running**.
        ```
        oc get pods -n hello-world
        ```
        {: pre}

        Example output:
        ```
        NAME                  READY     STATUS             RESTARTS   AGE
        hello-world-1-9cv7d   1/1       Running            0          30m
        hello-world-1-build   0/1       Completed          0          31m
        hello-world-1-deploy  0/1       Completed          0          31m
        ```
        {: screen}
4.  Set up a route so that you can publicly access the hello world service. By default, the hostname is in the format of `<service_name>-<project>.<cluster_name>-<random_ID>.<region>.containers.appdomain.cloud`. If you want to customize the hostname, include the `--hostname=<hostname>` flag. **Note**: The hostname that is assigned to your route is different than the Ingress subdomain that is assigned by default to your cluster. Your route does not use the Ingress subdomain.
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

For more information about working with your apps, see the [{{site.data.keyword.openshiftshort}} developer activities](https://docs.openshift.com/container-platform/4.5/welcome/index.html#developer-activities){: external} documentation.

Install two popular {{site.data.keyword.openshiftlong_notm}} add-ons: [{{site.data.keyword.la_full_notm}}](/docs/openshift?topic=openshift-health#openshift_logdna) and [{{site.data.keyword.mon_full_notm}}](/docs/openshift?topic=openshift-health-monitor#openshift_sysdig).
