---

copyright:
  years: 2014, 2021
lastupdated: "2021-04-15"

keywords: openshift, openshift container storage, ocs, vpc, roks

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



# Installing OpenShift Container Storage in your cluster
{: #ocs-storage-install}

OpenShift Container Storage is a highly available storage solution that you can use to manage persistent storage for your containerized databases and other stateful apps in {{site.data.keyword.openshiftlong}} clusters.
{: shortdesc}

**Supported infrastructure provider**:
  * <img src="images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> VPC Generation 2 compute
  * <img src="images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Classic

**Minimum required permissions**: **Administrator** platform access role and the **Manager** service access role for the cluster in {{site.data.keyword.containerlong_notm}}.

## Choosing on an OCS installation path
{: #ocs-install-path}

After [preparing your cluster for OpenShift Container Storage](/docs/openshift?topic=openshift-ocs-storage-prep), you must determine the best installation path of the OCS drivers and operators for your cluster and your desired OCS storage cluster configuration.
{: shortdesc}

The installation method that you choose for OCS determines your configuration options when you create your storage cluster later. If you want to change the configuration later, you must uninstall and reinstall the add-on.
{: important}

You can install OCS in your cluster by using one of the following methods:
  * Installing the [managed cluster add-on for OpenShift Container Storage](#install-ocs-addon).
  * Installing the community OpenShift Container Storage operator from the OperatorHub in the [{{site.data.keyword.openshiftshort}} web console](#ocs-install-oh).

The following table provides an overview of the benefits and supported features for each OCS installation method.

| Feature | OCS cluster add-on | OperatorHub |
|---------------|-------------|-----------------|
| Set up {{site.data.keyword.cos_full_notm}} as your default backing store during installation. | <img src="images/confirm.svg" width="32" alt="Feature available" style="width:32px;" /> |  |
| Granular control over storage cluster volume sizes. | <img src="images/confirm.svg" width="32" alt="Feature available" style="width:32px;" /> | |
| Create a storage cluster from the web console. | | <img src="images/confirm.svg" width="32" alt="Feature available" style="width:32px;" /> |
{: caption="OCS installation path comparison." caption-side="top"}


<br />

## Installing the OCS add-on
{: #install-ocs-addon}

You can install the OCS cluster add-on from the console or the CLI.
{: shortdesc}

Before you install the OCS add-on, [plan your OCS set up](/docs/openshift?topic=openshift-ocs-storage-prep).

### Optional: Setting up an {{site.data.keyword.cos_full_notm}} service instance
{: #ocs-create-cos}

If you want to set up {{site.data.keyword.cos_full_notm}} as the default backing store in your OCS storage cluster, create an instance of {{site.data.keyword.cos_full_notm}}. Then, create a set of HMAC credentials and a Kubernetes secret that uses your {{site.data.keyword.cos_short}} HMAC credentials. If you do not specify {{site.data.keyword.cos_full_notm}} credentials during installation, then the default backing store in your OCS storage cluster is created by using the PVs in your cluster. You can [set up additional backing stores](/docs/openshift?topic=openshift-ocs-manage-deployment#ocs-backing-store-setup) after deploying OCS, but you cannot change the default backing store.

[Access your {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-access_cluster).

1. Create an `openshift-storage` namespace in your cluster. The OCS driver pods are deployed to this namespace. Copy the following YAML and save it as `os-namespace.yaml` on your local machine.
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

**Next steps**: Install OCS by using the managed add-on from the [command line](#install-ocs-cli) or the [console](#install-ocs-console).


<br />

### Installing the OpenShift Container Storage add-on from the console
{: #install-ocs-console}

To install OCS in your cluster, complete the following steps.
{: shortdesc}

1. From the [{{site.data.keyword.openshiftshort}} clusters console](https://cloud.ibm.com/kubernetes/clusters?platformType=openshift){: external}, select the cluster for which you want to install the OCS add-on.
2. On the cluster **Overview** page, click **Add-ons**.
3. On the OpenShift Container Storage card, click **Install**.

**Next steps**: [Create your OCS storage cluster](/docs/openshift?topic=openshift-ocs-storage-cluster-setup).

### Installing the OpenShift Container Storage add-on from the CLI
{: #install-ocs-cli}

You can install the OCS add-on by using the [`ibmcloud oc cluster addon enable` command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_cluster_addon_enable).
{: shortdesc}

1. Install the `openshift-container-storage` add-on.
  ```sh
  ibmcloud oc cluster addon enable openshift-container-storage -c <cluster_name>
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

**Next steps**: [Create your OCS storage cluster](/docs/openshift?topic=openshift-ocs-storage-cluster-setup).

### Removing the OpenShift Container Storage add-on from your cluster
{: #ocs-addon-rm}

You can remove OCS add-on from your cluster by using the [{{site.data.keyword.openshiftshort}} clusters console](https://cloud.ibm.com/kubernetes/clusters?platformType=openshift){: external} or the CLI.
{: shortdesc}

When you disable the OpenShift Container Storage add-on, only the OCS operator is removed from your cluster. Your existing workloads remain, but you cannot create more OCS workloads. You also cannot delete your `OcsCluster` custom resource after the operator is removed. If you want to remove all of your OCS resources and data, see [Removing OCS from your cluster](#ocs-vpc-remove-deployment). If you removed the add-on and cannot delete your `OcsCluster`, reinstall the add-on, then delete the `OcsCluster`.
{: note}

#### Uninstalling the OpenShift Container Storage add-on from the console
{: #ocs-addon-rm-console}

To uninstall the OpenShift Container Storage add-on from your cluster, complete the following steps.
{: shortdesc}

1. **Optional**: To remove the add-on and all OCS resources, first [remove OCS from your cluster](#ocs-vpc-remove-deployment).
2. From the [{{site.data.keyword.openshiftshort}} clusters console](https://cloud.ibm.com/kubernetes/clusters?platformType=openshift){: external}, select the cluster for which you want to remove the OpenShift Container Storage add-on.
3. On the cluster **Overview** page, click **Add-ons**.
4. On the OpenShift Container Storage card, click **Uninstall**.

#### Uninstalling the OpenShift Container Storage add-on from the CLI
{: #ocs-addon-rm-cli}

You can uninstall the OpenShift Container Storage add-on from your cluster by using the [{{site.data.keyword.openshiftshort}} clusters console](https://cloud.ibm.com/kubernetes/clusters?platformType=openshift){: external} or the CLI.
{: shortdesc}

1. **Optional**: To remove the add-on and all OCS resources, first [remove OCS from your cluster](#ocs-vpc-remove-deployment).

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

## Installing OpenShift Container Storage from OperatorHub
{: #ocs-install-oh}

Before you can install OCS from OperatorHub, you must deploy the following configmap to your cluster to set update the kubelet path for the OCS drivers.
{: shortdesc}

1. Save the following confimap to a file on your local machine.
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
      name: openshift-storage
  - kind: ConfigMap
    apiVersion: v1
    metadata:
      name: rook-ceph-operator-config
      namespace: openshift-storage # Enter the namespace where you want to install the the OCS Operator.
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
1. In OperatorHub, search for `openshift container storage`.
1. Click the **OpenShift Container Storage** and click **Install**

**Next steps**: [Create your OCS storage cluster](/docs/openshift?topic=openshift-ocs-storage-cluster-setup).
