---

copyright:
  years: 2014, 2020
lastupdated: "2020-07-21"

keywords: openshift, red hat, red hat openshift, rhos, roks, rhoks, dev

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



<style>
    <!--
        #tutorials { /* hide the page header */
            display: none !important;
        }
        .allCategories {
            display: flex !important;
            flex-direction: row !important;
            flex-wrap: wrap !important;
        }
        .categoryBox {
            flex-grow: 1 !important;
            width: calc(33% - 20px) !important;
            text-decoration: none !important;
            margin: 0 10px 20px 0 !important;
            padding: 16px !important;
            border: 1px #dfe6eb solid !important;
            box-shadow: 0 1px 2px 0 rgba(0, 0, 0, 0.2) !important;
            text-align: center !important;
            text-overflow: ellipsis !important;
            overflow: hidden !important;
        }
        .solutionBoxContainer {}
        .solutionBoxContainer a {
            text-decoration: none !important;
            border: none !important;
        }
        .solutionBox {
            display: inline-block !important;
            width: 100% !important;
            margin: 0 10px 20px 0 !important;
            padding: 16px !important;
            background-color: #f4f4f4 !important;
        }
        @media screen and (min-width: 960px) {
            .solutionBox {
            width: calc(50% - 3%) !important;
            }
            .solutionBox.solutionBoxFeatured {
            width: calc(50% - 3%) !important;
            }
            .solutionBoxContent {
            height: 350px !important;
            }
        }
        @media screen and (min-width: 1298px) {
            .solutionBox {
            width: calc(33% - 2%) !important;
            }
            .solutionBoxContent {
            min-height: 350px !important;
            }
        }
        .solutionBox:hover {
            border: 1px rgb(136, 151, 162)solid !important;
            box-shadow: 0 1px 2px 0 rgba(0, 0, 0, 0.2) !important;
        }
        .solutionBoxContent {
            display: flex !important;
            flex-direction: column !important;
        }
        .solutionBoxTitle {
            margin: 0rem !important;
            margin-bottom: 5px !important;
            font-size: 14px !important;
            font-weight: 900 !important;
            line-height: 16px !important;
            height: 37px !important;
            text-overflow: ellipsis !important;
            overflow: hidden !important;
            display: -webkit-box !important;
            -webkit-line-clamp: 2 !important;
            -webkit-box-orient: vertical !important;
            -webkit-box-align: inherit !important;
        }
        .solutionBoxDescription {
            flex-grow: 1 !important;
            display: flex !important;
            flex-direction: column !important;
        }
        .descriptionContainer {
        }
        .descriptionContainer p {
            margin: 0 !important;
            overflow: hidden !important;
            display: -webkit-box !important;
            -webkit-line-clamp: 4 !important;
            -webkit-box-orient: vertical !important;
            font-size: 14px !important;
            font-weight: 400 !important;
            line-height: 1.5 !important;
            letter-spacing: 0 !important;
            max-height: 70px !important;
        }
        .architectureDiagramContainer {
            flex-grow: 1 !important;
            min-width: calc(33% - 2%) !important;
            padding: 0 16px !important;
            text-align: center !important;
            display: flex !important;
            flex-direction: column !important;
            justify-content: center !important;
            background-color: #f4f4f4;
        }
        .architectureDiagram {
            max-height: 175px !important;
            padding: 5px !important;
            margin: 0 auto !important;
        }
    -->
    </style>

