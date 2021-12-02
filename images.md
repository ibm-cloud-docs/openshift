---

copyright: 
  years: 2014, 2021
lastupdated: "2021-12-01"

keywords: openshift, registry, pull secret, secrets

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}


# Building images for your apps
{: #images}

A Docker image is the basis for every container that you create with {{site.data.keyword.openshiftlong}}.
{: shortdesc}

An image is created from a Dockerfile, which is a file that contains instructions to build the image. A Dockerfile might reference build artifacts in its instructions that are stored separately, such as an app, the app's configuration, and its dependencies.
  
## Building images
{: #build_images}

You can build your images in several ways, including the following {{site.data.keyword.cloud_notm}} services.
{: shortdesc}

{{site.data.keyword.codeenginefull_notm}}
:    {{site.data.keyword.codeengineshort}} supports building images from a Dockerfile and Cloud Native Buildpacks and automatically pushing the images to {{site.data.keyword.registrylong}}. For more information, see [Planning your build](/docs/codeengine?topic=codeengine-plan-build).

Tekton pipelines
:    The {{site.data.keyword.contdelivery_short}} service includes several Tekton tasks that you can reference within your pipelines to build  images. For more information, see [Tekton pipelines](/docs/ContinuousDelivery?topic=ContinuousDelivery-pipeline_container_images#pipeline_tekton_images).

## Deploying containers from an existing image stream in the internal registry
{: #oc_imagestream_deploy}

You can deploy an app from an existing [image stream](https://docs.openshift.com/container-platform/4.8/openshift_images/image-streams-manage.html){: external} that your cluster administrator set up in the internal registry of your {{site.data.keyword.openshiftshort}} cluster. For example, your cluster administrator might have [set up the image stream to import an image from an external private registry](/docs/openshift?topic=openshift-registry#imagestream_registry), such as {{site.data.keyword.registrylong_notm}}.
{: shortdesc}

### Using an image stream with the CLI
{: #oc_imagestream_deploy_cli}

1. [Access your {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-access_cluster).
2. List the available image streams in a project. If you know the project, name, and tag of the image stream, you can use local image streams in other projects without setting up image pull stream credentials.

    ```sh
    oc get is -n <project>
    ```
    {: pre}

3. Create your app from the image stream.

    ```sh
    oc new-app --image-stream="<project>/<imagestream>:<tag>"
    ```
    {: pre}

### Using an image stream from the {{site.data.keyword.openshiftshort}} web console
{: #oc_imagestream_deploy-ui}

1. From the [{{site.data.keyword.openshiftshort}} web console](/docs/openshift?topic=openshift-deploy_app#deploy_apps_ui), switch to the **Developer** perspective and click **+Add**.
2. In the **Add** pane menu bar, select a **Project** that is not `default` to create your app in, and click **Container Image**.
3. In the **Image** section, select **Image name from internal registry**.
4. Select `default` **Project**, `<image>` **ImageStreams**, and `<tag>` **Tag** of the image stream that you previously created.
5. Review the rest of the application details, and click **Create**.





## Deploying containers from an {{site.data.keyword.registrylong_notm}} image to the `default` {{site.data.keyword.openshiftshort}} project
{: #namespace}

You can deploy containers to your cluster from an IBM-provided public image or a private image that is stored in your {{site.data.keyword.registrylong_notm}} namespace. For more information about how your cluster accesses registry images, see [Understanding how your cluster is authorized to pull images from {{site.data.keyword.registrylong_notm}}](/docs/openshift?topic=openshift-registry#cluster_registry_auth).
{: shortdesc}

Before you begin:
1. [Set up a namespace in {{site.data.keyword.registrylong_notm}} and push images to this namespace](/docs/Registry?topic=Registry-getting-started#gs_registry_namespace_add).
2. [Create an {{site.data.keyword.openshiftshort}} cluster](/docs/containers?topic=containers-clusters).
3. [Access your {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-access_cluster).

To deploy a container into the **default** project of your cluster:

1. Create a deployment configuration file that is named `<deployment>.yaml`.
2. Define the deployment and the image to use from your project in {{site.data.keyword.registrylong_notm}}.

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


    `<deployment>`
    :   Give your deployment a name.
    
    `<number_of_replicas>`
    :   Enter the number of replica pods that the deployment creates.
    
    `app: <app_name>`
    :   Use the name of your app as a label for the container.
    
    `name: <app_name>`
    :   Give your container a name, such as the name of your `app` label.
    
    `image: <region>.icr.io/project>/image>:tag>`
    :   Replace the image URL variables with the information for your image:
    :   `region>`: The regional {{site.data.keyword.registrylong_notm}} API endpoint for the registry domain. To list the domain for the region that you are logged in to, run `ibmcloud cr api`.
    :   `namespace>`: The registry namespace. To get your namespace information, run `ibmcloud cr namespace-list`.
    :   `image>:tag>`: The image and tag that you want to use for your container. To list the images that are available in your registry namespace, run `ibmcloud cr images`.


3. Create the deployment in your cluster.

    ```sh
    oc apply -f <deployment>.yaml
    ```
    {: pre}



## Deploying containers from an encrypted image
{: #encrypted-images}

Deploy containers from an encrypted image to your cluster by using the Image Key Synchronizer cluster add-on.
{: shortdesc}

In clusters that run {{site.data.keyword.openshiftshort}} 4.5 or later, [the CRI-O container runtime supports using encrypted container images](https://github.com/cri-o/cri-o/blob/main/tutorials/decryption.md){: external}. Encrypted container images are Open Container Initiative (OCI) images that contain encrypted layer contents. Instead of securing an image for individual developers, such as a developer using image pull secrets to pull images from a registry, you can enable image encryption for a specific cluster. In this way, you can ensure that encrypted images are run only in those specific clusters that have the image decryption key.

To run an app by using an encrypted image, you must share the key for decrypting the image with the container runtime on the worker nodes in the cluster. When you enable the Image Key Synchronizer add-on in your cluster, the synchronizer daemon set is deployed in the `image-key-synchronizer` project. You can then create Kubernetes secrets that contain the image decryption keys in that project. The add-on adds the keys to a specific directory on the worker nodes where the container runtime can access and use the keys to decrypt container images. Note that the Image Key Synchronizer add-on also supports private keys that are first [wrapped by a root key that is stored in an {{site.data.keyword.keymanagementservicelong}} instance](/docs/key-protect?topic=key-protect-envelope-encryption).

Before you begin

1. Download and install the CLI clients for the following open source tools:
    - [OpenSSL](https://www.openssl.org/source/){: external}, to generate an RSA key pair.
    - [Docker Engine CLI](https://www.docker.com/products/container-runtime#/download){: external}, to locally pull images from an image registry.
    - [Skopeo](https://github.com/containers/skopeo/blob/main/install.md){: external}, to encrypt OCI container images.

2. [Access your {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-access_cluster). Note that encrypted images are supported only for {{site.data.keyword.openshiftshort}} version 4.5 and later.

3. Optional: When you create a public and private key pair for the image encryption, you can provide the private key directly in a secret, or first wrap the private key by using a {{site.data.keyword.keymanagementserviceshort}} root key. To prepare to wrap the private key:
    1. [Install the {{site.data.keyword.keymanagementserviceshort}} CLI plug-in](/docs/key-protect?topic=key-protect-set-up-cli).
    2. [Create a {{site.data.keyword.keymanagementserviceshort}} service instance](/docs/key-protect?topic=key-protect-provision#provision).
    3. [Create a {{site.data.keyword.keymanagementserviceshort}} root key](/docs/key-protect?topic=key-protect-create-root-keys#create-root-keys).
    4. Get the following values for your {{site.data.keyword.keymanagementserviceshort}} instance:
        - [The service instance ID](/docs/key-protect?topic=key-protect-retrieve-instance-ID).
        - [The API key for the service instance ID](/docs/account?topic=account-serviceidapikeys#create_service_key).
        - [The service endpoint URL](/docs/key-protect?topic=key-protect-regions#service-endpoints).
    5. Create a Kubernetes secret named `keyprotect-config` that contains the values that you retrieved. The Image Key Synchronizer add-on uses the environment variables in this secret to authenticate with your {{site.data.keyword.keymanagementserviceshort}} instance.
    
        ```yaml
        apiVersion: v1
        kind: Secret
        metadata:
          name: keyprotect-config
          namespace: image-key-synchronizer
        type: Opaque
        stringData:
          config.json: |
              {
                  "keyprotect-url":"<service_endpoint>",
                  "instance-id": "<service_instance_ID>",
                  "apikey": "<service_instance_ID_API_key>"
              }
        ```
        {: codeblock}

To deploy containers that use encrypted images:

1. Enable the Image Key Synchronizer add-on.

    ```sh
    ibmcloud oc cluster addon enable image-key-synchronizer -c <cluster_name_or_ID>
    ```
    {: pre}

2. Verify that the `addon-image-key-syncrhonizer` daemon set was successfully created in the `image-key-synchronizer` project in your cluster.

    ```sh
    oc get ds addon-image-key-syncrhonizer -n image-key-synchronizer
    ```
    {: pre}

3. Use `openssl` to generate a private and public RSA key pair.

    ```sh
    openssl genrsa --out myprivatekey.pem
    openssl rsa -in myprivatekey.pem -pubout -out mypubkey.pem
    ```
    {: pre}

4. Provide the private key directly in a secret, or first wrap the private key by using a {{site.data.keyword.keymanagementserviceshort}} root key. After you create the secret in the `image-key-synchronizer` project, the Image Key Synchronizer add-on automatically copies the private key to the `/etc/crio/keys/synced` directory on your worker nodes.
    - **To provide the private key directly**: Save the private key as a Kubernetes secret in the `image-key-synchronizer` project.
        ```sh
        oc create -n image-key-synchronizer secret generic --type=key --from-file=myprivatekey.pem <secret_name>
        ```
        {: codeblock}

    - **To wrap the private key by using a {{site.data.keyword.keymanagementserviceshort}} root key**:
        1. Encode your private key in base64, and copy the output.

            ```sh
            cat myprivatekey.pem | base64
            ```
            {: pre}

        2. Use the {{site.data.keyword.keymanagementserviceshort}} CLI plug-in to wrap the base64-encoded private key with your root key. In the output, copy the ciphertext of the wrapped private key.

            ```sh
            ibmcloud kp key wrap <root_key_ID> -p <base64_encoded_private_key>
            ```
            {: pre}

        3. Save the wrapped private key as a Kubernetes secret in the `image-key-synchronizer` project.
        
            ```yaml
            apiVersion: v1
            kind: Secret
            type: kp-key
            metadata:
            name: <secret_name>
            namespace: image-key-synchronizer
            stringData:
            rootkeyid: "<root_key_ID>"
            ciphertext: "<wrapped_private_key_cipertext>"
            ```
            {: pre}

        4. Create the secret.
        
            ```sh
            oc apply -n image-key-synchronizer -f <secret_name>.yaml
            ```
            {: pre}

5. Use `docker` to locally pull an OCI image. Replace `<source_image>` with the repository of the image and `<tag>` with the tag of the image that you want to use, such as `latest`.

    ```sh
    docker pull <source_image>:<tag>
    ```
    {: pre}

6. Use `skopeo` to encrypt the local image. This command copies the OCI image that you previously pulled, uses your public key to encrypt the image, and saves the encrypted image to a different local file. Consider naming the encrypted image `<source_image>_encrypted` for easy identification.

    ```sh
    skopeo copy --encryption-key jwe:./mypubkey.pem <source_image>:<tag> <source_image>_encrypted:<tag>
    ```
    {: pre}

7. Optional: To locally verify that the image is encrypted, you can try to decrypt the image with an incorrect key.
    1. Generate a new private key.
    
        ```sh
        openssl genrsa -out wrongkey.pem 1024
        ```
        {: pre}

    2. Attempt to use this new key to decrypt the image. The decryption command fails because the incorrect private key was specified.

        ```sh
        skopeo copy --decryption-key ./wrongkey.pem <source_image>_encrypted:<tag> <source_image>_decrypted:<tag>
        ```
        {: pre}

8. Optional: [Push the encrypted image to {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-getting-started#gs_registry_images_pushing), which supports encrypted OCI images.

9. Specify the encrypted image in your app deployment. For example, if you pushed the encrypted image to {{site.data.keyword.registrylong_notm}}, you can follow the example in [Deploying containers from an {{site.data.keyword.registrylong_notm}} image to the `default` {{site.data.keyword.openshiftshort}} project](/docs/openshift?topic=openshift-images#namespace). When you create the deployment in your cluster, the container runtime uses the private decryption key in the `/etc/crio/keys/synced` directory to decrypt the image before running it.

10. For any subsequent images that you want to encrypt, you can either use the same public key to encrypt the images with Skopeo, or repeat these steps to use a different public and private key pair.

If you later decide to disable the add-on, the `addon-image-key-syncrhonizer` daemon set is removed, but the `image-key-synchronizer` project and any secrets that you created in that project are not removed, and the container runtime can still use the secrets to run encrypted images. If you want to remove the keys from your worker nodes as well, you must delete the corresponding secrets from the `image-key-synchronizer` project before you disable the add-on.
{: note}

For the list of changes for each Image Key Synchronizer add-on version, see the [{{site.data.keyword.cloud_notm}} Image Key Synchronizer add-on changelog](/docs/openshift?topic=openshift-image-key-synchronizer-changelog).
{: tip}





## Referring to the image pull secret in your pod deployment
{: #pod_imagePullSecret}

If the cluster administrator did not [store the image pull secret in the Kubernetes service account](/docs/openshift?topic=openshift-registry#use_imagePullSecret), all deployments that don't specify a service account can't use the image pull secret to deploy containers. Instead, you can define an image pull secret in your pod deployment. When you refer to the image pull secret in a pod deployment, the image pull secret is valid for this pod only and can't be shared across pods in the {{site.data.keyword.openshiftshort}} project.
{: shortdesc}

Before you begin
- [Create an image pull secret](/docs/openshift?topic=openshift-registry#other) to access images in other registries or {{site.data.keyword.openshiftshort}} projects other than `default`.
- [Access your {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-access_cluster).

To refer to the image pull secret in your pod deployment,

1. Create a pod configuration file that is named `mypod.yaml`.
2. Define the pod and the image pull secret to access images in {{site.data.keyword.registrylong_notm}}.

    To access a private image,
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

    To access an {{site.data.keyword.cloud_notm}} public image,
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


    `container_name>`
    :   The name of the container to deploy to your cluster.
    `namespace_name>`
    :   The registry namespace where the image is stored. To list available namespaces, run `ibmcloud cr namespace-list`.
    `image_name>`
    :   The name of the image to use. To list available images in an {{site.data.keyword.cloud_notm}} account, run `ibmcloud cr image-list`.
    `tag>`
    :   The version of the image that you want to use. If no tag is specified, the image that is tagged **latest** is used by default.
    `<secret_name>`
    :   The name of the image pull secret that you created earlier.

3. Save your changes.
4. Create the deployment in your cluster.

    ```sh
    oc apply -f mypod.yaml
    ```
    {: pre}



## Pushing images to {{site.data.keyword.registrylong_notm}}
{: #push-images}

After the cluster administrator [sets up an image registry with {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-getting-started#getting-started), you can securely store and share Docker images with other users by adding images to your namespace.
{: shortdesc}

For example, you might pull an image from any private or public registry source, and then tag it for later use in {{site.data.keyword.registrylong_notm}}. Or, you might push a Docker image that you work with to your namespace so that other users can access the image. To get started, see [Adding images to your namespace](/docs/Registry?topic=Registry-registry_images_).



## Managing security of images in {{site.data.keyword.registrylong_notm}} with Vulnerability Advisor
{: #va-images}

Vulnerability Advisor checks the security status of container images that are provided by IBM, third parties, or added to your organization's {{site.data.keyword.registrylong_notm}} namespace.
{: shortdesc}

When you add an image to a namespace, the image is automatically scanned by Vulnerability Advisor to detect security issues and potential vulnerabilities. If security issues are found, instructions are provided to help fix the reported vulnerability. To get started, see [Managing image security with Vulnerability Advisor](/docs/Registry?topic=va-va_index).



## Setting up trusted content for container images
{: #trusted_images}

You can build containers from trusted images that are signed and stored in {{site.data.keyword.registrylong_notm}}, and prevent deployments from unsigned or vulnerable images.
{: shortdesc}

1. [Sign images for trusted content](/docs/Registry?topic=Registry-registry_trustedcontent#registry_trustedcontent). After you set up trust for your images, you can manage trusted content and signers that can push images to your registry.
2. To enforce a policy so that only signed images can be used to build containers in your cluster, [install the open source Portieris project](#portieris-image-sec).
3. Cluster users can deploy apps that are built from trusted images.
    1. [Deploy to the `default` Kubernetes namespace](/docs/openshift?topic=openshift-images#namespace).
    2. [Deploy to a different Kubernetes namespace, or from a different {{site.data.keyword.cloud_notm}} region or account](/docs/openshift?topic=openshift-registry#other).



## Enabling image security enforcement in your cluster
{: #portieris-image-sec}

When you enable image security enforcement in your cluster, you install the open-source Portieris Kubernetes project. Then, you can create image policies to prevent pods that don't meet the policies, such as unsigned images, from running in your cluster.
{: shortdesc}

For more information, see the [Portieris documentation](https://github.com/IBM/portieris){: external}.

There is a [known issue](https://github.com/IBM/portieris/issues/350){: external} when updating a cluster from {{site.data.keyword.openshiftshort}} 4.7 to {{site.data.keyword.openshiftshort}} 4.8. Do not upgrade your cluster to from version 4.7 to version 4.8 if it has image security enforcement enabled. 
{: important}

**Mutated images**: By default, Portieris uses the `MutatingAdmissionWebhook` admission controller to mutate your image to refer to the image by a digest instead of a tag. However, you might have some deployment technology that rejects a mutated image. If so, you can use the [image mutation option](https://github.com/IBM/portieris/blob/master/README.md#image-mutation-option){: external} and [policy](https://github.com/IBM/portieris/blob/master/POLICIES.md#image-mutation-option){: external} to change the default behavior.
{: note}

### Enabling or disabling image security enforcement
{: #portieris-enable}

**{{site.data.keyword.openshiftshort}} version 4.5 or later**: You can enable or disable image security enforcement for your cluster from the CLI or console. For earlier versions, see the [Portieris documentation](https://github.com/IBM/portieris){: external}.
{: shortdesc}

#### Enabling or disabling image security enforcement with the CLI
{: #portieris-enable-cli}

See the following commands.
- [`ibmcloud oc cluster image-security enable`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs-image-security-enable)
- [`ibmcloud oc cluster image-security disable`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs-image-security-disable)

#### Enabling or disabling image security enforcement from the console
{: #portieris-enable-ui}

1. From the [{{site.data.keyword.openshiftshort}} clusters console](https://cloud.ibm.com/kubernetes/clusters?platformType=openshift){: external}, select your cluster.
2. From the **Overview** tab, in the **Summary** pane, find the **Image security enforcement** field and click **Enable** or **Disable**.

### Default image policies
{: #portieris-default-policies}

When you enable image security enforcement, {{site.data.keyword.openshiftlong_notm}} automatically creates certain image policies in your cluster. When you disable the feature, the underlying `ClusterImagePolicy` CRD is removed, which removes all the default image policies and any custom images policies that you created.
{: shortdesc}

- Image policies with the name `ibm-signed-image-enforcement` restrict the images that are run in the project to {{site.data.keyword.openshiftlong_notm}} images only. Do not modify these image policies. Any changes that you make are overwritten within a few minutes.
- Other image policies, such as `default` or `default-allow-all`, permit images that are not restricted by another image policy. You can modify these image policies and your changes are preserved, but don't rename the image policy. If you rename the policy, more policies with the default name and settings are created.

To review the image policies in your cluster,

Before you begin

[Access your {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-access_cluster).

1. List the image policies that apply globally to the cluster. For an example configuration, see the [Portieris policy documentation](https://github.com/IBM/portieris/blob/master/helm/portieris/templates/policies.yaml#L66){: external}.

    ```sh
    oc get ClusterImagePolicy
    ```
    {: pre}

2. List the image policies that apply to particular namespaces within the cluster. For an example configuration, see the [Portieris policy documentation](https://github.com/IBM/portieris/blob/master/helm/portieris/templates/policies.yaml#L14){: external}.

    ```sh
    oc get ImagePolicy --all-namespaces
    ```
    {: pre}




