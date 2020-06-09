---

copyright:
  years: 2014, 2020
lastupdated: "2020-06-09"

keywords: openshift, roks, rhoks, rhos, registry, pull secret, secrets

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





# Building images for your apps
{: #images}


A Docker image is the basis for every container that you create with {{site.data.keyword.openshiftlong}}.
{:shortdesc}

An image is created from a Dockerfile, which is a file that contains instructions to build the image. A Dockerfile might reference build artifacts in its instructions that are stored separately, such as an app, the app's configuration, and its dependencies.

## Deploying containers from an existing image stream in the internal registry
{: #oc_imagestream_deploy}

You can deploy an app from an existing [image stream](https://docs.openshift.com/container-platform/4.3/openshift_images/image-streams-manage.html){: external} that your cluster administrator set up in the internal registry of your OpenShift cluster. For example, your cluster administrator might have [set up the image stream to import an image from an external private registry](/docs/openshift?topic=openshift-registry#imagestream_registry), such as {{site.data.keyword.registrylong_notm}}.
{: shortdesc}

**Using an image stream from the CLI**:
1.  [Access your OpenShift cluster](/docs/openshift?topic=openshift-access_cluster).
2.  List the available image streams in a project. If you know the project, name, and tag of the image stream, you can use local image streams in other projects without setting up image pull stream credentials.
    ```
    oc get is -n <project>
    ```
    {: pre}
3.  Create your app from the image stream.
    ```
    oc new-app --image-stream="<project>/<imagestream>:<tag>"
    ```
    {: pre}

**Using an image stream from the OpenShift web console**:
1.  From the [OpenShift web console](/docs/openshift?topic=openshift-deploy_app#deploy_apps_ui), switch to the **Developer** perspective and click **+Add**.
2.  In the **Add** pane menu bar, select a **Project** that is not `default` to create your app in, and click **Container Image**.
3.  In the **Image** section, select **Image name from internal registry**.
4.  Select `default` **Project**, `<image>` **ImageStreams**, and `<tag>` **Tag** of the image stream that you previously created.
5.  Review the rest of the application details, and click **Create**.

<br />



## Deploying containers from an {{site.data.keyword.registrylong_notm}} image to the `default` OpenShift project
{: #namespace}

You can deploy containers to your cluster from an IBM-provided public image or a private image that is stored in your {{site.data.keyword.registrylong_notm}} namespace. For more information about how your cluster accesses registry images, see [Understanding how your cluster is authorized to pull images from {{site.data.keyword.registrylong_notm}}](/docs/openshift?topic=openshift-registry#cluster_registry_auth).
{:shortdesc}

Before you begin:
1. [Set up a namespace in {{site.data.keyword.registrylong_notm}} and push images to this namespace](/docs/Registry?topic=Registry-getting-started#gs_registry_namespace_add).
2. [Create an OpenShift cluster](/docs/openshift?topic=openshift-clusters).
3. [Access your {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-access_cluster).

To deploy a container into the **default** project of your cluster:

1.  Create a deployment configuration file that is named `<deployment>.yaml`.
2.  Define the deployment and the image to use from your project in {{site.data.keyword.registrylong_notm}}.

    ```yaml
    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: <deployment>
    spec:
      replicas: <number_of_replicas>
      selector:
        matchLabels:
          app: <app_name>
      template:
        metadata:
          labels:
            app: <app_name>
        spec:
          containers:
          - name: <app_name>
            image: <region>.icr.io/<project>/<image>:<tag>
    ```
    {: codeblock}

    <table>
    <caption>Understanding the YAML file components</caption>
    <col width="20%">
    <thead>
    <th>Parameter</th>
    <th>Description</th>
    </thead>
    <tbody>
    <tr>
    <td><code><em>&lt;deployment&gt;</em></code></td>
    <td>Give your deployment a name.</td>
    </tr>
    <tr>
    <td><code><em>&lt;number_of_replicas&gt;</em></code></td>
    <td>Enter the number of replica pods that the deployment creates.</td>
    </tr>
    <tr>
    <td><code>app: <em>&lt;app_name&gt;</em></code></td>
    <td>Use the name of your app as a label for the container.</td>
    </tr>
    <tr>
    <td><code>name: <em>&lt;app_name&gt;</em></code></td>
    <td>Give your container a name, such as the name of your `app` label.</td>
    </tr>
    <tr>
    <td><code>image: <em>&lt;region&gt;</em>.icr.io/<em>&lt;project&gt;</em>/<em>&lt;image&gt;</em>:<em>&lt;tag&gt;</em></code></td>
    <td>Replace the image URL variables with the information for your image:
      <ul><li>**`<region>`**: The regional {{site.data.keyword.registrylong_notm}} API endpoint for the registry domain. To list the domain for the region that you are logged in to, run `ibmcloud cr api`.</li>
      <li>**`<namespace>`**: The registry namespace. To get your namespace information, run `ibmcloud cr namespace-list`.</li>
      <li>**`<image>:<tag>`**: The image and tag that you want to use for your container. To list the images that are available in your registry namespace, run `ibmcloud cr images`.</li></ul></td>
    </tr>
    </tbody></table>

3.  Create the deployment in your cluster.

    ```
    oc apply -f <deployment>.yaml
    ```
    {: pre}

<br />


## Referring to the image pull secret in your pod deployment
{: #pod_imagePullSecret}

If the cluster administrator did not [store the image pull secret in the Kubernetes service account](/docs/openshift?topic=openshift-registry#use_imagePullSecret), all deployments that do not specify a service account cannot use the image pull secret to deploy containers. Instead, you can define an image pull secret in your pod deployment. When you refer to the image pull secret in a pod deployment, the image pull secret is valid for this pod only and cannot be shared across pods in the OpenShift project.
{: shortdesc}

Before you begin:
* [Create an image pull secret](/docs/openshift?topic=openshift-registry#other) to access images in other registries or OpenShift projects other than `default`.
* [Access your {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-access_cluster).

Steps:

1.  Create a pod configuration file that is named `mypod.yaml`.
2.  Define the pod and the image pull secret to access images in {{site.data.keyword.registrylong_notm}}.

    To access a private image:
    ```yaml
    apiVersion: v1
    kind: Pod
    metadata:
      name: mypod
    spec:
      containers:
        - name: <container_name>
          image: <region>.icr.io/<namespace_name>/<image_name>:<tag>
      imagePullSecrets:
        - name: <secret_name>
    ```
    {: codeblock}

    To access an {{site.data.keyword.cloud_notm}} public image:
    ```yaml
    apiVersion: v1
    kind: Pod
    metadata:
      name: mypod
    spec:
      containers:
        - name: <container_name>
          image: icr.io/<image_name>:<tag>
      imagePullSecrets:
        - name: <secret_name>
    ```
    {: codeblock}

    <table>
    <caption>Understanding the YAML file components</caption>
    <col width="20%">
    <thead>
    <th>Parameter</th>
    <th>Description</th>
    </thead>
    <tbody>
    <tr>
    <td><code><em>&lt;container_name&gt;</em></code></td>
    <td>The name of the container to deploy to your cluster.</td>
    </tr>
    <tr>
    <td><code><em>&lt;namespace_name&gt;</em></code></td>
    <td>The registry namespace where the image is stored. To list available namespaces, run `ibmcloud cr namespace-list`.</td>
    </tr>
    <tr>
    <td><code><em>&lt;image_name&gt;</em></code></td>
    <td>The name of the image to use. To list available images in an {{site.data.keyword.cloud_notm}} account, run `ibmcloud cr image-list`.</td>
    </tr>
    <tr>
    <td><code><em>&lt;tag&gt;</em></code></td>
    <td>The version of the image that you want to use. If no tag is specified, the image that is tagged <strong>latest</strong> is used by default.</td>
    </tr>
    <tr>
    <td><code><em>&lt;secret_name&gt;</em></code></td>
    <td>The name of the image pull secret that you created earlier.</td>
    </tr>
    </tbody></table>

3.  Save your changes.
4.  Create the deployment in your cluster.
    ```
    oc apply -f mypod.yaml
    ```
    {: pre}

<br />


## Pushing images to {{site.data.keyword.registrylong_notm}}
{: #push-images}

After the cluster administrator [sets up an image registry with {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-getting-started#getting-started), you can securely store and share Docker images with other users by adding images to your namespace.
{: shortdesc}

For example, you might pull an image from any private or public registry source, and then tag it for later use in {{site.data.keyword.registrylong_notm}}. Or, you might push a Docker image that you work with to your namespace so that other users can access the image. To get started, see [Adding images to your namespace](/docs/Registry?topic=Registry-registry_images_).

<br />


## Managing security of images in {{site.data.keyword.registrylong_notm}} with Vulnerability Advisor
{: #va-images}

Vulnerability Advisor checks the security status of container images that are provided by IBM, third parties, or added to your organization's {{site.data.keyword.registrylong_notm}} namespace.
{: shortdesc}

When you add an image to a namespace, the image is automatically scanned by Vulnerability Advisor to detect security issues and potential vulnerabilities. If security issues are found, instructions are provided to help fix the reported vulnerability. To get started, see [Managing image security with Vulnerability Advisor](/docs/Registry?topic=va-va_index).

<br />


