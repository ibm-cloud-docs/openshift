---

copyright: 
  years: 2014, 2021
lastupdated: "2021-10-26"

keywords: openshift, roks, rhos, rhoks, vpn, on-prem, gateway, static

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}


# Adding static routes to worker nodes
{: #static-routes}

Create static routes on your worker nodes by enabling the static routes add-on for {{site.data.keyword.openshiftlong}} clusters.
{: shortdesc}

## About static routes
{: #about-static-routes}

When you configure your cluster network to communicate with other networks over the private network, you might need to add custom static routes on your worker nodes. Static routes allow worker nodes to successfully re-route response packets from your cluster to an IP address in on-premises data center through a VPN or a gateway appliance.
{: shortdesc}

For example, you might use a VPN to connect your cluster to an on-premises data center over the private network. Additionally, your private VPN connection preserves the source IP address in requests between the cluster and the data center.

When an on-premises service sends a request to an app in your cluster, the worker node that your app pod is on drops the response due to reverse path filtering (RPF). RPF is a Linux kernel feature that drops any responses to IP addresses that are not listed in the worker node's routing tables. The response is dropped because the on-premises IP address that was preserved in the request is not routable by the worker node.

In this case, you can create a static route so that when a request's source IP address is from one of your on-premises subnets, the response is sent to the VPN gateway IP address instead. By adding this static route to the worker nodes' routing tables, you ensure the following:
* Response packets are not dropped due to RPF, because a routing rule that points to the on-premises IP address exists.
* Response packets are successfully routed first through the VPN gateway IP address, and then re-routed to your on-premises IP address.

The static route cluster add-on can be used to apply and manage static routes only. You are responsible for configuring and managing your own VPN, gateway appliance, or {{site.data.keyword.BluDirectLink}} connection.
{: note}



## Enabling the static route add-on
{: #enable-add-on}

To get started with static routes in {{site.data.keyword.openshiftlong_notm}}, enable the static route add-on.
{: shortdesc}

**Before you begin**
* Ensure that you have the [**Administrator** IAM platform access role for the cluster in {{site.data.keyword.containerlong_notm}}](/docs/openshift?topic=openshift-users#checking-perms).
* [Access your {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-access_cluster).

### Enabling the static route add-on from the console
{: #enable-add-on-console}

To use the {{site.data.keyword.cloud_notm}} console, follow these steps.

1. In your [cluster dashboard](https://cloud.ibm.com/kubernetes/clusters){: external}, click the name of the cluster where you want to install the static route add-on.
2. Click the **Add-ons** tab.
3. On the **Static Route** card, click **Install**.
4. Click **Install** again.
5. On the **Static Route** card, verify that the add-on is listed.


### Enabling the static route add-on with the CLI
{: #enable-add-on-cli}

To use the CLI, follow these steps.

1. [Target the CLI to your cluster](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure).

2. Enable the `static-route` add-on.

    ```sh
    ibmcloud oc cluster addon enable static-route --cluster <cluster_name_or_ID>
    ```
    {: pre}

3. Verify that the static route add-on has a status of `Addon Ready`.

    ```sh
    ibmcloud oc cluster addon ls --cluster <cluster_name_or_ID>
    ```
    {: pre}

    Example output
    
    ```sh
    Name              Version     Health State   Health Status
    static-route      1.0.0       normal         Addon Ready
    ```
    {: screen}



## Creating static routes
{: #create-route-resources}

After you [enable the static route add-on](#enable-add-on), you can create and apply resources for custom routes.
{: shortdesc}

1. Create a YAML file for a static route resource.

    ```yaml
    apiVersion: static-route.ibm.com/v1
    kind: StaticRoute
    metadata:
      name: <route_name>
    spec:
      subnet: "<subnet_CIDR>"
      gateway: "<gateway_IP>"
      selectors:
        - key: "<label_key>"
          values:
            - "<label_value>"
          operator: In
    ```
    {: codeblock}

    Example
    
    ```yaml
    apiVersion: static-route.ibm.com/v1
    kind: StaticRoute
    metadata:
      name: mystaticroute
    spec:
      subnet: "192.168.0.0/24"
      gateway: "10.0.0.1"
      selectors:
        - key: "kubernetes.io/arch"
          values:
            - "amd64"
          operator: In
    ```
    {: screen}

    `subnet`
    :   Specify the CIDR of the external subnet from which requests to the worker nodes are sent, such as a subnet in an on-premises network. The external subnet cannot be in the following reserved ranges. The device interconnect range, `198.18.0.0/15`, is permitted.
        - `10.0.0.0/8`
        - `172.16.0.0/16`
        - `172.18.0.0/16`
        - `172.19.0.0/16`
        - `172.20.0.0/16`
        - `192.168.255.0/24`
        
    `gateway`
    :   If your gateway IP address exists on the same subnet as your worker nodes, specify the gateway IP address. If your gateway IP address exists on another subnet in your IBM Cloud private network, do not include this field. In this case, worker nodes send responses to the private network's backend router, and the router sends the response to the gateway on the other subnet. When the static route is created, the backend router's IP address in the `10.0.0.0/8` range is automatically assigned as a default gateway.
    
    `selectors`
    :   To create the static route only on certain worker nodes based on worker node labels, include the `key` and `values` for the label.


2. Create the static routes by applying the YAML file to your cluster.

    ```sh
    oc apply -f <route_name>.yaml
    ```
    {: pre}

3. Verify that the static route is created. In the output, check the `node_status` for each worker node where you create the static route.

    ```sh
    oc get staticroute <route_name> -o yaml
    ```
    {: pre}

    Example output
    
    ```sh
    apiVersion: static-route.ibm.com/v1
    kind: StaticRoute
    metadata:
        annotations:
          kubectl.kubernetes.io/last-applied-configuration: |
        {"apiVersion":"static-route.ibm.com/v1","kind":"StaticRoute","metadata":{"annotations":{},"name":"mystaticroute"},"spec":{"selectors":[{"key":"kubernetes.io/arch","operator":"In","values":["amd64"]}],"subnet":"10.94.227.46/24"}}
    creationTimestamp: "2020-05-20T16:43:12Z"
    finalizers:
    - finalizer.static-route.ibm.com
    generation: 1
    name: mystaticroute
    resourceVersion: "3753886"
    selfLink: /apis/static-route.ibm.com/v1/staticroutes/mystaticroute
    uid: f284359f-9d13-4e27-9d3a-8fb38cbc7a5c
      spec:
        selectors:
        - key: kubernetes.io/arch
          operator: In
          values:
          - amd64
        subnet: 10.94.227.46/24
      status:
        nodeStatus:
        - error: ""
          hostname: 10.94.227.19
          state:
            gateway: 10.94.227.1
            selectors:
            - key: kubernetes.io/arch
              operator: In
              values:
              - amd64
            subnet: 10.94.227.46/24
        - error: ""
          hostname: 10.94.227.22
          state:
            gateway: 10.94.227.1
            selectors:
            - key: kubernetes.io/arch
              operator: In
              values:
              - amd64
            subnet: 10.94.227.46/24
    ```
    {: screen}







