---

copyright:
  years: 2014, 2020
lastupdated: "2020-06-23"

keywords: oks, iro, openshift, red hat, red hat openshift, rhos, roks, rhoks

subcollection: openshift

---

{:beta: .beta}
{:codeblock: .codeblock}
{:deprecated: .deprecated}
{:download: .download}
{:external: target="_blank" .external}
{:faq: data-hd-content-type='faq'}
{:gif: data-image-type='gif'}
{:help: data-hd-content-type='help'}
{:important: .important}
{:new_window: target="_blank"}
{:note: .note}
{:pre: .pre}
{:preview: .preview}
{:screen: .screen}
{:shortdesc: .shortdesc}
{:support: data-reuse='support'}
{:table: .aria-labeledby="caption"}
{:tip: .tip}
{:troubleshoot: data-hd-content-type='troubleshoot'}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:tsSymptoms: .tsSymptoms}



# Logging and monitoring cluster health
{: #health}

For cluster metrics and app logging and monitoring, {{site.data.keyword.openshiftlong}} clusters include built-in tools to help you manage the health of your single cluster instance. You can also set up {{site.data.keyword.cloud_notm}} tools for multi-cluster analysis or other use cases, such as {{site.data.keyword.containerlong_notm}} add-ons: {{site.data.keyword.la_full_notm}} and {{site.data.keyword.mon_full_notm}}.
{: shortdesc}

## Understanding options for logging and monitoring
{: #oc_logmet_options}

To help understand when to use the built-in OpenShift tools or {{site.data.keyword.cloud_notm}} integrations, review the following table.

<table summary="The rows are read left to right, with the type of solution in column one, the description of the built-in OpenShift tooling in column two, and the description of the {{site.data.keyword.cloud_notm}} integration in column three.">
    <caption>Comparing OpenShift and {{site.data.keyword.cloud_notm}} logging and monitoring solutions</caption>
    <thead>
      <th>Type</th>
      <th>OpenShift tools</th>
      <th>{{site.data.keyword.cloud_notm}} integrations</th>
    </thead>
    <tbody>
    <tr>
        <td>**Cluster and app logging**</td>
        <td>**Built-in OpenShift logging tools**:<ul>
          <li>Built-in view of pod logs in the OpenShift web console.</li>
          <li>Built-in pod logs are not configured with persistent storage. You must integrate with a cloud database to back up the logging data and make it highly available, and manage the logs yourself.</li></ul>
          <p class="note"><img src="images/icon-version-311.png" alt="Version 3.11 icon" width="30" style="width:30px; border-style: none"/> **OpenShift 3.11**: You cannot run the Ansible playbook to deploy the [OpenShift Container Platform Elasticsearch, Fluentd, and Kibana (EFK) stack ![External link icon](../icons/launch-glyph.svg "External link icon")](https://docs.openshift.com/container-platform/3.11/install_config/aggregate_logging.html) because you cannot modify the default configuration of the Red Hat OpenShift on IBM Cloud cluster.</p><p class="note"><img src="images/icon-version-43.png" alt="Version 4.3 icon" width="30" style="width:30px; border-style: none"/> **OpenShift 4.3**: To set up an [OpenShift Container Platform Elasticsearch, Fluentd, and Kibana (EFK) stack ![External link icon](../icons/launch-glyph.svg "External link icon")](https://docs.openshift.com/container-platform/4.3/logging/cluster-logging.html), see [installing the cluster logging operator](#oc_logging_operator).</p></td>
        <td>**{{site.data.keyword.la_full_notm}}**:<ul>
          <li>Customizable user interface for live streaming of log tailing, real-time troubleshooting, issue alerts, and log archiving.</li>
          <li>Quick integration with the cluster via a script.</li>
          <li>Aggregated logs across clusters and cloud providers.</li>
          <li>Historical access to logs that is based on the plan you choose.</li>
          <li>Highly available, scalable, and compliant with industry security standards.</li>
          <li>Integrated with {{site.data.keyword.cloud_notm}} IAM for user access management.</li>
          <li>Flexible plans, including a free `Lite` option.</li></ul>
          <br>To get started, see [Creating a logging configuration to forward cluster and app logs to {{site.data.keyword.la_full_notm}}](#openshift_logdna).</td>
    </tr>
    <tr>
        <td>**API audit logging**</td>
        <td>**Built-in OpenShift audit logging tools**:<br>
        API audit logging to monitor user-initiated activities is currently not supported.</td>
        <td>**{{site.data.keyword.la_full_notm}}**:<ul>
          <li>Customizable user interface for live streaming of log tailing, real-time troubleshooting, issue alerts, and log archiving.</li>
          <li>Quick integration with the cluster via a script.</li>
          <li>Aggregated logs across clusters and cloud providers.</li>
          <li>Historical access to logs that is based on the plan you choose.</li>
          <li>Highly available, scalable, and compliant with industry security standards.</li>
          <li>Integrated with {{site.data.keyword.cloud_notm}} IAM for user access management.</li>
          <li>Flexible plans, including a free `Lite` option.</li></ul>
          <br>To get started, see [Forwarding Kubernetes API audit logs to LogDNA](#openshift_logdna_audit).<p class="note">Forwarding Kubernetes API audit logs to LogDNA is not supported for version 3.11 clusters.</p><br>
          **{{site.data.keyword.at_full_notm}}**:<br>
          Use {{site.data.keyword.at_full_notm}} to view cluster management events that are generated by the Red Hat OpenShift on IBM Cloud API. To access these logs, [provision an instance of {{site.data.keyword.at_full_notm}}](/docs/Activity-Tracker-with-LogDNA?topic=Activity-Tracker-with-LogDNA-getting-started). For more information about the types of {{site.data.keyword.containerlong_notm}} events that you can track, see [Activity Tracker events](/docs/openshift?topic=openshift-at_events).</td>
    </tr>
    <tr>
        <td>**Monitoring**</td>
        <td>**Built-in OpenShift monitoring tools**:<ul>
          <li>Built-in Prometheus and Grafana deployments in `openshift-monitoring` project for cluster metrics.</li>
          <li>At-a-glance, real-time view of how your pods consume cluster resources that can be accessed from the OpenShift **Cluster Console**.</li>
          <li>Monitoring is on a per-cluster basis.</li>
          <li>The `openshift-monitoring` project stack is set up in a single zone only. No persistent storage is available to back up or view metric history.</li></ul>
          <br>For more information, see [the OpenShift documentation ![External link icon](../icons/launch-glyph.svg "External link icon")](http://docs.openshift.com/container-platform/4.3/monitoring/cluster_monitoring/about-cluster-monitoring.html).</td>
        <td>**{{site.data.keyword.mon_full_notm}}**:<ul>
          <li>Customizable user interface for a unified look at your cluster metrics, container security, resource usage, alerts, and custom events.</li>
          <li>Quick integration with the cluster via a script.</li>
          <li>Aggregated metrics and container monitoring across clusters and cloud providers for consistent operations enablement.</li>
          <li>Historical access to metrics that is based on the timeline and plan, and ability to capture and download trace files.</li>
          <li>Highly available, scalable, and compliant with industry security standards.</li>
          <li>Integrated with {{site.data.keyword.cloud_notm}} IAM for user access management.</li>
          <li>Free trial to try out the capabilities.</li></ul>
          <br>To get started, see [Creating a monitoring configuration to forward cluster and app metrics to {{site.data.keyword.mon_full_notm}}](#openshift_sysdig).</td>
    </tr>
    </tbody>
</table>

<br />




## Creating a logging configuration to forward cluster and app logs to {{site.data.keyword.la_full_notm}}
{: #openshift_logdna}

Use the Red Hat OpenShift on IBM Cloud observability plug-in to create a logging configuration for {{site.data.keyword.la_full_notm}} in your cluster, and use this logging configuration to automatically collect and forward pod logs to {{site.data.keyword.la_full_notm}}.
{: shortdesc}

You can have only one logging configuration for {{site.data.keyword.la_full_notm}} in your cluster at a time. If you want to use a different {{site.data.keyword.la_full_notm}} service instance to send logs to, first remove any existing logging configuration and then follow the steps to create your new one.
{: note}



Before you begin:
- Verify that you are assigned the **Editor** platform role and **Manager** server access role for {{site.data.keyword.la_full_notm}}.
- Verify that you are assigned the **Administrator** platform role and the **Manager** service access role for all Kubernetes namespaces in {{site.data.keyword.containerlong_notm}} to create the logging configuration. To view a logging configuration or launch the LogDNA dashboard after the logging configuration is created, users must be assigned the **Administrator** platform role and the **Manager** service access for the `ibm-observe` Kubernetes namespace in {{site.data.keyword.containerlong_notm}}.
- If you want to use the CLI to set up the logging configuration:
  - [Install the Red Hat OpenShift on IBM Cloud observability CLI plug-in (`ibmcloud ob`)](/docs/containers?topic=containers-cs_cli_install#cs_cli_install_steps).
  - [Access your OpenShift cluster](/docs/openshift?topic=openshift-access_cluster).

To set up a logging configuration for your cluster:

1. Create an [{{site.data.keyword.la_full_notm}} service instance](/docs/Log-Analysis-with-LogDNA?topic=Log-Analysis-with-LogDNA-provision) and note the name of the instance. The service instance must belong to the same {{site.data.keyword.cloud_notm}} account where you created your cluster, but can be in a different resource group and {{site.data.keyword.cloud_notm}} region than your cluster.
2. Set up a logging configuration for your cluster. When you create the logging configuration, an OpenShift project `ibm-observe` is created and a LogDNA agent is deployed as a daemonset to all worker nodes in your cluster. This agent collects logs with the extension `*.log` and extensionless files that are stored in the `/var/log` directory of your pod from all projects, including `kube-system`. The agent then forwards the logs to the {{site.data.keyword.la_full_notm}} service.

   - **From the console:**
     1. From the [Red Hat OpenShift on IBM Cloud console](https://cloud.ibm.com/kubernetes/clusters?platformType=openshift){: external}, select the cluster for which you want to create a LogDNA logging configuration.
     2. On the cluster **Overview** page, click **Connect**.
     3. Select the region and the {{site.data.keyword.la_full_notm}} service instance that you created earlier, and click **Connect**.

   - **From the CLI:**
     1.  Create the LogDNA logging configuration. When you create the LogDNA logging configuration, the ingestion key that was last added is retrieved automatically. If you want to use a different ingestion key, add the `--logdna-ingestion-key <ingestion_key>` option to the command.

         ```
         ibmcloud ob logging config create --cluster <cluster_name_or_ID> --instance <LogDNA_instance_name_or_ID>
         ```
         {: pre}

         Example output:
         ```
         Creating configuration...
         OK
         ```
         {: screen}

     2. Verify that the logging configuration was added to your cluster.
        ```
        ibmcloud ob logging config list --cluster <cluster_name_or_ID>
        ```
        {: pre}

        Example output:
        ```
        Listing configurations...

        OK
        Instance Name                            Instance ID                            CRN   
        IBM Cloud Log Analysis with LogDNA-opm   1a111a1a-1111-11a1-a1aa-aaa11111a11a   crn:v1:prod:public:logdna:us-south:a/a11111a1aaaaa11a111aa11a1aa1111a:1a111a1a-1111-11a1-a1aa-aaa11111a11a::  
        ```
        {: screen}

3. Optional: Verify that the LogDNA agent was set up successfully.
   1. If you used the console to create the LogDNA logging configuration, log in to your cluster. For more information, see [Access your OpenShift cluster](/docs/openshift?topic=openshift-access_cluster)..

   2. Verify that the daemonset for the LogDNA agent was created and all instances are listed as `AVAILABLE`.
      ```
      oc get daemonsets -n ibm-observe
      ```
      {: pre}

      Example output:
      ```
      NAME           DESIRED   CURRENT   READY   UP-TO-DATE   AVAILABLE   NODE SELECTOR   AGE
      logdna-agent   9         9         9       9            9           <none>          14m
      ```
      {: screen}

      The number of daemonset instances that are deployed equals the number of worker nodes in your cluster.

   3. Review the configmap that was created for your LogDNA agent.
      ```
      oc describe configmap -n ibm-observe
      ```
      {: pre}

4. Access the logs for your pods from the LogDNA dashboard.
   1. From the [Red Hat OpenShift on IBM Cloud console](https://cloud.ibm.com/kubernetes/clusters?platformType=openshift){: external}, select the cluster that you configured.  
   2. On the cluster **Overview** page, click **Launch**. The LogDNA dashboard opens.
   3. Review the pod logs that the LogDNA agent collected from your cluster. It might take a few minutes for your first logs to show.

5. Review how you can [search and filter logs in the LogDNA dashboard](/docs/Log-Analysis-with-LogDNA?topic=Log-Analysis-with-LogDNA-view_logs). 


## Forwarding Kubernetes API audit logs to {{site.data.keyword.la_full_notm}}
{: #openshift_logdna_audit}

Collect and forward any events that are passed through your Kubernetes API server to {{site.data.keyword.la_full_notm}}.
{: shortdesc}

Forwarding Kubernetes API audit logs to LogDNA is not supported for version 3.11 clusters.
{: note}

In the following steps, you create an audit system in your cluster that consists of an audit webhook, a log collection service and webserver app, and a logging agent. The webhook collects the Kubernetes API server events from your cluster master. The log collection service is a Kubernetes `ClusterIP` service that is created from an image from the public {{site.data.keyword.cloud_notm}} registry. This service exposes a simple `node.js` HTTP webserver app that is exposed only on the private network. The webserver app parses the log data from the audit webhook and creates each log as a unique JSON line. Finally, the logging agent forwards the logs from the webserver app to {{site.data.keyword.la_full_notm}}, where you can view the logs.

To see how the audit webhook collects logs, check out the {{site.data.keyword.containerlong_notm}} [`kube-audit` policy](https://github.com/IBM-Cloud/kube-samples/blob/master/kube-audit/kube-audit-policy.yaml){: external}.

You cannot modify the default `kube-audit` policy or apply your own custom policy.
{: note}

**Before you begin**:

* You must have the following permissions:
  * [**Administrator** {{site.data.keyword.cloud_notm}} IAM platform role](/docs/openshift?topic=openshift-users#platform) for the cluster.
  * [**Administrator** {{site.data.keyword.cloud_notm}} IAM platform role](/docs/iam?topic=iam-userroles) for {{site.data.keyword.la_full_notm}}.
* For the cluster that you want to collect API server audit logs from: [Access your OpenShift cluster](/docs/openshift?topic=openshift-access_cluster).
* Keep in mind that only one audit webhook can be created in a cluster.

**To forward Kubernetes API audit logs to {{site.data.keyword.la_full_notm}}:**

1. [Set up an {{site.data.keyword.la_full_notm}} instance and configure the LogDNA agent in your cluster](#openshift_logdna).

2. Target the global container registry for public {{site.data.keyword.cloud_notm}} images.
  ```
  ibmcloud cr region-set global
  ```
  {: pre}

3. Optional: For more information about the `kube-audit` image, inspect `icr.io/ibm/ibmcloud-kube-audit-to-logdna`.
  ```
  ibmcloud cr image-inspect icr.io/ibm/ibmcloud-kube-audit-to-logdna
  ```
  {: pre}

4. Create a configuration file that is named `ibmcloud-kube-audit.yaml`. This configuration file creates a log collection service and a deployment that pulls the `icr.io/ibm/ibmcloud-kube-audit-to-logdna` image to create a log collection container.
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

5. Create the deployment in the `default` namespace of your cluster.
  ```
  kubectl create -f ibmcloud-kube-audit.yaml
  ```
  {: pre}

6. Verify that the `ibmcloud-kube-audit-service` pod has a **STATUS** of `Running`.
  ```
  kubectl get pods -l app=ibmcloud-kube-audit
  ```
  {: pre}

  Example output:
  ```
  NAME                                             READY   STATUS         RESTARTS   AGE
  ibmcloud-kube-audit-c75cb84c5-qtzqd              1/1     Running        0          21s
  ```
  {: screen}

7. Verify that the `ibmcloud-kube-audit-service` service is deployed in your cluster. In the output, note the **CLUSTER_IP**.
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

8. Create the audit webhook to collect Kubernetes API server event logs. Add the `http://` prefix to the **CLUSTER_IP**.
  ```
  ibmcloud oc cluster master audit-webhook set --cluster <cluster_name_or_ID> --remote-server http://172.21.xxx.xxx
  ```
  {: pre}

9. Verify that the audit webhook is created in your cluster.
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

10. Apply the webhook to your Kubernetes API server by refreshing the cluster master.
  ```
  ibmcloud oc cluster master refresh --cluster <cluster_name_or_ID>
  ```
  {: pre}

11. After the master refresh completes, access your logs from the LogDNA dashboard.
    1. From the [{{site.data.keyword.cloud_notm}} **Observability > Logging** console](https://cloud.ibm.com/observe/logging), in the row for your {{site.data.keyword.la_short}} instance, click **View LogDNA**. The LogDNA dashboard opens.
    2. Wait a few minutes for your logs to display.

<br />


## Creating a monitoring configuration to forward cluster and app metrics to {{site.data.keyword.mon_full_notm}} 
{: #openshift_sysdig}

Use the Red Hat OpenShift on IBM Cloud observability plug-in to create a monitoring configuration for {{site.data.keyword.mon_full_notm}} in your cluster, and use this monitoring configuration to automatically collect and forward metrics to {{site.data.keyword.mon_full_notm}}.
{: shortdesc}

With {{site.data.keyword.mon_full_notm}}, you can collects cluster and pod metrics, such as the CPU and memory usage of your worker nodes, incoming and outgoing HTTP traffic for your pods, and data about several infrastructure components. In addition, the agent can collect custom application metrics by using either a Prometheus-compatible scraper or a StatsD facade.

You can have only one monitoring configuration for {{site.data.keyword.mon_full_notm}} in your cluster at a time. If you want to use a different {{site.data.keyword.mon_full_notm}} service instance to send metrics to, first remove any existing monitoring configuration and then follow the steps to create your new one.
{: note}


Before you begin:
- Verify that you are assigned the **Editor** platform role and **Manager** server access role for {{site.data.keyword.mon_full_notm}}.
- Verify that you are assigned the **Administrator** platform role and the **Manager** service access role for all Kubernetes namespaces in {{site.data.keyword.containerlong_notm}} to create the monitoring configuration. To view a monitoring configuration or launch the Sysdig dashboard after the monitoring configuration is created, users must be assigned the **Administrator** platform role and the **Manager** service access role for the `ibm-observe` Kubernetes namespace in {{site.data.keyword.containerlong_notm}}.
- If you want to use the CLI to set up the monitoring configuration:
  - [Install the Red Hat OpenShift on IBM Cloud observability CLI plug-in (`ibmcloud ob`)](/docs/containers?topic=containers-cs_cli_install#cs_cli_install_steps).
  - [Access your OpenShift cluster](/docs/openshift?topic=openshift-access_cluster).

To set up a monitoring configuration for your cluster:

1. Create an [{{site.data.keyword.mon_full_notm}} service instance](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-provision) and note the name of the instance. The service instance must belong to the same {{site.data.keyword.cloud_notm}} account where you created your cluster, but can be in a different resource group and {{site.data.keyword.cloud_notm}} region than your cluster.
2. Set up a monitoring configuration for your cluster. When you create the monitoring configuration, an OpenShift project `ibm-observe` is created and a Sysdig agent is deployed as a Kubernetes daemonset to all worker nodes in your cluster. This agent collects cluster and pod metrics, such as the worker node CPU and memory usage, or the amount incoming and outgoing network traffic to your pods.

   - **From the console: **
     1. From the [Red Hat OpenShift on IBM Cloud console](https://cloud.ibm.com/kubernetes/clusters?platformType=openshift){: external}, select the cluster for which you want to create a Sysdig monitoring configuration.
     2. On the cluster **Overview** page, click **Connect**.
     3. Select the region and the {{site.data.keyword.mon_full_notm}} service instance that you created earlier, and click **Connect**.

   - **From the CLI: **
     1. Create the Sysdig monitoring configuration. When you create the Sysdig monitoring configuration, the access key that was last added is retrieved automatically. If you want to use a different access key, add the `--sysdig-access-key <access_key>` option to the command.

        ```
        ibmcloud ob monitoring config create --cluster <cluster_name_or_ID> --instance <Sysdig_instance_name_or_ID>
        ```
        {: pre}

        Example output:
        ```
        Creating configuration...
        OK
        ```
        {: screen}

     2. Verify that the monitoring configuration was added to your cluster.
        ```
        ibmcloud ob monitoring config list --cluster <cluster_name_or_ID>
        ```
        {: pre}

        Example output:
        ```
        Listing configurations...

        OK
        Instance Name                            Instance ID                            CRN   
        IBM Cloud Monitornig with Sysdig-aaa     1a111a1a-1111-11a1-a1aa-aaa11111a11a   crn:v1:prod:public:sysdig:us-south:a/a11111a1aaaaa11a111aa11a1aa1111a:1a111a1a-1111-11a1-a1aa-aaa11111a11a::  
        ```
        {: screen}

3. Optional: Verify that the Sysdig agent was set up successfully.
   1. If you used the console to create the Sysdig monitoring configuration, log in to your cluster. For more information, see [Access your OpenShift cluster](/docs/openshift?topic=openshift-access_cluster).
   2. Verify that the daemonset for the Sysdig agent was created and all instances are listed as `AVAILABLE`.
      ```
      oc get daemonsets -n ibm-observe
      ```
      {: pre}

      Example output:
      ```
      NAME           DESIRED   CURRENT   READY   UP-TO-DATE   AVAILABLE   NODE SELECTOR   AGE
      sysdig-agent   9         9         9       9            9           <none>          14m
      ```
      {: screen}

      The number of daemonset instances that are deployed equals the number of worker nodes in your cluster.

   3. Review the configmap that was created for your Sysdig agent.
      ```
      oc describe configmap -n ibm-observe
      ```
      {: pre}

4. Access the metrics for your pods and cluster from the Sysdig dashboard.
   1. From the [Red Hat OpenShift on IBM Cloud console](https://cloud.ibm.com/kubernetes/clusters?platformType=openshift){: external}, select the cluster that you configured.
   2. On the cluster **Overview** page, click **Launch**. The Sysdig dashboard opens.
   3. Review the pod and cluster metrics that the Sysdig agent collected from your cluster. It might take a few minutes for your first metrics to show.

5. Review how you can work with the [Sysdig dashboard](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-dashboards#dashboards) to further analyze your metrics.


## Using the cluster logging operator
{: #oc_logging_operator}

To deploy the [OpenShift Container Platform cluster logging operator](https://docs.openshift.com/container-platform/4.3/logging/cluster-logging.html){: external} on your Red Hat OpenShift on IBM Cloud cluster, you must modify the default path to collect container logs. Container logs in Red Hat OpenShift on IBM Cloud clusters are located in the `/var/data` directory.
{: shortdesc}

### Installing the cluster logging operator
{: #oc_logging_operator_install}

1.  [Access your OpenShift cluster](/docs/openshift?topic=openshift-access_cluster).
2.  Create the `openshift-logging` project that is used by the cluster logging operator.
    ```
    oc create ns openshift-logging
    ```
    {: pre}
3.  Label the project with the tag that the cluster logging operator uses.
    ```
    oc label ns openshift-logging openshift.io/cluster-monitoring="true"
    ```
    {: pre}
4.  [Install the **Elasticsearch Operator** operator from the OperatorHub in your cluster](https://docs.openshift.com/container-platform/4.3/operators/olm-adding-operators-to-cluster.html){: external}.
    1.  From the OpenShift web console **Administrator** perspective, click **Operators > OperatorHub**.
    2.  In the **Filter by keyword** field, enter `Elasticsearch Operator`, click **Elasticsearch Operator**, then click **Install**.
    3.  Confirm the **Update Channel** matches your cluster version, then click **Subscribe**.
    4.  Wait until the Elasticsearch Operator status is successfully installed.
5.  Install the **Cluster logging** operator from the OperatorHub in your cluster.
    1.  From the OpenShift web console **Administrator** perspective, click **Operators > OperatorHub**.
    2.  In the **Filter by keyword** field, enter `Cluster Logging`, click **Cluster Logging**, then click **Install**.
    3.  For **Installation Mode**, click **A specific namespace on the cluster**.
    4.  From the project dropdown list, select **openshift-logging**.
    5.  Confirm the **Update Channel** matches your cluster version, then click **Subscribe**.
    6.  Wait until the Cluster Logging Operator status is successfully installed.
6.  Create an instance of cluster logging.
    1.  From the OpenShift web console **Installed Operators** page, click **Cluster Logging**.
    2.  In the **Provided APIs** section, **Cluster Logging** tile, click **Create Instance**.
    3.  Modify the configuration YAML to change the storage class for the Elasticsearch log storage from `gp2` to `ibmc-block-gold`.
        ```
        ...
            elasticsearch:
              nodeCount: 3
              redundancyPolicy: SingleRedundancy
              storage:
                storageClassName: ibmc-block-gold
                size: 200G
        ...
        ```
        {: copyblock}
    4.  Click **Create**.
    5.  Verify that the operator, Elasticsearch, Fluentd, and Kibana pods are all **Running**.
7.  Update the default value of the container logs in the Fluentd daemon set.
    1.  Change your cluster logging instance management state to `unmanaged` by following the [OpenShift documentation](https://docs.openshift.com/container-platform/4.3/logging/config/cluster-logging-management.html#cluster-logging-management-state-changing_cluster-logging-curator){: external}. By making the cluster logging instance unmanaged, you are able to update component configurations so that they are not overwritten. Do **not** change the Elasticsearch management state.
    2.  From the OpenShift console `openshift-logging` project, click **Workloads > Daemon Sets**, and click the **Fluentd** daemon set.
    3.  In the `volumeMounts` section, add the `/var/data` container log path to the mount path.
        ```
        volumeMounts:
        - mountPath: /var/data
          name: vardata
        ```
        {: codeblock}
    4.  In the `volumes` section, add the `/var/data` container log path to the host path.
        ```
        volumes:
        - hostPath:
            path: /var/data/
            type: ""
          name: vardata
        ```
        {: codeblock}
    5.  Apply your changes and wait for the Fluentd pods to re-create.
8.  Verify that container logs are sent to Elasticsearch by checking the Kibana console.
    1.  From the OpenShift console `openshift-logging` project, click **Networking > Routers**, and click the **Kibana** route.
    2.  In the Kibana console that opens, confirm that you see logs for containers.

### Uninstalling the cluster logging operator
{: #oc_logging_operator_remove}

If you remove the cluster logging operator, the `openshift-logging` project and custom resource definitions (CRDs) still exist. You must delete the project and CRDs.
{: shortdesc}

1.  [Access your OpenShift cluster](/docs/openshift?topic=openshift-access_cluster).
2.  Uninstall the cluster logging operator from the cluster. For instructions, see the [OpenShift documentation](https://docs.openshift.com/container-platform/4.3/operators/olm-deleting-operators-from-cluster.html){: external}.
3.  Uninstall the cluster logging operator from the cluster. For instructions, see the [OpenShift documentation](https://docs.openshift.com/container-platform/4.3/operators/olm-deleting-operators-from-cluster.html){: external}.
4.  Delete the `openshift-logging` project.
    ```
    oc delete ns openshift-logging
    ```
    {: pre}
5.  Delete the cluster logging and Elasticsearch CRDs.
    ```
    oc delete crd clusterloggings.logging.openshift.io
    ```
    {: pre}

    ```
    oc delete crd elasticsearches.logging.openshift.io 
    ```
    {: pre}
