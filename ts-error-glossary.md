---

copyright:
  years: 2025, 2026

lastupdated: "2026-08-20"

keywords: openshift, error messages, error codes, troubleshooting reference

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}

# Troubleshooting error message reference
{: #ts-error-glossary}

This reference lists all documented error messages and error codes across troubleshooting topics for {{site.data.keyword.openshiftlong_notm}}. Entries are grouped by component and link to the full troubleshooting topic.
{: shortdesc}

## Clusters and masters
{: #ts-errors-cluster}

| Error message | Troubleshooting topic |
| --- | --- |
| `Cannot complete cluster master operations because the cluster has a broken webhook application.` | [Why do cluster master operations fail due to a broken webhook?](/docs/openshift?topic=openshift-webhooks_update) |
| `Cannot complete cluster master upgrade because the Upgradeable status condition is set to False.` | [Why do I see a `Cannot complete cluster master upgrade` message?](/docs/openshift?topic=openshift-ts-cluster-master-upgrade) |
| `The master is approaching its allotted memory resource limit (93%).` | [Why does my cluster master status say it is approaching its resource limit?](/docs/openshift?topic=openshift-master_resource_limit) |
| `etcd database size is approaching the maximum` | [Why do I see an `etcd database size is approaching the maximum` error?](/docs/openshift?topic=openshift-ts-etcd-capacity) |
| `The 'configuration' field is not a valid Kubernetes PodSecurityConfiguration setting.` | [Why do I get an error that my PodSecurityConfiguration is not valid?](/docs/openshift?topic=openshift-ts-pod-security-reset) |
| `No VPC is available. Create a VPC.` | [VPC: Why is no VPC available when I create a cluster in the console?](/docs/openshift?topic=openshift-ts_no_vpc) |
| `Your cluster can't pull images from the 'icr.io' domains because an IAM access policy could not be created.` | [Why can't the cluster pull images from {{site.data.keyword.registrylong_notm}} during creation?](/docs/openshift?topic=openshift-ts_image_pull_create) |
| `Image security enforcement update canceled. CAE008: can't enable Portieris image security enforcement because the cluster already has a conflicting image admission controller installed.` | [Why is my Portieris cluster image security enforcement installation canceled?](/docs/openshift?topic=openshift-portieris_enable) |
| `incorrect account for worker`, `Worker deploy failed due to network communications failing`, `Unable to connect to the IBM Cloud account.` | [Why can't I create or delete clusters or worker nodes?](/docs/openshift?topic=openshift-cluster_infra_errors) |
| `Unable to create cluster. The 'vpc-gen2' infrastructure operation failed with the message: the provided token is not authorized to view the specified subnet` | [Why do I get an `infrastructure operation failed` error when creating a VPC cluster?](/docs/openshift?topic=openshift-ts-resource-group-permissions) |
| `No resources found.`, `connection timed out`, `dial tcp: connect: connection timed out` | [Debugging common CLI issues with clusters](/docs/openshift?topic=openshift-ts_clis) |
| `Encrypted storage cannot be configured. Review the customer root key configuration for the worker pool.` | [Why can't I create a VPC cluster with encrypted worker nodes?](/docs/openshift?topic=openshift-ts-vpc-byok-encrypted-storage) |
| `Pending security group creation` | [When I create a VPC cluster, my worker nodes are stuck in `Pending security group creation`](/docs/openshift?topic=openshift-ts-sbd-cluster-create-quota) |
| `Infrastructure instance status is 'failed': Can't start instance because provisioning failed.` | [Why do I see DNS failures after adding a custom DNS resolver?](/docs/openshift?topic=openshift-ts-sbd-custom-dns) |
| `Could not store the cloud object storage bucket and IAM service key.` | [Why do I get an error about a cloud object storage bucket when I create a cluster?](/docs/openshift?topic=openshift-ts_cos_bucket_cluster_create) |
| `Could not find user.` | [Why do I see a `Could not find user` error when I try to access the web console?](/docs/openshift?topic=openshift-ts-cluster-ocp-console) |
| `No resources found.` | [After logging in to my cluster, why do I see a no resources found message?](/docs/openshift?topic=openshift-rhoks_ts_not_found) |
| `VPN server configuration update failed.` | [Why does the cluster master return a VPN server error?](/docs/openshift?topic=openshift-rhoks_ts_openvpn_login) |
| Version shows as not up to date in `oc get clusterversion` output | [Why does OpenShift show the cluster version is not up to date?](/docs/openshift?topic=openshift-ts-cluster-version-downlevel) |
| Image streams not populated on a secure by default cluster | [Why don't image streams populate on a secure by default cluster?](/docs/openshift?topic=openshift-ts_cluster_sbd_image_stream) |
| `sysdig-agent` pods in `CrashLoopBackOff` on private-only RHCOS cluster | [Why are `sysdig-agent` pods in `CrashLoopBackOff` on a private-only RHCOS cluster?](/docs/openshift?topic=openshift-ts-cluster-sysdig-ebpf) |
{: caption="Cluster and master error messages" caption-side="bottom"}

## Worker nodes
{: #ts-errors-workers}

| Error message | Troubleshooting topic |
| --- | --- |
| `The worker node instance ID changed. Reload the worker node if bare metal hardware was serviced.` | [Classic: Why is the bare metal instance ID inconsistent with worker records?](/docs/openshift?topic=openshift-bm_machine_id) |
| `The dedicated hosts for the zone 'eu-de-2' are not ready.` | [VPC: Why can't I create worker nodes on dedicated hosts?](/docs/openshift?topic=openshift-ts-worker-dedicated) |
| `SoftLayerAPIError(SoftLayer_Exception_Public): Could not obtain network VLAN with id #123456.` | [Classic: Why can't I add worker nodes with an invalid VLAN ID?](/docs/openshift?topic=openshift-suspended) |
| `Registration failed – The plan containers.kubernetes.vpc.gen2.roks is not available in <region>.` | [Why do I see a `Registration failed` error when I try to provision or reload worker nodes?](/docs/openshift?topic=openshift-ts-worker-plan-not-avail) |
| `A VSI with this profile will put user over quota.` | [VPC worker nodes fail to provision due to quota limits](/docs/openshift?topic=openshift-ts-worker-vpc-quota) |
| `warning: Container container-00 is unable to start due to an error: Back-off pulling image "registry.redhat.io/rhel8/support-tools"` | [After creating a version 4.15 cluster, my app no longer works](/docs/openshift?topic=openshift-ts-sbd-app-not-working) |
{: caption="Worker node error messages" caption-side="bottom"}

## Network health check (NHC) errors
{: #ts-errors-nhc}

The following error codes appear in the output of the `ibmcloud oc cluster health issues` command.

| Error code | Severity | Description | Troubleshooting topic |
| --- | --- | --- | --- |
| `NHC001` | Warning | Tigera operator has been reporting that Calico is in 'progressing' state for over an hour. | [Why does the Network status show an `NHC001` error?](/docs/openshift?topic=openshift-ts-network-nhc001) |
| `NHC003` | Warning | Some worker nodes in the cluster can not reach container image registries to pull images. | [Why does the Network status show an `NHC003` error?](/docs/openshift?topic=openshift-ts-network-nhc003) |
| `NHC004` | Warning | Some worker nodes in the cluster can not resolve VPE gateway hostnames. | [Why does the Network status show an `NHC004` error?](/docs/openshift?topic=openshift-ts-network-nhc004) |
| `NHC005` | Warning | Tigera operator is reporting that Calico is in 'degraded' state. | [Why does the Network status show an `NHC005` error?](/docs/openshift?topic=openshift-ts-network-nhc005) |
| `NHC006` | Warning | One or more DNS resolvers are not reachable from certain worker nodes. | [Why does the Network status show an `NHC006` error?](/docs/openshift?topic=openshift-ts-network-nhc006) |
| `NHC007` | Warning | One or more DNS resolvers are not reachable from certain worker nodes. | [Why does the Network status show an `NHC007` error?](/docs/openshift?topic=openshift-ts-network-nhc007) |
| `NHC009` | Error | The IAM token exchange request failed. | [Why does the Network status show an `NHC009` error?](/docs/openshift?topic=openshift-ts-network-nhc009) |
| `NHC010` | Error | Exceeded security group rules related quota. | [Why does the Network status show an `NHC010` error?](/docs/openshift?topic=openshift-ts-network-nhc010) |
| `NHC011` | Error | Exceeded security group related quota. | [Why does the Network status show an `NHC011` error?](/docs/openshift?topic=openshift-ts-network-nhc011) |
{: caption="Network health check (NHC) error codes" caption-side="bottom"}

## Ingress status errors (ERR and ESS codes)
{: #ts-errors-ingress-codes}

The following error codes appear in the output of the `ibmcloud oc ingress status-report get` command. Shared codes appear in both {{site.data.keyword.containerlong_notm}} and {{site.data.keyword.openshiftlong_notm}}.

| Error code | Error message | Troubleshooting topic |
| --- | --- | --- |
| `ERRDSIA` | The subdomain has incorrect addresses registered. | [Ingress error: ERRDSIA](/docs/openshift?topic=openshift-ts-ingress-errdsia) |
| `ERRDRISS` | The subdomain has DNS resolution issues. | [Ingress error: ERRDRISS](/docs/openshift?topic=openshift-ts-ingress-errdriss) |
| `ERRDSAISS` | The external provider for the given subdomain has authorization issues. | [Ingress error: ERRDSAISS](/docs/openshift?topic=openshift-ts-ingress-errdsaiss) |
| `ERRDSISS` | The subdomain has TLS secret issues. | [Ingress error: ERRDSISS](/docs/openshift?topic=openshift-ts-ingress-errdsiss) |
| `ERRSAM` | The load balancer service address is missing. | [Ingress error: ERRSAM](/docs/openshift?topic=openshift-ts-ingress-errsam) |
| `ESSDNE` | The secret is not present on the cluster or is in the wrong namespace. | [Ingress error: ESSDNE](/docs/openshift?topic=openshift-ts-ingress-essdne) |
| `ESSEC` | The certificate for TLS secret expired or will expire soon. | [Ingress error: ESSEC](/docs/openshift?topic=openshift-ts-ingress-essec) |
| `ESSEF` | The Opaque secret field expired or will expire soon. | [Ingress error: ESSEF](/docs/openshift?topic=openshift-ts-ingress-essef) |
| `ESSSMG` | Could not find the secret group. | [Ingress error: ESSSMG](/docs/openshift?topic=openshift-ts-ingress-esssmg) |
| `ESSSMI` | Could not access Secrets Manager instance. | [Ingress error: ESSSMI](/docs/openshift?topic=openshift-ts-ingress-esssmi) |
| `ESSSMINF` | The Secrets Manager instance is not found. | [Ingress error: ESSSMINF](/docs/openshift?topic=openshift-ts-ingress-esssminf) |
| `ESSVC` | The CRN does not match the default secret with the same domain. | [Ingress error: ESSVC](/docs/openshift?topic=openshift-ts-ingress-essvc) |
| `ESSWS` | The secret status shows a warning. | [Ingress error: ESSWS](/docs/openshift?topic=openshift-ts-ingress-essws) |
| `ERRESNF` | The external service is missing. | [Ingress error: ERRESNF](/docs/openshift?topic=openshift-ts-ingress-erresnf) |
| `ERRIODEG` | The Ingress Operator is in a degraded state. | [Ingress error: ERRIODEG](/docs/openshift?topic=openshift-ts-ingress-erriodeg) |
| `ERRIONF` | The Ingress Operator is missing from the cluster. | [Ingress error: ERRIONF](/docs/openshift?topic=openshift-ts-ingress-errionf) |
| `ERRRNA` | One or more routes not admitted. | [Ingress error: ERRRNA](/docs/openshift?topic=openshift-ts-ingress-errrna) |
| `ERRSAMO` | The load balancer service address is missing. | [Ingress error: ERRSAMO](/docs/openshift?topic=openshift-ts-ingress-errsamo) |
| `ERRSEIPM` | The service is missing one or more worker IPs. | [Ingress error: ERRSEIPM](/docs/openshift?topic=openshift-ts-ingress-errseipm) |
| | `XXX.us-south.containers.appdomain.cloud: dial tcp: ... can't marshal DNS message` | [Why does the DNS Operator show a `RouteHealthDegraded` or `can't marshal DNS message` error?](/docs/openshift?topic=openshift-ts-ingress-operator-degraded) |
{: caption="Ingress status error codes (ERR and ESS)" caption-side="bottom"}

## Load balancers
{: #ts-errors-lb}

| Error message | Troubleshooting topic |
| --- | --- |
| `The VPC load balancer that routes requests to this Kubernetes LoadBalancer service is offline.` | [VPC clusters: Why can't my app connect via load balancer?](/docs/openshift?topic=openshift-vpc_ts_lb) |
| `The subnet with ID(s) '<subnet_id>' has insufficient available ipv4 addresses.` | [VPC clusters: Why does a Kubernetes `LoadBalancer` service fail with no IPs?](/docs/openshift?topic=openshift-vpc_no_lb) |
| `The load balancer was created in zone <zone>. This setting cannot be changed.` | [VPC Clusters: My VPC NLB has a zone error and does not update](/docs/openshift?topic=openshift-ts-nlb-vpc-zone) |
| `Warning CreatingCloudLoadBalancerFailed ... Failed ensuring LoadBalancer: FindLoadBalancer failed ... 401 Unauthorized ... BXNIM0430E` | [Why do I see `SyncLoadBalancerFailed` errors when creating a VPC cluster?](/docs/openshift?topic=openshift-ts-loadbalancer-sync-failed) |
| Security group protocol mismatch events on load balancer creation or update | [VPC clusters: Security group protocol error creating or updating a LoadBalancer](/docs/openshift?topic=openshift-vpc_ts_lb_security_group_error) |
| `CAE003: Unable to determine the ingress IP address for the network load balancer.` | [Classic clusters: Why does the master status have an ingress IP address for NLB error?](/docs/openshift?topic=openshift-rhoks_ts_openvpn_subnet) |
| VPC load balancer health status shows only 2 of N instances as passing | [VPC clusters: Why do I see VPC load balancer health status failures?](/docs/openshift?topic=openshift-vpc_lb_healthcheck) |
| `Error on cloud load balancer ... Service and associated VPC load balancer do not match ... hostname.invalid` | [Why does my Private Path NLB contain a `hostname.invalid` error?](/docs/openshift?topic=openshift-ts-ppnlb-hostname) |
| Ingress subdomain DNS issue | [Why does my Ingress subdomain have a DNS issue?](/docs/openshift?topic=openshift-ingress_subdomain_dns_marshal) |
{: caption="Load balancer error messages" caption-side="bottom"}

## Apps and services
{: #ts-errors-apps}

| Error message | Troubleshooting topic |
| --- | --- |
| `Failed to create pod sandbox: rpc error: ... failed to request 1 IPv4 addresses. IPAM allocated only 0` | [Why don't my containers start?](/docs/openshift?topic=openshift-ts-app-container-start) |
| `ImagePullBackOff` or image pull authorization errors | [Why do images fail to pull from registry with `ImagePullBackOff` or authorization errors?](/docs/openshift?topic=openshift-ts-app-image-pull) |
| `pull QPS exceeded` errors during image pulls | [Why do pods show `pull QPS exceeded` errors during image pulls?](/docs/openshift?topic=openshift-ts-vpc-image-pull-qps) |
| `Error: failed to download "<helm_repo>/<chart_name>"` | [Troubleshooting helm chart installation updated configuration values](/docs/openshift?topic=openshift-ts-app-helm-install) |
| `This service doesn't support creation of keys` | [Resolving service binding errors in IBM Cloud clusters](/docs/openshift?topic=openshift-ts-app-svc-key) |
| Pod remains in `Pending` state | [Why do pods remain in pending state?](/docs/openshift?topic=openshift-ts-app-pod-pending) |
| Pod repeatedly fails to restart or is unexpectedly removed | [Why do pods repeatedly fail to restart or are unexpectedly removed?](/docs/openshift?topic=openshift-ts-app-pod-fail) |
| `error: build error: After retrying 2 times, Pull image still failed due to error: unauthorized: authentication required` | [Why does my build error due to image pull authentication?](/docs/openshift?topic=openshift-ts-app-build-img-pull) |
| `received unexpected HTTP status: 504 Gateway Time-out` | [Why does pushing to the internal registry time out?](/docs/openshift?topic=openshift-ts-app-timeout) |
| `error: build error: Failed to push image: error copying layers and metadata` | [Why does my pod not build with a permission denied error because of security context constraint (SCC)?](/docs/openshift?topic=openshift-ts-app-scc) |
| `dial tcp 161.26.0.28:443: connect: network is unreachable` | [Why can't I push images to the internal registry from outside the VPC network?](/docs/openshift?topic=openshift-ts-app-ocr-vpc-push) |
| Pod is in `CrashLoopBackOff` status | [Why are my pods in a `CrashLoopBackOff` status?](/docs/openshift?topic=openshift-ts-app-pod-crashloop) |
| `oc debug` fails with a `container is unable to start error` | [Why does the `oc debug` command fail with a `container is unable to start error`?](/docs/openshift?topic=openshift-ts-app-oc-debug) |
| `The entitlement 'ocp_entitled' was not found.` | [Why do I see a license or entitlement error when creating a worker pool?](/docs/openshift?topic=openshift-ts-workerpool-license-entitlement) |
| `Error: Unable to find a match: kernel-headers-VERSION kernel-devel-VERSION` | [Why does my NVIDIA GPU driver installation fail on RHEL 9 worker nodes?](/docs/openshift?topic=openshift-ts-gpu-driver-rhel9-eus) |
| `Failed to get StorageCluster","error":"no matches for kind \"StorageCluster\" in version \"ocs.openshift.io/v1\"` | [Why are no pods listed in the `openshift-storage` namespace?](/docs/openshift?topic=openshift-ts-ocs-no-pods) |
| Pods in `openshift-marketplace` namespace in `ImagePullBackOff` | [Pods in the `openshift-marketplace` namespace are in `ImagePullBackOff`](/docs/openshift?topic=openshift-ts-openshift-marketplace) |
| `failed to set feature gates` error on worker node upgrade | [Why do I see a `failed to set feature gates` error when upgrading a worker node?](/docs/openshift?topic=openshift-ts-cloud-pak-ds) |
| Confidential container scheduling failure: `Insufficient kata.peerpods.io/vm` | [How do I troubleshoot confidential containers?](/docs/openshift?topic=openshift-ts-confidential-containers) |
{: caption="App and service error messages" caption-side="bottom"}

## Permissions and credentials
{: #ts-errors-perms}

| Error message | Troubleshooting topic |
| --- | --- |
| `User doesn't have permissions to create or manage Storage` | [What permissions do I need to manage storage and create PVCs?](/docs/openshift?topic=openshift-missing_permissions) |
{: caption="Permission and credential error messages" caption-side="bottom"}

## Secure by default (SBD)
{: #ts-errors-sbd}

| Error message | Troubleshooting topic |
| --- | --- |
| `warning: Container container-00 is unable to start due to an error: Back-off pulling image "registry.redhat.io/rhel8/support-tools"` | [After creating a version 4.15 cluster, my app no longer works](/docs/openshift?topic=openshift-ts-sbd-app-not-working) |
| `Pending security group creation` | [When I create a VPC cluster, my worker nodes are stuck in `Pending security group creation`](/docs/openshift?topic=openshift-ts-sbd-cluster-create-quota) |
| `Infrastructure instance status is 'failed': Can't start instance because provisioning failed.` | [Why do I see DNS failures after adding a custom DNS resolver?](/docs/openshift?topic=openshift-ts-sbd-custom-dns) |
| Nodeport apps not working after updating to version 4.15 | [Fixing nodeport apps after updating cluster version 4.15 or later](/docs/openshift?topic=openshift-ts-sbd-nodeport-not-working) |
| Other clusters in the VPC failing after creating a version 4.15 cluster | [After creating a version 4.15 cluster, applications running in other clusters in my VPC are failing](/docs/openshift?topic=openshift-ts-sbd-other-clusters) |
| VSIs cannot access VPE gateway | [Why can't my VSIs access VPE gateway?](/docs/openshift?topic=openshift-ts-sbd-vsi-vpe) |
{: caption="Secure by default (SBD) error messages" caption-side="bottom"}

## File Storage
{: #ts-errors-file}

| Error message | Troubleshooting topic |
| --- | --- |
| `MountVolume.SetUp failed for volume ... mount.nfs: access denied by server while mounting` | [Classic: Why am I denied server access when mounting a volume to a worker node?](/docs/openshift?topic=openshift-ts-storage-file-access-denied) |
| `write-permission` or non-root user ownership errors on NFS mount path | [Why does my app fail when a non-root user owns the NFS file storage mount path?](/docs/openshift?topic=openshift-nonroot) |
| Group ID error applying NFS file storage permissions | [Why does my app fail with a group ID error for NFS file storage permissions?](/docs/openshift?topic=openshift-root) |
| Non-root user cannot add access to persistent storage | [Why can't I add non-root user access to persistent storage?](/docs/openshift?topic=openshift-cs_storage_nonroot) |
| File systems for worker nodes changed to read-only | [Why are the file systems for worker nodes changed to read-only?](/docs/openshift?topic=openshift-readonly_nodes) |
| PVC remains in pending state (file storage) | [Why does my file storage PVC stay in a pending state?](/docs/openshift?topic=openshift-file_pvc_pending) |
| `MetadataServiceNotEnabled` | [Why do I see a `MetadataServiceNotEnabled` error for {{site.data.keyword.filestorage_vpc_short}}?](/docs/openshift?topic=openshift-ts-storage-vpc-file-eit-metadata) |
| `MountingTargetFailed` or `rpc error: code = DeadlineExceeded desc = context deadline exceeded` | [Why do I see a `MountingTargetFailed` error for {{site.data.keyword.filestorage_vpc_short}}?](/docs/openshift?topic=openshift-ts-storage-vpc-file-eit-mount-failed) |
| `SubnetFindFailed` or `rpc error: code = FailedPrecondition` on PVC creation | [Why does PVC creation fail for {{site.data.keyword.filestorage_vpc_short}}?](/docs/openshift?topic=openshift-ts-storage-vpc-file-eit-pvc-fails) |
| `UnresponsiveMountHelperContainerUtility` | [Why do I see an `UnresponsiveMountHelperContainerUtility` error for {{site.data.keyword.filestorage_vpc_short}}?](/docs/openshift?topic=openshift-ts-storage-vpc-file-eit-unresponsive) |
| `shares_snapshot_operation_not_allowed` | [Why can't I create {{site.data.keyword.filestorage_vpc_short}} snapshots?](/docs/openshift?topic=openshift-ts-storage-vpc-file-snapshot-create) |
| `shares_snapshot_not_found` on PVC restore | [Why can't I restore my {{site.data.keyword.filestorage_vpc_short}} snapshot to a PVC?](/docs/openshift?topic=openshift-ts-storage-vpc-file-snapshot-restore) |
| VPC File Storage snapshot cannot be deleted | [Why can't I delete my {{site.data.keyword.filestorage_vpc_short}} snapshot?](/docs/openshift?topic=openshift-ts-storage-vpc-file-snapshot-delete) |
| `'rfs' profile is not accessible` or `stunnel manager is not initialized` | [Troubleshooting Regional File Storage encryption in transit](/docs/openshift?topic=openshift-ts-storage-vpc-file-rfs-eit) |
| VPC File Storage PVC stays in `Pending` with capacity roundoff | [Why does my PVC stay in Pending status when using capacity roundoff?](/docs/openshift?topic=openshift-ts-storage-vpc-file-capacity-roundoff) |
| VPC File Storage deployment permissions error | [Why does my {{site.data.keyword.filestorage_vpc_short}} deployment fail due to a permissions error?](/docs/openshift?topic=openshift-ts-storage-vpc-file-non-root) |
| App pod stuck in `Container creating` when mounting VPC File Storage | [Why is my app pod stuck in `Container creating` when trying to mount {{site.data.keyword.filestorage_vpc_short}}?](/docs/openshift?topic=openshift-ts-vpc-file-container-creating) |
| File Storage add-on in `Critical` state | [Why is the {{site.data.keyword.filestorage_vpc_short}} add-on in `Critical` state?](/docs/containers?topic=containers-ts-storage-file-addon-cm) |
{: caption="File Storage error messages" caption-side="bottom"}

## Block Storage
{: #ts-errors-block}

| Error message | Troubleshooting topic |
| --- | --- |
| `failed to mount the volume as "ext4", it already contains xfs. Mount error: mount failed: exit status 32` | [Why does mounting existing block storage to a pod fail with the wrong file system?](/docs/openshift?topic=openshift-block_filesystem) |
| `Volume not attached` | [Why do I get a `Volume not attached` error when trying to expand a {{site.data.keyword.block_storage_is_short}} volume?](/docs/openshift?topic=openshift-block_not_attached_vpc) |
| Block storage changes to read-only | [Why does block storage change to read-only?](/docs/openshift?topic=openshift-readonly_block) |
| `Message: 50% throttling of CPU in namespace kube-system for container ibmcloud-block-storage-driver-container` | [Why does the Block storage plug-in Helm chart give CPU throttling warnings?](/docs/openshift?topic=openshift-block_helm_cpu) |
| Block storage PVC remains in pending state | [Why does my block storage PVC stay in a pending state?](/docs/openshift?topic=openshift-block_pvc_pending) |
| App cannot access or write to PVC (block) | [Why can't my app access or write to a PVC?](/docs/openshift?topic=openshift-block_app_failures) |
| `Labels: ibm.io/pv-connectivity-status: limited` | [Why does my Block Storage persistent volume show a `limited` connectivity status?](/docs/openshift?topic=openshift-block-pv-limited-connectivity) |
| Block Storage API key reset causes provisioning failure | [{{site.data.keyword.block_storage_is_short}} PVC creation fails after API key reset](/docs/openshift?topic=openshift-vpc-block-api-key-reset-ts) |
| `UNEXPECTED INCONSISTENCY; RUN fsck MANUALLY.` | [Why does mounting {{site.data.keyword.blockstorageshort}} fail with a file system check error?](/docs/openshift?topic=openshift-ts-storage-fsck) |
| Block storage volume snapshot cannot be deleted | [Why can't I delete my {{site.data.keyword.block_storage_is_short}} volume snapshot resources?](/docs/openshift?topic=openshift-ts-storage-volumesnapshotdelete) |
| Block storage snapshot creation fails | [Why can't I create {{site.data.keyword.block_storage_is_short}} snapshots?](/docs/openshift?topic=openshift-ts-storage-snapshotfails) |
| Charges still appear for block storage devices after deleting the cluster | [Why am I still seeing charges for block storage devices after deleting my cluster?](/docs/openshift?topic=openshift-ts_storage_clean_volume) |
{: caption="Block Storage error messages" caption-side="bottom"}

## Object Storage
{: #ts-errors-cos}

| Error message | Troubleshooting topic |
| --- | --- |
| `pvc:...:can't access bucket <bucket_name>: NotFound: Not Found` | [Why can't my PVC access an existing bucket?](/docs/openshift?topic=openshift-cos_access_bucket_fails) |
| `Error: symlink ... helm-ibmc: file exists` | [Why does installing the Object storage Helm plug-in fail?](/docs/openshift?topic=openshift-cos_helm_fails) |
| `d--------- 1 root root 0 Jan 1 1970 <file_name>` (non-root user cannot access files) | [Resolving non-root user access issues to files in IBM Cloud](/docs/openshift?topic=openshift-cos_nonroot_access) |
| `EPERM: operation not permitted` | [Why does my app pod fail with an `Operation not permitted` error?](/docs/openshift?topic=openshift-cos_operation_not_permitted) |
| `chown: changing ownership of '<volume_mount_path>': Input/output error` | [Why can't the ownership of the mount path be changed?](/docs/openshift?topic=openshift-cos_mountpath_error) |
| `Error: rendered manifest contains a resource that already exists. ... existing_kind: storageClass` | [Why does installing the {{site.data.keyword.cos_full_notm}} plug-in fail?](/docs/openshift?topic=openshift-cos_plugin_fails) |
| `Bad value for ibm.io/object-store-endpoint ... scheme is missing.` | [Why do I see wrong s3fs or IAM API endpoints when I create a PVC?](/docs/openshift?topic=openshift-cos_api_endpoint_failure) |
| `SignatureDoesNotMatch: The request signature we calculated does not match the signature you provided.` | [Why do I see wrong credentials or access denied messages when I create a PVC?](/docs/openshift?topic=openshift-cred_failure) |
| Object Storage PVC remains in pending state | [Why does my PVC remain in a pending state?](/docs/openshift?topic=openshift-cos_pvc_pending) |
| `can't get credentials: can't get secret tsecret-key: secrets "secret-key" not found` | [Why does PVC or pod creation fail due to not finding the Kubernetes secret?](/docs/openshift?topic=openshift-cos_secret_access_fails) |
| `Transport endpoint is not connected.` | [Why is the transport endpoint not connected?](/docs/openshift?topic=openshift-cos_transport_ts_connect) |
| `Error mounting volume: s3fs mount failed: s3fs: error while loading shared libraries: libfuse.so.2` | [Why do I see a volume mounting error when using the {{site.data.keyword.cos_full_notm}} plug-in?](/docs/openshift?topic=openshift-ts-cos-storage-dep) |
| Transport endpoint not connected errors when using the COS cluster add-on | [Why do I see transport endpoint not connected errors when using the {{site.data.keyword.cos_full_notm}} cluster add-on?](/docs/openshift?topic=openshift-ts-storage-cos-csi-addon) |
{: caption="Object Storage error messages" caption-side="bottom"}

## Portworx Storage
{: #ts-errors-portworx}

| Error message | Troubleshooting topic |
| --- | --- |
| `kp.Error: ... msg='Unauthorized: The user does not have access to the specified resource'` | [Why does encryption fail with an invalid KMS endpoint?](/docs/openshift?topic=openshift-px-kms-endpoint) |
{: caption="Portworx Storage error messages" caption-side="bottom"}


## {{site.data.keyword.openshiftlong_notm}} Data Foundation (ODF)
{: #ts-errors-odf}

| Error message | Troubleshooting topic |
| --- | --- |
| `Failed to get StorageCluster","error":"no matches for kind \"StorageCluster\" in version \"ocs.openshift.io/v1\"` | [Why are no pods listed in the `openshift-storage` namespace?](/docs/openshift?topic=openshift-ts-ocs-no-pods) |
| ODF pods stuck at `Pending` | [Why are the OpenShift Data Foundation pods stuck at `Pending`?](/docs/openshift?topic=openshift-ts-ocs-pods-pending-status) |
| ODF storage cluster stuck at `Progressing` | [Why is the status of my OpenShift Data Foundation storage cluster stuck at `Progressing`?](/docs/openshift?topic=openshift-ocs-ts-error-progressing) |
| `ceph-cluster-controller: failed to reconcile ... must be no more than 63 characters` | [Why is the status of my OpenShift Data Foundation storage cluster stuck at `Failed to reconcile`?](/docs/openshift?topic=openshift-ts-ocs-roks-debug) |
{: caption="ODF error messages (Red Hat OpenShift on IBM Cloud only)" caption-side="bottom"}

## OpenShift Virtualization
{: #ts-errors-virt}

| Error message | Troubleshooting topic |
| --- | --- |
| OpenShift Virtualization Operator installation fails | [Why does the OpenShift Virtualization Operator installation fail?](/docs/openshift?topic=openshift-ts-virt-operator-install-fails) |
| HyperConverged resource deployment fails | [Why does the HyperConverged resource deployment fail?](/docs/openshift?topic=openshift-ts-virt-hyperconverged-deployment-fails) |
| VM disks fail to provision | [Why do VM disks fail to provision?](/docs/openshift?topic=openshift-ts-virt-vm-disks-fail-to-provision) |
| PVCs remain in `Pending` state | [Why do persistent volume claims stay in `Pending` for OpenShift Virtualization?](/docs/openshift?topic=openshift-ts-virt-pvcs-pending) |
| ODF installation fails for OpenShift Virtualization | [Why does the OpenShift Data Foundation installation fail for OpenShift Virtualization?](/docs/openshift?topic=openshift-ts-virt-odf-installation-fails) |
| Virtual machine fails to start | [Why does a virtual machine fail to start?](/docs/openshift?topic=openshift-ts-virt-vm-fails-to-start) |
| Live migration fails | [Why does live migration fail for a virtual machine?](/docs/openshift?topic=openshift-ts-virt-live-migration-fails) |
| Virtual machine cannot access the network | [Why can't a virtual machine access the network?](/docs/openshift?topic=openshift-ts-virt-vm-cannot-access-network) |
| VNI attachment fails | [Why does a VNI attachment fail?](/docs/openshift?topic=openshift-ts-virt-vni-attachment-fails) |
| Localnet user defined network not working | [Why is the localnet user defined network not working?](/docs/openshift?topic=openshift-ts-virt-localnet-udn-not-working) |
| VMs with VNI attachments cannot communicate | [Why can't VMs with VNI attachments communicate?](/docs/openshift?topic=openshift-ts-virt-vni-vms-cannot-communicate) |
| Virtual machine performance is poor | [Why is virtual machine performance poor?](/docs/openshift?topic=openshift-ts-virt-vm-performance-is-poor) |
| Live migration is slow | [Why is live migration slow?](/docs/openshift?topic=openshift-ts-virt-live-migration-is-slow) |
{: caption="OpenShift Virtualization error messages (Red Hat OpenShift on IBM Cloud only)" caption-side="bottom"}


## Related links
{: #ts-errors-related}

- [Checking the Ingress status report](/docs/openshift?topic=openshift-ingress-status)
- [Checking the status of Network components](/docs/openshift?topic=openshift-network-status)
- [Cluster states and statuses](/docs/openshift?topic=openshift-cluster-states-reference)
- [Worker node states](/docs/openshift?topic=openshift-worker-node-state-reference)
- [Getting help and support](/docs/openshift?topic=openshift-get-help)
