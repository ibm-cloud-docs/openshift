---

copyright:
  years: 2014, 2019
lastupdated: "2019-08-01"

keywords: openshift, roks, rhoks, rhos

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
{:deprecated: .deprecated}
{:download: .download}
{:preview: .preview}

# Transportation use cases for {{site.data.keyword.cloud_notm}}
{: #cs_uc_transport}

These use cases highlight how workloads on {{site.data.keyword.openshiftlong}} can
take advantage of toolchains for rapid app updates and multiregion deployments across the globe. At the same time, these workloads can connect to existing back-end systems, use Watson AI for personalization, and access IOT data with {{site.data.keyword.messagehub_full}}.

{: shortdesc}

## Shipping company increases availability of worldwide systems for business partner ecosystem
{: #uc_shipping}

An IT Exec has worldwide shipping routing and scheduling systems that partners interact with. Partners require up-to-the-minute information from these systems that access IoT device data. But, these systems were unable to scale across the globe with sufficient HA. 
{: shortdesc}

Why {{site.data.keyword.cloud_notm}}: Red Hat OpenShift on IBM Cloud scales containerized apps with five 9s of availability to meet growing demands. App deployments occur 40 times daily when Developers experiment easily, pushing changes to Development and Test systems quickly. The IoT Platform makes access to IoT data easy.

Key technologies:    
* [Multi-regions for business partner ecosystem ](/docs/containers?topic=containers-regions-and-zones#regions-and-zones)
* [Horizontal scaling](/docs/containers?topic=containers-app#highly_available_apps)
* [Open toolchains in {{site.data.keyword.contdelivery_full}}](https://www.ibm.com/cloud/garage/toolchains/)
* [Cloud services for innovation](https://www.ibm.com/cloud/products/#analytics)
* [{{site.data.keyword.messagehub_full}} to feed event data to apps](/docs/services/EventStreams?topic=eventstreams-about#about)

**Context: Shipping company increases availability of worldwide systems for business partner ecosystem**

* Regional differences for shipping logistics made it difficult to keep up with growing number of partners in multiple countries. An example is the unique regulations and transit logistics, where the company must maintain consistent records across borders.
* Just-in-time data meant that the worldwide systems must be highly available to reduce lags in transit operations. Time tables for shipping terminals are highly controlled and in some cases inflexible. Web usage is growing, so instability might cause a poor user experience.
* Developers needed to constantly evolve apps, but traditional tools slowed their ability to deploy updates and features frequently.  

**The solution**

The shipping company needs to cohesively manage shipping time tables, inventories, and customs paperwork. Then, they can accurately share the location of shipments, shipping contents, and delivery schedules to their customers. They’re taking the guess work out of when a good (such as an appliance, clothing, or produce) will arrive so that their shipping customers can communicate that information to their own customers.

The solution is made up of these primary components:
1. Streaming data from IoT devices for each shipping container: manifests and location
2. Customs paperwork that’s digitally shared with applicable ports and transit partners, including access control
3. App for shipping customers that aggregates and communicates arrival information for shipped goods, including APIs for shipping customers to reuse shipment data in their own retail and business-to-business apps

For the shipping company to work with global partners, the routing and scheduling systems required local modifications to fit each region’s language, regulations, and unique port logistics. Red Hat OpenShift on IBM Cloud offers global coverage in multiple regions, including North America, Europe, Asia, and Australia so that the apps reflected the needs of its partners, in each country.

IoT devices stream data that {{site.data.keyword.messagehub_full}} distributes to the regional port apps and associated Customs and Container manifest data stores. {{site.data.keyword.messagehub_full}} is landing point for IoT events. It  distributes the events based on the managed connectivity that the Watson IoT Platform offers to {{site.data.keyword.messagehub_full}}.

After events are in {{site.data.keyword.messagehub_full}}, they're persisted for immediate use in port transit apps and for any point in the future. Apps that require the lowest latency directly consume in real time from the event stream ({{site.data.keyword.messagehub_full}}). Other future apps, such as analytics tools, can choose to consume in a batch mode from the event store with {{site.data.keyword.cos_full}}.

Since shipping data is shared with the customers of the company, the Developers ensure that the customers can use APIs to surface shipping data in their own apps. Examples of those apps are mobile tracking apps or web e-commerce solutions. The Developers are also busy with building and maintaining the regional port apps that gather and disseminate the customs records and shipping manifests. In short, they need to focus on coding instead of managing the infrastructure. Thus, they chose Red Hat OpenShift on IBM Cloud because IBM simplifies infrastructure management:
* Managing Kubernetes master, IaaS, and operational components, such as Ingress and storage
* Monitoring health and recovery for worker nodes
* Providing global compute, so Developers aren't responsible for infrastructure in several regions where they need workloads and data to reside

To achieve global availability, the Development, Test, and Production systems were deployed across the globe in several data centers. For HA, they use a combination of multiple clusters in different geographic regions as well as multizone clusters. They can easily deploy the port app to meet business needs:
* In Frankfort clusters to comply with the local European regulations
* In the United States clusters to ensure local availability and failure recovery

They also spread the workload across multizone clusters in Frankfurt to ensure that the European version of the app is available and also balances the workload efficiently. Because each region uploads unique data with the port app, the app’s clusters are hosted in regions where latency is low.

For Developers, much of the continuous integration and delivery (CI/CD) process can be automated with {{site.data.keyword.contdelivery_full}}. The company can define workflow toolchains to prepare container images, check for vulnerabilities, and deploy them to the Kubernetes cluster.

**Solution model**

On-demand compute, storage, and event management that run in public cloud with access to shipment data across the globe, as needed

Technical solution:
* Red Hat OpenShift on IBM Cloud
* {{site.data.keyword.messagehub_full}}
* {{site.data.keyword.cos_full}}
* {{site.data.keyword.contdelivery_full}}

**Step 1: Containerize apps, by using microservices**

* Integrate apps into a set of cooperative microservices in Red Hat OpenShift on IBM Cloud based on functional areas of the app and its dependencies.
* Deploy apps to containers in Red Hat OpenShift on IBM Cloud.
* Provide standardized DevOps dashboards through Kubernetes.
* Enables on-demand scaling of compute for batch and other inventory workloads that run infrequently.
* Use {{site.data.keyword.messagehub_full}} to manage streaming data from IoT devices.

**Step 2: Ensure global availability**
* Built-in HA tools in Red Hat OpenShift on IBM Cloud balance the workload within each geographic region, including self-healing and load balancing.
* Load-balancing, firewalls, and DNS are handled by IBM Cloud Internet Services.
* Using the toolchains and Helm deployment tools, the apps are also deployed to clusters across the globe, so workloads and data meet regional requirements.

**Step 3: Share data**
* {{site.data.keyword.cos_full}} plus {{site.data.keyword.messagehub_full}} provides real-time and historically data storage.
* APIs allow the customers of the shipping company to share data into their apps.

**Step 4: Deliver continuously**
* {{site.data.keyword.contdelivery_full}} helps Developers to quickly provision an integrated toolchain, by using customizable, shareable templates with tools from IBM, third parties, and open source. Automate builds and tests, controlling quality with analytics.
* After Developers build and test the apps in their Development and Test clusters, they use the IBM CI/CD toolchains to deploy apps into clusters across the globe.
* Red Hat OpenShift on IBM Cloud provides easy rollout and roll-back of apps; tailored apps are deployed to meet regional requirements through the intelligent routing and load balancing of Istio.

**Results**

* With Red Hat OpenShift on IBM Cloud and IBM CI/CD tools, regional versions of apps are hosted near to the physical devices that they gather data from.
* Microservices greatly reduce time to delivery for patches, bug fixes, and new features. Initial development is fast, and updates are frequent.
* Shipping customers have real-time access to shipments’ locations, delivery schedules, and even approved port records.
* Transit partners at various shipping terminals are aware of manifests and shipment details so that onsite logistics are improved, instead of delayed.
* Separately from this story, [Maersk and IBM formed a joint venture](https://www.ibm.com/press/us/en/pressrelease/53602.wss) to improve international supply chains with Blockchain.

## Airline delivers innovative Human Resources (HR) benefits site in under 3 weeks
{: #uc_airline}

An HR Exec (CHRO) needs a new HR benefits site with an innovative chatbot, but current Development tools and platform mean long lead times for apps to go live. This situation includes long waits for hardware procurement.
{: shortdesc}

Why {{site.data.keyword.cloud_notm}}: Red Hat OpenShift on IBM Cloud provides easy spin-up of compute. Then, Developers can experiment easily, pushing changes to Development and Test systems quickly with open toolchains. Their traditional software development tools get a boost when they add on IBM Watson Assistant. The new benefits site was created in less than 3 weeks.

Key technologies:    
* [Clusters that fit varied CPU, RAM, storage needs](/docs/openshift?topic=openshift-planning_worker_nodes#planning_worker_nodes)
* [Chatbot service powered by Watson](https://developer.ibm.com/code/patterns/create-cognitive-banking-chatbot/)
* [DevOps native tools, including open toolchains in {{site.data.keyword.contdelivery_full}}](https://www.ibm.com/cloud/garage/toolchains/)
* [SDK for Node.js](/docs/runtimes/nodejs?topic=Nodejs-nodejs_runtime#nodejs_runtime)

**Context: Rapidly building and deploying innovative HR benefits site in less than 3 weeks**
* Employee growth and changing HR policies meant that a whole new site would be required for annual enrollment.
* Interactive features, such as a chatbot, were expected to help communicate new HR policies to existing employees.
* Due to growth in number employees, the site traffic is increasing, but their infrastructure budget remains flat.
* The HR team faced pressure to move faster: roll out new site features quickly and post last-minute benefit changes frequently.
* The enrollment period lasts for two weeks, and so downtime for the new app isn't tolerated.

**The solution**

The airline wants to design an open culture that puts people first. The HR Executive is well aware that a focus on rewarding and retaining talent impacts the airline’s profitability. Thus, the annual rollout of benefits is a key aspect of fostering an employee-centered culture.

They need a solution that helps the Developers and their users:
* FRONT-END TO EXISTING BENEFITS: insurance, educational offerings, wellness, and more
* REGION-SPECIFIC FEATURES: each country has unique HR policies so that the overall site might look similar but show region-specific benefits
* DEVELOPER-FRIENDLY TOOLS that accelerate rollout of features and bug fixes
* CHATBOT to provide authentic conversations about benefits and resolve users requests and questions efficiently.

Technical solution:
* Red Hat OpenShift on IBM Cloud
* IBM Watson Assistant and Tone Analyzer
* {{site.data.keyword.contdelivery_full}}
* IBM Logging and Monitoring
* {{site.data.keyword.SecureGatewayfull}}
* {{site.data.keyword.appid_full_notm}}

Accelerated development is a key win for the HR Exec. The team gets started by containerizing their apps and putting them in the cloud. With the use of modern containers, Developers can experiment easily with Node.js SDK and push changes to Development and Test systems, which are scaled out on separate clusters. Those pushes were automated with open toolchains and {{site.data.keyword.contdelivery_full}}. No longer were updates to the HR site languishing in slow, error-prone build processes. They can deliver incremental updates to their site, daily or even more frequently.  Moreover logging and monitoring for the HR site is rapidly integrated, especially for how the site pulls personalized data from back-end benefit systems. Developers don’t waste time building complex logging systems, just to be able to troubleshoot live systems. Developers don't need to become experts in cloud security, they can enforce policy driven authentication easily by using {{site.data.keyword.appid_full_notm}}.

With Red Hat OpenShift on IBM Cloud, they went from over-built hardware in a private data center to customizable compute that reduces IT operations, maintenance, and energy. To host the HR site, they could easily design Kubernetes clusters to fit their CPU, RAM, and storage needs. Another factor for less personnel costs is that IBM manages Kubernetes, so the Developers can focus on delivering better employee experience for benefits enrollment.

Red Hat OpenShift on IBM Cloud provides scalable compute resources and the associated DevOps dashboards to create, scale, and tear down apps and services on demand. Using industry-standard containers technology apps can be quickly developed and shared across multiple Development, Test, and Production environments. This setup provides the immediate benefit of scalability. Using Kubernetes rich set of deployment and runtime objects, the HR team can monitor and manage upgrades to apps reliably. They can also replicate and scale the apps, by using defined rules and the automated Kubernetes orchestrator.

**Step 1: Containers, microservices, and the Garage Method**
* Apps are built in a set of cooperative microservices that run in Red Hat OpenShift on IBM Cloud. The architecture represents the functional areas of the app with the most quality problems.
* Deploy apps to container in Red Hat OpenShift on IBM Cloud, continuously scanned with IBM Vulnerability Advisor.
* Provide standardized DevOps dashboards through Kubernetes.
* Adopt the essential agile and iterative development practices within the IBM Garage Method to enable frequent releases of new functions, patches, and fixes without downtime.

**Step 2: Connections to existing benefits back-end**
* {{site.data.keyword.SecureGatewayfull}} is used to create a secure tunnel to on-premises systems that host the benefits systems.  
* Combination of on-premises data and Red Hat OpenShift on IBM Cloud lets them access sensitive data while they adhere to regulations.
* Chatbot conversations fed back into HR policies, allowing the benefits site to reflect which benefits were most and least popular, including targeted improvements to poorly performing initiatives.

**Step 3: Chatbot and personalization**
* IBM Watson Assistant provides tools to quickly scaffold a chatbot that can provide the right benefits information to users.
* Watson Tone Analyzer ensures that customers are satisfied with the chatbot conversations and take human intervention when necessary.

**Step 4: Deliver continuously across the globe**
* {{site.data.keyword.contdelivery_full}} helps Developers to quickly provision an integrated toolchain, by using customizable, shareable templates with tools from IBM, third parties, and open source. Automate builds and tests, controlling quality with analytics.
* After Developers build and test the apps in their Development and Test clusters, they use the IBM CI/CD toolchains to deploy apps into Production clusters across the globe.
* Red Hat OpenShift on IBM Cloud provides easy rollout and roll-back of apps. Tailored apps are deployed to meet regional requirements through the intelligent routing and load balancing of Istio.
* Built-in HA tools in Red Hat OpenShift on IBM Cloud balance the workload within each geographic region, including self-healing and load balancing.

**Results**
* With tools like the chatbot, the HR team proved to their workforce that innovation was part of the corporate culture, not just buzz words.
* Authenticity with personalization in the site addressed the changing expectations of the airline’s workforce today.
* Last-minute updates to the HR site, including ones that driven by the employees chatbot conversations, went live quickly because Developers were pushing changes at least 10 times daily.
* With infrastructure management taken care of by IBM, the Development team was freed up to deliver the site in only 3 weeks.



