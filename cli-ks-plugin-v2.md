---

copyright:
  years: 2024, 2026
lastupdated: "2026-08-03"

keywords: openshift, cli reference, kubernetes cli, openshift cli, {{site.data.keyword.openshiftlong_notm}}

subcollection: openshift

content-type: cli-docs

---

{{site.data.keyword.attribute-definition-list}}

# {{site.data.keyword.openshiftlong_notm}} CLI reference
{: #kubernetes-service-cli}

Refer to these commands to create and manage **both community Kubernetes or {{site.data.keyword.redhat_openshift_notm}} clusters** in {{site.data.keyword.openshiftlong}}.
{: shortdesc}

In the command line, you are notified when updates to the `ibmcloud` CLI and plug-ins are available. Be sure to keep your CLI up-to-date so that you can use all available commands and options.


## Prerequisites
{: #ks-cli-prereq}

* Install the [{{site.data.keyword.cloud_notm}} CLI](/docs/openshift?topic=openshift-cli-install).
* Install the `ks` plug-in by running the following command:

   ```sh
   ibmcloud plugin install ks
   ```
   {: pre}

You're notified on the command line when updates to the {{site.data.keyword.cloud_notm}} CLI and plug-ins are available. Be sure to keep your CLI up to date so that you can use the latest commands. You can view the current version of all installed plug-ins by running **`ibmcloud plugin list`**.
{: tip}

## ibmcloud oc commands
{: #cli_commands}

The following tables list the `ibmcloud oc` command groups. For a complete list of all `ibmcloud oc` commands as they are structured in the CLI, see the [CLI map](/docs/openshift?topic=openshift-icks_map).
{: shortdesc}

| Command group | Description |
| --- | --- |
| [`ibmcloud oc api`](#api-cli) | View or set the API endpoint and API version for the service. |
| [`ibmcloud oc api-key`](#api-key-cli) | View information about the API key for a cluster or reset it to a new key. |
| [`ibmcloud oc credential`](#credential-cli) | Set and unset credentials that allow you to access the IBM Cloud classic infrastructure portfolio through your IBM Cloud account. |
| [`ibmcloud oc infra-permissions`](#infra-permissions-cli) | View information about infrastructure permissions that allow you to access the IBM Cloud classic infrastructure portfolio through your IBM Cloud account. |
| [`ibmcloud oc init`](#init-cli) | Initialize the Kubernetes Service plug-in and get authentication tokens. |
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


## `ibmcloud oc api` commands
{: #api-cli}

View or set the API endpoint and API version for the service.

### `ibmcloud oc api`
{: #api-cli}



View or set the API endpoint and API version for the service.
{: shortdesc}

```sh
ibmcloud oc api [--api-version VERSION] [--endpoint ENDPOINT] [--insecure] [-q] [--skip-ssl-validation]
```
{: pre}

#### Command options
{: #api-options}


`--api-version VERSION`
:    Specify the API version of the service that you want to use.

`--endpoint ENDPOINT`
:    Set the API endpoint for the service.

`--insecure`
:    Allow an insecure HTTP connection.

`-q`
:    Do not show the message of the day or update reminders.

`--skip-ssl-validation`
:    Allow insecure SSL certificates.


#### Examples
{: #api-examples}

View or set the API endpoint and API version for the service.

```sh
ibmcloud ks api \
  --endpoint ENDPOINT \
  --insecure INSECURE \
  --skip-ssl-validation IP_ADDRESS
```
{: pre}



## `ibmcloud oc api-key` commands
{: #api-key-cli}

View information about the API key for a cluster or reset it to a new key.

### `ibmcloud oc api-key info`
{: #api-key-info-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} 

View information about the API key owner for a cluster.
{: shortdesc}

```sh
ibmcloud oc api-key info --cluster CLUSTER [--output OUTPUT] [-q]
```
{: pre}

#### Command options
{: #api-key-info-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #api-key-info-examples}

View information about the API key owner for a cluster.

```sh
ibmcloud ks api-key info --cluster CLUSTER_NAME_OR_ID --output json -q
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
{: pre}

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

Replace the API key for all clusters in the specified region and targeted resource group.

```sh
ibmcloud ks api-key reset --output json --region REGION -f
```
{: pre}



## `ibmcloud oc cluster` commands
{: #cluster-cli}

View and modify cluster and cluster service settings.

### `ibmcloud oc cluster addon disable acm`
{: #cluster-addon-disable-acm-cli}



The Red Hat Advanced Cluster Management add-on
{: shortdesc}

```sh
ibmcloud oc cluster addon disable acm --cluster CLUSTER [-f] [-q]
```
{: pre}

#### Command options
{: #cluster-addon-disable-acm-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #cluster-addon-disable-acm-examples}

The Red Hat Advanced Cluster Management add-on.

```sh
ibmcloud ks cluster addon disable acm --cluster CLUSTER_NAME_OR_ID -f -q
```
{: pre}


### `ibmcloud oc cluster addon disable cluster-autoscaler`
{: #cluster-addon-disable-cluster-autoscaler-cli}



The IBM Cloud Kubernetes Service Cluster Autoscaler.
{: shortdesc}

```sh
ibmcloud oc cluster addon disable cluster-autoscaler --cluster CLUSTER [-f] [-q]
```
{: pre}

#### Command options
{: #cluster-addon-disable-cluster-autoscaler-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #cluster-addon-disable-cluster-autoscaler-examples}

The IBM Cloud Kubernetes Service Cluster Autoscaler.

```sh
ibmcloud ks cluster addon disable cluster-autoscaler --cluster CLUSTER_NAME_OR_ID -f -q
```
{: pre}


### `ibmcloud oc cluster addon disable debug-tool`
{: #cluster-addon-disable-debug-tool-cli}



The IBM Cloud Kubernetes Service Diagnostics and Debug Tool.
{: shortdesc}

```sh
ibmcloud oc cluster addon disable debug-tool --cluster CLUSTER [-f] [-q]
```
{: pre}

#### Command options
{: #cluster-addon-disable-debug-tool-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #cluster-addon-disable-debug-tool-examples}

The IBM Cloud Kubernetes Service Diagnostics and Debug Tool.

```sh
ibmcloud ks cluster addon disable debug-tool --cluster CLUSTER_NAME_OR_ID -f -q
```
{: pre}


### `ibmcloud oc cluster addon disable hpcs-router`
{: #cluster-addon-disable-hpcs-router-cli}



The IBM Cloud HPCS Router Operator add-on for Red Hat OpenShift on IBM Cloud.
{: shortdesc}

```sh
ibmcloud oc cluster addon disable hpcs-router --cluster CLUSTER [-f] [-q]
```
{: pre}

#### Command options
{: #cluster-addon-disable-hpcs-router-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #cluster-addon-disable-hpcs-router-examples}

The IBM Cloud HPCS Router Operator add-on for Red Hat OpenShift on IBM Cloud.

```sh
ibmcloud ks cluster addon disable hpcs-router --cluster CLUSTER_NAME_OR_ID -f -q
```
{: pre}


### `ibmcloud oc cluster addon disable ibm-storage-operator`
{: #cluster-addon-disable-ibm-storage-operator-cli}

The `cluster addon disable ibm-storage-operator` command is a beta feature.
{: beta}



The IBM Cloud Storage operator add-on.
{: shortdesc}

```sh
ibmcloud oc cluster addon disable ibm-storage-operator --cluster CLUSTER [-f] [-q]
```
{: pre}

#### Command options
{: #cluster-addon-disable-ibm-storage-operator-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #cluster-addon-disable-ibm-storage-operator-examples}

The IBM Cloud Storage operator add-on.

```sh
ibmcloud ks cluster addon disable ibm-storage-operator \
  --cluster CLUSTER_NAME_OR_ID \
  -f \
  -q
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
{: pre}

#### Command options
{: #cluster-addon-disable-image-key-synchronizer-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #cluster-addon-disable-image-key-synchronizer-examples}

The IBM Cloud Image Key Synchronizer add-on.

```sh
ibmcloud ks cluster addon disable image-key-synchronizer \
  --cluster CLUSTER_NAME_OR_ID \
  -f \
  -q
```
{: pre}


### `ibmcloud oc cluster addon disable knative`
{: #cluster-addon-disable-knative-cli}



The Knative serverless framework.
{: shortdesc}

```sh
ibmcloud oc cluster addon disable knative --cluster CLUSTER [-f] [-q]
```
{: pre}

#### Command options
{: #cluster-addon-disable-knative-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #cluster-addon-disable-knative-examples}

The Knative serverless framework.

```sh
ibmcloud ks cluster addon disable knative --cluster CLUSTER_NAME_OR_ID -f -q
```
{: pre}


### `ibmcloud oc cluster addon disable kube-terminal`
{: #cluster-addon-disable-kube-terminal-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

The IBM Cloud Kubernetes Service web terminal.
{: shortdesc}

```sh
ibmcloud oc cluster addon disable kube-terminal --cluster CLUSTER [-f] [-q]
```
{: pre}

#### Command options
{: #cluster-addon-disable-kube-terminal-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #cluster-addon-disable-kube-terminal-examples}

The IBM Cloud Kubernetes Service web terminal.

```sh
ibmcloud ks cluster addon disable kube-terminal --cluster CLUSTER_NAME_OR_ID -f -q
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
{: pre}

#### Command options
{: #cluster-addon-disable-openshift-data-foundation-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #cluster-addon-disable-openshift-data-foundation-examples}

The Red Hat OpenShift Data Foundation on IBM Cloud add-on.

```sh
ibmcloud ks cluster addon disable openshift-data-foundation \
  --cluster CLUSTER_NAME_OR_ID \
  -f \
  -q
```
{: pre}


### `ibmcloud oc cluster addon disable static-route`
{: #cluster-addon-disable-static-route-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

The IBM Cloud Kubernetes Service static route add-on.
{: shortdesc}

```sh
ibmcloud oc cluster addon disable static-route --cluster CLUSTER [-f] [-q]
```
{: pre}

#### Command options
{: #cluster-addon-disable-static-route-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #cluster-addon-disable-static-route-examples}

The IBM Cloud Kubernetes Service static route add-on.

```sh
ibmcloud ks cluster addon disable static-route --cluster CLUSTER_NAME_OR_ID -f -q
```
{: pre}


### `ibmcloud oc cluster addon disable vpc-block-csi-driver`
{: #cluster-addon-disable-vpc-block-csi-driver-cli}

[Classic infrastructure]{: tag-classic-inf} 

The IBM Cloud VPC Block Storage CSI Driver.
{: shortdesc}

```sh
ibmcloud oc cluster addon disable vpc-block-csi-driver --cluster CLUSTER [-f] [-q]
```
{: pre}

#### Command options
{: #cluster-addon-disable-vpc-block-csi-driver-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #cluster-addon-disable-vpc-block-csi-driver-examples}

The IBM Cloud VPC Block Storage CSI Driver.

```sh
ibmcloud ks cluster addon disable vpc-block-csi-driver \
  --cluster CLUSTER_NAME_OR_ID \
  -f \
  -q
```
{: pre}


### `ibmcloud oc cluster addon enable acm`
{: #cluster-addon-enable-acm-cli}



The Red Hat Advanced Cluster Management add-on
{: shortdesc}

```sh
ibmcloud oc cluster addon enable acm --cluster CLUSTER [-f] [--param PARAM] [-q] [--version VERSION] [-y]
```
{: pre}

#### Command options
{: #cluster-addon-enable-acm-options}


`--cluster CLUSTER`, `-c CLUSTER`
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

The Red Hat Advanced Cluster Management add-on.

```sh
ibmcloud ks cluster addon enable acm \
  --cluster CLUSTER_NAME_OR_ID \
  -y Y \
  --version VERSION
```
{: pre}


### `ibmcloud oc cluster addon enable cluster-autoscaler`
{: #cluster-addon-enable-cluster-autoscaler-cli}



The IBM Cloud Kubernetes Service Cluster Autoscaler.
{: shortdesc}

```sh
ibmcloud oc cluster addon enable cluster-autoscaler --cluster CLUSTER [-q] [--version VERSION] [-y]
```
{: pre}

#### Command options
{: #cluster-addon-enable-cluster-autoscaler-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`-q`
:    Do not show the message of the day or update reminders.

`--version VERSION`
:    Specify the version of the add-on to install. If no version is specified, the default version is installed.

`-y`
:    Enable all add-on dependencies.


#### Examples
{: #cluster-addon-enable-cluster-autoscaler-examples}

The IBM Cloud Kubernetes Service Cluster Autoscaler.

```sh
ibmcloud ks cluster addon enable cluster-autoscaler \
  --cluster CLUSTER_NAME_OR_ID \
  -y Y \
  --version VERSION
```
{: pre}


### `ibmcloud oc cluster addon enable debug-tool`
{: #cluster-addon-enable-debug-tool-cli}



The IBM Cloud Kubernetes Service Diagnostics and Debug Tool.
{: shortdesc}

```sh
ibmcloud oc cluster addon enable debug-tool --cluster CLUSTER [-q] [--version VERSION] [-y]
```
{: pre}

#### Command options
{: #cluster-addon-enable-debug-tool-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`-q`
:    Do not show the message of the day or update reminders.

`--version VERSION`
:    Specify the version of the add-on to install. If no version is specified, the default version is installed.

`-y`
:    Enable all add-on dependencies.


#### Examples
{: #cluster-addon-enable-debug-tool-examples}

The IBM Cloud Kubernetes Service Diagnostics and Debug Tool.

```sh
ibmcloud ks cluster addon enable debug-tool \
  --cluster CLUSTER_NAME_OR_ID \
  -y Y \
  --version VERSION
```
{: pre}


### `ibmcloud oc cluster addon enable hpcs-router`
{: #cluster-addon-enable-hpcs-router-cli}



The IBM Cloud HPCS Router Operator add-on for Red Hat OpenShift on IBM Cloud.
{: shortdesc}

```sh
ibmcloud oc cluster addon enable hpcs-router --cluster CLUSTER [-q] [--version VERSION] [-y]
```
{: pre}

#### Command options
{: #cluster-addon-enable-hpcs-router-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`-q`
:    Do not show the message of the day or update reminders.

`--version VERSION`
:    Specify the version of the add-on to install. If no version is specified, the default version is installed.

`-y`
:    Enable all add-on dependencies.


#### Examples
{: #cluster-addon-enable-hpcs-router-examples}

The IBM Cloud HPCS Router Operator add-on for Red Hat OpenShift on IBM Cloud.

```sh
ibmcloud ks cluster addon enable hpcs-router \
  --cluster CLUSTER_NAME_OR_ID \
  -y Y \
  --version VERSION
```
{: pre}


### `ibmcloud oc cluster addon enable ibm-storage-operator`
{: #cluster-addon-enable-ibm-storage-operator-cli}

The `cluster addon enable ibm-storage-operator` command is a beta feature.
{: beta}



The IBM Cloud Storage operator add-on.
{: shortdesc}

```sh
ibmcloud oc cluster addon enable ibm-storage-operator --cluster CLUSTER [-q] [--version VERSION] [-y]
```
{: pre}

#### Command options
{: #cluster-addon-enable-ibm-storage-operator-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`-q`
:    Do not show the message of the day or update reminders.

`--version VERSION`
:    Specify the version of the add-on to install. If no version is specified, the default version is installed.

`-y`
:    Enable all add-on dependencies.


#### Examples
{: #cluster-addon-enable-ibm-storage-operator-examples}

The IBM Cloud Storage operator add-on.

```sh
ibmcloud ks cluster addon enable ibm-storage-operator \
  --cluster CLUSTER_NAME_OR_ID \
  -y Y \
  --version VERSION
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
{: pre}

#### Command options
{: #cluster-addon-enable-image-key-synchronizer-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`-q`
:    Do not show the message of the day or update reminders.

`--version VERSION`
:    Specify the version of the add-on to install. If no version is specified, the default version is installed.

`-y`
:    Enable all add-on dependencies.


#### Examples
{: #cluster-addon-enable-image-key-synchronizer-examples}

The IBM Cloud Image Key Synchronizer add-on.

```sh
ibmcloud ks cluster addon enable image-key-synchronizer \
  --cluster CLUSTER_NAME_OR_ID \
  -y Y \
  --version VERSION
```
{: pre}


### `ibmcloud oc cluster addon enable istio-extras`
{: #cluster-addon-enable-istio-extras-cli}

The `cluster addon enable istio-extras` command is deprecated.
{: deprecated}



Extra components for Istio, including Grafana, Jaeger, and Kiali.
{: shortdesc}

```sh
ibmcloud oc cluster addon enable istio-extras --cluster CLUSTER [-q] [--version VERSION] [-y]
```
{: pre}

#### Command options
{: #cluster-addon-enable-istio-extras-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`-q`
:    Do not show the message of the day or update reminders.

`--version VERSION`
:    Specify the version of the add-on to install. If no version is specified, the default version is installed.

`-y`
:    Enable all add-on dependencies.


#### Examples
{: #cluster-addon-enable-istio-extras-examples}

Extra components for Istio, including Grafana, Jaeger, and Kiali.

```sh
ibmcloud ks cluster addon enable istio-extras \
  --cluster CLUSTER_NAME_OR_ID \
  -y Y \
  --version VERSION
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
{: pre}

#### Command options
{: #cluster-addon-enable-istio-sample-bookinfo-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`-q`
:    Do not show the message of the day or update reminders.

`--version VERSION`
:    Specify the version of the add-on to install. If no version is specified, the default version is installed.

`-y`
:    Enable all add-on dependencies.


#### Examples
{: #cluster-addon-enable-istio-sample-bookinfo-examples}

The BookInfo sample application for Istio.

```sh
ibmcloud ks cluster addon enable istio-sample-bookinfo \
  --cluster CLUSTER_NAME_OR_ID \
  -y Y \
  --version VERSION
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
{: pre}

#### Command options
{: #cluster-addon-enable-openshift-data-foundation-options}


`--cluster CLUSTER`, `-c CLUSTER`
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

The Red Hat OpenShift Data Foundation on IBM Cloud add-on.

```sh
ibmcloud ks cluster addon enable openshift-data-foundation \
  --cluster CLUSTER_NAME_OR_ID \
  -y Y \
  --version VERSION
```
{: pre}


### `ibmcloud oc cluster addon enable static-route`
{: #cluster-addon-enable-static-route-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

The IBM Cloud Kubernetes Service static route add-on.
{: shortdesc}

```sh
ibmcloud oc cluster addon enable static-route --cluster CLUSTER [-q] [--version VERSION] [-y]
```
{: pre}

#### Command options
{: #cluster-addon-enable-static-route-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`-q`
:    Do not show the message of the day or update reminders.

`--version VERSION`
:    Specify the version of the add-on to install. If no version is specified, the default version is installed.

`-y`
:    Enable all add-on dependencies.


#### Examples
{: #cluster-addon-enable-static-route-examples}

The IBM Cloud Kubernetes Service static route add-on.

```sh
ibmcloud ks cluster addon enable static-route \
  --cluster CLUSTER_NAME_OR_ID \
  -y Y \
  --version VERSION
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
{: pre}

#### Command options
{: #cluster-addon-get-options}


`--addon ADDON`
:    The add-on name or ID.

`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #cluster-addon-get-examples}

View details of an installed add-on.

```sh
ibmcloud ks cluster addon get --cluster CLUSTER_NAME_OR_ID --addon ADDON --output json
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
{: pre}

#### Command options
{: #cluster-addon-ls-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #cluster-addon-ls-examples}

List enabled add-ons.

```sh
ibmcloud ks cluster addon ls --cluster CLUSTER_NAME_OR_ID --output json -q
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
{: pre}

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

View installation options for an add-on.

```sh
ibmcloud ks cluster addon options --addon ADDON --version VERSION --output json
```
{: pre}


### `ibmcloud oc cluster addon update acm`
{: #cluster-addon-update-acm-cli}



The Red Hat Advanced Cluster Management add-on
{: shortdesc}

```sh
ibmcloud oc cluster addon update acm --cluster CLUSTER [-f] [-q] [--version VERSION] [-y]
```
{: pre}

#### Command options
{: #cluster-addon-update-acm-options}


`--cluster CLUSTER`, `-c CLUSTER`
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

The Red Hat Advanced Cluster Management add-on.

```sh
ibmcloud ks cluster addon update acm \
  --cluster CLUSTER_NAME_OR_ID \
  -y Y \
  --version VERSION
```
{: pre}


### `ibmcloud oc cluster addon update alb-oauth-proxy`
{: #cluster-addon-update-alb-oauth-proxy-cli}



The IBM Cloud Kubernetes Service ALB OAuth Proxy add-on.
{: shortdesc}

```sh
ibmcloud oc cluster addon update alb-oauth-proxy --cluster CLUSTER [-f] [-q] [--version VERSION] [-y]
```
{: pre}

#### Command options
{: #cluster-addon-update-alb-oauth-proxy-options}


`--cluster CLUSTER`, `-c CLUSTER`
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

The IBM Cloud Kubernetes Service ALB OAuth Proxy add-on.

```sh
ibmcloud ks cluster addon update alb-oauth-proxy \
  --cluster CLUSTER_NAME_OR_ID \
  -y Y \
  --version VERSION
```
{: pre}


### `ibmcloud oc cluster addon update cluster-autoscaler`
{: #cluster-addon-update-cluster-autoscaler-cli}



The IBM Cloud Kubernetes Service Cluster Autoscaler.
{: shortdesc}

```sh
ibmcloud oc cluster addon update cluster-autoscaler --cluster CLUSTER [-f] [-q] [--version VERSION] [-y]
```
{: pre}

#### Command options
{: #cluster-addon-update-cluster-autoscaler-options}


`--cluster CLUSTER`, `-c CLUSTER`
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

The IBM Cloud Kubernetes Service Cluster Autoscaler.

```sh
ibmcloud ks cluster addon update cluster-autoscaler \
  --cluster CLUSTER_NAME_OR_ID \
  -y Y \
  --version VERSION
```
{: pre}


### `ibmcloud oc cluster addon update debug-tool`
{: #cluster-addon-update-debug-tool-cli}



The IBM Cloud Kubernetes Service Diagnostics and Debug Tool.
{: shortdesc}

```sh
ibmcloud oc cluster addon update debug-tool --cluster CLUSTER [-f] [-q] [--version VERSION] [-y]
```
{: pre}

#### Command options
{: #cluster-addon-update-debug-tool-options}


`--cluster CLUSTER`, `-c CLUSTER`
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

The IBM Cloud Kubernetes Service Diagnostics and Debug Tool.

```sh
ibmcloud ks cluster addon update debug-tool \
  --cluster CLUSTER_NAME_OR_ID \
  -y Y \
  --version VERSION
```
{: pre}


### `ibmcloud oc cluster addon update headlamp`
{: #cluster-addon-update-headlamp-cli}

The `cluster addon update headlamp` command is a beta feature.
{: beta}



The IBM Cloud Kubernetes Service Headlamp add-on.
{: shortdesc}

```sh
ibmcloud oc cluster addon update headlamp --cluster CLUSTER [-f] [-q] [--version VERSION] [-y]
```
{: pre}

#### Command options
{: #cluster-addon-update-headlamp-options}


`--cluster CLUSTER`, `-c CLUSTER`
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

The IBM Cloud Kubernetes Service Headlamp add-on.

```sh
ibmcloud ks cluster addon update headlamp \
  --cluster CLUSTER_NAME_OR_ID \
  -y Y \
  --version VERSION
```
{: pre}


### `ibmcloud oc cluster addon update hpcs-router`
{: #cluster-addon-update-hpcs-router-cli}



The IBM Cloud HPCS Router Operator add-on for Red Hat OpenShift on IBM Cloud.
{: shortdesc}

```sh
ibmcloud oc cluster addon update hpcs-router --cluster CLUSTER [-f] [-q] [--version VERSION] [-y]
```
{: pre}

#### Command options
{: #cluster-addon-update-hpcs-router-options}


`--cluster CLUSTER`, `-c CLUSTER`
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

The IBM Cloud HPCS Router Operator add-on for Red Hat OpenShift on IBM Cloud.

```sh
ibmcloud ks cluster addon update hpcs-router \
  --cluster CLUSTER_NAME_OR_ID \
  -y Y \
  --version VERSION
```
{: pre}


### `ibmcloud oc cluster addon update ibm-storage-operator`
{: #cluster-addon-update-ibm-storage-operator-cli}

The `cluster addon update ibm-storage-operator` command is a beta feature.
{: beta}



The IBM Cloud Storage operator add-on.
{: shortdesc}

```sh
ibmcloud oc cluster addon update ibm-storage-operator --cluster CLUSTER [-f] [-q] [--version VERSION] [-y]
```
{: pre}

#### Command options
{: #cluster-addon-update-ibm-storage-operator-options}


`--cluster CLUSTER`, `-c CLUSTER`
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

The IBM Cloud Storage operator add-on.

```sh
ibmcloud ks cluster addon update ibm-storage-operator \
  --cluster CLUSTER_NAME_OR_ID \
  -y Y \
  --version VERSION
```
{: pre}


### `ibmcloud oc cluster addon update image-key-synchronizer`
{: #cluster-addon-update-image-key-synchronizer-cli}



The IBM Cloud Image Key Synchronizer add-on.
{: shortdesc}

```sh
ibmcloud oc cluster addon update image-key-synchronizer --cluster CLUSTER [-f] [-q] [--version VERSION] [-y]
```
{: pre}

#### Command options
{: #cluster-addon-update-image-key-synchronizer-options}


`--cluster CLUSTER`, `-c CLUSTER`
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

The IBM Cloud Image Key Synchronizer add-on.

```sh
ibmcloud ks cluster addon update image-key-synchronizer \
  --cluster CLUSTER_NAME_OR_ID \
  -y Y \
  --version VERSION
```
{: pre}


### `ibmcloud oc cluster addon update istio`
{: #cluster-addon-update-istio-cli}



The managed Istio service mesh.
{: shortdesc}

```sh
ibmcloud oc cluster addon update istio --cluster CLUSTER [-f] [-q] [--version VERSION] [-y]
```
{: pre}

#### Command options
{: #cluster-addon-update-istio-options}


`--cluster CLUSTER`, `-c CLUSTER`
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

The managed Istio service mesh.

```sh
ibmcloud ks cluster addon update istio \
  --cluster CLUSTER_NAME_OR_ID \
  -y Y \
  --version VERSION
```
{: pre}


### `ibmcloud oc cluster addon update istio-extras`
{: #cluster-addon-update-istio-extras-cli}

The `cluster addon update istio-extras` command is deprecated.
{: deprecated}



Extra components for Istio, including Grafana, Jaeger, and Kiali.
{: shortdesc}

```sh
ibmcloud oc cluster addon update istio-extras --cluster CLUSTER [-f] [-q] [--version VERSION] [-y]
```
{: pre}

#### Command options
{: #cluster-addon-update-istio-extras-options}


`--cluster CLUSTER`, `-c CLUSTER`
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

Extra components for Istio, including Grafana, Jaeger, and Kiali.

```sh
ibmcloud ks cluster addon update istio-extras \
  --cluster CLUSTER_NAME_OR_ID \
  -y Y \
  --version VERSION
```
{: pre}


### `ibmcloud oc cluster addon update istio-sample-bookinfo`
{: #cluster-addon-update-istio-sample-bookinfo-cli}

The `cluster addon update istio-sample-bookinfo` command is deprecated.
{: deprecated}



The BookInfo sample application for Istio.
{: shortdesc}

```sh
ibmcloud oc cluster addon update istio-sample-bookinfo --cluster CLUSTER [-f] [-q] [--version VERSION] [-y]
```
{: pre}

#### Command options
{: #cluster-addon-update-istio-sample-bookinfo-options}


`--cluster CLUSTER`, `-c CLUSTER`
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

The BookInfo sample application for Istio.

```sh
ibmcloud ks cluster addon update istio-sample-bookinfo \
  --cluster CLUSTER_NAME_OR_ID \
  -y Y \
  --version VERSION
```
{: pre}


### `ibmcloud oc cluster addon update knative`
{: #cluster-addon-update-knative-cli}



The Knative serverless framework.
{: shortdesc}

```sh
ibmcloud oc cluster addon update knative --cluster CLUSTER [-f] [-q] [--version VERSION] [-y]
```
{: pre}

#### Command options
{: #cluster-addon-update-knative-options}


`--cluster CLUSTER`, `-c CLUSTER`
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

The Knative serverless framework.

```sh
ibmcloud ks cluster addon update knative \
  --cluster CLUSTER_NAME_OR_ID \
  -y Y \
  --version VERSION
```
{: pre}


### `ibmcloud oc cluster addon update kube-terminal`
{: #cluster-addon-update-kube-terminal-cli}



The IBM Cloud Kubernetes Service web terminal.
{: shortdesc}

```sh
ibmcloud oc cluster addon update kube-terminal --cluster CLUSTER [-f] [-q] [--version VERSION] [-y]
```
{: pre}

#### Command options
{: #cluster-addon-update-kube-terminal-options}


`--cluster CLUSTER`, `-c CLUSTER`
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

The IBM Cloud Kubernetes Service web terminal.

```sh
ibmcloud ks cluster addon update kube-terminal \
  --cluster CLUSTER_NAME_OR_ID \
  -y Y \
  --version VERSION
```
{: pre}


### `ibmcloud oc cluster addon update openshift-data-foundation`
{: #cluster-addon-update-openshift-data-foundation-cli}



The Red Hat OpenShift Data Foundation on IBM Cloud add-on
{: shortdesc}

```sh
ibmcloud oc cluster addon update openshift-data-foundation --cluster CLUSTER [-f] [-q] [--version VERSION] [-y]
```
{: pre}

#### Command options
{: #cluster-addon-update-openshift-data-foundation-options}


`--cluster CLUSTER`, `-c CLUSTER`
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

The Red Hat OpenShift Data Foundation on IBM Cloud add-on.

```sh
ibmcloud ks cluster addon update openshift-data-foundation \
  --cluster CLUSTER_NAME_OR_ID \
  -y Y \
  --version VERSION
```
{: pre}


### `ibmcloud oc cluster addon update static-route`
{: #cluster-addon-update-static-route-cli}



The IBM Cloud Kubernetes Service static route add-on.
{: shortdesc}

```sh
ibmcloud oc cluster addon update static-route --cluster CLUSTER [-f] [-q] [--version VERSION] [-y]
```
{: pre}

#### Command options
{: #cluster-addon-update-static-route-options}


`--cluster CLUSTER`, `-c CLUSTER`
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

The IBM Cloud Kubernetes Service static route add-on.

```sh
ibmcloud ks cluster addon update static-route \
  --cluster CLUSTER_NAME_OR_ID \
  -y Y \
  --version VERSION
```
{: pre}


### `ibmcloud oc cluster addon update vpc-block-csi-driver`
{: #cluster-addon-update-vpc-block-csi-driver-cli}



The IBM Cloud VPC Block Storage CSI Driver.
{: shortdesc}

```sh
ibmcloud oc cluster addon update vpc-block-csi-driver --cluster CLUSTER [-f] [-q] [--version VERSION] [-y]
```
{: pre}

#### Command options
{: #cluster-addon-update-vpc-block-csi-driver-options}


`--cluster CLUSTER`, `-c CLUSTER`
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

The IBM Cloud VPC Block Storage CSI Driver.

```sh
ibmcloud ks cluster addon update vpc-block-csi-driver \
  --cluster CLUSTER_NAME_OR_ID \
  -y Y \
  --version VERSION
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
{: pre}

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

List supported versions for managed add-ons.

```sh
ibmcloud ks cluster addon versions \
  --output json \
  --addon ADDON \
  --show-defaults SHOW-DEFAULTS
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
{: pre}

#### Command options
{: #cluster-ca-create-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #cluster-ca-create-examples}

Create a CA certificate for your cluster.

```sh
ibmcloud ks cluster ca create --cluster CLUSTER_NAME_OR_ID -f -q
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
{: pre}

#### Command options
{: #cluster-ca-get-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #cluster-ca-get-examples}

View the details of a cluster's CA certificate.

```sh
ibmcloud ks cluster ca get --cluster CLUSTER_NAME_OR_ID --output json -q
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
{: pre}

#### Command options
{: #cluster-ca-rotate-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #cluster-ca-rotate-examples}

Rotate the CA certificates of a cluster, which requires that you previously created CA certificates.

```sh
ibmcloud ks cluster ca rotate --cluster CLUSTER_NAME_OR_ID -f -q
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
{: pre}

#### Command options
{: #cluster-ca-status-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #cluster-ca-status-examples}

View the rotation status of CA certificates for a cluster.

```sh
ibmcloud ks cluster ca status --cluster CLUSTER_NAME_OR_ID -q
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
{: pre}

#### Command options
{: #cluster-config-options}


`--admin`
:    Retrieve administrator certificates and PEM keys.

`--cluster CLUSTER`, `-c CLUSTER`
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

Download the Kubernetes configuration files and certificates to connect to your cluster by using kubectl commands.

```sh
ibmcloud ks cluster config --cluster CLUSTER_NAME_OR_ID --admin --network
```
{: pre}


### `ibmcloud oc cluster create classic`
{: #cluster-create-classic-cli}

[Classic infrastructure]{: tag-classic-inf} 

Create a cluster with worker nodes on classic infrastructure.
{: shortdesc}

```sh
ibmcloud oc cluster create classic --flavor FLAVOR --name NAME --zone ZONE [--disable-disk-encrypt] [--entitlement ENTITLEMENT] [--hardware HARDWARE] [--location LOCATION] [--no-subnet] [--operating-system SYSTEM] [--pod-subnet SUBNET] [--private-service-endpoint] [--private-vlan VLAN] [--public-service-endpoint] [-q] [--service-subnet SUBNET] [--skip-advance-permissions-check] [--sm-group GROUP] [--sm-instance INSTANCE] [--version VERSION] [--workers COUNT] --private-only
```
{: pre}

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

Create a cluster with worker nodes on classic infrastructure.

```sh
ibmcloud ks cluster create classic \
  --private-only \
  --name NAME \
  --zone ZONE \
  --private-vlan VLAN_ID
```
{: pre}


### `ibmcloud oc cluster create satellite`
{: #cluster-create-satellite-cli}



Create an IBM Cloud Satellite cluster on your own infrastructure.
{: shortdesc}

```sh
ibmcloud oc cluster create satellite --location LOCATION --name NAME --version VERSION [--enable-config-admin] [--entitlement ENTITLEMENT] [--host-label LABEL ...] [--infrastructure-topology TOPOLOGY] [--operating-system SYSTEM] [--pod-network-interface-selection SELECTION] [--pod-subnet SUBNET] [--pull-secret SECRET] [-q] [--service-subnet SUBNET] [--sm-group GROUP] [--sm-instance INSTANCE] [--workers COUNT] [--zone ZONE]
```
{: pre}

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

Create an IBM Cloud Satellite cluster on your own infrastructure.

```sh
ibmcloud ks cluster create satellite \
  --workers COUNT \
  --host-label HOSTNAME \
  --location LOCATION \
  --name NAME
```
{: pre}


### `ibmcloud oc cluster create vpc-classic`
{: #cluster-create-vpc-classic-cli}



Create a cluster with worker nodes on Virtual Private Cloud (VPC) Gen 1 infrastructure.
{: shortdesc}

```sh
ibmcloud oc cluster create vpc-classic --flavor FLAVOR --name NAME --subnet-id ID --vpc-id ID --zone ZONE [--disable-public-service-endpoint] [--entitlement ENTITLEMENT] [--operating-system SYSTEM] [--pod-subnet SUBNET] [-q] [--service-subnet SUBNET] [--sm-group GROUP] [--sm-instance INSTANCE] [--version VERSION] [--workers COUNT]
```
{: pre}

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

Create a cluster with worker nodes on Virtual Private Cloud (VPC) Gen 1 infrastructure.

```sh
ibmcloud ks cluster create vpc-classic --name NAME --zone ZONE --vpc-id VPC_ID
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
{: pre}

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

Create a cluster with worker nodes on Virtual Private Cloud (VPC) Gen 2 infrastructure.

```sh
ibmcloud ks cluster create vpc-gen2 \
  --cos-instance INSTANCE_ID \
  --name NAME \
  --zone ZONE \
  --vpc-id VPC_ID
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
{: pre}

#### Command options
{: #cluster-get-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.

`--show-resources`
:    Show additional cluster resources such as add-ons, VLANs, and subnets.


#### Examples
{: #cluster-get-examples}

Get the details of a registered cluster.

```sh
ibmcloud sat cluster get --cluster CLUSTER_NAME_OR_ID --output json -q
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
{: pre}

#### Command options
{: #cluster-image-security-disable-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #cluster-image-security-disable-examples}

Disable image security enforcement in your cluster.

```sh
ibmcloud ks cluster image-security disable --cluster CLUSTER_NAME_OR_ID -q
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
{: pre}

#### Command options
{: #cluster-image-security-enable-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #cluster-image-security-enable-examples}

Enable image security enforcement in your cluster.

```sh
ibmcloud ks cluster image-security enable --cluster CLUSTER_NAME_OR_ID -f -q
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
{: pre}

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

List all registered clusters in your IBM Cloud account.

```sh
ibmcloud sat cluster ls --filter FILTER --limit LIMIT --output json
```
{: pre}


### `ibmcloud oc cluster master console-oauth-access get`
{: #cluster-master-console-oauth-access-get-cli}



Get the OpenShift web console and OAuth server access type.
{: shortdesc}

```sh
ibmcloud oc cluster master console-oauth-access get --cluster CLUSTER [--output OUTPUT] [-q]
```
{: pre}

#### Command options
{: #cluster-master-console-oauth-access-get-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #cluster-master-console-oauth-access-get-examples}

Get the OpenShift web console and OAuth server access type.

```sh
ibmcloud ks cluster master console-oauth-access get \
  --cluster CLUSTER_NAME_OR_ID \
  --output json \
  -q
```
{: pre}


### `ibmcloud oc cluster master console-oauth-access set`
{: #cluster-master-console-oauth-access-set-cli}



Set the OpenShift web console and OAuth server access type.
{: shortdesc}

```sh
ibmcloud oc cluster master console-oauth-access set --cluster CLUSTER [-f] [-q] [--type TYPE]
```
{: pre}

#### Command options
{: #cluster-master-console-oauth-access-set-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`-q`
:    Do not show the message of the day or update reminders.

`--type TYPE`
:    Specify the OpenShift web console and OAuth server access type. Accepted values: `vpe-gateway`, `legacy`


#### Examples
{: #cluster-master-console-oauth-access-set-examples}

Set the OpenShift web console and OAuth server access type.

```sh
ibmcloud ks cluster master console-oauth-access set \
  --cluster CLUSTER_NAME_OR_ID \
  --type TYPE \
  -f
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
{: pre}

#### Command options
{: #cluster-master-pod-security-get-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #cluster-master-pod-security-get-examples}

View the PodSecurity admission configuration for a cluster's Kubernetes API server.

```sh
ibmcloud ks cluster master pod-security get \
  --cluster CLUSTER_NAME_OR_ID \
  --output json \
  -q
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
{: pre}

#### Command options
{: #cluster-master-pod-security-policy-disable-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #cluster-master-pod-security-policy-disable-examples}

Disable PodSecurityPolicy for a cluster's Kubernetes API server.

```sh
ibmcloud ks cluster master pod-security policy disable --cluster CLUSTER_NAME_OR_ID -q
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
{: pre}

#### Command options
{: #cluster-master-pod-security-policy-enable-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #cluster-master-pod-security-policy-enable-examples}

Enable PodSecurityPolicy for a cluster's Kubernetes API server.

```sh
ibmcloud ks cluster master pod-security policy enable --cluster CLUSTER_NAME_OR_ID -q
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
{: pre}

#### Command options
{: #cluster-master-pod-security-policy-get-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #cluster-master-pod-security-policy-get-examples}

View the PodSecurityPolicy configuration for a cluster's Kubernetes API server.

```sh
ibmcloud ks cluster master pod-security policy get \
  --cluster CLUSTER_NAME_OR_ID \
  --output json \
  -q
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
{: pre}

#### Command options
{: #cluster-master-pod-security-set-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`--config-file FILE`
:    The filepath of a custom PodSecurity configuration. If not specified, the Kubernetes defaults are applied. For more information, see https://ibm.biz/BdPtUB

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #cluster-master-pod-security-set-examples}

Set and enable the PodSecurity admission configuration for a cluster's Kubernetes API server.

```sh
ibmcloud ks cluster master pod-security set \
  --cluster CLUSTER_NAME_OR_ID \
  --config-file FILE_PATH \
  -q
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
{: pre}

#### Command options
{: #cluster-master-pod-security-unset-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #cluster-master-pod-security-unset-examples}

Remove the PodSecurity admission configuration for a cluster's Kubernetes API server.

```sh
ibmcloud ks cluster master pod-security unset --cluster CLUSTER_NAME_OR_ID -q
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
{: pre}

#### Command options
{: #cluster-master-private-service-endpoint-allowlist-add-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`-q`
:    Do not show the message of the day or update reminders.

`--subnet SUBNET`
:    Specify the subnet CIDR.


#### Examples
{: #cluster-master-private-service-endpoint-allowlist-add-examples}

Add subnets to a cluster's private service endpoint allowlist.

```sh
ibmcloud ks cluster master private-service-endpoint allowlist add \
  --cluster CLUSTER_NAME_OR_ID \
  --subnet SUBNET_CIDR \
  -q
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
{: pre}

#### Command options
{: #cluster-master-private-service-endpoint-allowlist-disable-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #cluster-master-private-service-endpoint-allowlist-disable-examples}

Disable the allowlist.

```sh
ibmcloud ks cluster master private-service-endpoint allowlist disable \
  --cluster CLUSTER_NAME_OR_ID \
  -f \
  -q
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
{: pre}

#### Command options
{: #cluster-master-private-service-endpoint-allowlist-enable-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #cluster-master-private-service-endpoint-allowlist-enable-examples}

Enable the allowlist.

```sh
ibmcloud ks cluster master private-service-endpoint allowlist enable \
  --cluster CLUSTER_NAME_OR_ID \
  -f \
  -q
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
{: pre}

#### Command options
{: #cluster-master-private-service-endpoint-allowlist-get-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #cluster-master-private-service-endpoint-allowlist-get-examples}

Get a cluster's private service endpoint allowlist.

```sh
ibmcloud ks cluster master private-service-endpoint allowlist get \
  --cluster CLUSTER_NAME_OR_ID \
  -q
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
{: pre}

#### Command options
{: #cluster-master-private-service-endpoint-allowlist-rm-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`-q`
:    Do not show the message of the day or update reminders.

`--subnet SUBNET`
:    Specify the subnet CIDR.


#### Examples
{: #cluster-master-private-service-endpoint-allowlist-rm-examples}

Remove subnets from a cluster's private service endpoint allowlist.

```sh
ibmcloud ks cluster master private-service-endpoint allowlist rm \
  --cluster CLUSTER_NAME_OR_ID \
  -f \
  --subnet SUBNET_CIDR
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
{: pre}

#### Command options
{: #cluster-master-private-service-endpoint-enable-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`-q`
:    Do not show the message of the day or update reminders.

`-y`
:    If the feature requires further action, such as reloading workers or refreshing the cluster master, then perform those actions with no user prompts.


#### Examples
{: #cluster-master-private-service-endpoint-enable-examples}

Enable the private service endpoint to make the master privately accessible.

```sh
ibmcloud ks cluster master private-service-endpoint enable \
  --cluster CLUSTER_NAME_OR_ID \
  -f \
  -y Y
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
{: pre}

#### Command options
{: #cluster-master-public-service-endpoint-disable-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`-q`
:    Do not show the message of the day or update reminders.

`-y`
:    If the feature requires further action, such as reloading workers or refreshing the cluster master, then perform those actions with no user prompts.


#### Examples
{: #cluster-master-public-service-endpoint-disable-examples}

Disable the public service endpoint to make the master only privately accessible.

```sh
ibmcloud ks cluster master public-service-endpoint disable \
  --cluster CLUSTER_NAME_OR_ID \
  -f \
  -y Y
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
{: pre}

#### Command options
{: #cluster-master-public-service-endpoint-enable-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`-q`
:    Do not show the message of the day or update reminders.

`-y`
:    If the feature requires further action, such as reloading workers or refreshing the cluster master, then perform those actions with no user prompts.


#### Examples
{: #cluster-master-public-service-endpoint-enable-examples}

Enable the public service endpoint to make the master publicly accessible.

```sh
ibmcloud ks cluster master public-service-endpoint enable \
  --cluster CLUSTER_NAME_OR_ID \
  -f \
  -y Y
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
{: pre}

#### Command options
{: #cluster-master-refresh-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #cluster-master-refresh-examples}

Restart the cluster master nodes to apply new Kubernetes API configuration changes.

```sh
ibmcloud ks cluster master refresh --cluster CLUSTER_NAME_OR_ID -q
```
{: pre}


### `ibmcloud oc cluster master satellite-service-endpoint allowlist add`
{: #cluster-master-satellite-service-endpoint-allowlist-add-cli}



Add subnets to a Satellite cluster's service endpoint allowlist.
{: shortdesc}

```sh
ibmcloud oc cluster master satellite-service-endpoint allowlist add --cluster CLUSTER --subnet SUBNET [--subnet SUBNET ...] [-q]
```
{: pre}

#### Command options
{: #cluster-master-satellite-service-endpoint-allowlist-add-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`-q`
:    Do not show the message of the day or update reminders.

`--subnet SUBNET`
:    Specify the subnet CIDR.


#### Examples
{: #cluster-master-satellite-service-endpoint-allowlist-add-examples}

Add subnets to a Satellite cluster's service endpoint allowlist.

```sh
ibmcloud ks cluster master satellite-service-endpoint allowlist add \
  --cluster CLUSTER_NAME_OR_ID \
  --subnet SUBNET_CIDR \
  -q
```
{: pre}


### `ibmcloud oc cluster master satellite-service-endpoint allowlist disable`
{: #cluster-master-satellite-service-endpoint-allowlist-disable-cli}



Disable the allowlist for a Satellite cluster. When disabled, authorized requests to the cluster master from any subnet are permitted through the Satellite service endpoint.
{: shortdesc}

```sh
ibmcloud oc cluster master satellite-service-endpoint allowlist disable --cluster CLUSTER [-f] [-q]
```
{: pre}

#### Command options
{: #cluster-master-satellite-service-endpoint-allowlist-disable-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #cluster-master-satellite-service-endpoint-allowlist-disable-examples}

Disable the allowlist for a Satellite cluster.

```sh
ibmcloud ks cluster master satellite-service-endpoint allowlist disable \
  --cluster CLUSTER_NAME_OR_ID \
  -f \
  -q
```
{: pre}


### `ibmcloud oc cluster master satellite-service-endpoint allowlist enable`
{: #cluster-master-satellite-service-endpoint-allowlist-enable-cli}



Enable the allowlist for a Satellite cluster. When enabled, only authorized requests to the cluster master from subnets in the allowlist are permitted through the Satellite service endpoint.
{: shortdesc}

```sh
ibmcloud oc cluster master satellite-service-endpoint allowlist enable --cluster CLUSTER [-f] [-q]
```
{: pre}

#### Command options
{: #cluster-master-satellite-service-endpoint-allowlist-enable-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #cluster-master-satellite-service-endpoint-allowlist-enable-examples}

Enable the allowlist for a Satellite cluster.

```sh
ibmcloud ks cluster master satellite-service-endpoint allowlist enable \
  --cluster CLUSTER_NAME_OR_ID \
  -f \
  -q
```
{: pre}


### `ibmcloud oc cluster master satellite-service-endpoint allowlist get`
{: #cluster-master-satellite-service-endpoint-allowlist-get-cli}



Get a Satellite cluster's service endpoint allowlist.
{: shortdesc}

```sh
ibmcloud oc cluster master satellite-service-endpoint allowlist get --cluster CLUSTER [-q]
```
{: pre}

#### Command options
{: #cluster-master-satellite-service-endpoint-allowlist-get-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #cluster-master-satellite-service-endpoint-allowlist-get-examples}

Get a Satellite cluster's service endpoint allowlist.

```sh
ibmcloud ks cluster master satellite-service-endpoint allowlist get \
  --cluster CLUSTER_NAME_OR_ID \
  -q
```
{: pre}


### `ibmcloud oc cluster master satellite-service-endpoint allowlist rm`
{: #cluster-master-satellite-service-endpoint-allowlist-rm-cli}



Remove subnets from a Satellite cluster's service endpoint allowlist.
{: shortdesc}

```sh
ibmcloud oc cluster master satellite-service-endpoint allowlist rm --cluster CLUSTER --subnet SUBNET [--subnet SUBNET ...] [-f] [-q]
```
{: pre}

#### Command options
{: #cluster-master-satellite-service-endpoint-allowlist-rm-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`-q`
:    Do not show the message of the day or update reminders.

`--subnet SUBNET`
:    Specify the subnet CIDR.


#### Examples
{: #cluster-master-satellite-service-endpoint-allowlist-rm-examples}

Remove subnets from a Satellite cluster's service endpoint allowlist.

```sh
ibmcloud ks cluster master satellite-service-endpoint allowlist rm \
  --cluster CLUSTER_NAME_OR_ID \
  -f \
  --subnet SUBNET_CIDR
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
{: pre}

#### Command options
{: #cluster-master-update-options}


`--cluster CLUSTER`, `-c CLUSTER`
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

Update the cluster master to the latest version.

```sh
ibmcloud ks cluster master update \
  --cluster CLUSTER_NAME_OR_ID \
  --force-update FORCE-UPDATE \
  -f
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
{: pre}

#### Command options
{: #cluster-pull-secret-apply-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #cluster-pull-secret-apply-examples}

Generate a new image pull secret that stores IAM credentials for the cluster to access images in IBM Cloud Container Reg.

```sh
ibmcloud ks cluster pull-secret apply --cluster CLUSTER_NAME_OR_ID -q
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
{: pre}

#### Command options
{: #cluster-rm-options}


`--cluster CLUSTER`, `-c CLUSTER`
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

Delete a cluster.

```sh
ibmcloud ks cluster rm --cluster CLUSTER_NAME_OR_ID -f --delete-storage DELETE-STORAGE
```
{: pre}


### `ibmcloud oc cluster service bind`
{: #cluster-service-bind-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

Add an IBM Cloud service to a cluster by binding the service instance to a Kubernetes namespace.
{: shortdesc}

```sh
ibmcloud oc cluster service bind --cluster CLUSTER --namespace NAMESPACE --service SERVICE [-q] --key KEY
```
{: pre}

#### Command options
{: #cluster-service-bind-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`--key KEY`
:    Specify the name or GUID of an existing service key. If you define a service key, you cannot set the `--role` option at the same time.

`--namespace NAMESPACE`, `-n NAMESPACE`
:    Specify the Kubernetes namespace.

`-q`
:    Do not show the message of the day or update reminders.

`--role ROLE`
:    Specify the IAM role for the service key. This flag does not work if you specify an existing key to use or for services that are not IAM-enabled, such as Cloud Foundry services.

`--service SERVICE`
:    Specify the name of the service instance. To see a list of available service instances, run `ibmcloud service list` for Cloud Foundry services, or `ibmcloud resource service-instances` for IAM-enabled services.


#### Examples
{: #cluster-service-bind-examples}

Add an IBM Cloud service to a cluster by binding the service instance to a Kubernetes namespace.

```sh
ibmcloud ks cluster service bind \
  --cluster CLUSTER_NAME_OR_ID \
  --namespace NAME \
  --key KEY
```
{: pre}


### `ibmcloud oc cluster service ls`
{: #cluster-service-ls-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

List services bound to a Kubernetes namespace.
{: shortdesc}

```sh
ibmcloud oc cluster service ls --cluster CLUSTER [--output OUTPUT] [-q] --all-namespaces
```
{: pre}

#### Command options
{: #cluster-service-ls-options}


`--all-namespaces`
:    Include all Kubernetes namespaces.

`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`--namespace NAMESPACE`, `-n NAMESPACE`
:    The Kubernetes namespace. Will use the `default` namespace if not specified.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #cluster-service-ls-examples}

List services bound to a Kubernetes namespace.

```sh
ibmcloud ks cluster service ls \
  --cluster CLUSTER_NAME_OR_ID \
  --namespace NAME \
  --all-namespaces NAME
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
{: pre}

#### Command options
{: #cluster-service-unbind-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`--namespace NAMESPACE`, `-n NAMESPACE`
:    Specify the Kubernetes namespace.

`-q`
:    Do not show the message of the day or update reminders.

`--service SERVICE`
:    Specify the name of the service instance. To see a list of available service instances, run `ibmcloud service list` for Cloud Foundry services, or `ibmcloud resource service-instances` for IAM-enabled services.


#### Examples
{: #cluster-service-unbind-examples}

Remove an IBM Cloud service from a cluster by unbinding it from a Kubernetes namespace.

```sh
ibmcloud ks cluster service unbind \
  --cluster CLUSTER_NAME_OR_ID \
  --namespace NAME \
  --service SERVICE
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
{: pre}

#### Command options
{: #cluster-subnet-add-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`-q`
:    Do not show the message of the day or update reminders.

`--subnet-id ID`
:    Specify the subnet ID.


#### Examples
{: #cluster-subnet-add-examples}

Make an existing public or private portable subnet in your IBM Cloud infrastructure account available to a classic clust.

```sh
ibmcloud ks cluster subnet add --cluster CLUSTER_NAME_OR_ID --subnet-id SUBNET_CIDR -q
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
{: pre}

#### Command options
{: #cluster-subnet-create-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`-q`
:    Do not show the message of the day or update reminders.

`--size SIZE`
:    Specify the size of the portable subnet. The size must be one of 8, 16, 32, 64.

`--vlan VLAN`
:    Specify the public or private VLAN ID.


#### Examples
{: #cluster-subnet-create-examples}

Create a portable subnet on your public or private VLAN and make it available to a classic cluster.

```sh
ibmcloud ks cluster subnet create \
  --cluster CLUSTER_NAME_OR_ID \
  --size SIZE \
  --vlan VLAN_ID
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
{: pre}

#### Command options
{: #cluster-subnet-detach-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`-q`
:    Do not show the message of the day or update reminders.

`--subnet-id ID`
:    Specify the subnet ID.


#### Examples
{: #cluster-subnet-detach-examples}

Detach an existing public or private portable subnet from a classic cluster.

```sh
ibmcloud ks cluster subnet detach \
  --cluster CLUSTER_NAME_OR_ID \
  -f \
  --subnet-id SUBNET_CIDR
```
{: pre}



## `ibmcloud oc credential` commands
{: #credential-cli}

Set and unset credentials that allow you to access the IBM Cloud classic infrastructure portfolio through your IBM Cloud account.

### `ibmcloud oc credential get`
{: #credential-get-cli}

[Classic infrastructure]{: tag-classic-inf} 

If you set up your IBM Cloud account to use different credentials to access the IBM Cloud classic infrastructure portfolio, get the infrastructure user name. This command applies to the targeted resource group, or to the default resource group if no resource group is targeted.
{: shortdesc}

```sh
ibmcloud oc credential get --region REGION [--output OUTPUT] [-q]
```
{: pre}

Aliases: `ibmcloud oc credential credentials-get`, `ibmcloud oc credentials-get`

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

If you set up your IBM Cloud account to use different credentials to access the IBM Cloud classic infrastructure portfol.

```sh
ibmcloud ks credential get --output json --region REGION -q
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
{: pre}

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

Set credentials that allow you to access the IBM Cloud classic infrastructure portfolio through your IBM Cloud account.

```sh
ibmcloud ks credential set classic \
  --infrastructure-username NAME \
  --infrastructure-api-key INFRASTRUCTURE-API-KEY \
  --region REGION
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
{: pre}

Aliases: `ibmcloud oc credential credentials-unset`, `ibmcloud oc credentials-unset`

#### Command options
{: #credential-unset-options}


`-q`
:    Do not show the message of the day or update reminders.

`--region REGION`
:    Specify the region to target.


#### Examples
{: #credential-unset-examples}

Remove the credentials that allow you to access the IBM Cloud classic infrastructure portfolio through your IBM Cloud ac.

```sh
ibmcloud ks credential unset --region REGION -q
```
{: pre}



## `ibmcloud oc experimental` commands
{: #experimental-cli}

[Expires on 2026-10-21] Experiment with new commands. IMPORTANT: Commands here will retire after the [date] in their description.

### `ibmcloud oc experimental trusted-profile default get`
{: #experimental-trusted-profile-default-get-cli}



[Expires on 2026-10-21] Get the default trusted profile for clusters created in a resource-group.
{: shortdesc}

```sh
ibmcloud oc experimental trusted-profile default get --region REGION --resource-group GROUP [--output OUTPUT] [-q]
```
{: pre}

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

Get the default trusted profile for clusters created in a resource-group.

```sh
ibmcloud ks experimental trusted-profile default get \
  --resource-group RESOURCE_GROUP \
  --region REGION \
  --output json
```
{: pre}


### `ibmcloud oc experimental trusted-profile default set`
{: #experimental-trusted-profile-default-set-cli}



[Expires on 2026-10-21] Set the default trusted profile for clusters created in a resource-group.
{: shortdesc}

```sh
ibmcloud oc experimental trusted-profile default set --region REGION --resource-group GROUP --trusted-profile PROFILE [--output OUTPUT] [-q]
```
{: pre}

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

Set the default trusted profile for clusters created in a resource-group.

```sh
ibmcloud ks experimental trusted-profile default set \
  --resource-group RESOURCE_GROUP \
  --trusted-profile FILE_PATH \
  --region REGION
```
{: pre}


### `ibmcloud oc experimental trusted-profile get`
{: #experimental-trusted-profile-get-cli}



[Expires on 2026-10-21] Get trusted profile for a cluster.
{: shortdesc}

```sh
ibmcloud oc experimental trusted-profile get --cluster CLUSTER [--output OUTPUT] [-q]
```
{: pre}

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

Get trusted profile for a cluster.

```sh
ibmcloud ks experimental trusted-profile get \
  --cluster CLUSTER_NAME_OR_ID \
  --output json \
  -q
```
{: pre}


### `ibmcloud oc experimental trusted-profile set`
{: #experimental-trusted-profile-set-cli}



[Expires on 2026-10-21] Set trusted profile on a cluster.
{: shortdesc}

```sh
ibmcloud oc experimental trusted-profile set --cluster CLUSTER --trusted-profile PROFILE [--output OUTPUT] [-q]
```
{: pre}

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

Set trusted profile on a cluster.

```sh
ibmcloud ks experimental trusted-profile set \
  --cluster CLUSTER_NAME_OR_ID \
  --trusted-profile FILE_PATH \
  --output json
```
{: pre}


### `ibmcloud oc experimental vni attach baremetal`
{: #experimental-vni-attach-baremetal-cli}



[Deactivated on 2026-05-20! Use `ibmcloud ks vni attach baremetal` instead] Attach a Virtual Network Interface to a bare metal worker node or cluster.
{: shortdesc}

```sh
ibmcloud oc experimental vni attach baremetal --vlan VLAN --vni VNI [--auto-delete] [--output OUTPUT] [-q] --cluster-id ID
```
{: pre}

#### Command options
{: #experimental-vni-attach-baremetal-options}


`--auto-delete`
:    Automatically delete the VNI when it is removed from the cluster.

`--cluster-id ID`, `-c ID`
:    The ID of the cluster.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.

`--vlan VLAN`
:    The VLAN ID for the bare metal node attachment. Must be unique for each VPC subnet. Multiple VNIs from the same subnet can reuse the VLAN ID. Valid range: 1-500.

`--vni VNI`
:    The ID of the Virtual Network Interface to attach. You must specify VNIs without any current target resource. To list all the VNIs, run `ibmcloud is vnis`. To check if a specific VNI is already attached to a resource, check for the "Target" field in 'ibmcloud is vni <VNI_ID>.

`--worker WORKER`, `-w WORKER`
:    The ID of the worker node.


#### Examples
{: #experimental-vni-attach-baremetal-examples}

Attach a Virtual Network Interface to a bare metal worker node or cluster.

```sh
ibmcloud ks experimental vni attach baremetal \
  --cluster-id CLUSTER_NAME_OR_ID \
  --worker WORKER_ID \
  --vni VNI
```
{: pre}


### `ibmcloud oc experimental vni attach virtual`
{: #experimental-vni-attach-virtual-cli}



[Expires on 2026-05-20] Attach a Virtual Network Interface to a virtual worker node.
{: shortdesc}

```sh
ibmcloud oc experimental vni attach virtual --vni VNI --worker WORKER [--auto-delete] [--output OUTPUT] [-q]
```
{: pre}

#### Command options
{: #experimental-vni-attach-virtual-options}


`--auto-delete`
:    Automatically delete the VNI when it is removed from the cluster.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.

`--vni VNI`
:    The ID of the Virtual Network Interface to attach. You must specify VNIs without any current target resource. To list all the VNIs, run `ibmcloud is vnis`. To check if a specific VNI is already attached to a resource, check for the "Target" field in 'ibmcloud is vni <VNI_ID>.

`--worker WORKER`, `-w WORKER`
:    The ID of the worker node.


#### Examples
{: #experimental-vni-attach-virtual-examples}

Attach a Virtual Network Interface to a virtual worker node.

```sh
ibmcloud ks experimental vni attach virtual \
  --vni VNI \
  --worker WORKER_ID \
  --auto-delete AUTO-DELETE
```
{: pre}


### `ibmcloud oc experimental vni detach`
{: #experimental-vni-detach-cli}



[Deactivated on 2026-05-20! Use `ibmcloud ks vni detach` instead] Detach a Virtual Network Interface from a worker node or cluster.
{: shortdesc}

```sh
ibmcloud oc experimental vni detach --vni VNI [-f] [--output OUTPUT] [-q] --cluster-id ID
```
{: pre}

#### Command options
{: #experimental-vni-detach-options}


`--cluster-id ID`, `-c ID`
:    The ID of the cluster.

`-f`
:    Force the command to run without user prompts.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.

`--vni VNI`
:    The ID of the Virtual Network Interface to detach.

`--worker WORKER`, `-w WORKER`
:    The ID of the worker node.


#### Examples
{: #experimental-vni-detach-examples}

Detach a Virtual Network Interface from a worker node or cluster.

```sh
ibmcloud ks experimental vni detach \
  --cluster-id CLUSTER_NAME_OR_ID \
  --worker WORKER_ID \
  --vni VNI
```
{: pre}


### `ibmcloud oc experimental vni ls`
{: #experimental-vni-ls-cli}



[Deactivated on 2026-05-20! Use `ibmcloud ks vni ls` instead] List Virtual Network Interfaces attached to a cluster or worker node.
{: shortdesc}

```sh
ibmcloud oc experimental vni ls [--after AFTER] [--first FIRST] [--output OUTPUT] [-q] (--cluster-id ID | --worker WORKER)
```
{: pre}

#### Command options
{: #experimental-vni-ls-options}


`--after AFTER`
:    Show Virtual Network Interfaces after the given cursor.

`--cluster-id ID`, `-c ID`
:    The ID of the cluster.

`--first FIRST`
:    View the next Virtual Network Interfaces, up to the first number of VNIs.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.

`--worker WORKER`, `-w WORKER`
:    The ID of the worker node.


#### Examples
{: #experimental-vni-ls-examples}

List Virtual Network Interfaces attached to a cluster or worker node.

```sh
ibmcloud ks experimental vni ls --cluster-id CLUSTER_ID
```
{: pre}



## `ibmcloud oc flavor` commands
{: #flavor-cli}

Getting flavor related information. Flavors determine how much virtual CPU, memory, and disk space is available to each worker node.

### `ibmcloud oc flavor get`
{: #flavor-get-cli}



Get the information of a flavor for a zone and provider.
{: shortdesc}

```sh
ibmcloud oc flavor get --flavor FLAVOR --provider PROVIDER --zone ZONE [--output OUTPUT] [-q]
```
{: pre}

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

Get the information of a flavor for a zone and provider.

```sh
ibmcloud ks flavor get --zone ZONE --provider PROVIDER_ID --flavor FLAVOR
```
{: pre}


### `ibmcloud oc flavor ls`
{: #flavor-ls-cli}



List available flavors for a zone.
{: shortdesc}

```sh
ibmcloud oc flavor ls --zone ZONE [--output OUTPUT] [--provider PROVIDER] [-q] [--show-os] [--show-storage]
```
{: pre}

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

List available flavors for a zone.

```sh
ibmcloud ks flavor ls --zone ZONE --show-storage SHOW-STORAGE --show-os SHOW-OS
```
{: pre}



## `ibmcloud oc infra-permissions` commands
{: #infra-permissions-cli}

View information about infrastructure permissions that allow you to access the IBM Cloud classic infrastructure portfolio through your IBM Cloud account.

### `ibmcloud oc infra-permissions get`
{: #infra-permissions-get-cli}

[Classic infrastructure]{: tag-classic-inf} 

Check whether the credentials that allow access to the IBM Cloud classic infrastructure portfolio for the targeted resource group are missing suggested or required infrastructure permissions. This command applies to the targeted resource group, or to the default resource group if no resource group is targeted.
{: shortdesc}

```sh
ibmcloud oc infra-permissions get [--output OUTPUT] [-q] [--region REGION]
```
{: pre}

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

Check whether the credentials that allow access to the IBM Cloud classic infrastructure portfolio for the targeted resou.

```sh
ibmcloud ks infra-permissions get --output json --region REGION -q
```
{: pre}



## `ibmcloud oc ingress` commands
{: #ingress-cli}

View and modify Ingress services and settings

### `ibmcloud oc ingress alb autoscale get`
{: #ingress-alb-autoscale-get-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

See autoscaling status and configuration for Ingress ALBs.
{: shortdesc}

```sh
ibmcloud oc ingress alb autoscale get --alb ALB --cluster CLUSTER [--output OUTPUT] [-q]
```
{: pre}

#### Command options
{: #ingress-alb-autoscale-get-options}


`--alb ALB`
:    The ALB ID. To see available ALB IDs, run `ibmcloud ks ingress alb ls`.

`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #ingress-alb-autoscale-get-examples}

See autoscaling status and configuration for Ingress ALBs.

```sh
ibmcloud ks ingress alb autoscale get \
  --cluster CLUSTER_NAME_OR_ID \
  --alb ALB_ID \
  --output json
```
{: pre}


### `ibmcloud oc ingress alb autoscale set`
{: #ingress-alb-autoscale-set-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

Configure autoscaling for Ingress ALBs.
{: shortdesc}

```sh
ibmcloud oc ingress alb autoscale set --alb ALB --cluster CLUSTER --max-replicas REPLICAS --min-replicas REPLICAS [--output OUTPUT] [-q] --cpu-average-utilization PERCENT
```
{: pre}

#### Command options
{: #ingress-alb-autoscale-set-options}


`--alb ALB`
:    The ALB ID. To see available ALB IDs, run `ibmcloud ks ingress alb ls`.

`--cluster CLUSTER`, `-c CLUSTER`
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

Configure autoscaling for Ingress ALBs.

```sh
ibmcloud ks ingress alb autoscale set \
  --cluster CLUSTER_NAME_OR_ID \
  --alb ALB_ID \
  --max-replicas MAX-REPLICAS
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
{: pre}

#### Command options
{: #ingress-alb-autoscale-unset-options}


`--alb ALB`
:    The ALB ID. To see available ALB IDs, run `ibmcloud ks ingress alb ls`.

`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #ingress-alb-autoscale-unset-examples}

Delete the autoscaling configuration for Ingress ALBs.

```sh
ibmcloud ks ingress alb autoscale unset --cluster CLUSTER_NAME_OR_ID --alb ALB_ID -q
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
{: pre}

#### Command options
{: #ingress-alb-autoupdate-disable-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #ingress-alb-autoupdate-disable-examples}

Disable automatic updates of all Ingress ALB pods in a cluster.

```sh
ibmcloud ks ingress alb autoupdate disable --cluster CLUSTER_NAME_OR_ID -q
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
{: pre}

#### Command options
{: #ingress-alb-autoupdate-enable-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #ingress-alb-autoupdate-enable-examples}

Enable automatic updates of all Ingress ALB pods in a cluster.

```sh
ibmcloud ks ingress alb autoupdate enable --cluster CLUSTER_NAME_OR_ID -q
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
{: pre}

#### Command options
{: #ingress-alb-autoupdate-get-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #ingress-alb-autoupdate-get-examples}

View whether the Ingress ALB pods in a cluster are set to automatically update and whether ALB pods are at the latest ve.

```sh
ibmcloud ks ingress alb autoupdate get --cluster CLUSTER_NAME_OR_ID --output json -q
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
{: pre}

#### Command options
{: #ingress-alb-create-classic-options}


`--cluster CLUSTER`, `-c CLUSTER`
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

Create and enable an Ingress ALB in a classic cluster.

```sh
ibmcloud ks ingress alb create classic \
  --cluster CLUSTER_NAME_OR_ID \
  --zone ZONE \
  --type TYPE
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
{: pre}

#### Command options
{: #ingress-alb-create-vpc-gen2-options}


`--cluster CLUSTER`, `-c CLUSTER`
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

Create and enable an Ingress ALB in a VPC Gen 2 cluster.

```sh
ibmcloud ks ingress alb create vpc-gen2 \
  --cluster CLUSTER_NAME_OR_ID \
  --zone ZONE \
  --type TYPE
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
{: pre}

#### Command options
{: #ingress-alb-disable-options}


`--alb ALB`
:    The ALB ID. To see available ALB IDs, run `ibmcloud ks ingress alb ls`.

`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #ingress-alb-disable-examples}

Disable an Ingress ALB in a cluster.

```sh
ibmcloud ks ingress alb disable --cluster CLUSTER_NAME_OR_ID --alb ALB_ID -q
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
{: pre}

#### Command options
{: #ingress-alb-enable-classic-options}


`--alb ALB`
:    The ALB ID. To see available ALB IDs, run `ibmcloud ks ingress alb ls`.

`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`--ip IP`
:    Specify a portable public or private IP address that is available on the `vlan` and in the `zone` of the ALB to be created or enabled.

`-q`
:    Do not show the message of the day or update reminders.

`--version VERSION`
:    Specify the ALB image version. To see supported image versions, run `ibmcloud ks ingress alb versions`.


#### Examples
{: #ingress-alb-enable-classic-examples}

Enable an Ingress ALB in a classic cluster.

```sh
ibmcloud ks ingress alb enable classic \
  --cluster CLUSTER_NAME_OR_ID \
  --alb ALB_ID \
  --version VERSION
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
{: pre}

#### Command options
{: #ingress-alb-enable-vpc-gen2-options}


`--alb ALB`
:    The ALB ID. To see available ALB IDs, run `ibmcloud ks ingress alb ls`.

`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`-q`
:    Do not show the message of the day or update reminders.

`--version VERSION`
:    Specify the ALB image version. To see supported image versions, run `ibmcloud ks ingress alb versions`.


#### Examples
{: #ingress-alb-enable-vpc-gen2-examples}

Enable an Ingress ALB in a VPC Gen 2 cluster.

```sh
ibmcloud ks ingress alb enable vpc-gen2 \
  --cluster CLUSTER_NAME_OR_ID \
  --alb ALB_ID \
  --version VERSION
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
{: pre}

#### Command options
{: #ingress-alb-get-options}


`--alb ALB`
:    The ALB ID. To see available ALB IDs, run `ibmcloud ks ingress alb ls`.

`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #ingress-alb-get-examples}

View the details of an Ingress ALB in a cluster.

```sh
ibmcloud ks ingress alb get --cluster CLUSTER_NAME_OR_ID --alb ALB_ID --output json
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
{: pre}

#### Command options
{: #ingress-alb-health-checker-disable-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #ingress-alb-health-checker-disable-examples}

Disable the Ingress health checker.

```sh
ibmcloud ks ingress alb health-checker disable --cluster CLUSTER_NAME_OR_ID -q
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
{: pre}

#### Command options
{: #ingress-alb-health-checker-enable-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #ingress-alb-health-checker-enable-examples}

Enable the Ingress health checker.

```sh
ibmcloud ks ingress alb health-checker enable --cluster CLUSTER_NAME_OR_ID -q
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
{: pre}

#### Command options
{: #ingress-alb-health-checker-get-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #ingress-alb-health-checker-get-examples}

View status of the Ingress health checker.

```sh
ibmcloud ks ingress alb health-checker get --cluster CLUSTER_NAME_OR_ID --output json -q
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
{: pre}

#### Command options
{: #ingress-alb-ls-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #ingress-alb-ls-examples}

List all Ingress ALB IDs in a cluster and whether ALB pods are at the latest version.

```sh
ibmcloud ks ingress alb ls --cluster CLUSTER_NAME_OR_ID --output json -q
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
{: pre}

#### Command options
{: #ingress-alb-update-options}


`--alb ALB`
:    To update a specific ALB, specify the ALB ID. To see available ALB IDs, run `ibmcloud ks ingress alb ls`. To update more than one ALB, specify one ALB ID in each flag, such as `--alb ID_1 --alb ID_2`. To update all ALBs, do not include this flag.

`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.

`--version VERSION`
:    Specify the ALB image version. To see supported image versions, run `ibmcloud ks ingress alb versions`.


#### Examples
{: #ingress-alb-update-examples}

Force a one-time update of the pods for individual or all ALBs in the cluster.

```sh
ibmcloud ks ingress alb update \
  --cluster CLUSTER_NAME_OR_ID \
  --version VERSION \
  --alb ALB_ID
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
{: pre}

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

List Ingress ALB image versions that are available.

```sh
ibmcloud ks ingress alb versions --region REGION --output json -q
```
{: pre}


### `ibmcloud oc ingress domain create`
{: #ingress-domain-create-cli}



Create an Ingress domain for a cluster.
{: shortdesc}

```sh
ibmcloud oc ingress domain create --cluster CLUSTER [--crn CRN] [--domain DOMAIN] [--domain-provider PROVIDER] [--domain-zone ZONE] [--hostname HOSTNAME] [--ip IP] [--is-default] [--output OUTPUT] [-q] [--secret-namespace NAMESPACE]
```
{: pre}

#### Command options
{: #ingress-domain-create-options}


`--cluster CLUSTER`, `-c CLUSTER`
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

Create an Ingress domain for a cluster.

```sh
ibmcloud ks ingress domain create \
  --cluster CLUSTER_NAME_OR_ID \
  --domain DOMAIN \
  --domain-provider DOMAIN
```
{: pre}


### `ibmcloud oc ingress domain default replace`
{: #ingress-domain-default-replace-cli}



Change a cluster's default Ingress domain.
{: shortdesc}

```sh
ibmcloud oc ingress domain default replace --cluster CLUSTER --domain DOMAIN [-q]
```
{: pre}

#### Command options
{: #ingress-domain-default-replace-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`--domain DOMAIN`
:    The Ingress domain. To see existing domains, run `ibmcloud ks ingress domain ls`.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #ingress-domain-default-replace-examples}

Change a cluster's default Ingress domain.

```sh
ibmcloud ks ingress domain default replace \
  --cluster CLUSTER_NAME_OR_ID \
  --domain DOMAIN \
  -q
```
{: pre}


### `ibmcloud oc ingress domain get`
{: #ingress-domain-get-cli}



View the details of an Ingress domain.
{: shortdesc}

```sh
ibmcloud oc ingress domain get --cluster CLUSTER --domain DOMAIN [--output OUTPUT] [-q]
```
{: pre}

#### Command options
{: #ingress-domain-get-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`--domain DOMAIN`
:    The Ingress domain. To see existing domains, run `ibmcloud ks ingress domain ls`.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #ingress-domain-get-examples}

View the details of an Ingress domain.

```sh
ibmcloud ks ingress domain get \
  --cluster CLUSTER_NAME_OR_ID \
  --domain DOMAIN \
  --output json
```
{: pre}


### `ibmcloud oc ingress domain ls`
{: #ingress-domain-ls-cli}



List all Ingress domains for a cluster.
{: shortdesc}

```sh
ibmcloud oc ingress domain ls --cluster CLUSTER [--output OUTPUT] [-q]
```
{: pre}

#### Command options
{: #ingress-domain-ls-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #ingress-domain-ls-examples}

List all Ingress domains for a cluster.

```sh
ibmcloud ks ingress domain ls --cluster CLUSTER_NAME_OR_ID --output json -q
```
{: pre}


### `ibmcloud oc ingress domain rm`
{: #ingress-domain-rm-cli}



Remove an Ingress domain from a cluster.
{: shortdesc}

```sh
ibmcloud oc ingress domain rm --cluster CLUSTER --domain DOMAIN [-f] [-q]
```
{: pre}

#### Command options
{: #ingress-domain-rm-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`--domain DOMAIN`
:    The Ingress domain. To see existing domains, run `ibmcloud ks ingress domain ls`.

`-f`
:    Force the command to run without user prompts.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #ingress-domain-rm-examples}

Remove an Ingress domain from a cluster.

```sh
ibmcloud ks ingress domain rm --cluster CLUSTER_NAME_OR_ID --domain DOMAIN -f
```
{: pre}


### `ibmcloud oc ingress domain secret regenerate`
{: #ingress-domain-secret-regenerate-cli}



Regenerate the certificate for an Ingress domain.
{: shortdesc}

```sh
ibmcloud oc ingress domain secret regenerate --cluster CLUSTER --domain DOMAIN [--output OUTPUT] [-q]
```
{: pre}

#### Command options
{: #ingress-domain-secret-regenerate-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`--domain DOMAIN`
:    The Ingress domain. To see existing domains, run `ibmcloud ks ingress domain ls`.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #ingress-domain-secret-regenerate-examples}

Regenerate the certificate for an Ingress domain.

```sh
ibmcloud ks ingress domain secret regenerate \
  --cluster CLUSTER_NAME_OR_ID \
  --domain DOMAIN \
  --output json
```
{: pre}


### `ibmcloud oc ingress domain secret rm`
{: #ingress-domain-secret-rm-cli}



Delete a secret for an Ingress domain and prevent future renewal of the certificate.
{: shortdesc}

```sh
ibmcloud oc ingress domain secret rm --cluster CLUSTER --domain DOMAIN [-f] [--output OUTPUT] [-q]
```
{: pre}

#### Command options
{: #ingress-domain-secret-rm-options}


`--cluster CLUSTER`, `-c CLUSTER`
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

Delete a secret for an Ingress domain and prevent future renewal of the certificate.

```sh
ibmcloud ks ingress domain secret rm --cluster CLUSTER_NAME_OR_ID --domain DOMAIN -f
```
{: pre}


### `ibmcloud oc ingress domain update`
{: #ingress-domain-update-cli}



Update an Ingress domain for a cluster. The records passed in will fully replace the current records associated with the domain. Passing in no records will unregister the current records from a domain.
{: shortdesc}

```sh
ibmcloud oc ingress domain update --cluster CLUSTER --domain DOMAIN [--hostname HOSTNAME] [--ip IP] [-q]
```
{: pre}

#### Command options
{: #ingress-domain-update-options}


`--cluster CLUSTER`, `-c CLUSTER`
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

Update an Ingress domain for a cluster.

```sh
ibmcloud ks ingress domain update \
  --cluster CLUSTER_NAME_OR_ID \
  --domain DOMAIN \
  --ip IP_ADDRESS
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
{: pre}

#### Command options
{: #ingress-instance-default-set-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`--name NAME`
:    The name of the registered IBM Cloud Secret Manager instance.

`-q`
:    Do not show the message of the day or update reminders.

`--secret-group GROUP`
:    Secret Group ID of the IBM Cloud Secret Manager instance where the secrets are persisted.


#### Examples
{: #ingress-instance-default-set-examples}

Set a registered IBM Cloud Secrets Manager instance as the default.

```sh
ibmcloud ks ingress instance default set \
  --cluster CLUSTER_NAME_OR_ID \
  --name NAME \
  --secret-group GROUP
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
{: pre}

#### Command options
{: #ingress-instance-default-unset-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`--name NAME`
:    The name of the registered IBM Cloud Secret Manager instance.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #ingress-instance-default-unset-examples}

Unset a registered IBM Cloud Secrets Manager instance from default.

```sh
ibmcloud ks ingress instance default unset --cluster CLUSTER_NAME_OR_ID --name NAME -q
```
{: pre}


### `ibmcloud oc ingress instance get`
{: #ingress-instance-get-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

View the details of an IBM Cloud Secrets Manager instance.
{: shortdesc}

```sh
ibmcloud oc ingress instance get --cluster CLUSTER --name NAME [--output OUTPUT] [-q]
```
{: pre}

#### Command options
{: #ingress-instance-get-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`--name NAME`
:    The name of the registered IBM Cloud Secret Manager instance.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #ingress-instance-get-examples}

View the details of an IBM Cloud Secrets Manager instance.

```sh
ibmcloud ks ingress instance get \
  --cluster CLUSTER_NAME_OR_ID \
  --name NAME \
  --output json
```
{: pre}


### `ibmcloud oc ingress instance ls`
{: #ingress-instance-ls-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

List all instances of the IBM Cloud Secrets Manager.
{: shortdesc}

```sh
ibmcloud oc ingress instance ls --cluster CLUSTER [--output OUTPUT] [-q] [--show-deleted]
```
{: pre}

#### Command options
{: #ingress-instance-ls-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.

`--show-deleted`
:    Show IBM Cloud Secret Manager instances that were unregistered from the cluster.


#### Examples
{: #ingress-instance-ls-examples}

List all instances of the IBM Cloud Secrets Manager.

```sh
ibmcloud ks ingress instance ls \
  --cluster CLUSTER_NAME_OR_ID \
  --output json \
  --show-deleted
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
{: pre}

#### Command options
{: #ingress-instance-register-options}


`--cluster CLUSTER`, `-c CLUSTER`
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

Register an IBM Cloud Secrets Manager instance to a cluster.

```sh
ibmcloud ks ingress instance register \
  --cluster CLUSTER_NAME_OR_ID \
  --crn CRN \
  --is-default IS-DEFAULT
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
{: pre}

#### Command options
{: #ingress-instance-unregister-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`--name NAME`
:    The name of the registered IBM Cloud Secret Manager instance.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #ingress-instance-unregister-examples}

Unregister an IBM Cloud Secrets Manager instance from a cluster.

```sh
ibmcloud ks ingress instance unregister --cluster CLUSTER_NAME_OR_ID --name NAME -q
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
{: pre}

Aliases: `ibmcloud oc ingress lb backend set`

#### Command options
{: #ingress-load-balancer-backend-set-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`--private-backend BACKEND`
:    Backend for private load balancer

`--public-backend BACKEND`
:    Backend for public load balancer

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #ingress-load-balancer-backend-set-examples}

Set the Ingress controller currently exposed by the VPC ALB load balancer.

```sh
ibmcloud ks ingress load-balancer backend set \
  --cluster CLUSTER_NAME_OR_ID \
  --private-backend PRIVATE-BACKEND \
  --public-backend PUBLIC-BACKEND
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
{: pre}

Aliases: `ibmcloud oc ingress lb get`

#### Command options
{: #ingress-load-balancer-get-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #ingress-load-balancer-get-examples}

Get the configuration of load balancers that expose Ingress ALBs in your cluster.

```sh
ibmcloud ks ingress load-balancer get --cluster CLUSTER_NAME_OR_ID --output json -q
```
{: pre}


### `ibmcloud oc ingress load-balancer proxy-protocol disable`
{: #ingress-load-balancer-proxy-protocol-disable-cli}

[Virtual Private Cloud]{: tag-vpc} 

Disable the PROXY protocol so that client connection information is no longer passed in request headers to ALBs.
{: shortdesc}

```sh
ibmcloud oc ingress load-balancer proxy-protocol disable --cluster CLUSTER [-f] [-q]
```
{: pre}

Aliases: `ibmcloud oc ingress lb proxy-protocol disable`

#### Command options
{: #ingress-load-balancer-proxy-protocol-disable-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #ingress-load-balancer-proxy-protocol-disable-examples}

Disable the PROXY protocol so that client connection information is no longer passed in request headers to ALBs.

```sh
ibmcloud ks ingress load-balancer proxy-protocol disable \
  --cluster CLUSTER_NAME_OR_ID \
  -f \
  -q
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
{: pre}

Aliases: `ibmcloud oc ingress lb proxy-protocol enable`

#### Command options
{: #ingress-load-balancer-proxy-protocol-enable-options}


`--cidr CIDR`
:    The IP address ranges of your load balancers in CIDR format. PROXY headers that are forwarded by load balancers in other IP ranges are not processed.

`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #ingress-load-balancer-proxy-protocol-enable-examples}

Enable the PROXY protocol so that client connection information is passed in request headers to ALBs.

```sh
ibmcloud ks ingress load-balancer proxy-protocol enable \
  --cluster CLUSTER_NAME_OR_ID \
  --cidr CIDR_ID \
  -f
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
{: pre}

#### Command options
{: #ingress-secret-create-options}


`--cert-crn CRN`
:    The certificate CRN.

`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`--field FIELD`
:    The secret CRN to include as a field. To pull in the secret without specifying the name, use `--field <crn>`. To specify the field name, use `--field name=<crn>`. To use the IBM Cloud Secrets Manager secret as the prefix, use `--field prefix=<crn>`.

`--name NAME`
:    A name for the Ingress secret that is created in the cluster.

`--namespace NAMESPACE`, `-n NAMESPACE`
:    Specify the Kubernetes namespace.

`--persist`
:    Persist the secret in the cluster so that it cannot be deleted.

`-q`
:    Do not show the message of the day or update reminders.

`--type TYPE`
:    The Ingress secret type. Can be TLS or Opaque. If no option is specified, TLS is applied by default.


#### Examples
{: #ingress-secret-create-examples}

Create an Ingress secret in a cluster for a secret stored in IBM Cloud Secret Manager.

```sh
ibmcloud ks ingress secret create \
  --cluster CLUSTER_NAME_OR_ID \
  --name NAME \
  --namespace NAME
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
{: pre}

#### Command options
{: #ingress-secret-field-add-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`--field FIELD`
:    The secret CRN to include as a field. To pull in the secret without specifying the name, use `--field <crn>`. To specify the field name, use `--field name=<crn>`. To use the IBM Cloud Secrets Manager secret as the prefix, use `--field prefix=<crn>`.

`--name NAME`
:    A name for the Ingress secret that is created in the cluster.

`--namespace NAMESPACE`, `-n NAMESPACE`
:    Specify the Kubernetes namespace.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #ingress-secret-field-add-examples}

Add fields to an existing Ingress secret.

```sh
ibmcloud ks ingress secret field add \
  --cluster CLUSTER_NAME_OR_ID \
  --name NAME \
  --namespace NAME
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
{: pre}

#### Command options
{: #ingress-secret-field-ls-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`--name NAME`
:    A name for the Ingress secret that is created in the cluster.

`--namespace NAMESPACE`, `-n NAMESPACE`
:    Specify the Kubernetes namespace.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.

`--show-crn`
:    Show CRN value of secret.


#### Examples
{: #ingress-secret-field-ls-examples}

View the fields of an Ingress secret.

```sh
ibmcloud ks ingress secret field ls \
  --cluster CLUSTER_NAME_OR_ID \
  --name NAME \
  --namespace NAME
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
{: pre}

#### Command options
{: #ingress-secret-field-rm-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`--field-name NAME`
:    The name of the field to remove from the secret.

`--name NAME`
:    A name for the Ingress secret that is created in the cluster.

`--namespace NAMESPACE`, `-n NAMESPACE`
:    Specify the Kubernetes namespace.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #ingress-secret-field-rm-examples}

Remove fields from an existing Ingress secret.

```sh
ibmcloud ks ingress secret field rm \
  --cluster CLUSTER_NAME_OR_ID \
  --name NAME \
  --namespace NAME
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
{: pre}

#### Command options
{: #ingress-secret-get-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`--name NAME`
:    A name for the Ingress secret that is created in the cluster.

`--namespace NAMESPACE`, `-n NAMESPACE`
:    Specify the Kubernetes namespace.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #ingress-secret-get-examples}

View the details of an Ingress secret.

```sh
ibmcloud ks ingress secret get \
  --cluster CLUSTER_NAME_OR_ID \
  --name NAME \
  --namespace NAME
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
{: pre}

#### Command options
{: #ingress-secret-ls-options}


`--cluster CLUSTER`, `-c CLUSTER`
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

List all Ingress secrets in a cluster.

```sh
ibmcloud ks ingress secret ls --cluster CLUSTER_NAME_OR_ID --show-deleted --output json
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
{: pre}

#### Command options
{: #ingress-secret-rm-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`--name NAME`
:    A name for the Ingress secret that is created in the cluster.

`--namespace NAMESPACE`, `-n NAMESPACE`
:    Specify the Kubernetes namespace.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #ingress-secret-rm-examples}

Remove an Ingress secret from a cluster.

```sh
ibmcloud ks ingress secret rm \
  --cluster CLUSTER_NAME_OR_ID \
  --name NAME \
  --namespace NAME
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
{: pre}

#### Command options
{: #ingress-secret-update-options}


`--cert-crn CRN`
:    The certificate CRN.

`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`--name NAME`
:    A name for the Ingress secret that is created in the cluster.

`--namespace NAMESPACE`, `-n NAMESPACE`
:    Specify the Kubernetes namespace.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #ingress-secret-update-examples}

Update an existing Ingress secret.

```sh
ibmcloud ks ingress secret update \
  --cluster CLUSTER_NAME_OR_ID \
  --name NAME \
  --namespace NAME
```
{: pre}


### `ibmcloud oc ingress security port80 disable`
{: #ingress-security-port80-disable-cli}



Disable the usage of port 80 in your cluster.
{: shortdesc}

```sh
ibmcloud oc ingress security port80 disable --cluster CLUSTER [-f] [-q]
```
{: pre}

Aliases: `ibmcloud oc ingress sec port80 disable`

#### Command options
{: #ingress-security-port80-disable-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #ingress-security-port80-disable-examples}

Disable the usage of port 80 in your cluster.

```sh
ibmcloud ks ingress security port80 disable --cluster CLUSTER_NAME_OR_ID -f -q
```
{: pre}


### `ibmcloud oc ingress security port80 enable`
{: #ingress-security-port80-enable-cli}



Enable the usage of port 80 in your cluster.
{: shortdesc}

```sh
ibmcloud oc ingress security port80 enable --cluster CLUSTER [-f] [-q]
```
{: pre}

Aliases: `ibmcloud oc ingress sec port80 enable`

#### Command options
{: #ingress-security-port80-enable-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #ingress-security-port80-enable-examples}

Enable the usage of port 80 in your cluster.

```sh
ibmcloud ks ingress security port80 enable --cluster CLUSTER_NAME_OR_ID -f -q
```
{: pre}


### `ibmcloud oc ingress security port80 get`
{: #ingress-security-port80-get-cli}



Get the security configuration of port 80 in your cluster.
{: shortdesc}

```sh
ibmcloud oc ingress security port80 get --cluster CLUSTER [--output OUTPUT] [-q]
```
{: pre}

Aliases: `ibmcloud oc ingress sec port80 get`

#### Command options
{: #ingress-security-port80-get-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #ingress-security-port80-get-examples}

Get the security configuration of port 80 in your cluster.

```sh
ibmcloud ks ingress security port80 get --cluster CLUSTER_NAME_OR_ID --output json -q
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
{: pre}

#### Command options
{: #ingress-status-report-disable-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #ingress-status-report-disable-examples}

Disable status reporting for Ingress components in a cluster.

```sh
ibmcloud ks ingress status-report disable --cluster CLUSTER_NAME_OR_ID --output json -q
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
{: pre}

#### Command options
{: #ingress-status-report-enable-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #ingress-status-report-enable-examples}

Enable status reporting for Ingress components in a cluster.

```sh
ibmcloud ks ingress status-report enable --cluster CLUSTER_NAME_OR_ID --output json -q
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
{: pre}

#### Command options
{: #ingress-status-report-get-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #ingress-status-report-get-examples}

Get the status report for Ingress components in a cluster.

```sh
ibmcloud ks ingress status-report get --cluster CLUSTER_NAME_OR_ID --output json -q
```
{: pre}


### `ibmcloud oc ingress status-report ignored-errors add`
{: #ingress-status-report-ignored-errors-add-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

Add warnings to be ignored by Ingress status for a cluster.
{: shortdesc}

```sh
ibmcloud oc ingress status-report ignored-errors add --cluster CLUSTER --code CODE [--code CODE ...] [--output OUTPUT] [-q]
```
{: pre}

#### Command options
{: #ingress-status-report-ignored-errors-add-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`--code CODE`
:    Code of the warning to be ignored.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #ingress-status-report-ignored-errors-add-examples}

Add warnings to be ignored by Ingress status for a cluster.

```sh
ibmcloud ks ingress status-report ignored-errors add \
  --code CODE \
  --cluster CLUSTER_NAME_OR_ID \
  --output json
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
{: pre}

#### Command options
{: #ingress-status-report-ignored-errors-ls-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #ingress-status-report-ignored-errors-ls-examples}

List warnings that are currently ignored by Ingress status for a cluster.

```sh
ibmcloud ks ingress status-report ignored-errors ls \
  --cluster CLUSTER_NAME_OR_ID \
  --output json \
  -q
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
{: pre}

#### Command options
{: #ingress-status-report-ignored-errors-rm-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`--code CODE`
:    Code of the warning to be removed.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #ingress-status-report-ignored-errors-rm-examples}

Remove warnings that are currently ignored by Ingress status for a cluster.

```sh
ibmcloud ks ingress status-report ignored-errors rm \
  --code CODE \
  --cluster CLUSTER_NAME_OR_ID \
  --output json
```
{: pre}



## `ibmcloud oc init` commands
{: #init-cli}

Initialize the Kubernetes Service plug-in and get authentication tokens.

### `ibmcloud oc init`
{: #init-cli}



Initialize the Kubernetes Service plug-in and get authentication tokens.
{: shortdesc}

```sh
ibmcloud oc init [--host HOST] [--insecure] [-p P] [-q] [-u U]
```
{: pre}

#### Command options
{: #init-options}


`--host HOST`
:    The API endpoint for the service.

`--insecure`
:    Allow an insecure HTTP connection.

`-p P`
:    The IBM Cloud password.

`-q`
:    Do not show the message of the day or update reminders.

`-u U`
:    The IBM Cloud user ID.


#### Examples
{: #init-examples}

Initialize the Kubernetes Service plug-in and get authentication tokens.

```sh
ibmcloud ks init --host HOSTNAME -u U -p POOL_NAME
```
{: pre}



## `ibmcloud oc kms` commands
{: #kms-cli}

View and configure Key Management Service integrations.

### `ibmcloud oc kms crk ls`
{: #kms-crk-ls-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

List available root keys for a Key Management Service instance.
{: shortdesc}

```sh
ibmcloud oc kms crk ls --instance-id ID [--output OUTPUT] [-q]
```
{: pre}

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

List available root keys for a Key Management Service instance.

```sh
ibmcloud ks kms crk ls --output json --instance-id INSTANCE_ID -q
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
{: pre}

#### Command options
{: #kms-enable-options}


`--cluster CLUSTER`, `-c CLUSTER`
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

Enable a key management service (KMS) in your cluster to encrypt your secrets.

```sh
ibmcloud ks kms enable \
  --cluster CLUSTER_NAME_OR_ID \
  --instance-id INSTANCE_ID \
  --crk CRK
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
{: pre}

#### Command options
{: #kms-instance-ls-options}


`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #kms-instance-ls-examples}

List available Key Management Service instances.

```sh
ibmcloud ks kms instance ls --output json -q
```
{: pre}



## `ibmcloud oc locations` commands
{: #locations-cli}

List supported IBM Cloud Kubernetes Service locations.

### `ibmcloud oc locations`
{: #locations-cli}



List supported IBM Cloud Kubernetes Service locations.
{: shortdesc}

```sh
ibmcloud oc locations
```
{: pre}

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

List supported IBM Cloud Kubernetes Service locations.

```sh
ibmcloud ks locations --provider PROVIDER_ID --show-flavors FLAVOR --output json
```
{: pre}



## `ibmcloud oc logging` commands
{: #logging-cli}

Forward logs from your cluster.

### `ibmcloud oc logging autoupdate disable`
{: #logging-autoupdate-disable-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} 

Disable automatic updates of all Fluentd pods in a cluster.
{: shortdesc}

```sh
ibmcloud oc logging autoupdate disable --cluster CLUSTER [-q]
```
{: pre}

#### Command options
{: #logging-autoupdate-disable-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #logging-autoupdate-disable-examples}

Disable automatic updates of all Fluentd pods in a cluster.

```sh
ibmcloud ks logging autoupdate disable --cluster CLUSTER_NAME_OR_ID -q
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
{: pre}

#### Command options
{: #logging-autoupdate-enable-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #logging-autoupdate-enable-examples}

Enable automatic updates of all Fluentd pods in a cluster.

```sh
ibmcloud ks logging autoupdate enable --cluster CLUSTER_NAME_OR_ID -q
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
{: pre}

#### Command options
{: #logging-autoupdate-get-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #logging-autoupdate-get-examples}

View whether your Fluentd pods are set to automatically update in a cluster.

```sh
ibmcloud ks logging autoupdate get --cluster CLUSTER_NAME_OR_ID --output json -q
```
{: pre}


### `ibmcloud oc logging config create`
{: #logging-config-create-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} 

Create a logging configuration. If you are using a Dedicated account, you must log in to the public IBM Cloud endpoint and target your public org and space to enable log forwarding.
{: shortdesc}

```sh
ibmcloud oc logging config create --cluster CLUSTER --logsource LOGSOURCE --type TYPE [--force-update] [--hostname HOSTNAME] [--output OUTPUT] [--port PORT] [-q] --ca-cert CERT --syslog-protocol PROTOCOL --verify-mode MODE --namespace NAMESPACE
```
{: pre}

#### Command options
{: #logging-config-create-options}


`-C CONTAINER`, `--app-container CONTAINER`
:    Specify the containers that you want to collect logs for. To specify more than one path, use multiple flags, such as `-C container1 -C container2`. This option is required for the `application` log source. If not provided, logs are collected from all containers from the application log paths passed in.

`--ca-cert CERT`
:    When the logging type is `syslog` and the protocol is tls, the Kubernetes secret name that contains the Certificate Authority certificate.

`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`--force-update`
:    Force an update of the Fluentd pods in the cluster to the latest version.

`--hostname HOSTNAME`
:    When logging type is `syslog`, the hostname or IP address of the log collector. When logging type is `ibm` (deprecated), the logging ingest endpoint. If you do not provide the logging ingest endpoint, then the current region's endpoint is used.

`--logsource LOGSOURCE`
:    The source of the logs to forward. Supported values are `container`, `application`, `ingress`, `worker`, `storage`, and `kubernetes`. This argument supports a comma separated list of log sources. If you do not provide a log source, logs for `container` and `ingress` are forwarded.

`--namespace NAMESPACE`, `-n NAMESPACE`
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

Create a logging configuration.

```sh
ibmcloud ks logging config create \
  --org ORG \
  --space SPACE \
  -C C \
  -p POOL_NAME \
  --cluster CLUSTER_NAME_OR_ID \
  --namespace NAME \
  --logsource LOGSOURCE
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
{: pre}

#### Command options
{: #logging-config-get-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`--logsource LOGSOURCE`
:    The kind of log source you want to filter for. Accepted values are `container`, `application`, `ingress`, `worker`, `storage` and `kubernetes`. If you do not pass a log source, all logging configurations for the cluster are returned.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #logging-config-get-examples}

View log forwarding configurations for a cluster.

```sh
ibmcloud ks logging config get \
  --cluster CLUSTER_NAME_OR_ID \
  --logsource LOGSOURCE \
  --output json
```
{: pre}


### `ibmcloud oc logging config rm`
{: #logging-config-rm-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} 

Delete a log forwarding configuration from a cluster.
{: shortdesc}

```sh
ibmcloud oc logging config rm --cluster CLUSTER [--force-update] [-q] --all
```
{: pre}

#### Command options
{: #logging-config-rm-options}


`--all`
:    Remove all log forwarding configurations.

`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`--force-update`
:    Force an update of the Fluentd pods in the cluster to the latest version.

`--id ID`
:    Specify the ID of the logging configuration.

`--namespace NAMESPACE`, `-n NAMESPACE`
:    The namespace you want to remove the log forwarding configuration from. If there is more than one config for the same namespace, use the `--id <logging configuration ID>` flag instead.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #logging-config-rm-examples}

Delete a log forwarding configuration from a cluster.

```sh
ibmcloud ks logging config rm --cluster CLUSTER_NAME_OR_ID --namespace NAME
```
{: pre}


### `ibmcloud oc logging config update`
{: #logging-config-update-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} 

Update a log forwarding configuration for a cluster.
{: shortdesc}

```sh
ibmcloud oc logging config update --cluster CLUSTER --id ID --logsource LOGSOURCE --type TYPE [--force-update] [--hostname HOSTNAME] [--output OUTPUT] [--port PORT] [-q] --ca-cert CERT --syslog-protocol PROTOCOL --verify-mode MODE --namespace NAMESPACE
```
{: pre}

#### Command options
{: #logging-config-update-options}


`-C CONTAINER`, `--app-container CONTAINER`
:    Specify the containers that you want to collect logs for. To specify more than one path, use multiple flags, such as `-C container1 -C container2`. This option is required for the `application` log source. If not provided, logs are collected from all containers from the application log paths passed in.

`--ca-cert CERT`
:    When the logging type is `syslog` and the protocol is tls, the Kubernetes secret name that contains the Certificate Authority certificate.

`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`--force-update`
:    Force an update of the Fluentd pods in the cluster to the latest version.

`--hostname HOSTNAME`
:    When logging type is `syslog`, the hostname or IP address of the log collector. When logging type is `ibm` (deprecated), the logging ingest endpoint. If you do not provide the logging ingest endpoint, then the current region's endpoint is used.

`--id ID`
:    Specify the ID of the logging configuration.

`--logsource LOGSOURCE`
:    The source of the logs to forward. Supported values are `container`, `application`, `ingress`, `worker`, `storage`, and `kubernetes`. This argument supports a comma separated list of log sources. If you do not provide a log source, logs for `container` and `ingress` are forwarded.

`--namespace NAMESPACE`, `-n NAMESPACE`
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

Update a log forwarding configuration for a cluster.

```sh
ibmcloud ks logging config update \
  --org ORG \
  --space SPACE \
  -C C \
  -p POOL_NAME \
  --cluster CLUSTER_NAME_OR_ID \
  --id <_id> \
  --namespace NAME
```
{: pre}


### `ibmcloud oc logging filter create`
{: #logging-filter-create-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} 

Filter out logs that are forwarded by your logging configuration.
{: shortdesc}

```sh
ibmcloud oc logging filter create --cluster CLUSTER [--container CONTAINER] [--force-update] [--lc LOGGING-CONFIG ...] [--level LEVEL] [--namespace NAMESPACE] [--output OUTPUT] [-q] [--type TYPE] --message MESSAGE
```
{: pre}

#### Command options
{: #logging-filter-create-options}


`--cluster CLUSTER`, `-c CLUSTER`
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

`--namespace NAMESPACE`, `-n NAMESPACE`
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

Filter out logs that are forwarded by your logging configuration.

```sh
ibmcloud ks logging filter create \
  --cluster CLUSTER_NAME_OR_ID \
  --type TYPE \
  --namespace NAME
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
{: pre}

#### Command options
{: #logging-filter-get-options}


`--cluster CLUSTER`, `-c CLUSTER`
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

View a logging filter configuration.

```sh
ibmcloud ks logging filter get \
  --cluster CLUSTER_NAME_OR_ID \
  --id <_id> \
  --show-matching-configs SHOW-MATCHING-CONFIGS
```
{: pre}


### `ibmcloud oc logging filter rm`
{: #logging-filter-rm-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} 

Delete a logging filter.
{: shortdesc}

```sh
ibmcloud oc logging filter rm --cluster CLUSTER [--force-update] [-q] --all
```
{: pre}

#### Command options
{: #logging-filter-rm-options}


`--all`
:    Delete all log forwarding filters.

`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`--force-update`
:    Force an update of the Fluentd pods in the cluster to the latest version.

`--id ID`
:    Specify the ID of the logging filter.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #logging-filter-rm-examples}

Delete a logging filter.

```sh
ibmcloud ks logging filter rm --cluster CLUSTER_NAME_OR_ID --id FILTER_ID
```
{: pre}


### `ibmcloud oc logging filter update`
{: #logging-filter-update-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} 

Update a logging filter.
{: shortdesc}

```sh
ibmcloud oc logging filter update --cluster CLUSTER --id ID [--container CONTAINER] [--force-update] [--lc LOGGING-CONFIG ...] [--level LEVEL] [--namespace NAMESPACE] [--output OUTPUT] [-q] [--type TYPE] --message MESSAGE
```
{: pre}

#### Command options
{: #logging-filter-update-options}


`--cluster CLUSTER`, `-c CLUSTER`
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

`--namespace NAMESPACE`, `-n NAMESPACE`
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

Update a logging filter.

```sh
ibmcloud ks logging filter update --cluster CLUSTER_NAME_OR_ID --id FILTER_ID --type TYPE
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
{: pre}

#### Command options
{: #logging-refresh-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`--force-update`
:    Force an update of the Fluentd pods in the cluster to the latest version.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #logging-refresh-examples}

Refresh the logging configuration for a cluster.

```sh
ibmcloud ks logging refresh \
  --cluster CLUSTER_NAME_OR_ID \
  --force-update FORCE-UPDATE \
  -q
```
{: pre}



## `ibmcloud oc messages` commands
{: #messages-cli}

View the current user messages.

### `ibmcloud oc messages`
{: #messages-cli}



View the current user messages.
{: shortdesc}

```sh
ibmcloud oc messages [-q]
```
{: pre}

#### Command options
{: #messages-options}


`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #messages-examples}

View the current user messages.

```sh
ibmcloud sat messages -q
```
{: pre}



## `ibmcloud oc nlb-dns` commands
{: #nlb-dns-cli}

Create and manage host names for network load balancer (NLB) IP addresses in a cluster and health check monitors for host names.

### `ibmcloud oc nlb-dns add`
{: #nlb-dns-add-cli}

[Classic infrastructure]{: tag-classic-inf} 

Add an NLB IP to an existing host name that you created with `ibmcloud ks nlb-dns create`.
{: shortdesc}

```sh
ibmcloud oc nlb-dns add --cluster CLUSTER --ip IP [--ip IP ...] --nlb-host HOST [--output OUTPUT] [-q]
```
{: pre}

#### Command options
{: #nlb-dns-add-options}


`--cluster CLUSTER`, `-c CLUSTER`
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

Add an NLB IP to an existing host name that you created with `ibmcloud ks nlb-dns create`.

```sh
ibmcloud ks nlb-dns add \
  --cluster CLUSTER_NAME_OR_ID \
  --ip IP_ADDRESS \
  --nlb-host HOSTNAME
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
{: pre}

#### Command options
{: #nlb-dns-create-classic-options}


`--cluster CLUSTER`, `-c CLUSTER`
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

Create a DNS host name to register one or more NLB IPs in a classic cluster.

```sh
ibmcloud ks nlb-dns create classic \
  --cluster CLUSTER_NAME_OR_ID \
  --ip IP_ADDRESS \
  --secret-namespace NAME
```
{: pre}


### `ibmcloud oc nlb-dns create vpc-gen2`
{: #nlb-dns-create-vpc-gen2-cli}

[Virtual Private Cloud]{: tag-vpc} 

Create a DNS record to register a load balancer host name or load balancer IP addresses in a VPC cluster.
{: shortdesc}

```sh
ibmcloud oc nlb-dns create vpc-gen2 --cluster CLUSTER [--output OUTPUT] [-q] [--secret-namespace NAMESPACE] --ip IP
```
{: pre}

#### Command options
{: #nlb-dns-create-vpc-gen2-options}


`--cluster CLUSTER`, `-c CLUSTER`
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

Create a DNS record to register a load balancer host name or load balancer IP addresses in a VPC cluster.

```sh
ibmcloud ks nlb-dns create vpc-gen2 \
  --cluster CLUSTER_NAME_OR_ID \
  --lb-host HOSTNAME \
  --secret-namespace NAME
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
{: pre}

#### Command options
{: #nlb-dns-get-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`--nlb-subdomain SUBDOMAIN`
:    The subdomain. To see existing subdomains, run `ibmcloud ks nlb-dns ls`.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #nlb-dns-get-examples}

View the details of a registered NLB host name in a cluster.

```sh
ibmcloud ks nlb-dns get \
  --cluster CLUSTER_NAME_OR_ID \
  --nlb-subdomain DOMAIN \
  --output json
```
{: pre}


### `ibmcloud oc nlb-dns ls`
{: #nlb-dns-ls-cli}



List the registered NLB host names and IP addresses in a cluster.
{: shortdesc}

```sh
ibmcloud oc nlb-dns ls --cluster CLUSTER [--output OUTPUT] [-q]
```
{: pre}

#### Command options
{: #nlb-dns-ls-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #nlb-dns-ls-examples}

List the registered NLB host names and IP addresses in a cluster.

```sh
ibmcloud ks nlb-dns ls --cluster CLUSTER_NAME_OR_ID --output json -q
```
{: pre}


### `ibmcloud oc nlb-dns monitor configure`
{: #nlb-dns-monitor-configure-cli}



Configure a health check monitor for an existing NLB host name in a cluster. To enable the monitor, include the `--enable` flag. To update an existing monitor, include only the flags for the settings that you want to change.
{: shortdesc}

```sh
ibmcloud oc nlb-dns monitor configure --cluster CLUSTER --nlb-host HOST [--enable] [--header HEADER ...] [--interval INTERVAL] [--output OUTPUT] [--path PATH] [--port PORT] [-q] [--timeout TIMEOUT] [--type TYPE]
```
{: pre}

#### Command options
{: #nlb-dns-monitor-configure-options}


`--cluster CLUSTER`, `-c CLUSTER`
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

Configure a health check monitor for an existing NLB host name in a cluster.

```sh
ibmcloud ks nlb-dns monitor configure \
  --port PORT \
  --cluster CLUSTER_NAME_OR_ID \
  --nlb-host HOSTNAME \
  --type TYPE
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
{: pre}

#### Command options
{: #nlb-dns-monitor-disable-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`--nlb-host HOST`
:    The host name. To see existing host names, run `ibmcloud ks nlb-dns ls`.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #nlb-dns-monitor-disable-examples}

Disable an existing health check monitor for a NLB host name in a cluster.

```sh
ibmcloud ks nlb-dns monitor disable \
  --cluster CLUSTER_NAME_OR_ID \
  --nlb-host HOSTNAME \
  --output json
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
{: pre}

#### Command options
{: #nlb-dns-monitor-enable-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`--nlb-host HOST`
:    The host name. To see existing host names, run `ibmcloud ks nlb-dns ls`.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #nlb-dns-monitor-enable-examples}

Enable a health check monitor for an NLB host name in a cluster.

```sh
ibmcloud ks nlb-dns monitor enable \
  --cluster CLUSTER_NAME_OR_ID \
  --nlb-host HOSTNAME \
  --output json
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
{: pre}

#### Command options
{: #nlb-dns-monitor-get-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`--nlb-host HOST`
:    The host name. To see existing host names, run `ibmcloud ks nlb-dns ls`.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #nlb-dns-monitor-get-examples}

View the settings for an existing health check monitor.

```sh
ibmcloud ks nlb-dns monitor get \
  --cluster CLUSTER_NAME_OR_ID \
  --nlb-host HOSTNAME \
  --output json
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
{: pre}

#### Command options
{: #nlb-dns-monitor-ls-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #nlb-dns-monitor-ls-examples}

List the health check monitor settings for each NLB host name in a cluster.

```sh
ibmcloud ks nlb-dns monitor ls --cluster CLUSTER_NAME_OR_ID --output json -q
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
{: pre}

#### Command options
{: #nlb-dns-replace-options}


`--cluster CLUSTER`, `-c CLUSTER`
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

Update an existing DNS host name by replacing the load balancer hostname associated with it in a VPC cluster.

```sh
ibmcloud ks nlb-dns replace \
  --cluster CLUSTER_NAME_OR_ID \
  --nlb-subdomain DOMAIN \
  --lb-host HOSTNAME
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
{: pre}

#### Command options
{: #nlb-dns-rm-classic-options}


`--cluster CLUSTER`, `-c CLUSTER`
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

Remove an NLB IP address from an NLB host name.

```sh
ibmcloud ks nlb-dns rm classic \
  --cluster CLUSTER_NAME_OR_ID \
  --ip IP_ADDRESS \
  --nlb-host HOSTNAME
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
{: pre}

#### Command options
{: #nlb-dns-rm-vpc-gen2-options}


`--cluster CLUSTER`, `-c CLUSTER`
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

Remove a load balancer host name or IP address from a DNS record in a VPC cluster.

```sh
ibmcloud ks nlb-dns rm vpc-gen2 \
  --cluster CLUSTER_NAME_OR_ID \
  --nlb-subdomain DOMAIN \
  --ip IP_ADDRESS
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
{: pre}

#### Command options
{: #nlb-dns-secret-regenerate-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`--nlb-subdomain SUBDOMAIN`
:    The subdomain. To see existing subdomains, run `ibmcloud ks nlb-dns ls`.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #nlb-dns-secret-regenerate-examples}

Regenerate the certificate and secret for an NLB subdomain.

```sh
ibmcloud ks nlb-dns secret regenerate \
  --cluster CLUSTER_NAME_OR_ID \
  --nlb-subdomain DOMAIN \
  --output json
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
{: pre}

#### Command options
{: #nlb-dns-secret-rm-options}


`--cluster CLUSTER`, `-c CLUSTER`
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

Delete a secret from an NLB subdomain and prevent future renewal of the certificate.

```sh
ibmcloud ks nlb-dns secret rm --cluster CLUSTER_NAME_OR_ID --nlb-subdomain DOMAIN -f
```
{: pre}



## `ibmcloud oc quota` commands
{: #quota-cli}

View the quota and limits for cluster-related resources in your IBM Cloud account.

### `ibmcloud oc quota ls`
{: #quota-ls-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

List all quota and limits for cluster-related resources in your IBM Cloud account.
{: shortdesc}

```sh
ibmcloud oc quota ls [--output OUTPUT] [--provider PROVIDER] [-q]
```
{: pre}

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

List all quota and limits for cluster-related resources in your IBM Cloud account.

```sh
ibmcloud ks quota ls --output json --provider PROVIDER_ID -q
```
{: pre}



## `ibmcloud oc script` commands
{: #script-cli}

Rewrite scripts that call IBM Cloud Kubernetes Service plug-in commands. Legacy-structured commands are replaced with beta-structured commands.

### `ibmcloud oc script update`
{: #script-update-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} 

Rewrite scripts that call IBM Cloud Kubernetes Service plug-in commands. Legacy-structured commands are replaced with beta-structured commands.
{: shortdesc}

```sh
ibmcloud oc script update [--in-place] FILE [FILE ...]
```
{: pre}

#### Command options
{: #script-update-options}


`--in-place FILE FILE`
:    Rewrite the source file with the updated command structure.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #script-update-examples}

Rewrite scripts that call IBM Cloud Kubernetes Service plug-in commands.

```sh
ibmcloud ks script update --in-place IN-PLACE -q
```
{: pre}



## `ibmcloud oc security-group` commands
{: #security-group-cli}

Run operations against a security group.

### `ibmcloud oc security-group ls`
{: #security-group-ls-cli}



List all security groups associated with a cluster.
{: shortdesc}

```sh
ibmcloud oc security-group ls --cluster CLUSTER [--attached-to ATTACHED] [--managed-by MANAGER] [--output OUTPUT] [-q] [--scope SCOPE]
```
{: pre}

#### Command options
{: #security-group-ls-options}


`--attached-to ATTACHED`
:    Filter the security groups by the components they are attached to. Accepted values: `cluster`, `load-balancer`, `vpc`, `vpe-gateway`, `worker-pool`

`--cluster CLUSTER`, `-c CLUSTER`
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

List all security groups associated with a cluster.

```sh
ibmcloud ks security-group ls \
  --cluster CLUSTER_NAME_OR_ID \
  --attached-to ATTACHED-TO \
  --scope SCOPE
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
{: pre}

#### Command options
{: #security-group-reset-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`-q`
:    Do not show the message of the day or update reminders.

`--security-group GROUP`, `--sg GROUP`
:    Specify security group ID.


#### Examples
{: #security-group-reset-examples}

Deletes all existing security group rules, and reapplies default rules.

```sh
ibmcloud ks security-group reset \
  --cluster CLUSTER_NAME_OR_ID \
  --security-group GROUP \
  -f
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
{: pre}

#### Command options
{: #security-group-sync-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`-q`
:    Do not show the message of the day or update reminders.

`--security-group GROUP`, `--sg GROUP`
:    Specify security group ID.


#### Examples
{: #security-group-sync-examples}

Reapplies default security group rules that do not exist.

```sh
ibmcloud ks security-group sync --cluster CLUSTER_NAME_OR_ID --security-group GROUP -q
```
{: pre}



## `ibmcloud oc storage` commands
{: #storage-cli}

View and modify storage resources.

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
{: pre}

#### Command options
{: #storage-attachment-create-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.

`--volume VOLUME`
:    Specify the volume ID. To list available volumes, run `ibmcloud ks storage volume ls`.

`--worker WORKER`, `-w WORKER`
:    Specify the worker ID. To list available workers, run `ibmcloud ks workers`.


#### Examples
{: #storage-attachment-create-examples}

Attach a storage volume to a worker node.

```sh
ibmcloud ks storage attachment create \
  --cluster CLUSTER_NAME_OR_ID \
  --worker WORKER_ID \
  --volume VOLUME
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
{: pre}

#### Command options
{: #storage-attachment-get-options}


`--attachment ATTACHMENT`
:    Specify the volume attachment ID. To list available attachments, run `ibmcloud ks storage attachment ls`.

`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.

`--worker WORKER`, `-w WORKER`
:    Specify the worker ID. To list available workers, run `ibmcloud ks workers`.


#### Examples
{: #storage-attachment-get-examples}

Get the details of a volume attachment in a cluster.

```sh
ibmcloud ks storage attachment get \
  --cluster CLUSTER_NAME_OR_ID \
  --worker WORKER_ID \
  --attachment ATTACHMENT
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
{: pre}

#### Command options
{: #storage-attachment-ls-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.

`--worker WORKER`, `-w WORKER`
:    Specify the worker ID. To list available workers, run `ibmcloud ks workers`.


#### Examples
{: #storage-attachment-ls-examples}

List all storage volume attachments of a worker in a cluster.

```sh
ibmcloud ks storage attachment ls \
  --cluster CLUSTER_NAME_OR_ID \
  --worker WORKER_ID \
  --output json
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
{: pre}

#### Command options
{: #storage-attachment-rm-options}


`--attachment ATTACHMENT`
:    Specify the volume attachment ID. To list available attachments, run `ibmcloud ks storage attachment ls`.

`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`-q`
:    Do not show the message of the day or update reminders.

`--worker WORKER`, `-w WORKER`
:    Specify the worker ID. To list available workers, run `ibmcloud ks workers`.


#### Examples
{: #storage-attachment-rm-examples}

Delete a volume attachment from a worker node.

```sh
ibmcloud ks storage attachment rm \
  --cluster CLUSTER_NAME_OR_ID \
  --worker WORKER_ID \
  --attachment ATTACHMENT
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
{: pre}

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

Get the details of a volume.

```sh
ibmcloud ks storage volume get --volume VOLUME --output json -q
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
{: pre}

#### Command options
{: #storage-volume-ls-options}


`--cluster CLUSTER`, `-c CLUSTER`
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

List the details of volumes.

```sh
ibmcloud ks storage volume ls \
  --cluster CLUSTER_NAME_OR_ID \
  --provider PROVIDER_ID \
  --zone ZONE
```
{: pre}



## `ibmcloud oc subnets` commands
{: #subnets-cli}

List available portable subnets in your IBM Cloud infrastructure account.

### `ibmcloud oc subnets`
{: #subnets-cli}



List available portable subnets in your IBM Cloud infrastructure account.
{: shortdesc}

```sh
ibmcloud oc subnets --provider PROVIDER [-l LOCATION ...] [--output OUTPUT] [-q] [--vpc-id ID] [--zone ZONE]
```
{: pre}

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

List available portable subnets in your IBM Cloud infrastructure account.

```sh
ibmcloud ks subnets \
  --vpc-id VPC_ID \
  --zone ZONE \
  --output json \
  --provider PROVIDER_ID \
  -l L
```
{: pre}



## `ibmcloud oc versions` commands
{: #versions-cli}

List all the container platform versions that are available for IBM Cloud Kubernetes Service clusters.

### `ibmcloud oc versions`
{: #versions-cli}



List all the container platform versions that are available for IBM Cloud Kubernetes Service clusters.
{: shortdesc}

```sh
ibmcloud oc versions [--output OUTPUT] [-q] [--show-version VERSION]
```
{: pre}

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

List all the container platform versions that are available for IBM Cloud Kubernetes Service clusters.

```sh
ibmcloud ks versions --output json --show-version VERSION -q
```
{: pre}



## `ibmcloud oc vlan` commands
{: #vlan-cli}

List public and private VLANs for a zone and view the VLAN spanning status.

### `ibmcloud oc vlan ls`
{: #vlan-ls-cli}

[Classic infrastructure]{: tag-classic-inf} 

List available public and private VLANs for a zone.
{: shortdesc}

```sh
ibmcloud oc vlan ls --zone ZONE [--output OUTPUT] [-q]
```
{: pre}

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

List available public and private VLANs for a zone.

```sh
ibmcloud ks vlan ls --zone ZONE --output json -q
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
{: pre}

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

View the VLAN spanning status for your IBM Cloud classic infrastructure account.

```sh
ibmcloud ks vlan spanning get --output json --region REGION -q
```
{: pre}



## `ibmcloud oc vni` commands
{: #vni-cli}

Attach, detach, and list Virtual Network Interfaces on worker nodes.

### `ibmcloud oc vni attach baremetal`
{: #vni-attach-baremetal-cli}

[Virtual Private Cloud]{: tag-vpc} 

Attach a Virtual Network Interface to a bare metal worker node or cluster.
{: shortdesc}

```sh
ibmcloud oc vni attach baremetal --vlan VLAN --vni VNI [--auto-delete] [--output OUTPUT] [-q] --cluster-id ID
```
{: pre}

#### Command options
{: #vni-attach-baremetal-options}


`--auto-delete`
:    Automatically delete the VNI when it is removed from the cluster.

`--cluster-id ID`, `-c ID`
:    The ID of the cluster.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.

`--vlan VLAN`
:    The VLAN ID for the bare metal node attachment. Must be unique for each VPC subnet. Multiple VNIs from the same subnet can reuse the VLAN ID. Valid range: 1-500.

`--vni VNI`
:    The ID of the Virtual Network Interface to attach. You must specify VNIs without any current target resource. To list all the VNIs, run `ibmcloud is vnis`. To check if a specific VNI is already attached to a resource, check for the "Target" field in 'ibmcloud is vni <VNI_ID>.

`--worker WORKER`, `-w WORKER`
:    The ID of the worker node.


#### Examples
{: #vni-attach-baremetal-examples}

Attach a Virtual Network Interface to a bare metal worker node or cluster.

```sh
ibmcloud ks vni attach baremetal \
  --cluster-id CLUSTER_NAME_OR_ID \
  --worker WORKER_ID \
  --vni VNI
```
{: pre}


### `ibmcloud oc vni detach`
{: #vni-detach-cli}

[Virtual Private Cloud]{: tag-vpc} 

Detach a Virtual Network Interface from a worker node or cluster.
{: shortdesc}

```sh
ibmcloud oc vni detach --vni VNI [-f] [--output OUTPUT] [-q] --cluster-id ID
```
{: pre}

#### Command options
{: #vni-detach-options}


`--cluster-id ID`, `-c ID`
:    The ID of the cluster.

`-f`
:    Force the command to run without user prompts.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.

`--vni VNI`
:    The ID of the Virtual Network Interface to detach.

`--worker WORKER`, `-w WORKER`
:    The ID of the worker node.


#### Examples
{: #vni-detach-examples}

Detach a Virtual Network Interface from a worker node or cluster.

```sh
ibmcloud ks vni detach --cluster-id CLUSTER_NAME_OR_ID --worker WORKER_ID --vni VNI
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
{: pre}

#### Command options
{: #vni-ls-options}


`--after AFTER`
:    Show Virtual Network Interfaces after the given cursor.

`--cluster-id ID`, `-c ID`
:    The ID of the cluster.

`--first FIRST`
:    View the next Virtual Network Interfaces, up to the first number of VNIs.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.

`--worker WORKER`, `-w WORKER`
:    The ID of the worker node.


#### Examples
{: #vni-ls-examples}

List Virtual Network Interfaces attached to a cluster or worker node.

```sh
ibmcloud ks vni ls --cluster-id CLUSTER_ID
```
{: pre}



## `ibmcloud oc vpc` commands
{: #vpc-cli}

Get information about VPCs and manage VPC clusters.

### `ibmcloud oc vpc ls`
{: #vpc-ls-cli}



List all VPCs in the targeted resource group. If no resource group is targeted, all VPCs in the account are listed.
{: shortdesc}

```sh
ibmcloud oc vpc ls [--output OUTPUT] [--provider PROVIDER] [-q]
```
{: pre}

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

List all VPCs in the targeted resource group.

```sh
ibmcloud ks vpc ls --provider PROVIDER_ID --output json -q
```
{: pre}


### `ibmcloud oc vpc outbound-traffic-protection disable`
{: #vpc-outbound-traffic-protection-disable-cli}



Disable outbound traffic protection for a Secure By Default VPC cluster.
{: shortdesc}

```sh
ibmcloud oc vpc outbound-traffic-protection disable --cluster CLUSTER [-f] [-q]
```
{: pre}

#### Command options
{: #vpc-outbound-traffic-protection-disable-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #vpc-outbound-traffic-protection-disable-examples}

Disable outbound traffic protection for a Secure By Default VPC cluster.

```sh
ibmcloud ks vpc outbound-traffic-protection disable --cluster CLUSTER_NAME_OR_ID -f -q
```
{: pre}


### `ibmcloud oc vpc outbound-traffic-protection enable`
{: #vpc-outbound-traffic-protection-enable-cli}



Enable outbound traffic protection for a Secure By Default VPC cluster.
{: shortdesc}

```sh
ibmcloud oc vpc outbound-traffic-protection enable --cluster CLUSTER [-f] [-q]
```
{: pre}

#### Command options
{: #vpc-outbound-traffic-protection-enable-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #vpc-outbound-traffic-protection-enable-examples}

Enable outbound traffic protection for a Secure By Default VPC cluster.

```sh
ibmcloud ks vpc outbound-traffic-protection enable --cluster CLUSTER_NAME_OR_ID -f -q
```
{: pre}


### `ibmcloud oc vpc secure-by-default enable`
{: #vpc-secure-by-default-enable-cli}



Enable Secure By Default VPC Networking for a VPC cluster using legacy Security Groups.
{: shortdesc}

```sh
ibmcloud oc vpc secure-by-default enable --cluster CLUSTER [--disable-outbound-traffic-protection] [-f] [-q]
```
{: pre}

#### Command options
{: #vpc-secure-by-default-enable-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`--disable-outbound-traffic-protection`
:    Include this option to allow public outbound access from the cluster workers. By default, public outbound access is blocked.

`-f`
:    Force the command to run without user prompts.

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #vpc-secure-by-default-enable-examples}

Enable Secure By Default VPC Networking for a VPC cluster using legacy Security Groups.

```sh
ibmcloud ks vpc secure-by-default enable \
  --cluster CLUSTER_NAME_OR_ID \
  -f \
  --disable-outbound-traffic-protection DISABLE-OUTBOUND-TRAFFIC-PROTECTION
```
{: pre}



## `ibmcloud oc webhook-create` commands
{: #webhook-create-cli}

Register a webhook in a cluster.

### `ibmcloud oc webhook-create`
{: #webhook-create-cli}



Register a webhook in a cluster.
{: shortdesc}

```sh
ibmcloud oc webhook-create --cluster CLUSTER --type TYPE --url URL [--level LEVEL] [-q]
```
{: pre}

#### Command options
{: #webhook-create-options}


`--cluster CLUSTER`, `-c CLUSTER`
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

Register a webhook in a cluster.

```sh
ibmcloud ks webhook-create --cluster CLUSTER_NAME_OR_ID --type TYPE --url URL
```
{: pre}



## `ibmcloud oc worker` commands
{: #worker-cli}

View and modify worker nodes for a cluster.

### `ibmcloud oc worker get`
{: #worker-get-cli}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [Satellite]{: tag-satellite} 

View the details of a worker node.
{: shortdesc}

```sh
ibmcloud oc worker get --cluster CLUSTER --worker WORKER [--output OUTPUT] [-q]
```
{: pre}

#### Command options
{: #worker-get-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.

`--worker WORKER`, `-w WORKER`
:    Specify the worker ID. To list available workers, run `ibmcloud ks workers`.


#### Examples
{: #worker-get-examples}

View the details of a worker node.

```sh
ibmcloud ks worker get --cluster CLUSTER_NAME_OR_ID --worker WORKER_ID --output json
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
{: pre}

#### Command options
{: #worker-ls-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.

`--show-delete-reason`
:    Show the reason for worker node deletion.

`--show-deleted`
:    Show worker nodes that were deleted from the cluster.

`--show-pools`
:    See the worker pool that each worker belongs to.

`--worker-pool POOL`, `-p POOL`
:    Show only worker nodes that belong to the worker pool you specify.


#### Examples
{: #worker-ls-examples}

List all worker nodes in a cluster.

```sh
ibmcloud ks worker ls \
  --cluster CLUSTER_NAME_OR_ID \
  --worker-pool POOL_NAME \
  --show-pools
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
{: pre}

#### Command options
{: #worker-reboot-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`--hard`
:    Force a hard restart of a worker node by cutting off power to the worker node. Use this option if the worker node is unresponsive or the worker node has a Docker hang.

`-q`
:    Do not show the message of the day or update reminders.

`--skip-master-health`
:    Skips checking of master health before initiating action.

`--worker WORKER`, `-w WORKER`
:    Specify one or more worker IDs.


#### Examples
{: #worker-reboot-examples}

Restart a worker node.

```sh
ibmcloud ks worker reboot \
  --cluster CLUSTER_NAME_OR_ID \
  --hard HARD \
  --skip-master-health IP_ADDRESS
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
{: pre}

#### Command options
{: #worker-reload-options}


`-f`
:    Force the command to run without user prompts.

`-q`
:    Do not show the message of the day or update reminders.

`--skip-master-health`
:    Skips checking of master health before initiating action.

`--worker WORKER`, `-w WORKER`
:    Specify one or more worker IDs.


#### Examples
{: #worker-reload-examples}

Delete the data, reimage, and reinstall Kubernetes with the latest patch version on one or more worker nodes.

```sh
ibmcloud ks worker reload --skip-master-health IP_ADDRESS -f --worker WORKER_ID
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
{: pre}

#### Command options
{: #worker-replace-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`-q`
:    Do not show the message of the day or update reminders.

`--update`
:    Update the worker node to the same major and minor version of the master and the latest patch. Also updates the operating system if the worker pool operating system has been updated.

`--worker WORKER`, `-w WORKER`
:    Specify the worker ID. To list available workers, run `ibmcloud ks workers`.


#### Examples
{: #worker-replace-examples}

Delete a worker node and replace it with a new worker node in the same worker pool.

```sh
ibmcloud ks worker replace \
  --cluster CLUSTER_NAME_OR_ID \
  --worker WORKER_ID \
  --update UPDATE
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
{: pre}

#### Command options
{: #worker-rm-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`-q`
:    Do not show the message of the day or update reminders.

`--worker WORKER`, `-w WORKER`
:    Specify one or more worker IDs.


#### Examples
{: #worker-rm-examples}

Remove a worker node from a cluster.

```sh
ibmcloud ks worker rm --cluster CLUSTER_NAME_OR_ID -f --worker WORKER_ID
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
{: pre}

#### Command options
{: #worker-update-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`-q`
:    Do not show the message of the day or update reminders.

`--worker WORKER`, `-w WORKER`
:    Specify one or more worker IDs.


#### Examples
{: #worker-update-examples}

Update one or more worker nodes in a classic cluster to a new Kubernetes version.

```sh
ibmcloud ks worker update --cluster CLUSTER_NAME_OR_ID -f --worker WORKER_ID
```
{: pre}



## `ibmcloud oc worker-pool` commands
{: #worker-pool-cli}

View and modify worker pools for a cluster.

### `ibmcloud oc worker-pool create classic`
{: #worker-pool-create-classic-cli}

[Classic infrastructure]{: tag-classic-inf} 

Add a worker pool to a classic cluster. No worker nodes are created until zones are added to the worker pool.
{: shortdesc}

```sh
ibmcloud oc worker-pool create classic --cluster CLUSTER --flavor FLAVOR --name NAME --size-per-zone SIZE [--disable-disk-encrypt] [--entitlement ENTITLEMENT] [--hardware HARDWARE] [--label LABEL ...] [--operating-system SYSTEM] [--output OUTPUT] [-q]
```
{: pre}

#### Command options
{: #worker-pool-create-classic-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`--disable-disk-encrypt`
:    Disable encryption on a worker node.

`--entitlement ENTITLEMENT`
:    Set this flag to `ocp_entitled` only if you use this cluster with a license such as a Cloud Pak that has an OpenShift entitlement.

`--flavor FLAVOR`
:    The flavor of a worker node. To see available flavors, run `ibmcloud ks flavor ls --zone <zone name>` (for public IBM Cloud accounts) or `ibmcloud ks flavor ls` (for IBM Cloud Dedicated accounts).

`--hardware HARDWARE`
:    The level of hardware isolation for your worker node. Use `dedicated` to have available physical resources dedicated to you only, or `shared` to allow physical resources to be shared with other IBM customers. For IBM Cloud Public accounts, the default value is shared. For IBM Cloud Dedicated accounts, dedicated is the only available option.

`--label LABEL`, `-l LABEL`
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

Add a worker pool to a classic cluster.

```sh
ibmcloud ks worker-pool create classic \
  --name NAME \
  --cluster CLUSTER_NAME_OR_ID \
  --size-per-zone ZONE
```
{: pre}


### `ibmcloud oc worker-pool create satellite`
{: #worker-pool-create-satellite-cli}



Add a worker pool to an IBM Cloud Satellite cluster. No worker nodes are created until zones are added to the worker pool.
{: shortdesc}

```sh
ibmcloud oc worker-pool create satellite --cluster CLUSTER --host-label LABEL [--host-label LABEL ...] --name NAME --size-per-zone SIZE --zone ZONE [--entitlement ENTITLEMENT] [--label LABEL ...] [--operating-system SYSTEM] [--output OUTPUT] [-q]
```
{: pre}

#### Command options
{: #worker-pool-create-satellite-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`--entitlement ENTITLEMENT`
:    Set this flag to `ocp_entitled` only if you use this cluster with a license such as a Cloud Pak that has an OpenShift entitlement.

`--host-label LABEL`, `--hl LABEL`
:    Enter any labels as key-value pairs to identify the host to assign to your Satellite control plane or Red Hat OpenShift cluster. The first host that has this label and is unassigned is automatically assigned to the control plane or cluster. To find available host labels, run `ibmcloud sat host get --host <host_name_or_ID> --location <location_name_or_ID>`.

`--label LABEL`, `-l LABEL`
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

Add a worker pool to an IBM Cloud Satellite cluster.

```sh
ibmcloud ks worker-pool create satellite \
  --name NAME \
  --cluster CLUSTER_NAME_OR_ID \
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
{: pre}

#### Command options
{: #worker-pool-create-vpc-classic-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`--entitlement ENTITLEMENT`
:    Set this flag to `ocp_entitled` only if you use this cluster with a license such as a Cloud Pak that has an OpenShift entitlement.

`--flavor FLAVOR`
:    The flavor of a worker node. To see available flavors, run `ibmcloud ks flavor ls --zone <zone name>` (for public IBM Cloud accounts) or `ibmcloud ks flavor ls` (for IBM Cloud Dedicated accounts).

`--label LABEL`, `-l LABEL`
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

Add a worker pool to a VPC Gen 1 cluster.

```sh
ibmcloud ks worker-pool create vpc-classic \
  --name NAME \
  --cluster CLUSTER_NAME_OR_ID \
  --flavor FLAVOR
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
{: pre}

#### Command options
{: #worker-pool-create-vpc-gen2-options}


`--cluster CLUSTER`, `-c CLUSTER`
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

`--label LABEL`, `-l LABEL`
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

Add a worker pool to a VPC Gen 2 cluster.

```sh
ibmcloud ks worker-pool create vpc-gen2 \
  --name NAME \
  --cluster CLUSTER_NAME_OR_ID \
  --flavor FLAVOR
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
{: pre}

#### Command options
{: #worker-pool-get-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.

`--worker-pool POOL`, `-p POOL`
:    Specify a worker pool.


#### Examples
{: #worker-pool-get-examples}

List the details of a worker pool.

```sh
ibmcloud ks worker-pool get \
  --cluster CLUSTER_NAME_OR_ID \
  --worker-pool POOL_NAME \
  --output json
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
{: pre}

#### Command options
{: #worker-pool-label-rm-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`-q`
:    Do not show the message of the day or update reminders.

`--worker-pool POOL`, `-p POOL`
:    Specify a worker pool.


#### Examples
{: #worker-pool-label-rm-examples}

Remove all custom Kubernetes labels from all worker nodes in a worker pool.

```sh
ibmcloud ks worker-pool label rm \
  --cluster CLUSTER_NAME_OR_ID \
  --worker-pool POOL_NAME \
  -f
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
{: pre}

#### Command options
{: #worker-pool-label-set-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`--label LABEL`, `-l LABEL`
:    Set custom Kubernetes labels in the format `key=value` for all the worker nodes in the worker pool. For multiple labels, repeat this flag. To keep any existing custom labels on the worker pool, include those labels with this flag.

`-q`
:    Do not show the message of the day or update reminders.

`--worker-pool POOL`, `-p POOL`
:    Specify a worker pool.


#### Examples
{: #worker-pool-label-set-examples}

Set custom Kubernetes labels for all worker nodes in a worker pool.

```sh
ibmcloud ks worker-pool label set \
  --cluster CLUSTER_NAME_OR_ID \
  --worker-pool POOL_NAME \
  --label <key=value>
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
{: pre}

#### Command options
{: #worker-pool-ls-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.


#### Examples
{: #worker-pool-ls-examples}

List all worker pools in a cluster.

```sh
ibmcloud ks worker-pool ls --cluster CLUSTER_NAME_OR_ID --output json -q
```
{: pre}


### `ibmcloud oc worker-pool operating-system set`
{: #worker-pool-operating-system-set-cli}



Set the operating system. After you set the operating system, you must update your workers by running either `ibmcloud ks worker update` or `ibmcloud ks worker replace`.
{: shortdesc}

```sh
ibmcloud oc worker-pool operating-system set --cluster CLUSTER --operating-system SYSTEM --worker-pool POOL [-q]
```
{: pre}

#### Command options
{: #worker-pool-operating-system-set-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`--operating-system SYSTEM`
:    Specify the name of the operating system.

`-q`
:    Do not show the message of the day or update reminders.

`--worker-pool POOL`, `-p POOL`
:    Specify a worker pool.


#### Examples
{: #worker-pool-operating-system-set-examples}

Set the operating system.

```sh
ibmcloud ks worker-pool operating-system set \
  --cluster CLUSTER_NAME_OR_ID \
  --worker-pool POOL_NAME \
  --operating-system OS
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
{: pre}

#### Command options
{: #worker-pool-rebalance-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`-q`
:    Do not show the message of the day or update reminders.

`--worker-pool POOL`, `-p POOL`
:    Specify a worker pool.


#### Examples
{: #worker-pool-rebalance-examples}

Rebalance a worker pool in a cluster.

```sh
ibmcloud ks worker-pool rebalance \
  --cluster CLUSTER_NAME_OR_ID \
  --worker-pool POOL_NAME \
  -f
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
{: pre}

#### Command options
{: #worker-pool-resize-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`-q`
:    Do not show the message of the day or update reminders.

`--size-per-zone SIZE`
:    Specify the desired number of workers per zone in this worker pool.

`--worker-pool POOL`, `-p POOL`
:    Specify a worker pool.


#### Examples
{: #worker-pool-resize-examples}

Resize the worker pool to the number of workers per zone that you specify.

```sh
ibmcloud ks worker-pool resize \
  --cluster CLUSTER_NAME_OR_ID \
  --worker-pool POOL_NAME \
  --size-per-zone ZONE
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
{: pre}

#### Command options
{: #worker-pool-rm-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`-q`
:    Do not show the message of the day or update reminders.

`--worker-pool POOL`, `-p POOL`
:    Specify a worker pool.


#### Examples
{: #worker-pool-rm-examples}

Remove a worker pool from a cluster.

```sh
ibmcloud ks worker-pool rm --cluster CLUSTER_NAME_OR_ID --worker-pool POOL_NAME -f
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
{: pre}

#### Command options
{: #worker-pool-taint-rm-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`-q`
:    Do not show the message of the day or update reminders.

`--worker-pool POOL`, `-p POOL`
:    Specify a worker pool.


#### Examples
{: #worker-pool-taint-rm-examples}

Remove all Kubernetes taints from all worker nodes in a worker pool.

```sh
ibmcloud ks worker-pool taint rm \
  --cluster CLUSTER_NAME_OR_ID \
  --worker-pool POOL_NAME \
  -f
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
{: pre}

#### Command options
{: #worker-pool-taint-set-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`-q`
:    Do not show the message of the day or update reminders.

`--taint TAINT`
:    Sets taints on all the workers in the worker pool. Specify the Kubernetes taint in the format `key=value:effect`. The `key=value` is a pair such as `env=prod` that you use to manage the worker node taint and matching pod tolerations. The `effect` is a Kubernetes taint effect such as `NoSchedule` that describes how the taint works.

`--worker-pool POOL`, `-p POOL`
:    Specify a worker pool.


#### Examples
{: #worker-pool-taint-set-examples}

Set Kubernetes taints for all worker nodes in a worker pool.

```sh
ibmcloud ks worker-pool taint set \
  --cluster CLUSTER_NAME_OR_ID \
  --worker-pool POOL_NAME \
  --taint TAINT
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
{: pre}

#### Command options
{: #worker-pool-zones-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.

`--worker-pool POOL`, `-p POOL`
:    Specify a worker pool.


#### Examples
{: #worker-pool-zones-examples}

View the zones attached to a worker pool.

```sh
ibmcloud ks worker-pool zones \
  --cluster CLUSTER_NAME_OR_ID \
  --worker-pool POOL_NAME \
  --output json
```
{: pre}



## `ibmcloud oc zone` commands
{: #zone-cli}

List availability zones and modify the zones attached to a worker pool.

### `ibmcloud oc zone add classic`
{: #zone-add-classic-cli}

[Classic infrastructure]{: tag-classic-inf} 

Add a zone to one or more worker pools in a classic cluster.
{: shortdesc}

```sh
ibmcloud oc zone add classic --cluster CLUSTER --worker-pool POOL [--worker-pool POOL ...] --zone ZONE [--output OUTPUT] [--private-vlan VLAN] [-q] --private-only
```
{: pre}

#### Command options
{: #zone-add-classic-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`--private-only`
:    Use this flag to prevent a public VLAN from being created. Required only when you specify the `--private-vlan` flag without specifying the `--public-vlan` flag.

`--private-vlan VLAN`
:    Specify the ID of the private VLAN. To see available VLANs, run '. When you specify a private VLAN, you must also specify either the `--public-vlan` flag or the '--private-only' flag.

`--public-vlan VLAN`
:    Specify the ID of the public VLAN. To see available VLANs, run '.

`-q`
:    Do not show the message of the day or update reminders.

`--worker-pool POOL`, `-p POOL`
:    The name of the worker pool to modify. To specify multiple worker pools, use multiple flags, such as `-p pool1 -p pool2`.

`--zone ZONE`
:    Specify the zone for the worker pool in a multizone cluster. To list available zones, run `ibmcloud ks zone ls`.


#### Examples
{: #zone-add-classic-examples}

Add a zone to one or more worker pools in a classic cluster.

```sh
ibmcloud ks zone add classic \
  --private-only \
  --cluster CLUSTER_NAME_OR_ID \
  --zone ZONE \
  --private-vlan VLAN_ID
```
{: pre}


### `ibmcloud oc zone add satellite`
{: #zone-add-satellite-cli}



Add a zone to one or more worker pools in a Satellite cluster.
{: shortdesc}

```sh
ibmcloud oc zone add satellite --cluster CLUSTER --worker-pool POOL [--worker-pool POOL ...] --zone ZONE [--output OUTPUT] [-q]
```
{: pre}

#### Command options
{: #zone-add-satellite-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`--output OUTPUT`
:    Prints the command output in the provided format. Accepted values: `json`

`-q`
:    Do not show the message of the day or update reminders.

`--worker-pool POOL`, `-p POOL`
:    The name of the worker pool to modify. To specify multiple worker pools, use multiple flags, such as `-p pool1 -p pool2`.

`--zone ZONE`
:    Specify the zone for the worker pool in a multizone cluster. To list available zones, run `ibmcloud ks zone ls`.


#### Examples
{: #zone-add-satellite-examples}

Add a zone to one or more worker pools in a Satellite cluster.

```sh
ibmcloud ks zone add satellite --cluster CLUSTER_NAME_OR_ID --zone ZONE --output json
```
{: pre}


### `ibmcloud oc zone add vpc-classic`
{: #zone-add-vpc-classic-cli}



Add a zone to one or more worker pools in a VPC Gen 1 cluster.
{: shortdesc}

```sh
ibmcloud oc zone add vpc-classic --cluster CLUSTER --subnet-id ID --worker-pool POOL --zone ZONE [--output OUTPUT] [-q]
```
{: pre}

#### Command options
{: #zone-add-vpc-classic-options}


`--cluster CLUSTER`, `-c CLUSTER`
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

Add a zone to one or more worker pools in a VPC Gen 1 cluster.

```sh
ibmcloud ks zone add vpc-classic \
  --cluster CLUSTER_NAME_OR_ID \
  --zone ZONE \
  --subnet-id SUBNET_CIDR
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
{: pre}

#### Command options
{: #zone-add-vpc-gen2-options}


`--cluster CLUSTER`, `-c CLUSTER`
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

Add a zone to one or more worker pools in a VPC Gen 2 cluster.

```sh
ibmcloud ks zone add vpc-gen2 \
  --cluster CLUSTER_NAME_OR_ID \
  --zone ZONE \
  --subnet-id SUBNET_CIDR
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
{: pre}

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

List all availability zones in a region.

```sh
ibmcloud ks zone ls \
  --region-only REGION \
  --provider PROVIDER_ID \
  --show-flavors FLAVOR
```
{: pre}


### `ibmcloud oc zone network-set`
{: #zone-network-set-cli}

[Classic infrastructure]{: tag-classic-inf} 

Set the network metadata in a specific zone for the given worker pools in a classic cluster.
{: shortdesc}

```sh
ibmcloud oc zone network-set --cluster CLUSTER --private-vlan VLAN --worker-pool POOL [--worker-pool POOL ...] --zone ZONE [-f] [-q] --private-only
```
{: pre}

#### Command options
{: #zone-network-set-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`--private-only`
:    Unset the public VLAN so that the workers in this zone are connected to a private VLAN only.

`--private-vlan VLAN`
:    Specify the ID of the private VLAN. To see available VLANs, run '.

`--public-vlan VLAN`
:    Specify the ID of the public VLAN. To see available VLANs, run '.

`-q`
:    Do not show the message of the day or update reminders.

`--worker-pool POOL`, `-p POOL`
:    The name of the worker pool to modify. To specify multiple worker pools, use multiple flags, such as `-p pool1 -p pool2`.

`--zone ZONE`
:    Specify the zone for the worker pool in a multizone cluster. To list available zones, run `ibmcloud ks zone ls`.


#### Examples
{: #zone-network-set-examples}

Set the network metadata in a specific zone for the given worker pools in a classic cluster.

```sh
ibmcloud ks zone network-set \
  --cluster CLUSTER_NAME_OR_ID \
  --zone ZONE \
  --private-vlan VLAN_ID
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
{: pre}

#### Command options
{: #zone-rm-options}


`--cluster CLUSTER`, `-c CLUSTER`
:    Specify the cluster name or ID.

`-f`
:    Force the command to run without user prompts.

`-q`
:    Do not show the message of the day or update reminders.

`--worker-pool POOL`, `-p POOL`
:    The name of the worker pool to modify. To specify multiple worker pools, use multiple flags, such as `-p pool1 -p pool2`.

`--zone ZONE`
:    Specify the zone for the worker pool in a multizone cluster. To list available zones, run `ibmcloud ks zone ls`.


#### Examples
{: #zone-rm-examples}

Remove a zone from one or more worker pools in a cluster.

```sh
ibmcloud ks zone rm --cluster CLUSTER_NAME_OR_ID --zone ZONE -f
```
{: pre}
