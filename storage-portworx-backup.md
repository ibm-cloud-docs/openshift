---

copyright: 
  years: 2014, 2023
lastupdated: "2023-05-03"

keywords: portworx, openshift

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}


## Backing up and restoring apps and data with PX-Backup
{: #storage_portworx_backup}

PX-Backup is a Portworx proprietary backup solution that is compatible with any {{site.data.keyword.openshiftlong_notm}} cluster. You can use PX-Backup to back up and restore {{site.data.keyword.openshiftlong_notm}} resources, apps and data across multiple clusters. For more information on PX-Backup, see [Understanding PX-Backup](https://backup.docs.portworx.com/understand/){: external}.
{: shortdesc}

To back up the data in your persistent volumes, you must have a storage class that supports snapshots in your cluster. Clusters with Portworx Enterprise have storage classes available that support snapshots by default. However, for clusters that don't have Portworx Enterprise, you must have a storage classes with snapshot support to back up your persistent volume data. The {{site.data.keyword.block_storage_is_short}} driver, {{site.data.keyword.blockstorageshort}} driver, and the {{site.data.keyword.filestorage_short}} driver don't have storage classes that support snapshots. If you have workloads that use these drivers, you can use PX-Backup to back up your apps, but not the data in the persistent volumes. For more information see [Backing up and restoring cluster data with PX-Backup](#px-backup-and-restore).
{: important}

### Installing PX-Backup on a {{site.data.keyword.openshiftlong_notm}} cluster
{: #px-backup-install}

Install PX-Backup on a {{site.data.keyword.openshiftlong_notm}} cluster in your {{site.data.keyword.cloud_notm}} account. After you install PX-backup on one cluster in your account, you can use it to back up or restore data and apps for any cluster in that same account.
{: shortdesc}

Before you begin:
- Make sure that your cluster meets the [minimum Portworx requirements](https://docs.portworx.com/start-here-installation/){: external}. 
- [Log in to your cluster](/docs/openshift?topic=openshift-access_cluster).
- Provision and attach 320Gi of block storage to your cluster. See [Setting up classic {{site.data.keyword.cloud_notm}} Block Storage](/docs/openshift?topic=openshift-block_storage) or [Setting up Block Storage for VPC](/docs/openshift?topic=openshift-vpc-block).


If you are installing PX-Backup in a newly provisioned cluster, [you must log in to it at least once](/docs/openshift?topic=openshift-access_cluster) before beginning the installation.
{: important}


1. Open the PX-Backup service from the [{{site.data.keyword.cloud_notm}} catalog](https://cloud.ibm.com/catalog/services/px-backup-for-kubernetes){: external}.
2. Select the same location where the  cluster you want to install PX-Backup on is located. You can find the location of your cluster from the {{site.data.keyword.openshiftlong_notm}} dashboard.
3. Enter the name for your PX-Backup service in the **Service name** field.
4. Select the resource group where you want to create the PX-Backup service.
5. In the **Tag** field, enter the name of the cluster where you want to install PX-Backup. After you complete the installation, you can't see the name of the cluster where you installed PX-Backup. To find the cluster more easily later, make sure that you enter the cluster name and any additional information as tags.
6. Enter your {{site.data.keyword.cloud_notm}} API key. After you enter the API key, the **Kubernetes or OpenShift cluster name** field appears. If you don't have an {{site.data.keyword.cloud_notm}} API key, see [Creating an API key](/docs/account?topic=account-userapikey#create_user_key) to create one.
7. In the **Kubernetes or OpenShift cluster name** field, select the cluster where you want to install PX-Backup.
8. Enter the name of the {{site.data.keyword.redhat_openshift_notm}} project where you want to install your PX-Backup service components. Do not use the `kube-system` or `default` namespace. If the {{site.data.keyword.redhat_openshift_notm}} project that you enter does not already exist in your cluster, it is automatically created during the installation.
9. Select an existing storage class in your cluster to provision persistent volumes for the PX-Backup service. The service uses this storage to store service metadata and is not used to back up your apps and data. [Your apps and data are backed up to an {{site.data.keyword.cos_full_notm}} service instance](#px-backup-storage).
10. Click **Create** to begin the PX-Backup installation. The installation may take a few minutes to complete.
11. [Verify that your PX-Backup service is installed correctly](#px-backup-verify).


### Verifying your PX-Backup installation
{: #px-backup-verify}

Verify that PX-Backup is correctly installed on your cluster.
{: shortdesc}


From the console

1. From the {{site.data.keyword.cloud_notm}} [Resource list](https://cloud.ibm.com/resources){: external}, find the PX-Backup service that you created.
1. Review the **Status** column to see if the installation succeeded or failed. The status might take a few minutes to update.
1. If the status changes to **Active**, verify that the PX-Backup pods, services and jobs are running in your cluster.
    1. From the {{site.data.keyword.cloud_notm}} [Resource list](https://cloud.ibm.com/resources){: external}, select the cluster where you installed PX-Backup.
    1. Open the {{site.data.keyword.redhat_openshift_notm}} web console.
    1. Click on **Projects**.
    1. Select the namespace where you installed the PX-Backup service components.
    1. In the **Inventory** section, select the option to display your pods.
    1. In the **Pods** table, verify that the status of each pod is **Running**.
    1. Click on **Networking>Routes**.
    1. Find the **px-backup-ui** route and verify that a URL is listed in the **Location** column.
    1. Click **Workloads>Jobs**.
    1. Verify that the **pxcentral-post-install-hook** job is complete.

From the CLI

1. From the {{site.data.keyword.cloud_notm}} [Resource list](https://cloud.ibm.com/resources){: external}, find the PX-Backup service you created.
2. Review the **Status** column to see if the installation succeeded or failed. The status might take a few minutes to update.
3. If the status changes to **Active**, verify that the PX-Backup pods are running in your cluster.
    1. [Access your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-access_cluster).
    2. Run the command to verify that the installation has completed.
        ```sh
        oc get po -n <px_backup_namespace> -ljob-name=pxcentral-post-install-hook  -o wide | awk '{print $1   $3}' | grep -iv error
        ```
        {: pre}

        Example output
        ```sh
        NAMESTATUS
        pxcentral-post-install-hook-5b86qCompleted
        ```
        {: screen}


### Logging in to the PX-Backup console
{: #px-backup-ui}

Access the PX-Backup console through the URL supplied in the {{site.data.keyword.openshiftlong_notm}} dashboard for the cluster where you installed the service.
{: shortdesc}

For VPC clusters

1. From the {{site.data.keyword.cloud_notm}} [Resource list](https://cloud.ibm.com/resources){: external}, select the cluster where you installed PX-Backup.
1. Open the {{site.data.keyword.redhat_openshift_notm}} web console .
1. Click on **Networking>Routes**.
1. Find the **px-backup-ui** route and click on the URL that is listed in the **Location** column to open the PX-Backup console.
1. Log in to the PX-Backup console. If you are the first user to access the console, you must log in in with the username `admin` and the password `admin`. You are redirected to a registration page to set a unique username and password. Subsequent users must register a new account to access the console.


For public classic clusters

1. From the {{site.data.keyword.cloud_notm}} [Resource list](https://cloud.ibm.com/resources){: external}, select the cluster where you installed PX-Backup.
1. Open the {{site.data.keyword.redhat_openshift_notm}} web console .
1. Click on **Networking>Routes**.
1. Find the **px-backup-ui** route and note the IP address and node port listed in the **Locations** column.
1. Copy and paste the IP address and node port into your web browser to open the PX-Backup console.
1. Log in to the PX-Backup console. If you are the first user to access the console, you must log in in with the username `admin` and the password `admin`. You are redirected to a registration page to set a unique username and password. Subsequent users must register a new account to access the console.


For private classic clusters, [expose the **px-backup-ui** service on your private cluster to access the PX-Backup console](/docs/containers?topic=containers-managed-ingress-setup).
{: note}

### Adding a backup location to your PX-Backup service
{: #px-backup-storage}

Create an {{site.data.keyword.cos_full_notm}} instance and bucket, and add them as a backup location to your PX-Backup service.
{: shortdesc}

Before you begin, [log in to the PX-Backup console](#px-backup-ui). Note that if you are the first user to access the console, you must login in with the username `admin` and the password `admin`. You are redirected to a registration page to set a unique username and password. Subsequent users must register a new account to access the console.

1. [Create your {{site.data.keyword.cos_full_notm}} service instance](/docs/openshift?topic=openshift-storage-cos-understand#create_cos_service).
2. [Create service credentials for your {{site.data.keyword.cos_full_notm}} service instance](/docs/openshift?topic=openshift-storage-cos-understand#create_cos_secret). Be sure to enable HMAC authentication by clicking **Advanced Options** in the **Create credential** dialog box and switching the **Include HMAC Credential** parameter to **On**.
3. Expand your credentials in the service credentials table. Note the **`access_key_id`** and the **`secret_access_key`** in the **`cos_hmac_keys`** section.
4. [Create a storage bucket in your {{site.data.keyword.cos_full_notm}} instance](/docs/cloud-object-storage?topic=cloud-object-storage-getting-started-cloud-object-storage).
5. Click on your bucket and note its location.
6. Open the bucket configuration page and note the endpoint that you must use to connect to your {{site.data.keyword.cos_full_notm}} instance.
    - If you installed PX-Backup on a private classic cluster, note the **private** endpoint.
    - If you installed PX-Backup on a private VPC cluster, note the **direct** endpoint.
    - For all other cluster types, note the **public** endpoint.
7. In the PX-Backup console, click **Backups**.
8. Click **Settings>Cloud Settings**.
9. Create a cloud account to specify your {{site.data.keyword.cos_full_notm}} instance as the backup location where your data and apps are stored.
    1. For the cloud provider, choose **AWS / S3 Compliant Object Store**.
    2. Enter a name for your cloud account.
    3. Enter the **`access_key_id`** that you retrieved earlier.
    4. Enter the **`secret_access_key`** that you retrieved earlier.
    5. Click **Add+** and return to the **Cloud Settings** page.
10. In the **Backup Locations** section, add your {{site.data.keyword.cos_full_notm}} bucket as the backup location for your PX-Backup service.
    1. Enter a name for your backup location.
    2. Select the cloud account that you created earlier.
    3. In the **Path/Bucket** field, enter the name of your bucket.
    4. In the **Region** field, enter the location of your bucket that you retrieved earlier.
    5. In the **Endpoint** field, enter the endpoint for your bucket that you retrieved earlier.
    6. Click **Add+** to create the backup location.

### Adding a {{site.data.keyword.openshiftlong_notm}} cluster to your PX-Backup service
{: #px-backup-cluster}

Add the {{site.data.keyword.openshiftlong_notm}} cluster that you want to back up with PX-Backup. You can select any cluster in your account, including the cluster where you installed PX-Backup.
{: shortdesc}

Before you begin:
- [Log in to the PX-Backup console](#px-backup-ui).
- [Log in to your account. If applicable, target the appropriate resource group. Set the context for your cluster.](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure)

The `kubeconfig` in clusters with PX-Backup expires after 24 hours. To prevent your cluster's `kubeconfig` file from expiring, set the context with your cluster using the `--admin` option.
`
ibmcloud oc cluster config --cluster <cluster_name> --admin
`
{: tip}

Adding a cluster:

1. In the PX-Backup console, click **Backups**.
2. Click **Add Cluster**.
3. Enter the name of the cluster that you want to back up.
4. In the CLI, get the `kubeconfig` file output for your cluster. Make sure that you have set the context to your cluster with the `--admin` option to prevent the `kubeconfig` from expiring.
    ```sh
    oc config view --flatten --minify
    ```
    {: pre}

5. Copy the entire `kubeconfig` CLI output and paste it into the **`Kubeconfig`** field in the PX-Backup console.
6. Select **Others** as your **Kubernetes Service**.
7. If the cluster that you want to add to the PX-Backup service does not have Portworx installed in it, [you must install Stork onto the cluster](#px-backup-stork). If you installed Portworx Enterprise in your cluster, Stork is installed by default.
8. Click **Submit**. If your cluster is successfully added, you are redirected to the **Backups** page. Make sure that your cluster is listed.
9. [Back up data from your cluster](#px-backup-and-restore).
10. Repeat these steps to add more clusters to your PX-Backup service.

#### Installing Stork on a non-Portworx cluster
{: #px-backup-stork}

If a cluster that you want to back up with PX-Backup does not have Portworx Enterprise installed on it, you must install Stork on to the cluster before adding it to your PX-Backup service.
{: shortdesc}

1. From the **Add Cluster** page in the PX-Backup console, copy the command to install Stork on a **Non-PX** cluster.
2. Open a text editor and paste the command.
3. Copy the URL in the command and enter it in to your web browser to open the YAML file for the Stork installation.
4. Copy and paste the entire YAML file into a new file in your text editor.
5. If the cluster you want to add is a private cluster, find the **image** field and replace `openstorage/stork:<version_number>` with `icr.io/ext/portworx/stork:<version_numer>`. To find the latest available version of Stork, see the [Stork releases](https://github.com/libopenstorage/stork/releases){: external}.
    ```sh
    - --health-monitor-interval=120
    - --webhook-controller=false
    image: openstore/stork:2.6.2
    imagePullPolicy:Always
    resources:
      requests:
         cpu: '0.1'
      name: stork
   serviceAccountName: stork-account  
    ```
    {: screen}

6. Save the file and run the command to apply the file to your cluster and install Stork.
    ```sh
    oc apply -f <file_name>.yaml
    ```
    {: pre}

7. Verify that Stork is successfully installed on your cluster and that all pods are running.
    ```sh
    oc get deployment -n kube-system | grep stork
    ```
    {: pre}

    Example output

    ```sh
    stork                3/3   3      3      7d20h
    ```
    {: screen}



### Backing up and restoring cluster data with PX-Backup
{: #px-backup-and-restore}


To back up data from your cluster or to restore data to your cluster, refer to the [PX-Backup documentation](https://backup.docs.portworx.com/use-px-backup/backup-restore/){: external}.
{: shortdesc}

**Back up apps and data from your cluster to {{site.data.keyword.cos_full_notm}}**: 
You can back up an entire cluster namespace, single apps, and the data that is stored in your persistent volumes to the {{site.data.keyword.cos_full_notm}} service instance that you set up as your backup location. Note that to back up data in persistent volumes, you must have a CSI snapshot storage class in your cluster. PX-Backup uses this storage class to first take a snapshot of your data and then sends this data to your {{site.data.keyword.cos_full_notm}} backup location. For more information, see the [PX-Backup documentation](https://backup.docs.portworx.com/use-px-backup/backup-restore/create-backup/perform-backup/){: external}.

**Restore any backup that you created to another cluster**: 
You can restore an entire namespace, your apps, or your data to any cluster that you added to the PX-Backup service. Use this PX-Backup capability if you want to migrate apps and data from one cluster to another. For more information, see the [PX-Backup documentation](https://backup.docs.portworx.com/use-px-backup/backup-restore/restore-backup/){: external}.

### Upgrading PX-Backup
{: #px-backup-upgrade}

Follow the Portworx documentation to [upgrade PX-backup](https://1.2.backup.docs.portworx.com/use-px-backup/upgrade/){: external}
{: shortdesc}





