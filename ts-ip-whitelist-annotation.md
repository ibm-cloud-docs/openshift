---

copyright:
  years: 2022, 2023
lastupdated: "2023-07-05"

keywords: openshift, ip_whitelist, annotation

subcollection: openshift
content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}




# Why can't I use the Red Hat annotations to restrict access to the {{site.data.keyword.redhat_openshift_notm}} Console?
{: #ip_whitelist}
{: troubleshoot}
{: support}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf}

When you use the Red Hat `ip_whitelist` allowlist annotation to allow only certain source IP addresses to access the {{site.data.keyword.redhat_openshift_notm}} Console, it does not work as expected.
{: tsSymptoms}

By default, the source IP address is not preserved from the client (console web browser) through the load balancer and to the router pod. Because the source IP address isn't available when the filtering is done in the router pod, you can't use the `ip_whitelist` annotation to allow certain IP addresses to access the console.
{: tsCauses}

Do not use the Red Hat `ip_whitelist` annotation to restrict {{site.data.keyword.redhat_openshift_notm}} Console access to specific IP address or IP address ranges. Instead, use Context Based Restrictions (CBR) for this purpose.
{: tsResolve}

For more information, see [Allowing Red Hat OpenShift on IBM Cloud to access other IBM Cloud resources by using CBR](/docs/openshift?topic=openshift-cbr&interface=ui#cbr-integrations).
