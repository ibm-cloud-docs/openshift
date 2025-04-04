---

copyright:
  years: 2014, 2025
lastupdated: "2025-04-04"


keywords: openshift, route, router

subcollection: openshift

---


{{site.data.keyword.attribute-definition-list}}





# {{site.data.keyword.cloud_notm}} HPCS Router add-on change log
{: #hpcs-router-changelog}

View information for version updates to the {{site.data.keyword.cloud_notm}} HPCS Router add-on.
{: shortdesc}

* **Patch updates**: {{site.data.keyword.cloud_notm}} keeps all your add-on components up-to-date by automatically rolling out patch updates to the most recent version of the HPCS Router that is offered by {{site.data.keyword.openshiftlong_notm}}.
* **Minor version updates**: The minor version of the HPCS Router add-on matches the minor version of your {{site.data.keyword.redhat_openshift_notm}} cluster. In the CLI, you can run `ibmcloud oc cluster addon ls -c <cluster_name_or_ID>` to check the current version of your add-on, and `ibmcloud oc cluster get -c <cluster_name_or_ID>` to check the current version of your cluster.

To view a list of add-ons and the supported {{site.data.keyword.redhat_openshift_notm}} versions, see the [supported add-on versions table](/docs/openshift?topic=openshift-supported-cluster-addon-versions) or run the following command.

```sh
ibmcloud oc cluster addon versions --addon hpcs-router
```
{: pre}

## Version 4.9.0
{: #4.9.0}

### Version 4.9.0_2290, released on 14 Jul 2022
{: #4_9_0_2290}

Resolves [CVE-2022-2097](https://nvd.nist.gov/vuln/detail/CVE-2022-2097){: external}.

### Version 4.9.0_2251, released on 7 Jul 2022
{: #4_9_0_2251}

- [CVE-2021-38561](https://nvd.nist.gov/vuln/detail/CVE-2021-38561){: external}.
- [CVE-2022-21698](https://nvd.nist.gov/vuln/detail/CVE-2022-21698){: external}.
- [CVE-2022-1271](https://nvd.nist.gov/vuln/detail/CVE-2022-1271){: external}.

### Version 4.9.0_1983, released on 13 Jun 2022
{: #4_9_0_1983}

Resolves [CVE-2021-3634](https://nvd.nist.gov/vuln/detail/CVE-2021-3634){: external}.

### Version 4.9.0_1559, released on 4 May 2022
{: #4_9_0_1559}

- [CVE-2018-25032](https://nvd.nist.gov/vuln/detail/CVE-2018-25032){: external}.
- [CVE-2022-28327](https://nvd.nist.gov/vuln/detail/CVE-2022-28327){: external}.
- [CVE-2022-24675](https://nvd.nist.gov/vuln/detail/CVE-2022-24675){: external}.
- [CVE-2022-27536](https://nvd.nist.gov/vuln/detail/CVE-2022-27536){: external}.
