---

copyright:
  years: 2023, 2023
lastupdated: "2023-08-28"

keywords: openshift, debug, cloud pak, daemson set, feature gates, failed to set

subcollection: openshift
content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}


# Why do I see a `failed to set feature gates` error when upgrading a worker node?
{: #ts-cloud-pak-ds}
{: troubleshoot}
{: support}


When you try to upgrade a worker node in a cluster with a Cloud Pak installation, the worker node goes from `Ready` to `Critical` and stays in `Critical`. Check if a ConfigMap exists for the Cloud Pak deployer by running `kubectl get cm cloud-pak-node-fix-config -n kube-system -o yaml`.
{: tsSymptoms}



This error happens because the Cloud Pak deployer (`cloud-pak-deployer`) makes changes to the kubelet config file. However, if the kubelet config file contains changes between versions, for example between 4.10 and 4.11, then the deployer doesn't update the config file.
{: tsCauses}

If you see this error, you must manually update the `cloud-pak-node-fix-config` configmap.
{: tsResolve}

Review the following steps based on your target cluster version.

### Upgrading from 4.11 to 4.12
{: #cdp-feature-gates-412}


1. Edit the ConfigMap and remove the following feature gates.

    ```yaml
    CSIMigrationAWS: False
    CSIMigrationGCE: False
    CRIContainerLogRotation: true
    ```
    {: screen}


    ```sh
    kubectl edit cm cloud-pak-node-fix-config -n kube-system -o yaml
    ```
    {: pre}

1. Reboot the worker node. 

1. After rebooting, continue to upgrade your worker nodes.

1. If the issue persists, contact support. Open a [support case](/docs/get-support?topic=get-support-using-avatar). In the case details, be sure to include any relevant log files, error messages, or command outputs.

### Upgrading from 4.10 to 4.11
{: #cdp-feature-gates-411}


1. Edit the ConfigMap and remove the following feature gates.

    ```yaml
    CSIMigrationOpenStack
    ServiceLBNodePortControl
    CSIMigrationAzureDisk
    ```
    {: screen}


    ```sh
    kubectl edit cm cloud-pak-node-fix-config -n kube-system -o yaml
    ```
    {: pre}

1. Reboot the worker node. 

1. After rebooting, continue to upgrade your worker nodes.

1. If the issue persists, contact support. Open a [support case](/docs/get-support?topic=get-support-using-avatar). In the case details, be sure to include any relevant log files, error messages, or command outputs.

