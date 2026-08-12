---

copyright:
  years: 2014, 2026
lastupdated: "2026-08-11"

keywords: openshift, clusters, access, private, endpoint, vpc, vpn, direct link

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}

# Accessing VPC clusters through the private cloud service endpoint
{: #access-private-vpc}

For {{site.data.keyword.redhat_openshift_notm}} VPC clusters that have only the private cloud service endpoint enabled, you must be connected to the VPC private network through a VPN or {{site.data.keyword.dl_full_notm}} connection to access the cluster.
{: shortdesc}

## Before you begin
{: #access-private-vpc-prereqs}

1. [Install the required CLI tools](/docs/openshift?topic=openshift-cli-install).
1. Set up one of the following connections to the VPC private network.
   - [Client-to-site VPN](/docs/vpc?topic=vpc-vpn-client-to-site-overview)
   - [Site-to-site VPN](/docs/vpc?topic=vpc-vpn-onprem-example)
   - [{{site.data.keyword.dl_full_notm}}](/docs/dl?topic=dl-get-started-with-ibm-cloud-dl)
1. Verify your cluster is healthy: `ibmcloud oc cluster get -c CLUSTER_NAME_OR_ID`.

## Accessing a private VPC cluster from the CLI
{: #access-private-vpc-cli}

1. Connect to your VPC private network using your VPN or Direct Link connection.
1. Set the cluster context using the private endpoint.
   ```sh
   ibmcloud oc cluster config -c CLUSTER_NAME_OR_ID --endpoint private
   ```
   {: pre}

1. Log in to the cluster.
   - **As admin**: `ibmcloud oc cluster config -c CLUSTER_NAME_OR_ID --admin --endpoint private`
   - **With a passcode**: `oc login -u passcode -p <iam_passcode> --server=<private_master_URL>`
   - **With an API key**: See [Accessing clusters from automation tools](/docs/openshift?topic=openshift-cluster-access-automation).

1. Verify access.
   ```sh
   oc version
   ```
   {: pre}

## Accessing through the Virtual Private Endpoint (VPE) gateway
{: #access-private-vpc-vpe}

VPC clusters also support access through a VPE gateway. See [Accessing VPC clusters through the Virtual Private Endpoint gateway](/docs/openshift?topic=openshift-cluster-access-vpe).
