---

copyright:
  years: 2020, 2023
lastupdated: "2023-12-15"

keywords: openshift, satellite, distributed cloud, on-prem, hybrid

subcollection: openshift

---


{{site.data.keyword.attribute-definition-list}}

# Creating {{site.data.keyword.satelliteshort}} clusters
{: #satellite-clusters}

[{{site.data.keyword.satelliteshort}}]{: tag-satellite}

You can create {{site.data.keyword.openshiftlong}} clusters in an {{site.data.keyword.satellitelong}} location, and use the hosts of your own infrastructure that you added to your location as the worker nodes for the cluster.
{: shortdesc}

## Prerequisites
{: #satcluster-prereqs}

Before you can create clusters in {{site.data.keyword.satellitelong_notm}}, you must first set up a location.
{: shortdesc}

1. [Review the {{site.data.keyword.satellitelong_notm}} components](/docs/satellite?topic=satellite-faqs) and the [location planning guide](/docs/satellite?topic=satellite-infrastructure-plan).
1. Review the [{{site.data.keyword.satelliteshort}} cluster limitations](/docs/openshift?topic=openshift-limitations#satellite_limits).
1. Prepare to create your {{site.data.keyword.satellitelong_notm}} location. Choose from one of the following options.
    Note that support for automatically creating a Red Hat CoreOS enabled location with Schematics is currently not available. If you want to create a Red Hat CoreOS enabled location, see [Manually creating a location](/docs/satellite?topic=satellite-loc-manual-create). Red Hat CoreOS is available in all supported {{site.data.keyword.satelliteshort}} locations and for {{site.data.keyword.redhat_openshift_notm}} version 4.9 and later.
    
    * You can automatically provision the hosts for your location. With this option, you create a custom role, or service ID, with your cloud provider credentials. This service ID is used to automatically provision virtual machines in your cloud provider. Once the VMs are provisioned and attached to your location, you can assign them to {{site.data.keyword.satellitelong_notm}} control plane or to the cloud services you want to use. To get started, see the [Automating your location set up with a {{site.data.keyword.bpshort}} template](/docs/satellite?topic=satellite-locations).
    * You can manually provision hosts either in your on-premises data center or in a public cloud. If you choose to manually provision the hosts for your location, make sure that your hosts meet the [minimum requirements](/docs/satellite?topic=satellite-host-reqs) and that you allow the [required outbound network access](/docs/satellite?topic=satellite-reqs-host-network). 
1. [Create an {{site.data.keyword.satellitelong_notm}} location](/docs/satellite?topic=satellite-locations).
1. Attach your hosts to your location and [set up your location control plane](/docs/satellite?topic=satellite-setup-control-plane).
1. [Attach at least 3 additional hosts to your location](/docs/satellite?topic=satellite-attach-hosts) to use as the worker nodes for your {{site.data.keyword.openshiftlong_notm}} cluster.
1. Make sure that the location that you select is healthy and in a **Normal** state before creating a cluster.



## Creating {{site.data.keyword.satelliteshort}} clusters from the console
{: #satcluster-create-console}
{: ui}

Use the {{site.data.keyword.cloud_notm}} console to create your {{site.data.keyword.redhat_openshift_notm}} clusters on your {{site.data.keyword.satelliteshort}} infrastructure.
{: shortdesc}

From the [{{site.data.keyword.redhat_openshift_notm}} clusters console](https://cloud.ibm.com/kubernetes/clusters?platformType=openshift){: external}, click **Create**. Then, review the following sections to set up your cluster.

Infrastructure
:   Select **{{site.data.keyword.satelliteshort}}**.

Location
:   Select the **Resource group** and the **{{site.data.keyword.satelliteshort}} location** where you want to create the cluster.

In RHCOS enabled locations, when you want to add worker pools to your cluster, you can use RHCOS or RHEL hosts. Make sure to attach hosts with the operating system that you want to use to your location before assigning them to a worker pool.
{: tip}

Infrastructure topology
:   - **Highly available**: Choose this option for most use cases. Create at least 3 worker nodes for high availability. 
:   - **Single replica**: Single-node clusters are recommended only in specific circumstances, and should only be used in resource-constrained edge locations that have multiple redundant locations running the same workload. If you are running your {{site.data.keyword.openshiftlong_notm}} cluster on {{site.data.keyword.satelliteshort}} infrastructure in a remote, resource-constrained edge location with limited resources, such as a small data center in a mobile tower, running a data plane with a smaller foot print might be beneficial for your setup. While typical {{site.data.keyword.openshiftlong_notm}} clusters require at least three worker nodes for high availability, you have the option to create a cluster that runs a single worker node. Single-node clusters have several limitations and should only be used in specific circumstances. Single-node clusters lack high availability. By provisioning a single-node cluster, you accept that you are more likely to experience downtime and disruptions in your workload. Single node clusters must run on a {{site.data.keyword.satelliteshort}} location with [CoreOS enabled](/docs/satellite?topic=satellite-locations#verify-coreos-location). Control plane hosts on your location and the host you assign to your single-node cluster must run either the RHEL 8 or RHCOS operating systems. Only supported for {{site.data.keyword.satelliteshort}} clusters that run version 4.11 or later. See the [Limitations](/docs/openshift?topic=openshift-limitations#satellite_limits) section for more information.

Default worker pool
:   Configure the details for your default worker pool.
:   - **Host operating system**: Select the operating system of the hosts that you want to use in the default worker pool of your cluster. In locations that are Red Hat CoreOS enabled, you can use either your RHCOS or RHEL hosts.
:   - **Worker pool zones** that {{site.data.keyword.satelliteshort}} uses to evenly assign hosts across zones that represent zones in your underlying infrastructure provider. Generally, create your worker pool across 3 zones for high availability.
:   - **vCPU**, **Memory (GB)**, and number of **Worker nodes per zone**: Request the resources that you want to create the worker pool with. {{site.data.keyword.satelliteshort}} can automatically assign available hosts to the worker pool to fulfill your request. Generally, select at least 1 worker node per zone for a total of 3 worker nodes in your cluster.

OpenShift version
:    Select your cluster version. Choose the default version, or you can specify a different [supported version](/docs/containers?topic=containers-cs_versions#cs_versions_available).

OpenShift Container Platform (OCP) license
:   All user clusters in your Satellite location are installed with OpenShift Container Platform, which incurs a licensing fee from Red Hat. However, you can bring your own OpenShift Container Platform license for clusters created with your on-premises infrastructure or for clusters created on-premises by using IBM Cloud Paks. Service clusters, which are the underlying platform for all {{site.data.keyword.cloud_notm}} services are created by services such as {{site.data.keyword.keymanagementserviceshort}} or {{site.data.keyword.cos_full_notm}} and do not require a license.
:   - **Apply my Cloud Pak entitlement**: Select this option to apply your Cloud Pak entitlement to the default worker pool. Cloud Pak entitlements are applied at the worker pool level. Do not exceed your entitlement. Keep in mind that your OpenShift Container Platform entitlements can be used with other cloud providers or in other environments. To avoid billing issues later, make sure that you use only what you are entitled to use. For example, you might have an entitlement for the OCP licenses for two worker nodes of 4 CPU and 16 GB memory, and you create this worker pool with two worker nodes of 4 CPU and 16 GB memory. You used your entire entitlement, and you can't use the same entitlement for other worker pools, cloud providers, or environments.
:   - **Purchase a license**: Purchase a new OpenShift Container Platform license for the default worker pool. This option is applied at the worker pool level. When you create additional worker pools you must purchase additional licenses.
:   - **Manage with Red Hat OpenShift Cluster Manager**: Specify an existing OCP entitlement for the worker nodes in this cluster by providing your Red Hat® account pull secret as a file or in raw JSON format. The cluster also uses this pull secret to download Red Hat OpenShift images from your own Red Hat account. This option is applied at the cluster level.



{{site.data.keyword.satelliteshort}} Config
:   Decide whether to enable cluster admin access for {{site.data.keyword.satelliteshort}} Config. If you don't grant {{site.data.keyword.satelliteshort}} Config access, you can't later use the {{site.data.keyword.satelliteshort}} Config functionality to view or deploy Kubernetes resources for your clusters. If you want to enable access later, you can [create custom RBAC roles for {{site.data.keyword.satelliteshort}} Config](/docs/satellite?topic=satellite-setup-clusters-satconfig#custom-access-cluster-wide).

Encryption
:    Enable data encryption with a key management service (KMS) to encrypt secrets and other sensitive information in your cluster. You can also [enable KMS](/docs/openshift?topic=openshift-encryption-setup) later.

Ingress secrets management
:   [{{site.data.keyword.secrets-manager_full_notm}}](/docs/openshift?topic=openshift-secrets-mgr) centrally manages Ingress subdomain certificates and other secrets in your cluster. You can choose to register a {{site.data.keyword.secrets-manager_short}} instance to your cluster during the cluster create process. You can also specify a secret group that you can use to control access to the secrets in your cluster. Both of these options can be configured or changed after you have created the cluster.

Clusters details
:   Give your cluster a name and enter any [{{site.data.keyword.cloud_notm}} tags](/docs/account?topic=account-tag) that you want to associate with your cloud resource. The cluster name must start with a letter, can contain letters, numbers, and hyphen (-), and must be 35 characters or fewer.

If you don't have any available and matching hosts in your {{site.data.keyword.satelliteshort}} location, the cluster is still created but enters a **Warning** state. [Attach hosts](/docs/satellite?topic=satellite-attach-hosts) to your {{site.data.keyword.satelliteshort}} location so that hosts can be assigned as worker nodes to the worker pool. If the hosts are not automatically assigned, you can also manually [assign {{site.data.keyword.satelliteshort}} hosts to your cluster](https://cloud.ibm.com/docs/satellite?topic=satellite-assigning-hosts). Ensure that hosts are assigned as worker nodes in each zone of your default worker pool.
{: note}

If your location hosts have private network connectivity only, or if you use Amazon Web Services, Google Cloud Platform, or Microsoft Azure hosts, you must be connected to your hosts' private network, such as through VPN access, to connect to your cluster and access the {{site.data.keyword.redhat_openshift_notm}} web console. Alternatively, if your hosts have public network connectivity, you can test access to your cluster by changing your cluster's and location's DNS records to [use your hosts' public IP addresses](/docs/openshift?topic=openshift-access_cluster#sat_public_access).
{: note}

Wait until your cluster reaches a **Normal** state, then [access your cluster](/docs/openshift?topic=openshift-access_cluster#access_cluster_sat) to access the {{site.data.keyword.redhat_openshift_notm}} web console or to run `oc` and `kubectl` commands from the CLI. If you enabled {{site.data.keyword.satelliteshort}} Config access, you must complete this step to synchronize the permissions.


## Creating {{site.data.keyword.satelliteshort}} clusters from the CLI
{: #satcluster-create-cli}
{: cli}

Use the {{site.data.keyword.satelliteshort}} CLI to create your {{site.data.keyword.redhat_openshift_notm}} clusters on your {{site.data.keyword.satelliteshort}} infrastructure.
{: shortdesc}

Before you begin, [install the {{site.data.keyword.satelliteshort}} CLI plug-in](/docs/satellite?topic=satellite-cli-install).

1. [Complete the prerequisite steps](#satcluster-prereqs).
2. Verify that your location is in a **Normal** state. The location is in a **Normal** state when you successfully created the {{site.data.keyword.satelliteshort}} control plane and all hosts that you use for the control plane are in a healthy state.
    ```sh
    ibmcloud sat location ls
    ```
    {: pre}

    Example output

    ```sh
    Retrieving locations...
    OK
    Name         ID                     Status            Ready   Created      Hosts (used/total)   Managed From   
    mylocation   brhtfum2015a6mgqj16g   normal            yes     4 days ago   3 / 6                Dallas   
    ```
    {: screen}

3. Create a {{site.data.keyword.redhat_openshift_notm}} cluster in your {{site.data.keyword.satelliteshort}} location. When you create the cluster, the cluster master is automatically created in your {{site.data.keyword.satelliteshort}} control plane. 

    - To ensure that hosts are automatically assigned as worker nodes in the default worker pool of your cluster, specify those hosts' labels in the `--host-label` options, and specify the number of worker nodes per zone in the `--workers` option. 
    - To enable cluster admin access for {{site.data.keyword.satelliteshort}} Config, include the `--enable-admin-agent` option. If you don't grant {{site.data.keyword.satelliteshort}} Config access, you can't later use the {{site.data.keyword.satelliteshort}} Config functionality to view or deploy Kubernetes resources for your clusters. If you want to enable access later, you can [create custom RBAC roles for {{site.data.keyword.satelliteshort}} Config](/docs/satellite?topic=satellite-setup-clusters-satconfig#custom-access-cluster-wide). 
    - For more information about this command's options, see the [CLI reference documentation](/docs/openshift?topic=openshift-kubernetes-service-cli#cli_cluster-create-satellite).
    - You can create a single-node cluster by including the `--infrastructure-topology` option and specifying the `single-replica` value when [creating a {{site.data.keyword.satelliteshort}} cluster in the CLI](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster). If this option is not included, the cluster is provisioned with the highly available setup of three worker nodes by default.
    - To bring your own OCP license, make sure to include your Red Hat pull secret to entitle the cluster to run OCP, either by uploading the pull secret in the console or by including the `--pull-secret` option in the `ibmcloud oc cluster create satellite` [command](/docs/openshift?topic=openshift-kubernetes-service-cli#cli_cluster-create-satellite).
    - To apply your Cloud Pak entitlement, make sure to include the `--entitlement cloud_pak` option.
    
    `--operating-system REDHAT_7_64|REDHAT_8_64|RHCOS`
:   Optional. The operating system of the worker nodes in your cluster. For a list of available operating sysems by cluster version, see [Available {{site.data.keyword.redhat_openshift_notm}} versions](/docs/openshift?topic=openshift-openshift_versions#openshift_versions_available). Note that to use your `RHCOS` hosts in your clusters, you must create a Red Hat CoreOS-enabled location and a cluster that runs version 4.9 or later. If no option is specified, the default [operating system that corresponds to the cluster version](/docs/openshift?topic=openshift-openshift_versions#openshift_versions_available) is used.

    
    Example `cluster create` command.

    ```sh
    ibmcloud oc cluster create satellite --location LOCATION --name NAME --pull-secret SECRET --version 4.13_openshift [--enable-admin-agent] [--host-label LABEL ...] [--operating-system (REDHAT_8_64|RHCOS)] [--pod-subnet SUBNET] [-q] [--service-subnet SUBNET] [--workers WORKERS-PER-ZONE] [--zone ZONE] [--entitlement ENTITLEMENT]
    ```
    {: pre}
    
    Example `cluster create` command using `RHCOS` hosts and applying a `--pull-secret` license.
    ```sh
    ibmcloud oc cluster create satellite --location LOCATION --name <cluster_name> --pull-secret SECRET --version VERSION --enable-admin-agent --operating-system RHCOS 
    ```
    {: pre}

    Example output

    ```sh
    Creating cluster...
    OK
    Cluster created with ID brkhsd220b6ktv7sjl50
    ```
    {: screen}

4. Wait for the cluster to reach a **Warning** state. The **Warning** state indicates that the cluster master is fully deployed, but no worker nodes could be detected in the cluster.
    ```sh
    ibmcloud oc cluster ls
    ```
    {: pre}

    Example output

    ```sh
    OK
    Name                ID                     State     Created          Workers   Location           Version                 Resource Group Name   Provider   
    satcluster          brkhsd220b6ktv7sjl50   warning   12 minutes ago   0         mylocation         4.5.23_1525_openshift   Default               satellite  
    ```
    {: screen}

5. Make sure that hosts are assigned as worker nodes to the cluster.
    * **Autoassignment**: If you included `--host-labels` when you created the cluster and you have available hosts with matching labels in your {{site.data.keyword.satelliteshort}} location, the worker nodes are automatically assigned to the cluster. If you don't have any available and matching hosts, the cluster is still created but enters a **Warning** state. [Attach hosts](/docs/satellite?topic=satellite-attach-hosts) to your {{site.data.keyword.satelliteshort}} location so that hosts can be assigned as worker nodes to the worker pool. If the hosts are not automatically assigned, you can also manually [assign {{site.data.keyword.satelliteshort}} hosts to your cluster](https://cloud.ibm.com/docs/satellite?topic=satellite-assigning-hosts).
    * **Manual assignment**: [Assign {{site.data.keyword.satelliteshort}} hosts to your cluster](https://cloud.ibm.com/docs/satellite?topic=satellite-assigning-hosts). After the hosts successfully bootstrap, the hosts function as the worker nodes for your cluster to run {{site.data.keyword.redhat_openshift_notm}} workloads. Generally, assign at least 3 hosts as worker nodes in your cluster.

6. Verify that your cluster reaches a **normal** state.
    ```sh
    ibmcloud oc cluster ls
    ```
    {: pre}

    Example output

    ```sh
    OK
    Name         ID                     State    Created        Workers   Location     Version                 Resource Group Name   Provider   
    satcluster   brkhsd220b6ktv7sjl50   normal   2 hours ago    3         mylocation   4.3.23_1525_openshift   Default               satellite   
    ```
    {: screen}

7. [Access your cluster](/docs/openshift?topic=openshift-access_cluster#access_cluster_sat) to run `oc` and `kubectl` commands or access the {{site.data.keyword.redhat_openshift_notm}} web console. If you enabled {{site.data.keyword.satelliteshort}} Config access, you must complete this step to synchronize the permissions.

If your location hosts have private network connectivity only, or if you use Amazon Web Services, Google Cloud Platform, or Microsoft Azure hosts, you must be connected to your hosts' private network, such as through VPN access, to connect to your cluster and access the {{site.data.keyword.redhat_openshift_notm}} web console. Alternatively, if your hosts have public network connectivity, you can test access to your cluster by changing your cluster's and location's DNS records to [use your hosts' public IP addresses](/docs/openshift?topic=openshift-access_cluster#sat_public_access).
{: note}




## Next steps
{: #sat-cluster-next-steps}

Accessing your cluster
:   Login to your cluster and verify pods are healthy and running. For more information, see [Accessing {{site.data.keyword.redhat_openshift_notm}} clusters on {{site.data.keyword.satelliteshort}}](/docs/openshift?topic=openshift-access_cluster#access_cluster_sat).

Setting up the internal image registry
:   By default, the internal registry does not run in your {{site.data.keyword.satelliteshort}} cluster because no backing storage is set up for the internal registry. You can set up the internal registry to use {{site.data.keyword.cos_short}}. For more information, see [Setting up the internal image registry for {{site.data.keyword.satelliteshort}} clusters](/docs/openshift?topic=openshift-satellite-clusters-registry).
    
Exposing apps
:   Several options exist to securely expose apps to traffic requests from the public network, from resources that are connected to your hosts' private network, or from resources in {{site.data.keyword.cloud_notm}}. Although these options include services that are available in standard {{site.data.keyword.redhat_openshift_notm}} clusters, the implementation of these services is different in {{site.data.keyword.redhat_openshift_notm}} clusters that were created on {{site.data.keyword.satelliteshort}}-provided infrastructure. For example, no load balancer services are created for the {{site.data.keyword.redhat_openshift_notm}} Ingress controller in your cluster. For a list of app exposure options and steps to configure them, see [Exposing apps in {{site.data.keyword.satelliteshort}} clusters](/docs/openshift?topic=openshift-sat-expose-apps).

Storing application data in persistent storage
:   Unlike standard {{site.data.keyword.redhat_openshift_notm}} clusters that are created on {{site.data.keyword.cloud_notm}} infrastructure, your {{site.data.keyword.satelliteshort}} clusters don't come installed with a storage driver that provides Kubernetes storage classes that are ready to use with Kubernetes persistent volumes for your apps. However, you can install your own storage driver to set up your apps to save their data in a backing storage device. Review the following common options. For more information, see [Understanding {{site.data.keyword.satelliteshort}} storage](/docs/satellite?topic=satellite-storage-template-ov).








