---

copyright:
  years: 2014, 2020
lastupdated: "2020-02-10"

keywords: kubernetes, openshift, roks, rhoks, rhos

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


# Deploying apps in OpenShift clusters
{: #openshift_apps}

With {{site.data.keyword.openshiftlong}} clusters, you can deploy apps from a remote file or repository such as GitHub with a single command. Also, your clusters come with various built-in services that you can use to help operate your cluster.
{: shortdesc}

## Moving your apps to OpenShift
{: #openshift_move_apps}


To create an app in your Red Hat OpenShift on IBM Cloud cluster, you can use the OpenShift console or CLI.
{: shortdesc}

### Deploying apps through the console
{: #deploy_apps_ui}

You can create apps through various methods in the OpenShift console by using the **Developer** perspective. For more information, see the [OpenShift documentation](https://docs.openshift.com/container-platform/4.2/applications/application-life-cycle-management/odc-creating-applications-using-developer-perspective.html){: external}.
{: shortdesc}

1.  From the [Cluster](https://cloud.ibm.com/kubernetes/clusters?platformType=openshift) page, select your cluster.
2.  Click **OpenShift web console**.
3.  From the perspective switcher, select **Developer**. The OpenShift web console switches to the Developer perspective, and the menu now offers items such as **+Add**, **Topology**, and **Builds**.
4.  Click **+Add**.
5.  In the **Add** pane menu bar, select the **Project** that you want to create your app in from the drop-down list.
6.  Click the method that you want to use to add your app, and follow the instructions. For example, click **From Git**.

### Deploying apps through the CLI
{: #deploy_apps_cli}

To create an app in your Red Hat OpenShift on IBM Cloud cluster, use the `oc new-app` [command](https://docs.openshift.com/container-platform/4.3/cli_reference/openshift_cli/developer-cli-commands.html#new-app){: external}. For more information, [try out the tutorial](/docs/openshift?topic=openshift-openshift_tutorial#openshift_deploy_app) and review the [OpenShift documentation](https://docs.openshift.com/container-platform/4.3/applications/application-life-cycle-management/creating-applications-using-cli.html){: external}.
{: shortdesc}


```
oc new-app --name <app_name> https://github.com/<path_to_app_repo> [--context-dir=<subdirectory>]
```
{: pre}

**What does the `new-app` command do?**<br>
The `new-app` command creates a build configuration and app image from the source code, a deployment configuration to deploy the container to pods in your cluster, and a service to expose the app within the cluster. For more information about the build process and other sources besides Git, see the [OpenShift documentation](https://docs.openshift.com/container-platform/4.3/applications/application-life-cycle-management/creating-applications-using-cli.html){: external}.

<br />


## Common app modification scenarios
{: openshift_move_apps_scenarios}
{: help}
{: support}

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
<td>The pod requires privileged access. See [Example steps for giving a deployment privileged access](#openshift_move_apps_example_scc). For more information, see the OpenShift documentation for [Managing Security Context Constraints (SCC) ![External link icon](../icons/launch-glyph.svg "External link icon")](https://docs.openshift.com/container-platform/4.3/authentication/managing-security-context-constraints.html).</td>
</tr>
<tr>
<td>Your apps are designed to run on Docker. These apps are often logging and monitoring tools that rely on the container runtime engine, call the container runtime API directly, and access container log directories.</td>
<td>In OpenShift, your image must be compatible to run with the CRI-O container runtime. For more information, see [Using the CRI-O Container Engine ![External link icon](../icons/launch-glyph.svg "External link icon")](https://docs.openshift.com/container-platform/3.11/crio/crio_runtime.html).</td>
</tr>
<tr>
<td>You deploy your app by using Helm. You might see an error similar to `User "system:serviceaccount:tiller:tiller" cannot create <resource>.rbac.authorization.k8s.io: RBAC: <resource>.rbac.authorization.k8s.io "<resource>.rbac.authorization.k8s.io" not found`</td>
<td>Make sure that you [set up Tiller](/docs/containers?topic=containers-helm#public_helm_install) with a privileged security account. Note that instead of using Tiller, you can update [Helm to version 3](/docs/containers?topic=containers-helm#migrate_v3), in which Tiller is removed. </td>
</tr>
<tr>
<td>Your app uses persistent file storage with a non-root user ID that cannot write to the mounted storage device.</td>
<td>[Adjust the security context](/docs/openshift?topic=openshift-cs_troubleshoot_storage#cs_storage_nonroot) for the app deployment so that `runAsUser` is set to `0`.</td>
</tr>
<tr>
<td>Your service is exposed on port 80 or another port less than 1024. You might see a `Permission denied` error.</td>
<td>Ports less than 1024 are privileged ports that are reserved for start-up processes. You might choose one of the following solutions:<ul>
<li>Change the port to 8080 or a similar port greater than 1024, and update your containers to listen on this port.</li>
<li>Add your container deployment to a privileged service account, such as in the [example for giving a deployment privileged access](#openshift_move_apps_example_scc).</li>
<li>Set up your container to listen on any network port, then update the container runtime to map that port to port 80 on the host by using [port forwarding ![External link icon](../icons/launch-glyph.svg "External link icon")](https://docs.openshift.com/container-platform/4.3/nodes/containers/nodes-containers-port-forwarding.html).</li></ul></td>
</tr>
<tr>
<td>Other use cases and scenarios</td>
<td>Review the OpenShift documentation for migrating databases, web framework apps, CI/CD, and other examples such as from [OCP version 2 to version 3 ![External link icon](../icons/launch-glyph.svg "External link icon")](https://docs.openshift.com/container-platform/3.11/dev_guide/migrating_applications/index.html), or [from OCP version 3 to version 4](/docs/openshift?topic=openshift-openshift_versions#ocp-3-to-4-migration).</td>
</tr>
</tbody>
</table>

### Example steps for giving a deployment privileged access
{: #openshift_move_apps_example_scc}

If you have an app that runs with root permissions, you must modify your deployment to work with the [security context constraints](/docs/openshift?topic=openshift-openshift_scc) that are set for your OpenShift cluster. For example, you might set up your project with a service account to control privileged access, and then modify your deployment to use this service account.
{: shortdesc}

Before you begin: [Access your OpenShift cluster](/docs/openshift?topic=openshift-access_cluster).

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
4.  Add a privileged security context constraint to the service account for the project.<p class="note">If you want to check what policies are included in the `privileged` SCC, run `oc describe scc privileged`. For more information about SCCs, see the [OpenShift documentation](https://docs.openshift.com/container-platform/4.3/authentication/managing-security-context-constraints.html){: external}.</p>
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


## Packaging apps in 4.3 clusters for reuse in multiple environments with Kustomize
{: #kustomize}

As part of a [twelve-factor](https://12factor.net/){: external}, cloud-native app, you want to maintain dev-to-prod parity by setting up a continuous development and delivery pipeline that uses a common, version-controlled codebase source. In your codebase repositories, you store your Kubernetes resource configuration manifest files, often in YAML format. You can use the Kubernetes project [Kustomize](https://kustomize.io/){: external} both to standardize and customize your deployments across multiple environments.
{: shortdesc}

For example, you can set up a base `kustomization` YAML to declare Kubernetes objects such as deployments and PVCs that are shared in your development, testing, and production environments. Next, you can set up separate `kustomization` YAMLs that have customized configurations for each environment, such as more replicas in production than testing. These customized YAMLs can then overlay, or build on, the shared base YAML so that you can manage environments that are mostly identical except for a few overlay configuration differences that you source-control. For more information about Kustomize such as a glossary and FAQs, check out the [Kustomize docs](https://github.com/kubernetes-sigs/kustomize/tree/master/docs){: external}.

<img src="images/icon-version-311.png" alt="Version 3.11 icon" width="30" style="width:30px; border-style: none"/> Kustomize is not supported for OpenShift clusters that run version 3.11.
{: note}

Before you begin: [Access your OpenShift cluster](/docs/openshift?topic=openshift-access_cluster).

To set up configuration files with Kustomize:
1.  [Install the `kustomize` tool](https://github.com/kubernetes-sigs/kustomize/blob/master/docs/INSTALL.md){: external}.
    *   For macOS, you can use the `brew` package manager.
        ```
        brew install kustomize
        ```
        {: pre}
    *   For Windows, you can use the `chocolatey` package manager.
        ```
        choco install kustomize
        ```
        {: pre}
2.  Create a directory for your app in a version control system, such as Git.
    ```
    git init ~/<my_app>
    ```
    {: pre}
3.  Create your repo structure for your `kustomize` [`base`](https://github.com/kubernetes-sigs/kustomize/blob/master/docs/glossary.md#base){: external} directory, [`overlay`](https://github.com/kubernetes-sigs/kustomize/blob/master/docs/glossary.md#overlay){: external} directory, and environment directories such as staging and production. In the subsequent steps, you set up these repos for use with `kustomize`.
    ```
    mkdir -p ~/<my_app>/base &&
    mkdir -p ~/<my_app>/overlay &&
    mkdir -p ~/<my_app>/overlay/staging &&
    mkdir -p ~/<my_app>/overlay/prod
    ```
    {: pre}

    Example repo structure:
    ```
    .
    ├── base
    └── overlay
        ├── prod
        └── staging
    ```
    {: screen}
4.  Set up the `base` repo.
    1.  Navigate to the base repo.
        ```
        cd ~/<my_app>/base
        ```
        {: pre}
    2.  Create an initial set of Kubernetes configuration YAML files for your app deployment.
    3.  Create a [`kustomization` file](https://github.com/kubernetes-sigs/kustomize#1-make-a-kustomization-file) that specifies the base configuration to be applied across environments. The `kustomization` file must include the list of Kubernetes resource configuration YAMLs that are stored in the same `base` repo. In the `kustomization` file, you can also add configurations that apply to all the resource YAMLs in the base repo, such as a prefix or suffix that is appended to all the resource names, a label, the existing namespace all the resources are created in, secrets, configmaps, and more.
        ```
        apiVersion: kustomize.config.k8s.io/v1beta1
        kind: Kustomization
        namespace: wasliberty
        namePrefix: kustomtest-
        nameSuffix: -v2
        commonLabels:
          app: kustomized-wasliberty
        resources:
        - deployment.yaml
        - service.yaml
        - pvc.yaml
        - configmap.yaml
        - secret.yaml
        ```
        {: codeblock}

        The names of the `resources` YAMLs must match the names of the other files in the `base` repo. You might include multiple configurations in the same file, but in the example, the configurations are separate files such as `deployment.yaml`, `service.yaml`, and `pvc.yaml`.

    4.  Build your resource YAML files with the configurations that you defined in the `kustomization` base YAML file. The resources are built by combining the configurations in the `kustomization` and resource YAMLs together. The combined YAML files are returned in `stdout` in the terminal output. Use this same command to build any subsequent changes that you make to the `kustomization` YAML, such adding a label.
        ```
        kustomize build
        ```
        {: pre}
5.  Set up your overlay repo with unique `kustomization` YAML files for each of your environments, such as staging and prod.
    1.  In the staging repo, create a `kustomization.yaml` file. Add any configurations that are unique to staging, such as a label, image tag, or YAML for a new component that you want to test out.
        ```
        apiVersion: kustomize.config.k8s.io/v1beta1
        kind: Kustomization
        namePrefix: staging-
        commonLabels:
          env: staging
          owner: TeamA
        bases:
        - ../../base
        patchesStrategicMerge:
        - configmap.yaml
        - new_staging_resource.yaml
        resources:
        - new_staging_resource.yaml
        ```
        {: codeblock}
        <table summary="A table that describes in Column 1 the YAML file fields and in Column 2 how to fill out those fields.">
        <caption>YAML components</caption>
        <thead>
        <th colspan=2><img src="images/idea.png" alt="Idea icon"/> Understanding the YAML file components</th>
        </thead>
        <tbody>
        <tr>
        <td><code>namePrefix</code></td>
        <td>Specify a prefix to attach to the name of each resource that you want to create with your staging `kustomization` file, such as `staging-`.</td>
        </tr>
        <tr>
        <td><code>commonLabels</code></td>
        <td>Add labels that are unique to the staging objects, such as the staging environment and responsible team.</td>
        </tr>
        <tr>
        <td><code>bases</code></td>
        <td>Add a relative path to a directory or URL to a remote repo that contains a base `kustomization` file. In this example, the relative path points to the base `kustomization` file in the `base` repo that you previously created. This field is required for an overlay `kustomization`.</td>
        </tr>
        <tr>
        <td><code>patchesStrategicMerge</code></td>
        <td>List the resource configuration YAML files that you want to merge to the base `kustomization`. You must also add these files to the same repo as the `kustomization` file, such as `overlay/staging`. These resource configuration files can contain small changes that are merged to the base configuration files of the same name as a patch. The resource gets all the components that are in the `base` configuration file, plus any additional components that you specify in the `overlay` configuration file.<br><br>If the configuration is a new file that is not in the base, you must also add the file name to the `resources` field.</td>
        </tr>
        <tr>
        <td><code>resources</code></td>
        <td>List any resource configuration YAML files that are unique to the staging repo and not included in the base repo. Include these files in the `patchesStrategicMerge` field also, and add them to the same repo as the `kustomization` file, such as `overlay/staging`.</td>
        </tr>
        <tr>
        <td>Other possible configurations</td>
        <td>For more configurations that you might add to your file, see the [Make a `kustomization` file ![External link icon](../icons/launch-glyph.svg "External link icon")](https://github.com/kubernetes-sigs/kustomize#1-make-a-kustomization-file).</td>
        </tr>
        </tbody></table>
    2.  Build your staging overlay configuration files.
        ```
        kustomize build overlay/staging
        ```
        {: pre}
    3.  Repeat these steps to create your prod overlay `kustomization` and other configuration YAML files. For example, you might increase the number of replicas in your `deployment.yaml` so that your prod environment can handle more user requests.
    4.  Review your `kustomize` repo structure to make sure that it includes all the YAML configuration files that you need. The structure might look similar to the following example.
        ```
        ├── base
        │   ├── configmap.yaml
        │   ├── deployment.yaml
        │   ├── kustomization.yaml
        │   ├── pvc.yaml
        │   ├── secret.yaml
        │   └── service.yaml
        └── overlay
            ├── prod
            │   ├── deployment.yaml
            │   ├── kustomization.yaml
            │   └── new_prod_resource.yaml
            └── staging
                ├── configmap.yaml
                ├── kustomization.yaml
                └── new_staging_resource.yaml
        ```
        {: screen}
6.  Apply the Kubernetes resources for the environment that you want to deploy. The following example uses the staging repo.
    1.  Navigate to the staging overlay directory. If you did not build your resources in the previous step, create them now.
        ```
        cd overlay/staging && kustomize build
        ```
        {: pre}
    2.  Apply the Kubernetes resources to your cluster. Include the `-k` flag and the directory where the `kustomization` file is located. For example, if you are already in the staging directory, include `../staging` to mark the path to the directory.
        ```
        oc apply -k ../staging
        ```
        {: pre}
        Example output:
        ```
        configmap/staging-kustomtest-configmap-v2 created
        secret/staging-kustomtest-secret-v2 created
        service/staging-kustomtest-service-v2 created
        deployment.apps/staging-kustomtest-deployment-v2 created
        job.batch/staging-pi created
        persistentvolumeclaim/staging-kustomtest-pvc-v2 created
        ```
    3.  Check to make sure that the staging-unique changes are applied. For example, if you added a `staging-` prefix, the pods and other resources that are created include this prefix in their name.
        ```
        oc get -k ../staging
        ```
        {: pre}
        Example output:
        ```
        NAME                                        DATA   AGE
        configmap/staging-kustomtest-configmap-v2   2      90s

        NAME                                  TYPE     DATA   AGE
        secret/staging-kustomtest-secret-v2   Opaque   2      90s

        NAME                                    TYPE       CLUSTER-IP      EXTERNAL-IP   PORT(S)          AGE
        service/staging-kustomtest-service-v2   NodePort   172.21.xxx.xxx   <none>        9080:30200/TCP   90s

        NAME                                               READY   UP-TO-DATE   AVAILABLE   AGE
        deployment.apps/staging-kustomtest-deployment-v2   0/3     3            0           91s

        NAME                   COMPLETIONS   DURATION   AGE
        job.batch/staging-pi   1/1           41s        2m37s

        NAME                                              STATUS    VOLUME   CAPACITY   ACCESS MODES   STORAGECLASS       AGE
        persistentvolumeclaim/staging-kustomtest-pvc-v2   Pending                                      ibmc-file-bronze   90s
        ```
        {: screen}
    4.  Repeat these steps for each environment that you want to build.
7.  **Optional**: Clean up your environment by removing all the resources that you applied with Kustomize.
    ```
    oc delete -k <directory>
    ```
    {: pre}
    Example output:
    ```
    configmap "staging-kustomtest-configmap-v2" deleted
    secret "staging-kustomtest-secret-v2" deleted
    service "staging-kustomtest-service-v2" deleted
    deployment.apps "staging-kustomtest-deployment-v2" deleted
    job.batch "staging-pi" deleted
    persistentvolumeclaim "staging-kustomtest-pvc-v2" deleted
    ```
    {: screen}

<br />



## Packaging apps in OpenShift 3.11 clusters by using Helm charts
{: #roks_helm}

You can add complex OpenShift apps to your cluster by using Helm charts.
{: shortdesc}

<img src="images/icon-version-43.png" alt="Version 4.3 icon" width="30" style="width:30px; border-style: none"/> In OpenShift clusters that run version 4.3 or later, instead of Helm charts, use [Operators](/docs/openshift?topic=openshift-operators) to package, deploy, and update apps or [Kustomize](#kustomize) to package apps for reuse. If you have custom Helm charts, you can create a [Helm-based Operator](https://docs.openshift.com/container-platform/4.2/operators/operator_sdk/osdk-helm.html){: external} instead.
{: tip}

[Helm](https://helm.sh){: external} is a Kubernetes package manager that uses Helm charts to define, install, and upgrade complex Kubernetes apps in your cluster. Helm charts package the specifications to generate YAML files for Kubernetes resources that build your app. These Kubernetes resources are automatically applied in your cluster and assigned a version by Helm. You can also use Helm to specify and package your own app and let Helm generate the YAML files for your Kubernetes resources.

Before you begin: [Log in to your account. If applicable, target the appropriate resource group. Set the context for your cluster.](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure)

To set up Helm v3 and the {{site.data.keyword.cloud_notm}} Helm repositories in your cluster:

1. Install the latest release of the version 3 [Helm CLI](https://github.com/helm/helm/releases){: external} on your local machine.

2. Add the {{site.data.keyword.cloud_notm}} Helm repositories to your Helm instance.
   ```
   helm repo add iks-charts https://icr.io/helm/iks-charts
   ```
   {: pre}
   ```
   helm repo add ibm-charts https://raw.githubusercontent.com/IBM/charts/master/repo/stable
   ```
   {: pre}
   ```
   helm repo add ibm-community https://raw.githubusercontent.com/IBM/charts/master/repo/community
   ```
   {: pre}
   ```
   helm repo add entitled https://raw.githubusercontent.com/IBM/charts/master/repo/entitled
   ```
   {: pre}

3. Update the repos to retrieve the latest versions of all Helm charts.
   ```
   helm repo update
   ```
   {: pre}

4. List the Helm charts that are currently available in the {{site.data.keyword.cloud_notm}} repositories.
   ```
   helm search repo iks-charts
   ```
   {: pre}
   ```
   helm search repo ibm-charts
   ```
   {: pre}
   ```
   helm search repo ibm-community
   ```
   {: pre}
   ```
   helm search repo entitled
   ```
   {: pre}

5. Identify the Helm chart that you want to install and follow the instructions in the Helm chart `README` to install the Helm chart in your cluster.

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

For more information about the console, see the [OpenShift documentation](https://docs.openshift.com/container-platform/4.3/applications/application-life-cycle-management/odc-creating-applications-using-developer-perspective.html){: external}.

<br />


## Accessing built-in OpenShift services
{: #openshift_access_oc_services}

Red Hat OpenShift on IBM Cloud comes with built-in services that you can use to help operate your cluster, such as the OpenShift console, Prometheus, and Grafana. You can access these services by using the local host of a [route](https://docs.openshift.com/container-platform/3.11/architecture/networking/routes.html){: external}. The default route domain names follow a cluster-specific pattern of `<service_name>-<namespace>.<cluster_name>-<random_ID>.<region>.containers.appdomain.cloud`.
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
