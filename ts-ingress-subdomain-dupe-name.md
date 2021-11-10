---

copyright: 
  years: 2014, 2021
lastupdated: "2021-11-10"

keywords: openshift

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}


# Why does no Ingress subdomain exist after I create clusters of the same or similar name?
{: #cs_rate_limit}

**Infrastructure provider**:
* ![Classic infrastructure provider icon.](images/icon-classic-2.svg) Classic
* ![VPC infrastructure provider icon.](images/icon-vpc-2.svg) VPC
* <img src="images/icon-satellite.svg" alt="{{site.data.keyword.satelliteshort}} infrastructure provider icon" width="15" style="width:15px; border-style: none"/> {{site.data.keyword.satelliteshort}}


You create and delete a cluster multiple times, such as for automation purposes.
{: tsSymptoms}

Every time that you create the cluster, you use either the same name or a name that is very similar to previous names that you used. When you run `ibmcloud oc cluster get --cluster <cluster>`, your cluster is in a `normal` state but no **Ingress Subdomain** or **Ingress Secret** are available.


When you create and delete a cluster that uses the same name multiple times, the Ingress subdomain for that cluster in the format `<cluster_name>.<globally_unique_account_HASH>-0000.<region>.containers.appdomain.cloud` is registered and unregistered each time.
{: tsCauses}

The certificate for the subdomain is also generated and deleted each time. If you create and delete a cluster with the same name 5 times or more within 7 days, you might reach the Let's Encrypt [Duplicate Certificate rate limit](https://letsencrypt.org/docs/rate-limits/?origin_team=T4LT36D1N){: external}, because the same Ingress subdomain and certificate are registered every time that you create the cluster. Because very long cluster names are truncated to 24 characters in the Ingress subdomain for the cluster, you can also reach the rate limit if you use multiple cluster names that have the same first 24 characters.


If you need to continue testing, you can change the name of the cluster so that when you create the new cluster a new, different Ingress subdomain and secret are registered.
{: tsResolve}







