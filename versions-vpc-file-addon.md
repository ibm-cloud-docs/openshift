---

copyright: 
  years: 2014, 2023
lastupdated: "2023-09-25"

keywords: file, add-on, changelog

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}



# {{site.data.keyword.filestorage_vpc_full_notm}} add-on change log 
{: #versions-vpc-file-addon}

The {{site.data.keyword.filestorage_vpc_short}} cluster add-on is available in Beta for allowlisted accounts only. 
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

### Change log for version 1.1.7_49, released 14 September 2023
{: #1.1.7_is_file_relnote}

- Updates UBI image to `8.8-1037`.
- Updates Golang to `1.19.12`.
- Resolves the following CVEs: 
    - [CVE-2023-34969](https://nvd.nist.gov/vuln/detail/CVE-2023-34969){: external}, [CVE-2023-28321](https://nvd.nist.gov/vuln/detail/CVE-2023-28321){: external}, [CVE-2023-2602](https://nvd.nist.gov/vuln/detail/CVE-2023-2602){: external}, [CVE-2023-2603](https://nvd.nist.gov/vuln/detail/CVE-2023-2603){: external}, [CVE-2023-28484](https://nvd.nist.gov/vuln/detail/CVE-2023-28484){: external}, [CVE-2023-29469](https://nvd.nist.gov/vuln/detail/CVE-2023-29469){: external}, [CVE-2023-27536](https://nvd.nist.gov/vuln/detail/CVE-2023-27536){: external}, [CVE-2023-3899](https://nvd.nist.gov/vuln/detail/CVE-2023-3899){: external}, and [CVE-2023-32681](https://nvd.nist.gov/vuln/detail/CVE-2023-32681){: external}.



### Change log for version 1.1.6_41, release 28 July 2023
{: #1.1.6_is_file_relnote}

- Tiered storage classes are deprecated and will be unsupported soon. To migrate, create new PVCs and that use a `dp2` storage class and redeploy your apps.
- Updates for the VPC API compatibility changes. For more information, see the [VPC REST API change log](/docs/vpc?topic=vpc-api-change-log-beta#23-may-2023-beta)
- Adds support for `dp2` profiles.
- Updates the UBI to version `8.8-1014` to resolve the following CVEs: [CVE-2023-1667](https://nvd.nist.gov/vuln/detail/CVE-2023-1667){: external}, [CVE-2023-2283](https://nvd.nist.gov/vuln/detail/CVE-2023-2283){: external}, [CVE-2023-26604](https://nvd.nist.gov/vuln/detail/CVE-2023-26604){: external}, and [CVE-2020-24736](https://nvd.nist.gov/vuln/detail/CVE-2020-24736){: external}.
- Updates Golang to version `1.19.11` to resolve [CVE-2023-29406](https://nvd.nist.gov/vuln/detail/CVE-2023-29406){: external}.

### Change log for version 1.1, released 3 July 2023
{: #1.1_is_file_relnote}

- Updates the following sidecar images: 
    - `storage-secret-sidecar` to `v1.2.24`.
    - `csi-node-driver-registrar` to `v2.7.0`.
    - `livenessprobe` to `v2.9.0`.
    - `csi-provisioner` to `v3.4.1`.
    - `csi-resizer` to `v1.7.0`.

- Updates the UBI image `8.8-860`.
- Updates Golang to `1.19.10`.
- Resolves the following CVEs: 
    - [CVE-2023-29403](https://nvd.nist.gov/vuln/detail/CVE-2023-29403){: external},
    - [CVE-2023-29404](https://nvd.nist.gov/vuln/detail/CVE-2023-29404){: external}
    - [CVE-2023-29405](https://nvd.nist.gov/vuln/detail/CVE-2023-29405){: external}
    - [CVE-2023-29402](https://nvd.nist.gov/vuln/detail/CVE-2023-29402){: external} 
    - [CVE-2023-29400](https://nvd.nist.gov/vuln/detail/CVE-2023-29400){: external}
    - [CVE-2023-24540](https://nvd.nist.gov/vuln/detail/CVE-2023-24540){: external}
    - [CVE-2023-24539](https://nvd.nist.gov/vuln/detail/CVE-2023-24539){: external} 
    - [CVE-2022-43552](https://nvd.nist.gov/vuln/detail/CVE-2022-43552){: external}
    - [CVE-2022-3204](https://nvd.nist.gov/vuln/detail/CVE-2022-3204){: external}
    - [CVE-2023-27535](https://nvd.nist.gov/vuln/detail/CVE-2023-27535){: external}
    - [CVE-2022-36227](https://nvd.nist.gov/vuln/detail/CVE-2022-36227){: external}
    - [CVE-2022-35252](https://nvd.nist.gov/vuln/detail/CVE-2022-35252){: external}




### Change log for version 1.1-beta, released 15 May 2023
{: #1.1_beta_is_file_relnote}

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






