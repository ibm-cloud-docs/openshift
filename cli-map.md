---

copyright: 
  years: 2022, 2026
lastupdated: "2026-09-21"

keywords: kubernetes, openshift

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}

# {{site.data.keyword.openshiftlong_notm}} CLI Map
{: #icks_map}

This page lists all `ibmcloud oc` commands as they are structured in the CLI. For more details on a specific command, click the command or see the [{{site.data.keyword.openshiftlong_notm}} CLI reference](/docs/openshift?topic=openshift-kubernetes-service-cli).




## `api` commands
{: #icks_map_api}

View the current API endpoint.

* [`ibmcloud ks api`](/docs/containers?topic=containers-kubernetes-service-cli#api-cli)


## `api-key` commands
{: #icks_map_api-key}

View information about the API key for a cluster or reset it to a new key.

* [`ibmcloud ks api-key help`](/docs/containers?topic=containers-kubernetes-service-cli#api-key-help-cli)
* [`ibmcloud ks api-key info`](/docs/containers?topic=containers-kubernetes-service-cli#api-key-info-cli)
* [`ibmcloud ks api-key reset`](/docs/containers?topic=containers-kubernetes-service-cli#api-key-reset-cli)


## `cluster` commands
{: #icks_map_cluster}

View and modify cluster and cluster service settings.

* **`cluster addon`**: View, enable, update, and disable cluster add-ons.
* **`cluster ca`**: Manage the Certificate Authority (CA) certificates of a cluster.
* **`cluster create`**: Create a classic or VPC cluster.
* **`cluster image-security`**: Manage image security enforcement in your cluster.
* **`cluster master`**: View and modify the master for a cluster.
* **`cluster pull-secret`**: Manage image pull secrets for the cluster to access images in IBM Cloud Container Registry.
* **`cluster service`**: View, bind, and unbind IBM Cloud services on a cluster.
* **`cluster subnet`**: Add and create portable subnets for a classic cluster.
    * [`ibmcloud ks cluster addon disable acm`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-addon-disable-acm-cli)
    * [`ibmcloud ks cluster addon disable alb-oauth-proxy`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-addon-disable-alb-oauth-proxy-cli)
    * [`ibmcloud ks cluster addon disable cluster-autoscaler`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-addon-disable-cluster-autoscaler-cli)
    * [`ibmcloud ks cluster addon disable debug-tool`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-addon-disable-debug-tool-cli)
    * **Beta** [`ibmcloud ks cluster addon disable headlamp`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-addon-disable-headlamp-cli)
    * [`ibmcloud ks cluster addon disable help`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-addon-disable-help-cli)
    * [`ibmcloud ks cluster addon disable hpcs-router`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-addon-disable-hpcs-router-cli)
    * **Beta** [`ibmcloud ks cluster addon disable ibm-storage-operator`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-addon-disable-ibm-storage-operator-cli)
    * [`ibmcloud ks cluster addon disable image-key-synchronizer`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-addon-disable-image-key-synchronizer-cli)
    * [`ibmcloud ks cluster addon disable istio`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-addon-disable-istio-cli)
    * **Deprecated** [`ibmcloud ks cluster addon disable istio-extras`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-addon-disable-istio-extras-cli)
    * **Deprecated** [`ibmcloud ks cluster addon disable istio-sample-bookinfo`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-addon-disable-istio-sample-bookinfo-cli)
    * [`ibmcloud ks cluster addon disable knative`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-addon-disable-knative-cli)
    * [`ibmcloud ks cluster addon disable kube-terminal`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-addon-disable-kube-terminal-cli)
    * [`ibmcloud ks cluster addon disable openshift-data-foundation`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-addon-disable-openshift-data-foundation-cli)
    * [`ibmcloud ks cluster addon disable static-route`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-addon-disable-static-route-cli)
    * [`ibmcloud ks cluster addon disable vpc-block-csi-driver`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-addon-disable-vpc-block-csi-driver-cli)
    * [`ibmcloud ks cluster addon enable acm`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-addon-enable-acm-cli)
    * [`ibmcloud ks cluster addon enable alb-oauth-proxy`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-addon-enable-alb-oauth-proxy-cli)
    * [`ibmcloud ks cluster addon enable cluster-autoscaler`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-addon-enable-cluster-autoscaler-cli)
    * [`ibmcloud ks cluster addon enable debug-tool`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-addon-enable-debug-tool-cli)
    * **Beta** [`ibmcloud ks cluster addon enable headlamp`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-addon-enable-headlamp-cli)
    * [`ibmcloud ks cluster addon enable help`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-addon-enable-help-cli)
    * [`ibmcloud ks cluster addon enable hpcs-router`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-addon-enable-hpcs-router-cli)
    * **Beta** [`ibmcloud ks cluster addon enable ibm-storage-operator`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-addon-enable-ibm-storage-operator-cli)
    * [`ibmcloud ks cluster addon enable image-key-synchronizer`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-addon-enable-image-key-synchronizer-cli)
    * [`ibmcloud ks cluster addon enable istio`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-addon-enable-istio-cli)
    * **Deprecated** [`ibmcloud ks cluster addon enable istio-extras`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-addon-enable-istio-extras-cli)
    * **Deprecated** [`ibmcloud ks cluster addon enable istio-sample-bookinfo`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-addon-enable-istio-sample-bookinfo-cli)
    * [`ibmcloud ks cluster addon enable openshift-data-foundation`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-addon-enable-openshift-data-foundation-cli)
    * [`ibmcloud ks cluster addon enable static-route`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-addon-enable-static-route-cli)
    * [`ibmcloud ks cluster addon enable vpc-block-csi-driver`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-addon-enable-vpc-block-csi-driver-cli)
    * [`ibmcloud ks cluster addon get`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-addon-get-cli)
    * [`ibmcloud ks cluster addon help`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-addon-help-cli)
    * [`ibmcloud ks cluster addon ls`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-addon-ls-cli)
    * [`ibmcloud ks cluster addon options`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-addon-options-cli)
    * [`ibmcloud ks cluster addon update acm`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-addon-update-acm-cli)
    * [`ibmcloud ks cluster addon update alb-oauth-proxy`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-addon-update-alb-oauth-proxy-cli)
    * [`ibmcloud ks cluster addon update cluster-autoscaler`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-addon-update-cluster-autoscaler-cli)
    * [`ibmcloud ks cluster addon update debug-tool`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-addon-update-debug-tool-cli)
    * **Beta** [`ibmcloud ks cluster addon update headlamp`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-addon-update-headlamp-cli)
    * [`ibmcloud ks cluster addon update help`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-addon-update-help-cli)
    * [`ibmcloud ks cluster addon update hpcs-router`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-addon-update-hpcs-router-cli)
    * **Beta** [`ibmcloud ks cluster addon update ibm-storage-operator`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-addon-update-ibm-storage-operator-cli)
    * [`ibmcloud ks cluster addon update image-key-synchronizer`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-addon-update-image-key-synchronizer-cli)
    * [`ibmcloud ks cluster addon update istio`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-addon-update-istio-cli)
    * **Deprecated** [`ibmcloud ks cluster addon update istio-extras`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-addon-update-istio-extras-cli)
    * **Deprecated** [`ibmcloud ks cluster addon update istio-sample-bookinfo`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-addon-update-istio-sample-bookinfo-cli)
    * [`ibmcloud ks cluster addon update knative`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-addon-update-knative-cli)
    * [`ibmcloud ks cluster addon update kube-terminal`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-addon-update-kube-terminal-cli)
    * [`ibmcloud ks cluster addon update openshift-data-foundation`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-addon-update-openshift-data-foundation-cli)
    * [`ibmcloud ks cluster addon update static-route`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-addon-update-static-route-cli)
    * [`ibmcloud ks cluster addon update vpc-block-csi-driver`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-addon-update-vpc-block-csi-driver-cli)
    * [`ibmcloud ks cluster addon versions`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-addon-versions-cli)
    * [`ibmcloud ks cluster ca create`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-ca-create-cli)
    * [`ibmcloud ks cluster ca get`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-ca-get-cli)
    * [`ibmcloud ks cluster ca help`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-ca-help-cli)
    * [`ibmcloud ks cluster ca rotate`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-ca-rotate-cli)
    * [`ibmcloud ks cluster ca status`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-ca-status-cli)
    * [`ibmcloud ks cluster config`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-config-cli)
    * [`ibmcloud ks cluster create classic`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-create-classic-cli)
    * [`ibmcloud ks cluster create help`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-create-help-cli)
    * [`ibmcloud ks cluster create satellite`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-create-satellite-cli)
    * [`ibmcloud ks cluster create vpc-classic`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-create-vpc-classic-cli)
    * [`ibmcloud ks cluster create vpc-gen2`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-create-vpc-gen2-cli)
    * [`ibmcloud ks cluster get`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-get-cli)
    * [`ibmcloud ks cluster help`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-help-cli)
    * [`ibmcloud ks cluster image-security disable`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-image-security-disable-cli)
    * [`ibmcloud ks cluster image-security enable`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-image-security-enable-cli)
    * [`ibmcloud ks cluster image-security help`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-image-security-help-cli)
    * [`ibmcloud ks cluster ls`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-ls-cli)
    * [`ibmcloud ks cluster master audit-webhook get`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-master-audit-webhook-get-cli)
    * [`ibmcloud ks cluster master audit-webhook help`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-master-audit-webhook-help-cli)
    * [`ibmcloud ks cluster master audit-webhook set`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-master-audit-webhook-set-cli)
    * [`ibmcloud ks cluster master audit-webhook unset`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-master-audit-webhook-unset-cli)
    * [`ibmcloud ks cluster master console-oauth-access get`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-master-console-oauth-access-get-cli)
    * [`ibmcloud ks cluster master console-oauth-access help`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-master-console-oauth-access-help-cli)
    * [`ibmcloud ks cluster master console-oauth-access set`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-master-console-oauth-access-set-cli)
    * [`ibmcloud ks cluster master help`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-master-help-cli)
    * [`ibmcloud ks cluster master pod-security get`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-master-pod-security-get-cli)
    * [`ibmcloud ks cluster master pod-security help`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-master-pod-security-help-cli)
    * [`ibmcloud ks cluster master pod-security policy disable`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-master-pod-security-policy-disable-cli)
    * [`ibmcloud ks cluster master pod-security policy enable`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-master-pod-security-policy-enable-cli)
    * [`ibmcloud ks cluster master pod-security policy get`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-master-pod-security-policy-get-cli)
    * [`ibmcloud ks cluster master pod-security policy help`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-master-pod-security-policy-help-cli)
    * [`ibmcloud ks cluster master pod-security set`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-master-pod-security-set-cli)
    * [`ibmcloud ks cluster master pod-security unset`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-master-pod-security-unset-cli)
    * **Deprecated** [`ibmcloud ks cluster master private-service-endpoint allowlist add`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-master-private-service-endpoint-allowlist-add-cli)
    * **Deprecated** [`ibmcloud ks cluster master private-service-endpoint allowlist disable`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-master-private-service-endpoint-allowlist-disable-cli)
    * **Deprecated** [`ibmcloud ks cluster master private-service-endpoint allowlist enable`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-master-private-service-endpoint-allowlist-enable-cli)
    * **Deprecated** [`ibmcloud ks cluster master private-service-endpoint allowlist get`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-master-private-service-endpoint-allowlist-get-cli)
    * [`ibmcloud ks cluster master private-service-endpoint allowlist help`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-master-private-service-endpoint-allowlist-help-cli)
    * **Deprecated** [`ibmcloud ks cluster master private-service-endpoint allowlist rm`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-master-private-service-endpoint-allowlist-rm-cli)
    * [`ibmcloud ks cluster master private-service-endpoint enable`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-master-private-service-endpoint-enable-cli)
    * [`ibmcloud ks cluster master private-service-endpoint help`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-master-private-service-endpoint-help-cli)
    * [`ibmcloud ks cluster master public-service-endpoint disable`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-master-public-service-endpoint-disable-cli)
    * [`ibmcloud ks cluster master public-service-endpoint enable`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-master-public-service-endpoint-enable-cli)
    * [`ibmcloud ks cluster master public-service-endpoint help`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-master-public-service-endpoint-help-cli)
    * [`ibmcloud ks cluster master refresh`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-master-refresh-cli)
    * [`ibmcloud ks cluster master satellite-service-endpoint allowlist add`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-master-satellite-service-endpoint-allowlist-add-cli)
    * [`ibmcloud ks cluster master satellite-service-endpoint allowlist disable`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-master-satellite-service-endpoint-allowlist-disable-cli)
    * [`ibmcloud ks cluster master satellite-service-endpoint allowlist enable`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-master-satellite-service-endpoint-allowlist-enable-cli)
    * [`ibmcloud ks cluster master satellite-service-endpoint allowlist get`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-master-satellite-service-endpoint-allowlist-get-cli)
    * [`ibmcloud ks cluster master satellite-service-endpoint allowlist help`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-master-satellite-service-endpoint-allowlist-help-cli)
    * [`ibmcloud ks cluster master satellite-service-endpoint allowlist rm`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-master-satellite-service-endpoint-allowlist-rm-cli)
    * [`ibmcloud ks cluster master satellite-service-endpoint help`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-master-satellite-service-endpoint-help-cli)
    * [`ibmcloud ks cluster master update`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-master-update-cli)
    * [`ibmcloud ks cluster pull-secret apply`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-pull-secret-apply-cli)
    * [`ibmcloud ks cluster pull-secret help`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-pull-secret-help-cli)
    * [`ibmcloud ks cluster rm`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-rm-cli)
    * [`ibmcloud ks cluster service bind`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-service-bind-cli)
    * [`ibmcloud ks cluster service help`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-service-help-cli)
    * [`ibmcloud ks cluster service ls`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-service-ls-cli)
    * [`ibmcloud ks cluster service unbind`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-service-unbind-cli)
    * [`ibmcloud ks cluster subnet add`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-subnet-add-cli)
    * [`ibmcloud ks cluster subnet create`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-subnet-create-cli)
    * [`ibmcloud ks cluster subnet detach`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-subnet-detach-cli)
    * [`ibmcloud ks cluster subnet help`](/docs/containers?topic=containers-kubernetes-service-cli#cluster-subnet-help-cli)


## `credential` commands
{: #icks_map_credential}

Set and unset credentials that allow you to access the IBM Cloud classic infrastructure portfolio through your IBM Cloud account.

* **`credential set`**: Set credentials that allow you to access the IBM Cloud classic infrastructure portfolio through your IBM Cloud account. This command applies to the targeted resource group, or to the default resource group if no resource group is targeted.
    * [`ibmcloud ks credential get`](/docs/containers?topic=containers-kubernetes-service-cli#credential-get-cli)
    * [`ibmcloud ks credential help`](/docs/containers?topic=containers-kubernetes-service-cli#credential-help-cli)
    * [`ibmcloud ks credential set classic`](/docs/containers?topic=containers-kubernetes-service-cli#credential-set-classic-cli)
    * [`ibmcloud ks credential set help`](/docs/containers?topic=containers-kubernetes-service-cli#credential-set-help-cli)
    * [`ibmcloud ks credential unset`](/docs/containers?topic=containers-kubernetes-service-cli#credential-unset-cli)


## `experimental` commands
{: #icks_map_experimental}

[Expires on 2026-10-21] Experiment with new commands. IMPORTANT: Commands here will retire after the [date] in their description.

* **`experimental trusted-profile`**: [Expires on 2026-10-21] View and set the trusted profile on a cluster or the default trusted profile for clusters created in a resource-group.
* **`experimental vni`**: [Deactivated on 2026-05-20! Use `ibmcloud ks vni` instead] Attach, detach, and list Virtual Network Interfaces on worker nodes.
    * [`ibmcloud ks experimental help`](/docs/containers?topic=containers-kubernetes-service-cli#experimental-help-cli)
    * [`ibmcloud ks experimental trusted-profile default get`](/docs/containers?topic=containers-kubernetes-service-cli#experimental-trusted-profile-default-get-cli)
    * [`ibmcloud ks experimental trusted-profile default help`](/docs/containers?topic=containers-kubernetes-service-cli#experimental-trusted-profile-default-help-cli)
    * [`ibmcloud ks experimental trusted-profile default set`](/docs/containers?topic=containers-kubernetes-service-cli#experimental-trusted-profile-default-set-cli)
    * [`ibmcloud ks experimental trusted-profile get`](/docs/containers?topic=containers-kubernetes-service-cli#experimental-trusted-profile-get-cli)
    * [`ibmcloud ks experimental trusted-profile help`](/docs/containers?topic=containers-kubernetes-service-cli#experimental-trusted-profile-help-cli)
    * [`ibmcloud ks experimental trusted-profile set`](/docs/containers?topic=containers-kubernetes-service-cli#experimental-trusted-profile-set-cli)


## `flavor` commands
{: #icks_map_flavor}

Getting flavor related information. Flavors determine how much virtual CPU, memory, and disk space is available to each worker node.

* [`ibmcloud ks flavor get`](/docs/containers?topic=containers-kubernetes-service-cli#flavor-get-cli)
* [`ibmcloud ks flavor help`](/docs/containers?topic=containers-kubernetes-service-cli#flavor-help-cli)
* [`ibmcloud ks flavor ls`](/docs/containers?topic=containers-kubernetes-service-cli#flavor-ls-cli)


## `infra-permissions` commands
{: #icks_map_infra-permissions}

View information about infrastructure permissions that allow you to access the IBM Cloud classic infrastructure portfolio through your IBM Cloud account.

* [`ibmcloud ks infra-permissions get`](/docs/containers?topic=containers-kubernetes-service-cli#infra-permissions-get-cli)
* [`ibmcloud ks infra-permissions help`](/docs/containers?topic=containers-kubernetes-service-cli#infra-permissions-help-cli)


## `ingress` commands
{: #icks_map_ingress}

View and modify Ingress services and settings

* **`ingress alb`**: View and configure an Ingress application load balancer (ALB).
* **`ingress domain`**: Manage a cluster's Ingress domains.
* **`ingress instance`**: Manage registered instances of the IBM Cloud Secrets Manager.
* **`ingress load-balancer`**: Modify load balancers that expose Ingress ALBs in your cluster.
* **`ingress secret`**: Manage Ingress secrets in a cluster.
* **`ingress security`**: Modify the ingress security configuration for your cluster.
* **`ingress status-report`**: View and configure Ingress status reports.
    * [`ibmcloud ks ingress alb autoscale get`](/docs/containers?topic=containers-kubernetes-service-cli#ingress-alb-autoscale-get-cli)
    * [`ibmcloud ks ingress alb autoscale help`](/docs/containers?topic=containers-kubernetes-service-cli#ingress-alb-autoscale-help-cli)
    * [`ibmcloud ks ingress alb autoscale set`](/docs/containers?topic=containers-kubernetes-service-cli#ingress-alb-autoscale-set-cli)
    * [`ibmcloud ks ingress alb autoscale unset`](/docs/containers?topic=containers-kubernetes-service-cli#ingress-alb-autoscale-unset-cli)
    * [`ibmcloud ks ingress alb autoupdate disable`](/docs/containers?topic=containers-kubernetes-service-cli#ingress-alb-autoupdate-disable-cli)
    * [`ibmcloud ks ingress alb autoupdate enable`](/docs/containers?topic=containers-kubernetes-service-cli#ingress-alb-autoupdate-enable-cli)
    * [`ibmcloud ks ingress alb autoupdate get`](/docs/containers?topic=containers-kubernetes-service-cli#ingress-alb-autoupdate-get-cli)
    * [`ibmcloud ks ingress alb autoupdate help`](/docs/containers?topic=containers-kubernetes-service-cli#ingress-alb-autoupdate-help-cli)
    * [`ibmcloud ks ingress alb create classic`](/docs/containers?topic=containers-kubernetes-service-cli#ingress-alb-create-classic-cli)
    * [`ibmcloud ks ingress alb create help`](/docs/containers?topic=containers-kubernetes-service-cli#ingress-alb-create-help-cli)
    * [`ibmcloud ks ingress alb create vpc-gen2`](/docs/containers?topic=containers-kubernetes-service-cli#ingress-alb-create-vpc-gen2-cli)
    * [`ibmcloud ks ingress alb disable`](/docs/containers?topic=containers-kubernetes-service-cli#ingress-alb-disable-cli)
    * [`ibmcloud ks ingress alb enable classic`](/docs/containers?topic=containers-kubernetes-service-cli#ingress-alb-enable-classic-cli)
    * [`ibmcloud ks ingress alb enable help`](/docs/containers?topic=containers-kubernetes-service-cli#ingress-alb-enable-help-cli)
    * [`ibmcloud ks ingress alb enable vpc-gen2`](/docs/containers?topic=containers-kubernetes-service-cli#ingress-alb-enable-vpc-gen2-cli)
    * [`ibmcloud ks ingress alb get`](/docs/containers?topic=containers-kubernetes-service-cli#ingress-alb-get-cli)
    * [`ibmcloud ks ingress alb health-checker disable`](/docs/containers?topic=containers-kubernetes-service-cli#ingress-alb-health-checker-disable-cli)
    * [`ibmcloud ks ingress alb health-checker enable`](/docs/containers?topic=containers-kubernetes-service-cli#ingress-alb-health-checker-enable-cli)
    * [`ibmcloud ks ingress alb health-checker get`](/docs/containers?topic=containers-kubernetes-service-cli#ingress-alb-health-checker-get-cli)
    * [`ibmcloud ks ingress alb health-checker help`](/docs/containers?topic=containers-kubernetes-service-cli#ingress-alb-health-checker-help-cli)
    * [`ibmcloud ks ingress alb help`](/docs/containers?topic=containers-kubernetes-service-cli#ingress-alb-help-cli)
    * [`ibmcloud ks ingress alb ls`](/docs/containers?topic=containers-kubernetes-service-cli#ingress-alb-ls-cli)
    * [`ibmcloud ks ingress alb update`](/docs/containers?topic=containers-kubernetes-service-cli#ingress-alb-update-cli)
    * [`ibmcloud ks ingress alb versions`](/docs/containers?topic=containers-kubernetes-service-cli#ingress-alb-versions-cli)
    * [`ibmcloud ks ingress domain create`](/docs/containers?topic=containers-kubernetes-service-cli#ingress-domain-create-cli)
    * [`ibmcloud ks ingress domain default help`](/docs/containers?topic=containers-kubernetes-service-cli#ingress-domain-default-help-cli)
    * [`ibmcloud ks ingress domain default replace`](/docs/containers?topic=containers-kubernetes-service-cli#ingress-domain-default-replace-cli)
    * [`ibmcloud ks ingress domain get`](/docs/containers?topic=containers-kubernetes-service-cli#ingress-domain-get-cli)
    * [`ibmcloud ks ingress domain help`](/docs/containers?topic=containers-kubernetes-service-cli#ingress-domain-help-cli)
    * [`ibmcloud ks ingress domain ls`](/docs/containers?topic=containers-kubernetes-service-cli#ingress-domain-ls-cli)
    * [`ibmcloud ks ingress domain rm`](/docs/containers?topic=containers-kubernetes-service-cli#ingress-domain-rm-cli)
    * [`ibmcloud ks ingress domain secret help`](/docs/containers?topic=containers-kubernetes-service-cli#ingress-domain-secret-help-cli)
    * [`ibmcloud ks ingress domain secret regenerate`](/docs/containers?topic=containers-kubernetes-service-cli#ingress-domain-secret-regenerate-cli)
    * [`ibmcloud ks ingress domain secret rm`](/docs/containers?topic=containers-kubernetes-service-cli#ingress-domain-secret-rm-cli)
    * [`ibmcloud ks ingress domain update`](/docs/containers?topic=containers-kubernetes-service-cli#ingress-domain-update-cli)
    * [`ibmcloud ks ingress help`](/docs/containers?topic=containers-kubernetes-service-cli#ingress-help-cli)
    * [`ibmcloud ks ingress instance default help`](/docs/containers?topic=containers-kubernetes-service-cli#ingress-instance-default-help-cli)
    * [`ibmcloud ks ingress instance default set`](/docs/containers?topic=containers-kubernetes-service-cli#ingress-instance-default-set-cli)
    * [`ibmcloud ks ingress instance default unset`](/docs/containers?topic=containers-kubernetes-service-cli#ingress-instance-default-unset-cli)
    * [`ibmcloud ks ingress instance get`](/docs/containers?topic=containers-kubernetes-service-cli#ingress-instance-get-cli)
    * [`ibmcloud ks ingress instance help`](/docs/containers?topic=containers-kubernetes-service-cli#ingress-instance-help-cli)
    * [`ibmcloud ks ingress instance ls`](/docs/containers?topic=containers-kubernetes-service-cli#ingress-instance-ls-cli)
    * [`ibmcloud ks ingress instance register`](/docs/containers?topic=containers-kubernetes-service-cli#ingress-instance-register-cli)
    * [`ibmcloud ks ingress instance unregister`](/docs/containers?topic=containers-kubernetes-service-cli#ingress-instance-unregister-cli)
    * [`ibmcloud ks ingress load-balancer backend help`](/docs/containers?topic=containers-kubernetes-service-cli#ingress-load-balancer-backend-help-cli)
    * [`ibmcloud ks ingress load-balancer backend set`](/docs/containers?topic=containers-kubernetes-service-cli#ingress-load-balancer-backend-set-cli)
    * [`ibmcloud ks ingress load-balancer get`](/docs/containers?topic=containers-kubernetes-service-cli#ingress-load-balancer-get-cli)
    * [`ibmcloud ks ingress load-balancer help`](/docs/containers?topic=containers-kubernetes-service-cli#ingress-load-balancer-help-cli)
    * [`ibmcloud ks ingress load-balancer proxy-protocol disable`](/docs/containers?topic=containers-kubernetes-service-cli#ingress-load-balancer-proxy-protocol-disable-cli)
    * [`ibmcloud ks ingress load-balancer proxy-protocol enable`](/docs/containers?topic=containers-kubernetes-service-cli#ingress-load-balancer-proxy-protocol-enable-cli)
    * [`ibmcloud ks ingress load-balancer proxy-protocol help`](/docs/containers?topic=containers-kubernetes-service-cli#ingress-load-balancer-proxy-protocol-help-cli)
    * [`ibmcloud ks ingress secret create`](/docs/containers?topic=containers-kubernetes-service-cli#ingress-secret-create-cli)
    * [`ibmcloud ks ingress secret field add`](/docs/containers?topic=containers-kubernetes-service-cli#ingress-secret-field-add-cli)
    * [`ibmcloud ks ingress secret field help`](/docs/containers?topic=containers-kubernetes-service-cli#ingress-secret-field-help-cli)
    * [`ibmcloud ks ingress secret field ls`](/docs/containers?topic=containers-kubernetes-service-cli#ingress-secret-field-ls-cli)
    * [`ibmcloud ks ingress secret field rm`](/docs/containers?topic=containers-kubernetes-service-cli#ingress-secret-field-rm-cli)
    * [`ibmcloud ks ingress secret get`](/docs/containers?topic=containers-kubernetes-service-cli#ingress-secret-get-cli)
    * [`ibmcloud ks ingress secret help`](/docs/containers?topic=containers-kubernetes-service-cli#ingress-secret-help-cli)
    * [`ibmcloud ks ingress secret ls`](/docs/containers?topic=containers-kubernetes-service-cli#ingress-secret-ls-cli)
    * [`ibmcloud ks ingress secret rm`](/docs/containers?topic=containers-kubernetes-service-cli#ingress-secret-rm-cli)
    * [`ibmcloud ks ingress secret update`](/docs/containers?topic=containers-kubernetes-service-cli#ingress-secret-update-cli)
    * [`ibmcloud ks ingress security help`](/docs/containers?topic=containers-kubernetes-service-cli#ingress-security-help-cli)
    * [`ibmcloud ks ingress security port80 disable`](/docs/containers?topic=containers-kubernetes-service-cli#ingress-security-port80-disable-cli)
    * [`ibmcloud ks ingress security port80 enable`](/docs/containers?topic=containers-kubernetes-service-cli#ingress-security-port80-enable-cli)
    * [`ibmcloud ks ingress security port80 get`](/docs/containers?topic=containers-kubernetes-service-cli#ingress-security-port80-get-cli)
    * [`ibmcloud ks ingress security port80 help`](/docs/containers?topic=containers-kubernetes-service-cli#ingress-security-port80-help-cli)
    * [`ibmcloud ks ingress status-report disable`](/docs/containers?topic=containers-kubernetes-service-cli#ingress-status-report-disable-cli)
    * [`ibmcloud ks ingress status-report enable`](/docs/containers?topic=containers-kubernetes-service-cli#ingress-status-report-enable-cli)
    * [`ibmcloud ks ingress status-report get`](/docs/containers?topic=containers-kubernetes-service-cli#ingress-status-report-get-cli)
    * [`ibmcloud ks ingress status-report help`](/docs/containers?topic=containers-kubernetes-service-cli#ingress-status-report-help-cli)
    * [`ibmcloud ks ingress status-report ignored-errors add`](/docs/containers?topic=containers-kubernetes-service-cli#ingress-status-report-ignored-errors-add-cli)
    * [`ibmcloud ks ingress status-report ignored-errors help`](/docs/containers?topic=containers-kubernetes-service-cli#ingress-status-report-ignored-errors-help-cli)
    * [`ibmcloud ks ingress status-report ignored-errors ls`](/docs/containers?topic=containers-kubernetes-service-cli#ingress-status-report-ignored-errors-ls-cli)
    * [`ibmcloud ks ingress status-report ignored-errors rm`](/docs/containers?topic=containers-kubernetes-service-cli#ingress-status-report-ignored-errors-rm-cli)


## `kms` commands
{: #icks_map_kms}

View and configure Key Management Service integrations.

* **`kms crk`**: List and configure the root keys for a Key Management Service instance.
* **`kms instance`**: View and configure available Key Management Service instances.
    * [`ibmcloud ks kms crk help`](/docs/containers?topic=containers-kubernetes-service-cli#kms-crk-help-cli)
    * [`ibmcloud ks kms crk ls`](/docs/containers?topic=containers-kubernetes-service-cli#kms-crk-ls-cli)
    * [`ibmcloud ks kms enable`](/docs/containers?topic=containers-kubernetes-service-cli#kms-enable-cli)
    * [`ibmcloud ks kms help`](/docs/containers?topic=containers-kubernetes-service-cli#kms-help-cli)
    * [`ibmcloud ks kms instance help`](/docs/containers?topic=containers-kubernetes-service-cli#kms-instance-help-cli)
    * [`ibmcloud ks kms instance ls`](/docs/containers?topic=containers-kubernetes-service-cli#kms-instance-ls-cli)


## `locations` commands
{: #icks_map_locations}

List supported IBM Cloud Kubernetes Service locations.

* [`ibmcloud ks locations`](/docs/containers?topic=containers-kubernetes-service-cli#locations-cli)


## `logging` commands
{: #icks_map_logging}

Forward logs from your cluster.

* **`logging autoupdate`**: Manage automatic updates of the Fluentd add-on in a cluster.
* **`logging config`**: View or modify log forwarding configurations for a cluster.
* **`logging filter`**: View or modify log filters for a cluster.
    * [`ibmcloud ks logging autoupdate disable`](/docs/containers?topic=containers-kubernetes-service-cli#logging-autoupdate-disable-cli)
    * [`ibmcloud ks logging autoupdate enable`](/docs/containers?topic=containers-kubernetes-service-cli#logging-autoupdate-enable-cli)
    * [`ibmcloud ks logging autoupdate get`](/docs/containers?topic=containers-kubernetes-service-cli#logging-autoupdate-get-cli)
    * [`ibmcloud ks logging autoupdate help`](/docs/containers?topic=containers-kubernetes-service-cli#logging-autoupdate-help-cli)
    * [`ibmcloud ks logging config create`](/docs/containers?topic=containers-kubernetes-service-cli#logging-config-create-cli)
    * [`ibmcloud ks logging config get`](/docs/containers?topic=containers-kubernetes-service-cli#logging-config-get-cli)
    * [`ibmcloud ks logging config help`](/docs/containers?topic=containers-kubernetes-service-cli#logging-config-help-cli)
    * [`ibmcloud ks logging config rm`](/docs/containers?topic=containers-kubernetes-service-cli#logging-config-rm-cli)
    * [`ibmcloud ks logging config update`](/docs/containers?topic=containers-kubernetes-service-cli#logging-config-update-cli)
    * [`ibmcloud ks logging filter create`](/docs/containers?topic=containers-kubernetes-service-cli#logging-filter-create-cli)
    * [`ibmcloud ks logging filter get`](/docs/containers?topic=containers-kubernetes-service-cli#logging-filter-get-cli)
    * [`ibmcloud ks logging filter help`](/docs/containers?topic=containers-kubernetes-service-cli#logging-filter-help-cli)
    * [`ibmcloud ks logging filter rm`](/docs/containers?topic=containers-kubernetes-service-cli#logging-filter-rm-cli)
    * [`ibmcloud ks logging filter update`](/docs/containers?topic=containers-kubernetes-service-cli#logging-filter-update-cli)
    * [`ibmcloud ks logging help`](/docs/containers?topic=containers-kubernetes-service-cli#logging-help-cli)
    * [`ibmcloud ks logging refresh`](/docs/containers?topic=containers-kubernetes-service-cli#logging-refresh-cli)


## `messages` commands
{: #icks_map_messages}

View the current user messages.

* [`ibmcloud ks messages`](/docs/containers?topic=containers-kubernetes-service-cli#messages-cli)


## `nlb-dns` commands
{: #icks_map_nlb-dns}

Create and manage host names for network load balancer (NLB) IP addresses in a cluster and health check monitors for host names.

* **`nlb-dns create`**: Create a DNS host name.
* **`nlb-dns monitor`**: Create and manage health check monitors for network load balancer (NLB) IP addresses and host names in a cluster
* **`nlb-dns rm`**: Remove an NLB IP or load balancer host name from an NLB host name.
* **`nlb-dns secret`**: Manage the secret for an NLB subdomain.
    * [`ibmcloud ks nlb-dns add`](/docs/containers?topic=containers-kubernetes-service-cli#nlb-dns-add-cli)
    * [`ibmcloud ks nlb-dns create classic`](/docs/containers?topic=containers-kubernetes-service-cli#nlb-dns-create-classic-cli)
    * [`ibmcloud ks nlb-dns create help`](/docs/containers?topic=containers-kubernetes-service-cli#nlb-dns-create-help-cli)
    * [`ibmcloud ks nlb-dns create vpc-gen2`](/docs/containers?topic=containers-kubernetes-service-cli#nlb-dns-create-vpc-gen2-cli)
    * [`ibmcloud ks nlb-dns get`](/docs/containers?topic=containers-kubernetes-service-cli#nlb-dns-get-cli)
    * [`ibmcloud ks nlb-dns help`](/docs/containers?topic=containers-kubernetes-service-cli#nlb-dns-help-cli)
    * [`ibmcloud ks nlb-dns ls`](/docs/containers?topic=containers-kubernetes-service-cli#nlb-dns-ls-cli)
    * [`ibmcloud ks nlb-dns monitor configure`](/docs/containers?topic=containers-kubernetes-service-cli#nlb-dns-monitor-configure-cli)
    * [`ibmcloud ks nlb-dns monitor disable`](/docs/containers?topic=containers-kubernetes-service-cli#nlb-dns-monitor-disable-cli)
    * [`ibmcloud ks nlb-dns monitor enable`](/docs/containers?topic=containers-kubernetes-service-cli#nlb-dns-monitor-enable-cli)
    * [`ibmcloud ks nlb-dns monitor get`](/docs/containers?topic=containers-kubernetes-service-cli#nlb-dns-monitor-get-cli)
    * [`ibmcloud ks nlb-dns monitor help`](/docs/containers?topic=containers-kubernetes-service-cli#nlb-dns-monitor-help-cli)
    * [`ibmcloud ks nlb-dns monitor ls`](/docs/containers?topic=containers-kubernetes-service-cli#nlb-dns-monitor-ls-cli)
    * [`ibmcloud ks nlb-dns replace`](/docs/containers?topic=containers-kubernetes-service-cli#nlb-dns-replace-cli)
    * [`ibmcloud ks nlb-dns rm classic`](/docs/containers?topic=containers-kubernetes-service-cli#nlb-dns-rm-classic-cli)
    * [`ibmcloud ks nlb-dns rm help`](/docs/containers?topic=containers-kubernetes-service-cli#nlb-dns-rm-help-cli)
    * [`ibmcloud ks nlb-dns rm vpc-gen2`](/docs/containers?topic=containers-kubernetes-service-cli#nlb-dns-rm-vpc-gen2-cli)
    * [`ibmcloud ks nlb-dns secret help`](/docs/containers?topic=containers-kubernetes-service-cli#nlb-dns-secret-help-cli)
    * [`ibmcloud ks nlb-dns secret regenerate`](/docs/containers?topic=containers-kubernetes-service-cli#nlb-dns-secret-regenerate-cli)
    * [`ibmcloud ks nlb-dns secret rm`](/docs/containers?topic=containers-kubernetes-service-cli#nlb-dns-secret-rm-cli)


## `quota` commands
{: #icks_map_quota}

View the quota and limits for cluster-related resources in your IBM Cloud account.

* [`ibmcloud ks quota help`](/docs/containers?topic=containers-kubernetes-service-cli#quota-help-cli)
* [`ibmcloud ks quota ls`](/docs/containers?topic=containers-kubernetes-service-cli#quota-ls-cli)


## `script` commands
{: #icks_map_script}

Rewrite scripts that call IBM Cloud Kubernetes Service plug-in commands. Legacy-structured commands are replaced with beta-structured commands.

* [`ibmcloud ks script help`](/docs/containers?topic=containers-kubernetes-service-cli#script-help-cli)
* [`ibmcloud ks script update`](/docs/containers?topic=containers-kubernetes-service-cli#script-update-cli)


## `security-group` commands
{: #icks_map_security-group}

Run operations against a security group.

* [`ibmcloud ks security-group help`](/docs/containers?topic=containers-kubernetes-service-cli#security-group-help-cli)
* [`ibmcloud ks security-group ls`](/docs/containers?topic=containers-kubernetes-service-cli#security-group-ls-cli)
* [`ibmcloud ks security-group reset`](/docs/containers?topic=containers-kubernetes-service-cli#security-group-reset-cli)
* [`ibmcloud ks security-group sync`](/docs/containers?topic=containers-kubernetes-service-cli#security-group-sync-cli)


## `storage` commands
{: #icks_map_storage}

View and modify storage resources.

* **`storage attachment`**: View and modify storage volume attachments of worker nodes in your cluster.
* **`storage volume`**: View a list of storage volumes.
    * **Beta** [`ibmcloud ks storage attachment create`](/docs/containers?topic=containers-kubernetes-service-cli#storage-attachment-create-cli)
    * **Beta** [`ibmcloud ks storage attachment get`](/docs/containers?topic=containers-kubernetes-service-cli#storage-attachment-get-cli)
    * [`ibmcloud ks storage attachment help`](/docs/containers?topic=containers-kubernetes-service-cli#storage-attachment-help-cli)
    * **Beta** [`ibmcloud ks storage attachment ls`](/docs/containers?topic=containers-kubernetes-service-cli#storage-attachment-ls-cli)
    * **Beta** [`ibmcloud ks storage attachment rm`](/docs/containers?topic=containers-kubernetes-service-cli#storage-attachment-rm-cli)
    * [`ibmcloud ks storage help`](/docs/containers?topic=containers-kubernetes-service-cli#storage-help-cli)
    * **Beta** [`ibmcloud ks storage volume get`](/docs/containers?topic=containers-kubernetes-service-cli#storage-volume-get-cli)
    * [`ibmcloud ks storage volume help`](/docs/containers?topic=containers-kubernetes-service-cli#storage-volume-help-cli)
    * **Beta** [`ibmcloud ks storage volume ls`](/docs/containers?topic=containers-kubernetes-service-cli#storage-volume-ls-cli)


## `subnets` commands
{: #icks_map_subnets}

List available portable subnets in your IBM Cloud infrastructure account.

* [`ibmcloud ks subnets`](/docs/containers?topic=containers-kubernetes-service-cli#subnets-cli)


## `versions` commands
{: #icks_map_versions}

List all the container platform versions that are available for IBM Cloud Kubernetes Service clusters.

* [`ibmcloud ks versions`](/docs/containers?topic=containers-kubernetes-service-cli#versions-cli)


## `vlan` commands
{: #icks_map_vlan}

List public and private VLANs for a zone and view the VLAN spanning status.

* **`vlan spanning`**: View the VLAN spanning status for your IBM Cloud classic infrastructure account.
    * [`ibmcloud ks vlan help`](/docs/containers?topic=containers-kubernetes-service-cli#vlan-help-cli)
    * [`ibmcloud ks vlan ls`](/docs/containers?topic=containers-kubernetes-service-cli#vlan-ls-cli)
    * [`ibmcloud ks vlan spanning get`](/docs/containers?topic=containers-kubernetes-service-cli#vlan-spanning-get-cli)
    * [`ibmcloud ks vlan spanning help`](/docs/containers?topic=containers-kubernetes-service-cli#vlan-spanning-help-cli)


## `vni` commands
{: #icks_map_vni}

Attach, detach, and list Virtual Network Interfaces on worker nodes.

* **`vni attach`**: Attach a Virtual Network Interface to a worker node.
    * [`ibmcloud ks vni attach baremetal`](/docs/containers?topic=containers-kubernetes-service-cli#vni-attach-baremetal-cli)
    * [`ibmcloud ks vni attach help`](/docs/containers?topic=containers-kubernetes-service-cli#vni-attach-help-cli)
    * [`ibmcloud ks vni detach`](/docs/containers?topic=containers-kubernetes-service-cli#vni-detach-cli)
    * [`ibmcloud ks vni help`](/docs/containers?topic=containers-kubernetes-service-cli#vni-help-cli)
    * [`ibmcloud ks vni ls`](/docs/containers?topic=containers-kubernetes-service-cli#vni-ls-cli)


## `vpc` commands
{: #icks_map_vpc}

Get information about VPCs and manage VPC clusters.

* **`vpc outbound-traffic-protection`**: Change the outbound traffic protection for a Secure By Default VPC cluster.
* **`vpc secure-by-default`**: Modify Secure By Default Network settings for a VPC cluster.
    * [`ibmcloud ks vpc help`](/docs/containers?topic=containers-kubernetes-service-cli#vpc-help-cli)
    * [`ibmcloud ks vpc ls`](/docs/containers?topic=containers-kubernetes-service-cli#vpc-ls-cli)
    * [`ibmcloud ks vpc outbound-traffic-protection disable`](/docs/containers?topic=containers-kubernetes-service-cli#vpc-outbound-traffic-protection-disable-cli)
    * [`ibmcloud ks vpc outbound-traffic-protection enable`](/docs/containers?topic=containers-kubernetes-service-cli#vpc-outbound-traffic-protection-enable-cli)
    * [`ibmcloud ks vpc outbound-traffic-protection help`](/docs/containers?topic=containers-kubernetes-service-cli#vpc-outbound-traffic-protection-help-cli)
    * [`ibmcloud ks vpc secure-by-default enable`](/docs/containers?topic=containers-kubernetes-service-cli#vpc-secure-by-default-enable-cli)
    * [`ibmcloud ks vpc secure-by-default help`](/docs/containers?topic=containers-kubernetes-service-cli#vpc-secure-by-default-help-cli)


## `webhook-create` commands
{: #icks_map_webhook-create}

Register a webhook in a cluster.

* [`ibmcloud ks webhook-create`](/docs/containers?topic=containers-kubernetes-service-cli#webhook-create-cli)


## `worker` commands
{: #icks_map_worker}

View and modify worker nodes for a cluster.

* [`ibmcloud ks worker get`](/docs/containers?topic=containers-kubernetes-service-cli#worker-get-cli)
* [`ibmcloud ks worker help`](/docs/containers?topic=containers-kubernetes-service-cli#worker-help-cli)
* [`ibmcloud ks worker ls`](/docs/containers?topic=containers-kubernetes-service-cli#worker-ls-cli)
* [`ibmcloud ks worker reboot`](/docs/containers?topic=containers-kubernetes-service-cli#worker-reboot-cli)
* [`ibmcloud ks worker reload`](/docs/containers?topic=containers-kubernetes-service-cli#worker-reload-cli)
* [`ibmcloud ks worker replace`](/docs/containers?topic=containers-kubernetes-service-cli#worker-replace-cli)
* [`ibmcloud ks worker rm`](/docs/containers?topic=containers-kubernetes-service-cli#worker-rm-cli)
* [`ibmcloud ks worker update`](/docs/containers?topic=containers-kubernetes-service-cli#worker-update-cli)


## `worker-pool` commands
{: #icks_map_worker-pool}

View and modify worker pools for a cluster.

* **`worker-pool create`**: Add a worker pool to a cluster. No worker nodes are created until zones are added to the worker pool.
* **`worker-pool label`**: Set and remove custom Kubernetes labels for all worker nodes in a worker pool.
* **`worker-pool operating-system`**: Manage the operating system of a worker pool.
* **`worker-pool taint`**: Set and remove Kubernetes taints for all worker nodes in a worker pool.
    * [`ibmcloud ks worker-pool create classic`](/docs/containers?topic=containers-kubernetes-service-cli#worker-pool-create-classic-cli)
    * [`ibmcloud ks worker-pool create help`](/docs/containers?topic=containers-kubernetes-service-cli#worker-pool-create-help-cli)
    * [`ibmcloud ks worker-pool create satellite`](/docs/containers?topic=containers-kubernetes-service-cli#worker-pool-create-satellite-cli)
    * [`ibmcloud ks worker-pool create vpc-classic`](/docs/containers?topic=containers-kubernetes-service-cli#worker-pool-create-vpc-classic-cli)
    * [`ibmcloud ks worker-pool create vpc-gen2`](/docs/containers?topic=containers-kubernetes-service-cli#worker-pool-create-vpc-gen2-cli)
    * [`ibmcloud ks worker-pool get`](/docs/containers?topic=containers-kubernetes-service-cli#worker-pool-get-cli)
    * [`ibmcloud ks worker-pool help`](/docs/containers?topic=containers-kubernetes-service-cli#worker-pool-help-cli)
    * [`ibmcloud ks worker-pool label help`](/docs/containers?topic=containers-kubernetes-service-cli#worker-pool-label-help-cli)
    * [`ibmcloud ks worker-pool label rm`](/docs/containers?topic=containers-kubernetes-service-cli#worker-pool-label-rm-cli)
    * [`ibmcloud ks worker-pool label set`](/docs/containers?topic=containers-kubernetes-service-cli#worker-pool-label-set-cli)
    * [`ibmcloud ks worker-pool ls`](/docs/containers?topic=containers-kubernetes-service-cli#worker-pool-ls-cli)
    * [`ibmcloud ks worker-pool operating-system help`](/docs/containers?topic=containers-kubernetes-service-cli#worker-pool-operating-system-help-cli)
    * [`ibmcloud ks worker-pool operating-system set`](/docs/containers?topic=containers-kubernetes-service-cli#worker-pool-operating-system-set-cli)
    * [`ibmcloud ks worker-pool rebalance`](/docs/containers?topic=containers-kubernetes-service-cli#worker-pool-rebalance-cli)
    * [`ibmcloud ks worker-pool resize`](/docs/containers?topic=containers-kubernetes-service-cli#worker-pool-resize-cli)
    * [`ibmcloud ks worker-pool rm`](/docs/containers?topic=containers-kubernetes-service-cli#worker-pool-rm-cli)
    * [`ibmcloud ks worker-pool taint help`](/docs/containers?topic=containers-kubernetes-service-cli#worker-pool-taint-help-cli)
    * [`ibmcloud ks worker-pool taint rm`](/docs/containers?topic=containers-kubernetes-service-cli#worker-pool-taint-rm-cli)
    * [`ibmcloud ks worker-pool taint set`](/docs/containers?topic=containers-kubernetes-service-cli#worker-pool-taint-set-cli)
    * [`ibmcloud ks worker-pool zones`](/docs/containers?topic=containers-kubernetes-service-cli#worker-pool-zones-cli)


## `zone` commands
{: #icks_map_zone}

List availability zones and modify the zones attached to a worker pool.

* **`zone add`**: Add a zone to one or more worker pools in a cluster.
    * [`ibmcloud ks zone add classic`](/docs/containers?topic=containers-kubernetes-service-cli#zone-add-classic-cli)
    * [`ibmcloud ks zone add help`](/docs/containers?topic=containers-kubernetes-service-cli#zone-add-help-cli)
    * [`ibmcloud ks zone add satellite`](/docs/containers?topic=containers-kubernetes-service-cli#zone-add-satellite-cli)
    * [`ibmcloud ks zone add vpc-classic`](/docs/containers?topic=containers-kubernetes-service-cli#zone-add-vpc-classic-cli)
    * [`ibmcloud ks zone add vpc-gen2`](/docs/containers?topic=containers-kubernetes-service-cli#zone-add-vpc-gen2-cli)
    * [`ibmcloud ks zone help`](/docs/containers?topic=containers-kubernetes-service-cli#zone-help-cli)
    * [`ibmcloud ks zone ls`](/docs/containers?topic=containers-kubernetes-service-cli#zone-ls-cli)
    * [`ibmcloud ks zone network-set`](/docs/containers?topic=containers-kubernetes-service-cli#zone-network-set-cli)
    * [`ibmcloud ks zone rm`](/docs/containers?topic=containers-kubernetes-service-cli#zone-rm-cli)
