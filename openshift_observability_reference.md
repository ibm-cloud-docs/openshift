---

copyright:
  years: 2014, 2020
lastupdated: "2020-12-17"

keywords: observability commands, observability cli, observability plug-in, logging commands, monitoring commands, logging cli, monitoring cli, logdna commands, sysdig commands, logging config, monitoring config

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



# Observability plug-in CLI
{: #observability_cli}

Refer to these commands to create and manage logging and monitoring configurations for your {{site.data.keyword.openshiftlong_notm}} cluster.
{: shortdesc}

Looking for `ibmcloud oc` commands? See the [{{site.data.keyword.openshiftlong_notm}} CLI reference](/docs/openshift?topic=openshift-kubernetes-service-cli).
{:tip}

## Logging commands


### `ibmcloud ob logging agent discover`
{:  #logging_agent_discover}

Discover LogDNA agents that you manually installed in your cluster without using the {{site.data.keyword.openshiftlong_notm}} observability plug-in, and make this logging configuration visible to the plug-in so that you can use the observability plug-in commands and functionality in the {{site.data.keyword.cloud_notm}} console to manage this configuration.
{: shortdesc}

```
ibmcloud ob logging agent discover --cluster CLUSTER [--instance LOGDNA_INSTANCE]
```
{: pre}

**Supported infrastructure provider**:
  * <img src="images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Classic
  * <img src="images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> VPC Generation 2 compute

**Minimum required permissions**:
- **Administrator** platform role and **Manager** service access role for all Kubernetes namespaces in {{site.data.keyword.containerlong_notm}}
- **Viewer** platform role for {{site.data.keyword.la_full_notm}}

**Command options**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>The name or ID of the cluster where you manually created a LogDNA logging configuration without using the {{site.data.keyword.openshiftlong_notm}} observability plug-in. To retrieve your cluster name or ID, run `ibmcloud oc clusters`. This value is required.</dd>

<dt><code>--instance <em>LOGDNA_INSTANCE</em></code></dt>
<dd>The ID or name of the {{site.data.keyword.la_full_notm}} service instance that you use in your logging configuration. This value is optional. If you do not provide this value, the {{site.data.keyword.la_full_notm}} service instance is automatically retrieved.</dd>

</dl>





### `ibmcloud ob logging config create`
{: #logging_config_create}

Create a logging configuration for your cluster to automatically collect pod logs and send them to {{site.data.keyword.la_full_notm}}.
{: shortdesc}

This command deploys a LogDNA agent as a Kubernetes daemon set in your cluster. The agent collects logs with the extension `*.log` and extensionless files that are stored in the `/var/log` directory of your pod from all projects, including `kube-system`. For more information, see [Forwarding cluster and app logs to {{site.data.keyword.la_full_notm}}](/docs/openshift?topic=openshift-health#openshift_logdna). For more information about {{site.data.keyword.la_full_notm}}, see [Securing your data](/docs/Log-Analysis-with-LogDNA?topic=Log-Analysis-with-LogDNA-mng-data).   

```
ibmcloud ob logging config create --cluster CLUSTER --instance LOGDNA_INSTANCE [--logdna-ingestion-key INGESTION_KEY] [--private-endpoint]  
```
{: pre}

**Supported infrastructure provider**:
  * <img src="images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Classic
  * <img src="images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> VPC Generation 2 compute

**Minimum required permissions**:
- **Administrator** platform role and **Manager** service access role for all Kubernetes namespaces in {{site.data.keyword.containerlong_notm}}
- **Editor** platform role and **Manager** server access role for {{site.data.keyword.la_full_notm}}

**Command options**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>The name or ID of the cluster for which you want to create a logging configuration for {{site.data.keyword.la_full_notm}}. To retrieve your cluster name or ID, run `ibmcloud oc clusters`. This value is required.</dd>

<dt><code>--instance <em>LOGDNA_INSTANCE</em></code></dt>
<dd>The ID or name of the {{site.data.keyword.la_full_notm}} service instance that you want to use to create the logging configuration. The service instance must be in the same {{site.data.keyword.cloud_notm}} account as your cluster, but can be in a different resource group or region than your cluster. To create a service instance, follow the steps in [Provision an instance](/docs/Log-Analysis-with-LogDNA?topic=Log-Analysis-with-LogDNA-provision). This value is required.</dd>

<dt><code>--logdna-ingestion-key <em>INGESTION_KEY</em></code></dt>
<dd>The LogDNA ingestion key that you want to use for your configuration. This value is optional. If you do not specify this option, the latest ingestion key is automatically retrieved.   </dd>

<dt><code>--private-endpoint</code><dt>
<dd>When you add this option to your command, the private service endpoint is used to connect to {{site.data.keyword.la_full_notm}}. To use the private service endpoint, your cluster must be enabled for using private service endpoints. {{site.data.keyword.openshiftlong_notm}} clusters that run version 4 do not support private service endpoints. You must use a cluster that runs version 3.11 to use this option. For more information, see worker communication to other services and networks in [clusters](/docs/openshift?topic=openshift-plan_clusters#worker-services-onprem). </dd>

</dl>

**Example**:
```
ibmcloud ob logging config create --cluster mycluster --instance mylogna
```
{: pre}

### `ibmcloud ob logging config delete`
{: #logging_config_delete}

Delete a LogDNA logging configuration from your cluster.
{: shortdesc}


To remove logging configurations that you manually set up without using the {{site.data.keyword.openshiftlong_notm}} observability plug-in, you must first make this configuration available to the plug-in by using the [`ibmcloud ob logging agent discover`](#logging_agent_discover) command.
{: note}

When you delete the logging configuration, the components that are deleted depend on how you created the logging configuration. For logging configurations that were created with the `ibmcloud ob logging config create` command, the daemon set for the LogDNA agent, the configmap, and secret are removed from your cluster, and pod logs are no longer sent to your {{site.data.keyword.la_full_notm}} service instance. Logging configurations that you manually created and made visible to the plug-in by using the `ibmcloud ob logging agent discover` command, only the configmap is removed. Your daemon set, secret, and the LogDNA agent are still deployed to your cluster and you must manually remove them. Because the configmap is removed, pod logs are no longer sent to your {{site.data.keyword.la_full_notm}} service instance. Independent of how you created the configuration, existing log data is still available in {{site.data.keyword.la_full_notm}} until your selected retention period ends.  
{: important}


```
ibmcloud ob logging config delete --cluster CLUSTER --instance LOGDNA_INSTANCE
```
{: pre}

**Supported infrastructure provider**:
  * <img src="images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Classic
  * <img src="images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> VPC Generation 2 compute

**Minimum required permissions**:
- **Administrator** platform role and **Manager** service access role for the `ibm-observe` Kubernetes namespaces in {{site.data.keyword.containerlong_notm}}.
- **Viewer** platform role for {{site.data.keyword.la_full_notm}}

**Command options**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>The name or ID of the cluster for which you want to delete an existing LogDNA logging configurations. To retrieve the cluster name or ID, run `ibmcloud oc clusters`. This value is required.</dd>

<dt><code>--instance <em>LOGDNA_INSTANCE</em></code></dt>
<dd>The ID or name of the {{site.data.keyword.la_full_notm}} service instance that you used in your logging configuration. To retrieve the service instance name, run `ibmcloud resource service-instances`. This value is required. </dd>

</dl>

**Example**:
```
ibmcloud ob logging config delete --cluster mycluster --instance mylogdna
```
{: pre}

### `ibmcloud ob logging config list`
{: #logging_config_list}

List all LogDNA logging configurations that were created for your cluster with the {{site.data.keyword.openshiftlong_notm}} observability plug-in.
{: shortdesc}


To list logging configurations that you manually set up without using the {{site.data.keyword.openshiftlong_notm}} observability plug-in, you must first make this configuration available to the plug-in by using the [`ibmcloud ob logging agent discover`](#logging_agent_discover) command.
{: note}

```
ibmcloud ob logging config list --cluster CLUSTER
```
{: pre}

**Supported infrastructure provider**:
  * <img src="images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Classic
  * <img src="images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> VPC Generation 2 compute

**Minimum required permissions**: 
- **Administrator** platform role and **Manager** service access role for the `ibm-observe` Kubernetes namespaces in {{site.data.keyword.containerlong_notm}}. 
- **Viewer** platform role for {{site.data.keyword.la_full_notm}}

**Command options**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>The name or ID of the cluster for which you want to list existing LogDNA logging configurations. This value is required.</dd>

</dl>



### `ibmcloud ob logging config enable public-endpoint|private-endpoint`
{: #logging_config_enable}

Use the public or private service endpoint to send data from your cluster to your LogDNA service instance.
{: shortdesc}

To use the private service endpoint, your cluster must be enabled for using private service endpoints. {{site.data.keyword.openshiftlong_notm}} clusters that run version 4 do not support private service endpoints. You must use a cluster that runs version 3.11 to use this option.
{: important}

```
ibmcloud ob logging config enable public-endpoint|private-endpoint --cluster CLUSTER --instance LOGDNA_INSTANCE
```
{: pre}

**Supported infrastructure provider**:
  * <img src="images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Classic
  * <img src="images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> VPC Generation 2 compute

**Minimum required permissions**:
- **Administrator** platform role and **Manager** service access role for all Kubernetes namespaces in {{site.data.keyword.containerlong_notm}}
- **Editor** platform role and **Manager** server access role for {{site.data.keyword.la_full_notm}}

**Command options**:
<dl>

<dt><code>public-endpoint|private-endpoint</code></dt>
<dd>Enter <code>public-endpoint</code> to use the public service endpoint of your {{site.data.keyword.la_full_notm}} service instance, or <code>private-endpoint</code> to use the private service endpoint to send logs from your cluster. This value is required. To use the private service endpoint, your cluster must be enabled for using private service endpoints. {{site.data.keyword.openshiftlong_notm}} clusters that run version 4 do not support private service endpoints. You must use a cluster that runs version 3.11 to use this option.  </dd>

<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>The name or ID of the cluster for which you want to enable the private or public service endpoint to connect to your LogDNA service instance. To retrieve your cluster name or ID, run `ibmcloud oc clusters`. This value is required.</dd>

<dt><code>--instance <em>LOGDNA_INSTANCE</em></code></dt>
<dd>The ID or name of the {{site.data.keyword.la_full_notm}} service instance to which you want to connect by using the public or private service endpoint. To retrieve the name, run `ibmcloud resource service-instances`. This value is required.</dd>

</dl>

### `ibmcloud ob logging config replace`
{: #logging_config_replace}

Replace the {{site.data.keyword.la_full_notm}} service instance or ingestion key that you use in your LogDNA logging configuration.
{: shortdesc}

**Replace the ingestion key of an existing {{site.data.keyword.la_full_notm}} service instance**:
```
ibmcloud ob logging config replace --cluster CLUSTER --instance LOGDNA_INSTANCE --logdna-ingestion-key INGESTION_KEY
```
{: pre}

**Replace the {{site.data.keyword.la_full_notm}} service instance**:
```
ibmcloud ob logging config replace --cluster CLUSTER --instance LOGDNA_INSTANCE  --new-instance LOGDNA_INSTANCE_NEW [--logdna-ingestion-key INGESTION_KEY]
```
{: pre}

**Supported infrastructure provider**:
  * <img src="images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Classic
  * <img src="images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> VPC Generation 2 compute

**Minimum required permissions**:
- **Administrator** platform role and **Manager** service access role for all Kubernetes namespaces in {{site.data.keyword.containerlong_notm}}
- **Editor** platform role and **Manager** server access role for {{site.data.keyword.la_full_notm}}

**Command options**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>The name or ID of the cluster for which you want to change the {{site.data.keyword.la_full_notm}} ingestion key or service instance that you use in your LogDNA logging configuration. This value is required.</dd>

<dt><code>--instance <em>LOGDNA_INSTANCE</em></code></dt>
<dd>The ID or name of the {{site.data.keyword.la_full_notm}} service instance for which you want to change the ingestion key, or the {{site.data.keyword.la_full_notm}} service instance that you want to replace. To retrieve the name, run `ibmcloud ob logging config list --cluster <cluster_name_or_ID>`. This value is required.</dd>

<dt><code>--new-instance <em>LOGDNA_INSTANCE_NEW</em></code></dt>
<dd>If you want to replace the {{site.data.keyword.la_full_notm}} service instance that you use in your LogDNA logging configuration, enter the ID or name of the new {{site.data.keyword.la_full_notm}} service instance that you want to use. This value is required if you want to replace the {{site.data.keyword.la_full_notm}} service instance. If you want to replace the ingestion key, do not include this command option.</dd>

<dt><code>--logdna-ingestion-key <em>INGESTION_KEY</em></code></dt>
<dd>The LogDNA ingestion key that you want to use for your configuration. For information about how to retrieve the ingestion key, see [Get the ingestion key through the {{site.data.keyword.cloud_notm}} UI](/docs/Log-Analysis-with-LogDNA?topic=Log-Analysis-with-LogDNA-ingestion_key#ibm_cloud_ui). This value is required if you want to replace the ingestion key, and optional if you want to replace the {{site.data.keyword.la_full_notm}} service instance. If you do not provide the ingestion key when replacing the {{site.data.keyword.la_full_notm}} service instance, the ingestion key that was last added is retrieved automatically.</dd>

</dl>

### `ibmcloud ob logging config show`
{: #logging_config_show}

Show the details of a LogDNA logging configuration.
{: shortdesc}

To show the details of logging configurations that you manually set up without using the {{site.data.keyword.openshiftlong_notm}} observability plug-in, you must first make this configuration available to the plug-in by using the [`ibmcloud ob logging agent discover`](#logging_agent_discover) command.
{: note}

```
ibmcloud ob logging config show --cluster CLUSTER --instance LOGDNA_INSTANCE
```
{: pre}

**Supported infrastructure provider**:
  * <img src="images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Classic
  * <img src="images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> VPC Generation 2 compute

**Minimum required permissions**:
- **Administrator** platform role and **Manager** service access role for the `ibm-observe` Kubernetes namespaces in {{site.data.keyword.containerlong_notm}}. 
- **Viewer** platform role for {{site.data.keyword.la_full_notm}}

**Command options**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>The name or ID of the cluster for which you want to list existing LogDNA logging configurations. To retrieve your cluster name or ID, run `ibmcloud oc clusters`. This value is required.</dd>

<dt><code>--instance <em>LOGDNA_INSTANCE</em></code></dt>
<dd>The ID or name of the {{site.data.keyword.la_full_notm}} service instance for which you want to show the logging configuration. To retrieve the name, run `ibmcloud resource service-instances`. This value is required.</dd>

</dl>

## Monitoring commands


### `ibmcloud ob monitoring agent discover`
{:  #monitoring_agent_discover}

Discover Sysdig agents that you manually installed in your cluster without using the {{site.data.keyword.openshiftlong_notm}} observability plug-in, and make this monitoring configuration visible to the plug-in so that you can use the observability plug-in commands and functionality in the {{site.data.keyword.cloud_notm}} console to manage this configuration.
{: shortdesc}

```
ibmcloud ob monitoring agent discover --cluster CLUSTER [--instance SYSDIG_INSTANCE]
```
{: pre}

**Supported infrastructure provider**:
  * <img src="images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Classic
  * <img src="images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> VPC Generation 2 compute

**Minimum required permissions**:
- **Administrator** platform role and **Manager** service access role for all Kubernetes namespaces in {{site.data.keyword.containerlong_notm}}
- **Viewer** platform role for {{site.data.keyword.mon_full_notm}}

**Command options**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>The name or ID of the cluster where you manually created a Sysdig monitoring configuration without using the {{site.data.keyword.openshiftlong_notm}} observability plug-in. To retrieve your cluster name or ID, run `ibmcloud oc clusters`. This value is required.</dd>

<dt><code>--instance <em>SYSDIG_INSTANCE</em></code></dt>
<dd>The ID or name of the {{site.data.keyword.mon_full_notm}} service instance that you use in your monitoring configuration. This value is optional. If you do not provide this value, the {{site.data.keyword.mon_full_notm}} service instance is automatically retrieved</dd>

</dl>


### `ibmcloud ob monitoring config create`
{: #monitoring_config_create}

Create a monitoring configuration for your cluster to automatically collect cluster and pod metrics, and send them to {{site.data.keyword.mon_full_notm}}.
{: shortdesc}

This command deploys a Sysdig agent as a Kubernetes daemon set in your cluster. The agent collects cluster and pod metrics, such as the worker node CPU and memory usage, and the amount of incoming and outgoing network traffic for your pods. For more information, see [Forwarding cluster and app metrics to {{site.data.keyword.mon_full_notm}}](/docs/openshift?topic=openshift-health-monitor#openshift_sysdig).

```
ibmcloud ob monitoring config create --cluster CLUSTER --instance SYSDIG_INSTANCE [--sysdig-access-key ACCESS_KEY] [--private-endpoint]
```
{: pre}

**Supported infrastructure provider**:
  * <img src="images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Classic
  * <img src="images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> VPC Generation 2 compute

**Minimum required permissions**:
- **Administrator** platform role and **Manager** service access role for all Kubernetes namespaces in {{site.data.keyword.containerlong_notm}}
- **Editor** platform role and **Manager** server access role for {{site.data.keyword.mon_full_notm}}

**Command options**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>The name or ID of the cluster for which you want to create a monitoring configuration for {{site.data.keyword.mon_full_notm}}. To retrieve your cluster name or ID, run `ibmcloud oc clusters`. This value is required.</dd>

<dt><code>--instance <em>SYSDIG_INSTANCE</em></code></dt>
<dd>The ID or name of the {{site.data.keyword.mon_full_notm}} service instance that you want to use to create the monitoring configuration. The service instance must be in the same {{site.data.keyword.cloud_notm}} account as your cluster, but can be in a different resource group or region than you cluster. To create a service instance, follow the steps in [Provision an instance](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-provision). This value is required.</dd>

<dt><code>--sysdig-access-key <em>ACCESS_KEY</em></code></dt>
<dd>The Sysdig access key that you want to use for your configuration. This value is optional. If you do not specify this option, the latest access key is used for your configuration. </dd>

<dt><code>--private-endpoint</code><dt>
<dd>When you add this option to your command, the private service endpoint is used to connect to {{site.data.keyword.mon_full_notm}}. To use the private service endpoint, your cluster must be enabled for using private service endpoints. {{site.data.keyword.openshiftlong_notm}} clusters that run version 4 do not support private service endpoints. You must use a cluster that runs version 3.11 to use this option. </dd>

</dl>

**Example**:
```
ibmcloud ob monitoring config create --cluster mycluster --instance mysysdig
```
{: pre}

### `ibmcloud ob monitoring config delete`
{: #monitoring_config_delete}

Delete a Sysdig monitoring configuration from your cluster.
{: shortdesc}


To remove monitoring configurations that you manually set up without using the {{site.data.keyword.openshiftlong_notm}} observability plug-in, you must first make this configuration available to the plug-in by using the [`ibmcloud ob monitoring agent discover`](#monitoring_agent_discover) command.
{: note}


When you delete the monitoring configuration, the components that are deleted depend on how you created the monitoring configuration. For monitoring configurations that were created with the `ibmcloud ob monitoring config create` command, the daemon set for the Sysdig agent, the configmap, and secret are removed from your cluster, and metrics are no longer sent to your {{site.data.keyword.mon_full_notm}} service instance. Monitoring configurations that you manually created and made visible to the plug-in by using the `ibmcloud ob monitoring agent discover` command, only the configmap is removed. Your daemon set, secret, and the Sysdig agent are still deployed to your cluster and you must manually remove them. Because the configmap is removed, metrics are no longer sent to your {{site.data.keyword.mon_full_notm}} service instance. Independent of how you created the configuration, existing metrics are still available in {{site.data.keyword.mon_full_notm}} until your selected retention period ends.  
{: important}

```
ibmcloud ob monitoring config delete --cluster CLUSTER --instance SYSDIG_INSTANCE
```
{: pre}

**Supported infrastructure provider**:
  * <img src="images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Classic
  * <img src="images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> VPC Generation 2 compute

**Minimum required permissions**:
- **Administrator** platform role and **Manager** service access role for the `ibm-observe` Kubernetes namespaces in {{site.data.keyword.containerlong_notm}}.
- **Viewer** platform role for {{site.data.keyword.mon_full_notm}}

**Command options**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>The name or ID of the cluster for which you want to delete an existing Sysdig logging configurations. To retrieve the cluster name or ID, run `ibmcloud oc clusters`. This value is required.</dd>

<dt><code>--instance <em>SYSDIG_INSTANCE</em></code></dt>
<dd>The ID or name of the {{site.data.keyword.mon_full_notm}} service instance that you used in your monitoring configuration. To retrieve the service instance name, run `ibmcloud resource service-instances`. This value is required. </dd>

</dl>

**Example**:
```
ibmcloud ob monitoring config delete --cluster mycluster --instance mysysdig
```
{: pre}

### `ibmcloud ob monitoring config list`
{: #monitoring_config_list}

List all Sysdig monitoring configurations that were created for your cluster with the {{site.data.keyword.openshiftlong_notm}} observability plug-in.
{: shortdesc}


To list monitoring configurations that you manually set up without using the {{site.data.keyword.openshiftlong_notm}} observability plug-in, you must first make this configuration available to the plug-in by using the [`ibmcloud ob monitoring agent discover`](#monitoring_agent_discover) command.
{: note}

```
ibmcloud ob monitoring config list --cluster CLUSTER
```
{: pre}

**Supported infrastructure provider**:
  * <img src="images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Classic
  * <img src="images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> VPC Generation 2 compute

**Minimum required permissions**: 
- **Administratorr** platform role and **Manager** service access role for the `ibm-observe` Kubernetes namespaces in {{site.data.keyword.containerlong_notm}}.
- **Viewer** platform role for {{site.data.keyword.mon_full_notm}}

**Command options**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>The name or ID of the cluster for which you want to list existing Sysdig monitoring configurations. This value is required.</dd>

</dl>


### `ibmcloud ob monitoring config enable public-endpoint|private-endpoint`
{: #monitoring_config_enable}

Use the public or private service endpoint to send metrics from your cluster to your Sysdig service instance.
{: shortdesc}

To use the private service endpoint, your cluster must be enabled for using private service endpoints. {{site.data.keyword.openshiftlong_notm}} clusters that run version 4 do not support private service endpoints. You must use a cluster that runs version 3.11 to use this option.
{: important}

```
ibmcloud ob monitoring config enable public-endpoint|private-endpoint --cluster CLUSTER --instance SYSDIG_INSTANCE
```
{: pre}

**Supported infrastructure provider**:
  * <img src="images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Classic
  * <img src="images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> VPC Generation 2 compute

**Minimum required permissions**:
- **Administrator** platform role and **Manager** service access role for all Kubernetes namespaces in {{site.data.keyword.containerlong_notm}}
- **Editor** platform role and **Manager** server access role for {{site.data.keyword.mon_full_notm}}

**Command options**:
<dl>

<dt><code>public-endpoint|private-endpoint</code></dt>
<dd>Enter <code>public-endpoint</code> to use the public service endpoint of your {{site.data.keyword.mon_full_notm}} service instance, or <code>private-endpoint</code> to use the private service endpoint to send metrics from your cluster. This value is required. To use the private service endpoint, your cluster must be enabled for using private service endpoints. {{site.data.keyword.openshiftlong_notm}} clusters that run version 4 do not support private service endpoints. You must use a cluster that runs version 3.11 to use this option.  </dd>

<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>The name or ID of the cluster for which you want to enable the private or public service endpoint to connect to your Sysdig service instance. To retrieve your cluster name or ID, run `ibmcloud oc clusters`. This value is required.</dd>

<dt><code>--instance <em>SYSDIG_INSTANCE</em></code></dt>
<dd>The ID or name of the {{site.data.keyword.mon_full_notm}} service instance to which you want to connect by using the public or private service endpoint. To retrieve the name, run `ibmcloud resource service-instances`. This value is required.</dd>

</dl>

### `ibmcloud ob monitoring config replace`
{: #monitoring_config_replace}

Replace the {{site.data.keyword.mon_full_notm}} service instance or service access key that you use in your Sysdig monitoring configuration.
{: shortdesc}

**Replace the service access key of an existing {{site.data.keyword.mon_full_notm}} service instance**:
```
ibmcloud ob logging config replace --cluster CLUSTER --instance SYSDIG_INSTANCE --sysdig-access-key ACCESS_KEY
```
{: pre}

**Replace the {{site.data.keyword.mon_full_notm}} service instance**:
```
ibmcloud ob logging config replace --cluster CLUSTER --instance SYSDIG_INSTANCE  --new-instance SYSDIG_INSTANCE_NEW [--sysdig-access-key ACCESS_KEY]
```
{: pre}

**Supported infrastructure provider**:
  * <img src="images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Classic
  * <img src="images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> VPC Generation 2 compute

**Minimum required permissions**:
- **Administrator** platform role and **Manager** service access role for all Kubernetes namespaces in {{site.data.keyword.containerlong_notm}}
- **Editor** platform role and **Manager** server access role for {{site.data.keyword.mon_full_notm}}

**Command options**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>The name or ID of the cluster for which you want to change the {{site.data.keyword.mon_full_notm}} service access key or service instance that you use in your Sysdig monitoring configuration. This value is required.</dd>

<dt><code>--instance <em>SYSDIG_INSTANCE</em></code></dt>
<dd>The ID or name of the {{site.data.keyword.mon_full_notm}} service instance for which you want to change the service access key, or the {{site.data.keyword.mon_full_notm}} service instance that you want to replace. To retrieve the name, run `ibmcloud ob monitoring config list --cluster <cluster_name_or_ID>`. This value is required.</dd>

<dt><code>--new-instance <em>SYSDIG_INSTANCE_NEW</em></code></dt>
<dd>If you want to replace the {{site.data.keyword.mon_full_notm}} service instance that you use in your Sysdig monitoring configuration, enter the ID or name of the new {{site.data.keyword.mon_full_notm}} service instance that you want to use. This value is required if you want to replace the {{site.data.keyword.mon_full_notm}} service instance. If you want to replace the service access key, do not include this command option.</dd>

<dt><code>--sysdig-access-key <em>ACCESS_KEY</em></code></dt>
<dd>The Sysdig service access key that you want to use for your configuration. For information about how to retrieve the service access key, see [Getting the access key through the {{site.data.keyword.cloud_notm}} UI](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-access_key#access_key_ibm_cloud_ui). This value is required if you want to replace the service access key, and optional if you want to replace the {{site.data.keyword.mon_full_notm}} service instance. If you do not provide the service access key when replacing the {{site.data.keyword.mon_full_notm}} service instance, the service access key that was last added is retrieved automatically.</dd>

</dl>

### `ibmcloud ob monitoring config show`
{: #monitoring_config_show}

Show the details of a Sysdig monitoring configuration.
{: shortdesc}

To show the details of monitoring configurations that you manually set up without using the {{site.data.keyword.openshiftlong_notm}} observability plug-in, you must first make this configuration available to the plug-in by using the [`ibmcloud ob monitoring agent discover`](#monitoring_agent_discover) command.
{: note}

```
ibmcloud ob monitoring config show --cluster CLUSTER --instance SYSDIG_INSTANCE
```
{: pre}

**Supported infrastructure provider**:
  * <img src="images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Classic
  * <img src="images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> VPC Generation 2 compute

**Minimum required permissions**: 
- **Administrator** platform role and **Manager** service access role for the `ibm-observe` Kubernetes namespaces in {{site.data.keyword.containerlong_notm}}.
- **Viewer** platform role for {{site.data.keyword.la_full_notm}}

**Command options**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>The name or ID of the cluster for which you want to list existing Sysdig monitoring configurations. To retrieve your cluster name or ID, run `ibmcloud oc clusters`. This value is required.</dd>

<dt><code>--instance <em>LOGDNA_INSTANCE</em></code></dt>
<dd>The ID or name of the {{site.data.keyword.mon_full_notm}} service instance for which you want to show the monitoring configuration. To retrieve the name, run `ibmcloud resource service-instances`. This value is required.</dd>

</dl>




