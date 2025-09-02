---
copyright: 
  years: 2025, 2025
lastupdated: "2025-09-02"

keywords: , nhc006, dns resolvers unreachable

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why does the Network status show an `NHC006` error?
{: #ts-network-nhc006}
{: troubleshoot}
{: support}

[Classic infrastructure]{: tag-classic-inf}

When you check the status of your cluster's health by running the `ibmcloud oc cluster health issues --cluster <CLUSTER_ID>`, you see an error similar to the following example.
{: tsSymptoms}

```sh
ID       Component   Severity   Description
NHC006   Network     Warning    One or more DNS resolvers are not reachable from certain worker nodes.
```
{: screen}

If you check the details of the issue, you will see which **DNS resolvers** cannot be accessed from which **worker node**.

```sh
ibmcloud ks cluster health issue get --cluster <CLUSTER_ID> --issue NHC006
```
{: pre}

This warning indicates that some worker nodes are unable to reach one or more DNS resolvers. This can lead to DNS failures and impact workload communication.
{: tsCauses}

1. Inspect Calico GlobalNetworkPolicies (GNP) by listing all GNPs.
    ```sh
    kubectl get globalnetworkpolicies.crd.projectcalico.org
    ```
    {: pre}

    Run the following command to review a specific policy.
    ```sh
    kubectl get globalnetworkpolicies.crd.projectcalico.org <policy-name> -o yaml
    ```
    {: pre}

1. Look for any `egress` rules that block DNS traffic (UDP/TCP port 53). Also check for `selector` fields that might improperly include worker nodes.

1. Validate DNS reachability from worker nodes using a debug pod
    ```sh
    kubectl run  -i --tty debug \
      --image=us.icr.io/armada-master/network-alpine:latest \
      --restart=Never \
      --overrides='
    {
      "apiVersion": "v1",
      "spec": {
        "nodeName": "<node-name>"
      }
    }' -- sh 
    ```
    {: pre}

1. Run the following commands inside the debug pod. If these fail, DNS might be blocked by policies or IaaS-level configurations.

    ```sh
    nslookup ibm.com
    ```
    {: pre}

    ```sh
    dig ibm.com
    ```
    {: pre}

1. Check IaaS-level firewalls and ACLs.
1. Ensure subnet ACLs allow **UDP and TCP port 53** outbound.
1. If the issue continues, contact support for further assistance. Open a [support case](/docs/account?topic=account-using-avatar). In the case details, be sure to include any relevant log files, error messages, or command outputs.
