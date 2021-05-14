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
 

# Common issues with worker nodes
{: #common_worker_nodes_issues}

Review common error messages and learn how to resolve them. Messages might begin with the prefix, `'<provider>' infrastructure exception:`, where `<provider>` identifies which infrastructure provider the worker node uses.
{: shortdesc}

**Infrastructure provider**:
  * <img src="../../images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Classic
  * <img src="../../images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> VPC

  <table summary="The columns are read from left to right. The first column has the error message. The second column describes the error and provides resolution steps.">
  <caption>Common error messages</caption>
    <col width="25%">
    <thead>
    <th>Error message</th>
    <th>Description and resolution</th>
    </thead>
    <tbody>
      <tr>
        <td>Your account is currently prohibited from ordering 'Computing Instances'.</td>
        <td>Your IBM Cloud infrastructure account might be restricted from ordering compute resources. Contact {{site.data.keyword.cloud_notm}} support by opening an [{{site.data.keyword.cloud_notm}} support case](/docs/containers?topic=containers-get-help).</td>
      </tr>
      <tr>
      <td>Could not place order.<br><br>
      Could not place order. There are insufficient resources behind router 'router_name' to fulfill the request for the following guests: 'worker_id'.</td>
      <td>The zone that you selected might not have enough infrastructure capacity to provision your worker nodes. Or you might have exceeded a limit in your IBM Cloud infrastructure account. To resolve, try one of the following options:
      <ul><li>Infrastructure resource availability in zones can fluctuate often. Wait a few minutes and try again.</li>
      <li>For a single zone cluster, create the cluster in a different zone. For a multizone cluster, add a zone to the cluster.</li>
      <li>Specify a different pair of public and private VLANs for your worker nodes in your IBM Cloud infrastructure account. For worker nodes that are in a worker pool, you can use the <code>ibmcloud oc zone network-set</code> [command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_zone_network_set).</li>
      <li>Contact your IBM Cloud infrastructure account manager to verify that you do not exceed an account limit, such as a global quota.</li>
      <li>Open an [IBM Cloud infrastructure support case](/docs/containers?topic=containers-get-help)</li></ul></td>
      </tr>
      <tr>
        <td>Could not obtain network VLAN with ID: <code>&lt;vlan id&gt;</code>.</td>
        <td>Your worker node could not be provisioned because the selected VLAN ID could not be found for one of the following reasons:<ul><li>You might have specified the VLAN number instead of the VLAN ID. The VLAN number is 3 or 4 digits long, whereas the VLAN ID is 7 digits long. Run <code>ibmcloud oc vlan ls --zone &lt;zone&gt;</code> to retrieve the VLAN ID.<li>The VLAN ID might not be associated with the IBM Cloud infrastructure account that you use. Run <code>ibmcloud oc vlan ls --zone &lt;zone&gt;</code> to list available VLAN IDs for your account. To change the IBM Cloud infrastructure account, see [`ibmcloud oc credential set`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_credentials_set). </ul></td>
      </tr>
      <tr>
        <td>The location provided for this order is invalid.</td>
        <td>Your IBM Cloud infrastructure is not set up to order compute resources in the selected data center. Contact [{{site.data.keyword.cloud_notm}} support](/docs/containers?topic=containers-get-help) to verify that you account is set up correctly.</td>
       </tr>
       <tr>
        <td>The user does not have the necessary {{site.data.keyword.cloud_notm}} classic infrastructure permissions to add servers
        </br></br>
        'Item' must be ordered with permission.
        </br></br>
        The IBM Cloud infrastructure credentials could not be validated.<br><br>
        '<Provider>' infrastructure request not authorized</td>
        <td>You might not have the required permissions to perform the action in your IBM Cloud infrastructure portfolio, or you are using the wrong infrastructure credentials. See [Setting up the API key to enable access to the infrastructure portfolio](/docs/containers?topic=containers-users#api_key).</td>
      </tr>
      <tr>
       <td>Worker unable to talk to {{site.data.keyword.containerlong_notm}} servers. Please verify your firewall setup is allowing traffic from this worker.
       <td><ul><li>If you have a firewall, [configure your firewall settings to allow outgoing traffic to the appropriate ports and IP addresses](/docs/containers?topic=containers-firewall#firewall_outbound).</li></ul></td>
     </tr>
  <tr>
    <td>The worker did not respond to the soft reboot request. A hard reboot might be necessary.</td>
    <td>Although you issued a reboot on your worker node, the worker node is unresponsive. You can rerun the [reboot command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_reboot) with the `--hard` flag to power off the worker node, or run the `worker reload` [command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_reload).</td>
  </tr>
      <tr>
  <td>Cannot create IMS portal token, as no IMS account is linked to the selected BSS account</br></br>Provided user not found or active</br></br>User account is currently cancel_pending.</br></br>The worker node instance '&lt;ID&gt;' cannot be found. Review '&lt;provider&gt;' infrastructure user permissions.<br><br>The worker node instance cannot be found. Review '&lt;provider&gt;' infrastructure user permissions.<br><br>The worker node instance cannot be identified. Review '&lt;provider&gt;' infrastructure user permissions.</td>
  <td>The owner of the API key that is used to access the IBM Cloud infrastructure portfolio does not have the required permissions to perform the action, or might be pending deletion.</br></br><strong>As the user</strong>, follow these steps:
  <ol><li>If you have access to multiple accounts, make sure that you are logged in to the account where you want to work with {{site.data.keyword.openshiftlong_notm}}. </li>
  <li>Run <code>ibmcloud oc api-key info --cluster &lt;cluster_name_or_ID&gt;</code> to view the current API key owner that is used to access the IBM Cloud infrastructure portfolio. </li>
  <li>Run <code>ibmcloud account list</code> to view the owner of the {{site.data.keyword.cloud_notm}} account that you currently use. </li>
  <li>Contact the owner of the {{site.data.keyword.cloud_notm}} account and report that the API key owner has insufficient permissions in IBM Cloud infrastructure or might be pending to be deleted. </li></ol>
  </br><strong>As the account owner</strong>, follow these steps:
  <ol><li>Review the [required classic permissions in IBM Cloud infrastructure](/docs/containers?topic=containers-users#infra_access) to perform the action that previously failed. For the VPC infrastructure provider, the API key owner must have the **Administrator** platform access role.</li>
  <li>Fix the permissions of the API key owner or create a new API key by using the [<code>ibmcloud oc api-key reset --region &lt;region&gt;</code>](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_api_key_reset) command. </li>
  <li>If you or another account admin manually set IBM Cloud infrastructure credentials in your account, run [<code>ibmcloud oc credential unset --region &lt;region&gt;</code>](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_credentials_unset) to remove the credentials from your account.</li></ol></td>
  </tr>
    </tbody>
  </table>


