---

copyright: 
  years: 2014, 2021
lastupdated: "2021-10-04"

keywords: openshift, roks, rhoks, rhos

subcollection: openshift
content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}



# Why can't I install a new strongSwan Helm chart release?
{: #cs_strongswan_release}

**Infrastructure provider**: ![Classic infrastructure provider icon.](images/icon-classic-2.svg) Classic


You modify your strongSwan Helm chart and try to install your new release by running `helm install vpn iks-charts/strongswan -f config.yaml`. However, you see the following error:
{: tsSymptoms}

```
Error: release vpn failed: deployments.extensions "vpn-strongswan" already exists
```
{: screen}


This error indicates that the previous release of the strongSwan chart was not completely uninstalled.
{: tsCauses}

Delete and re-install the Helm chart.
{: tsResolve}

1. Delete the previous chart release.
    ```sh
    helm uninstall vpn -n <project>
    ```
    {: pre}

2. Delete the deployment for the previous release. Deletion of the deployment and associated pod takes up to 1 minute.
    ```sh
    oc delete deploy vpn-strongswan
    ```
    {: pre}

3. Verify that the deployment has been deleted. The deployment `vpn-strongswan` does not appear in the list.
    ```sh
    oc get deployments
    ```
    {: pre}

4. Re-install the updated strongSwan Helm chart with a new release name.
    ```sh
    helm install vpn iks-charts/strongswan -f config.yaml
    ```
    {: pre}






