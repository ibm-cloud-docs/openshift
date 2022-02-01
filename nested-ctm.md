---

copyright: 
  years: 2014, 2022
lastupdated: "2022-02-01"

keywords: openshift, help, network, dns, health check

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}


# Ingress health checks fail on Akamai Global Load Balancer (GLB) configurations
{: #cs_ingress_health_check_ctm}
{: support}

**Supported infrastructure provider**:
* ![Classic infrastructure provider icon.](images/icon-classic-2.svg) Classic
* <img src="images/icon-satellite.svg" alt="{{site.data.keyword.satelliteshort}} infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Satellite


When you try to include Ingress subdomains that have health checks enabled in your Akamai Global Traffic Managment (GTM) configuration, the health checks fail.
{: tsSymptoms}


Akamai Global Traffic Managment (GTM) configurations don't support nested subdomains.
{: tsCauses}

Disable the default health check for the Ingress subdomain. For more information see the `nlb-dns monitor disable` [command reference](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_nlb-dns-monitor-disable).
{: tsResolve}

```sh
ibmcloud oc nlb-dns monitor disable --cluster CLUSTER --nlb-host SUBDOMAIN 
```
{: pre}







