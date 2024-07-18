---

copyright: 
  years: 2014, 2024
lastupdated: "2024-07-18"


keywords: <containers>kubernetes, help, network, connectivity</containers><openshift>openshift</openshift>

subcollection: <containers>containers</containers><openshift>openshift</openshift>

content-type: troubleshoot

---


{{site.data.keyword.attribute-definition-list}}





# Debugging your Portworx installation
{: #debug-portworx}
{: support}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf}

<openshift>
This troubleshooting topic applies to only {{site.data.keyword.redhat_openshift_notm}} clusters that run version 3.11.
{: note}

</openshift>


When you create a Portworx service instance from the {{site.data.keyword.cloud_notm}} catalog, the Portworx installation in your cluster fails and the service instance shows a status of **Provision failure**.
{: tsSymptoms}


Before Portworx is installed in your cluster, a number of checks are performed to verify the information that you provided on the Portworx service page of the {{site.data.keyword.cloud_notm}} catalog.
{: tsCauses} 

If one of these checks fails, the status of the Portworx service is changed to **Provision failure**. You can't see the details of what check failed or what information is missing to complete the installation.


Follow this guide to start troubleshooting your Portworx installation and to verify the information that you entered in the {{site.data.keyword.cloud_notm}} catalog.
{: tsResolve}

If you find information that you entered incorrectly or you must change the setup of your cluster, correct the information or the cluster setup. Then, create a new Portworx service instance to restart the installation.

## Step 1: Verifying the {{site.data.keyword.cloud_notm}} catalog information
{: #px-verify-catalog}

Start by verifying that the information that you entered in the {{site.data.keyword.cloud_notm}} catalog is correct. If information was entered incorrectly, the installation does not pass the pre-installation checks and fails without starting the installation.
{: shortdesc}

1. Verify that the cluster where you want to install Portworx is located in the {{site.data.keyword.cloud_notm}} region and resource group that you selected.
    ```sh
    <containers>ibmcloud ks</containers><openshift>ibmcloud oc</openshift> cluster get --cluster <cluster_name_or_ID>
    ```
    {: pre}

2. Verify that the {{site.data.keyword.cloud_notm}} API key that you entered has sufficient permissions to work with your cluster. You must be assigned the **Editor** platform access role and the **Manager** service access role for <containers>{{site.data.keyword.containerlong_notm}}</containers><openshift>{{site.data.keyword.openshiftlong_notm}}</openshift>. For more information, see [User access permissions](/docs/<containers>containers</containers><openshift>openshift</openshift>?topic=<containers>containers</containers><openshift>openshift</openshift>-iam-platform-access-roles).
3. Verify that you entered the `etcd` API endpoint for your Databases for etcd service instance in the correct format.  

    1. [Retrieve the Databases for etcd endpoint](/docs/<containers>containers</containers><openshift>openshift</openshift>?topic=<containers>containers</containers><openshift>openshift</openshift>-storage_portworx_kv_store).
    2. Add the etcd endpoint in the format `etcd:<etcd_endpoint1>;etcd:<etcd_endpoint2>`. If you have more than one endpoint, include all endpoints and separate them with a semicolon (;).

        Example endpoint:
        ```sh
        etcd:https://1ab234c5-12a1-1234-a123.databases.appdomain.cloud:32059
        ```
        {: screen}

4. Verify that you stored the credentials to access your Databases for etcd service instance in a Kubernetes secret in your cluster. For more information, see [Setting up a Databases for etcd service instance for Portworx metadata](/docs/<containers>containers</containers><openshift>openshift</openshift>?topic=<containers>containers</containers><openshift>openshift</openshift>-storage_portworx_kv_store).
    1. Review steps 4-6 and verify that you retrieved the correct username, password, and certificate.
    2. List the secrets in your cluster and look for the secret that holds the credentials of your Databases for etcd service instance.
        ```sh
        <containers>kubectl</containers><openshift>oc</openshift> get secrets
        ```
        {: pre}

    3. Make sure that the username, password, and certificate are stored as a base64 encoded value in your Kubernetes secret.
    4. Verify that you entered the correct name of the secret in the {{site.data.keyword.cloud_notm}} catalog.
5. If you chose to set up volume encryption with {{site.data.keyword.keymanagementservicelong_notm}}, make sure that you created an instance of {{site.data.keyword.keymanagementservicelong_notm}} in your {{site.data.keyword.cloud_notm}} account and that you stored the credentials to access your instance in a Kubernetes secret in the `portworx` <containers>namespace</containers><openshift>project</openshift> of your cluster. For more information, see [Enabling per-volume encryption for your Portworx volumes](/docs/<containers>containers</containers><openshift>openshift</openshift>?topic=<containers>containers</containers><openshift>openshift</openshift>-storage_portworx_encryption).
    1. Make sure that the API key of your service ID, and the {{site.data.keyword.keymanagementservicelong_notm}} instance ID, root key, and API endpoint are stored as base64 values in the Kubernetes secret of your cluster.
    2. Make sure that you named your secret `px-ibm`.
    3. Make sure that you created the secret in the `portworx` <containers>namespace</containers><openshift>project</openshift> of your cluster.

## Step 2: Verifying the cluster setup
{: #px-verify-cluster}

If you entered the correct information on the {{site.data.keyword.cloud_notm}} catalog page, verify that your cluster is correctly set up for Portworx.
{: shortdesc}

1. Verify that the cluster that you want to use meets the [minimum hardware requirements for Portworx](https://docs.portworx.com/portworx-enterprise/platform/prerequisites){: external}.
2. If you want to use a virtual machine cluster, make sure that you [added raw, unformatted, and unmounted block storage](/docs/<containers>containers</containers><openshift>openshift</openshift>?topic=<containers>containers</containers><openshift>openshift</openshift>-utilities#manual_block) to your cluster so that Portworx can include the disks into the Portworx storage layer.


## Step 3: Reach out to Portworx and IBM
{: #px-support}

Contact Portworx support by using one of the following methods.

- Sending an e-mail to `support@purestorage.com`.

- Calling `+1 (866) 244-7121` or `+1 (650) 729-4088` in the United States or one of the [International numbers](https://support.purestorage.com/bundle/m_contact_us/page/Pure_Storage_Technical_Services/Technical_Services_Information/topics/reference/r_contact_us.html).

- Opening an issue in the [Portworx Service Portal](https://support.purestorage.com/bundle/m_contact_us/page/Pure_Storage_Technical_Services/Technical_Services_Information/topics/reference/r_contact_us.html){: external}. If you don't have an account, see [Request access](https://purestorage.my.site.com/customers/CustomerAccessRequest){: external}.





