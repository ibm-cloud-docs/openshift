---

copyright: 
  years: 2014, 2022
lastupdated: "2022-05-06"

keywords: openshift

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}


# Why does binding a service to a cluster results in service not found error?
{: #ts-app-svc-bind-not-found}
{: support}

**Infrastructure provider**:
* ![Classic](../icons/classic.svg "Classic") Classic
* ![VPC](../icons/vpc.svg "VPC") VPC


When you run `ibmcloud oc cluster service bind --cluster <cluster_name> --namespace <project> --service <service_instance_name>`, you see the following message.
{: tsSymptoms}

```
Binding service to a namespace...
FAILED

The specified IBM Cloud service could not be found. If you just created the service, wait a little and then try to bind it again. To view available IBM Cloud service instances, run 'ibmcloud service list'. (E0023)
```
{: screen}


To bind services to a cluster, you must have the Cloud Foundry developer user role for the space where the service instance is provisioned.
{: tsCauses}

In addition, you must have the {{site.data.keyword.cloud_notm}} IAM Editor platform access to {{site.data.keyword.containerlong_notm}}. To access the service instance, you must be logged in to the space where the service instance is provisioned.



**As a user in the cluster:**
{: tsResolve}

1. Log in to {{site.data.keyword.cloud_notm}}.
    ```sh
    ibmcloud login
    ```
    {: pre}

2. Target the org and the space where the service instance is provisioned.
    ```sh
    ibmcloud target -o <org> -s <space>
    ```
    {: pre}

3. Verify that you are in the right space by listing your service instances.
    ```sh
    ibmcloud service list
    ```
    {: pre}

4. Try binding the service again. If you get the same error, then contact the account administrator and verify that you have sufficient permissions to bind services (see the following account admin steps).

**As the account admin:**

1. Verify that the user who experiences this problem has [Editor permissions for {{site.data.keyword.containerlong_notm}}](/docs/openshift?topic=openshift-users#checking-perms).

2. Verify that the user who experiences this problem has the [Cloud Foundry developer role for the space](/docs/account?topic=account-mngcf#update_cf_access) where the service is provisioned.

3. If the correct permissions exists, try assigning a different permission and then re-assigning the required permission.

4. Wait a few minutes, then let the user try to bind the service again.

5. If this does not resolve the problem, then the {{site.data.keyword.cloud_notm}} IAM permissions are out of sync and you can't resolve the issue yourself. [Contact IBM support](/docs/get-support?topic=get-support-using-avatar) by opening a support case. Make sure to provide the cluster ID, the user ID, and the service instance ID.
    1. Retrieve the cluster ID.
        ```sh
        ibmcloud oc cluster ls
        ```
        {: pre}

    2. Retrieve the service instance ID.
        ```sh
        ibmcloud service show <service_name> --guid
        ```
        {: pre}








