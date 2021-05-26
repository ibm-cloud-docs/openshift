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
  
  
# Version 3.11: Why does a connection via WebSocket close after 60 seconds?
{: #cs_ingress_websocket}

**Infrastructure provider and version**:
* <img src="../images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Classic
* <img src="../images/icon-version-311.png" alt="Version 3.11 icon" width="30" style="width:30px; border-style: none"/> {{site.data.keyword.openshiftshort}} version 3.11 clusters

{: tsSymptoms}
Your Ingress service exposes an app that uses a WebSocket. However, the connection between a client and your WebSocket app closes when no traffic is sent between them for 60 seconds.

{: tsCauses}
The connection to your WebSocket app might drop after 60 seconds of inactivity for one of the following reasons:

* Your Internet connection has a proxy or firewall that doesn't tolerate long connections.
* A timeout in the ALB to the WebSocket app terminates the connection.

{: tsResolve}
To prevent the connection from closing after 60 seconds of inactivity:

1. If you connect to your WebSocket app through a proxy or firewall, make sure the proxy or firewall isn't configured to automatically terminate long connections.

2. To keep the connection alive, you can increase the value of the timeout or set up a heartbeat in your app.
  * **Change the timeout**: Increase the value of the `proxy-read-timeout` in your ALB configuration. For example, to change the timeout from `60s` to a larger value like `300s`, add this [annotation](/docs/openshift?topic=openshift-comm-ingress-annotations#custom-connect-and-read-timeouts) to your Ingress resource file: `nginx.ingress.kubernetes.io/proxy-read-timeout: 300`. The timeout is changed for all public ALBs in your cluster.
  * **Set up a heartbeat**: If you don't want to change the ALB's default read timeout value, set up a heartbeat in your WebSocket app. When you set up a heartbeat protocol by using a framework like [WAMP](https://wamp-proto.org/){: external}, the app's upstream server periodically sends a "ping" message on a timed interval and the client responds with a "pong" message. Set the heartbeat interval to 58 seconds or less so that the "ping/pong" traffic keeps the connection open before the 60-second timeout is enforced.
