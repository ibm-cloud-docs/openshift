---

copyright:
  years: 2014, 2021
lastupdated: "2021-09-21"

keywords: openshift, roks, rhoks, rhos

subcollection: openshift
content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}  

# Why does my build error due to image pull authentication?
{: #ts-app-build-img-pull}
{: troubleshoot}

**Infrastructure provider**:
    * <img src="../images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Classic
    * <img src="../images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> VPC


When a build such as from Operator Hub or the built-in developer content catalog tries to pull an image from a Red Hat registry, the build might fail with an authentication error similar to the following.
{: tsSymptoms}

```
error: build error: After retrying 2 times, Pull image still failed due to error: unauthorized: authentication required
```
{: screen}


By default, your cluster is set up with image pull secrets to Red Hat registries such as `registry.redhat.io`, `registry.connect.redhat.com`, and `cloud.openshift.com`. Additionally in the `default` project, your cluster has image pull secrets to access the `<region>.icr.io` registries for {{site.data.keyword.registrylong_notm}}.
{: tsCauses}

However, if an operator or built-in template has a build component that must pull an image from a private registry, the build might fail with an authentication error because the build does not have access to the default image pull secrets in its service account. By default, builds can pull images that are stored only in the internal registry.


Set up the build with access to the image, either by pulling the image from the private registry or by importing the image from the private registry into the internal registry.
{: tsResolve} 

For more information, see the [{{site.data.keyword.openshiftshort}} documentation](http://docs.openshift.com/container-platform/4.7/cicd/builds/creating-build-inputs.html){: external}.

1. Check the build configuration file to see what registry the build needs pull access to. For example, if your build is part of an {{site.data.keyword.openshiftshort}} template, the build config `spec.strategy.sourceStrategy.from.name` value refers to the `registry.redhat.io` private registry.
    ```
    oc -n openshift get template react-web-app-example -o yaml
    ```
    {: pre}

    Example output:
    ```
    strategy:
      sourceStrategy:
        from:
          kind: DockerImage
          name: registry.redhat.io/rhoar-nodejs-tech-preview/rhoar-nodejs-10-webapp
    ```
    {: screen}

2. Set up the build with image pull access. You can choose from pulling the image from the private registry or using an image stream from the internal registry.
    *   **Pull image from a private registry**:
        1. In each project, add an image pull secret with pull access to the private registry that the build uses.    
            *  **For Red Hat registries**: [Copy the `pull-secret` secret](/docs/openshift?topic=openshift-registry#copy_imagePullSecret) from the `openshift-config` project. This secret includes pull access to the following private registries: `cloud.openshift.com`, `quay.io`, `registry.connect.redhat.com`, and `registry.redhat.io`.
            *  **For {{site.data.keyword.registrylong_notm}}**: [Copy the `<region>.icr.io` secrets](/docs/openshift?topic=openshift-registry#copy_imagePullSecret) from the `default` project.
            *  **For other private registries**: [Create an image pull secret](/docs/openshift?topic=openshift-registry#private_images) with image pull access to the private registry.
        2. [Add the secret to the builder service account](/docs/openshift?topic=openshift-registry#store_imagePullSecret) or [specify the image pull secret in the build configuration file](/docs/openshift?topic=openshift-images#pod_imagePullSecret).

            Example to link the secret to the builder service account in a project.
            ```
            oc secrets link builder <pull-secret>
            ```
            {: pre}

            Example to refer to the secret in the build configuration file.
            ```
            spec:
              output:
                to:
                  kind: "DockerImage"
                  name: "<private.registry.com>/<namespace>/<image>:<tag>"
                pushSecret:
                  name: "<pull-secret>"
            ```
            {: codeblock}

    * **Use an image stream from the internal registry**: [Create an image stream in the internal registry from an imported image from the private registry](/docs/openshift?topic=openshift-registry#imagestream_registry). Then, update the build configuration file to refer to the image stream instead of pulling the image directly from the private registry.


