---

copyright:
  years: 2026
lastupdated: "2026-09-17"

keywords: openshift, resiliency, high availability, control plane, patch, master refresh, replica set, pod disruption budget, probes

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}

# Developing and testing apps for resiliency
{: #app-resiliency}

Learn how {{site.data.keyword.openshiftlong_notm}} handles control plane maintenance, how maintenance updates affect running workloads, and how to test and architect your applications for high resiliency.
{: shortdesc}

## Overview of cluster architecture and responsibilities
{: #app-resiliency-overview}

{{site.data.keyword.openshiftlong_notm}} is a managed Kubernetes service. In every cluster, architecture is divided into two planes with [distinct ownership responsibilities](/docs/openshift?topic=openshift-responsibilities_{{site.data.keyword.containershort}}):

Control plane
:   Managed by {{site.data.keyword.IBM_notm}}. Includes the Kubernetes API server, etcd, controller manager, and scheduler.

Data plane
:   Managed by you. Includes worker nodes, application pods, storage configurations, and networking add-ons.

| Plane | Managed by | Components |
|---|---|---|
| Control plane | {{site.data.keyword.IBM_notm}} | API server, etcd, controller manager, scheduler |
| Data plane | You | Worker nodes, application pods, storage, networking add-ons |
{: caption="Ownership responsibilities for cluster control plane and data plane" caption-side="bottom"}

{{site.data.keyword.IBM_notm}} regularly applies patch version updates to the control plane. These patches address security vulnerabilities, apply critical bug fixes, and ensure that clusters remain compliant with {{site.data.keyword.IBM_notm}} security requirements. Understanding how these patches are applied helps you make informed decisions about your application architecture.

Applications running in cloud environments are exposed to dynamic conditions, including transient network disruptions, hosting infrastructure maintenance, and third-party service latency. Designing and testing for resiliency across all conditions ensures reliable production workloads.

## How {{site.data.keyword.IBM_notm}} applies control plane patches
{: #control-plane-patches}

Control plane components for every {{site.data.keyword.openshiftlong_notm}} cluster run in a highly available (HA) configuration. Multiple replicas of each component are distributed across independent availability zones so that no single point of failure exists within the control plane.

When a patch upgrade is applied, {{site.data.keyword.IBM_notm}} uses a rolling recreate strategy. Replicas are updated sequentially:

- The Kubernetes API server remains reachable throughout the upgrade.
- Cluster operations, such as scheduling, autoscaling, and health checks, continue uninterrupted.
- {{site.data.keyword.IBM_notm}} provides a graceful shutdown delay to allow in-flight connections to complete before a pod is removed.

Control plane patch upgrades are designed so that there is no impact on user applications running in the data plane. Your pods, services, and workloads continue running normally on worker nodes throughout the process.
{: note}

## Workload impact during control plane updates
{: #workload-impact}

Because the data plane is user-managed, {{site.data.keyword.IBM_notm}} control plane patches do not restart, reschedule, or modify your worker nodes or running application pods.

However, applications or tooling that make frequent, direct calls to the Kubernetes API (such as custom controllers, operators, CI/CD pipelines, or monitoring agents that watch cluster state) must handle transient API errors gracefully. Follow general Kubernetes best practices:

- Implement retry logic with exponential back-off for all API calls.
- Avoid relying on persistent open connections to the API server without reconnection logic.

## Simulating scenarios to test application resiliency
{: #simulating-resiliency}

To build confidence in application resiliency, simulate production failure conditions in a nonproduction environment before scheduled maintenance or unexpected disruptions occur.

During any simulation, monitor your applications for indicators of disruption: unexpected pod restarts, spikes in error logs, degraded response times, or dropped client requests. Use these observations to refine retry logic, tune health probes, or adjust replica topology.

Running cluster management commands (such as master refresh or worker pool resize) requires Administrator or Operator platform access and cluster management service permissions. If you are an application developer without cluster infrastructure access, coordinate with your cluster administrator to run these simulations.
{: note}

### Simulating a control plane patch with a control plane refresh
{: #simulate-control-plane-refresh}

Triggering a control plane refresh initiates the rolling update process that {{site.data.keyword.IBM_notm}} uses during patch upgrades. This test verifies that your application and tooling handle control plane replica transitions smoothly.

1. Trigger a control plane refresh on your cluster.

   ```sh
   ibmcloud oc cluster master refresh --cluster CLUSTER_NAME_OR_ID
   ```
   {: pre}

1. Verify that your applications continue processing traffic without interruption and that client-facing endpoints remain responsive.

### Simulating network routing updates by adding and removing worker nodes
{: #simulate-worker-routing}

Adding and removing worker nodes causes Kubernetes to update internal network routing logic across the cluster, simulating the conditions that occur when nodes cycle during infrastructure maintenance.

1. Resize your worker pool to add a temporary worker node.

   ```sh
   ibmcloud oc worker-pool resize --cluster CLUSTER_NAME_OR_ID --worker-pool WORKER_POOL_NAME --size-per-zone NEW_SIZE
   ```
   {: pre}

1. Monitor your application logs and response latency while the new worker node initializes and joins the cluster network.

1. When the test is complete, remove the test worker node.

   To perform a targeted removal of the specific worker node created in step 1:

   1. Cordon and drain the worker node before deleting it to ensure workloads are gracefully rescheduled.

      ```sh
      oc cordon NODE_NAME
      oc drain NODE_NAME --ignore-daemonsets --delete-emptydir-data
      ```
      {: pre}

   1. Delete the worker node from the cluster.

      ```sh
      ibmcloud oc worker rm --cluster CLUSTER_NAME_OR_ID --worker WORKER_ID
      ```
      {: pre}

   1. Resize the worker pool back to its original capacity by using the `ibmcloud oc worker-pool resize` command with your original `--size-per-zone` value.

   As an alternative, less targeted approach, you can simply resize the worker pool back to its original size by using the `ibmcloud oc worker-pool resize` command from step 1 without explicitly deleting a specific node.

## Recommended practices for workload resiliency
{: #resiliency-best-practices}

The resiliency of your application during cluster events depends on how your workloads are designed and configured. Apply the following recommended practices to your Kubernetes workload specifications:

### Run multiple replicas for every workload
{: #resiliency-replicas}

A single-replica deployment cannot tolerate disruption. Set `spec.replicas` to at least `2` (preferably `3` or more for production workloads) so that the loss or rescheduling of a single pod does not cause downtime.

### Spread replicas across zones and worker nodes
{: #resiliency-topology-spread}

Configure `topologySpreadConstraints` or pod anti-affinity rules in your deployment configuration. Distributing pods across multiple availability zones and worker nodes prevents a single zone disruption or node maintenance event from taking down all replicas simultaneously.

### Configure Pod Disruption Budgets (PDBs)
{: #resiliency-pdb}

A `PodDisruptionBudget` resource specifies the minimum number or percentage of pods that must remain available during voluntary disruptions, such as node draining or cluster updates. Define a PDB for every critical workload to prevent administrative operations from evicting more pods than your application can tolerate.

### Define readiness and liveness probes
{: #resiliency-probes}

Configure readiness and liveness probes in your container specifications:

- **Readiness probes:** Ensure that Kubernetes routes traffic only to pods that are initialized and ready to serve requests.
- **Liveness probes:** Enable Kubernetes to automatically restart containers that enter a deadlocked or unhealthy state.

### Set appropriate resource requests and limits
{: #resiliency-resources}

Specify realistic CPU and memory requests and limits for each container. Requests ensure that the Kubernetes scheduler places pods on nodes with sufficient capacity. Limits prevent a single container from consuming excessive resources and degrading co-located workloads on the same worker node.

### Implement graceful shutdown handling
{: #resiliency-graceful-shutdown}

When a pod is terminated, Kubernetes sends a `SIGTERM` signal before sending `SIGKILL`. Design your application to catch `SIGTERM`, stop accepting new connections, complete in-flight transactions, and exit cleanly. Set an appropriate `terminationGracePeriodSeconds` in your pod specification to give your application sufficient time to drain traffic.

### Avoid relying on long-lived connections to the API server
{: #resiliency-api-connections}

Kubernetes watch requests and streaming connections (such as `oc exec`, port-forwards, or custom API client watches) connect directly to a specific control plane replica. When that replica cycles during a patch upgrade, the connection closes. Workloads and tooling must implement automatic reconnection logic with exponential back-off.

### Use retry logic and circuit breakers
{: #resiliency-retry-logic}

When your application interacts with the Kubernetes API, external databases, or downstream microservices, implement retry logic with exponential back-off and jitter. Use circuit breaker patterns to prevent cascading failures when an upstream or downstream dependency is temporarily unavailable.

## Next steps
{: #resiliency-next-steps}

- Review [Planning app deployments](/docs/openshift?topic=openshift-plan_deploy) to learn more about workload types and Kubernetes objects.
- Learn about [Deploying apps to clusters](/docs/openshift?topic=openshift-app) with complete configuration examples.
- Read [High availability and disaster recovery](/docs/openshift?topic=openshift-ha-dr) for cluster-level availability strategies.

## Related links
{: #resiliency-related-links}

- [Pod Topology Spread Constraints](https://kubernetes.io/docs/concepts/scheduling-eviction/topology-spread-constraints/){: external}
- [Assigning Pods to Nodes](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/){: external}
- [Pod Disruption Budgets](https://kubernetes.io/docs/concepts/workloads/pods/disruptions/#pod-disruption-budgets){: external}
- [Configure Liveness, Readiness and Startup Probes](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/){: external}
- [Container Lifecycle Hooks](https://kubernetes.io/docs/concepts/containers/container-lifecycle-hooks/){: external}
