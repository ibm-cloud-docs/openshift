---

copyright:
  years: 2014, 2020
lastupdated: "2020-01-29"

keywords: openshift, roks, rhoks, rhos

subcollection: openshift

---

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


# IBM Cloud storage utilities
{: #utilities}

## Installing the IBM Cloud Block Storage Attacher plug-in (beta)
{: #block_storage_attacher}

Use the {{site.data.keyword.cloud_notm}} Block Storage Attacher plug-in to attach raw, unformatted, and unmounted block storage to a classic worker node in your cluster.  
{: shortdesc}

For example, you want to store your data with a software-defined storage solution (SDS), such as [Portworx](/docs/openshift?topic=openshift-portworx), but you do not want to use classic bare metal worker nodes that are optimized for SDS usage and that come with extra local disks. To add local disks to your classic non-SDS worker node, you must manually create your block storage devices in your {{site.data.keyword.cloud_notm}} infrastructure account and use the {{site.data.keyword.cloud_notm}} Block Volume Attacher to attach the storage to your non-SDS worker node.

The {{site.data.keyword.cloud_notm}} Block Volume Attacher plug-in creates pods on every worker node in your cluster as part of a daemon set and sets up a Kubernetes storage class that you later use to attach the block storage device to your non-SDS worker node.

Looking for instructions for how to update or remove the {{site.data.keyword.cloud_notm}} Block Volume Attacher plug-in? See [Updating the plug-in](#update_block_attacher) and [Removing the plug-in](#remove_block_attacher).
{: tip}

1.  [Follow the instructions](/docs/containers?topic=containers-helm#public_helm_install) to install the Helm client on your local machine and install the Helm server (Tiller) with a service account.

2.  Verify that tiller is installed with a service account.

    ```
    oc get serviceaccount -n kube-system | grep tiller
    ```
    {: pre}

    Example output:

    ```
    NAME                                 SECRETS   AGE
    tiller                               1         2m
    ```
    {: screen}

3. Update the Helm repo to retrieve the latest version of all Helm charts in this repo.
   ```
   helm repo update
   ```
   {: pre}

4. Install the {{site.data.keyword.cloud_notm}} Block Volume Attacher plug-in. When you install the plug-in, pre-defined block storage classes are added to your cluster.
   ```
   helm install iks-charts/ibm-block-storage-attacher --name block-attacher
   ```
   {: pre}

   Example output:
   ```
   NAME:   block-volume-attacher
   LAST DEPLOYED: Thu Sep 13 22:48:18 2018
   NAMESPACE: default
   STATUS: DEPLOYED

   RESOURCES:
   ==> v1beta1/ClusterRoleBinding
   NAME                             AGE
   ibmcloud-block-storage-attacher  1s

   ==> v1beta1/DaemonSet
   NAME                             DESIRED  CURRENT  READY  UP-TO-DATE  AVAILABLE  NODE SELECTOR  AGE
   ibmcloud-block-storage-attacher  0        0        0      0           0          <none>         1s

   ==> v1/StorageClass
   NAME                 PROVISIONER                AGE
   ibmc-block-attacher  ibm.io/ibmc-blockattacher  1s

   ==> v1/ServiceAccount
   NAME                             SECRETS  AGE
   ibmcloud-block-storage-attacher  1        1s

   ==> v1beta1/ClusterRole
   NAME                             AGE
   ibmcloud-block-storage-attacher  1s

   NOTES:
   Thank you for installing: ibmcloud-block-storage-attacher.   Your release is named: block-volume-attacher

   Please refer Chart README.md file for attaching a block storage
   Please refer Chart RELEASE.md to see the release details/fixes
   ```
   {: screen}

5. Verify that the {{site.data.keyword.cloud_notm}} Block Volume Attacher daemon set is installed successfully.
   ```
   oc get pod -n kube-system -o wide | grep attacher
   ```
   {: pre}

   Example output:
   ```
   ibmcloud-block-storage-attacher-z7cv6           1/1       Running            0          19m
   ```
   {: screen}

   The installation is successful when you see one or more **ibmcloud-block-storage-attacher** pods. The number of pods equals the number of worker nodes in your cluster. All pods must be in a **Running** state.

6. Verify that the storage class for the {{site.data.keyword.cloud_notm}} Block Volume Attacher is created successfully.
   ```
   oc get storageclasses | grep attacher
   ```
   {: pre}

   Example output:
   ```
   ibmc-block-attacher       ibm.io/ibmc-blockattacher   11m
   ```
   {: screen}

### Updating the IBM Cloud Block Storage Attacher plug-in
{: #update_block_attacher}

You can upgrade the existing {{site.data.keyword.cloud_notm}} Block Storage Attacher plug-in to the latest version.
{: shortdesc}

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

3. Find the name of the Helm chart for the {{site.data.keyword.cloud_notm}} Block Storage Attacher plug-in.
   ```
   helm list | grep ibm-block-storage-attacher
   ```
   {: pre}

   Example output:
   ```
   <helm_chart_name>	1       	Wed Aug  1 14:55:15 2018	DEPLOYED	ibm-block-storage-attacher-1.0.0	default
   ```
   {: screen}

4. Upgrade the {{site.data.keyword.cloud_notm}} Block Storage Attacher to latest.
   ```
   helm upgrade --force --recreate-pods <helm_chart_name> ibm-block-storage-attacher
   ```
   {: pre}

### Removing the IBM Cloud Block Volume Attacher plug-in
{: #remove_block_attacher}

If you do not want to provision and use the {{site.data.keyword.cloud_notm}} Block Storage Attacher plug-in in your cluster, you can uninstall the Helm chart.
{: shortdesc}

1. Find the name of the Helm chart for the {{site.data.keyword.cloud_notm}} Block Storage Attacher plug-in.
   ```
   helm list | grep ibm-block-storage-attacher
   ```
   {: pre}

   Example output:
   ```
   <helm_chart_name>	1       	Wed Aug  1 14:55:15 2018	DEPLOYED	ibm-block-storage-attacher-1.0.0	default
   ```
   {: screen}

2. Delete the {{site.data.keyword.cloud_notm}} Block Storage Attacher plug-in by removing the Helm chart.
   ```
   helm delete --purge <helm_chart_name>
   ```
   {: pre}

3. Verify that the {{site.data.keyword.cloud_notm}} Block Storage Attacher plug-in pods are removed.
   ```
   oc get pod -n kube-system -o wide | grep attacher
   ```
   {: pre}

   The removal of the pods is successful if no pods are displayed in your CLI output.

4. Verify that the {{site.data.keyword.cloud_notm}} Block Storage Attacher storage class is removed.
   ```
   oc get storageclasses | grep attacher
   ```
   {: pre}

   The removal of the storage class is successful if no storage class is displayed in your CLI output.

   <br />


## Automatically provisioning unformatted block storage and authorizing your worker nodes to access the storage
{: #automatic_block}

You can use the {{site.data.keyword.cloud_notm}} Block Volume Attacher plug-in to automatically add raw, unformatted, and unmounted block storage with the same configuration to all classic worker nodes in your cluster.
{: shortdesc}

The `mkpvyaml` container that is included in the {{site.data.keyword.cloud_notm}} Block Volume Attacher plug-in is configured to run a script that finds all worker nodes in your cluster, creates raw block storage in the {{site.data.keyword.cloud_notm}} infrastructure portal, and then authorizes the worker nodes to access the storage.

To add different block storage configurations, add block storage to a subset of worker nodes only, or to have more control over the provisioning process, choose to [manually add block storage](#manual_block).
{: tip}


1. Log in to {{site.data.keyword.cloud_notm}} and target the resource group that your cluster is in.
   ```
   ibmcloud login
   ```
   {: pre}

2.  Clone the {{site.data.keyword.cloud_notm}} Storage Utilities repo.
    ```
    git clone https://github.com/IBM/ibmcloud-storage-utilities.git
    ```
    {: pre}

3. Navigate in to the `block-storage-utilities` directory.
   ```
   cd ibmcloud-storage-utilities/block-storage-provisioner
   ```
   {: pre}

4. Open the `yamlgen.yaml` file and specify the block storage configuration that you want to add to every worker node in the cluster.
   ```yaml
   #
   # Can only specify 'performance' OR 'endurance' and associated clause
   #
   cluster:  <cluster_name>    #  Enter the name of your cluster
   region:   <region>          #  Enter the IBM Cloud Kubernetes Service region where you created your cluster
   type:  <storage_type>       #  Enter the type of storage that you want to provision. Choose between "performance" or "endurance"
   offering: storage_as_a_service   
   # performance:
   #    - iops:  <iops>       
   endurance:
     - tier:  2                #   [0.25|2|4|10]
   size:  [ 20 ]               #   Enter the size of your storage in gigabytes
   ```
   {: codeblock}

   <table>
   <caption>Understanding the YAML file components</caption>
   <thead>
   <th colspan=2><img src="images/idea.png" alt="Idea icon"/> Understanding the YAML file components</th>
   </thead>
   <tbody>
   <tr>
   <td><code>cluster</code></td>
   <td>Enter the name of your cluster where you want to add raw block storage. </td>
   </tr>
   <tr>
   <td><code>region</code></td>
   <td>Enter the {{site.data.keyword.containerlong_notm}} region where you created your cluster. Run <code>ibmcloud oc cluster get --cluster &lt;cluster_name_or_ID&gt;</code> to find the region of your cluster.  </td>
   </tr>
   <tr>
   <td><code>type</code></td>
   <td>Enter the type of storage that you want to provision. Choose between <code>performance</code> or <code>endurance</code>. For more information, see [Deciding on your block storage configuration](/docs/openshift?topic=openshift-block_storage#block_predefined_storageclass).  </td>
   </tr>
   <tr>
   <td><code>performance.iops</code></td>
   <td>If you want to provision `performance` storage, enter the number of IOPS. For more information, see [Deciding on your block storage configuration](/docs/openshift?topic=openshift-block_storage#block_predefined_storageclass). If you want to provision `endurance` storage, remove this section or comment it out by adding `#` to the beginning of each line.
   </tr>
   <tr>
   <td><code>endurance.tier</code></td>
   <td>If you want to provision `endurance` storage, enter the number of IOPS per gigabyte. For example, if you want to provision block storage as it is defined in the `ibmc-block-bronze` storage class, enter 2. For more information, see [Deciding on your block storage configuration](/docs/openshift?topic=openshift-block_storage#block_predefined_storageclass). If you want to provision `performance` storage, remove this section or comment it out by adding `#` to the beginning of each line. </td>
   </tr>
   <tr>
   <td><code>size</code></td>
   <td>Enter the size of your storage in gigabytes. See [Deciding on your block storage configuration](/docs/openshift?topic=openshift-block_storage#block_predefined_storageclass) to find supported sizes for your storage tier. </td>
   </tr>
   </tbody>
   </table>  

5. Retrieve your IBM Cloud infrastructure username and API key. The username and API key are used by the `mkpvyaml` script to access the cluster.
   1.  Log in to the [{{site.data.keyword.cloud_notm}} console](https://cloud.ibm.com){: external}.
   2.  From the menu bar, select **Manage > Access (IAM)**.
   3.  Select the **Users** tab and then click on your username.
   4.  In the **API keys** pane, find the entry **Classic infrastructure API key** and click the **Actions menu** ![Action menu icon](../icons/action-menu-icon.svg "Action menu icon") **> Details**.
   5.  Copy the API username and API key.

6. Store the credentials in an environment variable.
   1. Add the environment variables.
      ```
      export SL_USERNAME=<infrastructure_username>
      ```
      {: pre}

      ```
      export SL_API_KEY=<infrastructure_api_key>
      ```
      {: pre}

   2. Verify that your environment variables are created successfully.
      ```
      printenv
      ```
      {: pre}

7.  Build and run the `mkpvyaml` container. When you run the container from the image, the `mkpvyaml.py` script is executed. The script adds a block storage device to every worker node in the cluster and authorizes each worker node to access the block storage device. At the end of the script, a `pv-<cluster_name>.yaml` YAML file is generated for you that you can later use to create the persistent volumes in the cluster.
    1.  Build the `mkpvyaml` container.
        ```
        docker build -t mkpvyaml .
        ```
        {: pre}
        Example output:
        ```
        Sending build context to Docker daemon   29.7kB
        Step 1/16 : FROM ubuntu:18.10
        18.10: Pulling from library/ubuntu
        5940862bcfcd: Pull complete
        a496d03c4a24: Pull complete
        5d5e0ccd5d0c: Pull complete
        ba24b170ddf1: Pull complete
        Digest: sha256:20b5d52b03712e2ba8819eb53be07612c67bb87560f121cc195af27208da10e0
        Status: Downloaded newer image for ubuntu:18.10
         ---> 0bfd76efee03
        Step 2/16 : RUN apt-get update
         ---> Running in 85cedae315ce
        Get:1 http://security.ubuntu.com/ubuntu cosmic-security InRelease [83.2 kB]
        Get:2 http://archive.ubuntu.com/ubuntu cosmic InRelease [242 kB]
        ...
        Step 16/16 : ENTRYPOINT [ "/docker-entrypoint.sh" ]
         ---> Running in 9a6842f3dbe3
        Removing intermediate container 9a6842f3dbe3
         ---> 7926f5384fc7
        Successfully built 7926f5384fc7
        Successfully tagged mkpvyaml:latest
        ```
        {: screen}
    2.  Run the container to execute the `mkpvyaml.py` script.
        ```
        docker run --rm -v `pwd`:/data -v ~/.bluemix:/config -e SL_API_KEY=$SL_API_KEY -e SL_USERNAME=$SL_USERNAME mkpvyaml
        ```
        {: pre}

        Example output:
        ```
        Unable to find image 'portworx/iks-mkpvyaml:latest' locally
        latest: Pulling from portworx/iks-mkpvyaml
        72f45ff89b78: Already exists
        9f034a33b165: Already exists
        386fee7ab4d3: Already exists
        f941b4ac6aa8: Already exists
        fe93e194fcda: Pull complete
        f29a13da1c0a: Pull complete
        41d6e46c1515: Pull complete
        e89af7a21257: Pull complete
        b8a7a212d72e: Pull complete
        5e07391a6f39: Pull complete
        51539879626c: Pull complete
        cdbc4e813dcb: Pull complete
        6cc28f4142cf: Pull complete
        45bbaad87b7c: Pull complete
        05b0c8595749: Pull complete
        Digest: sha256:43ac58a8e951994e65f89ed997c173ede1fa26fb41e5e764edfd3fc12daf0120
        Status: Downloaded newer image for portworx/iks-mkpvyaml:latest

        kube-dal10-abc1d23e123456ac8b12a3c1e12b123a4 10.XXX.XX.XX
        Creating Vol of size 20 with type:  endurance
                  Ordering block storage of size: 20 for host: kube-dal10-abc1d23e123456ac8b12a3c1e12b123a4
                  ORDER ID =  30087291
        kube-dal10-abc1d23e123456ac8b12a3c1e12b123a4 10.XXX.XX.XX
        Creating Vol of size 20 with type:  endurance
                  Ordering block storage of size: 20 for host: kube-dal10-abc1d23e123456ac8b12a3c1e12b123a4
                  ORDER ID =  30087293
        kube-dal12-abc1d23e123456ac8b12a3c1e12b456v1 10.XXX.XX.XX
        Creating Vol of size 20 with type:  endurance
                  Ordering block storage of size: 20 for host: kube-dal12-abc1d23e123456ac8b12a3c1e12b456v1
                  ORDER ID =  30085655
                  No volume yet ... for orderID :  30087291
                  No volume yet ... for orderID :  30087291
                  No volume yet ... for orderID :  30087291
                  No volume yet ... for orderID :  30087291
                  Order ID =  30087291 has created VolId =  12345678
                  Granting access to volume: 12345678 for HostIP: 10.XXX.XX.XX
                  Order ID =  30087293 has created VolId =  87654321
                  Granting access to volume: 87654321 for HostIP: 10.XXX.XX.XX
                  Vol 53002831 is not yet ready ...
                  Granting access to volume: 87654321 for HostIP: 10.XXX.XX.XX
                  Order ID =  30085655 has created VolId =  98712345
                  Granting access to volume: 98712345 for HostIP: 10.XXX.XX.XX
        Output file created as :  pv-<cluster_name>.yaml
        ```
        {: screen}

7. [Attach the block storage devices to your worker nodes](#attach_block).

<br />


## Manually adding block storage to specific worker nodes
{: #manual_block}

Use this option if you want to add different block storage configurations, add block storage to a subset of worker nodes only, or to have more control over the provisioning process.
{: shortdesc}

1. List the worker nodes in your cluster and note the private IP address and the zone of the non-SDS worker nodes where you want to add a block storage device.
   ```
   ibmcloud oc worker ls --cluster <cluster_name_or_ID>
   ```
   {: pre}

2. Review step 3 and 4 in [Deciding on your block storage configuration](/docs/openshift?topic=openshift-block_storage#block_predefined_storageclass) to choose the type, size, and number of IOPS for the block storage device that you want to add to your non-SDS worker node.    

3. Create the block storage device in the same zone that your non-SDS worker node is in.

   **Example for provisioning 20 GB endurance block storage with two IOPS per GB:**
   ```
   ibmcloud sl block volume-order --storage-type endurance --size 20 --tier 2 --os-type LINUX --datacenter dal10
   ```
   {: pre}

   **Example for provisioning 20 GB performance block storage with 100 IOPS:**
   ```
   ibmcloud sl block volume-order --storage-type performance --size 20 --iops 100 --os-type LINUX --datacenter dal10
   ```
   {: pre}

4. Verify that the block storage device is created and note the **`id`** of the volume. **Note:** If you do not see your block storage device right away, wait a few minutes. Then, run this command again.
   ```
   ibmcloud sl block volume-list
   ```
   {: pre}

   Example output:
   ```
   id         username          datacenter   storage_type                capacity_gb   bytes_used   ip_addr         lunId   active_transactions   
   123456789  IBM02SL1234567-8  dal10        performance_block_storage   20            -            161.12.34.123   0       0   
   ```
   {: screen}

5. Review the details for your volume and note the **`Target IP`** and **`LUN Id`**.
   ```
   ibmcloud sl block volume-detail <volume_ID>
   ```
   {: pre}

   Example output:
   ```
   Name                       Value   
   ID                         1234567890   
   User name                  IBM123A4567890-1   
   Type                       performance_block_storage   
   Capacity (GB)              20   
   LUN Id                     0   
   IOPs                       100   
   Datacenter                 dal10   
   Target IP                  161.12.34.123   
   # of Active Transactions   0   
   Replicant Count            0
   ```
   {: screen}

6. Authorize the non-SDS worker node to access the block storage device. Replace `<volume_ID>` with the volume ID of your block storage device that you retrieved earlier, and `<private_worker_IP>` with the private IP address of the non-SDS worker node where you want to attach the device.

   ```
   ibmcloud sl block access-authorize <volume_ID> -p <private_worker_IP>
   ```
   {: pre}

   Example output:
   ```
   The IP address 123456789 was authorized to access <volume_ID>.
   ```
   {: screen}

7. Verify that your non-SDS worker node is successfully authorized and note the **`host_iqn`**, **`username`**, and **`password`**.
   ```
   ibmcloud sl block access-list <volume_ID>
   ```
   {: pre}

   Example output:
   ```
   ID          name                 type   private_ip_address   source_subnet   host_iqn                                      username   password           allowed_host_id   
   123456789   <private_worker_IP>  IP     <private_worker_IP>  -               iqn.2018-09.com.ibm:ibm02su1543159-i106288771   IBM02SU1543159-I106288771   R6lqLBj9al6e2lbp   1146581   
   ```
   {: screen}

   The authorization is successful when the **`host_iqn`**, **`username`**, and **`password`** are assigned.

8. [Attach the block storage devices to your worker nodes](#attach_block).

<br />



## Attaching raw block storage to non-SDS worker nodes
{: #attach_block}

To attach the block storage device to a non-SDS worker node, you must create a persistent volume (PV) with the {{site.data.keyword.cloud_notm}} Block Volume Attacher storage class and the details of your block storage device.
{: shortdesc}

**Before you begin**:
- Make sure that you [automatically](#automatic_block) or [manually](#manual_block) created raw, unformatted, and unmounted block storage to your non-SDS worker nodes.
- [Log in to your account. If applicable, target the appropriate resource group. Set the context for your cluster.](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure)

**To attach raw block storage to non-SDS worker nodes**:
1. Prepare the PV creation.  
   - **If you used the `mkpvyaml` container:**
     1. Open the `pv-<cluster_name>.yaml` file.
        ```
        nano pv-<cluster_name>.yaml
        ```
        {: pre}

     2. Review the configuration for your PVs.

   - **If you manually added block storage:**
     1. Create a `pv.yaml` file. The following command creates the file with the `nano` editor.
        ```
        nano pv.yaml
        ```
        {: pre}

     2. Add the details of your block storage device to the PV.
        ```yaml
        apiVersion: v1
        kind: PersistentVolume
        metadata:
          name: <pv_name>
          annotations:
            ibm.io/iqn: "<IQN_hostname>"
            ibm.io/username: "<username>"
            ibm.io/password: "<password>"
            ibm.io/targetip: "<targetIP>"
            ibm.io/lunid: "<lunID>"
            ibm.io/nodeip: "<private_worker_IP>"
            ibm.io/volID: "<volume_ID>"
        spec:
          capacity:
            storage: <size>
          accessModes:
            - ReadWriteOnce
          hostPath:
              path: /
          storageClassName: ibmc-block-attacher
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
      	<td>Enter a name for your PV.</td>
      	</tr>
        <tr>
        <td><code>ibm.io/iqn</code></td>
        <td>Enter the IQN hostname that you retrieved earlier. </td>
        </tr>
        <tr>
        <td><code>ibm.io/username</code></td>
        <td>Enter the IBM Cloud infrastructure username that you retrieved earlier. </td>
        </tr>
        <tr>
        <td><code>ibm.io/password</code></td>
        <td>Enter the IBM Cloud infrastructure password that you retrieved earlier. </td>
        </tr>
        <tr>
        <td><code>ibm.io/targetip</code></td>
        <td>Enter the target IP that you retrieved earlier. </td>
        </tr>
        <tr>
        <td><code>ibm.io/lunid</code></td>
        <td>Enter the LUN ID of your block storage device that you retrieved earlier. </td>
        </tr>
        <tr>
        <td><code>ibm.io/nodeip</code></td>
        <td>Enter the private IP address of the worker node where you want to attach the block storage device and that you authorized earlier to access your block storage device. </td>
        </tr>
        <tr>
          <td><code>ibm.io/volID</code></td>
        <td>Enter the ID of the block storage volume that you retrieved earlier. </td>
        </tr>
        <tr>
        <td><code>storage</code></td>
        <td>Enter the size of the block storage device that you created earlier. For example, if your block storage device is 20 gigabytes, enter <code>20Gi</code>.  </td>
        </tr>
        </tbody>
        </table>
2. Create the PV to attach the block storage device to your non-SDS worker node.
   - **If you used the `mkpvyaml` container:**
     ```
     oc apply -f pv-<cluster_name>.yaml
     ```
     {: pre}

   - **If you manually added block storage:**
     ```
     oc apply -f  block-volume-attacher/pv.yaml
     ```
     {: pre}

3. Verify that the block storage is successfully attached to your worker node.
   ```
   oc describe pv <pv_name>
   ```
   {: pre}

   Example output:
   ```
   Name:            kube-wdc07-cr398f790bc285496dbeb8e9137bc6409a-w1-pv1
   Labels:          <none>
   Annotations:     ibm.io/attachstatus=attached
                    ibm.io/dm=/dev/dm-1
                    ibm.io/iqn=iqn.2018-09.com.ibm:ibm02su1543159-i106288771
                    ibm.io/lunid=0
                    ibm.io/mpath=3600a09803830445455244c4a38754c66
                    ibm.io/nodeip=10.176.48.67
                    ibm.io/password=R6lqLBj9al6e2lbp
                    ibm.io/targetip=161.26.98.114
                    ibm.io/username=IBM02SU1543159-I106288771
                    kubectl.kubernetes.io/last-applied-configuration={"apiVersion":"v1","kind":"PersistentVolume","metadata":{"annotations":{"ibm.io/iqn":"iqn.2018-09.com.ibm:ibm02su1543159-i106288771","ibm.io/lunid":"0"...
   Finalizers:      []
   StorageClass:    ibmc-block-attacher
   Status:          Available
   Claim:           
   Reclaim Policy:  Retain
   Access Modes:    RWO
   Capacity:        20Gi
   Node Affinity:   <none>
   Message:         
   Source:
       Type:          HostPath (bare host directory volume)
       Path:          /
       HostPathType:  
   Events:            <none>
   ```
   {: screen}

   The block storage device is successfully attached when the **ibm.io/dm** is set to a device ID, such as `/dev/dm/1`, and you can see **ibm.io/attachstatus=attached** in the **Annotations** section of your CLI output.

If you want to detach a volume, delete the PV. Detached volumes are still authorized to be accessed by a specific worker node and are attached again when you create a new PV with the {{site.data.keyword.cloud_notm}} Block Volume Attacher storage class to attach a different volume to the same worker node. To avoid attaching the old detached volume again, unauthorize the worker node to access the detached volume by using the `ibmcloud sl block access-revoke` command. Detaching the volume does not remove the volume from your IBM Cloud infrastructure account. To cancel the billing for your volume, you must manually [remove the storage from your IBM Cloud infrastructure account](/docs/containers?topic=containers-cleanup).
{: note}

<br />




<br />


## Backing up and restoring PVC data for file and block storage
{: #ibmcloud-backup-restore}

With the {{site.data.keyword.cloud_notm}} Backup Restore Helm chart, you can create a one-time or scheduled backup for data that is stored in a file storage or block storage persistent volume claim (PVC). Your data is stored in an {{site.data.keyword.cos_full_notm}} service instance that you create and own. You can use existing backups in your {{site.data.keyword.cos_full_notm}} service instance to restore data to a PVC in your cluster.
{: shortdesc}

**What happens when I install the Helm chart?**</br>
When you install the Helm chart, a Kubernetes pod is created in your cluster that performs a one-time or periodic backup of your PVC data, or restores data from {{site.data.keyword.cos_full_notm}} to a PVC. You configure your backup or restore in the `values.yaml` file that is provided with the Helm chart or by setting flags in the `helm install` command.

**What limitations do I need to be aware of?**</br>
If you want to back up or restore data of a block storage PVC, your PVC must not be mounted to an app. Block storage is mounted with a RWO access mode. This access allows only one pod to be mounted to the block storage at a time. To back up or restore your data, you must remove the pod that uses the storage to unmount the PVC. After the backup or restoring of data is finished, you can re-create your pod and mount the backed up or restored PVC.

**What do I need before I get started?** </br>
To back up or restore data to {{site.data.keyword.cos_full_notm}}, you must [set up an {{site.data.keyword.cos_full_notm}} service instance, create service credentials to access the service, and create a bucket that can hold your data](#backup_restore_setup_object_storage).  

### Setting up an {{site.data.keyword.cos_full_notm}} service instance
{: #backup_restore_setup_object_storage}

Create and configure an {{site.data.keyword.cos_full_notm}} service instance to serve as the repository for the data that you want to back up.
{: shortdesc}

1. Create an [{{site.data.keyword.cos_full_notm}} service instance](/docs/openshift?topic=openshift-object_storage#create_cos_service) that uses HMAC credentials.
2. Store your [{{site.data.keyword.cos_full_notm}} credentials in a Kubernetes secret](docs/openshift?topic=openshift-object_storage#create_cos_secret).
3. Create your first {{site.data.keyword.cos_full_notm}} bucket.
   1. In the navigation on the service details page, click **Buckets**.
   2. Click **Create bucket**. A dialog box is displayed.
   3. Enter a unique name for your bucket. The name must be unique within {{site.data.keyword.cos_full_notm}} across all regions and across all {{site.data.keyword.cloud_notm}} accounts.
   4. From the **Resiliency** list, select the level of availability that you want for your data. For more information, see [{{site.data.keyword.cos_full_notm}} regions and endpoints](/docs/cloud-object-storage/basics?topic=cloud-object-storage-endpoints#endpoints).
   5. Change the **Location** to the region where you want to store your data. Keep in mind that your data might not be allowed to be stored in every region due to legal reasons.  
   6. Click **Create**.
4. Retrieve the {{site.data.keyword.cos_full_notm}} host name for your bucket.
   1. Click on your bucket name that you created in the previous step.
   2. In the navigation on the service details page, click **Buckets** > **Configuration**.
   3. Note the public URL that you can use to access the data in your bucket.

For more information about configuring your service instance, see the [{{site.data.keyword.cos_full_notm}}](/docs/cloud-object-storage?topic=cloud-object-storage-getting-started) documentation.

### Using {{site.data.keyword.cos_full_notm}} to back up and restore PVC data
{: #backup-restore-pvc}

You can use the {{site.data.keyword.cloud_notm}} Backup Restore Helm chart to back up data in a file storage or block storage PVC to {{site.data.keyword.cos_full_notm}}, or restore data from {{site.data.keyword.cos_full_notm}} to a PVC in your cluster.
{: shortdesc}

Before you begin:
- Make sure that you have a PVC that you can back up or restore data to. For more information about how to create a PVC, see [Adding file storage to apps](/docs/openshift?topic=openshift-file_storage#add_file) and [Adding block storage to apps](/docs/openshift?topic=openshift-block_storage#add_block).
- If you want to back up a block storage PVC, make sure that your PVC is not mounted to an app. Block storage is mounted with a RWO access mode. This access allows only one pod to be mounted to the block storage at a time. To back up your data, you must remove the app pod that mounts the storage. To check whether a pod is mounted to your PVC, run the following command.
  ```sh
  oc get pods --all-namespaces -o=jsonpath='{range .items[*]}{"\n"}{.metadata.name}{":\t"}{range .spec.volumes[*]}{.persistentVolumeClaim.claimName}{" "}{end}{end}' | grep "<pvc_name>"
  ```
  {: pre}
- [Retrieve your {{site.data.keyword.cos_full_notm}} service credentials, the bucket name, and the bucket hostname](#backup_restore_setup_object_storage).
- [Follow the instructions](/docs/containers?topic=containers-helm#public_helm_install) to install the Helm client on your local machine, install the Helm server (Tiller) with a service account, and set up the {{site.data.keyword.cloud_notm}} Helm chart repositories.
- [Log in to your account. If applicable, target the appropriate resource group. Set the context for your cluster.](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure)

You can deploy the `ibm-storage-backup` pod or the `ibm-storage-restore` pod by either editing and applying the `values.yaml` file of the Helm chart, or by running the `helm install` command from the CLI.
{: note}

To back up or restore a PVC by editing the `values.yaml` file:

1. Download the latest Helm chart version to your local machine.
  ```
  helm fetch --untar iks-charts/ibmcloud-backup-restore
  ```
  {: pre}

2. Open the `values.yaml` file in the nano command line editor.
  ```
  nano ibmcloud-backup-restore/values.yaml
  ```
  {: pre}

3. Configure your Helm chart to back up or restore PVC data. You can configure the backup for more than one PVC.

  Example to create a backup pod by configuring the `values.yaml` file:

  ```yaml
  image:
    repository: icr.io/iks-charts/ibmcloud-backup-restore
    pullPolicy: Always
    tag: latest
  ACCESS_KEY_ID: # Example: 10110abab1111bbb111aa1aaa111b1a1
  SECRET_ACCESS_KEY: # Example: a1aba11aaa11b11b11aa1111a1111ba111111111a0b1b11a
  ENDPOINT: # Example: s3.us-east.cloud-object-storage.appdomain.cloud
  BUCKET_NAME: # Example: my-bucket
  BACKUP_NAME: # Example: my_backup
  PVC_NAMES:
    - # Example: my_pvc
    - # Optional example: my_pvc2
  CHART_TYPE: # Example: backup
  BACKUP_TYPE: # Example: incremental
  SCHEDULE_TYPE: # Example: periodic
  SCHEDULE_INFO: # Example: weekly
  ```
  {: codeblock}

  <table>
    <caption>Understanding the <code>values.yaml</code> file</caption>
    <thead>
    <th colspan=2><img src="images/idea.png" alt="Idea icon"/> Understanding the `values.yaml` file components</th>
    </thead>
    <tbody>
    <tr>
    <td><code>ACCESS_KEY_ID</code></td>
    <td>Enter the access key ID of the {{site.data.keyword.cos_full_notm}} service credentials that you retrieved earlier. </td>
    </tr>
    <tr>
    <td><code>SECRET_ACCESS_KEY</code></td>
    <td>Enter the secret access key of the {{site.data.keyword.cos_full_notm}} service credentials that you retrieved earlier.</td>
    </tr>
    <tr>
    <td><code>ENDPOINT</code></td>
    <td>Enter the public {{site.data.keyword.cos_full_notm}} s3 API endpoint for your bucket that you retrieved earlier. </td>
    </tr>
    <tr>
    <td><code>BUCKET_NAME</code></td>
    <td><ul><li><strong>Backup: </strong>Enter the name of the {{site.data.keyword.cos_full_notm}} bucket that you created earlier. You use this bucket to store PVC data when you perform a backup. </li><li><strong>Restore: </strong>Enter the name of the {{site.data.keyword.cos_full_notm}} bucket where your backup is stored. </li></ul></td>
    </tr>
    <tr>
    <td><code>BACKUP_NAME</code></td>
    <td><ul><li><strong>Backup: </strong>Enter the name of the backup that you want to create in {{site.data.keyword.cos_full_notm}}. </li><li><strong>Restore: </strong>Enter the name of the backup that you created with the {{site.data.keyword.cloud_notm}} Backup Restore Helm chart in {{site.data.keyword.cos_full_notm}}. If you have multiple full backups in your {{site.data.keyword.cos_full_notm}} service instance, the PVC is restored with the data of the last full backup. If you have incremental backups, the PVC is restored with the data of the last full backup, including all incremental backups up to the day where you start the restore. </li></ul> </td>
    </tr>
    <tr>
    <td><code>PVC_NAMES</code></td>
    <td><ul><li><strong>Backup: </strong>Enter the name of the PVC that you want to back up. If you want to back up multiple PVCs, add each PVC to the list of PVCs. To list available PVCs in your cluster that you can back up, run <code>oc get pvc</code>. </li><li><strong>Restore: </strong>Enter the name of the PVC to which you want to restore data from {{site.data.keyword.cos_full_notm}}. You can restore data to one PVC at a time only. To list available PVCs in your cluster that you can restore data to, run <code>oc get pvc</code>.</li></ul></td>
    </tr>
    <tr>
    <td><code>BACKUP_TYPE</code></td>
    <td>Required only for backups. Enter <strong>full</strong> to create a full backup, or <strong>incremental</strong> if you want to back up only new or changed files. If you choose <strong>incremental</strong>, you must specify the <code>SCHEDULING_INFO</code> and <code>SCHEDULING_TYPE</code> option. If you don't specify the <code>BACKUP_TYPE</code> option, a full backup is created by default. </td>
    </tr>
    <tr>
    <td><code>SCHEDULE_TYPE</code></td>
    <td>Required only for backups. Enter <strong>periodic</strong> to create scheduled backups, or leave this option empty to create a one-time backup. If you want to create periodic backups, you must define the backup interval in the <code>SCHEDULE_INFO</code> option. </td>
    </tr>
    <tr>
    <td><code>SCHEDULE_INFO</code></td>
    <td>Required only for backups. If you want to create periodic backups, you must decide on the backup schedule. Choose between <strong>hourly</strong>, <strong>daily</strong>, or <strong>weekly</strong>. If you set this option, you must set <code>SCHEDULE_TYPE</code> to <strong>periodic</strong>.</td>
    </tr>
    </tbody>
  </table>

4. Save and close the `values.yaml` file.

5.  Install the Helm chart with your custom settings in the `values.yaml` file. When you install the Helm chart and you configure a backup or restore, an `ibm-storage-backup` or an `ibm-storage-restore` pod is deployed to your cluster. The backup pod backs up the data from your PVC to {{site.data.keyword.cos_full_notm}} and the restore pod restores data to a PVC. Replace `<release_name>` with a name for your Helm chart.

    *   Install the Helm chart by using the `helm install` command.

        ```
        helm install ./ibmcloud-backup-restore --name <release_name>
        ```
        {: pre}

        Example output for backup:

        ```
        NAME: <release_name>
        LAST DEPLOYED: Mon Jan 20 09:17:02 2020
        NAMESPACE: default
        STATUS: deployed
        REVISION: 1
        TEST SUITE: None
        NOTES:
        Thank you for installing: ibmcloud-backup-restore.   Your release is named: <release_name>

        Please refer Chart README.md file for creating a sample PVC
        Please refer Chart RELEASE.md to see the release details/fixes
        ```
        {: screen}

    *   Optional: Install the Helm chart by setting flags in the `helm install` command. You can name your release by specifying the `--name` parameter.
        <p><pre class="pre"><code>helm install ./ibmcloud-backup-restore --set ACCESS_KEY_ID=&lt;access_key_ID&gt;<br> --set SECRET_ACCESS_KEY=&lt;secret_access_key&gt;<br> --set ENDPOINT=&lt;public_bucket_endpoint&gt; --set BUCKET_NAME=&lt;bucket_name&gt;<br> --set BACKUP_NAME=&lt;backup_name&gt; --set PVC_NAMES[0]=&lt;pvc_name1&gt;<br> --set PVC_NAMES[1]=&lt;pvc_name2&gt; --set CHART_TYPE=backup<br> --set BACKUP_TYPE=&lt;backup_type&gt; --set SCHEDULE_TYPE=&lt;schedule_type&gt;<br> --set SCHEDULE_INFO=&lt;schedule_info&gt; --name &lt;release_name&gt;</code></p>

5. Verify that your data backup or restore completed successfully. </br>
  **Backup**:
  1. Verify that the `ibm-storage-backup` pod has a status of **Running**.
    ```
    oc get pods | grep backup
    ```
    {: pre}

    Example output:
    ```
    ibm-storage-backup                        1/1     Running             0          64m
    ```
    {: screen}

  2. Review the logs of the `ibm-storage-backup` pod to make sure that your backup was successful. When you see the `... backup completed` message in the event logs, your backup completed successfully.

    ```
    oc logs ibm-storage-backup
    ```
    {: pre}

    Example output for daily backups:<br>

    ```
    [2019-04-18 16:01:51,157] [utilities : 151] [INFO] *****************Start logging to ./Backup.log
    [2019-04-18 16:01:51,158] [backup : 48] [INFO] Starting backup:
    [2019-04-18 16:01:51,158] [configureOS : 66] [INFO] Configuring duplicity with IBM CloudObjectStorage i.e s3.
    [2019-04-18 16:01:51,158] [backup : 62] [INFO] Configuration done!!!
    [2019-04-18 16:01:51,158] [backup : 78] [INFO] Got all required input from config file!!
    [2019-04-18 16:01:52,366] [backup : 119] [WARNING] Incremental backup was not created
    [2019-04-18 16:01:52,366] [backup : 120] [INFO] duplicity  --no-encryption incremental /myvol s3://s3.us-south.cloud-object-storage.appdomain.cloud/mybucket/helm-backup command failed due to Fatal Error: Unable to start incremental backup.  Old signatures not found and incremental specified

    [2019-04-18 16:01:52,367] [backup : 121] [INFO] A full backup is required before incremental backups can begin. Creating a one-time full backup and will run incremental backups for scheduled backups.
    [2019-04-18 16:01:54,357] [backup : 129] [INFO] Full backup completed
    [2019-04-18 16:01:54,357] [backup : 130] [INFO] Local and Remote metadata are synchronized, no sync needed.
    Last full backup date: none
    --------------[ Backup Statistics ]--------------
    StartTime 1555603313.31 (Thu Apr 18 16:01:53 2019)
    EndTime 1555603313.32 (Thu Apr 18 16:01:53 2019)
    ElapsedTime 0.01 (0.01 seconds)
    SourceFiles 3
    SourceFileSize 20495 (20.0 KB)
    NewFiles 3
    NewFileSize 20495 (20.0 KB)
    DeletedFiles 0
    ChangedFiles 0
    ChangedFileSize 0 (0 bytes)
    ChangedDeltaSize 0 (0 bytes)
    DeltaEntries 3
    RawDeltaSize 15 (15 bytes)
    TotalDestinationSizeChange 183 (183 bytes)
    Errors 0
    -------------------------------------------------

    [2019-04-18 16:01:54,357] [backup : 162] [INFO] Scheduling backup as per configurations, please do not stop this program or run this in background !!!
    [2019-04-18 16:01:54,358] [backup : 166] [INFO] Schedule info is: ['daily']
    [2019-04-18 16:01:54,358] [backup : 172] [INFO] Scheduled for daily!!!
    ```
    {: screen}

6.  Verify that your data is successfully backed up or restored.
    * **Backup**:
      1. Find your {{site.data.keyword.cos_full_notm}} service instance in the [{{site.data.keyword.cloud_notm}} resource list](https://cloud.ibm.com/resources).
      2. From the navigation, select **Buckets** and click on the bucket that you used in your backup configuration. Your backup is displayed as an object in your bucket.
      3. Review the compressed files. You can download the `*.gz` file, extract the file, and verify the backed-up data.

    * **Restore**:
      1.  Create a `deployment.yaml` file with a pod that mounts the PVC that contains your restored data. The following example deploys an `nginx` pod that mounts the PVC on the `/test` mount directory.
            ```yaml
            apiVersion: apps/v1
            kind: Deployment
            metadata:
              name: restore
              labels:
              app: nginx
            spec:
              selector:
                matchLabels:
                  app: nginx
              template:
                metadata:
                  labels:
                    app: nginx
                spec:
                  containers:
                    - image: nginx
                      name: nginx
                      volumeMounts:
                      - name: <volume_name> # Example: my_volume
                        mountPath: <mount_path> # Example: /test
                    volumes:
                    - name: <volume_name> # Example: my_volume
                      persistentVolumeClaim:
                        claimName: <pvc_name> # Example: my_pvc
            ```
            {: codeblock}

            <table>
            <caption>Understanding the <code>deployment.yaml</code> file components</caption>
            <thead>
            <th colspan=2><img src="images/idea.png" alt="Idea icon"/> Understanding the YAML file components</th>
            </thead>
            <tbody>
            <tr>
            <td><code>spec.containers.image</code></td>
            <td>The name of the image that you want to use. To list available images in your {{site.data.keyword.registryshort_notm}} account, run <code>ibmcloud cr image-list</code>.</td>
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

      2.  Create the deployment.
            ```
            oc apply -f deployment.yaml
            ```
            {: pre}

      3.  Verify that your pod has a status of **Running**.

            If you find that your `ibm-storage-restore` pod does not reach a **Completed** or **CrashLoopBackOff** status, restoring your data might have failed. Run `oc logs ibm-storage-restore` to find the root cause for the failure.
            {: tip}

            ```
            oc get pods | grep restore
            ```
            {: pre}

            Example output:
            ```
            restore-7dfc6f4c78-wkcqp                  1/1     Running             0          3m54s
            ```
            {: screen}

      4.  Log in to your pod.
            ```
            oc exec <pod_name> -it bash
            ```
            {: pre}

      5.  Navigate to the mount directory that you specified in your deployment YAML.
            ```
            cd <mount_directory>
            ```
            {: pre}

      6.  List the files in your mount directory to verify that all your data is restored to the mount directory.
            ```
            ls
            ```
            {: pre}

      7.  Delete the Helm chart installation from your cluster. This step is required if you restored data to a block storage PVC. Block storage is mounted with a RWO access mode. This access allows only one pod to be mounted to the block storage at a time. Because the `ibm-storage-restore` pod already mounts the PVC, you must remove the pod to release the PVC so that you can mount the PVC to a different pod in your cluster.
            ```
            helm delete <release_name> --purge
            ```
            {: pre}

      8.  You successfully restored your backup. You can now mount the PVC that binds the PV to any other pod in your cluster to access the restored files. If the container data that was backed up included a non-root user, you must add non-root permissions to your new container. For more information, see [Adding non-root user access to volumes](/docs/openshift?topic=openshift-cs_troubleshoot_storage#cs_storage_nonroot).


