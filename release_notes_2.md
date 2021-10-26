---

copyright: 
  years: 2014, 2021
lastupdated: "2021-10-26"

keywords: openshift, roks, rhos, rhoks

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}

# Release notes
{: #rel-notes}

Use the release notes to learn about the latest changes to the {{site.data.keyword.openshiftlong}} documentation that are grouped by month.
{: shortdesc}


For information about releases that occured before August 30th, see [Release notes](/docs/openshift?topic=openshift-iks-release).


Looking for {{site.data.keyword.cloud_notm}} status, platform announcements, security bulletins, or maintenance notifications? See [{{site.data.keyword.cloud_notm}} status](https://cloud.ibm.com/status?selected=status){: external}.
{: note}



## October 2021
{: #release-oct-2021}

Review the release notes for October 2021.
{: shortdesc}

### 26 October 2021
{: #26oct2021}
{: release-note}

CLI changelog
:   The [CLI changelog](/docs/containers?topic=containers-cs_cli_changelog) is updated for version 1.0.334. 

### 25 October 2021
{: #25oct2021}
{: release-note}

Worker node fix pack update
:   Changelog documentation is available for {{site.data.keyword.openshiftshort}} version [`4.8.15_1532_openshift`](/docs/openshift?topic=openshift-openshift_changelog#4815_1532),[`4.7.34_1537_openshift`](/docs/openshift?topic=openshift-openshift_changelog#4734_1537), [`4.6.48_1561_openshift`](/docs/openshift?topic=openshift-openshift_changelog#4648_1561), and [`3.11.524_1609_openshift`](/docs/openshift?topic=openshift-openshift_changelog#311524_1609).

### 22 October 2021
{: #22oct2021}
{: release-note}

{{site.data.keyword.cos_full_notm}} plug-in.
:   [Version 2.1.6](/docs/containers?topic=containers-cos_plugin_changelog) is released.

### 19 October 2021
{: #19oct2021}
{: release-note}

Ingress ALB changelog updates
:   Updated the [Ingress ALB changelog](/docs/containers?topic=containers-iks-release) for versions `0.49.3_1745_iks` and `1.0.3_1730_iks`.

### 18 October 2021
{: #18oct2021}
{: release-note}

New troubleshooting topic
:   See [Why does my cluster master status say it is approaching its resource limit?](/docs/containers?topic=containers-master_resource_limit). 

{{site.data.keyword.cloud_notm}} HPCS Router add-on
:   The [{{site.data.keyword.cloud_notm}} HPCS Router add-on](/docs/openshift?topic=openshift-hpcs-router-changelog) version 4.5 is deprecated.


OpenShift Data Foundation
:   The default behavior for the [ODF add-on](/docs/openshift?topic=openshift-ocs-storage-prep) has changed. Previously, when you deployed the add-on by using the CLI, the default value of the `odfDeploy` parameter was `false` and so only the add-on was installed. However, now the default value of `odfDeploy` is `true`, so when you enable the add-on, the add-on automatically creates storage resources in your cluster. 



### 13 October 2021
{: #13oct2021}
{: release-note}

CLI changelog
:   The [CLI changelog](/docs/containers?topic=containers-cs_cli_changelog) is updated for version 1.0.331. 

### 11 October 2021
{: #11oct2021}
{: release-note}



Unsupported {{site.data.keyword.openshiftshort}} version 4.5
:   {{site.data.keyword.openshiftshort}} version 4.5 is unsupported. To continue receiving important security updates and support, you must [update your cluster to a supported version](/docs/openshift?topic=openshift-openshift_versions#version_types) immediately.

Worker node fix pack update
:   Changelog documentation is available for {{site.data.keyword.openshiftshort}} version [`4.8.13_1528_openshift`](/docs/openshift?topic=openshift-openshift_changelog#4813_1528_openshift),[`4.7.32_1534_openshift`](/docs/openshift?topic=openshift-openshift_changelog#4732_1534_openshift), [`4.6.46_1558_openshift`](/docs/openshift?topic=openshift-openshift_changelog#4646_1558_openshift), and [`3.11.524_1606_openshift`](/docs/openshift?topic=openshift-openshift_changelog#311524_1606_openshift).

### 7 October 2021
{: #7oct2021}
{: release-note}

Istio add-on change log
:   [Version `1.11.3`](/docs/containers?topic=containers-istio-changelog#1113) of the Istio managed add-on is released.

Cluster autoscaler add-on.
:   [Version 1.0.4](/docs/containers?topic=containers-ca_changelog) is released.



### 6 October 2021
{: #6oct2021}
{: release-note}

{{site.data.keyword.block_storage_is_short}} add-on.
:   [Version 4.0.1_780](/docs/containers?topic=containers-vpc_bs_changelog) is released.


### 5 October 2021
{: #5oct2021}
{: release-note}

Updated supported, deprecated, and unsupported versions for strongSwan Helm chart.
:   [Upgrading or disabling the strongSwan Helm chart](/docs/openshift?topic=openshift-vpn#vpn_upgrade)


{{site.data.keyword.cloud_notm}} Image Key Synchronizer add-on changelog.
:   [Version 1.0.0_690](/docs/openshift?topic=openshift-image-key-synchronizer-changelog#1_0_0690) is released.

{{site.data.keyword.cos_full_notm}} plug-in.
:   [Version 2.1.5](/docs/containers?topic=containers-cos_plugin_changelog) is released.


## September 2021
{: #release-sep-2021}

Review the release notes for September 2021.
{: shortdesc}

### 29 September 2021
{: #29sep2021}
{: release-note}

New! OpenShift 4.8
:   You can create or [update clusters to OpenShift version 4.8](/docs/openshift?topic=openshift-openshift_versions#ocp48). With OpenShift 4.8, you get the latest OpenShift features, as well as component updates on {{site.data.keyword.openshiftlong_notm}}. For more information, [see the blog announcement](https://www.ibm.com/cloud/blog/announcements/openshift-version-48-now-available-in-red-hat-openshift-on-ibm-cloud){: external}.

Deprecated and unsupported OpenShift versions
:   With the release of OpenShift 4.8, clusters that run version 4.5 remain deprecated, with a tentative unsupported date of 10 Oct 2021. Clusters that run versions 4.3 or 4.4 are unsupported. Update your cluster to at least [version 4.6](/docs/openshift?topic=openshift-openshift_versions#ocp46) as soon as possible.

Master fix pack and worker node fix pack update
:   Change log documentation is available for OpenShift version [`4.8.11_1526_openshift` and `4.8.12_1527_openshift`](/docs/openshift?topic=openshift-openshift_changelog#4811_1526_and_4812_1527).



### 27 September 2021
{: #27sep2021}
{: release-note}

Master fix pack update
:   Change log documentation is available for {{site.data.keyword.openshiftshort}} version [`4.7.30_1532_openshift`](/docs/openshift?topic=openshift-openshift_changelog#4730_1532),[`4.6.44_1556_openshift`](/docs/openshift?topic=openshift-openshift_changelog#4644_1556), [`4.5.41_1552_openshift`](/docs/openshift?topic=openshift-openshift_changelog#4541_1552), and [`3.11.521_1604_openshift`](/docs/openshift?topic=openshift-openshift_changelog#311521_1604).


Worker node fix pack update
:   Change log documentation is available for {{site.data.keyword.openshiftshort}} version [`4.5.41_1553_openshift`](/docs/openshift?topic=openshift-openshift_changelog#4541_1553),[`4.6.45_1557_openshift`](/docs/openshift?topic=openshift-openshift_changelog#4645_1557_openshift), [`4.7.31_1533_openshift`](/docs/openshift?topic=openshift-openshift_changelog#4731_1533_openshift), and [`3.11.521_1605_openshift`](/docs/openshift?topic=openshift-openshift_changelog#311521_1605_openshift).

### 23 September 2021
{: #23sep2021}
{: release-note}

Review the release notes for 23 September 2021.
{: shortdesc}

Istio add-on change log
:   [Version `1.11.2`](/docs/containers?topic=containers-istio-changelog#1112) of the Istio managed add-on is released.

### 22 September 2021
{: #22sep2021}
{: release-note}

Review the release notes for 22 September 2021.
{: shortdesc}

Ingress ALB version change log
:   [Version `1.0.0_1699_iks`](/docs/containers?topic=containers-cluster-add-ons-changelog#1_0_0) is now available. Updates for versions [`0.48.1_1698_iks`](/docs/containers?topic=containers-cluster-add-ons-changelog#0_48_0) and [`0.43.0_1697_iks`](/docs/containers?topic=containers-cluster-add-ons-changelog#0_47_0) are available in the change log. 



### 21 September 2021
{: #21sep2021}
{: release-note}

Review the release notes for 21 September 2021.
{: shortdesc}

HPCS Router add-on
:   Version `4.5.0_861` and `4.6.0_860` of the [HPCS Router](/docs/openshift?topic=openshift-hpcs-router-changelog) add-on are available.


### 16 September 2021
{: #16sep2021}
{: release-note}

{{site.data.keyword.block_storage_is_short}} add-on  
:   Version [`4.0.0_769`](/docs/containers?topic=containers-vpc_bs_changelog) is available.





### 15 September 2021
{: #15sep2021}
{: release-note}

Review the release notes for 16 September 2021.
{: shortdesc}


OpenShift Data Foundation  
:   The OpenShift Data Foundation add-on is now generally available for {{site.data.keyword.openshiftlong}} clusters. The add-on is available for VPC, {{site.data.keyword.satelliteshort}}, and classic clusters. For more information, see [Understanding OpenShift Data Foundation](/docs/openshift?topic=openshift-ocs-storage-prep).



### 14 September 2021
{: #14sep2021}
{: release-note}

Review the release notes for 14 September 2021.
{: shortdesc}

Ingress ALB version change log
:   [Version `1.0.0_1645_iks`](/docs/containers?topic=containers-cluster-add-ons-changelog#1_0_0) is now available. Updates for versions [`0.48.1_1613_iks`](/docs/containers?topic=containers-cluster-add-ons-changelog#0_48_0) and [`0.47.0_1614_iks`](/docs/containers?topic=containers-cluster-add-ons-changelog#0_47_0) are available in the change log. 

Istio add-on change log
:   [Version `1.10.4`](/docs/containers?topic=containers-istio-changelog#1104) and [version `1.9.8`](/docs/containers?topic=containers-istio-changelog#198) of the Istio managed add-on is released.


### 13 September 2021
{: #13sep2021}
{: release-note}

Worker node fix pack update
:   Change log documentation is available for {{site.data.keyword.openshiftshort}} version [`4.5.41_1551_openshift`](/docs/openshift?topic=openshift-openshift_changelog#4541_1551),[`4.6.44_1555_openshift`](/docs/openshift?topic=openshift-openshift_changelog#4644_1555), [`4.7.29_1531_openshift`](/docs/openshift?topic=openshift-openshift_changelog#4729_1531), and [`3.11.501_1603_openshift`](/docs/openshift?topic=openshift-openshift_changelog#311501_1603).

### 9 September 2021
{: #9sep2021}
{: release-note}

Ingress ALB changelog
:   Updated the [change log](/docs/containers?topic=containers-cluster-add-ons-changelog#kube_ingress_changelog) for versions `0.48.1_1613_iks`, `0.47.0_1614_iks`, and `0.43.0_1612_iks`.



### 8 September 2021
{: #8sep2021}
{: release-note}

Review the release notes for 8 September 2021.
{: shortdesc}

HPCS Router add-on
:   Updated version changelog for the [HPCS Router](/docs/openshift?topic=openshift-hpcs-router-changelog) add-on.

### 1 September 2021
{: #1sep2021}
{: release-note}

Review the release notes for 1 September 2021.
{: shortdesc}

{{site.data.keyword.block_storage_is_short}} add-on
:   Version [`4.0`](/docs/containers?topic=containers-vpc_bs_changelog) is available.

{{site.data.keyword.cos_full_notm}} plug-in 
:   Version [`2.1.4`](/docs/containers?topic=containers-cos_plugin_changelog) is available.


## August 2021
{: #release-aug-2021}

Review the release notes for August 2021.
{: shortdesc}

### 31 August 2021
{: #31aug2021}
{: release-note}

Review the release notes for 31 August 2021.
{: shortdesc}

Istio add-on changelog
:   [Version 1.11.1](/docs/containers?topic=containers-istio-changelog#1111) of the Istio managed add-on is released.

New! Sao Paolo multizone region
:   You can now create VPC clusters in the Sao Paolo, Brazil [location](/docs/containers?topic=containers-regions-and-zones).

 VPC disk encryption on worker nodes
:   Now, you can manage the encryption for the disk on your VPC worker nodes. For more information, see [VPC worker nodes](/docs/openshift?topic=openshift-encryption#worker-encryption-vpc).

### 30 August 2021
{: #30aug2021}
{: release-note}

Review the release notes for 30 August 2021.
{: shortdesc}

Worker node fix pack update
:   Changelog documentation is available for {{site.data.keyword.openshiftshort}} version [`4.6.43_1554_openshift`](/docs/openshift?topic=openshift-openshift_changelog#4643_1554), [`4.7.24_1530_openshift`](/docs/openshift?topic=openshift-openshift_changelog#4724_1530), and [`3.11.501_1602_openshift`](/docs/openshift?topic=openshift-openshift_changelog#311501_1602).
