---

copyright:
  years: 2025, 2025
lastupdated: "2025-06-13"


keywords: logging, monitoring, duplicate lobs, observability

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}



# Why am I seeing duplicate metrics or logs being sent from my clusters?
{: #ts-dupe-logs}
{: troubleshoot}
{: support}


You are seeing duplicate log entries for your clusters.
{: tsSymptoms}


The most common cause for this issue is that you have multiple logging agents installed in your cluster.
{: tsCauses}


Remove the unsupported observability plug-in resources from your cluster.
{: tsResolve}


1. Check for the unsupported agents.
    ```sh
    oc get daemonsets -n ibm-observe
    ```
    {: pre}

1. If there is a `logdna-agent` or a `sysdig-agent`, remove them.

    Example output that shows the resources which need to be removed.
    ```sh
    NAME           DESIRED   CURRENT   READY   UP-TO-DATE   AVAILABLE   NODE SELECTOR   AGE
    logdna-agent   9         9         9       9            9           <none>          4d
    sysdig-agent   9         9         9       9            9           <none>          4d
    ```
    {: screen}


1. Delete the resources.
    ```sh
    oc delete daemonset logdna-agent -n ibm-observe
    oc kubectl delete daemonset sysdig-agent -n ibm-observe
    ```
    {: pre}



1. Verify the daemonset and its pods were deleted.
    ```sh
    oc get daemonset logdna-agent -n ibm-observe
    oc get pods -l app=logdna-agent -n ibm-observe
    oc get daemonset sysdig-agent -n ibm-observe
    oc get pods -l app=sysdig-agent -n ibm-observe
    ```
    {: pre}

