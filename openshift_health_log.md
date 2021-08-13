---

copyright:
  years: 2014, 2021
lastupdated: "2021-08-13"

keywords: oks, iro, openshift, red hat, red hat openshift, rhos, roks, rhoks

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
{:audio: .audio}
{:authenticated-content: .authenticated-content}
{:beta: .beta}
{:c#: .ph data-hd-programlang='c#'}
{:c#: data-hd-programlang="c#"}
{:cli: .ph data-hd-interface='cli'}
{:codeblock: .codeblock}
{:curl: #curl .ph data-hd-programlang='curl'}
{:curl: .ph data-hd-programlang='curl'}
{:deprecated: .deprecated}
{:dotnet-standard: .ph data-hd-programlang='dotnet-standard'}
{:download: .download}
{:external: .external target="_blank"}
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
{:java: #java .ph data-hd-programlang='java'}
{:java: .ph data-hd-programlang='java'}
{:java: data-hd-programlang="java"}
{:javascript: .ph data-hd-programlang='javascript'}
{:javascript: data-hd-programlang="javascript"}
{:middle: .ph data-hd-position='middle'}
{:navgroup: .navgroup}
{:new_window: target="_blank"}
{:node: .ph data-hd-programlang='node'}
{:note: .note}
{:objectc: .ph data-hd-programlang='Objective C'}
{:objectc: data-hd-programlang="objectc"}
{:org_name: data-hd-keyref="org_name"}
{:php: .ph data-hd-programlang='PHP'}
{:php: data-hd-programlang="php"}
{:pre: .pre}
{:preview: .preview}
{:python: .ph data-hd-programlang='python'}
{:python: data-hd-programlang="python"}
{:right: .ph data-hd-position='right'}
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
{:step: data-tutorial-type='step'} 
{:subsection: outputclass="subsection"}
{:support: data-reuse='support'}
{:swift: #swift .ph data-hd-programlang='swift'}
{:swift: .ph data-hd-programlang='swift'}
{:swift: data-hd-programlang="swift"}
{:table: .aria-labeledby="caption"}
{:term: .term}
{:terraform: .ph data-hd-interface='terraform'}
{:tip: .tip}
{:tooling-url: data-tooling-url-placeholder='tooling-url'}
{:topicgroup: .topicgroup}
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

 
 


# Logging for clusters
{: #health}

For cluster and app logs, {{site.data.keyword.openshiftlong}} clusters include built-in tools to help you manage the health of your single cluster instance. You can also set up {{site.data.keyword.cloud_notm}} tools for multi-cluster analysis or other use cases, such as {{site.data.keyword.containerlong_notm}} add-ons: {{site.data.keyword.la_full_notm}} and {{site.data.keyword.mon_full_notm}}.
{: shortdesc}

## Understanding options for logging
{: #oc_logmet_options}

To help understand when to use the built-in {{site.data.keyword.openshiftshort}} tools or {{site.data.keyword.cloud_notm}} integrations, review the following information.
{: shortdesc}

<dl>

<dt>{{site.data.keyword.la_full_notm}}</dt>
<dd><ul>
<li>Customizable user interface for live streaming of log tailing, real-time troubleshooting issue alerts, and log archiving.</li>
<li>Quick integration with the cluster via a script.</li>
<li>Aggregated logs across clusters and cloud providers.</li>
<li>Historical access to logs that is based on the plan you choose.</li>
<li>Highly available, scalable, and compliant with industry security standards.</li>
<li>Integrated with {{site.data.keyword.cloud_notm}} IAM for user access management.</li>
<li>Flexible plans, including a free `Lite` option.</li></ul>
<br>To get started, see [Forwarding cluster and app logs to {{site.data.keyword.la_full_notm}}](#openshift_logging).</dd>

<dt>Built-in {{site.data.keyword.openshiftshort}} logging tools</dt>
<dd><ul>
<li>Built-in view of pod logs in the {{site.data.keyword.openshiftshort}} web console.</li>
<li>Built-in pod logs are not configured with persistent storage. You must integrate with a cloud database to back up the logging data and make it highly available, and manage the logs yourself.</li></ul>
<p class="note"><img src="images/icon-version-311.png" alt="Version 3.11 icon" width="30" style="width:30px; border-style: none"/> **{{site.data.keyword.openshiftshort}} 3.11**: You cannot run the Ansible playbook to deploy the [OpenShift Container Platform Elasticsearch, Fluentd, and Kibana EFK stack ![External link icon](../icons/launch-glyph.svg "External link icon")](https://docs.openshift.com/container-platform/3.11/install_config/aggregate_logging.html) because you cannot modify the default configuration of the {{site.data.keyword.openshiftlong_notm}} cluster.</p>
<p class="note"><img src="images/icon-version-43.png" alt="Version 4 icon" width="30" style="width:30px; border-style: none"/> **{{site.data.keyword.openshiftshort}} 4**: To set up an [OpenShift Container Platform Elasticsearch, Fluentd, and Kibana EFK stack ![External link icon](../icons/launch-glyph.svg "External link icon")](https://docs.openshift.com/container-platform/4.6/logging/cluster-logging.html), see [installing the cluster logging operator](#oc_logging_operator). Keep in mind that your worker nodes must have at least 4 cores and GB memory to run the cluster logging stack.</p>
</dd>

<dt>Service logs: {{site.data.keyword.at_full}}</dt>
<dd>Use {{site.data.keyword.at_full_notm}} to view cluster management events that are generated by the {{site.data.keyword.openshiftlong_notm}} API. To access these logs, [provision an instance of {{site.data.keyword.at_full_notm}}](/docs/activity-tracker?topic=activity-tracker-getting-started). For more information about the types of {{site.data.keyword.containerlong_notm}} events that you can track, see [Activity Tracker events](/docs/openshift?topic=openshift-at_events).</dd>

<dt>API server logs: {{site.data.keyword.la_full_notm}}</dt>
<dd><ul>
<li>Customizable user interface for live streaming of log tailing, real-time troubleshooting issue alerts, and log archiving.</li>
<li>Quick integration with the cluster via a script.</li>
<li>Aggregated logs across clusters and cloud providers.</li>
<li>Historical access to logs that is based on the plan you choose.</li>
<li>Highly available, scalable, and compliant with industry security standards.</li>
<li>Integrated with {{site.data.keyword.cloud_notm}} IAM for user access management.</li>
<li>Flexible plans, including a free `Lite` option.</li></ul>
<br>To get started, see [Forwarding Kubernetes API audit logs to {{site.data.keyword.la_short}}](/docs/openshift?topic=openshift-health-audit).<p class="note">Forwarding Kubernetes API audit logs to {{site.data.keyword.la_short}} is not supported for version 3.11 clusters.</dd>

<dt>Built-in {{site.data.keyword.openshiftshort}} audit logging tools</dt>
<dd>API audit logging to monitor user-initiated activities is currently not supported.</dd>

</dl>

<br />

## Forwarding cluster and app logs to {{site.data.keyword.la_full_notm}}
{: #openshift_logging}

Use the {{site.data.keyword.openshiftlong_notm}} observability plug-in to create a logging configuration for {{site.data.keyword.la_full_notm}} in your cluster, and use this logging configuration to automatically collect and forward pod logs to {{site.data.keyword.la_full_notm}}.
{: shortdesc}

Considerations for using the {{site.data.keyword.openshiftlong_notm}} observability plug-in:
* You can have only one logging configuration for {{site.data.keyword.la_full_notm}} in your cluster at a time. If you want to use a different {{site.data.keyword.la_full_notm}} service instance to send logs to, use the [`ibmcloud ob logging config replace`](/docs/containers?topic=containers-observability_cli#logging_config_replace) command.
* {{site.data.keyword.openshiftshort}} clusters in {{site.data.keyword.satelliteshort}} cannot currently use the {{site.data.keyword.openshiftlong_notm}} console or the observability plug-in CLI to enable logging for {{site.data.keyword.satelliteshort}} clusters. You must manually deploy logging agents to your cluster to forward logs to {{site.data.keyword.la_short}}.
* If you created a {{site.data.keyword.la_short}} configuration in your cluster without using the {{site.data.keyword.openshiftlong_notm}} observability plug-in, you can use the [`ibmcloud ob logging agent discover`](/docs/containers?topic=containers-observability_cli#logging_agent_discover) command to make the configuration visible to the plug-in. Then, you can use the observability plug-in commands and functionality in the {{site.data.keyword.cloud_notm}} console to manage the configuration.

Before you begin:
- Verify that you are assigned the **Editor** platform access role and **Manager** server access role for {{site.data.keyword.la_full_notm}}.
- Verify that you are assigned the **Administrator** platform access role and the **Manager** service access role for all Kubernetes namespaces in {{site.data.keyword.containerlong_notm}} to create the logging configuration. To view a logging configuration or launch the {{site.data.keyword.la_short}} dashboard after the logging configuration is created, users must be assigned the **Administrator** platform access role and the **Manager** service access for the `ibm-observe` Kubernetes namespace in {{site.data.keyword.containerlong_notm}}.
- If you want to use the CLI to set up the logging configuration:
  - [Install the {{site.data.keyword.openshiftlong_notm}} observability CLI plug-in (`ibmcloud ob`)](/docs/containers?topic=containers-cs_cli_install#cs_cli_install_steps).
  - [Access your {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-access_cluster).

To set up a logging configuration for your cluster:

1. Create an [{{site.data.keyword.la_full_notm}} service instance](/docs/log-analysis?topic=log-analysis-provision) and note the name of the instance. The service instance must belong to the same {{site.data.keyword.cloud_notm}} account where you created your cluster, but can be in a different resource group and {{site.data.keyword.cloud_notm}} region than your cluster.
2. Set up a logging configuration for your cluster. When you create the logging configuration, an {{site.data.keyword.openshiftshort}} project `ibm-observe` is created and a {{site.data.keyword.la_short}} agent is deployed as a daemon set to all worker nodes in your cluster. This agent collects logs with the extension `*.log` and extensionless files that are stored in the `/var/log` directory of your pod from all projects, including `kube-system`. The agent then forwards the logs to the {{site.data.keyword.la_full_notm}} service.

   - **From the console:**
     1. From the [{{site.data.keyword.openshiftshort}} clusters console](https://cloud.ibm.com/kubernetes/clusters?platformType=openshift){: external}, select the cluster for which you want to create a {{site.data.keyword.la_short}} configuration.
     2. On the cluster **Overview** page, click **Connect**.
     3. Select the region and the {{site.data.keyword.la_full_notm}} service instance that you created earlier, and click **Connect**.

   - **From the CLI:**
     1.  Create the {{site.data.keyword.la_short}} configuration. When you create the {{site.data.keyword.la_short}} configuration, the ingestion key that was last added is retrieved automatically. If you want to use a different ingestion key, add the `--logdna-ingestion-key <ingestion_key>` option to the command.

         To use a different ingestion key after you created your logging configuration, use the [`ibmcloud ob logging config replace`](/docs/containers?topic=containers-observability_cli#logging_config_replace) command.
         {: tip}

         ```
         ibmcloud ob logging config create --cluster <cluster_name_or_ID> --instance <Log_Analysis_instance_name_or_ID>
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
        Instance Name                Instance ID                            CRN   
        IBM Cloud Log Analysis-opm   1a111a1a-1111-11a1-a1aa-aaa11111a11a   crn:v1:prod:public:logdna:us-south:a/a11111a1aaaaa11a111aa11a1aa1111a:1a111a1a-1111-11a1-a1aa-aaa11111a11a::  
        ```
        {: screen}

3. Optional: Verify that the {{site.data.keyword.la_short}} agent was set up successfully.
   1. If you used the console to create the {{site.data.keyword.la_short}} configuration, log in to your cluster. For more information, see [Access your {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-access_cluster)..

   2. Verify that the daemon set for the {{site.data.keyword.la_short}} agent was created and all instances are listed as `AVAILABLE`.
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

      The number of daemon set instances that are deployed equals the number of worker nodes in your cluster.

   3. Review the configmap that was created for your {{site.data.keyword.la_short}} agent.
      ```
      oc describe configmap -n ibm-observe
      ```
      {: pre}

4. Access the logs for your pods from the {{site.data.keyword.la_short}} dashboard.
   1. From the [{{site.data.keyword.openshiftshort}} clusters console](https://cloud.ibm.com/kubernetes/clusters?platformType=openshift){: external}, select the cluster that you configured.  
   2. On the cluster **Overview** page, click **Launch**. The {{site.data.keyword.la_short}} dashboard opens.
   3. Review the pod logs that the {{site.data.keyword.la_short}} agent collected from your cluster. It might take a few minutes for your first logs to show.

5. Review how you can [search and filter logs in the {{site.data.keyword.la_short}} dashboard](/docs/log-analysis?topic=log-analysis-view_logs).

<br />

## Using the cluster logging operator
{: #oc_logging_operator}

To deploy the OpenShift Container Platform cluster logging operator and stack on your {{site.data.keyword.openshiftlong_notm}} cluster, see the [{{site.data.keyword.openshiftshort}} documentation](https://docs.openshift.com/container-platform/4.6/logging/cluster-logging.html){: external}. Additionally, you must update the cluster logging instance to use an {{site.data.keyword.cloud_notm}} Block Storage storage class.
{: shortdesc}

1.  Prepare your worker pool to run the operator.
    1.  Create a [VPC](/docs/openshift?topic=openshift-add_workers#vpc_pools) or [classic](/docs/openshift?topic=openshift-add_workers#classic_pools) worker pool with a flavor of **at least 4 cores and 32 GB memory** and 3 worker nodes.
    2.  [Label the worker pool](/docs/openshift?topic=openshift-add_workers#worker_pool_labels).
    3.  [Taint the worker pool](/docs/openshift?topic=openshift-kubernetes-service-cli#worker_pool_taint) so that other workloads cannot run on the worker pool.
2.  [Access your {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-access_cluster).
3.  From the {{site.data.keyword.openshiftshort}} web console **Administrator** perspective, click **Operators > Installed Operators**.
4.  Click **Cluster Logging**.
5.  In the **Provided APIs** section, **Cluster Logging** tile, click **Create Instance**.
6.  Modify the configuration YAML to change the storage class for the ElasticSearch log storage from `gp2` to one of the following storage classes that vary with your cluster infrastructure provider.
    * **Classic clusters**: `ibmc-block-gold`
    * **VPC clusters**: `ibmc-vpc-block-10iops-tier`

    ```
    ...
        elasticsearch:
          nodeCount: 3
          redundancyPolicy: SingleRedundancy
          storage:
            storageClassName: ibmc-block-gold #or ibmc-vpc-block-10iops-tier for VPC clusters
            size: 200G
    ...
    ```
    {: copyblock}
7.  Modify the configuration YAML to include the node selector and toleration for the worker pool label and taint that you previously created. For more information and examples, see the following {{site.data.keyword.openshiftshort}} documents. The examples use a label and toleration of `logging: clo-efk`.
    * [Node selector](https://docs.openshift.com/container-platform/4.6/logging/config/cluster-logging-moving-nodes.html){: external}. Add the node selector to the Elasticsearch (`logstore`)and Kibana (`visualization`), and Fluentd (`collector.logs`) pods.
      ```
      spec:
        logStore:
          elasticsearch:
            nodeSelector:
              logging: clo-efk
        ...
        visualization:
          kibana:
            nodeSelector:
              logging: clo-efk
        ...
        collection:
          logs:
            fluentd:
              nodeSelector:
                logging: clo-efk
      ```
      {: codeblock}
    * [Toleration](https://docs.openshift.com/container-platform/4.6/logging/config/cluster-logging-tolerations.html){: external}. Add the node selector to the Elasticsearch (`logstore`)and Kibana (`visualization`), and Fluentd (`collector.logs`) pods.
      ```
      spec:
        logStore:
          elasticsearch:
            tolerations:
            - key: app
              value: clo-efk
              operator: "Exists"
              effect: "NoExecute"
        ...
        visualization:
          kibana:
            tolerations:
            - key: app
              value: clo-efk
              operator: "Exists"
              effect: "NoExecute"
        ...
        collection:
          logs:
            fluentd:
              tolerations:
              - key: app
                value: clo-efk
                operator: "Exists"
                effect: "NoExecute"
      ```
      {: codeblock}
8.  Click **Create**.
9.  Verify that the operator, Elasticsearch, Fluentd, and Kibana pods are all **Running**.
