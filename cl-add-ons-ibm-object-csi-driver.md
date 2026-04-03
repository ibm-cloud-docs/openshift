---

copyright:
  years: 2024, 2026

lastupdated: "2026-04-02"


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


### v1.0.18_320539369, released 02 April 2026
{: #cl-add-ons-ibm-object-csi-driver-v1018_320539369}

[Default version]{: tag-green}

- Resolves the following CVEs: [CVE-2026-33186](https://nvd.nist.gov/vuln/detail/CVE-2026-33186){: external}.
- Updates Go to version `1.25.8`.
- Updates rclone mounter version to 1.73.3 


### v1.0.17_320539369, released 24 March 2026
{: #cl-add-ons-ibm-object-csi-driver-v1017_320539369}

- Resolves the following CVEs: [CVE-2026-27142](https://nvd.nist.gov/vuln/detail/CVE-2026-27142){: external}, [CVE-2026-27139](https://nvd.nist.gov/vuln/detail/CVE-2026-27139){: external}, [CVE-2026-1229](https://nvd.nist.gov/vuln/detail/CVE-2026-1229){: external}, and [CVE-2026-25679](https://nvd.nist.gov/vuln/detail/CVE-2026-25679){: external}.
- Updates Go to version `1.25.8`.
- Updates rclone mounter version to 1.73.2 
- Adds support for setting the quota limit for the buckets.


### v1.0.13_297764008, released 14 November 2025
{: #cl-add-ons-ibm-object-csi-driver-v1013_297764008}

- Resolves the following CVEs: [CVE-2025-58185](https://nvd.nist.gov/vuln/detail/CVE-2025-58185){: external}, [CVE-2025-58189](https://nvd.nist.gov/vuln/detail/CVE-2025-58189){: external}, [CVE-2025-61723](https://nvd.nist.gov/vuln/detail/CVE-2025-61723){: external}, [CVE-2025-61725](https://nvd.nist.gov/vuln/detail/CVE-2025-61725){: external}, and [CVE-2025-5318](https://nvd.nist.gov/vuln/detail/CVE-2025-5318){: external}.
- Updates Go to version `1.25.4`.
- Update mountOptions for existing S3FS and `rclone` storage classes for improved performance. 
