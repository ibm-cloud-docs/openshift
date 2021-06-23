---

copyright:
  years: 2014, 2021
lastupdated: "2021-06-23"

keywords: openshift, openshift data foundation, openshift container storage, ocs, vpc, roks

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
{:terraform: .ph data-hd-interface='terraform'}
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
  

# Installing OpenShift Data Foundation in your cluster
{: #ocs-storage-install}

OpenShift Data Foundation is a highly available storage solution that you can use to manage persistent storage for your containerized databases and other stateful apps in {{site.data.keyword.openshiftlong}} clusters.
{: shortdesc}

**Supported infrastructure provider**:
  * <img src="images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> VPC
  * <img src="images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Classic
  * <img src="images/icon-satellite.svg" alt="{{site.data.keyword.satelliteshort}} infrastructure provider icon" width="15" style="width:15px; border-style: none"/> {{site.data.keyword.satelliteshort}}

**Minimum required permissions**: **Administrator** platform access role and the **Manager** service access role for the cluster in {{site.data.keyword.containerlong_notm}}.

## Choosing an ODF installation path
{: #ocs-install-path}

After [preparing your cluster for OpenShift Data Foundation](/docs/openshift?topic=openshift-ocs-storage-prep), you must determine the best installation path for your desired storage cluster configuration.
{: shortdesc}

The installation method that you choose determines your configuration options when you create your storage cluster later. If you want to change the configuration later, you must uninstall and reinstall the add-on.
{: important}

You can install ODF in your cluster by using one of the following methods:
  * Installing the [managed cluster add-on for OpenShift Data Foundation](#install-ocs-addon).
  * Installing the OpenShift Data Foundation operator from the OperatorHub in the [{{site.data.keyword.openshiftshort}} web console](#ocs-install-oh).

The following table provides an overview of the benefits and supported features for each installation method.

| Feature | Cluster add-on | OperatorHub |
|---------------|-------------|-----------------|
| Set up {{site.data.keyword.cos_full_notm}} as your default backing store during installation. | <img src="images/confirm.svg" width="32" alt="Feature available" style="width:32px;" /> |  |
| Granular control over storage cluster volume sizes. | <img src="images/confirm.svg" width="32" alt="Feature available" style="width:32px;" /> | |
| Create a storage cluster from the web console. | | <img src="images/confirm.svg" width="32" alt="Feature available" style="width:32px;" /> |
{: caption="Installation path comparison." caption-side="top"}


<br />

## Installing the ODF add-on
{: #install-ocs-addon}

You can install the cluster add-on from the console or the CLI.
{: shortdesc}

Before you install the add-on, [plan your ODF set up](/docs/openshift?topic=openshift-ocs-storage-prep).

### Optional: Setting up an {{site.data.keyword.cos_full_notm}} service instance
{: #ocs-create-cos}

If you want to set up {{site.data.keyword.cos_full_notm}} as the default backing store in your storage cluster, create an instance of {{site.data.keyword.cos_full_notm}}. Then, create a set of HMAC credentials and a Kubernetes secret that uses your {{site.data.keyword.cos_short}} HMAC credentials. If you do not specify {{site.data.keyword.cos_full_notm}} credentials during installation, then the default backing store in your storage cluster is created by using the PVs in your cluster. You can set up additional backing stores after deploying ODF, but you can't change the default backing store.

[Access your {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-access_cluster).

1. Create an `openshift-storage` namespace in your cluster. The driver pods are deployed to this namespace. Copy the following YAML and save it as `os-namespace.yaml` on your local machine.
    ```yaml
    apiVersion: v1
    kind: Namespace
    metadata:
      labels:
        openshift.io/cluster-monitoring: "true"
      name: openshift-storage
    ```
    {: codeblock}

1. Create the `openshift-storage` namespace by using the YAML file that you saved.
    ```sh
    oc create -f os-namespace.yaml
    ```
    {: pre}

1. Verify that the namespace is created.
    ```sh
    oc get namespaces | grep storage
    ```
    {: pre}

1. Create an {{site.data.keyword.cos_full_notm}} service instance.
    ```sh
    ibmcloud resource service-instance-create noobaa-store cloud-object-storage standard global
    ```
    {: pre}

1. Create HMAC credentials. Make a note of your credentials.
    ```sh
    ibmcloud resource service-key-create cos-cred-rw Writer --instance-name noobaa-store --parameters '{"HMAC": true}'
    ```
    {: pre}

1. Create the Kubernetes secret named `ibm-cloud-cos-creds` in the `openshift-storage` namespace that uses your {{site.data.keyword.cos_short}} HMAC credentials. When you run the command, specify your {{site.data.keyword.cos_short}} HMAC access key ID and secret access key. Note that your secret must be named `ibm-cloud-cos-creds`.
    ```sh
    oc -n 'openshift-storage' create secret generic 'ibm-cloud-cos-creds' --type=Opaque --from-literal=IBM_COS_ACCESS_KEY_ID=<access_key_id> --from-literal=IBM_COS_SECRET_ACCESS_KEY=<secret_access_key>
    ```
    {: pre}

1. Verify that your secret is created.
    ```sh
    oc get secrets -A | grep cos
    ```
    {: pre}

**Next steps**: Install ODF by using the managed add-on from the [command line](#install-odf-cli) or the [console](#install-ocs-console).


<br />

### Installing the OpenShift Data Foundation add-on from the console
{: #install-ocs-console}

To install ODF in your cluster, complete the following steps.
{: shortdesc}

1. From the [{{site.data.keyword.openshiftshort}} clusters console](https://cloud.ibm.com/kubernetes/clusters?platformType=openshift){: external}, select the cluster for which you want to install the add-on.
2. On the cluster **Overview** page, click **Add-ons**.
3. On the OpenShift Data Foundation card, click **Install**.

**Next steps**: [Create your storage cluster](/docs/openshift?topic=openshift-ocs-storage-cluster-setup).

### Installing the add-on from the CLI
{: #install-odf-cli}

You can install the add-on by using the [`ibmcloud oc cluster addon enable` command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_cluster_addon_enable).
{: shortdesc}


The default version of the OpenShift Data Foundation add-on is 4.7.0. If you have a cluster version other than the default, you must specify the `--version 4.6.0` flag when you enable the add-on.
{: note}

1. Review the add-on configuration options.
  ```sh
  ibmcloud cluster addon options --addon openshift-container-storage
  ```
  {: pre}

  ```sh
  Add-on Options
  Option                Default Value   
  monStorageClassName   ibmc-vpc-block-metro-10iops-tier   
  osdSize               250Gi   
  osdDevicePaths        invalid   
  workerNodes           all   
  ocsUpgrade            false   
  ocsDeploy             false   
  monSize               20Gi   
  numOfOsd              1   
  monDevicePaths        invalid   
  osdStorageClassName   ibmc-vpc-block-metro-10iops-tier
  ```
  {: screen}

1. Enable the `openshift-container-storage` add-on and specify the `"ocsDeploy=true"` true. If you want to override any of the default parameters, specify the `--param "key=value"` flag for each parameter you want to override. For more information, see the parameters and the default values, see the [VPC parameter reference](/docs/openshift?topic=openshift-ocs-storage-cluster-setup#ocs-vpc-param-ref).

  ```sh
  ibmcloud oc cluster addon enable openshift-container-storage -c <cluster_name> --version <version> --param "ocsDeploy=true"
  ```
  {: pre}

  **Example command for overriding the `osdSize` parameter**:
  ```sh
  ibmcloud oc cluster addon enable openshift-container-storage -c <cluster_name> --version <version> --param "ocsDeploy=true" --param "osdSize=500Gi"
  ```
  {: pre}

1. Verify the add-on is in a `Ready` state.
  ```sh
  ibmcloud oc cluster addon ls -c <cluster_name>
  ```
  {: pre}

1. Verify that the `ibm-ocs-operator-controller-manager-*****` pod is running in the `kube-system` namespace.
  ```sh
  oc get pods -A | grep ibm-ocs-operator-controller-manager
  ```
  {: pre}


### Removing the OpenShift Data Foundation add-on from your cluster
{: #ocs-addon-rm}

You can remove ODF add-on from your cluster by using the [{{site.data.keyword.openshiftshort}} clusters console](https://cloud.ibm.com/kubernetes/clusters?platformType=openshift){: external} or the CLI.
{: shortdesc}

When you disable the OpenShift Data Foundation add-on, only the ODF operator is removed from your cluster. Your existing workloads remain, but you cannot create more ODF workloads. You also cannot delete your `OcsCluster` custom resource after the operator is removed. If you want to remove all of your ODF resources and data, see [Removing ODF from your cluster](/docs/openshift?topic=openshift-ocs-manage-deployment#ocs-remove-storage-cluster). If you removed the add-on and cannot delete your `OcsCluster`, reinstall the add-on, then delete the `OcsCluster`.
{: note}

#### Uninstalling the OpenShift Data Foundation add-on from the console
{: #ocs-addon-rm-console}

To remove the OpenShift Data Foundation add-on from your cluster, complete the following steps.
{: shortdesc}

1. **Optional**: To remove the add-on and all ODF resources, first [remove the add-on from your cluster](/docs/openshift?topic=openshift-ocs-manage-deployment#ocs-remove-storage-cluster).
2. From the [{{site.data.keyword.openshiftshort}} clusters console](https://cloud.ibm.com/kubernetes/clusters?platformType=openshift){: external}, select the cluster for which you want to remove the OpenShift Data Foundation add-on.
3. On the cluster **Overview** page, click **Add-ons**.
4. On the OpenShift Data Foundation card, click **Uninstall**.

#### Uninstalling the OpenShift Data Foundation add-on from the CLI
{: #ocs-addon-rm-cli}

You can uninstall the OpenShift Data Foundation add-on from your cluster by using the [{{site.data.keyword.openshiftshort}} clusters console](https://cloud.ibm.com/kubernetes/clusters?platformType=openshift){: external} or the CLI.
{: shortdesc}

1. **Optional**: To remove the add-on and all ODF resources, first [remove add-on from your cluster](/docs/openshift?topic=openshift-ocs-manage-deployment#ocs-remove-storage-cluster).

2. Uninstall the add-on.
  ```
  ibmcloud oc cluster addon disable openshift-container-storage -c <cluster_name>
  ```
  {: pre}

3. Verify that the add-on is removed.
  ```
  ibmcloud oc cluster addon ls -c <cluster_name>
  ```
  {: pre}

<br />

## Installing OpenShift Data Foundation from OperatorHub
{: #ocs-install-oh}

Before you can install the operator from OperatorHub, you must deploy the following configmap to your cluster to set the kubelet path for the storage drivers.
{: shortdesc}

1. Save the following configmap to a file on your local machine.
  ```yaml
  apiVersion: v1
  kind: List
  metadata:
    name: configmap
  items:
  - apiVersion: v1
    kind: Namespace
    metadata:
      labels:
        openshift.io/cluster-monitoring: "true"
      name: openshift-storage # Enter the namespace where you want to install the OCS Operator.
  - kind: ConfigMap
    apiVersion: v1
    metadata:
      name: rook-ceph-operator-config
      namespace: openshift-storage # Enter the namespace where you want to install the OCS Operator.
    data:
      ROOK_CSI_KUBELET_DIR_PATH: "/var/data/kubelet"
  ```
  {: codeblock}

1. Create the configmap in your cluster.
  ```sh
  oc create -f <configmap.yaml>
  ```
  {: pre}

1. From the web console, click **Operators** > **OperatorHub**.
1. In OperatorHub, search for `OpenShift Data Foundation`.
1. Click the **OpenShift Data Foundation** and click **Install**

**Next steps**: [Create your ODF storage cluster by using the web console](/docs/openshift?topic=openshift-ocs-storage-cluster-setup#ocs-create-storagecluster-console).
