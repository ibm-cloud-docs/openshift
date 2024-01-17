---

copyright: 
  years: 2023, 2024
lastupdated: "2024-01-17"


keywords: openshift, kubernetes, help, cluster, upgrades,

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}



# Why do I see a `Cannot complete cluster master upgrade` message?
{: #ts-cluster-master-upgrade}
{: troubleshoot}
{: support}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [{{site.data.keyword.satelliteshort}}]{: tag-satellite}


When upgrading a cluster master, you receive a `Cannot complete cluster master upgrade` error message similar to the following example.
{: tsSymptoms}


```sh
Cannot complete cluster master upgrade because the Upgradeable status condition is set to False.
```
{: screen}

There are a variety of reasons why the Cluster Version Operator would report back an `Upgradeable` status of `False`.  For example, if you are upgrading from {{site.data.keyword.redhat_openshift_notm}} 4.13 to 4.14, and receive this error message, then your cluster administrators likely have not yet acknowledged that they have evaluated and removed the deprecated APIs in Kubernetes version 1.27. For more information, see [Preparing to update to OpenShift Container Platform 4.14](https://docs.openshift.com/container-platform/4.14/updating/preparing_for_updates/updating-cluster-prepare.html#update-preparing-ack_updating-cluster-prepare){: external}.
{: tsCauses}

Run the following command to check the reason(s) that your cluster isn't in an upgradeable state.
{: tsResolve}

```sh
oc get clusterversion version -o json | jq '.status.conditions[] | select(.type == "Upgradeable")'
```
{: pre}

1. Review the [Version information and update actions](/docs/openshift?topic=openshift-openshift_versions) for the version you want to update to. Evaluate your cluster for APIs that have been removed in the new version. For example in {{site.data.keyword.redhat_openshift_notm}} 4.14 and Kubernetes 1.27 the `storage.k8s.io/v1beta1` API is removed. 

1. Review the `reason` and `message` fields from the JSON object for the `False` upgradeable status. If you are attempting an upgrade from {{site.data.keyword.redhat_openshift_notm}} 4.13 to {{site.data.keyword.redhat_openshift_notm}} 4.14 and there has not been an administrator acknowledgment, the message includes `* Kubernetes 1.27 and therefore OpenShift 4.14 remove several APIs which require admin consideration. Please see https://access.redhat.com/articles/6958395 for details and instructions.`. If you don't have access to a Red Hat account to view the solution, you can perform the following steps to resolve the issue as a cluster administrator.

1. Migrate any affected components to use the appropriate new API version including tools, workloads, or any other components that run or interact with the cluster. For example, {{site.data.keyword.redhat_openshift_notm}} 4.14 clusters use Kubernetes 1.27 and face the same [deprecations](https://kubernetes.io/docs/reference/using-api/deprecation-guide/#v1-27){: external}.


1. After you've successfully migrated off of removed APIs like `storage.k8s.io/v1beta1`, you can acknowledge that your cluster is ready to upgrade to the next version of {{site.data.keyword.redhat_openshift_notm}}.

    Cluster administrators are responsible for ensuring that removed APIs are no longer being used and migration to supported APIs is completed before providing this administrator acknowledgment. IBM Cloud can assist with the evaluation, but cannot identify all possible instances where removed APIs are being used, especially in external tools and idle workloads.
    {: important}

1. Follow the steps to [Provide the administrator acknowledgment](https://docs.openshift.com/container-platform/4.14/updating/preparing_for_updates/updating-cluster-prepare.html#update-preparing-ack_updating-cluster-prepare){: external} that you have migrated off the removed APIs.

1. After you have completed the previous migration steps, run the following command again. Note, it may take several minutes for the `Upgradeable` status to update. If no data is returned, the `Upgradeable` status has been removed and you can retry the cluster upgrade.
    ```sh
    oc get clusterversion version -o json | jq '.status.conditions[] | select(.type == "Upgradeable")'
    ```
    {: pre}
  






