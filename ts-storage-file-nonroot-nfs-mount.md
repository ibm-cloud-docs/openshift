---

copyright: 
  years: 2014, 2022
lastupdated: "2022-03-16"

keywords: openshift

subcollection: openshift

content-type: troubleshoot

---


{{site.data.keyword.attribute-definition-list}}


# Why does my app fail when a non-root user owns the NFS file storage mount path?
{: #nonroot}
{: support}

**Infrastructure provider**: ![Classic infrastructure provider icon.](images/icon-classic-2.svg) Classic


After you [add NFS storage](/docs/openshift?topic=openshift-file_storage#file_app_volume_mount) to your deployment, the deployment of your container fails. When you retrieve the logs for your container, you might see errors such as the following. The pod fails and is stuck in a reload cycle.
{: tsSymptoms}

```sh
write-permission
```
{: screen}

```sh
don't have required permission
```
{: screen}

```sh
can't create directory '/bitnami/mariadb/data': Permission denied
```
{: screen}


By default, non-root users don't have write permission on the volume mount path for NFS-backed storage. Some common app images, such as Jenkins and Nexus3, specify a non-root user that owns the mount path in the Dockerfile.
{: tsCauses}

When you create a container from this Dockerfile, the creation of the container fails due to insufficient permissions of the non-root user on the mount path. To grant write permission, you can modify the Dockerfile to temporarily add the non-root user to the root user group before it changes the mount path permissions, or use an init container.

If you use a Helm chart to deploy the image, edit the Helm deployment to use an init container.
{: tip}




When you include an [init container](https://kubernetes.io/docs/concepts/workloads/pods/init-containers/){: external} in your deployment, you can give a non-root user that is specified in your Dockerfile write permissions for the volume mount path inside the container.
{: tsResolve}

The init container starts before your app container starts. The init container creates the volume mount path inside the container, changes the mount path to be owned by the correct (non-root) user, and closes. Then, your app container starts with the non-root user that must write to the mount path. Because the path is already owned by the non-root user, writing to the mount path is successful. If you don't want to use an init container, you can modify the Dockerfile to add non-root user access to NFS file storage.




**Before you begin**: 



* [Access your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-access_cluster).
* Pick a [security context constraint (SCC)](/docs/openshift?topic=openshift-openshift_scc) that lets your deployment perform `chown` operations.

**To use an init container to give a non-root user write permissions to the volume mount path**:

1. Open the Dockerfile for your app and get the user ID (UID) and group ID (GID) from the user that you want to give writer permission on the volume mount path. In the example from a Jenkins Dockerfile, the information is:
    - UID: `1000`
    - GID: `1000`

    **Example**:

    ```yaml
    FROM openjdk:8-jdk

    RUN apt-get update && apt-get install -y git curl && rm -rf /var/lib/apt/lists/*

    ARG user=jenkins
    ARG group=jenkins
    ARG uid=1000
    ARG gid=1000
    ARG http_port=8080
    ARG agent_port=50000

    ENV JENKINS_HOME /var/jenkins_home
    ENV JENKINS_SLAVE_AGENT_PORT ${agent_port}
    ...
    ```
    {: screen}

2. Add persistent storage to your app by creating a persistent volume claim (PVC). This example uses the `ibmc-file-bronze` storage class. To review available storage classes, run `oc get storageclasses`.

    ```yaml
    apiVersion: v1
    kind: PersistentVolumeClaim
    metadata:
      name: mypvc
      annotations:
        volume.beta.kubernetes.io/storage-class: "ibmc-file-bronze"
    spec:
      accessModes:
        - ReadWriteMany
      resources:
        requests:
          storage: 20Gi
    ```
    {: codeblock}

3. Create the PVC.

    ```sh
    oc apply -f mypvc.yaml
    ```
    {: pre}

4. In your deployment `.yaml` file, add the init container. Include the UID and GID that you previously retrieved.

    ```yaml
    initContainers:
    - name: initcontainer # Or replace the name
      image: alpine:latest
      command: ["/bin/sh", "-c"]
      args:
        - chown <UID>:<GID> /mount; # Replace UID and GID with values from the Dockerfile
      volumeMounts:
      - name: volume # Or you can replace with any name
        mountPath: /mount # Must match the mount path in the args line
    ```
    {: codeblock}

    Review the following example Jenkins deployment.

    ```yaml
    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: my-pod
    spec:
      replicas: 1
      selector:
        matchLabels:
          app: jenkins      
      template:
        metadata:
          labels:
            app: jenkins
        spec:
          containers:
          - name: jenkins
            image: jenkins
            volumeMounts:
            - mountPath: /var/jenkins_home
              name: volume
          volumes:
          - name: volume
            persistentVolumeClaim:
              claimName: mypvc
          initContainers:
          - name: permissionsfix
            image: alpine:latest
            command: ["/bin/sh", "-c"]
            args:
              - chown 1000:1000 /mount;
            volumeMounts:
            - name: volume
              mountPath: /mount
    ```
    {: codeblock}

5. Create the pod and mount the PVC to your pod.

    ```sh
    oc apply -f my-pod.yaml
    ```
    {: pre}

    Is the init container failing? Because {{site.data.keyword.redhat_openshift_notm}} sets restricted security context constraints, you might see an error such as `chown: /opt/ibm-ucd/server/ext_lib: Operation not permitted`. For your deployment, [use an SCC](/docs/openshift?topic=openshift-openshift_scc) that allows `chown` operations and try again.
    {: note}

6. Verify that the volume is successfully mounted to your pod. Note the pod name and **Containers/Mounts** path.

    ```sh
    oc describe pod <my-pod>
    ```
    {: pre}

    Example output

    ```shyaml
    Name:       mypod-123456789
    Namespace:    default
    ...
    Init Containers:
    ...
    Mounts:
        /mount from volume (rw)
        /var/run/secrets/kubernetes.io/serviceaccount from default-token-cp9f0 (ro)
    ...
    Containers:
        jenkins:
        Container ID:
        Image:        jenkins
        Image ID:
        Port:          <none>
        State:        Waiting
            Reason:        PodInitializing
        Ready:        False
        Restart Count:    0
        Environment:    <none>
        Mounts:
            /var/jenkins_home from volume (rw)
            /var/run/secrets/kubernetes.io/serviceaccount from default-token-cp9f0 (ro)
    ...
    Volumes:
        myvol:
        Type:    PersistentVolumeClaim (a reference to a PersistentVolumeClaim in the same namespace)
        ClaimName:    mypvc
        ReadOnly:      false

    ```
    {: screen}

7. Log in to the pod by using the pod name that you previously noted.
    ```sh
    oc exec -it <my-pod-123456789> /bin/bash
    ```
    {: pre}

8. Verify the permissions of your container's mount path. In the example, the mount path is `/var/jenkins_home`.

    ```sh
    ls -ln /var/jenkins_home
    ```
    {: pre}

    Example output
    
    ```sh
    jenkins@mypod-123456789:/$ ls -ln /var/jenkins_home
    total 12
    -rw-r--r-- 1 1000 1000  102 Mar  9 19:58 copy_reference_file.log
    drwxr-xr-x 2 1000 1000 4096 Mar  9 19:58 init.groovy.d
    drwxr-xr-x 9 1000 1000 4096 Mar  9 20:16 war
    ```
    {: screen}

    This output shows that the GID and UID from your Dockerfile (in this example, `1000` and `1000`) own the mount path inside the container.








