---

copyright:
  years: 2014, 2020
lastupdated: "2020-02-12"

keywords: openshift, roks, rhoks, rhos, registry, pull secret, secrets

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




# Building images for your apps
{: #images}

{{site.data.keyword.openshiftlong}} clusters include an internal registry to build, deploy, and manage container images locally. For a private registry to manage and control access to images across your enterprise, you can also set up your cluster to use {{site.data.keyword.registrylong}}.
{: shortdesc}

A Docker image is the basis for every container that you create with Red Hat OpenShift on IBM Cloud. An image is created from a Dockerfile, which is a file that contains instructions to build the image. A Dockerfile might reference build artifacts in its instructions that are stored separately, such as an app, the app's configuration, and its dependencies.

## Choosing an image registry solution
{: #openshift_registry_options}

Your app's images must be stored in a container registry that your cluster can access to deploy apps into your cluster. You can choose to use the built-in registry of your OpenShift cluster, a private registry with access restricted to select users, or a public registry. Review the following table to decide which option is suited for your use case.
{: shortdesc}

<table summary="The rows are read left to right, with the type of registry in column one and the description of the registry in column two.">
    <caption>Choosing an image registry solution</caption>
    <thead>
      <th>Registry</th>
      <th>Description</th>
    </thead>
    <tbody>
    <tr>
        <td>Internal OpenShift Container Registry (OCR)</td>
        <td>Your cluster is set up with the internal OpenShift Container Registry so that OpenShift can automatically build, deploy, and manage your application lifecycle from within the cluster. Images are stored in a backing {{site.data.keyword.cloud_notm}} classic file storage device that is provisioned at cluster creation time. If you need more storage, you can resize the device.
        <br><br>Use cases:<ul>
        <li>OpenShift-native image stream, build, and app deployment process on a per cluster basis.</li>
        <li>Images can be shared across all projects in the cluster, with access that is controlled through RBAC roles.</li>
        <li>Integrating the registry with other Red Hat products like CloudForms for extended features such as vulnerability scanning.</li>
        <li>Option to expose the registry with a route for public network access.</li></ul>
        <br>For more information, see [Using the internal registry](#openshift_internal_registry).</td>
    </tr>
    <tr>
        <td>Private registry</td>
        <td>Private registries are a good choice to protect your images from being used and changed by unauthorized users. Private registries must be set up by the cluster administrator to make sure that access, storage quotas, image trust and other features work as intended.<br><br>
        By default, your [OpenShift clusters are integrated with the private {{site.data.keyword.registrylong_notm}}](#openshift_iccr) through image pull secrets that are set up in the `default` project. {{site.data.keyword.registrylong_notm}} is a highly available, multi-tenant private registry to store your own images. You can also pull IBM-provided images from the global `icr.io` registry, and licensed software from the entitled registry. With {{site.data.keyword.registrylong_notm}}, you can manage images for multiple clusters with seamless integration with {{site.data.keyword.cloud_notm}} IAM and billing.<br><br>
        Advantages of {{site.data.keyword.registrylong_notm}} over the internal registry:<ul>
        <li>Sharing images across multiple clusters without needing to push images to multiple registries.</li>
        <li>[Automatically scanning](/docs/Registry?topic=va-va_index) the vulnerability of images.</li>
        <li>Controlling access through [{{site.data.keyword.cloud_notm}} IAM policies](/docs/Registry?topic=registry-user) and [separate regional registries](/docs/Registry?topic=registry-registry_overview#registry_regions).</li>
        <li>[Retaining images](/docs/Registry?topic=registry-registry_retention) without requiring storage space in your cluster or an attached storage device. You can also set policies to manage the quantity of images to prevent them from taking up too much space.</li>
        <li>Using the private service endpoint so that clusters on only the private network can still access the registry.</li>
        <li>[Setting storage and image pull traffic quotas](/docs/Registry?topic=registry-registry_quota) to better control image storage, usage, and billing.</li>
        <li>Pulling licensed IBM content from the [entitled registry](/docs/containers?topic=containers-images#secret_entitled_software).</li></ul>
        <br>To get started, see the following topics:<ul>
        <li>[Getting started with {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=registry-getting-started).</li>
        <li>[Using {{site.data.keyword.registrylong_notm}}](#openshift_iccr).</li></ul></td>
    </tr>
    <tr>
        <td>Public registry</td>
        <td>Public registries such as Docker Hub are an easy way to share images across teams, companies, clusters, or cloud providers. Some public registries might also offer a private registry component.<br><br>Use cases:<ul>
        <li>Pushing and pulling images on the public network.</li>
        <li>Quick testing of a container across multiple cloud providers.</li>
        <li>Do not need enterprise-grade features such as vulnerability scanning or access management.</li></ul>
        <br>For more information, see the public registry's documentation, such as [Quay ![External link icon](../icons/launch-glyph.svg "External link icon")](https://quay.io/) or [Docker Hub ![External link icon](../icons/launch-glyph.svg "External link icon")](https://hub.docker.com/).</td>
    </tr>
    </tbody>
</table>



## Using the internal registry
{: #openshift_internal_registry}

OpenShift clusters are set up by default with an internal registry. When you delete the cluster, the internal registry and its images are also deleted. If you want to persist your images, consider using a private registry such as {{site.data.keyword.registrylong_notm}}, backing up your images to persistent storage such as {{site.data.keyword.objectstorageshort}}, or creating a separate, stand-alone OpenShift container registry (OCR) cluster. For more information, see the [OpenShift docs](https://docs.openshift.com/container-platform/4.3/registry/architecture-component-imageregistry.html){: external}.
{: shortdesc}

### Storing images in the internal registry
{: #storage_internal_registry}

By default, your OpenShift cluster's internal registry uses an [{{site.data.keyword.cloud_notm}} File Storage](/docs/openshift?topic=openshift-file_storage) volume to store the registry images. You can review the default size of the storage volume, or update the volume size.
{: shortdesc}

To view volume details including the storage class and size, you can describe the persistent volume claim.

```
oc describe pvc registry-backing -n default
```
{: pre}

Example output:
```
Name:          registry-backing
Namespace:     default
StorageClass:  ibmc-file-bronze
Status:        Bound
Volume:        pvc-1c6bb7e9-b3f3-11e9-a5b4-020670ab62dc
Labels:        billingType=hourly
               region=us-east
               zone=wdc04
Annotations:   ibm.io/provisioning-status=complete
               kubectl.kubernetes.io/last-applied-configuration={"apiVersion":"v1","kind":"PersistentVolumeClaim","metadata":{"annotations":{},"labels":{"billingType":"hourly"},"name":"registry-backing","namespace":...
               pv.kubernetes.io/bind-completed=yes
               pv.kubernetes.io/bound-by-controller=yes
               volume.beta.kubernetes.io/storage-provisioner=ibm.io/ibmc-file
Finalizers:    [kubernetes.io/pvc-protection]
Capacity:      20Gi
Access Modes:  RWX
Events:        <none>
```
{: screen}

If your registry needs additional gigabytes of storage for your images, you can resize the file storage volume. For more information, see [Changing the size and IOPS of your existing storage device](/docs/openshift?topic=openshift-file_storage#file_change_storage_configuration). When you resize the volume in your IBM Cloud infrastructure account, the attached PVC description is not updated. Instead, you can log in to the `image-registry` (OpenShift 4.3) or `docker-registry` (OpenShift 3.11) pod that uses the `registry-backing` PVC to verify that the volume is resized.
{: note}

### Setting up a secure external route for the internal registry
{: #route_internal_registry}

By default, your OpenShift cluster has an internal registry that is available through a service with an internal IP address. If you want to make the internal registry available on the public network, you can set up a secure re-encrypt route. For example, you might set up your cluster's internal registry to act as a public registry for deployments in other projects or clusters.
{: shortdesc}

Before you begin:
*  Confirm that you have the [**Manager** {{site.data.keyword.cloud_notm}} IAM service role](/docs/openshift?topic=openshift-access_reference#service) for the cluster.
*  Make sure that your cluster has public network connectivity to expose the internal registry with a public route.
*  Install Docker on your local machine.
*  [Access your OpenShift cluster](/docs/openshift?topic=openshift-access_cluster).

<img src="images/icon-version-311.png" alt="Version 3.11 icon" width="30" style="width:30px; border-style: none"/> For OpenShift 3.11 clusters, the internal registry is in the `default` project and uses the `docker-registry` service. The following steps are specific for 4.3 clusters. To set up the route in a 3.11 cluster, replace the `openshift-image-registry` project with `default` and the `image-registry` service with `docker-registry`. 
{: important}

To use the internal registry, set up a public route to access the registry. Then, create an image pull secret that includes the credentials to access the registry so that deployments in other projects can pull images from this registry.

1.  From the `openshift-image-registry` project, make sure that the `image-registry` service exists for the internal registry.
    ```
    oc get svc
    ```
    {: pre}

    Example output:
    ```
    NAME                      TYPE           CLUSTER-IP       EXTERNAL-IP     PORT(S)                      AGE
    image-registry            ClusterIP      172.21.xxx.xxx    <none>          5000/TCP                     36d
    image-registry-operator   ClusterIP      None             <none>          60000/TCP                     36d
    ```
    {: screen}
2.  Create a secured route for the `image-registry` service that uses `reencrypt` TLS termination. With re-encryption, the router terminates the TLS connection with a certificate, and then re-encrypts the connection to the internal registry with a different certificate. With this approach, the full path of the connection between the user and the internal registry is encrypted. To provide your own custom domain name, include the `--hostname` flag.
    ```
    oc create route reencrypt --service=image-registry
    ```
    {: pre}
3.  Retrieve the hostname (**HOST/PORT**) and the **PORT** that were assigned to the `image-registry` route.
    ```
    oc get route image-registry
    ```
    {: pre}
    Example output:
    ```
    NAME              HOST/PORT                                                                                                  PATH      SERVICES          PORT       TERMINATION   WILDCARD
    image-registry   image-registry-openshift-image-registry.<cluster_name>-<ID_string>.<region>.containers.appdomain.cloud             image-registry   5000-tcp   reencrypt     None
    ```
    {: screen}
4.  Edit the route to set the [load balancing strategy](https://docs.openshift.com/container-platform/3.11/architecture/networking/routes.html#load-balancing){: external} to `source` so that the same client IP address reaches the same server, as in a passthrough route setup. You can set the strategy by adding an annotation in the `metadata.annotations` section: `haproxy.router.openshift.io/balance: source`. You can edit the configuration file from the **OpenShift Application Console** or in your terminal by running the following command.
    ```
    oc edit route image-registry
    ```
    {: pre}

    Annotation to add:
    ```
    apiVersion: route.openshift.io/v1
    kind: Route
    metadata:
    annotations:
        haproxy.router.openshift.io/balance: source
    ...
    ```
    {: screen}
5.  Log in to the internal registry by using the route as the hostname.
    ```
    docker login -u $(oc whoami) -p $(oc whoami -t) image-registry-openshift-image-registry.<cluster_name>-<ID_string>.<region>.containers.appdomain.cloud
    ```
    {: pre}
6.  Now that you are logged in, try pushing a sample `hello-world` app to the internal registry.
    1.  Pull the `hello-world` image from DockerHub, or build an image on your local machine.
        ```
        docker pull hello-world
        ```
        {: pre}
    2.  Tag the local image with the hostname of your internal registry, the project that you want to deploy the image to, and the image name and tag.
        ```
        docker tag hello-world:latest image-registry-openshift-image-registry.<cluster_name>-<ID_string>.<region>.containers.appdomain.cloud/<project>/<image_name>:<tag>
        ```
        {: pre}
    3.  Push the image to your cluster's internal registry.
        ```
        docker push image-registry-openshift-image-registry.<cluster_name>-<ID_string>.<region>.containers.appdomain.cloud/<project>/<image_name>:<tag>
        ```
        {: pre}
    4.  Verify that the image is added to the OpenShift image stream.
        ```
        oc get imagestream
        ```
        {: pre}

        Example output:
        ```
        NAME          DOCKER REPO                                                            TAGS      UPDATED
        hello-world   image-registry-openshift-image-registry.svc:5000/default/hello-world   latest    7 hours ago
        ```
        {: screen}
7.  To enable deployments in your project to pull images from the internal registry, create an image pull secret in your project that holds the credentials to access your internal registry. Then, add the image pull secret to the default service account for each project.
    1.  List the image pull secrets that the default service account uses, and note the secret that begins with `default-dockercfg`.
        ```
        oc describe sa default
        ```
        {: pre}
        Example output:
        ```
        ...
        Image pull secrets:  default-icr-io
                     default-us-icr-io
                     default-uk-icr-io
                     default-de-icr-io
                     default-au-icr-io
                     default-jp-icr-io
                     default-dockercfg-mpcn4
        ...
        ```
        {: screen}
    2.  Get the encoded secret information from the `data` field of the configuration file.
        ```
        oc get secret <default-dockercfg-name> -o yaml
        ```
        {: pre}
        Example output:
        ```
        apiVersion: v1
        data:
          .dockercfg: ey...=
        ```
        {: screen}
    3.  Decode the value of the `data` field.
        ```
        echo "<ey...=>" | base64 -D
        ```
        {: pre}
        Example output:
        ```
        {"172.21.xxx.xxx:5000":{"username":"serviceaccount","password":"eyJ...
        ```
        {: screen}
    4.  Create a new image pull secret for the internal registry.
        * **<secret_name>**: Give your image pull secret a name, such as `internal-registry`.
        * **--namespace**: Enter the project to create the image pull secret in, such as `default`.
        * **--docker-server**: Instead of the internal service IP address (`172.21.xxx.xxx:5000`), enter the hostname of the `image-registry` route with the port (`image-registry-openshift-image-registry.<cluster_name>-<ID_string>.<region>.containers.appdomain.cloud:5000`).
        * **--docker-username**: Copy the `"username"` from the previous image pull secret, such as `serviceaccount`.
        * **--docker-password**: Copy the `"password"` from the previous image pull secret.
        * **--docker-email**: If you have one, enter your Docker email address. If you do not, enter a fictional email address, such as `a@b.c`. This email is required to create a Kubernetes secret, but is not used after creation.

        ```
        oc create secret image-registry internal-registry --namespace default --docker-server image-registry-openshift-image-registry.<cluster_name>-<ID_string>.<region>.containers.appdomain.cloud:5000 --docker-username serviceaccount --docker-password <eyJ...> --docker-email a@b.c
        ```
        {: pre}
    5.  Add the image pull secret to the default service account of your project.
        ```
        oc patch -n <namespace_name> serviceaccount/default --type='json' -p='[{"op":"add","path":"/imagePullSecrets/-","value":{"name":"<image_pull_secret_name>"}}]'
        ```
        {: pre}
    6.  Repeat these steps for each project that you want to pull images from the internal registry.

Now that you set up the internal registry with an accessible route, you can log in, push, and pull images to the registry. For more information, see the [OpenShift documentation](https://docs.openshift.com/container-platform/4.3/registry/accessing-the-registry.html){: external}.

<br />


## Using {{site.data.keyword.registrylong_notm}}
{: #openshift_iccr}

By default, your Red Hat OpenShift on IBM Cloud cluster is set up to pull images from the remote, private {{site.data.keyword.registrylong_notm}} `icr.io` domains in the `default` project. If you want to use images that are stored in {{site.data.keyword.registrylong_notm}} for other projects, you must create image pull secrets for each global and regional registry. Then, add the image pull secrets to each project, and to a service account for each project or to each deployment.
{: shortdesc}

For more information, see the following topics.
* [Understanding how to authorize your cluster to pull images from a registry](#cluster_registry_auth).
* [Copying the `default-<region>-icr-io` secrets](#copy_imagePullSecret) from the `default` project to the project that you want to pull images from.
* [Creating your own image pull secret](#other_registry_accounts).
* [Adding the image pull secret](#use_imagePullSecret) to your deployment configuration or to the project service account.

<br />







## Deploying containers from an {{site.data.keyword.registryshort_notm}} image to the `default` OpenShift project
{: #namespace}

You can deploy containers to your cluster from an IBM-provided public image or a private image that is stored in your {{site.data.keyword.registryshort_notm}} namespace. For more information about how your cluster accesses registry images, see [Understanding how your cluster is authorized to pull images from {{site.data.keyword.registrylong_notm}}](#cluster_registry_auth).
{:shortdesc}

Before you begin:
1. [Set up a namespace in {{site.data.keyword.registryshort_notm}} and push images to this namespace](/docs/Registry?topic=registry-getting-started#gs_registry_namespace_add).
2. [Create a cluster](/docs/openshift?topic=openshift-clusters).
4. [Access your OpenShift cluster](/docs/openshift?topic=openshift-access_cluster).

To deploy a container into the **default** project of your cluster:

1.  Create a deployment configuration file that is named `mydeployment.yaml`.
2.  Define the deployment and the image to use from your project in {{site.data.keyword.registryshort_notm}}.

    ```yaml
    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: <app_name>-deployment
    spec:
      replicas: 3
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
            image: <region>.icr.io/<namespace>/<my_image>:<tag>
    ```
    {: codeblock}

    Replace the image URL variables with the information for your image:
    *  **`<app_name>`**: The name of your app.
    *  **`<region>`**: The regional {{site.data.keyword.registryshort_notm}} API endpoint for the registry domain. To list the domain for the region that you are logged in to, run `ibmcloud cr api`.
    *  **`<namespace>`**: The registry namespace. To get your namespace information, run `ibmcloud cr namespace-list`.
    *  **`<my_image>:<tag>`**: The image and tag that you want to use to build the container. To get the images available in your registry, run `ibmcloud cr images`.

3.  Create the deployment in your cluster.

    ```
    oc apply -f mydeployment.yaml
    ```
    {: pre}

<br />


## Understanding how to authorize your cluster to pull images from a registry
{: #cluster_registry_auth}

To pull images from a registry, your Red Hat OpenShift on IBM Cloud cluster uses a special type of Kubernetes secret, an `imagePullSecret`. This image pull secret stores the credentials to access a container registry. The container registry can be your namespace in {{site.data.keyword.registrylong_notm}}, a namespace in {{site.data.keyword.registrylong_notm}} that belongs to a different {{site.data.keyword.cloud_notm}} account, or any other private registry such as Docker. Your cluster is set up to pull images from your namespace in {{site.data.keyword.registrylong_notm}} and deploy containers from these images to the `default` Kubernetes namespace in your cluster. If you need to pull images in other cluster OpenShift project or other registries, you must set up the image pull secret.
{:shortdesc}

**How is my cluster set up to pull images from the `default` OpenShift project?**<br>
When you create a cluster, the cluster has an {{site.data.keyword.cloud_notm}} IAM service ID that is given an IAM **Reader** service access role policy to {{site.data.keyword.registrylong_notm}}. The service ID credentials are impersonated in a non-expiring API key that is stored in image pull secrets in your cluster. The image pull secrets are added to the `default` Kubernetes namespace and the list of secrets in the `default` service account for this OpenShift project. By using image pull secrets, your deployments can pull (read-only access) images in your [global and regional registry](/docs/Registry?topic=registry-registry_overview#registry_regions) to build containers in the `default` OpenShift project. The global registry securely stores public, IBM-provided images that you can refer to across your deployments instead of having different references for images that are stored in each regional registry. The regional registry securely stores your own private Docker images.

**Can I restrict pull access to a certain regional registry?**<br>
Yes, you can [edit the existing IAM policy of the service ID](/docs/iam?topic=iam-serviceidpolicy#access_edit) that restricts the **Reader** service access role to that regional registry or a registry resource such as a namespace. Before you can customize registry IAM policies, you must [enable {{site.data.keyword.cloud_notm}} IAM policies for {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=registry-user#existing_users).

  Want to make your registry credentials even more secured? Ask your cluster admin to [enable a key management service provider](/docs/openshift?topic=openshift-encryption#keyprotect) in your cluster to encrypt Kubernetes secrets in your cluster, such as the `imagePullSecret` that stores your registry credentials.
  {: tip}

**Can I pull images in a OpenShift project other than `default`?**<br>
Not by default. By using the default cluster setup, you can deploy containers from any image that is stored in your {{site.data.keyword.registrylong_notm}} namespace into the `default` OpenShift project of your cluster. To use these images in other OpenShift projects or other {{site.data.keyword.cloud_notm}} accounts, [you have the option to copy or create your own image pull secret](#other).

**Can I pull images from a different {{site.data.keyword.cloud_notm}} account?**<br>
Yes, create an API key in the {{site.data.keyword.cloud_notm}} account that you want to use. Then, create an image pull secret that stores those API key credentials in each cluster and cluster namespace that you want to pull from. [Follow along with this example that uses an authorized service ID API key](#other_registry_accounts).

To use a non-{{site.data.keyword.cloud_notm}} registry such as Docker, see [Accessing images that are stored in other private registries](#private_images).

**Does the API key need to be for a service ID? What happens if I reach the limit of service IDs for my account?**<br>
The default cluster setup creates a service ID to store {{site.data.keyword.cloud_notm}} IAM API key credentials in the image pull secret. However, you can also create an API key for an individual user and store those credentials in an image pull secret. If you reach the [IAM limit for service IDs](/docs/iam?topic=iam-iam_limits#iam_limits), your cluster is created without the service ID and image pull secret and cannot pull images from the `icr.io` registry domains by default. You must [create your own image pull secret](#other_registry_accounts), but by using an API key for an individual user such as a functional ID, not an {{site.data.keyword.cloud_notm}} IAM service ID.

**After I copy or create an image pull secret in another OpenShift project, am I done?**<br>
Not quite. Your containers must be authorized to pull images by using the secret that you created. You can add the image pull secret to the service account for the namespace, or refer to the secret in each deployment. For instructions, see [Using the image pull secret to deploy containers](#use_imagePullSecret).

<br />


## Using an image pull secret to access images in other {{site.data.keyword.cloud_notm}} accounts or external private registries from non-default OpenShift projects
{: #other}

Set up your own image pull secret in your cluster to deploy containers to OpenShift projects other than `default`, use images that are stored in other {{site.data.keyword.cloud_notm}} accounts, or use images that are stored in external private registries. Further, you might create your own image pull secret to apply IAM access policies that restrict permissions to specific registry image namespaces, or actions (such as `push` or `pull`).
{:shortdesc}

After you create the image pull secret, your containers must use the secret to be authorized to pull an image from the registry. You can add the image pull secret to the service account for the project, or refer to the secret in each deployment. For instructions, see [Using the image pull secret to deploy containers](#use_imagePullSecret).

Image pull secrets are valid only for the OpenShift projects that they were created for. Repeat these steps for every namespace where you want to deploy containers.
{: tip}

Before you begin:

1.  [Set up a namespace in {{site.data.keyword.registryshort_notm}} and push images to this namespace](/docs/Registry?topic=registry-getting-started#gs_registry_namespace_add).
2.  [Create a cluster](/docs/openshift?topic=openshift-clusters).
4.  [Access your OpenShift cluster](/docs/openshift?topic=openshift-access_cluster).

<br/>
To use your own image pull secret, choose among the following options:
- [Copy the image pull secret](#copy_imagePullSecret) from the default OpenShift project to other projects in your cluster.
- [Create new IAM API key credentials and store them in an image pull secret](#other_registry_accounts) to access images in other {{site.data.keyword.cloud_notm}} accounts or to apply IAM policies that restrict access to certain registry domains or namespaces.
- [Create an image pull secret to access images in external private registries](#private_images).

<br/>
If you already created an image pull secret in your project that you want to use in your deployment, see [Deploying containers by using the created `imagePullSecret`](#use_imagePullSecret).

### Copying an existing image pull secret
{: #copy_imagePullSecret}

You can copy an image pull secret, such as the one that is automatically created for the `default` OpenShift project, to other projects in your cluster. If you want to use different {{site.data.keyword.cloud_notm}} IAM API key credentials for this project such as to restrict access to specific projects, or to pull images from other {{site.data.keyword.cloud_notm}} accounts, [create an image pull secret](#other_registry_accounts) instead.
{: shortdesc}

1.  List available OpenShift projects in your cluster, or create a project to use.
    ```
    oc get projects
    ```
    {: pre}

    Example output:
    ```
    default          Active    79d
    ibm-cert-store   Active    79d
    ibm-system       Active    79d
    kube-public      Active    79d
    kube-system      Active    79d
    ```
    {: screen}

    To create a project:
    ```
    oc new-project <project_name>
    ```
    {: pre}
2.  List the existing image pull secrets in the `default` OpenShift project for {{site.data.keyword.registrylong_notm}}.
    ```
    oc get secrets -n default | grep icr
    ```
    {: pre}
    Example output:
    ```
    default-us-icr-io                          kubernetes.io/dockerconfigjson        1         16d
    default-uk-icr-io                          kubernetes.io/dockerconfigjson        1         16d
    default-de-icr-io                          kubernetes.io/dockerconfigjson        1         16d
    default-au-icr-io                          kubernetes.io/dockerconfigjson        1         16d
    default-jp-icr-io                          kubernetes.io/dockerconfigjson        1         16d
    default-icr-io                             kubernetes.io/dockerconfigjson        1         16d
    ```
    {: screen}
3.  Copy each image pull secret from the `default` project to the project of your choice. The new image pull secrets are named `<project_name>-icr-<region>-io`. If you pull images from only a certain region, you can copy only that region's image pull secret.
    ```
    oc get secret default-us-icr-io -n default -o yaml | sed 's/default/<new-project>/g' | oc -n <new-project> create -f -   
    ```
    {: pre}
    ```
    oc get secret default-uk-icr-io -n default -o yaml | sed 's/default/<new-project>/g' | oc -n <new-project> create -f -
    ```
    {: pre}
    ```
    oc get secret default-de-icr-io -n default -o yaml | sed 's/default/<new-project>/g' | oc -n <new-project> create -f -
    ```
    {: pre}
    ```
    oc get secret default-au-icr-io -n default -o yaml | sed 's/default/<new-project>/g' | oc -n <new-project> create -f -
    ```
    {: pre}
    ```
    oc get secret default-jp-icr-io -n default -o yaml | sed 's/default/<new-project>/g' | oc -n <new-project> create -f -
    ```
    {: pre}
    ```
    oc get secret default-icr-io -n default -o yaml | sed 's/default/<new-project>/g' | oc -n <new-project> create -f -
    ```
    {: pre}
4.  Verify that the secrets are created successfully.
    ```
    oc get secrets -n <project_name>
    ```
    {: pre}
5.  [Use the image pull secret to deploy containers](#use_imagePullSecret). You can choose between referring to the image pull secret separately in each deployment, or adding the image pull secret to a Kubernetes service account so that any pod in the project can use the image pull secret when you deploy a container.

### Creating an image pull secret with different IAM API key credentials for more control or access to images in other {{site.data.keyword.cloud_notm}} accounts
{: #other_registry_accounts}

You can assign {{site.data.keyword.cloud_notm}} IAM access policies to users or a service ID to restrict permissions to specific registry image namespaces or actions (such as `push` or `pull`). Then, create an API key and store these registry credentials in an image pull secret for your cluster.
{: shortdesc}

For example, to access images in other {{site.data.keyword.cloud_notm}} accounts, create an API key that stores the {{site.data.keyword.registryshort_notm}} credentials of a user or service ID in that account. Then, in your cluster's account, save the API key credentials in an image pull secret for each cluster and cluster project.

The following steps create an API key that stores the credentials of an {{site.data.keyword.cloud_notm}} IAM service ID. Instead of using a service ID, you might want to create an API key for a user ID that has an {{site.data.keyword.cloud_notm}} IAM service access policy to {{site.data.keyword.registryshort_notm}}. However, make sure that the user is a functional ID or have a plan in case the user leaves so that the cluster can still access the registry.
{: note}

1.  List available OpenShift projects in your cluster, or create a project to use where you want to deploy containers from your registry images.
    ```
    oc get projects
    ```
    {: pre}

    Example output:
    ```
    default          Active    79d
    ibm-cert-store   Active    79d
    ibm-system       Active    79d
    kube-public      Active    79d
    kube-system      Active    79d
    ```
    {: screen}

    To create a project:
    ```
    oc new-project <project_name>
    ```
    {: pre}
2.  Create an {{site.data.keyword.cloud_notm}} IAM service ID for your cluster that is used for the IAM policies and API key credentials in the image pull secret. Be sure to give the service ID a description that helps you retrieve the service ID later, such as including both the cluster and project name.
    ```
    ibmcloud iam service-id-create <cluster_name>-<project>-id --description "Service ID for IBM Cloud Container Registry in Kubernetes cluster <cluster_name> project <project>"
    ```
    {: pre}
3.  Create a custom {{site.data.keyword.cloud_notm}} IAM policy for your cluster service ID that grants access to {{site.data.keyword.registryshort_notm}}.
    ```
    ibmcloud iam service-policy-create <cluster_service_ID> --roles <service_access_role> --service-name container-registry [--region <IAM_region>] [--resource-type namespace --resource <registry_namespace>]
    ```
    {: pre}
    <table>
    <caption>Understanding this command's components</caption>
    <thead>
    <th colspan=2><img src="images/idea.png" alt="Idea icon"/> Understanding this command's components</th>
    </thead>
    <tbody>
    <tr>
    <td><code><em>&lt;cluster_service_ID&gt;</em></code></td>
    <td>Required. Replace with the `<cluster_name>-<kube_namespace>-id` service ID that you previously created for your Kubernetes cluster.</td>
    </tr>
    <tr>
    <td><code>--service-name <em>container-registry</em></code></td>
    <td>Required. Enter `container-registry` so that the IAM policy is for {{site.data.keyword.registrylong_notm}}.</td>
    </tr>
    <tr>
    <td><code>--roles <em>&lt;service_access_role&gt;</em></code></td>
    <td>Required. Enter the [service access role for {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=registry-iam#service_access_roles) that you want to scope the service ID access to. Possible values are `Reader`, `Writer`, and `Manager`.</td>
    </tr>
    <tr>
    <td><code>--region <em>&lt;IAM_region&gt;</em></code></td>
    <td>Optional. If you want to scope the access policy to certain IAM regions, enter the regions in a comma-separated list. Possible values are `au-syd`, `eu-gb`, `eu-de`, `jp-tok`, `us-south`, and `global`.</td>
    </tr>
    <tr>
    <td><code>--resource-type <em>namespace</em> --resource <em>&lt;registry_namespace&gt;</em></code></td>
    <td>Optional. If you want to limit access to only images in certain [{{site.data.keyword.registrylong_notm}} namespaces](/docs/Registry?topic=registry-registry_overview#registry_namespaces), enter `namespace` for the resource type and specify the `<registry_namespace>`. To list registry namespaces, run `ibmcloud cr namespaces`.</td>
    </tr>
    </tbody></table>
4.  Create an API key for the service ID. Name the API key similar to your service ID, and include the service ID that you previously created, ``<cluster_name>-<kube_namespace>-id`. Be sure to give the API key a description that helps you retrieve the key later.
    ```
    ibmcloud iam service-api-key-create <cluster_name>-<kube_namespace>-key <cluster_name>-<kube_namespace>-id --description "API key for service ID <service_id> in Kubernetes cluster <cluster_name> namespace <kube_namespace>"
    ```
    {: pre}
5.  Retrieve your **API Key** value from the output of the previous command.
    ```
    Please preserve the API key! It cannot be retrieved after it's created.

    Name          <cluster_name>-<kube_namespace>-key   
    Description   key_for_registry_for_serviceid_for_kubernetes_cluster_multizone_namespace_test   
    Bound To      crn:v1:bluemix:public:iam-identity::a/1bb222bb2b33333ddd3d3333ee4ee444::serviceid:ServiceId-ff55555f-5fff-6666-g6g6-777777h7h7hh   
    Created At    2019-02-01T19:06+0000   
    API Key       i-8i88ii8jjjj9jjj99kkkkkkkkk_k9-llllll11mmm1   
    Locked        false   
    UUID          ApiKey-222nn2n2-o3o3-3o3o-4p44-oo444o44o4o4   
    ```
    {: screen}
6.  Create a Kubernetes image pull secret to store the API key credentials in the cluster's namespace. Repeat this step for each `icr.io` domain, OpenShift project, and cluster that you want to pull images from registry with this service ID's IAM credentials.
    ```
    oc --namespace <project> create secret docker-registry <secret_name> --docker-server=<registry_URL> --docker-username=iamapikey --docker-password=<api_key_value> --docker-email=<docker_email>
    ```
    {: pre}

    <table>
    <caption>Understanding this command's components</caption>
    <thead>
    <th colspan=2><img src="images/idea.png" alt="Idea icon"/> Understanding this command's components</th>
    </thead>
    <tbody>
    <tr>
    <td><code>--namespace <em>&lt;project&gt;</em></code></td>
    <td>Required. Specify the OpenShift project of your cluster that you used for the service ID name.</td>
    </tr>
    <tr>
    <td><code><em>&lt;secret_name&gt;</em></code></td>
    <td>Required. Enter a name for your image pull secret.</td>
    </tr>
    <tr>
    <td><code>--docker-server <em>&lt;registry_URL&gt;</em></code></td>
    <td>Required. Set the URL to the image registry where your registry namespace is set up. Available registry domains:<ul>
    <li>AP North (Tokyo): `jp.icr.io`</li>
    <li>AP South (Sydney): `au.icr.io`</li>
    <li>EU Central (Frankfurt): `de.icr.io`</li>
    <li>UK South (London): `uk.icr.io`</li>
    <li>US South (Dallas): `us.icr.io`</li></ul></td>
    </tr>
    <tr>
    <td><code>--docker-username iamapikey</code></td>
    <td>Required. Enter the username to log in to your private registry. For {{site.data.keyword.registryshort_notm}}, the username is set to the value <strong><code>iamapikey</code></strong>.</td>
    </tr>
    <tr>
    <td><code>--docker-password <em>&lt;token_value&gt;</em></code></td>
    <td>Required. Enter the value of your **API Key** that you previously retrieved.</td>
    </tr>
    <tr>
    <td><code>--docker-email <em>&lt;docker-email&gt;</em></code></td>
    <td>Required. If you have one, enter your Docker email address. If you do not, enter a fictional email address, such as `a@b.c`. This email is required to create a Kubernetes secret, but is not used after creation.</td>
    </tr>
    </tbody></table>
7.  Verify that the secret was created successfully. Replace <em>&lt;kubernetes_namespace&gt;</em> with the namespace where you created the image pull secret.

    ```
    oc get secrets --namespace <project>
    ```
    {: pre}
8.  [Add the image pull secret to a Kubernetes service account so that any pod in the project can use the image pull secret when you deploy a container](#use_imagePullSecret).

### Accessing images that are stored in other private registries
{: #private_images}

If you already have a private registry, you must store the registry credentials in a Kubernetes image pull secret and reference this secret from your configuration file.
{:shortdesc}

Before you begin:

1.  [Create a cluster](/docs/openshift?topic=openshift-clusters).
2.  [Access your OpenShift cluster](/docs/openshift?topic=openshift-access_cluster).

To create an image pull secret:

1.  Create the Kubernetes secret to store your private registry credentials.

    ```
    oc --namespace <project> create secret docker-registry <secret_name>  --docker-server=<registry_URL> --docker-username=<docker_username> --docker-password=<docker_password> --docker-email=<docker_email>
    ```
    {: pre}

    <table>
    <caption>Understanding this command's components</caption>
    <thead>
    <th colspan=2><img src="images/idea.png" alt="Idea icon"/> Understanding this command's components</th>
    </thead>
    <tbody>
    <tr>
    <td><code>--namespace <em>&lt;project&gt;</em></code></td>
    <td>Required. The OpenShift project of your cluster where you want to use the secret and deploy containers to. To list available projects in your cluster, run <code>oc get projects</code>.</td>
    </tr>
    <tr>
    <td><code><em>&lt;secret_name&gt;</em></code></td>
    <td>Required. The name that you want to use for your <code>imagePullSecret</code>.</td>
    </tr>
    <tr>
    <td><code>--docker-server <em>&lt;registry_URL&gt;</em></code></td>
    <td>Required. The URL to the registry where your private images are stored.</td>
    </tr>
    <tr>
    <td><code>--docker-username <em>&lt;docker_username&gt;</em></code></td>
    <td>Required. The username to log in to your private registry.</td>
    </tr>
    <tr>
    <td><code>--docker-password <em>&lt;token_value&gt;</em></code></td>
    <td>Required. The value of your registry token that you retrieved earlier.</td>
    </tr>
    <tr>
    <td><code>--docker-email <em>&lt;docker-email&gt;</em></code></td>
    <td>Required. If you have one, enter your Docker email address. If you do not have one, enter a fictional email address, such as `a@b.c`. This email is required to create a Kubernetes secret, but is not used after creation.</td>
    </tr>
    </tbody></table>

2.  Verify that the secret was created successfully. Replace <em>&lt;project&gt;</em> with the name of the project where you created the `imagePullSecret`.

    ```
    oc get secrets --namespace <project>
    ```
    {: pre}

3.  [Create a pod that references the image pull secret](#use_imagePullSecret).

<br />


## Using the image pull secret to deploy containers
{: #use_imagePullSecret}

You can define an image pull secret in your pod deployment or store the image pull secret in your Kubernetes service account so that it is available for all deployments that do not specify a service account.
{: shortdesc}

Choose between the following options:
* [Referring to the image pull secret in your pod deployment](#pod_imagePullSecret): Use this option if you do not want to grant access to your registry for all pods in your project by default.
* [Storing the image pull secret in the Kubernetes service account](#store_imagePullSecret): Use this option to grant access to images in your registry for all deployments in the selected OpenShift projects.

Before you begin:
* [Create an image pull secret](#other) to access images in other registries or OpenShift projects other than `default`.
* [Access your OpenShift cluster](/docs/openshift?topic=openshift-access_cluster).

### Referring to the image pull secret in your pod deployment
{: #pod_imagePullSecret}

When you refer to the image pull secret in a pod deployment, the image pull secret is valid for this pod only and cannot be shared across pods in the OpenShift project.
{:shortdesc}

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
    <thead>
    <th colspan=2><img src="images/idea.png" alt="Idea icon"/> Understanding the YAML file components</th>
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

### Storing the image pull secret in the Kubernetes service account for the selected project
{:#store_imagePullSecret}

Every OpenShift project has a Kubernetes service account that is named `default`. You can add the image pull secret to this service account to grant access to images in your registry. Deployments that do not specify a service account automatically use the `default` service account for this OpenShift project.
{:shortdesc}

1. Check if an image pull secret already exists for your default service account.
   ```
   oc describe serviceaccount default -n <project_name>
   ```
   {: pre}
   When `<none>` is displayed in the **Image pull secrets** entry, no image pull secret exists.  
2. Add the image pull secret to your default service account.
   - **To add the image pull secret when no image pull secret is defined:**
       ```
       oc patch -n <project_name> serviceaccount/default -p '{"imagePullSecrets":[{"name": "<image_pull_secret_name>"}]}'
       ```
       {: pre}
   - **To add the image pull secret when an image pull secret is already defined:**
       ```
       oc patch -n <project_name> serviceaccount/default --type='json' -p='[{"op":"add","path":"/imagePullSecrets/-","value":{"name":"<image_pull_secret_name>"}}]'
       ```
       {: pre}
3. Verify that your image pull secret was added to your default service account.
   ```
   oc describe serviceaccount default -n <project_name>
   ```
   {: pre}

   Example output:
   ```
   Name:                default
   Namespace:           <namespace_name>
   Labels:              <none>
   Annotations:         <none>
   Image pull secrets:  <image_pull_secret_name>
   Mountable secrets:   default-token-sh2dx
   Tokens:              default-token-sh2dx
   Events:              <none>
   ```
   {: pre}

4. Deploy a container from an image in your registry.
   ```yaml
   apiVersion: v1
   kind: Pod
   metadata:
     name: mypod
   spec:
     containers:
       - name: <container_name>
         image: <region>.icr.io/<namespace_name>/<image_name>:<tag>
   ```
   {: codeblock}

5. Create the deployment in the cluster.
   ```
   oc apply -f mypod.yaml
   ```
   {: pre}

<br />


## Setting up a cluster to pull entitled software
{: #secret_entitled_software}

You can set up your Red Hat OpenShift on IBM Cloud cluster to pull entitled software, which is a collection of protected container images that are packaged in Helm charts that you are licensed to use by IBM. Entitled software is stored in a special {{site.data.keyword.registrylong_notm}} `cp.icr.io` domain. To access this domain, you must create an image pull secret with an entitlement key for your cluster and add this image pull secret to the Kubernetes service account of each project where you want to deploy this entitled software.
{: shortdesc}

Do you have older entitled software from Passport Advantage? Use the [PPA importer tool](/docs/containers?topic=containers-hybrid_iks_icp#hybrid_ppa_importer) instead to deploy this software in your cluster.
{: tip}

Before you begin: [Access your OpenShift cluster](/docs/openshift?topic=openshift-access_cluster).

1.  Get the entitlement key for your entitled software library.
    1.  Log in to [MyIBM.com](https://myibm.ibm.com){: external} and scroll to the **Container software library** section. Click **View library**.
    2.  From the **Access your container software > Entitlement keys** page, click **Copy key**. This key authorizes access to all the entitled software in your container software library.
2.  In the project that you want to deploy your entitled containers, create an image pull secret so that you can access the `cp.icr.io` entitled registry. For more information, see [Accessing images that are stored in other private registries](#private_images).
    ```
    oc create secret docker-registry entitled-cp-icr-io --docker-server=cp.icr.io --docker-username=cp --docker-password=<entitlement_key> --docker-email=<docker_email> -n <project>
    ```
    {: pre}
3.  Add the image to the service account of the namespace so that any container in the project can use the entitlement key to pull entitled images. For more information, see [Using the image pull secret to deploy containers](#use_imagePullSecret).
    ```
    oc patch -n <project> serviceaccount/default --type='json' -p='[{"op":"add","path":"/imagePullSecrets/","value":{"name":"entitled-cp-icr-io"}}]'
    ```
    {: pre}
4.  Create a pod in the project that builds a container from an image in the entitled registry.
    ```
    oc run <pod_name> --image=cp.icr.io/<image_name> -n <project>
    ```
    {: pre}
5.  Check that your container was able to successfully build from the entitled image by verifying that the pod is in a **Running** status.
    ```
    oc get pod <pod_name> -n <project>
    ```
    {: pre}

Wondering what to do next? You can [set up the **entitled** Helm chart repository](/docs/openshift?topic=openshift-helm), where Helm charts that incorporate entitled software are stored. If you already have Helm installed in your cluster, run `helm repo add entitled https://raw.githubusercontent.com/IBM/charts/master/repo/entitled`.
{: tip}

<br />






