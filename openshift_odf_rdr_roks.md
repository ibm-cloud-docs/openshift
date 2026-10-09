---

copyright:
  years: 2025, 2026
lastupdated: "2026-10-09"


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
1. Install the ACM add-on on the hub cluster.
1. Import the managed clusters into ACM.
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

1. [Create a VPC cluster](/docs/openshift?topic=openshift-cluster-create-vpc-gen2) in `us-east` to install ACM on. This is the hub cluster that you can use to manage your ODF clusters. Make sure your hub cluster has at least 3 worker nodes that run RHCOS, available compute capacity of at least 16 vCPU and 64 GB, outbound traffic disabled, and meets all of the [prerequisites for ACM](/docs/openshift?topic=openshift-acm&interface=ui#before). The following example command creates a cluster for ACM in `us-east`.

    ```sh
    ibmcloud ks cluster create vpc-gen2 --flavor bx2.16x64 --name acm-hub-cluster-dr-odf --subnet-id SUBNET_ID --vpc-id VPC_ID --zone us-east-2 --version 4.21.31_openshift --workers 3 --cos-instance COS_CRN --disable-outbound-traffic-protection --cni OVNKubernetes
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

1. Verify that the trusted profile secret was created in the cluster. This command can take up to 10 minutes to complete. Wait for the secret to appear before proceeding to install the ACM add-on. If you proceed before the secret is created, the ACM add-on installation will fail.
    ```sh
    oc get secrets -n kube-system | grep ibm-cloud-credentials
    ```
    {: pre}

1. If you are using ODF version 4.21 or later, install the OpenShift GitOps operator on the hub cluster.
    1. On the **Core platform** perspective of the hub cluster's OpenShift web console, navigate to **Ecosystem** > **Software Catalog** and search for **Red Hat OpenShift GitOps**.
    1. Click the **Red Hat OpenShift GitOps** tile.
    1. On the **Install Operator** page, select an **Update channel** and a **GitOps version** to install.
    1. Choose an **Installed Namespace**. The default installation namespace is `openshift-gitops-operator`.

        For GitOps version 1.10 and later, the default namespace changed from `openshift-operators` to `openshift-gitops-operator`.
        {: note}

    1. Select the **Enable Operator recommended cluster monitoring on this Namespace** checkbox to enable cluster monitoring.
    1. Click **Install**. Red Hat OpenShift GitOps is installed in all namespaces of the cluster.
    1. Verify that the Red Hat OpenShift GitOps Operator is listed in **Operators** > **Installed Operators** and that the **Status** shows **Succeeded**.

    After installation, OpenShift GitOps automatically sets up a ready-to-use Argo CD instance in the `openshift-gitops` namespace, and an Argo CD icon is displayed in the console toolbar.
    {: note}

## Step 3. Create the managed clusters
{: #managed-cluster-create}

[Managed cluster]{: tag-warm-gray}

1. [Create a VPC cluster](/docs/openshift?topic=openshift-cluster-create-vpc-gen2) in `us-east` with at least 3 worker nodes that run RHCOS, available compute capacity of at least 16 vCPU and 64 GB, and outbound traffic protection disabled. This will be the primary managed ODF cluster. The following example command creates a cluster in `us-east`.

    ```sh
    ibmcloud ks cluster create vpc-gen2 --flavor bx2.16x64 --name managed-cluster-1-dr-odf --subnet-id SUBNET_ID --vpc-id VPC_ID --zone us-east-2 --version 4.21.31_openshift --workers 3 --cos-instance COS_CRN --disable-outbound-traffic-protection --cni OVNKubernetes
    ```
    {: pre}

1. [Create a VPC cluster](/docs/openshift?topic=openshift-cluster-create-vpc-gen2) in `jp-tok` with at least 3 worker nodes that run RHCOS, available compute capacity of at least 16 vCPU and 64 GB, and outbound traffic protection disabled. This will be the secondary managed ODF cluster. For high availability, make sure that the secondary cluster's network does not overlap with the primary cluster's network. The following example command creates a cluster in `jp-tok`.

    ```sh
    ibmcloud ks cluster create vpc-gen2 --flavor bx2.16x64 --name managed-cluster-2-dr-odf --subnet-id SUBNET_ID --vpc-id VPC_ID --zone jp-tok --version 4.21.31_openshift --workers 3 --cos-instance COS_CRN --disable-outbound-traffic-protection --cni OVNKubernetes
    ```
    {: pre}

## Step 4. Install the ACM add-on on the hub cluster
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

1. Run the command to enable the add-on. Be sure to specify the `billingPlan` and `isLicenseAccepted` parameters.

    ```sh
    ibmcloud oc cluster addon enable acm --cluster HUB_CLUSTER_ID --param 'billingPlan=PLAN' --param 'isLicenseAccepted=BOOLEAN'
    ```
    {: pre}

    Command parameters. See the example command below for an example of each parameter type.

    `--cluster`
    :   Required. The ID of the hub cluster to install the ACM add-on to.

    `--param 'billingPlan='`
    :   Required. The billing plan you want to select for ACM. Specify `KUBERNETES` for the **ACM for Kubernetes** plan.

    `--param 'isLicenseAccepted='`
    :   Required. Set this to `true` to accept the license agreement for the selected billing plan. The add-on will not install successfully unless the license is accepted. By accepting this license, you agree to the applicable terms and conditions and acknowledge your understanding of the services included in the selected plan.

    Example command to install the ACM add-on with the **ACM for Kubernetes** billing plan.

    ```sh
    ibmcloud oc cluster addon enable acm --cluster a5bcde982dfer2nwxq73 --param 'billingPlan=KUBERNETES' --param 'isLicenseAccepted=true'
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
        oc describe acmhub
        ```
        {: pre}

        Example output.

        ```sh
        Status
            Message: ACM installed successfully
        ```
        {: screen}

## Step 5. Import the managed clusters into ACM
{: #hub-acm-import}

[Hub cluster]{: tag-blue} [Managed cluster]{: tag-warm-gray}

Import both managed clusters into ACM so that the hub cluster can manage them.

1. Open the OpenShift web console for the hub cluster.

2. From the **Fleet Management** perspective, click **Import cluster**.

3. Enter the **Name** of the first managed cluster, select a **Cluster set** if applicable, and enter **Additional labels** if applicable.

4. For **Import mode**, select **Run import commands manually** and click **Next**.

5. Optionally select an automation template and click **Next**.

6. Review the details and click **Generate command**. Copy the command that is displayed.

7. Log in to the first managed cluster and run the copied command with `kubectl` configured for that cluster.

8. Repeat steps 2–7 for the second managed cluster.

9. In the **Fleet Management** perspective, verify that both managed clusters are listed and show a **Ready** status before proceeding.

## Step 6. Configure the Submariner add-on
{: #submariner}

[Hub cluster]{: tag-blue} [Managed cluster]{: tag-warm-gray}

Configure the Submariner add-on to establish cross-cluster networking between your two managed clusters. Choose one of the following options based on your infrastructure and cluster types:

- **Option 1: Transit Gateway (Preferred)** — Supported for both {{site.data.keyword.openshiftlong_notm}} and Red Hat OpenShift Virtualization Service (ROVS) clusters with Virtual Server Instances (VSI) and Bare Metal worker nodes.
- **Option 2: Network Load Balancer (NLB)** — Supported for {{site.data.keyword.openshiftlong_notm}} clusters with VSI worker nodes only.

### Option 1: Use {{site.data.keyword.tg_full_notm}} to connect VPCs (Preferred)
{: #submariner-tg}

[Hub cluster]{: tag-blue}

Use {{site.data.keyword.tg_full_notm}} for high-performance direct cross-VPC communication. This option supports {{site.data.keyword.openshiftlong_notm}} and Red Hat OpenShift Virtualization Service clusters on both VSI and Bare Metal infrastructure.

1. Identify the VPCs used by your managed clusters:
   - For **{{site.data.keyword.openshiftlong_notm}}**: Go to the [{{site.data.keyword.cloud_notm}} console](https://cloud.ibm.com/){: external} > Navigation Menu > **Containers** > **Clusters** > select your cluster > note the **VPC**.
   - For **Red Hat OpenShift Virtualization Service**: Go to the [{{site.data.keyword.cloud_notm}} console](https://cloud.ibm.com/){: external} > Navigation Menu > **Infrastructure** > **OpenShift Virtualization** > select your cluster > note the **VPC**.

1. Create a Transit Gateway and add connections to both managed cluster VPCs:
   1. In the [{{site.data.keyword.cloud_notm}} console](https://cloud.ibm.com/){: external}, navigate to **Infrastructure** > **Network** > **Transit Gateway**.
   1. Click **Create**.
   1. Enter a **Transit Gateway name** and select your **Resource group**.
   1. Select the **Routing**:
      - **Local routing**: Choose this option if both managed clusters reside within the same region.
      - **Global routing**: Choose this option if your managed clusters are deployed across different regions.
   1. Under **Connections**, add connections for both VPCs:
      - **Connection 1**: Select **VPC** for network connection, choose the region for Cluster 1, and select the VPC for Cluster 1.
      - **Connection 2**: Select **VPC** for network connection, choose the region for Cluster 2, and select the VPC for Cluster 2.
   1. Click **Create**.

1. Create a ClusterSet resource on the hub cluster and add your managed clusters:
   1. In the ACM console on your hub cluster, navigate to **Fleet Management** > **Infrastructure** > **Clusters** > **ClusterSet**.
   1. Click **Create Cluster Set** and provide a name for the cluster set (for example, `<CLUSTERSET>`).
   1. Click **Manage Cluster Assignments** and add both managed clusters to the cluster set.

1. On the hub cluster, create the Submariner Broker configuration file `submariner-broker.yaml`.

   ```yaml
   apiVersion: submariner.io/v1alpha1
   kind: Broker
   metadata:
     name: submariner-broker
     namespace: <CLUSTERSET>-broker
     labels:
       cluster.open-cluster-management.io/backup: submariner
   spec:
     globalnetEnabled: true
   ```
   {: codeblock}

   Set `globalnetEnabled: true` if the managed clusters have overlapping networks (pod and service CIDRs). If your managed clusters do not have overlapping CIDRs, set `globalnetEnabled: false`.
   {: note}

1. Apply the Broker configuration to the hub cluster.

   ```sh
   oc apply -f submariner-broker.yaml
   ```
   {: pre}

1. On the hub cluster, create the `SubmarinerConfig` custom resource file `SubmarinerConfig-mc1.yaml` for managed cluster 1.

   ```yaml
   apiVersion: submarineraddon.open-cluster-management.io/v1alpha1
   kind: SubmarinerConfig
   metadata:
     name: submariner
     namespace: <MANAGED_CLUSTER1>
   spec:
     cableDriver: libreswan
     forceUDPEncaps: true
     gatewayConfig:
       gateways: 2
     NATTEnable: false
   ```
   {: codeblock}

1. On the hub cluster, create the `SubmarinerConfig` custom resource file `SubmarinerConfig-mc2.yaml` for managed cluster 2.

   ```yaml
   apiVersion: submarineraddon.open-cluster-management.io/v1alpha1
   kind: SubmarinerConfig
   metadata:
     name: submariner
     namespace: <MANAGED_CLUSTER2>
   spec:
     cableDriver: libreswan
     forceUDPEncaps: true
     gatewayConfig:
       gateways: 2
     NATTEnable: false
   ```
   {: codeblock}

1. Apply both `SubmarinerConfig` resources on the hub cluster.

   ```sh
   oc apply -f SubmarinerConfig-mc1.yaml
   oc apply -f SubmarinerConfig-mc2.yaml
   ```
   {: pre}

1. On the hub cluster, create the `ManagedClusterAddOn` custom resource file `ManagedClusterAddOn-mc1.yaml` for managed cluster 1.

   ```yaml
   apiVersion: addon.open-cluster-management.io/v1alpha1
   kind: ManagedClusterAddOn
   metadata:
     name: submariner
     namespace: <MANAGED_CLUSTER1>
   spec:
     installNamespace: submariner-operator
   ```
   {: codeblock}

1. On the hub cluster, create the `ManagedClusterAddOn` custom resource file `ManagedClusterAddOn-mc2.yaml` for managed cluster 2.

   ```yaml
   apiVersion: addon.open-cluster-management.io/v1alpha1
   kind: ManagedClusterAddOn
   metadata:
     name: submariner
     namespace: <MANAGED_CLUSTER2>
   spec:
     installNamespace: submariner-operator
   ```
   {: codeblock}

1. Apply both `ManagedClusterAddOn` resources on the hub cluster.

   ```sh
   oc apply -f ManagedClusterAddOn-mc1.yaml
   oc apply -f ManagedClusterAddOn-mc2.yaml
   ```
   {: pre}

1. Verify that the Submariner add-on status displays as healthy in the ACM console.
   1. Navigate to **Fleet Management** > **Infrastructure** > **Clusters** > **ClusterSet**.
   1. Select your cluster set and click **Submariner Add-on**.
   1. Confirm that **Connection Status** shows **Healthy** with a green checkmark.

1. (Optional) Run additional Submariner connectivity and diagnostic tests using the `subctl` CLI:

   1. Install the `subctl` CLI tool on your local system:
      ```sh
      curl -Ls https://get.submariner.io | bash
      export PATH=$PATH:~/.local/bin
      echo export PATH=\$PATH:~/.local/bin >> ~/.profile
      ```
      {: pre}

   1. Check gateway and route agent connections on managed cluster 1:
      ```sh
      subctl diagnose connections --kubeconfig ./<MANAGED_CLUSTER1_KUBECONFIG>.yaml
      ```
      {: pre}

   1. Check gateway and route agent connections on managed cluster 2:
      ```sh
      subctl diagnose connections --kubeconfig ./<MANAGED_CLUSTER2_KUBECONFIG>.yaml
      ```
      {: pre}

   1. Run the end-to-end connectivity test suite between the clusters:
      ```sh
      subctl verify --context <MANAGED_CLUSTER1_CONTEXT> --tocontext <MANAGED_CLUSTER2_CONTEXT> --only connectivity --verbose --image-override=submariner-nettest=quay.io/submariner/nettest:0.24.1
      ```
      {: pre}

### Option 2: Use Network Load Balancers to connect VPCs
{: #submariner-nlb}

[Hub cluster]{: tag-blue}

Follow these steps to install and configure the Submariner add-on through the ACM console using Network Load Balancers. This option is supported for {{site.data.keyword.openshiftlong_notm}} clusters with VSI worker nodes only. For more detailed information, see [Deploying Submariner by using the console](https://docs.redhat.com/en/documentation/red_hat_advanced_cluster_management_for_kubernetes/2.11/html/networking/networking#deploying-submariner-console){: external} in the Red Hat documentation.

1. Navigate to the ACM console on your hub cluster. Click **Fleet Management** > **Clusters** > **Cluster sets**.
1. Click **Create cluster set**. Follow the prompts to add your two managed clusters to the cluster set.
1. Click the option to install the Submariner add-on to the cluster set.
1. Select the managed clusters as target clusters for add-on installation.
1. When reviewing the configuration for both clusters, change the following settings as shown and leave the rest as default:
   - `globalnetEnabled: true` (checked)
   - `gateways: 2`
   - `NATTEnable: false` (unchecked)
   - `cableDriver: vxlan`
1. Click **Install**.
1. Wait for the Submariner add-on status to show healthy (green checkmark). This can take up to 20 minutes.


## Step 7. Install and configure OpenShift Data Foundation
{: #odf_install}

[Managed cluster]{: tag-warm-gray}

Install and configure ODF on your 2 managed clusters. Make sure to complete these steps on both the primary and secondary managed cluster.

Before running any `oc` commands in this section, make sure your context is set to the managed cluster you are configuring. Run `ibmcloud oc cluster config --cluster MANAGED_CLUSTER_NAME_OR_ID --admin` to switch contexts, then verify with `oc config current-context`.
{: important}

1. For each managed cluster, install the OpenShift Data Foundation add-on from the [{{site.data.keyword.cloud_notm}} console](https://cloud.ibm.com){: external}.
    1. Navigate to your cluster's **Overview** page and scroll down to the **Add-ons** section.
    1. Under **OpenShift Data Foundation**, click **Install**.
    1. Check the box for **Deploy NooBaa Multi-Cloud Object Gateway**.
    1. Click **Install** again to confirm.
    1. Wait for the ODF add-on status to change from **Enabling** to **Normal** (green checkmark) before proceeding.


1. Verify that ODF installed successfully. In the output, check that the status says `Ready`.

    The UI **Normal** status reflects that the add-on was deployed, but the ODF operator may still need a few minutes to finish initializing and registering its resources.
    {: note}

    ```sh
    oc get storagecluster -n openshift-storage ocs-storagecluster -o jsonpath='{.status.phase}{"\n"}'
    ```
    {: pre}

The following steps must be completed on each managed cluster. Switch your context to the first managed cluster using `ibmcloud oc cluster config --cluster MANAGED_CLUSTER_NAME_OR_ID --admin`, complete all steps through the end of this section, then switch to the second managed cluster and repeat.
{: important}

1. Run the command to update the `ACM Managed Cluster Name` in the `storageCluster` resource's `multiClusterService` section. This allows ODF to use GlobalNet. For more information, see [Creating an OpenShift Data Foundation cluster on managed clusters](https://docs.redhat.com/documentation/red_hat_openshift_data_foundation/4.21/html/configuring_openshift_data_foundation_disaster_recovery_for_openshift_workloads/rdr-solution#creating-odf-cluster-on-managed-clusters_rdr){: external}.

    Replace `MANAGED_CLUSTER_NAME` with the name of the cluster your context is currently pointed at.
    {: note}

    ```sh
    kubectl patch storagecluster -n openshift-storage ocs-storagecluster --type merge -p'{"spec":{"network":{"multiClusterService":{"clusterID":"MANAGED_CLUSTER_NAME","enabled":true}}}}'
    ```
    {: pre}

    Example output.

    ```sh
    storagecluster.ocs.openshift.io/ocs-storagecluster patched
    ```
    {: screen}

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

1. Verify that the service exports are healthy. Each service export must report `Valid=True` and `Ready=True`.

    ```sh
    oc get serviceexport -n openshift-storage -o jsonpath='{range .items[*]}{.metadata.name}{"\t"}{range .status.conditions[*]}{.type}{"="}{.status}{" "}{end}{"\n"}{end}'
    ```
    {: pre}

    Example output:
    ```sh
    rook-ceph-mon-d Valid=True Ready=True
    rook-ceph-mon-e Valid=True Ready=True
    rook-ceph-mon-f Valid=True Ready=True
    rook-ceph-osd-0 Valid=True Ready=True
    rook-ceph-osd-1 Valid=True Ready=True
    rook-ceph-osd-2 Valid=True Ready=True
    ```
    {: screen}

1. If a service export doesn't reach the `Valid` and `Ready` state, describe the resource and check the error message. Replace `SERVICE_EXPORT_NAME` with the name of the service export that isn't healthy.

    ```sh
    oc describe serviceexport SERVICE_EXPORT_NAME -n openshift-storage
    ```
    {: pre}

    A known issue in Submariner 0.24.1 causes the following error message because the Submariner Lighthouse component restricts exporting services from `openshift-*` namespaces.

    ```text
    Service in namespace "openshift-storage" cannot be exported due to namespace restriction
    ```
    {: screen}

    If you see this error, create the `submariner-lighthouse-agent` config map in the `submariner-operator` namespace of the managed cluster. This config map removes the namespace restriction.

    ```sh
    oc create configmap submariner-lighthouse-agent \
      --from-literal=import-namespace-deny-list="kube-" \
      -n submariner-operator
    ```
    {: pre}

    After you create the config map, run the command from the previous step again to confirm that the service exports reach the `Valid=True Ready=True` state.

1. Create a service export for `ocs-provider-server`.

    ```sh
    oc apply -f - <<EOF
    apiVersion: multicluster.x-k8s.io/v1alpha1
    kind: ServiceExport
    metadata:
      name: ocs-provider-server
      namespace: openshift-storage
    EOF
    ```
    {: pre}

    Example output.

    ```sh
    serviceexport.multicluster.x-k8s.io/ocs-provider-server created
    ```
    {: screen}

1. Run the command to update the `storageCluster` resource to use the `ocs-provider-server` service export you created.

    ```sh
    oc annotate storagecluster ocs-storagecluster -n openshift-storage ocs.openshift.io/api-server-exported-address=MANAGED_CLUSTER_NAME.ocs-provider-server.openshift-storage.svc.clusterset.local:50051.
    ```
    {: pre}

    Example output.

    ```sh
    storagecluster.ocs.openshift.io/ocs-storagecluster annotated
    ```
    {: screen}

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

Install the ODF Multicluster Orchestrator on your hub cluster and create the disaster recovery (DR) policy that enables mirroring between your two managed clusters.

1. Install the ODF Multicluster Orchestrator on the hub cluster.
    1. Install the OpenShift GitOps operator on the hub cluster if you haven't already. For installation steps, see the end of [Step 2. Create a trusted profile for the hub cluster](#hub-cluster-trusted-profile).
    1. On the **Core platform** perspective of the hub cluster's OpenShift web console, navigate to **Ecosystem** > **Software Catalog** and search for **ODF Multicluster Orchestrator**.
    1. Click the **ODF Multicluster Orchestrator** tile. Make sure to select the **same version number** as the ODF version you installed onto the managed clusters in the previous section. Keep all other default settings and click **Install**.
    1. Ensure that the operator resources are installed in the `openshift-operators` project and available to all namespaces. Click **Install** again to confirm.

    The ODF Multicluster Orchestrator also installs the OpenShift DR Hub Operator on the hub cluster as a dependency.
    {: note}

1. Verify the installation by checking that the operator pods are running. Make sure your CLI context is set to the hub cluster before running this command.

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

1. On the hub cluster, create a DR policy with a 5 minute sync interval and specify each managed cluster in the parameters. This creates NooBaa object buckets on both managed clusters and enables ODF Ceph block pool mirroring for volume replication.
    1. On the **Fleet Management** perspective of the hub cluster's OpenShift web console, navigate to **Data Services** > **Disaster recovery** > **Policies** > **Create DRPolicy**.
    2. Create a DR policy that includes the following parameters.
        - Connected clusters: PRIMARY_MANAGED_CLUSTER_NAME, SECONDARY_MANAGED_CLUSTER_NAME
        - Replication policy: Asynchronous
        - Replication interval: 5m
        - If applicable, select **Enable disaster recovery support for restored and cloned PersistentVolumeClaims (For Data Foundation only)** under **Advanced settings**.

        Red Hat explicitly states that this option should only be used with discovered applications and environments where cloned/restored RBD volumes are actively supported.
        {: note}

1. On the **hub cluster**, run the following commands to verify that the DR policy was created and applied to the managed clusters. Make sure your CLI context is set to the hub cluster before running these commands.

    ```sh
    ibmcloud oc cluster config --cluster HUB_CLUSTER_NAME --admin
    ```
    {: pre}

    ```sh
    oc get drpolicy DRPOLICY_NAME -o jsonpath='{.status.conditions[].reason}{"\n"}'
    ```
    {: pre}

    Example output.

    ```sh
    Succeeded
    ```
    {: screen}

    ```sh
    oc get drclusters
    ```
    {: pre}

    Example output.

    ```sh
    NAME               AGE
    managed-cluster1   4m42s
    managed-cluster2   4m42s
    ```
    {: screen}

1. On **each managed cluster**, verify that the DR policy was applied and is in a healthy state. Switch your CLI context to each managed cluster before running these commands.

    ```sh
    ibmcloud oc cluster config --cluster MANAGED_CLUSTER_NAME --admin
    ```
    {: pre}

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
