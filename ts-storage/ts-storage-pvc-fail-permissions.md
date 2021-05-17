---

copyright:
  years: 2014, 2021
lastupdated: "2021-05-14"

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
 

# What permissions do I need to manage storage and create PVCs?
{: #missing_permissions}

**Infrastructure provider**:
* <img src="../../images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Classic
* <img src="../../images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> VPC

{: tsSymptoms}
When you create a PVC, the PVC remains pending. When you run `oc describe pvc <pvc_name>`, you see an error message similar to the following:

```
User doesn't have permissions to create or manage Storage
```
{: screen}

{: tsCauses}
The IAM API key or the IBM Cloud infrastructure API key that is stored in the `storage-secret-store` Kubernetes secret of your cluster  does not have all the required permissions to provision persistent storage.

{: tsResolve}
1. Retrieve the IAM key or IBM Cloud infrastructure API key that is stored in the `storage-secret-store` Kubernetes secret of your cluster and verify that the correct API key is used.
   ```
   oc get secret storage-secret-store -n kube-system -o yaml | grep slclient.toml: | awk '{print $2}' | base64 --decode
   ```
   {: pre}

   Example output:
   ```
   [Bluemix]
   iam_url = "https://iam.bluemix.net"
   iam_client_id = "bx"
   iam_client_secret = "bx"
   iam_api_key = "<iam_api_key>"
   refresh_token = ""
   pay_tier = "paid"
   containers_api_route = "https://us-south.containers.bluemix.net"

   [Softlayer]
   encryption = true
   softlayer_username = ""
   softlayer_api_key = ""
   softlayer_endpoint_url = "https://api.softlayer.com/rest/v3"
   softlayer_iam_endpoint_url = "https://api.softlayer.com/mobile/v3"
   softlayer_datacenter = "dal10"
   ```
   {: screen}

   The IAM API key is listed in the `Bluemix.iam_api_key` section of your CLI output. If the `Softlayer.softlayer_api_key` is empty at the same time, then the IAM API key is used to determine your infrastructure permissions. The IAM API key is automatically set by the user who runs the first action that requires the IAM **Administrator** platform access role in a resource group and region. If a different API key is set in `Softlayer.softlayer_api_key`, then this key takes precedence over the IAM API key. The `Softlayer.softlayer_api_key` is set when a cluster admin runs the `ibmcloud oc credentials-set` command.

2. If you want to change the credentials, update the API key that is used.
    1.  To update the IAM API key, use the `ibmcloud oc api-key reset` [command](/docs/containers?topic=containers-cli-plugin-kubernetes-service-cli#cs_api_key_reset). To update the IBM Cloud infrastructure key, use the `ibmcloud oc credential set` [command](/docs/containers?topic=containers-cli-plugin-kubernetes-service-cli#cs_credentials_set).
    2. Wait about 10 - 15 minutes for the `storage-secret-store` Kubernetes secret to update, then verify that the key is updated.
       ```
       oc get secret storage-secret-store -n kube-system -o yaml | grep slclient.toml: | awk '{print $2}' | base64 --decode
       ```
       {: pre}

3. If the API key is correct, verify that the key has the correct permission to provision persistent storage.
   1. Contact the account owner to verify the permission of the API key.
   2. As the account owner, select **Manage** > **Access (IAM)** from the navigation in the {{site.data.keyword.cloud_notm}} console.
   3. Select **Users** and find the user whose API key you want to use.
   4. From the actions menu, select **Manage user details**.
   5. Go to the **Classic infrastructure** tab.
   6. Expand the **Account** category and verify that the **Add/ Upgrade Storage (Storage Layer)** permission is assigned.
   7. Expand the **Services** category and verify that the **Storage Manage** permission is assigned.
4. Remove the PVC that failed.
   ```
   oc delete pvc <pvc_name>
   ```
   {: pre}

5. Re-create the PVC.
   ```
   oc apply -f pvc.yaml
   ```
   {: pre}
