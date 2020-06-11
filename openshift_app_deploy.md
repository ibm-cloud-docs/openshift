---

copyright:
  years: 2014, 2020
lastupdated: "2020-06-11"

keywords: kubernetes, openshift, roks, rhoks, rhos

subcollection: openshift

---

{:beta: .beta}
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



# Deploying apps in OpenShift clusters
{: #deploy_app}

With {{site.data.keyword.openshiftlong}} clusters, you can deploy apps from a remote file or repository such as GitHub with a single command. Also, your clusters come with various built-in services that you can use to help operate your cluster.
{: shortdesc}

## Moving your apps to OpenShift
{: #openshift_move_apps}

To create an app in your Red Hat OpenShift on IBM Cloud cluster, you can use the OpenShift console or CLI.
{: shortdesc}

Seeing errors when you deploy your app? OpenShift has different default settings than community Kubernetes, such as stricter security context constraints. Review the [common scenarios where you might need to modify your apps](/docs/openshift?topic=openshift-plan_deploy#openshift_move_apps_scenarios) so that you can deploy them on OpenShift clusters.
{: tip}

### Deploying apps through the console
{: #deploy_apps_ui}

You can create apps through various methods in the OpenShift console by using the **Developer** perspective. For more information, see the [OpenShift documentation](http://docs.openshift.com/container-platform/4.2/applications/application_life_cycle_management/odc-creating-applications-using-developer-perspective.html){: external}.
{: shortdesc}

1.  From the [Cluster](https://cloud.ibm.com/kubernetes/clusters?platformType=openshift) page, select your cluster.
2.  Click **OpenShift web console**.
3.  From the perspective switcher, select **Developer**. The OpenShift web console switches to the Developer perspective, and the menu now offers items such as **+Add**, **Topology**, and **Builds**.
4.  Click **+Add**.
5.  In the **Add** pane menu bar, select the **Project** that you want to create your app in from the drop-down list.
6.  Click the method that you want to use to add your app, and follow the instructions. For example, click **From Git**.

### Deploying apps through the CLI
{: #deploy_apps_cli}

To create an app in your Red Hat OpenShift on IBM Cloud cluster, use the `oc new-app` [command](https://docs.openshift.com/container-platform/4.2/cli_reference/openshift_cli/developer-cli-commands.html#new-app){: external}. For example, you might refer to a public GitHub repo, a public GitLab repo with a URL that ends in `.git`, or another local or remote repo. For more information, [try out the tutorial](/docs/openshift?topic=openshift-openshift_tutorial#openshift_deploy_app) and review the [OpenShift documentation](http://docs.openshift.com/container-platform/4.2/applications/application_life_cycle_management/creating-applications-using-cli.html){: external}.
{: shortdesc}

```
oc new-app --name <app_name> https://github.com/<path_to_app_repo> [--context-dir=<subdirectory>]
```
{: pre}

**What does the `new-app` command do?**<br>
The `new-app` command creates a build configuration and app image from the source code, a deployment configuration to deploy the container to pods in your cluster, and a service to expose the app within the cluster. For more information about the build process and other sources besides Git, see the [OpenShift documentation](http://docs.openshift.com/container-platform/4.3/applications/application_life_cycle_management/creating-applications-using-cli.html){: external}.

<br />


## Deploying apps to specific worker nodes by using labels
{: #node_affinity}

When you deploy an app, the app pods indiscriminately deploy to various worker nodes in your cluster. In some cases, you might want to restrict the worker nodes that the app pods to deploy to. For example, you might want app pods to deploy to only worker nodes in a certain worker pool because those worker nodes are on bare metal machines. To designate the worker nodes that app pods must deploy to, add an affinity rule to your app deployment.
{:shortdesc}

Before you begin:
*   [Access your OpenShift cluster](/docs/openshift?topic=openshift-access_cluster).
*   Make sure that you are assigned a [service role](/docs/openshift?topic=openshift-users#platform) that grants the appropriate Kubernetes RBAC role so that you can work with Kubernetes resources in the OpenShift project.
*  **Optional**: [Set a label for the worker pool](/docs/openshift?topic=openshift-add_workers#worker_pool_labels) that you want to run the app on.

To deploy apps to specific worker nodes:

1.  Get the ID of the worker pool that you want to deploy app pods to.
    ```
    ibmcloud oc worker-pool ls --cluster <cluster_name_or_ID>
    ```
    {: pre}

2.  List the worker nodes that are in the worker pool, and note one of the **Private IP** addresses.
    ```
    ibmcloud oc worker ls --cluster <cluster_name_or_ID> --worker-pool <worker_pool_name_or_ID>
    ```
    {: pre}

3.  Describe the worker node. In the **Labels** output, note the worker pool ID label, `ibm-cloud.kubernetes.io/worker-pool-id`.

    <p class="tip">The steps in this topic use a worker pool ID to deploy app pods only to worker nodes within that worker pool. To deploy app pods to specific worker nodes by using a different label, note this label instead. For example, to deploy app pods only to worker nodes on a specific private VLAN, use the `privateVLAN=` label.</p>

    ```
    oc describe node <worker_node_private_IP>
    ```
    {: pre}

    Example output:
    ```
    Name:               10.xxx.xx.xxx
    Roles:              <none>
    Labels:             arch=amd64
                        beta.kubernetes.io/arch=amd64
                        beta.kubernetes.io/instance-type=b3c.4x16.encrypted
                        beta.kubernetes.io/os=linux
                        failure-domain.beta.kubernetes.io/region=us-south
                        failure-domain.beta.kubernetes.io/zone=dal10
                        ibm-cloud.kubernetes.io/encrypted-docker-data=true
                        ibm-cloud.kubernetes.io/ha-worker=true
                        ibm-cloud.kubernetes.io/iaas-provider=softlayer
                        ibm-cloud.kubernetes.io/machine-type=b3c.4x16.encrypted
                        ibm-cloud.kubernetes.io/sgx-enabled=false
                        ibm-cloud.kubernetes.io/worker-pool-id=00a11aa1a11aa11a1111a1111aaa11aa-11a11a
                        ibm-cloud.kubernetes.io/worker-version=1.17.6_1534
                        kubernetes.io/hostname=10.xxx.xx.xxx
                        privateVLAN=1234567
                        publicVLAN=7654321
    Annotations:        node.alpha.kubernetes.io/ttl=0
    ...
    ```
    {: screen}

4. [Add an affinity rule](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/){: external} for the worker pool ID label to the app deployment.

    Example YAML:

    ```yaml
    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: with-node-affinity
    spec:
      template:
        spec:
          affinity:
            nodeAffinity:
              requiredDuringSchedulingIgnoredDuringExecution:
                nodeSelectorTerms:
                - matchExpressions:
                  - key: ibm-cloud.kubernetes.io/worker-pool-id
                    operator: In
                    values:
                    - <worker_pool_ID>
    ...
    ```
    {: codeblock}

    In the **affinity** section of the example YAML, `ibm-cloud.kubernetes.io/worker-pool-id` is the `key` and `<worker_pool_ID>` is the `value`.

5. Apply the updated deployment configuration file.
    ```
    oc apply -f with-node-affinity.yaml
    ```
    {: pre}

6. Verify that the app pods deployed to the correct worker nodes.

    1. List the pods in your cluster.
        ```
        oc get pods -o wide
        ```
        {: pre}

        Example output:
        ```
        NAME                   READY     STATUS              RESTARTS   AGE       IP               NODE
        cf-py-d7b7d94db-vp8pq  1/1       Running             0          15d       172.30.xxx.xxx   10.176.48.78
        ```
        {: screen}

    2. In the output, identify a pod for your app. Note the **NODE** private IP address of the worker node that the pod is on.

        In the previous example output, the app pod `cf-py-d7b7d94db-vp8pq` is on a worker node with the IP address `10.xxx.xx.xxx`.

    3. List the worker nodes in the worker pool that you designated in your app deployment.

        ```
        ibmcloud oc worker ls --cluster <cluster_name_or_ID> --worker-pool <worker_pool_name_or_ID>
        ```
        {: pre}

        Example output:

        ```
        ID                                                 Public IP       Private IP     Machine Type      State    Status  Zone    Version
        kube-dal10-crb20b637238bb471f8b4b8b881bbb4962-w7   169.xx.xxx.xxx  10.176.48.78   b3c.4x16          normal   Ready   dal10   1.8.6_1504
        kube-dal10-crb20b637238bb471f8b4b8b881bbb4962-w8   169.xx.xxx.xxx  10.176.48.83   b3c.4x16          normal   Ready   dal10   1.8.6_1504
        kube-dal12-crb20b637238bb471f8b4b8b881bbb4962-w9   169.xx.xxx.xxx  10.176.48.69   b3c.4x16          normal   Ready   dal12   1.8.6_1504
        ```
        {: screen}

        If you created an app affinity rule based on another factor, get that value instead. For example, to verify that the app pod deployed to a worker node on a specific VLAN, view the VLAN that the worker node is on by running `ibmcloud oc worker get --cluster <cluster_name_or_ID> --worker <worker_ID>`.
        {: tip}

    4. In the output, verify that the worker node with the private IP address that you identified in the previous step is deployed in this worker pool.

<br />





<br />


## Deploying Cloud Paks, licensed software, and other integrations
{: #openshift_app_cloud_paks}

You can deploy IBM Cloud Paks&trade;, licensed software, and other 3rd party integrations to Red Hat OpenShift on IBM Cloud clusters. You have various tools to deploy integrations, such as {{site.data.keyword.cloud_notm}} service binding, managed add-ons, Helm charts, and more. After you install an integration, follow that product's documentation for configuration settings and other instructions to integrate with your apps. For more information, see [Enhancing cluster capabilities with integrations](/docs/openshift?topic=openshift-supported_integrations).
{: shortdesc}

<br />


## Accessing the OpenShift web console
{: #openshift_console}

You can use the OpenShift console to manage your apps, deploy apps from the catalog, and access built-in functionality to help you operate your cluster. The OpenShift console is deployed to your cluster by default, instead of the Kubernetes dashboard as in community Kubernetes clusters.
{: shortdesc}

For more information about the console, see the [OpenShift documentation](http://docs.openshift.com/container-platform/4.3/applications/application_life_cycle_management/odc-creating-applications-using-developer-perspective.html){: external}.

1.  From the [Red Hat OpenShift on IBM Cloud console](https://cloud.ibm.com/kubernetes/clusters?platformType=openshift){: external}, select your OpenShift cluster, then click **OpenShift web console**.
2.  Explore the different areas of the OpenShift web console, as described in the following tabbed table.

    <table class="simple-tab-table" id="console1" tab-title="OCP 4" tab-group="console-version" aria-describedby="tableSummary-19ecbef4c01853826b42de82471b9035">
    <caption caption-side="top">
      <img src="images/icon-version-43.png" alt="Version 4.3 icon" width="30" style="width:30px; border-style: none"/> OpenShift console overview<br>
      <span class="table-summary" id="tableSummary-19ecbef4c01853826b42de82471b9035">The rows are read from left to right. The area of the console is in the first column, the location in the console is in the second column, and the description of the console area in the third column. You can change between OpenShift console versions by toggling the tabs at the beginning of the table.</span>
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
    <td>From the Administrator perspective, you can manage and set up the components that your team needs to run your apps, such as projects for your workloads, networking, and operators for integrating IBM, Red Hat, 3rd party, and custom services into the cluster. For more information, see [Viewing cluster information](http://docs.openshift.com/container-platform/4.2/web_console/using-dashboard-to-get-cluster-information.html){: external} in the OpenShift documentation.</td>
    </tr>
    <tr>
    <td>Developer perspective</td>
    <td>Side navigation menu perspective switcher.</td>
    <td>From the Developer perspective, you can add apps to your cluster in a variety of ways, such as from Git repositories,container images, drag-and-drop or uploaded YAML files, operator catalogs, and more. The **Topology** view presents a unique way to visualize the workloads that run in a project and navigate their components from sidebars that aggregate related resources, including pods, services, routes, and metadata. For more information, see [Developer perspective](http://docs.openshift.com/container-platform/4.2/web_console/odc-about-developer-perspective.html){: external} in the OpenShift documentation.</td>
    </tr>
    </tbody>
    </table>
    <table class="simple-tab-table" id="console2" tab-title="OCP 3" tab-group="console-version" aria-describedby="tableSummary-a4edc48da30a2a6943cabb6b3a128df4">
    <caption caption-side="top">
      <img src="images/icon-version-311.png" alt="Version 3.11 icon" width="30" style="width:30px; border-style: none"/> OpenShift console overview<br>
      <span class="table-summary" id="tableSummary-a4edc48da30a2a6943cabb6b3a128df4">The rows are read from left to right. The area of the console is in the first column, the location in the console is in the second column, and the description of the console area in the third column. You can change between OpenShift console versions by toggling the tabs at the beginning of the table.</span>
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
    <td>Browse the catalog of built-in services that you can deploy on OpenShift. For example, if you already have a `node.js` app that is hosted on GitHub, you can click the **Languages** tab and deploy a **JavaScript** app. The **My Projects** pane provides a quick view of all the projects that you have access to, and clicking on a project takes you to the Application Console. For more information, see the [OpenShift Web Console Walkthrough](https://docs.openshift.com/container-platform/3.11/getting_started/developers_console.html){: external} in the OpenShift documentation.</td>
    </tr>
    <tr>
    <td>Application Console</td>
    <td>Dropdown menu in the **OpenShift Container Platform** menu bar.</td>
    <td>For each project that you have access to, you can manage your OpenShift resources such as pods, services, routes, builds, images or persistent volume claims. You can also view and analyze logs for these resources, or add services from the catalog to the project. For more information, see the [OpenShift Web Console Walkthrough](https://docs.openshift.com/container-platform/3.11/getting_started/developers_console.html){: external} in the OpenShift documentation.</td>
    </tr>
    <tr>
    <td>Cluster Console</td>
    <td>Dropdown menu in the **OpenShift Container Platform** menu bar.</td>
    <td>For cluster-wide administrators across all the projects in the cluster, you can manage projects, service accounts,RBAC roles, role bindings, and resource quotas. You can also see the status and events for resources within the cluster in a combined view. For more information, see the [OpenShift Web Console Walkthrough](https://docs.openshift.com/container-platform/3.11/getting_started/developers_console.html){: external} in the OpenShift documentation.</td>
    </tr>
    </tbody>
    </table><p></p>
3.  To work with your cluster in the CLI, click your profile **IAM#user.name@email.com > Copy Login Command**. Display and copy the `oc login` token command into your terminal to authenticate via the CLI.


<br />


## Accessing built-in OpenShift services
{: #openshift_access_oc_services}

Red Hat OpenShift on IBM Cloud comes with built-in services that you can use to help operate your cluster, such as the OpenShift console, Prometheus, and Grafana. You can access these services by using the local host of a [route](https://docs.openshift.com/container-platform/4.3/networking/routes/route-configuration.html){: external}. The default route domain names follow a cluster-specific pattern of `<service_name>-<namespace>.<cluster_name>-<random_ID>.<region>.containers.appdomain.cloud`.
{:shortdesc}

<img src="images/icon-version-311.png" alt="Version 3.11 icon" width="30" style="width:30px; border-style: none"/> This topic is specific to OpenShift version 3.11.
{: note}

You can access the built-in OpenShift service routes from the [console](#openshift_services_console) or [CLI](#openshift_services_cli). You might want to use the console to navigate through Kubernetes resources in one project. By using the CLI, you can list resources such as routes across projects.

### Accessing built-in OpenShift services from the console
{: #openshift_services_console}
1.  From the OpenShift web console, in the dropdown menu in the OpenShift container platform menu bar, click **Application Console**.
2.  Select the **default** project, then in the navigation pane, click **Applications > Pods**.
3.  Verify that the **router** pods are in a **Running** status. The router functions as the ingress point for external network traffic. You can use the router to publicly expose the services in your cluster on the router's external IP address by using a route. The router listens on the public host network interface, unlike your app pods that listen only on private IPs. The router proxies external requests for route hostnames that you associate with services. Requests are sent to the IPs of the app pods that are identified by the service.
4.  From the **default** project navigation pane, click **Applications > Deployments** and then click the **registry-console** deployment. Your OpenShift cluster comes with an internal registry that you can use to manage local images for your deployments. To view your images, click **Applications > Routes** and open the registry console **Hostname** URL.
5.  In the OpenShift container platform menu bar, from the dropdown menu, click **Cluster Console**.
6.  From the navigation pane, expand **Monitoring**.
7.  Click the built-in monitoring tool that you want to access, such as **Dashboards**. The Grafana route opens in the following format: `https://grafana-openshift-monitoring.<cluster_name>-<random_ID>.<region>.containers.appdomain.cloud`.<p class="note">The first time that you access the hostname, you might need to authenticate, such as by clicking **Log in with OpenShift** and authorizing access to your IAM identity.</p>

### Accessing built-in OpenShift services from the CLI
{: #openshift_services_cli}

1.  From the **Application Console** or **Service Console** view in the OpenShift  web console, click your profile **IAM#user.name@email.com > Copy Login Command** and paste the login command into your terminal to authenticate.
    ```
    oc login https://c1-e.<region>.containers.cloud.ibm.com:<port> --token=<access_token>
    ```
    {: pre}
2.  Verify that your router is deployed. The router functions as the ingress point for external network traffic. You can use the router to publicly expose the services in your cluster on the router's external IP address by using a route. The router listens on the public host network interface, unlike your app pods that listen only on private IPs. The router proxies external requests for route hostnames that you associate with services. Requests are sent to the IPs of the app pods that are identified by the service.
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
2.  Get the **Host/Port** hostname of the service route that you want to access. For example, you might want to access your Grafana dashboard to check metrics on your cluster's resource usage. The default route domain names follow a cluster-specific pattern of `<service_name>-<namespace>.<cluster_name>-<random_ID>.<region>.containers.appdomain.cloud`.
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
3.  In your web browser, open the route that you want to access, for example: `https://grafana-openshift-monitoring.<cluster_name>-<random_ID>.<region>.containers.appdomain.cloud`. The first time that you access the hostname, you might need to authenticate, such as by clicking **Log in with OpenShift** and authorizing access to your IAM identity.

<br>
Now you're in the built-in OpenShift app! For example, if you're in Grafana, you might check out your namespace CPU usage or other graphs. To access other built-in tools, open their route hostnames.

