---

copyright:
  years: 2014, 2021
lastupdated: "2021-09-09"

keywords: red hat openshift, red hat openshift on ibm cloud, openshift container platform, red hat, create openshift cluster, openshift vpc cluster, openshift classic cluster, red hat cluster, openshift, containers, clusters, roks, rhoks, rhos

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
{:release-note: data-hd-content-type='release-note'}
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
{:video: .video}
{:video: .video} -->
{{site.data.keyword.attribute-definition-list}}
  

{[css-tiles.html]}

# Getting started with {{site.data.keyword.openshiftlong_notm}}
{: #getting-started}

With {{site.data.keyword.openshiftlong_notm}}, you can deploy apps on highly available {{site.data.keyword.openshiftshort}} clusters that run the [{{site.data.keyword.openshiftlong_notm}} Container Platform](https://docs.openshift.com/container-platform/4.6/welcome/index.html){: external} software on Red Hat Enterprise Linux machines.
{: shortdesc}

First, create a classic {{site.data.keyword.openshiftlong}} cluster or a cluster on the second generation of compute infrastructure in a Virtual Private Cloud (VPC). Then, deploy and expose a sample app in your cluster.
<br>

To complete the getting started tutorial, use a [Pay-As-You-Go or Subscription {{site.data.keyword.containerlong}} account](/docs/account?topic=account-upgrading-account) where you are the owner or have [full Administrator access](/docs/account?topic=account-assign-access-resources).
{: note}

<div class=solutionBoxContainer>
    <div class="solutionBox">
    <a href = "#clusters_gs">
    <div>
            <p><strong><img src="images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Create a classic cluster</strong></p>
            <p class="bx--type-caption">Create an {{site.data.keyword.openshiftshort}} cluster on {{site.data.keyword.cloud_notm}} classic workers nodes, subnets, and VLAN networking. Choose from a variety of virtual, bare metal, or software-defined storage flavors.</p>
    </div>
    </a>
    </div>
    <div class="solutionBox">
        <a href = "#vpc-gen2-gs">
        <div>
            <p><strong><img src="images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Create a VPC cluster</strong></p>
            <p class="bx--type-caption">Create your cluster on the second generation of compute resources in a Virtual Private Cloud (VPC) that gives you the security of a private cloud with the scalability of a public cloud.</p>
        </div>
    </a>
    </div>
    <div class="solutionBox">
    <a href = "#deploy-app">
    <div>
            <p><strong><img src="images/icon-containers-bw.svg" alt="{{site.data.keyword.openshiftshort}} Container icon" width="15" style="width:15px; border-style: none"/> Deploy and expose an app</strong></p>
            <p class="bx--type-caption">In your {{site.data.keyword.openshiftshort}} cluster, deploy a sample app from a container image that is stored in Docker Hub. Then, expose it with a router to get an IP address for quick testing of your first app.</p>
    </div>
    </a>
    </div>
</div>



## Creating a classic {{site.data.keyword.openshiftshort}} cluster
{: #clusters_gs}

<img src="images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Create a {{site.data.keyword.openshiftlong_notm}} cluster on classic {{site.data.keyword.cloud_notm}} infrastructure in the {{site.data.keyword.cloud_notm}} console. To get started, create a cluster that runs OpenShift Container Platform version 4.6. The operating system is Red Hat Enterprise Linux 7.
{: shortdesc}

Want to learn more about customizing your cluster setup with the CLI? Check out [Creating an {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-clusters).
{: tip}

1. Log in to your [{{site.data.keyword.cloud_notm}} account](https://cloud.ibm.com/){: external}.
2. From the **Catalog**, click [**{{site.data.keyword.openshiftlong_notm}}**](https://cloud.ibm.com/kubernetes/catalog/about?platformType=openshift){: external}.
3. Review the platform version details, **{{site.data.keyword.openshiftshort}} 4.6.28**.
4. If you see the **OCP entitlement** section: Leave the value set to **Purchase additional licenses for this worker pool** because you are not using an {{site.data.keyword.cloud_notm}} Pak for this getting started cluster.
5. For the **Infrastructure**, select **Classic**.
6. Configure the **Location** details for your cluster.
    1. Select the **Resource group** that you want to create your cluster in. You cannot change the resource group later. If you do not select a resource group, your cluster is created in the default resource group.
    2. Select a **Geography** to create the cluster in, such as **North America**. The geography helps filter the **Availability** and **Data centers** values that you can select.
    3. Select the **Availability** that you want for your cluster, such as **Single zone**.
    4. Select the **Worker zone** to create your cluster in, such as **Dallas 10**.
7. Configure your **Worker pool** setup.
    1. If you want a larger size for your worker nodes, click **Change flavor**. Otherwise, leave the default **4 vCPUs / 16 GB** flavor selected.
    2. Set how many worker nodes to create per zone, such as the minimum value of **2**. For more information, see [What is the smallest size cluster that I can make?](/docs/openshift?topic=openshift-faqs#smallest_cluster).
8. Complete the **Resource details** to customize the cluster name and any tags that you want to use to organize your {{site.data.keyword.cloud_notm}} resources.
9. In the **Summary** pane, review the order summary and then click **Create**.<p class="note">Your cluster creation might take some time to complete. After the cluster state shows **Normal**, the cluster network and load balancing components take about 10 more minutes to deploy and update the cluster domain that you use for the {{site.data.keyword.openshiftshort}} web console and other routes. Before you continue, wait until the cluster is ready by checking that the **Ingress Subdomain** follows a pattern of `<cluster_name>.<globally_unique_account_HASH>-0001.<region>.containers.appdomain.cloud`.</p>
10. Verify that your cluster setup is finished before you continue to the next step by checking that the worker nodes on the **Worker Nodes** tab have a **Status** of normal.

Now that your cluster is ready, [deploying your first app](#deploy-app)!





## Creating a VPC cluster
{: #vpc-gen2-gs}

<img src="images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Create a VPC cluster by using the {{site.data.keyword.cloud_notm}} console. VPC {{site.data.keyword.openshiftshort}} clusters run version 4.6, which includes Kubernetes version 1.19. The operating system is Red Hat Enterprise Linux 7.
{: shortdesc}

Want to learn more about customizing your cluster setup with the CLI? Check out [Creating a VPC cluster](/docs/openshift?topic=openshift-clusters#clusters_vpcg2).
{: tip}

1. Create a Virtual Private Cloud (VPC) on generation 2 compute.
    1. Navigate to the [VPC create console](https://cloud.ibm.com/vpc/provision/vpc){: external}.
    3. Give the VPC a name and select a resource group to deploy the VPC into.
    4. Give the VPC subnet a name and select the location where you want to create the cluster.
    5. Attach a public gateway to your subnet so that you can access public endpoints from your cluster. This public gateway is used later on to access default {{site.data.keyword.openshiftshort}} components like the web console, OperatorHub, and service catalog.
    6. Click **Create virtual private cloud**.
2. From the [{{site.data.keyword.openshiftlong_notm}} dashboard](https://cloud.ibm.com/kubernetes/landing?platformType=openshift){: external}, click **Create cluster**.
3. Configure your cluster's VPC environment.
    1. Review the platform version details, **{{site.data.keyword.openshiftshort}} 4.6.28**.
    2. If you see the **OCP entitlement** section: Leave the value set to **Purchase additional licenses for this worker pool** because you are not using an {{site.data.keyword.cloud_notm}} Pak for this getting started cluster.
    3. For the **Infrastructure**, select **VPC**.
    4. From the **Virtual private cloud** drop-down menu, select the VPC that you created earlier.
    5. From the **Cloud Object Storage** drop-down menu, select a standard {{site.data.keyword.cos_full_notm}} instance to use for the internal {{site.data.keyword.openshiftshort}} container registry, or [create a standard {{site.data.keyword.cos_full_notm}} instance](/docs/cloud-object-storage/basics?topic=cloud-object-storage-provision#provision-instance) to use.
4. Configure the **Location** details for your cluster.
    1. Select the **Resource group** that you want to create your cluster in. You cannot change the resource group later. If you do not select a resource group, your cluster is created in the default resource group.
    2. Select the zones to create your cluster in. The zones are filtered based on the VPC that you selected, and include the subnets that you previously created.
5. Configure your **Worker pool** setup.
    1. If you want a larger size for your worker nodes, click **Change flavor**. Otherwise, leave the default **4 vCPUs / 16 GB** flavor selected.
    2. Set how many worker nodes to create per zone, such as the minimum value of **2**. For more information, see [What is the smallest size cluster that I can make?](/docs/openshift?topic=openshift-faqs#smallest_cluster).
6. Complete the **Resource details** to customize the cluster name and any tags that you want to use to organize your {{site.data.keyword.cloud_notm}} resources.
7. In the **Summary** pane, review the order summary and then click **Create**.<p class="note">Your cluster creation might take some time to complete. After the cluster state shows **Normal**, the cluster network and load balancing components take about 10 more minutes to deploy and update the cluster domain that you use for the {{site.data.keyword.openshiftshort}} web console and other routes. Before you continue, wait until the cluster is ready by checking that the **Ingress Subdomain** follows a pattern of `<cluster_name>.<globally_unique_account_HASH>-0001.<region>.containers.appdomain.cloud`.



The worker node can take a few minutes to provision, but you can see the progress in the **Worker nodes** tab. When the status reaches `Ready`, you can start working with your cluster by [deploying your first app](#deploy-app)!



## Deploying an app with the {{site.data.keyword.openshiftshort}} service catalog
{: #deploy-app}

From the {{site.data.keyword.openshiftshort}} console, you can deploy one of the built-in service catalog apps and expose the app with a route.
{: shortdesc}

1. From the cluster details page, click **OpenShift web console**.
2. From the side navigation menu in the **Administrator** perspective, click **Home > Projects** and then click **Create Project**. Enter a name for your project, and click **Create**. Now that your project is created by the administrator, you can switch to the Developer perspective to create an app.
3. From the side navigation menu, select **Developer** from the perspective switcher.
4. Click **+Add**. From the **Add** pane menu bar, make sure that the **Project** is the one that you just created.
5. Click **From Catalog**. The **Developer Catalog** opens in the pane.
6. From the navigation menu in the pane, click **Languages > JavaScript**.
7. Click **Node.js**, and then click **Create Application**. Note that you might need to click **Clear All Filters** to display the **Node.js** option. After you select **Node.js**, the **Create Source-to-Image Application** pane opens.
8. In the **Git** section, click **Try Sample**.
9. Scroll to confirm that **Deployment** and **Create a route to the application** are selected, and then click **Create**.
8. Wait a few minutes for the pods to deploy. To check the status of the pods, from the **Topology** pane, click your **`nodejs`** app and review its sidebar. You must see that the `nodejs` build is complete, and that the `nodejs` pod is in a **Running** state to continue.
9. When the deployment is complete, click the route location URL, which has a format similar to the following.

    ```
    http://nodejs-<project>.<cluster_name>-<hash>.<region>.containers.appdomain.cloud
    ```
    {: screen}

    A new tab in your browser opens with a message similar to the following.
    ```
    Welcome to your Node.js application on OpenShift
    ```
    {: screen}

10. **Optional**: To clean up the resources that you created, select **Administrator** from the perspective switcher, navigate to **Home > Projects**, click your project's action menu, and click **Delete Project**.


## What's next?
{: #whats-next}

* Complete the [{{site.data.keyword.openshiftlong_notm}} classic cluster tutorial](/docs/openshift?topic=openshift-openshift_tutorial) or the [{{site.data.keyword.openshiftlong_notm}} VPC cluster tutorial](/docs/openshift?topic=openshift-vpc_rh_tutorial) to:
    * Set up your {{site.data.keyword.cloud_notm}} and {{site.data.keyword.openshiftshort}} CLI.
    * Deploy an app that uses an {{site.data.keyword.cloud_notm}} service.
* For more information about working with your apps, see the [{{site.data.keyword.openshiftshort}} developer activities](https://docs.openshift.com/container-platform/4.6/welcome/index.html#developer-activities){: external} documentation.

Looking for an overview of all your options in {{site.data.keyword.openshiftlong_notm}}? Check out the curated [learning path for administrators](/docs/openshift?topic=openshift-learning-path-admin) or [learning path for developers](/docs/openshift?topic=openshift-learning-path-dev).
{: tip}





