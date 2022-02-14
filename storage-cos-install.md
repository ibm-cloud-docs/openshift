---

copyright:
  years: 2014, 2022
lastupdated: "2022-02-14"

keywords: openshift

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}

# Installing the {{site.data.keyword.cos_full_notm}} plug-in
{: #storage_cos_install}

Install the {{site.data.keyword.cos_full_notm}} plug-in with a Helm chart to set up pre-defined storage classes for {{site.data.keyword.cos_full_notm}}. You can use these storage classes to create a PVC to provision {{site.data.keyword.cos_full_notm}} for your apps.
{: shortdesc}

Looking for instructions for how to update or remove the {{site.data.keyword.cos_full_notm}} plug-in? See [Updating the plug-in](#update_cos_plugin) and [Removing the plug-in](#remove_cos_plugin).
{: tip}

The {{site.data.keyword.cos_full_notm}} plug-in requires at least 0.2 vCPU and 128 MB of memory.
{: note}

Before you begin: [Access your {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-access_cluster).

To install the `ibmc` Helm plug-in and the `ibm-object-storage-plugin`:

1. Make sure that your worker node applies the latest patch for your minor version to run your worker node with the latest security settings. The patch version also ensures that the root password on the worker node is renewed. 

    If you did not apply updates or reload your worker node within the last 90 days, your root password on the worker node expires and the installation of the storage plug-in might fail. 
    {: note}

    1. List the current patch version of your worker nodes.
        ```sh
        ibmcloud oc worker ls --cluster <cluster_name_or_ID>
        ```
        {: pre}

        Example output
        ```sh
        OK
        ID                                                  Public IP        Private IP     Machine Type           State    Status   Zone    Version
        kube-dal10-crb1a23b456789ac1b20b2nc1e12b345ab-w26   169.xx.xxx.xxx    10.xxx.xx.xxx   b3c.4x16.encrypted     normal   Ready    dal10   1.21.6_1523*
        ```
        {: screen}

        If your worker node does not apply the latest patch version, you see an asterisk (`*`) in the **Version** column of your CLI output.

    2. Review the [version changelog](/docs/containers?topic=containers-changelog) to find the changes that are in the latest patch version.

    3. Apply the latest patch version by reloading your worker node. Follow the instructions in the [ibmcloud oc worker reload command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_reload) to gracefully reschedule any running pods on your worker node before you reload your worker node. Note that during the reload, your worker node machine is updated with the latest image and data is deleted if not [stored outside the worker node](/docs/openshift?topic=openshift-storage_planning#persistent_storage_overview).
1. Review the changelog and verify support for your [cluster version and architecture](/docs/containers?topic=containers-cos_plugin_changelog).
2. [Follow the instructions](/docs/openshift?topic=openshift-helm#install_v3) to install the version 3 Helm client on your local machine.

    If you enabled [VRF](/docs/account?topic=account-vrf-service-endpoint#vrf) and [service endpoints](/docs/account?topic=account-vrf-service-endpoint#service-endpoint) in your {{site.data.keyword.cloud_notm}} account, you can use the private {{site.data.keyword.cloud_notm}} Helm repository to keep your image pull traffic on the private network. If you can't enable VRF or service endpoints in your account, use the public Helm repository.
    {: note}

3. Add the {{site.data.keyword.cloud_notm}} Helm repo to your cluster.

    ```sh
    helm repo add ibm-helm https://raw.githubusercontent.com/IBM/charts/master/repo/ibm-helm
    ```
    {: pre}

4. Update the Helm repo to retrieve the most recent version of all Helm charts in this repo.
    ```sh
    helm repo update
    ```
    {: pre}

5. If you installed the {{site.data.keyword.cos_full_notm}} Helm plug-in earlier, remove the `ibmc` plug-in.
    ```sh
    helm plugin uninstall ibmc
    ```
    {: pre}

6. Download the Helm charts and unpack the charts in your current directory.

    ```sh
    helm fetch --untar ibm-helm/ibm-object-storage-plugin
    ```
    {: pre}

    If the output shows `Error: failed to untar: a file or directory with the name ibm-object-storage-plugin already exists`, delete your `ibm-object-storage-plugin` directory and rerun the `helm fetch` command.
    {: tip}

7. If you use OS X or a Linux distribution, install the {{site.data.keyword.cos_full_notm}} Helm plug-in `ibmc`. The plug-in automatically retrieves your cluster location and to set the API endpoint for your {{site.data.keyword.cos_full_notm}} buckets in your storage classes. If you use Windows as your operating system, continue with the next step.
    1. Install the Helm plug-in.
        ```sh
        helm plugin install ./ibm-object-storage-plugin/helm-ibmc
        ```
        {: pre}

    2. Verify that the `ibmc` plug-in is installed successfully.
        ```sh
        helm ibmc --help
        ```
        {: pre}

        If the output shows the error `Error: fork/exec /home/iksadmin/.helm/plugins/helm-ibmc/ibmc.sh: permission denied`, run `chmod 755 /Users/<user_name>/Library/helm/plugins/helm-ibmc/ibmc.sh`. Then, rerun `helm ibmc --help`.
        {: tip}

        Example output

        ```sh
        helm version: v3.2.4+g0ad800e
        Install or upgrade Helm charts in IBM K8S Service(IKS) and IBM Cloud Private(ICP)
        Usage:
            helm ibmc [command]
        Available Commands:
            install           Install a Helm chart
            upgrade           Upgrade the release to a new version of the Helm chart
        Available Flags:
            -h, --help        (Optional) This text.
            -u, --update      (Optional) Update this plugin to the latest version
        Example Usage:
            Install: helm ibmc install ibm-object-storage-plugin ibm-helm/ibm-object-storage-plugin
            Upgrade: helm ibmc upgrade [RELEASE] ibm-helm/ibm-object-storage-plugin
        Note:
            1. It is always recommended to install latest version of ibm-object-storage-plugin chart.
            2. It is always recommended to have 'kubectl' client up-to-date.
        ```
        {: screen}

8. Optional: Limit the {{site.data.keyword.cos_full_notm}} plug-in to access only the Kubernetes secrets that hold your {{site.data.keyword.cos_full_notm}} service credentials. By default, the plug-in can access all Kubernetes secrets in your cluster.
    1. [Create your {{site.data.keyword.cos_full_notm}} service instance](#create_cos_service).
    2. [Store your {{site.data.keyword.cos_full_notm}} service credentials in a Kubernetes secret](#create_cos_secret).
    3. From the `ibm-object-storage-plugin`, navigate to the `templates` directory and list available files.
        **OS X and Linux**

        ```sh
        cd templates && ls
        ```
        {: pre}

        **Windows**

        ```sh
        chdir templates && dir
        ```
        {: pre}

    4. Open the `provisioner-sa.yaml` file and look for the `ibmcloud-object-storage-secret-reader` `ClusterRole` definition.
    5. Add the name of the secret that you created earlier to the list of secrets that the plug-in is authorized to access in the `resourceNames` section.
        ```yaml
        kind: ClusterRole
        apiVersion: rbac.authorization.k8s.io/v1beta1
        metadata:
         name: ibmcloud-object-storage-secret-reader
        rules:
        - apiGroups: [""]
          resources: ["secrets"]
          resourceNames: ["<secret_name1>","<secret_name2>"]
          verbs: ["get"]
        ```
        {: codeblock}

    6. Save your changes and navigate to your working directory.


9. Install the `ibm-object-storage-plugin` in your cluster. When you install the plug-in, pre-defined storage classes are added to your cluster. If you completed the previous step for limiting the {{site.data.keyword.cos_full_notm}} plug-in to access only the Kubernetes secrets that hold your {{site.data.keyword.cos_full_notm}} service credentials and you are still targeting the `templates` directory, change directories to your working directory. **VPC clusters only**: To enable authorized IPs on VPC, set the `--set bucketAccessPolicy=true` flag.

Example `helm ibmc install` command for OS X and Linux.

```sh
helm ibmc install ibm-object-storage-plugin ibm-helm/ibm-object-storage-plugin --set license=true [--set bucketAccessPolicy=false]
```
{: pre}

Example `helm install` command for Windows.

```sh
helm install ibm-object-storage-plugin ./ibm-object-storage-plugin --set dcname="${DC_NAME}" --set provider="${CLUSTER_PROVIDER}" --set workerOS="${WORKER_OS}" --region="${REGION} --set platform="${PLATFORM}" --set license=true [--set bucketAccessPolicy=false]
```
{: pre}


`DC_NAME`
:   The cluster data center. To retrieve the data center, run `oc get cm cluster-info -n kube-system -o jsonpath="{.data.cluster-config\.json}{'\n'}"`. Store the data center value in an environment variable by running `SET DC_NAME=<datacenter>`. Optional: Set the environment variable in Windows PowerShell by running `$env:DC_NAME="<datacenter>"`.

`CLUSTER_PROVIDER`
:   The infrastructure provider. To retrieve this value, run `oc get nodes -o jsonpath="{.items[*].metadata.labels.ibm-cloud\.kubernetes\.io\/iaas-provider}{'\n'}"`. If the output from the previous step contains `softlayer`, then set the `CLUSTER_PROVIDER` to `"IBMC"`. If the output contains `gc`, `ng`, or `g2`, then set the `CLUSTER_PROVIDER` to `"IBMC-VPC"`. Store the infrastructure provider in an environment variable. For example: `SET CLUSTER_PROVIDER="IBMC-VPC"`.

`WORKER_OS` and `PLATFORM`
:   The operating system of the worker nodes. To retrieve these values, run `oc get nodes -o jsonpath="{.items[*].metadata.labels.ibm-cloud\.kubernetes\.io\/os}{'\n'}"`. Store the operating system of the worker nodes in an environment variable. For {{site.data.keyword.openshiftlong_notm}} clusters, run `SET WORKER_OS="redhat"` and `SET PLATFORM="openshift"`. 

`REGION`
:   The region of the worker nodes. To retrieve this value, run `oc get nodes -o yaml | grep 'ibm-cloud\.kubernetes\.io/region'`. Store the region of the worker nodes in an environment variable by running `SET REGION="< region>"`. |