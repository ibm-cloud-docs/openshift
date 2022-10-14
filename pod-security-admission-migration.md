---

copyright: 
  years: 2022, 2022
lastupdated: "2022-10-13"

keywords: openshift, deploy, migrating psps to pod security, pod security admission, migrate to pod security admission

subcollection: openshift

content-type: tutorial
services: openshift
account-plan: paid
completion-time: 60m

---

{{site.data.keyword.attribute-definition-list}}

# Migrating from PSPs to Pod Security Admission
{: #pod-security-admission-migration}
{: toc-content-type="tutorial"}
{: toc-services="openshift"}
{: toc-completion-time="60m"}


The initial release of Kubernetes version 1.25 on the {{site.data.keyword.openshiftlong_notm}} supports upgrading from version 1.24 for clusters that use our default `PodSecurityPolicy` configuration if the following requirements are met.
{: shortdesc}


- All pods run under the `ibm-privileged-psp` PSP.
- All service accounts and users are authorized to use the `ibm-privileged-psp` through the `privileged-psp-user` cluster role binding.
- All service accounts and users are authorized to use the `ibm-restricted-psp` through the `restricted-psp-user` cluster role binding.
- No `PodSecurityPolicies` are defined beyond those provided by the IBM Cloud Kubernetes Service: `ibm-privileged-psp`, `ibm-anyuid-psp`, `ibm-anyuid-hostpath-psp`, `ibm-anyuid-hostaccess-psp`, and `ibm-restricted-psp`.

These restrictions ensure that pods run properly under the default Pod Security Admission configuration provided in v1.25.

Note that these restrictions don't mean that all pods are privileged. Instead, the pods use a PSP that allows privileged pods. Nor do these restrictions preclude the use of third party security policy admission controllers as long as the controllers work properly within this PSP configuration.

If you created your own PSPs or changed these cluster role bindings to restrict use of the `ibm-privileged-psp`, you cannot upgrade to v1.25 at this time.

Complete the following steps to confirm that the cluster PSP configuration satisfies the requirements for upgrading to Pod Security.

## Checking for non-IBM PSPs
{: #psa-migration-check-psp}
{: step}

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


## Checking for pods not using `ibm-privileged-psp`
{: #psa-migration-pod-check}
{: step}

Complete the following steps to find any pods that are using PSPs other than `ibm-privileged-psp`.

One difference between Pod Security Admission and `PodSecurityPolicies` is that Pod Security Admission is validating while the `PodSecurityPolicies` can be mutating.  This makes it important that pods use the `ibm-privileged-psp`, which is not a mutating PSP, before you upgrade. Because both Pod Security Admission and the `ibm-privileged-psp` are validating, pods work the same under either one.

For example, if a pod is currently running under `ibm-restricted-psp`, it might set the `fsGroup` and `supplementalGroups` to `1` in the pod `securityContext` section, based on the `MustRunAs` range in the PSP. In other words, the `ibm-restricted-psp` can change the pod `securityContext`. Such changes are visible as a difference between the securityContext of the running pod and the securityContext in the pod template of the deployment or similar resource that creates the pod. The `ibm-privileged-psp` is not mutating, so a pod running under it might run with different groups and might not be able to access data stored in an existing PVC.

1. Get the details of all pods and check their PSPs.

    ```sh
    kubectl get pods -A -o jsonpath="{.items[*].metadata.annotations.kubernetes\.io\/psp}" | tr " " "\n" | sort -u
    ```
    {: pre}
    
1. Review the command output for any PSPs that are not `ibm-privileged-psp`. If your pods are using a different PSP, you must update your application to use the `ibm-privileged-psp` before upgraing your cluster. If no other PSPs are listed, you can continue with the upgrade.

Upgrading to 1.25 is not recommended if the output lists a PSP other than the `ibm-privileged-psp` PSP.
{: important}


### Verifying the `privileged-psp-user` cluster role binding is using default configuration
{: #psa-migration-verify-crb}
{: step}

Complete the following steps to verify the `privileged-psp-user` cluster role binding is using default configuration.

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


### Verifying the `restricted-psp-user` ClusterRoleBinding is using default configuration
{: psa-migration-crb-verify}
{: step}

Complete the following steps the verify the `restricted-psp-user` ClusterRoleBinding is using the default configuration.

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


### References
{: psa-migration-references}

Review the following information before you migrate from Pod Security Policies to Pod Security Admission. Do **not** follow the migration guide as-is as some actions are not appropriate for {{site.data.keyword.openshiftlong_notm}} clusters.

- [Migrate from `PodSecurityPolicy` to the Built-In PodSecurity Admission Controller](https://kubernetes.io/docs/tasks/configure-pod-container/migrate-from-psp/){: external}

- [PSP to PSA tool](https://github.com/kubernetes-sigs/pspmigrator){: external}


