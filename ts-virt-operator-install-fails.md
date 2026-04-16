---

copyright:
  years: 2026, 2026

lastupdated: "2026-04-16"

keywords: openshift virtualization, operator install, openshift-cnv, catalogsource, subscription

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why does the OpenShift Virtualization Operator installation fail?
{: #ts-virt-operator-install-fails}
{: troubleshoot}
{: support}

[Virtual Private Cloud]{: tag-vpc}
[4.17 and later]{: tag-red}
[Bare metal worker nodes only]{: tag-warm-gray}
[RHCOS only]{: tag-magenta}

You try to install the OpenShift Virtualization Operator, but the installation does not complete successfully.
{: tsSymptoms}

The cluster is not fully prepared for the operator installation. Common causes include disabled default catalog sources, outbound traffic protection that blocks required access, or a failed subscription in the `openshift-cnv` namespace.
{: tsCauses}

To resolve the issue,
{: tsResolve}

 verify the catalog sources, outbound traffic protection setting, and operator subscription.

1. Verify that the default catalog sources are enabled.
   ```sh
   oc get catalogsource -n openshift-marketplace
   ```
   {: pre}

2. If catalog sources are not listed, enable them.
   ```sh
   oc patch operatorhub cluster --type json -p '[{"op": "add", "path": "/spec/disableAllDefaultSources", "value": false}]'
   ```
   {: pre}

3. Check whether outbound traffic protection is enabled.
   ```sh
   ibmcloud oc vpc outbound-traffic-protection get -c <cluster_name>
   ```
   {: pre}

4. If outbound traffic protection is enabled, disable it.
   ```sh
   ibmcloud oc vpc outbound-traffic-protection disable -c <cluster_name>
   ```
   {: pre}

5. Review the operator subscription status.
   ```sh
   oc get subscription -n openshift-cnv
   oc describe subscription hco-operatorhub -n openshift-cnv
   ```
   {: pre}

6. Review the operator logs for errors.
   ```sh
   oc logs -n openshift-cnv -l app=kubevirt-hyperconverged-operator
   ```
   {: pre}

7. If the operator still does not install, review [Installing the OpenShift Virtualization Operator](/docs/openshift?topic=openshift-oc-virtualization) and collect the command output before you contact [{{site.data.keyword.cloud_notm}} support](/docs/get-support).
