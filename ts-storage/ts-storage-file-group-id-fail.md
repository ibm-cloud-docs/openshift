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
  
  
# File storage: Why does my app fail with a group ID error for NFS file storage permissions?
{: #root}

**Infrastructure provider**: <img src="../images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Classic

{: tsSymptoms}
After you [create](/docs/openshift?topic=openshift-file_storage#add_file) or [add existing](/docs/openshift?topic=openshift-file_storage#existing_file) NFS storage to your cluster, your app's container deployment fails. You see group ID (GID) error messages.

{: tsCauses}
When you create a container from an image that does not specify a user and user ID (UID), all instructions in the Dockerfile are run by the root user (UID: 0) inside the container by default. However, when you want to mount an NFS file share to your container, the user ID `0` inside the container is mapped to the user ID `nobody` on the NFS host system. Therefore, the volume mount path is owned by the user ID `nobody` and not by `root`. This security feature is also known as root squash. Root squash protects the data within NFS by mounting the container without granting the user ID root permissions on the actual NFS host file system.

{: tsResolve}
Use a Kubernetes [`DaemonSet`](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/){: external} to enable root permission to the storage mount path on all of your worker nodes for NFSv4 file shares.

To allow root permission on the volume mount path, you must set up a configmap on your worker node. The configmap maps the user ID `nobody` from the NFS host system to the root user ID `0` in your container. This process is also referred to as no root squash. An effective way of updating all of your worker nodes is to use a daemon set, which runs a specified pod on every worker node in your cluster. In this case, the pod that is controlled by the daemon set updates each of your worker nodes to enable root permission on the volume mount path.

The deployment is configured to allow the daemon set pod to run in privileged mode, which is necessary to access the host file system. Running a pod in privileged mode does create a security risk, so use this option with caution.

While the daemon set is running, new worker nodes that are added to the cluster are automatically updated.

Before you begin:

* [Create persistent storage](/docs/openshift?topic=openshift-file_storage#add_file).
* [Access your {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-access_cluster).

Steps:

1.  Copy the `norootsquash` daemon set [deployment YAML file](https://github.com/IBM-Cloud/kube-samples/tree/master/daemonset-sample){: external}

2.  Create the `norootsquash` daemon set deployment.
    ```sh
    oc apply -f norootsquash.yaml
    ```
    {: pre}

3.  Get the name of the pod that your storage volume is mounted to. This pod is not the same as the `norootsquash`  pods.
    ```sh
    oc get pods
    ```
    {: pre}

4.  Log in to the pod.
    ```sh
    oc exec -it mypod /bin/bash
    ```
    {: pre}

5.  Verify that the permissions to the mount path are `root`.
    ```sh
    root@mypod:/# ls -al /mnt/myvol/
    total 8
    drwxr-xr-x 2 root root 4096 Feb  7 20:49 .
    drwxr-xr-x 1 root root 4096 Feb 20 18:19 .
    ```
    {: pre}

    This output shows that the UID in the first row is now owned by `root` (instead of previously `nobody`).

6.  If the UID is owned by `nobody`, exit the pod and reboot your cluster's worker nodes. Wait for the nodes to reboot.
    ```sh
    ibmcloud oc worker reboot --cluster <my_cluster> --worker <my_worker1>,<my_worker2>
    ```
    {: pre}

7. Repeat Steps 4 and 5 to verify the permissions.



