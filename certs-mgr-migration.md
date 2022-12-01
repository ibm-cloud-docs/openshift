---

copyright:

  years: 2022, 2022
lastupdated: "2022-12-01"

keywords: certificate manager, certificates, secrets, migration, secrets manager

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}


# Migrating from {{site.data.keyword.cloudcerts_long_notm}} to {{site.data.keyword.secrets-manager_full_notm}}
{: #certs-mgr-migration}

With the deprecation of {{site.data.keyword.cloudcerts_long}}, you can now manage certificates with {{site.data.keyword.secrets-manager_short}}. For a comparison between the two services and details on migrating your resources, see [Migrating certificates from Certificate Manager](/docs/secrets-manager?topic=secrets-manager-migrate-from-certificate-manager#migrate-process). 
{: shortdesc}

Support for {{site.data.keyword.cloudcerts_short}} in {{site.data.keyword.openshiftlong_notm}} clusters is set to end in late 2022, and any remaining {{site.data.keyword.cloudcerts_short}} instances are set to be deleted on 31 Dec 2022. Secrets in deleted {{site.data.keyword.cloudcerts_short}} are written directly to the cluster. If you do not migrate your secrets and set a default {{site.data.keyword.secrets-manager_short}}, your secrets are written only to the cluster and not to any manager instance.
{: note}

## Setting up your {{site.data.keyword.secrets-manager_short}} instance
{: #certs-mgr_setup}

Follow the steps to set up {{site.data.keyword.secrets-manager_short}} in your cluster.
{: shortdesc}

**Supported infrastructure providers**: 
- Classic
- VPC

The steps to migrate to {{site.data.keyword.secrets-manager_short}} involves regenerating your secrets, which is rate-limited to five times per week. Follow the steps in this document carefully, as repeating them might cause you to reach the limit before you finish the migration.
{: important}

### Step 1: Enable service-to-service communication
{: #certs-mgr_setup_s2s }

Integrating {{site.data.keyword.secrets-manager_short}} with your {{site.data.keyword.redhat_openshift_notm}} cluster requires service-to-service communication authorization. Follow the steps below to set up the authorization. For additional info, see [Integrations for {{site.data.keyword.secrets-manager_short}}](/docs/secrets-manager?topic=secrets-manager-integrations#create-authorization).
{: shortdesc}
 
1. In the {{site.data.keyword.cloud_notm}} console, click **Manage** > **Access (IAM)**.
2. Click **Authorizations**.
3. Click **Create**.
4. In the **Source service** list, select **Kubernetes Service**.
5. Select the option to scope the access to **All resources**.
6. In the **Target service** list, select **{{site.data.keyword.secrets-manager_short}}**.
7. Select the option to scope the access to **All resources**. 
8. In the **Service access** section, check the **Manager** option. 
9. Click **Authorize**. 

### Step 2: Creating a {{site.data.keyword.secrets-manager_short}} instance
{: #certs-mgr_setup_create}

To create a {{site.data.keyword.secrets-manager_short}} instance in the CLI or the UI, refer to the {{site.data.keyword.secrets-manager_short}} documentation. It might take several minutes for the {{site.data.keyword.secrets-manager_short}} instance to fully provision.
{: shortdesc}

- [Create a {{site.data.keyword.secrets-manager_short}} instance in CLI](/docs/secrets-manager?topic=secrets-manager-create-instance&interface=cli).
- [Create a {{site.data.keyword.secrets-manager_short}} instance in the UI](/docs/secrets-manager?topic=secrets-manager-create-instance&interface=ui).

When you create a {{site.data.keyword.secrets-manager_short}} instance, it is not provisioned directly in your cluster. You must register your new {{site.data.keyword.secrets-manager_short}} instance to your cluster in the next step. 
{: note}

### Step 3: Registering your {{site.data.keyword.secrets-manager_short}} instance to your cluster
{: #certs-mgr_setup_register}

Follow the steps to register your {{site.data.keyword.secrets-manager_short}} instance to your cluster.
{: shortdesc}

1. Get the CRN of the {{site.data.keyword.secrets-manager_short}} instance. In the output, the CRN is in the **ID** row. 

    ```sh
    ibmcloud resource service-instance <instance_name>
    ```
    {: pre}

    Example output.

    ```sh
    Name:                  my-secrets-manager-instance 
    ID:                    crn:v1:bluemix:public:secrets-manager:us-south:a/1aa111aa1a11111aaa1a1111aa1aa111:111a1111-11a1-111a-1111-1a1a1a1111a1::
    GUID:                  111a1111-11a1-111a-1111-1a1a1a1111a1 
    Location:              us-south   
    Service Name:          secrets-manager   
    Service Plan Name:     standard   
    Resource Group Name:   default   
    State:                 active   
    Type:                  service_instance   
    Sub Type:                 
    Created at:            2022-06-08T12:46:45Z   
    Created by:            user@ibm.com   
    Updated at:            2022-06-08T12:54:45Z 
    ```
    {: screen}

2. Register the instance to your cluster. Specify the instance CRN found in the previous step.

    If you want to register an instance to a cluster and also [set it as the default instance](#certs-mgr_setup_default), include the `--is-default` option. Otherwise, you can set a default instance with the `ibmcloud oc ingress instance set` command.
    {: tip}

    ```sh
    ibmcloud oc ingress instance register --cluster <cluster_name_or_id> --crn <instance_crn> [--is-default]
    ```
    {: pre}


3. Verify that the {{site.data.keyword.secrets-manager_short}} instance was registered to the cluster. 

    ```sh
    ibmcloud oc ingress instance ls --cluster <cluster_name_or_id>
    ```
    {: pre}

    Example output.

    ```sh
    Name                                Type              Is Default   Status    Secret Group   CRN   
    my-secrets-manager-instance         secrets-manager   false        created   default        crn:v1:bluemix:public:secrets-manager:us-south:a/1aa111aa1a11111aaa1a1111aa1aa111:111a1111-11a1-111a-1111-1a1a1a1111a1::   
    ```
    {: screen}

You can specify a {{site.data.keyword.secrets-manager_short}} instance and a secret group when you [create a cluster](/docs/containers?topic=containers-clusters&interface=cli) with the [`ibmcloud oc cluster create classic`](/docs/containers?topic=containers-kubernetes-service-cli&interface=cli#cs_cluster_create) or [`ibmcloud oc cluster create vpc-gen2`](/docs/containers?topic=containers-kubernetes-service-cli&interface=cli#cli_cluster-create-vpc-gen2) commands. Use the `--sm-instance` option to register an instance to the cluster and the `--sm-group` option to specify a secret group that can access the secrets on the cluster.
{: tip} 


### Step 4: Set a default {{site.data.keyword.secrets-manager_short}} instance and regenerate your secrets
{: #certs-mgr_setup_default}

When you set a default {{site.data.keyword.secrets-manager_short}} instance, all new Ingress subdomain certificates are stored in that instance.
{: shortdesc}

1. Run the command to set the new default instance. You can optionally specify a [secret group](/docs/secrets-manager?topic=secrets-manager-secret-groups) that is allowed access to the secrets in the instance. 

    ```sh
    ibmcloud oc ingress instance default set --cluster <cluster_name_or_id> --name <instance_name> --secret-group <secret_group_id>
    ```
    {: pre}

2. Regenerate your secrets. Any secrets that are managed by IBM, such as your default Ingress secrets, are uploaded to the new default instance. These secrets are automatically updated and the CRN is changed to reference the {{site.data.keyword.secrets-manager_short}} instance.

    1. List the nlb-dns subdomains in your cluster.

        ```sh
        ibmcloud oc nlb-dns ls --cluster <cluster_name_or_id>
        ```
        {: pre}
  
    2. For each subdomain in your cluster, run the command to regenerate your IBM-managed secrets. This updates the CRN of these secrets to reference the CRN of the default {{site.data.keyword.secrets-manager_short}} instance.

        Regenerating your secrets is rate-limited to five times per week. Follow the steps in this document carefully, as repeating them might cause you to reach the limit. If you do not regenerate your secrets, or if you have reached the limit, your secrets are uploaded to your {{site.data.keyword.secrets-manager_short}} instance at the next renewal cycle. 
        {: important}


        ```sh
        ibmcloud oc nlb-dns secret regenerate --cluster <cluster_name_or_id> --nlb-subdomain <nlb_subdomain>
        ```
        {: pre}


    3. Verify that your default Ingress secrets regenerated. In the output, the CRN of the default Ingress secrets should contain `secrets-manager`. Note that some of your secret CRNs might contain `cloudcerts` instead. These secrets are updated in the next step. 

        It might take several minutes for your secrets to regenerate. During this process, the **Status** column in the output says `regenerating` or `creating`. The status switches to `created` when the regeneration is complete. 
        {: note}

        ```sh
        ibmcloud oc ingress secret ls --cluster <cluster_name_or_id>
        ```
        {: pre}

        Example output.

        ```sh
        Name                                         Namespace           CRN                                                                                                                                                                  Expires On                 Domain                                                                           Status    Type   
        secret-11111aa1a1a11aa1111111a11a1a11a-000  default   crn:v1:bluemix:public:secrets-manager:us-south:a/1aa111aa1a11111aaa1a1111aa1aa111:111a1111-11a1-111a-1111-1a1a1a1111a1:secret:a111aa11-11a1-1111-a111-11a11aa111a1   2022-12-21T19:52:29+0000   secret-11111aa1a1a11aa1111111a11a1a11a-000.us-south.containers.appdomain.cloud   created   TLS   
        secret-22222aa2a2a22aa2222222a22a2a22a-000  default   crn:v1:bluemix:public:secrets-manager:us-south:a/2aa222aa2a22222aaa2a2222aa2aa222:222a2222-22a2-222a-2222-2a2a2a2a2:secret:a222aa22-22a2-2222-a222-22a22aa222a2   2022-12-21T19:52:29+0000   secret-22222aa2a2a22aa2222222a22a2a22a-000.us-south.containers.appdomain.cloud   created   TLS  
        secret-11111aa1a1a11aa1111111a11a1a11a-000  istio-system   crn:v1:bluemix:public:cloudcerts:us-south:a/1aa111aa1a11111aaa1a1111aa1aa111:111a1111-11a1-111a-1111-1a1a1a1111a1:secret:a111aa11-11a1-1111-a111-11a11aa111a1  
        ```
        {: screen}

### Step 5: Update the CRNs of secrets that are not managed by IBM
{: #certs-mgr_setup_crn}

 In the previous step, you regenerated your IBM-managed secrets, including your default Ingress secrets, and updated their CRN values. If you have secrets that are not managed by IBM, such as secrets you created in a different namespace, and they reference the CRN of a regenerated Ingress secret, you must update them so the CRNs match. 

 **Example scenario**: You have a default, IBM-managed Ingress secret in the `default` namespace. You run the **`ibmcloud oc ingress secret create`** command and reference the CRN of the default Ingress secret to mirror the secret in the `istio-system` namespace. This new secret is not managed by IBM, but its CRN matches the CRN of the Ingress secret in the `default` namespace. Later, you set a default {{site.data.keyword.secrets-manager_short}} instance and regenerate the default Ingress secret, which changes its CRN. The CRN of the secret in the `istio-system` namespace no longer matches the CRN of the default Ingress secret, so you must update it to match. 

To check whether a secret is managed by IBM Cloud, run `ibmcloud oc ingress secret get` to view the details of the secret. In the output, if **User Managed** is marked **false**, the secret is managed by IBM Cloud. If it is marked **true**, the secret is not managed by IBM Cloud.
{: tip}

If you do not change the CRN of your non-IBM managed secrets, they do not automatically update. In this case, you are responsible for regularly updating these secrets with the [`ibmcloud oc ingress secret update`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_ingress_secret_update) command.
{: important}

Follow these steps to update the CRN values.

1. List the secrets in your cluster. For each secret, check the CRN in the output. If a secret's CRN contains `cloudcerts`, it must be updated. Note the domain of the secret. 

    ```sh
    ibmcloud oc ingress secret ls --cluster <cluster_name_or_id>
    ```
    {: pre}

    Example output.

    ```sh
    Name                                         Namespace           CRN                                                                                                                                                                  Expires On                 Domain                                                                           Status    Type   
    secret-11111aa1a1a11aa1111111a11a1a11a-000  default   crn:v1:bluemix:public:secrets-manager:us-south:a/1aa111aa1a11111aaa1a1111aa1aa111:111a1111-11a1-111a-1111-1a1a1a1111a1:secret:a111aa11-11a1-1111-a111-11a11aa111a1   2022-12-21T19:52:29+0000   secret-11111aa1a1a11aa1111111a11a1a11a-000.us-south.containers.appdomain.cloud   created   TLS   
    secret-22222aa2a2a22aa2222222a22a2a22a-000  default   crn:v1:bluemix:public:secrets-manager:us-south:a/2aa222aa2a22222aaa2a2222aa2aa222:222a2222-22a2-222a-2222-2a2a2a2a2:secret:a222aa22-22a2-2222-a222-22a22aa222a2   2022-12-21T19:52:29+0000   secret-22222aa2a2a22aa2222222a22a2a22a-000.us-south.containers.appdomain.cloud   created   TLS  
    secret-11111aa1a1a11aa1111111a11a1a11a-000  default   crn:v1:bluemix:public:cloudcerts:us-south:a/1aa111aa1a11111aaa1a1111aa1aa111:111a1111-11a1-111a-1111-1a1a1a1111a1:secret:a111aa11-11a1-1111-a111-11a11aa111a1   2022-12-21T19:52:29+0000   secret-11111aa1a1a11aa1111111a11a1a11a-000.us-south.containers.appdomain.cloud   created   TLS  
    ```
    {: screen}

2. In the same output, find the regenerated secret, indicated by `secrets-manager` in the CRN, that has the same domain as the secret that must be updated. Save the CRN of this secret.

3. For the secret that must be updated, run the command to change the CRN. Specify the CRN saved in the previous step. 

    ```sh
    ibmcloud oc ingress secret update --cluster <cluster_name_or_id> --name <secret_name> --namespace <namespace> --cert-crn <new_crn>
    ```
    {: pre}

### Step 6: Unregister your {{site.data.keyword.cloudcerts_short}} instance
{: #certs-mgr_unregister}

After you have migrated your secrets to {{site.data.keyword.secrets-manager_short}}, unregister your {{site.data.keyword.cloudcerts_short}} from your cluster.
{: shortdesc}

1. List the manager instances in your cluster and note the name of the {{site.data.keyword.cloudcerts_short}} instance you want to remove. In the output, the {{site.data.keyword.cloudcerts_short}} instances list `cloudcerts` in the **Type** column.

    ```sh
    ibmcloud oc ingress instance ls --cluster <cluster_name_or_id>
    ```
    {: pre}

2. Unregister the instance.

    ```sh
    ibmcloud oc ingress instance unregister --name <cloud_certs_instance> --cluster <cluster_name_or_id>
    ```
    {: pre}


### Step 7: Optional. Delete the {{site.data.keyword.cloudcerts_short}} instance.
{: #certs-mgr_delete}

Follow the steps to delete the {{site.data.keyword.cloudcerts_short}} instance. If you do not delete the instance now, it is automatically deleted when {{site.data.keyword.cloudcerts_short}} becomes unsupported in December 2022.
{: shortdesc}

1. In the {{site.data.keyword.cloud_notm}} console, find and click on the {{site.data.keyword.cloudcerts_short}} instance in the **Resources** list. 
2. Click **Actions**>**Delete Service**.
3. Click **OK**.


## Migrating your secrets without using {{site.data.keyword.secrets-manager_short}}
{: #certs-mgr_alt}

If you are migrating your secrets off {{site.data.keyword.cloudcerts_short}}, but do not want to use {{site.data.keyword.secrets-manager_short}}, you can write your secrets directly to your cluster. Make sure to read the [Migration FAQ](#certs-mgr_migration_faq) section to understand how your secrets must be handled if they are not stored in a {{site.data.keyword.secrets-manager_short}} instance. 
{: shortdesc}

Follow the steps to migrate your secrets without creating a {{site.data.keyword.secrets-manager_short}} instance.

1. List the manager instances in your cluster and note the name of the {{site.data.keyword.cloudcerts_short}} instance you want to remove.

    ```sh
    ibmcloud oc ingress instance ls --cluster <cluster_name_or_id>
    ```
    {: pre}

2. Unregister the instance from your cluster.

    ```sh
    ibmcloud oc ingress instance unregister --name <cloud_certs_instance> --cluster <cluster_name_or_id>
    ```
    {: pre}

3. Manually regenerate your secrets to remove them from the {{site.data.keyword.cloudcerts_short}} instance.

   1. List the nlb-dns subdomains in your cluster.

       ```sh
       ibmcloud oc nlb-dns ls --cluster <cluster_name_or_id>
       ```
       {: pre}
  
   2. For each subdomain in your cluster, run the command to regenerate the secrets.

       Regenerating your secrets is rate-limited to five times per week. Follow the steps in this document carefully, as repeating them might cause you to reach the limit. If you do not regenerate your secrets, or if you have reached the limit, your secrets are uploaded to your {{site.data.keyword.secrets-manager_short}} instance at the next renewal cycle.
       {: important}

       ```sh
       ibmcloud oc nlb-dns secret regenerate --cluster <cluster_name_or_id> --nlb-subdomain <nlb_subdomain>
       ```
       {: pre}

4. Verify that the secrets are removed from the {{site.data.keyword.cloudcerts_short}} instance. List the secrets in your cluster and check that the value in the **CRN** column contains `NO_DEFAULT_INSTANCE`. 

    ```sh
    ibmcloud oc ingress secret ls --cluster <cluster_name_or_id>
    ```
    {: pre}

    Example output.

    ```sh
    Name                                         Namespace           CRN                                                                                                                                                                  Expires On                 Domain                                                                           Status    Type   
    secret-11111aa1a1a11aa1111111a11a1a11a-000  default   NO_DEFAULT_INSTANCE   2022-12-21T19:52:29+0000   secret-11111aa1a1a11aa1111111a11a1a11a-000.us-south.containers.appdomain.cloud   created   TLS   
    secret-22222aa2a2a22aa2222222a22a2a22a-000  default   NO_DEFAULT_INSTANCE   2022-12-21T19:52:29+0000   secret-22222aa2a2a22aa2222222a22a2a22a-000.us-south.containers.appdomain.cloud   created   TLS   
    ```
    {: screen}


5. Optional. Follow the steps to [delete the {{site.data.keyword.cloudcerts_short}} instance](#certs-mgr_delete). If you do not delete the instance now, it is automatically deleted when {{site.data.keyword.cloudcerts_short}} becomes unsupported in December 2022.



## Migration FAQ
{: #certs-mgr_migration_faq}

Keep the following points in mind when migrating from {{site.data.keyword.cloudcerts_short}} to {{site.data.keyword.secrets-manager_short}}.
{: shortdesc}

What functionality can I gain with {{site.data.keyword.secrets-manager_short}}?
:   With {{site.data.keyword.secrets-manager_short}}, you can:
    - Create managed Kubernetes secrets with Ingress TLS certificates included.
    - Create Kubernetes secrets of any type by using the CRN of any {{site.data.keyword.secrets-manager_short}} instance you own.
    - Automatically update your secrets in your cluster on a regular basis.
    - Track the expiration dates of your certificates from the {{site.data.keyword.cloud_notm}} console.
    - Control who has access to your secrets by creating secret groups for approved users.

Are secrets that are stored in a registered {{site.data.keyword.secrets-manager_short}} instance automatically updated?
:   Yes. If you have a {{site.data.keyword.secrets-manager_short}} instance registered to your cluster, the secrets on the cluster are automatically updated with the values from {{site.data.keyword.secrets-manager_short}} once a day. These updates are made using the value of the the secret from the corresponding CRN.

Are my secrets automatically updated if I do not create and register a {{site.data.keyword.secrets-manager_short}} instance?
:    If you do not have a {{site.data.keyword.secrets-manager_short}} instance registered to your cluster, your default Ingress secrets continue to update automatically every 90 days and are applied to your cluster. However, any secrets you created that *reference* the default Ingress secret are not automatically updated. 
:    **Example scenario**: You have a default Ingress certificate in the `default` namespace. You run the **`ibmcloud oc ingress secret create`** command and reference the CRN of the default Ingress certificate to mirror the certificate in the `istio-system` namespace. Without a {{site.data.keyword.secrets-manager_short}} instance, the default Ingress certificate in the `default` namespace automatically updates. However, you are responsible for regularly updating the certificate in the `istio-system` namespace with the **`ibmcloud oc ingress secret update`** command. 

I created secrets that reference a default Ingress certificate, but I have not created and registered a {{site.data.keyword.secrets-manager_short}} instance and have not migrated my secrets from {{site.data.keyword.cloudcerts_short}}. Can I still manually update these secrets with the **`ibmcloud oc ingress secret`** commands?
:   Yes. The `ibmcloud oc ingress secret` commands support secrets with {{site.data.keyword.cloudcerts_long_notm}} CRNs until 31 December 2022.


## Timeline for {{site.data.keyword.cloudcerts_short}} end of support
{: #certs-mgr_timeline}

{{site.data.keyword.cloudcerts_short}} instances are no longer automatically provisioned in new clusters. Review the list of important dates regarding {{site.data.keyword.cloudcerts_short}} end of support.
{: shortdesc}

The following information is provided for general awareness only. Dates that are marked with a dagger (`†`) are tentative and subject to change. This timeline and the details regarding the {{site.data.keyword.cloudcerts_short}} end of support are tentative and subject to change. 
{: important}

1 December 2022`†`
:   CRNs that reference secrets stored in {{site.data.keyword.cloudcerts_short}} are no longer used to update secrets in the cluster.
:   `ibmcloud oc ingress secret` commands no longer support CRNs that reference secrets stored in {{site.data.keyword.cloudcerts_short}}.

31 December 2022`†`
:   {{site.data.keyword.cloudcerts_short}} becomes fully unsupported.
:   Any remaining {{site.data.keyword.cloudcerts_short}} instances are deleted.
:   Secrets in deleted {{site.data.keyword.cloudcerts_short}} are written directly to the cluster. If you do not migrate your secrets and set a default {{site.data.keyword.secrets-manager_short}}, your secrets are written only to the cluster and not to any manager instance.


