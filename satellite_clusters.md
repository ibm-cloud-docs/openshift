---

copyright:
  years: 2014, 2020
lastupdated: "2020-11-17"

keywords: openshift, satellite, distributed cloud, on-prem, hybrid

subcollection: openshift

---

{:DomainName: data-hd-keyref="APPDomain"}
{:DomainName: data-hd-keyref="DomainName"}
{:android: data-hd-operatingsystem="android"}
{:apikey: data-credential-placeholder='apikey'}
{:app_key: data-hd-keyref="app_key"}
{:app_name: data-hd-keyref="app_name"}
{:app_secret: data-hd-keyref="app_secret"}
{:app_url: data-hd-keyref="app_url"}
{:authenticated-content: .authenticated-content}
{:beta: .beta}
{:c#: data-hd-programlang="c#"}
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
{:java: #java .ph data-hd-programlang='java'}
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
{:swift: #swift .ph data-hd-programlang='swift'}
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
{:unity: .ph data-hd-programlang='unity'}
{:url: data-credential-placeholder='url'}
{:user_ID: data-hd-keyref="user_ID"}
{:vb.net: .ph data-hd-programlang='vb.net'}
{:video: .video}


# Creating {{site.data.keyword.openshiftshort}} clusters in {{site.data.keyword.satelliteshort}}
{: #satellite-clusters}

{{site.data.keyword.satellitelong}} is available as a closed beta and subject to change. To register for the beta, see the [product details page](https://cloud.ibm.com/satellite/beta){: external}. For more information, see the [{{site.data.keyword.satellitelong_notm}} documentation](/docs/satellite?topic=satellite-getting-started).
{: beta}

You can create {{site.data.keyword.openshiftlong}} clusters in an {{site.data.keyword.satellitelong}} location, and use the hosts of your own infrastructure that you added to your location as the worker nodes for the cluster.
{: shortdesc}

## Prerequisites
{: #satcluster-prereqs}

Before you can create clusters on your own infrastructure, you must set up an {{site.data.keyword.satellitelong_notm}} location.
{: shortdesc}

1. [Create an {{site.data.keyword.satellitelong_notm}} location](/docs/satellite?topic=satellite-locations#location-create).
2. [Set up the location control plane](/docs/satellite?topic=satellite-locations#setup-control-plane).
3. [Attach at least 3 hosts to your location](/docs/satellite?topic=satellite-hosts#attach-hosts) to use as the worker nodes for your {{site.data.keyword.openshiftlong_notm}} cluster.

<br />

## Creating {{site.data.keyword.openshiftshort}} clusters on {{site.data.keyword.satelliteshort}} from the console
{: #satcluster-create-console}

Use the {{site.data.keyword.cloud_notm}} console to create your {{site.data.keyword.openshiftshort}} clusters on your {{site.data.keyword.satelliteshort}} infrastructure.
{: shortdesc}

1. [Complete the prerequisite steps](#satcluster-prereqs).
2. From the [{{site.data.keyword.openshiftlong_notm}} clusters console](https://cloud.ibm.com/kubernetes/clusters?platformType=openshift), click **Create**.
3. In the **Infrastructure** section, select **{{site.data.keyword.satelliteshort}}**.
4. Select the {{site.data.keyword.satelliteshort}} location where you want to create the cluster. Make sure that the location that you select is in a **Normal** state.
5. Enter a name for your cluster. The name must start with a letter, can contain letters, numbers, and hyphen (-), and must be 35 characters or fewer.
6. Click **Create**. When you create the cluster, the cluster master is automatically created in your {{site.data.keyword.satelliteshort}} control plane, but no worker nodes are created for your cluster yet.
7. Wait for the cluster to reach a **Warning** state. The **Warning** state indicates that the cluster master is fully deployed, but no worker nodes could be detected in the cluster.
8. [Assign {{site.data.keyword.satelliteshort}} hosts to your cluster](/docs/satellite?topic=satellite-hosts#host-assign). After the hosts successfully bootstrap, the hosts function as the worker nodes for your cluster to run {{site.data.keyword.openshiftshort}} workloads. Generally, assign at least 3 hosts as worker nodes in your cluster.
9. From the [{{site.data.keyword.openshiftlong_notm}} clusters console](https://cloud.ibm.com/kubernetes/clusters?platformType=openshift), verify that your cluster reaches a **Normal** state.
10.   If the hosts that you assigned to the cluster are from an Amazon Web Services or Google Cloud Platform cloud provider, you must manually register the cluster DNS. For more information, see the [AWS](/docs/satellite?topic=satellite-providers#aws-reqs-dns-cluster-nlb) or [GCP](/docs/satellite?topic=satellite-providers#gcp-reqs-dns-cluster-nlb) provider topics in the {{site.data.keyword.satelliteshort}} documentation.
11. Optional: [Set up the internal container image registry](#satcluster-internal-registry).

## Creating {{site.data.keyword.openshiftshort}} clusters on {{site.data.keyword.satelliteshort}} from the CLI
{: #satcluster-create-cli}

Use the {{site.data.keyword.satelliteshort}} CLI to create your {{site.data.keyword.openshiftshort}} clusters on your {{site.data.keyword.satelliteshort}} infrastructure.
{: shortdesc}

Before you begin, [install the {{site.data.keyword.satelliteshort}} CLI plug-in](/docs/satellite?topic=satellite-setup-cli).

1. [Complete the prerequisite steps](#satcluster-prereqs).
2. Verify that your location is in a **Normal** state. The location is in a **Normal** state when you successfully created the {{site.data.keyword.satelliteshort}} control plane and all hosts that you use for the control plane are in a healthy state.
   ```
   ibmcloud sat location ls
   ```
   {: pre}

   Example output:
   ```
   Retrieving locations...
   OK
   Name         ID                     Status            Ready   Created      Hosts (used/total)   Managed From   
   mylcoation   brhtfum2015a6mgqj16g   normal            yes     4 days ago   3 / 6                Dallas   
   ```
   {: screen}

3. Create an {{site.data.keyword.openshiftshort}} cluster in your {{site.data.keyword.satelliteshort}} location. When you create the cluster, the cluster master is automatically created in your {{site.data.keyword.satelliteshort}} control plane, but no worker nodes are created for your cluster yet. To add worker nodes, you must later assign compute hosts from your location to your {{site.data.keyword.openshiftshort}} cluster.
   ```
   ibmcloud oc cluster create satellite --name <cluster_name> --location <location_name_or_ID> --version 4.4_openshift
   ```
   {: pre}

   Example output:
   ```
   Creating cluster...
   OK
   Cluster created with ID brkhsd220b6ktv7sjl50
   ```
   {: screen}

   <table summary="This table is read from left to right. The first column has the command component. The second column has the description of the component.">
    <caption>Understanding this command's components</caption>
      <thead>
      <th>Component</th>
      <th>Description</th>
      </thead>
      <tbody>
      <tr>
      <td><code>--name &lt;cluster_name&gt;</code></td>
      <td>Enter a name for your cluster. The name must start with a letter, can contain letters, numbers, and hyphen (-), and must be 35 characters or fewer. </td>
      </tr>
      <tr>
      <td><code>--location &lt;location_name_or_ID&gt;</code></td>
      <td>Enter the name or ID of the location where you want to create the cluster. To retrieve the location name or ID, run <code>ibmcloud sat location ls</code>.</td>
      </tr>
      <tr>
      <td><code>--version</code></td>
      <td>Enter the {{site.data.keyword.openshiftlong_notm}} version that you want to run in your cluster. For a list of supported versions, run <code>ibmcloud oc versions</code>. </td>
      </tr>
      </tbody>
    </table>

4. Wait for the cluster to reach a **Warning** state. The **Warning** state indicates that the cluster master is fully deployed, but no worker nodes could be detected in the cluster.
   ```
   ibmcloud oc cluster ls
   ```
   {: pre}

   Example output:
   ```
   OK
   Name                ID                     State     Created          Workers   Location           Version                 Resource Group Name   Provider   
   satcluster          brkhsd220b6ktv7sjl50   warning   12 minutes ago   0         mylocation.        4.3.23_1525_openshift   Default               satellite  
   ```
   {: screen}

5. [Assign {{site.data.keyword.satelliteshort}} hosts to your cluster](/docs/satellite?topic=satellite-hosts#host-assign-cli). After the hosts successfully bootstrap, the hosts function as the worker nodes for your cluster to run {{site.data.keyword.openshiftshort}} workloads. Generally, assign at least 3 hosts as worker nodes in your cluster.

6. Verify that your cluster reaches a **normal** state.
   ```
   ibmcloud oc cluster ls
   ```
   {: pre}

   Example output:
   ```
   OK
   Name         ID                     State    Created        Workers   Location     Version                 Resource Group Name   Provider   
   satcluster   brkhsd220b6ktv7sjl50   normal   2 hours ago    3         mylocation   4.3.23_1525_openshift   Default               satellite   
   ```
   {: screen}

7. If the hosts that you assigned to the cluster are from an Amazon Web Services or Google Cloud Platform cloud provider, you must manually register the cluster DNS. For more information, see the [AWS](/docs/satellite?topic=satellite-providers#aws-reqs-dns-cluster-nlb) or [GCP](/docs/satellite?topic=satellite-providers#gcp-reqs-dns-cluster-nlb) provider topics in the {{site.data.keyword.satelliteshort}} documentation.

8. Optional: [Set up the internal container image registry](#satcluster-internal-registry).

<br />

## Accessing and working with your {{site.data.keyword.openshiftshort}} clusters
{: #satcluster-access}

After you created your {{site.data.keyword.openshiftshort}} cluster, you can use the capabilities in {{site.data.keyword.openshiftlong_notm}} to work with your cluster.
{: shortdesc}

Review common tasks that you might be interested in:

- [Accessing {{site.data.keyword.openshiftshort}} clusters](/docs/openshift?topic=openshift-access_cluster)
- [Assigning cluster access](/docs/openshift?topic=openshift-users)

<br />

## Setting up the internal container image registry
{: #satcluster-internal-registry}

By default, the internal registry does not run in your {{site.data.keyword.satelliteshort}} cluster because no backing storage is set up for the internal registry. Review the following options to set up the internal registry.
{: shortdesc}

*  **Non-persistent data on the worker node**: See [Storing images in the worker node empty directory](/docs/openshift?topic=openshift-registry#emptydir_internal_registry).
*  **Persistent data in {{site.data.keyword.cos_full_notm}}**: See the resolution steps in [Cluster create error about cloud object storage bucket](/docs/openshift?topic=openshift-cs_troubleshoot#ts_cos_bucket_cluster_create).

By default, the [image registry operator management state](https://docs.openshift.com/container-platform/4.5/registry/configuring-registry-operator.html#registry-operator-configuration-resource-overview_configuring-registry-operator){: external} is set to `Unmanaged`. After you change the storage section in the configmap to use a different solution such as the `emptyDir`, you must update the management state to `Managed`. Then, the operator creates the internal registry pod. Use the following command: `oc patch configs.imageregistry.operator.openshift.io/cluster --type merge -p '{"spec":{"managementState":"Managed"}}'`
{: note}

## Limitations for {{site.data.keyword.openshiftshort}} clusters in {{site.data.keyword.satellitelong_notm}}
{: #satcluster-limitations}

See [{{site.data.keyword.satelliteshort}} cluster limitations](/docs/openshift?topic=openshift-openshift_limitations#satellite_limits).
{: shortdesc}

<br />

## Storing application data in persistent storage
{: #satcluster-storage}

Unlike standard {{site.data.keyword.openshiftshort}} clusters that are created on {{site.data.keyword.cloud_notm}} infrastructure, your {{site.data.keyword.satelliteshort}} clusters do not come installed with a storage driver that provides Kubernetes storage classes that are ready to use with Kubernetes persistent volumes for your apps. However, you can install your own storage driver to set up your apps to save their data in a backing storage device. Review the following common options.
{: shortdesc}

*  Install the [{{site.data.keyword.cos_full_notm}} plug-in](/docs/openshift?topic=openshift-object_storage) in your cluster.
*  Manually set up a storage operator that uses a backing storage provider in your cluster. For more information, see the storage operator provider documentation.
*  Use local storage on the host, such as the [local storage operator](https://docs.openshift.com/container-platform/4.4/storage/persistent_storage/persistent-storage-local.html){: external}.

<br />

## Removing {{site.data.keyword.satelliteshort}} worker nodes or clusters
{: #satcluster-rm}

When you remove {{site.data.keyword.openshiftshort}} clusters or worker nodes in a cluster, the hosts that provide the compute capacity for your worker nodes are not automatically deleted. Instead, the hosts remain attached to your {{site.data.keyword.satelliteshort}} location, but require you to reload the host to be able to reassign the hosts to other {{site.data.keyword.satelliteshort}} resources.
{: shortdesc}

1. Back up any data that runs in the worker node or cluster that you want to save. For example, you might save a copy of all the data in your cluster and upload these files to a persistent storage solution, such as {{site.data.keyword.cos_full_notm}}.
   ```
   oc get all --all-namespaces -o yaml
   ```
   {: pre}
2. Get the **Worker ID** of each host in your cluster.
   ```
   ibmcloud sat host ls --location <satellite_location_name_or_ID>
   ```
   {: pre}

   Example output:
   ```
   Retrieving hosts...
   OK
   Name              ID                     State      Status   Cluster          Worker ID                                                 Worker IP   	
   machine-name-1    aaaaa1a11aaaaaa111aa   assigned   Ready    infrastructure   sat-virtualser-4d7fa07cd3446b1f9d8131420f7011e60d372ca2   169.xx.xxx.xxx   	
   machine-name-2    bbbbbbb22bb2bbb222b2   assigned   Ready    infrastructure   sat-virtualser-9826f0927254b12b4018a95327bd0b45d0513f59   169.xx.xxx.xxx   	
   machine-name-3    ccccc3c33ccccc3333cc   assigned   Ready    mycluster12345   sat-virtualser-948b454ea091bd9aeb8f0542c2e8c19b82c5bf7a   169.xx.xxx.xxx   	
   ```
   {: screen}
3. Remove the worker nodes or clusters by referring to the following options. The corresponding hosts in your {{site.data.keyword.satelliteshort}} location become unassigned and require a reload before you can use them for other {{site.data.keyword.satelliteshort}} resources.
   *  [Resize worker pools](/docs/openshift?topic=openshift-add_workers#resize_pool) to reduce the number of worker nodes in the cluster.
   *  [Remove individual worker nodes](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_rm) from the cluster.
   *  [Remove the cluster](/docs/openshift?topic=openshift-remove).
4. For each worker node that you removed, decide what to do with the corresponding host in your {{site.data.keyword.satelliteshort}} location.
   *  [Reload the host operating system](/docs/satellite?topic=satellite-hosts#host-update) so that you can assign the host to other {{site.data.keyword.satelliteshort}} resources such as the location control plane or other clusters.
   *  Delete the hosts from your underlying infrastructure provider. For more information, refer to the infrastructure provider documentation.
