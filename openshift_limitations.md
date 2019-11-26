---

copyright:
  years: 2014, 2019
lastupdated: "2019-11-26"

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

# Service limitations
{: #openshift_limitations}

{{site.data.keyword.openshiftlong}} and the OpenShift open source project come with default service settings and limitations to ensure security, convenience, and basic functionality. Some of the limitations you might be able to change where noted.
{: shortdesc}
<br>

If you anticipate reaching any of the following Red Hat OpenShift on IBM Cloud limitations, contact the IBM team in the [internal ![External link icon](../icons/launch-glyph.svg "External link icon")](https://ibm-argonauts.slack.com/messages/C4S4NUCB1) or [external Slack ![External link icon](../icons/launch-glyph.svg "External link icon")](https://ibm-container-service.slack.com).
{: tip}

## Service limitations
{: #tech_limits}
<br>

Red Hat OpenShift on IBM Cloud comes with the following service limitations<roks311-vpc> that apply to all clusters, independent of what infrastructure provider you plan to use</roks311-vpc>. 
{: shortdesc}

In addition to the service limitations, make sure to also review the limitations for [classic](#classic_limits)<roks311-vpc> or [VPC](#vpc_ks_limits)</roks311-vpc> clusters.
{: note}

<table summary="This table contains information on the Red Hat OpenShift on IBM Cloud limitations. Columns are read from left to right. In the first column is the type of limitation and in the second column is the description of the limitation.">
<caption>Red Hat OpenShift on IBM Cloud limitations</caption>
<thead>
  <tr>
    <th>Category</th>
    <th>Description</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>API rate limits</td>
    <td>100 requests per 10 seconds to the Red Hat OpenShift on IBM Cloud API for each unique source IP address.</td>
  </tr>
  <tr>
    <td>Worker node host access</td>
    <td>For security, you cannot SSH into the worker node compute host.</td>
  </tr>
  <tr>
    <td>Kubernetes pod logs</td>
    <td>To check the logs for individual app pods, you can use the terminal to run `oc logs <pod name>`. Do not use the Kubernetes dashboard to stream logs for your pods, which might cause a disruption in your access to the Kubernetes dashboard.</td>
  </tr>
</tbody>
</table>


<br />

## OpenShift cluster limitations
{: #oc_limits}

Review the following limitations that are specific to Red Hat OpenShift on IBM Cloud clusters.
{: shortdesc}

### Cluster
{: #oc_limits_cluster}

*   You can create only standard clusters, not free clusters. Instead, you can create a free Kubernetes cluster, and then redeploy the apps that you try out in the Kubernetes cluster to your OpenShift cluster.
*   [Locations](/docs/openshift?topic=openshift-regions-and-zones) are available in all six worldwide multizone metro and select single zone regions.
*   You cannot create a cluster with worker nodes that run multiple operating systems, such as OpenShift on Red Hat Enterprise Linux and community Kubernetes on Ubuntu.


### Networking
{: #oc_limits_networking}

Private network load balancers (NLBs) cannot be registered with the domain name server (DNS), so the cluster cannot be created with only a private network interface. At least some of the cluster's worker nodes must have both public and private VLANs. You can still create a private service to expose your apps on only the private network.

### Storage
{: #oc_limits_storage}

Because of the way that {{site.data.keyword.cloud_notm}} NFS file storage configures Linux user permissions, you might encounter errors when you use file storage. If so, you might need to configure [OpenShift Security Context Constraints ![External link icon](../icons/launch-glyph.svg "External link icon")](https://docs.openshift.com/container-platform/3.11/admin_guide/manage_scc.html) or use a different storage type.

### Logging and Metrics
{: #oc_limits_metrics}

**Logging**: You cannot run the Ansible playbook to deploy the [OpenShift Container Platform Elasticsearch, Fluentd, and Kibana (EFK) stack ![External link icon](../icons/launch-glyph.svg "External link icon")](https://docs.openshift.com/container-platform/3.11/install_config/aggregate_logging.html) because you cannot modify the default configuration of the Red Hat OpenShift on IBM Cloud cluster.

**Metrics**: The [built-in Prometheus](/docs/openshift?topic=openshift-openshift_apps#openshift_access_oc_services) alert manager includes two rules that display as active alerts in a `FIRING` state: `KubeControllerManagerDown` and `KubeSchedulerDown`. These components are part of the IBM-managed cluster master, so you can ignore these alerts.

Example alert:
```
alert: KubeControllerManagerDown
expr: absent(up{job="kube-controllers"}
  == 1)
for: 15m
labels:
  severity: critical
annotations:
  message: KubeControllerManager has disappeared from Prometheus target discovery.
```
{: screen}

<br />



## Classic cluster limitations
{: #classic_limits}

Classic infrastructure clusters in Red Hat OpenShift on IBM Cloud are released with the following limitations.
{: shortdesc}

<table>
  <thead>
    <th>Category</th>
    <th>Description</th>
  </thead>
  <tbody>
    <tr>
      <td>Compute</td>
      <td><ul><li>Worker nodes are available in [select flavors](/docs/openshift?topic=openshift-planning_worker_nodes#shared_dedicated_node) of compute resources.</li><li>You can have 900 worker nodes per cluster. If you plan to exceed 900 per cluster, contact the Red Hat OpenShift on IBM Cloud team in the [internal ![External link icon](../icons/launch-glyph.svg "External link icon")](https://ibm-argonauts.slack.com/messages/C4S4NUCB1) or [external Slack ![External link icon](../icons/launch-glyph.svg "External link icon")](https://ibm-container-service.slack.com) first. If you see an IBM Cloud infrastructure capacity limit on the number of instances per data center or that are ordered each month, contact your IBM Cloud infrastructure representative.</li><li>You can run 110 pods per worker node. If you have worker nodes that run Kubernetes 1.13.7_1527, 1.14.3_1524, or later, and are provisioned with 11 CPU cores or more, you can support 10 pods per core, up to a limit of 250 pods per worker node. The number of pods includes `kube-system` and `ibm-system` pods that run on the worker node. For improved performance, consider limiting the number of pods that you run per compute core so that you do not overuse the worker node. For example, on a worker node with a `b3c.4x16` flavor, you might run 10 pods per core that use no more than 75% of the worker node total capacity.</li></ul></td>
    </tr>
    <tr>
      <td>Load balancing for apps</td>
      <td><ul><li>You can have 65,000 IPs per cluster in the 172.21.0.0/16 range that you can assign to Kubernetes services within the cluster.</li><li>The Ingress application load balancer (ALB) can process 32,768 connections per second. </li></ul>
      </td>
    </tr>
    <tr>
      <td>Storage</td>
      <td>You can have a total of 250 IBM Cloud infrastructure file and block storage volumes per account. If you mount more than this amount, you might see an "out of capacity" message when you provision persistent volumes and need to contact your IBM Cloud infrastructure representative. For more FAQs, see the [file](/docs/infrastructure/FileStorage?topic=FileStorage-file-storage-faqs#how-many-volumes-can-i-provision-) and [block](/docs/infrastructure/BlockStorage?topic=BlockStorage-block-storage-faqs#how-many-instances-can-share-the-use-of-a-block-storage-volume-) storage docs.</td>
    </tr>
  </tbody>
  </table><roks311-vpc>

## VPC cluster limitations
{: #vpc_ks_limits}

VPC Generation 1 compute clusters in Red Hat OpenShift on IBM Cloud are released with the following limitations.
{: shortdesc}


<table>
  <thead>
    <th>Category</th>
    <th>Description</th>
  </thead>
  <tbody>
    <tr>
      <td>Compute</td>
      <td><ul><li>You can have up to 100 worker nodes across all VPC clusters per account.</li><li>Only certain flavors are available for worker node virtual machines.</li><li>Bare metal machines are not supported.</li><li>You cannot update or reload worker nodes. Instead, you can delete the worker node and rebalance the worker pool with the <code>ibmcloud oc worker replace</code> command.</li></ul>
        </td>
    </tr>
    <tr>
      <td>Container platforms</td>
      <td>VPC clusters are available for only community Kubernetes clusters, not OpenShift clusters.</td>
    </tr>
    <tr>
      <td>Load balancing for apps</td>
      <td>See [Exposing apps with VPC load balancers: Limitations](/docs/openshift?topic=openshift-vpc-lbaas#lbaas_limitations). </td>
    </tr>
    <tr>
      <td>Location</td>
      <td>VPC clusters are available in the following [multizone metro locations](/docs/openshift?topic=openshift-regions-and-zones#zones): Dallas, Frankfurt, London, Sydney, and Tokyo.</td>
    </tr>
    <tr>
      <td>Security groups</td>
      <td>You cannot use [VPC security groups](/docs/infrastructure/security-groups?topic=security-groups-about-ibm-security-groups#about-ibm-security-groups) to control traffic for your cluster. VPC security groups are applied to the network interface of a single virtual server to filter traffic at the hypervisor level. However, the worker nodes of your VPC cluster exist in a service account and are not listed in the VPC infrastructure dashboard. You cannot attach a security group to your worker nodes instances.</td>
    </tr>
    <tr>
      <td>Storage</td>
      <td><ul><li>You can set up VPC Block Storage and {{site.data.keyword.cos_full_notm}} only.</li><li>VPC Block Storage is available as a cluster add-on. For more information, see [Storing data on VPC Block Storage](/docs/openshift?topic=openshift-vpc-block). Make sure to [attach a public gateway to all the VPC subnets](/docs/vpc-on-classic?topic=vpc-on-classic-creating-a-vpc-using-the-ibm-cloud-cli#step-5-attach-a-public-gateway) that the cluster uses so that you can provision VPC Block Storage.</li><li>{{site.data.keyword.cos_full_notm}} is available as a Helm chart. For more information, see [Storing data on {{site.data.keyword.cos_full_notm}}](/docs/openshift?topic=openshift-object_storage).</li><li>File storage and Portworx software-defined storage (SDS) are not available.</li></ul></td>
    </tr>
    <tr>
      <td>strongSwan VPN service</td>
      <td>Only [outbound VPN connections from the cluster](/docs/openshift?topic=openshift-vpn#strongswan_3) can be established. Additionally, because VPC clusters do not support UDP load balancers, the following <code>config.yaml</code> options are not supported for use in strongSwan Helm charts in VPC clusters: <ul><li><code>enableServiceSourceIP</code></li><li><code>loadBalancerIP</code></li><li><code>zoneLoadBalancer</code></li><li><code>connectUsingLoadBalancerIP</code></li></ul></td>
    </tr>
    <tr>
      <td>Versions</td>
      <td>VPC clusters must run Kubernetes version 1.15 or later.</td>
    </tr>
    <tr>
      <td>Virtual Private Cloud</td>
      <td>See [Known limitations](/docs/vpc-on-classic?topic=vpc-on-classic-known-limitations).</td>
    </tr>
    <tr>
      <td>v2 API</td>
      <td>VPC clusters use the [Red Hat OpenShift on IBM Cloud v2 API](/docs/openshift?topic=openshift-cs_api_install#api_about). The v2 API is currently under development, with only a limited number of API operations currently available. You can run certain v1 API operations against the VPC cluster, such as `GET /v1/clusters` or `ibmcloud oc cluster ls`, but not all the information that a Classic cluster has is returned or you might experience unexpected results. For supported VPC v2 operations, see the [CLI reference topic for VPC commands](/docs/openshift?topic=openshift-kubernetes-service-cli#cli_classic_vpc_about).</td>
    </tr>
  </tbody>
  </table></roks311-vpc>



