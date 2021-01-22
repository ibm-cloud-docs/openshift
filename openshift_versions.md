---

copyright:
  years: 2014, 2021
lastupdated: "2021-01-22"

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
{:authenticated-content: .authenticated-content}
{:beta: .beta}
{:c#: data-hd-programlang="c#"}
{:cli: .ph data-hd-interface='cli'}
{:codeblock: .codeblock}
{:curl: .ph data-hd-programlang='curl'}
{:deprecated: .deprecated}
{:dotnet-standard: .ph data-hd-programlang='dotnet-standard'}
{:download: .download}
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
{:java: .ph data-hd-programlang='java'}
{:java: data-hd-programlang="java"}
{:javascript: .ph data-hd-programlang='javascript'}
{:javascript: data-hd-programlang="javascript"}
{:new_window: target="_blank"}
{:note .note}
{:note: .note}
{:objectc data-hd-programlang="objectc"}
{:org_name: data-hd-keyref="org_name"}
{:php: data-hd-programlang="php"}
{:pre: .pre}
{:preview: .preview}
{:python: .ph data-hd-programlang='python'}
{:python: data-hd-programlang="python"}
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
{:subsection: outputclass="subsection"}
{:support: data-reuse='support'}
{:swift: .ph data-hd-programlang='swift'}
{:swift: data-hd-programlang="swift"}
{:table: .aria-labeledby="caption"}
{:term: .term}
{:tip: .tip}
{:tooling-url: data-tooling-url-placeholder='tooling-url'}
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
* [{{site.data.keyword.openshiftshort}} 4.5 release notes overview](https://docs.openshift.com/container-platform/4.5/release_notes/ocp-4-5-release-notes.html){: external}
* [{{site.data.keyword.openshiftshort}} 4.4 release notes overview](https://docs.openshift.com/container-platform/4.4/release_notes/ocp-4-4-release-notes.html){: external}
* Deprecated: [{{site.data.keyword.openshiftshort}} 4.3 release notes overview](https://docs.openshift.com/container-platform/4.3/release_notes/ocp-4-3-release-notes.html){: external}
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
|Major|3.x.x|You|Operation changes for clusters, including scripts or deployments.|
|Minor|x.11.x|You|Operation changes for clusters, including scripts or deployments.|
|Patch|x.x.104_1507|IBM and you|{{site.data.keyword.openshiftshort}} patches, as well as other {{site.data.keyword.cloud_notm}} Provider component updates such as security and operating system patches. IBM updates masters automatically, but you apply patches to worker nodes. See more about patches in the following section.|
{: caption="Impacts of {{site.data.keyword.openshiftshort}} updates" caption-side="top"}

<dl>
  <dt>**Major and minor updates (4.5)**</dt>
  <dd><p>First, [update your master node](/docs/openshift?topic=openshift-update#master) and then [update the worker nodes](/docs/openshift?topic=openshift-update#worker_node). Worker nodes cannot run an {{site.data.keyword.openshiftshort}} major or minor version that is greater than the masters. Additionally, your worker nodes can be only one version behind the master version (`n-1`).</p><p class="note">If you use an `oc` or `oc` CLI version that does match at least the `major.minor` version of your clusters, you might experience unexpected results. Make sure to keep your cluster and [CLI versions](/docs/openshift?topic=openshift-openshift-cli#cli_oc) up-to-date.</p></dd>
  <dt>**Patch updates (4.5.24_xxxx_openshift)**</dt>
  <dd><p>Changes across patches are documented in the [Version changelog](/docs/openshift?topic=openshift-openshift_versions). Master patches are applied automatically, but you initiate worker node patches updates. Worker nodes can also run patch versions that are greater than the masters. As updates become available, you are notified when you view information about the master and worker nodes in the {{site.data.keyword.cloud_notm}} console or CLI, such as with the following commands: `ibmcloud oc cluster ls`, `cluster get`, `worker ls`, or `worker get`.</p>
  <p>Patches can be for worker nodes, masters, or both.</p>
  <ul><li>**Worker node patches**: Check monthly to see whether an update is available, and use the `ibmcloud oc worker update` [command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_update) or the `ibmcloud oc worker reload` [command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_reload) to apply these security and operating system patches. During an update or reload, your worker node machine is reimaged, and data is deleted if not [stored outside the worker node](/docs/openshift?topic=openshift-storage_planning#persistent_storage_overview).</li>
  <li>**Master patches**: Master patches are applied automatically over the course of several days, so a master patch version might show up as available before it is applied to your master. The update automation also skips clusters that are in an unhealthy state or have operations currently in progress. Occasionally, IBM might disable automatic updates for a specific master fix pack, as noted in the changelog, such as a patch that is only needed if a master is updated from one minor version to another. In any of these cases, you can choose to safely use the `ibmcloud oc cluster master update` [command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_cluster_update) yourself without waiting for the update automation to apply.</li></ul></dd>
</dl>

<br />

## {{site.data.keyword.openshiftshort}} versions
{: #version_types}

{{site.data.keyword.openshiftlong_notm}} supports the following versions of {{site.data.keyword.openshiftshort}}. The worker node operating system is Red Hat Enterprise Linux 7.

* **Latest and default**: 4.5 (Kubernetes 1.18)
* **Other**: 4.4 (Kubernetes 1.17)
* **Deprecated**: 3.11 (Kubernetes 1.11), 4.3 (Kubernetes 1.16)

To check the Kubernetes server version of a cluster, log in to the cluster and run the following command.

```
oc version
```
{: pre}

Example output:
```
Client Version: 4.5.3
Server Version: 4.5.12
Kubernetes Version: v1.18.2
```
{: screen}

## Release history
{: #openshift_release_history}

The following table records {{site.data.keyword.openshiftlong_notm}} version release history. You can use this information for planning purposes, such as to estimate general time frames when a certain release might become unsupported.
{: shortdesc}

**How soon after an OCP release is the version available in {{site.data.keyword.cloud_notm}}?**<br>
After the Red Hat OpenShift Container Platform community releases a version update, the IBM team begins a process of hardening and testing the release for {{site.data.keyword.openshiftlong_notm}} environments. Availability and unsupported release dates depend on the results of these tests, community updates, security patches, and technology changes between versions. Plan to keep your cluster master and worker node version up-to-date.

**Why is the deprecated version 3.11 supported longer than more recent versions like 4.3?**<br>
In general, the last minor version of a major version is supported longer than other minor versions. Because you cannot update a cluster from one major version to another (such as version 3 to 4), this longer support period gives you time to create clusters at a more recent version. Minor versions of a more recent major version might become unsupported before the last minor version of a deprecated major version because the more recent major version has subsequent minor releases that are supported. For example, version 4.3 becomes unsupported before the deprecated version 3.11 because version 4 has future minor releases, but 3.11 is the last minor version of version 3.

**What is different for deprecated versions?**<br>
Your apps still run, and you can log in to the cluster to manage your {{site.data.keyword.openshiftshort}} resources. You can still manage your cluster lifecycle, such as by adding and reloading worker nodes. However, security patch updates might not be provided. To continue receiving important security updates and the latest functionality, create a cluster at a supported version. You receive a notification in the console and CLI to update your cluster to a supported version about 45 days before the deprecated version becomes unsupported.

Dates that are marked with a dagger (`†`) are tentative and subject to change.
{: important}

<table summary="This table shows the release history for {{site.data.keyword.openshiftlong_notm}}.">
<caption>Release history for {{site.data.keyword.openshiftlong_notm}}.</caption>
<col width="20%" align="center">
<col width="20%">
<col width="30%">
<col width="30%">
<thead>
<tr>
<th>Supported?</th>
<th>{{site.data.keyword.openshiftshort}} / Kubernetes version</th>
<th>{{site.data.keyword.openshiftlong_notm}}<br>release date</th>
<th>{{site.data.keyword.openshiftlong_notm}}<br>unsupported date</th>
</tr>
</thead>
<tbody>
<tr>
  <td><img src="images/checkmark-filled.png" align="left" width="32" style="width:32px;" alt="This version is supported."/></td>
  <td>4.5 / 1.18</td>
  <td>13 Oct 2020</td>
  <td>August 2021 `†`</td>
</tr>
<tr>
  <td><img src="images/checkmark-filled.png" align="left" width="32" style="width:32px;" alt="This version is supported."/></td>
  <td>4.4 / 1.17</td>
  <td>21 Jul 2020</td>
  <td>May 2021 `†`</td>
</tr>
<tr>
  <td><img src="images/warning-filled.png" align="left" width="32" style="width:32px;" alt="This version is deprecated."/></td>
  <td>4.3 / 1.16</td>
  <td>20 Apr 2020</td>
  <td>7 Mar 2021 `†`</td>
</tr>
<tr>
  <td><img src="images/warning-filled.png" align="left" width="32" style="width:32px;" alt="This version is deprecated."/></td>
  <td>3.11 / 1.11</td>
  <td>01 Aug 2019</td>
  <td>June 2022 `†`</td>
</tr>
</tbody>
</table>

<br />

## {{site.data.keyword.openshiftshort}} 4.5
{: #ocp45}

<img src="images/certified_kubernetes_1x18.png" style="padding-right: 10px;" align="left" alt="This badge indicates Kubernetes version 1.18 certification for {{site.data.keyword.openshiftlong_notm}}."/> {{site.data.keyword.openshiftlong_notm}} is a Certified Kubernetes product for version 1.18 under the CNCF Kubernetes Software Conformance Certification program. _Kubernetes® is a registered trademark of The Linux Foundation in the United States and other countries, and is used pursuant to a license from The Linux Foundation._

Review changes that you might need to make when you [update a cluster](/docs/openshift?topic=openshift-update) that runs {{site.data.keyword.openshiftshort}} 4.4 to {{site.data.keyword.openshiftshort}} 4.5.
{: shortdesc}

You cannot update a cluster that runs 3.11 to a version 4 cluster. For more information, see [Migrating from version 3.11 to 4 clusters](#ocp-3-to-4-migration).
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
| Image registry configuration | New version 4.5 clusters that run on the VPC Gen 2 infrastructure provider and use {{site.data.keyword.cos_full_notm}} now proxy container image traffic through the internal registry pods directly to the {{site.data.keyword.cos_short}} endpoints. To configure this proxying for version 4.5 clusters that were updated from a previous version, see [the troubleshooting topic](/docs/openshift?topic=openshift-cs_troubleshoot_app#ts-app-ocr-vpc-push). |
| **Unsupported**: `kubelet` statistics | The `kubelet` statistics that were available via the `/stats` endpoint are unsupported and removed. The cluster insights panel in the cluster console no longer reports statistics from this endpoint. |
| Temporary `oc` and `kubectl` latency | RBAC operations are now performed asynchronously. After you run `ibmcloud oc cluster config` for the first time after the update, `oc` and `kubectl` commands might fail for a few seconds while RBAC synchronizes for the first time. Afterward, `oc` and `kubectl` commands perform as expected. If you use automation to access the cluster with `oc` and `kubectl` commands, add retry logic for `oc` and `kubectl` commands after a `kubeconfig` file is successfully retrieved. |
| `oc adm policy` | The `oc adm policy` commands now manage role-based access control (RBAC) resources rather than modifying security context constraints (SCCs) directly for managing permissions within the cluster. Update any components that rely on direct changes to SCCs to use RBAC to manage permissions. |
| `oc new-app` | For more information, see the `oc new-app` deployment resources notes in the [{{site.data.keyword.openshiftshort}} release notes](https://docs.openshift.com/container-platform/4.5/release_notes/ocp-4-5-release-notes.html#ocp-4-5-oc-new-app-deployment-resources){: external}. |
{: caption="Changes to make after you update the master to {{site.data.keyword.openshiftshort}} 4.5" caption-side="top"}
{: summary="The rows are read from left to right. The type of update action is in the first column, and a description of the update action type is in the second column."}

<br />

## {{site.data.keyword.openshiftshort}} 4.4
{: #ocp44}

<img src="images/certified_kubernetes_1x17.png" style="padding-right: 10px;" align="left" alt="This badge indicates Kubernetes version 1.17 certification for {{site.data.keyword.openshiftlong_notm}}."/> {{site.data.keyword.openshiftlong_notm}} is a Certified Kubernetes product for version 1.17 under the CNCF Kubernetes Software Conformance Certification program. _Kubernetes® is a registered trademark of The Linux Foundation in the United States and other countries, and is used pursuant to a license from The Linux Foundation._

Review changes that you might need to make when you [update a cluster](/docs/openshift?topic=openshift-update) that runs {{site.data.keyword.openshiftshort}} 4.3 to {{site.data.keyword.openshiftshort}} 4.4.
{: shortdesc}

With {{site.data.keyword.openshiftshort}} 4.4, you get access to Kubernetes version 1.17 APIs that enable features such as [key management service (KMS)](/docs/openshift?topic=openshift-encryption#keyprotect) integration. For more information, see the [{{site.data.keyword.cloud_notm}} blog](https://www.ibm.com/cloud/blog/announcements/openshift-version-44-now-available-in-red-hat-openshift-on-ibm-cloud){: external}.

You cannot update a cluster that runs 3.11 to a version 4 cluster. For more information, see [Migrating from version 3.11 to 4 clusters](#ocp-3-to-4-migration).
{: important}

### Update before master
{: #44_before}

The following table shows the actions that you must take before you [update the cluster master](/docs/openshift?topic=openshift-update#master).
{: shortdesc}

| Type | Description |
| ---- | ----------- |
| Add-ons and plug-ins | For each add-on and plug-in that you installed in your cluster, check for any impacts that might be caused by updating the cluster version. For instructions, see [Steps to update the cluster master](/docs/containers?topic=containers-update#master-steps) and refer to the add-on and plug-in documentation. |
| Temporary `oc` and `kubectl` latency | RBAC operations are now performed asynchronously. After you run `ibmcloud oc cluster config` for the first time after the update, `oc` and `kubectl` commands might fail for a few seconds while RBAC synchronizes for the first time. Afterward, `oc` and `kubectl` commands perform as expected. If you use automation to access the cluster with `oc` and `kubectl` commands, add retry logic for `oc` and `kubectl` commands after a `kubeconfig` file is successfully retrieved. |
| **Unsupported:** Deprecated Kubernetes APIs are removed | Although Kubernetes version 1.16 removed several common, deprecated Kubernetes APIs, {{site.data.keyword.openshiftshort}} version 4.3, which is based on Kubernetes version 1.16, kept these APIs enabled. Now, {{site.data.keyword.openshiftshort}} version 4.4, which is based on Kubernetes version 1.17, removes these Kubernetes APIs that were removed in the Kubernetes 1.16 project. You can take the following steps to mitigate impact to your Kubernetes resources. Note that the blog was written specifically for {{site.data.keyword.containerlong_notm}} clusters, but the tips apply to {{site.data.keyword.openshiftlong_notm}}, too.<ol><li>Follow the [blog update tips](https://www.ibm.com/cloud/blog/announcements/kubernetes-version-1-16-removes-deprecated-apis){: external}.</li><li>Update the configuration files for any impacted Kubernetes resources, such as daemon sets, deployments, replica sets, stateful sets, and network policies.</li><li>If you [add services to your cluster by using Helm charts](/docs/openshift?topic=openshift-helm), update to Helm version 2.15.2 or later.</li></ol>|
| **Unsupported:** Deprecated and removed {{site.data.keyword.openshiftshort}} features | For more information, review the [{{site.data.keyword.openshiftshort}} version 4.4 deprecated and removed features](https://docs.openshift.com/container-platform/4.4/release_notes/ocp-4-4-release-notes.html#ocp-4-4-deprecated-removed-features). |
| Kubernetes API server checks client certificates before tokens | For more information, review [`kube-apiserver` checks client certificates before tokens](https://docs.openshift.com/container-platform/4.4/release_notes/ocp-4-4-release-notes.html#ocp-4-4-kube-apiserver-check-certs-before-tokens). |
{: caption="Changes to make before you update the master to {{site.data.keyword.openshiftshort}} 4.4" caption-side="top"}
{: summary="The rows are read from left to right. The type of update action is in the first column, and a description of the update action type is in the second column."}

## Deprecated: {{site.data.keyword.openshiftshort}} 4.3
{: #ocp43}

<img src="images/certified_kubernetes_1x16.png" style="padding-right: 10px;" align="left" alt="This badge indicates Kubernetes version 1.16 certification for {{site.data.keyword.openshiftlong_notm}}."/> {{site.data.keyword.openshiftlong_notm}} is a Certified Kubernetes product for version 1.16 under the CNCF Kubernetes Software Conformance Certification program. _Kubernetes® is a registered trademark of The Linux Foundation in the United States and other countries, and is used pursuant to a license from The Linux Foundation._

{{site.data.keyword.openshiftshort}} version 4.3 is deprecated, and becomes unsupported 7 March 2021 (date subject to change). [Update your clusters](/docs/openshift?topic=openshift-update) to at least {{site.data.keyword.openshiftshort}} version 4.4 as soon as possible.
{: deprecated}

With the release of OpenShift Container Platform 4.3, you get a new experience and capabilities for managing your cluster and its workloads. For more information, see the [{{site.data.keyword.openshiftshort}} blog](https://www.openshift.com/blog/introducing-red-hat-openshift-4-3-to-enhance-kubernetes-security/){: external}.
{: shortdesc}

To create a 4.3 cluster, [try out the tutorial](/docs/openshift?topic=openshift-openshift_tutorial). You cannot update an existing version 3.11 cluster to a 4.3 cluster, but you can [migrate workloads to version 4 clusters](#ocp-3-to-4-migration).

Review the following benefit highlights when you use version 4.3 clusters.
*   Ability to use your own [Operators](/docs/openshift?topic=openshift-operators) or operators that are provided by the OperatorHub to package and deploy services for your cluster.
*   New [{{site.data.keyword.openshiftshort}} web console experience](/docs/openshift?topic=openshift-openshift_tutorial#openshift_oc_console) that reorganizes your cluster resources and workflows into two perspectives for the **Administrator** and **Developer**.
*   Update of the underlying Kubernetes API to 1.16 so that you can use new capabilities such as extensibility for core Kubernetes APIs, an updated `kubectl` experience, cluster lifecycle stability enhancements, support for projects such as `kustomize`, persistent local volumes, and custom resource and operator support.
*   [Ingress controllers are integrated into the Ingress Operator](/docs/openshift?topic=openshift-ingress-about-roks4) so that you can use routers to proxy app requests instead of application load balancers (ALBs).

For more information, check out the [comparison table between supported features of 3.11 and 4](/docs/openshift?topic=openshift-cs_ov#3.11_vs_4.3) or review the [service limitations](/docs/openshift?topic=openshift-openshift_limitations#ocp4_limitations).

<br />

## Migrating from version 3.11 to 4 clusters
{: #ocp-3-to-4-migration}

You cannot update your {{site.data.keyword.openshiftlong_notm}} cluster from version 3.11 to version 4, such as version 4.3. Instead, you can use the [{{site.data.keyword.openshiftshort}} Migration Operator](https://github.com/konveyor/mig-operator){: external} to migrate your workloads from a version 3.11 source cluster to a version 4 destination cluster.
{: shortdesc}

<p class="important">Keep in mind the following limitations to the migration operator.<ul><li>The {{site.data.keyword.openshiftshort}} Migration Operator is a community tool that you choose to use, and is not supported by IBM or Red Hat.</li><li>You must [complete the prerequisites](#ocp3to4-migrate-prereqs) to prepare the resources in your {{site.data.keyword.cloud_notm}} account.</li><li>The instructions are intended for version 1.0.1 of the migration operator and for 3.11 source and 4.3 destination clusters. The instructions might not work with other versions.</li><li>The migration operator console does not work with {{site.data.keyword.openshiftlong_notm}}. Instead, you can use the CLI to apply configuration files.</li><li>The migration operator is scoped to resources within a project or multiple projects. You cannot migrate resources that reside outside a project, such as cluster role bindings.</li><li>You cannot configure cross-origin resource sharing for 3.11 clusters.</li></ul></p>

**How does the migration operator work?**<br>
The migration operator is a set of custom resources that use [Velero](https://velero.io/){: external} and [Restic](https://restic.net/){: external} open source projects to back up your cluster resources in a project to an {{site.data.keyword.cos_full_notm}} service instance. Then, the operator restores the project resources on the destination cluster. For more information, see the [{{site.data.keyword.openshiftshort}} tech topic](https://www.openshift.com/learn/topics/migration){: external} and a [conceptual overview of the architecture](https://github.com/konveyor/mig-operator/blob/master/docs/usage/2.md).

For an architectural overview of the custom resource definitions that are applied in the clusters, see [CRD Architecture](https://github.com/konveyor/mig-operator/blob/master/docs/usage/5.md#51-crd-architecture){: external}.

**Can I try out the migration with a sample app?**<br>
Yes, the open source documentation includes two examples of [MSSQL](https://github.com/konveyor/mig-operator/blob/master/docs/usage/3.md){: external} and [Sock Shop](https://github.com/konveyor/mig-operator/blob/master/docs/usage/4.md){: external} apps. Keep in mind that the migration operator console is not supported in {{site.data.keyword.openshiftlong_notm}}, so you can use the CLI instead.

**If the console does not work, where are instructions to apply the configuration files myself?**<br>
After you complete the [prerequisites](#ocp3to4-migrate-prereqs), you can use the following [steps](#ocp3to4-migrate-source) as an example to configure your source and destination clusters for the migration. Remember that the instructions are intended for version 1.0.1 of the migration operator and for 3.11 source and 4.3 destination clusters. The instructions might not work with other versions, and are not updated in sync with the [open source community project docs](https://github.com/konveyor/mig-operator/tree/master/docs/usage){: external}.

### Prerequisites
{: #ocp3to4-migrate-prereqs}

Before you migrate your workloads from an {{site.data.keyword.openshiftshort}} version 3.11 cluster to a version 4.3 cluster, make sure that you have the following resources.
{: shortdesc}

1.  Identify your source {{site.data.keyword.openshiftlong_notm}} version 3.11 cluster.
2.  [Create](/docs/openshift?topic=openshift-clusters) a destination {{site.data.keyword.openshiftlong_notm}} version 4.3 cluster.

    For multizone clusters, both the source and destination clusters must be in the same zones. Also, to migrate persistent storage from the source cluster, both the source and destination clusters must be in the same zone.
    {: important}

3.  Prepare an [{{site.data.keyword.cos_full_notm}}](https://cloud.ibm.com/objectstorage/){: external} bucket for the migration backup and restore.
    1.  Identify an existing or create an {{site.data.keyword.cos_short}} instance. When you create the instance, make sure to select **Include HMAC Credential**. For more information, see [Preparing your object storage service instance](/docs/openshift?topic=openshift-object_storage#create_cos_service).
    2.  [Create a bucket](/docs/cloud-object-storage?topic=cloud-object-storage-getting-started-cloud-object-storage#gs-create-buckets) in your {{site.data.keyword.cos_short}} instance. Note the bucket's region **Location**, such as `us-south`.
    3.  Get your HMAC authentication credentials. From the {{site.data.keyword.cos_full_notm}} instance in the console, click **Service credentials** and find credentials that include a `cos_hmac_keys` object with `access_key_id` and `secret_access_key` values. If you do not have credentials with HMAC keys, click **New credential**. Create credentials that include HMAC credentials.
    4.  Get your {{site.data.keyword.cos_short}} instance endpoint for the same geography as your cluster is in. From the {{site.data.keyword.cos_full_notm}} instance in the console, click **Endpoints** and then select the location that you want to use. For example, `https://s3.us.cloud-object-storage.appdomain.cloud`.

### Step 1: Deploy the migration operator to the source cluster
{: #ocp3to4-migrate-source}

Deploy the migration operator to the source {{site.data.keyword.openshiftlong_notm}} version 3.11 cluster.
{: shortdesc}

1.  For your version 3.11 cluster: [Access your {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-access_cluster).
2.  Get the **Master URL** endpoint of the cluster. You use this endpoint later to set up the migration controller in the destination cluster.
    ```
    ibmcloud oc cluster get -c <cluster_name_or_ID>
    ```
    {: pre}

    Example output:
    ```
    Master URL: https://c100-e.<region>.containers.cloud.ibm.com:32xxx
    ```
    {: screen}
3.  Check that the app status that you want to migrate is **Running** before you migrate the app. If the status is not healthy, describe the pod for more information to troubleshoot the issue.
    ```
    oc get pods -n <project>
    ```
    {: pre}
4.  Deploy the migration operator to your source cluster. The configuration includes setting up an `openshift-migration` project; creating a custom resource definition for the migration operator; creating a service account, roles, and rolebindings for the resources; and creating the migration operator deployment.
    ```
    oc create -f https://raw.githubusercontent.com/konveyor/mig-operator/master/deploy/non-olm/latest/operator.yml
    ```
    {: pre}
5.  Deploy the migration controller to your source cluster.
    1.  Get the migration controller configuration file from GitHub.
        ```
        curl https://raw.githubusercontent.com/konveyor/mig-operator/master/deploy/non-olm/latest/controller-3.yml > migration-controller3.yaml
        ```
        {: pre}
    2.  Uncomment and replace the `mig_ui_cluster_api_endpoint` value with the cluster master URL that you previously retrieved.
    3.  Apply the configuration file to your cluster.
        ```
        oc apply -f migration-controller3.yaml
        ```
        {: pre}
6.  Verify that the migration operator, Restic, and Velero pods are in a **Running** status. The pods might take a few minutes to provision.
    ```
    oc get pods -n openshift-migration
    ```
    {: pre}
7.  Encode the service account token so that you can use it later in a secret in the destination cluster.
    ```
    oc sa get-token migration-operator -n openshift-migration | base64
    ```
    {: pre}

Now, you are ready to deploy the migration operator on the destination cluster.

### Step 2: Deploy the migration operator to the destination cluster
{: #ocp3to4-migrate-destination}

Deploy the migration operator to the destination {{site.data.keyword.openshiftlong_notm}} version 4.3 cluster.
{: shortdesc}

1.  For your version 4.3 cluster: [Access your {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-access_cluster).
2.  Deploy the migration operator to your destination cluster. The configuration includes setting up an `openshift-migration` project; creating a custom resource definition for the migration operator; creating a service account, roles, and rolebindings for the resources; and creating the migration operator deployment.
    ```
    oc create -f https://raw.githubusercontent.com/konveyor/mig-operator/master/deploy/non-olm/latest/operator.yml
    ```
    {: pre}
3.  Deploy the migration controller to your destination cluster. You must deploy the controller to both clusters due to the limitation of the migration operator console not being supported in {{site.data.keyword.openshiftlong_notm}}.
    1.  Get the migration controller configuration file from GitHub.
        ```
        curl https://raw.githubusercontent.com/konveyor/mig-operator/master/deploy/non-olm/latest/controller-4.yml > migration-controller4.yaml
        ```
        {: pre}
    2.  Change the `migration_ui` value to `false` and save the file.
    3.  Apply the configuration file to your cluster.
        ```
        oc apply -f migration-controller4.yaml
        ```
        {: pre}
4.  Verify that the migration operator, Restic, and Velero pods are in a **Running** status. The pods might take a few minutes to provision.
    ```
    oc get pods -n openshift-migration
    ```
    {: pre}

### Step 3: Configure storage information in the destination cluster
{: #ocp3to4-storage-destination}

Both the version 3.11 source and 4.3 destination clusters have the migration operator installed. Now, you can set up the storage resources that are needed to back up and restore the data from the source cluster to the destination cluster.
{: shortdesc}

1.  Encode the {{site.data.keyword.cos_full_notm}} service credentials that you created in the [prerequisites](#ocp3to4-migrate-prereqs). Replace `<access_key_id>` and `<secret_access_key>` with your HMAC key values.

    Do not use `echo` when you base64 encode the values because `echo` injects an extra line character that causes the authentication to fail.
    {: tip}

    ```
    printf "<access_key_id>" | base64
    ```
    {: pre}

    ```
    printf "<secret_access_key>" | base64
    ```
    {: pre}
2.  Create a configuration file for a secret in your destination cluster that includes the encoded `<access_key_id>` and `<secret_access_key>` values.
    ```
    apiVersion: v1
    kind: Secret
    metadata:
      namespace: openshift-migration
      name: migstorage-creds
    type: Opaque
    data:
      aws-access-key-id: <encoded_access_key_id>
      aws-secret-access-key: <encoded_secret_access_key>
    ```
    {: codeblock}
3.  Create the secret.
    ```
    oc create -f migstorage-creds.yaml
    ```
    {: pre}
4.  Create a configuration file for a migration storage resource that has the information of your {{site.data.keyword.cos_full_notm}} configuration that you retrieved in the [prerequisites](#ocp3to4-migrate-prereqs).

    * **`<cos_bucket_name>`**: Replace with the name of your bucket in the {{site.data.keyword.cos_short}} instance, such as `migrate_bucket`.
    * **`<cos_endpoint>`** (twice): Replace with the public endpoint of your {{site.data.keyword.cos_short}} instance, such as `https://s3.us.cloud-object-storage.appdomain.cloud`.
    * **`<cos_bucket_region>`** (twice): Replace with the region of your {{site.data.keyword.cos_short}} instance that you can find in the endpoint, such as `us`.

    ```
    apiVersion: migration.openshift.io/v1alpha1
    kind: MigStorage
    metadata:
      labels:
        controller-tools.k8s.io: "1.0"
      name: migstorage-sample
      namespace: openshift-migration
    spec:
      backupStorageProvider: aws
      volumeSnapshotProvider: aws
      backupStorageConfig:
        awsBucketName: <cos_bucket_name>
        awsRegion: <cos_bucket_region>
        credsSecretRef:
          namespace: openshift-migration
          name: migstorage-creds
        awsPublicUrl: https://<cos_endpoint>
        awsS3Url: https://<cos_endpoint>
      volumeSnapshotConfig:
        awsRegion: <cos_bucket_region>
        credsSecretRef:
          namespace: openshift-migration
          name: migstorage-creds
    ```
    {: codeblock}
5.  Create the migration storage resource.
    ```
    oc create -f migstorage-sample.yaml
    ```
    {: pre}
6.  Check that the migration controller successfully connected to your {{site.data.keyword.cos_short}} instance. In the `Status.Conditions` section, review the `Message`.
    ```
    oc -n openshift-migration describe migstorage migstorage-sample 
    ```
    {: pre}

    Example of a successful connection:
    ```
    Status:
      Conditions:
        Category:              Required
        Last Transition Time:  2020-01-20T18:49:07Z
        Message:               The storage is ready.
        Status:                True
        Type:                  Ready
    ```
    {: screen}

    Example of unsuccessful connection with a message to help you resolve the issue. For example, the following error is resolved by adding `https://` to the {{site.data.keyword.cos_short}} endpoint.
    ```
    Status:
      Conditions:
        Category:              Critical
        Last Transition Time:  2020-01-20T16:59:05Z
        Message:               The `backupStorageConfig` settings [PublicURL] not valid.
        Reason:                NotSupported
        Status:                True
        Type:                  InvalidBackupStorageSettings
    ```
    {: screen}

### Step 4: Configure the destination cluster with information about the source cluster
{: #ocp3to4-migrate-configure-destination}

To migrate workloads from the version 3.11 source cluster, the version 4.3 destination cluster must have credentials to the source cluster and additional information configured.
{: shortdesc}

1.  Create configuration file for a secret in your destination cluster that includes the encoded credentials to your source cluster that you retrieved in [Step 1](#ocp3to4-migrate-source).
    ```
    apiVersion: v1
    kind: Secret
    metadata:
      name: sa-token-remote
      namespace: openshift-migration
    type: Opaque
    data:
      saToken: <encoded_source_cluster_secret>
    ```
    {: codeblock}
2.  Create the secret.
    ```
    oc create -f sa-secret-source.yaml
    ```
    {: pre}
3.  Create a configuration file for a migration cluster resource that refers to the version 3.11 source cluster's master URL that you retrieved in [Step 1](#ocp3to4-migrate-source).
    ```
    apiVersion: migration.openshift.io/v1alpha1
    kind: MigCluster
    metadata:
      labels:
        controller-tools.k8s.io: "1.0"
      name: migcluster-remote
      namespace: openshift-migration
    spec:
      isHostCluster: false
      url: "<master_url_source_cluster>"
      serviceAccountSecretRef:
        name: sa-token-remote
        namespace: openshift-migration
    ```
    {: codeblock}
4.  Create the source migration cluster resource.
    ```
    oc create -f mig-cluster-source.yaml
    ```
    {: pre}  
5.  Check that the migration cluster resource in your version 4.3 destination cluster successfully connected to your source cluster. In the `Status.Conditions` section, review the `Message`.
    ```
    oc -n openshift-migration describe migcluster migcluster-remote
    ```
    {: pre}

    Example of a successful connection:
    ```
    Status:
      Conditions:
        Category:              Required
        Last Transition Time:  2020-01-20T18:49:07Z
        Message:               The cluster is ready.
        Status:                True
        Type:                  Ready
    ```
    {: screen}

6.  Create another migration cluster resource that identifies this version 4.3 destination cluster as the host cluster for the migration process.
    ```
    cat <<EOF | oc create -f -
    apiVersion: migration.openshift.io/v1alpha1
    kind: MigCluster
    metadata:
      labels:
        controller-tools.k8s.io: "1.0"
      name: migcluster-local
      namespace: openshift-migration
    spec:
      isHostCluster: true
    EOF
    ```
    {: codeblock}
7.  Create a configmap so that the migration process can move images from the source cluster's internal registry to the internal registry of the destination cluster.
    ```
    cat <<EOF | oc create -f -
    apiVersion: v1
    data:
      config.yaml: '{"imagePolicyConfig":{"internalRegistryHostname":"image-registry.openshift-image-registry.svc:5000"}}'
    kind: ConfigMap
    metadata:
      name: config
      namespace: openshift-apiserver
    EOF
    ```
    {: codeblock}

### Step 5: Run the migration
{: #ocp3to4-migrate-run}

To complete the migration process, create a sample plan to verify that what you want to migrate is included. Then, run the migration.
{: shortdesc}

1.  In your version 4.3 destination cluster, create a configuration file for a migration plan resource that identifies the previous migration cluster and storage resources that you created. Replace the `namespaces` values with all the projects that you want to migrate from the source to the destination cluster.
    ```
    apiVersion: migration.openshift.io/v1alpha1
    kind: MigPlan
    metadata:
      labels:
        controller-tools.k8s.io: "1.0"
      name: migplan-sample
      namespace: openshift-migration
    spec:

      srcMigClusterRef:
        name: migcluster-remote
        namespace: openshift-migration

      destMigClusterRef:
        name: migcluster-local
        namespace: openshift-migration

      migStorageRef:
        name: migstorage-sample
        namespace: openshift-migration

      namespaces:
      - <project_in_source_cluster>
      - <project_in_source_cluster>
    ```
    {: codeblock}
2.  Create the migration plan.
    ```
    oc create -f mig-plan.yaml
    ```
    {: pre}
3.  Verify that the resources that you want to migrate are included in the migration plan. Keep in mind that if you migrate persistent storage, your source and destination clusters must be in the zone. In the `Status.Conditions` section, review the `Message` fields.
    ```
    oc -n openshift-migration describe migplan migplan-sample
    ```
    {: pre}

    Example of a successful message.
    ```
    Message:               The migration plan is ready.
    ```
    {: screen}

    Example of an unsuccessful message with troubleshooting information.
    ```
    Message:               Namespaces [migrate-hw] not found on the source cluster.
    ```
    {: screen}
4.  Create the migration that refers to the plan that you previously created.
    ```
    cat <<EOF | oc create -f -
    apiVersion: migration.openshift.io/v1alpha1
    kind: MigMigration
    metadata:
      labels:
        controller-tools.k8s.io: "1.0"
      name: migplan-sample
      namespace: openshift-migration
    spec:
      stage: false
      quiescePods: true
      keepAnnotations: true
      migPlanRef:
        name: migplan-sample
        namespace: openshift-migration
    EOF
    ```
    {: codeblock}

5.  Scale down pods on your version 3.11 source cluster because the migration cannot mount the backup pod storage while the app pods on your cluster run.

    Scaling down your app might cause downtime for your users. To prevent downtime, try creating a project that the migration plan does not include and deploy your app in that project.
    {: important}

    ```
    oc -n <deployment_config_name> scale --replicas=0 dc/<deployment_config_name>
    ```
    {: pre}

    ```
    oc -n <deployment_name> scale --replicas=0 dc/<deployment_name>
    ```
    {: pre}

6.  Check the status of your migration. The migration can take some time to complete.

    Check the status of all pods. If a pod is not in a **Running** status, describe the pod and check the `Events` section for errors.
    ```
    oc -n openshift-migration get pods
    ```
    {: pre}

    Check the logs of the pod to continue troubleshooting any errors.
    ```
    oc -n openshift-migration logs <migration-controller-pod>
    ```
    {: pre}

    In the `Status.Conditions` section, check the `Message` field for any `Errors`.
    ```
    oc -n openshift-migration describe migmigration <your-migration-name>
    ```
    {: pre}

    Do you see an error message similar to `Message: The migration has failed. See: Errors.`? Try [Debugging failed migrations](https://github.com/konveyor/mig-operator/blob/master/docs/usage/5.md){: external}. For example, if you see a `Backup` error, check the Velero pod logs on the source cluster for more troubleshooting information.
    {: tip}

The migration is complete when the version 4.3 destination cluster includes the project and resources that you migrated.
