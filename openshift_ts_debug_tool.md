---

copyright:
  years: 2014, 2021
lastupdated: "2021-09-10"

keywords: openshift, roks, rhoks, rhos

subcollection: openshift
content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}} 

# Running tests with the Diagnostics and Debug Tool
{: #debug-tool}
{: troubleshoot}
{: support}

While you troubleshoot, you can use the {{site.data.keyword.containerlong_notm}} Diagnostics and Debug Tool to run tests and gather pertinent information from your cluster.
{: shortdesc}

**Infrastructure provider**:
* <img src="images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Classic
* <img src="images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> VPC

## Prerequisites
{: #debug-tool-prereqs}

If you previously installed the debug tool by using Helm, first uninstall the `ibmcloud-iks-debug` Helm chart.
1. Find the installation name of your Helm chart.
    ```
    helm list -n <project> | grep ibmcloud-iks-debug
    ```
    {: pre}

    Example output:
    ```
    <helm_chart_name> 1 Thu Sep 13 16:41:44 2019 DEPLOYED ibmcloud-iks-debug-1.0.0 default
    ```
    {: screen}

2. Uninstall the debug tool installation by deleting the Helm chart.
    ```
    helm uninstall <helm_chart_name> -n <project>
    ```
    {: pre}

3. Verify that the debug tool pods are removed. When the uninstallation is complete, no pods are returned by the following command.
    ```
    oc get pod --all-namespaces | grep ibmcloud-iks-debug
    ```
    {: pre}

## Enabling the Diagnostics and Debug Tool add-on
{: #debug-tool-enable}

1. In the [{{site.data.keyword.openshiftshort}} clusters console](https://cloud.ibm.com/kubernetes/clusters?platformType=openshift){: external}, click the name of the cluster where you want to install the debug tool add-on.

2. Click the **Add-ons** tab.

3. On the Diagnostics and Debug Tool card, click **Install**.

4. In the dialog box, click **Install**. Note that it can take a few minutes for the add-on to be installed. To resolve some common issues that you might encounter during the add-on deployment, see [Reviewing add-on state and statuses](/docs/containers?topic=containers-debug_addons).

5. On the Diagnostics and Debug Tool card, click **Dashboard**.

6. In the debug tool dashboard, select individual tests or a group of tests to run. Some tests check for potential warnings, errors, or issues, and some tests only gather information that you can reference while you troubleshoot. For more information about the function of each test, click the information icon next to the test's name.

7. Click **Run**.

8. Check the results of each test.
    * If any test fails, click the information icon next to the test's name in the left column for information about how to resolve the issue.
    * You can also use the results of tests to gather information, such as complete YAMLs, that can help you debug your cluster in the following sections.


