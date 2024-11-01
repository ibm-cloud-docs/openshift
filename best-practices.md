---

copyright: 
  years: 2024, 2024
lastupdated: "2024-11-01"


keywords: openshift, {{site.data.keyword.openshiftlong_notm}}, best practices
subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}


# Best practices for {{site.data.keyword.openshiftlong_notm}}
{: #best-practices-service}
{: support}

## Keep your cluster environment up to date
{: #bp-1}

Check monthly for available security and operating system patches to [update your worker nodes](/docs/openshift?topic=openshift-update#worker_node).

Make sure to [update your cluster](/docs/openshift?topic=openshift-update) regularly to remain on a supported version {{site.data.keyword.redhat_openshift_notm}}.

## Keep your command line tools up to date
{: #bp-2}

In the command line, you are notified when updates to the `ibmcloud` CLI and plug-ins are available. Be sure to keep your CLI up-to-date so that you can use all available commands and options.

Make sure that [your `oc` CLI](/docs/openshift?topic=openshift-cli-install) client matches the same Kubernetes version as your cluster server. [Kubernetes does not support](https://kubernetes.io/releases/version-skew-policy/){: external} `oc` client versions that are 2 or more versions apart from the server version (n +/- 2).

## Document your environment architecture
{: #bp-3}

Maintaining up-to-date documentation and diagrams can help when debugging issues. For more information, see [Documenting your environment architecture](/docs/openshift?topic=openshift-document-environment).

## Subscribe to RSS
{: #bp-4}

You can receive documentation release notes for {{site.data.keyword.openshiftlong_notm}} via RSS. For more information, see [Subscribing to an RSS feed](/docs/openshift?topic=openshift-best-practices-service#bp-4).
