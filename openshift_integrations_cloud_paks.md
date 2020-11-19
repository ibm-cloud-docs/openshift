---

copyright:
  years: 2014, 2020
lastupdated: "2020-11-19"

keywords: openshift, roks, rhoks, rhos, cloud pak, cloud pack, cloudpak, cloudpack, icp, cloud paks, cloudpaks, cloud packs, cloudpacks, icd, icp4d, icpa, icp4a

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
{:authenticated-content: .authenticated-content}
{:beta: .beta}
{:c#: data-hd-programlang="c#"}
{:cli: .ph data-hd-interface='cli'}
{:codeblock: .codeblock}
{:curl: .ph data-hd-programlang='curl'}
{:deprecated: .deprecated}
{:dotnet-standard: .ph data-hd-programlang='dotnet-standard'}
{:download: .download}
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
{:java: .ph data-hd-programlang='java'}
{:java: data-hd-programlang="java"}
{:javascript: .ph data-hd-programlang='javascript'}
{:javascript: data-hd-programlang="javascript"}
{:new_window: target="_blank"}
{:note .note}
{:note: .note}
{:objectc data-hd-programlang="objectc"}
{:org_name: data-hd-keyref="org_name"}
{:php: data-hd-programlang="php"}
{:pre: .pre}
{:preview: .preview}
{:python: .ph data-hd-programlang='python'}
{:python: data-hd-programlang="python"}
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
{:subsection: outputclass="subsection"}
{:support: data-reuse='support'}
{:swift: .ph data-hd-programlang='swift'}
{:swift: data-hd-programlang="swift"}
{:table: .aria-labeledby="caption"}
{:term: .term}
{:tip: .tip}
{:tooling-url: data-tooling-url-placeholder='tooling-url'}
{:troubleshoot: data-hd-content-type='troubleshoot'}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:tsSymptoms: .tsSymptoms}
{:tutorial: data-hd-content-type='tutorial'}
{:ui: .ph data-hd-interface='ui'}
{:unity: .ph data-hd-programlang='unity'}
{:url: data-credential-placeholder='url'}
{:user_ID: data-hd-keyref="user_ID"}
{:vb.net: .ph data-hd-programlang='vb.net'}
{:video: .video}



