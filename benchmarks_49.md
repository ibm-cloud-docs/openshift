---

copyright: 
  years: 2014, 2022
lastupdated: "2022-03-16"

keywords: openshift

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}

# {{site.data.keyword.openshiftlong_notm}} version 4.9: CIS Kubernetes Benchmark
{: #cis-benchmark-49}

The Center for Internet Security (CIS) publishes the [CIS Kubernetes Benchmark](https://www.cisecurity.org/benchmark/kubernetes/){: external} as a framework of specific steps to configure Kubernetes more securely and with standards that are commensurate to various industry regulations. This document contains the results of the version 1.5 CIS Kubernetes benchmark for clusters that run {{site.data.keyword.openshiftlong_notm}} version 4.9. For more information or help understanding the benchmark, see [Using the benchmark](/docs/containers?topic=containers-cis-benchmark).
{: shortdesc}


## 1 Master Node Security Configuration
{: #cis-section-1-49}

Reivew the Master Node Security Configuration results of the version 1.5 CIS Kubernetes benchmark.
{: shortdesc}

### 1.1 Master Node Configuration Files
{: #cis-benchmark-11-49}

| Section | Recommendation | Scored/Not Scored | Level | Result | Responsibility |
| --- | --- | --- | --- | --- | --- |
| 1.1.1 | Ensure that the API server pod specification file permissions are set to 644 or more restrictive | Scored | 1 | Pass | {{site.data.keyword.IBM_notm}} |
| 1.1.2 | Ensure that the API server pod specification file ownership is set to root:root | Scored | 1 | Pass | {{site.data.keyword.IBM_notm}} |
| 1.1.3 | Ensure that the controller manager pod specification file permissions are set to 644 or more restrictive | Scored | 1 | Pass | {{site.data.keyword.IBM_notm}} |
| 1.1.4 | Ensure that the controller manager pod specification file ownership is set to root:root | Scored | 1 | Pass | {{site.data.keyword.IBM_notm}} |
| 1.1.5 | Ensure that the scheduler pod specification file permissions are set to 644 or more restrictive | Scored | 1 | Pass | {{site.data.keyword.IBM_notm}} |
| 1.1.6 | Ensure that the scheduler pod specification file ownership is set to root:root | Scored | 1 | Pass | {{site.data.keyword.IBM_notm}} |
| 1.1.7 | Ensure that the etcd pod specification file permissions are set to 644 or more restrictive | Scored | 1 | Pass | {{site.data.keyword.IBM_notm}} |
| 1.1.8 | Ensure that the etcd pod specification file ownership is set to root:root | Scored | 1 | Pass | {{site.data.keyword.IBM_notm}} |
| 1.1.9 | Ensure that the Container Network Interface file permissions are set to 644 or more restrictive | Not Scored | 1 | Pass | {{site.data.keyword.IBM_notm}} |
| 1.1.10 | Ensure that the Container Network Interface file ownership is set to root:root | Not Scored | 1 | Pass | {{site.data.keyword.IBM_notm}} |
| 1.1.11 | Ensure that the etcd data directory permissions are set to 700 or more restrictive | Scored | 1 | Pass | {{site.data.keyword.IBM_notm}} |
| 1.1.12 | Ensure that the etcd data directory ownership is set to etcd:etcd | Scored | 1 | Pass | {{site.data.keyword.IBM_notm}} |
| 1.1.13 | Ensure that the admin.conf file permissions are set to 644 or more restrictive | Scored | 1 | Pass | {{site.data.keyword.IBM_notm}} |
| 1.1.14 | Ensure that the admin.conf file ownership is set to root:root | Scored | 1 | Pass | {{site.data.keyword.IBM_notm}} |
| 1.1.15 | Ensure that the scheduler.conf file permissions are set to 644 or more restrictive | Scored | 1 | Pass | {{site.data.keyword.IBM_notm}} |
| 1.1.16 | Ensure that the scheduler.conf file ownership is set to root:root | Scored | 1 | Pass | {{site.data.keyword.IBM_notm}} |
| 1.1.17 | Ensure that the controller-manager.conf file permissions are set to 644 or more restrictive | Scored | 1 | Pass | {{site.data.keyword.IBM_notm}} |
| 1.1.18 | Ensure that the controller-manager.conf file ownership is set to root:root | Scored | 1 | Pass | {{site.data.keyword.IBM_notm}} |
| 1.1.19 | Ensure that the Kubernetes PKI directory and file ownership is set to root:root | Scored | 1 | Pass | {{site.data.keyword.IBM_notm}} |
| 1.1.20 | Ensure that the Kubernetes PKI certificate file permissions are set to 644 or more restrictive | Scored | 1 | Pass | {{site.data.keyword.IBM_notm}} |
| 1.1.21 | Ensure that the Kubernetes PKI key file permissions are set to 600 | Scored | 1 | Pass | {{site.data.keyword.IBM_notm}} |
{: summary="The rows are read from left to right. The first column is the section number for the benchmark recommendation. The second column is the benchmark recommendation. The third column is the scoring of the recommendation, either scored or not scored. The fourth column is the level of the recommendation, either 1 for basic or 2 for more advanced and performance-impacting. The fifth column contains the result of whether the service passes or fails the recommendation. The sixth column designates the responsibility of passing the recommendation, either IBM or shared between IBM and you."}
{: caption="Section 1.1 Master node benchmark results" caption-side="top"}


### 1.2 API Server
{: #cis-benchmark-12-49}

| Section | Recommendation | Scored/Not Scored | Level | Result | Responsibility |
| --- | --- | --- | --- | --- | --- |
| 1.1.1 | Ensure that the API server pod specification file permissions are set to 644 or more restrictive | Scored | 1 | Pass | {{site.data.keyword.IBM_notm}} |
| 1.1.2 | Ensure that the API server pod specification file ownership is set to root:root | Scored | 1 | Pass | {{site.data.keyword.IBM_notm}} |
| 1.1.3 | Ensure that the controller manager pod specification file permissions are set to 644 or more restrictive | Scored | 1 | Pass | {{site.data.keyword.IBM_notm}} |
| 1.1.4 | Ensure that the controller manager pod specification file ownership is set to root:root | Scored | 1 | Pass | {{site.data.keyword.IBM_notm}} |
| 1.1.5 | Ensure that the scheduler pod specification file permissions are set to 644 or more restrictive | Scored | 1 | Pass | {{site.data.keyword.IBM_notm}} |
| 1.1.6 | Ensure that the scheduler pod specification file ownership is set to root:root | Scored | 1 | Pass | {{site.data.keyword.IBM_notm}} |
| 1.1.7 | Ensure that the etcd pod specification file permissions are set to 644 or more restrictive | Scored | 1 | Pass | {{site.data.keyword.IBM_notm}} |
| 1.1.8 | Ensure that the etcd pod specification file ownership is set to root:root | Scored | 1 | Pass | {{site.data.keyword.IBM_notm}} |
| 1.1.9 | Ensure that the Container Network Interface file permissions are set to 644 or more restrictive | Not Scored | 1 | Pass | {{site.data.keyword.IBM_notm}} |
| 1.1.10 | Ensure that the Container Network Interface file ownership is set to root:root | Not Scored | 1 | Pass | {{site.data.keyword.IBM_notm}} |
| 1.1.11 | Ensure that the etcd data directory permissions are set to 700 or more restrictive | Scored | 1 | Pass | {{site.data.keyword.IBM_notm}} |
| 1.1.12 | Ensure that the etcd data directory ownership is set to etcd:etcd | Scored | 1 | Pass | {{site.data.keyword.IBM_notm}} |
| 1.1.13 | Ensure that the admin.conf file permissions are set to 644 or more restrictive | Scored | 1 | Pass | {{site.data.keyword.IBM_notm}} |
| 1.1.14 | Ensure that the admin.conf file ownership is set to root:root | Scored | 1 | Pass | {{site.data.keyword.IBM_notm}} |
| 1.1.15 | Ensure that the scheduler.conf file permissions are set to 644 or more restrictive | Scored | 1 | Pass | {{site.data.keyword.IBM_notm}} |
| 1.1.16 | Ensure that the scheduler.conf file ownership is set to root:root | Scored | 1 | Pass | {{site.data.keyword.IBM_notm}} |
| 1.1.17 | Ensure that the controller-manager.conf file permissions are set to 644 or more restrictive | Scored | 1 | Pass | {{site.data.keyword.IBM_notm}} |
| 1.1.18 | Ensure that the controller-manager.conf file ownership is set to root:root | Scored | 1 | Pass | {{site.data.keyword.IBM_notm}} |
| 1.1.19 | Ensure that the Kubernetes PKI directory and file ownership is set to root:root | Scored | 1 | Pass | {{site.data.keyword.IBM_notm}} |
| 1.1.20 | Ensure that the Kubernetes PKI certificate file permissions are set to 644 or more restrictive | Scored | 1 | Pass | {{site.data.keyword.IBM_notm}} |
| 1.1.21 | Ensure that the Kubernetes PKI key file permissions are set to 600 | Scored | 1 | Pass | {{site.data.keyword.IBM_notm}} |
{: summary="The rows are read from left to right. The first column is the section number for the benchmark recommendation. The second column is the benchmark recommendation. The third column is the scoring of the recommendation, either scored or not scored. The fourth column is the level of the recommendation, either 1 for basic or 2 for more advanced and performance-impacting. The fifth column contains the result of whether the service passes or fails the recommendation. The sixth column designates the responsibility of passing the recommendation, either IBM or shared between IBM and you."}
{: caption="Section 1.2 API Server benchmark results" caption-side="top"}

### 1.3 Controller Manager
{: #cis-benchmark-13-49}

| Section | Recommendation | Scored/Not Scored | Level | Result | Responsibility |
| --- | --- | --- | --- | --- | --- |
| 1.3.1 | Ensure that the `--terminated-pod-gc-threshold` argument is set as appropriate | Scored | 1 | Pass | {{site.data.keyword.IBM_notm}} |
| 1.3.2 | Ensure that the `--profiling` argument is set to false | Scored | 1 | Pass | {{site.data.keyword.IBM_notm}} |
| 1.3.3 | Ensure that the `--use-service-account-credentials` argument is set to true | Scored | 1 | Pass | {{site.data.keyword.IBM_notm}} |
| 1.3.4 | Ensure that the `--service-account-private-key-file` argument is set as appropriate | Scored | 1 | Pass | {{site.data.keyword.IBM_notm}} |
| 1.3.5 | Ensure that the `--root-ca-file` argument is set as appropriate | Scored | 1 | Pass | {{site.data.keyword.IBM_notm}} |
| 1.3.6 | Ensure that the RotateKubeletServerCertificate argument is set to true | Scored | 2 | Pass | {{site.data.keyword.IBM_notm}} |
| 1.3.7 | Ensure that the `--bind-address` argument is set to 127.0.0.1 | Scored | 1 | Pass | {{site.data.keyword.IBM_notm}} |
{: summary="The rows are read from left to right. The first column is the section number for the benchmark recommendation. The second column is the benchmark recommendation. The third column is the scoring of the recommendation, either scored or not scored. The fourth column is the level of the recommendation, either 1 for basic or 2 for more advanced and performance-impacting. The fifth column contains the result of whether the service passes or fails the recommendation. The sixth column designates the responsibility of passing the recommendation, either IBM or shared between IBM and you."}
{: caption="Section 1.3 Controller Manager benchmark results" caption-side="top"}


### 1.4 Scheduler
{: #cis-benchmark-14-49}

| Section | Recommendation | Scored/Not Scored | Level | Result | Responsibility |
| --- | --- | --- | --- | --- | --- |
| 1.4.1 | Ensure that the `--profiling` argument is set to false | Scored | 1 | Pass | {{site.data.keyword.IBM_notm}} |
| 1.4.2 | Ensure that the `--bind-address` argument is set to 127.0.0.1 | Scored | 1 | Pass | {{site.data.keyword.IBM_notm}} |
{: summary="The rows are read from left to right. The first column is the section number for the benchmark recommendation. The second column is the benchmark recommendation. The third column is the scoring of the recommendation, either scored or not scored. The fourth column is the level of the recommendation, either 1 for basic or 2 for more advanced and performance-impacting. The fifth column contains the result of whether the service passes or fails the recommendation. The sixth column designates the responsibility of passing the recommendation, either IBM or shared between IBM and you."}
{: caption="Section 1.4 Scheduler benchmark results" caption-side="top"}

## 2 Etcd Node Configuration
{: #cis-section-2-49}

Reivew the Etcd Node Configuration results of the version 1.5 CIS Kubernetes benchmark.
{: shortdesc}

| Section | Recommendation | Scored/Not Scored | Level | Result | Responsibility |
| --- | --- | --- | --- | --- | --- |
| 2.1 | Ensure that the `--cert-file` and `--key-file` arguments are set as appropriate | Scored | 1 | Pass | {{site.data.keyword.IBM_notm}} |
| 2.2 | Ensure that the `--client-cert-auth` argument is set to true | Scored | 1 | Pass | {{site.data.keyword.IBM_notm}} |
| 2.3 | Ensure that the `--auto-tls` argument is not set to true | Scored | 1 | Pass | {{site.data.keyword.IBM_notm}} |
| 2.4 | Ensure that the `--peer-cert-file` and `--peer-key-file` arguments are set as appropriate | Scored | 1 | Pass | {{site.data.keyword.IBM_notm}} |
| 2.5 | Ensure that the `--peer-client-cert-auth` argument is set to true | Scored | 1 | Pass | {{site.data.keyword.IBM_notm}} |
| 2.6 | Ensure that the `--peer-auto-tls` argument is not set to true | Scored | 1 | Pass | {{site.data.keyword.IBM_notm}} |
| 2.7 | Ensure that a unique Certificate Authority is used for etcd | Not Scored | 2 | Pass | {{site.data.keyword.IBM_notm}} |
{: summary="The rows are read from left to right. The first column is the section number for the benchmark recommendation. The second column is the benchmark recommendation. The third column is the scoring of the recommendation, either scored or not scored. The fourth column is the level of the recommendation, either 1 for basic or 2 for more advanced and performance-impacting. The fifth column contains the result of whether the service passes or fails the recommendation. The sixth column designates the responsibility of passing the recommendation, either IBM or shared between IBM and you."}
{: caption="Section 2 Etcd Node Configuration benchmark results" caption-side="top"}


## 3 Control Plane Configuration
{: #cis-section-3-49}

Reivew the Control Plane Configuration results of the version 1.5 CIS Kubernetes benchmark.
{: shortdesc}

### 3.1 Authentication and Authorization
{: #cis-benchmark-31-49}

| Section | Recommendation | Scored/Not Scored | Level | Result | Responsibility |
| --- | --- | --- | --- | --- | --- |
| 3.1.1 | Client certificate authentication should not be used for users | Not Scored | 2 | Pass | Shared |
{: summary="The rows are read from left to right. The first column is the section number for the benchmark recommendation. The second column is the benchmark recommendation. The third column is the scoring of the recommendation, either scored or not scored. The fourth column is the level of the recommendation, either 1 for basic or 2 for more advanced and performance-impacting. The fifth column contains the result of whether the service passes or fails the recommendation. The sixth column designates the responsibility of passing the recommendation, either IBM or shared between IBM and you."}
{: caption="Section 3.1 Authentication and Authorization benchmark results" caption-side="top"}

### 3.2 Logging
{: #cis-benchmark-32-49}

| Section | Recommendation | Scored/Not Scored | Level | Result | Responsibility |
| --- | --- | --- | --- | --- | --- |
| 3.2.1 | Ensure that a minimal audit policy is created | Scored | 1 | [Fail](#cis-benchmark-remediations-49) | Shared |
| 3.2.2 | Ensure that the audit policy covers key security concerns | Not Scored | 2 | [Fail](#cis-benchmark-remediations-49) | Shared |
{: summary="The rows are read from left to right. The first column is the section number for the benchmark recommendation. The second column is the benchmark recommendation. The third column is the scoring of the recommendation, either scored or not scored. The fourth column is the level of the recommendation, either 1 for basic or 2 for more advanced and performance-impacting. The fifth column contains the result of whether the service passes or fails the recommendation. The sixth column designates the responsibility of passing the recommendation, either IBM or shared between IBM and you."}
{: caption="Section 3.2 Logging benchmark results" caption-side="top"}

## 4 Worker Node Security Configuration
{: #cis-section-4-49}

Reivew the Worker Node Security Configuration results of the version 1.5 CIS Kubernetes benchmark.
{: shortdesc}

### 4.1 Worker Node Configuration Files
{: #cis-benchmark-41-49}

| Section | Recommendation | Scored/Not Scored | Level | Result | Responsibility |
| --- | --- | --- | --- | --- | --- |
| 4.1.1 | Ensure that the kubelet service file permissions are set to 644 or more restrictive | Scored | 1 | Pass | {{site.data.keyword.IBM_notm}} |
| 4.1.2 | Ensure that the kubelet service file ownership is set to root:root | Scored | 1 | Pass | {{site.data.keyword.IBM_notm}} |
| 4.1.3 | Ensure that the proxy kubeconfig file permissions are set to 644 or more restrictive | Scored | 1 | Pass | {{site.data.keyword.IBM_notm}} |
| 4.1.4 | Ensure that the proxy kubeconfig file ownership is set to root:root | Scored | 1 | Pass | {{site.data.keyword.IBM_notm}} |
| 4.1.5 | Ensure that the kubelet.conf file permissions are set to 644 or more restrictive | Scored | 1 | Pass | {{site.data.keyword.IBM_notm}} |
| 4.1.6 | Ensure that the kubelet.conf file ownership is set to root:root | Scored | 1 | Pass | {{site.data.keyword.IBM_notm}} |
| 4.1.7 | Ensure that the certificate authorities file permissions are set to 644 or more restrictive | Scored | 1 | Pass | {{site.data.keyword.IBM_notm}} |
| 4.1.8 | Ensure that the client certificate authorities file ownership is set to root:root | Scored | 1 | Pass | {{site.data.keyword.IBM_notm}} |
| 4.1.9 | Ensure that the kubelet configuration file has permissions set to 644 or more restrictive | Scored | 1 | Pass | {{site.data.keyword.IBM_notm}} |
| 4.1.10 | Ensure that the kubelet configuration file ownership is set to root:root | Scored | 1 | Pass | {{site.data.keyword.IBM_notm}} |
{: summary="The rows are read from left to right. The first column is the section number for the benchmark recommendation. The second column is the benchmark recommendation. The third column is the scoring of the recommendation, either scored or not scored. The fourth column is the level of the recommendation, either 1 for basic or 2 for more advanced and performance-impacting. The fifth column contains the result of whether the service passes or fails the recommendation. The sixth column designates the responsibility of passing the recommendation, either IBM or shared between IBM and you."}
{: caption="Section 4.1 Worker Node Configuration benchmark results" caption-side="top"}


### 4.2 Kubelet
{: #cis-benchmark-42-49}

| Section | Recommendation | Scored/Not Scored | Level | Result | Responsibility |
| --- | --- | --- | --- | --- | --- |
| 4.2.1 | Ensure that the `--anonymous-auth` argument is set to false | Scored | 1 | Pass | {{site.data.keyword.IBM_notm}} |
| 4.2.2 | Ensure that the `--authorization-mode` argument is not set to AlwaysAllow | Scored | 1 | Pass | {{site.data.keyword.IBM_notm}} |
| 4.2.3 | Ensure that the `--client-ca-file` argument is set as appropriate | Scored | 1 | Pass | {{site.data.keyword.IBM_notm}} |
| 4.2.4 | Ensure that the `--read-only-port` argument is set to 0 | Scored | 1 | Pass | {{site.data.keyword.IBM_notm}} |
| 4.2.5 | Ensure that the `--streaming-connection-idle-timeout` argument is not set to 0 | Scored | 1 | Pass | {{site.data.keyword.IBM_notm}} |
| 4.2.6 | Ensure that the `--protect-kernel-defaults` argument is set to true | Scored | 1 | [Fail](#cis-benchmark-remediations-49) | {{site.data.keyword.IBM_notm}} |
| 4.2.7 | Ensure that the `--make-iptables-util-chains` argument is set to true | Scored | 1 | Pass | {{site.data.keyword.IBM_notm}} |
| 4.2.8 | Ensure that the `--hostname-override` argument is not set | Not Scored | 1 | [Fail](#cis-benchmark-remediations-49) | {{site.data.keyword.IBM_notm}} |
| 4.2.9 | Ensure that the `--event-qps` argument is set to 0 or a level which ensures appropriate event capture | Not Scored | 2 | Pass | {{site.data.keyword.IBM_notm}} |
| 4.2.10 | Ensure that the `--tls-cert-file` and `--tls-private-key-file` arguments are set as appropriate | Scored | 1 | Pass | {{site.data.keyword.IBM_notm}} |
| 4.2.11 | Ensure that the `--rotate-certificates` argument is not set to false | Scored | 1 | Pass | {{site.data.keyword.IBM_notm}} |
| 4.2.12 | Ensure that the RotateKubeletServerCertificate argument is set to true | Scored | 1 | Pass | {{site.data.keyword.IBM_notm}} |
| 4.2.13 | Ensure that the Kubelet only makes use of Strong Cryptographic Ciphers | Not Scored | 1 | Pass | {{site.data.keyword.IBM_notm}} |
{: summary="The rows are read from left to right. The first column is the section number for the benchmark recommendation. The second column is the benchmark recommendation. The third column is the scoring of the recommendation, either scored or not scored. The fourth column is the level of the recommendation, either 1 for basic or 2 for more advanced and performance-impacting. The fifth column contains the result of whether the service passes or fails the recommendation. The sixth column designates the responsibility of passing the recommendation, either IBM or shared between IBM and you."}
{: caption="Section 4.2 Kubelet benchmark results" caption-side="top"}

## 5 Kubernetes Policies
{: #cis-section-5-49}

Reivew the Kubernetes Policies results of the version 1.5 CIS Kubernetes benchmark.
{: shortdesc}

### 5.1 RBAC and Service Accounts
{: #cis-benchmark-51-49}

| Section | Recommendation | Scored/Not Scored | Level | Result | Responsibility |
| --- | --- | --- | --- | --- | --- |
| 5.1.1 | Ensure that the cluster-admin role is only used where required | Not Scored | 1 | Pass | Shared |
| 5.1.2 | Minimize access to secrets | Not Scored | 1 | [Fail](#cis-benchmark-remediations-49) | Shared |
| 5.1.3 | Minimize wildcard use in Roles and ClusterRoles | Not Scored | 1 | [Fail](#cis-benchmark-remediations-49) | Shared |
| 5.1.4 | Minimize access to create pods | Not Scored | 1 | Pass | Shared |
| 5.1.5 | Ensure that default service accounts are not actively used. | Scored | 1 | [Fail](#cis-benchmark-remediations-49) | Shared |
| 5.1.6 | Ensure that Service Account Tokens are only mounted where necessary | Not Scored | 1 | [Fail](#cis-benchmark-remediations-49) | Shared |
{: summary="The rows are read from left to right. The first column is the section number for the benchmark recommendation. The second column is the benchmark recommendation. The third column is the scoring of the recommendation, either scored or not scored. The fourth column is the level of the recommendation, either 1 for basic or 2 for more advanced and performance-impacting. The fifth column contains the result of whether the service passes or fails the recommendation. The sixth column designates the responsibility of passing the recommendation, either IBM or shared between IBM and you."}
{: caption="Section 5.1 RBAC and Service Accounts benchmark results" caption-side="top"}


### 5.2 Pod Security Policies
{: #cis-benchmark-52-49}

| Section | Recommendation | Scored/Not Scored | Level | Result | Responsibility |
| --- | --- | --- | --- | --- | --- |
| 5.2.1 | Minimize the admission of privileged containers | Not Scored | 1 | [Pass](#cis-benchmark-remediations-49) | Shared |
| 5.2.2 | Minimize the admission of containers wishing to share the host process ID namespace | Scored | 1 | [Pass](#cis-benchmark-remediations-49) | Shared |
| 5.2.3 | Minimize the admission of containers wishing to share the host IPC namespace | Scored | 1 | [Pass](#cis-benchmark-remediations-49) | Shared |
| 5.2.4 | Minimize the admission of containers wishing to share the host network namespace | Scored | 1 | [Pass](#cis-benchmark-remediations-49) | Shared |
| 5.2.5 | Minimize the admission of containers with allowPrivilegeEscalation | Scored | 1 | [Pass](#cis-benchmark-remediations-49) | Shared |
| 5.2.6 | Minimize the admission of root containers | Not Scored | 2 | [Pass](#cis-benchmark-remediations-49) | Shared |
| 5.2.7 | Minimize the admission of containers with the NET_RAW capability | Not Scored | 1 | [Pass](#cis-benchmark-remediations-49) | Shared |
| 5.2.8 | Minimize the admission of containers with added capabilities | Not Scored | 1 | [Pass](#cis-benchmark-remediations-49) | Shared |
| 5.2.9 | Minimize the admission of containers with capabilities assigned | Not Scored | 2 | [Pass](#cis-benchmark-remediations-49) | Shared |
{: summary="The rows are read from left to right. The first column is the section number for the benchmark recommendation. The second column is the benchmark recommendation. The third column is the scoring of the recommendation, either scored or not scored. The fourth column is the level of the recommendation, either 1 for basic or 2 for more advanced and performance-impacting. The fifth column contains the result of whether the service passes or fails the recommendation. The sixth column designates the responsibility of passing the recommendation, either IBM or shared between IBM and you."}
{: caption="Section 5.2 Pod Security Policies benchmark results" caption-side="top"}



### 5.3 Network Policies and CNI
{: #cis-benchmark-53-49}

| Section | Recommendation | Scored/Not Scored | Level | Result | Responsibility |
| --- | --- | --- | --- | --- | --- |
| 5.3.1 | Ensure that the CNI in use supports Network Policies | Not Scored | 1 | Pass | {{site.data.keyword.IBM_notm}} |
| 5.3.2 | Ensure that all Namespaces have Network Policies defined | Scored | 2 | [Fail](#cis-benchmark-remediations-49) | Shared |
{: summary="The rows are read from left to right. The first column is the section number for the benchmark recommendation. The second column is the benchmark recommendation. The third column is the scoring of the recommendation, either scored or not scored. The fourth column is the level of the recommendation, either 1 for basic or 2 for more advanced and performance-impacting. The fifth column contains the result of whether the service passes or fails the recommendation. The sixth column designates the responsibility of passing the recommendation, either IBM or shared between IBM and you."}
{: caption="Section 5.3 Network Policies and CNI benchmark results" caption-side="top"}


### 5.4 Secrets Management
{: #cis-benchmark-54-49}

| Section | Recommendation | Scored/Not Scored | Level | Result | Responsibility |
| --- | --- | --- | --- | --- | --- |
| 5.4.1 | Prefer using secrets as files over secrets as environment variables | Not Scored | 1 | [Fail](#cis-benchmark-remediations-49) | Shared |
| 5.4.2 | Consider external secret storage | Not Scored | 2 | [Fail](#cis-benchmark-remediations-49) | Shared |
{: summary="The rows are read from left to right. The first column is the section number for the benchmark recommendation. The second column is the benchmark recommendation. The third column is the scoring of the recommendation, either scored or not scored. The fourth column is the level of the recommendation, either 1 for basic or 2 for more advanced and performance-impacting. The fifth column contains the result of whether the service passes or fails the recommendation. The sixth column designates the responsibility of passing the recommendation, either IBM or shared between IBM and you."}
{: caption="Section 5.4 Secrets Management benchmark results" caption-side="top"}

### 5.5 Extensible Admission Control
{: #cis-benchmark-55-49}

| Section | Recommendation | Scored/Not Scored | Level | Result | Responsibility |
| --- | --- | --- | --- | --- | --- |
| 5.5.1 | Configure Image Provenance using ImagePolicyWebhook admission controller | Not Scored | 2 | [Fail](#cis-benchmark-remediations-49) | Shared |
{: summary="The rows are read from left to right. The first column is the section number for the benchmark recommendation. The second column is the benchmark recommendation. The third column is the scoring of the recommendation, either scored or not scored. The fourth column is the level of the recommendation, either 1 for basic or 2 for more advanced and performance-impacting. The fifth column contains the result of whether the service passes or fails the recommendation. The sixth column designates the responsibility of passing the recommendation, either IBM or shared between IBM and you."}
{: caption="Section 5.5 Extensible Admission Control benchmark results" caption-side="top"}

### 5.6 General Policies
{: #cis-benchmark-56-49}

| Section | Recommendation | Scored/Not Scored | Level | Result | Responsibility |
| --- | --- | --- | --- | --- | --- |
| 5.6.1 | Create administrative boundaries between resources using namespaces | Not Scored | 1 | Pass | Shared |
| 5.6.2 | Ensure that the seccomp profile is set to docker/default in your pod definitions | Not Scored | 2 | [Fail](#cis-benchmark-remediations-49) | Shared |
| 5.6.3 | Apply Security Context to Your Pods and Containers | Not Scored | 2 | [Fail](#cis-benchmark-remediations-49) | Shared |
| 5.6.4 | The default namespace should not be used | Scored | 2 | Pass | Shared |
{: summary="The rows are read from left to right. The first column is the section number for the benchmark recommendation. The second column is the benchmark recommendation. The third column is the scoring of the recommendation, either scored or not scored. The fourth column is the level of the recommendation, either 1 for basic or 2 for more advanced and performance-impacting. The fifth column contains the result of whether the service passes or fails the recommendation. The sixth column designates the responsibility of passing the recommendation, either IBM or shared between IBM and you."}
{: caption="Section 5.6 General Policies benchmark results" caption-side="top"}


## IBM Remediations and Explanations
{: #cis-benchmark-remediations-49}

Review information from IBM on the CIS Benchmark results.
{: shortdesc}

| Section | Remediation/Explanation |
| --- | --- |
| 1.2.1 | {{site.data.keyword.openshiftlong_notm}} utilizes RBAC for cluster protection, but allows anonymous discovery, which is considered reasonable per [CIS Kubernetes Benchmark](https://www.cisecurity.org/benchmark/kubernetes/). |
| 1.2.10 | {{site.data.keyword.openshiftlong_notm}} does not enable the [*EventRateLimit*](https://kubernetes.io/docs/reference/access-authn-authz/admission-controllers/#eventratelimit) admission controller since it is a Kubernetes alpha feature. |
| 1.2.12 | {{site.data.keyword.openshiftlong_notm}} does not enable the [*AlwaysPullImages*](https://kubernetes.io/docs/reference/access-authn-authz/admission-controllers/#alwayspullimages) admission controller since it overrides a container's *imagePullPolicy* and may impact performance. |
| 1.2.13 | {{site.data.keyword.openshiftlong_notm}} supports [pod security context constraints](/docs/openshift?topic=openshift-openshift_scc) which are similar to Kubernetes pod security policies. |
| 1.2.16 | {{site.data.keyword.openshiftlong_notm}} supports [pod security context constraints](/docs/openshift?topic=openshift-openshift_scc) which are similar to Kubernetes pod security policies. |
| 1.2.22 | {{site.data.keyword.openshiftlong_notm}} can optionally [enable Kubernetes API server auditing](/docs/openshift?topic=openshift-health-audit). |
| 1.2.23 | {{site.data.keyword.openshiftlong_notm}} can optionally [enable Kubernetes API server auditing](/docs/openshift?topic=openshift-health-audit). |
| 1.2.24 | {{site.data.keyword.openshiftlong_notm}} can optionally [enable Kubernetes API server auditing](/docs/openshift?topic=openshift-health-audit). |
| 1.2.25 | {{site.data.keyword.openshiftlong_notm}} can optionally [enable Kubernetes API server auditing](/docs/openshift?topic=openshift-health-audit). |
| 1.2.33 | {{site.data.keyword.openshiftlong_notm}} can optionally [enable a Kubernetes Key Management Service (KMS) provider](/docs/openshift?topic=openshift-encryption#kms). |
| 1.2.34 | {{site.data.keyword.openshiftlong_notm}} can optionally [enable a Kubernetes Key Management Service (KMS) provider](/docs/openshift?topic=openshift-encryption#kms). |
| 3.2.1 | {{site.data.keyword.openshiftlong_notm}} can optionally [enable Kubernetes API server auditing](/docs/openshift?topic=openshift-health-audit). |
| 3.2.2 | {{site.data.keyword.openshiftlong_notm}} can optionally [enable Kubernetes API server auditing](/docs/openshift?topic=openshift-health-audit). |
| 4.2.6 | {{site.data.keyword.openshiftlong_notm}} does not protect kernel defaults in order to allow customers to tune kernel parameters. |
| 4.2.8 | {{site.data.keyword.openshiftlong_notm}} ensures that the hostname matches the name issued by the infrastructure. |
| 5.1.2 | {{site.data.keyword.openshiftlong_notm}} deploys some system components that could have their Kubernetes secret access further restricted. |
| 5.1.3 | {{site.data.keyword.openshiftlong_notm}} deploys some system components that could have their Kubernetes resource access further restricted. |
| 5.1.5 | {{site.data.keyword.openshiftlong_notm}} does not set [*automountServiceAccountToken: false*](https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/#use-the-default-service-account-to-access-the-api-server) for each default service account. |
| 5.1.6 | {{site.data.keyword.openshiftlong_notm}} deploys some system components that could set [*automountServiceAccountToken: false*](https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/#use-the-default-service-account-to-access-the-api-server). |
| 5.2.1 | {{site.data.keyword.openshiftlong_notm}} can optionally [configure security context constraints](/docs/openshift?topic=openshift-openshift_scc). |
| 5.2.2 | {{site.data.keyword.openshiftlong_notm}} can optionally [configure security context constraints](/docs/openshift?topic=openshift-openshift_scc). |
| 5.2.3 | {{site.data.keyword.openshiftlong_notm}} can optionally [configure security context constraints](/docs/openshift?topic=openshift-openshift_scc). |
| 5.2.4 | {{site.data.keyword.openshiftlong_notm}} can optionally [configure security context constraints](/docs/openshift?topic=openshift-openshift_scc). |
| 5.2.5 | {{site.data.keyword.openshiftlong_notm}} can optionally [configure security context constraints](/docs/openshift?topic=openshift-openshift_scc). |
| 5.2.6 | {{site.data.keyword.openshiftlong_notm}} can optionally [configure security context constraints](/docs/openshift?topic=openshift-openshift_scc). |
| 5.2.7 | {{site.data.keyword.openshiftlong_notm}} can optionally [configure security context constraints](/docs/openshift?topic=openshift-openshift_scc). |
| 5.2.8 | {{site.data.keyword.openshiftlong_notm}} can optionally [configure security context constraints](/docs/openshift?topic=openshift-openshift_scc). |
| 5.2.9 | {{site.data.keyword.openshiftlong_notm}} can optionally [configure security context constraints](/docs/openshift?topic=openshift-openshift_scc). |
| 5.3.2 | {{site.data.keyword.openshiftlong_notm}} has a set of [default Calico network policies defined]( /docs/openshift?topic=openshift-network_policies#default_policy) and [additional network policies can optionally be added](/docs/openshift?topic=openshift-network_policies#adding_network_policies). |
| 5.4.1 | {{site.data.keyword.openshiftlong_notm}} deploys some system components that could prefer using secrets as files over secrets as environment variables. |
| 5.4.2 | {{site.data.keyword.openshiftlong_notm}} can optionally [enable a Kubernetes Key Management Service (KMS) provider](/docs/openshift?topic=openshift-encryption#kms). |
| 5.5.1 | {{site.data.keyword.openshiftlong_notm}} can optionally [enable image security enforcement](/docs/openshift?topic=openshift-images#portieris-image-sec). |
| 5.6.2 | {{site.data.keyword.openshiftlong_notm}} does not annotate all pods with [seccomp profiles](https://kubernetes.io/docs/concepts/policy/pod-security-policy/#seccomp). |
| 5.6.3 | {{site.data.keyword.openshiftlong_notm}} deploys some system components that do not set a [pod or container *securityContext*](https://kubernetes.io/docs/tasks/configure-pod-container/security-context/). |
{: summary="The rows are read from left to right. The first column is the section number for the benchmark recommendation. The second column contains details on the remediation actions."}
{: caption="Explanation and remediation" caption-side="top"}



