---

copyright:
  years: 2014, 2019
lastupdated: "2019-07-26"

keywords: kubernetes, iks, logmet, logs, metrics

subcollection: containers

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:download: .download}
{:preview: .preview}


# Logging and monitoring
{: #health}

Set up logging and monitoring in {{site.data.keyword.containerlong}} to help you troubleshoot issues and improve the health and performance of your Kubernetes clusters and apps.
{: shortdesc}

Continuous monitoring and logging is the key to detecting attacks on your cluster and troubleshooting issues as they arise. By continuously monitoring your cluster, you're able to better understand your cluster capacity and the availability of resources that are available to your app. With this insight, you can prepare to protect your apps against downtime. **Note**: To configure logging and monitoring, you must use a standard cluster in {{site.data.keyword.containerlong_notm}}.

## Choosing a logging solution
{: #logging_overview}

By default, logs are generated and written locally for all of the following {{site.data.keyword.containerlong_notm}} cluster components: worker nodes, containers, applications, persistent storage, Ingress application load balancer, Kubernetes API, and the `kube-system` namespace. Several logging solutions are available to collect, forward, and view these logs.
{: shortdesc}

You can choose your logging solution based on which cluster components you need to collect logs for. A common implementation is to choose a logging service that you prefer based on its analysis and interface capabilities, such as {{site.data.keyword.loganalysisfull}}, {{site.data.keyword.la_full}}, or a third-party service. You can then use {{site.data.keyword.cloudaccesstrailfull}} to audit user activity in the cluster and backup cluster master logs to {{site.data.keyword.cos_full}}. **Note**: To configure logging, you must have a standard Kubernetes cluster.

<dl>

<dt>{{site.data.keyword.la_full_notm}}</dt>
<dd>Manage pod container logs by deploying LogDNA as a third-party service to your cluster. To use {{site.data.keyword.la_full_notm}}, you must deploy a logging agent to every worker node in your cluster. This agent collects logs with the extension `*.log` and extensionless files that are stored in the `/var/log` directory of your pod from all namespaces, including `kube-system`. The agent then forwards the logs to the {{site.data.keyword.la_full_notm}} service. For more information about the service, see the [{{site.data.keyword.la_full_notm}}](/docs/services/Log-Analysis-with-LogDNA?topic=LogDNA-about) documentation. To get started, see [Managing Kubernetes cluster logs with {{site.data.keyword.loganalysisfull_notm}} with LogDNA](/docs/services/Log-Analysis-with-LogDNA/tutorials?topic=LogDNA-kube#kube).
</dd>

<dt>Fluentd with {{site.data.keyword.loganalysisfull_notm}}</dt>
<dd><p class="deprecated">Previously, you could create a logging configuration to forward logs that are collected by the Fluentd cluster component to {{site.data.keyword.loganalysisfull_notm}}. As of 30 April 2019, you cannot provision new {{site.data.keyword.loganalysisshort_notm}} instances, and all Lite plan instances are deleted. Existing premium plan instances are supported until 30 September 2019. To continue collecting logs for your cluster, you must set up {{site.data.keyword.la_full_notm}} or change your configuration to forward logs to an external server.</p>
</dd>

<dt>Fluentd with an external server</dt>
<dd>To collect, forward, and view logs for a cluster component, you can create a logging configuration by using Fluentd. When you create a logging configuration, the [Fluentd ![External link icon](../icons/launch-glyph.svg "External link icon")](https://www.fluentd.org/) cluster component collects logs from the paths for a specified source. Fluentd can then forward these logs to an external server that accepts a syslog protocol. To get started, see [Understanding cluster and app log forwarding to syslog](#logging).
</dd>

<dt>{{site.data.keyword.cloudaccesstrailfull_notm}}</dt>
<dd>To monitor user-initiated administrative activity made in your cluster, you can collect and forward audit logs to {{site.data.keyword.cloudaccesstrailfull_notm}}. Clusters generate two types of {{site.data.keyword.cloudaccesstrailshort}} events.
<ul><li>Cluster management events are automatically generated and forwarded to {{site.data.keyword.cloudaccesstrailshort}}.</li>
<li>Kubernetes API server audit events are automatically generated, but you must [create a logging configuration](#api_forward) so that Fluentd can forward these logs to {{site.data.keyword.cloudaccesstrailshort}}.</li></ul>
For more information about the types of {{site.data.keyword.containerlong_notm}} events that you can track, see [Activity Tracker events](/docs/containers?topic=containers-at_events). For more information about the service, see the [Activity Tracker](/docs/services/cloud-activity-tracker?topic=cloud-activity-tracker-getting-started) documentation.
<p class="note">{{site.data.keyword.containerlong_notm}} is currently not configured to use {{site.data.keyword.at_full}}. To manage cluster management events and Kubernetes API audit logs, continue to use {{site.data.keyword.cloudaccesstrailfull_notm}} with LogAnalysis.</p>
</dd>

<dt>{{site.data.keyword.cos_full_notm}}</dt>
<dd>To collect, forward, and view logs for your cluster's Kubernetes master, you can take a snapshot of your master logs at any point in time to collect in an {{site.data.keyword.cos_full_notm}} bucket. The snapshot includes anything that is sent through the API server, such as pod scheduling, deployments, or RBAC policies. To get started, see [Collecting master logs](#collect_master).</dd>

<dt>Third-party services or configure your own logging</dt>
<dd>If you have special requirements, you can set up your own logging solution. Check out third-party logging services that you can add to your cluster in [Logging and monitoring integrations](/docs/containers?topic=containers-supported_integrations#health_services). To check the logs of an individual Kubernetes pod or other resource, you can run `kubectl logs <resource_name>`. By default, logs are stored in `/var/log` for the namespace. For example, you can collect container logs from the `/var/log/pods/` path. You might write a script to export logs to a persistent storage device that you can use to analyze with your own logging solution.<p class="important">To check the logs for individual app pods, run `kubectl logs <pod name>`. Do not use the Kubernetes dashboard to stream logs for your pods, which might cause a disruption in your access to the Kubernetes dashboard.</p></dd>

</dl>

<br />


## Forwarding cluster and app logs to {{site.data.keyword.la_full_notm}}
{: #logdna}

Manage pod container logs by deploying LogDNA as a third-party service to your cluster.
{: shortdesc}

To use {{site.data.keyword.la_full_notm}}, you must deploy a logging agent to every worker node in your cluster. This agent collects logs with the extension `*.log` and extensionless files that are stored in the `/var/log` directory of your pod from all namespaces, including `kube-system`. The agent then forwards the logs to the {{site.data.keyword.la_full_notm}} service. For more information about the service, see the [{{site.data.keyword.la_full_notm}}](/docs/services/Log-Analysis-with-LogDNA?topic=LogDNA-about) documentation. To get started, see [Managing Kubernetes cluster logs with {{site.data.keyword.loganalysisfull_notm}} with LogDNA](/docs/services/Log-Analysis-with-LogDNA/tutorials?topic=LogDNA-kube#kube).

<br />


## Deprecated: Forwarding cluster, app, and Kubernetes API audit logs to {{site.data.keyword.loganalysisfull_notm}}
{: #loga}

Previously, you could create a logging configuration to forward logs that are collected by the Fluentd cluster component to {{site.data.keyword.loganalysisfull_notm}}. As of 30 April 2019, {{site.data.keyword.loganalysisfull_notm}} is deprecated. You cannot provision new {{site.data.keyword.loganalysisshort_notm}} instances, and all Lite plan instances are deleted. Existing premium plan instances are supported until 30 September 2019.
{: deprecated}

To continue collecting logs for your cluster, you have the following options:
* Set up {{site.data.keyword.la_full_notm}}. For more information, see [Transitioning to {{site.data.keyword.la_full_notm}}](/docs/services/CloudLogAnalysis?topic=cloudloganalysis-transition).
* [Change your configuration to forward logs to an external server](#configuring).

For more information about existing {{site.data.keyword.loganalysisshort_notm}} instances, see the [{{site.data.keyword.loganalysisshort_notm}} documentation](/docs/services/CloudLogAnalysis?topic=cloudloganalysis-containers_kube_other_logs).

<br />


## Forwarding cluster, app, and Kubernetes API audit logs to an external server
{: #configuring}

Configure log forwarding for {{site.data.keyword.containerlong_notm}} standard clusters to an external server.
{: shortdesc}

### Understanding log forwarding to an external server
{: #logging}

By default, logs are collected by the [Fluentd ![External link icon](../icons/launch-glyph.svg "External link icon")](https://www.fluentd.org/) add-on in your cluster. When you create a logging configuration for a source in your cluster such as a container, the logs that Fluentd collects from that source's paths are forwarded to an external server. The traffic from the source to the logging service on the ingestion port is encrypted.
{: shortdesc}

**What are the sources that I can configure log forwarding for?**

In the following image, you can see the location of the sources that you can configure logging for.

<img src="images/log_sources.png" width="600" alt="Log sources in your cluster" style="width:600px; border-style: none"/>

1. `worker`: Information that is specific to the infrastructure configuration that you have for your worker node. Worker logs are captured in syslog and contain operating system events. In `auth.log` you can find information on the authentication requests that are made to the OS.</br>**Paths**:
    * `/var/log/syslog`
    * `/var/log/auth.log`

2. `container`: Information that is logged by a running container.</br>**Paths**: Anything that is written to `STDOUT` or `STDERR`.

3. `application`: Information about events that occur at the application level. This could be a notification that an event took place such as a successful login, a warning about storage, or other operations that can be performed at the app level.</br>**Paths**: You can set the paths that your logs are forwarded to. However, in order for logs to be sent, you must use an absolute path in your logging configuration or the logs cannot be read. If your path is mounted to your worker node, it might have created a symlink. Example: If the specified path is `/usr/local/spark/work/app-0546/0/stderr` but the logs actually go to `/usr/local/spark-1.0-hadoop-1.2/work/app-0546/0/stderr`, then the logs cannot be read.

4. `storage`: Information about persistent storage that is set up in your cluster. Storage logs can help you set up problem determination dashboards and alerts as part of your DevOps pipeline and production releases. **Note**: The paths `/var/log/kubelet.log` and `/var/log/syslog` also contain storage logs, but logs from these paths are collected by the `kubernetes` and `worker` log sources.</br>**Paths**:
    * `/var/log/ibmc-s3fs.log`
    * `/var/log/ibmc-block.log`

  **Pods**:
    * `portworx-***`
    * `ibmcloud-block-storage-attacher-***`
    * `ibmcloud-block-storage-driver-***`
    * `ibmcloud-block-storage-plugin-***`
    * `ibmcloud-object-storage-plugin-***`

5. `kubernetes`: Information from the kubelet, the kube-proxy, and other Kubernetes events that happen in the kube-system namespace of the worker node.</br>**Paths**:
    * `/var/log/kubelet.log`
    * `/var/log/kube-proxy.log`
    * `/var/log/event-exporter/1..log`

6. `kube-audit`: Information about cluster-related actions that is sent to the Kubernetes API server, including the time, the user, and the affected resource.

7. `ingress`: Information about the network traffic that comes into a cluster through the Ingress ALB.</br>**Paths**:
    * `/var/log/alb/ids/*.log`
    * `/var/log/alb/ids/*.err`
    * `/var/log/alb/customerlogs/*.log`
    * `/var/log/alb/customerlogs/*.err`

</br>

**What configuration options do I have?**

The following table shows the different options that you have when you configure logging and their descriptions.

<table>
<caption> Understanding logging configuration options</caption>
  <thead>
    <th>Option</th>
    <th>Description</th>
  </thead>
  <tbody>
    <tr>
      <td><code><em>&lt;cluster_name_or_ID&gt;</em></code></td>
      <td>The name or ID of the cluster.</td>
    </tr>
    <tr>
      <td><code><em>--log_source</em></code></td>
      <td>The source that you want to forward logs from. Accepted values are <code>container</code>, <code>application</code>, <code>worker</code>, <code>kubernetes</code>, <code>ingress</code>, <code>storage</code>, and <code>kube-audit</code>. This argument supports a comma-separated list of log sources to apply to the configuration. If you do not provide a log source, logging configurations are created for <code>container</code> and <code>ingress</code> log sources.</td>
    </tr>
    <tr>
      <td><code><em>--type syslog</em></code></td>
      <td>The value <code>syslog</code> forwards your logs to an external server.</p>
      </dd></td>
    </tr>
    <tr>
      <td><code><em>--namespace</em></code></td>
      <td>Optional: The Kubernetes namespace that you want to forward logs from. Log forwarding is not supported for the <code>ibm-system</code> and <code>kube-system</code> Kubernetes namespaces. This value is valid only for the <code>container</code> log source. If you do not specify a namespace, then all namespaces in the cluster use this configuration.</td>
    </tr>
    <tr>
      <td><code><em>--hostname</em></code></td>
      <td><p>For {{site.data.keyword.loganalysisshort_notm}}, use the [ingestion URL](/docs/services/CloudLogAnalysis?topic=cloudloganalysis-log_ingestion#log_ingestion_urls). If you do not specify an ingestion URL, the endpoint for the region in which you created your cluster is used.</p>
      <p>For syslog, specify the host name or IP address of the log collector service.</p></td>
    </tr>
    <tr>
      <td><code><em>--port</em></code></td>
      <td>The ingestion port. If you do not specify a port, then the standard port <code>9091</code> is used.
      <p>For syslog, specify the port of the log collector server. If you do not specify a port, then the standard port <code>514</code> is used.</td>
    </tr>
    <tr>
      <td><code><em>--app-containers</em></code></td>
      <td>Optional: To forward logs from apps, you can specify the name of the container that contains your app. You can specify more than one container by using a comma-separated list. If no containers are specified, logs are forwarded from all of the containers that contain the paths that you provided.</td>
    </tr>
    <tr>
      <td><code><em>--app-paths</em></code></td>
      <td>The path on a container that the apps log to. To forward logs with source type <code>application</code>, you must provide a path. To specify more than one path, use a comma-separated list. Example: <code>/var/log/myApp1/*,/var/log/myApp2/*</code></td>
    </tr>
    <tr>
      <td><code><em>--syslog-protocol</em></code></td>
      <td>When the logging type is <code>syslog</code>, the transport layer protocol. You can use the following protocols: `udp`, `tls`, or `tcp`. When forwarding to a rsyslog server with the <code>udp</code> protocol, logs that are over 1KB are truncated.</td>
    </tr>
    <tr>
      <td><code><em>--ca-cert</em></code></td>
      <td>Required: When the logging type is <code>syslog</code> and the protocol is <code>tls</code>, the Kubernetes secret name that contains the Certificate Authority certificate.</td>
    </tr>
    <tr>
      <td><code><em>--verify-mode</em></code></td>
      <td>When the logging type is <code>syslog</code> and the protocol is <code>tls</code>, the verification mode. Supported values are <code>verify-peer</code> and the default <code>verify-none</code>.</td>
    </tr>
    <tr>
      <td><code><em>--skip-validation</em></code></td>
      <td>Optional: Skip the validation of the org and space names when they are specified. Skipping validation decreases processing time, but an invalid logging configuration will not correctly forward logs.</td>
    </tr>
  </tbody>
</table>

**Am I responsible for keeping Fluentd updated?**

In order to change your logging or filter configurations, the Fluentd logging add-on must be at the latest version. By default, automatic updates to the add-on are enabled. To disable automatic updates, see [Updating cluster add-ons: Fluentd for logging](/docs/containers?topic=containers-update#logging-up).

**Can I forward some logs, but not others, from one source in my cluster?**

Yes. For example, if you have a particularly chatty pod, you might want to prevent logs from that pod from taking up log storage space, while still allowing other pods' logs to be forwarded. To prevent logs from a specific pod from being forwarded, see [Filtering logs](#filter-logs).

<br />


### Forwarding cluster and app logs
{: #enable-forwarding}

Create a configuration for cluster and app logging. You can differentiate between the different logging options by using flags.
{: shortdesc}

**Forwarding logs to your own server over the `udp` or `tcp` protocols**

1. Ensure that you have the [**Editor** or **Administrator** {{site.data.keyword.cloud_notm}} IAM platform role](/docs/containers?topic=containers-users#platform).

2. For the cluster where the log source is located: [Log in to your account. If applicable, target the appropriate resource group. Set the context for your cluster.](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure)

3. Set up a server that accepts a syslog protocol in 1 of 2 ways:
  * Set up and manage your own server or have a provider manage it for you. If a provider manages the server for you, get the logging endpoint from the logging provider.

  * Run syslog from a container. For example, you can use this [deployment .yaml file ![External link icon](../icons/launch-glyph.svg "External link icon")](https://github.com/IBM-Cloud/kube-samples/blob/master/deploy-apps-clusters/deploy-syslog-from-kube.yaml) to fetch a Docker public image that runs a container in your cluster. The image publishes the port `514` on the public cluster IP address, and uses this public cluster IP address to configure the syslog host.

  You can see your logs as valid JSON by removing syslog prefixes. To do so, add the following code to the top of your <code>etc/rsyslog.conf</code> file where your rsyslog server is running: <code>$template customFormat,"%msg%\n"</br>$ActionFileDefaultTemplate customFormat</code>
  {: tip}

4. Create a log forwarding configuration.
    ```
    ibmcloud ks logging-config-create --cluster <cluster_name_or_ID> --logsource <log_source> --namespace <kubernetes_namespace> --hostname <log_server_hostname_or_IP> --port <log_server_port> --type syslog --app-containers <containers> --app-paths <paths_to_logs> --syslog-protocol <protocol> --skip-validation
    ```
    {: pre}

</br></br>

**Forwarding logs to your own server over the `tls` protocol**

The following steps are general instructions. Prior to using the container in a production environment, be sure that any security requirements that you need, are met.
{: tip}

1. Ensure that you have the following [{{site.data.keyword.cloud_notm}} IAM roles](/docs/containers?topic=containers-users#platform):
    * **Editor** or **Administrator** platform role for the cluster
    * **Writer** or **Manager** service role for the `kube-system` namespace

2. For the cluster where the log source is located: [Log in to your account. If applicable, target the appropriate resource group. Set the context for your cluster.](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure)

3. Set up a server that accepts a syslog protocol in 1 of 2 ways:
  * Set up and manage your own server or have a provider manage it for you. If a provider manages the server for you, get the logging endpoint from the logging provider.

  * Run syslog from a container. For example, you can use this [deployment .yaml file ![External link icon](../icons/launch-glyph.svg "External link icon")](https://github.com/IBM-Cloud/kube-samples/blob/master/deploy-apps-clusters/deploy-syslog-from-kube.yaml) to fetch a Docker public image that runs a container in your cluster. The image publishes the port `514` on the public cluster IP address, and uses this public cluster IP address to configure the syslog host. You need to inject the relevant Certificate Authority and server-side certificates and update the `syslog.conf` to enable `tls` on your server.

4. Save your Certificate Authority certificate to a file named `ca-cert`. It must be that exact name.

5. Create a secret in the `kube-system` namespace for the `ca-cert` file. When you create your logging configuration, use the secret name for the `--ca-cert` flag.
    ```
    kubectl -n kube-system create secret generic --from-file=ca-cert
    ```
    {: pre}

6. Create a log forwarding configuration.
    ```
    ibmcloud ks logging-config-create --cluster <cluster name or id> --logsource <log source> --type syslog --syslog-protocol tls --hostname <ip address of syslog server> --port <port for syslog server, 514 is default> --ca-cert <secret name> --verify-mode <defaults to verify-none>
    ```
    {: pre}

### Forwarding Kubernetes API audit logs
{: #audit_enable}

To audit any events that are passed through your Kubernetes API server, you can create a configuration to forward events to your external server.
{: shortdesc}

For more information about Kubernetes audit logs, see the <a href="https://kubernetes.io/docs/tasks/debug-application-cluster/audit/" target="blank">auditing topic <img src="../icons/launch-glyph.svg" alt="External link icon"></a> in the Kubernetes documentation.

* Currently, a default audit policy is used for all clusters with this logging configuration.
* Currently, filters are not supported.
* There can be only one `kube-audit` configuration per cluster, but you can forward logs to {{site.data.keyword.cloudaccesstrailshort}} and an external server by creating a logging configuration and a webhook.
* You must have the [**Administrator** {{site.data.keyword.cloud_notm}} IAM platform role](/docs/containers?topic=containers-users#platform) for the cluster.

**Before you begin**

1. Set up a remote logging server where you can forward the logs. For example, you can [use Logstash with Kubernetes ![External link icon](../icons/launch-glyph.svg "External link icon")](https://kubernetes.io/docs/tasks/debug-application-cluster/audit/#use-logstash-to-collect-and-distribute-audit-events-from-webhook-backend) to collect audit events.

2. For the cluster that you want to collect API server audit logs from: [Log in to your account. If applicable, target the appropriate resource group. Set the context for your cluster.](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure)

To forward Kubernetes API audit logs:

1. Set up the webhook. If you do not provide any information in the flags, a default configuration is used.

    ```
    ibmcloud ks apiserver-config-set audit-webhook <cluster_name_or_ID> --remoteServer <server_URL_or_IP> --caCert <CA_cert_path> --clientCert <client_cert_path> --clientKey <client_key_path>
    ```
    {: pre}

  <table>
  <caption>Understanding this command's components</caption>
    <thead>
      <th colspan=2><img src="images/idea.png" alt="Idea icon"/> Understanding this command's components</th>
    </thead>
    <tbody>
      <tr>
        <td><code><em>&lt;cluster_name_or_ID&gt;</em></code></td>
        <td>The name or ID of the cluster.</td>
      </tr>
      <tr>
        <td><code><em>&lt;server_URL&gt;</em></code></td>
        <td>The URL or IP address for the remote logging service that you want to send logs to. Certificates are ignored if you provide an unsecure server URL.</td>
      </tr>
      <tr>
        <td><code><em>&lt;CA_cert_path&gt;</em></code></td>
        <td>The file path for the CA certificate that is used to verify the remote logging service.</td>
      </tr>
      <tr>
        <td><code><em>&lt;client_cert_path&gt;</em></code></td>
        <td>The file path for the client certificate that is used to authenticate against the remote logging service.</td>
      </tr>
      <tr>
        <td><code><em>&lt;client_key_path&gt;</em></code></td>
        <td>The file path for the corresponding client key that is used to connect to the remote logging service.</td>
      </tr>
    </tbody>
  </table>

2. Verify that log forwarding was enabled by viewing the URL for the remote logging service.

    ```
    ibmcloud ks apiserver-config-get audit-webhook <cluster_name_or_ID>
    ```
    {: pre}

    Example output:
    ```
    OK
    Server:			https://8.8.8.8
    ```
    {: screen}

3. Apply the configuration update by restarting the Kubernetes master.

    ```
    ibmcloud ks apiserver-refresh --cluster <cluster_name_or_ID>
    ```
    {: pre}

4. Optional: If you want to stop forwarding audit logs, you can disable your configuration.
    1. For the cluster that you want to stop collecting API server audit logs from: [Log in to your account. If applicable, target the appropriate resource group. Set the context for your cluster.](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure)
    2. Disable the webhook back-end configuration for the cluster's API server.

        ```
        ibmcloud ks apiserver-config-unset audit-webhook <cluster_name_or_ID>
        ```
        {: pre}

    3. Apply the configuration update by restarting the Kubernetes master.

        ```
        ibmcloud ks apiserver-refresh --cluster <cluster_name_or_ID>
        ```
        {: pre}

### Filtering logs that are forwarded
{: #filter-logs}

You can choose which logs to forward to your external server by filtering out specific logs for a period of time. You can differentiate between the different filtering options by using flags.
{: shortdesc}

<table>
<caption>Understanding the options for log filtering</caption>
  <thead>
    <th colspan=2><img src="images/idea.png" alt="Idea icon"/> Understanding log filtering options</th>
  </thead>
  <tbody>
    <tr>
      <td>&lt;cluster_name_or_ID&gt;</td>
      <td>Required: The name or ID of the cluster that you want to filter logs for.</td>
    </tr>
    <tr>
      <td><code>&lt;log_type&gt;</code></td>
      <td>The type of logs that you want to apply the filter to. Currently <code>all</code>, <code>container</code>, and <code>host</code> are supported.</td>
    </tr>
    <tr>
      <td><code>&lt;configs&gt;</code></td>
      <td>Optional: A comma-separated list of your logging configuration IDs. If not provided, the filter is applied to all of the cluster logging configurations that are passed to the filter. You can view log configurations that match the filter by using the <code>--show-matching-configs</code> option.</td>
    </tr>
    <tr>
      <td><code>&lt;kubernetes_namespace&gt;</code></td>
      <td>Optional: The Kubernetes namespace that you want to forward logs from. This flag applies only when you are using log type <code>container</code>.</td>
    </tr>
    <tr>
      <td><code>&lt;container_name&gt;</code></td>
      <td>Optional: The name of the container from which you want to filter logs.</td>
    </tr>
    <tr>
      <td><code>&lt;logging_level&gt;</code></td>
      <td>Optional: Filters out logs that are at the specified level and less. Acceptable values in their canonical order are <code>fatal</code>, <code>error</code>, <code>warn/warning</code>, <code>info</code>, <code>debug</code>, and <code>trace</code>. As an example, if you filtered logs at the <code>info</code> level, <code>debug</code>, and <code>trace</code> are also filtered. **Note**: You can use this flag only when log messages are in JSON format and contain a level field. To display your messages in JSON, append the <code>--json</code> flag to the command.</td>
    </tr>
    <tr>
      <td><code>&lt;message&gt;</code></td>
      <td>Optional: Filters out logs that contain a specified message that is written as a regular expression.</td>
    </tr>
    <tr>
      <td><code>&lt;filter_ID&gt;</code></td>
      <td>Optional: The ID of the log filter.</td>
    </tr>
    <tr>
      <td><code>--show-matching-configs</code></td>
      <td>Optional: Show the logging configurations that each filter applies to.</td>
    </tr>
    <tr>
      <td><code>--all</code></td>
      <td>Optional: Delete all of your log forwarding filters.</td>
    </tr>
  </tbody>
</table>

1. Create a logging filter.
  ```
  ibmcloud ks logging-filter-create --cluster <cluster_name_or_ID> --type <log_type> --logging-configs <configs> --namespace <kubernetes_namespace> --container <container_name> --level <logging_level> --regex-message <message>
  ```
  {: pre}

2. View the log filter that you created.

  ```
  ibmcloud ks logging-filter-get --cluster <cluster_name_or_ID> --id <filter_ID> --show-matching-configs
  ```
  {: pre}

3. Update the log filter that you created.
  ```
  ibmcloud ks logging-filter-update --cluster <cluster_name_or_ID> --id <filter_ID> --type <server_type> --logging-configs <configs> --namespace <kubernetes_namespace --container <container_name> --level <logging_level> --regex-message <message>
  ```
  {: pre}

4. Delete a log filter that you created.

  ```
  ibmcloud ks logging-filter-rm --cluster <cluster_name_or_ID> --id <filter_ID> [--all]
  ```
  {: pre}

### Verifying, updating, and deleting log forwarding
{: #verifying-log-forwarding}

**Verifying**</br>
You can verify that your configuration is set up correctly in 1 of 2 ways:

* To list all of the logging configurations in a cluster:
  ```
  ibmcloud ks logging-config-get --cluster <cluster_name_or_ID>
  ```
  {: pre}

* To list the logging configurations for one type of log source:
  ```
  ibmcloud ks logging-config-get --cluster <cluster_name_or_ID> --logsource <source>
  ```
  {: pre}

**Updating**</br>
You can update a logging configuration that you already created:
```
ibmcloud ks logging-config-update --cluster <cluster_name_or_ID> --id <log_config_id> --namespace <namespace> --type <server_type> --syslog-protocol <protocol> --logsource <source> --hostname <hostname_or_ingestion_URL> --port <port> --space <cluster_space> --org <cluster_org> --app-containers <containers> --app-paths <paths_to_logs>
```
{: pre}

**Deleting**</br>
You can stop forwarding logs by deleting one or all of the logging configurations for a cluster:

* To delete one logging configuration:
  ```
  ibmcloud ks logging-config-rm --cluster <cluster_name_or_ID> --id <log_config_ID>
  ```
  {: pre}

* To delete all of the logging configurations:
  ```
  ibmcloud ks logging-config-rm --cluster <my_cluster> --all
  ```
  {: pre}

<br />


## Forwarding Kubernetes API audit logs to {{site.data.keyword.cloudaccesstrailfull_notm}}
{: #api_forward}

Kubernetes automatically audits any events that are passed through your Kubernetes API server. You can forward the events to {{site.data.keyword.cloudaccesstrailfull_notm}}.
{: shortdesc}

For more information about Kubernetes audit logs, see the <a href="https://kubernetes.io/docs/tasks/debug-application-cluster/audit/" target="blank">auditing topic <img src="../icons/launch-glyph.svg" alt="External link icon"></a> in the Kubernetes documentation.

* Currently, a default audit policy is used for all clusters with this logging configuration.
* Currently, filters are not supported.
* There can be only one `kube-audit` configuration per cluster, but you can forward logs to {{site.data.keyword.cloudaccesstrailshort}} and an external server by creating a logging configuration and a webhook.
* You must have the [**Administrator** {{site.data.keyword.cloud_notm}} IAM platform role](/docs/containers?topic=containers-users#platform) for the cluster.

{{site.data.keyword.containerlong_notm}} is currently not configured to use {{site.data.keyword.at_full}}. To manage Kubernetes API audit logs, continue to use {{site.data.keyword.cloudaccesstrailfull_notm}} with LogAnalysis.
{: note}

**Before you begin**

1. Verify permissions. If you specified a space when you created the cluster, then both the account owner and {{site.data.keyword.containerlong_notm}} key owner need Manager, Developer, or Auditor permissions in that space.

2. For the cluster that you want to collect API server audit logs from: [Log in to your account. If applicable, target the appropriate resource group. Set the context for your cluster.](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure)

**Forwarding logs**

1. Create a logging configuration.

    ```
    ibmcloud ks logging-config-create --cluster <cluster_name_or_ID> --logsource kube-audit --space <cluster_space> --org <cluster_org> --hostname <ingestion_URL> --type ibm
    ```
    {: pre}

    Example command and output:

    ```
    ibmcloud ks logging-config-create --cluster myCluster --logsource kube-audit
    Creating logging configuration for kube-audit logs in cluster myCluster...
    OK
    Id                                     Source      Namespace   Host                                   Port     Org    Space   Server Type   Protocol  Application Containers   Paths
    14ca6a0c-5bc8-499a-b1bd-cedcf40ab850   kube-audit    -         ingest-au-syd.logging.bluemix.net✣    9091✣     -       -         ibm          -              -                  -

    ✣ Indicates the default endpoint for the {{site.data.keyword.loganalysisshort_notm}} service.

    ```
    {: screen}

    <table>
    <caption>Understanding this command's components</caption>
      <thead>
        <th colspan=2><img src="images/idea.png" alt="Idea icon"/> Understanding this command's components</th>
      </thead>
      <tbody>
        <tr>
          <td><code><em>&lt;cluster_name_or_ID&gt;</em></code></td>
          <td>The name or ID of the cluster.</td>
        </tr>
        <tr>
          <td><code><em>&lt;ingestion_URL&gt;</em></code></td>
          <td>The endpoint where you want to forward logs. If you do not specify an [ingestion URL](/docs/services/CloudLogAnalysis?topic=cloudloganalysis-log_ingestion#log_ingestion_urls), the endpoint for the region in which you created your cluster is used.</td>
        </tr>
        <tr>
          <td><code><em>&lt;cluster_space&gt;</em></code></td>
          <td>Optional: The name of the Cloud Foundry space that you want to send logs to. When forwarding logs to {{site.data.keyword.loganalysisshort_notm}}, the space and org are specified in the ingestion point. If you do not specify a space, logs are sent to the account level.</td>
        </tr>
        <tr>
          <td><code><em>&lt;cluster_org&gt;</em></code></td>
          <td>The name of the Cloud Foundry org that the space is in. This value is required if you specified a space.</td>
        </tr>
      </tbody>
    </table>

2. View your cluster logging configuration to verify that it was implemented the way that you intended.

    ```
    ibmcloud ks logging-config-get --cluster <cluster_name_or_ID>
    ```
    {: pre}

    Example command and output:
    ```
    ibmcloud ks logging-config-get --cluster myCluster
    Retrieving cluster myCluster logging configurations...
    OK
    Id                                     Source        Namespace   Host                                 Port    Org   Space   Server Type  Protocol  Application Containers   Paths
    a550d2ba-6a02-4d4d-83ef-68f7a113325c   container     *           ingest-au-syd.logging.bluemix.net✣  9091✣   -     -         ibm           -          -              -
    14ca6a0c-5bc8-499a-b1bd-cedcf40ab850   kube-audit    -           ingest-au-syd.logging.bluemix.net✣  9091✣   -     -         ibm           -          -              -       
    ```
    {: screen}

3. To view the Kubernetes API audit events that you forward:
  1. Log in to your {{site.data.keyword.cloud_notm}} account.
  2. From the catalog, provision an instance of the {{site.data.keyword.cloudaccesstrailshort}} service in the same account as your instance of {{site.data.keyword.containerlong_notm}}.
  3. On the **Manage** tab of the {{site.data.keyword.cloudaccesstrailshort}} dashboard, select the account or space domain.
    * **Account logs**: Cluster management events and Kubernetes API server audit events are available in the **account domain** for the {{site.data.keyword.cloud_notm}} region where the events are generated.
    * **Space logs**: If you specified a space when you configured your logging configuration in step 2, these events are available in the **space domain** that is associated with the Cloud Foundry space where the {{site.data.keyword.cloudaccesstrailshort}} service is provisioned.
  4. Click **View in Kibana**.
  5. Set the time frame that you want to view logs for. The default is 24 hours.
  6. To narrow your search, you can click the edit icon for `ActivityTracker_Account_Search_in_24h` and add fields in the **Available Fields** column.

  To let other users view account and space events, see [Granting permissions to see account events](/docs/services/cloud-activity-tracker/how-to?topic=cloud-activity-tracker-grant_permissions#grant_permissions).
  {: tip}

<br />


## Collecting master logs in an {{site.data.keyword.cos_full_notm}} bucket
{: #collect_master}

With {{site.data.keyword.containerlong_notm}}, you can take a snapshot of your master logs at any point in time to collect in an {{site.data.keyword.cos_full_notm}} bucket. The snapshot includes anything that is sent through the API server, such as pod scheduling, deployments, or RBAC policies.
{: shortdesc}

Because Kubernetes API Server logs are automatically streamed, they're also automatically deleted to make room for the new logs coming in. By keeping a snapshot of logs at a specific point in time, you can better troubleshoot issues, look into usage differences, and find patterns to help maintain more secure applications.

**Before you begin**

* [Provision an instance](/docs/services/cloud-object-storage/basics?topic=cloud-object-storage-gs-dev) of {{site.data.keyword.cos_short}} from the {{site.data.keyword.cloud_notm}} catalog.
* Ensure that you have the [**Administrator** {{site.data.keyword.cloud_notm}} IAM platform role](/docs/containers?topic=containers-users#platform) for the cluster.

**Creating a snapshot**

1. Create an Object Storage bucket through the {{site.data.keyword.cloud_notm}} console by following [this getting started tutorial](/docs/services/cloud-object-storage?topic=cloud-object-storage-getting-started#gs-create-buckets).

2. Generate [HMAC service credentials](/docs/services/cloud-object-storage/iam?topic=cloud-object-storage-service-credentials) in the bucket that you created.
  1. In the **Service Credentials** tab of the {{site.data.keyword.cos_short}} dashboard, click **New Credential**.
  2. Give the HMAC credentials the `Writer` service role.
  3. In the **Add Inline Configuration Parameters** field, specify `{"HMAC":true}`.

3. Through the CLI, make a request for a snapshot of your master logs.

  ```
  ibmcloud ks logging-collect --cluster <cluster name or ID> --cos-bucket <COS_bucket_name> --cos-endpoint <location_of_COS_bucket> --hmac-key-id <HMAC_access_key_ID> --hmac-key <HMAC_access_key>
  ```
  {: pre}

  <table>
  <caption>Understanding this command's components</caption>
    <thead>
      <th colspan=2><img src="images/idea.png" alt="Idea icon"/> Understanding this command's components</th>
    </thead>
    <tbody>
      <tr>
        <td><code>--cluster <em>&lt;cluster_name_or_ID&gt;</em></code></td>
        <td>The name or ID of the cluster.</td>
      </tr>
      <tr>
        <td><code>--cos-bucket <em>&lt;COS_bucket_name&gt;</em></code></td>
        <td>The name of the {{site.data.keyword.cos_short}} bucket that you want to store your logs in.</td>
      </tr>
      <tr>
        <td><code>--cos-endpoint <em>&lt;location_of_COS_bucket&gt;</em></code></td>
        <td>The regional, cross regional, or single data center {{site.data.keyword.cos_short}} endpoint for the bucket that you are storing your logs in. For available endpoints, see [Endpoints and storage locations](/docs/services/cloud-object-storage/basics?topic=cloud-object-storage-endpoints) in the {{site.data.keyword.cos_short}} documentation.</td>
      </tr>
      <tr>
        <td><code>--hmac-key-id <em>&lt;HMAC_access_key_ID&gt;</em></code></td>
        <td>The unique ID for your HMAC credentials for your {{site.data.keyword.cos_short}} instance.</td>
      </tr>
      <tr>
        <td><code>--hmac-key <em>&lt;HMAC_access_key&gt;</em></code></td>
        <td>The HMAC key for your {{site.data.keyword.cos_short}} instance.</td>
      </tr>
    </tbody>
  </table>

  Example command and response:

  ```
  ibmcloud ks logging-collect --cluster mycluster --cos-bucket mybucket --cos-endpoint s3-api.us-geo.objectstorage.softlayer.net --hmac-key-id e2e7f5c9fo0144563c418dlhi3545m86 --hmac-key c485b9b9fo4376722f692b63743e65e1705301ab051em96j
  There is no specified log type. The default master will be used.
  Submitting log collection request for master logs for cluster mycluster...
  OK
  The log collection request was successfully submitted. To view the status of the request run ibmcloud ks logging-collect-status mycluster.
  ```
  {: screen}

4. Check the status of your request. It can take some time for the snapshot to complete, but you can check to see whether your request is successfully being completed or not. You can find the name of the file that contains your master logs in the response and use the {{site.data.keyword.cloud_notm}} console to download the file.

  ```
  ibmcloud ks logging-collect-status --cluster <cluster_name_or_ID>
  ```
  {: pre}

  Example output:

  ```
  ibmcloud ks logging-collect-status --cluster mycluster
  Getting the status of the last log collection request for cluster mycluster...
  OK
  State     Start Time             Error   Log URLs
  success   2018-09-18 16:49 PDT   - s3-api.us-geo.objectstorage.softlayer.net/mybucket/master-0-0862ae70a9ae6c19845ba3pc0a2a6o56-1297318756.tgz
  s3-api.us-geo.objectstorage.softlayer.net/mybucket/master-1-0862ae70a9ae6c19845ba3pc0a2a6o56-1297318756.tgz
  s3-api.us-geo.objectstorage.softlayer.net/mybucket/master-2-0862ae70a9ae6c19845ba3pc0a2a6o56-1297318756.tgz
  ```
  {: screen}

<br />


## Choosing a monitoring solution
{: #view_metrics}

Metrics help you monitor the health and performance of your clusters. You can use the standard Kubernetes and container runtime features to monitor the health of your clusters and apps. **Note**: Monitoring is supported only for standard clusters.
{:shortdesc}

**Does IBM monitor my cluster?**

Every Kubernetes master is continuously monitored by IBM. {{site.data.keyword.containerlong_notm}} automatically scans every node where the Kubernetes master is deployed for vulnerabilities that are found in Kubernetes and OS-specific security fixes. If vulnerabilities are found, {{site.data.keyword.containerlong_notm}} automatically applies fixes and resolves vulnerabilities on behalf of the user to ensure master node protection. You are responsible for monitoring and analyzing the logs for the rest of your cluster components.

To avoid conflicts when using metrics services, be sure that clusters across resource groups and regions have unique names.
{: tip}

<dl>
  <dt>{{site.data.keyword.mon_full_notm}}</dt>
    <dd>Gain operational visibility into the performance and health of your apps by deploying Sysdig as a third-party service to your worker nodes to forward metrics to {{site.data.keyword.monitoringlong}}. For more information, see [Analyzing metrics for an app that is deployed in a Kubernetes cluster](/docs/services/Monitoring-with-Sysdig/tutorials?topic=Sysdig-kubernetes_cluster#kubernetes_cluster).</dd>

  <dt>Kubernetes dashboard</dt>
    <dd>The Kubernetes dashboard is an administrative web interface where you can review the health of your worker nodes, find Kubernetes resources, deploy containerized apps, and troubleshoot apps with logging and monitoring information. For more information about how to access your Kubernetes dashboard, see [Launching the Kubernetes dashboard for {{site.data.keyword.containerlong_notm}}](/docs/containers?topic=containers-app#cli_dashboard).</dd>

  <dt>Deprecated: Metrics dashboard in cluster overview page of {{site.data.keyword.cloud_notm}} console and output of <code>ibmcloud ks cluster-get</code></dt>
    <dd>{{site.data.keyword.containerlong_notm}} provides information about the health and capacity of your cluster and the usage of your cluster resources. You can use this console to scale out your cluster, work with your persistent storage, and add more capabilities to your cluster through {{site.data.keyword.cloud_notm}} service binding. To view metrics, go to the **Kubernetes** > **Clusters** dashboard, select a cluster, and click the **Metrics** link.
  <p class="deprecated">The link to the metrics dashboard in the cluster overview page of the {{site.data.keyword.cloud_notm}} console and in the output of `ibmcloud ks cluster-get` is deprecated. Clusters that are created after 03 May 2019 are not created with the metrics dashboard link. Clusters that are created on or before 03 May 2019 continue to have the link to the metrics dashboard.</p></dd>

  <dt>{{site.data.keyword.monitoringlong_notm}}</dt>
    <dd><p>Metrics for standard clusters are located in the {{site.data.keyword.cloud_notm}} account that was logged in to when the Kubernetes cluster was created. If you specified an {{site.data.keyword.cloud_notm}} space when you created the cluster, then metrics are located in that space. Container metrics are collected automatically for all containers that are deployed in a cluster. These metrics are sent and are made available through Grafana. For more information about metrics, see [Monitoring for the {{site.data.keyword.containerlong_notm}}](/docs/services/cloud-monitoring/containers?topic=cloud-monitoring-monitoring_bmx_containers_ov#monitoring_bmx_containers_ov).</p>
    <p>To access the Grafana dashboard, go to one of the following URLs and select the {{site.data.keyword.cloud_notm}} account or space where you created the cluster.</p>
    <table summary="The first row in the table spans both columns. The rest of the rows should be read left to right, with the server zone in column one and IP addresses to match in column two.">
      <caption>IP addresses to open for monitoring traffic</caption>
            <thead>
            <th>{{site.data.keyword.containerlong_notm}} region</th>
            <th>Monitoring address</th>
            <th>Monitoring subnets</th>
            </thead>
          <tbody>
            <tr>
             <td>EU Central</td>
             <td><code>metrics.eu-de.bluemix.net</code></td>
             <td><code>158.177.65.80/30</code></td>
            </tr>
            <tr>
             <td>UK South</td>
             <td><code>metrics.eu-gb.bluemix.net</code></td>
             <td><code>169.50.196.136/29</code></td>
            </tr>
            <tr>
              <td>US East, US South, AP North, AP South</td>
              <td><code>metrics.ng.bluemix.net</code></td>
              <td><code>169.47.204.128/29</code></td>
             </tr>
            </tbody>
          </table> </dd>
</dl>

### Other health monitoring tools
{: #health_tools}

You can configure other tools for more monitoring capabilities.
<dl>
  <dt>Prometheus</dt>
    <dd>Prometheus is an open source monitoring, logging, and alerting tool that was designed for Kubernetes. The tool retrieves detailed information about the cluster, worker nodes, and deployment health based on the Kubernetes logging information. For more information about the setup, see the [CoreOS instructions ![External link icon](../icons/launch-glyph.svg "External link icon")](https://github.com/coreos/prometheus-operator/tree/master/contrib/kube-prometheus).</dd>
</dl>

<br />




## Viewing cluster states
{: #states}

Review the state of a Kubernetes cluster to get information about the availability and capacity of the cluster, and potential problems that might occur.
{:shortdesc}

To view information about a specific cluster, such as its zones, service endpoint URLs, Ingress subdomain, version, and owner, use the `ibmcloud ks cluster-get --cluster <cluster_name_or_ID>` [command](/docs/containers?topic=containers-cli-plugin-kubernetes-service-cli#cs_cluster_get). Include the `--showResources` flag to view more cluster resources such as add-ons for storage pods or subnet VLANs for public and private IPs.

You can review information about the overall cluster, the IBM-managed master, and your worker nodes. To troubleshoot your cluster and worker nodes, see [Troubleshooting clusters](/docs/containers?topic=containers-cs_troubleshoot#debug_clusters).

### Cluster states
{: #states_cluster}

You can view the current cluster state by running the `ibmcloud ks clusters` command and locating the **State** field. 
{: shortdesc}

<table summary="Every table row should be read left to right, with the cluster state in column one and a description in column two.">
<caption>Cluster states</caption>
   <thead>
   <th>Cluster state</th>
   <th>Description</th>
   </thead>
   <tbody>
<tr>
   <td>`Aborted`</td>
   <td>The deletion of the cluster is requested by the user before the Kubernetes master is deployed. After the deletion of the cluster is completed, the cluster is removed from your dashboard. If your cluster is stuck in this state for a long time, open an [{{site.data.keyword.cloud_notm}} support case](/docs/containers?topic=containers-cs_troubleshoot#ts_getting_help).</td>
   </tr>
 <tr>
     <td>`Critical`</td>
     <td>The Kubernetes master cannot be reached or all worker nodes in the cluster are down. If you enabled {{site.data.keyword.keymanagementservicelong_notm}} in your cluster, the {{site.data.keyword.keymanagementserviceshort}} container might fail to encrypt or decrypt your cluster secrets. If so, you can view an error with more information when you run `{[kubectl]} get secrets`.</td>
    </tr>
   <tr>
     <td>`Delete failed`</td>
     <td>The Kubernetes master or at least one worker node cannot be deleted.  </td>
   </tr>
   <tr>
     <td>`Deleted`</td>
     <td>The cluster is deleted but not yet removed from your dashboard. If your cluster is stuck in this state for a long time, open an [{{site.data.keyword.cloud_notm}} support case](/docs/containers?topic=containers-cs_troubleshoot#ts_getting_help). </td>
   </tr>
   <tr>
   <td>`Deleting`</td>
   <td>The cluster is being deleted and cluster infrastructure is being dismantled. You cannot access the cluster.  </td>
   </tr>
   <tr>
     <td>`Deploy failed`</td>
     <td>The deployment of the Kubernetes master could not be completed. You cannot resolve this state. Contact IBM Cloud support by opening an [{{site.data.keyword.cloud_notm}} support case](/docs/containers?topic=containers-cs_troubleshoot#ts_getting_help).</td>
   </tr>
     <tr>
       <td>`Deploying`</td>
       <td>The Kubernetes master is not fully deployed yet. You cannot access your cluster. Wait until your cluster is fully deployed to review the health of your cluster.</td>
      </tr>
      <tr>
       <td>`Normal`</td>
       <td>All worker nodes in a cluster are up and running. You can access the cluster and deploy apps to the cluster. This state is considered healthy and does not require an action from you.<p class="note">Although the worker nodes might be normal, other infrastructure resources, such as [networking](/docs/containers?topic=containers-cs_troubleshoot_network) and [storage](/docs/containers?topic=containers-cs_troubleshoot_storage), might still need attention. If you just created the cluster, some parts of the cluster that are used by other services such as Ingress secrets or registry image pull secrets, might still be in process.</p></td>
    </tr>
      <tr>
       <td>`Pending`</td>
       <td>The Kubernetes master is deployed. The worker nodes are being provisioned and are not available in the cluster yet. You can access the cluster, but you cannot deploy apps to the cluster.  </td>
     </tr>
   <tr>
     <td>`Requested`</td>
     <td>A request to create the cluster and order the infrastructure for the Kubernetes master and worker nodes is sent. When the deployment of the cluster starts, the cluster state changes to <code>Deploying</code>. If your cluster is stuck in the <code>Requested</code> state for a long time, open an [{{site.data.keyword.cloud_notm}} support case](/docs/containers?topic=containers-cs_troubleshoot#ts_getting_help). </td>
   </tr>
   <tr>
     <td>`Updating`</td>
     <td>The Kubernetes API server that runs in your Kubernetes master is being updated to a new Kubernetes API version. During the update, you cannot access or change the cluster. Worker nodes, apps, and resources that the user deployed are not modified and continue to run. Wait for the update to complete to review the health of your cluster. </td>
   </tr>
   <tr>
    <td>`Unsupported`</td>
    <td>The [Kubernetes version](/docs/containers?topic=containers-cs_versions#cs_versions) that the cluster runs is no longer supported. Your cluster's health is no longer actively monitored or reported. Additionally, you cannot add or reload worker nodes. To continue receiving important security updates and support, you must update your cluster. Review the [version update preparation actions](/docs/containers?topic=containers-cs_versions#prep-up), then [update your cluster](/docs/containers?topic=containers-update#update) to a supported Kubernetes version.<br><br><p class="note">Clusters that are three or more versions behind the oldest supported version cannot be updated. To avoid this situation, you can update the cluster to a Kubernetes version less than three ahead of the current version, such as 1.12 to 1.14. Further, if your cluster runs version 1.5, 1.7, or 1.8, then the version is too far behind to update. Instead, you must [create a cluster](/docs/containers?topic=containers-clusters#clusters) and [deploy your apps](/docs/containers?topic=containers-app#app) to the cluster.</p></td>
   </tr>
    <tr>
       <td>`Warning`</td>
       <td><ul><li>At least one worker node in the cluster is not available, but other worker nodes are available and can take over the workload. Try to [reload](/docs/containers?topic=containers-cli-plugin-kubernetes-service-cli#cs_worker_reload) the unavailable worker nodes.</li>
       <li>Your cluster has zero worker nodes, such as if you created a cluster without any worker nodes or manually removed all the worker nodes from the cluster. [Resize your worker pool](/docs/containers?topic=containers-add_workers#resize_pool) to add worker nodes to recover from a `Warning` state.</li>
       <li>A control plane operation for your cluster failed. View the cluster in the console or run `ibmcloud ks cluster-get --cluster <cluster_name_or_ID>` to [check the **Master Status** for further debugging](/docs/containers?topic=containers-cs_troubleshoot#debug_master).</li></ul></td>
    </tr>
   </tbody>
 </table>




### Master states
{: #states_master}

Your {{site.data.keyword.containerlong_notm}} includes an IBM-managed master with highly available replicas, automatic security patch updates applied for you, and automation in place to recover in case of an incident. You can check the health, status, and state of the cluster master by running `ibmcloud ks cluster-get --cluster <cluster_name_or_ID>`.
{: shortdesc} 

**Master Health**<br>
The **Master Health** reflects the state of master components and notifies you if something needs your attention. The health might be one of the following:
*   `error`: The master is not operational. IBM is automatically notified and takes action to resolve this issue. You can continue monitoring the health until the master is `normal`.
*   `normal`: The master is operational and healthy. No action is required.
*   `unavailable`: The master might not be accessible, which means some actions such as resizing a worker pool are temporarily unavailable. IBM is automatically notified and takes action to resolve this issue. You can continue monitoring the health until the master is `normal`. 
*   `unsupported`: The master runs an unsupported version of Kubernetes. You must [update your cluster](/docs/containers?topic=containers-update) to return the master to `normal` health.

**Master Status and State**<br>
The **Master Status** provides details of what operation from the master state is in progress. The status includes a timestamp of how long the master has been in the same state, such as `Ready (1 month ago)`. The **Master State** reflects the lifecycle of possible operations that can be performed on the master, such as deploying, updating, and deleting. Each state is described in the following table.

<table summary="Every table row should be read left to right, with the master state in column one and a description in column two.">
<caption>Master states</caption>
   <thead>
   <th>Master state</th>
   <th>Description</th>
   </thead>
   <tbody>
<tr>
   <td>`deployed`</td>
   <td>The master is successfully deployed. Check the status to verify that the master is `Ready` or to see if an update is available.</td>
   </tr>
 <tr>
     <td>`deploying`</td>
     <td>The master is currently deploying. Wait for the state to become `deployed` before working with your cluster, such as adding worker nodes.</td>
    </tr>
   <tr>
     <td>`deploy_failed`</td>
     <td>The master failed to deploy. IBM Support is notified and works to resolve the issue. Check the **Master Status** field for more information, or wait for the state to become `deployed`.</td>
   </tr>
   <tr>
   <td>`deleting`</td>
   <td>The master is currently deleting because you deleted the cluster. You cannot undo a deletion. After the cluster is deleted, you can no longer check the master state because the cluster is completely removed.</td>
   </tr>
     <tr>
       <td>`delete_failed`</td>
       <td>The master failed to delete. IBM Support is notified and works to resolve the issue. You cannot resolve the issue by trying to delete the cluster again. Instead, check the **Master Status** field for more information, or wait for the cluster to delete.</td>
      </tr>
      <tr>
       <td>`updating`</td>
       <td>The master is updating its Kubernetes version. The update might be a patch update that is automatically applied, or a minor or major version that you applied by updating the cluster. During the update, your highly available master can continue processing requests, and your app workloads and worker nodes continue to run. After the master update is complete, you can [update your worker nodes](/docs/containers?topic=containers-update#worker_node).<br><br>
       If the update is unsuccessful, the master returns to a `deployed` state and continues running the previous version. IBM Support is notified and works to resolve the issue. You can check if the update failed in the **Master Status** field.</td>
    </tr>
   </tbody>
 </table>




### Worker node states
{: #states_workers}

You can view the current worker node state by running the `ibmcloud ks workers --cluster <cluster_name_or_ID` command and locating the **State** and **Status** fields.
{: shortdesc}

<table summary="Every table row should be read left to right, with the cluster state in column one and a description in column two.">
<caption>Worker node states</caption>
  <thead>
  <th>Worker node state</th>
  <th>Description</th>
  </thead>
  <tbody>
<tr>
    <td>`Critical`</td>
    <td>A worker node can go into a Critical state for many reasons: <ul><li>You initiated a reboot for your worker node without cordoning and draining your worker node. Rebooting a worker node can cause data corruption in <code>containerd</code>, <code>kubelet</code>, <code>kube-proxy</code>, and <code>calico</code>. </li>
    <li>The pods that are deployed to your worker node do not use resource limits for [memory ![External link icon](../icons/launch-glyph.svg "External link icon")](https://kubernetes.io/docs/tasks/configure-pod-container/assign-memory-resource/) and [CPU ![External link icon](../icons/launch-glyph.svg "External link icon")](https://kubernetes.io/docs/tasks/configure-pod-container/assign-cpu-resource/). Without resource limits, pods can consume all available resources, leaving no resources for other pods to run on this worker node. This overcommitment of workload causes the worker node to fail. </li>
    <li><code>containerd</code>, <code>kubelet</code>, or <code>calico</code> went into an unrecoverable state after it ran hundreds or thousands of containers over time. </li>
    <li>You set up a Virtual Router Appliance for your worker node that went down and cut off the communication between your worker node and the Kubernetes master. </li><li> Current networking issues in {{site.data.keyword.containerlong_notm}} or IBM Cloud infrastructure that causes the communication between your worker node and the Kubernetes master to fail.</li>
    <li>Your worker node ran out of capacity. Check the <strong>Status</strong> of the worker node to see whether it shows <strong>Out of disk</strong> or <strong>Out of memory</strong>. If your worker node is out of capacity, consider to either reduce the workload on your worker node or add a worker node to your cluster to help load balance the workload.</li>
    <li>The device was powered off from the [{{site.data.keyword.cloud_notm}} console resource list ![External link icon](../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/resources). Open the resource list and find your worker node ID in the **Devices** list. In the action menu, click **Power On**.</li></ul>
    In many cases, [reloading](/docs/containers?topic=containers-cli-plugin-kubernetes-service-cli#cs_worker_reload) your worker node can solve the problem. When you reload your worker node, the latest [patch version](/docs/containers?topic=containers-cs_versions#version_types) is applied to your worker node. The major and minor version is not changed. Before you reload your worker node, make sure to cordon and drain your worker node to ensure that the existing pods are terminated gracefully and rescheduled onto remaining worker nodes. </br></br> If reloading the worker node does not resolve the issue, go to the next step to continue troubleshooting your worker node. </br></br><strong>Tip:</strong> You can [configure health checks for your worker node and enable Autorecovery](/docs/containers?topic=containers-health#autorecovery). If Autorecovery detects an unhealthy worker node based on the configured checks, Autorecovery triggers a corrective action like an OS reload on the worker node. For more information about how Autorecovery works, see the [Autorecovery blog ![External link icon](../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/blogs/bluemix/2017/12/autorecovery-utilizes-consistent-hashing-high-availability/).
    </td>
   </tr>
   <tr>
   <td>`Deployed`</td>
   <td>Updates are successfully deployed to your worker node. After updates are deployed, {{site.data.keyword.containerlong_notm}} starts a health check on the worker node. After the health check is successful, the worker node goes into a <code>Normal</code> state. Worker nodes in a <code>Deployed</code> state usually are ready to receive workloads, which you can check by running <code>{[kubectl]} get nodes</code> and confirming that the state shows <code>Normal</code>. </td>
   </tr>
    <tr>
      <td>`Deploying`</td>
      <td>When you update the Kubernetes version of your worker node, your worker node is redeployed to install the updates. If you reload or reboot your worker node, the worker node is redeployed to automatically install the latest patch version. If your worker node is stuck in this state for a long time, continue with the next step to see whether a problem occurred during the deployment. </td>
   </tr>
      <tr>
      <td>`Normal`</td>
      <td>Your worker node is fully provisioned and ready to be used in the cluster. This state is considered healthy and does not require an action from the user. **Note**: Although the worker nodes might be normal, other infrastructure resources, such as [networking](/docs/containers?topic=containers-cs_troubleshoot_network) and [storage](/docs/containers?topic=containers-cs_troubleshoot_storage), might still need attention.</td>
   </tr>
 <tr>
      <td>`Provisioning`</td>
      <td>Your worker node is being provisioned and is not available in the cluster yet. You can monitor the provisioning process in the <strong>Status</strong> column of your CLI output. If your worker node is stuck in this state for a long time, continue with the next step to see whether a problem occurred during the provisioning.</td>
    </tr>
    <tr>
      <td>`Provision_failed`</td>
      <td>Your worker node could not be provisioned. Continue with the next step to find the details for the failure.</td>
    </tr>
 <tr>
      <td>`Reloading`</td>
      <td>Your worker node is being reloaded and is not available in the cluster. You can monitor the reloading process in the <strong>Status</strong> column of your CLI output. If your worker node is stuck in this state for a long time, continue with the next step to see whether a problem occurred during the reloading.</td>
     </tr>
     <tr>
      <td>`Reloading_failed`</td>
      <td>Your worker node could not be reloaded. Continue with the next step to find the details for the failure.</td>
    </tr>
    <tr>
      <td>`Reload_pending`</td>
      <td>A request to reload or to update the Kubernetes version of your worker node is sent. When the worker node is being reloaded, the state changes to <code>Reloading</code>. </td>
    </tr>
    <tr>
     <td>`Unknown`</td>
     <td>The Kubernetes master is not reachable for one of the following reasons:<ul><li>You requested an update of your Kubernetes master. The state of the worker node cannot be retrieved during the update. If the worker node remains in this state for an extended period of time even after the Kubernetes master is successfully updated, try to [reload](/docs/containers?topic=containers-cli-plugin-kubernetes-service-cli#cs_worker_reload) the worker node.</li><li>You might have another firewall that is protecting your worker nodes, or changed firewall settings recently. {{site.data.keyword.containerlong_notm}} requires certain IP addresses and ports to be opened to allow communication from the worker node to the Kubernetes master and vice versa. For more information, see [Firewall prevents worker nodes from connecting](/docs/containers?topic=containers-cs_troubleshoot_clusters#cs_firewall).</li><li>The Kubernetes master is down. Contact {{site.data.keyword.cloud_notm}} support by opening an [{{site.data.keyword.cloud_notm}} support case](/docs/containers?topic=containers-cs_troubleshoot#ts_getting_help).</li></ul></td>
</tr>
   <tr>
      <td>`Warning`</td>
      <td>Your worker node is reaching the limit for memory or disk space. You can either reduce work load on your worker node or add a worker node to your cluster to help load balance the work load.</td>
</tr>
  </tbody>
</table>




## Configuring health monitoring for worker nodes with Autorecovery
{: #autorecovery}

The Autorecovery system uses various checks to query worker node health status. If Autorecovery detects an unhealthy worker node based on the configured checks, Autorecovery triggers a corrective action like an OS reload on the worker node. Only one worker node undergoes a corrective action at a time. The worker node must successfully complete the corrective action before any other worker node undergoes a corrective action. For more information, see this [Autorecovery blog post ![External link icon](../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/blogs/bluemix/2017/12/autorecovery-utilizes-consistent-hashing-high-availability/).
{: shortdesc}

Autorecovery requires at least one healthy node to function properly. Configure Autorecovery with active checks only in clusters with two or more worker nodes.
{: note}

Before you begin:
- Ensure that you have the following [{{site.data.keyword.cloud_notm}} IAM roles](/docs/containers?topic=containers-users#platform):
    - **Administrator** platform role for the cluster
    - **Writer** or **Manager** service role for the `kube-system` namespace
- [Log in to your account. If applicable, target the appropriate resource group. Set the context for your cluster.](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure)

To configure Autorecovery:

1.  [Follow the instructions](/docs/containers?topic=containers-helm#public_helm_install) to install the Helm client on your local machine, install the Helm server (tiller) with a service account, and add the {{site.data.keyword.cloud_notm}} Helm repository.

2.  Verify that tiller is installed with a service account.
    ```
    kubectl get serviceaccount -n kube-system | grep tiller
    ```
    {: pre}

    Example output:
    ```
    NAME                                 SECRETS   AGE
    tiller                               1         2m
    ```
    {: screen}

3. Create a configuration map file that defines your checks in JSON format. For example, the following YAML file defines three checks: an HTTP check and two Kubernetes API server checks. Refer to the tables following the example YAML file for information about the three kinds of checks and information about the individual components of the checks.<p class="tip">*Define each check as a unique key in the `data` section of the configuration map.</p>

   ```
   kind: ConfigMap
   apiVersion: v1
   metadata:
     name: ibm-worker-recovery-checks
     namespace: kube-system
   data:
     checknode.json: |
       {
         "Check":"KUBEAPI",
         "Resource":"NODE",
         "FailureThreshold":3,
         "CorrectiveAction":"RELOAD",
         "CooloffSeconds":1800,
         "IntervalSeconds":180,
         "TimeoutSeconds":10,
         "Enabled":true
       }
     checkpod.json: |
       {
         "Check":"KUBEAPI",
         "Resource":"POD",
         "PodFailureThresholdPercent":50,
         "FailureThreshold":3,
         "CorrectiveAction":"RELOAD",
         "CooloffSeconds":1800,
         "IntervalSeconds":180,
         "TimeoutSeconds":10,
         "Enabled":true
       }
     checkhttp.json: |
       {
         "Check":"HTTP",
         "FailureThreshold":3,
         "CorrectiveAction":"REBOOT",
         "CooloffSeconds":1800,
         "IntervalSeconds":180,
         "TimeoutSeconds":10,
         "Port":80,
         "ExpectedStatus":200,
         "Route":"/myhealth",
         "Enabled":false
       }
   ```
   {:codeblock}

   <table summary="Understanding the components of the configmap">
   <caption>Understanding the configmap components</caption>
   <thead>
   <th colspan=2><img src="images/idea.png" alt="Idea icon"/>Understanding the configmap components</th>
   </thead>
   <tbody>
   <tr>
   <td><code>name</code></td>
   <td>The configuration name <code>ibm-worker-recovery-checks</code> is a constant and cannot be changed.</td>
   </tr>
   <tr>
   <td><code>namespace</code></td>
   <td>The <code>kube-system</code> namespace is a constant and cannot be changed.</td>
   </tr>
   <tr>
   <td><code>checknode.json</code></td>
   <td>Defines a Kubernetes API node check that checks whether each worker node is in the <code>Ready</code> state. The check for a specific worker node counts as a failure if the worker node is not in the <code>Ready</code> state. The check in the example YAML runs every 3 minutes. If it fails three consecutive times, the worker node is reloaded. This action is equivalent to running <code>ibmcloud ks worker-reload</code>.<br></br>The node check is enabled until you set the <b>Enabled</b> field to <code>false</code> or remove the check.</td>
   </tr>
   <tr>
   <td><code>checkpod.json</code></td>
   <td>
   Defines a Kubernetes API pod check that checks the total percentage of <code>NotReady</code> pods on a worker node based on the total pods that are assigned to that worker node. The check for a specific worker node counts as a failure if the total percentage of <code>NotReady</code> pods is greater than the defined <code>PodFailureThresholdPercent</code>. The check in the example YAML runs every 3 minutes. If it fails three consecutive times, the worker node is reloaded. This action is equivalent to running <code>ibmcloud ks worker-reload</code>. For example, the default <code>PodFailureThresholdPercent</code> is 50%. If the percentage of <code>NotReady</code> pods is greater than 50% three consecutive times, the worker node is reloaded. <br></br>By default, pods in all namespaces are checked. To restrict the check to only pods in a specified namespace, add the <code>Namespace</code> field to the check. The pod check is enabled until you set the <b>Enabled</b> field to <code>false</code> or remove the check.
   </td>
   </tr>
   <tr>
   <td><code>checkhttp.json</code></td>
   <td>Defines an HTTP check that checks if an HTTP server that runs on your worker node is healthy. To use this check, you must deploy an HTTP server on every worker node in your cluster by using a [daemon set ![External link icon](../icons/launch-glyph.svg "External link icon")](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/). You must implement a health check that is available at the <code>/myhealth</code> path and that can verify whether your HTTP server is healthy. You can define other paths by changing the <code>Route</code> parameter. If the HTTP server is healthy, you must return the HTTP response code that is defined in <code>ExpectedStatus</code>. The HTTP server must be configured to listen on the private IP address of the worker node. You can find the private IP address by running <code>kubectl get nodes</code>.<br></br>
   For example, consider two nodes in a cluster that have the private IP addresses 10.10.10.1 and 10.10.10.2. In this example, two routes are checked for a 200 HTTP response: <code>http://10.10.10.1:80/myhealth</code> and <code>http://10.10.10.2:80/myhealth</code>.
   The check in the example YAML runs every 3 minutes. If it fails three consecutive times, the worker node is rebooted. This action is equivalent to running <code>ibmcloud ks worker-reboot</code>.<br></br>The HTTP check is disabled until you set the <b>Enabled</b> field to <code>true</code>.</td>
   </tr>
   </tbody>
   </table>

   <table summary="Understanding individual components of checks">
   <caption>Understanding the individual components of checks</caption>
   <thead>
   <th colspan=2><img src="images/idea.png" alt="Idea icon"/>Understanding the individual components of checks </th>
   </thead>
   <tbody>
   <tr>
   <td><code>Check</code></td>
   <td>Enter the type of check that you want Autorecovery to use. <ul><li><code>HTTP</code>: Autorecovery calls HTTP servers that run on each node to determine whether the nodes are running properly.</li><li><code>KUBEAPI</code>: Autorecovery calls the Kubernetes API server and reads the health status data reported by the worker nodes.</li></ul></td>
   </tr>
   <tr>
   <td><code>Resource</code></td>
   <td>When the check type is <code>KUBEAPI</code>, enter the type of resource that you want Autorecovery to check. Accepted values are <code>NODE</code> or <code>POD</code>.</td>
   </tr>
   <tr>
   <td><code>FailureThreshold</code></td>
   <td>Enter the threshold for the number of consecutive failed checks. When this threshold is met, Autorecovery triggers the specified corrective action. For example, if the value is 3 and Autorecovery fails a configured check three consecutive times, Autorecovery triggers the corrective action that is associated with the check.</td>
   </tr>
   <tr>
   <td><code>PodFailureThresholdPercent</code></td>
   <td>When the resource type is <code>POD</code>, enter the threshold for the percentage of pods on a worker node that can be in a [<strong><code>NotReady</code></strong> ![External link icon](../icons/launch-glyph.svg "External link icon")](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-probes/#define-readiness-probes) state. This percentage is based on the total number of pods that are scheduled to a worker node. When a check determines that the percentage of unhealthy pods is greater than the threshold, the check counts as one failure.</td>
   </tr>
   <tr>
   <td><code>CorrectiveAction</code></td>
   <td>Enter the action to run when the failure threshold is met. A corrective action runs only while no other workers are being repaired and when this worker node is not in a cool-off period from a previous action. <ul><li><code>REBOOT</code>: Reboots the worker node.</li><li><code>RELOAD</code>: Reloads all of the necessary configurations for the worker node from a clean OS.</li></ul></td>
   </tr>
   <tr>
   <td><code>CooloffSeconds</code></td>
   <td>Enter the number of seconds Autorecovery must wait to issue another corrective action for a node that was already issued a corrective action. The cool off period starts at the time a corrective action is issued.</td>
   </tr>
   <tr>
   <td><code>IntervalSeconds</code></td>
   <td>Enter the number of seconds in between consecutive checks. For example, if the value is 180, Autorecovery runs the check on each node every 3 minutes.</td>
   </tr>
   <tr>
   <td><code>TimeoutSeconds</code></td>
   <td>Enter the maximum number of seconds that a check call to the database takes before Autorecovery terminates the call operation. The value for <code>TimeoutSeconds</code> must be less than the value for <code>IntervalSeconds</code>.</td>
   </tr>
   <tr>
   <td><code>Port</code></td>
   <td>When the check type is <code>HTTP</code>, enter the port that the HTTP server must bind to on the worker nodes. This port must be exposed on the IP of every worker node in the cluster. Autorecovery requires a constant port number across all nodes for checking servers. Use [daemon sets ![External link icon](../icons/launch-glyph.svg "External link icon")](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/) when you deploy a custom server into a cluster.</td>
   </tr>
   <tr>
   <td><code>ExpectedStatus</code></td>
   <td>When the check type is <code>HTTP</code>, enter the HTTP server status that you expect to be returned from the check. For example, a value of 200 indicates that you expect an <code>OK</code> response from the server.</td>
   </tr>
   <tr>
   <td><code>Route</code></td>
   <td>When the check type is <code>HTTP</code>, enter the path that is requested from the HTTP server. This value is typically the metrics path for the server that is running on all of the worker nodes.</td>
   </tr>
   <tr>
   <td><code>Enabled</code></td>
   <td>Enter <code>true</code> to enable the check or <code>false</code> to disable the check.</td>
   </tr>
   <tr>
   <td><code>Namespace</code></td>
   <td> Optional: To restrict <code>checkpod.json</code> to checking only pods in one namespace, add the <code>Namespace</code> field and enter the namespace.</td>
   </tr>
   </tbody>
   </table>

4. Create the configuration map in your cluster.
    ```
    kubectl apply -f ibm-worker-recovery-checks.yaml
    ```
    {: pre}

5. Verify that you created the configuration map with the name `ibm-worker-recovery-checks` in the `kube-system` namespace with the proper checks.
    ```
    kubectl -n kube-system get cm ibm-worker-recovery-checks -o yaml
    ```
    {: pre}

6. Deploy Autorecovery into your cluster by installing the `ibm-worker-recovery` Helm chart.
    ```
    helm install --name ibm-worker-recovery iks-charts/ibm-worker-recovery  --namespace kube-system
    ```
    {: pre}

7. After a few minutes, you can check the `Events` section in the output of the following command to see activity on the Autorecovery deployment.
    ```
    kubectl -n kube-system describe deployment ibm-worker-recovery
    ```
    {: pre}

8. If you do not see activity on the Autorecovery deployment, you can check the Helm deployment by running the tests that are included in the Autorecovery chart definition.
    ```
    helm test ibm-worker-recovery
    ```
    {: pre}
