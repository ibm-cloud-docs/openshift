---

copyright: 
  years: 2014, 2022
lastupdated: "2022-02-03"

keywords: openshift, red hat, red hat openshift, oc

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}


# CLI changelog
{: #cs_cli_changelog}

In the command line, you are notified when updates to the `ibmcloud` CLI and plug-ins are available. Be sure to keep your CLI up-to-date so that you can use all available commands and flags.
{: shortdesc}


Refer to the following changelogs for a summary of changes for each version of the [{{site.data.keyword.openshiftlong_notm}} plug-in](/docs/openshift?topic=openshift-openshift-cli), which uses the `ibmcloud oc` alias.


## Version 1.0
{: #10}

Review the following changes for 1.0 versions of the CLI plug-in.
{: shortdesc}

## Version 1.0.353
{: #cli-10353}

Version 1.0.353 of the CLI was released on 3 December 2021.

:   Updates the help text in various languages.

## Version 1.0.347
{: #cli-10347}

Version 1.0.347 of the CLI was released on 15 November 2021.

:   Updates various output messages.

## Version 1.0.344
{: #cli-10344}

Version 1.0.344 of the CLI was released on 15 November 2021.

:   Includes a Go version update from `1.16.7` to `1.16.10` and other fixes.

## Version 1.0.334
{: #cli-10334}

Version 1.0.334 of the CLI was released on 26 October 2021.
{: shortdesc}

- Adds the `ibmcloud oc cluster master private-service-endpoint disable` command. You can now disable private service endpoints to remove private accessibility to your cluster master. 
- Updates the help text in various languages. 

## Version 1.0.331
{: #cli-10331}

Version 1.0.331 of the CLI was released on 12 October 2021.
{: shortdesc}

- Adds the `--policy` flag to the `ibmcloud oc master audit-webhook set` command. You can now configure the amount of information included in your cluster audits by specifying the `default` or `verbose` audit policy type.

## Version 1.0.312
{: #cli-10312}

Version 1.0.312 of the CLI was released on 9 August 2021.

- Removes the `ibmcloud oc nlb-dns monitor status` command. Checking the health of individual IP addresses, which was previously supported by the Cloudflare DNS provider, is not supported by the Akamai DNS provider. Instead, you can check the overall health of a subdomain by using the `ibmcloud oc nlb-dns monitor ls` command. For more information on the migration to Akamai for all `containers.appdomain.cloud`, `containers.mybluemix.net`, and `containers.cloud.ibm.com` domains, see the [migration announcement](https://cloud.ibm.com/notifications?selected=1621697674798){: external}.
- Removes the `ibmcloud oc cluster addon enable kube-terminal` command. The Kubernetes web terminal add-on became unsupported on 1 July 2021. Instead, use the [IBM Cloud Shell])/docs/containers?topic=containers-cs_cli_install#cloud-shell).

- Adds CLI support for the [OpenShift Data Foundation storage add-on](/docs/openshift?topic=openshift-ocs-manage-deployment).
- Makes the `ibmcloud oc cluster addon update` feature available to all users.
- Updates the help text in various languages.

## Version 1.0.300
{: #cli-10300}

Version 1.0.300 of the CLI was released on 12 July 2021.

- Updates the help text in various languages.

## Version 1.0.295
{: #cli-10295}

Version 1.0.295 of the CLI was released on 24 June 2021.

- Removes the unsupported {{site.data.keyword.openshiftlong_notm}} Ingress image version from the output of `ibmcloud oc alb version ls`.
- In all `ibmcloud oc cluster create` commands, updated the help text to indicate that you must set the `--workers` flag value to at least 2.
- Adds the following updates for add-on commands: - Adds the `ibmcloud oc cluster addon get` command to view the details of an installed add-on. 
- Adds the `ibmcloud oc cluster addon options` command to view optional installation settings for an add-on. 
- Adds the `--param` flag to specify an optional installation setting for the `ibmcloud oc cluster addon enable openshift-container-storage` command. 
- Updates the help text in various languages.

## Version 1.0.275
{: #cli-10275}

Version 1.0.275 of the CLI was released on 26 May 2021.
  
- The `--region` flag is now required for the `ibmcloud oc api-key reset`, `ibmcloud oc credential get`, and `ibmcloud oc credential set` commands. 
- Adds the `ibmcloud oc cluster addon versions` command to list the {{site.data.keyword.openshiftshort}} versions that are supported for each add-on version, and deprecates the `ibmcloud oc addon-versions` command.
- The `ibmcloud oc image-security disable` and `ibmcloud oc image-security enable` commands are now generally available. 
- The IAM token that is used for your CLI session is now refreshed 5 minutes before expiration to keep the session active. 
- Updates the help text in various languages.

## Version 1.0.258
{: #cli-10258}

Version 1.0.258 of the CLI was released on 26 April 2021.
  
- Adds the `--ip` flag to the `ibmcloud oc nlb-dns create vpc-gen2` and `ibmcloud oc nlb-dns rm vpc-gen2` commands to support DNS records for Network Load Balancers for VPC. 
- Adds the `--dns-type` flag to `ibmcloud oc nlb-dns create` commands to specify the DNS provider type for the subdomain registration. Currently, only `public` DNS is supported. 
- Adds a warning that the `--region` flag is planned to be required for the `ibmcloud oc api-key reset`, `ibmcloud oc credential get`, and `ibmcloud oc credential set` commands as of 10 May 2021. The region is already required by the API. Currently in the CLI, the region defaults to the targeted region if the `--region` flag is not used. 
- In the output of the `ibmcloud oc addon-versions` command, changes the `Min. OpenShift version` column to `Supported Openshift Range`. 
- When `--output json` is specified for the `ibmcloud oc storage attachment get` or `ibmcloud oc storage attachment ls` commands, fixes the output so that a volume table is not printed after the JSON output. 
- Fixes a `golang` vulnerability for [CVE-2020-28852](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-28852){: external}. 
- Updates the help text in various languages.

## Version 1.0.233
{: #cli-10233}

Version 1.0.233 of the CLI was released on 1 March 2021.

- Adds `satellite` as a supported provider to the output of the `ibmcloud oc cluster ls` command. 
- [Removes `beta` tags from `ibmcloud sat` commands for the generally available release of {{site.data.keyword.satellitelong_notm}}.](/docs/satellite?topic=satellite-satellite-cli-changelog).

## Version 1.0.231
{: #cli-10231}

Version 1.0.231 of the CLI was released on 25 February 2021.

- Updates the Go version to 1.15.8. 
- Updates the help text in various languages.

## Version 1.0.223
{: #cli-102238}

Version 1.0.223 of the CLI was released on 8 February 2021.

- Adds the [`ibmcloud oc worker-pool label set`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_pool_label_set) and [`ibmcloud oc worker-pool label rm`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_pool_label_rm) commands to set and remove custom Kubernetes labels for all worker nodes in a worker pool.
- [Adds several commands and command changes for managing {{site.data.keyword.openshiftshort}} clusters in {{site.data.keyword.satelliteshort}}](/docs/satellite?topic=satellite-satellite-cli-changelog).

## Version 1.0.208
{: #cli-10208}

Version 1.0.208 of the CLI was released on 18 December 2020.

- Updates the help text in various languages.

## Version 1.0.206
{: #cli-10206}

Version 1.0.206 of the CLI was released on 10 December 2020.

- Adds the `ibmcloud oc ingress lb get`, `ibmcloud oc ingress lb proxy-protocol disable`, and `ibmcloud oc ingress lb proxy-protocol disable` [beta commands](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_ingress_lb_proxy-protocol_enable) to manage the configuration of load balancers that expose Ingress ALBs in your cluster. For example, you can enable the NGINX PROXY protocol so that client connection information is passed in request headers to ALBs. 
- Adds the optional `--endpoint` flag to the `ibmcloud oc cluster config` command to specify a type of endpoint for the cluster context, such as the cluster's private cloud service endpoint. 
- Updates the help text in various languages. 
- Updates the Go version to 1.15.6.

## Version 1.0.197
{: #cli-10197}

Version 1.0.197 of the CLI was released on 18 November 2020.

- Adds a warning message to the `ibmcloud oc cluster config` command about temporary `oc` command failures due to RBAC synchronization. 
- Ensures that incident IDs are returned with 500-level messages. 
- In `ibmcloud oc cluster storage` commands, the cluster name is now accepted in the `--cluster` flag in addition to the cluster ID. 
- Updates the output of the `ibmcloud oc ingress alb migrate` command to be more readable. 
- Updates the help text in various languages.

## Version 1.0.178
{: #cli-10178}

Version 1.0.178 of the CLI was released on 6 October 2020.

- Updates the Go version to 1.15.2.
- Updates the help text in various languages.

## Version 1.0.171
{: #cli-10171}

Version 1.0.171 of the CLI was released on 24 September 2020.

- Shifts all existing `ibmcloud oc cluster feature` commands into the [`ibmcloud oc cluster master`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_cluster_master_pse_enable) subcategory. 
- Adds the cluster `Status`, the `Pod Subnet`, and the `Service Subnet` fields to the output of the `ibmcloud oc cluster get` command. 
- Updates the help text in various languages.

## Version 1.0.157
{: #cli-10157}

Version 1.0.157 of the CLI was released on 24 August 2020.

**Added commands**: The following commands are added. 
- Adds the [`ibmcloud oc cluster ca create`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_cluster_ca_create), [`ibmcloud oc cluster ca rotate`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_cluster_ca_rotate), and [`ibmcloud oc cluster ca status`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_cluster_ca_status) commands to manage the rotation of certificate authority (CA) certificates for your cluster components. 
- Adds the [`ibmcloud oc ingress secret`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_ingress_secret_create) set of beta commands to manage Ingress secrets in your cluster, such as creating secrets for TLS certificates that are stored in {{site.data.keyword.cloudcerts_long_notm}}. 
- Adds the [`ibmcloud oc ingress alb migrate`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_alb_migrate_start) set of beta commands to migrate resources that are formatted for ALBs that run the {{site.data.keyword.openshiftlong_notm}} Ingress image to resources that are formatted for ALBs that run the Kubernetes Ingress image. 
- Adds the [`ibmcloud oc ingress alb enable`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_alb_configure) and [`ibmcloud oc ingress alb disable`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_alb_disable) commands. 
- Adds the optional `--version` flag to the `ibmcloud oc ingress alb create` command to specify the {{site.data.keyword.openshiftlong_notm}} Ingress image version or Kubernetes Ingress image version for the ALB.

**Renamed commands**: The following commands are shifted to new naming categories. 
- Shifts all existing `ibmcloud oc alb` commands into the [`ibmcloud oc ingress alb`](/docs/openshift?topic=openshift-kubernetes-service-cli#alb-commands) subcategory. 
- Changes the names of the following flags in the relevant `ibmcloud oc ingress alb` commands: `--alb-id` to `--alb`, `--secret-name` to `--name`, and `--user-ip` to `--ip`.

**Deprecated commands**: The following commands are deprecated in favor of the new commands. 
- Deprecates the `ibmcloud oc alb cert` set of commands. 
- Deprecates the `ibmcloud oc alb configure` command. 
- Removes the deprecated `ibmcloud oc alb rollback` command,

## Version 1.0.143
{: #cli-10143}

Version 1.0.143 of the CLI was released on 6 August 2020.

- Adds the [`ibmcloud oc quota ls`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_quota_ls) command to list all quota and limits for cluster-related resources in your {{site.data.keyword.cloud_notm}} account. 
- Deprecates the `--json` flag. To print a command output in JSON format, use the `--output json` flag instead. 
- Deprecates the `-s` flag. To not show the message of the day or update reminders in command output, use the `-q` flag instead. 
- Updates `ibmcloud oc cluster ls` command so that if you include the `--ouput json` flag but don't include the `--provider` flag, only classic clusters are returned. 
- Corrects the example master update command that is displayed in the output of the `ibmcloud oc cluster get` command when a master update is available. 
- Adds information about the effects of worker node replacement in the warning message for the `ibmcloud oc worker replace` command. 
- Standardizes the help text for flags that have a list of supported values. 
- Updates the help text in various languages.

## Version 1.0.118
{: #cli-10118}

Version 1.0.118 of the CLI was released on 7 July 2020.

- Deprecates the `ibmcloud oc cluster user-subnet add`, `ibmcloud oc cluster user-subnet rm`, and `ibmcloud oc va` commands.
- Updates the Go version to 1.13.12 for [CVE-2020-7919](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-7919){: external}. 
- Fixes a bug for downloading the Calico configuration by using the `--network` flag in the `ibmcloud oc cluster config` command. 
- Updates the help text for the `--endpoint` flag of the `ibmcloud oc kms enable` command. 
- Updates the help text in various languages.

## Version 1.0.99
{: #cli-1099}

Version 1.0.99 of the CLI was released on 15 June 2020.


- Adds the `--cos-instance` flag to the `ibmcloud oc cluster create vpc-gen2` command to back up the images from your {{site.data.keyword.openshiftshort}} internal registry to a bucket in your {{site.data.keyword.cos_full_notm}} instance.
- Updates the help text in various places.

## Version 1.0.94
{: #cli-1094}

Version 1.0.94 of the CLI was released on 9 June 2020.

- Adds the [`ibmcloud oc cluster addon enable static-route`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_cluster_addon_enable_static-route) and [`ibmcloud oc cluster addon disable static-route`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_cluster_addon_disable_static-route) commands to manage the Static Route add-on for your cluster. 
- Adds the [`ibmcloud oc worker-pool taint set`](/docs/openshift?topic=openshift-kubernetes-service-cli#worker_pool_taint_set) and [`ibmcloud oc worker-pool taint rm`](/docs/openshift?topic=openshift-kubernetes-service-cli#worker_pool_taint_rm) commands to set and remove Kubernetes taints on worker nodes in a worker pool. 
- Beta: Adds the [`ibmcloud oc storage`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_storage) set of commands to view and modify storage resources in your cluster. 
- Moves the `ibmcloud oc locations` command to the `Informational Commands` group in the help output of `ibmcloud oc`. 
- Updates the help text for options in the `ibmcloud oc nlb-dns monitor configure` command. 
- Updates the help text in various languages.

## Version 1.0.84
{: #cli-1084}

Version 1.0.84 of the CLI was released on 26 May 2020.

- Fixes bugs for credentials in Kubernetes configuration contexts: 
    - When you download the contexts for clusters that run Kubernetes version 1.17 or later, those contexts are merged into your `kubeconfig` file. The tokens from the version 1.17 or later contexts now don't overwrite tokens for any version 1.16 or later contexts. 
    - Credentials are now correctly added to your `kubeconfig` file when you download the context for a cluster. 
    - Fixes credential issues for CLI plug-in installations on macOS that don't use `cgo`. 
- Adds commands for creating and managing VPC clusters.
    - [`alb configure vpc-gen2`](/docs/containers?topic=containers-kubernetes-service-cli#cli_alb_configure_vpc_gen2)
    - [`alb create vpc-gen2`](/docs/containers?topic=containers-kubernetes-service-cli#cli_alb-create-vpc-gen2)
    - [`cluster create vpc-gen2`](/docs/openshift?topic=openshift-kubernetes-service-cli#cli_cluster-create-vpc-gen2)
    - [`nlb-dns create vpc-gen2`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_nlb-dns-create-vpc-gen2)
    - [`nlb-dns rm vpc-gen2`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_nlb-dns-rm-vpc-gen2)
    - [`worker-pool create vpc-gen2`](/docs/openshift?topic=openshift-kubernetes-service-cli#cli_worker_pool_create_vpc_gen2)
    - [`zone add vpc-gen2`](/docs/openshift?topic=openshift-kubernetes-service-cli#cli_zone-add-vpc-gen2)
- Adds the **Ingress Status** and **Ingress Message** fields to the output of the `ibmcloud oc cluster get` command. For more information about these fields, see [Checking the status of Ingress components](/docs/containers?topic=containers-ingress-status).
- Adds the ALB ID to the output of the `ibmcloud oc alb create` command. 
- Adds the supported `Auth version` to the output of the `ibmcloud oc alb versions` command. 
- Adds the supported range of Kubernetes versions that your cluster must run to the output of the `ibmcloud oc addon versions` command. 
- Updates the help text in various languages.

## Version 1.0.57
{: #cli-1057}

Version 1.0.57 of the CLI was released on 7 May 2020.

- Adds a check for deprecated positional arguments. 
- Updates the macOS DNS resolver to fix network issues when you use the CLI plug-in with a VPN connection. 
- Help documentation updates: 
    - Adds instructions for enabling or disabling an add-on to the help text for the `ibmcloud oc addon-versions` command. 
    - Clarifies optional and required flags in flag help text. 
    - Updates the help text in various languages.

## Version 1.0.28
{: #cli-1028}

Version 1.0.28 of the CLI was released on 6 April 2020.

- Adds the optional `--alb-id` flag to `ibmcloud oc alb update` so that you can specify IDs of individual ALBs to update. 
- Adds the optional `--show-storage` flag to `ibmcloud oc flavors` to show additional raw disks that are available for [SDS worker node flavors](/docs/openshift?topic=openshift-planning_worker_nodes#sds). 
- Adds a message to the output of `ibmcloud oc pull-secret apply` about the amount of time it takes for the pull secrets to be applied to your cluster.

## Version 1.0.15
{: #cli-1015}

Version 1.0.15 of the CLI was released on 24 March 2020.

- Adds the [`ibmcloud oc nlb-dns secret regenerate`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_nlb-dns-secret-regenerate) and [`ibmcloud oc nlb-dns secret rm`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_nlb-dns-secret-rm) commands to help you manage secrets for NLB subdomains. 
- Adds the optional `--worker-pool WORKER_POOL` flag to `ibmcloud oc zone rm`. 
- Deprecates the option to specify a YAML file in the `--file` flag of the `ibmcloud oc cluster create` and `ibmcloud oc worker add` commands. Instead, specify values for your cluster in the supported flags for these commands. 
- Fixes the following bugs: 
    - For `ibmcloud oc cluster rm`, the `--force-delete-storage` flag no longer sets the `-f` flag.
- Updates the help text in various languages.

## Version 1.0.0
{: #cli-100}

Version 1.0.0 of the CLI was released on 26 March 2020.

- Introduces permanent behavior and syntax changes that are not compatible with earlier versions. For a summary of the changes in version 1.0, see [Using version 1.0 of the plug-in](#changelog_beta).


## Deprecated versions
{: #deprecated}

All versions of the CLI plug-in that are earlier than version 1.0 are no longer supported. You can review the archive of the changelogs. To update to the latest version, see [Updating to version 1.0 of the plug-in](#changelog_beta).
{: shortdesc}

### Updating to version 1.0 of the plug-in
{: #changelog_beta}

Version 1.0 of the CLI plug-in was released on 16 March 2020. This version contains permanent syntax and behavior changes that are not compatible with earlier versions.

To maintain all CLI functionality, update and test any automation before you update to 1.0 by checking out the [`ibmcloud oc script update` command](/docs/openshift?topic=openshift-kubernetes-service-cli#script_update) and setting your `IKS_BETA_VERSION` environment variable to `1.0`. After you update your scripts, update your CLI to version `1.0` of the plug-in.
{: important}

Check out the following syntax and behavior changes between each version of the CLI plug-in:

|Functionality|`0.2`|`0.3`|`0.4`|`1.0`|
|-------------|-----|-----|-----|-----|
| Supported? | Deprecated | Deprecated | Deprecated | Default |
| `ibmcloud oc help` output structure  \n -  Legacy: Alphabetical list of commands  \n -  Latest: Categories of commands | Legacy | Legacy | Latest | Latest |
| Command structure  \n -  Legacy: Hyphenated structure (`ibmcloud oc cluster-get`)  \n -  Latest: Spaced structure (`ibmcloud oc cluster get`) | Legacy and latest | Legacy and latest | Legacy and latest | Latest |
| Positional arguments  \n -  Legacy: Arguments specified by position (`cluster-get mycluster`)  \n -  Latest: Arguments specified by flags (`cluster get --cluster mycluster`) | Legacy and latest | Legacy and latest | Legacy and latest | Latest |
| Repeated arguments  \n -  Legacy: Comma-delineated values (`--worker-pools pool1,pool2,pool3 ...`)  \n -  Latest: Repeated flags for each value with optional shorthand flag aliases (`-p pool1 -p pool2 ...`) | Legacy | Legacy | Legacy and latest | Latest |
| Flag format  \n -  Legacy: Camel-case (`--showResources`)  \n -  Latest: Dashed (`--show-resources`) | Legacy | Legacy | Legacy and latest | Latest |
| Cluster context provided by `ibmcloud oc cluster-config`  \n -  Legacy: Provides a command that you must copy and paste to set the new `kubeconfig` file as your current `KUBECONFIG` environment variable. You must set your environment variable before you can interact with your cluster.  \n -  Latest: Appends the new `kubeconfig` file to your existing `kubeconfig` file in `~/.kube/config` or the [last file that is set by the `KUBECONFIG` environment variable](/docs/containers?topic=containers-cs_cli_install#cli_temp_kubeconfig). After you run `ibmcloud oc cluster config`, you can interact with your cluster immediately, and quickly [change the context to other clusters in the Kubernetes context](/docs/containers?topic=containers-cs_cli_install#cli_config_multiple). | Legacy | Legacy | Legacy | Latest |
{: caption="Latest versions of the redesigned {{site.data.keyword.openshiftlong_notm}} plug-in" caption-side="top"}

### Version 0.4
{: #04}

Review the following changes for 0.4 versions of the CLI plug-in.
{: shortdesc}

Version 0.4 of the CLI plug-in is deprecated. To update to the latest version, see [Updating to version 1.0 of the plug-in](#changelog_beta).
{: deprecated}

#### Version 0.4.102
{: #cli-04102}

Version 0.4.102 of the CLI was released on 4 March 2020.

- Version 3.11 clusters only: Adds the [`ibmcloud oc alb create classic`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_alb_create) command so that you can create and enable new public or private ALBs in a zone. 
- Removes the beta tag from `ibmcloud oc kms` commands. 
- Adds `--public-endpoint` as an optional flag to the `ibmcloud oc kms enable` command. Include this flag only if you want to use the KMS public cloud service endpoint instead of the private cloud service endpoint. 
- Fixes a bug so that the new `--version` flag is accepted in `ibmcloud oc cluster create` commands. 
- Help documentation updates: 
    - Fixes incorrect deprecation warnings for commands that are correctly formatted with version 1.0 syntax. 
    - Removes incorrect `ibmcloud ks cs` syntax from command deprecation warnings.
    - Updates the help text in various languages.

#### Version 0.4.90
{: #cli-0490}

Version 0.4.90 of the CLI was released on 19 February 2020.

- Updates the Go version to 1.13.5 and removes `xgo`. 
- **Command updates**: 
    - Adds the `--provider` flag to the [`ibmcloud oc flavors`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_machine_types) command. 
    - Accepts newer flag names like `--flavor` instead of `--machine-type` across various commands.
    - Deprecates the `--disable-deployment` flag of the `ibmcloud oc alb configure vpc-classic` command. 
- **VPC-specific command updates**: 
    - Fixes the [`ibmcloud oc zone rm`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_zone_rm) command for VPC multizone clusters. 
    - For the [`ibmcloud oc vpcs`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_vpcs) command, defaults to list only generation 1 (`vpc-classic`) VPCs. 
    - Revises the `ibmcloud oc worker-pool create vpc-classic` command to remove the `--disable-disk-encrypt` flag and to hide the `--hardware` flag because it only accepts one value. 
- **Help documentation updates**: 
    - Add deprecation warnings to encourage you to use the newer `classic` subcommands. For example, use `ibmcloud oc cluster create classic` instead of `ibmcloud oc cluster create`.
    - Adds links to the {{site.data.keyword.openshiftlong_notm}} documentation in various help topics.
    - Standardizes formatting in help text, such as adding single quotes around variable names or styling for URLs. 
    - Updates the help text in various languages.|

#### Version 0.4.66
{: #cli-0466}

Version 0.4.66 of the CLI was released on 19 December 2019.

- Adds a **Status** field to the `ibmcloud oc alb cert get` command. The previous **Status** field is now called **State**. 
- Fixes a bug so that help text is now properly displayed for top-level commands, such as `ibmcloud oc flavors` and `ibmcloud oc subnets`.

#### Version 0.4.64
{: #cli-0464}

Version 0.4.64 of the CLI was released on 11 December 2019.


- Adds the `--entitlement` flag to the `ibmcloud oc cluster create` and `ibmcloud oc worker-pool create` commands. Include this flag only if you use this cluster with an [IBM Cloud Pak](/docs/openshift?topic=openshift-openshift_cloud_paks) that has an {{site.data.keyword.openshiftshort}} entitlement.
- Updates the Go version to 1.12.11. 
- Updates the help text in various languages.
  
#### Version 0.4.61
{: #cli-0461}

Version 0.4.61 of the CLI was released on 26 November 2019.

- Removes the `kube-audit` log source option from `ibmcloud oc logging config` commands.
- Adds a column to the output of `ibmcloud oc addon-versions` for the minimum required {{site.data.keyword.openshiftshort}} version.
- Adds a check to verify that you are logged in to the {{site.data.keyword.cloud_notm}} CLI before a command request is issued. 
- Updates the help text in various languages.
  
#### Version 0.4.51
{: #cli-0451}

Version 0.4.51 of the CLI was released on 7 November 2019.

- Adds the [`ibmcloud oc kms crk ls`](/docs/openshift?topic=openshift-kubernetes-service-cli#ks_kms_crk_ls), [`ibmcloud oc kms enable`](/docs/openshift?topic=openshift-kubernetes-service-cli#ks_kms_enable), and [`ibmcloud oc kms instance ls`](/docs/openshift?topic=openshift-kubernetes-service-cli#ks_kms_instance_ls) commands to create and manage key management service (KMS) providers in a cluster. 
- Adds the optional `--skip-advance-permissions-check` flag to `ibmcloud oc cluster create` and `ibmcloud oc cluster rm`. 
- Changes the `--vpc-id` flag to be optional for `ibmcloud oc worker-pool create vpc-classic`. 
- Fixes the error message for when no cluster name or ID is specified for `ibmcloud oc worker get` or `ibmcloud oc worker-pool get`. 
- Adds `public` and `private` as supported values for the `--hardware` flag of `ibmcloud oc worker-pool create classic`. 
- When the `--admin` flag is included in `ibmcloud oc cluster config`, removes `-admin` from the cluster name in the `KUBECONFIG` file path. 
- Updates all command help to use the new space-separated syntax.

#### Version 0.4.42
{: #cli-0442}

Version 0.4.42 of the CLI was released on 24 October 2019.

- Adds the cluster ID to the output of `ibmcloud oc cluster create`. 
- Updates the Go version to 1.12.10 to fix `golang` vulnerabilities for [CVE-2019-16276](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-16276){: external}.

#### Version 0.4.38
{: #cli-0438}

Version 0.4.38 of the CLI was released on 14 October 2019.


- Adds the `--secret-namespace` flag to the `ibmcloud oc nlb-dns create classic` and `ibmcloud oc nlb-dns create vpc-classic` commands to specify the Kubernetes namespace that you want the SSL secret for the DNS subdomain to be created in. 
- Updates status information of worker nodes for VPC clusters. 
- Updates the help text in various languages.

#### Version 0.4.31
{: #cli-0431}

Version 0.4.31 of the CLI was released on 24 September 2019.


- Removes the deprecated `region get`, `region set`, and `region ls` commands from help output. 
- Updates command structure to the new spaced format in help output. 
- Adds a warning to the output of legacy `cluster config` behavior. For more information, see the [version 1.0 plug-in documentation](/docs/openshift?topic=openshift-cs_cli_changelog#changelog_beta). 
- Fixes a bug so that `worker reload` and `messages` commands now fail if the command errors. 
- Updates the help text in various languages.

#### Version 0.4.23
{: #cli-0423}

Version 0.4.23 of the CLI was released on 16 September 2019.

- Decreases startup time for the plug-in. 
- Fixes a Go version issue for macOS users. 
- Improves debug tracing. 
- In `ibmcloud oc logging filter` commands, the syntax of the `--logging-config` flag changes from accepting multiple values in a comma-separated list to requiring repeated flags. 
- Minor bug and security fixes. 
- Updates message, warning, and help text.

#### Version 0.4.3
{: #cli-043}

Version 0.4.3 of the CLI was released on 4 September 2019.

- Adds deprecation warnings for legacy commands to error messages that are sent to `stderr`.

#### Version 0.4.1
{: #cli-041}

Version 0.4.1 of the CLI was released on 3 April 2019.

- Sets the {{site.data.keyword.openshiftlong_notm}} plug-in to the redesigned format by default. This redesigned version includes changes such as categorical lists instead of an alphabetical list of commands in the output of `ibmcloud oc help`, spaced-structured commands instead of hyphenated-structure commands, repeated flags instead of multiple values in comma-separated lists, and more. For a full list of the changes between version `0.3` and `0.4`, see the comparison table in [Using the beta {{site.data.keyword.openshiftlong_notm}} plug-in](/docs/openshift?topic=openshift-cs_cli_changelog#changelog_beta). 
- Adds the [`ibmcloud oc script update`](/docs/openshift?topic=openshift-kubernetes-service-cli#script_update) command to rewrite scripts that call `ibmcloud oc` commands. 
- Improves error handling for `ibmcloud oc cluster ls`. 
- Updates help text.



### Version 0.3
{: #03}

Review the following changes for 0.3 versions of the CLI plug-in.
{: shortdesc}

Version 0.3 of the CLI plug-in is deprecated. To update to the latest version, see [Updating to version 1.0 of the plug-in](#changelog_beta).
{: deprecated}

#### Version 0.3.112
{: #cli-03112}

Version 0.3.112 of the CLI was released on 19 August 2019.

- With the release of the [{{site.data.keyword.containerlong_notm}} version 2 API](/docs/openshift?topic=openshift-cs_api_install#api_about), the {{site.data.keyword.cloud_notm}} CLI `kubernetes-service` plug-in supports both classic and VPC infrastructure providers. Some `ibmcloud oc` commands support only one type of infrastructure, whereas other commands include additional names or options. 
- Adds the `--pod-subnet` and `--service-subnet` flags to the `ibmcloud oc cluster create classic` commands for standard clusters that run Kubernetes 1.15 or later. If you plan to connect your cluster to on-premises networks, you can avoid subnet conflicts by specifying a custom subnet CIDR that provides the private IP addresses for your pods and subnets. 
- Enhances the `ibmcloud oc nlb-dns create` and `ibmcloud oc nlb-dns add` commands so that you can add more than one IP address at a time. For example, to create a DNS entry for multiple network load balancer IP addresses, use multiple flags such as `ibmcloud oc nlb-dns create --cluster mycluster --ip IP1 --ip IP2`.

#### Version 0.3.103
{: #cli-03103}

Version 0.3.103 of the CLI was released on 12 August 2019.

- General refactoring and improvements.

#### Version 0.3.99
{: #cli-0399}

Version 0.3.99 of the CLI was released on 5 August 2019.

- Improves error handling for `ibmcloud oc cluster config`. 
- Updates the help text in various languages.

#### Version 0.3.95
{: #cli-0395}

Version 0.3.95 of the CLI was released on 30 July 2019.


- Adds the `ibmcloud oc` alias to the {{site.data.keyword.containershort_notm}} plug-in for management of {{site.data.keyword.openshiftlong_notm}} clusters.
- Adds the [`ibmcloud oc cluster subnet detach`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_cluster_subnet_detach) command to detach a public or private portable subnet in a classic IBM Cloud infrastructure account from a cluster. 
- Renames the `ibmcloud oc machine-types` command to `ibmcloud oc flavors`. You can still use the `machine-types` alias. 
- In the output of `ibmcloud oc flavors (machine-types)`, indicates flavors that are supported only for {{site.data.keyword.containerlong_notm}} or only for {{site.data.keyword.openshiftlong_notm}}. 
- In the output of `ibmcloud oc cluster get`, changes the term `Owner` to `Creator` to reflect that the field returns information about the user that created the cluster. 
- Improves error handling for `ibmcloud oc zone add`. 
- Updates the help text in various languages.

#### Version 0.3.58
{: #cli-0358}

Version 0.3.58 of the CLI was released on 2 July 2019.

- Fixes a bug so that a worker pool rebalance message is not returned when the cluster autoscaler is enabled.
- Fixes a bug to support the default OpenShift cluster version.
- Updates help text for the `cluster master private-service-endpoint enable` and `nlb-dns monitor configure` commands. 
- Updates the help text in various languages.
  
#### Version 0.3.49
{: #cli-0349}

Version 0.3.49 of the CLI was released on 18 June 2019.

- Updates the Go version to 1.12.6.

#### Version 0.3.47
{: #cli-0347}

Version 0.3.47 of the CLI was released on 15 June 2019.

- Fixes a bug so that empty tables are not returned in the output of `ibmcloud oc kube-versions`. 
- Updates the NLB DNS model so that an array of NLB IP addresses is returned by `ibmcloud oc nlb-dns ls`. 
- Changes the description text for the {{site.data.keyword.containerlong_notm}} CLI plug-in.

#### Version 0.3.34
{: #cli-0334}

Version 0.3.34 of the CLI was released on 31 May 2019.

Adds support for creating {{site.data.keyword.openshiftlong_notm}} clusters:
- Adds support for {{site.data.keyword.openshiftshort}} versions in the `--version` flag of the `cluster create classic` command. For example, to create a standard {{site.data.keyword.openshiftshort}} cluster, you can pass in `--version 3.11_openshift` in your `cluster create classic` command.
- Adds the `versions` command to list all supported Kubernetes and {{site.data.keyword.openshiftshort}} versions. 
- Deprecates the `kube-versions` command.

#### Version 0.3.33
{: #cli-0333}

Version 0.3.33 of the CLI was released on 30 May 2019.

- Adds the `--powershell` flag to the `cluster config` command to retrieve Kubernetes environment variables in Windows PowerShell format. 
- Deprecates the `region get`, `region set`, and `region ls` commands. For more information, see [global endpoint functionality](/docs/openshift?topic=openshift-regions-and-zones#endpoint).

#### Version 0.3.28
{: #cli-0328}

Version 0.3.28 of the CLI was released on 23 May 2019.

- Adds the [`ibmcloud oc infra-permissions get`](/docs/openshift?topic=openshift-kubernetes-service-cli#infra_permissions_get) command to check whether the credentials that allow [access to the IBM Cloud infrastructure portfolio](/docs/containers?topic=containers-access-creds) for the targeted resource group and region are missing suggested or required infrastructure permissions.
- Removes the `--force-update` flag from the `worker update` command. 
- Adds the **VLAN ID** column to the output of the `alb ls` and `alb get` commands. 
- Adds the **Multizone Metro** column to the output of the `locations` command to designate zones that are multizone-capable. 
- Adds the **Master State** and **Master Health** fields to the output of the `cluster get` command. For more information, see [Master states](/docs/containers?topic=containers-health-monitor#states_master). 
- Updates the help text in various languages.

#### Version 0.3.8
{: #cli-038}

Version 0.3.8 of the CLI was released on 30 April 2019.

- Adds support for [global endpoint functionality](/docs/openshift?topic=openshift-regions-and-zones#endpoint) in version `0.3`. By default, you can now view and manage all your {{site.data.keyword.containerlong_notm}} resources in all locations. You are not required to target a region to work with resources. 
- Adds the [`ibmcloud oc locations`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_supported-locations) command to list all locations that {{site.data.keyword.containerlong_notm}} supports. 
- Adds the `--location` flag to the `cluster ls` and `zone ls` commands to filter resources by one or more locations. - Adds the `--region` flag to the `credential set/unset/get`, `api-key reset`, and `vlan spanning get` commands. To run these commands, you must specify a region in the `--region` flag.


### Version 0.2
{: #02}

Review the following changes for 0.2 versions of the CLI plug-in.
{: shortdesc}

Version 0.2 of the CLI plug-in is deprecated. To update to the latest version, see [Updating to version 1.0 of the plug-in](#changelog_beta).
{: deprecated}

#### Version 0.2.102
{: #cli-02102}

Version 0.2.102 of the CLI was released on 15 April 2019.

- Adds the [`ibmcloud oc nlb-dns` group of commands](/docs/openshift?topic=openshift-kubernetes-service-cli#nlb-dns) for registering and managing a subdomain for network load balancer (NLB) IP addresses, and the [`ibmcloud oc nlb-dns monitor` group of commands](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_nlb-dns-monitor-configure) for creating and modifying health check monitors for NLB subdomains. For more information, see [Registering NLB IPs with a DNS subdomain](/docs/openshift?topic=openshift-loadbalancer_hostname#loadbalancer_hostname_dns).

#### Version 0.2.99
{: #cli-0299}

Version 0.2.99 of the CLI was released on 9 April 2019.

- Updates help text. 
- Updates the Go version to 1.12.2.

#### Version 0.2.95
{: #cli-02}

Version 0.2.95 of the CLI was released on 3 April 2019.

- Adds versioning support for managed cluster add-ons.
- Adds the [`ibmcloud oc addon-versions`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_addon_versions) command. 
- Adds the `--version` flag to [`ibmcloud oc cluster addon enable`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_cluster_addon_enable) commands.
- Updates the help text in various languages. 
- Updates short links to documentation in help text. 
- Fixes a bug where JSON error messages printed in an incorrect format. 
- Fixes a bug where using the silent flag (`-s`) on some commands prevented errors from printing.
  
#### Version 0.2.80
{: #cli-0280}

Version 0.2.80 of the CLI was released on 19 March 2019.

- Adds support for enabling [master-to-worker communication with service endpoints](/docs/openshift?topic=openshift-plan_clusters#workeruser-master) in standard clusters in [VRF-enabled accounts](/docs/account?topic=account-vrf-service-endpoint#vrf). 
- Adds the `--private-service-endpoint` and `--public-service-endpoint` flags to the [`ibmcloud oc cluster-create`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_cluster_create) command. 
- Adds the **Public Service Endpoint URL** and **Private Service Endpoint URL** fields to the output of `ibmcloud oc cluster get`. 
- Adds the [`ibmcloud oc cluster master private-service-endpoint enable`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_cluster_master_pse_enable) command. 
- Adds the [`ibmcloud oc cluster master public-service-endpoint enable`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_cluster_master_pub_se_enable) command.
- Updates the help text in various languages. 
- Updates the Go version to 1.11.6. 
- Resolves intermittent networking issues for macOS users.

#### Version 0.2.75
{: #cli-0275}

Version 0.2.75 of the CLI was released on 14 March 2019.

- Hides raw HTML from error outputs. 
- Fixes typos in help text. 
- Updates the help text in various languages.

#### Version 0.2.61
{: #cli-0261}

Version 0.2.61 of the CLI was released on 26 February 2019.

- Adds the `cluster pull-secret apply` command, which creates an IAM service ID for the cluster, policies, API key, and image pull secrets so that containers that run in the `default` Kubernetes namespace can pull images from IBM Cloud Container Registry. For new clusters, image pull secrets that use IAM credentials are created by default. Use this command to update existing clusters or if your cluster has an image pull secret error during creation. For more information, see [the doc](/docs/openshift?topic=openshift-registry#cluster_registry_auth). 
- Fixes a bug where `ibmcloud oc init` failures caused help output to be printed.

#### Version 0.2.53
{: #cli-0253}

Version 0.2.53 of the CLI was released on 19 February 2019.

- Fixes a bug where the region was ignored for `ibmcloud oc api-key reset`, `ibmcloud oc credential get/set`, and `ibmcloud oc vlan spanning get`. 
- Improves performance for `ibmcloud oc worker update`. 
- Adds the version of the add-on in `ibmcloud oc cluster addon enable` prompts.

#### Version 0.2.44
{: #cli-0244}

Version 0.2.44 of the CLI was released on 8 February 2019.

- Adds `--skip-rbac` option to the `ibmcloud oc cluster config` command to skip adding user Kubernetes RBAC roles based on the {{site.data.keyword.cloud_notm}} IAM service access roles to the cluster configuration. Include this option only if you [manage your own Kubernetes RBAC roles](/docs/openshift?topic=openshift-users#rbac). If you use [{{site.data.keyword.cloud_notm}} IAM service access roles](/docs/openshift?topic=openshift-access_reference#service) to manage all your RBAC users, don't include this option. - Updates the Go version to 1.11.5.

#### Version 0.2.40
{: #cli-0240}

Version 0.2.40 of the CLI was released on 6 February 2019.

- Adds the [`ibmcloud oc cluster addon ls`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_cluster_addons), [`ibmcloud oc cluster addon enable`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_cluster_addon_enable), and [`ibmcloud oc cluster addon disable`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_cluster_addon_disable) commands for working with managed cluster add-ons such as the [Istio](/docs/containers?topic=containers-istio) managed add-on for {{site.data.keyword.containerlong_notm}}. 
- Improves help text for {{site.data.keyword.Bluemix_dedicated_notm}} users of the `ibmcloud oc vlan ls` command.

#### Version 0.2.30
{: #cli-0230}

Version 0.2.30 of the CLI was released on 31 January 2019.

- Increases the default timeout value for `ibmcloud oc cluster config` to `500s`.

#### Version 0.2.19
{: #cli-0219}

Version 0.2.19 of the CLI was released on 16 January 2019.

- Adds the `IKS_BETA_VERSION` environment variable to enable the redesigned beta version of the {{site.data.keyword.openshiftlong_notm}} plug-in CLI. To try out the redesigned version, see [Using the beta command structure](/docs/openshift?topic=openshift-cs_cli_changelog#changelog_beta). 
- Increases the default timeout value for `ibmcloud oc subnets` to `60s`. 
- Fixes a minor bug and updates the help text in various languages.


### Version 0.1
{: #01}

Review the following changes for 0.1 versions of the CLI plug-in.
{: shortdesc}

Version 0.1 of the CLI plug-in is deprecated. To update to the latest version, see [Updating to version 1.0 of the plug-in](#changelog_beta).
{: deprecated}

#### Version 0.1.668
{: #cli-01668}

Version 0.1.68 of the CLI was released on 18  December 2018.

- Changes the default API endpoint from `containers.bluemix.net` to `containers.cloud.ibm.com`. 
- Fixes bug so that command help text and error messages display properly for various languages. 
- Displays command help faster.

#### Version 0.1.654
{: #cli-01654}

Version 0.1.654 of the CLI was released on 5  December 2018.

- Updates the help text in various languages.

#### Version 0.1.638
{: #cli-01638}

Version 0.1.638 of the CLI was released on 15 November 2018.

- Adds the [`ibmcloud oc cluster-refresh`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_apiserver_refresh) alias to the `apiserver-refresh` command. 
- Adds the resource group name to the output of `ibmcloud oc cluster get` and `ibmcloud oc cluster ls`.

#### Version 0.1.635
{: #cli-01635}

Version 0.1.635 of the CLI was released on 6 November 2018.

Adds commands for managing automatic updates of the Ingress ALB cluster add-on: 
- [`ibmcloud oc alb autoupdate disable`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_alb_autoupdate_disable)
- [`ibmcloud oc alb autoupdate enable`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_alb_autoupdate_enable)
- [`ibmcloud oc alb autoupdate get`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_alb_autoupdate_get)
- `ibmcloud oc alb rollback` 
- [`ibmcloud oc alb-update`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_alb_update)

#### Version 0.1.621
{: #cli-01621}

Version 0.1.621 of the CLI was released on 30 October 2018.


- Adds the [`ibmcloud oc credential get` command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_credential_get). 
- Adds support for the `storage` log source to all cluster logging commands. For more information, see [Understanding cluster and app log forwarding](/docs/containers?topic=containers-health#logging). 
- Adds the `--network` flag to the [`ibmcloud oc cluster config` command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_cluster_config), which downloads the Calico configuration file to run all Calico commands. 
- Minor bug fixes and refactoring.

#### Version 0.1.593
{: #cli-01593}

Version 0.1.593 of the CLI was released on 10 October 2018.

- Adds the resource group ID to the output of `ibmcloud oc cluster get`. 
- When [{{site.data.keyword.keymanagementserviceshort}} is enabled](/docs/openshift?topic=openshift-encryption#keyprotect) as a key management service (KMS) provider in your cluster, adds the KMS enabled field in the output of `ibmcloud oc cluster get`.

#### Version 0.1.591
{: #cli-01591}

Version 0.1.591 of the CLI was released on 2 October 2018.

- Adds support for [resource groups](/docs/openshift?topic=openshift-clusters#cluster_prepare).

#### Version 0.1.590
{: #cli-01590}

Version 0.1.590 of the CLI was released on 1 October 2018.


- Adds the [`ibmcloud oc key-protect-enable` command](/docs/openshift?topic=openshift-kubernetes-service-cli#ks_kms) to enable {{site.data.keyword.keymanagementserviceshort}} as a key management service (KMS) provider in your cluster. 
- Adds the `--skip-master-health` flag to the [ibmcloud oc worker reboot](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_reboot) and [ibmcloud oc worker reload](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_reboot) commands to skip the master health check before initiating the reboot or reload. 
- Renames `Owner Email` to `Owner` in the output of `ibmcloud oc cluster get`.
  
  
