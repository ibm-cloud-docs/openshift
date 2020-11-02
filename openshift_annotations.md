---

copyright:
  years: 2014, 2020
lastupdated: "2020-11-02"

keywords: openshift, roks, rhoks, rhos, nginx, ingress controller, annotations

subcollection: openshift

---

{:DomainName: data-hd-keyref="APPDomain"}
{:DomainName: data-hd-keyref="DomainName"}
{:android: data-hd-operatingsystem="android"}
{:apikey: data-credential-placeholder='apikey'}
{:app_key: data-hd-keyref="app_key"}
{:app_name: data-hd-keyref="app_name"}
{:app_secret: data-hd-keyref="app_secret"}
{:app_url: data-hd-keyref="app_url"}
{:authenticated-content: .authenticated-content}
{:beta: .beta}
{:c#: data-hd-programlang="c#"}
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
{:java: #java .ph data-hd-programlang='java'}
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
{:swift: #swift .ph data-hd-programlang='swift'}
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
{:unity: .ph data-hd-programlang='unity'}
{:url: data-credential-placeholder='url'}
{:user_ID: data-hd-keyref="user_ID"}
{:vb.net: .ph data-hd-programlang='vb.net'}
{:video: .video}



# {{site.data.keyword.openshiftlong_notm}} Ingress annotations
{: #ingress_annotation}

To add capabilities to your Ingress application load balancer (ALB), you can specify annotations as metadata in an Ingress resource.
{: shortdesc}



<img src="images/icon-version-43.png" alt="Version 4 icon" width="30" style="width:30px; border-style: none"/> These custom {{site.data.keyword.openshiftlong_notm}} annotations (`ingress.bluemix.net/<annotation>`) and Kubernetes NGINX annotations (`nginx.ingress.kubernetes.io/<annotation>`) are not supported for the router or the Ingress resource in {{site.data.keyword.openshiftshort}} version 4. If you want to customize routing rules for apps in a cluster that runs {{site.data.keyword.openshiftshort}} version 4, you can use [HAProxy annotations for the {{site.data.keyword.openshiftshort}} router](https://docs.openshift.com/container-platform/4.3/networking/routes/route-configuration.html#nw-route-specific-annotations_route-configuration){: external} that manages traffic for your app. These supported annotations are in the format `haproxy.router.openshift.io/<annotation>` or `router.openshift.io/<annotation>`. To add annotations to the router, run `oc edit svc router-default -n openshift-ingress`.
{: important}

<img src="images/icon-version-311.png" alt="Version 3.11 icon" width="30" style="width:30px; border-style: none"/> In {{site.data.keyword.openshiftshort}} version 3.11 clusters, these custom {{site.data.keyword.openshiftlong_notm}} annotations (`ingress.bluemix.net/<annotation>`) are applicable for ALBs that run the {{site.data.keyword.openshiftlong_notm}} Ingress image only. If your ALBs run the [Kubernetes Ingress image instead](/docs/openshift?topic=openshift-ingress-types), these custom annotations are not supported. You must instead use [Kubernetes NGINX annotations](https://kubernetes.github.io/ingress-nginx/user-guide/nginx-configuration/annotations/){: external} (`nginx.ingress.kubernetes.io/<annotation>`) in your Ingress resources.
{: important}




|General annotations|Name|Description|
|-------------------|----|-----------|
| [Custom error actions](#custom-errors) | `custom-errors, custom-error-actions` | Indicate custom actions that the ALB can take for specific HTTP errors. |
| [Location snippets](#location-snippets) | `location-snippets` | Add a custom location block configuration for a service. |
| [Private ALB routing](#alb-id) | `ALB-ID` | Route incoming requests to your apps with a private ALB. |
| [Server snippets](#server-snippets) | `server-snippets` | Add a custom server block configuration. |
{: caption="General annotations" caption-side="top"}

<br>

|Connection annotations|Name|Description|
|----------------------|----|-----------|
| [Custom connect-timeouts and read-timeouts](#proxy-connect-timeout) | `proxy-connect-timeout, proxy-read-timeout` | Set the time that the ALB waits to connect to and read from the back-end app before the back-end app is considered unavailable. |
| [Keepalive requests](#keepalive-requests) | `keepalive-requests` | Set the maximum number of requests that can be served through one keepalive connection. |
| [Keepalive timeout](#keepalive-timeout) | `keepalive-timeout` | Set the maximum time that a keepalive connection stays open between the client and the ALB proxy server. |
| [Proxy next upstream](#proxy-next-upstream-config) | `proxy-next-upstream-config` | Set when the ALB can pass a request to the next upstream server. |
| [Session-affinity with cookies](#sticky-cookie-services) | `sticky-cookie-services` | Always route incoming network traffic to the same upstream server by using a sticky cookie. |
| [Upstream fail timeout](#upstream-fail-timeout) | `upstream-fail-timeout` | Set the amount of time during which the ALB can attempt to connect to the server before the server is considered unavailable. |
| [Upstream keepalive](#upstream-keepalive) | `upstream-keepalive` | Set the maximum number of idle keepalive connections for an upstream server. |
| [Upstream keepalive timeout](#upstream-keepalive-timeout) | `upstream-keepalive-timeout` | Set the maximum time that a keepalive connection stays open between the ALB proxy server and your app's upstream server. |
| [Upstream max fails](#upstream-max-fails) | `upstream-max-fails` | Set the maximum number of unsuccessful attempts to communicate with the server before the server is considered unavailable. |
{: caption="Connection annotations" caption-side="top"}

<br>

|HTTPS and TLS/SSL authentication annotations|Name|Description|
|--------------------------------------------|----|-----------|
| [Custom HTTP and HTTPS ports](#custom-port) | `custom-port` | Change the default ports for HTTP (port 80) and HTTPS (port 443) network traffic. |
| [HTTP redirects to HTTPS](#redirect-to-https) | `redirect-to-https` | Redirect insecure HTTP requests on your domain to HTTPS. |
| [HTTP Strict Transport Security (HSTS)](#hsts) | `hsts` | Set the browser to access the domain only by using HTTPS. |
| [Mutual authentication](#mutual-auth) | `mutual-auth` | Configure mutual authentication for the ALB. |
| [SSL services support](#ssl-services) | `ssl-services` | Allow SSL services support to encrypt traffic to your upstream apps that require HTTPS. |
| [TCP ports](#tcp-ports) | `tcp-ports` | Access an app via a non-standard TCP port.|
{: caption="HTTPS and TLS/SSL authentication annotations" caption-side="top"}

<br>

|Path routing annotations|Name|Description|
|------------------------|----|-----------|
| [External services](#proxy-external-service) | `proxy-external-service` | Add path definitions to external services, such as a service hosted in {{site.data.keyword.cloud_notm}}. |
| [Location modifier](#location-modifier) | `location-modifier` | Modify the way the ALB matches the request URI against the app path. |
| [Rewrite paths](#rewrite-path) | `rewrite-path` | Route incoming network traffic to a different path that your back-end app listens on. |
{: caption="Path routing annotations" caption-side="top"}

<br>

|Proxy buffer annotations|Name|Description|
|------------------------|----|-----------|
| [Large client header buffers](#large-client-header-buffers) | `large-client-header-buffers` | Set the maximum number and size of buffers that read large client request headers. |
| [Client response data buffering](#proxy-buffering) | `proxy-buffering` | Disable the buffering of a client response on the ALB while sending the response to the client. |
| [Proxy buffers](#proxy-buffers) | `proxy-buffers` | Set the number and size of the buffers that read a response for a single connection from the proxied server. |
| [Proxy buffer size](#proxy-buffer-size) | `proxy-buffer-size` | Set the size of the buffer that reads the first part of the response that is received from the proxied server. |
| [Proxy busy buffers size](#proxy-busy-buffers-size) | `proxy-busy-buffers-size` | Set the size of proxy buffers that can be busy. |
{: caption="Proxy buffer annotations" caption-side="top"}

<br>

|Request and response annotations|Name|Description|
|--------------------------------|----|-----------|
| [Add server port to host header](#add-host-port) | `add-host-port` | Add the server port to the host for routing requests. |
| [Client request body size](#client-max-body-size) | `client-max-body-size` | Set the maximum size of the body that the client can send as part of a request. |
| [Additional client request or response header](#proxy-add-headers) | `proxy-add-headers, response-add-headers` | Add header information to a client request before forwarding the request to your back-end app or to a client response before sending the response to the client. |
| [Client response header removal](#response-remove-headers) | `response-remove-headers` | Remove header information from a client response before forwarding the response to the client. |
{: caption="Request and response annotations" caption-side="top"}

<br>

|Service limit annotations|Name|Description|
|------------------------|----|-----------|
| [Global rate limits](#global-rate-limit) | `global-rate-limit` | Limit the request processing rate and number of connections per a defined key for all services. |
| [Service rate limits](#service-rate-limit) | `service-rate-limit` | Limit the request processing rate and the number of connections per a defined key for specific services. |
{: caption="Service limit annotations" caption-side="top"}

<br>

|User authentication annotations|Name|Description|
|-------------------------------|----|-----------|
| [{{site.data.keyword.appid_short}} Authentication](#appid-auth) | `appid-auth` | Use {{site.data.keyword.appid_full}} to authenticate with your app. |
{: caption="User authentication annotations" caption-side="top"}

<br>

## General annotations
{: #general}

### Custom error actions (`custom-errors`, `custom-error-actions`)
{: #custom-errors}

Indicate custom actions that the ALB can take for specific HTTP errors.
{: shortdesc}

**Description**

To handle specific HTTP errors that might occur, you can set up custom error actions for the ALB to take.

* The `custom-errors` annotation defines the service name, the HTTP error to handle, and the name of the error action that the ALB takes when it encounters the specified HTTP error for the service.
* The `custom-error-actions` annotation defines custom error actions in NGINX code snippets.

For example, in the `custom-errors` annotation, you can set up the ALB to handle `401` HTTP errors for `app1` by returning a custom error action called `/errorAction401`. Then, in the `custom-error-actions` annotation, you can define a code snippet that is called `/errorAction401` so that the ALB returns a custom error page to the client.</br>

You can also use the `custom-errors` annotation to redirect the client to an error service that you manage. You must define the path to this error service in the `paths` section of the Ingress resource file.

**Sample Ingress resource YAML**


```yaml
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: myingress
  annotations:
    ingress.bluemix.net/custom-errors: "serviceName=<app1> httpError=<401> errorActionName=</errorAction401>;serviceName=<app2> httpError=<403> errorActionName=</errorPath>"
    ingress.bluemix.net/custom-error-actions: |
      errorActionName=</errorAction401>
      #Example custom error snippet
      proxy_pass http://example.com/forbidden.html;
      <EOS>
  spec:
    tls:
    - hosts:
      - mydomain
      secretName: mysecret
    rules:
    - host: mydomain
      http:
        paths:
        - path: /path1
          backend:
            serviceName: app1
            servicePort: 80
        - path: /path2
          backend:
            serviceName: app2
            servicePort: 80
        - path: </errorPath>
          backend:
            serviceName: <error-svc>
            servicePort: 80
```
{: codeblock}

|Annotation field|Value|
|----------------|-----|
| `serviceName` | Replace `<app1>` with the name of the Kubernetes service that the custom error applies to. The custom error applies only to the specific paths that use this same upstream service. If you do not set a service name, then the custom errors are applied to all service paths. |
| `httpError` | Replace `<401>` with the HTTP error code that you want to handle with a custom error action. |
| `errorActionName` | Replace `</errorAction401>` with the name of a custom error action to take or the path to an error service.<ul><li>If you specify the name of a custom error action, you must define that error action in a code snippet in the `custom-error-actions` annotation. In the sample YAML, `app1` uses `/errorAction401`, which is defined in the snippet in the `custom-error-actions` annotation.</li><li>If you specify the path to an error service, you must specify that error path and the name of the error service in the `paths` section. In the sample YAML, `app2` uses `/errorPath`, which is defined at the end of the `paths` section.</li></ul> |
| `ingress.bluemix.net/custom-error-actions` | Define a custom error action that the ALB takes for the service and HTTP error that you specified. Use an NGINX code snippet and end each snippet with `<EOS>`. In the sample YAML, the ALB passes a custom error page, `http://example.com/forbidden.html`, to the client when a `401` error occurs for `app1`.|
{: caption="Understanding the annotation components" caption-side="top"}

<br />

### Location snippets (`location-snippets`)
{: #location-snippets}

Add a custom location block configuration for a service.
{: shortdesc}

**Description**

A server block is an NGINX directive that defines the configuration for the ALB virtual server. A location block is an NGINX directive defined within the server block. Location blocks define how Ingress processes the request URI, or the part of the request that comes after the domain name or IP address and port.

When a server block receives a request, the location block matches the URI to a path and the request is forwarded to the IP address of the pod where the app is deployed. By using the `location-snippets` annotation, you can modify how the location block forwards requests to particular services.

To modify the server block as a whole instead, see the [`server-snippets`](#server-snippets) annotation.

To view server and location blocks in the NGINX configuration file, run the following command for one of your ALB pods: `oc exec -ti <alb_pod> -n kube-system -c nginx-ingress -- cat ./etc/nginx/conf.d/<kubernetes_namespace>-<ingress_resource_name>.conf`
{: tip}

**Sample Ingress resource YAML**


```yaml
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: myingress
  annotations:
    ingress.bluemix.net/location-snippets: |
      serviceName=<myservice1>
      # Example location snippet
      proxy_request_buffering off;
      rewrite_log on;
      proxy_set_header "x-additional-test-header" "location-snippet-header";
      <EOS>
      serviceName=<myservice2>
      proxy_set_header Authorization "";
      <EOS>
spec:
  tls:
  - hosts:
    - mydomain
    secretName: mytlssecret
  rules:
  - host: mydomain
    http:
      paths:
      - path: /
        backend:
          serviceName: myservice
          servicePort: 8080
```
{: codeblock}

|Annotation field|Value|
|----------------|-----|
| `serviceName` | Replace `<myservice>` with the name of the service that you created for your app. |
| Location snippet | Provide the configuration snippet that you want to use for the specified service. The sample snippet for the `myservice1` service configures the location block to turn off proxy request buffering, turn on log rewrites, and set additional headers when it forwards a request to the service. The sample snippet for the `myservice2` service sets an empty `Authorization` header. Every location snippet must end with the value `<EOS>`. |
{: caption="Understanding the annotation components" caption-side="top"}

<br />

### Private ALB routing (`ALB-ID`)
{: #alb-id}

Route incoming requests to your apps with a private ALB.
{: shortdesc}

**Description**

Choose a private ALB to route incoming requests instead of the public ALB.

**Sample Ingress resource YAML**

```yaml
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: myingress
  annotations:
    ingress.bluemix.net/ALB-ID: "<private_ALB_ID_1>;<private_ALB_ID_2>"
spec:
  tls:
  - hosts:
    - mydomain
    secretName: mytlssecret
  rules:
  - host: mydomain
    http:
      paths:
      - path: /
        backend:
          serviceName: myservice
          servicePort: 8080
```
{: codeblock}

|Annotation field|Value|
|----------------|-----|
| `<private_ALB_ID>` | The ID for your private ALB. To find the private ALB ID, run `ibmcloud oc ingress alb ls --cluster <my_cluster>`. If you have a multizone cluster with more than one private ALB enabled, you can provide a list of ALB IDs separated by `;`. For example: `ingress.bluemix.net/ALB-ID: <private_ALB_ID_1>;<private_ALB_ID_2>;<private_ALB_ID_3>` |
{: caption="Understanding the annotation components" caption-side="top"}

<br />

### Server snippets (`server-snippets`)
{: #server-snippets}

Add a custom server block configuration.
{: shortdesc}

**Description**

A server block is an NGINX directive that defines the configuration for the ALB virtual server. By providing a custom configuration snippet in the `server-snippets` annotation, you can modify how the ALB handles requests at the server level.

To view server and location blocks in the NGINX configuration file, run the following command for one of your ALB pods: `oc exec -ti <alb_pod> -n kube-system -c nginx-ingress -- cat ./etc/nginx/conf.d/<kubernetes_namespace>-<ingress_resource_name>.conf`
{: tip}

**Sample Ingress resource YAML**


```yaml
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: myingress
  annotations:
    ingress.bluemix.net/server-snippets: |
      # Example snippet
      location = /health {
      return 200 'Healthy';
      add_header Content-Type text/plain;
      }
spec:
  tls:
  - hosts:
    - mydomain
    secretName: mytlssecret
  rules:
  - host: mydomain
    http:
      paths:
      - path: /
        backend:
          serviceName: myservice
          servicePort: 8080
```
{: codeblock}

|Annotation field|Value|
|----------------|-----|
| Server snippet | Provide the configuration snippet that you want to use. This sample snippet specifies a location block to handle `/health` requests. The location block is configured to return a healthy response and add a header when it forwards a request. |
{: caption="Understanding the annotation components" caption-side="top"}

You can use the `server-snippets` annotation to add a header for all service responses at a server level:
{: tip}

```yaml
annotations:
  ingress.bluemix.net/server-snippets: |
    add_header <header1> <value1>;
```
{: codeblock}

<br />

## Connection annotations
{: #connection}

With connection annotations, you can change how the ALB connects to the back-end app and upstream-servers, and set timeouts or a maximum number of keepalive connections before the app or server is considered to be unavailable.
{: shortdesc}

### Custom connect-timeouts and read-timeouts (`proxy-connect-timeout`, `proxy-read-timeout`)
{: #proxy-connect-timeout}

Set the time that the ALB waits to connect to and read from the back-end app before the back-end app is considered unavailable.
{: shortdesc}

**Description**

When a client request is sent to the Ingress ALB, a connection to the back-end app is opened by the ALB. By default, the ALB waits 60 seconds to receive a reply from the back-end app. If the back-end app does not reply within 60 seconds, then the connection request is aborted and the back-end app is considered to be unavailable.

After the ALB is connected to the back-end app, response data is read from the back-end app by the ALB. During this read operation, the ALB waits a maximum of 60 seconds between two read operations to receive data from the back-end app. If the back-end app does not send data within 60 seconds, the connection to the back-end app is closed and the app is considered to be not available.

A 60 second connect-timeout and read-timeout are the default timeouts on a proxy and usually should not be changed.

If the availability of your app is not steady or your app is slow to respond because of high workloads, you might want to increase the connect-timeout or read-timeout. Keep in mind that increasing the timeout impacts the performance of the ALB as the connection to the back-end app must stay open until the timeout is reached.

On the other hand, you can decrease the timeout to gain performance on the ALB. Ensure that your back-end app is able to handle requests within the specified timeout, even during higher workloads.

**Sample Ingress resource YAML**

```yaml
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
 name: myingress
 annotations:
   ingress.bluemix.net/proxy-connect-timeout: "serviceName=<myservice> timeout=<connect_timeout>"
   ingress.bluemix.net/proxy-read-timeout: "serviceName=<myservice> timeout=<read_timeout>"
spec:
 tls:
 - hosts:
   - mydomain
   secretName: mytlssecret
 rules:
 - host: mydomain
   http:
     paths:
     - path: /
       backend:
         serviceName: myservice
         servicePort: 8080
```
{: codeblock}

|Annotation field|Value|
|----------------|-----|
| `<connect_timeout>` | The number of seconds or minutes to wait to connect to the back-end app, for example `65s` or `1m`. A connect-timeout cannot exceed 75 seconds. |
| `<read_timeout>` | The number of seconds or minutes to wait before the back-end app is read, for example `65s` or `2m`.|
{: caption="Understanding the annotation components" caption-side="top"}

<br />

### Keepalive requests (`keepalive-requests`)
{: #keepalive-requests}

**Description**

Sets the maximum number of requests that can be served through one keepalive connection.

**Sample Ingress resource YAML**

```yaml
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: myingress
  annotations:
    ingress.bluemix.net/keepalive-requests: "serviceName=<myservice> requests=<max_requests>"
spec:
  tls:
  - hosts:
    - mydomain
    secretName: mytlssecret
  rules:
  - host: mydomain
    http:
      paths:
      - path: /
        backend:
          serviceName: <myservice>
          servicePort: 8080
```
{: codeblock}


|Annotation field|Value|
|----------------|-----|
| `serviceName` | Replace `<myservice>` with the name of the Kubernetes service that you created for your app. This parameter is optional. The configuration is applied to all of the services in the Ingress subdomain unless a service is specified. If the parameter is provided, the keepalive requests are set for the given service. If the parameter is not provided, the keepalive requests are set at the server level of the `nginx.conf` for all the services that do not have the keepalive requests configured. |
| `requests` | Replace `<max_requests>` with the maximum number of requests that can be served through one keepalive connection. |
{: caption="Understanding the annotation components" caption-side="top"}

<br />

### Keepalive timeout (`keepalive-timeout`)
{: #keepalive-timeout}

**Description**

Sets the maximum time that a keepalive connection stays open between the client and the ALB proxy server. If you do not use this annotation, the default timeout value is `60s`.

**Sample Ingress resource YAML**

```yaml
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
 name: myingress
 annotations:
   ingress.bluemix.net/keepalive-timeout: "serviceName=<myservice> timeout=<time>s"
spec:
 tls:
 - hosts:
   - mydomain
   secretName: mytlssecret
 rules:
 - host: mydomain
   http:
     paths:
     - path: /
       backend:
         serviceName: myservice
         servicePort: 8080
```
{: codeblock}


|Annotation field|Value|
|----------------|-----|
| `serviceName` | Replace `<myservice>` with the name of the Kubernetes service that you created for your app. This parameter is optional. If the parameter is provided, the keepalive timeout is set for the given service. If the parameter is not provided, the keepalive timeout is set at the server level of the `nginx.conf` for all the services that do not have the keepalive timeout configured. |
| `timeout` | Replace `<time>` with an amount of time in seconds. Example: `timeout=20s`. A `0` value disables the keepalive client connections. |
{: caption="Understanding the annotation components" caption-side="top"}

<br />

### Proxy next upstream (`proxy-next-upstream-config`)
{: #proxy-next-upstream-config}

Set when the ALB can pass a request to the next upstream server.
{: shortdesc}

**Description**

The Ingress ALB acts as a proxy between the client app and your app. Some app setups require multiple upstream servers that handle incoming client requests from the ALB. Sometimes the proxy server that the ALB uses cannot establish a connection with an upstream server that the app uses. The ALB can then try to establish a connection with the next upstream server to pass the request to it instead. You can use the `proxy-next-upstream-config` annotation to set in which cases, for how long, and how many times the ALB can try to pass a request to the next upstream server.

Timeout is always configured when you use `proxy-next-upstream-config`, so don't add `timeout=true` to this annotation.
{: note}

**Sample Ingress resource YAML**


```yaml
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: myingress
  annotations:
    ingress.bluemix.net/proxy-next-upstream-config: "serviceName=<myservice1> retries=<tries> timeout=<time> error=true http_502=true; serviceName=<myservice2> http_403=true non_idempotent=true"
spec:
  tls:
  - hosts:
    - mydomain
    secretName: mysecret
  rules:
  - host: mydomain
    http:
      paths:
      - path: /
        backend:
          serviceName: myservice1
          servicePort: 80
```
{: codeblock}


|Annotation field|Value|
|----------------|-----|
| `serviceName` | Replace `<myservice>` with the name of the Kubernetes service that you created for your app. |
| `retries` | Replace `<tries>` with the maximum number of times that the ALB tries to pass a request to the next upstream server. This number includes the original request. To turn off this limitation, use `0`. If you do not specify a value, the default value `0` is used. |
| `timeout` | Replace `<time>` with the maximum amount of time, in seconds, that the ALB tries to pass a request to the next upstream server. For example, to set a time of 30 seconds, enter `30s`. To turn off this limitation, use `0`. If you do not specify a value, the default value `0` is used. |
| `error` | If set to `true`, the ALB passes a request to the next upstream server when an error occurred while establishing a connection with the first upstream server, passing a request to it, or reading the response header. |
| `invalid_header` | If set to `true`, the ALB passes a request to the next upstream server when the first upstream server returns an empty or invalid response. |
| `http_502` | If set to `true`, the ALB passes a request to the next upstream server when the first upstream server returns a response with the code 502. You can designate the following HTTP response codes: `500`, `502`, `503`, `504`, `403`, `404`, `429`. |
| `non_idempotent` | If set to `true`, the ALB can pass requests with a non-idempotent method to the next upstream server. By default, the ALB does not pass these requests to the next upstream server. |
| `off` | To prevent the ALB from passing requests to the next upstream server, set to `true`. |
{: caption="Understanding the annotation components" caption-side="top"}

<br />

### Session-affinity with cookies (`sticky-cookie-services`)
{: #sticky-cookie-services}

Use the sticky cookie annotation to add session affinity to your ALB and always route incoming network traffic to the same upstream server.
{: shortdesc}

**Description**

For high availability, some app setups require you to deploy multiple upstream servers that handle incoming client requests. When a client connects to your back-end app, you can use session-affinity so that a client is served by the same upstream server during a session or for the time it takes to complete a task. You can configure your ALB to ensure session-affinity by always routing incoming network traffic to the same upstream server.

Every client that connects to your back-end app is assigned to one of the available upstream servers by the ALB. The ALB creates a session cookie that is stored in the client's app, which is included in the header information of every request between the ALB and the client. The information in the cookie ensures that all requests are handled by the same upstream server throughout the session.

Relying on sticky sessions can add complexity and reduce your availability. For example, you might have an HTTP server that maintains some session state for an initial connection so that the HTTP service accepts only subsequent requests with the same session state value. However, this prevents easy horizontal scaling of the HTTP service. Consider using an external database, such as Redis or Memcached, to store the HTTP request session value so that you can maintain the session state across multiple servers.
{: note}

When you include multiple services, use a semi-colon (;) to separate them.

**Sample Ingress resource YAML**

```yaml
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: myingress
  annotations:
    ingress.bluemix.net/sticky-cookie-services: "serviceName=<myservice1> name=<cookie_name1> expires=<expiration_time1> path=<cookie_path1> hash=sha1 [secure] [httponly]"
spec:
  tls:
  - hosts:
    - mydomain
    secretName: mytlssecret
  rules:
  - host: mydomain
    http:
      paths:
      - path: /service1_path
        backend:
          serviceName: <myservice1>
          servicePort: 8080
      - path: /service2_path
        backend:
          serviceName: <myservice2>
          servicePort: 80
```
{: codeblock}


|Annotation field|Value|
|----------------|-----|
| `serviceName` | Replace `<myservice>` with the name of the Kubernetes service that you created for your app. |
| `name` | Replace `<cookie_name>` with the name of a sticky cookie that is created during a session. |
| `expires` | Replace `<expiration_time>` with the time in seconds (s), minutes (m), or hours (h) before the sticky cookie expires. This time is independent of the user activity. After the cookie is expired, the cookie is deleted by the client web browser and no longer sent to the ALB. For example, to set an expiration time of 1 second, 1 minute, or 1 hour, enter `1s`, `1m`, or `1h`. |
| `path` | Replace `<cookie_path>` with the path that is appended to the Ingress subdomain and that indicates for which domains and subdomains the cookie is sent to the ALB. For example, if your Ingress domain is `www.myingress.com` and you want to send the cookie in every client request, you must set `path=/`. If you want to send the cookie only for `www.myingress.com/myapp` and all its subdomains, then you must set `path=/myapp`. |
| `hash` | The hash algorithm that protects the information in the cookie. Only `sha1` is supported. SHA1 creates a hash sum based on the information in the cookie and appends this hash sum to the cookie. The server can decrypt the information in the cookie and verify data integrity. |
| `secure` | Include this parameter to enable secure cookies that are transferred only via HTTPS. This parameter is not required for HTTPS connections, but causes failures for HTTP connections. |
| `httponly` | Include this parameter to help prevent Cross Site Scripting attacks that use JavaScript to steal session cookies. If any apps that you expose with Ingress require JavaScript to interact with the session cookie, do not include this parameter. |
{: caption="Understanding the annotation components" caption-side="top"}

<br />

### Upstream fail timeout (`upstream-fail-timeout`)
{: #upstream-fail-timeout}

Set the amount of time during which the ALB can attempt to connect to the server.
{: shortdesc}

**Description**

Set the amount of time during which the ALB can attempt to connect to a server before the server is considered unavailable. For a server to be considered unavailable, the ALB must hit the maximum number of failed connection attempts set by the [`upstream-max-fails`](#upstream-max-fails) annotation within the set amount of time. This amount of time also determines how long the server is considered unavailable.

**Sample Ingress resource YAML**

```yaml
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: myingress
  annotations:
    ingress.bluemix.net/upstream-fail-timeout: "serviceName=<myservice> fail-timeout=<fail_timeout>"
spec:
  tls:
  - hosts:
    - mydomain
    secretName: mytlssecret
  rules:
  - host: mydomain
    http:
      paths:
      - path: /
        backend:
          serviceName: myservice
          servicePort: 8080
```
{: codeblock}

|Annotation field|Value|
|----------------|-----|
| `serviceName` (optional) | Replace `<myservice>` with the name of the Kubernetes service that you created for your app. |
| `fail-timeout` | Replace `<fail_timeout>` with the amount of time that the ALB can attempt to connect to a server before the server is considered unavailable. The default is `10s`. Time must be in seconds. |
{: caption="Understanding the annotation components" caption-side="top"}

<br />

### Upstream keepalive (`upstream-keepalive`)
{: #upstream-keepalive}

Set the maximum number of idle keepalive connections for an upstream server.
{: shortdesc}

**Description**

Set the maximum number of idle keepalive connections to the upstream server of a given service. The upstream server has 64 idle keepalive connections by default.

**Sample Ingress resource YAML**

```yaml
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: myingress
  annotations:
    ingress.bluemix.net/upstream-keepalive: "serviceName=<myservice> keepalive=<max_connections>"
spec:
  tls:
  - hosts:
    - mydomain
    secretName: mytlssecret
  rules:
  - host: mydomain
    http:
      paths:
      - path: /
        backend:
          serviceName: myservice
          servicePort: 8080
```
{: codeblock}


|Annotation field|Value|
|----------------|-----|
| `serviceName` | Replace `<myservice>` with the name of the Kubernetes service that you created for your app. |
| `keepalive` | Replace `<max_connections>` with the maximum number of idle keepalive connections to the upstream server. The default is `64`. A `0` value disables upstream keepalive connections for the given service. |
{: caption="Understanding the annotation components" caption-side="top"}

<br />

### Upstream keepalive timeout (`upstream-keepalive-timeout`)
{: #upstream-keepalive-timeout}

**Description**

Sets the maximum time that a keepalive connection stays open between the ALB proxy server and the upstream server for your back-end app. If you do not use this annotation, the default timeout value is `60s`.

**Sample Ingress resource YAML**

```yaml
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
 name: myingress
 annotations:
   ingress.bluemix.net/upstream-keepalive-timeout: "serviceName=<myservice> timeout=<time>s"
spec:
 tls:
 - hosts:
   - mydomain
   secretName: mytlssecret
 rules:
 - host: mydomain
   http:
     paths:
     - path: /
       backend:
         serviceName: myservice
         servicePort: 8080
```
{: codeblock}


|Annotation field|Value|
|----------------|-----|
| `serviceName` | Replace `<myservice>` with the name of the Kubernetes service that you created for your app. This parameter is optional. |
| `timeout` | Replace `<time>` with an amount of time in seconds. Example: `timeout=20s`. A `0` value disables the keepalive client connections. |
{: caption="Understanding the annotation components" caption-side="top"}

<br />

### Upstream max fails (`upstream-max-fails`)
{: #upstream-max-fails}

Set the maximum number of unsuccessful attempts to communicate with the server.
{: shortdesc}

**Description**

Set the maximum number of times the ALB can fail to connect to the server before the server is considered unavailable. For the server to be considered unavailable, the ALB must hit the maximum number within the duration of time set by the [`upstream-fail-timeout`](#upstream-fail-timeout) annotation. The duration of time that the server is considered unavailable is also set by the `upstream-fail-timeout` annotation.

**Sample Ingress resource YAML**

```yaml
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: myingress
  annotations:
    ingress.bluemix.net/upstream-max-fails: "serviceName=<myservice> max-fails=<max_fails>"
spec:
  tls:
  - hosts:
    - mydomain
    secretName: mytlssecret
  rules:
  - host: mydomain
    http:
      paths:
      - path: /
        backend:
          serviceName: myservice
          servicePort: 8080
```
{: codeblock}

|Annotation field|Value|
|----------------|-----|
| `serviceName(Optional)` | Replace `<myservice>` with the name of the Kubernetes service that you created for your app. |
| `max-fails` | Replace `<max_fails>` with the maximum number of unsuccessful attempts the ALB can make to communicate with the server. The default is `1`. A `0` value disables the annotation. |
{: caption="Understanding the annotation components" caption-side="top"}

<br />

## HTTPS and TLS/SSL authentication annotations
{: #https-auth}

With HTTPS and TLS/SSL authentication annotations, you can configure your ALB for HTTPS traffic, change default HTTPS ports, enable SSL encryption for traffic that is sent to your back-end apps, or set up mutual authentication.
{: shortdesc}

### Custom HTTP and HTTPS ports (`custom-port`)
{: #custom-port}

Change the default ports for HTTP (port 80) and HTTPS (port 443) network traffic.
{: shortdesc}

**Description**

By default, the Ingress ALB is configured to listen for incoming HTTP network traffic on port 80 and for incoming HTTPS network traffic on port 443. You can change the default ports to add security to your ALB domain, or to enable only an HTTPS port.

To enable mutual authentication on a port, [configure the ALB to open the valid port](/docs/openshift?topic=openshift-ingress#opening_ingress_ports) and then specify that port in the [`mutual-auth` annotation](#mutual-auth). Do not use the `custom-port` annotation to specify a port for mutual authentication.
{: note}

**Sample Ingress resource YAML**

```yaml
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
 name: myingress
 annotations:
   ingress.bluemix.net/custom-port: "protocol=<protocol1> port=<port1>;protocol=<protocol2> port=<port2>"
spec:
 tls:
 - hosts:
   - mydomain
   secretName: mytlssecret
 rules:
 - host: mydomain
   http:
     paths:
     - path: /
       backend:
         serviceName: myservice
         servicePort: 8080
```
{: codeblock}

|Annotation field|Value|
|----------------|-----|
| `<protocol>` | Enter `http` or `https` to change the default port for incoming HTTP or HTTPS network traffic. |
| `<port>` | Enter the port number to use for incoming HTTP or HTTPS network traffic. <p class="note">When a custom port is specified for either HTTP or HTTPS, the default ports are no longer valid for both HTTP and HTTPS. For example, to change the default port for HTTPS to 8443, but use the default port for HTTP, you must set custom ports for both: `custom-port: "protocol=http port=80; protocol=https port=8443"`.</p> |
{: caption="Understanding the annotation components" caption-side="top"}


**Usage**

1. Review open ports for your ALB.
  ```
  oc get service -n kube-system
  ```
  {: pre}

  Your CLI output looks similar to the following:
  ```
  NAME                                             TYPE           CLUSTER-IP     EXTERNAL-IP    PORT(S)                      AGE
  public-cr18e61e63c6e94b658596ca93d087eed9-alb1   LoadBalancer   10.xxx.xx.xxx    169.xx.xxx.xxx 80:30416/TCP,443:32668/TCP   109d
  ```
  {: screen}

2. Open the ALB config map.
  ```
  oc edit configmap ibm-cloud-provider-ingress-cm -n kube-system
  ```
  {: pre}

3. Add the non-default HTTP and HTTPS ports to the config map. Replace `<port>` with the HTTP or HTTPS port that you want to open.
  <p class="note">By default, ports 80 and 443 are open. If you want to keep 80 and 443 open, you must also include them in addition to any other TCP ports you specify in the `public-ports` field. If you enabled a private ALB, you must also specify any ports you want to keep open in the `private-ports` field. For more information, see [Opening ports in the Ingress ALB](/docs/openshift?topic=openshift-ingress#opening_ingress_ports).</p>
  ```yaml
  apiVersion: v1
  kind: ConfigMap
  data:
    public-ports: <port1>;<port2>
  metadata:
    creationTimestamp: 2017-08-22T19:06:51Z
    name: ibm-cloud-provider-ingress-cm
    namespace: kube-system
    resourceVersion: "1320"
    selfLink: /api/v1/namespaces/kube-system/configmaps/ibm-cloud-provider-ingress-cm
    uid: <uid>
  ```
  {: codeblock}

4. Verify that your ALB is reconfigured with the non-default ports.
  ```
  oc get service -n kube-system
  ```
  {: pre}

  Your CLI output looks similar to the following:
  ```
  NAME                                             TYPE           CLUSTER-IP       EXTERNAL-IP    PORT(S)                           AGE
  public-cr18e61e63c6e94b658596ca93d087eed9-alb1   LoadBalancer   10.xxx.xx.xxx    169.xx.xxx.xxx <port1>:30776/TCP,<port2>:30412/TCP   109d
  ```
  {: screen}

5. Configure your Ingress to use the non-default ports when routing incoming network traffic to your services. Use the annotation in the sample YAML file in this reference.

6. Update your ALB configuration.
  ```
  oc apply -f myingress.yaml
  ```
  {: pre}

7. Open your preferred web browser to access your app. Example: `https://<ibmdomain>:<port>/<service_path>/`

<br />

### HTTP redirects to HTTPS (`redirect-to-https`)
{: #redirect-to-https}

Convert insecure HTTP client requests to HTTPS.
{: shortdesc}

**Description**

You set up your Ingress ALB to secure your domain with the IBM-provided TLS certificate or your custom TLS certificate. Some users might try to access your apps by using an insecure `http` request to your ALB domain, for example `http://www.myingress.com`, instead of using `https`. You can use the redirect annotation to always convert insecure HTTP requests to HTTPS. If you do not use this annotation, insecure HTTP requests are not converted into HTTPS requests by default and might expose unencrypted confidential information to the public.


Redirecting HTTP requests to HTTPS is disabled by default.

**Sample Ingress resource YAML**

```yaml
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
 name: myingress
 annotations:
   ingress.bluemix.net/redirect-to-https: "True"
spec:
 tls:
 - hosts:
   - mydomain
   secretName: mytlssecret
 rules:
 - host: mydomain
   http:
     paths:
     - path: /
       backend:
         serviceName: myservice
         servicePort: 8080
```
{: codeblock}

<br />

### HTTP Strict Transport Security (`hsts`)
{: #hsts}

**Description**

HSTS instructs the browser to access a domain only by using HTTPS. Even if the user enters or follows a plain HTTP link, the browser strictly upgrades the connection to HTTPS.

**Sample Ingress resource YAML**

```yaml
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: myingress
  annotations:
    ingress.bluemix.net/hsts: enabled=true maxAge=<31536000> includeSubdomains=true
spec:
  tls:
  - hosts:
    - mydomain
    secretName: mysecret
  rules:
  - host: mydomain
    http:
      paths:
      - path: /service1_path
        backend:
          serviceName: myservice1
          servicePort: 8443
      - path: /service2_path
        backend:
          serviceName: myservice2
          servicePort: 8444
          ```
{: codeblock}

|Annotation field|Value|
|----------------|-----|
| `enabled` | Use `true` to enable HSTS. |
| `maxAge` | Replace `<31536000>` with an integer that represents how many seconds a browser will cache sending requests straight to HTTPS. The default is `31536000`, which is equal to 1 year. |
| `includeSubdomains` | Use `true` to tell the browser that the HSTS policy also applies to all subdomains of the current domain. The default is `true`.  |
{: caption="Understanding the annotation components" caption-side="top"}

<br />

### Mutual authentication (`mutual-auth`)
{: #mutual-auth}

Configure mutual authentication for the ALB.
{: shortdesc}

**Description**

Configure mutual authentication of downstream traffic for the Ingress ALB. The external client authenticates the server and the server also authenticates the client by using certificates. Mutual authentication is also known as certificate-based authentication or two-way authentication.

Use the `mutual-auth` annotation for SSL termination between the client and the Ingress ALB. Use the [`ssl-services` annotation](#ssl-services) for SSL termination between the Ingress ALB and the back-end app.

The mutual authentication annotation validates client certificates. To forward client certificates in a header for the applications to handle authorization, you can use the following [`proxy-add-headers` annotation](#proxy-add-headers): `"ingress.bluemix.net/proxy-add-headers": "serviceName=router-set {\n X-Forwarded-Client-Cert $ssl_client_escaped_cert;\n}\n"`
{: tip}

**Pre-requisites**


* You must have a valid mutual authentication secret that contains the required `ca.crt`. To create a mutual authentication secret, see the steps at the end of this section.
* To enable mutual authentication on a port other than 443, [configure the ALB to open the valid port](/docs/openshift?topic=openshift-ingress#opening_ingress_ports) and then specify that port in this annotation. Do not use the `custom-port` annotation to specify a port for mutual authentication.

**Sample Ingress resource YAML**

```yaml
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: myingress
  annotations:
    ingress.bluemix.net/mutual-auth: "secretName=<mysecret> port=<port>"
spec:
  tls:
  - hosts:
    - mydomain
    secretName: mytlssecret
  rules:
  - host: mydomain
    http:
      paths:
      - path: /
        backend:
          serviceName: myservice
          servicePort: 8080
```
{: codeblock}

|Annotation field|Value|
|----------------|-----|
| `secretName` | Replace `<mysecret>` with a name for the secret resource. |
| `port` | Replace `<port>` with the ALB port number. |
{: caption="Understanding the annotation components" caption-side="top"}

**To create a mutual authentication secret:**

1. Generate a certificate authority (CA) cert and key from your certificate provider. If you have your own domain, purchase an official TLS certificate for your domain. Make sure the [CN](https://support.dnsimple.com/articles/what-is-common-name/){: external} is different for each certificate.
    For testing purposes, you can create a self-signed certificate by using OpenSSL. For more information, see this [self-signed SSL certificate tutorial](https://www.akadia.com/services/ssh_test_certificate.html){: external} or this [mutual authentication tutorial, which includes creating your own CA](https://rollout.io/blog/how-to-set-up-mutual-tls-authentication/){: external}.
    {: tip}
2. [Convert the cert into base64](https://www.base64encode.org/){: external}.
3. Create a secret YAML file by using cert.
   ```yaml
   apiVersion: v1
   kind: Secret
   metadata:
     name: ssl-my-test
   type: Opaque
   data:
     ca.crt: <ca_certificate>
   ```
   {: codeblock}
4. Create a Kubernetes secret for your certificate.
   ```
   oc apply -f ssl-my-test
   ```
   {: pre}

<br />

### SSL services support (`ssl-services`)
{: #ssl-services}

Allow HTTPS requests and encrypt traffic to your upstream apps.
{: shortdesc}

**Description**

When your Ingress resource configuration has a TLS section, the Ingress ALB can handle HTTPS-secured URL requests to your app. By default, the ALB terminates the TLS termination and decrypts the request before using the HTTP protocol to forward the traffic to your apps. If you have apps that require the HTTPS protocol and need traffic to be encrypted, use the `ssl-services` annotation. With the `ssl-services` annotation, the ALB terminates the external TLS connection, then creates a new SSL connection between the ALB and the app pod. Traffic is re-encrypted before it is sent to the upstream pods.

If your back-end app can handle TLS and you want to add additional security, you can add one-way or mutual authentication by providing a certificate that is contained in a secret.

Use the `ssl-services` annotation for SSL termination between the Ingress ALB and the back-end app. Use the [`mutual-auth` annotation](#mutual-auth) for SSL termination between the client and the Ingress ALB.
{: tip}

**Sample Ingress resource YAML**

```yaml
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: <myingressname>
  annotations:
    ingress.bluemix.net/ssl-services: ssl-service=<myservice1> ssl-secret=<service1-ssl-secret> proxy-ssl-verify-depth=<verification_depth> proxy-ssl-name=<service_CN>;ssl-service=<myservice2> ssl-secret=<service2-ssl-secret> proxy-ssl-verify-depth=<verification_depth> proxy-ssl-name=<service_CN>
spec:
  tls:
  - hosts:
    - mydomain
    secretName: mysecret
  rules:
  - host: mydomain
    http:
      paths:
      - path: /service1_path
        backend:
          serviceName: myservice1
          servicePort: 8443
      - path: /service2_path
        backend:
          serviceName: myservice2
          servicePort: 8444
          ```
{: codeblock}

|Annotation field|Value|
|----------------|-----|
| `ssl-service` | Replace `<myservice>` with the name of the service that requires HTTPS. Traffic is encrypted from the ALB to this app's service. |
| `ssl-secret` | If your back-end app can handle TLS and you want to add additional security, replace `<service-ssl-secret>` with the one-way or mutual authentication secret for the service.<ul><li>If you provide a one-way authentication secret, the value must contain the `trusted.crt` from the upstream server. To create a one-way secret, see the steps at the end of this section.</li><li>If you provide a mutual authentication secret, the value must contain the required `client.crt` and `client.key` that your app is expecting from the client. To create a mutual authentication secret, see the steps at the end of this section.</li></ul><p class="important">If you do not provide a secret, Ingress does not verify the connection and relies on the back-end app to correctly use TLS. The connection is still encrypted, but insecure connections might be permitted. You might choose to omit a secret if you want to test the connection and do not have certificates ready, or if your certificates are expired and you want to allow insecure connections.</p> |
| `proxy-ssl-verify-depth` | Optional: If you specify a secret in the `ssl-secret` parameter, replace `<verification_depth>` with the maximum number of certificates that are expected in the proxied HTTPS server certificates chain. This value indicates the maximum number of HTTPS server certificates in the chain that the ALB verifies. The size of your server certificates chain can vary based on which kinds of authentication you set up. By default, the depth is set to `5`, which is sufficient for most cases. If you have a larger certificate chain, you can change the value of this parameter. The value must be an integer from `1` to `10`. |
| `proxy-ssl-name` | Optional: Specify a server name for the back-end server that is protected by the SSL certificate. The ALB uses this server name as the Common Name (CN), instead of the CN in the certificate of the back-end server, to check the certificate of the back-end HTTPS server. This server name is also passed to the back-end server in the Server Name Indication (SNI) extension during the TLS handshake.</br></br>Specifying an override CN for each service is helpful when you create two or more Ingress resource files, and the resources share the same wildcard trusted certificate for the secret. In this case, the resource share the same CN for the certificate. Because the ALB generates the back-end server name based on the CN in the certificate, the ALB configuration is invalid because the two services in the separate resources have the same back-end server name. You must use `proxy-ssl-name` to provide an override CN that is unique to each services' back-end server.</br></br>For example, you might want the hostname to be `foo.mydomain.com` for Ingress resource A, and `mydomain.com` for Ingress resource B. You create one trusted certificate for both resources by using a wildcard CN. In the `ssl-services` annotation for resource A, you specify the CN as `proxy-ssl-name=foo.mydomain.com`. In the `ssl-services` annotation for resource B, you specify the CN as `proxy-ssl-name=mydomain.com`. The ALB can now generate two distinct back-end server names for the services in each resource.</br></br>The CN must exactly match the name of the back-end HTTPS server where the certificate is installed. If the certificate is issued for a subdomain, specify the full subdomain, such as `test.example.com`. If you use a wildcard certificate, you can specify the full hostname, such as `test.example.com` or `foo.example.com`, so that each hostname can use the same certificate. |
{: caption="Understanding the annotation components" caption-side="top"}

**To create a one-way authentication secret:**

1. Get the certificate authority (CA) key and certificate from your upstream server and an SSL client certificate. The IBM ALB is based on NGINX, which requires the root certificate, intermediate certificate, and back-end certificate. For more information, see the [NGINX docs](https://docs.nginx.com/nginx/admin-guide/security-controls/securing-http-traffic-upstream/){: external}.
2. [Convert the cert into base64](https://www.base64encode.org/){: external}.
3. Create a secret YAML file by using the cert.
   ```yaml
   apiVersion: v1
   kind: Secret
   metadata:
     name: ssl-my-test
   type: Opaque
   data:
     trusted.crt: <ca_certificate>
   ```
   {: codeblock}

   To also enforce mutual authentication for upstream traffic, you can provide a `client.crt` and `client.key` in addition to the `trusted.crt` in the data section.
   {: tip}

4. Create a Kubernetes secret for your certificate.
   ```
   oc apply -f ssl-my-test
   ```
   {: pre}

</br>
**To create a mutual authentication secret:**

1. Generate a certificate authority (CA) cert and key from your certificate provider. If you have your own domain, purchase an official TLS certificate for your domain. Make sure the [CN](https://support.dnsimple.com/articles/what-is-common-name/){: external} is different for each certificate.
    For testing purposes, you can create a self-signed certificate by using OpenSSL. For more information, see this [self-signed SSL certificate tutorial](https://www.akadia.com/services/ssh_test_certificate.html){: external} or this [mutual authentication tutorial, which includes creating your own CA](https://rollout.io/blog/how-to-set-up-mutual-tls-authentication/){: external}.
    {: tip}
2. [Convert the cert into base64](https://www.base64encode.org/){: external}.
3. Create a secret YAML file by using the cert.
   ```yaml
   apiVersion: v1
   kind: Secret
   metadata:
     name: ssl-my-test
   type: Opaque
   data:
     client.crt: <ca_certificate>
     client.key: <ca_key>
   ```
   {: codeblock}
4. Create a Kubernetes secret for your certificate.
   ```
   oc apply -f ssl-my-test
   ```
   {: pre}

<br />

### TCP ports (`tcp-ports`)
{: #tcp-ports}

Access an app via a non-standard TCP port.
{: shortdesc}

**Description**

Use this annotation for an app that runs a TCP streams workload.

The ALB operates in pass-through mode and forwards traffic to back-end apps. SSL termination is not supported in this case. The TLS connection is not terminated and passes through untouched.
{: note}

**Sample Ingress resource YAML**

```yaml
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: myingress
  annotations:
    ingress.bluemix.net/tcp-ports: "serviceName=<myservice> ingressPort=<ingress_port> servicePort=<service_port>"
spec:
  tls:
  - hosts:
    - mydomain
    secretName: mysecret
  rules:
  - host: mydomain
    http:
      paths:
      - path: /
        backend:
          serviceName: myservice
          servicePort: 80
```
{: codeblock}

|Annotation field|Value|
|----------------|-----|
| `serviceName` | Replace `<myservice>` with the name of the Kubernetes service to access over non-standard TCP port. |
| `ingressPort` | Replace `<ingress_port>` with the TCP port on which you want to access your app. |
| `servicePort` | This parameter is optional. When provided, the port is substituted to this value before traffic is sent to the back-end app. Otherwise, the port remains the same as the Ingress port. If you don't want to set this parameter, you can remove it from your configuration.  |
{: caption="Understanding the annotation components" caption-side="top"}

**Usage**

1. Review open ports for your ALB.
  ```
  oc get service -n kube-system
  ```
  {: pre}

  Your CLI output looks similar to the following:
  ```
  NAME                                             TYPE           CLUSTER-IP       EXTERNAL-IP      PORT(S)                      AGE
  public-cr18e61e63c6e94b658596ca93d087eed9-alb1   LoadBalancer   10.xxx.xx.xxx    169.xx.xxx.xxx   80:30416/TCP,443:32668/TCP   109d
  ```
  {: screen}

2. Open the ALB config map.
  ```
  oc edit configmap ibm-cloud-provider-ingress-cm -n kube-system
  ```
  {: pre}

3. Add the TCP ports to the config map. Replace `<port>` with the TCP ports that you want to open.
  By default, ports 80 and 443 are open. If you want to keep 80 and 443 open, you must also include them in addition to any other TCP ports you specify in the `public-ports` field. If you enabled a private ALB, you must also specify any ports that you want to keep open in the `private-ports` field. For more information, see [Opening ports in the Ingress ALB](/docs/openshift?topic=openshift-ingress#opening_ingress_ports).
  {: note}
  ```yaml
  apiVersion: v1
  kind: ConfigMap
  data:
    public-ports: 80;443;<port1>;<port2>
  metadata:
    creationTimestamp: 2017-08-22T19:06:51Z
    name: ibm-cloud-provider-ingress-cm
    namespace: kube-system
    resourceVersion: "1320"
    selfLink: /api/v1/namespaces/kube-system/configmaps/ibm-cloud-provider-ingress-cm
    uid: <uid>
   ```
  {: codeblock}

4. Verify that your ALB is re-configured with the TCP ports.
  ```
  oc get service -n kube-system
  ```
  {: pre}
  Your CLI output looks similar to the following:
  ```
  NAME                                             TYPE           CLUSTER-IP       EXTERNAL-IP      PORT(S)                               AGE
  public-cr18e61e63c6e94b658596ca93d087eed9-alb1   LoadBalancer   10.xxx.xx.xxx    169.xx.xxx.xxx   <port1>:30776/TCP,<port2>:30412/TCP   109d
  ```
  {: screen}

5. Configure the ALB to access your app via a non-standard TCP port. Use the `tcp-ports` annotation in the sample YAML file in this reference.

6. Either create your ALB resource or update your existing ALB configuration.
  ```
  oc apply -f myingress.yaml
  ```
  {: pre}

7. Curl the Ingress subdomain to access your app. Example: `curl <domain>:<ingressPort>`

<br />

## Path routing annotations
{: #path-routing}

The Ingress ALB routes traffic to the paths that back-end apps listen on. With path routing annotations, you can configure how the ALB routes traffic to your apps.
{: shortdesc}

### External services (`proxy-external-service`)
{: #proxy-external-service}

Add path definitions to external services, such as services hosted in {{site.data.keyword.cloud_notm}}.
{: shortdesc}

**Description**

Add path definitions to external services. Use this annotation only when your app operates on an external service instead of a back-end service, and you want to route requests to that external service through the Ingress subdomain or custom subdomain that you specify. When you use this annotation to create an external service route, only `client-max-body-size`, `proxy-read-timeout`, `proxy-connect-timeout`, and `proxy-buffering` annotations are supported in conjunction. Any other annotations are not supported in conjunction with `proxy-external-service`.

You cannot specify multiple hosts for a single service and path.
{: note}

Looking to forward requests to the IP address of your external service instead of routing requests through the Ingress ALB? You can set up a [Kubernetes endpoint that defines the external IP address and port of the app](/docs/openshift?topic=openshift-ingress#external_ip).
{: tip}

**Sample Ingress resource YAML**

```yaml
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: myingress
  annotations:
    ingress.bluemix.net/proxy-external-service: "path=<mypath> external-svc=https:<external_service> host=<ingress_subdomain>"
spec:
  rules:
  - host: <ingress_subdomain>
```
{: codeblock}

|Annotation field|Value|
|----------------|-----|
| `path` | Replace `<mypath>` with the path that the external service listens on. |
| `external-svc` | Replace `<external_service>` with the external service to be called. For example, `https://<myservice>.<region>.appdomain.com`. |
| `host` | Replace `<ingress_subdomain>` with the Ingress subdomain for your cluster or the custom domain that you set up. |
{: caption="Understanding the annotation components" caption-side="top"}

<br />

### Location modifier (`location-modifier`)
{: #location-modifier}

Modify the way the ALB matches the request URI against the app path.
{: shortdesc}

**Description**

By default, ALBs process the paths that apps listen on as prefixes. When an ALB receives a request to an app, the ALB checks the Ingress resource for a path (as a prefix) that matches the beginning of the request URI. If a match is found, the request is forwarded to the IP address of the pod where the app is deployed.

The `location-modifier` annotation changes the way the ALB searches for matches by modifying the location block configuration. The location block determines how requests are handled for the app path.

To handle regular expression (regex) paths, this annotation is required.
{: note}

|Modifier|Description|
|--------|-----------|
| `=` | The equal sign modifier causes the ALB to select exact matches only. When an exact match is found, the search stops and the matching path is selected.<br>For example, if your app listens on `/tea`, the ALB selects only exact `/tea` paths when matching a request to your app. |
| `~` | The tilde modifier causes the ALB to process paths as case-sensitive regex paths during matching.<br>For example, if your app listens on `/coffee`, the ALB can select `/ab/coffee` or `/123/coffee` paths when matching a request to your app even though the paths are not explicitly set for your app. |
| `~*` | The tilde modifier that is followed by an asterisk modifier causes the ALB to process paths as case-insensitive regex paths during matching.<br>For example, if your app listens on `/coffee`, the ALB can select `/ab/Coffee` or `/123/COFFEE` paths when matching a request to your app even though the paths are not explicitly set for your app. |
| `^~` | The carat followed by a tilde modifier causes the ALB to select the best non-regex match instead of a regex path. |
{: caption="Supported modifiers" caption-side="top"}

**Sample Ingress resource YAML**

```yaml
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: myingress
  annotations:
    ingress.bluemix.net/location-modifier: "modifier='<location_modifier>' serviceName=<myservice1>;modifier='<location_modifier>' serviceName=<myservice2>"
spec:
  tls:
  - hosts:
    - mydomain
    secretName: mysecret
  rules:
  - host: mydomain
    http:
      paths:
      - path: /
        backend:
          serviceName: myservice
          servicePort: 80
```
{: codeblock}

|Annotation field|Value|
|----------------|-----|
| `modifier` | Replace `<location_modifier>` with the location modifier you want to use for the path. Supported modifiers are `'='`, `'~'`, `'~\*'`, and `'^~'`. You must surround the modifiers in single quotes. |
| `serviceName` | Replace `<myservice>` with the name of the Kubernetes service you created for your app. |
{: caption="Understanding the annotation components" caption-side="top"}

<br />

### Rewrite paths (`rewrite-path`)
{: #rewrite-path}

Route incoming network traffic on an ALB domain path to a different path that your back-end app listens on.
{: shortdesc}

**Description**

Your Ingress ALB domain routes incoming network traffic on `mykubecluster.us-south.containers.appdomain.cloud/beans` to your app. Your app listens on `/coffee`, instead of `/beans`. To forward incoming network traffic to your app, add the rewrite annotation to your Ingress resource configuration file. The rewrite annotation ensures that incoming network traffic on `/beans` is forwarded to your app by using the `/coffee` path. When including multiple services, use only a semi-colon (;) with no space before or after the semi-colon to separate them.

**Sample Ingress resource YAML**

```yaml
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: myingress
  annotations:
    ingress.bluemix.net/rewrite-path: "serviceName=<myservice1> rewrite=<target_path1>;serviceName=<myservice2> rewrite=<target_path2>"
spec:
  tls:
  - hosts:
    - mydomain
    secretName: mysecret
  rules:
  - host: mydomain
    http:
      paths:
      - path: /beans
        backend:
          serviceName: myservice1
          servicePort: 80
```
{: codeblock}

|Annotation field|Value|
|----------------|-----|
| `serviceName` | Replace `<myservice>` with the name of the Kubernetes service that you created for your app. |
| `rewrite` | Replace `<target_path>` with the path that your app listens on. Incoming network traffic on the ALB domain is forwarded to the Kubernetes service by using this path. Most apps do not listen on a specific path, but use the root path and a specific port. In the example for `mykubecluster.us-south.containers.appdomain.cloud/beans`, the rewrite path is `/coffee`. <p class= "note">If you apply this file and the URL shows a `404` response, your backend app might be listening on a path that ends in `/`. Try adding a trailing `/` to this rewrite field, then reapply the file and try the URL again.</p> |
{: caption="Understanding the annotation components" caption-side="top"}

<br />

## Proxy buffer annotations
{: #proxy-buffer}

The Ingress ALB acts as a proxy between your back-end app and the client web browser. With proxy buffer annotations, you can configure how data is buffered on your ALB when you send or receive data packets.
{: shortdesc}

### Large client header buffers (`large-client-header-buffers`)
{: #large-client-header-buffers}

Set the maximum number and size of buffers that read large client request headers.
{: shortdesc}

**Description**

Buffers that read large client request headers are allocated only by demand: If a connection is transitioned into the keepalive state after the end-of-request processing, these buffers are released. By default, there are `4` buffers and buffer size is equal to `8K` bytes. If a request line exceeds the set maximum size of one buffer, the `414 Request-URI Too Large` HTTP error is returned to the client. Additionally, if a request header field exceeds the set maximum size of one buffer, the `400 Bad Request` error is returned to the client. You can adjust the maximum number and size of buffers that are used for reading large client request headers.

**Sample Ingress resource YAML**

```yaml
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
 name: myingress
 annotations:
   ingress.bluemix.net/large-client-header-buffers: "number=<number> size=<size>"
spec:
 tls:
 - hosts:
   - mydomain
   secretName: mytlssecret
 rules:
 - host: mydomain
   http:
     paths:
     - path: /
       backend:
         serviceName: myservice
         servicePort: 8080
```
{: codeblock}

|Annotation field|Value|
|----------------|-----|
| `<number>` | The maximum number of buffers that should be allocated to read large client request header. For example, to set it to 4, define `4`. |
| `<size>` | The maximum size of buffers that read large client request header. For example, to set it to 16 kilobytes, define `16k`. The size must end with a `k` for kilobyte or `m` for megabyte. |
{: caption="Understanding the annotation components" caption-side="top"}

<br />

### Client response data buffering (`proxy-buffering`)
{: #proxy-buffering}

Use the buffer annotation to disable the storage of response data on the ALB while the data is sent to the client.
{: shortdesc}

**Description**

The Ingress ALB acts as a proxy between your back-end app and the client web browser. When a response is sent from the back-end app to the client, the response data is buffered on the ALB by default. The ALB proxies the client response and starts sending the response to the client at the client's pace. After all data from the back-end app is received by the ALB, the connection to the back-end app is closed. The connection from the ALB to the client remains open until the client receives all data.

If buffering of response data on the ALB is disabled, data is immediately sent from the ALB to the client. The client must be able to handle incoming data at the pace of the ALB. If the client is too slow, the upstream connection remains open until the client can catch up.

Response data buffering on the ALB is enabled by default.

**Sample Ingress resource YAML**

```yaml
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
 name: myingress
 annotations:
   ingress.bluemix.net/proxy-buffering: "enabled=false serviceName=<myservice1>"
spec:
 tls:
 - hosts:
   - mydomain
   secretName: mytlssecret
 rules:
 - host: mydomain
   http:
     paths:
     - path: /
       backend:
         serviceName: myservice
         servicePort: 8080
```
{: codeblock}

|Annotation field|Value|
|----------------|-----|
| `enabled` | To disable response data buffering on the ALB, set to `false`. |
| `serviceName` | Replace <em>`<myservice1>`</em> with the name of the Kubernetes service that you created for your app. Separate multiple services with a semi-colon (;). This field is optional. If you do not specify a service name, then all services use this annotation. |
{: caption="Understanding the annotation components" caption-side="top"}

<br />

### Proxy buffers (`proxy-buffers`)
{: #proxy-buffers}

Configure the number and size of proxy buffers for the ALB.
{: shortdesc}

**Description**

Set the number and size of the buffers that read a response for a single connection from the proxied server. The configuration is applied to all of the services in the Ingress subdomain unless a service is specified. For example, if a configuration such as `serviceName=SERVICE number=2 size=1k` is specified, 1k is applied to the service. If a configuration such as `number=2 size=1k` is specified, 1k is applied to all of the services in the Ingress subdomain.</br>
<p class="tip">If you get the error message `upstream sent too big header while reading response header from upstream`, the upstream server in your back end sent a header size that is larger than the default limit. Increase the size for both `proxy-buffers` and [`proxy-buffer-size`](#proxy-buffer-size).</p>

**Sample Ingress resource YAML**

```yaml
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
 name: proxy-ingress
 annotations:
   ingress.bluemix.net/proxy-buffers: "serviceName=<myservice> number=<number_of_buffers> size=<size>"
spec:
 tls:
 - hosts:
   - mydomain
   secretName: mytlssecret
 rules:
 - host: mydomain
   http:
     paths:
     - path: /
       backend:
         serviceName: myservice
         servicePort: 8080
```
{: codeblock}

|Annotation field|Value|
|----------------|-----|
| `serviceName` | Replace `<myservice>` with the name for a service to apply proxy-buffers. |
| `number` | Replace `<number_of_buffers>` with a number, such as `2`. |
| `size` | Replace `<size>` with the size of each buffer in kilobytes (k or K), such as `1K`. |
{: caption="Understanding the annotation components" caption-side="top"}

<br />

### Proxy buffer size (`proxy-buffer-size`)
{: #proxy-buffer-size}

Configure the size of the proxy buffer that reads the first part of the response.
{: shortdesc}

**Description**

Set the size of the buffer that reads the first part of the response that is received from the proxied server. This part of the response usually contains a small response header. The configuration is applied to all of the services in the Ingress subdomain unless a service is specified. For example, if a configuration such as `serviceName=SERVICE size=1k` is specified, 1k is applied to the service. If a configuration such as `size=1k` is specified, 1k is applied to all of the services in the Ingress subdomain.

If you get the error message `upstream sent too big header while reading response header from upstream`, the upstream server in your back end sent a header size that is larger than the default limit. Increase the size for both `proxy-buffer-size` and [`proxy-buffers`](#proxy-buffers).
{: tip}

**Sample Ingress resource YAML**

```yaml
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
 name: proxy-ingress
 annotations:
   ingress.bluemix.net/proxy-buffer-size: "serviceName=<myservice> size=<size>"
spec:
 tls:
 - hosts:
   - mydomain
   secretName: mytlssecret
 rules:
 - host: mydomain
   http:
     paths:
     - path: /
       backend:
         serviceName: myservice
         servicePort: 8080
```
{: codeblock}

|Annotation field|Value|
|----------------|-----|
| `serviceName` | Replace `<myservice>` with the name of a service to apply proxy-buffers-size. |
| `size` | Replace `<size>` with the size of each buffer in kilobytes (k or K), such as `1K`. To calculate the proper size, you can check out [this blog post](https://www.getpagespeed.com/server-setup/nginx/tuning-proxy_buffer_size-in-nginx){: external}. |
{: caption="Understanding the annotation components" caption-side="top"}

<br />

### Proxy busy buffers size (`proxy-busy-buffers-size`)
{: #proxy-busy-buffers-size}

Configure the size of proxy buffers that can be busy.
{: shortdesc}

**Description**

Limit the size of any buffers that are sending a response to the client while the response is not yet fully read. In the meantime, the rest of the buffers can read the response and, if needed, buffer part of the response to a temporary file. The configuration is applied to all of the services in the Ingress subdomain unless a service is specified. For example, if a configuration such as `serviceName=SERVICE size=1k` is specified, 1k is applied to the service. If a configuration such as `size=1k` is specified, 1k is applied to all of the services in the Ingress subdomain.

**Sample Ingress resource YAML**

```yaml
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
 name: proxy-ingress
 annotations:
   ingress.bluemix.net/proxy-busy-buffers-size: "serviceName=<myservice> size=<size>"
spec:
 tls:
 - hosts:
   - mydomain
   secretName: mytlssecret
 rules:
 - host: mydomain
   http:
     paths:
     - path: /
       backend:
         serviceName: myservice
         servicePort: 8080
         ```
{: codeblock}

|Annotation field|Value|
|----------------|-----|
| `serviceName` | Replace `<myservice>` with the name of a service to apply proxy-busy-buffers-size. |
| `size` | Replace `<size>` with the size of each buffer in kilobytes (k or K), such as `1K`. |
{: caption="Understanding the annotation components" caption-side="top"}

<br />

## Request and response annotations
{: #request-response}

Use request and response annotations to add or remove header information from the client and server requests, and to change the size of the body that the client can send.
{: shortdesc}

### Add server port to host header (`add-host-port`)
{: #add-host-port}

Add a server port to the client request before the request is forwarded to your back-end app.
{: shortdesc}

**Description**

Add the `:server_port` to the host header of a client request before forwarding the request to your back-end app.

**Sample Ingress resource YAML**

```yaml
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
 name: myingress
 annotations:
   ingress.bluemix.net/add-host-port: "enabled=true serviceName=<myservice>"
spec:
 tls:
 - hosts:
   - mydomain
   secretName: mytlssecret
 rules:
 - host: mydomain
   http:
     paths:
     - path: /
       backend:
         serviceName: myservice
         servicePort: 8080
```
{: codeblock}

|Annotation field|Value|
|----------------|-----|
| `enabled` | Set to `true` to add `:server_port` to the host header of requests. |
| `serviceName` | Replace <em>`<myservice>`</em> with the name of the Kubernetes service that you created for your app. Separate multiple services with a semi-colon (;). This field is optional. If you do not specify a service name, then all services use this annotation. |
{: caption="Understanding the annotation components" caption-side="top"}

<br />

### Additional client request or response header (`proxy-add-headers`, `response-add-headers`)
{: #proxy-add-headers}

Add extra header information to a client request before sending the request to the back-end app or to a client response before sending the response to the client.
{: shortdesc}

**Description**

The Ingress ALB acts as a proxy between the client app and your back-end app. Client requests that are sent to the ALB are processed (proxied) and put into a new request that is then sent to your back-end app. Similarly, back-end app responses that are sent to the ALB are processed (proxied) and put into a new response that is then sent to the client. Proxying a request or response removes HTTP header information, such as the username, that was initially sent from the client or back-end app.

If your back-end app requires HTTP header information, you can use the `proxy-add-headers` annotation to add header information to the client request before the request is forwarded by the ALB to the back-end app. If the client web app requires HTTP header information, you can use the `response-add-headers` annotation to add header information to the response before the response is forwarded by the ALB to the client web app.<br>

</br>

The `response-add-headers` annotation does not support global headers for all services. To add a header for all service responses at a server level, you can use the [`server-snippets` annotation](#server-snippets):
{: tip}
```yaml
annotations:
  ingress.bluemix.net/server-snippets: |
    add_header <header1> <value1>;
```
{: codeblock}
</br>

**Sample Ingress resource YAML**

```yaml
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: myingress
  annotations:
    ingress.bluemix.net/proxy-add-headers: |
      serviceName=<myservice1> {
      <header1> <value1>;
      <header2> <value2>;
      }
      serviceName=<myservice2> {
      <header3> <value3>;
      }
    ingress.bluemix.net/response-add-headers: |
      serviceName=<myservice1> {
      <header1>:<value1>;
      <header2>:<value2>;
      }
      serviceName=<myservice2> {
      <header3>:<value3>;
      }
spec:
  tls:
  - hosts:
    - mydomain
    secretName: mytlssecret
  rules:
  - host: mydomain
    http:
      paths:
      - path: /service1_path
        backend:
          serviceName: <myservice1>
          servicePort: 8080
      - path: /service2_path
        backend:
          serviceName: <myservice2>
          servicePort: 80
```
{: codeblock}

|Annotation field|Value|
|----------------|-----|
| `service_name` | Replace `<myservice>` with the name of the Kubernetes service that you created for your app. |
| `<header>` | The key of the header information to add to the client request or client response. |
| `<value>` | The value of the header information to add to the client request or client response. |
{: caption="Understanding the annotation components" caption-side="top"}

<br />

### Client response header removal (`response-remove-headers`)
{: #response-remove-headers}

Remove header information that is included in the client response from the back-end end app before the response is sent to the client.
{: shortdesc}

**Description**

The Ingress ALB acts as a proxy between your back-end app and the client web browser. Client responses from the back-end app that are sent to the ALB are processed (proxied), and put into a new response that is then sent from the ALB to the client web browser. Although proxying a response removes http header information that was initially sent from the back-end app, this process might not remove all back-end app specific headers. Remove header information from a client response before the response is forwarded from the ALB to the client web browser.

**Sample Ingress resource YAML**


```yaml
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: myingress
  annotations:
    ingress.bluemix.net/response-remove-headers: |
      serviceName=<myservice1> {
      "<header1>";
      "<header2>";
      }
      serviceName=<myservice2> {
      "<header3>";
      }
spec:
  tls:
  - hosts:
    - mydomain
    secretName: mytlssecret
  rules:
  - host: mydomain
    http:
      paths:
      - path: /service1_path
        backend:
          serviceName: <myservice1>
          servicePort: 8080
      - path: /service2_path
        backend:
          serviceName: <myservice2>
          servicePort: 80
```
{: codeblock}

|Annotation field|Value|
|----------------|-----|
| `service_name` | Replace `<myservice>` with the name of the Kubernetes service that you created for your app. |
| `<header>` | The key of the header to remove from the client response. |
{: caption="Understanding the annotation components" caption-side="top"}

<br />

### Client request body size (`client-max-body-size`)
{: #client-max-body-size}

Set the maximum size of the body that the client can send as part of a request.
{: shortdesc}

**Description**

To maintain the expected performance, the maximum client request body size is set to 1 megabyte. When a client request with a body size over the limit is sent to the Ingress ALB, and the client does not allow data to be divided, the ALB returns a 413 (Request Entity Too Large) HTTP response to the client. A connection between the client and the ALB is not possible until the size of the request body is reduced. When the client allows data to be split up into multiple chunks, data is divided into packages of 1 megabyte and sent to the ALB.

You might want to increase the maximum body size because you expect client requests with a body size that is greater than 1 megabyte. For example, you want your client to be able to upload large files. Increasing the maximum request body size might impact the performance of your ALB because the connection to the client must stay open until the request is received.

Some client web browsers cannot display the 413 HTTP response message properly.
{: note}

**Sample Ingress resource YAML**

```yaml
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
 name: myingress
 annotations:
   ingress.bluemix.net/client-max-body-size: "serviceName=<myservice> size=<size>; size=<size>"
spec:
 tls:
 - hosts:
   - mydomain
   secretName: mytlssecret
 rules:
 - host: mydomain
   http:
     paths:
     - path: /
       backend:
         serviceName: myservice
         servicePort: 8080
```
{: codeblock}

|Annotation field|Value|
|----------------|-----|
| `serviceName` | Optional: To apply a client max body size to a specific service, replace `<myservice>` with the name of the service. If you do not specify a service name, the size is applied to all services. In the example YAML, the format `"serviceName=<myservice> size=<size>; size=<size>"` applies the first size to the `myservice` service and applies the second size to all other services.|
| `size` | Replace `<size>` with the maximum size of the client response body. For example, to set the maximum size to 200 megabytes, define `200m`. You can set the size to 0 to disable the check of the client request body size. |
{: caption="Understanding the annotation components" caption-side="top"}

<br />

## Service limit annotations
{: #service-limit}

With service limit annotations, you can change the default request processing rate and the number of connections that can come from a single IP address.
{: shortdesc}

### Global rate limits (`global-rate-limit`)
{: #global-rate-limit}

Limit the request processing rate and number of connections per a defined key for all services.
{: shortdesc}

**Description**

For all services, limit the request processing rate and the number of connections per a defined key that are coming from a single IP address for all paths of the selected back ends.

**Sample Ingress resource YAML**

```yaml
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: myingress
  annotations:
    ingress.bluemix.net/global-rate-limit: "key=<key> rate=<rate> conn=<number-of-connections>"
spec:
  tls:
  - hosts:
    - mydomain
    secretName: mytlssecret
  rules:
  - host: mydomain
    http:
      paths:
      - path: /
        backend:
          serviceName: myservice
          servicePort: 8080
```
{: codeblock}

|Annotation field|Value|
|----------------|-----|
| `key` | Supported values are `location`, `$http_` headers, and `$uri`. To set a global limit for incoming requests based on the zone or service, use `key=location`. To set a global limit for incoming requests based on the header, use `X-USER-ID key=$http_x_user_id`. |
| `rate` | Replace `<rate>` with the processing rate. Enter a value as a rate per second (r/s) or rate per minute (r/m). Example: `50r/m`. |
| `conn` | Replace `<number-of-connections>` with the number of connections. |
{: caption="Understanding the annotation components" caption-side="top"}

<br />

### Service rate limits (`service-rate-limit`)
{: #service-rate-limit}

Limit the request processing rate and the number of connections for specific services.
{: shortdesc}

**Description**

For specific services, limit the request processing rate and the number of connections per a defined key that are coming from a single IP address for all paths of the selected back ends.

**Sample Ingress resource YAML**

```yaml
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: myingress
  annotations:
    ingress.bluemix.net/service-rate-limit: "serviceName=<myservice> key=<key> rate=<rate> conn=<number_of_connections>"
spec:
  tls:
  - hosts:
    - mydomain
    secretName: mytlssecret
  rules:
  - host: mydomain
    http:
      paths:
      - path: /
        backend:
          serviceName: myservice
          servicePort: 8080
```
{: codeblock}

|Annotation field|Value|
|----------------|-----|
| `serviceName` | Replace `<myservice>` with the name of the service for which you want to limit the processing rate. |
| `key` | Supported values are `location`, `$http_` headers, and `$uri`. To set a global limit for incoming requests based on the zone or service, use `key=location`. To set a global limit for incoming requests based on the header, use `X-USER-ID key=$http_x_user_id`. |
| `rate` | Replace `<rate>` with the processing rate. To define a rate per second, use r/s: `10r/s`. To define a rate per minute, use r/m: `50r/m`. |
| `conn` | Replace `<number-of-connections>` with the number of connections. |
{: caption="Understanding the annotation components" caption-side="top"}

<br />

## User authentication annotations
{: #user-authentication}

Use user authentication annotations if you want to use {{site.data.keyword.appid_full_notm}} to authenticate with your apps.
{: shortdesc}

### {{site.data.keyword.appid_short_notm}} Authentication (`appid-auth`)
{: #appid-auth}

Use {{site.data.keyword.appid_full_notm}} to authenticate with your app.
{: shortdesc}

**Description**

Authenticate web or API HTTP/HTTPS requests with {{site.data.keyword.appid_short_notm}}.

If you set the request type to web, a web request that contains an {{site.data.keyword.appid_short_notm}} access token is validated. If token validation fails, the web request is rejected. If the request does not contain an access token, then the request is redirected to the {{site.data.keyword.appid_short_notm}} login page. For {{site.data.keyword.appid_short_notm}} web authentication to work, cookies must be enabled in the user's browser.

If you set the request type to api, an API request that contains an {{site.data.keyword.appid_short_notm}} access token is validated. If the request does not contain an access token, a 401: Unauthorized error message is returned to the user.

For security reasons, {{site.data.keyword.appid_short_notm}} authentication supports only back ends with TLS/SSL enabled.
{: note}

**Usage**

Because the app uses {{site.data.keyword.appid_short_notm}} for authentication, you must provision an {{site.data.keyword.appid_short_notm}} instance, configure the instance with valid redirect URIs, and generate a bind secret by binding the instance to your cluster.

1. Choose an existing or create a new {{site.data.keyword.appid_short_notm}} instance.
  * To use an existing instance, ensure that the service instance name doesn't contain spaces. To remove spaces, select the more options menu next to the name of your service instance and select **Rename service**.
  * To provision a [new {{site.data.keyword.appid_short_notm}} instance](https://cloud.ibm.com/catalog/services/app-id):
      1. Replace the auto-filled **Service name** with your own unique name for the service instance. The service instance name can't contain spaces.
      2. Choose the same region that your cluster is deployed in.
      3. Click **Create**.

2. Add redirect URLs for your app. A redirect URL is the callback endpoint of your app. To prevent phishing attacks, {{site.data.keyword.appid_full_notm}} validates the request URL against the allowlist of redirect URLs.
  1. In the {{site.data.keyword.appid_short_notm}} management console, navigate to **Manage Authentication**.
  2. In the **Identity providers** tab, make sure that you have an Identity Provider selected. If no Identity Provider is selected, the user will not be authenticated but will be issued an access token for anonymous access to the app.
  3. In the **Authentication settings** tab, add redirect URLs for your app in the format `http://<hostname>/<app_path>/appid_callback` or `https://<hostname>/<app_path>/appid_callback`.

    {{site.data.keyword.appid_full_notm}} offers a logout function: If `/logout` exists in your {{site.data.keyword.appid_full_notm}} path, cookies are removed and the user is sent back to the login page. To use this function, you must append `/appid_logout` to your domain in the format `https://<hostname>/<app_path>/appid_logout` and include this URL in the redirect URLs list.
    {: note}

3. Bind the {{site.data.keyword.appid_short_notm}} service instance to your cluster. The command creates a service key for the service instance, or you can include the `--key` flag to use existing service key credentials. 
  ```
  ibmcloud oc cluster service bind --cluster <cluster_name_or_ID> --namespace <namespace> --service <service_instance_name> [--key <service_instance_key>]
  ```
  {: pre}
  When the service is successfully added to your cluster, a cluster secret is created that holds the credentials of your service instance. Example CLI output:
  ```
  ibmcloud oc cluster service bind --cluster mycluster --namespace mynamespace --service appid1
  Binding service instance to namespace...
  OK
  Namespace:    mynamespace
  Secret name:  binding-<service_instance_name>
  ```
  {: screen}

4. Get the secret that was created in your cluster namespace.
  ```
  oc get secrets --namespace=<namespace>
  ```
  {: pre}

5. Use the bind secret and the cluster namespace to add the `appid-auth` annotation to your Ingress resource.

<p class="important">When you use the bind secret in the `appid-auth` annotation, the secret is cached by the Ingress ALB. If you change the {{site.data.keyword.appid_short_notm}} service binding, the new secret for {{site.data.keyword.appid_short_notm}} that is generated is not used by the ALB. You must restart your ALB pods to pick up the new secret.  You can find the ALB pod names by running `oc get pods -n kube-system | grep alb` and restart the ALB pods by running `oc delete pod <pod> -n kube-system` for each pod.</p>


**Sample Ingress resource YAML**

```yaml
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: myingress
  annotations:
    ingress.bluemix.net/appid-auth: "bindSecret=<bind_secret> namespace=<namespace> requestType=<request_type> serviceName=<myservice> idToken=true"
spec:
  tls:
  - hosts:
    - mydomain
    secretName: mytlssecret
  rules:
  - host: mydomain
    http:
      paths:
      - path: /
        backend:
          serviceName: myservice
          servicePort: 8080
```
{: codeblock}

|Annotation field|Value|
|----------------|-----|
| `bindSecret` | Replace <em>`<bind_secret>`</em> with the Kubernetes secret, which stores the bind secret for your {{site.data.keyword.appid_short_notm}} service instance. |
| `namespace` | Replace <em>`<namespace>`</em> with the namespace of the bind secret. This field defaults to the `default` namespace. |
| `requestType` | Replace <em>`<request_type>`</em> with the type of request you want to send to {{site.data.keyword.appid_short_notm}}. Accepted values are `web` or `api`. The default is `api`. |
| `serviceName` | Replace <em>`<myservice>`</em> with the name of the Kubernetes service that you created for your app. This field is required. Specify only one service name per service path that you define in the resource file. |
| `idToken=true` | Optional: The Liberty OIDC client is unable to parse both the access and the identity token at the same time. When working with Liberty, set this value to false so that the identity token is not sent to the Liberty server. |
{: caption="Understanding the annotation components" caption-side="top"}



## Preserving the source IP address
{: #preserve_source_ip}

By default, the source IP address of the client request is not preserved. When a client request to your app is sent to your cluster, the request is routed to a pod for the load balancer service that exposes the ALB. If no app pod exists on the same worker node as the load balancer service pod, the load balancer forwards the request to an app pod on a different worker node. The source IP address of the package is changed to the public IP address of the worker node where the app pod runs.

To preserve the original source IP address of the client request, you can enable [source IP preservation](https://kubernetes.io/docs/tutorials/services/source-ip/#source-ip-for-services-with-typeloadbalancer){: external}. Preserving the client’s IP is useful, for example, when app servers have to apply security and access-control policies.

<p class="note">When source IP preservation is enabled, load balancers shift from forwarding traffic to an app pod on a different worker node to an app pod on the same worker node. Your apps might experience downtime during this shift.</br></br>If you [disable an ALB](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_alb_configure), any source IP changes you make to the load balancer service that exposes the ALB are lost. When you re-enable the ALB, you must enable source IP again.</p>

**Before you begin**: If you configured edge nodes in your cluster, ALB pods are deployed to edge nodes and can only forward traffic to app pods that are also deployed to those edge nodes. Ensure that you have [at least three edge worker nodes per zone](/docs/openshift?topic=openshift-edge#edge_nodes).

To enable source IP preservation, edit the load balancer service that exposes an Ingress ALB:

1. Enable source IP preservation for a single ALB or for all the ALBs in your cluster.
    * To set up source IP preservation for a single ALB:
        1. Get the ID of the ALB for which you want to enable source IP. The ALB services have a format similar to `public-cr18e61e63c6e94b658596ca93d087eed9-alb1` for a public ALB or `private-cr18e61e63c6e94b658596ca93d087eed9-alb1` for a private ALB.
            ```
            oc get svc -n kube-system | grep alb
            ```
            {: pre}

        2. Open the YAML for the load balancer service that exposes the ALB.
            ```
            oc edit svc <ALB_ID> -n kube-system
            ```
            {: pre}

        3. Under **`spec`**, change the value of **`externalTrafficPolicy`** from `Cluster` to `Local`.

        4. Save and close the configuration file. The output is similar to the following:

            ```
            service "public-cr18e61e63c6e94b658596ca93d087eed9-alb1" edited
            ```
            {: screen}
    * To set up source IP preservation for all public ALBs in your cluster, run the following command:
        ```
        oc get svc -n kube-system | grep alb | awk '{print $1}' | grep "^public" | while read alb; do oc patch svc $alb -n kube-system -p '{"spec":{"externalTrafficPolicy":"Local"}}'; done
        ```
        {: pre}

        Example output:
        ```
        "public-cr18e61e63c6e94b658596ca93d087eed9-alb1", "public-cr17e61e63c6e94b658596ca92d087eed9-alb2" patched
        ```
        {: screen}

    * To set up source IP preservation for all private ALBs in your cluster, run the following command:
        ```
        oc get svc -n kube-system | grep alb | awk '{print $1}' | grep "^private" | while read alb; do oc patch svc $alb -n kube-system -p '{"spec":{"externalTrafficPolicy":"Local"}}'; done
        ```
        {: pre}

        Example output:
        ```
        "private-cr18e61e63c6e94b658596ca93d087eed9-alb1", "private-cr17e61e63c6e94b658596ca92d087eed9-alb2" patched
        ```
        {: screen}

2. Verify that the source IP is being preserved in your ALB pods logs.
    1. Get the ID of a pod for the ALB that you modified.
        ```
        oc get pods -n kube-system | grep alb
        ```
        {: pre}

    2. Open the logs for that ALB pod. Verify that the IP address for the `client` field is the client request IP address instead of the load balancer service IP address.
        ```
        oc logs <ALB_pod_ID> nginx-ingress -n kube-system
        ```
        {: pre}

3. Now, when you look up the headers for the requests that are sent to your back-end app, you can see the client IP address in the `x-forwarded-for` header.

4. If you no longer want to preserve the source IP, you can revert the changes that you made to the service.
    * To revert source IP preservation for your public ALBs:
        ```
        oc get svc -n kube-system | grep alb | awk '{print $1}' | grep "^public" | while read alb; do oc patch svc $alb -n kube-system -p '{"spec":{"externalTrafficPolicy":"Cluster"}}'; done
        ```
        {: pre}
    * To revert source IP preservation for your private ALBs:
        ```
        oc get svc -n kube-system | grep alb | awk '{print $1}' | grep "^private" | while read alb; do oc patch svc $alb -n kube-system -p '{"spec":{"externalTrafficPolicy":"Cluster"}}'; done
        ```
        {: pre}

<br />

## Configuring SSL protocols and SSL ciphers at the HTTP level
{: #ssl_protocols_ciphers}

Enable SSL protocols and ciphers at the global HTTP level by editing the `ibm-cloud-provider-ingress-cm` configmap.
{: shortdesc}

For example, if you still have legacy clients that require TLS 1.0 or 1.1 support, you must manually enable these TLS versions to override the default setting of TLS 1.2 and TLS 1.3 only. For more information about how to see the TLS versions that your clients use to access your apps, see this [{{site.data.keyword.cloud_notm}} blog post](https://www.ibm.com/cloud/blog/ibm-cloud-kubernetes-service-alb-update-tls-1-0-and-1-1-disabled-by-default).

When you specify the enabled protocols for all hosts, the TLSv1.1 and TLSv1.2 parameters (1.1.13, 1.0.12) work only when OpenSSL 1.0.1 or higher is used. The TLSv1.3 parameter (1.13.0) works only when OpenSSL 1.1.1 built with TLSv1.3 support is used.
{: note}

To edit the configmap to enable SSL protocols and ciphers:

1. Edit the configuration file for the `ibm-cloud-provider-ingress-cm` configmap resource.

    ```
    oc edit cm ibm-cloud-provider-ingress-cm -n kube-system
    ```
    {: pre}

2. Add the SSL protocols and ciphers. Format ciphers according to the [OpenSSL library cipher list format](https://www.openssl.org/docs/man1.0.2/man1/ciphers.html){: external}.

   ```yaml
   apiVersion: v1
   data:
     ssl-protocols: "TLSv1 TLSv1.1 TLSv1.2 TLSv1.3"
     ssl-ciphers: "HIGH:!aNULL:!MD5:!CAMELLIA:!AESCCM:!ECDH+CHACHA20"
   kind: ConfigMap
   metadata:
     name: ibm-cloud-provider-ingress-cm
     namespace: kube-system
   ```
   {: codeblock}

3. Save the configuration file.

4. Verify that the configmap changes were applied. The changes are applied to your ALBs automatically.

   ```
   oc get cm ibm-cloud-provider-ingress-cm -n kube-system -o yaml
   ```
   {: pre}

<br />

## Sending your custom certificate to legacy clients
{: #default_server_cert}

If you have legacy devices that do not support Server Name Indication (SNI) and you use a [custom TLS certificate in your Ingress resources](/docs/openshift?topic=openshift-ingress#public_inside_3), you must edit the ALB's server settings to use your custom TLS certificate and custom TLS secret.
{: shortdesc}

When you create a classic cluster, a Let's Encrypt certificate is generated for the default Ingress secret that IBM provides. If you create a custom secret in your cluster and specify this custom secret for TLS termination in your Ingress resources, the Ingress ALB sends the certificate for your custom secret to the client instead of the default Let's Encrypt certificate. However, if a client does not support SNI, the Ingress ALB defaults to the Let's Encrypt certificate because the default secret is listed in the ALB's default server settings. To send your custom certificate to devices that do not support SNI, complete the following steps to change the ALB's default server settings to your custom secret.

1. Edit the `alb-default-server` Ingress resource.
    ```
    oc edit ingress alb-default-server -n kube-system
    ```
    {: pre}

2. In the `spec.tls` section, change the value of the `hosts.secretName` setting to the name of your custom secret that contains your custom certificate.
   Example:
   ```yaml
   spec:
     rules:
     ...
     tls:
     - hosts:
       - invalid.mycluster-<hash>-0000.us-south.containers.appdomain.cloud
       secretName: <custom_secret_name>
   ```
   {: codeblock}

3. Save the resource file.

4. Verify that the resource now points to your custom secret name. The changes are applied to your ALBs automatically.
   ```
   oc get ingress alb-default-server -n kube-system -o yaml
   ```
   {: pre}

<br />

## Tuning ALB performance
{: #perf_tuning}

To optimize performance of your Ingress ALBs, you can change the default settings according to your needs.
{: shortdesc}

### Adding ALB socket listeners for each NGINX worker process
{: #reuse-port}

Increase the number of socket listeners from one socket listener for each ALB to one socket listener for each NGINX worker process for that ALB by using the `reuse-port` Ingress directive.
{: shortdesc}

When the `reuse-port` option is disabled, a single listening socket notifies an ALB about incoming connections, and all NGINX worker processes for that ALB attempt to take the connection. But when `reuse-port` is enabled, one socket listener exists for each worker process. Instead of each worker process attempting to take the connection, the Linux kernel determines which available socket listener gets the connection. Lock contention between workers is reduced, which can improve performance. For more information about the benefits and drawbacks of the `reuse-port` directive, see [this NGINX blog post](https://www.nginx.com/blog/socket-sharding-nginx-release-1-9-1/){: external}.

1. Edit the configuration file for the `ibm-cloud-provider-ingress-cm` configmap resource.
    ```
    oc edit cm ibm-cloud-provider-ingress-cm -n kube-system
    ```
    {: pre}

2. In the `data` section, add `reuse-port: "true"`. Example:
   ```yaml
   apiVersion: v1
   data:
     private-ports: 80;443;9443
     public-ports: 80;443
     reuse-port: "true"
   ...
   ```
   {: codeblock}

3. Save the configuration file.

4. Verify that the configmap changes were applied. The changes are applied to your ALBs automatically.

   ```
   oc get cm ibm-cloud-provider-ingress-cm -n kube-system -o yaml
   ```
   {: pre}

### Enabling log buffering and flush timeout
{: #access-log}

By default, the Ingress ALB logs each request as it arrives. If you have an environment that is heavily used, logging each request as it arrives can greatly increase disk I/O utilization. To avoid continuous disk I/O, you can enable log buffering and flush timeout for the ALB by editing the `ibm-cloud-provider-ingress-cm` Ingress configmap. When buffering is enabled, instead of performing a separate write operation for each log entry, the ALB buffers a series of entries and writes them to the file together in a single operation.
{: shortdesc}

1. Create and edit the configuration file for the `ibm-cloud-provider-ingress-cm` configmap resource.

    ```
    oc edit cm ibm-cloud-provider-ingress-cm -n kube-system
    ```
    {: pre}

2. Edit the configmap.
    1. Enable log buffering by adding the `access-log-buffering` field and setting it to `"true"`.

    2. Set the threshold for when the ALB should write buffered contents to the log.
        * Buffer size: Add the `buffer` field and set it to how much log memory can be held in the buffer before the ALB writes the buffered contents to the log file. For example, if the default value of `100KB` is used, the ALB writes buffer contents to the log file every time the buffer reaches 100KB of log content.
        * Time interval: Add the `flush` field and set it to how often the ALB should write to the log file. For example, if the default value of `5m` is used, the ALB writes buffer contents to the log file once every 5 minutes.
        * Time interval or buffer size: When both `flush` and `buffer` are set, the ALB writes buffer content to the log file based on whichever threshold parameter is met first.

      ```yaml
      apiVersion: v1
      kind: ConfigMap
      data:
        access-log-buffering: "true"
        flush-interval: "5m"
        buffer-size: "100KB"
      metadata:
        name: ibm-cloud-provider-ingress-cm
        ...
      ```
      {: codeblock}

3. Save the configuration file.

4. Verify that the logs for an ALB now contain buffered content that is written according to the memory size or time interval you set.

   ```
   oc logs -n kube-system <ALB_ID> -c nginx-ingress
   ```
   {: pre}

### Changing the number or duration of keepalive connections
{: #keepalive_time}

Keepalive connections can have a major impact on performance by reducing the CPU and network usage that is needed to open and close connections. To optimize the performance of your ALBs, you can change the maximum number of keepalive connections between the ALB and the client and how long the keepalive connections can last.
{: shortdesc}

1. Edit the configuration file for the `ibm-cloud-provider-ingress-cm` configmap resource.

    ```
    oc edit cm ibm-cloud-provider-ingress-cm -n kube-system
    ```
    {: pre}

2. Change the values of `keep-alive-requests` and `keep-alive`.
    * `keep-alive-requests`: The number of keepalive client connections that can stay open to the Ingress ALB. The default is `4096`.
    * `keep-alive`: The timeout, in seconds, during which the keepalive client connection stays open to the Ingress ALB. The default is `8s`.
   ```yaml
   apiVersion: v1
   data:
     keep-alive-requests: "4096"
     keep-alive: "8s"
   kind: ConfigMap
   metadata:
     name: ibm-cloud-provider-ingress-cm
     namespace: kube-system
   ```
   {: codeblock}

3. Save the configuration file.

4. Verify that the configmap changes were applied. The changes are applied to your ALBs automatically.

   ```
   oc get cm ibm-cloud-provider-ingress-cm -n kube-system -o yaml
   ```
   {: pre}

### Changing the pending connections backlog
{: #backlog}

You can decrease the default backlog setting for how many pending connections can wait in the server queue.
{: shortdesc}

In the `ibm-cloud-provider-ingress-cm` Ingress configmap, the `backlog` field sets the maximum number of pending connections that can wait in the server queue. By default, `backlog` is set to `32768`. You can override the default by editing the Ingress configmap.

1. Edit the configuration file for the `ibm-cloud-provider-ingress-cm` configmap resource.

    ```
    oc edit cm ibm-cloud-provider-ingress-cm -n kube-system
    ```
    {: pre}

2. Change the value of `backlog` from `32768` to a lower value. The value must be equal to or lesser than 32768.

   ```yaml
   apiVersion: v1
   data:
     backlog: "32768"
   kind: ConfigMap
   metadata:
     name: ibm-cloud-provider-ingress-cm
     namespace: kube-system
   ```
   {: codeblock}

3. Save the configuration file.

4. Verify that the configmap changes were applied. The changes are applied to your ALBs automatically.

   ```
   oc get cm ibm-cloud-provider-ingress-cm -n kube-system -o yaml
   ```
   {: pre}




