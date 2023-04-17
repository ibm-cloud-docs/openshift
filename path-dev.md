---

copyright: 
  years: 2014, 2023
lastupdated: "2023-04-17"

keywords: openshift, red hat, red hat openshift, dev

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}







# Learning path for developers
{: #learning-path-dev}

Following a curated learning path to deploy highly available containerized apps in {{site.data.keyword.redhat_openshift_notm}} clusters and use the powerful tools of {{site.data.keyword.openshiftlong_notm}} to automate, isolate, secure, manage, and monitor your app workloads across zones or regions.
{: shortdesc}


## Access the cluster
{: #dev_cluster}

Begin working with your cluster by setting up the CLI and accessing the cluster.
{: shortdesc}

1. **CLI setup**: [Set up the CLIs](/docs/openshift?topic=openshift-openshift-cli) that are necessary to create and work with clusters. As you work with your cluster, refer to the [command reference](/docs/openshift?topic=openshift-kubernetes-service-cli) and keep track of CLI version updates with the [CLI change log](/docs/openshift?topic=openshift-cs_cli_changelog).
2. **User permissions**: Ensure that your cluster administrator gives you the proper [{{site.data.keyword.cloud_notm}} IAM role](/docs/openshift?topic=openshift-learning-path-admin#admin_secure) to access the cluster.
3. **Cluster access**: [Access your cluster through the public or private cloud service endpoint](/docs/containers?topic=containers-access_cluster).

Need help? Check out [Troubleshooting clusters and masters](/docs/openshift?topic=openshift-debug_clusters) and [Troubleshooting worker nodes](/docs/openshift?topic=openshift-debug_worker_nodes).
{: tip}


## Plan your deployment
{: #dev_plan}

Before you deploy an app, decide how you want to set up your app so that your app can be accessed properly and be integrated with other services.
{: shortdesc}

1. **Kubernetes-native**: [Plan your strategy for developing a Kubernetes-native app](/docs/openshift?topic=openshift-plan_deploy).
2. **Highly available**: [Plan your strategy for a highly available deployment](/docs/openshift?topic=openshift-plan_deploy#highly_available_apps).

Looking for serverless? Try [{{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-getting-started).
{: tip}

## Develop your app
{: #dev_develop}

Configure your app in a YAML file that declares the configuration of the Kubernetes object, and plan your app versioning strategy.
{: shortdesc}

1. **Develop your app**:
    1. Review the [basics of Kubernetes-native app deployments](/docs/openshift?topic=openshift-plan_deploy#kube-objects).
    2. Build app containers from [images in the internal, public, or private registries](/docs/openshift?topic=openshift-images).
    3. Specify your [app requirements in a YAML file](/docs/openshift?topic=openshift-openshift_apps#app_yaml), which declares the configuration of the Kubernetes object.
2. **Version your app**:
    1. Version 4: To plan customized configurations for more than one environment, such as development, testing, and production environments, [use the Kustomize tool](/docs/openshift?topic=openshift-openshift_apps#kustomize) to manage your configuration YAML file.
    2. If you want to run your app in multiple clusters, public and private environments, or even multiple cloud providers, [package your application to help automate deployments](/docs/openshift?topic=openshift-plan_deploy#packaging).

Need help? Check out [Troubleshooting apps and integrations](/docs/openshift?topic=openshift-debug_apps).
{: tip}


## Deploy your app
{: #dev_deploy}

Deploy your app to the cluster by running your app configuration file.
{: shortdesc}


- [Deploying apps through the console](/docs/openshift?topic=openshift-deploy_app#deploy_apps_ui).
- [Deploying apps through the CLI](/docs/openshift?topic=openshift-deploy_app#deploy_apps_cli).
- [Deploying apps to specific worker nodes by using labels](/docs/openshift?topic=openshift-deploy_app#node_affinity).


Need help? Check out [Troubleshooting apps and integrations](/docs/openshift?topic=openshift-debug_apps).
{: tip}


## Test, log, and monitor
{: #dev_test}

While you conduct performance testing on your app, set up logging and monitoring to help you troubleshoot issues, gain visibility into your workloads, and improve the health and performance of your apps.
{: shortdesc}

In a test environment, deliberately create various non-ideal scenarios, such as deleting all worker nodes in a zone to replicate a zonal failure. Review the logs and metrics to check how your app recovers.

1. **Test access**: Test access to your app by creating a public or private [NodePort](/docs/openshift?topic=openshift-nodeport) on your worker nodes.
2. **Understand logging and monitoring options**: [Choose solutions for app and cluster logging, audit logging, and monitoring](/docs/openshift?topic=openshift-health#oc_logmet_options) based on your needs.
3. **Monitoring through the console**: Open the [OpenShift web console](/docs/openshift?topic=openshift-deploy_app#openshift_console) to view information about your app resources.
4. **{{site.data.keyword.la_short}} and {{site.data.keyword.mon_short}}**: To monitor cluster health, forward logs to [{{site.data.keyword.la_full_notm}}](/docs/openshift?topic=openshift-health#openshift_logging) and metrics to [{{site.data.keyword.mon_full_notm}}](/docs/openshift?topic=openshift-health-monitor).



## Update your app
{: #dev_update}

Perform rolling updates and rollbacks of apps without downtime for your users.
{: shortdesc}

1. **Update strategy**: [Plan your strategy for keeping your app up-to-date](/docs/openshift?topic=openshift-update_app#updating_apps).
2. **Set up updates**:
    - Add a [rolling update to your deployment file](/docs/openshift?topic=openshift-update_app#app_rolling)
    - Set up [a continuous delivery pipeline for a cluster](/docs/openshift?topic=openshift-cicd).
3. **Scaling**: Enable [horizontal pod autoscaling](/docs/openshift?topic=openshift-update_app#app_scaling) to automatically increase or decrease the number of instances of your apps based on CPU.



## Secure your app
{: #dev_secure}

Use Kubernetes secrets to store confidential information, such as credentials or keys, and encrypt data in Kubernetes secrets to prevent unauthorized users from accessing sensitive app information.
{: shortdesc}


1. **Secrets**: Store personal or sensitive information in [Kubernetes secrets](/docs/openshift?topic=openshift-security#pi) that your app can access.
2. **Secret encryption**: [Encrypt secrets by using a KMS provider](/docs/openshift?topic=openshift-encryption#keyprotect) and [verify that secrets are encrypted](/docs/openshift?topic=openshift-encryption#verify_kms).



## Expose your app
{: #dev_expose}

Publicly expose an app in your cluster to the internet or privately expose an app in your cluster to the private network only.
{: shortdesc}

1. **Plan service discovery**:
    1. Understand the [basics of Kubernetes service discovery](/docs/openshift?topic=openshift-plan_deploy#service_discovery).
    2. [Choose an app exposure service](/docs/openshift?topic=openshift-cs_network_planning) that fits your requirements for incoming traffic to the app.
2. **Expose your app**:
    - Load balancers:
        - Classic clusters:
            1. Create an [NLB 1.0](/docs/openshift?topic=openshift-loadbalancer) or [NLB 2.0](/docs/openshift?topic=openshift-loadbalancer-v2).
            2. [Register a DNS subdomain](/docs/openshift?topic=openshift-loadbalancer_hostname#loadbalancer_hostname) for the NLB.
        - VPC clusters: Set up a [VPC load balancer](/docs/openshift?topic=openshift-vpc-lbaas).

    - Ingress: Configure Ingress for the [public network](/docs/openshift?topic=openshift-ingress-public-expose&interface=ui) or the [private network](/docs/openshift?topic=openshift-ingress-private-expose&interface=ui).

    - Routes: [Create a route to expose your app on a subdomain.](/docs/openshift?topic=openshift-openshift_routes)

Need help? Check out [Troubleshooting Ingress](/docs/containers?topic=containers-ingress-debug) and [Troubleshooting load balancers](/docs/openshift?topic=openshift-cs_loadbalancer_fails).
{: tip}

## Add app storage
{: #dev_storage}

1. **Storage basics**: Start by understanding the [basics of Kubernetes storage](/docs/openshift?topic=openshift-kube_concepts).
2. **Requirements**: Determine your [requirements for a storage solution](/docs/openshift?topic=openshift-storage-plan).
3. **Choose a solution**: Using your storage requirements, choose a storage solution by comparing [your options](/docs/openshift?topic=openshift-storage-plan).

Need help? Check out the troubleshooting page for your persistent storage solution.
{: tip}

## Add integrations
{: #dev_integrate}

Enhance app capabilities by integrating various external services and catalog services in your cluster with your app.
{: shortdesc}

1. **Review supported integrations**:
    - [All supported integrations](/docs/containers?topic=containers-supported_integrations#supported_integrations)
    - [{{site.data.keyword.openshiftlong_notm}} partners](/docs/openshift?topic=openshift-service-partners)
    - [{{site.data.keyword.cloud_notm}} services and third-party integrations](/docs/openshift?topic=openshift-ibm-3rd-party-integrations)
    - [Cloud Paks](/docs/openshift?topic=openshift-openshift_cloud_paks)
    - [Operators](/docs/openshift?topic=openshift-operators)
2. **Add services to your cluster**: Ask your cluster administrator to [add the integration to your cluster](/docs/openshift?topic=openshift-learning-path-admin#admin_integrate).
3. **Access services from your app**: Ensure that your app can access the service. For example, to access an IBM Cloud service instance from your app, you must [make the service credentials that are stored in the Kubernetes secret available to your app](/docs/openshift?topic=openshift-service-binding#adding_app).

Need help? Check out [Troubleshooting apps and integrations](/docs/openshift?topic=openshift-debug_worker_nodes).
{: tip}f


