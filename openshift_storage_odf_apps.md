---

copyright:
  years: 2014, 2021
lastupdated: "2021-10-19"

keywords: openshift, openshift data foundation, openshift container storage, ocs, vpc, roks

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}

# Deploying an app on OpenShift Data Foundation
{: #odf-deploy-app}

After you install the OpenShift Data Foundation add-on for your {{site.data.keyword.openshiftlong}} cluster, you can use the ODF storage classes to create a persistent volume claim (PVC). Then, refer to the PVC in your deployment so that your app can save and use data from the underlying ODF storage device.
{: shortdesc}

**Minimum required permissions**: **Editor** platform access role and the **Writer** service access role for the cluster in {{site.data.keyword.containerlong_notm}}.

[Access your {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-access_cluster).

1. List the ODF storage classes. For more information about ODF storage classes, see the [Storage class reference](/docs/openshift?topic=openshift-ocs-sc-ref#ocs-sc-ref).
    ```sh
    oc get sc | grep openshift
    ```
    {: pre}

    **Example output**
    ```sh
    ocs-storagecluster-ceph-rbd                   openshift-storage.rbd.csi.ceph.com      Delete          Immediate              true                   14d
    ocs-storagecluster-ceph-rgw                   openshift-storage.ceph.rook.io/bucket   Delete          Immediate              false                  14d
    ocs-storagecluster-cephfs                     openshift-storage.cephfs.csi.ceph.com   Delete          Immediate              true                   14d
    openshift-storage.noobaa.io                   openshift-storage.noobaa.io/obc         Delete          Immediate              false                  14d
    ```
    {: screen}


1. Create a PVC that refers to the storage class that you want to use. Save and edit the following PVC configuration file to refer to the storage class that you want to use.
    **Example PVC for using the `ocs-storagecluster-cephfs` storage class.**
    ```yaml
    apiVersion: v1
    kind: PersistentVolumeClaim
    metadata:
      name: odf-pvc
    spec:
      accessModes:
      - ReadWriteOnce
      resources:
        requests:
          storage: 10Gi
      storageClassName: ocs-storagecluster-cephfs
    ```
    {: codeblock}

1. Create the PVC in your cluster.
    ```sh
    oc create -f <my-pvc.yaml>
    ```
    {: pre}

1. Create a YAML configuration file for a pod that mounts the PVC that you created. The following example creates an `nginx` pod that writes the current date and time to a `test.txt` file.
    ```yaml
    apiVersion: v1
    kind: Pod
    metadata:
      name: app
    spec:
      containers:
      - name: app
        image: nginx
        command: ["/bin/sh"]
        args: ["-c", "while true; do echo $(date -u) >> /test/test.txt; sleep 600; done"]
        volumeMounts:
        - name: persistent-storage
          mountPath: /test
      volumes:
      - name: persistent-storage
        persistentVolumeClaim:
          claimName: odf-pvc
    ```
    {: codeblock}

1. Create the pod in your cluster.
    ```sh
    oc apply -f pod.yaml
    ```
    {: pre}

1. To verify that the pod is deployed, wait for your app to get into a `Running` status.
    ```sh
    oc get pods
    ```
    {: pre}

    Example output

    ```sh
    NAME                                READY   STATUS    RESTARTS   AGE
    app                                 1/1     Running   0          2m58s
    ```
    {: screen}

1. Verify that the app can write data.
    1. Log in to your pod.
        ```sh
        oc exec <app-pod-name> -it bash
        ```
        {: pre}

    1. Display the contents of the `test.txt` file to confirm that your app can write data to your persistent storage.
        ```sh
        cat /test/test.txt
        ```
        {: pre}

        Example output
        ```sh
        Tue Mar 2 20:09:19 UTC 2021
        Tue Mar 2 20:09:25 UTC 2021
        Tue Mar 2 20:09:31 UTC 2021
        Tue Mar 2 20:09:36 UTC 2021
        Tue Mar 2 20:09:42 UTC 2021
        Tue Mar 2 20:09:47 UTC 2021
        ```
        {: screen}

    1. Exit the pod.
        ```sh
        exit
        ```
        {: pre}









