---

copyright:
  years: 2014, 2021
lastupdated: "2021-08-13"

keywords: openshift, roks, rhoks, rhos

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

 
  

# Classic: Opening required ports and IP addresses in your firewall
{: #firewall}

<img src="images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> This firewall information is specific to classic clusters. For VPC clusters, see [Opening required ports and IP addresses in your firewall for VPC clusters](/docs/openshift?topic=openshift-vpc-firewall).
{: note}

Review these situations in which you might need to open specific ports and IP addresses in your firewalls for your {{site.data.keyword.openshiftlong}} clusters.
{: shortdesc}

* [Corporate firewalls](#corporate): If corporate network policies prevent access from your local system to public endpoints via proxies or firewalls, you must allow access to run `ibmcloud`, `ibmcloud oc`, `ibmcloud cr`, `oc`, and `calicoctl` commands from your local system.
* [Gateway appliance firewalls](#vyatta_firewall): If you have firewalls set up on the public or private network in your IBM Cloud infrastructure account, such as a VRA, you must open IP ranges, ports, and protocols to allow worker nodes to communicate with the master, with infrastructure resources, and with other {{site.data.keyword.cloud_notm}} services. You can also open ports to allow incoming traffic to services exposing apps in your cluster.
* [Calico network policies](#firewall_calico_egress): If you use Calico network policies to act as a firewall to restrict all worker node egress, you must allow your worker nodes to access the resources that are required for the cluster to function.
* [Other services or network firewalls](#allowlist_workers): To allow your cluster to access services that run inside or outside {{site.data.keyword.cloud_notm}} or in on-premises networks and that are protected by a firewall, you must add the IP addresses of your worker nodes in that firewall.


## Opening ports in a corporate firewall 
{: #corporate}

If corporate network policies prevent access from your local system to public endpoints via proxies or firewalls, you must allow access to run [`ibmcloud`, `ibmcloud oc`, and `ibmcloud cr` commands](#firewall_bx), [`oc` commands](#firewall_kubectl), and [`calicoctl` commands](#firewall_calicoctl) from your local system.
{: shortdesc}

### Running `ibmcloud`, `ibmcloud oc`, and `ibmcloud cr` commands from behind a firewall
{: #firewall_bx}

If corporate network policies prevent access from your local system to public endpoints via proxies or firewalls, to run `ibmcloud`, `ibmcloud oc` and `ibmcloud cr` commands, you must allow TCP access for {{site.data.keyword.cloud_notm}}, {{site.data.keyword.openshiftlong_notm}}, and {{site.data.keyword.registrylong_notm}}.
{: shortdesc}

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
    ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

    ```
    {: screen}


5. Allow access to the [{{site.data.keyword.registrylong_notm}} regions](/docs/Registry?topic=Registry-registry_overview#registry_regions) that you plan to use on port 443 and 4443 in your firewall. The global registry stores IBM-provided public images, and regional registries store your own private or public images. If your firewall is IP-based, you can see which IP addresses are opened when you allow access to the {{site.data.keyword.registrylong_notm}} regional service endpoints by reviewing [this table](#firewall_registry).

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




### Running `oc` commands from behind a firewall
{: #firewall_kubectl}

If corporate network policies prevent access from your local system to public endpoints via proxies or firewalls, to run `oc` commands, you must allow TCP access for the cluster.
{: shortdesc}

When a cluster is created, the port in the service endpoint URLs is randomly assigned from within 20000-32767. You can either choose to open port range 20000-32767 for any cluster that might get created or you can choose to allow access for a specific existing cluster.

Before you begin, allow access to [run `ibmcloud oc` commands](#firewall_bx).

To allow access for a specific cluster:

1. Log in to the {{site.data.keyword.cloud_notm}} CLI. Enter your {{site.data.keyword.cloud_notm}} credentials when prompted. If you have a federated account, include the `--sso` option.

    ```
    ibmcloud login [--sso]
    ```
    {: pre}

2. If the cluster is in a resource group other than `default`, target that resource group. To see the resource group that each cluster belongs to, run `ibmcloud oc cluster ls`. **Note**: You must have at least the [**Viewer** role](/docs/openshift?topic=openshift-users#checking-perms) for the resource group.

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

    * If the public cloud service endpoint is enabled:
    
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

    * If the private cloud service endpoint is enabled, you must be in your {{site.data.keyword.cloud_notm}} private network or connect to the private network through a VPN connection to verify your connection to the master. **Note**: You must [expose the master endpoint through a private load balancer](/docs/openshift?topic=openshift-access_cluster#access_private_se) so that users can access the master through a VPN or {{site.data.keyword.BluDirectLink}} connection.
    
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



### Running `calicoctl` commands from behind a firewall
{: #firewall_calicoctl}

If corporate network policies prevent access from your local system to public endpoints via proxies or firewalls, to run `calicoctl` commands, you must allow TCP access for the Calico commands.
{: shortdesc}

Before you begin, allow access to run [`ibmcloud` commands](#firewall_bx) and [`oc` commands](#firewall_kubectl).

1. Retrieve the IP address from the master URL that you used to allow the [`oc` commands](#firewall_kubectl).

2. Get the port for etcd.

    ```
    oc get cm -n kube-system cluster-info -o yaml | grep etcd_host
    ```
    {: pre}

3. Allow access for the Calico policies via the master URL IP address and the etcd port.


## Opening ports in gateway appliance firewalls
{: #vyatta_firewall}
{: help}
{: support}

If you have firewalls set up on the [public network](#firewall_outbound) or [private network](#firewall_private) in your IBM Cloud infrastructure account, such as a Virtual Router Appliance (Vyatta), you must open IP ranges, ports, and protocols to allow worker nodes to communicate with the master, with infrastructure resources, and with other {{site.data.keyword.cloud_notm}} services.
{: shortdesc}

### Opening required ports in a public firewall
{: #firewall_outbound}

If you have a firewall on the public network in your IBM Cloud infrastructure account, such as a Virtual Router Appliance (Vyatta), you must open IP ranges, ports, and protocols in your firewall to allow worker nodes to communicate with the master, with infrastructure resources, and with other {{site.data.keyword.cloud_notm}} services.
{: shortdesc}

Before you begin, note the public IP address for each worker node in the cluster.

```
ibmcloud oc worker ls --cluster <cluster_name_or_ID>
```
{: pre}

#### Allow worker notes to communicate with cluster master
{: #master_ips}

To allow worker nodes to communicate with the cluster master over the public cloud service endpoint, allow outgoing network traffic from the source *<each_worker_node_publicIP>* to the destination TCP/UDP port range 20000-32767 and port 443, and the following IP addresses and network groups. Additionally, if you plan to use Ingress or routes to expose apps in your cluster, allow incoming network traffic through these ports to your worker node IP addresses as well so that the {{site.data.keyword.openshiftshort}} control plane can check the health of your routers.

* `TCP/UDP port range 20000-32767, port 443 FROM <each_worker_node_publicIP> TO <public_IPs>`
* Replace *<public_IPs>* with the public IP addresses of the region that your cluster is located.

| Region             | Public IP address  | 
|--------------------|------------------|
| AP North (`che01`, `hkg02`, `seo01`, `sng01`, `tok02`, `tok04`, `tok05`) | `119.81.222.210`, `128.168.71.117`, `128.168.75.194`, `128.168.85.154`, `135.90.69.66`, `135.90.69.82`, `161.202.126.210`, `161.202.186.226`, `161.202.56.10`, `161.202.57.34`, `165.192.69.69`, `165.192.80.146`, `165.192.95.90`, `169.38.70.10`, `169.38.79.170`, `169.56.1.162`, `169.56.132.234`, `169.56.48.114`, `169.56.69.242`, `169.56.96.42` | 
| AP South (`syd01`, `syd04`, `syd05`) | `130.198.64.19`, `130.198.66.26`, `130.198.79.170`, `130.198.83.34`, `130.198.102.82`, `135.90.66.2`, `135.90.69.82`, `135.90.68.114`, `135.90.89.234`, `168.1.6.106`, `168.1.8.195`, `168.1.12.98`, `168.1.39.34`, `168.1.58.66` | 
| EU Central (`ams03`, `mil01`, `osl01`, `par01`, `fra02`, `fra04`, `fra05`) | `149.81.103.98`, `149.81.104.122`, `149.81.113.154`, `149.81.123.18`, `149.81.142.90`, `149.81.180.114`, `149.81.180.122`, `149.81.78.114`, `158.177.107.50`, `158.177.112.146`, `158.177.138.138`, `158.177.151.2`, `158.177.156.178`, `158.177.198.138`, `158.177.79.34`, `159.122.141.69`, `159.122.150.2`, `159.8.79.250`, `159.8.86.149`, `161.156.115.138`, `161.156.12.82`, `161.156.120.74`, `161.156.183.218`, `161.156.187.226`, `161.156.65.42`, `161.156.65.82`, `161.156.79.26`, `169.50.146.82`, `169.50.169.110`, `169.50.184.18`, `169.50.56.174`, `169.51.73.50`, `169.51.91.162` |
| Osaka (`osa21`, `osa22`,` osa23`) | `163.68.69.114`, `163.68.69.122`, `163.69.65.114`, `163.69.65.122`, `163.73.64.250`, `163.73.65.194` | 
| UK South (`lon02`, `lon04`, `lon05`, `lon06`) | `141.125.66.26`, `141.125.77.58`, `141.125.91.138`, `158.175.65.170`, `158.175.77.178`, `158.175.111.42`, `158.175.125.194`, `158.175.150.122`, `158.176.71.242`, `158.176.94.26`, `158.176.95.146`, `158.176.123.130`, `158.176.142.26`, `159.122.224.242`, `159.122.242.78` |
| US East (`mon01`, `tor01`, `wdc04`, `wdc06`, `wdc07`) | `52.117.88.42`, `169.47.162.130`, `169.47.174.106`, `169.53.167.50`, `169.53.171.210`, `169.54.126.219`, `169.54.80.106`, `169.60.100.242`, `169.60.101.42`, `169.60.73.142`, `169.60.92.50`, `169.61.109.34`, `169.61.74.210`, `169.61.83.62`, `169.62.10.162`, `169.62.10.20`, `169.62.9.250`, `169.63.111.82`, `169.63.149.122`, `169.63.158.82`, `169.63.160.13`, `169.63.75.82`, `169.63.88.178`, `169.63.88.186`, `169.63.94.210` |
| US South (`mex01`, `sao01`, `sjc03`, `sjc04`, `dal10`, `dal12`, `dal13`) | `50.22.129.34`, `52.116.231.210`, `52.116.254.234`, `52.117.197.210`, `52.117.212.34`, `52.117.215.162`, `52.117.232.194`, `52.117.240.106`, `52.117.28.138`, `169.45.67.210`, `169.45.88.98`, `169.46.110.218`, `169.46.111.122`, `169.46.24.210`, `169.46.27.234`, `169.46.68.234`, `169.46.7.238`, `169.46.89.50`, `169.47.109.34`, `169.47.115.18`, `169.47.201.194`, `169.47.209.66`, `169.47.229.90`, `169.47.232.210`, `169.47.239.34`, `169.47.70.10`, `169.47.71.138`, `169.48.110.250`, `169.48.143.218`, `169.48.161.242`, `169.48.230.146`, `169.48.244.66`, `169.57.100.18`, `169.57.13.10`, `169.57.151.10`, `169.57.154.98`, `169.59.219.90`, `169.59.230.98`, `169.60.128.2`, `169.60.170.234`, `169.61.175.106`, `169.61.177.2`, `169.61.228.138`, `169.61.28.66`, `169.61.29.194`, `169.61.60.130`, `169.62.166.98`, `169.62.189.26`, `169.62.206.234`, `169.62.82.197`, `169.62.87.170`, `169.63.39.66`, `169.63.47.250` |
 {: summary="The first row in the table spans both columns. The rest of the rows should be read left to right, with the region in column one and IP addresses to match in column two."}
 {: caption="Table 1. IP addresses to open for outgoing traffic" caption-side="top"}

#### Allow worker nodes to communicate with {{site.data.keyword.registrylong_notm}}
{: #firewall_registry}

To permit worker nodes to communicate with {{site.data.keyword.registrylong_notm}}, allow outgoing network traffic from the worker nodes to [{{site.data.keyword.registrylong_notm}} regions](/docs/Registry?topic=Registry-registry_overview#registry_regions).

* `TCP port 443 FROM <each_worker_node_publicIP> TO <registry_subnet>`
* Replace *<registry_subnet>* with the registry subnet to which you want to allow traffic. The global registry stores IBM-provided public images, and regional registries store your own private or public images.
  
| {{site.data.keyword.openshiftlong_notm}} region | Registry address  | Registry public subnets |
|---------------|-------------|-------------| 
| Global registry across {{site.data.keyword.openshiftlong_notm}} regions | `icr.io`  Deprecated: `registry.bluemix.net` | `169.62.37.240/29`, `169.60.98.80/29`, `169.63.104.232/29` |
| AP North | `jp.icr.io` | `161.202.146.80/29`, `128.168.71.64/29`, `165.192.71.216/29` |
| AP South | `au.icr.io` Deprecated: `registry.au-syd.bluemix.net` | `168.1.1.240/29`, `130.198.88.128/29`, `135.90.66.48/29` |
| EU Central | `de.icr.io` Deprecated: `registry.eu-de.bluemix.net` | `169.50.58.104/29`, `161.156.93.16/29`, `149.81.79.152/29` |
| Osaka | `jp2.icr.io` | `163.68.67.32/28`, `163.69.67.0/28`, `163.73.67.64/28` |
| Toronto | `ca.icr.io` | `158.85.100.0/29`, `163.74.65.192/29`, `163.75.66.88/29` |
| UK South | `uk.icr.io` Deprecated: `registry.eu-gb.bluemix.net` | `158.175.97.184/29`</br>`158.176.105.64/29`, `141.125.71.136/29` |
| US East, US South | `us.icr.io` Deprecated: `registry.ng.bluemix.net` | `169.61.234.224/29`, `169.61.135.160/29`, `169.61.46.80/29` |
{: summary="The first row in the table spans both columns. The rest of the rows should be read left to right, with the server zone in column one and IP addresses to match in column two."}
{: caption="Table 2. IP addresses to open for Registry traffic" caption-side="top"}
    
#### Allow outgoing network traffic from worker node to IAM
{: #firewall-iam}

Allow outgoing network traffic from your worker node to {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM). Your firewall must be Layer 7 to allow the IAM domain name. IAM does not have specific IP addresses that you can allow. If your firewall does not support Layer 7, you can allow all HTTPS network traffic on port 443.

* `TCP port 443 FROM <each_worker_node_publicIP> TO https://iam.bluemix.net`
* `TCP port 443 FROM <each_worker_node_publicIP> TO https://iam.cloud.ibm.com`

#### Optional: Allow outgoing network traffic from the worker nodes to {{site.data.keyword.mon_short}} and {{site.data.keyword.la_short}} services
{: #firewall-mon-la}

* **{{site.data.keyword.mon_full_notm}}**: 
     
    - `TCP port 443, port 6443 FROM <each_worker_node_public_IP> TO <monitoring_public_IP>`
    - Replace *<monitoring_public_IP>* with the [{{site.data.keyword.mon_short}} IP addresses](/docs/monitoring?topic=monitoring-endpoints).
        
* **{{site.data.keyword.la_full_notm}}**:
     
    - `TCP port 443, port 80 FROM <each_worker_node_public_IP> TO <logging_public_IP>`
    - Replace *<logging_public_IP>* with the [{{site.data.keyword.la_short}} IP addresses](/docs/log-analysis?topic=log-analysis-endpoints#endpoints_api_public).

#### Next steps
{: #firewall_next_steps}

If you use load balancer services, ensure that all traffic that uses the VRRP protocol is allowed between worker nodes on the public and private interfaces. {{site.data.keyword.openshiftlong_notm}} uses the VRRP protocol to manage IP addresses for public and private load balancers.

If you use Ingress or routes to expose apps in your cluster, allow incoming network traffic from [Akamai's source IP addresses](https://github.com/IBM-Cloud/kube-samples/tree/master/akamai/gtm-liveness-test){: external} on port 80 to the IP addresses of your router services so that the {{site.data.keyword.openshiftshort}} control plane can check the health of your routers.

From 07 to 31 July 2021, the DNS provider is changed from Cloudflare to Akamai for all `containers.appdomain.cloud`, `containers.mybluemix.net`, and `containers.cloud.ibm.com` domains for all clusters in {{site.data.keyword.openshiftlong_notm}}. If you currently allow inbound traffic to your classic cluster from the Cloudflare source IP addresses, you must also allow inbound traffic from the [Akamai source IP addresses](https://github.com/IBM-Cloud/kube-samples/tree/master/akamai/gtm-liveness-test){: external} before 07 July. After the migration completes on 31 July, you can remove the Cloudflare IP address rules. For more information, see the [announcement](https://cloud.ibm.com/notifications?selected=1621697674798){: external}.
{: important}




### Opening required ports in a private firewall
{: #firewall_private}

If you have a firewall on the private network in your IBM Cloud infrastructure account, such as a Virtual Router Appliance (Vyatta), you must open IP ranges, ports, and protocols in your firewall to allow worker nodes to communicate with the master, with each other, with infrastructure resources, and with other {{site.data.keyword.cloud_notm}} services.
{: shortdesc}

**Before you begin**

1. Allow the IBM Cloud infrastructure private IP ranges so that you can create worker nodes in your cluster.

    1. Allow the appropriate IBM Cloud infrastructure private IP ranges. See [Backend (private) Network](/docs/hardware-firewall-dedicated?topic=hardware-firewall-dedicated-ibm-cloud-ip-ranges#back-end-private-network).
    2. Allow the IBM Cloud infrastructure private IP ranges for all of the [zones](/docs/openshift?topic=openshift-regions-and-zones#locations) that you are using. **Note**: You must add the `166.8.0.0/14` and `161.26.0.0/16` IP ranges, the IP ranges for the `dal01`, `dal10`, `wdc04` zones, and if your cluster is in the Europe geography, the `ams01` zone. See [Service Network (on backend/private network)](/docs/hardware-firewall-dedicated?topic=hardware-firewall-dedicated-ibm-cloud-ip-ranges#service-network-on-back-end-private-network-).

2. Note the private IP address for each worker node in the cluster.

    ```
    ibmcloud oc worker ls --cluster <cluster_name_or_ID>
    ```
    {: pre}

#### Allow worker nodes to communicate with cluster master
{: #firewall_private_worker}

To allow worker nodes to communicate with the cluster master over the private cloud service endpoint, allow outgoing network traffic from the source *<each_worker_node_privateIP>* to the destination TCP/UDP port range 20000-32767 and port 443, and the following IP addresses and network groups.

*`TCP/UDP port range 20000-32767, port 443 FROM <each_worker_node_privateIP> TO <private_IPs>`
* Replace *<private_IPs>* with the private IP addresses of the region where your cluster is located.
    
| Region | Private IP address  |
|---------------|-------------|
| AP North (`che01`, `hkg02`, `seo01`, `sng01`, `tok02`, `tok04`, `tok05`) | `166.9.40.21`, `166.9.40.36`, `166.9.40.39`, `166.9.40.6`, `166.9.40.7`, `166.9.40.8`, `166.9.42.23`, `166.9.42.28`, `166.9.42.55`, `166.9.42.6`, `166.9.42.7`, `166.9.44.15`, `166.9.44.3`, `166.9.44.4`, `166.9.44.47`, `166.9.44.5`, `166.9.46.4`, `166.9.60.2` |
| AP South (`syd01`, `syd04`, `syd05`) | `166.9.52.14`, `166.9.52.15`, `166.9.52.23`, `166.9.52.30`, `166.9.52.31`, `166.9.54.11`, `166.9.54.12`, `166.9.54.13`, `166.9.54.21`, `166.9.54.32`, `166.9.54.33`, `166.9.56.10`, `166.9.56.11`, `166.9.56.16`, `166.9.56.24`, `166.9.56.36` |
| EU Central (`ams03`, `mil01`, `osl01`, `par01`, `fra02`, `fra04`, `fra05`) | `166.9.28.107`, `166.9.28.17`, `166.9.28.19`, `166.9.28.20`, `166.9.28.22`, `166.9.28.23`, `166.9.28.24`, `166.9.28.43`, `166.9.28.64`, `166.9.28.84`, `166.9.28.87`, `166.9.28.91`, `166.9.28.94`, `166.9.28.95`, `166.9.30.100`, `166.9.30.11`, `166.9.30.12`, `166.9.30.13`, `166.9.30.22`, `166.9.30.41`, `166.9.30.54`, `166.9.30.56`, `166.9.30.9`, `166.9.30.92`, `166.9.32.101`, `166.9.32.20`, `166.9.32.26`, `166.9.32.27`, `166.9.32.28`, `166.9.32.44`, `166.9.32.54`, `166.9.32.56`, `166.9.32.8`, `166.9.32.84`, `166.9.32.88`, `166.9.32.9` |
| Osaka (`osa21`, `osa22`, `osa23`) | `166.9.70.6`, `166.9.70.8`, `166.9.71.8`, `166.9.71.10`, `166.9.72.9`, `166.9.72.10` | 
| UK South (`lon02`,` lon04`, `lon05`, `lon06`) | `166.9.34.17`, `166.9.34.42`, `166.9.34.45`, `166.9.34.5`, `166.9.34.50`, `166.9.34.6`, `166.9.36.10`, `166.9.36.11`, `166.9.36.12`, `166.9.36.13`, `166.9.36.23`, `166.9.36.30`, `166.9.36.54`, `166.9.36.65`, `166.9.38.18`, `166.9.38.28`, `166.9.38.47`, `166.9.38.54`, `166.9.38.6`, `166.9.38.7` |
| US East (`mon01`, `tor01`, `wdc04`, `wdc06`,` wdc07`) | `166.9.20.11`, `166.9.20.117`, `166.9.20.12`, `166.9.20.13`, `166.9.20.187`, `166.9.20.38`, `166.9.20.42`, `166.9.20.63`, `166.9.20.80`, `166.9.22.10`, `166.9.22.109`, `166.9.22.26`, `166.9.22.43`, `166.9.22.51`, `166.9.22.52`, `166.9.22.8`, `166.9.22.9`, `166.9.24.19`, `166.9.24.22`, `166.9.24.35`, `166.9.24.4`, `166.9.24.45`, `166.9.24.47`, `166.9.24.5`, `166.9.24.90` |
| US South (`mex01`, `sao01`, `sjc03`, `sjc04`, `dal10`, `dal12`, `dal13`) | `166.9.12.140`, `166.9.12.141`, `166.9.12.142`, `166.9.12.143`, `166.9.12.144`, `166.9.12.151`, `166.9.12.193`, `166.9.12.196`, `166.9.12.26`, `166.9.12.99`, `166.9.13.31`, `166.9.13.93`, `166.9.13.94`, `166.9.14.122`, `166.9.14.125`, `166.9.14.202`, `166.9.14.204`, `166.9.14.205`, `166.9.14.95`, `166.9.15.130`, `166.9.15.69`, `166.9.15.70`, `166.9.15.71`, `166.9.15.72`, `166.9.15.73`, `166.9.15.74`, `166.9.15.75`, `166.9.15.76`, `166.9.16.113`, `166.9.16.137`, `166.9.16.149`, `166.9.16.183`, `166.9.16.184`, `166.9.16.185`, `166.9.16.38`, `166.9.16.39`, `166.9.16.5`, `166.9.17.2`, `166.9.17.35`, `166.9.17.37`, `166.9.17.39`, `166.9.48.124`, `166.9.48.171`, `166.9.48.175`, `166.9.48.50`, `166.9.48.76`, `166.9.51.104`, `166.9.51.106`, `166.9.51.16`, `166.9.51.54`, `166.9.51.74`, `166.9.58.104`, `166.9.58.11`, `166.9.58.16`, `166.9.58.170`, `166.9.58.65` |
{: summary="The first row in the table spans both columns. The rest of the rows should be read left to right, with the region in column one and IP addresses to match in column three."}
{: caption="Table 3. IP addresses to open for outgoing traffic" caption-side="top"}

#### Open ports
{: #firewall_private_open_ports}

Open the following ports that are necessary for worker nodes to function properly.

* Allow outbound TCP and UDP connections from the workers to ports 80 and 443 to allow worker node updates and reloads.
* Allow outbound TCP and UDP to port 2049 to allow mounting file storage as volumes.
* Allow outbound TCP and UDP to port 3260 for communication to block storage.
* Allow inbound TCP and UDP connections to port 10250 for the {{site.data.keyword.openshiftshort}} dashboard and commands such as `oc logs` and `oc exec`.
* Allow inbound and outbound connections to TCP and UDP port 53 and port 5353 for DNS access.

#### Enable worker-to-worker communication
{: #firewall_private_worker2worker}

Enable worker-to-worker communication by allowing all TCP, UDP, VRRP, and IPEncap traffic between worker nodes on the public and private interfaces. {{site.data.keyword.openshiftlong_notm}} uses the VRRP protocol to manage IP addresses for private load balancers and the IPEncap protocol to permit pod to pod traffic across subnets.

#### Permit worker nodes to communicate with {{site.data.keyword.registrylong_notm}}
{: #firewall_private_container_registry}

To permit worker nodes to communicate with {{site.data.keyword.registrylong_notm}}, allow outgoing network traffic from the worker nodes to [{{site.data.keyword.registrylong_notm}} regions](/docs/Registry?topic=Registry-registry_overview#registry_regions):

* `TCP port 443, port 4443 FROM <each_worker_node_privateIP> TO <registry_subnet>`
* Replace *<registry_subnet>* with the registry subnet to which you want to allow traffic. The global registry stores IBM-provided public images, and regional registries store your own private or public images. Port 4443 is required for notary functions, such as [Verifying image signatures](/docs/Registry?topic=Registry-registry_trustedcontent#registry_trustedcontent). 
    
| {{site.data.keyword.openshiftlong_notm}} region | Registry address  | Registry private IP addresses |
|---------------|-------------|-------------|
| Global registry across {{site.data.keyword.openshiftlong_notm}} regions | `private.icr.io` `cp.icr.io` | `166.9.20.31`, `166.9.22.22`, `166.9.24.16` |
| AP North | `private.jp.icr.io` | `166.9.40.20`, `166.9.42.21`, `166.9.44.12` |
| AP South | `private.au.icr.io` | `166.9.52.20`, `166.9.54.19`, `166.9.56.13` |
| EU Central | `private.de.icr.io` | `166.9.28.35`, `166.9.30.2`, `166.9.32.2` |
| Osaka | `private.jp2.icr.io` | `166.9.70.4`, `166.9.71.5`, `166.9.72.6` |
| Toronto | `private.ca.icr.io` | `166.9.76.12`, `166.9.77.11`, `166.9.78.11` |
| UK South | `private.uk.icr.io` | `166.9.36.19`, `166.9.38.14`, `166.9.34.12` |
| US East, US South | `private.us.icr.io` | `166.9.12.227`, `166.9.15.116`, `166.9.16.244` |
{: summary="The first row in the table spans both columns. The rest of the rows should be read left to right, with the server zone in column one and IP addresses to match in column two."}
{: caption="Table 4. IP addresses to open for Registry traffic" caption-side="top"}
   
#### Optional: Set up firewall rules for {{site.data.keyword.la_full_notm}} and {{site.data.keyword.mon_full_notm}} services
{: #firewall_private_mon_la}

To send logging and metric data, set up firewall rules for your {{site.data.keyword.la_full_notm}} and {{site.data.keyword.mon_full_notm}} services.

* [{{site.data.keyword.la_short}} private endpoints](/docs/log-analysis?topic=log-analysis-endpoints#endpoints_api_private)
* [{{site.data.keyword.mon_short}} private endpoints](/docs/monitoring?topic=monitoring-endpoints#endpoints_monitoring)


### Opening ports in a public or private firewall for inbound traffic to NodePort, load balancer, and Ingress services, and {{site.data.keyword.openshiftshort}} routes
{: #firewall_inbound}

You can allow incoming access to NodePort, load balancer, and Ingress services, and {{site.data.keyword.openshiftshort}} routes.
{: shortdesc}


<dl>
  <dt>NodePort service</dt>
  <dd>Open the port that you configured when you deployed the service to the public or private IP addresses for all of the worker nodes to allow traffic to. To find the port, run `oc get svc`. The port is in the 20000-32000 range.</dd>
  <dt>Load balancer service</dt>
  <dd>Open the port that you configured when you deployed the service to the load balancer service's public or private IP address.</dd>
  <dt>Ingress</dt>
  <dd>Open port 80 for HTTP and port 443 for HTTPS to the public or private IP address for the Ingress application load balancer.</dd>
  <dt>Route</dt>
  <dd>Open port 80 for HTTP and port 443 for HTTPS to the router's public IP address.</dd>
</dl>




## Allowing the cluster to access resources through Calico network policies
{: #firewall_calico_egress}

Instead of setting up a gateway firewall device, you can choose to use [Calico network policies](/docs/openshift?topic=openshift-network_policies) to act as a cluster firewall on the public or private network. For more information, see the following topics.
{: shortdesc}

* [Isolating clusters on the public network](/docs/openshift?topic=openshift-network_policies#isolate_workers_public).
* [Isolating clusters on the private network](/docs/openshift?topic=openshift-network_policies#isolate_workers).



## Allowing traffic from your cluster in other services' firewalls or in on-premises firewalls
{: #allowlist_workers}

If you want to access services that run inside or outside {{site.data.keyword.cloud_notm}} or on-premises and that are protected by a firewall, you can add the IP addresses of your worker nodes in that firewall to allow outbound network traffic to your cluster. For example, you might want to read data from an {{site.data.keyword.cloud_notm}} database that is protected by a firewall, or specify your worker node subnets in an on-premises firewall to allow network traffic from your cluster.
{: shortdesc}

1. [Access your {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-access_cluster).

2. Get the worker node subnets or the worker node IP addresses.

    * **Worker node subnets**: If you anticipate changing the number of worker nodes in your cluster frequently, such as if you enable the [cluster autoscaler](/docs/openshift?topic=openshift-ca#ca), you might not want to update your firewall for each new worker node. Instead, you can add the VLAN subnets that the cluster uses. Keep in mind that the VLAN subnet might be shared by worker nodes in other clusters.
    Note that the **primary public subnets** that {{site.data.keyword.openshiftlong_notm}} provisions for your cluster come with 14 available IP addresses, and can be shared by other clusters on the same VLAN. When you have more than 14 worker nodes, another subnet is ordered, so the subnets that you need to allow can change. To reduce the frequency of change, create worker pools with worker node flavors of higher CPU and memory resources so that you don't need to add worker nodes as often.
    
      1. List the worker nodes in your cluster.
    
         ```
         ibmcloud oc worker ls --cluster <cluster_name_or_ID>
         ```
         {: pre}

      2. From the output of the previous step, note all the unique network IDs (first three octets) of the **Public IP** for the worker nodes in your cluster. In the following output, the unique network IDs are `169.xx.178` and `169.xx.210`.
    
         ```sh
         ID                                                  Public IP        Private IP     Machine Type        State    Status   Zone    Version   
         kube-dal10-crb2f60e9735254ac8b20b9c1e38b649a5-w31   169.xx.178.101   10.xxx.xx.xxx   b3c.4x16.encrypted   normal   Ready    dal10   1.20.7   
         kube-dal10-crb2f60e9735254ac8b20b9c1e38b649a5-w34   169.xx.178.102   10.xxx.xx.xxx   b3c.4x16.encrypted   normal   Ready    dal10   1.20.7  
         kube-dal12-crb2f60e9735254ac8b20b9c1e38b649a5-w32   169.xx.210.101   10.xxx.xx.xxx   b3c.4x16.encrypted   normal   Ready    dal12   1.20.7   
         kube-dal12-crb2f60e9735254ac8b20b9c1e38b649a5-w33   169.xx.210.102   10.xxx.xx.xxx   b3c.4x16.encrypted   normal   Ready    dal12   1.20.7  
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

      4. Retrieve the subnet address. In the output, find the number of **IPs**. Then, raise `2` to the power of `n` equal to the number of IPs. For example, if the number of IPs is `16`, then `2` is raised to the power of `4` (`n`) to equal `16`. Now get the subnet CIDR by subtracting the value of `n` from `32` bits. For example, when `n` equals `4`, then the CIDR is `28` (from the equation `32 - 4 = 28`). Combine the **identifier** mask with the CIDR value to get the full subnet address. In the previous output, the subnet addresses are:
      
         *   `169.xx.210.xxx/28`
         *   `169.xx.178.xxx/28`
         
    * **Individual worker node IP addresses**: If you have a small number of worker nodes that run only one app and do not need to scale, or if you want to add only one worker node, list all the worker nodes in your cluster and note the **Public IP** addresses. If your worker nodes are connected to a private network only and you want to connect to {{site.data.keyword.cloud_notm}} services by using the private cloud service endpoint, note the **Private IP** addresses instead. Only these worker nodes are added. If you delete the worker nodes or add worker nodes to the cluster, you must update your firewall accordingly.
    
      ```
      ibmcloud oc worker ls --cluster <cluster_name_or_ID>
      ```
      {: pre}

4. Add the subnet CIDR or IP addresses to your service's firewall for outbound traffic or your on-premises firewall for inbound traffic.
5. Repeat these steps for each cluster that you want to allow traffic to or from.



## Updating IAM firewalls for {{site.data.keyword.containershort}} IP addresses
{: #iam_allowlist}

By default, all IP addresses can be used to log in to the {{site.data.keyword.cloud_notm}} console and access your cluster. In the IBM Cloud Identity and Access Management (IAM) console, you can generate a firewall by [creating an allowlist by specifying which IP addresses have access](/docs/account?topic=account-ips), and all other IP addresses are restricted. If you use an IAM firewall, you must add the CIDRs of the {{site.data.keyword.openshiftlong_notm}} control plane for the zones in the region where your cluster is located to the allowlist. You must allow these CIDRs so that {{site.data.keyword.openshiftlong_notm}} can create Ingress ALBs and `LoadBalancers` in your cluster.
{: shortdesc}

Setting up an IAM allowlist blocks access to the {{site.data.keyword.openshiftshort}} web console. Do not use an IAM allowlist if you must access the {{site.data.keyword.openshiftshort}} web console for your cluster.
{: important}

**Before you begin**: The following steps require you to change the IAM allowlist for the user whose credentials are used for the cluster's region and resource group infrastructure permissions. If you are the credentials owner, you can change your own IAM allowlist settings. If you are not the credentials owner, but you are assigned the **Editor** or **Administrator** IBM Cloud IAM platform access role for the [User Management service](/docs/account?topic=account-account-services), you can update the restricted IP addresses for the credentials owner.

1. Identify what user credentials are used for the cluster's region and resource group infrastructure permissions.

    1. Check the API key for a region and resource group of the cluster.
    
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
        
    2. Check if the infrastructure account for the region and resource group is manually set to use a different IBM Cloud infrastructure account.
    
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
        
2. Get the CIDRs of the private and public subnets that your worker nodes are attached to.

    ```
    ibmcloud oc cluster get -c <cluster_name_or_ID> --show-resources
    ```
    {: pre}

    Example output:
    
    ```
    Name:                           mycluster
    ID:                             df222b2222d64944ab99ed63bb4567b6
    State:                          normal
    Status:                         All Workers
    ...

    Subnet VLANs
    VLAN ID   Subnet CIDR        Public   User-managed
    2234947   10.176.22.48/29    false    false
    2294021   10.185.94.144/29   false    false
    2234945   169.46.17.0/29     true     false
    2294019   169.48.228.72/29   true     false
    ```
    {: screen}
    
3. Log in to the [{{site.data.keyword.cloud_notm}} console](https://cloud.ibm.com/){: external}.
4. From the menu bar, click **Manage** > **Access (IAM)**, and select **Users**.
5. Select the user that you found in step 1 from the list.
6. From the **User details** page, go to the **IP address restrictions** section.
7. For **Classic infrastructure**, enter the [CIDRs of the region where your cluster is located](https://github.com/IBM-Cloud/kube-samples/tree/master/iam-firewall-ips){: external}. To find the region that your cluster's zones are location in, see the `README` for the directory.
8. Enter the CIDRs of the worker node subnets that you found in step 2.
9. Click **Apply**.


