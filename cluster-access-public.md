---

copyright:
  years: 2014, 2026
lastupdated: "2026-08-19"

keywords: openshift, clusters, access, public, endpoint, console, cli, login

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}

# Accessing clusters through the public cloud service endpoint
{: #cluster-access-public}

For {{site.data.keyword.redhat_openshift_notm}} Classic and VPC clusters that have a public cloud service endpoint enabled, you can log in from the {{site.data.keyword.cloud_notm}} console or the CLI.
{: shortdesc}

## Before you begin
{: #access-public-prereqs}

1. [Install the required CLI tools](/docs/openshift?topic=openshift-cli-install).
1. If your network is protected by a company firewall, [allow access to the required API endpoints and ports](/docs/openshift?topic=openshift-firewall#corporate).
1. Verify your cluster is healthy: `ibmcloud oc cluster get -c CLUSTER_NAME_OR_ID`.

## Connecting from the {{site.data.keyword.cloud_notm}} console
{: #access-public-console}

1. In the [{{site.data.keyword.cloud_notm}} console](https://cloud.ibm.com/){: external}, navigate to your cluster.
1. Click **{{site.data.keyword.redhat_openshift_notm}} web console**.
1. To continue in the CLI, click your profile name, then click **Copy Login Command**.
1. Click **Display Token**, copy the `oc login` command, and paste it into your terminal.

Log out of both the {{site.data.keyword.cloud_notm}} console and the {{site.data.keyword.redhat_openshift_notm}} web console before closing your browser. You must complete both steps to successfully log out.
{: note}

## Connecting from the CLI
{: #access-public-cli}

Choose one of the following options.

### Log in as admin
{: #access-public-cli-admin}

Run the following command to download the TLS certificates and set the cluster context. Requires the **Administrator** platform access role.

```sh
ibmcloud oc cluster config -c CLUSTER_NAME_OR_ID --admin
```
{: pre}

### Log in with a passcode
{: #access-public-cli-passcode}

1. Get the master URL: `ibmcloud oc cluster get -c CLUSTER_NAME_OR_ID`
1. Open [https://iam.cloud.ibm.com/identity/passcode](https://iam.cloud.ibm.com/identity/passcode){: external} and copy your one-time passcode.
1. Log in to the cluster.
   ```sh
   oc login -u passcode -p <iam_passcode> --server=<master_URL>
   ```
   {: pre}

### Log in with an API key
{: #access-public-cli-apikey}

See [Accessing clusters from automation tools by using an API key](/docs/openshift?topic=openshift-cluster-access-automation).
