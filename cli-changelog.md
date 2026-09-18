---

copyright: 
  years: 2014, 2026
lastupdated: "2026-09-18"


keywords: openshift, {{site.data.keyword.openshiftlong_notm}}, oc, ks

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}



# CLI change log
{: #cs_cli_changelog}


In the command line, you are notified when updates to the `ibmcloud` CLI and plug-ins are available. Be sure to keep your CLI up-to-date so that you can use all available commands and options.
{: shortdesc}


Refer to the following change logs for a summary of changes for each version of the [{{site.data.keyword.openshiftlong_notm}} plug-in](/docs/openshift?topic=openshift-cli-install), which uses the `ibmcloud oc` alias.
  
## Version 1.0
{: #10}

Review the following changes for 1.0 versions of the CLI plug-in.
{: shortdesc}

## Version v1.0.864
{: #cli-01864}

Version 1.0.864 of the CLI was released on 14 September 2026.
- Updates dependencies to address CVEs. No new functionality.

## Version v1.0.843
{: #cli-01843}

Version 1.0.843 of the CLI was released on 27 August 2026.
- Improves the help text descriptions for add-on, logging, and ingress commands. No new commands or flags are added.
- Fixes an issue where trailing slashes were not trimmed from API endpoint URLs.
- Updates dependencies to address CVEs.

## Version v1.0.829
{: #cli-01829}

Version 1.0.829 of the CLI was released on 19 August 2026.
- Updates dependencies to address CVEs. No new functionality.

## Version v1.0.815
{: #cli-01815}

Version 1.0.815 of the CLI was released on 03 August 2026.
- Adds Cloud Service Endpoint (CSE) support.
- Updates dependencies. No other new functionality.

## Version v1.0.804
{: #cli-01804}

Version 1.0.804 of the CLI was released on 25 July 2026.
- Updates dependencies to address CVEs. No new functionality.

## Version v1.0.796
{: #cli-01796}

Version 1.0.796 of the CLI was released on 22 July 2026.
- Adds the `--offering` and `--show-defaults` flags to the [`ibmcloud ks cluster addon versions`](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-addon-versions-cli) command.

## Version v1.0.791
{: #cli-01791}

Version 1.0.791 of the CLI was released on 09 July 2026.
- Fixes an issue where the `_openshift` suffix was not trimmed from version strings in the `Version` column of the table output when a cluster was in an updating state. For example, `4.19.32_1582_openshift --> 4.20.23_1551_openshift` now displays as `4.19.32_1582 --> 4.20.23_1551`. This fix applies to table output only; JSON output is not affected.

## Version v1.0.775
{: #cli-01775}

Version 1.0.775 of the CLI was released on 28 May 2026.
- Removes the `--header-timeout` parameter from the [`ibmcloud ks ingress lb proxy-protocol enable`](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-load-balancer-proxy-protocol-enable-cli) command.

## Version v1.0.773
{: #cli-01773}

Version 1.0.773 of the CLI was released on 23 May 2026.
- Marks deprecated `cluster master private-service-endpoint allowlist` commands as hidden in the CLI.

## Version v1.0.770
{: #cli-01770}

Version 1.0.770 of the CLI was released on 11 May 2026.
- Includes general refactoring and improvements.


## Version v1.0.768
{: #cli-01768}

Version 1.0.768 of the CLI was released on 05 May 2026.
- Promotes Virtual Network Interface (VNI) commands from experimental to generally available. The new commands include:
    - `ibmcloud ks vni attach baremetal` - Attach a VNI to a bare metal worker node or cluster
    - `ibmcloud ks vni detach` - Detach a VNI from a worker node or cluster
    - `ibmcloud ks vni ls` - List VNIs attached to a cluster or worker node
- Includes general refactoring and improvements.

## Version v1.0.765
{: #cli-01765}

Version 1.0.765 of the CLI was released on 30 April 2026.
- Simplifies VNI list query and JSON output for improved performance and clarity.
- Includes general refactoring and improvements.

## Version v1.0.763
{: #cli-01763}

Version 1.0.763 of the CLI was released on 28 April 2026.
- Updates the Headlamp add-on to beta status.
- Includes general refactoring and improvements.

## Version v1.0.762
{: #cli-01762}

Version 1.0.762 of the CLI was released on 23 April 2026.
- Adds support for the Headlamp add-on management commands:
- `ibmcloud ks cluster addon enable headlamp` - Enable the Headlamp add-on for a cluster
- `ibmcloud ks cluster addon update headlamp` - Update the Headlamp add-on
- `ibmcloud ks cluster addon disable headlamp` - Disable the Headlamp add-on
- Extends ALB version information to include Traefik Ingress controller versions and status alongside Kubernetes Ingress versions.
- Updates the `ibmcloud ks ingress alb versions` command output to display both Kubernetes and Traefik Ingress controller versions with their respective statuses.
- Refactors ALB version listing functionality for improved code organization.
- Includes general refactoring and improvements.

## Version v1.0.760
{: #cli-01760}

Version 1.0.760 of the CLI was released on 21 April 2026.
- Adds experimental `ibmcloud ks experimental vni` command group for managing Virtual Network Interfaces (VNI) on VPC clusters. The new commands include:
- `ibmcloud ks experimental vni attach` - Attach a VNI to a worker node (supports both bare metal and virtual nodes)
- `ibmcloud ks experimental vni detach` - Detach a VNI from a worker node
- `ibmcloud ks experimental vni ls` - List VNIs attached to a cluster or specific worker node
- Includes general refactoring and improvements.

## Version v1.0.759
{: #cli-01759}

Version 1.0.759 of the CLI was released on 20 April 2026.
- Enhances the `ibmcloud ks worker reload` command to support VPC bare metal worker nodes in addition to classic worker nodes.
- Updates the `ibmcloud ks worker reload` command to make the `--cluster` flag optional. The cluster is now automatically determined from the worker ID. Note: The `--cluster` flag is deprecated and will be ignored if provided.
- Extends the expiration date for experimental `trusted-profile` commands from 14 April 2026 to 14 July 2026.
- Migrates the `worker reload` command to use the GraphQL API for improved performance and support for VPC bare metal nodes.
- Updates dependencies including apigateway, service-engine, and various Go modules.
- Includes general refactoring and improvements.





## Version v1.0.756
{: #cli-01756}

Version 1.0.756 of the CLI was released on 06 April 2026.
- Adds the `ibmcloud ks ingress lb backend set` command to configure which Ingress controller (Kubernetes or Traefik) is exposed by VPC load balancers.
- Updates the help text for `ibmcloud ks worker replace --update` command to indicate that the command updates the worker node operating system when the worker pool OS has been updated.
- Extends ALB version information to include Traefik Ingress controller versions and status.
- Includes general refactoring and improvements.


## Version v1.0.753
{: #cli-01753}

Version 1.0.753 of the CLI was released on 27 March 2026.
- Adds upgrade indicator symbols to the `Status` or `State` column in the output of the `ibmcloud sat location ls`, `ibmcloud sat location get`, `ibmcloud sat hosts`, and `ibmcloud sat host get` commands. A `*` symbol indicates that one or more control plane hosts are at least one patch version behind. A `‡` symbol indicates that one or more control plane hosts are at least one major or minor version behind. For more information, see [Identifying control plane hosts that need updating](/docs/satellite?topic=satellite-host-update-location#host-update-identify-cli).


## Version v1.0.745
{: #cli-01745}

Version 1.0.745 of the CLI was released on 14 January 2026.
- Adds the `ibmcloud ks ingress security port80` command group for managing port 80 on VPC clusters.
- Extends the expiration date on several experimental commands.


## Version v1.0.732
{: #cli-01732} 

- Adds network plug-in details to the output of the `cluster get` command.
- Includes general refactoring and improvements.
- Updates the help text.

## Version v1.0.727
{: #cli-01727}

- Adds the container network interface `[--cni CNI]` option to the `ibmcloud ks cluster create vpc-gen2` command.
- Includes general refactoring and improvements.
- Updates the help text.

## Version v1.0.724
{: #cli-01724}

- Includes general refactoring and improvements.
- Updates the help text.

## Version v1.0.718
{: #cli-01078}

Extends the experimental date for the `trusted profile` commands.

## Version v1.0.717
{: #cli-010717}

Adds the `--domain-provider` option to the `ingress domain create` command. For more information, see [Setting up a domain for your cluster](https://ibm.biz/containers-ingress-domains).

## Version v1.0.715
{: #cli-010715}

Updates the output of `ibmcloud ks cluster get` to include more information about trusted profile IDs.

## Version v1.0.714
{: #cli-010714}

Version 1.0.714 of the CLI was released on 05 August 2025.
- Removes the `--allows-insecure`, `--description DESCRIPTION`, `--expected-body BODY`,  `--expected-codes CODES`, `--follows-redirects`, and `--method METHOD` options from the `ibmcloud ks nlb-dns monitor configure` command.
- Includes general refactoring and improvements.
- Updates the help text.

## Version v1.0.706
{: #cli-010706}

Version 1.0.706 of the CLI was released on 10 June 2025.
- Adds the `--show-crn` option to the `ibmcloud oc ingress secret field ls` command.
- Adds the `--delete-openshift-registry-cos-bucket` option to the `ibmcloud oc cluster rm` command for {{site.data.keyword.openshiftlong_notm}} clusters.
- Deprecates the `--description`, `--expected-body`, `--expected-codes`, `--follows-redirects`, `--header`, `--method`, and `--retries` options in the `nlb-dns monitor` configure command. For more information, see the [ibmcloud ks nlb-dns monitor configure](/docs/openshift?topic=openshift-kubernetes-service-cli#nlb-dns-monitor-configure-cli) reference.
- Includes general refactoring and improvements.

## Version v1.0.687
{: #cli-010687}

Version 1.0.687 of the CLI was released on 13 March 2025.
- Adds the `--show-crn` option to the `ibmcloud oc ingress secret ls` command.
- Adds the `--output OUTPUT` option to the `ibmcloud oc api-key reset` command.
- Includes general refactoring and improvements.

## Version v1.0.679
{: #cli-010679}

Version 1.0.679 of the CLI was released on 17 February 2025.
- Includes general refactoring and improvements.

## Version v1.0.677
{: #cli-010677}

- Adds the `--show-os` option to the `ibmcloud oc flavor ls` command. 
- Deprecates all `ibmcloud oc cluster master private-service-endpoint allowlist` commands.
- Removes the `--gateway-enabled`option from the `ibmcloud oc cluster create classic` command.

## Version v1.0.674
{: #cli-010674}

- Updates the `sat location update` command from experimental to non-experimental.

## Version v1.0.673
{: #cli-010673}

- Adds the `vpc secure-by-default` command group.
- Adds the `endpoint authn get` command for Satellite.
- Adds the `-f` force option to `worker-pool rebalance`.
- Updates the help text when referring to Key Management Service (KMS).

## Version v1.0.665
{: #cli-010665}


Version 1.0.665 of the CLI was released on 18 September 2024.
- Adds the `ibmcloud oc worker-pool operating-system set` command.
- Adds the `--physical-address` and `--capability` options to the `ibmcloud sat location create` command.
- Adds operating system information to the output of the `ibmcloud oc workers` and `ibmcloud oc worker get` commands.
- Adds Secure By Default networking and outbound traffic protection information to the output of `ibmcloud oc cluster get`.

## Version v1.0.657
{: #cli-010657}

Version 1.0.657 of the CLI was released on 10 September 2024.
- `ibmcloud sat sat connector` commands are no longer experimental. 
- Changes the output of `ibmcloud sat connector ls` to include only one page of results and adds options for pagination. 


## Version v1.0.652
{: #cli-010652}

Version 1.0.652 of the CLI was released on 23 August 2024.
- Makes the `ibmcloud sat agent` and the `ibmcloud sat endpoint authn` and `ibmcloud sat acl` commands not experimental.
- Fixes GraphQL bugs and help text improvements.
- Updates the expiration date format for `experimental` commands.
- Extends the expiration date of `connector` commands.
- Updates the `ibmcloud sat location dns register` command to no longer require exactly 3 IP addresses.
- Adds the `ibmcloud sat agent ls` command.
- Adds the `enable` and `disable` commands to the `ibmcloud sat endpoint` group.
- Updates entitlement options to use `ocp_entitled` instead of `cloud_pak`, and indicates `worker-pool` as required when it is required.
- Makes the `--worker-pool` option required for the `zone add`, `zone rm`, and `zone network-set` commands.

## Version v1.0.640
{: #cli-010640}

Version 1.0.640 of the CLI was released on 17 July 2024.
- Changes the `--entitlement cloud_pak` option in the `cluster create` command to be `--entitlement ocp_entitled` to allow for other entitlements besides Cloud Paks.
- Adds the `--worker-pool POOL` option to the `ibmcloud oc zone add`, `ibmcloud oc zone network set`, and `ibmcloud oc zone network rm` commands.

## Version v1.0.638
{: #cli-010638}

Version 1.0.638 of the CLI was released on 12 July 2024.
- Adds `ibmcloud sat experimental endpoint acl` commands.
- Adds support for the beta `ibm-object-csi-driver` add-on.
- Updates error messages.

## Version v1.0.635
{: #cli-010635}

Version 1.0.635 of the CLI was released on 10 July 2024.
- Adds storage operator add-on commands.
- Hides the `--dest-type` option from the `ibmcloud sat endpoint update command`.

## Version v1.0.632
{: #cli-010632}

Version 1.0.635 of the CLI was released on 09 July 2024.
- Adds the `--physical-address` and `--capability value` options to the `ibmcloud sat location create` command.

## Version v1.0.630
{: #cli-010630}

Version 1.0.630 of the CLI was released on 24 June 2024.
- Updates the validation logic on the `worker-pool resize` command.

## Version v1.0.628
{: #cli-010628}

Version 1.0.628 of the CLI was released on 17 June 2024.
- Adds support for managing endpoints for {{site.data.keyword.satelliteshort}} Connectors by using the the `--connector-id` option in the `ibmcloud sat connector endpoint` commands.
- Adds the `--idle-timeout-seconds` option to `ibmcloud sat connector endpoint create` and `ibmcloud sat connector endpoint update`.
- Adds `ibmcloud sat experimental endpoint authn set` command and `ibmcloud sat experimental endpoint authn rotate` commands.



## Version v1.0.618
{: #cli-010618}

Version 1.0.618 of the CLI was released on 02 May 2024.
- Extends the experimental date of the `ibmcloud sat experimental connector` commands to 01 July 2024.

## Version v1.0.617
{: #cli-010617}

Version 1.0.617 of the CLI was released on 24 April 2024.
- Adds the `ibmcloud oc vpc outbound-traffic-protection disable` and `enable` [commands](/docs/openshift?topic=openshift-kubernetes-service-cli#vpc-outbound-traffic-protection-disable-cli). 
- Adds the `ibmcloud oc vpc ls` [command](/docs/openshift?topic=openshift-kubernetes-service-cli#vpc-ls-cli).
- Updates the help text in various languages.

## Version v1.0.613
{: #cli-010613}

Version 1.0.613 of the CLI was released on 18 April 2024.
- Adds the `ibmcloud oc cluster master console-oauth-access get` and `set` [commands](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-master-console-oauth-access-get-cli). 
- Adds the `ibmcloud oc security-group ls` [command](/docs/openshift?topic=openshift-kubernetes-service-cli#security-group-ls-cli).
- Updates the help text in various languages.


## Version v1.0.601
{: #cli-010601}

Version 1.0.601 of the CLI was released on 27 February 2024.
- Adds the `--disable-outbound-traffic-protection` option for the `ibmcloud oc cluster create vpc-gen2` command. 

## Version v1.0.597
{: #cli-01597}

Version 0.1.597 of the CLI was released on 27 February 2024.
- Adds the `[-f]` option for the `ibmcloud sat connector remove` command. 

## Version v1.0.595
{: #cli-01959}

Version 0.1.595 of the CLI was released on 08 February 2024.
- Adds the `ibmcloud sat storage assignment autopatch` command for enabling and disabling automatic patch updates to your Satellite storage assignments.
- Adds the `patch` alias to the `ibmcloud sat storage assignment upgrade` command.

## Version v1.0.589
{: #cli-01589}

Version 0.1.589 of the CLI was released on 19 January 2024.
- Adds the `sat experimental connector agent` commands.
- Deprecates the `private service endpoint disable` commands.
- Updates to experimental commands.
- Resolves [CVE-2023-48795](https://nvd.nist.gov/vuln/detail/cve-2023-48795){: external}.
- Upgrades the golang version.
- Updates the phrasing of various commands and help text strings. 
