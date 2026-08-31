---

copyright:
  years: 2014, 2026
lastupdated: "2026-08-31"

keywords: openshift, clusters, access, private, endpoint, classic, vpn

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}

# Accessing Classic clusters through the private cloud service endpoint
{: #access-private-classic}

For {{site.data.keyword.redhat_openshift_notm}} Classic clusters that have only the private cloud service endpoint enabled, you must be connected to the IBM Cloud classic private network through a VPN connection to access the cluster.
{: shortdesc}

## Before you begin
{: #access-private-classic-prereqs}

1. [Install the required CLI tools](/docs/openshift?topic=openshift-cli-install).
1. Set up a [{{site.data.keyword.vpn_full}}](/docs/iaas-vpn?topic=iaas-vpn-getting-started) connection to the IBM Cloud classic private network.
1. Verify your cluster is healthy: `ibmcloud oc cluster get -c CLUSTER_NAME_OR_ID`.

## Accessing a private Classic cluster from the CLI
{: #access-private-classic-cli}

1. Connect to the IBM Cloud classic private network using your VPN client.
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
