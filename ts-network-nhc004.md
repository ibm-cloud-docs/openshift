---
copyright: 
  years: 2025, 2025
lastupdated: "2025-09-04"

keywords: , nhc004, vpe gateway hostname resolution

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why does the Network status show an `NHC004` error?
{: #ts-network-nhc004}
{: troubleshoot}
{: support}

[Virtual Private Cloud]{: tag-vpc}

When you check the status of your cluster's health by running the `ibmcloud oc cluster health issues --cluster <CLUSTER_ID>`, you see an error similar to the following example.
{: tsSymptoms}

```sh
ID       Component   Severity   Description
NHC004   Network     Warning    Some worker nodes in the cluster can not resolve VPE gateway hostnames.
```
{: screen}

This warning indicates that DNS resolution is failing for hostnames associated with Virtual Private Endpoints (VPE). This can affect services that rely on private connectivity to IBM Cloud services.
{: tsCauses}

Make sure that your worker nodes have correct DNS resolvers configured and can resolve the VPE gateway hostnames. The following steps help you confirm whether the DNS resolution issue is due to unreachable VPE endpoints or an incorrect configuration.
{: tsResolve}

## How to find the VPE gateways for a VPC cluster
{: #find-vpe-gateways}

To identify the VPE gateways used by your IBM Cloud Kubernetes Service cluster, follow these steps:

### 1. Use the IBM Cloud CLI to list endpoint gateways
{: #list-gateways-from-cli}

1. Run the following command to list all VPE (endpoint) gateways in your VPC.

    ```sh
    ibmcloud is endpoint-gateways
    ```
    {: pre}
    
    Example command to list VPEs for a specific VPC.

    ```sh
    ibmcloud is endpoint-gateways --vpc <VPC-ID>
    ```
    {: pre}

2. Filter the output for `iks-cluster_ID` and look for `Service Endpoints`. This shows the sassociated services, IP addresses, and endpoint names.


### 2. Use the IBM Cloud console to list endpoint gateways
{: #list-gateways-in-cloud-console}

1. Navigate to **VPC Infrastructure > Endpoint Gateways**
2. Select your VPC
3. Review configured gateways for private service access and view DNS/IP information

### 3. After finding the VPE gateway hostname complete the following steps.
{: #error-checking}

1. From a pod running on a worker node, launch a debug shell:

    ```sh
    kubectl run -i --tty debug --image=us.icr.io/armada-master/network-alpine:latest --restart=Never -- sh
    ```
    {: pre}

2. Inside the pod, try resolving a VPE gateway hostname.

    ```sh
    nslookup <vpe-hostname>
    ```
    {: pre}

    ```sh
    dig <vpe-hostname>
    ```
    {: pre}

3. Test DNS resolution directly using a VPC DNS service.

    ```sh
    dig <vpe-hostname> @161.26.0.7
    ```
    {: pre}

    ```sh
    dig <vpe-hostname> @161.26.0.8
    ```
    {: pre}

4. If your cluster is using custom DNS configurations (e.g., modified CoreDNS settings), inspect the config.

    ```sh
    kubectl get configmap coredns -n kube-system -o yaml
    ```
    {: pre}

5. If required, update the CoreDNS configuration to ensure VPE-resolving DNS servers are included, then reload CoreDNS.

    ```sh
    kubectl rollout restart deployment coredns -n kube-system
    ```
    {: pre}

6. Ensure that your VPC DNS settings allow access to the VPE hostnames. In the IBM Cloud console, navigate to **VPC > DNS services** and validate the DNS rules.

- For more on Virtual private endpoint (VPE) gateways in IBM Cloud Kubernetes Service, see [Virtual private endpoint (VPE) gateways](https://cloud.ibm.com/docs/containers?topic=containers-vpc-security-group-reference#sbd-managed-vpe-gateways){: external}.

- After corrections, wait a few minutes and recheck the cluster health status.

- If the issue persists, contact support for further assistance. Open a [support case](/docs/account?topic=account-using-avatar). In the case details, be sure to include any relevant log files, error messages, or command outputs.
