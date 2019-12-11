---

copyright:
  years: 2014, 2019
lastupdated: "2019-12-11"

keywords: openshift, roks, rhoks, rhos, cloud pak, cloud pack, cloudpak, cloudpack, icp, cloud paks, cloudpaks, cloud packs, cloudpacks, icd, icp4d, icpa, icp4a

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
{:important: .important}
{:download: .download}
{:preview: .preview} 
{:external: target="_blank" .external}

# Adding Cloud Paks
{: #openshift_cloud_paks}

[IBM Cloud Paks&trade; ![External link icon](../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/cloud/paks/) are containerized, licensed IBM middleware and open source software components that you can use to modernize, move, and build cloud-native business applications in hybrid and multicloud deployments. By running exclusively on OpenShift and Red Hat Enterprise Linux, Cloud Paks are built atop a secure stack and maintain consistency in deployment and behavior across cloud providers. You have greater flexibility to run and manage your workloads securely where you need them: on-premises, off-premises, in a backup provider, and in {{site.data.keyword.cloud_notm}}.
{: shortdesc}

## Overview of Cloud Pak offerings
{: #oc_cloud_pak_ov}

You can deploy the entire set of Cloud Paks to manage your full-stack cloud apps, data, integration, automation, and management across OpenShift cloud providers.
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
| Use cases | <ul><li>Consistently and securely manage your apps that are deployed in Kubernetes and OpenShift clusters across multiple cloud providers.</li><li>Consolidate event monitoring information across clusters in off-prem and on-prem clouds.</li><li>Optimize workflows with automatic provisioning of virtual machines and other infrastructure resources across clouds providers.</li></ul> |
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

[IBM Cloud Paks ![External link icon](../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/cloud/paks/) are containerized, licensed IBM middleware and open source software components as part of your hybrid cloud solution. IBM Cloud Paks run exclusively on OpenShift clusters, not community Kubernetes clusters.
{: shortdesc}



1. In the [{{site.data.keyword.cloud_notm}} catalog ![External link icon](../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/catalog?search=label%3Acloud-paks), under **Offering Type**, check **Cloud Paks**.
2. Select the Cloud Pak that you want to deploy, and follow the installation instructions. Each Cloud Pak requires an entitlement from [IBM Passport Advantage ![External link icon](../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/software/passportadvantage/), and has its own configuration settings. For more information, view the **About** tab and Cloud Pak documentation.



Now you can run your Cloud Pak on your OpenShift cluster! 

<br />


## FAQs for Cloud Pak on Red Hat OpenShift on IBM Cloud
{: #faq_cloud_paks}

Review frequently asked questions for [IBM Cloud Paks ![External link icon](../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/cloud/paks/) on Red Hat OpenShift on IBM Cloud clusters. For questions about Cloud Paks that run on other distributions such as on-premises, OpenShift Dedicated, or OpenShift Container Platform on different cloud providers, consult those cloud providers' documentation.
{: shortdesc}

### How do I install a Cloud Pak in my Red Hat OpenShift on IBM Cloud cluster? How do I access it later?
{: #cloud_pak_manage}

Cloud Paks are integrated with the {{site.data.keyword.cloud_notm}} catalog so that you can quickly configure and install the all the Cloud Pak components into an existing or new OpenShift cluster. When you install the Cloud Pak, the Cloud Pak is provisioned with [{{site.data.keyword.bpshort}}](/docs/schematics?topic=schematics-about-schematics) and a {{site.data.keyword.bpshort}} workspace is created for you. You can use the workspace later to access information about your Cloud Pak installation. You access your Cloud Pak services from the Cloud Pak URL. For more information, consult each [Cloud Pak's documentation](#oc_cloud_pak_ov).

### Can I use the OpenShift entitlement that comes with my Cloud Pak for my cluster?
{: #cloud_pak_byo_entitlement}

Yes, if your Cloud Pak includes an entitlement to run certain worker node flavors that are installed with OpenShift Container Platform. To view your entitlements, check in [IBM Passport Advantage](https://www.ibm.com/software/passportadvantage/index.html){: external}. 

You can create the cluster or the worker pool within an existing cluster with the Cloud Pak entitlement by using the `--entitlement cloud_pak` option in the [`ibmcloud oc cluster create classic`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_cluster_create) or [`ibmcloud oc worker-pool create classic`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_pool_create) CLI commands. Make sure to specify the correct number and flavor of worker nodes that you are entitled to use.



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

When you set up your Cloud Pak, you might need to work with OpenShift-specific resources, such as security context constraints. Make sure that you use the [`oc` CLI or `kubectl` version 1.12 CLI](/docs/openshift?topic=openshift-openshift-cli#cli_oc) to interact with these resources, such as `oc get scc`. The `kubectl` CLI version 1.11 has a bug that yields an error when you run commands against OpenShift-specific resources, such as `kubectl get scc`.
{: shortdesc}
