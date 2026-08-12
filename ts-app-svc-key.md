---

copyright: 
  years: 2014, 2026
lastupdated: "2026-08-12"


keywords: kubernetes, openshift

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}





# Resolving service binding errors in IBM Cloud clusters
{: #ts-app-svc-key}
{: support}

Learn how to troubleshoot service binding issues in IBM Cloud clusters when services don't support service keys, and find alternative integration methods.
{: shortdesc}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf}


When you run `ibmcloud oc cluster service bind --cluster <cluster_name> --namespace <project> --service <service_instance_name>`, you see the following message.
{: tsSymptoms}

```sh
This service doesn't support creation of keys
```
{: screen}



Some services in {{site.data.keyword.cloud_notm}}, such as {{site.data.keyword.keymanagementservicelong}} don't support the creation of service credentials, also referred to as service keys. Without the support of service keys, the service can't be bound to a cluster. To learn how to connect services, see [Connecting services to apps](/docs/account?topic=account-service_credentials).
{: tsCauses}



To integrate services that don't support service keys, check if the service provides an API that you can use to access the service directly from your app. For example, if you want to use {{site.data.keyword.keymanagementservicelong}}, see the [API reference](https://cloud.ibm.com/apidocs/key-protect){: external}.
{: tsResolve}
