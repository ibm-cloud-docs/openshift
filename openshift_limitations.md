---

copyright:
  years: 2014, 2020
lastupdated: "2020-02-06"

keywords: openshift, roks, rhoks, rhos

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


# Service limitations
{: #openshift_limitations}

{{site.data.keyword.openshiftlong}} and the OpenShift open source project come with default service settings and limitations to ensure security, convenience, and basic functionality. Some of the limitations you might be able to change where noted.
{: shortdesc}
<br>

If you anticipate reaching any of the following Red Hat OpenShift on IBM Cloud limitations, contact the IBM team in the [internal](https://ibm-argonauts.slack.com/messages/C4S4NUCB1){: external} or [external Slack](https://ibm-container-service.slack.com){: external}.
{: tip}

## Service limitations
{: #tech_limits}

Red Hat OpenShift on IBM Cloud comes with the following service limitations.
{: shortdesc}

| Category | Description |
| -------- | ----------- |
| API rate limits | 100 requests per 10 seconds to the Red Hat OpenShift on IBM Cloud API for each unique source IP address. |
| App deployment | The apps that you deploy to and services that you integrate with your cluster must be able to run on the operating system of the worker nodes. |
| Container images | You cannot use the [Container Image Security Enforcement (CISE) Helm chart](/docs/services/Registry?topic=registry-security_enforce) with OpenShift clusters. |
| Free clusters | You can create only standard clusters, not free clusters. Instead, you can create a free Kubernetes cluster, and then redeploy the apps that you try out in the Kubernetes cluster to your OpenShift cluster. |
| Kubernetes | Make sure to review the [Kubernetes project limitations](https://kubernetes.io/docs/setup/best-practices/cluster-large/){: external}. |
| OpenShift | Make sure to review the [OpenShift Container Platform limitations](https://docs.openshift.com/container-platform/3.11/scaling_performance/cluster_limits.html#scaling-performance-cluster-limits){: external} for your version.|
| Kubernetes pod logs | To check the logs for individual app pods, you can use the terminal to run `oc logs <pod name>`. Do not use the Kubernetes dashboard to stream logs for your pods, which might cause a disruption in your access to the Kubernetes dashboard. |
| Kubernetes API audit logs | Collecting and forwarding API audit logs to {{site.data.keyword.la_full_notm}} is not supported. |
| Logging | You cannot run the Ansible playbook to deploy the [OpenShift Container Platform Elasticsearch, Fluentd, and Kibana (EFK) stack](https://docs.openshift.com/container-platform/3.11/install_config/aggregate_logging.html){: external} because you cannot modify the default configuration of the Red Hat OpenShift on IBM Cloud cluster. |
| Monitoring | The [built-in Prometheus](/docs/openshift?topic=openshift-openshift_apps#openshift_access_oc_services) alert manager includes two rules that display as active alerts in a `FIRING` state: `KubeControllerManagerDown` and `KubeSchedulerDown`. These components are part of the IBM-managed cluster master, so you can ignore these alerts.</br></br>Example alert:</br>`alert: KubeControllerManagerDown`</br>`expr: absent(up{job="kube-controllers"}`</br>`  == 1)</br>for: 15m</br>labels:`</br>  `severity: critical`</br>`annotations:`</br>` message: KubeControllerManager has disappeared from Prometheus target discovery.`|
{: summary="This table contains information on general Red Hat OpenShift on IBM Cloud limitations. Columns are read from left to right. In the first column is the type of limitation and in the second column is the description of the limitation."}
{: caption="Red Hat OpenShift on IBM Cloud limitations"}

<br />




## Classic cluster limitations
{: #classic_limits}

Classic infrastructure clusters in Red Hat OpenShift on IBM Cloud are released with the following limitations.
{: shortdesc}

### Compute
{: #classic_compute_limit}

</br>

| Category | Description |
| -------- | ----------- |
| Operating system | You cannot create a cluster with worker nodes that run multiple operating systems, such as OpenShift on Red Hat Enterprise Linux and community Kubernetes on Ubuntu. |
| Pod instances | You can run 110 pods per worker node. If you have worker nodes that run Kubernetes 1.13.7_1527, 1.14.3_1524, or later, and are provisioned with 11 CPU cores or more, you can support 10 pods per core, up to a limit of 250 pods per worker node. The number of pods includes `kube-system` and `ibm-system` pods that run on the worker node. For improved performance, consider limiting the number of pods that you run per compute core so that you do not overuse the worker node. For example, on a worker node with a `b3c.4x16` flavor, you might run 10 pods per core that use no more than 75% of the worker node total capacity. |
| Worker node flavors | Worker nodes are available in [select flavors](/docs/openshift?topic=openshift-planning_worker_nodes#shared_dedicated_node) of compute resources. |
| Worker node host access | For security, you cannot SSH into the worker node compute host. |
| Worker node instances | You can have 900 worker nodes per cluster. If you plan to exceed 900 per cluster, contact the Red Hat OpenShift on IBM Cloud team in the [internal](https://ibm-argonauts.slack.com/messages/C4S4NUCB1){: external} or [external Slack](https://ibm-container-service.slack.com){: external} first. If you see an IBM Cloud infrastructure capacity limit on the number of instances per data center or that are ordered each month, contact your IBM Cloud infrastructure representative. |
{: summary="This table contains information on compute limitations for classic clusters. Columns are read from left to right. In the first column is the type of limitation and in the second column is the description of the limitation."}
{: caption="Classic cluster compute limitations"}

### Networking
{: #classic_networking_limit}

</br>

| Category | Description |
| -------- | ----------- |
| Ingress ALBs | <ul><li>The Ingress application load balancer (ALB) can process 32,768 connections per second. </li><li>HTTP2 is not supported.</li></ul> |
| Network load balancers (NLB)| <ul><li>You cannot create version 2.0 network load balancers (NLB 2.0) to expose your apps.</li><li>You cannot create subdomains for private NLBs.</li><li>You can register up to 128 subdomains. This limit can be lifted on request by opening a [support case](/docs/get-support?topic=get-support-getting-customer-support).</li></ul> | 
| Private VLANs only | Private network load balancers (NLBs) cannot be registered with the domain name server (DNS), so the cluster cannot be created with only a private network interface. At least some of the cluster's worker nodes must have both public and private VLANs. You can still create a private service to expose your apps on only the private network. |
| Service endpoints | When you create a cluster, you must enable the public service endpoint, and can optionally enable the private service endpoint. If no public service endpoint for the cluster exists, a subdomain for the router is not generated. | 
| strongSwan VPN service | See [strongSwan VPN service considerations](/docs/openshift?topic=openshift-vpn#strongswan_limitations). |
| Service IP addresses | You can have 65,000 IPs per cluster in the 172.21.0.0/16 range that you can assign to Kubernetes services within the cluster. |
| Subnets per VLAN | Each VLAN has a limit of 40 subnets. |
{: summary="This table contains information on networking limitations for classic clusters. Columns are read from left to right. In the first column is the type of limitation and in the second column is the description of the limitation."}
{: caption="Classic cluster networking limitations"}

### Storage
{: #classic_storage_limit}

</br>

| Category | Description |
| -------- | ----------- |
| Volume instances | You can have a total of 250 IBM Cloud infrastructure file and block storage volumes per account. If you mount more than this amount, you might see an "out of capacity" message when you provision persistent volumes and need to contact your IBM Cloud infrastructure representative. For more FAQs, see the [file](/docs/FileStorage?topic=FileStorage-file-storage-faqs#how-many-volumes-can-i-provision-) and [block](/docs/BlockStorage?topic=BlockStorage-block-storage-faqs#how-many-instances-can-share-the-use-of-a-block-storage-volume-) storage docs. |
| File storage | Because of the way that {{site.data.keyword.cloud_notm}} NFS file storage configures Linux user permissions, you might encounter errors when you use file storage. If so, you might need to configure [OpenShift Security Context Constraints](https://docs.openshift.com/container-platform/3.11/admin_guide/manage_scc.html){: external} or use a different storage type. |
{: summary="This table contains information on storage limitations for classic clusters. Columns are read from left to right. In the first column is the type of limitation and in the second column is the description of the limitation."}
{: caption="Classic cluster storage limitations"}

<br />




