---
copyright: 
  years: 2025, 2025
lastupdated: "2025-12-03"

keywords: nhc005, calico degraded, tigera operator

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why does the Network status show an `NHC005` error?
{: #ts-network-nhc005}
{: troubleshoot}
{: support}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf}

When you check the status of your cluster's health by running the `ibmcloud oc cluster health issues --cluster <CLUSTER_ID>`, you see an error similar to the following example.
{: tsSymptoms}

```sh
ID       Component   Severity   Description
NHC005   Network     Warning    Tigera operator is reporting that Calico is in 'degraded' state.
```
{: screen}

This warning indicates that the Tigera operator, which manages Calico in IBM Cloud Kubernetes Service, has detected that Calico is in a degraded state. This could impact network policies, pod networking, or other network-related features.
{: tsCauses}

Check the logs of the Tigera operator and Calico components to investigate the cause of the degradation.
{: tsResolve}

1. Check Tigera status custom resources and conditions and look for `"conditions"` with `"Progressing": true`.
    ```sh
    kubectl get tigerastatus -o yaml
    ```
    {: pre}

    ```sh
    kubectl get tigerastatus calico -o yaml
    ```
    {: pre}

2. Check Calico and Calico-typha components status by listing the Calico pods in `calico-system` namespace:
    ```sh
    kubectl get pods -n calico-system
    ```
    {: pre}

3. Check the rollout status of deployments and daemonset.
    ```sh
    kubectl rollout status deployment/calico-kube-controllers -n calico-system
    kubectl rollout status deployment/calico-typha -n calico-system
    kubectl rollout status daemonset/calico-node -n calico-system
    ```
    {: pre}

4. If pods are not ready or stuck in `Init` or `CrashLoopBackOff`, get the pod logs.
    ```sh
    kubectl logs <pod-name> -n calico-system
    ```
    {: pre}

5. Look for any configuration errors, networking issues, or crash loops in logs.

6. After resolving any identified issues, wait a few minutes and recheck the network health.

7. For more information, see [Controlling traffic with network policies](/docs/openshift?topic=openshift-network_policies){: external} and [Debugging Calico components](/docs/openshift?topic=openshift-calico_log_level){: external}

8. If the issue persists, contact support for further assistance. Open a [support case](/docs/account?topic=account-using-avatar). In the case details, be sure to include any relevant log files, error messages, or command outputs.
