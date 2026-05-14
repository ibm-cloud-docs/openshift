---

copyright: 
  years: 2014, 2026
lastupdated: "2026-05-14"


keywords: openshift

subcollection: openshift

content-type: troubleshoot

---


{{site.data.keyword.attribute-definition-list}}





# Why does PVC or pod creation fail due to not finding the Kubernetes secret?
{: #cos_secret_access_fails}
{: support}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf}

PVC or pod creation fails because the Kubernetes secret for {{site.data.keyword.cos_full_notm}} is not found or incorrectly referenced.
{: shortdesc}

When you create your PVC or deploy a pod that mounts the PVC, the creation or deployment fails.
{: tsSymptoms}

Example error message for a PVC creation failure:

```sh
can't get credentials: can't get secret tsecret-key: secrets "secret-key" not found
```
{: screen}

Example error message for a pod creation failure:

```sh
persistentvolumeclaim "pvc-3" not found (repeated 3 times)
```
{: screen}


The Kubernetes secret that you created is not referenced correctly in your deployment YAML file or is not set to the `ibm/ibmc-s3fs` type.
{: tsCauses}

## Resolving the issue
{: #cos-secret-resolve}

This task requires the [**Writer** or **Manager** {{site.data.keyword.cloud_notm}} IAM service access role](/docs/openshift?topic=openshift-iam-platform-access-roles) for all projects.
{: tsResolve}

1. List the secrets in your cluster and review the secret type. The secret must show `ibm/ibmc-s3fs` as the **Type**.

    ```sh
    oc get secrets --all-namespaces
    ```
    {: pre}

2. If your secret does not show `ibm/ibmc-s3fs` as the **Type**, [re-create your secret](/docs/openshift?topic=openshift-storage-cos-understand#create_cos_secret).

3. Check your YAML configuration file for your PVC and pod to verify that you used the correct secret name.

4. Verify that the secret exists in the same namespace as your PVC or pod.

    ```sh
    oc get secret <secret_name> -n <namespace>
    ```
    {: pre}

5. After correcting the secret reference, redeploy your PVC or pod and verify it mounts successfully.

    ```sh
    oc get pvc
    oc get pods
    ```
    {: pre}
