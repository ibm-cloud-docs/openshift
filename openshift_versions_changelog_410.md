---

copyright:
  years: 2022, 2022
lastupdated: "2022-05-06"

keywords: openshift, 4.10, update, upgrade, BOM, bill of materials, versions, patch

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}


# Version 4.10 change log
{: #openshift_changelog_410}

View information of version changes for major, minor, and patch updates that are available for your {{site.data.keyword.openshiftlong}} clusters that run version 4.10. Changes include updates to {{site.data.keyword.redhat_openshift_notm}}, Kubernetes, and {{site.data.keyword.cloud_notm}} Provider components.
{: shortdesc}

## Overview
{: #openshift_changelog_overview_410}

Unless otherwise noted in the change logs, the {{site.data.keyword.cloud_notm}} provider version enables {{site.data.keyword.redhat_openshift_notm}} APIs and features that are at beta. {{site.data.keyword.redhat_openshift_notm}} alpha features, which are subject to change, are disabled.
{: shortdesc}

Check the [Security Bulletins on {{site.data.keyword.cloud_notm}} Status](https://cloud.ibm.com/status?selected=security) for security vulnerabilities that affect {{site.data.keyword.openshiftlong_notm}}. You can filter the results to view only **Kubernetes Service** security bulletins that are relevant to {{site.data.keyword.openshiftlong_notm}}. Change log entries that address other security vulnerabilities but don't include a {{site.data.keyword.IBM_notm}} security bulletin are for vulnerabilities that are not known to affect {{site.data.keyword.openshiftlong_notm}} in normal usage. If you run privileged containers, run commands on the workers, or execute untrusted code, then you might be at risk.

Master patch updates are applied automatically. Worker node patch updates can be applied by reloading or updating the worker nodes. For more information about major, minor, and patch versions and preparation actions between minor versions, see [{{site.data.keyword.redhat_openshift_notm}} versions](/docs/openshift?topic=openshift-openshift_changelog).
{: tip}


## Change logs
{: #410_changelog}

Review the version 4.10 change log.
{: shortdesc}


### Change log for fix pack 4.10.9_1515_openshift (master) and 4.10.10_1516_openshift (worker node), released 27 April 2022
{: #4109_1515_openshift_and_41010_1516_openshift}

| Component | Previous | Current | Description |
| --- | --- | --- | --- |
| Calico | v3.21.5 | v3.22.2 | See the [Calico release notes](https://projectcalico.docs.tigera.io/releases){: external}. |
| Calico Operator | v1.23.7 | v1.25.7 | See the [Calico Operator release notes](https://github.com/tigera/operator/releases/tag/v1.25.7){: external}. |
| IBM Cloud Controller Manager | v1.22.8-7 | v1.23.5-9 | Updated to support the Kubernetes `1.23.5` release and to use Go version `1.17.8`. Classic load balancers are updated to improve availability during updates. In addition, creating a mixed protocol load balancer is not supported. |
| OpenShift (master) | 4.9.28 | 4.10.9 | See the [OpenShift release notes](https://docs.openshift.com/container-platform/4.10/release_notes/ocp-4-10-release-notes.html#ocp-4-10-9){: external}. |
| OpenShift (worker) | 4.9.29 | 4.10.10 | See the [OpenShift release notes](https://docs.openshift.com/container-platform/4.10/release_notes/ocp-4-10-release-notes.html#ocp-4-10-10){: external}. Worker nodes are configured to pull images in parallel. |
| Red Hat OpenShift Control Plane Operator | v4.9.0-20220412 | v4.10.0-20220420 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.10.0+20220420){: external}. |
| Red Hat OpenShift configuration | N/A | N/A | Updated the [feature gate configuration](/docs/openshift?topic=openshift-service-settings#feature-gates). |
| {{site.data.keyword.openshiftlong_notm}} Metrics Server | v4.9.0-20220412 | v4.10.0-20220420 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.10.0+20220420){: external}. |
| {{site.data.keyword.openshiftlong_notm}} toolkit | 4.9.0+20220412 | 4.10.0+20220420 | See the [{{site.data.keyword.openshiftlong_notm}} toolkit release notes](https://github.com/openshift/ibm-roks-toolkit/releases/tag/v4.10.0+20220420){: external}. |
{: summary="The rows are read from left to right. The first column is the changed component. The second column is the previous version number of the component. The third column is the current version number of the component. The fourth column contains a brief description of the change made to the component."}
{: caption="Changes since version 4.9.28_1536_openshift master and 4.9.29_1537_openshift worker node" caption-side="top"}
