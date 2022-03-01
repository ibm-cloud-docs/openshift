---

copyright:
  years: 2014, 2022
lastupdated: "2022-03-01"

keywords: openshift, noobaa, openshift container storage, openshift data foundation, storage classes

subcollection: openshift

---


{{site.data.keyword.attribute-definition-list}}

# Managing the Multi-Cloud Object Gateway
{: #odf-manage-noobaa}

You can use NooBaa to manage your s3 compatible object storage resources, like IBM {{site.data.keyword.cos_short}}, AWS s3, or Azure Blob storage. With NooBaa, you can also create and manage your object storage consistently across clusters and zones.
{: shortdesc}


## Setting up backing stores by using the NooBaa CLI
{: #odf-backingstore}

Backing stores are NooBaa resources for managing your s3 compatible services and buckets. When you create a backing store, you provide your s3 service credentials like your access key ID, secret access key, and endpoint for your object storage service. After you add backing stores to your cluster, you can [create bucket classes](#odf-bucketclass) which allow you to configure data federation policies for your s3 compatible storage services.
{: shortdesc}

After you deploy ODF, you can configure more backing stores in your storage cluster. You can create a backing store by using any s3 compatible object store such as AWS or {{site.data.keyword.cos_full_notm}}.

You can also create and manage your backing stores in the {{site.data.keyword.redhat_openshift_notm}} web console.
{: tip}

To add a backing store to your storage cluster by using the NooBaa CLI:

[Access your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-access_cluster).

1. Install the [NooBaa Operator CLI](https://github.com/noobaa/noobaa-operator){: external}.
1. Run the `noobaa backingstore create` command to see a list of supported backing store types.
    ```sh
    noobaa backingstore create
    ```
    {: pre}

    Example output
    ```sh
    Create backing store

    Available Commands:
    aws-s3               Create aws-s3 backing store
    azure-blob           Create azure-blob backing store
    google-cloud-storage Create google-cloud-storage backing store
    ibm-cos              Create ibm-cos backing store
    pv-pool              Create pv-pool backing store
    s3-compatible        Create s3-compatible backing store
    ```
    {: screen}

1. Get the details of the service that you want to use. If you want to set up an {{site.data.keyword.cos_full_notm}}, get your HMAC credentials. For more information, see [Using HMAC credentials](/docs/cloud-object-storage?topic=cloud-object-storage-uhc-hmac-credentials-main). The following example command shows the configuration parameters that are required to create a backing store by using an {{site.data.keyword.cos_full_notm}} service instance.
    ```sh
    noobaa backingstore create ibm-cos <backing-store-name> -n openshift-storage --access-key=<access-key> --endpoint=<endpoint> --secret-key=<secret-key> --target-bucket<target-bucket>
    ```
    {: pre}

1. Get the details of your backing store.
    ```sh
    noobaa backingstore status <backing-store-name> -n openshift-storage
    ```
    {: pre}
    

## Creating a bucket class that uses two backing stores with a mirror placement policy
{: #odf-bucketclass}

After you have [installed ODF](/docs/openshift?topic=openshift-deploy-odf-vpc) and configured at least two [backing stores](#odf-backingstore), you can create a bucket class that uses multiple backing stores. Bucket classes allow you to configure data federation policies across your backing stores. Then, when your apps write objects to your bucket, you can mirror or spread the objects across two or more backing stores.

**Before you begin** [Install the NooBaa CLI](https://github.com/NooBaa/NooBaa-operator){: external})

1. Get the status of your NooBaa instance. For clusters in {{site.data.keyword.cloud_notm}}, target the `openshift-storage` namespace.
    ```sh
    noobaa status -n openshift-storage
    ```
    {: pre}

2. Verify you have at least two backing stores.
    ```sh
    noobaa backingstore list -n openshift-storage
    ```
    {: pre}

3. Create a bucket class that uses two of your backing stores and has a `Mirror` policy to mirror objects across two or more backing stores.
    ```sh
    noobaa bucketclass create <bucketclass-name> --backingstores=[<backingstore_one>,<backingstore_two>] --placement='<placement>' -n <namespace>
    ```
    {: pre}

4. **Optional** You can also create a bucket class by using a YAML configuration file.
    ```yaml
    apiVersion: noobaa.io/v1alpha1
    kind: BucketClass
    metadata:
    labels:
        app: noobaa
    name: mirror-bucket-class
    namespace: openshift-storage
    spec:
    placementPolicy:
        tiers:
        - backingStores:
        - backing-store-one
        - backing-store-two
        placement: Mirror
    ```
    {: codeblock}

## Creating a storage class
{: #odf-sc}

After you create backing stores and a bucket class, create a storage class to make your bucket class resources available across the namespaces in your cluster.

1. Create a storage class YAML file that contains a name for your storage class in the format `<name>-noobaa.noobaa.io`, the name of the bucket class that you want to use, and the provisioner set to `openshift-storage.noobaa.io/obc`.
    ```yaml
    metadata:
        name: <name>-noobaa.noobaa.io
      parameters:
    bucketclass: <bucket-class-name>
    provisioner: openshift-storage.noobaa.io/obc
    reclaimPolicy: Delete
    volumeBindingMode: Immediate
    ```
    {: codeblock}

1. Create the storage class in your cluster.
    ```sh
    oc create -f sc.yaml
    ```
    {: pre}

1. Verify the storage class is created.
    ```sh
    oc get sc
    ```
    {: pre}

## Creating an Object Bucket Claim
{: odf-obc}

After you create backing stores and a bucket class, you can create an object bucket claim that you can use to claim storage resources for your s3 apps.
{: shortdesc}

1. Create an object bucket claim YAML file that references the bucket class that you created earlier.
    ```yaml
    apiVersion: objectbucket.io/v1alpha1
    kind: ObjectBucketClaim
    metadata:
        name: cos-obc
      spec:
    storageClassName: cos-noobaa.noobaa.io
    bucketName: cos-bucket
    ```
    {: codeblock}

1. Create the object bucket claim in your cluster.
    ```sh
    oc apply -f obc.yaml
    ```
    {: pre}

1. Verify the OBC is created.
    ```sh
    noobaa obc list
    ```
    {: pre}

1. List the secrets and config maps in your cluster and verify that the corresponding secret and config map for your OBC are created.
    ```sh
    oc get secrets | grep <obc-name> && oc get cm | grep <obc-name>
    ```
    {: pre}

## Deploying an s3 app in the Multicloud Object Gateway
{: #mcg-deploy-app}

1. Create an app YAML file that references the secret and config map from your OBC. The following example app uses the `banst/awscli` image and configures the AWS CLI.
    ```yaml
    apiVersion: v1
    kind: Pod
    metadata:
        name: app
    labels:
      app: app
    spec:
        containers:
        - name: app
        envFrom:
        - secretRef:
            name: <secret-name>
        - configMapRef:
            name: <config-map-name>
        image: banst/awscli
        command:
            - sh
            - "-c"
            - |
                echo "----> Configuring S3 endpoint ...";
                pip install awscli-plugin-endpoint;
                aws configure set plugins.endpoint awscli_plugin_endpoint;
                aws configure set s3.endpoint_url https://s3.openshift-storage.svc;
                echo "----> Configuring certificates ...";
                aws configure set ca_bundle /var/run/secrets/kubernetes.io/serviceaccount/service-ca.crt;
                echo "----> Copying files ...";
                aws s3 cp --recursive /etc s3://$BUCKET_NAME;
                echo "----> List files ...";
                aws s3 ls $BUCKET_NAME;
                echo "----> Done.";
    ```
    {: codeblock}

1. Create the app in your cluster.
    ```sh
    oc create -f app.yaml
    ```
    {: pre}

1. Verify your app is running.
    ```sh
    oc get pods
    ```
    {: pre}








