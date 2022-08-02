---

copyright:
  years: 2014, 2022
lastupdated: "2022-08-02"

keywords: openshift

subcollection: openshift
content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}


# Why does the cluster master return a VPN server error?
{: #rhoks_ts_openvpn_login}
{: support}

Supported infrastructure providers
:   Classic
:   VPC 


After you create or update a cluster, the master status returns a VPN server configuration error message similar to the following.
{: tsSymptoms}

```sh
VPN server configuration update failed. IBM Cloud support has been notified and is working to resolve this issue.
```
{: screen}


The infrastructure credentials that are associated with the resource group that the cluster is created in are missing (such as the API key owner is no longer part of the account) or missing required permissions.
{: tsCauses}


[Complete the troubleshooting guide](/docs/openshift?topic=openshift-worker_infra_errors) to check and update the infrastructure credentials that are used for the resource group.
{: tsResolve}






