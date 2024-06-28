---

copyright: 
  years: 2024, 2024
lastupdated: "2024-06-28"


keywords: kubernetes, openshift, MountingTargetFailed, encryption in-transit, eit

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}


# Why do I see a `MountingTargetFailed` error for {{site.data.keyword.filestorage_vpc_short}}?
{: #ts-storage-vpc-file-eit-mount-failed}

[Virtual Private Cloud]{: tag-vpc}


Your app that uses encryption in-transit {{site.data.keyword.filestorage_vpc_short}} fails to start and you see an error message similar to the following.
{: tsSymptoms}


```sh
Code: MountingTargetFailed, Description: Failed to mount target., BackendError: Response from mount-helper-container -> Exit Status Code: exit status 1 ,ResponseCode: 500, Action: Check node server logs for more details on mount failure.}
```
{: screen}


```sh
Warning  FailedMount  5m     kubelet            MountVolume.SetUp failed for volume "pvc-3985f611-538b-4a1c-b80a-36e313ba8157" : rpc error: code = Internal desc = {RequestID: c90443bc-cb90-4905-b2fe-488735b0579e , Code: MetadataServiceNotEnabled, Description: Failed to mount target., BackendError: Response from mount-helper-container -> Exit Status Code: exit status 1 ,ResponseCode: 500, Action: Metadata service might not be enabled for worker node. Make sure to use IKS>=1.30 or ROKS>=4.16 cluster.}
```
{: screen}



Encryption in-transit is available in {{site.data.keyword.openshiftlong_notm}} version 4.16  and later. You might see the previous errors if you try using EIT features in a cluster version 4.15 and earlier.
{: tsCauses}


Get the logs by using the requestID mentioned in the description.
{: tsResolve}

1. Get the node where the application pod is running and the volumeID.
    ```sh
    kubectl get pods -n application -o wide
    ```
    {: pre}

    ```sh
    my-eit-app                            0/1     ContainerCreating   0          128s   10.240.0.238     10.240.0.238   <none>           <none>
    ```
    {: screen}

1. Review the logs for the same node server pod.

    ```sh
    kubectl get pods -n kube-system -o wide | grep vpc-file-csi-node | grep <nodeID>
    ```
    {: pre}

    ```sh
    ibm-vpc-file-csi-node-xxxx                          4/4     Running     0             75m     10.240.0.238  10.240.0.238     <none>           <none>
    ```
    {: pre}

    ```sh
    kubectl logs ibm-vpc-file-csi-node-xxxx -n kube-system -c iks-vpc-file-node-driver | grep c90443bc-cb90-4905-b2fe-488735b0579e 
    ```
    {: pre}

    Review the events.

    ```sh
    Type     Reason       Age                   From               Message
    ----     ------       ----                  ----               -------
    Normal   Scheduled    5m59s                 default-scheduler  Successfully assigned default/eit-app-5dcfd457f4-29jsr to test
    Warning  FailedMount  119s (x2 over 4m)     kubelet            MountVolume.SetUp failed for volume "pvc-129c8073-95f7-4cba-bff0-fd3a0cde0f94" : rpc error: code = DeadlineExceeded desc = context deadline exceeded
    Warning  FailedMount  102s (x2 over 3m57s)  kubelet            Unable to attach or mount volumes: unmounted volumes=[my-volume], unattached volumes=[], failed to process volumes=[]: timed out waiting for the condition
    ```
    {: screen}


1. Get the node where the application pod is running and the volumeID

    ```sh
    kubectl get pods -n application -o wide
    ```
    {: pre}

    ```
    my-eit-app                            0/1     ContainerCreating   0          128s   10.240.0.238     10.240.0.238   <none>           <none>
    ```
    {: screen}

    ```sh
    kubectl describe pv <pv-name> | grep volumeID
    ```
    {: pre}

1.  Get the `nodeServer` logs of the node where application is running.

    ```sh
    kubectl get pods -n kube-system | grep file | grep NODEIP
    ```
    {: pre}


1. Get the `requestID` from the following command.
    ```sh
    kubectl logs ibm-vpc-file-csi-node-xxxx -n kube-system -c iks-vpc-file-node-driver | grep <volumeID>
    ```
    {: pre}

1. Review the events for the `requestID`.
    ```sh
    kubectl logs ibm-vpc-file-csi-node-xxxx -n kube-system -c iks-vpc-file-node-driver | grep <requestID>
    ```
    {: pre}


