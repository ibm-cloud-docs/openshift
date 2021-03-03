---

copyright:
  years: 2017, 2021
lastupdated: "2021-03-03"

keywords: openshift, roks, rhoks, rhos, audit

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



# {{site.data.keyword.at_full_notm}} events
{: #at_events}

You can view, manage, and audit user-initiated activities in your {{site.data.keyword.openshiftlong}} community Kubernetes or {{site.data.keyword.openshiftshort}} cluster by using the {{site.data.keyword.at_full}} service.
{: shortdesc}

{{site.data.keyword.openshiftlong_notm}} automatically generates cluster management events and forwards these event logs to {{site.data.keyword.at_full_notm}}. To access these logs, you must [provision an instance of {{site.data.keyword.at_full_notm}}](/docs/Activity-Tracker-with-LogDNA?topic=Activity-Tracker-with-LogDNA-getting-started).



## Cluster management events
{: #cluster-events}

The following list of the cluster management events are sent to {{site.data.keyword.at_full_notm}}.
{: shortdesc}


|Action|Description|
|------|-----------|
| `containers-kubernetes.account.create` | A classic infrastructure account is set for a region and resource group. This event is created when you run the [`ibmcloud oc credential set classic`](/docs/containers-cli-plugin?topic=containers-cli-plugin-kubernetes-service-cli#cs_logging_create) command. |
| `containers-kubernetes.account.delete` | A classic infrastructure account is removed for a region and resource group. This event is created when you run the [`ibmcloud oc ks credential unset`](/docs/containers-cli-plugin?topic=containers-cli-plugin-kubernetes-service-cli#cs_credentials_unset) command. |
| `containers-kubernetes.account.get` | The Kubernetes configuration file for a cluster (`kubeconfig`) is requested. |
| `containers-kubernetes.account.update` | Various account updates for a cluster are requested, such as setting the autoupdate policy for a cluster or integrating the cluster with a key management service (KMS). For more details on the action, review the target host address for the API method in the event. |
| `containers-kubernetes.cluster.config` | A `kubeconfig` file that contains the certificates and secrets to access a cluster is requested. |
| `containers-kubernetes.cluster.create` | A classic or VPC cluster is created or failed to create. |
| `containers-kubernetes.cluster.delete` | A cluster is deleted. |
| `containers-kubernetes.cluster.update` | Various updates to a cluster are requested, such as refreshing the master API server or enabling an add-on. For more details on the action, review the target host address for the API method in the event.|
| `containers-kubernetes.credentials.ready-to-use` | The cluster's control plane is updated to use a stored API key that authorizes underlying actions to other {{site.data.keyword.cloud_notm}} services, such as compute, networking, and storage infrastructure resources. |
| `containers-kubernetes.logging-config.create` | A log forwarding configuration is created. |
| `containers-kubernetes.logging-config.delete` | A log forwarding configuration is deleted. |
| `containers-kubernetes.logging-config.refresh` | A log forwarding configuration is refreshed. |
| `containers-kubernetes.logging-filter.create` | A logging filter is created. |
| `containers-kubernetes.logging-filter.delete` | A logging filter is deleted. |
| `containers-kubernetes.logging-filter.update` | A logging filter is updated. |
| `containers-kubernetes.logging-autoupdate.changed` | The logging add-on auto updater is enabled or disabled. |
| `containers-kubernetes.masterlog-retrieve` | A master log collection for the cluster is requested. |
| `containers-kubernetes.masterlog-status` | The status for the most recent master log collection is requested. |
| `containers-kubnertes.cluster.rbac.update` | The service is updating IAM information such as service roles for the cluster. This event is not triggered by a specific API method, but happens periodically in the background. |
| `containers-kubernetes.service.create` | An {{site.data.keyword.cloud_notm}} service is bound to a cluster. |
| `containers-kubernetes.service.delete` | An {{site.data.keyword.cloud_notm}} service is unbound from a cluster. |
| `containers-kubernetes.subnet.add` | An existing IBM Cloud infrastructure subnet is added to a cluster. |
| `containers-kubernetes.subnet.create` | A subnet is created. |
| `containers-kubernetes.subnet.update` | Attach or detach a public or private portable subnet with a cluster. |
| `containers-kubernetes.vlan.create` | Deprecated: A user-managed subnet is added to a cluster.|
| `containers-kubernetes.vlan.delete` | Deprecated: A user-managed subnet is removed from a cluster.|
| `containers-kubernetes.worker.create` | A worker node is created. |
| `containers-kubernetes.worker.delete` | A worker node is deleted. |
| `containers-kubernetes.worker.update` | A worker node is updated.|
| `containers-kubernetes.workerpool.create` | A worker pool is created.|
| `containers-kubernetes.workerpool.delete` | A worker pool is deleted. |
| `containers-kubernetes.workerpool.update` | A worker pool is updated. |
| `containers-kubernetes.zone.delete` | A zone is deleted from a worker pool. |
| `containers-kubernetes.zone.update` | The networking attributes for a zone that a worker pool uses are updated. |
{: caption="Cluster management events" caption-side="top"}
{: summary="The table rows are read from left to right. The first column contains the event for the action. The second column describes the action."}



## Ingress ALB events
{: #ingress-alb-events}

The following list of Ingress application load balancer (ALB) events are sent to {{site.data.keyword.at_full_notm}}.
{: shortdesc}

|Action|Description|
|------|-----------|
| `containers-kubernetes.cluster-alb.create` | A public or private ALB is created in the cluster. |
| `containers-kubernetes.cluster-alb.delete` | An ALB is disabled. |
| `containers-kubernetes.cluster-alb.enable` | An existing ALB is enabled in a cluster. |
| `containers-kubernetes.cluster-alb.get` | Details of an ALB are viewed. |
| `containers-kubernetes.cluster-alb.list` | ALBs in a cluster are listed. |
| `containers-kubernetes.cluster-alb.update` | ALB pods are updated. |
| `containers-kubernetes.cluster-alb-policy.get` | The status of automatic updates for Ingress ALBs is viewed. |
| `containers-kubernetes.cluster-alb-migration.start` | A migration of {{site.data.keyword.cloud_notm}} Ingress configmap and Ingress resources to the Kubernetes Ingress format is started. |
| `containers-kubernetes.cluster-alb-migration-status.get` | The status of the migration process is viewed. |
| `containers-kubernetes.cluster-ingress-status.get` | The status of migrated Ingress resources in a cluster is viewed. |
| `containers-kubernetes.cluster-alb-migration.cleanup` | Ingress resources and configmaps that are no longer needed after an Ingress migration are deleted. |
| `containers-kubernetes.cluster-alb-policy.update` | Automatic updates for the ALBs are enabled or disabled, or all ALB pods in a cluster are rolled back to their previously running build. |
| `containers-kubernetes.alb-image.list` | Supported Ingress controller images are listed. |
{: caption="Ingress ALB events" caption-side="top"}
{: summary="The table rows are read from left to right. The first column contains the event for the action. The second column describes the action."}

## Ingress secret events
{: #ingress-secret-events}

The following list of Ingress secret events are sent to {{site.data.keyword.at_full_notm}}.
{: shortdesc}

|Action|Description|
|------|-----------|
| `containers-kubernetes.cluster-ingress-secret.get` | Details for an Ingress secret are viewed. |
| `containers-kubernetes.cluster-ingress-secret.list` | Ingress secrets for a cluster are listed. |
| `containers-kubernetes.cluster-ingress-secret.create` | An Ingress secret for a certificate is created. |
| `containers-kubernetes.cluster-ingress-secret.delete` | An Ingress secret is deleted from the cluster. |
| `containers-kubernetes.cluster-ingress-secret.update` | The certificate for an Ingress secret is updated. |
| `containers-kubernetes.cluster-ingress-secret.notify` | When the default {{site.data.keyword.cloudcerts_short}} instance is created for a cluster, the {{site.data.keyword.cloudcerts_short}} notification channel for certificate updates is created. |
{: caption="Ingress secret events" caption-side="top"}
{: summary="The table rows are read from left to right. The first column contains the event for the action. The second column describes the action."}

## Observability events for logging and monitoring
{: #at-lm}

The following list of the logging and monitoring configuration events are sent to {{site.data.keyword.at_full_notm}} by the {{site.data.keyword.containerlong_notm}} observability plug-in.
{: shortdesc}

|Action|Description|
|------|-----------|
| `containers-kubernetes.observe-logging.create` | A LogDNA logging configuration is created for the cluster. | 
| `containers-kubernetes.observe-logging.get` | The details of a LogDNA logging configuration are returned. | 
| `containers-kubernetes.observe-logging.list` | LogDNA logging configurations for a cluster are listed. | 
| `containers-kubernetes.observe-logging.modify` | A LogDNA logging configuration is updated. | 
| `containers-kubernetes.observe-logging.remove` | A LogDNA logging configuration is removed from the cluster.| 
| `containers-kubernetes.observe-monitoring.create` | A Sysdig monitoring configuration is created for the cluster. | 
| `containers-kubernetes.observe-monitoring.get` | The details of a Sysdig monitoring configuration are returned. | 
| `containers-kubernetes.observe-monitoring.list` | Sysdig monitoring configurations for a cluster are listed. | 
| `containers-kubernetes.observe-monitoring.modify` | A Sysdig monitoring configuration is updated. |
| `containers-kubernetes.observe-monitoring.remove` | A Sysdig monitoring configuration is removed from the cluster. |
{: caption="Observability events for logging and monitoring" caption-side="top"}
{: summary="The table rows are read from left to right. The first column contains the event for the action. The second column describes the action."}

## NLB DNS events
{: #ingress-nlb-dns-events}

The following list of network load balancer (NLB) DNS events are sent to {{site.data.keyword.at_full_notm}}.
{: shortdesc}

|Action|Description|
|------|-----------|
| `containers-kubernetes.cluster-nlb-dns.list` | Registered NLB subdomains and NLB IP addresses are listed. |
| `containers-kubernetes.cluster-nlb-dns-monitor.get` | The health check monitor settings for an NLB subdomain are viewed. |
| `containers-kubernetes.cluster-nlb-dns-monitor.list` | The health check monitor settings for all NLB subdomains are listed. |
| `containers-kubernetes.cluster-nlb-dns-monitor-status.list` | The health check status for the IP addresses behind NLB subdomains in a cluster are listed. |
| `containers-kubernetes.cluster-nlb-dns-monitor.create` | A health check monitor for an NLB subdomain is configured. |
| `containers-kubernetes.cluster-ingress-secret.delete` | A secret is removed from an NLB subdomain. |
| `containers-kubernetes.cluster-ingress-secret.update` | Certificates for a secret are regenerated. |
| `containers-kubernetes.cluster-nlb-dns.create` | An NLB subdomain is created and associated with one or more NLB IP addresses (classic) or a hostname (VPC). |
| `containers-kubernetes.cluster-lb-hostname.delete` | The VPC load balancer hostname is removed from the DNS record for an existing NLB subdomain. |
| `containers-kubernetes.cluster-lb-hostname.update` | The DNS record for an NLB subdomain in a VPC cluster is updated by replacing the load balancer hostname. |
| `containers-kubernetes.cluster-nlb-dns.update` | A DNS record in a classic cluster is updated by adding an NLB IP address. |
| `containers-kubernetes.cluster-nlb-dns-monitor.update` | The health check monitor for an NLB subdomain is enabled or disabled. |
{: caption="NLB DNS events" caption-side="top"}
{: summary="The table rows are read from left to right. The first column contains the event for the action. The second column describes the action."}

## Private service endpoint allowlist events
{: #acl-events}

The following table lists the actions related to access control lists (ACLs) and the generation of events for clusters that use a private service endpoint allowlist.
{: shortdesc}

| Action  | Description  |
|---------|--------------|
| `containers-kubernetes.containers-kubernetes.network.acl.delete ` | The private service endpoint allowlist feature for a cluster is disabled. |
| `containers-kubernetes.containers-kubernetes.network.acl.get` | The subnet allowlist for the private service endpoint of a cluster is requested.  |
| `containers-kubernetes.containers-kubernetes.network.acl.update` | The private service endpoint allowlist feature for a cluster is enabled, subnets are added to the allowlist, or subnets are removed from the allowlist. |
{: caption="ACL events" caption-side="top"}
{: summary="The table rows are read from left to right. The first column contains the event for the action. The second column describes the action."}



## Storage events
{: #storage-events}

The following table lists the actions related to storage resources and the generation of events.
{: shortdesc}

| Action  | Description  |
|---------|--------------|
| `containers-kubernetes.storage-volume.delete` | A volume is deleted. |
| `containers-kubernetes.storage-volume.list` | Volumes in the {{site.data.keyword.cloud_notm}} account or as filtered by provider are retrieved. |
| `containers-kubernetes.storage-volume.read` | A volume is retrieved |
| `containers-kubernetes.storage-volume.update` | A volume is updated. |
| `containers-kubernetes.storage-attachment.create` | A volume attachment is created. | 
| `containers-kubernetes.storage-attachment.delete` | A volume attachment is deleted. |
| `containers-kubernetes.storage-attachment.list` | Volume attachments are retrieved. |
| `containers-kubernetes.storage-attachment.read` | A volume attachment is retrieved. |
{: caption="Storage events" caption-side="top"}
{: summary="The table rows are read from left to right. The first column contains the event for the action. The second column describes the action."}





## Viewing your cluster events
{: #at-ui}

To [view events](/docs/Activity-Tracker-with-LogDNA?topic=Activity-Tracker-with-LogDNA-view_events) that are sent to {{site.data.keyword.at_full_notm}}, you select the {{site.data.keyword.at_short}} instance that matches with the location of your {{site.data.keyword.openshiftlong_notm}} cluster.
{: shortdesc}

The following table shows the {{site.data.keyword.at_short}} location where your events are sent to. To view your events, make sure that you have an {{site.data.keyword.at_short}} instance in the location that matches your cluster location. Note that clusters in the Montreal, Toronto, and Washington, D.C. locations forward all events to the Dallas {{site.data.keyword.at_short}} location.

| {{site.data.keyword.openshiftlong_notm}} classic location | {{site.data.keyword.at_short}} event location |
|-----|-----|-----|
| Dallas (dal10, dal12, dal13) | Dallas |
| Mexico City (mex01) | Dallas |
| Montreal (mon01) | Dallas |
| San Jose (sjc03, sjc04) | Dallas |
| São Paulo (sao01) | Dallas |
| Toronto (tor01) | Dallas |
| Washington, D.C. (wdc04, wdc06, wdc07) | Dallas |
| Amsterdam (ams03) | Frankfurt |
| Frankfurt (fra02, fra04, fra05) | Frankfurt |
| Milan (mil01) | Frankfurt |
| Oslo (osl01) | Frankfurt |
| Paris (par01) | Frankfurt |
| London (lon02, lon04, lon05, lon06) | London |
| Sydney (syd01, syd04, syd05) | Tokyo |
| Chennai (che01) | Tokyo |
| Hong Kong SAR of the PRC (hkg02) | Tokyo |
| Seoul (seo01) | Tokyo |
| Singapore (sng01) | Tokyo |
| Tokyo (tok02, tok04, tok05) | Tokyo |
{: caption="Corresponding {{site.data.keyword.at_short}} instance and {{site.data.keyword.openshiftlong_notm}} cluster locations." caption-side="top"}
{: class="simple-tab-table"}
{: #atlocationclassic}
{: tab-title=" Locations for classic clusters"}
{: tab-group="at-locations"}

| {{site.data.keyword.openshiftlong_notm}} VPC location | {{site.data.keyword.at_short}} event location |
|-----|-----|-----|
| Dallas (us-south-1, us-south-2, us-south-3) | Dallas |
| Washington, D.C. (us-east-1, us-east-2, us-east-3) | Dallas |
| Frankfurt (eu-de-1, eu-de-2, eu-de-3) | Frankfurt |
| London (eu-gb-1, eu-gb-2, eu-gb-3) | London |
| Sydney (au-syd-1, au-syd-2, au-syd-3) | Tokyo |
| Tokyo (jp-tok-1, jp-tok-2, jp-tok-3) | Tokyo |
{: class="simple-tab-table"}
{: caption="Corresponding {{site.data.keyword.at_short}} instance and {{site.data.keyword.openshiftlong_notm}} cluster locations." caption-side="top"}
{: #atlocationvpc}
{: tab-title="Locations for VPC clusters"}
{: tab-group="at-locations"}


