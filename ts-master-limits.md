---

copyright: 
  years: 2014, 2022
lastupdated: "2022-02-09"

keywords: openshift, roks, rhoks, rhos, limits

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}


# Why does my cluster master status say it is approaching its resource limit?
{: #master_resource_limit}
{: support}

**Infrastructure provider**:
* ![Classic infrastructure provider icon.](images/icon-classic-2.svg) Classic
* ![VPC infrastructure provider icon.](images/icon-vpc-2.svg) VPC


You see a master status similar to the following example.
{: tsSymptoms}

```sh
The master is approaching its allotted memory resource limit (93%).  Please consider reducing load on your master.  Exceeding the defined resource limit could cause reduced performance for your cluster's master control plane.
```
{: screen}

Our managed customer masters have a resource cap that limits the amount of memory and CPU that they can consume.
{: tsCauses}

If your master status shows the previous message, then your master is consuming enough resources to approach its given limit.  At this point, this message is a warning. Your master control plane is still healthy and functioning as normal.  However, if you don't take action, your master can reach the limits, potentially causing performance and functional issues.

You have a few options when it comes to dealing with this.
{: tsResolve}


- Identify the cause of the high resource usage and make changes to lower the usage.
    - Look for applications that may be generating high load against your master. 
    - Reduce the number of resources, such as secrets, configmaps, and replicasets.  If a cluster contains a high number of resources, then the queries can cause the master to be overloaded. Use the **`kubectl get raw`** command to find the top resources by count. For example, run 
        ```
        kubectl get --raw /metrics | grep ^etcd_object_counts | sort -n -k2
        ```
        {: pre}

- Request a higher resource limit for your master.  To request a higher limit, [open a support ticket](/docs/openshift?topic=openshift-get-help#help-support) with justification.  Requests are reviewed and granted on a cluster by cluster basis. 

- Do nothing and risk future performance and functional issues in your master control plane.
