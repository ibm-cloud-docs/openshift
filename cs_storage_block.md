---

copyright:
  years: 2014, 2019
lastupdated: "2019-07-26"

keywords: kubernetes, iks

subcollection: containers

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}rwo
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:download: .download}
{:preview: .preview}

# Storing data on classic IBM Cloud Block Storage
{: #block_storage}

{{site.data.keyword.cloud_notm}} Block Storage is persistent, high-performance iSCSI storage that you can add to your apps by using Kubernetes persistent volumes (PVs). You can choose between predefined storage tiers with GB sizes and IOPS that meet the requirements of your workloads. To find out whether {{site.data.keyword.cloud_notm}} Block Storage is the right storage option for you, see [Choosing a storage solution](/docs/containers?topic=containers-storage_planning#choose_storage_solution). For more information about pricing, see [Billing](/docs/infrastructure/BlockStorage?topic=BlockStorage-About#billing).
{: shortdesc}

{{site.data.keyword.cloud_notm}} Block Storage is available for standard clusters only. If your cluster cannot access the public network, such as a private cluster behind a firewall or a cluster with only the private service endpoint that is enabled, make sure that you installed the {{site.data.keyword.cloud_notm}} Block Storage plug-in version 1.3.0 or later to connect to your block storage instance over the private network. Block storage instances are specific to a single zone. If you have a multizone cluster, consider [multizone persistent storage options](/docs/containers?topic=containers-storage_planning#persistent_storage_overview).
{: important}

## Installing the {{site.data.keyword.cloud_notm}} Block Storage plug-in in your cluster
{: #install_block}

Install the {{site.data.keyword.cloud_notm}} Block Storage plug-in with a Helm chart to set up pre-defined storage classes for block storage. You can use these storage classes to create a PVC to provision block storage for your apps.
{: shortdesc}

Before you begin: [Log in to your account. If applicable, target the appropriate resource group. Set the context for your cluster.](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure)

1. Make sure that your worker node applies the latest patch for your minor version.
   1. List the current patch version of your worker nodes.
      ```
      ibmcloud ks workers --cluster <cluster_name_or_ID>
      ```
      {: pre}

      Example output:
      ```
      OK
      ID                                                  Public IP        Private IP     Machine Type           State    Status   Zone    Version
      kube-dal10-crb1a23b456789ac1b20b2nc1e12b345ab-w26   169.xx.xxx.xxx    10.xxx.xx.xxx   b3c.4x16.encrypted     normal   Ready    dal10   1.13.8_1523*
      ```
      {: screen}

      If your worker node does not apply the latest patch version, you see an asterisk (`*`) in the **Version** column of your CLI output.

   2. Review the [version changelog](/docs/containers?topic=containers-changelog#changelog) to find the changes that are included in the latest patch version.

   3. Apply the latest patch version by reloading your worker node. Follow the instructions in the [ibmcloud ks worker-reload command](/docs/containers?topic=containers-cli-plugin-kubernetes-service-cli#cs_worker_reload) to gracefully reschedule any running pods on your worker node before you reload your worker node. Note that during the reload, your worker node machine is updated with the latest image and data is deleted if not [stored outside the worker node](/docs/containers?topic=containers-storage_planning#persistent_storage_overview).

1.  [Follow the instructions](/docs/containers?topic=containers-helm#public_helm_install) to install the Helm client on your local machine, and install the Helm server (Tiller) with a service account in your cluster.

    The installation of the Helm server Tiller requires public network connection to the public Google Container Registry. If your cluster cannot access the public network, such as a private cluster behind a firewall or a cluster with only the private service endpoint that is enabled, you can choose to [pull the Tiller image to your local machine and push the image to your namespace in {{site.data.keyword.registryshort_notm}}](/docs/containers?topic=containers-helm#private_local_tiller), or to [install the Helm chart without using Tiller](/docs/containers?topic=containers-helm#private_install_without_tiller).
    {: note}

2.  Verify that Tiller is installed with a service account.

    ```
    {[kubectl]} get serviceaccount -n kube-system tiller
    ```
    {: pre}

    Example output:

    ```
    NAME                                 SECRETS   AGE
    tiller                               1         2m
    ```
    {: screen}

3. Add the {{site.data.keyword.cloud_notm}} Helm chart repository to the cluster where you want to use the {{site.data.keyword.cloud_notm}} Block Storage plug-in.
   ```
   helm repo add iks-charts https://icr.io/helm/iks-charts
   ```
   {: pre}

4. Update the Helm repo to retrieve the latest version of all Helm charts in this repo.
   ```
   helm repo update
   ```
   {: pre}

5. Install the {{site.data.keyword.cloud_notm}} Block Storage plug-in. When you install the plug-in, pre-defined block storage classes are added to your cluster.
   ```
   helm install iks-charts/ibmcloud-block-storage-plugin
   ```
   {: pre}

   Example output:
   ```
   NAME:   bald-olm
   LAST DEPLOYED: Wed Apr 18 10:02:55 2018
   NAMESPACE: default
   STATUS: DEPLOYED

   RESOURCES:
   ==> v1beta1/DaemonSet
   NAME                           DESIRED  CURRENT  READY  UP-TO-DATE  AVAILABLE  NODE SELECTOR  AGE
   ibmcloud-block-storage-driver  0        0        0      0           0          <none>         0s

   ==> v1beta1/Deployment
   NAME                           DESIRED  CURRENT  UP-TO-DATE  AVAILABLE  AGE
   ibmcloud-block-storage-plugin  1        0        0           0          0s

   ==> v1/StorageClass
   NAME                      PROVISIONER        AGE
   ibmc-block-bronze         ibm.io/ibmc-block  0s
   ibmc-block-custom         ibm.io/ibmc-block  0s
   ibmc-block-gold           ibm.io/ibmc-block  0s
   ibmc-block-retain-bronze  ibm.io/ibmc-block  0s
   ibmc-block-retain-custom  ibm.io/ibmc-block  0s
   ibmc-block-retain-gold    ibm.io/ibmc-block  0s
   ibmc-block-retain-silver  ibm.io/ibmc-block  0s
   ibmc-block-silver         ibm.io/ibmc-block  0s

   ==> v1/ServiceAccount
   NAME                           SECRETS  AGE
   ibmcloud-block-storage-plugin  1        0s

   ==> v1beta1/ClusterRole
   NAME                           AGE
   ibmcloud-block-storage-plugin  0s

   ==> v1beta1/ClusterRoleBinding
   NAME                           AGE
   ibmcloud-block-storage-plugin  0s

   NOTES:
   Thank you for installing: ibmcloud-block-storage-plugin.   Your release is named: bald-olm
   ```
   {: screen}

6. Verify that the installation was successful.
   ```
   {[kubectl]} get pod -n kube-system | grep block
   ```
   {: pre}

   Example output:
   ```
   ibmcloud-block-storage-driver-kh4mt                              1/1       Running   0          27d       10.118.98.19   10.118.98.19
   ibmcloud-block-storage-plugin-58c5f9dc86-pbl4t                   1/1       Running   0          14d       172.21.0.204   10.118.98.19
   ```
   {: screen}

   The installation is successful when you see one `ibmcloud-block-storage-plugin` pod and one or more `ibmcloud-block-storage-driver` pods. The number of `ibmcloud-block-storage-driver` pods equals the number of worker nodes in your cluster. All pods must be in a **Running** state.

7. Verify that the storage classes for block storage were added to your cluster.
   ```
   {[kubectl]} get storageclasses | grep block
   ```
   {: pre}

   Example output:
   ```
   ibmc-block-bronze            ibm.io/ibmc-block
   ibmc-block-custom            ibm.io/ibmc-block
   ibmc-block-gold              ibm.io/ibmc-block
   ibmc-block-retain-bronze     ibm.io/ibmc-block
   ibmc-block-retain-custom     ibm.io/ibmc-block
   ibmc-block-retain-gold       ibm.io/ibmc-block
   ibmc-block-retain-silver     ibm.io/ibmc-block
   ibmc-block-silver            ibm.io/ibmc-block
   ```
   {: screen}

8. Repeat these steps for every cluster where you want to provision block storage.

You can now continue to [create a PVC](#add_block) to provision block storage for your app.


### Updating the {{site.data.keyword.cloud_notm}} Block Storage plug-in
You can upgrade the existing {{site.data.keyword.cloud_notm}} Block Storage plug-in to the latest version.
{: shortdesc}

Before you begin: [Log in to your account. If applicable, target the appropriate resource group. Set the context for your cluster.](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure)

1. Update the Helm repo to retrieve the latest version of all helm charts in this repo.
   ```
   helm repo update
   ```
   {: pre}

2. Optional: Download the latest Helm chart to your local machine. Then, extract the package and review the `release.md` file to find the latest release information.
   ```
   helm fetch iks-charts/ibmcloud-block-storage-plugin
   ```
   {: pre}

3. Find the name of the block storage Helm chart that you installed in your cluster.
   ```
   helm ls | grep ibmcloud-block-storage-plugin
   ```
   {: pre}

   Example output:
   ```
   myhelmchart 	1       	Mon Sep 18 15:31:40 2017	DEPLOYED	ibmcloud-block-storage-plugin-0.1.0	default
   ```
   {: screen}

4. Upgrade the {{site.data.keyword.cloud_notm}} Block Storage plug-in to the latest version.
   ```
   helm upgrade --force --recreate-pods <helm_chart_name>  iks-charts/ibmcloud-block-storage-plugin
   ```
   {: pre}

5. Optional: When you update the plug-in, the `default` storage class is unset. If you want to set the default storage class to a storage class of your choice, run the following command.
   ```
   {[kubectl]} patch storageclass <storageclass> -p '{"metadata": {"annotations":{"storageclass.kubernetes.io/is-default-class":"true"}}}'
   ```
   {: pre}


### Removing the {{site.data.keyword.cloud_notm}} Block Storage plug-in
If you do not want to provision and use {{site.data.keyword.cloud_notm}} Block Storage in your cluster, you can uninstall the Helm chart.
{: shortdesc}

Removing the plug-in does not remove existing PVCs, PVs, or data. When you remove the plug-in, all the related pods and daemon sets are removed from your cluster. You cannot provision new block storage for your cluster or use existing block storage PVCs and PVs after you remove the plug-in.
{: important}

Before you begin:
- [Log in to your account. If applicable, target the appropriate resource group. Set the context for your cluster.](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure)
- Make sure that you do not have any PVCs or PVs in your cluster that use block storage.

To remove the plug-in:

1. Find the name of the block storage Helm chart that you installed in your cluster.
   ```
   helm ls | grep ibmcloud-block-storage-plugin
   ```
   {: pre}

   Example output:
   ```
   myhelmchart 	1       	Mon Sep 18 15:31:40 2017	DEPLOYED	ibmcloud-block-storage-plugin-0.1.0	default
   ```
   {: screen}

2. Delete the {{site.data.keyword.cloud_notm}} Block Storage plug-in.
   ```
   helm delete <helm_chart_name>
   ```
   {: pre}

3. Verify that the block storage pods are removed.
   ```
   {[kubectl]} get pod -n kube-system | grep ibmcloud-block-storage-plugin
   ```
   {: pre}
   The removal of the pods is successful if no pods are displayed in your CLI output.

4. Verify that the block storage classes are removed.
   ```
   {[kubectl]} get storageclasses | grep block
   ```
   {: pre}
   The removal of the storage classes is successful if no storage classes are displayed in your CLI output.

<br />



## Deciding on the block storage configuration
{: #block_predefined_storageclass}

{{site.data.keyword.containerlong}} provides pre-defined storage classes for block storage that you can use to provision block storage with a specific configuration.
{: shortdesc}

Every storage class specifies the type of block storage that you provision, including available size, IOPS, file system, and the retention policy.  

Make sure to choose your storage configuration carefully to have enough capacity to store your data. After you provision a specific type of storage by using a storage class, you cannot change the size, type, IOPS, or retention policy for the storage device. If you need more storage or storage with a different configuration, you must [create a new storage instance and copy the data](/docs/containers?topic=containers-kube_concepts#update_storageclass) from the old storage instance to your new one.
{: important}

1. List available storage classes in {{site.data.keyword.containerlong}}.
    ```
    {[kubectl]} get storageclasses | grep block
    ```
    {: pre}

    Example output:
    ```
    $ {[kubectl]} get storageclasses
    NAME                         TYPE
    ibmc-block-custom            ibm.io/ibmc-block
    ibmc-block-bronze            ibm.io/ibmc-block
    ibmc-block-gold              ibm.io/ibmc-block
    ibmc-block-silver            ibm.io/ibmc-block
    ibmc-block-retain-bronze     ibm.io/ibmc-block
    ibmc-block-retain-silver     ibm.io/ibmc-block
    ibmc-block-retain-gold       ibm.io/ibmc-block
    ibmc-block-retain-custom     ibm.io/ibmc-block
    ```
    {: screen}

2. Review the configuration of a storage class.
   ```
   {[kubectl]} describe storageclass <storageclass_name>
   ```
   {: pre}

   For more information about each storage class, see the [storage class reference](#block_storageclass_reference). If you do not find what you are looking for, consider creating your own customized storage class. To get started, check out the [customized storage class samples](#block_custom_storageclass).
   {: tip}

3. Choose the type of block storage that you want to provision.
   - **Bronze, silver, and gold storage classes:** These storage classes provision [Endurance storage](/docs/infrastructure/BlockStorage?topic=BlockStorage-About#provendurance). With Endurance storage, you can choose the size of the storage in gigabytes at predefined IOPS tiers.
   - **Custom storage class:** This storage class provisions [Performance storage](/docs/infrastructure/BlockStorage?topic=BlockStorage-About#provperformance). With performance storage, you have more control over the size of the storage and the IOPS.

4. Choose the size and IOPS for your block storage. The size and the number of IOPS define the total number of IOPS (input/ output operations per second) that serves as an indicator for how fast your storage is. The more total IOPS your storage has, the faster it processes read and write operations.
   - **Bronze, silver, and gold storage classes:** These storage classes come with a fixed number of IOPS per gigabyte and are provisioned on SSD hard disks. The total number of IOPS depends on the size of the storage that you choose. You can select any whole number of gigabyte within the allowed size range, such as 20 Gi, 256 Gi, or 11854 Gi. To determine the total number of IOPS, you must multiply the IOPS with the selected size. For example, if you select a 1000Gi block storage size in the silver storage class that comes with 4 IOPS per GB, your storage has a total of 4000 IOPS.  
     <table>
         <caption>Table of storage class size ranges and IOPS per gigabyte</caption>
         <thead>
         <th>Storage class</th>
         <th>IOPS per gigabyte</th>
         <th>Size range in gigabytes</th>
         </thead>
         <tbody>
         <tr>
         <td>Bronze</td>
         <td>2 IOPS/GB</td>
         <td>20-12000 Gi</td>
         </tr>
         <tr>
         <td>Silver</td>
         <td>4 IOPS/GB</td>
         <td>20-12000 Gi</td>
         </tr>
         <tr>
         <td>Gold</td>
         <td>10 IOPS/GB</td>
         <td>20-4000 Gi</td>
         </tr>
         </tbody></table>
   - **Custom storage class:** When you choose this storage class, you have more control over the size and IOPS that you want. For the size, you can select any whole number of gigabyte within the allowed size range. The size that you choose determines the IOPS range that is available to you. You can choose an IOPS that is a multiple of 100 that is in the specified range. The IOPS that you choose is static and does not scale with the size of the storage. For example, if you choose 40Gi with 100 IOPS, your total IOPS remains 100. </br></br>The IOPS to gigabyte ratio also determines the type of hard disk that is provisioned for you. For example, if you have 500Gi at 100 IOPS, your IOPS to gigabyte ratio is 0.2. Storage with a ratio of less than or equal to 0.3 is provisioned on SATA hard disks. If your ratio is greater than 0.3, then your storage is provisioned on SSD hard disks.
     <table>
         <caption>Table of custom storage class size ranges and IOPS</caption>
         <thead>
         <th>Size range in gigabytes</th>
         <th>IOPS range in multiples of 100</th>
         </thead>
         <tbody>
         <tr>
         <td>20-39 Gi</td>
         <td>100-1000 IOPS</td>
         </tr>
         <tr>
         <td>40-79 Gi</td>
         <td>100-2000 IOPS</td>
         </tr>
         <tr>
         <td>80-99 Gi</td>
         <td>100-4000 IOPS</td>
         </tr>
         <tr>
         <td>100-499 Gi</td>
         <td>100-6000 IOPS</td>
         </tr>
         <tr>
         <td>500-999 Gi</td>
         <td>100-10000 IOPS</td>
         </tr>
         <tr>
         <td>1000-1999 Gi</td>
         <td>100-20000 IOPS</td>
         </tr>
         <tr>
         <td>2000-2999 Gi</td>
         <td>200-40000 IOPS</td>
         </tr>
         <tr>
         <td>3000-3999 Gi</td>
         <td>200-48000 IOPS</td>
         </tr>
         <tr>
         <td>4000-7999 Gi</td>
         <td>300-48000 IOPS</td>
         </tr>
         <tr>
         <td>8000-9999 Gi</td>
         <td>500-48000 IOPS</td>
         </tr>
         <tr>
         <td>10000-12000 Gi</td>
         <td>1000-48000 IOPS</td>
         </tr>
         </tbody></table>

5. Choose if you want to keep your data after the cluster or the persistent volume claim (PVC) is deleted.
   - If you want to keep your data, then choose a `retain` storage class. When you delete the PVC, only the PVC is deleted. The PV, the physical storage device in your IBM Cloud infrastructure account, and your data still exist. To reclaim the storage and use it in your cluster again, you must remove the PV and follow the steps for [using existing block storage](#existing_block).
   - If you want the PV, the data, and your physical block storage device to be deleted when you delete the PVC, choose a storage class without `retain`.

6. Choose if you want to be billed hourly or monthly. Check the [pricing ![External link icon](../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/cloud/block-storage/pricing) for more information. By default, all block storage devices are provisioned with an hourly billing type.

<br />



## Adding block storage to apps
{: #add_block}

Create a persistent volume claim (PVC) to [dynamically provision](/docs/containers?topic=containers-kube_concepts#dynamic_provisioning) block storage for your cluster. Dynamic provisioning automatically creates the matching persistent volume (PV) and orders the actual storage device in your IBM Cloud infrastructure account.
{:shortdesc}

Block storage comes with a `ReadWriteOnce` access mode. You can mount it to only one pod on one worker node in the cluster at a time.
{: note}

Before you begin:
- If you have a firewall, [allow egress access](/docs/containers?topic=containers-firewall#pvc) for the IBM Cloud infrastructure IP ranges of the zones that your clusters are in so that you can create PVCs.
- Install the [{{site.data.keyword.cloud_notm}} block storage plug-in](#install_block).
- [Decide on a pre-defined storage class](#block_predefined_storageclass) or create a [customized storage class](#block_custom_storageclass).

Looking to deploy block storage in a stateful set? For more information, see [Using block storage in a stateful set](#block_statefulset).
{: tip}

To add block storage:

1.  Create a configuration file to define your persistent volume claim (PVC) and save the configuration as a `.yaml` file.

    -  **Example for bronze, silver, gold storage classes**:
       The following `.yaml` file creates a claim that is named `mypvc` of the `"ibmc-block-silver"` storage class, billed `"hourly"`, with a gigabyte size of `24Gi`.

       ```
       apiVersion: v1
       kind: PersistentVolumeClaim
       metadata:
         name: mypvc
         labels:
           billingType: "hourly"
	       region: us-south
           zone: dal13
       spec:
         accessModes:
           - ReadWriteOnce
         resources:
           requests:
             storage: 24Gi
	     storageClassName: ibmc-block-silver
       ```
       {: codeblock}

    -  **Example for using the custom storage class**:
       The following `.yaml` file creates a claim that is named `mypvc` of the storage class `ibmc-block-retain-custom`, billed `"hourly"`, with a gigabyte size of `45Gi` and IOPS of `"300"`.

       ```
       apiVersion: v1
       kind: PersistentVolumeClaim
       metadata:
         name: mypvc
         labels:
           billingType: "hourly"
	       region: us-south
           zone: dal13
       spec:
         accessModes:
           - ReadWriteOnce
         resources:
           requests:
             storage: 45Gi
             iops: "300"
	     storageClassName: ibmc-block-retain-custom
       ```
       {: codeblock}

       <table>
       <caption>Understanding the YAML file components</caption>
       <thead>
       <th colspan=2><img src="images/idea.png" alt="Idea icon"/> Understanding the YAML file components</th>
       </thead>
       <tbody>
       <tr>
       <td><code>metadata.name</code></td>
       <td>Enter the name of the PVC.</td>
       </tr>
       <tr>
         <td><code>metadata.labels.billingType</code></td>
         <td>Specify the frequency for which your storage bill is calculated, "monthly" or "hourly". The default is "hourly".</td>
       </tr>
       <tr>
       <td><code>metadata.labels.region</code></td>
       <td>Specify the region where you want to provision your block storage. If you specify the region, you must also specify a zone. If you do not specify a region, or the specified region is not found, the storage is created in the same region as your cluster. <p class="note">This option is supported only with the IBM Cloud Block Storage plug-in version 1.0.1 or higher. For older plug-in versions, if you have a multizone cluster, the zone in which your storage is provisioned is selected on a round-robin basis to balance volume requests evenly across all zones. To specify the zone for your storage, you can create a [customized storage class](#block_multizone_yaml) first. Then, create a PVC with your customized storage class.</p></td>
       </tr>
       <tr>
       <td><code>metadata.labels.zone</code></td>
	<td>Specify the zone where you want to provision your block storage. If you specify the zone, you must also specify a region. If you do not specify a zone or the specified zone is not found in a multizone cluster, the zone is selected on a round-robin basis. <p class="note">This option is supported only with the IBM Cloud Block Storage plug-in version 1.0.1 or higher. For older plug-in versions, if you have a multizone cluster, the zone in which your storage is provisioned is selected on a round-robin basis to balance volume requests evenly across all zones. To specify the zone for your storage, you can create a [customized storage class](#block_multizone_yaml) first. Then, create a PVC with your customized storage class.</p></td>
	</tr>
        <tr>
        <td><code>spec.resources.requests.storage</code></td>
        <td>Enter the size of the block storage, in gigabytes (Gi). After your storage is provisioned, you cannot change the size of your block storage. Make sure to specify a size that matches the amount of data that you want to store. </td>
        </tr>
        <tr>
        <td><code>spec.resources.requests.iops</code></td>
        <td>This option is available for the custom storage classes only (`ibmc-block-custom / ibmc-block-retain-custom`). Specify the total IOPS for the storage, selecting a multiple of 100 within the allowable range. If you choose an IOPS other than one that is listed, the IOPS is rounded up.</td>
        </tr>
	<tr>
	<td><code>spec.storageClassName</code></td>
	<td>The name of the storage class that you want to use to provision block storage. You can choose to use one of the [IBM-provided storage classes](#block_storageclass_reference) or [create your own storage class](#block_custom_storageclass). </br> If you do not specify a storage class, the PV is created with the default storage class <code>ibmc-file-bronze</code><p>**Tip:** If you want to change the default storage class, run <code>{[kubectl]} patch storageclass &lt;storageclass&gt; -p '{"metadata": {"annotations":{"storageclass.kubernetes.io/is-default-class":"true"}}}'</code> and replace <code>&lt;storageclass&gt;</code> with the name of the storage class.</p></td>
	</tr>
        </tbody></table>

    If you want to use a customized storage class, create your PVC with the corresponding storage class name, a valid IOPS, and size.   
    {: tip}

2.  Create the PVC.

    ```
    {[kubectl]} apply -f mypvc.yaml
    ```
    {: pre}

3.  Verify that your PVC is created and bound to the PV. This process can take a few minutes.

    ```
    {[kubectl]} describe pvc mypvc
    ```
    {: pre}

    Example output:

    ```
    Name:		mypvc
    Namespace:	default
    StorageClass:	""
    Status:		Bound
    Volume:		pvc-0d787071-3a67-11e7-aafc-eef80dd2dea2
    Labels:		<none>
    Capacity:	20Gi
    Access Modes:	RWO
    Events:
      FirstSeen	LastSeen	Count	From								SubObjectPath	Type		Reason			Message
      ---------	--------	-----	----								-------------	--------	------			-------
      3m		3m		1	{ibm.io/ibmc-block 31898035-3011-11e7-a6a4-7a08779efd33 }			Normal		Provisioning		External provisioner is provisioning volume for claim "default/my-persistent-volume-claim"
      3m		1m		10	{persistentvolume-controller }							Normal		ExternalProvisioning	cannot find provisioner "ibm.io/ibmc-block", expecting that a volume for the claim is provisioned either manually or via external software
      1m		1m		1	{ibm.io/ibmc-block 31898035-3011-11e7-a6a4-7a08779efd33 }			Normal		ProvisioningSucceeded	Successfully provisioned volume pvc-0d787071-3a67-11e7-aafc-eef80dd2dea2

    ```
    {: screen}

4.  {: #block_app_volume_mount}To mount the PV to your deployment, create a configuration `.yaml` file and specify the PVC that binds the PV.

    ```
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
    <th colspan=2><img src="images/idea.png" alt="Idea icon"/> Understanding the YAML file components</th>
    </thead>
    <tbody>
        <tr>
    <td><code>metadata.labels.app</code></td>
    <td>A label for the deployment.</td>
      </tr>
      <tr>
        <td><code>spec.selector.matchLabels.app</code> <br/> <code>spec.template.metadata.labels.app</code></td>
        <td>A label for your app.</td>
      </tr>
    <tr>
    <td><code>template.metadata.labels.app</code></td>
    <td>A label for the deployment.</td>
      </tr>
    <tr>
    <td><code>spec.containers.image</code></td>
    <td>The name of the image that you want to use. To list available images in your {{site.data.keyword.registryshort_notm}} account, run `ibmcloud cr image-list`.</td>
    </tr>
    <tr>
    <td><code>spec.containers.name</code></td>
    <td>The name of the container that you want to deploy to your cluster.</td>
    </tr>
    <tr>
    <td><code>spec.containers.volumeMounts.mountPath</code></td>
    <td>The absolute path of the directory to where the volume is mounted inside the container. Data that is written to the mount path is stored under the root directory in your physical block storage instance. If you want to share a volume between different apps, you can specify [volume sub paths ![External link icon](../icons/launch-glyph.svg "External link icon")](https://kubernetes.io/docs/concepts/storage/volumes/#using-subpath) for each of your apps. </td>
    </tr>
    <tr>
    <td><code>spec.containers.volumeMounts.name</code></td>
    <td>The name of the volume to mount to your pod.</td>
    </tr>
    <tr>
    <td><code>volumes.name</code></td>
    <td>The name of the volume to mount to your pod. Typically this name is the same as <code>volumeMounts/name</code>.</td>
    </tr>
    <tr>
    <td><code>volumes.persistentVolumeClaim.claimName</code></td>
    <td>The name of the PVC that binds the PV that you want to use. </td>
    </tr>
    </tbody></table>

5.  Create the deployment.
     ```
     {[kubectl]} apply -f <local_yaml_path>
     ```
     {: pre}

6.  Verify that the PV is successfully mounted.

     ```
     {[kubectl]} describe deployment <deployment_name>
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

<br />




## Using existing block storage in your cluster
{: #existing_block}

If you have an existing physical storage device that you want to use in your cluster, you can manually create the PV and PVC to [statically provision](/docs/containers?topic=containers-kube_concepts#static_provisioning) the storage.
{: shortdesc}

Before you can start to mount your existing storage to an app, you must retrieve all necessary information for your PV.  

### Step 1: Retrieving the information of your existing block storage
{: #existing-block-1}

1.  Retrieve or generate an API key for your IBM Cloud infrastructure account.
    1. Log in to the [IBM Cloud infrastructure portal ![External link icon](../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/classic?).
    2. Select **Account**, then **Users**, and then **User List**.
    3. Find your user ID.
    4. In the **API KEY** column, click **Generate** to generate an API key or **View** to view your existing API key.
2.  Retrieve the API user name for your IBM Cloud infrastructure account.
    1. From the **User List** menu, select your user ID.
    2. In the **API Access Information** section, find your **API Username**.
3.  Log in to the IBM Cloud infrastructure CLI plug-in.
    ```
    ibmcloud sl init
    ```
    {: pre}

4.  Choose to authenticate by using the user name and API key for your IBM Cloud infrastructure account.
5.  Enter the user name and API key that you retrieved in the previous steps.
6.  List available block storage devices.
    ```
    ibmcloud sl block volume-list
    ```
    {: pre}

    Example output:
    ```
    id         username            datacenter   storage_type              capacity_gb   bytes_used   ip_addr         lunId   active_transactions
    38642141   IBM02SEL1543159-1   dal10        endurance_block_storage   20            -            169.xx.xxx.xxx   170     0
    ```
    {: screen}

7.  Note the `id`, `ip_addr`, `capacity_gb`, the `datacenter`, and `lunId` of the block storage device that you want to mount to your cluster. **Note:** To mount existing storage to a cluster, you must have a worker node in the same zone as your storage. To verify the zone of your worker node, run `ibmcloud ks workers --cluster <cluster_name_or_ID>`.

### Step 2: Creating a persistent volume (PV) and a matching persistent volume claim (PVC)
{: #existing-block-2}

1.  Optional: If you have storage that you provisioned with a `retain` storage class, when you remove the PVC, the PV and the physical storage device are not removed. To reuse the storage in your cluster, you must remove the PV first.
    1. List existing PVs.
       ```
       {[kubectl]} get pv
       ```
       {: pre}

       Look for the PV that belongs to your persistent storage. The PV is in a `released` state.

    2. Remove the PV.
       ```
       {[kubectl]} delete pv <pv_name>
       ```
       {: pre}

    3. Verify that the PV is removed.
       ```
       {[kubectl]} get pv
       ```
       {: pre}

2.  Create a configuration file for your PV. Include the block storage `id`, `ip_addr`, `capacity_gb`, the `datacenter`, and `lunIdID` that you retrieved earlier.

    ```
    apiVersion: v1
    kind: PersistentVolume
    metadata:
      name: mypv
      labels:
         failure-domain.beta.kubernetes.io/region: <region>
         failure-domain.beta.kubernetes.io/zone: <zone>
    spec:
      capacity:
        storage: "<storage_size>"
      accessModes:
        - ReadWriteOnce
      flexVolume:
        driver: "ibm/ibmc-block"
        fsType: "<fs_type>"
        options:
          "Lun": "<lun_ID>"
          "TargetPortal": "<IP_address>"
          "VolumeID": "<volume_ID>"
          "volumeName": "<volume_name>"
      ```
      {: codeblock}

    <table>
    <caption>Understanding the YAML file components</caption>
    <thead>
    <th colspan=2><img src="images/idea.png" alt="Idea icon"/> Understanding the YAML file components</th>
    </thead>
    <tbody>
    <tr>
    <td><code>metadata.name</code></td>
    <td>Enter the name of the PV that you want to create.</td>
    </tr>
    <tr>
    <td><code>metadata.labels</code></td>
    <td>Enter the region and the zone that you retrieved earlier. You must have at least one worker node in the same region and zone as your persistent storage to mount the storage in your cluster. If a PV for your storage already exists, [add the zone and region label](/docs/containers?topic=containers-kube_concepts#storage_multizone) to your PV.
    </tr>
    <tr>
    <td><code>spec.flexVolume.fsType</code></td>
    <td>Enter the file system type that is configured for your existing block storage. Choose between <code>ext4</code> or <code>xfs</code>. If you do not specify this option, the PV defaults to <code>ext4</code>. When the wrong `fsType` is defined, then the PV creation succeeds, but the mounting of the PV to a pod fails. </td></tr>	    
    <tr>
    <td><code>spec.capacity.storage</code></td>
    <td>Enter the storage size of the existing block storage that you retrieved in the previous step as <code>capacity-gb</code>. The storage size must be written in gigabytes, for example, 20Gi (20 GB) or 1000Gi (1 TB).</td>
    </tr>
    <tr>
    <td><code>flexVolume.options.Lun</code></td>
    <td>Enter the lun ID for your block storage that you retrieved earlier as <code>lunId</code>.</td>
    </tr>
    <tr>
    <td><code>flexVolume.options.TargetPortal</code></td>
    <td>Enter the IP address of your block storage that you retrieved earlier as <code>ip_addr</code>. </td>
    </tr>
    <tr>
	    <td><code>flexVolume.options.VolumeId</code></td>
	    <td>Enter the ID of your block storage that you retrieved earlier as <code>id</code>.</td>
	    </tr>
	    <tr>
		    <td><code>flexVolume.options.volumeName</code></td>
		    <td>Enter a name for your volume.</td>
	    </tr>
    </tbody></table>

3.  Create the PV in your cluster.
    ```
    {[kubectl]} apply -f mypv.yaml
    ```
    {: pre}

4. Verify that the PV is created.
    ```
    {[kubectl]} get pv
    ```
    {: pre}

5. Create another configuration file to create your PVC. In order for the PVC to match the PV that you created earlier, you must choose the same value for `storage` and `accessMode`. The `storage-class` field must be empty. If any of these fields do not match the PV, then a new PV is created automatically instead.

     ```
     kind: PersistentVolumeClaim
     apiVersion: v1
     metadata:
      name: mypvc
     spec:
      accessModes:
        - ReadWriteOnce
      resources:
        requests:
          storage: "<storage_size>"
      storageClassName:
     ```
     {: codeblock}

6.  Create your PVC.
     ```
     {[kubectl]} apply -f mypvc.yaml
     ```
     {: pre}

7.  Verify that your PVC is created and bound to the PV that you created earlier. This process can take a few minutes.
     ```
     {[kubectl]} describe pvc mypvc
     ```
     {: pre}

     Example output:

     ```
     Name: mypvc
     Namespace: default
     StorageClass:	""
     Status: Bound
     Volume: pvc-0d787071-3a67-11e7-aafc-eef80dd2dea2
     Labels: <none>
     Capacity: 20Gi
     Access Modes: RWO
     Events:
       FirstSeen LastSeen Count From        SubObjectPath Type Reason Message
       --------- -------- ----- ----        ------------- -------- ------ -------
       3m 3m 1 {ibm.io/ibmc-block 31898035-3011-11e7-a6a4-7a08779efd33 } Normal Provisioning External provisioner is provisioning volume  for claim "default/my-persistent-volume-claim"
       3m 1m	 10 {persistentvolume-controller } Normal ExternalProvisioning cannot find provisioner "ibm.io/ibmc-block", expecting that  a volume for the claim is provisioned either manually or via external software
       1m 1m 1 {ibm.io/ibmc-block 31898035-3011-11e7-a6a4-7a08779efd33 } Normal ProvisioningSucceeded	Successfully provisioned volume  pvc-0d787071-3a67-11e7-aafc-eef80dd2dea2
     ```
     {: screen}

You successfully created a PV and bound it to a PVC. Cluster users can now [mount the PVC](#block_app_volume_mount) to their deployments and start reading from and writing to the PV.

<br />



## Using block storage in a stateful set
{: #block_statefulset}

If you have a stateful app such as a database, you can create stateful sets that use block storage to store your app's data. Alternatively, you can use an {{site.data.keyword.cloud_notm}} database-as-a-service and store your data in the cloud.
{: shortdesc}

**What do I need to be aware of when adding block storage to a stateful set?** </br>
To add storage to a stateful set, you specify your storage configuration in the `volumeClaimTemplates` section of your stateful set YAML. The `volumeClaimTemplates` is the basis for your PVC and can include the storage class and the size or IOPS of your block storage that you want to provision. However, if you want to include labels in your `volumeClaimTemplates`, Kubernetes does not include these labels when creating the PVC. Instead, you must add the labels directly to your stateful set.

You cannot deploy two stateful sets at the same time. If you try to create a stateful set before a different one is fully deployed, then the deployment of your stateful set might lead to unexpected results.
{: important}

**How can I create my stateful set in a specific zone?** </br>
In a multizone cluster, you can specify the zone and region where you want to create your stateful set in the `spec.selector.matchLabels` and `spec.template.metadata.labels` section of your stateful set YAML. Alternatively, you can add those labels to a [customized storage class](/docs/containers?topic=containers-kube_concepts#customized_storageclass) and use this storage class in the `volumeClaimTemplates` section of your stateful set.

**Can I delay binding of a PV to my stateful pod until the pod is ready?**<br>
Yes, you can [create a custom storage class](#topology_yaml) for your PVC that includes the [`volumeBindingMode: WaitForFirstConsumer` ![External link icon](../icons/launch-glyph.svg "External link icon")](https://kubernetes.io/docs/concepts/storage/storage-classes/#volume-binding-mode) field.

**What options do I have to add block storage to a stateful set?** </br>
If you want to automatically create your PVC when you create the stateful set, use [dynamic provisioning](#block_dynamic_statefulset). You can also choose to [pre-provision your PVCs or use existing PVCs](#block_static_statefulset) with your stateful set.  

### Dynamic provisioning: Creating the PVC when you create a stateful set
{: #block_dynamic_statefulset}

Use this option if you want to automatically create the PVC when you create the stateful set.
{: shortdesc}

Before you begin: [Log in to your account. If applicable, target the appropriate resource group. Set the context for your cluster.](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure)

1. Verify that all existing stateful sets in your cluster are fully deployed. If a stateful set is still being deployed, you cannot start creating your stateful set. You must wait until all stateful sets in your cluster are fully deployed to avoid unexpected results.
   1. List existing stateful sets in your cluster.
      ```
      {[kubectl]} get statefulset --all-namespaces
      ```
      {: pre}

      Example output:
      ```
      NAME              DESIRED   CURRENT   AGE
      mystatefulset     3         3         6s
      ```
      {: screen}

   2. View the **Pods Status** of each stateful set to ensure that the deployment of the stateful set is finished.  
      ```
      {[kubectl]} describe statefulset <statefulset_name>
      ```
      {: pre}

      Example output:
      ```
      Name:               nginx
      Namespace:          default
      CreationTimestamp:  Fri, 05 Oct 2018 13:22:41 -0400
      Selector:           app=nginx,billingType=hourly,region=us-south,zone=dal10
      Labels:             app=nginx
                          billingType=hourly
                          region=us-south
                          zone=dal10
      Annotations:        {[kubectl]}.kubernetes.io/last-applied-configuration={"apiVersion":"apps/v1","kind":"StatefulSet","metadata":{"annotations":{},"name":"nginx","namespace":"default"},"spec":{"podManagementPolicy":"Par...
      Replicas:           3 desired | 3 total
      Pods Status:        0 Running / 3 Waiting / 0 Succeeded / 0 Failed
      Pod Template:
        Labels:  app=nginx
                 billingType=hourly
                 region=us-south
                 zone=dal10
      ...
      ```
      {: screen}

      A stateful set is fully deployed when the number of replicas that you find in the **Replicas** section of your CLI output equals the number of **Running** pods in the **Pods Status** section. If a stateful set is not fully deployed yet, wait until the deployment is finished before you proceed.

2. Create a configuration file for your stateful set and the service that you use to expose the stateful set.

   - **Example stateful set that specifies a zone:**

     The following example shows how to deploy NGINX as a stateful set with three replicas. For each replica, a 20 gigabyte block storage device is provisioned based on the specifications that are defined in the `ibmc-block-retain-bronze` storage class. All storage devices are provisioned in the `dal10` zone. Because block storage cannot be accessed from other zones, all replicas of the stateful set are also deployed onto worker nodes that are located in `dal10`.

     ```
     apiVersion: v1
     kind: Service
     metadata:
      name: nginx
      labels:
        app: nginx
     spec:
      ports:
      - port: 80
        name: web
      clusterIP: None
      selector:
        app: nginx
     ---
     apiVersion: apps/v1
     kind: StatefulSet
     metadata:
      name: nginx
     spec:
      serviceName: "nginx"
      replicas: 3
      podManagementPolicy: Parallel
      selector:
        matchLabels:
          app: nginx
          billingType: "hourly"
          region: "us-south"
          zone: "dal10"
      template:
        metadata:
          labels:
            app: nginx
            billingType: "hourly"
            region: "us-south"
            zone: "dal10"
        spec:
          containers:
          - name: nginx
            image: k8s.gcr.io/nginx-slim:0.8
            ports:
            - containerPort: 80
              name: web
            volumeMounts:
            - name: myvol
              mountPath: /usr/share/nginx/html
      volumeClaimTemplates:
      - metadata:
          name: myvol
        spec:
          accessModes:
          - ReadWriteOnce
          resources:
            requests:
              storage: 20Gi
              iops: "300" #required only for performance storage
	      storageClassName: ibmc-block-retain-bronze
     ```
     {: codeblock}

   - **Example stateful set with anti-affinity rule and delayed block storage creation:**

     The following example shows how to deploy NGINX as a stateful set with three replicas. The stateful set does not specify the region and zone where the block storage is created. Instead, the stateful set uses an anti-affinity rule to ensure that the pods are spread across worker nodes and zones. By defining `topologykey: failure-domain.beta.kubernetes.io/zone`, the Kubernetes scheduler cannot schedule a pod on a worker node if the worker node is in the same zone as a pod that has the `app: nginx` label. For each stateful set pod, two PVCs are created as defined in the `volumeClaimTemplates` section, but the creation of the block storage instances is delayed until a stateful set pod that uses the storage is scheduled. This setup is referred to as [topology-aware volume scheduling](https://kubernetes.io/blog/2018/10/11/topology-aware-volume-provisioning-in-kubernetes/).

     ```
     apiVersion: storage.k8s.io/v1
     kind: StorageClass
     metadata:
       name: ibmc-block-bronze-delayed
     parameters:
       billingType: hourly
       classVersion: "2"
       fsType: ext4
       iopsPerGB: "2"
       sizeRange: '[20-12000]Gi'
       type: Endurance
     provisioner: ibm.io/ibmc-block
     reclaimPolicy: Delete
     volumeBindingMode: WaitForFirstConsumer
     ---
     apiVersion: v1
     kind: Service
     metadata:
       name: nginx
       labels:
         app: nginx
     spec:
       ports:
       - port: 80
         name: web
       clusterIP: None
       selector:
         app: nginx
     ---
     apiVersion: apps/v1
     kind: StatefulSet
     metadata:
       name: web
     spec:
       serviceName: "nginx"
       replicas: 3
       podManagementPolicy: "Parallel"
       selector:
         matchLabels:
           app: nginx
       template:
         metadata:
           labels:
             app: nginx
         spec:
           affinity:
             podAntiAffinity:
               preferredDuringSchedulingIgnoredDuringExecution:
               - weight: 100
                 podAffinityTerm:
                   labelSelector:
                     matchExpressions:
                     - key: app
                       operator: In
                       values:
                       - nginx
                   topologyKey: failure-domain.beta.kubernetes.io/zone
           containers:
           - name: nginx
             image: k8s.gcr.io/nginx-slim:0.8
             ports:
             - containerPort: 80
               name: web
             volumeMounts:
             - name: myvol1
               mountPath: /usr/share/nginx/html
             - name: myvol2
               mountPath: /tmp1
       volumeClaimTemplates:
       - metadata:
           name: myvol1
         spec:
           accessModes:
           - ReadWriteOnce # access mode
           resources:
             requests:
               storage: 20Gi
	       storageClassName: ibmc-block-bronze-delayed
       - metadata:
           name: myvol2
         spec:
           accessModes:
           - ReadWriteOnce # access mode
           resources:
             requests:
               storage: 20Gi
	       storageClassName: ibmc-block-bronze-delayed
     ```
     {: codeblock}

     <table>
     <caption>Understanding the stateful set YAML file components</caption>
     <thead>
     <th colspan=2><img src="images/idea.png" alt="Idea icon"/> Understanding the stateful set YAML file components</th>
     </thead>
     <tbody>
     <tr>
     <td style="text-align:left"><code>metadata.name</code></td>
     <td style="text-align:left">Enter a name for your stateful set. The name that you enter is used to create the name for your PVC in the format: <code>&lt;volume_name&gt;-&lt;statefulset_name&gt;-&lt;replica_number&gt;</code>. </td>
     </tr>
     <tr>
     <td style="text-align:left"><code>spec.serviceName</code></td>
     <td style="text-align:left">Enter the name of the service that you want to use to expose your stateful set. </td>
     </tr>
     <tr>
     <td style="text-align:left"><code>spec.replicas</code></td>
     <td style="text-align:left">Enter the number of replicas for your stateful set. </td>
     </tr>
     <tr>
     <td style="text-align:left"><code>spec.podManagementPolicy</code></td>
     <td style="text-align:left">Enter the pod management policy that you want to use for your stateful set. Choose between the following options: <ul><li><strong>`OrderedReady`: </strong>With this option, stateful set replicas are deployed one after another. For example, if you specified three replicas, then Kubernetes creates the PVC for your first replica, waits until the PVC is bound, deploys the stateful set replica, and mounts the PVC to the replica. After the deployment is finished, the second replica is deployed. For more information about this option, see [`OrderedReady` Pod Management ![External link icon](../icons/launch-glyph.svg "External link icon")](https://kubernetes.io/docs/concepts/workloads/controllers/statefulset/#orderedready-pod-management). </li><li><strong>Parallel: </strong>With this option, the deployment of all stateful set replicas is started at the same time. If your app supports parallel deployment of replicas, then use this option to save deployment time for your PVCs and stateful set replicas. </li></ul></td>
     </tr>
     <tr>
     <td style="text-align:left"><code>spec.selector.matchLabels</code></td>
     <td style="text-align:left">Enter all labels that you want to include in your stateful set and your PVC. Labels that you include in the <code>volumeClaimTemplates</code> of your stateful set are not recognized by Kubernetes. Sample labels that you might want to include are: <ul><li><code><strong>region</strong></code> and <code><strong>zone</strong></code>: If you want all your stateful set replicas and PVCs to be created in one specific zone, add both labels. You can also specify the zone and region in the storage class that you use. If you do not specify a zone and region and you have a multizone cluster, the zone in which your storage is provisioned is selected on a round-robin basis to balance volume requests evenly across all zones.</li><li><code><strong>billingType</strong></code>: Enter the billing type that you want to use for your PVCs. Choose between <code>hourly</code> or <code>monthly</code>. If you do not specify this label, all PVCs are created with an hourly billing type. </li></ul></td>
     </tr>
     <tr>
     <td style="text-align:left"><code>spec.template.metadata.labels</code></td>
     <td style="text-align:left">Enter the same labels that you added to the <code>spec.selector.matchLabels</code> section. </td>
     </tr>
     <tr>
     <td style="text-align:left"><code>spec.template.spec.affinity</code></td>
     <td style="text-align:left">Specify your anti-affinity rule to ensure that your stateful set pods are distributed across worker nodes and zones. The example shows an anti-affinity rule where the stateful set pod prefers not to be scheduled on a worker node where a pod runs that has the `app: nginx` label. The `topologykey: failure-domain.beta.kubernetes.io/zone` restricts this anti-affinity rule even more and prevents the pod to be scheduled on a worker node if the worker node is in the same zone as a pod that has the `app: nginx` label. By using this anti-affinity rule, you can achieve anti-affinity across worker nodes and zones. </td>
     </tr>
     <tr>
     <td style="text-align:left"><code>spec.volumeClaimTemplates.metadata.name</code></td>
     <td style="text-align:left">Enter a name for your volume. Use the same name that you defined in the <code>spec.containers.volumeMount.name</code> section. The name that you enter here is used to create the name for your PVC in the format: <code>&lt;volume_name&gt;-&lt;statefulset_name&gt;-&lt;replica_number&gt;</code>. </td>
     </tr>
     <tr>
     <td style="text-align:left"><code>spec.volumeClaimTemplates.spec.resources.</code></br><code>requests.storage</code></td>
     <td style="text-align:left">Enter the size of the block storage in gigabytes (Gi).</td>
     </tr>
     <tr>
     <td style="text-align:left"><code>spec.volumeClaimTemplates.spec.resources.</code></br><code>requests.iops</code></td>
     <td style="text-align:left">If you want to provision [performance storage](#block_predefined_storageclass), enter the number of IOPS. If you use an endurance storage class and specify a number of IOPS, the number of IOPS is ignored. Instead, the IOPS that is specified in your storage class is used.  </td>
     </tr>
     <tr>
     <td style="text-align:left"><code>spec.volumeClaimTemplates.</code></br><code>spec.storageClassName</code></td>
     <td style="text-align:left">Enter the storage class that you want to use. To list existing storage classes, run <code>{[kubectl]} get storageclasses | grep block</code>. If you do not specify a storage class, the PVC is created with the default storage class that is set in your cluster. Make sure that the default storage class uses the <code>ibm.io/ibmc-block</code> provisioner so that your stateful set is provisioned with block storage.</td>
     </tr>
     </tbody></table>

4. Create your stateful set.
   ```
   {[kubectl]} apply -f statefulset.yaml
   ```
   {: pre}

5. Wait for your stateful set to be deployed.
   ```
   {[kubectl]} describe statefulset <statefulset_name>
   ```
   {: pre}

   To see the current status of your PVCs, run `{[kubectl]} get pvc`. The name of your PVC is formatted as `<volume_name>-<statefulset_name>-<replica_number>`.
   {: tip}

### Static provisioning: Using existing PVCs with a stateful set
{: #block_static_statefulset}

You can pre-provision your PVCs before creating your stateful set or use existing PVCs with your stateful set.
{: shortdesc}

When you [dynamically provision your PVCs when creating the stateful set](#block_dynamic_statefulset), the name of the PVC is assigned based on the values that you used in the stateful set YAML file. In order for the stateful set to use existing PVCs, the name of your PVCs must match the name that would automatically be created when using dynamic provisioning.

Before you begin: [Log in to your account. If applicable, target the appropriate resource group. Set the context for your cluster.](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure)

1. If you want to pre-provision the PVC for your stateful set before you create the stateful set, follow steps 1-3 in [Adding block storage to apps](#add_block) to create a PVC for each stateful set replica. Make sure that you create your PVC with a name that follows the following format: `<volume_name>-<statefulset_name>-<replica_number>`.
   - **`<volume_name>`**: Use the name that you want to specify in the `spec.volumeClaimTemplates.metadata.name` section of your stateful set, such as `nginxvol`.
   - **`<statefulset_name>`**: Use the name that you want to specify in the `metadata.name` section of your stateful set, such as `nginx_statefulset`.
   - **`<replica_number>`**: Enter the number of your replica, starting with 0.

   For example, if you must create three stateful set replicas, create three PVCs with the following names: `nginxvol-nginx_statefulset-0`, `nginxvol-nginx_statefulset-1`, and `nginxvol-nginx_statefulset-2`.  

   Looking to create a PVC and PV for an existing storage device? Create your PVC and PV by using [static provisioning](#existing_block).

2. Follow the steps in [Dynamic provisioning: Creating the PVC when you create a stateful set](#block_dynamic_statefulset) to create your stateful set. The name of your PVC follows the format `<volume_name>-<statefulset_name>-<replica_number>`. Make sure to use the following values from your PVC name in the stateful set specification:
   - **`spec.volumeClaimTemplates.metadata.name`**: Enter the `<volume_name>` of your PVC name.
   - **`metadata.name`**: Enter the `<statefulset_name>` of your PVC name.
   - **`spec.replicas`**: Enter the number of replicas that you want to create for your stateful set. The number of replicas must equal the number of PVCs that you created earlier.

   If your PVCs are in different zones, do not include a region or zone label in your stateful set.
   {: note}

3. Verify that the PVCs are used in your stateful set replica pods.
   1. List the pods in your cluster. Identify the pods that belong to your stateful set.
      ```
      {[kubectl]} get pods
      ```
      {: pre}

   2. Verify that your existing PVC is mounted to your stateful set replica. Review the **`ClaimName`** in the **`Volumes`** section of your CLI output.
      ```
      {[kubectl]} describe pod <pod_name>
      ```
      {: pre}

      Example output:
      ```
      Name:           nginx-0
      Namespace:      default
      Node:           10.xxx.xx.xxx/10.xxx.xx.xxx
      Start Time:     Fri, 05 Oct 2018 13:24:59 -0400
      ...
      Volumes:
        myvol:
          Type:       PersistentVolumeClaim (a reference to a PersistentVolumeClaim in the same namespace)
          ClaimName:  myvol-nginx-0
     ...
      ```
      {: screen}

<br />


## Changing the size and IOPS of your existing storage device
{: #block_change_storage_configuration}

If you want to increase storage capacity or performance, you can modify your existing volume.
{: shortdesc}

For questions about billing and to find the steps for how to use the {{site.data.keyword.cloud_notm}} console to modify your storage, see [Expanding Block Storage capacity](/docs/infrastructure/BlockStorage?topic=BlockStorage-expandingcapacity#expandingcapacity) and [Adjusting IOPS](/docs/infrastructure/BlockStorage?topic=BlockStorage-adjustingIOPS). Updates that you make from the console are not reflected in the persistent volume (PV). To add this information to the PV, run `{[kubectl]} patch pv <pv_name>` and manually update the size and IOPS in the **Labels** and **Annotation** section of your PV.
{: tip}

1. List the PVCs in your cluster and note the name of the associated PV from the **VOLUME** column.
   ```
   {[kubectl]} get pvc
   ```
   {: pre}

   Example output:
   ```
   NAME             STATUS    VOLUME                                     CAPACITY   ACCESS MODES   STORAGECLASS        AGE
   myvol            Bound     pvc-01ac123a-123b-12c3-abcd-0a1234cb12d3   20Gi       RWO            ibmc-block-bronze    147d
   ```
   {: screen}

2. If you want to change the IOPS and the size for your block storage, edit the IOPS in the `metadata.labels.IOPS` section of your PV first. You can change to a lower or greater IOPS value. Make sure that you enter an IOPS that is supported for the storage type that you have. For example, if you have endurance block storage with 4 IOPS, you can change the IOPS to either 2 or 10. For more supported IOPS values, see [Deciding on your block storage configuration](/docs/containers?topic=containers-block_storage#block_predefined_storageclass).
   ```
   {[kubectl]} edit pv <pv_name>
   ```
   {: pre}

   To change the IOPS from the CLI, you must also change the size of your block storage. If you want to change only the IOPS, but not the size, you must [request the IOPS change from the console](/docs/infrastructure/BlockStorage?topic=BlockStorage-adjustingIOPS).
   {: note}

3. Edit the PVC and add the new size in the `spec.resources.requests.storage` section of your PVC. You can change to a greater size only up to the maximum capacity that is set by your storage class. You cannot downsize your existing storage. To see available sizes for your storage class, see [Deciding on the block storage configuration](/docs/containers?topic=containers-block_storage#block_predefined_storageclass).
   ```
   {[kubectl]} edit pvc <pvc_name>
   ```
   {: pre}

4. Verify that the volume expansion is requested. The volume expansion is successfully requested when you see a `FileSystemResizePending` message in the **Conditions** section of your CLI output. 
   ```
   {[kubectl]} describe pvc <pvc_name>
   ```
   {: pre}

   Example output:
   ```
   ...
   Conditions:
   Type                      Status  LastProbeTime                     LastTransitionTime                Reason  Message
   ----                      ------  -----------------                 ------------------                ------  -------
   FileSystemResizePending   True    Mon, 01 Jan 0001 00:00:00 +0000   Thu, 25 Apr 2019 15:52:49 -0400           Waiting for user to (re-)start a pod to finish file system resize of volume on node.
   ```
   {: screen}

5. List all the pods that mount the PVC. If your PVC is mounted by a pod, the volume expansion is automatically processed. If your PVC is not mounted by a pod, you must mount the PVC to a pod so that the volume expansion can be processed. 
   ```
   {[kubectl]} get pods --all-namespaces -o=jsonpath='{range .items[*]}{"\n"}{.metadata.name}{":\t"}{range .spec.volumes[*]}{.persistentVolumeClaim.claimName}{" "}{end}{end}' | grep "<pvc_name>"
   ```
   {: pre}

   Mounted pods are returned in the format: `<pod_name>: <pvc_name>`.

6. If your PVC is not mounted by a pod, [create a pod or deployment and mount the PVC](/docs/containers?topic=containers-block_storage#add_block). If your PVC is mounted by a pod, continue with the next step. 

7. Monitor the volume expansion status. The volume expansion is complete when you see the `"message":"Success"` message in your CLI output.
   ```
   {[kubectl]} get pv <pv_name> -o go-template=$'{{index .metadata.annotations "ibm.io/volume-expansion-status"}}\n'
   ```
   {: pre}

   Example output:
   ```
   {"size":50,"iops":500,"orderid":38832711,"start":"2019-04-30T17:00:37Z","end":"2019-04-30T17:05:27Z","status":"complete","message":"Success"}
   ```
   {: screen}

8. Verify that the size and IOPS are changed in the **Labels** section of your CLI output.
   ```
   {[kubectl]} describe pv <pv_name>
   ```
   {: pre}

   Example output:
   ```
   ...
   Labels:       CapacityGb=50
                 Datacenter=dal10
                 IOPS=500
   ```
   {: screen}


## Backing up and restoring data
{: #block_backup_restore}

Block storage is provisioned into the same location as the worker nodes in your cluster. The storage is hosted on clustered servers by IBM to provide availability in case a server goes down. However, block storage is not backed up automatically and might be inaccessible if the entire location fails. To protect your data from being lost or damaged, you can set up periodic backups that you can use to restore your data when needed.
{: shortdesc}

Review the following backup and restore options for your block storage:

<dl>
  <dt>Set up periodic snapshots</dt>
  <dd><p>You can [set up periodic snapshots for your block storage](/docs/infrastructure/BlockStorage?topic=BlockStorage-snapshots#snapshots), which is a read-only image that captures the state of the instance at a point in time. To store the snapshot, you must request snapshot space on your block storage. Snapshots are stored on the existing storage instance within the same zone. You can restore data from a snapshot if a user accidentally removes important data from the volume.</br></br> <strong>To create a snapshot for your volume: </strong><ol><li>[Log in to your account. If applicable, target the appropriate resource group. Set the context for your cluster.](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure)</li><li>Log in to the `ibmcloud sl` CLI. <pre class="pre"><code>ibmcloud sl init</code></pre></li><li>List existing PVs in your cluster. <pre class="pre"><code>{[kubectl]} get pv</code></pre></li><li>Get the details for the PV for which you want to create snapshot space and note the volume ID, the size, and the IOPS. <pre class="pre"><code>{[kubectl]} describe pv &lt;pv_name&gt;</code></pre> The size and IOPS are shown in the <strong>Labels</strong> section of your CLI output. To find the volume ID, review the <code>ibm.io/network-storage-id</code> annotation of your CLI output. </li><li>Create the snapshot size for your existing volume with the parameters that you retrieved in the previous step. <pre class="pre"><code>ibmcloud sl block snapshot-order &lt;volume_ID&gt; --size &lt;size&gt; --tier &lt;iops&gt;</code></pre></li><li>Wait for the snapshot size to create. <pre class="pre"><code>ibmcloud sl block volume-detail &lt;volume_ID&gt;</code></pre>The snapshot size is successfully provisioned when the <strong>Snapshot Size (GB)</strong> in your CLI output changes from 0 to the size that you ordered. </li><li>Create the snapshot for your volume and note the ID of the snapshot that is created for you. <pre class="pre"><code>ibmcloud sl block snapshot-create &lt;volume_ID&gt;</code></pre></li><li>Verify that the snapshot is created successfully. <pre class="pre"><code>ibmcloud sl block snapshot-list &lt;volume_ID&gt;</code></pre></li></ol></br><strong>To restore data from a snapshot to an existing volume: </strong><pre class="pre"><code>ibmcloud sl block snapshot-restore &lt;volume_ID&gt; &lt;snapshot_ID&gt;</code></pre></p></dd>
  <dt>Replicate snapshots to another zone</dt>
 <dd><p>To protect your data from a zone failure, you can [replicate snapshots](/docs/infrastructure/BlockStorage?topic=BlockStorage-replication#replication) to a block storage instance that is set up in another zone. Data can be replicated from the primary storage to the backup storage only. You cannot mount a replicated block storage instance to a cluster. When your primary storage fails, you can manually set your replicated backup storage to be the primary one. Then, you can mount it to your cluster. After your primary storage is restored, you can restore the data from the backup storage.</p></dd>
 <dt>Duplicate storage</dt>
 <dd><p>You can [duplicate your block storage instance](/docs/infrastructure/BlockStorage?topic=BlockStorage-duplicatevolume#duplicatevolume) in the same zone as the original storage instance. A duplicate has the same data as the original storage instance at the point in time that you create the duplicate. Unlike replicas, use the duplicate as an independent storage instance from the original. To duplicate, first set up snapshots for the volume.</p></dd>
  <dt>Back up data to {{site.data.keyword.cos_full}}</dt>
  <dd><p>You can use the [**ibm-backup-restore image**](/docs/services/RegistryImages/ibm-backup-restore?topic=RegistryImages-ibmbackup_restore_starter#ibmbackup_restore_starter) to spin up a backup and restore pod in your cluster. This pod contains a script to run a one-time or periodic backup for any persistent volume claim (PVC) in your cluster. Data is stored in your {{site.data.keyword.cos_full}} instance that you set up in a zone.</p><p class="note">Block storage is mounted with an RWO access mode. This access allows only one pod to be mounted to the block storage at a time. To back up your data, you must unmount the app pod from the storage, mount it to your backup pod, back up the data, and remount the storage to your app pod. </p>
To make your data even more highly available and protect your app from a zone failure, set up a second {{site.data.keyword.cos_short}} instance and replicate data across zones. If you need to restore data from your {{site.data.keyword.cos_short}} instance, use the restore script that is provided with the image.</dd>
<dt>Copy data to and from pods and containers</dt>
<dd><p>You can use the `{[kubectl]} cp` [command![External link icon](../icons/launch-glyph.svg "External link icon")](https://kubernetes.io/docs/reference/kubectl/overview/#cp) to copy files and directories to and from pods or specific containers in your cluster.</p>
<p>Before you begin: [Log in to your account. If applicable, target the appropriate resource group. Set the context for your cluster.](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure) If you do not specify a container with <code>-c</code>, the command uses to the first available container in the pod.</p>
<p>You can use the command in various ways:</p>
<ul>
<li>Copy data from your local machine to a pod in your cluster: <pre class="pre"><code>{[kubectl]} cp <var>&lt;local_filepath&gt;/&lt;filename&gt;</var> <var>&lt;namespace&gt;/&lt;pod&gt;:&lt;pod_filepath&gt;</var></code></pre></li>
<li>Copy data from a pod in your cluster to your local machine: <pre class="pre"><code>{[kubectl]} cp <var>&lt;namespace&gt;/&lt;pod&gt;:&lt;pod_filepath&gt;/&lt;filename&gt;</var> <var>&lt;local_filepath&gt;/&lt;filename&gt;</var></code></pre></li>
<li>Copy data from your local machine to a specific container that runs in a pod in your cluster: <pre class="pre"><code>{[kubectl]} cp <var>&lt;local_filepath&gt;/&lt;filename&gt;</var> <var>&lt;namespace&gt;/&lt;pod&gt;:&lt;pod_filepath&gt;</var> -c <var>&lt;container&gt;</var></code></pre></li>
</ul></dd>
  </dl>

<br />


## Storage class reference
{: #block_storageclass_reference}

### Bronze
{: #block_bronze}

<table>
<caption>Block storage class: bronze</caption>
<thead>
<th>Characteristics</th>
<th>Setting</th>
</thead>
<tbody>
<tr>
<td>Name</td>
<td><code>ibmc-block-bronze</code></br><code>ibmc-block-retain-bronze</code></td>
</tr>
<tr>
<td>Type</td>
<td>[Endurance storage](/docs/infrastructure/BlockStorage?topic=BlockStorage-About#provendurance)</td>
</tr>
<tr>
<td>File system</td>
<td>ext4</td>
</tr>
<tr>
<td>IOPS per gigabyte</td>
<td>2</td>
</tr>
<tr>
<td>Size range in gigabytes</td>
<td>20-12000 Gi</td>
</tr>
<tr>
<td>Hard disk</td>
<td>SSD</td>
</tr>
<tr>
<td>Billing</td>
<td>The default billing type depends on the version of your {{site.data.keyword.cloud_notm}} Block Storage plug-in: <ul><li> Version 1.0.1 and higher: Hourly</li><li>Version 1.0.0 and lower: Monthly</li></ul></td>
</tr>
<tr>
<td>Pricing</td>
<td>[Pricing information![External link icon](../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/cloud/block-storage/pricing)</td>
</tr>
</tbody>
</table>


### Silver
{: #block_silver}

<table>
<caption>Block storage class: silver</caption>
<thead>
<th>Characteristics</th>
<th>Setting</th>
</thead>
<tbody>
<tr>
<td>Name</td>
<td><code>ibmc-block-silver</code></br><code>ibmc-block-retain-silver</code></td>
</tr>
<tr>
<td>Type</td>
<td>[Endurance storage](/docs/infrastructure/BlockStorage?topic=BlockStorage-About#provendurance)</td>
</tr>
<tr>
<td>File system</td>
<td>ext4</td>
</tr>
<tr>
<td>IOPS per gigabyte</td>
<td>4</td>
</tr>
<tr>
<td>Size range in gigabytes</td>
<td>20-12000 Gi</td>
</tr>
<tr>
<td>Hard disk</td>
<td>SSD</td>
</tr>
<tr>
<td>Billing</td>
<td>The default billing type depends on the version of your {{site.data.keyword.cloud_notm}} Block Storage plug-in: <ul><li> Version 1.0.1 and higher: Hourly</li><li>Version 1.0.0 and lower: Monthly</li></ul></td>
</tr>
<tr>
<td>Pricing</td>
<td>[Pricing information![External link icon](../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/cloud/block-storage/pricing)</td>
</tr>
</tbody>
</table>

### Gold
{: #block_gold}

<table>
<caption>Block storage class: gold</caption>
<thead>
<th>Characteristics</th>
<th>Setting</th>
</thead>
<tbody>
<tr>
<td>Name</td>
<td><code>ibmc-block-gold</code></br><code>ibmc-block-retain-gold</code></td>
</tr>
<tr>
<td>Type</td>
<td>[Endurance storage](/docs/infrastructure/BlockStorage?topic=BlockStorage-About#provendurance)</td>
</tr>
<tr>
<td>File system</td>
<td>ext4</td>
</tr>
<tr>
<td>IOPS per gigabyte</td>
<td>10</td>
</tr>
<tr>
<td>Size range in gigabytes</td>
<td>20-4000 Gi</td>
</tr>
<tr>
<td>Hard disk</td>
<td>SSD</td>
</tr>
<tr>
<td>Billing</td>
<td>The default billing type depends on the version of your {{site.data.keyword.cloud_notm}} Block Storage plug-in: <ul><li> Version 1.0.1 and higher: Hourly</li><li>Version 1.0.0 and lower: Monthly</li></ul></td>
</tr>
<tr>
<td>Pricing</td>
<td>[Pricing information![External link icon](../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/cloud/block-storage/pricing)</td>
</tr>
</tbody>
</table>

### Custom
{: #block_custom}

<table>
<caption>Block storage class: custom</caption>
<thead>
<th>Characteristics</th>
<th>Setting</th>
</thead>
<tbody>
<tr>
<td>Name</td>
<td><code>ibmc-block-custom</code></br><code>ibmc-block-retain-custom</code></td>
</tr>
<tr>
<td>Type</td>
<td>[Performance](/docs/infrastructure/BlockStorage?topic=BlockStorage-About#provperformance)</td>
</tr>
<tr>
<td>File system</td>
<td>ext4</td>
</tr>
<tr>
<td>IOPS and size</td>
<td><strong>Size range in gigabytes / IOPS range in multiples of 100</strong><ul><li>20-39 Gi / 100-1000 IOPS</li><li>40-79 Gi / 100-2000 IOPS</li><li>80-99 Gi / 100-4000 IOPS</li><li>100-499 Gi / 100-6000 IOPS</li><li>500-999 Gi / 100-10000 IOPS</li><li>1000-1999 Gi / 100-20000 IOPS</li><li>2000-2999 Gi / 200-40000 IOPS</li><li>3000-3999 Gi / 200-48000 IOPS</li><li>4000-7999 Gi / 300-48000 IOPS</li><li>8000-9999 Gi / 500-48000 IOPS</li><li>10000-12000 Gi / 1000-48000 IOPS</li></ul></td>
</tr>
<tr>
<td>Hard disk</td>
<td>The IOPS to gigabyte ratio determines the type of hard disk that is provisioned. To determine your IOPS to gigabyte ratio, you divide the IOPS by the size of your storage. </br></br>Example: </br>You chose 500Gi of storage with 100 IOPS. Your ratio is 0.2 (100 IOPS/500Gi). </br></br><strong>Overview of hard disk types per ratio:</strong><ul><li>Less than or equal to 0.3: SATA</li><li>Greater than 0.3: SSD</li></ul></td>
</tr>
<tr>
<td>Billing</td>
<td>The default billing type depends on the version of your {{site.data.keyword.cloud_notm}} Block Storage plug-in: <ul><li> Version 1.0.1 and higher: Hourly</li><li>Version 1.0.0 and lower: Monthly</li></ul></td>
</tr>
<tr>
<td>Pricing</td>
<td>[Pricing information![External link icon](../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/cloud/block-storage/pricing)</td>
</tr>
</tbody>
</table>

<br />


## Sample customized storage classes
{: #block_custom_storageclass}

You can create a customized storage class and use the storage class in your PVC.
{: shortdesc}

{{site.data.keyword.containerlong_notm}} provides [pre-defined storage classes](#block_storageclass_reference) to provision block storage with a particular tier and configuration. In some cases, you might want to provision storage with a different configuration that is not covered in the pre-defined storage classes. You can use the examples in this topic to find sample customized storage classes.

To create your customized storage class, see [Customizing a storage class](/docs/containers?topic=containers-kube_concepts#customized_storageclass). Then, [use your customized storage class in your PVC](#add_block).

### Creating topology-aware storage
{: #topology_yaml}

To use block storage in a multizone cluster, your pod must be scheduled in the same zone as your block storage instance so that you can read and write to the volume. Before topology-aware volume scheduling was introduced by Kubernetes, the dynamic provisioning of your storage automatically created the block storage instance when a PVC was created. Then, when you created your pod, the Kubernetes scheduler tried to deploy the pod to the same data center as your block storage instance.
{: shortdesc}

Creating the block storage instance without knowing the constraints of the pod can lead to unwanted results. For example, your pod might not be able to be scheduled to the same worker node as your storage because the worker node has insufficient resources or the worker node is tainted and does not allow the pod to be scheduled. With topology-aware volume scheduling, the block storage instance is delayed until the first pod that uses the storage is created.

Topology-aware volume scheduling is supported on clusters that run Kubernetes version 1.12 or later only. To use this feature, make sure that you installed the {{site.data.keyword.cloud_notm}} Block Storage plug-in version 1.2.0 or later.
{: note}

The following examples show how to create storage classes that delay the creation of the block storage instance until the first pod that uses this storage is ready to be scheduled. To delay the creation, you must include the `volumeBindingMode: WaitForFirstConsumer` option. If you do not include this option, the `volumeBindingMode` is automatically set to `Immediate` and the block storage instance is created when you create the PVC.

- **Example for Endurance block storage:**
  ```
  apiVersion: storage.k8s.io/v1
  kind: StorageClass
  metadata:
    name: ibmc-block-bronze-delayed
  parameters:
    billingType: hourly
    classVersion: "2"
    fsType: ext4
    iopsPerGB: "2"
    sizeRange: '[20-12000]Gi'
    type: Endurance
  provisioner: ibm.io/ibmc-block
  reclaimPolicy: Delete
  volumeBindingMode: WaitForFirstConsumer
  ```
  {: codeblock}

- **Example for Performance block storage:**
  ```
  apiVersion: storage.k8s.io/v1
  kind: StorageClass
  metadata:
   name: ibmc-block-performance-storageclass
   labels:
     kubernetes.io/cluster-service: "true"
  provisioner: ibm.io/ibmc-block
  parameters:
   billingType: "hourly"
   classVersion: "2"
   sizeIOPSRange: |-
     "[20-39]Gi:[100-1000]"
     "[40-79]Gi:[100-2000]"
     "[80-99]Gi:[100-4000]"
     "[100-499]Gi:[100-6000]"
     "[500-999]Gi:[100-10000]"
     "[1000-1999]Gi:[100-20000]"
     "[2000-2999]Gi:[200-40000]"
     "[3000-3999]Gi:[200-48000]"
     "[4000-7999]Gi:[300-48000]"
     "[8000-9999]Gi:[500-48000]"
     "[10000-12000]Gi:[1000-48000]"
   type: "Performance"
  reclaimPolicy: Delete
  volumeBindingMode: WaitForFirstConsumer
  ```
  {: codeblock}

### Specifying the zone and region
{: #block_multizone_yaml}

If you want to create your block storage in a specific zone, you can specify the zone and region in a customized storage class.
{: shortdesc}

Use the customized storage class if you use the {{site.data.keyword.cloud_notm}} Block Storage plug-in version 1.0.0 or if you want to [statically provision block storage](#existing_block) in a specific zone. In all other cases, [specify the zone directly in your PVC](#add_block).
{: note}

The following `.yaml` file customizes a storage class that is based on the `ibm-block-silver` non-retaining storage class: the `type` is `"Endurance"`, the `iopsPerGB` is `4`, the `sizeRange` is `"[20-12000]Gi"`, and the `reclaimPolicy` is set to `"Delete"`. The zone is specified as `dal12`. To use a different storage class as your base, see the [storage class reference](#block_storageclass_reference).

Create the storage class in the same region and zone as your cluster and worker nodes. To get the region of your cluster, run `ibmcloud ks cluster-get --cluster <cluster_name_or_ID>` and look for the region prefix in the **Master URL**, such as `eu-de` in `https://c2.eu-de.containers.cloud.ibm.com:11111`. To get the zone of your worker node, run `ibmcloud ks workers --cluster <cluster_name_or_ID>`.

- **Example for Endurance block storage:**
  ```
  apiVersion: storage.k8s.io/v1
  kind: StorageClass
  metadata:
    name: ibmc-block-silver-mycustom-storageclass
    labels:
      kubernetes.io/cluster-service: "true"
  provisioner: ibm.io/ibmc-block
  parameters:
    zone: "dal12"
    region: "us-south"
    type: "Endurance"
    iopsPerGB: "4"
    sizeRange: "[20-12000]Gi"
  reclaimPolicy: "Delete"
  ```
  {: codeblock}

- **Example for Performance block storage:**
  ```
  apiVersion: storage.k8s.io/v1
  kind: StorageClass
  metadata:
    name: ibmc-block-performance-storageclass
    labels:
      kubernetes.io/cluster-service: "true"
  provisioner: ibm.io/ibmc-block
  parameters:
    zone: "dal12"
    region: "us-south"
    type: "Performance"
    sizeIOPSRange: |-
      "[20-39]Gi:[100-1000]"
      "[40-79]Gi:[100-2000]"
      "[80-99]Gi:[100-4000]"
      "[100-499]Gi:[100-6000]"
      "[500-999]Gi:[100-10000]"
      "[1000-1999]Gi:[100-20000]"
      "[2000-2999]Gi:[200-40000]"
      "[3000-3999]Gi:[200-48000]"
      "[4000-7999]Gi:[300-48000]"
      "[8000-9999]Gi:[500-48000]"
      "[10000-12000]Gi:[1000-48000]"
  reclaimPolicy: "Delete"
  ```
  {: codeblock}

### Mounting block storage with an `XFS` file system
{: #xfs}

The following examples create a storage class that provisions block storage with an `XFS` file system.
{: shortdesc}

- **Example for Endurance block storage:**
  ```
  apiVersion: storage.k8s.io/v1
  kind: StorageClass
  metadata:
    name: ibmc-block-custom-xfs
    labels:
      addonmanager.kubernetes.io/mode: Reconcile
  provisioner: ibm.io/ibmc-block
  parameters:
    type: "Endurance"
    iopsPerGB: "4"
    sizeRange: "[20-12000]Gi"
    fsType: "xfs"
  reclaimPolicy: "Delete"
  ```

- **Example for Performance block storage:**
  ```
  apiVersion: storage.k8s.io/v1
  kind: StorageClass
  metadata:
    name: ibmc-block-custom-xfs
    labels:
      addonmanager.kubernetes.io/mode: Reconcile
  provisioner: ibm.io/ibmc-block
  parameters:
    type: "Performance"
    sizeIOPSRange: |-
      [20-39]Gi:[100-1000]
      [40-79]Gi:[100-2000]
      [80-99]Gi:[100-4000]
      [100-499]Gi:[100-6000]
      [500-999]Gi:[100-10000]
      [1000-1999]Gi:[100-20000]
      [2000-2999]Gi:[200-40000]
      [3000-3999]Gi:[200-48000]
      [4000-7999]Gi:[300-48000]
      [8000-9999]Gi:[500-48000]
      [10000-12000]Gi:[1000-48000]
    fsType: "xfs"
  reclaimPolicy: "Delete"
  classVersion: "2"
  ```
  {: codeblock}

<br />



