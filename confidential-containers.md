---

copyright:
  years: 2025, 2025
lastupdated: "2025-09-29"

keywords: confidential containers

subcollection: openshift

---


{{site.data.keyword.attribute-definition-list}}

# Creating confidential containers
{: #confidential-containers}

Learn how to install and use confidential containers, which are also known as Kata Containers or OpenShift Sandboxed Containers, in a {{site.data.keyword.openshiftlong_notm}} cluster.



## What are confidential containers?
{: #what-is-it?}

A confidential container provides a secure runtime environment for sensitive workloads, but allows you to continue to work within existing workflows.

The IBM Cloud implementation of confidential containers leverages peer pods to extend the functionality of Red Hat OpenShift pods into a separate VSI from the worker node. This extension creates a trusted execution environment beyond traditional Kubernetes and OpenShift. 


Learn more:
- Review the [reasons](https://docs.redhat.com/en/documentation/openshift_sandboxed_containers/1.10/html/deploying_openshift_sandboxed_containers/about-osc#osc-features_about-osc) you might use confidential containers.
- Check out the [FAQ](/docs/openshift?topic=openshift-faqs#conf-cont-cost) for confidential containers.


## Prerequisites
{: #prerequisites}

- Ensure you have a {{site.data.keyword.openshiftlong_notm}} cluster in a [region that supports TDX Virtual Server Instances (VSIs)](/docs/vpc?topic=vpc-about-confidential-computing-vpc).

- If necessary, enable [OperatorHub](https://cloud.ibm.com/docs/openshift?topic=openshift-operators). Sometimes OperatorHub is disabled in a cluster for security reasons.

- Your cluster must have a public interface or you can connect to its environment through a VPN.


## Step 1: Installing the operator
{: #install-operator}

Install the OpenShift Sandboxed Containers Operator to manage the lifecycle of confidential containers in clusters.

1. Open the [cluster dashboard](https://cloud.ibm.com/containers/cluster-management/clusters).

1. Click **OpenShift web console** > **Operators** > **OperatorHub**.

1. Search for `OpenShift Sandboxed Containers Operator`.

1. Install the supported and stable version of the OpenShift Sandboxed Containers Operator, version 1.10.3. Refer to Red Hat's [Operator Update Information Checker](https://access.redhat.com/labs/ocpouic/?operator=sandboxed-containers-operator) for supported OpenShift versions.



## Step 2: Importing the peer pod image
{: #peer-pod-image}

The OpenShift Sandboxed Containers Operator launches a special operating system inside the peer pod that must be imported into your IBM Cloud Account. This operating system is required to deploy a workload to a confidential container.

The peer pod image contains a full Red Hat Enterprise Linux (RHEL) 9.6 operating system with the software required to instantiate a container in a Confidential Virtual Machine (CVM).

All configurations and installed packages in the operating system remain the default Red Hat values. However, the IBM Cloud VSIs require `cloud init` to work. In the scripts, `cloud init` is prevented from being uninstalled when it is finished building the `podvm`, which is a key difference from its [source image](https://github.com/confidential-devhub/coco-podvm-scripts/tree/konflux-osc-dm-verity-image).
{: note}

Before you begin:

Validate version compatibility. The image is supported for the following versions.
- OpenShift Sandboxed Containers Operator version 1.10.3
- OpenShift versions 4.19, 4.18, 4.17, and 4.16 clusters

To import the peer pod image:

1. Open the [compute images](https://cloud.ibm.com/infrastructure/compute/images).

1. Click the **Create +** icon, choose a region with TDX-capable VSIs, and complete the required fields.

1. For **Image source**, select **Cloud Object Storage**.

1. For the **Locate by image file URL** field, enter `cos://us-south/podvm-image/rhel9-podvm-latest.qcow2`.

1. Click **Create custom image**.

1. When the image is added to the [Images list](https://cloud.ibm.com/infrastructure/compute/images), click the image name and select **IDs**. Then, note the **Image ID** to use later.

1. Repeat these steps when a new version of the image is available.



## Step 3: Creating an API key or trusted profile
{: #api-key-or-trusted-profile}

Confidential containers require a credential to instantiate the peer pod through `kata-remote` when a secure workload is launched. This credential must be either a valid API key or trusted profile with permissions to create a VSI in your account.

-  **API Key** from the UI {: ui}

   1. From the IBM Cloud dashboard, click **Manage** > **Access (IAM)** > **API keys**.
   
   1. Click the **Create** button to create a key.

   2. Save this key securely because it cannot be retrieved from this page later.

- **API Key** from the CLI. {: cli}

    Run the following command and save the output.
    ```sh
    ibmcloud iam api-key-create <key_name>
    ```
    {: pre}

- **Trusted Profile**

    1. Open the [trusted profiles dashboard](https://cloud.ibm.com/iam/trusted-profiles).

    2. [Create a trusted profile](/docs/openshift?topic=openshift-configure-trusted-profile) and grant the profile the necessary permissions to create virtual servers from OpenShift.

        a. Create a trusted profile.

        ```sh
        ibmcloud iam trusted-profile-create <NAME> [--description <DESCRIPTION>]
        ```
        {: pre}

        b. Allow the resources in `openshift-sandboxed-containers-operator` to use the trusted profile.
        
        ```sh
        ibmcloud iam trusted-profile-rule-create <NAME or ID of the trusted profile> --name <RULE_NAME> --type Profile-CR --conditions claim:namespace,operator:EQUALS,value:openshift-sandboxed-containers-operator --cr-type ROKS_SA
        ```
        {: pre}

        c. Allow access to the VPC Infrastructure Services (`is`).
        
        To allow access for every resource in the account:
        ```sh
        ibmcloud iam trusted-profile-policy-create <NAME or ID of the trusted profile>  --roles Editor,Writer --service-name is
        ```
        {: pre}

        To allow access for a specific resource group:
        ```sh
        iam trusted-profile-policy-create <NAME or ID of the trusted profile> --roles Viewer [--resource-group-id <resource group>]
        ```
        {: pre}

   



## Step 4: Creating an SSH key (Optional)
{: #ssh-key}

In test clusters, you might find it helpful to have an SSH key ready to troubleshoot why something isn't starting and to view logs. In production clusters, you probably do not want the SSH functionality enabled.

1. Click **Infrastructure** > **Compute** > **SSH Keys**.

1. Create an SSH key and note the **SSH key ID**.



## Step 5: Configuring confidential containers
{: #configure-confidential-containers}

After the Operator is installed, create ConfigMaps to allow Kata to handle workloads in the IBM Cloud account.

Before you begin, you can either complete these steps to set up the CLI or you can use the [IBM Cloud shell](https://cloud.ibm.com/shell) to run commands.

1. [Install the `ks` and the `oc` CLI tools](/docs/openshift?topic=openshift-cli-install).

1. List the clusters in the account.

    ```sh
    ibmcloud ks cluster ls
    ```
    {: pre}

1. Run the `config` command.

    ```sh
    ibmcloud ks cluster config --cluster CLUSTER_ID --admin --endpoint link
    ```
    {: pre}

1. Confirm that the `oc` commands run properly.

    ```sh
    oc get nodes
    ```
    {: pre}


To configure confidential containers:

1. Set up environment variables for the API key, trusted profile ID, cluster name, PodVM image ID, SSH key ID, and VPC ID.

    ```sh
    export IBMCLOUD_API_KEY=<your API key>
    export IBMCLOUD_TRUSTED_PROFILE_ID="<your Trusted Profile ID>"
    export CLUSTER_NAME=<your cluster name>
    export PODVM_IMAGE_ID=<PodVM image ID provided by IBM or a custom-built image>
    export SSH_KEY_ID=<SSH key ID to be used by the peer pod VSI>
    export VPC_ID=<the VPC that your Openshift cluster is in>
    ```
    {: pre}

1. Create the `feature-gates.yaml` ConfigMap.

    ```yaml
    apiVersion: v1
    kind: ConfigMap
    metadata:
      name: osc-feature-gates
      namespace: openshift-sandboxed-containers-operator
    data:
      deploymentMode: "DaemonSetFallback" # or DaemonSet to force it
      confidential: "true"
      layeredImageDeployment: "false"
    ```
    {: codeblock}

1. Apply the ConfigMap.

    ```sh
    oc apply -f feature-gates.yaml
    ```
    {: pre}

1. Create the `peer-pods-secret.yaml`.

    ```yaml
    apiVersion: v1
    kind: Secret
    metadata:
      name: peer-pods-secret
      namespace: openshift-sandboxed-containers-operator
    type: Opaque
    stringData:
      # either IBMCLOUD_API_KEY or IBMCLOUD_IAM_PROFILE_ID must be set
      # if you specify both the IBMCLOUD_API_KEY will be used
      IBMCLOUD_API_KEY: "$IBMCLOUD_API_KEY"
      IBMCLOUD_IAM_ENDPOINT: "https://iam.cloud.ibm.com/identity/token"
      IBMCLOUD_IAM_PROFILE_ID: "$IBMCLOUD_TRUSTED_PROFILE_ID"
    ```
    {: codeblock}

1. Apply the secret to the cluster.

    ```sh
    oc apply -f peer-pods-secret.yaml
    ```
    {: pre}

1. Create the `peer-pods-cm.yaml` ConfigMap. 

    ```yaml

    apiVersion: v1
    kind: ConfigMap
    metadata:
      name: peer-pods-cm
      namespace: openshift-sandboxed-containers-operator
    data:
      CLOUD_PROVIDER: "ibmcloud"
      IBMCLOUD_PODVM_IMAGE_ID: "$PODVM_IMAGE_ID"
      IBMCLOUD_PODVM_INSTANCE_PROFILE_LIST: "bx3dc-2x10"
      IBMCLOUD_PODVM_INSTANCE_PROFILE_NAME: "bx3dc-2x10"
      IBMCLOUD_RESOURCE_GROUP_ID: "$(ibmcloud is vpc "$VPC_ID" -json | jq -r .resource_group.id)"
      IBMCLOUD_SSH_KEY_ID: "$SSH_KEY_ID"
      IBMCLOUD_VPC_ENDPOINT: "https://us-east.iaas.cloud.ibm.com/v1"
      IBMCLOUD_VPC_ID: "$VPC_ID"
      IBMCLOUD_VPC_SG_ID: "$(ibmcloud ks security-group ls --cluster $CLUSTER_NAME -json | jq -r '.[] | select(.type == "cluster") | .id')"
      CLOUD_CONFIG_VERIFY: "false"
      CRI_RUNTIME_ENDPOINT: "/run/cri-runtime/containerd.sock"
      ENABLE_CLOUD_PROVIDER_EXTERNAL_PLUGIN: "false"
      VXLAN_PORT: ""
      TUNNEL_TYPE: ""
      INITDATA: ""
    ```
    {: codeblock}

1. Apply the ConfigMap. 

    ```sh
    oc apply -f peer-pods-cm.yaml
    ```
    {: pre}
    
1. Create the `kata-runtime-settings.yaml` KataConfig.

    ```yaml
    apiVersion: kataconfiguration.openshift.io/v1
    kind: KataConfig
    metadata:
      name: kata-runtime-settings
      namespace: openshift-sandboxed-containers-operator
    spec:
      enablePeerPods: true
      logLevel: info
     #checkNodeEligibility: true
     #kataConfigPoolSelector:
     #  matchLabels:
     #    <label_key>: '<label_value>'
    ```
    {: codeblock}

1. Apply the KataConfig.

    ```sh
    oc apply -f kata-runtime-settings.yaml
    ```
    {: pre}

1. As Kata is installed and the daemonsets are started, you can run the following command to watch the labels update with the current state of the installation. When installation is complete, the state is displayed as `installed`.

    ```sh
    oc get nodes --output yaml|egrep "kata-ds-rpm-install|ibm-cloud.kubernetes.io/worker-id"
    ```
    {: pre}

    Possible states:

    - `waiting_to_install`: The Kata installation is queued on the node.
    - `installing`: The Kata installation is in progress.
    - `installed`: Kata is installed successfully on the node.
    - `waiting_for_reboot`: The node must be rebooted to complete the installation or uninstallation.
    - `waiting_to_uninstall`: The Kata uninstallation is queued on the node.
    - `uninstalling`: The Kata uninstallation is in progress.
    - `uninstalled`: Kata is uninstalled successfully from the node.

1. When the labels are updated, [reboot](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_reboot) the worker node.


## Step 6: Configuring a trust authority
{: #trustee}

Attestation is a critical part of confidential containers. You must validate supply chain code security, that the code running in the container wasn’t modified. You can leverage an Intel TDX chip and the key-broker-service protocol. The image for a `podvm` already has working TDX driver code and a `kbs_client` in it. You must configure the INITDATA with the trustee details though. 

1. Select a trustee. There are many options for trustee in confidential containers.

    - For development purposes, you might launch a [VM for a trustee](https://github.com/confidential-containers/cloud-api-adaptor/blob/main/src/cloud-api-adaptor/ibmcloud/ROKS_SETUP.md#deploy-a-test-trustee) on it. 

    - For a production-level service, you might use [Intel Trust Authority](https://docs.trustauthority.intel.com/main/articles/articles/ita/introduction.html).


2. If you selected the VM for a trustee for development purposes, complete these configuration steps.

    a. Get the IP address of the VSI.

    ```sh
    export KBS_SERVICE_ENDPOINT="https://REPLACE_WITH_TRUSTEE_IP:8080"
    export INITDATA=$(cat <<EOF | gzip | base64 -w0
    algorithm = "sha256"
    version = "0.1.0"

    [data]
    "aa.toml" = '''
    [token_configs]
    [token_configs.coco_as]
    url = "$KBS_SERVICE_ENDPOINT"

    [token_configs.kbs]
    url = "$KBS_SERVICE_ENDPOINT"
    '''

    "cdh.toml"  = '''
    socket = 'unix:///run/confidential-containers/cdh.sock'
    credentials = []

    [kbc]
    name = "cc_kbc"
    url = "$KBS_SERVICE_ENDPOINT"
    '''
    EOF
    )
    ```
    {: pre}

    b. Verify the `$INITDATA` environment variable.

    ```sh
    echo $INITDATA
    ```
    {: pre}

    c. Add the value for the variable to the `peer-pods-cm.yaml` ConfigMap in the `openshift-sandboxed-containers-operator` namespace.

    d. If confidential containers are already installed, restart the `cloud-api-adapter` daemonset in the openshift-sandboxed-containers-operator namespace.

    e. Repeat these steps for each workload entry of `INITDATA`.
    
    f. The `INITDATA` value can be applied to an individual container as an annotation and the container that starts is configured to use the trustee. This annotation can be helpful when testing new trustees or making sure that changes to `INITDATA` don’t break any confidential containers. 

    Example annotation:

    ```yaml
    apiVersion: v1
    kind: Pod
      metadata:
        name: mypod
        annotations:
          io.katacontainers.config.hypervisor.cc_init_data: $INITDATA
    spec:
      runtimeClassName: kata-remote
    ```
    {: codeblock}



## Step 7: Running a confidential container workload
{: #run-workload}

After all labels are updated to `installed`, deploy a workload by using the `kata-remote` runtime class name in a `pod.yaml` file. You can use the Hello World example as a test workload in a confidential container. 

1. Create a `pod.yaml` file.

    ```yaml
    apiVersion: v1
    kind: Pod
    metadata:
    name: helloworld
    namespace: default
    spec:
    runtimeClassName: kata-remote
    containers:
    - name: helloworld
        image: docker.io/istio/examples-helloworld-v1:1.0
        ports:
        - containerPort: 5000
    ```
    {: codeblock}

1. Create the pod.

    ```sh
    oc create -f pod.yaml
    ```
    {: pre}

1. Monitor the deployment in the [Virtual Servers list](https://cloud.ibm.com/infrastructure/compute/vs).

1. Review the logs in the `openshift-sandboxed-containers-operator` namespace.

    - Controller managed pod logs: `pod/controller-manager-UNIQUE_ID`
    - Cloud API adapter pod logs: `pod/osc-caa-ds-UNIQUE_ID`
    - Application logs: Depends on location specified.

    You can also review critical information by running the following command.

    ```sh
    oc describe pod/helloworld
    ```
    {: pre}

Your confidential containers setup is now complete! Still need help? Check out the [troubleshooting](/docs/openshift?topic=openshift-ts-confidential-containers).



## Removing workloads and tools
{: #uninstall}

Completing these steps in the wrong order could leave resources behind that you are billed for, such as a VSI.
{: important}

### Removing workloads
{: #uninstall_workloads}

1. Delete the workloads from the cluster that use confidential containers.

    a. Show all pods.

    ```sh
    oc get pods -A -o json | jq '.items[] | select(.spec.runtimeClassName == "kata-remote") | "\(.metadata.namespace)/\(.metadata.name)"'
    ```
    {: pre}

    b. Delete the pods, which deletes the VSIs deployed for them.  

    If you changed the previous ConfigMaps to invalid configurations or the credentials have been removed, the software cannot complete the API calls to remove the resources and they will have to manually be removed. Manual removal should only be used in this scenario because you might be required you to make a new OpenShift cluster or replace workers.
    {: note}

1. Delete the Kata configuration. The `kata-runtime-settings.yaml` removes the Kata from the workers, which you can watch as the labels are updated.

    a. Monitor the node labels until they are in the `waiting_for_reboot` state.

    b. [Reboot](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_reboot) the workers one at a time to finish uninstalling the Kata on the worker node.

    c. If other workloads are running on this cluster, cordon the worker, drain it, and then restart it.
        
    d. Wait until the `kata-runtime-settings.yaml` deletion is finished after rebooting to continue to the next step. There are processes that must finish uninstalling after reboot.

    Do not continue if `kata-runtime-settings.yaml` resources fail to delete.
    {: important}

1. Delete the ConfigMaps.


### Uninstalling the operator
{: #uninstall_operator}

After you have removed the workloads, you can uninstall the OpenShift Sandboxed Containers Operator.

1. Uninstall the operator. 

1. Confirm there are no remaining resources in the `openshift-sandboxed-containers-operator` namespace.

1. Delete the namespace.
