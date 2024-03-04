---

copyright:
  years: 2022, 2024
lastupdated: "2024-03-04"


keywords: openshift, ingress, troubleshoot ingress, ingress operator, ingress cluster operator, ingress operator missing

subcollection: openshift
content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}




# Why does the Ingress status show an `ERRIONF` error?
{: #ts-ingress-errionf}
{: troubleshoot}
{: support}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [{{site.data.keyword.satelliteshort}}]{: tag-satellite}

You can use the `ibmcloud oc ingress status-report ignored-errors add` command to add an error to the ignored-errors list. Ignored errors still appear in the output of the `ibmcloud oc ingress status-report get` command, but are ignored when calculating the overall Ingress Status.
{: tip}

When you check the status of your cluster's Ingress components by running the `ibmcloud oc ingress status-report get` command, you see an error similar to the following.
{: tsSymptoms}

```sh
The Ingress Operator is missing from the cluster (ERRIONF).
```
{: screen}


The Ingress Operator is included in {{site.data.keyword.redhat_openshift_notm}} by default. An underlying cluster issue is causing the Operator to not deploy successfully.
{: tsCauses}



Verify that the `ingress` ClusterOperator resource exists in your cluster.
{: tsResolve}

1. Get the details of the `ingress` ClusterOperator.
    ```sh
    oc get clusteroperator ingress
    ```
    {: pre}
    
    Example output.
    
    ```sh
    NAME      VERSION   AVAILABLE   PROGRESSING   DEGRADED   SINCE   MESSAGE
    ingress   4.10.22   True        False         False      45d
    ```
    {: screen}
    
1. If the Operator exists and `Progressing` is `True`, wait 10 to 15 minutes to allow time for the Operator to finish deploying. If the operator doesn't exist, continue with the troubleshooting steps.
    
1. Follow the steps to review your cluster master and worker node states.
    - [Review master health](/docs/openshift?topic=openshift-debug_master#review-master-health).
    - [Review worker node states](/docs/openshift?topic=openshift-worker-node-state-reference).

1. Refresh your cluster masters.
    ```sh
    ibmcloud oc cluster master refresh
    ```
    {: pre}
    
    
1. After you refresh your cluster master, wait 10 to 15 minutes and then check the Ingress Operator status again by running the **`oc get clusteroperator ingress`** command. If the resource is still not created or is in a degraded state, contact support. Open a [support case](/docs/get-support?topic=get-support-using-avatar). In the case details, be sure to include any relevant log files, error messages, or command outputs.


