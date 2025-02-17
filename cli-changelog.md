---

copyright: 
  years: 2014, 2025
lastupdated: "2025-02-17"


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
- Updates the `golang` version to resolve [CVE-2022-41723](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2022-41723){: external}.
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

## Version 1.0.404
{: #cli-10404}

Version 1.0.404 of the CLI was released on 28 April 2022.
- Adds features visible to select users only. 

## Version 1.0.403
{: #cli-10403}

Version 1.0.403 of the CLI was released on 26 April 2022.
- Adds support for M1 processor on Linux and macOS.
- Updates the help text in various languages. 

## Version 1.0.394
{: #cli-10394}

Version 1.0.394 of the CLI was released on 7 April 2022.
- Adds the `--operating-system` label to `ibmcloud oc worker-pool create satellite` and `ibmcloud oc cluster create satellite`.

## Version 1.0.384
{: #cli-10384}

Version 1.0.384 of the CLI was released on 21 March 2022.
- Adds the `--output` option to the `ibmcloud oc storage assignment ls` and `ibmcloud oc storage config ls` commands.


## Version 1.0.374
{: #cli-10374}

Version 1.0.374 of the CLI was released on 24 February 2022.
- Removes the default zone in the `ibmcloud oc cluster create satellite` command.
- Fixes a routing issue for the `ibmcloud sat storage assignment create --cluster` and the `ibmcloud sat storage assignment ls --cluster` commands.


## Version 1.0.372
{: #cli-10372}

Version 1.0.372 of the CLI was released on 18 February 2022.
- Modifies relevant commands to accept either the `--worker-pool` or `-p` options for worker pool options.
- Updates JSON outputs to include additional resources, such as add-ons, VLANs, and subnets. 
- Makes `ibmcloud oc ingress` commands generally available.
- Updates the `ibmcloud oc ingress alb get` command output to include ALB status. 
- Adds the new `ibmcloud oc nlb-dns get` command.
- Adds the new `ibmcloud oc ca get` command.
- Updates the `ibmcloud oc location get` command output to indicate whether the location has IaaS provider credentials stored.
- Updates the `ibmcloud oc storage assignment ls` command to include the `--config` option option, allowing you to list only storage assignments created with the specified configuration.
- Updates the help text in various languages. 

## Version 1.0.353
{: #cli-10353}

Version 1.0.353 of the CLI was released on 3 December 2021.
- Updates the `ibmcloud sat location get` command output to include `Ignition Server Port` and `Konnectivity Server Port`.
- Updates the help text in various languages.
- Updates the help text in various languages.

## Version 1.0.347
{: #cli-10347}

Version 1.0.347 of the CLI was released on 15 November 2021.
- Updates various output messages.

## Version 1.0.344
{: #cli-10344}

Version 1.0.344 of the CLI was released on 15 November 2021.
- Includes a Go version update from `1.16.7` to `1.16.10` and other fixes.

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

- Adds the `--output` option for the `ibmcloud sat storage get` command.
- Adds the `--policy` option to the `ibmcloud oc master audit-webhook set` command. You can now configure the amount of information included in your cluster audits by specifying the `default` or `verbose` audit policy type.


## Version 1.0.327
{: #cli-10327}

Version 1.0.327 of the CLI was released on 11 October 2021.
{: shortdesc}

- Adds the `--data-location` option for the `ibmcloud sat config create` command and the `--location` option for the `ibmcloud sat storage assignment ls` command.
- Updates the help text in various languages.

## Version 1.0.312
{: #cli-10312}

Version 1.0.312 of the CLI was released on 9 August 2021.

- Removes the `ibmcloud oc nlb-dns monitor status` command. Checking the health of individual IP addresses, which was previously supported by the Cloudflare DNS provider, is not supported by the Akamai DNS provider. Instead, you can check the overall health of a subdomain by using the `ibmcloud oc nlb-dns monitor ls` command. For more information on the migration to Akamai for all `containers.appdomain.cloud`, `containers.mybluemix.net`, and `containers.cloud.ibm.com` domains, see the [migration announcement](https://cloud.ibm.com/notifications?selected=1621697674798){: external}.
- Removes the `ibmcloud oc cluster addon enable kube-terminal` command. The Kubernetes web terminal add-on became unsupported on 1 July 2021. Instead, use the [IBM Cloud Shell](/docs/cloud-shell?topic=cloud-shell-shell-ui).
- Adds CLI support for the [OpenShift Data Foundation storage add-on](/docs/openshift?topic=openshift-ocs-manage-deployment).
- Makes the `ibmcloud oc cluster addon update` feature available to all users.
- Includes the subscription status in the output of the `ibmcloud sat subscription get` and `ibmcloud sat subscription ls` commands.
- Adds the option to display the output of the `ibmcloud sat subscription get` and `ibmcloud sat subscription ls` commands in JSON format.
- Updates the help text in various languages.
- Displays OpenVPN Server Port details in the `ibmcloud sat location get` command output.
- Updates the help text in various languages.

## Version 1.0.300
{: #cli-10300}

Version 1.0.300 of the CLI was released on 12 July 2021.

- Adds the following parameters to the `ibmcloud sat location create` command so that you can optionally specify an infrastructure provider along with the region and credentials for the provider: `--provider`, `--provider-region`, and `--provider-credential`.
- Updates the help text in various languages.

## Version 1.0.295
{: #cli-10295}

Version 1.0.295 of the CLI was released on 24 June 2021.

- Removes the unsupported {{site.data.keyword.openshiftlong_notm}} Ingress image version from the output of `ibmcloud oc alb version ls`.
- In all `ibmcloud oc cluster create` commands, updated the help text to indicate that you must set the `--workers` option value to at least 2.
- Adds the following updates for add-on commands: - Adds the `ibmcloud oc cluster addon get` command to view the details of an installed add-on. 
- Adds the `ibmcloud oc cluster addon options` command to view optional installation settings for an add-on. 
- Adds the `--param` option to specify an optional installation setting for the `ibmcloud oc cluster addon enable openshift-container-storage` command.
- The `ibmcloud sat storage config` and `ibmcloud sat storage template` commands are now generally available.
- Adds the `--cluster` and `--service-cluster-id` option to the `ibmcloud sat storage assignment ls` command to filter output by the ID of a cluster that you created or the ID of a {{site.data.keyword.satelliteshort}}-enabled {{site.data.keyword.cloud_notm}} service cluster.
- Adds the `--service-cluster-id` option to the `ibmcloud sat storage assignment create` command to deploy storage drivers to a specific {{site.data.keyword.satelliteshort}}-enabled {{site.data.keyword.cloud_notm}} service cluster.
- Updates the help text in various languages.

## Version 1.0.275
{: #cli-10275}

Version 1.0.275 of the CLI was released on 26 May 2021.
  
- The `--region` option is now required for the `ibmcloud oc api-key reset`, `ibmcloud oc credential get`, and `ibmcloud oc credential set` commands. 
- Adds the `ibmcloud oc cluster addon versions` command to list the {{site.data.keyword.redhat_openshift_notm}} versions that are supported for each add-on version, and deprecates the `ibmcloud oc addon-versions` command
- The `ibmcloud oc image-security disable` and `ibmcloud oc image-security enable` commands are now generally available. 
- The IAM token that is used for your CLI session is now refreshed 5 minutes before expiration to keep the session active.
- Adds the `--cluster` option to the `ibmcloud sat storage assignment create` command to assign to an individual cluster ID instead of a cluster group.
- Adds `--location` as a required option to the `ibmcloud sat storage config create` command and an optional option to the `ibmcloud sat storage config ls` command.
- Changes the `--config` option to `--config-name` in the `ibmcloud sat storage config sc add` command.
- Adds the optional `--output json` option to the `ibmcloud sat config get`, `ibmcloud sat config ls`, and `ibmcloud sat config version get` commands.
- Increases the maximum size for the file in the `--read-config` option of the `ibmcloud sat config version create` command from 1MB to 3MB.
- Fixes the `ibmcloud sat group create` command to enable cluster group creation.
- The IAM token that is used for your CLI session is now refreshed 5 minutes before expiration to keep the session active.
- Updates the help text in various languages.


## Version 1.0.258
{: #cli-10258}

Version 1.0.258 of the CLI was released on 26 April 2021.
  
- Adds the `--ip` option to the `ibmcloud oc nlb-dns create vpc-gen2` and `ibmcloud oc nlb-dns rm vpc-gen2` commands to support DNS records for Network Load Balancers for VPC. 
- Adds the `--dns-type` option to `ibmcloud oc nlb-dns create` commands to specify the DNS provider type for the subdomain registration. Currently, only `public` DNS is supported. 
- Adds a warning that the `--region` option is planned to be required for the `ibmcloud oc api-key reset`, `ibmcloud oc credential get`, and `ibmcloud oc credential set` commands as of 10 May 2021. The region is already required by the API. Currently in the CLI, the region defaults to the targeted region if the `--region` option is not used. 
- In the output of the `ibmcloud oc addon-versions` command, changes the `Min. OpenShift version` column to `Supported Openshift Range`. 
- When `--output json` is specified for the `ibmcloud oc storage attachment get` or `ibmcloud oc storage attachment ls` commands, fixes the output so that a volume table is not printed after the JSON output. 
- Fixes a `golang` vulnerability for [CVE-2020-28852](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-28852){: external}.
- Adds the `ibmcloud sat storage config sc add`, `ibmcloud sat storage config sc get`, and `ibmcloud sat storage config sc ls` beta commands to create and view your own storage classes of {{site.data.keyword.satelliteshort}} storage configurations.
- Adds the `ibmcloud sat messages` command to view current messages from {{site.data.keyword.satellitelong_notm}}.
- Fixes a `golang` vulnerability for [CVE-2020-28852](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-28852){: external}.
- Adds the `ibmcloud sat storage assignment upgrade` and `ibmcloud sat storage config upgrade` commands.
- Updates the CLI help text in various languages.

## Version 1.0.233
{: #cli-10233}

Version 1.0.233 of the CLI was released on 1 March 2021.
- Adds the `ibmcloud sat storage config rm` command to remove a {{site.data.keyword.satelliteshort}} storage configuration.
- Removes `beta` tags from `ibmcloud sat` commands for the generally available release of {{site.data.keyword.satellitelong_notm}}.
- Adds `satellite` as a supported provider to the output of the `ibmcloud oc cluster ls` command. 
- Removes `beta` tags from `ibmcloud sat` commands for the generally available release of {{site.data.keyword.satellitelong_notm}}.
- General refactoring and improvements.

## Version 1.0.231
{: #cli-10231}

Version 1.0.231 of the CLI was released on 25 February 2021.
- Adds the `ibmcloud sat service ls` command to view {{site.data.keyword.satelliteshort}}-enabled {{site.data.keyword.cloud_notm}} service clusters in your {{site.data.keyword.satelliteshort}} location.  \n 1. Updates the Go version to 1.15.8.  \n 1. Updates the help text in various languages.
- Updates the Go version to 1.15.8. 
- Updates the help text in various languages.

## Version 1.0.223
{: #cli-102238}

Version 1.0.223 of the CLI was released on 8 February 2021.

- Adds the [`ibmcloud oc worker-pool label set`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_pool_label_set) and [`ibmcloud oc worker-pool label rm`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_pool_label_rm) commands to set and remove custom Kubernetes labels for all worker nodes in a worker pool.
- [Adds several commands and command changes for managing {{site.data.keyword.redhat_openshift_notm}} clusters in {{site.data.keyword.satelliteshort}}](/docs/openshift?topic=openshift-cs_cli_changelog).
- Adds the `ibmcloud sat storage` command group to view and manage the storage resources that run in {{site.data.keyword.redhat_openshift_notm}} clusters that are registered with {{site.data.keyword.satelliteshort}} Config.
- Adds the optional `--ha-zone` option to the `ibmcloud sat location create` command to specify three arbitrary zone names in your {{site.data.keyword.satelliteshort}} location.
- Adds the optional `--reset-key` option to the `ibmcloud sat host attach` command to reset the key that the control plane uses to communicate with all the hosts in the location.
- Moves `ibmcloud sat config configuration` commands to the `ibmcloud sat config` command group.
- Moves `ibmcloud sat config subscription` commands to the `ibmcloud sat subscription` command group.
- Renames `cluster-group` commands and `--cluster-group` options to `group`.
- Renames `configuration` commands and `--configuration` flags to `config`.
- Renames `--type` options to `--file-format`. 
- Renames the `--label` (short form `-l`) option in the `ibmcloud sat host assign`, `attach`, and `update` commands to `--host-label` (short form `-hl`).
- Adds the [`ibmcloud oc worker-pool create satellite` command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_pool_create_sat) to add worker pools to {{site.data.keyword.redhat_openshift_notm}} clusters in {{site.data.keyword.satelliteshort}}.
- Adds the [`ibmcloud oc zone add satellite` command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_zone_add_sat) to add zones to {{site.data.keyword.redhat_openshift_notm}} clusters and worker pools in {{site.data.keyword.satelliteshort}}.
- Adds the optional `--host-label`, `--pod-subnet`, `--pull-secret`, `--service-subnet`, `--workers`, and `--zone` flags to the [`ibmcloud oc cluster create satellite` command](/docs/openshift?topic=openshift-kubernetes-service-cli#cli_cluster-create-satellite).
- Adds the `satellite` value to the `--provider` option in the [`ibmcloud oc zone ls` command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_datacenters) to list zones in your {{site.data.keyword.satelliteshort}} location. 

## Version 1.0.208
{: #cli-10208}

Version 1.0.208 of the CLI was released on 18 December 2020.

- Updates the help text in various languages.

## Version 1.0.206
{: #cli-10206}

Version 1.0.206 of the CLI was released on 10 December 2020.

- Adds the `ibmcloud oc ingress lb get`, `ibmcloud oc ingress lb proxy-protocol disable`, and `ibmcloud oc ingress lb proxy-protocol disable` [beta commands](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_ingress_lb_proxy-protocol_enable) to manage the configuration of load balancers that expose Ingress ALBs in your cluster. For example, you can enable the NGINX PROXY protocol so that client connection information is passed in request headers to ALBs. 
- Adds the optional `--endpoint` option to the `ibmcloud oc cluster config` command to specify a type of endpoint for the cluster context, such as the cluster's private cloud service endpoint. 
- Updates the help text in various languages. 
- Updates the Go version to 1.15.6.

## Version 1.0.197
{: #cli-10197}

Version 1.0.197 of the CLI was released on 18 November 2020.

- Adds a warning message to the `ibmcloud oc cluster config` command about temporary `oc` command failures due to RBAC synchronization. 
- Ensures that incident IDs are returned with 500-level messages. 
- In `ibmcloud oc cluster storage` commands, the cluster name is now accepted in the `--cluster` option in addition to the cluster ID. 
- Updates the output of the `ibmcloud oc ingress alb migrate` command to be more readable.
- Adds the `--endpoint` option to the [`ibmcloud oc cluster config` command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_cluster_config) to use the Link endpoint URL for the cluster context.
- Updates the help text in various languages.

## Version 1.0.178
{: #cli-10178}

Version 1.0.178 of the CLI was released on 6 October 2020.

- Updates the Go version to 1.15.2.
- Updates the help text in various languages.
- Adds `http-tunnel` as a supported source or destination protocol in the `ibmcloud sat endpoint create` and `ibmcloud sat endpoint update` commands.

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
- Adds the `ibmcloud oc ingress alb migrate` set of beta commands to migrate resources that are formatted for ALBs that run the {{site.data.keyword.openshiftlong_notm}} Ingress image to resources that are formatted for ALBs that run the Kubernetes Ingress image. 
- Adds the [`ibmcloud oc ingress alb enable`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_alb_configure) and [`ibmcloud oc ingress alb disable`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_alb_disable) commands. 
- Adds the optional `--version` option to the `ibmcloud oc ingress alb create` command to specify the {{site.data.keyword.openshiftlong_notm}} Ingress image version or Kubernetes Ingress image version for the ALB.

**Renamed commands**: The following commands are shifted to new naming categories. 
- Shifts all existing `ibmcloud oc alb` commands into the [`ibmcloud oc ingress alb`](/docs/openshift?topic=openshift-kubernetes-service-cli#alb-commands) subcategory. 
- Changes the names of the following options in the relevant `ibmcloud oc ingress alb` commands: `--alb-id` to `--alb`, `--secret-name` to `--name`, and `--user-ip` to `--ip`.

**Deprecated commands**: The following commands are deprecated in favor of the new commands. 
- Deprecates the `ibmcloud oc alb cert` set of commands. 
- Deprecates the `ibmcloud oc alb configure` command. 
- Removes the deprecated `ibmcloud oc alb rollback` command,

## Version 1.0.143
{: #cli-10143}

Version 1.0.143 of the CLI was released on 6 August 2020.

- Adds the [`ibmcloud oc quota ls`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_quota_ls) command to list all quota and limits for cluster-related resources in your {{site.data.keyword.cloud_notm}} account. 
- Deprecates the `--json` option. To print a command output in JSON format, use the `--output json` option instead. 
- Deprecates the `-s` option. To not show the message of the day or update reminders in command output, use the `-q` option instead. 
- Updates `ibmcloud oc cluster ls` command so that if you include the `--ouput json` option but don't include the `--provider` option, only classic clusters are returned. 
- Corrects the example master update command that is displayed in the output of the `ibmcloud oc cluster get` command when a master update is available. 
- Adds information about the effects of worker node replacement in the warning message for the `ibmcloud oc worker replace` command. 
- Standardizes the help text for options that have a list of supported values. 
- Updates the help text in various languages.

## Version 1.0.118
{: #cli-10118}

Version 1.0.118 of the CLI was released on 7 July 2020.

- Deprecates the `ibmcloud oc cluster user-subnet add`, `ibmcloud oc cluster user-subnet rm`, and `ibmcloud oc va` commands.
- Updates the Go version to 1.13.12 for [CVE-2020-7919](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-7919){: external}. 
- Fixes a bug for downloading the Calico configuration by using the `--network` option in the `ibmcloud oc cluster config` command. 
- Updates the help text for the `--endpoint` option of the `ibmcloud oc kms enable` command. 
- Updates the help text in various languages.

## Version 1.0.99
{: #cli-1099}

Version 1.0.99 of the CLI was released on 15 June 2020.


- Adds the `--cos-instance` option to the `ibmcloud oc cluster create vpc-gen2` command to back up the images from your {{site.data.keyword.redhat_openshift_notm}} internal registry to a bucket in your {{site.data.keyword.cos_full_notm}} instance.
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
- Adds the **Ingress Status** and **Ingress Message** fields to the output of the `ibmcloud oc cluster get` command. For more information about these fields, see [Checking the status of Ingress components](/docs/openshift?topic=openshift-ingress-status).
- Adds the ALB ID to the output of the `ibmcloud oc alb create` command. 
- Adds the supported `Auth version` to the output of the `ibmcloud oc alb versions` command. 
- Adds the supported range of Kubernetes versions that your cluster must run to the output of the `ibmcloud oc addon versions` command. 
- Updates the help text in various languages.

## Version 1.0.57
{: #cli-1057}

Version 1.0.57 of the CLI was released on 7 May 2020.

- Adds a check for deprecated positional options. 
- Updates the macOS DNS resolver to fix network issues when you use the CLI plug-in with a VPN connection. 
- Help documentation updates: 
    - Adds instructions for enabling or disabling an add-on to the help text for the `ibmcloud oc addon-versions` command. 
    - Clarifies optional and required options in option help text. 
    - Updates the help text in various languages.

## Version 1.0.28
{: #cli-1028}

Version 1.0.28 of the CLI was released on 6 April 2020.

- Adds the optional `--alb-id` option to `ibmcloud oc alb update` so that you can specify IDs of individual ALBs to update. 
- Adds the optional `--show-storage` option to `ibmcloud oc flavors` to show additional raw disks that are available for [SDS worker node flavors](/docs/openshift?topic=openshift-classic-flavors). In the tables for each metro area section, SDS flavors are in the **Bare Metal** tabs and end with `.ssd`.
- Adds a message to the output of `ibmcloud oc pull-secret apply` about the amount of time it takes for the pull secrets to be applied to your cluster.

## Version 1.0.15
{: #cli-1015}

Version 1.0.15 of the CLI was released on 24 March 2020.

- Adds the [`ibmcloud oc nlb-dns secret regenerate`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_nlb-dns-secret-regenerate) and [`ibmcloud oc nlb-dns secret rm`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_nlb-dns-secret-rm) commands to help you manage secrets for NLB subdomains. 
- Adds the optional `--worker-pool WORKER_POOL` option to `ibmcloud oc zone rm`. 
- Deprecates the option to specify a YAML file in the `--file` option of the `ibmcloud oc cluster create` and `ibmcloud oc worker add` commands. Instead, specify values for your cluster in the supported options for these commands. 
- Fixes the following bugs: 
    - For `ibmcloud oc cluster rm`, the `--force-delete-storage` option no longer sets the `-f` option.
- Updates the help text in various languages.

## Version 1.0.0
{: #cli-100}

Version 1.0.0 of the CLI was released on 26 March 2020.

- Introduces permanent behavior and syntax changes that are not compatible with earlier versions.
