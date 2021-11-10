---

copyright:
  years: 2014, 2021
lastupdated: "2021-11-10"

keywords: openshift, registry, pull secret, secrets

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}


# Setting up an image registry
{: #registry}





{{site.data.keyword.openshiftlong}} clusters include an internal registry to build, deploy, and manage container images locally. For a private registry to manage and control access to images across your enterprise, you can also set up your cluster to use {{site.data.keyword.registrylong}}.
{: shortdesc}



<openshift-chunk>

## Choosing an image registry solution
{: #openshift_registry_options}

Your app's images must be stored in a container registry that your cluster can access to deploy apps into your cluster. You can choose to use the built-in registry of your {{site.data.keyword.openshiftshort}} cluster, a private registry with access restricted to select users, or a public registry. Review the following table to choose the best option for your use case.
{: shortdesc}

Internal {{site.data.keyword.openshiftshort}} Container Registry (OCR)
:   Your cluster is set up with the internal {{site.data.keyword.openshiftshort}} Container Registry so that {{site.data.keyword.openshiftshort}} can automatically build, deploy, and manage your application lifecycle from within the cluster. Images are stored in a backing {{site.data.keyword.cloud_notm}} classic file storage device that is provisioned at cluster creation time. If you need more storage, you can resize the device. Use cases:
    - {{site.data.keyword.openshiftshort}}-native image stream, build, and app deployment process on a per cluster basis.
    - Images can be shared across all projects in the cluster, with access that is controlled through RBAC roles.
    - Integrating the internal registry with other Red Hat products like CloudForms for extended features such as vulnerability scanning.
    - Option to expose the internal registry with a route so that users can pull images from the registry over the public network.
    - Option to set up the internal registry to [pull images](#imagestream_registry) from or [push images](#builds_registry) to a private registry such as {{site.data.keyword.registrylong_notm}}.
    For more information, see [Using the internal registry](#openshift_internal_registry).

Private registry
:   Private registries are a good choice to protect your images from unauthorized users. Private registries must be set up by the cluster administrator to make sure that access, storage quotas, image trust and other features work as intended. By default, your [{{site.data.keyword.openshiftshort}} clusters](#openshift_iccr) are integrated with the private {{site.data.keyword.registrylong_notm}} through image pull secrets in the `default` project. {{site.data.keyword.registrylong_notm}} is a highly available, multi-tenant private registry to store your own images. You can also pull IBM-provided images from the global `icr.io` registry, and licensed software from the entitled registry. With {{site.data.keyword.registrylong_notm}}, you can manage images for multiple clusters with integration with {{site.data.keyword.cloud_notm}} IAM and billing. Advantages of using {{site.data.keyword.registrylong_notm}} with the internal registry:
    - Local image caching for faster builds via the internal registry.
    - Deployments in other projects can see the image stream so that you don't have to copy pull secrets to each project.
    - Sharing images across multiple clusters without needing to push images to multiple registries.</li>
    - [Automatically scanning](/docs/Registry?topic=va-va_index) the vulnerability of images.
    - Controlling access through [{{site.data.keyword.cloud_notm}} IAM policies](/docs/Registry?topic=Registry-user) and [separate regional registries](/docs/Registry?topic=Registry-registry_overview#registry_regions).
    - [Retaining images](/docs/Registry?topic=Registry-registry_retention) without requiring storage space in your cluster or an attached storage device. You can also set policies to manage the quantity of images to prevent them from taking up too much space.
    - Version 4 clusters on VPC infrastructure: Using the private registry service endpoint so that clusters that use only a private cloud service endpoint can still access the registry.
    - [Setting storage and image pull traffic quotas](/docs/Registry?topic=Registry-registry_quota) to better control image storage, usage, and billing.
    - Pulling licensed IBM content from the [entitled registry](/docs/openshift?topic=openshift-registry#secret_entitled_software).
    To get started, see the following topics:
    - [Getting started with {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-getting-started).  
    - [Importing images from {{site.data.keyword.registrylong_notm}}](#imagestream_registry) into the internal registry image stream.  
    - [Using {{site.data.keyword.registrylong_notm}}](#openshift_iccr).

Public registry
:   Public registries such as Docker Hub are a way to share images across teams, companies, clusters, or cloud providers. Some public registries might also offer a private registry component. Use cases:
    - Pushing and pulling images on the public network.
    - Quick testing of a container across cloud providers.
    - Don't need enterprise-grade features such as vulnerability scanning or access management.
    For more information, see the public registry's documentation, such as [Quay](https://quay.io/){: external} or [Docker Hub](https://hub.docker.com/).


## Storing images in the internal registry
{: #openshift_internal_registry}

{{site.data.keyword.openshiftshort}} clusters have an internal registry by default. The images in the internal registry are backed up, but vary depending on the infrastructure provider of your {{site.data.keyword.openshiftlong_notm}} cluster.
{: shortdesc}

- ![Classic infrastructure provider icon.](images/icon-classic-2.svg) <img src="images/icon-version-311.png" alt="Version 3.11 icon" width="30" style="width:30px; border-style: none"/> <img src="images/icon-version-43.png" alt="Version 4 icon" width="30" style="width:30px; border-style: none"/> **Classic clusters**: Your {{site.data.keyword.openshiftshort}} cluster is set up by default with an internal registry that uses classic {{site.data.keyword.cloud_notm}} File Storage as the backing storage. When you delete the cluster, the internal registry and its images are also deleted. If you want to persist your images, consider using a private registry such as {{site.data.keyword.registrylong_notm}}, backing up your images to persistent storage such as {{site.data.keyword.objectstorageshort}}, or creating a separate, stand-alone {{site.data.keyword.openshiftshort}} container registry (OCR) cluster. For more information, see the [{{site.data.keyword.openshiftshort}} docs](https://docs.openshift.com/container-platform/4.7/registry/architecture-component-imageregistry.html){: external}.
- ![VPC infrastructure provider icon.](images/icon-vpc-2.svg) <img src="images/icon-version-43.png" alt="Version 4 icon" width="30" style="width:30px; border-style: none"/> **VPC clusters (version 4 only)**: The internal registry of your {{site.data.keyword.openshiftshort}} cluster backs up your images to a bucket that is automatically created in an {{site.data.keyword.cos_full_notm}} instance in your account. Any data that is stored in the object storage bucket remains even if you delete the cluster.
- **Classic, VPC, or {{site.data.keyword.satelliteshort}} clusters**: You can optionally choose to set up the internal registry to store data in the `emptyDir` of the worker node where the internal registry pod runs. Keep in mind that this data is not persistent, and if the pod or worker node is restarted, the stored data is deleted and unrecoverable. You might store the images locally in the `emptyDir` to increase performance if you build containers from large images regularly.

### VPC: Backing up your {{site.data.keyword.openshiftshort}} internal image registry to {{site.data.keyword.cos_full_notm}}
{: #cos_image_registry}

Your images in your {{site.data.keyword.openshiftshort}} cluster internal registry are automatically backed up to an {{site.data.keyword.cos_full_notm}} bucket. Any data that is stored in the object storage bucket remains even if you delete the cluster.
{: shortdesc}

![VPC infrastructure provider icon.](images/icon-vpc-2.svg) <img src="images/icon-version-43.png" alt="Version 4 icon" width="30" style="width:30px; border-style: none"/> The internal registry is backed up to {{site.data.keyword.cos_full_notm}} only for {{site.data.keyword.openshiftlong_notm}} clusters that run version 4 on VPC infrastructure.
{: note}

However, if the bucket fails to create when you create your cluster, you must manually create a bucket and set up your cluster to use the bucket. In the meantime, the internal registry uses an `emptyDir` Kubernetes volume that stores your container images on the secondary disk of your worker node. The `emptyDir` volumes are not considered persistent highly available storage, and if you delete the pods that use the image, the image is automatically deleted.

To manually create a bucket for your internal registry, see [Cluster create error about cloud object storage bucket](/docs/openshift?topic=openshift-ts_cos_bucket_cluster_create).

### Classic: Storing images in the internal registry
{: #storage_internal_registry}

![Classic infrastructure provider icon.](images/icon-classic-2.svg) By default, your {{site.data.keyword.openshiftshort}} cluster's internal registry uses an [{{site.data.keyword.cloud_notm}} File Storage](/docs/openshift?topic=openshift-file_storage) volume to store the registry images. You can review the default size of the storage volume, or update the volume size.
{: shortdesc}

**Viewing volume details**

To view volume details including the storage class and size, you can describe the persistent volume claim.

**Version 4**

```sh
oc describe pvc -n openshift-image-registry image-registry-storage
```
{: pre}

**Version 3**

```sh
oc describe pvc registry-backing -n default
```
{: pre}

**Changing volume details**:
If your registry needs additional gigabytes of storage for your images, you can resize the file storage volume. For more information, see [Changing the size and IOPS of your existing storage device](/docs/openshift?topic=openshift-file_storage#file_change_storage_configuration). When you resize the volume in your IBM Cloud infrastructure account, the attached PVC description is not updated. Instead, you can log in to the `openshift-image-registry` ({{site.data.keyword.openshiftshort}} 4) or `docker-registry` ({{site.data.keyword.openshiftshort}} 3.11) pod that uses the `registry-backing` PVC to verify that the volume is resized.

<img src="images/icon-version-311.png" alt="Version 3.11 icon" width="30" style="width:30px; border-style: none"/> **{{site.data.keyword.openshiftshort}} 3.11 only**: Don't change the name of the `registry-backing` PVC, even if you change the volume details. Any master operation, such as patch version update or API server refresh, reverts the PVC name back to `registry-backing`, and the custom-named PVC becomes inaccessible.
{: important}

### Storing images in the worker node empty directory
{: #emptydir_internal_registry}

You might store the internal registry images locally in the `emptyDir` of the worker node, such as a bare metal worker node, to increase performance if you build containers from large images regularly. 
{: shortdesc}

Keep in mind that this data is not persistent, and if the pod or worker node is restarted, the stored data is deleted and unrecoverable.
{: important}

1. [Access your {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-access_cluster).
2. [Update the image registry operator configmap](https://docs.openshift.com/container-platform/4.7/registry/configuring_registry_storage/configuring-registry-storage-baremetal.html#installation-registry-storage-non-production_configuring-registry-storage-baremetal){: external} to set the storage to use the `emptyDir` of the worker node.
    ```sh
    oc patch configs.imageregistry.operator.openshift.io/cluster --type merge --patch '{"spec":{"storage":{"emptyDir":{}}}}'
    ```
    {: pre}

3. If the [image registry operator management state](https://docs.openshift.com/container-platform/4.7/registry/configuring-registry-operator.html#registry-operator-configuration-resource-overview_configuring-registry-operator){: external} is set to `Unmanaged`, such as in {{site.data.keyword.satelliteshort}} clusters, update the management state to `Managed`. Now, the operator updates the internal registry pod.
    ```sh
    oc patch configs.imageregistry.operator.openshift.io/cluster --type merge -p '{"spec":{"managementState":"Managed"}}'
    ```
    {: pre}

4. Get the details of the internal registry pod so that you can verify your updates.
    1. Check that the `image-registry` pod is running and that a pod runs per worker node in the cluster.

        ```sh
        oc get pods -n openshift-image-registry
        ```
        {: pre}

        Example output

        ```sh
        NAME                                               READY   STATUS    RESTARTS   AGE
        cluster-image-registry-operator-695bf78ffc-zvkhd   2/2     Running   0          33m
        image-registry-6774598589-65cnx                    1/1     Running   0          112s
        node-ca-gg66r                                      1/1     Running   0          113s
        node-ca-n8jpq                                      1/1     Running   0          113s
        node-ca-p2d7j                                      1/1     Running   0          113s
        ```
        {: screen}

    2. Get the public IP address of the **Node** that the `image-registry` pod runs on.

        ```sh
        oc describe pod -n openshift-image-registry <image-registry-pod> | grep Node
        ```
        {: pre}

        Example output

        ```sh
        Node:               169.xx.xxx.xxx/169.xx.xxx.xxx
        ```
        {: screen}

        If the worker node IP address is private, run `ibmcloud oc worker ls -c <cluster> | grep <private_IP>` and note the corresponding public IP address.
        {: tip}

    3. Get the **UID** of the `image-registry` pod in the `metadata.uid` section in the pod YAML (not the UID of the replica set in the `metadata.ownerReferences.uid` section).

        ```sh
        oc get pod -n openshift-image-registry <image-registry-pod> -o yaml
        ```
        {: pre}  

        Example output

        ```yaml
        apiVersion: v1
        kind: Pod
        metadata:
            uid: e8d7718d-b0bd-47e2-9aaa-05f3a608fd9b
        ...
        ```
        {: screen}

5. Verify that the internal registry stores data to the `emptyDir` of the worker node.
    1. [Access the registry directly from the cluster](https://docs.openshift.com/container-platform/4.7/registry/accessing-the-registry.html#registry-accessing-directly_accessing-the-registry){: external}, using the worker node that you previously retrieved. Follow the steps to push a test image to the internal registry.

        To complete these steps in the {{site.data.keyword.openshiftshort}} documentation, you need the `podman` CLI tool. Your worker nodes might not have this CLI tool by default. See the [Podman installation guide](https://podman.io/getting-started/installation.html){: external} for RHEL 7.
        {: tip}

    2. Navigate to the internal registry pod folder that saves to the `emptyDir`. For `<pod_uid>`, use the pod **UID** that you retrieved earlier.
        ```sh
        cd var/lib/kubelet/pods/<pod_uid>/volumes/kubernetes.io~empty-dir/registry-storage/docker/registry/v2/repositories/openshift
        ```
        {: pre}

    3. Verify that your image is in repository directory.
        ```sh
        ls
        ```
        {: pre}

        Example output
        ```sh
        <myimage>  nginx  ...
        ```
        {: screen}



## Setting up a secure external route for the internal registry
{: #route_internal_registry}

By default, your {{site.data.keyword.openshiftshort}} cluster has an internal registry that is available through a service with an internal IP address. If you want to make the internal registry available on the public network, you can set up a secure re-encrypt route. For example, you might set up your cluster's internal registry to act as a public registry for deployments in other projects or clusters.
{: shortdesc}

Before you begin:
*  Confirm that you have the [**Manager** {{site.data.keyword.cloud_notm}} IAM service access role](/docs/openshift?topic=openshift-access_reference#service) for the cluster.
*  Make sure that your cluster has public network connectivity to expose the internal registry with a public route.
*  Install Docker on your local machine.
*  [Access your {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-access_cluster).

<img src="images/icon-version-311.png" alt="Version 3.11 icon" width="30" style="width:30px; border-style: none"/> For {{site.data.keyword.openshiftshort}} 3.11 clusters, the internal registry is in the `default` project and uses the `docker-registry` service. The following steps are specific for version 4 clusters. To set up the route in a 3.11 cluster, replace the `openshift-image-registry` project with `default` and the `image-registry` service with `docker-registry`.
{: important}

To use the internal registry, set up a public route to access the registry. Then, create an image pull secret that includes the credentials to access the registry so that deployments in other projects can pull images from this registry.

1. From the `openshift-image-registry` project, make sure that the `image-registry` service exists for the internal registry.

    ```sh
    oc get svc -n openshift-image-registry
    ```
    {: pre}

    Example output

    ```sh
    NAME                      TYPE           CLUSTER-IP       EXTERNAL-IP     PORT(S)                      AGE
    image-registry            ClusterIP      172.21.xxx.xxx    <none>          5000/TCP                     36d
    image-registry-operator   ClusterIP      None             <none>          60000/TCP                     36d
    ```
    {: screen}

2. Create a secured route for the `image-registry` service that uses `reencrypt` TLS termination. With re-encryption, the router terminates the TLS connection with a certificate, and then re-encrypts the connection to the internal registry with a different certificate. With this approach, the full path of the connection between the user and the internal registry is encrypted. To provide your own custom domain name, include the `--hostname` flag.

    ```sh
    oc create route reencrypt --service=image-registry -n openshift-image-registry
    ```
    {: pre}

3. Retrieve the hostname (**HOST/PORT**) and the **PORT** that were assigned to the `image-registry` route.

    ```sh
    oc get route image-registry -n openshift-image-registry
    ```
    {: pre}

    Example output

    ```sh
    NAME              HOST/PORT                                                                                                  PATH      SERVICES          PORT       TERMINATION   WILDCARD
    image-registry   image-registry-openshift-image-registry.<cluster_name>-<ID_string>.<region>.containers.appdomain.cloud             image-registry   5000-tcp   reencrypt     None
    ```
    {: screen}

4. Edit the route to set the [load balancing strategy](https://docs.openshift.com/container-platform/3.11/architecture/networking/routes.html#load-balancing){: external} to `source` so that the same client IP address reaches the same server, as in a passthrough route setup. You can set the strategy by adding an annotation in the `metadata.annotations` section: `haproxy.router.openshift.io/balance: source`. You can edit the configuration file from the **{{site.data.keyword.openshiftshort}} Application Console** or in your command line by running the following command.

    ```sh
    oc edit route image-registry -n openshift-image-registry
    ```
    {: pre}

    Add the annotation.
    ```yaml
    apiVersion: route.openshift.io/v1
    kind: Route
    metadata:
    annotations:
        haproxy.router.openshift.io/balance: source
    ...
    ```
    {: screen}

5. If corporate network policies prevent access from your local system to public endpoints via proxies or firewalls, [allow access to the route subdomain](/docs/openshift?topic=openshift-vpc-firewall#openshift-registry) that you create for the internal registry in the following steps.

6. Log in to the internal registry by using the route as the hostname.

    ```sh
    docker login -u $(oc whoami) -p $(oc whoami -t) image-registry-openshift-image-registry.<cluster_name>-<ID_string>.<region>.containers.appdomain.cloud
    ```
    {: pre}

7. Now that you are logged in, try pushing a sample `hello-world` app to the internal registry.
    1. Pull the `hello-world` image from DockerHub, or build an image on your local machine.

        ```sh
        docker pull hello-world
        ```
        {: pre}

    2. Tag the local image with the hostname of your internal registry, the project that you want to deploy the image to, and the image name and tag.

        ```sh
        docker tag hello-world:latest image-registry-openshift-image-registry.<cluster_name>-<ID_string>.<region>.containers.appdomain.cloud/<project>/<image_name>:<tag>
        ```
        {: pre}

    3. Push the image to your cluster's internal registry.

        ```sh
        docker push image-registry-openshift-image-registry.<cluster_name>-<ID_string>.<region>.containers.appdomain.cloud/<project>/<image_name>:<tag>
        ```
        {: pre}

    4. Verify that the image is added to the {{site.data.keyword.openshiftshort}} image stream.

        ```sh
        oc get imagestream
        ```
        {: pre}

        Example output

        ```sh
        NAME          DOCKER REPO                                                            TAGS      UPDATED
        hello-world   image-registry-openshift-image-registry.svc:5000/default/hello-world   latest    7 hours ago
        ```
        {: screen}

8. To enable deployments in your project to pull images from the internal registry, create an image pull secret in your project that holds the credentials to access your internal registry. Then, add the image pull secret to the default service account for each project.

    1. List the image pull secrets that the default service account uses, and note the secret that begins with `default-dockercfg`.

        ```sh
        oc describe sa default
        ```
        {: pre}

        Example output

        ```sh
        ...
        Image pull secrets:
        all-icr-io
        default-dockercfg-mpcn4
        ...
        ```
        {: screen}

    2. Get the encoded secret information from the `data` field of the configuration file.

        ```sh
        oc get secret <default-dockercfg-name> -o yaml
        ```
        {: pre}

        Example output

        ```yaml
        apiVersion: v1
        data:
          .dockercfg: ey...=
        ```
        {: screen}

    3. Decode the value of the `data` field.

        ```sh
        echo "<ey...=>" | base64 -D
        ```
        {: pre}

        Example output

        ```sh
        {"172.21.xxx.xxx:5000":{"username":"serviceaccount","password":"eyJ...
        ```
        {: screen}

    4. Create a new image pull secret for the internal registry.

        - `secret_name`: Give your image pull secret a name, such as `internal-registry`.
        - `--namespace`: Enter the project to create the image pull secret in, such as `default`.
        - `--docker-server`: Instead of the internal service IP address (`172.21.xxx.xxx:5000`), enter the hostname of the `image-registry` route with the port (`image-registry-openshift-image-registry.<cluster_name>-<ID_string>.<region>.containers.appdomain.cloud:5000`).
        - `--docker-username`: Copy the `"username"` from the previous image pull secret, such as `serviceaccount`.
        - `--docker-password`: Copy the `"password"` from the previous image pull secret.
        - `--docker-email`: If you have one, enter your Docker email address. If you don't, enter a fictional email address, such as `a@b.c`. This email is required to create a Kubernetes secret, but is not used after creation.

        ```sh
        oc create secret image-registry internal-registry --namespace default --docker-server image-registry-openshift-image-registry.<cluster_name>-<ID_string>.<region>.containers.appdomain.cloud:5000 --docker-username serviceaccount --docker-password <eyJ...> --docker-email a@b.c
        ```
        {: pre}

    5. Add the image pull secret to the default service account of your project.

        ```sh
        oc patch -n <namespace_name> serviceaccount/default --type='json' -p='[{"op":"add","path":"/imagePullSecrets/-","value":{"name":"<image_pull_secret_name>"}}]'
        ```
        {: pre}

    6. Repeat these steps for each project that you want to pull images from the internal registry.

Now that you set up the internal registry with an accessible route, you can log in, push, and pull images to the registry. For more information, see the [{{site.data.keyword.openshiftshort}} documentation](https://docs.openshift.com/container-platform/4.7/registry/accessing-the-registry.html){: external}.



## Importing images from {{site.data.keyword.registrylong_notm}} into the internal registry image stream
{: #imagestream_registry}

By default, your {{site.data.keyword.openshiftlong_notm}} cluster is set up to pull images from the remote, private {{site.data.keyword.registrylong_notm}} `icr.io` domains in the `default` project. You can import an image from {{site.data.keyword.registrylong_notm}} into the internal registry of your {{site.data.keyword.openshiftshort}} cluster by tagging the image as an [image stream](https://docs.openshift.com/container-platform/4.7/openshift_images/image-streams-manage.html){: external}. With this setup, you can deploy apps from the image by using the local cache of the internal registry, which can make your app deployments build faster. Also, deployments in other projects can refer to the image stream so that you don't have to create image pull secret credentials to {{site.data.keyword.registrylong_notm}} in each project.
{: shortdesc}

If you update your image in {{site.data.keyword.registrylong_notm}}, the image is not pulled automatically into the internal registry of your {{site.data.keyword.openshiftshort}} cluster. Instead, [configure periodic importing](https://docs.openshift.com/container-platform/4.7/openshift_images/image-streams-manage.html#images-imagestreams-import_image-streams-managing){: external}, or repeat these steps to tag the image. Depending on the image pull policy that you use in your deployment, you might also need to restart your deployment.
{: note}

Want to learn more about how builds, image streams, and the internal registry work together? Read the [{{site.data.keyword.openshiftshort}} docs](https://docs.openshift.com/container-platform/4.7/registry/architecture-component-imageregistry.html){: external}, or check out [this blog on managing container images](https://cloudowski.com/articles/why-managing-container-images-on-openshift-is-better-than-on-kubernetes/){: external}.
{: tip}

1. [Access your {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-access_cluster).
2. Switch to the `default` project to pull your image into the image stream. The `default` project is already set up with credentials to access the `icr.io` registries.

    ```sh
    oc project default
    ```
    {: pre}

3. List the available images in your {{site.data.keyword.registrylong_notm}}. Note the **Repository** and **Tag** of the image that you want to pull into the internal registry of your {{site.data.keyword.openshiftshort}} cluster.

    ```sh
    ibmcloud cr images
    ```
    {: pre}

4. Tag the image to pull it from your {{site.data.keyword.registrylong_notm}} namespace into the internal registry as an image stream. For more information, see the [{{site.data.keyword.openshiftshort}} documentation](https://docs.openshift.com/container-platform/4.7/openshift_images/image-streams-manage.html){: external} or run `oc tag --help`.

    ```sh
    oc tag <region>.icr.io/<namespace>/<image>:<tag> default/<image>:<tag> --reference-policy=local [--scheduled]
    ```
    {: pre}

    - `<region>.icr.io/<namespace>/<image>:<tag>`: Use the **Repository** and **Tag** information that you previously retrieved to fill out the {{site.data.keyword.registrylong_notm}} region, namespace, image, and tag name of the image that you want to pull.
    - `default/<image>:<tag>`: Enter the information for the internal image stream that you create from the {{site.data.keyword.registrylong_notm}} tagged image. You create this image stream in the `default` project, which is also the project where the image stream is created if you don't specify a project. The values for `<image>:<tag>` typically match the values that you previously retrieved.</td>
    - `--reference-policy=local`: Set this value to `local` so that a copy of the image from {{site.data.keyword.registrylong_notm}} is imported into the local cache of the internal registry and made available to the cluster's projects as an image stream. If you don't include this value, the image stream refers back to {{site.data.keyword.registrylong_notm}} when you use it in your deployments and therefore requires credentials in the project.
    - `--scheduled`: Set this optional flag to set up periodic importing of the image from {{site.data.keyword.registrylong_notm}} into the internal registry. The default frequency is 15 minutes. For more information, see the [{{site.data.keyword.openshiftshort}} documentation](https://docs.openshift.com/container-platform/4.7/openshift_images/image-streams-manage.html#images-imagestreams-import_image-streams-managing){: external}. 

5. Verify that your image stream is created.

    ```sh
    oc get imagestreams
    ```
    {: pre}

6. Verify that the image stream successfully pulled the image from {{site.data.keyword.registrylong_notm}}. In the output, check that the **latest tagged from** image matches your `* <region>.icr.io/<namespace>/<image>@<digest>` image.

    ```sh
    oc describe is/<imagestream>
    ```
    {: pre}

    Example output

    ```sh
    NAME:            <imagestream>
    Namespace:        default
    Created:        2 days ago
    Labels:            <none>
    Annotations:        openshift.io/image.dockerRepositoryCheck=2020-03-31T09:41:36Z
    Image Repository:    image-registry.openshift-image-registry.svc:5000/default/ant1
    Image Lookup:        local=false
    Unique Images:        1
    Tags:                1

    latest
        tagged from <region>.icr.io/<namespace>/<image>:<tag>

        * <region>.icr.io/<namespace>/<image>@<digest>
            2 days ago
    ```
    {: screen}

Now, your developers can [use the image stream in an app deployment](/docs/openshift?topic=openshift-images#oc_imagestream_deploy). The image successfully builds from the locally pulled image in the internal registry. You don't need to set up an image pull secret in the project to {{site.data.keyword.registrylong_notm}}, because the image stream is local to the cluster.



## Setting up builds in the internal registry to push images to {{site.data.keyword.registrylong_notm}}
{: #builds_registry}

When you create a [build](https://docs.openshift.com/container-platform/4.7/cicd/builds/understanding-image-builds.html){: external} in your {{site.data.keyword.openshiftlong_notm}} cluster, you can [set up the internal registry to push the image to your external repository](http://docs.openshift.com/container-platform/4.7/cicd/builds/creating-build-inputs.html){: external} in {{site.data.keyword.registrylong_notm}}. By default, the image pull secret in the `default` project of your cluster only has read access to pull images from {{site.data.keyword.registrylong_notm}}. To push images, you must add a secret with write access.
{: shortdesc}

1. [Access your {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-access_cluster).
2. Switch to the `default` project.

    ```sh
    oc project default
    ```
    {: pre}

3. [Follow the steps to set up an {{site.data.keyword.cloud_notm}} IAM API key](/docs/openshift?topic=openshift-registry#other_registry_accounts) with the `Reader` and `Writer` service access roles to pull from and push images to your `icr.io` registries.

    Keep in mind that any user with access to the project can use this secret to push images to your private registry. You might want to set up [logging and monitoring](/docs/openshift?topic=openshift-health) tools so that you can observe who does what actions in your cluster.
    {: note}

4. Repeat the previous step for each `icr.io` region that you want to push images to.
5. Add the secret to the build service account and refer to the secrets in the build configuration file. For more information, see the [{{site.data.keyword.openshiftshort}} documentation](http://docs.openshift.com/container-platform/4.7/cicd/builds/creating-build-inputs.html){: external}.
    1. Add the secret to the build service account by linking the secret that you just created to the `builder` role that all builds in the cluster use.

        ```sh
        oc secrets link builder <secret_name>
        ```
        {: pre}

    2. List the build configurations and note the ones that you want to give push and pull access to {{site.data.keyword.registrylong_notm}}.

        ```sh
        oc get bc
        ```
        {: pre}

    3. Set the image push secret for the build configuration to use the secret that you just created with `Writer` service access to {{site.data.keyword.registrylong_notm}}.

        ```sh
        oc set build-secret --push bc/<build_config_name> <secret_name>
        ```
        {: pre}

    4. Set the image pull secret for the build configuration to pull from the registry that you want to pull the initial build image from. For example, you can use the secret that you just created with `Reader` service access to {{site.data.keyword.registrylong_notm}} if the source image is in an {{site.data.keyword.registrylong_notm}} repository.

        ```sh
        oc set build-secret --pull bc/<build_config_name> <secret_name>
        ```
        {: pre}

6. After you update the build service account and build configuration file to push to {{site.data.keyword.registrylong_notm}}, restart your build.

    ```sh
    oc start-build <build_name>
    ```
    {: pre}

7. Get the name of your build pod, such as `<build>-2-build`.

    ```sh
    oc get pods
    ```
    {: pre}

8. Check the logs of the build and note where the image was pushed.

    ```sh
    oc logs <build_pod>
    ```
    {: pre}

    Example of a successful image push log.

    ```sh
    ...
    Successfully pushed <region>.icr.io/<namespace>/<build_name>@sha256:<hash>
    Push successful
    ```
    {: screen}

9. Check your images in your private registry to confirm that the image is created.

    ```sh
    ibmcloud cr image list
    ```
    {: pre}

    Example output

    ```sh
    Repository                                Tag       Digest     Namespace     Created         Size     Security status   
    <region>.icr.io/<namespace>/<build_name>  latest    <digest>   <namespace>   2 minutes ago   182 MB   33 Issues  
    ```
    {: screen}

Your {{site.data.keyword.openshiftshort}} build can now pull images from and push images to {{site.data.keyword.registrylong_notm}}.



## Using {{site.data.keyword.registrylong_notm}}
{: #openshift_iccr}

By default, your {{site.data.keyword.openshiftlong_notm}} cluster is set up to pull images from the remote, private {{site.data.keyword.registrylong_notm}} `icr.io` domains in the `default` project. If you want to use images that are stored in {{site.data.keyword.registrylong_notm}} for other projects, you can pull the image to the internal registry in an image stream, or create image pull secrets for each global and regional registry in each project.
{: shortdesc}

**To import images into the internal registry**: See [Importing images from {{site.data.keyword.registrylong_notm}} into the internal registry image stream](#imagestream_registry).

**To pull images directly from the external {{site.data.keyword.registrylong_notm}}**: See the following topics.
* [Understanding how to authorize your cluster to pull images from a registry](#cluster_registry_auth).
* [Copying the `all-icr-io` secret](#copy_imagePullSecret) from the `default` project to the project that you want to pull images from.
* [Creating your own image pull secret](#other_registry_accounts).
* [Adding the image pull secret](#use_imagePullSecret) to your deployment configuration or to the project service account.


</openshift-chunk>



## Understanding how to authorize your cluster to pull images from a private registry
{: #cluster_registry_auth}

To pull images from a registry, your {{site.data.keyword.openshiftlong_notm}} cluster uses a special type of Kubernetes secret, an `imagePullSecret`. This image pull secret stores the credentials to access a container registry.
{: shortdesc}

The container registry can be:
* A private namespace in your own {{site.data.keyword.registrylong_notm}}.
* A private namespace in {{site.data.keyword.registrylong_notm}} that belongs to a different {{site.data.keyword.cloud_notm}} account.
* Any other private registry such as Docker.

However, by default, your cluster is set up to pull images from only your account's namespaces in {{site.data.keyword.registrylong_notm}}, and deploy containers from these images to the `default` {{site.data.keyword.openshiftshort}} project in your cluster. If you need to pull images in other projects of the cluster or from other container registries, then you must set up your own image pull secrets.

### Default image pull secret setup
{: #cluster_registry_auth_default}

Generally, your {{site.data.keyword.openshiftlong_notm}} cluster is set up to pull images from all {{site.data.keyword.registrylong_notm}} `icr.io` domains from the `default` {{site.data.keyword.openshiftshort}} project only. Review the following FAQs to learn more about how to pull images in other {{site.data.keyword.openshiftshort}} projects or accounts, restrict pull access, or why your cluster might not have the default image pull secrets.
{: shortdesc}

**How is my cluster set up to pull images from the `default` {{site.data.keyword.openshiftshort}} project?**

When you create a cluster, the cluster has an {{site.data.keyword.cloud_notm}} IAM service ID that is given an IAM **Reader** service access role policy to {{site.data.keyword.registrylong_notm}}. The service ID credentials are impersonated in a non-expiring API key that is stored in image pull secrets in your cluster. The image pull secrets are added to the `default` Kubernetes namespace and the list of secrets in the `default` service account for this {{site.data.keyword.openshiftshort}} project. By using image pull secrets, your deployments can pull images (read-only access) from the [global and regional {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-registry_overview#registry_regions) to deploy containers in the `default` {{site.data.keyword.openshiftshort}} project.

* The global registry securely stores public images that are provided by IBM. You can refer to these public images across your deployments instead of having different references for images that are stored in each regional registry.
* The regional registry securely stores your own private Docker images.

**What if I don't have image pull secrets in the `default` {{site.data.keyword.openshiftshort}} project?**

You can check the image pull secrets by [logging in to your cluster](/docs/openshift?topic=openshift-access_cluster) and running `oc get secrets -n default | grep "icr-io"`. If no `icr` secrets are listed, the person who created the cluster might not have had the required permissions to {{site.data.keyword.registrylong_notm}} in IAM. See [Updating existing clusters to use the API key image pull secret](#imagePullSecret_migrate_api_key).

**Can I restrict pull access to a certain regional registry?**

Yes, you can [edit the existing IAM policy of the service ID](/docs/account?topic=account-serviceids#update_serviceid) that restricts the **Reader** service access role to that regional registry or a registry resource such as a namespace. Before you can customize registry IAM policies, you must [enable {{site.data.keyword.cloud_notm}} IAM policies for {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-user#existing_users).

Want to make your registry credentials even more secured Ask your cluster admin to [enable a key management service provider](/docs/openshift?topic=openshift-encryption#keyprotect) in your cluster to encrypt Kubernetes secrets in your cluster, such as the image pull secret that stores your registry credentials.
{: tip}


**Can I pull images in a {{site.data.keyword.openshiftshort}} project other than `default`?**

Not by default. By using the default cluster setup, you can deploy containers from any image that is stored in your {{site.data.keyword.registrylong_notm}} namespace into the `default` {{site.data.keyword.openshiftshort}} project of your cluster. To use these images in any other {{site.data.keyword.openshiftshort}} projects or other {{site.data.keyword.cloud_notm}} accounts, [you have the option to copy or create your own image pull secrets](#other).


**Can I pull images from a different {{site.data.keyword.cloud_notm}} account?**

Yes, create an API key in the {{site.data.keyword.cloud_notm}} account that you want to use. Then, in each project of each cluster that you want to pull images from the {{site.data.keyword.cloud_notm}} account, create a secret that holds the API key. For more information, [follow along with this example that uses an authorized service ID API key](#other_registry_accounts).

To use a non-{{site.data.keyword.cloud_notm}} registry such as Docker, see [Accessing images that are stored in other private registries](#private_images).

**Does the API key need to be for a service ID? What happens if I reach the limit of service IDs for my account?**

The default cluster setup creates a service ID to store {{site.data.keyword.cloud_notm}} IAM API key credentials in the image pull secret. However, you can also create an API key for an individual user and store those credentials in an image pull secret. If you reach the [IAM limit for service IDs](/docs/account?topic=account-policy-limits), your cluster is created without the service ID and image pull secret and cannot pull images from the `icr.io` registry domains by default. You must [create your own image pull secret](#other_registry_accounts), but by using an API key for an individual user such as a functional ID, not an {{site.data.keyword.cloud_notm}} IAM service ID.

**I see image pull secrets for the regional registry domains and all registry domains. Which one do I use?**

Previously, {{site.data.keyword.openshiftlong_notm}} created separate image pull secrets for each regional, public `icr.io` registry domain. Now, all the public and private `icr.io` registry domains for all regions are stored in a single `all-icr-io` image pull secret that is automatically created in the `default` Kubernetes project of your cluster.

For workloads in other Kubernetes namespaces in the cluster to pull container images from a private registry, you can now copy only the `all-icr-io` image pull secret to that Kubernetes project. Then, specify the `all-icr-io` secret in your service account or deployment. You do not need to copy the image pull secret that matches the regional registry of your image anymore. Also, keep in mind that you do not need image pull secrets for public registries, which do not require authentication.



**After I copy or create an image pull secret in another {{site.data.keyword.openshiftshort}} project, am I done?**

Not quite. Your containers must be authorized to pull images by using the secret that you created. You can add the image pull secret to the service account for the namespace, or refer to the secret in each deployment. For instructions, see [Using the image pull secret to deploy containers](#use_imagePullSecret).

### Private network connection to `icr.io` registries
{: #cluster_registry_auth_private}

When you set up your {{site.data.keyword.cloud_notm}} account to use service endpoints, you can use a private network connection to push images to and to pull images from {{site.data.keyword.registrylong_notm}}. When you use the private network to pull images, your image pull traffic is not charged as [public bandwidth](/docs/openshift?topic=openshift-costs#bandwidth), because the traffic is on the private network. For more information, see the [{{site.data.keyword.registrylong_notm}} private network documentation](/docs/Registry?topic=Registry-registry_private).
{: shortdesc}

**What do I need to do to set up my cluster to use the private connection to `icr.io` registries?**

1. Enable a [Virtual Router Function (VRF)](/docs/account?topic=account-vrf-service-endpoint#vrf) for your IBM Cloud infrastructure account so that you can use the {{site.data.keyword.registrylong_notm}} private cloud service endpoint. To enable VRF, see [Enabling VRF](/docs/account?topic=account-vrf-service-endpoint#vrf). To check whether a VRF is already enabled, use the `ibmcloud account show` command.
2. [Enable your {{site.data.keyword.cloud_notm}} account to use service endpoints](/docs/account?topic=account-vrf-service-endpoint#service-endpoint).

Now, {{site.data.keyword.registrylong_notm}} automatically uses the private cloud service endpoint. You do not need to enable the private cloud service endpoint for your {{site.data.keyword.openshiftlong_notm}} clusters.

**Do I have to use the private `icr.io` registry addresses for anything else?**

Yes, if you [sign your images for trusted content](/docs/Registry?topic=Registry-registry_trustedcontent), the signatures contain the registry domain name. If you want to use the private `icr.io` domain for your signed images, resign your images with the private `icr.io` domains.



## Updating existing clusters to use the API key image pull secret
{: #imagePullSecret_migrate_api_key}

New {{site.data.keyword.openshiftlong_notm}} clusters store an API key in [image pull secrets to authorize access to {{site.data.keyword.registrylong_notm}}](#cluster_registry_auth). With these image pull secrets, you can deploy containers from images that are stored in the `icr.io` registry domains. You can add the image pull secrets to your cluster if your cluster was not created with the secrets.
{: shortdesc}

**Before you begin**
1. [Access your {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-access_cluster).
2. Make sure that you have the following permissions: {{site.data.keyword.cloud_notm}} IAM **Operator or Administrator** platform access role for {{site.data.keyword.openshiftlong_notm}}. The account owner can give you the role by running the following command.

    ```sh
    ibmcloud iam user-policy-create <your_user_email> --service-name containers-kubernetes --roles <(Administrator|Operator)>
    ```
    {: pre}

2. {{site.data.keyword.cloud_notm}} IAM **Administrator** platform access role for {{site.data.keyword.registrylong_notm}}, across all regions and resource groups. The policy cannot be scoped to a particular region or resource group. The account owner can give you the role by running the following command.

    ```sh
    ibmcloud iam user-policy-create <your_user_email> --service-name container-registry --roles Administrator
    ```
    {: pre}

 3. If your account [restricts service ID creation](/docs/account?topic=account-restrict-service-id-create), add the **Service ID creator** role to **Identity and Access Management** in the console (`iam-identity` in the API or CLI).
 
4. If your account [restricts API key creation](/docs/account?topic=account-allow-api-create), add the **User API key creator** role to **Identity and Access Management** in the console (`iam-identity` in the API or CLI).<

### Updating your image pull secret
{: #update-pull-secret}

To update your cluster image pull secret in the `default` Kubernetes namespace.
{: shortdesc}

1. Get your cluster ID.

    ```sh
    ibmcloud oc cluster ls
    ```
    {: pre}

2. Run the following command to create a service ID for the cluster and assign the service ID an IAM **Reader** service access role for {{site.data.keyword.registrylong_notm}}. The command also creates an API key to impersonate the service ID credentials and stores the API key in a Kubernetes image pull secret in the cluster. The image pull secret is in the `default` {{site.data.keyword.openshiftshort}} project.

    ```sh
    ibmcloud oc cluster pull-secret apply --cluster <cluster_name_or_ID>
    ```
    {: pre}

    When you run this command, the creation of IAM credentials and image pull secrets is initiated and can take some time to complete. You cannot deploy containers that pull an image from the {{site.data.keyword.registrylong_notm}} `icr.io` domains until the image pull secrets are created.
    {: important}

3. Verify that the image pull secrets are created in your cluster.

    ```sh
    oc get secrets | grep icr-io
    ```
    {: pre}

    Example output

    ```sh
    all-icr-io           kubernetes.io/dockerconfigjson        1         16d
    ```
    {: screen}

    To maintain backwards compatibility, your {{site.data.keyword.openshiftshort}} 3.11 clusters have a separate image pull secret for each {{site.data.keyword.registrylong_notm}} region. However, you can copy and refer to only the `all-icr-io` image pull secret, which has credentials to the public and private `icr.io` registry domains for all regions.
    {: note}

4. Update your [container deployments](/docs/openshift?topic=openshift-openshift_apps#image) to pull images from the `icr.io` domain name.
5. Optional: If you have a firewall, make sure you [allow outbound network traffic to the registry subnets](/docs/openshift?topic=openshift-firewall#firewall_outbound) for the domains that you use.

**What's next?**
* To pull images in {{site.data.keyword.openshiftshort}} projects other than `default` or from other {{site.data.keyword.cloud_notm}} accounts, [copy or create another image pull secret](#other).
* To restrict the image pull secret access to particular registry resources such as namespaces or regions:
    1. Make sure that [{{site.data.keyword.cloud_notm}} IAM policies for {{site.data.keyword.registrylong_notm}} are enabled](/docs/Registry?topic=Registry-user#existing_users).
    2. [Edit the {{site.data.keyword.cloud_notm}} IAM policies](/docs/account?topic=account-serviceids#update_serviceid) for the service ID, or [create another image pull secret](#other_registry_accounts).



## Using an image pull secret to access images in other {{site.data.keyword.cloud_notm}} accounts or external private registries from non-default {{site.data.keyword.openshiftshort}} projects
{: #other}

Set up your own image pull secret in your cluster to deploy containers to {{site.data.keyword.openshiftshort}} projects other than `default`, use images that are stored in other {{site.data.keyword.cloud_notm}} accounts, or use images that are stored in external private registries. Further, you might create your own image pull secret to apply IAM access policies that restrict permissions to specific registry image namespaces, or actions (such as `push` or `pull`).
{: shortdesc}

After you create the image pull secret, your containers must use the secret to be authorized to pull an image from the registry. You can add the image pull secret to the service account for the project, or refer to the secret in each deployment. For instructions, see [Using the image pull secret to deploy containers](#use_imagePullSecret).

Image pull secrets are valid only for the {{site.data.keyword.openshiftshort}} projects that they were created for. Repeat these steps for every namespace where you want to deploy containers.
{: tip}


Before you begin:

1. [Set up a namespace in {{site.data.keyword.registrylong_notm}} and push images to this namespace](/docs/Registry?topic=Registry-getting-started#gs_registry_namespace_add).
2. [Create an {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-clusters).
3. [Access your {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-access_cluster).



To use your own image pull secret, choose among the following options:

- [Copy the image pull secret](#copy_imagePullSecret) from the default {{site.data.keyword.openshiftshort}} project to other projects in your cluster.
- [Create new IAM API key credentials and store them in an image pull secret](#other_registry_accounts) to access images in other {{site.data.keyword.cloud_notm}} accounts or to apply IAM policies that restrict access to certain registry domains or namespaces.
- [Create an image pull secret to access images in external private registries](#private_images).



If you already created an image pull secret in your project that you want to use in your deployment, see [Deploying containers by using the created `imagePullSecret`](#use_imagePullSecret).

### Copying an existing image pull secret
{: #copy_imagePullSecret}

You can copy an image pull secret, such as the one that is automatically created for the `default` {{site.data.keyword.openshiftshort}} project, to other projects in your cluster. If you want to use different {{site.data.keyword.cloud_notm}} IAM API key credentials for this project such as to restrict access to specific projects, or to pull images from other {{site.data.keyword.cloud_notm}} accounts, [create an image pull secret](#other_registry_accounts) instead.
{: shortdesc}

1. List available {{site.data.keyword.openshiftshort}} projects in your cluster, or create a project to use.

    ```sh
    oc get projects
    ```
    {: pre}

    Example output

    ```sh
    default          Active
    ibm-cert-store   Active
    ibm-system       Active
    kube-public      Active
    kube-system      Active
    ```
    {: screen}

    To create a project

    ```sh
    oc new-project <project_name>
    ```
    {: pre}

2. List the existing image pull secrets in the `default` {{site.data.keyword.openshiftshort}} project for {{site.data.keyword.registrylong_notm}}.

    ```sh
    oc get secrets -n default | grep icr-io
    ```
    {: pre}

    Example output

    ```sh
    all-icr-io          kubernetes.io/dockerconfigjson        1         16d
    ```
    {: screen}

3. Copy the `all-icr-io` image pull secret from the `default` project to the project of your choice. The new image pull secrets are named `<project_name>-icr-<region>-io`.

    ```sh
    oc get secret all-icr-io -n default -o yaml | sed 's/default/<new-project>/g' | oc create -n <new-project> -f -   
    ```
    {: pre}

4. Verify that the secrets are created successfully.

    ```sh
    oc get secrets -n <project_name> | grep icr-io
    ```
    {: pre}

5. To deploy containers, [add the image pull secret](#use_imagePullSecret) to each deployment or to the service account of the project so that any deployment in the project can pull images from the registry.

### Creating an image pull secret with different IAM API key credentials for more control or access to images in other {{site.data.keyword.cloud_notm}} accounts
{: #other_registry_accounts}

You can assign {{site.data.keyword.cloud_notm}} IAM access policies to users or a service ID to restrict permissions to specific registry image namespaces or actions (such as `push` or `pull`). Then, create an API key and store these registry credentials in an image pull secret for your cluster.
{: shortdesc}

For example, to access images in other {{site.data.keyword.cloud_notm}} accounts, create an API key that stores the {{site.data.keyword.registrylong_notm}} credentials of a user or service ID in that account. Then, in your cluster's account, save the API key credentials in an image pull secret for each cluster and cluster project.

The following steps create an API key that stores the credentials of an {{site.data.keyword.cloud_notm}} IAM service ID. Instead of using a service ID, you might want to create an API key for a user ID that has an {{site.data.keyword.cloud_notm}} IAM service access policy to {{site.data.keyword.registrylong_notm}}. However, make sure that the user is a functional ID or have a plan in case the user leaves so that the cluster can still access the registry.
{: note}

1. List available {{site.data.keyword.openshiftshort}} projects in your cluster, or create a project to use where you want to deploy containers from your registry images.

    ```sh
    oc get projects
    ```
    {: pre}

    Example output

    ```sh
    default          Active
    ibm-cert-store   Active
    ibm-system       Active
    kube-public      Active
    kube-system      Active
    ```
    {: screen}

    To create a project

    ```sh
    oc new-project <project_name>
    ```
    {: pre}

2. Create an {{site.data.keyword.cloud_notm}} IAM service ID for your cluster that is used for the IAM policies and API key credentials in the image pull secret. Be sure to give the service ID a description that helps you retrieve the service ID later, such as including both the cluster and project name.

    ```sh
    ibmcloud iam service-id-create <cluster_name>-<project>-id --description "Service ID for IBM Cloud Container Registry in {{site.data.keyword.openshiftshort}} cluster <cluster_name> project <project>"
    ```
    {: pre}

3. Create a custom {{site.data.keyword.cloud_notm}} IAM policy for your cluster service ID that grants access to {{site.data.keyword.registrylong_notm}}.
    ```sh
    ibmcloud iam service-policy-create <cluster_service_ID> --roles <service_access_role> --service-name container-registry [--region <IAM_region>] [--resource-type namespace --resource <registry_namespace>]
    ```
    {: pre}

    `cluster_service_ID`
    :   Required. Replace with the `<cluster_name>-<kube_namespace>-id` service ID that you previously created for your Kubernetes cluster.</td>
    
    `--service-name container-registry`
    :   Required. Enter `container-registry` so that the IAM policy is for {{site.data.keyword.registrylong_notm}}.
    
    `--roles <service_access_role>`
    :   Required. Enter the [service access role](/docs/Registry?topic=Registry-iam#service_access_roles) for {{site.data.keyword.registrylong_notm}} that you want to scope the service ID access to. Possible values are `Reader`, `Writer`, and `Manager`.
    
    `--region <IAM_region>`
    :   Optional. If you want to scope the access policy to certain IAM regions, enter the regions in a comma-separated list. Possible values are `global` and the [local registry regions](/docs/Registry?topic=Registry-registry_overview#registry_regions_local).
    
    `--resource-type namespace --resource <registry_namespace>`
    :   Optional. If you want to limit access to only images in certain [{{site.data.keyword.registrylong_notm}} namespaces](/docs/Registry?topic=Registry-registry_setup_cli_namespace#registry_setup_cli_namespace_plan), enter `namespace` for the resource type and specify the `<registry_namespace>`. To list registry namespaces, run `ibmcloud cr namespaces`.

4. Create an API key for the service ID. Name the API key similar to your service ID, and include the service ID that you previously created,
    `<cluster_name>-<kube_namespace>-id`. Be sure to give the API key a description that helps you retrieve the key later
    
    ```sh
    ibmcloud iam service-api-key-create <cluster_name>-<project>-key <cluster_name>-<project>-id --description "API key for service ID <service_id> in {{site.data.keyword.openshiftshort}} cluster <cluster_name> project <project>"
    ```
    {: pre}

5. Retrieve your **API Key** value from the output of the previous command.

    ```sh
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

6. Create an image pull secret to store the API key credentials in the cluster project. Repeat this step for each project of each cluster for each `icr.io` domain that you want to pull images from.

    ```sh
    oc --namespace <project> create secret docker-registry <secret_name> --docker-server=<registry_URL> --docker-username=iamapikey --docker-password=<api_key_value> --docker-email=<docker_email>
    ```
    {: pre}

    `--namespace <project>`
    :   Required. Specify the {{site.data.keyword.openshiftshort}} project of your cluster that you used for the service ID name.

    `<secret_name>`
    :   Required. Enter a name for your image pull secret.
    
    `--docker-server <registry_URL>`
    :   Required. Set the URL to the image registry where your registry namespace is set up. For available domains, see [Local regions](/docs/Registry?topic=Registry-registry_overview#registry_regions).
    
    `--docker-username iamapikey`
    :   Required. Enter the username to log in to your private registry. If you use {{site.data.keyword.registrylong_notm}}, enter `iamapikey`.
    
    `--docker-password <token_value>`
    :   Required. Enter the value of your `API Key` that you previously retrieved.
    
    `--docker-email <docker-email>`
    :   Required. If you have one, enter your Docker email address. If you do not, enter a fictional email address, such as `a@b.c`. This email is required to create a Kubernetes secret, but is not used after creation.

7. Verify that the secret was created successfully. Replace <em>&lt;project&gt;</em> with the project where you created the image pull secret.

    ```sh
    oc get secrets --namespace <project>
    ```
    {: pre}

8. [Add the image pull secret to a Kubernetes service account so that any pod in the project can use the image pull secret when you deploy a container](#use_imagePullSecret).

### Accessing images that are stored in other private registries
{: #private_images}

If you already have a private registry, you must store the registry credentials in a Kubernetes image pull secret and reference this secret from your configuration file.
{: shortdesc}

Before you begin:

1. [Create an {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-clusters).
2. [Access your {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-access_cluster).

To create an image pull secret:

1. Create the Kubernetes secret to store your private registry credentials.

    ```sh
    oc --namespace <project> create secret docker-registry <secret_name>  --docker-server=<registry_URL> --docker-username=<docker_username> --docker-password=<docker_password> --docker-email=<docker_email>
    ```
    {: pre}

    `--namespace <project>`
    :   Required. The {{site.data.keyword.openshiftshort}} project of your cluster where you want to use the secret and deploy containers to. To list available projects in your cluster, run `oc get projects`.
    
    `<secret_name>`
    :   Required. The name that you want to use for your image pull secret.
    
    `--docker-server <registry_URL>`
    :   Required. The URL to the registry where your private images are stored.
    
    `--docker-username <docker_username>`
    :   Required. The username to log in to your private registry.
    
    `--docker-password <token_value>`
    :   Required. The password to log in to your private registry, such as a token value.
   
    `--docker-email <docker-email>`
    :   Required. If you have one, enter your Docker email address. If you do not have one, enter a fictional email address, such as `a@b.c`. This email is required to create a Kubernetes secret, but is not used after creation.

2. Verify that the secret was created successfully. Replace `<project>` with the name of the project where you created the image pull secret.

    ```sh
    oc get secrets --namespace <project>
    ```
    {: pre}

3. [Create a pod that references the image pull secret](#use_imagePullSecret).



## Using the image pull secret to deploy containers
{: #use_imagePullSecret}

You can define an image pull secret in your pod deployment or store the image pull secret in your Kubernetes service account so that it is available for all deployments that do not specify a Kubernetes service account in the project.
{: shortdesc}

To plan how image pull secrets are used in your cluster, choose between the following options.

* Referring to the image pull secret in your pod deployment: Use this option if you do not want to grant access to your registry for all pods in your project by default. Developers can [include the image pull secret in each pod deployment](/docs/openshift?topic=openshift-images#pod_imagePullSecret) that must access your registry.
* Storing the image pull secret in the Kubernetes service account: Use this option to grant access to images in your registry for all deployments in the selected {{site.data.keyword.openshiftshort}} projects. To store an image pull secret in the Kubernetes service account, use the [following steps](#store_imagePullSecret).

### Storing the image pull secret in the Kubernetes service account for the selected project
{: #store_imagePullSecret}

Every {{site.data.keyword.openshiftshort}} project has a Kubernetes service account that is named `default`. Within the project, you can add the image pull secret to this service account to grant access for pods to pull images from your registry. Deployments that do not specify a service account automatically use the `default` service account for this {{site.data.keyword.openshiftshort}} project.
{: shortdesc}

1. Check if an image pull secret already exists for your default service account.

    ```sh
    oc describe serviceaccount default -n <project_name>
    ```
    {: pre}

    When `<none>` is displayed in the **Image pull secrets** entry, no image pull secret exists.

2. Add the image pull secret to your default service account.

    - Example command to add the image pull secret when no image pull secret is defined.

        ```sh
        oc patch -n <project_name> serviceaccount/default -p '{"imagePullSecrets":[{"name": "<image_pull_secret_name>"}]}'
        ```
        {: pre}

    - Example command to add the image pull secret when an image pull secret is already defined.

        ```sh
        oc patch -n <project_name> serviceaccount/default --type='json' -p='[{"op":"add","path":"/imagePullSecrets/-","value":{"name":"<image_pull_secret_name>"}}]'
        ```
        {: pre}

3. Verify that your image pull secret was added to your default service account.

    ```sh
    oc describe serviceaccount default -n <project_name>
    ```
    {: pre}

    Example output

    ```sh
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

    If the **Image pull secrets** says `<secret> (not found)`, verify that the image pull secret exists in the same project as your service account by running `oc get secrets -n project`.

4. Create a pod configuration file that is named `mypod.yaml` to deploy a container from an **image** in your registry.

    ```yaml
    apiVersion: v1
    kind: Pod
    metadata:
      name: mypod
    spec:
      containers:
        - name: mypod-container
          image: <region>.icr.io/<project>/<image>:<tag>
    ```
    {: codeblock}

5. Create the pod in the cluster by applying the `mypod.yaml` configuration file.

    ```sh
    oc apply -f mypod.yaml
    ```
    {: pre}



## Setting up a cluster to pull entitled software
{: #secret_entitled_software}

You can set up your {{site.data.keyword.openshiftlong_notm}} cluster to pull entitled software, which is a collection of protected container images that are packaged in Helm charts that you are licensed to use by IBM. Entitled software is stored in a special {{site.data.keyword.registrylong_notm}} `cp.icr.io` domain. To access this domain, you must create an image pull secret with an entitlement key for your cluster and add this image pull secret to the Kubernetes service account of each project where you want to deploy this entitled software.
{: shortdesc}

Before you begin: [Access your {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-access_cluster).

1. Get the entitlement key for your entitled software library.
    1. Log in to [MyIBM.com](https://myibm.ibm.com){: external} and scroll to the **Container software library** section. Click **View library**.
    2. From the **Access your container software > Entitlement keys** page, click **Copy key**. This key authorizes access to all the entitled software in your container software library.
2. In the project that you want to deploy your entitled containers, create an image pull secret so that you can access the `cp.icr.io` entitled registry. Use the **entitlement key** that you previously retrieved as the `--docker-password` value. For more information, see [Accessing images that are stored in other private registries](#private_images).

    ```sh
    oc create secret docker-registry entitled-cp-icr-io --docker-server=cp.icr.io --docker-username=cp --docker-password=<entitlement_key> --docker-email=<docker_email> -n <project>
    ```
    {: pre}

3. Add the image pull secret to the service account of the namespace so that any container in the project can use the entitlement key to pull entitled images. For more information, see [Using the image pull secret to deploy containers](#use_imagePullSecret).

    ```sh
    oc patch -n <project> serviceaccount/default --type='json' -p='[{"op":"add","path":"/imagePullSecrets/-","value":{"name":"entitled-cp-icr-io"}}]'
    ```
    {: pre}

4. Create a pod in the project that builds a container from an image in the entitled registry.

    ```sh
    oc run <pod_name> --image=cp.icr.io/<image_name> -n <project> --generator=run-pod/v1
    ```
    {: pre}

5. Check that your container was able to successfully build from the entitled image by verifying that the pod is in a **Running** status.

    ```sh
    oc get pod <pod_name> -n <project>
    ```
    {: pre}

Wondering what to do next? You can [set up the **entitled** Helm chart repository](/docs/openshift?topic=openshift-helm), where Helm charts that incorporate entitled software are stored. If you already have Helm installed in your cluster, run `helm repo add entitled https://raw.githubusercontent.com/IBM/charts/master/repo/entitled`.
{: tip}



## Adding a private registry to the global pull secret
{: #cluster_global_pull_secret}

With OpenShift Container Platform, you can set up a global image pull secret that each worker node in the cluster can use to pull images from a private registry.
{: shortdesc}

By default, your {{site.data.keyword.openshiftlong_notm}} cluster has a global image pull secret for the following registries, so that default {{site.data.keyword.openshiftshort}} components can be deployed.
* `cloud.openshift.com`
* `quay.io`
* `registry.connect.redhat.com`
* `registry.redhat.io`

Do not replace the global pull secret with a pull secret that does not have credentials to the default Red Hat registries. If you do, the default {{site.data.keyword.openshiftshort}} components that are installed in your cluster, such as the OperatorHub, might fail because they cannot pull images from these registries.
{: important}

Before you begin:
*   [Download the `jq` JSON processor command line package](https://stedolan.github.io/jq/download/){: external}. You use `jq` to combine the JSON value of the default global pull secret with the private registry pull secret that you want to add.
*   [Access your {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-access_cluster).

To add private registries, edit the global `pull-secret` in the `openshift-config` project.
1. Create a secret value that holds the credentials to access your private registry and store the decoded secret value in a JSON file. When you create the secret value, the credentials are automatically encoded to base64. By using the `--dry-run` option, the secret value is created only and no secret object is created in your cluster. The decoded secret value is then stored in a JSON file to later use in your global pull secret.

    ```sh
    oc create secret docker-registry <secret_name> --docker-server=<registry_URL> --docker-username=<docker_username> --docker-password=<docker_password> --docker-email=<docker_email> --dry-run=true --output="jsonpath={.data.\.dockerconfigjson}" | base64 --decode > myregistryconfigjson
    ```
    {: pre}

    `--namespace <project>`
    :   Required. The {{site.data.keyword.openshiftshort}} project of your cluster where you want to use the secret and deploy containers to. To list available projects in your cluster, run `oc get ns`.
    
    `<secret_name>`
    :   Required. The name that you want to use for your image pull secret.
    
    `--docker-server <registry_URL>`
    :   Required. The URL to the registry where your private images are stored.
    
    `--docker-username <docker_username>`
    :   Required. The username to log in to your private registry.
    
    `--docker-password <token_value>`
    :   Required. The password to log in to your private registry, such as a token value.
    
    `--docker-email <docker-email>`
    :   Required. If you have one, enter your Docker email address. If you do not have one, enter a fictional email address, such as `a@b.c`. This email is required to create a Kubernetes secret, but is not used after creation.
    
    `--dry-run=true`
    :   Include this flag to create the secret value only, and not create and store the secret object in your cluster.
    
    `--output="jsonpath={.data.\.dockerconfigjson}"`
    :   Get only the `.dockerconfigjson` value from the data section of the Kubernetes secret.

    `| base64 --decode > myregistryconfigjson`
    :   Download the decoded secret data to a local `myregistryconfigjson` file.

2. Retrieve the decoded secret value of the default global pull secret and store the value in a `dockerconfigjson` file.

    ```sh
    oc get secret pull-secret -n openshift-config --output="jsonpath={.data.\.dockerconfigjson}" | base64 --decode > dockerconfigjson
    ```
    {: pre}

3. Combine the downloaded private registry pull secret `myregistryconfigjson` file with the default global pull secret `dockerconfigjson` file.

    ```sh
    jq -s '.[0] * .[1]' dockerconfigjson myregistryconfigjson > dockerconfigjson-merged
    ```
    {: pre}

4. Update the global pull secret with the combined `dockerconfigjson-merged` file.

    ```sh
    oc set data secret/pull-secret -n openshift-config --from-file=.dockerconfigjson=dockerconfigjson-merged
    ```
    {: pre}

5. Verify that the global pull secret is updated. Check that your private registry and each of the default Red Hat registries are in the output of the following command.

    ```sh
    oc get secret pull-secret -n openshift-config --output="jsonpath={.data.\.dockerconfigjson}" | base64 --decode
    ```
    {: pre}

    Example output

    ```sh
    {
        "auths": {
            "cloud.openshift.com": {
                "auth": "<encoded_string>",
                "email": "email@example.com"
            },
            "quay.io": {
                "auth": "<encoded_string>",
                "email": "email@example.com"
            },
            "registry.connect.redhat.com": {
                "auth": "<encoded_string>",
                "email": "email@example.com"
            },
            "registry.redhat.io": {
                "auth": "<encoded_string>",
                "email": "email@example.com"
            },
            "<private_registry>": {
                "username": "iamapikey",
                "password": "<encoded_string>",
                "email": "email@example.com",
                "auth": "<encoded_string>"
            }
        }
    }
    ```
    {: screen}

6. To pick up the global configuration changes, reload all of the worker nodes in your cluster.
    1. Note the **ID** of the worker nodes in your cluster.

        ```sh
        ibmcloud oc worker ls -c <cluster_name_or_ID>
        ```
        {: pre}

    2. Reload each worker node. You can reload multiple worker nodes by including multiple `-w` flags, but make sure to leave enough worker nodes running at the same time for your apps to avoid an outage.

        ```sh
        ibmcloud oc worker reload -c <cluster_name_or_ID> -w <workerID_1> -w <workerID_2>
        ```
        {: pre}

7. After the worker nodes are back in a healthy state, verify that the global pull secret is updated on a worker node.
    1. Start a debugging pod to log in to a worker node. Use the **Private IP** that you retrieved earlier for the `<node_name>`.

        ```sh
        oc debug node/<node_name>
        ```
        {: pre}

    2. Change the root directory to the host so that you can view files on the worker node.

        ```sh
        chroot /host
        ```
        {: pre}

    3. Verify that the Docker configuration file has the registry credentials that match the global pull secret that you set.

        ```sh
        vi /.docker/config.json
        ```
        {: pre}



## Updating an {{site.data.keyword.containerlong_notm}} containerd custom registry configuration
{: #update_containerd_registry_config}

With Kubernetes version 1.22 or later, you can use containerd configuration files on worker nodes to configure pulling from a container registry. You can use a daemonset to update the configurations across all nodes in a cluster, which prevents configurations from being wiped when worker nodes reload or when new workers are added. 

### Example daemonset to update a containerd custom registry configuration 
{: #ds-example-registry}

Use the example YAML file to define a daemonset that runs on all worker nodes to set or update a containerd registry host configuration and mount to the corresponding containerd registry path.

The example sets the following registry host configuration for dockerhub. This registry host configuration is already provided and automatically configured during the worker provisioning phase. The init container initializes `hosts.toml` on every worker node after deployment and after worker nodes reload or restart. 

```sh
server = "https://docker.io"
[host."https://registry-1.docker.io"]
capabilities = ["pull", "resolve"]
```
{: screen}


**Example YAML file**:

```yaml
apiVersion: apps/v1
kind: DaemonSet
metadata:
labels:
    name: containerd-dockerhub-registry-config
name: containerd-dockerhub-registry-config
namespace: kube-system
spec:
selector:
    matchLabels:
    name: containerd-dockerhub-registry-config
template:
    metadata:
    labels:
        name: containerd-dockerhub-registry-config
    spec:
    initContainers:
    - image: alpine:3.13.6
        name: containerd-dockerhub-registry-config
        command:
        - /bin/sh
        - -c
        - |
            #!/bin/sh
            set -uo pipefail
            cat << EOF > /etc/containerd/certs.d/docker.io/hosts.toml
            server = "https://docker.io"
            [host."https://registry-1.docker.io"]
            capabilities = ["pull", "resolve"]
            EOF
        volumeMounts:
        - mountPath: /etc/containerd/certs.d/docker.io/
        name: dockerhub-registry-config
    containers:
    - name: pause
        image: "us.icr.io/armada-master/pause:3.5"
        imagePullPolicy: IfNotPresent
    volumes:
    - name: dockerhub-registry-config
        hostPath:
        path: /etc/containerd/certs.d/docker.io/
```
{: codeblock}

For more information on updating a containerd registry host configuration, see the [containerd documentation](https://github.com/containerd/containerd/blob/v1.5.6/docs/hosts.md){: external}.
