---

copyright:
  years: 2024, 2024
lastupdated: "2024-10-01"


keywords: kubernetes, openshift, object storage add-in, cos

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}



# Installing the {{site.data.keyword.cos_full_notm}} cluster add-on
{: #storage-cos-install-addon}

The {{site.data.keyword.cos_full_notm}} cluster add-on is available in Beta for allowlisted accounts only. To get added to the allowlist, contact support. For more information, see [Requesting access to allowlisted features](/docs/openshift?topic=openshift-allowlist-request).
{: beta}

Prerequisites
:   The {{site.data.keyword.cos_full_notm}} plug-in requires at least 0.2 vCPU and 128 MB of memory.

## Enabling the {{site.data.keyword.cos_full_notm}} add-on
{: #enable-cos-addon}


Before you begin: [Access your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-access_cluster).

1. List the add-ons and find the version you want to install.
    ```sh
    ibmcloud oc cluster addon versions
    ```
    {: pre}

    Example output
    ```sh
    OK
    Name                        Version            Supported Kubernetes Range   Supported OpenShift Range   Kubernetes Default                   OpenShift Default
    ibm-object-csi-driver       0.1 (default)      >=1.30.0                     >=4.15.0                    -                                    -
    ```
    {: screen}

1. Install the add-on.
    ```sh
    ibmcloud oc cluster addon enable --addon ibm-object-csi-driver --cluster CLUSTER [--version VERSION]
    ```
    {: pre}

1. Verify the installation.
    ```sh
    ibmcloud oc cluster addon ls --cluster CLUSTER
    ```
    {: pre}

    ```sh
    OK
    Name                    Version   Health State   Health Status
    ibm-object-csi-driver   0.1       normal         Addon Ready. For more info: http://ibm.biz/addon-state (H1500)
    ```
    {: screen}

1. List the available storage classes.
    ```sh
    oc get sc | grep object
    ```
    {: pre}

    ```sh
    ibm-object-storage-smart-rclone             cos.s3.csi.ibm.io   Delete          Immediate           false                  17h
    ibm-object-storage-smart-rclone-retain      cos.s3.csi.ibm.io   Retain          Immediate           false                  17h
    ibm-object-storage-smart-s3fs               cos.s3.csi.ibm.io   Delete          Immediate           false                  17h
    ibm-object-storage-smart-s3fs-retain        cos.s3.csi.ibm.io   Retain          Immediate           false                  17h
    ibm-object-storage-standard-rclone          cos.s3.csi.ibm.io   Delete          Immediate           false                  17h
    ibm-object-storage-standard-rclone-retain   cos.s3.csi.ibm.io   Retain          Immediate           false                  17h
    ibm-object-storage-standard-s3fs            cos.s3.csi.ibm.io   Delete          Immediate           false                  17h
    ibm-object-storage-standard-s3fs-retain     cos.s3.csi.ibm.io   Retain          Immediate           false                  17h
    ```
    {: screen}


## Deploying an app that uses {{site.data.keyword.cos_full_notm}}
{: #cos-addon-app}

### Create a Kubernetes secret that contains your COS credentials.
{: #cos-addon-app-secret}

1. [Access your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-access_cluster).

1. Save the following configuration as a file called `secret.yaml`.

    ```yaml
    apiVersion: v1
    kind: Secret
    type: cos-s3-csi-driver
    metadata:
        name: <secret_name> # Name your secret
        namespace: <namespace> # Specify the namespace where you want to create the secret.
    data:
        bucketName: <base64-encoded-bucket-name>
        apiKey: <base64-encoded COS Service-Instance-API-key>
        accessKey: <base64 encoded HMAC access key>
        secretKey: <base64 encoded HMAC secret key>
    ```
    {: codeblock}

1. Encode the credentials that you retrieved in the previous section to base64. Repeat this command for each parameter.
    ```sh
    echo -n "<value>" | base64
    ```
    {: pre}

1. Update the configuration file with the base64 encoded values.

1. Create the secret.
    ```sh
    oc apply -f secret.yaml
    ```
    {: pre}


### Create a PVC
{: #cos-addon-app-pvc}

1. Save the following configuration to a file called `pvc.yaml`.

    ```yaml
    apiVersion: v1
    kind: PersistentVolumeClaim
    metadata:
    name: <pvc_name> # Give your PVC the same name as the secret you created in the previous step.
    namespace: <namespace> # The namespace where you want to create the PVC.
    spec:
    accessModes:
    - ReadWriteMany
    resources:
    requests:
        storage: 10Gi
    storageClassName: <storage_class_name> # The storage class you want to use.
    ```
    {: codeblock}

1. Edit the configuration file values. Make sure to specify the same namespace where you created your secret. For a list of storage classes, see the [Storage class reference](#cos-sc-ref-addon).

1. Create the PVC.
    ```sh
    oc apply -f pvc.yaml
    ```
    {: pre}

### Create a deployment
{: #cos-addon-app-dep}

1. Save the following configuration to a file called `dep.yaml`.

    ```yaml
    apiVersion: apps/v1
    kind: Deployment
    metadata:
    name: <name>
    labels:
        app: <name>
    spec:
    replicas: 1
    selector:
        matchLabels:
        app: <name>
    template:
        metadata:
        labels:
            app: <name>
        spec:
        containers:
        - name: app-frontend
            image: <image> # Enter your app image. 
            imagePullPolicy: IfNotPresent
            volumeMounts:
            - mountPath: <path_you_want_to_mount_the_volume_on> # For example `/dev`
            name: cos-csi-volume
        volumes:
        - name: cos-csi-volume
            persistentVolumeClaim:
            claimName: <pvc_name> # Enter the name of the PVC you created earlier.
    ```
    {: codeblock}

1. Create the deployment.
    ```sh
    oc apply -f dep.yaml
    ```
    {: pre}



## Setting up autorecovery for stale volumes
{: #cos-addon-autorecovery}

1. Copy the following yaml and save it as a file called `stale.yaml`
    ```yaml
    apiVersion: objectdriver.csi.ibm.com/v1alpha1
    kind: RecoverStaleVolume
    metadata:
      labels:
        app.kubernetes.io/name: recoverstalevolume
        app.kubernetes.io/instance: recoverstalevolume-sample
      name: recoverstalevolume-sample
      namespace: default
    spec:
      logHistory: 200
      data:
        - namespace: default # The namesapce where your app is deployed
          deployments: [<A comma separated list of all the apps you want to recover>]
    ```
    {: codeblock}

1. Create the `RecoverStaleVolume` resource in your cluster.

    ```sh
    oc create -f stale.yaml
    ```
    {: pre}

    Example output

    ```sh
    recoverstalevolume.objectdriver.csi.ibm.com/recoverstalevolume-sample created
    ```
    {: screen}


1. Verify that the resource was created.
    ```sh
    oc get recoverstalevolume
    ```
    {: pre}

    Example output

    ```sh
    NAME  AGE  recoverstalevolume-sample   41s
    ```
    {: screen}

1. If the issue persists, contact support. Open a [support case](/docs/get-support?topic=get-support-using-avatar). In the case details, be sure to include any relevant log files, error messages, or command outputs.


### Verifying recovery by simulating an error
{: #cos_transport_verify_recovery}

1. List your deployments.
    ```sh
    oc get deploy -o wide
    ```
    {: pre}

    Example output

    ```sh
    NAME               READY   UP-TO-DATE   AVAILABLE   AGE     CONTAINERS     IMAGES     SELECTOR
    cos-csi-test-app   1/1     1            1           7h24m   app-frontend   rabbitmq   app=cos-csi-test-app
    ```
    {: screen}

1. List your app pods.
    ```sh
    oc get pods -o wide
    ```
    {: pre}

    Example output
    ```sh
    NAME                                READY   STATUS    RESTARTS   AGE     IP             NODE           NOMINATED NODE   READINESS GATES
    cos-csi-test-app-6b99bd8bf4-5lt7p   1/1     Running   0          7h24m   172.30.69.21   10.73.114.86   <none>           <none>
    ```
    {: screen}

1. List the pods in the `ibm-object-csi-operator` namespace.
    ```sh
    oc get pods -n ibm-object-csi-operator -o wide
    ```
    {: pre}


    ```sh
    NAME                                                          READY   STATUS    RESTARTS   AGE     IP              NODE           NOMINATED NODE   READINESS GATES
    ibm-object-csi-controller-d64df8f57-l6grj                     3/3     Running   0          7h31m   172.30.69.19    10.73.114.86   <none>           <none>
    ibm-object-csi-node-6d4x4                                     3/3     Running   0          7h31m   172.30.64.24    10.48.3.149    <none>           <none>
    ibm-object-csi-node-gg5pj                                     3/3     Running   0          7h31m   172.30.116.13   10.93.120.14   <none>           <none>
    ibm-object-csi-node-vk8jf                                     3/3     Running   0          7h31m   172.30.69.20    10.73.114.86   <none>           <none>
    ibm-object-csi-operator-controller-manager-8544d4f798-llbf8   1/1     Running   0          7h37m   172.30.69.18    10.73.114.86   <none>           <none>
    ```
    {: pre}

1. Delete the `ibm-object-csi-node-xxx` pod in the `ibm-object-csi-operator` namespace.

    ```sh
    oc delete pod ibm-object-csi-node-vk8jf -n ibm-object-csi-operator
    ```
    {: pre}

    Example output
    ```sh
    pod "ibm-object-csi-node-vk8jf" deleted
    ```
    {: screen}


1. List the pods in the `ibm-object-csi-operator` namespace.
    ```sh
    oc get pods -n ibm-object-csi-operator -o wide
    ```
    {: pre}

    Example output

    ```sh
    NAME                                                          READY   STATUS    RESTARTS   AGE     IP              NODE           NOMINATED NODE   READINESS GATES
    ibm-object-csi-controller-d64df8f57-l6grj                     3/3     Running   0          7h37m   172.30.69.19    10.73.114.86   <none>           <none>
    ibm-object-csi-node-6d4x4                                     3/3     Running   0          7h37m   172.30.64.24    10.48.3.149    <none>           <none>
    ibm-object-csi-node-gg5pj                                     3/3     Running   0          7h37m   172.30.116.13   10.93.120.14   <none>           <none>
    ibm-object-csi-node-kmn94                                     3/3     Running   0          8s      172.30.69.23    10.73.114.86   <none>           <none>
    ibm-object-csi-operator-controller-manager-8544d4f798-llbf8   1/1     Running   0          7h43m   172.30.69.18    10.73.114.86   <none>           <none>
    ```
    {: screen}


1. Get the logs of the `ibm-object-csi-operator-controller-manager` to follow the app pod recovery. Note that the Operator deletes the app's pod so that they get restarted.
    ```sh
    2024-07-10T17:25:39Z	INFO	recoverstalevolume_controller	Time to complete	{"fetchVolumeStatsFromNodeServerPodLogs": 0.066584637}
    2024-07-10T17:25:39Z	INFO	recoverstalevolume_controller	Volume Stats from NodeServer Pod Logs	{"Request.Namespace": "default", "Request.Name": "recoverstalevolume-sample", "volume-stas": {"pvc-9d12a2f5-09a9-4eb4-b1f5-2a727249ed2b":"transport endpoint is not connected "}}
    2024-07-10T17:25:39Z	INFO	recoverstalevolume_controller	Stale Volume Found	{"Request.Namespace": "default", "Request.Name": "recoverstalevolume-sample", "volume": "pvc-9d12a2f5-09a9-4eb4-b1f5-2a727249ed2b"}
    2024-07-10T17:25:39Z	INFO	recoverstalevolume_controller	Pod using stale volume	{"Request.Namespace": "default", "Request.Name": "recoverstalevolume-sample", "volume-name": "pvc-9d12a2f5-09a9-4eb4-b1f5-2a727249ed2b", "pod-name": "cos-csi-test-app-6b99bd8bf4-5lt7p"}
    2024-07-10T17:25:39Z	INFO	recoverstalevolume_controller	Pod deleted.	{"Request.Namespace": "default", "Request.Name": "recoverstalevolume-sample"}
    ```
    {: pre}



## Disabling the {{site.data.keyword.cos_full_notm}} add-on
{: #disable-cos-addon}

1. Run the following command to disable the add-on.
    ```sh
     ibmcloud ks cluster addon disable ibm-object-csi-driver --cluster CLUSTER
     ```
     {: pre}

    Example output
     ```sh
    Data and resources that you created for the add-on might be deleted when the add-on is disabled. Continue? [y/N]> y
    Disabling add-on ibm-object-csi-driver for cluster XXX...
    OK
    ```
    {: screen}

1. Verify the add-on was removed.
    ```sh
    ibmcloud oc cluster addon ls --cluster CLUSTER
    ```
    {: pre}


## {{site.data.keyword.cos_full_notm}} cluster add-on storage classes
{: #cos-sc-ref-addon}

| Name | Reclaim policy | Binding mode |
| --- | --- | --- |
| ibm-object-storage-smart-rclone | Delete | Immediate |
| ibm-object-storage-smart-rclone-retain | Retain | Immediate |
| ibm-object-storage-smart-s3fs | Delete | Immediate |
| ibm-object-storage-smart-s3fs-retain | Retain | Immediate |
| ibm-object-storage-standard-rclone | Delete | Immediate |
| ibm-object-storage-standard-rclone-retain | Retain | Immediate |
| ibm-object-storage-standard-s3fs |  Delete | Immediate |
| ibm-object-storage-standard-s3fs-retain | Retain | Immediate |
{: caption="COS cluster add-on storage classes." caption-side="bottom"}

