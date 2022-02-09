---

copyright: 
  years: 2022, 2022
lastupdated: "2022-02-09"

keywords: openshift

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}

# {{site.data.keyword.openshiftlong_notm}} CLI Map
{: #icks_map}

This page lists all `ibmcloud oc` commands as they are structured in the CLI. For more details on a specific command, click on the command or see the [{{site.data.keyword.openshiftlong_notm}} CLI reference](/docs/containers?topic=containers-kubernetes-service-cli).



## ibmcloud oc cluster
{: #icks_map_cluster}

[View and modify cluster and cluster service settings](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster).
{: shortdesc}

* **`cluster addon`**: View, enable, update, and disable cluster add-ons.
    * [`ibmcloud oc cluster addon disable`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_cluster_addon_disable)
    * [`ibmcloud oc cluster addon enable`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_cluster_addon_enable)
    * [`ibmcloud oc cluster addon get`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_cluster_addon_get)
    * [`ibmcloud oc cluster addon ls`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_cluster_addons)
    * [`ibmcloud oc cluster addon options`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_cluster_addon_options)
    * [`ibmcloud oc cluster addon update`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_cluster_addon_update)
    * [`ibmcloud oc cluster addon versions`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_addon_versions)
* **`cluster ca`**: Manage the Certificate Authority (CA) certificates of a cluster.
    * [`ibmcloud oc cluster ca create`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_cluster_ca_create)
    * [`ibmcloud oc cluster ca rotate`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_cluster_ca_rotate)
    * [`ibmcloud oc cluster ca status`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_cluster_ca_status)
* [`ibmcloud oc cluster config`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_cluster_config)
* **`cluster create`**: Create a classic or VPC cluster.
    * [`ibmcloud oc cluster create classic`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_cluster_create)
    * [`ibmcloud oc cluster create vpc-gen2`](/docs/openshift?topic=openshift-kubernetes-service-cli#cli_cluster-create-vpc-gen2)
* [`ibmcloud oc cluster get`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_cluster_get)
* **`cluster image-security`**: Manage image security enforcement in your cluster.
    * [`ibmcloud oc cluster image-security disable`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs-image-security-disable)
    * [`ibmcloud oc cluster image-security enable`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs-image-security-enable)
* [`ibmcloud oc cluster ls`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_clusters)
* **`cluster master`**: View and modify the master for a cluster.
    * **`cluster master audit-webhook`**: View and modify the audit webhook configuration for a cluster's Kubernetes API server.
        * [`ibmcloud oc cluster master audit-webhook get`](/docs/containers?topic=containers-kubernetes-service-cli#cs_apiserver_config_get) 
        * [`ibmcloud oc cluster master audit-webhook set`](/docs/containers?topic=containers-kubernetes-service-cli#cs_apiserver_config_set) 
        * [`ibmcloud oc cluster master audit-webhook unset`](/docs/containers?topic=containers-kubernetes-service-cli#cs_apiserver_config_unset) 
    * **`cluster master private-service-endpoint`**: Manage the private service endpoint of a cluster.
        * **`ibmcloud oc cluster master private-service-endpoint allowlist`**: Manage the private service endpoint allowlist.
            * [`ibmcloud oc cluster master private-service-endpoint allowlist add`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_master_pse_allowlist_add)
            * [`ibmcloud oc cluster master private-service-endpoint allowlist disable`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_master_pse_allowlist_disable)
            * [`ibmcloud oc cluster master private-service-endpoint allowlist enable`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_master_pse_allowlist_enable)
            * [`ibmcloud oc cluster master private-service-endpoint allowlist get`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_master_pse_allowlist_get)
            * [`ibmcloud oc cluster master private-service-endpoint allowlist rm`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_master_pse_allowlist_rm)
        * [`ibmcloud oc cluster master private-service-endpoint enable`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_cluster_master_pse_enable)
    * **`cluster master public-service-endpoint`**: Manage the public service endpoint of a cluster.
        * [`ibmcloud oc cluster master public-service-endpoint disable`](/docs/containers?topic=containers-kubernetes-service-cli#cs_cluster_master_pub_se_disable)
        * [`ibmcloud oc cluster master public-service-endpoint enable`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_cluster_master_pub_se_enable)
    * [`ibmcloud oc cluster master refresh`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_apiserver_refresh)
    * [`ibmcloud oc cluster master update`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_cluster_update)
* **`cluster pull-secret`**: Manage image pull secrets for the cluster to access images in IBM Cloud Container Registry.
    * [`ibmcloud oc cluster pull-secret apply`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_cluster_pull_secret_apply) 
* [`ibmcloud oc cluster rm`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_cluster_rm)
* **`cluster service`**: View, bind, and unbind IBM Cloud services on a cluster.
    * [`ibmcloud oc cluster service bind`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_cluster_service_bind)
    * [`ibmcloud oc cluster service ls`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_cluster_services)
    * [`ibmcloud oc cluster service unbind`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_cluster_service_unbind)
* **`cluster subnet`**: Add and create portable subnets for a classic cluster.
    * [`ibmcloud oc cluster subnet add`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_cluster_subnet_add)
    * [`ibmcloud oc cluster subnet create`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_cluster_subnet_create)
    * [`ibmcloud oc cluster subnet detach`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_cluster_subnet_detach)

## ibmcloud oc worker
{: #icks_map_worker}

[View and modify worker nodes for a cluster](/docs/openshift?topic=openshift-kubernetes-service-cli#worker_node_commands).
{: shortdesc}

* **Deprecated** [`ibmcloud oc worker add`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_add) 
* [`ibmcloud oc worker get`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_get)
* [`ibmcloud oc worker ls`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_workers)
* [`ibmcloud oc worker reboot`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_reboot)
* [`ibmcloud oc worker reload`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_reload)
* [`ibmcloud oc worker replace`](/docs/openshift?topic=openshift-kubernetes-service-cli#cli_worker_replace)
* [`ibmcloud oc worker rm`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_rm)
* [`ibmcloud oc worker update`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_update)

## ibmcloud oc worker-pool
{: #icks_map_worker-pool}

[View and modify worker pools for a cluster](/docs/openshift?topic=openshift-kubernetes-service-cli#worker-pool).
{: shortdesc}

* **`worker-pool create`**: Add a worker pool to a cluster. No worker nodes are created until zones are added to the worker pool.
    * [`ibmcloud oc worker-pool create classic`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_pool_create)
    * [`ibmcloud oc worker-pool create vpc-gen2`](/docs/openshift?topic=openshift-kubernetes-service-cli#cli_worker_pool_create_vpc_gen2)
* [`ibmcloud oc worker-pool get`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_pool_get)
* **`worker-pool label`**: Set and remove custom Kubernetes labels for all worker nodes in a worker pool.
    * [`ibmcloud oc worker-pool label rm`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_pool_label_rm)
    * [`ibmcloud oc worker-pool label set`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_pool_label_set)
* [`ibmcloud oc worker-pool ls`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_pools)
* [`ibmcloud oc worker-pool rebalance`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_rebalance)
* [`ibmcloud oc worker-pool resize`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_pool_resize)
* [`ibmcloud oc worker-pool rm`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_pool_rm)
* **[`worker-pool taint`]**: Set and remove Kubernetes taints for all worker nodes in a worker pool.
    * [`ibmcloud oc worker-pool taint rm`](/docs/openshift?topic=openshift-kubernetes-service-cli#worker_pool_taint_rm)
    * [`ibmcloud oc worker-pool taint set`](/docs/openshift?topic=openshift-kubernetes-service-cli#worker_pool_taint_set)
* [`ibmcloud oc worker-pool zones`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_pool_zones)

## ibmcloud oc zone
{: #icks_map_zone}

[List availability zones and modify the zones attached to a worker pool](/docs/openshift?topic=openshift-kubernetes-service-cli#zone).
{: shortdesc}

* **`zone add`**: Add a zone to one or more worker pools in a cluster.
    * [`ibmcloud oc zone add classic`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_zone_add)
    * [`ibmcloud oc zone add vpc-gen2`](/docs/openshift?topic=openshift-kubernetes-service-cli#cli_zone-add-vpc-gen2)
* [`ibmcloud oc zone ls`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_datacenters)
* [`ibmcloud oc zone network-set`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_zone_network_set)
* [`ibmcloud oc zone rm`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_zone_rm)

## ibmcloud oc ingress
{: #icks_map_ingress}

**Beta** [View and modify Ingress services and settings](/docs/openshift?topic=openshift-kubernetes-service-cli#alb-commands).
{: shortdesc}

* **`ingress alb`**: View and configure an Ingress application load balancer (ALB).
    * **`ingress alb autoupdate`**: Manage automatic updates for the Ingress ALB add-on in a cluster.
        * [`ibmcloud oc ingress alb autoupdate disable`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_alb_autoupdate_disable)
        * [`ibmcloud oc ingress alb autoupdate enable`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_alb_autoupdate_enable)
        * [`ibmcloud oc ingress alb autoupdate get`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_alb_autoupdate_get)
    * **`ingress alb create`**: Create an Ingress ALB in a cluster.
        * [`ibmcloud oc ingress alb create classic`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_alb_create)
        * [`ibmcloud oc ingress alb create vpc-gen2`](/docs/containers?topic=containers-kubernetes-service-cli#cli_alb-create-vpc-gen2)
    * [`ibmcloud oc ingress alb disable`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_alb_disable)
    * **`ingress alb enable`**: Enable an Ingress ALB in a cluster.
        * [`ibmcloud oc ingress alb enable classic`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_alb_configure)
        * [`ibmcloud oc ingress alb enable vpc-gen2`](/docs/containers?topic=containers-kubernetes-service-cli#cli_alb_configure_vpc_gen2)
    * [`ibmcloud oc ingress alb get`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_alb_get)
    * [`ibmcloud oc ingress alb ls`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_albs)
    * **`ingress alb migrate`**: Migrate your IBM Cloud Ingress configmap and resources to the Kubernetes Ingress format.
        * [`ibmcloud oc ingress alb migrate clean`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_alb_migrate_clean)
        * [`ibmcloud oc ingress alb migrate start`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_alb_migrate_start)
        * [`ibmcloud oc ingress alb migrate status`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_alb_migrate_status)
    * [`ibmcloud oc ingress alb update`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_alb_update)
    * [`ibmcloud oc ingress alb versions`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_alb_versions)
* **`ingress lb`**: Modify load balancers that expose Ingress ALBs in your cluster.
    * [`ibmcloud oc ingress lb get`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_ingress_lb_proxy-protocol_get)
    * **`ingress lb proxy-protocol`**: **VPC only** Modify the PROXY protocol configuration for ALB load balancers.
        * [`ibmcloud oc ingress lb proxy-protocol disable`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_ingress_lb_proxy-protocol_disable)
        * [`ibmcloud oc ingress lb proxy-protocol enable`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_ingress_lb_proxy-protocol_enable)
* **`ingress secret`**: Manage Ingress secrets in a cluster.
    * [`ibmcloud oc ingress secret create`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_ingress_secret_create)
    * [`ibmcloud oc ingress secret get`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_ingress_secret_get)
    * [`ibmcloud oc ingress secret ls`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_ingress_secret_ls)
    * [`ibmcloud oc ingress secret rm`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_ingress_secret_rm)
    * [`ibmcloud oc ingress secret update`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_ingress_secret_update)
* [`ibmcloud oc ingress status`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_ingress_status)

## ibmcloud oc logging
{: #icks_map_logging}

[Forward logs from your cluster.](/docs/containers?topic=containers-kubernetes-service-cli#logging_commands).
{: shortdesc}

* **`logging autoupdate`**: Manage automatic updates of the Fluentd add-on in a cluster.
    * [`ibmcloud oc logging autoupdate disable`](/docs/containers?topic=containers-kubernetes-service-cli#cs_log_autoupdate_disable)
    * [`ibmcloud oc logging autoupdate enable`](/docs/containers?topic=containers-kubernetes-service-cli#cs_log_autoupdate_enable)
    * [`ibmcloud oc logging autoupdate get`](/docs/containers?topic=containers-kubernetes-service-cli#cs_log_autoupdate_get)
* [`ibmcloud oc logging collect`](/docs/containers?topic=containers-kubernetes-service-cli#cs_log_collect)
* [`ibmcloud oc logging collect-status`](/docs/containers?topic=containers-kubernetes-service-cli#cs_log_collect_status)
* **`logging config`**: View or modify log forwarding configurations for a cluster.
    * [`ibmcloud oc logging config create`](/docs/containers?topic=containers-kubernetes-service-cli#cs_logging_create)
    * [`ibmcloud oc logging config get`](/docs/containers?topic=containers-kubernetes-service-cli#cs_logging_get)
    * [`ibmcloud oc logging config rm`](/docs/containers?topic=containers-kubernetes-service-cli#cs_logging_rm)
    * [`ibmcloud oc logging config update`](/docs/containers?topic=containers-kubernetes-service-cli#cs_logging_update)
* **`logging filter`**: View or modify log filters for a cluster.
    * [`ibmcloud oc logging filter create`](/docs/containers?topic=containers-kubernetes-service-cli#cs_log_filter_create)
    * [`ibmcloud oc logging filter get`](/docs/containers?topic=containers-kubernetes-service-cli#cs_log_filter_view)
    * [`ibmcloud oc logging filter rm`](/docs/containers?topic=containers-kubernetes-service-cli#cs_log_filter_delete)
    * [`ibmcloud oc logging filter update`](/docs/containers?topic=containers-kubernetes-service-cli#cs_log_filter_update)
* [`ibmcloud oc logging refresh`](/docs/containers?topic=containers-kubernetes-service-cli#cs_logging_refresh)

## ibmcloud oc nlb-dns
{: icks_map_nlb-dns}

[Create and manage host names for network load balancer (NLB) IP addresses in a cluster and health check monitors for host names](/docs/openshift?topic=openshift-kubernetes-service-cli#nlb-dns).
{: shortdesc}

* [`ibmcloud oc nlb-dns add`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_nlb-dns-add)
* **`nlb-dns create`**: Create a DNS host name.
    * [`ibmcloud oc nlb-dns create classic`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_nlb-dns-create)
    * [`ibmcloud oc nlb-dns create vpc-gen2`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_nlb-dns-create-vpc-gen2)
* [`ibmcloud oc nlb-dns ls`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_nlb-dns-ls)
* **`nlb-dns monitor`**: Create and manage health check monitors for network load balancer (NLB) IP addresses and host names in a cluster.
    * [`ibmcloud oc nlb-dns monitor configure`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_nlb-dns-monitor-configure)
    * [`ibmcloud oc nlb-dns monitor disable`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_nlb-dns-monitor-disable)
    * [`ibmcloud oc nlb-dns monitor enable`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_nlb-dns-monitor-enable)
    * [`ibmcloud oc nlb-dns monitor get`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_nlb-dns-monitor-get)
    * [`ibmcloud oc nlb-dns monitor ls`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_nlb-dns-monitor-ls)
* [`ibmcloud oc nlb-dns replace`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_nlb-dns-replace)
* **`nlb-dns rm`**: Create and manage health check monitors for network load balancer (NLB) IP addresses and host names in a cluster.
    * [`ibmcloud oc nlb-dns rm classic`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_nlb-dns-rm)
    * [`ibmcloud oc nlb-dns rm vpc-gen2`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_nlb-dns-rm-vpc-gen2)
* **Beta** **`nlb-dns secret`**:  Manage the secret for an NLB subdomain.
    * [`ibmcloud oc nlb-dns secret regenerate`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_nlb-dns-secret-regenerate)
    * [`ibmcloud oc nlb-dns secret rm`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_nlb-dns-secret-rm)

## ibmcloud oc webhook-create
{: #icks_map_webhook-create}

[Register a webhook in a cluster](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_webhook_create).
{: shortdesc}

## ibmcloud oc api-key 
{: #icks_map_api-key}

[View information about the API key for a cluster or reset it to a new key](/docs/openshift?topic=openshift-kubernetes-service-cli#api_key-commands).
{: shortdesc}

* [`ibmcloud oc api-key info`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_api_key_info)
* [`ibmcloud oc api-key reset`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_api_key_reset)

## ibmcloud oc credential
{: #icks_map_credential}

[Set and unset credentials that allow you to access the IBM Cloud classic infrastructure portfolio through your IBM Cloud account](/docs/openshift?topic=openshift-kubernetes-service-cli#credential).
{: shortdesc}

* [`ibmcloud oc credential get`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_credential_get)
* [`ibmcloud oc credential set classic`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_credentials_set)
* [`ibmcloud oc credential unset`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_credentials_unset)

## ibmcloud oc infra-permissions
{: #icks_map_infra-permissions}

[View information about infrastructure permissions that allow you to access the IBM Cloud classic infrastructure portfolio through your IBM Cloud account](/docs/openshift?topic=openshift-kubernetes-service-cli#infra-commands).
{: shortdesc}

* [`ibmcloud oc infra-permissions get`](/docs/openshift?topic=openshift-kubernetes-service-cli#infra_permissions_get)

## ibmcloud oc kms 
{: #icks_map_kms}

[View and configure Key Management Service integrations](/docs/openshift?topic=openshift-kubernetes-service-cli#ks_kms).
{: shortdesc}

* **`kms crk`**: List and configure the root keys for a Key Management Service instance.
    * [`ibmcloud oc kms crk ls`](/docs/openshift?topic=openshift-kubernetes-service-cli#ks_kms_crk_ls)
* [`ibmcloud oc kms enable`](/docs/openshift?topic=openshift-kubernetes-service-cli#ks_kms_enable)
* **`kms instance`**: View and configure available Key Management Service instances.
    * [`ibmcloud oc kms instance ls`](/docs/openshift?topic=openshift-kubernetes-service-cli#ks_kms_instance_ls)

## ibmcloud oc quota 
{: #icks_map_quota}

[View the quota and limits for cluster-related resources in your IBM Cloud account](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_quota).

* [`ibmcloud oc quota ls`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_quota_ls)

## ibmcloud oc subnets 
{: #icks_map_subnets}

[List available portable subnets in your IBM Cloud infrastructure account](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_subnets).
{: shortdesc}

## ibmcloud oc vlan 
{: #icks_map_vlan}

[List public and private VLANs for a zone and view the VLAN spanning status](/docs/openshift?topic=openshift-kubernetes-service-cli#vlan).
{: shortdesc}

* [`ibmcloud oc vlan ls`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_vlans)
* **`vlan spanning`**: View the VLAN spanning status for your IBM Cloud classic infrastructure account.
    * [`ibmcloud oc vlan spanning get`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_vlan_spanning_get)
    
## ibmcloud oc vpcs 
{: #icks_map_vpcs}

[List all VPCs in the targeted resource group. If no resource group is targeted, then all VPCs in the account are listed.](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_vpcs).
{: shortdesc}

## ibmcloud oc flavors
{: #icks_map_flavors}

[List available flavors for a zone](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_machine_types).
{: shortdesc}

## ibmcloud oc locations
{: #icks_map_locations}

[List supported IBM Cloud Kubernetes Service locations](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_supported-locations).
{: shortdesc}

## ibmcloud oc messages
{: #icks_map_messages}

[View the current user messages](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_messages).
{: shortdesc}

## ibmcloud oc versions
{: #icks_map_versions}

[List all the container platform versions that are available for IBM Cloud Kubernetes Service clusters](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_versions_command).
{: shortdesc}

## ibmcloud oc api
{: #icks_map_api}

**Deprecated** [View or set the API endpoint and API version for the service](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_cli_api).
{: shortdesc}

## ibmcloud oc init
{: #icks_map_init}

[Initialize the Kubernetes Service plug-in and get authentication tokens](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_init).
{: shortdesc}

## ibmcloud oc script  
{: #icks_map_script}

[Rewrite scripts that call IBM Cloud Kubernetes Service plug-in commands](/docs/openshift?topic=openshift-kubernetes-service-cli#script).
{: shortdesc}

* [`ibmcloud oc script update`](/docs/openshift?topic=openshift-kubernetes-service-cli#script_update)

## ibmcloud oc storage 
{: #icks_map_storage}

**Beta** [View and modify storage resources](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_storage).
{: shortdesc}

* **`storage attachment`**: View and modify storage volume attachments of worker nodes in your cluster.
    * [`ibmcloud oc storage attachment create`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_storage_att_cr)
    * [`ibmcloud oc storage attachment get`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_storage_att_get)
    * [`ibmcloud oc storage attachment ls`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_storage_att_ls)
    * [`ibmcloud oc storage attachment rm`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_storage_att_rm)
* **`storage volume`**: View a list of storage volumes.
    * [`ibmcloud oc storage volume get`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_storage_att_ls_c)
    * [`ibmcloud oc storage volume ls`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_storage_att_ls_2)
    
    
