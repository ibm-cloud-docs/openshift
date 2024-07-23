---

copyright: 
  years: 2024, 2024
lastupdated: "2024-07-23"


keywords: openshift, rclone, migrate

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}



# Migrating Cloud Object Storage (COS) resources between IBM Cloud accounts
{: #storage-rclone-migration}

Complete the following steps to move the contents of a COS bucket in one account to a COS bucket in a separate account.

## Prerequisites
{: #rclone-migration-prereqs}


* A COS bucket with HMAC credentials for each instance of Cloud Object Storage that you are migrating between. For more information, see [Service credentials](/docs/cloud-object-storage?topic=cloud-object-storage-service-credentials).

* Install `rclone`. For more information, see the [docs](https://rclone.org/install/).


## Configuring `rclone`
{: #rclone-config}
{: step}


1. After you have `rclone` installed, you must generate a configuration file that defines the 2 COS instances. You can do this by running the command `rclone config` command.

    ```sh
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
    ```sh
    n/s/q> n
    ```
    {: pre}

    Example remote name
    ```sh
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
    ```sh
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

1. Complete the previous steps again to add your second COS instance and when you've verified that everything looks correct choose q to quit the configuration process.


## Syncing between COS buckets
{: #rclone-inspect}


After configuring rclone, you can now sync between buckets. But first, review the contents of each bucket.

1. View the contents of the bucket in the first instance.

    ```sh
    rclone ls cos-instance-1:BUCKET-NAME
        45338 AddNFSAccess.png
        48559 AddingNFSAccess.png
        66750 ChooseGroup.png
        2550 CloudPakApplications.png
        4643 CloudPakAutomation.png
        4553 CloudPakData.png
        5123 CloudPakIntegration.png
        4612 CloudPakMultiCloud.png
        23755 CompletedAddingNFSAccess.png
      174525 CreateNetworkShare1.png
        69836 CreateNetworkShare2.png
        76863 CreateStoragePool.png
        50489 CreateStoragePool1.png
        56297 CreateStoragePool2.png
        2340 applications-icon.svg
        6979 automation-icon.svg
      120584 cloud-paks-leadspace.png
        9255 data-icon.svg
    ```
    {: screen}

1. View the contents of the bucket in instance 2.

    ```sh
    rclone ls cos-instance-2:BUCKET-NAME
    ```
    {: pre}


## Syncing contents between buckets
{: #rclone-sync}


1. To move the data from one bucket to another, you can use the `rclone sync` command. In this example `cos-instance-1:BUCKET` is in one account while `cos-instance-2:BUCKET` is a second instance of COS in a separate account.

    Example

    ```sh
    rclone sync -P cos-instance-1:BUCKET cos-instance-2:BUCKET
    ```
    {: pre}

    Example output

    ```sh
    Transferred:      754.933k / 754.933 kBytes, 100%, 151.979 kBytes/s, ETA 0s
    Errors:                 0
    Checks:                 0 / 0, -
    Transferred:           18 / 18, 100%
    Elapsed time:        4.9
    ```
    {: screen}

1. Verify the contents of the bucket in `cos-instance-1` have been synced to the bucket in `cos-instance-2`.

    ```sh
    rclone ls cos-instance-2:BUCKET
    ```
    {: pre}

    Example output

    ```sh
    45338 AddNFSAccess.png
    48559 AddingNFSAccess.png
    66750 ChooseGroup.png
    2550 CloudPakApplications.png
    4643 CloudPakAutomation.png
    4553 CloudPakData.png
    5123 CloudPakIntegration.png
    4612 CloudPakMultiCloud.png
    23755 CompletedAddingNFSAccess.png
    174525 CreateNetworkShare1.png
    69836 CreateNetworkShare2.png
    76863 CreateStoragePool.png
    50489 CreateStoragePool1.png
    56297 CreateStoragePool2.png
    2340 applications-icon.svg
    6979 automation-icon.svg
    120584 cloud-paks-leadspace.png
    9255 data-icon.svg
    ```
    {: screen}

## Next steps
{: #rclone-next-steps}

Redeploy your apps that use COS. For more information, see [Adding Object Storage to apps](/docs/openshift?topic=openshift-storage_cos_apps).

