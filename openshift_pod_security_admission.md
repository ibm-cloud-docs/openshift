---

copyright:
  years: 2022, 2022
lastupdated: "2022-09-07"

keywords: openshift, security, admission, pod security, configure pod security

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}

# Pod security admission
{: #pod_security_admission}

{{site.data.keyword.openshiftlong_notm}} versions 4.11 and later include support for Kubernetes pod security admission. Pod security admission implements the Kuberntes pod security standards that restrict the behavior of pods, providing warning messages and `kube-apiserver` audit events for pods that violate the pod security profile policy configured for the relevant namespace.
{: shortdesc}

For more information, see [Pod Security Admission](https://kubernetes.io/docs/concepts/security/pod-security-admission/){: external} and [Pod Security Standards](https://kubernetes.io/docs/concepts/security/pod-security-standards/){: external} in the Kubernetes documentation. 

## Configuring pod security admission
{: #pod_security_profiles}

The default pod security configuration globally enforces the `privileged` Kubernetes pod security profile, which is unrestricted and allows for known privilege escalations, and generates warnings and audit events based on the policies set by the `restricted` profile. The `restricted` profile is heavily restricted and follows the current pod hardening best practices. For more information about pod security profiles, see [Profile details](https://kubernetes.io/docs/concepts/security/pod-security-standards/){: external} in the Kubernetes documentation.
{: shortdesc}

## Configuring pod security admission
{: #pod_security_configure}

You can configure the pod security behavior at the namespace level with predefined pod security labels. For confiuration steps, see [Controlling pod security admission synchronization](https://docs.openshift.com/container-platform/4.11/authentication/understanding-and-managing-pod-security-admission.html#security-context-constraints-psa-opting_understanding-and-managing-pod-security-admission) in the Red Hat OpenShift documentation. 

For more information about configuring `apiserver` logs for {{site.data.keyword.openshiftshort}}, see [Kubernetes API server audit logs](/docs/openshift?topic=openshift-health-audit#audit-api-server).
{: tip}


