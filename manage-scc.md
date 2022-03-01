---

copyright: 
  years: 2014, 2022
lastupdated: "2022-03-01"

keywords: openshift

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}


# Managing security and compliance with {{site.data.keyword.redhat_openshift_notm}}
{: #manage-security-compliance}

{{site.data.keyword.openshiftlong}} is integrated with the {{site.data.keyword.compliance_short}} to help you manage security and compliance for your organization.
{: shortdesc}

With the {{site.data.keyword.compliance_short}}, you can:

* Monitor for controls and goals that pertain to {{site.data.keyword.openshiftlong_notm}}.
* Define rules for {{site.data.keyword.openshiftlong_notm}} that can help to standardize resource configuration.

## Monitoring security and compliance posture with {{site.data.keyword.redhat_openshift_notm}}
{: #monitor-clusters}

As a security or compliance focal, you can use the {{site.data.keyword.openshiftlong_notm}} [goals](#x2117978){: term} to help ensure that your organization is adhering to the external and internal standards for your industry. By using the {{site.data.keyword.compliance_short}} to validate the resource configurations in your account against a [profile](#x2034950){: term}, you can identify potential issues as they arise.
{: shortdesc}

all the goals for {{site.data.keyword.openshiftlong_notm}} are added to the {{site.data.keyword.cloud_notm}} Best Practices Controls 1.0 profile but can also be mapped to other profiles.
{: note}

To start monitoring your resources, check out [Getting started with {{site.data.keyword.compliance_short}}](/docs/security-compliance?topic=security-compliance-getting-started).

### Available goals for {{site.data.keyword.redhat_openshift_notm}}
{: #clusters-available-goals}

Review the following goals for {{site.data.keyword.openshiftlong_notm}}.
{: shortdesc}


- **Check whether {{site.data.keyword.redhat_openshift_notm}} worker nodes are updated to the latest image to ensure patching of vulnerabilities.** You can review the worker node version by selecting your cluster in the [{{site.data.keyword.redhat_openshift_notm}} clusters console](https://cloud.ibm.com/kubernetes/clusters?platformType=openshift){: external} or in the command line by running `ibmcloud oc worker ls -c <cluster_name_or_ID>`. For more information, see the [Version changelog](/docs/openshift?topic=openshift-openshift_changelog).
- **Check whether {{site.data.keyword.redhat_openshift_notm}} clusters are accessible only by using private cloud service endpoints.** You can enable the private cloud service endpoint only for VPC clusters. Review which cloud service endpoints are enabled by selecting your cluster in the [{{site.data.keyword.redhat_openshift_notm}} clusters console](https://cloud.ibm.com/kubernetes/clusters?platformType=openshift){: external} or in the command line by running `ibmcloud oc cluster get -c <cluster_name_or_ID>`. For more information, see the [Example scenarios for VPC cluster network setup](/docs/openshift?topic=openshift-plan_vpc_basics#vpc-workeruser-master).
- **Check whether your {{site.data.keyword.redhat_openshift_notm}} cluster has image pull secrets enabled.** To verify that your cluster has the default image pull secrets, [log in](/docs/openshift?topic=openshift-access_cluster), run `oc get secrets -n default` and look for the `all-icr-io` secret. To create the image pull images to {{site.data.keyword.registrylong_notm}} in your cluster, see [Updating existing clusters to use the API key image pull secret
](/docs/openshift?topic=openshift-registry#imagePullSecret_migrate_api_key).
- **Check whether {{site.data.keyword.redhat_openshift_notm}} clusters are enabled with {{site.data.keyword.monitoringlong_notm}}.** For more information, see [Forwarding cluster and app metrics to {{site.data.keyword.monitoringlong_notm}}](/docs/openshift?topic=openshift-health-monitor#openshift_monitoring).
- **Check whether {{site.data.keyword.redhat_openshift_notm}} clusters are enabled with {{site.data.keyword.la_full_notm}}.** For more information, see [Forwarding cluster and app logs to {{site.data.keyword.la_full_notm}}](/docs/openshift?topic=openshift-health#openshift_logging).
- **Check whether {{site.data.keyword.redhat_openshift_notm}} Ingress is configured only with TLS v1.2 for all inbound traffic.** For more information, see [About Ingress](/docs/openshift?topic=openshift-ingress-about-roks4).
- **Check whether the {{site.data.keyword.redhat_openshift_notm}} version is up-to-date.** You can review the cluster version by selecting your cluster in the [{{site.data.keyword.redhat_openshift_notm}} clusters console](https://cloud.ibm.com/kubernetes/clusters?platformType=openshift){: external} or in the command line by running `ibmcloud oc cluster get -c <cluster_name_or_ID>`. For more information, see the [Version information and update actions](/docs/openshift?topic=openshift-openshift_versions).






