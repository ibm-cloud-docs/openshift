---

copyright: 
  years: 2022, 2025
lastupdated: "2025-04-17"


keywords: kubernetes, openshift

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}

# Why does my {{site.data.keyword.filestorage_vpc_short}} deployment fail due to a permissions error?
{: #ts-storage-vpc-file-non-root}
{: support}

[Virtual Private Cloud]{: tag-vpc}


Your app that uses {{site.data.keyword.filestorage_vpc_short}} fails with a permissions error.
{: tsSymptoms}

You created your own storage class to use with an existing file share, but did not specify the correct `uid` and `gid`. When a process runs on UNIX and Linux, the operating system identifies a user with a user ID (UID) and group with a group ID (GID). These IDs determine which system resources a user or group can access. For example, if the file storage user ID is 12345 and its group ID is 6789, then the mount on the host node and in the container must have those same IDs. The container’s main process must match one or both of those IDs to access the file share.
{: tsCauses}

You can resolve the issue in one of the following ways.
{: tsResolve}


- If you need your app to run as non-root, create your own storage class with the correct `uid` and `gid` that your app needs. 

- If you want to run your app as as root user, edit your deployment to use `fsGroup: 0`.



## Create your own storage class and specify the `uid` and `gid` your app needs
{: #ts-vpc-new-sc}

If you want to use {{site.data.keyword.filestorage_vpc_short}} with static provisioning, you must reference the correct `uid` and `gid`.

1. Create a storage class with the correct `uid` and `gid` that your app needs.

    ```yaml
    apiVersion: storage.k8s.io/v1
    kind: StorageClass
    metadata:
      name: custom-storageclas
    provisioner: vpc.file.csi.ibm.io
    mountOptions:
        - hard
        - nfsvers=4.0
        - sec=sys
    parameters:
      profile: "custom-iops"            # The VPC Storage profile used. /docs/vpc?topic=vpc-block-storage-profiles&interface=ui#tiers-beta
      iops: "400"                       # Default IOPS. User can override from secrets
      billingType: "hourly"             # The default billing policy used. User can override this default
      encrypted: "false"                # By default, all PVC using this class will only be provider managed encrypted. The user can override this default
      encryptionKey: ""                 # If encrypted is true, then a user must specify the encryption key used associated KP instance
      resourceGroup: ""                 # Use resource group if specified here. Otherwise, use the one mentioned in storage-secrete-store
      zone: ""                          # By default, the storage vpc driver will select a zone. The user can override this default
      tags: ""                          # A list of tags "a, b, c" that will be created when the volume is created. This can be overidden by user
      classVersion: "1"
      uid: "1234"                           # The initial user identifier for the file share.
      gid: "5678"                           # The initial group identifier for the file share.
    reclaimPolicy: "Delete"
    allowVolumeExpansion: true
    ```
    {: codeblock}

1. Create the customized storage class in your cluster.

    ```sh
    oc apply -f custom-storageclass.yaml
    ```
    {: pre}

1. Verify that your storage class is available in the cluster.

    ```sh
    oc get sc
    ```
    {: pre}

    Example output
    
    ```sh
    NAME                                          PROVISIONER
    ibmc-vpc-file-10iops-tier                     vpc.file.csi.ibm.io
    ibmc-vpc-file-3iops-tier                      vpc.file.csi.ibm.io
    ibmc-vpc-file-5iops-tier                      vpc.file.csi.ibm.io
    ibmc-vpc-file-retain-10iops-tier              vpc.file.csi.ibm.io
    ibmc-vpc-file-retain-3iops-tier               vpc.file.csi.ibm.io
    ibmc-vpc-file-retain-5iops-tier               vpc.file.csi.ibm.io
    ibmc-vpc-file-custom                         vpc.file.csi.ibm.io
    ```
    {: screen}

1. [Add filestorage to your app](/docs/openshift?topic=openshift-storage-file-vpc-apps)

## Edit your app to run as root with `fsGroup: 0`
{: #ts-vpc-yaml-sc}

1. Log in to your cluster. 

1. Identify the deployment in your cluster that you want to edit.
    ```sh
    kubectl get deployments
    ```
    {: pre}

1. Edit the deployment by adding `fsGroup: 0` in the `securityContext` section of your deployment.

    ```sh
    kubectl get deployment -o yaml YOUR-DEPLOYMENT
    ```
    {: pre}

    ```yaml
    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: <deployment_name>
      labels:
        app: <deployment_label>
    spec:
      securityContext:
        fsGroup: 0
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
            claimName: PVC-NAME
    ```
    {: codeblock}

1. Apply the changes to your deployment.
