---

copyright:
  years: 2014, 2021
lastupdated: "2021-10-04"

keywords: openshift, debug

subcollection: openshift
content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

  

# Why does the `oc debug` command fail with a `container is unable to start error`?
{: #ts-app-oc-debug}
{: troubleshoot}



When you run the `oc debug` command on a private cluster, you see an error message similar to the following.
{: tsSymptoms}

```sh
oc debug node/<node-name>
Starting pod/1024104-debug ...
To use host binaries, run `chroot /host`

warning: Container container-00 is unable to start due to an error: Back-off pulling image "quay.io/openshift-release-dev/ocp-v4.0-art-dev@sha256:7dd7a3a1be7009629c709e6c88a1551d471aba9bf3deb873bc5f4d814675edfe"
```
{: screen}

The `oc debug` command starts a debug pod on the node that you specify. The debug pod uses a public container image from the `quay.io` container registry. On private clusters without access to the public Internet, your cluster can't pull the debug container image from the public registry.
{: tsCauses}


To resolve this issue, pull an `ocp-release` image from `quay.io` and push it to your private image registry. Then, when you run the `oc debug` command, specify the private container image that you want to use.
{: tsResolve}


1. Pull an image from [quay.io](https://quay.io/repository/openshift-release-dev/ocp-release?tab=tags){: external} that matches your cluster version and architecture. For example, if you have a `4.7.19` cluster, pull the `quay.io/openshift-release-dev/ocp-release:4.7.19-x86_64` image. Note that you must have a Red Hat account and permissions to pull images.
    ```sh
    docker pull quay.io/openshift-release-dev/ocp-release:4.7.19-x86_64
    ```
    {: pre}

1. [Tag and push the image to your private container registry](/docs/Registry?topic=Registry-getting-started).

1. Retry the `oc debug` command with the `--image=icr.io` flag.
    ```sh
    oc debug node/<node-name> --image=icr.io/<namespace>/<image>:<tag>
    ```
    {: pre}







