---

copyright:
  years: 2014, 2020
lastupdated: "2020-01-08"

keywords: openshift, roks, rhoks, rhos, ingress, alb, health, prometheus

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


# Logging and monitoring Ingress
{: #ingress_health}

Customize logging and set up monitoring to help you troubleshoot issues and improve the performance of your Ingress configuration.
{: shortdesc}

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

<table>
<caption>Understanding fields in the default Ingress log format</caption>
<thead>
<th colspan=2><img src="images/idea.png" alt="Idea icon"/> Understanding fields in the default Ingress log format</th>
</thead>
<tbody>
<tr>
<td><code>"time_date": "$time_iso8601"</code></td>
<td>The local time in the ISO 8601 standard format when the log is written.</td>
</tr>
<tr>
<td><code>"client": "$remote_addr"</code></td>
<td>The IP address of the request package that the client sent to your app. This IP can change based on the following situations:<ul><li>When a client request to your app is sent to your cluster, the request is routed to a pod for the load balancer service that exposes the ALB. If no app pod exists on the same worker node as the load balancer service pod, the load balancer forwards the request to an app pod on a different worker node. The source IP address of the request package is changed to the public IP address of the worker node where the app pod is running.</li><li>If [source IP preservation is enabled](/docs/openshift?topic=openshift-ingress-settings#preserve_source_ip), the original IP address of the client request to your app is recorded instead.</li></ul></td>
</tr>
<tr>
<td><code>"host": "$http_host"</code></td>
<td>The host, or subdomain, that your apps are accessible through. This subdomain is configured in the Ingress resource files for your ALBs.</td>
</tr>
<tr>
<td><code>"scheme": "$scheme"</code></td>
<td>The kind of request: <code>HTTP</code> or <code>HTTPS</code>.</td>
</tr>
<tr>
<td><code>"request_method": "$request_method"</code></td>
<td>The method of the request call to the back-end app, such as <code>GET</code> or <code>POST</code>.</td>
</tr>
<tr>
<td><code>"request_uri": "$uri"</code></td>
<td>The original request URI to your app path. ALBs process the paths that apps listen on as prefixes. When an ALB receives a request from a client to an app, the ALB checks the Ingress resource for a path (as a prefix) that matches the path in the request URI.</td>
</tr>
<tr>
<td><code>"request_id": "$request_id"</code></td>
<td>A unique request identifier generated from 16 random bytes.</td>
</tr>
<tr>
<td><code>"status": $status</code></td>
<td>The status code for the connection session.<ul>
<li><code>200</code>: Session completed successfully</li>
<li><code>400</code>: Client data can't be parsed</li>
<li><code>403</code>: Access forbidden; for example, when access is limited for certain client IP addresses</li>
<li><code>500</code>: Internal server error</li>
<li><code>502</code>: Bad gateway; for example, if an upstream server can't be selected or reached</li>
<li><code>503</code>: Service unavailable; for example, when access is limited by the number of connections</li>
</ul></td>
</tr>
<tr>
<td><code>"upstream_addr": "$upstream_addr"</code></td>
<td>The IP address and port or the path to the UNIX-domain socket of the upstream server. If several servers are contacted during request processing, their addresses are separated by commas: <code>"192.168.1.1:80, 192.168.1.2:80, unix:/tmp/sock"</code>. If the request is redirected internally from one server group to another, then the server addresses from different groups are separated by colons: <code>"192.168.1.1:80, 192.168.1.2:80, unix:/tmp/sock : 192.168.10.1:80, 192.168.10.2:80"</code>. If the ALB can't select a server, the name of the server group is logged instead.</td>
</tr>
<tr>
<td><code>"upstream_status": $upstream_status</code></td>
<td>The status code of the response obtained from the upstream server for the back-end app, such as standard HTTP response codes. Status codes of several responses are separated by commas and colons like addresses in the <code>$upstream_addr</code> variable. If the ALB can't select a server, the 502 (Bad Gateway) status code is logged.</td>
</tr>
<tr>
<td><code>"request_time": $request_time</code></td>
<td>The request processing time, which is measured in seconds with a milliseconds resolution. This time starts when the ALB reads the client request's first bytes and stops when the ALB sends the response's last bytes to the client. The log is written immediately after the request processing time stops.</td>
</tr>
<tr>
<td><code>"upstream_response_time": $upstream_response_time</code></td>
<td>The time that it takes the ALB to receive the response from the upstream server for the back-end app, which is measured in seconds with a milliseconds resolution. Times of several responses are separated by commas and colons.</td>
</tr>
<tr>
<td><code>"upstream_connect_time": $upstream_connect_time</code></td>
<td>The time that it takes the ALB to establish a connection with the upstream server for the back-end app, which is measured in seconds with a milliseconds resolution. If TLS/SSL is enabled in your Ingress resource configuration, this time includes time spent on the handshake. Times of several connections are separated by commas and colons.</td>
</tr>
<tr>
<td><code>"upstream_header_time": $upstream_header_time</code></td>
<td>The time that it takes the ALB to receive the response header from the upstream server for the back-end app, which is measured in seconds with a milliseconds resolution. Times of several connections are separated by commas and colons.</td>
</tr>
</tbody></table>

## Customizing Ingress log content and format
{: #ingress_log_format}

You can customize the content and format of logs that are collected for the Ingress ALB.
{:shortdesc}

By default, Ingress logs are formatted in JSON and display common log fields. However, you can also create a custom log format by choosing which log components are forwarded and how the components are arranged in the log output

Before you begin, ensure that you have the [**Writer** or **Manager** {{site.data.keyword.cloud_notm}} IAM service role](/docs/openshift?topic=openshift-users#platform) for the `kube-system` namespace.

1. Edit the configuration file for the `ibm-cloud-provider-ingress-cm` configmap resource.

    ```
    oc edit cm ibm-cloud-provider-ingress-cm -n kube-system
    ```
    {: pre}

2. Add a <code>data</code> section. Add the `log-format` field and optionally, the `log-format-escape-json` field.

    ```
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
    <caption>YAML file components</caption>
    <thead>
    <th colspan=2><img src="images/idea.png" alt="Idea icon"/> Understanding the log-format configuration</th>
    </thead>
    <tbody>
    <tr>
    <td><code>log-format</code></td>
    <td>Replace <code>&lt;key&gt;</code> with the name for the log component and <code>&lt;log_variable&gt;</code> with a variable for the log component that you want to collect in log entries. You can include text and punctuation that you want the log entry to contain, such as quotation marks around string values and commas to separate log components. For example, formatting a component like <code>request: "$request"</code> generates the following in a log entry: <code>request: "GET / HTTP/1.1"</code> . For a list of all the variables you can use, see the <a href="http://nginx.org/en/docs/varindex.html">NGINX variable index</a>.<br><br>To log an additional header such as <em>x-custom-ID</em>, add the following key-value pair to the custom log content: <br><pre class="codeblock"><code>customID: $http_x_custom_id</code></pre> <br>Hyphens (<code>-</code>) are converted to underscores (<code>_</code>) and <code>$http_</code> must be added as a prefix to the custom header name.</td>
    </tr>
    <tr>
    <td><code>log-format-escape-json</code></td>
    <td>Optional: By default, logs are generated in text format. To generate logs in JSON format, add the <code>log-format-escape-json</code> field and use value <code>true</code>.</td>
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
    ```
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

The ALB metrics exporter pods must deploy to the same worker nodes that your ALBs are deployed to. If your ALBs run on edge worker nodes, and those edge nodes are tainted to prevent other workload deployments, the metrics exporter pods cannot be scheduled. You must remove the taints by running `oc taint node <node_name> dedicated:NoSchedule- dedicated:NoExecute-`.
{: note}

1.  **Important**: [Follow the instructions](/docs/containers?topic=containers-helm#public_helm_install) to install the Helm client on your local machine, install the Helm server (tiller) with a service account, and add the {{site.data.keyword.cloud_notm}} Helm repositories.

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

3. Install the Prometheus Helm chart to your cluster. Replace <ingress_subdomain> with the Ingress subdomain for your cluster. The URL for the Prometheus dashboard is a combination of the default Prometheus subdomain, `prom-dash`, and your Ingress subdomain, for example `prom-dash.mycluster-<hash>-0000.us-south.containers.appdomain.cloud`. To find the Ingress subdomain for your cluster, run <code>ibmcloud oc cluster get --cluster &lt;cluster_name&gt;</code>.
  ```
  helm install --name prometheus . --set nameSpace=kube-system --set hostName=prom-dash.<ingress_subdomain>
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

The following table lists the supported ALB metric names with the metric labels in the format `<ALB_metric_name>_<metric_label>`
<table>
<thead>
<th colspan=2><img src="images/idea.png" alt="Idea icon"/> Supported ALB metrics</th>
</thead>
<tbody>
<tr>
<td><code>connections_reading</code></td>
<td>The total number of reading client connections.</td>
</tr>
<tr>
<td><code>connections_accepted</code></td>
<td>The total number of accepted client connections.</td>
</tr>
<tr>
<td><code>connections_active</code></td>
<td>The total number of active client connections.</td>
</tr>
<tr>
<td><code>connections_handled</code></td>
<td>The total number of handled client connections.</td>
</tr>
<tr>
<td><code>connections_requests</code></td>
<td>The total number of requested client connections.</td>
</tr>
<tr>
<td><code>connections_waiting</code></td>
<td>The total number of waiting client connections.</td>
</tr>
<tr>
<td><code>connections_writing</code></td>
<td>The total number of writing client connections.</td>
</tr>
<tr>
<td><code>totalHandledRequest_1xx</code></td>
<td>The number of responses with status codes 1xx.</td>
</tr>
<tr>
<td><code>totalHandledRequest_2xx</code></td>
<td>The number of responses with status codes 2xx.</td>
</tr>
<tr>
<td><code>totalHandledRequest_3xx</code></td>
<td>The number of responses with status codes 3xx.</td>
</tr>
<tr>
<td><code>totalHandledRequest_4xx</code></td>
<td>The number of responses with status codes 4xx.</td>
</tr>
<tr>
<td><code>totalHandledRequest_5xx</code></td>
<td>The number of responses with status codes 5xx.</td>
</tr>
<tr>
<td><code>totalHandledRequest_total</code></td>
<td>The total number of client requests received from clients.</td>
  </tr></tbody>
</table>

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

<table>
<thead>
<th colspan=2><img src="images/idea.png" alt="Idea icon"/> Understanding the server metric format</th>
</thead>
<tbody>
<tr>
<td><code>&lt;ALB-ID&gt;</code></td>
<td>The ALB ID. In the previous example, the ALB ID is <code>public\_cra6a6eb9e897e41c4a5e58f957b417aec\_alb1</code>.</td>
</tr>
<tr>
<td><code>&lt;SUB-TYPE&gt;</code></td>
<td>The subtype of metric. Each subtype corresponds to one or more metric names.
<ul>
<li><code>bytes</code> and <code>processing\_time</code> correspond to metrics <code>in</code> and <code>out</code>.</li>
<li><code>cache</code> corresponds to metrics <code>bypass</code>, <code>expired</code>, <code>hit</code>, <code>miss</code>, <code>revalidated</code>, <code>scare</code>, <code>stale</code>, and <code>updating</code>.</li>
<li><code>requests</code> corresponds to metrics <code>requestMsec</code>, <code>1xx</code>, <code>2xx</code>, <code>3xx</code>, <code>4xx</code>, <code>5xx</code>, and <code>total</code>.</li></ul>
In the previous example, the subtype is <code>bytes</code>.</td>
</tr>
<tr>
<td><code>&lt;SERVER-NAME&gt;</code></td>
<td>The name of the server that is defined in the Ingress resource. To maintain compatibility with Prometheus, periods (<code>.</code>) are replaced by underscores <code>(\_)</code>. In the previous example, the server name is <code>dev_demostg1_stg_us_south_containers_appdomain_cloud</code>.</td>
</tr>
<tr>
<td><code>&lt;METRIC_NAME&gt;</code></td>
<td>The name of the collected metric type. For a list of metric names, see the following table for supported server metrics. In the previous example, the metric name is <code>out</code>.</td>
</tr>
<tr>
<td><code>&lt;VALUE&gt;</code></td>
<td>The value of the collected metric. In the previous example, the value is <code>22319</code>.</td>
</tr>
</tbody></table>

The following table lists the supported server metric names.

<table>
<thead>
<th colspan=2><img src="images/idea.png" alt="Idea icon"/> Supported server metrics</th>
</thead>
<tbody>
<tr>
<td><code>in</code></td>
<td>The total number of bytes received from clients.</td>
</tr>
<tr>
<td><code>out</code></td>
<td>The total number of bytes sent to clients.</td>
</tr>
<tr>
<td><code>bypass</code></td>
<td>The number of times that a cacheable item was fetched from the origin server because it has not met the threshold for being in the cache (for example, number of requests).</td>
</tr>
<tr>
<td><code>expired</code></td>
<td>The number of times that an item was found in the cache but was not selected because it was expired.</td>
</tr>
<tr>
<td><code>hit</code></td>
<td>The number of times that a valid item was selected from the cache.</td>
</tr>
<tr>
<td><code>miss</code></td>
<td>The number of times that no valid cache item was found in the cache and the server fetched the item from the origin server.</td>
</tr>
<tr>
<td><code>revalidated</code></td>
<td>The number of times that an expired item in the cache was revalidated.</td>
</tr>
<tr>
<td><code>scarce</code></td>
<td>The number of times the cache removed seldom-used or low-priority items to free up scarce memory.</td>
</tr>
<tr>
<td><code>stale</code></td>
<td>The number of times that an expired item was in found in the cache, but because another request caused the server to fetch the item from the origin server, the item was selected from the cache.</td>
</tr>
<tr>
<td><code>updating</code></td>
<td>The number of times that stale content was updated.</td>
</tr>
<tr>
<td><code>requestMsec</code></td>
<td>The average of request processing times in milliseconds.</td>
</tr>
<tr>
<td><code>1xx</code></td>
<td>The number of responses with status codes 1xx.</td>
</tr>
<tr>
<td><code>2xx</code></td>
<td>The number of responses with status codes 2xx.</td>
</tr>
<tr>
<td><code>3xx</code></td>
<td>The number of responses with status codes 3xx.</td>
</tr>
<tr>
<td><code>4xx</code></td>
<td>The number of responses with status codes 4xx.</td>
</tr>
<tr>
<td><code>5xx</code></td>
<td>The number of responses with status codes 5xx.</td>
</tr>
<tr>
<td><code>total</code></td>
<td>The total number of responses with status codes.</td>
  </tr></tbody>
</table>

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

<table>
<thead>
<th colspan=2><img src="images/idea.png" alt="Idea icon"/> Understanding the upstream type 1 metric format</th>
</thead>
<tbody>
<tr>
<td><code>&lt;ALB-ID&gt;</code></td>
<td>The ALB ID. In the previous example, the ALB ID is <code>public\_crf02710f54fcc40889c301bfd6d5b77fe\_alb1</code>.</td>
</tr>
<tr>
<td><code>&lt;SUB-TYPE&gt;</code></td>
<td>The subtype of metric. Supported values are <code>bytes</code>, <code>processing\_time</code>, and <code>requests</code>. In the previous example, the subtype is <code>bytes</code>.</td>
</tr>
<tr>
<td><code>&lt;UPSTREAM-NAME&gt;</code></td>
<td>The name of the upstream service that is defined in the Ingress resource. To maintain compatibility with Prometheus, periods (<code>.</code>) are replaced by underscores <code>(\_)</code>. In the previous example, the upstream name is <code>default-cafe-ingress-dev_demostg1_us-south_containers_appdomain_cloud-coffee-svc</code>.</td>
</tr>
<tr>
<td><code>&lt;METRIC_NAME&gt;</code></td>
<td>The name of the collected metric type. For a list of metric names, see the following table for supported upstream type 1 metrics. In the previous example, the metric name is <code>in</code>.</td>
</tr>
<tr>
<td><code>&lt;VALUE&gt;</code></td>
<td>The value of the collected metric. In the previous example, the value is <code>1227</code>.</td>
</tr>
</tbody></table>

The following table lists the supported upstream type 1 metric names.

<table>
<thead>
<th colspan=2><img src="images/idea.png" alt="Idea icon"/> Supported upstream type 1 metrics</th>
</thead>
<tbody>
<tr>
<td><code>in</code></td>
<td>The total number of bytes received from the ALB server.</td>
</tr>
<tr>
<td><code>out</code></td>
<td>The total number of bytes sent to the ALB server.</td>
</tr>
<tr>
<td><code>1xx</code></td>
<td>The number of responses with status codes 1xx.</td>
</tr>
<tr>
<td><code>2xx</code></td>
<td>The number of responses with status codes 2xx.</td>
</tr>
<tr>
<td><code>3xx</code></td>
<td>The number of responses with status codes 3xx.</td>
</tr>
<tr>
<td><code>4xx</code></td>
<td>The number of responses with status codes 4xx.</td>
</tr>
<tr>
<td><code>5xx</code></td>
<td>The number of responses with status codes 5xx.</td>
</tr>
<tr>
<td><code>total</code></td>
<td>The total number of responses with status codes.</td>
  </tr></tbody>
</table>

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

<table>
<thead>
<th colspan=2><img src="images/idea.png" alt="Idea icon"/> Understanding the upstream type 2 metric format</th>
</thead>
<tbody>
<tr>
<td><code>&lt;ALB-ID&gt;</code></td>
<td>The ALB ID. In the previous example, the ALB ID is <code>public\_cra6a6eb9e897e41c4a5e58f957b417aec\_alb1</code>.</td>
</tr>
<td><code>&lt;UPSTREAM-NAME&gt;</code></td>
<td>The name of the upstream service that is defined in the Ingress resource. To maintain compatibility with Prometheus, periods (<code>.</code>) are replaced by underscores (<code>\_</code>). In the previous example, the upstream name is <code>demostg1\_stg\_us\_south\_containers\_appdomain\_cloud\_tea\_svc</code>.</td>
</tr>
<tr>
<td><code>&lt;POD\_IP&gt;</code></td>
<td>The IP address and port of a specific upstream service pod. To maintain compatibility with Prometheus, periods (<code>.</code>) and colons (<code>:</code>) are replaced by underscores <code>(_)</code>. In the previous example, the upstream pod IP is <code>172_30_75_6_80</code>.</td>
</tr>
<tr>
<td><code>&lt;METRIC_NAME&gt;</code></td>
<td>The name of the collected metric type. For a list of metric names, see the following table for Supported upstream type 2 metrics. In the previous example, the metric name is <code>requestMsec</code>.</td>
</tr>
<tr>
<td><code>&lt;VALUE&gt;</code></td>
<td>The value of the collected metric. In the previous example, the value is <code>40</code>.</td>
</tr>
</tbody></table>

The following table lists the supported upstream type 2 metric names.

<table>
<thead>
<th colspan=2><img src="images/idea.png" alt="Idea icon"/> Supported upstream type 2 metrics</th>
</thead>
<tbody>
<tr>
<td><code>requestMsec</code></td>
<td>The average of request processing times, including upstream, in milliseconds.</td>
</tr>
<tr>
<td><code>responseMsec</code></td>
<td>The average of only upstream response processing times in milliseconds.</td>
  </tr></tbody>
</table>

<br />


## Increasing the shared memory zone size for Ingress metrics collection
{: #vts_zone_size}

Shared memory zones are defined so that worker processes can share information such as cache, session persistence, and rate limits. A shared memory zone, called the virtual host traffic status zone, is set up for Ingress to collect metrics data for an ALB.
{:shortdesc}

In the `ibm-cloud-provider-ingress-cm` Ingress configmap, the `vts-status-zone-size` field sets the size of the shared memory zone for metrics data collection. By default, `vts-status-zone-size` is set to `10m`. If you have a large environment that requires more memory for metrics collection, you can override the default to instead use a larger value by following these steps.

Before you begin, ensure that you have the [**Writer** or **Manager** {{site.data.keyword.cloud_notm}} IAM service role](/docs/openshift?topic=openshift-users#platform) for the `kube-system` namespace.

1. Edit the configuration file for the `ibm-cloud-provider-ingress-cm` configmap resource.

    ```
    oc edit cm ibm-cloud-provider-ingress-cm -n kube-system
    ```
    {: pre}

2. Change the value of `vts-status-zone-size` from `10m` to a larger value.

   ```
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



