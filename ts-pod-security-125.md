---

copyright: 
  years: 2022, 2022
lastupdated: "2022-10-13"

keywords: openshift, help, cluster master operations error, CAE009

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}



# Why does my cluster upgrade fail due to Pod Security upgrade prerequisites?
{: #ts-app-pod-security}
{: support}


When you upgrade your {{site.data.keyword.openshiftlong_notm}} from Kubernetes version 1.24 to version 1.25, the upgrade fails and you see an error message similar to the following example.
{: Symptoms}

```sh
Version update cancelled. CAE009: Cannot complete cluster master operations because the cluster does not pass Pod Security upgrade prerequisites. Reason: [ClusterRoleBinding 'restricted-psp-user' does not have expected subjects]. For more information, see the troubleshooting docs: 'https://ibm.biz/master_pod_security_upgrade_iks_125'
```
{: screen}


The Kubernetes `PodSecurityPolicy` admission controller was removed in Kubernetes 1.25 and replaced with a new Pod Security Admission controller.
{: tsCauses}

To safely upgrade a {{site.data.keyword.openshiftlong_notm}} cluster from version 1.24 to version 1.25, the cluster `PodSecurityPolicies` (PSP) and associated role-based access control must satisfy the following prerequisites.

- No PSPs beyond the 5 {{site.data.keyword.cloud_notm}} defined PSPs can exist.
- The {{site.data.keyword.cloud_notm}} defined cluster role bindings that give all users and service accounts authority to use the {{site.data.keyword.cloud_notm}} defined privileged and restricted PSPs must exist.

These prerequisites ensure that the cluster's version 1.24 `PodSecurityPolicy` configuration is equivalent to version 1.25 Pod Security Admission configuration and the upgrade and switch to Pod Security Admission does not break existing applications. Note these prerequisite do not preclude use of third party pod security providers.


Before you begin

- Review the [1.25 version information and update actions](/docs/containers?topic=containers-cs_versions_125).
- Review the [Migrating from PSPs to Pod Security Admission](/docs/containers?topic=containers-pod-security-admission-migration) guide.


If you are not ready to migrate to Pod Security Admission, you can clear the status message by performing a cluster master refresh. 
{: tip}

If you already performed the Pod Security Admission upgrade prerequisite actions, the error message indicates an action that you might have missed or an unexpected change to {{site.data.keyword.openshiftlong_notm}} defined resources that you need to address. Complete the following steps based on the message you are seeing.
{: tsResolve}


## Could not get `PodSecurityPolicies`
{: #could-not-get-psps}

1. Run the following to command to get your PSPs.
    ```sh
    kubectl get podsecuritypolicies
    ```
    {: pre}

1. If there is no error, try again to upgrade the cluster master.

## Found non-IBM `PodSecurityPolicy`
{: #non-ibm-psp}

There are additional PSPs that need to be removed.

Before you upgrade your cluster to version 1.25, verify that only the following PSPs exist.

- `ibm-privileged-psp`
- `ibm-anyuid-psp`
- `ibm-anyuid-hostpath-psp`
- `ibm-anyuid-hostaccess-psp`
- `ibm-restricted-psp`


1. List your PSPs.

    ```sh
    kubectl get podsecuritypolicies
    ```
    {: pre}

1. If the additional PodSecurityPolicy is no longer in use, delete it. If there are additional pod security policies, [review the migration guide](/docs/containers?topic=containers-pod-security-admission-migration).

    ```sh
    kubectl delete podsecuritypolicies PSP
    ```
    {: pre}

1. Retry the cluster upgrade.

## Could not get ClusterRoleBinding privileged-psp-user
{: #psp-user-not-get}

This message indicates the `privileged-psp-user` cluster role binding does not exist or that some other error prevented the upgrade operation from reading the resource.

1. List the resource.
    ```sh
    kubectl get clusterrolebindings privileged-psp-user
    ```
    {: pre}

1. If you get a `NotFound` error, create or update the `privileged-psp-user` [cluster role binding](#create-privileged-psp-user).

## ClusterRoleBinding `privileged-psp-user` does not have expected roleRef
{: #unexpected-role-ref}

This error indicates an unexpected change and that the cluster role binding is referencing the wrong cluster role.

1. Delete the cluster role binding.

    ```sh
    kubectl delete clusterrolebinding privileged-psp-user
    ```
    {: pre}

1. Create the `privileged-psp-user` [cluster role binding](#create-privileged-psp-user).

## ClusterRoleBinding privileged-psp-user does not have expected subjects
{: #psp-privilieged-unexpected-subjects}

If this change was intentional, you must first determine whether your apps can run with the [cluster role binding](#create-privileged-psp-user). If they can, Create or update restricted-psp-user [cluster role binding](#create-restricted-psp-user).


## Could not get ClusterRoleBinding `restricted-psp-user`
{: #psp-restrictred-user-missing}

This message indicates the `restricted-psp-user` cluster role binding does not exist or some other error prevented the upgrade operation from reading the resource.

1. Get the details of the `restricted-psp-user` cluster role binding.
    ```sh
    kubectl get clusterrolebindings restricted-psp-user
    ```
    {: pre}

1. If you get a `NotFound` error, create or update restricted-psp-user [cluster role binding](#create-restricted-psp-user).

## ClusterRoleBinding `restricted-psp-user` does not have expected roleRef
{: #psp-restricted-role-ref}

This error indicates is an unexpected change and that the cluster role binding is referencing the wrong cluster role.

Complete the following steps to change the `roleRef`.

1. Delete the cluster role binding.
    ```sh
    kubectl delete clusterrolebinding restricted-psp-user
    ```
    {: pre}

1. Create or update restricted-psp-user [cluster role binding](#create-restricted-psp-user).

## ClusterRoleBinding restricted-psp-user does not have expected subjects
{: #psp-restricted-subjects}

If this change was intentional, you must first determine if applications can run properly with the [cluster role binding](#create-restricted-psp-user).

Then, create or update restricted-psp-user [cluster role binding](#create-restricted-psp-user).

## Creating or updating the `privileged-psp-user` ClusterRoleBinding
{: #create-privileged-psp-user}

Create or update `privileged-psp-user` cluster role binding by running the following command.

```sh
kubectl apply -f - <<EOF
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: privileged-psp-user
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
EOF
```
{: codeblock}

## Creating the `restricted-psp-user` cluster role binding
{: #create-restricted-psp-user}

Create or update the `restricted-psp-user` ClusterRoleBinding by running the following command.

```sh
kubectl apply -f - <<EOF
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: restricted-psp-user
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
EOF
```
{: codeblock}



