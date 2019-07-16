---

copyright:
  years: 2014, 2019
lastupdated: "2019-07-16"

keywords: kubernetes, iks, oks, iro, openshift, red hat, red hat openshift, rhos, roks, rhoks

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
{:important: .important}
{:deprecated: .deprecated}
{:download: .download}
{:preview: .preview}
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}

# Tutorial: Creating an IBM Cloud Red Hat OpenShift Container Platform cluster (beta)
{: #openshift_tutorial} 

Red Hat OpenShift on IBM Cloud is available as a beta to test out OpenShift clusters. Not all the features of {{site.data.keyword.containerlong}} are available during the beta. Also, any OpenShift beta clusters that you create remain for only 30 days after the beta ends and Red Hat OpenShift on IBM Cloud becomes generally available.
{: preview}

With the **Red Hat OpenShift on IBM Cloud beta**, you can create {{site.data.keyword.containerlong_notm}} clusters with worker nodes that come installed with the Red Hat OpenShift on IBM Cloud Container Platform orchestration software. You get all the [advantages of managed {{site.data.keyword.containerlong_notm}}](/docs/containers?topic=containers-responsibilities_iks) for your cluster infrastructure environment, while using the [OpenShift tooling and catalog ![External link icon](../icons/launch-glyph.svg "External link icon")](https://docs.openshift.com/container-platform/3.11/welcome/index.html) that runs on Red Hat Enterprise Linux for your app deployments.
{: shortdesc}

OpenShift worker nodes are available for paid accounts and standard clusters only. Red Hat OpenShift on IBM Cloud supports OpenShift version 3.11 only, which includes Kubernetes version 1.11. The operating system is Red Hat Enterprise Linux 7.
{: note}

## Objectives
{: #openshift_objectives}

In the tutorial lessons, you create a standard Red Hat OpenShift on IBM Cloud cluster, open the OpenShift console, access built-in OpenShift components, deploy an app that uses {{site.data.keyword.cloud_notm}} services in an OpenShift project, and expose the app on an OpenShift route so that external users can access the service.
{: shortdesc}

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
    *   The [**Administrator** platform role](/docs/containers?topic=containers-users#platform) for {{site.data.keyword.containerlong_notm}}
    *   The [**Writer** or **Manager** service role](/docs/containers?topic=containers-users#platform) for {{site.data.keyword.containerlong_notm}}
    *   The [**Administrator** platform role](/docs/containers?topic=containers-users#platform) for {{site.data.keyword.registrylong_notm}}
*    Make sure that the [API key](/docs/containers?topic=containers-users#api_key) for the {{site.data.keyword.cloud_notm}} region and resource group is set up with the correct infrastructure permissions, **Super User**, or the [minimum roles](/docs/containers?topic=containers-access_reference#infra) to create a cluster.

<br />


## Lesson 1: Creating a Red Hat OpenShift on IBM Cloud cluster
{: #openshift_create_cluster}

Create a Red Hat OpenShift on IBM Cloud cluster in {{site.data.keyword.containerlong_notm}}. To learn about what components are set up when you create a cluster, see the [Service architecture](/docs/openshift?topic=openshift-openshift-service-arch). OpenShift is available for only standard clusters. You can learn more about the price of standard clusters in the [frequently asked questions](/docs/openshift?topic=openshift-faqs#charges).
{:shortdesc}

Any OpenShift clusters that you create during the beta remain for 30 days after the beta ends and Red Hat OpenShift on IBM Cloud becomes generally available.
{: important}

1.  Install the command-line tools.
    *   [Install the {{site.data.keyword.cloud_notm}} CLI (`ibmcloud`), {{site.data.keyword.containershort_notm}} plug-in (`ibmcloud ks`), and {{site.data.keyword.registryshort_notm}} plug-in (`ibmcloud cr`)](/docs/containers?topic=containers-cs_cli_install#cs_cli_install_steps).
    *   [Install the OpenShift Origin (`oc`) and Kubernetes (`kubectl`) CLIs](/docs/containers?topic=containers-cs_cli_install#cli_oc).
1.  Log in to the account that you set up to create OpenShift clusters. Target the **us-east** or **eu-gb** region and the resource group. If you have a federated account, include the `--sso` flag.
    ```
    ibmcloud login -r (us-east|eu-gb) [-g default] [--sso]
    ```
    {: pre}
2.  Create a cluster.
    ```
    ibmcloud ks cluster-create --name <name> --location <zone> --kube-version <openshift_version> --machine-type <worker_node_flavor> --workers <number_of_worker_nodes_per_zone> --public-vlan <public_VLAN_ID> --private-vlan <private_VLAN_ID>
    ```
    {: pre}

    Example command to create a cluster with three workers nodes that have four cores and 16 GB memory in Washington, DC.

    ```
    ibmcloud ks cluster-create --name my_openshift --location wdc04 --kube-version 3.11_openshift --machine-type b3c.4x16.encrypted  --workers 3 --public-vlan <public_VLAN_ID> --private-vlan <private_VLAN_ID>
    ```
    {: pre}

    <table summary="The first row in the table spans both columns. The rest of the rows should be read left to right, with the command component in column one and the matching description in column two.">
    <caption>cluster-create components</caption>
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
    <td>Enter a name for your cluster. The name must start with a letter, can contain letters, numbers, and hyphen (-), and must be 35 characters or fewer. Use a name that is unique across {{site.data.keyword.cloud_notm}} regions.</td>
    </tr>
    <tr>
    <td><code>--location <em>&lt;zone&gt;</em></code></td>
    <td>Specify the zone where you want to create your cluster. For the beta, available zones are `wdc04, wdc06, wdc07, lon04, lon05,` or `lon06`.</p></td>
    </tr>
    <tr>
      <td><code>--kube-version <em>&lt;openshift_version&gt;</em></code></td>
      <td>You must choose a supported OpenShift version. OpenShift versions include a Kubernetes version that differs from the Kubernetes versions that are available on native Kubernetes Ubuntu clusters. To list available OpenShift versions, run `ibmcloud ks versions`. To create a cluster with the latest the patch version, you can specify just the major and minor version, such as ` 3.11_openshift`.<br><br>Red Hat OpenShift on IBM Cloud supports OpenShift version 3.11 only, which includes Kubernetes version 1.11. The operating system is Red Hat Enterprise Linux 7.</td>
    </tr>
    <tr>
    <td><code>--machine-type <em>&lt;worker_node_flavor&gt;</em></code></td>
    <td>Choose a machine type. You can deploy your worker nodes as virtual machines on shared or dedicated hardware, or as physical machines on bare metal. Available physical and virtual machines types vary by the zone in which you deploy the cluster. To list available machine-types, run `ibmcloud ks machine-types --zone <zone>`.</td>
    </tr>
    <tr>
    <td><code>--workers <em>&lt;number_of_worker_nodes_per_zone&gt;</em></code></td>
    <td>The number of worker nodes to include in the cluster. You might want to specify at least three worker nodes so that your cluster has enough resources to run the default components and for high availability. If the <code>--workers</code> option is not specified, one worker node is created.</td>
    </tr>
    <tr>
    <td><code>--public-vlan <em>&lt;public_vlan_id&gt;</em></code></td>
    <td>If you already have a public VLAN set up in your IBM Cloud infrastructure (SoftLayer) account for that zone, enter the ID of the public VLAN. To check available VLANs, run `ibmcloud ks vlans --zone <zone>`. <br><br>If you do not have a public VLAN in your account, do not specify this option. {{site.data.keyword.containerlong_notm}} automatically creates a public VLAN for you.</td>
    </tr>
    <tr>
    <td><code>--private-vlan <em>&lt;private_vlan_id&gt;</em></code></td>
    <td>If you already have a private VLAN set up in your IBM Cloud infrastructure (SoftLayer) account for that zone, enter the ID of the private VLAN. To check available VLANs, run `ibmcloud ks vlans --zone <zone>`. <br><br>If you do not have a private VLAN in your account, do not specify this option. {{site.data.keyword.containerlong_notm}} automatically creates a private VLAN for you.</td>
    </tr>
    </tbody></table>
3.  List your cluster details. Review the cluster **State**, check the **Ingress Subdomain**, and note the **Master URL**.<p class="note">Your cluster creation might take some time to complete. After the cluster state shows **Normal**, the cluster network and load-balancing components take about 10 more minutes to deploy and update the cluster domain that you use for the OpenShift web console and other routes. Wait until the cluster is ready before continuing to the next step by checking that the **Ingress Subdomain** follows a pattern of `<cluster_name>.<region>.containers.appdomain.cloud`.</p>
    ```
    ibmcloud ks cluster-get --cluster <cluster_name_or_ID>
    ```
    {: pre}
4.  Download the configuration files to connect to your cluster.
    ```
    ibmcloud ks cluster-config --cluster <cluster_name_or_ID>
    ```
    {: pre}

    When the download of the configuration files is finished, a command is displayed that you can copy and paste to set the path to the local Kubernetes configuration file as an environment variable.

    Example for OS X:

    ```
    export KUBECONFIG=/Users/<user_name>/.bluemix/plugins/kubernetes-service/clusters/<cluster_name>/kube-config-<datacenter>-<cluster_name>.yml
    ```
    {: screen}
5.  In your browser, navigate to the address of your **Master URL** and append `/console`. For example, `https://c0.containers.cloud.ibm.com:23652/console`.
6.  From the OpenShift web console menu bar, click your profile **IAM#user.name@email.com > Copy Login Command**. Paste the copied `oc` login command into your terminal to authenticate via the CLI.<p class="tip">Save your cluster master URL to access the OpenShift console later. In future sessions, you can skip the `cluster-config` step and copy the login command from the console instead.</p>
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

    If you cannot perform operations that require Administrator permissions, such as listing all the worker nodes or pods in a cluster, download the TLS certificates and permission files for the cluster administrator by running the `ibmcloud ks cluster-config --cluster <cluster_name_or_ID> --admin` command.
    {: tip}

<br />


## Lesson 2: Accessing built-in OpenShift services
{: #openshift_access_oc_services}

Red Hat OpenShift on IBM Cloud comes with built-in services that you can use to help operate your cluster, such as the OpenShift console, Prometheus, and Grafana. For the beta, to access these services, you can use the local host of a [route ![External link icon](../icons/launch-glyph.svg "External link icon")](https://docs.openshift.com/container-platform/3.11/architecture/networking/routes.html). The default route domain names follow a cluster-specific pattern of `<service_name>-<namespace>.<cluster_name>-<random_ID>.<region>.containers.appdomain.cloud`.
{:shortdesc}

You can access the built-in OpenShift service routes from the [console](#openshift_services_console) or [CLI](#openshift_services_cli). You might want to use the console to navigate through Kubernetes resources in one project. By using the CLI, you can list resources such as routes across projects.

### Accessing built-in OpenShift services from the console
{: #openshift_services_console}
1.  From the OpenShift web console, in the dropdown menu in the OpenShift container platform menu bar, click **Application Console**.
2.  Select the **default** project, then in the navigation pane, click **Applications > Pods**.
3.  Verify that the **router** pods are in a **Running** status. The router functions as the ingress point for external network traffic. You can use the router to publicly expose the services in your cluster on the router's external IP address by using a route. The router listens on the public host network interface, unlike your app pods that listen only on private IPs. The router proxies external requests for route host names to the IPs of the app pods that are identified by the service that you associated with the route host name.
4.  From the **default** project navigation pane, click **Applications > Deployments** and then click the **registry-console** deployment. Your OpenShift cluster comes with an internal registry that you can use to manage local images for your deployments. To view your images, click **Applications > Routes** and open the registry console **Hostname** URL.
5.  In the OpenShift container platform menu bar, from the dropdown menu, click **Cluster Console**.
6.  From the navigation pane, expand **Monitoring**.
7.  Click the built-in monitoring tool that you want to access, such as **Dashboards**. The Grafana route opens, `https://grafana-openshift-monitoring.<cluster_name>-<random_ID>.<region>.containers.appdomain.cloud`.<p class="note">The first time that you access the host name, you might need to authenticate, such as by clicking **Log in with OpenShift** and authorizing access to your IAM identity.</p>

### Accessing built-in OpenShift services from the CLI
{: #openshift_services_cli}

1.  From the **Application Console** or **Service Console** view in the OpenShift  web console, click your profile **IAM#user.name@email.com > Copy Login Command** and paste the login command into your terminal to authenticate.
    ```
    oc login https://c1-e.<region>.containers.cloud.ibm.com:<port> --token=<access_token>
    ```
    {: pre}
2.  Verify that your router is deployed. The router functions as the ingress point for external network traffic. You can use the router to publicly expose the services in your cluster on the router's external IP address by using a route. The router listens on the public host network interface, unlike your app pods that listen only on private IPs. The router proxies external requests for route host names to the IPs of the app pods that are identified by the service that you associated with the route host name.
    ```
    oc get svc router -n default
    ```
    {: pre}

    Example output:
    ```
    NAME      TYPE           CLUSTER-IP               EXTERNAL-IP     PORT(S)                      AGE
    router    LoadBalancer   172.21.xxx.xxx   169.xx.xxx.xxx   80:30399/TCP,443:32651/TCP                      5h
    ```
    {: screen}
2.  Get the **Host/Port** host name of the service route that you want to access. For example, you might want to access your Grafana dashboard to check metrics on your cluster's resource usage. The default route domain names follow a cluster-specific pattern of `<service_name>-<namespace>.<cluster_name>-<random_ID>.<region>.containers.appdomain.cloud`.
    ```
    oc get route --all-namespaces
    ```
    {: pre}

    Example output:
    ```
    NAMESPACE                          NAME                HOST/PORT                                                                    PATH                  SERVICES            PORT               TERMINATION          WILDCARD
    default                            registry-console    registry-console-default.<cluster_name>-<random_ID>.<region>.containers.appdomain.cloud                              registry-console    registry-console   passthrough          None
    kube-service-catalog               apiserver           apiserver-kube-service-catalog.<cluster_name>-<random_ID>.<region>.containers.appdomain.cloud                        apiserver           secure             passthrough          None
    openshift-ansible-service-broker   asb-1338            asb-1338-openshift-ansible-service-broker.<cluster_name>-<random_ID>.<region>.containers.appdomain.cloud            asb                 1338               reencrypt            None
    openshift-console                  console             console.<cluster_name>-<random_ID>.<region>.containers.appdomain.cloud                                              console             https              reencrypt/Redirect   None
    openshift-monitoring               alertmanager-main   alertmanager-main-openshift-monitoring.<cluster_name>-<random_ID>.<region>.containers.appdomain.cloud                alertmanager-main   web                reencrypt            None
    openshift-monitoring               grafana             grafana-openshift-monitoring.<cluster_name>-<random_ID>.<region>.containers.appdomain.cloud                          grafana             https              reencrypt            None
    openshift-monitoring               prometheus-k8s      prometheus-k8s-openshift-monitoring.<cluster_name>-<random_ID>.<region>.containers.appdomain.cloud                   prometheus-k8s      web                reencrypt
    ```
    {: screen}
3.  In your web browser, open the route that you want to access, for example: `https://grafana-openshift-monitoring.<cluster_name>-<random_ID>.<region>.containers.appdomain.cloud`. The first time that you access the host name, you might need to authenticate, such as by clicking **Log in with OpenShift** and authorizing access to your IAM identity.

<br>
Now you're in the built-in OpenShift app! For example, if you're in Grafana, you might check out your namespace CPU usage or other graphs. To access other built-in tools, open their route host names.

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
4.  Set up a route so that you can publicly access the hello world service. By default, the host name is in the format of `<service_name>-<namespace>.<cluster_name>-<random_ID>.<region>.containers.appdomain.cloud`. If you want to customize the host name, include the `--hostname=<hostname>` flag.
    1.  Create a route for the **hello-world** service.
        ```
        oc create route edge --service=hello-world -n hello-world
        ```
        {: pre}
    2.  Get the route host name address from the **Host/Port** output.
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
5.  Access your app.
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


## Lesson 4: Setting up LogDNA and Sysdig add-ons to monitor cluster health
{: #openshift_logdna_sysdig}

Because OpenShift sets up stricter [Security Context Constraints (SCC) ![External link icon](../icons/launch-glyph.svg "External link icon")](https://docs.openshift.com/container-platform/3.11/admin_guide/manage_scc.html) by default than native Kubernetes, you might find that some apps or cluster add-ons that you use on native Kubernetes cannot be deployed on OpenShift in the same way. In particular, many images require to run as a `root` user or as a privileged container, which is prevented in OpenShift by default. In this lesson, you learn how to modify the default SCCs by creating privileged security accounts and updating the `securityContext` in the pod specification to use two popular {{site.data.keyword.containerlong_notm}} add-ons: {{site.data.keyword.la_full_notm}} and {{site.data.keyword.mon_full_notm}}.
{: shortdesc}

Before you begin, log in to your cluster as an administrator.
1.  Open your OpenShift console at `https://<master_URL>/console`. For example, `https://c0.containers.cloud.ibm.com:23652/console`.
2.  From the OpenShift web console menu bar, click your profile **IAM#user.name@email.com > Copy Login Command** and paste the copied `oc` login command into your terminal to authenticate via the CLI.
3.  Download the admin configuration files for your cluster.
    ```
    ibmcloud ks cluster-config --cluster <cluster_name_or_ID> --admin
    ```
    {: pre}

    When the download of the configuration files is finished, a command is displayed that you can copy and paste to set the path to the local Kubernetes configuration file as an environment variable.

    Example for OS X:

    ```
    export KUBECONFIG=/Users/<user_name>/.bluemix/plugins/kubernetes-service/clusters/<cluster_name>/kube-config-<datacenter>-<cluster_name>.yml
    ```
    {: screen}
4.  Continue the lesson to set up [{{site.data.keyword.la_short}}](#openshift_logdna) and [{{site.data.keyword.mon_short}}](#openshift_sysdig).

### Lesson 4a: Setting up LogDNA
{: #openshift_logdna}

Set up a project and privileged service account for {{site.data.keyword.la_full_notm}}. Then, create a {{site.data.keyword.la_short}} instance in your {{site.data.keyword.cloud_notm}} account. To integrate your {{site.data.keyword.la_short}} instance with your OpenShift cluster, you must modify the daemon set that is deployed to use the privileged service account to run as root.
{: shortdesc}

1.  Set up the project and privileged service account for LogDNA.
    1.  As a cluster administrator, create a `logdna` project.
        ```
        oc adm new-project logdna
        ```
        {: pre}
    2.  Target the project so that the subsequent resources that you create are in the `logdna` project namespace.
        ```
        oc project logdna
        ```
        {: pre}
    3.  Create a service account for the `logdna` project.
        ```
        oc create serviceaccount logdna
        ```
        {: pre}
    4.  Add a privileged security context constraint to the service account for the `logdna` project.<p class="note">If you want to check what authorization the `privileged` SCC policy gives the service account, run `oc describe scc privileged`. For more information about SCCs, see the [OpenShift docs ![External link icon](../icons/launch-glyph.svg "External link icon")](https://docs.openshift.com/container-platform/3.11/admin_guide/manage_scc.html).</p>
        ```
        oc adm policy add-scc-to-user privileged -n logdna -z logdna
        ```
        {: pre}
2.  Create your {{site.data.keyword.la_full_notm}} instance in the same resource group as your cluster. Select a pricing plan that determines the retention period for your logs, such as `lite` which retains logs for 0 days. The region does not have to match the region of your cluster. For more information, see [Provisioning an instance](/docs/services/Log-Analysis-with-LogDNA/tutorials?topic=LogDNA-provision) and [Pricing plans](/docs/services/Log-Analysis-with-LogDNA?topic=LogDNA-about#overview_pricing_plans).
    ```
    ibmcloud resource service-instance-create <service_instance_name> logdna (lite|7-days|14-days|30-days) <region> [-g <resource_group>]
    ```
    {: pre}

    Example command:
    ```
    ibmcloud resource service-instance-create logdna-openshift logdna lite us-south
    ```
    {: pre}

    In the output, note the service instance **ID**, which is in the format `crn:v1:bluemix:public:logdna:<region>:<ID_string>::`.
    ```
    Service instance <name> was created.

    Name:         <name>   
    ID:           crn:v1:bluemix:public:logdna:<region>:<ID_string>::   
    GUID:         <guid>   
    Location:     <region>   
    ...
    ```
    {: screen}    
3.  Get your {{site.data.keyword.la_short}} instance ingestion key. The LogDNA ingestion key is used to open a secure web socket to the LogDNA ingestion server and to authenticate the logging agent with the {{site.data.keyword.la_short}} service.
    1.  Create a service key for your LogDNA instance.
        ```
        ibmcloud resource service-key-create <key_name> Administrator --instance-id <logdna_instance_ID>
        ```
        {: pre}
    2.  Note the **ingestion_key** of your service key.
        ```
        ibmcloud resource service-key <key_name>
        ```
        {: pre}

        Example output:
        ```
        Name:          <key_name>  
        ID:            crn:v1:bluemix:public:logdna:<region>:<ID_string>::    
        Created At:    Thu Jun  6 21:31:25 UTC 2019   
        State:         active   
        Credentials:                                   
                       apikey:                   <api_key_value>      
                       iam_apikey_description:   Auto-generated for key <ID>     
                       iam_apikey_name:          <key_name>       
                       iam_role_crn:             crn:v1:bluemix:public:iam::::role:Administrator      
                       iam_serviceid_crn:        crn:v1:bluemix:public:iam-identity::<ID_string>     
                       ingestion_key:            111a11aa1a1a11a1a11a1111aa1a1a11    
        ```
        {: screen}
4.  Create a Kubernetes secret to store your LogDNA ingestion key for your service instance.
    ```
     oc create secret generic logdna-agent-key --from-literal=logdna-agent-key=<logDNA_ingestion_key>
    ```
    {: pre}
5.  Create a Kubernetes daemon set to deploy the LogDNA agent on every worker node of your Kubernetes cluster. The LogDNA agent collects logs with the extension `*.log` and extensionless files that are stored in the `/var/log` directory of your pod. By default, logs are collected from all namespaces, including `kube-system`, and automatically forwarded to the {{site.data.keyword.la_short}} service.
    ```
    oc create -f https://assets.us-south.logging.cloud.ibm.com/clients/logdna-agent-ds.yaml
    ```
    {: pre}
6.  Edit the LogDNA agent daemon set configuration to refer to the service account that you previously created and to set the security context to privileged.
    1.  Download a local copy of the configuration file to edit.
        ```
        oc get ds logdna-agent -n logdna -o yaml > logdna-ds.yaml
        ```
        {: pre}
    2.  In the configuration file, add the following specifications.
        *   In `spec.template.spec`, add `serviceAccount: logdna`.
        *   In `spec.template.spec.containers`, add `securityContext: privileged: true`.
        *   If you created your {{site.data.keyword.la_short}} instance in a region other than `us-south`, update the `spec.template.spec.containers.env` environment variable values for the `LDAPIHOST` and `LDLOGHOST` with the `<region>`.

        Example:
        ```
        apiVersion: extensions/v1beta1
        kind: DaemonSet
        spec:
          ...
          template:
            ...
            spec:
              serviceAccount: logdna
              containers:
              - securityContext:
                  privileged: true
                ...
                env:
                - name: LOGDNA_AGENT_KEY
                  valueFrom:
                    secretKeyRef:
                      key: logdna-agent-key
                      name: logdna-agent-key
                - name: LDAPIHOST
                  value: api.<region>.logging.cloud.ibm.com
                - name: LDLOGHOST
                  value: logs.<region>.logging.cloud.ibm.com
              ...
        ```
        {: screen}
    3.  Save the configuration file and apply your changes.
        ```
        oc apply -f logdna-ds.yaml
        ```
        {: pre}
7.  Verify that the `logdna-agent` pod on each node is in a **Running** status.
    ```
    oc get pods
    ```
    {: pre}
8.  From the [{{site.data.keyword.cloud_notm}} Observability > Logging console](https://cloud.ibm.com/observe/logging), in the row for your {{site.data.keyword.la_short}} instance, click **View LogDNA**. The LogDNA dashboard opens. After a few minutes, your cluster's logs are displayed, and you can begin to analyze your logs.

For more information about how to use {{site.data.keyword.la_short}}, see the [Next steps docs](/docs/services/Log-Analysis-with-LogDNA?topic=LogDNA-kube#kube_next_steps).

### Lesson 4b: Setting up Sysdig
{: #openshift_sysdig}

Create an {{site.data.keyword.mon_full_notm}} instance in your {{site.data.keyword.cloud_notm}} account. To integrate your {{site.data.keyword.mon_short}} instance with your OpenShift cluster, you must run a script that creates a project and privileged service account for the Sysdig agent.
{: shortdesc}

1.  Create your {{site.data.keyword.mon_full_notm}} instance in the same resource group as your cluster. Select a pricing plan that determines the retention period for your logs, such as `lite`. The region does not have to match the region of your cluster. For more information, see [Provisioning an instance](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-provision).
    ```
    ibmcloud resource service-instance-create <service_instance_name> sysdig-monitor (lite|graduated-tier) <region> [-g <resource_group>]
    ```
    {: pre}

    Example command:
    ```
    ibmcloud resource service-instance-create sysdig-openshift sysdig-monitor lite us-south
    ```
    {: pre}

    In the output, note the service instance **ID**, which is in the format `crn:v1:bluemix:public:logdna:<region>:<ID_string>::`.
    ```
    Service instance <name> was created.

    Name:         <name>   
    ID:           crn:v1:bluemix:public:sysdig-monitor:<region>:<ID_string>::   
    GUID:         <guid>   
    Location:     <region>   
    ...
    ```
    {: screen}    
2.  Get your {{site.data.keyword.mon_short}} instance access key. The Sysdig access key is used to open a secure web socket to the Sysdig ingestion server and to authenticate the monitoring agent with the {{site.data.keyword.mon_short}} service.
    1.  Create a service key for your Sysdig instance.
        ```
        ibmcloud resource service-key-create <key_name> Administrator --instance-id <sysdig_instance_ID>
        ```
        {: pre}
    2.  Note the **Sysdig Access Key** and **Sysdig Collector Endpoint** of your service key.
        ```
        ibmcloud resource service-key <key_name>
        ```
        {: pre}

        Example output:
        ```
        Name:          <key_name>  
        ID:            crn:v1:bluemix:public:sysdig-monitor:<region>:<ID_string>::    
        Created At:    Thu Jun  6 21:31:25 UTC 2019   
        State:         active   
        Credentials:                                   
                       Sysdig Access Key:           11a1aa11-aa1a-1a1a-a111-11a11aa1aa11      
                       Sysdig Collector Endpoint:   ingest.<region>.monitoring.cloud.ibm.com      
                       Sysdig Customer Id:          11111      
                       Sysdig Endpoint:             https://<region>.monitoring.cloud.ibm.com  
                       apikey:                   <api_key_value>      
                       iam_apikey_description:   Auto-generated for key <ID>     
                       iam_apikey_name:          <key_name>       
                       iam_role_crn:             crn:v1:bluemix:public:iam::::role:Administrator      
                       iam_serviceid_crn:        crn:v1:bluemix:public:iam-identity::<ID_string>       
        ```
        {: screen}
3.  Run the script to set up an `ibm-observe` project with a privileged service account and a Kubernetes daemon set to deploy the Sysdig agent on every worker node of your Kubernetes cluster. The Sysdig agent collects metrics such as the worker node CPU usage, worker node memory usage, HTTP traffic to and from your containers, and data about several infrastructure components.

    In the following command, replace <code><sysdig_access_key></code> and <code><sysdig_collector_endpoint></code> with the values from the service key that you created earlier. For <code>&lt;tag&gt;</code>, you can associate tags with your Sysdig agent, such as `role:service,location:us-south` to help you identify the environment that the metrics come from.

    ```
    curl -sL https://ibm.biz/install-sysdig-k8s-agent | bash -s -- -a <sysdig_access_key> -c <sysdig_collector_endpoint> -t <tag> -ac 'sysdig_capture_enabled: false' --openshift
    ```
    {: pre}

    Example output:
    ```
    * Detecting operating system
    * Downloading Sysdig cluster role yaml
    * Downloading Sysdig config map yaml
    * Downloading Sysdig daemonset v2 yaml
    * Creating project: ibm-observe
    * Creating sysdig-agent serviceaccount in project: ibm-observe
    * Creating sysdig-agent access policies
    * Creating sysdig-agent secret using the ACCESS_KEY provided
    * Retreiving the IKS Cluster ID and Cluster Name
    * Setting cluster name as <cluster_name>
    * Setting ibm.containers-kubernetes.cluster.id 1fbd0c2ab7dd4c9bb1f2c2f7b36f5c47
    * Updating agent configmap and applying to cluster
    * Setting tags
    * Setting collector endpoint
    * Adding additional configuration to dragent.yaml
    * Enabling Prometheus
    configmap/sysdig-agent created
    * Deploying the sysdig agent
    daemonset.extensions/sysdig-agent created
    ```
    {: screen}

4.  Verify that the `sydig-agent` pods on each node show that **1/1** pods are ready and that each pod has a **Running** status.
    ```
    oc get pods
    ```
    {: pre}

    Example output:
    ```
    NAME                 READY     STATUS    RESTARTS   AGE
    sysdig-agent-qrbcq   1/1       Running   0          1m
    sysdig-agent-rhrgz   1/1       Running   0          1m
    ```
    {: screen}
5.  From the [{{site.data.keyword.cloud_notm}} Observability > Monitoring console](https://cloud.ibm.com/observe/logging), in the row for your {{site.data.keyword.mon_short}} instance, click **View Sysdig**. The Sysdig dashboard opens, and you can begin to analyze your cluster metrics.

For more information about how to use {{site.data.keyword.mon_short}}, see the [Next steps docs](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-kubernetes_cluster#kubernetes_cluster_next_steps).

### Optional: Cleaning up
{: #openshift_logdna_sysdig_cleanup}

Remove the {{site.data.keyword.la_short}} and {{site.data.keyword.mon_short}} instances from your cluster and {{site.data.keyword.cloud_notm}} account. Note that unless you store the logs and metrics in [persistent storage](/docs/services/Log-Analysis-with-LogDNA?topic=LogDNA-archiving), you cannot access this information after you delete the instances from your account.
{: shortdesc}

1.  Clean up the {{site.data.keyword.la_short}} and {{site.data.keyword.mon_short}} instances in your cluster by removing the projects that you created for them. When you delete a project, its resources such as service accounts and daemon sets are also removed.
    ```
    oc delete project logdna
    ```
    {: pre}
    ```
    oc delete project ibm-observe
    ```
    {: pre}
2.  Remove the instances from your {{site.data.keyword.cloud_notm}} account.
    *   [Removing a {{site.data.keyword.la_short}} instance](/docs/services/Log-Analysis-with-LogDNA?topic=LogDNA-remove).
    *   [Removing a {{site.data.keyword.mon_short}} instance](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-remove).

<br />


## What's next?
{: #openshift_next}

For more information about working with your apps and routing services, see the [OpenShift Developer Guide](https://docs.openshift.com/container-platform/3.11/dev_guide/index.html).

Install LogDNA & Sysdig.


