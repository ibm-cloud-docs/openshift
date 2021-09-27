---

copyright: 
  years: 2014, 2021
lastupdated: "2021-09-27"

keywords: openshift, roks

subcollection: openshift

---



{{site.data.keyword.attribute-definition-list}}


# Setting Kubernetes API priority and fairness
{: #kubeapi-priority}

Your {{site.data.keyword.openshiftlong}} clusters have default settings in place to process simultaneous requests to the API server and prevent traffic overload. You can configure your own flow schema and priority levels for requests that are made to the API server of your clusters. For more information, see [API priority and fairness](https://kubernetes.io/docs/concepts/cluster-administration/flow-control/){: external} in the Kubernetes documentation.
{: shortdesc}

For example, you might have a user or namespace that runs your critical apps in prod. You can create a flow schema and priority so that your critical apps have a higher priority for the API server to fulfill their requests than other apps in the cluster.

The Kubernetes API priority and feature gate is enabled in clusters that run {{site.data.keyword.openshiftshort}} version 4.6 or later.
{: note}

## Reviewing default flow schema and priority levels
{: #kubeapi-default-priority}

{{site.data.keyword.openshiftlong_notm}} sets certain default flow schema and priority levels in addition to the default settings from Kubernetes.
{: shortdesc}

You can create your own flow schema and priorities, but do not modify the default settings. Unexpected results might occur in your cluster when you modify API request priorities.
{: important}

Before you begin: [Access your {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-access_cluster).

1. List the flow schemas in your cluster.
    ```
    oc get flowschemas
    ```
    {: pre} 

2. Review the details of a particular flow schema to understand the scope of the flow schema, including which resources can make prioritized API requests, what type of API requests can be made, and what objects the requests can modify.
    ```
    oc describe flowschema <flow-schema-name>
    ```
    {: pre}

{{site.data.keyword.openshiftlong_notm}} sets the following flow schemas:
* `apiserver-health`
* `calico-system-service-accounts`
* `ibm-system-service-accounts`
* `tigera-operator-service-accounts`





