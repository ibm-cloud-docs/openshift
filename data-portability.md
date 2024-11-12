---

copyright:
  years: 2024, 2024
lastupdated: "2024-11-12"

keywords: data, portability

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}

# Understanding data portability for {{site.data.keyword.openshiftlong_notm}}
{: #data-portability}

[Data Portability](#x2113280){: term} involves a set of tools and procedures that enable customers to export the digital artifacts that are needed to implement similar workload and data processing on different service providers or on-premises software. It includes procedures for copying and storing the service customer content, including the related configuration that is used by the service to store and process the data, on the customer’s own location.
{: shortdesc}

## Responsibilities
{: #data-portability-responsibilities}

{{site.data.keyword.Bluemix_notm}} provides interfaces and instructions to guide the customer to copy and store the service customer content, including the related configuration, on their own selected location.

The customer is responsible for the use of the exported data and configuration for data portability to other infrastructures, which includes:

- The planning and execution for setting up alternative infrastructure on different cloud providers or on-premises software that provide similar capabilities to the {{site.data.keyword.IBM_notm}} services.
- The planning and execution for the porting of the required application code on the alternative infrastructure, including the adaptation of customer's application code, deployment automation, and so on.
- The conversion of the exported data and configuration to the format that's required by the alternative infrastructure and adapted applications.

For more information, see [Your responsibilities with {{site.data.keyword.openshiftlong_notm}}](/docs/openshift?topic=openshift-responsibilities_iks).


## Data export procedures
{: #data-portability-procedures}

{{site.data.keyword.openshiftlong_notm}} provides mechanisms to export your content that was uploaded, stored, and processed using the service.


### Exporting data by using the `oc` CLI
{: #export-procedure-kubectl}





You can use the `oc` CLI to export and save the resources from your cluster. For more information, see the [Kubernetes documentation](https://docs.openshift.com/container-platform/4.17/cli_reference/openshift_cli/developer-cli-commands.html){: external}.

Example `oc get` [commands](https://docs.openshift.com/container-platform/4.17/cli_reference/openshift_cli/developer-cli-commands.html#oc-get){: external}.



```sh
oc get pod pod1 -o yaml
```
{: pre}


### Exporting data by using Velero
{: #export-velero}

The following example exports data from {{site.data.keyword.openshiftlong_notm}} to {{site.data.keyword.cos_full_notm}}. However, you can adapt these steps to export data to other s3 providers. 

1. [Install the Velero CLI](https://velero.io/docs/v1.14/basic-install/){: external}.
1. [Install {{site.data.keyword.openshiftlong_notm}} CLI](/docs/openshift?topic=openshift-cli-install).
1. [Create an IBM Cloud Object Storage instance](/docs/cloud-object-storage?topic=cloud-object-storage-provision#provision-instance) to store Velero resources.
1. [Create a COS bucket](/docs/cloud-object-storage?topic=cloud-object-storage-getting-started-cloud-object-storage#gs-create-buckets). Enter a unique name, then select `cross-region` for resiliency and `us-geo` for region.
1. [Create new HMAC credentials](/docs/cloud-object-storage?topic=cloud-object-storage-uhc-hmac-credentials-main) with the **Manager** role.
1. Create a local credentials file for Velero. Enter the HMAC credentials from the prior step.

    ```txt
    [default]
    aws_access_key_id=<HMAC_access_key_id>
    aws_secret_access_key=<HMAC_secret_access_key>
    ```
    {: codeblock}

1. Create an [IAM Access Group](/docs/account?topic=account-groups&interface=ui) and assign the Service ID of the COS credentials from Step 3 to Cloud Object Storage. Include **Manager** and **Viewer** permissions. This gives Velero access to read and write to the COS bucket that you created.

1. [Access your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-access_cluster).

1. Install Velero on your cluster. If you selected a different region for the COS instance, adjust the command with the appropriate endpoints. By default, this targets all storage in the cluster for backup.

    ```sh
    velero install --provider aws --bucket <bucket-name> --secret-file <hmac-credentials-file> --use-volume-snapshots=false --default-volumes-to-fs-backup --use-node-agent --plugins velero/velero-plugin-for-aws:v1.9.0 --image velero/velero:v1.13.0 --backup-location-config region=us-geo,s3ForcePathStyle="true",s3Url=https://s3.direct.us.cloud-object-storage.appdomain.cloud
    ```
    {: pre}

1. Check the Velero pod status.
    ```sh
    kubectl get pods -n velero
    ```
    {: pre}

1. Create a backup of the cluster. The following command backs up all PVCs, PVs, and pods from the `default` namespace. You can also apply filters to target specific resources or namespaces.
    ```sh
    velero backup create mybackup --include-resources pvc,pv,pod --default-volumes-to-fs-backup --snapshot-volumes=false --include-namespaces default --exclude-namespaces kube-system,test-namespace
    ```
    {: pre}

1. Check the backup status.
    ```sh
    velero backup describe mybackup
    ```
    {: pre}


You can now view or download the cluster resources from your {{site.data.keyword.cos_full_notm}} bucket.

You can also migrate the clusters resources that you backed up to {{site.data.keyword.cos_full_notm}} to another s3 instance and bucket in a different cloud provider.

For more information about restoring Velero snapshots, see [Cluster migration](https://velero.io/docs/v1.14/migration-case/){: external}.

To see an example scenario that uses `velero` in IBM Cloud for migrating from a Classic to VPC cluster, see [Migrate Block Storage PVCs from an IBM Cloud Kubernetes Classic cluster to VPC cluster](https://community.ibm.com/community/user/cloud/blogs/baker-pratt/2024/07/15/migrate-block-storage-pvcs-from-an-ibm-cloud-kuber){: external}.
{: tip}

### Other options for exporting data
{: #data-other}

| Title | Description |
| --- | --- |
| [`Rclone`](https://rclone.org/){: external} | Review the [Migrating Cloud Object Storage (COS) apps and data between IBM Cloud accounts](https://cloud.ibm.com/docs/openshift?topic=openshift-storage-cos-app-migration) tutorial to see how to move data that is one COS bucket to another COS bucket in IBM Cloud or in another cloud provider by using `rclone`. |
| [OpenShift APIs for Data Protection](https://access.redhat.com/articles/5456281){: external} (OADP) | OADP (OpenShift APIs for Data Protection) is an operator that Red Hat has created to create backup and restore APIs for OpenShift clusters. For more information, see [Backup and restore Red Hat OpenShift cluster applications with OADP](https://developer.ibm.com/tutorials/awb-backup-and-restore-redhat-openshift-clusters-with-oadp/){: external} and the [OADP documentation](https://docs.openshift.com/container-platform/4.17/backup_and_restore/application_backup_and_restore/oadp-intro.html){: external} |
| [Backing up and restoring apps and data with Portworx Backup](/docs/openshift?topic=openshift-storage_portworx_backup#px-backup-storage) | This document walks you through setting up PX Backup. You can configure clusters from other providers and restore data from IBM Cloud to the new provider. |
| [Wanclouds](https://wanclouds.net/){: external} VPC+ DRaaS (VPC+ Disaster Recovery as a Service) | Review the Wanclouds Multi Cloud Backup, Disaster Recovery and Optimization as a Service. For more information, see the [Wanclouds documentation](https://docs.wanclouds.net/ibm/About-VPC-DRaas/){: external}. |
{: caption="Other options for exporting data" caption-side="bottom"}


## Exported data formats
{: #data-portability-data-formats}


- Cluster resources exported via `oc` can be exported in several file types. For more information, see the [Output options](https://kubernetes.io/docs/reference/kubectl/#output-options){: external}.

- Cluster resources exported via `velero` are exported in JSON format. For more information, see the [Output file format](https://velero.io/docs/v1.14/output-file-format/){: external}.




## Data ownership
{: #data-ownership}

All exported data is classified as customer content and is therefore applied to them full customer ownership and licensing rights, as stated in [IBM Cloud Service Agreement](https://www.ibm.com/support/customer/csol/terms/?id=Z126-6304_WS).
