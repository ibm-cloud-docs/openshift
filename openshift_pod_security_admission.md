---

copyright:
  years: 2022, 2022
lastupdated: "2022-09-19"

keywords: openshift, security, admission, pod security, configure pod security

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}

# Pod security admission
{: #pod_security_admission}

{{site.data.keyword.openshiftlong_notm}} versions 4.11 and later include support for Kubernetes pod security admission. Pod security admission implements the Kuberntes pod security standards that restrict the behavior of pods, providing warning messages and `kube-apiserver` audit events for pods that violate the pod security profile policy configured for the relevant namespace.
{: shortdesc}

For more information, see [Pod Security Admission](https://kubernetes.io/docs/concepts/security/pod-security-admission/){: external} and [Pod Security Standards](https://kubernetes.io/docs/concepts/security/pod-security-standards/){: external} in the Kubernetes documentation. 

## Understanding security profiles
{: #pod_security_profiles}

The Kubernetes pod security standards define the following three profiles.
{: shortdesc}

Privileged
:   The default pod security configuration globally enforces the `privileged` Kubernetes pod security profile, which is unrestricted and allows for known privilege escalations, and generates warnings and audit events based on the policies set by the `restricted` profile.

Baseline
:   The `baseline` profile is a restrictive profile which prevents known privilege escalations. Allows the default (minimally specified) Pod configuration.

Restricted
:   The `restricted` profile is heavily restricted and follows the current pod hardening best practices. 

For more information about pod security profiles, see [Profile details](https://kubernetes.io/docs/concepts/security/pod-security-standards/){: external} in the Kubernetes documentation.

## Configuring pod security admission
{: #pod_security_configure}

You can configure the pod security behavior at the namespace level with predefined pod security labels. For confiuration steps, see [Controlling pod security admission synchronization](https://docs.openshift.com/container-platform/4.11/authentication/understanding-and-managing-pod-security-admission.html#security-context-constraints-psa-opting_understanding-and-managing-pod-security-admission) in the Red Hat OpenShift documentation. 

For more information about configuring `apiserver` logs for {{site.data.keyword.openshiftshort}}, see [Kubernetes API server audit logs](/docs/openshift?topic=openshift-health-audit#audit-api-server).
{: tip}

Pod security admission provides the ability to enforce, warn, and generate audit events for pods that would violate the security profiles.
In OpenShift 4.11 the default configuration enforces the privileged profile, while generating warnings and audit events based on the `restricted` profile. This behavior can be controlled at the namespace level through the use of predefined pod security labels on namespaces. When the Pod security profiles are enforced, you might see warnings such as the following example.

```sh
`Warning: would violate PodSecurity "restricted:latest": host namespaces (hostNetwork=true, hostPID=true), privileged (container "container-00" must not set securityContext.privileged=true), allowPrivilegeEscalation != false (container "container-00" must set securityContext.allowPrivilegeEscalation=false), unrestricted capabilities (container "container-00" must set securityContext.capabilities.drop=["ALL"]), restricted volume types (volume "host" uses restricted volume type "hostPath"), runAsNonRoot != true (pod or container "container-00" must set securityContext.runAsNonRoot=true), runAsUser=0 (container "container-00" must not set runAsUser=0), seccompProfile (pod or container "container-00" must set securityContext.seccompProfile.type to "RuntimeDefault" or "Localhost")`
```
{: screen}

In this example, the pod is still created and can run as long the service account is authorized to a `SecurityContextConstraint`. The warning indicates that changes to the `securityContext` of the pod and container are required for the pod to run under the specified pod security profile, such as setting `allowPrivilegeEscalation=false` or that a pod security profile that allows those capabilites must be used.

{{site.data.keyword.redhat_openshift_notm}} also includes a controller that applies namespace labels based on the SCC permissions of the service accounts in a given namespace. Both pod security admission and SCCs are applied. You can use primarily SCCs and let the pod security admission synchronization controller adjust the pod security label on the namespace. Or, you can use primarily pod security profiles with a namespace role binding that allows all serviceaccounts in the namespace to use an equivalent (or more privileged) SCC. Do not define role bindings or cluster role bindings that apply globally such as all authorized users or all service accounts in all namespaces as these can affect {{site.data.keyword.redhat_openshift_notm}} components that expect to be running under a particular SCC.

### Understanding {{site.data.keyword.openshiftlong_notm}} pod security namespace labeling
{: #pod-sec-namespace-labels}

{{site.data.keyword.openshiftlong_notm}} adds the `privileged` Pod Security labels to the following namespaces.

- `kube-system`
- `ibm-system`
- `calico-system`
- `tigera-operator`

Do not remove or change the labels for these namespaces. These namesapces are in addition to the `openshift-*` namespaces labeled by Red Hat.
{: important}

### Additional resources
{: #pod-sec-additional-resources}

- [Understanding and managing pod security admission](https://docs.openshift.com/container-platform/4.11/authentication/understanding-and-managing-pod-security-admission.html){: external}.
- [Pod Security Admission in {{site.data.keyword.redhat_openshift_notm}} 4.11](https://cloud.redhat.com/blog/pod-security-admission-in-openshift-4.11){: external}.
- [Kubernetes API server audit logs](/docs/openshift?topic=openshift-health-audit#audit-api-server) describes how to configure API server audit logs in the {{site.data.keyword.openshiftlong_notm}} service.


