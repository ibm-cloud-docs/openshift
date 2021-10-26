---

copyright: 
  years: 2014, 2021
lastupdated: "2021-10-26"

keywords: openshift, roks, rhoks, logmet, logs, metrics, audit, events

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}


# Reviewing service, API server, and worker node logs
{: #health-audit}

Forward audit logs for {{site.data.keyword.openshiftlong_notm}}, the Kubernetes API server, and the worker nodes to a logging instance such as {{site.data.keyword.at_full}}. With audit logs, you're able to understand better what operations are initiated by users in your cluster, which can help you troubleshoot issues or report compliance to industry and internal standards.
{: shortdesc}

## Kubernetes API server audit logs
{: #audit-api-server}

To monitor user-initiated, Kubernetes administrative activity made within your cluster, you can collect and forward audit events that are passed through your Kubernetes API server to {{site.data.keyword.la_full_notm}} or an external server. Although the Kubernetes API server for your cluster is enabled for auditing by default, no auditing data is available until you set up log forwarding.
{: shortdesc}

### Considerations and prerequisites
{: #prereqs-apiserver-logs}

Before you set up a Kubernetes API audit configuration, review the following information.
{: shortdesc}

* To see how the audit webhook collects logs, check out the {{site.data.keyword.openshiftlong_notm}} [`openshift-audit` policy](https://github.com/IBM-Cloud/kube-samples/blob/master/kube-audit/openshift-audit-policy.yaml){: external}.
    You cannot modify the default policy or apply your own custom policy.
    {: note}

* For Kubernetes audit logs and verbosity, see the [Kubernetes documentation](https://kubernetes.io/docs/tasks/debug-application-cluster/audit/){: external}.
* Only one audit webhook can be created in a cluster.
* You must have the  [**Administrator** {{site.data.keyword.cloud_notm}} IAM platform access role](/docs/openshift?topic=openshift-users#checking-perms) for the {{site.data.keyword.openshiftlong_notm}} cluster.

To get started, follow the instructions to send Kubernetes API audit logs [to {{site.data.keyword.la_full_notm}}](#audit-api-server-la)or [to a resource in the {{site.data.keyword.cloud_notm}} private network](#audit-api-server-priv).

### Forwarding Kubernetes API audit logs to {{site.data.keyword.la_short}}
{: #audit-api-server-la}

To forward audit logs to {{site.data.keyword.la_full_notm}}, you can create a Kubernetes audit system by using the provided image and deployment.
{: shortdesc}

The Kubernetes audit system in your cluster consists of an audit webhook, a log collection service and webserver app, and a logging agent. The webhook collects the Kubernetes API server events from your cluster master. The log collection service is a Kubernetes `ClusterIP` service that is created from an image from the public {{site.data.keyword.cloud_notm}} registry. This service exposes a simple `node.js` HTTP webserver app that is exposed only on the private network. The webserver app parses the log data from the audit webhook and creates each log as a unique JSON line. Finally, the logging agent forwards the logs from the webserver app to {{site.data.keyword.la_full_notm}}, where you can view the logs.

**Before you begin**: Ensure that you reviewed the [considerations and prerequisites](#prereqs-apiserver-logs) and that you have the [**Administrator** {{site.data.keyword.cloud_notm}} IAM platform access role](/docs/account?topic=account-userroles) for {{site.data.keyword.la_full_notm}}.

1. Target the global container registry for public {{site.data.keyword.cloud_notm}} images.
    ```sh
    ibmcloud cr region-set global
    ```
    {: pre}

2. Optional: For more information about the `kube-audit` image, inspect `icr.io/ibm/ibmcloud-kube-audit-to-logdna`.
    ```sh
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
    ```sh
    kubectl create -f ibmcloud-kube-audit.yaml
    ```
    {: pre}

5. Verify that the `ibmcloud-kube-audit-service` pod has a **STATUS** of `Running`.
    ```sh
    kubectl get pods -l app=ibmcloud-kube-audit
    ```
    {: pre}

    Example output

    ```sh
    NAME                                             READY   STATUS             RESTARTS   AGE
    ibmcloud-kube-audit-c75cb84c5-qtzqd              1/1     Running   0          21s
    ```
    {: screen}

6. Verify that the `ibmcloud-kube-audit-service` service is deployed in your cluster. In the output, note the **CLUSTER_IP**.
    ```sh
    kubectl get svc -l app=ibmcloud-kube-audit
    ```
    {: pre}

    Example output

    ```sh
    NAME                          TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)          AGE
    ibmcloud-kube-audit-service   ClusterIP   172.21.xxx.xxx   <none>        80/TCP           1m
    ```
    {: screen}
    
7. [Log in to your account. If applicable, target the appropriate resource group. Set the context for your cluster.](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure) Make sure to specify the `--admin` flag.
    ```sh
    ibmcloud oc cluster config --cluster <cluster> --admin
    ```
    {: pre}
    
8. View your current config by running the `kubectl config view` command and review the output for the `certificate-authority`, `client-certificate`, and `client-key`.
    ```sh
    oc config view --minify
    ```
    {: pre}
    
    Example output
    
    ```sh
    clusters:
    - cluster:
        certificate-authority: /Users/user/.bluemix/plugins/container-service/clusters/cluster-name-a111a11a11aa1aa11a11-admin/ca-aaa00-id-cluster.pem
        ...
        ...
        client-certificate: /Users/user/.bluemix/plugins/container-service/clusters/cluster-name-a111a11a11aa1aa11a11-admin/admin.pem
        client-key: /Users/user/.bluemix/plugins/container-service/clusters/cluster-name-a111a11a11aa1aa11a11-admin/admin-key.pem
    ```
    {: screen}
    

9. Configure the audit webhook and specify the `certificate-authority`, `client-certificate`, and `client-key` that you retreived in the previous step.
    ```sh
    ibmcloud oc cluster master audit-webhook set --cluster <cluster> --remote-server https://127.0.0.1:2040/api/v1/namespaces/default/services/ibmcloud-kube-audit-service/proxy/post --ca-cert <certificate-authority> --client-cert <client-certificate> --client-key <client-key>
    ```
    {: pre}

10. Verify that the audit webhook is created in your cluster.
    ```sh
    ibmcloud oc cluster master audit-webhook get --cluster <cluster_name_or_ID>
    ```
    {: pre}

    Example output

    ```sh
    OK
    Server:            http://172.21.xxx.xxx
    ```
    {: screen}

11. Apply the webhook to your Kubernetes API server by refreshing the cluster master. It might take several minutes for the master to refresh.
    ```sh
    ibmcloud oc cluster master refresh --cluster <cluster_name_or_ID>
    ```
    {: pre}

12. While the master refreshes, [provision an instance of {{site.data.keyword.la_full_notm}} and deploy a logging agent to every worker node in your cluster](/docs/log-analysis?topic=log-analysis-tutorial-use-logdna). The logging agent is required to forward logs from inside your cluster to the {{site.data.keyword.la_full_notm}} service. If you already set up logging agents in your cluster, you can skip this step.

13. After the master refresh completes and the logging agents are running on your worker nodes, you can [view your Kubernetes API audit logs in {{site.data.keyword.la_full_notm}}](/docs/log-analysis?topic=log-analysis-tutorial-use-logdna).

After you set up the audit webhook in your cluster, you can monitor version updates to the `kube-audit-to-logdna` image by running `ibmcloud cr image-list --include-ibm | grep ibmcloud-kube-audit`. To see the version of the image that currently runs in your cluster, run `oc get pods | grep ibmcloud-kube-audit` to find the audit pod name, and run `kubectl describe pod <pod_name>` to see the image version.
{: tip}


### Forwarding Kubernetes API audit logs to a resource in the {{site.data.keyword.cloud_notm}} private network
{: #audit-api-server-priv}

Forward audit logs to a resource other than {{site.data.keyword.la_short}} that is outside of your cluster and accessible in the {{site.data.keyword.cloud_notm}} private network.
{: shortdesc}

Before you begin, ensure that you reviewed the [considerations and prerequisites](#prereqs-apiserver-logs).

1. Create a configuration file that is named `kube-audit-remote-private-ip.yaml`. This configuration file creates an endpoint and service for the IP address of the resource that your cluster sends logs to through the {{site.data.keyword.cloud_notm}} private network. Do not include a selector in the service.
    ```yaml
    apiVersion: v1
    kind: Endpoints
    metadata:
      name: kube-audit-remote-private-ip
    subsets:
      - addresses:
          - ip: <logging_resource_private_IP>
        ports:
          - port: 31100
    ---
    apiVersion: v1
    kind: Service
    metadata:
      name: kube-audit-remote-private-ip
    spec:
      ports:
        - protocol: TCP
          port: 80
          targetPort: 31100
    ```
    {: codeblock}

2. Create the endpoint and service.
    ```sh
    kubectl create -f kube-audit-remote-private-ip.yaml
    ```
    {: pre}

3. Verify that the `kube-audit-remote-private-ip` service is deployed in your cluster. In the output, note the **CLUSTER-IP**.
    ```sh
    kubectl get svc
    ```
    {: pre}

    Example output

    ```sh
    NAME                          TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)          AGE
    ...
    kube-audit-remote-private-ip  ClusterIP   172.21.xxx.xxx   <none>        80/TCP           1m
    ```
    {: screen}

4. Create the audit webhook to collect Kubernetes API server event logs. Add the `http://` prefix to the `CLUSTER-IP` of the service that you previously retrieved.
    ```sh
    ibmcloud oc cluster master audit-webhook set --cluster <cluster_name_or_ID> --remote-server http://172.21.xxx.xxx
    ```
    {: pre}

5. Verify that the audit webhook is created in your cluster.
    ```sh
    ibmcloud oc cluster master audit-webhook get --cluster <cluster_name_or_ID>
    ```
    {: pre}

    Example output

    ```sh
    OK
    Server:            http://172.21.xxx.xxx
    ```
    {: screen}

6. Apply the webhook to your Kubernetes API server by refreshing the cluster master. The master might take several minutes to refresh.
    ```sh
    ibmcloud oc cluster master refresh --cluster <cluster_name_or_ID>
    ```
    {: pre}

After the master refresh completes, your logs are sent to the private IP address of your logging resource.





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



## Service audit logs
{: #audit-service}

By default, {{site.data.keyword.openshiftlong_notm}} generates and sends events to {{site.data.keyword.at_full_notm}}. To see these events, you must create an {{site.data.keyword.at_full_notm}} instance. For more information, see [{{site.data.keyword.at_full_notm}} events](/docs/containers?topic=containers-at_events).




