---

copyright: 
  years: 2025, 2025
lastupdated: "2025-11-24"


keywords: kubernetes, rebalance, resize, node scaling, ca, autoscaler, openshift

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}



# Rebalancing or resizing autoscaled worker pools
{: #ca_update_worker_node_pool}

Before you can rebalance or resize your worker pool, you must remove the worker pool from the autoscaler configmap to disable autoscaling.


1. Edit `iks-ca-configmap` and disable the worker pool that you want to resize or rebalance by removing it from the `workerPoolsConfig.json` section.

    ```sh
    oc edit cm -n kube-system iks-ca-configmap
    ```
    {: pre}

    Example output

    ```yaml
    apiVersion: v1
    data:
      workerPoolsConfig.json: |
        [
         {"name": "","minSize": 1,"maxSize": 2,"enabled":false}
        ]
    kind: ConfigMap
    ```
    {: screen}

2. Save the `iks-ca-configmap`.

3. [Resize](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_pool_resize) or [rebalance](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_rebalance) your worker pool.

4. **Optional** [Update your VPC worker nodes](/docs/openshift?topic=openshift-update#vpc_worker_node).

5. Add the worker pool to the `iks-ca-configmap`.
    ```sh
    oc edit cm -n kube-system iks-ca-configmap
    ```
    {: pre}

    Example
    ```yaml
    apiVersion: v1
    data:
      workerPoolsConfig.json: |
        [
         {"name": "<worker_pool>","minSize": 1,"maxSize": 2,"enabled":false}
        ]
    kind: ConfigMap
    ```
    {: screen}


