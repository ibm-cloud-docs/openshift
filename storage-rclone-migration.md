---

copyright: 
  years: 2024, 2024
lastupdated: "2024-11-11"


keywords: openshift, rclone, migrate

subcollection: openshift

content-type: tutorial
services: containers, cloud-object-storage 
account-plan: paid
completion-time: 2h

---

{{site.data.keyword.attribute-definition-list}}



# Migrating Cloud Object Storage (COS) apps and data between IBM Cloud accounts
{: #storage-cos-app-migration}
{: toc-content-type="tutorial"}
{: toc-services="containers, cloud-object-storage"}
{: toc-completion-time="2h"}

[Classic infrastructure]{: tag-classic-inf} [Virtual Private Cloud]{: tag-vpc}

In this tutorial, you'll migrate a COS app and data from an {{site.data.keyword.containerlong_notm}} cluster in one account, to a {{site.data.keyword.openshiftlong_notm}} cluster in a separate account.


## Prerequisites
{: #cos-migration-prereqs}

[Account 1]{: tag-purple}

In Account 1, you must have the following.

* An {{site.data.keyword.containerlong_notm}} cluster.

* A COS instance and a set of HMAC credentials. For more information, see [Service credentials](/docs/cloud-object-storage?topic=cloud-object-storage-service-credentials).

* The [COS plug-in installed in your cluster](/docs/containers?topic=containers-storage_cos_install).


[Account 2]{: tag-teal}

In Account 2, the destination account to migrate to, you must have the following.

* A {{site.data.keyword.openshiftlong_notm}} cluster.

* The [COS plug-in installed in your cluster](/docs/openshift?topic=openshift-storage_cos_install).

* A COS instance and a set of HMAC credentials. For more information, see [Service credentials](/docs/cloud-object-storage?topic=cloud-object-storage-service-credentials).

* An empty bucket in your COS instance.

## Optional: Deploy an app in your cluster
{: #cos-mig-app-deploy}
{: step}

[Account 1]{: tag-purple}

If you don't already have an app that you want to migrate, you can deploy the following example app.

1. Create a PVC that references your object storage configuration.

    ```yaml
    kind: PersistentVolumeClaim
    apiVersion: v1
    metadata: 
      name: demo #Enter a name for your PVC.
      namespace: default
      annotations: 
      ibm.io/auto-create-bucket: "true"
      ibm.io/auto-delete-bucket: "false" 
      ibm.io/secret-name: SECRET-NAME #Enter the name of the secret you created earlier.
      ibm.io/secret-namespace: NAMESPACE #Enter the namespace where you want to create the PVC.
    spec: 
        accessModes:
        - ReadWriteOnce
        resources:
            requests:
              storage: 10Gi
        storageClassName: ibmc-s3fs-cos #The storage class that you want to use.
    ```
    {: codeblock}

1. Create the PVC in your cluster.

    ```txt
    oc apply -f pvc-cos.yaml
    ```
    {: pre}

1. Create a YAML configuration file for a pod that mounts the PVC that you create.

    ```yaml
    apiVersion: v1
    kind: Pod
    metadata:
      name: demo-pod
      namespace: default
    spec:
      securityContext:
        runAsUser: 2000
        fsGroup: 2000
      volumes:
      - name: demo-vol
        persistentVolumeClaim:
          claimName: demo
      containers:
      - name: test
        image: nginxinc/nginx-unprivileged
        imagePullPolicy: Always
        volumeMounts:
        - name: demo-vol
          mountPath: /mnt/cosvol
    ```
    {: codeblock}
   

1. Create the pod in your cluster.

    ```txt
    oc apply -f demo-pod.yaml
    ```
    {: pre}

1. Verify that the pod is deployed. Note that it might take a few minutes for your app to get into a `Running` state.

    ```txt
    oc get pods
    ```
    {: pre}

    ```txt
    NAME                                READY   STATUS    RESTARTS   AGE
    demo-pod                            1/1     Running   0          2m58s
    ```
    {: screen}

1. Verify that the app can write to your block storage volume by logging in to your pod.

   ```txt
   oc exec demo-pod -- bash -c "ls /mnt/cosvol"
   ```
   {: pre}

## Get the details of your app
{: #cos-mig-app-details}
{: step}

[Account 1]{: tag-purple}

1. List the pods and PVCs.
    ```txt
    oc get pods
    ```
    {: pre}

1. Describe your PVC and review the details and make a note of the bucket name.
    ```txt
    oc describe PVC -o yaml
    ```
    {: pre}

## Install `rclone`
{: #rclone-install}
{: step}

Follow the `rclone` docs for [installation steps](https://rclone.org/install/).


## Configure `rclone` for your bucket in Account 1
{: #rclone-config-1}
{: step}

[Account 1]{: tag-purple}

After you have `rclone` installed, you must generate a configuration file that defines the COS instance that you want to migrate data from.

1. Run the `rclone config` command.

    ```txt
    rclone config
    ```
    {: pre}

    Example output
    ```txt
    2020/01/16 09:39:33 NOTICE: Config file "/Users/ryan/.config/rclone/rclone.conf" not found - using defaults
    No remotes found - make a new one
    n) New remote
    s) Set configuration password
    q) Quit config
    ```
    {: screen}

1. Enter `n` to set up a new remote, then provide a name for your remote.
    ```txt
    n/s/q> n
    ```
    {: pre}

    Example remote name
    ```txt
    name> cos-instance-1
    ```
    {: codeblock}

1. From the list of providers, select `Amazon S3 Compliant Storage Provider` which includes `IBM COS`.
    ```txt
    Enter a string value. Press Enter for the default ("").
    Choose a number from below, or type in your own value
    1 / 1Fichier
      \ "fichier"
    2 / Alias for an existing remote
      \ "alias"
    3 / Amazon Drive
      \ "amazon cloud drive"
    4 / Amazon S3 Compliant Storage Provider (AWS, Alibaba, Ceph, Digital Ocean, Dreamhost, IBM COS, Minio, etc)
      \ "s3"
    5 / Backblaze B2
      \ "b2"
    ...
    provider> 4
    ```
    {: screen}

1. Select `IBM COS` as your s3 provider. 

    ```txt
    Choose your S3 provider.
    Enter a string value. Press Enter for the default ("").
    Choose a number from below, or type in your own value
    1 / Amazon Web Services (AWS) S3
      \ "AWS"
    2 / Alibaba Cloud Object Storage System (OSS) formerly Aliyun
      \ "Alibaba"
    3 / Ceph Object Storage
      \ "Ceph"
    4 / Digital Ocean Spaces
      \ "DigitalOcean"
    5 / Dreamhost DreamObjects
      \ "Dreamhost"
    6 / IBM COS S3
      \ "IBMCOS"
    7 / Minio Object Storage
      \ "Minio"
    8 / Netease Object Storage (NOS)
      \ "Netease"
    9 / Wasabi Object Storage
      \ "Wasabi"
    10 / Any other S3 compatible provider
      \ "Other"
    ```
    {: screen}


1. Add your COS credentials by select option `1`.
    ```txt
    Option env_auth.
    Get AWS credentials from runtime (environment variables or EC2/ECS meta data if no env vars).
    Only applies if access_key_id and secret_access_key is blank.
    Choose a number from below, or type in your own boolean value (true or false).
    Press Enter for the default (false).
    1 / Enter AWS credentials in the next step.
      \ (false)
    2 / Get AWS credentials from the environment (env vars or IAM).
      \ (true)
    env_auth> 1
    ```
    {: screen}

1. When prompted, provide the `access_key_id` and `secret_access_key` of your COS instance. For more information, see [Service credentials](/docs/cloud-object-storage?topic=cloud-object-storage-service-credentials).
    ```txt
    AWS Access Key ID.
    Leave blank for anonymous access or runtime credentials.
    Enter a string value. Press Enter for the default ("").
    access_key_id> xxxxxxxxxxxxxxxxxxxxx
    AWS Secret Access Key (password)
    Leave blank for anonymous access or runtime credentials.
    Enter a string value. Press Enter for the default ("").
    secret_access_key> xxxxxxxxxxxxxxxxxxxxxxxxxxxxx
    ```
    {: screen}

1. In the `Region to connect to` prompt, select option `1`.

    ```txt
    Region to connect to.
    Leave blank if you are using an S3 clone and you don't have a region.
    Enter a string value. Press Enter for the default ("").
    Choose a number from below, or type in your own value
    1 / Use this if unsure. Will use v4 signatures and an empty region.
      \ ""
    2 / Use this only if v4 signatures don't work, eg pre Jewel/v10 CEPH.
      \ "other-v2-signature"
    region> 1
    ```
    {: screen}


1. In the `Endpoint for IBM COS S3 API` prompt, select option `1`.

    ```txt
    Endpoint for IBM COS S3 API.
    Specify if using an IBM COS On Premise.
    Enter a string value. Press Enter for the default ("").
    Choose a number from below, or type in your own value
    1 / US Cross Region Endpoint
      \ "s3-api.us-geo.objectstorage.softlayer.net"
    2 / US Cross Region Dallas Endpoint
      \ "s3-api.dal.us-geo.objectstorage.softlayer.net"
    3 / US Cross Region Washington DC Endpoint
      \ "s3-api.wdc-us-geo.objectstorage.softlayer.net"
    ...
    endpoint> 1
    ```
    {: screen}

1. In the `Location constraint` prompt, press **Return** to use the default.
    ```txt
    Location constraint - must match endpoint when using IBM Cloud Public.
    For on-prem COS, do not make a selection from this list, hit enter
    Enter a string value. Press Enter for the default ("").
    Choose a number from below, or type in your own value
    1 / US Cross Region Standard
      \ "us-standard"
    2 / US Cross Region Vault
      \ "us-vault"
    3 / US Cross Region Cold
      \ "us-cold"
    4 / US Cross Region Flex
      \ "us-flex"
    ...
    ```
    {: screen}

1. In the ACL policy prompt, select `private`.
    ```txt
    Note that this ACL is applied when server side copying objects as S3
    doesn't copy the ACL from the source but rather writes a fresh one.
    Enter a string value. Press Enter for the default ("").
    Choose a number from below, or type in your own value
    1 / Owner gets FULL_CONTROL. No one else has access rights (default). This acl is available on IBM Cloud (Infra), IBM Cloud (Storage), On-Premise COS
      \ "private"
    2 / Owner gets FULL_CONTROL. The AllUsers group gets READ access. This acl is available on IBM Cloud (Infra), IBM Cloud (Storage), On-Premise IBM COS
      \ "public-read"
    3 / Owner gets FULL_CONTROL. The AllUsers group gets READ and WRITE access. This acl is available on IBM Cloud (Infra), On-Premise IBM COS
      \ "public-read-write"
    4 / Owner gets FULL_CONTROL. The AuthenticatedUsers group gets READ access. Not supported on Buckets. This acl is available on IBM Cloud (Infra) and On-Premise IBM COS
      \ "authenticated-read"
    acl> 1
    ```
    {: screen}

1. Skip the advanced config option and confirm your setup.
    ```txt
    Edit advanced config? (y/n)
    y) Yes
    n) No
    y/n> n
    Remote config
    --------------------
    [cos-instance-1]
    type = s3
    provider = IBMCOS
    env_auth = false
    access_key_id = xxxxxx
    secret_access_key = xxxxxxxxx
    endpoint = s3-api.us-geo.objectstorage.softlayer.net
    location_constraint = us-standard
    acl = private
    --------------------
    y) Yes this is OK
    e) Edit this remote
    d) Delete this remote
    y/e/d> y
    Current remotes:

    Name                 Type
    ====                 ====
    cos-instance-1      s3
    ```
    {: screen}

1. Repeat the previous steps to add the COS instance in your second account. When you've verified the information, press `q` to quit the configuration process.

## Configure `rclone` for your bucket in Account 2
{: #rclone-config-2}
{: step}

[Account 2]{: tag-teal}

Repeat the steps to configure `rclone` for Account 2.

1. Run the `rclone config` command.

    ```txt
    rclone config
    ```
    {: pre}

    Example output
    ```txt
    2020/01/16 09:39:33 NOTICE: Config file "/Users/ryan/.config/rclone/rclone.conf" not found - using defaults
    No remotes found - make a new one
    n) New remote
    s) Set configuration password
    q) Quit config
    ```
    {: screen}

1. Enter `n` to set up a new remote, then provide a name for your remote.
    ```txt
    n/s/q> n
    ```
    {: pre}

    Example remote name
    ```txt
    name> cos-instance-2
    ```
    {: codeblock}

1. From the list of providers, select `Amazon S3 Compliant Storage Provider` which includes `IBM COS`.
    ```txt
    Enter a string value. Press Enter for the default ("").
    Choose a number from below, or type in your own value
    1 / 1Fichier
      \ "fichier"
    2 / Alias for an existing remote
      \ "alias"
    3 / Amazon Drive
      \ "amazon cloud drive"
    4 / Amazon S3 Compliant Storage Provider (AWS, Alibaba, Ceph, Digital Ocean, Dreamhost, IBM COS, Minio, etc)
      \ "s3"
    5 / Backblaze B2
      \ "b2"
    ...
    provider> 4
    ```
    {: screen}

1. Select `IBM COS` as your s3 provider. 

    ```txt
    Choose your S3 provider.
    Enter a string value. Press Enter for the default ("").
    Choose a number from below, or type in your own value
    1 / Amazon Web Services (AWS) S3
      \ "AWS"
    2 / Alibaba Cloud Object Storage System (OSS) formerly Aliyun
      \ "Alibaba"
    3 / Ceph Object Storage
      \ "Ceph"
    4 / Digital Ocean Spaces
      \ "DigitalOcean"
    5 / Dreamhost DreamObjects
      \ "Dreamhost"
    6 / IBM COS S3
      \ "IBMCOS"
    7 / Minio Object Storage
      \ "Minio"
    8 / Netease Object Storage (NOS)
      \ "Netease"
    9 / Wasabi Object Storage
      \ "Wasabi"
    10 / Any other S3 compatible provider
      \ "Other"
    ```
    {: screen}


1. Add your COS credentials by select option `1`.
    ```txt
    Option env_auth.
    Get AWS credentials from runtime (environment variables or EC2/ECS meta data if no env vars).
    Only applies if access_key_id and secret_access_key is blank.
    Choose a number from below, or type in your own boolean value (true or false).
    Press Enter for the default (false).
    1 / Enter AWS credentials in the next step.
      \ (false)
    2 / Get AWS credentials from the environment (env vars or IAM).
      \ (true)
    env_auth> 1
    ```
    {: screen}

1. When prompted, provide the `access_key_id` and `secret_access_key` of your COS instance. For more information, see [Service credentials](/docs/cloud-object-storage?topic=cloud-object-storage-service-credentials).
    ```txt
    AWS Access Key ID.
    Leave blank for anonymous access or runtime credentials.
    Enter a string value. Press Enter for the default ("").
    access_key_id> xxxxxxxxxxxxxxxxxxxxx
    AWS Secret Access Key (password)
    Leave blank for anonymous access or runtime credentials.
    Enter a string value. Press Enter for the default ("").
    secret_access_key> xxxxxxxxxxxxxxxxxxxxxxxxxxxxx
    ```
    {: screen}

1. In the `Region to connect to` prompt, select option `1`.

    ```txt
    Region to connect to.
    Leave blank if you are using an S3 clone and you don't have a region.
    Enter a string value. Press Enter for the default ("").
    Choose a number from below, or type in your own value
    1 / Use this if unsure. Will use v4 signatures and an empty region.
      \ ""
    2 / Use this only if v4 signatures don't work, eg pre Jewel/v10 CEPH.
      \ "other-v2-signature"
    region> 1
    ```
    {: screen}


1. In the `Endpoint for IBM COS S3 API` prompt, select option `1`.

    ```txt
    Endpoint for IBM COS S3 API.
    Specify if using an IBM COS On Premise.
    Enter a string value. Press Enter for the default ("").
    Choose a number from below, or type in your own value
    1 / US Cross Region Endpoint
      \ "s3-api.us-geo.objectstorage.softlayer.net"
    2 / US Cross Region Dallas Endpoint
      \ "s3-api.dal.us-geo.objectstorage.softlayer.net"
    3 / US Cross Region Washington DC Endpoint
      \ "s3-api.wdc-us-geo.objectstorage.softlayer.net"
    ...
    endpoint> 1
    ```
    {: screen}

1. In the `Location constraint` prompt, press **Return** to use the default.
    ```txt
    Location constraint - must match endpoint when using IBM Cloud Public.
    For on-prem COS, do not make a selection from this list, hit enter
    Enter a string value. Press Enter for the default ("").
    Choose a number from below, or type in your own value
    1 / US Cross Region Standard
      \ "us-standard"
    2 / US Cross Region Vault
      \ "us-vault"
    3 / US Cross Region Cold
      \ "us-cold"
    4 / US Cross Region Flex
      \ "us-flex"
    ...
    ```
    {: screen}

1. In the ACL policy prompt, select `private`.
    ```txt
    Note that this ACL is applied when server side copying objects as S3
    doesn't copy the ACL from the source but rather writes a fresh one.
    Enter a string value. Press Enter for the default ("").
    Choose a number from below, or type in your own value
    1 / Owner gets FULL_CONTROL. No one else has access rights (default). This acl is available on IBM Cloud (Infra), IBM Cloud (Storage), On-Premise COS
      \ "private"
    2 / Owner gets FULL_CONTROL. The AllUsers group gets READ access. This acl is available on IBM Cloud (Infra), IBM Cloud (Storage), On-Premise IBM COS
      \ "public-read"
    3 / Owner gets FULL_CONTROL. The AllUsers group gets READ and WRITE access. This acl is available on IBM Cloud (Infra), On-Premise IBM COS
      \ "public-read-write"
    4 / Owner gets FULL_CONTROL. The AuthenticatedUsers group gets READ access. Not supported on Buckets. This acl is available on IBM Cloud (Infra) and On-Premise IBM COS
      \ "authenticated-read"
    acl> 1
    ```
    {: screen}

1. Skip the advanced config option and confirm your setup.
    ```txt
    Edit advanced config? (y/n)
    y) Yes
    n) No
    y/n> n
    Remote config
    --------------------
    [cos-instance-2]
    type = s3
    provider = IBMCOS
    env_auth = false
    access_key_id = xxxxxx
    secret_access_key = xxxxxxxxx
    endpoint = s3-api.us-geo.objectstorage.softlayer.net
    location_constraint = us-standard
    acl = private
    --------------------
    y) Yes this is OK
    e) Edit this remote
    d) Delete this remote
    y/e/d> y
    Current remotes:

    Name                 Type
    ====                 ====
    cos-instance-1      s3
    cos-instance-2      s3
    ```
    {: screen}

1. Repeat the previous steps to add the COS instance in your second account. When you've verified the information, press `q` to quit the configuration process.

## View the contents of your COS buckets
{: #rclone-inspect}
{: step}

[Account 1]{: tag-purple} [Account 2]{: tag-teal}


After configuring `rclone`, review the contents of each bucket and then sync the data between buckets in each account.

1. View the contents of the bucket in the first instance.

    ```txt
    rclone ls cos-instance-1:bucket-1
        45338 test.txt
    ```
    {: screen}

1. View the contents of the bucket in instance 2. In this example the bucket name is `bucket-2`.

    ```txt
    rclone ls cos-instance-2:bucket-2
    ```
    {: pre}


## Syncing contents between buckets
{: #rclone-sync}
{: step}

[Account 1]{: tag-purple} [Account 2]{: tag-teal}


1. To move the data from one bucket to another, you can use the `rclone sync` command. In this example `cos-instance-1:bucket-1` is in one account while `cos-instance-2:bucket-2` is a second instance of COS in a separate account.

    Example

    ```txt
    rclone sync -P cos-instance-1:bucket-1 cos-instance-2:bucket-2
    ```
    {: pre}

    Example output

    ```txt
    Transferred:      754.933k / 754.933 kBytes, 100%, 151.979 kBytes/s, ETA 0s
    Errors:                 0
    Checks:                 0 / 0, -
    Transferred:           18 / 18, 100%
    Elapsed time:        4.9
    ```
    {: screen}

1. Verify the contents of the bucket in `cos-instance-1` have been synced to the bucket in `cos-instance-2`.

    ```txt
    rclone ls cos-instance-2:bucket-2
    ```
    {: pre}

    Example output

    ```txt
    45338 test.txt
    ```
    {: screen}


## Redeploy your app in Account 2
{: #cos-app-redploy}
{: step}

[Account 2]{: tag-teal}

1. [Access your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-access_cluster).

1. Copy the following PVC and save it to a file called `pvc.yaml`

    ```yaml
    kind: PersistentVolumeClaim
    apiVersion: v1
    metadata: 
      name: demo # Enter a name for your PVC.
      namespace: default
      annotations:
      ibm.io/bucket-name: "bucket-2" # Enter the name of the bucket in Account 2
      ibm.io/auto-create-bucket: "false"
      ibm.io/auto-delete-bucket: "false"
      ibm.io/secret-name: SECRET-NAME #Enter the name of the secret you created earlier.
      ibm.io/secret-namespace: NAMESPACE #Enter the namespace where you want to create the PVC.
    spec: 
        accessModes:
        - ReadWriteOnce
        resources:
            requests:
              storage: 10Gi
        storageClassName: ibmc-s3fs-cos #The storage class that you want to use.
    ```
    {: codeblock}

1. Create the PVC in your cluster.
    ```txt
    oc apply -f pvc.yaml
    ```
    {: pre}


1. Create a YAML configuration file for a pod that mounts the PVC that you create.

    ```yaml
    apiVersion: v1
    kind: Pod
    metadata:
      name: demo-pod
      namespace: default
    spec:
      securityContext:
        runAsUser: 2000
        fsGroup: 2000
      volumes:
      - name: demo-vol
        persistentVolumeClaim:
          claimName: demo
      containers:
      - name: test
        image: nginxinc/nginx-unprivileged
        imagePullPolicy: Always
        volumeMounts:
        - name: demo-vol
          mountPath: /mnt/cosvol
    ```
    {: codeblock}


1. Create the pod in your cluster.

    ```txt
    oc apply -f demo-pod.yaml
    ```
    {: pre}

1. Verify that the pod is deployed. Note that it might take a few minutes for your app to get into a `Running` state.

    ```txt
    oc get pods
    ```
    {: pre}

    ```txt
    NAME                                READY   STATUS    RESTARTS   AGE
    demo-pod                            1/1     Running   0          2m58s
    ```
    {: screen}

1. Verify that the app can write to your block storage volume by logging in to your pod.

   ```txt
   oc exec demo-pod -- bash -c "ls /mnt/cosvol"
   ```
   {: pre}

   ```txt
   test.txt
   ```
   {: pre}
