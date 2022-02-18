---

copyright: 
  years: 2014, 2022
lastupdated: "2022-02-18"

keywords: openshift

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}


# Why does my cluster stay in a pending state?
{: #cs_cluster_pending}
{: support}

**Infrastructure provider**:
* ![Classic infrastructure provider icon.](images/icon-classic-2.svg) Classic
* ![VPC infrastructure provider icon.](images/icon-vpc-2.svg) VPC


When you deploy your cluster, it remains in a pending state and doesn't start.
{: tsSymptoms}


If you just created the cluster, the worker nodes might still be configuring. If you already wait for a while, you might have an invalid VLAN.
{: tsCauses}



You can try one of the following solutions:
{: tsResolve}

    - Check the status of your cluster by running `ibmcloud oc cluster ls`. Then, check to be sure that your worker nodes are deployed by running `ibmcloud oc worker ls --cluster <cluster_name>`.
    - Check to see whether your VLAN is valid. To be valid, a VLAN must be associated with infrastructure that can host a worker with local disk storage. You can [list your VLANs](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_vlans) by running `ibmcloud oc vlan ls --zone <zone>` if the VLAN does not show in the list, then it is not valid. Choose a different VLAN.



