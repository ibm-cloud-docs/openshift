---

copyright:
  years: 2014, 2021
lastupdated: "2021-09-10"

keywords: openshift, roks, rhoks, rhos

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}  


# Financial services use cases for {{site.data.keyword.cloud_notm}}
{: #cs_uc_finance}

These use cases highlight how workloads on {{site.data.keyword.openshiftlong}} can
take advantage of high availability, high-performance compute, easy spin-up of clusters for faster development, and AI from {{site.data.keyword.ibmwatson}}.
{: shortdesc}

## Mortgage company trims costs and accelerates regulatory compliance
{: #uc_mortgage}

A Risk Management VP for a residential mortgage company processes 70 million records a day, but the on-premises system was slow and also inaccurate. IT expenses soared because hardware quickly went out of date and wasn't utilized fully. While they waited for hardware provisioning, their regulatory compliance slowed.  
{: shortdesc}

Why {{site.data.keyword.cloud_notm}}: To improve risk analysis, the company looked to {{site.data.keyword.openshiftlong_notm}} and IBM Cloud Analytic services to reduce costs, increase worldwide availability, and ultimately accelerate regulatory compliance. With {{site.data.keyword.openshiftlong_notm}} in multiple regions, their analysis apps can be containerized and deployed across the globe, improving availability and addressing local regulations. Those deployments are accelerated with familiar open source tools, already part of {{site.data.keyword.openshiftlong_notm}}.

{{site.data.keyword.openshiftlong_notm}} and key technologies:
* [Horizontal scaling](/docs/openshift?topic=openshift-plan_deploy#highly_available_apps)
* [Multiple regions for high availability](/docs/openshift?topic=openshift-regions-and-zones#regions-and-zones)
* [Clusters that fit varied CPU, RAM, storage needs](/docs/openshift?topic=openshift-planning_worker_nodes#planning_worker_nodes)
* [Container security and isolation](/docs/openshift?topic=openshift-security#security)
* [{{site.data.keyword.cloudant}} to persist and sync data across apps](/docs/Cloudant?topic=Cloudant-getting-started-with-cloudant)
* [SDK for Node.js](/docs/cloud-foundry-public?topic=cloud-foundry-public-getting-started-node)

**The solution**

They started by containerizing the analysis apps and putting them in the cloud. In a flash, their hardware headaches went away. They were able to easily design Kubernetes clusters to fit their high-performance CPU, RAM, storage, and security needs. And when their analysis apps change, they can add or shrink compute without huge hardware investments. With the {{site.data.keyword.openshiftlong_notm}} horizontal scaling, their apps scale with the growing number of records, resulting in faster regulatory reports. {{site.data.keyword.openshiftlong_notm}} provides elastic compute resources around the world that are secure and highly performant for full usage of modern compute resources.

Now those apps receive high-volume data from a data warehouse on {{site.data.keyword.cloudant}}. Cloud-based storage in {{site.data.keyword.cloudant}} ensures higher availability than when it was locked in an on-premises system. Since availability is essential, the apps are deployed across global data centers: for DR and for latency too.

They also accelerated their risk analysis and compliance. Their predictive and risk analytics functions, such as Monte Carlo calculations, are now constantly updated through iterative agile deployments. Container orchestration is handled by a managed Kubernetes so that operations costs are reduced too. Ultimately risk analysis for mortgages is more responsive to the fast-paced changes in the market.

**Context: Compliance and financial modeling for residential mortgages**

* Heightened need for better financial risk management drives increases in regulatory oversight. The same needs drive the associated review in risk assessment processes and disclosure of more granular, integrated, and abundant regulatory reporting.
* High Performance Computing Grids are the key infrastructure components for financial modeling.

The problem of the company right now is scale and time to delivery.

Their current environment is 7+ years old, on-premises, and with limited compute, storage, and I/O capacity.
Server refreshes are costly and take a long time to complete.
Software and app updates follow an informal process and aren't repeatable.
The actual HPC grid is hard to program against. The API is too complex for new Developers who are brought onboard and requires non-documented knowledge.
And major app upgrades take 6 - 9 months to complete.

**Solution model: On-demand compute, storage, and I/O services that run in public cloud with secure access to on-premises enterprise assets as needed**

* Secure and scalable document storage that supports structured and unstructured document query
* "Lift and shift" existing enterprise assets and app while they enabled the integration to some on-premises systems that won't be migrated
* Shorten time-to-deploy solutions and implement standard DevOps and monitoring processes to address bugs that affected reporting accuracy

**Detailed solution**

* {{site.data.keyword.openshiftlong_notm}}
* {{site.data.keyword.cos_full_notm}}
* {{site.data.keyword.sqlquery_notm}} (Spark)
* {{site.data.keyword.cloudant}}
* {{site.data.keyword.SecureGateway}}

{{site.data.keyword.openshiftlong_notm}} provides scalable compute resources and the associated DevOps dashboards to create, scale, and tear down apps and services on demand. Using industry-standard containers, apps can initially be rehosted on {{site.data.keyword.openshiftlong_notm}} quickly without major architectural changes.

This solution provides the immediate benefit of scalability. By using Kubernetes's rich set of deployment and runtime objects, the mortgage company monitors and manages the upgrades to apps reliably. They're also able to replicate and scale the apps that use defined rules and the automated Kubernetes orchestrator.

{{site.data.keyword.SecureGateway}} is used to create a secure pipeline to on-premises databases and documents for apps that are rehosted to run in {{site.data.keyword.openshiftlong_notm}}.

{{site.data.keyword.cos_full_notm}} is for all raw document and data storage as they go forward. For Monte Carlo simulations, a workflow pipeline is put in place where simulation data is in structured files that are stored in {{site.data.keyword.cos_full_notm}}. A trigger to start the simulation scales compute services in {{site.data.keyword.openshiftlong_notm}} to split the data of the files into N event buckets for simulation processing. {{site.data.keyword.openshiftlong_notm}} automatically scales to N associated service executions and writes intermediate results to {{site.data.keyword.cos_full_notm}}. Those results are processed by another set of the {{site.data.keyword.openshiftlong_notm}} compute services to produce the final results.

{{site.data.keyword.cloudant}} is a modern NoSQL database that is useful for many data-driven use cases: from key-value to complex document-oriented data storage and query. To manage the growing set of regulatory and management report rules, the mortgage company uses {{site.data.keyword.cloudant}} to store documents that are associated with raw regulatory data the come into the firm. Compute processes on {{site.data.keyword.openshiftlong_notm}} are triggered to compile, process, and publish the data in various reporting formats. Intermediate results common across reports are stored as {{site.data.keyword.cloudant}} documents so template-driven processes can be used to produce the necessary reports.

**Results**

* Complex financial simulations are completed in 25% of the time than was previously possible with the existing on-premises systems.
* Time to deployment improved from the previous 6 - 9 months to 1 - 3 weeks on average. This improvement occurs because {{site.data.keyword.openshiftlong_notm}} allows for a disciplined, controlled process for ramping up app containers and replacing them with newer versions. Reporting bugs can be fixed quickly, addressing issues, such as accuracy.
* Regulatory reporting costs were reduced with a consistent, scalable set of storage and compute services that {{site.data.keyword.openshiftlong_notm}} and {{site.data.keyword.cloudant}} bring.
* Over time, the original apps that were initially "lifted and shifted" to the cloud were rearchitected into cooperative microservices that run on {{site.data.keyword.openshiftlong_notm}}. This action further sped up development and time to deploy and allowed more innovation due to the relative ease of experimentation. They also released innovative apps with newer versions of microservices to take advantage of market and business conditions (that is, so called situational apps and microservices).


## Payment tech company streamlines developer productivity, deploying AI-enabled tools to their partners 4 times faster
{: #uc_payment_tech}

A Development Exec has Developers that use on-premises application tools that slow down prototyping while they wait for hardware procurement.
{: shortdesc}

Why {{site.data.keyword.cloud_notm}}: {{site.data.keyword.openshiftlong_notm}} provides spin-up of compute by using open-source standard technology. After the company moved to {{site.data.keyword.openshiftlong_notm}}, Developers have access to DevOps friendly tools, such as portable and easily shared containers.

Then, Developers can experiment easily, pushing changes to Development and Test systems quickly with open toolchains. Their  application development tools get a new face when they add on AI cloud services to apps with a click.

Key technologies:
* [Clusters that fit varied CPU, RAM, storage needs](/docs/openshift?topic=openshift-planning_worker_nodes#planning_worker_nodes)
* [DevOps native tools, including open toolchains in {{site.data.keyword.contdelivery_full}}](https://www.ibm.com/cloud/architecture/toolchains/)
* [IBM Cloud Pak for Applications](https://www.ibm.com/cloud/cloud-pak-for-applications)
* [Fraud prevention with {{site.data.keyword.watson}} AI](https://www.ibm.com/cloud/watson-studio)
* [DevOps native tools, including open toolchains in {{site.data.keyword.contdelivery_full}}](https://www.ibm.com/cloud/architecture/toolchains/)
* [SDK for Node.js](/docs/cloud-foundry-public?topic=cloud-foundry-public-getting-started-node)
* [Sign-on capability without changing app code by using {{site.data.keyword.appid_short_notm}}](/docs/appid?topic=appid-getting-started)

**Context: Streamlining developer productivity and deploying AI tools to partners 4 times faster**

* Disruption is rampant in the payment industry that also has dramatic growth both in the consumer and business-to-business segments. But updates to payment tools were slow.
* Cognitive features are needed to target fraudulent transactions in new and faster ways.
* With the growing numbers of partners and their transactions, the tool traffic increases, but their infrastructure budget needs to decrease, by maximizing efficiency of the resources.
* Their technical debt is growing, not shrinking from an inability to release quality software to keep up with market demands.
* Capital expense budgets are under tight control, and IT feels they don't have the budget or staff to create the testing and staging landscapes with their in-house systems.
* Security is increasingly a primary concern, and this concern only adds to the delivery burden that all cause even more delays.

**The solution**

The Development Exec is faced with many challenges in the dynamic payment industry. Regulations, consumer behaviors, fraud, competitors, and market infrastructures are all rapidly evolving. Fast-paced development is essential to being part of the future payment world.

Their business model is to provide payment tools to business partners, so they can help these financial institutions and other organizations deliver security-rich digital payment experiences.

They need a solution that helps the Developers and their business partners:
* FRONT-END TO PAYMENT TOOLS: fee systems, payment tracking including cross-border, regulatory compliance, biometrics, remittance, and more
* REGULATION-SPECIFIC FEATURES: each country has unique regulations so that the overall toolset might look similar but show country-specific benefits
* DEVELOPER-FRIENDLY TOOLS that accelerate roll-out of features and bug fixes
* FRAUD DETECTION AS A SERVICE (FDaaS) uses {{site.data.keyword.watson}} AI to keep one step ahead of frequent and growing fraudulent actions

**Solution model**

On-demand compute, DevOps tools, and AI that run in public cloud with access to back-end payment systems. Implement a CI/CD process to dramatically shorten delivery cycles.

Technical solution:
* {{site.data.keyword.openshiftlong_notm}}
* IBM Cloud Pak for Applications
* {{site.data.keyword.contdelivery_full}}
* IBM Cloud Logging and Monitoring
* {{site.data.keyword.ibmwatson_notm}} for Financial Services
* {{site.data.keyword.appid_full_notm}}

They started by containerizing the payment tool VMs and putting them in the cloud. In a flash, their hardware headaches went away. They were able to easily design Kubernetes clusters to fit their CPU, RAM, storage, and security needs. And when their payment tools need to change, they can add or shrink compute without expensive and slow hardware purchases.

With {{site.data.keyword.openshiftlong_notm}} horizontal scaling, their apps scale with the growing number of partners, resulting in faster growth. {{site.data.keyword.openshiftlong_notm}} provides elastic compute resources around the world that are secure for full usage of modern compute resources.

Accelerated development is a key win for the Exec. With the use of modern containers, Developers can experiment easily in the languages of their choice, pushing changes to Development and Test systems, scaled out on separate clusters. Those pushes were automated with open toolchains and {{site.data.keyword.contdelivery_full}}. No longer were updates to the tools languishing in slow, error-prone build processes. They can deliver incremental updates to their tools, daily or even more frequently.

Also, logging and monitoring for the tools, especially where they used {{site.data.keyword.watson}} AI, rapidly integrate into the system. Developers don’t waste time building complex logging systems, just to be able to troubleshoot their live systems. A key factor for less staffing costs is that IBM manages Kubernetes, so the Developers can focus on better payment tools.

Security first: With bare metal for {{site.data.keyword.openshiftlong_notm}}, the sensitive payment tools now have familiar isolation but within the flexibility of public cloud. Scans for vulnerabilities are run continuously.

**Step 1: Lift and shift to secure compute**
* Migrate virtual machine images to container images that run in {{site.data.keyword.openshiftlong_notm}} in the public {{site.data.keyword.cloud_notm}}. Deploy IBM Cloud Pak for Applications, so that developers have their familiar application development tools on the cloud. 
* From that core, Vulnerability Advisor provides image, policy, container, and packaging vulnerability scanning.
* Private data center / on-premises capital costs are greatly reduced and replaced with a utility computing model that scales based on workload demand.
* Consistently enforce policy-driven authentication to your services and APIs with a simple Ingress annotation. With declarative security you can ensure user authentication and token validation by using {{site.data.keyword.appid_short_notm}}.

**Step 2: Operations and connections to existing payment systems back-end**
* Use IBM {{site.data.keyword.SecureGateway}} to maintain secure connections to remaining on-premises tool systems.
* Provide standardized DevOps dashboards and practices through Kubernetes.
* After Developers build and test apps in Development and Test clusters, they use the {{site.data.keyword.contdelivery_full}} toolchains to deploy apps into the {{site.data.keyword.openshiftlong_notm}} clusters across the globe.
* Built-in HA tools in {{site.data.keyword.openshiftlong_notm}} balance the workload within each geographic region, including self-healing and load balancing.

**Step 3: Analyze and prevent fraud**
* Deploy IBM {{site.data.keyword.watson}} for Financial Services to prevent and detect fraud.
* Using the toolchains and Helm deployment tools, the apps are also deployed to the {{site.data.keyword.openshiftlong_notm}} clusters across the globe. Then, workloads and data meet regional regulations.

**Results**
* Lifting the existing monolithic VMs into cloud-hosted containers was a first step that allowed the Development Exec to save on capital and operations costs.
* With infrastructure management taken care of by IBM, the Development team was freed up to deliver updates 10 times daily.
* In parallel, the provider implemented simple time-boxed iterations to get a handle on the existing technical debt.
* With the number of transactions they process, they can scale their operations exponentially.
* At the same time, new fraud analysis with {{site.data.keyword.watson}} increased the speed of detection and prevention, reducing fraud 4 times more than the region’s average.



