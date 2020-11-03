---

copyright:
  years: 2014, 2020
lastupdated: "2020-11-03"

keywords: openshift, roks, rhoks, rhos

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




# Storing data on {{site.data.keyword.block_storage_is_short}} (Gen 1 and Gen 2 compute)
{: #vpc-block}

[{{site.data.keyword.block_storage_is_full}} (Gen 1 and Gen 2 compute)](/docs/vpc?topic=vpc-block-storage-about#vpc-storage-encryption) provides hypervisor-mounted, high-performance data storage for your virtual server instances that you can provision within a VPC.
{: shortdesc}

You can choose between predefined storage tiers with GB sizes and IOPS that meet the requirements of your workloads. To find out if {{site.data.keyword.block_storage_is_short}} is the right storage option for you, see [Choosing a storage solution](/docs/openshift?topic=openshift-storage_planning#choose_storage_solution). For pricing information, see [Pricing for {{site.data.keyword.block_storage_is_short}}](https://www.ibm.com/cloud/vpc/pricing).

The {{site.data.keyword.block_storage_is_short}} add-on is installed and enabled by default on VPC clusters. You can enable or disable the add-on by using the [`addon enable`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_cluster_addon_enable) or [`addon disable`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_cluster_addon_disable) command in the CLI.
{: note}

## Quickstart for {{site.data.keyword.cloud_notm}} {{site.data.keyword.block_storage_is_short}}
{: #vpc_block_qs}

In this quickstart guide, you create a 10Gi 5IOPS tier {{site.data.keyword.block_storage_is_short}} volume in your cluster by creating a PVC to dynamically provision the volume. Then, you create an app deployment that mounts your PVC.
{: shortdesc}

1. Create a file for your PVC and name it `pvc.yaml`.

  ```yaml
  apiVersion: v1
  kind: PersistentVolumeClaim
  metadata:
    name: my-pvc
  spec:
    accessModes:
    - ReadWriteOnce
    resources:
      requests:
        storage: 10Gi
    storageClassName: ibmc-vpc-block-5iops-tier
  ```
  {: codeblock}

2. Create the PVC in your cluster.
  ```sh
  oc apply -f pvc.yaml
  ```
  {: pre}

3. After your PVC is bound, create an app deployment that uses your PVC. Create a file for your deployment and name it `deployment.yaml`.

  ```yaml
  apiVersion: apps/v1
  kind: Deployment
  metadata:
    name: my-deployment
    labels:
      app:
  spec:
    selector:
      matchLabels:
        app: my-app
    template:
      metadata:
        labels:
          app: my-app
      spec:
        containers:
        - image: # Your contanerized app image.
          name: my-container
          volumeMounts:
          - name: my-volume
            mountPath: /mount-path
        volumes:
        - name: my-volume
          persistentVolumeClaim:
            claimName: my-pvc
  ```
  {: codeblock}

3. Create the deployment in your cluster.
  ```sh
  oc apply -f deployment.yaml
  ```
  {: pre}

For more information, see:
  * [Adding {{site.data.keyword.block_storage_is_short}} to apps](#vpc-block-add).
  * [Storage class reference](#vpc-block-reference).
  * [Customizing the default storage settings](#vpc-customize-default).

## Adding {{site.data.keyword.block_storage_is_short}} to your apps
{: #vpc-block-add}

Choose your {{site.data.keyword.block_storage_is_short}} profile and create a persistent volume claim to dynamically provision {{site.data.keyword.block_storage_is_short}} for your cluster. Dynamic provisioning automatically creates the matching persistent volume and orders the physical storage device in your {{site.data.keyword.cloud_notm}} account.
{: shortdesc}

1. Decide on the [{{site.data.keyword.block_storage_is_short}} profile](/docs/vpc?topic=vpc-block-storage-profiles) that best meets the capacity and performance requirements that you want.

2. Select the corresponding storage class for your {{site.data.keyword.block_storage_is_short}} profile.

   All IBM pre-defined storage classes set up {{site.data.keyword.block_storage_is_short}} with an `ext4` file system by default. If you want to use a different file system, such as `xfs` or `ext3`, [create a customized storage class](#vpc-block-xfs).
   {: note}

   <table summary="The columns are read from left to right. The first column has the storage profile. The second column describes the corresponding storage class for the profile.">
   <caption>Overview of {{site.data.keyword.block_storage_is_short}} profiles</caption>
   <thead>
     <th>{{site.data.keyword.block_storage_is_short}} profile</th>
     <th>Corresponding storage class</th>
   </thead>
   <tbody>
   <tr>
    <td> 10 IOPS/GB </td>
    <td> <code>ibmc-vpc-block-10iops-tier</code></br><code>ibmc-vpc-block-retain-10iops-tier</code></td>
    </tr>
    <tr>
   <td>5 IOPS/GB </td>
   <td><code>ibmc-vpc-block-5iops-tier</code></br><code>ibmc-vpc-block-retain-5iops-tier</code></td>
   </tr>
   <tr>
   <td>3 IOPS/GB </td>
   <td><code>ibmc-vpc-block-general-purpose</code></br><code>ibmc-vpc-block-retain-general-purpose</code></td>
   </tr>
   <tr>
   <td> Custom </td>
   <td> <code>ibmc-vpc-block-custom</code></br><code>ibmc-vpc-block-retain-custom</code></td>
   </tr>
   </tbody>
   </table>

3. Decide on your {{site.data.keyword.block_storage_is_short}} configuration.
   1. Choose a size for your storage. Make sure that the size is supported by the {{site.data.keyword.block_storage_is_short}} profile that you chose.
   2. Choose if you want to keep your data after the cluster or the persistent volume claim (PVC) is deleted.
      - If you want to keep your data, then choose a `retain` storage class. When you delete the PVC, only the PVC is deleted. The persistent volume (PV), the physical storage device in your {{site.data.keyword.cloud_notm}} account, and your data still exist. To reclaim the storage and use it in your cluster again, you must remove the PV and follow the steps for using existing {{site.data.keyword.block_storage_is_short}}.
      - If you want the PV, the data, and your physical {{site.data.keyword.block_storage_is_short}} device to be deleted when you delete the PVC, choose a storage class without `retain`.

4. Create a configuration file to define your persistent volume claim and save the configuration as a YAML file.
   ```yaml
   apiVersion: v1
   kind: PersistentVolumeClaim
   metadata:
     name: <pvc_name>
   spec:
     accessModes:
     - ReadWriteOnce
     resources:
       requests:
         storage: <size>
     storageClassName: <storage_class>
   ```
   {: codeblock}

   <table summary="The columns are read from left to right. The first column has the parameter of the YAML file. The second column describes the parameter.">
   <caption>Understanding the YAML file components</caption>
   <col width="25%">
   <thead>
    <th>Component</th>
    <th>Description</th>
   </thead>
   <tbody>
   <tr>
   <td><code>name</code></td>
   <td>Enter a name for your PVC.</td>
   </tr>
   <tr>
   <td><code>accessMode</code></td>
   <td>{{site.data.keyword.block_storage_is_short}} supports a `ReadWriteOnce` access mode only. You can mount the PVC to one pod on one worker node in the cluster at a time.</td>
   </tr>
   <tr>
   <td><code>storage</code></td>
   <td>Enter the size of the {{site.data.keyword.block_storage_is_short}} instance, in gigabytes (Gi). Make sure that the size is supported in the {{site.data.keyword.block_storage_is_short}} profile that you chose. For example, if you want 10 gigabyte of {{site.data.keyword.blockstorageshort}}, enter `10Gi`.  </td>
   </tr>
   <tr>
   <td><code>storageClassName</code></td>
   <td>Enter the storage class name that you selected earlier.</td>
   </tr>
   </tbody>
   </table>

5. Create the PVC in your cluster.
   ```
   oc apply -f pvc.yaml
   ```
   {: pre}

6. Verify that your PVC is created and bound to the PV. This process can take a few minutes.
   ```
   oc describe pvc <pvc_name>
   ```
   {: pre}

   Example output:
   ```
   Name:          mypvv
   Namespace:     default
   StorageClass:  ibmc-vpc-block-5iops-tier
   Status:        Bound
   Volume:        
   Labels:        <none>
   Annotations:   oc.kubernetes.io/last-applied-configuration:
                 {"apiVersion":"v1","kind":"PersistentVolumeClaim","metadata":{"annotations":{},"name":"csi-block-pvc-good","namespace":"default"},"spec":{...
               volume.beta.kubernetes.io/storage-provisioner: vpc.block.csi.ibm.io
   Finalizers:    [kubernetes.io/pvc-protection]
   Capacity: 10Gi   
   Access Modes:  
   VolumeMode:    Filesystem
   Events:
     Type       Reason                Age               From                         Message
     ----       ------                ----              ----                         -------
     Normal     ExternalProvisioning  9s (x3 over 18s)  persistentvolume-controller  waiting for a volume to be created, either by external provisioner "vpc.block.csi.ibm.io" or manually created by system administrator
   Mounted By:  <none>
   ```
   {: screen}

7. Create a deployment configuration file for your app and mount the PVC to your app.
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
           volumeMounts:
           - name: <volume_name>
             mountPath: /<file_path>
         volumes:
         - name: <volume_name>
           persistentVolumeClaim:
             claimName: <pvc_name>
   ```
   {: codeblock}

   <table summary="The columns are read from left to right. The first column has the parameter of the YAML file. The second column describes the parameter.">
   <caption>Understanding the YAML file components</caption>
   <col width="25%">
   <thead>
    <th>Component</th>
    <th>Description</th>
   </thead>
   <tbody>
   <tr>
   <td><code>labels.app</code></td>
   <td>In the metadata section, enter a label for the deployment.</td>
   </tr>
   <tr>
   <td><code>matchLabels.app</code> <br/> <code>labels.app</code></td>
   <td>In the spec selector and template metadata sections, enter a label for your app.</td>
   </tr>
   <tr>
   <td><code>image</code></td>
   <td>Specify the name of the container image that you want to use. To list available images in your {{site.data.keyword.registrylong_notm}} account, run `ibmcloud cr image-list`.</td>
   </tr>
   <tr>
   <td><code>name</code></td>
   <td>Specify the name of the container that you want to deploy in your pod.</td>
   </tr>
   <tr>
   <td><code>mountPath</code></td>
   <td>In the container volume mounts section, specify the absolute path of the directory to where the PVC is mounted inside the container.  </td>
   </tr>
   <tr>
   <td><code>name</code></td>
   <td>In the container volume mounts section, enter the name of the volume to mount to your pod. You can enter any name that you want. </td>
   </tr>
   <tr>
   <td><code>name</code></td>
   <td>In the volumes section, enter the name of the volume to mount to your pod. Typically this name is the same as <code>volumeMounts.name</code>.</td>
   </tr>
   <tr>
   <td><code>claimName</code></td>
   <td>In the volumes persistent volume claim section, enter the name of the PVC that you created earlier. </td>
   </tr>
   </tbody></table>

8. Create the deployment in your cluster.
   ```
   oc apply -f deployment.yaml
   ```
   {: pre}

9. Verify that the PVC is successfully mounted to your app. It might take a few minutes for your pods to get into a **Running** state.

   During the deployment of your app, you might see intermittent `Unable to mount volumes` errors in the **Events** section of your CLI output. The {{site.data.keyword.block_storage_is_short}} add-on automatically retries mounting the storage to your apps. Wait a few more minutes for the storage to mount to your app.
   {: tip}

   ```
   oc describe deployment <deployment_name>
   ```
   {: pre}

   Example output:
   ```
   ...
   Volumes:
   myvol:
     Type:    PersistentVolumeClaim (a reference to a PersistentVolumeClaim in the same namespace)
     ClaimName:    mypvc
     ReadOnly:    false
   ```
   {: screen}

   <br />

## Using an existing {{site.data.keyword.block_storage_is_short}} instance
{: #vpc-block-static}

If you have an existing physical {{site.data.keyword.block_storage_is_short}} device that you want to use in your cluster, you can manually create the PV and PVC to statically provision the storage.
{: shortdesc}


You can attach a volume to one worker node only. Make sure that the volume is in the same zone as the worker node for the attachment to succeed.
{: note}

1. Determine the volume that you want to attach to a worker node in your VPC cluster. Note the **volume ID**.
  ```
  ibmcloud is volumes
  ```
  {: pre}

2. List the details of your volume. Note the **Size**, **Zone**, and **IOPS**. These values are used to create your PV.
  ```
  ibmcloud is volume <volume_id>
  ```
  {: pre}

3. Retrieve a list of worker nodes in your VPC cluster. Note the **Zone** of the worker node that is in the same zone as your storage volume.
  ```
  ibmcloud oc worker ls <cluster_name>
  ```
  {: pre}

4. Optional: If you provisioned your physical {{site.data.keyword.block_storage_is_short}} instance by using a `retain` storage class, the PV and the physical storage is not removed when you remove the PVC. To use your physical {{site.data.keyword.block_storage_is_short}} device in your cluster, you must remove the existing PV first.  

   1. List the PVs in your cluster and look for the PV that belongs to your {{site.data.keyword.block_storage_is_short}} device. The PV is in a `released` state.
      ```
      oc get pv
      ```
      {: pre}

   2. Remove the PV.
      ```
      oc delete pv <pv_name>
      ```
      {: pre}

5.  Create a configuration file for your PV. Include the **ID**, **Size**, **Zone**, and **IOPS** that you retrieved earlier.

    ```yaml
    apiVersion: v1
    kind: PersistentVolume
    metadata:
      name: <pv_name> # Example: my-persistent-volume
    spec:
      accessModes:
      - ReadWriteOnce
      capacity:
        storage: <vpc_block_storage_size> # Example: 20Gi
      csi:
        driver: vpc.block.csi.ibm.io
        fsType: ext4
        volumeAttributes:
          iops: "<vpc_block_storage_iops>" # Example: "3000"
          volumeId: <vpc_block_storage_ID> # Example: a1a11a1a-a111-1111-1a11-1111a11a1a11
          zone: "<vpc_block_zone>" # Example: "eu-de-3"
        volumeHandle: <vpc_block_storage_ID>
      nodeAffinity:
        required:
          nodeSelectorTerms:
          - matchExpressions:
            - key: failure-domain.beta.kubernetes.io/zone
              operator: In
              values:
              - <worker_node_zone> # Example: eu-de-3
            - key: failure-domain.beta.kubernetes.io/region
              operator: In
              values:
              - <worker_node_region> # Example: eu-de
      persistentVolumeReclaimPolicy: Retain
      storageClassName: ""
      volumeMode: Filesystem
    ```
    {: codeblock}

    <table summary="The columns are read from left to right. The first column has the parameter of the YAML file. The second column describes the parameter.">
   <caption>Understanding the YAML file components</caption>
   <col width="25%">
   <thead>
    <th>Component</th>
    <th>Description</th>
   </thead>
   <tbody>
   <tr>
   <td><code>name</code></td>
   <td>In the metadata section, enter a name for your PV. </td>
   </tr>
   <tr>
      <td><code>storage</code></td>
   <td>In the spec capacity section, enter the size of your {{site.data.keyword.blockstorageshort}} volume in gigabytes (Gi) that you retrieved earlier. For example, if the size of your device is 100 GB, enter <code>100Gi</code>.  </td>
   </tr>
   <tr>
   <td><code>iops</code></td>
   <td>In the spec CSI volume attributes section, enter the Max IOPS of the {{site.data.keyword.blockstorageshort}} volume that you retrieved earlier.</td>
   </tr>
   <tr>
   <td><code>zone</code></td>
   <td>In the spec CSI volume attributes section, enter the VPC block zone that matches the location that you retrieved earlier. For example, if your location is **Washington DC-1**, then use `us-east-1` as your zone. To list available zones, run `ibmcloud is zones`. To find an overview of available VPC zones and locations, see [Creating a VPC in a different region](/docs/vpc?topic=vpc-creating-a-vpc-in-a-different-region).</td>
   </tr>
   <tr>
   <td><code>volumeId</code></br><code>spec.csi.volumeHandle</code></td>
   <td>In the spec CSI volume attributes section, enter the ID of the {{site.data.keyword.blockstorageshort}} volume that you retrieved earlier. </td>
   </tr>
   <tr>
   <td><code>storageClassName</code></td>
   <td>For the spec storage class name, enter an empty string.</td>
   </tr>
   <tr>
   <td><code>matchExpressions</code></td>
   <td>In the spec node affinity section, enter the node selector terms to match the zone. For the key, enter <code>failure-domain.beta.kubernetes.io/zone</code>. For the value, enter the zone of your worker node where you want to attach storage.</td>
   </tr>
   <td><code>matchExpressions</code></td>
   <td>In the spec node affinity section, enter the node selector terms to match the region. For the key, enter <code>failure-domain.beta.kubernetes.io/region</code>. For the value, enter the region of the worker node where you want to attach storage.</td>
   </tr>
   </tbody>
   </table>

6. Create the PV in your cluster.
   ```
   oc apply -f pv.yaml
   ```
   {: pre}

7. Verify that the PV is created in your cluster.
   ```
   oc get pv
   ```
   {: pre}

8. Create another configuration file for your PVC. In order for the PVC to match the PV that you created earlier, you must choose the same value for the storage size and access mode. In your storage class field, enter an empty string value to match your PV. If any of these fields do not match the PV, then a new PV and a {{site.data.keyword.blockstorageshort}} instance are created automatically via dynamic provisioning.
   ```yaml
   apiVersion: v1
   kind: PersistentVolumeClaim
   metadata:
     name: <pvc_name>
   spec:
     accessModes:
     - ReadWriteOnce
     resources:
       requests:
         storage: <vpc_block_storage_size>
     storageClassName: ""
   ```
   {: codeblock}

8. Create your PVC.
   ```
   oc apply -f pvc.yaml
   ```
   {: pre}

9. Verify that your PVC is created and bound to the PV that you created earlier. This process can take a few minutes.
   ```
   oc describe pvc <pvc_name>
   ```
   {: pre}

10. Create a deployment or a pod that uses your PVC.

<br />

## Updating the {{site.data.keyword.block_storage_is_short}} add-on
{: #vpc-addon-update}

You can update the {{site.data.keyword.block_storage_is_short}} add-on by disabling and re-enabling the add-on in your cluster.
{: shortdesc}

1. Check to see if an update is available. If an update is available, the plug-in version is flagged with an asterisk and the latest version is shown. Note the latest version as this value is used later.
  ```
  ibmcloud oc cluster addons --cluster <cluster_name_or_ID>
  ```
  {: pre}

  Example output:
  ```
  Name                   Version                 Health State   Health Status   
  vpc-block-csi-driver   1.0.0* (2.0.0 latest)   normal         Addon Ready
  ```
  {: screen}

2. Disable the {{site.data.keyword.block_storage_is_short}} add-on.
  ```
  ibmcloud oc cluster addon disable vpc-block-csi-driver --cluster <cluster_name_or_ID> -f
  ```
  {: pre}

  Example Output
  ```
  Disabling add-on vpc-block-csi-driver for cluster <cluster_name_or_ID>...
  OK
  ```
  {: screen}

2. Verify that the add-on is disabled. If the add-on is disabled it does not appear in the list of add-ons in your cluster. The add-on might still display in your list of add-ons for a few minutes after running the `disable` command.
  ```
  ibmcloud oc cluster addon ls --cluster <cluster_name_or_ID>
  ```
  {: pre}

3. Re-enable the add-on and specify the latest version that you retrieved earlier.
  ```
  ibmcloud oc cluster addon enable vpc-block-csi-driver --version <version> --cluster <cluster_name_or_ID>
  ```
  {: pre}

  Example Output
  ```
  Enabling add-on vpc-block-csi-driver(2.0.0) for cluster <cluster_name_or_ID>...
  OK
  ```
  {: screen}

4. Verify that the add-on is in the `Addon Ready` state. The add-on might take a few minutes to become ready.
  ```
  ibmcloud oc cluster addon ls --cluster <cluster_name_or_ID>
  ```
  {: pre}

  Example Output
  ```
  Name                   Version   Health State   Health Status   
  vpc-block-csi-driver   2.0.0     normal         Addon Ready
  ```
  {: screen}

## Setting up encryption for {{site.data.keyword.block_storage_is_short}}
{: #vpc-block-encryption}

Use {{site.data.keyword.keymanagementservicelong}} to create a private root key that you use in your {{site.data.keyword.block_storage_is_short}} instance to encrypt data as it is written to the storage. After you create the private root key, create a custom storage class or a Kubernetes secret with your root key and then use this storage class or secret to provision your {{site.data.keyword.block_storage_is_short}} instance.
{: shortdesc}

1.  [Create a {{site.data.keyword.keymanagementserviceshort}} service instance](/docs/key-protect?topic=key-protect-provision#provision).

2.  [Create a root key](/docs/key-protect?topic=key-protect-create-root-keys#create-root-keys). By default, the root key is created without an expiration date.

3. Retrieve the service CRN for your root key.
   1. From the {{site.data.keyword.keymanagementserviceshort}} details page, select the **Manage** tab to find the list of your keys.
   2. Find the root key that you created and from the actions menu, click **View CRN**.
   3. Note the CRN of your root key.

4. Authorize {{site.data.keyword.block_storage_is_short}} to access {{site.data.keyword.keymanagementservicelong}}.
   1. From the {{site.data.keyword.cloud_notm}} menu, select **Manage** > **Access (IAM)**.
   2. From the menu, select **Authorizations**.
   3. Click **Create**.
   4. Select **Cloud {{site.data.keyword.blockstorageshort}}** as your source service.
   5. Select **Key Protect** as your target service.
   6. Select the **Reader** service access role and click **Authorize**.

5. [Decide if you want to store the {{site.data.keyword.keymanagementserviceshort}} root key CRN in a customized storage class or in a Kubernetes secret](/docs/openshift?topic=openshift-vpc-block#vpc-customize-default). Then, follow the steps to create a customized storage class or a Kubernetes secret.

   **Example customized storage class**:
   ```yaml
   apiVersion: storage.k8s.io/v1
   kind: StorageClass
   metadata:
     name: <storage_class_name>
   provisioner: vpc.block.csi.ibm.io
   parameters:
     profile: "5iops-tier"
     sizeRange: "[10-2000]GiB"
     csi.storage.k8s.io/fstype: "ext4"
     billingType: "hourly"
     encrypted: "true"
     encryptionKey: "<encryption_key>"
     resourceGroup: ""
     zone: ""
     tags: ""
     generation: "gc"
     classVersion: "1"
   reclaimPolicy: "Delete"
   ```
   {: codeblock}

   <table summary="The columns are read from left to right. The first column has the parameter of the YAML file. The second column describes the parameter.">
    <caption>Understanding the YAML file components</caption>
    <col width="25%">
    <thead>
    <th>Component</th>
    <th>Description</th>
    </thead>
    <tbody>
    <tr>
    <td><code>name</code></td>
    <td>Enter a name for your storage class.</td>
    </tr>
    <tr>
    <td><code>encrypted</code></td>
    <td>In the parameters, enter <strong>true</strong> to create a storage class that sets up encryption for your {{site.data.keyword.blockstorageshort}} volumes. If you set this option to <strong>true</strong>, you must provide the root key CRN of your {{site.data.keyword.keymanagementserviceshort}} service instance that you want to use in <code>parameters.encryptionKey</code>.</td>
    </tr>
    <tr>
    <td><code>encryptionKey</code></td>
    <td>In the parameters, enter the root key CRN that you retrieved earlier.</td>
    </tr>
    </tbody>
    </table>

    **Example Kubernetes secret**:
    ```yaml
    apiVersion: v1
    kind: Secret
    type: vpc.block.csi.ibm.io
    metadata:
      name: <secret_name>
      namespace: <namespace_name>
    stringData:
      encrypted: <true_or_false>
    data
      encryptionKey: <encryption_key>
    ```
    {: codeblock}

    <table summary="The columns are read from left to right. The first column has the parameter of the YAML file. The second column describes the parameter.">
    <caption>Understanding the YAML file components</caption>
    <col width="25%">
    <thead>
    <th>Component</th>
    <th>Description</th>
    </thead>
    <tbody>
    <tr>
    <td><code>name</code></td>
    <td>Enter a name for your secret.</td>
    </tr>
    <tr>
    <td><code>namespace</code></td>
    <td>Enter the namespace where you want to create your secret.</td>
    </tr>
    <tr>
    <td><code>encrypted</code></td>
    <td>In the parameters, enter <strong>true</strong> to set up encryption for your {{site.data.keyword.blockstorageshort}} volumes. </td>
    </tr>
    <tr>
    <td><code>encryptionKey</code></td>
    <td>In the parameters, enter the root key CRN of your {{site.data.keyword.keymanagementserviceshort}} service instance that you want to use to encrypt your {{site.data.keyword.blockstorageshort}} volume. To use your root key CRN in a secret, you must first convert it to base64 by running <code>echo  -n "<root_key_CRN>" | base64</code>. </td>
    </tr>
    </tbody>
    </table>

6. Follow steps 4-9 in [Adding {{site.data.keyword.block_storage_is_short}} to your apps](#vpc-block-add) to create a PVC with your customized storage class to provision {{site.data.keyword.block_storage_is_short}} that is configured for encryption with your {{site.data.keyword.keymanagementserviceshort}} root key. Then, mount this storage to an app pod.

    Your app might take a few minutes to mount the storage and get into a **Running** state.
    {: note}

7. Verify that your data is encrypted.
   1. List your {{site.data.keyword.blockstorageshort}} volumes and note the **ID** of the instance that you created. The storage instance **Name** equals the name of the PV that was automatically created when you created the PVC.
      ```
      ibmcloud is vols
      ```
      {: pre}

      Example output:
      ```
      ID                                     Name                                       Status      Capacity   IOPS   Profile           Attachment type   Created                     Zone         Resource group
      a395b603-74bf-4703-8fcb-b68e0b4d6960   pvc-479d590f-ca72-4df2-a30a-0941fceeca42   available   10         3000   5iops-tier        data              2019-08-17T12:29:18-05:00   us-south-1   a8a12accd63b437bbd6d58fb6a462ca7
      ```
      {: screen}

   2. Using the volume **ID**, list the details for your {{site.data.keyword.blockstorageshort}} instance to ensure that your {{site.data.keyword.keymanagementserviceshort}} root key is stored in the storage instance. You can find the root key in the **Encryption key** field of your CLI output.
      ```
      ibmcloud is vol <volume_ID>
      ```
      {: codeblock}

      Example output:
      ```
      ID                                     a395b603-74bf-4703-8fcb-b68e0b4d6960   
      Name                                   pvc-479d590f-ca72-4df2-a30a-0941fceeca42   
      Status                                 available   
      Capacity                               10   
      IOPS                                   3000   
      Profile                                5iops-tier   
      Encryption key                         crn:v1:bluemix:public:kms:us-south:a/6ef045fd2b43266cfe8e6388dd2ec098:53369322-958b-421c-911a-c9ae8d5156d1:key:47a985d1-5f5e-4477-93fc-12ce9bae343f   
      Encryption                             user_managed   
      Resource group                         a8a12accd63b437bbd6d58fb6a462ca7
      Created                                2019-08-17T12:29:18-05:00
      Zone                                   us-south-1   
      Volume Attachment Instance Reference
      ```
      {: screen}

      <br />

## Customizing the default storage settings
{: #vpc-customize-default}

You can change some of the default PVC settings by using a customized storage class or a Kubernetes secret to create {{site.data.keyword.block_storage_is_short}} with your customized settings.
{: shortdesc}

**What is the benefit of using a secret and specifying my parameters in a customized storage class?**</br>
As a cluster admin, [create a customized storage class](#vpc-customize-storage-class) when you want all of the PVCs that your cluster users create to be provisioned with a specific configuration and you don't want to enable your cluster users to override the default configuration.

However, when multiple configurations are required and you don't want to create a customized storage class for every possible PVC configuration, you can create one customized storage class with the default PVC settings and a reference to a generic [Kubernetes secret](#vpc-block-storageclass-secret). If your cluster users must override the default settings of your customized storage class, they can do so by creating a Kubernetes secret that holds their custom settings.

When you want to set up encryption for your {{site.data.keyword.blockstorageshort}} instance, you can also use a Kubernetes secret if you want to encode the {{site.data.keyword.keymanagementserviceshort}} root key CRN to base64 instead of providing the key directly in the customized storage class.

### Creating a custom storage class
{: #vpc-customize-storage-class}

Create your own customized storage class with the preferred settings for your {{site.data.keyword.blockstorageshort}} instance.
{: shortdesc}

You might create a custom storage class if you want to:
* Set a custom IOPs value.
* Set up {{site.data.keyword.block_storage_is_short}} with a file system type other than `ext4`.{: #vpc-block-xfs}
* Set up encryption.
* Set a custom size range.

To create your own storage class:

1. Review the [Storage class reference](#vpc-block-reference) to determine the `profile` that you want to use for your storage class. You can also review the [custom profiles]((/docs/vpc?topic=vpc-block-storage-profiles#custom)) if you want to specify custom IOPs for your {{site.data.keyword.block_storage_is_short}}.

  If you want to use a pre-installed storage class as a template, you can get the details of a storage class by using the `oc get sc <storageclass>` command.
  {: tip}

2. Create a customized storage class configuration file.
   ```yaml
   apiVersion: storage.k8s.io/v1
   kind: StorageClass
   metadata:
     name: <storage_class_name>
   provisioner: vpc.block.csi.ibm.io
   parameters:
     profile: "<profile>"
     sizeRange: "<size_range>"
     csi.storage.k8s.io/fstype: "<file_system_type>"
     billingType: "hourly"
     encrypted: "<encrypted_true_false>"
     encryptionKey: "<encryption_key>"
     resourceGroup: ""
     zone: "<zone>"
     tags: "<tags>"
     generation: "gc"
     classVersion: "1"
     iops: "<iops>" # Only specify this parameter if you are using the "custom" profile.
   reclaimPolicy: "<reclaim_policy>"
   volumeBindingMode: <volume_binding_mode>
   ```
   {: codeblock}

    <table summary="The columns are read from left to right. The first column has the parameter of the YAML file. The second column describes the parameter.">
    <caption>Understanding the YAML file components</caption>
    <col width="25%">
    <thead>
    <th>Component</th>
    <th>Description</th>
    </thead>
    <tbody>
      <tr>
      <td><code>name</code></td>
      <td>Enter a name for your storage class.</td>
      </tr>
      <tr>
      <td><code>profile</code></td>
      <td>Enter the profile that you selected in the previous step, or enter <code>custom</code> to use a custom IOPs value.</td>
      </tr>
      <tr>
      <td><code>sizeRange</code></td>
      <td>In the parameters, enter the size range for your storage in gigabytes (GiB), such as <code>[10-2000]GiB</code>. The size range must match the {{site.data.keyword.block_storage_is_short}} profile that you specify in <code>parameters.profile</code>. To find supported storage sizes for a specific profile, see [Tiered IOPS profiles](/docs/vpc?topic=vpc-block-storage-profiles). Any PVC that uses this storage class must specify a size value that is within this range.</td>
      </tr>
      <tr>
      <td><code>csi.storage.k8s.io/fstype</code></td>
      <td>In the parameters, enter the file system for your {{site.data.keyword.blockstorageshort}} instance. Choose <code>xfs</code>, <code>ext3</code>, or <code>ext4</code>. The default value is <code>ext4</code> and is used if you do not specify a file system.</td>
      </tr>
      <tr>
      <td><code>encrypted</code></td>
      <td>In the parameters, enter <strong>true</strong> to create a storage class that sets up encryption for your {{site.data.keyworblockstorageshort}} volume. If you set this option to <strong>true</strong>, you must provide the root key CRN of your {{site.data.keyword.keymanagementserviceshort}} service instance that you want to use in <code>parameterencryptionKey</code>. For more information about encrypting your data, see [Setting up encryption for your {{site.data.keyword.block_storage_is_short}}](#vpc-block-encryption).</td>
      </tr>
      <tr>
      <td><code>encryptionKey</code></td>
      <td>If you entered <strong>true</strong> for <code>parameters.encrypted</code>, then enter the root key CRN of your {{site.data.keyword.keymanagementserviceshort}} service instance that you want to use to encrypt your {{site.data.keyword.blockstorageshort}} volume. For more information about encrypting your data, see [Setting up encryption for your {{site.data.keyword.block_storage_is_short}}](#vpc-block-encryption).</td>
      </tr>
      <tr>
      <td><code>zone</code></td>
      <td>In the parameters, enter the VPC zone where you want to create the {{site.data.keyword.block_storage_is_short}} instance. Make sure that you use a zone that your worker nodes are connected to. To list VPC zones that your worker nodes use, run <code>ibmcloud oc cluster get --cluster &lt;cluster_name_or_ID&gt;</code> and look at the <strong>Worker Zones</strong> field in your CLI output. If you do not specify a zone, one of the worker node zones is automatically selected for your {{site.data.keyword.block_storage_is_short}} instance.</td>
      </tr>
      <tr>
      <td><code>tags</code></td>
      <td>In the parameters, enter a comma-separated list of tags to apply to your {{site.data.keyworblock_storage_is_short}} instance. Tags can help you find instances more easily or group your instances based on common characteristics, such as the app or the environment that it is used for. </td>
      </tr>
      <tr>
      <td><code>iops</code></td>
      <td>If you entered <code>custom</code> for the <code>profile</code>, enter a value for the IOPs that you want your {{site.data.keyword.block_storage_is_short}} to use. Refer to the [{{site.data.keyword.block_storage_is_short}} custom IOPs profile](/docs/vpc?topic=vpc-block-storage-profiles#custom) table for a list of supported IOPs ranges by volume size.</td>
      </tr>
      <tr>
      <td><code>reclaimPolicy</code></td>
      <td>Enter the reclaim policy for your storage class. If you want to keep the PV, the physical storage device and your data when you remove the PVC, enter <code>Retain</code>. If you want to delete the PV, the physical storage device and your data when you remove the PVC, enter <code>Delete</code>.</td>
      </tr>
      <tr>
      <td><code>volumeBindingMode</code></td>
      <td>Choose if you want to delay the creation of the {{site.data.keyword.block_storage_is_short}} instance until the first pod that uses this storage is ready to be scheduled. To delay the creation, enter <code>WaitForFirstConsumer</code>. To create the instance when you create the PVC, enter <code>Immediate</code>.</td>
      </tr>
   </tbody>
   </table>

4. Create the customized storage class in your cluster.
   ```
   oc apply -f custom-storageclass.yaml
   ```
   {: pre}

5. Verify that your storage class is available in the cluster.
   ```
   oc get storageclasses 
   ```
   {: pre}

   Example output:
   ```sh
   NAME                                    PROVISIONER            AGE
   ibmc-vpc-block-10iops-tier              vpc.block.csi.ibm.io   4d21h
   ibmc-vpc-block-5iops-tier               vpc.block.csi.ibm.io   4d21h
   ibmc-vpc-block-custom                   vpc.block.csi.ibm.io   4d21h
   ibmc-vpc-block-general-purpose          vpc.block.csi.ibm.io   4d21h
   ibmc-vpc-block-retain-10iops-tier       vpc.block.csi.ibm.io   4d21h
   ibmc-vpc-block-retain-5iops-tier        vpc.block.csi.ibm.io   4d21h
   ibmc-vpc-block-retain-custom            vpc.block.csi.ibm.io   4d21h
   ibmc-vpc-block-retain-general-purpose   vpc.block.csi.ibm.io   4d21h
   &lt;custom-storageclass&gt;             vpc.block.csi.ibm.io   4m26s
   ```
   {: screen}

6. Follow the steps in [Adding {{site.data.keyword.block_storage_is_short}} to your apps](#vpc-block-add) to create a PVC with your customized storage class to provision {{site.data.keyword.block_storage_is_short}}. Then, mount this storage to a sample app.

7. **Optional**: [Verify your {{site.data.keyword.block_storage_is_short}} file system type](#vpc-block-fs-verify).

### Verifying your {{site.data.keyword.block_storage_is_short}} file system
{: #vpc-block-fs-verify}

You can create a customized storage class to provision {{site.data.keyword.block_storage_is_short}} with a different file system, such as `xfs` or `ext3`. By default, all {{site.data.keyword.block_storage_is_short}} instances are provisioned with an `ext4` file system.
{: shortdesc}

1. Follow the steps to [create a customized storage class](#vpc-customize-storage-class) with the file system that you want to use.

2. Follow steps 4-9 in [Adding {{site.data.keyword.block_storage_is_short}} to your apps](#vpc-block-add) to create a PVC with your customized storage class to provision {{site.data.keyword.blockstorageshort}} with a different file system. Then, mount this storage to an app pod.

   Your app might take a few minutes to mount the storage and get into a **Running** state.
   {: note}

3. Verify that your storage is mounted with the correct file system.
   1. List the pods in your cluster and note the **Name** of the pod that you used to mount your storage.
      ```sh
      oc get pods
      ```
      {: pre}

   2. Log in to your pod.
      ```sh
      oc exec <pod_name> -it bash
      ```
      {: pre}

   3. List the mount paths inside your pod.  
      ```sh
      mount | grep /dev/xvdg
      ```
      {: pre}

      Example output for `xfs`:
      ```sh
      /dev/xvdg on /test type xfs (rw,relatime,attr2,inode64,noquota)
      ```
      {: pre}

   4. Exit your pod.
      ```sh
      exit
      ```
      {: pre}

### Storing your custom PVC settings in a Kubernetes secret
{: #vpc-block-storageclass-secret}

Specify your PVC settings in a Kubernetes secret and reference this secret in a customized storage class. Then, use the customized storage class to create a PVC with the custom parameters that you set in your secret.
{: shortdesc}

**What options do I have to use the Kubernetes secret?** </br>
As a cluster admin, you can choose if you want to allow each cluster user to override the default settings of a storage class, or if you want to create one secret that everyone in your cluster must use and that enforces base64 encoding for your {{site.data.keyword.keymanagementserviceshort}} root key CRN.

- **[Every user can customize the default settings](#customize-with-secret)**: In this scenario, the cluster admin creates one customized storage class with the default PVC settings and a reference to a generic Kubernetes secret. Cluster users can override the default settings of the storage class by creating a Kubernetes secret with the PVC settings that they want. In order for the customized settings in the secret to get applied to your {{site.data.keyword.blockstorageshort}} instance, you must create a PVC with the same name as your Kubernetes secret.

- **[Enforce base64 encoding for the {{site.data.keyword.keymanagementserviceshort}} root key](#static-secret)**: In this scenario, you create one customized storage class with the default PVC settings and a reference to a static Kubernetes secret that overrides or enhances the default settings of the customized storage class. Your cluster users cannot override the default settings by creating their own Kubernetes secret. Instead, cluster users must provision {{site.data.keyword.block_storage_is_short}} with the configuration that you chose in your customized storage class and secret. The benefit of using this method over creating a [customized storage class](#vpc-customize-storage-class) only is that you can enforce base64 encoding for the root key CRN of your {{site.data.keyword.keymanagementserviceshort}} service instance when you want to encrypt the data in your {{site.data.keyword.blockstorageshort}} instance.  

**What do I need to be aware of before I start using the Kubernetes secret for my PVC settings?** </br>
Some of the PVC settings, such as the `reclaimPolicy`, `fstype`, or the `volumeBindingMode` cannot be set in the Kubernetes secret and must be set in the storage class. As the cluster admin, if you want to enable your cluster users to override your default settings, you must ensure that you set up enough customized storage classes that reference a generic Kubernetes secret so that your users can provision {{site.data.keyword.block_storage_is_short}} with different `reclaimPolicy`, `fstype`, and `volumeBindingMode` settings.

### Enabling every user to customize the default PVC settings
{: #customize-with-secret}

1. As the cluster admin, follow the steps to [create a customized storage class](#vpc-customize-storage-class). In the customized storage class YAML file, reference the Kubernetes secret in the `metadata.annotation` section as follows. Make sure to add the code as-is and not to change variables names.
   ```
   csi.storage.k8s.io/provisioner-secret-name: ${pvc.name}
   csi.storage.k8s.io/provisioner-secret-namespace: ${pvc.namespace}
   ```
   {: codeblock}

2. As the cluster user, create a Kubernetes secret that customizes the default settings of the storage class.
   ```yaml
   apiVersion: v1
   kind: Secret
   type: vpc.block.csi.ibm.io
   metadata:
     name: <secret_name>
     namespace: <namespace_name>
   stringData:
     iops: "<IOPS_value>"
     zone: "<zone>"
     tags: "<tags>"
     encrypted: <true_or_false>
     resourceGroup: "<resource_group>"
   data
     encryptionKey: <encryption_key>
   ```
   {: codeblock}

    <table summary="The columns are read from left to right. The first column has the parameter of the YAML file. The second column describes the parameter.">
    <caption>Understanding the YAML file components</caption>
    <col width="25%">
    <thead>
    <th>Component</th>
    <th>Description</th>
    </thead>
    <tbody>
        <tr>
           <td><code>name</code></td>
           <td>Enter a name for your Kubernetes secret. </td>
       </tr>
       <tr>
           <td><code>namespace</code></td>
           <td>Enter the namespace where you want to create your secret. To reference the secret in your PVC, the PVC must be created in the same namespace. </td>
       </tr>
       <tr>
          <td><code>iops</code></td>
          <td>In the string data section, enter the range of IOPS that you want to allow for your {{site.data.keyword.blockstorageshort}} instance. The range that you enter must match the {{site.data.keyword.block_storage_is_short}} tier that you plan to use. </td>
       </tr>
       <tr>
          <td><code>zone</code></td>
          <td>In the string data section, enter the VPC zone where you want to create the {{site.data.keyword.blockstorageshort}} instance. Make sure that you use a zone that your worker nodes are connected to. To list VPC zones that your worker nodes use, run `ibmcloud oc cluster get --cluster <cluster_name_or_ID>` and look at the <strong>Worker Zones</strong> field in your CLI output. If you do not specify a zone, one of the worker node zones is automatically selected for your {{site.data.keyword.blockstorageshort}} instance.</td>
       </tr>
       <tr>
          <td><code>tags</code></td>
          <td>In the string data section, enter a comma-separated list of tags to use when the PVC is created. Tags can help you find your storage instance more easily after it is created.</td>
       </tr>
       <tr>
          <td><code>resourceGroup</code></td>
          <td>In the string data section, enter the resource group that you want your {{site.data.keyword.blockstorageshort}} instance to get access to. If you do not enter a resource group, the instance is automatically authorized to access resources of the resource group that your cluster belongs to. </td>
       </tr>
       <tr>
          <td><code>encrypted</code></td>
          <td>In the string data section, enter <strong>true</strong> to create a secret that sets up encryption for {{site.data.keyword.blockstorageshort}} volumes. If you set this option to <strong>true</strong>, you must provide the root key CRN of your {{site.data.keyword.keymanagementserviceshort}} service instance that you want to use in <code>parameters.encryptionKey</code>. For more information about encrypting your data, see [Setting up encryption for your {{site.data.keyword.block_storage_is_short}}](#vpc-block-encryption).</td>
       </tr>
       <tr>
          <td><code>encryptionKey</code></td>
          <td>In the data section, if you entered <strong>true</strong> for <code>parameters.encrypted</code>, then enter the root key CRN of your {{site.data.keyword.keymanagementserviceshort}} service instance that you want to use to encrypt your {{site.data.keyword.blockstorageshort}} volumes. To use your root key CRN in a secret, you must first convert it to base64 by running `echo  -n "<root_key_CRN>" | base64`. For more information about encrypting your data, see [Setting up encryption for your {{site.data.keyword.block_storage_is_short}}](#vpc-block-encryption).</td>
       </tr>
       </tbody>
       </table>

3. Create your Kubernetes secret.
   ```
   oc apply -f secret.yaml
   ```
   {: pre}

4. Follow the steps in [Adding {{site.data.keyword.block_storage_is_short}} to your apps](#vpc-block-add) to create a PVC with your custom settings. Make sure to create the PVC with the customized storage class that the cluster admin created and use the same name for your PVC that you used for your secret. Using the same name for the secret and the PVC triggers the storage provider to apply the settings of the secret in your PVC.

### Enforcing base64 encoding for the {{site.data.keyword.keymanagementserviceshort}} root key CRN
{: #static-secret}

1. As the cluster admin, create a Kubernetes secret that includes the base64 encoded value for your {{site.data.keyword.keymanagementserviceshort}} root key CRN. To retrieve the root key CRN, see [Setting up encryption for your {{site.data.keyword.block_storage_is_short}}](/docs/openshift?topic=openshift-vpc-block#vpc-block-encryption).
   ```yaml
   apiVersion: v1
   kind: Secret
   type: vpc.block.csi.ibm.io
   metadata:
     name: <secret_name>
     namespace: <namespace_name>
   stringData:
     encrypted: <true_or_false>
     resourceGroup: "<resource_group>"
   data
     encryptionKey: <encryption_key>
   ```
   {: codeblock}

    <table summary="The columns are read from left to right. The first column has the parameter of the YAML file. The second column describes the parameter.">
    <caption>Understanding the YAML file components</caption>
    <col width="25%">
    <thead>
    <th>Component</th>
    <th>Description</th>
    </thead>
    <tbody>
        <tr>
           <td><code>name</code></td>
           <td>Enter a name for your Kubernetes secret. </td>
       </tr>
       <tr>
           <td><code>namespace</code></td>
           <td>Enter the namespace where you want to create your secret. To reference the secret in your PVC, the PVC must be created in the same namespace. </td>
       </tr>
       <tr>
          <td><code>encrypted</code></td>
          <td>In the string data section, enter <strong>true</strong> to create a secret that sets up encryption for {{site.data.keyword.blockstorageshort}} volumes. If you set this option to <strong>true</strong>, you must provide the root key CRN of your {{site.data.keyword.keymanagementserviceshort}} service instance that you want to use in <code>parameters.encryptionKey</code>. For more information about encrypting your data, see [Setting up encryption for your {{site.data.keyword.block_storage_is_short}}](#vpc-block-encryption).</td>
       </tr>
       <tr>
          <td><code>encryptionKey</code></td>
          <td>In the data section, if you entered <strong>true</strong> for <code>parameters.encrypted</code>, then enter the root key CRN of your {{site.data.keyword.keymanagementserviceshort}} service instance that you want to use to encrypt your {{site.data.keyword.blockstorageshort}} volume. To use your root key CRN in a secret, you must first convert it to base 64 by running `echo  -n "<root_key_CRN>" | base64`. For more information about encrypting your data, see [Setting up encryption for your {{site.data.keyword.block_storage_is_short}}](#vpc-block-encryption).</td>
       </tr>
       </tbody>
       </table>

2. Create the Kubernetes secret.
   ```
   oc apply -f secret.yaml
   ```
   {: pre}

3. Follow the steps to [create a customized storage class](#vpc-customize-storage-class). In the customized storage class YAML file, reference the Kubernetes secret in the `metadata.annotation` section as follows. Make sure to enter the name of the Kubernetes secret that you created earlier and the namespace where you created the secret.
   ```
   csi.storage.k8s.io/provisioner-secret-name: <secret_name>
   csi.storage.k8s.io/provisioner-secret-namespace: <secret_namespace>
   ```
   {: codeblock}

4. As the cluster user, follow the steps in [Adding {{site.data.keyword.block_storage_is_short}} to your apps](#vpc-block-add) to create a PVC from your customized storage class.

<br />

## Backing up and restoring data
{: #vpc-block-backup-restore}

Data that is stored on {{site.data.keyword.block_storage_is_short}} is secured across redundant fault zones in your region. To manually back up your data, use the Kubernetes `oc cp` command.
{: shortdesc}

You can use the `oc cp` [command](https://kubernetes.io/docs/reference/kubectl/overview/#cp){: external} to copy files and directories to and from pods or specific containers in your cluster

Before you begin: [Access your {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-access_cluster).

To back up or restore data, choose between the following options:

- Copy data from your local machine to a pod in your cluster:
  ```
  oc cp <local_filepath>/<filename> <namespace>/<pod>:<pod_filepath>
  ```
  {: pre}

- Copy data from a pod in your cluster to your local machine:
  ```
  oc cp <namespace>/<pod>:<pod_filepath>/<filename> <local_filepath>/<filename>
  ```
  {: pre}

- Copy data from your local machine to a specific container that runs in a pod in your cluster:
  ```
  oc cp <local_filepath>/<filename> <namespace>/<pod>:<pod_filepath> -c <container>
  ```
  {: pre}

  <br />

## Storage class reference
{: #vpc-block-reference}

Storage classes that have `retain` in the title have a reclaim policy of **Retain**. Example: `ibmc-file-retain-bronze`. Storage classes that do not have `retain` in the title have a reclaim policy of **Delete**. Example: `ibmc-file-bronze`.
{: tip}

| Characteristics | Setting|
|:-----------------|:-----------------|
| Name | <code>ibmc-vpc-block-10iops-tier</code></br><code>ibmc-vpc-block-retain-10iops-tier</code> |
| File system | `ext4` |
| Corresponding {{site.data.keyword.block_storage_is_short}} tier | [10 IOPS/GB](/docs/vpc?topic=vpc-block-storage-profiles#tiers) |
| Reclaim policy | <code>ibmc-vpc-block-10iops-tier</code>: Delete</br><code>ibmc-vpc-block-retain-10iops-tier</code>: Retain |
| Billing | Hourly |
| Pricing | [Pricing information](https://www.ibm.com/cloud/vpc/pricing)|
{: class="simple-tab-table"}
{: caption="{{site.data.keyword.block_storage_is_short}} class: 10 IOPS-tier" caption-side="top"}
{: #vpc-block-10iops}
{: tab-title="10 IOPS-tier"}
{: tab-group="{{site.data.keyword.block_storage_is_short}} class"}

| Characteristics | Setting|
|:-----------------|:-----------------|
| Name | <code>ibmc-vpc-block-5iops-tier</code></br><code>ibmc-vpc-block-retain-5iops-tier</code> |
| File system | `ext4` |
| Corresponding {{site.data.keyword.block_storage_is_short}} tier | [5 IOPS/GB](/docs/vpc?topic=vpc-block-storage-profiles#tiers) |
| Reclaim policy | <code>ibmc-vpc-block-5iops-tier</code>: Delete</br><code>ibmc-vpc-block-retain-5iops-tier</code>: Retain |
| Billing | Hourly |
| Pricing | [Pricing information](https://www.ibm.com/cloud/vpc/pricing)|
{: class="simple-tab-table"}
{: caption="{{site.data.keyword.block_storage_is_short}} class: 5 IOPS-tier" caption-side="top"}
{: #vpc-block-5iops}
{: tab-title="5 IOPS-tier"}
{: tab-group="{{site.data.keyword.block_storage_is_short}} class"}

| Characteristics | Setting|
|:-----------------|:-----------------|
| Name | <code>ibmc-vpc-block-custom</code></br><code>ibmc-vpc-block-retain-custom</code> |
| File system | `ext4` |
| Corresponding {{site.data.keyword.block_storage_is_short}} tier | [Custom](/docs/vpc?topic=vpc-block-storage-profiles#custom) |
| Reclaim policy | <code>ibmc-vpc-block-custom</code>: Delete</br><code>ibmc-vpc-block-retain-custom</code>: Retain |
| Billing | Hourly |
| Pricing | [Pricing information](https://www.ibm.com/cloud/vpc/pricing)|
{: class="simple-tab-table"}
{: caption="{{site.data.keyword.block_storage_is_short}} class: custom" caption-side="top"}
{: #vpc-block-custom}
{: tab-title="Custom"}
{: tab-group="{{site.data.keyword.block_storage_is_short}} class"}

| Characteristics | Setting|
|:-----------------|:-----------------|
| Name | <code>ibmc-vpc-block-general-purpose</code></br><code>ibmc-vpc-block-retain-general-purpose</code> |
| File system | `ext4` |
| Corresponding {{site.data.keyword.block_storage_is_short}} tier | [3 IOPS/GB](/docs/vpc?topic=vpc-block-storage-profiles#tiers) |
| Reclaim policy | <code>ibmc-vpc-block-general-purpose</code>: Delete</br><code>ibmc-vpc-block-retain-general-purpose</code>: Retain |
| Billing | Hourly |
| Pricing | [Pricing information](https://www.ibm.com/cloud/vpc/pricing)|
{: class="simple-tab-table"}
{: caption="{{site.data.keyword.block_storage_is_short}} class: 3 IOPS-tier" caption-side="top"}
{: #vpc-block-3iops}
{: tab-title="General purpose"}
{: tab-group="{{site.data.keyword.block_storage_is_short}} class"}

## Removing persistent storage from a cluster
{: #cleanup}

When you set up persistent storage in your cluster, you have three main components: the Kubernetes persistent volume claim (PVC) that requests storage, the Kubernetes persistent volume (PV) that is mounted to a pod and described in the PVC, and the IBM Cloud infrastructure instance, such as classic file or block storage. Depending on how you created your storage, you might need to delete all three components separately. 
{: shortdesc}

### Understanding your storage removal options
{: #storage_delete_options}

Removing persistent storage from your {{site.data.keyword.cloud_notm}} account varies depending on how you provisioned the storage and what components you already removed.
{: shortdesc}

**Is my persistent storage deleted when I delete my cluster?**</br>
During cluster deletion, you have the option to remove your persistent storage. However, depending on how your storage was provisioned, the removal of your storage might not include all storage components.

If you [dynamically provisioned](/docs/openshift?topic=openshift-kube_concepts#dynamic_provisioning) storage with a storage class that sets `reclaimPolicy: Delete`, your PVC, PV, and the storage instance are automatically deleted when you delete the cluster. For storage that was [statically provisioned](/docs/openshift?topic=openshift-kube_concepts#static_provisioning), or storage that you provisioned with a storage class that sets `reclaimPolicy: Retain`, the PVC and the PV are removed when you delete the cluster, but your storage instance and your data remain. You are still charged for your storage instance. Also, if you deleted your cluster in an unhealthy state, the storage might still exist even if you chose to remove it.

**How do I delete the storage when I want to keep my cluster?** </br>
When you dynamically provisioned the storage with a storage class that sets `reclaimPolicy: Delete`, you can remove the PVC to start the deletion process of your persistent storage. Your PVC, PV, and storage instance are automatically removed.

For storage that was [statically provisioned](/docs/openshift?topic=openshift-kube_concepts#static_provisioning), or storage that you provisioned with a storage class that sets `reclaimPolicy: Retain`, you must manually remove the PVC, PV, and the storage instance to avoid further charges.

**How does the billing stop after I delete my storage?**</br>
Depending on what storage components you delete and when, the billing cycle might not stop immediately. If you delete the PVC and PV, but not the storage instance in your {{site.data.keyword.cloud_notm}} account, that instance still exists and you are charged for it.

If you delete the PVC, PV, and the storage instance, the billing cycle stops depending on the `billingType` that you chose when you provisioned your storage and how you chose to delete the storage.

- When you manually cancel the persistent storage instance from the {{site.data.keyword.cloud_notm}} console or the `ibmcloud sl` CLI, billing stops as follows:
  - **Hourly storage**: Billing stops immediately. After your storage is canceled, you might still see your storage instance in the console for up to 72 hours.
  - **Monthly storage**: You can choose between immediate cancellation or cancellation on the anniversary date. In both cases, you are billed until the end of the current billing cycle, and billing stops for the next billing cycle. After your storage is canceled, you might still see your storage instance in the console or the CLI for up to 72 hours.
    - **Immediate cancellation**: Choose this option to immediately remove your storage. Neither you nor your users can use the storage anymore or recover the data.
    - **Anniversary date**: Choose this option to cancel your storage on the next anniversary date. Your storage instances remain active until the next anniversary date and you can continue to use them until this date, such as to give your team time to make backups of your data.

- When you dynamically provisioned the storage with a storage class that sets `reclaimPolicy: Delete` and you choose to remove the PVC, the PV and the storage instance are immediately removed. For hourly billed storage, billing stops immediately. For monthly billed storage, you are still charged for the remainder of the month. After your storage is removed and billing stops, you might still see your storage instance in the console or the CLI for up to 72 hours.

**What do I need to be aware of before I delete persistent storage?** </br>
When you clean up persistent storage, you delete all the data that is stored in it. If you need a copy of the data, make a backup for [file storage](/docs/openshift?topic=openshift-file_storage#file_backup_restore) or [block storage](/docs/openshift?topic=openshift-block_storage#block_backup_restore).

**I deleted my storage instance. Why can I still see my instance?** </br>
After you remove persistent storage, it can take up to 72 hours for the removal to be fully processed and for the storage to disappear from your {{site.data.keyword.cloud_notm}} console or CLI.


### Cleaning up persistent storage
{: #storage_remove}

Remove the PVC, PV, and the storage instance from your {{site.data.keyword.cloud_notm}} account to avoid further charges for your persistent storage.
{: shortdesc}

Before you begin:
- Make sure that you backed up any data that you want to keep.
- [Access your {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-access_cluster).

To clean up persistent data:

1.  List the PVCs in your cluster and note the **`NAME`** of the PVC, the **`STORAGECLASS`**, and the name of the PV that is bound to the PVC and shown as **`VOLUME`**.
    ```
    oc get pvc
    ```
    {: pre}

    Example output:
    ```
    NAME                  STATUS    VOLUME                                     CAPACITY   ACCESSMODES   STORAGECLASS            AGE
    claim1-block-bronze   Bound     pvc-06886b77-102b-11e8-968a-f6612bb731fb   20Gi       RWO           ibmc-block-bronze       78d
    claim-file-bronze     Bound     pvc-457a2b96-fafc-11e7-8ff9-b6c8f770356c   4Gi        RWX           ibmc-file-bronze-retain 105d
    claim-file-silve      Bound     pvc-1efef0ba-0c48-11e8-968a-f6612bb731fb   24Gi       RWX           ibmc-file-silver        83d
    ```
    {: screen}

2. Review the **`ReclaimPolicy`** and **`billingType`** for the storage class.
   ```
   oc describe storageclass <storageclass_name>
   ```
   {: pre}

   If the reclaim policy says `Delete`, your PV and the physical storage are removed when you remove the PVC. If the reclaim policy says `Retain`, or if you provisioned your storage without a storage class, then your PV and physical storage are not removed when you remove the PVC. You must remove the PVC, PV, and the physical storage separately.

   If your storage is charged monthly, you still get charged for the entire month, even if you remove the storage before the end of the billing cycle.
   {: important}

3. Remove any pods that mount the PVC.
   1. List the pods that mount the PVC.
      ```
      oc get pods --all-namespaces -o=jsonpath='{range .items[*]}{"\n"}{.metadata.name}{":\t"}{range .spec.volumes[*]}{.persistentVolumeClaim.claimName}{" "}{end}{end}' | grep "<pvc_name>"
      ```
      {: pre}

      Example output:
      ```
      blockdepl-12345-prz7b:	claim1-block-bronze  
      ```
      {: screen}

      If no pod is returned in your CLI output, you do not have a pod that uses the PVC.

   2. Remove the pod that uses the PVC. If the pod is part of a deployment, remove the deployment.
      ```
      oc delete pod <pod_name>
      ```
      {: pre}

   3. Verify that the pod is removed.
      ```
      oc get pods
      ```
      {: pre}

4. Remove the PVC.
   ```
   oc delete pvc <pvc_name>
   ```
   {: pre}

5. Review the status of your PV. Use the name of the PV that you retrieved earlier as **`VOLUME`**.
   ```
   oc get pv <pv_name>
   ```
   {: pre}

   When you remove the PVC, the PV that is bound to the PVC is released. Depending on how you provisioned your storage, your PV goes into a `Deleting` state if the PV is deleted automatically, or into a `Released` state, if you must manually delete the PV. **Note**: For PVs that are automatically deleted, the status might briefly say `Released` before it is deleted. Rerun the command after a few minutes to see whether the PV is removed.

6. If your PV is not deleted, manually remove the PV.
   ```
   oc delete pv <pv_name>
   ```
   {: pre}

7. Verify that the PV is removed.
   ```
   oc get pv
   ```
   {: pre}


