---

copyright:
  years: 2024, 2026

lastupdated: "2026-04-27"


keywords: change log, version history, OpenShift AI

subcollection: "openshift"

---

{{site.data.keyword.attribute-definition-list}}




# OpenShift AI add-on version change log
{: #cl-add-ons-openshift-ai}


Patch updates
:   Patch updates are delivered automatically by IBM and don't contain any feature updates or changes in the supported add-on and cluster versions.

Release updates
:   Release updates contain new features or changes in the supported add-on or cluster versions. You must manually apply release updates to your cluster autoscaler add-on.

To view a list of add-ons and the supported cluster versions, run the following command or see the [Supported cluster add-ons table](/docs/openshift?topic=openshift-supported-cluster-addon-versions).

```sh
ibmcloud oc cluster addon versions
```
{: pre}


Review the version history for OpenShift AI.
{: shortdesc}


## Version 419
{: #cl-add-ons-openshift-ai-419}


### v419.0.0_333601315, released 26 April 2026
{: #cl-add-ons-openshift-ai-v41900_333601315}

- Resolves the following CVEs: [CVE-2026-25679](https://nvd.nist.gov/vuln/detail/CVE-2026-25679){: external}, [CVE-2026-33211](https://nvd.nist.gov/vuln/detail/CVE-2026-33211){: external}, [CVE-2026-33186](https://nvd.nist.gov/vuln/detail/CVE-2026-33186){: external}, and [CVE-2026-27139](https://nvd.nist.gov/vuln/detail/CVE-2026-27139){: external}.
- Updates Go to version `1.25.9`.
- Installs Red Hat `openshift-ai` operator version `3.3.0`.
- Optionally installs NFD operator based on latest version available for channel `stable`.
- Optionally installs NVIDIA GPU operator based on latest version available for channel `stable`.
- Optionally installs Pipeline operator based on latest version available for channel `latest`.


## Version 418
{: #cl-add-ons-openshift-ai-418}


### v418.1.0_320919095, released 03 March 2026
{: #cl-add-ons-openshift-ai-v41810_320919095}

[Default version]{: tag-green}

- Resolves the following CVEs: [CVE-2025-61727](https://nvd.nist.gov/vuln/detail/CVE-2025-61727){: external}, [CVE-2025-61729](https://nvd.nist.gov/vuln/detail/CVE-2025-61729){: external}, [CVE-2025-61726](https://nvd.nist.gov/vuln/detail/CVE-2025-61726){: external}, [CVE-2025-61730](https://nvd.nist.gov/vuln/detail/CVE-2025-61730){: external}, [CVE-2025-68121](https://nvd.nist.gov/vuln/detail/CVE-2025-68121){: external}, [CVE-2026-0861](https://nvd.nist.gov/vuln/detail/CVE-2026-0861){: external}, [CVE-2025-15281](https://nvd.nist.gov/vuln/detail/CVE-2025-15281){: external}, and [CVE-2026-0915](https://nvd.nist.gov/vuln/detail/CVE-2026-0915){: external}.
- Updates Go to version `1.25.7`.
- Installs Red Hat `openshift-ai` operator version `2.25.2`.


### v418.0.0_295927267, released 11 November 2025
{: #cl-add-ons-openshift-ai-v41800_295927267}

- Resolves the following CVEs: [CVE-2025-23266](https://nvd.nist.gov/vuln/detail/CVE-2025-23266){: external}, and [CVE-2025-23267](https://nvd.nist.gov/vuln/detail/CVE-2025-23267){: external}.
- Updates Go to version `1.25.3`.
- Installs Red Hat `openshift-ai` operator version `2.22.2`.
- Optionally installs NFD operator based on latest version available for channel `stable`.
- Optionally installs NVIDIA GPU operator based on latest version available for channel `stable`.
- Optionally installs Pipeline operator based on latest version available for channel `latest`.


## Version 417
{: #cl-add-ons-openshift-ai-417}


### v417.1.0_320919116, released 03 March 2026
{: #cl-add-ons-openshift-ai-v41710_320919116}

[Default version]{: tag-green}

- Resolves the following CVEs: [CVE-2025-61727](https://nvd.nist.gov/vuln/detail/CVE-2025-61727){: external}, [CVE-2025-61729](https://nvd.nist.gov/vuln/detail/CVE-2025-61729){: external}, [CVE-2025-61726](https://nvd.nist.gov/vuln/detail/CVE-2025-61726){: external}, [CVE-2025-61730](https://nvd.nist.gov/vuln/detail/CVE-2025-61730){: external}, [CVE-2025-68121](https://nvd.nist.gov/vuln/detail/CVE-2025-68121){: external}, [CVE-2026-0861](https://nvd.nist.gov/vuln/detail/CVE-2026-0861){: external}, [CVE-2025-15281](https://nvd.nist.gov/vuln/detail/CVE-2025-15281){: external}, and [CVE-2026-0915](https://nvd.nist.gov/vuln/detail/CVE-2026-0915){: external}.
- Updates Go to version `1.25.7`.
- Installs Red Hat `openshift-ai` operator version `2.25.2`.


### 417.0.4_300761316, released 27 November 2025
{: #cl-add-ons-openshift-ai-41704_300761316}

- Resolves the following CVEs: [CVE-2025-23266](https://nvd.nist.gov/vuln/detail/CVE-2025-23266){: external}, [CVE-2025-23267](https://nvd.nist.gov/vuln/detail/CVE-2025-23267){: external}, [CVE-2025-47906](https://nvd.nist.gov/vuln/detail/CVE-2025-47906){: external}, [CVE-2025-61724](https://nvd.nist.gov/vuln/detail/CVE-2025-61724){: external}, [CVE-2025-47912](https://nvd.nist.gov/vuln/detail/CVE-2025-47912){: external}, [CVE-2025-61723](https://nvd.nist.gov/vuln/detail/CVE-2025-61723){: external}, [CVE-2025-58189](https://nvd.nist.gov/vuln/detail/CVE-2025-58189){: external}, and [CVE-2025-58185](https://nvd.nist.gov/vuln/detail/CVE-2025-58185){: external}.
- Updates Go to version `1.25.3`.


### 417.0.2_672, released 07 October 2025
{: #cl-add-ons-openshift-ai-41702_672}

- Resolves the following CVEs: [CVE-2025-10725](https://nvd.nist.gov/vuln/detail/CVE-2025-10725){: external}.
- Updates Go to version `1.24.4`.
- This build fixes the security issue found with Red Hat OpenShift AI operator where low-privileged attacker with access to an authenticated account could potentially escalate their access to a full cluster administrator 
- Installs Red Hat `openshift-ai` operator version `2.22.2`.


### 417.0.0_533, released 19 August 2025
{: #cl-add-ons-openshift-ai-41700_533}

- Updates Go to version `1.23.11`.
- Installs Red Hat `openshift-ai` operator version `2.22.0`.
- Optionally installs NFD operator based on latest version available for channel `stable`.
- Optionally installs NVIDIA GPU operator based on latest version available for channel `stable`.
- Optionally installs Pipeline operator based on latest version available for channel `latest`.


## Version 416
{: #cl-add-ons-openshift-ai-416}


### 416.3.1_300541549, released 27 November 2025
{: #cl-add-ons-openshift-ai-41631_300541549}

- Resolves the following CVEs: [CVE-2025-23266](https://nvd.nist.gov/vuln/detail/CVE-2025-23266){: external}, [CVE-2025-23267](https://nvd.nist.gov/vuln/detail/CVE-2025-23267){: external}, [CVE-2025-47906](https://nvd.nist.gov/vuln/detail/CVE-2025-47906){: external}, [CVE-2025-61724](https://nvd.nist.gov/vuln/detail/CVE-2025-61724){: external}, [CVE-2025-47912](https://nvd.nist.gov/vuln/detail/CVE-2025-47912){: external}, [CVE-2025-61723](https://nvd.nist.gov/vuln/detail/CVE-2025-61723){: external}, [CVE-2025-58189](https://nvd.nist.gov/vuln/detail/CVE-2025-58189){: external}, and [CVE-2025-58185](https://nvd.nist.gov/vuln/detail/CVE-2025-58185){: external}.
- Updates Go to version `1.25.3`.


### 416.3.0_671, released 07 October 2025
{: #cl-add-ons-openshift-ai-41630_671}

- Resolves the following CVEs: [CVE-2025-10725](https://nvd.nist.gov/vuln/detail/CVE-2025-10725){: external}.
- Updates Go to version `1.24.4`.
- This build fixes the security issue found with Red Hat OpenShift AI operator where low-privileged attacker with access to an authenticated account could potentially escalate their access to a full cluster administrator 
- Installs Red Hat `openshift-ai` operator version `2.22.2`.


### 416.2.5_598, released 12 September 2025
{: #cl-add-ons-openshift-ai-41625_598}

- Resolves the following CVEs: [CVE-2025-8058](https://nvd.nist.gov/vuln/detail/CVE-2025-8058){: external}.
- Updates Go to version `1.24.4`.


### 416.2.3_543, released 17 July 2025
{: #cl-add-ons-openshift-ai-41623_543}

- Resolves the following CVEs: [CVE-2025-4673](https://nvd.nist.gov/vuln/detail/CVE-2025-4673){: external}, and [CVE-2025-4802](https://nvd.nist.gov/vuln/detail/CVE-2025-4802){: external}.
- Updates Go to version `1.23.11`.
- This build fixes the issue with workbench creation faced in Red Hat OpenShift AI 2.19.0 
- Installs Red Hat `openshift-ai` operator version `2.19.1`.


### 416.2.2_537, released 23 June 2025
{: #cl-add-ons-openshift-ai-41622_537}

- Resolves the following CVEs: [CVE-2025-4802](https://nvd.nist.gov/vuln/detail/CVE-2025-4802){: external}.
- Updates Go to version `1.23.10`.
- Installs Red Hat `openshift-ai` operator version `2.19.0`.


### 416.1.2_495, released 25 April 2025
{: #cl-add-ons-openshift-ai-41612_495}

- Resolves the following CVEs: [CVE-2025-22871](https://nvd.nist.gov/vuln/detail/CVE-2025-22871){: external}, [CVE-2025-0395](https://nvd.nist.gov/vuln/detail/CVE-2025-0395){: external}, and [CVE-2025-22871](https://nvd.nist.gov/vuln/detail/CVE-2025-22871){: external}.
- Updates Go to version `1.23.8`.


### 416.1.1_491, released 16 April 2025
{: #cl-add-ons-openshift-ai-41611_491}

- Updates Go to version `1.23.8`.
- Installs Red Hat `openshift-ai` operator version `2.16.2`.


### 416.1.0_486, released 27 March 2025
{: #cl-add-ons-openshift-ai-41610_486}

- Resolves the following CVEs: [CVE-2025-22868](https://nvd.nist.gov/vuln/detail/CVE-2025-22868){: external}.
- Updates Go to version `1.23.7`.
- Installs Red Hat `openshift-ai` operator version `2.16.1`.


### 416.0.1_474, released 05 March 2025
{: #cl-add-ons-openshift-ai-41601_474}

- Resolves the following CVEs: [CVE-2024-45338](https://nvd.nist.gov/vuln/detail/CVE-2024-45338){: external}.
- Updates Go to version `1.23.6`.


### v416.4.0_320919164, released 03 March 2025
{: #cl-add-ons-openshift-ai-v41640_320919164}

[Default version]{: tag-green}

- Resolves the following CVEs: [CVE-2025-61727](https://nvd.nist.gov/vuln/detail/CVE-2025-61727){: external}, [CVE-2025-61729](https://nvd.nist.gov/vuln/detail/CVE-2025-61729){: external}, [CVE-2025-61726](https://nvd.nist.gov/vuln/detail/CVE-2025-61726){: external}, [CVE-2025-61730](https://nvd.nist.gov/vuln/detail/CVE-2025-61730){: external}, [CVE-2025-68121](https://nvd.nist.gov/vuln/detail/CVE-2025-68121){: external}, [CVE-2026-0861](https://nvd.nist.gov/vuln/detail/CVE-2026-0861){: external}, [CVE-2025-15281](https://nvd.nist.gov/vuln/detail/CVE-2025-15281){: external}, and [CVE-2026-0915](https://nvd.nist.gov/vuln/detail/CVE-2026-0915){: external}.
- Updates Go to version `1.25.7`.
- Installs Red Hat `openshift-ai` operator version `2.25.2`.


### 416.0.0_424, released 21 January 2025
{: #cl-add-ons-openshift-ai-41600_424}

- Updates Go to version `1.22.10`.
- Installs Red Hat `openshift-ai` operator version `2.13.1`.
- Optionally installs NFD operator based on latest version available for channel `stable`.
- Optionally installs NVIDIA GPU operator based on latest version available for channel `stable`.
- Optionally installs Pipeline operator based on latest version available for channel `latest`.
