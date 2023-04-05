---

copyright:
  years: 2020, 2023
lastupdated: "2023-04-05"

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
1. Prepare to create your {{site.data.keyword.satellitelong_notm}} location. Choose from one of the following options.
    Note that support for automatically creating a Red Hat CoreOS enabled location with Schematics is currently not available. If you want to create a Red Hat CoreOS enabled location, see [Manually creating a location](/docs/satellite?topic=satellite-locations#location-create-console). Red Hat CoreOS is available in all supported {{site.data.keyword.satelliteshort}} locations and for {{site.data.keyword.redhat_openshift_notm}} version 4.9 and later.
    
    * You can automatically provision the hosts for your location. With this option, you create a custom role, or service ID, with your cloud provider credentials. This service ID is used to automatically provision virtual machines in your cloud provider. Once the VMs are provisioned and attached to your location, you can assign them to {{site.data.keyword.satellitelong_notm}} control plane or to the cloud services you want to use. To get started, see the [Automating your location set up with a {{site.data.keyword.bpshort}} template](/docs/satellite?topic=satellite-locations#satloc-template).
    * You can manually provision hosts either in your on-premises data center or in a public cloud. If you choose to manually provision the hosts for your location, make sure that your hosts meet the [minimum requirements](/docs/satellite?topic=satellite-host-reqs) and that you allow the [required outbound network access](/docs/satellite?topic=satellite-reqs-host-network). 
1. [Create an {{site.data.keyword.satellitelong_notm}} location](/docs/satellite?topic=satellite-locations).
1. Attach your hosts to your location and [set up your location control plane](/docs/satellite?topic=satellite-setup-control-plane).
1. [Attach at least 3 additional hosts to your location](/docs/satellite?topic=satellite-attach-hosts) to use as the worker nodes for your {{site.data.keyword.openshiftlong_notm}} cluster.



## Creating {{site.data.keyword.redhat_openshift_notm}} clusters on {{site.data.keyword.satelliteshort}} from the console
{: #satcluster-create-console}

Use the {{site.data.keyword.cloud_notm}} console to create your {{site.data.keyword.redhat_openshift_notm}} clusters on your {{site.data.keyword.satelliteshort}} infrastructure.
{: shortdesc}

1. [Complete the prerequisite steps](#satcluster-prereqs).
1. From the [{{site.data.keyword.redhat_openshift_notm}} clusters console](https://cloud.ibm.com/kubernetes/clusters?platformType=openshift){: external}, click **Create**.
1. In the **Infrastructure** section, select **{{site.data.keyword.satelliteshort}}**.
1. In the **OCP entitlement** section, specify an existing OCP entitlement for the worker nodes in this cluster by providing your [{{site.data.keyword.redhat_full}} account pull secret](https://console.redhat.com/openshift/install/pull-secret){: external} as a file or in raw JSON format. The cluster also uses this pull secret to download {{site.data.keyword.redhat_openshift_notm}} images from your own {{site.data.keyword.redhat_notm}} account.

1. In the **Location** section, select the {{site.data.keyword.satelliteshort}} location where you want to create the cluster. Make sure that the location that you select is in a **Normal** state.
1. In the **Operating System** section, select the operating system of the hosts that you want to use in the default worker pool of your cluster. In locations that are Red Hat CoreOS enabled, you can use either your RHCOS or RHEL hosts.
    In RHCOS enabled locations, when you want to add worker pools to your cluster, you can use RHCOS or RHEL hosts. Make sure to attach hosts with the operating system that you want to use to your location before assigning them to a worker pool.
    {: tip} 

1. In the **Worker pools** section, configure the details for your default worker pool.
    1. Select the **Satellite zones** that {{site.data.keyword.satelliteshort}} uses to evenly assign hosts across zones that represent zones in your underlying infrastructure provider. Generally, create your worker pool across 3 zones for high availability.
    1. Request the **vCPU**, **Memory (GB)**, and number of **Worker nodes per zone** that you want to create the worker pool with. {{site.data.keyword.satelliteshort}} can automatically assign available hosts to the worker pool to fulfill your request. Generally, select at least 1 worker node per zone for a total of 3 worker nodes in your cluster.
1. In the **{{site.data.keyword.satelliteshort}} Config** section, decide whether to enable cluster admin access for {{site.data.keyword.satelliteshort}} Config. If you don't grant {{site.data.keyword.satelliteshort}} Config access, you can't later use the {{site.data.keyword.satelliteshort}} Config functionality to view or deploy Kubernetes resources for your clusters. If you want to enable access later, you can [create custom RBAC roles for {{site.data.keyword.satelliteshort}} Config](/docs/satellite?topic=satellite-setup-clusters-satconfig-access).
1. For the **Resource details**, enter a **Cluster name** and any [{{site.data.keyword.cloud_notm}} tags](/docs/account?topic=account-tag) that you want to associate with your cloud resource. The cluster name must start with a letter, can contain letters, numbers, and hyphen (-), and must be 35 characters or fewer.
1. Click **Create**. When you create the cluster, the cluster master is automatically created in your {{site.data.keyword.satelliteshort}} location control plane, and your worker pool is automatically assigned available hosts that match your worker node request.
1. Wait for the cluster to reach a **Normal** state.

    If you don't have any available and matching hosts in your {{site.data.keyword.satelliteshort}} location, the cluster is still created but enters a **Warning** state. [Attach hosts](/docs/satellite?topic=satellite-attach-hosts) to your {{site.data.keyword.satelliteshort}} location so that hosts can be assigned as worker nodes to the worker pool. If the hosts are not automatically assigned, you can also manually [assign {{site.data.keyword.satelliteshort}} hosts to your cluster](/docs/satellite?topic=satellite-assigning-hosts#host-assign-manual). Ensure that hosts are assigned as worker nodes in each zone of your default worker pool.
    {: note}

1. From the [{{site.data.keyword.redhat_openshift_notm}} clusters console](https://cloud.ibm.com/kubernetes/clusters?platformType=openshift){: external}, verify that your cluster reaches a **Normal** state.
1. [Access your cluster](/docs/openshift?topic=openshift-access_cluster#access_cluster_sat) to access the {{site.data.keyword.redhat_openshift_notm}} web console or to run `oc` and `kubectl` commands from the CLI. If you enabled {{site.data.keyword.satelliteshort}} Config access, you must complete this step to synchronize the permissions.

    If your location hosts have private network connectivity only, or if you use Amazon Web Services, Google Cloud Platform, or Microsoft Azure hosts, you must be connected to your hosts' private network, such as through VPN access, to connect to your cluster and access the {{site.data.keyword.redhat_openshift_notm}} web console. Alternatively, if your hosts have public network connectivity, you can test access to your cluster by changing your cluster's and location's DNS records to [use your hosts' public IP addresses](/docs/openshift?topic=openshift-access_cluster#sat_public_access).
    {: note}

1. Optional: [Set up the internal container image registry](#satcluster-internal-registry).



## Creating {{site.data.keyword.redhat_openshift_notm}} clusters on {{site.data.keyword.satelliteshort}} from the CLI
{: #satcluster-create-cli}

Use the {{site.data.keyword.satelliteshort}} CLI to create your {{site.data.keyword.redhat_openshift_notm}} clusters on your {{site.data.keyword.satelliteshort}} infrastructure.
{: shortdesc}

Before you begin, [install the {{site.data.keyword.satelliteshort}} CLI plug-in](/docs/satellite?topic=satellite-setup-cli).

To create the cluster in a {{site.data.keyword.satelliteshort}} location, you must use {{site.data.keyword.redhat_openshift_notm}} version 4.5 or later. 
{: note}

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
    - To enable cluster admin access for {{site.data.keyword.satelliteshort}} Config, include the `--enable-admin-agent` option. If you don't grant {{site.data.keyword.satelliteshort}} Config access, you can't later use the {{site.data.keyword.satelliteshort}} Config functionality to view or deploy Kubernetes resources for your clusters. If you want to enable access later, you can [create custom RBAC roles for {{site.data.keyword.satelliteshort}} Config](/docs/satellite?topic=satellite-setup-clusters-satconfig-access). 
    - For more information about this command's options, see the [CLI reference documentation](/docs/openshift?topic=openshift-kubernetes-service-cli#cli_cluster-create-satellite).
    
    `--operating-system REDHAT_7_64|REDHAT_8_64|RHCOS`
:   Optional. The operating system of the worker nodes in your cluster. For a list of available operating sysems by cluster version, see [Available {{site.data.keyword.redhat_openshift_notm}} versions](/docs/openshift?topic=openshift-openshift_versions#openshift_versions_available). Note that to use your `RHCOS` hosts in your clusters, you must create a Red Hat CoreOS-enabled location and a cluster that runs version 4.9 or later. If no option is specified, the default [operating system that corresponds to the cluster version](/docs/openshift?topic=openshift-openshift_versions#openshift_versions_available) is used.

    
    Example `cluster create` command.

    ```sh
    ibmcloud oc cluster create satellite --location <location_name_or_ID> --name <cluster_name> --pull-secret <secret> --version 4.10_openshift [--enable-admin-agent] [--host-label LABEL ...] [--operating-system (REDHAT_7_64|REDHAT_8_64|RHCOS)] [--pod-subnet SUBNET] [-q] [--service-subnet SUBNET] [--workers <workers_per_zone>] [--zone <zone_name>]
    ```
    {: pre}
    
    Example `cluster create` command using `RHCOS` hosts and cluster version `4.9.23_1122`.
    ```sh
    ibmcloud oc cluster create satellite --location <location_name_or_ID> --name <cluster_name> --pull-secret <secret> --version 4.9.23_1122_openshift --enable-admin-agent --operating-system RHCOS 
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
    * **Autoassignment**: If you included `--host-labels` when you created the cluster and you have available hosts with matching labels in your {{site.data.keyword.satelliteshort}} location, the worker nodes are automatically assigned to the cluster. If you don't have any available and matching hosts, the cluster is still created but enters a **Warning** state. [Attach hosts](/docs/satellite?topic=satellite-attach-hosts) to your {{site.data.keyword.satelliteshort}} location so that hosts can be assigned as worker nodes to the worker pool. If the hosts are not automatically assigned, you can also manually [assign {{site.data.keyword.satelliteshort}} hosts to your cluster](/docs/satellite?topic=satellite-assigning-hosts#host-assign-manual).
    * **Manual assignment**: [Assign {{site.data.keyword.satelliteshort}} hosts to your cluster](/docs/satellite?topic=satellite-assigning-hosts#host-assign-manual). After the hosts successfully bootstrap, the hosts function as the worker nodes for your cluster to run {{site.data.keyword.redhat_openshift_notm}} workloads. Generally, assign at least 3 hosts as worker nodes in your cluster.

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

8. Optional: [Set up the internal container image registry](#satcluster-internal-registry).

After you [access your cluster](/docs/openshift?topic=openshift-access_cluster#access_cluster_sat) and run `oc get nodes` or `oc describe node <worker_node>`, you might see that the worker nodes have `master,worker` roles. In OpenShift Container Platform clusters, operators use the master role as a `nodeSelector` so that OCP can deploy default components that are controlled by operators, such as the internal registry, in your cluster. The {{site.data.keyword.satelliteshort}} hosts that you assigned to your cluster function as worker nodes only, and no master node processes, such as the API server or Kubernetes scheduler, run on your worker nodes.
{: note}


## Creating single-node clusters for resource-constrained edge locations
{: #single-node}

If you are running your {{site.data.keyword.openshiftlong_notm}} cluster on {{site.data.keyword.satelliteshort}} infrastructure in a remote, resource-constrained edge location with limited resources, such as a small data center in a mobile tower, running a data plane with a smaller foot print might be beneficial for your setup. While typical {{site.data.keyword.openshiftlong_notm}} clusters require at least three worker nodes for high availability, you have the option to create a cluster that runs a single worker node. Single-node clusters have several limitations and should only be used in specific circumstances. 
{: shortdesc}

Single-node clusters are recommended only in specific circumstances, and should only be used in resource-constrained edge locations that have multiple redundant locations running the same workload. See the [Limitations](#single-node-limitations) section for more information. 
{: important}

Single-node clusters lack high availability. By provisioning a single-node cluster, you accept that you are more likely to experience downtime and disruptions in your workload.
{: important}

### Limitations
{: #single-node-limitations}

Any cluster with fewer than three worker nodes lacks high availability. By provisioning a single-node cluster, you accept that you are more likely to experience downtime and disruptions in your workload, and that regular worker node upgrades result in your workload going offline. Additionally, if a cluster is provisioned as a single-node cluster, it can not later be converted to a standard, highly available cluster. You can add more nodes, but standard deployments do not increase in replica size and the cluster does not become highly available. 
{: shortdesc}

* OpenShift Data Foundation is not supported on single-node clusters.
* Portworx is not supported on single-node clusters.

### Requirements
{: #single-node-requirements}

Single-node clusters must meet the following requirements:
{: shortdesc}

* Must run on a {{site.data.keyword.satelliteshort}} location with [CoreOS enabled](/docs/satellite?topic=satellite-locations#verify-coreos-location).
* Control plane hosts on your location and the host you assign to your single-node cluster must run either the RHEL 8 or RHCOS operating systems.
* Only supported for {{site.data.keyword.satelliteshort}} clusters that run version 4.11 or later.

### Creating a single-node cluster
{: #single-node-create}

You can create a single-node cluster by including the `--infrastructure-topology` option and specifying the `single-replica` value when [creating a {{site.data.keyword.satelliteshort}} cluster in the CLI](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster). If this option is not included, the cluster is provisioned with the highly available setup of three worker nodes by default.
{: shortdesc}


## Accessing and working with your {{site.data.keyword.satelliteshort}} clusters
{: #satcluster-access}

After you created your {{site.data.keyword.redhat_openshift_notm}} cluster, you can use the capabilities in {{site.data.keyword.openshiftlong_notm}} to work with your cluster.
{: shortdesc}

Review common tasks that you might be interested in:

- [Accessing {{site.data.keyword.redhat_openshift_notm}} clusters on {{site.data.keyword.satelliteshort}}](/docs/openshift?topic=openshift-access_cluster#access_cluster_sat)
- [Assigning cluster access](/docs/openshift?topic=openshift-users)



## Setting up the internal container image registry
{: #satcluster-internal-registry}

By default, the internal registry does not run in your {{site.data.keyword.satelliteshort}} cluster because no backing storage is set up for the internal registry. Review the following options to set up the internal registry.
{: shortdesc}

*  **Non-persistent data on the worker node**: See [Storing images in the worker node empty directory](/docs/openshift?topic=openshift-registry#emptydir_internal_registry).
*  **Persistent data in {{site.data.keyword.cos_full_notm}}**: See [Setting up the internal container image registry with {{site.data.keyword.cos_full_notm}}](#satcluster-internal-registry-cos)

By default, the [image registry operator management state](https://docs.openshift.com/container-platform/4.10/registry/configuring-registry-operator.html#registry-operator-configuration-resource-overview_configuring-registry-operator){: external} is set to `Unmanaged`. After you change the storage section in the ConfigMap to use a different solution such as the `emptyDir`, you must update the management state to `Managed`. Then, the operator creates the internal registry pod. Use the following command: `oc patch configs.imageregistry.operator.openshift.io/cluster --type merge -p '{"spec":{"managementState":"Managed"}}'`
{: note}

### Setting up the internal container image registry with {{site.data.keyword.cos_full_notm}}
{: #satcluster-internal-registry-cos}

You can configure the internal image registry in your {{site.data.keyword.satelliteshort}} cluster with {{site.data.keyword.cos_full_notm}} as the backing storage.
{: shortdesc}

1. Determine if you have an {{site.data.keyword.cos_full_notm}} instance that meets the requirements.
    1. In the {{site.data.keyword.cloud_notm}} console, navigate to the **Resources** menu and list your storage instances. 
    2. Identify your {{site.data.keyword.cos_short}} instances and find the **Location** column. If an instance was created in {{site.data.keyword.cloud_notm}}, its location is listed as **Global**.
    3. If you do not have an instance that meets the requirements, follow the steps to create one.
        1. From the {{site.data.keyword.cos_full_notm}}, click **Create Instance**.
        2. Under **Choose an Infrastructure**, select the **{{site.data.keyword.cloud_notm}}** option. 
        3. Select a pricing plan and a service name.
        4. Choose the resource group where your {{site.data.keyword.satelliteshort}} components are stored.
        5. Click create. Note that it might take several minutes for your instance to provision.
2. Create a bucket to use when you set up your image registry. Your bucket must be configured with regional resiliency. For more information on creating bucket, see [Setting up {{site.data.keyword.cos_full_notm}}](/docs/containers?topic=containers-storage-cos-understand).
    1. Click on your {{site.data.keyword.cos_short}} instance.
    2. Click **Create a bucket**.
    3. Select the option to **Customize your bucket**.
    4. Under **Resiliency**, select **Regional**.
    5. From the **Location** drop down menu, choose the region that is closest to where your location is managed from. For example, if your location is managed from `wdc` (Washington, DC), choose the `us-east` region. To check where a {{site.data.keyword.satelliteshort}} location is managed from, run `ibmcloud sat location ls` in the CLI.
    6. Under **Storage class**, select **Standard**.
    7. Configure the remaining categories to your preferences.
    8. Click **Create bucket**.
3. Create service credentials that enable your cluster to communicate with your {{site.data.keyword.cos_short}} instance.
    1. In the navigation pane, click **Service credentials**, then click **New credential**.
    2. Enter a name for the new credential.
    3. From the drop down menu, choose the **Writer** role. 
    4. Click **Advanced options**, then select the option to **Include HMAC Credential**.
    5. Click **Add**.
    6. In the **Service Credentials** table, expand your new credential. Note the `access_key_id` and the `secret_access_key_id`. Do not share these credentials with anyone. 
        Example credentials to save. 
        ```sh
        "cos_hmac_keys": {
            "access_key_id": "1111111a1111111a11aa1a111111111a11aa1a111a11a1a1",
            "secret_access_key": "222222b222222b22bb2b22222222b22bb2b222b22b2b2"
        }
        ```
        {: screen}
        
4. In the CLI, create a secret with the service credentials you created and saved.
    1. [Log in to your account. If applicable, target the appropriate resource group. Set the context for your cluster.](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure)
    2. Create the secret.
        ```sh
        oc create secret generic image-registry-private-configuration-user --from-literal=REGISTRY_STORAGE_S3_ACCESSKEY=<access_key_id> --from-literal=REGISTRY_STORAGE_S3_SECRETKEY=<secret_access_key> --namespace openshift-image-registry
        ```
        {: pre}
        
5. Change the management state of the {{site.data.keyword.redhat_openshift_notm}} Register operator.
    ```sh
    oc patch configs.imageregistry.operator.openshift.io cluster --type merge --patch '{"spec":{"managementState":"Managed"}}'
    ```
    {: pre}
    
6. Edit the configuration storage attributes to store images in your {{site.data.keyword.cos_short}} bucket.
    1. Find and save your {{site.data.keyword.satelliteshort}} location's regional link endpoint. In the output, the endpoint is listed under the **Address** column.
        ```sh
        ibmcloud sat endpoint ls --location <location_name> | grep satellite-cosRegional
        ```
        {: pre}

        Example output.
        ```sh
        ID                           Name                                              Destination Type   Address       
        cavvku1p1h1gcfgk1kn1_uwokw   satellite-cosRegional-cavvku1p1h1gcfgk1kn1        cloud              TLS   i11aa11a1a1a11a11-1a11a1aaa1a1a1a1a-c000.us-east.satellite.appdomian.cloud:11111 
        ```
        {: pre}
        
    1. Open the file editor in the CLI.
        ```sh
        oc edit configs.imageregistry.operator.openshift.io/cluster
        ```
        {: pre}
        
    1. Find the following section to edit. 
        ```sh
        storage:
            emptyDir: {}
            managementState: Managed
        storageManaged: true
        ```
        {: screen}
        
    1. Replace `emptyDir: {}` with your bucket information and location endpoints.
        ```sh
            s3:
            bucket: <bucket_name>
            region: <bucket_region>
            regionEndpoint: <location_link_endpoint>
            virtualHostedStyle: false
        ```
        {: screen}
        
        Example section after adding the bucket and location information.
        ```sh
          storage:
            managementState: Managed
            s3:
            bucket: my_bucket
            region: us-east
            regionEndpoint: https://i11aa11a1a1a11a11-1a11a1aaa1a1a1a1a-c000.us-east.satellite.appdomian.cloud:11111
            virtualHostedStyle: false
          storageManaged: true
        ```
        {: screen}
        
    1. Save and apply the changes.
7. Verify that the image registry was configured by checking for a pod that begins with `image-registry-` in the `openshift-image-registry` namespace. 
    ```sh
    oc get pod -n openshift-image-registry
    ```
    {: pre}

    Example output.
    ```sh
    NAME                                               READY   STATUS      RESTARTS      AGE
    image-registry-63p54b8add-vkjju                    1/1      Running      0              16m
    ```
    {: screen}
    

## Exposing apps
{: #satcluster-expose-apps}

Several options exist to securely expose apps to traffic requests from the public network, from resources that are connected to your hosts' private network, or from resources in {{site.data.keyword.cloud_notm}}. Although these options include services that are available in standard {{site.data.keyword.redhat_openshift_notm}} clusters, the implementation of these services is different in {{site.data.keyword.redhat_openshift_notm}} clusters that were created on {{site.data.keyword.satelliteshort}}-provided infrastructure. For example, no load balancer services are created for the {{site.data.keyword.redhat_openshift_notm}} Ingress controller in your cluster. For a list of app exposure options and steps to configure them, see [Exposing apps in {{site.data.keyword.satelliteshort}} clusters](/docs/openshift?topic=openshift-sat-expose-apps).

## Storing application data in persistent storage
{: #satcluster-storage}

Unlike standard {{site.data.keyword.redhat_openshift_notm}} clusters that are created on {{site.data.keyword.cloud_notm}} infrastructure, your {{site.data.keyword.satelliteshort}} clusters don't come installed with a storage driver that provides Kubernetes storage classes that are ready to use with Kubernetes persistent volumes for your apps. However, you can install your own storage driver to set up your apps to save their data in a backing storage device. Review the following common options. For more information, see [Understanding {{site.data.keyword.satelliteshort}} storage](/docs/satellite?topic=satellite-storage-template-ov).




## Removing {{site.data.keyword.satelliteshort}} worker nodes or clusters
{: #satcluster-rm}

When you remove {{site.data.keyword.redhat_openshift_notm}} clusters or worker nodes in a cluster, the hosts that provide the compute capacity for your worker nodes are not automatically deleted. Instead, the hosts remain attached to your {{site.data.keyword.satelliteshort}} location, but require you to reload the host to be able to reassign the hosts to other {{site.data.keyword.satelliteshort}} resources.

1. Back up any data that runs in the worker node or cluster that you want to save. For example, you might save a copy of all the data in your cluster and upload these files to a persistent storage solution, such as {{site.data.keyword.cos_full_notm}}.
    ```sh
    oc get all --all-namespaces -o yaml
    ```
    {: pre}

2. Get the **Worker ID** of each host in your cluster.
    ```sh
    ibmcloud sat host ls --location <satellite_location_name_or_ID>
    ```
    {: pre}

    Example output

    ```sh
    Retrieving hosts...
    OK
    Name              ID                     State      Status   Cluster          Worker ID                                                 Worker IP       
    machine-name-1    aaaaa1a11aaaaaa111aa   assigned   Ready    infrastructure   sat-virtualser-4d7fa07cd3446b1f9d8131420f7011e60d372ca2   169.xx.xxx.xxx       
    machine-name-2    bbbbbbb22bb2bbb222b2   assigned   Ready    infrastructure   sat-virtualser-9826f0927254b12b4018a95327bd0b45d0513f59   169.xx.xxx.xxx       
    machine-name-3    ccccc3c33ccccc3333cc   assigned   Ready    mycluster12345   sat-virtualser-948b454ea091bd9aeb8f0542c2e8c19b82c5bf7a   169.xx.xxx.xxx       
    ```
    {: screen}

3. Remove the worker nodes or clusters by referring to the following options. The corresponding hosts in your {{site.data.keyword.satelliteshort}} location become unassigned and require a reload before you can use them for other {{site.data.keyword.satelliteshort}} resources.
    *  [Resize worker pools](/docs/openshift?topic=openshift-add_workers#resize_pool) to reduce the number of worker nodes in the cluster.
    *  [Remove individual worker nodes](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_rm) from the cluster.
    *  [Remove the cluster](/docs/openshift?topic=openshift-remove).
4. For each worker node that you removed, decide what to do with the corresponding host in your {{site.data.keyword.satelliteshort}} location.
    *  Reload the host operating system so that you can re-attach and re-assign the host to other {{site.data.keyword.satelliteshort}} resources such as the location control plane or other clusters. For more information, see the update process in [Updating {{site.data.keyword.satelliteshort}} location control plane hosts](/docs/satellite?topic=satellite-host-update-location).
    *  Delete the hosts from your underlying infrastructure provider. For more information, refer to the infrastructure provider documentation.

   

## Limitations for {{site.data.keyword.redhat_openshift_notm}} clusters in {{site.data.keyword.satellitelong_notm}}
{: #satcluster-limitations}

See [{{site.data.keyword.satelliteshort}} cluster limitations](/docs/openshift?topic=openshift-openshift_limitations#satellite_limits).
{: shortdesc}

## Pricing for clusters in {{site.data.keyword.satelliteshort}}
{: #satcluster-pricing}

Review the table for information on charges related to {{site.data.keyword.redhat_openshift_notm}} clusters in {{site.data.keyword.satellitelong_notm}}. For information about Location pricing, see [{{site.data.keyword.satelliteshort}} pricing](/docs/satellite?topic=satellite-sat-pricing).
{: shortdesc}

Looking for an estimate? Try the [Cost estimator](/docs/billing-usage?topic=billing-usage-cost#cost) or review the [Pricing model](https://www.ibm.com/cloud/satellite/pricing){: external}
{: tip}

| Type of charge | Clusters created after 15 November 2022 | Clusters created before 15 November 2022 | What the charge covers |
| --- | --- | --- | --- |
| Cluster management fee | A flat monthly fee for the cluster, charged hourly. | Per vCPU hour of the hosts that are assigned to the cluster as worker nodes | The benefits of {{site.data.keyword.openshiftlong_notm}}, such as installation and security patch updates of OpenShift Container Platform for your worker nodes; managing your cluster with a suite of API, CLI, and UI tools; integration with {{site.data.keyword.cloud_notm}} platform tooling such as IAM; continuous monitoring by {{site.data.keyword.IBM_notm}} Site Reliability Engineers; access to {{site.data.keyword.cloud_notm}} support; and more. |
| Worker node management fee | Per vCPU hour of the hosts that are assigned to the cluster as worker nodes. | Per vCPU hour of the hosts that are assigned to the cluster as worker nodes. | The benefits of {{site.data.keyword.satellitelong_notm}}, such as to create the cluster on any compatible infrastructure that you want; tooling to consistently deploy apps, storage drivers, and endpoints across the location; integration with {{site.data.keyword.cloud_notm}} platform tooling such as IAM; continuous monitoring by {{site.data.keyword.IBM_notm}} Site Reliability Engineers; access to {{site.data.keyword.cloud_notm}} support; and more. |
| OCP licensing fee | Per vCPU hour. You can either purchase a license during cluster creation or [bring your own](#byo-ocp-satellite). | Per vCPU hour. You can either purchase a license during cluster creation or [bring your own](#byo-ocp-satellite). |
{: caption="Red Hat OpenShift cluster on Satellite charges." caption-side="bottom"}



## Bringing your own OCP license
{: #byo-ocp-satellite}



All user clusters in your Satellite location are installed with OpenShift Container Platform, which incurs a licensing fee from Red Hat. However, you can bring your own OpenShift Container Platform license for clusters created with your on-premises infrastructure or for clusters created by using IBM Cloud Paks.
{: shortdesc}


When you create the cluster, make sure to include your Red Hat pull secret to entitle the cluster to run OCP, either by uploading the pull secret in the console or by including the `--pull-secret` option in the `ibmcloud oc cluster create satellite` [command](/docs/openshift?topic=openshift-kubernetes-service-cli#cli_cluster-create-satellite).

Service clusters, which are the underlying platform for all {{site.data.keyword.cloud_notm}} services are created by services such as {{site.data.keyword.keymanagementserviceshort}} or {{site.data.keyword.cos_full_notm}} and do not require a license.



