---

copyright:
  years: 2014, 2021
lastupdated: "2021-08-25"

keywords: openshift, roks, rhoks, rhos, clusters

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
  


# Creating a cluster by using a {{site.data.keyword.bpfull_notm}} template
{: #templates}

Automate the creation of a cluster in {{site.data.keyword.openshiftlong}} by using an {{site.data.keyword.bpfull_notm}} template. 
{: shortdesc}

Creating a cluster by using a template is available as a technical preview only, and isn't intended for production workloads.
{: preview}

**What do I get when I deploy the secure cluster template?**
When you create a secure cluster by using the {{site.data.keyword.bpshort}} template, you get a multizone, private-only cluster with logging and monitoring enabled as well as {{site.data.keyword.cloudaccesstraillong_notm}} and {{site.data.keyword.cos_full_notm}} instances. The secure cluster doesn't have public network access, so to access your cluster, you must [set up a VPN connection](/docs/openshift?topic=openshift-access_cluster#access_vpn_openshift). For more information and specifications, see [Resources that are created from the template](#sch-tf-resources-created).
## Resources that are created from the template
{: #sch-tf-resources-created}

When you create a cluster with the template, the following resources are created by default in your {{site.data.keyword.cloud_notm}} account, unless you customize the template.
{: shortdesc}

For more details, review the [workspace in {{site.data.keyword.bpfull_notm}}](https://cloud.ibm.com/schematics/workspaces){: external} if you created the cluster from the UI. Or, if you created the cluster from the CLI, review the [{{site.data.keyword.terraform-provider_full_notm}} template](https://github.com/terraform-ibm-modules/terraform-ibm-cluster/tree/master/examples/secure-roks-cluster){: external}.

The following resources are provisioned by default, but you can customize some of the resources, for example worker node flavor.

*   1 Virtual Private Cloud (VPC) instance with the following details:
    *   3 subnets, 1 per zone.
    *   1 security group with pre-configured rules.
*   1 {{site.data.keyword.openshiftlong_notm}} cluster with the following features:
    *   9 worker nodes of flavor type `bx2.16x64` with 16 vCPUs and 64 GB of memory that are evenly spread across the 3 zones in your VPC.
    *   1 default worker pool with 3 worker nodes per zone across 3 zones.
*   1 {{site.data.keyword.loganalysislong_notm}} instance to enable logging from the cluster.
*   1 {{site.data.keyword.cloudaccesstraillong_notm}} instance to enable audit logs from the cluster, such as when a user creates a call against the {{site.data.keyword.openshiftlong_notm}} API.
*   1 {{site.data.keyword.monitoringlong_notm}} instance to enable metrics such as node usage from the cluster.
*   1 {{site.data.keyword.keymanagementservicelong_notm}} instance and customer root key (CRK) to encrypt the cluster master, including Kubernetes secrets in the cluster.
*   1 {{site.data.keyword.cos_full_notm}} instance and bucket to back up certain [cluster data](/docs/containers?topic=containers-service-arch#ibm-data). You cannot select your own instance.


## Creating a secure cluster by using a template from the UI
{: #sch-secure-cluster-ui}
{: ui}

With the secure cluster template, you can create a cluster from the UI with {{site.data.keyword.bpfull_notm}} that already includes certain security integrations such as encryption, logging, and monitoring enabled by default.
{: shortdesc}

1. Log in to the [{{site.data.keyword.openshiftshort}} clusters console](https://cloud.ibm.com/kubernetes/clusters?platformType=openshift){: external} and click **Create cluster +**.
2. From the **Create** tab in the **Select your template** section, click **Secure**.
3. Review the pre-configured details for the secure template, including the following sections. To change these values, click **Edit**. When you are finished, click **Done editing** to apply your changes.
    - **Location**: Review the resource group and {{site.data.keyword.cloud_notm}} multizone location where the cluster is created.
    - **Orchestration service**: Review the container platform, version, and entitlement details.

        For the **OCP entitlement**, you can select an entitlement for a worker pool, if you have one. In most cases, leave the value set to **Purchase additional licenses for this worker pool**. If you have an {{site.data.keyword.cloud_notm}} Pak with an {{site.data.keyword.openshiftshort}} entitlement that you want to use, you can select **Apply my Cloud Pak OCP entitlement to this worker pool**. Later, when you configure the worker pool, make sure to select only the flavor and number of worker nodes that your entitlement permits.
        {: note}
    - **VPC**: Review the subnet IP range for your location. 

    - **Resource details**: Review the resource prefix that is automatically added to each {{site.data.keyword.cloud_notm}} resource that is created. You can also optionally provide your own {{site.data.keyword.cloud_notm}} IAM API key if you do not need a new API key generated for you.
    - **Integrations**: A new instance of each of the following {{site.data.keyword.cloud_notm}} services is created for you by default. You can edit the template to select an existing instance.
4. In the **Summary** pane, click **Create**.

## Creating a secure cluster by using a template with the CLI
{: #tf-secure-cluster-cli}
{: cli}

With the secure cluster template, you can create a cluster from the CLI with {{site.data.keyword.terraform-provider_full_notm}} that already has certain security integrations such as encryption, logging, and monitoring enabled by default.
{: shortdesc}

**Before you begin**:
1. [Install the {{site.data.keyword.terraform-provider_full_notm}} CLI](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-setup_cli).
2. [Configure the {{site.data.keyword.terraform-provider_full_notm}}](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-reference).
3. [Access your {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-access_cluster).

**Creating a secure cluster from an {{site.data.keyword.terraform-provider_full_notm}} template in the CLI**:

1. Clone the [GitHub repository for {{site.data.keyword.terraform-provider_full_notm}} modules](https://github.com/terraform-ibm-modules/terraform-ibm-cluster/){: external}.
    ```bash
    git@github.com:terraform-ibm-modules/terraform-ibm-cluster.git
    ```
    {: pre}

2. Go to the `examples/secure-roks-cluster` directory, and review the [`README.md` file](https://github.com/terraform-ibm-modules/terraform-ibm-cluster/tree/master/examples/secure-roks-cluster){: external} for more information about how to update any of the template default variables.
3. Run the Terraform commands to initialize, plan, and apply the template. You can monitor the progress from the command line.
    ```bash
    terraform init
    ```
    {: pre}

    ```bash
    terraform plan
    ```
    {: pre}

    ```bash
    terraform apply
    ```
    {: pre}

4. **Optional**: To clean up the resources that the template created, you can use a Terraform command.
    ```bash
    terraform destroy
    ```
    {: pre}



## Next steps
{: #sch-tf-whats-next}

The {{site.data.keyword.bpshort}} template helps with the initial creation. After creating the cluster, you are in control for continued cluster management actions, such as [updating the cluster](/docs/containers?topic=containers-update), [adding worker nodes](/docs/containers?topic=containers-add_workers), updating any of your VPC network options, and using the security integrations to monitor your cluster.
{: shortdesc} 

To fully [remove](/docs/containers?topic=containers-remove) your cluster and the resources created by the secure cluster template, make sure to [destroy your workspace in {{site.data.keyword.bpshort}}](/docs/schematics?topic=schematics-workspace-setup#del-workspace). Removing the cluster and not removing the workspace in {{site.data.keyword.bpshort}} doesn't remove all the resources this template deploys.







