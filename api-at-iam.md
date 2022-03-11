---

copyright: 
  years: 2014, 2022
lastupdated: "2022-03-10"

keywords: openshift

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}


# IAM and {{site.data.keyword.cloudaccesstrailshort}} action by API method
{: #api-at-iam}

When you use {{site.data.keyword.openshiftlong}} such as through the command line or console, the service calls application programming interface (API) methods to complete your requests. In {{site.data.keyword.cloud_notm}} IAM, each API operation is associated with an IAM action that the user must have an access role to use the API operation. You can keep track of the requests that you make with an {{site.data.keyword.at_full_notm}} instance.
{: shortdesc}

Review the following list of {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM) actions and {{site.data.keyword.at_full_notm}} events that correspond to each API method in {{site.data.keyword.openshiftlong_notm}}.

For more information, see the following topics.
- [{{site.data.keyword.openshiftlong_notm}} API docs](https://containers.cloud.ibm.com/global/swagger-global-api/#/){: external}
- [User access permissions](/docs/containers?topic=containers-access_reference)
- [{{site.data.keyword.at_full_notm}} events](/docs/containers?topic=containers-at_events).

## Account
{: #ks-account}

Review the following account API methods, their corresponding actions in {{site.data.keyword.cloud_notm}} IAM, and the events that are sent to {{site.data.keyword.at_full_notm}} for {{site.data.keyword.openshiftlong_notm}}.
{: shortdesc}

| API Method | Description | IAM action for the API | Event sent to {{site.data.keyword.cloudaccesstrailshort}} |
| --- | --- | --- | --- |
| `DELETE​/v1​/credentials` | Remove {{site.data.keyword.cloud_notm}} infrastructure account credentials from your {{site.data.keyword.openshiftlong_notm}} account. | `containers-kubernetes.cluster.create` | `containers-kubernetes.account.delete` |
| `GET​/v1​/addons` | List available add-ons that you can enable in a cluster. | - | - |
| `GET​/v1​/config` | List configuration values for your {{site.data.keyword.cloud_notm}} account. | `containers-kubernetes.cluster.read` | - |
| `GET​/v1​/credentials` | View the {{site.data.keyword.cloud_notm}} infrastructure account credentials that are set for your {{site.data.keyword.openshiftlong_notm}} account. | `containers-kubernetes.cluster.read` | - |
| `GET​/v1​/datacenters​/{datacenter}​/machine-types` | List available machine types for a zone (data center). | - | - |
| `GET​/v1​/datacenters​/{datacenter}​/vlans` | List available VLANs for a zone. | - | - |
| `GET​/v1​/infra-permissions` | Get details on the permissions that the {{site.data.keyword.cloud_notm}} infrastructure credentials have. | `containers-kubernetes.cluster.read` | - |
| `GET​/v1​/kube-versions` | Deprecated: List available Kubernetes versions. | - | - |
| `GET​/v1​/locations` | List available locations. | - | - |
| `GET​/v1​/messages` | View the current user messages. | - | - |
| `GET​/v1​/prodconfig` | List product-specific values to substitute for variables in other files. | - | - |
| `GET​/v1​/regions` | Deprecated: List available Kubernetes Service regions. | - | - |
| `GET​/v1​/subnets` | List available {{site.data.keyword.cloud_notm}} infrastructure subnets. | `containers-kubernetes.cluster.read` | - |
| `GET​/v1​/subnets​/vlan-spanning` | View the VLAN spanning status. | `containers-kubernetes.cluster.read` | - |
| `GET​/v1​/user-config` | View a user's ability to create free and standard clusters in a region and resource group. | `containers-kubernetes.cluster.read` | - |
| `GET​/v1​/versions` | List available {{site.data.keyword.openshiftlong_notm}} versions. | `containers-kubernetes.cluster.read` | - |
| `GET​/v1​/zones` | List available zones (data centers). | - | - |
| `GET​/v2​/getMessages` | View the current user messages. | - | - |
| `GET​/v2​/getQuota` | View the quota for resources per region in the account. | `containers-kubernetes.cluster.read` | - |
| `GET​/v2​/getVersions` | List available {{site.data.keyword.openshiftlong_notm}} versions. | `containers-kubernetes.cluster.read` | - |
| `GET​/v2​/vpc​/getZones` | List available zones in a region. | - | - |
| `POST​/v1​/credentials` | Set {{site.data.keyword.cloud_notm}} infrastructure account credentials for your {{site.data.keyword.openshiftlong_notm}} account. | `containers-kubernetes.cluster.create` | - |
| `POST​/v1​/keys` | Reset the IAM API key. | `containers-kubernetes.cluster.create` | - |
{: summary="The rows are read from left to right. The first column is the API method. The second column is a description of the method. The third column is the action that the user must have an access policy to the service in {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM), if any. The fourth column is the event that is sent for the method to {{site.data.keyword.at_full_notm}} instance, if any."}
{: caption="Account API methods, IAM actions, and {{site.data.keyword.cloudaccesstrailshort}} events."}



## Cluster
{: #ks-cluster}

Review the following cluster API methods, their corresponding actions in {{site.data.keyword.cloud_notm}} IAM, and the events that are sent to {{site.data.keyword.at_full_notm}} for {{site.data.keyword.openshiftlong_notm}}.
{: shortdesc}

| API Method | Description | IAM action for the API | {{site.data.keyword.cloudaccesstrailshort}} event |
| --- | --- | --- | --- |
| `DELETE​/v1​/clusters​/{idOrName}` | Delete a cluster. | `containers-kubernetes.cluster.create` | `containers-kubernetes.cluster.delete` |
| `DELETE​/v1​/clusters​/{idOrName}​/apiserverconfigs​/auditwebhook` | Delete an audit webhook configuration. | `containers-kubernetes.cluster.operate` | `containers-kubernetes.cluster.delete`  |
| `DELETE​/v1​/clusters​/{idOrName}​/services​/{namespace}​/{serviceInstanceId}` | Unbind an {{site.data.keyword.cloud_notm}} service from a cluster. | `containers-kubernetes.cluster.operate` | `containers-kubernetes.service.delete` |
| `DELETE​/v1​/clusters​/{idOrName}​/usersubnets​/{subnetId}​/vlans​/{vlanId}` | Remove a user-managed subnet from a cluster. | `containers-kubernetes.cluster.operate` | `containers-kubernetes.vlan.delete`  |
| `GET​/v1​/clusters` | List the clusters that you have access to. | `containers-kubernetes.cluster.read` | - |
| `GET​/v1​/clusters​/{idOrName}` | View details for a cluster. | `containers-kubernetes.cluster.read` | - |
| `GET​/v1​/clusters​/{idOrName}​/addons` | View details of the add-ons that are enabled in a cluster. | `containers-kubernetes.cluster.read` | - |
| `GET​/v1​/clusters​/{idOrName}​/apiserverconfigs​/auditwebhook` | View details for an audit webhook configuration. | `containers-kubernetes.cluster.read` | - |
| `GET​/v1​/clusters​/{idOrName}​/config` | Get the cluster-specific configuration and certificates. | `containers-kubernetes.cluster.read` | `containers-kubernetes.cluster.config` |
| `GET​/v1​/clusters​/{idOrName}​/services` | List the {{site.data.keyword.cloud_notm}} services bound to a cluster across all namespaces. | `containers-kubernetes.cluster.read` | - |
| `GET​/v1​/clusters​/{idOrName}​/services​/{namespace}` | List the {{site.data.keyword.cloud_notm}} services bound to a specific namespace in a cluster. | `containers-kubernetes.cluster.read` | - |
| `GET​/v1​/clusters​/{idOrName}​/subnets` | List subnets from your {{site.data.keyword.cloud_notm}} infrastructure account that are bound to a cluster. | `containers-kubernetes.cluster.read` | - |
| `GET​/v1​/clusters​/{idOrName}​/usersubnets` | List user-managed subnets that are bound to a cluster. | `containers-kubernetes.cluster.read` | - |
| `GET​/v1​/clusters​/{idOrName}​/webhooks` | List all webhooks for a cluster. | `containers-kubernetes.cluster.read` | - |
| `GET​/v1​/clusters​/{idOrName}​/workerpools` | List the worker pools in a cluster. | `containers-kubernetes.cluster.read` | - |
| `GET​/v2​/classic​/getCluster` | Get detailed cluster information. | `containers-kubernetes.cluster.read` | - |
| `GET​/v2​/classic​/getClusters` | List the classic clusters that you have access to. | `containers-kubernetes.cluster.read` | - |
| `GET​/v2​/classic​/getVLANs` | List available classic infrastructure VLANs for a zone. | `containers-kubernetes.cluster.read` | - |
| `GET​/v2​/getCluster` | View details for a cluster. | `containers-kubernetes.cluster.read` | - |
| `GET​/v2​/getClusterAddons` | View details of the add-ons that are enabled in a cluster. | `containers-kubernetes.cluster.read` | - |
| `GET​/v2​/getCRKs` | List the root keys for a key management service (KMS) instance. | `containers-kubernetes.cluster.read` | - |
| `GET​/v2​/getFlavors` | List available flavors types for a VPC zone (data center). | - | - |
| `GET​/v2​/getKMSInstances` | Get key management service (KMS) instances tied to an account | `containers-kubernetes.cluster.read` | - |
| `GET​/v2​/getKubeconfig` | Get the cluster's `kubeconfig` file. Optionally include the network configuration file. | `containers-kubernetes.cluster.read` | `containers-kubernetes.account.get` |
| `GET​/v2​/vpc​/getCluster` | Get detailed information for a VPC cluster. | `containers-kubernetes.cluster.read` | - |
| `GET​/v2​/vpc​/getClusters` | List the VPC clusters that you have access to. | `containers-kubernetes.cluster.read` | - |
| `GET​/v2​/vpc​/getSubnets` | View subnets for a given VPC. | `containers-kubernetes.cluster.read` | - |
| `GET​/v2​/vpc​/getVPC` | View details of a VPC. | `containers-kubernetes.cluster.read` | - |
| `GET​/v2​/vpc​/getVPCs` | View available VPCs for the infrastructure provider. | `containers-kubernetes.cluster.read` | - |
| `PATCH​/v1​/clusters​/{idOrName}​/addons` | Enable, disable, or update add-ons for a cluster. | `containers-kubernetes.cluster.create` | `containers-kubernetes.cluster.update`  |
| `PATCH​/v1​/clusters​/{idOrName}​/subnets​/{subnetId}` | Detach a public or private portable subnet from a cluster. | `containers-kubernetes.cluster.operate` | | `containers-kubernetes.subnet.update` |  |
| `POST​/v1​/clusters` | Create a cluster. | `containers-kubernetes.cluster.create` | `containers-kubernetes.cluster.create` |
| `POST​/v1​/clusters​/{idOrName}​/kms` | Create a key management service (KMS) provider configuration for a cluster. | `containers-kubernetes.cluster.create` | `containers-kubernetes.account.update` |
| `POST​/v1​/clusters​/{idOrName}​/services` | Bind an {{site.data.keyword.cloud_notm}} service to a cluster. | `containers-kubernetes.cluster.update` | `containers-kubernetes.service.create` |
| `POST​/v1​/clusters​/{idOrName}​/usersubnets`   | Add an existing user-managed subnet to a cluster. | `containers-kubernetes.cluster.operate` | `containers-kubernetes.subnet.create`  |
| `POST​/v1​/clusters​/{idOrName}​/vlans​/{vlanId}` | Create an {{site.data.keyword.cloud_notm}} infrastructure subnet and add it to an existing cluster. | `containers-kubernetes.cluster.create` | `containers-kubernetes.vlan.create`  |
| `POST​/v1​/clusters​/{idOrName}​/webhooks` | Add a webhook to a cluster. | `containers-kubernetes.cluster.update` | `containers-kubernetes.cluster.create` |
| `POST​/v2​/applyRBACAndGetKubeconfig` | Apply IAM roles to the cluster, then retrieve the cluster's `kubeconfig` file. Optionally include the network configuration file. | `containers-kubernetes.cluster.create` | `containers-kubernetes.cluster.update` |
| `POST​/v2​/autoUpdateMaster` | Set the `autoupdate` status of the cluster master. | `containers-kubernetes.cluster.create` | containers-kubernetes.account.update  |
| `POST​/v2​/disablePrivateServiceEndpoint` | Disable a private cloud service endpoint for a cluster. | `containers-kubernetes.cluster.create` | containers-kubernetes.cluster.update   |
| `POST​/v2​/disablePublicServiceEndpoint` | Disable a public cloud service endpoint for a cluster. | `containers-kubernetes.cluster.create` | `containers-kubernetes.cluster.update` |
| `POST​/v2​/enableKMS` | Enable a key management service (KMS) for a cluster | `containers-kubernetes.cluster.create` | containers-kubernetes.account.update |
| `POST​/v2​/enablePrivateServiceEndpoint` | Enable the private cloud service endpoint for a cluster. | `containers-kubernetes.cluster.create` | `containers-kubernetes.cluster.update` |
| `POST​/v2​/enablePublicServiceEndpoint` | Enable the public cloud service endpoint for a cluster. | `containers-kubernetes.cluster.create` | `containers-kubernetes.cluster.update` |
| `POST​/v2​/enablePullSecret` | Create image pull secret to {{site.data.keyword.registrylong_notm}} in the default Kubernetes namespace. | `containers-kubernetes.cluster.operate` | `containers-kubernetes.cluster.update` |
| `POST​/v2​/refreshMaster` | Refresh the Kubernetes master. | `containers-kubernetes.cluster.operate` | `containers-kubernetes.account.update` |
| `POST​/v2​/updateMaster` | Update the version of the Kubernetes cluster master node. | `containers-kubernetes.cluster.operate` | `containers-kubernetes.account.update` |
| `POST​/v2​/vpc​/createCluster` | Create a VPC cluster. | `containers-kubernetes.cluster.create` | `containers-kubernetes.cluster.create` |
| `PUT​/v1​/clusters​/{idOrName}` | Update the version of the Kubernetes cluster master node. | `containers-kubernetes.cluster.operate` | `containers-kubernetes.cluster.update` |
| `PUT​/v1​/clusters​/{idOrName}​/apiserverconfigs​/auditwebhook` | Create or update an audit webhook configuration for a cluster. | `containers-kubernetes.cluster.update` | `containers-kubernetes.cluster.update`  |
| `PUT​/v1​/clusters​/{idOrName}​/masters` | Refresh the Kubernetes master. | `containers-kubernetes.cluster.operate` | `containers-kubernetes.cluster.update` |
| `PUT​/v1​/clusters​/{idOrName}​/subnets​/{subnetId}` | Add an existing {{site.data.keyword.cloud_notm}} infrastructure subnet to an existing cluster. | `containers-kubernetes.cluster.operate` | `containers-kubernetes.subnet.update`  |
{: summary="The rows are read from left to right. The first column is the API method. The second column is a description of the method. The third column is the action that the user must have an access policy to the service in {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM), if any. The fourth column is the event that is sent for the method to {{site.data.keyword.at_full_notm}} instance, if any."}
{: caption="Cluster API methods, IAM actions, and {{site.data.keyword.cloudaccesstrailshort}} events."}



## Ingress
{: #ks-ingress}

Review the following Ingress API methods, their corresponding actions in {{site.data.keyword.cloud_notm}} IAM, and the events that are sent to {{site.data.keyword.at_full_notm}} for {{site.data.keyword.openshiftlong_notm}}.
{: shortdesc}

| API Method | Description | IAM action for the API | {{site.data.keyword.cloudaccesstrailshort}} event |
| --- | --- | --- | --- |
| `GET​/ingress​/v2​/secret​/getSecret`   | View Ingress secret details. | `containers-kubernetes.cluster.create` | `cluster-ingress-secret.get` |
| `GET​/ingress​/v2​/secret​/getSecrets` | View Ingress secrets for a cluster. | `containers-kubernetes.cluster.create` | `cluster-ingress-secret.list` |
| `POST​/ingress​/v2​/secret​/createSecret` | Create an Ingress secret for a certificate. | `containers-kubernetes.cluster.create` | `cluster-ingress-secret.create` |
| `POST​/ingress​/v2​/secret​/deleteSecret` | Delete an Ingress secret from the cluster. | `containers-kubernetes.cluster.create` | `cluster-ingress-secret.delete` |
| `POST​/ingress​/v2​/secret​/updateSecret` | Update an Ingress secret for a certificate. | `containers-kubernetes.cluster.create` | `cluster-ingress-secret.update` |
| `GET/ingress/v2/load-balancer/configuration` | Get the configuration of load balancers for Ingress ALBs. | `containers-kubernetes.cluster.read` |  |
| `PATCH/ingress/v2/load-balancer/configuration` | Update the configuration of load balancers for Ingress ALBs. | `containers-kubernetes.cluster.operate` |  |
{: summary="The rows are read from left to right. The first column is the API method. The second column is a description of the method. The third column is the action that the user must have an access policy to the service in {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM), if any. The fourth column is the event that is sent for the method to {{site.data.keyword.at_full_notm}} instance, if any."}
{: caption="Ingress API methods, IAM actions, and {{site.data.keyword.cloudaccesstrailshort}} events."}



## Ingress ALB
{: #ks-alb}

Review the following Ingress application load balancer (ALB) API methods, their corresponding actions in {{site.data.keyword.cloud_notm}} IAM, and the events that are sent to {{site.data.keyword.at_full_notm}} for {{site.data.keyword.openshiftlong_notm}}.
{: shortdesc}

| API Method | Description | IAM action for the API | {{site.data.keyword.cloudaccesstrailshort}} event |
| --- | --- | --- | --- |
| `DELETE​/v1​/alb​/albs​/{albID}` | Disable an ALB in a classic cluster. | `containers-kubernetes.cluster.update` | `cluster-alb.delete` |
| `DELETE​/v1​/alb​/clusters​/{idOrName}​/albsecrets` | Delete an ALB secret that is imported from {{site.data.keyword.cloudcerts_short}} from a classic cluster. | `containers-kubernetes.cluster.create` | `cluster-ingress-secret.delete` |
| `GET​/v1​/alb​/albs​/{albID}` | View details of an ALB in a classic cluster. | `containers-kubernetes.cluster.read` | `cluster-alb.get` |
| `GET​/v1​/alb​/albtypes` | List the ALB types that are supported in classic clusters. | `containers-kubernetes.cluster.read` | - | |
| `GET​/v1​/alb​/clusters​/{idOrName}`   | List all ALBs in a classic cluster. | `containers-kubernetes.cluster.read` | `cluster-alb.list` |
| `GET​/v1​/alb​/clusters​/{idOrName}​/albsecrets` | View details of an ALB secret that you imported from {{site.data.keyword.cloudcerts_short}} to a classic cluster. | `containers-kubernetes.cluster.create` | `cluster-ingress-secret.list` |
| `GET​/v1​/alb​/clusters​/{idOrName}​/updatepolicy` | Check if automatic updates for Ingress ALBs are enabled in a classic cluster. | `containers-kubernetes.cluster.update` | `cluster-alb-policy.get` |
| `GET​/v2​/alb​/getAlb` | View details of an ALB. | `containers-kubernetes.cluster.read` | `cluster-alb.get` |
| `GET​/v2​/alb​/getAlbImages` | List supported Ingress controller images. | `containers-kubernetes.cluster.read` | `alb-image.list` |
| `GET​/v2​/alb​/getClusterAlbs` | List all ALBs in a cluster. | `containers-kubernetes.cluster.read` | `cluster-alb.list` |
| `GET​/v2​/alb​/getMigrationStatus` | Get the status of the Ingress migration process. | `containers-kubernetes.cluster.read` | `cluster-alb-migration-status.get` |
| `GET​/v2​/alb​/getStatus` | Get the status of the Ingress resources in a cluster. | `containers-kubernetes.cluster.read` | `cluster-ingress-status.get` |
| `POST​/v1​/alb​/albs` | Enable an existing ALB in a classic cluster. | `containers-kubernetes.cluster.update` | `cluster-alb.enable` |
| `POST​/v1​/alb​/albsecrets` | Import an ALB secret from {{site.data.keyword.cloudcerts_short}} to a cluster. | `containers-kubernetes.cluster.create` | `cluster-ingress-secret.create` |
| `POST​/v1​/alb​/clusters​/{idOrName}​/zone​/{zoneId}` | Create a public or private ALB in a classic cluster. | `containers-kubernetes.cluster.update` | `cluster-alb.create` |
| `POST​/v2​/alb​/cleanupMigration` | Clean up any Ingress resources and configmaps that are no longer needed after an Ingress migration. | `containers-kubernetes.cluster.create` | `cluster-alb-migration.cleanup` |
| `POST​/v2​/alb​/startMigration` | Start a migration of your {{site.data.keyword.cloud_notm}} Ingress configmap and Ingress resources to the Kubernetes Ingress format. | `containers-kubernetes.cluster.create` | `cluster-alb-migration.start` |
| `POST​/v2​/alb​/updateAlb` | Update ALBs in a cluster. | `containers-kubernetes.cluster.update` | `cluster-alb.update` |
| `POST​/v2​/alb​/vpc​/createAlb` | Create a public or private ALB in a VPC cluster. | `containers-kubernetes.cluster.update` | `cluster-alb.create` |
| `POST​/v2​/alb​/vpc​/disableAlb` | Disable an ALB in a VPC cluster. | `containers-kubernetes.cluster.update` | `cluster-alb.delete` |
| `POST​/v2​/alb​/vpc​/enableAlb` | Enable an existing ALB in a VPC cluster. | `containers-kubernetes.cluster.update` | `cluster-alb.enable` |
| `PUT​/v1​/alb​/albsecrets` | Update an ALB secret that you imported from {{site.data.keyword.cloudcerts_short}}. | `containers-kubernetes.cluster.create` | `cluster-ingress-secret.update` |
| `PUT​/v1​/alb​/clusters​/{idOrName}​/update` | Force a one-time update of all ALB pods to the latest build. | `containers-kubernetes.cluster.update` | `cluster-alb.update` |
| `PUT​/v1​/alb​/clusters​/{idOrName}​/updatepolicy` | Enable or disable automatic updates for the Ingress ALBs in a cluster. | `containers-kubernetes.cluster.update` | `cluster-alb-policy.update` |
| `PUT​/v1​/alb​/clusters​/{idOrName}​/updaterollback` | Roll back all ALB pods in a cluster to their previously running build. | `containers-kubernetes.cluster.update` | `cluster-alb-policy.update` |
{: summary="The rows are read from left to right. The first column is the API method. The second column is a description of the method. The third column is the action that the user must have an access policy to the service in {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM), if any. The fourth column is the event that is sent for the method to {{site.data.keyword.at_full_notm}} instance, if any."}
{: caption="ALB API methods, IAM actions, and {{site.data.keyword.cloudaccesstrailshort}} events."}



## Fluentd logging
{: #ks-logging}

Review the following Fluentd logging configuration API methods, their corresponding actions in {{site.data.keyword.cloud_notm}} IAM, and the events that are sent to {{site.data.keyword.at_full_notm}} for {{site.data.keyword.openshiftlong_notm}}.
{: shortdesc}

| API Method | Description | IAM action for the API | {{site.data.keyword.cloudaccesstrailshort}} event |
| --- | --- | --- | --- |
| `DELETE​/v1​/logging​/{idOrName}​/filterconfigs` | Deletes all logging filter configurations for the cluster. | `containers-kubernetes.cluster.update` | `containers-kubernetes.logging-filter.delete`  |
| `DELETE​/v1​/logging​/{idOrName}​/filterconfigs​/{id}` | Delete a logging filter configuration. | `containers-kubernetes.cluster.update` | `containers-kubernetes.logging-filter.delete`  |
| `DELETE​/v1​/logging​/{idOrName}​/loggingconfig` | Delete all log forwarding configurations for a cluster. | `containers-kubernetes.cluster.update` | `containers-kubernetes.logging-config.delete`  |
| `DELETE​/v1​/logging​/{idOrName}​/loggingconfig​/{logSource}​/{id}` | Delete a log forwarding configuration. | `containers-kubernetes.cluster.update` | `containers-kubernetes.logging-config.delete`  |
| `GET​/v1​/log-collector​/{idOrName}​/masterlogs` | Show the status for the most recent master log collection request. | `containers-kubernetes.cluster.read` | `containers-kubernetes.masterlog-status`  |
| `GET​/v1​/logging​/{idOrName}​/clusterkeyowner` | View information about the containers-kubernetes-key API key owner. | `containers-kubernetes.cluster.read` | - |
| `GET​/v1​/logging​/{idOrName}​/default` | View the default logging endpoint for the target region. | `containers-kubernetes.cluster.read` | - |
| `GET​/v1​/logging​/{idOrName}​/filterconfigs` | List all logging filter configurations in the cluster. | `containers-kubernetes.cluster.read` | - |
| `GET​/v1​/logging​/{idOrName}​/filterconfigs​/{id}` | View a logging filter configuration. | `containers-kubernetes.cluster.read` | - |
| `GET​/v1​/logging​/{idOrName}​/loggingconfig` | List all log forwarding configurations in the cluster. | `containers-kubernetes.cluster.read` | - |
| `GET​/v1​/logging​/{idOrName}​/loggingconfig​/{logSource}` | List all log forwarding configurations for a log source in the cluster. | `containers-kubernetes.cluster.read` | - |
| `GET​/v1​/logging​/{idOrName}​/updatepolicy` | Check if automatic updates for the Fluentd logging add-on are enabled in the cluster. | `containers-kubernetes.cluster.read` | - |
| `POST​/v1​/log-collector​/{idOrName}​/masterlogs` | Create a new master log collection request. | `containers-kubernetes.cluster.create` | `containers-kubernetes.masterlog-retrieve`  |
| `POST​/v1​/logging​/{idOrName}​/filterconfigs` | Create a logging filter configuration. | `containers-kubernetes.cluster.update` | `containers-kubernetes.logging-filter.create`  |
| `POST​/v1​/logging​/{idOrName}​/loggingconfig​/{logSource}` | Create a log forwarding configuration. | `containers-kubernetes.cluster.update` | `containers-kubernetes.logging-config.create`  |
| `PUT​/v1​/logging​/{idOrName}​/filterconfigs​/{id}` | Update a logging filter configuration. | `containers-kubernetes.cluster.update` | - |
| `PUT​/v1​/logging​/{idOrName}​/loggingconfig​/{logSource}​/{id}` | Update a log forwarding configuration. | `containers-kubernetes.cluster.update` | - |
| `PUT​/v1​/logging​/{idOrName}​/refresh` | Refresh the cluster's logging configuration. | `containers-kubernetes.cluster.update` | `containers-kubernetes.logging-config.refresh`  |
| `PUT​/v1​/logging​/{idOrName}​/updatepolicy` | Enable or disable automatic updates for the Fluentd logging add-on in the cluster. | `containers-kubernetes.cluster.create` | `containers-kubernetes.logging-autoupdate.changed`  |
{: summary="The rows are read from left to right. The first column is the API method. The second column is a description of the method. The third column is the action that the user must have an access policy to the service in {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM), if any. The fourth column is the event that is sent for the method to {{site.data.keyword.at_full_notm}} instance, if any."}
{: caption="Logging API methods, IAM actions, and {{site.data.keyword.cloudaccesstrailshort}} events."}



## NLB DNS
{: #ks-nlb-dns}

Review the following network load balancer (NLB) domain name system (DNS) API methods, their corresponding actions in {{site.data.keyword.cloud_notm}} IAM, and the events that are sent to {{site.data.keyword.at_full_notm}} for {{site.data.keyword.openshiftlong_notm}}.
{: shortdesc}                                    

| API Method | Description | IAM action for the API | {{site.data.keyword.cloudaccesstrailshort}} event |
| --- | --- | --- | --- |
| `DELETE​/v1​/nlb-dns​/clusters​/{idOrName}​/host​/{nlbHost}​/ip​/{nlbIP}​/remove` | Remove an IP address from an NLB subdomain. | `containers-kubernetes.cluster.update` | `cluster-nlb-dns.delete` |
| `GET​/v1​/nlb-dns​/clusters​/{idOrName}​/list` | List registered NLB subdomains and NLB IP addresses. | `containers-kubernetes.cluster.read` | `cluster-nlb-dns.list` |
| `GET​/v1​/nlb-dns​/health​/clusters​/{idOrName}​/host​/{nlbHost}​/config` | View the health check monitor settings for an NLB subdomain. | `containers-kubernetes.cluster.read` | `cluster-nlb-dns-monitor.get` |
| `GET​/v1​/nlb-dns​/health​/clusters​/{idOrName}​/list` | List the health check monitor settings for all NLB subdomains. | `containers-kubernetes.cluster.read` | `cluster-nlb-dns-monitor.list` |
| `GET​/v1​/nlb-dns​/health​/clusters​/{idOrName}​/status` | List the health check status for the IPs behind NLB subdomains in a cluster. | `containers-kubernetes.cluster.read` | `cluster-nlb-dns-monitor-status.list` |
| `GET​/v2​/nlb-dns​/getNlbDNSList` | List registered NLB subdomains in a cluster. | `containers-kubernetes.cluster.read` | `cluster-nlb-dns.list` |
| `PATCH​/v1​/nlb-dns​/health​/clusters​/{idOrName}​/config` | Configure a health check monitor for an NLB subdomain. | `containers-kubernetes.cluster.update` | `cluster-nlb-dns-monitor.create` |
| `POST​/v1​/nlb-dns​/clusters​/{idOrName}​/register` | Create a NLB subdomain and associate one or more NLB IP addresses with it. | `containers-kubernetes.cluster.update` | `cluster-nlb-dns.update` |
| `POST​/v2​/nlb-dns​/deleteSecret` | Remove a secret from an NLB subdomain. | `containers-kubernetes.cluster.update` | `cluster-ingress-secret.delete` |
| `POST​/v2​/nlb-dns​/regenerateCert` | Regenerate certificates for a secret. | `containers-kubernetes.cluster.update` | `cluster-ingress-secret.update` |
| `POST​/v2​/nlb-dns​/vpc​/createNlbDNS` | Create a NLB subdomain in a VPC cluster and associate a load balancer hostname with it. | `containers-kubernetes.cluster.update` | `cluster-nlb-dns.create` |
| `POST​/v2​/nlb-dns​/vpc​/removeLBHostname` | Remove the load balancer hostname from the DNS record for an existing NLB subdomain. | `containers-kubernetes.cluster.update` | `cluster-lb-hostname.delete` |
| `POST​/v2​/nlb-dns​/vpc​/ReplaceLBHostname` | Update the DNS record for an NLB subdomain by replacing the load balancer hostname. | `containers-kubernetes.cluster.update` | `cluster-lb-hostname.update` |
| `PUT​/v1​/nlb-dns​/clusters​/{idOrName}​/add` | Update a DNS record by adding an NLB IP address. | `containers-kubernetes.cluster.update` | `cluster-nlb-dns.update` |
| `PUT​/v1​/nlb-dns​/clusters​/{idOrName}​/health` | Enable or disable a health check monitor for an NLB subdomain. | `containers-kubernetes.cluster.update` | `cluster-nlb-dns-monitor.update` |
{: summary="The rows are read from left to right. The first column is the API method. The second column is a description of the method. The third column is the action that the user must have an access policy to the service in {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM), if any. The fourth column is the event that is sent for the method to {{site.data.keyword.at_full_notm}} instance, if any."}
{: caption="NLB DNS API methods, IAM actions, and {{site.data.keyword.cloudaccesstrailshort}} events."}



## Observability: {{site.data.keyword.la_short}}
{: #ks-observability-logging}

Review the following observability logging API methods, their corresponding actions in {{site.data.keyword.cloud_notm}} IAM, and the events that are sent to {{site.data.keyword.at_full_notm}} for {{site.data.keyword.openshiftlong_notm}}.
{: shortdesc}                                

| API Method | Description | IAM action for the API | {{site.data.keyword.cloudaccesstrailshort}} event |
| --- | --- | --- | --- |
| `GET​/v2​/observe​/logging​/getConfig` | Show the details of an existing {{site.data.keyword.la_short}} configuration. | `containers-kubernetes.cluster.read` | - |
| `GET​/v2​/observe​/logging​/getConfigs` | List all {{site.data.keyword.la_short}} configurations for a cluster. | `containers-kubernetes.cluster.read` | - |
| `POST​/v2​/observe​/logging​/createConfig` | Create a {{site.data.keyword.la_short}} configuration for a cluster. | `containers-kubernetes.cluster.create` | `containers-kubernetes.observe.logging.create`  |
| `POST​/v2​/observe​/logging​/discoverAgent` | Discover a {{site.data.keyword.la_short}} agent previously deployed in the cluster. | `containers-kubernetes.cluster.create` | - |
| `POST​/v2​/observe​/logging​/modifyConfig` | Update a {{site.data.keyword.la_short}} configuration in the cluster. | `containers-kubernetes.cluster.create` | `containers-kubernetes.observe.logging.modify`  |
| `POST​/v2​/observe​/logging​/removeConfig` | Remove a {{site.data.keyword.la_short}} configuration from a cluster. | `containers-kubernetes.cluster.create` | `containers-kubernetes.observe.logging.remove`  |
{: summary="The rows are read from left to right. The first column is the API method. The second column is a description of the method. The third column is the action that the user must have an access policy to the service in {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM), if any. The fourth column is the event that is sent for the method to {{site.data.keyword.at_full_notm}} instance, if any."}
{: caption="Observability logging API methods, IAM actions, and {{site.data.keyword.cloudaccesstrailshort}} events."}



## Observability: {{site.data.keyword.mon_short}}
{: #ks-observability-monitoring}

Review the following observability monitoring API methods, their corresponding actions in {{site.data.keyword.cloud_notm}} IAM, and the events that are sent to {{site.data.keyword.at_full_notm}} for {{site.data.keyword.openshiftlong_notm}}.
{: shortdesc}

| API Method | Description | IAM action for the API | {{site.data.keyword.cloudaccesstrailshort}} event |
| --- | --- | --- | --- |
| `GET​/v2​/observe​/monitoring​/getConfig` | Show the details of an existing {{site.data.keyword.mon_short}} configuration. | `containers-kubernetes.cluster.read` | - |
| `GET​/v2​/observe​/monitoring​/getConfigs` | List all {{site.data.keyword.mon_short}} configurations for a cluster. | `containers-kubernetes.cluster.read` | - |
| `POST​/v2​/observe​/monitoring​/createConfig` | Create a {{site.data.keyword.mon_short}} configuration for a cluster. | `containers-kubernetes.cluster.create` | `containers-kubernetes.observe.monitoring.create`  |
| `POST​/v2​/observe​/monitoring​/discoverAgent` | Discover a {{site.data.keyword.mon_short}} agent previously deployed in the cluster. | `containers-kubernetes.cluster.create` | - |
| `POST​/v2​/observe​/monitoring​/modifyConfig` | Update a {{site.data.keyword.mon_short}} configuration in the cluster. | `containers-kubernetes.cluster.create` | `containers-kubernetes.observe.monitoring.modify`  |
| `POST​/v2​/observe​/monitoring​/removeConfig` | Remove a {{site.data.keyword.mon_short}} configuration from a cluster. | `containers-kubernetes.cluster.create` | `containers-kubernetes.observe.monitoring.remove`  |
{: summary="The rows are read from left to right. The first column is the API method. The second column is a description of the method. The third column is the action that the user must have an access policy to the service in {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM), if any. The fourth column is the event that is sent for the method to {{site.data.keyword.at_full_notm}} instance, if any."}
{: caption="Observability monitoring API methods, IAM actions, and {{site.data.keyword.cloudaccesstrailshort}} events."}



## Private service endpoint allowlist
{: #ks-acl}

Review the following access control list (ACL) API methods, their corresponding actions in {{site.data.keyword.cloud_notm}} IAM, and the events that are sent to {{site.data.keyword.at_full_notm}} for {{site.data.keyword.openshiftlong_notm}} if you use a private cloud service endpoint allowlist.
{: shortdesc}

| API Method | Description | IAM action for the API | {{site.data.keyword.cloudaccesstrailshort}} event |
| --- | --- | --- | --- |
| `DELETE​/v1​/acl​/{idOrName}` | Disable the private cloud service endpoint allowlist feature for a cluster. | `containers-kubernetes.cluster.create` | `containers-kubernetes.network-acl.delete`  |
| `GET​/v1​/acl​/{idOrName}` | Get the subnets in the private cloud service endpoint allowlist. | `containers-kubernetes.cluster.read` | `containers-kubernetes.network-acl.get`  |
| `PATCH​/v1​/acl​/{idOrName}​/add` | Add subnets to a cluster's private cloud service endpoint allowlist. | `containers-kubernetes.cluster.create` | `containers-kubernetes.network-acl.update`  |
| `PATCH​/v1​/acl​/{idOrName}​/rm` | Remove subnets from a cluster's private cloud service endpoint allowlist. | `containers-kubernetes.cluster.create` | `containers-kubernetes.network-acl.update`  |
| `POST​/v1​/acl​/{idOrName}​/enable` | Enables the private cloud service endpoint allowlist feature for a cluster. | `containers-kubernetes.cluster.create` | `containers-kubernetes.network-acl.update` |
{: summary="The rows are read from left to right. The first column is the API method. The second column is a description of the method. The third column is the action that the user must have an access policy to the service in {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM), if any. The fourth column is the event that is sent for the method to {{site.data.keyword.at_full_notm}} instance, if any."}
{: caption="ACL API methods, IAM actions, and {{site.data.keyword.cloudaccesstrailshort}} events."}



## Satellite
{: #sat-api}

Review the following API methods, their corresponding actions in {{site.data.keyword.cloud_notm}} IAM, and the events that are sent to {{site.data.keyword.at_full_notm}} for {{site.data.keyword.satellitelong_notm}}.
{: shortdesc}                                    

| API Method | Description | IAM action for the API | {{site.data.keyword.cloudaccesstrailshort}} event |
| --- | --- | --- | --- |
| `GET​/v2​/nlb-dns​/getSatLocationSubdomains` | List registered NLB subdomains in a Satellite location. | `containers-kubernetes.cluster.read` | - |
| `POST​/v2​/nlb-dns​/registerMSCDomains` | Register NLB subdomains `c001`, `c002`, and `c003`, which each correspond to an IP address of a host that is assigned to the {{site.data.keyword.satelliteshort}} location control plane. The `c000` subdomain corresponds to all the IP addresses for the cluster. Also, register one CNAME, `ce00`, for the specified {{site.data.keyword.satelliteshort}} location control plane. | `containers-kubernetes.cluster.operate` | - |
| `GET​/v2​/satellite​/getClusters` | List the {{site.data.keyword.cloud_notm}} Satellite clusters that you have access to. | `containers-kubernetes.cluster.read` | - |
| `GET​/v2​/satellite​/getController` | Get the details for an {{site.data.keyword.cloud_notm}} Satellite location. | `containers-kubernetes.cluster.read` | - |
| `GET​/v2​/satellite​/getControllers` | List the {{site.data.keyword.cloud_notm}} Satellite locations that you have access to. | `containers-kubernetes.cluster.read` | - |
| `GET​/v2​/satellite​/hostqueue​/getHosts` | List the hosts in your {{site.data.keyword.cloud_notm}} Satellite location. | `containers-kubernetes.cluster.read` | - |
| `POST​/v2​/satellite​/createCluster` | Create an {{site.data.keyword.cloud_notm}} Satellite cluster. | `containers-kubernetes.cluster.create` | `containers-kubernetes.cluster.create` |
| `POST​/v2​/satellite​/createController` | Create an {{site.data.keyword.cloud_notm}} Satellite location. | `containers-kubernetes.cluster.create` | `containers-kubernetes.cluster.create` |
| `POST​/v2​/satellite​/hostqueue​/createAssignment` | Assign a host to an {{site.data.keyword.cloud_notm}} Satellite location or cluster. | `containers-kubernetes.cluster.operate` | `containers-kubernetes.cluster.create` |
| `POST​/v2​/satellite​/hostqueue​/createRegistrationScript` | Attach a host to an {{site.data.keyword.cloud_notm}} Satellite location. | `containers-kubernetes.cluster.operate` | `containers-kubernetes.cluster.create` |
| `POST​/v2​/satellite​/hostqueue​/removeHost` | Remove a host from an {{site.data.keyword.cloud_notm}} Satellite location or cluster. | `containers-kubernetes.cluster.operate` | `containers-kubernetes.cluster.delete` |
| `POST​/v2​/satellite​/hostqueue​/updateHost` | Update a host in your {{site.data.keyword.cloud_notm}} Satellite location. | `containers-kubernetes.cluster.operate` | `containers-kubernetes.cluster.update` |
| `POST​/v2​/satellite​/removeController` | Remove an {{site.data.keyword.cloud_notm}} Satellite Location. | `containers-kubernetes.cluster.create` | `containers-kubernetes.cluster.delete` |
{: summary="The rows are read from left to right. The first column is the API method. The second column is a description of the method. The third column is the action that the user must have an access policy to the service in {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM), if any. The fourth column is the event that is sent for the method to {{site.data.keyword.at_full_notm}} instance, if any."}
{: caption="{{site.data.keyword.satelliteshort}} API methods, IAM actions, and {{site.data.keyword.cloudaccesstrailshort}} events."}



## Storage
{: #ks-storage}

Review the following storage API methods, their corresponding actions in {{site.data.keyword.cloud_notm}} IAM, and the events that are sent to {{site.data.keyword.at_full_notm}} for {{site.data.keyword.openshiftlong_notm}}.
{: shortdesc}                                    

| API Method | Description | IAM action for the API | {{site.data.keyword.cloudaccesstrailshort}} event |
| --- | --- | --- | --- |
| `GET​/v2​/storage​/getAttachment` | Get details of a storage attachment. | `containers-kubernetes.cluster.read` | `containers-kubernetes.containers-kubernetes.storage.attachment.read`  |
| `GET​/v2​/storage​/getAttachments` | List storage attachments | `containers-kubernetes.cluster.read` | `containers-kubernetes.containers-kubernetes.storage.attachment.read`  |
| `GET​/v2​/storage​/getVolume` | Get the details of a storage volume. | `containers-kubernetes.cluster.read` | `containers-kubernetes.containers-kubernetes.storage.volume.read`  |
| `GET​/v2​/storage​/getVolumes` | List storage volumes for a cluster or for the account if no cluster is provided. | `containers-kubernetes.cluster.read` | `containers-kubernetes.containers-kubernetes.storage.volume.read`  |
| `POST​/v2​/storage​/createAttachment` | Attach a volume to a worker node. | `containers-kubernetes.cluster.update` | `containers-kubernetes.containers-kubernetes.storage.attachment.create`  |
| `POST​/v2​/storage​/deleteAttachment` | Detach a volume from a worker node. | `containers-kubernetes.cluster.update` | `containers-kubernetes.containers-kubernetes.storage.attachment.delete`  |
{: summary="The rows are read from left to right. The first column is the API method. The second column is a description of the method. The third column is the action that the user must have an access policy to the service in {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM), if any. The fourth column is the event that is sent for the method to {{site.data.keyword.at_full_notm}} instance, if any."}
{: caption="Storage API methods, IAM actions, and {{site.data.keyword.cloudaccesstrailshort}} events."}



## Worker nodes and worker pools
{: #ks-workers}

Review the following worker node and worker pool API methods, their corresponding actions in {{site.data.keyword.cloud_notm}} IAM, and the events that are sent to {{site.data.keyword.at_full_notm}} for {{site.data.keyword.openshiftlong_notm}}.
{: shortdesc}

| API Method | Description | IAM action for the API | {{site.data.keyword.cloudaccesstrailshort}} event |
| --- | --- | --- | --- |
| `DELETE​/v1​/clusters​/{idOrName}​/workerpools​/{poolidOrName}` | Remove a worker pool from a cluster. | `containers-kubernetes.cluster.operate` | `containers-kubernetes.workerpool.delete` |
| `DELETE​/v1​/clusters​/{idOrName}​/workerpools​/{poolidOrName}​/zones​/{zoneid}` | Remove a zone from a worker pool. | `containers-kubernetes.cluster.operate` | `containers-kubernetes.zone.delete` |
| `DELETE​/v1​/clusters​/{idOrName}​/workers​/{workerId}` | Delete a worker node from a cluster. | `containers-kubernetes.cluster.operate` | `containers-kubernetes.worker.delete` |
| `GET​/v1​/clusters​/{idOrName}​/workerpools​/{poolidOrName}` | View details for a worker pool. | `containers-kubernetes.cluster.read` | - |
| `GET​/v1​/clusters​/{idOrName}​/workers` | List all worker nodes in a cluster. | `containers-kubernetes.cluster.read` | - |
| `GET​/v1​/clusters​/{idOrName}​/workers​/{workerId}` | View details of a worker node. | `containers-kubernetes.cluster.read` | - |
| `GET​/v2​/classic​/getWorker` | View details of a worker node for classic cluster. | `containers-kubernetes.cluster.read` | - |
| `GET​/v2​/classic​/getWorkerPool` | View details of a worker pool for a classic cluster. | `containers-kubernetes.cluster.read` | - |
| `GET​/v2​/classic​/getWorkerPools` | View details of a worker pool for a classic cluster. | `containers-kubernetes.cluster.read` | - |
| `GET​/v2​/classic​/getWorkers` | View all workers for a classic cluster. | `containers-kubernetes.cluster.read` | - |
| `GET​/v2​/getWorker` | View details of a worker node for cluster. | `containers-kubernetes.cluster.read` | - |
| `GET​/v2​/getWorkerPool` | View details of a worker pool for a cluster. | `containers-kubernetes.cluster.read` | - |
| `GET​/v2​/getWorkerPools` | View details of a worker pool for a cluster. | `containers-kubernetes.cluster.read` | - |
| `GET​/v2​/getWorkers` | View all workers for cluster. | `containers-kubernetes.cluster.read` | - |
| `GET​/v2​/vpc​/getWorker` | View details of a worker node for VPC cluster. | `containers-kubernetes.cluster.read` | - |
| `GET​/v2​/vpc​/getWorkerPool` | View details of a worker pool for a VPC cluster. | `containers-kubernetes.cluster.read` | - |
| `GET​/v2​/vpc​/getWorkerPools` | View details of a worker pool for a VPC cluster. | `containers-kubernetes.cluster.read` | - |
| `GET​/v2​/vpc​/getWorkers` | View all workers for VPC cluster. | `containers-kubernetes.cluster.read` | - |
| `PATCH​/v1​/clusters​/{idOrName}​/workerpools​/{poolidOrName}` | Resize or rebalance a worker pool. | `containers-kubernetes.cluster.operate` | `containers-kubernetes.workerpool.update` |
| `PATCH​/v1​/clusters​/{idOrName}​/workerpools​/{poolidOrName}​/zones​/{zoneid}` | Updates network configuration for a worker pool for a given zone. | `containers-kubernetes.cluster.operate` | `containers-kubernetes.zone.update` |
| `POST​/v1​/clusters​/{idOrName}​/workerpools` | Create a worker pool for a cluster. | `containers-kubernetes.cluster.operate` | `containers-kubernetes.workerpool.create` |
| `POST​/v1​/clusters​/{idOrName}​/workerpools​/{poolidOrName}​/zones` | Add a zone to the specified worker pool for a cluster. | `containers-kubernetes.cluster.operate` | `containers-kubernetes.workerpool.create` |
| `POST​/v1​/clusters​/{idOrName}​/workers` | Add worker nodes to a cluster. | `containers-kubernetes.cluster.operate` | `containers-kubernetes.worker.create` |
| `POST​/v2​/rebalanceWorkerPool` | Rebalance workers in a worker pool. | `containers-kubernetes.cluster.operate` | `containers-kubernetes.account.update` |
| `POST​/v2​/removeWorker` | Delete a worker node from a cluster. | `containers-kubernetes.cluster.operate` | `containers-kubernetes.account.delete` |
| `POST​/v2​/removeWorkerPool` | Removes a worker pool. | `containers-kubernetes.cluster.operate` | `containers-kubernetes.account.delete` |
| `POST​/v2​/replaceWorker` | Replace a worker node with a new worker node. | `containers-kubernetes.cluster.operate` | `containers-kubernetes.account.update` |
| `POST​/v2​/resizeWorkerPool` | Resize an existing worker pool. | `containers-kubernetes.cluster.operate` | `containers-kubernetes.workerpool.update` |
| `POST​/v2​/setWorkerPoolLabels` | Set custom labels for a worker pool. | `containers-kubernetes.cluster.operate` | `containers-kubernetes.account.update` |
| `POST​/v2​/setWorkerPoolTaints` | Set custom taints for a worker pool. | `containers-kubernetes.cluster.operate` | `containers-kubernetes.account.update` |
| `POST​/v2​/vpc​/createWorkerPool` | Create a worker pool for a VPC cluster. | `containers-kubernetes.cluster.operate` | `containers-kubernetes.account.create`  |
| `POST​/v2​/vpc​/createWorkerPoolZone` | Create a zone in the specified worker pool for a VPC cluster. | `containers-kubernetes.cluster.operate` | `containers-kubernetes.account.create`  |
| `POST​/v2​/vpc​/replaceWorker` | Replace a worker node with a new worker node. | `containers-kubernetes.cluster.operate` | `containers-kubernetes.account.create`  |
| `PUT​/v1​/clusters​/{idOrName}​/workers​/{workerId}` | Reboot, reload, or update a worker node for a cluster. | `containers-kubernetes.cluster.operate` | `containers-kubernetes.worker.update`  |
{: summary="The rows are read from left to right. The first column is the API method. The second column is a description of the method. The third column is the action that the user must have an access policy to the service in {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM), if any. The fourth column is the event that is sent for the method to {{site.data.keyword.at_full_notm}} instance, if any."}
{: caption="Worker node and worker pool API methods, IAM actions, and {{site.data.keyword.cloudaccesstrailshort}} events."}




