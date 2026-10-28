---

copyright:
  years: 2024, 2026

lastupdated: "2026-10-28"


keywords: change log, version history, Object Storage plug in

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}




# Object Storage plug in
{: #cl-object-storage-plug-in}


Review the version history for Object Storage plug in.
{: shortdesc}


## Version 2.2
{: #cl-object-storage-plug-in-2.2}


### 28 October 2026, Version 2.2 - 2.2.60
{: #cl-object-storage-plug-in-2260}

- Resolves the following CVEs: [CVE-2026-14456](https://nvd.nist.gov/vuln/detail/cve-2026-14456){: external}, [CVE-2026-14457](https://nvd.nist.gov/vuln/detail/cve-2026-14457){: external}, [CVE-2026-18798](https://nvd.nist.gov/vuln/detail/cve-2026-18798){: external}, [CVE-2026-54874](https://nvd.nist.gov/vuln/detail/cve-2026-54874){: external}, [CVE-2026-63072](https://nvd.nist.gov/vuln/detail/cve-2026-63072){: external}, [CVE-2026-63073](https://nvd.nist.gov/vuln/detail/cve-2026-63073){: external}, [CVE-2026-63074](https://nvd.nist.gov/vuln/detail/cve-2026-63074){: external}, [CVE-2026-63075](https://nvd.nist.gov/vuln/detail/cve-2026-63075){: external}, [CVE-2026-63076](https://nvd.nist.gov/vuln/detail/cve-2026-63076){: external}, [CVE-2026-75803](https://nvd.nist.gov/vuln/detail/cve-2026-75803){: external}, [CVE-2026-84782](https://nvd.nist.gov/vuln/detail/cve-2026-84782){: external}, [CVE-2026-18477](https://nvd.nist.gov/vuln/detail/cve-2026-18477){: external}, [CVE-2026-18508](https://nvd.nist.gov/vuln/detail/cve-2026-18508){: external}, [CVE-2026-5704](https://nvd.nist.gov/vuln/detail/cve-2026-5704){: external}, [CVE-2026-41991](https://nvd.nist.gov/vuln/detail/cve-2026-41991){: external}, [CVE-2026-41992](https://nvd.nist.gov/vuln/detail/cve-2026-41992){: external}, [CVE-2026-56391](https://nvd.nist.gov/vuln/detail/cve-2026-56391){: external}, [CVE-2026-56392](https://nvd.nist.gov/vuln/detail/cve-2026-56392){: external}, [CVE-2026-103111](https://nvd.nist.gov/vuln/detail/cve-2026-103111){: external}, [CVE-2026-86145](https://nvd.nist.gov/vuln/detail/cve-2026-86145){: external}, [CVE-2026-89161](https://nvd.nist.gov/vuln/detail/cve-2026-89161){: external}, [CVE-2026-89157](https://nvd.nist.gov/vuln/detail/cve-2026-89157){: external}, [CVE-2026-89158](https://nvd.nist.gov/vuln/detail/cve-2026-89158){: external}, [CVE-2026-89156](https://nvd.nist.gov/vuln/detail/cve-2026-89156){: external}, [CVE-2026-89160](https://nvd.nist.gov/vuln/detail/cve-2026-89160){: external}, [CVE-2026-18374](https://nvd.nist.gov/vuln/detail/cve-2026-18374){: external}, [CVE-2026-19542](https://nvd.nist.gov/vuln/detail/cve-2026-19542){: external}, [CVE-2026-6368](https://nvd.nist.gov/vuln/detail/cve-2026-6368){: external}, [CVE-2026-6791](https://nvd.nist.gov/vuln/detail/cve-2026-6791){: external}, [CVE-2026-77117](https://nvd.nist.gov/vuln/detail/cve-2026-77117){: external}, [CVE-2026-80489](https://nvd.nist.gov/vuln/detail/cve-2026-80489){: external}, [CVE-2026-114406](https://nvd.nist.gov/vuln/detail/cve-2026-114406){: external}, [CVE-2026-78669](https://nvd.nist.gov/vuln/detail/cve-2026-78669){: external}, [CVE-2026-97031](https://nvd.nist.gov/vuln/detail/cve-2026-97031){: external}, [CVE-2026-78659](https://nvd.nist.gov/vuln/detail/cve-2026-78659){: external}, [CVE-2026-78660](https://nvd.nist.gov/vuln/detail/cve-2026-78660){: external}, [CVE-2026-94440](https://nvd.nist.gov/vuln/detail/cve-2026-94440){: external}, [CVE-2026-56866](https://nvd.nist.gov/vuln/detail/cve-2026-56866){: external}, [CVE-2026-78663](https://nvd.nist.gov/vuln/detail/cve-2026-78663){: external}, [CVE-2026-94439](https://nvd.nist.gov/vuln/detail/cve-2026-94439){: external}, [CVE-2026-94448](https://nvd.nist.gov/vuln/detail/cve-2026-94448){: external}, [CVE-2026-97032](https://nvd.nist.gov/vuln/detail/cve-2026-97032){: external}, [CVE-2026-111943](https://nvd.nist.gov/vuln/detail/cve-2026-111943){: external}, and [CVE-2026-97030](https://nvd.nist.gov/vuln/detail/cve-2026-97030){: external}.
- Updates Go to version `1.26.10`.
- Updated driver daemonset pods to use initContainer to copy required files on the host 
- Shell removed from provider and provisioner 
- Helm v4 compatibility for the ibmc plugin


### 27 August 2026, Version 2.2 - 2.2.59
{: #cl-object-storage-plug-in-2259}

- Resolves the following CVEs: [CVE-2026-33818](https://nvd.nist.gov/vuln/detail/cve-2026-33818){: external}, [CVE-2026-39821](https://nvd.nist.gov/vuln/detail/cve-2026-39821){: external}, [CVE-2026-46600](https://nvd.nist.gov/vuln/detail/cve-2026-46600){: external}, [CVE-2026-56853](https://nvd.nist.gov/vuln/detail/cve-2026-56853){: external}, [CVE-2026-56858](https://nvd.nist.gov/vuln/detail/cve-2026-56858){: external}, [CVE-2026-56859](https://nvd.nist.gov/vuln/detail/cve-2026-56859){: external}, [CVE-2026-56860](https://nvd.nist.gov/vuln/detail/cve-2026-56860){: external}, and [CVE-2026-56862](https://nvd.nist.gov/vuln/detail/cve-2026-56862){: external}.
- Updates Go to version `1.26.6`.
- WORKER_OS detection issue on RHEL 9 due to unquoted tr syntax in ibmc.sh 


### 15 August 2026, Version 2.2 - 2.2.58
{: #cl-object-storage-plug-in-2258}

- Resolves the following CVEs: [CVE-2026-41989](https://nvd.nist.gov/vuln/detail/cve-2026-41989){: external}, and [CVE-2026-13757](https://nvd.nist.gov/vuln/detail/cve-2026-13757){: external}.
- Updates Go to version `1.26.5`.


### 28 July 2026, Version 2.2 - 2.2.57
{: #cl-object-storage-plug-in-2257}

- Resolves the following CVEs: [CVE-2026-42505](https://nvd.nist.gov/vuln/detail/cve-2026-42505){: external}, [CVE-2026-54369](https://nvd.nist.gov/vuln/detail/cve-2026-54369){: external}, [CVE-2026-54370](https://nvd.nist.gov/vuln/detail/cve-2026-54370){: external}, [CVE-2026-5928](https://nvd.nist.gov/vuln/detail/cve-2026-5928){: external}, [CVE-2026-6238](https://nvd.nist.gov/vuln/detail/cve-2026-6238){: external}, [CVE-2026-5435](https://nvd.nist.gov/vuln/detail/cve-2026-5435){: external}, and [GHSA-hrxh-6v49-42gf](https://github.com/advisories/ghsa-hrxh-6v49-42gf){: external}.
- Updates Go to version `1.26.5`.


### 03 July 2026, Version 2.2 - 2.2.56
{: #cl-object-storage-plug-in-2256}

- Resolves the following CVEs: [CVE-2025-5278](https://nvd.nist.gov/vuln/detail/cve-2025-5278){: external}, and [CVE-2026-5450](https://nvd.nist.gov/vuln/detail/cve-2026-5450){: external}.
- Updates Go to version `1.25.11`.


### 22 June 2026, Version 2.2 - 2.2.55
{: #cl-object-storage-plug-in-2255}

- Resolves the following CVEs: [CVE-2026-34182](https://nvd.nist.gov/vuln/detail/cve-2026-34182){: external}, [CVE-2026-34183](https://nvd.nist.gov/vuln/detail/cve-2026-34183){: external}, [CVE-2026-45445](https://nvd.nist.gov/vuln/detail/cve-2026-45445){: external}, [CVE-2026-45447](https://nvd.nist.gov/vuln/detail/cve-2026-45447){: external}, [CVE-2026-34180](https://nvd.nist.gov/vuln/detail/cve-2026-34180){: external}, [CVE-2026-34181](https://nvd.nist.gov/vuln/detail/cve-2026-34181){: external}, [CVE-2026-42764](https://nvd.nist.gov/vuln/detail/cve-2026-42764){: external}, [CVE-2026-42766](https://nvd.nist.gov/vuln/detail/cve-2026-42766){: external}, [CVE-2026-42767](https://nvd.nist.gov/vuln/detail/cve-2026-42767){: external}, [CVE-2026-42768](https://nvd.nist.gov/vuln/detail/cve-2026-42768){: external}, [CVE-2026-42769](https://nvd.nist.gov/vuln/detail/cve-2026-42769){: external}, [CVE-2026-42770](https://nvd.nist.gov/vuln/detail/cve-2026-42770){: external}, [CVE-2026-7383](https://nvd.nist.gov/vuln/detail/cve-2026-7383){: external}, [CVE-2026-9076](https://nvd.nist.gov/vuln/detail/cve-2026-9076){: external}, [CVE-2026-45446](https://nvd.nist.gov/vuln/detail/cve-2026-45446){: external}, and [CVE-2026-2303](https://nvd.nist.gov/vuln/detail/cve-2026-2303){: external}.
- Updates Go to version `1.25.11`.


### 05 June 2026, Version 2.2 - 2.2.54
{: #cl-object-storage-plug-in-2254}

- Resolves the following CVEs: [CVE-2026-4438](https://nvd.nist.gov/vuln/detail/cve-2026-4438){: external}, [CVE-2026-4046](https://nvd.nist.gov/vuln/detail/cve-2026-4046){: external}, [CVE-2026-4437](https://nvd.nist.gov/vuln/detail/cve-2026-4437){: external}, and [CVE-2026-28390](https://nvd.nist.gov/vuln/detail/cve-2026-28390){: external}.
- Updates Go to version `1.25.11`.
