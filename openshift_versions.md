---

copyright:
  years: 2014, 2019
lastupdated: "2019-07-19"

keywords: openshift, roks, rhoks, rhos, version, rhel

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

# Version information and update actions
{: #openshift_versions}

Red Hat OpenShift on IBM Cloud clusters run at OpenShift version 3.11, which includes the Kubernetes project version 1.11. The worker node operating system is Red Hat Enterprise Linux 7.
{: shortdesc}

For more information about the OpenShift  and Kubernetes project versions, review the following information.
* [OpenShift Release Notes Overview ![External link icon](../icons/launch-glyph.svg "External link icon")](https://docs.openshift.com/container-platform/3.11/release_notes/index.html)
* [Kubernetes changelog ![External link icon](../icons/launch-glyph.svg "External link icon")](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG.md)

## Update types
{: #openshift_update_types}

Your Red Hat OpenShift on IBM Cloud cluster has three types of updates: major, minor, and patch. As updates become available, you are notified when you view information about the worker nodes, such as in the console or in the CLI with the `oc workers --cluster <cluster>` or `oc worker-get --cluster <cluster> --worker <worker>` commands.
{:shortdesc}

|Update type|Examples of version labels|Updated by|Impact
|-----|-----|-----|-----|
|Major|3.x.x|You|Operation changes for clusters, including scripts or deployments.|
|Minor|x.11.x|You|Operation changes for clusters, including scripts or deployments.|
|Patch|x.x.104_1507|IBM and you|OpenShift patches, as well as other {{site.data.keyword.cloud_notm}} Provider component updates such as security and operating system patches. IBM updates masters automatically, but you apply patches to worker nodes. See more about patches in the following section.|
{: caption="Impacts of OpenShift updates" caption-side="top"}

<dl>
  <dt>**Major and minor updates (3.11)**</dt>
  <dd><p>First, [update your master node](/docs/openshift?topic=containers-update#master) and then [update the worker nodes](/docs/openshift?topic=containers-update#worker_node). Worker nodes cannot run an OpenShift major or minor version that is greater than the masters.</p><p class="note">If you use an `oc` or `kubectl` CLI version that does match at least the `major.minor` version of your clusters, you might experience unexpected results. Make sure to keep your cluster and [CLI versions](/docs/openshift?topic=openshift-openshift-cli#cli_oc) up-to-date.</p></dd>
  <dt>**Patch updates (x.x.104_1507)**</dt>
  <dd><p>Master patches are applied automatically, but you initiate worker node patches updates. Worker nodes can also run patch versions that are greater than the masters. As updates become available, you are notified when you view information about the master and worker nodes in the {{site.data.keyword.cloud_notm}} console or CLI, such as with the following commands: `oc clusters`, `cluster-get`, `workers`, or `worker-get`.</p>
  <p>Patches can be for worker nodes, masters, or both.</p>
  <ul><li>**Worker node patches**: Check monthly to see whether an update is available, and use the `oc worker-update` [command](/docs/openshift?topic=containers-cli-plugin-kubernetes-service-cli#cs_worker_update) or the `oc worker-reload` [command](/docs/openshift?topic=containers-cli-plugin-kubernetes-service-cli#cs_worker_reload) to apply these security and operating system patches. During an update or reload, your worker node machine is reimaged, and data is deleted if not [stored outside the worker node](/docs/openshift?topic=containers-storage_planning#persistent_storage_overview).</li>
  <li>**Master patches**: Master patches are applied automatically over the course of several days, so a master patch version might show up as available before it is applied to your master. The update automation also skips clusters that are in an unhealthy state or have operations currently in progress. Occasionally, IBM might disable automatic updates for a specific master fix pack, as noted in the changelog, such as a patch that is only needed if a master is updated from one minor version to another. In any of these cases, you can choose to safely use the `oc cluster-update` [command](/docs/openshift?topic=containers-cli-plugin-kubernetes-service-cli#cs_cluster_update) yourself without waiting for the update automation to apply.</li></ul></dd>
</dl>

<br />


## Release history
{: #openshift_release_history}

The following table records Red Hat OpenShift on IBM Cloud version release history. You can use this information for planning purposes, such as to estimate general time frames when a certain release might become unsupported. After the Red Hat OpenShift community releases a version update, the IBM team begins a process of hardening and testing the release for {{site.data.keyword.containerlong_notm}} environments. Availability and unsupported release dates depend on the results of these tests, community updates, security patches, and technology changes between versions. Plan to keep your cluster master and worker node version up-to-date.
{: shortdesc}

Red Hat OpenShift on IBM Cloud was first generally available with OpenShift version 3.11, which includes the Kubernetes project version 1.11. Dates that are marked with a dagger (`†`) are tentative and subject to change.
{: important}

<table summary="This table shows the release history for Red Hat OpenShift on IBM Cloud.">
<caption>Release history for Red Hat OpenShift on IBM Cloud.</caption>
<col width="20%" align="center">
<col width="20%">
<col width="30%">
<col width="30%">
<thead>
<tr>
<th>Supported?</th>
<th>OpenShift / Kubernetes version</th>
<th>Red Hat OpenShift on IBM Cloud<br>release date</th>
<th>Red Hat OpenShift on IBM Cloud}<br>unsupported date</th>
</tr>
</thead>
<tbody>
<tr>
  <td><img src="images/checkmark-filled.png" align="left" width="32" style="width:32px;" alt="This version is supported."/></td>
  <td>3.11 / 1.11</td>
  <td>01 Aug 2019</td>
  <td>`†`</td>
</tr>
</tbody>
</table>
