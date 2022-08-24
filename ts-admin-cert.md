---

copyright: 
  years: 2022, 2022
lastupdated: "2022-08-24"

keywords: certificate, secret, create certificate, troubleshoot certificate, troubleshoot secret

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}



# Why can't I create a new admin certificate?
{: #ts_admin-cert}
{: troubleshoot}
{: support}


When you try to create a new admin certificate, you see an error message similar to the following example.
{: tsSymptoms}

```sh
You have reached the maximum number of admin certificates. To create a new admin certificate, you must remove an existing one by revoking a user's IAM admin permissions and then removing their entry from the `ibm-admin-cert` ClusterRoleBinding.
```
{: screen}

You have reached the limit of 50 admin certificates per cluster. 
{: tsCauses}

You must remove an existing admin certificate before you can add a new one.
{: tsResolve}

To complete the following tasks, you must have the **Administrator** IAM access role for the cluster. 

1. Log in to the CLI. 

2. [Remove the user's IAM access permissions](/docs/account?topic=cli-ibmcloud_commands_iam).

3. Set the context for your cluster. Include the `--admin` option.

    ```sh
    ibmcloud oc cluster config --cluster mycluster --admin
    ```
    {: pre}

4. Edit the `ibm-admin-cert` ClusterRoleBinding file. The following command opens an editor in your terminal window. 

    ```sh
    oc edit clusterrolebinding ibm-admin-cert
    ```
    {: pre}

5. In the `ibm-admin-cert` ClusterRoleBinding file, find the admin certificate to remove. If you logged in with a service ID, the name of the entry contains `Service-ID-XX`, with `XX` as the service ID to remove. Otherwise, the name of the entry contains `IBMid-XX` in the name, with `XX` as the user ID to remove. 

    The following entries show examples to remove. 

    ```sh
    - apiGroup: rbac.authorization.k8s.io
    kind: User
    name: iam-ServiceId-XXX-admin-<DATE>
    ```
    {: screen}

    ```sh
    - apiGroup: rbac.authorization.k8s.io
    kind: User
    name: IBMid-YYY-admin-<DATE>
    ```
    {: screen}

6. Try again to create the admin certificate. 
    

 
