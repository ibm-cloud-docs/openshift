---

copyright: 
  years: 2023, 2025
lastupdated: "2025-10-06"


keywords: openshift, {{site.data.keyword.openshiftlong_notm}}, kubernetes, allowlist, operating system, rhel, ubuntu

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}



# Checking your cluster version, operating system, and Kubernetes server version
{: #flavor-os-check}

Review the following steps to check your {{site.data.keyword.openshiftlong_notm}} cluster version, worker node versions and operating system, and Kubernetes server version. For a list of supported versions and operating systems, see the [Version information](/docs/openshift?topic=openshift-openshift_versions).
{: shortdesc}

## Checking your cluster master version, worker node version, and worker node operating system in the console
{: #cluster-version-ui}
{: ui}

1. From the [console](https://cloud.ibm.com/containers/cluster-management/clusters){: external}, review your cluster master version.
1. Select your cluster, then select **Worker nodes** to review your worker node version.
1. Select **Worker pools** then expand your worker pools to see their operating system.


## Checking your cluster master version in the CLI
{: #cluster-version-cli}
{: cli}

Log in to your cluster to check your cluster version.

1. [Log in to your account. If applicable, target the appropriate resource group. Set the context for your cluster.](/docs/containers?topic=containers-access_cluster)
1. List your clusters and review the output.
    ```sh
    ibmcloud oc cluster ls
    ```
    {: pre}

    Example output
    ```sh
    cluster-us-south              cn6thtsd0ghdc110k9jg   normal        2 months ago   3         Dallas               4.14.10_1546_openshift    Default               vpc-gen2
    ```
    {: screen}

## Checking your worker node version in the CLI
{: #worker-version-cli}
{: cli}

Log in to your cluster to check your cluster version.

1. [Log in to your account. If applicable, target the appropriate resource group. Set the context for your cluster.](/docs/containers?topic=containers-access_cluster)
1. Get your cluster ID.
    ```sh
    ibmcloud oc cluster ls
    ```
    {: pre}

1. List your worker nodes and review the output.
    ```sh
    ibmcloud oc worker ls -c CLUSTER
    ```
    {: pre}

    Example output
    ```sh
    ID                                                      Primary IP     Flavor     State    Status   Zone       Version
    kube-cn5gdcio0lv9l8m831ig-bharoksvpc-default-00000197   10.248.128.5   bx2.4x16   normal   Ready    jp-osa-3   4.14.10_1546_openshift*
    kube-cn5gdcio0lv9l8m831ig-bharoksvpc-default-000002a3   10.248.64.5    bx2.4x16   normal   Ready    jp-osa-2   4.14.10_1546_openshift*
    kube-cn5gdcio0lv9l8m831ig-bharoksvpc-default-00000371   10.248.0.5     bx2.4x16   normal   Ready    jp-osa-1   4.14.10_1546_openshift*
    ```
    {: screen}

## Checking a cluster's Kubernetes server version in the CLI
{: #kube-version-check}
{: cli}


To check the Kubernetes server version of a cluster, log in to the cluster and run the following command.




```sh
oc version
```
{: pre}

Example output
```sh
Client Version: 4.18.3
Server Version: 4.18.12
Kubernetes Version: v1.32.2
```
{: screen}



## Checking your worker node operating system in the CLI
{: #worker-os-check}
{: cli}

When you create a worker pool, you choose the flavor, which describes the operating system along with the compute resources of the worker nodes.

You can also log in to your cluster to check the operating system of the worker nodes.
1. [Log in to your account. If applicable, target the appropriate resource group. Set the context for your cluster.](/docs/containers?topic=containers-access_cluster)
2. List your worker nodes.
    ```sh
    oc get nodes
    ```
    {: pre}

3. Describe your worker node and check for the operating system label that IBM applies, or the **OS Image** and **Operating System** fields in the **System Info** section.
    ```sh
    oc describe node <node>
    ```
    {: pre}

    Example output

    ```sh
    NAME:               10.xxx.xx.xxx
    Roles:              <none>
    Labels:             arch=amd64
                        ...
                        ibm-cloud.kubernetes.io/os=UBUNTU_20_64
                        ...
                        kubernetes.io/arch=amd64
                        kubernetes.io/hostname=10.189.33.198
                        kubernetes.io/os=linux
    ...
    System Info:
        OS Image:                   Ubuntu 24.04.5 LTS
        Operating System:           linux
        Architecture:               amd64
        ...
    ```
    {: screen}
