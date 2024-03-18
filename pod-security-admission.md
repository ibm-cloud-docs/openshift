---

copyright: 
  years: 2022, 2024
lastupdated: "2024-03-18"


keywords: openshift, deploy, pod security admission, pod security, security profiles

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}



# Pod security admission
{: #pod-security-admission}

Pod security admission implements the Kubernetes pod security standards that restrict the behavior of pods, providing warning messages and `kube-apiserver` audit events for pods that violate the pod security profile policy configured for the relevant namespace.
{: shortdesc}

{{site.data.keyword.openshiftlong_notm}} version 4.11 and later includes support for Kubernetes pod security admission. For more information, see [Pod Security Admission](https://kubernetes.io/docs/concepts/security/pod-security-admission/){: external} and [Pod Security Standards](https://kubernetes.io/docs/concepts/security/pod-security-standards/){: external} in the Kubernetes documentation.

Pod Security Admission is always enabled for {{site.data.keyword.openshiftlong_notm}} version 4.11 and later. Earlier versions of Kubernetes use [pod security policies](/docs/containers?topic=containers-psp).
{: note}

## Understanding security profiles
{: #pod_security_profiles}

The Kubernetes pod security standards define the following three profiles.
{: shortdesc}

Privileged
:   The default pod security configuration globally enforces the `privileged` Kubernetes pod security profile, which is unrestricted and allows for known privilege escalations, and generates warnings and audit events based on the policies set by the `restricted` profile.

Baseline
:   The `baseline` profile is a restrictive profile that prevents known privilege escalations. Allows the default (minimally specified) Pod configuration.

Restricted
:   The `restricted` profile is heavily restricted and follows the current pod hardening best practices. 

For more information about pod security profiles, see [Profile details](https://kubernetes.io/docs/concepts/security/pod-security-standards/){: external} in the Kubernetes documentation.


Pod Security Admission contains three modes that define what action the control plane takes if a potential violation is detected.

enforce
:   Policy violations cause the pod to be rejected.

audit
:   Policy violations trigger the addition of an audit annotation to the event recorded in the audit log, but are otherwise allowed.

warn
:   Policy violations trigger a user-facing warning, but are otherwise allowed.

As security standards or profiles implementations change to address new features, you can configure Pod Security Admission to use a specific version of the roles. The following versions are supported.

- A Kubernetes major.minor version (for example, `v1.25`)
- `latest`

## What if Pod Security Admission isn't the right choice for me?
{: #what-if-psa}

While Pod Security Admission is always enabled, it can be one of multiple admission controllers. You can configure third-party Kubernetes admission controllers to implement other security policy models that suit your use case.

If you configure Pod Security Admission to enforce, warn, and audit by using the `privileged` profile, then the control plane allows all pods to run. You can then configure other admission controllers to reject them.

You can install a third-party admission controller as long as it doesn't take either of the following actions.
- It doesn't install its own pod security policies (PSPs).
- It doesn't rely on PSPs to enforce parts of the policy.

## Configuring Pod Security admission namespace labels
{: #psa-namespace-labels}

You can define the admission control mode you want to use for pod security in each namespace. Kubernetes defines a set of labels that you can set to define which of the predefined Pod Security Standard profiles you want to use for a namespace. The label you select defines what action the control plane takes if a potential violation is detected.

By default, {{site.data.keyword.openshiftlong_notm}} adds the `privileged` Pod Security labels to the following namespaces. These namespaces are labeled to `enforce`, `audit`, and `warn` by using the `privileged` profile.

- `kube-system` 
- `ibm-system`
- `ibm-operators`
- `calico-system` 
- `tigera-operator` 


Do not remove or change the labels for these namespaces or any of the `openshift-*` namespaces.
{: important}

A namespace can be labeled to set the pod security profile for any or all the Pod Security Admission `modes`. 

For example, you can label a namespace to enforce the `privileged` profile in addition to using `warn` or `audit` by using the `baseline` profile.

This label allows administrators and application developers to dry-run applications by looking for only warnings and audit records against the `baseline` profile without rejecting pods. Then, you can make necessary changes to your workloads before changing the enforce mode to `baseline`.

The Pod Security Admission namespace labels are of the form `pod-security.kubernetes.io/<MODE>: <LEVEL>` and `pod-security.kubernetes.io/<MODE>-version: <VERSION>`.

- `pod-security.kubernetes.io/enforce`
- `pod-security.kubernetes.io/enforce-version`
- `pod-security.kubernetes.io/audit`
- `pod-security.kubernetes.io/audit-version`
- `pod-security.kubernetes.io/warn`
- `pod-security.kubernetes.io/warn-version`

To label a namespace to enforce the `privileged` profile and generate warnings and audit events for violations of the `baseline` profile, use the following labels.

- `pod-security.kubernetes.io/enforce: privileged`
- `pod-security.kubernetes.io/enforce-version: latest`
- `pod-security.kubernetes.io/audit: baseline`
- `pod-security.kubernetes.io/audit-version: latest`
- `pod-security.kubernetes.io/warn: baseline`
- `pod-security.kubernetes.io/warn-version: latest`




## Default Pod Security Admission plug-in configuration
{: #psa-plugin-config-default}

{{site.data.keyword.openshiftlong_notm}} uses the following `PodSecurityConfiguration` by default.

```yaml
apiVersion: pod-security.admission.config.k8s.io/v1
kind: PodSecurityConfiguration
defaults:
  enforce: "privileged"
  enforce-version: "latest"
  audit: "privileged"
  audit-version: "latest"
  warn: "privileged"
  warn-version: "latest"
exemptions:
  usernames: []
  runtimeClasses: []
  namespaces: []
```
{: codeblock}








## Configuring pod security admission
{: #pod-security-configure}


You can configure the pod security behavior at the namespace level with predefined pod security labels. For more information about configuration, see [Controlling pod security admission synchronization](https://docs.openshift.com/container-platform/4.11/authentication/understanding-and-managing-pod-security-admission.html#security-context-constraints-psa-opting_understanding-and-managing-pod-security-admission){: external} in the Red Hat OpenShift documentation. Note that the steps vary for each cluster version, so make sure you are viewing the steps for the correct version. 

For more information about configuring `apiserver` logs for {{site.data.keyword.openshiftshort}}, see [Kubernetes API server audit logs](/docs/openshift?topic=openshift-health-audit#audit-api-server).
{: tip}

Pod security admission provides the ability to enforce, warn, and generate audit events for pods that violate the security profiles.
In OpenShift 4.11, the default configuration enforces the privileged profile, while also generating warnings and audit events based on the `restricted` profile. This behavior can be controlled at the namespace level through the use of predefined pod security labels on namespaces. When the Pod security profiles are enforced, you might see warnings such as the following example.

```sh
`Warning: would violate PodSecurity "restricted:latest": host namespaces (hostNetwork=true, hostPID=true), privileged (container "container-00" must not set securityContext.privileged=true), allowPrivilegeEscalation != false (container "container-00" must set securityContext.allowPrivilegeEscalation=false), unrestricted capabilities (container "container-00" must set securityContext.capabilities.drop=["ALL"]), restricted volume types (volume "host" uses restricted volume type "hostPath"), runAsNonRoot != true (pod or container "container-00" must set securityContext.runAsNonRoot=true), runAsUser=0 (container "container-00" must not set runAsUser=0), seccompProfile (pod or container "container-00" must set securityContext.seccompProfile.type to "RuntimeDefault" or "Localhost")`
```
{: screen}

In this example, the pod is still created and can run as long the service account is authorized to a `SecurityContextConstraint` profile. The warning indicates that changes to the `securityContext` profile of the pod and container are required for the pod to run under the specified pod security profile, such as setting the `allowPrivilegeEscalation=false` option or that a pod security profile that allows those capabilities must be used.

{{site.data.keyword.redhat_openshift_notm}} also includes a controller that applies namespace labels based on the SCC permissions of the service accounts in a given namespace. Both pod security admission and SCCs are applied. You can use primarily SCCs and use the pod security admission synchronization controller to adjust the pod security label on the namespace. Or, you can use primarily pod security profiles with a namespace role binding that allows all service accounts in the namespace to use an equivalent (or more privileged) SCC. Do not define role bindings or cluster role bindings that apply globally, such as all authorized users or all service accounts in all namespaces as these bindings can affect {{site.data.keyword.redhat_openshift_notm}} components that expect to be running under a particular SCC.

## Additional resources
{: #pod-sec-additional-resources}

- [Understanding and managing pod security admission](https://docs.openshift.com/container-platform/4.11/authentication/understanding-and-managing-pod-security-admission.html){: external}.
- [Pod Security Admission in {{site.data.keyword.redhat_openshift_notm}} 4.11](https://www.redhat.com/blog/pod-security-admission-in-openshift-4.11){: external}.
- [Kubernetes API server audit logs](/docs/openshift?topic=openshift-health-audit#audit-api-server) describes how to configure API server audit logs in the {{site.data.keyword.openshiftlong_notm}} service.



