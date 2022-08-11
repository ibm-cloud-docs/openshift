---

copyright:
  years: 2022, 2022
lastupdated: "2022-08-11"

keywords: openshift

subcollection: openshift

content-type: tutorial
services: openshift,cloud-object-storage
account-plan: paid
completion-time: 45m

---

{{site.data.keyword.attribute-definition-list}}

# Setting capacity quotas for apps that use {{site.data.keyword.cos_full_notm}}
{: #storage-cos-tutorial-quota}
{: toc-content-type="tutorial"}
{: toc-services="openshift, cloud-object-storage"}
{: toc-completion-time="45m"}

With {{site.data.keyword.cos_full_notm}}, you can dynamically provision buckets for apps running in your {{site.data.keyword.openshiftlong_notm}} clusters. You can also dynamically set capacity quotas on those buckets during provisioning. Quotas can help you manage the resources your workloads use while also avoiding unnecessary charges.
{: shortdesc}

Supported infrastructure providers
:   Classic
:   VPC

## Objectives
{: #storage-cos-quota-objectives}

In this tutorial, you install the {{site.data.keyword.cos_short}} plug-in in your cluster and enable quotas for any persistent volume claims (PVC) created with the plug-in. 

Then, you create a PVC which dynamically creates a bucket with a quota limit in your {{site.data.keyword.cos_short}} instace. 

After that, you upload a file to your bucket and deploy a simple app to your cluster that mounts the bucket and prints the contents of that file.

## Prerequisites
{: #storage-cos-quota-prereqs}

Before beginning this tutorial make sure you have created or installed the following resources and tools.

- An {{site.data.keyword.cloud_notm}} account. For more information, see [Creating an account](/docs/account?topic=account-account-getting-started).
- The CLI tools including the {{site.data.keyword.cloud_notm}} CLI, the Containers service CLI plug-in, and the Helm CLI. For more information, see [Getting started with the {{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-getting-started).
- A {{site.data.keyword.openshiftlong_notm}} cluster. If you have a VPC cluster, make sure your VPC has a public gateway attached. For more information, see [Creating clusters](/docs/containers?topic=containers-clusters)
- An {{site.data.keyword.cos_short}} instance in the same region as your cluster. For more information, see [Provision an instance of {{site.data.keyword.cos_short}}](/docs/cloud-object-storage?topic=cloud-object-storage-provision).


## Creating a set of service credentials
{: #storage-cos-quota-credentials}
{: step}

1. Follow the steps to create a set of HMAC [service credentials for your {{site.data.keyword.cos_short}} instance](/docs/cloud-object-storage?topic=cloud-object-storage-service-credentials). Note that the credentials you create must have the **Manager** role to create buckets. 

1. After you create a set of HMAC service credentials, review the details of your credentials and make a note of the `apikey`, `access_key_id`, and `secret_access_key`. Save these values for the next step.


## Creating a secret to store your credentials
{: #storage-cos-quota-secret}
{: step}

1. Create a secret by using the `apikey`, `access_key_id`, and `secret_access_key` from your service credentials.
    ```sh
    oc create secret generic my-cos-secret --type=ibm/ibmc-s3fs --from-literal=access-key=ACCESS-KEY --from-literal=secret-key=SECRET-KEY --from-literal=res-conf-apikey=API-KEY
    ```
    {: pre}
    
    Example output.
    ```sh
    secret/my-cos-secret created
    ```
    {: screen}

1. Verify the secret was created.
    ```sh
    oc get secrets | grep my-cos
    ```
    {: pre}
    
    Example output.
    ```sh   
    my-cos-secret              ibm/ibmc-s3fs                         3      11m
    ```
    {: screen}


## Installing the plug-in
{: #storage-cos-quota-install}
{: step}

When you install the plug-in in your cluster, make sure to specify the `--set quotaLimit=true` option. Specifying this option means any buckets you create with PVCs have a quota limit equal to the storage size in the PVC.
{: important}

1. Follow the steps to [install the plug-in and enable quota limits](/docs/openshift?topic=openshift-storage_cos_install). If you've already installed the plug-in in your cluster, you can skip this step. To see if the plug-in is already installed, follow the next step.

1. Verify the plug-in is installed by listing the driver pods.

    ```sh
    oc get pods -n ibm-object-s3fs | grep object
    ```
    {: pre}
    
    Example output.
    ```sh
    ibmcloud-object-storage-driver-k9x4l             1/1     Running   0          6m52s
    ibmcloud-object-storage-driver-kj9m6             1/1     Running   0          6m52s
    ibmcloud-object-storage-driver-l8gqk             1/1     Running   0          6m52s
    ibmcloud-object-storage-plugin-576fb8bd7-sxlkb   1/1     Running   0          6m52s
    ```
    {: screen}

## Dynamically provisioning a bucket with a quota
{: #storage-cos-quota-create-bucket}
{: step}

You can use dynamic provisioning to automatically create a {{site.data.keyword.cos_short}} bucket when you a create a PVC.

1. Copy the following PVC configuration and save it to a file called `pvc.yaml`. This example PVC automatically creates a bucket with a quota equal to `20Gi`.

    ```yaml
    kind: PersistentVolumeClaim
    apiVersion: v1
    metadata:
      name: my-cos-pvc
      namespace: default
      annotations:
        ibm.io/auto-create-bucket: "true"
        ibm.io/auto-delete-bucket: "true"
        ibm.io/secret-name: "my-cos-secret" 
        ibm.io/quota-limit: "true"
    spec:
      accessModes:
        - ReadWriteOnce
      resources:
        requests:
          storage: 20Gi
      storageClassName: ibmc-s3fs-standard-cross-region
    ```
    {: codeblock}

1. Create the PVC in your cluster.
    ```sh
    oc apply -f pvc.yaml
    ```
    
    Example output.
    ```sh
    persistentvolumeclaim/my-cos-pvc created
    ```
    {: screen}


1. List your PVCs and verify the `my-cos-pvc` is in the `Bound` state.
    ```sh
    NAME         STATUS   VOLUME                                     CAPACITY   ACCESS MODES   STORAGECLASS                      AGE
    my-cos-pvc   Bound    pvc-64a4e0c9-b5ec-40e3-8b7e-77ff47ae6c5e   20Gi       RWO            ibmc-s3fs-standard-cross-region   6s
    ```
    {: screen}

1. [Navigate to your {{site.data.keyword.cos_short}} instance in the console](https://cloud.ibm.com/objectstorage) and click the **Buckets** tab.

1. Review the details of the automatically created bucket. The bucket name is in the format `tmp-s3fs-XXXX`. 

1. Click the `tmp-s3fs-XXXX` bucket, then click the **Configuration** tab.

1. On the **Configuration** page, look for the **Quota enforcement** section. Note that the bucket was automatically created with a quota equal to the size you specified in the PVC. In this example, the value was `20Gi`.

## Uploading a file to your bucket
{: #storage-cos-quota-create-file}
{: step}

1. Save the following Pod configuration to a file called `pod.yaml`.

    ```yaml
    apiVersion: v1
    kind: Pod
    metadata:
      name: cat-test-file
    spec: 
      containers:
        - name: app
          image: nginx
          volumeMounts:
          - name: my-vol
            mountPath: "/mnt"
          command: ["/bin/sh"]
          args: ["-c", "cat mnt/pod.yaml && sleep 5 && exit"]
      volumes:
        - name: my-vol
          persistentVolumeClaim:
            claimName: my-cos-pvc
    ```
    {: codeblock}
    
1. [Navigate to your {{site.data.keyword.cos_short}} instance in the console](https://cloud.ibm.com/objectstorage) and click the **Buckets** tab.

1. Click the `tmp-s3fs-XXXX` bucket, then click **Upload**.

1. Upload the `pod.yaml` file that you saved earlier.


## Creating an app that mounts the bucket
{: #storage-cos-quota-create-app}
{: step}

1. Copy the following Pod configuration and save it to a file called `pod.yaml`. This example pod mounts the bucket that was created by the `my-cos-pvc` PVC and prints the contents of the `pod.yaml` file you uploaded earlier.
    ```yaml
    apiVersion: v1
    kind: Pod
    metadata:
      name: cat-test-file
    spec: 
      containers:
        - name: app
          image: nginx
          volumeMounts:
          - name: my-vol
            mountPath: "/mnt"
          command: ["/bin/sh"]
          args: ["-c", "cat mnt/pod.yaml && sleep 5 && exit"]
      volumes:
        - name: my-vol
          persistentVolumeClaim:
            claimName: my-cos-pvc
    ```
    {: codeblock}
    
1. Create the pod in your cluster.
    ```sh
    oc apply -f pod.yaml
    ```
    {: pre}
    
    Example output.
    ```sh
    pod/cat-test-file created
    ```
    {: screen}
    
1. Get the logs of the `cat-test-file` pod. In this example, the logs contain the printed contents of the `pod.yaml` file you uploaded earlier.
    ```yaml
    apiVersion: v1
    kind: Pod
    metadata:
      name: cat-test-file
    spec: 
      containers:
        - name: app
          image: nginx
          volumeMounts:
          - name: my-vol
            mountPath: "/mnt"
          command: ["/bin/sh"]
          args: ["-c", "cat mnt/pod.yaml && sleep 5 && exit"]
      volumes:
        - name: my-vol
          persistentVolumeClaim:
            claimName: my-cos-pvc
    ```
    {: screen}


## Review
{: #storage-cos-quota-review}

In this tutorial, you installed the {{site.data.keyword.cos_short}} plug-in in your cluster and enabled quotas for any PVCs created with the plug-in. Then, you created a PVC which dynamically created a bucket with a quota limit in your {{site.data.keyword.cos_short}} instance. After that, you deployed a simple app that prints the contents of a file in your bucket.


## Next steps
{: #storage-cos-quota-next}


- Set up the [{{site.data.keyword.cos_short}} CLI](/docs/cloud-object-storage?topic=cloud-object-storage-cli-plugin-ic-cos-cli) to point to your bucket.
- Use the {{site.data.keyword.cos_short}} SDKs to [add storage to your apps](/docs/cloud-object-storage?topic=cloud-object-storage-sdk-gs).
