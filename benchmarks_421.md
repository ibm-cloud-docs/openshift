---

copyright: 
  years: 2026, 2026
lastupdated: "2026-05-18"

keywords: openshift, benchmarks, 4.21, openshift benchmarks, openshift 4.21

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}

# 4.21 CIS Kubernetes benchmark
{: #cis-benchmark-421}

The Center for Internet Security (CIS) publishes the [CIS Kubernetes Benchmark](https://www.cisecurity.org/benchmark/kubernetes/){: external} as a framework of specific steps to configure Kubernetes more securely and with standards that are commensurate to various industry regulations. This document contains the results of the version 1.5 CIS Kubernetes benchmark for clusters that run {{site.data.keyword.openshiftlong_notm}} version 4.21. For more information or help understanding the benchmark, see [Using the benchmark](/docs/openshift?topic=openshift-cis-benchmark).
{: shortdesc}


## 1 Master node security configuration
{: #1-master-node-security-configuration-421}

### 1.1 Master node configuration files
{: #11-master-node-configuration-files-421}

| Section | Recommendation. | Scored? | Level | Result | Responsibility |
| ------ | -------------------------------------------------------------------------------------------------------- | ----------------- | ----- | ------ | -------------- |
| 1.1.1  | Ensure that the API server pod specification file permissions are set to `600` or more restrictive. | Scored            | 1     | Pass   | {{site.data.keyword.IBM_notm}}            |
| 1.1.2  | Ensure that the API server pod specification file ownership is set to `root:root`. | Scored            | 1     | Pass   | {{site.data.keyword.IBM_notm}}            |
| 1.1.3  | Ensure that the controller manager pod specification file permissions are set to `600` or more restrictive. | Scored            | 1     | Pass   | {{site.data.keyword.IBM_notm}}            |
| 1.1.4  | Ensure that the controller manager pod specification file ownership is set to `root:root`. | Scored            | 1     | Pass   | {{site.data.keyword.IBM_notm}}            |
| 1.1.5  | Ensure that the scheduler pod specification file permissions are set to `600` or more restrictive. | Scored            | 1     | Pass   | {{site.data.keyword.IBM_notm}}            |
| 1.1.6  | Ensure that the scheduler pod specification file ownership is set to `root:root`. | Scored            | 1     | Pass   | {{site.data.keyword.IBM_notm}}            |
| 1.1.7  | Ensure that the etcd pod specification file permissions are set to `600` or more restrictive. | Scored            | 1     | Pass   | {{site.data.keyword.IBM_notm}}            |
| 1.1.8  | Ensure that the etcd pod specification file ownership is set to `root:root`. | Scored            | 1     | Pass   | {{site.data.keyword.IBM_notm}}            |
| 1.1.9  | Ensure that the Container Network Interface file permissions are set to `600` or more restrictive. | Not Scored        | 1     | Pass   | {{site.data.keyword.IBM_notm}}            |
| 1.1.10 | Ensure that the Container Network Interface file ownership is set to `root:root`. | Not Scored        | 1     | Pass   | {{site.data.keyword.IBM_notm}}            |
| 1.1.11 | Ensure that the etcd data directory permissions are set to `700` or more restrictive. | Scored            | 1     | Pass   | {{site.data.keyword.IBM_notm}}            |
| 1.1.12 | Ensure that the etcd data directory ownership is set to `etcd:etcd`. | Scored            | 1     | Pass   | {{site.data.keyword.IBM_notm}}            |
| 1.1.13 | Ensure that the default administrative credential file permissions are set to `600`. | Scored            | 1     | Pass   | {{site.data.keyword.IBM_notm}}            |
| 1.1.14 | Ensure that the default administrative credential file ownership is set to `root:root`. | Scored            | 1     | Pass   | {{site.data.keyword.IBM_notm}}            |
| 1.1.15 | Ensure that the `scheduler.conf` file permissions are set to `600` or more restrictive. | Scored            | 1     | Pass   | {{site.data.keyword.IBM_notm}}            |
| 1.1.16 | Ensure that the `scheduler.conf` file ownership is set to `root:root`. | Scored            | 1     | Pass   | {{site.data.keyword.IBM_notm}}            |
| 1.1.17 | Ensure that the `controller-manager.conf` file permissions are set to `600` or more restrictive. | Scored            | 1     | Pass   | {{site.data.keyword.IBM_notm}}            |
| 1.1.18 | Ensure that the `controller-manager.conf` file ownership is set to `root:root`. | Scored            | 1     | Pass   | {{site.data.keyword.IBM_notm}}            |
| 1.1.19 | Ensure that the Kubernetes PKI directory and file ownership is set to `root:root`. | Scored            | 1     | Pass   | {{site.data.keyword.IBM_notm}}            |
| 1.1.20 | Ensure that the Kubernetes PKI certificate file permissions are set to `644` or more restrictive. | Not Scored        | 1     | Pass   | {{site.data.keyword.IBM_notm}}            |
| 1.1.21 | Ensure that the Kubernetes PKI key file permissions are set to `600`. | Not Scored        | 1     | Pass   | {{site.data.keyword.IBM_notm}}            |
{: caption="Section 1.1 Master node configuration files benchmark results" caption-side="bottom"}

### 1.2 API server
{: #12-api-server-421}

| Section | Recommendation. | Scored? | Level | Result                                     | Responsibility |
| ------ | ------------------------------------------------------------------------------------------------------ | ----------------- | ----- | ------------------------------------------ | -------------- |
| 1.2.1  | Ensure that the `--anonymous-auth` argument is set to `false`. | Not Scored        | 1     | [Fail](#ibm-remediations-and-explanations-421) | {{site.data.keyword.IBM_notm}}            |
| 1.2.2  | Ensure that the `--token-auth-file` parameter is not set. | Scored            | 1     | Pass                                       | {{site.data.keyword.IBM_notm}}            |
| 1.2.3  | Ensure that the `DenyServiceExternalIPs` is set. | Not Scored        | 1     | [Fail](#ibm-remediations-and-explanations-421) | {{site.data.keyword.IBM_notm}}            |
| 1.2.4  | Ensure that the `--kubelet-client-certificate` and `--kubelet-client-key` arguments are set as appropriate. | Scored            | 1     | Pass                                       | {{site.data.keyword.IBM_notm}}            |
| 1.2.5  | Ensure that the `--kubelet-certificate-authority` argument is set as appropriate. | Scored            | 1     | Pass                                       | {{site.data.keyword.IBM_notm}}            |
| 1.2.6  | Ensure that the `--authorization-mode` argument is not set to `AlwaysAllow`. | Scored            | 1     | Pass                                       | {{site.data.keyword.IBM_notm}}            |
| 1.2.7  | Ensure that the `--authorization-mode` argument includes Node. | Scored            | 1     | Pass                                       | {{site.data.keyword.IBM_notm}}            |
| 1.2.8  | Ensure that the `--authorization-mode` argument includes RBAC. | Scored            | 1     | Pass                                       | {{site.data.keyword.IBM_notm}}            |
| 1.2.9  | Ensure that the admission control plug-in `EventRateLimit` is set. | Not Scored        | 1     | [Fail](#ibm-remediations-and-explanations-421) | {{site.data.keyword.IBM_notm}}            |
| 1.2.10 | Ensure that the admission control plug-in `AlwaysAdmit` is not set. | Scored            | 1     | Pass                                       | {{site.data.keyword.IBM_notm}}            |
| 1.2.11 | Ensure that the admission control plug-in `AlwaysPullImages` is set. | Not Scored        | 1     | [Fail](#ibm-remediations-and-explanations-421) | {{site.data.keyword.IBM_notm}}            |
| 1.2.12 | Ensure that the admission control plug-in `ServiceAccount` is set. | Scored            | 2     | Pass                                       | {{site.data.keyword.IBM_notm}}            |
| 1.2.13 | Ensure that the admission control plug-in `NamespaceLifecycle` is set. | Scored            | 2     | Pass                                       | {{site.data.keyword.IBM_notm}}            |
| 1.2.14 | Ensure that the admission control plug-in `NodeRestriction` is set. | Scored            | 2     | Pass                                       | {{site.data.keyword.IBM_notm}}            |
| 1.2.15 | Ensure that the `--profiling` argument is set to `false`. | Scored            | 1     | Pass                                       | {{site.data.keyword.IBM_notm}}            |
| 1.2.16 | Ensure that the `--audit-log-path` argument is set. | Scored            | 1     | Pass                                       | Shared         |
| 1.2.17 | Ensure that the `--audit-log-maxage` argument is set to `30` or as appropriate. | Scored            | 1     | [Fail](#ibm-remediations-and-explanations-421) | Shared         |
| 1.2.18 | Ensure that the `--audit-log-maxbackup` argument is set to `10` or as appropriate. | Scored            | 1     | Pass                                       | Shared         |
| 1.2.19 | Ensure that the `--audit-log-maxsize` argument is set to `100` or as appropriate. | Scored            | 1     | Pass                                       | Shared         |
| 1.2.20 | Ensure that the `--request-timeout` argument is set as appropriate. | Not Scored        | 1     | Pass                                       | {{site.data.keyword.IBM_notm}}            |
| 1.2.21 | Ensure that the `--service-account-lookup` argument is set to `true`. | Scored            | 1     | Pass                                       | {{site.data.keyword.IBM_notm}}            |
| 1.2.22 | Ensure that the `--service-account-key-file` argument is set as appropriate. | Scored            | 1     | Pass                                       | {{site.data.keyword.IBM_notm}}            |
| 1.2.23 | Ensure that the `--etcd-certfile` and `--etcd-keyfile` arguments are set as appropriate. | Scored            | 1     | Pass                                       | {{site.data.keyword.IBM_notm}}            |
| 1.2.24 | Ensure that the `--tls-cert-file` and `--tls-private-key-file` arguments are set as appropriate. | Scored            | 1     | Pass                                       | {{site.data.keyword.IBM_notm}}            |
| 1.2.25 | Ensure that the `--client-ca-file` argument is set as appropriate. | Scored            | 1     | Pass                                       | {{site.data.keyword.IBM_notm}}            |
| 1.2.26 | Ensure that the `--etcd-cafile` argument is set as appropriate. | Scored            | 1     | Pass                                       | {{site.data.keyword.IBM_notm}}            |
| 1.2.27 | Ensure that the `--encryption-provider-config` argument is set as appropriate. | Not Scored        | 1     | [Fail](#ibm-remediations-and-explanations-421) | Shared         |
| 1.2.28 | Ensure that encryption providers are appropriately configured. | Not Scored        | 1     | [Fail](#ibm-remediations-and-explanations-421) | Shared         |
| 1.2.29 | Ensure that the API Server only makes use of Strong Cryptographic Ciphers. | Not Scored        | 1     | Pass                                       | {{site.data.keyword.IBM_notm}}            |
| 1.2.30 | Ensure that the `--service-account-extend-token-expiration` parameter is set to `false`. | Scored            | 1     | [Fail](#ibm-remediations-and-explanations-421) | {{site.data.keyword.IBM_notm}}            |
{: caption="Section 1.2 API server benchmark results" caption-side="bottom"}

### 1.3 Controller manager
{: #13-controller-manager-421}

| Section| Recommendation. | Scored? | Level | Result | Responsibility |
| ----- | --------------------------------------------------------------------------------- | ----------------- | ----- | ------ | -------------- |
| 1.3.1 | Ensure that the `--terminated-pod-gc-threshold` argument is set as appropriate. | Not Scored        | 1     | Pass   | {{site.data.keyword.IBM_notm}}            |
| 1.3.2 | Ensure that the `--profiling` argument is set to `false`. | Scored            | 1     | Pass   | {{site.data.keyword.IBM_notm}}            |
| 1.3.3 | Ensure that the `--use-service-account-credentials` argument is set to `true`. | Scored            | 1     | Pass   | {{site.data.keyword.IBM_notm}}            |
| 1.3.4 | Ensure that the `--service-account-private-key-file` argument is set as appropriate. | Scored            | 1     | Pass   | {{site.data.keyword.IBM_notm}}            |
| 1.3.5 | Ensure that the `--root-ca-file` argument is set as appropriate. | Scored            | 1     | Pass   | {{site.data.keyword.IBM_notm}}            |
| 1.3.6 | Ensure that the `RotateKubeletServerCertificate` argument is set to `true`. | Scored            | 1     | Pass   | {{site.data.keyword.IBM_notm}}            |
| 1.3.7 | Ensure that the `--bind-address` argument is set to `127.0.0.1`. | Scored            | 1     | Pass   | {{site.data.keyword.IBM_notm}}            |
{: caption="Section 1.3 Controller manager benchmark results" caption-side="bottom"}

### 1.4 Scheduler
{: #14-scheduler-421}

| Section| Recommendation. | Scored? | Level | Result | Responsibility |
| ----- | ----------------------------------------------------------- | ----------------- | ----- | ------ | -------------- |
| 1.4.1 | Ensure that the `--profiling` argument is set to `false`. | Scored            | 1     | Pass   | {{site.data.keyword.IBM_notm}}            |
| 1.4.2 | Ensure that the `--bind-address` argument is set to `127.0.0.1`. | Scored            | 1     | Pass   | {{site.data.keyword.IBM_notm}}            |
{: caption="Section 1.4 Scheduler benchmark results" caption-side="bottom"}

## 2 Etcd node configuration
{: #2-etcd-node-configuration-421}

| #   | Recommendation. | Scored? | Level | Result | Responsibility |
| --- | ------------------------------------------------------------------------------------- | ----------------- | ----- | ------ | -------------- |
| 2.1 | Ensure that the `--cert-file` and `--key-file` arguments are set as appropriate. | Scored            | 1     | Pass   | {{site.data.keyword.IBM_notm}}            |
| 2.2 | Ensure that the `--client-cert-auth` argument is set to `true`. | Scored            | 1     | Pass   | {{site.data.keyword.IBM_notm}}            |
| 2.3 | Ensure that the `--auto-tls` argument is not set to `true`. | Scored            | 1     | Pass   | {{site.data.keyword.IBM_notm}}            |
| 2.4 | Ensure that the `--peer-cert-file` and `--peer-key-file` arguments are set as appropriate. | Scored            | 1     | Pass   | {{site.data.keyword.IBM_notm}}            |
| 2.5 | Ensure that the `--peer-client-cert-auth` argument is set to `true`. | Scored            | 1     | Pass   | {{site.data.keyword.IBM_notm}}            |
| 2.6 | Ensure that the `--peer-auto-tls` argument is not set to `true`. | Scored            | 1     | Pass   | {{site.data.keyword.IBM_notm}}            |
| 2.7 | Ensure that a unique Certificate Authority is used for etcd. | Not Scored        | 2     | Pass   | {{site.data.keyword.IBM_notm}}            |
{: caption="Section 2 Etcd node configuration benchmark results" caption-side="bottom"}

## 3 Control plane configuration
{: #3-control-plane-configuration-421}

### 3.1 Authentication and authorization
{: #31-authentication-and-authorization-421}

| Section| Recommendation. | Scored? | Level | Result | Responsibility |
| ----- | ----------------------------------------------------------------- | ----------------- | ----- | ------ | -------------- |
| 3.1.1 | Client certificate authentication should not be used for users. | Not Scored        | 1     | Pass   | Shared         |
| 3.1.2 | Service account token authentication should not be used for users. | Not Scored        | 1     | Pass   | Shared         |
| 3.1.3 | Bootstrap token authentication should not be used for users. | Not Scored        | 1     | Pass   | Shared         |
{: caption="Section 3.1 Authentication and authorization benchmark results" caption-side="bottom"}

### 3.2 Logging
{: #32-logging-421}

| Section| Recommendation. | Scored? | Level | Result                                     | Responsibility |
| ----- | --------------------------------------------------------- | ----------------- | ----- | ------------------------------------------ | -------------- |
| 3.2.1 | Ensure that a minimal audit policy is created. | Not Scored        | 1     | [Fail](#ibm-remediations-and-explanations-421) | Shared         |
| 3.2.2 | Ensure that the audit policy covers key security concerns. | Not Scored        | 2     | [Fail](#ibm-remediations-and-explanations-421) | Shared         |
{: caption="Section 3.2 Logging benchmark results" caption-side="bottom"}

## 4 Worker nodes (RHEL_9_64)
{: #4-worker-nodes-rhel_9_64-421}

### 4.1 Worker node configuration files
{: #41-worker-node-configuration-files-421}

| Section | Recommendation. | Scored? | Level | Result | Responsibility |
| ------ | --------------------------------------------------------------------------------------------------------------- | ----------------- | ----- | ------ | -------------- |
| 4.1.1  | Ensure that the kubelet service file permissions are set to `600` or more restrictive. | Scored            | 1     | Pass   | {{site.data.keyword.IBM_notm}}            |
| 4.1.2  | Ensure that the kubelet service file ownership is set to `root:root`. | Scored            | 1     | Pass   | {{site.data.keyword.IBM_notm}}            |
| 4.1.3  | If proxy `kubeconfig` file exists ensure permissions are set to `600` or more restrictive. | Not Scored        | 1     | Pass   | {{site.data.keyword.IBM_notm}}            |
| 4.1.4  | If proxy `kubeconfig` file exists ensure ownership is set to `root:root`. | Not Scored        | 1     | Pass   | {{site.data.keyword.IBM_notm}}            |
| 4.1.5  | Ensure that the `--`kubeconfig`` `kubelet.conf` file permissions are set to `600` or more restrictive. | Scored            | 1     | Pass   | {{site.data.keyword.IBM_notm}}            |
| 4.1.6  | Ensure that the `--`kubeconfig`` `kubelet.conf` file ownership is set to `root:root`. | Scored            | 1     | Pass   | {{site.data.keyword.IBM_notm}}            |
| 4.1.7  | Ensure that the certificate authorities file permissions are set to `644` or more restrictive. | Not Scored        | 1     | Pass   | {{site.data.keyword.IBM_notm}}            |
| 4.1.8  | Ensure that the client certificate authorities file ownership is set to `root:root`. | Not Scored        | 1     | Pass   | {{site.data.keyword.IBM_notm}}            |
| 4.1.9  | If the kubelet config.yaml configuration file is being used validate permissions set to `600` or more restrictive. | Scored            | 1     | Pass   | {{site.data.keyword.IBM_notm}}            |
| 4.1.10 | If the kubelet config.yaml configuration file is being used validate file ownership is set to `root:root`. | Scored            | 1     | Pass   | {{site.data.keyword.IBM_notm}}            |
{: caption="Section 4.1 Worker node configuration files benchmark results" caption-side="bottom"}

### 4.2 Kubelet
{: #42-kubelet-421}

| Section | Recommendation. | Scored? | Level | Result                                     | Responsibility |
| ------ | ------------------------------------------------------------------------------------------------- | ----------------- | ----- | ------------------------------------------ | -------------- |
| 4.2.1  | Ensure that the `--anonymous-auth` argument is set to `false`. | Scored            | 1     | Pass                                       | {{site.data.keyword.IBM_notm}}            |
| 4.2.2  | Ensure that the `--authorization-mode` argument is not set to `AlwaysAllow`. | Scored            | 1     | Pass                                       | {{site.data.keyword.IBM_notm}}            |
| 4.2.3  | Ensure that the `--client-ca-file` argument is set as appropriate. | Scored            | 1     | Pass                                       | {{site.data.keyword.IBM_notm}}            |
| 4.2.4  | Verify that if defined, `readOnlyPort` is set to `0`. | Not Scored        | 1     | Pass                                       | {{site.data.keyword.IBM_notm}}            |
| 4.2.5  | Ensure that the `--streaming-connection-idle-timeout` argument is not set to `0`. | Not Scored        | 1     | Pass                                       | {{site.data.keyword.IBM_notm}}            |
| 4.2.6  | Ensure that the `--make-iptables-util-chains` argument is set to `true`. | Scored            | 1     | Pass                                       | {{site.data.keyword.IBM_notm}}            |
| 4.2.7  | Ensure that the `--hostname-override` argument is not set. | Not Scored        | 1     | [Fail](#ibm-remediations-and-explanations-421) | {{site.data.keyword.IBM_notm}}            |
| 4.2.8  | Ensure that the `eventRecordQPS` argument is set to a level which ensures appropriate event capture. | Not Scored        | 2     | Pass                                       | {{site.data.keyword.IBM_notm}}            |
| 4.2.9  | Ensure that the `--tls-cert-file` and `--tls-private-key-file` arguments are set as appropriate. | Not Scored        | 1     | Pass                                       | {{site.data.keyword.IBM_notm}}            |
| 4.2.10 | Ensure that the `--rotate-certificates` argument is not set to `false`. | Scored            | 1     | [Fail](#ibm-remediations-and-explanations-421) | {{site.data.keyword.IBM_notm}}            |
| 4.2.11 | Verify that the `RotateKubeletServerCertificate` argument is set to `true`. | Not Scored        | 1     | Pass                                       | {{site.data.keyword.IBM_notm}}            |
| 4.2.12 | Ensure that the Kubelet only makes use of Strong Cryptographic Ciphers. | Not Scored        | 1     | Pass                                       | {{site.data.keyword.IBM_notm}}            |
| 4.2.13 | Ensure that a limit is set on pod `PIDs`. | Not Scored        | 1     | Pass                                       | {{site.data.keyword.IBM_notm}}            |
| 4.2.14 | Ensure that the `--seccomp-default` parameter is set to `true`. | Not Scored        | 1     | Pass                                       | {{site.data.keyword.IBM_notm}}            |
{: caption="Section 4.2 Kubelet benchmark results" caption-side="bottom"}

### 4.3 Kube-proxy
{: #43-kube-proxy-421}

| Section| Recommendation. | Scored? | Level | Result | Responsibility |
| ----- | ---------------------------------------------------------------- | ----------------- | ----- | ------ | -------------- |
| 4.3.1 | Ensure that the kube-proxy metrics service is bound to localhost. | Scored            | 1     | Pass   | {{site.data.keyword.IBM_notm}}            |
{: caption="Section 4.3 Kube-proxy benchmark results" caption-side="bottom"}

## 4 Worker node security configuration (RHCOS)
{: #4-worker-node-security-configuration-rhcos-421}

### 4.1 Worker node configuration files
{: #41-worker-node-configuration-files-421}

| Section | Recommendation. | Scored? | Level | Result | Responsibility |
| ------ | --------------------------------------------------------------------------------------------------------------- | ----------------- | ----- | ------ | -------------- |
| 4.1.1  | Ensure that the kubelet service file permissions are set to `600` or more restrictive. | Scored            | 1     | Pass   | {{site.data.keyword.IBM_notm}}            |
| 4.1.2  | Ensure that the kubelet service file ownership is set to `root:root`. | Scored            | 1     | Pass   | {{site.data.keyword.IBM_notm}}            |
| 4.1.3  | If proxy `kubeconfig` file exists ensure permissions are set to `600` or more restrictive. | Not Scored        | 1     | Pass   | {{site.data.keyword.IBM_notm}}            |
| 4.1.4  | If proxy `kubeconfig` file exists ensure ownership is set to `root:root`. | Not Scored        | 1     | Pass   | {{site.data.keyword.IBM_notm}}            |
| 4.1.5  | Ensure that the `--`kubeconfig`` `kubelet.conf` file permissions are set to `600` or more restrictive. | Scored            | 1     | Pass   | {{site.data.keyword.IBM_notm}}            |
| 4.1.6  | Ensure that the `--`kubeconfig`` `kubelet.conf` file ownership is set to `root:root`. | Scored            | 1     | Pass   | {{site.data.keyword.IBM_notm}}            |
| 4.1.7  | Ensure that the certificate authorities file permissions are set to `644` or more restrictive. | Not Scored        | 1     | Pass   | {{site.data.keyword.IBM_notm}}            |
| 4.1.8  | Ensure that the client certificate authorities file ownership is set to `root:root`. | Not Scored        | 1     | Pass   | {{site.data.keyword.IBM_notm}}            |
| 4.1.9  | If the kubelet config.yaml configuration file is being used validate permissions set to `600` or more restrictive. | Scored            | 1     | Pass   | {{site.data.keyword.IBM_notm}}            |
| 4.1.10 | If the kubelet config.yaml configuration file is being used validate file ownership is set to `root:root`. | Scored            | 1     | Pass   | {{site.data.keyword.IBM_notm}}            |
{: caption="Section 4.1 Worker node configuration files benchmark results" caption-side="bottom"}

### 4.2 Kubelet
{: #42-kubelet-421}

| Section | Recommendation. | Scored? | Level | Result                                     | Responsibility |
| ------ | ------------------------------------------------------------------------------------------------- | ----------------- | ----- | ------------------------------------------ | -------------- |
| 4.2.1  | Ensure that the `--anonymous-auth` argument is set to `false`. | Scored            | 1     | Pass                                       | {{site.data.keyword.IBM_notm}}            |
| 4.2.2  | Ensure that the `--authorization-mode` argument is not set to `AlwaysAllow`. | Scored            | 1     | Pass                                       | {{site.data.keyword.IBM_notm}}            |
| 4.2.3  | Ensure that the `--client-ca-file` argument is set as appropriate. | Scored            | 1     | Pass                                       | {{site.data.keyword.IBM_notm}}            |
| 4.2.4  | Verify that if defined, `readOnlyPort` is set to `0`. | Not Scored        | 1     | Pass                                       | {{site.data.keyword.IBM_notm}}            |
| 4.2.5  | Ensure that the `--streaming-connection-idle-timeout` argument is not set to `0`. | Not Scored        | 1     | Pass                                       | {{site.data.keyword.IBM_notm}}            |
| 4.2.6  | Ensure that the `--make-iptables-util-chains` argument is set to `true`. | Scored            | 1     | Pass                                       | {{site.data.keyword.IBM_notm}}            |
| 4.2.7  | Ensure that the `--hostname-override` argument is not set. | Not Scored        | 1     | [Fail](#ibm-remediations-and-explanations-421) | {{site.data.keyword.IBM_notm}}            |
| 4.2.8  | Ensure that the `eventRecordQPS` argument is set to a level which ensures appropriate event capture. | Not Scored        | 2     | Pass                                       | {{site.data.keyword.IBM_notm}}            |
| 4.2.9  | Ensure that the `--tls-cert-file` and `--tls-private-key-file` arguments are set as appropriate. | Not Scored        | 1     | Pass                                       | {{site.data.keyword.IBM_notm}}            |
| 4.2.10 | Ensure that the `--rotate-certificates` argument is not set to `false`. | Scored            | 1     | Pass                                       | {{site.data.keyword.IBM_notm}}            |
| 4.2.11 | Verify that the `RotateKubeletServerCertificate` argument is set to `true`. | Not Scored        | 1     | Pass                                       | {{site.data.keyword.IBM_notm}}            |
| 4.2.12 | Ensure that the Kubelet only makes use of Strong Cryptographic Ciphers. | Not Scored        | 1     | Pass                                       | {{site.data.keyword.IBM_notm}}            |
| 4.2.13 | Ensure that a limit is set on pod `PIDs`. | Not Scored        | 1     | Pass                                       | {{site.data.keyword.IBM_notm}}            |
| 4.2.14 | Ensure that the `--seccomp-default` parameter is set to `true`. | Not Scored        | 1     | Pass                                       | {{site.data.keyword.IBM_notm}}            |
{: caption="Section 4.2 Kubelet benchmark results" caption-side="bottom"}

### 4.3 Kube-proxy
{: #43-kube-proxy-421}

| Section| Recommendation. | Scored? | Level | Result | Responsibility |
| ----- | ---------------------------------------------------------------- | ----------------- | ----- | ------ | -------------- |
| 4.3.1 | Ensure that the kube-proxy metrics service is bound to localhost. | Scored            | 1     | Pass   | {{site.data.keyword.IBM_notm}}            |
{: caption="Section 4.3 Kube-proxy benchmark results" caption-side="bottom"}

## 5 Policies
{: #5-policies-421}

### 5.1 RBAC and service accounts
{: #51-rbac-and-service-accounts-421}

| Section | Recommendation. | Scored? | Level | Result                                     | Responsibility |
| ------ | ------------------------------------------------------------------------------------- | ----------------- | ----- | ------------------------------------------ | -------------- |
| 5.1.1  | Ensure that the cluster-admin role is only used where required. | Not Scored        | 1     | Pass                                       | Shared         |
| 5.1.2  | Minimize access to secrets. | Not Scored        | 1     | [Fail](#ibm-remediations-and-explanations-421) | Shared         |
| 5.1.3  | Minimize wildcard use in `Roles` and `ClusterRoles`. | Not Scored        | 1     | [Fail](#ibm-remediations-and-explanations-421) | Shared         |
| 5.1.4  | Minimize access to create pods. | Not Scored        | 1     | Pass                                       | Shared         |
| 5.1.5  | Ensure that default service accounts are not actively used. | Not Scored        | 1     | [Fail](#ibm-remediations-and-explanations-421) | Shared         |
| 5.1.6  | Ensure that Service Account Tokens are only mounted where necessary. | Not Scored        | 1     | [Fail](#ibm-remediations-and-explanations-421) | Shared         |
| 5.1.7  | Avoid use of system:masters group. | Not Scored        | 1     | Pass                                       | Shared         |
| 5.1.8  | Limit use of the Bind, Impersonate and Escalate permissions in the Kubernetes cluster. | Not Scored        | 1     | Pass                                       | Shared         |
| 5.1.9  | Minimize access to create persistent volumes. | Not Scored        | 1     | Pass                                       | Shared         |
| 5.1.10 | Minimize access to the proxy sub-resource of nodes. | Not Scored        | 1     | Pass                                       | Shared         |
| 5.1.11 | Minimize access to the approval sub-resource of certificatesigningrequests objects. | Not Scored        | 1     | Pass                                       | Shared         |
| 5.1.12 | Minimize access to webhook configuration objects. | Not Scored        | 1     | Pass                                       | Shared         |
| 5.1.13 | Minimize access to the service account token creation. | Not Scored        | 1     | Pass                                       | Shared         |
{: caption="Section 5.1 RBAC and service accounts benchmark results" caption-side="bottom"}

### 5.2 Pod security standards
{: #52-pod-security-standards-421}

| Section | Recommendation. | Scored? | Level | Result                                     | Responsibility |
| ------ | ----------------------------------------------------------------------------------- | ----------------- | ----- | ------------------------------------------ | -------------- |
| 5.2.1  | Ensure that the cluster has at least one active policy control mechanism in place. | Not Scored        | 1     | Pass                                       | Shared         |
| 5.2.2  | Minimize the admission of privileged containers. | Not Scored        | 1     | [Pass](#ibm-remediations-and-explanations-421) | Shared         |
| 5.2.3  | Minimize the admission of containers wishing to share the host process ID namespace. | Not Scored        | 1     | [Pass](#ibm-remediations-and-explanations-421) | Shared         |
| 5.2.4  | Minimize the admission of containers wishing to share the host IPC namespace. | Not Scored        | 1     | [Pass](#ibm-remediations-and-explanations-421) | Shared         |
| 5.2.5  | Minimize the admission of containers wishing to share the host network namespace. | Not Scored        | 1     | [Pass](#ibm-remediations-and-explanations-421) | Shared         |
| 5.2.6  | Minimize the admission of containers with `allowPrivilegeEscalation`. | Not Scored        | 1     | [Pass](#ibm-remediations-and-explanations-421) | Shared         |
| 5.2.7  | Minimize the admission of root containers. | Not Scored        | 2     | [Pass](#ibm-remediations-and-explanations-421) | Shared         |
| 5.2.8  | Minimize the admission of containers with the NET_RAW capability. | Not Scored        | 1     | [Pass](#ibm-remediations-and-explanations-421) | Shared         |
| 5.2.9  | Minimize the admission of containers with capabilities assigned. | Not Scored        | 2     | [Pass](#ibm-remediations-and-explanations-421) | Shared         |
| 5.2.10 | Minimize the admission of Windows `HostProcess` Containers. | Not Scored        | 1     | Pass                                       | Shared         |
| 5.2.11 | Minimize the admission of `HostPath` volumes. | Not Scored        | 1     | Pass                                       | Shared         |
| 5.2.12 | Minimize the admission of containers which use `HostPorts`. | Not Scored        | 1     | Pass                                       | Shared         |
{: caption="Section 5.2 Pod security standards benchmark results" caption-side="bottom"}

### 5.3 Network policies and CNI
{: #53-network-policies-and-cni-421}

| Section| Recommendation. | Scored? | Level | Result | Responsibility |
| ----- | -------------------------------------------------------- | ----------------- | ----- | ------ | -------------- |
| 5.3.1 | Ensure that the CNI in use supports Network Policies. | Not Scored        | 1     | Pass   | {{site.data.keyword.IBM_notm}}            |
| 5.3.2 | Ensure that all Namespaces have Network Policies defined. | Not Scored        | 2     | Pass   | Shared         |
{: caption="Section 5.3 Network policies and CNI benchmark results" caption-side="bottom"}

### 5.4 Secrets management
{: #54-secrets-management-421}

| Section| Recommendation. | Scored? | Level | Result                                     | Responsibility |
| ----- | ------------------------------------------------------------------- | ----------------- | ----- | ------------------------------------------ | -------------- |
| 5.4.1 | Prefer using secrets as files over secrets as environment variables. | Not Scored        | 2     | [Fail](#ibm-remediations-and-explanations-421) | Shared         |
| 5.4.2 | Consider external secret storage. | Not Scored        | 2     | [Fail](#ibm-remediations-and-explanations-421) | Shared         |
{: caption="Section 5.4 Secrets management benchmark results" caption-side="bottom"}

### 5.5 Extensible admission control
{: #55-extensible-admission-control-421}

| Section| Recommendation. | Scored? | Level | Result                                     | Responsibility |
| ----- | ------------------------------------------------------------------------ | ----------------- | ----- | ------------------------------------------ | -------------- |
| 5.5.1 | Configure Image Provenance using `ImagePolicyWebhook` admission controller. | Not Scored        | 2     | [Fail](#ibm-remediations-and-explanations-421) | Shared         |
{: caption="Section 5.5 Extensible admission control benchmark results" caption-side="bottom"}

### 5.6 General policies
{: #56-general-policies-421}

| Section| Recommendation. | Scored? | Level | Result                                     | Responsibility |
| ----- | -------------------------------------------------------------------------------- | ----------------- | ----- | ------------------------------------------ | -------------- |
| 5.6.1 | Create administrative boundaries between resources using namespaces. | Not Scored        | 1     | Pass                                       | Shared         |
| 5.6.2 | Ensure that the `seccomp` profile is set to docker/default in your pod definitions. | Not Scored        | 2     | [Fail](#ibm-remediations-and-explanations-421) | Shared         |
| 5.6.3 | Apply Security Context to Your Pods and Containers. | Not Scored        | 2     | [Fail](#ibm-remediations-and-explanations-421) | Shared         |
| 5.6.4 | The default namespace should not be used. | Not Scored        | 2     | Pass                                       | Shared         |
{: caption="Section 5.6 General policies benchmark results" caption-side="bottom"}

### {{site.data.keyword.IBM_notm}} remediations and explanations
{: #ibm-remediations-and-explanations-421}

| Section | `Remediation and explanation`. |
| ------ | ----- |
| 1.2.1  | {{site.data.keyword.openshiftlong_notm}} utilizes RBAC for cluster protection, but allows anonymous discovery, which is considered reasonable per [CIS Kubernetes Benchmark](https://www.cisecurity.org/benchmark/kubernetes/){: external}. |
| 1.2.3  | OpenShift employs [other mitigating controls](https://docs.redhat.com/en/documentation/openshift_container_platform/4.21/html/ingress_and_load_balancing/configuring-ingress-cluster-traffic#restrictions-on-ip-assignment_configuring-externalip){: external} to restrict service external `IPs`. |
| 1.2.9  | {{site.data.keyword.openshiftlong_notm}} does not enable the [_EventRateLimit_](https://kubernetes.io/docs/reference/access-authn-authz/admission-controllers/#eventratelimit){: external} admission controller since it is a Kubernetes alpha feature. |
| 1.2.11 | {{site.data.keyword.openshiftlong_notm}} does not enable the [_AlwaysPullImages_](https://kubernetes.io/docs/reference/access-authn-authz/admission-controllers/#alwayspullimages){: external} admission controller since it overrides a container's `_imagePullPolicy_` and may impact performance. |
| 1.2.17 | {{site.data.keyword.openshiftlong_notm}} can optionally [enable Kubernetes API server auditing](/docs/openshift?topic=openshift-health-audit). |
| 1.2.27 | {{site.data.keyword.openshiftlong_notm}} can optionally [enable a Kubernetes Key Management Service (KMS) provider](/docs/openshift?topic=openshift-encryption#cluster-secret-encryption). |
| 1.2.28 | {{site.data.keyword.openshiftlong_notm}} can optionally [enable a Kubernetes Key Management Service (KMS) provider](/docs/openshift?topic=openshift-encryption#cluster-secret-encryption). |
| 1.2.30 | OpenShift [does not support](https://access.redhat.com/solutions/7020228){: external} disabling `--service-account-extend-token-expiration`. |
| 3.2.1  | {{site.data.keyword.openshiftlong_notm}} can optionally [enable Kubernetes API server auditing](/docs/openshift?topic=openshift-health-audit). |
| 3.2.2  | {{site.data.keyword.openshiftlong_notm}} can optionally [enable Kubernetes API server auditing](/docs/openshift?topic=openshift-health-audit). |
| 4.2.7  | {{site.data.keyword.openshiftlong_notm}} ensures that the hostname matches the name issued by the infrastructure. |
| 4.2.10 | {{site.data.keyword.openshiftlong_notm}} rotates certificates on every worker node reload or update. |
| 5.1.2  | {{site.data.keyword.openshiftlong_notm}} deploys some system components that could have their Kubernetes secret access further restricted. |
| 5.1.3  | {{site.data.keyword.openshiftlong_notm}} deploys some system components that could have their Kubernetes resource access further restricted. |
| 5.1.5  | {{site.data.keyword.openshiftlong_notm}} does not set `[_automountServiceAccountToken:` false_](https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/#use-the-default-service-account-to-access-the-api-server){: external} for each default service account. |
| 5.1.6  | {{site.data.keyword.openshiftlong_notm}} deploys some system components that could set `[_automountServiceAccountToken:` false_](https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/#use-the-default-service-account-to-access-the-api-server){: external}. |
| 5.2.2  | {{site.data.keyword.openshiftlong_notm}} can optionally configure [OpenShift security context constraints](/docs/openshift?topic=openshift-openshift_scc) and [Kubernetes pod security admission](https://kubernetes.io/docs/concepts/security/pod-security-admission/){: external} which are similar to the deprecated [Kubernetes pod security policies](https://kubernetes.io/docs/concepts/security/pod-security-policy/){: external}. |
| 5.2.3  | {{site.data.keyword.openshiftlong_notm}} can optionally configure [OpenShift security context constraints](/docs/openshift?topic=openshift-openshift_scc) and [Kubernetes pod security admission](https://kubernetes.io/docs/concepts/security/pod-security-admission/){: external} which are similar to the deprecated [Kubernetes pod security policies](https://kubernetes.io/docs/concepts/security/pod-security-policy/){: external}. |
| 5.2.4  | {{site.data.keyword.openshiftlong_notm}} can optionally configure [OpenShift security context constraints](/docs/openshift?topic=openshift-openshift_scc) and [Kubernetes pod security admission](https://kubernetes.io/docs/concepts/security/pod-security-admission/){: external} which are similar to the deprecated [Kubernetes pod security policies](https://kubernetes.io/docs/concepts/security/pod-security-policy/){: external}. |
| 5.2.5  | {{site.data.keyword.openshiftlong_notm}} can optionally configure [OpenShift security context constraints](/docs/openshift?topic=openshift-openshift_scc) and [Kubernetes pod security admission](https://kubernetes.io/docs/concepts/security/pod-security-admission/){: external} which are similar to the deprecated [Kubernetes pod security policies](https://kubernetes.io/docs/concepts/security/pod-security-policy/){: external}. |
| 5.2.6  | {{site.data.keyword.openshiftlong_notm}} can optionally configure [OpenShift security context constraints](/docs/openshift?topic=openshift-openshift_scc) and [Kubernetes pod security admission](https://kubernetes.io/docs/concepts/security/pod-security-admission/){: external} which are similar to the deprecated [Kubernetes pod security policies](https://kubernetes.io/docs/concepts/security/pod-security-policy/){: external}. |
| 5.2.7  | {{site.data.keyword.openshiftlong_notm}} can optionally configure [OpenShift security context constraints](/docs/openshift?topic=openshift-openshift_scc) and [Kubernetes pod security admission](https://kubernetes.io/docs/concepts/security/pod-security-admission/){: external} which are similar to the deprecated [Kubernetes pod security policies](https://kubernetes.io/docs/concepts/security/pod-security-policy/){: external}. |
| 5.2.8  | {{site.data.keyword.openshiftlong_notm}} can optionally configure [OpenShift security context constraints](/docs/openshift?topic=openshift-openshift_scc) and [Kubernetes pod security admission](https://kubernetes.io/docs/concepts/security/pod-security-admission/){: external} which are similar to the deprecated [Kubernetes pod security policies](https://kubernetes.io/docs/concepts/security/pod-security-policy/){: external}. |
| 5.2.9  | {{site.data.keyword.openshiftlong_notm}} can optionally configure [OpenShift security context constraints](/docs/openshift?topic=openshift-openshift_scc) and [Kubernetes pod security admission](https://kubernetes.io/docs/concepts/security/pod-security-admission/){: external} which are similar to the deprecated [Kubernetes pod security policies](https://kubernetes.io/docs/concepts/security/pod-security-policy/){: external}. |
| 5.4.1  | {{site.data.keyword.openshiftlong_notm}} deploys some system components that could prefer using secrets as files over secrets as environment variables. |
| 5.4.2  | {{site.data.keyword.openshiftlong_notm}} can optionally [enable Secrets Manager service](/docs/openshift?topic=openshift-secrets-mgr). |
| 5.5.1  | {{site.data.keyword.openshiftlong_notm}} can optionally [enable image security enforcement](/docs/openshift?topic=openshift-images#portieris-image-sec). |
| 5.6.2  | {{site.data.keyword.openshiftlong_notm}} does not annotate all pods with [`seccomp` profiles](https://kubernetes.io/docs/concepts/security/pod-security-policy/#seccomp){: external}. |
| 5.6.3  | {{site.data.keyword.openshiftlong_notm}} deploys some system components that do not set a [pod or container _securityContext_](https://kubernetes.io/docs/tasks/configure-pod-container/security-context/){: external}. |
{: caption="Section {{site.data.keyword.IBM_notm}} remediations and explanations benchmark results" caption-side="bottom"}
