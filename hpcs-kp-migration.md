---

copyright:
  years: 2025, 2026
lastupdated: "2026-01-08"


keywords: key protect, hpcs, kp, migrate, odf, encryption

subcollection: openshift

---


{{site.data.keyword.attribute-definition-list}}


# Migrating from Hyper Protect Crypto Services to Key Protect
{: #migrate_hpcs_kp}


Migrate your Hyper Protect Crypto Services (HPCS) encryption for ODF to use Key Protect (KP) instead. 
{: shortdesc}


## Considerations for custom storage classes
{: #custom-storageclass}

If you are migrating between separate clusters and are using a custom storage class, then you must make sure that the storage class name is the same for both the source and target cluster. Create a storage class in the source cluster using the HPCS instance key and save a backup in the COS bucket. Then, create a storage class with the same name on the target cluster using the KP instance key. After you create the storage class on both clusters, continue with the migration steps.

If you are migrating a single cluster to use KP instead of HPCS and are using a custom storage class, then you must create custom storage classes that use the same name with both the HPCS and KP instance keys. However, a cluster cannot have two storage classes with the same name, so it is important to ensure that you complete these steps in the following order. 

    1. If you do not already have one on the cluster, create a storage class with the HPCS instance key.
    2. Create backups for the application namespace, original custom storage class, and PVC.
    3. Upload the backups into the COS bucket. 
    4. Delete the storage class you created with the HPCS instance key. 
    5. Create a storage class with the KP instance key, using the same name as the previous storage class you created and deleted.
    6. Restore the backups on the cluster. 


## Migration steps
{: #migration-steps}

Follow these steps if you want to migrate data from a source cluster that uses ODF and HPCS to a target cluster that uses ODF and KP. Or, you can migrate an individual cluster that uses HPCS to instead use KP, in which case the source cluster and target cluster are the same. 


1. Install the Red Hat OpenShift API for Data Protection (OADP) from OperatorHub onto both the source and target clusters.
    1. Navigate to the clusters page.
    2. Click `OpenShift Web Console`.
    3. Click `OperatorHub` and search for the OADP operator. Follow the prompts to install the operator.
    4. Repeat these steps for the target cluster. 


2. Create an IBM Cloud Object Storage (COS) bucket. 
    1. Navigate to the [COS overview page](https://cloud.ibm.com/objectstorage/overview){: external} and click **Instances**. 
    2. Select an instance to create a bucket in. If you do not have a COS instance, follow the prompts to create one. 
    3. In the COS instance, click **Create bucket**. 
    4. Click the new bucket, then click **Overview**.
    5. Save the name of the bucket, the region that the bucket is located in, and the public endpoint URL to reference later.
    


3. Create a service credential in the COS instance.
    1. [Select the same COS instance](https://cloud.ibm.com/objectstorage/instances){: external} that you created the bucket in, then click **Service credentials**.
    2. Create a credential with the `Object Writer` role and the `Manager permission`. Select the option to include HMAC credential. 

    
    3. In the service credentials list, click to expand the service credential you just created. Note the `access_key_id` and `secret_access_key` and save them in a secure file as `aws_access_key_id` and `aws_secret_access_key` respectively. 

    
4. On both the source and target cluster, create a secret with the credentials you saved. Note the name of the secret to reference later. 

    ```sh
    oc create secret generic cloud-credentials -n openshift-adp --from-file cloud=<hmac_file_name>
    ```
    {: pre}
   
5. In both the target and source cluster, create a DataProtectionApplication ClusterResource to configure OADP for the cluster. Use the same ClusterResource for both clusters.

    ```yaml
    apiVersion: oadp.openshift.io/v1alpha1
    kind: DataProtectionApplication
    metadata:
    name: velero-sample
    namespace: openshift-adp
    spec:
    backupLocations:
    - velero:
        config:
            profile: default
            region: <bucket-region>  # The region that the COS bucket is located in
            s3ForcePathStyle: "true"
            s3Url: https://s3.us-south.cloud-object-storage.appdomain.cloud/
        credential:
            key: cloud
            name: <secret-name> # The name of the secret that contains the COS credentials
        default: true
        objectStorage:
            bucket: <bucket-name> # The name of the COS bucket
            prefix: velero
        provider: aws
    configuration:
        nodeAgent:
        enable: true
        uploaderType: restic
        velero:
        defaultPlugins
        - openshift
        - aws
        - csi
    ```
    {: screen}

    Apply the file to each cluster. 

    ```sh
    oc apply -f <filename>
    ```
    {: pre}

6. After you create the DataProtectionApplication resource, verify that OADP pods have deployed in the `openshift-adp` namespace.

    ```sh
    oc get all -n openshift-adp
    ```
    {: pre}

    For each node in the cluster, you should have have a `velero` and `node-agent` pod  and a `velero` batch job. The following example is for a cluster that has three nodes. 

    ```sh
    NAME                                                                 READY   STATUS      RESTARTS   AGE
    pod/auto-en-velero-sample-1-kopia-maintain-job-1762936994449-4hhz5   0/1     Completed   0          177m
    pod/auto-en-velero-sample-1-kopia-maintain-job-1762940894459-v5n5f   0/1     Completed   0          112m
    pod/auto-en-velero-sample-1-kopia-maintain-job-1762944794467-2h77f   0/1     Completed   0          47m
    pod/node-agent-2nnlm                                                 1/1     Running     0          28h
    pod/node-agent-2rlnc                                                 1/1     Running     0          28h
    pod/node-agent-qstkk                                                 1/1     Running     0          28h
    ...

    NAME                                                                 STATUS     COMPLETIONS   DURATION   AGE
    job.batch/auto-en-velero-sample-1-kopia-maintain-job-1762936994449   Complete   1/1           19s        177m
    job.batch/auto-en-velero-sample-1-kopia-maintain-job-1762940894459   Complete   1/1           15s        112m
    job.batch/auto-en-velero-sample-1-kopia-maintain-job-1762944794467   Complete   1/1           14s        47m
    ...
    ```
    {: screen}


7. On the source cluster, create a ClusterResource to backup the application namespace data before migration. If you are migrating an individual cluster rather than migrating between separate clusters, you should also create backup YAML configurations for the StorageClass and PVC. 

    If you are migrating an individual cluster that uses a custom storage class, make sure you have read the information in [Considerations for custom storage classes](#custom-storageclass) before you proceed with creating and restoring backups.
    {: important}

    ```yaml
    apiVersion: velero.io/v1
    kind: Backup
    metadata:
    name: mybackup  
    namespace: openshift-adp
    spec:
    storageLocation: velero-sample-1
    includedNamespaces:
    - default
    - additional-namespace-example  # Include all namespaces you want to backup
    snapshotVolumes: true
    datamover: velero
    snapshotMoveData: true
    ```
    {: screen}
    
    Apply the file to create the backup. 

    ```sh
    oc apply -f <filename>
    ```
    {: pre}

8. Verify that the backup data is stored in the COS bucket. 
    1. Navigate to the [COS overview page](https://cloud.ibm.com/objectstorage/overview){: external} and click **Instances**. 
    2. Select the COS instance, then the bucket where you stored the backup. This is the same bucket you created earlier. 
    3. Click **Objects**.
    4. Check that the backed up data is in the bucket.


9. On the target cluster, create a ClusterResource to migrate and restore the application namespace data on the target cluster. For `backupName`, make sure to specify the name of the backup ClusterResources you created previously.

    ```yaml
    apiVersion: velero.io/v1
    kind: Restore
    metadata:
    name: myrestore
    namespace: openshift-adp
    spec:
    backupName: mybackup # The name of the backup CR 
    includedNamespaces:
    - default
    restorePVs: true
    ```
    {: codeblock}

    Apply the file to restore the data on the target cluster. 

    ```sh
    oc apply -f <filename>
    ```
    {: pre}
