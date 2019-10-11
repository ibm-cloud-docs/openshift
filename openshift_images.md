---

copyright:
  years: 2014, 2019
lastupdated: "2019-10-11"

keywords: openshift, roks, rhoks, rhos

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

# Building images for your apps 
{: #openshift-images}

{{site.data.keyword.openshiftlong}} clusters include an internal registry to build, deploy, and manage container images locally. For a private registry to manage and control access to images across your enterprise, you can also set up your cluster to use {{site.data.keyword.registrylong}}.
{: shortdesc}

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
        <td>Your cluster is set up with the internal OpenShift Container Registry so that OpenShift can automatically build, deploy, and manage your application lifecycle from within the cluster. Images are stored in a backing {{site.data.keyword.cloud_notm}} classic block storage device that is provisioned at cluster creation time. If you need more storage, you can resize the device.
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
        <li>[Automatically scanning](/docs/services/Registry?topic=va-va_index) the vulnerability of images.</li>
        <li>Controlling access through [{{site.data.keyword.cloud_notm}} IAM policies](/docs/services/Registry?topic=registry-user) and [separate regional registries](/docs/services/Registry?topic=registry-registry_overview#registry_regions).</li>
        <li>[Retaining images](/docs/services/Registry?topic=registry-registry_retention) without requiring storage space in your cluster or an attached storage device. You can also set policies to manage the quantity of images to prevent them from taking up too much space.</li>
        <li>Using the private service endpoint so that clusters on only the private network can still access the registry.</li>
        <li>[Setting storage and image pull traffic quotas](/docs/services/Registry?topic=registry-registry_quota) to better control image storage, usage, and billing.</li>
        <li>Pulling licensed IBM content from the [entitled registry](/docs/containers?topic=containers-images#secret_entitled_software).</li></ul>
        <br>To get started, see the following topics:<ul>
        <li>[Getting started with {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-getting-started).</li>
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

OpenShift clusters are set up by default with an internal registry. When you delete the cluster, the internal registry and its images are also deleted. If you want to persist your images, consider using a private registry such as {{site.data.keyword.registrylong_notm}}, backing up your images to persistent storage such as {{site.data.keyword.objectstorageshort}}, or creating a separate, stand-alone OpenShift container registry (OCR) cluster. For more information, see the [OpenShift docs ![External link icon](../icons/launch-glyph.svg "External link icon")](https://docs.openshift.com/container-platform/3.11/install_config/registry/index.html#install-config-registry-overview).
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

If your registry needs additional gigabytes of storage for your images, you can resize the file storage volume. For more information, see [Changing the size and IOPS of your existing storage device](/docs/openshift?topic=openshift-file_storage#file_change_storage_configuration). When you resize the volume in your IBM Cloud infrastructure account, the attached PVC description is not updated. Instead, you can log in to the `docker-registry` pod that uses the `registry-backing` PVC to verify that the volume is resized.
{: note}

### Setting up a secure external route for the internal registry
{: #route_internal_registry}

By default, your OpenShift cluster has an internal registry that is available through a service with an internal IP address. If you want to make the internal registry available on the public network, you can set up a secure re-encrypt route. For example, you might set up your cluster's internal registry to act as a public registry for deployments in other projects or clusters.
{: shortdesc}

Before you begin: 
*  Confirm that you have the [**Manager** {{site.data.keyword.cloud_notm}} IAM service role](/docs/openshift?topic=openshift-access_reference#service) for the cluster.
*  Make sure that your cluster has public network connectivity to expose the internal registry with a public route.
*  Install Docker on your local machine.
*  [Access your OpenShift cluster](/docs/openshift?topic=openshift-openshift_access_cluster).

To use the internal registry, set up a public route to access the registry. Then, create an image pull secret that includes the credentials to access the registry so that deployments in other projects can pull images from this registry.

1.  From the `default` project, make sure that the `docker-registry` service exists for the internal registry.
    ```
    oc get svc
    ```
    {: pre}

    Example output:
    ```
    NAME               TYPE           CLUSTER-IP       EXTERNAL-IP     PORT(S)                      AGE
    docker-registry    ClusterIP      172.21.xxx.xxx    <none>          5000/TCP                     36d
    kubernetes         ClusterIP      172.21.xxx.xxx    <none>          443/TCP,53/UDP,53/TCP        36d
    registry-console   ClusterIP      172.21.xxx.xxx    <none>          9000/TCP                     36d
    router             LoadBalancer   172.21.xxx.xxx    169.xx.xxx.xxx   80:31049/TCP,443:30219/TCP   36d
    ```
    {: screen}
2.  Create a secured route for the `docker-registry` service that uses `reencrypt` TLS termination. With re-encryption, the router terminates the TLS connection with a certificate, and then re-encrypts the connection to the internal registry with a different certificate. With this approach, the full path of the connection between the user and the internal registry is encrypted. To provide your own custom domain name, include the `--hostname` flag.
    ```
    oc create route reencrypt --service=docker-registry
    ```
    {: pre}
3.  Retrieve the hostname (**HOST/PORT**) and the **PORT** that were assigned to the `docker-registry` route.
    ```
    oc get route docker-registry
    ```
    {: pre}
    Example output:
    ```
    NAME              HOST/PORT                                                                                                  PATH      SERVICES          PORT       TERMINATION   WILDCARD
    docker-registry   docker-registry-default.<cluster_name>-<ID_string>.<region>.containers.appdomain.cloud             docker-registry   5000-tcp   reencrypt     None
    ```
    {: screen}
4.  Edit the route to set the [load balancing strategy ![External link icon](../icons/launch-glyph.svg "External link icon")](https://docs.openshift.com/container-platform/3.11/architecture/networking/routes.html#load-balancing) to `source` so that the same client IP address reaches the same server, as in a passthrough route setup. You can set the strategy by adding an annotation in the `metadata.annotations` section: `haproxy.router.openshift.io/balance: source`. You can edit the configuration file from the **OpenShift Application Console** or in your terminal by running the following command.
    ```
    oc edit route docker-registry
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
    docker login -u $(oc whoami) -p $(oc whoami -t) docker-registry-default.<cluster_name>-<ID_string>.<region>.containers.appdomain.cloud
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
        docker tag hello-world:latest docker-registry-default.<cluster_name>-<ID_string>.<region>.containers.appdomain.cloud/<project>/<image_name>:<tag>
        ```
        {: pre}
    3.  Push the image to your cluster's internal registry.
        ```
        docker push docker-registry-default.<cluster_name>-<ID_string>.<region>.containers.appdomain.cloud/<project>/<image_name>:<tag>
        ```
        {: pre}
    4.  Verify that the image is added to the OpenShift image stream.
        ```
        oc get imagestream
        ```
        {: pre}

        Example output:
        ```
        NAME          DOCKER REPO                                            TAGS      UPDATED
        hello-world   docker-registry.default.svc:5000/default/hello-world   latest    7 hours ago
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
        * **--docker-server**: Instead of the internal service IP address (`172.21.xxx.xxx:5000`), enter the hostname of the `docker-registry` route with the port (`docker-registry-default.<cluster_name>-<ID_string>.<region>.containers.appdomain.cloud:5000`).
        * **--docker-username**: Copy the `"username"` from the previous image pull secret, such as `serviceaccount`.
        * **--docker-password**: Copy the `"password"` from the previous image pull secret.
        * **--docker-email**: If you have one, enter your Docker email address. If you do not, enter a fictional email address, such as `a@b.c`. This email is required to create a Kubernetes secret, but is not used after creation.
        
        ```
        oc create secret docker-registry internal-registry --namespace default --docker-server docker-registry-default.<cluster_name>-<ID_string>.<region>.containers.appdomain.cloud:5000 --docker-username serviceaccount --docker-password <eyJ...> --docker-email a@b.c
        ```
        {: pre}
    5.  Add the image pull secret to the default service account of your project.
        ```
        oc patch -n <namespace_name> serviceaccount/default --type='json' -p='[{"op":"add","path":"/imagePullSecrets/-","value":{"name":"<image_pull_secret_name>"}}]'
        ```
        {: pre}
    6.  Repeat these steps for each project that you want to pull images from the internal registry.

Now that you set up the internal registry with an accessible route, you can log in, push, and pull images to the registry. For more information, see the [OpenShift documentation ![External link icon](../icons/launch-glyph.svg "External link icon")](/container-platform/3.11/install_config/registry/accessing_registry.html#access-logging-in-to-the-registry).

<br />


## Using {{site.data.keyword.registrylong_notm}}
{: #openshift_iccr}

By default, your Red Hat OpenShift on IBM Cloud cluster is set up to pull images from the remote, private {{site.data.keyword.registrylong_notm}} `icr.io` domains in the `default` project. If you want to use images that are stored in {{site.data.keyword.registrylong_notm}} for other projects, you must create image pull secrets for each global and regional registry. Then, add the image pull secrets to each project, and to a service account for each project or to each deployment.
{: shortdesc}

For more information, see the following topics in the {{site.data.keyword.containershort_notm}} docs.
* [Understanding how to authorize your cluster to pull images from a registry](/docs/containers?topic=containers-images#cluster_registry_auth).
* [Copying the `default-<region>-icr-io` secrets](/docs/containers?topic=containers-images#copy_imagePullSecret) from the `default` namespace to the namespace that you want to pull images from.
* [Creating your own image pull secret](/docs/containers?topic=containers-images#other_registry_accounts).
* [Adding the image pull secret](/docs/containers?topic=containers-images#use_imagePullSecret) to your deployment configuration or to the namespace service account.
