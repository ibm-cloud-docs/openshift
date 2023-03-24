---

copyright:
  years: 2022, 2023
lastupdated: "2023-03-24"

keywords: openshift, openshift data foundation, openshift container storage, vpc, air-gapped

subcollection: openshift

content-type: tutorial
services: openshift, vpc
account-plan:
completion-time: 2h

---


{{site.data.keyword.attribute-definition-list}}




# Installing OpenShift Data Foundation on a private cluster
{: #openshift-storage-odf-private}
{: toc-content-type="tutorial"}
{: toc-services="openshift, vpc"}
{: toc-completion-time="2h"}


OpenShift Data Foundation is a highly available storage solution that you can use to manage persistent storage for your containerized workloads in {{site.data.keyword.openshiftlong}} clusters.
{: shortdesc}

This is an experimental feature that is available for evaluation and testing purposes and might change without notice.
{: experimental}

In standard OpenShift Data Foundation configurations, the operators and drivers pull images from public container registries like registry.redhat.io. However, in private-only, air-gapped clusters (without access to the public internet) you must first mirror the ODF images to {{site.data.keyword.registrylong_notm}}, then configure your OpenShift Data Foundation deployment to pull those images from a private container registry.

Since this approach involves manually mirroring images from registry.redhat.io to your {{site.data.keyword.registrylong_notm}}, this means you are responsible for repeating the mirroring process to get the latest patch updates or security fixes when they are available for OpenShift Data Foundation.
{: important}




## Prerequisites 
{: #odf-private-prereq}

Before you install OpenShift Data Foundation in your cluster, meet the following prerequisite conditions.

1. Create a Red Hat account if you do not already have one. For more information on creating a Red Hat account, see [Create a Red Hat login](https://www.redhat.com/wapps/ugc/register.html?_flowId=register-flow&_flowExecutionKey=e1s1){: external}.
1. Create or have access to a private cluster for OpenShift Data Foundation. If you already have a private cluster make sure it meets the following requirements.
    - Your cluster version must be at least version 4.11.
    - Your worker node operating system must be RHEL 8.
    - 1 Virtual Private Cloud (VPC) with 3 subnets (1 per zone) with no public gateway attached.
    - 1 {{site.data.keyword.openshiftlong_notm}} cluster with at least 3 worker nodes spread evenly across 3 zones. The worker nodes must be at least 16x64.
1. An {{site.data.keyword.registrylong_notm}} instance with at least one namespace in the same region as your cluster. If you don't have an instance of {{site.data.keyword.registrylong_notm}}, see [Getting started with {{site.data.keyword.registryshort}}](/docs/Registry?topic=Registry-getting-started) to create one.



## Create an additional subnet in your VPC and attach a Public Gateway
{: #odf-storage-private-vm}
{: step}

In addition to the 3 required subnets, create another subnet and attach a public gateway to it.

[From the Subnets for VPC console](https://cloud.ibm.com/vpc-ext/network/subnets){: external}, create an additional subnet in your VPC. Note that this subnet must be separate from the subnets your worker nodes are in and must have a public gateway attached.


## Create a bastion host
{: #odf-storage-bastion}
{: step}

[From the Virtual Servers for VPC console](https://cloud.ibm.com/vpc-ext/provision/vs){: external}, create a virtual server in the subnet that you created in the previous step. This virtual server is used as a bastion host to connect to your private cluster. The operating system for your bastion host must be at least Ubuntu 20.04 or RHEL 8.

## Reserve a floating IP and bind it to your bastion host
{: #odf-floating-ip-bind}
{: step}

[From the **Floating IPs** console](https://cloud.ibm.com/vpc-ext/network/floatingIPs){: external}, reserve a floating IP in the zone where the subnet that you created earlier is located and bind it to your bastion host.

## Install the CLI tools
{: #odf-cli-install-bastion}
{: step}

1. From the {{site.data.keyword.redhat_openshift_notm}} [downloads page](https://console.redhat.com/openshift/downloads), download the {{site.data.keyword.redhat_openshift_notm}} command-line interface (`oc`) and the {{site.data.keyword.redhat_openshift_notm}} Client (oc) mirror plug-in.

1. Copy the `oc` and the `oc-mirror` tar files to your bastion host. 
    ```sh
    scp /path/to/download root@BASTION-HOST-IP:/root
    ```
    {: pre}
    
    
1. Log in to your bastion host. For more information, see [Connecting to your instance](/docs/vpc?topic=vpc-creating-a-vpc-using-the-ibm-cloud-console&interface=cli#connecting-to-your-instance).
    ```sh
    ssh -i <path-to-key-file> root@<bastion-host-ip-address>
    ```
    {: pre}
    
1. Unpack each of tar files and move them to `/usr/local/bin`.
    ```sh
    tar -C /usr/local/bin -xvzf oc.tar.gz
    ```
    {: pre}
    
    ```sh
    tar -C /usr/local/bin -xvzf oc-mirror.tar.gz
    ```
    {: pre}
    
1. Install the {{site.data.keyword.cloud_notm}} CLI tools.
    ```sh
    curl -fsSL https://clis.cloud.ibm.com/install/linux | sh
    ```
    {: pre}
    
1. Install the `container-service` and `container-registry` plug-ins.
    ```sh
    ibmcloud plugin install container-service
    ```
    {: pre}
    
    ```sh
    ibmcloud plugin install container-registry
    ```
    {: pre}
    
1. Install [Podman](https://podman.io/getting-started/installation){: external}.
    

## Log in to your cluster and disable the default OperatorHub sources
{: #odf-storage-disable-operatorhub}
{: step}

In a restricted network environment, you must have administrator access to disable the default catalogs. You can then configure OperatorHub to use local catalog sources.

While logged into your bastion host, complete the following steps.

1. [Access your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-access_cluster).

1. Disable the default remote OperatorHub sources.
    ```sh
    oc patch operatorhub cluster --type json -p '[{"op": "add", "path": "/spec/disableAllDefaultSources", "value": true}]'
    ```
    {: pre}

## Log in to your container registries
{: #odf-storage-login-registry}
{: step}

1. Log in to `registry.redhat.io`. If you don't have a Red Hat account, follow the steps to [create one](https://sso.redhat.com/auth/realms/redhat-external/protocol/openid-connect/auth?client_id=customer-portal&redirect_uri=https%3A%2F%2Faccess.redhat.com%2Fwebassets%2Favalon%2Fj%2Fincludes%2Fsession%2Fscribe%2F%3FredirectTo%3Dhttps%253A%252F%252Faccess.redhat.com%252Ftags%252Flogin&state=cb7a0391-a189-468d-b979-aaebc5344f26&nonce=1e7e5af7-0323-46da-8a69-54d204a182e8&response_mode=fragment&response_type=code&scope=openid).

    ```sh
    podman login registry.redhat.io
    ```
    {: pre}


1. Log in to {{site.data.keyword.registrylong_notm}} with the username `iamapikey`.
    ```sh
    podman login us.icr.io -u iamapikey -p IAM-API-KEY
    ```
    {: pre}
    
    
## Create a namespace in {{site.data.keyword.registrylong_notm}}
{: #odf-private-registry-namespace-create}
{: step}

1. Set the {{site.data.keyword.registrylong_notm}} region in your CLI. This region must be the same region your cluster is in.
    ```sh
    ibmcloud cr region-set us-south
    ```
    {: pre}
    
1. Create a namespace in {{site.data.keyword.registrylong_notm}}. This namespace is used for the OpenShift Data Foundation images.
    ```sh
    ibmcloud cr namespace-add NAMESPACE
    ```
    {: pre}


## Mirror the Operator index to {{site.data.keyword.registrylong_notm}}
{: #odf-storage-mirror-catalog}
{: step}

1. Copy the following `ImageSetConfiguration` and save it as a file called `imageset.yaml`.
    ```yaml
    apiVersion: mirror.openshift.io/v1alpha2
    kind: ImageSetConfiguration
    storageConfig:
      registry:
        imageURL: us.icr.io/NAMESPACE/redhat-operator-index 
        skipTLS: false
    mirror:
      operators:
        - catalog: registry.redhat.io/redhat/redhat-operator-index:v4.10
          packages:
            - name: local-storage-operator
            - name: ocs-operator
            - name: mcg-operator
            - name: odf-operator
            - name: odf-csi-addons-operator
    ```
    {: codeblock}

1. Mirror the OpenShift Data Foundation images from `registry.redhat.io` to your {{site.data.keyword.registrylong_notm}} namespace.
    
    Before running `oc-mirror` make sure to set the umask of your bastion host to `0022`.
    {: important}

    ```sh
    oc-mirror --config=imageset.yaml docker://us.icr.io/NAMESPACE --dest-skip-tls
    ```
    {: pre}


## Create a secret to pull images from {{site.data.keyword.registrylong_notm}}
{: #odf-storage-create-secret}
{: step}

1. Find and record your unique Red Hat registry pull secret. For more information on how to find your Red Hat registry pull secret, see [Red Hat Container Registry Authentication](https://access.redhat.com/RegistryAuthentication){: external}.

1. Rename the `pull-secret` file secret to `auth.json`.

1. Encode your IAM API key in base64.
    ```sh
    printf "iamapikey:IAM-API-KEY" | base64
    ```
    {: pre}

1. Add the following section to your `auth.json` file.
    ```json 
    {"auths": {"us.icr.io": {"auth": "BASE64-VALUE","email": "IBM-EMAIL"}}}
    ```
    {: codeblock}

1. Create the secret in the `openshift-marketplace` namespace.
    ```sh
    oc create secret generic odf-secret -n openshift-marketplace --from-file=.dockerconfigjson=auth.json  --type=kubernetes.io/dockerconfig
    ```
    {: pre}

## Update the catalog source in your cluster
{: #odf-storage-create-catalog}
{: step}

1. After mirroring is complete, a results directory is created on your bastion host called `oc-mirror-workspace`.

1. Change directories into the `oc-mirror-workspace` directory.
    ```sh
    cd oc-mirror-workspace
    ```
    {: pre}
    
1. Look for a `results-XXX` directory and `cd` into it.
    ```sh
    ls
    ```
    {: pre}
    
    ```sh
    cd results-XXX
    ```
    {: pre}

1. Look for the `catalogSource-redhat-operator-index.yaml`.
    ```sh
    ls
    ```
    {: pre}

1. Edit the catalog source. Change the name to `redhat-operators`, add the `odf-secret`, and your registry details.
    ```yaml
    apiVersion: operators.coreos.com/v1alpha1
    kind: CatalogSource
    metadata:
      name: redhat-operators # Make sure the name is redhat-operators
      namespace: openshift-marketplace
    spec:
      image: us.icr.io/NAMESPACE/redhat/redhat-operator-index:v4.10 # Add your registry
      sourceType: grpc
      displayName: Red Hat Operators
      publisher: Red Hat
      updateStrategy:
        registryPoll:
          interval: 10m0s
      secrets: # Add the odf-secret
        - "odf-secret" 
    ```
    {: codeblock}

1. Create the catalog source in your cluster.
    ```sh
    oc create -f catalogSource-redhat-operator-index.yaml
    ```
    {: pre}

1. Verify that the pods and `packagemanifest` are created in your cluster. 
    ```sh 
    oc get pods,packagemanifest -n openshift-marketplace
    ```
    {: pre}




## Update your image pull secret
{: #odf-private-update-dockerconf}
{: step}

1. Extract the global pull secret to a file called `.dockerconfigjson`.
    ```sh
    oc extract secret/pull-secret -n openshift-config --to=.
    ```
    {: pre}
    
    Example output
    ```sh
    .dockerconfigjson
    ```
    {: pre}

1. Print the details of your `auth.json` file.
    ```sh
    printf auth.json
    ```
    {: pre}
    
1. Add the `icr.io` section from `auth.json` to your `.dockerconfigjson`.
    ```json 
    {"auths": {"us.icr.io": {"auth": "BASE64-VALUE","email": "IBM-EMAIL"}}}
    ```
    {: codeblock}
    

1. Update the pull secret in the `openshift-config` namespace to use your `.dockerconfigjson`.
    ```sh
    oc set data secret/pull-secret -n openshift-config --from-file=.dockerconfigjson
    ```
    {: pre}

## Replace each worker node to pick up configuration changes
{: #odf-private-reload-workers}
{: step}

1. Get a list of nodes in your cluster.
    ```sh
    ibmcloud oc worker ls -c CLUSTER
    ```
    {: pre}

1. Run the `ibmcloud oc worker replace` to replace each worker node in your cluster.
    ```sh
    ibmcloud oc worker replace -c CLUSTER --worker WORKER-NODE
    ```
    {: pre}
    
## Update the `registries.conf` file on each node
{: #odf-private}
{: step}

After replacing each worker node, start a debug pod on each node and update the `registries.conf` file.

1. List your worker nodes with `oc get nodes`.
    ```sh
    oc get nodes
    ```
    {: pre}

1. Start a debug pod on one of the nodes.
    ```sh
    oc debug node/NODE-NAME
    ```
    {: pre}
 
1. Allow host binaries.
    ```sh
    chroot /host
    ```
    {: pre}
    
1. Open the `registries.conf` file.
    ```sh
    vi etc/containers/registries.conf
    ```
    {: pre}
    
    
1. Append the following image mappings to the `registries.conf` file.
    ```txt
    [[registry]]
      location = "registry.redhat.io/odf4"
      insecure = false
      blocked = false
      mirror-by-digest-only = false
      prefix = ""

      [[registry.mirror]]
      location = "us.icr.io/NAMESPACE/odf4"
      insecure = false

    [[registry]]
      location = "registry.redhat.io/openshift4"
      insecure = false
      blocked = false
      mirror-by-digest-only = false
      prefix = ""

      [[registry.mirror]]
      location = "us.icr.io/NAMESPACE/openshift4"
      insecure = false

    [[registry]]
      location = "registry.redhat.io/ocs4"
      insecure = false
      blocked = false
      mirror-by-digest-only = false
      prefix = ""

      [[registry.mirror]]
      location = "us.icr.io/NAMESPACE/ocs4"
      insecure = false

    [[registry]]
      location = "registry.redhat.io/rhceph"
      insecure = false
      blocked = false
      mirror-by-digest-only = false
      prefix = ""

      [[registry.mirror]]
      location = "us.icr.io/NAMESPACE/rhceph"
      insecure = false

    [[registry]]
      location = "registry.redhat.io/rhel8"
      insecure = false
      blocked = false
      mirror-by-digest-only = false
      prefix = ""

      [[registry.mirror]]
      location = "us.icr.io/NAMESPACE/rhel8"
      insecure = false
    ```
    {: codeblock}


1. For each of the registry mirrors that you added in the previous step (`openshift4`, `ocs4`, `rhceph`, `rhel8`), remove the duplicate entry in `registries.conf` that has an `armada-master` mirror location.

    Example `rhel8` registry to remove from `registries.conf`.
    ```sh
    [[registry]]
      location = "registry.redhat.io/rhel8/postgresql-12"
      insecure = false
      blocked = false
      mirror-by-digest-only = false
      prefix = ""

      [[registry.mirror]]
      location = "us.icr.io/armada-master/rhel8-postgresql-12"
      insecure = false
    ```
    {: screen}
    
1. Repeat the previous steps to update the `registries.conf` file on each worker node.


## Reboot each worker node
{: #odf-private-reboot-workers}
{: step}

1. Reboot each worker node in your cluster one at a time.
    ```sh
    ibmcloud oc worker reboot -c CLUSTER -w WORKER
    ```
    {: pre}
    
1. Wait for each node to reach the `Ready` status before rebooting the next.
    
    
    
## Install the OpenShift Data Foundation add-on from the console
{: #install-odf-console-private}
{: step}

To install ODF in your cluster, complete the following steps.
{: shortdesc}

1. Before you enable the add-on, review the [change log](/docs/openshift?topic=openshift-odf_addon_changelog) for the latest version information. Note that the add-on supports `n+1` cluster versions. For example, you can deploy version `4.10.0` of the add-on to an OCP `4.9` or `4.11` cluster. If you have a cluster version other than the default, you must install the add-on from the CLI and specify the `--version` option.
1. [Review the parameter reference](/docs/openshift?topic=openshift-deploy-odf-vpc&interface=ui#odf-vpc-param-ref)
1. From the [{{site.data.keyword.redhat_openshift_notm}} clusters console](https://cloud.ibm.com/kubernetes/clusters?platformType=openshift){: external}, select the cluster where you want to install the add-on.
1. On the cluster **Overview** page, find the OpenShift Data Foundation card and click **Install**. The **Install ODF** panel opens.
1. In the **Install ODF** panel, enter the configuration parameters that you want to use for your ODF deployment.
1. Select either **Essentials** or **Advanced** as your billing plan.
1. If you want to automatically discover the available storage devices on your worker nodes and use them in ODF, select **Local disk discovery**.
1. In the **Worker nodes** field, enter the node names of the worker nodes where you want to deploy ODF. You must enter at least 3 worker node names. To find your node names, run the `oc get nodes` command in your cluster. Leave this field blank to deploy ODF on all worker nodes.
1. In the **Number of OSD disks required** field, enter the number of OSD disks (app storage) to provision on each worker node.
1. If you are re-enabling the add-on to upgrade the add-on version, select the **Upgrade ODF** option.
1. If you want to encrypt the volumes used by the ODF system pods, select **Enable cluster encryption**.
1. If you want to enable encryption on the OSD volumes (app storage), select **Enable volume encryption**.
    1. In the **Instance name** field, enter the name of your {{site.data.keyword.hscrypto}} instance. For example: `Hyper-Protect-Crypto-Services-eugb`.
    1. In the **Instance ID** field, enter your {{site.data.keyword.hscrypto}} instance ID. For example: `d11a1a43-aa0a-40a3-aaa9-5aaa63147aaa`.
    1. In the **Secret name** field, enter the name of the secret that you created by using your {{site.data.keyword.hscrypto}} credentials. For example: `ibm-hpcs-secret`.
    1. In the **Base URL** field, enter the public endpoint of your {{site.data.keyword.hscrypto}} instance. For example: `https://api.eu-gb.hs-crypto.cloud.ibm.com:8389`.
    1. In the **Token URL** field, enter `https://iam.cloud.ibm.com/identity/token`.


## Verify OpenShift Data Foundation is running
{: #odf-private-verify}
{: step}

1. List the pods in the `openshift-storage` namespace and verify they are running.
    ```sh
    oc get pods -n openshift-storage
    ```
    {: pre}
    
    
1. List the available storage classes.
    ```sh
    oc get sc
    ```
    {: pre}






