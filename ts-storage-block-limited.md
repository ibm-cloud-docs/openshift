---

copyright: 
  years: 2023, 2023
lastupdated: "2023-11-01"

keywords: openshift, kubernetes, help, network, connectivity, target port, limited, alerts

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}





# Why does my Block Storage persistent volume show a `limited` connectivity status?
{: #block-pv-limited-connectivity}
{: support}

[Classic infrastructure]{: tag-classic-inf}

When you describe your {{site.data.keyword.blockstorageshort}} persistent volume (PV), you see a label similar to the following example.
{: tsSymptoms}

```sh
Labels: ibm.io/pv-connectivity-status: limited
```
{: screen}


The {{site.data.keyword.blockstorageshort}} driver looks for 2 target ports when you mount a PVC to a PV. If 2 target ports can't be found when mounting the volume, the `ibm.io/pv-connectivity-status: limited` label is added to the PV.
{: tsCauses}

If your PV shows a `limited` connectivity status, then only 1 target port was available at mount time. Usually, this situation is due to maintenance impacts. 
{: tsResolve}

1. Review that IBM Cloud status console for potential maintenance impacts. Do not reload or restart your deployments if your PVs have `limited` connectivity.

1. If there is no ongoing maintenance, or if the issue persists, contact support. Open a [support case](/docs/get-support?topic=get-support-using-avatar). In the case details, be sure to include any relevant log files, error messages, or command outputs..

You can also set up monitoring alerts for `limited` connected PVs. For more information, see [Setting up monitoring for `limited` connectivity PVs](/docs/openshift?topic=openshift-block_storage#storage-block-vpc-limited-monitoring).
{: tip}

