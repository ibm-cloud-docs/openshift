---

copyright: 
  years: 2022, 2023
lastupdated: "2023-07-26"

keywords: webhooks, admission control, ,openshift

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}



# Accessing the cluster master with admission controllers and webhooks
{: #access_webhooks}

Admission controllers intercept authorized API requests from various Kubernetes resources before the requests reach the API server that runs in your {{site.data.keyword.openshiftlong_notm}} cluster master. Mutating admission webhooks might modify the request, and validating admission webhooks check the request. If either webhook rejects a request, the entire request fails. Advanced features, whether built-in or added on, often require admission controllers as a security precaution and to control what requests are sent to the API server. For more information, see [Using Admission Controllers](https://kubernetes.io/docs/reference/access-authn-authz/admission-controllers/){: external} and [Dynamic Admission Control](https://kubernetes.io/docs/reference/access-authn-authz/extensible-admission-controllers/){: external} in the Kubernetes documentation.

## Can I create my own admission controllers?
{: #access_webhooks_create_controllers}

Yes, see the [Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/extensible-admission-controllers/){: external} and [{{site.data.keyword.redhat_openshift_notm}}](https://docs.openshift.com/container-platform/4.12/architecture/admission-plug-ins.html){: external} documentation for more information. 

As noted in the Kubernetes documentation, you can use admission controllers for operations that are otherwise handled by the control plane. As such, take great caution when you configure a custom admission controller. You are responsible for any changes that happen in your cluster because of a custom admission controller.
{: important}


## What are the best practices for using webhooks?
{: #webhook-best-practice}

Keep in mind the following best practices and considerations when you configure a webhook.

- Create [replica pods](/docs/containers?topic=containers-app#replicaset) for the webhook so that if one pod goes down, the webhook can still process requests from your resources. Spread the replica pods across zones, if possible.
- Set an appropriate `failurePolicy` option, such as whether your webhook fails or ignores connection failures or timeouts. You might set the `failurePolicy` to `Ignore` if you want your webhook to ignore connection errors an timeouts. Note that this does not change how the `apiserver` behaves if the webhook rejects a request.
- Review the `timeoutSeconds` interval. Older webhooks that use the `v1beta1.admissionregistration.k8s.io` API have a default timeout of 30 seconds. The `v1` API uses a default of 10 seconds. If the webhook failure policy is Ignore and the current `timeoutSeconds` is 30, consider reducing the timeout to 10 seconds. For OpenShift clusters, control plane components often have their own timeout of 13 seconds.
- Set appropriate CPU and memory [resource requests and limits](/docs/containers?topic=containers-app#resourcereq) for your webhook.
- Add [liveness and readiness probes](/docs/openshift?topic=openshift-app#probe) to help make sure your webhook container is running and ready to serve requests.
- Set pod [anti-affinity scheduling rules](/docs/openshift?topic=openshift-app#affinity) to prefer that your webhook pods run on different worker nodes and zones when possible. You might use [pod topology](https://kubernetes.io/docs/concepts/scheduling-eviction/topology-spread-constraints/){: external} instead. However, avoid [taints](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/){: external} or forced affinity that might restrict where the webhook pods can be scheduled.
- [Set pod priority](/docs/openshift?topic=openshift-pod_priority) to `system-cluster-critical` for the webhook pods so that other pods can't take resources from your webhook pods.
- Scope your webhook to the appropriate project. Avoid webhooks that process resources that run in system-critical projects that are set up in your cluster by default, such as `kube-system`, `ibm-system`, `ibm-operators`, `calico-system`, `tigera-operator` and `openshift-*` projects.
- Review the `namespaceSelector` option. You can add labels to the certain critical namespaces, such as `kube-system`, so the webhook is not called for these cases. This setup is called an "opt out" style configuration. Or, you can configure the `namespaceSelector` option so the webhook is called only for namespaces that have a specific label. This setup is called an "opt in" configuration. Depending on the purpose of the webhook, it might be important that the webhook be called for all namespaces. Review the `namespaceSelector` configuration options in the [Kubernetes documentation](https://kubernetes.io/docs/reference/access-authn-authz/extensible-admission-controllers/#matching-requests-namespaceselector){: external} and adjust your webhook configuration.
- Make sure that the worker nodes in your cluster are [the correct size for running your webhook applications](/docs/openshift?topic=openshift-strategy#sizing). For example, if your pods request more CPU or memory than the worker node can provide, the pods are not scheduled.


## What other types of apps use admission controllers?
{: #access_webhooks-app-use-controllers}

Many cluster add-ons, plug-ins, and other third-party extensions use admission controllers. Some common ones include:
- [Portieris](/docs/openshift?topic=openshift-images#portieris-image-sec)




## I need help with a broken webhook. What can I do?
{: #access_webhooks-help}

For help troubleshooting webhooks, see [Debugging webhooks](/docs/openshift?topic=openshift-ts-webhook-debug) or [Cluster can't update because of broken webhook](/docs/openshift?topic=openshift-webhooks_update).





