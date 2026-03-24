---

copyright:
  years: 2025, 2026
lastupdated: "2026-03-24"


keywords: key protect, hpcs, kp, migrate, cos, encryption

subcollection: openshift

---


{{site.data.keyword.attribute-definition-list}}


# Migrating from Hyper Protect Crypto Services to Key Protect for COS
{: #migrate_hpcs_kp_cos}

Migrate your Hyper Protect Crypto Services (HPCS) encryption for the {{site.data.keyword.cos_full_notm}} s3fs plugin to use Key Protect (KP) instead. 
{: shortdesc}

## Before you begin
{: #before}

Before you begin, follow these steps to determine if you need to migrate your COS plugin to use Key Protect instead of HPCS. 

1. Get the CRN of your HPCS and KP instances. Run the following command for each instance.

    ```sh
    ibmcloud resource service-instance <instance-name>
    ```
    {: pre}

    Example output.

    ```sh
    Name:  my-hpcs-instance
    ID:    crn:v1:bluemix:public:kms:us-south:a/1ab234cd5e678fgh9a0123bc4de567:f89gh01a-bcd2-3456-e789-f0g1234h5ab6::
    ```
    {: pre}

1. List all secrets in your cluster that are the `ibm/ibmc-s3fs` type.

    ```sh
    kubectl get secrets --field-selector type=ibm/ibmc-s3fs
    ```
    {: pre}

2. For each `ibm/ibmc-s3fs` secret, [review the secret contents](https://kubernetes.io/docs/tasks/configmap-secret/managing-secret-using-kubectl/#decoding-secret){: external} and find the `kp-root-key-crn` root key in the `data` section. Note any secret with a `kp-root-key-crn` value that includes the string `hs-crypto`, which indicates that it is an HPCS root key and must be migrated. Save this list of secrets to migrate. If there are no `kp-root-key-crn` values that contain `hs-crypto`, then you do not need to follow the migration steps. 

## Prerequisites for migration
{: #pre}

Complete these steps before you begin.

1. If you have a COS helm chart installed on your cluster, ensure that it [runs the latest version](https://helm.sh/docs/helm/helm_upgrade/){: external}. 
2. If you do not already have one, make a new Key Protect instance and a new set of Key Protect keys for encryption. Make sure your Key Protect instance is created in the same region as your cluster. This is required for the Key Protect instance to access your COS resources. 
3. [Create a service-to-service authorization](/docs/account?topic=account-serviceauth&interface=ui#create-auth) for Key Protect to access your COS resources. Set the **source** service as Key Protect and the **target** service as COS, and set the access level to at least **Reader**. 

## Migration steps
{: #steps}

Follow these steps to migrate your COS plugin to Key Protect.

If all of your COS secrets and PVCs are in a specific namespace, you can scope the following steps to that namespace. Otherwise, search through all namesapces on your cluster.
{: tip}


### Step 1. List PVCs to migrate
{: #pvc}
{: step}

Determine which PVCs must be migrated.

1. List all PVCs on your cluster or in the relevant namespace. 
    ```sh
    oc get pvc [-n <namespace>]
    ```
    {: pre}

2. Describe each PVC. 
    ```sh
    oc describe pvc <pvc-name>
    ```
    {: pre}

3. In the PVC output, find the **Annotations** section and check if the `volume.kubernetes.io/storage-provisioner: ibm.io/ibmc-s3fs` is listed. 
4. If the annotation is listed, look for the `ibm.io/secret-name` annotation.
5. If the `volume.kubernetes.io/storage-provisioner: ibm.io/ibmc-s3fs` annotation is listed **and** the `ibm.io/secret-name` value matches any of the secrets you found to have an HPCS root key, the PVC must be migrated. Note the PVC name. 
6. Repeat these steps for each PVC. Save the list of PVCs to migrate. 


### Step 2. List pods to migrate
{: #pods}

Determine which pods must be migrated. 

1. List all pods on your cluster or in the relevant namespace. 
    ```sh
    oc get pods [-n <namespace>]
    ```
    {: pre}

2. Describe each pod. 
    ```sh
    oc describe pod <pod-name>
    ```
    {: pre}

3. In the output, find the **Volumes** section and check the name of each **PersistentVolumeClaim**. If any of the PVCs in the output are also included in the list of PVCs to migrate, then the pod must be migrated. Note the name of the pod. 
4. Repeat these steps for each pod. Save the list of pods to migrate. 

### Step 3. Create new secrets
{: #secrets-new}

Create new secrets that use the Key Protect root key instead of the HPCS root key. 

1. Get the CRN of your Key Protect instance and encode it to base64.
    ```sh
    ibmcloud resource service-instance <kp-instance-name>
    ```
    {: pre}

    ```sh
    echo  -n "<root_key_CRN>" | base64
    ```
    {: pre}

2. For each secret that you must migrate, get the secret yaml.
    ```sh
    oc get secret <secret-name> -o yaml
    ```
    {: pre}

3. Copy the yaml into a file to create a new secret. Change the `kp-root-key-crn` to instead point to the base64 encoded CRN of the Key Protect instance. Append a string to the end of the secret name to help differentiate the new secret from the old one.

    When you recreate your PVCs, you must specify the new copy of the secret used by the PVC. Make sure the name of the new secret corresponds to the old secret, but still allows you to differentiate between the two.
    {: important}

4. Apply the secret.
    ```sh
    kubectl apply -f <secret-file-name>
    ```
    {: pre}

5. Repeat these steps for each secret that needs to be migrated.

### Step 4. Recreate PVCs
{: #pvcs-new}

Recreate your PVCs so they point to the new secrets.

1. For each PVC that you must migrate, get the PVC yaml. 
    ```sh
    oc get PVC <pvc-name> -o yaml
    ```
    {: pre}

2. Copy the yaml into a file to create a new PVC. Change the `ibm.io/secret-name` and `ibm.io/secret-namespace` annotations to point to the new secret that corresponds to the secret previously listed. Append a string to the end of the PVC name to help differentiate it from the old PVC. 

3. Apply the new PVC. 
    ```sh
    oc apply -f <pvc-file-name>
    ```
    {: pre}

4. Get the details of the PVC and verify that it is in the **Bound** state. 
    ```sh
    oc get PVC <pvc>
    ```
    {: pre}

5. Repeat these steps for each PVC that needs to be migrated. 

### Step 5. Update pods 
{: #pods-new}

Update the pods so they point to the new PVCs.

1. Determine the type of resource that was used. In the output, find the **ownerReferences** section and note the **kind** of resource and the **name** of the resource listed.
    ```sh
    oc describe pod <pod-name>
    ```
    {: pre}

2. Follow the update strategies based on the resource listed in the **ownerReferences** section. 
    - `DaemonSet`: [Rolling update on a DaemonSet](https://kubernetes.io/docs/tasks/manage-daemon/update-daemon-set/){: external}
    - `Deployment`: [Updating a Deployment](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/#updating-a-deployment){: external}
    - `StatefulSet`: [Update strategies for StatefulSets](https://kubernetes.io/docs/concepts/workloads/controllers/statefulset/#update-strategies){: external}
    - No resource listed: If no resource is listed, the pod is a stand-alone pod and must be recreated manually with the new PVC name. Follow the steps in [Manually recreating the pod](#pods-manual).


#### Manually recreating the pod
{: #pods-manual}

1. Get the pod yaml. 
    ```sh
    oc describe <resource-type> <resource-name> -o yaml
    ```
    {: pre}

2. Copy the yaml into a file to create a new pod. In the **volumes** section of the yaml, change the **PersistentVolumeClaim** to point to the new PVC that corresponds to the PVC previously listed. Append a string to the end of the new resource name to help differentiate it from the old resource.

3. Apply the new yaml file. 
    ```sh
    oc apply -f <pod-yaml-file>
    ```
    {: pre}

4. Verify that the pod is running. 
    ```sh
    oc get pods
    ```
    {: pre}

5. Repeat these steps for each pod that needs to be manually migrated. 
