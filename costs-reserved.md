---

copyright:
  years: 2014, 2026
lastupdated: "2026-07-20"

keywords: openshift, reservations, worker node, deprecated, end of support

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}

# Reservations for classic worker node costs
{: #reservations}

[Classic infrastructure]{: tag-classic-inf}

Review information about reservations for classic infrastructure worker nodes on {{site.data.keyword.openshiftlong}}, including the deprecation timeline and steps to migrate your workloads.
{: shortdesc}

Reservations for classic infrastructure worker nodes are deprecated. No new reservation contracts can be created after 15 October 2026. Existing reservations and contracts continue to be supported until their contract expiration dates.
{: deprecated}

## Deprecation timeline
{: #reservations-deprecation-timeline}

| Stage | Date | Description |
| --- | --- | --- |
| Deprecation announcement | July 2025 | Reservations on {{site.data.keyword.openshiftlong}} are deprecated. No new reservations can be created. |
| End of new contracts | 15 October 2026 | No new reservation contracts can be created. Existing contracts continue until their individual expiration dates. |
{: caption="Reservations deprecation timeline" caption-side="bottom"}

## Migrating workloads from reservations
{: #reservations-deprecation-migrate}

To prevent loss of service, you must create non-reserved worker pools and migrate your workloads before each reservation contract expires. If a contract expires while you have more worker nodes in use than the remaining reservation capacity, worker nodes that exceed the capacity are deleted automatically.
{: important}

1. Find your active reservation contracts and note the expiration date of each one. The expiration date is your deadline for migrating any workloads that use that contract's worker nodes.
   1. Log in to the [{{site.data.keyword.openshiftlong_notm}} reservations console](https://cloud.ibm.com/kubernetes/reservations){: external}.
   2. Click each reservation to view the contracts and their expiration dates in the **Contracts** section.

2. Create a new worker pool that does not use a reservation. For more information, see the documentation for your service.
   - [Adding worker nodes to classic clusters in {{site.data.keyword.containerlong_notm}}](/docs/containers?topic=containers-add-workers-classic#add_pool)
   - [Adding worker nodes to classic clusters in {{site.data.keyword.openshiftlong_notm}}](/docs/openshift?topic=openshift-add-workers-classic#add_pool)

3. Migrate your workloads from the reserved worker pool to the new worker pool. Use labels or node selectors to reschedule your existing workloads to the new worker pool. [VERIFY: Confirm whether additional migration steps are recommended for this specific context.]

4. Delete the worker pools that use reservations after workload migration is complete.

## About reservations
{: #ri-about}

A reservation is a {{site.data.keyword.cloud_notm}} resource that describes the flavor, location, and other details of worker nodes that you purchased. Contracts associated with a reservation are agreements to pay a fixed monthly amount for a set number of worker nodes for a 1 or 3 year term.

Reservations are available only for classic infrastructure worker nodes in multizone regions (MZRs). Worker pools that use reservations cannot use the cluster autoscaler add-on.
{: note}

When a contract expires, your reservation is checked against remaining capacity from other active contracts. If you have more worker nodes in use than the remaining capacity, worker nodes that exceed the total capacity are deleted. To avoid unexpected deletions, scale down your worker pools before a contract ends to match the remaining reservation capacity.
{: important}

You cannot modify the terms of a contract, such as the duration, number of worker nodes, or flavor. You can remove unneeded worker nodes from your clusters, but you cannot get a refund for unused capacity.

## Reviewing reservation usage
{: #ri-review}

You can review your {{site.data.keyword.openshiftlong_notm}} reservation usage and billing details.
{: shortdesc}

Before you begin, make sure that you have the following roles in {{site.data.keyword.cloud_notm}} IAM.
* **Viewer** platform access role for **Kubernetes Service** to view reservation usage details.
* **Viewer** platform access role for **Account Management > Billing** service to view billing details.

**Reservation usage**:
1. Log in to the [{{site.data.keyword.openshiftlong_notm}} reservations console](https://cloud.ibm.com/kubernetes/reservations){: external}.
2. Review the **Usage** column to see how many worker nodes of the total amount are in use, such as `1 of 3 worker nodes`.
3. Review the **Clusters** column to see how many clusters have worker nodes that use the reservation.

**Billing details**:
1. Log in to the [{{site.data.keyword.cloud_notm}} billing console](https://cloud.ibm.com/billing){: external}.
2. From the navigation menu, click **Usage**.
3. From the **Services** table, find the **Kubernetes Service** row and click **View plans**.
4. From the plans table, find the row for your reservation name and click **View details**.
5. Review the details for the reserved worker nodes that are associated with the contracts of your reservation.

## Next steps
{: #reservations-next}

- [Add worker nodes to classic clusters in {{site.data.keyword.containerlong_notm}}](/docs/containers?topic=containers-add-workers-classic)
- [Add worker nodes to classic clusters in {{site.data.keyword.openshiftlong_notm}}](/docs/openshift?topic=openshift-add-workers-classic)
- [Plan your cluster for high availability](/docs/openshift?topic=openshift-ha_clusters)
