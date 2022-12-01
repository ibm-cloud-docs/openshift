---

copyright: 
  years: 2014, 2022
lastupdated: "2022-12-01"

keywords: openshift

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

Supported infrastructure providers
:   Classic
:   VPC

## Enabling the Diagnostics and Debug Tool add-on
{: #debug-tool-enable}

1. In the [{{site.data.keyword.redhat_openshift_notm}} clusters console](https://cloud.ibm.com/kubernetes/clusters?platformType=openshift){: external}, click the name of the cluster where you want to install the debug tool add-on.

2. Click the **Add-ons** tab.

3. On the Diagnostics and Debug Tool card, click **Install**.

4. In the dialog box, click **Install**. Note that it can take a few minutes for the add-on to be installed. To resolve some common issues that you might encounter during the add-on deployment, see [Reviewing add-on state and statuses](/docs/openshift?topic=openshift-debug_addons).

5. On the Diagnostics and Debug Tool card, click **Dashboard**.

6. In the debug tool dashboard, select individual tests or a group of tests to run. Some tests check for potential warnings, errors, or issues, and some tests only gather information that you can reference while you troubleshoot. For more information about the function of each test, click the information icon next to the test's name.

7. Click **Run**.

8. Check the results of each test.
    * If any test fails, click the information icon next to the test's name in the left column for information about how to resolve the issue.
    * You can also use the results of tests to gather information, such as complete YAMLs, that can help you debug your cluster in the following sections.




