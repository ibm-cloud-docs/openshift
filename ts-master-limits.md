---

copyright: 
  years: 2014, 2025
lastupdated: "2025-10-06"


keywords: openshift, roks, rhoks, rhos, limits

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}





# Why does my cluster master status say it is approaching its resource limit?
{: #master_resource_limit}
{: support}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf}


You see a master status similar to the following example.
{: tsSymptoms}

```sh
The master is approaching its allotted memory resource limit (93%).  Please consider reducing load on your master.  Exceeding the defined resource limit could cause reduced performance for your cluster's master control plane.
```
{: screen}

Our managed customer masters have a resource cap that limits the amount of memory and CPU that they can consume.
{: tsCauses}

If your master status shows the previous message, then your master is consuming enough resources to approach its given limit.  At this point, this message is a warning. Your master control plane is still healthy and functioning as normal.  However, if you don't act, your master can reach the limits, potentially causing performance and functional issues.

You have a few options when it comes to dealing with this.
{: tsResolve}


- Identify the cause of the high resource usage and make changes to reduce the usage.
    - Look for applications that might be generating high load against your master. You can use the [Kubernetes API server audit logs](/docs/openshift?topic=openshift-health-audit) to identify applications causing high resource load.
    - Reduce the number of resources, such as secrets, configmaps, and replicasets.  If a cluster contains a high number of resources, then the queries can cause the master to be overloaded. Use the **`kubectl get raw`** command to find the top resources by count. For example, run 
        ```sh
        kubectl get --raw /metrics | grep ^apiserver_storage_objects | sort -n -k2
        ```
        {: pre}

- For each resource listed, we recommend avoiding a count above 250 per node. For example, a standard 3-node cluster should not exceed 750 per resource.

- Request a higher resource limit for your master.  To request a higher limit, [open a support ticket](/docs/openshift?topic=openshift-get-help) with justification.  Requests are reviewed and granted on a cluster by cluster basis. 

- Do nothing and risk future performance and functional issues in your master control plane.
