---

copyright:
  years: 2014, 2021
lastupdated: "2021-09-10"

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

As of 10 July 2021, version `0.0.2` of the OpenShift Container Storage add-on is deprecated and becomes unsupported on 24 July 2021. Add-on versions `4.6.0` and `4.7.0` are now available. If you have version `0.0.2` of the add-on installed in your cluster, update the add-on to a supported version. The OpenShift Container Storage add-on supports n+1 cluster versions. If you have a 4.6 cluster, update to add-on version `4.6.0` or `4.7.0`. If you have a 4.7 cluster, update to add-on version `4.7.0`.
{: important}

To view a list of add-ons and the supported {{site.data.keyword.openshiftshort}} versions, run the following command.
```sh
ibmcloud oc cluster addon versions --addon openshift-container-storage
```
{: pre}

Refer to the following table for a summary of changes for each version of the [OpenShift Data Foundation} add-on](/docs/openshift?topic=openshift-deploy-odf-vpc).

Refer to the following tables for a summary of changes for each version of the [OpenShift Data Foundation} add-on.

| OpenShift Data Foundation add-on | Is default? | Supported? | {{site.data.keyword.openshiftshort}} version support |
| --- | --- | --- | --- |
| 4.7.0 | <img src="images/icon-checkmark-confirm.svg" width="32" alt="Supported" style="width:32px;" /> | <img src="images/icon-checkmark-confirm.svg" width="32" alt="Supported" style="width:32px;" /> | 4.7 |
| 4.6.0 | | <img src="images/icon-checkmark-confirm.svg" width="32" alt="Supported" style="width:32px;" /> | 4.6 |
{: caption="Add-on versions" caption-side="top"}
{: summary="The rows are read from left to right. The first column is the add-on version. The second column indicates the default version. The third column is the version's supported state. The fourth column is the {{site.data.keyword.openshiftshort}} version of your cluster that the add-on version is supported for."}




