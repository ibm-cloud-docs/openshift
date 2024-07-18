---

copyright:
  years: 2024, 2024
lastupdated: "2024-07-18"


keywords: openshift, version, update, upgrade, 4.16, update openshift

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}


# 4.16 version information and update actions
{: #cs_versions_416}

Review information about version 4.16 of {{site.data.keyword.openshiftlong_notm}}. This version is based on Kubernetes version {{site.data.keyword.openshift_416_kube_version}}. 
{: shortdesc}

Looking for general information about updating clusters, or information on a different version? See [Red Hat {{site.data.keyword.redhat_openshift_notm}} on IBM Cloud version information](/docs/openshift?topic=openshift-openshift_versions) and the version [4.16 release notes](https://docs.openshift.com/container-platform/4.16/release_notes/ocp-4-16-release-notes.html#ocp-4-16-release-notes){: external}.
{: tip}

![This badge indicates Kubernetes version 1.28 certification for {{site.data.keyword.openshiftlong_notm}}](images/certified-kubernetes-color.svg){: caption="Figure 1. Kubernetes version 1.28 certification badge" caption-side="bottom"}

{{site.data.keyword.openshiftlong_notm}} is a Certified Kubernetes product for version 1.28 under the CNCF Kubernetes Software Conformance Certification program. _Kubernetes® is a registered trademark of The Linux Foundation in the United States and other countries, and is used pursuant to a license from The Linux Foundation._


## Release timeline 
{: #release_timeline_416}

The following table includes the expected release timeline for version 4.16. You can use this information for planning purposes, such as to estimate the general time that the version might become unsupported. 
{: shortdesc}

Dates that are marked with a dagger (`†`) are tentative and subject to change.
{: important}

| Supported? | {{site.data.keyword.redhat_openshift_notm}} / Kubernetes version | Release date | Unsupported date |
| --- | --- | --- | --- |
| Supported | 4.16 / {{site.data.keyword.openshift_416_kube_version}} | {{site.data.keyword.openshift_416_release_date}} | {{site.data.keyword.openshift_416_unsupported_date}}`†` |
{: caption="Release history for {{site.data.keyword.openshiftlong_notm}} version 4.16." caption-side="bottom"}

## Preparing to update
{: #prep-up-416}

Review changes that you might need to make when you [update a cluster](/docs/openshift?topic=openshift-update) to version 4.16. This information summarizes updates that are likely to have an impact on deployed apps when you update.
{: shortdesc}

The backup and restore Helm chart is supported on <containers>{{site.data.keyword.containerlong_notm}}</containers><openshift>{{site.data.keyword.openshiftlong_notm}}</openshift> 4.16 clusters. However, only the COS direct endpoints are supported. For example: `s3.direct.us.cloud-object-storage.appdomain.cloud`.
{: note}

<containers>{{site.data.keyword.containerlong_notm}}</containers><openshift>{{site.data.keyword.openshiftlong_notm}}</openshift> version 4.16 clusters do not yet support [Rotating CA certificates in your cluster](/docs/openshift?topic=openshift-cert-rotate). Do not update your cluster to version 4.16 if this support is required.
{: note}


### Update before master
{: #416_before}

The following table shows the actions that you must take before you [update the cluster master](/docs/openshift?topic=openshift-update#master).
{: shortdesc}

| Type | Description |
| --- | --- |
{: caption="Changes to make before you update the master to Red Hat OpenShift 4.16" caption-side="bottom"}

## Checking the `Upgradeable` status of your cluster
{: #status-check-416}

Run the following command to check the `Upgradeable` status of your cluster.

```sh
oc get clusterversion version -o json | jq '.status.conditions[] | select(.type == "Upgradeable")'
```
{: pre}

Example output where the `Upgradeable` status is `False`.

```sh
{
  "lastTransitionTime": "2023-10-04T15:55:54Z",
  "message": "Kubernetes 1.27 and therefore OpenShift 4.16 remove several APIs which require admin consideration. Please see the knowledge article https://access.redhat.com/articles/6958395 for details and instructions.",
  "reason": "AdminAckRequired",
  "status": "False",
  "type": "Upgradeable"
}
```
{: screen}

If the `Upgradeable` status is `False`, the condition information provides instructions that must be followed before upgrading. For more information, see [Providing the administrator acknowledgment](https://docs.openshift.com/container-platform/4.16/updating/preparing_for_updates/updating-cluster-prepare.html#update-preparing-ack_updating-cluster-prepare){: external}.
