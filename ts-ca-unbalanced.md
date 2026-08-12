---

copyright: 
  years: 2014, 2026
lastupdated: "2026-08-12"


keywords: openshift, autoscaler

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why are my autoscaled worker pools unbalanced?
{: #ts-ca-unbalanced}

Learn why your worker pool becomes unbalanced across zones when you enable the cluster autoscaler.
{: shortdesc}


During a scale-up, the cluster autoscaler balances nodes across zones, with a permitted difference of plus or minus one worker node.
{: tsSymptoms}

Your pending workloads might not request enough capacity to make each zone balanced.
{: tsCauses}

To balance the worker pools manually, [update your cluster autoscaler ConfigMap](/docs/openshift?topic=openshift-cluster-scaling-install-addon-enable) to remove the unbalanced worker pool. Then, run the `ibmcloud oc worker-pool rebalance` [command](/docs/openshift?topic=openshift-kubernetes-service-cli#worker-pool-rebalance-cli), and add the worker pool back to the cluster autoscaler ConfigMap.
{: tsResolve}


For Satellite clusters, do not use the `ibmcloud oc worker-pool rebalance` command if you have manually assigned worker nodes to your worker pool. Rebalancing a pool with manually assigned worker nodes might remove more than the expected number of worker nodes.
{: important}
