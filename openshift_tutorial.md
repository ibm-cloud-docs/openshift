---

copyright:
  years: 2014, 2022
lastupdated: "2022-09-06"

keywords: kubernetes, openshift, red hat, red hat openshift

subcollection: openshift

content-type: tutorial
services: openshift
account-plan:
completion-time: 45m

---

{{site.data.keyword.attribute-definition-list}}



# Creating {{site.data.keyword.openshiftlong_notm}} clusters
{: #openshift_tutorial}
{: toc-content-type="tutorial"}
{: toc-services="openshift"}
{: toc-completion-time="45m"}

Create a cluster with worker nodes that come installed with {{site.data.keyword.redhat_openshift_notm}} container orchestration platform.
{: shortdesc}

With {{site.data.keyword.openshiftlong}}, you can create highly available clusters with virtual or bare metal worker nodes that come installed with the {{site.data.keyword.openshiftlong_notm}} Container Platform orchestration software. You get all the [advantages of a managed offering](/docs/openshift?topic=openshift-cs_ov) for your cluster infrastructure environment, while using the [{{site.data.keyword.redhat_openshift_notm}} tooling and catalog](https://docs.openshift.com/container-platform/4.9/welcome/index.html){: external} that runs on Red Hat Enterprise Linux for your app deployments.

{{site.data.keyword.redhat_openshift_notm}} worker nodes are available for paid accounts and standard clusters only. In this tutorial, you create a cluster that runs version 4.9. The operating system is Red Hat Enterprise Linux 7.
{: note}

## Objectives
{: #openshift_objectives}

In the tutorial lessons, you create a standard {{site.data.keyword.openshiftlong_notm}} cluster, open the {{site.data.keyword.redhat_openshift_notm}} console, access built-in {{site.data.keyword.redhat_openshift_notm}} components, deploy an app in a {{site.data.keyword.redhat_openshift_notm}} project, and expose the app on a {{site.data.keyword.redhat_openshift_notm}} route so that external users can access the service.
{: shortdesc}

![OpenShift tutorial diagram.](images/roks_tutorial.png){: caption="Figure 1. OpenShift tutorial diagram" caption-side="bottom"}

## Audience
{: #openshift_audience}

This tutorial is for cluster administrators who want to learn how to create a {{site.data.keyword.openshiftlong_notm}} cluster for the first time by using the CLI.
{: shortdesc}

## Prerequisites
{: #openshift_prereqs}

Complete the following prerequisite steps to set up permissions and the command-line environment.
{: shortdesc}

**Permissions**: If you are the account owner, you already have the required permissions to create a cluster and can continue to the next step. Otherwise, ask the account owner to [set up the API key and assign you the minimum user permissions in {{site.data.keyword.cloud_notm}} IAM](/docs/openshift?topic=openshift-access_reference#cluster_create_permissions).

**Command-line tools**: For quick access to your resources from the command line, try the [{{site.data.keyword.cloud-shell_notm}}](https://cloud.ibm.com/shell){: external}. Otherwise, set up your local command-line environment by completing the following steps.
1. [Install the {{site.data.keyword.cloud_notm}} CLI (`ibmcloud`), {{site.data.keyword.containershort_notm}} plug-in (`ibmcloud oc`), and {{site.data.keyword.registrylong_notm}} plug-in (`ibmcloud cr`)](/docs/openshift?topic=openshift-openshift-cli#cs_cli_install_steps).
2. [Install the {{site.data.keyword.redhat_openshift_notm}} (`oc`) and Kubernetes (`kubectl`) CLIs](/docs/openshift?topic=openshift-openshift-cli#cli_oc).



## Create a {{site.data.keyword.openshiftlong_notm}} cluster
{: #openshift_create_cluster}
{: step}

Create a {{site.data.keyword.openshiftlong_notm}} cluster. To learn about what components are set up when you create a cluster, see the [Service architecture](/docs/openshift?topic=openshift-service-architecture). {{site.data.keyword.redhat_openshift_notm}} is available for only standard clusters. You can learn more about the price of standard clusters in the [frequently asked questions](/docs/openshift?topic=openshift-faqs#charges).
{: shortdesc}

1. Log in to the account and resource group where you want to create {{site.data.keyword.redhat_openshift_notm}} clusters. If you have a federated account, include the `--sso` flag.
    ```sh
    ibmcloud login [-g <resource_group>] [--sso]
    ```
    {: pre}

2. Create a cluster with a unique name. The following command creates a version 4.9 cluster in Washington, DC with the minimum configuration of 2 worker nodes that have at least 4 cores and 16 GB memory so that default {{site.data.keyword.redhat_openshift_notm}} components can deploy. If you have existing VLANs that you want to use, get the VLAN IDs by running `ibmcloud oc vlan ls --zone <zone>`. For more information, see [Creating a standard classic cluster in the CLI](/docs/openshift?topic=openshift-clusters#clusters_cli_steps).
    ```sh
    ibmcloud oc cluster create classic --name my_openshift --location wdc04 --version 4.9_openshift --flavor b3c.4x16.encrypted  --workers 2  --public-vlan <public_VLAN_ID> --private-vlan <private_VLAN_ID> --public-service-endpoint
    ```
    {: pre}

3. List your cluster details. Review the cluster **State**, check the **Ingress Subdomain**, and note the **Master URL**.

    Your cluster creation might take some time to complete. After the cluster state shows **Normal**, the cluster network and Ingress components take about 10 more minutes to deploy and update the cluster domain that you use for the {{site.data.keyword.redhat_openshift_notm}} web console and other routes. Before you continue, wait until the cluster is ready by checking that the **Ingress Subdomain** follows a pattern of `<cluster_name>.<globally_unique_account_HASH>-0001.<region>.containers.appdomain.cloud`.
    {: note}
    
    ```sh
    ibmcloud oc cluster get --cluster <cluster_name_or_ID>
    ```
    {: pre}

4. Download and add the `kubeconfig` configuration file for your cluster to your existing `kubeconfig` in `~/.kube/config` or the last file in the `KUBECONFIG` environment variable.
    ```sh
    ibmcloud oc cluster config --cluster <cluster_name_or_ID>
    ```
    {: pre}

5. In your browser, navigate to the address of your **Master URL** and append `/console`. For example, `https://c0.containers.cloud.ibm.com:23652/console`.
6. From the {{site.data.keyword.redhat_openshift_notm}} web console menu bar, click your profile **IAM#user.name@email.com > Copy Login Command**. Display and copy the `oc login` token command into your command line to authenticate via the CLI.
    Save your cluster master URL to access the {{site.data.keyword.redhat_openshift_notm}} console later. In future sessions, you can skip the `cluster config` step and copy the login command from the console instead.
    {: tip}
    
7. Verify that the `oc` commands run properly with your cluster by checking the version.
    ```sh
    oc version
    ```
    {: pre}

    Example output

    ```sh
    Client Version: v4.9.0
    Kubernetes Version: v1.23.10.2
    ```
    {: screen}

    If you can't perform operations that require Administrator permissions, such as listing all the worker nodes or pods in a cluster, download the TLS certificates and permission files for the cluster administrator by running the `ibmcloud oc cluster config --cluster <cluster_name_or_ID> --admin` command.
    {: tip}

## Navigate the {{site.data.keyword.redhat_openshift_notm}} console
{: #openshift_oc_console}
{: step}

{{site.data.keyword.openshiftlong_notm}} comes with built-in services that you can use to help operate your cluster, such as the {{site.data.keyword.redhat_openshift_notm}} console.
{: shortdesc}

### {{site.data.keyword.redhat_openshift_notm}} console overview
{: #openshift_console4_overview_tutorial}

1. From the [{{site.data.keyword.redhat_openshift_notm}} clusters console](https://cloud.ibm.com/kubernetes/clusters?platformType=openshift){: external}, select your {{site.data.keyword.redhat_openshift_notm}} cluster, then click **OpenShift web console**.
2. To work with your cluster in the CLI, click your profile **`IAM#user.name@email.com` > Copy Login Command**. Display and copy the `oc login` token command into your command line to authenticate by using the CLI.

You can explore the following areas of the {{site.data.keyword.redhat_openshift_notm}} web console.

Administrator perspective
:   The Administrator perspective is available from the side navigation menu perspective switcher. From the Administrator perspective, you can manage and set up the components that your team needs to run your apps, such as projects for your workloads, networking, and operators for integrating IBM, Red Hat, 3rd party, and custom services into the cluster. For more information, see [Viewing cluster information](http://docs.openshift.com/container-platform/4.9/web_console/using-dashboard-to-get-cluster-information.html){: external} in the {{site.data.keyword.redhat_openshift_notm}} documentation.

Developer perspective
:   The Developer perspective is available from the side navigation menu perspective switcher. From the Developer perspective, you can add apps to your cluster in a variety of ways, such as from Git repositories,container images, drag-and-drop or uploaded YAML files, operator catalogs, and more. The **Topology** view presents a unique way to visualize the workloads that run in a project and navigate their components from sidebars that aggregate related resources, including pods, services, routes, and metadata. For more information, see [Developer perspective](https://docs.openshift.com/container-platform/4.9/web_console/web-console-overview.html{: external} in the {{site.data.keyword.redhat_openshift_notm}} documentation. 



## Deploy an app to your {{site.data.keyword.redhat_openshift_notm}} cluster
{: #openshift_deploy_app}
{: step}

With {{site.data.keyword.openshiftlong_notm}}, you can create a new app and expose your app service via a {{site.data.keyword.redhat_openshift_notm}} Ingress controller for external users to use.
{: shortdesc}

If you took a break from the last lesson and started a new command line, make sure that you log back in to your cluster. Open your {{site.data.keyword.redhat_openshift_notm}} web console at `https://<master_URL>/console`. For example, `https://c0.containers.cloud.ibm.com:23652/console`. Then from the menu bar, click your profile **IAM#user.name@email.com > Copy Login Command**. Display and copy the `oc login` token command into your command line to authenticate via the CLI.
{: tip}

1. Create a project for your Hello World app. A project is a {{site.data.keyword.redhat_openshift_notm}} version of a Kubernetes namespace with additional annotations.
    ```sh
    oc new-project hello-world
    ```
    {: pre}

2. Build the sample app [from the source code](https://github.com/IBM/container-service-getting-started-wt){: external}. With the {{site.data.keyword.redhat_openshift_notm}} `new-app` command, you can refer to a directory in a remote repository that contains the Dockerfile and app code to build your image. The command builds the image, stores the image in the local Docker registry, and creates the app deployment configurations (`dc`) and services (`svc`). For more information about creating new apps, [see the {{site.data.keyword.redhat_openshift_notm}} docs](https://docs.openshift.com/container-platform/4.9/applications/creating_applications/){: external}.
    ```sh
    oc new-app --name hello-world https://github.com/IBM/container-service-getting-started-wt --context-dir="Lab 1"
    ```
    {: pre}

3. Verify that the sample Hello World app components are created.
    1. List the **hello-world** services and note the service name. Your app listens for traffic on these internal cluster IP addresses unless you create a route for the service so that the Ingress controller can forward external traffic requests to the app.
        ```sh
        oc get svc -n hello-world
        ```
        {: pre}

        Example output
        ```sh
        NAME          TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)    AGE
        hello-world   ClusterIP   172.21.xxx.xxx   <none>       8080/TCP   31m
        ```
        {: screen}

    2. List the pods. Pods with `build` in the name are jobs that **Completed** as part of the new app build process. Make sure that the **hello-world** pod status is **Running**.
        ```sh
        oc get pods -n hello-world
        ```
        {: pre}

        Example output
        ```sh
        NAME                  READY     STATUS             RESTARTS   AGE
        hello-world-1-9cv7d   1/1       Running            0          30m
        hello-world-1-build   0/1       Completed          0          31m
        hello-world-1-deploy  0/1       Completed          0          31m
        ```
        {: screen}

4. Set up a route so that you can publicly access the hello world service. By default, the hostname is in the format of `<service_name>-<project>.<cluster_name>-<random_ID>.<region>.containers.appdomain.cloud`. If you want to customize the hostname, include the `--hostname=<hostname>` flag. **Note**: The hostname that is assigned to your route is different than the Ingress subdomain that is assigned by default to your cluster. Your route does not use the Ingress subdomain.
    1. Create a route for the **hello-world** service.
        ```sh
        oc create route edge --service=hello-world -n hello-world
        ```
        {: pre}

    2. Get the route hostname address from the **Host/Port** output.
        ```sh
        oc get route -n hello-world
        ```
        {: pre}

        Example output
        ```sh
        NAME          HOST/PORT                         PATH                                        SERVICES      PORT       TERMINATION   WILDCARD
        hello-world   hello-world-hello.world.<cluster_name>-<random_ID>.<region>.containers.appdomain.cloud    hello-world   8080-tcp   edge/Allow    None
        ```
        {: screen}

5. Access your app. Be sure to append `https://` to your route hostname.
    ```sh
    curl https://hello-world-hello-world.<cluster_name>-<random_ID>.<region>.containers.appdomain.cloud
    ```
    {: pre}

    Example output

    ```sh
    Hello world from hello-world-9cv7d! Your app is up and running in a cluster!
    ```
    {: screen}

6. **Optional** To clean up the resources that you created in this lesson, you can use the labels that are assigned to each app.
    1. List all the resources for each app in the `hello-world` project.
        ```sh
        oc get all -l app=hello-world -o name -n hello-world
        ```
        {: pre}

        Example output
        ```sh
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

    2. Delete all the resources that you created.
        ```sh
        oc delete all -l app=hello-world -n hello-world
        ```
        {: pre}



## What's next?
{: #openshift_next}

For more information about working with your apps, see the [{{site.data.keyword.redhat_openshift_notm}} developer activities](https://docs.openshift.com/container-platform/4.9/welcome/index.html#developer-activities){: external} documentation.

Install two popular {{site.data.keyword.openshiftlong_notm}} add-ons: [{{site.data.keyword.la_full_notm}}](/docs/openshift?topic=openshift-health#openshift_logging) and [{{site.data.keyword.mon_full_notm}}](/docs/openshift?topic=openshift-health-monitor).

