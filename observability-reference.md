---

copyright: 
  years: 2014, 2021
lastupdated: "2021-10-21"

keywords: observability commands, observability cli, observability plug-in, logging commands, monitoring commands, logging cli, monitoring cli, logging config, monitoring config

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}


# Observability plug-in CLI
{: #observability_cli}

Refer to these commands to create and manage logging and monitoring configurations for your {{site.data.keyword.openshiftlong_notm}} cluster.
{: shortdesc}

Looking for `ibmcloud oc` commands? See the [{{site.data.keyword.openshiftlong_notm}} CLI reference](/docs/containers?topic=containers-kubernetes-service-cli).
{: tip}

## Logging commands
{: #logging-commands}
### `ibmcloud ob logging agent discover`
{: #logging_agent_discover}

Discover {{site.data.keyword.la_short}} agents that you manually installed in your cluster without using the {{site.data.keyword.openshiftlong_notm}} observability plug-in, and make this logging configuration visible to the plug-in so that you can use the observability plug-in commands and functionality in the {{site.data.keyword.cloud_notm}} console to manage this configuration.
{: shortdesc}

```sh
ibmcloud ob logging agent discover --cluster CLUSTER [--instance LOGGING_INSTANCE]
```
{: pre}

**Supported infrastructure provider**:
* ![Classic infrastructure provider icon.](images/icon-classic-2.svg) Classic
* ![VPC infrastructure provider icon.](images/icon-vpc-2.svg) VPC

**Minimum required permissions**:
- **Administrator** platform access role and **Manager** service access role for all Kubernetes namespaces in {{site.data.keyword.containerlong_notm}}
- **Viewer** platform access role for {{site.data.keyword.la_full_notm}}

**Command options**:
`--cluster CLUSTER`
:   The name or ID of the cluster where you manually created a {{site.data.keyword.la_short}} configuration without using the {{site.data.keyword.openshiftlong_notm}} observability plug-in. To retrieve your cluster name or ID, run `ibmcloud oc clusters`. This value is required.

`--instance LOGGING_INSTANCE`
:   The ID or name of the {{site.data.keyword.la_full_notm}} service instance that you use in your logging configuration. This value is optional. If you do not provide this value, the {{site.data.keyword.la_full_notm}} service instance is automatically retrieved.





### `ibmcloud ob logging config create`
{: #logging_config_create}

Create a logging configuration for your cluster to automatically collect pod logs and send them to {{site.data.keyword.la_full_notm}}.
{: shortdesc}

This command deploys a {{site.data.keyword.la_short}} agent as a Kubernetes daemon set in your cluster. The agent collects logs with the extension `*.log` and extensionless files that are stored in the `/var/log` directory of your pod from all projects, including `kube-system`. For more information, see [Forwarding cluster and app logs to {{site.data.keyword.la_full_notm}}](/docs/openshift?topic=openshift-health#openshift_logging). For more information about {{site.data.keyword.la_full_notm}}, see [Securing your data](/docs/log-analysis?topic=log-analysis-mng-data).   

```sh
ibmcloud ob logging config create --cluster CLUSTER --instance LOGGING_INSTANCE [--logdna-ingestion-key INGESTION_KEY] [--private-endpoint]  
```
{: pre}

**Supported infrastructure provider**:
* ![Classic infrastructure provider icon.](images/icon-classic-2.svg) Classic
* ![VPC infrastructure provider icon.](images/icon-vpc-2.svg) VPC

**Minimum required permissions**:
- **Administrator** platform access role and **Manager** service access role for all Kubernetes namespaces in {{site.data.keyword.containerlong_notm}}
- **Editor** platform access role and **Manager** server access role for {{site.data.keyword.la_full_notm}}

**Command options**:

`--cluster CLUSTER`
:   The name or ID of the cluster for which you want to create a logging configuration for {{site.data.keyword.la_full_notm}}. To retrieve your cluster name or ID, run `ibmcloud oc clusters`. This value is required.

`--instance LOGGING_INSTANCE`
:   The ID or name of the {{site.data.keyword.la_full_notm}} service instance that you want to use to create the logging configuration. The service instance must be in the same {{site.data.keyword.cloud_notm}} account as your cluster, but can be in a different resource group or region than your cluster. To create a service instance, follow the steps in [Provision an instance](/docs/log-analysis?topic=log-analysis-provision). This value is required.

`--logdna-ingestion-key INGESTION_KEY`
:   The {{site.data.keyword.la_short}} ingestion key that you want to use for your configuration. This value is optional. If you do not specify this option, the latest ingestion key is automatically retrieved.   

`--private-endpoint
:   When you add this option to your command, the private cloud service endpoint is used to connect to {{site.data.keyword.la_full_notm}}. To use the private cloud service endpoint, your cluster must be enabled for using private cloud service endpoints. {{site.data.keyword.openshiftlong_notm}} clusters that run version 4 do not support private cloud service endpoints. You must use a cluster that runs version 3.11 to use this option. For more information, see worker communication to other services and networks in [clusters](/docs/openshift?topic=openshift-plan_clusters#worker-services-onprem). 



Example command
```sh
ibmcloud ob logging config create --cluster mycluster --instance mylogna
```
{: pre}

### `ibmcloud ob logging config delete`
{: #logging_config_delete}

Delete a {{site.data.keyword.la_short}} configuration from your cluster.
{: shortdesc}


To remove logging configurations that you manually set up without using the {{site.data.keyword.openshiftlong_notm}} observability plug-in, you must first make this configuration available to the plug-in by using the `ibmcloud ob logging agent discover` [command](#logging_agent_discover).
{: note}

When you delete the logging configuration, the components that are deleted depend on how you created the logging configuration. For logging configurations that were created with the `ibmcloud ob logging config create` command, the daemon set for the {{site.data.keyword.la_short}} agent, the configmap, and secret are removed from your cluster, and pod logs are no longer sent to your {{site.data.keyword.la_full_notm}} service instance. Logging configurations that you manually created and made visible to the plug-in by using the `ibmcloud ob logging agent discover` command, only the configmap is removed. Your daemon set, secret, and the {{site.data.keyword.la_short}} agent are still deployed to your cluster and you must manually remove them. Because the configmap is removed, pod logs are no longer sent to your {{site.data.keyword.la_full_notm}} service instance. Independent of how you created the configuration, existing log data is still available in {{site.data.keyword.la_full_notm}} until your selected retention period ends.  
{: important}


```sh
ibmcloud ob logging config delete --cluster CLUSTER --instance LOGGING_INSTANCE
```
{: pre}

**Supported infrastructure provider**:
* ![Classic infrastructure provider icon.](images/icon-classic-2.svg) Classic
* ![VPC infrastructure provider icon.](images/icon-vpc-2.svg) VPC

**Minimum required permissions**:
- **Administrator** platform access role and **Manager** service access role for the `ibm-observe` Kubernetes namespaces in {{site.data.keyword.containerlong_notm}}.
- **Viewer** platform access role for {{site.data.keyword.la_full_notm}}

**Command options**:

`--cluster CLUSTER`
:   The name or ID of the cluster for which you want to delete an existing {{site.data.keyword.la_short}} configurations. To retrieve the cluster name or ID, run `ibmcloud oc clusters`. This value is required.

`--instance LOGGING_INSTANCE`
:   The ID or name of the {{site.data.keyword.la_full_notm}} service instance that you used in your logging configuration. To retrieve the service instance name, run `ibmcloud resource service-instances`. This value is required. 



Example command
```sh
ibmcloud ob logging config delete --cluster mycluster --instance mylogginginstance
```
{: pre}

### `ibmcloud ob logging config list`
{: #logging_config_list}

List all {{site.data.keyword.la_short}} configurations that were created for your cluster with the {{site.data.keyword.openshiftlong_notm}} observability plug-in.
{: shortdesc}


To list logging configurations that you manually set up without using the {{site.data.keyword.openshiftlong_notm}} observability plug-in, you must first make this configuration available to the plug-in by using the [`ibmcloud ob logging agent discover`](#logging_agent_discover) command.
{: note}

```sh
ibmcloud ob logging config list --cluster CLUSTER
```
{: pre}

**Supported infrastructure provider**:
* ![Classic infrastructure provider icon.](images/icon-classic-2.svg) Classic
* ![VPC infrastructure provider icon.](images/icon-vpc-2.svg) VPC

**Minimum required permissions**: 
- **Administrator** platform access role and **Manager** service access role for the `ibm-observe` Kubernetes namespaces in {{site.data.keyword.containerlong_notm}}. 
- **Viewer** platform access role for {{site.data.keyword.la_full_notm}}

**Command options**:

`--cluster CLUSTER`
:   The name or ID of the cluster for which you want to list existing {{site.data.keyword.la_short}} configurations. This value is required.





### `ibmcloud ob logging config enable public-endpoint|private-endpoint`
{: #logging_config_enable}

Use the public or private cloud service endpoint to send data from your cluster to your {{site.data.keyword.la_short}} service instance.
{: shortdesc}

To use the private cloud service endpoint, your cluster must be enabled for using private cloud service endpoints. {{site.data.keyword.openshiftlong_notm}} clusters that run version 4 do not support private cloud service endpoints. You must use a cluster that runs version 3.11 to use this option.
{: important}

```sh
ibmcloud ob logging config enable public-endpoint|private-endpoint --cluster CLUSTER --instance LOGGING_INSTANCE
```
{: pre}

**Supported infrastructure provider**:
* ![Classic infrastructure provider icon.](images/icon-classic-2.svg) Classic
* ![VPC infrastructure provider icon.](images/icon-vpc-2.svg) VPC

**Minimum required permissions**:
- **Administrator** platform access role and **Manager** service access role for all Kubernetes namespaces in {{site.data.keyword.containerlong_notm}}
- **Editor** platform access role and **Manager** server access role for {{site.data.keyword.la_full_notm}}

**Command options**:


`public-endpoint|private-endpoint`
:   Enter `public-endpoint` to use the public cloud service endpoint of your {{site.data.keyword.la_full_notm}} service instance, or `private-endpoint` to use the private cloud service endpoint to send logs from your cluster. This value is required. To use the private cloud service endpoint, your cluster must be enabled for using private cloud service endpoints. {{site.data.keyword.openshiftlong_notm}} clusters that run version 4 do not support private cloud service endpoints. You must use a cluster that runs version 3.11 to use this option.  

`--cluster CLUSTER`
:   The name or ID of the cluster for which you want to enable the private or public cloud service endpoint to connect to your {{site.data.keyword.la_short}} service instance. To retrieve your cluster name or ID, run `ibmcloud oc clusters`. This value is required.

`--instance LOGGING_INSTANCE`
:   The ID or name of the {{site.data.keyword.la_full_notm}} service instance to which you want to connect by using the public or private cloud service endpoint. To retrieve the name, run `ibmcloud resource service-instances`. This value is required.



### `ibmcloud ob logging config replace`
{: #logging_config_replace}

Replace the {{site.data.keyword.la_full_notm}} service instance or ingestion key that you use in your {{site.data.keyword.la_short}} configuration.
{: shortdesc}

**Replace the ingestion key of an existing {{site.data.keyword.la_full_notm}} service instance**:
```sh
ibmcloud ob logging config replace --cluster CLUSTER --instance LOGGING_INSTANCE --logdna-ingestion-key INGESTION_KEY
```
{: pre}

**Replace the {{site.data.keyword.la_full_notm}} service instance**:
```sh
ibmcloud ob logging config replace --cluster CLUSTER --instance LOGGING_INSTANCE  --new-instance LOGGING_INSTANCE_NEW [--logdna-ingestion-key INGESTION_KEY]
```
{: pre}

**Supported infrastructure provider**:
* ![Classic infrastructure provider icon.](images/icon-classic-2.svg) Classic
* ![VPC infrastructure provider icon.](images/icon-vpc-2.svg) VPC

**Minimum required permissions**:
- **Administrator** platform access role and **Manager** service access role for all Kubernetes namespaces in {{site.data.keyword.containerlong_notm}}
- **Editor** platform access role and **Manager** server access role for {{site.data.keyword.la_full_notm}}

**Command options**:

`--cluster CLUSTER`
:   The name or ID of the cluster for which you want to change the {{site.data.keyword.la_full_notm}} ingestion key or service instance that you use in your {{site.data.keyword.la_short}} configuration. This value is required.

`--instance LOGGING_INSTANCE`
:   The ID or name of the {{site.data.keyword.la_full_notm}} service instance for which you want to change the ingestion key, or the {{site.data.keyword.la_full_notm}} service instance that you want to replace. To retrieve the name, run `ibmcloud ob logging config list --cluster <cluster_name_or_ID>`. This value is required.

`--new-instance LOGGING_INSTANCE_NEW`
:   If you want to replace the {{site.data.keyword.la_full_notm}} service instance that you use in your {{site.data.keyword.la_short}} configuration, enter the ID or name of the new {{site.data.keyword.la_full_notm}} service instance that you want to use. This value is required if you want to replace the {{site.data.keyword.la_full_notm}} service instance. If you want to replace the ingestion key, do not include this command option.

`--logdna-ingestion-key INGESTION_KEY`
:   The {{site.data.keyword.la_short}} ingestion key that you want to use for your configuration. For information about how to retrieve the ingestion key, see [Get the ingestion key through the {{site.data.keyword.cloud_notm}} UI](/docs/log-analysis?topic=log-analysis-ingestion_key#ibm_cloud_ui). This value is required if you want to replace the ingestion key, and optional if you want to replace the {{site.data.keyword.la_full_notm}} service instance. If you do not provide the ingestion key when replacing the {{site.data.keyword.la_full_notm}} service instance, the ingestion key that was last added is retrieved automatically.



### `ibmcloud ob logging config show`
{: #logging_config_show}

Show the details of a {{site.data.keyword.la_short}} configuration.
{: shortdesc}

To show the details of logging configurations that you manually set up without using the {{site.data.keyword.openshiftlong_notm}} observability plug-in, you must first make this configuration available to the plug-in by using the [`ibmcloud ob logging agent discover`](#logging_agent_discover) command.
{: note}

```sh
ibmcloud ob logging config show --cluster CLUSTER --instance LOGGING_INSTANCE
```
{: pre}

**Supported infrastructure provider**:
* ![Classic infrastructure provider icon.](images/icon-classic-2.svg) Classic
* ![VPC infrastructure provider icon.](images/icon-vpc-2.svg) VPC

**Minimum required permissions**:
- **Administrator** platform access role and **Manager** service access role for the `ibm-observe` Kubernetes namespaces in {{site.data.keyword.containerlong_notm}}. 
- **Viewer** platform access role for {{site.data.keyword.la_full_notm}}

**Command options**:

`--cluster CLUSTER`
:   The name or ID of the cluster for which you want to list existing {{site.data.keyword.la_short}} configurations. To retrieve your cluster name or ID, run `ibmcloud oc clusters`. This value is required.

`--instance LOGGING_INSTANCE`
:   The ID or name of the {{site.data.keyword.la_full_notm}} service instance for which you want to show the logging configuration. To retrieve the name, run `ibmcloud resource service-instances`. This value is required.



## Monitoring commands


### `ibmcloud ob monitoring agent discover`
{: #monitoring_agent_discover}

Discover {{site.data.keyword.mon_short}} agents that you manually installed in your cluster without using the {{site.data.keyword.openshiftlong_notm}} observability plug-in, and make this monitoring configuration visible to the plug-in so that you can use the observability plug-in commands and functionality in the {{site.data.keyword.cloud_notm}} console to manage this configuration.
{: shortdesc}

```sh
ibmcloud ob monitoring agent discover --cluster CLUSTER [--instance MONITORING_INSTANCE]
```
{: pre}

**Supported infrastructure provider**:
* ![Classic infrastructure provider icon.](images/icon-classic-2.svg) Classic
* ![VPC infrastructure provider icon.](images/icon-vpc-2.svg) VPC

**Minimum required permissions**:
- **Administrator** platform access role and **Manager** service access role for all Kubernetes namespaces in {{site.data.keyword.containerlong_notm}}
- **Viewer** platform access role for {{site.data.keyword.mon_full_notm}}

**Command options**:

`--cluster CLUSTER`
:   The name or ID of the cluster where you manually created a {{site.data.keyword.mon_short}} configuration without using the {{site.data.keyword.openshiftlong_notm}} observability plug-in. To retrieve your cluster name or ID, run `ibmcloud oc clusters`. This value is required.

`--instance MONITORING_INSTANCE`
:   The ID or name of the {{site.data.keyword.mon_full_notm}} service instance that you use in your monitoring configuration. This value is optional. If you do not provide this value, the {{site.data.keyword.mon_full_notm}} service instance is automatically retrieved




### `ibmcloud ob monitoring config create`
{: #monitoring_config_create}

Create a monitoring configuration for your cluster to automatically collect cluster and pod metrics, and send them to {{site.data.keyword.mon_full_notm}}.
{: shortdesc}

This command deploys a {{site.data.keyword.mon_short}} agent as a Kubernetes daemon set in your cluster. The agent collects cluster and pod metrics, such as the worker node CPU and memory usage, and the amount of incoming and outgoing network traffic for your pods. For more information, see [Forwarding cluster and app metrics to {{site.data.keyword.mon_full_notm}}](/docs/openshift?topic=openshift-health-monitor#openshift_monitoring).

```sh
ibmcloud ob monitoring config create --cluster CLUSTER --instance MONITORING_INSTANCE [--sysdig-access-key ACCESS_KEY] [--private-endpoint]
```
{: pre}

**Supported infrastructure provider**:
* ![Classic infrastructure provider icon.](images/icon-classic-2.svg) Classic
* ![VPC infrastructure provider icon.](images/icon-vpc-2.svg) VPC

**Minimum required permissions**:
- **Administrator** platform access role and **Manager** service access role for all Kubernetes namespaces in {{site.data.keyword.containerlong_notm}}
- **Editor** platform access role and **Manager** server access role for {{site.data.keyword.mon_full_notm}}

**Command options**:

`--cluster CLUSTER`
:   The name or ID of the cluster for which you want to create a monitoring configuration for {{site.data.keyword.mon_full_notm}}. To retrieve your cluster name or ID, run `ibmcloud oc clusters`. This value is required.

`--instance MONITORING_INSTANCE`
:   The ID or name of the {{site.data.keyword.mon_full_notm}} service instance that you want to use to create the monitoring configuration. The service instance must be in the same {{site.data.keyword.cloud_notm}} account as your cluster, but can be in a different resource group or region than you cluster. To create a service instance, follow the steps in [Provision an instance](/docs/monitoring?topic=monitoring-provision). This value is required.

`--sysdig-access-key ACCESS_KEY`
:   The {{site.data.keyword.mon_short}} access key that you want to use for your configuration. This value is optional. If you do not specify this option, the latest access key is used for your configuration. 

`--private-endpoint
:   When you add this option to your command, the private cloud service endpoint is used to connect to {{site.data.keyword.mon_full_notm}}. To use the private cloud service endpoint, your cluster must be enabled for using private cloud service endpoints. {{site.data.keyword.openshiftlong_notm}} clusters that run version 4 do not support private cloud service endpoints. You must use a cluster that runs version 3.11 to use this option. 



Example command
```sh
ibmcloud ob monitoring config create --cluster mycluster --instance mymonitoringinstance
```
{: pre}

### `ibmcloud ob monitoring config delete`
{: #monitoring_config_delete}

Delete a {{site.data.keyword.mon_short}} configuration from your cluster.
{: shortdesc}


To remove monitoring configurations that you manually set up without using the {{site.data.keyword.openshiftlong_notm}} observability plug-in, you must first make this configuration available to the plug-in by using the ibmcloud ob monitoring agent discover` [command](#monitoring_agent_discover).
{: note}


When you delete the monitoring configuration, the components that are deleted depend on how you created the monitoring configuration. For monitoring configurations that were created with the `ibmcloud ob monitoring config create` command, the daemon set for the {{site.data.keyword.mon_short}} agent, the configmap, and secret are removed from your cluster, and metrics are no longer sent to your {{site.data.keyword.mon_full_notm}} service instance. Monitoring configurations that you manually created and made visible to the plug-in by using the `ibmcloud ob monitoring agent discover` command, only the configmap is removed. Your daemon set, secret, and the {{site.data.keyword.mon_short}} agent are still deployed to your cluster and you must manually remove them. Because the configmap is removed, metrics are no longer sent to your {{site.data.keyword.mon_full_notm}} service instance. Independent of how you created the configuration, existing metrics are still available in {{site.data.keyword.mon_full_notm}} until your selected retention period ends.  
{: important}

```sh
ibmcloud ob monitoring config delete --cluster CLUSTER --instance MONITORING_INSTANCE
```
{: pre}

**Supported infrastructure provider**:
* ![Classic infrastructure provider icon.](images/icon-classic-2.svg) Classic
* ![VPC infrastructure provider icon.](images/icon-vpc-2.svg) VPC

**Minimum required permissions**:
- **Administrator** platform access role and **Manager** service access role for the `ibm-observe` Kubernetes namespaces in {{site.data.keyword.containerlong_notm}}.
- **Viewer** platform access role for {{site.data.keyword.mon_full_notm}}

**Command options**:

`--cluster CLUSTER`
:   The name or ID of the cluster for which you want to delete an existing {{site.data.keyword.mon_short}} configuration. To retrieve the cluster name or ID, run `ibmcloud oc cluster ls`. This value is required.

`--instance MONITORING_INSTANCE`
:   The ID or name of the {{site.data.keyword.mon_full_notm}} service instance that you used in your monitoring configuration. To retrieve the service instance name, run `ibmcloud resource service-instances`. This value is required. 



Example command
```sh
ibmcloud ob monitoring config delete --cluster mycluster --instance mymonitoringinstance
```
{: pre}

### `ibmcloud ob monitoring config list`
{: #monitoring_config_list}

List all {{site.data.keyword.mon_short}} configurations that were created for your cluster with the {{site.data.keyword.openshiftlong_notm}} observability plug-in.
{: shortdesc}


To list monitoring configurations that you manually set up without using the {{site.data.keyword.openshiftlong_notm}} observability plug-in, you must first make this configuration available to the plug-in by using the [`ibmcloud ob monitoring agent discover`](#monitoring_agent_discover) command.
{: note}

```sh
ibmcloud ob monitoring config list --cluster CLUSTER
```
{: pre}

**Supported infrastructure provider**:
* ![Classic infrastructure provider icon.](images/icon-classic-2.svg) Classic
* ![VPC infrastructure provider icon.](images/icon-vpc-2.svg) VPC

**Minimum required permissions**: 
- **Administratorr** platform access role and **Manager** service access role for the `ibm-observe` Kubernetes namespaces in {{site.data.keyword.containerlong_notm}}.
- **Viewer** platform access role for {{site.data.keyword.mon_full_notm}}

**Command options**:

`--cluster CLUSTER`
:   The name or ID of the cluster for which you want to list existing {{site.data.keyword.mon_short}} configurations. This value is required.




### `ibmcloud ob monitoring config enable public-endpoint|private-endpoint`
{: #monitoring_config_enable}

Use the public or private cloud service endpoint to send metrics from your cluster to your {{site.data.keyword.mon_short}} service instance.
{: shortdesc}

To use the private cloud service endpoint, your cluster must be enabled for using private cloud service endpoints. {{site.data.keyword.openshiftlong_notm}} clusters that run version 4 do not support private cloud service endpoints. You must use a cluster that runs version 3.11 to use this option.
{: important}

```sh
ibmcloud ob monitoring config enable public-endpoint|private-endpoint --cluster CLUSTER --instance MONITORING_INSTANCE
```
{: pre}

**Supported infrastructure provider**:
* ![Classic infrastructure provider icon.](images/icon-classic-2.svg) Classic
* ![VPC infrastructure provider icon.](images/icon-vpc-2.svg) VPC

**Minimum required permissions**:
- **Administrator** platform access role and **Manager** service access role for all Kubernetes namespaces in {{site.data.keyword.containerlong_notm}}
- **Editor** platform access role and **Manager** server access role for {{site.data.keyword.mon_full_notm}}

**Command options**:


`public-endpoint|private-endpoint`
:   Enter `public-endpoint` to use the public cloud service endpoint of your {{site.data.keyword.mon_full_notm}} service instance, or `private-endpoint` to use the private cloud service endpoint to send metrics from your cluster. This value is required. To use the private cloud service endpoint, your cluster must be enabled for using private cloud service endpoints. {{site.data.keyword.openshiftlong_notm}} clusters that run version 4 do not support private cloud service endpoints. You must use a cluster that runs version 3.11 to use this option.  

`--cluster CLUSTER`
:   The name or ID of the cluster for which you want to enable the private or public cloud service endpoint to connect to your {{site.data.keyword.mon_short}} service instance. To retrieve your cluster name or ID, run `ibmcloud oc clusters`. This value is required.

`--instance MONITORING_INSTANCE`
:   The ID or name of the {{site.data.keyword.mon_full_notm}} service instance to which you want to connect by using the public or private cloud service endpoint. To retrieve the name, run `ibmcloud resource service-instances`. This value is required.



### `ibmcloud ob monitoring config replace`
{: #monitoring_config_replace}

Replace the {{site.data.keyword.mon_full_notm}} service instance or service access key that you use in your {{site.data.keyword.mon_short}} configuration.
{: shortdesc}

**Replace the service access key of an existing {{site.data.keyword.mon_full_notm}} service instance**:
```sh
ibmcloud ob logging config replace --cluster CLUSTER --instance MONITORING_INSTANCE --sysdig-access-key ACCESS_KEY
```
{: pre}

**Replace the {{site.data.keyword.mon_full_notm}} service instance**:
```sh
ibmcloud ob logging config replace --cluster CLUSTER --instance MONITORING_INSTANCE  --new-instance MONITORING_INSTANCE_NEW [--sysdig-access-key ACCESS_KEY]
```
{: pre}

**Supported infrastructure provider**:
* ![Classic infrastructure provider icon.](images/icon-classic-2.svg) Classic
* ![VPC infrastructure provider icon.](images/icon-vpc-2.svg) VPC

**Minimum required permissions**:
- **Administrator** platform access role and **Manager** service access role for all Kubernetes namespaces in {{site.data.keyword.containerlong_notm}}
- **Editor** platform access role and **Manager** server access role for {{site.data.keyword.mon_full_notm}}

**Command options**:

`--cluster CLUSTER`
:   The name or ID of the cluster for which you want to change the {{site.data.keyword.mon_full_notm}} service access key or service instance that you use in your {{site.data.keyword.mon_short}} configuration. This value is required.

`--instance MONITORING_INSTANCE`
:   The ID or name of the {{site.data.keyword.mon_full_notm}} service instance for which you want to change the service access key, or the {{site.data.keyword.mon_full_notm}} service instance that you want to replace. To retrieve the name, run `ibmcloud ob monitoring config list --cluster <cluster_name_or_ID>`. This value is required.

`--new-instance MONITORING_INSTANCE_NEW`
:   If you want to replace the {{site.data.keyword.mon_full_notm}} service instance that you use in your {{site.data.keyword.mon_short}} configuration, enter the ID or name of the new {{site.data.keyword.mon_full_notm}} service instance that you want to use. This value is required if you want to replace the {{site.data.keyword.mon_full_notm}} service instance. If you want to replace the service access key, do not include this command option.

`--sysdig-access-key ACCESS_KEY`
:   The {{site.data.keyword.mon_short}} service access key that you want to use for your configuration. For information about how to retrieve the service access key, see [Getting the access key through the {{site.data.keyword.cloud_notm}} UI](/docs/monitoring?topic=monitoring-access_key#access_key_ibm_cloud_ui). This value is required if you want to replace the service access key, and optional if you want to replace the {{site.data.keyword.mon_full_notm}} service instance. If you do not provide the service access key when replacing the {{site.data.keyword.mon_full_notm}} service instance, the service access key that was last added is retrieved automatically.



### `ibmcloud ob monitoring config show`
{: #monitoring_config_show}

Show the details of a {{site.data.keyword.mon_short}} configuration.
{: shortdesc}

To show the details of monitoring configurations that you manually set up without using the {{site.data.keyword.openshiftlong_notm}} observability plug-in, you must first make this configuration available to the plug-in by using the [`ibmcloud ob monitoring agent discover`](#monitoring_agent_discover) command.
{: note}

```sh
ibmcloud ob monitoring config show --cluster CLUSTER --instance MONITORING_INSTANCE
```
{: pre}

**Supported infrastructure provider**:
* ![Classic infrastructure provider icon.](images/icon-classic-2.svg) Classic
* ![VPC infrastructure provider icon.](images/icon-vpc-2.svg) VPC

**Minimum required permissions**: 
- **Administrator** platform access role and **Manager** service access role for the `ibm-observe` Kubernetes namespaces in {{site.data.keyword.containerlong_notm}}.
- **Viewer** platform access role for {{site.data.keyword.la_full_notm}}

**Command options**:

`--cluster CLUSTER`
:   The name or ID of the cluster for which you want to list existing {{site.data.keyword.mon_short}} configurations. To retrieve your cluster name or ID, run `ibmcloud oc clusters`. This value is required.

`--instance LOGGING_INSTANCE`
:   The ID or name of the {{site.data.keyword.mon_full_notm}} service instance for which you want to show the monitoring configuration. To retrieve the name, run `ibmcloud resource service-instances`. This value is required.






