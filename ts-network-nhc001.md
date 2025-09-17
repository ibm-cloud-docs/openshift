---
copyright: 
  years: 2025, 2025
lastupdated: "2025-09-17"

keywords: nhc001, calico progressing, tigera operator

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why does the Network status show an `NHC001` error?
{: #ts-network-nhc001}
{: troubleshoot}
{: support}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf}

When you check the status of your cluster's health by running the `ibmcloud oc cluster health issues --cluster <CLUSTER_ID>`, you see an error similar to the following example.
{: tsSymptoms}

```sh
ID       Component   Severity   Description
NHC001   Network     Warning    Tigera operator has been reporting that Calico is in 'progressing' state for over an hour.
```
{: screen}

This warning means the Tigera operator has been reporting that Calico is stuck in a 'progressing' state, potentially due to component deployment delays or underlying issues.
{: tsCauses}

Investigate the logs of the Tigera operator and Calico components to understand what is preventing Calico from reaching a healthy state.
{: tsResolve}

1. Check Tigera status custom resources and conditions. Look for `"conditions"` with `"Progressing": true`.
    ```sh
    kubectl get tigerastatus -o yaml
    ```
    {: pre}

    ```sh
    kubectl get tigerastatus calico -o yaml
    ```
    {: pre}


2. Check Calico and Calico-typha components status by listing Calico pods in `calico-system`. namespace:
    ```sh
    kubectl get pods -n calico-system
    ```
    {: pre}

    Check the rollout status of deployments and daemonset.
    ```sh
    kubectl rollout status deployment/calico-kube-controllers -n calico-system
    kubectl rollout status deployment/calico-typha -n calico-system
    kubectl rollout status daemonset/calico-node -n calico-system
    ```
    {: pre}

3. If pods are not ready or stuck in `Init` or `CrashLoopBackOff`, get logs:
    ```sh
    kubectl logs <pod-name> -n calico-system
    ```
    {: pre}

4. Wait for components to complete rollout. After addressing any issues (e.g., CrashLoopBackOff, image pull errors), wait a few minutes for Tigera to refresh the state.

5. For more information, see [Controlling traffic with network policies](https://cloud.ibm.com/docs/containers?topic=containers-network_policies){: external} and [Debugging Calico components](https://cloud.ibm.com/docs/containers?topic=containers-calico_log_level){: external}

6. If the issue continues, contact support for assistance. Open a [support case](/docs/account?topic=account-using-avatar). In the case details, be sure to include any relevant log files, error messages, or command outputs.
