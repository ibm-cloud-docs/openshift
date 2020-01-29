---

copyright:
  years: 2017, 2020
lastupdated: "2020-01-29"

keywords: openshift, roks, rhoks, rhos, audit

subcollection: openshift

---

{:codeblock: .codeblock}
{:deprecated: .deprecated}
{:download: .download}
{:external: target="_blank" .external}
{:faq: data-hd-content-type='faq'}
{:gif: data-image-type='gif'}
{:help: data-hd-content-type='help'}
{:important: .important}
{:new_window: target="_blank"}
{:note: .note}
{:pre: .pre}
{:preview: .preview}
{:screen: .screen}
{:shortdesc: .shortdesc}
{:support: data-reuse='support'}
{:table: .aria-labeledby="caption"}
{:tip: .tip}
{:troubleshoot: data-hd-content-type='troubleshoot'}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:tsSymptoms: .tsSymptoms}


# {{site.data.keyword.at_full_notm}} events
{: #at_events}

You can view, manage, and audit user-initiated activities in your {{site.data.keyword.openshiftlong}} community Kubernetes or OpenShift cluster by using the {{site.data.keyword.at_full}} service. 
{: shortdesc}

Red Hat OpenShift on IBM Cloud automatically generates cluster management events and forwards these event logs to {{site.data.keyword.at_full_notm}}. To access these logs, you must [provision an instance of {{site.data.keyword.at_full_notm}}](/docs/Activity-Tracker-with-LogDNA?topic=logdnaat-getting-started).


## Tracking cluster management events
{: #cluster-events}

The following list of the cluster management events are sent to {{site.data.keyword.at_full_notm}}.
{: shortdesc}

<table>
<tr>
<th>Action</th>
<th>Description</th></tr><tr>
<td><code>containers-kubernetes.account-credentials.set</code></td>
<td>Infrastructure credentials in a region for a resource group are set.</td></tr><tr>
<td><code>containers-kubernetes.account-credentials.unset</code></td>
<td>Infrastructure credentials in a region for a resource group are unset.</td></tr><tr>
<td><code>containers-kubernetes.alb.create</code></td>
<td>An Ingress ALB is created.</td></tr><tr>
<td><code>containers-kubernetes.alb.delete</code></td>
<td>An Ingress ALB is deleted.</td></tr><tr>
<td><code>containers-kubernetes.apikey.reset</code></td>
<td>An API key is reset for a region and resource group.</td></tr><tr>
<td><code>containers-kubernetes.cluster.create</code></td>
<td>A cluster is created.</td></tr><tr>
<td><code>containers-kubernetes.cluster.delete</code></td>
<td>A cluster is deleted.</td></tr><tr>
<td><code>containers-kubernetes.cluster-feature.enable</code></td>
<td>A feature, such as the public or private service endpoint, is enabled on a cluster.</td></tr><tr>
<td><code>containers-kubernetes.logging-config.create</code></td>
<td>A log forwarding configuration is created.</td></tr><tr>
<td><code>containers-kubernetes.logging-config.delete</code></td>
<td>A log forwarding configuration is deleted.</td></tr><tr>
<td><code>containers-kubernetes.logging-config.update</code></td>
<td>A log forwarding configuration is updated.</td></tr><tr>
<td><code>containers-kubernetes.logging-config.refresh</code></td>
<td>A log forwarding configuration is refreshed.</td></tr><tr>
<td><code>containers-kubernetes.logging-filter.create</code></td>
<td>A logging filter is created.</td></tr><tr>
<td><code>containers-kubernetes.logging-filter.delete</code></td>
<td>A logging filter is deleted.</td></tr><tr>
<td><code>containers-kubernetes.logging-filter.update</code></td>
<td>A logging filter is updated.</td></tr><tr>
<td><code>containers-kubernetes.logging-autoupdate.changed</code></td>
<td>The logging add-on auto updater is enabled or disabled.</td></tr><tr>
<td><code>containers-kubernetes.mzlb.create</code></td>
<td>A multizone load balancer is created.</td></tr><tr>
<td><code>containers-kubernetes.mzlb.delete</code></td>
<td>A multizone load balancer is deleted.</td></tr><tr>
<td><code>containers-kubernetes.service.bind</code></td>
<td>A service is bound to a cluster.</td></tr><tr>
<td><code>containers-kubernetes.service.unbind</code></td>
<td>A service is unbound from a cluster.</td></tr><tr>
<td><code>containers-kubernetes.subnet.add</code></td>
<td>An existing IBM Cloud infrastructure subnet is added to a cluster.</td></tr><tr>
<td><code>containers-kubernetes.subnet.create</code></td>
<td>A subnet is created.</td></tr><tr>
<td><code>containers-kubernetes.usersubnet.add</code></td>
<td>A user-managed subnet is added to a cluster.</td></tr><tr>
<td><code>containers-kubernetes.usersubnet.delete</code></td>
<td>A user-managed subnet is removed from a cluster.</td></tr><tr>
<td><code>containers-kubernetes.version.update</code></td>
<td>The Kubernetes version of a cluster master node is updated.</td></tr><tr>
<td><code>containers-kubernetes.worker.create</code></td>
<td>A worker node is created.</td></tr><tr>
<td><code>containers-kubernetes.worker.delete</code></td>
<td>A worker node is deleted.</td></tr><tr>
<td><code>containers-kubernetes.worker.reboot</code></td>
<td>A worker node is rebooted.</td></tr><tr>
<td><code>containers-kubernetes.worker.reload</code></td>
<td>A worker node is reloaded.</td></tr><tr>
<td><code>containers-kubernetes.worker.update</code></td>
<td>A worker node is updated.</td></tr>
</table>

## Viewing your cluster events
{: #at-ui}

To [view events](/docs/Activity-Tracker-with-LogDNA?topic=logdnaat-view_events) that are sent to {{site.data.keyword.at_full_notm}}, you select the {{site.data.keyword.at_short}} instance that matches with the location of your Red Hat OpenShift on IBM Cloud cluster. You must first have an instance of {{site.data.keyword.at_short}} in each of the locations where your cluster is. Use the following table to find which {{site.data.keyword.at_short}} location your events are sent to based on the Red Hat OpenShift on IBM Cloud location where the cluster is located. Note that clusters in the Montreal, Toronto, and Washington, D.C. locations are available in Dallas.
{: shortdesc}

| Red Hat OpenShift on IBM Cloud metro | Red Hat OpenShift on IBM Cloud data center | {{site.data.keyword.at_short}} event location |
|-----|-----|-----|
| Dallas | dal10, dal12, dal13 | Dallas |
| Mexico City | mex01 | Dallas |
| Montreal | mon01 | Dallas |
| San Jose | sjc03, sjc04 | Dallas |
| São Paulo | sao01 | Dallas |
| Toronto | tor01 | Dallas |
| Washington, D.C. | wdc04, wdc06, wdc07 | Dallas |
| Amsterdam | ams03 | Frankfurt |
| Frankfurt | fra02, fra04, fra05 | Frankfurt |
| Milan | mil01 | Frankfurt |
| Oslo | osl01 | Frankfurt |
| Paris | par01 | Frankfurt |
| London | lon02,lon04, lon05, lon06 | London |
| Sydney | syd01, syd04, syd05 | Sydney |
| Melbourne | mel01 | Sydney |
| Chennai | che01 | Tokyo |
| Hong Kong<br>SAR of the PRC | hkg02 | Tokyo |
| Seoul | seo01 | Tokyo |
| Singapore | sng01 | Tokyo |
| Tokyo | tok02, tok04, tok05 | Tokyo |
{: caption="Corresponding {{site.data.keyword.at_short}} instance and Red Hat OpenShift on IBM Cloud cluster locations." caption-side="top"}



