---

copyright:
  years: 2014, 2021
lastupdated: "2021-06-02"

keywords: openshift, roks, rhoks, rhos

subcollection: openshift
content-type: troubleshoot

---

{:DomainName: data-hd-keyref="APPDomain"}
{:DomainName: data-hd-keyref="DomainName"}
{:android: data-hd-operatingsystem="android"}
{:api: .ph data-hd-interface='api'}
{:apikey: data-credential-placeholder='apikey'}
{:app_key: data-hd-keyref="app_key"}
{:app_name: data-hd-keyref="app_name"}
{:app_secret: data-hd-keyref="app_secret"}
{:app_url: data-hd-keyref="app_url"}
{:authenticated-content: .authenticated-content}
{:beta: .beta}
{:c#: data-hd-programlang="c#"}
{:cli: .ph data-hd-interface='cli'}
{:codeblock: .codeblock}
{:curl: .ph data-hd-programlang='curl'}
{:deprecated: .deprecated}
{:dotnet-standard: .ph data-hd-programlang='dotnet-standard'}
{:download: .download}
{:external: target="_blank" .external}
{:faq: data-hd-content-type='faq'}
{:fuzzybunny: .ph data-hd-programlang='fuzzybunny'}
{:generic: data-hd-operatingsystem="generic"}
{:generic: data-hd-programlang="generic"}
{:gif: data-image-type='gif'}
{:go: .ph data-hd-programlang='go'}
{:help: data-hd-content-type='help'}
{:hide-dashboard: .hide-dashboard}
{:hide-in-docs: .hide-in-docs}
{:important: .important}
{:ios: data-hd-operatingsystem="ios"}
{:java: .ph data-hd-programlang='java'}
{:java: data-hd-programlang="java"}
{:javascript: .ph data-hd-programlang='javascript'}
{:javascript: data-hd-programlang="javascript"}
{:new_window: target="_blank"}
{:note .note}
{:note: .note}
{:objectc data-hd-programlang="objectc"}
{:org_name: data-hd-keyref="org_name"}
{:php: data-hd-programlang="php"}
{:pre: .pre}
{:preview: .preview}
{:python: .ph data-hd-programlang='python'}
{:python: data-hd-programlang="python"}
{:route: data-hd-keyref="route"}
{:row-headers: .row-headers}
{:ruby: .ph data-hd-programlang='ruby'}
{:ruby: data-hd-programlang="ruby"}
{:runtime: architecture="runtime"}
{:runtimeIcon: .runtimeIcon}
{:runtimeIconList: .runtimeIconList}
{:runtimeLink: .runtimeLink}
{:runtimeTitle: .runtimeTitle}
{:screen: .screen}
{:script: data-hd-video='script'}
{:service: architecture="service"}
{:service_instance_name: data-hd-keyref="service_instance_name"}
{:service_name: data-hd-keyref="service_name"}
{:shortdesc: .shortdesc}
{:space_name: data-hd-keyref="space_name"}
{:step: data-tutorial-type='step'}
{:subsection: outputclass="subsection"}
{:support: data-reuse='support'}
{:swift: .ph data-hd-programlang='swift'}
{:swift: data-hd-programlang="swift"}
{:table: .aria-labeledby="caption"}
{:term: .term}
{:terraform: .ph data-hd-interface='terraform'}
{:tip: .tip}
{:tooling-url: data-tooling-url-placeholder='tooling-url'}
{:troubleshoot: data-hd-content-type='troubleshoot'}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:tsSymptoms: .tsSymptoms}
{:tutorial: data-hd-content-type='tutorial'}
{:ui: .ph data-hd-interface='ui'}
{:unity: .ph data-hd-programlang='unity'}
{:url: data-credential-placeholder='url'}
{:user_ID: data-hd-keyref="user_ID"}
{:vbnet: .ph data-hd-programlang='vb.net'}
{:video: .video}
  
  
# File storage: Why can't I add non-root user access to persistent storage?
{: #cs_storage_nonroot}

**Infrastructure provider**: <img src="../images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Classic

{: tsSymptoms}
After you [add non-root user access to persistent storage](/docs/openshift?topic=openshift-nonroot) or deploy a Helm chart with a non-root user ID specified, the user cannot write to the mounted storage.

{: tsCauses}
Your app deployment or Helm chart configuration specifies the [security context](https://kubernetes.io/docs/tasks/configure-pod-container/security-context/) for the pod's `fsGroup` (group ID) and `runAsUser` (user ID). Generally, a pod's default security context sets [`runAsNonRoot`](https://kubernetes.io/docs/concepts/policy/pod-security-policy/#users-and-groups) so that the pod cannot run as the root user. Because the `fsGroup` setting is not designed for shared storage such as NFS file storage, the `fsGroup` setting is not supported, and the `runAsUser` setting is automatically set to `2020`. These default settings do not allow other non-root users to write to the mounted storage.

{: tsResolve}
To allow a non-root user read and write access to a file storage device, you must allocate a [supplemental group ID](https://kubernetes.io/docs/concepts/policy/pod-security-policy/#users-and-groups){: external} in a storage class, refer to this storage class in the PVC, and set the pod's security context with a `runAsUser` value that is automatically added to the supplemental group ID. When you grant the supplemental group ID read and write access to the file storage, any non-root user that belongs to the group ID, including your pod, is granted access to the file storage.

You can use one of the provided [`gid` storage classes](/docs/openshift?topic=openshift-file_storage#file_storageclass_reference) or create a custom storage class to define your own supplemental group ID.

Allocating a supplemental group ID for a non-root user of a file storage device is supported for single zone clusters only, and cannot be used in multizone clusters.
{: note}

1. Select one of the [provided `gid` storage classes](/docs/openshift?topic=openshift-file_storage#file_storageclass_reference) to assign the default group ID `65531` to your non-root user that you want to read and write to your file storage. If you want to assign a custom group ID, create a YAML file for a customized storage class. In your customized storage class YAML file, include the `gidAllocate: "true"` parameter and define the group ID in the `gidFixed` parameter.

   **Example storage classes for assigning the default group ID `65531`**:
   - `ibmc-file-bronze-gid`
   - `ibmc-file-silver-gid`
   - `ibmc-file-gold-gid`

   **Example customized storage class to specify a different group ID**:
   ```yaml
   apiVersion: storage.k8s.io/v1beta1
   kind: StorageClass
   metadata:
     name: ibmc-file-bronze-gid-custom
     labels:
       kubernetes.io/cluster-service: "true"
   provisioner: ibm.io/ibmc-file
   parameters:
     type: "Endurance"
     iopsPerGB: "2"
     sizeRange: "[1-12000]Gi"
     mountOptions: nfsvers=4.1,hard
     billingType: "hourly"
     reclaimPolicy: "Delete"
     classVersion: "2"
     gidAllocate: "true"
     gidFixed: "65165"
   ```
   {: codeblock}

   To create the storage class in your cluster, run `kubectl apply -f storageclass.yaml`.

3. Create a YAML file for your PVC that uses the storage class that you created.

   ```yaml
   kind: PersistentVolumeClaim
   apiVersion: v1
   metadata:
   name: gid-pvc
   labels:
     billingType: "monthly"
   spec:
   accessModes:
     - ReadWriteMany
   resources:
     requests:
       storage: 20Gi
   storageClassName: ibmc-file-bronze-gid
   ```
   {: codeblock}

4. Create the PVC in your cluster.
   ```sh
   kubectl apply -f pvc.yaml
   ```
   {: pre}

5. Wait a few minutes for the file storage to be provisioned and the PVC to change to a `Bound` status. Note that if you created the PVC in a multizone cluster, the PVC remains in a `pending` state.
   {: note}
   ```sh
   kubectl get pvc
   ```
   {: pre}

   **Example output**:
   ```sh
   NAME      STATUS   VOLUME                                     CAPACITY   ACCESS MODES   STORAGECLASS           AGE
   gid-pvc   Bound    pvc-5e4acab4-9b6f-4278-b53c-22e1d3ffa123   20Gi       RWX            ibmc-file-bronze-gid   2m54s
   ```
   {: screen}

6. Create a YAML file for your deployment that mounts the PVC that you created. In the `spec.template.spec.securityContext.runAsUser` field, specify the non-root user ID that you want to use. This user ID is automatically added to the supplemental group ID that is defined in the storage class to gain read and write access to the file storage.

   **Example for creating an `node-hello` deployment**:
   ```yaml
   apiVersion: apps/v1
   kind: Deployment
   metadata:
     name: gid-deployment
     labels:
       app: gid
   spec:
     selector:
       matchLabels:
         app: gid
     template:
       metadata:
         labels:
           app: gid
       spec:
         containers:
         - image: gcr.io/google-samples/node-hello:1.0
           name: gid-container
           volumeMounts:
           - name: gid-vol
             mountPath: /myvol
         securityContext:
           runAsUser: 2020
         volumes:
         - name: gid-vol
           persistentVolumeClaim:
             claimName: gid-pvc
   ```
   {: codeblock}

7. Create the deployment in your cluster.
   ```sh
   kubectl apply -f deployment.yaml
   ```
   {: pre}

8. Verify that your pod is in a **Running** status.
   ```sh
   kubectl get pods
   ```
   {: pre}

   **Example output**:
   ```sh
   NAME                              READY   STATUS    RESTARTS   AGE
   gid-deployment-5dc86db4c4-5hbts   2/2     Running   0          69s
   ```
   {: screen}

9. Log in to your pod.
    ```sh
    kubectl exec <pod_name> -it bash
    ```
    {: pre}

## Verifying the read and write permissions for the non-root user
{: #verify-rw-permissions}
1. List the user ID and group IDs for the current user inside the pod. The setup is correct if your non-root user ID is listed as `uid` and the supplemental group ID that you defined in your storage class is listed under `groups`.
  ```sh
  id
  ```
  {: pre}

  **Example output**:
  ```sh
  uid=2020 gid=0(root) groups=0(root), 65531
  ```
  {: screen}

2. List the permissions for your volume mount directory that you defined in your deployment. The setup is correct if the supplemental group ID that you defined in your storage class is listed with read and write permissions in your volume mount directory.
  ```sh
  ls -l /<volume_mount_path>
  ```
  {: pre}

  **Example output**:
  ```sh
  drwxrwxr-x 2 nobody 65531 4096 Dec 11 07:40 .
  drwxr-xr-x 1 root   root  4096 Dec 11 07:30 ..
  ```
  {: screen}

3. Create a file in your mount directory.
  ```sh
  echo "Able to write to file storage with my non-root user." > /myvol/gidtest.txt
  ```
  {: pre}

4. List the permissions for the files in your volume mount directory.
  ```sh
  ls -al /mnt/nfsvol/
  ```
  {: pre}

  **Example output**:
  ```sh
  drwxrwxr-x 2 nobody      65531 4096 Dec 11 07:40 .
  drwxr-xr-x 1 root        root  4096 Dec 11 07:30 ..
  -rw-r--r-- 1 2020   4294967294   42 Dec 11 07:40 gidtest.txt .
  ```
  {: screen}

  In your CLI output, the non-root user ID is listed with read and write access to the file that you created.

5. Exit your pod.
  ```sh
  exit
  ```
  {: pre}


If you need to change the ownership of the mount path from `nobody`, see [App fails when a non-root user owns the NFS file storage mount path](/docs/openshift?topic=openshift-nonroot).
{: tip}



