---

copyright: 
  years: 2022, 2022
lastupdated: "2022-07-14"

keywords: openshift, benchmarks, 4.9, compliance operator, compliance

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}


# {{site.data.keyword.openshiftlong_notm}} version 4.9 compliance operator benchmark
{: #benchmarks_49_co}




## 1 Control plane components
{: #co-benchmark-49-cp}

### 1.1 Master node configuration files
{: #co-benchmark-49-11}

Master node configuration is not stored as a set of files, and
therefore rules in section 1.1 are out of the scope of automated
check by Compliance Operator.

### 1.2 API server
{: #co-benchmark-49-12}

| Section|Recommendation|Manual/Automated|Level|Result |
| -- | -- | -- | -- | -- |
| 1.2.1|Ensure that anonymous requests are authorized. |Manual|1|Pass |
| 1.2.2|Ensure that the `--basic-auth-file` option is not set. |Automated|1|Pass |
| 1.2.3|Ensure that the `--token-auth-file` parameter is not set. |Automated|1|Pass |
| 1.2.4|Use `https` for kubelet connections. |Automated|1|[FAIL](#co-benchmark-49-remdiations) |
| 1.2.5|Ensure that the kubelet uses certificates to authenticate. |Automated|1|Pass |
| 1.2.6|Verify that the kubelet certificate authority is set as appropriate. |Automated|1|Pass |
| 1.2.7|Ensure that the `--authorization-mode` option is not set to `AlwaysAllow`. |Automated|1|Pass |
| 1.2.8|Verify that the Node authorizer is enabled. |Automated|1|Pass |
| 1.2.9|Verify that RBAC is enabled. |Automated|1|Pass |
| 1.2.10|Ensure that the `APIPriorityAndFairness` feature gate is enabled. |Manual|1|Pass |
| 1.2.11|Ensure that the admission control plug-in `AlwaysAdmit` is not set. |Automated|1|Pass |
| 1.2.12|Ensure that the admission control plug-in `AlwaysPullImages` is not set. |Manual|1|Pass |
| 1.2.13|Ensure that the admission control plug-in `SecurityContextDeny` is not set. |Manual|1|Pass |
| 1.2.14|Ensure that the admission control plug-in `ServiceAccount` is set. |Automated|1|Pass |
| 1.2.15|Ensure that the admission control plug-in `NamespaceLifecycle` is set. |Automated|1|Pass |
| 1.2.16|Ensure that the admission control plug-in `SecurityContextConstraint` is set. |Automated|1|Pass |
| 1.2.17|Ensure that the admission control plug-in `NodeRestriction` is set. |Automated|1|Pass |
| 1.2.18|Ensure that the `--insecure-bind-address` option is not set. |Automated|1|Pass |
| 1.2.19|Ensure that the `--insecure-port option` is set to `0`. |Automated|1|[Not checked](#co-benchmark-49-remdiations) |
| 1.2.20|Ensure that the `--secure-port option` is not set to `0`. |Automated|1|Pass |
| 1.2.21|Ensure that the `healthz` endpoint is protected by RBAC. |Automated|1|Pass |
| 1.2.22|Ensure that the `--audit-log-path` option is set. |Automated|1|Pass |
| 1.2.23|Ensure that the audit logs are forwarded off the cluster for retention. |Automated|1|[Not checked](#co-benchmark-49-remdiations) |
| 1.2.24|Ensure that the `maximumRetainedFiles` option is set to `10` or as appropriate. |Automated|1|Pass |
| 1.2.25|Ensure that the `maximumFileSizeMegabytes` option is set to `100` or as appropriate. |Automated|1|Pass |
| 1.2.26|Ensure that the `--request-timeout` option is set as appropriate. |Automated|1|Pass |
| 1.2.27|Ensure that the `--service-account-lookup` option is set to `true`. |Automated|1|Pass |
| 1.2.28|Ensure that the `--service-account-key-file` option is set as appropriate. |Automated|1|Pass |
| 1.2.29|Ensure that the `--etcd-certfile` and `--etcd-keyfile` options are set as appropriate. |Automated|1|Pass |
| 1.2.30|Ensure that the `--tls-cert-file` and `--tls-private-key-file` options are set as appropriate. |Automated|1|Pass |
| 1.2.31|Ensure that the `--client-ca-file` option is set as appropriate. |Automated|1|Pass |
| 1.2.32|Ensure that the `--etcd-cafile` option is set as appropriate. |Automated|1|Pass |
| 1.2.33|Ensure that the `--encryption-provider-config` option is set as appropriate. |Manual|1|[Not checked](#co-benchmark-49-remdiations) |
| 1.2.34|Ensure that encryption providers are appropriately configured. |Manual|1|[Not checked](#co-benchmark-49-remdiations) |
| 1.2.35|Ensure that the API Server makes use of only Strong Cryptographic Ciphers. |Manual|1|Pass |
{: caption="Section 1.2 API server benchmark results" caption-side="top"}

### 1.3 Controller manager
{: #co-benchmark-49-11}

| Section|Recommendation|Manual/Automated|Level|Result |
| -- | -- | -- | -- | -- |
| 1.3.1|Ensure that garbage collection is configured as appropriate. |Manual|1|Not checked |
| 1.3.2|Ensure that controller manager healthz endpoints are protected by RBAC. |Automated|1|Pass |
| 1.3.3|Ensure that the `--use-service-account-credentials` option is set to `true`. |Automated|1|Pass |
| 1.3.4|Ensure that the `--service-account-private-key-file` option is set as appropriate. |Automated|1|Pass |
| 1.3.5|Ensure that the `--root-ca-file option` is set as appropriate. |Automated. |1|Pass |
| 1.3.6|Ensure that the `RotateKubeletServerCertificate` option is set to `true`. |Automated|2|Pass |
| 1.3.7|Ensure that the `--bind-address` option is set to `127.0.0.1`. |Automated |1|Pass |
{: caption="Section 1.3 Controller manager benchmark results" caption-side="top"}


### 1.4 Scheduler
{: #co-benchmark-49-11}

| Section|Recommendation|Manual/Automated|Level|Result |
| -- | -- | -- | -- | -- |
| 1.4.1|Ensure that the healthz endpoints for the scheduler are protected by RBAC. |Automated|1|Pass |
| 1.4.2|Verify that the scheduler API service is protected by authentication and authorization. |Automated|1|Pass |
{: caption="Section 1.4 Scheduler benchmark results" caption-side="top"}


## 2 etcd
{: #co-benchmark-49-2}

| Section|Recommendation|Manual/Automated|Level|Result |
| -- | -- | -- | -- | -- |
| 2.1|Ensure that the `--cert-file` and `--key-file` options are set as appropriate. |Automated|1|Pass |
| 2.2|Ensure that the `--client-cert-auth` option is set to `true`. |Automated|1|Pass |
| 2.3|Ensure that the `--auto-tls option` is not set to `true`. |Automated|1|Pass |
| 2.4|Ensure that the `--peer-cert-file` and --peer-key-file options are set as appropriate. |Automated|1|Pass |
| 2.5|Ensure that the `--peer-client-cert-auth option` is set to `true`. |Automated|1|Pass |
| 2.6|Ensure that the `--peer-auto-tls` option is not set to `true`. |Automated|1|Pass |
| 2.7|Ensure that a unique certificate authority is used for etcd. |Manual|2|[Not checked](#co-benchmark-49-remdiations) |
{: caption="Section 2 etcd benchmark results" caption-side="top"}

## 3 Control plane configuration
{: #co-benchmark-49-3}

### 3.1 Authentication and authorization
{: #co-benchmark-49-31}

| Section|Recommendation|Manual/Automated|Level|Result |
| -- | -- | -- | -- | -- |
| 3.1.1|Do not use client certificate authentication for users.|Manual|2|Pass |
{: caption="Section 3.1 Authentication and Authorization benchmark results" caption-side="top"}


### 3.2 Logging
{: #co-benchmark-49-32}

| Section|Recommendation|Manual/Automated|Level|Result |
| -- | -- | -- | -- | -- |
| 3.2.1|Ensure that a minimal audit policy is created. |Automated|1|Pass |
| 3.2.2|Ensure that the audit policy covers key security concerns. |Manual|2|Pass |
{: caption="Section 3.3 Logging benchmark results" caption-side="top"}

## 4 Worker nodes
{: #co-benchmark-49-4}

Follow the instruction in [Using the compliance operator](/docs/openshift?topic=openshift-compliance-operator) to perform automated check for worker node configuration.


## 5 Policies
{: #co-benchmark-49-5}

### 5.1 RBAC and service accounts
{: #co-benchmark-49-51}

| Section|Recommendation|Manual/Automated|Level|Result |
| -- | -- | -- | -- | -- |
| 5.1.1|Ensure that the `cluster-admin` role is only used where required. |Manual|1|Fail |
| 5.1.2|Minimize access to secrets. |Manual|1|Fail |
| 5.1.3|Minimize wildcard use in Roles and `ClusterRoles`. |Manual|1|Fail |
| 5.1.4|Minimize access to create pods. |Manual|1|Fail |
| 5.1.5|Ensure that default service accounts are not actively used. |Automated|1|Fail |
| 5.1.6|Ensure that Service Account Tokens are mounted only where necessary. |Manual|1|Fail |
{: caption="Section 5.1 RBAC and Service Accounts benchmark results" caption-side="top"}


### 5.2 Pod Security Policies
{: #co-benchmark-49-52}

| Section|Recommendation|Manual/Automated|Level|Result |
| -- | -- | -- | -- | -- |
| 5.2.1|Minimize the admission of privileged containers|Manual|1|Fail |
| 5.2.2|Minimize the admission of containers wanting to share the host process ID namespace|Automated|1|Fail |
| 5.2.3|Minimize the admission of containers wanting to share the host IPC namespace|Automated|1|Fail |
| 5.2.4|Minimize the admission of containers wanting to share the host network namespace|Automated|1|Fail |
| 5.2.5|Minimize the admission of containers with `allowPrivilegeEscalation`.|Automated|1|Fail |
| 5.2.6|Minimize the admission of root containers|Manual|2|Fail |
| 5.2.7|Minimize the admission of containers with the `NET_RAW` capability|Manual|1|Fail |
| 5.2.8|Minimize the admission of containers with added capabilities|Manual|1|[Not checked](#co-benchmark-49-remdiations) |
| 5.2.9|Minimize the admission of containers with capabilities assigned|Manual|2|Fail |
{: caption="Section 5.2 Pod Security Policies benchmark results" caption-side="top"}


### 5.3 Network policies and CNI
{: #co-benchmark-49-53}

| Section|Recommendation|Manual/Automated|Level|Result |
| -- | -- | -- | -- | -- |
| 5.3.1|Ensure that the CNI in use supports network policies.|Manual|1|[Not checked](#co-benchmark-49-remdiations) |
| 5.3.2|Ensure that all namespaces define network policies.|Automated|2|[Not checked](#co-benchmark-49-remdiations) |
{: caption="Section 5.3 Network policies and CNI benchmark results" caption-side="top"}

### 5.4 Secrets management
{: #co-benchmark-49-54}

| Section|Recommendation|Manual/Automated|Level|Result |
| -- | -- | -- | -- | -- |
| 5.4.1|Prefer using secrets as files over secrets as environment variables. |Manual|1|Fail |
| 5.4.2|Consider external secret storage. |Manual|2|Fail |
{: caption="Section 5.4 Secrets management benchmark results" caption-side="top"}


### 5.5 Extensible admission control
{: #co-benchmark-49-55}

| Section|Recommendation|Manual/Automated|Level|Result |
| -- | -- | -- | -- | -- |
| 5.5.1|Configure image provenance by using image controller configuration parameters. |Manual|2|Fail |
{: caption="Section 5.5 Extensible admission control benchmark results" caption-side="top"}

### 5.7 General policies
{: #co-benchmark-49-57}

| Section|Recommendation|Manual/Automated|Level|Result |
| -- | -- | -- | -- | -- |
| 5.7.1|Create administrative boundaries between resources by using namespaces. |Manual|1|Not checked |
| 5.7.2|Ensure that the seccomp profile is set to `docker/default` in your pod definitions. |Manual|2|Not checked |
| 5.7.3|Apply security context to your pods and containers. |Manual|2|Not checked |
| 5.7.4|Do not use the default namespace. |Automated|2|Not checked |
{: caption="Section 5.7 General policies benchmark results" caption-side="top"}

## {{site.data.keyword.IBM_notm}} Remediations and explanations
{: #co-benchmark-49-remdiations}

Review information from {{site.data.keyword.cloud_notm}} about the CIS Benchmark results.

| Section | Recommendation/Explanation |
| --- | --- |
| 1.2.4 | {{site.data.keyword.openshiftshort}} configures the {{site.data.keyword.cloud_notm}} IAM identity provider by default. |
| 1.2.19 | Fix is coming with https://github.com/ComplianceAsCode/content/pull/8995. |
| 1.2.23 | {{site.data.keyword.openshiftshort}} can optionally enable Kubernetes API server auditing. |
| 1.2.33 | {{site.data.keyword.openshiftshort}} can optionally enable a Kubernetes Key Management Service (KMS) provider. |
| 1.2.34 | {{site.data.keyword.openshiftshort}} can optionally enable a Kubernetes Key Management Service (KMS) provider. |
| 2.7 | {{site.data.keyword.openshiftshort}} configures a unique certificate authority for etcd. |
| 5.2.8 | {{site.data.keyword.openshiftshort}} installs custom SCCs. |
| 5.3.1 | Review the [issue in GitHub](https://github.com/ComplianceAsCode/content/issues/9047){: external}. |
| 5.3.2 | {{site.data.keyword.openshiftshort}} defines a set of default Calico network policies and additional network policies can optionally be added. |
{: caption="Remediations and explanations" caption-side="top"}
