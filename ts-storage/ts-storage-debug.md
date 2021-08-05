---

copyright:
  years: 2014, 2021
lastupdated: "2021-08-05"

keywords: openshift, roks, rhoks, rhos

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
{:audio: .audio}
{:authenticated-content: .authenticated-content}
{:beta: .beta}
{:c#: .ph data-hd-programlang='c#'}
{:c#: data-hd-programlang="c#"}
{:cli: .ph data-hd-interface='cli'}
{:codeblock: .codeblock}
{:curl: #curl .ph data-hd-programlang='curl'}
{:curl: .ph data-hd-programlang='curl'}
{:deprecated: .deprecated}
{:dotnet-standard: .ph data-hd-programlang='dotnet-standard'}
{:download: .download}
{:external: .external target="_blank"}
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
{:middle: .ph data-hd-position='middle'}
{:navgroup: .navgroup}
{:new_window: target="_blank"}
{:node: .ph data-hd-programlang='node'}
{:note: .note}
{:note:.deprecated}
{:objectc: .ph data-hd-programlang='Objective C'}
{:objectc: data-hd-programlang="objectc"}
{:org_name: data-hd-keyref="org_name"}
{:php: .ph data-hd-programlang='PHP'}
{:php: data-hd-programlang="php"}
{:pre: .pre}
{:preview: .preview}
{:python: .ph data-hd-programlang='python'}
{:python: data-hd-programlang="python"}
{:right: .ph data-hd-position='right'}
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
{:step: data-tutorial-type='step'} 
{:subsection: outputclass="subsection"}
{:support: data-reuse='support'}
{:swift: #swift .ph data-hd-programlang='swift'}
{:swift: .ph data-hd-programlang='swift'}
{:swift: data-hd-programlang="swift"}
{:table: .aria-labeledby="caption"}
{:term: .term}
{:terraform: .ph data-hd-interface='terraform'}
{:tip: .tip}
{:tooling-url: data-tooling-url-placeholder='tooling-url'}
{:topicgroup: .topicgroup}
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
  
  
# Debugging persistent storage failures
{: #debug_storage}
{: troubleshoot}
{: support}

Review the options to debug persistent storage and find the root causes for failures.
{: shortdesc}

## Checking whether the pod that mounts your storage instance is successfully deployed
{: #check-pod-success-deploy}

1. List the pods in your cluster. A pod is successfully deployed if the pod shows a status of **Running**.
   ```sh
   oc get pods
   ```
   {: pre}

2. Get the details of your pod and check whether errors are displayed in the **Events** section of your CLI output.
   ```sh
   oc describe pod <pod_name>
   ```
   {: pre}


3. Retrieve the logs for your app and check whether you can see any error messages.
   ```sh
   oc logs <pod_name>
   ```
   {: pre}

## Restarting your app pod
{: #ts-restart-app-pod}

1. If your pod is part of a deployment, delete the pod and let the deployment rebuild it. If your pod is not part of a deployment, delete the pod and reapply your pod configuration file.
  ```sh
  oc delete pod <pod_name>
  ```
  {: pre}

  ```sh
  oc apply -f <app.yaml>
  ```
  {: pre}

3. If restarting your pod does not resolve the issue, [reload your worker node](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_reload).

4. Verify that you use the latest {{site.data.keyword.cloud_notm}} and {{site.data.keyword.containerlong_notm}} plug-in version.
   ```sh
   ibmcloud update
   ```
   {: pre}

   ```sh
   ibmcloud plugin repo-plugins
   ```
   {: pre}

## Verifying that the storage driver and plug-in pods show a status of **Running**
{: #verify_driver_pod_running_status}

1. List the pods in the `kube-system` project.
   ```sh
   oc get pods -n kube-system
   ```
   {: pre}

2. If the storage driver and plug-in pods do not show a **Running** status, get more details of the pod to find the root cause. Depending on the status of your pod, you might not be able to execute all of the following commands.
   1. Get the names of the containers that run in the driver pod.
      ```sh
      kubectl get pod <pod_name> -n kube-system -o jsonpath="{.spec['containers','initContainers'][*].name}" | tr -s '[[:space:]]' '\n'
      ```
      {: pre}

      Example output for {{site.data.keyword.block_storage_is_short}} with three containers:
      ```sh
      csi-provisioner
      csi-attacher
      iks-vpc-block-driver
      ```
      {: screen}

      Example output for {{site.data.keyword.blockstorageshort}}:
      ```sh
      ibmcloud-block-storage-driver-container
      ```
      {: pre}

   2. Export the logs from the driver pod to a `logs.txt` file on your local machine. Include the driver container name.
      ```sh
      oc logs <pod_name> -n kube-system -c <container_name> > logs.txt
      ```
      {: pre}

   3. Review the log file.
      ```sh
      cat logs.txt
      ```
      {: pre}

3. Analyze the **Events** section of the CLI output of the `oc describe pod` command and the latest logs to find the root cause for the error.

## Checking whether your PVC is successfully provisioned.
{: #check_pvc_provision}


1. Check the state of your PVC. A PVC is successfully provisioned if the PVC shows a status of **Bound**.
   ```sh
   oc get pvc
   ```
   {: pre}

2. If the state of the PVC shows **Pending**, retrieve the error for why the PVC remains pending.
   ```sh
   oc describe pvc <pvc_name>
   ```
   {: pre}

3. Review common errors that can occur during the PVC creation.
   - [File storage and classic block storage: PVC remains in a pending state](/docs/containers?topic=containers-file_pvc_pending)
   - [Object storage: PVC remains in a pending state](/docs/containers?topic=containers-cos_pvc_pending)

4. Review common errors that can occur when you mount a PVC to your app.
   - [File storage: App cannot access or write to PVC](/docs/containers?topic=containers-file_app_failures)
   - [Classic Block storage: App cannot access or write to PVC](/docs/containers?topic=containers-block_app_failures)
   - [Object storage: Accessing files with a non-root user fails](/docs/containers?topic=containers-cos_nonroot_access)

7. Verify that the `kubectl` CLI version that you run on your local machine matches the Kubernetes version that is installed in your cluster. If you use a `kubectl` CLI version that does not match at least the major.minor version of your cluster, you might experience unexpected results. For example, [Kubernetes does not support ![External link icon](../icons/launch-glyph.svg “External link icon”)](https://kubernetes.io/releases/version-skew-policy/) `kubectl` client versions that are 2 or more versions apart from the server version (n +/- 2).
   1. Show the `kubectl` CLI version that is installed in your cluster and your local machine.
      ```sh
      oc version
      ```
      {: pre}

      Example output:
      ```sh
      Client Version: version.Info{Major:"1", Minor:"1.20", GitVersion:"v1.20.7", GitCommit:"641856db18352033a0d96dbc99153fa3b27298e5", GitTreeState:"clean", BuildDate:"2019-03-25T15:53:57Z", GoVersion:"go1.12.1", Compiler:"gc", Platform:"darwin/amd64"}
      Server Version: version.Info{Major:"1", Minor:"1.20", GitVersion:"v1.20.7+IKS", GitCommit:"e15454c2216a73b59e9a059fd2def4e6712a7cf0", GitTreeState:"clean", BuildDate:"2019-04-01T10:08:07Z", GoVersion:"go1.11.5", Compiler:"gc", Platform:"linux/amd64"}
      ```
      {: screen}

      The CLI versions match if you can see the same version in `GitVersion` for the client and the server. You can ignore the `+IKS` part of the version for the server.
   2. If the `kubectl` CLI versions on your local machine and your cluster do not match, either [update your cluster](/docs/containers?topic=containers-update) or [install a different CLI version on your local machine](/docs/containers?topic=containers-cs_cli_install#kubectl).


8. For {{site.data.keyword.block_storage_is_short}}, [verify that you have the latest version of the add-on](/docs/openshift?topic=openshift-vpc-block#vpc-addon-update).

9. For classic block storage, object storage, and Portworx only: Make sure that you installed the latest Helm chart version for the plug-in.

   **Block and object storage**:

   1. Update your Helm chart repositories.
      ```sh
      helm repo update
      ```
      {: pre}

   2. List the Helm charts in the repository.
      **For classic block storage**:
        ```sh
        helm search repo iks-charts | grep block-storage-plugin
        ```
        {: pre}

        Example output:
        ```sh
        iks-charts-stage/ibmcloud-block-storage-plugin	1.5.0        	                                        	A Helm chart for installing ibmcloud block storage plugin   
        iks-charts/ibmcloud-block-storage-plugin      	1.5.0        	                                        	A Helm chart for installing ibmcloud block storage plugin   
        ```
        {: screen}

      **For object storage**:
        ```sh
        helm search repo ibm-charts | grep object-storage-plugin
        ```
        {: pre}

        Example output:
        ```sh
        ibm-charts/ibm-object-storage-plugin         	1.0.9        	1.0.9                         	A Helm chart for installing ibmcloud object storage plugin  
        ```
        {: screen}

   3. List the installed Helm charts in your cluster and compare the version that you installed with the version that is available.
      ```sh
      helm list --all-namespaces
      ```
      {: pre}

   4. If a more recent version is available, install this version. For instructions, see [Updating the {{site.data.keyword.cloud_notm}} Block Storage plug-in](/docs/containers?topic=containers-block_storage#update_block) and [Updating the {{site.data.keyword.cos_full_notm}} plug-in](/docs/openshift?topic=openshift-object_storage#update_cos_plugin).

## Portworx
{: #ts-portworx-helm}

   1. Find the [latest Helm chart version](https://github.com/IBM/charts/tree/master/community/portworx){: external} that is available.

   2. List the installed Helm charts in your cluster and compare the version that you installed with the version that is available.
      ```sh
      helm list --all-namespaces
      ```
      {: pre}

   3. If a more recent version is available, install this version. For instructions, see [Updating Portworx in your cluster](/docs/openshift?topic=openshift-portworx#update_portworx).


## OpenShift Data Foundation 
{: #ts-ocs-debug}

Describe your ODF resources and review the command outputs for any error messages.
{: shortdesc}

1. List the name of your ODF cluster. 
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

1. Describe the storage cluster and review the `Events` section of the output for any error messages. 
    ```sh
    oc describe ocscluster <ocscluster-name>
    ```
    {: pre}

2. List the pods in the `kube-system` namespace and verify that they are `Running.`
    ```sh
    oc get pods -n kube-system
    ```
    {: pre}

4. Describe the `ibm-ocs-operator-controller-manager` pod and review the `Events` section in the output for any error messages.
    ```sh
    oc describe pod <ibm-ocs-operator-controller-manager-a1a1a1a> -n kube-system
    ```
    {: pre}

5. Review the logs of the `ibm-ocs-operator-controller-manager`.
    ```sh
    oc logs <ibm-ocs-operator-controller-manager-a1a1a1a> -n kube-system
    ```
    {: pre}

6. Describe NooBaa and review the `Events` section of the output for any error messages.
    ```sh
    oc describe noobaa -n openshift-storage
    ```
    {: pre}




