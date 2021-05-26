---

copyright:
  years: 2014, 2021
lastupdated: "2021-05-14"

keywords: openshift, red hat, red hat openshift, rhos, roks, rhoks, odo

subcollection: openshift

content-type: tutorial
services: containers, openshift
account-plan:
completion-time: 10m

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
  
  
# Developing in clusters with the OpenShift Do CLI
{: #odo-tutorial}
{: toc-content-type="tutorial"}
{: toc-services="containers, openshift"}
{: toc-completion-time="10m"}

Accelerate application development on any Kubernetes cluster with the {{site.data.keyword.openshiftshort}} Do (`odo`) command-line interface (CLI) tool.
{: shortdesc}

Designed to improve the developer experience, the `odo` CLI has a simple syntax to help you get started with developing and deploying apps to a Kubernetes cluster. With version 2.0, `odo` supports any Kubernetes platform, not just OpenShift Container Platform. You can use `odo` for {{site.data.keyword.containerlong}} or {{site.data.keyword.openshiftlong}} clusters.

## Objectives
{: #odo-objectives}

- Create and deploy a NodeJS app to a Kubernetes cluster by using the `odo` command line.
- Use the iterative development capabilities of `odo` to push code changes to your cluster in real time.  
- View deployment information and verify that your app is up and running.

## Audience
{: #odo-audience}

This tutorial is intended for software developers who have some familiarity with Kubernetes application development. Instead of configuring a bunch of YAML files and using the `kubectl` CLI to administer the system, you prefer a simpler syntax that is focused more around the developer experience.

## Prerequisites
{: #odo-prereqs}

* [Install the {{site.data.keyword.cloud_notm}} CLI ](/docs/cli?topic=cli-getting-started).
* [Install the `odo` CLI](https://docs.openshift.com/container-platform/4.6/cli_reference/developer_cli_odo/installing-odo.html){: external}.
* [Create](/docs/openshift?topic=openshift-getting-started) or identify an existing Kubernetes cluster to use. In the CLI, you can list clusters by running `ibmcloud oc cluster ls`.

## Create a microservice
{: #odo-new-microservice}
{: step}

After you complete the [prerequisites](#odo-prereqs) install the CLI and select a cluster, you can start creating your microservice with `odo`.
{: shortdesc}

1.  [Log in to your account. If applicable, target the appropriate resource group. Set the context for your cluster.](/docs/openshift?topic=openshift-cs_cli_install#cs_cli_configure)
2.  Verify that the `odo` CLI is able to communicate with your cluster by listing the projects in your cluster. The projects represent Kubernetes namespaces where your apps and other microservice resources run.
    ```
    odo project list
    ```
    {: pre}
3.  Create a project for your NodeJS application. An application, or _app_, is a program that is designed for your users. The app represents the overall experience, not an individual microservice. As such, the app might consist of many microservices, each microserivce referred to as a _component_ in `odo`.
    ```
    odo project create nodejs-test
    ```
    {: pre}

    Example output:
    ```
    ✓  Project 'nodejs-test' is ready for use
    ✓  New project created and now using project: nodejs-test
    ```
    {: screen}
4.  In your command line, create or change directories to the path where your NodeJS app files are stored, or where you want to store the app files.

    If you do not have an existing NodeJS app and want to download a start kit in a later step, the directory must be empty.
    {: note}

    ```
    cd nodejs-test-app
    ```
    {: pre}
5.  Create the NodeJS component in your project. The `odo` CLI prompts you to select the language, name, and project for your new component.
    ```
    odo create
    ```
    {: pre}

    1.  Select the `nodejs` component, as shown in the following example. Example output:
        ```
        ? Which devfile component type do you wish to create  [Use arrows to move, type to filter]
        java-openliberty
        java-quarkus
        java-springboot
        java-vertx
        > nodejs
        python
        python-django
        ```
        {: screen}
    2.  Enter `nodejs-test` for the component name, as shown in the following example.
        ```
        ? What do you wish to name the new devfile component nodejs-test
        ```
        {: screen}
    3.  Use the **Enter** key or re-enter `nodejs-test` for the project that you previously created, as shown in the following example.
        ```
        ? What project do you want the devfile component to be created in nodejs-test
        ```
        {: screen}
    4.  Optional: If you do not have an existing NodeJS app in your directory, you can download a starter kit, as shown in the following example. You can confirm the files are downloaded by running `ls` from the directory.
        ```
        ? Do you want to download a starter project Yes
        ```
        {: screen}

## Push a microservice to the cluster
{: #odo-push-microservice}
{: step}

Now that you have a NodeJS component that is based on your local code, you can push the NodeJS component to your cluster.
{: shortdesc}

You might wonder, how can the microservice be pushed to the cluster without a Dockerfile to describe the image, a YAML file to describe the Kubernetes resource, a Helm chart, or other similar configuration file? The `odo` command line uses the [{{site.data.keyword.openshiftshort}} `source-to-image`](https://github.com/openshift/source-to-image){: external} capability to generate all the configuration files that are needed to deploy the microservice to the Kubernetes cluster.

1.  Push the NodeJS component to your cluster. The `odo` CLI validates the NodeJS component and packages the component as a deployable container.
    ```
    odo push
    ```
    {: pre}

    Example output:
    ```
    Validation
    ✓  Validating the devfile [710378ns]

    Creating Kubernetes resources for component nodejs-test
    ✓  Waiting for component to start [33s]

    Applying URL changes
    ✓  URL http-3000: http://http-3000-nodejs-test-nodejs-test.<cluster_name>-<ID>.<region>.containers.appdomain.cloud/ created

    Syncing to component nodejs-test
    ✓  Checking files for pushing [2ms]
    ✓  Syncing files to the component [15s]

    Executing devfile commands for component nodejs-test
    ✓  Executing install command "npm install" [10s]
    ✓  Executing run command "npm start" [8s]

    Pushing devfile component nodejs-test
    ✓  Changes successfully pushed to component

    ```
    {: screen}
2.  Verify that the component is running in your cluster. You can also view the component from your cluster's {{site.data.keyword.openshiftshort}} web console.
    ```
    oc get all -n nodejs-test
    ```
    {: pre}
3.  In the output of the previous step, copy the route for your microservice that users can access from outside the cluster.
4.  In a web browser, open the URL of your NodeJS app. You see your app, or if you used the starter kit, a message similar to the following.
    ```
    Hello from Node.js Starter Application!
    ```
    {: screen}

## What's next?
{: #odo-next-steps}

Now that you have a microservice running in your cluster, you might wonder what comes next.
{: shortdesc}

*   **Add more microservices to your app**: You can repeat this process to build out your app by adding microservices.
*   **Develop your app iteratively**: Whenever you need to make changes to your microservice, rerun the `odo push` command from the app directory to update the microservice in your cluster.

    Don't want to remember to push each time? Try the `odo watch` command to monitor for local file changes and automatically push the saved updates to your cluster.
    {: tip}

*   **Learn more about OpenShift Do**: Learn more about the features of `odo` by visiting the [{{site.data.keyword.redhat_notm}} {{site.data.keyword.openshiftshort}} Do CLI Documentation](https://docs.openshift.com/container-platform/4.6/cli_reference/developer_cli_odo/understanding-odo.html){: external}.
