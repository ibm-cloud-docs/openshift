---

copyright:
  years: 2014, 2020
lastupdated: "2020-07-31"

keywords: observability commands, observability cli, observability plug-in, logging commands, monitoring commands, logging cli, monitoring cli, logdna commands, sysdig commands, logging config, monitoring config

subcollection: containers

---

{:beta: .beta}
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
{:step: data-tutorial-type='step'}


# Observability plug-in CLI
{: #observability_cli}

Refer to these commands to create and manage logging and monitoring configurations for your Red Hat OpenShift on IBM Cloud cluster.
{: shortdesc}

Looking for `ibmcloud oc` commands? See the [Red Hat OpenShift on IBM Cloud CLI reference](/docs/openshift?topic=openshift-kubernetes-service-cli).
{:tip}

## Logging commands




### `ibmcloud ob logging config create`
{: #logging_config_create}

Create a logging configuration for your cluster to automatically collect pod logs and send them to {{site.data.keyword.la_full_notm}}.
{: shortdesc}

This command deploys a LogDNA agent as a Kubernetes daemonset in your cluster. The agent collects logs with the extension `*.log` and extensionless files that are stored in the `/var/log` directory of your pod from all projects, including `kube-system`. For more information, see [Creating a logging configuration to forward cluster and app logs to {{site.data.keyword.la_full_notm}}](/docs/openshift?topic=openshift-health#openshift_logdna). For more information about {{site.data.keyword.la_full_notm}}, see [Securing your data](/docs/Log-Analysis-with-LogDNA?topic=Log-Analysis-with-LogDNA-mng-data).   

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
<dd>When you add this option to your command, the private service endpoint is used to connect to {{site.data.keyword.la_full_notm}}. To use the private service endpoint, your cluster must be enabled for using private service endpoints. Red Hat OpenShift on IBM Cloud clusters that run version 4 do not support private service endpoints. You must use a cluster that runs version 3.11 to use this option. For more information, see worker communication to other services and networks in [clusters](/docs/openshift?topic=openshift-plan_clusters#worker-services-onprem). </dd>

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



Existing logging configurations that you manually set up and that were not created with the Red Hat OpenShift on IBM Cloud observability plug-in are cannot be deleted with this command.
{: note}



When you delete the logging configuration, the daemonset for the LogDNA agent, the configmap, and secret are removed from your cluster, and pod logs are no longer sent to your {{site.data.keyword.la_full_notm}} service instance. However, existing log data is still available in {{site.data.keyword.la_full_notm}} until your selected retention period ends.  
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

List all LogDNA logging configurations that were created for your cluster with the Red Hat OpenShift on IBM Cloud observability plug-in.
{: shortdesc}


Existing logging configurations that you manually set up and that were not created with the Red Hat OpenShift on IBM Cloud observability plug-in are not listed with this command.
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


### `ibmcloud ob logging config show`
{: #logging_config_show}

Show the details of a LogDNA logging configuration.
{: shortdesc}

You cannot use this command to show the details of an existing logging configuration that you manually set up without the Red Hat OpenShift on IBM Cloud observability plug-in.
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


### `ibmcloud ob monitoring config create`
{: #monitoring_config_create}

Create a monitoring configuration for your cluster to automatically collect cluster and pod metrics, and send them to {{site.data.keyword.mon_full_notm}}.
{: shortdesc}

This command deploys a Sysdig agent as a Kubernetes daemonset in your cluster. The agent collects cluster and pod metrics, such as the worker node CPU and memory usage, and the amount of incoming and outgoing network traffic for your pods. For more information, see [Creating a monitoring configuration to forward cluster and app metrics to {{site.data.keyword.mon_full_notm}}](/docs/openshift?topic=openshift-health#openshift_sysdig).

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
<dd>When you add this option to your command, the private service endpoint is used to connect to {{site.data.keyword.mon_full_notm}}. To use the private service endpoint, your cluster must be enabled for using private service endpoints. Red Hat OpenShift on IBM Cloud clusters that run version 4 do not support private service endpoints. You must use a cluster that runs version 3.11 to use this option. </dd>

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


Existing monitoring configurations that you manually set up and that were not created with the Red Hat OpenShift on IBM Cloud observability plug-in cannot be deleted with this command.
{: note}


When you delete the monitoring configuration, the daemonset for the Sysdig agent, the configmap, and secret are removed from your cluster, and pod and cluster metrics are no longer sent to your {{site.data.keyword.mon_full_notm}} service instance. However, existing metrics are still available in {{site.data.keyword.mon_full_notm}} until your selected retention period ends.  
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
- **Viewer** platform role for {{site.data.keyword.la_full_notm}}

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

List all Sysdig monitoring configurations that were created for your cluster with the Red Hat OpenShift on IBM Cloud observability plug-in.
{: shortdesc}


Existing monitoring configurations that you manually set up and that were not created with the Red Hat OpenShift on IBM Cloud observability plug-in are not listed with this command.
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



### `ibmcloud ob monitoring config show`
{: #monitoring_config_show}

Show the details of a Sysdig monitoring configuration.
{: shortdesc}


You cannot use this command to show the details of an existing monitoring configuration that you manually set up without the Red Hat OpenShift on IBM Cloud observability plug-in. 

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





