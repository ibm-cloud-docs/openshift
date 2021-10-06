---

copyright:
  years: 2014, 2021
lastupdated: "2021-10-06"

keywords: openshift, roks, rhoks, rhos

subcollection: openshift
content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

  

# Classic clusters: Why does the master status have an ingress IP address for NLB error?
{: #rhoks_ts_openvpn_subnet}

**Infrastructure provider**: ![Classic infrastructure provider icon.](images/icon-classic-2.svg) Classic


When you run `ibmcloud oc cluster get -c <cluster_name_or_ID>`, you see the following error message in the **Master Status** field.
{: tsSymptoms}

```
CAE003: Unable to determine the ingress IP address for the network load balancer.
```
{: screen}

Additionally, when you run `ibmcloud oc nlb-dns create` to create a subdomain for a network load balancer (NLB), the command might fail with a message that the cluster is not found, the input parameters are incorrect, or you do not have the required roles.


The OpenVPN server could not be configured because load balancer IP address that exposes the default router could not be found. The router's load balancer service might not have been assigned an IP address because your cluster does not have a subnet with available portable IP addresses, or the load balancer setup did not complete.
{: tsCauses}


Verify that your cluster has available subnets, and that the load balancer setup completed successfully.
{: tsResolve}


## Verifying that your cluster has available subnets
{: #verify_subnets}

1. Check that your cluster has a **Subnet CIDR** for public and private subnets. If you set up a private VLAN-only cluster, you might have only a private subnet.
    ```sh
    ibmcloud oc cluster get --cluster <cluster_name_or_ID> --show-resources
    ```
    {: pre}

    Example output

    ```sh
    NAME:                           <cluster_name>   
    ...

    Subnet VLANs
    VLAN ID   Subnet CIDR        Public   User-managed   
    2345678   10.xxx.xx.xxx/29   false    false   
    2876543   169.xx.xxx.xxx/29  true     false
    ```
    {: screen}

2. If the cluster does not have a subnet, [create a subnet for the cluster](/docs/containers?topic=containers-subnets#request) or [add an existing subnet from your account to the cluster](/docs/containers?topic=containers-subnets#add-existing).
3. If the cluster does have a subnet, [check for available portable IP addresses](/docs/containers?topic=containers-subnets#review_ip) and if necessary, [add more portable IP address by adding a subnet](/docs/containers?topic=containers-subnets#adding_ips).
4. Refresh the master to restart the OpenVPN setup so that it uses the available subnet.
    ```sh
    ibmcloud oc cluster master refresh --cluster <cluster_name_or_ID>
    ```
    {: pre}

## Verifying that the load balancer setup completed successfully
{: #verify_nlb}

1. Check that the `ibm-cloud-provider-ip-*` pods for the load balancer are in a **Running** status.
    ```sh
    oc get pods -n ibm-system | grep ibm-cloud-provider-ip
    ```
    {: pre}

2. If a pod is not running, review the **Events** in the pod details to troubleshoot the issue further.
    ```sh
    oc describe pod -n kube-system <pod_name>
    ```
    {: pre}

3. After you resolve the load balancer pod issue, refresh the master to restart the NLB setup.
    ```sh
    ibmcloud oc cluster master refresh --cluster <cluster_name_or_ID>
    ```
    {: pre}






