---

copyright:
  years: 2014, 2019
lastupdated: "2019-09-10"

keywords: openshift, roks, rhoks, rhos

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


# Opening required ports and IP addresses in your firewall
{: #firewall}

Review these situations in which you might need to open specific ports and IP addresses in your firewalls for your {{site.data.keyword.openshiftlong}} clusters.
{:shortdesc}



* [Corporate firewalls](#corporate): If corporate network policies prevent access from your local system to public endpoints via proxies or firewalls, you must allow access to run `ibmcloud`, `ibmcloud oc`, `ibmcloud cr`, `oc`, and `calicoctl` commands from your local system.
* [Gateway device firewalls](#vyatta_firewall): If you have firewalls set up on the public or private network in your IBM Cloud infrastructure account, you must open IP ranges, ports, and protocols to allow worker nodes to communicate with the master, with infrastructure resources, and with other {{site.data.keyword.cloud_notm}} services. You can also open ports to allow incoming traffic to services exposing apps in your cluster.
* [Calico network policies](#firewall_calico_egress): If you use Calico network policies to act as a firewall to restrict all worker node egress, you must allow your worker nodes to access the resources that are required for the cluster to function.
* [Other services or network firewalls](#whitelist_workers): To allow your cluster to access services that run inside or outside {{site.data.keyword.cloud_notm}} or in on-premises networks and that are protected by a firewall, you must add the IP addresses of your worker nodes in that firewall.

<br />


## Opening ports in a corporate firewall
{: #corporate}

If corporate network policies prevent access from your local system to public endpoints via proxies or firewalls, you must allow access to run [`ibmcloud`, `ibmcloud oc`, and `ibmcloud cr` commands](#firewall_bx), [`oc` commands](#firewall_kubectl), and [`calicoctl` commands](#firewall_calicoctl) from your local system.
{: shortdesc}

### Running `ibmcloud`, `ibmcloud oc`, and `ibmcloud cr` commands from behind a firewall
{: #firewall_bx}

If corporate network policies prevent access from your local system to public endpoints via proxies or firewalls, to run `ibmcloud`, `ibmcloud oc` and `ibmcloud cr` commands, you must allow TCP access for {{site.data.keyword.cloud_notm}}, Red Hat OpenShift on IBM Cloud, and {{site.data.keyword.registrylong_notm}}.
{:shortdesc}

1. Allow access to `cloud.ibm.com` on port 443 in your firewall.
2. Verify your connection by logging in to {{site.data.keyword.cloud_notm}} through this API endpoint.
  ```
  ibmcloud login -a https://cloud.ibm.com/
  ```
  {: pre}
3. Allow access to `containers.cloud.ibm.com` on port 443 in your firewall.
4. Verify your connection. If access is configured correctly, ships are displayed in the output.
   ```
   curl https://containers.cloud.ibm.com/v1/
   ```
   {: pre}

   Example output:
   ```
                                     )___(
                              _______/__/_
                     ___     /===========|   ___
    ____       __   [\\\]___/____________|__[///]   __
    \   \_____[\\]__/___________________________\__[//]___
     \                                                    |
      \                                                  /
   ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

   ```
   {: screen}
5. Allow access to the [{{site.data.keyword.registrylong_notm}} regions](/docs/services/Registry?topic=registry-registry_overview#registry_regions) that you plan to use on port 443 and 4443 in your firewall. The global registry stores IBM-provided public images, and regional registries store your own private or public images. If your firewall is IP-based, you can see which IP addresses are opened when you allow access to the {{site.data.keyword.registryshort_notm}} regional service endpoints by reviewing [this table](#firewall_registry).
  * Global registry: `icr.io`
  * AP North: `jp.icr.io`
  * AP South: `au.icr.io`
  * EU Central: `de.icr.io`
  * UK South: `uk.icr.io`
  * US East, US South: `us.icr.io`

6. Verify your connection. The following is an example for the US East and US South regional registry. If access is configured correctly, a message of the day is returned in the output.
   ```
   curl https://us.icr.io/api/v1/messages
   ```
   {: pre}

</br>

### Running `oc` commands from behind a firewall
{: #firewall_kubectl}

If corporate network policies prevent access from your local system to public endpoints via proxies or firewalls, to run `oc` commands, you must allow TCP access for the cluster.
{:shortdesc}

When a cluster is created, the port in the service endpoint URLs is randomly assigned from within 20000-32767. You can either choose to open port range 20000-32767 for any cluster that might get created or you can choose to allow access for a specific existing cluster.

Before you begin, allow access to [run `ibmcloud oc` commands](#firewall_bx).

To allow access for a specific cluster:

1. Log in to the {{site.data.keyword.cloud_notm}} CLI. Enter your {{site.data.keyword.cloud_notm}} credentials when prompted. If you have a federated account, include the `--sso` option.

   ```
   ibmcloud login [--sso]
   ```
   {: pre}

2. If the cluster is in a resource group other than `default`, target that resource group. To see the resource group that each cluster belongs to, run `ibmcloud oc cluster ls`. **Note**: You must have at least the [**Viewer** role](/docs/containers?topic=containers-users#platform) for the resource group.
   ```
   ibmcloud target -g <resource_group_name>
   ```
   {: pre}

4. Get the name of your cluster.

   ```
   ibmcloud oc cluster ls
   ```
   {: pre}

5. Retrieve the service endpoint URLs for your cluster.
 * If only the **Public Service Endpoint URL** is populated, get this URL. Your authorized cluster users can access the master through this endpoint on the public network.
 * If only the **Private Service Endpoint URL** is populated, get this URL. Your authorized cluster users can access the master through this endpoint on the private network.
 * If both the **Public Service Endpoint URL** and **Private Service Endpoint URL** are populated, get both URLs. Your authorized cluster users can access the master through the public endpoint on the public network or the private endpoint on the private network.

  ```
  ibmcloud oc cluster get --cluster <cluster_name_or_ID>
  ```
  {: pre}

  Example output:
  ```
  ...
  Public Service Endpoint URL:    https://c3.<region>.containers.cloud.ibm.com:30426
  Private Service Endpoint URL:   https://c3-private.<region>.containers.cloud.ibm.com:31140
  ...
  ```
  {: screen}

6. Allow access to the service endpoint URLs and ports that you got in the previous step. If your firewall is IP-based, you can see which IP addresses are opened when you allow access to the service endpoint URLs by reviewing [this table](#master_ips).

7. Verify your connection.
  * If the public service endpoint is enabled:
    ```
    curl --insecure <public_service_endpoint_URL>/version
    ```
    {: pre}

    Example command:
    ```
    curl --insecure https://c3.<region>.containers.cloud.ibm.com:31142/version
    ```
    {: pre}

    Example output:
    ```
    {
     "major": "1",
     "minor": "7+",
     "gitVersion": "v1.7.4-2+eb9172c211dc41",
     "gitCommit": "eb9172c211dc4108341c0fd5340ee5200f0ec534",
     "gitTreeState": "clean",
     "buildDate": "2017-11-16T08:13:08Z",
     "goVersion": "go1.8.3",
     "compiler": "gc",
     "platform": "linux/amd64"
    }
    ```
    {: screen}
  * If the private service endpoint is enabled, you must be in your {{site.data.keyword.cloud_notm}} private network or connect to the private network through a VPN connection to verify your connection to the master. **Note**: You must [expose the master endpoint through a private load balancer](/docs/containers?topic=containers-clusters#access_on_prem) so that users can access the master through a VPN or {{site.data.keyword.BluDirectLink}} connection.
    ```
    curl --insecure <private_service_endpoint_URL>/version
    ```
    {: pre}

    Example command:
    ```
    curl --insecure https://c3-private.<region>.containers.cloud.ibm.com:31142/version
    ```
    {: pre}

    Example output:
    ```
    {
     "major": "1",
     "minor": "7+",
     "gitVersion": "v1.7.4-2+eb9172c211dc41",
     "gitCommit": "eb9172c211dc4108341c0fd5340ee5200f0ec534",
     "gitTreeState": "clean",
     "buildDate": "2017-11-16T08:13:08Z",
     "goVersion": "go1.8.3",
     "compiler": "gc",
     "platform": "linux/amd64"
    }
    ```
    {: screen}

8. Optional: Repeat these steps for each cluster that you need to expose.

</br>

### Running `calicoctl` commands from behind a firewall
{: #firewall_calicoctl}

If corporate network policies prevent access from your local system to public endpoints via proxies or firewalls, to run `calicoctl` commands, you must allow TCP access for the Calico commands.
{:shortdesc}

Before you begin, allow access to run [`ibmcloud` commands](#firewall_bx) and [`oc` commands](#firewall_kubectl).

1. Retrieve the IP address from the master URL that you used to allow the [`oc` commands](#firewall_kubectl).

2. Get the port for etcd.

  ```
  oc get cm -n kube-system cluster-info -o yaml | grep etcd_host
  ```
  {: pre}

3. Allow access for the Calico policies via the master URL IP address and the etcd port.

<br />


## Opening ports in gateway device firewalls
{: #vyatta_firewall}

If you have firewalls set up on the [public network](#firewall_outbound) or [private network](#firewall_private) in your IBM Cloud infrastructure account, you must open IP ranges, ports, and protocols to allow worker nodes to communicate with the master, with infrastructure resources, and with other {{site.data.keyword.cloud_notm}} services.
{: shortdesc}

### Opening required ports in a public firewall
{: #firewall_outbound}

If you have a firewall on the public network in your IBM Cloud infrastructure account, you must open IP ranges, ports, and protocols in your firewall to allow worker nodes to communicate with the master, with infrastructure resources, and with other {{site.data.keyword.cloud_notm}} services.
{:shortdesc}

1.  Note the public IP address for each worker node in the cluster.
    ```
    ibmcloud oc worker ls --cluster <cluster_name_or_ID>
    ```
    {: pre}

2. To allow worker nodes to communicate with the cluster master over the public service endpoint, allow outgoing network traffic from the source <em>&lt;each_worker_node_publicIP&gt;</em> to the destination TCP/UDP port range 20000-32767 and port 443, and the following IP addresses and network groups.
   - `TCP/UDP port range 20000-32767, port 443 FROM <each_worker_node_publicIP> TO <public_IPs>`
   -  Replace <em>&lt;public_IPs&gt;</em> with the public IP addresses of the zones in the region that your cluster is located.<p class="important">You must allow outgoing traffic to port 443 for **all of the zones within the region** to balance the load during the bootstrapping process.</p>
    {: #master_ips}
    <table summary="The first row in the table spans both columns. The rest of the rows should be read left to right, with the server zone in column one and IP addresses to match in column two.">
      <caption>IP addresses to open for outgoing traffic</caption>
          <thead>
          <th>Region</th>
          <th>Zone</th>
          <th>Public IP address</th>
          </thead>
        <tbody>
          <tr>
            <td>AP North</td>
            <td>che01<br>hkg02<br>seo01<br>sng01<br><br>tok02, tok04, tok05</td>
            <td><code>169.38.70.10</code><br><code>169.56.132.234</code><br><code>169.56.69.242</code><br><code>161.202.186.226</code><br><br><code>161.202.126.210, 128.168.71.117, 165.192.69.69, 165.192.80.146, 169.56.48.114, 128.168.75.194</code></td>
           </tr>
          <tr>
             <td>AP South</td>
             <td>mel01<br><br>syd01, syd04, syd05</td>
             <td><code>168.1.97.67</code><br><br><code>168.1.8.195, 130.198.66.26, 168.1.12.98, 130.198.64.19, 135.90.66.2, 130.198.102.82, 168.1.58.66</code></td>
          </tr>
          <tr>
             <td>EU Central</td>
             <td>ams03<br>mil01<br>osl01<br>par01<br><br>fra02, fra04, fra05</td>
             <td><code>169.50.169.110, 169.50.154.194</code><br><code>159.122.190.98, 159.122.141.69</code><br><code>169.51.73.50</code><br><code>159.8.86.149, 159.8.98.170</code><br><br><code>169.50.56.174, 161.156.65.42, 149.81.78.114, 158.177.198.138, 149.81.104.122, 161.156.65.82</code></td>
            </tr>
          <tr>
            <td>UK South</td>
            <td>lon02, lon04, lon05, lon06</td>
            <td><code>159.122.242.78, 158.175.111.42, 158.176.94.26, 159.122.224.242, 158.175.65.170, 158.176.95.146, 158.176.71.242, 141.125.77.58, 158.175.125.194</code></td>
          </tr>
          <tr>
            <td>US East</td>
             <td>mon01<br>tor01<br><br>wdc04, wdc06, wdc07</td>
             <td><code>169.54.126.219</code><br><code>169.53.167.50</code><br><br><code>169.63.88.186, 169.60.73.142, 169.61.109.34, 169.63.88.178, 169.60.101.42, 169.61.83.62, 169.47.174.106, 169.61.74.210, 169.63.149.122</code></td>
          </tr>
          <tr>
            <td>US South</td>
            <td>hou02<br>mex01<br>sao01<br>sjc03<br>sjc04<br><br>dal10,dal12,dal13</td>
            <td><code>184.173.44.62</code><br><code>169.57.100.18</code><br><code>169.57.151.10</code><br><code>169.45.67.210</code><br><code>169.62.82.197</code><br><br><code>169.46.7.238, 169.48.230.146, 169.61.29.194, 169.46.110.218, 169.47.70.10, 169.62.166.98, 169.48.143.218, 169.61.177.2, 169.60.128.2, 169.62.206.234, 169.61.175.106, 169.48.161.242</code></td>
          </tr>
          </tbody>
        </table>

3.  {: #firewall_registry}To permit worker nodes to communicate with {{site.data.keyword.registrylong_notm}}, allow outgoing network traffic from the worker nodes to [{{site.data.keyword.registrylong_notm}} regions](/docs/services/Registry?topic=registry-registry_overview#registry_regions):
  - `TCP port 443, port 4443 FROM <each_worker_node_publicIP> TO <registry_subnet>`
  -  Replace <em>&lt;registry_subnet&gt;</em> with the registry subnet to which you want to allow traffic. The global registry stores IBM-provided public images, and regional registries store your own private or public images. Port 4443 is required for notary functions, such as [Verifying image signatures](/docs/services/Registry?topic=registry-registry_trustedcontent#registry_trustedcontent). <table summary="The first row in the table spans both columns. The rest of the rows should be read left to right, with the server zone in column one and IP addresses to match in column two.">
  <caption>IP addresses to open for Registry traffic</caption>
    <thead>
      <th>Red Hat OpenShift on IBM Cloud region</th>
      <th>Registry address</th>
      <th>Registry public subnets</th>
    </thead>
    <tbody>
      <tr>
        <td>Global registry across <br>Red Hat OpenShift on IBM Cloud regions</td>
        <td><code>icr.io</code><br><br>
        Deprecated: <code>registry.bluemix.net</code></td>
        <td><code>169.60.72.144/28</code></br><code>169.61.76.176/28</code></br><code>169.62.37.240/29</code></br><code>169.60.98.80/29</code></br><code>169.63.104.232/29</code></td>
      </tr>
      <tr>
        <td>AP North</td>
        <td><code>jp.icr.io</code><br><br>
        Deprecated: <code>registry.au-syd.bluemix.net</code></td>
        <td><code>161.202.146.86/29</code></br><code>128.168.71.70/29</code></br><code>165.192.71.222/29</code></td>
      </tr>
      <tr>
        <td>AP South</td>
        <td><code>au.icr.io</code><br><br>
        Deprecated: <code>registry.au-syd.bluemix.net</code></td>
        <td><code>168.1.45.160/27</code></br><code>168.1.139.32/27</code></br><code>168.1.1.240/29</code></br><code>130.198.88.128/29</code></br><code>135.90.66.48/29</code></td>
      </tr>
      <tr>
        <td>EU Central</td>
        <td><code>de.icr.io</code><br><br>
        Deprecated: <code>registry.eu-de.bluemix.net</code></td>
        <td><code>169.50.56.144/28</code></br><code>159.8.73.80/28</code></br><code>169.50.58.104/29</code></br><code>161.156.93.16/29</code></br><code>149.81.79.152/29</code></td>
       </tr>
       <tr>
        <td>UK South</td>
        <td><code>uk.icr.io</code><br><br>
        Deprecated: <code>registry.eu-gb.bluemix.net</code></td>
        <td><code>159.8.188.160/27</code></br><code>169.50.153.64/27</code></br><code>158.175.97.184/29</code></br><code>158.176.105.64/29</code></br><code>141.125.71.136/29</code></td>
       </tr>
       <tr>
        <td>US East, US South</td>
        <td><code>us.icr.io</code><br><br>
        Deprecated: <code>registry.ng.bluemix.net</code></td>
        <td><code>169.55.39.112/28</code></br><code>169.46.9.0/27</code></br><code>169.55.211.0/27</code></br><code>169.61.234.224/29</code></br><code>169.61.135.160/29</code></br><code>169.61.46.80/29</code></td>
       </tr>
      </tbody>
    </table>

4. Allow outgoing network traffic from your worker node to {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM). Your firewall must be Layer 7 to whitelist the IAM domain name. IAM does not have specific IP addresses that you can whitelist. If your firewall does not support Layer 7, you can allow all HTTPS network traffic on port 443.
    - `TCP port 443 FROM <each_worker_node_publicIP> TO https://iam.bluemix.net`
    - `TCP port 443 FROM <each_worker_node_publicIP> TO https://iam.cloud.ibm.com`

5. Optional: Allow outgoing network traffic from the worker nodes to {{site.data.keyword.monitoringlong_notm}}, {{site.data.keyword.loganalysislong_notm}}, Sysdig, and LogDNA services:
    *   **{{site.data.keyword.monitoringlong_notm}}**:
        <pre class="screen">TCP port 443, port 9095 FROM &lt;each_worker_node_public_IP&gt; TO &lt;monitoring_subnet&gt;</pre>
        Replace <em>&lt;monitoring_subnet&gt;</em> with the subnets for the monitoring regions to which you want to allow traffic:
        <p><table summary="The first row in the table spans both columns. The rest of the rows should be read left to right, with the server zone in column one and IP addresses to match in column two.">
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
              </table></p>
    *   **{{site.data.keyword.mon_full_notm}}**:
        <pre class="screen">TCP port 443, port 6443 FROM &lt;each_worker_node_public_IP&gt; TO &lt;sysdig_public_IP&gt;</pre>
        Replace <em>&lt;sysdig_public_IP&gt;</em> with the [Sysdig IP addresses](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-network#network).
    *   **{{site.data.keyword.loganalysislong_notm}}**:
        <pre class="screen">TCP port 443, port 9091 FROM &lt;each_worker_node_public_IP&gt; TO &lt;logging_public_IP&gt;</pre>
        Replace <em>&lt;logging_public_IP&gt;</em> with all of the addresses for the logging regions to which you want to allow traffic:
        <p><table summary="The first row in the table spans both columns. The rest of the rows should be read left to right, with the server zone in column one and IP addresses to match in column two.">
        <caption>IP addresses to open for logging traffic</caption>
                <thead>
                <th>{{site.data.keyword.containerlong_notm}} region</th>
                <th>Logging address</th>
                <th>Logging IP addresses</th>
                </thead>
                <tbody>
                  <tr>
                    <td>US East, US South</td>
                    <td><code>ingest.logging.ng.bluemix.net</code></td>
                    <td><code>169.48.79.236</code><br><code>169.46.186.113</code></td>
                  </tr>
                  <tr>
                   <td>UK South</td>
                   <td><code>ingest.logging.eu-gb.bluemix.net</code></td>
                   <td><code>169.50.115.113</code></td>
                  </tr>
                  <tr>
                   <td>EU Central</td>
                   <td><code>ingest-eu-fra.logging.bluemix.net</code></td>
                   <td><code>158.177.88.43</code><br><code>159.122.87.107</code></td>
                  </tr>
                  <tr>
                   <td>AP South, AP North</td>
                   <td><code>ingest-au-syd.logging.bluemix.net</code></td>
                   <td><code>130.198.76.125</code><br><code>168.1.209.20</code></td>
                  </tr>
                 </tbody>
               </table></p>
    *   **{{site.data.keyword.la_full_notm}}**:
        <pre class="screen">TCP port 443, port 80 FROM &lt;each_worker_node_public_IP&gt; TO &lt;logDNA_public_IP&gt;</pre>
        Replace &gt;<em>logDNA_public_IP&gt;</em> with the [LogDNA IP addresses](/docs/services/Log-Analysis-with-LogDNA?topic=LogDNA-network#network).

6. If you use load balancer services, ensure that all traffic that uses the VRRP protocol is allowed between worker nodes on the public and private interfaces. Red Hat OpenShift on IBM Cloud uses the VRRP protocol to manage IP addresses for public and private load balancers.

</br>

### Opening required ports in a private firewall
{: #firewall_private}

If you have a firewall on the private network in your IBM Cloud infrastructure account, you must open IP ranges, ports, and protocols in your firewall to allow worker nodes to communicate with the master, with each other, with infrastructure resources, and with other {{site.data.keyword.cloud_notm}} services.
{:shortdesc}

1. Allow the IBM Cloud infrastructure private IP ranges so that you can create worker nodes in your cluster.
  1. Allow the appropriate IBM Cloud infrastructure private IP ranges. See [Backend (private) Network](/docs/infrastructure/hardware-firewall-dedicated?topic=hardware-firewall-dedicated-ibm-cloud-ip-ranges#backend-private-network).
  2. Allow the IBM Cloud infrastructure private IP ranges for all of the [zones](/docs/containers?topic=containers-regions-and-zones#zones) that you are using. **Note**: You must add IPs for the `dal01`, `dal10`, `wdc04` zones, and if your cluster is in the Europe geography, the `ams01` zone. See [Service Network (on backend/private network)](/docs/infrastructure/hardware-firewall-dedicated?topic=hardware-firewall-dedicated-ibm-cloud-ip-ranges#service-network-on-backend-private-network-).

2. Note the private IP address for each worker node in the cluster.
    ```
    ibmcloud oc worker ls --cluster <cluster_name_or_ID>
    ```
    {: pre}

3.  To allow worker nodes to communicate with the cluster master over the private service endpoint, allow outgoing network traffic from the source <em>&lt;each_worker_node_privateIP&gt;</em> to the destination TCP/UDP port range 20000-32767 and port 443. With DNS-based private service endpoints, the IP addresses can change. Whitelist the following private IP address range.
    ```
    166.8.0.0/14
    ```
    {: codeblock}

4. Open the following ports that are necessary for worker nodes to function properly.
  - Allow outbound TCP and UDP connections from the workers to ports 80 and 443 to allow worker node updates and reloads.
  - Allow outbound TCP and UDP to port 2049 to allow mounting file storage as volumes.
  - Allow outbound TCP and UDP to port 3260 for communication to block storage.
  - Allow inbound TCP and UDP connections to port 10250 for the OpenShift dashboard and commands such as `oc logs` and `oc exec`.
  - Allow inbound and outbound connections to TCP and UDP port 53 for DNS access.

5. Enable worker-to-worker communication by allowing all TCP, UDP, VRRP, and IPEncap traffic between worker nodes on the public and private interfaces. Red Hat OpenShift on IBM Cloud uses the VRRP protocol to manage IP addresses for private load balancers and the IPEncap protocol to permit pod to pod traffic across subnets.

7. {: #pvc}To create persistent volume claims in a cluster where worker nodes are connected to private VLANs only, make sure that your cluster is set up with the following Kubernetes version or {{site.data.keyword.cloud_notm}} storage plug-in versions. These versions enable private network communication from your cluster to your persistent storage instances.
    <table>
    <caption>Overview of required Kubernetes or {{site.data.keyword.cloud_notm}} storage plug-in versions for private clusters</caption>
    <thead>
      <th>Type of storage</th>
      <th>Required version</th>
   </thead>
   <tbody>
     <tr>
       <td>File storage</td>
       <td>Kubernetes version <code>1.13.4_1512</code>, <code>1.12.6_1544</code>, <code>1.11.8_1550</code>, <code>1.10.13_1551</code>, or later</td>
     </tr>
     <tr>
       <td>Block storage</td>
       <td>{{site.data.keyword.cloud_notm}} Block Storage plug-in version 1.3.0 or later</td>
     </tr>
     <tr>
       <td>Object storage</td>
       <td><ul><li>{{site.data.keyword.cos_full_notm}} plug-in version 1.0.3 or later</li><li>{{site.data.keyword.cos_full_notm}} service set up with HMAC authentication</li></ul></td>
     </tr>
   </tbody>
   </table>

   If you must use a Kubernetes version or {{site.data.keyword.cloud_notm}} storage plug-in version that does not support network communication over the private network, or if you want to use {{site.data.keyword.cos_full_notm}} without HMAC authentication, allow egress access through your firewall to IBM Cloud infrastructure and {{site.data.keyword.cloud_notm}} Identity and Access Management:
   - Allow all egress network traffic on TCP port 443.
   - Allow access to the IBM Cloud infrastructure IP range for the zone that your cluster is in for both the [**Front-end (public) network**](/docs/infrastructure/hardware-firewall-dedicated?topic=hardware-firewall-dedicated-ibm-cloud-ip-ranges#frontend-public-network) and [**Back-end (private) Network**](/docs/infrastructure/hardware-firewall-dedicated?topic=hardware-firewall-dedicated-ibm-cloud-ip-ranges#backend-private-network). To find the zone of your cluster, run `ibmcloud oc cluster ls`.

</br>

### Opening ports in a public or private firewall for inbound traffic to NodePort, load balancer, and Ingress services, and OpenShift routes
{: #firewall_inbound}

You can allow incoming access to NodePort, load balancer, and Ingress services, and OpenShift routes.
{:shortdesc}

<dl>
  <dt>NodePort service</dt>
  <dd>Open the port that you configured when you deployed the service to the public or private IP addresses for all of the worker nodes to allow traffic to. To find the port, run `oc get svc`. The port is in the 20000-32000 range.<dd>
  <dt>Load balancer service</dt>
  <dd>Open the port that you configured when you deployed the service to the load balancer service's public or private IP address.</dd>
  <dt>Ingress</dt>
  <dd>Open port 80 for HTTP or port 443 for HTTPS to the public or private IP address for the Ingress application load balancer.</dd>
  <dt>Route</dt>
  <dd>Open port 80 for HTTP or port 443 for HTTPS to the router's public IP address.</dd>
</dl>

<br />


## Allowing the cluster to access resources through Calico network policies
{: #firewall_calico_egress}

Instead of setting up a gateway firewall device, you can choose to use [Calico network policies](/docs/containers?topic=containers-network_policies) to act as a cluster firewall on the public or private network. For more information, see the following topics.
{: shortdesc}

* [Isolating clusters on the public network](/docs/containers?topic=containers-network_policies#isolate_workers_public).
* [Isolating clusters on the private network](/docs/containers?topic=containers-network_policies#isolate_workers).

<br />


## Whitelisting your cluster in other services' firewalls or in on-premises firewalls
{: #whitelist_workers}

If you want to access services that run inside or outside {{site.data.keyword.cloud_notm}} or on-premises and that are protected by a firewall, you can add the IP addresses of your worker nodes in that firewall to allow outbound network traffic to your cluster. For example, you might want to read data from an {{site.data.keyword.cloud_notm}} database that is protected by a firewall, or whitelist your worker node subnets in an on-premises firewall to allow network traffic from your cluster.
{:shortdesc}

1.  [Log in to your account. If applicable, target the appropriate resource group. Set the context for your cluster.](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure)

2. Get the worker node subnets or the worker node IP addresses.
  * **Worker node subnets**: If you anticipate changing the number of worker nodes in your cluster frequently, such as if you enable the [cluster autoscaler](/docs/containers?topic=containers-ca#ca), you might not want to update your firewall for each new worker node. Instead, you can whitelist the VLAN subnets that the cluster uses. Keep in mind that the VLAN subnet might be shared by worker nodes in other clusters.
    <p class="note">The **primary public subnets** that Red Hat OpenShift on IBM Cloud provisions for your cluster come with 14 available IP addresses, and can be shared by other clusters on the same VLAN. When you have more than 14 worker nodes, another subnet is ordered, so the subnets that you need to whitelist can change. To reduce the frequency of change, create worker pools with worker node flavors of higher CPU and memory resources so that you don't need to add worker nodes as often.</p>
    1. List the worker nodes in your cluster.
      ```
      ibmcloud oc worker ls --cluster <cluster_name_or_ID>
      ```
      {: pre}

    2. From the output of the previous step, note all the unique network IDs (first three octets) of the **Public IP** for the worker nodes in your cluster. If you want to whitelist a private-only cluster, note the **Private IP** instead. In the following output, the unique network IDs are `169.xx.178` and `169.xx.210`.
        ```
        ID                                                  Public IP        Private IP     Machine Type        State    Status   Zone    Version   
        kube-dal10-crb2f60e9735254ac8b20b9c1e38b649a5-w31   169.xx.178.101   10.xxx.xx.xxx   b3c.4x16.encrypted   normal   Ready    dal10   1.14.6   
        kube-dal10-crb2f60e9735254ac8b20b9c1e38b649a5-w34   169.xx.178.102   10.xxx.xx.xxx   b3c.4x16.encrypted   normal   Ready    dal10   1.14.6  
        kube-dal12-crb2f60e9735254ac8b20b9c1e38b649a5-w32   169.xx.210.101   10.xxx.xx.xxx   b3c.4x16.encrypted   normal   Ready    dal12   1.14.6   
        kube-dal12-crb2f60e9735254ac8b20b9c1e38b649a5-w33   169.xx.210.102   10.xxx.xx.xxx   b3c.4x16.encrypted   normal   Ready    dal12   1.14.6  
        ```
        {: screen}
    3.  List the VLAN subnets for each unique network ID.
        ```
        ibmcloud sl subnet list | grep -e <networkID1> -e <networkID2>
        ```
        {: pre}

        Example output:
        ```
        ID        identifier       type                 network_space   datacenter   vlan_id   IPs   hardware   virtual_servers
        1234567   169.xx.210.xxx   ADDITIONAL_PRIMARY   PUBLIC          dal12        1122334   16    0          5   
        7654321   169.xx.178.xxx   ADDITIONAL_PRIMARY   PUBLIC          dal10        4332211   16    0          6    
        ```
        {: screen}
    4.  Retrieve the subnet address. In the output, find the number of **IPs**. Then, raise `2` to the power of `n` equal to the number of IPs. For example, if the number of IPs is `16`, then `2` is raised to the power of `4` (`n`) to equal `16`. Now get the subnet CIDR by subtracting the value of `n` from `32` bits. For example, when `n` equals `4`, then the CIDR is `28` (from the equation `32 - 4 = 28`). Combine the **identifier** mask with the CIDR value to get the full subnet address. In the previous output, the subnet addresses are:
        *   `169.xx.210.xxx/28`
        *   `169.xx.178.xxx/28`
  * **Individual worker node IP addresses**: If you have a small number of worker nodes that run only one app and do not need to scale, or if you want to whitelist only one worker node, list all the worker nodes in your cluster and note the **Public IP** addresses. If your worker nodes are connected to a private network only and you want to connect to {{site.data.keyword.cloud_notm}} services by using the private service endpoint, note the **Private IP** addresses instead. Only these worker nodes are whitelisted. If you delete the worker nodes or add worker nodes to the cluster, you must update your firewall accordingly.
    ```
    ibmcloud oc worker ls --cluster <cluster_name_or_ID>
    ```
    {: pre}
4.  Add the subnet CIDR or IP addresses to your service's firewall for outbound traffic or your on-premises firewall for inbound traffic.
5.  Repeat these steps for each cluster that you want to whitelist.

<br />


## Updating IAM whitelists for {{site.data.keyword.containershort}} IP addresses
{: #iam_whitelist}

By default, all IP addresses can be used to log in to the {{site.data.keyword.cloud_notm}} console and access your cluster. In the IBM Cloud Identity and Access Management (IAM) console, you can [create a whitelist by specifying which IP addresses have access](/docs/iam?topic=iam-ips), and all other IP addresses are restricted. If you use an IAM whitelist, you must whitelist the CIDRs of the {{site.data.keyword.containerlong_notm}} control plane for the zones in the region where your cluster is located. You must whitelist these CIDRs so that {{site.data.keyword.containerlong_notm}} can create Ingress ALBs and `LoadBalancers` in your cluster.
{: shortdesc}

**Before you begin**: The following steps require you to change the IAM whitelist for the user whose credentials are used for the cluster's region and resource group infrastructure permissions. If you are the credentials owner, you can change your own IAM whitelist settings. If you are not the credentials owner, but you are assigned the **Editor** or **Administrator** IBM Cloud IAM platform role for the [User Management service](/docs/iam?topic=iam-account-services), you can update the restricted IP addresses for the credentials owner.

1. Identify what user credentials are used for the cluster's region and resource group infrastructure permissions.
    1.  Check the API key for a region and resource group of the cluster.
        ```
        ibmcloud oc api-key info --cluster <cluster_name_or_ID>
        ```
        {: pre}

        Example output:
        ```
        Getting information about the API key owner for cluster <cluster_name>...
        OK
        Name                Email   
        <user_name>         <name@email.com>
        ```
        {: screen}
    2.  Check if the infrastructure account for the region and resource group is manually set to use a different IBM Cloud infrastructure account.
        ```
        ibmcloud oc credential get --region <us-south>
        ```
        {: pre}

        **Example output if credentials are set to use a different account**. In this case, the user's infrastructure credentials are used for the region and resource group that you targeted, even if a different user's credentials are stored in the API key that you retrieved in the previous step.
        ```
        OK
        Infrastructure credentials for user name <1234567_name@email.com> set for resource group <resource_group_name>.
        ```
        {: screen}

        **Example output if credentials are not set to use a different account**. In this case, the API key owner that you retrieved in the previous step has the infrastructure credentials that are used for the region and resource group.
        ```
        FAILED
        No credentials set for resource group <resource_group_name>.: The user credentials could not be found. (E0051)
        ```
        {: screen}
2. Log in to the [{{site.data.keyword.cloud_notm}} console ![External link icon](../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/).
3. From the menu bar, click **Manage** > **Access (IAM)**, and select **Users**.
4. Select the user that you found in step 1 from the list.
5. From the **User details** page, go to the **IP address restrictions** section.
6. For **Classic infrastructure**, enter the CIDRs of the zones in the region where your cluster is located.<p class="note">You must whitelist all of the zones within the region that your cluster is in.</p>
  <table summary="The first row in the table spans both columns. The rest of the rows should be read left to right, with the region in column one, the zone in column two, and IP addresses to match in column three.">
  <caption>CIDRs to whitelist in IAM</caption>
    <thead>
    <th>Region</th>
    <th>Zone</th>
    <th>Private IP address</th>
    </thead>
  <tbody>
    <tr>
      <td>AP North</td>
      <td>che01<br>hkg02<br>seo01<br>sng01<br><br>tok02, tok04, tok05</td>
      <td><code>169.38.111.192/26, 169.38.113.64/27, 169.38.97.192/28</code><br><code>169.56.143.0/26</code><br><code>169.56.110.64/26</code><br><code>119.81.192.0/26</code><br><br><code>161.202.136.0/26, 169.56.40.128/25, 128.168.68.128/26, 165.192.70.64/26</code></td>
     </tr>
    <tr>
       <td>AP South</td>
       <td>mel01<br><br>syd01, syd04, syd05</td>
       <td><code>168.1.122.192/26</code><br><br><code>168.1.199.0/26, 168.1.209.192/26, 168.1.212.128/25, 130.198.67.0/26, 130.198.74.128/26, 130.198.78.128/25, 130.198.92.192/26, 130.198.96.128/25, 130.198.98.0/24, 135.90.68.64/28, 135.90.69.16/28, 135.90.69.160/27, 135.90.73.0/26, 135.90.75.0/27, 135.90.78.128/26</code></td>
    </tr>
    <tr>
       <td>EU Central</td>
       <td>ams03<br>mil01<br>osl01<br>par01<br><br>fra02, fra04, fra05</td>
       <td><code>169.50.177.128/25, 169.50.185.32/27, 169.51.161.128/25, 169.51.39.64/26, 169.51.41.64/26</code><br><code>159.122.157.192/26, 159.122.168.128/25, 159.122.169.64/26, 169.51.193.0/24</code><br><code>169.51.84.64/26</code><br><code>159.8.74.64/27, 169.51.22.64/26, 169.51.28.128/25, 169.51.3.64/26</code><br><br><code>158.177.160.0/25, 158.177.84.64/26, 169.50.48.160/28, 169.50.58.160/27, 161.156.102.0/26, 161.156.125.80/28, 161.156.66.224/27, 149.81.105.192/26, 149.81.124.16/28, 149.81.72.192/27</code></td>
      </tr>
    <tr>
      <td>UK South</td>
      <td>lon02, lon04, lon06</td>
      <td><code>159.8.171.0/26, 169.50.199.64/26, 169.50.220.32/27, 169.50.221.0/25, 158.175.101.64/26, 158.175.136.0/25, 158.175.136.128/25, 158.175.139.0/25, 158.175.141.0/24, 158.175.68.192/26, 158.175.77.64/26, 158.175.78.192/26, 158.175.81.128/25, 158.176.111.128/26, 158.176.112.0/26, 158.176.66.208/28, 158.176.75.240/28, 158.176.92.32/27, 158.176.95.64/27</code></td>
    </tr>
    <tr>
      <td>US East</td>
       <td>mon01<br>tor01<br><br>wdc04, wdc06, wdc07</td>
       <td><code>169.54.109.192/26</code><br><code>169.53.178.192/26, 169.55.148.128/25</code><br><br><code>169.47.160.0/26, 169.47.160.128/26, 169.60.104.64/26, 169.60.76.192/26, 169.63.137.0/25, 169.61.85.64/26, 169.62.0.64/26</code></td>
    </tr>
    <tr>
      <td>US South</td>
      <td>hou02<br>mex01<br>sao01<br>sjc03<br>sjc04<br><br>dal10,dal12,dal13</td>
      <td><code>173.193.93.0/24, 184.172.208.0/25, 184.173.6.0/26</code><br><code>169.57.18.48/28, 169.57.91.0/27</code><br><code>169.57.190.64/26, 169.57.192.128/25</code><br><code>169.44.207.0/26</code><br><code>169.62.73.192/26</code><br><br><code>169.46.30.128/26, 169.48.138.64/26, 169.48.180.128/25, 169.61.206.128/26, 169.63.199.128/25, 169.63.205.0/25, 169.47.126.192/27, 169.47.79.192/26, 169.48.201.64/26, 169.48.212.64/26, 169.48.238.128/25, 169.61.137.64/26, 169.61.176.64/26, 169.61.188.128/25, 169.61.189.128/25, 169.63.18.128/25, 169.63.20.0/25, 169.63.24.0/24, 169.60.131.192/26, 169.62.130.0/26, 169.62.130.64/26, 169.62.216.0/25, 169.62.222.0/25, 169.62.253.0/25</code></td>
    </tr>
    </tbody>
  </table>
7. Click **Apply**.



