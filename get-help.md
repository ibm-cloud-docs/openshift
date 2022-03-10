---

copyright: 
  years: 2014, 2022
lastupdated: "2022-03-10"

keywords: red hat openshift, openshift container platform, red hat, red hat cluster, openshift, containers, clusters

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}


# Getting help
{: #get-help}

Still having issues with your cluster? Review different ways to get help and support for your {{site.data.keyword.openshiftlong_notm}} clusters. For any questions or feedback, post in Slack.
{: shortdesc}

## General ways to resolve cluster issues
{: #help-general}
{: support}

1. Keep your cluster environment up to date.
    * Check monthly for available security and operating system patches to [update your worker nodes](/docs/containers?topic=containers-update#worker_node).
    * [Update your cluster](/docs/containers?topic=containers-update#master) to the latest default version for [{{site.data.keyword.redhat_openshift_notm}}](/docs/openshift?topic=openshift-openshift_versions).
2. Make sure that your command line tools are up to date.
    * In the command line, you are notified when updates to the `ibmcloud` CLI and plug-ins are available. Be sure to keep your CLI up-to-date so that you can use all available commands and options.
    * Make sure that [your `oc` CLI](/docs/openshift?topic=openshift-openshift-cli#cli_oc) client matches the same Kubernetes version as your cluster server. [Kubernetes does not support](https://kubernetes.io/releases/version-skew-policy/){: external} `oc` client versions that are 2 or more versions apart from the server version (n +/- 2).



## Reviewing issues and status
{: #help-cloud-status}

1. To see whether {{site.data.keyword.cloud_notm}} is available, [check the {{site.data.keyword.cloud_notm}} status page](https://cloud.ibm.com/status?selected=status){: external}.
2. Filter for the **Kubernetes Service** component.
3. Review the [limitations and known issues documentation](/docs/containers?topic=containers-limitations).
4. For issues in open source projects that are used by {{site.data.keyword.cloud_notm}}, see the [IBM Open Source and Third Party policy](https://www.ibm.com/support/pages/node/737271){: external}. For example, you might check the {{site.data.keyword.redhat_openshift_notm}} [Bugzilla](https://bugzilla.redhat.com/){: external}.



## Feedback and questions
{: #feedback-qs}

1. Post in the {{site.data.keyword.containershort}} Slack.
    * If you are an external user, post in the [#openshift](https://ibm-cloud-success.slack.com/messages/CKCJLJCH4){: external} channel. 
2. Review forums such as {{site.data.keyword.redhat_openshift_notm}} help or Stack Overflow to see whether other users ran into the same issue. When you use the forums to ask a question, tag your question so that it is seen by the {{site.data.keyword.cloud_notm}} development teams.
    * If you have technical questions about developing or deploying clusters or apps with {{site.data.keyword.openshiftlong_notm}}, post your question on [Stack Overflow](https://stackoverflow.com/questions/tagged/ibm-cloud+containers){: external} and tag your question with `ibm-cloud`, `openshift`,  and `containers`.
    * See [Getting help](/docs/get-support?topic=get-support-using-avatar) for more details about using the forums.



## Contacting support
{: #help-support}

Before you open a support case, gather relevant information about your cluster environment.
{: shortdesc}

1. Get your cluster details.

    ```sh
    ibmcloud oc cluster get -c <cluster_name_or_ID>
    ```
    {: pre}

2. If your issue involves worker nodes, get the worker node details.

    1. List all worker nodes in the cluster, and note the **ID** of any worker nodes with an unhealthy **State** or **Status**.
    
        ```sh
        ibmcloud oc worker ls -c <cluster_name_or_ID>
        ```
        {: pre}

    2. Get the details of the unhealthy worker node.
    
        ```sh
        ibmcloud oc worker get -w <worker_ID> -c <cluster_name_or_ID>
        ```
        {: pre}

3. For issues with resources within your cluster such as pods or services, log in to the cluster and use the Kubernetes API to get more information about them.

    You can also use the [{{site.data.keyword.containerlong_notm}} Diagnostics and Debug Tool](/docs/containers?topic=containers-debug-tool) to gather and export pertinent information to share with IBM Support.
    {: tip}

4. Contact IBM Support by [opening a case](https://cloud.ibm.com/unifiedsupport/cases/form){: external}. To learn about opening an IBM support case, or about support levels and case severities, see [Contacting support](/docs/get-support?topic=get-support-using-avatar).

5. For the **Problem type**, search for or select **{{site.data.keyword.openshiftlong_notm}}**.

6. For the **Case details**, provide a descriptive title and include the details that you previously gathered. From the **Resources**, you can also select the cluster that the issue is related to.




