---

copyright:
  years: 2014, 2021
lastupdated: "2021-08-13"

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
  

# Why does installing the Object storage `ibmc` Helm plug-in fail?
{: #cos_helm_fails}

**Infrastructure provider**:
* <img src="../images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Classic
* <img src="../images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> VPC


<img src="../images/icon-version-311.png" alt="Version 3.11 icon" width="30" style="width:30px; border-style: none"/> This troubleshooting topic applies only to {{site.data.keyword.openshiftshort}} clusters that run version 3.11.
{: note}



{: tsSymptoms}
When you install the {{site.data.keyword.cos_full_notm}} `ibmc` Helm plug-in, the installation fails with one of the following errors:
```sh
Error: symlink /Users/iks-charts/ibm-object-storage-plugin/helm-ibmc /Users/ibm/.helm/plugins/helm-ibmc: file exists
```
{: screen}

```sh
Error: fork/exec /home/iksadmin/.helm/plugins/helm-ibmc/ibmc.sh: permission denied
```
{: screen}

{: tsCauses}
When the `ibmc` Helm plug-in is installed, a symlink is created from the `~/.helm/plugins/helm-ibmc` directory for Linux systems or the `~/Library/helm/plugins/helm-ibmc` directory for Mac OS to the directory where the `ibmc` Helm plug-in is located on your local system, which is usually in `./ibmcloud-object-storage-plugin/helm-ibmc`. When you remove the `ibmc` Helm plug-in from your local system, or you move the `ibmc` Helm plug-in directory to a different location, the symlink is not removed.

If you see a `permission denied` error, you do not have the required `read`, `write`, and `execute` permission on the `ibmc.sh` bash file so that you can execute `ibmc` Helm plug-in commands.

{: tsResolve}

**For symlink errors**:

1. Remove the {{site.data.keyword.cos_full_notm}} Helm plug-in.
    **Linux**
    ```
    rm -rf ~/.helm/plugins/helm-ibmc
    ```
    {: pre}

    **Mac OS**
    ```
    rm -rf ~/Library/helm/plugins/helm-ibmc for macOS
    ```
    {: pre}

2. Follow the [documentation](/docs/openshift?topic=openshift-object_storage#install_cos) to re-install the `ibmc` Helm plug-in and the {{site.data.keyword.cos_full_notm}} plug-in.

**For permission errors**:

1. Change the permissions for the `ibmc` plug-in.
    **Linux**
    ```
    chmod 755 ~/.helm/plugins/helm-ibmc/ibmc.sh
    ```
    {: pre}

    **Mac OS**
    ```
    chmod 755 ~/Library/helm/plugins/helm-ibmc/ibmc.sh
    ```

2. Try out the `ibm` Helm plug-in.
    ```
    helm ibmc --help
    ```
    {: pre}

3. [Continue installing the {{site.data.keyword.cos_full_notm}} plug-in](/docs/openshift?topic=openshift-object_storage#install_cos).




