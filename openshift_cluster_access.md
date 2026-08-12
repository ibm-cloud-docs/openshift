---

copyright:
  years: 2014, 2026
lastupdated: "2026-08-11"

keywords: openshift, clusters, access, endpoint, private, public, vpe, satellite

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}

# Accessing {{site.data.keyword.redhat_openshift_notm}} clusters
{: #access_cluster}
{: help}
{: support}

After your {{site.data.keyword.openshiftlong_notm}} cluster is created, you can connect to it using several methods depending on your cluster type, network configuration, and use case. If you're not sure which method applies to you, start by identifying your cluster's infrastructure type and whether it has a public service endpoint (see [Choosing an access method](#access-method-choose) below).
{: shortdesc}

## Before you begin
{: #access-prereqs}

1. [Install the IBM Cloud CLI, the OpenShift CLI (`oc`), and required plug-ins](/docs/openshift?topic=openshift-cli-install).
1. If you haven't created a cluster yet, [create one now](/docs/openshift?topic=openshift-clusters). Otherwise, proceed to the next step.
1. If your network is protected by a company firewall, [allow access to the required API endpoints and ports](/docs/openshift?topic=openshift-firewall#corporate).
1. Verify your cluster is healthy by running `ibmcloud oc cluster get -c CLUSTER_NAME_OR_ID`. A healthy cluster shows `State: normal`. If you see a different state, see [Debugging clusters](/docs/openshift?topic=openshift-debug_clusters).
1. If your IBM Cloud account uses multifactor authentication (MFA), ensure it is enabled at the account level — contact your account owner if you're unsure. This is required for the `ibmcloud login` step when connecting to your cluster. For instructions, see [Enabling MFA](/docs/iam?topic=iam-enablemfa).

## Choosing an access method
{: #access-method-choose}

The right access method depends on your cluster infrastructure type, whether your cluster has a public or private service endpoint, and your network connectivity.

Not sure which type you have? In the IBM Cloud console, go to **OpenShift → Clusters**, click your cluster, and check the **Infrastructure** field on the Overview tab — it shows **VPC**, **Classic**, or **Satellite**. To check whether your cluster has a public or private service endpoint, look at the **Public Service Endpoint URL** and **Private Service Endpoint URL** fields on the same page, or run `ibmcloud oc cluster get -c CLUSTER_NAME_OR_ID` and check those fields in the output.
{: tip}

| Access method | Cluster type | Use when |
| --- | --- | --- |
| [Public cloud service endpoint](/docs/openshift?topic=openshift-access-public) | Classic, VPC | Your cluster has a public endpoint and you are connecting from outside the IBM Cloud network |
| [Private cloud service endpoint — VPC](/docs/openshift?topic=openshift-access-private-vpc) | VPC | Your cluster is private-only and you are connected to the VPC network through a VPN or Direct Link connection |
| [Private cloud service endpoint — Classic](/docs/openshift?topic=openshift-access-private-classic) | Classic | Your cluster is private-only and you are connected to the classic private network |
| [Virtual Private Endpoint (VPE) gateway](/docs/openshift?topic=openshift-cluster-access-vpe) | VPC | Your VPC cluster uses VPE for private master connectivity |
| [Satellite cluster service URL](/docs/openshift?topic=openshift-cluster-access-satellite) | Satellite | Your cluster runs on Satellite infrastructure |
| [API key or service ID](/docs/openshift?topic=openshift-cluster-access-automation) | All | Automated pipelines and non-interactive scripts |
| [Accessing private clusters by using the WireGuard VPN](/docs/openshift?topic=openshift-cluster-access-wireguard) | Classic, VPC | You want to access a private-only cluster from outside IBM Cloud using a WireGuard VPN |
{: caption="Cluster access methods" caption-side="bottom"}

## Advanced configuration
{: #access-advanced-config}

The following topics cover additional configuration required for specific access scenarios. Complete the primary access method above before applying these steps.

| Configuration topic | Cluster type | When to use |
| --- | --- | --- |
| [Setting the OAuth access type](/docs/openshift?topic=openshift-setting-oauth-access-type) | VPC | Your VPC cluster uses only the private service endpoint and you need to configure how the OpenShift console and OAuth are exposed |
| [Configuring security group rules for VPE gateway console access](/docs/openshift?topic=openshift-console-apiserver-oauthvpe) | VPC | Your cluster uses VPE gateway OAuth access and you need to add security group rules to allow VPN client connections to the API server and OAuth server |
{: caption="Advanced access configuration" caption-side="bottom"}
