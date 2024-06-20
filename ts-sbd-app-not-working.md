---

copyright: 
  years: 2024, 2024
lastupdated: "2024-06-20"


keywords: openshift, {{site.data.keyword.openshiftlong_notm}}, secure by default, app not working, {{site.data.keyword.openshiftlong_notm}}, outbound traffic protection, 4.15, 1.30

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}


# After creating a version 4.15 cluster, my app no longer works
{: #ts-sbd-app-not-working}
{: support}

[Virtual Private Cloud]{: tag-vpc}
[4.15 and later]{: tag-red}

After creating a version 4.15 cluster, your app no longer works and you see an error message similar to the following.
{: tsSymptoms}

```sh
warning: Container container-00 is unable to start due to an error: Back-off pulling image "registry.redhat.io/rhel8/support-tools"
```
{: pre}


Applications that have external public dependencies such as image registries like `ghcr.io`, repositories like GitHub, and so on might no longer function correctly after enabling the secure by default outbound traffic protection. Secure by default clusters have all public access disabled by default.
{: tsCauses}


Review the following steps for your use case.
{: tsResolve}

## Allowing outbound access
{: #allow-outbound-ts}

Review your options for allowing all outbound access or allowing outbound access selectively. For more information, see [Managing outbound traffic protection in VPC clusters](/docs/openshift?topic=openshift-sbd-allow-outbound).

