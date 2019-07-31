---

copyright:
  years: 2014, 2019
lastupdated: "2019-07-31"

keywords: openshift, roks, rhoks, rhos, compliance, security standards

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
{:download: .download}
{:preview: .preview}



# Service architecture
{: #openshift-service-arch}

The following diagram and table describe the default components that are set up in a {{site.data.keyword.openshiftlong}} architecture.
{: shortdesc}

For more information about the OpenShift Container Platform architecture, see the [OpenShift docs ![External link icon](../icons/launch-glyph.svg "External link icon")](https://docs.openshift.com/container-platform/3.11/architecture/index.html).
{: note}

![Red Hat OpenShift on IBM Cloud cluster architecture](/images/cs_org_ov_both_ses_rhos.png)

Scroll through the following table for more information about the cluster master and worker node components.

| Master components| Description |
|:-----------------|:-----------------|
| Replicas | Master components, including the OpenShift Kubernetes API server and etcd data store have three replicas and, if located in a multizone metro, are spread across zones for even higher availability. The master components are backed up every 8 hours.|
| `rhos-api` | The OpenShift Kubernetes API server serves as the main entry point for all cluster management requests from the worker node to the master. The API server validates and processes requests that change the state of Kubernetes resources, such as pods or services, and stores this state in the etcd data store.|
| `openvpn-server` | The OpenVPN server works with the OpenVPN client to securely connect the master to the worker node. This connection supports `apiserver proxy` calls to your pods and services, and `oc exec`, `attach`, and `logs` calls to the kubelet.|
| `etcd` | etcd is a highly available key value store that stores the state of all Kubernetes resources of a cluster, such as services, deployments, and pods. Data in etcd is backed up to an encrypted storage instance that IBM manages.|
| `rhos-controller` | The OpenShift controller manager watches for newly created pods and decides where to deploy them based on capacity, performance needs, policy constraints, anti-affinity specifications, and workload requirements. If no worker node can be found that matches the requirements, the pod is not deployed in the cluster. The controller also watches the state of cluster resources, such as replica sets. When the state of a resource changes, for example if a pod in a replica set goes down, the controller manager initiates correcting actions to achieve the required state. The `rhos-controller` functions as both the scheduler and controller manager in a community Kubernetes configuration. |
| `cloud-controller-manager` | The cloud controller manager manages cloud provider-specific components such as the {{site.data.keyword.cloud_notm}} load balancer.|
| Admission controllers | Admission controllers are implemented for specific features in OpenShift and {{site.data.keyword.containerlong_notm}}. With admission controllers, you can set up policies in your cluster that determine whether a particular action in the cluster is allowed or not. In the policy, you can specify conditions when a user cannot perform an action, even if this action is part of the general permissions that you assigned the user by using RBAC. Therefore, admission controllers can provide an extra layer of security for your cluster before an API request is processed by the Kubernetes API server. </br></br> When you create an OpenShift cluster, {{site.data.keyword.containerlong_notm}} automatically installs the following [Kubernetes admission controllers ![External link icon](../icons/launch-glyph.svg "External link icon")](https://kubernetes.io/docs/admin/admission-controllers/) in the given order in the Kubernetes master, which cannot be changed by the user:<ul><li>`NamespaceLifecycle`</li><li>`LimitRanger`</li><li>`ServiceAccount`</li><li>`DefaultStorageClass`</li><li>`ResourceQuota`</li><li>`StorageObjectInUseProtection`</li><li>`PersistentVolumeClaimResize`</li><li>[`Priority`](/docs/containers?topic=containers-pod_priority#pod_priority)</li><li>`BuildByStrategy`</li><li>`OriginPodNodeEnvironment`</li><li>`PodNodeSelector`</li><li>`ExternalIPRanger`</li><li>`NodeRestriction`</li><li>`SecurityContextConstraint`</li><li>`SCCExecRestrictions`</li><li>`PersistentVolumeLabel`</li><li>`OwnerReferencesPermissionEnforcement`</li><li>`PodTolerationRestriction`</li><li>`openshift.io/JenkinsBootstrapper`</li><li>`openshift.io/BuildConfigSecretInjector`</li><li>`openshift.io/ImageLimitRange`</li><li>`openshift.io/RestrictedEndpointsAdmission`</li><li>`openshift.io/ImagePolicy`</li><li>`openshift.io/IngressAdmission`</li><li>`openshift.io/ClusterResourceQuota`</li><li>`MutatingAdmissionWebhook`</li><li>`ValidatingAdmissionWebhook`</li></ul></br><p>You can [install your own admission controllers in the cluster ![External link icon](../icons/launch-glyph.svg "External link icon")](https://kubernetes.io/docs/reference/access-authn-authz/extensible-admission-controllers/#admission-webhooks) or choose from the optional admission controllers that {{site.data.keyword.containerlong_notm}} provides.</p><ul><li><strong>[Container image security enforcer](/docs/services/Registry?topic=registry-security_enforce#security_enforce):</strong> Use this admission controller to enforce Vulnerability Advisor policies in your cluster to block deployments from vulnerable images.</li></ul></br><p class="note">If you manually installed admission controllers and you do not want to use them anymore, make sure to remove them entirely. If admission controllers are not entirely removed, they might block all actions that you want to perform on the cluster.</p>
{: caption="Table 1. OpenShift master components." caption-side="top"}
{: #rhos-components-1}
{: tab-title="Master"}
{: tab-group="rhos-components"}
{: class="simple-tab-table"}

| Worker node components| Description |
|:-----------------|:-----------------|
| Operating System | Red Hat OpenShift on IBM Cloud worker nodes run on the Red Hat Enterprise Linux 7 operating system. |
| Projects | OpenShift organizes your resources into projects, which are Kubernetes namespaces with annotations, and includes many more components than community Kubernetes clusters to run OpenShift features such as the catalog. Select components of projects are described in the following rows. For more information, see [Projects and users ![External link icon](../icons/launch-glyph.svg "External link icon")](https://docs.openshift.com/container-platform/3.11/architecture/core_concepts/projects_and_users.html).|
| `kube-system` | This namespace includes many components that are used to run Kubernetes on the worker node.<ul><li>**`ibm-master-proxy`**: The `ibm-master-proxy` is a daemon set that forwards requests from the worker node to the IP addresses of the highly available master replicas. In single zone clusters, the master has three replicas on separate hosts. For clusters that are in a multizone-capable zone, the master has three replicas that are spread across zones. A highly available load balancer forwards requests to the master domain name to the master replicas.</li><li>**`openvpn-client`**: The OpenVPN client works with the OpenVPN server to securely connect the master to the worker node. This connection supports `apiserver proxy` calls to your pods and services, and `oc exec`, `attach`, and `logs` calls to the kubelet.</li><li>**`kubelet`**: The kubelet is a worker node agent that runs on every worker node and is responsible for monitoring the health of pods that run on the worker node and for watching the events that the Kubernetes API server sends. Based on the events, the kubelet creates or removes pods, ensures liveness and readiness probes, and reports back the status of the pods to the Kubernetes API server.</li><li>**`calico`**: Calico manages network policies for your cluster, and includes a few components to manage container network connectivity, IP address assignment, and network traffic control.</li><li>**Other components**: The `kube-system` namespace also includes components to manage IBM-provided resources such as storage plug-ins for file and block storage, ingress application load balancer (ALB), `fluentd` logging, and `keepalived`.</li></ul>|
| `ibm-system` | This namespace includes the `ibm-cloud-provider-ip` deployment that works with `keepalived` to provide health checking and Layer 4 load balancing for requests to app pods.|
| `kube-proxy-and-dns`| This namespace includes the components to validate incoming network traffic against the `iptables` rules that are set up on the worker node, and proxies requests that are allowed to enter or leave the cluster.|
| `default` | This namespace is used if you do not specify a namespace or create a project for your Kubernetes resources. In addition, the default namespace includes the following components to support your OpenShift clusters.<ul><li>**`router`**: OpenShift uses [routes ![External link icon](../icons/launch-glyph.svg "External link icon")](https://docs.openshift.com/container-platform/3.11/architecture/networking/routes.html) to expose an app's service on a host name so that external clients can reach the service. The router maps the service to the host name.</li><li>**`docker-registry`** and **`registry-console`**: OpenShift provides an internal [container image registry ![External link icon](../icons/launch-glyph.svg "External link icon")](https://docs.openshift.com/container-platform/3.11/install_config/registry/index.html) that you can use to locally manage and view images through the console. Alternatively, you can set up the private {{site.data.keyword.registrylong_notm}}.</li></ul>|
| Other projects | Other components are installed in various namespaces by default to enable functionality such as logging, monitoring, and the OpenShift console.<ul><li><code>ibm-cert-store</code></li><li><code>kube-public</code></li><li><code>kube-service-catalog</code></li><li><code>openshift</code></li><li><code>openshift-ansible-service-broker</code></li><li><code>openshift-console</code></li><li><code>openshift-infra</code></li><li><code>openshift-monitoring</code></li><li><code>openshift-node</code></li><li><code>openshift-template-service-broker</code></li><li><code>openshift-web-console</code></li></ul>|
{: caption="Table 2. OpenShift worker node components." caption-side="top"}
{: #rhos-components-2}
{: tab-title="Worker nodes"}
{: tab-group="rhos-components"}
{: class="simple-tab-table"}
