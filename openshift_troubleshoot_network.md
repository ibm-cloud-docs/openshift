---

copyright:
  years: 2014, 2021
lastupdated: "2021-04-21"

keywords: openshift, roks, rhoks, rhos

subcollection: openshift
content-type: troubleshoot

---

{:DomainName: data-hd-keyref="APPDomain"}
{:DomainName: data-hd-keyref="DomainName"}
{:android: data-hd-operatingsystem="android"}
{:api: .ph data-hd-interface='api'}
{:apikey: data-credential-placeholder='apikey'}
{:app_key: data-hd-keyref="app_key"}
{:app_name: data-hd-keyref="app_name"}
{:app_secret: data-hd-keyref="app_secret"}
{:app_url: data-hd-keyref="app_url"}
{:authenticated-content: .authenticated-content}
{:beta: .beta}
{:c#: data-hd-programlang="c#"}
{:cli: .ph data-hd-interface='cli'}
{:codeblock: .codeblock}
{:curl: .ph data-hd-programlang='curl'}
{:deprecated: .deprecated}
{:dotnet-standard: .ph data-hd-programlang='dotnet-standard'}
{:download: .download}
{:external: target="_blank" .external}
{:faq: data-hd-content-type='faq'}
{:fuzzybunny: .ph data-hd-programlang='fuzzybunny'}
{:generic: data-hd-operatingsystem="generic"}
{:generic: data-hd-programlang="generic"}
{:gif: data-image-type='gif'}
{:go: .ph data-hd-programlang='go'}
{:help: data-hd-content-type='help'}
{:hide-dashboard: .hide-dashboard}
{:hide-in-docs: .hide-in-docs}
{:important: .important}
{:ios: data-hd-operatingsystem="ios"}
{:java: .ph data-hd-programlang='java'}
{:java: data-hd-programlang="java"}
{:javascript: .ph data-hd-programlang='javascript'}
{:javascript: data-hd-programlang="javascript"}
{:new_window: target="_blank"}
{:note .note}
{:note: .note}
{:objectc data-hd-programlang="objectc"}
{:org_name: data-hd-keyref="org_name"}
{:php: data-hd-programlang="php"}
{:pre: .pre}
{:preview: .preview}
{:python: .ph data-hd-programlang='python'}
{:python: data-hd-programlang="python"}
{:route: data-hd-keyref="route"}
{:row-headers: .row-headers}
{:ruby: .ph data-hd-programlang='ruby'}
{:ruby: data-hd-programlang="ruby"}
{:runtime: architecture="runtime"}
{:runtimeIcon: .runtimeIcon}
{:runtimeIconList: .runtimeIconList}
{:runtimeLink: .runtimeLink}
{:runtimeTitle: .runtimeTitle}
{:screen: .screen}
{:script: data-hd-video='script'}
{:service: architecture="service"}
{:service_instance_name: data-hd-keyref="service_instance_name"}
{:service_name: data-hd-keyref="service_name"}
{:shortdesc: .shortdesc}
{:space_name: data-hd-keyref="space_name"}
{:step: data-tutorial-type='step'}
{:subsection: outputclass="subsection"}
{:support: data-reuse='support'}
{:swift: .ph data-hd-programlang='swift'}
{:swift: data-hd-programlang="swift"}
{:table: .aria-labeledby="caption"}
{:term: .term}
{:tip: .tip}
{:tooling-url: data-tooling-url-placeholder='tooling-url'}
{:troubleshoot: data-hd-content-type='troubleshoot'}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:tsSymptoms: .tsSymptoms}
{:tutorial: data-hd-content-type='tutorial'}
{:ui: .ph data-hd-interface='ui'}
{:unity: .ph data-hd-programlang='unity'}
{:url: data-credential-placeholder='url'}
{:user_ID: data-hd-keyref="user_ID"}
{:vbnet: .ph data-hd-programlang='vb.net'}
{:video: .video}
 


