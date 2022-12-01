---

copyright: 
  years: 2022, 2022
lastupdated: "2022-12-01"

keywords: openshift

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}



# Cloud Foundry roles
{: #cloud-foundry-roles}

Cloud Foundry roles grant access to organizations and spaces within the account. To see the list of Cloud Foundry-based services in {{site.data.keyword.cloud_notm}}, run `ibmcloud service list`. To learn more, see all available [org and space roles](/docs/account?topic=account-mngcf) or the steps for [managing Cloud Foundry access](/docs/account?topic=account-mngcf) in the {{site.data.keyword.cloud_notm}} IAM documentation.
{: shortdesc}

The following table shows the Cloud Foundry roles that are required for cluster action permissions.

| Cloud Foundry role | Cluster management permissions |
| -------------- | -------------- |
| Space role: Manager | Manage user access to an {{site.data.keyword.cloud_notm}} space |
| Space role: Developer |  - Create {{site.data.keyword.cloud_notm}} service instances \n - Bind {{site.data.keyword.cloud_notm}} service instances to clusters \n - View logs from a cluster's log forwarding configuration at the space level |
{: caption="Table 1. Cluster management permissions by Cloud Foundry role" caption-side="bottom"}
