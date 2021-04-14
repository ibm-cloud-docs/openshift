---

copyright:
  years: 2014, 2021
lastupdated: "2021-04-14"

keywords: openshift, openshift container storage, ocs, vpc, roks

subcollection: openshift

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
 


# Deploying an app that uses OpenShift Container Storage
{: #ocs-deploy-app}

After you install the OpenShift Container Storage add-on for your {{site.data.keyword.openshiftlong}} cluster, you can use the OCS storage classes to create a persistent volume claim (PVC). Then, refer to the PVC in your deployment so that your app can save and use data from the underlying OCS storage device.
{: shortdesc}

Before you begin, [prepare your cluster](/docs/openshift?topic=openshift-ocs-storage-prep) and [install OCS](/docs/openshift?topic=openshift-ocs-storage-install).

**Minimum required permissions**: **Editor** platform access role and the **Writer** service access role for the cluster in {{site.data.keyword.containerlong_notm}}.

[Access your {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-access_cluster).

1. List the OCS storage classes. For more information about OCS storage classes, see the [Storage class reference](#ocs-sc-ref).
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
    name: ocs-pvc
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
         claimName: ocs-pvc
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

   Example output:
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

      Example output:
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


<br />



