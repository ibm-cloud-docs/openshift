---

copyright:
  years: 2014, 2022
lastupdated: "2022-05-06"

keywords: odf, openshift data foundation add-on, changelog

subcollection: openshift, container storage

---

{{site.data.keyword.attribute-definition-list}}


# OpenShift Data Foundation add-on changelog
{: #odf_addon_changelog}

View information for updates to the OpenShift Data Foundation add-on in your {{site.data.keyword.openshiftlong}} clusters.
{: shortdesc}

Note that the add-on supports`n+1` cluster versions.
{: note}

To view a list of add-ons and the supported {{site.data.keyword.redhat_openshift_notm}} versions, run the following command.

```sh
ibmcloud oc cluster addon versions --addon openshift-data-foundation
```
{: pre}

Refer to the following table for a summary of changes for each version of the [OpenShift Data Foundation add-on](/docs/openshift?topic=openshift-deploy-odf-vpc).

| Add-on version | Is default? | Supported? | {{site.data.keyword.redhat_openshift_notm}} version support |
| --- | --- | --- | --- |
| 4.9.0 | Yes | Yes | >=4.9.0 <4.11.0 |
| 4.8.0 | Yes | Yes | >=4.8.0 <4.10.0 |
| 4.7.0 | No | Yes | >=4.7.0 <4.9.0 |
{: caption="Add-on versions" caption-side="top"}
{: summary="The rows are read from left to right. The first column is the add-on version. The second column indicates the default version. The third column is the version's supported state. The fourth column is the version of your cluster that the add-on version is supported for."}









