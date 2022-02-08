---

copyright:
  years: 2014, 2022
lastupdated: "2022-02-08"

keywords: openshift

subcollection: openshift

---


{{site.data.keyword.attribute-definition-list}}


# Using the compliance operator
{: #compliance-operator}

With the compliance operator, you can check whether the worker nodes in your cluster meet the set of criteria in the profile that is tailored to {{site.data.keyword.openshiftlong}}. For more information, see the [{{site.data.keyword.openshiftshort}} documentation](https://docs.openshift.com/container-platform/4.8/security/compliance_operator/compliance-operator-understanding.html){: external}.
{: shortdesc}

![Version 4 icon.](images/icon-version-43.png) The compliance operator is available for clusters that run {{site.data.keyword.openshiftlong_notm}} version 4.6 or later.
{: note}

Looking for the CIS Kubernetes benchmark? See [Running the worker node CIS Kubernetes benchmark](/docs/openshift?topic=openshift-cis-benchmark#cis-worker-test).
{: tip}

## Installing the compliance operator with the tailored profile
{: #comp-op-install}

Install the compliance operator with the tailored profile for worker nodes in your {{site.data.keyword.openshiftlong_notm}} cluster.
{: shortdesc}

Before you begin, make sure that you have the **Manager** [service access role](/docs/openshift?topic=openshift-access_reference#service) to the cluster.

1. [Access your {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-access_cluster).
2. Install the compliance operator.

    The following substeps use the {{site.data.keyword.openshiftshort}} web console, but for other installation methods, see the [open source project documentation](https://github.com/openshift/compliance-operator/blob/master/doc/tutorials/workshop/content/exercises/02-installation.md){: external}. For example, you might have a private network-only cluster that does not permit access to the {{site.data.keyword.openshiftshort}} web console. Keep in mind that your worker nodes in a private cluster must have access to the `quay.io` registry to pull the compliance operator image.
    {: note}

    1. From the {{site.data.keyword.openshiftshort}} web console **Administrator** perspective in the menu bar, click **Operators > OperatorHub**.
    2. Filter for and click the `Compliance Operator`.
    3. Click **Install**.
    4. On the Operator Installation page, confirm the default configurations to install the operator with automatic updates for your cluster version and create an `openshift-compliance` namespace. Then, click **Install**.
    5. Wait for the operator to be ready to use.
3. Create a scan setting in the `openshift-compliance` namespace by using the configuration file from the [`kube-samples` GitHub repository](https://github.com/IBM-Cloud/kube-samples/tree/master/roks-compliance-operator){: external}. The scan setting defines how often and which objects the compliance operator scans. By default, the scan runs hourly on worker nodes. You can modify the scan settings, such as changing the frequency of the scan by updating the `schedule: "0 */1 * * *"` field.
    ```sh
    oc apply -n openshift-compliance -f https://raw.githubusercontent.com/IBM-Cloud/kube-samples/master/roks-compliance-operator/scansetting.yaml
    ```
    {: pre}

4. Create the tailored profile for {{site.data.keyword.openshiftlong_notm}} by using the configuration file from the [`kube-samples` GitHub repository](https://github.com/IBM-Cloud/kube-samples/tree/master/roks-compliance-operator){: external}. The target profile sets and disables certain rules based on their relevance to the managed offering, and explains the rationale for the rules.
    ```sh
    oc apply -n openshift-compliance -f https://raw.githubusercontent.com/IBM-Cloud/kube-samples/master/roks-compliance-operator/tailoredprofile.yaml
    ```
    {: pre}

5. To begin the compliance scans, create a binding for the scan setting by using the configuration file from the [`kube-samples` GitHub repository](https://github.com/IBM-Cloud/kube-samples/tree/master/roks-compliance-operator){: external}.
    ```sh
    oc apply -n openshift-compliance -f https://raw.githubusercontent.com/IBM-Cloud/kube-samples/master/roks-compliance-operator/scansettingbinding.yaml
    ```
    {: pre}

6. Wait for the scan pods to reach a **Completed** status on each worker node. By default, the scans run hourly.
    ```sh
    oc get pods -n openshift-compliance
    ```
    {: pre}

    Example output with completed scan pods
    ```sh
    NAME                                             READY   STATUS      RESTARTS   AGE
    aggregator-pod-roks-cis-node-worker              0/1     Completed   0          53s
    compliance-operator-68965986bb-f4k5m             1/1     Running     0          17m
    ocp4-openshift-compliance-pp-6f854dcb9d-zh5tv    1/1     Running     0          16m
    rhcos4-openshift-compliance-pp-f9db847bb-d5ttq   1/1     Running     0          16m
    roks-cis-node-worker-10.184.xx.111-pod           0/2     Completed   0          2m58s
    roks-cis-node-worker-10.184.xx.222-pod           0/2     Completed   0          2m58s
    roks-cis-node-worker-10.184.xx.333-pod           0/2     Completed   0          2m57s
    roks-cis-node-worker-10.184.xx.444-pod           0/2     Completed   0          2m57s
    ```
    {: screen}

7. Check the compliance scan results.
    ```sh
    oc -n openshift-compliance get compliancecheckresults
    ```
    {: pre}

    Example results
    ```sh
    NAME                                                  STATUS   SEVERITY
    roks-cis-node-worker-etcd-unique-ca                   SKIP     medium
    roks-cis-node-worker-file-groupowner-cni-conf         PASS     medium
    roks-cis-node-worker-file-groupowner-kubelet-conf     PASS     medium
    roks-cis-node-worker-file-owner-cni-conf              PASS     medium
    ...
    ```
    {: screen}

8. Interpret the scan **STATUS** results. For more details, review the upstream project documentation in the [What's next?](#comp-op-next) section.
    - **PASS**: Your worker nodes passed the check and no action is required.
    - **SKIP**: The benchmark check is not applicable to worker nodes. For more information, check the `rationale` for the check in the `roks-cis-node` tailored profile.
    - **FAIL**: Your worker nodes did not pass the check. An application or other resource in your cluster possibly modified the default system configuration. Consider the following actions:
        - Review the details in the `roks-cis-node` tailored profile for the check that fails. Then, review the resources that you deployed in the cluster to see if any might have modified the default system configuration for the check.
        - Reload the worker node and see if the check passes on the next scan.


## What's next?
{: #comp-op-next}

Now, you set up the compliance operator to scan your worker nodes against the {{site.data.keyword.openshiftlong_notm}} tailored profile. You can leave the scan running to make sure that changes to your cluster don't introduce compliance risks. You might also add your own profiles to scan for other compliance items that are unique to your business requirements. To clean up the resources that you created, you can uninstall the operator delete the `openshift-compliance` namespace.
{: external}

For more ways to use the compliance operator, review the OpenShift Container Platform documentation, such as the following resources.
- [Understanding the compliance operator](https://docs.openshift.com/container-platform/4.8/security/compliance_operator/compliance-operator-understanding.html){: external} documentation set.
- [Self-paced compliance operator workshop in GitHub](https://github.com/openshift/compliance-operator/tree/master/doc/tutorials){: external}.
- How does the compliance operator work? [Part 1](https://cloud.redhat.com/blog/how-does-compliance-operator-work-for-openshift-part-1){: external} and [Part 2](https://cloud.redhat.com/blog/how-does-compliance-operator-work-for-openshift-part-2){: external} blogs.






