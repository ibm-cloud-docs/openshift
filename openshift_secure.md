---

copyright:
  years: 2014, 2020
lastupdated: "2020-07-16"

keywords: openshift, roks, rhoks, rhos, vpc

subcollection: openshift

---

{:beta: .beta}
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



# Security for Red Hat OpenShift on IBM Cloud
{: #security}

You can use built-in security features in {{site.data.keyword.openshiftlong}} for risk analysis and security protection. These features help you to protect your cluster infrastructure and network communication, isolate your compute resources, and ensure security compliance across your infrastructure components and container deployments.
{: shortdesc}

## Overview of security threats for your cluster
{: #threats}

To protect your cluster from being compromised, you must understand potential security threats for your cluster and what you can do to reduce the exposure to vulnerabilities.
{: shortdesc}

<img src="images/cs_security_threats.png" width="400" alt="Security threats for your cluster" style="width:400px; border-style: none"/>

Cloud security and the protection of your systems, infrastructure, and data against attacks became very important over the last couple of years as companies continue to move their workloads into the public cloud. A cluster consists of several components that each can put your environment at risk for malicious attacks. To protect your cluster against these security threats, you must make sure that you apply the latest Red Hat OpenShift on IBM Cloud, OpenShift, and Kubernetes security features and updates in all cluster components.

These components include:
- [OpenShift API server and etcd data store](#apiserver)
- [Worker nodes](#workernodes)
- [Network](#network)
- [Persistent storage](#storage)
- [Monitoring and Logging](#monitoring_logging)
- [Container images and registry](#images_registry)
- [Container isolation and security](#container)
- [Personal information](#pi)

<br />



##OpenShift API server and etcd
{: #apiserver}

The OpenShift API server and etcd data store are the most sensitive components that run in your OpenShift master. If an unauthorized user or system gets access to your OpenShift API server, the user or system can change settings, manipulate, or take control of your cluster, which puts your cluster at risk for malicious attacks.
{: shortdesc}

To protect your OpenShift API server and etcd data store, you must secure and limit the access to your OpenShift API server for both human users and Kubernetes service accounts.

**How is access to my OpenShift API server granted?**

By default, Kubernetes requires every request to go through several stages before access to the API server is granted:

<ol><li><strong>Authentication: </strong>Validates the identity of a registered user or service account.</li><li><strong>Authorization: </strong>Limits the permissions of authenticated users and service accounts to ensure that they can access and operate only the cluster components that you want them to.</li><li><strong>Admission control: </strong>Validates or mutates requests before they are processed by the OpenShift API server. Many Kubernetes features require admission controllers in order to properly function.</li></ol>

**What does Red Hat OpenShift on IBM Cloud do to secure my OpenShift API server and etcd data store?** </br>
The following image shows the default cluster security settings that address authentication, authorization, admission control, and secure connectivity between the Kubernetes master and worker nodes.


<img src="images/oc_security_apiserver_access.png" width="600" alt="Security stages when accessing the Kubernetes API server" style="width:600px; border-style: none"/>

<table>
<caption>OpenShift API server and etcd security</caption>
  <thead>
  <th>Security feature</th>
  <th>Description</th>
  </thead>
  <tbody>
    <tr>
      <td>Fully managed and dedicated OpenShift master</td>
      <td>Every cluster in Red Hat OpenShift on IBM Cloud is controlled by a dedicated OpenShift master that is managed by IBM in an IBM-owned {{site.data.keyword.cloud_notm}} account. The OpenShift master is set up with the following dedicated components that are not shared with other IBM customers.
        <ul><li><strong>etcd data store:</strong> Stores all Kubernetes resources of a cluster, such as `Services`, `Deployments`, and `Pods`. Kubernetes `ConfigMaps` and `Secrets` are app data that is stored as key value pairs so that they can be used by an app that runs in a pod. Data in etcd is stored on the local disk of the OpenShift master and is backed up to {{site.data.keyword.cos_full_notm}}. Data is encrypted during transit to {{site.data.keyword.cos_full_notm}} and at rest. You can choose to enable encryption for your etcd data on the local disk of your OpenShift master by [enabling {{site.data.keyword.keymanagementservicelong_notm}} encryption](/docs/openshift?topic=openshift-encryption#keyprotect) for your cluster. When etcd data is sent to a pod, data is encrypted via TLS to ensure data protection and integrity.</li>
          <li><strong>openshift-api:</strong> Serves as the main entry point for all cluster management requests from the worker node to the OpenShift master. The API server validates and processes requests that change the state of cluster resources, such as pods or services, and stores this state in the etcd data store.</li>
          
          <li><strong>openshift-controller:</strong> Watches for newly created pods and decides where to deploy them based on capacity, performance needs, policy constraints, anti-affinity specifications, and workload requirements. If no worker node can be found that matches the requirements, the pod is not deployed in the cluster. The controller also watches the state of cluster resources, such as replica sets. When the state of a resource changes, for example if a pod in a replica set goes down, the controller manager initiates correcting actions to achieve the required state. </li>
            <li><strong>cloud-controller-manager:</strong> The cloud controller manager manages cloud provider-specific components such as the {{site.data.keyword.cloud_notm}} load balancer. </li>
          <li><strong>OpenVPN:</strong> Red Hat OpenShift on IBM Cloud-specific component to provide secured network connectivity for all OpenShift master to worker node communication. The OpenVPN server works with the OpenVPN client to securely connect the master to the worker node. This connection supports <code>apiserver proxy</code> requests to your pods and services, and <code>oc</code> <code>exec</code>, <code>attach</code>, and <code>logs</code> requests to the kubelet. The connection from the worker nodes to the master is automatically secured with TLS certificates.  </li></ul></td>
    </tr>
    <tr>
    <td>Continuous monitoring by IBM Site Reliability Engineers (SREs)</td>
    <td>The OpenShift master, including all the master components, compute, networking, and storage resources are continuously monitored by IBM Site Reliability Engineers (SREs). The SREs apply the latest security standards, detect and remediate malicious activities, and work to ensure reliability and availability of Red Hat OpenShift on IBM Cloud. </td>
    </tr>
    <tr>
      <td>CIS Kubernetes master benchmark</td>
      <td>To configure Red Hat OpenShift on IBM Cloud, IBM engineers follow relevant cybersecurity practices from the Kubernetes master benchmark that is published by the [Center of Internet Security (CIS) ![External link icon](../icons/launch-glyph.svg "External link icon")](https://www.cisecurity.org/benchmark/kubernetes/). The cluster master and all worker nodes are deployed with images that meet the benchmark.</td>
    </tr>
    <tr>
      <td>Secure communication via TLS</td>
      <td>To use Red Hat OpenShift on IBM Cloud, you must authenticate with the service by using your credentials. When you are authenticated, Red Hat OpenShift on IBM Cloud generates TLS certificates that encrypt the communication to and from the OpenShift API server and etcd data store to ensure a secure end-to-end communication between the worker nodes and the OpenShift master. These certificates are never shared across clusters or across OpenShift master components. </td>
    </tr>
    <tr>
      <td>OpenVPN connectivity to worker nodes</td>
      <td>Although Kubernetes secures the communication between the master and worker nodes by using the <code>https</code> protocol, no authentication is provided on the worker node by default. To secure this communication, Red Hat OpenShift on IBM Cloud automatically sets up an OpenVPN connection between the OpenShift master and the worker node when the cluster is created.</td>
    </tr>
    <tr>
      <td>Fine-grained access control</td>
      <td>As the account administrator you can [grant access to other users for Red Hat OpenShift on IBM Cloud](/docs/openshift?topic=openshift-users#users) by using {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM). {{site.data.keyword.cloud_notm}} IAM provides secure authentication with the {{site.data.keyword.cloud_notm}} platform, Red Hat OpenShift on IBM Cloud, and all the resources in your account. Setting up proper user roles and permissions is key to limit who can access your resources and to limit the damage that a user can do when legitimate permissions are misused. </br></br>You can select from the following pre-defined user roles that determine the set of actions that the user can perform: <ul><li><strong>Platform roles:</strong> Determine the cluster and worker node management-related actions that a user can perform in Red Hat OpenShift on IBM Cloud. Platform roles also assign users the `basic-users` and `self-provisioners` RBAC role. With these RBAC roles, you can create an OpenShift project in the cluster, in which you can deploy apps and other Kubernetes resources. As the creator of the project, you are automatically assigned the `admin` RBAC role for the project so that you can fully control what you want to deploy and run in your project. However, these RBAC roles do not grant access to other OpenShift projects. To view and access other OpenShift projects, you must be assigned the appropriate service access role in IAM.  </li><li><strong>Service access roles:</strong> Determine the [Kubernetes RBAC role](https://kubernetes.io/docs/reference/access-authn-authz/rbac/) that is assigned to the user and the actions that a user can run against the OpenShift API server. While the <code>basic-users</code> and <code>self-provisioners</code> RBAC role that is assigned with a platform role lets you create and manage your own OpenShift projects, you cannot view, access, or work with other OpenShift projects until you are assigned a service access role. For more information about the corresponding RBAC roles that are assigned to a user and associated permissions, see [{{site.data.keyword.cloud_notm}} IAM service roles](/docs/openshift?topic=openshift-access_reference#service). </li><li><strong>Classic infrastructure:</strong> Enables access to your classic {{site.data.keyword.cloud_notm}} infrastructure resources. Example actions that are permitted by classic infrastructure roles are viewing the details of cluster worker node machines or editing networking and storage resources.</li>
  <li><strong>VPC infrastructure:</strong> Enables access to VPC infrastructure resources. Example actions that are permitted by VPC infrastructure roles are creating a VPC, adding subnets, changing floating IP addresses, and creating VPC Block Storage instances. </li></ul> </br> For more information about access control in a cluster, see [Assigning cluster access](/docs/openshift?topic=openshift-users).</td>
    </tr>
    <tr>
      <td>Admission controllers</td>  
      <td>Admission controllers are implemented for specific features in Kubernetes and Red Hat OpenShift on IBM Cloud. With admission controllers, you can set up policies in your cluster that determine whether a particular action in the cluster is allowed or not. In the policy, you can specify conditions when a user cannot perform an action, even if this action is part of the general permissions that you assigned the user by using RBAC roles. Therefore, admission controllers can provide an extra layer of security for your cluster before an API request is processed by the OpenShift API server. </br></br> When you create a cluster, Red Hat OpenShift on IBM Cloud automatically installs the following [Kubernetes admission controllers ![External link icon](../icons/launch-glyph.svg "External link icon")](https://kubernetes.io/docs/reference/access-authn-authz/admission-controllers/) in the given order in the OpenShift master, which cannot be changed by the user: <ul><li>`NamespaceLifecycle`</li><li>`LimitRanger`</li>
      <li>`ServiceAccount`</li>
      <li>`DefaultStorageClass`</li>
      <li>`ResourceQuota`</li>
      <li>`StorageObjectInUseProtection`</li>
      <li>`PersistentVolumeClaimResize`</li>
      <li>`Priority`</li>
      <li>`BuildByStrategy`</li>
      <li>`OriginPodNodeEnvironment`</li>
      <li>`PodNodeSelector`</li>
      <li>`ExternalIPRanger`</li>
      <li>`NodeRestriction`</li>
      <li>`SecurityContextConstraint`</li>
      <li>`SCCExecRestrictions`</li>
      <li>`PersistentVolumeLabel`</li>
      <li>`OwnerReferencesPermissionEnforcement`</li>
      <li>`PodTolerationRestriction`</li>
      <li>`openshift.io/JenkinsBootstrapper`</li>
      <li>`openshift.io/BuildConfigSecretInjector`</li>
      <li>`openshift.io/ImageLimitRange`</li>
      <li>`openshift.io/RestrictedEndpointsAdmission`</li>
      <li>`openshift.io/ImagePolicy`</li>
      <li>`openshift.io/IngressAdmission`</li>
      <li>`openshift.io/ClusterResourceQuota`</li>
      <li>`MutatingAdmissionWebhook`</li>
      <li>`ValidatingAdmissionWebhook`</li></ul>
</br>
      You can [install your own admission controllers in the cluster ![External link icon](../icons/launch-glyph.svg "External link icon")](https://kubernetes.io/docs/reference/access-authn-authz/extensible-admission-controllers/#admission-webhooks) or choose from the optional admission controllers that Red Hat OpenShift on IBM Cloud provides: <ul><li><strong>[Container image security enforcer](/docs/Registry?topic=Registry-security_enforce#security_enforce):</strong> Use this admission controller to enforce Vulnerability Advisor policies in your cluster to block deployments from vulnerable images.</li></ul></br><p class="note">If you manually installed admission controllers and you do not want to use them anymore, make sure to remove them entirely. If admission controllers are not entirely removed, they might block all actions that you want to perform on the cluster.</p></td>
    </tr>
  </tbody>
</table>

**What else can I do to secure my OpenShift API server?**</br>
You can decide how you want your master and worker nodes to communicate and how your cluster users can access the OpenShift API server by enabling the private service endpoint only, the public service endpoint only, or the public and private service endpoints.

Note that your options for service endpoints vary based on your cluster's {[site.data.keyword.openshiftshort]} version and infrastructure provider. For more information about service endpoints, see worker-to-master and user-to-master communication in [classic clusters](/docs/openshift?topic=openshift-plan_clusters#workeruser-master) and [VPC clusters](/docs/openshift?topic=openshift-plan_clusters#vpc-workeruser-master).

<br />


## Worker node
{: #workernodes}

Worker nodes carry the deployments and services that make up your app. When you host workloads in the public cloud, you want to ensure that your app is protected from being accessed, changed, or monitored by an unauthorized user or software.
{: shortdesc}

**Who owns the worker node and am I responsible to secure it?** </br>
The ownership of a worker node depends on the type of cluster that you create and the infrastructure provider that you choose.


- **Standard classic clusters**: Worker nodes are provisioned in to your {{site.data.keyword.cloud_notm}} account. The worker nodes are dedicated to you and you are responsible to request timely updates to the worker nodes to ensure that the worker node OS and {{site.data.keyword.containerlong_notm}} components apply the latest security updates and patches.
- **Standard VPC clusters**: Worker nodes are provisioned in to an {{site.data.keyword.cloud_notm}} account that is owned by IBM to enable monitoring of malicious activities and apply security updates. You cannot access your worker nodes by using the VPC dashboard. However, you can manage your worker nodes by using the {{site.data.keyword.containerlong_notm}} console, CLI, or API. The virtual machines that make up your worker nodes are dedicated to you and you are responsible to request timely updates so that your worker node OS and {{site.data.keyword.containerlong_notm}} components apply the latest security updates and patches.

For more information, see [Your responsibilities by using Red Hat OpenShift on IBM Cloud](/docs/openshift?topic=openshift-responsibilities_iks).

Use the `ibmcloud oc worker update` [command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_update) regularly (such as monthly) to deploy updates and security patches to the operating system and to update the OpenShift version that your worker nodes run. When updates are available, you are notified when you view information about the master and worker nodes in the {{site.data.keyword.cloud_notm}} console or CLI, such as with the `ibmcloud oc clusters ls` or `ibmcloud oc workers ls --cluster <cluster_name>` commands. Worker node updates are provided by IBM as a full worker node image that includes the latest security patches. To apply the updates, the worker node must be reimaged and reloaded with the new image. Keys for the root user are automatically rotated when the worker node is reloaded.
{: important}

**How does my worker node setup look like?**</br>
The following image shows the components that are set up for every worker node to protect your worker node from malicious attacks.

The image does not include components that ensure secure end-to-end communication to and from the worker node. For more information, see [network security](#network).
{: note}


<img src="images/oc_worker_setup.png" width="600" alt="Worker node setup in Red Hat OpenShift on IBM Cloud (excluding network security)" style="width:600px; border-style: none"/>

<table>
<caption>Worker node security setup</caption>
  <thead>
  <th>Security feature</th>
  <th>Description</th>
  </thead>
  <tbody>
    <tr><td>CIS-compliant RHEL image</td><td>Every worker node is set up with an Red Hat Enterprise Linux (RHEL) operating system that implements the benchmarks that are published by the Center of Internet Security (CIS). The operating system cannot be changed by the user or the owner of the machine. To review the current RHEL version, run <code>oc get nodes -o wide</code>. IBM works with internal and external security advisory teams to address potential security compliance vulnerabilities. Security updates and patches for the operating system are made available through Red Hat OpenShift on IBM Cloud and must be installed by the user to keep the worker node secure.<p class="important">Red Hat OpenShift on IBM Cloud uses a Red Hat Enterprise Linux kernel for worker nodes. You can run containers based on any Linux distribution in Red Hat OpenShift on IBM Cloud. Check with your container image vendor to verify that your container images can be run on an Red Hat Enterprise kernel.</p></td></tr>
    <tr>
    <td>Continuous monitoring by Site Reliability Engineers (SREs) </td>
    <td>The image that is installed on your worker nodes is continuously monitored by IBM Site Reliability Engineers (SREs) to detect vulnerabilities and security compliance issues. To address vulnerabilities, SREs create security patches and fix packs for your worker nodes. Make sure to apply these patches when they are available to ensure a secure environment for your worker nodes and the apps that you run on top of them.</td>
    </tr>
    <tr>
      <td>CIS Kubernetes worker node benchmark</td>
      <td>To configure Red Hat OpenShift on IBM Cloud, IBM engineers follow relevant cybersecurity practices from the Kubernetes worker node benchmark that is published by the [Center of Internet Security (CIS) ![External link icon](../icons/launch-glyph.svg "External link icon")](https://www.cisecurity.org/benchmark/kubernetes/).</td>
    </tr>
    <tr>
  <td>Compute isolation</td>
  <td>Worker nodes are dedicated to a cluster and do not host workloads of other clusters. When you create a classic cluster, you can choose to provision your worker nodes as [physical machines (bare metal) or as virtual machines](/docs/openshift?topic=openshift-planning_worker_nodes#planning_worker_nodes) that run on shared or dedicated physical hardware. Worker nodes in in a standard VPC compute cluster can be provisioned as virtual machines on shared infrastructure only.</td>
</tr>
<tr>
  <td>Option to deploy bare metal on classic</td>
  <td>If you create a standard classic cluster, you can choose to provision your worker nodes on bare metal physical servers (instead of virtual server instances). With bare metal machines, you have additional control over the compute host, such as the memory or CPU. This setup eliminates the virtual machine hypervisor that allocates physical resources to virtual machines that run on the host. Instead, all of a bare metal machine's resources are dedicated exclusively to the worker, so you don't need to worry about "noisy neighbors" sharing resources or slowing down performance. Bare metal servers are dedicated to you, with all its resources available for cluster usage.</br></br><p class="note">Bare metal machines are not supported in VPC Gen 1 compute clusters.</p></td>
</tr>
<tr>
  <td id="encrypted_disk">Encrypted disks</td>
    <td>By default, every worker node is provisioned with two local SSD, AES 256-bit encrypted data partitions. The first partition contains the kernel image that is used to boot the worker node and is not encrypted. The second partition holds the container file system and is unlocked by using LUKS encryption keys. Each worker node in a cluster has its own unique LUKS encryption key, managed by Red Hat OpenShift on IBM Cloud. When you create a cluster or add a worker node to an existing cluster, the keys are pulled securely and then discarded after the encrypted disk is unlocked. <p class="note">Encryption can impact disk I/O performance. For workloads that require high-performance disk I/O, test a cluster with encryption both enabled and disabled to help you decide whether to turn off encryption.</p></td>
      </tr>
    <tr>
      <td>SELinux</td>
      <td>Every worker node is set up with security and access policies that are enforced by [Security-Enhanced Linux (SELinux)](https://www.redhat.com/en/topics/linux/what-is-selinux){: external} profiles that are loaded into the worker node during bootstrapping. SELinux profiles cannot be changed by the user or owner of the machine. </td>
    </tr>
    <tr>
      <td>SSH disabled</td>
      <td>By default, SSH access is disabled on the worker node to protect your cluster from malicious attacks. When SSH access is disabled, access to the cluster is forced via the OpenShift API server. The OpenShift API server requires every request to be checked against the policies that are set in the authentication, authorization, and admission control module before the request is executed in the cluster. </br></br>  If you have a standard cluster and you want to install more features on your worker node, you can choose between the add-ons that are provided by Red Hat OpenShift on IBM Cloud or use [Kubernetes daemon sets ![External link icon](../icons/launch-glyph.svg "External link icon")](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/) for everything that you want to run on every worker node. For any one-time action that you must execute, use [Kubernetes jobs ![External link icon](../icons/launch-glyph.svg "External link icon")](https://kubernetes.io/docs/concepts/workloads/controllers/jobs-run-to-completion/).</td>
    </tr>
  </tbody>
  </table>

<br />


## Network
{: #network}
The classic approach to protect a company's network is to set up a firewall and block any unwanted network traffic to your apps. While this is still true, research shows that many malicious attacks come from insiders or authorized users who misuse their assigned permissions.
{: shortdesc}

### Network segmentation and privacy
{: #network_segmentation}

To protect your network and limit the range of damage that a user can do when access to a network is granted, you must make sure that your workloads are as isolated as possible and that you limit the number of apps and worker nodes that are publicly exposed.
{: shortdesc}

**What network traffic is allowed for my cluster by default?**</br>
All containers are protected by [predefined Calico network policy settings](/docs/openshift?topic=openshift-network_policies#default_policy) that are configured on every worker node during cluster creation. By default, all outbound network traffic is allowed for all worker nodes. Inbound network traffic is blocked with the following exceptions:
- **NodePort**: The [Kubernetes NodePort range](https://kubernetes.io/docs/concepts/services-networking/service/#nodeport){: external} is opened by default so that you can expose apps with [NodePort services](/docs/openshift?topic=openshift-nodeport). To block inbound network traffic on NodePorts in your cluster, see [Controlling inbound traffic to NLB or NodePort services](/docs/openshift?topic=openshift-network_policies#block_ingress).
- **IBM monitoring ports**: By default, IBM opens a few ports on your cluster so that network traffic can be monitored by IBM and for IBM to automatically install security updates for the OpenShift master.
Access from the OpenShift master to the worker node's kubelet is secured by an OpenVPN tunnel. For more information, see the [Red Hat OpenShift on IBM Cloud architecture](/docs/openshift?topic=openshift-service-arch).

**What is network segmentation and how can I set it up for a cluster?** </br>
Network segmentation describes the approach to divide a network into multiple subnetworks. You can group apps and related data to be accessed by a specific group in your organization. Apps that run in one subnetwork cannot see or access apps in another subnetwork. Network segmentation also limits the access that is provided to an insider or third-party software and can limit the range of malicious activities.   

Red Hat OpenShift on IBM Cloud provides {{site.data.keyword.cloud_notm}} VLANs that ensure quality network performance and network isolation for worker nodes. A VLAN configures a group of worker nodes and pods as if they were attached to the same physical wire. VLANs are dedicated to your {{site.data.keyword.cloud_notm}} account and not shared across IBM customers. In classic clusters, if you have multiple VLANs for your cluster, multiple subnets on the same VLAN, or a multizone classic cluster, you must enable a [Virtual Router Function (VRF)](/docs/dl?topic=dl-overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud) for your IBM Cloud infrastructure account so your worker nodes can communicate with each other on the private network. To enable VRF, [contact your IBM Cloud infrastructure account representative](/docs/dl?topic=dl-overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud#benefits-of-moving-to-vrf). To check whether a VRF is already enabled, use the `ibmcloud account show` command. If you cannot or do not want to enable VRF, enable [VLAN spanning](/docs/vlans?topic=vlans-vlan-spanning#vlan-spanning). To perform this action, you need the **Network > Manage Network VLAN Spanning** [infrastructure permission](/docs/openshift?topic=openshift-users#infra_access), or you can request the account owner to enable it. To check whether VLAN spanning is already enabled, use the `ibmcloud oc vlan spanning get --region <region>` [command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_vlan_spanning_get).

When you enable VRF or VLAN spanning for your account, network segmentation is removed for your clusters.
{: important}

Review the following table to see your options for how to achieve network segmentation when you enable VRF or VLAN spanning for your account.

|Security feature|Description|
|-------|----------------------------------|
|Set up custom network policies with Calico|You can use the built-in Calico interface to [set up custom Calico network policies](/docs/openshift?topic=openshift-network_policies#network_policies) for your worker nodes. For example, you can allow or block network traffic on specific network interfaces, for specific pods, or services. To set up custom network policies, you must [install the <code>calicoctl</code> CLI](/docs/openshift?topic=openshift-network_policies#cli_install).|
|Support for {{site.data.keyword.cloud_notm}} network firewalls|Red Hat OpenShift on IBM Cloud is compatible with all [{{site.data.keyword.cloud_notm}} firewall offerings](https://www.ibm.com/cloud/network-security){: external}. For example, you can set up a firewall with custom network policies to provide dedicated network security for your standard cluster and to detect and remediate network intrusion. For example, you might choose to set up a [Virtual Router Appliance](/docs/virtual-router-appliance?topic=virtual-router-appliance-about-the-vra) to act as your firewall and block unwanted traffic. When you set up a firewall, [you must also open up the required ports and IP addresses](/docs/openshift?topic=openshift-firewall#firewall) for each region so that the master and the worker nodes can communicate.|
{: caption="Network segmentation options" caption-side="top"}

**What else can I do to reduce the surface for external attacks?**</br>
The more apps or worker nodes that you expose publicly, the more steps you must take to prevent external malicious attacks. Review the following table to find options for how to keep apps and worker nodes private.

|Security feature|Description|
|-------|----------------------------------|
|Limit the number of exposed apps|By default, your apps and services that run within the cluster are not reachable over the public internet. You can choose if you want to expose your apps to the public, or if you want your apps and services be reachable on the private network only. When you keep your apps and services private, you can leverage the built-in security features to assure secured communication between worker nodes and pods. To expose services and apps to the public internet, you can use OpenShift routes, or leverage the [NLB and Ingress ALB support](/docs/openshift?topic=openshift-cs_network_planning#openshift_routers) to securely make your services publicly available. Ensure that only necessary services are exposed, and revisit the list of exposed apps regularly to ensure that they are still valid. |
|Limit public internet connectivity with edge nodes|Every worker node is configured to accept app pods and associated load balancer or ingress pods. You can label worker nodes as [edge nodes](/docs/openshift?topic=openshift-edge#edge) to force load balancer pods to be deployed to these worker nodes only. In addition, you can [taint your worker nodes](/docs/openshift?topic=openshift-edge#edge_workloads) so that app pods cannot schedule onto the edge nodes. With edge nodes, you can isolate the networking workload on fewer worker nodes in your cluster and keep other worker nodes in the cluster private.|
{: caption="Private services and worker node options" caption-side="top"}

**What if I want to connect my cluster to an on-prem data center?**</br>
To connect your worker nodes and apps to an on-prem data center, you can configure a [VPN IPSec endpoint with a strongSwan service, a Virtual Router Appliance, or with a Fortigate Security Appliance](/docs/openshift?topic=openshift-vpn#vpn).

### Network segmentation and privacy for VPC clusters
{: #network_segmentation_vpc}

To protect your network and limit the range of damage that a user can do when access to a network is granted, you must make sure that your workloads are as isolated as possible and that you limit the number of apps and worker nodes that are publicly exposed.
{: shortdesc}

**What network traffic is allowed for my cluster by default?**</br>
By default, worker nodes are connected to [VPC subnets](/docs/openshift?topic=openshift-vpc-subnets) on the private network only and do not have a public network interface. All public ingress to and egress from your worker nodes is blocked.


To run default OpenShift components such as the web console or OperatorHub, you must attach a [public gateway](/docs/vpc?topic=vpc-about-networking-for-vpc#public-gateway-for-external-connectivity) to the VPC subnets that the worker nodes are deployed to. All egress is permitted for worker nodes on a subnet with an attached public gateway, but all ingress is still blocked.


If you deploy apps in your cluster that must receive traffic requests from the internet, you can [create a VPC load balancer](/docs/openshift?topic=openshift-vpc-lbaas) to expose your apps. To allow ingress network traffic to your apps, you must configure your VPC load balancer for the ingress network traffic that you want to receive.

**What is network segmentation and how can I set it up for a cluster?** </br>
Network segmentation describes the approach to divide a network into multiple subnetworks. You can group apps and related data to be accessed by a specific group in your organization. Apps that run in one subnetwork cannot see or access apps in another subnetwork. Network segmentation also limits the access that is provided to an insider or third-party software and can limit the range of malicious activities.  

Red Hat OpenShift on IBM Cloud provides {{site.data.keyword.vpc_short}} subnets that ensure quality network performance and network isolation for worker nodes. A VPC subnet consists of a specified private IP address range (CIDR block) and configures a group of worker nodes and pods as if they were attached to the same physical wire. VPC subnets are dedicated to your {{site.data.keyword.cloud_notm}} account and not shared across IBM customers.

VPC subnets provide a channel for connectivity among the worker nodes within the cluster. Any system that is connected to any of the private subnets in the same VPC can communicate with workers. For example, all subnets in one VPC can communicate through private layer 3 routing with a built-in VPC router. If your clusters do not need to communicate, you can achieve the best network segmentation by creating the clusters in separate VPCs. If you have multiple clusters that must communicate with each other, you can create the clusters in the same VPC. Although subnets within one VPC can be shared by multiple clusters in that VPC, you can achieve better network segmentation by using different subnets for clusters within one VPC.

To achieve further private network segmentation between VPC subnets for your account, you can set up custom network policies with VPC access control lists (ACLs). When you create a VPC, a default ACL is created in the format `allow-all-network-acl-<VPC_ID>` for the VPC. Any subnet that you create in the VPC is attached to this ACL by default. The ACL includes an inbound rule and an outbound rule that allow all traffic between your worker nodes on a subnet and any system on the subnets in the same VPC. If you want to specify which private network traffic is permitted to the worker nodes on your VPC subnets, you can create a custom ACL for each subnet in the VPC. For example, you can [create a set of ACL rules](/docs/openshift?topic=openshift-vpc-network-policy#acls) to block most inbound and outbound private network traffic of a cluster, while allowing communication that is necessary for the cluster to function.

**What else can I do to reduce the surface for external attacks?**</br>
The more apps or worker nodes that you expose publicly, the more steps you must take to prevent external malicious attacks. Review the following table to find options for how to keep apps and worker nodes private.

|Security feature|Description|
|-------|----------------------------------|
|Limit the number of exposed apps|By default, your apps and services that run within the cluster are not reachable over the public internet. You can choose if you want to expose your apps to the public, or if you want your apps and services be reachable on the private network only. When you keep your apps and services private, you can leverage the built-in security features to assure secured communication between worker nodes and pods. To expose services and apps to the public internet, you can leverage the [VPC load balancer and Ingress ALB support](/docs/containers?topic=containers-cs_network_planning#pattern_public_vpc) to securely make your services publicly available. Ensure that only necessary services are exposed, and revisit the list of exposed apps regularly to ensure that they are still valid. |
|Limit public network egress to one subnet with a public gateway|If pods on your worker nodes need to connect to a public external endpoint, you can attach a public gateway to the subnet that those worker nodes are on.|
{: caption="VPC network security options" caption-side="top"}

**What if I want to connect my cluster to other networks, like other VPCs, an on-prem data center, or IBM Cloud classic resources?**</br>
Depending on the network that you want to connect your worker nodes to, you can [choose a VPN solution](/docs/openshift?topic=openshift-vpc-vpnaas).

### Expose apps with routes
{: #expose-apps-with-routes}

If you want to allow incoming network traffic from the internet, you can expose your apps by using [routes](https://docs.openshift.com/container-platform/4.3/networking/routes/route-configuration.html){: external}.  
{: shortdesc}

Every OpenShift cluster is automatically set up with an OpenShift router that is assigned a unique domain name and secured with a TLS certificate. When you expose your app by using a route, your app is assigned a URL from the OpenShift router.

**How can I create secured routes and control TLS termination?** </br>
When you create a route for your app, you can decide to create a secured (HTTPS) or unsecured (HTTP) route. For secured routes, you can decide where you want to implement the TLS termination, such as at the router or at the pod. For more information, see [Exposing apps with routes](/docs/openshift?topic=openshift-openshift_routes).

### Expose apps with LoadBalancer and Ingress services
{: #network_lb_ingress}

You can use network load balancer (NLB) and Ingress application load balancer (ALB) networking services to connect your apps to the public internet or to external private networks. Review the following optional settings for NLBs and ALBs that you can use to meet back-end app security requirements or encrypt traffic as it moves through your cluster.
{: shortdesc}

**Can I use security groups to manage my cluster's network traffic?** </br>
Classic clusters: {{site.data.keyword.cloud_notm}} [security groups](/docs/security-groups?topic=security-groups-about-ibm-security-groups#about-ibm-security-groups) are applied to the network interface of a single virtual server to filter traffic at the hypervisor level. If you want to manage traffic for each worker node, you can use security groups. When you create a security group, you must allow the VRRP protocol, which Red Hat OpenShift on IBM Cloud uses to manage NLB IP addresses. To uniformly manage traffic for your cluster across all of your worker nodes, use [Calico and Kubernetes policies](/docs/openshift?topic=openshift-network_policies).

VPC clusters: Use [access control lists (ACLs) and Kubernetes network policies](/docs/openshift?topic=openshift-vpc-network-policy) to manage network traffic into and out of your cluster. When you create a VPC cluster, a default [VPC security group](/docs/vpc?topic=vpc-using-security-groups) is created automatically and applied to the network interface of your worker nodes to filter traffic at the hypervisor level. While the default security group in VPC Gen 1 allows all traffic to your worker nodes, the default security group in VPC Gen 2 clusters does not allow traffic to your worker nodes. You can make changes to the default security group, such as to allow incoming TCP traffic to ports `30000-32767` of your VPC Gen 2 worker nodes. However, because the worker nodes of your VPC cluster exist in a service account and are not listed in the VPC infrastructure dashboard, you cannot create more security groups and apply them to your individual worker nodes.



**How can I do TLS termination with LoadBalancer and Ingress services?** </br>
The Ingress service offers TLS termination at two points in the traffic flow:
* [Decrypt package upon arrival](/docs/openshift?topic=openshift-ingress#public_inside_2): By default, the Ingress ALB load balances HTTP network traffic to the apps in your cluster. To also load balance incoming HTTPS connections, you can configure the ALB to decrypt the network traffic and forward the decrypted request to the apps that are exposed in your cluster. If you use the IBM-provided Ingress subdomain, you can use the IBM-provided TLS certificate. If you use a custom domain, you can use your own TLS certificate to manage TLS termination.
* [Re-encrypt package before you forward it to upstream apps](/docs/openshift?topic=openshift-ingress_annotation#ssl-services): The ALB decrypts HTTPS requests before forwarding traffic to your apps. If you have apps that require HTTPS and need traffic to be encrypted before it is forwarded to those upstream apps, you can use the `ssl-services` annotation. If your upstream apps can handle TLS, you can optionally provide a certificate that is contained in a one-way or mutual-authentication TLS secret.

<br />


## Persistent storage
{: #storage}

Review supported options for encrypting and protecting your data on persistent storage in {{site.data.keyword.cloud_notm}}.
{: shortdesc}

By default, all {{site.data.keyword.cloud_notm}} storage solutions automatically encrypt your data at rest with an IBM-managed encryption key at no additional cost. For more information, see the following links.
- [Classic NFS File Storage](/docs/FileStorage?topic=FileStorage-mng-data#provisioning-storage-with-encryption)
- [Classic Block Storage](/docs/BlockStorage?topic=BlockStorage-mng-data#encryption-at-rest-for-snapshots-or-replicated-storage)
- [{{site.data.keyword.cos_full_notm}}](/docs/cloud-object-storage?topic=cloud-object-storage-encryption)


Depending on the type of storage that you choose, you can set up additional encryption with {{site.data.keyword.keymanagementservicelong_notm}} to protect your data in transit and at rest with your own encryption key.

- [{{site.data.keyword.cos_full_notm}}](/docs/cloud-object-storage?topic=cloud-object-storage-encryption)
- [Portworx](/docs/openshift?topic=openshift-portworx#encrypt_volumes)</br>

You can also use an {{site.data.keyword.cloud_notm}} database service, such as [{{site.data.keyword.cloudant}} NoSQL DB](/docs/Cloudant?topic=Cloudant-getting-started-with-cloudant), to persist data in a managed database outside the cluster. Data that is stored with a cloud database service can be accessed across clusters, zones, and regions. For security-related information, see the database service-specific {{site.data.keyword.cloud_notm}} documentation.

<br />


## Monitoring and logging
{: #monitoring_logging}

The key to detect malicious attacks in your cluster is the proper monitoring and logging of metrics and all the events that happen in the cluster. Monitoring and logging can also help you understand the cluster capacity and availability of resources for your app so that you can plan accordingly to protect your apps from a downtime.
{: shortdesc}

**Does IBM monitor my cluster?**</br>
Every cluster master is continuously monitored by IBM to control and remediate process level Denial-Of-Service (DOS) attacks. Red Hat OpenShift on IBM Cloud automatically scans every node where the master is deployed for vulnerabilities that are found in Kubernetes, Openshift, and OS-specific security fixes. If vulnerabilities are found, Red Hat OpenShift on IBM Cloud automatically applies fixes and resolves vulnerabilities on behalf of the user to ensure master node protection.  

**What information is logged?**</br>
By default, Red Hat OpenShift on IBM Cloud automatically collects logs for the following cluster components:

- **Containers**: Logs that are written to `STDOUT` or `STDERR`.
- **Apps**: Logs that are written to a specific path inside your app.
- **Workers**: Logs from the Red Hat Enterprise Linux operating system that are sent to `/var/log/syslog` and `/var/log/auth.log`.
- **OpenShift API server**: Every cluster-related action that is sent to the OpenShift API server is logged for auditing reasons, including the time, the user, and the affected resource. For more information, see [Kubernetes audit logs](https://kubernetes.io/docs/tasks/debug-application-cluster/audit/){: external}. You can access these logs by using {{site.data.keyword.at_full_notm}}. For more information, see the [getting started tutorial](/docs/Activity-Tracker-with-LogDNA?topic=Activity-Tracker-with-LogDNA-getting-started). 
- **Routers**: Logs inbound network traffic on routes. 
- **Kubernetes system components**: Logs from the `kubelet`, the `kube-proxy`, and other components that run in the `kube-system` namespace.

To access the logs of your cluster components, set up [{{site.data.keyword.la_full_notm}}](/docs/openshift?topic=openshift-health#openshift_logdna). {{site.data.keyword.la_full_notm}} provides access to all your logs and you can aggregate logs and build your own customized views across multiple clusters.

**How can I monitor the health and performance of my cluster?**</br>
You can verify the health, capacity, and performance of your apps, services, and worker nodes by monitoring your cluster components and compute resources from the Red Hat OpenShift on IBM Cloud console or CLI, such as the CPU and memory usage. To view more in-depth metrics for your cluster, you can use the built-in monitoring capabilities that are based on open source technologies, such as [Prometheus and Grafana](http://docs.openshift.com/container-platform/4.3/monitoring/cluster_monitoring/about-cluster-monitoring.html){: external}. Prometheus is automatically installed when you create the cluster and you can use the tool to access real-time cluster and app metrics. Prometheus metrics are not stored persistently. To access historic metrics and to compare metrics across multiple clusters, use [{{site.data.keyword.mon_full_notm}}](/docs/openshift?topic=openshift-health#openshift_sysdig) instead.

To set up a host-based intrusion detection system (HIDS) and security event log monitoring (SELM), install third-party tools that are designed to monitor your cluster and containerized apps to detect intrusion or misuse, such as [Twistlock](https://www.paloaltonetworks.com/prisma/cloud){: external} or the [Sysdig Falco project](https://sysdig.com/opensource/falco/){: external}. Sysdig Falco is a separate tool and is not included if you choose to install the IBM-provided [Sysdig add-on](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-kubernetes_cluster#kubernetes_cluster){: external} in your cluster.  

**How can I audit events that happen in my cluster?**</br>
You can [set up {{site.data.keyword.cloudaccesstraillong}} in your Red Hat OpenShift on IBM Cloud cluster](/docs/openshift?topic=openshift-at_events#at_events). For more information, view the [{{site.data.keyword.cloudaccesstrailshort}} documentation](/docs/Activity-Tracker-with-LogDNA?topic=Activity-Tracker-with-LogDNA-getting-started).

**What are my options to enable trust in my cluster?** </br>
By default, Red Hat OpenShift on IBM Cloud provides many features for your cluster components so that you can deploy your containerized apps in a security-rich environment. Extend your level of trust in your cluster to better ensure that what happens within your cluster is what you intended to happen. You can implement trust in your cluster in various ways, as shown in the following diagram.

<img src="images/trusted_story.png" width="700" alt="Deploying containers with trusted content" style="width:700px; border-style: none"/>

1.  **Content Trust for your images**: Ensure the integrity of your images by enabling content trust in your {{site.data.keyword.registrylong_notm}}. With trusted content, you can control who can sign images as trusted. After trusted signers push an image to your registry, users can pull the signed content so that they can verify the source of the image. For more information, see [Signing images for trusted content](/docs/Registry?topic=Registry-registry_trustedcontent#registry_trustedcontent).

2.  **Container Image Security Enforcement**: Create an admission controller with custom policies so that you can verify container images before you deploy them. With Container Image Security Enforcement, you control where the images are deployed from and ensure that they meet [Vulnerability Advisor](/docs/va?topic=va-va_index) policies or [content trust](/docs/Registry?topic=Registry-registry_trustedcontent#registry_trustedcontent) requirements. If a deployment does not meet the policies that you set, security enforcement prevents modifications to your cluster. For more information, see [Enforcing container image security](/docs/Registry?topic=Registry-security_enforce#security_enforce).

3.  **Image Vulnerability Scanner**: By default, Vulnerability Advisor scans images that are stored in {{site.data.keyword.registrylong_notm}} to find potential security vulnerabilities. For more information, see [Managing image security with Vulnerability Advisor](/docs/Registry?topic=va-va_index).

4.  **Network insights with Security Advisor (beta)**: With {{site.data.keyword.cloud_notm}} Security Advisor, you can centralize security insights from {{site.data.keyword.cloud_notm}} services such as Vulnerability Advisor and {{site.data.keyword.cloudcerts_short}}. When you enable Security Advisor in your cluster, you can view reports about suspicious incoming and outgoing network traffic. For more information, see [Network Analytics](/docs/security-advisor?topic=security-advisor-setup-network#setup-network). To install, see [Setting up monitoring of suspicious clients and server IP addresses for a Kubernetes cluster](/docs/security-advisor?topic=security-advisor-setup-network#setup-network).

5.  **{{site.data.keyword.cloudcerts_long_notm}}**: If you want to [expose your app by using a custom domain with TLS](/docs/openshift?topic=openshift-ingress#ingress_expose_public), you can store your TLS certificate in {{site.data.keyword.cloudcerts_short}}. Expired or about-to-expire certificates can also be reported in your {{site.data.keyword.security-advisor_short}} dashboard. For more information, see [Getting started with {{site.data.keyword.cloudcerts_short}}](/docs/certificate-manager?topic=certificate-manager-getting-started#getting-started).

<br />


## Image and registry
{: #images_registry}

Every deployment is based on an image that holds the instructions for how to spin up the container that runs your app. These instructions include the operating system inside the container and extra software that you want to install. To protect your app, you must protect the image and establish checks to ensure the image's integrity.
{: shortdesc}

**Should I use a public or a private registry to store my images?** </br>
Public registries, such as Docker Hub, can be used to get started with Docker images and Kubernetes to create your first containerized app in a cluster. But when it comes to enterprise applications, avoid registries that you don't know or don't trust to protect your cluster from malicious images. Keep your images in a private registry, like the one provided in {{site.data.keyword.registrylong_notm}} or the [internal registry](https://docs.openshift.com/container-platform/4.3/registry/architecture-component-imageregistry.html){: external} that is automatically set up in your OpenShift cluster, and make sure to control access to the registry and the image content that can be pushed.

**Why is it important to check images against vulnerabilities?** </br>
Research shows that most malicious attacks leverage known software vulnerabilities and weak system configurations. When you deploy a container from an image, the container spins up with the OS and extra binaries that you described in the image. Just like you protect your virtual or physical machine, you must eliminate known vulnerabilities in the OS and binaries that you use inside the container to protect your app from being accessed by unauthorized users. </br>

**How can I ensure secure container images?** </br>
To protect your apps, consider to address the following areas:

1. **Automate the build process and limit permissions**: </br>
Automate the process to build your container image from your source code to eliminate source code variations and defects. By integrating the build process into your CI/CD pipeline, you can ensure that your image is scanned and built only if the image passes the security checks that you specified. To avoid that developers apply hot fixes to sensitive images, limit the number of people in your organization who have access to the build process.

2. **Scan images before they deploy into production:** </br>
Make sure to scan every image before you deploy a container from it. For example, if you use {{site.data.keyword.registrylong_notm}}, all images are automatically scanned for vulnerabilities when you push the image to your namespace. If vulnerabilities are found, consider eliminating the vulnerabilities or block deployment for those images. Find a person or team in your organization who is responsible for monitoring and removing vulnerabilities. Depending on your organizational structure, this person might be part of a security, operations, or deployment team. Use admission controllers, such as the [Container Image Security Enforcement](/docs/Registry?topic=Registry-security_enforce#security_enforce) to block deployments from images that did not pass vulnerability checks and enable [content trust](/docs/Registry?topic=Registry-registry_trustedcontent#registry_trustedcontent) so that images must be approved by a trusted signer before they can be pushed to the container registry.

3. **Regularly scan running containers:** </br>
Even if you deployed a container from an image that passes the vulnerability check, the operating system or binaries that run in the container might get vulnerable over time. To protect your app, you must ensure that running containers are regularly scanned so that you can detect and remediate vulnerabilities. Depending on the app, to add extra security, you can establish a process that takes down vulnerable containers after they are detected.

**Can I use the built-in container registry in my OpenShift cluster to address build automation, image and container scanning?** </br>
You can use the built-in container registry to automate the container image build process from your source code in an external source repository to your internal registry. However, images are not automatically scanned for vulnerabilities when they are pushed to the internal registry. To set up image scanning, set up a registry namespace and push your images to the managed {{site.data.keyword.registrylong_notm}} instead. 

**How can {{site.data.keyword.registrylong_notm}} help me to protect my images and deployment process?**  


![Deploying containers with trusted content](images/oc_image_security.png)

<table>
<caption>Security for images and deployments</caption>
  <thead>
    <th>Security feature</th>
    <th>Description</th>
  </thead>
  <tbody>
    <tr>
      <td>Secured Docker private image repository in {{site.data.keyword.registrylong_notm}}</td>
      <td>Set up your own Docker [image repository](/docs/Registry?topic=Registry-getting-started#getting-started) in a multi-tenant, highly available, and scalable private image registry that is hosted and managed by IBM. By using the registry, you can build, securely store, and share Docker images across cluster users. </br></br>Learn more about [securing your personal information](/docs/openshift?topic=openshift-security#pi) when you work with container images.</td>
    </tr>
    <tr>
      <td>Push images with trusted content only</td>
      <td>Ensure the integrity of your images by enabling [content trust](/docs/Registry?topic=Registry-registry_trustedcontent#registry_trustedcontent) in your image repository. With trusted content, you can control who can sign images as trusted and push images to a specific registry namespace. After trusted signers push an image to a registry namespace, users can pull the signed content so that they can verify the publisher and the integrity of the image.</td>
    </tr>
    <tr>
      <td>Automatic vulnerability scans</td>
      <td>When you use {{site.data.keyword.registrylong_notm}}, you can leverage the built-in security scanning that is provided by [Vulnerability Advisor](/docs/va?topic=va-va_index#va_registry_cli). Every image that is pushed to your registry namespace is automatically scanned for vulnerabilities against a database of known CentOS, Debian, Red Hat, and Ubuntu issues. If vulnerabilities are found, Vulnerability Advisor provides instructions for how to resolve them to ensure image integrity and security.</td>
    </tr>
    <tr>
      <td>Block deployments from vulnerable images or untrusted users</td>
      <td>Create an admission controller with custom policies so that you can verify container images before you deploy them. With [Container Image Security Enforcement](/docs/Registry?topic=Registry-security_enforce#security_enforce), you control where the images are deployed from and ensure that they meet Vulnerability Advisor policies or content trust requirements. If a deployment does not meet the policies that you set, the admission controller blocks the deployment in your cluster.</td>
    </tr>
  </tbody>
  </table>
  </br>

**What options do I have to scan running containers for vulnerabilities?** </br>
You can install third-party solutions in your cluster, such as [Twistlock](https://www.paloaltonetworks.com/prisma/cloud){: external} or [StackRox](https://www.stackrox.com){: external} to scan running containers and block malicious activities when they are detected.

<br />


## Container isolation and security
{: #container}

When you run multiple apps in your cluster, you want to make sure that your workloads run isolated from each other and that you restrict the permissions of your pods within the cluster to avoid noisy neighbors or denial-of-service attacks.
{: shortdesc}

**What is an OpenShift project and why should I use it?** </br>
  OpenShift projects are a way to virtually partition a cluster and provide isolation for your deployments and the groups of users that want to move their workload onto the cluster. With projects, you can organize resources across worker nodes and also across zones in multizone clusters.  

Every cluster is set up with a set of default OpenShift projects that include the deployments and services that are required for Red Hat OpenShift on IBM Cloud to run properly and manage the cluster. For more information, see the [service architecture](/docs/openshift?topic=openshift-service-arch). Cluster administrators automatically have access to these projects and can set up additional projects in the cluster. In addition, cluster users who are granted access to the cluster can create their own project and, as the creator of the project, can manage the project with administrator permissions. However, cluster users do not have access to other projects by default, unless they are granted access by a cluster administrator. 

For every project that you have in the cluster, make sure to set up proper [RBAC policies](/docs/openshift?topic=openshift-users#rbac) to limit access to this project, control what gets deployed, and to set proper [resource quotas and limit ranges](https://docs.openshift.com/enterprise/3.2/dev_guide/compute_resources.html){: external}.
{: important}

**Should I set up a single-tenant or a multi-tenant cluster?** </br>
In a single-tenant cluster, you create one cluster for every group of people that must run workloads in a cluster. Usually, this team is responsible to manage the cluster and to properly configure and secure it. Multi-tenant clusters use multiple projects to isolate tenants and their workloads.

<img src="images/cs_single_multitenant.png" width="600" alt="Single tenant vs. multi-tenant cluster" style="width:600px; border-style: none"/>

Deciding between single-tenant and multi-tenant clusters depends on the number of teams that must run workloads in a cluster, their service requirements, the size of the service, and the level of isolation that you want to achieve for your workloads.

A single-tenant cluster might be your option if you have many teams with complex services that each must have control over the lifecycle of the cluster. This includes having the freedom to decide when a cluster is updated or what resources can be deployed to the cluster. You can also configure a single-tenant cluster to allow privileged pods without putting other tenants at risk of being compromised. Keep in mind that managing a cluster requires in-depth Kubernetes, OpenShift, and infrastructure knowledge to ensure cluster capacity and security for your deployments.  

Multi-tenant clusters use OpenShift projects to isolate tenants and are usually managed by a separate team that does not belong to one of the tenants. A multi-tenant cluster might be your option if you have multiple teams that must run small workloads in a cluster, and where creating a single-tenant cluster that is highly available across multiple zones does not bring the cost benefits that you want. While multi-tenant clusters usually require fewer people to manage and administer the cluster, they might not provide the level of isolation that you need and add more complexity in the following areas:

- **Access:** When you set up multiple projects, you must configure proper RBAC policies for each project to ensure resource isolation. RBAC policies are complex and require in-depth Kubernetes knowledge.
- **Privileged pods:** If one tenant in a multi-tenant cluster requires to run privileged pods, this pod can access other projects in the cluster or damage the shared compute host. Controlling privileged pods is a complex task that requires effort and deep technical expertise. Use [security context constraints (SCCs)](/docs/openshift?topic=openshift-openshift_scc#oc_sccs) to control what resources your tenants can deploy in the cluster.
- **Network policies:** Because your worker nodes are connected to the same private network, you must make sure that you have strict firewall policies in place to prevent pods from accessing pods in other namespaces.
- **Compute resource limitation:** To ensure that every team has the necessary resources to deploy services and run apps in the cluster, you must set up [resource quotas](https://kubernetes.io/docs/concepts/policy/resource-quotas/) for every namespace. Resource quotas determine the deployment constraints for a project, such as the number of Kubernetes resources that you can deploy, and the amount of CPU and memory that can be consumed by those resources. After you set a quota, users must include resource requests and limits in their deployments.
- **Shared cluster resources:** If you run multiple tenants in one cluster, some cluster resources, such as the  OpenShift router, Ingress application load balancer (ALB) or available portable IP addresses are shared across tenants. Smaller services might have a hard time using shared resources if they must compete against large services in the cluster.
- **Updates:** You can run one OpenShift API version at a time only. All apps that run in a cluster must comply with the current OpenShift API version independent of the team that owns the app. When you want to update a cluster, you must ensure that all teams are ready to switch to a new OpenShift API version and that apps are updated accordingly. This also means that individual teams have less control over the OpenShift API version they want to run.
- **Changes in cluster setup:** If you want to change the cluster setup or reschedule workloads onto new worker nodes, you must roll out this change across tenants. This roll out requires more reconciliation and testing than in a single-tenant cluster.
- **Communication process:** When you manage multiple tenants, consider setting up a communication process so that tenants know where to go when an issue with the cluster exists, or when they need more resources for their services. This communication process also includes informing your tenants about all changes in the cluster setup or planned updates.

Although single-tenant and multi-tenant clusters come with roughly the same costs, single-tenant clusters provide a higher level of isolation than the projects in a multi-tenant cluster. For better workload isolation, use single-tenant clusters.
{: important}

**How can I control pod permissions?** </br>
To control pod permissions within or across projects, Red Hat OpenShift on IBM Cloud uses security context constraints (SCCs). By default, every cluster is set up with [OpenShift SCCs](/docs/openshift?topic=openshift-openshift_scc#oc_sccs) and a set of [IBM-provided SCCs](/docs/openshift?topic=openshift-openshift_scc#ibm_sccs) that you can assign to service accounts, pods, deployments, or projects to limit the permissions within the cluster. If you do not explicitly assign an SCC, your pods use the `restricted` SCC. OpenShift SCCs are stricter than the default pod security policies in community Kubernetes clusters. You might need to modify an app that runs in a community Kubernetes cluster so that this app can run in OpenShift. For more information, see [Configuring security context constraints](/docs/openshift?topic=openshift-openshift_scc). 

**What else can I do to protect my container?**

|Security feature|Description|
|-------|----------------------------------|
|Limit the number of privileged containers|Containers run as a separate Linux process on the compute host that is isolated from other processes. Although users have root access inside the container, the permissions of this user are limited outside the container to protect other Linux processes, the host file system, and host devices. Some apps require access to the host file system or advanced permissions to run properly. You can run containers in privileged mode to allow the container the same access as the processes running on the compute host.<p class="important">Keep in mind that privileged containers can cause huge damage to the cluster and the underlying compute host if they become compromised. Try to limit the number of containers that run in privileged mode and consider changing the configuration for your app so that the app can run without advanced permissions. If you want to block privileged containers from running in your cluster, consider setting up custom [security context constraints](/docs/openshift?topic=openshift-openshift_scc#customize_sccs).</p>|
|Apply OS security settings to pods|You can customize the default [security context constraints](https://docs.openshift.com/enterprise/3.0/admin_guide/manage_scc.html) to control the user ID and group ID that can run inside the container, or the user ID and group ID that owns the volume mount path. For more information , see [Configuring security context constraints](/docs/openshift?topic=openshift-openshift_scc). |
|Set CPU and memory limits for containers|Every container requires a specific amount of CPU and memory to properly start and to continue to run. You can define [Limit ranges](https://docs.openshift.com/enterprise/3.1/dev_guide/limits.html){: external} for your containers or pods to limit the amount of CPU and memory that they can consume. If no limits for CPU and memory are set, and the container is busy, the container uses all the resources that are available. This high consumption of resources might affect other containers on the worker node that do not have enough resources to properly start or run, and puts your worker node at risk for denial-of-service attacks.|

{: caption="Other security protections" caption-side="top"}

<br />


## Storing personal information
{: #pi}

You are responsible for ensuring the security of your personal information in Kubernetes resources and container images. Personal information includes your name, address, phone number, email address, or other information that might identify, contact, or locate you, your customers, or anyone else.
{: shortdesc}

<dl>
  <dt>Use a Kubernetes secret to store personal information</dt>
  <dd>Store personal information only in Kubernetes resources that are designed to hold personal information. For example, do not use your name in the name of an OpenShift project, deployment, service, or config map. For proper protection and encryption, store personal information in [secrets](https://docs.openshift.com/container-platform/3.11/dev_guide/secrets.html){: external} instead.</dd>

  <dt>Use a Kubernetes `imagePullSecret` to store image registry credentials</dt>
  <dd>Do not store personal information in container images or registry namespaces. For proper protection and encryption, store registry credentials in <a href="/docs/openshift?topic=openshift-registry#other">Kubernetes `imagePullSecrets`</a> and other personal information in [secrets](https://docs.openshift.com/container-platform/3.11/dev_guide/secrets.html){: external} instead. Remember that if personal information is stored in a previous layer of an image, deleting an image might not be sufficient to delete this personal information.</dd>
  </dl>



On SGX-enabled bare metal worker nodes, you can encrypt your data in use by using [{{site.data.keyword.datashield_short}}](/docs/data-shield?topic=data-shield-getting-started). Similar to the way encryption works for data at rest and data in motion, Fortanix Runtime Encryption that is integrated with {{site.data.keyword.datashield_short}} protects keys, data, and apps from external and internal threats. The threats might include malicious insiders, cloud providers, OS-level hacks, or network intruders.

## Kubernetes security bulletins
{: #security_bulletins}

If vulnerabilities are found in Kubernetes, Kubernetes releases CVEs in security bulletins to inform users and to describe the actions that users must take to remediate the vulnerability. Kubernetes security bulletins that affect Red Hat OpenShift on IBM Cloud users or the {{site.data.keyword.cloud_notm}} platform are published in the [{{site.data.keyword.cloud_notm}} security bulletin](https://cloud.ibm.com/status?component=containers-kubernetes&selected=security).

Some CVEs require the latest patch update for a OpenShift version that you can install as part of the regular [cluster update process](/docs/openshift?topic=openshift-update#update) in Red Hat OpenShift on IBM Cloud. Make sure to apply security patches in time to protect your cluster from malicious attacks. For more information about what is included in a security patch, refer to the [version changelog](/docs/openshift?topic=openshift-openshift_changelog).



