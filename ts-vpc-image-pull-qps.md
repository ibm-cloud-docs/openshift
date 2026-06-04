---

copyright:
  years: 2026
lastupdated: "2026-06-03"

keywords: vpc, image pull, qps exceeded, bandwidth, worker nodes, secondary storage

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why do pods show "pull QPS exceeded" errors during image pulls?
{: #ts-vpc-image-pull-qps}
{: troubleshoot}
{: support}

When pods are starting up, you might see errors indicating that image pull operations are being throttled with messages like "pull QPS exceeded".
{: shortdesc}

When you deploy pods that need to pull container images, you might observe the following symptoms:
{: tsSymptoms}

- Error messages containing "pull QPS exceeded" during pod startup
- Slow image pull times, especially when pulling multiple large images
- Pods taking longer than expected to reach the `Running` state
- Image pull operations appearing to be throttled or rate-limited

The most likely cause of slow image pulling with "pull QPS exceeded" errors is that your VPC worker nodes are hitting their disk I/O bandwidth limit.
{: tsCauses}

VPC worker nodes have different bandwidth limits depending on their configuration:

- **Standard worker nodes (without secondary storage)**: Limited to **393 Mbps (49 MB/sec)** for disk I/O operations
- **Worker nodes with secondary storage**: Higher bandwidth limits depending on the storage tier selected

When multiple pods attempt to pull large container images simultaneously:

1. Each image pull operation consumes disk I/O bandwidth
2. The combined bandwidth demand can quickly saturate the 49 MB/sec limit
3. Once the limit is reached, image pull operations slow down significantly
4. Kubernetes might report "pull QPS exceeded" errors as it throttles operations

To determine if you are hitting the VPC worker node bandwidth limit, use the IBM Cloud monitoring capabilities.
{: tsResolve}




## Check disk I/O bandwidth
{: #check-bandwidth-openshift}

1. Navigate to **Observe → Metrics** in the OpenShift console for your cluster.

2. Use the following Prometheus query to monitor disk read and write rates:

    ```promql
    irate(node_disk_read_bytes_total[2m]) + irate(node_disk_written_bytes_total[2m])
    ```
    {: codeblock}

3. Interpret the results:
    - If any devices show values approaching or at **49M (49 MB/sec)**, you are hitting the bandwidth limit.
    - Sustained values at or near this limit during image pull operations confirm bandwidth saturation.
    - Multiple spikes to this limit indicate repeated bandwidth constraints.





### Check image pull times
{: #check-pull-times}

You can also check image pull times directly:

```sh
oc get events -A | grep -E "Successfully pulled image"
```
{: pre}

This command shows how long each image pull took, helping you identify slow pulls.

## Resolve the issue
{: #resolve-bandwidth}

### Primary solution: Use worker pools with secondary storage
{: #use-secondary-storage}

The recommended solution is to use worker pools with secondary storage attached. Secondary storage with `10iops-tier` provides dedicated I/O bandwidth that doesn't compete with the boot disk, resulting in much higher throughput for concurrent image pulls and faster pod startup times.

1. [Create a new worker pool](/docs/containers?topic=containers-add-workers-vpc) with secondary storage.
    - When you create a new worker pool, select a flavor with secondary storage.
    - Use one of the `10iops-tier` storage options for optimal performance.

2. [Migrate your workloads](/docs/containers?topic=containers-update_app#app_rolling) to the new pool.

3. [Drain and remove the old worker pool](/docs/containers?topic=containers-kubernetes-service-cli#cs_worker_pool_rm) after migration is complete.



### Additional considerations
{: #additional-considerations}

While upgrading to secondary storage is the primary solution, you can also:

Reduce image sizes
:   Use multi-stage builds and minimize layers

Use image caching
:   Pre-pull commonly used images to worker nodes

Optimize imagePullPolicy
:   Configure your pod specifications to reduce unnecessary pulls:
    - Use `imagePullPolicy: IfNotPresent` to pull images only if they don't already exist on the node.
    - Avoid `imagePullPolicy: Always` unless you specifically need to pull the latest version every time.
    - For production workloads, use specific image tags, not `latest`, combined with `IfNotPresent` to minimize pulls.

Set up monitoring and alerts
:   Set up alerts for sustained high disk I/O rates that approach 49 MB/sec.
    - Monitor image pull times as part of your deployment metrics.
    - Track pod startup times to identify performance degradation.


