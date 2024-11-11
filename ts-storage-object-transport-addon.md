---

copyright: 
  years: 2024, 2024
lastupdated: "2024-11-08"


keywords: openshift, {{site.data.keyword.openshiftlong_notm}}, kubernetes, help, network, connectivity

subcollection: openshift

content-type: troubleshoot

---


{{site.data.keyword.attribute-definition-list}}

# Why do I see transport endpoint not connected errors when using the {{site.data.keyword.cos_full_notm}} cluster add-on?
{: #cos_transport_ts_connect_addon}
{: support}

The following steps apply to the {{site.data.keyword.cos_full_notm}} cluster add-on only. If you are using the Helm plug-in, see [Why do I see transport endpoint not connected errors?](/docs/openshift?topic=openshift-cos_transport_ts_connect) instead.
{: important}



When the connection is lost between the `ibm-object-csi-driver` node server pods and application pods, you might see `TransportEndpoint` connection errors.
{: tsSymptoms}


One possible case for this error is when patch updates are applied. In this case, apps pods can experience temporary connection errors.
{: tsCauses}


The `ibm-object-csi-driver` supports autorecovery of volumes which have lost connection to `s3fs`. Autorecovery can be achieved by deploying a custom resource provided by the `ibm-object-csi-driver`. This resource continuously monitors the applications and the namespace that you specify and automatically restarts app pods when `TransportEndpoint` errors occur.
{: tsResolve}

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


1. Verify the resource was created.
    ```sh
    oc get recoverstalevolume
    ```
    {: pre}

    Example output

    ```sh
    NAME  AGE  recoverstalevolume-sample   41s
    ```
    {: screen}

1. If the issue persists, contact support. Open a [support case](/docs/account?topic=account-using-avatar). In the case details, be sure to include any relevant log files, error messages, or command outputs.


## Verifying recovery by simulating an error
{: #cos_transport_verify}

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
