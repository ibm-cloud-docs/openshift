---

copyright: 
  years: 2023, 2026
lastupdated: "2026-01-09"

keywords: openshift, benchmarks, 4.14, openshift benchmarks, openshift 4.14, compliance operator, compliance

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}

# 4.14 compliance operator benchmark
{: #benchmarks-414-co}



This version is no longer supported. Update your cluster to a [supported version](/docs/openshift?topic=openshift-openshift_versions) as soon as possible.
{: important}



Review the compliance operator benchmark results for {{site.data.keyword.openshiftlong_notm}} version 4.14. 
{: shortdesc}

## 1 Control plane components
{: #Control-Plane-Components-414-co}

### 1.1 Master node configuration files
{: #Master-Node-Configuration-Files-414-co}

The master node configuration is not stored as a set of files; and therefore, rules in section 1.1 are out of the scope of the automated check by the compliance operator.

### 1.2 API server
{: #API-Server-414-co}


| Section|Recommendation|Manual/Automated|Level|Result |
| -- | -- | -- | -- | -- |
| 1.2.1|Ensure that anonymous requests are authorized. |Automated|1|Pass |
| 1.2.2|Ensure that the `--basic-auth-file` argument is not set. |Automated|1|Pass |
| 1.2.3|Ensure that the `--token-auth-file` parameter is not set. |Automated|1|Pass |
| 1.2.4|Use https for kubelet connections. |Automated|1|Pass |
| 1.2.5|Ensure that the kubelet uses certificates to authenticate. |Automated|1|Pass |
| 1.2.6|Verify that the kubelet certificate authority is set as appropriate. |Automated|1|Pass |
| 1.2.7|Ensure that the `--authorization-mode` argument is not set to `AlwaysAllow`. |Automated|1|Pass |
| 1.2.8|Verify that the Node authorizer is enabled. |Automated|1|Pass |
| 1.2.9|Verify that RBAC is enabled. |Automated|1|Pass |
| 1.2.10|Ensure that the `APIPriorityAndFairness` feature gate is enabled. |Manual|1|Pass |
| 1.2.11|Ensure that the admission control plug-in `AlwaysAdmit` is not set. |Automated|1|Pass |
| 1.2.12|Ensure that the admission control plug-in `AlwaysPullImages` is not set. |Automated|1|Pass |
| 1.2.13|Ensure that the admission control plug-in `SecurityContextDeny` is not set. |Automated|1|Pass |
| 1.2.14|Ensure that the admission control plug-in `ServiceAccount` is set. |Automated|1|Pass |
| 1.2.15|Ensure that the admission control plug-in `NamespaceLifecycle` is set. |Automated|1|Pass |
| 1.2.16|Ensure that the admission control plug-in `SecurityContextConstraint` is set. |Automated|1|Pass |
| 1.2.17|Ensure that the admission control plug-in `NodeRestriction` is set. |Automated|1|Pass |
| 1.2.18|Ensure that the `--insecure-bind-address` argument is not set. |Automated|1|Pass |
| 1.2.19|Ensure that the `--insecure-port` argument is set to 0. |Automated|1|Pass |
| 1.2.20|Ensure that the `--secure-port` argument is not set to 0. |Automated|1|MISSING |
| 1.2.21|Ensure that the `healthz` endpoint is protected by RBAC. |Automated|1|MISSING |
| 1.2.22|Ensure that the `--audit-log-path` argument is set. |Automated|1|Pass |
| 1.2.23|Ensure that the audit logs are forwarded off the cluster for retention. |Automated|1|[Not checked](#ibm-remediations-and-explanations-414-co) |
| 1.2.24|Ensure that the `maximumRetainedFiles` argument is set to `10` or as appropriate. |Automated|1|Pass |
| 1.2.25|Ensure that the `maximumFileSizeMegabytes` argument is set to `100` or as appropriate. |Automated|1|Pass |
| 1.2.26|Ensure that the `--request-timeout` argument is set as appropriate. |Automated|1|Pass |
| 1.2.27|Ensure that the `--service-account-lookup` argument is set to true. |Automated|1|Pass |
| 1.2.28|Ensure that the `--service-account-key-file` argument is set as appropriate. |Automated|1|Pass |
| 1.2.29|Ensure that the `--etcd-certfile` and `--etcd-keyfile` arguments are set as appropriate. |Automated|1|Pass |
| 1.2.30|Ensure that the `--tls-cert-file` and `--tls-private-key-file` arguments are set as appropriate. |Automated|1|Pass |
| 1.2.31|Ensure that the `--client-ca-file` argument is set as appropriate. |Automated|1|Pass |
| 1.2.32|Ensure that the `--etcd-cafile` argument is set as appropriate. |Automated|1|Pass |
| 1.2.33|Ensure that the `--encryption-provider-config` argument is set as appropriate. |Manual|1|[Not checked](#ibm-remediations-and-explanations-414-co) |
| 1.2.34|Ensure that encryption providers are appropriately configured. |Manual|1|[Not checked](#ibm-remediations-and-explanations-414-co) |
| 1.2.35|Ensure that the API Server only makes use of Strong Cryptographic Ciphers. |Manual|1|Pass |
{: caption="Section 1.2 API server benchmark results"}

### 1.3 Controller manager
{: #Controller-Manager-414-co}


| Section|Recommendation|Manual/Automated|Level|Result |
| -- | -- | -- | -- | -- |
| 1.3.1|Ensure that garbage collection is configured as appropriate. |Manual|1|Not checked |
| 1.3.2|Ensure that controller manager `healthz` endpoints are protected by RBAC. |Automated|1|MISSING |
| 1.3.3|Ensure that the `--use-service-account-credentials` argument is set to true. |Automated|1|Pass |
| 1.3.4|Ensure that the `--service-account-private-key-file` argument is set as appropriate. |Automated|1|Pass |
| 1.3.5|Ensure that the `--root-ca-file` argument is set as appropriate. |Automated|1|MISSING |
| 1.3.6|Ensure that the `RotateKubeletServerCertificate` argument is set to true. |Automated|2|Pass |
| 1.3.7|Ensure that the `--bind-address` argument is set to `127.0.0.1`. |Automated|1|Pass |
{: caption="Section 1.3 Controller manager benchmark results"}

### 1.4 Scheduler
{: #Scheduler-414-co}


| Section|Recommendation|Manual/Automated|Level|Result |
| -- | -- | -- | -- | -- |
| 1.4.1|Ensure that the `healthz` endpoints for the scheduler are protected by RBAC. |Automated|1|MISSING |
| 1.4.2|Verify that the scheduler API service is protected by authentication and authorization. |Automated|1|Pass |
{: caption="Section 1.4 Scheduler benchmark results"}

## 2 Etcd
{: #etcd-414-co}


| Section|Recommendation|Manual/Automated|Level|Result |
| -- | -- | -- | -- | -- |
| 2.1|Ensure that the `--cert-file` and `--key-file` arguments are set as appropriate. |Automated|1|Pass |
| 2.2|Ensure that the `--client-cert-auth` argument is set to true. |Automated|1|Pass |
| 2.3|Ensure that the `--auto-tls` argument is not set to true. |Automated|1|Pass |
| 2.4|Ensure that the `--peer-cert-file` and `--peer-key-file` arguments are set as appropriate. |Automated|1|Pass |
| 2.5|Ensure that the `--peer-client-cert-auth` argument is set to true. |Automated|1|Pass |
| 2.6|Ensure that the `--peer-auto-tls` argument is not set to true. |Automated|1|Pass |
| 2.7|Ensure that a unique Certificate Authority is used for etcd. |Manual|2|[Not checked](#ibm-remediations-and-explanations-414-co) |
{: caption="Section 2 etcd benchmark results"}

## 3 Control plane configuration
{: #Control-Plane-Configuration-414-co}

### 3.1 Authentication and authorization
{: #Authentication-and-Authorization-414-co}


| Section|Recommendation|Manual/Automated|Level|Result |
| -- | -- | -- | -- | -- |
| 3.1.1|Client certificate authentication should not be used for users. |Manual|2|Pass |
{: caption="Section 3.1 Authentication and Authorization benchmark results"}

### 3.2 Logging
{: #Logging-414-co}


| Section|Recommendation|Manual/Automated|Level|Result |
| -- | -- | -- | -- | -- |
| 3.2.1|Ensure that a minimal audit policy is created. |Automated|1|Pass |
| 3.2.2|Ensure that the audit policy covers key security concerns. |Manual|2|Pass |
{: caption="Section 3.3 Logging benchmark results"}

## 4 Worker nodes
{: #Worker-Nodes-414-co}

Follow the instruction in [Using the compliance operator](/docs/openshift?topic=openshift-compliance-operator) to perform automated check for worker node configuration.



## 5 Policies
{: #Policies-414-co}

### 5.1 RBAC and service accounts
{: #RBAC-and-Service-Accounts-414-co}


| Section|Recommendation|Manual/Automated|Level|Result |
| -- | -- | -- | -- | -- |
| 5.1.1|Ensure that the cluster-admin role is only used where required. |Manual|1|Pass |
| 5.1.2|Minimize access to secrets. |Manual|1|Not checked |
| 5.1.3|Minimize wildcard use in `Roles` and `ClusterRoles`. |Manual|1|Not checked |
| 5.1.4|Minimize access to create pods. |Manual|1|Not checked |
| 5.1.5|Ensure that default service accounts are not actively used. |Automated|1|Not checked |
| 5.1.6|Ensure that Service Account Tokens are only mounted where necessary. |Manual|1|Not checked |
{: caption="Section 5.1 RBAC and Service Accounts benchmark results"}

### 5.2 Pod security policies
{: #Pod-Security-Policies-414-co}


| Section|Recommendation|Manual/Automated|Level|Result |
| -- | -- | -- | -- | -- |
| 5.2.1|Minimize the admission of privileged containers. |Manual|1|Not checked |
| 5.2.2|Minimize the admission of containers wishing to share the host process ID namespace. |Automated|1|Not checked |
| 5.2.3|Minimize the admission of containers wishing to share the host IPC namespace. |Automated|1|Not checked |
| 5.2.4|Minimize the admission of containers wishing to share the host network namespace. |Automated|1|Not checked |
| 5.2.5|Minimize the admission of containers with `allowPrivilegeEscalation`. |Automated|1|Not checked |
| 5.2.6|Minimize the admission of root containers. |Manual|2|Not checked |
| 5.2.7|Minimize the admission of containers with the NET_RAW capability. |Manual|1|Not checked |
| 5.2.8|Minimize the admission of containers with added capabilities. |Manual|1|[Not checked](#ibm-remediations-and-explanations-414-co) |
| 5.2.9|Minimize the admission of containers with capabilities assigned. |Manual|2|Not checked |
{: caption="Section 5.2 Pod Security Policies benchmark results"}

### 5.3 Network policies and CNI
{: #Network-Policies-and-CNI-414-co}


| Section|Recommendation|Manual/Automated|Level|Result |
| -- | -- | -- | -- | -- |
| 5.3.1|Ensure that the CNI in use supports Network Policies. |Manual|1|Pass |
| 5.3.2|Ensure that all Namespaces have Network Policies defined. |Automated|2|[Not checked](#ibm-remediations-and-explanations-414-co) |
{: caption="Section 5.3 Network policies and CNI benchmark results"}

### 5.4 Secrets management
{: #Secrets-Management-414-co}


| Section|Recommendation|Manual/Automated|Level|Result |
| -- | -- | -- | -- | -- |
| 5.4.1|Prefer using secrets as files over secrets as environment variables. |Manual|1|Not checked |
| 5.4.2|Consider external secret storage. |Manual|2|Not checked |
{: caption="Section 5.4 Secrets management benchmark results"}

### 5.5 Extensible admission control
{: #Extensible-Admission-Control-414-co}


| Section|Recommendation|Manual/Automated|Level|Result |
| -- | -- | -- | -- | -- |
| 5.5.1|Configure Image Provenance using image controller configuration parameters. |Manual|2|Not checked |
{: caption="Section 5.5 Extensible admission control benchmark results"}

### 5.7 General policies
{: #General-Policies-414-co}


| Section|Recommendation|Manual/Automated|Level|Result |
| -- | -- | -- | -- | -- |
| 5.7.1|Create administrative boundaries between resources using namespaces. |Manual|1|Not checked |
| 5.7.2|Ensure that the `seccomp` profile is set to docker/default in your pod definitions. |Manual|2|Not checked |
| 5.7.3|Apply Security Context to Your Pods and Containers. |Manual|2|Not checked |
| 5.7.4|The default namespace should not be used. |Automated|2|Not checked |
{: caption="Section 5.7 General policies benchmark results"}

## IBM remediations and explanations
{: #ibm-remediations-and-explanations-414-co}

Review information from {{site.data.keyword.IBM_notm}} on the CIS Benchmark results.

| Section | Recommendation/Explanation |
| --- | --- |
| 1.2.23 | Red Hat OpenShift on {{site.data.keyword.IBM_notm}} Cloud can optionally enable Kubernetes API server auditing. |
| 1.2.33 | Red Hat OpenShift on {{site.data.keyword.IBM_notm}} Cloud can optionally enable a Kubernetes Key Management Service (KMS) provider. |
| 1.2.34 | Red Hat OpenShift on {{site.data.keyword.IBM_notm}} Cloud can optionally enable a Kubernetes Key Management Service (KMS) provider. |
| 2.7 | Red Hat OpenShift on {{site.data.keyword.IBM_notm}} Cloud configures a unique Certificate Authority for etcd. |
| 5.2.8 | Red Hat OpenShift on {{site.data.keyword.IBM_notm}} Cloud installs custom `SCCs`. |
| 5.3.2 | Red Hat OpenShift on {{site.data.keyword.IBM_notm}} Cloud has a set of default Calico network policies defined and additional network policies can optionally be added. |
{: caption="Remediations and explanations"}
