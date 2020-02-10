---

copyright:
  years: 2014, 2020
lastupdated: "2020-02-10"

keywords: oks, iro, openshift, red hat, red hat openshift, rhos, roks, rhoks

subcollection: openshift

---

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
          <br>To get started, see [Setting up LogDNA](#openshift_logdna).</td>
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
          Use {{site.data.keyword.at_full_notm}} to view cluster management events that are generated by the Red Hat OpenShift on IBM Cloud API. To access these logs, [provision an instance of {{site.data.keyword.at_full_notm}}](/docs/Activity-Tracker-with-LogDNA?topic=logdnaat-getting-started). For more information about the types of {{site.data.keyword.containerlong_notm}} events that you can track, see [Activity Tracker events](/docs/openshift?topic=containers-at_events).</td>
    </tr>
    <tr>
        <td>**Monitoring**</td>
        <td>**Built-in OpenShift monitoring tools**:<ul>
          <li>Built-in Prometheus and Grafana deployments in `openshift-monitoring` project for cluster metrics.</li>
          <li>At-a-glance, real-time view of how your pods consume cluster resources that can be accessed from the OpenShift **Cluster Console**.</li>
          <li>Monitoring is on a per-cluster basis.</li>
          <li>The `openshift-monitoring` project stack is set up in a single zone only. No persistent storage is available to back up or view metric history.</li></ul>
          <br>For more information, see [the OpenShift documentation ![External link icon](../icons/launch-glyph.svg "External link icon")](https://docs.openshift.com/container-platform/4.3/monitoring/cluster-monitoring/about-cluster-monitoring.html).</td>
        <td>**{{site.data.keyword.mon_full_notm}}**:<ul>
          <li>Customizable user interface for a unified look at your cluster metrics, container security, resource usage, alerts, and custom events.</li>
          <li>Quick integration with the cluster via a script.</li>
          <li>Aggregated metrics and container monitoring across clusters and cloud providers for consistent operations enablement.</li>
          <li>Historical access to metrics that is based on the timeline and plan, and ability to capture and download trace files.</li>
          <li>Highly available, scalable, and compliant with industry security standards.</li>
          <li>Integrated with {{site.data.keyword.cloud_notm}} IAM for user access management.</li>
          <li>Free trial to try out the capabilities.</li></ul>
          <br>To get started, see [Setting up Sysdig](#openshift_sysdig).</td>
    </tr>
    </tbody>
</table>

<br />


## Setting up LogDNA and Sysdig add-ons to monitor cluster health
{: #openshift_logdna_sysdig}

Because OpenShift sets up stricter [Security Context Constraints (SCC)](https://docs.openshift.com/container-platform/4.3/authentication/managing-security-context-constraints.html){: external} by default than community Kubernetes, you might find that some apps or cluster add-ons that you use on community Kubernetes cannot be deployed on OpenShift in the same way. In particular, many images must run as a `root` user or as a privileged container, which is prevented in OpenShift by default. You can modify the default SCCs by creating privileged security accounts and updating the `securityContext` in the pod specification to use two popular {{site.data.keyword.containerlong_notm}} add-ons: {{site.data.keyword.la_full_notm}} and {{site.data.keyword.mon_full_notm}}.
{: shortdesc}

### Setting up logging with LogDNA
{: #openshift_logdna}

Set up logging in your OpenShift cluster with {{site.data.keyword.la_full_notm}}. When you deploy the LogDNA agent, it collects logs with the extension `*.log` and extensionless files that are stored in the `/var/log` directory of your pod. By default, logs are collected from all namespaces, including `kube-system`, and automatically forwarded to the {{site.data.keyword.la_short}} service.
{: shortdesc}

In the following steps, you set up a project and privileged service account for {{site.data.keyword.la_full_notm}}. Then, create a {{site.data.keyword.la_short}} instance in your {{site.data.keyword.cloud_notm}} account. To integrate your {{site.data.keyword.la_short}} instance with your OpenShift cluster, you must modify the daemon set that is deployed to use the privileged service account to run as root.

**Before you begin**:

* You must have the following permissions:
  * [**Administrator** {{site.data.keyword.cloud_notm}} IAM platform role](/docs/containers?topic=containers-users#platform) for the cluster.
  * [**Administrator** {{site.data.keyword.cloud_notm}} IAM platform role](/docs/iam?topic=iam-userroles) for {{site.data.keyword.la_full_notm}}.
* For the cluster that you want to collect API server audit logs from: [Log in to your account. If applicable, target the appropriate resource group. Set the context for your cluster.](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure)

**To set up {{site.data.keyword.la_full_notm}}:**

1.  Follow the [{{site.data.keyword.la_full_notm}} documentation](/docs/Log-Analysis-with-LogDNA?topic=LogDNA-config_agent_os_cluster) to set up the OpenShift project, the service account, and the LogDNA agent in your cluster.
2.  Access your logs from the LogDNA dashboard.
    1. From the [{{site.data.keyword.cloud_notm}} **Observability > Logging** console](https://cloud.ibm.com/observe/logging), in the row for your {{site.data.keyword.la_short}} instance, click **View LogDNA**. The LogDNA dashboard opens.
    2. Wait a few minutes for your logs to display.

For more information about how to use {{site.data.keyword.la_short}}, see the [Next steps docs](/docs/Log-Analysis-with-LogDNA?topic=LogDNA-kube#kube_next_steps).

<br />


### Setting up API audit log forwarding to LogDNA
{: #openshift_logdna_audit}

Collect and forward any events that are passed through your Kubernetes API server to {{site.data.keyword.la_full_notm}}.
{: shortdesc}

In the following steps, you create an audit system in your cluster that consists of an audit webhook, a log collection service and webserver app, and a logging agent. The webhook collects the Kubernetes API server events from your cluster master. The log collection service is a Kubernetes `ClusterIP` service that is created from an image from the public {{site.data.keyword.cloud_notm}} registry. This service exposes a simple `node.js` HTTP webserver app that is exposed only on the private network. The webserver app parses the log data from the audit webhook and creates each log as a unique JSON line. Finally, the logging agent forwards the logs from the webserver app to {{site.data.keyword.la_full_notm}}, where you can view the logs.

To see how the audit webhook collects logs, check out the {{site.data.keyword.containerlong_notm}} [`kube-audit` policy](https://github.com/IBM-Cloud/kube-samples/blob/master/kube-audit/kube-audit-policy.yaml){: external}.

You cannot modify the default `kube-audit` policy or apply your own custom policy.
{: note}

**Before you begin**:

* You must have the following permissions:
  * [**Administrator** {{site.data.keyword.cloud_notm}} IAM platform role](/docs/containers?topic=containers-users#platform) for the cluster.
  * [**Administrator** {{site.data.keyword.cloud_notm}} IAM platform role](/docs/iam?topic=iam-userroles) for {{site.data.keyword.la_full_notm}}.
* For the cluster that you want to collect API server audit logs from: [Log in to your account. If applicable, target the appropriate resource group. Set the context for your cluster.](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure)
* Keep in mind that only one audit webhook can be created in a cluster.

**To forward Kubernetes API audit logs to {{site.data.keyword.la_full_notm}}:**

1. [Set up a {{site.data.keyword.la_full_notm}} instance and configure the LogDNA agent in your cluster](#openshift_logdna).

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


### Setting up monitoring with Sysdig
{: #openshift_sysdig}

Create an {{site.data.keyword.mon_full_notm}} instance in your {{site.data.keyword.cloud_notm}} account. To integrate your {{site.data.keyword.mon_short}} instance with your OpenShift cluster, you must run a script that creates a project and privileged service account for the Sysdig agent.
{: shortdesc}

**Before you begin**:

* You must have the following permissions:
  * [**Administrator** {{site.data.keyword.cloud_notm}} IAM platform role](/docs/containers?topic=containers-users#platform) for the cluster.
  * [**Administrator** {{site.data.keyword.cloud_notm}} IAM platform role](/docs/iam?topic=iam-userroles) for {{site.data.keyword.mon_full_notm}}.
* For the cluster that you want to collect API server audit logs from: [Log in to your account. If applicable, target the appropriate resource group. Set the context for your cluster.](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure)

**To set up {{site.data.keyword.mon_full_notm}}:**

1.  Create your {{site.data.keyword.mon_full_notm}} instance in the same resource group as your cluster. Select a pricing plan that determines the retention period for your logs, such as `lite`. The region does not have to match the region of your cluster. For more information, see [Provisioning an instance](/docs/Monitoring-with-Sysdig?topic=Sysdig-provision).
    ```
    ibmcloud resource service-instance-create <service_instance_name> sysdig-monitor (lite|graduated-tier) <region> [-g <resource_group>]
    ```
    {: pre}

    Example command:
    ```
    ibmcloud resource service-instance-create sysdig-openshift sysdig-monitor lite us-south
    ```
    {: pre}

    In the output, note the service instance **ID**, which is in the format `crn:v1:bluemix:public:logdna:<region>:<ID_string>::`.
    ```
    Service instance <name> was created.

    Name:         <name>   
    ID:           crn:v1:bluemix:public:sysdig-monitor:<region>:<ID_string>::   
    GUID:         <guid>   
    Location:     <region>   
    ...
    ```
    {: screen}    
2.  Get your {{site.data.keyword.mon_short}} instance access key. The Sysdig access key is used to open a secure web socket to the Sysdig ingestion server and to authenticate the monitoring agent with the {{site.data.keyword.mon_short}} service.
    1.  Create a service key for your Sysdig instance.
        ```
        ibmcloud resource service-key-create <key_name> Administrator --instance-id <sysdig_instance_ID>
        ```
        {: pre}
    2.  Note the **Sysdig Access Key** and **Sysdig Collector Endpoint** of your service key.
        ```
        ibmcloud resource service-key <key_name>
        ```
        {: pre}

        Example output:
        ```
        Name:          <key_name>  
        ID:            crn:v1:bluemix:public:sysdig-monitor:<region>:<ID_string>::    
        Created At:    Thu Jun  6 21:31:25 UTC 2019   
        State:         active   
        Credentials:                                   
                       Sysdig Access Key:           11a1aa11-aa1a-1a1a-a111-11a11aa1aa11      
                       Sysdig Collector Endpoint:   ingest.<region>.monitoring.cloud.ibm.com      
                       Sysdig Customer Id:          11111      
                       Sysdig Endpoint:             https://<region>.monitoring.cloud.ibm.com  
                       apikey:                   <api_key_value>      
                       iam_apikey_description:   Auto-generated for key <ID>     
                       iam_apikey_name:          <key_name>       
                       iam_role_crn:             crn:v1:bluemix:public:iam::::role:Administrator      
                       iam_serviceid_crn:        crn:v1:bluemix:public:iam-identity::<ID_string>       
        ```
        {: screen}
3.  Run the script to set up an `ibm-observe` project with a privileged service account and a Kubernetes daemon set to deploy the Sysdig agent on every worker node of your Kubernetes cluster. The Sysdig agent collects metrics such as the worker node CPU usage, worker node memory usage, HTTP traffic to and from your containers, and data about several infrastructure components.

    In the following command, replace <code>&lt;sysdig_access_key&gt;</code> and <code>&lt;sysdig_collector_endpoint&gt;</code> with the values from the service key that you created earlier. For <code>&lt;tag&gt;</code>, you can associate tags with your Sysdig agent, such as `role:service,location:us-south` to help you identify the environment that the metrics come from.

    ```
    curl -sL https://ibm.biz/install-sysdig-k8s-agent | bash -s -- -a <sysdig_access_key> -c <sysdig_collector_endpoint> -t <tag> -ac 'sysdig_capture_enabled: false' --openshift
    ```
    {: pre}

    Example output:
    ```
    * Detecting operating system
    * Downloading Sysdig cluster role yaml
    * Downloading Sysdig config map yaml
    * Downloading Sysdig daemonset v2 yaml
    * Creating project: ibm-observe
    * Creating sysdig-agent serviceaccount in project: ibm-observe
    * Creating sysdig-agent access policies
    * Creating sysdig-agent secret using the ACCESS_KEY provided
    * Retreiving the IKS Cluster ID and Cluster Name
    * Setting cluster name as <cluster_name>
    * Setting ibm.containers-kubernetes.cluster.id 1fbd0c2ab7dd4c9bb1f2c2f7b36f5c47
    * Updating agent configmap and applying to cluster
    * Setting tags
    * Setting collector endpoint
    * Adding additional configuration to dragent.yaml
    * Enabling Prometheus
    configmap/sysdig-agent created
    * Deploying the sysdig agent
    daemonset.extensions/sysdig-agent created
    ```
    {: screen}

4.  Verify that the `sydig-agent` pods on each node show that **1/1** pods are ready and that each pod has a **Running** status.
    ```
    oc get pods
    ```
    {: pre}

    Example output:
    ```
    NAME                 READY     STATUS    RESTARTS   AGE
    sysdig-agent-qrbcq   1/1       Running   0          1m
    sysdig-agent-rhrgz   1/1       Running   0          1m
    ```
    {: screen}
5.  From the [{{site.data.keyword.cloud_notm}} **Observability > Monitoring** console](https://cloud.ibm.com/observe/logging), in the row for your {{site.data.keyword.mon_short}} instance, click **View Sysdig**. The Sysdig dashboard opens, and you can analyze your cluster metrics.

For more information about how to use {{site.data.keyword.mon_short}}, see the [Next steps docs](/docs/Monitoring-with-Sysdig?topic=Sysdig-kubernetes_cluster#kubernetes_cluster_next_steps).

<br />


### Optional: Cleaning up
{: #openshift_logdna_sysdig_cleanup}

Remove the {{site.data.keyword.la_short}} and {{site.data.keyword.mon_short}} instances from your cluster and {{site.data.keyword.cloud_notm}} account. Note that unless you store the logs and metrics in [persistent storage](/docs/Log-Analysis-with-LogDNA?topic=LogDNA-archiving), you cannot access this information after you delete the instances from your account.
{: shortdesc}

1.  Clean up the {{site.data.keyword.la_short}} and {{site.data.keyword.mon_short}} instances in your cluster by removing the projects that you created for them. When you delete a project, its resources such as service accounts and daemon sets are also removed.
    ```
    oc delete project logdna-agent
    ```
    {: pre}
    ```
    oc delete project ibm-observe
    ```
    {: pre}
2.  Remove the instances from your {{site.data.keyword.cloud_notm}} account.
    *   [Removing a {{site.data.keyword.la_short}} instance](/docs/Log-Analysis-with-LogDNA?topic=LogDNA-remove).
    *   [Removing a {{site.data.keyword.mon_short}} instance](/docs/Monitoring-with-Sysdig?topic=Sysdig-remove).

<br />


## Setting up {{site.data.keyword.cloud_notm}} logging and monitoring tools
{: #openshift_other_logmet}

For more information about other logging and monitoring tools that you can set up, including {{site.data.keyword.cloud_notm}} services, see the following topics in the {{site.data.keyword.containershort_notm}} docs.
{: shortdesc}

* [Choosing a logging solution](/docs/containers?topic=containers-health#logging_overview).
* [Choosing a monitoring solution](/docs/containers?topic=containers-health#view_metrics).



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
    5.  Apply your changes and wait for the Fluentd pods to recreate.
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

