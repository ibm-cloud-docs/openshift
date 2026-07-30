---

copyright: 
  years: 2022, 2026
lastupdated: "2026-07-30"


keywords: kubernetes, openshift

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}




# {{site.data.keyword.openshiftlong_notm}} CLI Map
{: #icks_map}

This page lists all `ibmcloud oc` commands as they are structured in the CLI. For more details on a specific command, click the command or see the [{{site.data.keyword.openshiftlong_notm}} CLI reference](/docs/openshift?topic=openshift-kubernetes-service-cli).



## ibmcloud oc cluster
{: #icks_map_cluster}

[View and modify cluster and cluster service settings](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster).
{: shortdesc}

* **`cluster addon`**: View, enable, update, and disable cluster add-ons.
    * [`ibmcloud oc cluster addon disable`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-addon-disable-cli)
    * [`ibmcloud oc cluster addon enable`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-addon-enable-cli)
    * [`ibmcloud oc cluster addon get`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-addon-get-cli)
    * [`ibmcloud oc cluster addon ls`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-addon-ls-cli)
    * [`ibmcloud oc cluster addon options`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-addon-options-cli)
    * [`ibmcloud oc cluster addon update`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-addon-update-cli)
    * [`ibmcloud oc cluster addon versions`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-addon-versions-cli)
* **`cluster ca`**: Manage the Certificate Authority (CA) certificates of a cluster.
    * [`ibmcloud oc cluster ca create`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-ca-create-cli)
    * [`ibmcloud oc cluster ca get`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-ca-get-cli)
    * [`ibmcloud oc cluster ca rotate`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-ca-rotate-cli)
    * [`ibmcloud oc cluster ca status`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-ca-status-cli)
* [`ibmcloud oc cluster config`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-config-cli)
* **`cluster create`**: Create a classic or VPC cluster.
    * [`ibmcloud oc cluster create classic`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-create-classic-cli)
    * [`ibmcloud oc cluster create vpc-gen2`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-create-vpc-gen2-cli)
* [`ibmcloud oc cluster get`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-get-cli)
* **`cluster image-security`**: Manage image security enforcement in your cluster.
    * [`ibmcloud oc cluster image-security disable`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-image-security-disable-cli)
    * [`ibmcloud oc cluster image-security enable`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-image-security-enable-cli)
* [`ibmcloud oc cluster ls`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-ls-cli)
* **`cluster master`**: View and modify the master for a cluster.
    * **`cluster master pod-security`**: View and modify your Pod Security configurations.
        * [`ibmcloud oc cluster master pod-security get`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-master-pod-security-get)
        * [`ibmcloud oc cluster master pod-security set`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-master-pod-security-set)
        * [`ibmcloud oc cluster master pod-security unset`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-master-pod-security-unset)
        * **`ibmcloud oc cluster master pod-security policy`**: View and modify the deprecated Pod Security policy configuration in supported clusters.
            * [`ibmcloud oc cluster master pod-security policy disable`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-master-pod-security-policy-disable)
            * [`ibmcloud oc cluster master pod-security policy enable`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-master-pod-security-policy-enable)
            * [`ibmcloud oc cluster master pod-security policy get`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-master-pod-security-policy-get)
    * **`cluster master private-service-endpoint`**: Manage the private service endpoint of a cluster.
        * **`ibmcloud oc cluster master private-service-endpoint allowlist`**: Manage the private service endpoint allowlist.
            * [`ibmcloud oc cluster master private-service-endpoint allowlist add`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-master-private-service-endpoint-allowlist-add-cli)
            * [`ibmcloud oc cluster master private-service-endpoint allowlist disable`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-master-private-service-endpoint-allowlist-disable-cli)
            * [`ibmcloud oc cluster master private-service-endpoint allowlist enable`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-master-private-service-endpoint-allowlist-enable-cli)
            * [`ibmcloud oc cluster master private-service-endpoint allowlist get`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-master-private-service-endpoint-allowlist-get-cli)
            * [`ibmcloud oc cluster master private-service-endpoint allowlist remove`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-master-private-service-endpoint-allowlist-rm-cli)
        * **`ibmcloud oc cluster master satellite-service-endpoint allowlist`**: Manage the {{site.data.keyword.satelliteshort}} service endpoint allowlist for a {{site.data.keyword.satelliteshort}} cluster with CoreOS-enabled.
            * [`ibmcloud oc cluster master satellite-service-endpoint allowlist add`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-master-sat-allowlist-add)
            * [`ibmcloud oc cluster master satellite-service-endpoint allowlist disable`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-master-sat-allowlist-disable)
            * [`ibmcloud oc cluster master satellite-service-endpoint allowlist enable`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-master-sat-allowlist-enable)
            * [`ibmcloud oc cluster master satellite-service-endpoint allowlist get`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-master-sat-allowlist-get)
            * [`ibmcloud oc cluster master satellite-service-endpoint allowlist remove`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-master-sat-allowlist-remove)
        * [`ibmcloud oc cluster master private-service-endpoint enable`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-master-private-service-endpoint-enable-cli)
    * **`cluster master public-service-endpoint`**: Manage the public service endpoint of a cluster.
        * [`ibmcloud oc cluster master public-service-endpoint enable`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-master-public-service-endpoint-enable-cli)
    * [`ibmcloud oc cluster master refresh`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-master-refresh-cli)
    * [`ibmcloud oc cluster master update`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-master-update-cli)
* **`cluster pull-secret`**: Manage image pull secrets for the cluster to access images in IBM Cloud Container Registry.
    * [`ibmcloud oc cluster pull-secret apply`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-pull-secret-apply-cli) 
* [`ibmcloud oc cluster rm`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-rm-cli)
* **`cluster service`**: View, bind, and unbind IBM Cloud services on a cluster.
    * [`ibmcloud oc cluster service bind`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-service-bind-cli)
    * [`ibmcloud oc cluster service ls`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-service-ls-cli)
    * [`ibmcloud oc cluster service unbind`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-service-unbind-cli)
* **`cluster subnet`**: Add and create portable subnets for a classic cluster.
    * [`ibmcloud oc cluster subnet add`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-subnet-add-cli)
    * [`ibmcloud oc cluster subnet create`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-subnet-create-cli)
    * [`ibmcloud oc cluster subnet detach`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-subnet-detach-cli)

## ibmcloud oc worker
{: #icks_map_worker}

[View and modify worker nodes for a cluster](/docs/openshift?topic=openshift-kubernetes-service-cli#worker_node_commands).
{: shortdesc}

* **Deprecated** [`ibmcloud oc worker add`](/docs/openshift?topic=openshift-kubernetes-service-cli#worker-pool-create-classic-cli) 
* [`ibmcloud oc worker get`](/docs/openshift?topic=openshift-kubernetes-service-cli#worker-get-cli)
* [`ibmcloud oc worker ls`](/docs/openshift?topic=openshift-kubernetes-service-cli#worker-ls-cli)
* [`ibmcloud oc worker reboot`](/docs/openshift?topic=openshift-kubernetes-service-cli#worker-reboot-cli)
* [`ibmcloud oc worker reload`](/docs/openshift?topic=openshift-kubernetes-service-cli#worker-reload-cli)
* [`ibmcloud oc worker replace`](/docs/openshift?topic=openshift-kubernetes-service-cli#worker-replace-cli)
* [`ibmcloud oc worker rm`](/docs/openshift?topic=openshift-kubernetes-service-cli#worker-rm-cli)
* [`ibmcloud oc worker update`](/docs/openshift?topic=openshift-kubernetes-service-cli#worker-update-cli)

## ibmcloud oc worker-pool
{: #icks_map_worker-pool}

[View and modify worker pools for a cluster](/docs/openshift?topic=openshift-kubernetes-service-cli#worker-pool).
{: shortdesc}

* **`worker-pool create`**: Add a worker pool to a cluster. No worker nodes are created until zones are added to the worker pool.
    * [`ibmcloud oc worker-pool create classic`](/docs/openshift?topic=openshift-kubernetes-service-cli#worker-pool-create-classic-cli)
    * [`ibmcloud oc worker-pool create vpc-gen2`](/docs/openshift?topic=openshift-kubernetes-service-cli#worker-pool-create-vpc-gen2-cli)
* [`ibmcloud oc worker-pool get`](/docs/openshift?topic=openshift-kubernetes-service-cli#worker-pool-get-cli)
* **`worker-pool label`**: Set and remove custom Kubernetes labels for all worker nodes in a worker pool.
    * [`ibmcloud oc worker-pool label rm`](/docs/openshift?topic=openshift-kubernetes-service-cli#worker-pool-label-rm-cli)
    * [`ibmcloud oc worker-pool label set`](/docs/openshift?topic=openshift-kubernetes-service-cli#worker-pool-label-set-cli)
* [`ibmcloud oc worker-pool ls`](/docs/openshift?topic=openshift-kubernetes-service-cli#worker-pool-ls-cli)
* [`ibmcloud oc worker-pool rebalance`](/docs/openshift?topic=openshift-kubernetes-service-cli#worker-pool-rebalance-cli)
* [`ibmcloud oc worker-pool resize`](/docs/openshift?topic=openshift-kubernetes-service-cli#worker-pool-resize-cli)
* [`ibmcloud oc worker-pool rm`](/docs/openshift?topic=openshift-kubernetes-service-cli#worker-pool-rm-cli)
* **[`worker-pool taint`]**: Set and remove Kubernetes taints for all worker nodes in a worker pool.
    * [`ibmcloud oc worker-pool taint rm`](/docs/openshift?topic=openshift-kubernetes-service-cli#worker_pool_taint_rm)
    * [`ibmcloud oc worker-pool taint set`](/docs/openshift?topic=openshift-kubernetes-service-cli#worker_pool_taint_set)
* [`ibmcloud oc worker-pool zones`](/docs/openshift?topic=openshift-kubernetes-service-cli#worker-pool-zones-cli)

## ibmcloud oc zone
{: #icks_map_zone}

[List availability zones and modify the zones attached to a worker pool](/docs/openshift?topic=openshift-kubernetes-service-cli#zone).
{: shortdesc}

* **`zone add`**: Add a zone to one or more worker pools in a cluster.
    * [`ibmcloud oc zone add classic`](/docs/openshift?topic=openshift-kubernetes-service-cli#zone-add-classic-cli)
    * [`ibmcloud oc zone add vpc-gen2`](/docs/openshift?topic=openshift-kubernetes-service-cli#zone-add-vpc-gen2-cli)
* [`ibmcloud oc zone ls`](/docs/openshift?topic=openshift-kubernetes-service-cli#locations-cli)
* [`ibmcloud oc zone network-set`](/docs/openshift?topic=openshift-kubernetes-service-cli#zone-network-set-cli)
* [`ibmcloud oc zone rm`](/docs/openshift?topic=openshift-kubernetes-service-cli#zone-rm-cli)

## ibmcloud oc ingress
{: #icks_map_ingress}

[View and modify Ingress services and settings](/docs/openshift?topic=openshift-kubernetes-service-cli#alb-commands).
{: shortdesc}

* **`ingress alb`**: View and configure an Ingress application load balancer (ALB).
    * **`ingress alb autoscale`**: Configure autoscaling for Ingress ALBs. 
        * [`ibmcloud oc ingress alb autouscale get`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-alb-autoscale-get-cli)
        * [`ibmcloud oc ingress alb autouscale set`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-alb-autoscale-set-cli)
        * [`ibmcloud oc ingress alb autouscale unset`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-alb-autoscale-unset-cli)
    * **`ingress alb autoupdate`**: Manage automatic updates for the Ingress ALB add-on in a cluster.
        * [`ibmcloud oc ingress alb autoupdate disable`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-alb-autoupdate-disable-cli)
        * [`ibmcloud oc ingress alb autoupdate enable`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-alb-autoupdate-enable-cli)
        * [`ibmcloud oc ingress alb autoupdate get`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-alb-autoupdate-get-cli)
    * **`ingress alb create`**: Create an Ingress ALB in a cluster.
        * [`ibmcloud oc ingress alb create classic`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-alb-create-classic-cli)
    * [`ibmcloud oc ingress alb disable`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-alb-disable-cli)
    * **`ingress alb enable`**: Enable an Ingress ALB in a cluster.
        * [`ibmcloud oc ingress alb enable classic`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-alb-update-cli)
    * [`ibmcloud oc ingress alb get`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-alb-get-cli)
    * **`ingress alb health-checker`**: Manage the Ingress ALB health checker.
        * [`ibmcloud oc ingress alb health-checker disable`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-alb-health-checker-disable-cli)
        * [`ibmcloud oc ingress alb health-checker enable`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-alb-health-checker-enable-cli)
        * [`ibmcloud oc ingress alb health-checker get`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-alb-health-checker-get-cli)
    * [`ibmcloud oc ingress alb ls`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-alb-ls-cli)
    * [`ibmcloud oc ingress alb update`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-alb-update-cli)
    * [`ibmcloud oc ingress alb versions`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-alb-versions-cli)
* **`ingress lb`**: Modify load balancers that expose Ingress ALBs in your cluster.
    * [`ibmcloud oc ingress lb get`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-load-balancer-proxy-protocol-get-cli)
    * **`ingress lb proxy-protocol`**: **VPC only** Modify the PROXY protocol configuration for ALB load balancers.
        * [`ibmcloud oc ingress lb proxy-protocol disable`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-load-balancer-proxy-protocol-disable-cli)
        * [`ibmcloud oc ingress lb proxy-protocol enable`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-load-balancer-proxy-protocol-enable-cli)
* **`ingress secret`**: Manage Ingress secrets in a cluster.
    * [`ibmcloud oc ingress secret create`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-secret-create-cli)
    * [`ibmcloud oc ingress secret get`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-secret-get-cli)
    * [`ibmcloud oc ingress secret ls`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-secret-ls-cli)
    * [`ibmcloud oc ingress secret rm`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-secret-rm-cli)
    * [`ibmcloud oc ingress secret update`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-secret-update-cli) 
* **`ingress status-report`**: View and manage ingress status reporting.
    * [`ibmcloud oc ingress status-report disable`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-status-report-disable-cli)
    * [`ibmcloud oc ingress status-report enable`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-status-report-enable-cli)
    * [`ibmcloud oc ingress status-report get`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-status-report-get-cli)
* **`ibmcloud oc ingress status-report ignore`**: Manage warnings to be ignored by ingress status reports.
    * [`ibmcloud oc ingress status-report ignore add`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-status-report-ignored-errors-add-cli)
    * [`ibmcloud oc ingress status-report ignore ls`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-status-report-ignored-errors-ls-cli)
    * [`ibmcloud oc ingress status-report ignore rm`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-status-report-ignored-errors-rm-cli)
    


## ibmcloud oc nlb-dns
{: #icks_map_nlb-dns}

[Create and manage host names for network load balancer (NLB) IP addresses in a cluster and health check monitors for host names](/docs/openshift?topic=openshift-kubernetes-service-cli#nlb-dns).
{: shortdesc}

* [`ibmcloud oc nlb-dns add`](/docs/openshift?topic=openshift-kubernetes-service-cli#nlb-dns-add-cli)
* **`nlb-dns create`**: Create a DNS host name.
    * [`ibmcloud oc nlb-dns create classic`](/docs/openshift?topic=openshift-kubernetes-service-cli#nlb-dns-create-classic-cli)
    * [`ibmcloud oc nlb-dns create vpc-gen2`](/docs/openshift?topic=openshift-kubernetes-service-cli#nlb-dns-create-vpc-gen2-cli)
* [`ibmcloud oc nlb-dns ls`](/docs/openshift?topic=openshift-kubernetes-service-cli#nlb-dns-ls-cli)
* [`ibmcloud oc nlb-dns get`](/docs/openshift?topic=openshift-kubernetes-service-cli#nlb-dns-get-cli)
* **`nlb-dns monitor`**: Create and manage health check monitors for network load balancer (NLB) IP addresses and host names in a cluster.
    * [`ibmcloud oc nlb-dns monitor configure`](/docs/openshift?topic=openshift-kubernetes-service-cli#nlb-dns-monitor-configure-cli)
    * [`ibmcloud oc nlb-dns monitor disable`](/docs/openshift?topic=openshift-kubernetes-service-cli#nlb-dns-monitor-disable-cli)
    * [`ibmcloud oc nlb-dns monitor enable`](/docs/openshift?topic=openshift-kubernetes-service-cli#nlb-dns-monitor-enable-cli)
    * [`ibmcloud oc nlb-dns monitor get`](/docs/openshift?topic=openshift-kubernetes-service-cli#nlb-dns-monitor-get-cli)
    * [`ibmcloud oc nlb-dns monitor ls`](/docs/openshift?topic=openshift-kubernetes-service-cli#nlb-dns-monitor-ls-cli)
* [`ibmcloud oc nlb-dns replace`](/docs/openshift?topic=openshift-kubernetes-service-cli#nlb-dns-replace-cli)
* **`nlb-dns rm`**: Create and manage health check monitors for network load balancer (NLB) IP addresses and host names in a cluster.
    * [`ibmcloud oc nlb-dns rm classic`](/docs/openshift?topic=openshift-kubernetes-service-cli#nlb-dns-rm-classic-cli)
    * [`ibmcloud oc nlb-dns rm vpc-gen2`](/docs/openshift?topic=openshift-kubernetes-service-cli#nlb-dns-rm-vpc-gen2-cli)
* **Beta** **`nlb-dns secret`**:  Manage the secret for an NLB subdomain.
    * [`ibmcloud oc nlb-dns secret regenerate`](/docs/openshift?topic=openshift-kubernetes-service-cli#nlb-dns-secret-regenerate-cli)
    * [`ibmcloud oc nlb-dns secret rm`](/docs/openshift?topic=openshift-kubernetes-service-cli#nlb-dns-secret-rm-cli)

## ibmcloud oc webhook-create
{: #icks_map_webhook-create}

[Register a webhook in a cluster](/docs/openshift?topic=openshift-kubernetes-service-cli#webhook-create-cli).
{: shortdesc}

## ibmcloud oc api-key 
{: #icks_map_api-key}

[View information about the API key for a cluster or reset it to a new key](/docs/openshift?topic=openshift-kubernetes-service-cli#api_key-commands).
{: shortdesc}

* [`ibmcloud oc api-key info`](/docs/openshift?topic=openshift-kubernetes-service-cli#api-key-info-cli)
* [`ibmcloud oc api-key reset`](/docs/openshift?topic=openshift-kubernetes-service-cli#api-key-reset-cli)

## ibmcloud oc credential
{: #icks_map_credential}

[Set and unset credentials that allow you to access the IBM Cloud classic infrastructure portfolio through your IBM Cloud account](/docs/openshift?topic=openshift-kubernetes-service-cli#credential).
{: shortdesc}

* [`ibmcloud oc credential get`](/docs/openshift?topic=openshift-kubernetes-service-cli#credential-get-cli)
* [`ibmcloud oc credential set classic`](/docs/openshift?topic=openshift-kubernetes-service-cli#credential-set-classic-cli)
* [`ibmcloud oc credential unset`](/docs/openshift?topic=openshift-kubernetes-service-cli#credential-unset-cli)

## ibmcloud oc infra-permissions
{: #icks_map_infra-permissions}

[View information about infrastructure permissions that allow you to access the IBM Cloud classic infrastructure portfolio through your IBM Cloud account](/docs/openshift?topic=openshift-kubernetes-service-cli#infra-commands).
{: shortdesc}

* [`ibmcloud oc infra-permissions get`](/docs/openshift?topic=openshift-kubernetes-service-cli#infra-permissions-get-cli)

## ibmcloud oc kms 
{: #icks_map_kms}

[View and configure Key Management Service integrations](/docs/openshift?topic=openshift-kubernetes-service-cli#kms-enable-cli).
{: shortdesc}

* **`kms crk`**: List and configure the root keys for a Key Management Service instance.
    * [`ibmcloud oc kms crk ls`](/docs/openshift?topic=openshift-kubernetes-service-cli#kms-crk-ls-cli)
* [`ibmcloud oc kms enable`](/docs/openshift?topic=openshift-kubernetes-service-cli#kms-enable-cli)
* **`kms instance`**: View and configure available Key Management Service instances.
    * [`ibmcloud oc kms instance ls`](/docs/openshift?topic=openshift-kubernetes-service-cli#kms-instance-ls-cli)

## ibmcloud oc quota 
{: #icks_map_quota}

[View the quota and limits for cluster-related resources in your IBM Cloud account](/docs/openshift?topic=openshift-kubernetes-service-cli#quota-ls-cli).

* [`ibmcloud oc quota ls`](/docs/openshift?topic=openshift-kubernetes-service-cli#quota-ls-cli)

## ibmcloud oc subnets 
{: #icks_map_subnets}

[List available portable subnets in your IBM Cloud infrastructure account](/docs/openshift?topic=openshift-kubernetes-service-cli#subnets-cli).
{: shortdesc}

## ibmcloud oc vlan 
{: #icks_map_vlan}

[List public and private VLANs for a zone and view the VLAN spanning status](/docs/openshift?topic=openshift-kubernetes-service-cli#vlan).
{: shortdesc}

* [`ibmcloud oc vlan ls`](/docs/openshift?topic=openshift-kubernetes-service-cli#vlan-ls-cli)
* **`vlan spanning`**: View the VLAN spanning status for your IBM Cloud classic infrastructure account.
    * [`ibmcloud oc vlan spanning get`](/docs/openshift?topic=openshift-kubernetes-service-cli#vlan-spanning-get-cli)
    
## ibmcloud oc vpcs 
{: #icks_map_vpcs}

[List all VPCs in the targeted resource group. If no resource group is targeted, then all VPCs in the account are listed.](/docs/openshift?topic=openshift-kubernetes-service-cli#vpc-ls-cli).
{: shortdesc}

## ibmcloud oc flavors
{: #icks_map_flavors}

[List available flavors for a zone](/docs/openshift?topic=openshift-kubernetes-service-cli#flavor-ls-cli).
{: shortdesc}

## ibmcloud oc locations
{: #icks_map_locations}

[List supported IBM Cloud Kubernetes Service locations](/docs/openshift?topic=openshift-kubernetes-service-cli#locations-cli).
{: shortdesc}

## ibmcloud oc messages
{: #icks_map_messages}

[View the current user messages](/docs/openshift?topic=openshift-kubernetes-service-cli#messages-cli).
{: shortdesc}

## ibmcloud oc versions
{: #icks_map_versions}

[List all the container platform versions that are available for IBM Cloud Kubernetes Service clusters](/docs/openshift?topic=openshift-kubernetes-service-cli#versions-cli).
{: shortdesc}

## ibmcloud oc api
{: #icks_map_api}

**Deprecated** [View or set the API endpoint and API version for the service](/docs/openshift?topic=openshift-kubernetes-service-cli#api-cli).
{: shortdesc}

## ibmcloud oc `init`
{: #icks_map_init}

[Initialize the Kubernetes Service plug-in and get authentication tokens](/docs/openshift?topic=openshift-kubernetes-service-cli#init-cli).
{: shortdesc}

## ibmcloud oc script  
{: #icks_map_script}

[Rewrite scripts that call IBM Cloud Kubernetes Service plug-in commands](/docs/openshift?topic=openshift-kubernetes-service-cli#script).
{: shortdesc}

* [`ibmcloud oc script update`](/docs/openshift?topic=openshift-kubernetes-service-cli#script_update)




## ibmcloud oc security-group
{: #icks_map_security_group}

[Reset or sync security group settings](/docs/openshift?topic=openshift-kubernetes-service-cli#security_group)

* [`ibmcloud oc security-group reset`](/docs/openshift?topic=openshift-kubernetes-service-cli#security_group_reset)
* [`ibmcloud oc security-group sync`](/docs/openshift?topic=openshift-kubernetes-service-cli#security_group_sync)



## ibmcloud oc storage 
{: #icks_map_storage}

**Beta** [View and modify storage resources](/docs/openshift?topic=openshift-kubernetes-service-cli#storage-attachment-create-cli).
{: shortdesc}

* **`storage attachment`**: View and modify storage volume attachments of worker nodes in your cluster.
    * [`ibmcloud oc storage attachment create`](/docs/openshift?topic=openshift-kubernetes-service-cli#storage-attachment-create-cli)
    * [`ibmcloud oc storage attachment get`](/docs/openshift?topic=openshift-kubernetes-service-cli#storage-attachment-get-cli)
    * [`ibmcloud oc storage attachment ls`](/docs/openshift?topic=openshift-kubernetes-service-cli#storage-attachment-ls-cli)
    * [`ibmcloud oc storage attachment rm`](/docs/openshift?topic=openshift-kubernetes-service-cli#storage-attachment-rm-cli)
* **`storage volume`**: View a list of storage volumes.
    * [`ibmcloud oc storage volume get`](/docs/openshift?topic=openshift-kubernetes-service-cli#storage-attachment-ls-cli)
    * [`ibmcloud oc storage volume ls`](/docs/openshift?topic=openshift-kubernetes-service-cli#storage-attachment-ls-cli)
    
    
