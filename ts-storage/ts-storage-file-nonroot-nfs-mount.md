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
  
  
# File storage: Why does my app fail when a non-root user owns the NFS file storage mount path?
{: #nonroot}

**Infrastructure provider**: <img src="../images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Classic

{: tsSymptoms}
After you [add NFS storage](/docs/openshift?topic=openshift-file_storage#file_app_volume_mount) to your deployment, the deployment of your container fails. When you retrieve the logs for your container, you might see errors such as the following. The pod fails and is stuck in a reload cycle.

```sh
write-permission
```
{: screen}

```sh
do not have required permission
```
{: screen}

```sh
cannot create directory '/bitnami/mariadb/data': Permission denied
```
{: screen}

{: tsCauses}
By default, non-root users do not have write permission on the volume mount path for NFS-backed storage. Some common app images, such as Jenkins and Nexus3, specify a non-root user that owns the mount path in the Dockerfile. When you create a container from this Dockerfile, the creation of the container fails due to insufficient permissions of the non-root user on the mount path. To grant write permission, you can modify the Dockerfile to temporarily add the non-root user to the root user group before it changes the mount path permissions, or use an init container.

If you use a Helm chart to deploy the image, edit the Helm deployment to use an init container.
{:tip}



{: tsResolve}
When you include an [init container](https://kubernetes.io/docs/concepts/workloads/pods/init-containers/){: external} in your deployment, you can give a non-root user that is specified in your Dockerfile write permissions for the volume mount path inside the container. The init container starts before your app container starts. The init container creates the volume mount path inside the container, changes the mount path to be owned by the correct (non-root) user, and closes. Then, your app container starts with the non-root user that must write to the mount path. Because the path is already owned by the non-root user, writing to the mount path is successful. If you do not want to use an init container, you can modify the Dockerfile to add non-root user access to NFS file storage.


**Before you begin**: 
* [Access your {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-access_cluster).
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
    {:screen}

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

3.  Create the PVC.

    ```sh
    oc apply -f mypvc.yaml
    ```
    {: pre}

4.  In your deployment `.yaml` file, add the init container. Include the UID and GID that you previously retrieved.

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

    **Example** for a Jenkins deployment:

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

5.  Create the pod and mount the PVC to your pod.
    ```sh
    oc apply -f my-pod.yaml
    ```
    {: pre}

    Is the init container failing? Because {{site.data.keyword.openshiftshort}} sets restricted security context constraints, you might see an error such as `chown: /opt/ibm-ucd/server/ext_lib: Operation not permitted`. For your deployment, [use an SCC](/docs/openshift?topic=openshift-openshift_scc) that allows `chown` operations and try again.
    {: note}

6. Verify that the volume is successfully mounted to your pod. Note the pod name and **Containers/Mounts** path.
   ```sh
   oc describe pod <my-pod>
   ```
   {: pre}

   **Example output**:
   ```yaml
   Name:       mypod-123456789
   Namespace:	default
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
       Image:		jenkins
       Image ID:
       Port:		  <none>
       State:		Waiting
         Reason:		PodInitializing
       Ready:		False
       Restart Count:	0
       Environment:	<none>
       Mounts:
         /var/jenkins_home from volume (rw)
         /var/run/secrets/kubernetes.io/serviceaccount from default-token-cp9f0 (ro)
   ...
   Volumes:
     myvol:
       Type:	PersistentVolumeClaim (a reference to a PersistentVolumeClaim in the same namespace)
       ClaimName:	mypvc
       ReadOnly:	  false

   ```
   {: screen}

7.  Log in to the pod by using the pod name that you previously noted.
    ```sh
    oc exec -it <my-pod-123456789> /bin/bash
    ```
    {: pre}

8. Verify the permissions of your container's mount path. In the example, the mount path is `/var/jenkins_home`.
   ```sh
   ls -ln /var/jenkins_home
   ```
   {: pre}

   **Example output**:
   ```sh
   jenkins@mypod-123456789:/$ ls -ln /var/jenkins_home
   total 12
   -rw-r--r-- 1 1000 1000  102 Mar  9 19:58 copy_reference_file.log
   drwxr-xr-x 2 1000 1000 4096 Mar  9 19:58 init.groovy.d
   drwxr-xr-x 9 1000 1000 4096 Mar  9 20:16 war
   ```
   {: screen}

   This output shows that the GID and UID from your Dockerfile (in this example, `1000` and `1000`) own the mount path inside the container.




