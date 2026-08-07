---

copyright:
  years: 2025, 2026
lastupdated: "2026-08-07"


keywords: openshift, openshift data foundation, openshift container storage, disaster recovery

subcollection: openshift

---


{{site.data.keyword.attribute-definition-list}}


# OpenShift Data Foundation Regional Disaster Recovery on {{site.data.keyword.openshiftlong_notm}} clusters
{: #openshift_odf_rdr_roks}

[Virtual Private Cloud]{: tag-vpc}
[4.17 and later]{: tag-red}

Regional Disaster Recovery ensures business continuity during the unavailability of a geographical region. You can use Red Hat Advanced Cluster Management (ACM) to set up the Regional Disaster Recovery solutions for OpenShift Data Foundation (ODF) clusters.
{: shortdesc}

Each step is labeled to indicate which cluster to run it on. Use the following legend as a reference.

| Tag | Cluster |
| --- | --- |
| [Hub cluster]{: tag-blue} | Steps to complete on the **hub cluster** (the cluster where ACM is installed). |
| [Managed cluster]{: tag-warm-gray} | Steps to complete on each **managed cluster** (the primary and secondary ODF clusters). |
{: caption="Cluster tag legend" caption-side="bottom"}

Here are the high-level steps of this solution:
1. Create the hub cluster.
1. Create a trusted profile for the hub cluster.
1. Create the managed clusters.
1. Prepare secrets for ACM on the hub cluster.
1. Install the ACM add-on on the hub cluster.
1. Install Submariner on the managed clusters to establish connectivity between them.
1. Install ODF on the managed clusters.
1. Configure the Regional Disaster Recovery policy.

With this set up, the hub cluster that you installed ACM on manages the ODF clusters. If your primary ODF cluster becomes unavailable, the hub cluster rolls over the apps and data from the primary ODF cluster to the secondary ODF cluster.

ODF Regional Disaster Recovery supports subscription-based, ApplicationSet-based, discovered, and VM-based applications. For full details, see [Supported applications and workloads](#app_support_detail) at the bottom of this page.
{: #app_support}

## Before you begin
{: #prereq}

Before you create the clusters, gather the VPC and Cloud Object Storage details you need to populate in the cluster creation commands.

1. Retrieve your VPC IDs. Note the ID of the VPC you want to use for each cluster.

    ```sh
    ibmcloud is vpcs
    ```
    {: pre}

1. Retrieve the subnet details for a specific VPC. Note the subnet IDs you want to use for each cluster.

    ```sh
    ibmcloud is subnets --vpc VPC_ID
    ```
    {: pre}

1. List your Cloud Object Storage instances.

    ```sh
    ibmcloud resource service-instances --service-name cloud-object-storage
    ```
    {: pre}

1. Retrieve the CRN of the instance you want to use. Note the value in the `ID` field.
    ```sh
    ibmcloud resource service-instance SERVICE_INSTANCE
    ```
    {: pre}

## Step 1. Create the hub cluster
{: #hub-cluster-create}

[Hub cluster]{: tag-blue}

This is the cluster you install ACM on to manage the primary and secondary ODF clusters. Make sure your hub cluster has at least `16 vCPU x 64 GB` compute capacity available.
{: shortdesc}

For each cluster, make sure to allow outbound traffic by including the `--disable-outbound-traffic-protection` parameter in the CLI or selecting the option to disable outbound traffic protection in the UI.
{: important}

1. [Create a VPC cluster](/docs/openshift?topic=openshift-cluster-create-vpc-gen2) in `us-east` to install ACM on. This is the hub cluster that you can use to manage your ODF clusters. Make sure your hub cluster has at least 3 worker nodes that run RHCOS, available compute capacity of at least 16 vCPU and 64 GB, outbound traffic disabled, and meets all of the [prequisites for ACM](/docs/openshift?topic=openshift-acm&interface=ui#before). The following example command creates a cluster for ACM in `us-east`.

    ```sh
    ibmcloud ks cluster create vpc-gen2 --flavor bx2.16x64 --name acm-hub-cluster-dr-odf --subnet-id SUBNET_ID --vpc-id VPC_ID --zone us-east-2 --version 4.21.27_openshift --workers 3 --cos-instance COS_CRN --disable-outbound-traffic-protection --cni OVNKubernetes
    ```
    {: pre}

1. Note the cluster ID from the output. You need it in a later step.

## Step 2. Create a trusted profile for the hub cluster
{: #hub-cluster-trusted-profile}

[Hub cluster]{: tag-blue}

1. Create the trusted profile.
    ```sh
    ibmcloud iam trusted-profile-create acm-operator-profile
    ```
    {: pre}

1. Create the compute resource trust rule, scoped to the `kube-system` namespace on Red Hat OpenShift compute resources.
    ```sh
    ibmcloud iam trusted-profile-rule-create acm-operator-profile \
      --name kube-system-rule \
      --type Profile-CR \
      --conditions claim:namespace,operator:EQUALS,value:kube-system \
      --cr-type ROKS_SA
    ```
    {: pre}

1. Assign the IAM access policy to the profile. Replace `CLUSTER_ID` with your hub cluster ID.
    ```sh
    ibmcloud iam trusted-profile-policy-create acm-operator-profile \
      --roles Reader,Viewer,Operator,Editor \
      --service-name containers-kubernetes \
      --service-instance CLUSTER_ID
    ```
    {: pre}

1. Assign the trusted profile to the hub cluster. After you assign a trusted profile to a cluster, it cannot be removed.
    ```sh
    ibmcloud oc experimental trusted-profile set --cluster CLUSTER_NAME_OR_ID --trusted-profile TRUSTED_PROFILE_ID
    ```
    {: pre}

1. If you are using ODF version 4.21 or later, install the OpenShift GitOps operator on the hub cluster. For installation steps, see [Installing Red Hat OpenShift GitOps Operator in web console](https://docs.redhat.com/en/documentation/red_hat_openshift_gitops/1.20/html-single/installing_gitops/index#installing-gitops-operator-in-web-console_installing-openshift-gitops){: external}.

## Step 3. Create the managed clusters
{: #managed-cluster-create}

[Managed cluster]{: tag-warm-gray}

1. [Create a VPC cluster](/docs/openshift?topic=openshift-cluster-create-vpc-gen2) in `us-east` with at least 3 worker nodes that run RHCOS, available compute capacity of at least 16 vCPU and 64 GB, and outbound traffic protection disabled. This will be the primary managed ODF cluster. The following example command creates a cluster in `us-east`.

    ```sh
    ibmcloud ks cluster create vpc-gen2 --flavor bx2.16x64 --name managed-cluster-1-dr-odf --subnet-id SUBNET_ID --vpc-id VPC_ID --zone us-east-2 --version 4.21.27_openshift --workers 3 --cos-instance COS_CRN --disable-outbound-traffic-protection --cni OVNKubernetes
    ```
    {: pre}

1. [Create a VPC cluster](/docs/openshift?topic=openshift-cluster-create-vpc-gen2) in `jp-tok` with at least 3 worker nodes that run RHCOS, available compute capacity of at least 16 vCPU and 64 GB, and outbound traffic protection disabled. This will be the secondary managed ODF cluster. For high availability, make sure that the secondary cluster's network does not overlap with the primary cluster's network. The following example command creates a cluster in `jp-tok`.

    ```sh
    ibmcloud ks cluster create vpc-gen2 --flavor bx2.16x64 --name managed-cluster-2-dr-odf --subnet-id SUBNET_ID --vpc-id VPC_ID --zone jp-tok --version 4.21.27_openshift --workers 3 --cos-instance COS_CRN --disable-outbound-traffic-protection --cni OVNKubernetes
    ```
    {: pre}

## Step 4. Prepare secrets for ACM
{: #prep-secret-rdr}

[Hub cluster]{: tag-blue}

For each cluster that you want to manage with ACM, you must create a secret on the hub cluster that includes the managed cluster's access token and server URL.

If you want to import managed clusters during the ACM add-on installation process, complete these steps before you begin the installation. If you choose to create the secrets and import managed clusters after the add-on is installed on the hub cluster, you can do so by completing [additional steps](/docs/openshift?topic=openshift-acm#after) with the CLI.
{: important}

Complete the following steps for each cluster that you want to manage.

1. On the cluster that you want to manage with ACM, run the command to find the server URL. In the output, find and note the **Master URL** value. This is the server URL to reference in the secret. You also use this URL in the following steps.

    ```sh
    ibmcloud oc cluster get -c CLUSTER_NAME_OR_ID
    ```
    {: pre}

    Example output.

    ```sh
    NAME:                           mycluster
    ID:                             1234567
    State:                          normal
    Created:                        2025-01-22T19:22:16+0000
    Location:                       dal10
    Master URL:                     https://c100-e.<region>.containers.cloud.ibm.com:<port>
    ...
    ```
    {: screen}

1. Retrieve the base URL of the Red Hat OpenShift oauth server. Replace `MASTER_URL` with the URL found in the previous step. The command extracts the base URL without the `/oauth/token` suffix.

    ```sh
    curl -sS MASTER_URL/.well-known/oauth-authorization-server | jq -r .token_endpoint | sed 's#/oauth/token##'
    ```
    {: pre}

    Example output.

    ```sh
    https://c111-e.us-east.containers.cloud.ibm.com:31282
    ```
    {: screen}

1. Retrieve an access token using the endpoint retrieved in the previous step. Execute the following cURL command, replacing `URL` with the output from the previous step and `API_KEY` with your [IBM Cloud API key](https://cloud.ibm.com/iam/apikeys){: external}. In the output, find the `ACCESS_TOKEN` contained in the **Location response**. This is the access token to include in the secret.

    Example curl request:

    ```sh
    curl -u 'apikey:API_KEY' -H "X-CSRF-Token: a" 'URL/oauth/authorize?client_id=openshift-challenging-client&response_type=token' -vvv
    ```
    {: pre}

    Example output. The ACCESS_TOKEN is included in the Location response string.

    ```sh
    < HTTP/1.1 302 Found
    < Cache-Control: no-cache, no-store, max-age=0, must-revalidate
    < Cache-Control: no-cache, no-store, max-age=0, must-revalidate
    < Expires: 0
    < Expires: Fri, 01 Jan 2030 00:00:00 GMT
    < Location: TOKEN_ENDPOINT/oauth/token/implicit#access_token=ACCESS_TOKEN&expires_in=86400&scope=user%3Afull&token_type=Bearer
    ...
    ```
    {: screen}

1. On the hub cluster, create a secret that contains the cluster access token and server URL. For information on creating secrets, see [Working with secrets](https://kubernetes.io/docs/concepts/configuration/secret/){: external} in the Kubernetes documentation.

    Example secret.

    ```yaml
    apiVersion: v1
    kind: Secret
    metadata:
      name: SECRET_NAME
      namespace: SECRET_NAMESPACE  # The namespace that the secret is to be created in
    type: Opaque
    stringData:
      token: ACCESS_TOKEN
      server: SERVER_URL
    ```
    {: pre}

## Step 5. Install the ACM add-on on the hub cluster
{: #hub-acm-install}

[Hub cluster]{: tag-blue}

Use the CLI to install the ACM add-on on the hub cluster.

1. Find the default version of the ACM add-on.

    ```sh
    ibmcloud oc cluster addon versions
    ```
    {: pre}

1. Review the ACM add-on options. In the command, specify the default version found in the previous step. Note any options you want to include when you install the add-on.

    ```sh
    ibmcloud oc cluster addon options --addon acm --version DEFAULT_VERSION
    ```
    {: pre}

1. If you want to import clusters to be managed by the add-on, follow the steps in [Preparing secrets for ACM](#prep-secret-rdr) if you have not already done so. Be sure to save the cluster ID and the name and namespace of the secret you create on the hub cluster. You can also complete this process after the add-on is installed on the hub cluster, however additional steps are required to [import managed clusters after installation](/docs/openshift?topic=openshift-acm#after).

1. Run the command to enable the add-on. Be sure to specify the `billingPlan` and `isLicenseAccepted` parameters, as well as the optional `--managedClusters` parameter if you want to import clusters during the installation process.

    ```sh
    ibmcloud oc cluster addon enable acm --cluster HUB_CLUSTER_ID --param 'managedClusters=["clusterid:CLUSTER_ID;secretname:SECRET_NAME;secretnamespace:SECRET_NAMESPACE;action:IMPORT"]' --param 'billingPlan=PLAN' --param 'isLicenseAccepted=BOOLEAN'
    ```
    {: pre}

    Command parameters. See the example command below for an example of each parameter type.

    `--cluster`
    :   Required. The ID of the hub cluster to install the ACM add-on to.

    `--param 'managedClusters=["]`
    :   Optional. Include this parameter one or more times to import managed clusters during the add-on installation process. You can also complete this step later. For more information, see [Preparing secrets for ACM](#prep-secret-rdr).
    :   Specify the following values:
    :   - **clusterid**: The ID of the managed cluster to import.
    :   - **secretname**: The name of the secret you created on the hub cluster. This secret contains the credentials for the managed cluster.
    :   - **secretnamespace**: The namespace of the secret you created on the hub cluster. This secret contains the credentials for the managed cluster.
    :   - **action:IMPORT**: The parameter that specifies the IMPORT action for the managed cluster.

    `--param 'billingPlan='`
    :   Required. The billing plan you want to select for ACM. Specify `KUBERNETES` for the **ACM for Kubernetes** plan.

    `--param 'isLicenseAccepted='`
    :   Required. Specify `TRUE` to accept the license agreement for the selected billing plan. By accepting this license, you agree to the applicable terms and conditions and acknowledge your understanding of the services included in the selected plan.

    Example command to install the ACM add-on with the **ACM for Kubernetes** billing plan and import a managed cluster.

    ```sh
    ibmcloud ks cluster addon enable acm --cluster a5bcde982dfer2nwxq73 --param 'managedClusters=["clusterid:w7rthce34gfbq7ww12d3;secretname:managed-secret-1;secretnamespace:managed-ns1;action:Import"]' --param 'billingPlan=KUBERNETES' --param 'isLicenseAccepted=true'
    ```
    {: pre}

1. Verify that the add-on installed. It might take several minutes for the add-on to show in the following outputs.

    1. On the hub cluster, check that the `acmhub` resource is created.
        ```sh
        oc get acmhub
        ```
        {: pre}

        Example output.

        ```sh
            NAME       AGE
            acm-auto   1h
        ```
        {: screen}

    1. On the hub cluster, check the `acmhub` status.

        ```sh
        oc describe acmhubstatus
        ```
        {: pre}

        Example output.

        ```sh
        status
            phase: Ready
        ```
        {: screen}

## Step 6. Configure the Submariner add-on
{: #submariner}

[Managed cluster]{: tag-warm-gray}

Follow the steps to install and configure the Submariner add-on, which establishes connectivity across your two managed clusters. These steps use the ACM console. For more detailed information, see [Deploying Submariner by using the console](https://docs.redhat.com/en/documentation/red_hat_advanced_cluster_management_for_kubernetes/2.11/html/networking/networking#deploying-submariner-console){: external} in the Red Hat documentation.

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


## Step 7. Install and configure OpenShift Data Foundation
{: #odf_install}

[Managed cluster]{: tag-warm-gray}

Install and configure ODF on your 2 managed clusters. Make sure to complete these steps on both the primary and secondary managed cluster.

1. Follow the steps to [install the OpenShift Data Foundation add-on](/docs/openshift?topic=openshift-deploy-odf-vpc&interface=cli#install-odf-cli-vpc) onto your 2 managed clusters. Specify the default ODF version or later. Make sure you include the option to enable NooBaa as an add-on option during the installation.

1. Verify that the ODF foundation installed successfully. In the output, check that the status says `Ready`.
    ```sh
    oc get storagecluster -n openshift-storage ocs-storagecluster -o jsonpath='{.status.phase}{"\n"}'
    ```
    {: pre}

1. Run the command to update the `ACM Managed Cluster Name` in the `storageCluster` resource’s `multiClusterService` section. This allows ODF to use GlobalNet. For more information, see [Creating an OpenShift Data Foundation cluster on managed clusters](https://docs.redhat.com/documentation/red_hat_openshift_data_foundation/4.21/html/configuring_openshift_data_foundation_disaster_recovery_for_openshift_workloads/rdr-solution#creating-odf-cluster-on-managed-clusters_rdr){: external}.

    Make sure to replace `MANAGED_CLUSTER_NAME` in the command with the name of your managed cluster.
    {: important}

    ```sh
    kubectl patch storagecluster -n openshift-storage ocs-storagecluster --type merge -p'{"spec":{"network":{"multiClusterService":{"clusterID":"MANAGED_CLUSTER_NAME","enabled":true}}}}'
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
    {: codeblock}

1. Run the command to update the `storageCluster` resource to use the `ocs-provider-server` service export you created.

    ```sh
    oc annotate storagecluster ocs-storagecluster -n openshift-storage ocs.openshift.io/api-server-exported-address=MANAGED_CLUSTER_NAME.ocs-provider-server.openshift-storage.svc.clusterset.local:50051.
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


## Step 8. Configure the Regional Disaster Recovery policy
{: #rdr-configure}

[Hub cluster]{: tag-blue}

Install the ODF Multicluster Orchestrator on your hub cluster and create the DR policy that enables mirroring between your two managed clusters.

1. Follow the steps to [install the ODF Multicluster Orchestrator](https://docs.redhat.com/en/documentation/red_hat_openshift_data_foundation/4.21/html-single/configuring_openshift_data_foundation_disaster_recovery_for_openshift_workloads/index#installing-odf-multicluster-orchestrator_mdr){: external} onto the **ACM hub cluster**. To ensure compatibility, make sure you install the **same version number** as the ODF version you installed onto the managed clusters in the previous section.
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
    {: screen}

1. On the **ACM hub cluster**, create a DR policy with a 5 minute sync interval and specify each managed cluster in the parameters. This creates NooBaa object buckets on both managed clusters and enables ODF Ceph block pool mirroring for volume replication.
    1. Navigate to the ACM console, then click **Fleet management** > **Data services** > **Disaster Recovery** > **Policies** > **Create DR Policy**.
    2. Create a DR policy that includes the following parameters.
        - Connected clusters: PRIMARY_MANAGED_CLUSTER_NAME, SECONDARY_MANAGED_CLUSTER_NAME
        - Replication policy: Asynchronous
        - Replication interval: 5m

1. On the hub cluster, run the commands to verify that the DR policy was created and applied to the managed clusters.

    ```sh
    oc get drpolicy DRPOLICY_NAME -o jsonpath='{.status.conditions[].reason}{"\n"}'
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

1. **Optional**: Review the [operators](#odf-rdr-operators) you can install to enhance ODF Regional Disaster Recovery features.

1. **Optional**: [Test your disaster recovery configuration](#odf-rdr-test).

## Optional operators for ODF Regional Disaster Recovery
{: #odf-rdr-operators}

Review the optional operators you can install on your ACM hub or managed clusters to enhance ODF Regional Disaster Recovery features. Note that IBM is not responsible for managing these operators.

You are responsible for managing these operators, including but not limited to updating, monitoring, recovery, and re-installation.
{: important}

| Operator | Description | Additional information |
| --- | --- | --- |
| OpenShift API for Data Protection (OADP) Operator | - Use to create backup and restore APIs for OpenShift clusters. \n - Install on **managed clusters**. | [Introduction to OpenShift API for data protection](https://docs.redhat.com/en/documentation/openshift_container_platform/4.21/html/backup_and_restore/oadp-application-backup-and-restore#oadp-introduction){: external} |
{: caption="Optional operators for ODF Regional Disaster Recovery" caption-side="bottom"}


## Testing your disaster recovery configuration
{: #odf-rdr-test}

Create a sample application to test your disaster recovery solution. For more information, see [Create sample application for testing disaster recovery application](https://docs.redhat.com/documentation/red_hat_openshift_data_foundation/4.21/html-single/configuring_openshift_data_foundation_disaster_recovery_for_openshift_workloads/index#create-sample-application-for-testing-mdrsolution_manage-rdr){: external}.


1. Deploy a subscription-based application from the ACM Console. The application's topology tab shows green when all application resources are deployed successfully.

1. On the application page, go to **Actions** > **Manage Data Policy**.

1. Assign the DR policy created earlier to this application.

1. Verify that the application pods are running on the primary cluster.

1. On the application page, go to **Actions** > **Failover application**. Select your secondary ODF cluster as the target cluster. Click **Initiate**.

1. Verify that the application pods are moved to the secondary cluster.

1. On the application page, go to **Actions** > **Relocate application**. Select your primary ODF cluster as the target cluster. Click **Initiate**.

1. Verify that the application pods are moved back to the primary cluster.

## Upgrading your ODF Regional Disaster Recovery environment
{: #odf-rdr-upgrade}

For information about when and how to upgrade the components of your ODF-RDR environment, see [Upgrading your ODF Regional Disaster Recovery environment](/docs/openshift?topic=openshift-openshift_odf_rdr_upgrade).

## Troubleshooting
{: #odf-rdr-troubleshoot}

If you encounter issues with your ODF Regional Disaster Recovery configuration, see [Verifying your OpenShift Data Foundation Regional Disaster Recovery configuration](/docs/openshift?topic=openshift-openshift_odf_rdr_verify) to check the health of each component in your setup.

## Supported applications and workloads
{: #app_support_detail}

Review the types of applications and workloads that you can apply Regional Disaster Recovery for after you complete the setup.

Subscription-based
:   An application is deployed from an external source, such as GitHub, a Helm repo, or Object Storage.
:   For more information, see [Creating a sample Subscription-based application](https://docs.redhat.com/en/documentation/red_hat_openshift_data_foundation/4.21/html-single/configuring_openshift_data_foundation_disaster_recovery_for_openshift_workloads/index#subscription-based-apps_manage-mdr){: external} in the Red Hat documentation.

ApplicationSet-based
:   An application is deployed from a GitHub repo using the GitOps operator, which manages continuous delivery. This includes two subtypes:
:   - **GitOps Pull Model (ArgoCD pull)**: A managed cluster pulls the application from GitHub using the GitOps operator.
:   - **GitOps Push Model (ArgoCD push)**: The GitOps operator pushes the application to the managed cluster during deployments and updates.
:   For more information, see [Creating Application-set based applications](https://docs.redhat.com/en/documentation/red_hat_openshift_data_foundation/4.21/html-single/configuring_openshift_data_foundation_disaster_recovery_for_openshift_workloads/index#creating-applicationset-application_manage-mdr){: external} in the Red Hat documentation.
:   For more information on the GitOps subtypes, see [Deploying Argo CD with Push and Pull model](https://docs.redhat.com/en/documentation/red_hat_advanced_cluster_management_for_kubernetes/2.15/html/gitops/gitops-overview#gitops-push-pull){: external} in the Red Hat documentation.

Discovered applications
:   An application was pre-deployed in a managed cluster without using ACM. In this case, you can use ACM discovery for the pre-installed app and still configure the DR policy.
:   For more information, see [Disaster recovery protection for discovered applications](https://docs.redhat.com/en/documentation/red_hat_openshift_data_foundation/4.21/html-single/configuring_openshift_data_foundation_disaster_recovery_for_openshift_workloads/index#protect-discovered-apps-regionaldr_manage-rdr){: external} in the Red Hat documentation.

Applications that include VM deployments
:   A VM-based application is deployed onto the managed cluster from the ACM console. These VM applications can be subscription based, ApplicationSet-based, or discovered, as described previously. Options to start, stop, pause, and delete VM operations are available from the ACM console for these types of applications.
:   For more information, see [Red Hat Advanced Cluster Management for Virtualization](https://www.redhat.com/en/resources/advanced-cluster-management-for-virtualization-datasheet){: external} in the Red Hat documentation.
