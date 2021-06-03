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
  
  
# Object Storage: Why is the transport endpoint not connected?
{: cos_transport_ts_connect}

**Infrastructure provider**:
* <img src="../images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Classic
* <img src="../images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> VPC

{: tsSymptoms}
When you create a PVC, you see an error message similar to the following:

```sh
Transport endpoint is not connected.
```
{: screen}

{: tsCauses}
To determine the cause of the issue, gather system logs by deploying an `inspectnode` pod.

{: tsResolve}
Follow the steps to gather logging information.

1. Create a `debug-pvc.yaml` file and specify the `ibm.io/debug-level: "info"` and `ibm.io/curl-debug: "true"` annonations.
   ```yaml
   apiVersion: v1
   kind: PersistentVolumeClaim
   metadata:
      annotations:
        ibm.io/auto-create-bucket: "false"
        ibm.io/auto-delete-bucket: "false"
        ibm.io/bucket: <bucket-name> # Enter the name of your bucket.
        ibm.io/secret-name: <cos-secret-name> # Enter the name of your Kubernetes secret that contains your COS credentails
        ibm.io/debug-level: "info"
        ibm.io/curl-debug: "true"
      name: debug-pvc
      namespace: default
   spec:
     storageClassName: ibmc-s3fs-standard-perf-regional
     accessModes:
     - ReadWriteOnce
     resources:
       requests:
         storage: 10Gi
   ```
   {: codeblock}

2. Create the `debug-pvc` PVC in your cluster.
   ```sh
   oc create -f debug-pvc.yaml>
   ```
   {: pre}

3. Redploy your app and reference the `debug-pvc`. Alternatively, you can use the following sample pod.
   ```yaml
   apiVersion: v1
   kind: Pod
   metadata:
      name: debug-pod
   spec:
      volumes:
      - name: nginx
         persistentVolumeClaim:
            claimName: cos-debug
      containers:
      - name: nginx
        image: nginx
        volumeMounts:
         - mountPath: /debug
           name: nginx
   ```
   {: codeblock}

4. Save the following daemonset configuration file as `inspectnode-ds.yaml`. After you deploy an app that references the PVC that you created earlier, deploy the daemonset when the `Transport endpoint is not connected.` error occurs to gather the logs.
   ```yaml
   apiVersion: apps/v1
   kind: DaemonSet
   metadata:
      namespace: default
      name: ibm-inspectnode
      labels:
         app: ibm-inspectnode
   spec:
      selector:
         matchLabels:
            app: ibm-inspectnode
      updateStrategy:
         type: RollingUpdate
      template:
         metadata:
            labels:
               app: ibm-inspectnode
         spec:
            tolerations:
            - operator: "Exists"
            hostNetwork: true
            containers:
              - name: inspectnode
               image: alpine:latest
               command: ["/bin/sh"]
               args: ["-c", "while true; do msg=$(date); echo $msg; sleep 30; done"]
               securityContext:
                  runAsUser: 0
               volumeMounts:
                 - mountPath: /host/var/log
                   name: host-log
            volumes:
              - name: host-log
                hostPath:
                  path: /var/log
   ```
   {: codeblock}

5. Create the deamonset in your cluster when the `Transport endpoint is not connected.` error occurs.
   ```sh
   oc create -f ./inspectnode-ds.yaml
   ```
   {: pre}

6. Get the name of the `inspectnode` pod that is deployed by the daemonset.
   ```sh
   oc get pods -n default -l app=ibm-inspectnode -o wide
   ```
   {: pre}

7. Copy the logs from `inspectnode` pod to your local machine. In the copy command, give your directory a name so that you can identify which node the logs are from. For example, `node-one.log`. You might also use the node IP in the directory name, for example: `10.XXX.XX.XXX.log`.
   ```sh
   oc cp <inspectnode_pod_name>:/host/var/log  ./<node_name>.log
   ```
   {: pre}

8. Review the `syslog` and the `s3fslog` for information about the `Transport endpoint` error. [Open a support ticket](/docs/openshift?topic=openshift-get-help#help-support) and share the log files that you gathered.

9. Delete the `ibm-inspectnode` daemonset that you deployed.
   ```sh
   oc delete daemonset ibm-inspectnode
   ```
   {: pre}



