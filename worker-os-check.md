---

copyright: 
  years: 2023, 2023
lastupdated: "2023-08-31"

keywords: openshift, kubernetes, allowlist, operating system, rhel, ubuntu, s390x

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}



# Checking your worker node operating system
{: #flavor-os-check}

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
        OS Image:                   Ubuntu 20.04.5 LTS
        Operating System:           linux
        Architecture:               amd64
        ...
    ```
    {: screen}

