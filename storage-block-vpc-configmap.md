---

copyright: 
  years: 2022, 2024
lastupdated: "2024-01-03"


keywords: openshift, block storage, snapshot

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}


# Customizing the {{site.data.keyword.block_storage_is_short}} configmap
{: #storage-block-vpc-configmap}


You can customize the {{site.data.keyword.block_storage_is_short}} configmap for more control over snapshot settings.
{: shortdesc}

1. Download the {{site.data.keyword.block_storage_is_short}} configmap and [review the parameters](#storage-block-vpc-configmap-reference).
    ```sh
    kubectl get cm addon-vpc-block-csi-driver-configmap -n kube-system -o yaml > vpc-configmap.yaml 
    ```
    {: pre}

1. Open the `configmap.yaml` file and update the settings that you want to change.
1. Reapply the configmap to your cluster.
    ```sh
    kubectl apply -f vpc-configmap.yaml
    ```
    {: pre}

1. Verify that the pods are restarted successfully and configurations are applied
    ```sh
    kubectl get pods -n kube-system | grep vpc-block
    ```
    {: pre}


## {{site.data.keyword.block_storage_is_short}} configmap reference
{: #storage-block-vpc-configmap-reference}


```yaml
data:
  IsVolumeSnapshotClassDefault: "true"
  IsStorageClassDefault: "true"
  AttachDetachMinRetryGAP: "3" # Initial retry interval for checking Attach/Detach Status. Default 3 seconds
  AttachDetachMinRetryAttempt: "3" # Number of attempts for AttachDetachMinRetryGAP. Default is 3 retries for 3 seconds retry gap.
  AttachDetachMaxRetryAttempt: "46" # Total number of retries for for checking Attach/Detach Status. Default is 46 times i.e ~7 mins (3 secs * 3 times + 6 secs * 6 times + 10 secs * 10 times)
  AttacherWorkerThreads: "15" # The number of goroutines for processing VolumeAttachments
  AttacherKubeAPIBurst: "10" # The number of requests to the Kubernetes API server, exceeding the QPS, that can be sent at any given time
  AttacherKubeAPIQPS: "5.0" # The number of requests per second sent by a Kubernetes client to the Kubernetes API server.
  
  
  # Adjust the resource request per container
  CSIDriverRegistrarCPURequest: "10m" #container:csi-driver-registrar, resource-type: cpu-request
  CSIDriverRegistrarMemoryRequest: "20Mi" #container:csi-driver-registrar,  resource-type: memory-request
  NodeDriverMemoryRequest: "30m" #container:iks-vpc-block-node-driver, resource-type: cpu-request
  NodeDriverCPURequest: "75Mi" #container:iks-vpc-block-node-driver, resource-type: memory-request
  LivenessProbeCPURequest: "5m" #container:liveness-probe, resource-type: cpu-request
  LivenessProbeMemoryRequest: "10Mi" #container:liveness-probe, resource-type: memory-request
  SecretSidecarCPURequest: "10m" #container:storage-secret-sidecar, resource-type: cpu-request
  SecretSidecarMemoryRequest: "20Mi" #container:storage-secret-sidecar, resource-type: memory-request
  CSIProvisionerCPURequest: "20m" #container:csi-provisioner, resource-type: cpu-request
  CSIProvisionerMemoryRequest: "40Mi" #container:csi-provisioner, resource-type: memory-request
  CSIAttacherCPURequest: "15m" #container:csi-attacher, resource-type: cpu-request
  CSIAttacherMemoryRequest: "30Mi" #container:csi-attacher, resource-type: memory-request
  CSIResizerCPURequest: "20m" #container:csi-resizer, resource-type: cpu-request
  CSIResizerMemoryRequest: "40Mi" #container:csi-resizer, resource-type: memory-request
  BlockDriverCPURequest: "75m" #container:iks-vpc-block-driver, resource-type: cpu-request
  BlockDriverMemoryRequest: "150Mi" #container:iks-vpc-block-driver, resource-type: memory-request
  CSISnapshotterCPURequest: "20m" #container:csi-snapshotter, resource-type: cpu-request
  CSISnapshotterMemoryRequest: "40Mi" #container:csi-snapshotter, resource-type: memory-request

  # Set resource limits per container
  CSIDriverRegistrarCPULimit: "40m" #container:csi-driver-registrar, resource-type: cpu-limit
  CSIDriverRegistrarMemoryLimit: "80Mi" #container:csi-driver-registrar, resource-type: memory-limit
  NodeDriverCPULimit: "120m" #container:iks-vpc-block-node-driver, resource-type: cpu-limit
  NodeDriverMemoryLimit: "300Mi" #container:iks-vpc-block-node-driver, resource-type: memory-limit
  LivenessProbeCPULimit: "20m" #container:liveness-probe, resource-type: cpu-limit
  LivenessProbeMemoryLimit: "40Mi" #container:liveness-probe, resource-type: memory-limit
  SecretSidecarCPULimit: "40m" #container:storage-secret-sidecar, resource-type: cpu-limit
  SecretSidecarMemoryLimit: "80Mi" #container:storage-secret-sidecar, resource-type: memory-limit
  CSIProvisionerCPULimit: "80m" #container:csi-provisioner, resource-type: cpu-limit
  CSIProvisionerMemoryLimit: "160Mi" #container:csi-provisioner, resource-type: memory-limit
  CSIAttacherCPULimits: "60m" #container:csi-attacher, resource-type: cpu-limit
  CSIAttacherMemoryLimit: "120Mi" #container:csi-attacher, resource-type: memory-limit
  CSIResizerCPULimit: "80m" #container:csi-resizer, resource-type: cpu-limit
  CSIResizerMemoryLimit: "160Mi" #container:csi-resizer, resource-type: memory-limit
  BlockDriverCPULimit: "300m" #container:iks-vpc-block-driver, resource-type: cpu-limit
  BlockDriverMemoryLimit: "600Mi" #container:iks-vpc-block-driver, resource-type: memory-limit
  CSISnapshotterCPULimit: "80m" #container:csi-snapshotter, resource-type: cpu-limit
  CSISnapshotterMemoryLimit: "160Mi" #container:csi-snapshotter, resource-type: memory-limit
  CSISnapshotterRetryIntervalStart: "1s" #container:csi-snapshotter, Initial retry interval of failed volume snapshot creation or deletion.
  CSISnapshotterRetryIntervalMax: "300s" #container:csi-snapshotter, Maximum retry interval of failed volume snapshot creation or deletion.
  CSISidecarLogLevel: "5" #container:csi-snapshotter, glog/klog log level
  IsSnapshotEnabled : "true" #container: iks-vpc-block-driver
  CustomSnapshotCreateDelay: "300" #container: iks-vpc-block-driver
  VolumeAttachmentLimit: "12" #container: iks-vpc-block-driver
```
{: codeblock}

