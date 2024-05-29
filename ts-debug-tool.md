---

copyright: 
  years: 2014, 2024
lastupdated: "2024-05-29"


keywords: kubernetes, openshift

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}





# Running tests with the Diagnostics and Debug Tool
{: #debug-tool}
{: troubleshoot}
{: support}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf}

While you troubleshoot, you can use the {{site.data.keyword.containerlong_notm}} Diagnostics and Debug Tool to run tests and gather pertinent information from your cluster.
{: shortdesc}


Only one version of the Diagnostics and Debug Tool is available at a time. This version is available for all clusters versions. The tool is updated approximately once a month to address vulnerabilities. These updates are applied automatically. When a new version is pushed to a production region, all installed instances in that region are updated.
{: note}


## Enable and run the Diagnostics and Debug Tool add-on
{: #debug-tool-enable}

1. In the [{{site.data.keyword.redhat_openshift_notm}} clusters console](https://cloud.ibm.com/kubernetes/clusters?platformType=openshift){: external}, click the name of the cluster where you want to install the debug tool add-on.


1. On the **Diagnostics and Debug Tool** card, click **Install**.

1. In the dialog box, click **Install**. Note that it can take a few minutes for the add-on to be installed. To resolve some common issues that you might encounter during the add-on deployment, see [Reviewing add-on state and statuses](/docs/openshift?topic=openshift-debug_addons).

1. On the Diagnostics and Debug Tool card, click **Dashboard**.

1. In the debug tool dashboard, select individual tests or a group of tests to run. Some tests check for potential warnings, errors, or issues, and some tests only gather information that you can reference while you troubleshoot. For more information about the function of each test, click the information icon next to the test's name.

1. Click **Run**.

1. Check the results of each test.
    * If any test fails, click the information icon next to the test's name for information about how to resolve the issue.
    * You can also use the results of tests to gather information, such as complete YAMLs, that can help you debug your cluster in the following sections.




