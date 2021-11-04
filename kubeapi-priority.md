---

copyright: 
  years: 2014, 2021
lastupdated: "2021-11-04"

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

| Flow schema | Resources that requests come from | Priority level |
| ----------- | --------- | -------------- |
| `apiserver-health` | Kubernetes API server health resources | Custom priority level for these resources |
| `calico-system-service-accounts` | Resources in the `calico-system` namespace that use a service account in the namespace | Same priority as `kube-system` namespace service accounts |
| `ibm-system-service-accounts` | Resources in the `ibm-system` namespace that use a service account in the namespace | Same priority as `kube-system` namespace service accounts |
| `tigera-operator-service-accounts` | Resources in the `tigera-operator` namespace that use a service account in the namespace | Same priority as `kube-system` namespace service accounts |
{: caption="Default flow schema and priority levels" caption-side="top"}
{: summary="The rows are read from left to right. The flow schema is listed in the first column, the resources that the requests come from are listed in the second column, and the priority level is listed in the third column."}

You can create your own flow schema and priorities, but do not modify the default settings. Unexpected results might occur in your cluster when you modify API request priorities.
{: important}

Follow the steps to review the flow schemas and priority levels set by {{site.data.keyword.openshiftlong_notm}}.

1. List all flow schemas in your cluster, including those set by {{site.data.keyword.openshiftlong_notm}}, and their corresponding priority levels .
    ```sh
    oc get flowschemas
    ```
    {: pre} 


2. Review the details of a particular flow schema including which resources can make prioritized API requests, what type of API requests can be made, and what objects the requests can modify.
    ```sh
    oc describe flowschema <flow-schema-name>
    ```
    {: pre}










