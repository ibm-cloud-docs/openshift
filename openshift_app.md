---

copyright:
  years: 2014, 2019
lastupdated: "2019-09-12"

keywords: kubernetes, openshift, roks, rhoks, rhos

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

# Deploying apps in OpenShift clusters
{: #openshift_apps}

With {{site.data.keyword.openshiftlong}} clusters, you can deploy apps from a remote file or repository such as GitHub with a single command. Also, your clusters come with various built-in services that you can use to help operate your cluster.
{: shortdesc}

## Moving your apps to OpenShift
{: #openshift_move_apps}

To create a new app in your Red Hat OpenShift on IBM Cloud cluster, use the `oc new-app` [command ![External link icon](../icons/launch-glyph.svg "External link icon")](https://docs.openshift.com/container-platform/3.11/cli_reference/basic_cli_operations.html#new-app). For more information, [try out the tutorial](/docs/openshift?topic=openshift-openshift_tutorial#openshift_deploy_app) and review the [OpenShift documentation ![External link icon](../icons/launch-glyph.svg "External link icon")](https://docs.openshift.com/container-platform/3.11/getting_started/developers_cli.html).
{: shortdesc}

```
oc new-app --name <app_name> https://github.com/<path_to_app_repo> [--context-dir=<subdirectory>]
```
{: pre}

**What does the `new-app` command do?**<br>
The `new-app` command creates a build configuration and app image from the source code, a deployment configuration to deploy the container to pods in your cluster, and a service to expose the app within the cluster. For more information about the build process and other sources besides Git, see the [OpenShift documentation ![External link icon](../icons/launch-glyph.svg "External link icon")](https://docs.openshift.com/container-platform/3.11/dev_guide/application_lifecycle/new_app.html#dev-guide-new-app).

<br />


## Common app modification scenarios
{: openshift_move_apps_scenarios}

OpenShift has different default settings than community Kubernetes, such as stricter security context constraints. Review the following common scenarios where you might need to modify your apps so that you can deploy them on OpenShift clusters.
{: shortdesc}

<table summary="The first column describes an app scenario. The second column explains the steps that you can take to address the app scenario.">
<caption>Common scenarios that require app modifications</caption>
<thead>
<tr>
<th>Scenario</th>
<th>Steps you can take</th>
</tr>
</thead>
<tbody>
<tr>
<td>Your app runs as root. You might see the pods fail with a `CrashLoopBackOff` status</td>
<td>The pod requires privileged access. See [Example steps for giving a deployment privileged access](#openshift_move_apps_example_scc). For more information, see the OpenShift documentation for [Managing Security Context Constraints (SCC) ![External link icon](../icons/launch-glyph.svg "External link icon")](https://docs.openshift.com/container-platform/3.11/admin_guide/manage_scc.html).</td>
</tr>
<tr>
<td>Your apps are designed to run on Docker. These apps are often logging and monitoring tools that rely on the container runtime engine, call the container runtime API directly, and access container log directories.</td>
<td>In OpenShift, your image must be compatible to run with the CRI-O container runtime. For more information, see [Using the CRI-O Container Engine ![External link icon](../icons/launch-glyph.svg "External link icon")](https://docs.openshift.com/container-platform/3.11/crio/crio_runtime.html).</td>
</tr>
<tr>
<td>You deploy your app by using Helm. You might see an error similar to `User "system:serviceaccount:tiller:tiller" cannot create <resource>.rbac.authorization.k8s.io: RBAC: <resource>.rbac.authorization.k8s.io "<resource>.rbac.authorization.k8s.io" not found`</td>
<td>Make sure that you [set up Tiller](/docs/containers?topic=containers-helm#public_helm_install) with a privileged security account.</td>
</tr>
<tr>
<td>Your app uses persistent file storage with a non-root user ID that cannot write to the mounted storage device.</td>
<td>[Adjust the security context](/docs/containers?topic=containers-cs_troubleshoot_storage#cs_storage_nonroot) for the app deployment so that `runAsUser` is set to `0`.</td>
</tr>
<tr>
<td>Your service is exposed on port 80 or another port less than 1024. You might see a `Permission denied` error.</td>
<td>Ports less than 1024 are privileged ports that are reserved for start-up processes. You might choose one of the following solutions:<ul>
<li>Change the port to 8080 or a similar port greater than 1024, and update your containers to listen on this port.</li>
<li>Add your container deployment to a privileged service account, such as in the [example for giving a deployment priviliged access](#openshift_move_apps_example_scc).</li>
<li>Set up your container to listen on any network port, then update the container runtime to map that port to port 80 on the host by using [port forwarding ![External link icon](../icons/launch-glyph.svg "External link icon")](https://docs.openshift.com/container-platform/3.11/dev_guide/port_forwarding.html).</li></ul></td>
</tr>
<tr>
<td>Other use cases and scenarios</td>
<td>Review the [OpenShift documentation ![External link icon](../icons/launch-glyph.svg "External link icon")](https://docs.openshift.com/container-platform/3.11/dev_guide/migrating_applications/index.html) for migrating databases, web framework apps, CI/CD, and other examples.</td>
</tr>
</table>

### Example steps for giving a deployment privileged access
{: #openshift_move_apps_example_scc}

If you have an app that runs with root permisisons, you must modify your deployment to work with the [security context constraints](/docs/openshift?topic=openshift-openshift_scc) that are set for your OpenShift cluster. For example, you might set up your project with a service account to control privilaged access, and then modify your deployment to use this service account.
{: shortdesc}

Before you begin: [Access your OpenShift cluster](/docs/openshift?topic=openshift-openshift_access_cluster).

1.  As a cluster administrator, create a project.
    ```
    oc adm new-project <project_name>
    ```
    {: pre}
2.  Target the project so that the subsequent resources that you create are in the project namespace.
    ```
    oc project <project_name>
    ```
    {: pre}
3.  Create a service account for the project.
    ```
    oc create serviceaccount <sa_name>
    ```
    {: pre}
4.  Add a privileged security context constraint to the service account for the project.<p class="note">If you want to check what policies are included in the `privileged` SCC, run `oc describe scc privileged`. For more information about SCCs, see the [OpenShift documentation ![External link icon](../icons/launch-glyph.svg "External link icon")](https://docs.openshift.com/container-platform/3.11/admin_guide/manage_scc.html).</p>
    ```
    oc adm policy add-scc-to-user privileged -n <project_name> -z <sa_name>
    ```
    {: pre}
5.  In your deployment configuration file, refer to the privileged service account and set the security context to privileged.
    *   In `spec.template.spec`, add `serviceAccount: <sa_name>`.
    *   In `spec.template.spec.containers`, add `securityContext: privileged: true`.

    Example:
    ```
    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: myapp_deployment
      labels:
        app: myapp
    spec:
      ...
      template:
        ...
        spec:
          serviceAccount: <sa_name>
          containers:
          - securityContext:
              privileged: true
          ...
    ```
    {: screen}
6.  Deploy your app configuration file.
    ```
    oc apply -f <filepath/deployment.yaml>
    ```
    {: pre}
7.  Verify that the pod is in a **Running** status. If your pod shows an error status or is stuck in one status for a long time, describe the pod and review the **Events** section to start troubleshooting your deployment.
    ```
    oc get pods
    ```
    {: pre}

<br />


## Deploying Cloud Paks, licensed software, and other integrations
{: #openshift_app_cloud_paks}

You can deploy IBM Cloud Paks&trade;, licensed software, and other 3rd party integrations to Red Hat OpenShift on IBM Cloud clusters. You have various tools to deploy integrations, such as {{site.data.keyword.cloud_notm}} service binding, managed add-ons, Helm charts, and more. After you install an integration, follow that product's documentation for configuration settings and other instructions to integrate with your apps. For more information, see [Enhancing cluster capabilities with integrations](/docs/openshift?topic=openshift-openshift_integrations).
{: shortdesc}

<br />


## Accessing the OpenShift web console
{: #openshift_console}

You can use the OpenShift console to manage your apps, deploy apps from the catalog, and access built-in functionality to help you operate your cluster. The OpenShift console is deployed to your cluster by default, instead of the Kubernetes dashboard as in community Kubernetes clusters.
{: shortdesc}

For a quick walk-through of the console, see the [tutorial](/docs/openshift?topic=openshift-openshift_tutorial#openshift_oc_console).

For more information about the console, see the [OpenShift documentation ![External link icon](../icons/launch-glyph.svg "External link icon")](https://docs.openshift.com/container-platform/3.11/getting_started/developers_console.html).

<br />


## Accessing built-in OpenShift services
{: #openshift_access_oc_services}

Red Hat OpenShift on IBM Cloud comes with built-in services that you can use to help operate your cluster, such as the OpenShift console, Prometheus, and Grafana. You can access these services by using the local host of a [route ![External link icon](../icons/launch-glyph.svg "External link icon")](https://docs.openshift.com/container-platform/3.11/architecture/networking/routes.html). The default route domain names follow a cluster-specific pattern of `<service_name>-<namespace>.<cluster_name>-<random_ID>.<region>.containers.appdomain.cloud`.
{:shortdesc}

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
