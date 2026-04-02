---

copyright:
  years: 2024, 2026

lastupdated: "2026-04-02"


keywords: change log, version history, Confidential containers

subcollection: "openshift"

---

{{site.data.keyword.attribute-definition-list}}




# Confidential containers
{: #cl-confidential-containers}


Review the version history for Confidential containers.
{: shortdesc}


## Version 20260319-02
{: #cl-confidential-containers-20260319-02}


### 20260319-02, released 19 March 2026
{: #cl-confidential-containers-20260319-02}

- Fixing systemd startup error in the image provided as feedback.
- `rhel9-podvm-hardened-20260319-02.qcow2`


## Version 20260318-10
{: #cl-confidential-containers-20260318-10}


### 20260318-10, released 18 March 2026
{: #cl-confidential-containers-20260318-10}

- Correcting image with ssh disabled. Previous still had SSH.
- `rhel9-podvm-hardened-20260318-10.qcow2`


## Version 20260312-07-hardened
{: #cl-confidential-containers-20260312-07-hardened}


### 20260312-07-hardened, released 12 March 2026
{: #cl-confidential-containers-20260312-07-hardened}

[Default version]{: tag-green}

- Initial production release of hardened PodVM images for Confidential Containers
- RHEL 9.7 based image with enhanced security hardening
- SSH access disabled for maximum security
- Supports IBM Cloud VPC infrastructure
- Compatible with OpenShift sandboxed containers operator
- Recommended for production workloads requiring strict security posture
- `rhel9-podvm-hardened-20260312-07.qcow2`


## Version 20260303-01
{: #cl-confidential-containers-20260303-01}


### 20260303-01, released 03 March 2026
{: #cl-confidential-containers-20260303-01}

[Default version]{: tag-green}

- Initial production release of standard PodVM images for Confidential Containers
- RHEL 9.7 based image with SSH access enabled for debugging
- Supports IBM Cloud VPC infrastructure
- Compatible with OpenShift sandboxed containers operator
- `rhel9-podvm-20260303-01.qcow2`

