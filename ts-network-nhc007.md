---
copyright: 
  years: 2025, 2025
lastupdated: "2025-09-17"

keywords: nhc007, dns traffic blocked

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why does the Network status show an `NHC007` error?
{: #ts-network-nhc007}
{: troubleshoot}
{: support}

[Virtual Private Cloud]{: tag-vpc}

When you check the status of your cluster's health by running the `ibmcloud oc cluster health issues --cluster <CLUSTER_ID>`, you see an error similar to the following example.
{: tsSymptoms}

```sh
ID       Component   Severity   Description
NHC007   Network     Warning    One or more DNS resolvers are not reachable from certain worker nodes.
```
{: screen}

If you check the details of the issue, you will see which **DNS resolvers** cannot be accessed from which **worker node**.

```sh
ibmcloud ks cluster health issue get --cluster <CLUSTER_ID> --issue NHC007
```
{: pre}

This warning indicates that DNS traffic from certain worker nodes is being blocked, possibly due to restrictive policies or IaaS-level configurations.
{: tsCauses}

Check your Calico HostEndpoint (HEP) and GlobalNetworkPolicy (GNP) resources, as well as your ACLs, security groups, and any other network appliances that may block outbound DNS traffic.
{: tsResolve}

1. Review Calico HostEndpoint (HEP) resources to list Calico HEPs and check if any HEP configurations might incorrectly apply restrictions to your worker node interfaces.

    ```sh
    kubectl get hostendpoints.crd.projectcalico.org
    ```
    {: pre}

    Example command to to describe a specific HEP.

    ```sh
    kubectl describe hostendpoints.crd.projectcalico.org <hep-name>
    ```
    {: pre}

1. Review Calico GlobalNetworkPolicies (GNP) to list GNPs.

    ```sh
    kubectl get globalnetworkpolicies.crd.projectcalico.org
    ```
    {: pre}

1. Inspect specific policies for restrictive DNS rules. Focus on `egress` rules that affect port 53 or apply to node labels/selectors.

    ```sh
    kubectl get globalnetworkpolicies.crd.projectcalico.org <policy-name> -o yaml
    ```
    {: pre}

1. Test DNS access from a debug pod, run a temporary debug pod, where use the affected worker nodes name for `nodeName`. If DNS fails here, it may be due to infrastructure-level blocks.

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

1. Run the following commands inside the debug pod.

    ```sh
    nslookup ibm.com
    ```
    {: pre}

    ```sh
    dig ibm.com
    ```
    {: pre}


1. Check ACLs (Access Control Lists).
    * In the console, navigate to **VPC > Access control lists** and ensure **outbound rules** allow both UDP port 53 and TCP port 53.

    * In the CLI inspect ACLs by running the following commands.

        ```sh
        ibmcloud is network-acls
        ```
        {: pre}

        ```sh
        ibmcloud is network-acl <acl-id>
        ```
        {: pre}

1. Inspect security group rules to find the security groups associated with your worker nodes and then run to check security group settings. Ensure there are no outbound rules blocking DNS traffic (UDP/TCP port 53).

    ```sh
    ibmcloud is security-group-rules <security-group-id>
    ```
    {: pre}



1. Review your infrastructure (network appliances, ACLs, etc.) and allow **UDP and TCP port 53** outbound traffic

1. If DNS is still unreachable after reviewing these items, contact support. Open a [support case](/docs/account?topic=account-using-avatar). In the case details, be sure to include any relevant log files, error messages, or command outputs.
