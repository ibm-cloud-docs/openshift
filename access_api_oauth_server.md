---

copyright:
  years: 2025, 2025
lastupdated: "2025-02-28"


keywords: oauth access, oauth, api server, vpe gateway, vpc

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}

# Accessing the OpenShift console when OAuth access is set to VPE gateway
{: #console-apiserver-oauthvpe}

For certain VPC clusters, setting the OAuth access to the VPE gateway type might prevent you from accessing the OpenShift web console. When OAuth access is set to the VPE gateway type, some cluster configurations require you to add security group rules that allow connections from the VPN to the cluster API server and OAuth server. These connections are required to access the OpenShift console. For more information, see [Understanding the cluster connection flow](/docs/openshift?topic=openshift-ts-cluster-console-vpe-priv#ts-console-vpe-priv-flow).

Not all clusters require these changes. These steps apply only if:
- You have changed your security groups so that traffic between the cluster workers and master VPE gateway is blocked, **OR**
- You have modified the `kube-<CLUSTER-ID>` security group, **OR**
- You applied a different or custom security group to the cluster master's VPE gateway, **OR**
- All the following conditions are true. 
    - Your cluster is a VPC cluster that has only private service endpoints. 
    - Your cluster's OAuth access is the vpe-gateway type.
    - Your cluster uses Secure by Default cluster networking. 

## Allowing connections from VPN clients to the API server and OAuth server
{: #apiserver-oauth-allow}

Follow these steps to allow inbound TCP connections from your VPN clients to your cluster's API server and OAuth server. 

If your cluster uses Secure by Default (SBD) networking and you modified or renamed any SBD security groups, you might need to adapt the commands in these steps to reference the modified security groups. 
{: note}

1. Get the name of the security group that applies to the VPE gateway. If you have not modified any security groups, the name uses the `kube-vpegw-<cluster-id>` format. However, if you have a SBD cluster and you replaced or modified the security group, it might have a different format. 
    ```sh
    ibmcloud is endpoint-gateway iks-<cluster-id>
    ```
    {: pre}

2. List the rules in the security group that is applied to the VPE gateway. Specify the full security group name you found in the previous step. If the security group has a different name, specify that name instead of `kube-vpegw-<cluster-id>`. If you have not made any modifications to your security group, the output lists three inbound rules that allow cluster workers to access the API server, Oauth, and Konnectivity server ports.

    ```sh
    ibmcloud is security-group kube-vpegw-<cluster-id>`
    ```
    {: pre}

3. Find the subnet used by your client system. If you are using more than one client system, repeat this step for each system.  

    A client system is any system that accesses the API server port and OAuth port, such as accessing the OpenShift web console or running the `oc login` command. 
    {: note}

    If you are using a standard [IBM Cloud client-to-site VPN](/docs/vpc?topic=vpc-vpn-client-to-site-overview), use the `ibmcloud is vpn-server <VPN-NAME-OR-ID>` command to find the subnet instead. In the output, find the `Client IP pool` to find the subnet. 
    {: note}

4. Get the API server port and OAuth port for your cluster. In the output, the API server port is the number at the end of the `VPE Gateway value`. The OAuth server port is the number at the end of the `OAuth Server URL` value. 

    ```sh
    ibmcloud oc cluster get -c ${CLUSTERID}
    ```
    {: pre}

5. Add a security group rule that allows the client system subnet to access the API server port and the OAuth server port when connecting to the VPC. Add a separate rule for each port. If you found a subnet for multiple client systems in the previous steps, repeat this step for each subnet.

    ```sh
    ibmcloud is security-group-rule-add kube-vpegw-${CLUSTERID} inbound tcp --port-min <API-SERVER-PORT>   --port-max <API-SERVER-PORT>   --remote <CLIENT-SYSTEM-SUBNET>
    ibmcloud is security-group-rule-add kube-vpegw-${CLUSTERID} inbound tcp --port-min <OAUTH-SERVER-PORT> --port-max <OAUTH-SERVER-PORT> --remote <CLIENT-SYSTEM-SUBNET>
    ```
    {: pre}

    Example command to add a security group for an API server port value `32100` and a client system subnet IP pool `192.168.192.0/22`.

    ```sh
    ibmcloud is security-group-rule-add kube-vpegw-${CLUSTERID} inbound tcp --port-min 32100 --port-max 32100 --remote 192.168.192.0/22`
    ```
    {: pre}

6. List the rules in the security group again to validate that the rules added in the previous step are present.

    ```sh
    ibmcloud is security-group kube-vpegw-<cluster-id>`
    ```
    {: pre}
