---

copyright:
  years: 2025, 2026
lastupdated: "2026-02-26"


keywords: openshift, openshift data foundation, openshift container storage, disaster recovery

subcollection: openshift

---


{{site.data.keyword.attribute-definition-list}}


# OpenShift Data Foundation Regional Disaster Recovery on {{site.data.keyword.openshiftlong_notm}} clusters
{: #openshift_odf_rdr_roks}

[Virtual Private Cloud]{: tag-vpc}
[4.17 and later]{: tag-red}

Regional Disaster Recovery ensures business continuity during the unavailability of a geographical region. You can use Red Hat Advanced Cluster Management (ACM) to set up the Regional Disaster Recovery solutions for ODF clusters.
{: shortdesc}

The following steps for setting ODF Disaster Recovery are available as a **Technical Preview** only and **not for production use**. For information on ACM specificially, see (Setting up the ACM add-on)[/docs/openshift?topic=openshift-acm&interface=ui].
{: preview}

Here are the high-level steps of this solution:
1. Create 3 VPC clusters, each in different regions or VPCs, and allow outbound traffic on each. One will be the hub cluster that you install ACM on to. The remaining 2 will be the managed ODF clusters (1 primary and 1 secondary backup).
1. Install ACM on 1 of the clusters you created. This will be the hub cluster.
1. Configure ACM and import the remaining 2 clusters so they can be managed by ACM. These will be the managed clusters.
1. Install Submariner on the 2 managed clusters to establish connectivity between them.
1. Install ODF on the 2 managed clusters. 
1. Configure the Regional Disaster Recovery policy. 

With this set up, the hub cluster that you installed ACM on manages the ODF clusters. In the event that your primary ODF cluster becomes unavailable, the hub cluster rolls over the apps and data from the primary ODF cluster to the secondary ODF cluster.

## Applications and workloads supported for Regional Disaster Recovery
{: #app_support}

Review the types of applications and workloads that you can apply Regional Diaster Recovery for. 

Subscription-based
:   An application is deployed from an external source, such as GitHub, a Helm repo, or Object Storage. 
:   For more information, see [Creating a sample Subscription-based application](https://docs.redhat.com/en/documentation/red_hat_openshift_data_foundation/4.19/html-single/configuring_openshift_data_foundation_disaster_recovery_for_openshift_workloads/index#subscription-based-apps_manage-mdr){: external} in the Red Hat documentation.

ApplicationSet-based
:   An application is depoyed from a GitHub repo using the GitOps operator, which manages continuous delivery. This includes two subtypes:
:   - **GitOps Pull Model (ArgoCD pull)**: A managed cluster pulls the application from GitHub using the GitOps operator. 
:   - **GitOps Push Model (ArgoCD push)**: The GitOps operator pushes the application to the managed cluster during deployments and updates. 
:   For more information, see [Creating Application-set based applications](https://docs.redhat.com/en/documentation/red_hat_openshift_data_foundation/4.19/html-single/configuring_openshift_data_foundation_disaster_recovery_for_openshift_workloads/index#creating-applicationset-application_manage-mdr){: external} in the Red Hat documentation.
:   For more information on the GitOps subtypes, see [Deploying Argo CD with Push and Pull model](https://docs.redhat.com/en/documentation/red_hat_advanced_cluster_management_for_kubernetes/2.15/html/gitops/gitops-overview#gitops-push-pull){: external} in the Red Hat documentation. 

Discovered applications
:   An application was pre-deployed in a managed cluster without using ACM. In this case, you can use ACM discovery for the pre-installed app and still configure the DR policy. 
:  For more information, see [Disaster recovery protection for discovered applications](https://docs.redhat.com/en/documentation/red_hat_openshift_data_foundation/4.20/html-single/configuring_openshift_data_foundation_disaster_recovery_for_openshift_workloads/index#protect-discovered-apps-regionaldr_manage-rdr){: external} in the Red Hat documentation. 

Applications that include VM deployments
:   A VM-based application is deployed onto the managed cluster from the ACM console. These VM applications can be subscription based, applicationSet based, or discovered, as described previously. Options to start, stop, pause and delete VM operations are available from the ACM console for these types of applications. 
:   For more information, see [Red Hat Advanced Cluster Management for Virtualization](https://www.redhat.com/en/resources/advanced-cluster-management-for-virtualization-datasheet){: external} in the Red Hat documentation. 


## Step 1. Creating the clusters
{: #clusters-cli}
{: cli}

Create 3 [VPC clusters](/docs/openshift?topic=openshift-cluster-create-vpc-gen2) in different regions. 
{: shortdesc} 

For each cluster, make sure to allow outbound traffic by including the `--disable-outbound-traffic-protection` parameter in the CLI or selecting the option to disable outbound traffic protection in the UI.
{: important}

1. [Create a VPC cluster](/docs/openshift?topic=openshift-cluster-create-vpc-gen2) in `us-east` to install ACM on. This is the hub cluster that you can use to manage your ODF clusters. Make sure your hub cluster has at least 3 worker nodes that run RHCOS and a minimum of 6 VCPU and 64 GB, and meets all of the [prequisites for ACM](/docs/openshift?topic=openshift-acm&interface=ui#before). The following example command creates a cluster for ACM in `us-east`.

    ```sh
    ibmcloud ks cluster create vpc-gen2 --flavor bx2.8x32 --name acm-hub-cluster-dr-odf --subnet-id 0101-0a10101-01a0-1a010-a10b-a101a0a101a0 --vpc-id r010-1aa01a0a-11a0-101a-01aa-1aaa0aaa1001 --zone us-east-2 --version 4.19.23_openshift --workers 3 --cos-instance crn:v1:bluemix:public :cloud-object-storage:global:a/a101a0101010aaaa1a0101aa0a101aa0:000aaaa-aaaa-10aa-a01a-aa1a01aa10a0:: --disable-outbound-traffic-protection
    ```
    {: pre}

1. If you have not already done so, make sure your hub cluster has a [trusted profile](/docs/openshift?topic=openshift-acm&interface=ui#trust-prof) for ACM.

1. [Create a VPC cluster](/docs/openshift?topic=openshift-cluster-create-vpc-gen2) in `us-east` with at least 3 worker nodes that run RHCOS and a minimum flavor of `6x64` and with outbound traffic protection disabled. This will be the primary managed ODF cluster. The following example command creates a cluster in `us-east.`

    ```sh
    ibmcloud ks cluster create vpc-gen2 --flavor bx2.8x32 --name managed-cluster-1-dr-odf --subnet-id 0101-0a10101-01a0-1a010-a10b-a101a0a101a0 --vpc-id r010-1aa01a0a-11a0-101a-01aa-1aaa0aaa1001 --zone us-east-2 --version 4.19.23_openshift --workers 3 --cos-instance crn:v1:bluemix:public :cloud-object-storage:global:a/a101a0101010aaaa1a0101aa0a101aa0:000aaaa-aaaa-10aa-a01a-aa1a01aa10a0:: --disable-outbound-traffic-protection
    ```
    {: pre}


1. [Create a VPC cluster](/docs/openshift?topic=openshift-cluster-create-vpc-gen2) in `jp-tok` with at least 3 worker nodes that run RHCOS and a minimum flavor of `6x64` and with outbound traffic protection disabled. This will be the secondary managed ODF cluster. For high availability, make sure that the secondary cluster's network does not overlap with the primary cluster's network. The following example command creates a cluster in `jp-tok`.

    ```sh
    ibmcloud ks cluster create vpc-gen2 --flavor bx2.8x32 --name managed-cluster-2-dr-odf --subnet-id 0101-0a10101-01a0-1a010-a10b-a101a0a101a0 --vpc-id r010-1aa01a0a-11a0-101a-01aa-1aaa0aaa1001 --zone jp-tok --version 4.19.23_openshift --workers 3 --cos-instance crn:v1:bluemix:public :cloud-object-storage:global:a/a101a0101010aaaa1a0101aa0a101aa0:000aaaa-aaaa-10aa-a01a-aa1a01aa10a0:: --disable-outbound-traffic-protection
    ```
    {: pre}


## Step 2. Install ACM on the hub cluster
{: #hub-acm-install} 

Prepare your hub cluster and install ACM.

1. For both the primary and seconday managed clusters, create the [required secrets for ACM](/docs/openshift?topic=openshift-acm&interface=ui#prep-secret). This step is required to manage your ODF clusters with the hub cluster. Note that these instructions also include creating secrets on the hub cluster. 

2. Follow the steps to [install the ACM add-on onto the hub cluster](/docs/openshift?topic=openshift-acm&interface=cli). You do not need to repeat the instruction to prepare secrets on the cluster if you completed the previous step. 

## Step 3. Import the clusters to be managed by the hub cluster
{: #import}

Follow the steps to [import the primary and secondary managed clusters](/docs/openshift?topic=openshift-acm#import) so that they can be managed by the hub cluster. 


## Step 4. Configure the Submariner add-on
{: #submariner}

Follow the steps to install and configure the Submariner add-on, which establishes connectivity across your two managed clusters. These steps use the ACM console. For more detailed information, see [Deploying Subarminer by using the console](https://docs.redhat.com/en/documentation/red_hat_advanced_cluster_management_for_kubernetes/2.11/html/networking/networking#deploying-submariner-console){: external} in the Red Hat Documentation. 

1. Navigate to the ACM console. Then click **Fleet Management** > **Infrastructure** > **Clusters** > **Clusterset**. 
1. Click **Create a cluster set**. Follow the prompts to add your two managed clusters to the cluster set. 
1. Click the option to install the Submariner add-on to the cluster set.
1. Select the managed clusters as target clusters for add-on installation. 
1. When reviewing the configuration for both clusters, change the following settings as shown and leave the rest as default. Then click **Install**.
    ```sh
    globalnetEnabled: true (checked)
    gateways: 2
    NATTEnable: false (unchecked)
    cableDriver: vxlan.
    ```
    {: code}
    
1. Wait for the Submariner add-on status to show healthy (green). This can take up to 20 minutes. 


## Step 5. Install and configure OpenShift Data Foundation
{: #odf_install}

Install and configure ODF on your 2 managed clusters. Make sure to complete these steps on both the primary and secondary managed cluster. 

1. Follow the steps to [install the OpenShift Data Foundation add-on](/docs/openshift?topic=openshift-deploy-odf-vpc&interface=cli#install-odf-cli-vpc) onto your 2 managed clusters. Specify the default ODF version or later. Make sure you include the option to enable NooBaa as an add-on option during the installation. 

1. Verify that the ODF foundation installed successfully. In the output, check that the status says `Ready`.
    ```sh
    oc get storagecluster -n openshift-storage ocs-storagecluster -o jsonpath='{.status.phase}{"\n"}'
    ```
    {: pre}

1. Run the command to update the `ACM Managed Cluster Name` in the `storageCluster` resource’s `multiClusterService` section. This allows ODF to use GlobalNet. For more information, see [Creating an OpenShift Data Foundation cluster on managed clusters](https://docs.redhat.com/documentation/red_hat_openshift_data_foundation/4.17/html/configuring_openshift_data_foundation_disaster_recovery_for_openshift_workloads/rdr-solution#creating-odf-cluster-on-managed-clusters_rdr){: external}.

    Make sure to replace `<managed_cluster_name>` in the command with the name of your managed cluster.
    {: important}

    ```sh
    kubectl patch storagecluster -n openshift-storage ocs-storagecluster --type merge -p'{"spec":{"network":{"multiClusterService":{"clusterID":"<managed_cluster_name>","enabled":true}}}}’
    ```
    {: pre}

1. Verify the service exports. This might take a few minutes to show in the output.
    ```sh
    oc get serviceexport -n openshift-storage
    ```
    {: pre}   

    Example output:   
    ```sh
    NAME              AGE
    rook-ceph-mon-d   4d14h
    rook-ceph-mon-e   4d14h
    rook-ceph-mon-f   4d14h
    rook-ceph-osd-0   4d14h
    rook-ceph-osd-1   4d14h
    rook-ceph-osd-2   4d14h
    ```
    {: screen} 

1. Create a service export for `ocs-provider-server` by using the following YAML.
    
    ```yaml
    apiVersion: multicluster.x-k8s.io/v1alpha1
    kind: ServiceExport
    metadata:
      name: ocs-provider-server
      namespace: openshift-storage
    ```
    {: screen}

1. Run the command to update the `storageCluster` resource to use the `ocs-provider-server` service export you created.
  
    ```sh
    oc annotate storagecluster ocs-storagecluster -n openshift-storage ocs.openshift.io/api-server-exported-address=<managed_cluster_name>.ocs-provider-server.openshift-storage.svc.clusterset.local:500511. 
    ```
    {: pre}

1. Verify that the `storageCluster` resource is ready. 

    ```sh
    oc get storagecluster -n openshift-storage
    ```
    {: pre} 

    Example output. 

    ```sh
    NAME                    PHASE   
    ocs-storagecluster      Ready    
    ```
    {: screen}


## Step 6. Configure the Regional Diaster Recovery policy
{: #rdr-configure}

Configure the ODF RDR policy. 

1. Follow the steps to [install the ODF Multicluster Orchestrator](https://docs.redhat.com/en/documentation/red_hat_openshift_data_foundation/4.16/html-single/configuring_openshift_data_foundation_disaster_recovery_for_openshift_workloads/index#installing-odf-multicluster-orchestrator_mdr){: external} onto the **ACM hub cluster**. To ensure compatibility, make sure you install the **same version number** as the ODF version you installed onto the managed clusters in the previous section. 
1. Verify the installation by checking that the operator pods are running. 

    ```sh
    oc get pods -n openshift-operators
    ```
    {: pre}

    Example output.

    ```sh
    NAME                                        READY   STATUS       RESTARTS    AGE
    odf-multicluster-console-6845b795b9-blxrn   1/1     Running      0           4d20h
    odfmo-controller-manager-f9d9dfb59-jbrsd    1/1     Running      0           4d20h
    ramen-hub-operator-6fb887f885-fss4w         2/2     Running      0           4d20h
    ```
    {: pre}

1. On the **ACM hub cluster**, create a DR policy with a 5 minute sync interval and specify each managed cluster in the parameters. This creates NooBaa object buckets on both managed clusters and enables ODF Ceph block pool mirroring for volume replication. 
  1. Navigate to the ACM console, then click **Fleet management** > **Data services** > **Disaster Recovery** > **Policies** > **Create DR Policy**.
  2. Create a DR policy that includes the following parameters.
      - Connected clusters: <primary_managed_cluster_name>, <secondary_managed_cluster_name>
      - Replication policy: Asynchronous
      - Replication interval: 5m

1. On the hub cluster, run the commands to verify that the DR policy was created and applied to the managed clusters. 

    ```sh
    oc get drpolicy <drpolicy_name> -o jsonpath='{.status.conditions[].reason}{"\n"}
    ```
    {: pre}
    
    ```sh
    oc get drclusters
    ```
    {: pre}

    Example output. 

    ```sh
    NAME        AGE
    managed-cluster1   4m42s
    managed-cluster2   4m42s
    ```
    {: screen}
  
1. On each managed cluster, verify that the DR policy was applied and is in a healthy state.

    ```sh
    oc get csv,pod -n openshift-dr-system
    ```
    {: pre}

    Example output.

    ```sh
    NAME                                                                          DISPLAY                         VERSION        REPLACES   PHASE
    clusterserviceversion.operators.coreos.com/odr-cluster-operator.v4.15.0       Openshift DR Cluster Operator   4.15.0                    Succeeded
    clusterserviceversion.operators.coreos.com/volsync-product.v0.8.0             VolSync                         0.8.0                     Succeeded

    NAME                                             READY   STATUS    RESTARTS   AGE
    pod/ramen-dr-cluster-operator-6467cf5d4c-cc8kz   2/2     Running   0          3d12h
    ```
    {: screen}

    ```sh
    oc get cephblockpool ocs-storagecluster-cephblockpool -n openshift-storage -o jsonpath='{.status.mirroringStatus.summary}{"\n"}'
    ```
    {: pre}

    Example output.

    ```sh
    {"daemon_health":"OK","health":"OK","image_health":"OK","states":{}}
    ```
    {: screen}

1. **Optional**: Review the [operators](#operators) you can install to enhance ODF Regional Disaster Recovery features.

1. **Optional**: [Test your disaster recovery configuration](#odf-rdr-test). 

## Optional operators for ODF Regional Disaster Recovery
{: #operators}

Review the optional operators you can install on your ACM hub or managed clusters to enhance ODF Regional Disaster Recovery features. Note that IBM is not responsible for managing these operators. 

You are responsible for managing these operators, including but not limited to updating, monitoring, recovery, and re-installation.
{: important}

| Operator | Description | Additional information |
|---|---|---|
| OpenShift API for Data Protection (OADP) Operator | - Use to create backup and restore APIs for OpenShift clusters. \n - Install on **managed clusters**.  | [Introduction to OpenShift API for data protection](https://docs.redhat.com/en/documentation/openshift_container_platform/4.18/html/backup_and_restore/oadp-application-backup-and-restore#oadp-introduction){: external} |
| Submariner | - Provides direct networking between two or more Kubernetes clusters in your environment. \n - Install on **managed clusters**. | [Submariner](https://docs.redhat.com/en/documentation/red_hat_advanced_cluster_management_for_kubernetes/2.2/html/manage_cluster/submariner){: external} |
{: caption="Optional operators for ODF Regional Disaster Recovery" caption-side="bottom"}

  
## Testing your disaster recovery configuration
{: #odf-rdr-test}

Create a sample application to test your disaster recovery solution. For more information, see [Create sample application for testing disaster recovery application](https://docs.redhat.com/documentation/red_hat_openshift_data_foundation/4.16/html-single/configuring_openshift_data_foundation_disaster_recovery_for_openshift_workloads/index#create-sample-application-for-testing-mdrsolution_manage-rdr){: external}.

  
1. Deploy a subscription-based application from the ACM Console. The application's topology tab shows green when all application resources are deployed successfully.
  
1. On the application page, go to **Actions** > **Manage Data Policy**.

1. Assign the DR policy created earlier to this application.

1. Verify that the application pods are running on the primary cluster.

1. On the application page, go to **Actions** > **Failover application**. Select your secondary ODF cluster as the target cluster. Click **Initiate**.

1. Verify that the application pods are moved to the secondary cluster.

1. On the application page, go to **Actions** > **Relocate application**. Select your primary ODF cluster as the target cluster. Click **Initiate**.

1. Verify that the application pods are moved back to the primary cluster.
        
