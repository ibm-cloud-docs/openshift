---

copyright: 
  years: 2022, 2022
lastupdated: "2022-11-04"

keywords: openshift

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}


# Classic infrastructure roles
{: #classic-roles}

A user with the **Super User** infrastructure access role [sets the API key for a region and resource group](/docs/openshift?topic=openshift-access-creds) so that infrastructure actions can be performed (or more rarely, [manually sets different account credentials](/docs/openshift?topic=openshift-access-creds#credentials). Then, the infrastructure actions that other users in the account can perform is authorized through {{site.data.keyword.cloud_notm}} IAM platform access roles. You don't need to edit the other users' classic infrastructure permissions. Use the following table to customize users' classic infrastructure permissions only when you can't assign **Super User** to the user who sets the API key. For instructions to assign permissions, see [Customizing infrastructure permissions](/docs/openshift?topic=openshift-access-creds#infra_access).
{: shortdesc}


Classic infrastructure permissions apply only to classic clusters. For VPC clusters, see [Granting user permissions for VPC resources](/docs/vpc?topic=vpc-managing-user-permissions-for-vpc-resources).
{: note}


Need to check that the API key or manually set credentials have the required and suggested infrastructure permissions? Use the `ibmcloud oc infra-permissions get` [command](/docs/openshift?topic=openshift-kubernetes-service-cli#infra_permissions_get).
{: tip}

The following table shows the classic infrastructure permissions that the credentials for a region and resource group can have for creating clusters and other common use cases. The description includes how you can assign the permission in the {{site.data.keyword.cloud_notm}} IAM Classic infrastructure console or the `ibmcloud sl` command. For more information, see the instructions for the [console](/docs/openshift?topic=openshift-access-creds#infra_console) or [CLI](/docs/openshift?topic=openshift-access-creds#infra_cli).

Create clusters
:    Classic infrastructure permissions that you must have to create a cluster. When you run `ibmcloud oc infra-permissions get`, these permissions are listed as **Required**. For other service permissions that you must have in {{site.data.keyword.cloud_notm}} IAM to create clusters, see [Permissions to create a cluster](/docs/openshift?topic=openshift-access_reference).

Other common use cases
:    Classic infrastructure permissions that you must have for other common scenarios. Even if you have permission to create a cluster, some limitations might apply. For example, you might not be able to create or work with a cluster with bare metal worker nodes or a public IP address. After cluster creation, further steps to add networking or storage resources might fail. When you run `ibmcloud oc infra-permissions get`, these permissions are listed as **Suggested**.

## Required classic infrastructure permissions
{: #required-classic-rbac}

| Permission | Description | IAM Assign Policy Console | CLI |
|:-----------------|:-----------------|:---------------|:----|
| IPMI Remote Management | Manage worker nodes.|Classic infrastructure > Permissions > Devices| `ibmcloud sl user permission-edit <user_id> --permission REMOTE_MANAGEMENT --enable true` |
| Add Server | Add worker nodes.   \n   \n  **Note**: For worker nodes that have public IP addresses, you also need the **Add Compute with Public Network Port** permission in the **Network** category. | Add Server: Classic infrastructure > Permissions > Account  \n  \n  Add Compute with Public Network Port: Classic infrastructure > Permissions > Network |Add Server:  `ibmcloud sl user permission-edit <user_id> --permission SERVER_ADD --enable true`  Add Compute with Public Network Port:  `ibmcloud sl user permission-edit <user_id> --permission PUBLIC_NETWORK_COMPUTE --enable true`|
| Cancel Server | Delete worker nodes. | Classic infrastructure > Permissions > Account| `ibmcloud sl user permission-edit <user_id> --permission SERVER_CANCEL --enable true`  |
| OS Reloads and Rescue Kernel | Update, reboot, and reload worker nodes. | Classic infrastructure > Permissions > Devices| `ibmcloud sl user permission-edit <user_id> --permission SERVER_RELOAD --enable true`  |
| View Virtual Server Details | Required if the cluster has VM worker nodes. List and get details of VM worker nodes. | Classic infrastructure > Permissions > Devices| `ibmcloud sl user permission-edit <user_id> --permission VIRTUAL_GUEST_VIEW --enable true`  |
| View Hardware Details | Required if the cluster has bare metal worker nodes. List and get details of bare metal worker nodes. | Classic infrastructure > Permissions > Devices| `ibmcloud sl user permission-edit <user_id> --permission HARDWARE_VIEW --enable true`  |
| Add Support Case | As part of the cluster creation automation, support cases are opened to provision the cluster infrastructure. | - | `ibmcloud sl user permission-edit <user_id> --permission TICKET_ADD --enable true`  |
| Edit Support Case | As part of the cluster creation automation, support cases are updated to provision the cluster infrastructure. | - | `ibmcloud sl user permission-edit <user_id> --permission TICKET_EDIT --enable true`  |
| View Support Case | As part of the cluster creation automation, support cases are used to provision the cluster infrastructure. | - | `ibmcloud sl user permission-edit <user_id> --permission TICKET_VIEW --enable true`  |
{: caption="Table 1: Required classic infrastructure permissions" caption-side="bottom"}


## Suggested classic infrastructure permissions
{: #classic-rbac-suggested}

| Permission | Description | IAM Assign Policy Console | CLI |
|:-----------------|:-----------------|:---------------|:----|
| Access All Virtual | Designate access to all VM worker nodes. Without this permission, a user who creates one cluster might not be able to view the VM worker nodes of another cluster even if the user has IAM access to both clusters. | Classic infrastructure > Devices > Check All virtual servers and Auto virtual server access| `ibmcloud sl user permission-edit <user_id> --permission ACCESS_ALL_GUEST --enable true` |
| Access All Hardware | Designate access to all bare metal worker nodes.  Without this permission, a user who creates one cluster might not be able to view the bare metal worker nodes of another cluster even if the user has IAM access to both clusters. | Classic infrastructure > Devices > Check All bare metal servers and Auto bare metal server access| `ibmcloud sl user permission-edit <user_id> --permission ACCESS_ALL_HARDWARE --enable true` |
| Add Compute with Public Network Port | Let worker nodes have a port that can be accessible on the public network. | Classic infrastructure > Permissions > Network| `ibmcloud sl user permission-edit <user_id> --permission PUBLIC_NETWORK_COMPUTE --enable true` |
| Manage DNS | Set up public load balancer or Ingress networking to expose apps. | Classic infrastructure > Permissions > Services| `ibmcloud sl user permission-edit <user_id> --permission DNS_MANAGE --enable true` |
| Edit Hostname/Domain | Set up public load balancer or Ingress networking to expose apps. | Classic infrastructure > Permissions > Devices| `ibmcloud sl user permission-edit <user_id> --permission HOSTNAME_EDIT --enable true` |
| Add IP Addresses | Add IP addresses to public or private subnets that are used for cluster load balancing. | Classic infrastructure > Permissions > Network| `ibmcloud sl user permission-edit <user_id> --permission IP_ADD --enable true` |
| Manage Network Subnet Routes | Manage public and private VLANs and subnets that are used for cluster load balancing. | Classic infrastructure > Permissions > Network| `ibmcloud sl user permission-edit <user_id> --permission NETWORK_ROUTE_MANAGE --enable true` |
| Manage Port Control | Manage ports that are used for app load balancing. | Classic infrastructure > Permissions > Devices| `ibmcloud sl user permission-edit <user_id> --permission PORT_CONTROL --enable true` |
| Manage Certificates (SSL) | Set up certificates that are used for cluster load balancing. | Classic infrastructure > Permissions > Services| `ibmcloud sl user permission-edit <user_id> --permission SECURITY_CERTIFICATE_MANAGE --enable true`  |
| View Certificates (SSL) | Set up certificates that are used for cluster load balancing. | Classic infrastructure > Permissions > Services| `ibmcloud sl user permission-edit <user_id> --permission SECURITY_CERTIFICATE_VIEW --enable true` |
| Add/Upgrade Storage (Storage Layer) | Create {{site.data.keyword.cloud_notm}} File or Block storage instances to attach as volumes to your apps for persistent storage of data. | Classic infrastructure > Permissions > Account| `ibmcloud sl user permission-edit <user_id> --permission ADD_SERVICE_STORAGE --enable true`  |
| Storage Manage | Manage {{site.data.keyword.cloud_notm}} File or Block storage instances that are attached as volumes to your apps for persistent storage of data. | Classic infrastructure > Permissions > Services| `ibmcloud sl user permission-edit <user_id> --permission NAS_MANAGE --enable true` |
{: caption="Table 2: Suggested classic infrastructure permissions" caption-side="bottom"}

