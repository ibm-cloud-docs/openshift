---

copyright: 
  years: 2014, 2025
lastupdated: "2025-10-16"


keywords: openshift, red hat, red hat openshift, admin

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}





# Learning path for administrators
{: #learning-path-admin}

Following a curated learning path through {{site.data.keyword.openshiftlong}} to create a cluster, manage the cluster's resources and lifecycle, and use the powerful tools of {{site.data.keyword.openshiftlong_notm}} to secure, manage, and monitor your cluster workloads.
{: shortdesc}



## Plan your environment
{: #admin_plan}

Start by designing a cluster for maximum availability and capacity for your workloads.
{: shortdesc}

1. **Environment strategy**:
    1. Define your [Kubernetes strategy](/docs/openshift?topic=openshift-strategy) for the cluster, such as deciding how many clusters to create for your environments.
    2. Plan your [security strategy](/docs/openshift?topic=openshift-security#network_segmentation), such as ensuring network segmentation and workload isolation.

2. **Cluster setup**: After you plan your environment, plan the setup for a specific cluster.
    1. Choose a [supported infrastructure provider](/docs/openshift?topic=openshift-overview#what-compute-infra-is-offered).
    2. Plan your cluster network setup.
        - [Understanding VPC cluster network basics](/docs/openshift?topic=openshift-plan_vpc_basics).
        - [Understanding Classic cluster network basics](/docs/openshift?topic=openshift-plan_basics).
    3. Plan your cluster for [high availability](/docs/openshift?topic=openshift-strategy).
    4. Plan your [worker node setup](/docs/openshift?topic=openshift-strategy#env_flavors_node).

Looking for serverless? Try [{{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-getting-started).
{: tip}

## Create a cluster
{: #admin_cluster}

Create a cluster with infrastructure, network, and availability setups that are customized to your use case and cloud environment.
{: shortdesc}

1. **Firewall**: If you have corporate firewalls, make sure that you [open the required ports and IP addresses](/docs/openshift?topic=openshift-firewall#corporate) to work with {{site.data.keyword.openshiftlong_notm}}.
2. **CLI and API**:
    1. [Set up the CLIs](/docs/openshift?topic=openshift-cli-install) that are necessary to create and work with clusters. As you work with your cluster, refer to the [command reference](/docs/openshift?topic=openshift-kubernetes-service-cli) and keep track of CLI version updates with the [CLI change log](/docs/openshift?topic=openshift-cs_cli_changelog).
    2. Optionally set up [automated deployments with the API](/docs/openshift?topic=openshift-cs_api_install). As you work with your cluster, refer to the [IBM Cloud Kubernetes Service API reference](https://cloud.ibm.com/apidocs/kubernetes/containers-v1-v2){: external} and [Community Kubernetes API reference](https://kubernetes.io/docs/reference/){: external}.
3. **Cluster deployment**:
    1. [Create the cluster](/docs/openshift?topic=openshift-clusters).
    2. After the cluster is ready, [access your cluster](/docs/containers?topic=containers-access_cluster).
    3. Spread your cluster across availability zones [adding worker nodes to Classic clusters](/docs/openshift?topic=openshift-add-workers-classic) or [adding worker nodes to VPC clusters](/docs/openshift?topic=openshift-add-workers-vpc). 
4. **User access**:
    * Make sure that your authorized cluster users can now also access the cluster by planning your user access strategy.
    * [Pick the correct access policy and role for your users](/docs/openshift?topic=openshift-iam-platform-access-roles). Choose the scope of user access to cluster instances, {{site.data.keyword.redhat_openshift_notm}} project, or resource groups.



Need help? Check out [Troubleshooting clusters and masters](/docs/openshift?topic=openshift-debug_clusters) and [Troubleshooting worker nodes](/docs/openshift?topic=openshift-debug_worker_nodes).
{: tip}


## Manage the network
{: #admin_network}

Review the following optional topics to manage the network connectivity of your cluster components and connections to other networks. For example, you might need to connect the workloads in your cluster to workloads in another private network. Or, you might return to this section later if you need to make more portable IP addresses available for load balancer services that expose apps in your cluster.
{: shortdesc}

- **Connections to other networks and workloads**: Set up VPN connectivity between your [classic cluster](/docs/openshift?topic=openshift-vpn) or [VPC cluster](/docs/openshift?topic=openshift-vpc-vpnaas) and remote network environments, other VPCs, and more.
    - To route responses from your cluster back to your on-premises network in VPN solutions that preserve the request source IP address, add [custom static routes](/docs/openshift?topic=openshift-static-routes) to worker nodes for on-premises subnets.
- **Subnets and VLANs**:
    - Add or change the available subnets and IP addresses for your [classic cluster](/docs/openshift?topic=openshift-subnets) or [VPC cluster](/docs/openshift?topic=openshift-vpc-subnets).
    - Classic clusters: Change the [VLAN connections for your worker nodes](/docs/containers?topic=containers-cs_network_cluster#change-vlans).



## Secure your cluster
{: #admin_secure}

Use built-in security features to protect your cluster infrastructure and network communication, isolate your compute resources, and ensure security compliance across your infrastructure components and container deployments.
{: shortdesc}

1. **Security strategy**: Start by reviewing all [security options](/docs/openshift?topic=openshift-security) that are available for your cluster.
2. **Network security**:
    - Classic clusters:
        1. To isolate networking workloads, you can restrict network traffic to [edge worker nodes](/docs/openshift?topic=openshift-edge).
        2. Set up a firewall by using a [gateway appliance](/docs/openshift?topic=openshift-firewall#vyatta_firewall) or [Calico network policies](/docs/openshift?topic=openshift-network_policies).
    - VPC clusters: Control traffic to and from your cluster with [VPC security groups](/docs/openshift?topic=openshift-vpc-security-group-manage).
3. **Workload security**:
    1. [Encrypt sensitive information](/docs/openshift?topic=openshift-encryption) in the cluster, such as the master's local disk and secrets.
    2. Set up a [private image registry](/docs/openshift?topic=openshift-security#images_registry) for your developers, such as the one provided by {{site.data.keyword.registryshort}}, to control access to the registry and the image content that can be pushed.
    3. [Set pod priority](/docs/openshift?topic=openshift-pod_priority) to indicate the relative priority of the pods that make up your cluster's workload.
    4. Authorize who can create and update pods by configuring [security context constraints (SCCs)](/docs/openshift?topic=openshift-openshift_scc).



## Logging and monitoring
{: #admin_health}

Set up logging and monitoring to help you troubleshoot issues and improve the health and performance of your Kubernetes clusters and apps.
{: shortdesc}




1. **Understand options**: [Choose solutions for app and cluster logging, audit logging, and monitoring](/docs/openshift?topic=openshift-health#oc_logmet_options) based on your needs.

2. **{{site.data.keyword.logs_full_notm}} and {{site.data.keyword.mon_short}}**: To monitor cluster health, forward logs to [{{site.data.keyword.logs_full_notm}}](/docs/openshift?topic=openshift-health) and metrics to [{{site.data.keyword.mon_full_notm}}](/docs/openshift?topic=openshift-health-monitor).






## Add a registry and CI/CD
{: #admin_registry}

Set up an image registry and a continuous integration and delivery (CI/CD) pipeline for your cluster.
{: shortdesc}

1. **Registry**: Choose and set up an [image registry](/docs/openshift?topic=openshift-registry) so that developers can pull images from the registry in their app deployment YAML files. Your cluster comes with the following default configurations that your developers can use.
    - **Internal {{site.data.keyword.redhat_openshift_notm}} container registry**: The [internal registry](/docs/openshift?topic=openshift-registry#openshift_internal_registry) is set up by default, with the images stored in an attached storage device. You can also choose to [pull an image from a private registry](/docs/openshift?topic=openshift-registry#imagestream_registry) like {{site.data.keyword.registrylong_notm}} into the image stream of the internal registry so that the image is available locally to all the projects in the cluster.
    - **Private registry**: Your cluster is set up to pull images from [{{site.data.keyword.registrylong_notm}}](/docs/openshift?topic=openshift-registry#openshift_iccr) in the `default` project only. To pull images from a private registry in other projects, [create an image pull secret](/docs/openshift?topic=openshift-registry#other) in the other projects or [import an image from your private registry into the internal registry image stream](/docs/openshift?topic=openshift-registry#imagestream_registry).
2. **CI/CD**:
    - Review available [options for automating app deployment](/docs/openshift?topic=openshift-cicd).
    - Set up toolchains with [{{site.data.keyword.deliverypipelinelong}}](/docs/openshift?topic=openshift-cicd).

## Add storage
{: #admin_storage}

Plan and add highly available persistent storage based on your app requirements, the type of data that you want to store, and how often you want to access this data.
{: shortdesc}

1. **Requirements**: Determine your [requirements for a storage solution](/docs/openshift?topic=openshift-storage-plan).
2. **Choose a solution**: Using your storage requirements, choose a storage solution by comparing [non-persistent](/docs/openshift?topic=openshift-storage-plan), [single-zone persistent](/docs/openshift?topic=openshift-storage-plan), or [multizone persistent](/docs/openshift?topic=openshift-storage-plan) storage.

Need help? Check out the troubleshooting page for your persistent storage solution.
{: tip}


## Add integrations
{: #admin_integrate}

Enhance cluster capabilities by integrating various external services and catalog services with your Kubernetes cluster.
{: shortdesc}

1. **Review supported integrations**:
    - [All supported integrations](/docs/containers?topic=containers-supported_integrations)
    - [{{site.data.keyword.openshiftlong_notm}} partners](/docs/openshift?topic=openshift-supported_integrations)

    - [{{site.data.keyword.cloud_notm}} services and third-party integrations](/docs/openshift?topic=openshift-ibm-3rd-party-integrations)
2. **Add services to your cluster**:
    - [Adding Cloud Paks](/docs/openshift?topic=openshift-openshift_cloud_paks)
    - [Adding services by using Operators](/docs/openshift?topic=openshift-operators)
    - [Adding services by using {{site.data.keyword.cloud_notm}} service binding](/docs/openshift?topic=openshift-service-binding)

Need help? Check out [Troubleshooting apps and integrations](/docs/openshift?topic=openshift-debug_worker_nodes).
{: tip}


## Manage the lifecycle
{: #admin_lifecycle}

Manage your cluster and worker nodes through each phase of the cluster lifecycle.
{: shortdesc}

- **Autoscaling**: [Automatically increase or decrease the number of worker nodes](/docs/openshift?topic=openshift-cluster-scaling-install-addon) based on the sizing needs of your scheduled workloads.
- **Updating**: Keep your environment up-to-date by frequently [updating clusters, worker nodes, and cluster components](/docs/openshift?topic=openshift-update). While you update, refer to these version reference pages:
    - [{{site.data.keyword.openshiftshort}} version information](/docs/openshift?topic=openshift-openshift_versions)
    - [Fluentd and Ingress ALB change log](/docs/containers?topic=containers-cl-ingress-alb)
- **Removing**: [Remove clusters and clean up related resources](/docs/openshift?topic=openshift-remove).



Need help? Check out troubleshooting [clusters and masters](/docs/openshift?topic=openshift-debug_clusters), [worker nodes](/docs/openshift?topic=openshift-debug_worker_nodes), or the [cluster autoscaler](/docs/openshift?topic=openshift-debug_cluster_autoscaler).
{: tip}
