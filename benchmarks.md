---

copyright: 
  years: 2014, 2022
lastupdated: "2022-02-10"

keywords: openshift

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}


# CIS Kubernetes Benchmark
{: #cis-benchmark}

The Center for Internet Security (CIS) publishes the [CIS Kubernetes Benchmark](https://www.cisecurity.org/benchmark/kubernetes/){: external} as a framework of specific steps to configure Kubernetes more securely and with standards that are commensurate to various industry regulations.
{: shortdesc}

When a new Kubernetes version is released as part of a [supported {{site.data.keyword.openshiftshort}} version](/docs/openshift?topic=openshift-openshift_versions#version_types), IBM engineers compare the default configuration of a cluster that runs that Kubernetes version against the benchmark and publishes the results in this documentation. You can review how specific versions of your {{site.data.keyword.openshiftlong}} clusters meet the CIS Kubernetes Benchmark.

## Using the benchmark
{: #cis-benchmark-use}

As a security administrator or auditor, you might want to compare your company's internal standards and external regulatory requirements with the CIS Kubernetes Benchmark. The benchmark recommendations are provided by the Center for Internet Security, not by IBM. IBM might not configure default settings in a way that meets every recommendation, but documents whether the recommendation is met to help you in your review. For example, you might use the benchmark in an audit to confirm that basic security measures are in place, and to identify areas where you might enhance your security.
{: shortdesc}

**What does the benchmark cover?**

The benchmark covers recommendations for master components, etcd, control plane configurations, worker nodes, and policies such as for users, network, and pod security. 

**What do the benchmark recommendations mean?**

The benchmark recommendations have scoring, levels, result status, and responsibilities as follows.

* **Scoring**
    * Scored: The overall benchmark score increases or decreases depending on whether the  recommendation is met.
    * Not scored: The overall benchmark score is not impacted, whether the recommendation is met.
* **Levels**
    * Level 1: Practical security measures that can be configured without inhibiting the service.
    * Level 2: More in-depth security measures that might reduce the performance or functionality of a service.
* **Result**
    * Pass: The service complies with the benchmark recommendation.
    * Fail: The service does not comply with the benchmark recommendation by default. Refer to the remediation section for an explanation and possible actions that you can take to comply with the benchmark recommendation.
* **Responsibility**
    * IBM: IBM is responsible for configuring the setting that the benchmark recommends.
    * Shared: You and IBM share responsibility for configuring the setting that the benchmark recommends.

**What parts of the benchmark am I responsible for?**

Because {{site.data.keyword.openshiftlong_notm}} is a managed offering, IBM already configures many security settings for you. For example, IBM manages and automatically applies updates to your cluster master. For your worker nodes, IBM provides security and version updates, but you must apply the updates. You are also responsible for your workload applications and data. For more information, see [Your responsibilities while using {{site.data.keyword.openshiftlong_notm}}](/docs/containers?topic=containers-responsibilities_iks).

**What if some part of the service fails to comply with a recommendation?**

First, check the explanation of the failure for any remediation steps.

Then, determine whether the failure is acceptable according to your security requirements. For example, some recommendations might be more in-depth configuration requirements than your particular processes or standards require. Also, some recommendations are not scored, and don't impact the overall benchmark score.

Next, decide whether the component falls within your responsibility. If so, you might need to change how you configure that component. For example, you might configure security context constraints for all your app deployments. For components that are not directly within your responsibility, assess whether you can use another {{site.data.keyword.cloud_notm}} service to meet the recommendation.

**What else can I do to increase the security and compliance of my cluster?**

See [Security for {{site.data.keyword.openshiftlong_notm}}](/docs/containers?topic=containers-security).



## Running the worker node CIS Kubernetes benchmark
{: #cis-worker-test}

To review the results of the CIS Kubernetes benchmark for [Section 4: Worker node security configuration](#cis-benchmark-15-4), you can run the test yourself. Because you own the worker nodes and are partially [responsible](/docs/containers?topic=containers-responsibilities_iks) for their compliance, you might make configuration changes that you want to validate on your own.
{: shortdesc}

These steps apply to clusters that run {{site.data.keyword.openshiftshort}} version 4.5 or later only.
{: note}

Before you begin: [Log in to your account. If applicable, target the appropriate resource group. Set the context for your cluster.](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure)

1. Create a project for the resources to run the benchmark.
    ```sh
    oc create ns ibm-kube-bench-test
    ```
    {: pre}

2. Create a configmap with the `config` and `node` configuration files from the [kube-samples](https://github.com/IBM-Cloud/kube-samples/tree/master/cis-kube-benchmark/cis-1.5/ibm){: external} GitHub repository.
    1. Download the the `config` and `node` configuration files into a local directory called `ibm`. You can also clone the repository and navigate into the `ibm` directory.
        * [`config` file](https://raw.githubusercontent.com/IBM-Cloud/kube-samples/master/cis-kube-benchmark/cis-1.5/ibm/config.yaml){: external}
        * [`node` file](https://raw.githubusercontent.com/IBM-Cloud/kube-samples/master/cis-kube-benchmark/cis-1.5/ibm/node.yaml){: external}
    2. Create the configmap by using the `--from-file` flag to specify the `ibm` directory where your downloaded the configuration files.
        ```sh
        oc create cm kube-bench-node -n ibm-kube-bench-test --from-file ibm
        ```
        {: pre}

3. Create a job to run the benchmark test based on the configurations that you previously created.
    ```sh
    oc apply -n ibm-kube-bench-test -f https://raw.githubusercontent.com/IBM-Cloud/kube-samples/master/cis-kube-benchmark/cis-1.5/ibm/job-node.yaml
    ```
    {: pre}

4. Check that the job successfully completed.
    ```sh
    oc get pods -n ibm-kube-bench-test -l job-name=kube-bench-node
    ```
    {: pre}

    Example output

    ```sh
    NAME                    READY   STATUS      RESTARTS   AGE
    kube-bench-node-hlvhc   0/1     Completed   0          23s
    ```
    {: screen}

5. Review the CIS Kubernetes benchmark results for your worker nodes by checking the pod logs.
    ```sh
    oc logs -n ibm-kube-bench-test -l job-name=kube-bench-node --tail=-1
    ```
    {: pre}

    Example output

    ```sh
    == Summary ==
    20 checks PASS
    2 checks FAIL
    1 checks WARN
    0 checks INFO
    ```
    {: screen}

6. Optional: When you are done reviewing results, delete the resources that you created.
    ```sh
    oc delete ns ibm-kube-bench-test
    ```
    {: pre}



## Benchmark 1.5 results for {{site.data.keyword.openshiftshort}} versions 4.6 - 4.8
{: #cis-benchmark-15}

Review how {{site.data.keyword.openshiftlong_notm}} complies with the version 1.5 CIS Kubernetes benchmark for clusters that run {{site.data.keyword.openshiftshort}} versions 4.6 - 4.8. For help understanding the benchmark, see [Using the benchmark](#cis-benchmark-use).
{: shortdesc}




### 1.1 Master Node Configuration Files
{: #cis-benchmark-15-1-1}

| # | Recommendation | Scored/Not Scored | Level | Result | Responsibility |
| --- | --- | --- | --- | --- | --- |
| 1.1.1 | Ensure that the API server pod specification file permissions are set to 644 or more restrictive | Scored | 1 | Pass | IBM |
| 1.1.2 | Ensure that the API server pod specification file ownership is set to root:root | Scored | 1 | Pass | IBM |
| 1.1.3 | Ensure that the controller manager pod specification file permissions are set to 644 or more restrictive | Scored | 1 | Pass | IBM |
| 1.1.4 | Ensure that the controller manager pod specification file ownership is set to root:root | Scored | 1 | Pass | IBM |
| 1.1.5 | Ensure that the scheduler pod specification file permissions are set to 644 or more restrictive | Scored | 1 | Pass | IBM |
| 1.1.6 | Ensure that the scheduler pod specification file ownership is set to root:root | Scored | 1 | Pass | IBM |
| 1.1.7 | Ensure that the etcd pod specification file permissions are set to 644 or more restrictive | Scored | 1 | Pass | IBM |
| 1.1.8 | Ensure that the etcd pod specification file ownership is set to root:root | Scored | 1 | Pass | IBM |
| 1.1.9 | Ensure that the Container Network Interface file permissions are set to 644 or more restrictive | Not Scored | 1 | Pass | IBM |
| 1.1.10 | Ensure that the Container Network Interface file ownership is set to root:root | Not Scored | 1 | Pass | IBM |
| 1.1.11 | Ensure that the etcd data directory permissions are set to 700 or more restrictive | Scored | 1 | Pass | IBM |
| 1.1.12 | Ensure that the etcd data directory ownership is set to etcd:etcd | Scored | 1 | Pass | IBM |
| 1.1.13 | Ensure that the admin.conf file permissions are set to 644 or more restrictive | Scored | 1 | Pass | IBM |
| 1.1.14 | Ensure that the admin.conf file ownership is set to root:root | Scored | 1 | Pass | IBM |
| 1.1.15 | Ensure that the scheduler.conf file permissions are set to 644 or more restrictive | Scored | 1 | Pass | IBM |
| 1.1.16 | Ensure that the scheduler.conf file ownership is set to root:root | Scored | 1 | Pass | IBM |
| 1.1.17 | Ensure that the controller-manager.conf file permissions are set to 644 or more restrictive | Scored | 1 | Pass | IBM |
| 1.1.18 | Ensure that the controller-manager.conf file ownership is set to root:root | Scored | 1 | Pass | IBM |
| 1.1.19 | Ensure that the Kubernetes PKI directory and file ownership is set to root:root | Scored | 1 | Pass | IBM |
| 1.1.20 | Ensure that the Kubernetes PKI certificate file permissions are set to 644 or more restrictive | Scored | 1 | Pass | IBM |
| 1.1.21 | Ensure that the Kubernetes PKI key file permissions are set to 600 | Scored | 1 | Pass | IBM |
{: summary="The rows are read from left to right. The first column is the section number for the benchmark recommendation. The second column is the benchmark recommendation. The third column is the scoring of the recommendation, either scored or not scored. The fourth column is the level of the recommendation, either 1 for basic or 2 for more advanced and performance-impacting. The fifth column contains the result of whether the service passes or fails the recommendation. The sixth column designates the responsibility of passing the recommendation, either IBM or shared between IBM and you."}
{: caption="Section 1.1 Master node benchmark results" caption-side="top"}

### 1.2 API Server
{: #cis-benchmark-15-1-2}

| # | Recommendation | Scored/Not Scored | Level | Result | Responsibility |
| --- | --- | --- | --- | --- | --- |
| 1.2.1 | Ensure that the --anonymous-auth argument is set to false | Not Scored | 1 | [Fail](#ibm-remediations-and-explanations) | IBM |
| 1.2.2 | Ensure that the --basic-auth-file argument is not set | Scored | 1 | Pass | IBM |
| 1.2.3 | Ensure that the --token-auth-file parameter is not set | Scored | 1 | Pass | IBM |
| 1.2.4 | Ensure that the --kubelet-https argument is set to true | Scored | 1 | Pass | IBM |
| 1.2.5 | Ensure that the --kubelet-client-certificate and --kubelet-client-key arguments are set as appropriate | Scored | 1 | Pass | IBM |
| 1.2.6 | Ensure that the --kubelet-certificate-authority argument is set as appropriate | Scored | 1 | Pass | IBM |
| 1.2.7 | Ensure that the --authorization-mode argument is not set to AlwaysAllow | Scored | 1 | Pass | IBM |
| 1.2.8 | Ensure that the --authorization-mode argument includes Node | Scored | 1 | Pass | IBM |
| 1.2.9 | Ensure that the --authorization-mode argument includes RBAC | Scored | 1 | Pass | IBM |
| 1.2.10 | Ensure that the admission control plugin EventRateLimit is set | Not Scored | 1 | [Fail](#ibm-remediations-and-explanations) | IBM |
| 1.2.11 | Ensure that the admission control plugin AlwaysAdmit is not set | Scored | 1 | Pass | IBM |
| 1.2.12 | Ensure that the admission control plugin AlwaysPullImages is set | Not Scored | 1 | [Fail](#ibm-remediations-and-explanations) | IBM |
| 1.2.13 | Ensure that the admission control plugin SecurityContextDeny is set if PodSecurityPolicy is not used | Not Scored | 1 | [Pass](#ibm-remediations-and-explanations) | IBM |
| 1.2.14 | Ensure that the admission control plugin ServiceAccount is set | Scored | 1 | Pass | IBM |
| 1.2.15 | Ensure that the admission control plugin NamespaceLifecycle is set | Scored | 1 | Pass | IBM |
| 1.2.16 | Ensure that the admission control plugin PodSecurityPolicy is set | Scored | 1 | [Pass](#ibm-remediations-and-explanations) | IBM |
| 1.2.17 | Ensure that the admission control plugin NodeRestriction is set | Scored | 1 | Pass | IBM |
| 1.2.18 | Ensure that the --insecure-bind-address argument is not set | Scored | 1 | Pass | IBM |
| 1.2.19 | Ensure that the --insecure-port argument is set to 0 | Scored | 1 | Pass | IBM |
| 1.2.20 | Ensure that the --secure-port argument is not set to 0 | Scored | 1 | Pass | IBM |
| 1.2.21 | Ensure that the --profiling argument is set to false | Scored | 1 | Pass | IBM |
| 1.2.22 | Ensure that the --audit-log-path argument is set | Scored | 1 | [Fail](#ibm-remediations-and-explanations) | Shared |
| 1.2.23 | Ensure that the --audit-log-maxage argument is set to 30 or as appropriate | Scored | 1 | [Fail](#ibm-remediations-and-explanations) | Shared |
| 1.2.24 | Ensure that the --audit-log-maxbackup argument is set to 10 or as appropriate | Scored | 1 | [Fail](#ibm-remediations-and-explanations) | Shared |
| 1.2.25 | Ensure that the --audit-log-maxsize argument is set to 100 or as appropriate | Scored | 1 | [Fail](#ibm-remediations-and-explanations) | Shared |
| 1.2.26 | Ensure that the --request-timeout argument is set as appropriate | Scored | 1 | Pass | IBM |
| 1.2.27 | Ensure that the --service-account-lookup argument is set to true | Scored | 1 | Pass | IBM |
| 1.2.28 | Ensure that the --service-account-key-file argument is set as appropriate | Scored | 1 | Pass | IBM |
| 1.2.29 | Ensure that the --etcd-certfile and --etcd-keyfile arguments are set as appropriate | Scored | 1 | Pass | IBM |
| 1.2.30 | Ensure that the --tls-cert-file and --tls-private-key-file arguments are set as appropriate | Scored | 1 | Pass | IBM |
| 1.2.31 | Ensure that the --client-ca-file argument is set as appropriate | Scored | 1 | Pass | IBM |
| 1.2.32 | Ensure that the --etcd-cafile argument is set as appropriate | Scored | 1 | Pass | IBM |
| 1.2.33 | Ensure that the --encryption-provider-config argument is set as appropriate | Scored | 1 | [Fail](#ibm-remediations-and-explanations) | Shared |
| 1.2.34 | Ensure that encryption providers are appropriately configured | Scored | 1 | [Fail](#ibm-remediations-and-explanations) | Shared |
| 1.2.35 | Ensure that the API Server only makes use of Strong Cryptographic Ciphers | Not Scored | 1 | Pass | IBM |
{: summary="The rows are read from left to right. The first column is the section number for the benchmark recommendation. The second column is the benchmark recommendation. The third column is the scoring of the recommendation, either scored or not scored. The fourth column is the level of the recommendation, either 1 for basic or 2 for more advanced and performance-impacting. The fifth column contains the result of whether the service passes or fails the recommendation. The sixth column designates the responsibility of passing the recommendation, either IBM or shared between IBM and you."}
{: caption="Section 1.2 API server benchmark results" caption-side="top"}

### 1.3 Controller Manager
{: #cis-benchmark-15-1-3}

| # | Recommendation | Scored/Not Scored | Level | Result | Responsibility |
| --- | --- | --- | --- | --- | --- |
| 1.3.1 | Ensure that the --terminated-pod-gc-threshold argument is set as appropriate | Scored | 1 | Pass | IBM |
| 1.3.2 | Ensure that the --profiling argument is set to false | Scored | 1 | Pass | IBM |
| 1.3.3 | Ensure that the --use-service-account-credentials argument is set to true | Scored | 1 | Pass | IBM |
| 1.3.4 | Ensure that the --service-account-private-key-file argument is set as appropriate | Scored | 1 | Pass | IBM |
| 1.3.5 | Ensure that the --root-ca-file argument is set as appropriate | Scored | 1 | Pass | IBM |
| 1.3.6 | Ensure that the RotateKubeletServerCertificate argument is set to true | Scored | 2 | Pass | IBM |
| 1.3.7 | Ensure that the --bind-address argument is set to 127.0.0.1 | Scored | 1 | Pass | IBM |
{: summary="The rows are read from left to right. The first column is the section number for the benchmark recommendation. The second column is the benchmark recommendation. The third column is the scoring of the recommendation, either scored or not scored. The fourth column is the level of the recommendation, either 1 for basic or 2 for more advanced and performance-impacting. The fifth column contains the result of whether the service passes or fails the recommendation. The sixth column designates the responsibility of passing the recommendation, either IBM or shared between IBM and you."}
{: caption="Section 1.3 Controller manager benchmark results" caption-side="top"}

### 1.4 Scheduler
{: #cis-benchmark-15-1-4}

| # | Recommendation | Scored/Not Scored | Level | Result | Responsibility |
| --- | --- | --- | --- | --- | --- |
| 1.4.1 | Ensure that the --profiling argument is set to false | Scored | 1 | Pass | IBM |
| 1.4.2 | Ensure that the --bind-address argument is set to 127.0.0.1 | Scored | 1 | Pass | IBM |
{: summary="The rows are read from left to right. The first column is the section number for the benchmark recommendation. The second column is the benchmark recommendation. The third column is the scoring of the recommendation, either scored or not scored. The fourth column is the level of the recommendation, either 1 for basic or 2 for more advanced and performance-impacting. The fifth column contains the result of whether the service passes or fails the recommendation. The sixth column designates the responsibility of passing the recommendation, either IBM or shared between IBM and you."}
{: caption="Section 1.4 Scheduler benchmark results" caption-side="top"}

## 2 `etcd` Node Configuration
{: #cis-benchmark-15-2}

| # | Recommendation | Scored/Not Scored | Level | Result | Responsibility |
| --- | --- | --- | --- | --- | --- |
| 2.1 | Ensure that the --cert-file and --key-file arguments are set as appropriate | Scored | 1 | Pass | IBM |
| 2.2 | Ensure that the --client-cert-auth argument is set to true | Scored | 1 | Pass | IBM |
| 2.3 | Ensure that the --auto-tls argument is not set to true | Scored | 1 | Pass | IBM |
| 2.4 | Ensure that the --peer-cert-file and --peer-key-file arguments are set as appropriate | Scored | 1 | Pass | IBM |
| 2.5 | Ensure that the --peer-client-cert-auth argument is set to true | Scored | 1 | Pass | IBM |
| 2.6 | Ensure that the --peer-auto-tls argument is not set to true | Scored | 1 | Pass | IBM |
| 2.7 | Ensure that a unique Certificate Authority is used for etcd | Not Scored | 2 | Pass | IBM |
{: summary="The rows are read from left to right. The first column is the section number for the benchmark recommendation. The second column is the benchmark recommendation. The third column is the scoring of the recommendation, either scored or not scored. The fourth column is the level of the recommendation, either 1 for basic or 2 for more advanced and performance-impacting. The fifth column contains the result of whether the service passes or fails the recommendation. The sixth column designates the responsibility of passing the recommendation, either IBM or shared between IBM and you."}
{: caption="Section 2 etcd benchmark results" caption-side="top"}

## 3 Control Plane Configuration
{: #cis-benchmark-15-3}

### 3.1 Authentication and Authorization
{: #cis-benchmark-15-3-1}

| # | Recommendation | Scored/Not Scored | Level | Result | Responsibility |
| --- | --- | --- | --- | --- | --- |
| 3.1.1 | Client certificate authentication should not be used for users | Not Scored | 2 | Pass | Shared |
{: summary="The rows are read from left to right. The first column is the section number for the benchmark recommendation. The second column is the benchmark recommendation. The third column is the scoring of the recommendation, either scored or not scored. The fourth column is the level of the recommendation, either 1 for basic or 2 for more advanced and performance-impacting. The fifth column contains the result of whether the service passes or fails the recommendation. The sixth column designates the responsibility of passing the recommendation, either IBM or shared between IBM and you."}
{: caption="Section 3.1 Authorization benchmark results" caption-side="top"}

### 3.2 Logging
{: #cis-benchmark-15-3-2}

| # | Recommendation | Scored/Not Scored | Level | Result | Responsibility |
| --- | --- | --- | --- | --- | --- |
| 3.2.1 | Ensure that a minimal audit policy is created | Scored | 1 | [Fail](#ibm-remediations-and-explanations) | Shared |
| 3.2.2 | Ensure that the audit policy covers key security concerns | Not Scored | 2 | [Fail](#ibm-remediations-and-explanations) | Shared |
{: summary="The rows are read from left to right. The first column is the section number for the benchmark recommendation. The second column is the benchmark recommendation. The third column is the scoring of the recommendation, either scored or not scored. The fourth column is the level of the recommendation, either 1 for basic or 2 for more advanced and performance-impacting. The fifth column contains the result of whether the service passes or fails the recommendation. The sixth column designates the responsibility of passing the recommendation, either IBM or shared between IBM and you."}
{: caption="Section 3.2 Logging benchmark results" caption-side="top"}

## 4 Worker Node Security Configuration
{: #cis-benchmark-15-4}

### 4.1 Worker Node Configuration Files
{: #cis-benchmark-15-4-1}

| # | Recommendation | Scored/Not Scored | Level | Result | Responsibility |
| --- | --- | --- | --- | --- | --- |
| 4.1.1 | Ensure that the kubelet service file permissions are set to 644 or more restrictive | Scored | 1 | Pass | IBM |
| 4.1.2 | Ensure that the kubelet service file ownership is set to root:root | Scored | 1 | Pass | IBM |
| 4.1.3 | Ensure that the proxy kubeconfig file permissions are set to 644 or more restrictive | Scored | 1 | Pass | IBM |
| 4.1.4 | Ensure that the proxy kubeconfig file ownership is set to root:root | Scored | 1 | Pass | IBM |
| 4.1.5 | Ensure that the kubelet.conf file permissions are set to 644 or more restrictive | Scored | 1 | Pass | IBM |
| 4.1.6 | Ensure that the kubelet.conf file ownership is set to root:root | Scored | 1 | Pass | IBM |
| 4.1.7 | Ensure that the certificate authorities file permissions are set to 644 or more restrictive | Scored | 1 | Pass | IBM |
| 4.1.8 | Ensure that the client certificate authorities file ownership is set to root:root | Scored | 1 | Pass | IBM |
| 4.1.9 | Ensure that the kubelet configuration file has permissions set to 644 or more restrictive | Scored | 1 | Pass | IBM |
| 4.1.10 | Ensure that the kubelet configuration file ownership is set to root:root | Scored | 1 | Pass | IBM |
{: summary="The rows are read from left to right. The first column is the section number for the benchmark recommendation. The second column is the benchmark recommendation. The third column is the scoring of the recommendation, either scored or not scored. The fourth column is the level of the recommendation, either 1 for basic or 2 for more advanced and performance-impacting. The fifth column contains the result of whether the service passes or fails the recommendation. The sixth column designates the responsibility of passing the recommendation, either IBM or shared between IBM and you."}
{: caption="Section 4.1 Worker node benchmark results" caption-side="top"}

### 4.2 Kubelet
{: #cis-benchmark-15-4-2}

| 4.2.1 | Ensure that the --anonymous-auth argument is set to false | Scored | 1 | Pass | IBM |
| 4.2.2 | Ensure that the --authorization-mode argument is not set to AlwaysAllow | Scored | 1 | Pass | IBM |
| 4.2.3 | Ensure that the --client-ca-file argument is set as appropriate | Scored | 1 | Pass | IBM |
| 4.2.4 | Ensure that the --read-only-port argument is set to 0 | Scored | 1 | Pass | IBM |
| 4.2.5 | Ensure that the --streaming-connection-idle-timeout argument is not set to 0 | Scored | 1 | Pass | IBM |
| 4.2.6 | Ensure that the --protect-kernel-defaults argument is set to true | Scored | 1 | [Fail](#ibm-remediations-and-explanations) | IBM |
| 4.2.7 | Ensure that the --make-iptables-util-chains argument is set to true | Scored | 1 | Pass | IBM |
| 4.2.8 | Ensure that the --hostname-override argument is not set | Not Scored | 1 | [Fail](#ibm-remediations-and-explanations) | IBM |
| 4.2.9 | Ensure that the --event-qps argument is set to 0 or a level which ensures appropriate event capture | Not Scored | 2 | Pass | IBM |
| 4.2.10 | Ensure that the --tls-cert-file and --tls-private-key-file arguments are set as appropriate | Scored | 1 | Pass | IBM |
| 4.2.11 | Ensure that the --rotate-certificates argument is not set to false | Scored | 1 | Pass | IBM |
| 4.2.12 | Ensure that the RotateKubeletServerCertificate argument is set to true | Scored | 1 | Pass | IBM |
| 4.2.13 | Ensure that the Kubelet only makes use of Strong Cryptographic Ciphers | Not Scored | 1 | Pass | IBM |
{: summary="The rows are read from left to right. The first column is the section number for the benchmark recommendation. The second column is the benchmark recommendation. The third column is the scoring of the recommendation, either scored or not scored. The fourth column is the level of the recommendation, either 1 for basic or 2 for more advanced and performance-impacting. The fifth column contains the result of whether the service passes or fails the recommendation. The sixth column designates the responsibility of passing the recommendation, either IBM or shared between IBM and you."}
{: caption="Section 4.2 Kubelet benchmark results" caption-side="top"}

## 5 Kubernetes Policies
{: #cis-benchmark-15-5}


### 5.1 RBAC and Service Accounts
{: #cis-benchmark-15-5-1}

| # | Recommendation | Scored/Not Scored | Level | Result | Responsibility |
| --- | --- | --- | --- | --- | --- |
| 5.1.1 | Ensure that the cluster-admin role is only used where required | Not Scored | 1 | Pass | Shared |
| 5.1.2 | Minimize access to secrets | Not Scored | 1 | [Fail](#ibm-remediations-and-explanations) | Shared |
| 5.1.3 | Minimize wildcard use in Roles and ClusterRoles | Not Scored | 1 | [Fail](#ibm-remediations-and-explanations) | Shared |
| 5.1.4 | Minimize access to create pods | Not Scored | 1 | Pass | Shared |
| 5.1.5 | Ensure that default service accounts are not actively used. | Scored | 1 | [Fail](#ibm-remediations-and-explanations) | Shared |
| 5.1.6 | Ensure that Service Account Tokens are only mounted where necessary | Not Scored | 1 | [Fail](#ibm-remediations-and-explanations) | Shared |
{: summary="The rows are read from left to right. The first column is the section number for the benchmark recommendation. The second column is the benchmark recommendation. The third column is the scoring of the recommendation, either scored or not scored. The fourth column is the level of the recommendation, either 1 for basic or 2 for more advanced and performance-impacting. The fifth column contains the result of whether the service passes or fails the recommendation. The sixth column designates the responsibility of passing the recommendation, either IBM or shared between IBM and you."}
{: caption="Section 5.1 RBAC benchmark results" caption-side="top"}

### 5.2 Pod Security Policies
{: #cis-benchmark-15-5-2}

| # | Recommendation | Scored/Not Scored | Level | Result | Responsibility |
| --- | --- | --- | --- | --- | --- |
| 5.2.1 | Minimize the admission of privileged containers | Not Scored | 1 | [Pass](#ibm-remediations-and-explanations) | Shared |
| 5.2.2 | Minimize the admission of containers wishing to share the host process ID namespace | Scored | 1 | [Pass](#ibm-remediations-and-explanations) | Shared |
| 5.2.3 | Minimize the admission of containers wishing to share the host IPC namespace | Scored | 1 | [Pass](#ibm-remediations-and-explanations) | Shared |
| 5.2.4 | Minimize the admission of containers wishing to share the host network namespace | Scored | 1 | [Pass](#ibm-remediations-and-explanations) | Shared |
| 5.2.5 | Minimize the admission of containers with allowPrivilegeEscalation | Scored | 1 | [Pass](#ibm-remediations-and-explanations) | Shared |
| 5.2.6 | Minimize the admission of root containers | Not Scored | 2 | [Pass](#ibm-remediations-and-explanations) | Shared |
| 5.2.7 | Minimize the admission of containers with the NET_RAW capability | Not Scored | 1 | [Pass](#ibm-remediations-and-explanations) | Shared |
| 5.2.8 | Minimize the admission of containers with added capabilities | Not Scored | 1 | [Pass](#ibm-remediations-and-explanations) | Shared |
| 5.2.9 | Minimize the admission of containers with capabilities assigned | Not Scored | 2 | [Pass](#ibm-remediations-and-explanations) | Shared |
{: summary="The rows are read from left to right. The first column is the section number for the benchmark recommendation. The second column is the benchmark recommendation. The third column is the scoring of the recommendation, either scored or not scored. The fourth column is the level of the recommendation, either 1 for basic or 2 for more advanced and performance-impacting. The fifth column contains the result of whether the service passes or fails the recommendation. The sixth column designates the responsibility of passing the recommendation, either IBM or shared between IBM and you."}
{: caption="Section 5.2 Pod security benchmark results" caption-side="top"}

### 5.3 Network Policies and CNI
{: #cis-benchmark-15-5-3}

| # | Recommendation | Scored/Not Scored | Level | Result | Responsibility |
| --- | --- | --- | --- | --- | --- |
| 5.3.1 | Ensure that the CNI in use supports Network Policies | Not Scored | 1 | Pass | IBM |
| 5.3.2 | Ensure that all Namespaces have Network Policies defined | Scored | 2 | [Fail](#ibm-remediations-and-explanations) | Shared |
{: summary="The rows are read from left to right. The first column is the section number for the benchmark recommendation. The second column is the benchmark recommendation. The third column is the scoring of the recommendation, either scored or not scored. The fourth column is the level of the recommendation, either 1 for basic or 2 for more advanced and performance-impacting. The fifth column contains the result of whether the service passes or fails the recommendation. The sixth column designates the responsibility of passing the recommendation, either IBM or shared between IBM and you."}
{: caption="Section 5.3 Network policies benchmark results" caption-side="top"}

### 5.4 Secrets Management
{: #cis-benchmark-15-5-4}

| # | Recommendation | Scored/Not Scored | Level | Result | Responsibility |
| --- | --- | --- | --- | --- | --- |
| 5.4.1 | Prefer using secrets as files over secrets as environment variables | Not Scored | 1 | [Fail](#ibm-remediations-and-explanations) | Shared |
| 5.4.2 | Consider external secret storage | Not Scored | 2 | [Fail](#ibm-remediations-and-explanations) | Shared |
{: summary="The rows are read from left to right. The first column is the section number for the benchmark recommendation. The second column is the benchmark recommendation. The third column is the scoring of the recommendation, either scored or not scored. The fourth column is the level of the recommendation, either 1 for basic or 2 for more advanced and performance-impacting. The fifth column contains the result of whether the service passes or fails the recommendation. The sixth column designates the responsibility of passing the recommendation, either IBM or shared between IBM and you."}
{: caption="Section 5.4 Secrets manager benchmark results" caption-side="top"}

### 5.5 Extensible Admission Control
{: #cis-benchmark-15-5-5}

| # | Recommendation | Scored/Not Scored | Level | Result | Responsibility |
| --- | --- | --- | --- | --- | --- |
| 5.5.1 | Configure Image Provenance using ImagePolicyWebhook admission controller | Not Scored | 2 | [Fail](#ibm-remediations-and-explanations) | Shared |
{: summary="The rows are read from left to right. The first column is the section number for the benchmark recommendation. The second column is the benchmark recommendation. The third column is the scoring of the recommendation, either scored or not scored. The fourth column is the level of the recommendation, either 1 for basic or 2 for more advanced and performance-impacting. The fifth column contains the result of whether the service passes or fails the recommendation. The sixth column designates the responsibility of passing the recommendation, either IBM or shared between IBM and you."}
{: caption="Section 5.6 Extensible admission control benchmark results" caption-side="top"}

### 5.6 General Policies
{: #cis-benchmark-15-5-6}

| # | Recommendation | Scored/Not Scored | Level | Result | Responsibility |
| --- | --- | --- | --- | --- | --- |
| 5.6.1 | Create administrative boundaries between resources using namespaces | Not Scored | 1 | Pass | Shared |
| 5.6.2 | Ensure that the seccomp profile is set to docker/default in your pod definitions | Not Scored | 2 | [Fail](#ibm-remediations-and-explanations) | Shared |
| 5.6.3 | Apply Security Context to Your Pods and Containers | Not Scored | 2 | [Fail](#ibm-remediations-and-explanations) | Shared |
| 5.6.4 | The default namespace should not be used | Scored | 2 | Pass | Shared |

{: summary="The rows are read from left to right. The first column is the section number for the benchmark recommendation. The second column is the benchmark recommendation. The third column is the scoring of the recommendation, either scored or not scored. The fourth column is the level of the recommendation, either 1 for basic or 2 for more advanced and performance-impacting. The fifth column contains the result of whether the service passes or fails the recommendation. The sixth column designates the responsibility of passing the recommendation, either IBM or shared between IBM and you."}
{: caption="Explanation and remediation" caption-side="top"}

### {{site.data.keyword.IBM_notm}} Remediations and Explanations
{: #ibm-remediations-and-explanations}


| # | Remediation/Explanation |
| --- | --- |
| 1.2.1 | ROKS utilizes RBAC for cluster protection, but allows anonymous discovery, which is considered reasonable per [CIS Kubernetes Benchmark](https://www.cisecurity.org/benchmark/kubernetes/). |
| 1.2.10 | ROKS does not enable the [*EventRateLimit*](https://kubernetes.io/docs/reference/access-authn-authz/admission-controllers/#eventratelimit) admission controller since it is a Kubernetes alpha feature. |
| 1.2.12 | ROKS does not enable the [*AlwaysPullImages*](https://kubernetes.io/docs/reference/access-authn-authz/admission-controllers/#alwayspullimages) admission controller since it overrides a container's *imagePullPolicy* and may impact performance. |
| 1.2.13 | ROKS supports [pod security context constraints](/docs/openshift?topic=openshift-openshift_scc) which are similar to Kubernetes pod security policies. |
| 1.2.16 | ROKS supports [pod security context constraints](/docs/openshift?topic=openshift-openshift_scc) which are similar to Kubernetes pod security policies. |
| 1.2.22 | ROKS can optionally [enable Kubernetes API server auditing](/docs/openshift?topic=openshift-health-audit). |
| 1.2.23 | ROKS can optionally [enable Kubernetes API server auditing](/docs/openshift?topic=openshift-health-audit). |
| 1.2.24 | ROKS can optionally [enable Kubernetes API server auditing](/docs/openshift?topic=openshift-health-audit). |
| 1.2.25 | ROKS can optionally [enable Kubernetes API server auditing](/docs/openshift?topic=openshift-health-audit). |
| 1.2.33 | ROKS can optionally [enable a Kubernetes Key Management Service (KMS) provider](/docs/openshift?topic=openshift-encryption#kms). |
| 1.2.34 | ROKS can optionally [enable a Kubernetes Key Management Service (KMS) provider](/docs/openshift?topic=openshift-encryption#kms). |
| 3.2.1 | ROKS can optionally [enable Kubernetes API server auditing](/docs/openshift?topic=openshift-health-audit). |
| 3.2.2 | ROKS can optionally [enable Kubernetes API server auditing](/docs/openshift?topic=openshift-health-audit). |
| 4.2.6 | ROKS does not protect kernel defaults in order to allow customers to tune kernel parameters. |
| 4.2.8 | ROKS ensures that the hostname matches the name issued by the infrastructure. |
| 5.1.2 | ROKS deploys some system components that could have their Kubernetes secret access further restricted. |
| 5.1.3 | ROKS deploys some system components that could have their Kubernetes resource access further restricted. |
| 5.1.5 | ROKS does not set [*automountServiceAccountToken: false*](https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/#use-the-default-service-account-to-access-the-api-server) for each default service account. |
| 5.1.6 | ROKS deploys some system components that could set [*automountServiceAccountToken: false*](https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/#use-the-default-service-account-to-access-the-api-server). |
| 5.2.1 | ROKS can optionally [configure security context constraints](/docs/openshift?topic=openshift-openshift_scc). |
| 5.2.2 | ROKS can optionally [configure security context constraints](/docs/openshift?topic=openshift-openshift_scc). |
| 5.2.3 | ROKS can optionally [configure security context constraints](/docs/openshift?topic=openshift-openshift_scc). |
| 5.2.4 | ROKS can optionally [configure security context constraints](/docs/openshift?topic=openshift-openshift_scc). |
| 5.2.5 | ROKS can optionally [configure security context constraints](/docs/openshift?topic=openshift-openshift_scc). |
| 5.2.6 | ROKS can optionally [configure security context constraints](/docs/openshift?topic=openshift-openshift_scc). |
| 5.2.7 | ROKS can optionally [configure security context constraints](/docs/openshift?topic=openshift-openshift_scc). |
| 5.2.8 | ROKS can optionally [configure security context constraints](/docs/openshift?topic=openshift-openshift_scc). |
| 5.2.9 | ROKS can optionally [configure security context constraints](/docs/openshift?topic=openshift-openshift_scc). |
| 5.3.2 | ROKS has a set of [default Calico network policies defined](/docs/openshift?topic=openshift-network_policies#default_policy) and [additional network policies can optionally be added](/docs/openshift?topic=openshift-network_policies#adding_network_policies). |
| 5.4.1 | ROKS deploys some system components that could prefer using secrets as files over secrets as environment variables. |
| 5.4.2 | ROKS can optionally [enable a Kubernetes Key Management Service (KMS) provider](/docs/openshift?topic=openshift-encryption#kms). |
| 5.5.1 | ROKS can optionally [enable image security enforcement](/docs/openshift?topic=openshift-images#portieris-image-sec). |
| 5.6.2 | ROKS does not annotate all pods with [seccomp profiles](https://kubernetes.io/docs/concepts/policy/pod-security-policy/#seccomp). |
| 5.6.3 | ROKS deploys some system components that do not set a [pod or container *securityContext*](https://kubernetes.io/docs/tasks/configure-pod-container/security-context/). |
{: summary="The rows are read from left to right. The first column is the section number for the benchmark recommendation. The second column is the benchmark recommendation. The third column is the scoring of the recommendation, either scored or not scored. The fourth column is the level of the recommendation, either 1 for basic or 2 for more advanced and performance-impacting. The fifth column contains the result of whether the service passes or fails the recommendation. The sixth column designates the responsibility of passing the recommendation, either {{site.data.keyword.IBM_notm}} or shared between {{site.data.keyword.IBM_notm}} and you."}
{: caption="Explanation and remediation" caption-side="top"}








