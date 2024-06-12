---

copyright:
  years: 2024, 2024

lastupdated: "2024-06-12"


keywords: change log, version history, ALB OAuth Proxy add on

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}

# ALB OAuth Proxy add on version change log
{: #alb-oauth-proxy-add-on-change-log}

Review the version history for ALB OAuth Proxy add on.
{: shortdesc}


## Version 2.0.0
{: #alb-oauth-proxy-add-on-2.0.0}


### 2.0.0_2301, released 06 June 24
{: #alb-oauth-proxy-add-on-2.0.0_2301}

- Resolves the following CVEs: [CVE-2024-2961](https://nvd.nist.gov/vuln/detail/CVE-2024-2961){: external}.
- oauth2-proxy v7.5.0-2417
- oauth2-proxy v7.5.0-2406

### 2.0.0_2266, released 04 June 24
{: #alb-oauth-proxy-add-on-2.0.0_2266}

- Resolves the following CVEs: [CVE-2024-2961](https://nvd.nist.gov/vuln/detail/CVE-2024-2961){: external}.
- Updates Go to version `1.22.3`.
- oauth2-proxy v7.5.0-2390
- oauth2-proxy v7.5.0-2387

### 2.0.0_2250, released 08 May 24
{: #alb-oauth-proxy-add-on-2.0.0_2250}

- Resolves the following CVEs: [CVE-2024-24786](https://nvd.nist.gov/vuln/detail/CVE-2024-24786){: external}, and [CVE-2023-45288](https://nvd.nist.gov/vuln/detail/CVE-2023-45288){: external}.
- Updates Go to version `1.22.0`.
- Initial release of 2.0.0
- oauth2-proxy v7.5.0-2231
- oauth2-proxy v7.5.0-2236
- oauth2-proxy v7.5.0-2255
- oauth2-proxy v7.5.0-2356
- oauth2-proxy v7.5.0-2344
- oauth2-proxy v7.5.0-2334
- oauth2-proxy v7.5.0-2295
- oauth2-proxy v7.5.0-2291
- oauth2-proxy v7.5.0-2281


### 2.0.0_2156, released 03 April 2024
{: #2.0.0_2156}

- Resolves [CVE-2024-24786](https://nvd.nist.gov/vuln/detail/CVE-2024-24786){: external}

### 2.0.0_2063, released on 16 January 2024
{: #2.0.0_2063}

- Resolves [CVE-2023-48795](https://nvd.nist.gov/vuln/detail/CVE-2023-48795){: external}.


### 2.0.0_1901, released on 25 October 2023
{: #2.0.0_1901}

- Resolves [CVE-2023-39325](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2023-39325){: external}.

### 2.0.0_1889, released on 18 October 2023
{: #2.0.0_1889}

- [CVE-2023-4911](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2023-4911){: external}.
- [CVE-2023-4527](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2023-4527){: external}.
- [CVE-2023-4806](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2023-4806){: external}.
- [CVE-2023-4813](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2023-4813){: external}.

### 2.0.0_1843, released on 26 September 2023
{: #2.0.0_1843}

- Updates `oauth2-proxy` from 7.4.0 to 7.5.0.
- Updates `go` version to 1.21.1.
- Dependency updates.
- Resolves [CVE-2023-3978](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2023-3978){: external}.

### 2.0.0_1715, released on 9 August 2023
{: #2_0_0_1715}

- Dependency updates.

### 2.0.0_1669, released on 12 July 2023
{: #2.0.0_1669}

- Updates `go` version to 1.20.5.
- Resolves [CVE-2023-32731](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2023-32731){: external}.

### 2.0.0_1528, released on 13 April 2023
{: #2.0.0_1528}

- Adds support for the `cookie-refresh` configuration option for `oauth2-proxy`. Using this feature might require additional configuration. For more information, see [Adding App ID authentication to apps](/docs/containers?topic=containers-comm-ingress-annotations#app-id-auth).

### 2.0.0_1487, released on 1 March 2023
{: #2_0_0_1487}

- Updates `go` version to 1.20.1.
- Resolves [CVE-2022-41723](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2022-41723){: external}.

### 2.0.0_1469, released on 22 February 2023
{: #2_0_0_1469}

- Dependency updates.
- Base image changes.

### 2.0.0_1420, released on 8 February 2023
{: #2_0_0_1420}

- Updates `go` version to 1.19.5.
- Adds support for multi-Ingress configurations.

### 2.0.0_1354, released on 15 December 2022
{: #2_0_0_1354}

- Updates `go` version to 1.19.4.
- Resolves [CVE-2022-41717](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2022-41717){: external}.

### 2.0.0_1315, released on 16 November 2022.
{: #2_0_0_1315}

- Updates `oauth2-proxy` from version 7.3.0 to version 7.4.0.
- Adds support for `cookie_csrf_expire` and `cookie_csrf_per_request` configuration option for `oauth2-proxy`.

### 2.0.0_1297, released on 27 October 2022.
{: #2_0_0_1297}

Resolves [CVE-2022-32149](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2022-32149){: external}.

### 2.0.0_1265, released on 3 October 2022.
{: #2_0_0_1265}

- Updates `oauth2-proxy` from version 7.2.0 to version 7.3.0.
- Adds support for `oidc-extra-audience` configuration option for `oauth2-proxy`.
- Resolves [CVE-2022-27664](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2022-27664).

### 2.0.0_1214, released on 12 September 2022.
{: #2_0_0_1214}

Adds the `whitelist-domains` configuration option to `oauth2-proxy`.

### 2.0.0_1187, released on 7 July 2022.
{: #2_0_0_1187}

- [CVE-2022-21698](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2022-21698){: external}
- [CVE-2022-27191](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2022-27191){: external}

### 2.0.0_1064, released on 4 May 2022.
{: #2_0_0_1064}

- [CVE-2022-28327](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2022-28327){: external}
- [CVE-2022-27536](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2022-27536){: external}

### 2.0.0_1023, released on 24 March 2022.
{: #2_0_0_1023}

The add-on logic has changed. It does not add a configuration snippet annotation to the Ingress resources anymore. This change makes the add-on compatible with the default ALB configuration that disables the usage of snippet annotations.

Resolves [CVE-2022-24921](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2022-24921){: external}

### 2.0.0_999, released on 28 February 2022.
{: #2_0_0_999}

- [CVE-2022-23772](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2022-23772){: external}
- [CVE-2022-23773](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2022-23773){: external}
- [CVE-2022-23806](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2022-23806){: external}

### 2.0.0_981, released on 10 February 2022.
{: #2_0_0_981}

This version addresses an issue that causes periodic restarts for the managed OAuth2 Proxy deployments.

### 2.0.0_923, released on 26 January 2022.
{: #2_0_0_923}

- [CVE-2021-44716](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-44716){: external}
- [CVE-2021-44717](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-44717){: external}

### 2.0.0_755, released on 19 November 2021.
{: #2_0_0_755}

- [CVE-2021-41771](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-41771){: external}
- [CVE-2021-41772](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-41772){: external}

### 2.0.0_704, released on 15 September 2021.
{: #2_0_0_704}

Version 2.0.0 of the add-on supports {{site.data.keyword.containerlong_notm}} clusters 1.19 and later. Version 1.0.0 of the add-on supports {{site.data.keyword.containerlong_notm}} clusters 1.21 and earlier. If you want to upgrade your {{site.data.keyword.containerlong_notm}} cluster to 1.22 or later, you must upgrade the add-on from 1.0.0 to 2.0.0 before the cluster upgrade.


## Version 1.0.0
{: #1_0_0-oauth}

As of 16 May 2022, version 1.0.0 of the add-on is no longer supported.
{: important}

### 1.0.0_1024, released on 24 March 2022.
{: #1_0_0_1024}

Resolves [CVE-2022-24921](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2022-24921){: external}

### 1.0.0_1001, released on 28 February 2022.
{: #1_0_0_1001}

- [CVE-2022-23772](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2022-23772){: external}
- [CVE-2022-23773](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2022-23773){: external}
- [CVE-2022-23806](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2022-23806){: external}

### 1.0.0_924, released on 26 January 2022.
{: #1_0_0_924}

- [CVE-2021-44716](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-44716){: external}
- [CVE-2021-44717](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-44717){: external}

### 1.0.0_756, released on 19 November 2021.
{: #1_0_0_756}

- [CVE-2021-41771](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-41771){: external}
- [CVE-2021-41772](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-41772){: external}

### 1.0.0_684, released on 23 August 2021.
{: #1_0_0_684}

- [CVE-2021-36221](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-36221){: external}

### 1.0.0_638, released on 10 August 2021.
{: #1_0_0_638}

- [CVE-2021-34558](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-34558){: external}
- [CVE-2021-21411](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-21411){: external}
- [CVE-2021-21291](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-21291){: external}

### 1.0.0_618, released on 17 June 2021.
{: #1_0_0_618}

- [CVE-2021-31525](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-31525){: external}
- [CVE-2021-33194](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-33194){: external}

### 1.0.0_590, released on 19 April 2021.
{: #1_0_0_590}

- [CVE-2021-3121](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-3121){: external}
- [CVE-2021-28851](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-28851){: external}
- [CVE-2021-28852](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2021-28852){: external}

### 1.0.0_574, released on 30 March 2021.
{: #1_0_0_574}

- [CVE-2021-3114](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3114){: external}
- [CVE-2021-3115](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-3115){: external}
