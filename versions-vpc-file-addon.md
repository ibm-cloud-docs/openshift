---

copyright: 
  years: 2014, 2023
lastupdated: "2023-05-18"

keywords: file, add-on, changelog

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}



# {{site.data.keyword.filestorage_vpc_full_notm}} add-on change log 
{: #versions-vpc-file-addon}

{{site.data.keyword.filestorage_vpc_short}} is available for allowlisted accounts in the Washington D.C., Dallas, Frankfurt, London, Sydney, Sao Paulo, and Tokyo regions. Contact your IBM Sales representative if you are interested in getting access.
{: preview}

{{site.data.keyword.filestorage_vpc_short}} is available in Beta. Do not use this add-on for production workloads.
{: beta} 


View information for patch updates to the {{site.data.keyword.filestorage_vpc_full_notm}} add-on in your {{site.data.keyword.openshiftlong_notm}} clusters.
{: shortdesc}

Patch updates
:   Patch updates are delivered automatically by IBM and don't contain any feature updates or changes in the supported add-on and cluster versions.

Release updates
:   Release updates contain new features for the {{site.data.keyword.filestorage_vpc_full_notm}} or changes in the supported add-on or cluster versions. You must manually apply release updates to your {{site.data.keyword.filestorage_vpc_full_notm}} add-on. To update your {{site.data.keyword.filestorage_vpc_full_notm}} add-on, see [Updating the {{site.data.keyword.filestorage_vpc_full_notm}} add-on](/docs/openshift?topic=openshift-storage-file-vpc-managing).

To view a list of add-ons and the supported cluster versions in the CLI, run the following command.
```sh
ibmcloud oc cluster addon versions --addon vpc-file-csi-driver
```
{: pre}

To view a list of add-ons and the supported cluster versions, see the [Supported cluster add-ons table](/docs/openshift?topic=openshift-supported-cluster-addon-versions).


## Version 1.1
{: #011_is_file}

### Change log for version 1.1-beta, released 15 May 2023
{: #1.1_is_file_relnote}

- Kubernetes dependencies upgraded to `1.26.4`.
- Controller pods are now deployed as `Deployment`, in previous releases pods were deployed as `Satefulsets`.
- Adds the `priorityClass` in the deployment file for controller and node pods.

## Version 1.0
{: #01_is_file}


### Change log for version 1.0, released 16 May 2023
{: #1.0_is_file_relnote}

- Updates the UBI image to `8.7-1107`.
- Updates Golang to `1.19.8`.
- Resolves the following CVEs: [CVE-2023-2453](https://nvd.nist.gov/vuln/detail/CVE-2023-2453){: external}, [CVE-2023-24537](https://nvd.nist.gov/vuln/detail/CVE-2023-24537){: external}, [CVE-2023-24538](https://nvd.nist.gov/vuln/detail/CVE-2023-24538){: external}.






