---

copyright:
  years: 2014, 2024
lastupdated: "2024-04-12"


keywords: openshift, integrations, entitlements, ocp entitled, licenses, license, red hat, {{site.data.keyword.openshiftlong_notm}}

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}


# Adding Cloud Paks, entitlements, or licenses to your cluster
{: #openshift_cloud_paks}

Review the following steps for adding [IBM Cloud Paks](https://www.ibm.com/cloud-paks/){: external}, {{site.data.keyword.redhat_openshift_notm}} licenses, and other entitlements to your {{site.data.keyword.openshiftlong_notm}} clusters
{: shortdesc}

## Assigning a Cloud Pak entitlement to your {{site.data.keyword.cloud_notm}} account
{: #oc_cloud_paks_assign}

To deploy a Cloud Pak to your {{site.data.keyword.openshiftlong_notm}} cluster, your entitlement to the Cloud Pak must be assigned to your {{site.data.keyword.cloud_notm}} account.
{: shortdesc}

1. Verify that your Cloud Pak entitlement is in your [**Container software library**](https://myibm.ibm.com/products-services/containerlibrary){: external}. If you don't see the entitlement, the entitlement might be owned by a different user. Verify the user, and if you still have issues, click **Contact IBM** from the container software library page.
2. Make sure that the {{site.data.keyword.cloud_notm}} account owner gives you permission to assign entitlements.
    1. From the [{{site.data.keyword.cloud_notm}} console](https://cloud.ibm.com/){: external} menu bar, click **Manage > Access (IAM)**.
    2. From the **Users** tab, click the user that you want to assign permissions.
    3. Click **Access policies > Assign access +**.
    4. Click **Account management**.
    5. From the **What type of access do you want to assign?** drop-down menu, select **License and Entitlement**.
    6. Select at least the **Editor** platform access role, then click **Add**.
3. [Assign the Cloud Pak entitlement to your {{site.data.keyword.cloud_notm}} account](/docs/account?topic=account-software-license).
4. Continue to [create the Cloud Pak instance](#oc_cloud_paks_add).


## Adding entitlements to your cluster
{: #oc_cloud_paks_add}
{: help}
{: support}

Before you begin:
* Verify that your account administrator [set up your {{site.data.keyword.cloud_notm}} account with the Cloud Pak entitlement](#oc_cloud_paks_assign).
* Make sure that you have the [required permissions to create a cluster](/docs/openshift?topic=openshift-iam-platform-access-roles).

1. Add your entitlement from [IBM Passport Advantage](https://www.ibm.com/software/passportadvantage/index.html){: external} to your {{site.data.keyword.openshiftlong_notm}} cluster.
    *  **For new clusters**: [Create a cluster](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_cluster_create) with the `--entitlement ocp_entitled` option. When you specify the number of workers (`--workers`) and flavor (`--flavor`), make sure to specify only the number and size of worker nodes that you are entitled to use. You can optionally specify the worker node operating system (`--operating-system`). After your cluster is created, you are not charged the {{site.data.keyword.redhat_openshift_notm}} license fee for the entitled worker nodes in the `default` worker pool. If you want to use a different worker pool for your Cloud Pak, follow the steps for existing clusters.
    * **For existing clusters or worker pools other than the `default`**: Create a [worker pool](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_pool_create) with the `--entitlement ocp_entitled` option. When you specify the number of workers (`--size-per-zone`) and flavor (`--flavor`), make sure to specify only the number and size of worker nodes that you are entitled to use. After creation, your worker pool does not charge you the {{site.data.keyword.redhat_openshift_notm}} license fee for your entitled worker nodes.

    Do not exceed your entitlement. Keep in mind that your OpenShift Container Platform entitlements can be used with other cloud providers or in other environments. To avoid billing issues later, make sure that you use only what you are entitled to use. For example, you might have an entitlement for the OCP licenses for two worker nodes of 4 CPU and 16 GB memory, and you create this worker pool with two worker nodes of 4 CPU and 16 GB memory. You used your entire entitlement, and you can't use the same entitlement for other worker pools, cloud providers, or environments.
    {: important}

2. In the [{{site.data.keyword.cloud_notm}} catalog](https://cloud.ibm.com/catalog?search=label%3Acloud_pak#software){: external}, in the **Software** tab, under **Offering Type**, check **Cloud Paks**.
3. Select the Cloud Pak that you want to deploy, and follow the installation instructions. Each Cloud Pak requires an entitlement from [IBM Passport Advantage](https://www.ibm.com/software/passportadvantage/){: external}, and has its own configuration settings. For more information, view the **About** tab and Cloud Pak documentation.

## Adding Cloud Pak images from an entitled registry
{: #oc_cloud_paks_registry}

You can deploy Cloud Pak images that you are already licensed to use in [IBM Passport Advantage](https://www.ibm.com/software/passportadvantage/){: external} to your {{site.data.keyword.openshiftlong_notm}} cluster by using the {{site.data.keyword.registrylong_notm}} entitled registry.
{: shortdesc}

1. Set up your cluster to [pull images from the entitled registry](/docs/openshift?topic=openshift-registry#secret_entitled_software).
2. [Set up Helm in your cluster](/docs/openshift?topic=openshift-helm) and add the **entitled** Helm repository.
3. Find and review the Helm chart from the [Helm catalog](https://cloud.ibm.com/kubernetes/helm){: external} or from the CLI by running `helm search repo entitled` and `helm show entitled/<chart_name>`.
4. Follow the instructions that are particular to each Cloud Pak installation, such as configuring the Helm chart values to work within {{site.data.keyword.redhat_openshift_notm}} security context constraints.


Now you can run your Cloud Pak on your {{site.data.keyword.redhat_openshift_notm}} cluster!



