---

copyright: 
  years: 2014, 2025
lastupdated: "2025-01-09"


keywords: kubernetes, openshift

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}





# Reviewing master health
{: #debug_master}
{: troubleshoot}
{: support}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf}

Review your cluster master health.
{: shortdesc}


## Reviewing master health, status, and states
{: #review-master-health}

[Cluster and master states](/docs/openshift?topic=openshift-cluster-states-reference&interface=ui)

## Understanding the impact of a master outage
{: #review-master-outage}

The [{{site.data.keyword.redhat_openshift_notm}} master](/docs/openshift?topic=openshift-service-architecture) is the main component that keeps your cluster up and running. The master stores cluster resources and their configurations in the etcd database that serves as the single point of truth for your cluster. The {{site.data.keyword.redhat_openshift_notm}} API server is the main entry point for all cluster management requests from the worker nodes to the master, or when you want to interact with your cluster resources.

If a master failure occurs, your workloads continue to run on the worker nodes, but you can't use `oc` commands to work with your cluster resources or view the cluster health until the {{site.data.keyword.redhat_openshift_notm}} API server in the master is back up. If a pod goes down during the master outage, the pod can't be rescheduled until the worker node can reach the {{site.data.keyword.redhat_openshift_notm}} API server again.

During a master outage, you can still run `ibmcloud oc` commands against the {{site.data.keyword.containerlong_notm}} API to work with your infrastructure resources, such as worker nodes or VLANs. If you change the current cluster configuration by adding or removing worker nodes to the cluster, your changes don't happen until the master is back up.

Do not restart or reboot a worker node during a master outage. This action removes the pods from your worker node. Because the Kubernetes API server is unavailable, the pods can't be rescheduled onto other worker nodes in the cluster.
{: important}
