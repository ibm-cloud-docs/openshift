---

copyright:
  years: 2024
lastupdated: "2025-01-28"

keywords:

subcollection: openshift

---




{{site.data.keyword.attribute-definition-list}}

# Service dependency map for IBM Cloud Kubernetes Service and Red Hat OpenShift on IBM Cloud
{: #service-dependencies}

If a service depends on other {{site.data.keyword.cloud_notm}} services, there can be impacts if any of the dependent services are having issues. The dependency severity indicates the impact to the service when the dependency is down.
{: shortdesc}

Critical
:   When the the dependency is down, the service is down.

Significant
:   When the dependency is down, the service features are impacted.

Medium
:   When the dependency is down, the service might be impacted and a workaround is possible.

Minimal
:   When the dependency is down, the main service features are not impacted.

The following table provides the dependency listing of this service following a standard deployment.


|Dependencies|Dependency impacts|Customer provided|Control or data plane|Location of dependency|
|:---|:---|:---|:---|:---|
| IBM Cloud Service Endpoints | Availability, Instance control, Operations, Security compliance | No | Both |  Same data center  |
| IBM Cloud Virtual Private Cloud | Availability, Instance control, Operations | Yes | Both |  Same zone  |
| IBM Cloud Databases - databases-for-postgresql | Availability, Instance control, Operations | No | Both |  Same region  |
| IBM Cloud Classic DNS Servers | Availability, Change management, Instance control | No | Both |  Same data center  |
| IBM Cloud Identity and Access Management | Access management, Availability, Instance control, Operations, Security compliance | No | Both |  [Global](https://cloud.ibm.com/docs/resiliency?topic=resiliency-ha-redundancy#global-service)  |
| IBM Cloud File Storage for Virtual Private Cloud | Availability, Disaster recovery, Instance control | No | Both |  Same zone  |
| IBM Cloud DNS Services | Availability, Change management, Disaster recovery, Instance control | Yes | Both |  Same region  |
| IBM Cloud Virtual Servers | Availability, Instance control, Operations | No | Both |  Same data center  |
| IBM Cloud Load Balancer for VPC | Availability, Operations | No | Both |  Same zone  |
| Akamai | Availability, Instance control | No | Both |  [Global](https://cloud.ibm.com/docs/resiliency?topic=resiliency-ha-redundancy#global-service)  |
| IBM Cloud Virtual Private Endpoint for VPC | Availability, Instance control | No | Both |  Same zone  |
| IBM Cloud File Storage | Availability, Disaster recovery, Instance control | No | Both |  Same data center  |
| IBM Cloud Global Search and Tagging | Availability | No | Both |  [Global](https://cloud.ibm.com/docs/resiliency?topic=resiliency-ha-redundancy#global-service)  |
| IBM Cloud Block Storage | Availability, Disaster recovery, Instance control | No | Both |  Same data center  |
| IBM Cloud Block Storage for Virtual Private Cloud | Availability, Instance control | No | Both |  Same zone  |
| IBM Cloud Virtual Server for VPC | Availability, Instance control | No | Both |  Same zone  |
{: row-headers}
{: caption="IBM Cloud Kubernetes Service and Red Hat OpenShift on IBM Cloud service dependency information - Critical dependencies" caption-side="top"}
{: tab-title="Critical dependencies"}
{: tab-group="service-dependency-data-for-containers-kubernetes"}
{: class="comparison-tab-table"}
{: #critical-deps}
{: summary="Use the buttons for the dependency level to change the context of the table. This table has row and column headers. The row headers details about the dependency. The column headers identify the dependency. To understand the details about each dependency, navigate to the row to find the dependency that you need more information about interested in."}

|Dependencies|Dependency impacts|Customer provided|Control or data plane|Location of dependency|
|:---|:---|:---|:---|:---|
| IBM Key Protect for IBM Cloud | Availability, Instance control, Operations, Security compliance | No | Both |  Same region  |
| IBM Cloud Global Resource Catalog | Availability, Change management, Instance control | No | Both |  [Global](https://cloud.ibm.com/docs/resiliency?topic=resiliency-ha-redundancy#global-service)  |
| IBM Cloud Bare Metal | Availability, Instance control, Operations | No | Both |  Same data center  |
| IBM Key Protect for IBM Cloud | Availability, Instance control, Security compliance | Yes | Both |  Same region  |
| RedHat OpenShift Cluster Manager | Availability | No | Both |  [Global](https://cloud.ibm.com/docs/resiliency?topic=resiliency-ha-redundancy#global-service)  |
| IBM Cloud Container Registry | Availability, Change management, Instance control, Operations | No | Both |  Same region  |
| IBM Cloud Classic NTP Servers | Availability, Change management, Instance control | No | Both |  Same data center  |
| Let's Encrypt | Availability | No | Both |  [Global](https://cloud.ibm.com/docs/resiliency?topic=resiliency-ha-redundancy#global-service)  |
| IBM Cloud Hyper Protect Crypto | Availability, Instance control | Yes | Both |  Same region  |
| IBM Cloud Business Support Services | Availability | No | Both |  [Global](https://cloud.ibm.com/docs/resiliency?topic=resiliency-ha-redundancy#global-service)  |
{: row-headers}
{: caption="IBM Cloud Kubernetes Service and Red Hat OpenShift on IBM Cloud service dependency information - Significant dependencies" caption-side="top"}
{: tab-title="Significant dependencies"}
{: tab-group="service-dependency-data-for-containers-kubernetes"}
{: class="comparison-tab-table"}
{: #significant-deps}
{: summary="Use the buttons for the dependency level to change the context of the table. This table has row and column headers. The row headers details about the dependency. The column headers identify the dependency. To understand the details about each dependency, navigate to the row to find the dependency that you need more information about interested in."}

|Dependencies|Dependency impacts|Customer provided|Control or data plane|Location of dependency|
|:---|:---|:---|:---|:---|
| IBM Cloud Secrets Manager| Change management | Yes | Both |  Same region  |
| IBM Cloud Secrets Manager| Change management, Disaster recovery, Security compliance | No | Both |  Same region  |
{: row-headers}
{: caption="IBM Cloud Kubernetes Service and Red Hat OpenShift on IBM Cloud service dependency information - Medium dependencies" caption-side="top"}
{: tab-title="Medium dependencies"}
{: tab-group="service-dependency-data-for-containers-kubernetes"}
{: class="comparison-tab-table"}
{: #medium-deps}
{: summary="Use the buttons for the dependency level to change the context of the table. This table has row and column headers. The row headers details about the dependency. The column headers identify the dependency. To understand the details about each dependency, navigate to the row to find the dependency that you need more information about interested in."}

|Dependencies|Dependency impacts|Customer provided|Control or data plane|Location of dependency|
|:---|:---|:---|:---|:---|
| SOS Inventory Management| Security compliance | No | Both |  [Global](https://cloud.ibm.com/docs/resiliency?topic=resiliency-ha-redundancy#global-service)  |
| PagerDuty| Operations | No | Both |  [Global](https://cloud.ibm.com/docs/resiliency?topic=resiliency-ha-redundancy#global-service)  |
| OSS Platform| Operations | No | Both |  [Global](https://cloud.ibm.com/docs/resiliency?topic=resiliency-ha-redundancy#global-service)  |
| IBM Cloud Object Storage| Disaster recovery | No | Both |  Same region  |
| LaunchDarkly| Operations | No | Both |  [Global](https://cloud.ibm.com/docs/resiliency?topic=resiliency-ha-redundancy#global-service)  |
| IBM Log Analysis Log Routing| Operations | No | Both |  Same region  |
| IBM Cloud Activity Tracker event routing| Security compliance | No | Both |  Same region  |
| Slack| Operations | No | Both |  [Global](https://cloud.ibm.com/docs/resiliency?topic=resiliency-ha-redundancy#global-service)  |
| IBM Cloud Privileged Access Gateway| Operations, Security compliance | No | Both |  Same region  |
| IBM Cloud Monitoring| Operations | No | Both |  Same region  |
{: row-headers}
{: caption="IBM Cloud Kubernetes Service and Red Hat OpenShift on IBM Cloud service dependency information - Minimal dependencies" caption-side="top"}
{: tab-title="Minimal dependencies"}
{: tab-group="service-dependency-data-for-containers-kubernetes"}
{: class="comparison-tab-table"}
{: #minimal-deps}
{: summary="Use the buttons for the dependency level to change the context of the table. This table has row and column headers. The row headers details about the dependency. The column headers identify the dependency. To understand the details about each dependency, navigate to the row to find the dependency that you need more information about interested in."}

This table can be used to answer the following questions:

- **What is the expected impact to the functions described?** Each severity tab in the table indicates the impact that your provisioned service might encounter if the dependency were to go offline. This means that the dependency high availability and disaster recovery influences the severity of the impact and therefore is used for general guidance to help you understand potential issues that might arise if the dependency was impacted by an incident.

   Services that are regional are not impacted by a severe outage of a single availability zone because of the failover that is built in to default to another zone. For these occurrences, there might be a slight performance impact, if any, while the system fails over to the other location. This also applies to global services where the impact is lowered even more as it can fail over to other regions if necessary. This reduces the frequency at which these items might have the impact that is shown.
   {: note}

- **What services does my service depend on?** The Dependencies column lists the services. These are the major service to service dependencies including major internal dependencies that might not be visible externally.

- **What function does the dependency impact?** Functions include access management, availability, change management, configuration management, customer responsibility, disaster recovery, instance control, none, operations or security compliance. If the dependency goes offline, these functions might be impacted. Definitions for each available values are as follows:

   access management
   :   Authentication, authorization and governance of the customer users access to the service and service instances.

   availability
   :   Availability of the service and service instances.

   change management
   :   Deployment, upgrade, patch, and so on of the service and service instances.

   configuration management
   :   Deployment, upgrade, patch, and so on of the service and service instances.

   customer responsibility
   :   Functions provides by customers to support specific service and service instances function. For example: {{site.data.keyword.keymanagementservicefull_notm}} instances provided by customer to support service BYOK encryption.

   disaster recovery
   :   Backup, recovery, restart of the service and service instances in case of disruption.

   instance control
   :   Creation, deletion, start, stop actions on lifecycle of the service instances.

   none
   :   No function impacted.

   operations
   :   Monitoring, troubleshooting, etc of the service and service instances.

   security compliance
   :   Vulnerability management and other security and compliance management of the service and service instances.

- The **Customer provided** column will show if there is any dependency that has been provided by the customer to enable specific functionality. (for example: To properly configure and set up using BYOK into a service, the customer would provision a service like {{site.data.keyword.keymanagementservicefull_notm}}. But there may be other examples like this.) For details on how to enable the features and which services you need to provision, please see the documentation on the service.

- **Where do dependency services need to be deployed regarding my service?** In the Location of dependency column you can view if the dependency is located in the same region or deployed to a specific data center. You can use this data with the data in the Control or data plane column for a quick reference to identify if your data leaves the region or not in a standard setup.

   To find where your service can be deployed, see [Service and infrastructure availability by location](/docs/overview?topic=overview-services_region).

   The table shows a standard cloud deployment. If a special deployment is used like Fedramp or other region-bound deployment models, the data might differ from the details available in the table. Refer to the specific deployment that you are using for that information.
   {: note}

- **Where are the separate control plane and data plane located, if applicable?** Sometimes, the dependency might have a separate control plane and data plane. In these cases, there are separate lines that show the location in relation to the deployed customer instance of the service where these will be provisioned. The lines might have different impacts and different functions. See the Control or data plane column to understand what possible impact this type of outage might have.

   Same region means that the dependent services are in the same region as the provisioned instance. Other values might show data center or region names if the service must be used from a specific region, a specific availability zone, or set of availability zones. If a service is tied to a specific region or site, and the region goes offline, the service might go offline as well. It is recommended that you go through the high availability and disaster recovery documentation of the dependency to determine if there are any steps that you should take to mitigate these types of risks.


For more information about the policies that are related to the services, you can refer to the following resources:

* [Service Level Agreement](https://www.ibm.com/support/customer/csol/terms/?id=i126-6605&lc=en){: external}
* [Shared responsibilities for using {{site.data.keyword.cloud_notm}} products](/docs/overview?topic=overview-shared-responsibilities)
* [Service and infrastructure availability by location](/docs/overview?topic=overview-services_region)
