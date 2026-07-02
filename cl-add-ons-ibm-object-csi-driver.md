---

copyright:
  years: 2024, 2026

lastupdated: "2026-07-02"


keywords: change log, version history, IBM Object CSI Driver

subcollection: "openshift"

---

{{site.data.keyword.attribute-definition-list}}




# IBM Object CSI Driver add-on version change log
{: #cl-add-ons-ibm-object-csi-driver}


Patch updates
:   Patch updates are delivered automatically by IBM and don't contain any feature updates or changes in the supported add-on and cluster versions.

Release updates
:   Release updates contain new features or changes in the supported add-on or cluster versions. You must manually apply release updates to your cluster autoscaler add-on.

To view a list of add-ons and the supported cluster versions, run the following command or see the [Supported cluster add-ons table](/docs/openshift?topic=openshift-supported-cluster-addon-versions).

```sh
ibmcloud oc cluster addon versions
```
{: pre}


Review the version history for IBM Object CSI Driver.
{: shortdesc}


## Version 1.0
{: #cl-add-ons-ibm-object-csi-driver-1.0}


### Version 1.0 - v1.0.23_349336907, released 03 July 2026
{: #cl-add-ons-ibm-object-csi-driver-v1023_349336907}

[Default version]{: tag-green}

- Resolves the following CVEs: [CVE-2026-2303](https://nvd.nist.gov/vuln/detail/CVE-2026-2303){: external}.
- Updates Go to version `1.26.4`.
- Added support for Cross-Regional StorageClass


### Version 1.0 - v1.0.22_348679631, released 22 June 2026
{: #cl-add-ons-ibm-object-csi-driver-v1022_348679631}

- Resolves the following CVEs: [CVE-2026-34182](https://nvd.nist.gov/vuln/detail/CVE-2026-34182){: external}, [CVE-2026-34183](https://nvd.nist.gov/vuln/detail/CVE-2026-34183){: external}, [CVE-2026-45445](https://nvd.nist.gov/vuln/detail/CVE-2026-45445){: external}, [CVE-2026-45447](https://nvd.nist.gov/vuln/detail/CVE-2026-45447){: external}, [CVE-2026-34180](https://nvd.nist.gov/vuln/detail/CVE-2026-34180){: external}, [CVE-2026-34181](https://nvd.nist.gov/vuln/detail/CVE-2026-34181){: external}, [CVE-2026-42764](https://nvd.nist.gov/vuln/detail/CVE-2026-42764){: external}, [CVE-2026-42766](https://nvd.nist.gov/vuln/detail/CVE-2026-42766){: external}, [CVE-2026-42767](https://nvd.nist.gov/vuln/detail/CVE-2026-42767){: external}, [CVE-2026-42768](https://nvd.nist.gov/vuln/detail/CVE-2026-42768){: external}, [CVE-2026-42769](https://nvd.nist.gov/vuln/detail/CVE-2026-42769){: external}, [CVE-2026-42770](https://nvd.nist.gov/vuln/detail/CVE-2026-42770){: external}, [CVE-2026-7383](https://nvd.nist.gov/vuln/detail/CVE-2026-7383){: external}, [CVE-2026-9076](https://nvd.nist.gov/vuln/detail/CVE-2026-9076){: external}, [CVE-2026-45446](https://nvd.nist.gov/vuln/detail/CVE-2026-45446){: external}, [CVE-2026-49980](https://nvd.nist.gov/vuln/detail/CVE-2026-49980){: external}, and [CVE-2026-39821](https://nvd.nist.gov/vuln/detail/CVE-2026-39821){: external}.
- Updates Go to version `1.26.4`.
- Updates rclone mounter version to 1.74.3 


### Version 1.0 - v1.0.21_333133599, released 09 June 2026
{: #cl-add-ons-ibm-object-csi-driver-v1021_333133599}

- Resolves the following CVEs: [CVE-2026-33814](https://nvd.nist.gov/vuln/detail/CVE-2026-33814){: external}, [CVE-2026-39836](https://nvd.nist.gov/vuln/detail/CVE-2026-39836){: external}, [CVE-2026-31790](https://nvd.nist.gov/vuln/detail/CVE-2026-31790){: external}, [CVE-2026-4438](https://nvd.nist.gov/vuln/detail/CVE-2026-4438){: external}, [CVE-2026-28390](https://nvd.nist.gov/vuln/detail/CVE-2026-28390){: external}, [CVE-2026-33811](https://nvd.nist.gov/vuln/detail/CVE-2026-33811){: external}, [CVE-2026-39820](https://nvd.nist.gov/vuln/detail/CVE-2026-39820){: external}, [CVE-2026-42499](https://nvd.nist.gov/vuln/detail/CVE-2026-42499){: external}, [CVE-2026-44973](https://nvd.nist.gov/vuln/detail/CVE-2026-44973){: external}, [CVE-2026-4046](https://nvd.nist.gov/vuln/detail/CVE-2026-4046){: external}, [CVE-2026-4437](https://nvd.nist.gov/vuln/detail/CVE-2026-4437){: external}, [CVE-2026-40355](https://nvd.nist.gov/vuln/detail/CVE-2026-40355){: external}, [CVE-2026-40356](https://nvd.nist.gov/vuln/detail/CVE-2026-40356){: external}, [CVE-2026-4878](https://nvd.nist.gov/vuln/detail/CVE-2026-4878){: external}, [CVE-2026-29111](https://nvd.nist.gov/vuln/detail/CVE-2026-29111){: external}, [CVE-2026-39823](https://nvd.nist.gov/vuln/detail/CVE-2026-39823){: external}, [CVE-2026-39826](https://nvd.nist.gov/vuln/detail/CVE-2026-39826){: external}, [CVE-2026-39825](https://nvd.nist.gov/vuln/detail/CVE-2026-39825){: external}, and [CVE-2026-44740](https://nvd.nist.gov/vuln/detail/CVE-2026-44740){: external}.
- Updates Go to version `1.26.4`.
- Updates rclone mounter version to 1.74.2 


### Version 1.0 - v1.0.20_333133599, released 25 May 2026
{: #cl-add-ons-ibm-object-csi-driver-v1020_333133599}

- Resolves the following CVEs: [CVE-2026-4878](https://nvd.nist.gov/vuln/detail/CVE-2026-4878){: external}, [CVE-2026-29111](https://nvd.nist.gov/vuln/detail/CVE-2026-29111){: external}, [CVE-2026-32952](https://nvd.nist.gov/vuln/detail/CVE-2026-32952){: external}, and [CVE-2026-29181](https://nvd.nist.gov/vuln/detail/CVE-2026-29181){: external}.
- Updates Go to version `1.25.9`.
- Updates rclone mounter version to 1.74.1 


### Version 1.0 - v1.0.19_333133599, released 26 April 2026
{: #cl-add-ons-ibm-object-csi-driver-v1019_333133599}

- Resolves the following CVEs: [CVE-2026-27135](https://nvd.nist.gov/vuln/detail/CVE-2026-27135){: external}, [CVE-2026-32280](https://nvd.nist.gov/vuln/detail/CVE-2026-32280){: external}, [CVE-2026-32283](https://nvd.nist.gov/vuln/detail/CVE-2026-32283){: external}, [CVE-2026-32289](https://nvd.nist.gov/vuln/detail/CVE-2026-32289){: external}, [CVE-2026-32281](https://nvd.nist.gov/vuln/detail/CVE-2026-32281){: external}, [CVE-2026-32288](https://nvd.nist.gov/vuln/detail/CVE-2026-32288){: external}, [CVE-2026-33809](https://nvd.nist.gov/vuln/detail/CVE-2026-33809){: external}, [CVE-2026-41176](https://nvd.nist.gov/vuln/detail/CVE-2026-41176){: external}, and [CVE-2026-41179](https://nvd.nist.gov/vuln/detail/CVE-2026-41179){: external}.
- Updates Go to version `1.25.9`.
- Updates rclone mounter version to 1.73.5. Fixes GHSA-xmrv-pmrh-hhx2 


### Version 1.0 - v1.0.18_320539369, released 02 April 2026
{: #cl-add-ons-ibm-object-csi-driver-v1018_320539369}

- Resolves the following CVEs: [CVE-2026-33186](https://nvd.nist.gov/vuln/detail/CVE-2026-33186){: external}.
- Updates Go to version `1.25.8`.
- Updates rclone mounter version to 1.73.3 


### Version 1.0 - v1.0.17_320539369, released 24 March 2026
{: #cl-add-ons-ibm-object-csi-driver-v1017_320539369}

- Resolves the following CVEs: [CVE-2026-27142](https://nvd.nist.gov/vuln/detail/CVE-2026-27142){: external}, [CVE-2026-27139](https://nvd.nist.gov/vuln/detail/CVE-2026-27139){: external}, [CVE-2026-1229](https://nvd.nist.gov/vuln/detail/CVE-2026-1229){: external}, and [CVE-2026-25679](https://nvd.nist.gov/vuln/detail/CVE-2026-25679){: external}.
- Updates Go to version `1.25.8`.
- Updates rclone mounter version to 1.73.2 
- Adds support for setting the quota limit for the buckets.


### Version 1.0 - v1.0.13_297764008, released 14 November 2025
{: #cl-add-ons-ibm-object-csi-driver-v1013_297764008}

- Resolves the following CVEs: [CVE-2025-58185](https://nvd.nist.gov/vuln/detail/CVE-2025-58185){: external}, [CVE-2025-58189](https://nvd.nist.gov/vuln/detail/CVE-2025-58189){: external}, [CVE-2025-61723](https://nvd.nist.gov/vuln/detail/CVE-2025-61723){: external}, [CVE-2025-61725](https://nvd.nist.gov/vuln/detail/CVE-2025-61725){: external}, and [CVE-2025-5318](https://nvd.nist.gov/vuln/detail/CVE-2025-5318){: external}.
- Updates Go to version `1.25.4`.
- Update mountOptions for existing S3FS and `rclone` storage classes for improved performance. 
