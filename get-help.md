---

copyright: 
  years: 2014, 2024
lastupdated: "2024-03-27"


keywords: openshift, {{site.data.keyword.openshiftlong_notm}}, support, get help

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}





# Getting help and support
{: #get-help}

Still having issues with your cluster? Review different ways to get help and support for your {{site.data.keyword.openshiftlong_notm}} clusters. For any questions or feedback, post in Slack.
{: shortdesc}

## Best practices
{: #help-general}
{: support}

Keep your cluster environment up to date.
:   Check monthly for available security and operating system patches to [update your worker nodes](/docs/openshift?topic=openshift-update#worker_node).
:   [Update your cluster](/docs/openshift?topic=openshift-update#master) to the latest default version for [{{site.data.keyword.redhat_openshift_notm}}](/docs/openshift?topic=openshift-openshift_versions).

Make sure that your command line tools are up to date.
:   In the command line, you are notified when updates to the `ibmcloud` CLI and plug-ins are available. Be sure to keep your CLI up-to-date so that you can use all available commands and options.
:   Make sure that [your `oc` CLI](/docs/openshift?topic=openshift-cli-install) client matches the same Kubernetes version as your cluster server. [Kubernetes does not support](https://kubernetes.io/releases/version-skew-policy/){: external} `oc` client versions that are 2 or more versions apart from the server version (n +/- 2).

[Document your environment architectrure](/docs/openshift?topic=openshift-document-environment).
:   Keeping up-to-date documentation and diagrams can help when debugging issues.



## Step 1: Review the status of {{site.data.keyword.cloud_notm}}
{: #help-cloud-status}

1. To see whether {{site.data.keyword.cloud_notm}} is available, [check the {{site.data.keyword.cloud_notm}} status page](https://cloud.ibm.com/status?selected=status){: external}.
2. Filter for the **Kubernetes Service** component.
3. Review the [limitations and known issues documentation](/docs/openshift?topic=openshift-limitations).
4. For issues in open source projects that are used by {{site.data.keyword.cloud_notm}}, see the [IBM Open Source and Third Party policy](https://www.ibm.com/support/pages/node/737271){: external}. For example, you might check the {{site.data.keyword.redhat_openshift_notm}} [Bugzilla](https://bugzilla.redhat.com/){: external}.



## Step 2: Gather details and document the problem
{: #ts-app-debug-gather}

When documenting details about the problem, be as specific as possible. For example, "Our app occasionally gets 502 Gateway errors when trying to retrieve transaction logs" is not helpful because it is not specific. Make sure you narrow down the problem as much as possible before documenting it. When documenting the problem, try to include the following.

Error messages and component details.
:   Provide the full error message and include details about which component is producing the error. For example, "All three app pods in clusterID ABCDEF occasionally fail on HTTPS calls to GET /transaction-logs from the global load balancer with the error `HTTP 502 Gateway Error: Web server received an invalid response while acting as a gateway or proxy server...`".

Source IP, destination IP, port, and protocol of the connection.
:   For example, "All three app pods in Kubernetes cluster with clusterID ABCDEF. Occasionally, HTTPS calls fail when trying to GET /transaction-logs to the GLB with the error The source pod IP is `172.22.5.10` and the destination IP is `150.40.40.35` port 433. The protocol is HTTPS. Other pods also use this IP address as do the other two GLB IPs `150.40.40.55` and `150.40.40.75`".

Start date, time, and frequency of the problem.
:   Review the following message examples.
    - "This problem affects approximately 2% of all connection attempts."
    - "This problem only occurs between 19:00 and 21:00 UTC, and during those times affects approximately 5% of all connection attempts."
    - "This problem occurs when connecting from pod ID `XYZ`. The problem began on 10/25/2023 at approximately 05:30 UTC"

Troubleshooting actions that you've already taken.
:   Document what has been tried so far and the results of those attempts to help further narrow down the problem.

## Step 3: Running tests to rule in or rule out each component
{: #ts-app-debug-narrow-1}

1. Try to recreate the problem outside of the full app flow. This might involve the following.
    - Using `curl` either on a separate system or in a test pod in a cluster to connect to the backend endpoint or service to rule in or out that the client might be the source of the problem.
    - Trying to connect to a known endpoint like `www.ibm.com` from the client or from a test pod in the cluster. If the known endpoint works consistently, but the real app endpoint doesn't, that helps to narrow down the problem.
2. Try to recreate the problem in a test environment using a test cluster.
    - If you **can't** recreate the problem in a test cluster, then you can focus on the differences between the test cluster and the real cluster as the possible sources of the problem.
    - If you **can** recreate it in a test cluster, then it is likely not a problem with the cluster itself. Also, you have an environment where you can test to further narrow down the problem without impacting your production environment.

## Step 4: Gathering more data
{: #ts-app-debug-gather-again}

Once you know the app flow, the specific error you are seeing, and where that error is coming from, you can gather more detailed data from the components involved. This might include the following logs.

- Pod and process logs on the impacted components.
- Cluster node logs such as `syslog` or `/var/log/messages`. For {{site.data.keyword.openshiftlong_notm}}, you can either use the Diagnostics and Debug Tool, or you can get `syslog` and other logs directly from the nodes.
    - [Debug tool](/docs/openshift?topic=openshift-debug-tool).
    - [Cluster node access](/docs/openshift?topic=openshift-cs_ssh_worker)
- Packet trace information. Running `tcpdump` is a common way to get packet trace information. For more information, see [Troubleshooting Load Balancers in {{site.data.keyword.cloud_notm}} Kubernetes Service by using `tcpdump`](https://www.ibm.com/blog/troubleshooting-load-balancers-in-ibm-cloud-kubernetes-service-using-tcpdump/){: external}.

## Step 4: Reach out in Slack or review user forums for similar issues
{: #feedback-qs}

1. Post in the {{site.data.keyword.containershort}} Slack.
    * If you are an external user, post in the [#openshift](https://ibm-cloud-success.slack.com/messages/CKCJLJCH4){: external}{: external} channel. 
1. Review forums such as {{site.data.keyword.redhat_openshift_notm}} help or Stack Overflow to see whether other users ran into the same issue. When you use the forums to ask a question, tag your question so that it is seen by the {{site.data.keyword.cloud_notm}} development teams.
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

    You can also use the [{{site.data.keyword.containerlong_notm}} Diagnostics and Debug Tool](/docs/openshift?topic=openshift-debug-tool) to gather and export pertinent information to share with IBM Support.
    {: tip}

4. Contact IBM Support by [opening a case](https://cloud.ibm.com/unifiedsupport/cases/form){: external}. To learn about opening an IBM support case, or about support levels and case severities, see [Contacting support](/docs/get-support?topic=get-support-using-avatar).

5. For the **Problem type**, search for or select {{site.data.keyword.openshiftlong_notm}}.

6. For the **Case details**, provide a descriptive title and include the details that you previously gathered. From the **Resources**, you can also select the cluster that the issue is related to.

7. Be as specific as possible and include and architecture diagrams or supplemental materials that you think you could help IBM Support troubleshoot the issue.









