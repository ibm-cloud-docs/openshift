---

copyright:
  years: 2014, 2021
lastupdated: "2021-11-22"

keywords: openshift, version, update, upgrade

subcollection: openshift

---


{{site.data.keyword.attribute-definition-list}}




# Version information and update actions
{: #openshift_versions}

Review information about the supported {{site.data.keyword.openshiftshort}} versions for {{site.data.keyword.openshiftlong}} clusters.
{: shortdesc}

For more information about the {{site.data.keyword.openshiftshort}} and Kubernetes project versions, review the following information.
* [{{site.data.keyword.openshiftshort}} 4.8 release notes overview](https://docs.openshift.com/container-platform/4.8/release_notes/ocp-4-8-release-notes.html){: external}
* [{{site.data.keyword.openshiftshort}} 4.7 release notes overview](https://docs.openshift.com/container-platform/4.7/release_notes/ocp-4-7-release-notes.html){: external}
* [{{site.data.keyword.openshiftshort}} 4.6 release notes overview](https://docs.openshift.com/container-platform/4.6/release_notes/ocp-4-6-release-notes.html){: external}
* Deprecated: [{{site.data.keyword.openshiftshort}} 3.11 release notes overview](https://docs.openshift.com/container-platform/3.11/release_notes/index.html){: external}
* [Kubernetes changelog](https://github.com/kubernetes/kubernetes/tree/master/CHANGELOG){: external}

## Update types
{: #openshift_update_types}

Your {{site.data.keyword.openshiftlong_notm}} cluster has three types of updates: major, minor, and patch. As updates become available, you are notified when you view information about the cluster master or worker nodes, such as with the `ibmcloud oc cluster ls`, `cluster get`, `worker ls`, or `worker get` commands.
{: shortdesc}

You must [update your cluster](/docs/openshift?topic=openshift-update) by using the {{site.data.keyword.openshiftlong_notm}} API, CLI, or console tools. You can't update your cluster version from OpenShift Container Platform tools such as the {{site.data.keyword.openshiftshort}} web console.
{: note}

|Update type|Examples of version labels|Updated by|Impact
|-----|-----|-----|-----|
|Major|4.x.x|You|Operation changes for clusters, including scripts or deployments.|
|Minor|x.6.x|You|Operation changes for clusters, including scripts or deployments.|
|Patch|x.x.18_1533|IBM and you|{{site.data.keyword.openshiftshort}} patches, as well as other {{site.data.keyword.cloud_notm}} Provider component updates such as security and operating system patches. IBM updates masters automatically, but you apply patches to worker nodes. See more about patches in the following section.|
{: caption="Impacts of {{site.data.keyword.openshiftshort}} updates" caption-side="top"}

### Major and minor updates (4.7)
{: #major_minor_updates}

First, [update your master node](/docs/openshift?topic=openshift-update#master) and then [update the worker nodes](/docs/openshift?topic=openshift-update#worker_node). Worker nodes can't run an {{site.data.keyword.openshiftshort}} major or minor version that is greater than the masters. Additionally, your worker nodes can be only one version behind the master version (`n-1`).
{: shortdesc}

If you use an `oc` or `oc` CLI version that does match at least the `major.minor` version of your clusters, you might experience unexpected results. Make sure to keep your cluster and [CLI versions](/docs/openshift?topic=openshift-openshift-cli#cli_oc) up-to-date.
{: note}


### Patch updates (4.7.29_xxxx_openshift)
{: #patch_updates_oc}

Changes across patches are documented in the [Version changelog](/docs/openshift?topic=openshift-openshift_versions). Master patches are applied automatically, but you initiate worker node patches updates.
{: shortdesc}

Worker nodes can also run patch versions that are greater than the masters. As updates become available, you are notified when you view information about the master and worker nodes in the {{site.data.keyword.cloud_notm}} console or CLI, such as with the following commands: `ibmcloud oc cluster ls`, `cluster get`, `worker ls`, or `worker get`. Patches can be for worker nodes, masters, or both.

**Worker node patches**: Check monthly to see whether an update is available, and use the `ibmcloud oc worker update` [command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_update) or the `ibmcloud oc worker reload` [command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_reload) to apply these security and operating system patches. During an update or reload, your worker node machine is reimaged, and data is deleted if not [stored outside the worker node](/docs/openshift?topic=openshift-storage_planning#persistent_storage_overview).

**Master patches**: Master patches are applied automatically over the course of several days, so a master patch version might show up as available before it is applied to your master. The update automation also skips clusters that are in an unhealthy state or have operations currently in progress. Occasionally, IBM might disable automatic updates for a specific master fix pack, as noted in the changelog, such as a patch that is only needed if a master is updated from one minor version to another. In any of these cases, you can choose to safely use the `ibmcloud oc cluster master update` [command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_cluster_update) yourself without waiting for the update automation to apply. When a master patch update is initiated for a cluster, the `containers-kubernetes.version.update` event is [sent to {{site.data.keyword.at_short}}](/docs/openshift?topic=openshift-at_events).






## {{site.data.keyword.openshiftshort}} versions
{: #version_types}

{{site.data.keyword.openshiftlong_notm}} supports the following versions of {{site.data.keyword.openshiftshort}}. The worker node operating system is Red Hat Enterprise Linux 7.

**Supported versions**:
* Latest: 4.8 (Kubernetes 1.21)
* Default: 4.7 (Kubernetes 1.20)
* 4.6 (Kubernetes 1.19)

**Deprecated and unsupported versions**:
* Deprecated: 3.11 (Kubernetes 1.11)
* Unsupported: 4.3 (Kubernetes 1.16), 4.4 (Kubernetes 1.17), 4.5 (Kubernetes 1.18)

To check the Kubernetes server version of a cluster, log in to the cluster and run the following command.

```sh
oc version
```
{: pre}

Example output
```sh
Client Version: 4.7.3
Server Version: 4.7.12
Kubernetes Version: v1.20.2
```
{: screen}

## Release history
{: #openshift_release_history}

The following table records {{site.data.keyword.openshiftlong_notm}} version release history. You can use this information for planning purposes, such as to estimate general time frames when a certain release might become unsupported.
{: shortdesc}

**How soon after an OCP release is the version available in {{site.data.keyword.cloud_notm}}?**

After the Red Hat OpenShift Container Platform community releases a version update, the IBM team begins a process of hardening and testing the release for {{site.data.keyword.openshiftlong_notm}} environments. Availability and unsupported release dates depend on the results of these tests, community updates, security patches, and technology changes between versions. Plan to keep your cluster master and worker node version up-to-date.

**Why is the deprecated version 3.11 supported longer than more recent versions like 4.3?**

In general, the last minor version of a major version is supported longer than other minor versions. Because you can't update a cluster from one major version to another (such as version 3 to 4), this longer support period gives you time to create clusters at a more recent version. Minor versions of a more recent major version might become unsupported before the last minor version of a deprecated major version because the more recent major version has subsequent minor releases that are supported. For example, version 4.3 becomes unsupported before the deprecated version 3.11 because version 4 has future minor releases, but 3.11 is the last minor version of version 3.

**What is different for deprecated versions?**

Your apps still run, and you can log in to the cluster to manage your {{site.data.keyword.openshiftshort}} resources. You can still manage your cluster lifecycle, such as by adding and reloading worker nodes. However, security patch updates might not be provided. To continue receiving important security updates and the latest functionality, create a cluster at a supported version. You receive a notification in the console and CLI to update your cluster to a supported version about 45 days before the deprecated version becomes unsupported.

Dates that are marked with a dagger (`†`) are tentative and subject to change.
{: important}

| Supported? | {{site.data.keyword.openshiftshort}} / Kubernetes version | Release date | Unsupported date |
| --- | --- | --- | --- |
| Supported | 4.8 / 1.21 | 29 Sep 2021 | Sep 2022`†` |
| Supported | 4.7 / 1.20 | 09 Jun 2021 | Jul 2022`†` |
| Supported | 4.6 / 1.19 | 17 Feb 2021 | May 2022 `†` |
| Not supported | 4.5 / 1.18 | 13 Oct 2020 | Oct 10 2021 `†` |
| Not supported | 4.4 / 1.17 | 21 Jul 2020 | 31 May 2021 |
| Not supported | 4.3 / 1.16 | 20 Apr 2020 | 7 Mar 2021 |
| Deprecated | 3.11 / 1.11 | 01 Aug 2019 | 06 Jun 2022 `†` |
{: caption="Release history for {{site.data.keyword.openshiftlong_notm}}." caption-side="top"}
{: summary="The rows are read from left to right. The first column is the supported status, the second column is OpenShift and Kubernetes version number. The third column is the release date. The fourth column is the unsupported date."}

## {{site.data.keyword.openshiftshort}} 4.8
{: #ocp48}

There is a [known issue](https://github.com/IBM/portieris/issues/350){: external} when updating a cluster from {{site.data.keyword.openshiftshort}} 4.7 to {{site.data.keyword.openshiftshort}} 4.8. Do not upgrade your cluster to from version 4.7 to version 4.8 if it has image security enforcement enabled. 
{: important}

![This badge indicates Kubernetes version 1.21 certification for {{site.data.keyword.containerlong_notm}}](images/certified_kubernetes_1x21.svg)
{{site.data.keyword.containerlong_notm}} is a Certified Kubernetes product for version 1.21 under the CNCF Kubernetes Software Conformance Certification program. _Kubernetes® is a registered trademark of The Linux Foundation in the United States and other countries, and is used pursuant to a license from The Linux Foundation._

Review changes that you might need to make when you [update a cluster](/docs/openshift?topic=openshift-update) that runs {{site.data.keyword.openshiftshort}} 4.7 to {{site.data.keyword.openshiftshort}} 4.8.
{: shortdesc}

### Update before master
{: #48_before}

The following table shows the actions that you must take before you [update the cluster master](/docs/openshift?topic=openshift-update#master).
{: shortdesc}

| Type | Description |
| ---- | ----------- |
| **Unsupported:** Deprecated and removed OpenShift features | For more information, review [OpenShift version 4.8 deprecated and removed features](https://docs.openshift.com/container-platform/4.8/release_notes/ocp-4-8-release-notes.html#ocp-4-8-deprecated-removed-features){: external}. |
| Container runtime default security context capabilities | The container runtime (i.e. CRI-O) default security context capabilities have been changed to match Red Hat OpenShift Container Platform (OCP). `NET_RAW` and `SYS_CHROOT` have been removed. This brings the security behavior of containers in line with OCP. If your app requires either of these capabilities and does not list them in the container or pod `securityContext`, then the app must be changed to include these capabilities. If these changes are not made, your microservices might fail to start and you might see a `permission denied` error. Applications developed for OCP already have the necessary changes.  |

## {{site.data.keyword.openshiftshort}} 4.7
{: #ocp47}

![This badge indicates Kubernetes version 1.20 certification for {{site.data.keyword.containerlong_notm}}](images/certified_kubernetes_1x20.svg)
{{site.data.keyword.containerlong_notm}} is a Certified Kubernetes product for version 1.20 under the CNCF Kubernetes Software Conformance Certification program. _Kubernetes® is a registered trademark of The Linux Foundation in the United States and other countries, and is used pursuant to a license from The Linux Foundation._

Review changes that you might need to make when you [update a cluster](/docs/openshift?topic=openshift-update) that runs {{site.data.keyword.openshiftshort}} 4.6 to {{site.data.keyword.openshiftshort}} 4.7.
{: shortdesc}

### Update before master
{: #47_before}

The following table shows the actions that you must take before you [update the cluster master](/docs/openshift?topic=openshift-update#master).
{: shortdesc}

| Type | Description |
| ---- | ----------- |
| Kubernetes snapshot CRDs | {{site.data.keyword.containerlong_notm}} installs Kubernetes snapshot custom resource definition (CRD) version `v1beta1`. If you use other Kubernetes snapshot CRD versions `v1` or `v1alpha1`, you must change the version to `v1beta1`. To check the currently installed version of your snapshot CRDs, run `grep snapshot.storage.k8s.io <<(kubectl get apiservices)`. Follow the Kubernetes documentation to [Upgrade from v1alpha1 to v1beta1](https://github.com/kubernetes-csi/external-snapshotter#upgrade-from-v1alpha1-to-v1beta1){: external} to make sure that your snapshot CRDs are at the correct `v1beta1` version. The steps to downgrade from version `v1` to `v1beta1` are the same as those to upgrade from `v1alpha1`. Do not follow the instructions to upgrade from version `v1beta1` to version `v1`. |
| **Unsupported:** Deprecated and removed {{site.data.keyword.openshiftshort}} features | For more information, review the [{{site.data.keyword.openshiftshort}} version 4.7 deprecated and removed features](https://docs.openshift.com/container-platform/4.7/release_notes/ocp-4-7-release-notes.html#ocp-4-7-deprecated-removed-features){: external}. |
{: caption="Changes to make before you update the master to {{site.data.keyword.openshiftshort}} 4.7" caption-side="top"}
{: summary="The rows are read from left to right. The type of update action is in the first column, and a description of the update action type is in the second column."}



## {{site.data.keyword.openshiftshort}} 4.6
{: #ocp46}

![This badge indicates Kubernetes version 1.19 certification for {{site.data.keyword.containerlong_notm}}](images/certified_kubernetes_1x19.svg)
{{site.data.keyword.containerlong_notm}} is a Certified Kubernetes product for version 1.19 under the CNCF Kubernetes Software Conformance Certification program. _Kubernetes® is a registered trademark of The Linux Foundation in the United States and other countries, and is used pursuant to a license from The Linux Foundation._

Review changes that you might need to make when you [update a cluster](/docs/openshift?topic=openshift-update) that runs {{site.data.keyword.openshiftshort}} 4.5 to {{site.data.keyword.openshiftshort}} 4.6.
{: shortdesc}

### Update before master
{: #46_before}

The following table shows the actions that you must take before you [update the cluster master](/docs/openshift?topic=openshift-update#master).
{: shortdesc}

| Type | Description |
| ---- | ----------- |
| Kubernetes snapshot CRDs | {{site.data.keyword.containerlong_notm}} installs Kubernetes snapshot custom resource definition (CRD) version `v1beta1`. If you use other Kubernetes snapshot CRD versions `v1` or `v1alpha1`, you must change the version to `v1beta1`. To check the currently installed version of your snapshot CRDs, run `grep snapshot.storage.k8s.io <<(kubectl get apiservices)`. Follow the Kubernetes documentation to [Upgrade from v1alpha1 to v1beta1](https://github.com/kubernetes-csi/external-snapshotter#upgrade-from-v1alpha1-to-v1beta1){: external} to make sure that your snapshot CRDs are at the correct `v1beta1` version. The steps to downgrade from version `v1` to `v1beta1` are the same as those to upgrade from `v1alpha1`. Do not follow the instructions to upgrade from version `v1beta1` to version `v1`. |
| VPC clusters: App URL character length | DNS resolution is managed by the cluster's [virtual private endpoint (VPE)](/docs/openshift?topic=openshift-vpc-subnets#vpc_basics_vpe), which can resolve URLs up to 130 characters. If you expose apps in your cluster with URLs, such as the Ingress subdomain or {{site.data.keyword.openshiftshort}} routes, ensure that the URLs are 130 characters or fewer. For example, if you use an auto-generated route name in the format `<service_name>-<project>.<cluster_name>-<random_hash>-0000.<region>.containers.appdomain.cloud` that exceeds 130 characters, you might need to [create a route that uses a shorter, custom subdomain](/docs/openshift?topic=openshift-openshift_routes#routes-setup) instead. |
| **Unsupported:** Deprecated and removed {{site.data.keyword.openshiftshort}} features | For more information, review the [OpenShift version 4.6 deprecated and removed features](https://docs.openshift.com/container-platform/4.6/release_notes/ocp-4-6-release-notes.html#ocp-4-6-deprecated-removed-features){: external}. |
{: caption="Changes to make before you update the master to {{site.data.keyword.openshiftshort}} 4.6" caption-side="top"}
{: summary="The rows are read from left to right. The type of update action is in the first column, and a description of the update action type is in the second column."}

## Archive
{: #version-archive}

Review unsupported versions of {{site.data.keyword.openshiftlong_notm}}.
{: shortdesc}

### {{site.data.keyword.openshiftshort}} 4.5 (Unsupported)
{: #ocp45}

As of 10 October 2021, {{site.data.keyword.openshiftlong_notm}} clusters that run [version 4.5](/docs/openshift?topic=openshift-changelog_archive) are unsupported.
{: shortdesc}

Unsupported clusters are not provided with security and patch updates and are not supported by {{site.data.keyword.cloud_notm}} Support. Although your cluster and apps might continue to run for a time, you can no longer create, reload, or take other corrective actions on your cluster master or worker nodes when an issue occurs. You can still delete the cluster or worker nodes, or update the cluster to the next version. Review the potential impacts and immediately [update the cluster](/docs/containers?topic=containers-update#update) to continue receiving important security updates and support.

### {{site.data.keyword.openshiftshort}} 4.4 (Unsupported)
{: #ocp44}

As of 31 May 2021, {{site.data.keyword.openshiftlong_notm}} clusters that run [version 4.4](/docs/openshift?topic=openshift-changelog_archive) are unsupported.
{: shortdesc}

Unsupported clusters are not provided with security and patch updates and are not supported by {{site.data.keyword.cloud_notm}} Support. Although your cluster and apps might continue to run for a time, you can no longer create, reload, or take other corrective actions on your cluster master or worker nodes when an issue occurs. You can still delete the cluster or worker nodes. To continue running your apps in {{site.data.keyword.openshiftlong_notm}}, [make a new cluster](/docs/containers?topic=containers-clusters#clusters) and [deploy your apps](/docs/containers?topic=containers-app#app) to the new cluster.

### {{site.data.keyword.openshiftshort}} 4.3 (Unsupported)
{: #ocp43}

As of 7 March 2021, {{site.data.keyword.openshiftlong_notm}} clusters that run [version 4.3](/docs/openshift?topic=openshift-changelog_archive) are unsupported.
{: shortdesc}

Unsupported clusters are not provided with security and patch updates and are not supported by {{site.data.keyword.cloud_notm}} Support. Although your cluster and apps might continue to run for a time, you can no longer create, reload, or take other corrective actions on your cluster master or worker nodes when an issue occurs. You can still delete the cluster or worker nodes. To continue running your apps in {{site.data.keyword.openshiftlong_notm}}, [make a new cluster](/docs/containers?topic=containers-clusters#clusters) and [deploy your apps](/docs/containers?topic=containers-app#app) to the new cluster.






