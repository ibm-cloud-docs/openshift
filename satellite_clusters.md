---

copyright:
  years: 2014, 2020
lastupdated: "2020-08-03"

keywords: openshift, satellite, distributed cloud, on-prem, hybrid

subcollection: openshift

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


# Creating {{site.data.keyword.satelliteshort}} clusters
{: #satellite-clusters}

You can create {{site.data.keyword.openshiftlong}} clusters in an {{site.data.keyword.satellitelong}} location, and use the hosts of your own infrastructure that you added to your location as the worker nodes for the cluster.
{: shortdesc}

## Creating {{site.data.keyword.satelliteshort}} clusters from the console
{: #satcluster-create-console}

Use the {{site.data.keyword.cloud_notm}} console to create your {{site.data.keyword.satelliteshort}} clusters.
{: shortdesc}

Before you begin, make sure that you [added at least 3 hosts to your location](/docs/satellite?topic=satellite-hosts#add-hosts-console) to use for your {{site.data.keyword.satelliteshort}} cluster.

1. From the [Red Hat OpenShift on IBM Cloud clusters console](https://cloud.ibm.com/kubernetes/clusters?platformType=openshift), click **Create**.
2. In the **Infrastructure** section, select **{{site.data.keyword.satelliteshort}}**.
3. Select the {{site.data.keyword.satelliteshort}} location where you want to create the cluster. Make sure that the location that you select is in a **Normal** state.
4. Enter a name for your cluster. The name must start with a letter, can contain letters, numbers, and hyphen (-), and must be 35 characters or fewer.
5. Click **Create**. When you create the cluster, the cluster master is automatically created in your {{site.data.keyword.satelliteshort}} control plane, but no worker nodes are created for your cluster yet.
6. Wait for the cluster to reach a **Warning** state. The **Warning** state indicates that the cluster master is fully deployed, but no worker nodes could be detected in the cluster.
7. [Assign {{site.data.keyword.satelliteshort}} hosts to your cluster](/docs/satellite?topic=satellite-hosts#host-assign-ui). After the hosts successfully bootstrap, the hosts function as the worker nodes for your cluster to run OpenShift workloads.
8. From the [Red Hat OpenShift on IBM Cloud clusters console](https://cloud.ibm.com/kubernetes/clusters?platformType=openshift), verify that your cluster reaches a **Normal** state.

{{site.data.keyword.satelliteshort}} clusters currently do not show in the {{site.data.keyword.satelliteshort}} cluster console as Razee is not yet automatically installed in these clusters. You must follow the [{{site.data.keyword.satelliteshort documentation](/docs/satellite?topic=satellite-cluster-config#existing-openshift-clusters) to attach the cluster to the {{site.data.keyword.satelliteshort}} Configuration.
{: important}



## Accessing and working with your {{site.data.keyword.satelliteshort}} clusters
{: #satcluster-access}

After you created your {{site.data.keyword.satelliteshort}} cluster, you can use the capabilities in Red Hat OpenShift on IBM Cloud to work with your cluster.
{: shortdesc}

Review common tasks that you might be interested in:

- [Accessing OpenShift clusters](/docs/openshift?topic=openshift-access_cluster)
- [Assigning cluster access](/docs/openshift?topic=openshift-users)

## Removing {{site.data.keyword.satelliteshort}} worker nodes or clusters
{: #satcluster-rm}

When you remove {{site.data.keyword.satelliteshort}} clusters or worker nodes in a cluster, the hosts the provide the compute capacity for your worker nodes are not automatically deleted. Instead, the hosts remain attached to your {{site.data.keyword.satelliteshort}} location, but require you to reload the host to be able to reassign the hosts to other {{site.data.keyword.satelliteshort}} resources. 
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

