---

copyright: 
  years: 2022, 2024
lastupdated: "2024-03-14"


keywords: openshift, webhooks, admission control, 

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}



# Accessing the cluster master with admission controllers and webhooks
{: #access_webhooks}

Admission controllers intercept authorized API requests from various Kubernetes resources before the requests reach the API server that runs in your {{site.data.keyword.openshiftlong_notm}} cluster master. Mutating admission webhooks might modify the request, and validating admission webhooks check the request. If either webhook rejects a request, the entire request fails. Advanced features, whether built-in or added on, often require admission controllers as a security precaution and to control what requests are sent to the API server. For more information, see [Using Admission Controllers](https://kubernetes.io/docs/reference/access-authn-authz/admission-controllers/){: external} and [Dynamic Admission Control](https://kubernetes.io/docs/reference/access-authn-authz/extensible-admission-controllers/){: external} in the Kubernetes documentation.

## Can I create my own admission controllers?
{: #access_webhooks_create_controllers}

Yes, see the [Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/extensible-admission-controllers/){: external} and [{{site.data.keyword.redhat_openshift_notm}}](https://docs.openshift.com/container-platform/4.14/architecture/admission-plug-ins.html){: external} documentation for more information. 

As noted in the Kubernetes documentation, you can use admission controllers for operations that are otherwise handled by the control plane. As such, take great caution when you configure a custom admission controller. You are responsible for any changes that happen in your cluster because of a custom admission controller.
{: important}


## What are the best practices for using webhooks?
{: #webhook-best-practice}

Keep in mind the following best practices and considerations when you configure a webhook.

- Create [replica pods](/docs/openshift?topic=openshift-app#replicaset) for the webhook so that if one pod goes down, the webhook can still process requests from your resources. Spread the replica pods across zones, if possible.
- Set an appropriate `failurePolicy` option, such as whether your webhook fails or ignores connection failures or timeouts. You might set the `failurePolicy` to `Ignore` if you want your webhook to ignore connection errors an timeouts. Note that this does not change how the `apiserver` behaves if the webhook rejects a request.
- Review the `timeoutSeconds` interval. Older webhooks that use the `v1beta1.admissionregistration.k8s.io` API have a default timeout of 30 seconds. The `v1` API uses a default of 10 seconds. If the webhook failure policy is Ignore and the current `timeoutSeconds` is 30, consider reducing the timeout to 10 seconds. For OpenShift clusters, control plane components often have their own timeout of 13 seconds.
- Set appropriate CPU and memory [resource requests and limits](/docs/openshift?topic=openshift-app#resourcereq) for your webhook.
- Add [liveness and readiness probes](/docs/openshift?topic=openshift-app#probe) to help make sure your webhook container is running and ready to serve requests.
- Set pod [anti-affinity scheduling rules](/docs/openshift?topic=openshift-app#affinity) to prefer that your webhook pods run on different worker nodes and zones when possible. You might use [pod topology](https://kubernetes.io/docs/concepts/scheduling-eviction/topology-spread-constraints/){: external} instead. However, avoid [taints](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/){: external} or forced affinity that might restrict where the webhook pods can be scheduled.
- [Set pod priority](/docs/openshift?topic=openshift-pod_priority) to `system-cluster-critical` for the webhook pods so that other pods can't take resources from your webhook pods.
- Scope your webhook to the appropriate project. Avoid webhooks that process resources that run in system-critical projects that are set up in your cluster by default, such as `kube-system`, `ibm-system`, `ibm-operators`, `calico-system`, `tigera-operator` and `openshift-*` projects.
- Review the `namespaceSelector` option. You can add labels to the certain critical namespaces, such as `kube-system`, so the webhook is not called for these cases. This setup is called an "opt out" style configuration. Or, you can configure the `namespaceSelector` option so the webhook is called only for namespaces that have a specific label. This setup is called an "opt in" configuration. Depending on the purpose of the webhook, it might be important that the webhook be called for all namespaces. Review the `namespaceSelector` configuration options in the [Kubernetes documentation](https://kubernetes.io/docs/reference/access-authn-authz/extensible-admission-controllers/#matching-requests-namespaceselector){: external} and adjust your webhook configuration.
- Make sure that the worker nodes in your cluster are [the correct size for running your webhook applications](/docs/openshift?topic=openshift-strategy). For example, if your pods request more CPU or memory than the worker node can provide, the pods are not scheduled.


## What other types of apps use admission controllers?
{: #access_webhooks-app-use-controllers}

Many cluster add-ons, plug-ins, and other third-party extensions use admission controllers. Some common ones include:
- [Portieris](/docs/openshift?topic=openshift-images#portieris-image-sec)



### Setting up admission controller webhooks
{: #configure-webhooks-122}

In cluster versions 4.14 and later, Konnectivity replaced the OpenVPN solution. If you have cluster version 4.14 and later, and your webhook uses the ClusterIP, you must update your webhook to use a Kubernetes service instead.
{: shortdesc}

You can configure a webhook by referencing the webhook app as a Kubernetes service, or by referencing the webhook app as an IP address or publicly registered DNS name.

    Example configuration for referencing the webhook app as a Kubernetes service


    ```yaml
    clientConfig:
       caBundle: #CA_BUNDLE_BASE64#
       service:
          name: admission-webhook
          namespace: default
          path: /validate
          port: 443
    ```
    {: codeblock}

    Example configuration for referencing the webhook app as an IP address or publicly registered DNS name


    ```yaml
    clientConfig:
       caBundle: #CA_BUNDLE_BASE64#
       url: https://#WEBHOOK_URL#:443/validate
    ```
    {: codeblock}

Note the following limitations for referencing the webhook app as an IP address or DNS name:

- If the URL is a DNS, then this DNS must be a publicly registered DNS name. Private DNS configurations are not supported.
- If the URL is an external IP address, which means the webhook service is outside of the cluster, the control plane network is used to connect to the service. The control plane must be able to reach the IP address. If, for example, the IP address is from an on-premises network and the control plane can't reach the IP address, the webhook service does not work.
- If the URL is a cluster IP address, which means the webhook service is inside of the cluster, the Kubernetes API needs to connect to cluster network. If you have cluster version 1.21 and later, and your webhook uses the cluster IP address, you must update your webhook to use a Kubernetes service instead.




## I need help with a broken webhook. What can I do?
{: #access_webhooks-help}

For help troubleshooting webhooks, see [Debugging webhooks](/docs/openshift?topic=openshift-ts-webhook-debug) or [Cluster can't update because of broken webhook](/docs/openshift?topic=openshift-webhooks_update).





