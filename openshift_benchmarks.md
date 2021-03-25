---

copyright:
  years: 2014, 2021
lastupdated: "2021-03-24"

keywords: openshift, roks

subcollection: openshift

---

{:DomainName: data-hd-keyref="APPDomain"}
{:DomainName: data-hd-keyref="DomainName"}
{:android: data-hd-operatingsystem="android"}
{:api: .ph data-hd-interface='api'}
{:apikey: data-credential-placeholder='apikey'}
{:app_key: data-hd-keyref="app_key"}
{:app_name: data-hd-keyref="app_name"}
{:app_secret: data-hd-keyref="app_secret"}
{:app_url: data-hd-keyref="app_url"}
{:authenticated-content: .authenticated-content}
{:beta: .beta}
{:c#: data-hd-programlang="c#"}
{:cli: .ph data-hd-interface='cli'}
{:codeblock: .codeblock}
{:curl: .ph data-hd-programlang='curl'}
{:deprecated: .deprecated}
{:dotnet-standard: .ph data-hd-programlang='dotnet-standard'}
{:download: .download}
{:external: target="_blank" .external}
{:faq: data-hd-content-type='faq'}
{:fuzzybunny: .ph data-hd-programlang='fuzzybunny'}
{:generic: data-hd-operatingsystem="generic"}
{:generic: data-hd-programlang="generic"}
{:gif: data-image-type='gif'}
{:go: .ph data-hd-programlang='go'}
{:help: data-hd-content-type='help'}
{:hide-dashboard: .hide-dashboard}
{:hide-in-docs: .hide-in-docs}
{:important: .important}
{:ios: data-hd-operatingsystem="ios"}
{:java: .ph data-hd-programlang='java'}
{:java: data-hd-programlang="java"}
{:javascript: .ph data-hd-programlang='javascript'}
{:javascript: data-hd-programlang="javascript"}
{:new_window: target="_blank"}
{:note .note}
{:note: .note}
{:objectc data-hd-programlang="objectc"}
{:org_name: data-hd-keyref="org_name"}
{:php: data-hd-programlang="php"}
{:pre: .pre}
{:preview: .preview}
{:python: .ph data-hd-programlang='python'}
{:python: data-hd-programlang="python"}
{:route: data-hd-keyref="route"}
{:row-headers: .row-headers}
{:ruby: .ph data-hd-programlang='ruby'}
{:ruby: data-hd-programlang="ruby"}
{:runtime: architecture="runtime"}
{:runtimeIcon: .runtimeIcon}
{:runtimeIconList: .runtimeIconList}
{:runtimeLink: .runtimeLink}
{:runtimeTitle: .runtimeTitle}
{:screen: .screen}
{:script: data-hd-video='script'}
{:service: architecture="service"}
{:service_instance_name: data-hd-keyref="service_instance_name"}
{:service_name: data-hd-keyref="service_name"}
{:shortdesc: .shortdesc}
{:space_name: data-hd-keyref="space_name"}
{:step: data-tutorial-type='step'}
{:subsection: outputclass="subsection"}
{:support: data-reuse='support'}
{:swift: .ph data-hd-programlang='swift'}
{:swift: data-hd-programlang="swift"}
{:table: .aria-labeledby="caption"}
{:term: .term}
{:tip: .tip}
{:tooling-url: data-tooling-url-placeholder='tooling-url'}
{:troubleshoot: data-hd-content-type='troubleshoot'}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:tsSymptoms: .tsSymptoms}
{:tutorial: data-hd-content-type='tutorial'}
{:ui: .ph data-hd-interface='ui'}
{:unity: .ph data-hd-programlang='unity'}
{:url: data-credential-placeholder='url'}
{:user_ID: data-hd-keyref="user_ID"}
{:vbnet: .ph data-hd-programlang='vb.net'}
{:video: .video}



# CIS Kubernetes Benchmark
{: #cis-benchmark}

The Center for Internet Security (CIS) publishes the [CIS Kubernetes Benchmark](https://www.cisecurity.org/benchmark/kubernetes/){: external} as a framework of specific steps to configure Kubernetes more securely and with standards that are commensurate to various industry regulations.
{: shortdesc}

When a new Kubernetes version is released as part of a [supported {{site.data.keyword.openshiftshort}} version](/docs/openshift?topic=openshift-openshift_versions#version_types), IBM engineers compare the default configuration of a cluster that runs that Kubernetes version against the benchmark and publishes the results in this documentation. You can review how specific versions of your {{site.data.keyword.openshiftlong}} clusters meet the CIS Kubernetes Benchmark.



## Running the worker node CIS Kubernetes benchmark
{: #cis-worker-test}

To review the results of the CIS Kubernetes benchmark for Section 4: Worker node security configuration, you can run the test yourself. Because you own the worker nodes and are partially [responsible](/docs/openshift?topic=openshift-responsibilities_iks) for their compliance, you might make configuration changes that you want to validate on your own.
{: shortdesc}

These steps apply to clusters that run {{site.data.keyword.openshiftshort}} version 4.5 or later only.
{: note}

Before you begin: [Log in to your account. If applicable, target the appropriate resource group. Set the context for your cluster.](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure)

1.  Create a project for the resources to run the benchmark.
    ```
    oc create ns ibm-kube-bench-test
    ```
    {: pre}
2.  Create a configmap with the `config` and `node` configuration files from the [kube-samples](https://github.com/IBM-Cloud/kube-samples/tree/master/cis-kube-benchmark/cis-1.5/ibm){: external} GitHub repository.
    1.  Download the the `config` and `node` configuration files into a local directory that is called `ibm`. You can also clone the repository and navigate into the `ibm` directory.
        * [`config` file](https://raw.githubusercontent.com/IBM-Cloud/kube-samples/master/cis-kube-benchmark/cis-1.5/ibm/config.yaml){: external}
        * [`node` file](https://raw.githubusercontent.com/IBM-Cloud/kube-samples/master/cis-kube-benchmark/cis-1.5/ibm/node.yaml){: external}
    2.  Create the configmap by using the `--from-file` flag to specify the `ibm` directory where your downloaded the configuration files.
        ```
        oc create cm kube-bench-node -n ibm-kube-bench-test --from-file ibm
        ```
        {: pre}
3.  Create a job to run the benchmark test based on the configurations that you previously created.
    ```
    oc apply -n ibm-kube-bench-test -f https://raw.githubusercontent.com/IBM-Cloud/kube-samples/master/cis-kube-benchmark/cis-1.5/ibm/job-node.yaml
    ```
    {: pre}
4.  Check that the job successfully completed.
    ```
    oc get pods -n ibm-kube-bench-test -l job-name=kube-bench-node
    ```
    {: pre}

    Example output:
    ```
    NAME                    READY   STATUS      RESTARTS   AGE
    kube-bench-node-hlvhc   0/1     Completed   0          23s
    ```
    {: screen}
5.  Review the CIS Kubernetes benchmark results for your worker nodes by checking the pod logs.
    ```
    oc logs -n ibm-kube-bench-test -l job-name=kube-bench-node --tail=-1
    ```
    {: pre}

    Example output:
    ```
    == Summary ==
    20 checks PASS
    2 checks FAIL
    1 checks WARN
    0 checks INFO
    ```
    {: screen}
6.  Optional: When you are done reviewing results, delete the resources that you created.
    ```
    oc delete ns ibm-kube-bench-test
    ```
    {: pre}

<br />

