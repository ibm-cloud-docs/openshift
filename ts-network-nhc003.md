---
copyright: 
  years: 2025, 2025
lastupdated: "2025-09-17"

keywords: nhc003, container registry unreachable

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why does the Network status show an `NHC003` error?
{: #ts-network-nhc003}
{: troubleshoot}
{: support}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf}

When you check the status of your cluster's health by running the `ibmcloud oc cluster health issues --cluster <CLUSTER_ID>`, you see an error similar to the following example.
{: tsSymptoms}

```sh
ID       Component   Severity   Description
NHC003   Network     Warning    Some worker nodes in the cluster can not reach container image registries to pull images.
```
{: screen}

If you check the details of the issue, you will see which registry cannot be accessed from which worker node.
```sh
ibmcloud ks cluster health issue get --cluster <CLUSTER_ID> --issue NHC003
```
{: pre}

This warning means that some of the worker nodes cannot access external container registries, such as Docker Hub, Quay, or IBM Cloud Container Registry, which prevents them from pulling images required by your workloads.
{: tsCauses}

Ensure the worker nodes have access to the internet and can reach external container registries. Also check network policies, security groups, and firewall settings.
{: tsResolve}

1. From a pod running on the affected node, check if the node can access the registry. Start a debug pod.
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

    Then inside the pod, try accessing a container registry.
    ```sh
    wget <registry_address>
    ```
    {: pre}

    Or use `curl` if available:
    ```sh
    curl -I <registry_address>
    ```
    {: pre}

2. Check if the worker nodes have outbound internet access by running a traceroute or ping from the debug pod.
    ```sh
    traceroute <registry_address>
    ```
    {: pre}

    ```sh
    ping <registry_address>
    ```
    {: pre}

3. Check if there are any restrictive network policies and global network policies in place.
    ```sh
    kubectl get networkpolicies --all-namespaces
    ```
    {: pre}

    ```sh
     kubectl get globalnetworkpolicies.crd.projectcalico.org
    ```
    {: pre}

    Look for policies that block egress traffic from worker nodes to the internet or to the specific registry domains.

4. Verify your cluster's security groups and make sure outbound traffic is allowed. For each worker node, check the security group. Make sure there are no rules blocking HTTPS (TCP port 443) or DNS (UDP port 53).

5. Review your infrastructure (network appliances, security groups, ACLs, etc.) and enable outbound access if necessary.

6. If you're using private container registries, verify DNS resolution and authentication is working.

7. After applying the fixes, wait a few minutes and recheck the cluster health.

8. If the issue persists, contact support for further assistance. Open a [support case](/docs/account?topic=account-using-avatar). In the case details, be sure to include any relevant log files, error messages, or command outputs.
