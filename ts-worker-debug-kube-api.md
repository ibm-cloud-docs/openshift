---

copyright: 
  years: 2014, 2022
lastupdated: "2022-01-31"

keywords: openshift

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}


# Debugging worker nodes with Kubernetes API
{: #debug-kube-nodes}
{: support}


If you have access to the cluster, you can debug the worker nodes by using the Kubernetes API on the `Node` resource.
{: shortdesc}

Before you begin, make sure that you have the **Manager** service access role in all namespaces for the cluster, which corresponds to the `cluster-admin` RBAC role.

1. [Access your {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-access_cluster).
2. List the worker nodes in your cluster and note the **NAME** of the worker nodes that are not in a `Ready` **STATUS**. Note that the **NAME** is the private IP address of the worker node.
    ```sh
    oc get nodes
    ```
    {: pre}

3. Describe the each worker node, and review the `Conditions` section in the output.
    * `Type`: The type of condition that might affect the worker node, such as memory or disk pressure.
    * `LastTransitionTime`: The most recent time that the status was updated. Use this time to identify when the issue with your worker node began, which can help you further troubleshoot the issue.

    ```sh
    oc describe node <name>
    ```
    {: pre}

4. Check the usage of the worker nodes.
    1. In the `Allocated resources` output of the previous command, review the workloads that use the worker node's CPU and memory resources. You might notice that some pods don't set resource limits, and are consuming more resources than you expected. If so, adjust the resource usage of the pods.
    2. Review the percentage of usage of CPU and memory across the worker nodes in your cluster. If the usage is consistently over 80%, [add more worker nodes](/docs/containers?topic=containers-add_workers) to the cluster to support the workloads.
5. Check for custom admission controllers that are installed in your cluster. Admission controllers often block required pods from running, which might make your worker nodes enter a critical state. If you have custom admission controllers, try removing them with `oc delete`. Then, check if the worker node issue resolves.
    ```sh
    kubectl get mutatingwebhookconfigurations --all-namespaces
    ```
    {: pre}

    ```sh
    kubectl get validatingwebhookconfigurations --all-namespaces
    ```
    {: pre}

6. If you configured [log forwarding](/docs/containers?topic=containers-health), review the node-related logs from the following paths.
    ```
    /var/log/containerd.log
    /var/log/kubelet.log
    /var/log/kube-proxy.log
    /var/log/syslog
    ```
    {: screen}

7. Check that a workload deployment does not cause the worker node issue.
    1. Taint the worker node with the issue.
        ```sh
        oc taint node NODEIP ibm-cloud-debug-isolate-customer-workload=true:NoExecute
        ```
        {: pre}

    2. Make sure that you deleted any custom admission controllers as described in step 5.
    3. Restart the worker node.
        * **Classic**: Reload the worker node.
          ```
          ibmcloud oc worker reload -c <cluster_name_or_ID> --worker <worker_ID>
          ```
          {: pre}

        * **VPC**: Replace the worker node.
          ```
          ibmcloud oc worker replace -c <cluster_name_or_ID> --worker <worker_ID> --update
          ```
          {: pre}

    4. Wait for the worker node to finish restarting. If the worker node enters a healthy state, the issue is likely caused by a workload.
    5. Schedule one workload at a time onto the worker node to see which workload causes the issue. To schedule the workloads, add the following toleration.
        ```
        tolerations:
        - effect: NoExecute
          key: ibm-cloud-debug-isolate-customer-workload
          operator: Exists
        ```
        {: pre}
        
    6. After you identify the workload that causes the issue, continue with [Debugging app deployments](/docs/containers?topic=containers-debug_apps).




