---

copyright:
  years: 2014, 2020
lastupdated: "2020-08-06"

keywords: openshift, roks, rhoks, rhos, ingress, alb, health, prometheus

subcollection: openshift

---

{:DomainName: data-hd-keyref="APPDomain"}
{:DomainName: data-hd-keyref="DomainName"}
{:android: data-hd-operatingsystem="android"}
{:apikey: data-credential-placeholder='apikey'}
{:app_key: data-hd-keyref="app_key"}
{:app_name: data-hd-keyref="app_name"}
{:app_secret: data-hd-keyref="app_secret"}
{:app_url: data-hd-keyref="app_url"}
{:authenticated-content: .authenticated-content}
{:beta: .beta}
{:c#: data-hd-programlang="c#"}
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
{:java: #java .ph data-hd-programlang='java'}
{:java: .ph data-hd-programlang='java'}
{:java: data-hd-programlang="java"}
{:javascript: .ph data-hd-programlang='javascript'}
{:javascript: data-hd-programlang="javascript"}
{:new_window: target="_blank"}
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
{:swift: #swift .ph data-hd-programlang='swift'}
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
{:unity: .ph data-hd-programlang='unity'}
{:url: data-credential-placeholder='url'}
{:user_ID: data-hd-keyref="user_ID"}
{:vb.net: .ph data-hd-programlang='vb.net'}
{:video: .video}


# Logging and monitoring Ingress
{: #ingress_health}

Customize logging and set up monitoring to help you troubleshoot issues and improve the performance of your Ingress configuration.
{: shortdesc}

<img src="images/icon-version-311.png" alt="Version 3.11 icon" width="30" style="width:30px; border-style: none"/> This information is applicable to clusters that run OpenShift version 3.11 only. To learn about Ingress for OpenShift version 4, see [About Ingress in OpenShift version 4(/docs/openshift?topic=openshift-ingress-about-roks4).
{: important}

## Viewing Ingress logs
{: #ingress_logs}

If you want to troubleshoot your Ingress or monitor Ingress activity, you can review the Ingress logs.
{: shortdesc}

Logs are automatically collected for your Ingress ALBs. To view the ALB logs, choose between two options.
* [Create a logging configuration for the Ingress service](/docs/openshift?topic=openshift-health#oc_logmet_options) in your cluster.
* Check the logs from the CLI. **Note**: You must have at least the [**Reader** {{site.data.keyword.cloud_notm}} IAM service role](/docs/openshift?topic=openshift-users#platform) for the `kube-system` namespace.
    1. Get the ID of a pod for an ALB.
        ```
        oc get pods -n kube-system | grep alb
        ```
        {: pre}

    2. Open the logs for that ALB pod.
        ```
        oc logs <ALB_pod_ID> nginx-ingress -n kube-system
        ```
        {: pre}


</br>The default Ingress log content is formatted in JSON and displays common fields that describe the connection session between a client and your app. An example log with the default fields looks like the following:

```
{"time_date": "2018-08-21T17:33:19+00:00", "client": "108.162.248.42", "host": "albhealth.multizone.us-south.containers.appdomain.cloud", "scheme": "http", "request_method": "GET", "request_uri": "/", "request_id": "c2bcce90cf2a3853694da9f52f5b72e6", "status": 200, "upstream_addr": "192.168.1.1:80", "upstream_status": 200, "request_time": 0.005, "upstream_response_time": 0.005, "upstream_connect_time": 0.000, "upstream_header_time": 0.005}
```
{: screen}

|Field in the default Ingress log format|Value|
|---|---|
|"time_date": "$time_iso8601"|The local time in the ISO 8601 standard format when the log is written.|
|"client": "$remote_addr"|The IP address of the request package that the client sent to your app. This IP can change based on the following situations:When a client request to your app is sent to your cluster, the request is routed to a pod for the load balancer service that exposes the ALB. If no app pod exists on the same worker node as the load balancer service pod, the load balancer forwards the request to an app pod on a different worker node. The source IP address of the request package is changed to the public IP address of the worker node where the app pod is running.If [source IP preservation is enabled](/docs/openshift?topic=openshift-ingress-settings#preserve_source_ip), the original IP address of the client request to your app is recorded instead.|
|"host": "$http_host"|The host, or subdomain, that your apps are accessible through. This subdomain is configured in the Ingress resource files for your ALBs.|
|"scheme": "$scheme"|The kind of request: HTTP or HTTPS.|
|"request_method": "$request_method"|The method of the request call to the back-end app, such as GET or POST.|
|"request_uri": "$uri"|The original request URI to your app path. ALBs process the paths that apps listen on as prefixes. When an ALB receives a request from a client to an app, the ALB checks the Ingress resource for a path (as a prefix) that matches the path in the request URI.|
|"request_id": "$request_id"|A unique request identifier generated from 16 random bytes.|
|"status": $status|The status code for the connection session.<ul><li>`200`: Session completed successfully</li><li>`400`: Client data can't be parsed</li><li>`403`: Access forbidden; for example, when access is limited for certain client IP addresses</li><li>`500`: Internal server error</li><li>`502`: Bad gateway; for example, if an upstream server can't be selected or reached</li><li>`503`: Service unavailable; for example, when access is limited by the number of connections</li></ul>|
|"upstream_addr": "$upstream_addr"|The IP address and port or the path to the UNIX-domain socket of the upstream server. If several servers are contacted during request processing, their addresses are separated by commas: "192.168.1.1:80, 192.168.1.2:80, unix:/tmp/sock". If the request is redirected internally from one server group to another, then the server addresses from different groups are separated by colons: "192.168.1.1:80, 192.168.1.2:80, unix:/tmp/sock : 192.168.10.1:80, 192.168.10.2:80". If the ALB can't select a server, the name of the server group is logged instead.|
|"upstream_status": $upstream_status|The status code of the response obtained from the upstream server for the back-end app, such as standard HTTP response codes. Status codes of several responses are separated by commas and colons like addresses in the $upstream_addr variable. If the ALB can't select a server, the 502 (Bad Gateway) status code is logged.|
|"request_time": $request_time|The request processing time, which is measured in seconds with a milliseconds resolution. This time starts when the ALB reads the client request's first bytes and stops when the ALB sends the response's last bytes to the client. The log is written immediately after the request processing time stops.|
|"upstream_response_time": $upstream_response_time|The time that it takes the ALB to receive the response from the upstream server for the back-end app, which is measured in seconds with a milliseconds resolution. Times of several responses are separated by commas and colons.|
|"upstream_connect_time": $upstream_connect_time|The time that it takes the ALB to establish a connection with the upstream server for the back-end app, which is measured in seconds with a milliseconds resolution. If TLS/SSL is enabled in your Ingress resource configuration, this time includes time spent on the handshake. Times of several connections are separated by commas and colons.|
|"upstream_header_time": $upstream_header_time|The time that it takes the ALB to receive the response header from the upstream server for the back-end app, which is measured in seconds with a milliseconds resolution. Times of several connections are separated by commas and colons.|
{: caption="Understanding fields in the default Ingress log format" caption-side="top"}

## Customizing Ingress log content and format
{: #ingress_log_format}

You can customize the content and format of logs that are collected for the Ingress ALB.
{: shortdesc}

By default, Ingress logs are formatted in JSON and display common log fields. However, you can also create a custom log format by choosing which log components are forwarded and how the components are arranged in the log output

Before you begin, ensure that you have the [**Writer** or **Manager** {{site.data.keyword.cloud_notm}} IAM service role](/docs/openshift?topic=openshift-users#platform) for the `kube-system` namespace.

1. Edit the configuration file for the `ibm-cloud-provider-ingress-cm` configmap resource.

    ```
    oc edit cm ibm-cloud-provider-ingress-cm -n kube-system
    ```
    {: pre}

2. Add a `data` section. Add the `log-format` field and optionally, the `log-format-escape-json` field.

    ```yaml
    apiVersion: v1
    data:
      log-format: '{<key1>: <log_variable1>, <key2>: <log_variable2>, <key3>: <log_variable3>}'
      log-format-escape-json: "true"
    kind: ConfigMap
    metadata:
      name: ibm-cloud-provider-ingress-cm
      namespace: kube-system
    ```
    {: codeblock}

    <table>
    <caption>Understanding the log-format configuration</caption>
    <col width="25%">
    <thead>
    <th>Parameter</th>
    <th>Description</th>
    </thead>
    <tbody>
    <tr>
    <td>`log-format`</td>
    <td>Replace `&lt;key&gt;` with the name for the log component and `&lt;log_variable&gt;` with a variable for the log component that you want to collect in log entries. You can include text and punctuation that you want the log entry to contain, such as quotation marks around string values and commas to separate log components. For example, formatting a component like `request: "$request"` generates the following in a log entry: `request: "GET / HTTP/1.1"` . For a list of all the variables you can use, see the [NGINX variable index](http://nginx.org/en/docs/varindex.html).<br><br>To log an additional header such as <em>x-custom-ID</em>, add the following key-value pair to the custom log content: <br><pre class="codeblock"><code>customID: $http_x_custom_id</code></pre> <br>Hyphens (`-`) are converted to underscores (`_`) and `$http_` must be added as a prefix to the custom header name.</td>
    </tr>
    <tr>
    <td>`log-format-escape-json`</td>
    <td>Optional: By default, logs are generated in text format. To generate logs in JSON format, add the `log-format-escape-json` field and use value `true`.</td>
    </tr>
    </tbody></table>

    For example, your log format might contain the following variables:
    ```
    apiVersion: v1
    data:
      log-format: '{remote_address: $remote_addr, remote_user: "$remote_user",
                    time_date: [$time_local], request: "$request",
                    status: $status, http_referer: "$http_referer",
                    http_user_agent: "$http_user_agent",
                    request_id: $request_id}'
    kind: ConfigMap
    metadata:
      name: ibm-cloud-provider-ingress-cm
      namespace: kube-system
    ```
    {: screen}

    A log entry according to this format looks like the following example:
    ```
    remote_address: 127.0.0.1, remote_user: "dbmanager", time_date: [30/Mar/2018:18:52:17 +0000], request: "GET / HTTP/1.1", status: 401, http_referer: "-", http_user_agent: "Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:47.0) Gecko/20100101 Firefox/47.0", request_id: a02b2dea9cf06344a25611c1d7ad72db
    ```
    {: screen}

    To create a custom log format that is based on the default format for ALB logs, modify the following section as needed and add it to your configmap:
    ```yaml
    apiVersion: v1
    data:
      log-format: '{"time_date": "$time_iso8601", "client": "$remote_addr",
                    "host": "$http_host", "scheme": "$scheme",
                    "request_method": "$request_method", "request_uri": "$uri",
                    "request_id": "$request_id", "status": $status,
                    "upstream_addr": "$upstream_addr", "upstream_status":
                    $upstream_status, "request_time": $request_time,
                    "upstream_response_time": $upstream_response_time,
                    "upstream_connect_time": $upstream_connect_time,
                    "upstream_header_time": $upstream_header_time}'
      log-format-escape-json: "true"
    kind: ConfigMap
    metadata:
      name: ibm-cloud-provider-ingress-cm
      namespace: kube-system
    ```
    {: codeblock}

4. Save the configuration file.

5. Verify that the configmap changes were applied.

   ```
   oc get cm ibm-cloud-provider-ingress-cm -n kube-system -o yaml
   ```
   {: pre}

4. To view the Ingress ALB logs, choose between two options.
    * [Create a logging configuration for the Ingress service](/docs/openshift?topic=openshift-health#oc_logmet_options) in your cluster.
    * Check the logs from the CLI.
        1. Get the ID of a pod for an ALB.
            ```
            oc get pods -n kube-system | grep alb
            ```
            {: pre}

        2. Open the logs for that ALB pod. Verify that logs follow the updated format.
            ```
            oc logs <ALB_pod_ID> nginx-ingress -n kube-system
            ```
            {: pre}

<br />


## Monitoring the Ingress ALB
{: #ingress_monitoring}

Monitor your ALBs by deploying a metrics exporter and Prometheus agent into your cluster.
{: shortdesc}

The ALB metrics exporter uses the NGINX directive, `vhost_traffic_status_zone`, to collect metrics data from the `/status/format/json` endpoint on each Ingress ALB pod. The metrics exporter automatically reformats each data field in the JSON file into a metric that is readable by Prometheus. Then, a Prometheus agent picks up the metrics that are produced by the exporter and makes the metrics visible on a Prometheus dashboard.

### Installing the metrics exporter Helm chart
{: #metrics-exporter}

Install the metrics exporter Helm chart to monitor an ALB in your cluster.
{: shortdesc}

The ALB metrics exporter pods must deploy to the same worker nodes that your ALBs are deployed to. If your ALBs run on edge worker nodes, and those edge nodes are tainted to prevent other workload deployments, the metrics exporter pods cannot be scheduled. You must remove the taints by running `oc adm taint node <node_name> dedicated:NoSchedule- dedicated:NoExecute-` or using the `ibmcloud oc worker-pool taint rm` command.
{: note}

1.  **Important**: [Follow the instructions](/docs/openshift?topic=openshift-helm#public_helm_install) to install the Helm client on your local machine, install the Helm server (Tiller) with a service account, and add the {{site.data.keyword.cloud_notm}} Helm repositories.

2. Install the `ibmcloud-alb-metrics-exporter` Helm chart to your cluster. This Helm chart deploys an ALB metrics exporter and creates an `alb-metrics-service-account` service account in the `kube-system` namespace. Replace `<zone>` with the zone where the ALB exists and `<alb_ID>` with the ID of the ALB that you want to collect metrics for. To view the IDs for the ALBs in your cluster, run `ibmcloud oc alb ls --cluster <cluster_name>`.
  ```
  helm install iks-charts/ibmcloud-alb-metrics-exporter --set metricsNameSpace=kube-system --set name=alb-<zone>-metrics-exporter --set albId=<alb_ID> --set albZone=<zone>
  ```
  {: pre}

3. Check the chart deployment status. When the chart is ready, the **STATUS** field near the beginning of the output has a value of `DEPLOYED`.
  ```
  helm status ibmcloud-alb-metrics-exporter
  ```
  {: pre}

4. Verify that the `ibmcloud-alb-metrics-exporter` pods are running.
  ```
  oc get pods -n kube-system -o wide
  ```
  {:pre}

  Example output:
  ```
  NAME                                             READY     STATUS      RESTARTS   AGE       IP               NODE
  ...
  alb-metrics-exporter-868fddf777-d49l5            1/1       Running     0          19s       172.30.xxx.xxx   10.xxx.xx.xxx
  alb-metrics-exporter-868fddf777-pf7x5            1/1       Running     0          19s       172.30.xxx.xxx   10.xxx.xx.xxx
  ```
  {:screen}

5. Repeat steps 2 - 4 for each ALB in your cluster.

6. Optional: [Install the Prometheus agent](#prometheus-agent) to pick up the metrics that are produced by the exporter and make the metrics visible on a Prometheus dashboard.

### Installing the Prometheus agent Helm chart
{: #prometheus-agent}

After you install the [metrics exporter](#metrics-exporter), you can install the Prometheus agent Helm chart to pick up the metrics that are produced by the exporter and make the metrics visible on a Prometheus dashboard.
{: shortdesc}

1. Download the `tar` file for the metrics exporter Helm chart from https://icr.io/helm/iks-charts/charts/ibmcloud-alb-metrics-exporter-1.0.7.tgz

2. Navigate to the Prometheus subfolder.
  ```
  cd ibmcloud-alb-metrics-exporter-1.0.7.tar/ibmcloud-alb-metrics-exporter/subcharts/prometheus
  ```
  {: pre}

3. Install the Prometheus Helm chart to your cluster. Replace <ingress_subdomain> with the Ingress subdomain for your cluster. The URL for the Prometheus dashboard is a combination of the default Prometheus subdomain, `prom-dash`, and your Ingress subdomain, for example `prom-dash.mycluster-<hash>-0000.us-south.containers.appdomain.cloud`. To find the Ingress subdomain for your cluster, run `ibmcloud oc cluster get --cluster <cluster_name>`.
  ```
  helm install . --set name=prometheus --set nameSpace=kube-system --set hostName=prom-dash.<ingress_subdomain>
  ```
  {: pre}

4. Check the chart deployment status. When the chart is ready, the **STATUS** field near the beginning of the output has a value of `DEPLOYED`.
    ```
    helm status prometheus
    ```
    {: pre}

5. Verify that the `prometheus` pod is running.
    ```
    oc get pods -n kube-system -o wide
    ```
    {:pre}

    Example output:
    ```
    NAME                                             READY     STATUS      RESTARTS   AGE       IP               NODE
    alb-metrics-exporter-868fddf777-d49l5            1/1       Running     0          19s       172.30.xxx.xxx   10.xxx.xx.xxx
    alb-metrics-exporter-868fddf777-pf7x5            1/1       Running     0          19s       172.30.xxx.xxx   10.xxx.xx.xxx
    prometheus-9fbcc8bc7-2wvbk                       1/1       Running     0          1m        172.30.xxx.xxx   10.xxx.xx.xxx
    ```
    {:screen}

6. In a browser, enter the URL for the Prometheus dashboard. This hostname has the format `prom-dash.mycluster-<hash>-0000.us-south.containers.appdomain.cloud`. The Prometheus dashboard for your ALB opens.

7. Review more information about the [ALB](#alb_metrics), [server](#server_metrics), and [upstream](#upstream_metrics) metrics listed in the dashboard.

### ALB metrics
{: #alb_metrics}

The `alb-metrics-exporter` automatically reformats each data field in the JSON file into a metric that is readable by Prometheus. ALB metrics collect data on the connections and responses the ALB is handling.
{: shortdesc}

ALB metrics are in the format `kube_system_<ALB-ID>_<METRIC-NAME> <VALUE>`. For example, if an ALB receives 23 responses with 2xx-level status codes, the metric is formatted as `kube_system_public_crf02710f54fcc40889c301bfd6d5b77fe_alb1_totalHandledRequest {.. metric="2xx"} 23` where `metric` is the prometheus label.

The following table lists the supported ALB metric names with the metric labels in the format `<ALB_metric_name>_<metric_label>`.

|Metric|Description|
|---|---|
|`connections_reading`|The total number of reading client connections.|
|`connections_accepted`|The total number of accepted client connections.|
|`connections_active`|The total number of active client connections.|
|`connections_handled`|The total number of handled client connections.|
|`connections_requests`|The total number of requested client connections.|
|`connections_waiting`|The total number of waiting client connections.|
|`connections_writing`|The total number of writing client connections.|
|`totalHandledRequest_1xx`|The number of responses with status codes 1xx.|
|`totalHandledRequest_2xx`|The number of responses with status codes 2xx.|
|`totalHandledRequest_3xx`|The number of responses with status codes 3xx.|
|`totalHandledRequest_4xx`|The number of responses with status codes 4xx.|
|`totalHandledRequest_5xx`|The number of responses with status codes 5xx.|
|`totalHandledRequest_total`|The total number of client requests received from clients.|
{: caption="Supported ALB metrics" caption-side="top"}

### Server metrics
{: #server_metrics}

The `alb-metrics-exporter` automatically reformats each data field in the JSON file into a metric that is readable by Prometheus. Server metrics collect data on the subdomain that are defined in an Ingress resource; for example, `dev.demostg1.stg.us.south.containers.appdomain.cloud`.
{: shortdesc}

Server metrics are in the format `kube_system_server_<ALB-ID>_<SUB-TYPE>_<SERVER-NAME>_<METRIC-NAME> <VALUE>`.

`<SERVER-NAME>_<METRIC-NAME>` are formatted as labels. For example, `albId="dev_demostg1_us-south_containers_appdomain_cloud",metric="out"`

For example, if the server sent a total of 22319 bytes to clients, the metric is formatted as:
```
kube_system_server_public_cra6a6eb9e897e41c4a5e58f957b417aec_alb1_bytes{albId="dev_demostg1_us-south_containers_appdomain_cloud",app="alb-metrics-exporter",instance="172.30.140.68:9913",job="kubernetes-pods",kubernetes_namespace="kube-system",kubernetes_pod_name="alb-metrics-exporter-7d495d785c-8wfw4",metric="out",pod_template_hash="3805183417"} 22319
```
{: screen}

|Metric field|Description|
|---|---|
|`<ALB-ID>`|The ALB ID. In the previous example, the ALB ID is `public\_cra6a6eb9e897e41c4a5e58f957b417aec\_alb1`.|
|`<SUB-TYPE>`|The subtype of metric. Each subtype corresponds to one or more metric names.
`bytes` and `processing\_time` correspond to metrics `in` and `out`.`cache` corresponds to metrics `bypass`, `expired`, `hit`, `miss`, `revalidated`, `scare`, `stale`, and `updating`.`requests` corresponds to metrics `requestMsec`, `1xx`, `2xx`, `3xx`, `4xx`, `5xx`, and `total`.In the previous example, the subtype is `bytes`.|
|`<SERVER-NAME>`|The name of the server that is defined in the Ingress resource. To maintain compatibility with Prometheus, periods (`.`) are replaced by underscores `(\_)`. In the previous example, the server name is `dev_demostg1_stg_us_south_containers_appdomain_cloud`.|
|`<METRIC_NAME>`|The name of the collected metric type. For a list of metric names, see the following table for supported server metrics. In the previous example, the metric name is `out`.|
|`<VALUE>`|The value of the collected metric. In the previous example, the value is `22319`.|
{: caption="Understanding the server metric format" caption-side="top"}

The following table lists the supported server metric names.

|Metric|Description|
|---|---|
|`in`|The total number of bytes received from clients.|
|`out`|The total number of bytes sent to clients.|
|`bypass`|The number of times that a cacheable item was fetched from the origin server because it has not met the threshold for being in the cache (for example, number of requests).|
|`expired`|The number of times that an item was found in the cache but was not selected because it was expired.|
|`hit`|The number of times that a valid item was selected from the cache.|
|`miss`|The number of times that no valid cache item was found in the cache and the server fetched the item from the origin server.|
|`revalidated`|The number of times that an expired item in the cache was revalidated.|
|`scarce`|The number of times the cache removed seldom-used or low-priority items to free up scarce memory.|
|`stale`|The number of times that an expired item was in found in the cache, but because another request caused the server to fetch the item from the origin server, the item was selected from the cache.|
|`updating`|The number of times that stale content was updated.|
|`requestMsec`|The average of request processing times in milliseconds.|
|`1xx`|The number of responses with status codes 1xx.|
|`2xx`|The number of responses with status codes 2xx.|
|`3xx`|The number of responses with status codes 3xx.|
|`4xx`|The number of responses with status codes 4xx.|
|`5xx`|The number of responses with status codes 5xx.|
|`total`|The total number of responses with status codes.|
{: caption="Supported server metrics" caption-side="top"}

### Upstream metrics
{: #upstream_metrics}

The `alb-metrics-exporter` automatically reformats each data field in the JSON file into a metric that is readable by Prometheus. Upstream metrics collect data on the back-end service that is defined in an Ingress resource.
{: shortdesc}

Upstream metrics are formatted in two ways.
* [Type 1](#type_one) includes the upstream service name.
* [Type 2](#type_two) includes the upstream service name and a specific upstream pod IP address.

#### Type 1 upstream metrics
{: #type_one}

Upstream type 1 metrics are in the format `kube_system_upstream_<ALB-ID>_<SUB-TYPE>_<UPSTREAM-NAME>_<METRIC-NAME> <VALUE>`.
{: shortdesc}

`<UPSTREAM-NAME>_<METRIC-NAME>` are formatted as labels. For example, `albId="default-cafe-ingress-dev_demostg1_us-south_containers_appdomain_cloud-coffee-svc",metric="in"`

For example, if the upstream service received a total of 1227 bytes from the ALB, the metric is formatted as:
```
kube_system_upstream_public_cra6a6eb9e897e41c4a5e58f957b417aec_alb1_bytes{albId="default-cafe-ingress-dev_demostg1_us-south_containers_appdomain_cloud-coffee-svc",app="alb-metrics-exporter",instance="172.30.140.68:9913",job="kubernetes-pods",kubernetes_namespace="kube-system",kubernetes_pod_name="alb-metrics-exporter-7d495d785c-8wfw4",metric="in",pod_template_hash="3805183417"} 1227
```
{: screen}

|Metric field|Description|
|---|---|
|`<ALB-ID>`|The ALB ID. In the previous example, the ALB ID is `public\_crf02710f54fcc40889c301bfd6d5b77fe\_alb1`.|
|`<SUB-TYPE>`|The subtype of metric. Supported values are `bytes`, `processing\_time`, and `requests`. In the previous example, the subtype is `bytes`.|
|`<UPSTREAM-NAME>`|The name of the upstream service that is defined in the Ingress resource. To maintain compatibility with Prometheus, periods (`.`) are replaced by underscores `(\_)`. In the previous example, the upstream name is `default-cafe-ingress-dev_demostg1_us-south_containers_appdomain_cloud-coffee-svc`.|
|`<METRIC_NAME>`|The name of the collected metric type. For a list of metric names, see the following table for supported upstream type 1 metrics. In the previous example, the metric name is `in`.|
|`<VALUE>`|The value of the collected metric. In the previous example, the value is `1227`.|
{: caption="Understanding fields in the default Ingress log format" caption-side="top"}

The following table lists the supported upstream type 1 metric names.

|Metric|Description|
|---|---|
|`in`|The total number of bytes received from the ALB server.|
|`out`|The total number of bytes sent to the ALB server.|
|`1xx`|The number of responses with status codes 1xx.|
|`2xx`|The number of responses with status codes 2xx.|
|`3xx`|The number of responses with status codes 3xx.|
|`4xx`|The number of responses with status codes 4xx.|
|`5xx`|The number of responses with status codes 5xx.|
|`total`|The total number of responses with status codes.|
{: caption="Understanding the upstream type 1 metric format" caption-side="top"}

#### Type 2 upstream metrics
{: #type_two}

Upstream type 2 metrics are in the format `kube_system_upstream_<ALB-ID>_<METRIC-NAME>_<UPSTREAM-NAME>_<POD-IP> <VALUE>`.
{: shortdesc}

`<UPSTREAM-NAME>_<POD-IP>` are formatted as labels. For example, `albId="default-cafe-ingress-dev_dev_demostg1_us-south_containers_appdomain_cloud-tea-svc",backend="172_30_75_6_80"`

For example, if the upstream service has an average request processing time (including upstream) of 40 milliseconds, the metric is formatted as:
```
kube_system_upstream_public_cra6a6eb9e897e41c4a5e58f957b417aec_alb1_requestMsec{albId="default-cafe-ingress-dev_dev_demostg1_us-south_containers_appdomain_cloud-tea-svc",app="alb-metrics-exporter",backend="172_30_75_6_80",instance="172.30.75.3:9913",job="kubernetes-pods",kubernetes_namespace="kube-system",kubernetes_pod_name="alb-metrics-exporter-7d495d785c-swkls",pod_template_hash="3805183417"} 40
```
{: screen}

|Metric field|Description|
|---|---|
|`<ALB-ID>`|The ALB ID. In the previous example, the ALB ID is `public\_cra6a6eb9e897e41c4a5e58f957b417aec\_alb1`.|
|`<UPSTREAM-NAME>`|The name of the upstream service that is defined in the Ingress resource. To maintain compatibility with Prometheus, periods (`.`) are replaced by underscores (`\_`). In the previous example, the upstream name is `demostg1\_stg\_us\_south\_containers\_appdomain\_cloud\_tea\_svc`.|
|`<POD\_IP>`|The IP address and port of a specific upstream service pod. To maintain compatibility with Prometheus, periods (`.`) and colons (`:`) are replaced by underscores `(_)`. In the previous example, the upstream pod IP is `172_30_75_6_80`.|
|`<METRIC_NAME>`|The name of the collected metric type. For a list of metric names, see the following table for Supported upstream type 2 metrics. In the previous example, the metric name is `requestMsec`.|
|`<VALUE>`|The value of the collected metric. In the previous example, the value is `40`.|
{: caption="Understanding the upstream type 2 metric format" caption-side="top"}

The following table lists the supported upstream type 2 metric names.

|Metric|Description|
|---|---|
|`requestMsec`|The average of request processing times, including upstream, in milliseconds.|
|`responseMsec`|The average of only upstream response processing times in milliseconds.|
{: caption="Supported upstream type 2 metrics" caption-side="top"}

<br />


## Increasing the shared memory zone size for Ingress metrics collection
{: #vts_zone_size}

Shared memory zones are defined so that worker processes can share information such as cache, session persistence, and rate limits. A shared memory zone, called the virtual host traffic status zone, is set up for Ingress to collect metrics data for an ALB.
{: shortdesc}

In the `ibm-cloud-provider-ingress-cm` Ingress configmap, the `vts-status-zone-size` field sets the size of the shared memory zone for metrics data collection. By default, `vts-status-zone-size` is set to `10m`. If you have a large environment that requires more memory for metrics collection, you can override the default to instead use a larger value by following these steps.

Before you begin, ensure that you have the [**Writer** or **Manager** {{site.data.keyword.cloud_notm}} IAM service role](/docs/openshift?topic=openshift-users#platform) for the `kube-system` namespace.

1. Edit the configuration file for the `ibm-cloud-provider-ingress-cm` configmap resource.

    ```
    oc edit cm ibm-cloud-provider-ingress-cm -n kube-system
    ```
    {: pre}

2. Change the value of `vts-status-zone-size` from `10m` to a larger value.

   ```yaml
   apiVersion: v1
   data:
     vts-status-zone-size: "10m"
   kind: ConfigMap
   metadata:
     name: ibm-cloud-provider-ingress-cm
     namespace: kube-system
   ```
   {: codeblock}

3. Save the configuration file.

4. Verify that the configmap changes were applied.

   ```
   oc get cm ibm-cloud-provider-ingress-cm -n kube-system -o yaml
   ```
   {: pre}



