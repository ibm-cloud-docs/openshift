---

copyright:
  years: 2021, 2021
lastupdated: "2021-06-22"

keywords: openshift, storage

subcollection: openshift
content-type: troubleshoot

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


# Why does my OpenShift Data Foundation storage cluster have an 'Error' status?
{: #ts-ocs-install-error-status}

{: tsSymptoms}
When you check the status of your ODF storage cluster by running `kubectl describe ocscluster <ocscluster-name>`, the status is `Error`.

{: tsCauses}
To determine why your storage cluster status is `Error`, check the logs of the `ibm-ocs-operator-controller-manager` pod for any error messages.

1. [Access your {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-access_cluster).
2. List the name of your ODF cluster. 
    ```sh
    oc get ocscluster
    ```
    {: pre}
    **Example output**:
    ```
    NAME             AGE
    ocscluster-vpc   71d
    ```
    {: screen}

2. View the status of your ODF cluster.
    ```sh
    oc describe ocscluster <ocscluster-name>
    ```
    {: pre}

2. Get the ID of the `ibm-ocs-operator-controller-manager` pod for your ODF cluster.
    ```sh
    oc get pods -n kube-system | grep ocs
    ```
    {: pre}
    **Example output**:
    ```
    NAME                                                  READY   STATUS    RESTARTS   AGE
    ibm-ocs-operator-controller-manager-f4bd9fd48-kl5tp   1/1     Running   0          11h
    ```
    {: screen}
   
3. Review the logs of the `ibm-ocs-operator-controller-manager` pod for error messages.
    ```sh
    oc logs <ibm-ocs-operator-controller-manager-a1a1a1a> -n kube-system
    ```
   {: pre}
  
{: tsResolve} 
Review the following ODF installation error messages for steps to resolve the related issue.

## Error: Number of worker nodes less than 3.
{: #ts-ocs-install-3workers}

When you describe your ODF storage cluster with the `[{kubectl]} describe ocscluster <ocscluster-name>` command, you see an error message similar to the following: 
```
Error: Number of worker nodes less than 3. At least 3 worker nodes are required for ocs deployment.
```
{: screen}

Fewer than 3 worker nodes are specified for ODF installation. ODF must install on a minimum of 3 worker nodes.

1. [Review the steps to prepare your cluster for ODF](/docs/openshift?topic=openshift-ocs-storage-prep).

2. Make sure that your cluster has at least 3 worker nodes specified for your ODF installation. 
    ```sh
    oc get nodes
    ```
    {: pre}

3. If your cluster does not have at least 3 worker nodes, [resize your worker pool](/docs/openshift?topic=openshift-add_workers#resize_pool).

4. Verify the additional nodes and note the private IP addresses in the `NAME` column of the output.
    ```sh
    oc get nodes
    ```
    {: pre}
    Example output:
    ```
    NAME            STATUS   ROLES           AGE   VERSION
    10.240.128.10   Ready    master,worker   70d   v1.19.0+2f3101c
    10.240.128.11   Ready    master,worker   70d   v1.19.0+2f3101c
    10.240.128.12   Ready    master,worker   70d   v1.19.0+2f3101c
    ```
    {: screen}

5. For classic clusters, [gather the device paths of the local disks on each worker node](/docs/openshift?topic=openshift-ocs-storage-prep#ocs-classic-get-devices).

6. If you have available worker nodes that do not have ODF installed, specify them in the CRD by [adding the private IP address of the nodes you want to specify](/docs/openshift?topic=openshift-ocs-storage-install#install-odf-cli). For classic clusters, you must also [add the device paths of the local disks that you found earlier for each node you want to specify](/docs/openshift?topic=openshift-ocs-storage-cluster-setup#ocs-classic-deploy-crd).

## Error: Failed to update storage cluster
{: #ts-ocs-install-decrease-capacity}

When you describe your cluster with the `oc describe ocscluster <ocscluster-name>` command, you see an error message similar to the following:
    ```
    Error: Failed to update storage cluster: Decreasing the capacity not allowed.
    ```
    {: screen}

A command to scale down ODF has failed because decreasing the storage capacity by decreasing the number of OSDs is not supported. If you want to scale down ODF, you will need to remove the ODF storage cluster, resize the classic or VPC cluster where ODF is installed, and then create and deploy a new storage cluster.

2. List the name of your ODF cluster. 
   ```sh
   oc get ocscluster
   ```
   {: pre}
   **Example output**:
   ```
   NAME             AGE
   ocscluster-vpc   71d
   ```
   {: screen}

3. Delete the storage cluster.
   ```sh
   oc delete ocscluster <ocs_cluster_name>
   ```
   {: pre}

4. Verify that your storage cluster is deleted and is not listed.
   ```sh
   oc get ocscluster
   ```
   {: pre}

5. Optional: If you want to remove worker nodes from your cluster, [resize the classic or VPC cluster where ODF is installed](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_pool_resize). Make sure that your cluster still has at least 3 worker nodes.

6. [Create and deploy a new ODF storage cluster](/docs/openshift?topic=openshift-ocs-storage-cluster-setup). If you want to deploy ODF on all worker nodes in your cluster, make sure that your cluster has at least 3 worker nodes. If you want to deploy ODF on a subset of worker nodes, make sure that you specify the private IP addresses of the worker nodes where you want to install ODF in your CRD.

## Error: Error in reconcile of local volumes
{: #ts-ocs-install-local-volumes}

When you describe your cluster with the `oc describe ocscluster <ocscluster-name>` command, you see an error message similar to the following:
    ```
    Error: "ERROR in reconcile of Local Volumes","error":"DevicePath has to be set for local volumes"
    ```
    {: screen}

You want to deploy ODF on a classic cluster by using local volumes, but the device paths for the disks that are required for ODF are either incorrect or are not specified in your CRD.

1. [Gather the device paths for the local disks on the worker nodes where you want to install ODF on](/docs/openshift?topic=openshift-ocs-storage-prep#ocs-classic-get-devices). 

2. [In your CRD, add the correct device paths to the `monDevicePaths` or `osdDevicePaths` fields](/docs/openshift?topic=openshift-ocs-storage-cluster-setup). 
