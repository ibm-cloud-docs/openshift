---

copyright: 
  years: 2022, 2026
lastupdated: "2026-08-26"

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

* [`ibmcloud oc api`](/docs/openshift?topic=openshift-kubernetes-service-cli#api-cli)


## `api-key` commands
{: #icks_map_api-key}

View information about the API key for a cluster or reset it to a new key.

* [`ibmcloud oc api-key help`](/docs/openshift?topic=openshift-kubernetes-service-cli#api-key-help-cli)
* [`ibmcloud oc api-key info`](/docs/openshift?topic=openshift-kubernetes-service-cli#api-key-info-cli)
* [`ibmcloud oc api-key reset`](/docs/openshift?topic=openshift-kubernetes-service-cli#api-key-reset-cli)


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
    * [`ibmcloud oc cluster addon disable acm`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-addon-disable-acm-cli)
    * [`ibmcloud oc cluster addon disable cluster-autoscaler`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-addon-disable-cluster-autoscaler-cli)
    * [`ibmcloud oc cluster addon disable debug-tool`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-addon-disable-debug-tool-cli)
    * [`ibmcloud oc cluster addon disable help`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-addon-disable-help-cli)
    * [`ibmcloud oc cluster addon disable hpcs-router`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-addon-disable-hpcs-router-cli)
    * **Beta** [`ibmcloud oc cluster addon disable ibm-storage-operator`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-addon-disable-ibm-storage-operator-cli)
    * [`ibmcloud oc cluster addon disable image-key-synchronizer`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-addon-disable-image-key-synchronizer-cli)
    * [`ibmcloud oc cluster addon disable knative`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-addon-disable-knative-cli)
    * [`ibmcloud oc cluster addon disable kube-terminal`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-addon-disable-kube-terminal-cli)
    * [`ibmcloud oc cluster addon disable openshift-data-foundation`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-addon-disable-openshift-data-foundation-cli)
    * [`ibmcloud oc cluster addon disable static-route`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-addon-disable-static-route-cli)
    * [`ibmcloud oc cluster addon disable vpc-block-csi-driver`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-addon-disable-vpc-block-csi-driver-cli)
    * [`ibmcloud oc cluster addon enable acm`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-addon-enable-acm-cli)
    * [`ibmcloud oc cluster addon enable cluster-autoscaler`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-addon-enable-cluster-autoscaler-cli)
    * [`ibmcloud oc cluster addon enable debug-tool`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-addon-enable-debug-tool-cli)
    * [`ibmcloud oc cluster addon enable help`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-addon-enable-help-cli)
    * [`ibmcloud oc cluster addon enable hpcs-router`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-addon-enable-hpcs-router-cli)
    * **Beta** [`ibmcloud oc cluster addon enable ibm-storage-operator`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-addon-enable-ibm-storage-operator-cli)
    * [`ibmcloud oc cluster addon enable image-key-synchronizer`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-addon-enable-image-key-synchronizer-cli)
    * **Deprecated** [`ibmcloud oc cluster addon enable istio-extras`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-addon-enable-istio-extras-cli)
    * **Deprecated** [`ibmcloud oc cluster addon enable istio-sample-bookinfo`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-addon-enable-istio-sample-bookinfo-cli)
    * [`ibmcloud oc cluster addon enable openshift-data-foundation`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-addon-enable-openshift-data-foundation-cli)
    * [`ibmcloud oc cluster addon enable static-route`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-addon-enable-static-route-cli)
    * [`ibmcloud oc cluster addon get`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-addon-get-cli)
    * [`ibmcloud oc cluster addon help`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-addon-help-cli)
    * [`ibmcloud oc cluster addon ls`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-addon-ls-cli)
    * [`ibmcloud oc cluster addon options`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-addon-options-cli)
    * [`ibmcloud oc cluster addon update acm`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-addon-update-acm-cli)
    * [`ibmcloud oc cluster addon update alb-oauth-proxy`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-addon-update-alb-oauth-proxy-cli)
    * [`ibmcloud oc cluster addon update cluster-autoscaler`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-addon-update-cluster-autoscaler-cli)
    * [`ibmcloud oc cluster addon update debug-tool`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-addon-update-debug-tool-cli)
    * **Beta** [`ibmcloud oc cluster addon update headlamp`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-addon-update-headlamp-cli)
    * [`ibmcloud oc cluster addon update help`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-addon-update-help-cli)
    * [`ibmcloud oc cluster addon update hpcs-router`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-addon-update-hpcs-router-cli)
    * **Beta** [`ibmcloud oc cluster addon update ibm-storage-operator`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-addon-update-ibm-storage-operator-cli)
    * [`ibmcloud oc cluster addon update image-key-synchronizer`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-addon-update-image-key-synchronizer-cli)
    * [`ibmcloud oc cluster addon update istio`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-addon-update-istio-cli)
    * **Deprecated** [`ibmcloud oc cluster addon update istio-extras`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-addon-update-istio-extras-cli)
    * **Deprecated** [`ibmcloud oc cluster addon update istio-sample-bookinfo`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-addon-update-istio-sample-bookinfo-cli)
    * [`ibmcloud oc cluster addon update knative`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-addon-update-knative-cli)
    * [`ibmcloud oc cluster addon update kube-terminal`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-addon-update-kube-terminal-cli)
    * [`ibmcloud oc cluster addon update openshift-data-foundation`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-addon-update-openshift-data-foundation-cli)
    * [`ibmcloud oc cluster addon update static-route`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-addon-update-static-route-cli)
    * [`ibmcloud oc cluster addon update vpc-block-csi-driver`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-addon-update-vpc-block-csi-driver-cli)
    * [`ibmcloud oc cluster addon versions`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-addon-versions-cli)
    * [`ibmcloud oc cluster ca create`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-ca-create-cli)
    * [`ibmcloud oc cluster ca get`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-ca-get-cli)
    * [`ibmcloud oc cluster ca help`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-ca-help-cli)
    * [`ibmcloud oc cluster ca rotate`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-ca-rotate-cli)
    * [`ibmcloud oc cluster ca status`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-ca-status-cli)
    * [`ibmcloud oc cluster config`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-config-cli)
    * [`ibmcloud oc cluster create classic`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-create-classic-cli)
    * [`ibmcloud oc cluster create help`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-create-help-cli)
    * [`ibmcloud oc cluster create satellite`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-create-satellite-cli)
    * [`ibmcloud oc cluster create vpc-classic`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-create-vpc-classic-cli)
    * [`ibmcloud oc cluster create vpc-gen2`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-create-vpc-gen2-cli)
    * [`ibmcloud oc cluster get`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-get-cli)
    * [`ibmcloud oc cluster help`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-help-cli)
    * [`ibmcloud oc cluster image-security disable`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-image-security-disable-cli)
    * [`ibmcloud oc cluster image-security enable`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-image-security-enable-cli)
    * [`ibmcloud oc cluster image-security help`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-image-security-help-cli)
    * [`ibmcloud oc cluster ls`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-ls-cli)
    * [`ibmcloud oc cluster master audit-webhook help`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-master-audit-webhook-help-cli)
    * [`ibmcloud oc cluster master console-oauth-access get`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-master-console-oauth-access-get-cli)
    * [`ibmcloud oc cluster master console-oauth-access help`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-master-console-oauth-access-help-cli)
    * [`ibmcloud oc cluster master console-oauth-access set`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-master-console-oauth-access-set-cli)
    * [`ibmcloud oc cluster master help`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-master-help-cli)
    * [`ibmcloud oc cluster master pod-security get`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-master-pod-security-get-cli)
    * [`ibmcloud oc cluster master pod-security help`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-master-pod-security-help-cli)
    * [`ibmcloud oc cluster master pod-security policy disable`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-master-pod-security-policy-disable-cli)
    * [`ibmcloud oc cluster master pod-security policy enable`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-master-pod-security-policy-enable-cli)
    * [`ibmcloud oc cluster master pod-security policy get`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-master-pod-security-policy-get-cli)
    * [`ibmcloud oc cluster master pod-security policy help`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-master-pod-security-policy-help-cli)
    * [`ibmcloud oc cluster master pod-security set`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-master-pod-security-set-cli)
    * [`ibmcloud oc cluster master pod-security unset`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-master-pod-security-unset-cli)
    * **Deprecated** [`ibmcloud oc cluster master private-service-endpoint allowlist add`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-master-private-service-endpoint-allowlist-add-cli)
    * **Deprecated** [`ibmcloud ks cluster master private-service-endpoint allowlist disable`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-master-private-service-endpoint-allowlist-disable-cli)
    * **Deprecated** [`ibmcloud ks cluster master private-service-endpoint allowlist enable`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-master-private-service-endpoint-allowlist-enable-cli)
    * **Deprecated** [`ibmcloud oc cluster master private-service-endpoint allowlist get`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-master-private-service-endpoint-allowlist-get-cli)
    * [`ibmcloud oc cluster master private-service-endpoint allowlist help`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-master-private-service-endpoint-allowlist-help-cli)
    * **Deprecated** [`ibmcloud oc cluster master private-service-endpoint allowlist rm`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-master-private-service-endpoint-allowlist-rm-cli)
    * [`ibmcloud oc cluster master private-service-endpoint enable`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-master-private-service-endpoint-enable-cli)
    * [`ibmcloud oc cluster master private-service-endpoint help`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-master-private-service-endpoint-help-cli)
    * [`ibmcloud oc cluster master public-service-endpoint disable`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-master-public-service-endpoint-disable-cli)
    * [`ibmcloud oc cluster master public-service-endpoint enable`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-master-public-service-endpoint-enable-cli)
    * [`ibmcloud oc cluster master public-service-endpoint help`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-master-public-service-endpoint-help-cli)
    * [`ibmcloud oc cluster master refresh`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-master-refresh-cli)
    * [`ibmcloud oc cluster master satellite-service-endpoint allowlist add`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-master-satellite-service-endpoint-allowlist-add-cli)
    * [`ibmcloud ks cluster master satellite-service-endpoint allowlist disable`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-master-satellite-service-endpoint-allowlist-disable-cli)
    * [`ibmcloud ks cluster master satellite-service-endpoint allowlist enable`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-master-satellite-service-endpoint-allowlist-enable-cli)
    * [`ibmcloud oc cluster master satellite-service-endpoint allowlist get`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-master-satellite-service-endpoint-allowlist-get-cli)
    * [`ibmcloud ks cluster master satellite-service-endpoint allowlist help`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-master-satellite-service-endpoint-allowlist-help-cli)
    * [`ibmcloud oc cluster master satellite-service-endpoint allowlist rm`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-master-satellite-service-endpoint-allowlist-rm-cli)
    * [`ibmcloud oc cluster master satellite-service-endpoint help`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-master-satellite-service-endpoint-help-cli)
    * [`ibmcloud oc cluster master update`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-master-update-cli)
    * [`ibmcloud oc cluster pull-secret apply`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-pull-secret-apply-cli)
    * [`ibmcloud oc cluster pull-secret help`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-pull-secret-help-cli)
    * [`ibmcloud oc cluster rm`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-rm-cli)
    * [`ibmcloud oc cluster service bind`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-service-bind-cli)
    * [`ibmcloud oc cluster service help`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-service-help-cli)
    * [`ibmcloud oc cluster service ls`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-service-ls-cli)
    * [`ibmcloud oc cluster service unbind`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-service-unbind-cli)
    * [`ibmcloud oc cluster subnet add`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-subnet-add-cli)
    * [`ibmcloud oc cluster subnet create`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-subnet-create-cli)
    * [`ibmcloud oc cluster subnet detach`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-subnet-detach-cli)
    * [`ibmcloud oc cluster subnet help`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-subnet-help-cli)


## `credential` commands
{: #icks_map_credential}

Set and unset credentials that allow you to access the IBM Cloud classic infrastructure portfolio through your IBM Cloud account.

* **`credential set`**: Set credentials that allow you to access the IBM Cloud classic infrastructure portfolio through your IBM Cloud account. This command applies to the targeted resource group, or to the default resource group if no resource group is targeted.
    * [`ibmcloud oc credential get`](/docs/openshift?topic=openshift-kubernetes-service-cli#credential-get-cli)
    * [`ibmcloud oc credential help`](/docs/openshift?topic=openshift-kubernetes-service-cli#credential-help-cli)
    * [`ibmcloud oc credential set classic`](/docs/openshift?topic=openshift-kubernetes-service-cli#credential-set-classic-cli)
    * [`ibmcloud oc credential set help`](/docs/openshift?topic=openshift-kubernetes-service-cli#credential-set-help-cli)
    * [`ibmcloud oc credential unset`](/docs/openshift?topic=openshift-kubernetes-service-cli#credential-unset-cli)


## `experimental` commands
{: #icks_map_experimental}

[Expires on 2026-10-21] Experiment with new commands. IMPORTANT: Commands here will retire after the [date] in their description.

* **`experimental trusted-profile`**: [Expires on 2026-10-21] View and set the trusted profile on a cluster or the default trusted profile for clusters created in a resource-group.
* **`experimental vni`**: [Deactivated on 2026-05-20! Use `ibmcloud ks vni` instead] Attach, detach, and list Virtual Network Interfaces on worker nodes.
    * [`ibmcloud oc experimental help`](/docs/openshift?topic=openshift-kubernetes-service-cli#experimental-help-cli)
    * [`ibmcloud oc experimental trusted-profile default get`](/docs/openshift?topic=openshift-kubernetes-service-cli#experimental-trusted-profile-default-get-cli)
    * [`ibmcloud oc experimental trusted-profile default help`](/docs/openshift?topic=openshift-kubernetes-service-cli#experimental-trusted-profile-default-help-cli)
    * [`ibmcloud oc experimental trusted-profile default set`](/docs/openshift?topic=openshift-kubernetes-service-cli#experimental-trusted-profile-default-set-cli)
    * [`ibmcloud oc experimental trusted-profile get`](/docs/openshift?topic=openshift-kubernetes-service-cli#experimental-trusted-profile-get-cli)
    * [`ibmcloud oc experimental trusted-profile help`](/docs/openshift?topic=openshift-kubernetes-service-cli#experimental-trusted-profile-help-cli)
    * [`ibmcloud oc experimental trusted-profile set`](/docs/openshift?topic=openshift-kubernetes-service-cli#experimental-trusted-profile-set-cli)


## `flavor` commands
{: #icks_map_flavor}

Getting flavor related information. Flavors determine how much virtual CPU, memory, and disk space is available to each worker node.

* [`ibmcloud oc flavor get`](/docs/openshift?topic=openshift-kubernetes-service-cli#flavor-get-cli)
* [`ibmcloud oc flavor help`](/docs/openshift?topic=openshift-kubernetes-service-cli#flavor-help-cli)
* [`ibmcloud oc flavor ls`](/docs/openshift?topic=openshift-kubernetes-service-cli#flavor-ls-cli)


## `infra-permissions` commands
{: #icks_map_infra-permissions}

View information about infrastructure permissions that allow you to access the IBM Cloud classic infrastructure portfolio through your IBM Cloud account.

* [`ibmcloud oc infra-permissions get`](/docs/openshift?topic=openshift-kubernetes-service-cli#infra-permissions-get-cli)
* [`ibmcloud oc infra-permissions help`](/docs/openshift?topic=openshift-kubernetes-service-cli#infra-permissions-help-cli)


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
    * [`ibmcloud oc ingress alb autoscale get`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-alb-autoscale-get-cli)
    * [`ibmcloud oc ingress alb autoscale help`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-alb-autoscale-help-cli)
    * [`ibmcloud oc ingress alb autoscale set`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-alb-autoscale-set-cli)
    * [`ibmcloud oc ingress alb autoscale unset`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-alb-autoscale-unset-cli)
    * [`ibmcloud oc ingress alb autoupdate disable`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-alb-autoupdate-disable-cli)
    * [`ibmcloud oc ingress alb autoupdate enable`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-alb-autoupdate-enable-cli)
    * [`ibmcloud oc ingress alb autoupdate get`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-alb-autoupdate-get-cli)
    * [`ibmcloud oc ingress alb autoupdate help`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-alb-autoupdate-help-cli)
    * [`ibmcloud oc ingress alb create classic`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-alb-create-classic-cli)
    * [`ibmcloud oc ingress alb create help`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-alb-create-help-cli)
    * [`ibmcloud oc ingress alb create vpc-gen2`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-alb-create-vpc-gen2-cli)
    * [`ibmcloud oc ingress alb disable`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-alb-disable-cli)
    * [`ibmcloud oc ingress alb enable classic`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-alb-enable-classic-cli)
    * [`ibmcloud oc ingress alb enable help`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-alb-enable-help-cli)
    * [`ibmcloud oc ingress alb enable vpc-gen2`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-alb-enable-vpc-gen2-cli)
    * [`ibmcloud oc ingress alb get`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-alb-get-cli)
    * [`ibmcloud oc ingress alb health-checker disable`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-alb-health-checker-disable-cli)
    * [`ibmcloud oc ingress alb health-checker enable`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-alb-health-checker-enable-cli)
    * [`ibmcloud oc ingress alb health-checker get`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-alb-health-checker-get-cli)
    * [`ibmcloud oc ingress alb health-checker help`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-alb-health-checker-help-cli)
    * [`ibmcloud oc ingress alb help`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-alb-help-cli)
    * [`ibmcloud oc ingress alb ls`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-alb-ls-cli)
    * [`ibmcloud oc ingress alb update`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-alb-update-cli)
    * [`ibmcloud oc ingress alb versions`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-alb-versions-cli)
    * [`ibmcloud oc ingress domain create`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-domain-create-cli)
    * [`ibmcloud oc ingress domain default help`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-domain-default-help-cli)
    * [`ibmcloud oc ingress domain default replace`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-domain-default-replace-cli)
    * [`ibmcloud oc ingress domain get`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-domain-get-cli)
    * [`ibmcloud oc ingress domain help`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-domain-help-cli)
    * [`ibmcloud oc ingress domain ls`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-domain-ls-cli)
    * [`ibmcloud oc ingress domain rm`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-domain-rm-cli)
    * [`ibmcloud oc ingress domain secret help`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-domain-secret-help-cli)
    * [`ibmcloud oc ingress domain secret regenerate`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-domain-secret-regenerate-cli)
    * [`ibmcloud oc ingress domain secret rm`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-domain-secret-rm-cli)
    * [`ibmcloud oc ingress domain update`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-domain-update-cli)
    * [`ibmcloud oc ingress help`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-help-cli)
    * [`ibmcloud oc ingress instance default help`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-instance-default-help-cli)
    * [`ibmcloud oc ingress instance default set`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-instance-default-set-cli)
    * [`ibmcloud oc ingress instance default unset`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-instance-default-unset-cli)
    * [`ibmcloud oc ingress instance get`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-instance-get-cli)
    * [`ibmcloud oc ingress instance help`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-instance-help-cli)
    * [`ibmcloud oc ingress instance ls`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-instance-ls-cli)
    * [`ibmcloud oc ingress instance register`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-instance-register-cli)
    * [`ibmcloud oc ingress instance unregister`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-instance-unregister-cli)
    * [`ibmcloud oc ingress load-balancer backend help`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-load-balancer-backend-help-cli)
    * [`ibmcloud oc ingress load-balancer backend set`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-load-balancer-backend-set-cli)
    * [`ibmcloud oc ingress load-balancer get`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-load-balancer-get-cli)
    * [`ibmcloud oc ingress load-balancer help`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-load-balancer-help-cli)
    * [`ibmcloud oc ingress load-balancer proxy-protocol disable`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-load-balancer-proxy-protocol-disable-cli)
    * [`ibmcloud oc ingress load-balancer proxy-protocol enable`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-load-balancer-proxy-protocol-enable-cli)
    * [`ibmcloud oc ingress load-balancer proxy-protocol help`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-load-balancer-proxy-protocol-help-cli)
    * [`ibmcloud oc ingress secret create`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-secret-create-cli)
    * [`ibmcloud oc ingress secret field add`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-secret-field-add-cli)
    * [`ibmcloud oc ingress secret field help`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-secret-field-help-cli)
    * [`ibmcloud oc ingress secret field ls`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-secret-field-ls-cli)
    * [`ibmcloud oc ingress secret field rm`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-secret-field-rm-cli)
    * [`ibmcloud oc ingress secret get`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-secret-get-cli)
    * [`ibmcloud oc ingress secret help`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-secret-help-cli)
    * [`ibmcloud oc ingress secret ls`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-secret-ls-cli)
    * [`ibmcloud oc ingress secret rm`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-secret-rm-cli)
    * [`ibmcloud oc ingress secret update`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-secret-update-cli)
    * [`ibmcloud oc ingress security help`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-security-help-cli)
    * [`ibmcloud oc ingress security port80 disable`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-security-port80-disable-cli)
    * [`ibmcloud oc ingress security port80 enable`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-security-port80-enable-cli)
    * [`ibmcloud oc ingress security port80 get`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-security-port80-get-cli)
    * [`ibmcloud oc ingress security port80 help`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-security-port80-help-cli)
    * [`ibmcloud oc ingress status-report disable`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-status-report-disable-cli)
    * [`ibmcloud oc ingress status-report enable`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-status-report-enable-cli)
    * [`ibmcloud oc ingress status-report get`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-status-report-get-cli)
    * [`ibmcloud oc ingress status-report help`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-status-report-help-cli)
    * [`ibmcloud oc ingress status-report ignored-errors add`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-status-report-ignored-errors-add-cli)
    * [`ibmcloud oc ingress status-report ignored-errors help`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-status-report-ignored-errors-help-cli)
    * [`ibmcloud oc ingress status-report ignored-errors ls`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-status-report-ignored-errors-ls-cli)
    * [`ibmcloud oc ingress status-report ignored-errors rm`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-status-report-ignored-errors-rm-cli)


## `kms` commands
{: #icks_map_kms}

View and configure Key Management Service integrations.

* **`kms crk`**: List and configure the root keys for a Key Management Service instance.
* **`kms instance`**: View and configure available Key Management Service instances.
    * [`ibmcloud oc kms crk help`](/docs/openshift?topic=openshift-kubernetes-service-cli#kms-crk-help-cli)
    * [`ibmcloud oc kms crk ls`](/docs/openshift?topic=openshift-kubernetes-service-cli#kms-crk-ls-cli)
    * [`ibmcloud oc kms enable`](/docs/openshift?topic=openshift-kubernetes-service-cli#kms-enable-cli)
    * [`ibmcloud oc kms help`](/docs/openshift?topic=openshift-kubernetes-service-cli#kms-help-cli)
    * [`ibmcloud oc kms instance help`](/docs/openshift?topic=openshift-kubernetes-service-cli#kms-instance-help-cli)
    * [`ibmcloud oc kms instance ls`](/docs/openshift?topic=openshift-kubernetes-service-cli#kms-instance-ls-cli)


## `locations` commands
{: #icks_map_locations}

List supported IBM Cloud Kubernetes Service locations.

* [`ibmcloud oc locations`](/docs/openshift?topic=openshift-kubernetes-service-cli#locations-cli)


## `logging` commands
{: #icks_map_logging}

Forward logs from your cluster.

* **`logging autoupdate`**: Manage automatic updates of the Fluentd add-on in a cluster.
* **`logging config`**: View or modify log forwarding configurations for a cluster.
* **`logging filter`**: View or modify log filters for a cluster.
    * [`ibmcloud oc logging autoupdate disable`](/docs/openshift?topic=openshift-kubernetes-service-cli#logging-autoupdate-disable-cli)
    * [`ibmcloud oc logging autoupdate enable`](/docs/openshift?topic=openshift-kubernetes-service-cli#logging-autoupdate-enable-cli)
    * [`ibmcloud oc logging autoupdate get`](/docs/openshift?topic=openshift-kubernetes-service-cli#logging-autoupdate-get-cli)
    * [`ibmcloud oc logging autoupdate help`](/docs/openshift?topic=openshift-kubernetes-service-cli#logging-autoupdate-help-cli)
    * [`ibmcloud oc logging config create`](/docs/openshift?topic=openshift-kubernetes-service-cli#logging-config-create-cli)
    * [`ibmcloud oc logging config get`](/docs/openshift?topic=openshift-kubernetes-service-cli#logging-config-get-cli)
    * [`ibmcloud oc logging config help`](/docs/openshift?topic=openshift-kubernetes-service-cli#logging-config-help-cli)
    * [`ibmcloud oc logging config rm`](/docs/openshift?topic=openshift-kubernetes-service-cli#logging-config-rm-cli)
    * [`ibmcloud oc logging config update`](/docs/openshift?topic=openshift-kubernetes-service-cli#logging-config-update-cli)
    * [`ibmcloud oc logging filter create`](/docs/openshift?topic=openshift-kubernetes-service-cli#logging-filter-create-cli)
    * [`ibmcloud oc logging filter get`](/docs/openshift?topic=openshift-kubernetes-service-cli#logging-filter-get-cli)
    * [`ibmcloud oc logging filter help`](/docs/openshift?topic=openshift-kubernetes-service-cli#logging-filter-help-cli)
    * [`ibmcloud oc logging filter rm`](/docs/openshift?topic=openshift-kubernetes-service-cli#logging-filter-rm-cli)
    * [`ibmcloud oc logging filter update`](/docs/openshift?topic=openshift-kubernetes-service-cli#logging-filter-update-cli)
    * [`ibmcloud oc logging help`](/docs/openshift?topic=openshift-kubernetes-service-cli#logging-help-cli)
    * [`ibmcloud oc logging refresh`](/docs/openshift?topic=openshift-kubernetes-service-cli#logging-refresh-cli)


## `messages` commands
{: #icks_map_messages}

View the current user messages.

* [`ibmcloud oc messages`](/docs/openshift?topic=openshift-kubernetes-service-cli#messages-cli)


## `nlb-dns` commands
{: #icks_map_nlb-dns}

Create and manage host names for network load balancer (NLB) IP addresses in a cluster and health check monitors for host names.

* **`nlb-dns create`**: Create a DNS host name.
* **`nlb-dns monitor`**: Create and manage health check monitors for network load balancer (NLB) IP addresses and host names in a cluster
* **`nlb-dns rm`**: Remove an NLB IP or load balancer host name from an NLB host name.
* **`nlb-dns secret`**: Manage the secret for an NLB subdomain.
    * [`ibmcloud oc nlb-dns add`](/docs/openshift?topic=openshift-kubernetes-service-cli#nlb-dns-add-cli)
    * [`ibmcloud oc nlb-dns create classic`](/docs/openshift?topic=openshift-kubernetes-service-cli#nlb-dns-create-classic-cli)
    * [`ibmcloud oc nlb-dns create help`](/docs/openshift?topic=openshift-kubernetes-service-cli#nlb-dns-create-help-cli)
    * [`ibmcloud oc nlb-dns create vpc-gen2`](/docs/openshift?topic=openshift-kubernetes-service-cli#nlb-dns-create-vpc-gen2-cli)
    * [`ibmcloud oc nlb-dns get`](/docs/openshift?topic=openshift-kubernetes-service-cli#nlb-dns-get-cli)
    * [`ibmcloud oc nlb-dns help`](/docs/openshift?topic=openshift-kubernetes-service-cli#nlb-dns-help-cli)
    * [`ibmcloud oc nlb-dns ls`](/docs/openshift?topic=openshift-kubernetes-service-cli#nlb-dns-ls-cli)
    * [`ibmcloud oc nlb-dns monitor configure`](/docs/openshift?topic=openshift-kubernetes-service-cli#nlb-dns-monitor-configure-cli)
    * [`ibmcloud oc nlb-dns monitor disable`](/docs/openshift?topic=openshift-kubernetes-service-cli#nlb-dns-monitor-disable-cli)
    * [`ibmcloud oc nlb-dns monitor enable`](/docs/openshift?topic=openshift-kubernetes-service-cli#nlb-dns-monitor-enable-cli)
    * [`ibmcloud oc nlb-dns monitor get`](/docs/openshift?topic=openshift-kubernetes-service-cli#nlb-dns-monitor-get-cli)
    * [`ibmcloud oc nlb-dns monitor help`](/docs/openshift?topic=openshift-kubernetes-service-cli#nlb-dns-monitor-help-cli)
    * [`ibmcloud oc nlb-dns monitor ls`](/docs/openshift?topic=openshift-kubernetes-service-cli#nlb-dns-monitor-ls-cli)
    * [`ibmcloud oc nlb-dns replace`](/docs/openshift?topic=openshift-kubernetes-service-cli#nlb-dns-replace-cli)
    * [`ibmcloud oc nlb-dns rm classic`](/docs/openshift?topic=openshift-kubernetes-service-cli#nlb-dns-rm-classic-cli)
    * [`ibmcloud oc nlb-dns rm help`](/docs/openshift?topic=openshift-kubernetes-service-cli#nlb-dns-rm-help-cli)
    * [`ibmcloud oc nlb-dns rm vpc-gen2`](/docs/openshift?topic=openshift-kubernetes-service-cli#nlb-dns-rm-vpc-gen2-cli)
    * [`ibmcloud oc nlb-dns secret help`](/docs/openshift?topic=openshift-kubernetes-service-cli#nlb-dns-secret-help-cli)
    * [`ibmcloud oc nlb-dns secret regenerate`](/docs/openshift?topic=openshift-kubernetes-service-cli#nlb-dns-secret-regenerate-cli)
    * [`ibmcloud oc nlb-dns secret rm`](/docs/openshift?topic=openshift-kubernetes-service-cli#nlb-dns-secret-rm-cli)


## `quota` commands
{: #icks_map_quota}

View the quota and limits for cluster-related resources in your IBM Cloud account.

* [`ibmcloud oc quota help`](/docs/openshift?topic=openshift-kubernetes-service-cli#quota-help-cli)
* [`ibmcloud oc quota ls`](/docs/openshift?topic=openshift-kubernetes-service-cli#quota-ls-cli)


## `script` commands
{: #icks_map_script}

Rewrite scripts that call IBM Cloud Kubernetes Service plug-in commands. Legacy-structured commands are replaced with beta-structured commands.

* [`ibmcloud oc script help`](/docs/openshift?topic=openshift-kubernetes-service-cli#script-help-cli)
* [`ibmcloud oc script update`](/docs/openshift?topic=openshift-kubernetes-service-cli#script-update-cli)


## `security-group` commands
{: #icks_map_security-group}

Run operations against a security group.

* [`ibmcloud oc security-group help`](/docs/openshift?topic=openshift-kubernetes-service-cli#security-group-help-cli)
* [`ibmcloud oc security-group ls`](/docs/openshift?topic=openshift-kubernetes-service-cli#security-group-ls-cli)
* [`ibmcloud oc security-group reset`](/docs/openshift?topic=openshift-kubernetes-service-cli#security-group-reset-cli)
* [`ibmcloud oc security-group sync`](/docs/openshift?topic=openshift-kubernetes-service-cli#security-group-sync-cli)


## `storage` commands
{: #icks_map_storage}

View and modify storage resources.

* **`storage attachment`**: View and modify storage volume attachments of worker nodes in your cluster.
* **`storage volume`**: View a list of storage volumes.
    * **Beta** [`ibmcloud oc storage attachment create`](/docs/openshift?topic=openshift-kubernetes-service-cli#storage-attachment-create-cli)
    * **Beta** [`ibmcloud oc storage attachment get`](/docs/openshift?topic=openshift-kubernetes-service-cli#storage-attachment-get-cli)
    * [`ibmcloud oc storage attachment help`](/docs/openshift?topic=openshift-kubernetes-service-cli#storage-attachment-help-cli)
    * **Beta** [`ibmcloud oc storage attachment ls`](/docs/openshift?topic=openshift-kubernetes-service-cli#storage-attachment-ls-cli)
    * **Beta** [`ibmcloud oc storage attachment rm`](/docs/openshift?topic=openshift-kubernetes-service-cli#storage-attachment-rm-cli)
    * [`ibmcloud oc storage help`](/docs/openshift?topic=openshift-kubernetes-service-cli#storage-help-cli)
    * **Beta** [`ibmcloud oc storage volume get`](/docs/openshift?topic=openshift-kubernetes-service-cli#storage-volume-get-cli)
    * [`ibmcloud oc storage volume help`](/docs/openshift?topic=openshift-kubernetes-service-cli#storage-volume-help-cli)
    * **Beta** [`ibmcloud oc storage volume ls`](/docs/openshift?topic=openshift-kubernetes-service-cli#storage-volume-ls-cli)


## `subnets` commands
{: #icks_map_subnets}

List available portable subnets in your IBM Cloud infrastructure account.

* [`ibmcloud oc subnets`](/docs/openshift?topic=openshift-kubernetes-service-cli#subnets-cli)


## `versions` commands
{: #icks_map_versions}

List all the container platform versions that are available for IBM Cloud Kubernetes Service clusters.

* [`ibmcloud oc versions`](/docs/openshift?topic=openshift-kubernetes-service-cli#versions-cli)


## `vlan` commands
{: #icks_map_vlan}

List public and private VLANs for a zone and view the VLAN spanning status.

* **`vlan spanning`**: View the VLAN spanning status for your IBM Cloud classic infrastructure account.
    * [`ibmcloud oc vlan help`](/docs/openshift?topic=openshift-kubernetes-service-cli#vlan-help-cli)
    * [`ibmcloud oc vlan ls`](/docs/openshift?topic=openshift-kubernetes-service-cli#vlan-ls-cli)
    * [`ibmcloud oc vlan spanning get`](/docs/openshift?topic=openshift-kubernetes-service-cli#vlan-spanning-get-cli)
    * [`ibmcloud oc vlan spanning help`](/docs/openshift?topic=openshift-kubernetes-service-cli#vlan-spanning-help-cli)


## `vni` commands
{: #icks_map_vni}

Attach, detach, and list Virtual Network Interfaces on worker nodes.

* **`vni attach`**: Attach a Virtual Network Interface to a worker node.
    * [`ibmcloud oc vni attach baremetal`](/docs/openshift?topic=openshift-kubernetes-service-cli#vni-attach-baremetal-cli)
    * [`ibmcloud oc vni attach help`](/docs/openshift?topic=openshift-kubernetes-service-cli#vni-attach-help-cli)
    * [`ibmcloud oc vni detach`](/docs/openshift?topic=openshift-kubernetes-service-cli#vni-detach-cli)
    * [`ibmcloud oc vni help`](/docs/openshift?topic=openshift-kubernetes-service-cli#vni-help-cli)
    * [`ibmcloud oc vni ls`](/docs/openshift?topic=openshift-kubernetes-service-cli#vni-ls-cli)


## `vpc` commands
{: #icks_map_vpc}

Get information about VPCs and manage VPC clusters.

* **`vpc outbound-traffic-protection`**: Change the outbound traffic protection for a Secure By Default VPC cluster.
* **`vpc secure-by-default`**: Modify Secure By Default Network settings for a VPC cluster.
    * [`ibmcloud oc vpc help`](/docs/openshift?topic=openshift-kubernetes-service-cli#vpc-help-cli)
    * [`ibmcloud oc vpc ls`](/docs/openshift?topic=openshift-kubernetes-service-cli#vpc-ls-cli)
    * [`ibmcloud oc vpc outbound-traffic-protection disable`](/docs/openshift?topic=openshift-kubernetes-service-cli#vpc-outbound-traffic-protection-disable-cli)
    * [`ibmcloud oc vpc outbound-traffic-protection enable`](/docs/openshift?topic=openshift-kubernetes-service-cli#vpc-outbound-traffic-protection-enable-cli)
    * [`ibmcloud oc vpc outbound-traffic-protection help`](/docs/openshift?topic=openshift-kubernetes-service-cli#vpc-outbound-traffic-protection-help-cli)
    * [`ibmcloud oc vpc secure-by-default enable`](/docs/openshift?topic=openshift-kubernetes-service-cli#vpc-secure-by-default-enable-cli)
    * [`ibmcloud oc vpc secure-by-default help`](/docs/openshift?topic=openshift-kubernetes-service-cli#vpc-secure-by-default-help-cli)


## `webhook-create` commands
{: #icks_map_webhook-create}

Register a webhook in a cluster.

* [`ibmcloud oc webhook-create`](/docs/openshift?topic=openshift-kubernetes-service-cli#webhook-create-cli)


## `worker` commands
{: #icks_map_worker}

View and modify worker nodes for a cluster.

* [`ibmcloud oc worker get`](/docs/openshift?topic=openshift-kubernetes-service-cli#worker-get-cli)
* [`ibmcloud oc worker help`](/docs/openshift?topic=openshift-kubernetes-service-cli#worker-help-cli)
* [`ibmcloud oc worker ls`](/docs/openshift?topic=openshift-kubernetes-service-cli#worker-ls-cli)
* [`ibmcloud oc worker reboot`](/docs/openshift?topic=openshift-kubernetes-service-cli#worker-reboot-cli)
* [`ibmcloud oc worker reload`](/docs/openshift?topic=openshift-kubernetes-service-cli#worker-reload-cli)
* [`ibmcloud oc worker replace`](/docs/openshift?topic=openshift-kubernetes-service-cli#worker-replace-cli)
* [`ibmcloud oc worker rm`](/docs/openshift?topic=openshift-kubernetes-service-cli#worker-rm-cli)
* [`ibmcloud oc worker update`](/docs/openshift?topic=openshift-kubernetes-service-cli#worker-update-cli)


## `worker-pool` commands
{: #icks_map_worker-pool}

View and modify worker pools for a cluster.

* **`worker-pool create`**: Add a worker pool to a cluster. No worker nodes are created until zones are added to the worker pool.
* **`worker-pool label`**: Set and remove custom Kubernetes labels for all worker nodes in a worker pool.
* **`worker-pool operating-system`**: Manage the operating system of a worker pool.
* **`worker-pool taint`**: Set and remove Kubernetes taints for all worker nodes in a worker pool.
    * [`ibmcloud oc worker-pool create classic`](/docs/openshift?topic=openshift-kubernetes-service-cli#worker-pool-create-classic-cli)
    * [`ibmcloud oc worker-pool create help`](/docs/openshift?topic=openshift-kubernetes-service-cli#worker-pool-create-help-cli)
    * [`ibmcloud oc worker-pool create satellite`](/docs/openshift?topic=openshift-kubernetes-service-cli#worker-pool-create-satellite-cli)
    * [`ibmcloud oc worker-pool create vpc-classic`](/docs/openshift?topic=openshift-kubernetes-service-cli#worker-pool-create-vpc-classic-cli)
    * [`ibmcloud oc worker-pool create vpc-gen2`](/docs/openshift?topic=openshift-kubernetes-service-cli#worker-pool-create-vpc-gen2-cli)
    * [`ibmcloud oc worker-pool get`](/docs/openshift?topic=openshift-kubernetes-service-cli#worker-pool-get-cli)
    * [`ibmcloud oc worker-pool help`](/docs/openshift?topic=openshift-kubernetes-service-cli#worker-pool-help-cli)
    * [`ibmcloud oc worker-pool label help`](/docs/openshift?topic=openshift-kubernetes-service-cli#worker-pool-label-help-cli)
    * [`ibmcloud oc worker-pool label rm`](/docs/openshift?topic=openshift-kubernetes-service-cli#worker-pool-label-rm-cli)
    * [`ibmcloud oc worker-pool label set`](/docs/openshift?topic=openshift-kubernetes-service-cli#worker-pool-label-set-cli)
    * [`ibmcloud oc worker-pool ls`](/docs/openshift?topic=openshift-kubernetes-service-cli#worker-pool-ls-cli)
    * [`ibmcloud oc worker-pool operating-system help`](/docs/openshift?topic=openshift-kubernetes-service-cli#worker-pool-operating-system-help-cli)
    * [`ibmcloud oc worker-pool operating-system set`](/docs/openshift?topic=openshift-kubernetes-service-cli#worker-pool-operating-system-set-cli)
    * [`ibmcloud oc worker-pool rebalance`](/docs/openshift?topic=openshift-kubernetes-service-cli#worker-pool-rebalance-cli)
    * [`ibmcloud oc worker-pool resize`](/docs/openshift?topic=openshift-kubernetes-service-cli#worker-pool-resize-cli)
    * [`ibmcloud oc worker-pool rm`](/docs/openshift?topic=openshift-kubernetes-service-cli#worker-pool-rm-cli)
    * [`ibmcloud oc worker-pool taint help`](/docs/openshift?topic=openshift-kubernetes-service-cli#worker-pool-taint-help-cli)
    * [`ibmcloud oc worker-pool taint rm`](/docs/openshift?topic=openshift-kubernetes-service-cli#worker-pool-taint-rm-cli)
    * [`ibmcloud oc worker-pool taint set`](/docs/openshift?topic=openshift-kubernetes-service-cli#worker-pool-taint-set-cli)
    * [`ibmcloud oc worker-pool zones`](/docs/openshift?topic=openshift-kubernetes-service-cli#worker-pool-zones-cli)


## `zone` commands
{: #icks_map_zone}

List availability zones and modify the zones attached to a worker pool.

* **`zone add`**: Add a zone to one or more worker pools in a cluster.
    * [`ibmcloud oc zone add classic`](/docs/openshift?topic=openshift-kubernetes-service-cli#zone-add-classic-cli)
    * [`ibmcloud oc zone add help`](/docs/openshift?topic=openshift-kubernetes-service-cli#zone-add-help-cli)
    * [`ibmcloud oc zone add satellite`](/docs/openshift?topic=openshift-kubernetes-service-cli#zone-add-satellite-cli)
    * [`ibmcloud oc zone add vpc-classic`](/docs/openshift?topic=openshift-kubernetes-service-cli#zone-add-vpc-classic-cli)
    * [`ibmcloud oc zone add vpc-gen2`](/docs/openshift?topic=openshift-kubernetes-service-cli#zone-add-vpc-gen2-cli)
    * [`ibmcloud oc zone help`](/docs/openshift?topic=openshift-kubernetes-service-cli#zone-help-cli)
    * [`ibmcloud oc zone ls`](/docs/openshift?topic=openshift-kubernetes-service-cli#zone-ls-cli)
    * [`ibmcloud oc zone network-set`](/docs/openshift?topic=openshift-kubernetes-service-cli#zone-network-set-cli)
    * [`ibmcloud oc zone rm`](/docs/openshift?topic=openshift-kubernetes-service-cli#zone-rm-cli)
