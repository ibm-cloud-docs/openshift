---

copyright:
  years: 2014, 2020
lastupdated: "2020-08-24"

keywords: openshift, roks, rhoks, rhos, nginx, ingress controller

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



# Beta: Kubernetes Ingress annotations
{: #comm-ingress-annotations}

Modify default ALB settings and add annotations to your Ingress resources for ALBs that run the Kubernetes Ingress image.
{: shortdesc}

Using the Kubernetes Ingress image for your ALBs is a beta feature. Beta features might experience intermittent errors.
{: beta}

<img src="images/icon-version-311.png" alt="Version 3.11 icon" width="30" style="width:30px; border-style: none"/> This information is for clusters that run {{site.data.keyword.openshiftshort}} version 3.11 only. To learn about Ingress for {{site.data.keyword.openshiftshort}} version 4, see [About Ingress in {{site.data.keyword.openshiftshort}} version 4](/docs/openshift?topic=openshift-ingress-about-roks4).
{: important}

## Customizing routing with annotations
{: #annotations}

To customize routing for Ingress, you can add [Kubernetes NGINX annotations](https://kubernetes.github.io/ingress-nginx/user-guide/nginx-configuration/annotations/){: external} (`nginx.ingress.kubernetes.io/<annotation>`). Custom {{site.data.keyword.openshiftlong_notm}} annotations (`ingress.bluemix.net/<annotation>`) are **not** supported.
{: shortdesc}

The following sections compares the custom {{site.data.keyword.openshiftlong_notm}} annotations with equivalent Kubernetes NGINX annotations. If no equivalent Kubernetes NGINX annotation exists, alternate options, such as configuring a field in the `ibm-k8s-controller-config` configmap or the `ibm-ingress-deploy-config` configmap, are listed.

Kubernetes NGINX annotations are always applied to all service paths in the resource, and you cannot specify service names within the annotations.
{: note}

### Add server port to host header

Add a server port to the client request before the request is forwarded to your back-end app.
{: shortdesc}

Previous {{site.data.keyword.openshiftlong_notm}} Ingress resource [annotation](/docs/openshift?topic=openshift-ingress_annotation#add-host-port):

```
ingress.bluemix.net/add-host-port: "enabled=true serviceName=app1"
```
{: screen}

Kubernetes Ingress field: No equivalent annotation exists. Configure proxying external services in a [server snippet annotation](https://kubernetes.github.io/ingress-nginx/user-guide/nginx-configuration/annotations/#server-snippet){:external} or as an `ibm-k8s-controller-config` configmap [field](https://kubernetes.github.io/ingress-nginx/user-guide/nginx-configuration/configmap/#proxy-set-headers){:external}.


### ALB ID

Route incoming requests to your apps with a private ALB.
{: shortdesc}

Previous {{site.data.keyword.openshiftlong_notm}} Ingress resource [annotation](/docs/openshift?topic=openshift-ingress_annotation#alb-id):

```
ingress.bluemix.net/alb-id: "private_ALB_ID"
```
{: screen}

Kubernetes Ingress resource [annotation](/docs/openshift?topic=openshift-ingress-types#alb-comm-create): Private ALBs are configured to use resources with this class.

```
kubernetes.io/ingress.class: "private-iks-k8s-nginx"
```
{: screen}

### {{site.data.keyword.appid_short_notm}} authentication

Configure Ingress with [{{site.data.keyword.appid_full_notm}}](https://cloud.ibm.com/catalog/services/app-id){: external} to enforce authentication for your apps.
{: shortdesc}

Previous {{site.data.keyword.openshiftlong_notm}} Ingress resource [annotation](/docs/openshift?topic=openshift-ingress_annotation#appid-auth):

```
ingress.bluemix.net/appid-auth: "bindSecret=bind_secret namespace=default requestType=web serviceName=app1 idToken=true"
```
{: screen}

Kubernetes Ingress field: See [Adding {{site.data.keyword.appid_short_notm}} authentication to apps](#app-id).


### Client request body size

Set the maximum size of the body that the client can send as part of a request.
{: shortdesc}

Previous {{site.data.keyword.openshiftlong_notm}} Ingress resource [annotations](/docs/openshift?topic=openshift-ingress_annotation#client-max-body-size):

```
ingress.bluemix.net/client-max-body-size: "serviceName=app1 size=200m"
```
{: screen}

Kubernetes `ibm-k8s-controller-config` configmap [field](https://kubernetes.github.io/ingress-nginx/user-guide/nginx-configuration/configmap/#proxy-body-size){: external}:

```
proxy-body-size: 200m
```
{: screen}


### Client response data buffering

Disable or enable the storage of response data on the ALB while the data is sent to the client.
{: shortdesc}

Previous {{site.data.keyword.openshiftlong_notm}} Ingress resource [annotation](/docs/openshift?topic=openshift-ingress_annotation#proxy-buffering):

```
ingress.bluemix.net/proxy-buffering: "enabled=false serviceName=app1"
```
{: screen}

Kubernetes Ingress field: Disabled by default. To enable, set the Ingress resource [annotation](https://kubernetes.github.io/ingress-nginx/user-guide/nginx-configuration/annotations/#rewrite){:external}:

```
nginx.ingress.kubernetes.io/proxy-buffering: "on"
```
{: screen}


### Custom connect and read timeouts

Set the time that the ALB waits to connect to and read from the back-end app before the back-end app is considered unavailable.
{: shortdesc}

Previous {{site.data.keyword.openshiftlong_notm}} Ingress resource [annotations](/docs/openshift?topic=openshift-ingress_annotation#proxy-connect-timeout):

```
ingress.bluemix.net/proxy-connect-timeout: "serviceName=app1 timeout=62s"
```
{: screen}
```
ingress.bluemix.net/proxy-read-timeout: "serviceName=app1 timeout=62s"
```
{: screen}

Kubernetes Ingress resource [annotations](https://kubernetes.github.io/ingress-nginx/user-guide/nginx-configuration/annotations/#custom-timeouts){:external}:

```
nginx.ingress.kubernetes.io/proxy-connect-timeout: 62
```
{: screen}
```
nginx.ingress.kubernetes.io/proxy-read-timeout: 62
```
{: screen}


### Custom error actions

Indicate custom actions that the ALB can take for specific HTTP errors.
{: shortdesc}

Previous {{site.data.keyword.openshiftlong_notm}} Ingress resource [annotations](/docs/openshift?topic=openshift-ingress_annotation#custom-errors):

```
ingress.bluemix.net/custom-errors: "serviceName=app1 httpError=401 errorActionName=/errorAction401"
```
{: screen}
```
ingress.bluemix.net/custom-error-actions: |
  errorActionName=/errorAction401
  proxy_pass http://example.com/forbidden.html;
  <EOS>
```
{: screen}

Kubernetes Ingress field: See the [`custom-http-errors` documentation](https://kubernetes.github.io/ingress-nginx/examples/customization/custom-errors/){:external}.


### Custom HTTP and HTTPS ports

Change the default ports for HTTP (port 80) and HTTPS (port 443) network traffic.
{: shortdesc}

Previous {{site.data.keyword.openshiftlong_notm}} Ingress fields:
* Ingress resource [annotation](/docs/openshift?topic=openshift-ingress_annotation#custom-port):
    ```
    ingress.bluemix.net/custom-port: "protocol=http port=8080;protocol=https port=8443"
    ```
    {: screen}
* `ibm-k8s-controller-config` configmap [field](/docs/containers?topic=containers-ingress_annotation#open_ports_iks):
    ```
    public-ports: "80;443;9443"
    ```
    {: screen}

Kubernetes Ingress fields:
* `ibm-ingress-deploy-config` configmap [fields](#comm-customize-deploy):
    ```
    httpPort=8080
    httpsPort=8443
    ```
    {: screen}
* [Modify each ALB service](/docs/containers?topic=containers-ingress_annotation#open_ports_kube)</li></ul>


### Custom request header

Add header information to a client request before forwarding the request to your back-end app.
{: shortdesc}

Previous {{site.data.keyword.openshiftlong_notm}} Ingress resource [annotation](/docs/openshift?topic=openshift-ingress_annotation#proxy-add-headers):

```
ingress.bluemix.net/proxy-add-headers: |
  serviceName=app1 {
  X-Different-Name “true”;
  x-request-start “t=${sec}”;
  x-using-nginx “true”
  }
```
{: screen}

Kubernetes `ibm-k8s-controller-config` configmap [field](https://kubernetes.github.io/ingress-nginx/user-guide/nginx-configuration/configmap/#proxy-set-headers):

```
proxy-set-headers: "ingress-nginx/custom-headers"
```
{: screen}

For the `custom-headers` configmap requirements, see [this example](https://github.com/kubernetes/ingress-nginx/blob/master/docs/examples/customization/custom-headers/custom-headers.yaml){:external}.


### Custom response header

Add header information to a client response before sending it to the client.
{: shortdesc}

Previous {{site.data.keyword.openshiftlong_notm}} Ingress resource [annotation](/docs/openshift?topic=openshift-ingress_annotation#proxy-add-headers):

```
ingress.bluemix.net/response-add-headers: |
  serviceName=<myservice1> {
  <header1>:<value1>;
```
{: screen}

Kubernetes Ingress resource [annotation](https://kubernetes.github.io/ingress-nginx/user-guide/nginx-configuration/annotations/#configuration-snippet){:external}:

```
nginx.ingress.kubernetes.io/configuration-snippet: |
  more_set_headers "Request-Id: $req_id";
```
{: screen}


### External services

Add path definitions to external services, such as services hosted in IBM Cloud.
{: shortdesc}

Previous {{site.data.keyword.openshiftlong_notm}} Ingress resource [annotation](/docs/openshift?topic=openshift-ingress_annotation#proxy-external-service):

```
ingress.bluemix.net/proxy-external-service: "path=/path external-svc=https:myexternal_service host=ingress_subdomain"
```
{: screen}

Kubernetes Ingress field: No equivalent annotation exists. Configure proxying external services in a [location snippet](https://kubernetes.github.io/ingress-nginx/user-guide/nginx-configuration/annotations/#configuration-snippet){:external} or replace proxying with a [permanent redirect to external services](https://kubernetes.github.io/ingress-nginx/user-guide/nginx-configuration/annotations/#permanent-redirect){:external}.


### HTTP redirects to HTTPS

Convert insecure HTTP client requests to HTTPS.
{: shortdesc}

Previous {{site.data.keyword.openshiftlong_notm}} Ingress resource [annotation](/docs/openshift?topic=openshift-ingress_annotation#redirect-to-https):

```
ingress.bluemix.net/redirect-to-https: "True"
```
{: screen}

Kubernetes Ingress fields: HTTP redirects to HTTPS by default. To disable:

* `ibm-k8s-controller-config` configmap [field](https://kubernetes.github.io/ingress-nginx/user-guide/nginx-configuration/configmap/#server-side-https-enforcement-through-redirect){:external}:
    ```
    ssl-redirect: "false"
    ```
    {: screen}
* Ingress resource [annotation](https://kubernetes.github.io/ingress-nginx/user-guide/nginx-configuration/annotations/#server-side-https-enforcement-through-redirect){:external}:
    ```
    nginx.ingress.kubernetes.io/ssl-redirect: "false"
    ```
    {: screen}


### HTTP Strict Transport Security

Set the browser to access the domain only by using HTTPS.
{: shortdesc}

Previous {{site.data.keyword.openshiftlong_notm}} Ingress resource [annotation](/docs/openshift?topic=openshift-ingress_annotation#hsts):

```
ingress.bluemix.net/hsts: enabled=true maxAge=31536000 includeSubdomains=true
```
{: screen}

Kubernetes Ingress fields: HSTS is enabled by default.
* To add max age and subdomain granularity, see [this NGINX blog](https://www.nginx.com/blog/http-strict-transport-security-hsts-and-nginx/){:external}.
* To disable, set the `ibm-k8s-controller-config` configmap [field](https://kubernetes.github.io/ingress-nginx/user-guide/nginx-configuration/configmap/#hsts){:external}:
    ```
    hsts: false
    ```
    {: screen}


### Keepalive requests

Set the maximum number of requests that can be served through one keepalive connection.
{: shortdesc}

Previous {{site.data.keyword.openshiftlong_notm}} Ingress resource [annotation](/docs/openshift?topic=openshift-ingress_annotation#keepalive-requests):

```
ingress.bluemix.net/keepalive-requests: "serviceName=app1 requests=75"
```
{: screen}


Kubernetes `ibm-k8s-controller-config` configmap [field](https://kubernetes.github.io/ingress-nginx/user-guide/nginx-configuration/configmap/#keep-alive-requests){:external}:

```
keep-alive: 75
```
{: screen}


### Large client header buffers

Set the maximum number and size of buffers that read large client request headers.
{: shortdesc}

Previous {{site.data.keyword.openshiftlong_notm}} Ingress resource [annotation](/docs/containers?topic=containers-ingress_annotation#large-client-header-buffersh):

```
ingress.bluemix.net/large-client-header-buffers: "number=4 size=8k"
```
{: screen}

Kubernetes `ibm-k8s-controller-config` configmap [field](https://kubernetes.github.io/ingress-nginx/user-guide/nginx-configuration/configmap/#large-client-header-buffers){:external}:

```
large-client-header-buffers: 4 8k
```
{: screen}


### Location modifier

Modify the way the ALB matches the request URI against the app path.
{: shortdesc}

Previous {{site.data.keyword.openshiftlong_notm}} Ingress resource [annotation](/docs/openshift?topic=openshift-ingress_annotation#location-modifier):

```
ingress.bluemix.net/location-modifier: "modifier='~' serviceName=app1"
```
{: screen}

Kubernetes Ingress resource [annotation](https://kubernetes.github.io/ingress-nginx/user-guide/nginx-configuration/annotations/#use-regex){:external}:

```
nginx.ingress.kubernetes.io/use-regex: "true"
```
{: screen}

For more info, see [this blog](https://kubernetes.github.io/ingress-nginx/user-guide/ingress-path-matching/#ingress-path-matching){: external}.


### Location snippets

Add a custom location block configuration for a service.
{: shortdesc}

Previous {{site.data.keyword.openshiftlong_notm}} Ingress resource [annotation](/docs/openshift?topic=openshift-ingress_annotation#location-snippets):

```
ingress.bluemix.net/location-snippets: |
  serviceName=app1
  more_set_headers "Request-Id: $req_id";
  <EOS>
```
{: screen}

Kubernetes Ingress resource [annotation](https://kubernetes.github.io/ingress-nginx/user-guide/nginx-configuration/annotations/#configuration-snippet){:external}:

```
nginx.ingress.kubernetes.io/configuration-snippet: |
  more_set_headers "Request-Id: $req_id";
```
{: screen}


### Mutual authentication

Configure mutual authentication for the ALB.
{: shortdesc}

Previous {{site.data.keyword.openshiftlong_notm}} Ingress resource [annotation](/docs/openshift?topic=openshift-ingress_annotation#mutual-auth):

```
ingress.bluemix.net/mutual-auth: "secretName=mysecret port=9080 serviceName=app1"
```
{: screen}

Kubernetes Ingress resource [annotations](https://kubernetes.github.io/ingress-nginx/user-guide/nginx-configuration/annotations/#client-certificate-authentication){:external}:

```
nginx.ingress.kubernetes.io/auth-tls-verify-client: "on"
nginx.ingress.kubernetes.io/auth-tls-secret: "default/ca-secret"
nginx.ingress.kubernetes.io/auth-tls-verify-depth: "1"
nginx.ingress.kubernetes.io/auth-tls-error-page: "http://www.mysite.com/error-cert.html"
nginx.ingress.kubernetes.io/auth-tls-pass-certificate-to-upstream: "true"
```
{: screen}

Note that mutual authentication cannot be applied to custom ports and must be applied to the HTTPS port.


### Proxy buffer size

Configure the size of the proxy buffer that reads the first part of the response.
{: shortdesc}

Previous {{site.data.keyword.openshiftlong_notm}} Ingress resource [annotation](/docs/openshift?topic=openshift-ingress_annotation#proxy-buffer-size):

```
ingress.bluemix.net/proxy-buffer-size: "serviceName=app1 size=8k"
```
{: screen}

Kubernetes Ingress resource [annotation](https://kubernetes.github.io/ingress-nginx/user-guide/nginx-configuration/annotations/#proxy-buffer-size){:external}:

```
nginx.ingress.kubernetes.io/proxy-buffer-size: "8k"
```
{: screen}


### Proxy buffers

Configure the number and size of proxy buffers for the ALB.
{: shortdesc}

Previous {{site.data.keyword.openshiftlong_notm}} Ingress resource [annotation](/docs/openshift?topic=openshift-ingress_annotation#proxy-buffers):

```
ingress.bluemix.net/proxy-buffers: "serviceName=app1 number=4 size=8k"
```
{: screen}

Kubernetes Ingress resource [annotations](https://kubernetes.github.io/ingress-nginx/user-guide/nginx-configuration/annotations/#proxy-buffering){:external}:

```
nginx.ingress.kubernetes.io/proxy-buffers-number: "4"
nginx.ingress.kubernetes.io/proxy-buffer-size: "8k"
```
{: screen}


### Proxy busy buffers size

Configure the size of proxy buffers that can be busy.
{: shortdesc}

Previous {{site.data.keyword.openshiftlong_notm}} Ingress resource [annotation](/docs/openshift?topic=openshift-ingress_annotation#proxy-busy-buffers-size):

```
ingress.bluemix.net/proxy-busy-buffers-size: "serviceName=app1 size=8k"
```
{: screen}

Kubernetes Ingress field: No equivalent annotation exists. Configure proxying external services in a [location snippet](https://kubernetes.github.io/ingress-nginx/user-guide/nginx-configuration/annotations/#configuration-snippet){:external}. For more info, see the [NGINX docs](http://nginx.org/en/docs/http/ngx_http_proxy_module.html#proxy_busy_buffers_size){: external}.


### Proxy next upstream

Set when the ALB can pass a request to the next upstream server.
{: shortdesc}

Previous {{site.data.keyword.openshiftlong_notm}} Ingress resource [annotation](/docs/openshift?topic=openshift-ingress_annotation#proxy-next-upstream-config):

```
ingress.bluemix.net/proxy-next-upstream-config: "serviceName=app1 retries=3 timeout=50s http_502=true non_idempotent=true"
```
{: screen}

Kubernetes Ingress fields:
* Global setting: `ibm-k8s-controller-config` configmap [fields](http://nginx.org/en/docs/http/ngx_http_proxy_module.html#proxy_next_upstream){:external}:
    ```
    retry-non-idempotent: true
    proxy-next-upstream: error timeout http_500
    ```
    {: screen}
* Per-resource setting: Ingress resource [annotations](https://kubernetes.github.io/ingress-nginx/user-guide/nginx-configuration/annotations/#custom-timeouts){:external}:
    ```
    nginx.ingress.kubernetes.io/proxy-next-upstream: http_500
    nginx.ingress.kubernetes.io/proxy-next-upstream-timeout: 50
    nginx.ingress.kubernetes.io/proxy-next-upstream-tries: 3
    ```
    {: screen}


### Rate limiting

Limit the request processing rate and number of connections per a defined key for all or specific services.
{: shortdesc}

Previous {{site.data.keyword.openshiftlong_notm}} Ingress resource [annotations](/docs/openshift?topic=openshift-ingress_annotation#global-rate-limit):

```
ingress.bluemix.net/global-rate-limit: "key=location rate=10r/s conn=75"
ingress.bluemix.net/service-rate-limit: "serviceName=app1 key=location rate=10r/s conn=75"
```
{: screen}

Kubernetes Ingress field: No directly equivalent annotation exists, but several Ingress resource [annotations for rate limiting](https://kubernetes.github.io/ingress-nginx/user-guide/nginx-configuration/annotations/#rate-limiting){: external} are available.


### Response header removal

Remove header information that is included in the client response from the back-end end app before the response is sent to the client.
{: shortdesc}

Previous {{site.data.keyword.openshiftlong_notm}} Ingress resource [annotation](/docs/openshift?topic=openshift-ingress_annotation#response-remove-headers):

```
ingress.bluemix.net/response-remove-headers: |
      serviceName=app1 {
      "header1";
      }
```
{: screen}

Kubernetes Ingress field: No equivalent annotation exists. Configure response header removal in a [location snippet](https://github.com/openresty/headers-more-nginx-module#more_clear_headers){:external}, or use the [`proxy_hide_header` field](http://nginx.org/en/docs/http/ngx_http_proxy_module.html#proxy_hide_header){:external} as a [configuration snippet](https://kubernetes.github.io/ingress-nginx/user-guide/nginx-configuration/annotations/#configuration-snippet){: external} in the `ibm-k8s-controller-config` configmap.


### Rewrite paths

Route incoming network traffic on an ALB domain path to a different path that your back-end app listens on.
{: shortdesc}

Previous {{site.data.keyword.openshiftlong_notm}} Ingress resource [annotation](/docs/openshift?topic=openshift-ingress_annotation#rewrite-path):

```
ingress.bluemix.net/rewrite-path: "serviceName=app1 rewrite=/newpath
```
{: screen}

Kubernetes Ingress resource [annotation](https://kubernetes.github.io/ingress-nginx/user-guide/nginx-configuration/annotations/#rewrite){:external}:

```
nginx.ingress.kubernetes.io/rewrite-target: /newpath
```
{: screen}


### Server snippets

Add a custom server block configuration.
{: shortdesc}

Previous {{site.data.keyword.openshiftlong_notm}} Ingress resource [annotation](/docs/openshift?topic=openshift-ingress_annotation#server-snippets):

```
ingress.bluemix.net/server-snippets: |
  location = /health {
  return 200 'Healthy';
  add_header Content-Type text/plain;
  }
```
{: screen}

Kubernetes Ingress resource [annotation](https://kubernetes.github.io/ingress-nginx/user-guide/nginx-configuration/annotations/#server-snippet){:external}:

```
nginx.ingress.kubernetes.io/server-snippet: |
  location = /health {
  return 200 'Healthy';
  add_header Content-Type text/plain;
  }
```
{: screen}


### Session affinity with cookies

Always route incoming network traffic to the same upstream server by using a sticky cookie.
{: shortdesc}

Previous {{site.data.keyword.openshiftlong_notm}} Ingress resource [annotation](/docs/openshift?topic=openshift-ingress_annotation#sticky-cookie-services):

```
ingress.bluemix.net/sticky-cookie-services: "serviceName=app1 path=/app1 name=cookie_name1 expires=48h secure httponly"
```
{: screen}

Kubernetes Ingress resource [annotations](https://kubernetes.github.io/ingress-nginx/user-guide/nginx-configuration/annotations/#session-affinity){:external}:

```
nginx.ingress.kubernetes.io/affinity: "cookie"
nginx.ingress.kubernetes.io/session-cookie-name: "cookie_name1"
nginx.ingress.kubernetes.io/session-cookie-expires: "172800"
nginx.ingress.kubernetes.io/session-cookie-max-age: "172800"
nginx.ingress.kubernetes.io/configuration-snippet: |
  more_set_headers "Set-Cookie: HttpOnly";
```
{: screen}

The Kubernetes Ingress controller adds the `Secure` and `HttpOnly` attributes to the sticky cookies by default, which cannot be changed.


### SSL services support

Allow SSL services support to encrypt traffic to your upstream apps that require HTTPS.
{: shortdesc}

Previous {{site.data.keyword.openshiftlong_notm}} Ingress resource [annotation](/docs/openshift?topic=openshift-ingress_annotation#ssl-services):

```
ingress.bluemix.net/ssl-services: ssl-service=app1 ssl-secret=app1-ssl-secret proxy-ssl-verify-depth=5 proxy-ssl-name=proxy-ssl-name=mydomain.com
```
{: screen}

Kubernetes Ingress resource [annotations](https://kubernetes.github.io/ingress-nginx/user-guide/nginx-configuration/annotations/#backend-certificate-authentication){:external}:

```
nginx.ingress.kubernetes.io/proxy-ssl-secret: app1-ssl-secret
nginx.ingress.kubernetes.io/proxy-ssl-verify-depth: 5
nginx.ingress.kubernetes.io/proxy-ssl-name: proxy-ssl-name=mydomain.com
nginx.ingress.kubernetes.io/proxy-ssl-verify: true
```
{: screen}


### TCP ports

Access an app via a non-standard TCP port.
{: shortdesc}

Previous {{site.data.keyword.openshiftlong_notm}} Ingress resource [annotation](/docs/openshift?topic=openshift-ingress_annotation#tcp-ports):

```
ingress.bluemix.net/tcp-ports: "serviceName=app1 ingressPort=8080 servicePort=9000"
```
{: screen}

Kubernetes `ibm-ingress-deploy-config` configmap [field](#comm-customize-deploy):

```
tcp-services-configmap=<configMap>
```
{: screen}

For the requirements of the `tcp-services-configmap`, see [this blog](https://kubernetes.github.io/ingress-nginx/user-guide/exposing-tcp-udp-services/){:external}.


### Upstream fail timeout

Set the amount of time during which the ALB can attempt to connect to the server.
{: shortdesc}

Previous {{site.data.keyword.openshiftlong_notm}} Ingress resource [annotation](/docs/openshift?topic=openshift-ingress_annotation#upstream-fail-timeout):

```
ingress.bluemix.net/upstream-fail-timeout: "serviceName=app1 fail-timeout=10s"
```
{: screen}

Kubernetes Ingress field: Currently, no configuration option for the Kubernetes Ingress exists.


### Upstream keepalive requests

Set the maximum number of requests that can be served through one keepalive connection.
{: shortdesc}

Previous {{site.data.keyword.openshiftlong_notm}} Ingress resource [annotation](/docs/openshift?topic=openshift-ingress_annotation#keepalive-requests):

```
ingress.bluemix.net/keepalive-requests: "serviceName=app1 requests=32”
```
{: screen}

Kubernetes `ibm-k8s-controller-config` configmap [field](https://kubernetes.github.io/ingress-nginx/user-guide/nginx-configuration/configmap/#upstream-keepalive-requests){:external}:

```
upstream-keepalive-requests: 32
```
{: screen}


### Upstream keepalive timeout

Set the maximum time that a keepalive connection stays open between the ALB proxy server and your app's upstream server.
{: shortdesc}

Previous {{site.data.keyword.openshiftlong_notm}} Ingress resource [annotation](/docs/openshift?topic=openshift-ingress_annotation#upstream-keepalive-timeout):

```
ingress.bluemix.net/keepalive-timeout: "serviceName=app1 timeout=32s"
```
{: screen}

Kubernetes `ibm-k8s-controller-config` configmap [field](https://kubernetes.github.io/ingress-nginx/user-guide/nginx-configuration/configmap/#upstream-keepalive-timeout){:external}:

```
upstream-keepalive-timeout: 32
```
{: screen}


### Upstream max fails

Set the maximum number of unsuccessful attempts to communicate with the server.
{: shortdesc}

Previous {{site.data.keyword.openshiftlong_notm}} Ingress resource [annotation](/docs/openshift?topic=openshift-ingress_annotation#upstream-max-fails):

```
ingress.bluemix.net/upstream-max-fails: "serviceName=app1 max-fails=2"
```
{: screen}

Kubernetes Ingress field: Currently, no configuration option for the Kubernetes Ingress exists.

<br />


## Customizing the ALB deployment
{: #comm-customize-deploy}

Customize the deployment for ALBs that run the Kubernetes Ingress image by creating an `ibm-ingress-deploy-config` configmap.
{: shortdesc}

The following options are specific to ALBs that run the Kubernetes Ingress image. To modify default Ingress settings that apply to ALBs regardless of image type, such as to enable source IP preservation or configure SSL protocols, see [Modifying default Ingress settings](/docs/openshift?topic=openshift-ingress_annotation).
{: tip}

1. Get the names of the services that expose each ALB.
  ```
  oc get svc -n kube-system | grep alb
  ```
  {: pre}

2. Create a configmap to customize the Ingress deployment.

  1. Create a YAML file for an `ibm-ingress-deploy-config` configmap. For each ALB ID, you can specify the following options.
     ```yaml
     apiVersion: v1
     kind: ConfigMap
     metadata:
       name: ibm-ingress-deploy-config
       namespace: kube-system
     data:
       <alb1-id>: '{"enableSslPassthrough":"<true|false>", "httpPort":"<port>", "httpsPort":"<port>", "ingressClass":"<class>", "replicas":<number_of_replicas>}'
       <alb2-id>: '{"enableSslPassthrough":"<true|false>", "httpPort":"<port>", "httpsPort":"<port>", "ingressClass":"<class>", "replicas":<number_of_replicas>}'
       ...
     ```
     {: screen}

     <table summary="The columns are read from left to right. The first column has the parameter of the configmap. The second column describes the parameter.">
     <caption>Understanding this configmap's components</caption>
     <col width="25%">
     <thead>
     <th>Parameter</th>
     <th>Description</th>
     </thead>
     <tbody>
     <tr><td>`enableSslPassthrough`</td><td>Enable SSL passthrough for the ALB. The TLS connection is not terminated and passes through untouched.</td></tr>
     <tr><td>`httpPort`, `httpsPort`</td><td>Expose non-default ports for the Ingress ALB by adding the HTTP or HTTPS ports that you want to open.</td></tr>
     <tr><td>`ingressClass`</td><td>If you specified a class other than `public-iks-k8s-nginx` or `private-iks-k8s-nginx` in your Ingress resource, specify the class.</td></tr>
     <tr><td>`replicas`</td><td>By default, each ALB has 2 replicas. Scale up your ALB processing capabilities by increasing the number of ALB pods.</td></tr>
     </tbody>
     </table>

  2. Create the `ibm-ingress-deploy-config` configmap in your cluster.
    ```
    oc create -f ibm-ingress-deploy-config.yaml
    ```
    {: pre}

  3. To pick up the changes, update your ALBs.
    ```
    ibmcloud oc ingress alb update -c <cluster_name_or_ID>
    ```
    {: pre}

3. If you specified non-standard HTTP or HTTPS ports, you must open the ports on each ALB service.
  1. For each ALB service that you found in step 1, edit the YAML file.
    ```
    oc edit svc -n kube-system <alb_svc_name>
    ```
    {: pre}

  2. In the `spec.ports` section, add the ports that you want to open.
      * By default, ports 80 and 443 are open. If you want to keep 80 and 443 open, do not remove them from this file. Any port that is not specified is closed.
      * Do not specify a `nodePort`. After you add the port and apply the changes, a `nodePort` is automatically assigned.

      Example:
      ```
      ...
        ports:
        - name: port-80
          nodePort: 32632
          port: 80
          protocol: TCP
          targetPort: 80
        - name: port-443
          nodePort: 32293
          port: 443
          protocol: TCP
          targetPort: 443
        - name: <new_port>
          port: <port>
          protocol: TCP
          targetPort: <port>
      ...
      ```
      {: screen}

  3. Save and close the file. Your changes are applied automatically.

<br />


## Adding {{site.data.keyword.appid_short_notm}} authentication to apps
{: #app-id}

Enforce authentication for your apps by configuring Ingress with [{{site.data.keyword.appid_full_notm}}](https://cloud.ibm.com/catalog/services/app-id){: external}.
{: shortdesc}

1. Choose an existing or create a new {{site.data.keyword.appid_short_notm}} instance.
  * To use an existing instance, ensure that the service instance name contains only alphanumeric characters or hyphens (`-`), and doesn't contain spaces. To change the name, select **Rename service** from the more options menu on your service instance details page.
  * To provision a [new {{site.data.keyword.appid_short_notm}} instance](https://cloud.ibm.com/catalog/services/app-id):
      1. Replace the auto-filled **Service name** with your own unique name for the service instance. The service instance name must contain only alphanumeric characters or hyphens (`-`), and can't contain spaces.
      2. Choose the same region that your cluster is deployed in.
      3. Click **Create**.

2. Add redirect URLs for your app. A redirect URL is the callback endpoint of your app. To prevent phishing attacks, {{site.data.keyword.appid_full_notm}} validates the request URL against the allowlist of redirect URLs.
  1. In the {{site.data.keyword.appid_short_notm}} management console, navigate to **Manage Authentication**.
  2. In the **Identity providers** tab, make sure that you have an Identity Provider selected. If no Identity Provider is selected, the user will not be authenticated but will be issued an access token for anonymous access to the app.
  3. In the **Authentication settings** tab, add redirect URLs for your app in the format `http://<hostname>/oauth2-<App_ID_service_instance_name>/callback` or `https://<hostname>/oauth2-<App_ID_service_instance_name>/callback`.

    {{site.data.keyword.appid_full_notm}} offers a logout function: If `/logout` exists in your {{site.data.keyword.appid_full_notm}} path, cookies are removed and the user is sent back to the login page. To use this function, you must append `/sign_out` to your domain in the format `http://<hostname>/oauth2-<App_ID_service_instance_name>/sign_out` or `https://<hostname>/oauth2-<App_ID_service_instance_name>/sign_out` and include this URL in the redirect URLs list.
    {: note}

3. Bind the {{site.data.keyword.appid_short_notm}} service instance to your cluster. The command creates a service key for the service instance, or you can include the `--key` flag to use existing service key credentials. Be sure to bind the service instance to the same project that your Ingress resources exist in.
  ```
  ibmcloud oc cluster service bind --cluster <cluster_name_or_ID> --namespace <project> --service <App_ID_service_instance_name> [--key <service_instance_key>]
  ```
  {: pre}
  When the service is successfully bound to your cluster, a cluster secret is created that holds the credentials of your service instance. Example CLI output:
  ```
  ibmcloud oc cluster service bind --cluster mycluster --namespace myproject --service appid1
  Binding service instance to namespace...
  OK
  Namespace:    myproject
  Secret name:  binding-<service_instance_name>
  ```
  {: screen}

4. Enable the ALB OAuth Proxy add-on in your cluster.
    1. Enable the `alb-oauth-proxy` add-on.
      ```
      ibmcloud oc cluster addon enable alb-oauth-proxy --cluster <cluster_name_or_ID>
      ```
      {: pre}
    2. Verify that the ALB OAuth Proxy add-on has a status of `Addon Ready`.
      ```
      ibmcloud oc cluster addon ls --cluster <cluster_name_or_ID>
      ```
      {: pre}

5. In the Ingress resources for apps where you want to add {{site.data.keyword.appid_short_notm}} authentication, add the following annotations to the `metadata.annotations` section.
  1. Using your {{site.data.keyword.appid_short_notm}} service instance name, add the following `auth-url` annotation.
     ```yaml
     ...
     annotations:
       nginx.ingress.kubernetes.io/auth-url: https://$host/oauth2-<App_ID_service_instance_name>/auth
     ...
     ```
     {: codeblock}

  2. Choose which tokens to send in the `Authorization` header to your app. For more information about ID and access tokens, see the [{{site.data.keyword.appid_short_notm}} documentation](/docs/appid?topic=appid-tokens){: external}.
     * To send only the `ID Token`, add the `nginx.ingress.kubernetes.io/auth-response-headers: Authorization` annotation.
     * To send only the `Access Token`, add the following information to the `access_by_lua_block{}` in the `configuration-snippet` annotation.
       ```yaml
       ...
       annotations:
         nginx.ingress.kubernetes.io/configuration-snippet: |
           auth_request_set $access_token $upstream_http_x_auth_request_access_token;
           access_by_lua_block {
             if ngx.var.access_token ~= "" then
               ngx.req.set_header("Authorization", "Bearer " .. ngx.var.access_token)
             end
           }
       ...
       ```
       {: codeblock}
     * To send the `Access Token` and the `ID Token`, add the following information to the `access_by_lua_block{}` in the `configuration-snippet` annotation.
       ```yaml
       ...
       annotations:
         nginx.ingress.kubernetes.io/configuration-snippet: |
           auth_request_set $access_token $upstream_http_x_auth_request_access_token;
           auth_request_set $id_token $upstream_http_authorization;
           access_by_lua_block {
             if ngx.var.id_token ~= "" and ngx.var.access_token ~= "" then
               ngx.req.set_header("Authorization", "Bearer " .. ngx.var.access_token .. " " .. ngx.var.id_token:match("%s*Bearer%s*(.*)"))
             end
           }
       ...
       ```
       {: codeblock}
  3. Optional: If your app accepts web requests instead of API requests, add the `nginx.ingress.kubernetes.io/auth-signin: https://$host/oauth2-<App_ID_service_instance_name>/start?rd=$escaped_request_uri` annotation.

6. Re-apply your Ingress resources to enforce {{site.data.keyword.appid_short_notm}} authentication.
  ```
  oc create -f <app_ingress_resource>.yaml -n project
  ```
  {: pre}

7. Verify that {{site.data.keyword.appid_short_notm}} authentication is enforced for your apps.
  * If your apps accept web requests: Access your app's URL in a web browser. If {{site.data.keyword.appid_short_notm}} is correctly applied, you are redirected to an {{site.data.keyword.appid_short_notm}} authentication log-in page.
  * If your apps accept API requests: Use an API key to curl your app's URL. If {{site.data.keyword.appid_short_notm}} is correctly applied, your app accepts the request and returns a `200` response. If you curl your apps without an API key in the request, or if the API key is not accepted by {{site.data.keyword.appid_short_notm}}, then your app rejects the request.

8. Optional: You can customize the default behavior of the OAuth proxy add-on by creating a custom resource.
    1. Check the default values for the OAuth proxy settings.
        ```
        oc describe crd oauthproxyconfigs.cloud.ibm.com
        ```
        {: pre}
    2. Create a YAML file that specifies values for the OAuth proxy settings that you want to change. If you do not want to change a setting, you can comment it out of the following YAML file. For more information about each field, see the field descriptions in the output of the previous command.
       ```
       apiVersion: cloud.ibm.com/v1
       kind: OAuthProxyConfig
       metadata:
         name: oauth2-<App_ID_service_instance_name>
         namespace: <project>
       spec:
         auth-logging: <true|false>
         auth-logging-format: "<format>"
         cookie-domain:
           - <onedomain.com>
           - <twodomain.com>
         cookie-expire: 168h0m0s
         cookie-samesite: "none"
         email-domain: <[one@domain.com,two@domain.com]>
         pass-access-token: <true|false>
         request-logging: <true|false>
         request-logging-format: "<format>"
         scope: "<scope>"
         set-xauthrequest: <true|false>
         set-authorization-header: <true|false>
         standard-logging: <true|false>
         standard-logging-format: "<format>"
         tls-secret-name: "<secret_name>"
       ```
       {: codeblock}
    3. Apply the custom resource to your add-on. Your changes are applied automatically.
      ```
      oc apply -f oauth2-proxy-app-id.yaml
      ```
      {: pre}




## Preserving the source IP address
{: #preserve_source_ip}

By default, the source IP address of the client request is not preserved. When a client request to your app is sent to your cluster, the request is routed to a pod for the load balancer service that exposes the ALB. If no app pod exists on the same worker node as the load balancer service pod, the load balancer forwards the request to an app pod on a different worker node. The source IP address of the package is changed to the public IP address of the worker node where the app pod runs.
{: shortdesc}

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


### Enabling log buffering and flush timeout
{: #access-log}

By default, the Ingress ALB logs each request as it arrives. If you have an environment that is heavily used, logging each request as it arrives can greatly increase disk I/O utilization. To avoid continuous disk I/O, you can enable log buffering and flush timeout for the ALB by editing the `ibm-k8s-controller-config` Ingress configmap. When buffering is enabled, instead of performing a separate write operation for each log entry, the ALB buffers a series of entries and writes them to the file together in a single operation.
{: shortdesc}

1. Edit the `ibm-k8s-controller-config` configmap.
    ```
    oc edit cm ibm-k8s-controller-config -n kube-system
    ```
    {: pre}

2. Set the threshold for when the ALB should write buffered contents to the log.
    * Buffer size: Add the `buffer` field and set it to how much log memory can be held in the buffer before the ALB writes the buffered contents to the log file. For example, if the default value of `100KB` is used, the ALB writes buffer contents to the log file every time the buffer reaches 100KB of log content.
    * Time interval: Add the `flush` field and set it to how often the ALB should write to the log file. For example, if the default value of `5m` is used, the ALB writes buffer contents to the log file once every 5 minutes.
    * Time interval or buffer size: When both `flush` and `buffer` are set, the ALB writes buffer content to the log file based on whichever threshold parameter is met first.

    ```yaml
    apiVersion: v1
    kind: ConfigMap
    data:
      access-log-params: "buffer=100KB, flush=5m"
    metadata:
      name: ibm-k8s-controller-config
      ...
    ```
    {: codeblock}

3. Save and close the configuration file. The changes are applied to your ALBs automatically.

4. Verify that the logs for an ALB now contain buffered content that is written according to the memory size or time interval you set.
   ```
   oc logs -n kube-system <ALB_ID> -c nginx-ingress
   ```
   {: pre}

### Changing the number or duration of keepalive connections
{: #keepalive_time}

Keepalive connections can have a major impact on performance by reducing the CPU and network usage that is needed to open and close connections. To optimize the performance of your ALBs, you can change the maximum number of keepalive connections between the ALB and the client and how long the keepalive connections can last.
{: shortdesc}

1. Edit the `ibm-k8s-controller-config` configmap.
    ```
    oc edit cm ibm-k8s-controller-config -n kube-system
    ```
    {: pre}

2. Change the values of `keep-alive-requests` and `keep-alive`.
    * `keep-alive-requests`: The number of keepalive client connections that can stay open to the Ingress ALB. The default is `4096`.
    * `keep-alive`: The timeout, in seconds, during which the keepalive client connection stays open to the Ingress ALB. The default is `8`.
   ```yaml
   apiVersion: v1
   data:
     keep-alive-requests: 4096
     keep-alive: 8
   kind: ConfigMap
   metadata:
     name: ibm-k8s-controller-config
     ...
   ```
   {: codeblock}

3. Save and close the configuration file. The changes are applied to your ALBs automatically.

4. Verify that the configmap changes were applied.
   ```
   oc get cm ibm-cloud-provider-ingress-cm -n kube-system -o yaml
   ```
   {: pre}

### Changing the number of simultaneous connections or worker processes
{: #worker_processes_connections}

Change the default setting for how many simultaneous connections the NGINX worker processes for one ALB can handle or how many worker processes can occur for one ALB.
{: shortdesc}

Each ALB has NGINX worker processes that process the client connections and communicate with the upstream servers for the apps that the ALB exposes. By changing the number of worker processes per ALB or how many connections the worker processes can handle, you can manage the maximum number of clients that an ALB can handle. Calculate your maximum client connections with the following formula: `maximum clients = worker_processes * worker_connections`.

* The `max-worker-connections` field sets the maximum number of simultaneous connections that can be handled by the NGINX worker processes for one ALB. The default value is `16384`. Note that the `max-worker-connections` parameter includes all connections that the ALB proxies, not just connections with clients. Additionally, the actual number of simultaneous connections cannot exceed the [limit on the maximum number of open files](#max-worker-files), which is set by the `max-worker-open-files` parameter. If you set the value of `max-worker-connections` to `0`, the value for `max-worker-open-files` is used instead.
* The `worker-processes` field sets the maximum number of NGINX worker processes for one ALB. The default value is `"auto"`, which indicates that the number of worker processes matches the number of cores on the worker node where the ALB is deployed. You can change this value to a number if your worker processes must perform high levels of I/0 operations.

1. Edit the `ibm-k8s-controller-config` configmap.
    ```
    oc edit cm ibm-k8s-controller-config -n kube-system
    ```
    {: pre}

2. Change the value of `max-worker-connections` or `worker-processes`.

   ```yaml
   apiVersion: v1
   data:
     max-worker-connections: 16384
     worker-processes: "auto"
   kind: ConfigMap
   metadata:
     name: ibm-k8s-controller-config
     ...
   ```
   {: codeblock}

3. Save the configuration file. The changes are applied to your ALBs automatically.

4. Verify that the configmap changes were applied.
   ```
   oc get cm ibm-k8s-controller-config -n kube-system -o yaml
   ```
   {: pre}

### Changing the number of open files for worker processes
{: #max-worker-files}

Change the default maximum for the number of files that can be opened by each worker node process for an ALB.
{: shortdesc}

Each ALB has NGINX worker processes that process the client connections and communicate with the upstream servers for the apps that the ALB exposes. If your worker processes are hitting the maximum number of files that can be opened, you might see a `Too many open files` error in your NGINX logs. By default, the `max-worker-open-files` parameter is set to `0`, which indicates that the value from the following formula is used: `system limit of maximum open files / worker-processes - 1024`. If you change the value to another integer, the formula no longer applies.

1. Edit the `ibm-k8s-controller-config` configmap.
    ```
    oc edit cm ibm-k8s-controller-config -n kube-system
    ```
    {: pre}

2. Change the value of `max-worker-open-files`.

   ```yaml
   apiVersion: v1
   data:
     max-worker-open-files: 0
   kind: ConfigMap
   metadata:
     name: ibm-k8s-controller-config
     ...
   ```
   {: codeblock}

3. Save the configuration file. The changes are applied to your ALBs automatically.

4. Verify that the configmap changes were applied.
   ```
   oc get cm ibm-k8s-controller-config -n kube-system -o yaml
   ```
   {: pre}