# Adding Cloud Paks
{: #openshift_cloud_paks}

[IBM Cloud Paks&trade;](https://www.ibm.com/cloud/paks/){: external} are containerized, licensed IBM middleware and open source software components that you can use to modernize, move, and build cloud-native business applications in hybrid and multicloud deployments. By running exclusively on {{site.data.keyword.openshiftshort}} and Red Hat Enterprise Linux, Cloud Paks are built atop a secure stack and maintain consistency in deployment and behavior across cloud providers. You have greater flexibility to run and manage your workloads securely where you need them: on-premises, off-premises, in a backup provider, and in {{site.data.keyword.cloud_notm}}.
{: shortdesc}

## Overview of Cloud Pak offerings
{: #oc_cloud_pak_ov}

You can deploy the entire set of Cloud Paks to manage your full-stack cloud apps, data, integration, automation, and management across {{site.data.keyword.openshiftshort}} cloud providers.
{: shortdesc}

| Area | Description |
| ---- | ------------ |
| Use cases | <ul><li>Run existing apps in traditional environments such as {{site.data.keyword.appserver_short}}.</li><li>Modernize existing apps to newer runtimes at your own pace.</li><li>Build new, cloud-native apps by using portable, open source software.</li></ul>  |
| [Catalog entry](https://cloud.ibm.com/catalog/content/ibm-cp-applications#about){: external} | For included components, require cluster size, and installation. |
| [Documentation](/docs/cloud-pak-applications?topic=cloud-pak-applications-getting-started){: external} | For more information such as postinstallation tasks and pricing. |
{: summary="The rows are read from left to right. The area of comparing the different Cloud Paks is in the first column, with the information for the Cloud Pak in the second column. You can change Cloud Paks by toggling the tabs at the beginning of the table."}
{: class="simple-tab-table"}
{: caption="Cloud Pak for Applications" caption-side="top"}
{: #cloudpak1}
{: tab-title="Applications"}
{: tab-group="cloudpak"}

| Area | Description |
| ---- | ------------ |
| Use cases | <ul><li>Set up an end-to-end platform to collect, organize, and analyze your data.</li><li>Create interactive data visualizations and analyze information for insights across data sets, without needing to code.</li><li>Operationalize your data with AI and a suite of governance tools to make sure that your data is curated, useful, trusted, and ready for analysis.</li></ul> |
| [Catalog entry](https://cloud.ibm.com/catalog/content/ibm-cp-data#about){: external} | For included components, require cluster size, and installation. |
| [Documentation](https://www.ibm.com/support/knowledgecenter/en/SSQNUZ){: external} | For more information such as postinstallation tasks and pricing. | |
{: summary="The rows are read from left to right. The area of comparing the different Cloud Paks is in the first column, with the information for the Cloud Pak in the second column. You can change Cloud Paks by toggling the tabs at the beginning of the table."}
{: class="simple-tab-table"}
{: caption="Cloud Pak for Data" caption-side="top"}
{: #cloudpak2}
{: tab-title="Data"}
{: tab-group="cloudpak"}

| Area | Description |
| ---- | ------------ |
| Use cases | <ul><li>Integrate workflows, APIs, logging, and events across multiple cloud environments, all from a unified platform.</li><li>Rapidly and securely transfer data across hybrid cloud environments.</li><li>Set up a multichannel gateway to expand and control access to the full range of your mobile, web app, API, SOA, B2B, and other cloud workloads.</li></ul>  |
| [Catalog entry](https://cloud.ibm.com/catalog/content/ibm-cp-integration#about){: external} | For included components, require cluster size, and installation. |
| [Documentation](https://www.ibm.com/support/knowledgecenter/en/SSGT7J){: external} | For more information such as postinstallation tasks and pricing. |
{: summary="The rows are read from left to right. The area of comparing the different Cloud Paks is in the first column, with the information for the Cloud Pak in the second column. You can change Cloud Paks by toggling the tabs at the beginning of the table."}
{: class="simple-tab-table"}
{: caption="Cloud Pak for Integration" caption-side="top"}
{: #cloudpak3}
{: tab-title="Integration"}
{: tab-group="cloudpak"}

| Area | Description |
| ---- | ------------ |
| Use cases | <ul><li>Digitize business operations and extend your workforce with digital labor.</li><li>Control and synchronize enterprise content servers and management systems across multiple channels, devices, and mobile environments.</li><li>Automate and visualize thousands of policies, decisions, and other business rules.</li></ul>  |
| [Catalog entry](https://cloud.ibm.com/catalog/content/ibm-cp-automation#about){: external} | For included components, require cluster size, and installation. |
| [Documentation](https://www.ibm.com/support/knowledgecenter/en/SSYHZ8_19.0.x/welcome/kc_welcome_dba_distrib.html){: external} | For more information such as postinstallation tasks and pricing. |
{: summary="The rows are read from left to right. The area of comparing the different Cloud Paks is in the first column, with the information for the Cloud Pak in the second column. You can change Cloud Paks by toggling the tabs at the beginning of the table."}
{: class="simple-tab-table"}
{: caption="Cloud Pak for Automation" caption-side="top"}
{: #cloudpak4}
{: tab-title="Automation"}
{: tab-group="cloudpak"}

| Area | Description |
| ---- | ------------ |
| Use cases | <ul><li>Consistently and securely manage your apps that are deployed in Kubernetes and {{site.data.keyword.openshiftshort}} clusters across multiple cloud providers.</li><li>Consolidate event monitoring information across clusters in off-prem and on-prem clouds.</li><li>Optimize workflows with automatic provisioning of virtual machines and other infrastructure resources across clouds providers.</li></ul> |
| [Catalog entry](https://cloud.ibm.com/catalog/content/ibm-cp-management#about){: external} | For included components, require cluster size, and installation. |
| [Documentation](https://www.ibm.com/support/knowledgecenter/SSFC4F/product_welcome_cloud_pak.html){: external} | For more information such as postinstallation tasks and pricing. |
{: summary="The rows are read from left to right. The area of comparing the different Cloud Paks is in the first column, with the information for the Cloud Pak in the second column. You can change Cloud Paks by toggling the tabs at the beginning of the table."}
{: class="simple-tab-table"}
{: caption="Cloud Pak for Management" caption-side="top"}
{: #cloudpak5}
{: tab-title="Management"}
{: tab-group="cloudpak"}

<br />

## Adding IBM Cloud Paks
{: #oc_cloud_paks_add}
{: help}
{: support}

[IBM Cloud Paks](https://www.ibm.com/cloud/paks/){: external} are containerized, licensed IBM middleware and open source software components as part of your hybrid cloud solution. IBM Cloud Paks run exclusively on {{site.data.keyword.openshiftshort}} clusters, not community Kubernetes clusters.
{: shortdesc}



Before you begin:
* Verify that your account administrator [set up your {{site.data.keyword.cloud_notm}} account with the Cloud Pak entitlement](#oc_cloud_paks_assign).
* Make sure that you have the [required permissions to create a cluster](/docs/openshift?topic=openshift-clusters#cluster_prepare). These permissions include the following:
  * The IAM **Administrator** platform role for {{site.data.keyword.containershort}}.
  * The IAM **Administrator** platform role for {{site.data.keyword.registryshort}}.
  * The IAM **Viewer** platform role for the resource group if you create the cluster in a resource group other than `default`.
  * The appropriate infrastructure permissions, such as an API key with the **Super User** role for classic infrastructure.

To add a Cloud Pak from the {{site.data.keyword.cloud_notm}} catalog:

1.  Add your Cloud Pak entitlement from [IBM Passport Advantage](https://www.ibm.com/software/passportadvantage/index.html){: external} to your {{site.data.keyword.openshiftlong_notm}} cluster.
    *  **For new clusters**: [Create a cluster](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_cluster_create) with the `--entitlement cloud_pak` option. When you specify the number of workers (`--workers`) and flavor (`--flavor`), make sure to specify only the number and size of worker nodes that you are entitled to use. After your cluster is created, you are not charged the {{site.data.keyword.openshiftshort}} license fee for the entitled worker nodes in the `default` worker pool. If you want to use a different worker pool for your Cloud Pak, follow the steps for existing clusters.
    * **For existing clusters or worker pools other than `default`**: Create a [worker pool](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_pool_create) with the `--entitlement cloud_pak` option. When you specify the number of workers (`--size-per-zone`) and flavor (`--flavor`), make sure to specify only the number and size of worker nodes that you are entitled to use. After creation, your worker pool does not charge you the {{site.data.keyword.openshiftshort}} license fee for your entitled worker nodes.

    Do not exceed your entitlement. Keep in mind that your OpenShift Container Platform entitlements can be used with other cloud providers or in other environments. To avoid billing issues later, make sure that you use only what you are entitled to use. For example, you might have an entitlement for the OCP licenses for two worker nodes of 4 CPU and 16 GB memory, and you create this worker pool with two worker nodes of 4 CPU and 16 GB memory. You used your entire entitlement, and you cannot use the same entitlement for other worker pools, cloud providers, or environments.
    {: important}

2. In the [{{site.data.keyword.cloud_notm}} catalog](https://cloud.ibm.com/catalog?search=label%3Acloud_pak#software){: external}, in the **Software** tab, under **Offering Type**, check **Cloud Paks**.
3. Select the Cloud Pak that you want to deploy, and follow the installation instructions. Each Cloud Pak requires an entitlement from [IBM Passport Advantage](https://www.ibm.com/software/passportadvantage/){: external}, and has its own configuration settings. For more information, view the **About** tab and Cloud Pak documentation.



Now you can run your Cloud Pak on your {{site.data.keyword.openshiftshort}} cluster!

<br />

## Assigning a Cloud Pak entitlement to your {{site.data.keyword.cloud_notm}} account
{: #oc_cloud_paks_assign}

To deploy a Cloud Pak to your {{site.data.keyword.openshiftlong_notm}} cluster, your entitlement to the Cloud Pak must be assigned to your {{site.data.keyword.cloud_notm}} account.
{: shortdesc}

1.  Verify that your {{site.data.keyword.cloud_notm}} account ID matches your IBM Passport Advantage ID.
    1.  Get your {{site.data.keyword.cloud_notm}} account ID.
        1.  Log in to [{{site.data.keyword.cloud_notm}}](https://cloud.ibm.com/){: external}.
        2.  From the menu bar, click **Manage > Account**.
        3.  From the navigation pane, click **Account Settings**, and note your **ID**, such as `1aa111aa1a11111aaa1a1111aa1aa111`.
    2.  Log in to [IBM Passport Advantage](https://www.ibm.com/software/passportadvantage/){: external} and check your account ID.
    3.  Compare the IDs. If the IDs do not match, try using a different {{site.data.keyword.cloud_notm}} or IBM Passport Advantage account that match. If you cannot find matching IDs, contact [eCustomer care](https://www-112.ibm.com/software/howtobuy/passportadvantage/homepage/ecarec){: external}.
2.  Make sure that the account owner gives you permission to assign entitlements.
    1.  From the [{{site.data.keyword.cloud_notm}} console](https://cloud.ibm.com/){: external} menu bar, click **Manage > Access (IAM)**.
    2.  From the **Users** tab, click the user that you want to assign permissions.
    3.  Click **Access policies > Assign access +**.
    4.  Click **Account management**.
    5.  From the **What type of access do you want to assign?** drop-down menu, select **License and Entitlement**.
    6.  Select at least the **Editor** platform role, then click **Add**.
3.  Assign the Cloud Pak license to your {{site.data.keyword.cloud_notm}} account.  
    1.  From the [{{site.data.keyword.cloud_notm}} software catalog](https://cloud.ibm.com/catalog#software){: external}, find the Cloud Pak that you want to assign.
    2.  From the **Create > Assign a license** section, select the license that you want to use and click **Assign**.
4.  Continue to [create the Cloud Pak instance](#oc_cloud_paks_add).

<br />

## FAQs for Cloud Pak on {{site.data.keyword.openshiftlong_notm}}
{: #faq_cloud_paks}

Review frequently asked questions for IBM Cloud Paks on {{site.data.keyword.openshiftlong_notm}} clusters. For questions about Cloud Paks that run on other distributions such as on-premises, {{site.data.keyword.openshiftshort}} Dedicated, or OpenShift Container Platform on different cloud providers, consult those cloud providers' documentation.
{: shortdesc}

### How do I install a Cloud Pak in my {{site.data.keyword.openshiftlong_notm}} cluster? How do I access it later?
{: #cloud_pak_manage}

Cloud Paks are integrated with the {{site.data.keyword.cloud_notm}} catalog so that you can quickly configure and install the all the Cloud Pak components into an existing or new {{site.data.keyword.openshiftshort}} cluster. When you install the Cloud Pak, the Cloud Pak is provisioned with [{{site.data.keyword.bpshort}}](/docs/schematics?topic=schematics-about-schematics) and a {{site.data.keyword.bpshort}} workspace is created for you. You can use the workspace later to access information about your Cloud Pak installation. You access your Cloud Pak services from the Cloud Pak URL. For more information, consult each [Cloud Pak's documentation](#oc_cloud_pak_ov).

### Can I use the {{site.data.keyword.openshiftshort}} entitlement that comes with my Cloud Pak for my cluster?
{: #cloud_pak_byo_entitlement}

Yes, if your Cloud Pak includes an entitlement to run certain worker node flavors that are installed with OpenShift Container Platform. To view your entitlements, check in [IBM Passport Advantage](https://www.ibm.com/software/passportadvantage/index.html){: external}. Note that your {{site.data.keyword.cloud_notm}} ID must match your IBM Passport Advantage ID.

You can create the cluster or the worker pool within an existing cluster with the Cloud Pak entitlement by using the `--entitlement cloud_pak` option in the [`ibmcloud oc cluster create classic`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_cluster_create) or [`ibmcloud oc worker-pool create classic`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_pool_create) CLI commands. Make sure to specify the correct number and flavor of worker nodes that you are entitled to use.

Do not exceed your entitlement. Keep in mind that your OpenShift Container Platform entitlements can be used with other cloud providers or in other environments. To avoid billing issues later, make sure that you use only what you are entitled to use. For example, you might have an entitlement for the OCP licenses for two worker nodes of 4 CPU and 16 GB memory, and you create this worker pool with two worker nodes of 4 CPU and 16 GB memory. You used your entire entitlement, and you cannot use the same entitlement for other worker pools, cloud providers, or environments.
{: important}



### What is included in a Cloud Pak?
{: #cloud_pak_included}

Cloud Paks are bundled, licensed, containerized software that is optimized to work together for enterprise use cases, including consistent deployment, access control, and billing. You can flexibly use parts of the Cloud Paks when you need them by choosing the right mix of virtual processor cores of the software to suit your workloads. You can also change the mix of virtual processor cores as your workloads evolve.
{: shortdesc}

Depending on the Cloud Pak, you get licensed IBM and open source software bundled together in a unified management experience with logging, monitoring, security, and access capabilities.
* **IBM products**: Cloud Paks extend licensed IBM software and middleware from [IBM Marketplace](https://www.ibm.com/products){: external}, and integrate these products with your cluster to modernize, optimize, and run hybrid cloud workloads.
* **Open-source software**: Cloud Paks might also include open source components for cloud-native and portable hybrid cloud solutions. Typically, open source software is unmanaged and you are responsible to keep your components up-to-date and secure. However, Cloud Paks help you consistently manage the entire lifecycle of the Cloud Pak components and the workloads that you run with them. Because the open source software is bundled together with the Cloud Pak, you get the benefits of IBM support and integration with select {{site.data.keyword.cloud_notm}} features such as billing.

To see the components of each Cloud Pak, consult the [Cloud Pak's documentation](#oc_cloud_pak_ov).

### What else do I need to know to use Cloud Paks?
{: #cloud_paks_other}

When you set up your Cloud Pak, you might need to work with {{site.data.keyword.openshiftshort}}-specific resources, such as security context constraints. Make sure that you use the [`oc` CLI or `kubectl` version 1.12 CLI](/docs/openshift?topic=openshift-openshift-cli#cli_oc) to interact with these resources, such as `oc get scc`. The `kubectl` CLI version 1.11 has a bug that yields an error when you run commands against {{site.data.keyword.openshiftshort}}-specific resources, such as `kubectl get scc`.
{: shortdesc}
