---

copyright:
  years: 2014, 2021
lastupdated: "2021-08-05"

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
{:audio: .audio}
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
{:note: .note}
{:note:.deprecated}
{:objectc: .ph data-hd-programlang='Objective C'}
{:objectc: data-hd-programlang="objectc"}
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
  
  
# Why is the status of my OpenShift Data Foundation storage cluster stuck at `Failed to reconcile`.
{: #ts-ocs-roks-debug}

**Infrastructure provider**:
* <img src="../images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Classic
* <img src="../images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> VPC

## ODF device set creation fails due to PVC names exceeding the Kubernetes character limit
{: #ocs-ts-sc-character-limit}

{: tsSymptoms}
When you create your ODF storage cluster and you run `oc describe storagecluster <storage-cluster-name>`, you see an error similar to the following.

```sh
ceph-cluster-controller: failed to reconcile. failed to reconcile cluster "ocs-storagecluster-cephcluster": failed to configure local ceph cluster: failed to create cluster: failed to start ceph osds: 3 failures encountered while running osds in namespace openshift-storage: failed to create "provision" job for node "ocs-deviceset-ibmc-vpc-block-metro-retain-10iops-tier-0-datnv6k". Job.batch "rook-ceph-osd-prepare-aaa000aaa111a1a0e10ba1a11aa1a119" is invalid: [spec.template.spec.volumes[8].name: Invalid value: "ocs-deviceset-ibmc-vpc-block-metro-retain-10iops-tier-0-aaaaa1b-bridge": must be no more than 63 characters
```
{: screen}

{: tsCauses}
Kubernetes PVC names must be fewer than 63 characters. If you a have multizone VPC cluster and create your ODF storage cluster by using a `retain` class like the `ibmc-vpc-block-metro-retain-10iops-tier`, the corresponding ODF device set PVCs that are created by using this storage class are assigned names that exceed the 63 character limit.

{: tsResolve}
Create a custom storage class that uses the same configuration as the pre-defined storage class that you want to use, but with a name that does not exceed 63 characters.

1. Get the YAML configuration of the storage class that you want to use in your ODF storage cluster and save it in a file on your local machine.
    ```sh
    oc get sc ibmc-vpc-block-metro-retain-10iops-tier -o yaml
    ```
    {: pre}

1. Edit the name of the storage class. Make sure that the name of your custom storage class is fewer than 30 characters to allow for the ODF storage cluster device set IDs to be under the 63 character kubernetes limit. Create the storage class in your cluster.
    ```sh
    oc create -f <custom-storage-class.yaml>
    ```
    {: pre}

1. Clean up your [ODF deployment](/docs/openshift?topic=openshift-ocs-manage-deployment#ocs-rm-cleanup-resources).

1. Create an ODF deployment that uses the custom storage class you created.
