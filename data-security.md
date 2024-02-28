---

copyright: 
  years: 2014, 2024
lastupdated: "2024-02-28"


keywords: openshift dedicated hosts

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}

# Overview of personal and sensitive data storage and removal options
{: #ibm-data}

Review what information is stored with IBM when you use {{site.data.keyword.openshiftlong_notm}}, how this data is stored and encrypted, and how you can permanently remove this information.
{: shortdesc}

## What information is stored with IBM when using {{site.data.keyword.openshiftlong_notm}}?
{: #pi-info}

For each cluster that you create with {{site.data.keyword.openshiftlong_notm}}, IBM stores the information that is described in the following table:

|Information type|Data|
|-------|----------|
|Personal information|The email address of the {{site.data.keyword.cloud_notm}} account that created the cluster.|
|Sensitive information|  - The TLS certificate and secret that is used for the assigned Ingress subdomain.  \n - The certificate authority that is used for the TLS certificate.  \n - The certificate authority, private keys, and TLS certificates for the {{site.data.keyword.redhat_openshift_notm}} master components, including the {{site.data.keyword.redhat_openshift_notm}} API server, etcd data store, and VPN.  \n - A customer root key in {{site.data.keyword.keymanagementservicelong_notm}} for each {{site.data.keyword.cloud_notm}} account that is used to encrypt personal and sensitive information.|
{: caption="Table 1. Information that is stored with IBM" caption-side="bottom"}

## How is my information stored and encrypted?
{: #pi-storage}

All information is stored in an etcd database and backed up every hour to {{site.data.keyword.cos_full_notm}}. The etcd database and {{site.data.keyword.cos_short}} service instance are owned and managed by the {{site.data.keyword.cloud_notm}} SRE team. For each {{site.data.keyword.cloud_notm}} account, a customer root key in {{site.data.keyword.keymanagementservicelong_notm}} is created that is managed by the {{site.data.keyword.openshiftlong_notm}} service team. This root key is used to encrypt all personal and sensitive information in etcd and in {{site.data.keyword.cos_short}}.

## Where is my information stored?
{: #pi-location}

The location where your information is stored depends on the location your cluster is in. By default, your data is stored in the {{site.data.keyword.openshiftlong_notm}} multizone metro area that is closest to your cluster. However, {{site.data.keyword.openshiftlong_notm}} might decide to store your data in a different multizone metro area to optimize the utilization of available compute resources. If you create your cluster in a non-multizone metro area, your data is still stored in the closest multizone metro area. This location might be in a different country than the one where you created your cluster. Make sure that your information can reside in a different country before you create your cluster in a non-multizone metro area.

The data that you create and own is always stored in the same location as the cluster. For more information about what data you can create in your cluster, how this data is encrypted, and how you can protect this data, see [Protecting sensitive information in your cluster](/docs/openshift?topic=openshift-encryption).
{: note}

## How can I remove my information?
{: #pi-removal}

Review your options to remove your information from {{site.data.keyword.openshiftlong_notm}}.
{: shortdesc}

Removing personal and sensitive information is permanent and not reversible. Make sure that you want to permanently remove your information before you proceed.
{: important}

Is my data removed when I remove the cluster?
:   Deleting a cluster does not remove all information from {{site.data.keyword.openshiftlong_notm}}. When you delete a cluster, cluster-specific information is removed from the etcd instance that is managed by IBM. However, your information still exists in the {{site.data.keyword.cos_full_notm}} backup and can still be accessed by the IBM service team by using the account-specific customer root key in {{site.data.keyword.keymanagementservicelong_notm}} that IBM owns and manages.

What options do I have to permanently remove my data?
:   To remove that data that IBM stores, choose between the following options. Note that removing your personal and sensitive information requires all your clusters to be deleted as well. Make sure that you backed up your app data before your proceed.

- **Open an {{site.data.keyword.cloud_notm}} support case**: Contact IBM Support to remove your personal and sensitive information from {{site.data.keyword.openshiftlong_notm}}. For more information, see [Getting support](/docs/get-support?topic=get-support-using-avatar).
- **End your {{site.data.keyword.cloud_notm}} subscription**: After you end your {{site.data.keyword.cloud_notm}} subscription, {{site.data.keyword.openshiftlong_notm}} removes the customer root key in {{site.data.keyword.keymanagementservicelong_notm}} that IBM created and managed for you as well as all the personal and sensitive information from the etcd data store and {{site.data.keyword.cos_short}} backup.


