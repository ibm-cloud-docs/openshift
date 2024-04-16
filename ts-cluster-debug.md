---

copyright: 
  years: 2014, 2024
lastupdated: "2024-04-15"


keywords: openshift, {{site.data.keyword.openshiftlong_notm}}, troubleshooting apps, app debugging, application troublshooting in clusters

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}


# Troubleshooting apps in {{site.data.keyword.openshiftlong_notm}}
{: #debug_clusters}
{: troubleshoot}
{: support}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [{{site.data.keyword.satelliteshort}}]{: tag-satellite}

The following steps help you troubleshoot application problems within your cluster and find the root causes for application errors or problems.
{: shortdesc}


## Review the status of {{site.data.keyword.cloud_notm}}
{: #troubleshooting-environments}
{: step}

1. To see whether {{site.data.keyword.cloud_notm}} is available, [check the {{site.data.keyword.cloud_notm}} status page](https://cloud.ibm.com/status?selected=status){: external}.
2. Filter for the **Kubernetes Service** component.
3. Review the [limitations and known issues documentation](/docs/openshift?topic=openshift-limitations).
4. For issues in open source projects that are used by {{site.data.keyword.cloud_notm}}, see the [IBM Open Source and Third Party policy](https://www.ibm.com/support/pages/node/737271){: external}. For example, you might check the {{site.data.keyword.redhat_openshift_notm}} [Bugzilla](https://bugzilla.redhat.com/){: external}.


## Get your cluster state and status and review the common issues
{: #ts-2}
{: step}

1. List your cluster and find the `State` of the cluster.

    ```sh
    ibmcloud oc cluster ls
    ```
    {: pre}

1. Review the `State` of your cluster. If your cluster is in a **Critical**, **Delete failed**, or **Warning** state, or is stuck in the **Pending** state for a long time. For more information, see [cluster states](/docs/openshift?topic=openshift-cluster-states-reference). 

1. Review the state of each worker node. For more information, see [worker node states](/docs/openshift?topic=openshift-worker-node-state-reference).
    ```sh
    ibmcloud oc worker ls -c CLUSTER
    ```
    {: pre}

1. Review the [common worker node issues](/docs/openshift?topic=openshift-common_worker_nodes_issues). 

1. Review the [debugging guide for worker node issues](/docs/openshift?topic=openshift-debug_worker_nodes).

## Gather details and document the problem
{: #ts-3}
{: step}

When documenting details about the problem, be as specific as possible. For example, "Our app occasionally gets 502 Gateway errors when trying to retrieve transaction logs" is not helpful because it is not specific. Make sure you narrow down the problem as much as possible before documenting it. When documenting the problem, try to include the following.

Environment architecture
:   Make sure you have documented your environment architecture so that you understand the components involved. For more information, see [Documenting your environment architecture](/docs/openshift?topic=openshift-document-environment).

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

## Running tests to rule in or rule out each component
{: #ts-4}
{: step}

1. Try to recreate the problem outside of the full app flow. This might involve the following.
    - Using `curl` either on a separate system or in a test pod in a cluster to connect to the backend endpoint or service to rule in or out that the client might be the source of the problem.
    - Trying to connect to a known endpoint like `www.ibm.com` from the client or from a test pod in the cluster. If the known endpoint works consistently, but the real app endpoint doesn't, that helps to narrow down the problem.
2. Try to recreate the problem in a test environment using a test cluster.
    - If you **can't** recreate the problem in a test cluster, then you can focus on the differences between the test cluster and the real cluster as the possible sources of the problem.
    - If you **can** recreate it in a test cluster, then it is likely not a problem with the cluster itself. Also, you have an environment where you can test to further narrow down the problem without impacting your production environment.

## Gathering more data
{: #ts-5}
{: step}

Once you know the app flow, the specific error you are seeing, and where that error is coming from, you can gather more detailed data from the components involved. This might include the following logs.

- Pod and process logs on the impacted components.
- Cluster node logs such as `syslog` or `/var/log/messages`. For {{site.data.keyword.openshiftlong_notm}}, you can either use the Diagnostics and Debug Tool, or you can get `syslog` and other logs directly from the nodes.
    - [Debug tool](/docs/openshift?topic=openshift-debug-tool).
    - [Cluster node access](/docs/openshift?topic=openshift-cs_ssh_worker)
- Packet trace information. Running `tcpdump` is a common way to get packet trace information. For more information, see [Troubleshooting Load Balancers in {{site.data.keyword.cloud_notm}} Kubernetes Service by using `tcpdump`](https://www.ibm.com/blog/troubleshooting-load-balancers-in-ibm-cloud-kubernetes-service-using-tcpdump/){: external}.

## Reach out in Slack or review user forums for similar issues
{: #ts-6}
{: step}

1. Post in the {{site.data.keyword.containershort}} Slack.
    * If you are an external user, post in the [#openshift](https://ibm-cloud-success.slack.com/messages/CKCJLJCH4){: external}{: external} channel. 
1. Review forums such as {{site.data.keyword.redhat_openshift_notm}} help or Stack Overflow to see whether other users ran into the same issue. When you use the forums to ask a question, tag your question so that it is seen by the {{site.data.keyword.cloud_notm}} development teams.
    * If you have technical questions about developing or deploying clusters or apps with {{site.data.keyword.openshiftlong_notm}}, post your question on [Stack Overflow](https://stackoverflow.com/questions/tagged/ibm-cloud+containers){: external} and tag your question with `ibm-cloud`, `openshift`,  and `containers`.
    * See [Getting help](/docs/get-support?topic=get-support-using-avatar) for more details about using the forums.


## Next steps
{: #advanced-ts-next}

If the issue persists, contact support. Open a [support case](/docs/get-support?topic=get-support-using-avatar). In the case details, be sure to include any relevant log files, error messages, or command outputs.






