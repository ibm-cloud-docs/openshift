---

copyright:
  years: 2014, 2020
lastupdated: "2020-04-15"

keywords: openshift, roks, rhoks, rhos, compliance, security standards

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


# Service architecture and dependencies
{: #service-arch}

Review sample architectures, components, and dependencies for your {{site.data.keyword.openshiftlong}} clusters.
{: shortdesc}

## Service architecture
{: #service-architecture}


For more information about the OpenShift Container Platform architecture, see the [OpenShift docs](https://docs.openshift.com/container-platform/4.3/architecture/architecture.html){: external}.
{: note}

![Red Hat OpenShift on IBM Cloud cluster architecture](/images/cs_org_ov_both_ses_roks.png)

Scroll through the following table for more information about the cluster master and worker node components.

| Master components| Description |
|:-----------------|:-----------------|
| Single tenancy | The master and all master components are dedicated only to you, and are not shared with other IBM customers. |
| Replicas | Master components, including the OpenShift Kubernetes API server and etcd data store have three replicas and, if located in a multizone metro, are spread across zones for even higher availability. The master components are backed up every 8 hours.|
| `openshift-api` | The OpenShift Kubernetes API server serves as the main entry point for all cluster management requests from the worker node to the master. The API server validates and processes requests that change the state of Kubernetes resources, such as pods or services, and stores this state in the etcd data store.|
| `openvpn-server` | The OpenVPN server works with the OpenVPN client to securely connect the master to the worker node. This connection supports `apiserver proxy` calls to your pods and services, and `oc exec`, `attach`, and `logs` calls to the kubelet.|
| `etcd` | etcd is a highly available key value store that stores the state of all Kubernetes resources of a cluster, such as services, deployments, and pods. Data in etcd is backed up to an encrypted storage instance that IBM manages.|
| `openshift-controller` | The OpenShift controller manager watches for newly created pods and decides where to deploy them based on capacity, performance needs, policy constraints, anti-affinity specifications, and workload requirements. If no worker node can be found that matches the requirements, the pod is not deployed in the cluster. The controller also watches the state of cluster resources, such as replica sets. When the state of a resource changes, for example if a pod in a replica set goes down, the controller manager initiates correcting actions to achieve the required state. The `openshift-controller` functions as both the scheduler and controller manager in a community Kubernetes configuration. |
| `cloud-controller-manager` | The cloud controller manager manages cloud provider-specific components such as the {{site.data.keyword.cloud_notm}} load balancer.|
| Admission controllers | Admission controllers are implemented for specific features in OpenShift and {{site.data.keyword.containerlong_notm}}. With admission controllers, you can set up policies in your cluster that determine whether a particular action in the cluster is allowed or not. In the policy, you can specify conditions when a user cannot perform an action, even if this action is part of the general permissions that you assigned the user by using RBAC. Therefore, admission controllers can provide an extra layer of security for your cluster before an API request is processed by the Kubernetes API server. </br></br> When you create an OpenShift cluster, {{site.data.keyword.containerlong_notm}} automatically installs the following [Kubernetes admission controllers](https://kubernetes.io/docs/reference/access-authn-authz/admission-controllers/){: external} in the given order in the Kubernetes master, which cannot be changed by the user:<ul><li>`NamespaceLifecycle`</li><li>`LimitRanger`</li><li>`ServiceAccount`</li><li>`DefaultStorageClass`</li><li>`ResourceQuota`</li><li>`StorageObjectInUseProtection`</li><li>`PersistentVolumeClaimResize`</li><li>[`Priority`](/docs/openshift?topic=openshift-pod_priority)</li><li>`BuildByStrategy`</li><li>`OriginPodNodeEnvironment`</li><li>`PodNodeSelector`</li><li>`ExternalIPRanger`</li><li>`NodeRestriction`</li><li>`SecurityContextConstraint`</li><li>`SCCExecRestrictions`</li><li>`PersistentVolumeLabel`</li><li>`OwnerReferencesPermissionEnforcement`</li><li>`PodTolerationRestriction`</li><li>`openshift.io/JenkinsBootstrapper`</li><li>`openshift.io/BuildConfigSecretInjector`</li><li>`openshift.io/ImageLimitRange`</li><li>`openshift.io/RestrictedEndpointsAdmission`</li><li>`openshift.io/ImagePolicy`</li><li>`openshift.io/IngressAdmission`</li><li>`openshift.io/ClusterResourceQuota`</li><li>`MutatingAdmissionWebhook`</li><li>`ValidatingAdmissionWebhook`</li></ul></br><p>You can [install your own admission controllers in the cluster](https://kubernetes.io/docs/reference/access-authn-authz/extensible-admission-controllers/#admission-webhooks){: external} or choose from the optional admission controllers that {{site.data.keyword.containerlong_notm}} provides.</p><ul><li><strong>[Container image security enforcer](/docs/Registry?topic=registry-security_enforce#security_enforce):</strong> Use this admission controller to enforce Vulnerability Advisor policies in your cluster to block deployments from vulnerable images.</li></ul></br><p class="note">If you manually installed admission controllers and you do not want to use them anymore, make sure to remove them entirely. If admission controllers are not entirely removed, they might block all actions that you want to perform on the cluster.</p>
{: caption="Table 1. OpenShift master components." caption-side="top"}
{: #roks-components-1}
{: tab-title="Master"}
{: tab-group="roks-components"}
{: class="simple-tab-table"}

| Worker node components| Description |
|:-----------------|:-----------------|
| Single tenancy | The worker nodes and all worker node components are dedicated only to you, and are not shared with other IBM customers. However, if you use worker node virtual machines, the underlying hardware might be shared with other IBM customers depending on the [level of hardware isolation](/docs/openshift?topic=openshift-planning_worker_nodes#vm) that you choose. |
| Operating System | Red Hat OpenShift on IBM Cloud worker nodes run on the Red Hat Enterprise Linux 7 operating system. |
| Projects | OpenShift organizes your resources into projects, which are Kubernetes namespaces with annotations, and includes many more components than community Kubernetes clusters to run OpenShift features such as the catalog. Select components of projects are described in the following rows. For more information, see [Working with projects](https://docs.openshift.com/container-platform/4.3/applications/projects/working-with-projects.html){: external}.|
| `kube-system` | This namespace includes many components that are used to run Kubernetes on the worker node.<ul><li>**`ibm-master-proxy`**: The `ibm-master-proxy` is a daemon set that forwards requests from the worker node to the IP addresses of the highly available master replicas. In single zone clusters, the master has three replicas on separate hosts. For clusters that are in a multizone-capable zone, the master has three replicas that are spread across zones. A highly available load balancer forwards requests to the master domain name to the master replicas.</li><li>**`openvpn-client`**: The OpenVPN client works with the OpenVPN server to securely connect the master to the worker node. This connection supports `apiserver proxy` calls to your pods and services, and `oc exec`, `attach`, and `logs` calls to the kubelet.</li><li>**`kubelet`**: The kubelet is a worker node agent that runs on every worker node and is responsible for monitoring the health of pods that run on the worker node and for watching the events that the Kubernetes API server sends. Based on the events, the kubelet creates or removes pods, ensures liveness and readiness probes, and reports back the status of the pods to the Kubernetes API server.</li><li>**`calico`**: Calico manages network policies for your cluster, and includes a few components to manage container network connectivity, IP address assignment, and network traffic control.</li><li>**Other components**: The `kube-system` namespace also includes components to manage IBM-provided resources such as storage plug-ins for file and block storage, ingress application load balancer (ALB), `fluentd` logging, and `keepalived`.</li></ul>|
| `ibm-system` | This namespace includes the `ibm-cloud-provider-ip` deployment that works with `keepalived` to provide health checking and Layer 4 load balancing for requests to app pods.|
| `kube-proxy-and-dns`| This namespace includes the components to validate incoming network traffic against the `iptables` rules that are set up on the worker node, and proxies requests that are allowed to enter or leave the cluster.|
| `default` | This namespace is used if you do not specify a namespace or create a project for your Kubernetes resources. In addition, the default namespace includes the following components to support your OpenShift clusters.<ul><li>**`router`**: OpenShift uses [routes](https://docs.openshift.com/container-platform/4.3/networking/routes/route-configuration.html){: external} to expose an app's service on a hostname so that external clients can reach the service. The router maps the service to the hostname. By default, the router includes two replicas. Make sure that your cluster has at least two worker nodes so that the router can run on separate compute hosts for higher availability.</li><li>**Version 4.3: `image-registry` and `image-registry-operator`. Version 3.11: `docker-registry`** and **`registry-console`.**: OpenShift provides an internal [container image registry](https://docs.openshift.com/container-platform/4.3/registry/architecture-component-imageregistry.html){: external} that you can use to locally manage and view images through the console. Alternatively, you can set up the private {{site.data.keyword.registrylong_notm}}. The internal registry comes with a classic {{site.data.keyword.cloud_notm}} File Storage volume in your IBM Cloud infrastructure account to [store the registry images](/docs/openshift?topic=openshift-registry#storage_internal_registry) that is provisioned through the `registry-backing` persistent volume claim (PVC).</li></ul>|
| Other projects | Other components are installed in various namespaces by default to enable functionality such as logging, monitoring, and the OpenShift console.<ul><li><code>ibm-cert-store</code></li><li><code>kube-public</code></li><li><code>kube-service-catalog</code></li><li><code>openshift</code></li><li><code>openshift-ansible-service-broker</code></li><li><code>openshift-console</code></li><li><code>openshift-infra</code></li><li><code>openshift-monitoring</code></li><li><code>openshift-node</code></li><li><code>openshift-template-service-broker</code></li><li><code>openshift-web-console</code></li></ul>|
{: caption="Table 2. OpenShift worker node components." caption-side="top"}
{: #roks-components-2}
{: tab-title="Worker nodes"}
{: tab-group="roks-components"}
{: class="simple-tab-table"}



## Overview of personal and sensitive data storage and removal options
{: #ibm-data}

Review what information is stored with IBM when you use Red Hat OpenShift on IBM Cloud, how this data is stored and encrypted, and how you can permanently remove this information.
{: shortdesc}

### What information is stored with IBM when using Red Hat OpenShift on IBM Cloud?
{: #pi-info}

For each cluster that you create with Red Hat OpenShift on IBM Cloud cluster, IBM stores the information that is described in the following table: 

|Information type|Data|
|-------|----------|
|Personal information|The email address of the {{site.data.keyword.cloud_notm}} account that created the cluster.|
|Sensitive information|<ul><li>The TLS certificate and secret that is used for the assigned Ingress subdomain. </li><li>The Certificate Authority that is used for the TLS certificate. </li><li>The Certificate Authority, private keys, and TLS certificates for the OpenShift master components, including the OpenShift API server, etcd data store, and VPN.</li><li>A customer root key in {{site.data.keyword.keymanagementservicelong_notm}} for each {{site.data.keyword.cloud_notm}} account that is used to encrypt personal and sensitive information.</li></ul>|


### How is my information stored and encrypted?
{: #pi-storage}

All information is stored in an etcd database and backed up every 8 hours to {{site.data.keyword.cos_full_notm}}. The etcd database and {{site.data.keyword.cos_short}} service instance are owned and managed by the {{site.data.keyword.cloud_notm}} SRE team. For each {{site.data.keyword.cloud_notm}} account, a customer root key in {{site.data.keyword.keymanagementservicelong_notm}} is created that is managed by the Red Hat OpenShift on IBM Cloud service team. This root key is used to encrypt all personal and sensitive information in etcd and in {{site.data.keyword.cos_short}}.

### Where is my information stored?
{: #pi-location}

The location where your information is stored depends on the location your cluster is in. By default, your data is stored in the Red Hat OpenShift on IBM Cloud multizone metro area that is closest to your cluster. However, Red Hat OpenShift on IBM Cloud might decide to store your data in a different multizone metro area to optimize the utilization of available compute resources. If you create your cluster in a non-multizone metro area, your data is still stored in the closest multizone metro area. This location might be in a different country than the one where you created your cluster. Make sure that your information can reside in a different country before you create your cluster in a non-multizone metro area. 

The data that you create and own is always stored in the same location as the cluster. For more information about what data you can create in your cluster, how this data is encrypted, and how you can protect this data, see [Protecting sensitive information in your cluster](/docs/containers?topic=containers-encryption).
{: note}

### How can I remove my information?
{: #pi-removal}

Review your options to remove your information from Red Hat OpenShift on IBM Cloud.
{: shortdesc}

Removing personal and sensitive information is permanent and nonreversible. Make sure that you want to permanently remove your information before you proceed.
{: important}

**Is my data removed when I remove the cluster?**</br>
Deleting a cluster does not remove all information from Red Hat OpenShift on IBM Cloud. When you delete a cluster, cluster-specific information is removed from the etcd instance that is managed by IBM. However, your information still exists in the {{site.data.keyword.cos_full_notm}} backup and can still be accessed by the IBM service team by using the account-specific customer root key in {{site.data.keyword.keymanagementservicelong_notm}} that IBM owns and manages. 

**What options do I have to permanently remove my data?**</br>
To remove that data that IBM stores, choose between the following options. Note that removing your personal and sensitive information requires all of your clusters to be deleted as well. Make sure that you backed up your app data before your proceed.

- **Open an {{site.data.keyword.cloud_notm}} support case**: Contact IBM Support to remove your personal and sensitive information from Red Hat OpenShift on IBM Cloud. For more information, see [Getting support](/docs/get-support?topic=get-support-getting-customer-support).
- **End your {{site.data.keyword.cloud_notm}} subscription**: After you end your {{site.data.keyword.cloud_notm}} subscription, Red Hat OpenShift on IBM Cloud removes the customer root key in {{site.data.keyword.keymanagementservicelong_notm}} that IBM created and managed for you as well as all the personal and sensitive information from the etcd data store and {{site.data.keyword.cos_short}} backup. 

{: important}





## Dependencies to other {{site.data.keyword.cloud_notm}} services
{: #dependencies-ibmcloud}

Review the {{site.data.keyword.cloud_notm}} services that Red Hat OpenShift on IBM Cloud connects to over the public network. 
{: shortdesc}


| Service name | Description| 
| -----------|-------------------------------| 
| Business Support Services for {{site.data.keyword.cloud_notm}} (BSS) | The `BSS` component is used to access information about the {{site.data.keyword.cloud_notm}} account, service subscription, service usage, and billing. | 
|{{site.data.keyword.cloudcerts_short}}|This service is used to retrieve the TLS certificates for custom Ingress domains that {{site.data.keyword.containerlong_notm}} users set up.|
| Global Search and Tagging (Ghost) | The `Ghost` component is used to look up information about other {{site.data.keyword.cloud_notm}} services, such as IDs, tags, or service attributes. |
| Hypersync and hyperwarp | This {{site.data.keyword.cloud_notm}} component is used to provide information about clusters so that the cluster is visible to other {{site.data.keyword.cloud_notm}} services and cluster information can be searched and displayed. |
|{{site.data.keyword.cloud_notm}} Command Line (CLI)|When Red Hat OpenShift on IBM Cloud runs CLI commands, the service connects to the service API endpoint over the public service endpoint.|
|{{site.data.keyword.registrylong_notm}}|This service is used to store the container images that Red Hat OpenShift on IBM Cloud uses to run the service.|
| {{site.data.keyword.la_full_notm}} | Red Hat OpenShift on IBM Cloud sends service logs to {{site.data.keyword.la_full_notm}}. These logs are monitored and analyzed by the service team to detect service issues and malicious activities. You can also use {{site.data.keyword.la_full_notm}} to manage your own pod container logs. To use {{site.data.keyword.la_full_notm}}, you must deploy a logging agent to every worker node in your cluster. This agent collects pod logs from all namespaces, including `kube-system`, and forwards the logs to {{site.data.keyword.la_full_notm}}. To get started, see [Setting up LogDNA and Sysdig add-ons to monitor cluster health](/docs/openshift?topic=openshift-health#openshift_logdna_sysdig).  |
| {{site.data.keyword.mon_full_notm}} | Red Hat OpenShift on IBM Cloud sends service metrics to {{site.data.keyword.mon_full_notm}}. These metrics are monitored by the service team to identify capacity and performance issues of the service. You can also use {{site.data.keyword.mon_full_notm}} to gain operational visibility into the performance and health of your apps. For more information, see [Setting up LogDNA and Sysdig add-ons to monitor cluster health](/docs/openshift?topic=openshift-health#openshift_logdna_sysdig).|
| {{site.data.keyword.cloudaccesstraillong_notm}} | Red Hat OpenShift on IBM Cloud integrates with {{site.data.keyword.at_full_notm}} to forward cluster audit events to the {{site.data.keyword.at_full_notm}} service instance that is set up and owned by the Red Hat OpenShift on IBM Cloud user. For more information, see [{{site.data.keyword.cloudaccesstraillong_notm}} events](/docs/containers?topic=containers-at_events).|
| IBMid profile service | The IBMid component is used to look up the IBMid from an email address. The IBMid is used to authenticate with {{site.data.keyword.cloud_notm}} via Identity and Access Management (IAM). |
| Identity and Access Management (IAM) | To authenticate requests to the service and authorize user actions, Red Hat OpenShift on IBM Cloud implements platform and service access roles in Identity and Access Management (IAM). For more information about required IAM permissions to work with the service, see [Assigning cluster access](/docs/containers?topic=containers-users). |
| Infrastructure Management System (IMS) | The Infrastructure Management System (IMS) component is used to provision, manage, and show information about classic infrastructure resources of the cluster, such as worker nodes, VLANs or subnets. |
| {{site.data.keyword.keymanagementservicelong_notm}} | To protect your cluster resources and data, Red Hat OpenShift on IBM Cloud. uses {{site.data.keyword.keymanagementservicelong_notm}} root keys to encrypt data in etcd, secrets, and on the worker node drive. For additional encryption, you can enable {{site.data.keyword.keymanagementserviceshort}} as a key management system provider in your cluster. For more information about how data is encrypted, see [Overview of cluster encryption](/docs/containers?topic=containers-encryption#encrypt_ov). | 
|{{site.data.keyword.cos_short}} (COS)|This service is used to store customer logs for all cluster master operations, such as `deploy`, `patch`, `update`, or `delete`, and to back up cluster metrics. Access to this service instance is protected by IAM policies and available to the Red Hat OpenShift on IBM Cloud service team only to detect malicious activity. All data is encrypted in transit and at rest.|
| User Account & Authentication (UAA) | This service is used to provide OAuth authentication for Cloud Foundry services. | 

## Dependencies to 3rd party services
{: #dependencies-3rd-party}

Review the list of 3rd party services that Red Hat OpenShift on IBM Cloud connects to over the public network. 
{: shortdesc}

| Service name | Description| 
| -----------|-------------------------------| 
| Akamai, Cloudflare | Akamai and Cloudflare are used as the primary providers for DNS, global load balancing, and web firewall capabilities in Red Hat OpenShift on IBM Cloud. |
| Github Enterprise | GitHub Enterprise is used to track service enhancements, features, and customer issues. When a customer issue is identified, the cluster ID, worker node IDs, the flavor of the worker nodes, and the zone where the worker nodes are deployed to are documented. This information is then shared with the service team to start troubleshooting the issue. | 
| Launch Darkly | To manage the roll out of new features in Red Hat OpenShift on IBM Cloud, Launch Darkly feature flags are used. A feature flag controls the visibility and availability of a feature to a selected user base. | 
| Let's Encrypt | This service is used as the Certificate authority to generate SSL certificates for customer owned public endpoints. All generated certificates are managed in {{site.data.keyword.cloudcerts_short}}.|
| Razee | [Razee](https://razee.io/){: external} is an open-source project that was developed by IBM to automate and manage the deployment of Kubernetes resources, versions, features, and security patches across Red Hat OpenShift on IBM Cloud environments, and to visualize deployment information. Razee integrates with Launch Darkly to control the visibility of these features to the Red Hat OpenShift on IBM Cloud use base. You can also use Razee to manage the rollout of your own deployments across multiple clusters. For more information, see the [Razee documentation](https://github.com/razee-io/Razee){: external}.   |
| Slack | Slack is used as the IBM-internal communication medium to troubleshoot cluster issues and bring together internal SMEs to resolve customer issues. Diagnostic information about clusters are sent to a private Slack channel and include the customer account ID, cluster ID, and details about the worker nodes. |

