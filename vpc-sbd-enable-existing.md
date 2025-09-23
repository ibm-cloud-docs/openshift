---

copyright: 
  years: 2024, 2025
lastupdated: "2025-09-23"

keywords: openshift, {{site.data.keyword.openshiftlong_notm}}, secure by default, outbound traffic protection, 4.15

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}


# Enabling secure by default for clusters created at 4.14 and earlier
{: #vpc-sbd-enable-existing}


[Virtual Private Cloud]{: tag-vpc}
[4.14 and earlier]{: tag-red}

The following steps walk you through enabling the security group configurations that were introduced with secure by default on clusters that were created before 4.15. Secure by default networking introduced new security group configurations and behaviors for newly provisioned VPC clusters created at 4.15 and later. Clusters created at versions 4.14 and earlier did not get the secure by default security group configurations when updating to 4.15.
{: shortdesc}

Enabling secure by default on your cluster is permanent and irreversible. The enablement process requires you to replace all the workers nodes in your cluster. Only enable secure by default when it's beneficial to do so. Note that load balancers might not be accessible until after you replace all your workers. For more information, see [Understanding secure by default](/docs/openshift?topic=openshift-vpc-security-group-reference).
{: important}


## Preparing to enable secure by default
{: #existing-cluster-sbd-prepare}

Understand that when you enable secure by default on your cluster then only the traffic that's necessary for the cluster to function is allowed and all other access is blocked.

- Verify your cluster is at a version that supports secure by default. Update your cluster to at least 4.15.
- Verify your cluster is not already secure by default. You can find this by running `ibmcloud ks cluster get` and reviewing the output.
- Verify that none of your worker nodes are currently in provisioning state.

    ```sh
    Retrieving cluster CLUSTER...
    OK
                                    
    Name:                           CLUSTER
    ID:                             CLUSTER
    State:                          normal
    Status:                         All Workers Normal
    ...
    Secure By Default Networking:   enabled
    Outbound Traffic Protection:    enabled
    ```
    {: screen}

- Verify you won't exceed any of the follow quotas. If any of the following quotas are exceeded, the enablement process fails. For more information, see [VPC quotas](/docs/vpc?topic=vpc-quotas).
    - You must have 15 or fewer clusters in your VPC. There is a maximum of 15 rules that can target other security groups as their source or destination. By default, {{site.data.keyword.openshiftlong_notm}} applies 1 rule that targets the `kube-<clusterID>` security group for each cluster in the VPC. Because of this quota, only 15 clusters can be created in a given VPC.
    - You must have 95 or fewer security groups in your VPC. You can have a maximum 100 security groups in a VPC. Enabling secure by default creates 4 security groups. If you have close to 100 security groups already, then consider reducing or consolidating them before proceeding.
    - You must have 4 or fewer security groups for your cluster workers. Cluster workers can have up to 5 security groups. Enabling secure by default adds one security group to your workers.
- If you have custom security group rules on your existing cluster worker security group (`kube-<clusterID>`) they are removed during enablement. If you want to keep these rules, make note of them ahead of time, and add them after the enablement.


## What happens when I enable secure by default?
{: #existing-cluster-what}


When you enable secure by default, the following set of secure by default security groups are created or updated.


| Security group | Description of changes |
| --- | --- |
| `kube-<clusterID>` | The cluster worker security group (`kube-<clusterID>`) is reset. This security group is attached to your cluster workers. Usually, this group already exists. However, if your workers currently use only your own custom, user defined security groups, this security group would not have been created during the initial creation of your cluster. In this case, this group is created. All existing rules are removed and the new secure by default security group rules are added to this security group. Load balancers apply the rules to both the cluster worker and load balancer security groups. |
| `kube-vpegw-<clusterID>` | A new security group for your master VPE gateway is created. Any existing rules are removed. Because this is a new group, most likely there are no rules. |
| `kube-vpegw-<vpcID>` | A new security group for your shared VPE gateways. This security group might already exist if there are existing secure by default clusters in your VPC. Because this group is shared by all clusters, it is only created one time. The previous VPE gateway security group (`kube-<vpcID>`) is removed from all your IBM-managed shared VPE gateways, and replaced with the new shared VPE gateway security group (`kube-vpegw-<vpcID>`). This might have already been done if you have other secure by default clusters at 4.15 and later in your VPC. |
| `kube-lbaas-<clusterID>` | A new security group for your load balancers. The security groups attached to your load balancers (NLB and ALB) are updated. The previous load balancer security group (`kube-<vpcID>`) is removed from your load balancers and replaced with the new load balancer security group (`kube-lbaas-<clusterID>`). If the previous security group does not exist on a load balancer, no action is taken. Only IBM-managed load balancers and security groups are affected. Custom security groups are not removed or replaced. |
| `kube-<vpcID>` | The previous VPE gateway security group (`kube-<vpcID>`) is removed from your master VPE gateway and replaced with the new master VPE gateway security group (`kube-vpegw-<clusterID>`). |
| Default VPC security group | The default VPC security group is no longer used. |
| Custom security groups | Any user defined security groups that are attached to cluster worker nodes are attached to the new workers. Custom security groups are not removed or replaced. |
{: caption="Security group changes when enabling secure by default" caption-side="bottom"}



## In what order are the changes applied?
{: #sbd-existing-update-order}

The following operations are performed when you update your cluster to secure by default.

1. The following set of secure by default security groups are created if they do not already exist.
    * `kube-<clusterID>`
    * `kube-vpegw-<clusterID`
    * `kube-vpegw-<vpcID>`
    * `kube-lbaas-<clusterID>`

1. The security groups attached to your VPE gateways are updated. Only IBM-managed gateways and security groups are affected. Custom security groups are not impacted. If the previous security group does not exist on a gateway, no action is taken.

1. The previous VPE gateway security group (`kube-<vpcID>`) is removed from your master VPE gateway and replaced with the new master VPE gateway security group (`kube-vpegw-<clusterID>`).

1. The previous VPE gateway security group (`kube-<vpcID>`) is removed from all your IBM-managed shared VPE gateways, and replaced with the new shared VPE gateway security group (`kube-vpegw-<vpcID>`). This might have already happened if you have other secure by default clusters in your VPC.

1. The security groups attached to your load balancers (NLB & ALB) are updated. Only IBM-managed load balancers and security groups are updated. Custom security groups are not impacted. If the previous security group does not exist on a load balancer, no action is taken.

1. The previous load balancer security group (`kube-<vpcID>`) is removed from your load balancers and replaced with the new load balancer security group (`kube-lbaas-<clusterID>`)

1. The cluster worker security group (`kube-<clusterID>`) is reset. 
    * All existing rules are removed.
    * New secure by default security group rules are added.

1. Load balancer rules are applied to both the cluster worker and load balancer security groups.

1. The master VPE gateway security group is reset.
    * All existing rules are removed. However, because this was newly created (in step 1), usually there are no rules.
    * The new secure by default security group rules are added.

The previous steps are handled automatically. However, clusters created before secure by default have the default VPC security group attached to the workers. This security group must be removed, but cannot be removed by the IBM provided automation. Therefore, you must manually replace your workers to complete the update process. During a worker replace the following updates happen.

1. The cluster worker security group (`kube-<clusterID>`) and any previously added user defined security groups are attached to the new worker.

1. The default VPC security group is no longer used. 


## Enabling secure by default
{: #existing-cluster-sbd-enable}

Complete the following steps to apply the secure by default security group configuration to your cluster.

1. Run the following command.

    ```sh
    ibmcloud oc vpc secure-by-default enable --cluster <CLUSTER ID> [--disable-outbound-traffic-protection][-f]
    ```
    {: pre}

1. Wait for the process to complete. A variety of factors can influence how long it takes to enable your cluster to secure by default. Usually it finishes in less than 5 minutes. You can verify that the process is finished by inspecting your new security groups.
    - Your master VPE gateway security group `kube-vpegw-CLUSTERID` contains rules.
    - Your load balancer security group `kube-lbaas-CLUSTERID` contains rules.


1. Replace all worker nodes in your cluster. 

    ```sh
    ibmcloud oc worker replace --cluster CLUSTER --worker WORKER -f
    ```
    {: pre}
