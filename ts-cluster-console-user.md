---

copyright:
  years: 2014, 2025
lastupdated: "2025-03-18"


keywords: openshift, console, user, error

subcollection: openshift
content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}




# Why do I see a `Could not find user` error when I try to access the web console?
{: #ts-cluster-ocp-console}

When you try to access the {{site.data.keyword.openshiftshort}} web console, you see an error message similar to the following.

```sh
Could not find user.
```
{: screen}

This error occurs when you try to access the {{site.data.keyword.openshiftshort}} web console directly, such as through a URL, rather than through the {{site.data.keyword.cloud_notm}} UI or without running the `ibmcloud oc cluster config` command. This prevents the IAM user role from synchronizing to the cluster. 
{: tsCauses}

Synchronize the IAM user information to the {{site.data.keyword.openshiftshort}} cluster. 
{: tsResolve}

Before you begin: 

[Access your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-access_cluster).

To synchronize the IAM information for the user, you have 2 options:
- Log in to your cluster from the [console](https://cloud.ibm.com/containers/cluster-management/clusters){: external}.
- Set your command line context for the cluster by running the  `ibmcloud oc cluster config --cluster CLUSTER` command.

If you use an API key for a functional ID or another user, make sure to log in as the correct user.
{: note}

After the impacted user completes the IAM synchronization, the cluster administrator can verify the user exists in the cluster by listing users with the `oc get users` command.
{: tip}
