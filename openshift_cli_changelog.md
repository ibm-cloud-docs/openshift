---

copyright:
  years: 2014, 2020
lastupdated: "2020-03-17"

keywords: openshift, red hat, red hat openshift, rhos, roks, rhoks, oc, ibmcloud oc

subcollection: openshift

---

{:codeblock: .codeblock}
{:deprecated: .deprecated}
{:download: .download}
{:external: target="_blank" .external}
{:faq: data-hd-content-type='faq'}
{:gif: data-image-type='gif'}
{:help: data-hd-content-type='help'}
{:important: .important}
{:new_window: target="_blank"}
{:note: .note}
{:pre: .pre}
{:preview: .preview}
{:screen: .screen}
{:shortdesc: .shortdesc}
{:support: data-reuse='support'}
{:table: .aria-labeledby="caption"}
{:tip: .tip}
{:troubleshoot: data-hd-content-type='troubleshoot'}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:tsSymptoms: .tsSymptoms}


# CLI changelog
{: #cs_cli_changelog}

In the terminal, you are notified when updates to the `ibmcloud` CLI and plug-ins are available. Be sure to keep your CLI up-to-date so that you can use all available commands and flags.
{:shortdesc}

<br>
Refer to the following tables for a summary of changes for each version of the [Red Hat OpenShift on IBM Cloud plug-in](/docs/openshift?topic=openshift-openshift-cli), which uses the `ibmcloud oc` alias.

## Using version 1.0 of the plug-in
{: #changelog_beta}

Version 1.0 of the CLI plug-in was released on 16 March 2020. This version contains permanent syntax and behavior changes that are not backwards compatible.</br></br>To maintain all CLI functionality, update and test any automation before you update to 1.0 by checking out the [`ibmcloud oc script update` command](/docs/openshift?topic=openshift-kubernetes-service-cli#script_update) and setting your `IKS_BETA_VERSION` environment variable to `1.0`. After you update your scripts, update your CLI to version `1.0` of the plug-in.
{: important}

Check out the following syntax and behavior changes between each version of the CLI plug-in:

|Functionality|`0.2`|`0.3`|`0.4`|`1.0`|
|-------------|-----|-----|-----|-----|
| Supported? | Deprecated | Deprecated | Deprecated | Default |
| `ibmcloud oc help` output structure<ul><li>Legacy: Alphabetical list of commands</li><li>Beta: Categories of commands</li></ul> | Legacy | Legacy | Beta | Beta |
| Command structure<ul><li>Legacy: Hyphenated structure (`ibmcloud oc alb-cert-get`)</li><li>Beta: Spaced structure (`ibmcloud oc alb cert get`)</li></ul> | Legacy and beta | Legacy and beta | Legacy and beta | Beta |
| Positional arguments<ul><li>Legacy: Arguments specified by position (`cluster-get mycluster`)</li><li>Beta: Arguments specified by flags (`cluster get --cluster mycluster`)</li></ul> | Legacy and beta | Legacy and beta | Legacy and beta | Beta |
| Repeated arguments<ul><li>Legacy: Comma-delineated values (`--worker-pools pool1,pool2,pool3 ...`)</li><li>Beta: Repeated flags for each value with optional shorthand flag aliases (`-p pool1 -p pool2 ...`)</li></ul> | Legacy | Legacy | Legacy and beta | Beta |
| Flag format<ul><li>Legacy: Camel-case (`--showResources`)</li><li>Beta: Dashed (`--show-resources`)</li></ul> | Legacy | Legacy | Legacy and beta | Beta |
| Cluster context provided by `ibmcloud oc cluster-config`<ul><li>Legacy: Provides a command that you must copy and paste to set the new `kubeconfig` file as your current `KUBECONFIG` environment variable. You must set your environment variable before you can interact with your cluster.</li><li>Beta: Appends the new `kubeconfig` file to your existing `kubeconfig` file in `~/.kube/config` or the first file that is set by the `KUBECONFIG` environment variable. After you run `ibmcloud oc cluster config`, you can interact with your cluster immediately.</li></ul> | Legacy | Legacy | Legacy | Beta |
| API endpoint<ul><li>Legacy: [Target a region and use a regional endpoint to work with resources in that region](/docs/openshift?topic=openshift-regions-and-zones#bluemix_regions).</li><li>Beta: [Use the global endpoint to work with resources in any location](/docs/openshift?topic=openshift-regions-and-zones#bluemix_regions).</li></ul> | Legacy | Beta | Beta | Beta |
{: caption="Beta versions of the redesigned Red Hat OpenShift on IBM Cloud plug-in" caption-side="top"}
{: summary="The rows are read from left to right, with the functionality in column one, version 0.2 of the CLI in column two, version 0.3 in column three, version 0.4 in column four, and version 1.0 in column five."}

<br />


## Version 1.0
{: #10}

Review the following changes for 1.0 versions of the CLI plug-in.
{: shortdesc}

Version 1.0 of the CLI plug-in was released on 16 March 2020. This version contains permanent syntax and behavior changes that are not backwards compatible.</br></br>To maintain all CLI functionality, update and test any automation before you update to 1.0 by checking out the [`ibmcloud oc script update` command](/docs/openshift?topic=openshift-kubernetes-service-cli#script_update) and setting your `IKS_BETA_VERSION` environment variable to `1.0`. After you update your scripts, update your CLI to version `1.0` of the plug-in.
{: important}

|Version|Release date|Changes|
|-------|------------|-------|
| 1.0.0 | 16 Mar 2020 | Introduces permanent behavior and syntax changes that are not backwards compatible. For a summary of the changes in version 1.0, see [Using version 1.0 of the plug-in](#changelog_beta).|
{: caption="Overview of version changes for version 1.0 of the {{site.data.keyword.containerlong_notm}} CLI plug-in" caption-side="top"}
{: summary="Overview of version changes for version 1.0 of the {{site.data.keyword.containerlong_notm}} CLI plug-in"}

<br />


## Version 0.4
{: #04}

Review the following changes for 0.4 versions of the CLI plug-in.
{: shortdesc}

|Version|Release date|Changes|
|-------|------------|-------|
| 0.4.102 | 04 Mar 2020 | <ul><li>Version 3.11 clusters only: Adds the [`ibmcloud oc alb create classic`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_alb_create) command so that you can create and enable new public or private ALBs in a zone.</li><li>Removes the beta tag from `ibmcloud oc kms` commands.</li><li>Adds `--public-endpoint` as an optional flag to the `ibmcloud oc kms enable` command. Include this flag only if you want to use the KMS public service endpoint instead of the private service endpoint.</li><li>Fixes a bug so that the new `--version` flag is accepted in `ibmcloud oc cluster create` commands.</li><li>Help documentation updates:<ul><li>Fixes incorrect deprecation warnings for commands that are correctly formatted with version 1.0 syntax.</li><li>Removes incorrect `ibmcloud ks cs` syntax from command deprecation warnings.</li><li>Updates the help text in various languages.</li></ul></li></ul>|
| 0.4.90 | 19 Feb 2020 | <ul><li>Updates the Go version to 1.13.5 and removes `xgo`.</li><li>**Command updates**:<ul><li>Adds the `--provider` flag to the [`ibmcloud oc flavors`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_machine_types) command.</li><li>Accepts newer flag names like `--flavor` instead of `--machine-type` across various commands.</li><li>Deprecates the `--disable-deployment` flag of the [`ibmcloud oc alb configure vpc-classic`](/docs/openshift?topic=openshift-kubernetes-service-cli#cli_alb_configure_vpc_classic) command.</li></ul></li><li>**VPC-specific command updates**:<ul><li>Fixes the [`ibmcloud oc zone rm`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_zone_rm) command for VPC multizone clusters.</li><li>For the [`ibmcloud oc vpcs`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_vpcs) command, defaults to list only generation 1 (`vpc-classic`) VPCs.</li><li>Revises the [`ibmcloud oc worker-pool create vpc-classic`](/docs/openshift?topic=openshift-kubernetes-service-cli#cli_worker_pool_create_vpc_classic) command to remove the `--disable-disk-encrypt` flag and to hide the `--hardware` flag because it only accepts one value.</li></ul></li><li>**Help documentation updates**:<ul><li>Add deprecation warnings to encourage you to use the newer `classic` subcommands. For example, use `ibmcloud oc cluster create classic` instead of `ibmcloud oc cluster create`.</li><li>Adds links to the Red Hat OpenShift on IBM Cloud documentation in various help topics.</li><li>Standardizes formatting in help text, such as adding single quotes around variable names or styling for URLs.</li><li>Updates the help text in various languages.</li></ul></li></ul>|
| 0.4.66 | 19 Dec 2019 | <ul><li>Adds a **Status** field to the [`ibmcloud oc alb cert get`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_alb_cert_get) command. The previous **Status** field is now called **State**.</li><li>Fixes a bug so that help text is now properly displayed for top-level commands, such as `ibmcloud oc flavors` and `ibmcloud oc subnets`.</li></ul>|
| 0.4.64 | 11 Dec 2019 | <ul><li>Adds the `--entitlement` flag to the `ibmcloud oc cluster create` and `ibmcloud oc worker-pool create` commands. Include this flag only if you use this cluster with an [IBM Cloud Pak&trade;](/docs/openshift?topic=openshift-openshift_cloud_paks) that has an OpenShift entitlement.</li><li>Updates the Go version to 1.12.11.</li><li>Updates the help text in various languages.</li></ul>|
| 0.4.61 | 26 Nov 2019 | <ul><li>Removes the `kube-audit` log source option from `ibmcloud oc logging config` commands.</li><li>Adds a column to the output of `ibmcloud oc addon-versions` for the minimum required OpenShift version.</li><li>Adds a check to verify that you are logged in to the {{site.data.keyword.cloud_notm}} CLI before a command request is issued.</li><li>Updates the help text in various languages.</li></ul>|
| 0.4.51 | 07 Nov 2019 | <ul><li>Adds the [`ibmcloud oc kms crk ls`](/docs/openshift?topic=openshift-kubernetes-service-cli#ks_kms_crk_ls), [`ibmcloud oc kms enable`](/docs/openshift?topic=openshift-kubernetes-service-cli#ks_kms_enable), and [`ibmcloud oc kms instance ls`](/docs/openshift?topic=openshift-kubernetes-service-cli#ks_kms_instance_ls) commands to create and manage key management service (KMS) providers in a cluster.</li><li>Adds the optional `--skip-advance-permissions-check` flag to `ibmcloud oc cluster create` and `ibmcloud oc cluster rm`.</li><li>Fixes the error message for when no cluster name or ID is specified for `ibmcloud oc worker get` or `ibmcloud oc worker-pool get`.</li><li>Adds `public` and `private` as supported values for the `--hardware` flag of `ibmcloud oc worker-pool create classic`.</li><li>When the `--admin` flag is included in `ibmcloud oc cluster config`, removes `-admin` from the cluster name in the `KUBECONFIG` file path.</li><li>Updates all command help to use the new space-separated syntax.</li></ul>|
| 0.4.42 | 24 Oct 2019 |<ul><li>Adds the cluster ID to the output of `ibmcloud oc cluster create`.</li><li>Updates the Go version to 1.12.10 to fix `golang` vulnerabilities for [CVE-2019-16276](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-16276){: external}.</li></ul>|
| 0.4.38 | 14 Oct 2019 |<ul><li>Adds the `--secret-namespace` flag to the `ibmcloud oc nlb-dns create classic` command to specify the Kubernetes namespace that you want the SSL secret for the DNS subdomain to be created in.</li><li>Updates the help text in various languages.</li></ul>|
| 0.4.31 | 24 Sep 2019 |<ul><li>Removes the deprecated `region get`, `region set`, and `region ls` commands from help output.</li><li>Updates command structure to the new spaced format in help output.</li><li>Adds a warning to the output of legacy `cluster config` behavior. For more information, see the [version 1.0 plug-in documentation](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_beta).</li><li>Fixes a bug so that `worker reload` and `messages` commands now fail if the command errors.</li><li>Updates the help text in various languages.</li></ul>|
| 0.4.23 | 16 Sep 2019 |<ul><li>Decreases startup time for the plug-in.</li><li>Fixes a Go version issue for macOS users.</li><li>Improves debug tracing.</li><li>In `ibmcloud oc logging filter` commands, changes the `--logging-config` flag from accepting multiple values in a comma-separated list to requiring repeated flags.</li><li>Minor bug and security fixes.</li><li>Updates message, warning, and help text.</li></ul>|
| 0.4.3 | 04 Sep 2019 | Adds deprecation warnings for legacy commands to error messages that are sent to `stderr`. |
| 0.4.1 | 03 Sep 2019 |<ul><li>Sets the Red Hat OpenShift on IBM Cloud plug-in to the redesigned format by default. This redesigned version includes changes such as categorical lists instead of an alphabetical list of commands in the output of `ibmcloud oc help`, spaced-structured commands instead of hyphenated-structure commands, repeated flags instead of multiple values in comma-separated lists, and more. For a full list of the changes between version `0.3` and `0.4`, see the comparison table in [Using the beta Red Hat OpenShift on IBM Cloud plug-in](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_beta).</li><li>Adds the [`ibmcloud oc script update`](/docs/openshift?topic=openshift-kubernetes-service-cli#script_update) command to rewrite scripts that call `ibmcloud oc` commands.</li><li>Improves error handling for `ibmcloud oc cluster ls`.</li><li>Updates help text.</li></ul>|
{: caption="Overview of version changes for version 0.4 of the {{site.data.keyword.containerlong_notm}} CLI plug-in" caption-side="top"}
{: summary="Overview of version changes for version 0.4 of the {{site.data.keyword.containerlong_notm}} CLI plug-in"}

<br />


## Version 0.3
{: #03}

Review the following changes for 0.3 versions of the CLI plug-in.
{: shortdesc}

Version 0.3 of the CLI plug-in is deprecated. Ensure that your Red Hat OpenShift on IBM Cloud plug-in uses the latest `0.4` version by running `ibmcloud plugin update kubernetes-service`.
{: deprecated}

|Version|Release date|Changes|
|-------|------------|-------|
| 0.3.112 | 19 Aug 2019 |<ul><li>Adds the `--pod-subnet` and `--service-subnet` flags to the `ibmcloud oc cluster create classic` commands for standard clusters that run Kubernetes 1.15 or later. If you plan to connect your cluster to on-premises networks, you can avoid subnet conflicts by specifying a custom subnet CIDR to provide the private IP addresses for pods and subnets.</li><li>Enhances the `ibmcloud oc nlb-dns create` and `ibmcloud oc nlb-dns add` commands so that you can add more than one IP address at a time. For example, to create a DNS entry for multiple network load balancer IP addresses, use multiple flags such as `ibmcloud oc nlb-dns create --cluster mycluster --ip IP1 --ip IP2`.</li></ul> |
| 0.3.103 | 12 Aug 2019 | General refactoring and improvements. |
| 0.3.99 | 05 Aug 2019 |<ul><li>Improves error handling for `ibmcloud oc cluster config`.</li><li>Updates the help text in various languages.</li></ul> |
| 0.3.95 | 30 Jul 2019 |<ul><li>Adds the `ibmcloud oc` alias to the {{site.data.keyword.containershort_notm}} plug-in for management of Red Hat OpenShift on IBM Cloud clusters.</li><li>Adds the [`ibmcloud oc cluster subnet detach`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_cluster_subnet_detach) command to detach a public or private portable subnet in a classic IBM Cloud infrastructure account from a cluster.</li><li>Renames the `ibmcloud oc machine-types` command to `ibmcloud oc flavors`. You can still use the `machine-types` alias.</li><li>In the output of `ibmcloud oc flavors (machine-types)`, indicates flavors that are supported only for {{site.data.keyword.containerlong_notm}} or only for Red Hat OpenShift on IBM Cloud.</li><li>In the output of `ibmcloud oc cluster get`, changes the term `Owner` to `Creator` to reflect that the field returns information about the user that created the cluster.</li><li>Improves error handling for `ibmcloud oc zone add`.</li><li>Updates the help text in various languages.</li></ul> |
| 0.3.58 | 02 Jul 2019 | <ul><li>Fixes a bug so that a worker pool rebalance message is not returned when the cluster autoscaler is enabled.</li><li>Fixes a bug to support the default OpenShift cluster version.</li><li>Updates help text for the `cluster feature enable private-service-endpoint` and `nlb-dns monitor configure` commands.</li><li>Updates the help text in various languages.</li></ul> |
| 0.3.49 | 18 Jun 2019 | Updates the Go version to 1.12.6. |
| 0.3.47 | 15 Jun 2019 | <ul><li>Fixes a bug so that empty tables are not returned in the output of `ibmcloud oc kube-versions`.</li><li>Updates the NLB DNS model so that an array of NLB IP addresses is returned by `ibmcloud oc nlb-dns ls`.</li><li>Changes the description text for the {{site.data.keyword.containerlong_notm}} CLI plug-in.</li></ul> |
| 0.3.34 | 31 May 2019 | Adds support for creating Red Hat OpenShift on IBM Cloud clusters:<ul><li>Adds support for OpenShift versions in the `--version` flag of the `cluster create classic` command. For example, to create a standard OpenShift cluster, you can pass in `--version 3.11_openshift` in your `cluster create classic` command.</li><li>Adds the `versions` command to list all supported Kubernetes and OpenShift versions.</li><li>Deprecates the `kube-versions` command.</li></ul> |
| 0.3.33 | 30 May 2019 | <ul><li>Adds the `--powershell` flag to the `cluster config` command to retrieve Kubernetes environment variables in Windows PowerShell format.</li><li>Deprecates the `region get`, `region set`, and `region ls` commands. For more information, see [global endpoint functionality](/docs/openshift?topic=openshift-regions-and-zones#endpoint).</li></ul> |
| 0.3.28 | 23 May 2019 | <ul><li>Adds the [`ibmcloud oc infra-permissions get`](/docs/openshift?topic=openshift-kubernetes-service-cli#infra_permissions_get) command to check whether the credentials that allow [access to the IBM Cloud infrastructure portfolio](/docs/openshift?topic=openshift-users#api_key) for the targeted resource group and region are missing suggested or required infrastructure permissions.</li><li>Removes the `--force-update` flag from the `worker update` command.</li><li>Adds the **VLAN ID** column to the output of the `alb ls` and `alb get` commands.</li><li>Adds the **Multizone Metro** column to the output of the `supported-locations` command to designate zones that are multizone-capable.</li><li>Adds the **Master State** and **Master Health** fields to the output of the `cluster get` command. For more information, see [Master states](/docs/containers?topic=containers-health#states_master).</li><li>Updates the help text in various languages.</li></ul> |
| 0.3.8 | 30 Apr 2019 | Adds support for [global endpoint functionality](/docs/openshift?topic=openshift-regions-and-zones#endpoint) in version `0.3`. By default, you can now view and manage all of your {{site.data.keyword.containerlong_notm}} resources in all locations. You are not required to target a region to work with resources.<ul><li>Adds the [`ibmcloud oc supported-locations`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_supported-locations) command to list all locations that {{site.data.keyword.containerlong_notm}} supports.</li><li>Adds the `--location` flag to the `cluster ls` and `zone ls` commands to filter resources by one or more locations.</li><li>Adds the `--region` flag to the `credential set/unset/get`, `api-key reset`, and `vlan spanning get` commands. To run these commands, you must specify a region in the `--region` flag.</li></ul> |
{: caption="Overview of version changes for version 0.3 of the {{site.data.keyword.containerlong_notm}} CLI plug-in" caption-side="top"}
{: summary="Overview of version changes for version 0.3 of the {{site.data.keyword.containerlong_notm}} CLI plug-in"}

<br />


## Version 0.2
{: #02}

Review the following changes for 0.2 versions of the CLI plug-in.
{: shortdesc}

Version 0.2 of the CLI plug-in is deprecated. Ensure that your Red Hat OpenShift on IBM Cloud plug-in uses the latest `0.4` version by running `ibmcloud plugin update kubernetes-service`.
{: deprecated}

|Version|Release date|Changes|
|-------|------------|-------|
| 0.2.102 | 15 Apr 2019 | Adds the [`ibmcloud oc nlb-dns` group of commands](/docs/openshift?topic=openshift-kubernetes-service-cli#nlb-dns) for registering and managing a subdomain for network load balancer (NLB) IP addresses, and the [`ibmcloud oc nlb-dns monitor` group of commands](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_nlb-dns-monitor-configure) for creating and modifying health check monitors for NLB subdomains. For more information, see [Registering NLB IPs with a DNS subdomain](/docs/openshift?topic=openshift-loadbalancer_hostname#loadbalancer_hostname_dns). |
| 0.2.99 | 09 Apr 2019 | <ul><li>Updates help text.</li><li>Updates the Go version to 1.12.2.</li></ul> |
| 0.2.95 | 03 Apr 2019 | <ul><li>Adds versioning support for managed cluster add-ons.</li><ul><li>Adds the [`ibmcloud oc addon-versions`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_addon_versions) command.</li><li>Adds the `--version` flag to [`ibmcloud oc cluster addon enable`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_cluster_addon_enable) commands.</li></ul><li>Updates the help text in various languages.</li><li>Updates short links to documentation in help text.</li><li>Fixes a bug where JSON error messages printed in an incorrect format.</li><li>Fixes a bug where using the silent flag (`-s`) on some commands prevented errors from printing.</li></ul> |
| 0.2.80 | 19 Mar 2019 | <ul><li>Adds support for enabling [master-to-worker communication with service endpoints](/docs/openshift?topic=openshift-plan_clusters#workeruser-master) in standard clusters in [VRF-enabled accounts](/docs/resources?topic=direct-link-overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud).<ul><li>Adds the `--private-service-endpoint` and `--public-service-endpoint` flags to the [`ibmcloud oc cluster-create`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_cluster_create) command.</li><li>Adds the **Public Service Endpoint URL** and **Private Service Endpoint URL** fields to the output of `ibmcloud oc cluster get`.</li><li>Adds the [`ibmcloud oc cluster feature enable private-service-endpoint`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_cluster_feature_enable_private_service_endpoint) command.</li><li>Adds the [`ibmcloud oc cluster feature enable public-service-endpoint`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_cluster_feature_enable_public_service_endpoint) command.</li><li>Adds the [`ibmcloud oc cluster feature disable public-service-endpoint`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_cluster_feature_disable) command.</li></ul></li><li>Updates the help text in various languages.</li><li>Updates the Go version to 1.11.6.</li><li>Resolves intermittent networking issues for macOS users.</li></ul> |
| 0.2.75 | 14 Mar 2019 | <ul><li>Hides raw HTML from error outputs.</li><li>Fixes typos in help text.</li><li>Updates the help text in various languages.</li></ul> |
| 0.2.61 | 26 Feb 2019 | <ul><li>Adds the `cluster pull-secret apply` command, which creates an IAM service ID for the cluster, policies, API key, and image pull secrets so that containers that run in the `default` Kubernetes namespace can pull images from IBM Cloud Container Registry. For new clusters, image pull secrets that use IAM credentials are created by default. Use this command to update existing clusters or if your cluster has an image pull secret error during creation. For more information, see [the doc](/docs/openshift?topic=openshift-registry#cluster_registry_auth).</li><li>Fixes a bug where `ibmcloud oc init` failures caused help output to be printed.</li></ul> |
| 0.2.53 | 19 Feb 2019 | <ul><li>Fixes a bug where the region was ignored for `ibmcloud oc api-key reset`, `ibmcloud oc credential get/set`, and `ibmcloud oc vlan spanning get`.</li><li>Improves performance for `ibmcloud oc worker update`.</li><li>Adds the version of the add-on in `ibmcloud oc cluster addon enable` prompts.</li></ul> |
| 0.2.44 | 08 Feb 2019 | <ul><li>Adds `--skip-rbac` option to the `ibmcloud oc cluster config` command to skip adding user Kubernetes RBAC roles based on the {{site.data.keyword.cloud_notm}} IAM service access roles to the cluster configuration. Include this option only if you [manage your own Kubernetes RBAC roles](/docs/openshift?topic=openshift-users#rbac). If you use [{{site.data.keyword.cloud_notm}} IAM service access roles](/docs/openshift?topic=openshift-access_reference#service) to manage all your RBAC users, do not include this option.</li><li>Updates the Go version to 1.11.5.</li></ul> |
| 0.2.40 | 06 Feb 2019 | <ul><li>Adds the [`ibmcloud oc cluster addon ls`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_cluster_addons), [`ibmcloud oc cluster addon enable`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_cluster_addon_enable), and [`ibmcloud oc cluster addon disable`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_cluster_addon_disable) commands for working with managed cluster add-ons such as the [Istio](/docs/containers?topic=containers-istio) and [Knative](/docs/containers?topic=containers-serverless-apps-knative) managed add-ons for {{site.data.keyword.containerlong_notm}}.</li><li>Improves help text for {{site.data.keyword.Bluemix_dedicated_notm}} users of the `ibmcloud oc vlan ls` command.</li></ul> |
| 0.2.30 | 31 Jan 2019 | Increases the default timeout value for `ibmcloud oc cluster config` to `500s`. |
| 0.2.19 | 16 Jan 2019 | <ul><li>Adds the `IKS_BETA_VERSION` environment variable to enable the redesigned beta version of the Red Hat OpenShift on IBM Cloud plug-in CLI. To try out the redesigned version, see [Using the beta command structure](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_beta).</li><li>Increases the default timeout value for `ibmcloud oc subnets` to `60s`.</li><li>Fixes a minor bug and updates the help text in various languages.</li></ul> |
{: caption="Overview of version changes for version 0.2 of the {{site.data.keyword.containerlong_notm}} CLI plug-in" caption-side="top"}
{: summary="Overview of version changes for version 0.2 of the {{site.data.keyword.containerlong_notm}} CLI plug-in"}

<br />


## Version 0.1
{: #01}

Review the following changes for 0.1 versions of the CLI plug-in.
{: shortdesc}

Version 0.1 of the CLI plug-in is deprecated. Ensure that your Red Hat OpenShift on IBM Cloud plug-in uses the latest `0.4` version by running `ibmcloud plugin update kubernetes-service`.
{: deprecated}

|Version|Release date|Changes|
|-------|------------|-------|
| 0.1.668 | 18 Dec 2018 | <ul><li>Changes the default API endpoint from `https://containers.bluemix.net` to `https://containers.cloud.ibm.com`.</li><li>Fixes bug so that command help text and error messages display properly for various languages.</li><li>Displays command help faster.</li></ul> |
| 0.1.654 | 05 Dec 2018 | Updates the help text in various languages. |
| 0.1.638 | 15 Nov 2018 |<ul><li>Adds the [`ibmcloud oc cluster-refresh`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_apiserver_refresh) alias to the `apiserver-refresh` command.</li><li>Adds the resource group name to the output of `ibmcloud oc cluster get` and `ibmcloud oc cluster ls`.</li></ul>|
| 0.1.635 | 06 Nov 2018 | Adds commands for managing automatic updates of the Ingress ALB cluster add-on:<ul><li>[`ibmcloud oc alb autoupdate disable`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_alb_autoupdate_disable)</li><li>[`ibmcloud oc alb autoupdate enable`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_alb_autoupdate_enable)</li><li>[`ibmcloud oc alb autoupdate get`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_alb_autoupdate_get)</li><li>[`ibmcloud oc alb rollback`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_alb_rollback)</li><li>[`ibmcloud oc alb-update`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_alb_update)</li></ul> |
| 0.1.621 | 30 Oct 2018 | <ul><li>Adds the [`ibmcloud oc credential get` command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_credential_get).</li><li>Adds support for the `storage` log source to all cluster logging commands. For more information, see [Understanding cluster and app log forwarding](/docs/containers?topic=containers-health#logging).</li><li>Adds the `--network` flag to the [`ibmcloud oc cluster config` command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_cluster_config), which downloads the Calico configuration file to run all Calico commands.</li><li>Minor bug fixes and refactoring</li></ul>|
| 0.1.593 | 10 Oct 2018 | <ul><li>Adds the resource group ID to the output of `ibmcloud oc cluster get`.</li><li>When [{{site.data.keyword.keymanagementserviceshort}} is enabled](/docs/openshift?topic=openshift-encryption#keyprotect) as a key management service (KMS) provider in your cluster, adds the KMS enabled field in the output of `ibmcloud oc cluster get`.</li></ul> |
| 0.1.591 | 02 Oct 2018 | Adds support for [resource groups](/docs/openshift?topic=openshift-clusters#cluster_prepare). |
| 0.1.590 | 01 Oct 2018 | <ul><li>Adds the [`ibmcloud oc logging collect`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_log_collect) and [`ibmcloud oc logging collect-status`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_log_collect_status) commands for collecting API server logs in your cluster.</li><li>Adds the [`ibmcloud oc key-protect-enable` command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_key_protect) to enable {{site.data.keyword.keymanagementserviceshort}} as a key management service (KMS) provider in your cluster.</li><li>Adds the `--skip-master-health` flag to the [ibmcloud oc worker reboot](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_reboot) and [ibmcloud oc worker reload](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_reboot) commands to skip the master health check before initiating the reboot or reload.</li><li>Renames `Owner Email` to `Owner` in the output of `ibmcloud oc cluster get`.</li></ul> |
{: caption="Overview of version changes for version 0.1 of the {{site.data.keyword.containerlong_notm}} CLI plug-in" caption-side="top"}
{: summary="Overview of version changes for version 0.1 of the {{site.data.keyword.containerlong_notm}} CLI plug-in"}
 


