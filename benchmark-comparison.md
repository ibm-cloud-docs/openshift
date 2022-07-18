---

copyright: 
  years: 2022, 2022
lastupdated: "2022-07-18"

keywords: openshift

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}



# Comparing the CIS Kubernetes and the compliance operator benchmarks
{: #benchmark-comparison}

Review the following tables for an overview of the differences between the CIS Kubernetes and the compliance operator benchmarks.
{: shortdesc}

## Major differences
{: #benchmark-comparison-major}

| Section | CIS Kubernetes Benchmark| Compliance Operator Benchmark| Description |
| ---| --- | --- | --- |
| 1.2.1 | Ensure that the `--anonymous-auth` option is set to `false`. | Ensure that anonymous requests are authorized. | Different approaches to acheive the same purpose. |
| 1.2.10 | Ensure that the admission control plug-in `EventRateLimit` is set. | Ensure that the `APIPriorityAndFairness` feature gate is enabled. | Different approaches to achieve the same purpose.|
| 1.2.12 | Ensure that the admission control plug-in `AlwaysPullImages` is set. | Ensure that the admission control plug-in `AlwaysPullImages` is not set | `AlwaysPullImages` causes error on OpenShift. |
| 1.2.13 | Ensure that the admission control plug-in `SecurityContextDeny` is set if PodSecurityPolicy is not used. | Ensure that the admission control plugin `SecurityContextDeny` is not set | `SecurityContextDeny` admission controller can't be enabled as it conflicts with the `SecurityContextConstraint` admission controller. |
| 1.2.16 | Ensure that the admission control plug-in `PodSecurityPolicy` is set. | Ensure that the admission control plug-in `SecurityContextConstraint` is set. | `SecurityContextConstraint` is unique to OpenShift |
| 1.2.21 | Ensure that the `--profiling` option is set to `false`. | Ensure that the healthz endpoint is protected by RBAC. | Profiling is enabled by default in OpenShift, but the profiling data is sent through the healthz port and the port must be protected by RBAC. |
| 1.2.23 | Ensure that the `--audit-log-maxage` option is set to `30` or as appropriate. | Ensure that the audit logs are forwarded off the cluster for retention. | OpenShift has an operator for logging instead of retaining logs in the cluster. |
| 1.2.24 | Ensure that the `--audit-log-maxbackup` option is set to `10` or as appropriate. | Ensure that the `maximumRetainedFiles` option is set to `10` or as appropriate. | Different parameter names. |
| 1.2.25 | Ensure that the `--audit-log-maxsize` option is set to `100` or as appropriate. | Ensure that the `maximumFileSizeMegabytes` option is set to `100` or as appropriate. | Different parameter names. |
| 1.3.1 | Ensure that the `--terminated-pod-gc-threshold` option is set as appropriate. | Ensure that garbage collection is configured as appropriate. | Different parameter names. |
| 1.3.2 | Ensure that the `--profiling` option is set to `false`. | Ensure that controller manager healthz endpoints are protected by RBAC. | Profiling is enabled by default in OpenShift, but the profiling data is sent through the  healthz port and the port must be protected by RBAC. |
| 1.4.1 | Ensure that the `--profiling` option is set to `false`. | Ensure that the healthz endpoints for the scheduler are protected by RBAC. | Profiling is enabled by default in OpenShift, but the profiling data is sent via healthz port and the port must be protected by RBAC. |
| 1.4.2 | Ensure that the `--bind-address` option is set to `127.0.0.1`. | Verify that the scheduler API service is protected by authentication and authorization. | OpenShift has different operator than vanilla kubernetes, and configuration for its security differs |
| 4.1.3 | Ensure that the proxy kubeconfig file permissions are set to `644` or more restrictive. | **If proxy kubeconfig file exists**, ensure permissions are set to 644 or more restrictive. | In OpenShift, the file is automatically created by `sdn` controller in a secure manner. |
| 4.1.4 | Ensure that the proxy kubeconfig file ownership is set to `root:root`. | **If proxy kubeconfig file exists**, ensure ownership is set to `root:root` | In OpenShift, the file is automatically created by `sdn` controller in a secure manner. |
{: caption="Major difference between the CIS Kubernetes Benchmark and the OpenShift Compliance Operator Benchmark" caption-side="top"}

## Minor differences
{: #benchmark-comparison-minor}

| Section | CIS Kubernetes Benchmark| CIS Kubernetes Benchmark| Description |
| ---| --- | --- | --- |
| 1.1.19 | Ensure that the Kubernetes PKI directory and file ownership is set to `root:root`. | Ensure that the OpenShift PKI directory and file ownership is set to `root:root`. | Kubernetes > OpenShift |
| 1.1.20 | Ensure that the Kubernetes PKI certificate file permissions are set to `644` or more restrictive. | Ensure that the OpenShift PKI certificate file permissions are set to 644 or more restrictive | Kubernetes > OpenShift |
| 1.1.21 | Ensure that the Kubernetes PKI key file permissions are set to 600 | Ensure that the OpenShift PKI key file permissions are set to 600 | Kubernetes > OpenShift |
| 1.2.4 | Ensure that the `--kubelet-https` option is set to `true` | Use https for kubelet connections. | No option specified for OpenShift. |
| 1.2.5 | Ensure that the `--kubelet-client-certificate` and `--kubelet-client-key` options are set as appropriate. | Ensure that the kubelet uses certificates to authenticate | No option specified for OpenShift. |
| 1.2.6 | Ensure that the `--kubelet-certificate-authority` option is set as appropriate. | Verify that the kubelet certificate authority is set as appropriate | No option specified for OpenShift. |
| 1.2.8 | Ensure that the `--authorization-mode` option includes Node. | Verify that the Node authorizer is enabled | No option specified for OpenShift. |
| 1.2.9 | Ensure that the `--authorization-mode` option includes RBAC. | Verify that RBAC is enabled | No option specified for OpenShift. |
| 4.1.5 | Ensure that the kubelet.conf file permissions are set to 644 or more restrictive. | Ensure that the `--kubeconfig kubelet.conf` file permissions are set to `644` or more restrictive. | Different wording for the same approach. |
| 4.1.6 | Ensure that the kubelet.conf file ownership is set to `root:root`. | Ensure that the `--kubeconfig kubelet.conf` file ownership is set to `root:root`. | Different wording for the same approach. |
| 4.1.9 | Ensure that the kubelet configuration file has permissions set to 644 or more restrictive. | Ensure that the kubelet `--config` configuration file has permissions set to `644` or more restrictive. | Different wording for the same approach. |
{: caption="Minor difference between the CIS Kubernetes Benchmark and the OpenShift Compliance Operator Benchmark" caption-side="top"}
