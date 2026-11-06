---

copyright:
  years: 2014, 2026
lastupdated: "2026-11-06"

keywords: openshift, reservations, worker node, unsupported, end of support

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}

# Reservations for classic worker node costs
{: #reservations}

[Classic infrastructure]{: tag-classic-inf}

Review information about existing reservations for classic infrastructure worker nodes on {{site.data.keyword.openshiftlong}}, including how to migrate your workloads and review reservation usage.
{: shortdesc}

Reservations for classic infrastructure worker nodes are no longer supported. You can't create new reservations or request access to reservations. Existing reservations and their contracts continue to work, and you can still view them, until each contract expires.
{: important}

## Migrating workloads from reservations
{: #reservations-deprecation-migrate}


Before you begin
:   To prevent loss of service, you must create non-reserved worker pools and migrate your workloads before each reservation contract expires. If a contract expires while you have more worker nodes in use than the remaining reservation capacity, worker nodes that exceed the capacity are deleted automatically.

1. Find your active reservation contracts and note the expiration date of each one. The expiration date is your deadline for migrating any workloads that use that contract's worker nodes.
   1. Log in to the [{{site.data.keyword.openshiftlong_notm}} reservations console](https://cloud.ibm.com/kubernetes/reservations){: external}.
   2. Click each reservation to view the contracts and their expiration dates in the **Contracts** section.

2. Create a new worker pool that does not use a reservation. For more information, see the documentation for your service.
   - [Adding worker nodes to classic clusters in {{site.data.keyword.containerlong_notm}}](/docs/containers?topic=containers-add-workers-classic#add_pool)
   - [Adding worker nodes to classic clusters in {{site.data.keyword.openshiftlong_notm}}](/docs/openshift?topic=openshift-add-workers-classic#add_pool)

3. Migrate your workloads from the reserved worker pool to the new worker pool. Use labels or node selectors to reschedule your existing workloads to the new worker pool.

4. Delete the worker pools that use reservations after workload migration is complete.

## Reviewing reservation usage
{: #ri-review}

You can review your {{site.data.keyword.openshiftlong_notm}} reservation usage and billing details.

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
- [Plan your cluster for high availability](/docs/openshift?topic=openshift-iks-ha-dr)
