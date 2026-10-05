---

copyright:
  years: 2026, 2026

lastupdated: "2026-10-05"


keywords: change log, version history, 4.22_openshift

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}





# 4.22 version change log
{: #openshift_changelog_422}

View information of version changes for major, minor, and patch updates that are available for your {{site.data.keyword.openshiftlong}} clusters that run this version. Changes include updates to {{site.data.keyword.redhat_openshift_notm}}, Kubernetes, and {{site.data.keyword.cloud_notm}} Provider components.
{: shortdesc}

## Overview
{: #changelog_overview_422}


Unless otherwise noted in the change logs, the {{site.data.keyword.cloud_notm}} provider version enables {{site.data.keyword.redhat_openshift_notm}} APIs and features that are at beta. {{site.data.keyword.redhat_openshift_notm}} alpha features are disabled and subject to change.
{: shortdesc}

Check the [Security Bulletins on {{site.data.keyword.cloud_notm}} Status](https://cloud.ibm.com/status?selected=security){: external} for security vulnerabilities that affect {{site.data.keyword.openshiftlong_notm}}. You can filter the results to view only **Kubernetes Service** security bulletins that are relevant to {{site.data.keyword.openshiftlong_notm}}. Change log entries that address other security vulnerabilities but don't include an {{site.data.keyword.IBM_notm}} security bulletin are for vulnerabilities that are not known to affect {{site.data.keyword.openshiftlong_notm}} in normal usage. If you run privileged containers, run commands on the workers, or execute untrusted code, then you might be at risk.

Master patch updates are applied automatically. Worker node patch updates can be applied by reloading or updating the worker nodes. For more information about major, minor, and patch versions and preparation actions between minor versions, see [{{site.data.keyword.redhat_openshift_notm}} versions](/docs/openshift?topic=openshift-openshift_versions).
{: tip}


## 28 September 2026, Master fix pack 4.22.13_1519_openshift
{: #cl-boms_master-42213_1519_openshift_M}

The following list shows the components that are in the master fix pack 4.22.13_1519_openshift. Master patch updates are applied automatically.
{: shortdesc}

Calico v3.31.7
:   See the [Calico release notes](https://docs.tigera.io/calico/3.31/release-notes/#calico-open-source-3317-bug-fix-release){: external}.


Cluster health image v1.6.19
:   New version contains updates and security fixes.


etcd v3.6.14
:   See the [etcd release notes](https://github.com/coreos/etcd/releases/v3.6.14){: external}.


IBM Cloud Block Storage driver and plug-in v2.5.28
:   New version contains updates and security fixes.


IBM Cloud Controller Manager v1.35.8-3
:   New version contains updates and security fixes.


IBM Cloud File Storage for Classic plug-in and monitor v457
:   New version contains updates and security fixes.


IBM Cloud RBAC Operator 109756b
:   New version contains updates and security fixes.


Key Management Service provider 2.10.30
:   New version contains updates and security fixes.


Kubernetes feature gates configuration 
:   `RotateKubeletServerCertificate=true`, `BuildCSIVolumes=true`, `NetworkLiveMigration=true`, `OpenShiftPodSecurityAdmission=false`, `AdminNetworkPolicy=true`, `KMSv1=false`, `ExternalOIDC=true`, `NetworkDiagnosticsConfig=true`, `ManagedBootImages=true`, `TranslateStreamCloseWebsocketRequests=false`, `NewOLM=false`, `DisableNodeKubeProxyVersion=false`, `ServiceAccountTokenNodeBinding=true`, `AdditionalRoutingCapabilities=true`, `CPMSMachineNamePrefix=true`, `ConsolePluginContentSecurityPolicy=true`, `GatewayAPI=true`, `GatewayAPIController=true`, `MetricsCollectionProfiles=true`, `NetworkSegmentation=true`, `RouteExternalCertificate=true`, `HighlyAvailableArbiter=true`, `ImageVolume=true`, `MachineConfigNodes=true`, `PinnedImages=true`, `ProcMountType=true`, `RouteAdvertisements=true`, `SigstoreImageVerification=true`, `StoragePerformantSecurityPolicy=true`, `UpgradeStatus=true`, `UserNamespacesPodSecurityStandards=true`, `UserNamespacesSupport=true`, `ExternalOIDCWithUIDAndExtraClaimMappings=true`, `HyperShiftOnlyDynamicResourceAllocation=true`, `ImageStreamImportMode=true`, `ManagedBootImagesvSphere=true`, `PreconfiguredUDNAddresses=true`, `SigstoreImageVerificationPKI=true`, `VolumeAttributesClass=true`. For more information, see [Kubernetes docs](https://kubernetes.io/docs/home/){: external}


Portieris admission controller v0.14.3
:   See the [Portieris admission controller release notes](https://github.com/IBM/portieris/releases/tag/v0.14.3){: external}


Red Hat OpenShift on IBM Cloud 4.22.13
:   See the [Red Hat OpenShift on IBM Cloud release notes](https://docs.redhat.com/en/documentation/openshift_container_platform/4.22/html/release_notes/ocp-4-22-release-notes#ocp-4-22-13_release-notes){: external}.


Tigera Operator v1.40.15
:   See the [Tigera Operator release notes](https://github.com/tigera/operator/releases/tag/v1.40.15){: external}.
