---

copyright:
  years: 2026, 2026
lastupdated: "2026-05-14"

keywords: openshift, benchmarks, 4.21, openshift benchmarks, openshift 4.21, compliance operator, compliance

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}

# 4.21 compliance operator benchmark
{: #benchmarks-421-co}

Review the compliance operator benchmark results for {{site.data.keyword.openshiftlong_notm}} version 4.21.
{: shortdesc}



## 1 Control plane components
{: #control-plane-components-421-co}



### 1.1 Master node configuration files
{: #master-node-configuration-files-421-co}


The master node configuration is not stored as a set of files; and therefore, rules in section 1.1 are out of the scope of the automated check by the compliance operator.



### 1.2 API server
{: #api-server-421-co}

| Section|Recommendation|Manual/Automated|Level|Result |
| -- | -- | -- | -- | -- |
| 1.2.1|Ensure that anonymous requests are authorized. |Automated|1|Not checked |
| 1.2.2|Use https for kubelet connections. |Automated|1|Pass |
| 1.2.3|Ensure that the kubelet uses certificates to authenticate. |Automated|1|Pass |
| 1.2.4|Verify that the kubelet certificate authority is set as appropriate. |Automated|1|Pass |
| 1.2.5|Ensure that the `--authorization-mode` argument is not set to `AlwaysAllow`. |Automated|1|Pass |
| 1.2.6|Verify that RBAC is enabled. |Automated|1|Pass |
| 1.2.7|Ensure that the `APIPriorityAndFairness` feature gate is enabled. |Manual|1|Inherently met |
| 1.2.8|Ensure that the admission control plug-in `AlwaysAdmit` is not set. |Automated|1|Pass |
| 1.2.9|Ensure that the admission control plug-in `AlwaysPullImages` is not set. |Automated|1|Pass |
| 1.2.10|Ensure that the admission control plug-in `ServiceAccount` is set. |Automated|1|Pass |
| 1.2.11|Ensure that the admission control plug-in `NamespaceLifecycle` is set. |Automated|1|Pass |
| 1.2.12|Ensure that the admission control plug-in `SecurityContextConstraint` is set. |Automated|1|Pass |
| 1.2.13|Ensure that the admission control plug-in `NodeRestriction` is set. |Automated|1|Pass |
| 1.2.14|Ensure that the `--insecure-bind-address` argument is not set. |Automated|1|Pass |
| 1.2.15|Ensure that the `--insecure-port` argument is set to 0. |Manual|1|Inherently met |
| 1.2.16|Ensure that the `--secure-port` argument is not set to 0. |Automated|1|Pass |
| 1.2.17|Ensure that the `healthz` endpoint is protected by RBAC. |Automated|1|Not checked |
| 1.2.18|Ensure that the `--audit-log-path` argument is set. |Automated|1|Pass |
| 1.2.19|Ensure that the audit logs are forwarded off the cluster for retention. |Automated|1|[Not checked](#ibm-remediations-and-explanations-421-co) |
| 1.2.20|Ensure that the `maximumRetainedFiles` argument is set to `10` or as appropriate. |Automated|1|[Not checked](#ibm-remediations-and-explanations-421-co) |
| 1.2.21|Configure Kubernetes API Server Maximum Audit Log Size. |Automated|1|Not checked |
| 1.2.22|Ensure that the `--request-timeout` argument is set. |Automated|1|Pass |
| 1.2.23|Ensure that the `--service-account-lookup` argument is set to true. |Automated|1|Pass |
| 1.2.24|Ensure that the `--service-account-key-file` argument is set as appropriate. |Automated|1|Pass |
| 1.2.25|Ensure that the `--etcd-certfile` and `--etcd-keyfile` arguments are set as appropriate. |Automated|1|Pass |
| 1.2.26|Ensure that the `--tls-cert-file` and `--tls-private-key-file` arguments are set as appropriate. |Automated|1|Pass |
| 1.2.27|Ensure that the `--client-ca-file` argument is set as appropriate. |Automated|1|Pass |
| 1.2.28|Ensure that the `--etcd-cafile` argument is set as appropriate. |Automated|1|Pass |
| 1.2.29|Ensure that encryption providers are appropriately configured. |Automated|1|[Not checked](#ibm-remediations-and-explanations-421-co) |
| 1.2.30|Ensure that the API Server only makes use of Strong Cryptographic Ciphers. |Automated|1|Not checked |
| 1.2.31|Ensure unsupported configuration overrides are not used. |Manual|1|Pass |
{: caption="Benchmarks for api server." caption-side="top"}


### 1.3 Controller manager
{: #controller-manager-421-co}

| Section|Recommendation|Manual/Automated|Level|Result |
| -- | -- | -- | -- | -- |
| 1.3.1|Ensure that controller manager `healthz` endpoints are protected by RBAC. |Automated|1|Not checked |
| 1.3.2|Ensure that the `--use-service-account-credentials` argument is set to true. |Automated|1|Pass |
| 1.3.3|Ensure that the `--service-account-private-key-file` argument is set as appropriate. |Automated|1|Pass |
| 1.3.4|Ensure that the `--root-ca-file` argument is set as appropriate. |Automated|1|Pass |
{: caption="Benchmarks for controller manager." caption-side="top"}


### 1.4 Scheduler
{: #scheduler-421-co}

| Section|Recommendation|Manual/Automated|Level|Result |
| -- | -- | -- | -- | -- |
| 1.4.1|Ensure that the `healthz` endpoints for the scheduler are protected by RBAC. |Automated|1|Not checked |
| 1.4.2|Verify that the scheduler API service is protected by RBAC. |Automated|1|Not checked |
{: caption="Benchmarks for scheduler." caption-side="top"}


## 2 Etcd
{: #etcd-421-co}

| Section|Recommendation|Manual/Automated|Level|Result |
| -- | -- | -- | -- | -- |
| 2.1|Ensure that the `--cert-file` and `--key-file` arguments are set as appropriate. |Automated|1|Pass |
| 2.2|Ensure that the `--client-cert-auth` argument is set to true. |Automated|1|Pass |
| 2.3|Ensure that the `--auto-tls` argument is not set to true. |Automated|1|Pass |
| 2.4|Ensure that the `--peer-cert-file` and `--peer-key-file` arguments are set as appropriate. |Automated|1|Pass |
| 2.5|Ensure that the `--peer-client-cert-auth` argument is set to true. |Automated|1|Pass |
| 2.6|Ensure that the `--peer-auto-tls` argument is not set to true. |Automated|1|Pass |
| 2.7|Ensure that a unique Certificate Authority is used for etcd. |Automated|2|[Not checked](#ibm-remediations-and-explanations-421-co) |
{: caption="Benchmarks for etcd." caption-side="top"}


## 3 Control plane configuration
{: #control-plane-configuration-421-co}



### 3.1 Authentication and authorization
{: #authentication-and-authorization-421-co}

| Section|Recommendation|Manual/Automated|Level|Result |
| -- | -- | -- | -- | -- |
| 3.1.1|Client certificate authentication should not be used for users. |Automated|2|Pass |
{: caption="Benchmarks for authentication and authorization." caption-side="top"}


### 3.2 Logging
{: #logging-421-co}

| Section|Recommendation|Manual/Automated|Level|Result |
| -- | -- | -- | -- | -- |
| 3.2.1|Ensure that a minimal audit policy is created. |Automated|1|Not checked |
| 3.2.2|Ensure that the audit policy covers key security concerns. |Automated|2|Not checked |
{: caption="Benchmarks for logging." caption-side="top"}



## 4 Worker nodes
{: #worker-nodes-421-co}



### 4.1 Worker node configuration files
{: #worker-node-configuration-files-421-co}

| Section|Recommendation|Manual/Automated|Level|Result |
| -- | -- | -- | -- | -- |
| 4.1.1|Ensure that the kubelet service file permissions are set to 644 or more restrictive. |Automated|1|Pass |
| 4.1.2|Ensure that the kubelet service file ownership is set to root:root. |Automated|1|Pass |
| 4.1.3|If proxy kube proxy configuration file exists ensure permissions are set to 644 or more restrictive. |Automated|1|Not checked |
| 4.1.4|If proxy kubeconfig file exists ensure ownership is set to root:root. |Automated|1|Not checked |
| 4.1.5|Ensure that the `--kubeconfig` `kubelet.conf` file permissions are set to 644 or more restrictive. |Automated|1|Pass |
| 4.1.6|Ensure that the `--kubeconfig` `kubelet.conf` file ownership is set to root:root. |Automated|1|Pass |
| 4.1.7|Ensure that the certificate authorities file permissions are set to 644 or more restrictive. |Automated|1|Pass |
| 4.1.8|Ensure that the client certificate authorities file ownership is set to root:root. |Automated|1|Pass |
| 4.1.9|Ensure that the kubelet `--config` configuration file has permissions set to 600 or more restrictive. |Automated|1|Pass |
| 4.1.10|Ensure that the kubelet configuration file ownership is set to root:root. |Automated|1|Pass |
{: caption="Benchmarks for worker node configuration files." caption-side="top"}


### 4.2 Kubelet
{: #kubelet-421-co}

| Section|Recommendation|Manual/Automated|Level|Result |
| -- | -- | -- | -- | -- |
| 4.2.1|Activate Garbage collection in OpenShift Container Platform 4, as appropriate. |Automated|1|Pass |
| 4.2.2|Ensure that the `--anonymous-auth` argument is set to false. |Automated|1|Pass |
| 4.2.3|Ensure that the `--authorization-mode` argument is not set to `AlwaysAllow`. |Automated|1|Pass |
| 4.2.4|Ensure that the `--client-ca-file` argument is set as appropriate. |Automated|1|Pass |
| 4.2.5|Verify that the read only port is not used or is set to 0. |Automated|1|Pass |
| 4.2.6|Ensure that the `--streaming-connection-idle-timeout` argument is not set to 0. |Automated|1|Pass |
| 4.2.7|Ensure that the `--make-iptables-util-chains` argument is set to true. |Automated|1|Pass |
| 4.2.8|Ensure that the `kubeAPIQPS` [`--event-qps`] argument is set to a level which ensures appropriate event capture. |Automated|2|Pass |
| 4.2.9|Ensure that the `--tls-cert-file` and `--tls-private-key-file` arguments are set as appropriate. |Automated|1|Pass |
| 4.2.10|Ensure that the `--rotate-certificates` argument is not set to false. |Automated|1|Pass |
| 4.2.11|Verify that the `RotateKubeletServerCertificate` argument is set to true. |Automated|1|Pass |
| 4.2.12|Ensure that the Kubelet only makes use of Strong Cryptographic Ciphers. |Automated|1|Pass |
{: caption="Benchmarks for kubelet." caption-side="top"}



## 5 Policies
{: #policies-421-co}



### 5.1 RBAC and service accounts
{: #rbac-and-service-accounts-421-co}

| Section|Recommendation|Manual/Automated|Level|Result |
| -- | -- | -- | -- | -- |
| 5.1.1|Ensure that the cluster-admin role is only used where required. |Manual|1|Manual |
| 5.1.2|Minimize access to secrets. |Manual|1|Manual |
| 5.1.3|Minimize wildcard use in `Roles` and `ClusterRoles`. |Manual|1|Manual |
| 5.1.4|Minimize access to create pods. |Manual|1|Manual |
| 5.1.5|Ensure that default service accounts are not actively used. |Manual|1|Manual |
| 5.1.6|Ensure that Service Account Tokens are only mounted where necessary. |Manual|1|Manual |
{: caption="Benchmarks for rbac and service accounts." caption-side="top"}


### 5.2 Security context constraints
{: #security-context-constraints-421-co}

| Section|Recommendation|Manual/Automated|Level|Result |
| -- | -- | -- | -- | -- |
| 5.2.1|Minimize the admission of privileged containers. |Manual|1|Manual |
| 5.2.2|Minimize the admission of containers wishing to share the host process ID namespace. |Manual|1|Manual |
| 5.2.3|Minimize the admission of containers wishing to share the host IPC namespace. |Manual|1|Manual |
| 5.2.4|Minimize the admission of containers wishing to share the host network namespace. |Manual|1|Manual |
| 5.2.5|Minimize the admission of containers with `allowPrivilegeEscalation`. |Manual|1|Manual |
| 5.2.6|Minimize the admission of root containers. |Manual|2|Manual |
| 5.2.7|Minimize the admission of containers with the NET_RAW capability. |Manual|1|Manual |
| 5.2.8|Minimize the admission of containers with added capabilities. |Automated|1|[Not checked](#ibm-remediations-and-explanations-421-co) |
| 5.2.9|Minimize the admission of containers with capabilities assigned. |Manual|2|Manual |
| 5.2.10|Minimize access to privileged Security Context Constraints. |Manual|2|Manual |
{: caption="Benchmarks for security context constraints." caption-side="top"}


### 5.3 Network policies and CNI
{: #network-policies-and-cni-421-co}

| Section|Recommendation|Manual/Automated|Level|Result |
| -- | -- | -- | -- | -- |
| 5.3.1|Ensure that the CNI in use supports Network Policies. |Automated|1|Not checked |
| 5.3.2|Ensure that all Namespaces have Network Policies defined. |Manual|2|[Manual](#ibm-remediations-and-explanations-421-co) |
{: caption="Benchmarks for network policies and CNI." caption-side="top"}


### 5.4 Secrets management
{: #secrets-management-421-co}

| Section|Recommendation|Manual/Automated|Level|Result |
| -- | -- | -- | -- | -- |
| 5.4.1|Prefer using secrets as files over secrets as environment variables. |Manual|1|Manual |
| 5.4.2|Consider external secret storage. |Manual|2|Manual |
{: caption="Benchmarks for secrets management." caption-side="top"}


### 5.5 Extensible admission control
{: #extensible-admission-control-421-co}

| Section|Recommendation|Manual/Automated|Level|Result |
| -- | -- | -- | -- | -- |
| 5.5.1|Configure Image Provenance using image controller configuration parameters. |Automated|2|Not checked |
{: caption="Benchmarks for extensible admission control." caption-side="top"}


### 5.7 General policies
{: #general-policies-421-co}

| Section|Recommendation|Manual/Automated|Level|Result |
| -- | -- | -- | -- | -- |
| 5.7.1|Create administrative boundaries between resources using namespaces. |Manual|1|Manual |
| 5.7.2|Ensure that the `seccomp` profile is set to docker/default in your pod definitions. |Manual|2|Manual |
| 5.7.3|Apply Security Context to Your Pods and Containers. |Manual|2|Manual |
| 5.7.4|The default namespace should not be used. |Manual|2|Manual |
{: caption="Benchmarks for general policies." caption-side="top"}

## {{site.data.keyword.IBM_notm}} remediations and explanations
{: #ibm-remediations-and-explanations-421-co}

Review information from {{site.data.keyword.IBM_notm}} on the CIS Benchmark results.

| Section | Recommendation/Explanation                                   |
| ------- | ------------------------------------------------------------ |
| 1.2.19 | Red Hat OpenShift on {{site.data.keyword.IBM_notm}} Cloud can optionally enable Kubernetes API server auditing. |
| 1.2.20 | Red Hat OpenShift on {{site.data.keyword.IBM_notm}} Cloud sets the `maximumRetainedFiles` argument to 1. |
| 1.2.29 | Red Hat OpenShift on {{site.data.keyword.IBM_notm}} Cloud can optionally enable a Kubernetes Key Management Service (KMS) provider. |
| 2.7 | Red Hat OpenShift on {{site.data.keyword.IBM_notm}} Cloud configures a unique Certificate Authority for etcd. |
| 5.2.8 | Red Hat OpenShift on {{site.data.keyword.IBM_notm}} Cloud installs custom `SCCs`. |
| 5.3.2 | Red Hat OpenShift on {{site.data.keyword.IBM_notm}} Cloud has a set of default Calico network policies defined and additional network policies can optionally be added. |
{: caption="Details for {{site.data.keyword.IBM_notm}} remediations and explanations." caption-side="top"}
