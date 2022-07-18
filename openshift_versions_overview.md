---

copyright:
  years: 2014, 2022
lastupdated: "2022-07-18"

keywords: openshift, version, update, upgrade

subcollection: openshift

---


{{site.data.keyword.attribute-definition-list}}


# {{site.data.keyword.openshiftshort}} version information
{: #openshift_versions}

Review information about the supported {{site.data.keyword.redhat_openshift_notm}} versions for {{site.data.keyword.openshiftlong}} clusters.
{: shortdesc}

For more details about the {{site.data.keyword.redhat_openshift_notm}} and Kubernetes project versions, review the RedHat OpenShift release notes.
* [{{site.data.keyword.redhat_openshift_notm}} 4.10 release notes overview](https://docs.openshift.com/container-platform/4.10/release_notes/ocp-4-10-release-notes.html){: external}
* [{{site.data.keyword.redhat_openshift_notm}} 4.9 release notes overview](https://docs.openshift.com/container-platform/4.9/release_notes/ocp-4-9-release-notes.html){: external}
* [{{site.data.keyword.redhat_openshift_notm}} 4.8 release notes overview](https://docs.openshift.com/container-platform/4.8/release_notes/ocp-4-8-release-notes.html){: external}
* [{{site.data.keyword.redhat_openshift_notm}} 4.7 release notes overview](https://docs.openshift.com/container-platform/4.7/release_notes/ocp-4-7-release-notes.html){: external}
* [{{site.data.keyword.redhat_openshift_notm}} 4.6 release notes overview](https://docs.openshift.com/container-platform/4.6/release_notes/ocp-4-6-release-notes.html){: external}
* [Kubernetes change log](https://github.com/kubernetes/kubernetes/tree/master/CHANGELOG){: external}

## Available {{site.data.keyword.redhat_openshift_notm}} versions
{: #openshift_versions_available}

{{site.data.keyword.openshiftlong_notm}} supports the following versions of {{site.data.keyword.redhat_openshift_notm}}. The worker node operating system is Red Hat Enterprise Linux (RHEL) 7.  

Dates that are marked with a dagger (`†`) are tentative and subject to change.
{: important}

Supported versions
:   4.10 (Kubernetes 1.23)
    - Release date: **27 Apr 2022**
    - Tentative unsupported date: **25 Oct 2023**`†`
    - [Version information and update actions](/docs/openshift?topic=openshift-cs_versions_410)
    - [Change log](/docs/openshift?topic=openshift-openshift_changelog_410)
   
:   **Default**: 4.9 (Kubernetes 1.22)
    - Release date: **09 Feb 2022**
    - Tentative unsupported date: **12 Jul 2023**`†`
    - [Version information and update actions](/docs/openshift?topic=openshift-cs_versions_49)
    - [Change log](/docs/openshift?topic=openshift-openshift_changelog_49)

:   4.8 (Kubernetes 1.21)
    - Release date: **29 Sep 2021**
    - Tentative unsupported date: **29 Mar 2023**`†`
    - [Version information and update actions](/docs/openshift?topic=openshift-cs_versions_48)
    - [Change log](/docs/openshift?topic=openshift-openshift_changelog_48)

:   4.7 (Kubernetes 1.20)
    - Release date: **09 Jun 2021**
    - Tentative unsupported date: **7 Dec 2022**`†`
    - [Version information and update actions](/docs/openshift?topic=openshift-cs_versions_47)
    - [Change log](/docs/openshift?topic=openshift-openshift_changelog_47)

:   4.6 (Kubernetes 1.19)
    - Release date: **17 Feb 2021**
    - Tentative unsupported date: **27 Oct 2022**`†`
    - [Version information and update actions](/docs/openshift?topic=openshift-cs_versions_46)
    - [Change log](/docs/openshift?topic=openshift-openshift_changelog_46)



Unsupported versions:
:    For infomation about unsupported versions, see the [archive](#version-archive). 

## Checking a cluster's Kubernetes server version
{: #openshift_server_version}

To check the Kubernetes server version of a cluster, log in to the cluster and run the following command.
{: shortdesc}

```sh
oc version
```
{: pre}

Example output
```sh
Client Version: 4.9.3
Server Version: 4.9.12
Kubernetes Version: v1.22.2
```
{: screen}

## Release lifecycle
{: #openshift_release_history}

Each supported version of IBM Cloud Kubernetes Service goes through a lifecycle of testing, development, general release, support, deprecation, and becoming unsupported. Review the descriptions of each phase of a version's lifecycle. 
{: shortdesc}

Estimated days and versions are provided for general understanding. Actual availability and release dates are subject to change and depend on various factors, such as community updates, security patches, and technology changes between versions.
{: note}

1. **Community release**: The OpenShift Container Platform community releases a new version. IBM engineers begin a process of testing and hardening the community version in preparation to release a supported RedHat OpenShift on IBM Cloud Service version.
2. **Latest supported version**: The version is released as the latest supported RedHat OpenShift on IBM Cloud Service version.
3. **Default version**: The version becomes the default supported RedHat OpenShift on IBM Cloud Service version.
4. **Supported version**: The version remains supported but is no longer the default version.
5. **Deprecated**: The version is deprecated, and security patch updates might not be provided. Versions are deprecated for approximately 90 days. Approximately 45 days after deprecation, you receive a notification in the console and CLI that you have approximately 45 days remaining to update your cluster to a supported version before its current version becomes unsupported. During the deprecation period, the version is still supported and your cluster is still functional, but might require updating to a supported release to fix security vulnerabilities. For example, you can add and reload worker nodes.
6. **Unsupported**: The version is unsupported. Unsupported clusters are not provided with security and patch updates and are not supported by {{site.data.keyword.cloud_notm}} Support. Although your cluster and apps might continue to run for a time, you can no longer create, reload, or take other corrective actions on your cluster master or worker nodes when an issue occurs. You can still delete the cluster or worker nodes, or update the cluster to the next version. Review the potential impacts and immediately [update the cluster](/docs/openshift?topic=openshift-update#update) to continue receiving important security updates and support. If the cluster master runs two or more versions behind the oldest supported version, you can no longer apply updates and must delete the cluster and create a new one.



## Archive
{: #version-archive}

Unsupported clusters are not provided with security and patch updates and are not supported by {{site.data.keyword.cloud_notm}} Support. Although your cluster and apps might continue to run for a time, you can no longer create, reload, or take other corrective actions on your cluster master or worker nodes when an issue occurs. You can still delete the cluster or worker nodes, or update the cluster to the next version. Review the potential impacts and immediately [update the cluster](/docs/openshift?topic=openshift-update#update) to continue receiving important security updates and support. If your cluster master is two or more versions behind the oldest supported version, you must [make a new cluster](/docs/openshift?topic=openshift-clusters#clusters) and [deploy your apps](/docs/openshift?topic=openshift-deploy_app) to the new cluster.
{: shortdesc}

**Unsupported Kubernetes versions**: 
:    [4.5](/docs/openshift?topic=openshift-changelog_archive#version-45), [4.4](/docs/openshift?topic=openshift-changelog_archive#version-44), [4.3](/docs/openshift?topic=openshift-changelog_archive#version-43), [3.11](/docs/openshift?topic=openshift-openshift_changelog_311).

