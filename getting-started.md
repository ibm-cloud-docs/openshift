---

copyright:
  years: 2014, 2023
lastupdated: "2023-09-25"

keywords: red hat openshift, openshift container platform, red hat, create openshift cluster, openshift vpc cluster, openshift classic cluster, red hat cluster, openshift, containers, clusters

subcollection: openshift

---


{{site.data.keyword.attribute-definition-list}}







# Getting started with {{site.data.keyword.openshiftlong_notm}}
{: #getting-started}

With {{site.data.keyword.openshiftlong_notm}}, you can deploy apps on highly available {{site.data.keyword.redhat_openshift_notm}} clusters.
{: shortdesc}

First, create a cluster or a cluster on Classic or VPC infrastructure. Then, deploy and expose a sample app in your cluster.

To complete the getting started tutorial, use a [Pay-As-You-Go or Subscription {{site.data.keyword.containerlong}} account](/docs/account?topic=account-upgrading-account) where you are the owner or have [full Administrator access](/docs/account?topic=account-assign-access-resources).
{: note}


## Creating a classic cluster in the console
{: #clusters_gs}
{: ui}


1. Log in to your [{{site.data.keyword.cloud_notm}} account](https://cloud.ibm.com/){: external}.
2. From the **Catalog**, click [**{{site.data.keyword.openshiftlong_notm}}**](https://cloud.ibm.com/kubernetes/catalog/about?platformType=openshift){: external}.
3. Review the platform version details, **{{site.data.keyword.redhat_openshift_notm}} 4.13.11**.
4. If you see the **OCP entitlement** section: Leave the value set to **Purchase additional licenses for this worker pool** because you are not using an {{site.data.keyword.cloud_notm}} Pak for this getting started cluster.
5. For the **Infrastructure**, select **Classic**.
6. Configure the **Location** details for your cluster.
    1. Select the **Resource group** that you want to create your cluster in. You can't change the resource group later. If you don't select a resource group, your cluster is created in the default resource group.
    2. Select a **Geography** to create the cluster in, such as **North America**. The geography helps filter the **Availability** and **Data centers** values that you can select.
    3. Select the **Availability** that you want for your cluster, such as **Single zone**.
    4. Select the **Worker zone** to create your cluster in, such as **Dallas 10**.
7. Configure your **Worker pool** setup.
    1. If you want a larger size for your worker nodes, click **Change flavor**. Otherwise, leave the default **4 vCPUs / 16 GB** flavor selected.
    2. Set how many worker nodes to create per zone, such as the minimum value of **2**. For more information, see [What is the smallest size cluster that I can make?](/docs/openshift?topic=openshift-faqs#smallest_cluster).
8. Complete the **Resource details** to customize the cluster name and any tags that you want to use to organize your {{site.data.keyword.cloud_notm}} resources.
9. In the **Summary** pane, review the order summary and then click **Create**.
    Your cluster creation might take some time to complete. After the cluster state shows **Normal**, the cluster network and load balancing components take about 10 more minutes to deploy and update the cluster domain that you use for the {{site.data.keyword.redhat_openshift_notm}} web console and other routes. Before you continue, wait until the cluster is ready by checking that the **Ingress Subdomain** follows a pattern of `<cluster_name>.<globally_unique_account_HASH>-0001.<region>.containers.appdomain.cloud`.
    {: note}

10. Verify that your cluster setup is finished before you continue to the next step by checking that the worker nodes on the **Worker Nodes** tab have a **Status** of normal.

Now that your cluster is ready, [deploying your first app](#deploy-app)!

## Creating a VPC cluster in the console
{: #vpc-gen2-gs}
{: ui}

1. Create a Virtual Private Cloud (VPC) on generation 2 compute.
    1. Navigate to the [VPC create console](https://cloud.ibm.com/vpc/provision/vpc){: external}.
    2. Give the VPC a name and select a resource group to deploy the VPC into.
    3. Give the VPC subnet a name and select the location where you want to create the cluster.
    4. Attach a public gateway to your subnet so that you can access public endpoints from your cluster. This public gateway is used later on to access default {{site.data.keyword.redhat_openshift_notm}} components like the web console, OperatorHub, and service catalog.
    5. Click **Create virtual private cloud**.
2. From the [{{site.data.keyword.openshiftlong_notm}} dashboard](https://cloud.ibm.com/kubernetes/landing?platformType=openshift){: external}, click **Create cluster**.
3. Configure your cluster's VPC environment.
    1. Review the platform version details, **{{site.data.keyword.redhat_openshift_notm}} 4.13.11**.
    2. If you see the **OCP entitlement** section: Leave the value set to **Purchase additional licenses for this worker pool** because you are not using an {{site.data.keyword.cloud_notm}} Pak for this getting started cluster.
    3. For the **Infrastructure**, select **VPC**.
    4. From the **Virtual private cloud** drop-down menu, select the VPC that you created earlier.
    5. From the **Cloud Object Storage** drop-down menu, select a standard {{site.data.keyword.cos_full_notm}} instance to use for the internal {{site.data.keyword.redhat_openshift_notm}} container registry, or [create a standard {{site.data.keyword.cos_full_notm}} instance](/docs/cloud-object-storage?topic=cloud-object-storage-provision) to use.
4. Configure the **Location** details for your cluster.
    1. Select the **Resource group** that you want to create your cluster in. You can't change the resource group later. If you don't select a resource group, your cluster is created in the default resource group.
    2. Select the zones to create your cluster in. The zones are filtered based on the VPC that you selected, and include the subnets that you previously created.
5. Configure your **Worker pool** setup.
    1. If you want a larger size for your worker nodes, click **Change flavor**. Otherwise, leave the default **4 vCPUs / 16 GB** flavor selected.
    2. Set how many worker nodes to create per zone, such as the minimum value of **2**. For more information, see [What is the smallest size cluster that I can make?](/docs/openshift?topic=openshift-faqs#smallest_cluster).
6. Complete the **Resource details** to customize the cluster name and any tags that you want to use to organize your {{site.data.keyword.cloud_notm}} resources.
7. In the **Summary** pane, review the order summary and then click **Create**.
    Your cluster creation might take some time to complete. After the cluster state shows **Normal**, the cluster network and load balancing components take about 10 more minutes to deploy and update the cluster domain that you use for the {{site.data.keyword.redhat_openshift_notm}} web console and other routes. Before you continue, wait until the cluster is ready by checking that the **Ingress Subdomain** follows a pattern of `<cluster_name>.<globally_unique_account_HASH>-0001.<region>.containers.appdomain.cloud`.
    {: note}
    
The Red Hat-provided OperatorHub source images require access to the `registry.redhat.io` and `quay.io` registries. If your cluster runs on a restricted network, such as in a VPC without a public gateway or classic worker nodes on only a private VLAN, these images are not accessible. To mirror the OperatorHub source images for use in your cluster, see [Disabling and mirroring OperatorHub catalog source images](/docs/openshift?topic=openshift-operators#mirror-operatorhub).
{: tip}

The worker node can take a few minutes to provision, but you can see the progress in the **Worker nodes** tab. When the status reaches `Ready`, you can start working with your cluster by [deploying your first app](#deploy-app)!

## Creating classic clusters in the {{site.data.keyword.openshiftlong_notm}} CLI
{: #clusters_gs_classic_cli}
{: cli}

Review the following example commands for creating classic clusters in the CLI.



Create a classic cluster on a shared virtual machine.

```sh
ibmcloud oc cluster create classic --name my_cluster --version 4.13_openshift --zone dal10 --flavor b3c.4x16 --hardware shared --workers 3
```
{: pre}


Create a classic cluster on bare metal architecture.

```sh
ibmcloud oc cluster create classic --name my_cluster --version 4.13_openshift --zone dal10 --flavor mb2c.4x32 --hardware dedicated --workers 3 --public-vlan <public_VLAN_ID> --private-vlan <private_VLAN_ID>
```
{: pre}

Create a classic cluster with an IBM Cloud Pak entitlement for a default worker pool of 3 worker nodes with 4 cores and 16 GB memory each.

```sh
ibmcloud oc cluster create classic --name cloud_pak_cluster --version 4.13_openshift --zone dal10 --flavor b3c.4x16 --hardware dedicated --workers 3 --entitlement cloud_pak --public-vlan <public_VLAN_ID> --private-vlan <private_VLAN_ID> [--operating-system (REDHAT_7_64|REDHAT_8_64)]
```
{: pre}

For a complete list of available RHEL versions and which cluster versions they are compatible with, see [Available {{site.data.keyword.redhat_openshift_notm}} versions](/docs/openshift?topic=openshift-openshift_versions#openshift_versions_available).

```sh
ibmcloud oc cluster create classic --name my_cluster --zone dal10 --flavor b3c.4x16 --version 4.9.28_openshift --operating-system REDHAT_8_64
```



For a classic multizone cluster, after you created the cluster in a [multizone metro](/docs/openshift?topic=openshift-regions-and-zones#zones-mz), [add zones](/docs/openshift?topic=openshift-add-workers-classic#add_zone):
```sh
ibmcloud oc zone add classic --zone <zone> --cluster <cluster_name_or_ID> --worker-pool <pool_name> --private-vlan <private_VLAN_ID> --public-vlan <public_VLAN_ID>
```
{: pre}

## Creating VPC clusters in the CLI
{: #clusters_gs_vpc_cli}
{: cli}

Review the sample commands for creating classic clusters in the CLI. For more detailed steps and information about creating clusters, see [Creating VPC clusters](/docs/openshift?topic=openshift-cluster-create-vpc-gen2&interface=cli#cluster_create_vpc). For information about planning your cluster set up, see [Preparing to create clusters](/docs/openshift?topic=openshift-clusters&interface=cli).
{: shortdesc}

Create a VPC cluster with three worker nodes.

```sh
ibmcloud oc cluster create vpc-gen2 --name my_cluster --version 4.13_openshift --zone us-east-1 --vpc-id <VPC_ID> --subnet-id <VPC_SUBNET_ID> --cos-instance <COS_CRN>--flavor bx2.4x16 --workers 3
```
{: pre}

For a VPC multizone cluster, after you created the cluster in a [multizone metro](/docs/openshift?topic=openshift-regions-and-zones#zones-vpc), [add zones](/docs/openshift?topic=openshift-add-workers-vpc#vpc_add_zone).

```sh
ibmcloud oc zone add vpc-gen2 --zone <zone> --cluster <cluster_name_or_ID> --worker-pool <pool_name> --subnet-id <VPC_SUBNET_ID>
```
{: pre}

## Deploying an app with the {{site.data.keyword.redhat_openshift_notm}} service catalog
{: #deploy-app}

From the {{site.data.keyword.redhat_openshift_notm}} console, you can deploy one of the built-in service catalog apps and expose the app with a route.
{: shortdesc}

1. From the cluster details page, click **OpenShift web console**.
2. From the side navigation menu in the **Administrator** perspective, click **Home > Projects** and then click **Create Project**. Enter a name for your project, and click **Create**. Now that your project is created by the administrator, you can switch to the Developer perspective to create an app.
3. From the side navigation menu, select **Developer** from the perspective switcher.
4. Click **+Add**. From the **Add** pane menu bar, make sure that the **Project** is the one that you just created.
5. Click **From Catalog**. The **Developer Catalog** opens in the pane.
6. From the navigation menu in the pane, click **Languages > JavaScript**.
7. Click **Node.js**, and then click **Create Application**. Note that you might need to click **Clear All Filters** to display the **Node.js** option. After you select **Node.js**, the **Create Source-to-Image Application** pane opens.
8. In the **Git** section, click **Try Sample**.
9. Scroll to confirm that **Deployment** and **Create a route to the application** are selected, and then click **Create**.
10. Wait a few minutes for the pods to deploy. To check the status of the pods, from the **Topology** pane, click your **`nodejs`** app and review its sidebar. You must see that the `nodejs` build is complete, and that the `nodejs` pod is in a **Running** state to continue.
11. When the deployment is complete, click the route location URL, which has a format similar to the following.

    ```sh
    http://nodejs-<project>.<cluster_name>-<hash>.<region>.containers.appdomain.cloud
    ```
    {: screen}

    A new tab in your browser opens with a message similar to the following.
    ```sh
    Welcome to your Node.js application on OpenShift
    ```
    {: screen}

12. **Optional**: To clean up the resources that you created, select **Administrator** from the perspective switcher, navigate to **Home > Projects**, click your project's action menu, and click **Delete Project**.


## What's next?
{: #whats-next}

| Suggestion  |  What you learn about {{site.data.keyword.redhat_openshift_notm}}|
|----------|------|
| [{{site.data.keyword.openshiftlong_notm}} classic cluster tutorial](/docs/openshift?topic=openshift-openshift_tutorial) or [{{site.data.keyword.openshiftlong_notm}} VPC cluster tutorial](/docs/openshift?topic=openshift-vpc_rh_tutorial) | - Set up your {{site.data.keyword.cloud_notm}} and {{site.data.keyword.redhat_openshift_notm}} CLI. \n - Deploy an app that uses an {{site.data.keyword.cloud_notm}} service. |
|[Learning path for administrators](/docs/openshift?topic=openshift-learning-path-admin)|See an overview of all the options in {{site.data.keyword.openshiftlong_notm}} for administrators.
|[Learning path for developers](/docs/openshift?topic=openshift-learning-path-dev)|See an overview of all the options in {{site.data.keyword.openshiftlong_notm}} for developers.
|[{{site.data.keyword.redhat_openshift_notm}} developer activities](https://docs.openshift.com/container-platform/4.13/welcome/index.html#developer-activities){: external} documentation | Learn how to work with your apps|
{: caption="What's next after completing the {{site.data.keyword.openshiftlong_notm}} getting started?" caption-side="bottom"}







