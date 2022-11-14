---

copyright: 
  years: 2022, 2022
lastupdated: "2022-11-14"

keywords: openshift, esssmg

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}


# Why does the Ingress status show an ESSSMG error?
{: #ts-ingress-esssmg}
{: troubleshoot}
{: support}

Supported infrastructure providers
:   Classic
:   VPC
:   {{site.data.keyword.satelliteshort}}

When you check the status of your cluster's Ingress components by running the `ibmcloud oc ingress status-report get` command, you see an error similar to the following example.
{: tsSymptoms}

```sh
Could not access Secrets Manager instance group, verify default group is accessible and exists within instance (ESSSMG).
```
{: screen}

{{site.data.keyword.openshiftlong_notm}} is unable to access the secret group that was registered with the cluster to upload the default Ingress certificates.
{: tsCauses}

Review your service-to-service authorization policies and verify that communication between {{site.data.keyword.openshiftlong_notm}} and {{site.data.keyword.secrets-manager_short}} is enabled.
{: tsResolve}

1. [Follow the steps to ensure there is a service-to-service authorization policy](/docs/openshift?topic=openshift-secrets-mgr#secrets-mgr_setup_s2s) configured to enable communication between {{site.data.keyword.openshiftlong_notm}} and {{site.data.keyword.secrets-manager_short}}.

1. If the policy exists, verify that the secret group registered with the cluster exists in the instance.
    - To view the instance registration details for your cluster run the **`ibmcloud oc ingress instance ls`** command. 
    - To view and modify the secret groups available in your instance, see [Organizing your secrets](/docs/secrets-manager?topic=secrets-manager-secret-groups).
    - To update the secret group for your cluster, run the **`ibmcloud oc ingress instance default set`** command and specify the `--secret-group` option.

1. If the issue persists, contact support. Open a [support case](/docs/get-support?topic=get-support-using-avatar). In the case details, be sure to include any relevant log files, error messages, or command outputs.



