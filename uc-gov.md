---

copyright: 
  years: 2014, 2021
lastupdated: "2021-11-05"

keywords: openshift, roks, rhoks, rhos

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}


# Government use cases for {{site.data.keyword.cloud_notm}}
{: #cs_uc_gov}

These use cases highlight how workloads on {{site.data.keyword.openshiftlong}} benefit from the public cloud. These workloads are isolated in global regions for data sovereignty, use {{site.data.keyword.watson}} machine learning instead of net-new code, and connect to on-premises databases.
{: shortdesc}

## Regional government improves collaboration and velocity with community Developers who combine public-private data
{: #uc_data_mashup}

An Open-Government Data Program Executive needs to share public data with the community and private sector, but the data is locked in an on-premises monolithic system.  
{: shortdesc}

Why {{site.data.keyword.cloud_notm}}: With {{site.data.keyword.openshiftlong_notm}}, the Exec delivers the transformative value of combined public-private data. Likewise, the service provides the public cloud platform to refactor and expose microservices from monolithic on-premises apps. Also, the public cloud allows government and the public partnerships to use external cloud services and collaboration-friendly open-source tools.

Key technologies:    
* [Clusters that fit varied CPU, RAM, storage needs](/docs/openshift?topic=openshift-planning_worker_nodes#planning_worker_nodes)
* [DevOps native tools, including open toolchains in {{site.data.keyword.contdelivery_full}}](https://www.ibm.com/cloud/architecture/toolchains/)
* [Provide access to public data with {{site.data.keyword.cos_full_notm}}](/docs/cloud-object-storage?topic=cloud-object-storage-getting-started-cloud-object-storage)
* [Plug-and-play IBM Cloud Analytics services](https://www.ibm.com/cloud/analytics)

**Context: Government improves collaboration and velocity with community Developers who combine public-private data**
* An “open government” model is the future, but this regional government agency can't make the leap with their on-premises systems.
* They want to support innovation and foster co-development between private sector, citizens, and public agencies.
* Disparate groups of Developers from the government and private organizations don’t have a unified open-source platform where they can share APIs and data easily.
* Government data is locked in on-premises systems with no easy public access.

**The solution**

An open-government transformation must be built on a foundation that provides performance, resilience, business continuity, and security. As innovation and co-development move ahead, agencies and citizens depend on software, services, and infrastructure companies to “protect and serve.”

To bust bureaucracy and transform government’s relationship with its constituency, they turned to open standards to build a platform for co-creation:

* OPEN DATA – data storage where citizens, government agencies, and businesses access, share, and enhance data freely
* OPEN APIs – a development platform where APIs are contributed by and reused with all community partners
* OPEN INNOVATION – a set of cloud services that allow Developers to plug in innovation instead of manually coding it

To start, the government uses {{site.data.keyword.cos_full_notm}} to store its public data in the cloud. This storage is free to use and reuse, shareable by anyone, and subject only to attribution and share alike. Sensitive data can be sanitized before it’s pushed to the cloud. Besides that, access controls are set up so that the cloud caps new data storage, where the community can demonstrate POCs of enhanced existing free data.

The government’s next step for the public-private partnerships was to establish an API economy that is hosted in {{site.data.keyword.apiconnect_long}}. There, community and enterprise Developers make data easily accessible in API form. Their goals are to have publicly available REST APIs, to enable interoperability, and to accelerate app integration. They use IBM {{site.data.keyword.SecureGateway}} to connect back to private data sources on-premises.

Finally, apps based on those shared APIs are hosted in {{site.data.keyword.openshiftlong_notm}}, where it’s easy to spin up clusters. Then, Developers across the community, private sector, and the government can co-create apps easily. In short, Developers need to focus on coding instead of managing the infrastructure. Thus, they chose {{site.data.keyword.openshiftlong_notm}} because IBM simplifies infrastructure management:
* Managing Kubernetes master, IaaS, and operational components, such as Ingress and storage
* Monitoring health and recovery for worker nodes
* Providing global compute, so Developers don’t have to stand up infrastructure in worldwide regions where they need workloads and data to be located

Moving compute workloads into the {{site.data.keyword.cloud_notm}} isn't enough though. The government needs to go through a process and methods transformation as well. By adopting the practices of the IBM Garage Method, the provider can implement an agile and iterative delivery process that supports modern DevOps practices like Continuous Integration and Delivery (CI/CD).

Much of the CI/CD process itself is automated with {{site.data.keyword.contdelivery_full}} in the cloud. The provider can define workflow toolchains to prepare container images, check for vulnerabilities, and deploy them to the Kubernetes cluster.

**Solution model**

On-demand compute, storage, and API tools run in the public cloud with secure access to and from on-premises data sources.

Technical solution:
* {{site.data.keyword.openshiftlong_notm}}
* {{site.data.keyword.cos_full_notm}} and {{site.data.keyword.cloudant}}
* {{site.data.keyword.apiconnect_long}}
* IBM {{site.data.keyword.SecureGateway}}
* {{site.data.keyword.contdelivery_full}}

**Step 1: Store data in the cloud**
* {{site.data.keyword.cos_full_notm}} provides historical data storage, accessible to all on the public cloud.
* Use {{site.data.keyword.cloudant}} with developer-provided keys to cache data in the cloud.
* Use IBM {{site.data.keyword.SecureGateway}} to maintain secure connections to existing on-premises databases.

**Step 2: Provide access to data with APIs**
* Use {{site.data.keyword.apiconnect_long}} for the API economy platform. APIs allow the public and private sectors to combine data into their apps.
* Create clusters for public-private apps, which are driven by the APIs.
* Structure apps into a set of cooperative microservices that run within {{site.data.keyword.openshiftlong_notm}}, which is based on functional areas of apps and their dependencies.
* Deploy the apps to containers that run in {{site.data.keyword.openshiftlong_notm}}. Built-in HA tools in {{site.data.keyword.openshiftlong_notm}} balance the workloads, including self-healing and load balancing.
* Provide standardized DevOps dashboards through Kubernetes, open-source tools familiar to all types of Developers.

**Step 3: Innovate with IBM Garage and cloud services**
* Adopt the agile and iterative development practices from the IBM Garage Method to enable frequent releases of features, patches, and fixes without downtime.
* Whether developers are in the public or private sector, {{site.data.keyword.contdelivery_full}} helps them to quickly provision an integrated toolchain, by using customizable, shareable templates.
* After Developers build and test the apps in their Dev and Test clusters, they use the {{site.data.keyword.contdelivery_full}} toolchains to deploy apps into production clusters.
* With {{site.data.keyword.watson}} AI, machine learning, and deep learning tools available from the {{site.data.keyword.cloud_notm}} catalog, Developers focus on domain problems. Instead of custom unique ML code, ML logic is snapped into apps with service bindings.

**Results**
* Normally slow public-private partnerships now quickly spin up apps in weeks instead of months. These development partnerships now deliver features and bug fixes up to 10 times per week.
* Development is accelerated when all participants use well-known open-source tools, such as Kubernetes. Long learning curves are no longer a blocker.
* Transparency in activities, information, and plans is provided to citizens and private sector. And, citizens are integrated into government processes, services, and support.
* Public-private partnerships conquer Herculean tasks, such as Zika virus tracking, smart electricity distribution, analysis of crime statistics, and university "new collar" education.

## Large public port secures exchange of port data and shipping manifests that connect public and private organizations
{: #uc_port}

IT Execs for a private shipping company and the government-operated port need to connect, provide visibility, and securely exchange port information. But no unified system existed to connect public port information and private shipping manifests.
{: shortdesc}

Why {{site.data.keyword.cloud_notm}}: {{site.data.keyword.openshiftlong_notm}} allows government and the public partnerships to use external cloud services and collaboration-friendly open-source tools. The containers provided a shareable platform where both the port and shipping company felt assured that the shared information was hosted on a secure platform. And that platform scales as they went from small Dev-Test systems to production-sized systems. Open toolchains further accelerated development by automating build, test, and deployments.

Key technologies:    
* [Clusters that fit varied CPU, RAM, storage needs](/docs/openshift?topic=openshift-planning_worker_nodes#planning_worker_nodes)
* [Container security and isolation](/docs/openshift?topic=openshift-security#security)
* [DevOps native tools, including open toolchains in {{site.data.keyword.contdelivery_full}}](https://www.ibm.com/cloud/architecture/toolchains/)
* [SDK for Node.js](/docs/cloud-foundry-public?topic=cloud-foundry-public-getting-started-node)

**Context: Port secures exchange of port data and shipping manifests that connects public and private organizations.**

* Disparate groups of Developers from the government and shipping company don’t have a unified platform where they can collaborate, which slows down deployments of updates and features.
* Developers are spread across the globe and across organizational boundaries, which means open-source and PaaS the best option.
* Security is a primary concern, and this concern increases the collaboration burden that impacts features and updates to the software, especially after the apps are in production.
* Just-in-time data meant that the worldwide systems must be highly available to reduce lags in transit operations. Time tables for shipping terminals are highly controlled and in some cases inflexible. Web usage is growing, so instability might cause poor user experience.

**The solution**

The port and the shipping company co-develop a unified trading system to electronically submit compliance-related information  for the clearance of goods and ships once, rather than to multiple agencies. Manifest and customs apps can quickly share contents of a particular shipment and ensure that all paperwork is electronically transferred and processed by agencies for the port.

So they create a partnership that is dedicated to solutions for the trade system:
* DECLARATIONS - App to take in shipping manifests and digitally process typical customs paperwork and to flag out-of-policy items for investigation and enforcement
* TARIFFS – App to calculate tariffs, submit charges electronically to shipper, and receive digital payments
* REGULATIONS – Flexible and configurable app that feeds previous two apps with ever-changing policies and regulations that affect imports, exports, and tariff processing

Developers started by deploying their apps in containers with {{site.data.keyword.openshiftlong_notm}}. They created clusters for a shared Dev environment that allow worldwide Developers to collaboratively deploy app improvements quickly. Containers allow each development team to use the language of their choice.

Security first: The IT Execs chose bare metal clusters. With bare metal for {{site.data.keyword.openshiftlong_notm}}, the sensitive customs workloads now have familiar isolation but within the flexibility of public cloud.

Because the shipping company also wants to work with other ports, app security is crucial. Shipping manifests and customs information are highly confidential. From that secure core, Vulnerability Advisor provides these scans:
* Image vulnerability scans
* Policy scans that are based on ISO 27k

At the same time, {{site.data.keyword.iamlong}} helps to control who has which level of access to the resources.

Developers focus on domain problems, by using existing tools: Instead of Developers that write unique logging and monitoring code, they snap it into apps, by binding {{site.data.keyword.cloud_notm}} services to clusters. Developers are also freed up from infrastructure management tasks because IBM takes care of Kubernetes and infrastructure upgrades, security, and more.

**Solution model**

On-demand compute, storage, and Node starter kits that run in the public cloud with secure access to shipping data across the globe, as needed. Compute in clusters is tamper-proof and isolated to bare metal.  

Technical solution:
* {{site.data.keyword.openshiftlong_notm}}
* {{site.data.keyword.openwhisk}}
* {{site.data.keyword.cloudant}}
* IBM {{site.data.keyword.SecureGateway}}

**Step 1: Containerize apps, by using microservices**
* Use the Node.js starter kit from IBM to jump start development.
* Structure apps into a set of cooperative microservices that run within {{site.data.keyword.openshiftlong_notm}} based on functional areas of the app and its dependencies.
* Deploy the manifest and shipment apps to container that run in {{site.data.keyword.openshiftlong_notm}}.
* Provide standardized DevOps dashboards through Kubernetes.
* Use IBM {{site.data.keyword.SecureGateway}} to maintain secure connections to existing on-premises databases.

**Step 2: Ensure global availability**
* After Developers deploy the apps in their Dev and Test clusters, they use the {{site.data.keyword.contdelivery_full}} toolchains and Helm to deploy country-specific apps into clusters across the globe.
* Workloads and data can then meet regional regulations.
* Built-in HA tools in {{site.data.keyword.openshiftlong_notm}} balance the workload within each geographic region, including self-healing and load balancing.

**Step 3: Data sharing**
* {{site.data.keyword.cloudant}} is a modern NoSQL database suitable a range of data-driven use cases from key-value to complex document-oriented data storage and query.
* To minimize queries to the regional databases, {{site.data.keyword.cloudant}} is used to cache the user's session data across apps.
* This configuration improves the front-end app usability and performance across apps on {{site.data.keyword.containershort}}.
* While worker apps in {{site.data.keyword.openshiftlong_notm}} analyze on-premises data and store results in {{site.data.keyword.cloudant}}, {{site.data.keyword.openwhisk}} reacts to changes and automatically sanitizes data on the incoming feeds of data.
* Similarly, notifications of shipments in one region can be triggered through data uploads so that all down-stream consumers can access new data.

**Results**
* With IBM starter kits, {{site.data.keyword.openshiftlong_notm}}, and {{site.data.keyword.contdelivery_full}} tools, global Developers work together across organizations and governments. They collaboratively develop customs apps, with familiar and interoperable tools.
* Microservices greatly reduce time to delivery for patches, bug fixes, and new features. Initial development is fast, and updates are frequently 10 times per week.
* Shipping customers and government officials have access to manifest data and can share customs data, while they comply with local regulations.
* The shipping company benefits from improved logistics management in the supply chain: reduced costs and faster clearance times.
* 99% are digital declarations, and 90% of imports processed without human intervention.




