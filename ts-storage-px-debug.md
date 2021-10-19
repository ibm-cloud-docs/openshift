---

copyright: 
  years: 2014, 2021
lastupdated: "2021-10-19"

keywords: openshift, roks, rhoks, rhos

subcollection: openshift
content-type: troubleshoot

---
{{site.data.keyword.attribute-definition-list}}


# Debugging your Portworx installation
{: #debug-portworx}

**Infrastructure provider**:
* ![Classic infrastructure provider icon.](images/icon-classic-2.svg) Classic
* ![VPC infrastructure provider icon.](images/icon-vpc-2.svg) VPC


<img src="images/icon-version-311.png" alt="Version 3.11 icon" width="30" style="width:30px; border-style: none"/> This troubleshooting topic applies only to {{site.data.keyword.openshiftshort}} clusters that run version 3.11.
{: note}




When you create a Portworx service instance from the {{site.data.keyword.cloud_notm}} catalog, the Portworx installation in your cluster fails and the service instance shows a status of **Provision failure**.
{: tsSymptoms}


Before Portworx is installed in your cluster, a number of checks are performed to verify the information that you provided on the Portworx service page of the {{site.data.keyword.cloud_notm}} catalog.
{: tsCauses} 

If one of these checks fails, the status of the Portworx service is changed to **Provision failure**. You cannot see the details of what check failed or what information is missing to complete the installation.


Follow this guide to start troubleshooting your Portworx installation and to verify the information that you entered in the {{site.data.keyword.cloud_notm}} catalog.
{: tsResolve}

If you find information that you entered incorrectly or you must change the setup of your cluster, correct the information or the cluster setup. Then, create a new Portworx service instance to restart the installation.

## Step 1: Verifying the {{site.data.keyword.cloud_notm}} catalog information
{: #px-verify-catalog}

Start by verifying that the information that you entered in the {{site.data.keyword.cloud_notm}} catalog is correct. If information was entered incorrectly, the installation does not pass the pre-installation checks and fails without starting the installation.
{: shortdesc}

1. Verify that the cluster where you want to install Portworx is located in the {{site.data.keyword.cloud_notm}} region and resource group that you selected.
    ```sh
    ibmcloud oc cluster get --cluster <cluster_name_or_ID>
    ```
    {: pre}

2. Verify that the {{site.data.keyword.cloud_notm}} API key that you entered has sufficient permissions to work with your cluster. You must be assigned the **Editor** platform access role and the **Manager** service access role for {{site.data.keyword.openshiftlong_notm}}. For more information, see [User access permissions](/docs/containers?topic=containers-access_reference).
3. Verify that you entered the `etcd` API endpoint for your Databases for etcd service instance in the correct format.  
    1. [Retrieve the Databases for etcd endpoint](/docs/openshift?topic=openshift-portworx#databases_credentials).
    2. Add the etcd endpoint in the format `etcd:<etcd_endpoint1>;etcd:<etcd_endpoint2>`. If you have more than one endpoint, include all endpoints and separate them with a semicolon (;).

        Example endpoint:
        ```sh
        etcd:https://1ab234c5-12a1-1234-a123.databases.appdomain.cloud:32059
        ```
        {: screen}

4. Verify that you stored the credentials to access your Databases for etcd service instance in a Kubernetes secret in your cluster. For more information, see [Setting up a Databases for etcd service instance for Portworx metadata](/docs/openshift?topic=openshift-portworx#portworx_database).
    1. Review steps 4-6 and verify that you retrieved the correct username, password, and certificate.
    2. List the secrets in your cluster and look for the secret that holds the credentials of your Databases for etcd service instance.
        ```sh
        oc get secrets
        ```
        {: pre}

    3. Make sure that the username, password, and certificate are stored as a base64 encoded value in your Kubernetes secret.
    4. Verify that you entered the correct name of the secret in the {{site.data.keyword.cloud_notm}} catalog.
5. If you chose to set up volume encryption with {{site.data.keyword.keymanagementservicelong_notm}}, make sure that you created an instance of {{site.data.keyword.keymanagementservicelong_notm}} in your {{site.data.keyword.cloud_notm}} account and that you stored the credentials to access your instance in a Kubernetes secret in the `portworx` project of your cluster. For more information, see [Enabling per-volume encryption for your Portworx volumes](/docs/openshift?topic=openshift-portworx#setup_encryption).
    1. Make sure that the API key of your service ID, and the {{site.data.keyword.keymanagementservicelong_notm}} instance ID, root key, and API endpoint are stored as base64 values in the Kubernetes secret of your cluster.
    2. Make sure that you named your secret `px-ibm`.
    3. Make sure that you created the secret in the `portworx` project of your cluster.

## Step 2: Verifying the cluster setup
{: #px-verify-cluster}

If you entered the correct information on the {{site.data.keyword.cloud_notm}} catalog page, verify that your cluster is correctly set up for Portworx.
{: shortdesc}

1. Verify that the cluster that you want to use meets the [minimum hardware requirements for Portworx](https://docs.portworx.com/start-here-installation/){: external}.
2. If you want to use a virtual machine cluster, make sure that you [added raw, unformatted, and unmounted block storage](/docs/openshift?topic=openshift-portworx#create_block_storage) to your cluster so that Portworx can include the disks into the Portworx storage layer.
3. Verify that your cluster is set up with public network connectivity. For more information, see [Understanding network basics of classic clusters](/docs/openshift?topic=openshift-plan_clusters#plan_basics).



## Step 3: Reach out to Portworx and IBM
{: #px-support}

If you run into an issue with using Portworx, you can open an issue in the [Portworx Service Portal](https://pure1.purestorage.com/support){: external}. You can also submit a request by sending an e-mail to `support@purestorage.com`. If you do not have an account on the Portworx Service Portal, send an e-mail to `support@purestorage.com`.




