---

copyright:
  years: 2022, 2022
lastupdated: "2022-08-22"

keywords: cbr, context based restrictions, security, cbr scenario, openshiftcbr

subcollection: openshift

content-type: tutorial
services: openshift
account-plan: paid
completion-time: 30m

---

{{site.data.keyword.attribute-definition-list}}

# Example context-based restrictions scenarios
{: #cbr-tutorial}
{: toc-content-type="tutorial"}
{: toc-services="openshift}
{: toc-completion-time="30m"}

With context-based restrictions, account owners and administrators can define and enforce access restrictions for {{site.data.keyword.cloud}} resources, based on the context of access requests. Access to {{site.data.keyword.openshiftlong_notm}} resources can be controlled with context-based restrictions and identity and access management policies. For more information, see [Protecting {{site.data.keyword.openshiftlong_notm}} resources with context-based restrictions](/docs/containers?topic=containers-cbr).
{: shortdesc}

Setting up context-based restrictions for {{site.data.keyword.openshiftlong_notm}} resources is available for allowlisted accounts only.
{: preview}

Context-based restrictions limit access to the {{site.data.keyword.openshiftlong_notm}} objects that your application runs on, such as pods and workers, but not the application itself. 
{: note}

## Understanding the scenario
{: #cbr-tutorial-scenario}

In this example scenario, you use context-based restrictions to restrict traffic to your cluster by allowing only an individual IP address to connect to the `cluster` APIs over the public network while still allowing all private traffic.

In the following steps, you start by creating a network zone, or allowlist, that includes a single IP address. Then, you create a context-based restrictions rule for your cluster that allows all private network access and allowlists the network zone that contains the individual IP address. When you create the rule, you associate it with the network zone that contains the individual IP address.


## Prerequisites
{: #cbr-tutorial-prereqs}

Before beginning this tutorial, make sure you have created or installed the following resources and tools.

- An {{site.data.keyword.cloud_notm}} account. For more information, see [Creating an account](/docs/account?topic=account-account-getting-started).
- The CLI tools including the {{site.data.keyword.cloud_notm}} CLI, the Containers service CLI plug-in, and the CBR plug-in. For more information, see [Getting started with the {{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-getting-started).
- A {{site.data.keyword.openshiftlong_notm}} cluster. For more information, see [Creating clusters](/docs/containers?topic=containers-clusters).
- Review the [What are context-based restrictions](/docs/account?topic=account-context-restrictions-whatis) docs to get an understanding of concepts of network zones and rules.
- Review the [Protecting {{site.data.keyword.openshiftlong_notm}} resources with context-based restrictions](/docs/openshift?topic=openshift-cbr) docs to understand how you can leverage CBR for your {{site.data.keyword.openshiftlong_notm}} resources.
- Review the [limitations for using CBR with {{site.data.keyword.openshiftlong_notm}}](/docs/openshift?topic=openshift-cbr&interface=cli#cbr-limitations).


## Creating your network zone
{: #cbr-tutorial-create-zone}
{: step}

[Access your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-access_cluster).
1. Run the following example command to create a network that includes only one client IP that you want to use.

    ```sh
    ibmcloud cbr zone-create --addresses 129.XX.XX.XX --description "Allow only client IP" --name allow-client-ip
    ```
    {: pre}
    
1. Verify the network zone was created.
    ```sh
    ibmcloud cbr zones
    ```
    { :pre}



## Creating your CBR rule
{: #cbr-tutorial-create-rule}
{: step}

1. After you create your network zone (allowlist), create a CBR rule and add the network zone you created in the previous step. The following example creates a rule that uses the `cluster` API type.

    ```sh
    ibmcloud cbr rule-create --api-types crn:v1:bluemix:public:containers-kubernetes::::api-type:cluster --description "privateAccess=allowAll, publicAccess=oneIP" --service-name containers-kubernetes --service-instance CLUSTER-ID --context-attributes endpointType=private --context-attributes endpointType=public,networkZoneId=allow-client-ip
    ```
    {: pre}
    
    Understanding the command options.
    
    `--api-types crn:v1:bluemix:public:containers-kubernetes::::api-type:cluster`
    :   Set the `crn:v1:bluemix:public:containers-kubernetes::::api-type:cluster` API to allow resources in the network zone you created earlier to access only the `cluster` APIs, which include the APIs for various `oc` commands.
    
    `--service-instance CLUSTER-ID`
    :   Scope the rule to a single cluster so that resources in the network zone you created earlier can access only the `CLUSTER-ID`.
    
    `--context-attributes endpointType=private`
    :   Set the context attribute `endpointType=private` without associating a network zone allows all private traffic to the cluster.
    
    `--context-attributes endpointType=public,networkZoneId=all-client-ip`
    :   Set the context attribute `endpointType=public` and associate the `networkZoneId=allow-client-ip` that you created earlier to allow only the resources in the `allow-client-ip` zone to access the cluster over the public network.
    
    
1. Verify the rule was created.
    ```sh
    ibmcloud cbr rules
    ```
    {: pre}
    
## Testing your context-based restrictions
{: #cbr-tutorial-create-test}
{: step}

To test your context-based restrictions setup, you can try calling the cluster APIs for your cluster, for example by listing pods, over the public network from an IP address other than the individual IP address that you allowlisted in your network zone. With this setup, all private connectivity is allowed, while only the individual IP address in your network zone can connect to the cluster APIs over the public network.

## Additional scenarios
{: #cbr-tutorial-create-additional-scenarios}

Now that you've created a simpled CBR network zone and rule, review the following more advanced examples to further control access to your {{site.data.keyword.openshiftlong_notm}} resources.

### Allowing different IPs to access the public and private service endpoints
{: #cbr-tutorial-scenarios-pub-priv-one-ip}

In this scenario, you allow different IP addresses or CIDRs to access the public and private service endpoints of your {{site.data.keyword.openshiftlong_notm}} clusters by creating separate network zones for each IP address. Then, you create a rule that allows each network zone to access the public or private service endpoints.

1. Create a network zone for a public IP address or CIDR and another for a private IP address or CIDR that you want to allow to access your {{site.data.keyword.openshiftlong_notm}} clusters.

    Example commands to create separate network zones called `public-IP-zone` and `private-IP-zone`. In this example, each zone contains multiple IP addresses or CIDRs, separated by a comma, that you want to allow to access your clusters. 

    ```sh
    ibmcloud cbr zone-create --addresses 1.2.3.4,12.12.12.0/24 --description "Allowed Public IP Addresses Zone" --name "public-ip-zone"
    ```
    {: pre}

    ```sh
    ibmcloud cbr zone-create --addresses 10.20.20.20,10.10.10.0/24 --description "Allowed Private IP Addresses Zone" --name "private-ip-zone"
    ```
    {: pre}
    
1. Get the IDs of the `private-ip-zone` and `public-ip-zone` zones you created in the previous step.
    ```sh
    ibmcloud cbr zones 
    ```
    {: pre}
    
1. Create a rule that allows the `private-ip-zone` to connect to your cluster's private service endpoint and that also allows the `public-ip-zone` to connect to your cluster's public service endpoint only. This rule applies to the cluster specified with the `--service-instance` option. If you want to apply the rule to all clusters in your account, do not specify a cluster. 
    ```sh
    ibmcloud cbr rule-create --context-attributes "endpointType=public,networkZoneId=PUBLIC-IP-ZONE-ID" --context-attributes "endpointType=private,networkZoneId=PRIVATE-IP-ZONE-ID" --description "Separate private and public IPs for cluster and management rule" --service-name containers-kubernetes --service-instance CLUSTER-ID
    ```
    {: pre}


### Allowing different IPs to access different API types over the public and private service endpoints
{: #cbr-tutorial-scenarios-pub-priv-api-types}

Similar to the previous scenario, in this scenario you allow one public IP address and one private IP address to access the respective public or private service endpoint for {{site.data.keyword.openshiftlong_notm}} clusters. However, in this scenario, access is further restricted by specific API types for the `cluster` and `management` APIs. For more information about the API types, see [Protecting specific APIs](/docs/containers?topic=containers-cbr&interface=cli#protect-api-types-cbr).

1. Create four network zones, one for each of the IP addresses you want to allow to access either the public or private `cluster` APIs or the public or private `management` apis. Note that you can include multiple IP addresses or CIDRs, separated by a comma, that you want to allow to access your clusters. 

    ```sh
    ibmcloud cbr zone-create --addresses 1.2.3.4,12.12.12.0/24 --description "Allowed Public IP Addresses for IKS and ROKS APIs" --name "public-mgmt-zone"
    ```
    {: pre}
    
    ```sh
    ibmcloud cbr zone-create --addresses 10.20.20.20,10.10.10.0/24 --description "Allowed Private IP Addresses IKS and ROKS APIs" --name "private-mgmt-zone"
    ```
    {: pre}
    
    ```sh
    ibmcloud cbr zone-create --addresses 11.11.11.0/24 --description "Allowed Public IP Addresses for cluster apiserver" --name "public-cluster-zone"
    ```
    {: pre}
    
    ```sh
    ibmcloud cbr zone-create --addresses 10.30.30.30 --description "Allowed Private IP Addresses for cluster apiserver" --name "private-cluster-zone"
    ```
    {: pre}


1. Get the IDs of the zones you created in the previous step.
    ```sh
    ibmcloud cbr zones 
    ```
    {: pre}
    
    Example output
    
    ```sh
    OK
    id                                 name                   address_count   
    c14c0839c13d8aa0afa8383e2be2e124   public-mgmt-zone       2   
    f9676ca6ef37685315fa254b89d73159   public-cluster-zone    1   
    c14c0839c13d8aa0afa8383e2be2e843   private-cluster-zone   1   
    b53353de929de39ac2381f9b4cde8507   private-mgmt-zone      2 
    ```
    {: pre}
    
1. Create a rule that protects access to the public and private `cluster` and `management` APIs by using the zones you created earlier.

    ```sh
    ibmcloud cbr rule-create --api-types crn:v1:bluemix:public:containers-kubernetes::::api-type:management --context-attributes "endpointType=public,networkZoneId=PUBLIC-MGMT-ZONE-ID" --context-attributes "endpointType=private,networkZoneId=PRIVATE-MGMT-ZONE-ID" --description "Separate private and public IPs for the management APIs" --service-name containers-kubernetes
    ```
    {: pre}
    
    ```sh
    ibmcloud cbr rule-create --api-types crn:v1:bluemix:public:containers-kubernetes::::api-type:cluster --context-attributes "endpointType=public,networkZoneId=PUBLIC-CLUSTER-ZONE-ID" --context-attributes "endpointType=private,networkZoneId=PRIVATE-CLUSTER-ZONE-ID" --description "Separate private and public IPs for cluster APIs" --service-name containers-kubernetes
    ```
    {: pre}




