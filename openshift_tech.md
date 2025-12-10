---

copyright:
  years: 2014, 2025
lastupdated: "2025-12-10"


keywords: openshift, compliance, security standards, red hat openshift, openshift container platform, red hat, openshift architecture, red hat architecture, openshift dependencies,

subcollection: openshift

---


{{site.data.keyword.attribute-definition-list}}




# Architecture and dependencies of the service
{: #service-architecture}

Review sample architectures, components, and dependencies for your {{site.data.keyword.openshiftlong}} clusters.
{: shortdesc}

In {{site.data.keyword.openshiftlong_notm}}, your clusters comprise an IBM-managed master that secures components such as the API server and etcd, and customer-managed worker nodes that you configure to run you app workloads, as well as {{site.data.keyword.redhat_openshift_notm}}-provided default components. The default components within the cluster, such as the {{site.data.keyword.redhat_openshift_notm}} web console or OperatorHub, vary with the {{site.data.keyword.redhat_openshift_notm}} version of your cluster.
{: shortdesc}

## Classic {{site.data.keyword.redhat_openshift_notm}} architecture
{: #service-architecture-4}

Review the architecture diagram and then scroll through the following tables for a description of master and worker node components in {{site.data.keyword.openshiftlong_notm}} clusters that run on classic infrastructure. For more information about the OpenShift Container Platform architecture, see the [{{site.data.keyword.redhat_openshift_notm}} docs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.19/html/architecture/architecture){: external}.
{: shortdesc}

When you run `oc get nodes`, you might notice that the **ROLES** of your worker nodes are marked as both `master,worker`. These nodes are worker nodes in {{site.data.keyword.cloud_notm}}, and don't include the master components that are managed by IBM. Instead, these nodes are marked as `master` because they run OpenShift Container Platform components that are required to set up and manage default resources within the cluster, such as the OperatorHub and internal registry.
{: note}

![{{site.data.keyword.openshiftlong_notm}} cluster architecture](/images/cs_org_ov_both_ses_roks4.svg){: caption="Red Hat OpenShift master components" caption-side="bottom"}

### {{site.data.keyword.redhat_openshift_notm}} master components
{: #service-architecture-4-master}

Review the following components in the IBM-managed master of your {{site.data.keyword.openshiftlong_notm}} cluster.
{: shortdesc}

You can't modify these components. IBM manages the components and automatically updates them during master patch updates.

In OpenShift Container Platform 4, many components are configured by a corresponding operator for ease of management. The following table discusses these operators and components together, to focus on the main functionality the component provides to the cluster.


Single tenancy
:  The master and all master components are dedicated only to you, and are not shared with other IBM customers.

Replicas
:   Master components, including the {{site.data.keyword.redhat_openshift_notm}} API server and etcd data store have three replicas and, if located in a multizone metro, are spread across zones for even higher availability.

`cloud-controller-manager`
:   The cloud controller manager manages cloud provider-specific components such as the {{site.data.keyword.cloud_notm}} load balancer.

`cluster-health`
:   The cluster health component monitors the health of the cluster and integrates with {{site.data.keyword.cloud_notm}} monitoring and metrics for the service.

`cluster-policy-controller`
:   The [`cluster-policy-controller`](https://github.com/openshift/cluster-policy-controller){: external} maintains policy resources that are required to create pods within the cluster.

`cluster-version-operator`
:   The cluster version operator (CVO) installs and updates other operators that run in the cluster. For more information, see the [GitHub project](https://github.com/openshift/cluster-version-operator){: external}.

`control-plane-operator`
:   The control plane operator manages the installation and update of control plane components in the master.

`etcd`, `etcd-molecule`, `etcd-operator`
:   etcd is a highly available key value store that stores the state of all Kubernetes resources of a cluster, such as services, deployments, and pods. Data in etcd is backed up every 8 hours to an encrypted storage instance that IBM manages.

`kube-controller-manager`, `openshift-controller-manager`
:   The [Kubernetes controller](https://github.com/openshift/cluster-kube-controller-manager-operator){: external} watches the state of objects within the cluster, such as the replica set of a workload. When the state of an object changes, for example if a pod in a replica set goes down, the controller manager initiates correcting actions to achieve the required state. The {{site.data.keyword.redhat_openshift_notm}} controller performs the same function for objects that are specific to the {{site.data.keyword.redhat_openshift_notm}} API, such as projects.

`kube-scheduler`
:   The [Kubernetes scheduler](https://github.com/openshift/cluster-kube-scheduler-operator){: external} watches for newly created pods and decides where to deploy them based on capacity, performance needs, policy constraints, anti-affinity specifications, and workload requirements. If no worker node can be found that matches the requirements, the pod is not deployed in the cluster.

`manifests-bootstrapper`
:   The `manifests-boot-strapper` job sets up the master with the required certificates to join as the master node of the cluster.

`oauth-openshift`
:   The built-in OAuth server is automatically set up to integrate with {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM). You can't add other supported identity providers to the cluster. For more information about how to authenticate with the cluster via IAM, see [Accessing {{site.data.keyword.redhat_openshift_notm}} clusters](/docs/openshift?topic=openshift-access_cluster).

`openshift-apiserver`, `openshift-apiserver-operator`, `kube-apiserver`
:   The API server is the main entry point for all cluster management requests from the worker node to the master. The API server validates and processes requests that change the state of Kubernetes objects, such as pods or services, and {{site.data.keyword.redhat_openshift_notm}} objects, such as projects or users. Then, the API server stores this state in the etcd data store.

`konnectivity-server`, `konnectivity-operator`
:   The Konnectivity server works with the Konnectivity agent to securely connect the master to the worker node. This connection supports `apiserver proxy` calls to your pods and services; `oc exec`, `attach`, and `logs` calls to the kubelet; and mutating and validating webhooks.

Admission controllers
:   Admission controllers are implemented for specific features in {{site.data.keyword.openshiftlong_notm}} clusters. With admission controllers, you can set up policies in your cluster that determine whether a particular action in the cluster is allowed or not. In the policy, you can specify conditions when a user can't perform an action, even if this action is part of the general permissions that you assigned the user by using RBAC. Therefore, admission controllers can provide an extra layer of security for your cluster before an API request is processed by the {{site.data.keyword.redhat_openshift_notm}} API server. When you create a {{site.data.keyword.redhat_openshift_notm}} cluster, the following [Kubernetes admission controllers](https://kubernetes.io/docs/reference/access-authn-authz/admission-controllers/){: external} are automatically installed in the given order in the {{site.data.keyword.redhat_openshift_notm}} master, which can't be changed by the user:
    - `NamespaceLifecycle`
    - `LimitRanger`
    - `ServiceAccount`
    - `DefaultStorageClass`
    - `ResourceQuota`
    - `StorageObjectInUseProtection`
    - `PersistentVolumeClaimResize`
    - `Priority`
    - `BuildByStrategy`
    - `OriginPodNodeEnvironment`
    - `PodNodeSelector`
    - `ExternalIPRanger`
    - `NodeRestriction`
    - `SecurityContextConstraint`
    - `SCCExecRestrictions`
    - `PersistentVolumeLabel`
    - `OwnerReferencesPermissionEnforcement`
    - `PodTolerationRestriction`
    - `openshift.io/JenkinsBootstrapper`
    - `openshift.io/BuildConfigSecretInjector`
    - `openshift.io/ImageLimitRange`
    - `openshift.io/RestrictedEndpointsAdmission`
    - `openshift.io/ImagePolicy`
    - `openshift.io/IngressAdmission`
    - `openshift.io/ClusterResourceQuota`
    - `MutatingAdmissionWebhook`
    - `ValidatingAdmissionWebhook`

:   You can [install your own admission controllers in the cluster](https://kubernetes.io/docs/reference/access-authn-authz/extensible-admission-controllers/#admission-webhooks){: external} or choose from the optional admission controllers that {{site.data.keyword.openshiftlong_notm}} provides. Container image security enforcement: Install [Portieris](/docs/openshift?topic=openshift-images#portieris-image-sec) to block container deployments from unsigned images.
:   If you manually installed admission controllers and you don't want to use them anymore, make sure to remove them entirely. If admission controllers aren't entirely removed, they might block all actions that you want to perform on the cluster.</p>


### {{site.data.keyword.redhat_openshift_notm}} worker node components
{: #service-architecture-4-workers}

Review the following components in the customer-managed worker nodes of your {{site.data.keyword.openshiftlong_notm}} cluster.
{: shortdesc}

These components run on your worker nodes because you are able to use them with the workloads that you deploy to your cluster. For example, your apps might use an operator from the OperatorHub that runs a container from an image in the internal registry. You are responsible for your usage of these components, but IBM provides updates for them in the worker node patch updates that you choose to apply.

In OpenShift Container Platform, many components are configured by a corresponding operator for ease of management. The following table discusses these operators and components together, to focus on the main functionality the component provides to the cluster.


Single tenancy
:   The worker nodes and all worker node components are dedicated only to you, and are not shared with other IBM customers. However, if you use worker node virtual machines, the underlying hardware might be shared with other IBM customers depending on the level of hardware isolation that you choose.

Operating System
:   For a list of supported operating systems by cluster version, see the [Version information](/docs/openshift?topic=openshift-openshift_versions).

CRI-O container runtime
:   Your worker nodes are installed with [CRI-O](https://cri-o.io/){: external} as the container runtime interface. For more information, see [Container runtime](/docs/openshift?topic=openshift-security#container-runtime).

Projects
:   {{site.data.keyword.redhat_openshift_notm}} organizes your resources into projects, which are Kubernetes namespaces with annotations, and includes many more components than community Kubernetes clusters to run {{site.data.keyword.redhat_openshift_notm}} features such as the catalog. Select components of projects are described in the following rows. For more information, see [Working on a project](https://docs.redhat.com/en/documentation/openshift_container_platform/4.19/html/building_applications/building-applications-overview#working-on-a-project){: external}.

`calico-system`, `tigera-operator`
:   Calico manages network policies for your cluster, and includes a few components to manage container network connectivity, IP address assignment, and network traffic control. The Tigera operator installs and manages the lifecycle of Calico components.

`default`
:   This project is used if you don't specify a project or create a project for your Kubernetes resources.

`ibm-system`
:   This project includes the `ibm-cloud-provider-ip` deployment that works with `keepalived` to provide health checking and Layer 4 load balancing for requests to app pods.

`kube-system`
:   This project includes many components that are used to run Kubernetes on the worker node.
    - `ibm-master-proxy`: The `ibm-master-proxy` is a daemon set that forwards requests from the worker node to the IP addresses of the highly available master replicas. In single zone clusters, the master has three replicas on separate hosts. For clusters that are in a multizone-capable zone, the master has three replicas that are spread across zones. A highly available load balancer forwards requests to the master domain name to the master replicas.
    - `kubelet`: The kubelet is a worker node agent that runs on every worker node and is responsible for monitoring the health of pods that run on the worker node and for watching the events that the API server sends. Based on the events, the kubelet creates or removes pods, ensures liveness and readiness probes, and reports back the status of the pods to the API server.
    - `vpn`: The Konnectivity agent works with the Konnectivity server to securely connect the master to the worker node. This connection supports `apiserver proxy` calls to your pods and services, and `oc exec`, `attach`, and `logs` calls to the kubelet.
    - Other components: The `kube-system` project also includes components to manage IBM-provided resources such as storage plug-ins for file and block storage, ingress application load balancer (ALB), and `keepalived`.

`openshift-cloud-credential-operator`
:   The cloud credential operator manages a controller for {{site.data.keyword.redhat_openshift_notm}} components that request cloud provider credentials. The controller ensures that only the credentials that are required for the operation are used, and not any elevated permissions like `admin`. For more information, see the [GitHub project](https://github.com/openshift/cloud-credential-operator){: external}.

`openshift-cluster-node-tuning-operator`
:   IBM manages the [node tuning operator](https://docs.redhat.com/en/documentation/openshift_container_platform/4.19/html/scalability_and_performance/using-node-tuning-operator){: external}, which runs a daemon set on each worker node in the cluster to tune worker nodes.

`openshift-cluster-samples-operator`
:   The [samples operator](https://docs.redhat.com/en/documentation/openshift_container_platform/4.19/html/images/configuring-samples-operator){: external} manages select image streams and templates that come with the {{site.data.keyword.redhat_openshift_notm}} cluster by default. You can deploy these templates from the [**Developer** perspective in the {{site.data.keyword.redhat_openshift_notm}} web console](/docs/openshift?topic=openshift-deploy_app).

`openshift-cluster-storage-operator`
:   The cluster storage operator makes sure that a default storage class is set.

`openshift-console`, `openshift-console-operator`
:   The {{site.data.keyword.redhat_openshift_notm}} web console is a web-based interface that you can use to manage the {{site.data.keyword.redhat_openshift_notm}} and Kubernetes resources that run in your cluster. You can also use the console to display an `oc login` token to authenticate to your cluster from a CLI. For more information, see [Navigating the {{site.data.keyword.redhat_openshift_notm}} console](/docs/openshift?topic=openshift-openshift_tutorial#openshift_oc_console).

`openshift-dns`, `openshift-dns-operator`
:   The DNS project includes the components to validate incoming network traffic against the `iptables` rules that are set up on the worker node, and proxies requests that are allowed to enter or leave the cluster.

`openshift-image-registry`
:   {{site.data.keyword.redhat_openshift_notm}} provides an internal [container image registry](https://docs.redhat.com/en/documentation/openshift_container_platform/4.19/html/registry/registry-overview){: external} that you can use to locally manage and view images through the console. Alternatively, you can [set up the private {{site.data.keyword.registrylong_notm}}](/docs/openshift?topic=openshift-registry#openshift_iccr) or [import images from {{site.data.keyword.registrylong_notm}} to the internal registry](/docs/openshift?topic=openshift-registry#imagestream_registry). The internal registry comes with a {{site.data.keyword.filestorage_short}} volume in your IBM Cloud infrastructure account to [store the registry images](/docs/openshift?topic=openshift-registry#openshift_internal_registry). The file storage volume is provisioned through the `image-registry-storage` persistent volume claim (PVC).

`openshift-ingress`, `openshift-ingress-operator`
:   {{site.data.keyword.redhat_openshift_notm}} uses [routes](https://docs.redhat.com/en/documentation/openshift_container_platform/4.19/html/ingress_and_load_balancing/routes){: external} to directly expose an app's service on a hostname so that external clients can reach the service. To create routes, the cluster uses the Ingress operator. You can also use [Ingress](/docs/openshift?topic=openshift-ingress-about-roks4) to expose apps externally and customize routing. Ingress consists of three components: the Ingress operator, Ingress controller, and Route resources. The Ingress controller maps the service to the hostname. By default, the Ingress controller includes two replicas. Make sure that your cluster has at least two worker nodes so that the Ingress controller can run on separate compute hosts for higher availability.

`openshift-marketplace`
:   The marketplace includes the [OperatorHub](https://docs.redhat.com/en/documentation/openshift_container_platform/4.19/html/operators/understanding-operators#olm-understanding-operatorhub){: external} that comes with the {{site.data.keyword.redhat_openshift_notm}} cluster by default. The OperatorHub includes operators from Red Hat and 3rd-party providers. Keep in mind that these operators are provided by the community, might not integrate with your cluster, and are not supported by IBM. You can [enable operators](/docs/openshift?topic=openshift-operators) from the OperatorHub in {{site.data.keyword.redhat_openshift_notm}} web console.

`openshift-monitoring`
:   OpenShift Container Platform includes a [built-in monitoring stack](https://docs.redhat.com/en/documentation/openshift_container_platform/4.19/html/monitoring/about-openshift-container-platform-monitoring){: external} for your cluster, that includes metrics and alert managing capabilities. For a comparison of the built-in monitoring stack and other options such as {{site.data.keyword.mon_full_notm}}, see [Understanding options for logging and monitoring](/docs/openshift?topic=openshift-health).

`openshift-multus`
:   OpenShift Container Platform uses the Multus container network interface (CNI) plug-in to allow [multiple pod networks](https://docs.redhat.com/en/documentation/openshift_container_platform/4.19/html/multiple_networks/understanding-multiple-networks){: external}. However, you can't configure the cluster to use multiple pod networks. {{site.data.keyword.openshiftlong_notm}} clusters support only Calico, which is set up for your cluster by default. If enabled, [Service Mesh](https://docs.redhat.com/en/documentation/openshift_container_platform/4.19/html/service_mesh/service-mesh-1-x){: external} uses the Multus plug-in.

`openshift-network-operator`
:   The [cluster network operator (CNO)](https://docs.redhat.com/en/documentation/openshift_container_platform/4.19/html/networking_operators/cluster-network-operator){: external} manages the cluster network components that are set up by default, such as the CNI pod network provider plug-in and DNS operator.

`openshift-operator-lifecycle-manager`
:   The [operator lifecycle manager (OLM)](https://docs.redhat.com/en/documentation/openshift_container_platform/4.19/html/operators/understanding-operators#operator-lifecycle-manager-olm){: external} manages the lifecycle of all operators and the catalog that run in the cluster, including the operators for the default components and any custom operators that you add.

`openshift-service-ca`, `openshift-service-ca-operator`
:   The certificate authority (CA) operator runs certificate signing and injects certificates into API server resources and configmaps in the cluster. For more information, see the [GitHub project](https://github.com/openshift/service-ca-operator){: external}.






## VPC cluster service architecture
{: #service-architecture_vpc}

The following architectural overviews are specific to the VPC infrastructure provider. For an architectural overview for the classic infrastructure provider, see [Classic cluster service architecture](#service-architecture).
{: note}

Review the architecture diagrams and then scroll through the following table for a description of master and worker node components in {{site.data.keyword.openshiftlong_notm}} clusters that run on virtual private cloud (VPC) compute infrastructure.
{: shortdesc}

### Cluster with public and private cloud service endpoints
{: #vpc-service-arch-public-and-private}

The following diagram shows the components of your cluster and how they interact when both the [public and private cloud service endpoints are enabled](/docs/openshift?topic=openshift-plan_vpc_basics#vpc-workeruser-master). Because both service endpoints are enabled, your VPC creates a public load balancer for each service for inbound traffic.

![{{site.data.keyword.openshiftlong_notm}} on VPC cluster architecture with public and private cloud service endpoints](/images/arch_roks_vpc.svg){: caption="Red Hat OpenShift on VPC cluster architecture with public and private cloud service endpoints" caption-side="bottom"}

### Cluster with private cloud service endpoint only
{: #vpc-service-arch-private-only}

The following diagram shows the components of your cluster and how they interact when only the [private cloud service endpoint is enabled](/docs/openshift?topic=openshift-plan_vpc_basics#vpc-workeruser-master). Because only the private cloud service endpoint is enabled, your VPC creates a private load balancer for each service for inbound traffic.

![{{site.data.keyword.openshiftlong_notm}} on VPC cluster architecture with the private cloud service endpoint only](images/arch_roks_vpc_private.svg){: caption="Red Hat OpenShift on VPC cluster architecture with the private cloud service endpoint only" caption-side="bottom"}



### VPC master and worker node components
{: #service-arch-vpc-4}

[Masters](#service-architecture-4-master) and [worker nodes](#service-architecture-4-workers) include the same components as described in the Classic cluster architecture for clusters. For more information about the OpenShift Container Platform architecture, see the [{{site.data.keyword.redhat_openshift_notm}} docs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.19/html/architecture/architecture){: external}.


Master
:   [Master components](#service-architecture-4-master), including the API server and etcd, have three replicas and are spread across zones for even higher availability. Masters include the same components as described in the Classic cluster architecture for clusters. The master and all the master components are dedicated only to you, and are not shared with other IBM customers.

Worker node
:   With {{site.data.keyword.openshiftlong_notm}}, the virtual machines that your cluster manages are instances that are called worker nodes. These worker nodes virtual machines and all the worker node components are dedicated to you only and are not shared with other IBM customers. However, the underlying hardware is shared with other IBM customers. You manage the worker nodes through the automation tools that are provided by {{site.data.keyword.openshiftlong_notm}}, such as the API, CLI, or console. Unlike classic clusters, you don't see VPC compute worker nodes in your infrastructure portal or separate infrastructure bill, but instead manage all maintenance and billing activity for the worker nodes from {{site.data.keyword.openshiftlong_notm}}.
:   Worker nodes include the same [components](#service-architecture-4-workers) as described in the Classic cluster architecture.
:   When you run `oc get nodes`, you might notice that the **ROLES** of your worker nodes are marked as both `master,worker`. These nodes are worker nodes in {{site.data.keyword.cloud_notm}}, and don't include the master components that are managed by IBM. Instead, these nodes are marked as `master` because they run OpenShift Container Platform components that are required to set up and manage default resources within the cluster, such as the OperatorHub and internal registry.

Cluster networking
:   Your worker nodes are created in a VPC subnet in the zone that you specify. Communication between the master and worker nodes is over the private network. If you create a cluster with the public and private cloud service endpoints enabled, authenticated external users can communicate with the master over the public network, such as to run `oc` commands. If you create a cluster with only the private cloud service endpoints enabled, authenticated external users can communicate with the master over the private network only. You can set up your cluster to communicate with resources in on-premises networks, other VPCs, or classic infrastructure by setting up a VPC VPN, {{site.data.keyword.dl_full_notm}}, or {{site.data.keyword.tg_full_notm}} on the private network.

App networking
:   Virtual Private Cloud load balancers are automatically created in your VPC outside the cluster for any networking services that you create in your cluster. For example, a VPC load balancer exposes the router services in your cluster by default. Or, you can create a Kubernetes `LoadBalancer` service for your apps, and a VPC load balancer is automatically generated. VPC load balancers are multizone and route requests for your app through the private node ports that are automatically opened on your worker nodes. If the public and private cloud service endpoints are enabled, the routers and VPC load balancers are created as public by default. If only the private cloud service endpoint is enabled, the routers and VPC load balancers are created as private by default. For more information, see [Public](/docs/openshift?topic=openshift-cs_network_planning#pattern_public_vpc) or [Private app networking for VPC clusters](/docs/openshift?topic=openshift-cs_network_planning#private_vpc). Calico is used as the cluster networking policy fabric.

Storage
:   You can set up {{site.data.keyword.cos_full_notm}} and {{site.data.keyword.databases-for}} only.
