---

copyright: 
  years: 2025, 2025
lastupdated: "2025-07-16"

keywords: openshift, {{site.data.keyword.openshiftlong_notm}}, secure by default, {{site.data.keyword.openshiftlong_notm}}, outbound traffic protection, limitations, vpe, vsi

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

[Virtual Private Cloud]{: tag-vpc}


# Why can't my VSIs access VPE gateway?
{: #ts-sbd-vsi-vpe}

[Virtual Private Cloud]{: tag-vpc}
[4.15 and later]{: tag-red}


Review the following scenarios for why your VSI can't access your VPE gateway.
{: tsSymptoms}

- You have a VSI that is able to communicate through your registry VPE gateway until a secure by default cluster is added to the VPC, then your VSI can no longer communicate through the gateway.
- You already have a secure by default environment and when you create a new VSI, that VSI cannot communicate through the existing gateways.



If you provision a VSI in a VPC containing [secure by default clusters](/docs/openshift?topic=openshift-vpc-security-group-reference) several VPE gateways [are created](/docs/openshift?topic=openshift-vpc-security-group-reference#sbd-managed-vpe-gateways). In a secure by default environment these gateways are attached to a [security group](/docs/openshift?topic=openshift-vpc-security-group-reference#vpc-sg-kube-vpegw-vpc-id) that, by default, only allows inbound traffic from {{site.data.keyword.openshiftlong_notm}} clusters in the VPC. Any standalone VSI will not have access.
{: tsCauses}

Choose from one of the following options to resolve the issue.
{: tsResolve}

- **Attach your `kube-CLUSTERID` security group to your VSI**.
    - Each cluster in your VPC has a security group attached to its worker nodes. The name of this security group is `kube-CLUSTERID`.
    - This security group has already been configured to talk to your VPE gateway. - You can attach any `kube-CLUSTERID` security group to your VSI allows the VSI to communicate through the VPE gateway.
    - You can attach security groups to your VSIs from the VPC console.

- **Add an inbound security group rule from your VSI security group to your VPE gateway security group**.
    1. Find the security group IDs for the current VSI and the `kube-vpegw-<vpcID>` security group.
        ```sh
        ibmcloud is security-groups
        ```
        {: pre}

    1. Add the following remote rule to `kube-vpegw-<vpcID>` from your VSI's security group
        ```sh
        ibmcloud is sg-rulec <kube-vpegw-vpcID> inbound all --remote <your-VSI-SG-ID>
        ```
        {: pre}

    1. Add a remote rule from your VSI security group to `kube-vpegw-<vpcID>`.
        ```sh
        ibmcloud is sg-rulec <your-VSI-SG> outbound all --remote  <ID of kube-vpegw-vpcID>
        ```
        {: pre}

If the issue persists, contact support. Open a [support case](/docs/account?topic=account-using-avatar). In the case details, be sure to include any relevant log files, error messages, or command outputs.

