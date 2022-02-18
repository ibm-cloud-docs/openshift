---

copyright: 
  years: 2014, 2022
lastupdated: "2022-02-18"

keywords: openshift

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}


# Classic clusters: Why can't my app connect via Ingress?
{: #cs_ingress_fails}
{: support}

**Infrastructure provider**: ![Classic infrastructure provider icon.](images/icon-classic-2.svg) Classic


You exposed your app by creating an Ingress resource for your app in your classic cluster.
{: tsSymptoms}

When you tried to connect to your app by using the public IP address or Ingress subdomain, the connection failed or timed out.
{: tsCauses}


First, check that your cluster is fully deployed and has at least 2 worker nodes available per zone to ensure high availability for your router for the Ingress controller.
{: tsResolve}

```sh
ibmcloud oc worker ls --cluster <cluster_name_or_ID>
```
{: pre}

In your CLI output, make sure that the **Status** of your worker nodes displays **Ready** and that the **Machine Type** shows a flavor other than **free**.

* If your standard cluster is fully deployed and has at least 2 worker nodes per zone, but no **Ingress Subdomain** is available, see [Why does no Ingress subdomain exist after cluster creation?](/docs/containers?topic=containers-ingress_subdomain).
* For other issues, troubleshoot your Ingress setup by following the steps in [Debugging Ingress](/docs/openshift?topic=openshift-ingress-debug-roks4).




