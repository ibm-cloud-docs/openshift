---

copyright:
  years: 2024, 2025

lastupdated: "2025-07-17"


keywords: change log, version history, OpenShift AI

subcollection: "openshift"

---

{{site.data.keyword.attribute-definition-list}}




# OpenShift AI add-on version change log
{: #cl-add-ons-openshift-ai}

Review the version history for OpenShift AI.
{: shortdesc}



## Version 416
{: #cl-add-ons-openshift-ai-416}


### 416.2.3_543, released 17 July 2025
{: #cl-add-ons-openshift-ai-41623_543}

[Default version]{: tag-green}

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

### 416.0.0_424, released 21 January 2025
{: #cl-add-ons-openshift-ai-41600_424}

- Updates Go to version `1.22.10`.
- Installs Red Hat `openshift-ai` operator version `2.13.1`.
- Optionally installs NFD operator based on latest version available for channel `stable`.
- Optionally installs NVIDIA GPU operator based on latest version available for channel `stable`.
- Optionally installs Pipeline operator based on latest version available for channel `latest`.
