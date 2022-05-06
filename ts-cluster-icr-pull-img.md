---

copyright: 
  years: 2014, 2022
lastupdated: "2022-05-06"

keywords: openshift

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}


# Why can't the cluster pull images from {{site.data.keyword.registrylong_notm}} during creation?
{: #ts_image_pull_create}
{: support}

**Infrastructure provider**:
* ![Classic](../icons/classic.svg "Classic") Classic
* ![VPC](../icons/vpc.svg "VPC") VPC


When you created a cluster, you received an error message similar to the following.
{: tsSymptoms}


```sh
Your cluster can't pull images from the {{site.data.keyword.registrylong_notm}} 'icr.io' domains because an IAM access policy could not be created. Make sure that you have the IAM Administrator platform access role to {{site.data.keyword.registrylong_notm}}. Then, create an image pull secret with IAM credentials to the registry by running 'ibmcloud ks cluster pull-secret apply'.
```
{: screen}


During cluster creation, a service ID is created for your cluster and assigned the **Reader** service access policy to {{site.data.keyword.registrylong_notm}}.
{: tsCauses}

Then, an API key for this service ID is generated and stored in [an image pull secret](/docs/openshift?topic=openshift-registry#cluster_registry_auth) to authorize the cluster to pull images from {{site.data.keyword.registrylong_notm}}.

To successfully assign the **Reader** service access policy to the service ID during cluster creation, you must have the **Administrator** platform access policy to {{site.data.keyword.registrylong_notm}}.
{: tsResolve}

Steps:
1. Make sure that the account owner gives you the **Administrator** role to {{site.data.keyword.registrylong_notm}}.
    ```sh
    ibmcloud iam user-policy-create <your_user_email> --service-name container-registry --roles Administrator
    ```
    {: pre}

2. [Use the `ibmcloud oc cluster pull-secret apply` command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_cluster_pull_secret_apply) to re-create an image pull secret with the appropriate registry credentials.






