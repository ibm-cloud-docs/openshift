---

copyright:
  years: 2025, 2025
lastupdated: "2025-01-30"


keywords: openshift, openshift data foundation, openshift container storage, disaster recovery

subcollection: openshift

---


{{site.data.keyword.attribute-definition-list}}




# OpenShift Data Foundation Regional Disaster Recovery on {{site.data.keyword.openshiftlong_notm}} clusters
{: #openshift_odf_rdr_roks}

[Virtual Private Cloud]{: tag-vpc}
[4.15 and later]{: tag-red}

Regional Disaster Recovery ensures business continuity during the unavailability of a geographical region. You can use Red Hat Advanced cluster management (ACM) to set up the Regional Disaster Recovery solutions for ODF clusters.
{: shortdesc}

The following steps for setting ODF Disaster Recovery are available as a Technical Preview only.
{: preview}


Here are the high-level steps of this solution:
1. Create the 3 VPC clusters (each in different regions/VPCs). All of them need to have the `--disable-outbound-traffic-protection` parameter.
1. Install ODF on 2 of them.
1. Install ACM on 1 of them.
1. Configure ACM to manage the 2 ODF clusters.

With this set up, the ACM cluster manages the ODF clusters. So if one ODF cluster goes down, then the ACM cluster rolls over the apps and data from that cluster to the other cluster.

## Creating the clusters
{: #odf-rdr-clusters}

Create 3 [VPC clusters](/docs/openshift?topic=openshift-clusters) in different regions. Make sure to include the `--disable-outbound-traffic-protection` parameter.
{: shortdesc}

1. Create managed cluster 1 in `us-east`, which will be the primary ODF cluster.
    ```sh
    ibmcloud ks cluster create vpc-gen2 --flavor bx2.16x64 --name managed-cluster-1-dr-odf
    --subnet-id 0767-5c97dd71-95e7-4f26-a31b-e2c7a8ad16f7 --vpc-id r014-8ac09b7e-99d0-460d-96bf-2dfe3eac1041
    --zone us-east-2 --pod-subnet 172.21.0.0/18 --service-subnet 172.22.0.0/16 --version 4.15.11_openshift --workers 3
    --cos-instance crn:v1:bluemix:public:cloud-object-storage:global:a/c468d8824937fecd8a0860fe0f379bf9:3887cefc-edcc-48df-a05e-ac3f02df10d5::
    --disable-outbound-traffic-protection
    ```
    {: pre}

1. Create managed cluster 2 in `jp-tok`, which will be the secondary ODF cluster. Ensure that managed cluster 2 does not have overlapping network with managed cluster 1.
    ```sh
    ibmcloud ks cluster create vpc-gen2 --flavor bx2.16x64 --name managed-cluster-2-dr-odf
    --subnet-id 02e7-4f2da612-6327-4968-88db-41d92c3e9c1b --vpc-id r022-fd23415e-fab0-42b1-b6da-567cc6f3df0c
    --zone jp-tok-1 --pod-subnet 172.23.0.0/18 --service-subnet 172.24.0.0/16 --version 4.15.11_openshift --workers 3
    --cos-instance crn:v1:bluemix:public:cloud-object-storage:global:a/c468d8824937fecd8a0860fe0f379bf9:3887cefc-edcc-48df-a05e-ac3f02df10d5::
    --disable-outbound-traffic-protection
    ```
    {: pre}

1. Create a hub cluster in `us-east` to install ACM on.
    ```sh
    ibmcloud ks cluster create vpc-gen2 --flavor bx2.8x32 --name acm-hub-cluster-dr-odf
    --subnet-id 0767-5c97dd71-95e7-4f26-a31b-e2c7a8ad16f7 --vpc-id r014-8ac09b7e-99d0-460d-96bf-2dfe3eac1041
    --zone us-east-2 --version 4.15.11_openshift --workers 3 --cos-instance crn:v1:bluemix:public
    :cloud-object-storage:global:a/c468d8824937fecd8a0860fe0f379bf9:3887cefc-edcc-48df-a05e-ac3f02df10d5::
    --disable-outbound-traffic-protection
    ```
    {: pre}

## Enabling the Red Hat OperatorHub catalog
{: #odf-rdr-enable-redhat}

By default, the Red Hat OperatorHub catalog is disabled. You need to enable it manually.
{: shortdesc}

1. Run the following command.
    ```sh
    kubectl edit operatorhub cluster -n openshift-marketplace
    ```
    {: pre}

1. Update `disableAllDefaultSources` value to `false`.

1. Verify that all marketplace pods are up.
    ```yaml
    spec:
    disableAllDefaultSources: false
    status:
      sources:
      - disabled: false
        name: redhat-operators
        status: Success
      - disabled: false
        name: certified-operators
        status: Success
      - disabled: false
        name: community-operators
        status: Success
      - disabled: false
        name: redhat-marketplace
        status: Success
    ```
    {: pre}   

## Setting up ACM on the hub cluster
{: #odf-rdr-install-acm}

Follow these steps to install ACM on the hub cluster and then set up the disaster recovery policy.
{: shortdesc}

1. Install ACM version 2.10 or later on the hub cluster from the [{{site.data.keyword.redhat_openshift_notm}} clusters console](https://cloud.ibm.com/kubernetes/clusters?platformType=openshift){: external}.
  
1. From **Operators** > **Installed Operators**, create a `MultiClusterHub` instance.
  
1. Open the ACM Console and import the 2 managed ODF clusters to the ACM hub.
      
      1. In the [{{site.data.keyword.redhat_openshift_notm}} clusters console](https://cloud.ibm.com/kubernetes/clusters?platformType=openshift){: external}, change the menu option on the top from **local-cluster** to **All Clusters** to switch to ACM console mode.
      1. Go to **Infrastructure** > **Console** > **Import Cluster**.
      1. Fill in the details for one of your managed ODF clusters and generate the command. 
      1. Click **Copy Command** to copy the import command and run it on the target cluster.
      1. Repeat these steps to import the other managed ODF cluster.

1. Configure the Submariner add-on from the ACM Console.

     1. Install Calico server onto both managed ODF clusters. For more information, see [Enable kubectl to manage Calico APIs](https://docs.tigera.io/calico/latest/operations/install-apiserver){: external}.
     2. Create a cluster set.
     3. Select to install Submariner add-ons for the cluster set.
     4. Select the managed ODF clusters as target clusters for add-on installation. 
     5. Keep the default settings when reviewing the configuration for both clusters and click **Install**.
     6. Wait for the Submariner add-on status to show healthy (green). This can take up to 20 minutes.

1. Install the OpenShift Data Foundation add-on version 4.15 or later on the primary and secondary managed clusters. Make sure you select the **Enable DR** option during the ODF installation. For more information, see [Installing the OpenShift Data Foundation add-on](/docs/openshift?topic=openshift-deploy-odf-vpc#install-odf-console-vpc).

1. Install ODF Multicluster Orchestrator to the ACM hub cluster. For more information, see [Installing ODF Multicluster Orchestrator on Hub cluster](https://docs.redhat.com/en/documentation/red_hat_openshift_data_foundation/4.16/html-single/configuring_openshift_data_foundation_disaster_recovery_for_openshift_workloads/index#installing-odf-multicluster-orchestrator_rdr){: external}.
  
1. Create a DR Policy for both managed ODF clusters with a sync interval of 5 minutes. For more information, see [Creating Disaster Recovery Policy on Hub cluster](https://docs.redhat.com/en/documentation/red_hat_openshift_data_foundation/4.16/html-single/configuring_openshift_data_foundation_disaster_recovery_for_openshift_workloads/index?extIdCarryOver=true&sc_cid=701f2000001OH7EAAW#creating-disaster-recovery-policy-on-hub-cluster_rdr){: external}. 
  
## Testing your disaster recovery configuration
{: #odf-rdr-test}

Create a sample application to test your disaster recovery solution. For more information, see [Create sample application for testing disaster recovery application](https://docs.redhat.com/en/documentation/red_hat_openshift_data_foundation/4.16/html-single/configuring_openshift_data_foundation_disaster_recovery_for_openshift_workloads/index#create-sample-application-for-testing-mdrsolution_manage-rdr){: external}.
{: shortdesc}
  
1. Deploy a subscription-based application from the ACM Console. The application's topology tab shows green when all application resources are deployed successfully.
  
1. On the application page, go to **Actions** > **Manage Data Policy**.

1. Assign the DR policy created earlier to this application.

1. Verify that the application pods are running on the primary cluster.

1. On the application page, go to **Actions** > **Failover application**. Select your secondary ODF cluster as the target cluster. Click **Initiate**.

1. Verify that the application pods are moved to the secondary cluster.

1. On the application page, go to **Actions** > **Relocate application**. Select your primary ODF cluster as the target cluster. Click **Initiate**.

1. Verify that the application pods are moved back to the primary cluster.
        
