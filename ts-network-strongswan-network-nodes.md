---

copyright: 
  years: 2014, 2021
lastupdated: "2021-10-06"

keywords: openshift, roks, rhoks, rhos

subcollection: openshift
content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}



# Why does strongSwan VPN connectivity fail after I add or delete worker nodes?
{: #cs_vpn_fails_worker_add}

**Infrastructure provider**: ![Classic infrastructure provider icon.](images/icon-classic-2.svg) Classic


You previously established a working VPN connection by using the strongSwan IPSec VPN service. However, after you added or deleted a worker node on your cluster, you experience one or more of the following symptoms:
{: tsSymptoms}

* You do not have a VPN status of `ESTABLISHED`
* You cannot access new worker nodes from your on-prem network
* You cannot access the remote network from pods that are running on new worker nodes


If you added a worker node to a worker pool:
{: tsCauses}

* The worker node was provisioned on a new private subnet that is not exposed over the VPN connection by your existing `localSubnetNAT` or `local.subnet` settings.
* VPN routes cannot be added to the worker node because the worker has taints or labels that are not included in your existing `tolerations` or `nodeSelector` settings.
* The VPN pod is running on the new worker node, but the public IP address of that worker node is not allowed through the on-premises firewall.

If you deleted a worker node:

* That worker node was the only node where a VPN pod was running, due to restrictions on certain taints or labels in your existing `tolerations` or `nodeSelector` settings.


Update the Helm chart values to reflect the worker node changes.
{: tsResolve}

1. Delete the existing Helm chart.

    ```sh
    helm uninstall <release_name> -n <project>
    ```
    {: pre}

2. Open the configuration file for your strongSwan VPN service.

    ```sh
    helm show values iks-charts/strongswan > config.yaml
    ```
    {: pre}

3. Check the following settings and change the settings to reflect the deleted or added worker nodes as necessary.

    **If you added a worker node:**

    <table summary="The columns are read from left to right. The first column has the worker node setting. The second column describes the setting.">
    <caption>Worker node settings</caption>
        <col width="25%">
        <thead>
        <th>Setting</th>
        <th>Description</th>
        </thead>
        <tbody>
        <tr>
        <td><code>localSubnetNAT</code></td>
        <td>The added worker might be deployed on a new, different private subnet than the other existing subnets that other worker nodes are on. If you use subnet NAT to remap your cluster's private local IP addresses and the worker was added on a new subnet, add the new subnet CIDR to this setting.</td>
        </tr>
        <tr>
        <td><code>nodeSelector</code></td>
        <td>If you previously limited VPN pod deployment to workers with a specific label, ensure the added worker node also has that label.</td>
        </tr>
        <tr>
        <td><code>tolerations</code></td>
        <td>If the added worker node is tainted, then change this setting to allow the VPN pod to run on all tainted workers with any taints or specific taints.</td>
        </tr>
        <tr>
        <td><code>local.subnet</code></td>
        <td>The added worker might be deployed on a new, different private subnet than the existing subnets that other workers are on. If your apps are exposed by NodePort or LoadBalancer services on the private network and the apps are on the added worker, add the new subnet CIDR to this setting. <strong>Note</strong>: If you add values to <code>local.subnet</code>, check the VPN settings for the on-premises subnet to see whether they also must be updated.</td>
        </tr>
        </tbody></table>

    **If you deleted a worker node:**

    <table summary="The columns are read from left to right. The first column has the worker node setting. The second column describes the setting.">
    <caption>Worker node settings</caption>
        <col width="25%">
        <thead>
        <th>Setting</th>
        <th>Description</th>
        </thead>
        <tbody>
        <tr>
        <td><code>localSubnetNAT</code></td>
        <td>If you use subnet NAT to remap specific private local IP addresses, remove any IP addresses from this setting that are from the old worker. If you use subnet NAT to remap entire subnets and no workers remain on a subnet, remove that subnet CIDR from this setting.</td>
        </tr>
        <tr>
        <td><code>nodeSelector</code></td>
        <td>If you previously limited VPN pod deployment to a single worker and that worker was deleted, change this setting to allow the VPN pod to run on other workers.</td>
        </tr>
        <tr>
        <td><code>tolerations</code></td>
        <td>If the worker that you deleted was not tainted, but the only workers that remain are tainted, change this setting to allow the VPN pod to run on workers with any taints or specific taints.
        </td>
        </tr>
        </tbody></table>

4. Install the new Helm chart with your updated values.
    ```sh
    helm install <release_name> iks-charts/strongswan -f config.yaml
    ```
    {: pre}

5. Check the chart deployment status. When the chart is ready, the **STATUS** field near the top of the output has a value of `DEPLOYED`.
    ```sh
    helm status <release_name>
    ```
    {: pre}

6. In some cases, you might need to change your on-prem settings and your firewall settings to match the changes you made to the VPN configuration file.

7. Start the VPN.
    * If the VPN connection is initiated by the cluster (`ipsec.auto` is set to `start`), start the VPN on the on-prem gateway, and then start the VPN on the cluster.
    * If the VPN connection is initiated by the on-prem gateway (`ipsec.auto` is set to `auto`), start the VPN on the cluster, and then start the VPN on the on-prem gateway.

8. Set the `STRONGSWAN_POD` environment variable.
    ```sh
    export STRONGSWAN_POD=$(oc get pod -l app=strongswan,release=<release_name> -o jsonpath='{ .items[0].metadata.name }')
    ```
    {: pre}

9. Check the status of the VPN.
    ```sh
    oc exec  $STRONGSWAN_POD -- ipsec status
    ```
    {: pre}

    * If the VPN connection has a status of `ESTABLISHED`, the VPN connection was successful. No further action is needed.
    * If you are still having connection issues, see [Why can't I establish VPN connectivity with the strongSwan Helm chart?](/docs/containers?topic=containers-cs_vpn_fails) to further troubleshoot your VPN connection.




