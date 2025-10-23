---

copyright: 
  years: 2014, 2025
lastupdated: "2025-10-22"


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
- Resolves [CVE-2023-48795](https://nvd.nist.gov/vuln/detail/CVE-2023-48795){: external}.
- Upgrades the golang version.
- Updates the phrasing of various commands and help text strings. 

## Version v1.0.579
{: #cli-01579}


Version 0.1.579 of the CLI was released on 7 November 2023.
- Deprecates `logging collect` commands.
- Removes beta tag for `sat storage assignment` commands.

## Version 0.1.573
{: #cli-01573}


Version 0.1.573 of the CLI was released on 10 October 2023.
- Deprecates the various `logging` commands.
- Updates the help text in various languages.


## Version v1.0.566
{: #cli-10566}

Version 1.0.566 of the CLI was released on 18 September 2023.
- Updates the phrasing of various commands and help text strings. 
- Updates the help text in various languages. 

## Version v1.0.540
{: #cli-10549}

Version 1.0.540 of the CLI was released on 19 July 2023.
- Adds new [`ibmcloud oc ingress alb autoscale`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_alb_autoscale_get) commands.
- Replaces the deprecated `ibmcloud oc alb ls` command in certain command help texts.
- Updates the help text in various languages. 

## Version v1.0.528
{: #cli-10528}

Version 1.0.528 of the CLI was released on 26 June 2023.
- Removes unnecessary translations.
- Updates to `ibmcloud sat cluster register` command better recognize response headers.
- Adds Satellite connector CLI commands.
- Adds support for multiple default cluster add-on versions depending on cluster version. Updates `cluster addon versions` output.
- Updates to `ibmcloud sat cluster register` command better recognize response headers.
- Updates for pod security admission.



## Version v1.0.523
{: #cli-10523}

Version 1.0.523 of the CLI was released on 25 May 2023.
- Adds doc links to command help. 
- Updates description for the Satellite service endpoint allowlist command.
- Updates CLI to handle the new multiple default add-on versions schema.
- - Adds doc links to command help.
- Updates description for the Satellite service endpoint allowlist command.
- Updates CLI to handle the new multiple default add-on versions schema.

## Version v1.0.516
{: #cli-10516}

Version 1.0.516 of the CLI was released on 16 May 2023.
- Updates `sat storage template` command outputs to include storage template provider details.
- Updates the help text in various languages. 


## Version v1.0.510 
{: #cli-10510}

Version 1.0.510 of the CLI was released on 11 April 2023.
- Adds support for Pod Security admission.
- Resolved an issue about config file race conditions.
- Updates the `ibmcloud oc ingress domain create` command output to return the full qualified domain.

## Version v1.0.498
{: #cli-10498}

Version 1.0.498 of the CLI was released on 1 March 2023.
- Adds the `ibmcloud oc cluster master pod-security get` command.
- Updates the `golang` version to resolve [CVE-2022-41723](https://www.cve.org/CVERecord?id=2022-41723){: external}.
- Adds an `Architecture` field to the `ibmcloud oc flavor get` command output.
- Improves formatting of the `ibmcloud oc ingress secret ls` command output.
- When the `ibmcloud oc cluster config` command returns, you can run `kubectl` or `oc` commands immediately without a waiting period.
- Adds the `--host-link-agent-endpoint` option to the `ibmcloud sat host attach` command.

## Version 1.0.489
{: #cli-10489}

Version 1.0.489 of the CLI was released on 30 January 2023.
- Adds a fix where table headings are no longer printed if the output of a command contains no results.
- Adds the `--secondary-storage` option to the `cluster create vpc-gen2`, `worker-pool create vpc-gen2`, and `flavor get` commands.

## Version 1.0.487
{: #cli-10487}

Version 1.0.487 of the CLI was released on 24 January 2023.
- Adds the `satellite-service-endpoint allowlist` commands
- Updates the help text in various languages.



## Version 1.0.480
{: #cli-10480}

Version 1.0.480 of the CLI was released on 14 December 2022.
- Adjusted `ibmcloud oc flavor get` and `ibmcloud oc flavor ls` commands to show secondary storage details.
- Introduced Secondary Storage Configuration for `worker-pool get`.
- Added Ignored Errors to `ingress status-report`.
- Updates `ibmcloud sat config create` and `ibmcloud sat subscription create` commands to support new options for GitOps.

## Version 1.0.471
{: #cli-10471}

Version 1.0.471 of the CLI was released on 1 December 2022.
- Adds new endpoint type `vpe`(Virtual Private Endpoint) for cluster config command. 
- Updates the cluster get command to show VPE url.
- Adds `infrastructureTopology` field to cluster response.
- Adds JSON output to Satellite get host command.

## Version 1.0.459
{: #cli-10459}

Version 1.0.459 of the CLI was released on 21 October 2022.
- Adds the `--infrastructure-topology` option for the `ibmcloud oc cluster create satellite` command. 
- Adds new `ibmcloud oc flavor get` and `ibmcloud oc flavor ls` commands.

## Version 1.0.454
{: #cli-10454}

Version 1.0.454 of the CLI was released on 3 October 2022.
- Adds new [Ingress status](/docs/openshift?topic=openshift-kubernetes-service-cli#alb-commands) commands.
- Adds the `--operating-system` option for the cluster create commands. 

## Version 1.0.452
{: #cli-10452}

Version 1.0.452 of the CLI was released on 21 September 2022.
- Updates the help text in various languages.

## Version 1.0.446
{: #cli-10446}

Version 1.0.446 of the CLI was released on 12 September 2022.
- Adds `--pod-network-interface-selection` option to location create flow.

## Version 1.0.444
{: #cli-10444}

Version 1.0.444 of the CLI was released on 8 September 2022.
- Adds {{site.data.keyword.secrets-manager_short}} registration to cluster create flow. 
- Adds worker-pool OS support.
- Removes Ingress migration command support.

## Version 1.0.439
{: #cli-10439}

Version 1.0.439 of the CLI was released on 26 Aug 2022.
- Adds new commands to enable, disable, and get status of ALB health checker.  

## Version 1.0.433
{: #cli-10433}

Version 1.0.433 of the CLI was released on 5 Aug 2022.
- Updates the help text in various languages. 

## Version 1.0.431
{: #cli-10431}

Version 1.0.431 of the CLI was released on 15 Jul 2022.
- The `KMS Account ID` string is now translatable.

## Version 1.0.430
{: #cli-10430}

Version 1.0.430 of the CLI was released on 13 Jul 2022.
- Adds the `--kms-account-id ID` option to various commands to support cross-account encryption for KMS enablement, VPC cluster, and worker pool creation.

## Version 1.0.426
{: #cli-10426}

Version 1.0.426 of the CLI was released on 6 Jul 2022.
- Adds the `ibmcloud sat key` commands, allowing you to view and manage your {{site.data.keyword.satelliteshort}} Config keys.
- Adds the `ibmcloud sat subscription identity set` command, which updates a Satellite subscription to use your identity to manage resources.
- Adds the `--secret-group` option to various {{site.data.keyword.secrets-manager_short}} commands. With this option, you can create secret groups to organize your secrets and control who on your team has access to them.

## Version 1.0.422
{: #cli-10422}

Version 1.0.422 of the CLI was released on 20 June 2022.
- Makes the `template-version` option optional for the `ibmcloud sat storage config create` command.
- Updates the output of the `ibmcloud sat storage template ls` and `ibmcloud sat storage template get` commands to specify if a version is deprecated or the current default template version.

## Version 1.0.420
{: #cli-10420}

Version 1.0.420 of the CLI was released on 15 June 2022.
- Adds the new `ibmcloud sat storage config param set` command.  /n 2. Updates the `ibmcloud sat storage template get` command output to indicate whether a storage config is mutable.

## Version 1.0.419
{: #cli-10419}

Version 1.0.419 of the CLI was released on 7 June 2022.
- Implements various backend updates. 

## Version 1.0.415
{: #cli-10415}

Version 1.0.415 of the CLI was released on 26 May 2022.
- Updates the help text in various languages.

## Version 1.0.408
{: #cli-10408}

Version 1.0.408 of the CLI was released on 6 May 2022.
- Fixes Ingress secret type backward compatibility. 
- Deprecates the Ingress migration tool.