# Cluster networking
{: #cs_troubleshoot_network}

As you use {{site.data.keyword.openshiftlong_notm}}, consider these techniques for troubleshooting the management of your cluster network.
{: shortdesc}

While you troubleshoot, you can use the [{{site.data.keyword.containerlong_notm}} Diagnostics and Debug Tool](/docs/openshift?topic=openshift-cs_troubleshoot#debug_utility) to run tests and gather pertinent information from your cluster.
{: tip}


## Missing the public `containers.appdomain.cloud` subdomain
{: #roks_ts_subdomain}
{: troubleshoot}
{: support}

**Infrastructure provider**:
  * <img src="images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Classic
  * <img src="images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> VPC

{: tsSymptoms}
When you expose an app through a router subdomain, you get a local subdomain instead of a public route, in the format: `<service_name>-<project_name>.router.default.svc.cluster.local`.

When you try to open the {{site.data.keyword.openshiftshort}} web console or another app route in your browser, you might see an error similar to the following.

```
Application is not available
The application is currently not serving requests on this endpoint.
```
{: screen}

{: tsCauses}
After the cluster is created and enters a **normal** state, the router subdomain networking and load balancing components still take some time to deploy. If you expose your app before the networking components fully provision, or if the components experience an error, your apps can only be exposed internally with the default router's `svc.cluster.local` domain.

When the components fully provision, a public router subdomain is available for your apps, in the format `<cluster-name>-<accountID-hashed>-<ssll>.<region>.containers.appdomain.cloud`.

{: tsResolve}

1.  After you create a cluster, wait some time before you expose your apps, even after the cluster enters a **normal** state.
2.  Check the **Master Status**. If the **Master Status** is not **Ready**, [review its status](/docs/openshift?topic=openshift-cs_troubleshoot#debug_master) and follow any troubleshooting information to resolve the issue.   
    ```
    ibmcloud oc cluster get -c <cluster_name_or_ID>
    ```
    {: pre}
3.  Check that your cluster has public connectivity so that the networking components can talk to the master as they deploy.
    * <img src="images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> **VPC clusters**: To run default {{site.data.keyword.openshiftshort}} components such as the web console or OperatorHub, a public gateway must be attached to the VPC subnets that the worker nodes are deployed to. To check whether a public gateway exists for your VPC subnets in each zone, see steps 3 and 4 in [Creating a VPC subnet and attaching a public gateway](/docs/openshift?topic=openshift-vpc-subnets#create_vpc_subnet_cli).
    * <img src="images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> **Classic clusters**:
      * In the output of Step 2, check that your cluster has a **Public Service Endpoint URL** and does not have a **Private Service Endpoint URL**.
         * If your cluster does not have a public cloud service endpoint, [enable it](/docs/openshift?topic=openshift-cs_network_cluster#set-up-public-se).
      * Check that at least some of the worker nodes in your cluster have a **Public IP** address. If no worker node does, you must [set up public VLANs for at least one worker pool](/docs/openshift?topic=openshift-cs_network_cluster#change-vlans).
          ```
          ibmcloud oc workers -c <cluster_name_or_ID>
          ```
          {: pre}
4.  In the output of Step 2, check that the **Ingress Subdomain** is available. The Ingress components in your cluster must provision before the router components can be created. If the **Ingress Subdomain** and **Ingress Secret** are not available, see [No Ingress subdomain exists after cluster creation](/docs/openshift?topic=openshift-cs_troubleshoot_debug_ingress#ingress_subdomain).
5.  Check that the **Hostname** of the router subdomain is in the format: `<cluster-name>-<accountID-hashed>-<ssll>.<region>.containers.appdomain.cloud`.
    ```
    ibmcloud oc nlb-dns ls -c <cluster_name_or_ID>
    ```
    {: pre}

    *  If after two hours of creating the cluster, the router subdomain is not updated, review the **Master Status** of the cluster again, and follow any troubleshooting steps to resolve the issue.

If the troubleshooting steps do not resolve the issue, see [Getting help](/docs/openshift?topic=openshift-get-help).

<br />


## Cannot establish VPN connectivity with the strongSwan Helm chart
{: #cs_vpn_fails}

**Infrastructure provider**: <img src="images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Classic

{: tsSymptoms}
When you check VPN connectivity by running `oc exec  $STRONGSWAN_POD -- ipsec status`, you do not see a status of `ESTABLISHED`, or the VPN pod is in an `ERROR` state or continues to crash and restart.

{: tsCauses}
Your Helm chart configuration file has incorrect values, missing values, or syntax errors.

{: tsResolve}
When you try to establish VPN connectivity with the strongSwan Helm chart, it is likely that the VPN status will not be `ESTABLISHED` the first time. You might need to check for several types of issues and change your configuration file accordingly. To troubleshoot your strongSwan VPN connectivity:

1. [Test and verify the strongSwan VPN connectivity](/docs/openshift?topic=openshift-vpn#vpn_test) by running the five Helm tests that are included in the strongSwan chart definition.

2. If you are unable to establish VPN connectivity after running the Helm tests, you can run the VPN debugging tool that is packaged inside of the VPN pod image.

    1. Set the `STRONGSWAN_POD` environment variable.

        ```
        export STRONGSWAN_POD=$(oc get pod -l app=strongswan,release=vpn -o jsonpath='{ .items[0].metadata.name }')
        ```
        {: pre}

    2. Run the debugging tool.

        ```
        oc exec  $STRONGSWAN_POD -- vpnDebug
        ```
        {: pre}

        The tool outputs several pages of information as it runs various tests for common networking issues. Output lines that begin with `ERROR`, `WARNING`, `VERIFY`, or `CHECK` indicate possible errors with the VPN connectivity.

    <br />

## Cannot install a new strongSwan Helm chart release
{: #cs_strongswan_release}

**Infrastructure provider**: <img src="images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Classic

{: tsSymptoms}
You modify your strongSwan Helm chart and try to install your new release by running `helm install vpn iks-charts/strongswan -f config.yaml`. However, you see the following error:
```
Error: release vpn failed: deployments.extensions "vpn-strongswan" already exists
```
{: screen}

{: tsCauses}
This error indicates that the previous release of the strongSwan chart was not completely uninstalled.

{: tsResolve}

1. Delete the previous chart release.
    ```
    helm uninstall vpn -n <project>
    ```
    {: pre}

2. Delete the deployment for the previous release. Deletion of the deployment and associated pod takes up to 1 minute.
    ```
    oc delete deploy vpn-strongswan
    ```
    {: pre}

3. Verify that the deployment has been deleted. The deployment `vpn-strongswan` does not appear in the list.
    ```
    oc get deployments
    ```
    {: pre}

4. Re-install the updated strongSwan Helm chart with a new release name.
    ```
    helm install vpn iks-charts/strongswan -f config.yaml
    ```
    {: pre}

<br />

## strongSwan VPN connectivity fails after you add or delete worker nodes
{: #cs_vpn_fails_worker_add}

**Infrastructure provider**: <img src="images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Classic

{: tsSymptoms}
You previously established a working VPN connection by using the strongSwan IPSec VPN service. However, after you added or deleted a worker node on your cluster, you experience one or more of the following symptoms:

* You do not have a VPN status of `ESTABLISHED`
* You cannot access new worker nodes from your on-prem network
* You cannot access the remote network from pods that are running on new worker nodes

{: tsCauses}
If you added a worker node to a worker pool:

* The worker node was provisioned on a new private subnet that is not exposed over the VPN connection by your existing `localSubnetNAT` or `local.subnet` settings
* VPN routes cannot be added to the worker node because the worker has taints or labels that are not included in your existing `tolerations` or `nodeSelector` settings
* The VPN pod is running on the new worker node, but the public IP address of that worker node is not allowed through the on-premises firewall

If you deleted a worker node:

* That worker node was the only node where a VPN pod was running, due to restrictions on certain taints or labels in your existing `tolerations` or `nodeSelector` settings

{: tsResolve}
Update the Helm chart values to reflect the worker node changes:

1. Delete the existing Helm chart.

    ```
    helm uninstall <release_name> -n <project>
    ```
    {: pre}

2. Open the configuration file for your strongSwan VPN service.

    ```
    helm show values ibm/strongswan > config.yaml
    ```
    {: pre}

3. Check the following settings and change the settings to reflect the deleted or added worker nodes as necessary.

    If you added a worker node:

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
     <td>The added worker might be deployed on a new, different private subnet than the existing subnets that other workers are on. If your apps are exposed by NodePort or LoadBalancer services on the private network and the apps are on the added worker, add the new subnet CIDR to this setting. **Note**: If you add values to `local.subnet`, check the VPN settings for the on-premises subnet to see whether they also must be updated.</td>
     </tr>
     </tbody></table>

    If you deleted a worker node:

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

    ```
    helm install <release_name> iks-charts/strongswan -f config.yaml
    ```
    {: pre}

5. Check the chart deployment status. When the chart is ready, the **STATUS** field near the top of the output has a value of `DEPLOYED`.

    ```
    helm status <release_name>
    ```
    {: pre}

6. In some cases, you might need to change your on-prem settings and your firewall settings to match the changes you made to the VPN configuration file.

7. Start the VPN.
    * If the VPN connection is initiated by the cluster (`ipsec.auto` is set to `start`), start the VPN on the on-prem gateway, and then start the VPN on the cluster.
    * If the VPN connection is initiated by the on-prem gateway (`ipsec.auto` is set to `auto`), start the VPN on the cluster, and then start the VPN on the on-prem gateway.

8. Set the `STRONGSWAN_POD` environment variable.

    ```
    export STRONGSWAN_POD=$(oc get pod -l app=strongswan,release=<release_name> -o jsonpath='{ .items[0].metadata.name }')
    ```
    {: pre}

9. Check the status of the VPN.

    ```
    oc exec  $STRONGSWAN_POD -- ipsec status
    ```
    {: pre}

    * If the VPN connection has a status of `ESTABLISHED`, the VPN connection was successful. No further action is needed.

    * If you are still having connection issues, see [Cannot establish VPN connectivity with the strongSwan Helm chart](#cs_vpn_fails) to further troubleshoot your VPN connection.
