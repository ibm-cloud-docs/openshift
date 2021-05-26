---

copyright:
  years: 2014, 2021
lastupdated: "2021-05-26"

keywords: openshift, roks, rhoks, logmet, logs, metrics, audit, events

subcollection: containers

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
  
  
# Reviewing service, API server, and worker node logs
{: #health-audit}

Forward audit logs for {{site.data.keyword.openshiftlong_notm}}, the Kubernetes API server, and the worker nodes to a logging instance such as {{site.data.keyword.at_full}}. With audit logs, you're able to understand better what operations are initiated by users in your cluster, which can help you troubleshoot issues or report compliance to industry and internal standards.
{: shortdesc}

## Kubernetes API server audit logs
{: #audit-api-server}

To monitor user-initiated, Kubernetes administrative activity made within your cluster, you can collect and forward audit events that are passed through your Kubernetes API server to {{site.data.keyword.la_full_notm}} or an external server. Although the Kubernetes API server for your cluster is enabled for auditing by default, no auditing data is available until you set up log forwarding.
{: shortdesc}

### Understanding the Kubernetes API audit configuration
{: #api-server-config}

To review the Kubernetes API audit configuration, review the following information.
* To see how the audit webhook collects logs, check out the {{site.data.keyword.openshiftlong_notm}} [`openshift-audit` policy](https://github.com/IBM-Cloud/kube-samples/blob/master/kube-audit/openshift-audit-policy.yaml){: external}.
  You cannot modify the default policy or apply your own custom policy.
  {: note}
* For Kubernetes audit logs and verbosity, see the [Kubernetes documentation](https://kubernetes.io/docs/tasks/debug-application-cluster/audit/){: external}.

### Forwarding Kubernetes API audit logs to {{site.data.keyword.la_short}}
{: #audit-api-server-la}

To set up your cluster to forward audit logs to {{site.data.keyword.la_full_notm}}, you can create a Kubernetes audit system by using the provided image and deployment.
{: shortdesc}

The Kubernetes audit system in your cluster consists of an audit webhook, a log collection service and webserver app, and a logging agent. The webhook collects the Kubernetes API server events from your cluster master. The log collection service is a Kubernetes `ClusterIP` service that is created from an image from the public {{site.data.keyword.cloud_notm}} registry. This service exposes a simple `node.js` HTTP webserver app that is exposed only on the private network. The webserver app parses the log data from the audit webhook and creates each log as a unique JSON line. Finally, the logging agent forwards the logs from the webserver app to {{site.data.keyword.la_full_notm}}, where you can view the logs.

For more information, see the following topics:
* To see how the audit webhook collects logs, check out the {{site.data.keyword.openshiftlong_notm}} [`openshift-audit` policy](https://github.com/IBM-Cloud/kube-samples/blob/master/kube-audit/openshift-audit-policy.yaml){: external}.
  You cannot modify the default policy or apply your own custom policy.
  {: note}
* For Kubernetes audit logs and verbosity, see the [Kubernetes documentation](https://kubernetes.io/docs/tasks/debug-application-cluster/audit/){: external}.

**Before you begin**:

* You must have the following permissions:
  * [**Administrator** {{site.data.keyword.cloud_notm}} IAM platform access role](/docs/openshift?topic=openshift-users#platform) for the {{site.data.keyword.openshiftlong_notm}} cluster.
  * [**Administrator** {{site.data.keyword.cloud_notm}} IAM platform access role](/docs/account?topic=account-userroles) for {{site.data.keyword.la_full_notm}}.
* For the cluster that you want to collect API server audit logs from: [Log in to your account. If applicable, target the appropriate resource group. Set the context for your cluster.](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure)
* Keep in mind that only one audit webhook can be created in a cluster. You can set up an audit webhook to forward logs to {{site.data.keyword.la_full_notm}} or to forward logs to an external syslog server, but not both.

**To forward Kubernetes API audit logs to {{site.data.keyword.la_full_notm}}:**

1. Target the global container registry for public {{site.data.keyword.cloud_notm}} images.
  ```
  ibmcloud cr region-set global
  ```
  {: pre}

2. Optional: For more information about the `kube-audit` image, inspect `icr.io/ibm/ibmcloud-kube-audit-to-logdna`.
  ```
  ibmcloud cr image-inspect icr.io/ibm/ibmcloud-kube-audit-to-logdna
  ```
  {: pre}

3. Create a configuration file that is named `ibmcloud-kube-audit.yaml`. This configuration file creates a log collection service and a deployment that pulls the `icr.io/ibm/ibmcloud-kube-audit-to-logdna` image to create a log collection container.
  ```yaml
  apiVersion: v1
  kind: List
  metadata:
    name: ibmcloud-kube-audit
  items:
    - apiVersion: apps/v1
      kind: Deployment
      metadata:
        name: ibmcloud-kube-audit
        labels:
          app: ibmcloud-kube-audit
      spec:
        replicas: 1
        selector:
          matchLabels:
            app: ibmcloud-kube-audit
        template:
          metadata:
            labels:
              app: ibmcloud-kube-audit
          spec:
            containers:
              - name: ibmcloud-kube-audit
                image: 'icr.io/ibm/ibmcloud-kube-audit-to-logdna:latest'
                ports:
                  - containerPort: 3000
    - apiVersion: v1
      kind: Service
      metadata:
        name: ibmcloud-kube-audit-service
        labels:
          app: ibmcloud-kube-audit
      spec:
        selector:
          app: ibmcloud-kube-audit
        ports:
          - protocol: TCP
            port: 80
            targetPort: 3000
        type: ClusterIP
  ```
  {: codeblock}

4. Create the deployment in the `default` namespace of your cluster.
  ```
  kubectl create -f ibmcloud-kube-audit.yaml
  ```
  {: pre}

5. Verify that the `ibmcloud-kube-audit-service` pod has a **STATUS** of `Running`.
  ```
  kubectl get pods -l app=ibmcloud-kube-audit
  ```
  {: pre}

  Example output:
  ```
  NAME                                             READY   STATUS             RESTARTS   AGE
  ibmcloud-kube-audit-c75cb84c5-qtzqd              1/1     Running   0          21s
  ```
  {: screen}

6. Verify that the `ibmcloud-kube-audit-service` service is deployed in your cluster. In the output, note the **CLUSTER_IP**.
  ```
  kubectl get svc -l app=ibmcloud-kube-audit
  ```
  {: pre}

  Example output:
  ```
  NAME                          TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)          AGE
  ibmcloud-kube-audit-service   ClusterIP   172.21.xxx.xxx   <none>        80/TCP           1m
  ```
  {: screen}

7. Create the audit webhook to collect Kubernetes API server event logs. Add the `http://` prefix to the **CLUSTER_IP**.
  ```
  ibmcloud oc cluster master audit-webhook set --cluster <cluster_name_or_ID> --remote-server http://172.21.xxx.xxx
  ```
  {: pre}

8. Verify that the audit webhook is created in your cluster.
  ```
  ibmcloud oc cluster master audit-webhook get --cluster <cluster_name_or_ID>
  ```
  {: pre}

  Example output:
  ```
  OK
  Server:			http://172.21.xxx.xxx
  ```
  {: screen}

9. Apply the webhook to your Kubernetes API server by refreshing the cluster master. It might take several minutes for the master to refresh.
  ```
  ibmcloud oc cluster master refresh --cluster <cluster_name_or_ID>
  ```
  {: pre}

10. While the master refreshes, [provision an instance of {{site.data.keyword.la_full_notm}} and deploy a logging agent to every worker node in your cluster](/docs/log-analysis?topic=log-analysis-kube#kube). The logging agent is required to forward logs from inside your cluster to the {{site.data.keyword.la_full_notm}} service. If you already set up logging agents in your cluster, you can skip this step.

11. After the master refresh completes and the logging agents are running on your worker nodes, you can [view your Kubernetes API audit logs in {{site.data.keyword.la_full_notm}}](/docs/log-analysis?topic=log-analysis-kube#kube_step3).



<br />



## Worker node audit logs
{: #audit-worker}

{{site.data.keyword.openshiftlong_notm}} uses the Linux Auditing System component, auditd, to monitor and log activity on the worker nodes. Although worker node auditing is enabled by default, no auditing data is available until you set up log forwarding to a {{site.data.keyword.la_short}} instance or external server.
{: shortdesc}

### Understanding the worker node audit configuration
{: #audit-worker-config}

The logs are stored in the `/var/log/audit` directory on the worker nodes. You can view the logs in {{site.data.keyword.la_short}} or your external server after you set up log forwarding.
{: shortdesc}

Auditd collects logs on various events, including the following:
- Linux system calls (syscalls)
- SELinux denials
- SELinux policy modificiations
- Software modifications through the `yum` package installer
- Systemd operations
- Linux user and group modifications
- Netfilter change modificiations 
- SSH Logins

### Setting up log forwarding for worker nodes
{: #audit-worker-setup}

See [Forwarding logs to an {{site.data.keyword.la_full_notm}} instance](/docs/containers?topic=containers-health#logging).
{: shortdesc}

<br />



## Service audit logs
{: #audit-service}

By default, {{site.data.keyword.openshiftlong_notm}} generates and sends events to {{site.data.keyword.at_full_notm}}. To see these events, you must create an {{site.data.keyword.at_full_notm}} instance. For more information, see [{{site.data.keyword.at_full_notm}} events](/docs/openshift?topic=openshift-at_events).
