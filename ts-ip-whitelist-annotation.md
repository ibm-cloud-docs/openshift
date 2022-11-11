---

copyright:
  years: 2022, 2022
lastupdated: "2022-11-11"

keywords: openshift

subcollection: openshift
content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}



# Why can't I use the `ip_whitelist` annotation to restrict access to the {{site.data.keyword.redhat_openshift_notm}} Console?
{: #ip_whitelist}
{: troubleshoot}
{: support}

Supported infrastructure providers
:   Classic
:   VPC

When you use the Red Hat `ip_whitelist` annotation to allow only certain source IPs to access the {{site.data.keyword.redhat_openshift_notm}} Console, it does not work as expected.
{: tsSymptoms}

By default, the source IP is not preserved from the client (console web browser) through the load balancer and to the router pod. This means you can't use the `ip_whitelist` annotation to allow certain IPs to access the console because the source IP isn't available when the filtering is done in the router pod.
{: tsCauses}

Do not use the Red Hat `ip_whitelist` annotation to restrict {{site.data.keyword.redhat_openshift_notm}} Console access to specific IP or IP ranges. Instead, use Context Based Restrictions (CBR) for this purpose.
{: tsResolve}

For more information, see [Allowing Red Hat OpenShift on IBM Cloud to access other IBM Cloud resources by using CBR](/docs/openshift?topic=openshift-cbr&interface=ui#cbr-integrations).
