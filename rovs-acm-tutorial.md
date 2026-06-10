---

copyright:
  years: 2026, 2026
lastupdated: "2026-06-10"

keywords: openshift, virtualization service, rovs, acm, advanced cluster management, tutorial, virtual machines

subcollection: openshift
content-type: tutorial
services: openshift
account-plan: paid
completion-time: 60m

---

{{site.data.keyword.attribute-definition-list}}

# Tutorial: Managing Virtualization Service clusters with Advanced Cluster Management
{: #rovs-acm-tutorial}
{: toc-content-type="tutorial"}
{: toc-services="openshift"}
{: toc-completion-time="60m"}

[Virtual Private Cloud]{: tag-vpc}
[4.21 and later]{: tag-red}
[Bare metal worker nodes only]{: tag-warm-gray}

Learn how to deploy and manage OpenShift Virtualization Service clusters using Red Hat Advanced Cluster Management (ACM) for centralized multi-cluster management and governance.
{: shortdesc}

This service is currently available as a beta release. Access is controlled by an allowlist. During the beta period, only console-based cluster creation is supported.
{: beta}

## Objectives
{: #rovs-acm-objectives}

In this tutorial, you will:

- Set up an ACM hub cluster for managing Virtualization Service clusters
- Deploy a Virtualization Service cluster as a managed cluster through ACM
- Configure policies and governance for virtual machine workloads
- Monitor and manage virtual machines across multiple clusters
- Implement disaster recovery strategies for VM workloads

## Before you begin
{: #rovs-acm-prereqs}

### Required permissions
{: #rovs-acm-permissions}

- **Administrator** role for {{site.data.keyword.containerlong_notm}}
- **Editor** or **Administrator** role for VPC Infrastructure Services
- Access to create and manage multiple OpenShift clusters

### Required tools
{: #rovs-acm-tools}

- [{{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-install-ibmcloud-cli)
- [{{site.data.keyword.containerlong_notm}} CLI plugin](/docs/openshift?topic=openshift-cli-install)
- [OpenShift CLI (`oc`)](/docs/openshift?topic=openshift-cli-install)
- [Helm CLI](https://helm.sh/docs/intro/install/){: external} (version 3.0 or later)

### Prerequisites
{: #rovs-acm-requirements}

- An existing OpenShift cluster (4.16 or later) to serve as the ACM hub cluster
- VPC infrastructure prepared for Virtualization Service clusters
- Familiarity with OpenShift and Kubernetes concepts
- Understanding of [Advanced Cluster Management concepts](https://access.redhat.com/documentation/en-us/red_hat_advanced_cluster_management_for_kubernetes){: external}

## Set up the ACM hub cluster
{: #rovs-acm-hub-setup}
{: step}

First, install Advanced Cluster Management on your hub cluster to enable centralized management.

### Install the ACM operator
{: #rovs-acm-install-operator}

1. Log in to your hub cluster:
   ```sh
   ibmcloud ks cluster config --cluster <hub-cluster-name> --admin
   ```
   {: pre}

2. Create a namespace for ACM:
   ```sh
   oc create namespace open-cluster-management
   ```
   {: pre}

3. Install the ACM operator from OperatorHub:
   ```sh
   cat <<EOF | oc apply -f -
   apiVersion: operators.coreos.com/v1alpha1
   kind: Subscription
   metadata:
     name: advanced-cluster-management
     namespace: open-cluster-management
   spec:
     channel: release-2.11
     installPlanApproval: Automatic
     name: advanced-cluster-management
     source: redhat-operators
     sourceNamespace: openshift-marketplace
   EOF
   ```
   {: pre}

4. Wait for the operator to be installed:
   ```sh
   oc get csv -n open-cluster-management
   ```
   {: pre}

   Wait until the CSV shows `PHASE: Succeeded`.

### Create the MultiClusterHub instance
{: #rovs-acm-create-hub}

1. Create the MultiClusterHub resource:
   ```sh
   cat <<EOF | oc apply -f -
   apiVersion: operator.open-cluster-management.io/v1
   kind: MultiClusterHub
   metadata:
     name: multiclusterhub
     namespace: open-cluster-management
   spec: {}
   EOF
   ```
   {: pre}

2. Monitor the installation:
   ```sh
   oc get mch -n open-cluster-management -w
   ```
   {: pre}

   Wait until the status shows `Running`. This can take 10-15 minutes.

3. Verify the ACM console is accessible:
   ```sh
   oc get route multicloud-console -n open-cluster-management
   ```
   {: pre}

4. Access the ACM console using the route URL and log in with your OpenShift credentials.

## Create a Virtualization Service cluster through ACM
{: #rovs-acm-create-cluster}
{: step}

Deploy a new Virtualization Service cluster as a managed cluster through the ACM interface.

### Prepare cluster credentials
{: #rovs-acm-credentials}

1. In the ACM console, navigate to **Credentials** > **Add credential**.

2. Select **IBM Cloud** as the credential type.

3. Enter your IBM Cloud credentials:
   - **Credential name**: `ibmcloud-vpc-creds`
   - **Namespace**: `open-cluster-management`
   - **API key**: Your IBM Cloud API key
   - **Region**: Your target region (e.g., `us-south`)

4. Click **Add** to save the credentials.

### Create a cluster set
{: #rovs-acm-cluster-set}

1. In the ACM console, navigate to **Infrastructure** > **Clusters**.

2. Click **Cluster sets** > **Create cluster set**.

3. Configure the cluster set:
   - **Cluster set name**: `virtualization-clusters`
   - **Description**: `Clusters running OpenShift Virtualization Service`

4. Click **Create**.

### Deploy the Virtualization Service cluster
{: #rovs-acm-deploy-cluster}

1. In the ACM console, navigate to **Infrastructure** > **Clusters**.

2. Click **Create cluster** > **IBM Cloud**.

3. Configure the cluster details:
   - **Cluster name**: `ve-managed-cluster-1`
   - **Cluster set**: Select `virtualization-clusters`
   - **Credentials**: Select `ibmcloud-vpc-creds`
   - **Infrastructure**: Select **VPC Gen 2**

4. Configure the cluster specifications:
   - **OpenShift version**: Select 4.21 or later
   - **Region**: Select your target region
   - **Zones**: Select at least 3 zones
   - **VPC**: Select your VPC
   - **Subnets**: Select subnets for each zone

5. Configure worker nodes:
   - **Flavor**: Select a bare metal flavor (e.g., `bx2d.metal.96x384`)
   - **Worker nodes per zone**: Enter `3`

6. In the **Additional configurations** section, add:
   ```yaml
   offering: openshift-vs
   ```
   {: codeblock}

7. Review the configuration and click **Create**.

8. Monitor the cluster creation in the ACM console. The cluster typically takes 30-45 minutes to provision.

## Configure governance policies for virtual machines
{: #rovs-acm-policies}
{: step}

Set up policies to ensure consistent configuration and compliance across your Virtualization Service clusters.

### Create a namespace policy
{: #rovs-acm-namespace-policy}

1. In the ACM console, navigate to **Governance** > **Policies**.

2. Click **Create policy**.

3. Configure the policy:
   - **Name**: `ve-required-namespaces`
   - **Namespace**: `open-cluster-management-policies`
   - **Remediation**: `enforce`

4. Add the policy template:
   ```yaml
   apiVersion: policy.open-cluster-management.io/v1
   kind: Policy
   metadata:
     name: ve-required-namespaces
     namespace: open-cluster-management-policies
   spec:
     remediationAction: enforce
     disabled: false
     policy-templates:
       - objectDefinition:
           apiVersion: policy.open-cluster-management.io/v1
           kind: ConfigurationPolicy
           metadata:
             name: ve-namespaces
           spec:
             remediationAction: enforce
             severity: high
             object-templates:
               - complianceType: musthave
                 objectDefinition:
                   apiVersion: v1
                   kind: Namespace
                   metadata:
                     name: vm-workloads
   ```
   {: codeblock}

5. Click **Create**.

6. Create a placement binding to apply the policy to your cluster set:
   ```sh
   cat <<EOF | oc apply -f -
   apiVersion: policy.open-cluster-management.io/v1
   kind: PlacementBinding
   metadata:
     name: ve-namespace-binding
     namespace: open-cluster-management-policies
   placementRef:
     name: virtualization-clusters-placement
     kind: PlacementRule
     apiGroup: apps.open-cluster-management.io
   subjects:
     - name: ve-required-namespaces
       kind: Policy
       apiGroup: policy.open-cluster-management.io
   EOF
   ```
   {: pre}

### Create a resource quota policy
{: #rovs-acm-quota-policy}

1. Create a policy to enforce resource quotas for VM workloads:
   ```sh
   cat <<EOF | oc apply -f -
   apiVersion: policy.open-cluster-management.io/v1
   kind: Policy
   metadata:
     name: ve-resource-quotas
     namespace: open-cluster-management-policies
   spec:
     remediationAction: enforce
     disabled: false
     policy-templates:
       - objectDefinition:
           apiVersion: policy.open-cluster-management.io/v1
           kind: ConfigurationPolicy
           metadata:
             name: vm-resource-quotas
           spec:
             remediationAction: enforce
             severity: medium
             object-templates:
               - complianceType: musthave
                 objectDefinition:
                   apiVersion: v1
                   kind: ResourceQuota
                   metadata:
                     name: vm-quota
                     namespace: vm-workloads
                   spec:
                     hard:
                       requests.cpu: "100"
                       requests.memory: 500Gi
                       persistentvolumeclaims: "50"
   EOF
   ```
   {: pre}

2. Bind the policy to your cluster set:
   ```sh
   cat <<EOF | oc apply -f -
   apiVersion: policy.open-cluster-management.io/v1
   kind: PlacementBinding
   metadata:
     name: ve-quota-binding
     namespace: open-cluster-management-policies
   placementRef:
     name: virtualization-clusters-placement
     kind: PlacementRule
     apiGroup: apps.open-cluster-management.io
   subjects:
     - name: ve-resource-quotas
       kind: Policy
       apiGroup: policy.open-cluster-management.io
   EOF
   ```
   {: pre}

### Create a security policy
{: #rovs-acm-security-policy}

1. Create a policy to enforce security standards for VMs:
   ```sh
   cat <<EOF | oc apply -f -
   apiVersion: policy.open-cluster-management.io/v1
   kind: Policy
   metadata:
     name: ve-vm-security
     namespace: open-cluster-management-policies
   spec:
     remediationAction: inform
     disabled: false
     policy-templates:
       - objectDefinition:
           apiVersion: policy.open-cluster-management.io/v1
           kind: ConfigurationPolicy
           metadata:
             name: vm-security-standards
           spec:
             remediationAction: inform
             severity: high
             object-templates:
               - complianceType: mustnothave
                 objectDefinition:
                   apiVersion: kubevirt.io/v1
                   kind: VirtualMachine
                   metadata:
                     namespace: vm-workloads
                   spec:
                     template:
                       spec:
                         domain:
                           devices:
                             disks:
                               - disk:
                                   bus: virtio
                                 name: containerdisk
   EOF
   ```
   {: pre}

## Monitor virtual machines across clusters
{: #rovs-acm-monitoring}
{: step}

Use ACM's observability features to monitor VM workloads across your managed clusters.

### Enable observability
{: #rovs-acm-enable-observability}

1. In the ACM console, navigate to **Observe environments** > **Overview**.

2. Click **Enable observability** if not already enabled.

3. Configure the observability settings:
   - **Storage size**: `100Gi` (adjust based on your needs)
   - **Storage class**: Select an available storage class
   - **Retention**: `7d` (adjust based on your needs)

4. Click **Enable**.

### Create custom dashboards for VMs
{: #rovs-acm-dashboards}

1. In the ACM console, navigate to **Observe environments** > **Grafana**.

2. Click **Create dashboard**.

3. Add panels to monitor:
   - VM CPU usage across clusters
   - VM memory usage across clusters
   - VM disk I/O metrics
   - VM network traffic
   - Number of running VMs per cluster

4. Save the dashboard as `Virtualization Service Overview`.

### Set up alerts
{: #rovs-acm-alerts}

1. Create an alert for high VM resource usage:
   ```sh
   cat <<EOF | oc apply -f -
   apiVersion: v1
   kind: ConfigMap
   metadata:
     name: thanos-ruler-custom-rules
     namespace: open-cluster-management-observability
   data:
     custom_rules.yaml: |
       groups:
         - name: vm-alerts
           interval: 30s
           rules:
             - alert: HighVMCPUUsage
               expr: kubevirt_vmi_vcpu_seconds_total > 0.8
               for: 5m
               labels:
                 severity: warning
               annotations:
                 summary: "High CPU usage on VM"
                 description: "VM {{ \$labels.name }} has high CPU usage"
             - alert: HighVMMemoryUsage
               expr: kubevirt_vmi_memory_used_bytes / kubevirt_vmi_memory_available_bytes > 0.9
               for: 5m
               labels:
                 severity: warning
               annotations:
                 summary: "High memory usage on VM"
                 description: "VM {{ \$labels.name }} has high memory usage"
   EOF
   ```
   {: pre}

## Deploy virtual machines through ACM
{: #rovs-acm-deploy-vms}
{: step}

Use ACM's application lifecycle management to deploy VMs across your managed clusters.

### Create an application for VM deployment
{: #rovs-acm-vm-application}

1. Create a Git repository with your VM definitions or use the ACM console.

2. In the ACM console, navigate to **Applications** > **Create application**.

3. Configure the application:
   - **Name**: `sample-vm-app`
   - **Namespace**: `vm-workloads`
   - **Repository type**: `Git`
   - **URL**: Your Git repository URL
   - **Branch**: `main`
   - **Path**: `vms/`

4. Configure placement:
   - **Cluster set**: Select `virtualization-clusters`
   - **Deploy to**: Select specific clusters or use labels

5. Create a sample VM definition in your Git repository:
   ```yaml
   apiVersion: kubevirt.io/v1
   kind: VirtualMachine
   metadata:
     name: fedora-vm
     namespace: vm-workloads
   spec:
     running: true
     template:
       metadata:
         labels:
           kubevirt.io/vm: fedora-vm
       spec:
         domain:
           devices:
             disks:
               - name: containerdisk
                 disk:
                   bus: virtio
               - name: cloudinitdisk
                 disk:
                   bus: virtio
             interfaces:
               - name: default
                 masquerade: {}
           resources:
             requests:
               memory: 2Gi
               cpu: 2
         networks:
           - name: default
             pod: {}
         volumes:
           - name: containerdisk
             containerDisk:
               image: quay.io/containerdisks/fedora:latest
           - name: cloudinitdisk
             cloudInitNoCloud:
               userData: |
                 #cloud-config
                 password: fedora
                 chpasswd: { expire: False }
   ```
   {: codeblock}

6. Click **Create** to deploy the application.

7. Monitor the deployment in the ACM console under **Applications**.

## Implement disaster recovery for VMs
{: #rovs-acm-dr}
{: step}

Set up disaster recovery strategies for your virtual machine workloads using ACM.

### Configure VM backup policies
{: #rovs-acm-backup}

1. Install the OADP (OpenShift API for Data Protection) operator on your managed clusters through ACM:
   ```sh
   cat <<EOF | oc apply -f -
   apiVersion: policy.open-cluster-management.io/v1
   kind: Policy
   metadata:
     name: install-oadp
     namespace: open-cluster-management-policies
   spec:
     remediationAction: enforce
     disabled: false
     policy-templates:
       - objectDefinition:
           apiVersion: policy.open-cluster-management.io/v1
           kind: ConfigurationPolicy
           metadata:
             name: oadp-operator
           spec:
             remediationAction: enforce
             severity: high
             object-templates:
               - complianceType: musthave
                 objectDefinition:
                   apiVersion: operators.coreos.com/v1alpha1
                   kind: Subscription
                   metadata:
                     name: oadp-operator
                     namespace: openshift-adp
                   spec:
                     channel: stable-1.3
                     name: oadp-operator
                     source: redhat-operators
                     sourceNamespace: openshift-marketplace
   EOF
   ```
   {: pre}

2. Create a backup schedule for VMs:
   ```sh
   cat <<EOF | oc apply -f -
   apiVersion: velero.io/v1
   kind: Schedule
   metadata:
     name: vm-daily-backup
     namespace: openshift-adp
   spec:
     schedule: "0 2 * * *"
     template:
       includedNamespaces:
         - vm-workloads
       includedResources:
         - virtualmachines
         - virtualmachineinstances
         - persistentvolumeclaims
       storageLocation: default
       ttl: 720h0m0s
   EOF
   ```
   {: pre}

### Set up VM migration between clusters
{: #rovs-acm-migration}

1. Create a placement rule for VM migration:
   ```sh
   cat <<EOF | oc apply -f -
   apiVersion: apps.open-cluster-management.io/v1
   kind: PlacementRule
   metadata:
     name: vm-migration-placement
     namespace: vm-workloads
   spec:
     clusterSelector:
       matchLabels:
         environment: production
         virtualization: enabled
     clusterReplicas: 1
   EOF
   ```
   {: pre}

2. Use ACM's application placement to migrate VMs between clusters by updating the placement rules.

## Next steps
{: #rovs-acm-next-steps}

Now that you have set up ACM for managing Virtualization Service clusters:

- [Explore advanced ACM features](https://access.redhat.com/documentation/en-us/red_hat_advanced_cluster_management_for_kubernetes){: external}
- [Learn about VM live migration](https://docs.redhat.com/en/documentation/openshift_container_platform/4.21/html/virtualization/live-migration){: external}
- [Configure advanced networking for VMs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.21/html/virtualization/index#virt-networking){: external}
- [Set up GitOps workflows for VM deployments](https://access.redhat.com/documentation/en-us/red_hat_advanced_cluster_management_for_kubernetes/2.11/html/applications/managing-applications){: external}
- [Implement multi-cluster service mesh](https://access.redhat.com/documentation/en-us/red_hat_advanced_cluster_management_for_kubernetes/2.11/html/services/services-overview){: external}

## Related information
{: #rovs-acm-related}

- [Advanced Cluster Management documentation](https://access.redhat.com/documentation/en-us/red_hat_advanced_cluster_management_for_kubernetes){: external}
- [OpenShift Virtualization documentation](https://docs.redhat.com/en/documentation/openshift_container_platform/4.21/html/virtualization){: external}
- [Managing Virtualization Service clusters](/docs/openshift?topic=openshift-rovs-manage)
- [Creating a Virtualization Service cluster](/docs/openshift?topic=openshift-rovs-cluster-create)
