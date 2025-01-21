---

copyright: 
  years: 2024, 2025
lastupdated: "2025-01-21"


keywords: openshift, {{site.data.keyword.openshiftlong_notm}}, ai, add-on

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}

# Managing the Red Hat OpenShift AI add-on
{: #ai-addon-manage}

{{site.data.keyword.attribute-definition-list}}

Use the following information to manage the OpenShift AI add-on.
{: shortdesc}

## Updating the IBM-managed OpenShift AI operator
{: #ai-addon-update}

Version updates for the OpenShift AI operator follow the schedule of version updates for the OpenShift AI Platform. If the OpenShift AI Platform releases a patch, minor, or major version update, a corresponding update is made available for the add-on. Based on the approval policy (`oaiInstallPlanApproval`) you set when the add-on was installed, you may need to manually approve and apply certain updates. 

Version rollbacks are not supported. You cannot undo an update to the OpenShift AI operator. Take this into consideration and make sure you choose your update strategy carefully, especially if you choose the `Automatic` approval policy. 
{: important}

### Major updates
{: #ai-addon-update-major}

The process to apply major updates depends on how you set the approval policy. 

Approval policy set to `Automatic`
:   You do not need to manually approve the major update. To apply the major update, you only need to run the [`ibmcloud oc cluster addon update openshift-ai` command](#ai-addon-update-apply). 

Approval policy set to `Manual`
:   Apply the major update by running the [`ibmcloud oc cluster addon update openshift-ai` command](#ai-addon-update-apply). Then, [manually approve the install plan](#ai-addon-update-approve) to complete the update. 

### Minor and patch updates 
{: #ai-addon-update-minorpatch}

The process to apply minor and patch updates depends on how you set the approval policy. 

Approval policy set to `Automatic`
:   You do not need to manually approve the update plan. Updates are applied automatically and you do not need to take any action. 

Approval policy set to `Manual`
:   - Some portions of the update might require manual approval, and others might not. The portions that require approval are indicated in the update notification. The portions of the update that do not require the approval are automatically applied.
:   - You must [manually approve](#ai-addon-update-approve) the portions of the update that require the approval.  After you approve the install plan, there are no additional steps to apply the command. 

### Applying the update
{: #ai-addon-update-apply}

To apply the update, run the following command. 

```sh
ibmcloud oc cluster addon update openshift-ai --cluster CLUSTER --version VERSION
```
{: pre}

### Approving the install plan and applying the update
{: #ai-addon-update-approve}

To approve the install plan, navigate to your cluster page and open the OpenShift web console. In the **Installed Operators** section, follow the prompts to manually approve the update install plan. For major updates, complete this step after you run the command to apply the update.

## Disabling the add-on
{: #ai-addon-disable}

Follow the steps to disable the OpenShift AI add-on.

1. **Optional**: Remove operators. Depending on the deletion policy you set for the add-on, the operators and components installed by the add-on may or may not be automatically removed when you disable the add-on. You can use the following commands to manually remove the operators. 

    Remove the Red Hat OpenShift AI Platform.
    ```sh
     oc -n kube-system patch cm managed-addon-rhoai-options --type json -p '[{"op": "replace", "path": "/data/oaiDeletePolicy", "value": "delete"}]
    ```
    {: pre}

    Remove the Node Feature Discovery Operator.
    ```sh
     oc -n kube-system patch cm managed-addon-rhoai-options --type json -p '[{"op": "replace", "path": "/data/nfdDeletePolicy", "value": "delete"}]
    ```
    {: pre}

    Remove the NVIDIA GPU Operator.
    ```sh
     oc -n kube-system patch cm managed-addon-rhoai-options --type json -p '[{"op": "replace", "path": "/data/nvidiaDeletePolicy", "value": "delete"}]
    ```
    {: pre}

    Remove the Pipeline Operator.
    ```sh
     oc -n kube-system patch cm managed-addon-rhoai-options --type json -p '[{"op": "replace", "path": "/data/pipelineDeletePolicy", "value": "delete"}]
    ```
    {: pre}

2. Run the command to disable the add-on.

    ```sh
    ibmcloud oc cluster addon disable openshift-ai --cluster CLUSTER
    ```
    {: pre}

    Example output.

    ```
    Data and resources that you created for the add-on might be deleted when the add-on is disabled. Continue? [y/N]> y
    Disabling add-on openshift-ai for cluster abcdefg123456...
    OK
    ```
    {: screen}


## Getting support for the OpenShift AI add-on
{: #ai-addon-support}

If you encounter issues related to the OpenShift AI add-on for IBM Cloud, you can [open a support case](/docs/openshift?topic=openshift-get-help). 

In your support case, make sure to include the output and details for the following commands. Including this information can help speed up the support process. 

Run these commands to gather details for the OpenShift AI platform. Include the outputs in your support case. 

```sh
ibmcloud oc cluster addon ls --cluster CLUSTER
oc get clusterversions
oc get subscription -A
oc get OperatorGroups -A
oc get csv
oc get IbmOpenshiftAI
oc describe IbmOpenshiftAI ibmopenshiftai-auto 
oc get all -n ibm-rhoai-operator
oc get Clusterpolicy gpu-cluster-policy
oc describe Clusterpolicy gpu-cluster-policy
oc -n redhat-ods-operator get subscription rhods-operator 
```
{: pre}

Run these commands to gather details for the cluster. Include the outputs in your support case. 

```sh
oc adm must-gather -- /usr/bin/gather_audit_logs
oc adm must-gather
tar cvaf must-gather.tar.gz must-gather.local.*/ 
```
{: pre}
