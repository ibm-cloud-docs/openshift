---

copyright: 
  years: 2014, 2025
lastupdated: "2025-12-02"


keywords: openshift, autoscaler

subcollection: openshift

content-type: troubleshoot

---


# Why can't I resize or rebalance my worker pool?
{: #ts-ca-resize}

When the cluster autoscaler is enabled for a worker pool, you can't [resize](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_pool_resize) or [rebalance](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_rebalance) your worker pools. 
{: tsSymptoms}

If you disable worker pools before you disable the `cluster-autoscaler` add-on, the worker pools can't be resized manually. 
{: tsCauses}

You must edit the ConfigMap to change the worker pool minimum or maximum sizes, or disable cluster autoscaling for that worker pool. See [Can I change how scale-up and scale-down work?](/docs/openshift?topic=openshift-cluster-scaling-classic-vpc#customize-scale-up-down).
{: tsResolve}

Don't use the `ibmcloud oc worker rm` [command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_rm) to remove individual worker nodes from your worker pool, which can unbalance the worker pool.

If you disabled the autoscaler, reinstall the cluster autoscaler, edit the ConfigMap to disable the worker pool, and try again.
