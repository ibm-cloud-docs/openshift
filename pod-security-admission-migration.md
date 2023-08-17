---

copyright: 
  years: 2022, 2023
lastupdated: "2023-08-17"

keywords: openshift, deploy, migrating psps to pod security, pod security admission, migrate to pod security admission

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}


# Migrating from PSPs to Pod Security Admission
{: #pod-security-admission-migration}

[Pod Security admission](/docs/containers?topic=containers-pod-security-admission&interface=ui) replaces Pod Security policies (PSPs) in clusters that run version 1.25 or later. Depending on your PSP configuration, you might need to take certain actions before upgrading your cluster from version 1.24 to 1.25.
{: shortdesc}

Your cluster must meet certain PSP configuration requirements before you can upgrade from version 1.24 to 1.25. If your cluster does not meet these requirements, the upgrade is blocked. Complete the following steps to check for any custom PSPs and remove them.
- **If you have not customized or altered PSPs in your cluster**, you can likely upgrade your cluster. However, it is recommended that you review the requirements to make sure that you do not need to modify your PSP configuration before you upgrade your cluster. 
- **If you have customized or altered PSPs in your cluster**, including creating your own PSPs, installing applications that create PSPs, or changing cluster role bindings to restrict the use of certain PSPs, you **must** modify your setup to meet the requirements for upgrading your cluster. 

Before you begin, review the information under [Decide whether Pod Security admission is right for you](https://kubernetes.io/docs/tasks/configure-pod-container/migrate-from-psp/){: external} in the Kubernetes documentation to familiarize yourself with the differences between PSPs and Pod Security admission. 
{: tip}

## Upgrade requirements
{: #psa-upgrade-reqs}

You can upgrade your cluster if your cluster setup meets the following requirements. These requirements ensure that pods run properly under the default Pod Security admission configuration provided in clusters that run version 1.25. If these requirements are not met, your cluster cannot upgrade unless you take additional migration steps.


* All pods run under the `ibm-privileged-psp` PSP.
* The `privileged-psp-user` cluster role binding uses the default configuration.
* The `restricted-psp-user` cluster role binding uses the default configuration.
* Only the following PSPs provided by {{site.data.keyword.cloud_notm}} are present, and no additional PSPs are configured.
    * `ibm-privileged-psp`
    * `ibm-anyuid-psp`
    * `ibm-anyuid-hostpath-psp`
    * `ibm-anyuid-hostaccess-psp`
    * `ibm-restricted-psp`

If your cluster meets these requirements, your pods use a PSP that allows privileged pods. However, meeting these requirements does not mean that all your pods are privileged. 

If you created your own PSPs, installed applications that create PSPs, or changed the cluster role bindings to restrict use of the `ibm-privileged-psp`, you must modify your setup to meet the listed requirements before you can upgrade your cluster. If you use third-party security policy admission controllers, your cluster can still meet these requirements as long as all controllers function properly within the PSP configuration. 

Complete the following steps to confirm that the cluster PSP configuration satisfies the requirements. If all requirements are satisfied, you can upgrade your cluster to version 1.25.

### Step 1: Check that all pods run under the ibm-privileged-psp PSP
{: #psa-migration-pod-check}

Complete the following steps ensure that all pods run under the `ibm-privileged-psp` PSP.

One difference between Pod Security Admission and `PodSecurityPolicies` is that Pod Security Admission is validating while the `PodSecurityPolicies` can be mutating.  This makes it important that pods use the `ibm-privileged-psp`, which is not a mutating PSP, before you upgrade. Because both Pod Security Admission and the `ibm-privileged-psp` are validating, pods work the same under either one.

For example, if a pod is currently running under `ibm-restricted-psp`, it might set the `fsGroup` and `supplementalGroups` to `1` in the pod `securityContext` section, based on the `MustRunAs` range in the PSP. In other words, the `ibm-restricted-psp` can change the pod `securityContext`. Such changes are visible as a difference between the `securityContext` of the running pod and the `securityContext` in the pod template of the deployment or similar resource that creates the pod. The `ibm-privileged-psp` is not mutating, so a pod running under it might run with different groups and might not be able to access data stored in an existing PVC.

1. Get the details of all pods and check their PSPs.

    ```sh
    kubectl get pods -A -o jsonpath="{.items[*].metadata.annotations.kubernetes\.io\/psp}" | tr " " "\n" | sort -u
    ```
    {: pre}
    
1. Review the command output for any PSPs that are not `ibm-privileged-psp`. If your pods are using a different PSP, you must update your application to use the `ibm-privileged-psp` before upgrading your cluster. If no other PSPs are listed, you can continue with the upgrade.

Upgrading to 1.25 is not recommended if the output lists a PSP other than the `ibm-privileged-psp` PSP.
{: important}


### Step 2: Verify the privileged-psp-user cluster role binding uses the default configuration
{: #psa-migration-verify-crb}

Complete the following steps to verify that the `privileged-psp-user` cluster role binding uses the default configuration. This ensures that all service accounts and users are authorized to use the `ibm-restricted-psp` through the `privileged-psp-user` cluster role binding.

Your upgrade to 1.25 fails if the cluster role binding does not have the default `role` and `subjects` exactly as shown in the following example.
{: important}

1. Get the details `privileged-psp-user` cluster role binding.

    ```sh
    kubectl get clusterrolebinding privileged-psp-user -o yaml
    ```
    {: pre}


1. Review the `role` and `subjects` in the output. If the output is different than the following example, do not upgrade to 1.25. If your `privileged-psp-user` cluster role binding matches the following example, you can continue with the upgrade.

    ```yaml
    apiVersion: rbac.authorization.k8s.io/v1
    kind: ClusterRoleBinding
    metadata:
      creationTimestamp: "2022-10-06T20:12:36Z"
      name: privileged-psp-user
      resourceVersion: "151862"
      uid: 15014736-94d2-4cba-a3a8-92dd36de453b
    roleRef:
      apiGroup: rbac.authorization.k8s.io
      kind: ClusterRole
      name: ibm-privileged-psp-user
    subjects:
    - apiGroup: rbac.authorization.k8s.io
      kind: Group
      name: system:masters
    - apiGroup: rbac.authorization.k8s.io
      kind: Group
      name: system:nodes
    - apiGroup: rbac.authorization.k8s.io
      kind: Group
      name: system:serviceaccounts
    - apiGroup: rbac.authorization.k8s.io
      kind: Group
      name: system:authenticated
    ```
    {: codeblock}


### Step 3: Verify the restricted-psp-user cluster role binding uses the default configuration
{: #psa-migration-crb-verify}

Complete the following steps to verify that the `restricted-psp-user` cluster role binding uses the default configuration. This ensures that all service accounts and users are authorized to use the `ibm-restricted-psp` through the `restricted-psp-user` cluster role binding. 

Your upgrade to 1.25 fails if the cluster role binding does not include the default `role` and `subjects` as shown in the following example.
{: important}

1. Get the details of the `restricted-psp-user` cluster role binding

    ```sh
    kubectl get clusterrolebinding restricted-psp-user -o yaml
    ```
    {: pre}
    
1. Review the command output. Do not upgrade your cluster to version 1.25 if the cluster role binding does not include default settings for the `role` and `subjects` as shown in the following example.
    
    ```yaml
    apiVersion: rbac.authorization.k8s.io/v1
    kind: ClusterRoleBinding
    metadata:
      creationTimestamp: "2022-10-06T20:13:10Z"
      name: restricted-psp-user
      resourceVersion: "151890"
      uid: 4edb362f-9933-48d7-95e2-f41cd9f4dead
    roleRef:
      apiGroup: rbac.authorization.k8s.io
      kind: ClusterRole
      name: ibm-restricted-psp-user
    subjects:
    - apiGroup: rbac.authorization.k8s.io
      kind: Group
      name: system:masters
    - apiGroup: rbac.authorization.k8s.io
      kind: Group
      name: system:nodes
    - apiGroup: rbac.authorization.k8s.io
      kind: Group
      name: system:serviceaccounts
    - apiGroup: rbac.authorization.k8s.io
      kind: Group
      name: system:authenticated
    ```
    {: codeblock}


### Step 4: Checking for non-IBM PSPs
{: #psa-migration-check-psp}

Complete the steps to check whether your cluster uses non-IBM PSPs.

Upgrading to version 1.25 fails if the command output includes additional PSPs to those in the following example. You might have additional PSP from third party applications and require updates to the applications or working with the application vendors to determine the proper upgrade strategy to use for those applications.
{: important}

1. List your pod security policies.

    ```sh
    kubectl get podsecuritypolicies -o name
    ```
    {: pre}
    
1. Review the command output.
    
    ```sh
    Warning: policy/v1beta1 PodSecurityPolicy is deprecated in v1.21+, unavailable in v1.25+
    podsecuritypolicy.policy/ibm-anyuid-hostaccess-psp
    podsecuritypolicy.policy/ibm-anyuid-hostpath-psp
    podsecuritypolicy.policy/ibm-anyuid-psp
    podsecuritypolicy.policy/ibm-privileged-psp
    podsecuritypolicy.policy/ibm-restricted-psp
    ```
    {: screen}

1. Update your apps to use the IBM PSPs.


## Migration steps
{: #psa-migration-steps}

If you determine that your cluster pod security configuration does not meet the [migration pre-requisites](#psa-upgrade-reqs), you must follow these migration steps to upgrade your cluster.

Several of the following Pod Security migration steps include links to sections in the Kubernetes documentation. Note that **not all steps included in the external Kubernetes documentation are relevant to {{site.data.keyword.openshiftlong_notm}} clusters.** Follow only the steps that are directly linked from this page. Do not follow the external Kubernetes migration guide in its entirety, as some actions are not appropriate for {{site.data.keyword.openshiftlong_notm}} clusters. Read the following steps carefully to ensure that you take the correct migration actions for your cluster.
{: important}

### Step 1: Enable Pod Security admission in your 1.24 cluster
{: #psa-migration-enable-124}

Enable Pod Security admission in your 1.24 cluster. This command updates the cluster master to use the new Pod Security admission configuration. It may take a few minutes for the cluster master to update.

```sh
ibmcloud oc cluster master pod-security set --cluster <CLUSTER>
```
{: pre}

### Step 2: Review namespace permissions
{: #psa-migration-namespace-perm}

Review the namespace permissions in the external Kubernetes documentation. If your Kubernetes permissions are managed by IAM service roles, the `Manager` service role is required to create or edit namespaces and to set pod security labels.

- [Review namespace permissions](https://kubernetes.io/docs/tasks/configure-pod-container/migrate-from-psp/#review-namespace-permissions){: external}
  
### Step 3: Simplify and standardize PSPs
{: #psa-migration-simplify}

Clean up your Pod Security configuration by following the steps in the external Kubernetes documentation. Do **not** modify or delete any of the following PSPs: `ibm-privileged-psp`, `ibm-anyuid-psp`, `ibm-anyuid-hostpath-psp`, `ibm-anyuid-hostaccess-psp` and `ibm-restricted-psp`.

- [Simplify & standardize PodSecurityPolicies](https://kubernetes.io/docs/tasks/configure-pod-container/migrate-from-psp/#simplify-psps){: external}

### Step 4: Update the namespaces in your cluster
{: #psa-migration-update-namespace}

Update the namespaces in your cluster by following the steps in the external Kubernetes documentation. These steps must be performed on every namespace in the cluster that is not managed by {{site.data.keyword.cloud_notm}}. Note the exceptions included in this section.

Do not delete or modify the Pod Security labels for the following namespaces that are managed by {{site.data.keyword.cloud_notm}}: `kube-system`, `ibm-system`, `ibm-operators`.
{: important}

In step **3.d. Bypass PodSecurity Policy** of the external documentation linked in this step, do not create the suggested privileged PSP. If you create this additional PSP, it must be deleted before you upgrade to version 1.25, as detailed in the [upgrade requirements](#psa-upgrade-reqs). Instead, use the following command to create a `RoleBinding` to the `ibm-privileged-psp-user` cluster role: `kubectl create -n $NAMESPACE rolebinding disable-psp --clusterrole ibm-privileged-psp-user --group system:serviceaccounts:$NAMESPACE`. 
{: important}

- [Update namespaces](https://kubernetes.io/docs/tasks/configure-pod-container/migrate-from-psp/#update-namespaces){: external}

### Step 5: Review the namespace creation process
{: #psa-migration-namespace-creation}

Review the information in the external Kubernetes documentation to ensure that the Pod Security profile is applied to any new namespaces that are created in your cluster.

- [Review namespace creation processes](https://kubernetes.io/docs/tasks/configure-pod-container/migrate-from-psp/#review-namespace-creation-process){: external}


### Step 6: Optional. Disable the PSP feature in the cluster
{: #psa-migration-disable-psp}

1. Disable the `PodSecurityPolicy` admission controller in the cluster. This command updates the cluster master to use the new configuration. 
    ```sh
    ibmcloud oc cluster master pod-security policy disable --cluster <cluster>
    ```
    {: pre}

2. Wait a few minutes for the cluster master update to complete.
3. Delete your PSPs and any associated `Roles`, `ClusterRoles`, `RoleBindings`, and `ClusterRoleBindings`. Make sure that the components you delete do not grant any other unrelated permissions that you might need elsewhere. Do **not** delete the following PSPs: `ibm-privileged-psp`, `ibm-anyuid-psp`, `ibm-anyuid-hostpath-psp`, `ibm-anyuid-hostaccess-psp` and `ibm-restricted-psp`. Do **not** delete the following `ClusterRoles` and `ClusterRoleBindings`: `privileged-psp-user` and `restricted-psp-user`.

If you need to re-enable PSPs in your 1.24 cluster, run `ibmcloud oc cluster master pod-security policy enable --cluster <cluster>`. This command updates the cluster master to use the PSP configuration.
{: tip}

### Step 7: Optional. Upgrade your cluster
{: #psa-migration-cluster-upgrade}

[Upgrade your cluster to version 1.25](/docs/containers?topic=containers-cs_versions_125&interface=ui) to use Pod Security admission. Or, keep your cluster at version 1.24 with Pod Security admission enabled until you are ready to upgrade. 


## References
{: #psa-migration-references}

Review the following information before you migrate from Pod Security Policies to Pod Security Admission. Do **not** follow the migration guide as-is as some actions are not appropriate for {{site.data.keyword.openshiftlong_notm}} clusters.

- [Pod Security Admission](/docs/openshift?topic=openshift-pod-security-admission)

- [Migrate from `PodSecurityPolicy` to the Built-In PodSecurity Admission Controller](https://kubernetes.io/docs/tasks/configure-pod-container/migrate-from-psp/){: external}

- [PSP to PSA tool](https://github.com/kubernetes-sigs/pspmigrator){: external}

- [Why does my cluster upgrade fail due to Pod Security upgrade prerequisites?](/docs/containers?topic=containers-ts-app-pod-security).


