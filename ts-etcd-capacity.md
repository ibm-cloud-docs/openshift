---

copyright:
  years: 2024, 2024
lastupdated: "2024-05-07"


keywords: openshift, {{site.data.keyword.openshiftlong_notm}}, etcd, capacity, database, limits
subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}




# Why do I see an `etcd database size is approaching the maximum` error?
{: #ts-etcd-capacity}
{: support}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [{{site.data.keyword.satelliteshort}}]{: tag-satellite}

You see an error message similar to the following.
{: tsSymptoms}

```sh
etcd database size is approaching the maximum
```
{: pre}

{{site.data.keyword.openshiftlong_notm}} uses an `etcd` database as its backing store for all cluster data. This database is where resources like configmaps, secrets, deployments, and all other Kubernetes resources are stored. {{site.data.keyword.openshiftlong_notm}} limits the size of the backing etcd database to a maximum of 4 GiB, which provides sufficient capacity under normal operating conditions. However, if a user or process creates an extremely large number of objects, the in-use database size can reach the maximum.
{: tsCauses}

Identify the resources which are occupying space in the etcd database.
{: tsResolve}


1. Inspect the metrics from the apiserver by running the following command.
    ```sh
    kubectl get --raw /metrics
    ```
    {: pre}
    
1. Search the output for `apiserver_storage_objects metrics`, which tells you how many of each kind of object is present in the etcd database. Look for resource types that have tens or hundreds of thousands of associated objects. These resources are the most likely cause of the issue. However, keep in mind that it is the size of these objects rather than their number that is important.

1. For the resources that you identified in the previous step, review and adjust their settings to reduce the number of objects that are getting created. For example, a common issue is misconfigured operators that automatically create too many secrets.

1. After adjust the resource settings, clean up the resources to bring the size of the etcd database back down.

1. If the issue persists, contact support. Open a [support case](/docs/get-support?topic=get-support-using-avatar). In the case details, be sure to include any relevant log files, error messages, or command outputs.

