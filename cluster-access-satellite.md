---

copyright:
  years: 2014, 2026
lastupdated: "2026-08-11"

keywords: openshift, satellite, clusters, access, service url, link endpoint, public network

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}

# Accessing clusters on {{site.data.keyword.satelliteshort}}
{: #cluster-access-satellite}

{{site.data.keyword.redhat_openshift_notm}} clusters on {{site.data.keyword.satelliteshort}} can be accessed through several methods depending on your network setup.
{: shortdesc}

## Before you begin
{: #cluster-access-satellite-prereqs}

1. [Install the required CLI tools](/docs/openshift?topic=openshift-cli-install).
1. [Create your {{site.data.keyword.satelliteshort}} cluster](/docs/openshift?topic=openshift-satellite-clusters).

## Accessing clusters through the cluster service URL
{: #access-cluster-sat-se}

Connect to your cluster through its service URL, which has the format `https://p1iuql40jam23qiuxt833-...satellite.appdomain.cloud:30710`.

1. In the [{{site.data.keyword.cloud_notm}} console](https://cloud.ibm.com/){: external}, navigate to your cluster.
1. Click **{{site.data.keyword.redhat_openshift_notm}} web console**.
1. Click your profile name, then click **Copy Login Command** > **Display Token**.
1. Copy the `oc login` command and paste it into your terminal.

If your hosts have private network connectivity only, you must connect through VPN to access the console. See [Accessing clusters from the public network](#sat-public-access) for options.
{: note}

## Accessing clusters from within the {{site.data.keyword.cloud_notm}} private network
{: #access-cluster-sat-link}

Use the {{site.data.keyword.satelliteshort}} Link endpoint to connect through the secured Link tunnel server. The endpoint format is `c-02.<region>.link.satellite.cloud.ibm.com:<port>`.

To use the `--endpoint link` option, you must configure a **Source** in your location. For more information, see [Accessing your Red Hat OpenShift API Satellite link endpoints](/docs/satellite?topic=satellite-link-endpoint-secure).
{: note}

```sh
ibmcloud oc cluster config -c CLUSTER_NAME_OR_ID --endpoint link --admin
```
{: pre}

## Accessing clusters from the public network
{: #sat-public-access}

If your hosts have public network connectivity and you want to connect from your local machine without a private VPN, you can update your cluster's subdomain DNS records to use your hosts' public IP addresses.

Making location and cluster subdomains publicly accessible is not recommended for production workloads.
{: important}

For full steps, see [Satellite Link endpoint documentation](/docs/satellite?topic=satellite-link-endpoint-secure).
