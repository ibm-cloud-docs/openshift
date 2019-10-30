---

copyright:
  years: 2014, 2019
lastupdated: "2019-10-30"

keywords: openshift, roks, rhos, rhoks, lb2.0, nlb

subcollection: openshift

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

# Registering a DNS subdomain for an NLB
{: #loadbalancer_hostname}



After you set up network load balancers (NLBs), you can create DNS entries for the NLB IPs by creating subdomains. You can also set up TCP/HTTP(S) monitors to health check the NLB IP addresses behind each subdomain.
{: shortdesc}

<dl>
<dt>Subdomain</dt>
<dd>When you create a public NLB in a single-zone or multizone cluster, you can expose your app to the internet by creating a subdomain for the NLB IP address. Additionally, {{site.data.keyword.cloud_notm}} takes care of generating and maintaining the wildcard SSL certificate for the subdomain for you.
<p>In multizone clusters, you can create a subdomain and add the NLB IP address in each zone to that subdomain DNS entry. For example, if you deployed NLBs for your app in three zones in US-South, you can create the subdomain `mycluster-a1b2cdef345678g9hi012j3kl4567890-0001.us-south.containers.appdomain.cloud` for the three NLB IP addresses. When a user accesses your app subdomain, the client accesses one of these IPs at random, and the request is sent to that NLB.</p>
<p class="note">You currently cannot create subdomains for private NLBs.</p></dd>
<dt>Health check monitor</dt>
<dd>Enable health checks on the NLB IP addresses behind a single subdomain to determine whether they are available or not. When you enable a monitor for your subdomain, the monitor health checks each NLB IP and keeps the DNS lookup results updated based on these health checks. For example, if your NLBs have IP addresses `1.1.1.1`, `2.2.2.2`, and `3.3.3.3`, a normal operation DNS lookup of your subdomain returns all 3 IPs, 1 of which the client accesses at random. If the NLB with IP address `3.3.3.3` becomes unavailable for any reason, such as due to zone failure, then the health check for that IP fails, the monitor removes the failed IP from the subdomain, and the DNS lookup returns only the healthy `1.1.1.1` and `2.2.2.2` IPs.</dd>
</dl>

You can see all subdomains that are registered for NLB IPs in your cluster by running the following command.
```
ibmcloud oc nlb-dns ls --cluster <cluster_name_or_id>
```
{: pre}

</br>

## Registering NLB IPs with a DNS subdomain
{: #loadbalancer_hostname_dns}

Expose your app to the public internet by creating a subdomain for the network load balancer (NLB) IP address.
{: shortdesc}

Before you begin:
* Review the following considerations and limitations.
  * You currently cannot create subdomains for private NLBs.
  * You can register up to 128 subdomains. This limit can be lifted on request by opening a [support case](/docs/get-support?topic=get-support-getting-customer-support).
* [Create an NLB for your app in a single-zone cluster](/docs/openshift?topic=openshift-loadbalancer#lb_config) or [create NLBs in each zone of a multizone cluster](/docs/openshift?topic=openshift-loadbalancer#multi_zone_config).

To create a subdomain for one or more NLB IP addresses:

1. Get the **EXTERNAL-IP** address for your NLB. If you have NLBs in each zone of a multizone cluster that expose one app, get the IPs for each NLB.
  ```
  oc get svc
  ```
  {: pre}

  In the following example output, the NLB **EXTERNAL-IP**s are `168.2.4.5` and `88.2.4.5`.
  ```
  NAME             TYPE           CLUSTER-IP       EXTERNAL-IP       PORT(S)                AGE
  lb-myapp-dal10   LoadBalancer   172.21.xxx.xxx   168.2.4.5         1883:30303/TCP         6d
  lb-myapp-dal12   LoadBalancer   172.21.xxx.xxx   88.2.4.5          1883:31303/TCP         6d
  ```
  {: screen}

2. Register the IP by creating a DNS subdomain. To specify multiple IP addresses, use multiple `--ip` flags.
  ```
  ibmcloud oc nlb-dns create classic --cluster <cluster_name_or_id> --ip <NLB_IP> --ip <NLB2_IP> ...
  ```
  {: pre}

3. Verify that the subdomain is created.
  ```
  ibmcloud oc nlb-dns ls --cluster <cluster_name_or_id>
  ```
  {: pre}

  Example output:
  ```
  Hostname                                                                                IP(s)              Health Monitor   SSL Cert Status           SSL Cert Secret Name
  mycluster-a1b2cdef345678g9hi012j3kl4567890-0001.us-south.containers.appdomain.cloud     ["168.2.4.5"]      None             created                   <certificate>
  ```
  {: screen}

4. Optional: Verify that the IPs are registered with your subdomain by running a `host` or `ns lookup`.
  Example command:
  ```
  host mycluster-a1b2cdef345678g9hi012j3kl4567890-0001.us-south.containers.appdomain.cloud
  ```
  {: pre}

  Example output:
  ```
  mycluster-a1b2cdef345678g9hi012j3kl4567890-0001.us-south.containers.appdomain.cloud has address 88.2.4.5
  mycluster-a1b2cdef345678g9hi012j3kl4567890-0001.us-south.containers.appdomain.cloud has address 168.2.4.5
  ```
  {: screen}

5. In a web browser, enter the URL to access your app through the subdomain that you created.

Next, you can [enable health checks on the subdomain by creating a health monitor](#loadbalancer_hostname_monitor).

</br>

## Understanding the subdomain format
{: #loadbalancer_hostname_format}

Subdomains for NLBs follow the format `<cluster_name>-<globally_unique_account_HASH>-0001.<region>.containers.appdomain.cloud`.
{: shortdesc}

For example, a subdomain that you create for an NLB might look like `mycluster-a1b2cdef345678g9hi012j3kl4567890-0001.us-south.containers.appdomain.cloud`. The following table describes each component of the subdomain.

<table>
<thead>
<th colspan=2><img src="images/idea.png" alt="Idea icon"/> Understanding the NLB subdomain format</th>
</thead>
<tbody>
<tr>
<td><code>&lt;cluster_name&gt;</code></td>
<td>The name of your cluster.
<ul><li>If the cluster name is 26 characters or fewer, the entire cluster name is included and is not modified: <code>myclustername</code>.</li>
<li>If the cluster name is 26 characters or greater and the cluster name is unique in this region, only the first 24 characters of the cluster name are used: <code>myveryverylongclusternam</code>.</li>
<li>If the cluster name is 26 characters or greater and there is an existing cluster of the same name in this region, only the first 17 characters of the cluster name are used and a dash with six random characters is added: <code>myveryverylongclu-ABC123</code>.</li></ul>
</td>
</tr>
<tr>
<td><code>&lt;globally_unique_account_HASH&gt;</code></td>
<td>A globally unique HASH is created for your {{site.data.keyword.cloud_notm}} account. All subdomains that you create for NLBs in clusters in your account use this globally unique HASH.</td>
</tr>
<tr>
<td><code>0001</code></td>
<td>
The first and second characters, <code>00</code>, indicate a public subdomain. The third and fourth characters, such as <code>01</code> or another number, act as a counter for each subdomain that you create.</td>
</tr>
<tr>
<td><code>&lt;region&gt;</code></td>
<td>The region that the cluster is created in.</td>
</tr>
<tr>
<td><code>containers.appdomain.cloud</code></td>
<td>The subdomain for Red Hat OpenShift on IBM Cloud subdomains.</td>
</tr>
</tbody>
</table>

</br>

## Enable health checks on a subdomain by creating a health monitor
{: #loadbalancer_hostname_monitor}

Enable health checks on the NLB IP addresses behind a single subdomain to determine whether they are available or not.
{: shortdesc}

Before you begin, [register NLB IPs with a DNS subdomain](#loadbalancer_hostname_dns).

1. Get the name of your subdomain. In the output, note that the host has a monitor **Status** of `Unconfigured`.
  ```
  ibmcloud oc nlb-dns monitor ls --cluster <cluster_name_or_id>
  ```
  {: pre}

  Example output:
  ```
  Hostname                                                                                   Status         Type    Port   Path
  mycluster-a1b2cdef345678g9hi012j3kl4567890-0001.us-south.containers.appdomain.cloud        Unconfigured   N/A     0      N/A
  ```
  {: screen}

2. Create a health check monitor for the subdomain. If you do not include a configuration parameter, the default value is used.
  ```
  ibmcloud oc nlb-dns monitor configure --cluster <cluster_name_or_id> --nlb-host <host_name> --enable --desc <description> --type <type> --method <method> --path <path> --timeout <timeout> --retries <retries> --interval <interval> --port <port> --expected-body <expected-body> --expected-codes <expected-codes> --follows-redirects <true> --allows-insecure <true>
  ```
  {: pre}

  <table>
  <caption>Understanding this command's components</caption>
  <thead>
  <th colspan=2><img src="images/idea.png" alt="Idea icon"/> Understanding this command's components</th>
  </thead>
  <tbody>
  <tr>
  <td><code>-c, --cluster &lt;cluster_name_or_ID&gt;</code></td>
  <td>Required: The name or ID of the cluster where the subdomain is registered.</td>
  </tr>
  <tr>
  <td><code>--nlb-host &lt;host_name&gt;</code></td>
  <td>Required: The subdomain to enable a health check monitor for.</td>
  </tr>
  <tr>
  <td><code>--enable</code></td>
  <td>Required: Enable the health check monitor for the subdomain.</td>
  </tr>
  <tr>
  <td><code>--description &lt;description&gt;</code></td>
  <td>A description of the health monitor.</td>
  </tr>
  <tr>
  <td><code>--type &lt;type&gt;</code></td>
  <td>The protocol to use for the health check: <code>HTTP</code>, <code>HTTPS</code>, or <code>TCP</code>. Default: <code>HTTP</code></td>
  </tr>
  <tr>
  <td><code>--method &lt;method&gt;</code></td>
  <td>The method to use for the health check. Default for <code>type</code> <code>HTTP</code> and <code>HTTPS</code>: <code>GET</code>. Default for <code>type</code> <code>TCP</code>: <code>connection_established</code></td>
  </tr>
  <tr>
  <td><code>--path &lt;path&gt;</code></td>
  <td>When <code>type</code> is <code>HTTPS</code>: The endpoint path to health check against. Default: <code>/</code></td>
  </tr>
  <tr>
  <td><code>--timeout &lt;timeout&gt;</code></td>
  <td>The timeout, in seconds, before the IP is considered unhealthy. Default: <code>5</code></td>
  </tr>
  <tr>
  <td><code>--retries &lt;retries&gt;</code></td>
  <td>When a timeout occurs, the number of retries to attempt before the IP is considered unhealthy. Retries are attempted immediately. Default: <code>2</code></td>
  </tr>
  <tr>
  <td><code>--interval &lt;interval&gt;</code></td>
  <td>The interval, in seconds, between each health check. Short intervals might improve failover time, but increase load on the IPs. Default: <code>60</code></td>
  </tr>
  <tr>
  <td><code>--port &lt;port&gt;</code></td>
  <td>The port number to connect to for the health check. When <code>type</code> is <code>TCP</code>, this parameter is required. When <code>type</code> is <code>HTTP</code> or <code>HTTPS</code>, define the port only if you use a port other than 80 for HTTP or 443 for HTTPS. Default for TCP: <code>0</code>. Default for HTTP: <code>80</code>. Default for HTTPS: <code>443</code>.</td>
  </tr>
  <tr>
  <td><code>--expected-body &lt;expected-body&gt;</code></td>
  <td>When <code>type</code> is <code>HTTP</code> or <code>HTTPS</code>: A case-insensitive substring that the health check looks for in the response body. If this string is not found, the IP is considered unhealthy.</td>
  </tr>
  <tr>
  <td><code>--expected-codes &lt;expected-codes&gt;</code></td>
  <td>When <code>type</code> is <code>HTTP</code> or <code>HTTPS</code>: HTTP codes that the health check looks for in the response. If the HTTP code is not found, the IP is considered unhealthy. Default: <code>2xx</code></td>
  </tr>
  <tr>
  <td><code>--allows-insecure &lt;true&gt;</code></td>
  <td>When <code>type</code> is <code>HTTP</code> or <code>HTTPS</code>: Set to <code>true</code> to not validate the certificate.</td>
  </tr>
  <tr>
  <td><code>--follows-redirects &lt;true&gt;</code></td>
  <td>When <code>type</code> is <code>HTTP</code> or <code>HTTPS</code>: Set to <code>true</code> to follow any redirects that are returned by the IP.</td>
  </tr>
  </tbody>
  </table>

  Example command:
  ```
  ibmcloud oc nlb-dns monitor configure --cluster mycluster --nlb-host mycluster-a1b2cdef345678g9hi012j3kl4567890-0001.us-south.containers.appdomain.cloud --enable --desc "Login page monitor" --type HTTPS --method GET --path / --timeout 5 --retries 2 --interval 60 --expected-body "healthy" --expected-codes 2xx --follows-redirects true
  ```
  {: pre}

3. Verify that the health check monitor is configured with the correct settings.
  ```
  ibmcloud oc nlb-dns monitor get --cluster <cluster_name_or_id> --nlb-host <host_name>
  ```
  {: pre}

  Example output:
  ```
  <placeholder - still want to test this one>
  ```
  {: screen}

4. View the health check status of the NLB IPs that are behind your subdomain.
  ```
  ibmcloud oc nlb-dns monitor status --cluster <cluster_name_or_id> --nlb-host <host_name>
  ```
  {: pre}

  Example output:
  ```
  Hostname                                                                                IP          Health Monitor   H.Monitor Status
  mycluster-a1b2cdef345678g9hi012j3kl4567890-0001.us-south.containers.appdomain.cloud     168.2.4.5   Enabled          Healthy
  mycluster-a1b2cdef345678g9hi012j3kl4567890-0001.us-south.containers.appdomain.cloud     88.2.4.5    Enabled          Healthy
  ```
  {: screen}

</br>

### Updating and removing IPs and monitors from subdomains
{: #loadbalancer_hostname_delete}

You can add and remove NLB IP addresses from subdomains that you have generated. You can also disable and enable health check monitors for subdomains as needed.
{: shortdesc}

**NLB IPs**

If you later add more NLBs in other zones of your cluster to expose the same app, you can add the NLB IPs to the existing subdomain.
```
ibmcloud oc nlb-dns add --cluster <cluster_name_or_id> --ip <NLB_IP> --ip <NLB2_IP> ... --nlb-host <host_name>
```
{: pre}

You can also remove IP addresses of NLBs that you no longer want to be registered with a subdomain. Note that you must run the following command for each IP address that you want to remove. If you remove all IPs from a subdomain, the subdomain still exists but no IPs are associated with it.
```
ibmcloud oc nlb-dns rm classic --cluster <cluster_name_or_id> --ip <ip> --nlb-host <host_name>
```
{: pre}

</br>

**Health check monitors**

If you need to change your health monitor configuration, you can change specific settings. Include only the flags for the settings that you want to change.
```
ibmcloud oc nlb-dns monitor configure --cluster <cluster_name_or_id> --nlb-host <host_name> --desc <description> --type <type> --method <method> --path <path> --timeout <timeout> --retries <retries> --interval <interval> --port <port> --expected-body <expected-body> --expected-codes <expected-codes> --follows-redirects <true> --allows-insecure <true>
```
{: pre}

You can disable the health check monitor for a subdomain at any time by running the following command:
```
ibmcloud oc nlb-dns monitor disable --cluster <cluster_name_or_id> --nlb-host <host_name>
```
{: pre}

To re-enable a monitor for a subdomain, run the following command:
```
ibmcloud oc nlb-dns monitor enable --cluster <cluster_name_or_id> --nlb-host <host_name>
```
{: pre}



</staging components>
