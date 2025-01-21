---

copyright: 
  years: 2025, 2025
lastupdated: "2025-01-21"


keywords: openshift

subcollection: openshift

content-type: troubleshoot

---


{{site.data.keyword.attribute-definition-list}}





# Debugging the Cloud Object Storage add-on
{: #ts-storage-cos-csi-addon}
{: support}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf}


The `ibm-object-csi-driver` add-on does not run properly.


Follow these steps to gather gather details about the issue.

1. Pull the cluster configuration. 
    ```sh
    ibmcloud ks cluster config -c <cluster_name/cluster_id>
    ```
    {: pre}
   
1. Check the health of the add-on to ensure it is deployed properly.
    ```sh
    ibmcloud ks cluster addon ls --cluster <cluster_name/cluster_id>
    ```
    {: pre}

1. Check the version of the installed add-on. It is recommended to use the latest version for better support.
    ```sh
    ibmcloud ks cluster addon ls --cluster <cluster_name/cluster_id> | grep ibm-object-csi-driver
    ```
    {: pre}

1. Make sure that all CSI driver pods are in `running` state.
    ```sh
    oc get pods -n ibm-object-csi-operator | grep ibm-object-csi
    ```
    {: pre}
  
If any CSI driver pod is in `ImagePullBackOff` state, that means the image used for pods creation is not avaialble in the registry or there might be permission issues. Gather the output from the previous steps and, contact support. Open a [support case](/docs/account?topic=account-using-avatar). In the case details, be sure to include any relevant log files, error messages, or command outputs.
  
If any CSI driver pod is in `CrashLoopBackOff` state, you can try the following steps:

1. Describe that pod.
    ```sh
    oc describe pod ibm-ibm-object-csi-xxx -n ibm-object-csi-operator
    ```
    {: pre}

1. Look for the container that is continuously restarting.

1. Collect logs for more details.
    ```sh
    oc logs ibm-ibm-object-csi-xxx -n ibm-object-csi-operator
    ```
    {: pre}

1. Upgrade the add-on to the latest version for a possible fix.

1. If the issue persists, contact support. Open a [support case](/docs/account?topic=account-using-avatar). In the case details, be sure to include any relevant log files, error messages, or command outputs.

If you need to contact support for further help, make sure you gather the following details for the support ticket.

* Add-on health status and add-on version mentioned above.

* PVC describe
    ```sh
    oc describe pvc <PVC-NAME> -n <PVC-NAMESPACE>
    ```
    {: pre}

* PV describe
    ```sh
    oc describe pv <pv-name>
    ```
    {: pre}

* Pod describe
    ```sh
    oc describe pod <POD-NAME> -n <POD-NAMESPACE> 
    ```
    {: pre}

* Logs of `controller-manager` pod
    ```sh
    oc logs ibm-ibm-object-csi-operator-controller-manager-xxx -n ibm-object-csi-operator 
    ```
    {: pre}

* Logs of `csi-node` pod
    ```sh
    oc logs ibm-object-csi-node-xxx -n ibm-object-csi-operator 
    ```
    {: pre}

