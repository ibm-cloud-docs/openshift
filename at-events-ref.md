---

copyright: 
  years: 2014, 2025
lastupdated: "2025-05-29"


keywords: openshift, {{site.data.keyword.openshiftlong_notm}}, kubernetes, audit

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}


# {{site.data.keyword.logs_full_notm}} events
{: #at_events_ref}

You can view, manage, and audit user-initiated activities in your {{site.data.keyword.openshiftlong}} community Kubernetes or {{site.data.keyword.redhat_openshift_notm}} cluster by using the {{site.data.keyword.logs_full_notm}} service.
{: shortdesc}

{{site.data.keyword.openshiftlong_notm}} automatically generates cluster management events and forwards these event logs to {{site.data.keyword.logs_full_notm}}.


## Cluster events
{: #clusters-events}


|Action|Description|
|------|-----------|
| `containers-kubernetes.cluster.config` | The Kubernetes configuration file (`kubeconfig`) for a cluster is requested. Depending on the request, the `kubeconfig` might contain administrator or network certificates and secrets to access the cluster. |
| `containers-kubernetes.cluster.create` | The creation of a cluster is requested. This event is sent for any type of cluster, such as clusters that are created in different infrastructure providers. |
| `containers-kubernetes.cluster.create-handler` | During cluster creation, this event signals the creation of the cluster network microservices. This event is sent for any type of cluster, such as clusters that are created in different infrastructure providers.  |
| `containers-kubernetes.cluster.list` | Clusters are listed. The list might be filtered by details such as the infrastructure provider. |
| `containers-kubernetes.cluster.delete` | A cluster is deleted. |
| `containers-kubernetes.cluster.get` | Details for a cluster are returned. |
| `containers-kubernetes.cluster-apikey-owner.get` | The API key owner for the region and resource group that the cluster is in is returned. |
| `containers-kubernetes.cluster-audit-webhook.delete` | A cluster audit webhook for forwarding master API server audit logs is removed. |
| `containers-kubernetes.cluster-audit-webhook.get` | Audit webhooks for a cluster are listed. |
| `containers-kubernetes.cluster-audit-webhook.update` | A cluster audit webhook for forwarding master API server audit logs is updated. |
| `containers-kubernetes.cluster-ca-certificate.create` | A certificate authority (CA) for a cluster is created. |
| `containers-kubernetes.cluster-ca-certificate.get` | A certificate authority (CA) for a cluster is retrieved. |
| `containers-kubernetes.cluster-ca-certificate.rotate` | The certificate authority (CA) for a cluster is rotated. |
| `containers-kubernetes.image-security.enable` | Image security is enabled. |
| `containers-kubernetes.image-security.disable` | Image security is disabled. |
| `containers-kubernetes.cluster-key-state.update` | The root key in the key management service (KMS) provider that the cluster uses is updated, such as a root key being enabled, disabled, or rotated in a key management service (KMS) provider.|
| `containers-kubernetes.cluster-kms.enable` | A key management service (KMS) provider is enabled for a cluster. |
| `containers-kubernetes.cluster-master.changed` | A cluster master operation is completed. |
| `containers-kubernetes.cluster-master.refresh` | A cluster master refresh is requested. |
| `containers-kubernetes.cluster-master.update` | A cluster master update is requested. |
| `containers-kubernetes.cluster-private-service-endpoint.disable` | The private cloud service endpoint for a cluster is disabled. |
| `containers-kubernetes.cluster-private-service-endpoint.enable` | The private cloud service endpoint for a cluster is enabled. |
| `containers-kubernetes.cluster-public-service-endpoint.disable` | The public cloud service endpoint for a cluster is disabled. |
| `containers-kubernetes.cluster-public-service-endpoint.enable` | The public cloud service endpoint for a cluster is enabled. |
| `containers-kubernetes.cluster-pull-secret.enable` | An image pull secret to {{site.data.keyword.registrylong_notm}} is created in the `default` project of the cluster. |
| `containers-kubernetes.cluster-rbac.apply` | {{site.data.keyword.cloud_notm}} IAM service access roles are synchronized with Kubernetes RBAC roles in the cluster. This event commonly happens while retrieving the Kubernetes configuration file (`kubeconfig`) for a cluster (the `containers-kubernetes.cluster.config` event). |
| `containers-kubernetes.cluster-rbac.update` | The {{site.data.keyword.cloud_notm}} IAM service access roles are synchronized with Kubernetes RBAC roles in the cluster. This event commonly happens after you update the service access role for a user in IAM. |
| `containers-kubernetes.cluster-rbac.status` | The status of the RBAC roles in the cluster is retrieved. |
| `containers-kubernetes.cluster-service.bind` | An {{site.data.keyword.cloud_notm}} service is bound to the cluster.|
| `containers-kubernetes.cluster-service.list` | The {{site.data.keyword.cloud_notm}} services that are bound to a cluster are listed. The list might be filtered by the cluster project.|
| `containers-kubernetes.cluster-service.unbind` | An {{site.data.keyword.cloud_notm}} service is removed from the cluster. |
| `containers-kubernetes.cluster-ssl-certificate.update` | An update for a named SSL certificate is initiated. |
| `containers-kubernetes.cluster-subnet.add` | A public or private portable subnet is added to a cluster. |
| `containers-kubernetes.cluster-subnet.create` | A public or private subnet is created for the cluster. |
| `containers-kubernetes.cluster-subnet.detach` | A public or private portable subnet is detached from a cluster.  |
| `containers-kubernetes.cluster-subnet.list` | The classic or VPC subnets for a cluster are listed. |
| `containers-kubernetes.cluster-user-subnet.add` | A user-managed subnet is added to the cluster. **Note**: User-added subnets are deprecated. |
| `containers-kubernetes.cluster.user-subnet.detach` | A user-managed subnet is detached from the cluster. **Note**: User-added subnets are deprecated. |
| `containers-kubernetes.cluster-user-subnet.list` | User-added subnets for a cluster are listed. **Note**: User-added subnets are deprecated. |
| `containers-kubernetes.cluster-webhook.create` | A cluster webhook, such as for Slack, is created. |
| `containers-kubernetes.cluster-webhook.list` | Webhooks for a cluster are listed. |
| `containers-kubernetes.version.update` | A master patch update is initiated for the cluster. Master patch updates are typically applied automatically by IBM to your cluster. |
{: caption="Cluster events" caption-side="bottom"}

## Cluster account events
{: #cluster-account-events}


|Action|Description|
|------|-----------|
| `containers-kubernetes.account-api-key.reset` | The API key that is used for all clusters in the region and resource group is set to the requesting user's API key credentials. |
| `containers-kubernetes.account-customer-root-key.list` | Root keys from key management service instances for the {{site.data.keyword.cloud_notm}} account are listed. |
| `containers-kubernetes.account-datacenter-vlan.list` | VLANs in an {{site.data.keyword.cloud_notm}} account for a particular data center are listed.|
| `containers-kubernetes.account-infra-credential.delete` | Classic infrastructure credentials for managing clusters in the region and resource group are deleted. |
| `containers-kubernetes.account-infra-credential.get` | Details on the classic infrastructure credentials that are set for managing clusters in the region and resource group are returned. |
| `containers-kubernetes.account-infra-credential.set` | Classic infrastructure credentials for managing clusters in the region and resource group are set. |
| `containers-kubernetes.account-infra-permission.get` | Details on the compute, networking, and storage classic infrastructure permissions that are set for managing clusters in the region and resource group are returned. |
| `containers-kubernetes.account-key-management-service-instance.list` | Key management service instances in the {{site.data.keyword.cloud_notm}} account are listed. |
| `containers-kubernetes.account-quota.get` | The quota for resources such as clusters or worker nodes for the {{site.data.keyword.cloud_notm}} account is returned. |
| `containers-kubernetes.account-reservation-contract.add` | A contract for a specific term and number of worker nodes is added to a reservation. |
| `containers-kubernetes.account-reservation-contract.list` | Contracts for a reservation are listed. |
| `containers-kubernetes.account-subnet.list` | Subnets in the {{site.data.keyword.cloud_notm}} classic infrastructure account are listed. |
| `containers-kubernetes.account-subnet-vlan-spanning.get` | Details on whether the {{site.data.keyword.cloud_notm}} account has VLAN spanning enabled are returned. |
| `containers-kubernetes.account-user-config.get` | Details on whether a user can create in a certain region and resource group are returned. |
| `containers-kubernetes.account-vpc.get` | Details for a virtual private cloud (VPC) instance are returned. |
| `containers-kubernetes.account-vpc.list` | Virtual private cloud (VPC) instances in the {{site.data.keyword.cloud_notm}} account are listed.  |
| `containers-kubernetes.account-worker-reservation.create` | A reservation for worker nodes is created. |
| `containers-kubernetes.account-worker-reservation.get` | Details of a reservation are returned. |
| `containers-kubernetes.account-worker-reservation.list` | Reservations are listed.|
{: caption="Cluster account events" caption-side="bottom"}

## Cluster add-on events
{: #cluster-addons}


|Action|Description|
|------|-----------|
| `containers-kubernetes.cluster-addon.disable` | A cluster add-on is disabled. |
| `containers-kubernetes.cluster-addon.enable` | A cluster add-on is enabled.|
| `containers-kubernetes.cluster-addon.list` | Cluster add-ons are listed. |
| `containers-kubernetes.cluster-addon.update` | A cluster add-on is updated. |
| `containers-kubernetes.cluster-addon-dashboard.start` | The Kubernetes dashboard proxy is started. |
| `containers-kubernetes.cluster-addon-debugtool-dashboard.start` | The diagnostics and debug tool add-on dashboard is started. |
| `containers-kubernetes.cluster-addon-terminal.start` | **Deprecated**: Starts the Kubernetes web terminal proxy. |
{: caption="Cluster add-on events" caption-side="bottom"}

## Fluentd logging events
{: #at-fluentd}

|Action|Description|
|------|-----------|
| `containers-kubernetes.cluster-logging-autoupdate.changed` | The logging update policy for the cluster is updated. |
| `containers-kubernetes.cluster-logging-autoupdate.get` | The details of the logging update policy for the cluster are returned. |
| `containers-kubernetes.cluster-logging-config.create` | A logging configuration for the cluster is created. |
| `containers-kubernetes.cluster-logging-config.delete` | A logging configuration is deleted from the cluster.|
| `containers-kubernetes.cluster-logging-config.get` | The details of a logging configuration for the cluster are returned. |
| `containers-kubernetes.cluster-logging-config.refresh` | The logging configuration for the cluster is refreshed. |
| `containers-kubernetes.cluster-logging-config.update` | A logging configuration for the cluster is updated. |
| `containers-kubernetes.cluster-logging-filter.create` | A logging filter configuration for the cluster is created. |
| `containers-kubernetes.cluster-logging-filter.delete` | A logging filter configuration is deleted from the cluster. |
| `containers-kubernetes.cluster-logging-filter.get` | The details of a logging filter configuration are returned. |
{: caption="Fluentd logging events" caption-side="bottom"}


## Ingress ALB events
{: #ingress-alb-events}


|Action|Description|
|------|-----------|
| `containers-kubernetes.cluster-ingress-instance.create` | An Ingress instance is created. |
| `containers-kubernetes.cluster-ingress-instance.delete` | An Ingress instance is delete.|
| `containers-kubernetes.cluster-ingress-instance.update` | An Ingress instance is update. |
| `containers-kubernetes.cluster-ingress-instance.list` | Ingress instances are lists. |
| `containers-kubernetes.cluster-ingress-instance.get` | An Ingress instance is retrieved. |
| `containers-kubernetes.cluster-ingress-status-state.set` | The state of the Ingress status is set. |
| `containers-kubernetes.cluster-ignored-ingress-status-errors.add` | An Ingress status error is added to the ignore list. |
| `containers-kubernetes.cluster-ignored-ingress-status-errors.remove` | An Ingress status error is removed from the ignore list. |
| `containers-kubernetes.cluster-alb.create` | A public or private ALB is created in the cluster. |
| `containers-kubernetes.cluster-alb.delete` | An ALB is disabled. |
| `containers-kubernetes.cluster-alb.enable` | An existing ALB is enabled in a cluster. |
| `containers-kubernetes.cluster-alb.get` | Details of an ALB are viewed. |
| `containers-kubernetes.cluster-alb-healthcheck.get` | Details of an ALB health check are viewed. |
| `containers-kubernetes.cluster-alb-healthcheck.set` | Details of an ALB health check are viewed. |
| `containers-kubernetes.cluster-alb.list` | ALBs in a cluster are listed. |
| `containers-kubernetes.cluster-alb.update` | ALB pods are updated. |
| `containers-kubernetes.cluster-alb-policy.get` | The status of automatic updates for Ingress ALBs is viewed. |
| `containers-kubernetes.cluster-alb-migration.start` | A migration of {{site.data.keyword.cloud_notm}} Ingress ConfigMap and Ingress resources to the Kubernetes Ingress format is started. |
| `containers-kubernetes.cluster-alb-migration-status.get` | The status of the migration process is viewed. |
| `containers-kubernetes.cluster-ingress-status.get` | The status of migrated Ingress resources in a cluster is viewed. |
| `containers-kubernetes.cluster-alb-migration.cleanup` | Ingress resources and configmaps that are no longer needed after an Ingress migration are deleted. |
| `containers-kubernetes.cluster-alb-policy.update` | Automatic updates for the ALBs are enabled or disabled, or all ALB pods in a cluster are rolled back to their previously running build. |
| `containers-kubernetes.alb-image.list` | Supported Ingress controller images are listed. |
{: caption="Ingress ALB events" caption-side="bottom"}


## Ingress secret events
{: #ingress-secret-events}

|Action|Description|
|------|-----------|
| `containers-kubernetes.cluster-ingress-secret.get` | Details for an Ingress secret are viewed. |
| `containers-kubernetes.cluster-ingress-secret.list` | Ingress secrets for a cluster are listed. |
| `containers-kubernetes.cluster-ingress-secret.create` | An Ingress secret for a certificate is created. |
| `containers-kubernetes.cluster-ingress-secret.delete` | An Ingress secret is deleted from the cluster. |
| `containers-kubernetes.cluster-ingress-secret.update` | The certificate for an Ingress secret is updated. |
| `containers-kubernetes.cluster-ingress-secret-field.add` | A field in an Ingress secret is added. |
| `containers-kubernetes.cluster-ingress-secret-field.remove` | A field in an Ingress secret is removed. |
{: caption="Ingress secret events" caption-side="bottom"}

## Observability events for logging and monitoring
{: #at-lm}


|Action|Description|
|------|-----------|
| `containers-kubernetes.observe-logging.create` | A {{site.data.keyword.logs_full_notm}} configuration is created for the cluster. |
| `containers-kubernetes.observe-logging.get` | The details of a {{site.data.keyword.logs_full_notm}} configuration are returned. |
| `containers-kubernetes.observe-logging.list` | {{site.data.keyword.logs_full_notm}} configurations for a cluster are listed. |
| `containers-kubernetes.observe-logging.modify` | A {{site.data.keyword.logs_full_notm}} configuration is updated. |
| `containers-kubernetes.observe-logging.remove` | A {{site.data.keyword.logs_full_notm}} configuration is removed from the cluster.|
| `containers-kubernetes.observe-monitoring.create` | A {{site.data.keyword.mon_short}} configuration is created for the cluster. |
| `containers-kubernetes.observe-monitoring.get` | The details of a {{site.data.keyword.mon_short}} configuration are returned. |
| `containers-kubernetes.observe-monitoring.list` | {{site.data.keyword.mon_short}} configurations for a cluster are listed. |
| `containers-kubernetes.observe-monitoring.modify` | A {{site.data.keyword.mon_short}} configuration is updated. |
| `containers-kubernetes.observe-monitoring.remove` | A {{site.data.keyword.mon_short}} configuration is removed from the cluster. |
{: caption="Observability events for logging and monitoring" caption-side="bottom"}


## NLB DNS events
{: #ingress-nlb-dns-events}


|Action|Description|
|------|-----------|
| `containers-kubernetes.cluster-nlb-dns.list` | Registered NLB subdomains and NLB IP addresses are listed. |
| `containers-kubernetes.cluster-nlb-dns-monitor.get` | The health check monitor settings for an NLB subdomain are viewed. |
| `containers-kubernetes.cluster-nlb-dns-monitor.list` | The health check monitor settings for all NLB subdomains are listed. |
| `containers-kubernetes.cluster-nlb-dns-monitor-status.list` | The health check status for the IP addresses behind NLB subdomains in a cluster are listed. |
| `containers-kubernetes.cluster-nlb-dns-monitor.create` | A health check monitor for an NLB subdomain is configured. |
| `containers-kubernetes.cluster-ingress-secret.delete` | A secret is removed from an NLB subdomain. |
| `containers-kubernetes.cluster-ingress-secret.update` | Certificates for a secret are regenerated. |
| `containers-kubernetes.cluster-nlb-dns.create` | An NLB subdomain is created and associated with one or more NLB IP addresses (classic) or a hostname (VPC). |
| `containers-kubernetes.cluster-lb-hostname.delete` | The VPC load balancer hostname is removed from the DNS record for an existing NLB subdomain. |
| `containers-kubernetes.cluster-lb-hostname.update` | The DNS record for an NLB subdomain in a VPC cluster is updated by replacing the load balancer hostname. |
| `containers-kubernetes.cluster-nlb-dns.update` | A DNS record in a classic cluster is updated by adding an NLB IP address. |
| `containers-kubernetes.cluster-nlb-dns-monitor.update` | The health check monitor for an NLB subdomain is enabled or disabled. |
{: caption="NLB DNS events" caption-side="bottom"}


## Private service endpoint allowlist events
{: #acl-events}

Private service endpoint allowlists are deprecated and support ends on 10 February 2025. Migrate from allowlists to context based restrictions as soon as possible. For more information, see [Migrating from a private service endpoint allowlist to context based restrictions (CBR)](/docs/openshift?topic=openshift-pse-to-cbr-migration).
{: deprecated}

The following table lists the actions related to access control lists (ACLs) and the generation of events for clusters that use a private cloud service endpoint allowlist.
{: shortdesc}

| Action  | Description  |
|---------|--------------|
| `containers-kubernetes.network.acl.delete` | The private cloud service endpoint allowlist feature for a cluster is disabled. |
| `containers-kubernetes.network.acl.get` | The subnet allowlist for the private cloud service endpoint of a cluster is requested.  |
| `containers-kubernetes.network.acl.update` | The private cloud service endpoint allowlist feature for a cluster is enabled, subnets are added to the allowlist, or subnets are removed from the allowlist. |
{: caption="ACL events" caption-side="bottom"}


## {{site.data.keyword.satelliteshort}} events
{: #satellite-events}

See the [{{site.data.keyword.satellitelong_notm}} documentation](/docs/satellite?topic=satellite-at_events).
{: shortdesc}

## Storage events
{: #storage-events}

The following table lists the actions related to storage resources and the generation of events.
{: shortdesc}

| Action  | Description  |
|---------|--------------|
| `containers-kubernetes.storage-volume.delete` | A volume is deleted. |
| `containers-kubernetes.storage-volume.list` | Volumes in the {{site.data.keyword.cloud_notm}} account or as filtered by provider are retrieved. |
| `containers-kubernetes.storage-volume.read` | A volume is retrieved |
| `containers-kubernetes.storage-volume.update` | A volume is updated. |
| `containers-kubernetes.storage-attachment.create` | A volume attachment is created. |
| `containers-kubernetes.storage-attachment.delete` | A volume attachment is deleted. |
| `containers-kubernetes.storage-attachment.list` | Volume attachments are retrieved. |
| `containers-kubernetes.storage-attachment.read` | A volume attachment is retrieved. |
| `containers-kubernetes.storage-odf.install` | The OpenShift Data Foundation add-on is enabled. |
| `containers-kubernetes.storage-odf.uninstall` The OpenShift Data Foundation add-on is disabled or the cluster is deleted. |
{: caption="Storage events" caption-side="bottom"}


## Worker node and worker pool events
{: #worker-events}


|Action|Description|
|------|-----------|
| `containers-kubernetes.cluster-worker.add` | A worker node is added to the cluster. **Note**: Adding stand-alone worker nodes is deprecated. |
| `containers-kubernetes.cluster-worker.list` | The worker nodes for a cluster are listed. |
| `containers-kubernetes.cluster-worker-pool.create` | A worker pool is created in the cluster. |
| `containers-kubernetes.cluster-worker-pool.delete` | A worker pool is deleted from a cluster. |  
| `containers-kubernetes.cluster-worker-pool.get` | The details of a worker pool in the cluster are returned. |
| `containers-kubernetes.cluster-worker-pool.list` | The worker pools for a cluster are listed. |
| `containers-kubernetes.cluster-worker-pool.rebalance` | A worker pool is rebalanced. |
| `containers-kubernetes.cluster-worker-pool.resize` | A worker pool is resized, to add or decrease the number of worker nodes in the pool. |
| `containers-kubernetes.cluster-worker-pool-autoscale.disable` | Autoscaling the worker pool is disabled.|  
| `containers-kubernetes.cluster-worker-pool-autoscale.enable` | Autoscaling the worker pool is enabled. |
| `containers-kubernetes.cluster-worker-pool-label.set` | Kubernetes labels for a worker pool are set. Existing and future worker nodes in the worker pool inherit the label. |
| `containers-kubernetes.cluster-worker-pool-taint.set` | Kubernetes taints for a worker pool are set. Existing and future worker nodes in the worker pool inherit the taint. |
| `containers-kubernetes.cluster-worker-pool-zone.create` | A zone is added to a worker pool. |
| `containers-kubernetes.cluster-worker-pool-zone.delete` | A zone is deleted from a worker pool. |
| `containers-kubernetes.cluster-worker-pool-zone.get` | The details of a zone that a worker pool spans in the cluster are returned as part of cluster autoscaler operations. |
| `containers-kubernetes.cluster-worker-pool-zone.list` | The worker pools for a cluster in a particular zone are listed as part of cluster autoscaler operations. |
| `containers-kubernetes.cluster-worker-pool-zone.resize` | A worker node is added to or removed from a zone that the worker pool spans.|
| `containers-kubernetes.cluster-worker-pool-zone-network.add` | The networking data, such as public and private VLAN data, is added for a zone that the worker pool spans.|
| `containers-kubernetes.cluster-worker-pool-zone-worker.list` | The worker nodes within a zone that a the worker pool spans are listed as part of cluster autoscaler operations. |
| `containers-kubernetes.worker.delete` | A worker node is deleted from the cluster. |
| `containers-kubernetes.worker.get` | The details of a worker node in the cluster are returned. |
| `containers-kubernetes.worker.reboot` | A worker node is rebooted. |
| `containers-kubernetes.worker.reload` | A worker node is reloaded. |
| `containers-kubernetes.worker.replace`| A worker node is removed and another worker node of the same flavor is created in the cluster. |
| `containers-kubernetes.worker.update` | A worker node version is updated. |
{: caption="Worker node and worker pool events" caption-side="bottom"}

## Viewing your cluster events
{: #at-ui}

To [view events](/docs/cloud-logs?topic=cloud-logs-getting-started) you select the {{site.data.keyword.logs_full_notm}} instance that matches with the location of your {{site.data.keyword.openshiftlong_notm}} cluster.
{: shortdesc}

The following table shows the {{site.data.keyword.logs_full_notm}} location where your events are sent to. To view your events, make sure that you have an instance in the location that matches your cluster location. Note that clusters in the Montreal, Toronto, and Washington, D.C. locations forward all events to the Dallas location.

| {{site.data.keyword.openshiftlong_notm}} classic location | {{site.data.keyword.logs_full_notm}} event location |
|-----|-----|
| Dallas (dal10, dal12, dal13) | Dallas |
| Montreal (mon01) | Washington, D.C. |
| San Jose (sjc03, sjc04) | Dallas |
| São Paulo (sao01) | Dallas |
| Toronto (tor01) | Toronto |
| Washington, D.C. (wdc04, wdc06, wdc07) | Washington, D.C. |
| Amsterdam (ams03) | Frankfurt |
| Frankfurt (fra02, fra04, fra05) | Frankfurt |
| Milan (mil01) | Frankfurt |
| Paris (par01) | Frankfurt |
| London (lon02, lon04, lon05, lon06) | London |
| Sydney (syd01, syd04, syd05) | Sydney |
| Chennai (che01) | Chennai |
| Seoul (seo01) | Seoul |
| Osaka (osa21, osa22, osa23) | Osaka |
| Singapore (sng01) | Tokyo |
| Tokyo (tok02, tok04, tok05) | Tokyo |
{: caption="Corresponding {{site.data.keyword.logs_full_notm}} instance and {{site.data.keyword.openshiftlong_notm}} cluster locations." caption-side="bottom"}



| {{site.data.keyword.openshiftlong_notm}} VPC location | {{site.data.keyword.logs_full_notm}} event location |
|-----|-----|
| Dallas (us-south-1, us-south-2, us-south-3) | Dallas |
| Frankfurt (eu-de-1, eu-de-2, eu-de-3) | Frankfurt |
| London (eu-gb-1, eu-gb-2, eu-gb-3) | London |
| Madrid (eu-es-1, eu-es-2, eu-es-3) | Madrid |
| São Paulo (br-sao-1, br-sao-2, br-sao-3) | Dallas |
| Sydney (au-syd-1, au-syd-2, au-syd-3) | Sydney |
| Tokyo (jp-tok-1, jp-tok-2, jp-tok-3) | Tokyo |
| Toronto (ca-tor-1, ca-tor-2, ca-tor-3) | Toronto |
| Washington, D.C. (us-east-1, us-east-2, us-east-3) | Washington, D.C. |
{: caption="Corresponding {{site.data.keyword.logs_full_notm}} instance and {{site.data.keyword.openshiftlong_notm}} cluster locations." caption-side="bottom"}
