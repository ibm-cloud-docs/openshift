---

copyright: 
  years: 2014, 2022
lastupdated: "2022-03-22"

keywords: openshift

subcollection: openshift


---


{{site.data.keyword.attribute-definition-list}}


# Retail use cases for {{site.data.keyword.cloud_notm}}
{: #cs_uc_retail}

These use cases highlight how workloads on {{site.data.keyword.openshiftlong}} can take advantage of analytics for market insights, multiregion deployments across the globe, and inventory management with {{site.data.keyword.messagehub_full}} and object storage.
{: shortdesc}

## Brick-and-mortar retailer shares data, by using APIs with global business partners to drive omnichannel sales
{: #uc_data-share}

A Line-of-Business (LOB) Exec needs to increase sales channels, but the retail system is closed off in an on-premises data center. The competition has global business partners to cross-sell and upsell permutations of their goods: across brick-and-mortar and online sites.  
{: shortdesc}

### Why {{site.data.keyword.cloud_notm}}
{: #uc_data-share_ibmcloud}

{{site.data.keyword.openshiftlong_notm}} provides a public-cloud ecosystem, where containers enable new business partners and other external players to co-develop apps and data, through APIs. Now that the retail system is on the public cloud, APIs also streamline data sharing and jump-start new app development. App deployments increase when Developers experiment easily, pushing changes to Development and Test systems quickly with toolchains.

{{site.data.keyword.openshiftlong_notm}} and key technologies:
* [Clusters that fit varied CPU, RAM, storage needs](/docs/openshift?topic=openshift-planning_worker_nodes#planning_worker_nodes)
* [{{site.data.keyword.cos_full}} to persist and sync data across apps](/docs/cloud-object-storage?topic=cloud-object-storage-getting-started-cloud-object-storage)
* [DevOps native tools, including open toolchains in {{site.data.keyword.contdelivery_full}}](https://www.ibm.com/cloud/architecture/toolchains/)

#### Context: Retailer shares data, by using APIs with global business partners to drive omnichannel sales
{: #uc_data-share_context}

* The retailer is faced with strong competitive pressures. First, they need to mask the complexity of crossing into new products and new channels. For example, they need to expand product sophistication. At the same time, it needs to be simpler for their customers to jump across brands.
* That ability to jump brand means that the retail ecosystem requires connectivity to business partners. Then, the cloud can bring new value from business partners, customers, and other external players.
* Burst user events, like Black Friday, strain existing online systems, forcing the retailer to over-provision the compute infrastructure.
* The retailer’s Developers needed to constantly evolve apps, but traditional tools slowed their ability to deploy updates and features frequently, especially when they collaborate with business partner teams.  

#### The solution
{: #uc_data-share_solution}

A smarter shopping experience is needed to increase customer retention and gross profit margin. The retailer’s traditional sales model was suffering due to the lack of business partner inventory for cross-sales and up-sales. Their shoppers are looking for increased convenience, so that they can quickly find related items together, such as yoga pants and mats.

The retailer must also provide customers with useful content, such as product information, alternative product information, reviews, and real-time inventory visibility. And those customers want it while online and in-store through personal mobile devices and mobile-equipped store associates.

The solution is made up of the following primary components.
* INVENTORY: App for business partner ecosystem that aggregates and communicates inventory, especially new product introductions, including APIs for business partners to reuse in their own retail and B2B apps
* CROSS- AND UP-SALES: App that surfaces cross-sell and up-sell opportunities with APIs that can be used in various e-commerce and mobile apps
* DEVELOPMENT ENVIRONMENT: Kubernetes clusters for Dev, Test, and Production systems increase collaboration and data sharing among the retailer and its business partners

For the retailer to work with global business partners, the inventory APIs required changes to fit each region’s language and market preferences. {{site.data.keyword.openshiftlong_notm}} offers coverage in multiple regions, including North America, Europe, Asia, and Australia, so that the APIs reflected the needs of each country and ensured low latency for API calls.

Another requirement is that inventory data must be shareable with the business partners and customers of the company. With the inventory APIs, Developers can surface information in apps, such as mobile inventory apps or web e-commerce solutions. The Developers are also busy with building and maintaining the primary e-commerce site. In short, they need to focus on coding instead of managing the infrastructure.

Thus, they chose {{site.data.keyword.openshiftlong_notm}} because IBM simplifies infrastructure management.
* Managing Kubernetes master, IaaS, and operational components, such as Ingress and storage
* Monitoring health and recovery for worker nodes
* Providing global compute, so Developers own hardware infrastructure in regions where they need workloads and data to reside

Moreover logging and monitoring for the API microservices, especially how they pull personalized data out of back-end systems, easily integrates with {{site.data.keyword.openshiftlong_notm}}. Developers don’t waste time building complex logging systems, just to be able to troubleshoot live systems.

{{site.data.keyword.messagehub_full}} acts as the just-in-time events platform to bring in the rapidly changing information from the business partners’ inventory systems to {{site.data.keyword.cos_full}}.

#### Solution model
{: #uc_data-share_model}

On-demand compute, storage, and event management that runs in public cloud with access to retail inventories across the globe, as needed

Technical solution:
* {{site.data.keyword.openshiftlong_notm}}
* {{site.data.keyword.messagehub_full}}
* {{site.data.keyword.cos_full}}
* {{site.data.keyword.contdelivery_full}}
* IBM Cloud Logging and Monitoring
* {{site.data.keyword.appid_short_notm}}

#### Step 1: Containerize apps by using microservices
{: #uc_data-share_step1}

* Structure apps into a set of cooperative microservices that run within {{site.data.keyword.openshiftlong_notm}} based on functional areas of the app and its dependencies.
* Deploy apps to container images that run in {{site.data.keyword.openshiftlong_notm}}.
* Provide standardized DevOps dashboards through Kubernetes.
* Enable on-demand scaling of compute for batch and other inventory workloads that run infrequently.

#### Step 2: Ensure global availability
{: #uc_data-share_step2}

* Built-in HA tools in {{site.data.keyword.openshiftlong_notm}} balance the workload within each geographic region, including self-healing and load balancing.
* Load-balancing, firewalls, and DNS are handled by IBM Cloud Internet Services.
* Using the toolchains and Helm deployment tools, the apps are also deployed to clusters across the globe, so workloads and data meet regional requirements, especially personalization.

#### Step 3: Understand users
{: #uc_data-share_step3}

* {{site.data.keyword.appid_short_notm}} provides sign-on capabilities without needing to change app code.
* After users have signed in, you can use {{site.data.keyword.appid_short_notm}} to create profiles and personalize a user's experience of your application.

#### Step 4: Share data
{: #uc_data-share_step4}

* {{site.data.keyword.cos_full}} plus {{site.data.keyword.messagehub_full}} provides real-time and historical data storage, so that cross-sales offers represent available inventory from business partners.
* APIs allow the retailer’s business partners to share data into their e-commerce and B2B apps.

#### Step 5: Deliver continuously
{: #uc_data-share_step5}

* Debugging the co-developed APIs becomes simpler when they add on IBM Cloud Logging and Monitoring tools, cloud-based ones that are accessible to the various Developers.
* {{site.data.keyword.contdelivery_full}} helps Developers to quickly provision an integrated toolchain by using customizable, shareable templates with tools from IBM, third parties, and open source. Automate builds and tests, controlling quality with analytics.
* After Developers build and test the apps in their Development and Test clusters, they use the IBM continuous integration and delivery (CI and CD) toolchains to deploy apps into clusters across the globe.
* {{site.data.keyword.openshiftlong_notm}} provides easy roll-out and roll-back of apps; tailored apps are deployed to test campaigns through the intelligent routing and load balancing of Istio.

#### Results
{: #uc_data-share_results}

* Microservices greatly reduce time to delivery for patches, bug fixes, and new features. Initial worldwide development is fast, and updates are as frequent as 40 times a week.
* The retailer and its business partners have immediate access to inventory availability and delivery schedules, by using the APIs.
* With {{site.data.keyword.openshiftlong_notm}} and IBM CI and CD tools, A-B versions of apps are ready to test campaigns.
* {{site.data.keyword.openshiftlong_notm}} provides scalable compute, so that the inventory and cross-sales API workloads can grow during high-volume periods of the year, such as the fall holidays.

## Traditional grocer increases customer traffic and sales with digital insights
{: #uc_grocer}

A Chief Marketing Officer (CMO) needs to increase customer traffic by 20% in stores by making the stores a differentiating asset. Large retail competitors and online retailers are stealing sales. At the same time, the CMO needs to reduce inventory without markdowns because holding inventory too long locks up millions in capital.
{: shortdesc}

### Why {{site.data.keyword.cloud_notm}}
{: #uc_grocer_ibmcloud}

{{site.data.keyword.openshiftlong_notm}} provides easy spin-up of more compute, where Developers quickly add Cloud Analytics services for sales behavior insights and digital market adaptability.

Key technologies:    
* [Horizontal scaling to accelerate development](/docs/openshift?topic=openshift-plan_deploy#highly_available_apps)
* [Clusters that fit varied CPU, RAM, storage needs](/docs/openshift?topic=openshift-planning_worker_nodes#planning_worker_nodes)
* [Insights to market trends with {{site.data.keyword.watson}} Discovery](https://www.ibm.com/cloud/watson-discovery)
* [DevOps native tools, including open toolchains in {{site.data.keyword.contdelivery_full}}](https://www.ibm.com/cloud/architecture/toolchains/)
* [Inventory management with {{site.data.keyword.messagehub_full}}](/docs/EventStreams?topic=EventStreams-about#about)

#### Context: Traditional grocer increases customer traffic and sales with digital insights
{: #uc_grocer_context}

* Competitive pressures from online retailers and large retail stores disrupted traditional grocery retail models. Sales are declining, evidenced by low foot traffic in physical stores.
* Their loyalty program needs a boost in the arm with a modern take on the printed coupons at check out. So Developers must constantly evolve the related apps, but traditional tools slow their ability to deploy updates and features frequently.  
* Certain high-value inventory isn’t moving as well as expected, but yet the “foodie” movement seems to be growing in major metropolitan markets.

#### The solution
{: #uc_grocer_solution}

The grocer needs an app to increase conversion and store traffic to generate new sales and build customer loyalty in a reusable cloud analytics platform. The in-store targeted experience can be an event along with a services or product vendor that attracts both loyalty and new customers based on affinity to the specific event. The store and business partner then offer incentives to come to the event as well as buying products from the store or business partner.  

After the event, customers are guided to purchasing the necessary products, so they can repeat the demonstrated activity on their own in the future. The targeted customer experience is measured with incentive redemption and new loyalty customer signups. The combination of a hyper-personalized marketing event and a tool to track in-store purchases can carry the targeted experience all the way through to product purchase. All these actions result in higher traffic and conversions.

As an example event, a local chef is brought into the store to show how to make a gourmet meal. The store provides an incentive to drive attendance. For example they provide a free appetizer at the chef's restaurant and an extra incentive to buy the ingredients for the demonstrated meal (for example, $20 off $150 cart).

The solution is made up of the following primary components.
1. INVENTORY ANALYSIS: the in-store events (recipes, ingredient lists, and product locations) are tailored to market the slow-moving inventory.
2. LOYALTY MOBILE APP provides targeted marketing with digital coupons, shopping lists, product inventory (prices, availability) on a store map, and social sharing.
3. SOCIAL MEDIA ANALYTICS provides personalization by detecting customers’ preferences in terms of trends: cuisines, chefs, and ingredients. The analytics connect regional trends with an individual’s Twitter, Pinterest, and Instagram activity.
4. DEVELOPER-FRIENDLY TOOLS accelerate roll-out of features and  bug fixes.

Back-end inventory systems for product inventory, store replenishment, and product forecasting have a wealth of information, but modern analytics can unlock new insights about how to better move high-end products. By using a combination of {{site.data.keyword.cloudant}} and IBM Streaming Analytics, the CMO can find the sweet spot of ingredients to match to custom in-store events.

{{site.data.keyword.messagehub_full}} acts as the just-in-time events platform to bring in the rapidly changing information from the inventory systems to IBM Streaming Analytics.

Social media analytics with {{site.data.keyword.watson}} Discovery (personality and tone insights) also feed in trends to the inventory analysis to improve product forecasting.

The loyalty mobile app provides detailed personalization information, especially when customers use its social sharing features, such as posting recipes.

In addition to the mobile app, the Developers are busy with building and maintaining the existing loyalty app that’s tied to traditional check-out coupons. In short, they need to focus on coding instead of managing the infrastructure. Thus, they chose {{site.data.keyword.openshiftlong_notm}} because IBM simplifies infrastructure management.
* Managing Kubernetes master, IaaS, and operational components, such as Ingress and storage
* Monitoring health and recovery for worker nodes
* Providing global compute, so Developers aren't responsible for infrastructure setup in data centers

#### Solution model
{: #uc_grocer_model}

On-demand compute, storage, and event management that runs in public cloud with access to back-end ERP systems

Technical solution:
* {{site.data.keyword.openshiftlong_notm}}
* {{site.data.keyword.messagehub_full}}
* {{site.data.keyword.cloudant}}
* IBM Streaming Analytics
* IBM {{site.data.keyword.watson}} Discovery

#### Step 1: Containerize apps, by using microservices
{: #uc_grocer_step1}

* Structure inventory analysis and mobile apps into microservices and deploy them to containers in {{site.data.keyword.openshiftlong_notm}}.
* Provide standardized DevOps dashboards through Kubernetes.
* Scale the compute on-demand for batch and other inventory workloads that run less frequently.

#### Step 2: Analyze inventory and trends
{: #uc_grocer_step2}

* {{site.data.keyword.messagehub_full}} acts as the just-in-time events platform to bring in the rapidly changing information from inventory systems to IBM Streaming Analytics.
* Social media analysis with {{site.data.keyword.watson}} Discovery and inventory systems data is integrated with IBM Streaming Analytics to deliver merchandising and marketing advice.

#### Step 3: Deliver promotions with mobile loyalty app
{: #uc_grocer_step3}

* Jump-start development of mobile app with the IBM Mobile Starter Kit and other IBM Mobile services, such as {{site.data.keyword.appid_full_notm}}.
* Promotions in the form of coupons and other entitlements are sent to users’ mobile app. The promotions were identified by using the inventory and social analysis, plus other back-end systems.
* Storage of promotion recipes on mobile app and conversions (redeemed check-out coupons) are fed back to ERP systems for further analysis.

#### Results
{: #uc_grocer_results}

* With {{site.data.keyword.openshiftlong_notm}}, microservices greatly reduce time to delivery for patches, bug fixes, and new features. Initial development is fast, and updates are frequent.
* Customer traffic and sales increased in stores by making the stores themselves a differentiating asset.
* At the same time, new insights from social and cognitive analysis improved reduced inventory OpEx (operating expenses).
* Social sharing in the mobile app also helps to identify and market to new customers.




