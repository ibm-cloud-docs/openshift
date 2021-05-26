---

copyright:
  years: 2014, 2021
lastupdated: "2021-05-19"

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
  

# Classic clusters: Why does the OpenVPN server have an ingress IP address for NLB error?
{: #rhoks_ts_openvpn_subnet}

**Infrastructure provider**: <img src="../images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Classic

{: tsSymptoms}
When you run `ibmcloud oc cluster get -c <cluster_name_or_ID>`, you see the following error message in the **Master Status** field.
```
CAE003: Unable to determine the ingress IP address for the network load balancer.
```
{: screen}

Additionally, when you run `ibmcloud oc nlb-dns create` to create a subdomain for a network load balancer (NLB), the command might fail with a message that the cluster is not found, the input parameters are incorrect, or you do not have the required roles.

{: tsCauses}
The OpenVPN server could not be configured because load balancer IP address that exposes the default router could not be found. The router's load balancer service might not have been assigned an IP address because your cluster does not have a subnet with available portable IP addresses, or the load balancer setup did not complete.

{: tsResolve}
Verify that your cluster has available subnets, and that the load balancer setup completed successfully.

## Verifying that your cluster has available subnets
{: #verify_subnets}

1.  Check that your cluster has a **Subnet CIDR** for public and private subnets. If you set up a private VLAN-only cluster, you might have only a private subnet.
    ```
    ibmcloud oc cluster get --cluster <cluster_name_or_ID> --show-resources
    ```
    {: pre}

    Example output:
    ```
    Name:                           <cluster_name>   
    ...

    Subnet VLANs
    VLAN ID   Subnet CIDR        Public   User-managed   
    2345678   10.xxx.xx.xxx/29   false    false   
    2876543   169.xx.xxx.xxx/29  true     false
    ```
    {: screen}
2.  If the cluster does not have a subnet, [create a subnet for the cluster](/docs/openshift?topic=openshift-subnets#request) or [add an existing subnet from your account to the cluster](/docs/openshift?topic=openshift-subnets#add-existing).
3.  If the cluster does have a subnet, [check for available portable IP addresses](/docs/openshift?topic=openshift-subnets#review_ip) and if necessary, [add more portable IP address by adding a subnet](/docs/openshift?topic=openshift-subnets#adding_ips).
4.  Refresh the master to restart the OpenVPN setup so that it uses the available subnet.
    ```
    ibmcloud oc cluster master refresh --cluster <cluster_name_or_ID>
    ```
    {: pre}

## Verifying that the load balancer setup completed successfully
{: #verify_nlb}

1.  Check that the `ibm-cloud-provider-ip-*` pods for the load balancer are in a **Running** status.
    ```
    oc get pods -n ibm-system | grep ibm-cloud-provider-ip
    ```
    {: pre}
2.  If a pod is not running, review the **Events** in the pod details to troubleshoot the issue further.
    ```
    oc describe pod -n kube-system <pod_name>
    ```
    {: pre}
3.  After you resolve the load balancer pod issue, refresh the master to restart the NLB setup.
    ```
    ibmcloud oc cluster master refresh --cluster <cluster_name_or_ID>
    ```
    {: pre}
