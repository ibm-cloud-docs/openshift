---

copyright: 
  years: 2024, 2024
lastupdated: "2024-06-07"

keywords: openshift, {{site.data.keyword.openshiftlong_notm}}, secure by default, {{site.data.keyword.openshiftlong_notm}}, outbound traffic protection, cluster create, quota, limitations

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}


# I use custom security groups and after creating a version 4.15 cluster, applications running in other clusters in my VPC are failing
{: #ts-sbd-other-clusters}


[Virtual Private Cloud]{: tag-vpc}
[4.15 and later]{: tag-red}

You use only custom security groups and you see worker creation failures and image pull errors in other clusters within your VPC after creating a version 4.15 cluster.
{: tsSymtpoms}

The following steps apply only in scenarios where you have opted out of using managed security groups and are instead using your own custom security groups.

With the introduction of Secure by Default Cluster VPC Networking in version 4.15, new VPE gateways and managed security groups are being used to manage network traffic.
{: tsCauses}

These new resources and rules might cause networking errors in the existing clusters in your VPC. Depending on how you created your previous clusters.

Before making a version 4.15 cluster, you created a cluster that does not use the managed cluster security group.

For example, you previously created clusters by using the `cluster create vpc-gen2` command with the `--cluster-security-group` option and did not include the `cluster` option.

The first time you create a Secure by Default cluster, the follow resources are created.

- A shared VPE gateway security group will be created (`kube-vpegw-<vpcID>`). All new and existing shared VPE gateways are updated to use it.

- Any previously existing managed security groups such as the `kube-<clusterID>` in the same VPC are updated with new rules to allow traffic through the new shared VPE gateway security group.

- Any future non-Secure by Default clusters in the same VPC will allow traffic through the new shared VPE gateway security group via the IKS-managed cluster security group (`kube-<clusterID>`).

Any existing or future non-secure by default cluster that does NOT use the managed cluster security group will not be able to access services through the VPE gateways. For example the Registry, {{site.data.keyword.openshiftlong_notm}} APIs, and more.
{: tsSymptoms}

To correct this problem add an inbound security group rule on the shared VPE gateway security group from one of your customer defined security groups.
{: tsResolve}  

1. Find the security group IDs for both your security group and the `kube-vpegw-<vpcID>` security group.

    ```sh
    ibmcloud is security-groups
    ```
    {: pre}

1. Add a remote rule to `kube-vpegw-<vpcID>` from your custom security group.
    ```sh
    ibmcloud is sg-rulec <kube-vpegw-vpcID> inbound all --remote <your SG ID>
    ```
    {: pre}

1. Add a remote rule from your custom security group to `kube-vpegw-<vpcID>`.
    ```sh
    ibmcloud is sg-rulec  <your SG> outbound all --remote  <ID of kube-vpegw-vpcID>
    ```
    {: pre}


