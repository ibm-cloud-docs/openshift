---

copyright:
  years: 2014, 2021
lastupdated: "2021-08-10"

keywords: openshift, roks, rhoks, rhos, version, rhel, update, upgrade

subcollection: openshift

---

{:DomainName: data-hd-keyref="APPDomain"}
{:DomainName: data-hd-keyref="DomainName"}
{:android: data-hd-operatingsystem="android"}
{:api: .ph data-hd-interface='api'}
{:apikey: data-credential-placeholder='apikey'}
{:app_key: data-hd-keyref="app_key"}
{:app_name: data-hd-keyref="app_name"}
{:app_secret: data-hd-keyref="app_secret"}
{:app_url: data-hd-keyref="app_url"}
{:audio: .audio}
{:authenticated-content: .authenticated-content}
{:beta: .beta}
{:c#: .ph data-hd-programlang='c#'}
{:c#: data-hd-programlang="c#"}
{:cli: .ph data-hd-interface='cli'}
{:codeblock: .codeblock}
{:curl: #curl .ph data-hd-programlang='curl'}
{:curl: .ph data-hd-programlang='curl'}
{:deprecated: .deprecated}
{:dotnet-standard: .ph data-hd-programlang='dotnet-standard'}
{:download: .download}
{:external: .external target="_blank"}
{:external: target="_blank" .external}
{:faq: data-hd-content-type='faq'}
{:fuzzybunny: .ph data-hd-programlang='fuzzybunny'}
{:generic: data-hd-operatingsystem="generic"}
{:generic: data-hd-programlang="generic"}
{:gif: data-image-type='gif'}
{:go: .ph data-hd-programlang='go'}
{:help: data-hd-content-type='help'}
{:hide-dashboard: .hide-dashboard}
{:hide-in-docs: .hide-in-docs}
{:important: .important}
{:ios: data-hd-operatingsystem="ios"}
{:java: #java .ph data-hd-programlang='java'}
{:java: .ph data-hd-programlang='java'}
{:java: data-hd-programlang="java"}
{:javascript: .ph data-hd-programlang='javascript'}
{:javascript: data-hd-programlang="javascript"}
{:middle: .ph data-hd-position='middle'}
{:navgroup: .navgroup}
{:new_window: target="_blank"}
{:node: .ph data-hd-programlang='node'}
{:note: .note}
{:objectc: .ph data-hd-programlang='Objective C'}
{:objectc: data-hd-programlang="objectc"}
{:org_name: data-hd-keyref="org_name"}
{:php: .ph data-hd-programlang='PHP'}
{:php: data-hd-programlang="php"}
{:pre: .pre}
{:preview: .preview}
{:python: .ph data-hd-programlang='python'}
{:python: data-hd-programlang="python"}
{:right: .ph data-hd-position='right'}
{:route: data-hd-keyref="route"}
{:row-headers: .row-headers}
{:ruby: .ph data-hd-programlang='ruby'}
{:ruby: data-hd-programlang="ruby"}
{:runtime: architecture="runtime"}
{:runtimeIcon: .runtimeIcon}
{:runtimeIconList: .runtimeIconList}
{:runtimeLink: .runtimeLink}
{:runtimeTitle: .runtimeTitle}
{:screen: .screen}
{:script: data-hd-video='script'}
{:service: architecture="service"}
{:service_instance_name: data-hd-keyref="service_instance_name"}
{:service_name: data-hd-keyref="service_name"}
{:shortdesc: .shortdesc}
{:space_name: data-hd-keyref="space_name"}
{:step: data-tutorial-type='step'}
{:step: data-tutorial-type='step'} 
{:subsection: outputclass="subsection"}
{:support: data-reuse='support'}
{:swift: #swift .ph data-hd-programlang='swift'}
{:swift: .ph data-hd-programlang='swift'}
{:swift: data-hd-programlang="swift"}
{:table: .aria-labeledby="caption"}
{:term: .term}
{:terraform: .ph data-hd-interface='terraform'}
{:tip: .tip}
{:tooling-url: data-tooling-url-placeholder='tooling-url'}
{:topicgroup: .topicgroup}
{:troubleshoot: data-hd-content-type='troubleshoot'}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:tsSymptoms: .tsSymptoms}
{:tutorial: data-hd-content-type='tutorial'}
{:ui: .ph data-hd-interface='ui'}
{:unity: .ph data-hd-programlang='unity'}
{:url: data-credential-placeholder='url'}
{:user_ID: data-hd-keyref="user_ID"}
{:vbnet: .ph data-hd-programlang='vb.net'}
{:video: .video}


# Version information and update actions
{: #openshift_versions}

Review information about the supported {{site.data.keyword.openshiftshort}} versions for {{site.data.keyword.openshiftlong}} clusters.
{: shortdesc}

For more information about the {{site.data.keyword.openshiftshort}} and Kubernetes project versions, review the following information.
* [{{site.data.keyword.openshiftshort}} 4.7 release notes overview](https://docs.openshift.com/container-platform/4.7/release_notes/ocp-4-7-release-notes.html){: external}
* [{{site.data.keyword.openshiftshort}} 4.6 release notes overview](https://docs.openshift.com/container-platform/4.6/release_notes/ocp-4-6-release-notes.html){: external}
* Deprecated: [{{site.data.keyword.openshiftshort}} 4.5 release notes overview](https://docs.openshift.com/container-platform/4.5/release_notes/ocp-4-5-release-notes.html){: external}
* Deprecated: [{{site.data.keyword.openshiftshort}} 3.11 release notes overview](https://docs.openshift.com/container-platform/3.11/release_notes/index.html){: external}
* [Kubernetes changelog](https://github.com/kubernetes/kubernetes/tree/master/CHANGELOG){: external}

## Update types
{: #openshift_update_types}

Your {{site.data.keyword.openshiftlong_notm}} cluster has three types of updates: major, minor, and patch. As updates become available, you are notified when you view information about the cluster master or worker nodes, such as with the `ibmcloud oc cluster ls`, `cluster get`, `worker ls`, or `worker get` commands.
{: shortdesc}

You must [update your cluster](/docs/openshift?topic=openshift-update) by using the {{site.data.keyword.openshiftlong_notm}} API, CLI, or console tools. You cannot update your cluster version from OpenShift Container Platform tools such as the {{site.data.keyword.openshiftshort}} web console.
{: note}

|Update type|Examples of version labels|Updated by|Impact
|-----|-----|-----|-----|
|Major|4.x.x|You|Operation changes for clusters, including scripts or deployments.|
|Minor|x.6.x|You|Operation changes for clusters, including scripts or deployments.|
|Patch|x.x.18_1533|IBM and you|{{site.data.keyword.openshiftshort}} patches, as well as other {{site.data.keyword.cloud_notm}} Provider component updates such as security and operating system patches. IBM updates masters automatically, but you apply patches to worker nodes. See more about patches in the following section.|
{: caption="Impacts of {{site.data.keyword.openshiftshort}} updates" caption-side="top"}

### Major and minor updates (4.6)
{: #major_minor_updates}

First, [update your master node](/docs/openshift?topic=openshift-update#master) and then [update the worker nodes](/docs/openshift?topic=openshift-update#worker_node). Worker nodes cannot run an {{site.data.keyword.openshiftshort}} major or minor version that is greater than the masters. Additionally, your worker nodes can be only one version behind the master version (`n-1`).
{: shortdesc}

If you use an `oc` or `oc` CLI version that does match at least the `major.minor` version of your clusters, you might experience unexpected results. Make sure to keep your cluster and [CLI versions](/docs/openshift?topic=openshift-openshift-cli#cli_oc) up-to-date.
{: note}


### Patch updates (4.6.28_xxxx_openshift)
{: #patch_updates_oc}

Changes across patches are documented in the [Version changelog](/docs/openshift?topic=openshift-openshift_versions). Master patches are applied automatically, but you initiate worker node patches updates.
{: shortdesc}

Worker nodes can also run patch versions that are greater than the masters. As updates become available, you are notified when you view information about the master and worker nodes in the {{site.data.keyword.cloud_notm}} console or CLI, such as with the following commands: `ibmcloud oc cluster ls`, `cluster get`, `worker ls`, or `worker get`. Patches can be for worker nodes, masters, or both.

**Worker node patches**: Check monthly to see whether an update is available, and use the `ibmcloud oc worker update` [command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_update) or the `ibmcloud oc worker reload` [command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_reload) to apply these security and operating system patches. During an update or reload, your worker node machine is reimaged, and data is deleted if not [stored outside the worker node](/docs/openshift?topic=openshift-storage_planning#persistent_storage_overview).

**Master patches**: Master patches are applied automatically over the course of several days, so a master patch version might show up as available before it is applied to your master. The update automation also skips clusters that are in an unhealthy state or have operations currently in progress. Occasionally, IBM might disable automatic updates for a specific master fix pack, as noted in the changelog, such as a patch that is only needed if a master is updated from one minor version to another. In any of these cases, you can choose to safely use the `ibmcloud oc cluster master update` [command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_cluster_update) yourself without waiting for the update automation to apply. When a master patch update is initiated for a cluster, the `containers-kubernetes.version.update` event is [sent to {{site.data.keyword.at_short}}](/docs/openshift?topic=openshift-at_events).




<br />

## {{site.data.keyword.openshiftshort}} versions
{: #version_types}

{{site.data.keyword.openshiftlong_notm}} supports the following versions of {{site.data.keyword.openshiftshort}}. The worker node operating system is Red Hat Enterprise Linux 7.

**Supported versions**:
* Latest: 4.7 (Kubernetes 1.20)
* Default: 4.6 (Kubernetes 1.19)

**Deprecated and unsupported versions**:
* Deprecated: 3.11 (Kubernetes 1.11), 4.5 (Kubernetes 1.18)
* Unsupported: 4.3 (Kubernetes 1.16), 4.4 (Kubernetes 1.17)

To check the Kubernetes server version of a cluster, log in to the cluster and run the following command.

```
oc version
```
{: pre}

Example output:
```
Client Version: 4.6.3
Server Version: 4.6.12
Kubernetes Version: v1.19.2
```
{: screen}

## Release history
{: #openshift_release_history}

The following table records {{site.data.keyword.openshiftlong_notm}} version release history. You can use this information for planning purposes, such as to estimate general time frames when a certain release might become unsupported.
{: shortdesc}

**How soon after an OCP release is the version available in {{site.data.keyword.cloud_notm}}?**

After the Red Hat OpenShift Container Platform community releases a version update, the IBM team begins a process of hardening and testing the release for {{site.data.keyword.openshiftlong_notm}} environments. Availability and unsupported release dates depend on the results of these tests, community updates, security patches, and technology changes between versions. Plan to keep your cluster master and worker node version up-to-date.

**Why is the deprecated version 3.11 supported longer than more recent versions like 4.3?**

In general, the last minor version of a major version is supported longer than other minor versions. Because you cannot update a cluster from one major version to another (such as version 3 to 4), this longer support period gives you time to create clusters at a more recent version. Minor versions of a more recent major version might become unsupported before the last minor version of a deprecated major version because the more recent major version has subsequent minor releases that are supported. For example, version 4.3 becomes unsupported before the deprecated version 3.11 because version 4 has future minor releases, but 3.11 is the last minor version of version 3.

**What is different for deprecated versions?**

Your apps still run, and you can log in to the cluster to manage your {{site.data.keyword.openshiftshort}} resources. You can still manage your cluster lifecycle, such as by adding and reloading worker nodes. However, security patch updates might not be provided. To continue receiving important security updates and the latest functionality, create a cluster at a supported version. You receive a notification in the console and CLI to update your cluster to a supported version about 45 days before the deprecated version becomes unsupported.

Dates that are marked with a dagger (`†`) are tentative and subject to change.
{: important}

| Supported? | {{site.data.keyword.openshiftshort}} | Kubernetes version | {{site.data.keyword.openshiftlong_notm}} release date | {{site.data.keyword.openshiftlong_notm}} unsupported date |
| --- | --- | --- | --- |
| Supported | 4.7 / 1.20 | 09 Jun 2021 | Jun 2022`†` |
| Supported | 4.6 / 1.19 | 17 Feb 2021 | Apr 2022 `†` |
| Supported | 4.5 / 1.18 | 13 Oct 2020 | 30 Sep 2021 `†` |
| Not supported | 4.4 / 1.17 | 21 Jul 2020 | 31 May 2021 |
| Not supported | 4.3 / 1.16 | 20 Apr 2020 | 7 Mar 2021 |
| Deprecated | 3.11 / 1.11 | 01 Aug 2019 | 06 Jun 2022 `†` |
{: caption="Release history for {{site.data.keyword.openshiftlong_notm}}." caption-side="top"}
{: summary="The rows are read from left to right. The first column is the supported status, the second column is OpenShift and Kubernetes version number. The third column is the release date. The fourth column is the unsupported date."}



## {{site.data.keyword.openshiftshort}} 4.7
{: #ocp47}

<img src="images/certified_kubernetes_1x20.png" style="padding-right: 10px;" align="left" alt="This badge indicates Kubernetes version 1.20 certification for {{site.data.keyword.openshiftlong_notm}}."/> {{site.data.keyword.openshiftlong_notm}} is a Certified Kubernetes product for version 1.20 under the CNCF Kubernetes Software Conformance Certification program. _Kubernetes® is a registered trademark of The Linux Foundation in the United States and other countries, and is used pursuant to a license from The Linux Foundation._

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

<br />

## {{site.data.keyword.openshiftshort}} 4.6
{: #ocp46}

<img src="images/certified_kubernetes_1x19.png" style="padding-right: 10px;" align="left" alt="This badge indicates Kubernetes version 1.19 certification for {{site.data.keyword.openshiftlong_notm}}."/> {{site.data.keyword.openshiftlong_notm}} is a Certified Kubernetes product for version 1.19 under the CNCF Kubernetes Software Conformance Certification program. _Kubernetes® is a registered trademark of The Linux Foundation in the United States and other countries, and is used pursuant to a license from The Linux Foundation._

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

<br />

## Deprecated: {{site.data.keyword.openshiftshort}} 4.5
{: #ocp45}

<img src="images/certified_kubernetes_1x18.png" style="padding-right: 10px;" align="left" alt="This badge indicates Kubernetes version 1.18 certification for {{site.data.keyword.openshiftlong_notm}}."/> {{site.data.keyword.openshiftlong_notm}} is a Certified Kubernetes product for version 1.18 under the CNCF Kubernetes Software Conformance Certification program. _Kubernetes® is a registered trademark of The Linux Foundation in the United States and other countries, and is used pursuant to a license from The Linux Foundation._

Review changes that you might need to make when you [update a cluster](/docs/openshift?topic=openshift-update) that runs {{site.data.keyword.openshiftshort}} 4.4 to {{site.data.keyword.openshiftshort}} 4.5.
{: shortdesc}

{{site.data.keyword.openshiftshort}} version 4.5 is deprecated, with a tentative unsupported date of 1 September 2021. Update your cluster to at least [version 4.6](#ocp46) as soon as possible.
{: deprecated}

You cannot update a cluster that runs 3.11 to a version 4 cluster. [Create a cluster](/docs/openshift?topic=openshift-clusters) and [copy your deployments](/docs/openshift?topic=openshift-update_app#copy_apps_cluster) from the outdated cluster to the new cluster.
{: important}

### Update before master
{: #45_before}

The following table shows the actions that you must take before you [update the cluster master](/docs/openshift?topic=openshift-update#master).
{: shortdesc}

| Type | Description |
| ---- | ----------- |
| {{site.data.keyword.openshiftshort}} update requirements | {{site.data.keyword.openshiftlong_notm}} cluster master updates require worker nodes to be at most 1 minor version behind the cluster master version (`n-1`). Additionally, for cluster master updates to version 4.5, all worker nodes in the cluster must run at least version `4.4.23`. Ensure your workers nodes are running the latest patch version before updating your cluster master. |
| **Unsupported:** Deprecated and removed {{site.data.keyword.openshiftshort}} features | For more information, review the [OpenShift version 4.5 deprecated and removed features](https://docs.openshift.com/container-platform/4.5/release_notes/ocp-4-5-release-notes.html#ocp-4-5-deprecated-removed-features){: external}. |
{: caption="Changes to make before you update the master to {{site.data.keyword.openshiftshort}} 4.5" caption-side="top"}
{: summary="The rows are read from left to right. The type of update action is in the first column, and a description of the update action type is in the second column."}

### Update after master
{: #45_after}

The following table shows the actions that you must take after you [update the cluster master](/docs/openshift?topic=openshift-update#master).
{: shortdesc}

| Type | Description |
| ---- | ----------- |
| Elasticsearch version upgrade for cluster logging | For more information, see the Elasticsearch version upgrade notes in the [{{site.data.keyword.openshiftshort}} release notes](https://docs.openshift.com/container-platform/4.5/release_notes/ocp-4-5-release-notes.html#ocp-4-5-elasticsearch-6){: external}. |
| Image registry configuration | New version 4.5 clusters that run on the VPC infrastructure provider and use {{site.data.keyword.cos_full_notm}} now proxy container image traffic through the internal registry pods directly to the {{site.data.keyword.cos_short}} endpoints. To configure this proxying for version 4.5 clusters that were updated from a previous version, see [the troubleshooting topic](/docs/openshift?topic=openshift-ts-app-ocr-vpc-push). |
| **Unsupported**: `kubelet` statistics | The `kubelet` statistics that were available via the `/stats` endpoint are unsupported and removed. The cluster insights panel in the cluster console no longer reports statistics from this endpoint. |
| Temporary `oc` and `kubectl` latency | RBAC operations are now performed asynchronously. After you run `ibmcloud oc cluster config` for the first time after the update, `oc` and `kubectl` commands might fail for a few seconds while RBAC synchronizes for the first time. Afterward, `oc` and `kubectl` commands perform as expected. If you use automation to access the cluster with `oc` and `kubectl` commands, add retry logic for `oc` and `kubectl` commands after a `kubeconfig` file is successfully retrieved. |
| `oc adm policy` | The `oc adm policy` commands now manage role-based access control (RBAC) resources rather than modifying security context constraints (SCCs) directly for managing permissions within the cluster. Update any components that rely on direct changes to SCCs to use RBAC to manage permissions. |
| `oc new-app` | For more information, see the `oc new-app` deployment resources notes in the [{{site.data.keyword.openshiftshort}} release notes](https://docs.openshift.com/container-platform/4.5/release_notes/ocp-4-5-release-notes.html#ocp-4-5-oc-new-app-deployment-resources){: external}. |
{: caption="Changes to make after you update the master to {{site.data.keyword.openshiftshort}} 4.5" caption-side="top"}
{: summary="The rows are read from left to right. The type of update action is in the first column, and a description of the update action type is in the second column."}

<br />

## Archive
{: #version-archive}

Review unsupported versions of {{site.data.keyword.openshiftlong_notm}}.
{: shortdesc}

### {{site.data.keyword.openshiftshort}} 4.4 (Unsupported)
{: #ocp44}

As of 31 May 2021, {{site.data.keyword.openshiftlong_notm}} clusters that run [version 4.4](/docs/openshift?topic=openshift-changelog_archive) are unsupported.
{: shortdesc}

Unsupported clusters are not provided with security and patch updates and are not supported by {{site.data.keyword.cloud_notm}} Support. Although your cluster and apps might continue to run for a time, you can no longer create, reload, or take other corrective actions on your cluster master or worker nodes when an issue occurs. You can still delete the cluster or worker nodes, or update the cluster to the next version. Review the potential impacts and immediately [update the cluster](/docs/containers?topic=containers-update#update) to continue receiving important security updates and support.

### {{site.data.keyword.openshiftshort}} 4.3 (Unsupported)
{: #ocp43}

As of 7 March 2021, {{site.data.keyword.openshiftlong_notm}} clusters that run [version 4.3](/docs/openshift?topic=openshift-changelog_archive) are unsupported.
{: shortdesc}

Unsupported clusters are not provided with security and patch updates and are not supported by {{site.data.keyword.cloud_notm}} Support. Although your cluster and apps might continue to run for a time, you can no longer create, reload, or take other corrective actions on your cluster master or worker nodes when an issue occurs. You can still delete the cluster or worker nodes. To continue running your apps in {{site.data.keyword.openshiftlong_notm}}, [make a new cluster](/docs/containers?topic=containers-clusters#clusters) and [deploy your apps](/docs/containers?topic=containers-app#app) to the new cluster.
