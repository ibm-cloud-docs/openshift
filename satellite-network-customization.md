


# Customizing your network setup in {{site.data.keyword.satelliteshort}} Locations and clusters
{: #satellite-network-customization}

There are several features that you can use to customize your {{site.data.keyword.satelliteshort}} network setup to better isolate and segment the services and workloads running in your location. Review the following sections for more information.



## Restricting NodePort service access
{: #nodeport-restrict-access}

By default, NodePort services are accessible on all network interfaces that are available to the cluster, for example `0.0.0.0`. 

However, in {{site.data.keyword.satelliteshort}} locations where multiple networks are available to the hosts, you can limit the available network interfaces for your services. 

To limit the range, you restrict the listening addresses for NodePort services at the cluster level. This restriction allows the cluster administrator to limit access to a specific network interface by using the IP subnet as the allowed listening address range. Complete the following steps to reconfigure the `kube-proxy` component to limit the listening address range for your NodePort services.


Incorrectly configuring the `node-port-addresses` might isolate your services from valid sources. Make sure you plan for all the required subnets your service needs. {{site.data.keyword.cloud_notm}} doesn't require access to any subnet to manage your clusters.
{: important}


1. [Access your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-access_cluster).
1. Prepare your planned source subnet CIDR list that you want to allow to access the NodePort Services.
1. Run the following command to get the `network.operator.openshift.io` configuration and save a copy in case you need to revert the changes.
    ```sh
    oc get network.operator.openshift.io cluster -o yaml
    ```
    {: pre}
    
1. Edit the `network.operator.openshift.io` configuration and set the subnet list under the `spec` section and include the required subnets for your NodePort service.
    ```yaml
    spec:
      kubeProxyConfig:
        proxyArguments:
          node-port-addresses:
          - 192.0.2.0/24
          - 198.51.100.0/24
    ```
    {: codeblock}
    
1. Save your changes and apply them to the cluster.

    ```sh
    oc apply -f updated-network-config.yaml
    ```
    {: pre}

1. For cluster version 4.10.x and earlier, set the management state of the cluster network operator to `Unmanaged`.

   ```sh
    oc patch network.operator.openshift.io cluster --type=merge --patch  '{"spec": {"managementState": "Unmanaged"}}'
   ```

1. Restart the `kube-proxy` DaemonSet to apply the changes. This operation is not disruptive.

    ```sh
    oc rollout restart ds -n openshift-kube-proxy openshift-kube-proxy
    ```
    {: pre}
    
1. Wait until all your `kube-proxy` pods are restarted. Check the status by running the following command.
    ```sh
    oc get po -n openshift-kube-proxy --selector app=kube-proxy
    ```
    {: pre}

1. For cluster version of 4.10.x and earlier, reset the management state of the cluster network operator to `Managed`. Note that this action might restart the proxy pods.

   ```sh
    oc patch network.operator.openshift.io cluster --type=merge --patch  '{"spec": {"managementState": "Managed"}}'
   ```

After all pods are restarted, your cluster is configured with the restricted subnets. You can repeat these steps to update or remove the subnet list as needed.

You can further restrict the traffic by using `NetworkPolicies` [on a per-service basis](https://kubernetes.io/docs/concepts/services-networking/network-policies/){: external}.
{: tip}


