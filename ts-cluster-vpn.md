---

copyright:
  years: 2014, 2022
lastupdated: "2022-01-31"

keywords: openshift

subcollection: openshift
content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why does the cluster master return a VPN server error?
{: #rhoks_ts_openvpn_login}
{: support}

**Infrastructure provider**:
* ![Classic infrastructure provider icon.](images/icon-classic-2.svg) Classic
* ![VPC infrastructure provider icon.](images/icon-vpc-2.svg) VPC 


After you create or update a cluster, the master status returns a VPN server configuration error message similar to the following.
{: tsSymptoms}

```
VPN server configuration update failed. IBM Cloud support has been notified and is working to resolve this issue.
```
{: screen}


The infrastructure credentials that are associated with the resource group that the cluster is created in are missing (such as the API key owner is no longer part of the account) or missing required permissions.
{: tsCauses}


[Complete the troubleshooting guide](/docs/openshift?topic=openshift-worker_infra_errors) to check and update the infrastructure credentials that are used for the resource group.
{: tsResolve}






