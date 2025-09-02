---
copyright: 
  years: 2025, 2025
lastupdated: "2025-09-02"

keywords: , nhc007, dns traffic blocked

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

1. Check Calico HostEndpoint (HEP) resources
To list Calico HEPs:
  ```sh
  kubectl get hostendpoints.crd.projectcalico.org
  ```
  {: pre}

To describe a specific HEP:
  ```sh
  kubectl describe hostendpoints.crd.projectcalico.org <hep-name>
  ```
  {: pre}

Check if any HEP configurations might incorrectly apply restrictions to your worker node interfaces.

2. Review Calico GlobalNetworkPolicies (GNP)
To list GNPs:
  ```sh
  kubectl get globalnetworkpolicies.crd.projectcalico.org
  ```
  {: pre}

Inspect specific policies for restrictive DNS rules:
  ```sh
  kubectl get globalnetworkpolicies.crd.projectcalico.org <policy-name> -o yaml
  ```
  {: pre}

Focus on `egress` rules that affect port 53 or apply to node labels/selectors.

3. Test DNS access from a debug pod
Run a temporary debug pod, where use the affected worker nodes name for `nodeName`:
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

Inside the pod:
  ```sh
  nslookup ibm.com
  ```
  {: pre}

Or:

  ```sh
  dig ibm.com
  ```
  {: pre}

If DNS fails here, it may be due to infrastructure-level blocks.

5. Check ACLs (Access Control Lists)
In the IBM Cloud console:
- Navigate to **VPC > Access control lists**
- Ensure **outbound rules** allow:
  - UDP port 53
  - TCP port 53

Or use CLI to inspect ACLs:
```sh
ibmcloud is network-acls
ibmcloud is network-acl <acl-id>
```

6. Inspect security group rules
Find the security groups associated with your worker nodes and then run to check security group settings:
  ```sh
  ibmcloud is security-group-rules <security-group-id>
  ```

Ensure there are no outbound rules blocking DNS traffic (UDP/TCP port 53).

7. If DNS is still unreachable after reviewing these items, contact support. Open a [support case](/docs/account?topic=account-using-avatar). In the case details, be sure to include any relevant log files, error messages, or command outputs.
