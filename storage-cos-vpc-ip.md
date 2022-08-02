---

copyright:
  years: 2014, 2022
lastupdated: "2022-08-02"

keywords: openshift

subcollection: openshift

---


{{site.data.keyword.attribute-definition-list}}



# VPC: Setting up authorized IP addresses for {{site.data.keyword.cos_full_notm}}
{: #storage_cos_vpc_ip}

You can authorize your VPC Cloud Service Endpoint source IP addresses to access your {{site.data.keyword.cos_full_notm}} bucket. When you set up authorized IP addresses, you can only access your bucket data from those IP addresses; for example, in an app pod.
{: shortdesc}

Minimum required permissions
:   **Manager** service access role for the {{site.data.keyword.openshiftlong_notm}} service.
:   **Writer** service access role for the {{site.data.keyword.cos_full_notm}} service.

**Supported infrastructure provider**:
* VPC

1. [Follow the instructions to install the `ibmc` Helm plug-in](/docs/containers?topic=containers-storage_cos_install). Make sure to install the `ibm-object-storage-plugin` and set the `bucketAccessPolicy` flag to `true`.

2. Create one `Manager` HMAC service credential and one `Writer` HMAC service credential for your {{site.data.keyword.cos_full_notm}} instance.
    * [Creating HMAC credentials from the console](/docs/cloud-object-storage?topic=cloud-object-storage-uhc-hmac-credentials-main).
    * [Creating HMAC credentials from the CLI](/docs/cloud-object-storage?topic=cloud-object-storage-uhc-hmac-credentials-main#uhc-create-hmac-credentials-cli).

3. Encode the `apikey` from your {{site.data.keyword.cos_full_notm}} Manager credentials to base64.

    ```sh
    echo -n "<cos_manager_apikey>" | base64
    ```
    {: pre}

4. Encode the `access-key` and `secret-key` from your {{site.data.keyword.cos_full_notm}} Writer credentials to base64.

    ```sh
    echo -n "<cos_writer_access-key>" | base64
    echo -n "<cos_writer_secret-key>" | base64
    ```
    {: pre}

5. Create a secret configuration file with the values that you encoded. For the `access-key` and `secret-key`, enter the base64 encoded `access-key` and `secret-key` from the Writer HMAC credentials that you created. For the `res-conf-apikey`, enter the base64 encoded `apikey` from your Manager HMAC credentials.
    ```yaml
    apiVersion: v1
    kind: Secret
    metadata:
        name: <secret_name>
      type: ibm/ibmc-s3fs
      data:
    access-key: # Enter your base64 encoded COS Writer access-key
    secret-key: # Enter your base64 encoded COS Writer secret-key
    res-conf-apikey: # Enter your base64 encoded COS Manager api-key
    ```
    {: codeblock}

6. Create the secret in your cluster.

    ```sh
    oc create -f secret.yaml
    ```
    {: pre}

7. Verify that the secret is created.

    ```sh
    oc get secrets
    ```
    {: pre}

8. Create a PVC that uses the secret you created. Set the `ibm.io/auto-create-bucket: "true"` and `ibm.io/auto_cache: "true"` annotations to automatically create a bucket that caches your data.

    ```yaml
    kind: PersistentVolumeClaim
    apiVersion: v1
    metadata:
        name: <pvc_name>
    annotations:
      ibm.io/auto-create-bucket: "true"
      ibm.io/auto-delete-bucket: "false"
      ibm.io/auto_cache: "true"
      ibm.io/bucket: "<bucket_name>"
      ibm.io/secret-name: "<secret_name>"
      ibm.io/secret-namespace: "<secret-namespace>" # By default, the COS plug-in searches for your secret in the same namespace where you create the PVC. If you created your secret in a namespace other than the namespace where you want to create your PVC, enter the namespace where you created your secret.
    spec:
      accessModes:
        - ReadWriteMany
      resources:
        requests:
          storage: 8Gi
      storageClassName: ibmc-s3fs-standard-regional
      volumeMode: Filesystem
    ```
    {: codeblock}

9. Get a list of the Cloud Service Endpoint source IP addresses of your VPC.

    1. Get a list of your VPCs.

        ```sh
        ibmcloud is vpcs
        ```
        {: pre}

    2. Get the details of your VPC and make a note of your Cloud Service Endpoint source IP addresses.

        ```sh
        ibmcloud is vpc <vpc_ID>
        ```
        {: pre}

        Example output
        
        ```sh                                              
        ...                                              
        Cloud Service Endpoint source IP addresses:    Zone         Address      
                                                    us-south-1   10.249.XXX.XX      
                                                    us-south-2   10.249.XXX.XX     
                                                    us-south-3   10.249.XXX.XX
        ```
        {: screen}

10. Verify that the Cloud Service Endpoint source IP addresses of your VPC are authorized in your {{site.data.keyword.cos_full_notm}} bucket.
    1. [From your {{site.data.keyword.cos_full_notm}} resource list](https://cloud.ibm.com/resources), select your {{site.data.keyword.cos_full_notm}} instance and select the bucket that you specified in your PVC.
    2. Select **Access Policies** > **Authorized IPs** and verify that the Cloud Service Endpoint source IP addresses of your VPC are displayed.

    You can't read or write to your bucket from the console. You can only access your bucket from within an app pod on your cluster.
    {: note}

11. [Create a deployment YAML that references the PVC you created](/docs/openshift?topic=openshift-storage_cos_apps#create-cos-deployment-steps).

12. Create the app in your cluster.

    ```sh
    oc create -f app.yaml
    ```
    {: pre}

13. Verify that your app pod is `Running`.

    ```sh
    oc get pods | grep <app_name>
    ```
    {: pre}

14. Verify that your volume is mounted and that you can read and write to your COS bucket.

    1. Log in to your app pod.

        ```sh
        oc exec -it <pod_name> bash
        ```
        {: pre}

    2. Verify that your COS bucket is mounted from your app pod and that you can read and write to your COS bucket. Run the disk free `df` command to see available disks in your system. Your COS bucket displays the `s3fs` file system type and the mount path that you specified in your PVC.

        ```sh
        df
        ```
        {: pre}

        In this example, the COS bucket is mounted at `/cos-vpc`.

        ```sh
        Filesystem        1K-blocks    Used    Available Use% Mounted on
        overlay           102048096 9071556     87786140  10% /
        tmpfs                 65536       0        65536   0% /dev
        tmpfs               7565792       0      7565792   0% /sys/fs/cgroup
        shm                   65536       0        65536   0% /dev/shm
        /dev/vda2         102048096 9071556     87786140  10% /etc/hosts
        s3fs           274877906944       0 274877906944   0% /cos-vpc
        tmpfs               7565792      44      7565748   1% /run/secrets/kubernetes.io/serviceaccount
        tmpfs               7565792       0      7565792   0% /proc/acpi
        tmpfs               7565792       0      7565792   0% /proc/scsi
        tmpfs               7565792       0      7565792   0% /sys/firmware
        ```
        {: screen}

    3. Change directories to the directory where your COS bucket is mounted. In this example the bucket is mounted at `/cos-vpc`.

        ```sh
        cd cos-vpc
        ```
        {: pre}

    4. Write a `test.txt` file to your COS bucket and list files to verify that the file was written.

        ```sh
        touch test.txt && ls
        ```
        {: pre}

    5. Remove the file and log out of your app pod.

        ```sh
        rm test.txt && exit
        ```
        {: pre}
        
        
        
