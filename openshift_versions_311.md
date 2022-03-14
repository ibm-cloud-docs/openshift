---

copyright:
  years: 2014, 2022
lastupdated: "2022-03-14"

keywords: openshift, version, update, upgrade

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}



# (Deprecated) 3.11 version 
{: #cs_versions_46}

Review information about version 3.11 of {{site.data.keyword.openshiftlong_notm}}, released 01 Aug 2019.
{: shortdesc}

Version 3.11 is deprecated, with a tentative unsupported date of June 2022. This is the last minor version of major version 3. Note that you [cannot update a cluster from one major version to another](#311_deprecated). 
{: deprecated}

Looking for general information about updating clusters, or information on a different version? See [Red Hat OpenShift on IBM Cloud version information](/docs/openshift?topic=openshift-openshift_changelog).
{: tip}


## Release timeline 
{: #release_timeline_46}

The following table includes the expected release timeline for version 4.6. You can use this information for planning purposes, such as to estimate the general time that the version might become unsupported. 
{: shortdesc}

Dates that are marked with a dagger (`†`) are tentative and subject to change.
{: important}

| Supported? | {{site.data.keyword.redhat_openshift_notm}} / Kubernetes version | Release date | Unsupported date |
| --- | --- | --- | --- |
| Deprecated | 3.11 / 1.11 | 01 Aug 2019 | 06 Jun 2022 `†` |
{: caption="Release history for {{site.data.keyword.openshiftlong_notm}} version 3.11." caption-side="top"}
{: summary="The rows are read from left to right. The first column is the supported status, the second column is OpenShift and Kubernetes version number. The third column is the release date. The fourth column is the unsupported date."}

### Why is the deprecated version 3.11 supported longer than more recent versions like 4.6?
{: #311_deprecated}

In general, the last minor version of a major version is supported longer than other minor versions. Because you can't update a cluster from one major version to another (such as version 3 to 4), this longer support period gives you time to create clusters at a more recent version. Minor versions of a more recent major version might become unsupported before the last minor version of a deprecated major version because the more recent major version has subsequent minor releases that are supported. For example, version 4.3 becomes unsupported before the deprecated version 3.11 because version 4 has future minor releases, but 3.11 is the last minor version of version 3.


