---

copyright:
  years: 2014, 2022
lastupdated: "2022-06-28"

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
* Deprecated: [{{site.data.keyword.redhat_openshift_notm}} 3.11 release notes overview](https://docs.openshift.com/container-platform/3.11/release_notes/index.html){: external}
* [Kubernetes change log](https://github.com/kubernetes/kubernetes/tree/master/CHANGELOG){: external}

## Available {{site.data.keyword.redhat_openshift_notm}} versions
{: #openshift_versions_available}

{{site.data.keyword.openshiftlong_notm}} supports the following versions of {{site.data.keyword.redhat_openshift_notm}}. The worker node operating system is Red Hat Enterprise Linux 7.

Supported versions
:   4.10 (Kubernetes 1.23)
    - [Version information and update actions](/docs/openshift?topic=openshift-cs_versions_410)
    - [Change log](/docs/openshift?topic=openshift-openshift_changelog_410)
   
:   **Default**: 4.9 (Kubernetes 1.22)
    - [Version information and update actions](/docs/openshift?topic=openshift-cs_versions_49)
    - [Change log](/docs/openshift?topic=openshift-openshift_changelog_49)

:   4.8 (Kubernetes 1.21)
    - [Version information and update actions](/docs/openshift?topic=openshift-cs_versions_48)
    - [Change log](/docs/openshift?topic=openshift-openshift_changelog_48)

:   4.7 (Kubernetes 1.20)
    - [Version information and update actions](/docs/openshift?topic=openshift-cs_versions_47)
    - [Change log](/docs/openshift?topic=openshift-openshift_changelog_47)

:    4.6 (Kubernetes 1.19)
    - [Version information and update actions](/docs/openshift?topic=openshift-cs_versions_46)
    - [Change log](/docs/openshift?topic=openshift-openshift_changelog_46)




Unsupported versions:
:   4.3 (Kubernetes 1.16), 4.4 (Kubernetes 1.17), 4.5 (Kubernetes 1.18)
:   [Archived change logs](#version-archive)

:   3.11 (Kubernetes 1.15)
    - [Version information and update actions](/docs/openshift?topic=openshift-openshift_changelog_311)
    - [Change log](/docs/openshift?topic=openshift-openshift_changelog_311)
     

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

## Release history
{: #openshift_release_history}

The following table records {{site.data.keyword.openshiftlong_notm}} version release history. You can use this information for planning purposes, such as to estimate general times when a certain release might become unsupported.
{: shortdesc}

Dates that are marked with a dagger (`†`) are tentative and subject to change.
{: important}

| Supported? | {{site.data.keyword.redhat_openshift_notm}} / Kubernetes version | Release date | Unsupported date |
| --- | --- | --- | --- |
| Supported | 4.10 / 1.23 | 27 Apr 2022 | October 2023`†` |
| Supported | 4.9 / 1.22 | 09 Feb 2022 | May 2023`†` |
| Supported | 4.8 / 1.21 | 29 Sep 2021 | Feb 2023`†` |
| Supported | 4.7 / 1.20 | 09 Jun 2021 | Dec 2022`†` |
| Supported | 4.6 / 1.19 | 17 Feb 2021 | 27 Oct 2022 `†` |
| Not supported | 4.5 / 1.18 | 13 Oct 2020 | 10 Oct 2021 |
| Not supported | 4.4 / 1.17 | 21 Jul 2020 | 31 May 2021 |
| Not supported | 4.3 / 1.16 | 20 Apr 2020 | 7 Mar 2021 |
| Not supported | 3.11 / 1.11 | 01 Aug 2019 | 06 Jun 2022 |
{: caption="Release history for {{site.data.keyword.openshiftlong_notm}}." caption-side="top"}
{: summary="The rows are read from left to right. The first column is the supported status, the second column is OpenShift and Kubernetes version number. The third column is the release date. The fourth column is the unsupported date."}

**How soon after an OCP release is the version available in {{site.data.keyword.cloud_notm}}?**

After the Red Hat OpenShift Container Platform community releases a version update, the IBM team begins a process of hardening and testing the release for {{site.data.keyword.openshiftlong_notm}} environments. Availability and unsupported release dates depend on the results of these tests, community updates, security patches, and technology changes between versions. Plan to keep your cluster master and worker node version up-to-date.

**Why is the deprecated version 3.11 supported longer than more recent versions like 4.3?**

In general, the last minor version of a major version is supported longer than other minor versions. Because you can't update a cluster from one major version to another (such as version 3 to 4), this longer support period gives you time to create clusters at a more recent version. Minor versions of a more recent major version might become unsupported before the last minor version of a deprecated major version because the more recent major version has subsequent minor releases that are supported. For example, version 4.3 becomes unsupported before the deprecated version 3.11 because version 4 has future minor releases, but 3.11 is the last minor version of version 3.

**What is different for deprecated versions?**

Your apps still run, and you can log in to the cluster to manage your {{site.data.keyword.redhat_openshift_notm}} resources. You can still manage your cluster lifecycle, such as by adding and reloading worker nodes. However, security patch updates might not be provided. To continue receiving important security updates and the latest functionality, create a cluster at a supported version. You receive a notification in the console and CLI to update your cluster to a supported version about 45 days before the deprecated version becomes unsupported.

## Archive
{: #version-archive}

Review unsupported versions of {{site.data.keyword.openshiftlong_notm}}.
{: shortdesc}

### {{site.data.keyword.redhat_openshift_notm}} 4.5 (Unsupported)
{: #ocp45}

As of 10 October 2021, {{site.data.keyword.openshiftlong_notm}} clusters that run [version 4.5](/docs/openshift?topic=openshift-changelog_archive) are unsupported.
{: shortdesc}

Unsupported clusters are not provided with security and patch updates and are not supported by {{site.data.keyword.cloud_notm}} Support. Although your cluster and apps might continue to run for a time, you can no longer create, reload, or take other corrective actions on your cluster master or worker nodes when an issue occurs. You can still delete the cluster or worker nodes, or update the cluster to the next version. Review the potential impacts and immediately [update the cluster](/docs/containers?topic=containers-update#update) to continue receiving important security updates and support.

### {{site.data.keyword.redhat_openshift_notm}} 4.4 (Unsupported)
{: #ocp44}

As of 31 May 2021, {{site.data.keyword.openshiftlong_notm}} clusters that run [version 4.4](/docs/openshift?topic=openshift-changelog_archive) are unsupported.
{: shortdesc}

Unsupported clusters are not provided with security and patch updates and are not supported by {{site.data.keyword.cloud_notm}} Support. Although your cluster and apps might continue to run for a time, you can no longer create, reload, or take other corrective actions on your cluster master or worker nodes when an issue occurs. You can still delete the cluster or worker nodes. To continue running your apps in {{site.data.keyword.openshiftlong_notm}}, [make a new cluster](/docs/containers?topic=containers-clusters#clusters) and [deploy your apps](/docs/containers?topic=containers-app#app) to the new cluster.

### {{site.data.keyword.redhat_openshift_notm}} 4.3 (Unsupported)
{: #ocp43}

As of 7 March 2021, {{site.data.keyword.openshiftlong_notm}} clusters that run [version 4.3](/docs/openshift?topic=openshift-changelog_archive) are unsupported.
{: shortdesc}

Unsupported clusters are not provided with security and patch updates and are not supported by {{site.data.keyword.cloud_notm}} Support. Although your cluster and apps might continue to run for a time, you can no longer create, reload, or take other corrective actions on your cluster master or worker nodes when an issue occurs. You can still delete the cluster or worker nodes. To continue running your apps in {{site.data.keyword.openshiftlong_notm}}, [make a new cluster](/docs/containers?topic=containers-clusters#clusters) and [deploy your apps](/docs/containers?topic=containers-app#app) to the new cluster.

### {{site.data.keyword.redhat_openshift_notm}} 3.11 (Unsupported)
{: #ocp311}

As of 6 June 2022, {{site.data.keyword.openshiftlong_notm}} clusters that run [version 3.11](/docs/openshift?topic=openshift-changelog_archive) are unsupported.
{: shortdesc}

Unsupported clusters are not provided with security and patch updates and are not supported by {{site.data.keyword.cloud_notm}} Support. Although your cluster and apps might continue to run for a time, you can no longer create, reload, or take other corrective actions on your cluster master or worker nodes when an issue occurs. You can still delete the cluster or worker nodes. To continue running your apps in {{site.data.keyword.openshiftlong_notm}}, [make a new cluster](/docs/containers?topic=containers-clusters#clusters) and [deploy your apps](/docs/containers?topic=containers-app#app) to the new cluster.