# Learning path for developers
{: #learning-path-dev}

Following a curated learning path to deploy highly available containerized apps in OpenShift clusters and use the powerful tools of Red Hat OpenShift on IBM Cloud to automate, isolate, secure, manage, and monitor your app workloads across zones or regions.
{: shortdesc}

<div class=solutionBoxContainer>
  <div class="solutionBox">
    <a href = "#dev_cluster">
      <div>
        <img src="images/desktop.svg" alt="Access icon" style="height:50px; border-style: none"/>
        <h2>Access the cluster</h2>
        <p class="bx--type-caption">Begin working with your cluster by setting up the CLI and accessing the cluster.</p>
      </div>
    </a>
  </div>
  <div class="solutionBox">
    <a href = "#dev_plan">
      <div>
        <img src="images/progress.svg" alt="Plan icon" style="height:50px; border-style: none"/>
        <h2>Plan your deployment</h2>
        <p class="bx--type-caption">Plan your app setup for optimal service integration and high availability.</p>
      </div>
    </a>
  </div>
  <div class="solutionBox">
    <a href = "#dev_develop">
      <div>
        <img src="images/design--and--development--02.svg" alt="Develop icon" style="height:50px; border-style: none"/>
        <h2>Develop your app</h2>
        <p class="bx--type-caption">Configure your app and set up your app versioning and delivery pipeline.</p>
      </div>
    </a>
  </div>
  <div class="solutionBox">
    <a href = "#dev_deploy">
      <div>
        <img src="images/app--developer.svg" alt="Deploy icon" style="height:50px; border-style: none"/>
        <h2>Deploy your app</h2>
        <p class="bx--type-caption">Deploy your app to the cluster by running your app configuration file.</p>
      </div>
    </a>
  </div>
  <div class="solutionBox">
    <a href = "#dev_test">
      <div>
        <img src="images/chart--line.svg" alt="Health icon" style="height:50px; border-style: none"/>
        <h2>Test, log, and monitor</h2>
        <p class="bx--type-caption">Conduct app performance testing and gain visibility into your workload health.</p>
      </div>
    </a>
  </div>
  <div class="solutionBox">
    <a href = "#dev_update">
      <div>
        <img src="images/networking--04.svg" alt="Update icon" style="height:50px; border-style: none"/>
        <h2>Update your app</h2>
        <p class="bx--type-caption">Perform rolling updates and rollbacks of apps without downtime for your users.</p>
      </div>
    </a>
  </div>
  <div class="solutionBox">
    <a href = "#dev_secure">
      <div>
        <img src="images/lock--alt.svg" alt="Security icon" style="height:50px; border-style: none"/>
        <h2>Secure your app</h2>
        <p class="bx--type-caption">Encrypt data and store confidential information in Kubernetes secrets.</p>
      </div>
    </a>
  </div>
  <div class="solutionBox">
    <a href = "#dev_expose">
      <div>
        <img src="images/global--network.svg" alt="Network icon" style="height:50px; border-style: none"/>
        <h2>Expose your app</h2>
        <p class="bx--type-caption">Expose an app to users on the internet or on a private network only.</p>
      </div>
    </a>
  </div>
  <div class="solutionBox">
    <a href = "#dev_storage">
      <div>
        <img src="images/data--storage.svg" alt="Storage icon" style="height:50px; border-style: none"/>
        <h2>Add app storage</h2>
        <p class="bx--type-caption">Plan and add highly available persistent storage for your app data.</p>
      </div>
    </a>
  </div>
  <div class="solutionBox">
    <a href = "#dev_integrate">
      <div>
        <img src="images/connect.svg" alt="Integrations icon" style="height:50px; border-style: none"/>
        <h2>Add integrations</h2>
        <p class="bx--type-caption">Enhance app capabilities by integrating external and catalog services.</p>
      </div>
    </a>
  </div>
</div>

## Access the cluster
{: #dev_cluster}

Begin working with your cluster by setting up the CLI and accessing the cluster.
{: shortdesc}

1. **CLI setup**: [Set up the CLIs](/docs/openshift?topic=openshift-openshift-cli) that are necessary to create and work with clusters. As you work with your cluster, refer to the [command reference](/docs/openshift?topic=openshift-kubernetes-service-cli) and keep track of CLI version updates with the [CLI changelog](/docs/openshift?topic=openshift-cs_cli_changelog).
2. **User permissions**: Ensure that your cluster administrator gives you the proper [{{site.data.keyword.cloud_notm}} IAM role](/docs/openshift?topic=openshift-learning-path-admin#admin_secure) to access the cluster.
3. **Cluster access**: [Access your cluster through the public or private service endpoint](/docs/openshift?topic=openshift-access_cluster).

</br>Need help? Check out [Troubleshooting clusters and masters](/docs/openshift?topic=openshift-cs_troubleshoot) and [Troubleshooting worker nodes](/docs/openshift?topic=openshift-cs_troubleshoot_clusters).

<br />


## Plan your deployment
{: #dev_plan}

Before you deploy an app, decide how you want to set up your app so that your app can be accessed properly and be integrated with other services.
{: shortdesc}

1. **Kubernetes-native**: [Plan your strategy for developing a Kubernetes-native app](/docs/openshift?topic=openshift-plan_deploy).
2. **Highly available**: [Plan your strategy for a highly available deployment](/docs/openshift?topic=openshift-plan_deploy#highly_available_apps).

<br />


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

</br>Need help? Check out [Troubleshooting apps and integrations](/docs/openshift?topic=openshift-cs_troubleshoot_app).

<br />


## Deploy your app
{: #dev_deploy}

Deploy your app to the cluster by running your app configuration file.
{: shortdesc}


* [Deploying apps through the console](/docs/openshift?topic=openshift-deploy_app#deploy_apps_ui)
* [Deploying apps through the CLI](/docs/openshift?topic=openshift-deploy_app#deploy_apps_cli)
* [Deploying apps to specific worker nodes by using labels](/docs/openshift?topic=openshift-deploy_app#node_affinity)


</br>Need help? Check out [Troubleshooting apps and integrations](/docs/openshift?topic=openshift-cs_troubleshoot_app).

<br />


## Test, log, and monitor
{: #dev_test}

While you conduct performance testing on your app, set up logging and monitoring to help you troubleshoot issues, gain visibility into your workloads, and improve the health and performance of your apps.
{: shortdesc}

In a test environment, deliberately create various non-ideal scenarios, such as deleting all worker nodes in a zone to replicate a zonal failure. Review the logs and metrics to check how your app recovers.

1. **Test access**: Test access to your app by creating a public or private [NodePort](/docs/openshift?topic=openshift-nodeport) on your worker nodes.
2. **Understand logging and monitoring options**: [Choose solutions for app and cluster logging, audit logging, and monitoring](/docs/openshift?topic=openshift-health#oc_logmet_options) based on your needs.
3. **Monitoring through the console**: Open the [OpenShift web console](/docs/openshift?topic=openshift-deploy_app#openshift_console) to view information about your app resources.
4. **LogDNA and Sysdig**: To monitor cluster health, forward logs to [LogDNA](/docs/openshift?topic=openshift-health#openshift_logdna) and metrics to [Sysdig](/docs/openshift?topic=openshift-health#openshift_sysdig).

<br />


## Update your app
{: #dev_update}

Perform rolling updates and rollbacks of apps without downtime for your users.
{: shortdesc}

1. **Update strategy**: [Plan your strategy for keeping your app up-to-date](/docs/openshift?topic=openshift-update_app#updating_apps).
2. **Set up updates**:
  * Add a [rolling update to your deployment file](/docs/openshift?topic=openshift-update_app#app_rolling)
  * Set up [a continuous delivery pipeline for a cluster](/docs/openshift?topic=openshift-cicd).
3. **Scaling**: Enable [horizontal pod autoscaling](/docs/openshift?topic=openshift-update_app#app_scaling) to automatically increase or decrease the number of instances of your apps based on CPU.

<br />


## Secure your app
{: #dev_secure}

Use Kubernetes secrets to store confidential information, such as credentials or keys, and encrypt data in Kubernetes secrets to prevent unauthorized users from accessing sensitive app information.
{: shortdesc}


1. **Secrets**: Store personal or sensitive information in [Kubernetes secrets](/docs/openshift?topic=openshift-security#pi) that your app can access.
2. **Secret encryption**: [Encrypt secrets by using a KMS provider](/docs/openshift?topic=openshift-encryption#keyprotect) and [verify that secrets are encrypted](/docs/openshift?topic=openshift-encryption#verify_kms).

<br />


## Expose your app
{: #dev_expose}

Publicly expose an app in your cluster to the internet or privately expose an app in your cluster to the private network only.
{: shortdesc}

1. **Plan service discovery**:
  1. Understand the [basics of Kubernetes service discovery](/docs/openshift?topic=openshift-plan_deploy#service_discovery).
  2. [Choose an app exposure service](/docs/openshift?topic=openshift-cs_network_planning) that fits your requirements for incoming traffic to the app.
2. **Expose your app**:
  * Load balancers:
    * Classic clusters:
        1. Create an [NLB 1.0](/docs/openshift?topic=openshift-loadbalancer) or [NLB 2.0](/docs/openshift?topic=openshift-loadbalancer-v2).
        2. [Register a DNS subdomain](/docs/openshift?topic=openshift-loadbalancer_hostname#loadbalancer_hostname) for the NLB.
    * VPC clusters: Set up a [VPC load balancer](/docs/openshift?topic=openshift-vpc-lbaas).

  * Ingress:
      * Version 4: Configure Ingress for the [public network](/docs/openshift?topic=openshift-ingress-roks4#ingress-roks4-public) or the [private network](/docs/openshift?topic=openshift-ingress-roks4#ingress-roks4-private).
      * Version 3.11 clusters: Configure Ingress for the [public network](/docs/openshift?topic=openshift-ingress#ingress_expose_public) or the [private network](/docs/openshift?topic=openshift-ingress#ingress_expose_private).

  * Routes: [Create a route to expose your app on a subdomain.](/docs/openshift?topic=openshift-openshift_routes)

</br>Need help? Check out [Troubleshooting Ingress](/docs/openshift?topic=openshift-cs_troubleshoot_debug_ingress) and [Troubleshooting load balancers](/docs/openshift?topic=openshift-cs_troubleshoot_lb).

<br />


## Add app storage
{: #dev_storage}

1. **Storage basics**: Start by understanding the [basics of Kubernetes storage](/docs/openshift?topic=openshift-kube_concepts).
2. **Requirements**: Determine your [requirements for a storage solution](/docs/openshift?topic=openshift-storage_planning).
3. **Choose a solution**: Using your storage requirements, choose a storage solution by comparing [non-persistent](/docs/openshift?topic=openshift-storage_planning#non_persistent_overview), [single-zone persistent](/docs/openshift?topic=openshift-storage_planning#single_zone_persistent_storage), or [multizone persistent](/docs/openshift?topic=openshift-storage_planning#persistent_storage_overview) storage.

</br>Need help? Check out [Troubleshooting persistent storage](/docs/openshift?topic=openshift-cs_troubleshoot_storage#cs_troubleshoot_storage).

<br />


## Add integrations
{: #dev_integrate}

Enhance app capabilities by integrating various external services and catalog services in your cluster with your app.
{: shortdesc}

1. **Review supported integrations**:
  * [All supported integrations](/docs/openshift?topic=openshift-supported_integrations#supported_integrations)
  * [Red Hat OpenShift on IBM Cloud partners](/docs/openshift?topic=openshift-service-partners)
  * [{{site.data.keyword.cloud_notm}} services and third-party integrations](/docs/openshift?topic=openshift-ibm-3rd-party-integrations)
  * [Cloud Paks](/docs/openshift?topic=openshift-openshift_cloud_paks)
  * [Operators](/docs/openshift?topic=openshift-operators)
2. **Add services to your cluster**: Ask your cluster administrator to [add the integration to your cluster](/docs/openshift?topic=openshift-learning-path-admin#admin_integrate).
3. **Access services from your app**: Ensure that your app can access the service. For example, to access an IBM Cloud service instance from your app, you must [make the service credentials that are stored in the Kubernetes secret available to your app](/docs/openshift?topic=openshift-service-binding#adding_app).

</br>Need help? Check out [Troubleshooting apps and integrations](/docs/openshift?topic=openshift-cs_troubleshoot_clusters).



