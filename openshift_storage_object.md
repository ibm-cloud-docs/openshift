---

copyright:
  years: 2014, 2020
lastupdated: "2020-08-17"

keywords: openshift, rhoks, roks, rhos

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



# Storing data on IBM Cloud Object Storage
{: #object_storage}

[{{site.data.keyword.cos_full_notm}}](/docs/cloud-object-storage?topic=cloud-object-storage-getting-started-cloud-object-storage) is persistent, highly available storage that you can mount to your apps. The plug-in is a Kubernetes Flex-Volume plug-in that connects Cloud {{site.data.keyword.cos_short}} buckets to pods in your cluster. Information that is stored with {{site.data.keyword.cos_full_notm}} is encrypted in transit and at rest, dispersed across multiple geographic locations, and accessed over HTTP by using a REST API.
{: shortdesc}

If you installed the {{site.data.keyword.cos_full_notm}} plug-in with Helm version 2, [migrate to Helm version 3](/docs/openshift?topic=openshift-helm#migrate_v3).
{: important}

With version 1.0.5, the {{site.data.keyword.cos_full_notm}} plug-in is renamed from `ibmcloud-object-storage-plugin` to `ibm-object-storage-plugin`. To install the new version of the plug-in, you must [uninstall the old Helm chart installation](#remove_cos_plugin) and [reinstall the Helm chart with the new {{site.data.keyword.cos_full_notm}} plug-in version](#install_cos).
{: note}

With version 1.0.8, the {{site.data.keyword.cos_full_notm}} plug-in Helm chart is now available in the `ibm-charts` Helm repository. Make sure to fetch the latest version of the Helm chart from this repository. To add the repository, run `helm repo add ibm-charts https://private.icr.io/helm/ibm-charts`.
{: note}

With version 2.0.0, the {{site.data.keyword.cos_full_notm}} Helm chart is now available in the `ibm-helm` repository. To add the repository, run `helm repo add ibm-helm https://raw.githubusercontent.com/IBM/charts/master/repo/ibm-helm`.
{: note}

<br />


## Creating your object storage service instance
{: #create_cos_service}

Before you can start using object storage in your cluster, you must provision an {{site.data.keyword.cos_full_notm}} service instance in your account.
{: shortdesc}

The {{site.data.keyword.cos_full_notm}} plug-in is configured to work with any s3 API endpoint. For example, you might want to use a local Cloud Object Storage server, such as [Minio](https://cloud.ibm.com/kubernetes/helm/ibm-charts/ibm-minio-objectstore), or connect to an s3 API endpoint that you set up at a different cloud provider instead of using an {{site.data.keyword.cos_full_notm}} service instance.

Follow these steps to create an {{site.data.keyword.cos_full_notm}} service instance. If you plan to use a local Cloud Object Storage server or a different s3 API endpoint, refer to the provider documentation to set up your Cloud Object Storage instance.

1. Deploy an {{site.data.keyword.cos_full_notm}} service instance.
  1.  Open the [{{site.data.keyword.cos_full_notm}} catalog page](https://cloud.ibm.com/catalog/services/cloud-object-storage).
  2.  Enter a name for your service instance, such as `cos-backup`, and select the same resource group that your cluster is in. To view the resource group of your cluster, run `ibmcloud oc cluster get --cluster <cluster_name_or_ID>`.   
  3.  Review the [plan options](https://www.ibm.com/cloud/object-storage/pricing/#s3api){: external} for pricing information and select a plan.
  4.  Click **Create**. The service details page opens.
2. {: #service_credentials}Retrieve the {{site.data.keyword.cos_full_notm}} service credentials.
  1.  In the navigation on the service details page, click **Service Credentials**.
  2.  Click **New credential**. A dialog box displays.
  3.  Enter a name for your credentials.
  4.  From the **Role** drop-down, select `Writer` or `Manager`. When you select `Reader`, then you cannot use the credentials to create buckets in {{site.data.keyword.cos_full_notm}} and write data to it.
  5.  Optional: In **Add Inline Configuration Parameters (Optional)**, enter `{"HMAC":true}` to create additional HMAC credentials for the {{site.data.keyword.cos_full_notm}} service. HMAC authentication adds an extra layer of security to the OAuth2 authentication by preventing the misuse of expired or randomly created OAuth2 tokens.
  6.  Click **Add**. Your new credentials are listed in the **Service Credentials** table.
  7.  Click **View credentials**.
  8.  Make note of the **apikey** to use OAuth2 tokens to authenticate with the {{site.data.keyword.cos_full_notm}} service. For HMAC authentication, in the **cos_hmac_keys** section, note the **access_key_id** and the **secret_access_key**.
3. [Store your service credentials in a Kubernetes secret inside the cluster](#create_cos_secret) to enable access to your {{site.data.keyword.cos_full_notm}} service instance.

<br />


## Creating a secret for the object storage service credentials
{: #create_cos_secret}

To access your {{site.data.keyword.cos_full_notm}} service instance to read and write data, you must securely store the service credentials in a Kubernetes secret. The {{site.data.keyword.cos_full_notm}} plug-in uses these credentials for every read or write operation to your bucket.
{: shortdesc}

Follow these steps to create a Kubernetes secret for the credentials of an {{site.data.keyword.cos_full_notm}} service instance. If you plan to use a local Cloud Object Storage server or a different s3 API endpoint, create a Kubernetes secret with the appropriate credentials.

Before you begin: [Access your {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-access_cluster).

1. Retrieve the **apikey**, or the **access_key_id** and the **secret_access_key** of your [{{site.data.keyword.cos_full_notm}} service credentials](#service_credentials).

2. Get the **GUID** of your {{site.data.keyword.cos_full_notm}} service instance.
   ```
   ibmcloud resource service-instance <service_name> | grep GUID
   ```
   {: pre}

3. Create a Kubernetes secret to store your service credentials. When you create your secret, all values are automatically encoded to base64. In the following example the secret name is `cos-write-access`.

   **Example for using the API key:**
   ```
   oc create secret generic cos-write-access --type=ibm/ibmc-s3fs --from-literal=api-key=<api_key> --from-literal=service-instance-id=<service_instance_guid>
   ```
   {: pre}

   **Example for HMAC authentication:**
   ```
   oc create secret generic cos-write-access --type=ibm/ibmc-s3fs --from-literal=access-key=<access_key_ID> --from-literal=secret-key=<secret_access_key>    
   ```
   {: pre}

   <table>
   <caption>Understanding the command components</caption>
   <thead>
      <th>Component</th>
      <th>Description</th>
    </thead>
   <tbody>
   <tr>
   <td><code>api-key</code></td>
   <td>Enter the API key that you retrieved from your {{site.data.keyword.cos_full_notm}} service credentials earlier. If you want to use HMAC authentication, specify the <code>access-key</code> and <code>secret-key</code> instead.  </td>
   </tr>
   <tr>
   <td><code>access-key</code></td>
   <td>Enter the access key ID that you retrieved from your {{site.data.keyword.cos_full_notm}} service credentials earlier. If you want to use OAuth2 authentication, specify the <code>api-key</code> instead.  </td>
   </tr>
   <tr>
   <td><code>secret-key</code></td>
   <td>Enter the secret access key that you retrieved from your {{site.data.keyword.cos_full_notm}} service credentials earlier. If you want to use OAuth2 authentication, specify the <code>api-key</code> instead.</td>
   </tr>
   <tr>
   <td><code>service-instance-id</code></td>
   <td>Enter the GUID of your {{site.data.keyword.cos_full_notm}} service instance that you retrieved earlier. </td>
   </tr>
   </tbody>
   </table>

4. Verify that the secret is created in your namespace.
    ```
    oc get secret
    ```
    {: pre}

    Example output:
    ```
    NAME                  TYPE                                  DATA   AGE
    cos-write-access      ibm/ibmc-s3fs                         2      7d19h
    default-au-icr-io     kubernetes.io/dockerconfigjson        1      55d
    default-de-icr-io     kubernetes.io/dockerconfigjson        1      55d
    ...
    ```
    {: screen}

5. [Install the {{site.data.keyword.cos_full_notm}} plug-in](#install_cos), or if you already installed the plug-in, [decide on the configuration]( #configure_cos) for your {{site.data.keyword.cos_full_notm}} bucket.

<br />



## Installing the IBM Cloud Object Storage plug-in
{: #install_cos}

Install the {{site.data.keyword.cos_full_notm}} plug-in with a Helm chart to set up pre-defined storage classes for {{site.data.keyword.cos_full_notm}}. You can use these storage classes to create a PVC to provision {{site.data.keyword.cos_full_notm}} for your apps.
{: shortdesc}

If you are using Helm version 2, [migrate to Helm version 3](/docs/openshift?topic=openshift-helm#migrate_v3) before installing the {{site.data.keyword.cos_full_notm}} plug-in.
{: important}

Looking for instructions for how to update or remove the {{site.data.keyword.cos_full_notm}} plug-in? See [Updating the plug-in](#update_cos_plugin) and [Removing the plug-in](#remove_cos_plugin).
{: tip}

Before you begin: [Access your {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-access_cluster).

To install the `ibmc` Helm plug-in and the `ibm-object-storage-plugin`:

1. Make sure that your worker node applies the latest patch for your minor version to run your worker node with the latest security settings. The patch version also ensures that the root password on the worker node is renewed. 
   
   If you did not apply updates or reload your worker node within the last 90 days, your root password on the worker node expires and the installation of the storage plug-in might fail. 
   {: note}
   1. List the current patch version of your worker nodes.
      ```
      ibmcloud oc worker ls --cluster <cluster_name_or_ID>
      ```
      {: pre}

      Example output:
      ```
      OK
      ID                                                  Public IP        Private IP     Machine Type           State    Status   Zone    Version
      kube-dal10-crb1a23b456789ac1b20b2nc1e12b345ab-w26   169.xx.xxx.xxx    10.xxx.xx.xxx   b3c.4x16.encrypted     normal   Ready    dal10   1.17.11_1523*
      ```
      {: screen}

      If your worker node does not apply the latest patch version, you see an asterisk (`*`) in the **Version** column of your CLI output.

   2. Review the [version changelog](/docs/containers?topic=containers-changelog) to find the changes that are included in the latest patch version.

   3. Apply the latest patch version by reloading your worker node. Follow the instructions in the [ibmcloud oc worker reload command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_reload) to gracefully reschedule any running pods on your worker node before you reload your worker node. Note that during the reload, your worker node machine is updated with the latest image and data is deleted if not [stored outside the worker node](/docs/openshift?topic=openshift-storage_planning#persistent_storage_overview).

2. [Follow the instructions](/docs/openshift?topic=openshift-openshift_apps#roks_helm) to install the version 3 Helm client on your local machine.

  If you enabled [VRF](/docs/dl?topic=dl-overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud) and [service endpoints](/docs/account?topic=account-vrf-service-endpoint#service-endpoint) in your {{site.data.keyword.cloud_notm}} account, you can use the private {{site.data.keyword.cloud_notm}} Helm repository to keep your image pull traffic on the private network. If you cannot enable VRF or service endpoints in your account, use the public Helm repository.
  {: note}

3. Add the {{site.data.keyword.cloud_notm}} Helm repo to your cluster.

  ```
  helm repo add ibm-helm https://raw.githubusercontent.com/IBM/charts/master/repo/ibm-helm
  ```
  {: pre}

4. Update the Helm repo to retrieve the latest version of all Helm charts in this repo.
  ```
  helm repo update
  ```
  {: pre}

5. If you previously installed the {{site.data.keyword.cos_full_notm}} Helm plug-in, remove the `ibmc` plug-in.
  ```
  helm plugin uninstall ibmc
  ```
  {: pre}

6. Download the Helm charts and unpack the charts in your current directory.

  ```
  helm fetch --untar ibm-helm/ibm-object-storage-plugin && cd ibm-object-storage-plugin
  ```
  {: pre}

  If the output shows `Error: failed to untar: a file or directory with the name ibm-object-storage-plugin already exists`, delete your `ibm-object-storage-plugin` directory and rerun the `helm fetch` command.
  {: tip}

7. If you use OS X or a Linux distribution, install the {{site.data.keyword.cos_full_notm}} Helm plug-in `ibmc`. The plug-in is used to automatically retrieve your cluster location and to set the API endpoint for your {{site.data.keyword.cos_full_notm}} buckets in your storage classes. If you use Windows as your operating system, continue with the next step.
  1. Install the Helm plug-in.
    ```
    helm plugin install ./helm-ibmc
    ```
    {: pre}

  2. Verify that the `ibmc` plug-in is installed successfully.
    ```
    helm ibmc --help
    ```
    {: pre}

    If the output shows the error `Error: fork/exec /home/iksadmin/.helm/plugins/helm-ibmc/ibmc.sh: permission denied`, run `chmod 755 /Users/<user_name>/Library/helm/plugins/helm-ibmc/ibmc.sh`. Then, rerun `helm ibmc --help`.
    {: tip}

    Example output:
    ```
    Helm version: v3.2.4+g0ad800e
    Install or upgrade Helm charts in IBM K8S Service(IKS) and IBM Cloud Private(ICP)
    Usage:
      helm ibmc [command]
    Available Commands:
      install           Install a Helm chart
      upgrade           Upgrade the release to a new version of the Helm chart
    Available Flags:
      -h, --help        (Optional) This text.
      -u, --update      (Optional) Update this plugin to the latest version
    Example Usage:
        Install: helm ibmc install ibm-object-storage-plugin ibm-helm/ibm-object-storage-plugin
        Upgrade: helm ibmc upgrade [RELEASE] ibm-helm/ibm-object-storage-plugin
    Note:
        1. It is always recommended to install latest version of ibm-object-storage-plugin chart.
        2. It is always recommended to have 'kubectl' client up-to-date.
    ```
    {: screen}

8. Optional: Limit the {{site.data.keyword.cos_full_notm}} plug-in to access only the Kubernetes secrets that hold your {{site.data.keyword.cos_full_notm}} service credentials. By default, the plug-in is authorized to access all Kubernetes secrets in your cluster.
   1. [Create your {{site.data.keyword.cos_full_notm}} service instance](#create_cos_service).
   2. [Store your {{site.data.keyword.cos_full_notm}} service credentials in a Kubernetes secret](#create_cos_secret).
   3. From the `ibm-object-storage-plugin`, navigate to the `templates` directory and list available files.  
      ```
      cd templates && ls
      ```
      {: pre}

   4. Open the `provisioner-sa.yaml` file and look for the `ibmcloud-object-storage-secret-reader` `ClusterRole` definition.
   5. Add the name of the secret that you created earlier to the list of secrets that the plug-in is authorized to access in the `resourceNames` section.
      ```yaml
      kind: ClusterRole
      apiVersion: rbac.authorization.k8s.io/v1beta1
      metadata:
        name: ibmcloud-object-storage-secret-reader
      rules:
      - apiGroups: [""]
        resources: ["secrets"]
        resourceNames: ["<secret_name1>","<secret_name2>"]
        verbs: ["get"]
      ```
      {: codeblock}
   6. Save your changes.

9. Install the `ibm-object-storage-plugin` in your cluster. When you install the plug-in, pre-defined storage classes are added to your cluster.

  - **For OS X and Linux:**
    - If you skipped the previous step, install without a limitation to specific Kubernetes secrets.</br>
      ```
      helm ibmc install ibm-object-storage-plugin ibm-helm/ibm-object-storage-plugin --set license=true
      ```
      {: pre}

    - If you completed the previous step, install with a limitation to specific Kubernetes secrets. If you are still targeting the `templates` directory, change directories.</br>
      ```
      cd ../..
      helm ibmc install ibm-object-storage-plugin ./ibm-object-storage-plugin --set license=true
      ```
      {: pre}

  - **For Windows:**
    1. Retrieve the `datacenter` where your cluster is deployed and store it in an environment variable.

      a. Retrieve the `datacenter`.
        ```
        oc get cm cluster-info -n kube-system -o jsonpath="{.data.cluster-config\.json}{'\n'}"
        ```
        {: pre}

      b. Store the `datacenter` in an environment variable.
        ```
        SET DC_NAME=<datacenter>
        ```
        {: pre}

        Example:
        ```
        SET DC_NAME=dal13
        ```
        {: pre}

      c. Optional: Set the environment variable in Windows PowerShell.
        ```
        $env:DC_NAME="<datacenter>"
        ```
        {: codeblock}

    2. Retrieve the infrastructure provider that your cluster uses and store it in an environment variable.

      a. Retrieve the infrastructure provider.
        ```
        oc get nodes -o jsonpath="{.items[*].metadata.labels.ibm-cloud\.kubernetes\.io\/iaas-provider}{'\n'}"
        ```
        {: pre}

      b. Store the infrastructure provider in an environment variable. If the output from the previous step contains `softlayer`, then set the `CLUSTER_PROVIDER` to `"IBMC"`. If the output contains `gc`, `ng`, or `g2`, then set the `CLUSTER_PROVIDER` to `"IBM-VPC"`.
        ```
        SET CLUSTER_PROVIDER="IBMC"
        ```
        {: pre}

        ```
        SET CLUSTER_PROVIDER="IBM-VPC"
        ```
        {: pre}

    3. Retrieve the operating system of the worker nodes and store it in an environment variable.

      a. Retrieve the operating system of the worker nodes.
        ```
        oc get nodes -o jsonpath="{.items[*].metadata.labels.ibm-cloud\.kubernetes\.io\/os}{'\n'}"
        ```
        {: pre}

      b. Store the operating system of the worker nodes in an environment variable.

        * If the output from the previous step contains `REDHAT`, then set the `WORKER_OS` to `"redhat"` and set the `PLATFORM` to `"openshift"`.

            ```
            SET WORKER_OS="redhat"
            SET PLATFORM="openshift"
            ```
            {: pre}

        * If the output from the previous contains `UBUNTU`, then set the `WORKER_OS` to `"debian"` and set the `PLATFORM` to `"k8s"`.

            ```
            SET WORKER_OS="debian"
            SET PLATFORM="k8s"
            ```
            {: pre}

    4. Install the plug-in.       
      - Install without a limitation to specific Kubernetes secrets.</br>
        ```
        helm install ibm-object-storage-plugin ibm-helm/ibm-object-storage-plugin --set dcname="${DC_NAME}" --set provider="${CLUSTER_PROVIDER}" --set workerOS="${WORKER_OS}" --set platform="${PLATFORM}" --set license=true
        ```
        {: pre}

      - Install the plug-in with a limitation to specific Kubernetes secrets.</br>
        ```
        cd ../..
        helm install ibm-object-storage-plugin ./ibm-object-storage-plugin --set dcname="${DC_NAME}" --set provider="${CLUSTER_PROVIDER}" --set workerOS="${WORKER_OS}" --set platform="${PLATFORM}" --set license=true
        ```
        {: pre}

10. Verify that the plug-in is installed correctly.
    ```
    oc get pod --all-namespaces -o wide | grep object
    ```
    {: pre}

    Example output:
    ```
    ibmcloud-object-storage-driver-9n8g8                              1/1       Running   0          2m
    ibmcloud-object-storage-plugin-7c774d484b-pcnnx                   1/1       Running   0          2m
    ```
    {: screen}

    The installation is successful when you see one `ibmcloud-object-storage-plugin` pod and one or more `ibmcloud-object-storage-driver` pods. The number of `ibmcloud-object-storage-driver` pods equals the number of worker nodes in your cluster. All pods must be in a `Running` state for the plug-in to function properly. If the pods fail, run `oc describe pod -n kube-system <pod_name>` to find the root cause for the failure.

11. Verify that the storage classes are created successfully.
    ```
    oc get storageclass | grep s3
    ```
    {: pre}

    Example output:
    ```
    ibmc-s3fs-cold-cross-region            ibm.io/ibmc-s3fs   8m
    ibmc-s3fs-cold-regional                ibm.io/ibmc-s3fs   8m
    ibmc-s3fs-flex-cross-region            ibm.io/ibmc-s3fs   8m
    ibmc-s3fs-flex-perf-cross-region       ibm.io/ibmc-s3fs   8m
    ibmc-s3fs-flex-perf-regional           ibm.io/ibmc-s3fs   8m
    ibmc-s3fs-flex-regional                ibm.io/ibmc-s3fs   8m
    ibmc-s3fs-standard-cross-region        ibm.io/ibmc-s3fs   8m
    ibmc-s3fs-standard-perf-cross-region   ibm.io/ibmc-s3fs   8m
    ibmc-s3fs-standard-perf-regional       ibm.io/ibmc-s3fs   8m
    ibmc-s3fs-standard-regional            ibm.io/ibmc-s3fs   8m
    ibmc-s3fs-vault-cross-region           ibm.io/ibmc-s3fs   8m
    ibmc-s3fs-vault-regional               ibm.io/ibmc-s3fs   8m
    ```
    {: screen}

    If you want to set one of the {{site.data.keyword.cos_full_notm}} storage classes as your default storage class, run `oc patch storageclass <storageclass> -p '{"metadata": {"annotations":{"storageclass.kubernetes.io/is-default-class":"true"}}}'`. Replace `<storageclass>` with the name of the {{site.data.keyword.cos_full_notm}} storage class.
    {: tip}

12. Follow the instructions to [add object storage to your apps](#add_cos).

If you're having trouble installing the {{site.data.keyword.cos_full_notm}} plug-in, see [Object storage: Installing the Object storage `ibmc` Helm plug-in fails](/docs/openshift?topic=openshift-cs_troubleshoot_storage#cos_helm_fails) and [Object storage: Installing the Object storage plug-in fails](/docs/openshift?topic=openshift-cs_troubleshoot_storage#cos_plugin_fails).
{: tip}

### Updating the IBM Cloud Object Storage plug-in
{: #update_cos_plugin}

You can upgrade the existing {{site.data.keyword.cos_full_notm}} plug-in to the latest version.
{: shortdesc}

1. If you previously installed version 1.0.4 or earlier of the Helm chart that is named `ibmcloud-object-storage-plugin`, remove this Helm installation from your cluster. Then, reinstall the Helm chart.
  1. Check whether the old version of the {{site.data.keyword.cos_full_notm}} Helm chart is installed in your cluster.  
    ```
    helm ls -A | grep ibm-object-storage-plugin
    ```
    {: pre}

    Example output:
    ```
    NAME        	  NAMESPACE  	REVISION	UPDATED                             	  STATUS  	CHART                              	APP VERSION	           
    <release_name>  <namespace> 	1       	2020-02-13 16:05:58.599679 -0500 EST	deployed	ibm-object-storage-plugin-1.1.2    	1.1.2
    ```
    {: screen}

  2. If you have version 1.0.4 or earlier of the Helm chart that is named `ibmcloud-object-storage-plugin`, remove the Helm chart from your cluster. If you have version 1.0.5 or later of the Helm chart that is named `ibm-object-storage-plugin`, continue with Step 2.
    ```
    helm uninstall ibmcloud-object-storage-plugin -n <namespace>
    ```
    {: pre}

  3. Follow the steps in [Installing the {{site.data.keyword.cos_full_notm}} plug-in](#install_cos) to install the latest version of the {{site.data.keyword.cos_full_notm}} plug-in.

2. Update the {{site.data.keyword.cloud_notm}} Helm repo to retrieve the latest version of all Helm charts in this repo.
  ```
  helm repo update
  ```
  {: pre}

3. If you use OS X or a Linux distribution, update the {{site.data.keyword.cos_full_notm}} `ibmc` Helm plug-in to the latest version.
  ```
  helm ibmc --update
  ```
  {: pre}

4. Download the latest {{site.data.keyword.cos_full_notm}} Helm chart to your local machine and extract the package to review the `release.md` file to find the latest release information.
  ```
  helm pull --untar ibm-helm/ibm-object-storage-plugin
  ```
  {: pre}

5. Install the latest version of the plug-in. </br>
  ```
  helm ibmc upgrade <release_name> ibm-helm/ibm-object-storage-plugin --force --set license=true
  ```
  {: pre}

6. Verify that the `ibmcloud-object-storage-plugin` is successfully upgraded.  
  ```
  oc rollout status deployment/ibmcloud-object-storage-plugin -n kube-system
  ```
  {: pre}

   The upgrade of the plug-in is successful when you see `deployment "ibmcloud-object-storage-plugin" successfully rolled out` in your CLI output.

7. Verify that the `ibmcloud-object-storage-driver` is successfully upgraded.
  ```
  oc rollout status ds/ibmcloud-object-storage-driver -n kube-system
  ```
  {: pre}

   The upgrade is successful when you see `daemon set "ibmcloud-object-storage-driver" successfully rolled out` in your CLI output.

8. Verify that the {{site.data.keyword.cos_full_notm}} pods are in a `Running` state.
   ```
   oc get pods -n <namespace> -o wide | grep object-storage
   ```
   {: pre}

If you're having trouble updating the {{site.data.keyword.cos_full_notm}} plug-in, see [Object storage: Installing the Object storage `ibmc` Helm plug-in fails](/docs/openshift?topic=openshift-cs_troubleshoot_storage#cos_helm_fails) and [Object storage: Installing the Object storage plug-in fails](/docs/openshift?topic=openshift-cs_troubleshoot_storage#cos_plugin_fails).
{: tip}

### Removing the IBM Cloud Object Storage plug-in
{: #remove_cos_plugin}

If you do not want to provision and use {{site.data.keyword.cos_full_notm}} in your cluster, you can uninstall the `ibm-object-storage-plugin` and the `ibmc` Helm plugin.
{: shortdesc}

Removing the `ibmc` Helm plug-in or the `ibm-object-storage-plugin` does not remove existing PVCs, PVs, data. When you remove the `ibm-object-storage-plugin`, all the related pods and daemon sets are removed from your cluster. You cannot provision new {{site.data.keyword.cos_full_notm}} for your cluster or use existing PVCs and PVs after you remove the plug-in, unless you configure your app to use the {{site.data.keyword.cos_full_notm}} API directly.
{: important}

Before you begin:

- [Access your {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-access_cluster).
- Make sure that you do not have any PVCs or PVs in your cluster that use {{site.data.keyword.cos_full_notm}}. To list all pods that mount a specific PVC, run `oc get pods --all-namespaces -o=jsonpath='{range .items[*]}{"\n"}{.metadata.name}{":\t"}{range .spec.volumes[*]}{.persistentVolumeClaim.claimName}{" "}{end}{end}' | grep "<pvc_name>"`.

To remove the `ibmc` Helm plugin and the `ibm-object-storage-plugin`:

1. Get the name of your `ibm-object-storage-plugin` Helm installation.
  ```
  helm ls -A | grep ibm-object-storage-plugin
  ```
  {: pre}

  Example output
  ```
  NAME                     	NAMESPACE	REVISION	UPDATED                             	STATUS  	CHART                              	APP VERSION	           
  ibm-object-storage-plugin	default  	2       	2020-04-01 08:46:01.403477 -0400 EDT	deployed	ibm-object-storage-plugin-1.1.4    	1.1.4  
  ```
  {: screen}

2. Uninstall the `ibm-object-storage-plugin`.
  ```
  helm uninstall <release_name>
  ```
  {: pre}

  Example command for a release named `ibm-object-storage-plugin`:
  ```
  helm uninstall ibm-object-storage-plugin
  ```
  {: pre}

3. Verify that the `ibm-object-storage-plugin` pods are removed.
  ```
  oc get pod -n <namespace> | grep object-storage
  ```
  {: pre}

  The removal of the pods is successful if no pods are displayed in your CLI output.

4. Verify that the storage classes are removed.
  ```
  oc get storageclasses | grep s3
  ```
  {: pre}

  The removal of the storage classes is successful if no storage classes are displayed in your CLI output.

5. If you use OS X or a Linux distribution, remove the `ibmc` Helm plug-in. If you use Windows, this step is not required.

  1. Remove the `ibmc` Helm plug-in.
    ```
    helm plugin uninstall ibmc
    ```
    {: pre}

  2. Verify that the `ibmc` plug-in is removed.
    ```
    helm plugin list
    ```
    {: pre}

    Example output:
    ```
    NAME	VERSION	DESCRIPTION
    ```
    {: screen}

    The `ibmc` plug-in is removed successfully if the `ibmc` plug-in is not listed in your CLI output.

    <br />



## Deciding on the object storage configuration
{: #configure_cos}

{{site.data.keyword.openshiftlong_notm}} provides pre-defined storage classes that you can use to create buckets with a specific configuration.
{: shortdesc}

1. List available storage classes in {{site.data.keyword.openshiftlong_notm}}.
   ```
   oc get storageclasses | grep s3
   ```
   {: pre}

   Example output:
   ```
   ibmc-s3fs-cold-cross-region            ibm.io/ibmc-s3fs   8m
   ibmc-s3fs-cold-regional                ibm.io/ibmc-s3fs   8m
   ibmc-s3fs-flex-cross-region            ibm.io/ibmc-s3fs   8m
   ibmc-s3fs-flex-perf-cross-region       ibm.io/ibmc-s3fs   8m
   ibmc-s3fs-flex-perf-regional           ibm.io/ibmc-s3fs   8m
   ibmc-s3fs-flex-regional                ibm.io/ibmc-s3fs   8m
   ibmc-s3fs-standard-cross-region        ibm.io/ibmc-s3fs   8m
   ibmc-s3fs-standard-perf-cross-region   ibm.io/ibmc-s3fs   8m
   ibmc-s3fs-standard-perf-regional       ibm.io/ibmc-s3fs   8m
   ibmc-s3fs-standard-regional            ibm.io/ibmc-s3fs   8m
   ibmc-s3fs-vault-cross-region           ibm.io/ibmc-s3fs   8m
   ibmc-s3fs-vault-regional               ibm.io/ibmc-s3fs   8m
   ```
   {: screen}

2. Choose a storage class that fits your data access requirements. The storage class determines the [pricing](https://www.ibm.com/cloud/object-storage/pricing/#s3api){: external} for storage capacity, read and write operations, and outbound bandwidth for a bucket. The option that is right for you is based on how frequently data is read and written to your service instance.
   - **Standard**: This option is used for hot data that is accessed frequently. Common use cases are web or mobile apps.
   - **Vault**: This option is used for workloads or cool data that are accessed infrequently, such as once a month or less. Common use cases are archives, short-term data retention, digital asset preservation, tape replacement, and disaster recovery.
   - **Cold**: This option is used for cold data that is rarely accessed (every 90 days or less), or inactive data. Common use cases are archives, long-term backups, historical data that you keep for compliance, or workloads and apps that are rarely accessed.
   - **Flex**: This option is used for workloads and data that do not follow a specific usage pattern, or that are too huge to determine or predict a usage pattern. **Tip:** Check out this [blog](https://www.ibm.com/blogs/cloud-archive/2017/03/interconnect-2017-changing-rules-storage/){: external} to learn how the Flex storage class works compared to traditional storage tiers.   

3. Decide on the level of resiliency for the data that is stored in your bucket.
   - **Cross-region**: With this option, your data is stored across three regions within a geolocation for highest availability. If you have workloads that are distributed across regions, requests are routed to the nearest regional endpoint. The API endpoint for the geolocation is automatically set by the `ibmc` Helm plug-in that you installed earlier based on the location that your cluster is in. For example, if your cluster is in `US South`, then your storage classes are configured to use the `US GEO` API endpoint for your buckets. For more information, see [Regions and endpoints](/docs/cloud-object-storage/basics?topic=cloud-object-storage-endpoints#endpoints).  
   - **Regional**: With this option, your data is replicated across multiple zones within one region. If you have workloads that are located in the same region, you see lower latency and better performance than in a cross-regional setup. The regional endpoint is automatically set by the `ibm` Helm plug-in that you installed earlier based on the location that your cluster is in. For example, if your cluster is in `US South`, then your storage classes were configured to use `US South` as the regional endpoint for your buckets. For more information, see [Regions and endpoints](/docs/cloud-object-storage/basics?topic=cloud-object-storage-endpoints#endpoints).

4. Review the detailed {{site.data.keyword.cos_full_notm}} bucket configuration for a storage class.
   ```
   oc describe storageclass <storageclass_name>
   ```
   {: pre}

   Example output:
   ```
   Name:                  ibmc-s3fs-standard-cross-region
   IsDefaultClass:        No
   Annotations:           <none>
   Provisioner:           ibm.io/ibmc-s3fs
   Parameters:            ibm.io/chunk-size-mb=16,ibm.io/curl-debug=false,ibm.io/debug-level=warn,ibm.io/iam-endpoint=https://iam.bluemix.net,ibm.io/kernel-cache=true,ibm.io/multireq-max=20,ibm.io/object-store-endpoint=https://s3-api.dal-us-geo.objectstorage.service.networklayer.com,ibm.io/object-store-storage-class=us-standard,ibm.io/parallel-count=2,ibm.io/s3fs-fuse-retry-count=5,ibm.io/stat-cache-size=100000,ibm.io/tls-cipher-suite=AESGCM
   AllowVolumeExpansion:  <unset>
   MountOptions:          <none>
   ReclaimPolicy:         Delete
   VolumeBindingMode:     Immediate
   Events:                <none>
   ```
   {: screen}

   <table>
   <caption>Understanding the storage class details</caption>
   <thead>
    <th>Component</th>
    <th>Description</th>
   </thead>
   <tbody>
   <tr>
   <td><code>ibm.io/chunk-size-mb</code></td>
   <td>The size of a data chunk that is read from or written to {{site.data.keyword.cos_full_notm}} in megabytes. Storage classes with <code>perf</code> in their name are set up with 52 megabytes. Storage classes without <code>perf</code> in their name use 16 megabyte chunks. For example, if you want to read a file that is `1GB`, the plug-in reads this file in multiple 16 or 52-megabyte chunks. </td>
   </tr>
   <tr>
   <td><code>ibm.io/curl-debug</code></td>
   <td>Enable the logging of requests that are sent to the {{site.data.keyword.cos_full_notm}} service instance. If enabled, logs are sent to `syslog` and you can [forward the logs to an external logging server](/docs/containers?topic=containers-health#logging). By default, all storage classes are set to <strong>false</strong> to disable this logging feature. </td>
   </tr>
   <tr>
   <td><code>ibm.io/debug-level</code></td>
   <td>The logging level that is set by the {{site.data.keyword.cos_full_notm}} plug-in. All storage classes are set up with the <strong>WARN</strong> logging level. </td>
   </tr>
   <tr>
   <td><code>ibm.io/iam-endpoint</code></td>
   <td>The API endpoint for {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM). </td>
   </tr>
   <tr>
   <td><code>ibm.io/kernel-cache</code></td>
   <td>Enable or disable the kernel buffer cache for the volume mount point. If enabled, data that is read from {{site.data.keyword.cos_full_notm}} is stored in the kernel cache to ensure fast read access to your data. If disabled, data is not cached and always read from {{site.data.keyword.cos_full_notm}}. Kernel cache is enabled for <code>standard</code> and <code>flex</code> storage classes, and disabled for <code>cold</code> and <code>vault</code> storage classes. </td>
   </tr>
   <tr>
   <td><code>ibm.io/multireq-max</code></td>
   <td>The maximum number of parallel requests that can be sent to the {{site.data.keyword.cos_full_notm}} service instance to list files in a single directory. All storage classes are set up with a maximum of 20 parallel requests.  </td>
   </tr>
   <tr>
   <td><code>ibm.io/object-store-endpoint</code></td>
   <td>The API endpoint to use to access the bucket in your {{site.data.keyword.cos_full_notm}} service instance. The endpoint is automatically set based on the region of your cluster. **Note**: If you want to access an existing bucket that is located in a different region than the one where your cluster is in, you must create a [custom storage class](/docs/openshift?topic=openshift-kube_concepts#customized_storageclass) and use the API endpoint for your bucket.</td>
   </tr>
   <tr>
   <td><code>ibm.io/object-store-storage-class</code></td>
   <td>The name of the storage class. </td>
   </tr>
   <tr>
   <td><code>ibm.io/parallel-count</code></td>
   <td>The maximum number of parallel requests that can be sent to the {{site.data.keyword.cos_full_notm}} service instance for a single read or write operation. Storage classes with <code>perf</code> in their name are set up with a maximum of 20 parallel requests. Storage classes without <code>perf</code> are set up with two parallel requests by default.  </td>
   </tr>
   <tr>
   <td><code>ibm.io/s3fs-fuse-retry-count</code></td>
   <td>The maximum number of retries for a read or write operation before the operation is considered unsuccessful. All storage classes are set up with a maximum of five retries.  </td>
   </tr>
   <tr>
   <td><code>ibm.io/stat-cache-size</code></td>
   <td>The maximum number of records that are kept in the {{site.data.keyword.cos_full_notm}} metadata cache. Every record can take up to 0.5 kilobytes. All storage classes set the maximum number of records to 100000 by default. </td>
   </tr>
   <tr>
   <td><code>ibm.io/tls-cipher-suite</code></td>
   <td>The TLS cipher suite that must be used when a connection to {{site.data.keyword.cos_full_notm}} is established via the HTTPS endpoint. The value for the cipher suite must follow the [OpenSSL format ![External link icon](../icons/launch-glyph.svg "External link icon")](https://www.openssl.org/docs/man1.0.2/man1/ciphers.html). If your worker nodes run an Ubuntu operating system, your storage classes are set up to use the <strong><code>AESGCM</code></strong> cipher suite by default. For worker nodes that run a Red Hat operating system, the <strong><code>ecdhe_rsa_aes_128_gcm_sha_256</code></strong> cipher suite is used by default.    </td>
   </tr>
   </tbody>
   </table>

   For more information about each storage class, see the [storage class reference](#cos_storageclass_reference). If you want to change any of the pre-set values, create your own [customized storage class](/docs/openshift?topic=openshift-kube_concepts#customized_storageclass).
   {: tip}

5. Decide on a name for your bucket. The name of a bucket must be unique in {{site.data.keyword.cos_full_notm}}. You can also choose to automatically create a name for your bucket by the {{site.data.keyword.cos_full_notm}} plug-in. To organize data in a bucket, you can create subdirectories.

   The storage class that you chose earlier determines the pricing for the entire bucket. You cannot define different storage classes for subdirectories. If you want to store data with different access requirements, consider creating multiple buckets by using multiple PVCs.
   {: note}

6. Choose if you want to keep your data and the bucket after the cluster or the persistent volume claim (PVC) is deleted. When you delete the PVC, the PV is always deleted. You can choose if you want to also automatically delete the data and the bucket when you delete the PVC. Your {{site.data.keyword.cos_full_notm}} service instance is independent from the retention policy that you select for your data and is never removed when you delete a PVC.

Now that you decided on the configuration that you want, you are ready to [create a PVC](#add_cos) to provision {{site.data.keyword.cos_full_notm}}.

<br />


## Adding object storage to apps
{: #add_cos}

Create a persistent volume claim (PVC) to provision {{site.data.keyword.cos_full_notm}} for your cluster.
{: shortdesc}

Depending on the settings that you choose in your PVC, you can provision {{site.data.keyword.cos_full_notm}} in the following ways:
- [Dynamic provisioning](/docs/openshift?topic=openshift-kube_concepts#dynamic_provisioning): When you create the PVC, the matching persistent volume (PV) and the bucket in your {{site.data.keyword.cos_full_notm}} service instance are automatically created.
- [Static provisioning](/docs/openshift?topic=openshift-kube_concepts#static_provisioning): You can reference an existing bucket in your {{site.data.keyword.cos_full_notm}} service instance in your PVC. When you create the PVC, only the matching PV is automatically created and linked to your existing bucket in {{site.data.keyword.cos_full_notm}}.

Before you begin:
- [Create and prepare your {{site.data.keyword.cos_full_notm}} service instance](#create_cos_service).
- [Create a secret to store your {{site.data.keyword.cos_full_notm}} service credentials](#create_cos_secret).
- [Decide on the configuration for your {{site.data.keyword.cos_full_notm}}](#configure_cos).

To add {{site.data.keyword.cos_full_notm}} to your cluster:

1. Create a configuration file to define your persistent volume claim (PVC).
   ```yaml
   kind: PersistentVolumeClaim
   apiVersion: v1
   metadata:
     name: <pvc_name>
     namespace: <namespace>
     annotations:
       ibm.io/auto-create-bucket: "<true_or_false>"
       ibm.io/auto-delete-bucket: "<true_or_false>"
       ibm.io/bucket: "<bucket_name>"
       ibm.io/object-path: "<bucket_subdirectory>"
       ibm.io/secret-name: "<secret_name>"
       ibm.io/endpoint: "https://<s3fs_service_endpoint>"
   spec:
     accessModes:
       - ReadWriteOnce
     resources:
       requests:
         storage: 8Gi # Enter a fictitious value
     storageClassName: <storage_class>
   ```
   {: codeblock}

   <table>
   <caption>Understanding the YAML file components</caption>
   <thead>
    <th>Component</th>
    <th>Description</th>
   </thead>
   <tbody>
   <tr>
   <td><code>name</code></td>
   <td>Enter the name of the PVC.</td>
   </tr>
   <tr>
   <td><code>namespace</code></td>
   <td>Enter the namespace where you want to create the PVC. The PVC must be created in the same namespace where you created the Kubernetes secret for your {{site.data.keyword.cos_full_notm}} service credentials and where you want to run your pod. </td>
   </tr>
   <tr>
   <td><code>ibm.io/auto-create-bucket</code></td>
   <td>Choose between the following options: <ul><li><strong>true</strong>: When you create the PVC, the PV and the bucket in your {{site.data.keyword.cos_full_notm}} service instance are automatically created. Choose this option to create a new bucket in your {{site.data.keyword.cos_full_notm}} service instance. </li><li><strong>false</strong>: Choose this option if you want to access data in an existing bucket. When you create the PVC, the PV is automatically created and linked to the bucket that you specify in <code>ibm.io/bucket</code>.</td>
   </tr>
   <tr>
   <td><code>ibm.io/auto-delete-bucket</code></td>
   <td>Choose between the following options: <ul><li><strong>true</strong>: Your data, the bucket, and the PV is automatically removed when you delete the PVC. Your {{site.data.keyword.cos_full_notm}} service instance remains and is not deleted. If you choose to set this option to <strong>true</strong>, then you must set <code>ibm.io/auto-create-bucket: true</code> and <code>ibm.io/bucket: ""</code> so that your bucket is automatically created with a name with the format <code>tmp-s3fs-xxxx</code>. </li><li><strong>false</strong>: When you delete the PVC, the PV is deleted automatically, but your data and the bucket in your {{site.data.keyword.cos_full_notm}} service instance remain. To access your data, you must create a new PVC with the name of your existing bucket. </li></ul>
   <tr>
   <td><code>ibm.io/bucket</code></td>
   <td>Choose between the following options: <ul><li>If <code>ibm.io/auto-create-bucket</code> is set to <strong>true</strong>: Enter the name of the bucket that you want to create in {{site.data.keyword.cos_full_notm}}. If in addition <code>ibm.io/auto-delete-bucket</code> is set to <strong>true</strong>, you must leave this field blank to automatically assign your bucket a name with the format <code>tmp-s3fs-xxxx</code>. The name must be unique in {{site.data.keyword.cos_full_notm}}. </li><li>If <code>ibm.io/auto-create-bucket</code> is set to <strong>false</strong>: Enter the name of the existing bucket that you want to access in the cluster. </li></ul> </td>
   </tr>
   <tr>
   <td><code>ibm.io/object-path</code></td>
   <td>Optional: Enter the name of the existing subdirectory in your bucket that you want to mount. Use this option if you want to mount a subdirectory only and not the entire bucket. To mount a subdirectory, you must set <code>ibm.io/auto-create-bucket: "false"</code> and provide the name of the bucket in <code>ibm.io/bucket</code>. </li></ul> </td>
   </tr>
   <tr>
   <td><code>ibm.io/secret-name</code></td>
   <td>Enter the name of the secret that holds the {{site.data.keyword.cos_full_notm}} credentials that you created earlier. </td>
   </tr>
   <tr>
  <td><code>ibm.io/endpoint</code></td>
  <td>If you created your {{site.data.keyword.cos_full_notm}} service instance in a location that is different from your cluster, enter the private or public service endpoint of your {{site.data.keyword.cos_full_notm}} service instance that you want to use. For an overview of available service endpoints, see [Additional endpoint information](/docs/cloud-object-storage?topic=cloud-object-storage-advanced-endpoints). By default, the <code>ibmc</code> Helm plug-in automatically retrieves your cluster location and creates the storage classes by using the {{site.data.keyword.cos_full_notm}} private service endpoint that matches your cluster location. If the cluster is in one of the metro city zones, such as `dal10`, the {{site.data.keyword.cos_full_notm}} private service endpoint for the metro city, in this case Dallas, is used. To verify that the service endpoint in your storage classes matches the service endpoint of your service instance, run `oc describe storageclass <storageclassname>`. Make sure that you enter your service endpoint in the format `https://<s3fs_private_service_endpoint>` for private service endpoints, or `http://<s3fs_public_service_endpoint>` for public service endpoints. If the service endpoint in your storage class matches the service endpoint of your {{site.data.keyword.cos_full_notm}} service instance, do not include the <code>ibm.io/endpoint</code> option in your PVC YAML file. </td>
  </tr>
   <tr>
   <td><code>storage</code></td>
   <td>In the spec resources requests section, enter a fictitious size for your {{site.data.keyword.cos_full_notm}} bucket in gigabytes. The size is required by Kubernetes, but not respected in {{site.data.keyword.cos_full_notm}}. You can enter any size that you want. The actual space that you use in {{site.data.keyword.cos_full_notm}} might be different and is billed based on the [pricing table ![External link icon](../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/cloud/object-storage/pricing/#s3api). </td>
   </tr>
   <tr>
   <td><code>storageClassName</code></td>
   <td>Choose between the following options: <ul><li>If <code>ibm.io/auto-create-bucket</code> is set to <strong>true</strong>: Enter the storage class that you want to use for your new bucket. </li><li>If <code>ibm.io/auto-create-bucket</code> is set to <strong>false</strong>: Enter the storage class that you used to create your existing bucket. </br></br>If you manually created the bucket in your {{site.data.keyword.cos_full_notm}} service instance or you cannot remember the storage class that you used, find your service instance in the {{site.data.keyword.cloud_notm}} dashboard and review the <strong>Class</strong> and <strong>Location</strong> of your existing bucket. Then, use the appropriate [storage class](#cos_storageclass_reference).<p class="note">The {{site.data.keyword.cos_full_notm}} API endpoint that is set in your storage class is based on the region that your cluster is in. If you want to access a bucket that is located in a different region than the one where your cluster is in, you must create a [custom storage class](/docs/openshift?topic=openshift-kube_concepts#customized_storageclass) and use the appropriate API endpoint for your bucket.</p></li></ul>  </td>
   </tr>
   </tbody>
   </table>

2. Create the PVC.
   ```
   oc apply -f filepath/pvc.yaml
   ```
   {: pre}

3. Verify that your PVC is created and bound to the PV.
   ```
   oc get pvc
   ```
   {: pre}

   Example output:
   ```
   NAME                  STATUS    VOLUME                                     CAPACITY   ACCESS MODES   STORAGECLASS                     AGE
   s3fs-test-pvc         Bound     pvc-b38b30f9-1234-11e8-ad2b-t910456jbe12   8Gi        RWO            ibmc-s3fs-standard-cross-region  1h
   ```
   {: screen}

4. Optional: If you plan to access your data with a non-root user, or added files to an existing {{site.data.keyword.cos_full_notm}} bucket by using the console or the API directly, make sure that the [files have the correct permission](/docs/openshift?topic=openshift-cs_troubleshoot_storage#cos_nonroot_access) assigned so that your app can successfully read and update the files as needed.

5.  {: #cos_app_volume_mount}To mount the PV to your deployment, create a configuration `.yaml` file and specify the PVC that binds the PV.

    ```yaml
    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: <deployment_name>
      labels:
        app: <deployment_label>
    spec:
      selector:
        matchLabels:
          app: <app_name>
      template:
        metadata:
          labels:
            app: <app_name>
        spec:
          containers:
          - image: <image_name>
            name: <container_name>
            securityContext:
              runAsUser: <non_root_user>
            volumeMounts:
            - name: <volume_name>
              mountPath: /<file_path>
          volumes:
          - name: <volume_name>
            persistentVolumeClaim:
              claimName: <pvc_name>
    ```
    {: codeblock}

    <table>
    <caption>Understanding the YAML file components</caption>
    <thead>
      <th>Component</th>
      <th>Description</th>
    </thead>
    <tbody>
    <tr>
    <td><code>app</code></td>
    <td>In the metadata section, enter label for the deployment.</td>
      </tr>
      <tr>
      <td><code>matchLabels.app</code> <br/> <code>labels.app</code></td>
      <td>In the spec selector and in the spec template metadata sections, enter a label for your app.</td>
      </tr>
    <tr>
    <td><code>image</code></td>
    <td>The name of the container image that you want to use. To list available images in your {{site.data.keyword.registrylong_notm}} account, run `ibmcloud cr image-list`.</td>
    </tr>
    <tr>
    <td><code>name</code></td>
    <td>The name of the container that you want to deploy to your cluster.</td>
    </tr>
    <tr>
    <td><code>runAsUser</code></td>
    <td>In the spec containers security context section, you can optionally set the run as user value. To run the app with a non-root user in a cluster that runs Kubernetes version 1.12 or earlier, specify the [security context](https://kubernetes.io/docs/tasks/configure-pod-container/security-context/){: external} for your pod by defining the non-root user.</td>
    </tr>
    <tr>
    <td><code>mountPath</code></td>
    <td>In the spec containers volume mounts section, enter the absolute path of the directory to where the volume is mounted inside the container. If you want to share a volume between different apps, you can specify [volume sub paths](https://kubernetes.io/docs/concepts/storage/volumes/#using-subpath){: external} for each of your apps.</td>
    </tr>
    <tr>
    <td><code>name</code></td>
    <td>In the spec containers volume mounts section, enter the name of the volume to mount to your pod.</td>
    </tr>
    <tr>
    <td><code>name</code></td>
    <td>In the volumes section, enter the name of the volume to mount to your pod. Typically this name is the same as <code>volumeMounts/name</code>.</td>
    </tr>
    <tr>
    <td><code>claimName</code></td>
    <td>In the volumes persistent volume claim section, enter the name of the PVC that binds the PV that you want to use. </td>
    </tr>
    </tbody></table>

6.  Create the deployment.
    ```
    oc apply -f <local_yaml_path>
    ```
    {: pre}

7.  Verify that the PV is successfully mounted.

    ```
    oc describe deployment <deployment_name>
    ```
    {: pre}

    The mount point is in the **Volume Mounts** field and the volume is in the **Volumes** field.

    ```
    Volume Mounts:
          /var/run/secrets/kubernetes.io/serviceaccount from default-token-tqp61 (ro)
          /volumemount from myvol (rw)
    ...
    Volumes:
      myvol:
        Type:	PersistentVolumeClaim (a reference to a PersistentVolumeClaim in the same namespace)
        ClaimName:	mypvc
        ReadOnly:	false
    ```
    {: screen}

8. Verify that you can write data to your {{site.data.keyword.cos_full_notm}} service instance.
   1. Log in to the pod that mounts your PV.
      ```
      oc exec <pod_name> -it bash
      ```
      {: pre}

   2. Navigate to your volume mount path that you defined in your app deployment.
   3. Create a text file.
      ```
      echo "This is a test" > test.txt
      ```
      {: pre}

   4. From the {{site.data.keyword.Bluemix}} dashboard, navigate to your {{site.data.keyword.cos_full_notm}} service instance.
   5. From the menu, select **Buckets**.
   6. Open your bucket, and verify that you can see the `test.txt` that you created.

   <br />


## Using object storage in a stateful set
{: #cos_statefulset}

If you have a stateful app such as a database, you can create stateful sets that use {{site.data.keyword.cos_full_notm}} to store your app's data. Alternatively, you can use an {{site.data.keyword.cloud_notm}} database-as-a-service, such as {{site.data.keyword.cloudant_short_notm}} and store your data in the cloud.
{: shortdesc}

Before you begin:
- [Create and prepare your {{site.data.keyword.cos_full_notm}} service instance](#create_cos_service).
- [Create a secret to store your {{site.data.keyword.cos_full_notm}} service credentials](#create_cos_secret).
- [Decide on the configuration for your {{site.data.keyword.cos_full_notm}}](#configure_cos).

To deploy a stateful set that uses object storage:

1. Create a configuration file for your stateful set and the service that you use to expose the stateful set. The following examples show how to deploy NGINX as a stateful set with three replicas, each replica with a separate bucket or sharing the same bucket.

   **Example to create a stateful set with three replicas, with each replica using a separate bucket**:
   ```yaml
   apiVersion: v1
   kind: Service
   metadata:
     name: nginx-v01
     namespace: default
     labels:
       app: nginx-v01 # must match spec.template.metadata.labels and spec.selector.matchLabels in stateful set YAML
   spec:
     ports:
     - port: 80
       name: web
     clusterIP: None
     selector:
       app: nginx-v01 # must match spec.template.metadata.labels and spec.selector.matchLabels in stateful set YAML
   ---
   apiVersion: apps/v1
   kind: StatefulSet
   metadata:
     name: web-v01
     namespace: default
   spec:
     selector:
       matchLabels:
         app: nginx-v01 # must match spec.template.metadata.labels in stateful set YAML and metadata.labels in service YAML
     serviceName: "nginx-v01"
     replicas: 3
     template:
       metadata:
         labels:
           app: nginx-v01 # must match spec.selector.matchLabels in stateful set YAML and metadata.labels in service YAML
       spec:
         terminationGracePeriodSeconds: 10
         containers:
         - name: nginx
           image: k8s.gcr.io/nginx-slim:0.8
           ports:
           - containerPort: 80
             name: web
           volumeMounts:
           - name: mypvc
             mountPath: /usr/share/nginx/html
     volumeClaimTemplates:
     - metadata:
         name: mypvc
         annotations:
           ibm.io/auto-create-bucket: "true"
           ibm.io/auto-delete-bucket: "true"
           ibm.io/bucket: ""
           ibm.io/secret-name: mysecret
           volume.beta.kubernetes.io/storage-class: ibmc-s3fs-standard-perf-cross-region
           volume.beta.kubernetes.io/storage-provisioner: ibm.io/ibmc-s3fs
       spec:
         accessModes: [ "ReadWriteOnce" ]
         storageClassName: "ibmc-s3fs-standard-perf-cross-region"
         resources:
           requests:
             storage: 1Gi
   ```
   {: codeblock}

   **Example to create a stateful set with three replicas that share the same bucket `mybucket`**:
   ```yaml
   apiVersion: v1
   kind: Service
   metadata:
     name: nginx-v01
     namespace: default
     labels:
       app: nginx-v01 # must match spec.template.metadata.labels and spec.selector.matchLabels in stateful set YAML
   spec:
     ports:
     - port: 80
       name: web
     clusterIP: None
     selector:
       app: nginx-v01 # must match spec.template.metadata.labels and spec.selector.matchLabels in stateful set YAML
   ---
   apiVersion: apps/v1
   kind: StatefulSet
   metadata:
     name: web-v01
     namespace: default
   spec:
     selector:
       matchLabels:
         app: nginx-v01 # must match spec.template.metadata.labels in stateful set YAML and metadata.labels in service YAML
     serviceName: "nginx-v01"
     replicas: 3
     template:
       metadata:
         labels:
           app: nginx-v01 # must match spec.selector.matchLabels in stateful set YAML and metadata.labels in service YAML
       spec:
         terminationGracePeriodSeconds: 10
         containers:
         - name: nginx
           image: k8s.gcr.io/nginx-slim:0.8
           ports:
           - containerPort: 80
             name: web
           volumeMounts:
           - name: mypvc
             mountPath: /usr/share/nginx/html
     volumeClaimTemplates:
     - metadata:
         name: mypvc
         annotations:
           ibm.io/auto-create-bucket: "false"
           ibm.io/auto-delete-bucket: "false"
           ibm.io/bucket: mybucket
           ibm.io/secret-name: mysecret
           volume.beta.kubernetes.io/storage-class: ibmc-s3fs-standard-perf-cross-region
           volume.beta.kubernetes.io/storage-provisioner: ibm.io/ibmc-s3fs
       spec:
         accessModes: [ "ReadOnlyMany" ]
         storageClassName: "ibmc-s3fs-standard-perf-cross-region"
         resources:
           requests:
             storage: 1Gi
   ```
   {: codeblock}


   <table>
    <caption>Understanding the stateful set YAML file components</caption>
    <thead>
    <th>Component</th>
    <th>Description</th>
    </thead>
    <tbody>
    <tr>
    <td style="text-align:left"><code>name</code></td>
    <td style="text-align:left">Enter a name for your stateful set. The name that you enter is used to create the name for your PVC in the format: <code>&lt;volume_name&gt;-&lt;statefulset_name&gt;-&lt;replica_number&gt;</code>. </td>
    </tr>
    <tr>
    <td style="text-align:left"><code>serviceName</code></td>
    <td style="text-align:left">Enter the name of the service that you want to use to expose your stateful set. </td>
    </tr>
    <tr>
    <td style="text-align:left"><code>replicas</code></td>
    <td style="text-align:left">Enter the number of replicas for your stateful set. </td>
    </tr>
    <tr>
    <td style="text-align:left"><code>matchLabels</code></td>
    <td style="text-align:left">In the spec selector match labels section, enter all labels that you want to include in your stateful set and your PVC. Labels that you include in the <code>volumeClaimTemplates</code> of your stateful set are not recognized by Kubernetes. Instead, you must define these labels in the <code>spec.selector.matchLabels</code> and <code>spec.template.metadata.labels</code> section of your stateful set YAML. To make sure that all your stateful set replicas are included into the load balancing of your service, include the same label that you used in the <code>spec.selector</code> section of your service YAML. </td>
    </tr>
    <tr>
    <td style="text-align:left"><code>labels</code></td>
    <td style="text-align:left">In the spec metadata labels section, enter the same labels that you added to the <code>spec.selector.matchLabels</code> section of your stateful set YAML. </td>
    </tr>
    <tr>
    <td><code>terminationGracePeriodSeconds</code></td>
    <td>Enter the number of seconds to give the <code>kubelet</code> to gracefully terminate the pod that runs your stateful set replica. For more information, see [Delete Pods ![External link icon](../icons/launch-glyph.svg "External link icon")](https://kubernetes.io/docs/tasks/run-application/force-delete-stateful-set-pod/#delete-pods). </td>
    </tr>
    <tr>
    <td style="text-align:left"><code>name</code></td>
    <td style="text-align:left">In the spec volume claim templates metadata section, enter a name for your volume. Use the same name that you defined in the <code>spec.containers.volumeMount.name</code> section. The name that you enter here is used to create the name for your PVC in the format: <code>&lt;volume_name&gt;-&lt;statefulset_name&gt;-&lt;replica_number&gt;</code>. </td>
    </tr>
    <tr>
    <td><code>ibm.io/auto-create-bucket</code></td>
    <td>In the spec volume claim templates metadata section, set an annotation to configure how buckets are created. Choose between the following options: <ul><li><strong>true: </strong>Choose this option to automatically create a bucket for each stateful set replica. </li><li><strong>false: </strong>Choose this option if you want to share an existing bucket across your stateful set replicas. Make sure to define the name of the bucket in the <code>spec.volumeClaimTemplates.metadata.annotions.ibm.io/bucket</code> section of your stateful set YAML.</li></ul></td>
    </tr>
    <tr>
    <td><code>ibm.io/auto-delete-bucket</code></td>
    <td>In the spec volume claim templates metadata section, set an annotation to configure how buckets are deleted. Choose between the following options: <ul><li><strong>true: </strong>Your data, the bucket, and the PV is automatically removed when you delete the PVC. Your {{site.data.keyword.cos_full_notm}} service instance remains and is not deleted. If you choose to set this option to true, then you must set <code>ibm.io/auto-create-bucket: true</code> and <code>ibm.io/bucket: ""</code> so that your bucket is automatically created with a name with the format <code>tmp-s3fs-xxxx</code>. </li><li><strong>false: </strong>When you delete the PVC, the PV is deleted automatically, but your data and the bucket in your {{site.data.keyword.cos_full_notm}} service instance remain. To access your data, you must create a new PVC with the name of your existing bucket.</li></ul></td>
    </tr>
    <tr>
    <td><code>ibm.io/bucket</code></td>
    <td>In the spec volume claim templates metadata section, set an annotation for the bucket details. Choose between the following options: <ul><li><strong>If <code>ibm.io/auto-create-bucket</code> is set to true: </strong>Enter the name of the bucket that you want to create in {{site.data.keyword.cos_full_notm}}. If in addition <code>ibm.io/auto-delete-bucket</code> is set to <strong>true</strong>, you must leave this field blank to automatically assign your bucket a name with the format tmp-s3fs-xxxx. The name must be unique in {{site.data.keyword.cos_full_notm}}.</li><li><strong>If <code>ibm.io/auto-create-bucket</code> is set to false: </strong>Enter the name of the existing bucket that you want to access in the cluster.</li></ul></td>
    </tr>
    <tr>
    <td><code>ibm.io/secret-name</code></td>
    <td>In the spec volume claim templates metadata annotations section, enter the name of the secret that holds the {{site.data.keyword.cos_full_notm}} credentials that you created earlier.</td>
    </tr>
    <tr>
    <td style="text-align:left"><code>kubernetes.io/storage-class</code></td>
    <td style="text-align:left">In the spec volume claim templates metadata annotations section, enter the storage class that you want to use. Choose between the following options: <ul><li><strong>If <code>ibm.io/auto-create-bucket</code> is set to true: </strong>Enter the storage class that you want to use for your new bucket.</li><li><strong>If <code>ibm.io/auto-create-bucket</code> is set to false: </strong>Enter the storage class that you used to create your existing bucket.</li></ul></br>  To list existing storage classes, run <code>oc get storageclasses | grep s3</code>. If you do not specify a storage class, the PVC is created with the default storage class that is set in your cluster. Make sure that the default storage class uses the <code>ibm.io/ibmc-s3fs</code> provisioner so that your stateful set is provisioned with object storage.</td>
    </tr>
    <tr>
    <td style="text-align:left"><code>storageClassName</code></td>
    <td>In the spec volume claim templates spec section, enter the same storage class that you entered in the <code>spec.volumeClaimTemplates.metadata.annotations.volume.beta.kubernetes.io/storage-class</code> section of your stateful set YAML.  </td>
    </tr>
    <tr>
    <td style="text-align:left"><code>storage</code></td>
    <td>In the spec volume claim templates spec resource requests section, enter a fictitious size for your {{site.data.keyword.cos_full_notm}} bucket in gigabytes. The size is required by Kubernetes, but not respected in {{site.data.keyword.cos_full_notm}}. You can enter any size that you want. The actual space that you use in {{site.data.keyword.cos_full_notm}} might be different and is billed based on the [pricing table ![External link icon](../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/cloud/object-storage/pricing/#s3api).</td>
    </tr>
    </tbody></table>

    <br />



## Backing up and restoring data
{: #cos_backup_restore}

{{site.data.keyword.cos_full_notm}} is set up to provide high durability for your data so that your data is protected from being lost. You can find the SLA in the [{{site.data.keyword.cos_full_notm}} service terms](https://www-03.ibm.com/software/sla/sladb.nsf/sla/bm-7857-03){: external}.
{: shortdesc}

{{site.data.keyword.cos_full_notm}} does not provide a version history for your data. If you need to maintain and access older versions of your data, you must set up your app to manage the history of data or implement alternative backup solutions. For example, you might want to store your {{site.data.keyword.cos_full_notm}} data in your on-prem database or use tapes to archive your data.
{: note}

<br />



## Storage class reference
{: #cos_storageclass_reference}

### Standard
{: #standard}

<table>
<caption>Object storage class: standard</caption>
<thead>
<th>Characteristics</th>
<th>Setting</th>
</thead>
<tbody>
<tr>
<td>Name</td>
<td><code>ibmc-s3fs-standard-cross-region</code></br><code>ibmc-s3fs-standard-perf-cross-region</code></br><code>ibmc-s3fs-standard-regional</code></br><code>ibmc-s3fs-standard-perf-regional</code></td>
</tr>
<tr>
<td>Default resiliency endpoint</td>
<td>The resiliency endpoint is automatically set based on the location that your cluster is in. For more information, see [Regions and endpoints](/docs/cloud-object-storage/basics?topic=cloud-object-storage-endpoints#endpoints). </td>
</tr>
<tr>
<td>Chunk size</td>
<td>Storage classes without `perf`: 16 MB</br>Storage classes with `perf`: 52 MB</td>
</tr>
<tr>
<td>Kernel cache</td>
<td>Enabled</td>
</tr>
<tr>
<td>Billing</td>
<td>Monthly</td>
</tr>
<tr>
<td>Pricing</td>
<td>[Pricing ![External link icon](../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/cloud/object-storage/pricing/#s3api)</td>
</tr>
</tbody>
</table>



### Vault
{: #Vault}

<table>
<caption>Object storage class: vault</caption>
<thead>
<th>Characteristics</th>
<th>Setting</th>
</thead>
<tbody>
<tr>
<td>Name</td>
<td><code>ibmc-s3fs-vault-cross-region</code></br><code>ibmc-s3fs-vault-regional</code></td>
</tr>
<tr>
<td>Default resiliency endpoint</td>
<td>The resiliency endpoint is automatically set based on the location that your cluster is in. For more information, see [Regions and endpoints](/docs/cloud-object-storage/basics?topic=cloud-object-storage-endpoints#endpoints). </td>
</tr>
<tr>
<td>Chunk size</td>
<td>16 MB</td>
</tr>
<tr>
<td>Kernel cache</td>
<td>Disabled</td>
</tr>
<tr>
<td>Billing</td>
<td>Monthly</td>
</tr>
<tr>
<td>Pricing</td>
<td>[Pricing ![External link icon](../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/cloud/object-storage/pricing/#s3api)</td>
</tr>
</tbody>
</table>

### Cold
{: #cold}

<table>
<caption>Object storage class: cold</caption>
<thead>
<th>Characteristics</th>
<th>Setting</th>
</thead>
<tbody>
<tr>
<td>Name</td>
<td><code>ibmc-s3fs-flex-cross-region</code></br><code>ibmc-s3fs-flex-perf-cross-region</code></br><code>ibmc-s3fs-flex-regional</code></br><code>ibmc-s3fs-flex-perf-regional</code></td>
</tr>
<tr>
<td>Default resiliency endpoint</td>
<td>The resiliency endpoint is automatically set based on the location that your cluster is in. For more information, see [Regions and endpoints](/docs/cloud-object-storage/basics?topic=cloud-object-storage-endpoints#endpoints). </td>
</tr>
<tr>
<td>Chunk size</td>
<td>16 MB</td>
</tr>
<tr>
<td>Kernel cache</td>
<td>Disabled</td>
</tr>
<tr>
<td>Billing</td>
<td>Monthly</td>
</tr>
<tr>
<td>Pricing</td>
<td>[Pricing ![External link icon](../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/cloud/object-storage/pricing/#s3api)</td>
</tr>
</tbody>
</table>

### Flex
{: #flex}

<table>
<caption>Object storage class: flex</caption>
<thead>
<th>Characteristics</th>
<th>Setting</th>
</thead>
<tbody>
<tr>
<td>Name</td>
<td><code>ibmc-s3fs-cold-cross-region</code></br><code>ibmc-s3fs-flex-perf-cross-region</code></br><code>ibmc-s3fs-cold-regional</code></br><code>ibmc-s3fs-flex-perf-regional</code></td>
</tr>
<tr>
<td>Default resiliency endpoint</td>
<td>The resiliency endpoint is automatically set based on the location that your cluster is in. For more information, see [Regions and endpoints](/docs/cloud-object-storage/basics?topic=cloud-object-storage-endpoints#endpoints). </td>
</tr>
<tr>
<td>Chunk size</td>
<td>Storage classes without `perf`: 16 MB</br>Storage classes with `perf`: 52 MB</td>
</tr>
<tr>
<td>Kernel cache</td>
<td>Enabled</td>
</tr>
<tr>
<td>Billing</td>
<td>Monthly</td>
</tr>
<tr>
<td>Pricing</td>
<td>[Pricing ![External link icon](../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/cloud/object-storage/pricing/#s3api)</td>
</tr>
</tbody>
</table>

## Limitations
{: #cos_limitations}

* {{site.data.keyword.cos_full_notm}} is based on the `s3fs-fuse` file system. You can review a list of limitations in the [`s3fs-fuse` repository](https://github.com/s3fs-fuse/s3fs-fuse#limitations).
* To access a file in {{site.data.keyword.cos_full_notm}} with a non-root user, you must set the `runAsUser` and `fsGroup` values in your deployment to the same value.



