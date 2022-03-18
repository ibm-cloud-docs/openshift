---

copyright:
  years: 2020, 2022
lastupdated: "2022-03-18"

keywords: COS, cloud object storage, satellite storage, object storage, satellite, satellite configurations,

subcollection: satellite

---

{{site.data.keyword.attribute-definition-list}}


# Installing the {{site.data.keyword.cos_full_notm}} plug-in on {{site.data.keyword.satelliteshort}} clusters
{: #storage-sat-cos}

Complete the following steps to set up {{site.data.keyword.cos_full_notm}} on your {{site.data.keyword.satelliteshort}} clusters.
{: shortdesc}

{{site.data.keyword.cos_short}} isn't supported for {{site.data.keyword.satelliteshort}} service clusters and is only supported for single cluster deployments. This means that to deploy {{site.data.keyword.cos_short}} to multiple {{site.data.keyword.satelliteshort}} clusters, you must repeat these steps for each cluster.
{: note}

You can use the {{site.data.keyword.cos_short}} plug-in with {{site.data.keyword.cos_full_notm}} or with another s3 object storage service such as AWS s3.


## Setting up your {{site.data.keyword.satelliteshort}} location
{: #sat-storage-cos-pre}

Before you deploy the {{site.data.keyword.cos_full_notm}} drivers on your {{site.data.keyword.satelliteshort}} clusters, set up your location.
{: shortdesc}

1. Before you can deploy the {{site.data.keyword.cos_full_notm}}, follow the steps to set up a [{{site.data.keyword.satelliteshort}} location](/docs/satellite?topic=satellite-locations) and create a cluster.
2. **Optional**: If you want use {{site.data.keyword.cos_full_notm}}, [create an instance](/docs/openshift?topic=openshift-storage-cos-understand).


## Retrieving the configuration parameters
{: #sat-storage-cos-params}

Retrieve the {{site.data.keyword.cos_full_notm}} Helm chart configuration parameters.
{: shortdesc}

1. [Log in to your account. If applicable, target the appropriate resource group. Set the context for your cluster.](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure)
1. Retrieve your worker operating system (`workerOS`) and platform information by running the following command. Make a note of the output.
    ```sh
    kubectl get nodes -o yaml | grep 'ibm-cloud\.kubernetes\.io/os'
    ```
    {: pre}
    
    Example output
    ```sh
    ibm-cloud.kubernetes.io/os: REDHAT_7_64
    ibm-cloud.kubernetes.io/os: REDHAT_7_64
    ```
    {: screen}
    
1. Retrieve the `kubelet` driver path by running the following command. Make a note of the output.
    ```sh
    kubectl get nodes -o yaml | grep 'node\.openshift\.io/os_id'
    ```
    {: pre}
    
    Example output
    
    ```sh
    node.openshift.io/os_id: rhel
    node.openshift.io/os_id: rhel
    ```
    {: screen}
    
## Installing Helm and adding the `ibm-helm` Helm repo
{: #sat-storage-cos-helm-deploy}
    
Install Helm and add the {{site.data.keyword.cos_full_notm}} Helm chart to your cluster by completing the following steps.
{: shortdesc}

You can deploy the {{site.data.keyword.cos_full_notm}} Helm chart to only a single cluster. Service clusters and cluster groups aren't supported. To deploy the Helm chart to multiple clusters, repeat the following steps for each cluster.
{: important}

1. [Log in to your account. If applicable, target the appropriate resource group. Set the context for your cluster.](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure)
1. Install [Helm](https://helm.sh/docs/intro/install/){: external}.
    
1. Run the following command to add the `ibm-helm` repo to your cluster.

    ```sh
    helm repo add ibm-helm https://raw.githubusercontent.com/IBM/charts/master/repo/ibm-helm
    ```
    {: pre}
    
1. Install the Helm chart on your local machine.
    ```sh
    helm fetch --untar ibm-helm/ibm-object-storage-plugin
    ```
    {: pre}
    
1. Update the `ibm-helm` repo.
    ```sh
    helm repo update
    ```
    {: pre}



### Installing the plug-in from the console
{: #sat-storage-cos-install-console}

Complete the following steps to install the {{site.data.keyword.cos_full_notm}} Helm chart from the console.


1. From the [{{site.data.keyword.satelliteshort}} console](https://cloud.ibm.com/satellite/locations){: external}, click **Clusters**. 
1. Click the cluster where you want to install the plug-in, click **Manage Cluster**, and then click **OpenShift web console**.
1. Open the **Developer** perspective, and click **Helm**.
1. In the **Project** menu, select the `ibm-object-s3fs` project. If you don't have an `ibm-object-s3fs` project, create it by clicking **Create Project**.
1. On the **Helm Charts** page, search for `ibm`, click the latest version of the `Ibm Object Storage Plugin` and click **Install Helm Chart**.
1. On the **Install Helm Chart** page, click **YAML View** and then enter the configuration parameters.

    Release name
    :   Enter `ibm-object-storage-plugin`.
    
    Access Policy
    :   Leave this setting as `false`.

    COS endpoint
    :   Enter the s3 endpoint that you want to use. 
    :   Example {{site.data.keyword.cos_full_notm}} endpoint: `https://s3.us.cloud-object-storage.appdomain.cloud`.
    :   Example AWS `eu-west-1` endpoint: `https://s3.eu-west-1.amazonaws.com`.

    Storage class
    :   Enter the storage class that you want to use. 
    :   Example {{site.data.keyword.cos_full_notm}} storage class: `us-smart`. For more information, see [Location constraints](/docs/cloud-object-storage/basics?topic=cloud-object-storage-classes#classes-locationconstraint).
    :   Example AWS storage class: ``.
    
    DataCenter
    :   Enter the location of your {{site.data.keyword.satelliteshort}} cluster. To retrieve this parameter run `ibmcloud sat cluster ls`. For example, if your data location is `wdc` enter `us-east`. For more information, see [{{site.data.keyword.satelliteshort}} locations](/docs/satellite?topic=satellite-sat-regions).

    IAM endpoint
    :   Enter `https://iam.cloud.ibm.com`.

    Kube driver
    :   The driver path for the `kubelet`. To find this parameter value, run `kubectl get nodes -o yaml | grep 'node\.openshift\.io/os_id'`. 
    :   If the output has `rhel`, enter `"/usr/libexec/kubernetes"`. 
    :   If the output has `rhcos`, enter `"/etc/kubernetes"`. 

    License
    :   Enable this setting as `true`.
    
    Container Platform
    :   The platform of the worker nodes. To retrieve this parameter, run `kubectl get nodes -o yaml | grep 'ibm-cloud\.kubernetes\.io/os'`.
    :   If the output is `REDHAT_7_64` or `OPENSHIFT` for example, enter `"redhat"` for the worker OS and `"openshift"` for the platform.

    Service Provider
    :   Enter `SATELLITE`.
    
    Region
    :   For {{site.data.keyword.cos_full_notm}}, enter `us-smart`.
    :   For AWS, enter your AWS region. For example, `us-east-1`.

    Worker OS
    :   The operating system of the worker nodes. To retrieve this parameter, run `kubectl get nodes -o yaml | grep 'ibm-cloud\.kubernetes\.io/os'`. 
    :   If the output is `REDHAT_7_64` for example, enter `"redhat"`.
    
    
1. Click **Install**

1. Verify your installation by listing the storage classes.
    ```sh
    oc get storageclass | grep ibmc-s3fs
    ```
    {: pre}
    
    Example output
    
    ```sh
    ibmc-s3fs-cos        ibm.io/ibmc-s3fs   Delete          Immediate           false                  2m23s
    ibmc-s3fs-cos-perf   ibm.io/ibmc-s3fs   Delete          Immediate           false                  2m23s
    ```
    {: pre}
    

## Creating a secret that uses your s3 credentials
{: #sat-storage-cos-secret}


1. Retrieve your `access-key` and `secret-key` credentials for your s3 object storage provider. 
    - For AWS, see [AWS s3](https://docs.aws.amazon.com/AmazonS3/latest/userguide/MakingRequests.html){: external}.
    - For {{site.data.keyword.cos_full_notm}}, see [Creating service credentials](/docs/containers?topic=containers-storage-cos-understand#create_cos_secret).
    
2. Encode your access key and secret key to base64.
    ```sh
    echo "access-key" | base64
    echo "secret-key" | base64
    ```
    {: pre}
    
3. Create a secret configuration file called `secret.yaml` that uses the credentials that you retrieved earlier. 
    
    ```sh
    apiVersion: v1
    metadata:
      name: my-secret
    data:
      access-key: <base64-encoded-access-key>
      secret-key: <base64-encoded-secret-key>
    kind: Secret
    type: ibm/ibmc-s3fs
    ```
    {: codeblock}
    
4. Create the secret in your cluster.
    ```sh
    kubectl apply -f secret.yaml
    ```
    {: pre}


## Deploying an app that uses object storage
{: #sat-storage-cos-app}


1. Create a persistent volume claim (PVC).
    ```yaml
    kind: PersistentVolumeClaim
    apiVersion: v1
    metadata: 
        name: <NAME> #Enter a name for your PVC.
        namespace: default
        annotations: 
        ibm.io/auto-create-bucket: "false"
        ibm.io/auto-delete-bucket: "false" 
        ibm.io/bucket: <BUCKET-NAME> #Enter the name of your object storage bucket.
        ibm.io/secret-name: <SECRET-NAME> #Enter the name of the secret you created earlier.
        ibm.io/secret-namespace: <default> #Enter the namespace where you want to create the PVC.
    spec: 
        accessModes:
        - ReadWriteOnce
        resources:
            requests:
                storage: 10gi
        storageClassName: ibmc-s3fs-cos #The storage class that you want to use. 
    ```
    {: codeblock}
    
    `name`
    :   Enter a name for your PVC.
    
    `bucket-name`
    :   Enter the name of the object storage bucket that you want to use for your app data.
    
    `secret-name`
    :   Enter the name of the secret that you created earlier. Example: "my-secret".
    
    `storageClassName`
    :   Enter the name of the storage class you want to use.
    :   For AWS, enter `Standard`.
    :   For {{site.data.keyword.cos_full_notm}}, enter `ibm-s3fs-cos` or `ibm-s3fs-cos-perf`.
    
2. Deploy an app pod that uses the PVC you created earlier.
    ```yaml
    apiVersion: v1
    kind: Pod
    metadata:
        name: cos-pod
    spec: 
        securityContext:
            runAsUser: 2000
            fsGroup: 2000
        volumes:
        -name: <VOLUME-NAME>
            persistentVolumeClaim:
                claimName: <PVC-NAME>
        - name: hostpath-test
            hostPath: 
            path: /var/mydata01
            type: DirectoryOrCreate
    containers: 
        - image: nginx # Your containerized app image.
        imagePullPolicy: Always
        volumeMounts:
            -name: devtest-vol
                mountPath: /mount-path # The mount path for your app. 
   ```
    
    
### Upgrading the Object Storage plug-in
{: #sat-storage-cos-upgrade}

You can upgrade the Object Storage plug-in in your cluster by running the following command.
{: shortdesc}

```sh
helm upgrade ibm-object-storage-plugin ibm-helm/ibm-object-storage-plugin  --set provider="SATELLITE" --set workerOS="<worker-os>" --set platform="<platform>" --set license=true --set cos.endpoint=<endpoint> --set cos.storageClass=<storage-class> [--version <new-version>] --namespace "ibm-object-s3fs"
```
{: pre}

`worker-os` and `platform`
:   The operating system of the worker nodes. To retrieve this parameter, run `kubectl get nodes -o yaml | grep 'ibm-cloud\.kubernetes\.io/os'`. 
:   If the output is `REDHAT_7_64` for example, enter `"redhat"` for the worker OS and `"openshift"` for the `platform`.

`kube-driver-path`
:   The driver path for the `kubelet`. To retrieve this parameter, run `kubectl get nodes -o yaml | grep 'node\.openshift\.io/os_id'`. 
:   If the output has `rhel`, enter `"/usr/libexec/kubernetes"`. 
:   If the output has `rhcos`, enter `"/etc/kubernetes"`.

`endpoint`
:   Enter the s3 endpoint that you want to use. 
:   Example {{site.data.keyword.cos_full_notm}} endpoint: `https://s3.us.cloud-object-storage.appdomain.cloud`.
:   Example AWS `eu-west-1` endpoint: `https://s3.eu-west-1.amazonaws.com`.

`new-version`
:   Enter the version that you want to upgrade to. Review the {{site.data.keyword.cos_full_notm}} [change log](/docs/containers?topic=containers-cos_plugin_changelog){: external} for version information.

`storageClass`
:   Enter the {{site.data.keyword.cos_full_notm}} storage class that you want to use.





## Uninstalling the plug-in and Helm chart
{: #sat-storage-cos-rm}

Complete the following steps to remove the Helm chart from your cluster.

```sh
helm uninstall <release_name> -n <namespace>
```
{: pre}







