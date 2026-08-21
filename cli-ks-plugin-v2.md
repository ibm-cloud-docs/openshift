---

copyright:
  years: 2024, 2026
lastupdated: "2026-08-21"

keywords: openshift, cli reference, openshift cli, {{site.data.keyword.openshiftlong_notm}}

subcollection: openshift

content-type: cli-docs

---

{{site.data.keyword.attribute-definition-list}}

# {{site.data.keyword.openshiftlong_notm}} CLI reference
{: #kubernetes-service-cli}

Refer to these commands to create and manage {{site.data.keyword.openshiftlong_notm}} clusters.
{: shortdesc}

In the command line, you are notified when updates to the `ibmcloud` CLI and plug-ins are available. Be sure to keep your CLI up-to-date so that you can use all available commands and options.


Prerequisites
{: #ks-cli-prereq}
{: dl}

Install the [{{site.data.keyword.cloud_notm}} CLI](/docs/openshift?topic=openshift-cli-install).
:   See [Getting started with the IBM Cloud CLI](/docs/openshift?topic=openshift-cli-install).

Install the `ks` plug-in.
:   Run the following command:

    ```console
    ibmcloud plugin install ks
    ```
    {: pre}


## ibmcloud oc commands
{: #cli_commands}

The following tables list the `ibmcloud oc` command groups. For a complete list of all `ibmcloud oc` commands as they are structured in the CLI, see the [CLI map](/docs/openshift?topic=openshift-icks_map).
{: shortdesc}

| Command group | Description |
| --- | --- |
| [`ibmcloud oc api`](#api-cli) | View the current API endpoint. |
| [`ibmcloud oc api-key`](#api-key-cli) | View information about the API key for a cluster or reset it to a new key. |
| [`ibmcloud oc credential`](#credential-cli) | Set and unset credentials that allow you to access the IBM Cloud classic infrastructure portfolio through your IBM Cloud account. |
| [`ibmcloud oc infra-permissions`](#infra-permissions-cli) | View information about infrastructure permissions that allow you to access the IBM Cloud classic infrastructure portfolio through your IBM Cloud account. |
| [`ibmcloud oc logging`](#logging-cli) | Forward logs from your cluster. |
| [`ibmcloud oc messages`](#messages-cli) | View the current user messages. |
| [`ibmcloud oc quota`](#quota-cli) | View the quota and limits for cluster-related resources in your IBM Cloud account. |
| [`ibmcloud oc script`](#script-cli) | Rewrite scripts that call IBM Cloud Kubernetes Service plug-in commands. Legacy-structured commands are replaced with beta-structured commands. |
| [`ibmcloud oc subnets`](#subnets-cli) | List available portable subnets in your IBM Cloud infrastructure account. |
| [`ibmcloud oc webhook-create`](#webhook-create-cli) | Register a webhook in a cluster. |
| [`ibmcloud oc vpc`](#vpc-cli) | Get information about VPCs and manage VPC clusters. |
| [`ibmcloud oc flavor`](#flavor-cli) | Getting flavor related information. Flavors determine how much virtual CPU, memory, and disk space is available to each worker node. |
| [`ibmcloud oc cluster`](#cluster-cli) | View and modify cluster and cluster service settings. |
| [`ibmcloud oc ingress`](#ingress-cli) | View and modify Ingress services and settings |
| [`ibmcloud oc kms`](#kms-cli) | View and configure Key Management Service integrations. |
| [`ibmcloud oc versions`](#versions-cli) | List all the container platform versions that are available for IBM Cloud Kubernetes Service clusters. |
| [`ibmcloud oc locations`](#locations-cli) | List supported IBM Cloud Kubernetes Service locations. |
| [`ibmcloud oc nlb-dns`](#nlb-dns-cli) | Create and manage host names for network load balancer (NLB) IP addresses in a cluster and health check monitors for host names. |
| **Beta** [`ibmcloud oc storage`](#storage-cli) | View and modify storage resources. |
| [`ibmcloud oc vlan`](#vlan-cli) | List public and private VLANs for a zone and view the VLAN spanning status. |
| [`ibmcloud oc vni`](#vni-cli) | Attach, detach, and list Virtual Network Interfaces on worker nodes. |
| [`ibmcloud oc worker`](#worker-cli) | View and modify worker nodes for a cluster. |
| [`ibmcloud oc worker-pool`](#worker-pool-cli) | View and modify worker pools for a cluster. |
| [`ibmcloud oc zone`](#zone-cli) | List availability zones and modify the zones attached to a worker pool. |
| [`ibmcloud oc security-group`](#security-group-cli) | Run operations against a security group. |
{: caption="ibmcloud oc CLI command groups" caption-side="bottom"}

## Api commands
{: #api-cli}

View the current API endpoint.
{: shortdesc}


### `ibmcloud oc api`
{: #api-cli}



View the current API endpoint.
{: shortdesc}

```sh
ibmcloud oc api [-q]
```

#### Command options
{: #api-options}


`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #api-examples}

View the current API endpoint

```sh
ibmcloud ks api
```
{: pre}


## Api-key commands
{: #api-key-cli}

View information about the API key for a cluster or reset it to a new key.
{: shortdesc}


### `ibmcloud oc api-key help`
{: #api-key-help-cli}



Show help
{: shortdesc}

```sh
ibmcloud oc api-key help
```


#### Examples
{: #api-key-help-examples}

Show help

```sh
ibmcloud ks api-key help
```
{: pre}


### `ibmcloud oc api-key info`
{: #api-key-info-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} 

View information about the API key owner for a cluster.
{: shortdesc}

```sh
ibmcloud oc api-key info --cluster CLUSTER [--output OUTPUT] [-q]
```

#### Command options
{: #api-key-info-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #api-key-info-examples}

View information about the API key owner for a cluster

```sh
ibmcloud ks api-key info --cluster CLUSTER
```
{: pre}


### `ibmcloud oc api-key reset`
{: #api-key-reset-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} 

Replace the API key for all clusters in the specified region and targeted resource group. If no resource group is targeted the command applies to the default resource group. For more information, see [http://ibm.biz/api-key](http://ibm.biz/api-key).
{: shortdesc}

```sh
ibmcloud oc api-key reset --region REGION [-f] [--output OUTPUT] [-q]
```

#### Command options
{: #api-key-reset-options}


`-f`
:    Force the command to run without user prompts.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.

`--region REGION`
:    Specify the region to target.


#### Examples
{: #api-key-reset-examples}

Replace the API key for all clusters in the specified region and targeted resource group

```sh
ibmcloud ks api-key reset --region REGION
```
{: pre}


## Cluster commands
{: #cluster-cli}

View and modify cluster and cluster service settings.
{: shortdesc}


### `ibmcloud oc cluster addon disable acm`
{: #cluster-addon-disable-acm-cli}



Disable the Red Hat Advanced Cluster Management add-on.
{: shortdesc}

```sh
ibmcloud oc cluster addon disable acm --cluster CLUSTER [-f] [-q]
```

#### Command options
{: #cluster-addon-disable-acm-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #cluster-addon-disable-acm-examples}

Disable the Red Hat Advanced Cluster Management add-on

```sh
ibmcloud ks cluster addon disable acm --cluster CLUSTER
```
{: pre}


### `ibmcloud oc cluster addon disable cluster-autoscaler`
{: #cluster-addon-disable-cluster-autoscaler-cli}



Disable the Cluster Autoscaler add-on.
{: shortdesc}

```sh
ibmcloud oc cluster addon disable cluster-autoscaler --cluster CLUSTER [-f] [-q]
```

#### Command options
{: #cluster-addon-disable-cluster-autoscaler-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #cluster-addon-disable-cluster-autoscaler-examples}

Disable the Cluster Autoscaler add-on

```sh
ibmcloud ks cluster addon disable cluster-autoscaler --cluster CLUSTER
```
{: pre}


### `ibmcloud oc cluster addon disable debug-tool`
{: #cluster-addon-disable-debug-tool-cli}



Disable the Diagnostics and Debug Tool add-on.
{: shortdesc}

```sh
ibmcloud oc cluster addon disable debug-tool --cluster CLUSTER [-f] [-q]
```

#### Command options
{: #cluster-addon-disable-debug-tool-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #cluster-addon-disable-debug-tool-examples}

Disable the Diagnostics and Debug Tool add-on

```sh
ibmcloud ks cluster addon disable debug-tool --cluster CLUSTER
```
{: pre}


### `ibmcloud oc cluster addon disable help`
{: #cluster-addon-disable-help-cli}



Show help
{: shortdesc}

```sh
ibmcloud oc cluster addon disable help
```


#### Examples
{: #cluster-addon-disable-help-examples}

Show help

```sh
ibmcloud ks cluster addon disable help
```
{: pre}


### `ibmcloud oc cluster addon disable hpcs-router`
{: #cluster-addon-disable-hpcs-router-cli}



Disable the HPCS Router Operator add-on for OpenShift.
{: shortdesc}

```sh
ibmcloud oc cluster addon disable hpcs-router --cluster CLUSTER [-f] [-q]
```

#### Command options
{: #cluster-addon-disable-hpcs-router-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #cluster-addon-disable-hpcs-router-examples}

Disable the HPCS Router Operator add-on for OpenShift

```sh
ibmcloud ks cluster addon disable hpcs-router --cluster CLUSTER
```
{: pre}


### `ibmcloud oc cluster addon disable ibm-storage-operator`
{: #cluster-addon-disable-ibm-storage-operator-cli}

The `cluster addon disable ibm-storage-operator` command is a beta feature.
{: beta}



Disable the IBM Cloud Storage Operator add-on.
{: shortdesc}

```sh
ibmcloud oc cluster addon disable ibm-storage-operator --cluster CLUSTER [-f] [-q]
```

#### Command options
{: #cluster-addon-disable-ibm-storage-operator-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #cluster-addon-disable-ibm-storage-operator-examples}

Disable the IBM Cloud Storage Operator add-on

```sh
ibmcloud ks cluster addon disable ibm-storage-operator --cluster CLUSTER
```
{: pre}


### `ibmcloud oc cluster addon disable image-key-synchronizer`
{: #cluster-addon-disable-image-key-synchronizer-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

The IBM Cloud Image Key Synchronizer add-on.
{: shortdesc}

```sh
ibmcloud oc cluster addon disable image-key-synchronizer --cluster CLUSTER [-f] [-q]
```

#### Command options
{: #cluster-addon-disable-image-key-synchronizer-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #cluster-addon-disable-image-key-synchronizer-examples}

The IBM Cloud Image Key Synchronizer add-on

```sh
ibmcloud ks cluster addon disable image-key-synchronizer --cluster CLUSTER
```
{: pre}


### `ibmcloud oc cluster addon disable knative`
{: #cluster-addon-disable-knative-cli}



Disable the Knative serverless framework add-on.
{: shortdesc}

```sh
ibmcloud oc cluster addon disable knative --cluster CLUSTER [-f] [-q]
```

#### Command options
{: #cluster-addon-disable-knative-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #cluster-addon-disable-knative-examples}

Disable the Knative serverless framework add-on

```sh
ibmcloud ks cluster addon disable knative --cluster CLUSTER
```
{: pre}


### `ibmcloud oc cluster addon disable kube-terminal`
{: #cluster-addon-disable-kube-terminal-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

Disable the Kubernetes web terminal add-on.
{: shortdesc}

```sh
ibmcloud oc cluster addon disable kube-terminal --cluster CLUSTER [-f] [-q]
```

#### Command options
{: #cluster-addon-disable-kube-terminal-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #cluster-addon-disable-kube-terminal-examples}

Disable the Kubernetes web terminal add-on

```sh
ibmcloud ks cluster addon disable kube-terminal --cluster CLUSTER
```
{: pre}


### `ibmcloud oc cluster addon disable openshift-data-foundation`
{: #cluster-addon-disable-openshift-data-foundation-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

The Red Hat OpenShift Data Foundation on IBM Cloud add-on
{: shortdesc}

```sh
ibmcloud oc cluster addon disable openshift-data-foundation --cluster CLUSTER [-f] [-q]
```

#### Command options
{: #cluster-addon-disable-openshift-data-foundation-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #cluster-addon-disable-openshift-data-foundation-examples}

The Red Hat OpenShift Data Foundation on IBM Cloud add-on

```sh
ibmcloud ks cluster addon disable openshift-data-foundation --cluster CLUSTER
```
{: pre}


### `ibmcloud oc cluster addon disable static-route`
{: #cluster-addon-disable-static-route-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

Disable the Static Route add-on.
{: shortdesc}

```sh
ibmcloud oc cluster addon disable static-route --cluster CLUSTER [-f] [-q]
```

#### Command options
{: #cluster-addon-disable-static-route-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #cluster-addon-disable-static-route-examples}

Disable the Static Route add-on

```sh
ibmcloud ks cluster addon disable static-route --cluster CLUSTER
```
{: pre}


### `ibmcloud oc cluster addon disable vpc-block-csi-driver`
{: #cluster-addon-disable-vpc-block-csi-driver-cli}

[Classic infrastructure]{: tag-classic-inf} 

Disable the VPC Block Storage CSI Driver add-on.
{: shortdesc}

```sh
ibmcloud oc cluster addon disable vpc-block-csi-driver --cluster CLUSTER [-f] [-q]
```

#### Command options
{: #cluster-addon-disable-vpc-block-csi-driver-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #cluster-addon-disable-vpc-block-csi-driver-examples}

Disable the VPC Block Storage CSI Driver add-on

```sh
ibmcloud ks cluster addon disable vpc-block-csi-driver --cluster CLUSTER
```
{: pre}


### `ibmcloud oc cluster addon enable acm`
{: #cluster-addon-enable-acm-cli}



Enable the Red Hat Advanced Cluster Management add-on.
{: shortdesc}

```sh
ibmcloud oc cluster addon enable acm --cluster CLUSTER [-f] [--param PARAM] [-q] [--version VERSION] [-y]
```

#### Command options
{: #cluster-addon-enable-acm-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`--param PARAM`
:    Specify installation options for the add-on. If no parameters are specified, the default values are used. Review the available options with the `ibmcloud ks cluster addon options` command.

`-q`
:    Do not show the message of the day or update reminders.

`--version VERSION`
:    Specify the version of the add-on to install. If no version is specified, the default version is installed.

`-y`
:    Enable all add-on dependencies.


#### Examples
{: #cluster-addon-enable-acm-examples}

Enable the Red Hat Advanced Cluster Management add-on

```sh
ibmcloud ks cluster addon enable acm --cluster CLUSTER
```
{: pre}


### `ibmcloud oc cluster addon enable cluster-autoscaler`
{: #cluster-addon-enable-cluster-autoscaler-cli}



Enable the Cluster Autoscaler add-on.
{: shortdesc}

```sh
ibmcloud oc cluster addon enable cluster-autoscaler --cluster CLUSTER [-q] [--version VERSION] [-y]
```

#### Command options
{: #cluster-addon-enable-cluster-autoscaler-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`-q`
:    Do not show the message of the day or update reminders.

`--version VERSION`
:    Specify the version of the add-on to install. If no version is specified, the default version is installed.

`-y`
:    Enable all add-on dependencies.


#### Examples
{: #cluster-addon-enable-cluster-autoscaler-examples}

Enable the Cluster Autoscaler add-on

```sh
ibmcloud ks cluster addon enable cluster-autoscaler --cluster CLUSTER
```
{: pre}


### `ibmcloud oc cluster addon enable debug-tool`
{: #cluster-addon-enable-debug-tool-cli}



Enable the Diagnostics and Debug Tool add-on.
{: shortdesc}

```sh
ibmcloud oc cluster addon enable debug-tool --cluster CLUSTER [-q] [--version VERSION] [-y]
```

#### Command options
{: #cluster-addon-enable-debug-tool-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`-q`
:    Do not show the message of the day or update reminders.

`--version VERSION`
:    Specify the version of the add-on to install. If no version is specified, the default version is installed.

`-y`
:    Enable all add-on dependencies.


#### Examples
{: #cluster-addon-enable-debug-tool-examples}

Enable the Diagnostics and Debug Tool add-on

```sh
ibmcloud ks cluster addon enable debug-tool --cluster CLUSTER
```
{: pre}


### `ibmcloud oc cluster addon enable help`
{: #cluster-addon-enable-help-cli}



Show help
{: shortdesc}

```sh
ibmcloud oc cluster addon enable help
```


#### Examples
{: #cluster-addon-enable-help-examples}

Show help

```sh
ibmcloud ks cluster addon enable help
```
{: pre}


### `ibmcloud oc cluster addon enable hpcs-router`
{: #cluster-addon-enable-hpcs-router-cli}



Enable the HPCS Router Operator add-on for OpenShift.
{: shortdesc}

```sh
ibmcloud oc cluster addon enable hpcs-router --cluster CLUSTER [-q] [--version VERSION] [-y]
```

#### Command options
{: #cluster-addon-enable-hpcs-router-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`-q`
:    Do not show the message of the day or update reminders.

`--version VERSION`
:    Specify the version of the add-on to install. If no version is specified, the default version is installed.

`-y`
:    Enable all add-on dependencies.


#### Examples
{: #cluster-addon-enable-hpcs-router-examples}

Enable the HPCS Router Operator add-on for OpenShift

```sh
ibmcloud ks cluster addon enable hpcs-router --cluster CLUSTER
```
{: pre}


### `ibmcloud oc cluster addon enable ibm-storage-operator`
{: #cluster-addon-enable-ibm-storage-operator-cli}

The `cluster addon enable ibm-storage-operator` command is a beta feature.
{: beta}



Enable the IBM Cloud Storage Operator add-on.
{: shortdesc}

```sh
ibmcloud oc cluster addon enable ibm-storage-operator --cluster CLUSTER [-q] [--version VERSION] [-y]
```

#### Command options
{: #cluster-addon-enable-ibm-storage-operator-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`-q`
:    Do not show the message of the day or update reminders.

`--version VERSION`
:    Specify the version of the add-on to install. If no version is specified, the default version is installed.

`-y`
:    Enable all add-on dependencies.


#### Examples
{: #cluster-addon-enable-ibm-storage-operator-examples}

Enable the IBM Cloud Storage Operator add-on

```sh
ibmcloud ks cluster addon enable ibm-storage-operator --cluster CLUSTER
```
{: pre}


### `ibmcloud oc cluster addon enable image-key-synchronizer`
{: #cluster-addon-enable-image-key-synchronizer-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

The IBM Cloud Image Key Synchronizer add-on.
{: shortdesc}

```sh
ibmcloud oc cluster addon enable image-key-synchronizer --cluster CLUSTER [-q] [--version VERSION] [-y]
```

#### Command options
{: #cluster-addon-enable-image-key-synchronizer-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`-q`
:    Do not show the message of the day or update reminders.

`--version VERSION`
:    Specify the version of the add-on to install. If no version is specified, the default version is installed.

`-y`
:    Enable all add-on dependencies.


#### Examples
{: #cluster-addon-enable-image-key-synchronizer-examples}

The IBM Cloud Image Key Synchronizer add-on

```sh
ibmcloud ks cluster addon enable image-key-synchronizer --cluster CLUSTER
```
{: pre}


### `ibmcloud oc cluster addon enable istio-extras`
{: #cluster-addon-enable-istio-extras-cli}

The `cluster addon enable istio-extras` command is deprecated.
{: deprecated}



Enable extra Istio components: Grafana, Jaeger, and Kiali.
{: shortdesc}

```sh
ibmcloud oc cluster addon enable istio-extras --cluster CLUSTER [-q] [--version VERSION] [-y]
```

#### Command options
{: #cluster-addon-enable-istio-extras-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`-q`
:    Do not show the message of the day or update reminders.

`--version VERSION`
:    Specify the version of the add-on to install. If no version is specified, the default version is installed.

`-y`
:    Enable all add-on dependencies.


#### Examples
{: #cluster-addon-enable-istio-extras-examples}

Enable extra Istio components: Grafana, Jaeger, and Kiali

```sh
ibmcloud ks cluster addon enable istio-extras --cluster CLUSTER
```
{: pre}


### `ibmcloud oc cluster addon enable istio-sample-bookinfo`
{: #cluster-addon-enable-istio-sample-bookinfo-cli}

The `cluster addon enable istio-sample-bookinfo` command is deprecated.
{: deprecated}



The BookInfo sample application for Istio.
{: shortdesc}

```sh
ibmcloud oc cluster addon enable istio-sample-bookinfo --cluster CLUSTER [-q] [--version VERSION] [-y]
```

#### Command options
{: #cluster-addon-enable-istio-sample-bookinfo-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`-q`
:    Do not show the message of the day or update reminders.

`--version VERSION`
:    Specify the version of the add-on to install. If no version is specified, the default version is installed.

`-y`
:    Enable all add-on dependencies.


#### Examples
{: #cluster-addon-enable-istio-sample-bookinfo-examples}

The BookInfo sample application for Istio

```sh
ibmcloud ks cluster addon enable istio-sample-bookinfo --cluster CLUSTER
```
{: pre}


### `ibmcloud oc cluster addon enable openshift-data-foundation`
{: #cluster-addon-enable-openshift-data-foundation-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

The Red Hat OpenShift Data Foundation on IBM Cloud add-on
{: shortdesc}

```sh
ibmcloud oc cluster addon enable openshift-data-foundation --cluster CLUSTER [-f] [--param PARAM] [-q] [--version VERSION] [-y]
```

#### Command options
{: #cluster-addon-enable-openshift-data-foundation-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`--param PARAM`
:    Specify installation options for the add-on. If no parameters are specified, the default values are used. Review the available options with the `ibmcloud ks cluster addon options` command.

`-q`
:    Do not show the message of the day or update reminders.

`--version VERSION`
:    Specify the version of the add-on to install. If no version is specified, the default version is installed.

`-y`
:    Enable all add-on dependencies.


#### Examples
{: #cluster-addon-enable-openshift-data-foundation-examples}

The Red Hat OpenShift Data Foundation on IBM Cloud add-on

```sh
ibmcloud ks cluster addon enable openshift-data-foundation --cluster CLUSTER
```
{: pre}


### `ibmcloud oc cluster addon enable static-route`
{: #cluster-addon-enable-static-route-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

Enable the Static Route add-on.
{: shortdesc}

```sh
ibmcloud oc cluster addon enable static-route --cluster CLUSTER [-q] [--version VERSION] [-y]
```

#### Command options
{: #cluster-addon-enable-static-route-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`-q`
:    Do not show the message of the day or update reminders.

`--version VERSION`
:    Specify the version of the add-on to install. If no version is specified, the default version is installed.

`-y`
:    Enable all add-on dependencies.


#### Examples
{: #cluster-addon-enable-static-route-examples}

Enable the Static Route add-on

```sh
ibmcloud ks cluster addon enable static-route --cluster CLUSTER
```
{: pre}


### `ibmcloud oc cluster addon get`
{: #cluster-addon-get-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

View details of an installed add-on.
{: shortdesc}

```sh
ibmcloud oc cluster addon get --addon ADDON --cluster CLUSTER [--output OUTPUT] [-q]
```

#### Command options
{: #cluster-addon-get-options}


`--addon ADDON`
:    The add-on name or ID.

`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #cluster-addon-get-examples}

View details of an installed add-on

```sh
ibmcloud ks cluster addon get --addon ADDON --cluster CLUSTER
```
{: pre}


### `ibmcloud oc cluster addon help`
{: #cluster-addon-help-cli}



Show help
{: shortdesc}

```sh
ibmcloud oc cluster addon help
```


#### Examples
{: #cluster-addon-help-examples}

Show help

```sh
ibmcloud ks cluster addon help
```
{: pre}


### `ibmcloud oc cluster addon ls`
{: #cluster-addon-ls-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

List enabled add-ons.
{: shortdesc}

```sh
ibmcloud oc cluster addon ls --cluster CLUSTER [--output OUTPUT] [-q]
```

#### Command options
{: #cluster-addon-ls-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #cluster-addon-ls-examples}

List enabled add-ons

```sh
ibmcloud ks cluster addon ls --cluster CLUSTER
```
{: pre}


### `ibmcloud oc cluster addon options`
{: #cluster-addon-options-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

View installation options for an add-on.
{: shortdesc}

```sh
ibmcloud oc cluster addon options --addon ADDON [--output OUTPUT] [-q] [--version VERSION]
```

#### Command options
{: #cluster-addon-options-options}


`--addon ADDON`
:    The add-on name or ID.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.

`--version VERSION`
:    Specify an add-on version to display options for. If no version is specified, the default version's options are displayed.


#### Examples
{: #cluster-addon-options-examples}

View installation options for an add-on

```sh
ibmcloud ks cluster addon options --addon ADDON
```
{: pre}


### `ibmcloud oc cluster addon update acm`
{: #cluster-addon-update-acm-cli}



Update the Red Hat Advanced Cluster Management add-on.
{: shortdesc}

```sh
ibmcloud oc cluster addon update acm --cluster CLUSTER [-f] [-q] [--version VERSION] [-y]
```

#### Command options
{: #cluster-addon-update-acm-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`-q`
:    Do not show the message of the day or update reminders.

`--version VERSION`
:    Specify the version of the add-on to install. If no version is specified, the default version is installed.

`-y`
:    Update all add-on dependencies.


#### Examples
{: #cluster-addon-update-acm-examples}

Update the Red Hat Advanced Cluster Management add-on

```sh
ibmcloud ks cluster addon update acm --cluster CLUSTER
```
{: pre}


### `ibmcloud oc cluster addon update alb-oauth-proxy`
{: #cluster-addon-update-alb-oauth-proxy-cli}



Update the ALB OAuth Proxy add-on.
{: shortdesc}

```sh
ibmcloud oc cluster addon update alb-oauth-proxy --cluster CLUSTER [-f] [-q] [--version VERSION] [-y]
```

#### Command options
{: #cluster-addon-update-alb-oauth-proxy-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`-q`
:    Do not show the message of the day or update reminders.

`--version VERSION`
:    Specify the version of the add-on to install. If no version is specified, the default version is installed.

`-y`
:    Update all add-on dependencies.


#### Examples
{: #cluster-addon-update-alb-oauth-proxy-examples}

Update the ALB OAuth Proxy add-on

```sh
ibmcloud ks cluster addon update alb-oauth-proxy --cluster CLUSTER
```
{: pre}


### `ibmcloud oc cluster addon update cluster-autoscaler`
{: #cluster-addon-update-cluster-autoscaler-cli}



Update the Cluster Autoscaler add-on.
{: shortdesc}

```sh
ibmcloud oc cluster addon update cluster-autoscaler --cluster CLUSTER [-f] [-q] [--version VERSION] [-y]
```

#### Command options
{: #cluster-addon-update-cluster-autoscaler-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`-q`
:    Do not show the message of the day or update reminders.

`--version VERSION`
:    Specify the version of the add-on to install. If no version is specified, the default version is installed.

`-y`
:    Update all add-on dependencies.


#### Examples
{: #cluster-addon-update-cluster-autoscaler-examples}

Update the Cluster Autoscaler add-on

```sh
ibmcloud ks cluster addon update cluster-autoscaler --cluster CLUSTER
```
{: pre}


### `ibmcloud oc cluster addon update debug-tool`
{: #cluster-addon-update-debug-tool-cli}



Update the Diagnostics and Debug Tool add-on.
{: shortdesc}

```sh
ibmcloud oc cluster addon update debug-tool --cluster CLUSTER [-f] [-q] [--version VERSION] [-y]
```

#### Command options
{: #cluster-addon-update-debug-tool-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`-q`
:    Do not show the message of the day or update reminders.

`--version VERSION`
:    Specify the version of the add-on to install. If no version is specified, the default version is installed.

`-y`
:    Update all add-on dependencies.


#### Examples
{: #cluster-addon-update-debug-tool-examples}

Update the Diagnostics and Debug Tool add-on

```sh
ibmcloud ks cluster addon update debug-tool --cluster CLUSTER
```
{: pre}


### `ibmcloud oc cluster addon update headlamp`
{: #cluster-addon-update-headlamp-cli}

The `cluster addon update headlamp` command is a beta feature.
{: beta}



Update the Headlamp add-on.
{: shortdesc}

```sh
ibmcloud oc cluster addon update headlamp --cluster CLUSTER [-f] [-q] [--version VERSION] [-y]
```

#### Command options
{: #cluster-addon-update-headlamp-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`-q`
:    Do not show the message of the day or update reminders.

`--version VERSION`
:    Specify the version of the add-on to install. If no version is specified, the default version is installed.

`-y`
:    Update all add-on dependencies.


#### Examples
{: #cluster-addon-update-headlamp-examples}

Update the Headlamp add-on

```sh
ibmcloud ks cluster addon update headlamp --cluster CLUSTER
```
{: pre}


### `ibmcloud oc cluster addon update help`
{: #cluster-addon-update-help-cli}



Show help
{: shortdesc}

```sh
ibmcloud oc cluster addon update help
```


#### Examples
{: #cluster-addon-update-help-examples}

Show help

```sh
ibmcloud ks cluster addon update help
```
{: pre}


### `ibmcloud oc cluster addon update hpcs-router`
{: #cluster-addon-update-hpcs-router-cli}



Update the HPCS Router Operator add-on for OpenShift.
{: shortdesc}

```sh
ibmcloud oc cluster addon update hpcs-router --cluster CLUSTER [-f] [-q] [--version VERSION] [-y]
```

#### Command options
{: #cluster-addon-update-hpcs-router-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`-q`
:    Do not show the message of the day or update reminders.

`--version VERSION`
:    Specify the version of the add-on to install. If no version is specified, the default version is installed.

`-y`
:    Update all add-on dependencies.


#### Examples
{: #cluster-addon-update-hpcs-router-examples}

Update the HPCS Router Operator add-on for OpenShift

```sh
ibmcloud ks cluster addon update hpcs-router --cluster CLUSTER
```
{: pre}


### `ibmcloud oc cluster addon update ibm-storage-operator`
{: #cluster-addon-update-ibm-storage-operator-cli}

The `cluster addon update ibm-storage-operator` command is a beta feature.
{: beta}



Update the IBM Cloud Storage Operator add-on.
{: shortdesc}

```sh
ibmcloud oc cluster addon update ibm-storage-operator --cluster CLUSTER [-f] [-q] [--version VERSION] [-y]
```

#### Command options
{: #cluster-addon-update-ibm-storage-operator-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`-q`
:    Do not show the message of the day or update reminders.

`--version VERSION`
:    Specify the version of the add-on to install. If no version is specified, the default version is installed.

`-y`
:    Update all add-on dependencies.


#### Examples
{: #cluster-addon-update-ibm-storage-operator-examples}

Update the IBM Cloud Storage Operator add-on

```sh
ibmcloud ks cluster addon update ibm-storage-operator --cluster CLUSTER
```
{: pre}


### `ibmcloud oc cluster addon update image-key-synchronizer`
{: #cluster-addon-update-image-key-synchronizer-cli}



Update the Image Key Synchronizer add-on.
{: shortdesc}

```sh
ibmcloud oc cluster addon update image-key-synchronizer --cluster CLUSTER [-f] [-q] [--version VERSION] [-y]
```

#### Command options
{: #cluster-addon-update-image-key-synchronizer-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`-q`
:    Do not show the message of the day or update reminders.

`--version VERSION`
:    Specify the version of the add-on to install. If no version is specified, the default version is installed.

`-y`
:    Update all add-on dependencies.


#### Examples
{: #cluster-addon-update-image-key-synchronizer-examples}

Update the Image Key Synchronizer add-on

```sh
ibmcloud ks cluster addon update image-key-synchronizer --cluster CLUSTER
```
{: pre}


### `ibmcloud oc cluster addon update istio`
{: #cluster-addon-update-istio-cli}



Update the managed Istio add-on.
{: shortdesc}

```sh
ibmcloud oc cluster addon update istio --cluster CLUSTER [-f] [-q] [--version VERSION] [-y]
```

#### Command options
{: #cluster-addon-update-istio-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`-q`
:    Do not show the message of the day or update reminders.

`--version VERSION`
:    Specify the version of the add-on to install. If no version is specified, the default version is installed.

`-y`
:    Update all add-on dependencies.


#### Examples
{: #cluster-addon-update-istio-examples}

Update the managed Istio add-on

```sh
ibmcloud ks cluster addon update istio --cluster CLUSTER
```
{: pre}


### `ibmcloud oc cluster addon update istio-extras`
{: #cluster-addon-update-istio-extras-cli}

The `cluster addon update istio-extras` command is deprecated.
{: deprecated}



Update extra Istio components: Grafana, Jaeger, and Kiali.
{: shortdesc}

```sh
ibmcloud oc cluster addon update istio-extras --cluster CLUSTER [-f] [-q] [--version VERSION] [-y]
```

#### Command options
{: #cluster-addon-update-istio-extras-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`-q`
:    Do not show the message of the day or update reminders.

`--version VERSION`
:    Specify the version of the add-on to install. If no version is specified, the default version is installed.

`-y`
:    Update all add-on dependencies.


#### Examples
{: #cluster-addon-update-istio-extras-examples}

Update extra Istio components: Grafana, Jaeger, and Kiali

```sh
ibmcloud ks cluster addon update istio-extras --cluster CLUSTER
```
{: pre}


### `ibmcloud oc cluster addon update istio-sample-bookinfo`
{: #cluster-addon-update-istio-sample-bookinfo-cli}

The `cluster addon update istio-sample-bookinfo` command is deprecated.
{: deprecated}



Update the BookInfo sample application for Istio.
{: shortdesc}

```sh
ibmcloud oc cluster addon update istio-sample-bookinfo --cluster CLUSTER [-f] [-q] [--version VERSION] [-y]
```

#### Command options
{: #cluster-addon-update-istio-sample-bookinfo-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`-q`
:    Do not show the message of the day or update reminders.

`--version VERSION`
:    Specify the version of the add-on to install. If no version is specified, the default version is installed.

`-y`
:    Update all add-on dependencies.


#### Examples
{: #cluster-addon-update-istio-sample-bookinfo-examples}

Update the BookInfo sample application for Istio

```sh
ibmcloud ks cluster addon update istio-sample-bookinfo --cluster CLUSTER
```
{: pre}


### `ibmcloud oc cluster addon update knative`
{: #cluster-addon-update-knative-cli}



Update the Knative serverless framework add-on.
{: shortdesc}

```sh
ibmcloud oc cluster addon update knative --cluster CLUSTER [-f] [-q] [--version VERSION] [-y]
```

#### Command options
{: #cluster-addon-update-knative-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`-q`
:    Do not show the message of the day or update reminders.

`--version VERSION`
:    Specify the version of the add-on to install. If no version is specified, the default version is installed.

`-y`
:    Update all add-on dependencies.


#### Examples
{: #cluster-addon-update-knative-examples}

Update the Knative serverless framework add-on

```sh
ibmcloud ks cluster addon update knative --cluster CLUSTER
```
{: pre}


### `ibmcloud oc cluster addon update kube-terminal`
{: #cluster-addon-update-kube-terminal-cli}



Update the Kubernetes web terminal add-on.
{: shortdesc}

```sh
ibmcloud oc cluster addon update kube-terminal --cluster CLUSTER [-f] [-q] [--version VERSION] [-y]
```

#### Command options
{: #cluster-addon-update-kube-terminal-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`-q`
:    Do not show the message of the day or update reminders.

`--version VERSION`
:    Specify the version of the add-on to install. If no version is specified, the default version is installed.

`-y`
:    Update all add-on dependencies.


#### Examples
{: #cluster-addon-update-kube-terminal-examples}

Update the Kubernetes web terminal add-on

```sh
ibmcloud ks cluster addon update kube-terminal --cluster CLUSTER
```
{: pre}


### `ibmcloud oc cluster addon update openshift-data-foundation`
{: #cluster-addon-update-openshift-data-foundation-cli}



Update the OpenShift Data Foundation add-on.
{: shortdesc}

```sh
ibmcloud oc cluster addon update openshift-data-foundation --cluster CLUSTER [-f] [-q] [--version VERSION] [-y]
```

#### Command options
{: #cluster-addon-update-openshift-data-foundation-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`-q`
:    Do not show the message of the day or update reminders.

`--version VERSION`
:    Specify the version of the add-on to install. If no version is specified, the default version is installed.

`-y`
:    Update all add-on dependencies.


#### Examples
{: #cluster-addon-update-openshift-data-foundation-examples}

Update the OpenShift Data Foundation add-on

```sh
ibmcloud ks cluster addon update openshift-data-foundation --cluster CLUSTER
```
{: pre}


### `ibmcloud oc cluster addon update static-route`
{: #cluster-addon-update-static-route-cli}



Update the Static Route add-on.
{: shortdesc}

```sh
ibmcloud oc cluster addon update static-route --cluster CLUSTER [-f] [-q] [--version VERSION] [-y]
```

#### Command options
{: #cluster-addon-update-static-route-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`-q`
:    Do not show the message of the day or update reminders.

`--version VERSION`
:    Specify the version of the add-on to install. If no version is specified, the default version is installed.

`-y`
:    Update all add-on dependencies.


#### Examples
{: #cluster-addon-update-static-route-examples}

Update the Static Route add-on

```sh
ibmcloud ks cluster addon update static-route --cluster CLUSTER
```
{: pre}


### `ibmcloud oc cluster addon update vpc-block-csi-driver`
{: #cluster-addon-update-vpc-block-csi-driver-cli}



Update the VPC Block Storage CSI Driver add-on.
{: shortdesc}

```sh
ibmcloud oc cluster addon update vpc-block-csi-driver --cluster CLUSTER [-f] [-q] [--version VERSION] [-y]
```

#### Command options
{: #cluster-addon-update-vpc-block-csi-driver-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`-q`
:    Do not show the message of the day or update reminders.

`--version VERSION`
:    Specify the version of the add-on to install. If no version is specified, the default version is installed.

`-y`
:    Update all add-on dependencies.


#### Examples
{: #cluster-addon-update-vpc-block-csi-driver-examples}

Update the VPC Block Storage CSI Driver add-on

```sh
ibmcloud ks cluster addon update vpc-block-csi-driver --cluster CLUSTER
```
{: pre}


### `ibmcloud oc cluster addon versions`
{: #cluster-addon-versions-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

List supported versions for managed add-ons.
{: shortdesc}

```sh
ibmcloud oc cluster addon versions [--addon ADDON] [--offering OFFERING] [--output OUTPUT] [-q] [--show-defaults]
```

#### Command options
{: #cluster-addon-versions-options}


`--addon ADDON`
:    Specify an add-on name to filter versions for.

`--offering OFFERING`
:    Specify an offering to filter versions for. Accepted values: `kubernetes`, `openshift`, `openshift-vs`

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.

`--show-defaults`
:    Show the default version columns in the output.


#### Examples
{: #cluster-addon-versions-examples}

List supported versions for managed add-ons

```sh
ibmcloud ks cluster addon versions
```
{: pre}


### `ibmcloud oc cluster ca create`
{: #cluster-ca-create-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

Create a CA certificate for your cluster. Then, you must rotate the previous certificates to use the new certificates.
{: shortdesc}

```sh
ibmcloud oc cluster ca create --cluster CLUSTER [-f] [-q]
```

#### Command options
{: #cluster-ca-create-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #cluster-ca-create-examples}

Create a CA certificate for your cluster

```sh
ibmcloud ks cluster ca create --cluster CLUSTER
```
{: pre}


### `ibmcloud oc cluster ca get`
{: #cluster-ca-get-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

View the details of a cluster's CA certificate.
{: shortdesc}

```sh
ibmcloud oc cluster ca get --cluster CLUSTER [--output OUTPUT] [-q]
```

#### Command options
{: #cluster-ca-get-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #cluster-ca-get-examples}

View the details of a cluster's CA certificate

```sh
ibmcloud ks cluster ca get --cluster CLUSTER
```
{: pre}


### `ibmcloud oc cluster ca help`
{: #cluster-ca-help-cli}



Show help
{: shortdesc}

```sh
ibmcloud oc cluster ca help
```


#### Examples
{: #cluster-ca-help-examples}

Show help

```sh
ibmcloud ks cluster ca help
```
{: pre}


### `ibmcloud oc cluster ca rotate`
{: #cluster-ca-rotate-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

Rotate the CA certificates of a cluster, which requires that you previously created CA certificates. Rotating invalidates the previous certificates and refreshes the API server of the cluster.
{: shortdesc}

```sh
ibmcloud oc cluster ca rotate --cluster CLUSTER [-f] [-q]
```

#### Command options
{: #cluster-ca-rotate-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #cluster-ca-rotate-examples}

Rotate the CA certificates of a cluster, which requires that you previously created CA certificates

```sh
ibmcloud ks cluster ca rotate --cluster CLUSTER
```
{: pre}


### `ibmcloud oc cluster ca status`
{: #cluster-ca-status-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

View the rotation status of CA certificates for a cluster.
{: shortdesc}

```sh
ibmcloud oc cluster ca status --cluster CLUSTER [-q]
```

#### Command options
{: #cluster-ca-status-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #cluster-ca-status-examples}

View the rotation status of CA certificates for a cluster

```sh
ibmcloud ks cluster ca status --cluster CLUSTER
```
{: pre}


### `ibmcloud oc cluster config`
{: #cluster-config-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

Download the Kubernetes configuration files and certificates to connect to your cluster by using kubectl commands.
{: shortdesc}

```sh
ibmcloud oc cluster config --cluster CLUSTER [--admin] [--endpoint ENDPOINT] [--network] [--output OUTPUT] [-q] [--skip-rbac]
```

#### Command options
{: #cluster-config-options}


`--admin`
:    Retrieve administrator certificates and PEM keys.

`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`--endpoint ENDPOINT`
:    The server URL to use for the cluster context. If you do not include this flag, the default cluster service endpoint is used. For more info, see [https://ibm.biz/context-kube](https://ibm.biz/context-kube) for Kubernetes or [https://ibm.biz/context-ocp](https://ibm.biz/context-ocp) for OpenShift clusters. Accepted values: `private`, `link`, `vpe`

`--network`
:    Retrieve the Calico network config with the Admin config.

`--output OUTPUT`
:    Prints the command output in the provided format and skips `kubeconfig` merges. A zip output does not contain a refresh token. Accepted values: `json`, `yaml`, `zip`

`-q`
:    Do not show the message of the day or update reminders.

`--skip-rbac`
:    Skip adding RBAC roles. Include this option only if you manage your own Kubernetes RBAC roles. If you use IAM service access roles to manage all your RBAC users, do not include this option.


#### Examples
{: #cluster-config-examples}

Download the Kubernetes configuration files and certificates to connect to your cluster by using kubectl commands

```sh
ibmcloud ks cluster config --cluster CLUSTER
```
{: pre}


### `ibmcloud oc cluster create classic`
{: #cluster-create-classic-cli}

[Classic infrastructure]{: tag-classic-inf} 

Create a cluster with worker nodes on classic infrastructure.
{: shortdesc}

```sh
ibmcloud oc cluster create classic --flavor FLAVOR --name NAME --zone ZONE [--disable-disk-encrypt] [--entitlement ENTITLEMENT] [--hardware HARDWARE] [--location LOCATION] [--no-subnet] [--operating-system SYSTEM] [--pod-subnet SUBNET] [--private-service-endpoint] [--private-vlan VLAN] [--public-service-endpoint] [-q] [--service-subnet SUBNET] [--skip-advance-permissions-check] [--sm-group GROUP] [--sm-instance INSTANCE] [--version VERSION] [--workers COUNT] (--private-only | --public-vlan VLAN)
```

#### Command options
{: #cluster-create-classic-options}


`--disable-disk-encrypt`
:    Disable encryption on a worker node.

`--entitlement ENTITLEMENT`
:    Set this flag to `ocp_entitled` only if you use this cluster with a license such as a Cloud Pak that has an OpenShift entitlement.

`--flavor FLAVOR`
:    The flavor of a worker node. To see available flavors, run `ibmcloud ks flavor ls --zone <zone name>` (for public IBM Cloud accounts) or `ibmcloud ks flavor ls` (for IBM Cloud Dedicated accounts).

`--hardware HARDWARE`
:    The level of hardware isolation for your worker node. Use `dedicated` to have available physical resources dedicated to you only, or `shared` to allow physical resources to be shared with other IBM customers. For IBM Cloud Public accounts, the default value is shared. For IBM Cloud Dedicated accounts, dedicated is the only available option.

`--location LOCATION`
:    [Deprecated]{: tag-deprecated} Flag maintained for compatibility with an earlier version. Use the `--zone` flag instead.

`--name NAME`
:    Enter a name for the cluster.

`--no-subnet`
:    Prevent the creation of a portable subnet when creating the cluster. By default, both a public and a private portable subnet are created on the associated VLAN, and this flag prevents that behavior. To add a subnet to the cluster later, run `ibmcloud ks cluster subnet add`.

`--operating-system SYSTEM`
:    Specify the name of the operating system.

`--pod-subnet SUBNET`
:    Specify a custom subnet CIDR to provide private IP addresses for pods. The subnet must be at least `/23` or larger. For more info, see [https://ibm.biz/cluster-create-classic](https://ibm.biz/cluster-create-classic)

`--private-only`
:    Use this flag to prevent a public VLAN from being created. Required only when you specify the `--private-vlan` flag without specifying the `--public-vlan` flag.

`--private-service-endpoint`
:    Enable the private service endpoint to make the master privately accessible.

`--private-vlan VLAN`
:    Conditional: Specify the ID of the private VLAN. To see available VLANs, run `ibmcloud ks vlan ls --zone <zone name>`. If you do not have a private VLAN yet, do not specify this option because one will be automatically created for you. When you specify a private VLAN, you must also specify either the `--public-vlan` flag or the `--private-only` flag.

`--public-service-endpoint`
:    Enable the public service endpoint to make the master publicly accessible.

`--public-vlan VLAN`
:    Conditional: Specify the ID of the public VLAN. To see available VLANs, run `ibmcloud ks vlan ls --zone <zone name>`. If you do not have a public VLAN yet, do not specify this option because one will be automatically created for you.

`-q`
:    Do not show the message of the day or update reminders.

`--service-subnet SUBNET`
:    Specify a custom subnet CIDR to provide private IP addresses for services. The subnet must be at least `/24` or larger. For more info, see [https://ibm.biz/cluster-create-classic](https://ibm.biz/cluster-create-classic). Default value: `172.21.0.0/16`

`--skip-advance-permissions-check`
:    Skip checking for infrastructure permissions before completing this action. Note that if you do not have the correct infrastructure permissions, this action might only partially succeed.

`--sm-group GROUP`
:    The Secret Group ID of the IBM Cloud Secrets Manager instance where your secrets are persisted.

`--sm-instance INSTANCE`
:    The CRN of the IBM Cloud Secrets Manager instance.

`--version VERSION`
:    Specify the Kubernetes or OpenShift version, including at least the major.minor version. If you do not include this flag, the default version is used. To see available versions, run `ibmcloud ks versions`.

`--workers COUNT`
:    The number of cluster worker nodes. Defaults to 1.

`--zone ZONE`
:    Specify the zone for the worker pool in a multizone cluster. To list available zones, run `ibmcloud ks zone ls`.


#### Examples
{: #cluster-create-classic-examples}

Create a cluster with worker nodes on classic infrastructure

```sh
ibmcloud ks cluster create classic --flavor FLAVOR --name NAME --zone ZONE --private-only
```
{: pre}


### `ibmcloud oc cluster create help`
{: #cluster-create-help-cli}



Show help
{: shortdesc}

```sh
ibmcloud oc cluster create help
```


#### Examples
{: #cluster-create-help-examples}

Show help

```sh
ibmcloud ks cluster create help
```
{: pre}


### `ibmcloud oc cluster create satellite`
{: #cluster-create-satellite-cli}



Create an IBM Cloud Satellite cluster on your own infrastructure.
{: shortdesc}

```sh
ibmcloud oc cluster create satellite --location LOCATION --name NAME --version VERSION [--enable-config-admin] [--entitlement ENTITLEMENT] [--host-label LABEL ...] [--infrastructure-topology TOPOLOGY] [--operating-system SYSTEM] [--pod-network-interface-selection SELECTION] [--pod-subnet SUBNET] [--pull-secret SECRET] [-q] [--service-subnet SUBNET] [--sm-group GROUP] [--sm-instance INSTANCE] [--workers COUNT] [--zone ZONE]
```

#### Command options
{: #cluster-create-satellite-options}


`--enable-config-admin`
:    Grant cluster `admin` access to Satellite Config to manage Kubernetes resources.

`--entitlement ENTITLEMENT`
:    Set this flag to `ocp_entitled` only if you use this cluster with a license such as a Cloud Pak that has an OpenShift entitlement.

`--host-label LABEL`, `--hl LABEL`
:    Enter any labels as key-value pairs to identify the host to assign to your Satellite control plane or Red Hat OpenShift cluster. The first host that has this label and is unassigned is automatically assigned to the control plane or cluster. To find available host labels, run `ibmcloud sat host get --host <host_name_or_ID> --location <location_name_or_ID>`.

`--infrastructure-topology TOPOLOGY`
:    Specify whether the cluster should run a single worker node or the default number of worker nodes. To create a single-node cluster, specify `single-replica`. To create a default cluster with multiple worker nodes, specify `highly-available`. The `highly-available` option is applied by default. Accepted values: `single-replica`, `highly-available`

`--location LOCATION`
:    The name or ID of the Satellite location. To find the location ID or name, run `ibmcloud sat location ls`.

`--name NAME`
:    Enter a name for the cluster.

`--operating-system SYSTEM`
:    Specify the name of the operating system.

`--pod-network-interface-selection SELECTION`
:    The method for selecting the node network interface for the internal pod network. This option can be used only if the Satellite location that you specify has Red Hat CoreOS enabled. To provide a direct URL or IP address, specify `can-reach=<url>` or `can-reach=<ip_address>`. To choose a network interface, specify `interface=<network_interface>`.

`--pod-subnet SUBNET`
:    Specify a custom subnet CIDR to provide private IP addresses for pods. The subnet must be at least `/23` or larger. For more info, see [https://ibm.biz/cluster-create-satellite](https://ibm.biz/cluster-create-satellite). Default value: `172.30.0.0/16`

`--pull-secret SECRET`
:    Specify an existing OpenShift entitlement for this cluster's worker nodes by providing your Red Hat account pull secret.

`-q`
:    Do not show the message of the day or update reminders.

`--service-subnet SUBNET`
:    Specify a custom subnet CIDR to provide private IP addresses for services. The subnet must be at least `/24` or larger. For more info, see [https://ibm.biz/cluster-create-satellite](https://ibm.biz/cluster-create-satellite). Default value: `172.21.0.0/16`

`--sm-group GROUP`
:    The Secret Group ID of the IBM Cloud Secrets Manager instance where your secrets are persisted.

`--sm-instance INSTANCE`
:    The CRN of the IBM Cloud Secrets Manager instance.

`--version VERSION`
:    The Red Hat OpenShift on IBM Cloud version, including at least the major.minor version. To see available versions, run `ibmcloud ks versions`.

`--workers COUNT`
:    The number of worker nodes per zone in the default worker pool. Required when `--host-label` is specified.

`--zone ZONE`
:    The zone for the default worker pool in a multizone cluster. To list zones for your location, run `ibmcloud sat location get`.


#### Examples
{: #cluster-create-satellite-examples}

Create an IBM Cloud Satellite cluster on your own infrastructure

```sh
ibmcloud ks cluster create satellite --location LOCATION --name NAME --version VERSION
```
{: pre}


### `ibmcloud oc cluster create vpc-classic`
{: #cluster-create-vpc-classic-cli}



Create a cluster with worker nodes on Virtual Private Cloud (VPC) Gen 1 infrastructure.
{: shortdesc}

```sh
ibmcloud oc cluster create vpc-classic --flavor FLAVOR --name NAME --subnet-id ID --vpc-id ID --zone ZONE [--disable-public-service-endpoint] [--entitlement ENTITLEMENT] [--operating-system SYSTEM] [--pod-subnet SUBNET] [-q] [--service-subnet SUBNET] [--sm-group GROUP] [--sm-instance INSTANCE] [--version VERSION] [--workers COUNT]
```

#### Command options
{: #cluster-create-vpc-classic-options}


`--disable-public-service-endpoint`
:    Disable the public service endpoint to prevent public access to the master.

`--entitlement ENTITLEMENT`
:    Set this flag to `ocp_entitled` only if you use this cluster with a license such as a Cloud Pak that has an OpenShift entitlement.

`--flavor FLAVOR`
:    The flavor of a worker node. To see available flavors, run `ibmcloud ks flavor ls --zone <zone name>` (for public IBM Cloud accounts) or `ibmcloud ks flavor ls` (for IBM Cloud Dedicated accounts).

`--name NAME`
:    Enter a name for the cluster.

`--operating-system SYSTEM`
:    Specify the name of the operating system.

`--pod-subnet SUBNET`
:    Specify a custom subnet CIDR to provide private IP addresses for pods. The subnet must be at least `/23` or larger. For more info, see [https://ibm.biz/cluster-create-vpc](https://ibm.biz/cluster-create-vpc)

`-q`
:    Do not show the message of the day or update reminders.

`--service-subnet SUBNET`
:    Specify a custom subnet CIDR to provide private IP addresses for services. The subnet must be at least `/24` or larger. For more info, see [https://ibm.biz/cluster-create-vpc](https://ibm.biz/cluster-create-vpc). Default value: `172.21.0.0/16`

`--sm-group GROUP`
:    The Secret Group ID of the IBM Cloud Secrets Manager instance where your secrets are persisted.

`--sm-instance INSTANCE`
:    The CRN of the IBM Cloud Secrets Manager instance.

`--subnet-id ID`
:    The VPC subnet to assign the cluster. To list available subnets, run `ibmcloud ks subnets --provider vpc-classic --vpc-id <vpc-id> --zone <vpc-zone>`.

`--version VERSION`
:    Specify the Kubernetes or OpenShift version, including at least the major.minor version. If you do not include this flag, the default version is used. To see available versions, run `ibmcloud ks versions`.

`--vpc-id ID`
:    The ID of the VPC in which to create the worker nodes. To list available IDs, run `ibmcloud ks vpcs`.

`--workers COUNT`
:    The number of worker nodes per zone in the default worker pool.  For OpenShift clusters, you must set this value to at least 2. For Kubernetes clusters, this value is optional.

`--zone ZONE`
:    Specify the zone for the worker pool in a multizone cluster. To list available zones, run `ibmcloud ks zone ls`.


#### Examples
{: #cluster-create-vpc-classic-examples}

Create a cluster with worker nodes on Virtual Private Cloud (VPC) Gen 1 infrastructure

```sh
ibmcloud ks cluster create vpc-classic \
  --flavor FLAVOR \
  --name NAME \
  --subnet-id ID \
  --vpc-id ID \
  --zone ZONE
```
{: pre}


### `ibmcloud oc cluster create vpc-gen2`
{: #cluster-create-vpc-gen2-cli}

[Virtual Private Cloud]{: tag-vpc} 

Create a cluster with worker nodes on Virtual Private Cloud (VPC) Gen 2 infrastructure.
{: shortdesc}

```sh
ibmcloud oc cluster create vpc-gen2 --flavor FLAVOR --name NAME --subnet-id ID --vpc-id ID --zone ZONE [--cluster-security-group GROUP ...] [--cni CNI] [--cos-instance INSTANCE] [--crk CRK] [--disable-outbound-traffic-protection] [--disable-public-service-endpoint] [--entitlement ENTITLEMENT] [--kms-account-id ID] [--kms-instance INSTANCE] [--offering OFFERING] [--operating-system SYSTEM] [--pod-subnet SUBNET] [-q] [--secondary-storage STORAGE] [--service-subnet SUBNET] [--sm-group GROUP] [--sm-instance INSTANCE] [--version VERSION] [--workers COUNT]
```

#### Command options
{: #cluster-create-vpc-gen2-options}


`--cluster-security-group GROUP`
:    Optional. Specify one or more security group IDs to apply to all workers on the cluster. For OpenShift version 4.15 and Kubernetes version 1.30 and later, these security groups are applied in addition to the IBM-managed `kube-clusterID` security group. For earlier cluster versions, specify the `--cluster-security-group cluster` option to apply the `kube-clusterID` security group. If no value is specified, a default set of security groups including `kube-clusterID` are applied.

`--cni CNI`
:    Set the network plugin for the cluster. Calico is set by default. Accepted values: `Calico`, `OVNKubernetes`

`--cos-instance INSTANCE`
:    Required for OpenShift clusters only. The CRN for the standard cloud object storage instance to back up the internal registry in your OpenShift cluster. To list the CRNs of your cloud object storage instances, run `ibmcloud resource service-instances --long --service-name cloud-object-storage`.

`--crk CRK`
:    The ID of the root key in your KMS instance to use for local disk encryption. To list available root keys, run `ibmcloud ks kms crk ls --instance-id <kms_instance>`.

`--disable-outbound-traffic-protection`
:    Include this option to allow public outbound access from the cluster workers. By default, public outbound access is blocked in OpenShift versions 4.15 and later and Kubernetes versions 1.30 and later.

`--disable-public-service-endpoint`
:    Disable the public service endpoint to prevent public access to the master.

`--entitlement ENTITLEMENT`
:    Set this flag to `ocp_entitled` only if you use this cluster with a license such as a Cloud Pak that has an OpenShift entitlement.

`--flavor FLAVOR`
:    The flavor of a worker node. To see available flavors, run `ibmcloud ks flavor ls --zone <zone name>` (for public IBM Cloud accounts) or `ibmcloud ks flavor ls` (for IBM Cloud Dedicated accounts).

`--kms-account-id ID`
:    The ID of the account that contains the KMS instance you want to use for local disk or secret encryption.

`--kms-instance INSTANCE`
:    The ID of the KMS instance to use for local disk encryption. To list available KMS instances, run `ibmcloud ks kms instance ls`.

`--name NAME`
:    Enter a name for the cluster.

`--offering OFFERING`
:    Specify the cluster offering. Accepted values: `kubernetes`, `openshift`, `openshift-vs`

`--operating-system SYSTEM`
:    Specify the name of the operating system.

`--pod-subnet SUBNET`
:    Specify a custom subnet CIDR to provide private IP addresses for pods. The subnet must be at least `/23` or larger. For more info, see [https://ibm.biz/cluster-create-vpc](https://ibm.biz/cluster-create-vpc)

`-q`
:    Do not show the message of the day or update reminders.

`--secondary-storage STORAGE`
:    The secondary storage option for the flavor. To view the secondary storage options that are available for a flavor, run `ibmcloud ks flavor get --provider vpc-gen2 --zone <zone name>`.

`--service-subnet SUBNET`
:    Specify a custom subnet CIDR to provide private IP addresses for services. The subnet must be at least `/24` or larger. For more info, see [https://ibm.biz/cluster-create-vpc](https://ibm.biz/cluster-create-vpc). Default value: `172.21.0.0/16`

`--sm-group GROUP`
:    The Secret Group ID of the IBM Cloud Secrets Manager instance where your secrets are persisted.

`--sm-instance INSTANCE`
:    The CRN of the IBM Cloud Secrets Manager instance.

`--subnet-id ID`
:    The VPC subnet to assign the cluster. To list available subnets, run `ibmcloud ks subnets --provider vpc-gen2 --vpc-id <vpc-id> --zone <vpc-zone>`.

`--version VERSION`
:    Specify the Kubernetes or OpenShift version, including at least the major.minor version. If you do not include this flag, the default version is used. To see available versions, run `ibmcloud ks versions`.

`--vpc-id ID`
:    The ID of the VPC in which to create the worker nodes. To list available IDs, run `ibmcloud ks vpcs`.

`--workers COUNT`
:    The number of worker nodes per zone in the default worker pool.  For OpenShift clusters, you must set this value to at least 2. For Kubernetes clusters, this value is optional.

`--zone ZONE`
:    Specify the zone for the worker pool in a multizone cluster. To list available zones, run `ibmcloud ks zone ls`.


#### Examples
{: #cluster-create-vpc-gen2-examples}

Create a cluster with worker nodes on Virtual Private Cloud (VPC) Gen 2 infrastructure

```sh
ibmcloud ks cluster create vpc-gen2 \
  --flavor FLAVOR \
  --name NAME \
  --subnet-id ID \
  --vpc-id ID \
  --zone ZONE
```
{: pre}


### `ibmcloud oc cluster get`
{: #cluster-get-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

View the details of a cluster.
{: shortdesc}

```sh
ibmcloud oc cluster get --cluster CLUSTER [--output OUTPUT] [-q] [--show-resources]
```

#### Command options
{: #cluster-get-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.

`--show-resources`
:    Show additional cluster resources such as add-ons, VLANs, and subnets.


#### Examples
{: #cluster-get-examples}

View the details of a cluster

```sh
ibmcloud ks cluster get --cluster CLUSTER
```
{: pre}


### `ibmcloud oc cluster help`
{: #cluster-help-cli}



Show help
{: shortdesc}

```sh
ibmcloud oc cluster help
```


#### Examples
{: #cluster-help-examples}

Show help

```sh
ibmcloud ks cluster help
```
{: pre}


### `ibmcloud oc cluster image-security disable`
{: #cluster-image-security-disable-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

Disable image security enforcement in your cluster.
{: shortdesc}

```sh
ibmcloud oc cluster image-security disable --cluster CLUSTER [-q]
```

#### Command options
{: #cluster-image-security-disable-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #cluster-image-security-disable-examples}

Disable image security enforcement in your cluster

```sh
ibmcloud ks cluster image-security disable --cluster CLUSTER
```
{: pre}


### `ibmcloud oc cluster image-security enable`
{: #cluster-image-security-enable-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

Enable image security enforcement in your cluster.
{: shortdesc}

```sh
ibmcloud oc cluster image-security enable --cluster CLUSTER [-f] [-q]
```

#### Command options
{: #cluster-image-security-enable-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #cluster-image-security-enable-examples}

Enable image security enforcement in your cluster

```sh
ibmcloud ks cluster image-security enable --cluster CLUSTER
```
{: pre}


### `ibmcloud oc cluster image-security help`
{: #cluster-image-security-help-cli}



Show help
{: shortdesc}

```sh
ibmcloud oc cluster image-security help
```


#### Examples
{: #cluster-image-security-help-examples}

Show help

```sh
ibmcloud ks cluster image-security help
```
{: pre}


### `ibmcloud oc cluster ls`
{: #cluster-ls-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

List all clusters in your IBM Cloud account.
{: shortdesc}

```sh
ibmcloud oc cluster ls [-l LOCATION ...] [--output OUTPUT] [--provider PROVIDER] [-q]
```

#### Command options
{: #cluster-ls-options}


`-l LOCATION`, `--location LOCATION`
:    A location to filter for. To list available locations, run `ibmcloud ks locations`.

`--output OUTPUT`
:    Prints the command output in the provided format. If you do not include the provider flag, only classic clusters are returned. Accepted values: `json`

`--provider PROVIDER`
:    Filter the list for a specific infrastructure provider. Accepted values: `classic`, `vpc-classic`, `vpc-gen2`, `satellite`

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #cluster-ls-examples}

List all clusters in your IBM Cloud account

```sh
ibmcloud ks cluster ls
```
{: pre}


### `ibmcloud oc cluster master audit-webhook help`
{: #cluster-master-audit-webhook-help-cli}



Show help
{: shortdesc}

```sh
ibmcloud oc cluster master audit-webhook help
```


#### Examples
{: #cluster-master-audit-webhook-help-examples}

Show help

```sh
ibmcloud ks cluster master audit-webhook help
```
{: pre}


### `ibmcloud oc cluster master console-oauth-access get`
{: #cluster-master-console-oauth-access-get-cli}



Get the OpenShift web console and OAuth server access type.
{: shortdesc}

```sh
ibmcloud oc cluster master console-oauth-access get --cluster CLUSTER [--output OUTPUT] [-q]
```

#### Command options
{: #cluster-master-console-oauth-access-get-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #cluster-master-console-oauth-access-get-examples}

Get the OpenShift web console and OAuth server access type

```sh
ibmcloud ks cluster master console-oauth-access get --cluster CLUSTER
```
{: pre}


### `ibmcloud oc cluster master console-oauth-access help`
{: #cluster-master-console-oauth-access-help-cli}



Show help
{: shortdesc}

```sh
ibmcloud oc cluster master console-oauth-access help
```


#### Examples
{: #cluster-master-console-oauth-access-help-examples}

Show help

```sh
ibmcloud ks cluster master console-oauth-access help
```
{: pre}


### `ibmcloud oc cluster master console-oauth-access set`
{: #cluster-master-console-oauth-access-set-cli}



Set the OpenShift web console and OAuth server access type.
{: shortdesc}

```sh
ibmcloud oc cluster master console-oauth-access set --cluster CLUSTER [-f] [-q] [--type TYPE]
```

#### Command options
{: #cluster-master-console-oauth-access-set-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`-q`
:    Do not show the message of the day or update reminders.

`--type TYPE`
:    Specify the OpenShift web console and OAuth server access type. Accepted values: `vpe-gateway`, `legacy`


#### Examples
{: #cluster-master-console-oauth-access-set-examples}

Set the OpenShift web console and OAuth server access type

```sh
ibmcloud ks cluster master console-oauth-access set --cluster CLUSTER
```
{: pre}


### `ibmcloud oc cluster master help`
{: #cluster-master-help-cli}



Show help
{: shortdesc}

```sh
ibmcloud oc cluster master help
```


#### Examples
{: #cluster-master-help-examples}

Show help

```sh
ibmcloud ks cluster master help
```
{: pre}


### `ibmcloud oc cluster master pod-security get`
{: #cluster-master-pod-security-get-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

View the PodSecurity admission configuration for a cluster's Kubernetes API server.
{: shortdesc}

```sh
ibmcloud oc cluster master pod-security get --cluster CLUSTER [--output OUTPUT] [-q]
```

#### Command options
{: #cluster-master-pod-security-get-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #cluster-master-pod-security-get-examples}

View the PodSecurity admission configuration for a cluster's Kubernetes API server

```sh
ibmcloud ks cluster master pod-security get --cluster CLUSTER
```
{: pre}


### `ibmcloud oc cluster master pod-security help`
{: #cluster-master-pod-security-help-cli}



Show help
{: shortdesc}

```sh
ibmcloud oc cluster master pod-security help
```


#### Examples
{: #cluster-master-pod-security-help-examples}

Show help

```sh
ibmcloud ks cluster master pod-security help
```
{: pre}


### `ibmcloud oc cluster master pod-security policy disable`
{: #cluster-master-pod-security-policy-disable-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

Disable PodSecurityPolicy for a cluster's Kubernetes API server.
{: shortdesc}

```sh
ibmcloud oc cluster master pod-security policy disable --cluster CLUSTER [-q]
```

#### Command options
{: #cluster-master-pod-security-policy-disable-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #cluster-master-pod-security-policy-disable-examples}

Disable PodSecurityPolicy for a cluster's Kubernetes API server

```sh
ibmcloud ks cluster master pod-security policy disable --cluster CLUSTER
```
{: pre}


### `ibmcloud oc cluster master pod-security policy enable`
{: #cluster-master-pod-security-policy-enable-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

Enable PodSecurityPolicy for a cluster's Kubernetes API server.
{: shortdesc}

```sh
ibmcloud oc cluster master pod-security policy enable --cluster CLUSTER [-q]
```

#### Command options
{: #cluster-master-pod-security-policy-enable-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #cluster-master-pod-security-policy-enable-examples}

Enable PodSecurityPolicy for a cluster's Kubernetes API server

```sh
ibmcloud ks cluster master pod-security policy enable --cluster CLUSTER
```
{: pre}


### `ibmcloud oc cluster master pod-security policy get`
{: #cluster-master-pod-security-policy-get-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

View the PodSecurityPolicy configuration for a cluster's Kubernetes API server.
{: shortdesc}

```sh
ibmcloud oc cluster master pod-security policy get --cluster CLUSTER [--output OUTPUT] [-q]
```

#### Command options
{: #cluster-master-pod-security-policy-get-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #cluster-master-pod-security-policy-get-examples}

View the PodSecurityPolicy configuration for a cluster's Kubernetes API server

```sh
ibmcloud ks cluster master pod-security policy get --cluster CLUSTER
```
{: pre}


### `ibmcloud oc cluster master pod-security policy help`
{: #cluster-master-pod-security-policy-help-cli}



Show help
{: shortdesc}

```sh
ibmcloud oc cluster master pod-security policy help
```


#### Examples
{: #cluster-master-pod-security-policy-help-examples}

Show help

```sh
ibmcloud ks cluster master pod-security policy help
```
{: pre}


### `ibmcloud oc cluster master pod-security set`
{: #cluster-master-pod-security-set-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

Set and enable the PodSecurity admission configuration for a cluster's Kubernetes API server.
{: shortdesc}

```sh
ibmcloud oc cluster master pod-security set --cluster CLUSTER [--config-file FILE] [-q]
```

#### Command options
{: #cluster-master-pod-security-set-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`--config-file FILE`
:    The filepath of a custom PodSecurity configuration. If not specified, the Kubernetes defaults are applied. For more information, see https://ibm.biz/BdPtUB

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #cluster-master-pod-security-set-examples}

Set and enable the PodSecurity admission configuration for a cluster's Kubernetes API server

```sh
ibmcloud ks cluster master pod-security set --cluster CLUSTER
```
{: pre}


### `ibmcloud oc cluster master pod-security unset`
{: #cluster-master-pod-security-unset-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

Remove the PodSecurity admission configuration for a cluster's Kubernetes API server.
{: shortdesc}

```sh
ibmcloud oc cluster master pod-security unset --cluster CLUSTER [-q]
```

#### Command options
{: #cluster-master-pod-security-unset-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #cluster-master-pod-security-unset-examples}

Remove the PodSecurity admission configuration for a cluster's Kubernetes API server

```sh
ibmcloud ks cluster master pod-security unset --cluster CLUSTER
```
{: pre}


### `ibmcloud oc cluster master private-service-endpoint allowlist add`
{: #cluster-master-private-service-endpoint-allowlist-add-cli}

The `cluster master private-service-endpoint allowlist add` command is deprecated.
{: deprecated}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} 

Add subnets to a cluster's private service endpoint allowlist.
{: shortdesc}

```sh
ibmcloud oc cluster master private-service-endpoint allowlist add --cluster CLUSTER --subnet SUBNET [--subnet SUBNET ...] [-q]
```

#### Command options
{: #cluster-master-private-service-endpoint-allowlist-add-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`-q`
:    Do not show the message of the day or update reminders.

`--subnet SUBNET`
:    Specify the subnet CIDR.


#### Examples
{: #cluster-master-private-service-endpoint-allowlist-add-examples}

Add subnets to a cluster's private service endpoint allowlist

```sh
ibmcloud ks cluster master private-service-endpoint allowlist add --cluster CLUSTER --subnet SUBNET
```
{: pre}


### `ibmcloud oc cluster master private-service-endpoint allowlist disable`
{: #cluster-master-private-service-endpoint-allowlist-disable-cli}

The `cluster master private-service-endpoint allowlist disable` command is deprecated.
{: deprecated}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} 

Disable the allowlist. When disabled, authorized requests to the cluster master from any subnet are permitted through the private service endpoint.
{: shortdesc}

```sh
ibmcloud oc cluster master private-service-endpoint allowlist disable --cluster CLUSTER [-f] [-q]
```

#### Command options
{: #cluster-master-private-service-endpoint-allowlist-disable-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #cluster-master-private-service-endpoint-allowlist-disable-examples}

Disable the allowlist

```sh
ibmcloud ks cluster master private-service-endpoint allowlist disable --cluster CLUSTER
```
{: pre}


### `ibmcloud oc cluster master private-service-endpoint allowlist enable`
{: #cluster-master-private-service-endpoint-allowlist-enable-cli}

The `cluster master private-service-endpoint allowlist enable` command is deprecated.
{: deprecated}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} 

Enable the allowlist. When enabled, only authorized requests to the cluster master from subnets in the allowlist are permitted through the private service endpoint.
{: shortdesc}

```sh
ibmcloud oc cluster master private-service-endpoint allowlist enable --cluster CLUSTER [-f] [-q]
```

#### Command options
{: #cluster-master-private-service-endpoint-allowlist-enable-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #cluster-master-private-service-endpoint-allowlist-enable-examples}

Enable the allowlist

```sh
ibmcloud ks cluster master private-service-endpoint allowlist enable --cluster CLUSTER
```
{: pre}


### `ibmcloud oc cluster master private-service-endpoint allowlist get`
{: #cluster-master-private-service-endpoint-allowlist-get-cli}

The `cluster master private-service-endpoint allowlist get` command is deprecated.
{: deprecated}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} 

Get a cluster's private service endpoint allowlist.
{: shortdesc}

```sh
ibmcloud oc cluster master private-service-endpoint allowlist get --cluster CLUSTER [-q]
```

#### Command options
{: #cluster-master-private-service-endpoint-allowlist-get-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #cluster-master-private-service-endpoint-allowlist-get-examples}

Get a cluster's private service endpoint allowlist

```sh
ibmcloud ks cluster master private-service-endpoint allowlist get --cluster CLUSTER
```
{: pre}


### `ibmcloud oc cluster master private-service-endpoint allowlist help`
{: #cluster-master-private-service-endpoint-allowlist-help-cli}



Show help
{: shortdesc}

```sh
ibmcloud oc cluster master private-service-endpoint allowlist help
```


#### Examples
{: #cluster-master-private-service-endpoint-allowlist-help-examples}

Show help

```sh
ibmcloud ks cluster master private-service-endpoint allowlist help
```
{: pre}


### `ibmcloud oc cluster master private-service-endpoint allowlist rm`
{: #cluster-master-private-service-endpoint-allowlist-rm-cli}

The `cluster master private-service-endpoint allowlist rm` command is deprecated.
{: deprecated}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} 

Remove subnets from a cluster's private service endpoint allowlist.
{: shortdesc}

```sh
ibmcloud oc cluster master private-service-endpoint allowlist rm --cluster CLUSTER --subnet SUBNET [--subnet SUBNET ...] [-f] [-q]
```

#### Command options
{: #cluster-master-private-service-endpoint-allowlist-rm-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`-q`
:    Do not show the message of the day or update reminders.

`--subnet SUBNET`
:    Specify the subnet CIDR.


#### Examples
{: #cluster-master-private-service-endpoint-allowlist-rm-examples}

Remove subnets from a cluster's private service endpoint allowlist

```sh
ibmcloud ks cluster master private-service-endpoint allowlist rm --cluster CLUSTER --subnet SUBNET
```
{: pre}


### `ibmcloud oc cluster master private-service-endpoint enable`
{: #cluster-master-private-service-endpoint-enable-cli}

[Classic infrastructure]{: tag-classic-inf} 

Enable the private service endpoint to make the master privately accessible.
{: shortdesc}

```sh
ibmcloud oc cluster master private-service-endpoint enable --cluster CLUSTER [-f] [-q] [-y]
```

#### Command options
{: #cluster-master-private-service-endpoint-enable-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`-q`
:    Do not show the message of the day or update reminders.

`-y`
:    If the feature requires further action, such as reloading workers or refreshing the cluster master, then perform those actions with no user prompts.


#### Examples
{: #cluster-master-private-service-endpoint-enable-examples}

Enable the private service endpoint to make the master privately accessible

```sh
ibmcloud ks cluster master private-service-endpoint enable --cluster CLUSTER
```
{: pre}


### `ibmcloud oc cluster master private-service-endpoint help`
{: #cluster-master-private-service-endpoint-help-cli}



Show help
{: shortdesc}

```sh
ibmcloud oc cluster master private-service-endpoint help
```


#### Examples
{: #cluster-master-private-service-endpoint-help-examples}

Show help

```sh
ibmcloud ks cluster master private-service-endpoint help
```
{: pre}


### `ibmcloud oc cluster master public-service-endpoint disable`
{: #cluster-master-public-service-endpoint-disable-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} 

Disable the public service endpoint to make the master only privately accessible.
{: shortdesc}

```sh
ibmcloud oc cluster master public-service-endpoint disable --cluster CLUSTER [-f] [-q] [-y]
```

#### Command options
{: #cluster-master-public-service-endpoint-disable-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`-q`
:    Do not show the message of the day or update reminders.

`-y`
:    If the feature requires further action, such as reloading workers or refreshing the cluster master, then perform those actions with no user prompts.


#### Examples
{: #cluster-master-public-service-endpoint-disable-examples}

Disable the public service endpoint to make the master only privately accessible

```sh
ibmcloud ks cluster master public-service-endpoint disable --cluster CLUSTER
```
{: pre}


### `ibmcloud oc cluster master public-service-endpoint enable`
{: #cluster-master-public-service-endpoint-enable-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} 

Enable the public service endpoint to make the master publicly accessible.
{: shortdesc}

```sh
ibmcloud oc cluster master public-service-endpoint enable --cluster CLUSTER [-f] [-q] [-y]
```

#### Command options
{: #cluster-master-public-service-endpoint-enable-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`-q`
:    Do not show the message of the day or update reminders.

`-y`
:    If the feature requires further action, such as reloading workers or refreshing the cluster master, then perform those actions with no user prompts.


#### Examples
{: #cluster-master-public-service-endpoint-enable-examples}

Enable the public service endpoint to make the master publicly accessible

```sh
ibmcloud ks cluster master public-service-endpoint enable --cluster CLUSTER
```
{: pre}


### `ibmcloud oc cluster master public-service-endpoint help`
{: #cluster-master-public-service-endpoint-help-cli}



Show help
{: shortdesc}

```sh
ibmcloud oc cluster master public-service-endpoint help
```


#### Examples
{: #cluster-master-public-service-endpoint-help-examples}

Show help

```sh
ibmcloud ks cluster master public-service-endpoint help
```
{: pre}


### `ibmcloud oc cluster master refresh`
{: #cluster-master-refresh-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

Restart the cluster master nodes to apply new Kubernetes API configuration changes. Your worker nodes, apps, and resources are not modified and continue to run.
{: shortdesc}

```sh
ibmcloud oc cluster master refresh --cluster CLUSTER [-q]
```

#### Command options
{: #cluster-master-refresh-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #cluster-master-refresh-examples}

Restart the cluster master nodes to apply new Kubernetes API configuration changes

```sh
ibmcloud ks cluster master refresh --cluster CLUSTER
```
{: pre}


### `ibmcloud oc cluster master satellite-service-endpoint allowlist add`
{: #cluster-master-satellite-service-endpoint-allowlist-add-cli}



Add subnets to a Satellite cluster's service endpoint allowlist.
{: shortdesc}

```sh
ibmcloud oc cluster master satellite-service-endpoint allowlist add --cluster CLUSTER --subnet SUBNET [--subnet SUBNET ...] [-q]
```

#### Command options
{: #cluster-master-satellite-service-endpoint-allowlist-add-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`-q`
:    Do not show the message of the day or update reminders.

`--subnet SUBNET`
:    Specify the subnet CIDR.


#### Examples
{: #cluster-master-satellite-service-endpoint-allowlist-add-examples}

Add subnets to a Satellite cluster's service endpoint allowlist

```sh
ibmcloud ks cluster master satellite-service-endpoint allowlist add \
  --cluster CLUSTER \
  --subnet SUBNET
```
{: pre}


### `ibmcloud oc cluster master satellite-service-endpoint allowlist disable`
{: #cluster-master-satellite-service-endpoint-allowlist-disable-cli}



Disable the allowlist for a Satellite cluster. When disabled, authorized requests to the cluster master from any subnet are permitted through the Satellite service endpoint.
{: shortdesc}

```sh
ibmcloud oc cluster master satellite-service-endpoint allowlist disable --cluster CLUSTER [-f] [-q]
```

#### Command options
{: #cluster-master-satellite-service-endpoint-allowlist-disable-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #cluster-master-satellite-service-endpoint-allowlist-disable-examples}

Disable the allowlist for a Satellite cluster

```sh
ibmcloud ks cluster master satellite-service-endpoint allowlist disable --cluster CLUSTER
```
{: pre}


### `ibmcloud oc cluster master satellite-service-endpoint allowlist enable`
{: #cluster-master-satellite-service-endpoint-allowlist-enable-cli}



Enable the allowlist for a Satellite cluster. When enabled, only authorized requests to the cluster master from subnets in the allowlist are permitted through the Satellite service endpoint.
{: shortdesc}

```sh
ibmcloud oc cluster master satellite-service-endpoint allowlist enable --cluster CLUSTER [-f] [-q]
```

#### Command options
{: #cluster-master-satellite-service-endpoint-allowlist-enable-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #cluster-master-satellite-service-endpoint-allowlist-enable-examples}

Enable the allowlist for a Satellite cluster

```sh
ibmcloud ks cluster master satellite-service-endpoint allowlist enable --cluster CLUSTER
```
{: pre}


### `ibmcloud oc cluster master satellite-service-endpoint allowlist get`
{: #cluster-master-satellite-service-endpoint-allowlist-get-cli}



Get a Satellite cluster's service endpoint allowlist.
{: shortdesc}

```sh
ibmcloud oc cluster master satellite-service-endpoint allowlist get --cluster CLUSTER [-q]
```

#### Command options
{: #cluster-master-satellite-service-endpoint-allowlist-get-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #cluster-master-satellite-service-endpoint-allowlist-get-examples}

Get a Satellite cluster's service endpoint allowlist

```sh
ibmcloud ks cluster master satellite-service-endpoint allowlist get --cluster CLUSTER
```
{: pre}


### `ibmcloud oc cluster master satellite-service-endpoint allowlist help`
{: #cluster-master-satellite-service-endpoint-allowlist-help-cli}



Show help
{: shortdesc}

```sh
ibmcloud oc cluster master satellite-service-endpoint allowlist help
```


#### Examples
{: #cluster-master-satellite-service-endpoint-allowlist-help-examples}

Show help

```sh
ibmcloud ks cluster master satellite-service-endpoint allowlist help
```
{: pre}


### `ibmcloud oc cluster master satellite-service-endpoint allowlist rm`
{: #cluster-master-satellite-service-endpoint-allowlist-rm-cli}



Remove subnets from a Satellite cluster's service endpoint allowlist.
{: shortdesc}

```sh
ibmcloud oc cluster master satellite-service-endpoint allowlist rm --cluster CLUSTER --subnet SUBNET [--subnet SUBNET ...] [-f] [-q]
```

#### Command options
{: #cluster-master-satellite-service-endpoint-allowlist-rm-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`-q`
:    Do not show the message of the day or update reminders.

`--subnet SUBNET`
:    Specify the subnet CIDR.


#### Examples
{: #cluster-master-satellite-service-endpoint-allowlist-rm-examples}

Remove subnets from a Satellite cluster's service endpoint allowlist

```sh
ibmcloud ks cluster master satellite-service-endpoint allowlist rm --cluster CLUSTER --subnet SUBNET
```
{: pre}


### `ibmcloud oc cluster master satellite-service-endpoint help`
{: #cluster-master-satellite-service-endpoint-help-cli}



Show help
{: shortdesc}

```sh
ibmcloud oc cluster master satellite-service-endpoint help
```


#### Examples
{: #cluster-master-satellite-service-endpoint-help-examples}

Show help

```sh
ibmcloud ks cluster master satellite-service-endpoint help
```
{: pre}


### `ibmcloud oc cluster master update`
{: #cluster-master-update-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

Update the cluster master to the latest version.
{: shortdesc}

```sh
ibmcloud oc cluster master update --cluster CLUSTER [-f] [--force-update] [-q] [--version VERSION]
```

#### Command options
{: #cluster-master-update-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`--force-update`
:    Attempt the update even if the change is greater than two minor versions from the worker node's current version.

`-q`
:    Do not show the message of the day or update reminders.

`--version VERSION`
:    Specify the Kubernetes or OpenShift version, including at least the major.minor version. If you do not include this flag, the default version is used. To see available versions, run `ibmcloud ks versions`.


#### Examples
{: #cluster-master-update-examples}

Update the cluster master to the latest version

```sh
ibmcloud ks cluster master update --cluster CLUSTER
```
{: pre}


### `ibmcloud oc cluster pull-secret apply`
{: #cluster-pull-secret-apply-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

Generate a new image pull secret that stores IAM credentials for the cluster to access images in IBM Cloud Container Registry.
{: shortdesc}

```sh
ibmcloud oc cluster pull-secret apply --cluster CLUSTER [-q]
```

#### Command options
{: #cluster-pull-secret-apply-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #cluster-pull-secret-apply-examples}

Generate a new image pull secret that stores IAM credentials for the cluster to access images in IBM Cloud Container Registry

```sh
ibmcloud ks cluster pull-secret apply --cluster CLUSTER
```
{: pre}


### `ibmcloud oc cluster pull-secret help`
{: #cluster-pull-secret-help-cli}



Show help
{: shortdesc}

```sh
ibmcloud oc cluster pull-secret help
```


#### Examples
{: #cluster-pull-secret-help-examples}

Show help

```sh
ibmcloud ks cluster pull-secret help
```
{: pre}


### `ibmcloud oc cluster rm`
{: #cluster-rm-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

Delete a cluster. All worker nodes, apps, and containers are permanently deleted. This action cannot be undone.
{: shortdesc}

```sh
ibmcloud oc cluster rm --cluster CLUSTER [--delete-openshift-registry-cos-bucket] [--delete-storage] [-f] [-q] [--skip-advance-permissions-check]
```

#### Command options
{: #cluster-rm-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`--delete-openshift-registry-cos-bucket`
:    Remove the COS bucket and the associated service key that holds the OpenShift registry backups on ROKS clusters

`--delete-storage`
:    Force the removal of the cluster's persistent storage. Deleted data cannot be recovered.

`-f`
:    Force the command to run without user prompts. The cluster's persistent storage is not deleted unless the `delete-storage` option is also provided. The COS bucket and it's associated service key is not deleted unless the `delete-openshift-registry-cos-bucket` option is also provided.

`-q`
:    Do not show the message of the day or update reminders.

`--skip-advance-permissions-check`
:    Skip checking for infrastructure permissions before completing this action. Note that if you do not have the correct infrastructure permissions, this action might only partially succeed.


#### Examples
{: #cluster-rm-examples}

Delete a cluster

```sh
ibmcloud ks cluster rm --cluster CLUSTER
```
{: pre}


### `ibmcloud oc cluster service bind`
{: #cluster-service-bind-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

Add an IBM Cloud service to a cluster by binding the service instance to a Kubernetes namespace.
{: shortdesc}

```sh
ibmcloud oc cluster service bind --cluster CLUSTER --namespace NAMESPACE --service SERVICE [-q] (--key KEY | --role ROLE)
```

#### Command options
{: #cluster-service-bind-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`--key KEY`
:    Specify the name or GUID of an existing service key. If you define a service key, you cannot set the `--role` option at the same time.

`-n CLUSTER`, `--namespace NAMESPACE`
:    Specify the Kubernetes namespace.

`-q`
:    Do not show the message of the day or update reminders.

`--role ROLE`
:    Specify the IAM role for the service key. This flag does not work if you specify an existing key to use or for services that are not IAM-enabled, such as Cloud Foundry services.

`--service SERVICE`
:    Specify the name of the service instance. To see a list of available service instances, run `ibmcloud service list` for Cloud Foundry services, or `ibmcloud resource service-instances` for IAM-enabled services.


#### Examples
{: #cluster-service-bind-examples}

Add an IBM Cloud service to a cluster by binding the service instance to a Kubernetes namespace

```sh
ibmcloud ks cluster service bind --cluster CLUSTER --namespace NAMESPACE --service SERVICE --key KEY
```
{: pre}


### `ibmcloud oc cluster service help`
{: #cluster-service-help-cli}



Show help
{: shortdesc}

```sh
ibmcloud oc cluster service help
```


#### Examples
{: #cluster-service-help-examples}

Show help

```sh
ibmcloud ks cluster service help
```
{: pre}


### `ibmcloud oc cluster service ls`
{: #cluster-service-ls-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

List services bound to a Kubernetes namespace.
{: shortdesc}

```sh
ibmcloud oc cluster service ls --cluster CLUSTER [--output OUTPUT] [-q] (--all-namespaces | --namespace NAMESPACE)
```

#### Command options
{: #cluster-service-ls-options}


`--all-namespaces`
:    Include all Kubernetes namespaces.

`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`-n CLUSTER`, `--namespace NAMESPACE`
:    The Kubernetes namespace. Will use the `default` namespace if not specified.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #cluster-service-ls-examples}

List services bound to a Kubernetes namespace

```sh
ibmcloud ks cluster service ls --cluster CLUSTER --all-namespaces
```
{: pre}


### `ibmcloud oc cluster service unbind`
{: #cluster-service-unbind-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

Remove an IBM Cloud service from a cluster by unbinding it from a Kubernetes namespace.
{: shortdesc}

```sh
ibmcloud oc cluster service unbind --cluster CLUSTER --namespace NAMESPACE --service SERVICE [-q]
```

#### Command options
{: #cluster-service-unbind-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`-n CLUSTER`, `--namespace NAMESPACE`
:    Specify the Kubernetes namespace.

`-q`
:    Do not show the message of the day or update reminders.

`--service SERVICE`
:    Specify the name of the service instance. To see a list of available service instances, run `ibmcloud service list` for Cloud Foundry services, or `ibmcloud resource service-instances` for IAM-enabled services.


#### Examples
{: #cluster-service-unbind-examples}

Remove an IBM Cloud service from a cluster by unbinding it from a Kubernetes namespace

```sh
ibmcloud ks cluster service unbind --cluster CLUSTER --namespace NAMESPACE --service SERVICE
```
{: pre}


### `ibmcloud oc cluster subnet add`
{: #cluster-subnet-add-cli}

[Classic infrastructure]{: tag-classic-inf} 

Make an existing public or private portable subnet in your IBM Cloud infrastructure account available to a classic cluster.
{: shortdesc}

```sh
ibmcloud oc cluster subnet add --cluster CLUSTER --subnet-id ID [-q]
```

#### Command options
{: #cluster-subnet-add-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`-q`
:    Do not show the message of the day or update reminders.

`--subnet-id ID`
:    Specify the subnet ID.


#### Examples
{: #cluster-subnet-add-examples}

Make an existing public or private portable subnet in your IBM Cloud infrastructure account available to a classic cluster

```sh
ibmcloud ks cluster subnet add --cluster CLUSTER --subnet-id ID
```
{: pre}


### `ibmcloud oc cluster subnet create`
{: #cluster-subnet-create-cli}

[Classic infrastructure]{: tag-classic-inf} 

Create a portable subnet on your public or private VLAN and make it available to a classic cluster.
{: shortdesc}

```sh
ibmcloud oc cluster subnet create --cluster CLUSTER --size SIZE --vlan VLAN [-q]
```

#### Command options
{: #cluster-subnet-create-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`-q`
:    Do not show the message of the day or update reminders.

`--size SIZE`
:    Specify the size of the portable subnet. The size must be one of 8, 16, 32, 64.

`--vlan VLAN`
:    Specify the public or private VLAN ID.


#### Examples
{: #cluster-subnet-create-examples}

Create a portable subnet on your public or private VLAN and make it available to a classic cluster

```sh
ibmcloud ks cluster subnet create --cluster CLUSTER --size SIZE --vlan VLAN
```
{: pre}


### `ibmcloud oc cluster subnet detach`
{: #cluster-subnet-detach-cli}

[Classic infrastructure]{: tag-classic-inf} 

Detach an existing public or private portable subnet from a classic cluster.
{: shortdesc}

```sh
ibmcloud oc cluster subnet detach --cluster CLUSTER --subnet-id ID [-f] [-q]
```

#### Command options
{: #cluster-subnet-detach-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`-q`
:    Do not show the message of the day or update reminders.

`--subnet-id ID`
:    Specify the subnet ID.


#### Examples
{: #cluster-subnet-detach-examples}

Detach an existing public or private portable subnet from a classic cluster

```sh
ibmcloud ks cluster subnet detach --cluster CLUSTER --subnet-id ID
```
{: pre}


### `ibmcloud oc cluster subnet help`
{: #cluster-subnet-help-cli}



Show help
{: shortdesc}

```sh
ibmcloud oc cluster subnet help
```


#### Examples
{: #cluster-subnet-help-examples}

Show help

```sh
ibmcloud ks cluster subnet help
```
{: pre}


## Credential commands
{: #credential-cli}

Set and unset credentials that allow you to access the IBM Cloud classic infrastructure portfolio through your IBM Cloud account.
{: shortdesc}


### `ibmcloud oc credential get`
{: #credential-get-cli}

[Classic infrastructure]{: tag-classic-inf} 

If you set up your IBM Cloud account to use different credentials to access the IBM Cloud classic infrastructure portfolio, get the infrastructure user name. This command applies to the targeted resource group, or to the default resource group if no resource group is targeted.
{: shortdesc}

```sh
ibmcloud oc credential get --region REGION [--output OUTPUT] [-q]
```

Aliases: `ibmcloud oc credentials-get`

#### Command options
{: #credential-get-options}


`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.

`--region REGION`
:    Specify the region to target.


#### Examples
{: #credential-get-examples}

If you set up your IBM Cloud account to use different credentials to access the IBM Cloud classic infrastructure portfolio, get the infrastructure user name

```sh
ibmcloud ks credential get --region REGION
```
{: pre}


### `ibmcloud oc credential help`
{: #credential-help-cli}



Show help
{: shortdesc}

```sh
ibmcloud oc credential help
```


#### Examples
{: #credential-help-examples}

Show help

```sh
ibmcloud ks credential help
```
{: pre}


### `ibmcloud oc credential set classic`
{: #credential-set-classic-cli}

[Classic infrastructure]{: tag-classic-inf} 

Set credentials that allow you to access the IBM Cloud classic infrastructure portfolio through your IBM Cloud account.
{: shortdesc}

```sh
ibmcloud oc credential set classic --infrastructure-api-key KEY --infrastructure-username USERNAME --region REGION [-q]
```

#### Command options
{: #credential-set-classic-options}


`--infrastructure-api-key KEY`
:    The API key of your IBM Cloud classic infrastructure account.

`--infrastructure-username USERNAME`
:    The user name of your IBM Cloud classic infrastructure account.

`-q`
:    Do not show the message of the day or update reminders.

`--region REGION`
:    Specify the region to target.


#### Examples
{: #credential-set-classic-examples}

Set credentials that allow you to access the IBM Cloud classic infrastructure portfolio through your IBM Cloud account

```sh
ibmcloud ks credential set classic \
  --infrastructure-api-key KEY \
  --infrastructure-username USERNAME \
  --region REGION
```
{: pre}


### `ibmcloud oc credential set help`
{: #credential-set-help-cli}



Show help
{: shortdesc}

```sh
ibmcloud oc credential set help
```


#### Examples
{: #credential-set-help-examples}

Show help

```sh
ibmcloud ks credential set help
```
{: pre}


### `ibmcloud oc credential unset`
{: #credential-unset-cli}

[Classic infrastructure]{: tag-classic-inf} 

Remove the credentials that allow you to access the IBM Cloud classic infrastructure portfolio through your IBM Cloud account. This command applies to the targeted resource group, or to the default resource group if no resource group is targeted.
{: shortdesc}

```sh
ibmcloud oc credential unset --region REGION [-q]
```

Aliases: `ibmcloud oc credentials-unset`

#### Command options
{: #credential-unset-options}


`-q`
:    Do not show the message of the day or update reminders.

`--region REGION`
:    Specify the region to target.


#### Examples
{: #credential-unset-examples}

Remove the credentials that allow you to access the IBM Cloud classic infrastructure portfolio through your IBM Cloud account

```sh
ibmcloud ks credential unset --region REGION
```
{: pre}


## Experimental commands
{: #experimental-cli}

[Expires on 2026-10-21] Experiment with new commands. IMPORTANT: Commands here will retire after the [date] in their description.
{: shortdesc}


### `ibmcloud oc experimental help`
{: #experimental-help-cli}



Show help
{: shortdesc}

```sh
ibmcloud oc experimental help
```


#### Examples
{: #experimental-help-examples}

Show help

```sh
ibmcloud ks experimental help
```
{: pre}


### `ibmcloud oc experimental trusted-profile default get`
{: #experimental-trusted-profile-default-get-cli}



[Expires on 2026-10-21] Get the default trusted profile for clusters created in a resource-group.
{: shortdesc}

```sh
ibmcloud oc experimental trusted-profile default get --region REGION --resource-group GROUP [--output OUTPUT] [-q]
```

#### Command options
{: #experimental-trusted-profile-default-get-options}


`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.

`--region REGION`
:    The region where the resource-group is located.

`--resource-group GROUP`
:    The resource-group whose default trusted profile is to be retrieved.


#### Examples
{: #experimental-trusted-profile-default-get-examples}

[Expires on 2026-10-21] Get the default trusted profile for clusters created in a resource-group

```sh
ibmcloud ks experimental trusted-profile default get --region REGION --resource-group GROUP
```
{: pre}


### `ibmcloud oc experimental trusted-profile default help`
{: #experimental-trusted-profile-default-help-cli}



Show help
{: shortdesc}

```sh
ibmcloud oc experimental trusted-profile default help
```


#### Examples
{: #experimental-trusted-profile-default-help-examples}

Show help

```sh
ibmcloud ks experimental trusted-profile default help
```
{: pre}


### `ibmcloud oc experimental trusted-profile default set`
{: #experimental-trusted-profile-default-set-cli}



[Expires on 2026-10-21] Set the default trusted profile for clusters created in a resource-group.
{: shortdesc}

```sh
ibmcloud oc experimental trusted-profile default set --region REGION --resource-group GROUP --trusted-profile PROFILE [--output OUTPUT] [-q]
```

#### Command options
{: #experimental-trusted-profile-default-set-options}


`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.

`--region REGION`
:    The region where the resource group is located.

`--resource-group GROUP`
:    The resource group ID to set the trusted profile on.

`--trusted-profile PROFILE`
:    The trusted profile ID.


#### Examples
{: #experimental-trusted-profile-default-set-examples}

[Expires on 2026-10-21] Set the default trusted profile for clusters created in a resource-group

```sh
ibmcloud ks experimental trusted-profile default set \
  --region REGION \
  --resource-group GROUP \
  --trusted-profile PROFILE
```
{: pre}


### `ibmcloud oc experimental trusted-profile get`
{: #experimental-trusted-profile-get-cli}



[Expires on 2026-10-21] Get trusted profile for a cluster.
{: shortdesc}

```sh
ibmcloud oc experimental trusted-profile get --cluster CLUSTER [--output OUTPUT] [-q]
```

#### Command options
{: #experimental-trusted-profile-get-options}


`--cluster CLUSTER`
:    The cluster ID to retrieve the trusted profile for.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #experimental-trusted-profile-get-examples}

[Expires on 2026-10-21] Get trusted profile for a cluster

```sh
ibmcloud ks experimental trusted-profile get --cluster CLUSTER
```
{: pre}


### `ibmcloud oc experimental trusted-profile help`
{: #experimental-trusted-profile-help-cli}



Show help
{: shortdesc}

```sh
ibmcloud oc experimental trusted-profile help
```


#### Examples
{: #experimental-trusted-profile-help-examples}

Show help

```sh
ibmcloud ks experimental trusted-profile help
```
{: pre}


### `ibmcloud oc experimental trusted-profile set`
{: #experimental-trusted-profile-set-cli}



[Expires on 2026-10-21] Set trusted profile on a cluster.
{: shortdesc}

```sh
ibmcloud oc experimental trusted-profile set --cluster CLUSTER --trusted-profile PROFILE [--output OUTPUT] [-q]
```

#### Command options
{: #experimental-trusted-profile-set-options}


`--cluster CLUSTER`
:    The cluster ID to set the the trusted profile on.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.

`--trusted-profile PROFILE`
:    The trusted profile ID.


#### Examples
{: #experimental-trusted-profile-set-examples}

[Expires on 2026-10-21] Set trusted profile on a cluster

```sh
ibmcloud ks experimental trusted-profile set --cluster CLUSTER --trusted-profile PROFILE
```
{: pre}


## Flavor commands
{: #flavor-cli}

Getting flavor related information. Flavors determine how much virtual CPU, memory, and disk space is available to each worker node.
{: shortdesc}


### `ibmcloud oc flavor get`
{: #flavor-get-cli}



Get the information of a flavor for a zone and provider.
{: shortdesc}

```sh
ibmcloud oc flavor get --flavor FLAVOR --provider PROVIDER --zone ZONE [--output OUTPUT] [-q]
```

#### Command options
{: #flavor-get-options}


`--flavor FLAVOR`
:    The flavor of a worker node. To see available flavors, run `ibmcloud ks flavor ls --zone <zone name>` (for public IBM Cloud accounts) or `ibmcloud ks flavor ls` (for IBM Cloud Dedicated accounts).

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`--provider PROVIDER`
:    Specify a provider. Available options are `classic`, `vpc-classic` and `vpc-gen2`.

`-q`
:    Do not show the message of the day or update reminders.

`--zone ZONE`
:    Specify the zone to list available flavors for. To list available zones, run `ibmcloud ks zone ls`.


#### Examples
{: #flavor-get-examples}

Get the information of a flavor for a zone and provider

```sh
ibmcloud ks flavor get --flavor FLAVOR --provider PROVIDER --zone ZONE
```
{: pre}


### `ibmcloud oc flavor help`
{: #flavor-help-cli}



Show help
{: shortdesc}

```sh
ibmcloud oc flavor help
```


#### Examples
{: #flavor-help-examples}

Show help

```sh
ibmcloud ks flavor help
```
{: pre}


### `ibmcloud oc flavor ls`
{: #flavor-ls-cli}



List available flavors for a zone.
{: shortdesc}

```sh
ibmcloud oc flavor ls --zone ZONE [--output OUTPUT] [--provider PROVIDER] [-q] [--show-os] [--show-storage]
```

#### Command options
{: #flavor-ls-options}


`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`--provider PROVIDER`
:    The provider type to get the flavors for. Accepted values: `classic`, `vpc-classic`, `vpc-gen2`, `satellite`

`-q`
:    Do not show the message of the day or update reminders.

`--show-os`
:    List supported operating systems.

`--show-storage`
:    Show additional storage drives.

`--zone ZONE`
:    Specify the zone to list available flavors for. To list available zones, run `ibmcloud ks zone ls`.


#### Examples
{: #flavor-ls-examples}

List available flavors for a zone

```sh
ibmcloud ks flavor ls --zone ZONE
```
{: pre}


## Infra-permissions commands
{: #infra-permissions-cli}

View information about infrastructure permissions that allow you to access the IBM Cloud classic infrastructure portfolio through your IBM Cloud account.
{: shortdesc}


### `ibmcloud oc infra-permissions get`
{: #infra-permissions-get-cli}

[Classic infrastructure]{: tag-classic-inf} 

Check whether the credentials that allow access to the IBM Cloud classic infrastructure portfolio for the targeted resource group are missing suggested or required infrastructure permissions. This command applies to the targeted resource group, or to the default resource group if no resource group is targeted.
{: shortdesc}

```sh
ibmcloud oc infra-permissions get [--output OUTPUT] [-q] [--region REGION]
```

#### Command options
{: #infra-permissions-get-options}


`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.

`--region REGION`
:    Specify the region to target. If a region is not already targeted, this argument must be specified. To check if a region is targeted, run `ibmcloud target`.


#### Examples
{: #infra-permissions-get-examples}

Check whether the credentials that allow access to the IBM Cloud classic infrastructure portfolio for the targeted resource group are missing suggested or required infrastructure permissions

```sh
ibmcloud ks infra-permissions get
```
{: pre}


### `ibmcloud oc infra-permissions help`
{: #infra-permissions-help-cli}



Show help
{: shortdesc}

```sh
ibmcloud oc infra-permissions help
```


#### Examples
{: #infra-permissions-help-examples}

Show help

```sh
ibmcloud ks infra-permissions help
```
{: pre}


## Ingress commands
{: #ingress-cli}

View and modify Ingress services and settings
{: shortdesc}


### `ibmcloud oc ingress alb autoscale get`
{: #ingress-alb-autoscale-get-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

See autoscaling status and configuration for Ingress ALBs.
{: shortdesc}

```sh
ibmcloud oc ingress alb autoscale get --alb ALB --cluster CLUSTER [--output OUTPUT] [-q]
```

#### Command options
{: #ingress-alb-autoscale-get-options}


`--alb ALB`
:    The ALB ID. To see available ALB IDs, run `ibmcloud ks ingress alb ls`.

`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #ingress-alb-autoscale-get-examples}

See autoscaling status and configuration for Ingress ALBs

```sh
ibmcloud ks ingress alb autoscale get --alb ALB --cluster CLUSTER
```
{: pre}


### `ibmcloud oc ingress alb autoscale help`
{: #ingress-alb-autoscale-help-cli}



Show help
{: shortdesc}

```sh
ibmcloud oc ingress alb autoscale help
```


#### Examples
{: #ingress-alb-autoscale-help-examples}

Show help

```sh
ibmcloud ks ingress alb autoscale help
```
{: pre}


### `ibmcloud oc ingress alb autoscale set`
{: #ingress-alb-autoscale-set-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

Configure autoscaling for Ingress ALBs.
{: shortdesc}

```sh
ibmcloud oc ingress alb autoscale set --alb ALB --cluster CLUSTER --max-replicas REPLICAS --min-replicas REPLICAS [--output OUTPUT] [-q] (--cpu-average-utilization PERCENT | --custom-metrics-file FILE)
```

#### Command options
{: #ingress-alb-autoscale-set-options}


`--alb ALB`
:    The ALB ID. To see available ALB IDs, run `ibmcloud ks ingress alb ls`.

`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`--cpu-average-utilization PERCENT`
:    Average CPU utilization threshold. Used to dynamically calculate the number of replicas.

`--custom-metrics-file FILE`
:    Path for the custom metric file. See https://ibm.biz/iks-ingress-custom-metrics for more details.

`--max-replicas REPLICAS`
:    The maximum replicas for the given ALB. Ensure you have enough workers.

`--min-replicas REPLICAS`
:    The minimum replicas for the given ALB. Must be greater or equal to 1. (Recommended minimum is 2 for high availability purposes.)

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #ingress-alb-autoscale-set-examples}

Configure autoscaling for Ingress ALBs

```sh
ibmcloud ks ingress alb autoscale set \
  --alb ALB \
  --cluster CLUSTER \
  --max-replicas REPLICAS \
  --min-replicas REPLICAS \
  --cpu-average-utilization PERCENT
```
{: pre}


### `ibmcloud oc ingress alb autoscale unset`
{: #ingress-alb-autoscale-unset-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

Delete the autoscaling configuration for Ingress ALBs.
{: shortdesc}

```sh
ibmcloud oc ingress alb autoscale unset --alb ALB --cluster CLUSTER [-q]
```

#### Command options
{: #ingress-alb-autoscale-unset-options}


`--alb ALB`
:    The ALB ID. To see available ALB IDs, run `ibmcloud ks ingress alb ls`.

`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #ingress-alb-autoscale-unset-examples}

Delete the autoscaling configuration for Ingress ALBs

```sh
ibmcloud ks ingress alb autoscale unset --alb ALB --cluster CLUSTER
```
{: pre}


### `ibmcloud oc ingress alb autoupdate disable`
{: #ingress-alb-autoupdate-disable-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

Disable automatic updates of all Ingress ALB pods in a cluster.
{: shortdesc}

```sh
ibmcloud oc ingress alb autoupdate disable --cluster CLUSTER [-q]
```

#### Command options
{: #ingress-alb-autoupdate-disable-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #ingress-alb-autoupdate-disable-examples}

Disable automatic updates of all Ingress ALB pods in a cluster

```sh
ibmcloud ks ingress alb autoupdate disable --cluster CLUSTER
```
{: pre}


### `ibmcloud oc ingress alb autoupdate enable`
{: #ingress-alb-autoupdate-enable-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

Enable automatic updates of all Ingress ALB pods in a cluster.
{: shortdesc}

```sh
ibmcloud oc ingress alb autoupdate enable --cluster CLUSTER [-q]
```

#### Command options
{: #ingress-alb-autoupdate-enable-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #ingress-alb-autoupdate-enable-examples}

Enable automatic updates of all Ingress ALB pods in a cluster

```sh
ibmcloud ks ingress alb autoupdate enable --cluster CLUSTER
```
{: pre}


### `ibmcloud oc ingress alb autoupdate get`
{: #ingress-alb-autoupdate-get-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

View whether the Ingress ALB pods in a cluster are set to automatically update and whether ALB pods are at the latest version.
{: shortdesc}

```sh
ibmcloud oc ingress alb autoupdate get --cluster CLUSTER [--output OUTPUT] [-q]
```

#### Command options
{: #ingress-alb-autoupdate-get-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #ingress-alb-autoupdate-get-examples}

View whether the Ingress ALB pods in a cluster are set to automatically update and whether ALB pods are at the latest version

```sh
ibmcloud ks ingress alb autoupdate get --cluster CLUSTER
```
{: pre}


### `ibmcloud oc ingress alb autoupdate help`
{: #ingress-alb-autoupdate-help-cli}



Show help
{: shortdesc}

```sh
ibmcloud oc ingress alb autoupdate help
```


#### Examples
{: #ingress-alb-autoupdate-help-examples}

Show help

```sh
ibmcloud ks ingress alb autoupdate help
```
{: pre}


### `ibmcloud oc ingress alb create classic`
{: #ingress-alb-create-classic-cli}

[Classic infrastructure]{: tag-classic-inf} 

Create and enable an Ingress ALB in a classic cluster.
{: shortdesc}

```sh
ibmcloud oc ingress alb create classic --cluster CLUSTER --type TYPE --vlan VLAN --zone ZONE [--ip IP] [-q] [--version VERSION]
```

#### Command options
{: #ingress-alb-create-classic-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`--ip IP`
:    Specify a portable public or private IP address that is available on the `vlan` and in the `zone` of the ALB to be created or enabled.

`-q`
:    Do not show the message of the day or update reminders.

`--type TYPE`
:    Specify the type of ALB. Available options: public, private

`--version VERSION`
:    Specify the ALB image version. To see supported image versions, run `ibmcloud ks ingress alb versions`.

`--vlan VLAN`
:    The VLAN ID. This VLAN must match the ALB `type` and must be in the same `zone` as the ALB that you want to create.

`--zone ZONE`
:    Specify the zone for the worker pool in a multizone cluster. To list available zones, run `ibmcloud ks zone ls`.


#### Examples
{: #ingress-alb-create-classic-examples}

Create and enable an Ingress ALB in a classic cluster

```sh
ibmcloud ks ingress alb create classic --cluster CLUSTER --type TYPE --vlan VLAN --zone ZONE
```
{: pre}


### `ibmcloud oc ingress alb create help`
{: #ingress-alb-create-help-cli}



Show help
{: shortdesc}

```sh
ibmcloud oc ingress alb create help
```


#### Examples
{: #ingress-alb-create-help-examples}

Show help

```sh
ibmcloud ks ingress alb create help
```
{: pre}


### `ibmcloud oc ingress alb create vpc-gen2`
{: #ingress-alb-create-vpc-gen2-cli}

[Virtual Private Cloud]{: tag-vpc} 

Create and enable an Ingress ALB in a VPC Gen 2 cluster.
{: shortdesc}

```sh
ibmcloud oc ingress alb create vpc-gen2 --cluster CLUSTER --type TYPE --zone ZONE [-q] [--version VERSION]
```

#### Command options
{: #ingress-alb-create-vpc-gen2-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`-q`
:    Do not show the message of the day or update reminders.

`--type TYPE`
:    Specify the type of ALB. Available options: public, private

`--version VERSION`
:    Specify the ALB image version. To see supported image versions, run `ibmcloud ks ingress alb versions`.

`--zone ZONE`
:    Specify the zone for the worker pool in a multizone cluster. To list available zones, run `ibmcloud ks zone ls`.


#### Examples
{: #ingress-alb-create-vpc-gen2-examples}

Create and enable an Ingress ALB in a VPC Gen 2 cluster

```sh
ibmcloud ks ingress alb create vpc-gen2 --cluster CLUSTER --type TYPE --zone ZONE
```
{: pre}


### `ibmcloud oc ingress alb disable`
{: #ingress-alb-disable-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

Disable an Ingress ALB in a cluster.
{: shortdesc}

```sh
ibmcloud oc ingress alb disable --alb ALB --cluster CLUSTER [-q]
```

#### Command options
{: #ingress-alb-disable-options}


`--alb ALB`
:    The ALB ID. To see available ALB IDs, run `ibmcloud ks ingress alb ls`.

`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #ingress-alb-disable-examples}

Disable an Ingress ALB in a cluster

```sh
ibmcloud ks ingress alb disable --alb ALB --cluster CLUSTER
```
{: pre}


### `ibmcloud oc ingress alb enable classic`
{: #ingress-alb-enable-classic-cli}

[Classic infrastructure]{: tag-classic-inf} 

Enable an Ingress ALB in a classic cluster.
{: shortdesc}

```sh
ibmcloud oc ingress alb enable classic --alb ALB --cluster CLUSTER [--ip IP] [-q] [--version VERSION]
```

#### Command options
{: #ingress-alb-enable-classic-options}


`--alb ALB`
:    The ALB ID. To see available ALB IDs, run `ibmcloud ks ingress alb ls`.

`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`--ip IP`
:    Specify a portable public or private IP address that is available on the `vlan` and in the `zone` of the ALB to be created or enabled.

`-q`
:    Do not show the message of the day or update reminders.

`--version VERSION`
:    Specify the ALB image version. To see supported image versions, run `ibmcloud ks ingress alb versions`.


#### Examples
{: #ingress-alb-enable-classic-examples}

Enable an Ingress ALB in a classic cluster

```sh
ibmcloud ks ingress alb enable classic --alb ALB --cluster CLUSTER
```
{: pre}


### `ibmcloud oc ingress alb enable help`
{: #ingress-alb-enable-help-cli}



Show help
{: shortdesc}

```sh
ibmcloud oc ingress alb enable help
```


#### Examples
{: #ingress-alb-enable-help-examples}

Show help

```sh
ibmcloud ks ingress alb enable help
```
{: pre}


### `ibmcloud oc ingress alb enable vpc-gen2`
{: #ingress-alb-enable-vpc-gen2-cli}

[Virtual Private Cloud]{: tag-vpc} 

Enable an Ingress ALB in a VPC Gen 2 cluster.
{: shortdesc}

```sh
ibmcloud oc ingress alb enable vpc-gen2 --alb ALB --cluster CLUSTER [-q] [--version VERSION]
```

#### Command options
{: #ingress-alb-enable-vpc-gen2-options}


`--alb ALB`
:    The ALB ID. To see available ALB IDs, run `ibmcloud ks ingress alb ls`.

`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`-q`
:    Do not show the message of the day or update reminders.

`--version VERSION`
:    Specify the ALB image version. To see supported image versions, run `ibmcloud ks ingress alb versions`.


#### Examples
{: #ingress-alb-enable-vpc-gen2-examples}

Enable an Ingress ALB in a VPC Gen 2 cluster

```sh
ibmcloud ks ingress alb enable vpc-gen2 --alb ALB --cluster CLUSTER
```
{: pre}


### `ibmcloud oc ingress alb get`
{: #ingress-alb-get-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

View the details of an Ingress ALB in a cluster.
{: shortdesc}

```sh
ibmcloud oc ingress alb get --alb ALB --cluster CLUSTER [--output OUTPUT] [-q]
```

#### Command options
{: #ingress-alb-get-options}


`--alb ALB`
:    The ALB ID. To see available ALB IDs, run `ibmcloud ks ingress alb ls`.

`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #ingress-alb-get-examples}

View the details of an Ingress ALB in a cluster

```sh
ibmcloud ks ingress alb get --alb ALB --cluster CLUSTER
```
{: pre}


### `ibmcloud oc ingress alb health-checker disable`
{: #ingress-alb-health-checker-disable-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

Disable the Ingress health checker.
{: shortdesc}

```sh
ibmcloud oc ingress alb health-checker disable --cluster CLUSTER [-q]
```

#### Command options
{: #ingress-alb-health-checker-disable-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #ingress-alb-health-checker-disable-examples}

Disable the Ingress health checker

```sh
ibmcloud ks ingress alb health-checker disable --cluster CLUSTER
```
{: pre}


### `ibmcloud oc ingress alb health-checker enable`
{: #ingress-alb-health-checker-enable-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

Enable the Ingress health checker.
{: shortdesc}

```sh
ibmcloud oc ingress alb health-checker enable --cluster CLUSTER [-q]
```

#### Command options
{: #ingress-alb-health-checker-enable-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #ingress-alb-health-checker-enable-examples}

Enable the Ingress health checker

```sh
ibmcloud ks ingress alb health-checker enable --cluster CLUSTER
```
{: pre}


### `ibmcloud oc ingress alb health-checker get`
{: #ingress-alb-health-checker-get-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

View status of the Ingress health checker.
{: shortdesc}

```sh
ibmcloud oc ingress alb health-checker get --cluster CLUSTER [--output OUTPUT] [-q]
```

#### Command options
{: #ingress-alb-health-checker-get-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #ingress-alb-health-checker-get-examples}

View status of the Ingress health checker

```sh
ibmcloud ks ingress alb health-checker get --cluster CLUSTER
```
{: pre}


### `ibmcloud oc ingress alb health-checker help`
{: #ingress-alb-health-checker-help-cli}



Show help
{: shortdesc}

```sh
ibmcloud oc ingress alb health-checker help
```


#### Examples
{: #ingress-alb-health-checker-help-examples}

Show help

```sh
ibmcloud ks ingress alb health-checker help
```
{: pre}


### `ibmcloud oc ingress alb help`
{: #ingress-alb-help-cli}



Show help
{: shortdesc}

```sh
ibmcloud oc ingress alb help
```


#### Examples
{: #ingress-alb-help-examples}

Show help

```sh
ibmcloud ks ingress alb help
```
{: pre}


### `ibmcloud oc ingress alb ls`
{: #ingress-alb-ls-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

List all Ingress ALB IDs in a cluster and whether ALB pods are at the latest version.
{: shortdesc}

```sh
ibmcloud oc ingress alb ls --cluster CLUSTER [--output OUTPUT] [-q]
```

#### Command options
{: #ingress-alb-ls-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #ingress-alb-ls-examples}

List all Ingress ALB IDs in a cluster and whether ALB pods are at the latest version

```sh
ibmcloud ks ingress alb ls --cluster CLUSTER
```
{: pre}


### `ibmcloud oc ingress alb update`
{: #ingress-alb-update-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

Force a one-time update of the pods for individual or all ALBs in the cluster.
{: shortdesc}

```sh
ibmcloud oc ingress alb update --cluster CLUSTER [--alb ALB ...] [--output OUTPUT] [-q] [--version VERSION]
```

#### Command options
{: #ingress-alb-update-options}


`--alb ALB`
:    To update a specific ALB, specify the ALB ID. To see available ALB IDs, run `ibmcloud ks ingress alb ls`. To update more than one ALB, specify one ALB ID in each flag, such as `--alb ID_1 --alb ID_2`. To update all ALBs, do not include this flag.

`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.

`--version VERSION`
:    Specify the ALB image version. To see supported image versions, run `ibmcloud ks ingress alb versions`.


#### Examples
{: #ingress-alb-update-examples}

Force a one-time update of the pods for individual or all ALBs in the cluster

```sh
ibmcloud ks ingress alb update --cluster CLUSTER
```
{: pre}


### `ibmcloud oc ingress alb versions`
{: #ingress-alb-versions-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

List Ingress ALB image versions that are available.
{: shortdesc}

```sh
ibmcloud oc ingress alb versions [--output OUTPUT] [-q] [--region REGION]
```

#### Command options
{: #ingress-alb-versions-options}


`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.

`--region REGION`
:    Specify the region to target.


#### Examples
{: #ingress-alb-versions-examples}

List Ingress ALB image versions that are available

```sh
ibmcloud ks ingress alb versions
```
{: pre}


### `ibmcloud oc ingress domain create`
{: #ingress-domain-create-cli}



Create an Ingress domain for a cluster.
{: shortdesc}

```sh
ibmcloud oc ingress domain create --cluster CLUSTER [--crn CRN] [--domain DOMAIN] [--domain-provider PROVIDER] [--domain-zone ZONE] [--hostname HOSTNAME] [--ip IP] [--is-default] [--output OUTPUT] [-q] [--secret-namespace NAMESPACE]
```

#### Command options
{: #ingress-domain-create-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`--crn CRN`
:    The CRN for the IBM CIS instance.

`--domain DOMAIN`
:    The Ingress domain. To see existing domains, run `ibmcloud ks ingress domain ls`.

`--domain-provider PROVIDER`
:    The DNS provider. The default DNS provider is our internal one. For supported providers see our documentation: https://ibm.biz/containers-ingress-domains

`--domain-zone ZONE`
:    The ZoneID for CIS.

`--hostname HOSTNAME`
:    For VPC clusters. The hostname to register for the domain.

`--ip IP`
:    The IP addresses to register for the domain.

`--is-default`
:    Include this option to set the relevant domain as the default domain for cluster.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.

`--secret-namespace NAMESPACE`
:    The namespace that the TLS secret is created in.


#### Examples
{: #ingress-domain-create-examples}

Create an Ingress domain for a cluster

```sh
ibmcloud ks ingress domain create --cluster CLUSTER
```
{: pre}


### `ibmcloud oc ingress domain default help`
{: #ingress-domain-default-help-cli}



Show help
{: shortdesc}

```sh
ibmcloud oc ingress domain default help
```


#### Examples
{: #ingress-domain-default-help-examples}

Show help

```sh
ibmcloud ks ingress domain default help
```
{: pre}


### `ibmcloud oc ingress domain default replace`
{: #ingress-domain-default-replace-cli}



Change a cluster's default Ingress domain.
{: shortdesc}

```sh
ibmcloud oc ingress domain default replace --cluster CLUSTER --domain DOMAIN [-q]
```

#### Command options
{: #ingress-domain-default-replace-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`--domain DOMAIN`
:    The Ingress domain. To see existing domains, run `ibmcloud ks ingress domain ls`.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #ingress-domain-default-replace-examples}

Change a cluster's default Ingress domain

```sh
ibmcloud ks ingress domain default replace --cluster CLUSTER --domain DOMAIN
```
{: pre}


### `ibmcloud oc ingress domain get`
{: #ingress-domain-get-cli}



View the details of an Ingress domain.
{: shortdesc}

```sh
ibmcloud oc ingress domain get --cluster CLUSTER --domain DOMAIN [--output OUTPUT] [-q]
```

#### Command options
{: #ingress-domain-get-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`--domain DOMAIN`
:    The Ingress domain. To see existing domains, run `ibmcloud ks ingress domain ls`.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #ingress-domain-get-examples}

View the details of an Ingress domain

```sh
ibmcloud ks ingress domain get --cluster CLUSTER --domain DOMAIN
```
{: pre}


### `ibmcloud oc ingress domain help`
{: #ingress-domain-help-cli}



Show help
{: shortdesc}

```sh
ibmcloud oc ingress domain help
```


#### Examples
{: #ingress-domain-help-examples}

Show help

```sh
ibmcloud ks ingress domain help
```
{: pre}


### `ibmcloud oc ingress domain ls`
{: #ingress-domain-ls-cli}



List all Ingress domains for a cluster.
{: shortdesc}

```sh
ibmcloud oc ingress domain ls --cluster CLUSTER [--output OUTPUT] [-q]
```

#### Command options
{: #ingress-domain-ls-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #ingress-domain-ls-examples}

List all Ingress domains for a cluster

```sh
ibmcloud ks ingress domain ls --cluster CLUSTER
```
{: pre}


### `ibmcloud oc ingress domain rm`
{: #ingress-domain-rm-cli}



Remove an Ingress domain from a cluster.
{: shortdesc}

```sh
ibmcloud oc ingress domain rm --cluster CLUSTER --domain DOMAIN [-f] [-q]
```

#### Command options
{: #ingress-domain-rm-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`--domain DOMAIN`
:    The Ingress domain. To see existing domains, run `ibmcloud ks ingress domain ls`.

`-f`
:    Force the command to run without user prompts.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #ingress-domain-rm-examples}

Remove an Ingress domain from a cluster

```sh
ibmcloud ks ingress domain rm --cluster CLUSTER --domain DOMAIN
```
{: pre}


### `ibmcloud oc ingress domain secret help`
{: #ingress-domain-secret-help-cli}



Show help
{: shortdesc}

```sh
ibmcloud oc ingress domain secret help
```


#### Examples
{: #ingress-domain-secret-help-examples}

Show help

```sh
ibmcloud ks ingress domain secret help
```
{: pre}


### `ibmcloud oc ingress domain secret regenerate`
{: #ingress-domain-secret-regenerate-cli}



Regenerate the certificate for an Ingress domain.
{: shortdesc}

```sh
ibmcloud oc ingress domain secret regenerate --cluster CLUSTER --domain DOMAIN [--output OUTPUT] [-q]
```

#### Command options
{: #ingress-domain-secret-regenerate-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`--domain DOMAIN`
:    The Ingress domain. To see existing domains, run `ibmcloud ks ingress domain ls`.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #ingress-domain-secret-regenerate-examples}

Regenerate the certificate for an Ingress domain

```sh
ibmcloud ks ingress domain secret regenerate --cluster CLUSTER --domain DOMAIN
```
{: pre}


### `ibmcloud oc ingress domain secret rm`
{: #ingress-domain-secret-rm-cli}



Delete a secret for an Ingress domain and prevent future renewal of the certificate.
{: shortdesc}

```sh
ibmcloud oc ingress domain secret rm --cluster CLUSTER --domain DOMAIN [-f] [--output OUTPUT] [-q]
```

#### Command options
{: #ingress-domain-secret-rm-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`--domain DOMAIN`
:    The Ingress domain. To see existing domains, run `ibmcloud ks ingress domain ls`.

`-f`
:    Force the command to run without user prompts.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #ingress-domain-secret-rm-examples}

Delete a secret for an Ingress domain and prevent future renewal of the certificate

```sh
ibmcloud ks ingress domain secret rm --cluster CLUSTER --domain DOMAIN
```
{: pre}


### `ibmcloud oc ingress domain update`
{: #ingress-domain-update-cli}



Update an Ingress domain for a cluster. The records passed in will fully replace the current records associated with the domain. Passing in no records will unregister the current records from a domain.
{: shortdesc}

```sh
ibmcloud oc ingress domain update --cluster CLUSTER --domain DOMAIN [--hostname HOSTNAME] [--ip IP] [-q]
```

#### Command options
{: #ingress-domain-update-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`--domain DOMAIN`
:    The Ingress domain. To see existing domains, run `ibmcloud ks ingress domain ls`.

`--hostname HOSTNAME`
:    For VPC clusters. The hostname to register for the domain.

`--ip IP`
:    The IP addresses to register for the domain.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #ingress-domain-update-examples}

Update an Ingress domain for a cluster

```sh
ibmcloud ks ingress domain update --cluster CLUSTER --domain DOMAIN
```
{: pre}


### `ibmcloud oc ingress help`
{: #ingress-help-cli}



Show help
{: shortdesc}

```sh
ibmcloud oc ingress help
```


#### Examples
{: #ingress-help-examples}

Show help

```sh
ibmcloud ks ingress help
```
{: pre}


### `ibmcloud oc ingress instance default help`
{: #ingress-instance-default-help-cli}



Show help
{: shortdesc}

```sh
ibmcloud oc ingress instance default help
```


#### Examples
{: #ingress-instance-default-help-examples}

Show help

```sh
ibmcloud ks ingress instance default help
```
{: pre}


### `ibmcloud oc ingress instance default set`
{: #ingress-instance-default-set-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

Set a registered IBM Cloud Secrets Manager instance as the default. If an existing default instance exists, it is unset.
{: shortdesc}

```sh
ibmcloud oc ingress instance default set --cluster CLUSTER --name NAME [-q] [--secret-group GROUP]
```

#### Command options
{: #ingress-instance-default-set-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`--name NAME`
:    The name of the registered IBM Cloud Secret Manager instance.

`-q`
:    Do not show the message of the day or update reminders.

`--secret-group GROUP`
:    Secret Group ID of the IBM Cloud Secret Manager instance where the secrets are persisted.


#### Examples
{: #ingress-instance-default-set-examples}

Set a registered IBM Cloud Secrets Manager instance as the default

```sh
ibmcloud ks ingress instance default set --cluster CLUSTER --name NAME
```
{: pre}


### `ibmcloud oc ingress instance default unset`
{: #ingress-instance-default-unset-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

Unset a registered IBM Cloud Secrets Manager instance from default.
{: shortdesc}

```sh
ibmcloud oc ingress instance default unset --cluster CLUSTER --name NAME [-q]
```

#### Command options
{: #ingress-instance-default-unset-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`--name NAME`
:    The name of the registered IBM Cloud Secret Manager instance.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #ingress-instance-default-unset-examples}

Unset a registered IBM Cloud Secrets Manager instance from default

```sh
ibmcloud ks ingress instance default unset --cluster CLUSTER --name NAME
```
{: pre}


### `ibmcloud oc ingress instance get`
{: #ingress-instance-get-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

View details of a registered Secrets Manager instance.
{: shortdesc}

```sh
ibmcloud oc ingress instance get --cluster CLUSTER --name NAME [--output OUTPUT] [-q]
```

#### Command options
{: #ingress-instance-get-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`--name NAME`
:    The name of the registered IBM Cloud Secret Manager instance.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #ingress-instance-get-examples}

View details of a registered Secrets Manager instance

```sh
ibmcloud ks ingress instance get --cluster CLUSTER --name NAME
```
{: pre}


### `ibmcloud oc ingress instance help`
{: #ingress-instance-help-cli}



Show help
{: shortdesc}

```sh
ibmcloud oc ingress instance help
```


#### Examples
{: #ingress-instance-help-examples}

Show help

```sh
ibmcloud ks ingress instance help
```
{: pre}


### `ibmcloud oc ingress instance ls`
{: #ingress-instance-ls-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

List registered Secrets Manager instances in your account.
{: shortdesc}

```sh
ibmcloud oc ingress instance ls --cluster CLUSTER [--output OUTPUT] [-q] [--show-deleted]
```

#### Command options
{: #ingress-instance-ls-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.

`--show-deleted`
:    Show IBM Cloud Secret Manager instances that were unregistered from the cluster.


#### Examples
{: #ingress-instance-ls-examples}

List registered Secrets Manager instances in your account

```sh
ibmcloud ks ingress instance ls --cluster CLUSTER
```
{: pre}


### `ibmcloud oc ingress instance register`
{: #ingress-instance-register-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

Register an IBM Cloud Secrets Manager instance to a cluster.
{: shortdesc}

```sh
ibmcloud oc ingress instance register --cluster CLUSTER --crn CRN [--is-default] [-q] [--secret-group GROUP]
```

#### Command options
{: #ingress-instance-register-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`--crn CRN`
:    CRN of the IBM Cloud Secret Manager instance.

`--is-default`
:    Set the IBM Cloud Secrets Manager instance as the default. If an existing default instance exists, it is unset.

`-q`
:    Do not show the message of the day or update reminders.

`--secret-group GROUP`
:    Secret Group ID of the IBM Cloud Secret Manager instance where the secrets are persisted.


#### Examples
{: #ingress-instance-register-examples}

Register an IBM Cloud Secrets Manager instance to a cluster

```sh
ibmcloud ks ingress instance register --cluster CLUSTER --crn CRN
```
{: pre}


### `ibmcloud oc ingress instance unregister`
{: #ingress-instance-unregister-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

Unregister an IBM Cloud Secrets Manager instance from a cluster.
{: shortdesc}

```sh
ibmcloud oc ingress instance unregister --cluster CLUSTER --name NAME [-q]
```

#### Command options
{: #ingress-instance-unregister-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`--name NAME`
:    The name of the registered IBM Cloud Secret Manager instance.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #ingress-instance-unregister-examples}

Unregister an IBM Cloud Secrets Manager instance from a cluster

```sh
ibmcloud ks ingress instance unregister --cluster CLUSTER --name NAME
```
{: pre}


### `ibmcloud oc ingress load-balancer backend help`
{: #ingress-load-balancer-backend-help-cli}



Show help
{: shortdesc}

```sh
ibmcloud oc ingress load-balancer backend help
```


#### Examples
{: #ingress-load-balancer-backend-help-examples}

Show help

```sh
ibmcloud ks ingress load-balancer backend help
```
{: pre}


### `ibmcloud oc ingress load-balancer backend set`
{: #ingress-load-balancer-backend-set-cli}

[Virtual Private Cloud]{: tag-vpc} 

Set the Ingress controller currently exposed by the VPC ALB load balancer.
{: shortdesc}

```sh
ibmcloud oc ingress load-balancer backend set --cluster CLUSTER [--private-backend BACKEND] [--public-backend BACKEND] [-q]
```

#### Command options
{: #ingress-load-balancer-backend-set-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`--private-backend BACKEND`
:    Backend for private load balancer

`--public-backend BACKEND`
:    Backend for public load balancer

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #ingress-load-balancer-backend-set-examples}

Set the Ingress controller currently exposed by the VPC ALB load balancer

```sh
ibmcloud ks ingress load-balancer backend set --cluster CLUSTER
```
{: pre}


### `ibmcloud oc ingress load-balancer get`
{: #ingress-load-balancer-get-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} 

Get the configuration of load balancers that expose Ingress ALBs in your cluster.
{: shortdesc}

```sh
ibmcloud oc ingress load-balancer get --cluster CLUSTER [--output OUTPUT] [-q]
```

#### Command options
{: #ingress-load-balancer-get-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #ingress-load-balancer-get-examples}

Get the configuration of load balancers that expose Ingress ALBs in your cluster

```sh
ibmcloud ks ingress load-balancer get --cluster CLUSTER
```
{: pre}


### `ibmcloud oc ingress load-balancer help`
{: #ingress-load-balancer-help-cli}



Show help
{: shortdesc}

```sh
ibmcloud oc ingress load-balancer help
```


#### Examples
{: #ingress-load-balancer-help-examples}

Show help

```sh
ibmcloud ks ingress load-balancer help
```
{: pre}


### `ibmcloud oc ingress load-balancer proxy-protocol disable`
{: #ingress-load-balancer-proxy-protocol-disable-cli}

[Virtual Private Cloud]{: tag-vpc} 

Disable the PROXY protocol on Ingress ALBs.
{: shortdesc}

```sh
ibmcloud oc ingress load-balancer proxy-protocol disable --cluster CLUSTER [-f] [-q]
```

#### Command options
{: #ingress-load-balancer-proxy-protocol-disable-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #ingress-load-balancer-proxy-protocol-disable-examples}

Disable the PROXY protocol on Ingress ALBs

```sh
ibmcloud ks ingress load-balancer proxy-protocol disable --cluster CLUSTER
```
{: pre}


### `ibmcloud oc ingress load-balancer proxy-protocol enable`
{: #ingress-load-balancer-proxy-protocol-enable-cli}

[Virtual Private Cloud]{: tag-vpc} 

Enable the PROXY protocol so that client connection information is passed in request headers to ALBs.
{: shortdesc}

```sh
ibmcloud oc ingress load-balancer proxy-protocol enable --cluster CLUSTER [--cidr CIDR ...] [-f] [-q]
```

#### Command options
{: #ingress-load-balancer-proxy-protocol-enable-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`--cidr CIDR`
:    The IP address ranges of your load balancers in CIDR format. PROXY headers that are forwarded by load balancers in other IP ranges are not processed.

`-f`
:    Force the command to run without user prompts.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #ingress-load-balancer-proxy-protocol-enable-examples}

Enable the PROXY protocol so that client connection information is passed in request headers to ALBs

```sh
ibmcloud ks ingress load-balancer proxy-protocol enable --cluster CLUSTER
```
{: pre}


### `ibmcloud oc ingress load-balancer proxy-protocol help`
{: #ingress-load-balancer-proxy-protocol-help-cli}



Show help
{: shortdesc}

```sh
ibmcloud oc ingress load-balancer proxy-protocol help
```


#### Examples
{: #ingress-load-balancer-proxy-protocol-help-examples}

Show help

```sh
ibmcloud ks ingress load-balancer proxy-protocol help
```
{: pre}


### `ibmcloud oc ingress secret create`
{: #ingress-secret-create-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

Create an Ingress secret in a cluster for a secret stored in IBM Cloud Secret Manager.
{: shortdesc}

```sh
ibmcloud oc ingress secret create --cluster CLUSTER --name NAME [--cert-crn CRN] [--field FIELD] [--namespace NAMESPACE] [--persist] [-q] [--type TYPE]
```

#### Command options
{: #ingress-secret-create-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`--cert-crn CRN`
:    The certificate CRN.

`--field FIELD`
:    The secret CRN to include as a field. To pull in the secret without specifying the name, use `--field <crn>`. To specify the field name, use `--field name=<crn>`. To use the IBM Cloud Secrets Manager secret as the prefix, use `--field prefix=<crn>`.

`-n CLUSTER`, `--namespace NAMESPACE`
:    Specify the Kubernetes namespace.

`--name NAME`
:    A name for the Ingress secret that is created in the cluster.

`--persist`
:    Persist the secret in the cluster so that it cannot be deleted.

`-q`
:    Do not show the message of the day or update reminders.

`--type TYPE`
:    The Ingress secret type. Can be TLS or Opaque. If no option is specified, TLS is applied by default.


#### Examples
{: #ingress-secret-create-examples}

Create an Ingress secret in a cluster for a secret stored in IBM Cloud Secret Manager

```sh
ibmcloud ks ingress secret create --cluster CLUSTER --name NAME
```
{: pre}


### `ibmcloud oc ingress secret field add`
{: #ingress-secret-field-add-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

Add fields to an existing Ingress secret.
{: shortdesc}

```sh
ibmcloud oc ingress secret field add --cluster CLUSTER --name NAME --namespace NAMESPACE [--field FIELD] [-q]
```

#### Command options
{: #ingress-secret-field-add-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`--field FIELD`
:    The secret CRN to include as a field. To pull in the secret without specifying the name, use `--field <crn>`. To specify the field name, use `--field name=<crn>`. To use the IBM Cloud Secrets Manager secret as the prefix, use `--field prefix=<crn>`.

`-n CLUSTER`, `--namespace NAMESPACE`
:    Specify the Kubernetes namespace.

`--name NAME`
:    A name for the Ingress secret that is created in the cluster.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #ingress-secret-field-add-examples}

Add fields to an existing Ingress secret

```sh
ibmcloud ks ingress secret field add --cluster CLUSTER --name NAME --namespace NAMESPACE
```
{: pre}


### `ibmcloud oc ingress secret field help`
{: #ingress-secret-field-help-cli}



Show help
{: shortdesc}

```sh
ibmcloud oc ingress secret field help
```


#### Examples
{: #ingress-secret-field-help-examples}

Show help

```sh
ibmcloud ks ingress secret field help
```
{: pre}


### `ibmcloud oc ingress secret field ls`
{: #ingress-secret-field-ls-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

View the fields of an Ingress secret.
{: shortdesc}

```sh
ibmcloud oc ingress secret field ls --cluster CLUSTER --name NAME --namespace NAMESPACE [--output OUTPUT] [-q] [--show-crn]
```

#### Command options
{: #ingress-secret-field-ls-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`-n CLUSTER`, `--namespace NAMESPACE`
:    Specify the Kubernetes namespace.

`--name NAME`
:    A name for the Ingress secret that is created in the cluster.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.

`--show-crn`
:    Show CRN value of secret.


#### Examples
{: #ingress-secret-field-ls-examples}

View the fields of an Ingress secret

```sh
ibmcloud ks ingress secret field ls --cluster CLUSTER --name NAME --namespace NAMESPACE
```
{: pre}


### `ibmcloud oc ingress secret field rm`
{: #ingress-secret-field-rm-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

Remove fields from an existing Ingress secret.
{: shortdesc}

```sh
ibmcloud oc ingress secret field rm --cluster CLUSTER --name NAME --namespace NAMESPACE [--field-name NAME] [-q]
```

#### Command options
{: #ingress-secret-field-rm-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`--field-name NAME`
:    The name of the field to remove from the secret.

`-n CLUSTER`, `--namespace NAMESPACE`
:    Specify the Kubernetes namespace.

`--name NAME`
:    A name for the Ingress secret that is created in the cluster.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #ingress-secret-field-rm-examples}

Remove fields from an existing Ingress secret

```sh
ibmcloud ks ingress secret field rm --cluster CLUSTER --name NAME --namespace NAMESPACE
```
{: pre}


### `ibmcloud oc ingress secret get`
{: #ingress-secret-get-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

View the details of an Ingress secret.
{: shortdesc}

```sh
ibmcloud oc ingress secret get --cluster CLUSTER --name NAME --namespace NAMESPACE [--output OUTPUT] [-q]
```

#### Command options
{: #ingress-secret-get-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`-n CLUSTER`, `--namespace NAMESPACE`
:    Specify the Kubernetes namespace.

`--name NAME`
:    A name for the Ingress secret that is created in the cluster.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #ingress-secret-get-examples}

View the details of an Ingress secret

```sh
ibmcloud ks ingress secret get --cluster CLUSTER --name NAME --namespace NAMESPACE
```
{: pre}


### `ibmcloud oc ingress secret help`
{: #ingress-secret-help-cli}



Show help
{: shortdesc}

```sh
ibmcloud oc ingress secret help
```


#### Examples
{: #ingress-secret-help-examples}

Show help

```sh
ibmcloud ks ingress secret help
```
{: pre}


### `ibmcloud oc ingress secret ls`
{: #ingress-secret-ls-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

List all Ingress secrets in a cluster.
{: shortdesc}

```sh
ibmcloud oc ingress secret ls --cluster CLUSTER [--output OUTPUT] [-q] [--show-crn] [--show-deleted]
```

#### Command options
{: #ingress-secret-ls-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.

`--show-crn`
:    Show CRN value of secret.

`--show-deleted`
:    Show secrets that were deleted from the cluster.


#### Examples
{: #ingress-secret-ls-examples}

List all Ingress secrets in a cluster

```sh
ibmcloud ks ingress secret ls --cluster CLUSTER
```
{: pre}


### `ibmcloud oc ingress secret rm`
{: #ingress-secret-rm-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

Remove an Ingress secret from a cluster.
{: shortdesc}

```sh
ibmcloud oc ingress secret rm --cluster CLUSTER --name NAME --namespace NAMESPACE [-q]
```

#### Command options
{: #ingress-secret-rm-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`-n CLUSTER`, `--namespace NAMESPACE`
:    Specify the Kubernetes namespace.

`--name NAME`
:    A name for the Ingress secret that is created in the cluster.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #ingress-secret-rm-examples}

Remove an Ingress secret from a cluster

```sh
ibmcloud ks ingress secret rm --cluster CLUSTER --name NAME --namespace NAMESPACE
```
{: pre}


### `ibmcloud oc ingress secret update`
{: #ingress-secret-update-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

Update an existing Ingress secret.
{: shortdesc}

```sh
ibmcloud oc ingress secret update --cluster CLUSTER --name NAME --namespace NAMESPACE [--cert-crn CRN] [-q]
```

#### Command options
{: #ingress-secret-update-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`--cert-crn CRN`
:    The certificate CRN.

`-n CLUSTER`, `--namespace NAMESPACE`
:    Specify the Kubernetes namespace.

`--name NAME`
:    A name for the Ingress secret that is created in the cluster.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #ingress-secret-update-examples}

Update an existing Ingress secret

```sh
ibmcloud ks ingress secret update --cluster CLUSTER --name NAME --namespace NAMESPACE
```
{: pre}


### `ibmcloud oc ingress security help`
{: #ingress-security-help-cli}



Show help
{: shortdesc}

```sh
ibmcloud oc ingress security help
```


#### Examples
{: #ingress-security-help-examples}

Show help

```sh
ibmcloud ks ingress security help
```
{: pre}


### `ibmcloud oc ingress security port80 disable`
{: #ingress-security-port80-disable-cli}



Disable the usage of port 80 in your cluster.
{: shortdesc}

```sh
ibmcloud oc ingress security port80 disable --cluster CLUSTER [-f] [-q]
```

#### Command options
{: #ingress-security-port80-disable-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #ingress-security-port80-disable-examples}

Disable the usage of port 80 in your cluster

```sh
ibmcloud ks ingress security port80 disable --cluster CLUSTER
```
{: pre}


### `ibmcloud oc ingress security port80 enable`
{: #ingress-security-port80-enable-cli}



Enable the usage of port 80 in your cluster.
{: shortdesc}

```sh
ibmcloud oc ingress security port80 enable --cluster CLUSTER [-f] [-q]
```

#### Command options
{: #ingress-security-port80-enable-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #ingress-security-port80-enable-examples}

Enable the usage of port 80 in your cluster

```sh
ibmcloud ks ingress security port80 enable --cluster CLUSTER
```
{: pre}


### `ibmcloud oc ingress security port80 get`
{: #ingress-security-port80-get-cli}



Get the security configuration of port 80 in your cluster.
{: shortdesc}

```sh
ibmcloud oc ingress security port80 get --cluster CLUSTER [--output OUTPUT] [-q]
```

#### Command options
{: #ingress-security-port80-get-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #ingress-security-port80-get-examples}

Get the security configuration of port 80 in your cluster

```sh
ibmcloud ks ingress security port80 get --cluster CLUSTER
```
{: pre}


### `ibmcloud oc ingress security port80 help`
{: #ingress-security-port80-help-cli}



Show help
{: shortdesc}

```sh
ibmcloud oc ingress security port80 help
```


#### Examples
{: #ingress-security-port80-help-examples}

Show help

```sh
ibmcloud ks ingress security port80 help
```
{: pre}


### `ibmcloud oc ingress status-report disable`
{: #ingress-status-report-disable-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

Disable status reporting for Ingress components in a cluster.
{: shortdesc}

```sh
ibmcloud oc ingress status-report disable --cluster CLUSTER [--output OUTPUT] [-q]
```

#### Command options
{: #ingress-status-report-disable-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #ingress-status-report-disable-examples}

Disable status reporting for Ingress components in a cluster

```sh
ibmcloud ks ingress status-report disable --cluster CLUSTER
```
{: pre}


### `ibmcloud oc ingress status-report enable`
{: #ingress-status-report-enable-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

Enable status reporting for Ingress components in a cluster.
{: shortdesc}

```sh
ibmcloud oc ingress status-report enable --cluster CLUSTER [--output OUTPUT] [-q]
```

#### Command options
{: #ingress-status-report-enable-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #ingress-status-report-enable-examples}

Enable status reporting for Ingress components in a cluster

```sh
ibmcloud ks ingress status-report enable --cluster CLUSTER
```
{: pre}


### `ibmcloud oc ingress status-report get`
{: #ingress-status-report-get-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

Get the status report for Ingress components in a cluster.
{: shortdesc}

```sh
ibmcloud oc ingress status-report get --cluster CLUSTER [--output OUTPUT] [-q]
```

#### Command options
{: #ingress-status-report-get-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #ingress-status-report-get-examples}

Get the status report for Ingress components in a cluster

```sh
ibmcloud ks ingress status-report get --cluster CLUSTER
```
{: pre}


### `ibmcloud oc ingress status-report help`
{: #ingress-status-report-help-cli}



Show help
{: shortdesc}

```sh
ibmcloud oc ingress status-report help
```


#### Examples
{: #ingress-status-report-help-examples}

Show help

```sh
ibmcloud ks ingress status-report help
```
{: pre}


### `ibmcloud oc ingress status-report ignored-errors add`
{: #ingress-status-report-ignored-errors-add-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

Suppress warnings from Ingress status reports for a cluster.
{: shortdesc}

```sh
ibmcloud oc ingress status-report ignored-errors add --cluster CLUSTER --code CODE [--code CODE ...] [--output OUTPUT] [-q]
```

#### Command options
{: #ingress-status-report-ignored-errors-add-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`--code CODE`
:    Code of the warning to be ignored.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #ingress-status-report-ignored-errors-add-examples}

Suppress warnings from Ingress status reports for a cluster

```sh
ibmcloud ks ingress status-report ignored-errors add --cluster CLUSTER --code CODE
```
{: pre}


### `ibmcloud oc ingress status-report ignored-errors help`
{: #ingress-status-report-ignored-errors-help-cli}



Show help
{: shortdesc}

```sh
ibmcloud oc ingress status-report ignored-errors help
```


#### Examples
{: #ingress-status-report-ignored-errors-help-examples}

Show help

```sh
ibmcloud ks ingress status-report ignored-errors help
```
{: pre}


### `ibmcloud oc ingress status-report ignored-errors ls`
{: #ingress-status-report-ignored-errors-ls-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

List warnings that are currently ignored by Ingress status for a cluster.
{: shortdesc}

```sh
ibmcloud oc ingress status-report ignored-errors ls --cluster CLUSTER [--output OUTPUT] [-q]
```

#### Command options
{: #ingress-status-report-ignored-errors-ls-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #ingress-status-report-ignored-errors-ls-examples}

List warnings that are currently ignored by Ingress status for a cluster

```sh
ibmcloud ks ingress status-report ignored-errors ls --cluster CLUSTER
```
{: pre}


### `ibmcloud oc ingress status-report ignored-errors rm`
{: #ingress-status-report-ignored-errors-rm-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

Remove warnings that are currently ignored by Ingress status for a cluster.
{: shortdesc}

```sh
ibmcloud oc ingress status-report ignored-errors rm --cluster CLUSTER --code CODE [--code CODE ...] [--output OUTPUT] [-q]
```

#### Command options
{: #ingress-status-report-ignored-errors-rm-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`--code CODE`
:    Code of the warning to be removed.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #ingress-status-report-ignored-errors-rm-examples}

Remove warnings that are currently ignored by Ingress status for a cluster

```sh
ibmcloud ks ingress status-report ignored-errors rm --cluster CLUSTER --code CODE
```
{: pre}


## Kms commands
{: #kms-cli}

View and configure Key Management Service integrations.
{: shortdesc}


### `ibmcloud oc kms crk help`
{: #kms-crk-help-cli}



Show help
{: shortdesc}

```sh
ibmcloud oc kms crk help
```


#### Examples
{: #kms-crk-help-examples}

Show help

```sh
ibmcloud ks kms crk help
```
{: pre}


### `ibmcloud oc kms crk ls`
{: #kms-crk-ls-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

List available root keys for a Key Management Service instance.
{: shortdesc}

```sh
ibmcloud oc kms crk ls --instance-id ID [--output OUTPUT] [-q]
```

#### Command options
{: #kms-crk-ls-options}


`--instance-id ID`
:    KMS instance ID. To see available KMS instances, run `ibmcloud ks kms instance ls`.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #kms-crk-ls-examples}

List available root keys for a Key Management Service instance

```sh
ibmcloud ks kms crk ls --instance-id ID
```
{: pre}


### `ibmcloud oc kms enable`
{: #kms-enable-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

Enable a key management service (KMS) in your cluster to encrypt your secrets.
{: shortdesc}

```sh
ibmcloud oc kms enable --cluster CLUSTER --crk CRK --instance-id ID [--kms-account-id ID] [--public-endpoint] [-q]
```

#### Command options
{: #kms-enable-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`--crk CRK`
:    A root key ID in your KMS instance. To list available root keys, run `ibmcloud ks kms crk ls --instance-id <kms_instance>`.

`--instance-id ID`
:    KMS instance ID. To see available KMS instances, run `ibmcloud ks kms instance ls`.

`--kms-account-id ID`
:    The ID of the account that contains the KMS instance you want to use for local disk or secret encryption.

`--public-endpoint`
:    Specify this option to use the KMS public service endpoint. Otherwise the KMS private service endpoint is used.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #kms-enable-examples}

Enable a key management service (KMS) in your cluster to encrypt your secrets

```sh
ibmcloud ks kms enable --cluster CLUSTER --crk CRK --instance-id ID
```
{: pre}


### `ibmcloud oc kms help`
{: #kms-help-cli}



Show help
{: shortdesc}

```sh
ibmcloud oc kms help
```


#### Examples
{: #kms-help-examples}

Show help

```sh
ibmcloud ks kms help
```
{: pre}


### `ibmcloud oc kms instance help`
{: #kms-instance-help-cli}



Show help
{: shortdesc}

```sh
ibmcloud oc kms instance help
```


#### Examples
{: #kms-instance-help-examples}

Show help

```sh
ibmcloud ks kms instance help
```
{: pre}


### `ibmcloud oc kms instance ls`
{: #kms-instance-ls-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

List available Key Management Service instances.
{: shortdesc}

```sh
ibmcloud oc kms instance ls [--output OUTPUT] [-q]
```

#### Command options
{: #kms-instance-ls-options}


`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #kms-instance-ls-examples}

List available Key Management Service instances

```sh
ibmcloud ks kms instance ls
```
{: pre}


## Locations commands
{: #locations-cli}

List supported IBM Cloud Kubernetes Service locations.
{: shortdesc}


### `ibmcloud oc locations`
{: #locations-cli}



List supported IBM Cloud Kubernetes Service locations.
{: shortdesc}

```sh
ibmcloud oc locations
```

#### Command options
{: #locations-options}


`--output`
:    Prints the command output in the provided format. Accepted values: `json`

`--provider`
:    Filter the list for a specific infrastructure provider. Accepted values: `classic`, `vpc-classic`, `vpc-gen2`, `satellite`

`-q`
:    Do not show the message of the day or update reminders.

`--show-flavors`
:    Show the available worker node flavors in the zone for VPC.


#### Examples
{: #locations-examples}

List supported IBM Cloud Kubernetes Service locations

```sh
ibmcloud ks locations
```
{: pre}


## Logging commands
{: #logging-cli}

Forward logs from your cluster.
{: shortdesc}


### `ibmcloud oc logging autoupdate disable`
{: #logging-autoupdate-disable-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} 

Disable automatic updates of all Fluentd pods in a cluster.
{: shortdesc}

```sh
ibmcloud oc logging autoupdate disable --cluster CLUSTER [-q]
```

#### Command options
{: #logging-autoupdate-disable-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #logging-autoupdate-disable-examples}

Disable automatic updates of all Fluentd pods in a cluster

```sh
ibmcloud ks logging autoupdate disable --cluster CLUSTER
```
{: pre}


### `ibmcloud oc logging autoupdate enable`
{: #logging-autoupdate-enable-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} 

Enable automatic updates of all Fluentd pods in a cluster.
{: shortdesc}

```sh
ibmcloud oc logging autoupdate enable --cluster CLUSTER [-q]
```

#### Command options
{: #logging-autoupdate-enable-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #logging-autoupdate-enable-examples}

Enable automatic updates of all Fluentd pods in a cluster

```sh
ibmcloud ks logging autoupdate enable --cluster CLUSTER
```
{: pre}


### `ibmcloud oc logging autoupdate get`
{: #logging-autoupdate-get-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} 

View whether your Fluentd pods are set to automatically update in a cluster.
{: shortdesc}

```sh
ibmcloud oc logging autoupdate get --cluster CLUSTER [--output OUTPUT] [-q]
```

#### Command options
{: #logging-autoupdate-get-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #logging-autoupdate-get-examples}

View whether your Fluentd pods are set to automatically update in a cluster

```sh
ibmcloud ks logging autoupdate get --cluster CLUSTER
```
{: pre}


### `ibmcloud oc logging autoupdate help`
{: #logging-autoupdate-help-cli}



Show help
{: shortdesc}

```sh
ibmcloud oc logging autoupdate help
```


#### Examples
{: #logging-autoupdate-help-examples}

Show help

```sh
ibmcloud ks logging autoupdate help
```
{: pre}


### `ibmcloud oc logging config create`
{: #logging-config-create-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} 

Create a logging configuration. If you are using a Dedicated account, you must log in to the public IBM Cloud endpoint and target your public org and space to enable log forwarding.
{: shortdesc}

```sh
ibmcloud oc logging config create --cluster CLUSTER --logsource LOGSOURCE --type TYPE [--force-update] [--hostname HOSTNAME] [--output OUTPUT] [--port PORT] [-q] (--ca-cert CERT --syslog-protocol PROTOCOL --verify-mode MODE | --org ORG --skip-validation --space SPACE) (--namespace NAMESPACE | -C CONTAINER -p PATH)
```

#### Command options
{: #logging-config-create-options}


`-C CONTAINER`, `--app-container CONTAINER`
:    Specify the containers that you want to collect logs for. To specify more than one path, use multiple flags, such as `-C container1 -C container2`. This option is required for the `application` log source. If not provided, logs are collected from all containers from the application log paths passed in.

`-c CONTAINER`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`--ca-cert CERT`
:    When the logging type is `syslog` and the protocol is tls, the Kubernetes secret name that contains the Certificate Authority certificate.

`--force-update`
:    Force an update of the Fluentd pods in the cluster to the latest version.

`--hostname HOSTNAME`
:    When logging type is `syslog`, the hostname or IP address of the log collector. When logging type is `ibm` (deprecated), the logging ingest endpoint. If you do not provide the logging ingest endpoint, then the current region's endpoint is used.

`--logsource LOGSOURCE`
:    The source of the logs to forward. Supported values are `container`, `application`, `ingress`, `worker`, `storage`, and `kubernetes`. This argument supports a comma separated list of log sources. If you do not provide a log source, logs for `container` and `ingress` are forwarded.

`-n CLUSTER`, `--namespace NAMESPACE`
:    The namespace you want to apply the log forwarding configuration to. Only use this flag with the `container` log source or if you do not specify a log source. If you do not specify a namespace, then all namespaces use this configuration.

`--org ORG`
:    [Deprecated]{: tag-deprecated} The org name to send logs to. This flag is only valid when the logging type is `ibm`. The org name is required when you specify a space name. If you do not specify a space name, then logs are forwarded at the account level.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-p PATH`, `--app-path PATH`
:    Specify the absolute file path to collect logs from inside the container. To specify more than one path, use multiple flags, such as `-p path1 -p path2`. Required parameter when specifying `application` for the log source. Wildcards such as `/var/log/*.log` are accepted but recursive globs such are `/var/log/**/test.log` are not.

`--port PORT`
:    The port of the log collector. If you do not specify a port, the default port for the ingestion endpoint is used for `ibm` (deprecated) and `514` is used for `syslog`.

`-q`
:    Do not show the message of the day or update reminders.

`--skip-validation`
:    Skips validation of the org and space names when they are specified. This can result in a broken logging config if the values are invalid but will take less time to process.

`--space SPACE`
:    [Deprecated]{: tag-deprecated} The space name to send logs to. This flag is only valid when the logging type is `ibm`. The space name is required when you specify an org name. If you do not specify a space name, then logs are forwarded at the account level.

`--syslog-protocol PROTOCOL`
:    When the logging type is `syslog`, the transport layer protocol. Supported values are `tls`, `tcp` and the default `udp`. When forwarding to an rsyslog server with the UDP protocol, logs that are over 1KB are truncated.

`--type TYPE`
:    The log forwarding protocol that you want to use. The only supported value is `syslog`.

`--verify-mode MODE`
:    When the logging type is `syslog` and the protocol is tls, the verification mode. Supported values are `verify-peer` and the default `verify-none`.


#### Examples
{: #logging-config-create-examples}

Create a logging configuration

```sh
ibmcloud ks logging config create \
  --cluster CLUSTER \
  --logsource LOGSOURCE \
  --type TYPE \
  --ca-cert CERT \
  --syslog-protocol PROTOCOL \
  --verify-mode MODE \
  --namespace NAMESPACE
```
{: pre}


### `ibmcloud oc logging config get`
{: #logging-config-get-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} 

View log forwarding configurations for a cluster.
{: shortdesc}

```sh
ibmcloud oc logging config get --cluster CLUSTER [--logsource LOGSOURCE] [--output OUTPUT] [-q]
```

#### Command options
{: #logging-config-get-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`--logsource LOGSOURCE`
:    The kind of log source you want to filter for. Accepted values are `container`, `application`, `ingress`, `worker`, `storage` and `kubernetes`. If you do not pass a log source, all logging configurations for the cluster are returned.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #logging-config-get-examples}

View log forwarding configurations for a cluster

```sh
ibmcloud ks logging config get --cluster CLUSTER
```
{: pre}


### `ibmcloud oc logging config help`
{: #logging-config-help-cli}



Show help
{: shortdesc}

```sh
ibmcloud oc logging config help
```


#### Examples
{: #logging-config-help-examples}

Show help

```sh
ibmcloud ks logging config help
```
{: pre}


### `ibmcloud oc logging config rm`
{: #logging-config-rm-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} 

Delete a log forwarding configuration from a cluster.
{: shortdesc}

```sh
ibmcloud oc logging config rm --cluster CLUSTER [--force-update] [-q] (--all | --id ID | --namespace NAMESPACE)
```

#### Command options
{: #logging-config-rm-options}


`--all`
:    Remove all log forwarding configurations.

`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`--force-update`
:    Force an update of the Fluentd pods in the cluster to the latest version.

`--id ID`
:    Specify the ID of the logging configuration.

`-n CLUSTER`, `--namespace NAMESPACE`
:    The namespace you want to remove the log forwarding configuration from. If there is more than one config for the same namespace, use the `--id <logging configuration ID>` flag instead.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #logging-config-rm-examples}

Delete a log forwarding configuration from a cluster

```sh
ibmcloud ks logging config rm --cluster CLUSTER --all
```
{: pre}


### `ibmcloud oc logging config update`
{: #logging-config-update-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} 

Update a log forwarding configuration for a cluster.
{: shortdesc}

```sh
ibmcloud oc logging config update --cluster CLUSTER --id ID --logsource LOGSOURCE --type TYPE [--force-update] [--hostname HOSTNAME] [--output OUTPUT] [--port PORT] [-q] (--ca-cert CERT --syslog-protocol PROTOCOL --verify-mode MODE | --org ORG --skip-validation --space SPACE) (--namespace NAMESPACE | -C CONTAINER -p PATH)
```

#### Command options
{: #logging-config-update-options}


`-C CONTAINER`, `--app-container CONTAINER`
:    Specify the containers that you want to collect logs for. To specify more than one path, use multiple flags, such as `-C container1 -C container2`. This option is required for the `application` log source. If not provided, logs are collected from all containers from the application log paths passed in.

`-c CONTAINER`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`--ca-cert CERT`
:    When the logging type is `syslog` and the protocol is tls, the Kubernetes secret name that contains the Certificate Authority certificate.

`--force-update`
:    Force an update of the Fluentd pods in the cluster to the latest version.

`--hostname HOSTNAME`
:    When logging type is `syslog`, the hostname or IP address of the log collector. When logging type is `ibm` (deprecated), the logging ingest endpoint. If you do not provide the logging ingest endpoint, then the current region's endpoint is used.

`--id ID`
:    Specify the ID of the logging configuration.

`--logsource LOGSOURCE`
:    The source of the logs to forward. Supported values are `container`, `application`, `ingress`, `worker`, `storage`, and `kubernetes`. This argument supports a comma separated list of log sources. If you do not provide a log source, logs for `container` and `ingress` are forwarded.

`-n CLUSTER`, `--namespace NAMESPACE`
:    The namespace you want to apply the log forwarding configuration to. Only use this flag with the `container` log source or if you do not specify a log source. If you do not specify a namespace, then all namespaces use this configuration.

`--org ORG`
:    [Deprecated]{: tag-deprecated} The org name to send logs to. This flag is only valid when the logging type is `ibm`. The org name is required when you specify a space name. If you do not specify a space name, then logs are forwarded at the account level.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-p PATH`, `--app-path PATH`
:    Specify the absolute file path to collect logs from inside the container. To specify more than one path, use multiple flags, such as `-p path1 -p path2`. Required parameter when specifying `application` for the log source. Wildcards such as `/var/log/*.log` are accepted but recursive globs such are `/var/log/**/test.log` are not.

`--port PORT`
:    The port of the log collector. If you do not specify a port, the default port for the ingestion endpoint is used for `ibm` (deprecated) and `514` is used for `syslog`.

`-q`
:    Do not show the message of the day or update reminders.

`--skip-validation`
:    Skips validation of the org and space names when they are specified. This can result in a broken logging config if the values are invalid but will take less time to process.

`--space SPACE`
:    [Deprecated]{: tag-deprecated} The space name to send logs to. This flag is only valid when the logging type is `ibm`. The space name is required when you specify an org name. If you do not specify a space name, then logs are forwarded at the account level.

`--syslog-protocol PROTOCOL`
:    When the logging type is `syslog`, the transport layer protocol. Supported values are `tls`, `tcp` and the default `udp`. When forwarding to an rsyslog server with the UDP protocol, logs that are over 1KB are truncated.

`--type TYPE`
:    The log forwarding protocol that you want to use. The only supported value is `syslog`.

`--verify-mode MODE`
:    When the logging type is `syslog` and the protocol is tls, the verification mode. Supported values are `verify-peer` and the default `verify-none`.


#### Examples
{: #logging-config-update-examples}

Update a log forwarding configuration for a cluster

```sh
ibmcloud ks logging config update \
  --cluster CLUSTER \
  --id ID \
  --logsource LOGSOURCE \
  --type TYPE \
  --ca-cert CERT \
  --syslog-protocol PROTOCOL \
  --verify-mode MODE \
  --namespace NAMESPACE
```
{: pre}


### `ibmcloud oc logging filter create`
{: #logging-filter-create-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} 

Create a filter to exclude log lines from forwarding.
{: shortdesc}

```sh
ibmcloud oc logging filter create --cluster CLUSTER [--container CONTAINER] [--force-update] [--lc LOGGING-CONFIG ...] [--level LEVEL] [--namespace NAMESPACE] [--output OUTPUT] [-q] [--type TYPE] (--message MESSAGE | --regex-message MESSAGE)
```

#### Command options
{: #logging-filter-create-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`--container CONTAINER`
:    The name of the container from which you want to filter out logs. This flag applies only when you are using log type container.

`--force-update`
:    Force an update of the Fluentd pods in the cluster to the latest version.

`--lc LOGGING-CONFIG`, `--logging-config LOGGING-CONFIG`
:    A logging configuration ID. If not provided, the filter is applied to all the cluster logging configurations that are passed to the filter. You can view log configurations that match the filter by using the --show-matching-configs flag with the command.

`--level LEVEL`
:    Filters out logs that are at the specified level and less. Acceptable values in their canonical order are fatal, error, warn/warning, info, debug, and trace. As an example, if you filtered logs at the info level, debug, and trace are also filtered. **Note**: You can use this flag only when log messages are in JSON format and contain a level field. Example output: {"log": "hello", "level": "info"}

`--message MESSAGE`
:    Filters out any logs that contain a specified message anywhere in the log. The message is matched literally and not as an expression. Example: The messages "Hello", "!", and "Hello, World!", would apply to the log "Hello, World!".

`-n LOGGING-CONFIG`, `--namespace NAMESPACE`
:    The Kubernetes namespace from which you want to filter logs.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.

`--regex-message MESSAGE`
:    Filters out any logs that contain a specified message regex pattern in the log. The message is matched as a regular expression. Example: The pattern "hello [0-9]" would apply to "hello 1", "hello 2", "hello 9"

`--type TYPE`
:    The type of logs that you want to apply the filter to. Currently all, container, and host are supported.


#### Examples
{: #logging-filter-create-examples}

Create a filter to exclude log lines from forwarding

```sh
ibmcloud ks logging filter create --cluster CLUSTER --message MESSAGE
```
{: pre}


### `ibmcloud oc logging filter get`
{: #logging-filter-get-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} 

View a logging filter configuration.
{: shortdesc}

```sh
ibmcloud oc logging filter get --cluster CLUSTER [--id ID] [--output OUTPUT] [-q] [--show-covering-filters] [--show-matching-configs]
```

#### Command options
{: #logging-filter-get-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`--id ID`
:    Specify the ID of the logging filter.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.

`--show-covering-filters`
:    Show the logging filters that render previous filters obsolete.

`--show-matching-configs`
:    Show the logging configurations that match the configuration that you're viewing.


#### Examples
{: #logging-filter-get-examples}

View a logging filter configuration

```sh
ibmcloud ks logging filter get --cluster CLUSTER
```
{: pre}


### `ibmcloud oc logging filter help`
{: #logging-filter-help-cli}



Show help
{: shortdesc}

```sh
ibmcloud oc logging filter help
```


#### Examples
{: #logging-filter-help-examples}

Show help

```sh
ibmcloud ks logging filter help
```
{: pre}


### `ibmcloud oc logging filter rm`
{: #logging-filter-rm-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} 

Delete a logging filter.
{: shortdesc}

```sh
ibmcloud oc logging filter rm --cluster CLUSTER [--force-update] [-q] (--all | --id ID)
```

#### Command options
{: #logging-filter-rm-options}


`--all`
:    Delete all log forwarding filters.

`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`--force-update`
:    Force an update of the Fluentd pods in the cluster to the latest version.

`--id ID`
:    Specify the ID of the logging filter.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #logging-filter-rm-examples}

Delete a logging filter

```sh
ibmcloud ks logging filter rm --cluster CLUSTER --all
```
{: pre}


### `ibmcloud oc logging filter update`
{: #logging-filter-update-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} 

Update a logging filter.
{: shortdesc}

```sh
ibmcloud oc logging filter update --cluster CLUSTER --id ID [--container CONTAINER] [--force-update] [--lc LOGGING-CONFIG ...] [--level LEVEL] [--namespace NAMESPACE] [--output OUTPUT] [-q] [--type TYPE] (--message MESSAGE | --regex-message MESSAGE)
```

#### Command options
{: #logging-filter-update-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`--container CONTAINER`
:    The name of the container from which you want to filter out logs. This flag applies only when you are using log type container.

`--force-update`
:    Force an update of the Fluentd pods in the cluster to the latest version.

`--id ID`
:    Specify the ID of the logging filter.

`--lc LOGGING-CONFIG`, `--logging-config LOGGING-CONFIG`
:    A logging configuration ID. If not provided, the filter is applied to all the cluster logging configurations that are passed to the filter. You can view log configurations that match the filter by using the --show-matching-configs flag with the command.

`--level LEVEL`
:    Filters out logs that are at the specified level and less. Acceptable values in their canonical order are fatal, error, warn/warning, info, debug, and trace. As an example, if you filtered logs at the info level, debug, and trace are also filtered. **Note**: You can use this flag only when log messages are in JSON format and contain a level field. Example output: {"log": "hello", "level": "info"}

`--message MESSAGE`
:    Filters out any logs that contain a specified message anywhere in the log. The message is matched literally and not as an expression. Example: The messages "Hello", "!", and "Hello, World!", would apply to the log "Hello, World!".

`-n LOGGING-CONFIG`, `--namespace NAMESPACE`
:    The Kubernetes namespace from which you want to filter logs.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.

`--regex-message MESSAGE`
:    Filters out any logs that contain a specified message regex pattern in the log. The message is matched as a regular expression. Example: The pattern "hello [0-9]" would apply to "hello 1", "hello 2", "hello 9"

`--type TYPE`
:    The type of logs that you want to apply the filter to. Currently all, container, and host are supported.


#### Examples
{: #logging-filter-update-examples}

Update a logging filter

```sh
ibmcloud ks logging filter update --cluster CLUSTER --id ID --message MESSAGE
```
{: pre}


### `ibmcloud oc logging help`
{: #logging-help-cli}



Show help
{: shortdesc}

```sh
ibmcloud oc logging help
```


#### Examples
{: #logging-help-examples}

Show help

```sh
ibmcloud ks logging help
```
{: pre}


### `ibmcloud oc logging refresh`
{: #logging-refresh-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} 

Refresh the logging configuration for a cluster.
{: shortdesc}

```sh
ibmcloud oc logging refresh --cluster CLUSTER [--force-update] [-q]
```

#### Command options
{: #logging-refresh-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`--force-update`
:    Force an update of the Fluentd pods in the cluster to the latest version.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #logging-refresh-examples}

Refresh the logging configuration for a cluster

```sh
ibmcloud ks logging refresh --cluster CLUSTER
```
{: pre}


## Messages commands
{: #messages-cli}

View the current user messages.
{: shortdesc}


### `ibmcloud oc messages`
{: #messages-cli}



View the current user messages.
{: shortdesc}

```sh
ibmcloud oc messages [-q]
```

#### Command options
{: #messages-options}


`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #messages-examples}

View the current user messages

```sh
ibmcloud ks messages
```
{: pre}


## Nlb-dns commands
{: #nlb-dns-cli}

Create and manage host names for network load balancer (NLB) IP addresses in a cluster and health check monitors for host names.
{: shortdesc}


### `ibmcloud oc nlb-dns add`
{: #nlb-dns-add-cli}

[Classic infrastructure]{: tag-classic-inf} 

Add an NLB IP to an existing host name that you created with `ibmcloud ks nlb-dns create`.
{: shortdesc}

```sh
ibmcloud oc nlb-dns add --cluster CLUSTER --ip IP [--ip IP ...] --nlb-host HOST [--output OUTPUT] [-q]
```

#### Command options
{: #nlb-dns-add-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`--ip IP`
:    One or more NLB IP addresses. To see load balancer IPs, run `kubectl get svc -n <namespace>`.

`--nlb-host HOST`
:    The host name. To see existing host names, run `ibmcloud ks nlb-dns ls`.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #nlb-dns-add-examples}

Add an NLB IP to an existing host name that you created with `ibmcloud ks nlb-dns create`

```sh
ibmcloud ks nlb-dns add --cluster CLUSTER --ip IP --nlb-host HOST
```
{: pre}


### `ibmcloud oc nlb-dns create classic`
{: #nlb-dns-create-classic-cli}

[Classic infrastructure]{: tag-classic-inf} 

Create a DNS host name to register one or more NLB IPs in a classic cluster.
{: shortdesc}

```sh
ibmcloud oc nlb-dns create classic --cluster CLUSTER --ip IP [--ip IP ...] [--output OUTPUT] [-q] [--secret-namespace NAMESPACE]
```

#### Command options
{: #nlb-dns-create-classic-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`--ip IP`
:    One or more NLB IP addresses. To see load balancer IPs, run `kubectl get svc -n <namespace>`.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.

`--secret-namespace NAMESPACE`
:    The namespace that the SSL secret is created in. If this flag is not specified, the secret is created in `default.`


#### Examples
{: #nlb-dns-create-classic-examples}

Create a DNS host name to register one or more NLB IPs in a classic cluster

```sh
ibmcloud ks nlb-dns create classic --cluster CLUSTER --ip IP
```
{: pre}


### `ibmcloud oc nlb-dns create help`
{: #nlb-dns-create-help-cli}



Show help
{: shortdesc}

```sh
ibmcloud oc nlb-dns create help
```


#### Examples
{: #nlb-dns-create-help-examples}

Show help

```sh
ibmcloud ks nlb-dns create help
```
{: pre}


### `ibmcloud oc nlb-dns create vpc-gen2`
{: #nlb-dns-create-vpc-gen2-cli}

[Virtual Private Cloud]{: tag-vpc} 

Create a DNS record to register a load balancer host name or load balancer IP addresses in a VPC cluster.
{: shortdesc}

```sh
ibmcloud oc nlb-dns create vpc-gen2 --cluster CLUSTER [--output OUTPUT] [-q] [--secret-namespace NAMESPACE] (--ip IP | --lb-host HOST)
```

#### Command options
{: #nlb-dns-create-vpc-gen2-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`--ip IP`
:    One or more NLB IP addresses. To see load balancer IPs, run `kubectl get svc -n <namespace>`.

`--lb-host HOST`
:    The VPC load balancer host name. To see load balancer host names, run `kubectl get svc -n <namespace>`.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.

`--secret-namespace NAMESPACE`
:    The namespace that the SSL secret is created in. If this flag is not specified, the secret is created in `default.`


#### Examples
{: #nlb-dns-create-vpc-gen2-examples}

Create a DNS record to register a load balancer host name or load balancer IP addresses in a VPC cluster

```sh
ibmcloud ks nlb-dns create vpc-gen2 --cluster CLUSTER --ip IP
```
{: pre}


### `ibmcloud oc nlb-dns get`
{: #nlb-dns-get-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

View the details of a registered NLB host name in a cluster.
{: shortdesc}

```sh
ibmcloud oc nlb-dns get --cluster CLUSTER --nlb-subdomain SUBDOMAIN [--output OUTPUT] [-q]
```

#### Command options
{: #nlb-dns-get-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`--nlb-subdomain SUBDOMAIN`
:    The subdomain. To see existing subdomains, run `ibmcloud ks nlb-dns ls`.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #nlb-dns-get-examples}

View the details of a registered NLB host name in a cluster

```sh
ibmcloud ks nlb-dns get --cluster CLUSTER --nlb-subdomain SUBDOMAIN
```
{: pre}


### `ibmcloud oc nlb-dns help`
{: #nlb-dns-help-cli}



Show help
{: shortdesc}

```sh
ibmcloud oc nlb-dns help
```


#### Examples
{: #nlb-dns-help-examples}

Show help

```sh
ibmcloud ks nlb-dns help
```
{: pre}


### `ibmcloud oc nlb-dns ls`
{: #nlb-dns-ls-cli}



List the registered NLB host names and IP addresses in a cluster.
{: shortdesc}

```sh
ibmcloud oc nlb-dns ls --cluster CLUSTER [--output OUTPUT] [-q]
```

#### Command options
{: #nlb-dns-ls-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #nlb-dns-ls-examples}

List the registered NLB host names and IP addresses in a cluster

```sh
ibmcloud ks nlb-dns ls --cluster CLUSTER
```
{: pre}


### `ibmcloud oc nlb-dns monitor configure`
{: #nlb-dns-monitor-configure-cli}



Configure a health check monitor for an existing NLB host name in a cluster. To enable the monitor, include the `--enable` flag. To update an existing monitor, include only the flags for the settings that you want to change.
{: shortdesc}

```sh
ibmcloud oc nlb-dns monitor configure --cluster CLUSTER --nlb-host HOST [--enable] [--header HEADER ...] [--interval INTERVAL] [--output OUTPUT] [--path PATH] [--port PORT] [-q] [--timeout TIMEOUT] [--type TYPE]
```

#### Command options
{: #nlb-dns-monitor-configure-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`--enable`
:    Enable the health check monitor for the host name.

`--header HEADER`
:    HTTP request headers for the health check are limited to the Host header. This flag is valid only for type `HTTP` or `HTTPS`. This flag accepts values in the following format: `--header Header-Name=value`. When updating a monitor, the existing headers are replaced by the ones you specify. To delete all existing headers specify the flag with an empty value `--header ""`.

`--interval INTERVAL`
:    The interval, in seconds, between each health check. Short intervals might improve failover time but increase load on the IPs. Must be in the range [60, 300]. Default: `60`

`--nlb-host HOST`
:    The host name. To see existing host names, run `ibmcloud ks nlb-dns ls`.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`--path PATH`
:    The endpoint path to health check against. This flag is valid only for type `HTTP` or `HTTPS`. Default: `/` 

`--port PORT`
:    The port number to connect to for the health check. When type is TCP, this flag is required. When type is HTTP or HTTPS, use this flag only for ports other than 80 for HTTP or 443 for HTTPS. HTTP default: `80`. HTTPS default: `443`.

`-q`
:    Do not show the message of the day or update reminders.

`--timeout TIMEOUT`
:    The timeout, in seconds, before the IP is considered unhealthy. Must be in the range [1, 60]. Default: `5`

`--type TYPE`
:    The protocol to use for the health check. Accepted values: `http`, `https`, `tcp`


#### Examples
{: #nlb-dns-monitor-configure-examples}

Configure a health check monitor for an existing NLB host name in a cluster

```sh
ibmcloud ks nlb-dns monitor configure --cluster CLUSTER --nlb-host HOST
```
{: pre}


### `ibmcloud oc nlb-dns monitor disable`
{: #nlb-dns-monitor-disable-cli}

[Classic infrastructure]{: tag-classic-inf} 

Disable an existing health check monitor for a NLB host name in a cluster..
{: shortdesc}

```sh
ibmcloud oc nlb-dns monitor disable --cluster CLUSTER --nlb-host HOST [--output OUTPUT] [-q]
```

#### Command options
{: #nlb-dns-monitor-disable-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`--nlb-host HOST`
:    The host name. To see existing host names, run `ibmcloud ks nlb-dns ls`.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #nlb-dns-monitor-disable-examples}

Disable an existing health check monitor for a NLB host name in a cluster

```sh
ibmcloud ks nlb-dns monitor disable --cluster CLUSTER --nlb-host HOST
```
{: pre}


### `ibmcloud oc nlb-dns monitor enable`
{: #nlb-dns-monitor-enable-cli}

[Classic infrastructure]{: tag-classic-inf} 

Enable a health check monitor for an NLB host name in a cluster. Note: You must first configure the monitor with `ibmcloud ks nlb-dns monitor configure`.
{: shortdesc}

```sh
ibmcloud oc nlb-dns monitor enable --cluster CLUSTER --nlb-host HOST [--output OUTPUT] [-q]
```

#### Command options
{: #nlb-dns-monitor-enable-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`--nlb-host HOST`
:    The host name. To see existing host names, run `ibmcloud ks nlb-dns ls`.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #nlb-dns-monitor-enable-examples}

Enable a health check monitor for an NLB host name in a cluster

```sh
ibmcloud ks nlb-dns monitor enable --cluster CLUSTER --nlb-host HOST
```
{: pre}


### `ibmcloud oc nlb-dns monitor get`
{: #nlb-dns-monitor-get-cli}

[Classic infrastructure]{: tag-classic-inf} 

View the settings for an existing health check monitor.
{: shortdesc}

```sh
ibmcloud oc nlb-dns monitor get --cluster CLUSTER --nlb-host HOST [--output OUTPUT] [-q]
```

#### Command options
{: #nlb-dns-monitor-get-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`--nlb-host HOST`
:    The host name. To see existing host names, run `ibmcloud ks nlb-dns ls`.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #nlb-dns-monitor-get-examples}

View the settings for an existing health check monitor

```sh
ibmcloud ks nlb-dns monitor get --cluster CLUSTER --nlb-host HOST
```
{: pre}


### `ibmcloud oc nlb-dns monitor help`
{: #nlb-dns-monitor-help-cli}



Show help
{: shortdesc}

```sh
ibmcloud oc nlb-dns monitor help
```


#### Examples
{: #nlb-dns-monitor-help-examples}

Show help

```sh
ibmcloud ks nlb-dns monitor help
```
{: pre}


### `ibmcloud oc nlb-dns monitor ls`
{: #nlb-dns-monitor-ls-cli}

[Classic infrastructure]{: tag-classic-inf} 

List the health check monitor settings for each NLB host name in a cluster.
{: shortdesc}

```sh
ibmcloud oc nlb-dns monitor ls --cluster CLUSTER [--output OUTPUT] [-q]
```

#### Command options
{: #nlb-dns-monitor-ls-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #nlb-dns-monitor-ls-examples}

List the health check monitor settings for each NLB host name in a cluster

```sh
ibmcloud ks nlb-dns monitor ls --cluster CLUSTER
```
{: pre}


### `ibmcloud oc nlb-dns replace`
{: #nlb-dns-replace-cli}

[Virtual Private Cloud]{: tag-vpc} 

Update an existing DNS host name by replacing the load balancer hostname associated with it in a VPC cluster.
{: shortdesc}

```sh
ibmcloud oc nlb-dns replace --cluster CLUSTER --lb-host HOST --nlb-subdomain SUBDOMAIN [--output OUTPUT] [-q]
```

#### Command options
{: #nlb-dns-replace-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`--lb-host HOST`
:    The VPC load balancer host name. To see load balancer host names, run `kubectl get svc -n <namespace>`.

`--nlb-subdomain SUBDOMAIN`
:    The subdomain. To see existing subdomains, run `ibmcloud ks nlb-dns ls`.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #nlb-dns-replace-examples}

Update an existing DNS host name by replacing the load balancer hostname associated with it in a VPC cluster

```sh
ibmcloud ks nlb-dns replace --cluster CLUSTER --lb-host HOST --nlb-subdomain SUBDOMAIN
```
{: pre}


### `ibmcloud oc nlb-dns rm classic`
{: #nlb-dns-rm-classic-cli}

[Classic infrastructure]{: tag-classic-inf} 

Remove an NLB IP address from an NLB host name. If you remove all IPs from a host name, the host name still exists but no IPs are associated with it.
{: shortdesc}

```sh
ibmcloud oc nlb-dns rm classic --cluster CLUSTER --ip IP --nlb-host HOST [--output OUTPUT] [-q]
```

#### Command options
{: #nlb-dns-rm-classic-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`--ip IP`
:    One NLB IP address. To see NLB IPs associated with the host name, run `ibmcloud ks nlb-dns ls`.

`--nlb-host HOST`
:    The host name. To see existing host names, run `ibmcloud ks nlb-dns ls`.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #nlb-dns-rm-classic-examples}

Remove an NLB IP address from an NLB host name

```sh
ibmcloud ks nlb-dns rm classic --cluster CLUSTER --ip IP --nlb-host HOST
```
{: pre}


### `ibmcloud oc nlb-dns rm help`
{: #nlb-dns-rm-help-cli}



Show help
{: shortdesc}

```sh
ibmcloud oc nlb-dns rm help
```


#### Examples
{: #nlb-dns-rm-help-examples}

Show help

```sh
ibmcloud ks nlb-dns rm help
```
{: pre}


### `ibmcloud oc nlb-dns rm vpc-gen2`
{: #nlb-dns-rm-vpc-gen2-cli}

[Virtual Private Cloud]{: tag-vpc} 

Remove a load balancer host name or IP address from a DNS record in a VPC cluster.
{: shortdesc}

```sh
ibmcloud oc nlb-dns rm vpc-gen2 --cluster CLUSTER --nlb-subdomain SUBDOMAIN [--ip IP] [--output OUTPUT] [-q]
```

#### Command options
{: #nlb-dns-rm-vpc-gen2-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`--ip IP`
:    One NLB IP address. To see NLB IPs associated with the host name, run `ibmcloud ks nlb-dns ls`.

`--nlb-subdomain SUBDOMAIN`
:    The subdomain. To see existing subdomains, run `ibmcloud ks nlb-dns ls`.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #nlb-dns-rm-vpc-gen2-examples}

Remove a load balancer host name or IP address from a DNS record in a VPC cluster

```sh
ibmcloud ks nlb-dns rm vpc-gen2 --cluster CLUSTER --nlb-subdomain SUBDOMAIN
```
{: pre}


### `ibmcloud oc nlb-dns secret help`
{: #nlb-dns-secret-help-cli}



Show help
{: shortdesc}

```sh
ibmcloud oc nlb-dns secret help
```


#### Examples
{: #nlb-dns-secret-help-examples}

Show help

```sh
ibmcloud ks nlb-dns secret help
```
{: pre}


### `ibmcloud oc nlb-dns secret regenerate`
{: #nlb-dns-secret-regenerate-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

Regenerate the certificate and secret for an NLB subdomain.
{: shortdesc}

```sh
ibmcloud oc nlb-dns secret regenerate --cluster CLUSTER --nlb-subdomain SUBDOMAIN [--output OUTPUT] [-q]
```

#### Command options
{: #nlb-dns-secret-regenerate-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`--nlb-subdomain SUBDOMAIN`
:    The subdomain. To see existing subdomains, run `ibmcloud ks nlb-dns ls`.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #nlb-dns-secret-regenerate-examples}

Regenerate the certificate and secret for an NLB subdomain

```sh
ibmcloud ks nlb-dns secret regenerate --cluster CLUSTER --nlb-subdomain SUBDOMAIN
```
{: pre}


### `ibmcloud oc nlb-dns secret rm`
{: #nlb-dns-secret-rm-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

Delete a secret from an NLB subdomain and prevent future renewal of the certificate.
{: shortdesc}

```sh
ibmcloud oc nlb-dns secret rm --cluster CLUSTER --nlb-subdomain SUBDOMAIN [-f] [--output OUTPUT] [-q]
```

#### Command options
{: #nlb-dns-secret-rm-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`--nlb-subdomain SUBDOMAIN`
:    The subdomain. To see existing subdomains, run `ibmcloud ks nlb-dns ls`.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #nlb-dns-secret-rm-examples}

Delete a secret from an NLB subdomain and prevent future renewal of the certificate

```sh
ibmcloud ks nlb-dns secret rm --cluster CLUSTER --nlb-subdomain SUBDOMAIN
```
{: pre}


## Quota commands
{: #quota-cli}

View the quota and limits for cluster-related resources in your IBM Cloud account.
{: shortdesc}


### `ibmcloud oc quota help`
{: #quota-help-cli}



Show help
{: shortdesc}

```sh
ibmcloud oc quota help
```


#### Examples
{: #quota-help-examples}

Show help

```sh
ibmcloud ks quota help
```
{: pre}


### `ibmcloud oc quota ls`
{: #quota-ls-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

List all quota and limits for cluster-related resources in your IBM Cloud account.
{: shortdesc}

```sh
ibmcloud oc quota ls [--output OUTPUT] [--provider PROVIDER] [-q]
```

#### Command options
{: #quota-ls-options}


`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`--provider PROVIDER`
:    Filter the list for a specific infrastructure provider. Accepted values: `classic`, `vpc-classic`, `vpc-gen2`, `satellite`

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #quota-ls-examples}

List all quota and limits for cluster-related resources in your IBM Cloud account

```sh
ibmcloud ks quota ls
```
{: pre}


## Script commands
{: #script-cli}

Rewrite scripts that call IBM Cloud Kubernetes Service plug-in commands. Legacy-structured commands are replaced with beta-structured commands.
{: shortdesc}


### `ibmcloud oc script help`
{: #script-help-cli}



Show help
{: shortdesc}

```sh
ibmcloud oc script help
```


#### Examples
{: #script-help-examples}

Show help

```sh
ibmcloud ks script help
```
{: pre}


### `ibmcloud oc script update`
{: #script-update-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} 

Rewrite scripts that call IBM Cloud Kubernetes Service plug-in commands. Legacy-structured commands are replaced with beta-structured commands.
{: shortdesc}

```sh
ibmcloud oc script update [--in-place] FILE [FILE ...]
```

#### Command options
{: #script-update-options}


`--in-place FILE FILE`
:    Rewrite the source file with the updated command structure.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #script-update-examples}

Rewrite scripts that call IBM Cloud Kubernetes Service plug-in commands

```sh
ibmcloud ks script update FILE
```
{: pre}


## Security-group commands
{: #security-group-cli}

Run operations against a security group.
{: shortdesc}


### `ibmcloud oc security-group help`
{: #security-group-help-cli}



Show help
{: shortdesc}

```sh
ibmcloud oc security-group help
```


#### Examples
{: #security-group-help-examples}

Show help

```sh
ibmcloud ks security-group help
```
{: pre}


### `ibmcloud oc security-group ls`
{: #security-group-ls-cli}



List all security groups associated with a cluster.
{: shortdesc}

```sh
ibmcloud oc security-group ls --cluster CLUSTER [--attached-to ATTACHED] [--managed-by MANAGER] [--output OUTPUT] [-q] [--scope SCOPE]
```

#### Command options
{: #security-group-ls-options}


`--attached-to ATTACHED`
:    Filter the security groups by the components they are attached to. Accepted values: `cluster`, `load-balancer`, `vpc`, `vpe-gateway`, `worker-pool`

`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`--managed-by MANAGER`
:    Specify `user` to return the security groups created by user. Specify `ibm` to return only the security groups managed by IBM. Accepted values: `ibm`, `user`

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.

`--scope SCOPE`
:    Specify `cluster` to return security groups scoped to the cluster.  Specify `vpc` to return security groups scoped to the entire VPC. Accepted values: `cluster`, `vpc`


#### Examples
{: #security-group-ls-examples}

List all security groups associated with a cluster

```sh
ibmcloud ks security-group ls --cluster CLUSTER
```
{: pre}


### `ibmcloud oc security-group reset`
{: #security-group-reset-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} 

Deletes all existing security group rules, and reapplies default rules.
{: shortdesc}

```sh
ibmcloud oc security-group reset --cluster CLUSTER --security-group GROUP [-f] [-q]
```

#### Command options
{: #security-group-reset-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`-q`
:    Do not show the message of the day or update reminders.

`--security-group GROUP`, `--sg GROUP`
:    Specify security group ID.


#### Examples
{: #security-group-reset-examples}

Deletes all existing security group rules, and reapplies default rules

```sh
ibmcloud ks security-group reset --cluster CLUSTER --security-group GROUP
```
{: pre}


### `ibmcloud oc security-group sync`
{: #security-group-sync-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} 

Reapplies default security group rules that do not exist. Does not delete any preexisting rules.
{: shortdesc}

```sh
ibmcloud oc security-group sync --cluster CLUSTER --security-group GROUP [-q]
```

#### Command options
{: #security-group-sync-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`-q`
:    Do not show the message of the day or update reminders.

`--security-group GROUP`, `--sg GROUP`
:    Specify security group ID.


#### Examples
{: #security-group-sync-examples}

Reapplies default security group rules that do not exist

```sh
ibmcloud ks security-group sync --cluster CLUSTER --security-group GROUP
```
{: pre}


## Storage commands
{: #storage-cli}

View and modify storage resources.
{: shortdesc}


### `ibmcloud oc storage attachment create`
{: #storage-attachment-create-cli}

The `storage attachment create` command is a beta feature.
{: beta}

[Virtual Private Cloud]{: tag-vpc} 

Attach a storage volume to a worker node.
{: shortdesc}

```sh
ibmcloud oc storage attachment create --cluster CLUSTER --volume VOLUME --worker WORKER [--output OUTPUT] [-q]
```

#### Command options
{: #storage-attachment-create-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.

`--volume VOLUME`
:    Specify the volume ID. To list available volumes, run `ibmcloud ks storage volume ls`.

`-w CLUSTER`, `--worker WORKER`
:    Specify the worker ID. To list available workers, run `ibmcloud ks workers`.


#### Examples
{: #storage-attachment-create-examples}

Attach a storage volume to a worker node

```sh
ibmcloud ks storage attachment create --cluster CLUSTER --volume VOLUME --worker WORKER_ID
```
{: pre}


### `ibmcloud oc storage attachment get`
{: #storage-attachment-get-cli}

The `storage attachment get` command is a beta feature.
{: beta}

[Virtual Private Cloud]{: tag-vpc} 

Get the details of a volume attachment in a cluster.
{: shortdesc}

```sh
ibmcloud oc storage attachment get --attachment ATTACHMENT --cluster CLUSTER --worker WORKER [--output OUTPUT] [-q]
```

#### Command options
{: #storage-attachment-get-options}


`--attachment ATTACHMENT`
:    Specify the volume attachment ID. To list available attachments, run `ibmcloud ks storage attachment ls`.

`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.

`-w CLUSTER`, `--worker WORKER`
:    Specify the worker ID. To list available workers, run `ibmcloud ks workers`.


#### Examples
{: #storage-attachment-get-examples}

Get the details of a volume attachment in a cluster

```sh
ibmcloud ks storage attachment get --attachment ATTACHMENT --cluster CLUSTER --worker WORKER_ID
```
{: pre}


### `ibmcloud oc storage attachment help`
{: #storage-attachment-help-cli}



Show help
{: shortdesc}

```sh
ibmcloud oc storage attachment help
```


#### Examples
{: #storage-attachment-help-examples}

Show help

```sh
ibmcloud ks storage attachment help
```
{: pre}


### `ibmcloud oc storage attachment ls`
{: #storage-attachment-ls-cli}

The `storage attachment ls` command is a beta feature.
{: beta}

[Virtual Private Cloud]{: tag-vpc} 

List all storage volume attachments of a worker in a cluster.
{: shortdesc}

```sh
ibmcloud oc storage attachment ls --cluster CLUSTER --worker WORKER [--output OUTPUT] [-q]
```

#### Command options
{: #storage-attachment-ls-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.

`-w CLUSTER`, `--worker WORKER`
:    Specify the worker ID. To list available workers, run `ibmcloud ks workers`.


#### Examples
{: #storage-attachment-ls-examples}

List all storage volume attachments of a worker in a cluster

```sh
ibmcloud ks storage attachment ls --cluster CLUSTER --worker WORKER_ID
```
{: pre}


### `ibmcloud oc storage attachment rm`
{: #storage-attachment-rm-cli}

The `storage attachment rm` command is a beta feature.
{: beta}

[Virtual Private Cloud]{: tag-vpc} 

Delete a volume attachment from a worker node.
{: shortdesc}

```sh
ibmcloud oc storage attachment rm --attachment ATTACHMENT --cluster CLUSTER --worker WORKER [-q]
```

#### Command options
{: #storage-attachment-rm-options}


`--attachment ATTACHMENT`
:    Specify the volume attachment ID. To list available attachments, run `ibmcloud ks storage attachment ls`.

`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`-q`
:    Do not show the message of the day or update reminders.

`-w CLUSTER`, `--worker WORKER`
:    Specify the worker ID. To list available workers, run `ibmcloud ks workers`.


#### Examples
{: #storage-attachment-rm-examples}

Delete a volume attachment from a worker node

```sh
ibmcloud ks storage attachment rm --attachment ATTACHMENT --cluster CLUSTER --worker WORKER_ID
```
{: pre}


### `ibmcloud oc storage help`
{: #storage-help-cli}



Show help
{: shortdesc}

```sh
ibmcloud oc storage help
```


#### Examples
{: #storage-help-examples}

Show help

```sh
ibmcloud ks storage help
```
{: pre}


### `ibmcloud oc storage volume get`
{: #storage-volume-get-cli}

The `storage volume get` command is a beta feature.
{: beta}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} 

Get the details of a volume.
{: shortdesc}

```sh
ibmcloud oc storage volume get --volume VOLUME [--output OUTPUT] [-q]
```

#### Command options
{: #storage-volume-get-options}


`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.

`--volume VOLUME`
:    Specify the volume ID. To list available volumes, run `ibmcloud ks storage volume ls`.


#### Examples
{: #storage-volume-get-examples}

Get the details of a volume

```sh
ibmcloud ks storage volume get --volume VOLUME
```
{: pre}


### `ibmcloud oc storage volume help`
{: #storage-volume-help-cli}



Show help
{: shortdesc}

```sh
ibmcloud oc storage volume help
```


#### Examples
{: #storage-volume-help-examples}

Show help

```sh
ibmcloud ks storage volume help
```
{: pre}


### `ibmcloud oc storage volume ls`
{: #storage-volume-ls-cli}

The `storage volume ls` command is a beta feature.
{: beta}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} 

List the details of volumes.
{: shortdesc}

```sh
ibmcloud oc storage volume ls [--cluster CLUSTER] [--output OUTPUT] [--provider PROVIDER] [-q] [--zone ZONE]
```

#### Command options
{: #storage-volume-ls-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`--provider PROVIDER`
:    Filter the list for a specific infrastructure provider. Accepted values: `classic`, `vpc-classic`, `vpc-gen2`, `satellite`

`-q`
:    Do not show the message of the day or update reminders.

`--zone ZONE`
:    A zone to filter for. To list available zones, run `ibmcloud ks locations`.


#### Examples
{: #storage-volume-ls-examples}

List the details of volumes

```sh
ibmcloud ks storage volume ls
```
{: pre}


## Subnets commands
{: #subnets-cli}

List available portable subnets in your IBM Cloud infrastructure account.
{: shortdesc}


### `ibmcloud oc subnets`
{: #subnets-cli}



List available portable subnets in your IBM Cloud infrastructure account.
{: shortdesc}

```sh
ibmcloud oc subnets --provider PROVIDER [-l LOCATION ...] [--output OUTPUT] [-q] [--vpc-id ID] [--zone ZONE]
```

#### Command options
{: #subnets-options}


`-l LOCATION`, `--location LOCATION`
:    A location to filter for. To list available locations, run `ibmcloud ks locations`.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`--provider PROVIDER`
:    Filter the list for a specific infrastructure provider. Available options: classic, vpc-classic, vpc-gen2

`-q`
:    Do not show the message of the day or update reminders.

`--vpc-id ID`
:    Required for provider types `vpc-classic` and `vpc-gen2`: The ID of the VPC to list subnets for. To list VPC IDs, run `ibmcloud ks vpcs`.

`--zone ZONE`
:    Required for provider types `vpc-classic` and `vpc-gen2`: The zone to list VPC subnets for. To list available zones, run `ibmcloud ks zone ls --provider vpc-classic|vpc-gen2`.


#### Examples
{: #subnets-examples}

List available portable subnets in your IBM Cloud infrastructure account

```sh
ibmcloud ks subnets --provider PROVIDER
```
{: pre}


## Versions commands
{: #versions-cli}

List all the container platform versions that are available for IBM Cloud Kubernetes Service clusters.
{: shortdesc}


### `ibmcloud oc versions`
{: #versions-cli}



List all the container platform versions that are available for IBM Cloud Kubernetes Service clusters.
{: shortdesc}

```sh
ibmcloud oc versions [--output OUTPUT] [-q] [--show-version VERSION]
```

#### Command options
{: #versions-options}


`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.

`--show-version VERSION`
:    Show only the versions for the specified container platform. Accepted values: `OpenShift`, `Kubernetes`


#### Examples
{: #versions-examples}

List all the container platform versions that are available for IBM Cloud Kubernetes Service clusters

```sh
ibmcloud ks versions
```
{: pre}


## Vlan commands
{: #vlan-cli}

List public and private VLANs for a zone and view the VLAN spanning status.
{: shortdesc}


### `ibmcloud oc vlan help`
{: #vlan-help-cli}



Show help
{: shortdesc}

```sh
ibmcloud oc vlan help
```


#### Examples
{: #vlan-help-examples}

Show help

```sh
ibmcloud ks vlan help
```
{: pre}


### `ibmcloud oc vlan ls`
{: #vlan-ls-cli}

[Classic infrastructure]{: tag-classic-inf} 

List available public and private VLANs for a zone.
{: shortdesc}

```sh
ibmcloud oc vlan ls --zone ZONE [--output OUTPUT] [-q]
```

#### Command options
{: #vlan-ls-options}


`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.

`--zone ZONE`
:    Specify the zone for the worker pool in a multizone cluster. To list available zones, run `ibmcloud ks zone ls`.


#### Examples
{: #vlan-ls-examples}

List available public and private VLANs for a zone

```sh
ibmcloud ks vlan ls --zone ZONE
```
{: pre}


### `ibmcloud oc vlan spanning get`
{: #vlan-spanning-get-cli}

[Classic infrastructure]{: tag-classic-inf} 

View the VLAN spanning status for your IBM Cloud classic infrastructure account.
{: shortdesc}

```sh
ibmcloud oc vlan spanning get [--output OUTPUT] [-q] [--region REGION]
```

#### Command options
{: #vlan-spanning-get-options}


`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.

`--region REGION`
:    Specify the region to target. If a region is not already targeted, this argument must be specified. To check if a region is targeted, run `ibmcloud target`.


#### Examples
{: #vlan-spanning-get-examples}

View the VLAN spanning status for your IBM Cloud classic infrastructure account

```sh
ibmcloud ks vlan spanning get
```
{: pre}


### `ibmcloud oc vlan spanning help`
{: #vlan-spanning-help-cli}



Show help
{: shortdesc}

```sh
ibmcloud oc vlan spanning help
```


#### Examples
{: #vlan-spanning-help-examples}

Show help

```sh
ibmcloud ks vlan spanning help
```
{: pre}


## Vni commands
{: #vni-cli}

Attach, detach, and list Virtual Network Interfaces on worker nodes.
{: shortdesc}


### `ibmcloud oc vni attach baremetal`
{: #vni-attach-baremetal-cli}

[Virtual Private Cloud]{: tag-vpc} 

Attach a Virtual Network Interface to a bare metal worker node or cluster.
{: shortdesc}

```sh
ibmcloud oc vni attach baremetal --vlan VLAN --vni VNI [--auto-delete] [--output OUTPUT] [-q] (--cluster-id ID | --worker WORKER)
```

#### Command options
{: #vni-attach-baremetal-options}


`--auto-delete`
:    Automatically delete the VNI when it is removed from the cluster.

`-c`, `--cluster-id ID`
:    The ID of the cluster.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.

`--vlan VLAN`
:    The VLAN ID for the bare metal node attachment. Must be unique for each VPC subnet. Multiple VNIs from the same subnet can reuse the VLAN ID. Valid range: 1-500.

`--vni VNI`
:    The ID of the Virtual Network Interface to attach. You must specify VNIs without any current target resource. To list all the VNIs, run `ibmcloud is vnis`. To check if a specific VNI is already attached to a resource, check for the "Target" field in 'ibmcloud is vni <VNI_ID>.

`-w ID`, `--worker WORKER`
:    The ID of the worker node.


#### Examples
{: #vni-attach-baremetal-examples}

Attach a Virtual Network Interface to a bare metal worker node or cluster

```sh
ibmcloud ks vni attach baremetal --vlan VLAN --vni VNI --cluster-id CLUSTER_NAME_OR_ID
```
{: pre}


### `ibmcloud oc vni attach help`
{: #vni-attach-help-cli}



Show help
{: shortdesc}

```sh
ibmcloud oc vni attach help
```


#### Examples
{: #vni-attach-help-examples}

Show help

```sh
ibmcloud ks vni attach help
```
{: pre}


### `ibmcloud oc vni detach`
{: #vni-detach-cli}

[Virtual Private Cloud]{: tag-vpc} 

Detach a Virtual Network Interface from a worker node or cluster.
{: shortdesc}

```sh
ibmcloud oc vni detach --vni VNI [-f] [--output OUTPUT] [-q] (--cluster-id ID | --worker WORKER)
```

#### Command options
{: #vni-detach-options}


`-c`, `--cluster-id ID`
:    The ID of the cluster.

`-f`
:    Force the command to run without user prompts.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.

`--vni VNI`
:    The ID of the Virtual Network Interface to detach.

`-w ID`, `--worker WORKER`
:    The ID of the worker node.


#### Examples
{: #vni-detach-examples}

Detach a Virtual Network Interface from a worker node or cluster

```sh
ibmcloud ks vni detach --vni VNI --cluster-id CLUSTER_NAME_OR_ID
```
{: pre}


### `ibmcloud oc vni help`
{: #vni-help-cli}



Show help
{: shortdesc}

```sh
ibmcloud oc vni help
```


#### Examples
{: #vni-help-examples}

Show help

```sh
ibmcloud ks vni help
```
{: pre}


### `ibmcloud oc vni ls`
{: #vni-ls-cli}

[Virtual Private Cloud]{: tag-vpc} 

List Virtual Network Interfaces attached to a cluster or worker node.
{: shortdesc}

```sh
ibmcloud oc vni ls [--after AFTER] [--first FIRST] [--output OUTPUT] [-q] (--cluster-id ID | --worker WORKER)
```

#### Command options
{: #vni-ls-options}


`--after AFTER`
:    Show Virtual Network Interfaces after the given cursor.

`-c`, `--cluster-id ID`
:    The ID of the cluster.

`--first FIRST`
:    View the next Virtual Network Interfaces, up to the first number of VNIs.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.

`-w ID`, `--worker WORKER`
:    The ID of the worker node.


#### Examples
{: #vni-ls-examples}

List Virtual Network Interfaces attached to a cluster or worker node

```sh
ibmcloud ks vni ls --cluster-id CLUSTER_NAME_OR_ID
```
{: pre}


## Vpc commands
{: #vpc-cli}

Get information about VPCs and manage VPC clusters.
{: shortdesc}


### `ibmcloud oc vpc help`
{: #vpc-help-cli}



Show help
{: shortdesc}

```sh
ibmcloud oc vpc help
```


#### Examples
{: #vpc-help-examples}

Show help

```sh
ibmcloud ks vpc help
```
{: pre}


### `ibmcloud oc vpc ls`
{: #vpc-ls-cli}



List all VPCs in the targeted resource group. If no resource group is targeted, all VPCs in the account are listed.
{: shortdesc}

```sh
ibmcloud oc vpc ls [--output OUTPUT] [--provider PROVIDER] [-q]
```

#### Command options
{: #vpc-ls-options}


`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`--provider PROVIDER`
:    The VPC infrastructure provider type. Supported values are `vpc-classic` and `vpc-gen2`. By default, VPCs of all provider types are returned.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #vpc-ls-examples}

List all VPCs in the targeted resource group

```sh
ibmcloud ks vpc ls
```
{: pre}


### `ibmcloud oc vpc outbound-traffic-protection disable`
{: #vpc-outbound-traffic-protection-disable-cli}



Disable outbound traffic protection for a Secure By Default VPC cluster.
{: shortdesc}

```sh
ibmcloud oc vpc outbound-traffic-protection disable --cluster CLUSTER [-f] [-q]
```

#### Command options
{: #vpc-outbound-traffic-protection-disable-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #vpc-outbound-traffic-protection-disable-examples}

Disable outbound traffic protection for a Secure By Default VPC cluster

```sh
ibmcloud ks vpc outbound-traffic-protection disable --cluster CLUSTER
```
{: pre}


### `ibmcloud oc vpc outbound-traffic-protection enable`
{: #vpc-outbound-traffic-protection-enable-cli}



Enable outbound traffic protection for a Secure By Default VPC cluster.
{: shortdesc}

```sh
ibmcloud oc vpc outbound-traffic-protection enable --cluster CLUSTER [-f] [-q]
```

#### Command options
{: #vpc-outbound-traffic-protection-enable-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #vpc-outbound-traffic-protection-enable-examples}

Enable outbound traffic protection for a Secure By Default VPC cluster

```sh
ibmcloud ks vpc outbound-traffic-protection enable --cluster CLUSTER
```
{: pre}


### `ibmcloud oc vpc outbound-traffic-protection help`
{: #vpc-outbound-traffic-protection-help-cli}



Show help
{: shortdesc}

```sh
ibmcloud oc vpc outbound-traffic-protection help
```


#### Examples
{: #vpc-outbound-traffic-protection-help-examples}

Show help

```sh
ibmcloud ks vpc outbound-traffic-protection help
```
{: pre}


### `ibmcloud oc vpc secure-by-default enable`
{: #vpc-secure-by-default-enable-cli}



Enable Secure By Default VPC Networking for a VPC cluster using legacy Security Groups.
{: shortdesc}

```sh
ibmcloud oc vpc secure-by-default enable --cluster CLUSTER [--disable-outbound-traffic-protection] [-f] [-q]
```

#### Command options
{: #vpc-secure-by-default-enable-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`--disable-outbound-traffic-protection`
:    Include this option to allow public outbound access from the cluster workers. By default, public outbound access is blocked.

`-f`
:    Force the command to run without user prompts.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #vpc-secure-by-default-enable-examples}

Enable Secure By Default VPC Networking for a VPC cluster using legacy Security Groups

```sh
ibmcloud ks vpc secure-by-default enable --cluster CLUSTER
```
{: pre}


### `ibmcloud oc vpc secure-by-default help`
{: #vpc-secure-by-default-help-cli}



Show help
{: shortdesc}

```sh
ibmcloud oc vpc secure-by-default help
```


#### Examples
{: #vpc-secure-by-default-help-examples}

Show help

```sh
ibmcloud ks vpc secure-by-default help
```
{: pre}


## Webhook-create commands
{: #webhook-create-cli}

Register a webhook in a cluster.
{: shortdesc}


### `ibmcloud oc webhook-create`
{: #webhook-create-cli}



Register a webhook in a cluster.
{: shortdesc}

```sh
ibmcloud oc webhook-create --cluster CLUSTER --type TYPE --url URL [--level LEVEL] [-q]
```

#### Command options
{: #webhook-create-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`--level LEVEL`
:    Set the notification level. Accepted values are `Normal` or `Warning`. The default is `Warning`.

`-q`
:    Do not show the message of the day or update reminders.

`--type TYPE`
:    The type of webhook that you want to use. Currently `slack` is supported.

`--url URL`
:    The webhook URL.


#### Examples
{: #webhook-create-examples}

Register a webhook in a cluster

```sh
ibmcloud ks webhook-create --cluster CLUSTER --type TYPE --url URL
```
{: pre}


## Worker commands
{: #worker-cli}

View and modify worker nodes for a cluster.
{: shortdesc}


### `ibmcloud oc worker get`
{: #worker-get-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

View the details of a worker node.
{: shortdesc}

```sh
ibmcloud oc worker get --cluster CLUSTER --worker WORKER [--output OUTPUT] [-q]
```

#### Command options
{: #worker-get-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.

`-w CLUSTER`, `--worker WORKER`
:    Specify the worker ID. To list available workers, run `ibmcloud ks workers`.


#### Examples
{: #worker-get-examples}

View the details of a worker node

```sh
ibmcloud ks worker get --cluster CLUSTER --worker WORKER_ID
```
{: pre}


### `ibmcloud oc worker help`
{: #worker-help-cli}



Show help
{: shortdesc}

```sh
ibmcloud oc worker help
```


#### Examples
{: #worker-help-examples}

Show help

```sh
ibmcloud ks worker help
```
{: pre}


### `ibmcloud oc worker ls`
{: #worker-ls-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

List all worker nodes in a cluster.
{: shortdesc}

```sh
ibmcloud oc worker ls --cluster CLUSTER [--output OUTPUT] [-q] [--show-delete-reason] [--show-deleted] [--show-pools] [--worker-pool POOL]
```

#### Command options
{: #worker-ls-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-p CLUSTER`, `--worker-pool POOL`
:    Show only worker nodes that belong to the worker pool you specify.

`-q`
:    Do not show the message of the day or update reminders.

`--show-delete-reason`
:    Show the reason for worker node deletion.

`--show-deleted`
:    Show worker nodes that were deleted from the cluster.

`--show-pools`
:    See the worker pool that each worker belongs to.


#### Examples
{: #worker-ls-examples}

List all worker nodes in a cluster

```sh
ibmcloud ks worker ls --cluster CLUSTER
```
{: pre}


### `ibmcloud oc worker reboot`
{: #worker-reboot-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

Restart a worker node.
{: shortdesc}

```sh
ibmcloud oc worker reboot --cluster CLUSTER --worker WORKER [--worker WORKER ...] [-f] [--hard] [-q] [--skip-master-health]
```

#### Command options
{: #worker-reboot-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`--hard`
:    Force a hard restart of a worker node by cutting off power to the worker node. Use this option if the worker node is unresponsive or the worker node has a Docker hang.

`-q`
:    Do not show the message of the day or update reminders.

`--skip-master-health`
:    Skips checking of master health before initiating action.

`-w CLUSTER`, `--worker WORKER`
:    Specify one or more worker IDs.


#### Examples
{: #worker-reboot-examples}

Restart a worker node

```sh
ibmcloud ks worker reboot --cluster CLUSTER --worker WORKER_ID
```
{: pre}


### `ibmcloud oc worker reload`
{: #worker-reload-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

Delete the data, reimage, and reinstall Kubernetes with the latest patch version on one or more worker nodes. This action cannot be undone. Classic nodes and bare metal VPC nodes are supported.
{: shortdesc}

```sh
ibmcloud oc worker reload --worker WORKER [--worker WORKER ...] [-f] [-q] [--skip-master-health]
```

#### Command options
{: #worker-reload-options}


`-f`
:    Force the command to run without user prompts.

`-q`
:    Do not show the message of the day or update reminders.

`--skip-master-health`
:    Skips checking of master health before initiating action.

`-w`, `--worker WORKER`
:    Specify one or more worker IDs.


#### Examples
{: #worker-reload-examples}

Delete the data, reimage, and reinstall Kubernetes with the latest patch version on one or more worker nodes

```sh
ibmcloud ks worker reload --worker WORKER_ID
```
{: pre}


### `ibmcloud oc worker replace`
{: #worker-replace-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

Delete a worker node and replace it with a new worker node in the same worker pool.
{: shortdesc}

```sh
ibmcloud oc worker replace --cluster CLUSTER --worker WORKER [-f] [-q] [--update]
```

#### Command options
{: #worker-replace-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`-q`
:    Do not show the message of the day or update reminders.

`--update`
:    Update the worker node to the same major and minor version of the master and the latest patch. Also updates the operating system if the worker pool operating system has been updated.

`-w CLUSTER`, `--worker WORKER`
:    Specify the worker ID. To list available workers, run `ibmcloud ks workers`.


#### Examples
{: #worker-replace-examples}

Delete a worker node and replace it with a new worker node in the same worker pool

```sh
ibmcloud ks worker replace --cluster CLUSTER --worker WORKER_ID
```
{: pre}


### `ibmcloud oc worker rm`
{: #worker-rm-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

Remove a worker node from a cluster.
{: shortdesc}

```sh
ibmcloud oc worker rm --cluster CLUSTER --worker WORKER [--worker WORKER ...] [-f] [-q]
```

#### Command options
{: #worker-rm-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`-q`
:    Do not show the message of the day or update reminders.

`-w CLUSTER`, `--worker WORKER`
:    Specify one or more worker IDs.


#### Examples
{: #worker-rm-examples}

Remove a worker node from a cluster

```sh
ibmcloud ks worker rm --cluster CLUSTER --worker WORKER_ID
```
{: pre}


### `ibmcloud oc worker update`
{: #worker-update-cli}

[Classic infrastructure]{: tag-classic-inf} 

Update one or more worker nodes in a classic cluster to a new Kubernetes version. During the update, the worker node is updated with the latest image and data is permanently deleted if not stored on persistent storage.
{: shortdesc}

```sh
ibmcloud oc worker update --cluster CLUSTER --worker WORKER [--worker WORKER ...] [-f] [-q]
```

#### Command options
{: #worker-update-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`-q`
:    Do not show the message of the day or update reminders.

`-w CLUSTER`, `--worker WORKER`
:    Specify one or more worker IDs.


#### Examples
{: #worker-update-examples}

Update one or more worker nodes in a classic cluster to a new Kubernetes version

```sh
ibmcloud ks worker update --cluster CLUSTER --worker WORKER_ID
```
{: pre}


## Worker-pool commands
{: #worker-pool-cli}

View and modify worker pools for a cluster.
{: shortdesc}


### `ibmcloud oc worker-pool create classic`
{: #worker-pool-create-classic-cli}

[Classic infrastructure]{: tag-classic-inf} 

Add a worker pool to a classic cluster. No worker nodes are created until zones are added to the worker pool.
{: shortdesc}

```sh
ibmcloud oc worker-pool create classic --cluster CLUSTER --flavor FLAVOR --name NAME --size-per-zone SIZE [--disable-disk-encrypt] [--entitlement ENTITLEMENT] [--hardware HARDWARE] [--label LABEL ...] [--operating-system SYSTEM] [--output OUTPUT] [-q]
```

#### Command options
{: #worker-pool-create-classic-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`--disable-disk-encrypt`
:    Disable encryption on a worker node.

`--entitlement ENTITLEMENT`
:    Set this flag to `ocp_entitled` only if you use this cluster with a license such as a Cloud Pak that has an OpenShift entitlement.

`--flavor FLAVOR`
:    The flavor of a worker node. To see available flavors, run `ibmcloud ks flavor ls --zone <zone name>` (for public IBM Cloud accounts) or `ibmcloud ks flavor ls` (for IBM Cloud Dedicated accounts).

`--hardware HARDWARE`
:    The level of hardware isolation for your worker node. Use `dedicated` to have available physical resources dedicated to you only, or `shared` to allow physical resources to be shared with other IBM customers. For IBM Cloud Public accounts, the default value is shared. For IBM Cloud Dedicated accounts, dedicated is the only available option.

`-l CLUSTER`, `--label LABEL`
:    Sets labels on all the workers in the worker pool.

`--name NAME`
:    Enter a name for the worker pool.

`--operating-system SYSTEM`
:    Specify the name of the operating system.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.

`--size-per-zone SIZE`
:    Specify the desired number of workers per zone in this worker pool.


#### Examples
{: #worker-pool-create-classic-examples}

Add a worker pool to a classic cluster

```sh
ibmcloud ks worker-pool create classic \
  --cluster CLUSTER \
  --flavor FLAVOR \
  --name NAME \
  --size-per-zone SIZE
```
{: pre}


### `ibmcloud oc worker-pool create help`
{: #worker-pool-create-help-cli}



Show help
{: shortdesc}

```sh
ibmcloud oc worker-pool create help
```


#### Examples
{: #worker-pool-create-help-examples}

Show help

```sh
ibmcloud ks worker-pool create help
```
{: pre}


### `ibmcloud oc worker-pool create satellite`
{: #worker-pool-create-satellite-cli}



Add a worker pool to an IBM Cloud Satellite cluster. No worker nodes are created until zones are added to the worker pool.
{: shortdesc}

```sh
ibmcloud oc worker-pool create satellite --cluster CLUSTER --host-label LABEL [--host-label LABEL ...] --name NAME --size-per-zone SIZE --zone ZONE [--entitlement ENTITLEMENT] [--label LABEL ...] [--operating-system SYSTEM] [--output OUTPUT] [-q]
```

#### Command options
{: #worker-pool-create-satellite-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`--entitlement ENTITLEMENT`
:    Set this flag to `ocp_entitled` only if you use this cluster with a license such as a Cloud Pak that has an OpenShift entitlement.

`--host-label LABEL`, `--hl LABEL`
:    Enter any labels as key-value pairs to identify the host to assign to your Satellite control plane or Red Hat OpenShift cluster. The first host that has this label and is unassigned is automatically assigned to the control plane or cluster. To find available host labels, run `ibmcloud sat host get --host <host_name_or_ID> --location <location_name_or_ID>`.

`-l LABEL`, `--label LABEL`
:    Sets labels on all the workers in the worker pool.

`--name NAME`
:    Enter a name for the worker pool.

`--operating-system SYSTEM`
:    Specify the name of the operating system.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.

`--size-per-zone SIZE`
:    Specify the desired number of workers per zone in this worker pool.

`--zone ZONE`
:    Specify the zone for the worker pool in a multizone cluster. To list available zones, run `ibmcloud ks zone ls`.


#### Examples
{: #worker-pool-create-satellite-examples}

Add a worker pool to an IBM Cloud Satellite cluster

```sh
ibmcloud ks worker-pool create satellite \
  --cluster CLUSTER \
  --host-label LABEL \
  --name NAME \
  --size-per-zone SIZE \
  --zone ZONE
```
{: pre}


### `ibmcloud oc worker-pool create vpc-classic`
{: #worker-pool-create-vpc-classic-cli}



Add a worker pool to a VPC Gen 1 cluster. No worker nodes are created until zones are added to the worker pool.
{: shortdesc}

```sh
ibmcloud oc worker-pool create vpc-classic --cluster CLUSTER --flavor FLAVOR --name NAME --size-per-zone SIZE [--entitlement ENTITLEMENT] [--label LABEL ...] [--operating-system SYSTEM] [--output OUTPUT] [-q] [--vpc-id ID]
```

#### Command options
{: #worker-pool-create-vpc-classic-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`--entitlement ENTITLEMENT`
:    Set this flag to `ocp_entitled` only if you use this cluster with a license such as a Cloud Pak that has an OpenShift entitlement.

`--flavor FLAVOR`
:    The flavor of a worker node. To see available flavors, run `ibmcloud ks flavor ls --zone <zone name>` (for public IBM Cloud accounts) or `ibmcloud ks flavor ls` (for IBM Cloud Dedicated accounts).

`-l CLUSTER`, `--label LABEL`
:    Sets labels on all the workers in the worker pool.

`--name NAME`
:    Enter a name for the worker pool.

`--operating-system SYSTEM`
:    Specify the name of the operating system.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.

`--size-per-zone SIZE`
:    Specify the desired number of workers per zone in this worker pool.

`--vpc-id ID`
:    The ID of the VPC in which to create the worker nodes, which must match the VPC that the cluster is in. To list the cluster's VPC ID, run `ibmcloud ks cluster get -c <cluster_name_or_ID>`. If this flag is not provided, then the worker pool defaults to the VPC ID of existing worker pools in the cluster.


#### Examples
{: #worker-pool-create-vpc-classic-examples}

Add a worker pool to a VPC Gen 1 cluster

```sh
ibmcloud ks worker-pool create vpc-classic \
  --cluster CLUSTER \
  --flavor FLAVOR \
  --name NAME \
  --size-per-zone SIZE
```
{: pre}


### `ibmcloud oc worker-pool create vpc-gen2`
{: #worker-pool-create-vpc-gen2-cli}

[Virtual Private Cloud]{: tag-vpc} 

Add a worker pool to a VPC Gen 2 cluster. No worker nodes are created until zones are added to the worker pool.
{: shortdesc}

```sh
ibmcloud oc worker-pool create vpc-gen2 --cluster CLUSTER --flavor FLAVOR --name NAME --size-per-zone SIZE [--crk CRK] [--disable-disk-encrypt] [--entitlement ENTITLEMENT] [--kms-account-id ID] [--kms-instance INSTANCE] [--label LABEL ...] [--operating-system SYSTEM] [--output OUTPUT] [-q] [--secondary-storage STORAGE] [--security-group GROUP ...] [--vpc-id ID]
```

#### Command options
{: #worker-pool-create-vpc-gen2-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`--crk CRK`
:    The ID of the root key in your KMS instance to use for local disk encryption. To list available root keys, run `ibmcloud ks kms crk ls --instance-id <kms_instance>`.

`--disable-disk-encrypt`
:    Disable encryption on a worker node.

`--entitlement ENTITLEMENT`
:    Set this flag to `ocp_entitled` only if you use this cluster with a license such as a Cloud Pak that has an OpenShift entitlement.

`--flavor FLAVOR`
:    The flavor of a worker node. To see available flavors, run `ibmcloud ks flavor ls --zone <zone name>` (for public IBM Cloud accounts) or `ibmcloud ks flavor ls` (for IBM Cloud Dedicated accounts).

`--kms-account-id ID`
:    The ID of the account that contains the KMS instance you want to use for local disk or secret encryption.

`--kms-instance INSTANCE`
:    The ID of the KMS instance to use for local disk encryption. To list available KMS instances, run `ibmcloud ks kms instance ls`.

`-l CLUSTER`, `--label LABEL`
:    Sets labels on all the workers in the worker pool.

`--name NAME`
:    Enter a name for the worker pool.

`--operating-system SYSTEM`
:    Specify the name of the operating system.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.

`--secondary-storage STORAGE`
:    The secondary storage option for the flavor. To view the secondary storage options that are available for a flavor, run `ibmcloud ks flavor get --provider vpc-gen2 --zone <zone name>`.

`--security-group GROUP`
:    Optional. Specify up to five security group IDs to apply to all workers in the worker pool.

`--size-per-zone SIZE`
:    Specify the desired number of workers per zone in this worker pool.

`--vpc-id ID`
:    The ID of the VPC in which to create the worker nodes, which must match the VPC that the cluster is in. To list the cluster's VPC ID, run `ibmcloud ks cluster get -c <cluster_name_or_ID>`. If this flag is not provided, then the worker pool defaults to the VPC ID of existing worker pools in the cluster.


#### Examples
{: #worker-pool-create-vpc-gen2-examples}

Add a worker pool to a VPC Gen 2 cluster

```sh
ibmcloud ks worker-pool create vpc-gen2 \
  --cluster CLUSTER \
  --flavor FLAVOR \
  --name NAME \
  --size-per-zone SIZE
```
{: pre}


### `ibmcloud oc worker-pool get`
{: #worker-pool-get-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

List the details of a worker pool.
{: shortdesc}

```sh
ibmcloud oc worker-pool get --cluster CLUSTER --worker-pool POOL [--output OUTPUT] [-q]
```

#### Command options
{: #worker-pool-get-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-p CLUSTER`, `--worker-pool POOL`
:    Specify a worker pool.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #worker-pool-get-examples}

List the details of a worker pool

```sh
ibmcloud ks worker-pool get --cluster CLUSTER --worker-pool POOL
```
{: pre}


### `ibmcloud oc worker-pool help`
{: #worker-pool-help-cli}



Show help
{: shortdesc}

```sh
ibmcloud oc worker-pool help
```


#### Examples
{: #worker-pool-help-examples}

Show help

```sh
ibmcloud ks worker-pool help
```
{: pre}


### `ibmcloud oc worker-pool label help`
{: #worker-pool-label-help-cli}



Show help
{: shortdesc}

```sh
ibmcloud oc worker-pool label help
```


#### Examples
{: #worker-pool-label-help-examples}

Show help

```sh
ibmcloud ks worker-pool label help
```
{: pre}


### `ibmcloud oc worker-pool label rm`
{: #worker-pool-label-rm-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

Remove all custom Kubernetes labels from all worker nodes in a worker pool.
{: shortdesc}

```sh
ibmcloud oc worker-pool label rm --cluster CLUSTER --worker-pool POOL [-f] [-q]
```

#### Command options
{: #worker-pool-label-rm-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`-p CLUSTER`, `--worker-pool POOL`
:    Specify a worker pool.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #worker-pool-label-rm-examples}

Remove all custom Kubernetes labels from all worker nodes in a worker pool

```sh
ibmcloud ks worker-pool label rm --cluster CLUSTER --worker-pool POOL
```
{: pre}


### `ibmcloud oc worker-pool label set`
{: #worker-pool-label-set-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

Set custom Kubernetes labels for all worker nodes in a worker pool.
{: shortdesc}

```sh
ibmcloud oc worker-pool label set --cluster CLUSTER --label LABEL [--label LABEL ...] --worker-pool POOL [-f] [-q]
```

#### Command options
{: #worker-pool-label-set-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`-l CLUSTER`, `--label LABEL`
:    Set custom Kubernetes labels in the format `key=value` for all the worker nodes in the worker pool. For multiple labels, repeat this flag. To keep any existing custom labels on the worker pool, include those labels with this flag.

`-p LABEL`, `--worker-pool POOL`
:    Specify a worker pool.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #worker-pool-label-set-examples}

Set custom Kubernetes labels for all worker nodes in a worker pool

```sh
ibmcloud ks worker-pool label set --cluster CLUSTER --label LABEL --worker-pool POOL
```
{: pre}


### `ibmcloud oc worker-pool ls`
{: #worker-pool-ls-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

List all worker pools in a cluster.
{: shortdesc}

```sh
ibmcloud oc worker-pool ls --cluster CLUSTER [--output OUTPUT] [-q]
```

#### Command options
{: #worker-pool-ls-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #worker-pool-ls-examples}

List all worker pools in a cluster

```sh
ibmcloud ks worker-pool ls --cluster CLUSTER
```
{: pre}


### `ibmcloud oc worker-pool operating-system help`
{: #worker-pool-operating-system-help-cli}



Show help
{: shortdesc}

```sh
ibmcloud oc worker-pool operating-system help
```


#### Examples
{: #worker-pool-operating-system-help-examples}

Show help

```sh
ibmcloud ks worker-pool operating-system help
```
{: pre}


### `ibmcloud oc worker-pool operating-system set`
{: #worker-pool-operating-system-set-cli}



Set the operating system. After you set the operating system, you must update your workers by running either `ibmcloud ks worker update` or `ibmcloud ks worker replace`.
{: shortdesc}

```sh
ibmcloud oc worker-pool operating-system set --cluster CLUSTER --operating-system SYSTEM --worker-pool POOL [-q]
```

#### Command options
{: #worker-pool-operating-system-set-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`--operating-system SYSTEM`
:    Specify the name of the operating system.

`-p CLUSTER`, `--worker-pool POOL`
:    Specify a worker pool.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #worker-pool-operating-system-set-examples}

Set the operating system

```sh
ibmcloud ks worker-pool operating-system set \
  --cluster CLUSTER \
  --operating-system SYSTEM \
  --worker-pool POOL
```
{: pre}


### `ibmcloud oc worker-pool rebalance`
{: #worker-pool-rebalance-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

Rebalance a worker pool in a cluster. Rebalancing adds and removes worker nodes to match the worker pool's size per zone. Satellite worker pools might remove manually assigned nodes if they do not match the worker pool's host labels.
{: shortdesc}

```sh
ibmcloud oc worker-pool rebalance --cluster CLUSTER --worker-pool POOL [-f] [-q]
```

#### Command options
{: #worker-pool-rebalance-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`-p CLUSTER`, `--worker-pool POOL`
:    Specify a worker pool.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #worker-pool-rebalance-examples}

Rebalance a worker pool in a cluster

```sh
ibmcloud ks worker-pool rebalance --cluster CLUSTER --worker-pool POOL
```
{: pre}


### `ibmcloud oc worker-pool resize`
{: #worker-pool-resize-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

Resize the worker pool to the number of workers per zone that you specify.
{: shortdesc}

```sh
ibmcloud oc worker-pool resize --cluster CLUSTER --size-per-zone SIZE --worker-pool POOL [-q]
```

#### Command options
{: #worker-pool-resize-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`-p CLUSTER`, `--worker-pool POOL`
:    Specify a worker pool.

`-q`
:    Do not show the message of the day or update reminders.

`--size-per-zone SIZE`
:    Specify the desired number of workers per zone in this worker pool.


#### Examples
{: #worker-pool-resize-examples}

Resize the worker pool to the number of workers per zone that you specify

```sh
ibmcloud ks worker-pool resize --cluster CLUSTER --size-per-zone SIZE --worker-pool POOL
```
{: pre}


### `ibmcloud oc worker-pool rm`
{: #worker-pool-rm-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

Remove a worker pool from a cluster.
{: shortdesc}

```sh
ibmcloud oc worker-pool rm --cluster CLUSTER --worker-pool POOL [-f] [-q]
```

#### Command options
{: #worker-pool-rm-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`-p CLUSTER`, `--worker-pool POOL`
:    Specify a worker pool.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #worker-pool-rm-examples}

Remove a worker pool from a cluster

```sh
ibmcloud ks worker-pool rm --cluster CLUSTER --worker-pool POOL
```
{: pre}


### `ibmcloud oc worker-pool taint help`
{: #worker-pool-taint-help-cli}



Show help
{: shortdesc}

```sh
ibmcloud oc worker-pool taint help
```


#### Examples
{: #worker-pool-taint-help-examples}

Show help

```sh
ibmcloud ks worker-pool taint help
```
{: pre}


### `ibmcloud oc worker-pool taint rm`
{: #worker-pool-taint-rm-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

Remove all Kubernetes taints from all worker nodes in a worker pool.
{: shortdesc}

```sh
ibmcloud oc worker-pool taint rm --cluster CLUSTER --worker-pool POOL [-f] [-q]
```

#### Command options
{: #worker-pool-taint-rm-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`-p CLUSTER`, `--worker-pool POOL`
:    Specify a worker pool.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #worker-pool-taint-rm-examples}

Remove all Kubernetes taints from all worker nodes in a worker pool

```sh
ibmcloud ks worker-pool taint rm --cluster CLUSTER --worker-pool POOL
```
{: pre}


### `ibmcloud oc worker-pool taint set`
{: #worker-pool-taint-set-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

Set Kubernetes taints for all worker nodes in a worker pool. Taints prevent pods without matching tolerations from running on the worker nodes.
{: shortdesc}

```sh
ibmcloud oc worker-pool taint set --cluster CLUSTER --taint TAINT [--taint TAINT ...] --worker-pool POOL [-f] [-q]
```

#### Command options
{: #worker-pool-taint-set-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`-p CLUSTER`, `--worker-pool POOL`
:    Specify a worker pool.

`-q`
:    Do not show the message of the day or update reminders.

`--taint TAINT`
:    Sets taints on all the workers in the worker pool. Specify the Kubernetes taint in the format `key=value:effect`. The `key=value` is a pair such as `env=prod` that you use to manage the worker node taint and matching pod tolerations. The `effect` is a Kubernetes taint effect such as `NoSchedule` that describes how the taint works.


#### Examples
{: #worker-pool-taint-set-examples}

Set Kubernetes taints for all worker nodes in a worker pool

```sh
ibmcloud ks worker-pool taint set --cluster CLUSTER --taint TAINT --worker-pool POOL
```
{: pre}


### `ibmcloud oc worker-pool zones`
{: #worker-pool-zones-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

View the zones attached to a worker pool.
{: shortdesc}

```sh
ibmcloud oc worker-pool zones --cluster CLUSTER --worker-pool POOL [--output OUTPUT] [-q]
```

#### Command options
{: #worker-pool-zones-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-p CLUSTER`, `--worker-pool POOL`
:    Specify a worker pool.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #worker-pool-zones-examples}

View the zones attached to a worker pool

```sh
ibmcloud ks worker-pool zones --cluster CLUSTER --worker-pool POOL
```
{: pre}


## Zone commands
{: #zone-cli}

List availability zones and modify the zones attached to a worker pool.
{: shortdesc}


### `ibmcloud oc zone add classic`
{: #zone-add-classic-cli}

[Classic infrastructure]{: tag-classic-inf} 

Add a zone to one or more worker pools in a classic cluster.
{: shortdesc}

```sh
ibmcloud oc zone add classic --cluster CLUSTER --worker-pool POOL [--worker-pool POOL ...] --zone ZONE [--output OUTPUT] [--private-vlan VLAN] [-q] (--private-only | --public-vlan VLAN)
```

#### Command options
{: #zone-add-classic-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-p CLUSTER`, `--worker-pool POOL`
:    The name of the worker pool to modify. To specify multiple worker pools, use multiple flags, such as `-p pool1 -p pool2`.

`--private-only`
:    Use this flag to prevent a public VLAN from being created. Required only when you specify the `--private-vlan` flag without specifying the `--public-vlan` flag.

`--private-vlan VLAN`
:    Specify the ID of the private VLAN. To see available VLANs, run '. When you specify a private VLAN, you must also specify either the `--public-vlan` flag or the '--private-only' flag.

`--public-vlan VLAN`
:    Specify the ID of the public VLAN. To see available VLANs, run '.

`-q`
:    Do not show the message of the day or update reminders.

`--zone ZONE`
:    Specify the zone for the worker pool in a multizone cluster. To list available zones, run `ibmcloud ks zone ls`.


#### Examples
{: #zone-add-classic-examples}

Add a zone to one or more worker pools in a classic cluster

```sh
ibmcloud ks zone add classic --cluster CLUSTER --worker-pool POOL --zone ZONE --private-only
```
{: pre}


### `ibmcloud oc zone add help`
{: #zone-add-help-cli}



Show help
{: shortdesc}

```sh
ibmcloud oc zone add help
```


#### Examples
{: #zone-add-help-examples}

Show help

```sh
ibmcloud ks zone add help
```
{: pre}


### `ibmcloud oc zone add satellite`
{: #zone-add-satellite-cli}



Add a zone to one or more worker pools in a Satellite cluster.
{: shortdesc}

```sh
ibmcloud oc zone add satellite --cluster CLUSTER --worker-pool POOL [--worker-pool POOL ...] --zone ZONE [--output OUTPUT] [-q]
```

#### Command options
{: #zone-add-satellite-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-p CLUSTER`, `--worker-pool POOL`
:    The name of the worker pool to modify. To specify multiple worker pools, use multiple flags, such as `-p pool1 -p pool2`.

`-q`
:    Do not show the message of the day or update reminders.

`--zone ZONE`
:    Specify the zone for the worker pool in a multizone cluster. To list available zones, run `ibmcloud ks zone ls`.


#### Examples
{: #zone-add-satellite-examples}

Add a zone to one or more worker pools in a Satellite cluster

```sh
ibmcloud ks zone add satellite --cluster CLUSTER --worker-pool POOL --zone ZONE
```
{: pre}


### `ibmcloud oc zone add vpc-classic`
{: #zone-add-vpc-classic-cli}



Add a zone to one or more worker pools in a VPC Gen 1 cluster.
{: shortdesc}

```sh
ibmcloud oc zone add vpc-classic --cluster CLUSTER --subnet-id ID --worker-pool POOL --zone ZONE [--output OUTPUT] [-q]
```

#### Command options
{: #zone-add-vpc-classic-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.

`--subnet-id ID`
:    The VPC subnet to assign the cluster. To list available subnets, run `ibmcloud ks subnets --provider vpc-classic --vpc-id <vpc-id> --zone <vpc-zone>`.

`--worker-pool POOL`
:    Specify a worker pool.

`--zone ZONE`
:    Specify the zone for the worker pool in a multizone cluster. To list available zones, run `ibmcloud ks zone ls`.


#### Examples
{: #zone-add-vpc-classic-examples}

Add a zone to one or more worker pools in a VPC Gen 1 cluster

```sh
ibmcloud ks zone add vpc-classic --cluster CLUSTER --subnet-id ID --worker-pool POOL --zone ZONE
```
{: pre}


### `ibmcloud oc zone add vpc-gen2`
{: #zone-add-vpc-gen2-cli}

[Virtual Private Cloud]{: tag-vpc} 

Add a zone to one or more worker pools in a VPC Gen 2 cluster.
{: shortdesc}

```sh
ibmcloud oc zone add vpc-gen2 --cluster CLUSTER --subnet-id ID --worker-pool POOL --zone ZONE [--output OUTPUT] [-q]
```

#### Command options
{: #zone-add-vpc-gen2-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.

`--subnet-id ID`
:    The VPC subnet to assign the cluster. To list available subnets, run `ibmcloud ks subnets --provider vpc-gen2 --vpc-id <vpc-id> --zone <vpc-zone>`.

`--worker-pool POOL`
:    Specify a worker pool.

`--zone ZONE`
:    Specify the zone for the worker pool in a multizone cluster. To list available zones, run `ibmcloud ks zone ls`.


#### Examples
{: #zone-add-vpc-gen2-examples}

Add a zone to one or more worker pools in a VPC Gen 2 cluster

```sh
ibmcloud ks zone add vpc-gen2 --cluster CLUSTER --subnet-id ID --worker-pool POOL --zone ZONE
```
{: pre}


### `ibmcloud oc zone help`
{: #zone-help-cli}



Show help
{: shortdesc}

```sh
ibmcloud oc zone help
```


#### Examples
{: #zone-help-examples}

Show help

```sh
ibmcloud ks zone help
```
{: pre}


### `ibmcloud oc zone ls`
{: #zone-ls-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

List all availability zones in a region.
{: shortdesc}

```sh
ibmcloud oc zone ls --provider PROVIDER [-l LOCATION ...] [--output OUTPUT] [-q] [--region-only] [--show-flavors]
```

#### Command options
{: #zone-ls-options}


`-l LOCATION`, `--location LOCATION`
:    A location to filter for. To list available locations, run `ibmcloud ks locations`.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`--provider PROVIDER`
:    Filter the list for a specific infrastructure provider. Available options: classic, vpc-classic, vpc-gen2, satellite

`-q`
:    Do not show the message of the day or update reminders.

`--region-only`
:    Show only regional data centers.

`--show-flavors`
:    Show the available worker node flavors in the zone for VPC.


#### Examples
{: #zone-ls-examples}

List all availability zones in a region

```sh
ibmcloud ks zone ls --provider PROVIDER
```
{: pre}


### `ibmcloud oc zone network-set`
{: #zone-network-set-cli}

[Classic infrastructure]{: tag-classic-inf} 

Set the network metadata in a specific zone for the given worker pools in a classic cluster.
{: shortdesc}

```sh
ibmcloud oc zone network-set --cluster CLUSTER --private-vlan VLAN --worker-pool POOL [--worker-pool POOL ...] --zone ZONE [-f] [-q] (--private-only | --public-vlan VLAN)
```

#### Command options
{: #zone-network-set-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`-p CLUSTER`, `--worker-pool POOL`
:    The name of the worker pool to modify. To specify multiple worker pools, use multiple flags, such as `-p pool1 -p pool2`.

`--private-only`
:    Unset the public VLAN so that the workers in this zone are connected to a private VLAN only.

`--private-vlan VLAN`
:    Specify the ID of the private VLAN. To see available VLANs, run '.

`--public-vlan VLAN`
:    Specify the ID of the public VLAN. To see available VLANs, run '.

`-q`
:    Do not show the message of the day or update reminders.

`--zone ZONE`
:    Specify the zone for the worker pool in a multizone cluster. To list available zones, run `ibmcloud ks zone ls`.


#### Examples
{: #zone-network-set-examples}

Set the network metadata in a specific zone for the given worker pools in a classic cluster

```sh
ibmcloud ks zone network-set \
  --cluster CLUSTER \
  --private-vlan VLAN \
  --worker-pool POOL \
  --zone ZONE \
  --private-only
```
{: pre}


### `ibmcloud oc zone rm`
{: #zone-rm-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

Remove a zone from one or more worker pools in a cluster.
{: shortdesc}

```sh
ibmcloud oc zone rm --cluster CLUSTER --worker-pool POOL [--worker-pool POOL ...] --zone ZONE [-f] [-q]
```

#### Command options
{: #zone-rm-options}


`-c`, `--cluster CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`-p CLUSTER`, `--worker-pool POOL`
:    The name of the worker pool to modify. To specify multiple worker pools, use multiple flags, such as `-p pool1 -p pool2`.

`-q`
:    Do not show the message of the day or update reminders.

`--zone ZONE`
:    Specify the zone for the worker pool in a multizone cluster. To list available zones, run `ibmcloud ks zone ls`.


#### Examples
{: #zone-rm-examples}

Remove a zone from one or more worker pools in a cluster

```sh
ibmcloud ks zone rm --cluster CLUSTER --worker-pool POOL --zone ZONE
```
{: pre}
