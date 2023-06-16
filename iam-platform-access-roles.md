---

copyright: 
  years: 2014, 2023
lastupdated: "2023-06-16"

keywords: openshift

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}




# IAM platform access roles
{: #iam-platform-access-roles}

{{site.data.keyword.openshiftlong_notm}} is configured to use {{site.data.keyword.cloud_notm}} IAM Identity Service roles. {{site.data.keyword.cloud_notm}} IAM platform access roles determine the actions that users can perform on {{site.data.keyword.cloud_notm}} resources such as clusters, worker nodes, and Ingress application load balancers (ALBs). {{site.data.keyword.cloud_notm}} IAM platform access roles also automatically set basic infrastructure permissions for users. To assign platform access roles, see [Granting users access to your cluster through {{site.data.keyword.cloud_notm}} IAM](/docs/openshift?topic=openshift-users#checking-perms).
{: shortdesc}

See the IAM Policy Management [API reference](https://cloud.ibm.com/apidocs/iam-policy-management#list-roles){: external} for more information on managing IAM roles with the API.
{: tip}

Do not assign {{site.data.keyword.cloud_notm}} IAM platform access roles at the same time as a service access role. You must assign platform and service access roles separately.
{: tip}

- **Actions requiring no permissions**: Any user in your account who runs the CLI command or makes the API call for the action sees the result, even if the user has no assigned permissions.
- **Viewer actions**: The Viewer platform access role includes the actions that require no permissions, plus the permissions that are shown in the Viewer tab of following table. With the Viewer role, users such as auditors or billing can see cluster details but not modify the infrastructure.
- **Editor actions**: The Editor platform access role includes the permissions that are granted by Viewer, plus the following. With the Editor role, users such as developers can bind services, work with Ingress resources, and set up log forwarding for their apps but can't modify the infrastructure.
- **Operator actions**: The Operator platform access role includes the permissions that are granted by Viewer, plus the permissions that are shown in the Operator tab of the following table. With the Operator role, users such as site reliability engineers, DevOps engineers, or cluster administrators can add worker nodes and troubleshoot infrastructure such as by reloading a worker node, but can't create or delete the cluster, change the credentials, or set up cluster-wide features like service endpoints or managed add-ons.
- **Administrator actions**: The Administrator platform access role includes all permissions that are granted by the Viewer, Editor, and Operator roles, plus the permissions that are show in the Administrator tab of the following table. With the Administrator role, users such as cluster or account administrators can create and delete clusters or set up cluster-wide features like service endpoints or managed add-ons. To create order such infrastructure resources such as worker node machines, VLANs, and subnets, Administrator users need the Super user [infrastructure role](/docs/openshift?topic=openshift-classic-roles) or the API key for the region must be set with the appropriate permissions.


{{../account/iam-service-roles.md#containers-kubernetes-roles}}





