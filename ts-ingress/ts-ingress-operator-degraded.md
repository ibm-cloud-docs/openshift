---

copyright:
  years: 2014, 2021
lastupdated: "2021-08-02"

keywords: openshift, roks, rhoks, rhos

subcollection: openshift
content-type: troubleshoot

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
{:c#: .ph data-hd-programlang='c#'}
{:c#: data-hd-programlang="c#"}
{:cli: .ph data-hd-interface='cli'}
{:codeblock: .codeblock}
{:curl: #curl .ph data-hd-programlang='curl'}
{:curl: .ph data-hd-programlang='curl'}
{:deprecated: .deprecated}
{:dotnet-standard: .ph data-hd-programlang='dotnet-standard'}
{:download: .download}
{:external: .external target="_blank"}
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
{:java: #java .ph data-hd-programlang='java'}
{:java: .ph data-hd-programlang='java'}
{:java: data-hd-programlang="java"}
{:javascript: .ph data-hd-programlang='javascript'}
{:javascript: data-hd-programlang="javascript"}
{:middle: .ph data-hd-position='middle'}
{:navgroup: .navgroup}
{:new_window: target="_blank"}
{:node: .ph data-hd-programlang='node'}
{:note .note}
{:note: .note}
{:note:.deprecated}
{:objectc data-hd-programlang="objectc"}
{:objectc: .ph data-hd-programlang='Objective C'}
{:org_name: data-hd-keyref="org_name"}
{:php: .ph data-hd-programlang='PHP'}
{:php: data-hd-programlang="php"}
{:pre: .pre}
{:preview: .preview}
{:python: .ph data-hd-programlang='python'}
{:python: data-hd-programlang="python"}
{:right: .ph data-hd-position='right'}
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
{:step: data-tutorial-type='step'} 
{:subsection: outputclass="subsection"}
{:support: data-reuse='support'}
{:swift: #swift .ph data-hd-programlang='swift'}
{:swift: .ph data-hd-programlang='swift'}
{:swift: data-hd-programlang="swift"}
{:table: .aria-labeledby="caption"}
{:term: .term}
{:terraform: .ph data-hd-interface='terraform'}
{:tip: .tip}
{:tooling-url: data-tooling-url-placeholder='tooling-url'}
{:topicgroup: .topicgroup}
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
  

# Why does the DNS Operator show a `RouteHealthDegraded` or `cannot marshal DNS message` error?
{: #ingress_subdomain}

**Infrastructure provider**:
  * <img src="../images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Classic
  * <img src="../images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> VPC

{: tsSymptoms}
You receive an error message similar to one of the following.

**Example error message when installing {{site.data.keyword.icp4dfull_notm}} from the console**
```sh
XXX.us-south.containers.appdomain.cloud: Get "http://image-registry-openshift-image-registry.ocp-data-privacy-prod-c-XXX.us-south.containers.appdomain.cloud/v2/": dial tcp: lookup image-registry-openshift-image-registry.ocp-data-privacy-prod-c-XXX.us-south.containers.appdomain.cloud on XXX.XX.X.XX:XX: cannot marshal DNS message
```
{: screen}

**Example `nslookup` error**
```sh
# nslookup XXX.XXX.databases.appdomain.cloud
Server:		XXX.XX.X.XX
Address:	XXX.XX.X.XX:XX

Non-authoritative answer:
*** Can't find XXX.XXX.databases.appdomain.cloud: Parse error

Non-authoritative answer:
*** Can't find XXX.XXX.databases.appdomain.cloud: Parse error
```
{: screen}

{: tsCauses}
The fix for [bug 1953097](https://bugzilla.redhat.com/show_bug.cgi?id=1970140){: external} enabled CoreDNS `bufsize` plugin responses of `1232` bytes. Some DNS resolvers can't receive responses greater than `512` bytes. Note that DNS resolvers that retry lookups using TCP, such as Dig, are not impacted. DNS clients that do not require UDP DNS messages to exceed 512 bytes are not impacted.


{: tsResolve}
1. [Update your cluster master](/docs/openshift?topic=openshift-update#master). For 4.6 clusters, update your master to version `4.6.38_openshift` or later. For 4.7 clusters, update your master to version `4.7.19_openshift` or later.
    ```sh
    ibmcloud oc cluster master update --cluster <clusterID> --version <4.6.38_openshift|4.7.19_openshift>
    ```
    {: pre}

1. After you update your master, run the `cluster get` command to get the cluster state and version and verify that the state is `deployed`.
    ```sh
    ibmcloud oc cluster get --cluster <clusterID>
    ```
    {: pre}

1. [Update your worker nodes](/docs/openshift?topic=openshift-update#master). For 4.6 clusters, update your worker nodes to version `4.6.38_openshift` or later. For 4.7 clusters, update your worker nodes to version `4.7.19_openshift` or later.

1. Get the details of the `openshift-dns` configmap and review the `bufsize` by running the following command. 
    ```sh
    oc get configmap -n openshift-dns dns-default -o yaml
    ```
    {: pre}

1. If the `bufsize` is still `1232`, get the name of the DNS Operator pod.
    ```sh
    oc get pods -n openshift-dns-operator
    ```
    {: pre}

    **Example output**
    ```sh
    NAME READY STATUS RESTARTS AGE
    dns-operator-111aa1aaab-xxxx1 2/2 Running 0 5h49m
    ```
    {: screen}

1. Delete the DNS Operator pod.
    ```sh
    oc delete pod <dns_operator_pod> -n openshift-dns-operator 
    ```
    {: pre}

1. Wait for the DNS pod to restart. Run `get pods` with the `--watch` flag to to verify that the pod is deployed.
    ```sh
    oc get pods -n openshift-dns --watch
    ```
    {: pre}

1. Verify that the DNS Operator pod is running.
    ```sh
    oc get pods -n openshift-dns-operator
    ```
    {: pre}

1. Get the configmap YAML and verify that the the `bufsize` is `512`. 
    ```sh
    oc get configmap -n openshift-dns dns-default -o yaml
    ```
    {: pre}

1. After a few minutes, verify that the DNS resolution works. If you see an `nslookup` error, retry the `nslookup`.

    ```sh
    / # nslookup XXX.XXX.databases.appdomain.cloud
    Server:		XXX.XX.X.XX
    Address:	XXX.XX.X.XX:XX

    Non-authoritative answer:
    XXX.XXX.databases.appdomain.cloud	canonical name = icd-prod-us-south-db-lm0sr.us-south.containers.appdomain.cloud
    icd-prod-us-south-db-lm0sr.us-south.containers.appdomain.cloud	canonical name = icd-prod-us-south-db-lm0sr.XXX.akadns.net

    Non-authoritative answer:
    XXX.XXX.databases.appdomain.cloud	canonical name = icd-prod-us-south-db-lm0sr.us-south.containers.appdomain.cloud
    icd-prod-us-south-db-lm0sr.us-south.containers.appdomain.cloud	canonical name = icd-prod-us-south-db-lm0sr.XXX.akadns.net
    Name:	icd-prod-us-south-db-lm0sr.XXX.akadns.net
    Address: XXX.XX.XXX.XX
    Name:	icd-prod-us-south-db-lm0sr.XXX.akadns.net
    Address: XXX.XX.X.XX
    Name:	icd-prod-us-south-db-lm0sr.XXX.akadns.net
    Address: XXX.XX.XXX.XXX
    ```
    {: codeblock}




