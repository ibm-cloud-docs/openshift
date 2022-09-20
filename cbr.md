---

copyright:
  years: 2022, 2022
lastupdated: "2022-09-19"

keywords: cbr, context based restrictions, security

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}



# Protecting {{site.data.keyword.openshiftlong_notm}} resources with context-based restrictions
{: #cbr}

Context-based restrictions give account owners and administrators the ability to define and enforce access restrictions for {{site.data.keyword.cloud}} resources based on the context of access requests. Access to {{site.data.keyword.openshiftlong_notm}} resources can be controlled with context-based restrictions and identity and access management policies.
{: shortdesc}

Setting up context-based restrictions for {{site.data.keyword.openshiftlong_notm}} resources is available for allowlisted accounts only.
{: preview}

These restrictions work with traditional IAM policies, which are based on identity, to provide an extra layer of protection. Unlike IAM policies, context-based restrictions don't assign access. Context-based restrictions check that an access request comes from an allowed context that you configure. Since both IAM access and context-based restrictions enforce access, context-based restrictions offer protection even in the face of compromised or mismanaged credentials. For more information, see [What are context-based restrictions](/docs/account?topic=account-context-restrictions-whatis).

A user must have the Administrator role on the {{site.data.keyword.openshiftlong_notm}} service to create, update, or delete rules. And a user must have either the Editor or Administrator role on the Context-based restrictions service to create, update, or delete network zones.
{: note}

Any {{site.data.keyword.cloudaccesstrailshort}} or audit log events generated will come from the context-based restrictions service, and not {{site.data.keyword.openshiftlong_notm}}. For more information, see [Monitoring context-based restrictions](/docs/account?topic=account-cbr-monitor). 

Attempts to access the cluster control plane, which can be restricted by using the `Cluster` API type, do not generate {{site.data.keyword.cloudaccesstrailshort}} or audit log events.
{: note}

## How {{site.data.keyword.openshiftlong_notm}} integrates with context-based restrictions
{: #cbr-overview}

You can create context-based restrictions (CBR) for {{site.data.keyword.openshiftlong_notm}} resources or for specific APIs. With Context-based restrictions, you can protect the following resources.


Protect {{site.data.keyword.openshiftlong_notm}} resources
:   [Restrict access to clusters, resource groups, or regions](#resources-types-cbr).

Protect specific APIs
:   Restrict accessing to provisioning and managing clusters and workers. Or, restrict access to Kubernetes APIs such as viewing pods and nodes. For more information, see [Protecting specific APIs](#protect-api-types-cbr).

Applications running on {{site.data.keyword.openshiftlong_notm}} clusters, for example web servers exposed by a Kubernetes LoadBalancer are not restricted by CBR rules.
{: note}


### Protecting {{site.data.keyword.openshiftlong_notm}} resources
{: #resources-types-cbr}

You can create CBR rules to protect specific regions, and clusters.

Cluster
:   Protects a specific {{site.data.keyword.openshiftlong_notm}} cluster. If you include a cluster in your CBR rule, resources in the network zones that you associate with the rule can interact only with that cluster.
:   If you use the CLI, you can specify the `--service-instance CLUSTER-ID` option to protect a specific cluster.
:   If you use the API, you can specify `"name": "serviceInstance","value": "CLUSTER-ID"` in the resource attributes.

Region
:   Protects {{site.data.keyword.openshiftlong_notm}} resources in a specific region. If you include a region in your CBR rule, resources in the network zones that you associate with the rule can interact only with resources in that region.
:   If you use the CLI, you can specify the `--region REGION` option to protect resources in a specific region.
:   If you use the API, you can specify `"name": "region","value": "REGION"` field in the resource attributes.

Resource group
:   Protects {{site.data.keyword.openshiftlong_notm}} resources in a specific resource group.
:   If you use the CLI, you can specify the `--resource-group-id RESOURCE-GROUP-ID` option to protect resources in a specific resource group.
:   If you use the API, you can specify `"name": "resourceGroupId","value": "RESOURCE-GROUP-ID"` field in the resource attributes.


### Protecting specific APIs
{: #protect-api-types-cbr}

You can create CBR rules to protect the following API types for {{site.data.keyword.openshiftlong_notm}}.

Cluster control plane APIs
:   Protect access to the APIs inside your clusters, such as the APIs for creating namespaces, pods, and more. CBR rules that apply to the cluster API type control access to your cluster API server, which includes all `oc` commands to that cluster. If you include the cluster control plane APIs in your CBR type, then resources in the network zone that associate with the rule can interact only with the cluster control plane APIs. All other requests are blocked.
:   If you use the CLI, you can specify the `--api-types` option and the `crn:v1:bluemix:public:containers-kubernetes::::api-type:cluster` type.
:   If you use the API, you can specify `"api_type_id": "crn:v1:bluemix:public:containers-kubernetes::::api-type:cluster"` in the `"operations"` spec.

Management APIs
:   Protect access to the APIs for provisioning and managing clusters, worker pools, and more. CBR rules that apply to the management API type control access the {{site.data.keyword.openshiftlong_notm}} APIs, which includes all `ibmcloud oc` commands calls, such as `ibmcloud oc clusters`, `ibmcloud oc cluster create`, and more. If you include the management APIs in your CBR type, then resources in the network zone that associate with the rule can interact only with the management APIs.
:   If you use the CLI, you can specify the `--api-types` option and the `crn:v1:bluemix:public:containers-kubernetes::::api-type:management` type.
:   If you use the API, you can specify `"api_type_id": "crn:v1:bluemix:public:containers-kubernetes::::api-type:cluster"` in the `"operations"` spec.

To follow an example CBR scenario, see [Setting up context-based restrictions](/docs/containers?topic=containers-cbr-tutorial).
{: tip}

### Allowing {{site.data.keyword.openshiftlong_notm}} to access other {{site.data.keyword.cloud_notm}} resources by using CBR
{: #cbr-integrations}

You must add the `containers-kubernetes` to your network zones for rules created against the following services.
{: important}

IAM Identity service 
:   Allow {{site.data.keyword.openshiftlong_notm}} to create tokens and API Keys like the cluster API Key and the {{site.data.keyword.registrylong_notm}} token and API Key.

IAM Access Management Service
:   Allow {{site.data.keyword.openshiftlong_notm}} to create an IAM Access Policy for Reader service access role to {{site.data.keyword.registrylong_notm}}.

IAM Access Groups Service
:   Allow {{site.data.keyword.openshiftlong_notm}} to look up access groups when syncing IAM access policies with RBAC in the cluster.

User Management
:   Allow {{site.data.keyword.openshiftlong_notm}} to access user information when syncing IAM access policies with RBAC in the cluster.



{{site.data.keyword.cos_full_notm}}
:   Allow {{site.data.keyword.openshiftlong_notm}} to back up the internal registry images in VPC clusters.


Key protect: 
:   Allow {{site.data.keyword.openshiftlong_notm}} to enable encryption on the cluster.



## Creating network zones
{: #create-cbr-network-zone-openshift}

Network zones act as allowlists for the target resources you define when you create CBR rules. After you create a network zone, or allowlist, you can create rules that define which resources the network zone can access.

Make sure to add the `containers-kubernetes` service to your network zones for rules that apply to other {{site.data.keyword.cloud_notm}} resources, such as a rule that protects {{site.data.keyword.cos_full_notm}} or some cluster operations might fail. For more information, see [Allowing {{site.data.keyword.openshiftlong_notm}} to access other {{site.data.keyword.cloud_notm}} resources by using CBR](#cbr-integrations).
{: important}

Review the [limitations](#cbr-limitations) before you create network zones.
{: note}

### Creating network zones from the API
{: #create-network-zone-api}
{: api}

You can create network zones by using the `/v1/zones` API. For more information, see the [API docs](/apidocs/context-based-restrictions#create-zone). You can add the `containers-kubernetes` service to your network zones to allow {{site.data.keyword.openshiftlong_notm}} to access resources and services in your account.



You can include multiple address types in your network zone payload. For more information, see the example payload in the [API docs](/apidocs/context-based-restrictions#create-zone).
{: tip}

Example payload to add {{site.data.keyword.openshiftlong_notm}} to a network zone. The `serviceRef` attribute for {{site.data.keyword.openshiftlong_notm}} is `containers-kubernetes`.

```json
{
  "name": "Example zone 1",
  "description": "",
  "addresses": [
    {
      "type": "serviceRef",
      "ref": {
        "service_name": "containers-kubernetes",
        "account_id": "ACCOUNT-ID"
      }
    }
  ]
}
```
{: codeblock}


Example payload to add multiple services, IP addresses, and VPCs to a network zone.

```json
{
  "name": "zone",
  "description": "",
  "addresses": [
    {
      "type": "ipAddress",
      "value": "192.168.0.0"
    },
    {
      "type": "vpc",
      "value": "crn:v1:bluemix:public:is:us-east:a/CRN"
    },
    {
      "type": "vpc",
      "value": "crn:v1:bluemix:public:is:us-south:a/CRN"
    },
    {
      "type": "serviceRef",
      "ref": {
        "service_name": "cloud-object-storage",
        "account_id": "ACCOUNT-ID"
      }
    },
    {
      "type": "serviceRef",
      "ref": {
        "service_name": "codeengine",
        "account_id": "ACCOUNT-ID"
      }
    },
    {
      "type": "serviceRef",
      "ref": {
        "service_name": "containers-kubernetes",
        "account_id": "ACCOUNT-ID"
      }
    },
    {
      "type": "serviceRef",
      "ref": {
        "service_type": "platform_service",
        "account_id": "ACCOUNT-ID"
      }
    },
    {
      "type": "serviceRef",
      "ref": {
        "service_name": "iam-groups",
        "account_id": "ACCOUNT-ID"
      }
    }
  ],
  "excluded": []
}
```
{: codeblock}

### Creating network zones from the CLI
{: #create-network-zone-cli}
{: cli}

1. To create network zones from the CLI, [install the CBR CLI plug-in](/docs/account?topic=cli-cbr-plugin#install-cbr-plugin). 
1. You can use the `cbr-zone-create` command to add resources to network zones. For more information, see the CBR [CLI reference](/docs/account?topic=cli-cbr-plugin#cbr-zones-cli). Note that the `service_name` for {{site.data.keyword.openshiftlong_notm}} is `containers-kubernetes`.
    
    To find a list of available service refs, run the `ibmcloud cbr service-ref-targets` [command](/docs/account?topic=cli-cbr-plugin#cbr-cli-service-ref-targets-command).
    {: tip}
    
    Example command to add the `containers-kubernetes` service to a network zone.
    
    ```sh
    ibmcloud cbr zone-create --name example-zone-1 --description "Example zone 1" --service-ref service_name=containers-kubernetes
    ```
    {: pre}
    
    
    The following example creates a network zone to allow a single public IP address to access. You can also use this example in conjunction with the [one IP example rule](#one-ip). For more information about this scenario, see [Setting up context-based restrictions](/docs/containers?topic=containers-cbr-tutorial).
    
    ```sh
    ibmcloud cbr zone-create --addresses 129.41.86.7 --description "Allow only client IP" --name allow-client-ip
    ```
    {: pre}
    


## Creating rules
{: #create-cbr-rule-openshift}

Define rules to protect access to resources in your account. The contexts that you define in your rules determine how the resources in your network zones (allowlists) can interact with the resources defined in the rule.

Review the [limitations](#cbr-limitations) before you create rules.
{: note}

### Creating rules by using the API
{: #create-cbr-rule-api}
{: api}

Review the following example requests to create rules. For more information about the `v1/rules` API, see the [API docs](/apidocs/context-based-restrictions#create-rule).

After you create a rule, it might take up to 10 minutes to before you can update that rule due to IAM TTL response caching.
{: note}

The following example payload creates a rule that protects the `CLUSTER-ID` cluster. Only resources in the `NETWORK-ZONE-ID` zone can access the cluster. Since no `operations` are specified, resources in the `NETWORK-ZONE-ID` zone can access both the `cluster` and `management` APIs.

```sh
{
  "description": "Example rule 1",
  "resources": [
    {
      "attributes": [
        {
          "name": "accountId",
          "value": "ACCOUNT-ID"
        },
        {
          "name": "serviceName",
          "value": "containers-kubernetes"
        },
        {
          "name": "serviceInstance",
          "value": "CLUSTER-ID"
        }
      ]
    }
  ],
  "contexts": [
    {
      "attributes": [
        {
          "name": "networkZoneId",
          "value": "NETWORK-ZONE-ID"
        },
        {
          "name": "endpointType",
          "value": "private"
        }
      ]
    }
  ]
}
```
{: codeblock}

The following example payload creates a rule that protects the `CLUSTER-ID` cluster. Only the resources defined in the `NETWORK-ZONE-ID` zone can access the cluster. Since the `cluster` API type is specified, resources in the `NETWORK-ZONE-ID` zone can access the cluster only through the cluster APIs over the private network.

```sh
{
  "description": "Example rule 2",
  "resources": [
    {
      "attributes": [
        {
          "name": "accountId",
          "value": "ACCOUNT-ID"
        },
        {
          "name": "serviceName",
          "value": "containers-kubernetes"
        },
        {
          "name": "serviceInstance",
          "value": "CLUSTER-ID"
        }
      ]
    }
  ],
  "operations": {
    "api_types": [
      {
        "api_type_id": "crn:v1:bluemix:public:containers-kubernetes::::api-type:cluster"
      }
    ]
  },
  "contexts": [
    {
      "attributes": [
        {
          "name": "networkZoneId",
          "value": "NETWORK-ZONE-ID"
        },
        {
          "name": "endpointType",
          "value": "private"
        }
      ]
    }
  ]
}
```
{: codeblock}


### Creating rules from the CLI
{: #create-cbr-rule-cli}
{: cli}

1. To create rules from the CLI, [install the CBR CLI plug-in](/docs/account?topic=cli-cbr-plugin#install-cbr-plugin). 
1. You can use the `ibmcloud cbr rule-create` [command](/docs/account?topic=cli-cbr-plugin#cbr-cli-rule-create-command) to create CBR rules. For more information, see the CBR [CLI reference](/docs/account?topic=cli-cbr-plugin#cbr-zones-cli). Note that the `service_name` for {{site.data.keyword.openshiftlong_notm}} is `containers-kubernetes`. To find a list of service names, run the `ibmcloud cbr service-ref-targets` command. To find a list of API types for a service, run the `ibmcloud cbr api-types --service-name SERVICE` command.

Example command to create a rule that uses the `addresses` key and the `cluster` API type and the `ipAddress` type.

```sh
ibmcloud cbr rule-create my-rule-1 --service-name containers-kubernetes --api-type crn:v1:bluemix:public:containers-kubernetes::::api-type:cluster --zone-id ZONE-ID
```
{: pre}

The following command creates a rule that protects the `CLUSTER-ID` cluster. Only resources in the `NETWORK-ZONE-ID` network zone can access the cluster. This rule includes both the `cluster` and `management` API types.

```sh
ibmcloud cbr rule-create my-rule-2 --service-name containers-kubernetes --service-instance CLUSTER-ID --zone-id NETWORK-ZONE-ID 
```
{: pre}

The following example command creates a rule that allows all private network connections, but allows only resources in the `allow-client-ip` network zone to connect to the cluster over the public network. For more information about this scenario, see [Setting up context-based restrictions](/docs/containers?topic=containers-cbr-tutorial).{: #one-ip}

```sh
ibmcloud cbr rule-create --api-types crn:v1:bluemix:public:containers-kubernetes::::api-type:cluster --description "privateAccess=allowAll, publicAccess=oneIP" --service-name containers-kubernetes --service-instance CLUSTER-ID --context-attributes endpointType=private --context-attributes endpointType=public,networkZoneId=allow-client-ip
```
{: pre}




## Limitations
{: #cbr-limitations}

- After you create a rule, it might take up to 10 minutes for the rule to take effect.
- {{site.data.keyword.openshiftlong_notm}} CBR rules that apply to all API types or the `cluster` API types must not reference network zones that contain IPv6 addresses. The APIs included in the `cluster` type don't support IPv6.
- If you add {{site.data.keyword.openshiftlong_notm}} resources to private-only network zones, the APIs for getting and listing clusters are still accessible over the public network.
- {{site.data.keyword.openshiftlong_notm}} CBR rules that apply to all API types or the cluster API types must not reference other services like {{site.data.keyword.cos_full_notm}} or {{site.data.keyword.keymanagementserviceshort}}
- {{site.data.keyword.openshiftlong_notm}} CBR rules that apply to all API types or the cluster API type do not support `Report-only` enforcement for the cluster API type.
- {{site.data.keyword.openshiftlong_notm}} CBR rules that apply to all API types or the cluster API types are limited to no more than 20 IPs/subnets for private rules, and 200 IPs/subnets for public rules. These limits are expected to increase after the backend scalability of our implementation of Red Hat OpenShift on IBM Cloud CBR is updated.
- {{site.data.keyword.openshiftlong_notm}} public CBR rules that apply to the cluster API type do not effect clusters that are private service endpoint only. All public traffic to the cluster APIserver is blocked. To use public CBR rules to control access to your cluster, update your cluster to enable public service endpoint
- Due to a limitation that is currently being addressed, when you create a single private CBR rule that applies to the cluster API type and specifies a single, empty network zone, the rule does not block the private service endpoint completely. Instead, the cluster is treated as if there are no CBR rules and allows all traffic. Until this limitation is resolved, you must create a private CBR rule with at least one IP, for example, `1.1.1.1/32`, or another IP that you control.
- Some {{site.data.keyword.openshiftlong_notm}} clusters that were created before 8/10/22 are not able to enforce public CBR rules for the cluster's APIserver. To check if your cluster supports these public cluster API type CBR rules, run the `ibmcloud ks cluster get -c <CLUSTER-ID>` command. If either of the Service Endpoint URLs starts with the `https://cXXX` (where XXX is any three digit number), then the cluster does support public CBR rules. If the Service Endpoint URLs starts with `https://cX` (where the number after the `c` is a single digit), then the cluster is not able to enforce public CBR rules for the cluster's APIserver. In order to use public CBR rules, you must create a new cluster.



