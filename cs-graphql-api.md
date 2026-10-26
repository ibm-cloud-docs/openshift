---
copyright:
  years: 2026
lastupdated: "2026-10-26"

keywords: containers, kubernetes, satellite, graphql, api, reference

subcollection: openshift
---

{{site.data.keyword.attribute-definition-list}}

# IBM Cloud Kubernetes Service GraphQL API reference
{: #cs-graphql-api}

The {{site.data.keyword.containerlong_notm}} GraphQL API is available at `https://containers.cloud.ibm.com/graphql`. Use this API to manage Satellite Connectors, Kubernetes clusters, and bare metal worker nodes programmatically.
{: shortdesc}

This page is auto-generated from the live schema.


## Queries
{: #queries}

Queries retrieve data without modifying any resources. Send a `POST` request to `https://containers.cloud.ibm.com/graphql` with your query in the request body.


### `node`
{: #node}

Find a Node for the given ID. Use fragments to select additional fields.
{: shortdesc}

| Type | Name | Description |
| --- | --- | --- |
| Returns | `Node` | |
| Argument | `id` (`ID!`) *(required)* | The Node's ID to find. |
{: caption="Returns and arguments for node" caption-side="bottom"}


#### Example request
{: #example-request-node}

```sh
curl -X POST https://containers.cloud.ibm.com/graphql \
  -H "Authorization: Bearer $IAM_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
  "query": "query node($id: ID!) {\n  node(id: $id) {\n    # ... select your fields here\n  }\n}",
  "variables": {
    "id": "abc123"
  }
}'
```


#### Example response
{: #example-response-node}

```json
{
  "data": {
    "node": "<Node>"
  }
}
```


### `satelliteConnectors`
{: #satelliteconnectors}

List the Satellite Connectors you have access to.
{: shortdesc}

| Type | Name | Description |
| --- | --- | --- |
| Returns | `SatelliteConnectorConnection` | |
| Argument | `after` (`String`) | Return Satellite Connectors after this cursor. |
| Argument | `first` (`Int`) | Return the first N Satellite Connectors. |
| Argument | `last` (`Int`) | Return the last N Satellite Connectors. |
| Argument | `before` (`String`) | Return Satellite Connectors before this cursor. |
{: caption="Returns and arguments for satelliteConnectors" caption-side="bottom"}


#### Example request
{: #example-request-satelliteconnectors}

```sh
curl -X POST https://containers.cloud.ibm.com/graphql \
  -H "Authorization: Bearer $IAM_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
  "query": "query satelliteConnectors($after: String, $first: Int, $last: Int, $before: String) {\n  satelliteConnectors(after: $after, first: $first, last: $last, before: $before) {\n    # ... select your fields here\n  }\n}",
  "variables": {
    "after": "example-value",
    "first": 0,
    "last": 0,
    "before": "example-value"
  }
}'
```


#### Example response
{: #example-response-satelliteconnectors}

```json
{
  "data": {
    "satelliteConnectors": {
      "edges": [
        {
          "cursor": "example-value",
          "node": {
            "createdDate": "2025-01-01T00:00:00Z",
            "crn": "<CloudResourceName>",
            "id": "abc123",
            "name": "example-value",
            "region": {
              "displayName": "...",
              "id": "...",
              "name": "..."
            },
            "resourceGroup": {
              "externalID": "...",
              "id": "...",
              "name": "..."
            },
            "state": "CREATED"
          }
        }
      ],
      "pageInfo": {
        "endCursor": "example-value",
        "hasNextPage": true,
        "hasPreviousPage": true,
        "startCursor": "example-value"
      }
    }
  }
}
```


## Mutations
{: #mutations}

Mutations create, update, or delete resources. Each mutation requires an IAM bearer token in the `Authorization` header.


### `addVirtualNetworkInterfaceToBareMetalNode`
{: #addvirtualnetworkinterfacetobaremetalnode}

Adds a virtual network interface (VNI) to a bare metal Kubernetes worker node.
{: shortdesc}

| Type | Name | Description |
| --- | --- | --- |
| Returns | `AddVirtualNetworkInterfaceToBareMetalNodePayload` | |
| Argument | `input` (`AddVirtualNetworkInterfaceToBareMetalNodeInput!`) *(required)* | Input parameters for adding the VNI to a bare metal node. |
{: caption="Returns and arguments for addVirtualNetworkInterfaceToBareMetalNode" caption-side="bottom"}


#### Example request
{: #example-request-addvirtualnetworkinterfacetobaremetalnode}

```sh
curl -X POST https://containers.cloud.ibm.com/graphql \
  -H "Authorization: Bearer $IAM_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
  "query": "mutation addVirtualNetworkInterfaceToBareMetalNode($input: AddVirtualNetworkInterfaceToBareMetalNodeInput!) {\n  addVirtualNetworkInterfaceToBareMetalNode(input: $input) {\n    # ... select your fields here\n  }\n}",
  "variables": {
    "input": "<AddVirtualNetworkInterfaceToBareMetalNodeInput>"
  }
}'
```


#### Example response
{: #example-response-addvirtualnetworkinterfacetobaremetalnode}

```json
{
  "data": {
    "addVirtualNetworkInterfaceToBareMetalNode": {
      "networkAttachment": "<NetworkAttachment>"
    }
  }
}
```


### `createKubernetesWorkloadMigrationPlan`
{: #createkubernetesworkloadmigrationplan}

Create a workload migration plan for classic cluster.
{: shortdesc}

| Type | Name | Description |
| --- | --- | --- |
| Returns | `CreateKubernetesWorkloadMigrationPlanPayload` | |
| Argument | `input` (`CreateKubernetesWorkloadMigrationPlanInput!`) *(required)* |  |
{: caption="Returns and arguments for createKubernetesWorkloadMigrationPlan" caption-side="bottom"}


#### Example request
{: #example-request-createkubernetesworkloadmigrationplan}

```sh
curl -X POST https://containers.cloud.ibm.com/graphql \
  -H "Authorization: Bearer $IAM_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
  "query": "mutation createKubernetesWorkloadMigrationPlan($input: CreateKubernetesWorkloadMigrationPlanInput!) {\n  createKubernetesWorkloadMigrationPlan(input: $input) {\n    # ... select your fields here\n  }\n}",
  "variables": {
    "input": "<CreateKubernetesWorkloadMigrationPlanInput>"
  }
}'
```


#### Example response
{: #example-response-createkubernetesworkloadmigrationplan}

```json
{
  "data": {
    "createKubernetesWorkloadMigrationPlan": {
      "clusterID": "example-value",
      "message": "example-value",
      "planID": "example-value",
      "regionName": "example-value"
    }
  }
}
```


### `createSatelliteConnector`
{: #createsatelliteconnector}

Create a Satellite Connector.
{: shortdesc}

| Type | Name | Description |
| --- | --- | --- |
| Returns | `CreateSatelliteConnectorPayload` | |
| Argument | `input` (`CreateSatelliteConnectorInput`) |  |
{: caption="Returns and arguments for createSatelliteConnector" caption-side="bottom"}


#### Example request
{: #example-request-createsatelliteconnector}

```sh
curl -X POST https://containers.cloud.ibm.com/graphql \
  -H "Authorization: Bearer $IAM_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
  "query": "mutation createSatelliteConnector($input: CreateSatelliteConnectorInput) {\n  createSatelliteConnector(input: $input) {\n    # ... select your fields here\n  }\n}",
  "variables": {
    "input": "<CreateSatelliteConnectorInput>"
  }
}'
```


#### Example response
{: #example-response-createsatelliteconnector}

```json
{
  "data": {
    "createSatelliteConnector": {
      "satelliteConnector": {
        "createdDate": "2025-01-01T00:00:00Z",
        "crn": "<CloudResourceName>",
        "id": "abc123",
        "name": "example-value",
        "region": {
          "displayName": "example-value",
          "id": "abc123",
          "name": "example-value"
        },
        "resourceGroup": {
          "externalID": "example-value",
          "id": "abc123",
          "name": "example-value"
        },
        "state": "CREATED"
      }
    }
  }
}
```


### `createVPCKubernetesClusterFromTemplate`
{: #createvpckubernetesclusterfromtemplate}

Create a VPC cluster from a classic cluster.
{: shortdesc}

| Type | Name | Description |
| --- | --- | --- |
| Returns | `CreateVPCKubernetesClusterFromTemplatePayload` | |
| Argument | `input` (`CreateVPCKubernetesClusterFromTemplateInput!`) *(required)* |  |
{: caption="Returns and arguments for createVPCKubernetesClusterFromTemplate" caption-side="bottom"}


#### Example request
{: #example-request-createvpckubernetesclusterfromtemplate}

```sh
curl -X POST https://containers.cloud.ibm.com/graphql \
  -H "Authorization: Bearer $IAM_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
  "query": "mutation createVPCKubernetesClusterFromTemplate($input: CreateVPCKubernetesClusterFromTemplateInput!) {\n  createVPCKubernetesClusterFromTemplate(input: $input) {\n    # ... select your fields here\n  }\n}",
  "variables": {
    "input": "<CreateVPCKubernetesClusterFromTemplateInput>"
  }
}'
```


#### Example response
{: #example-response-createvpckubernetesclusterfromtemplate}

```json
{
  "data": {
    "createVPCKubernetesClusterFromTemplate": {
      "classicClusterID": "example-value",
      "message": "example-value",
      "regionName": "example-value"
    }
  }
}
```


### `createVPCKubernetesClusterTemplate`
{: #createvpckubernetesclustertemplate}

Generate VPC meta data
{: shortdesc}

| Type | Name | Description |
| --- | --- | --- |
| Returns | `CreateVPCKubernetesClusterTemplatePayload` | |
| Argument | `input` (`CreateVPCKubernetesClusterTemplateInput!`) *(required)* |  |
{: caption="Returns and arguments for createVPCKubernetesClusterTemplate" caption-side="bottom"}


#### Example request
{: #example-request-createvpckubernetesclustertemplate}

```sh
curl -X POST https://containers.cloud.ibm.com/graphql \
  -H "Authorization: Bearer $IAM_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
  "query": "mutation createVPCKubernetesClusterTemplate($input: CreateVPCKubernetesClusterTemplateInput!) {\n  createVPCKubernetesClusterTemplate(input: $input) {\n    # ... select your fields here\n  }\n}",
  "variables": {
    "input": "<CreateVPCKubernetesClusterTemplateInput>"
  }
}'
```


#### Example response
{: #example-response-createvpckubernetesclustertemplate}

```json
{
  "data": {
    "createVPCKubernetesClusterTemplate": {
      "classic": {
        "addOns": [
          "<?>"
        ],
        "controlPlaneVersion": "example-value",
        "createdDate": "example-value",
        "crn": "example-value",
        "dataCenterName": "example-value",
        "id": "abc123",
        "name": "example-value",
        "nodeCount": 0,
        "nodePools": [
          "<?>"
        ],
        "regionName": "example-value",
        "resourceGroupID": "example-value",
        "resourceGroupName": "example-value",
        "serviceEndpoints": {
          "privateServiceEndpointEnabled": true,
          "publicServiceEndpointEnabled": true
        }
      },
      "vpc": {
        "addOns": [
          "<?>"
        ],
        "allZoneNames": [
          "<?>"
        ],
        "controlPlaneVersion": "example-value",
        "cosInstance": "example-value",
        "defaultNodePoolEntitlement": "example-value",
        "disablePublicServiceEndpoint": true,
        "keyManagementService": {
          "actualInstances": [
            "<?>"
          ],
          "actualRootKeyIDs": [
            "<?>"
          ],
          "desiredInstance": "example-value",
          "desiredRootKeyID": "example-value"
        },
        "name": "example-value",
        "nodePools": [
          "<?>"
        ],
        "offeringName": "example-value",
        "podSubnetCIDR": "example-value",
        "regionName": "example-value",
        "resourceGroupID": "example-value",
        "serviceSubnetCIDR": "example-value",
        "vpcID": "example-value"
      }
    }
  }
}
```


### `reinitializeKubernetesNode`
{: #reinitializekubernetesnode}

Reinitialize a Kubernetes node. Not supported on VPC virtual server instances today.
{: shortdesc}

| Type | Name | Description |
| --- | --- | --- |
| Returns | `ReinitializeKubernetesNodePayload` | |
| Argument | `input` (`ReinitializeKubernetesNodeInput`) |  |
{: caption="Returns and arguments for reinitializeKubernetesNode" caption-side="bottom"}


#### Example request
{: #example-request-reinitializekubernetesnode}

```sh
curl -X POST https://containers.cloud.ibm.com/graphql \
  -H "Authorization: Bearer $IAM_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
  "query": "mutation reinitializeKubernetesNode($input: ReinitializeKubernetesNodeInput) {\n  reinitializeKubernetesNode(input: $input) {\n    # ... select your fields here\n  }\n}",
  "variables": {
    "input": "<ReinitializeKubernetesNodeInput>"
  }
}'
```


#### Example response
{: #example-response-reinitializekubernetesnode}

```json
{
  "data": {
    "reinitializeKubernetesNode": {
      "node": "<KubernetesNode>"
    }
  }
}
```


### `removeSatelliteConnector`
{: #removesatelliteconnector}

Remove a Satellite Connector.
{: shortdesc}

| Type | Name | Description |
| --- | --- | --- |
| Returns | `RemoveSatelliteConnectorPayload` | |
| Argument | `input` (`RemoveSatelliteConnectorInput`) |  |
{: caption="Returns and arguments for removeSatelliteConnector" caption-side="bottom"}


#### Example request
{: #example-request-removesatelliteconnector}

```sh
curl -X POST https://containers.cloud.ibm.com/graphql \
  -H "Authorization: Bearer $IAM_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
  "query": "mutation removeSatelliteConnector($input: RemoveSatelliteConnectorInput) {\n  removeSatelliteConnector(input: $input) {\n    # ... select your fields here\n  }\n}",
  "variables": {
    "input": "<RemoveSatelliteConnectorInput>"
  }
}'
```


#### Example response
{: #example-response-removesatelliteconnector}

```json
{
  "data": {
    "removeSatelliteConnector": {
      "satelliteConnector": {
        "createdDate": "2025-01-01T00:00:00Z",
        "crn": "<CloudResourceName>",
        "id": "abc123",
        "name": "example-value",
        "region": {
          "displayName": "example-value",
          "id": "abc123",
          "name": "example-value"
        },
        "resourceGroup": {
          "externalID": "example-value",
          "id": "abc123",
          "name": "example-value"
        },
        "state": "CREATED"
      }
    }
  }
}
```


### `removeVirtualNetworkInterfaceFromNode`
{: #removevirtualnetworkinterfacefromnode}

Removes a virtual network interface from a Kubernetes worker node.
{: shortdesc}

| Type | Name | Description |
| --- | --- | --- |
| Returns | `RemoveVirtualNetworkInterfaceFromNodePayload` | |
| Argument | `input` (`RemoveVirtualNetworkInterfaceFromNodeInput!`) *(required)* | Input parameters for removing the VNI from a node. |
{: caption="Returns and arguments for removeVirtualNetworkInterfaceFromNode" caption-side="bottom"}


#### Example request
{: #example-request-removevirtualnetworkinterfacefromnode}

```sh
curl -X POST https://containers.cloud.ibm.com/graphql \
  -H "Authorization: Bearer $IAM_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
  "query": "mutation removeVirtualNetworkInterfaceFromNode($input: RemoveVirtualNetworkInterfaceFromNodeInput!) {\n  removeVirtualNetworkInterfaceFromNode(input: $input) {\n    # ... select your fields here\n  }\n}",
  "variables": {
    "input": "<RemoveVirtualNetworkInterfaceFromNodeInput>"
  }
}'
```


#### Example response
{: #example-response-removevirtualnetworkinterfacefromnode}

```json
{
  "data": {
    "removeVirtualNetworkInterfaceFromNode": {
      "cluster": {
        "id": "abc123",
        "name": "example-value",
        "networkAttachments": {
          "edges": [
            {
              "cursor": "...",
              "node": "..."
            }
          ],
          "pageInfo": {
            "endCursor": "...",
            "hasNextPage": "...",
            "hasPreviousPage": "...",
            "startCursor": "..."
          }
        },
        "region": {
          "displayName": "example-value",
          "id": "abc123",
          "name": "example-value"
        },
        "vpcMigration": {
          "allNamespaces": {
            "edges": "...",
            "pageInfo": "..."
          },
          "classicClusterTemplate": {
            "addOns": "...",
            "controlPlaneVersion": "...",
            "createdDate": "...",
            "crn": "...",
            "dataCenterName": "...",
            "id": "...",
            "name": "...",
            "nodeCount": "...",
            "nodePools": "...",
            "regionName": "...",
            "resourceGroupID": "...",
            "resourceGroupName": "...",
            "serviceEndpoints": "..."
          },
          "status": {
            "addonMigrationStatus": "...",
            "clusterUpgradeStatus": "...",
            "globalResourcesMigrationStatus": "...",
            "policyMigrationStatus": "..."
          },
          "vpcClusterTemplate": {
            "addOns": "...",
            "allZoneNames": "...",
            "controlPlaneVersion": "...",
            "cosInstance": "...",
            "defaultNodePoolEntitlement": "...",
            "disablePublicServiceEndpoint": "...",
            "keyManagementService": "...",
            "name": "...",
            "nodePools": "...",
            "offeringName": "...",
            "podSubnetCIDR": "...",
            "regionName": "...",
            "resourceGroupID": "...",
            "serviceSubnetCIDR": "...",
            "vpcID": "..."
          },
          "workloadMigrationPlan": {
            "clusterID": "...",
            "createdAt": "...",
            "errorMessage": "...",
            "message": "...",
            "migrationPlanID": "...",
            "workloadPlanDetails": "..."
          },
          "workloadMigrationPlans": {
            "edges": "...",
            "pageInfo": "..."
          }
        }
      },
      "node": "<NetworkAttachable>",
      "virtualNetworkInterface": "<VirtualNetworkInterface>"
    }
  }
}
```


### `startKubernetesWorkloadMigration`
{: #startkubernetesworkloadmigration}

Start workload migration for a classic-to-VPC cluster pair using BRS.
{: shortdesc}

| Type | Name | Description |
| --- | --- | --- |
| Returns | `StartKubernetesWorkloadMigrationPayload` | |
| Argument | `input` (`StartKubernetesWorkloadMigrationInput!`) *(required)* |  |
{: caption="Returns and arguments for startKubernetesWorkloadMigration" caption-side="bottom"}


#### Example request
{: #example-request-startkubernetesworkloadmigration}

```sh
curl -X POST https://containers.cloud.ibm.com/graphql \
  -H "Authorization: Bearer $IAM_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
  "query": "mutation startKubernetesWorkloadMigration($input: StartKubernetesWorkloadMigrationInput!) {\n  startKubernetesWorkloadMigration(input: $input) {\n    # ... select your fields here\n  }\n}",
  "variables": {
    "input": "<StartKubernetesWorkloadMigrationInput>"
  }
}'
```


#### Example response
{: #example-response-startkubernetesworkloadmigration}

```json
{
  "data": {
    "startKubernetesWorkloadMigration": {
      "classicClusterID": "example-value",
      "message": "example-value",
      "migrationPlanID": "example-value",
      "regionName": "example-value"
    }
  }
}
```


### `updateSatelliteLocation`
{: #updatesatellitelocation}

Update a Satellite Location.
{: shortdesc}

| Type | Name | Description |
| --- | --- | --- |
| Returns | `UpdateSatelliteLocationPayload` | |
| Argument | `input` (`UpdateSatelliteLocationInput`) |  |
{: caption="Returns and arguments for updateSatelliteLocation" caption-side="bottom"}


#### Example request
{: #example-request-updatesatellitelocation}

```sh
curl -X POST https://containers.cloud.ibm.com/graphql \
  -H "Authorization: Bearer $IAM_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
  "query": "mutation updateSatelliteLocation($input: UpdateSatelliteLocationInput) {\n  updateSatelliteLocation(input: $input) {\n    # ... select your fields here\n  }\n}",
  "variables": {
    "input": "<UpdateSatelliteLocationInput>"
  }
}'
```


#### Example response
{: #example-response-updatesatellitelocation}

```json
{
  "data": {
    "updateSatelliteLocation": {
      "satelliteLocation": {
        "description": "example-value",
        "id": "abc123",
        "name": "example-value"
      }
    }
  }
}
```


## Object types
{: #object-types}

Object types represent the concrete resources and response payloads returned by the API.


### Account
{: #account}

An IBM Cloud account.
{: shortdesc}

| Type | Name | Description |
| --- | --- | --- |
| Field | `externalID` (`String!`) | The account's IBM Cloud ID. |
{: caption="Fields for Account" caption-side="bottom"}


### AddVirtualNetworkInterfaceToBareMetalNodePayload
{: #addvirtualnetworkinterfacetobaremetalnodepayload}

Response payload for adding a VNI to a bare metal node.
{: shortdesc}

| Type | Name | Description |
| --- | --- | --- |
| Field | `networkAttachment` (`NetworkAttachment!`) | The created network attachment with its properties. |
{: caption="Fields for AddVirtualNetworkInterfaceToBareMetalNodePayload" caption-side="bottom"}


### BareMetalNetworkAttachmentByVLAN
{: #baremetalnetworkattachmentbyvlan}

Network attachment for bare metal nodes using VLAN tagging.
{: shortdesc}

| Type | Name | Description |
| --- | --- | --- |
| Implements | `NetworkAttachment` | |
| Field | `attachedTo` (`NetworkAttachable!`) | The bare metal node this interface is attached to. |
| Field | `canFloat` (`Boolean!`) | Whether this attachment can float between nodes in the cluster. |
| Field | `virtualNetworkInterface` (`VirtualNetworkInterface!`) | The virtual network interface that is attached. |
| Field | `vlanID` (`Int`) | VLAN ID used for this attachment (2-500). Null if not yet assigned. |
{: caption="Fields for BareMetalNetworkAttachmentByVLAN" caption-side="bottom"}


### BareMetalVirtualNetworkInterface
{: #baremetalvirtualnetworkinterface}

Virtual network interface attached to a bare metal server.
{: shortdesc}

| Type | Name | Description |
| --- | --- | --- |
| Implements | `VirtualNetworkInterface` | |
| Field | `autoDelete` (`Boolean`) | Whether the VNI should be automatically deleted when detached. |
| Field | `externalID` (`String!`) | The VPC resource ID of this VNI. |
| Field | `macAddress` (`MACAddress`) | MAC address assigned to this network interface. |
| Field | `name` (`String`) | Human-readable name of the VNI. |
| Field | `primaryIPAddress` (`IPv4Address`) | Primary IPv4 address assigned to this network interface. |
| Field | `securityGroups` (`SecurityGroupConnection`) | Security groups applied to this network interface.  \n **Arguments for `securityGroups`**  \n * `after` (`String`) — Cursor to start fetching from. \n * `first` (`Int`) — Maximum number of items to return. |
| Field | `subnet` (`Subnet!`) | The VPC subnet this network interface is connected to. |
{: caption="Fields for BareMetalVirtualNetworkInterface" caption-side="bottom"}


### ClassicKubernetesClusterServiceEndpointsTemplate
{: #classickubernetesclusterserviceendpointstemplate}

Service endpoint configuration for a cluster.
{: shortdesc}

| Type | Name | Description |
| --- | --- | --- |
| Field | `privateServiceEndpointEnabled` (`Boolean!`) | Whether private service endpoint is enabled. |
| Field | `publicServiceEndpointEnabled` (`Boolean!`) | Whether public service endpoint is enabled. |
{: caption="Fields for ClassicKubernetesClusterServiceEndpointsTemplate" caption-side="bottom"}


### ClassicKubernetesClusterTemplate
{: #classickubernetesclustertemplate}

A Classic Kubernetes cluster.
{: shortdesc}

| Type | Name | Description |
| --- | --- | --- |
| Field | `addOns` (`[?]!`) | Cluster add-ons |
| Field | `controlPlaneVersion` (`String!`) | The Kubernetes version. |
| Field | `createdDate` (`String!`) | The date when this cluster was created. |
| Field | `crn` (`String!`) | Cluster CRN |
| Field | `dataCenterName` (`String!`) | Data center. |
| Field | `id` (`ID!`) | The cluster ID. |
| Field | `name` (`String!`) | The cluster name. |
| Field | `nodeCount` (`Int!`) | Number of workers |
| Field | `nodePools` (`[?]!`) | Worker pools in the classic cluster. |
| Field | `regionName` (`String!`) | The region the cluster is in. |
| Field | `resourceGroupID` (`String!`) | The resource group ID containing this cluster. |
| Field | `resourceGroupName` (`String!`) | The resource group name containing this cluster. |
| Field | `serviceEndpoints` (`ClassicKubernetesClusterServiceEndpointsTemplate!`) | Service endpoint configuration. |
{: caption="Fields for ClassicKubernetesClusterTemplate" caption-side="bottom"}


### ClassicKubernetesClusterVPCMigrationStatus
{: #classickubernetesclustervpcmigrationstatus}

Cluster migration status.
{: shortdesc}

| Type | Name | Description |
| --- | --- | --- |
| Field | `addonMigrationStatus` (`VPCMigrationComponentAddOnStatus!`) | Add-On migration status |
| Field | `clusterUpgradeStatus` (`VPCMigrationComponentClusterStatus!`) | Cluster upgrade status |
| Field | `globalResourcesMigrationStatus` (`VPCMigrationComponentGlobalResourcesStatus!`) | Global resources migration status |
| Field | `policyMigrationStatus` (`VPCMigrationComponentPolicyStatus!`) | Policy migration status |
{: caption="Fields for ClassicKubernetesClusterVPCMigrationStatus" caption-side="bottom"}


### ClassicKubernetesNamespaceTemplate
{: #classickubernetesnamespacetemplate}

Classic kubernetes namespace template
{: shortdesc}

| Type | Name | Description |
| --- | --- | --- |
| Field | `labels` (`[?]!`) | Kubernetes labels on the namespace. The UI can use these for sorting and filtering. |
| Field | `name` (`String!`) | Namespace name. |
| Field | `status` (`String!`) | Namespace phase (e.g. Active, Terminating). |
{: caption="Fields for ClassicKubernetesNamespaceTemplate" caption-side="bottom"}


### CreateKubernetesWorkloadMigrationPlanPayload
{: #createkubernetesworkloadmigrationplanpayload}

Response payload for creating a workload migration plan
{: shortdesc}

| Type | Name | Description |
| --- | --- | --- |
| Field | `clusterID` (`String!`) | The classic cluster ID. |
| Field | `message` (`String!`) | Success message. |
| Field | `planID` (`String!`) | The generated migration plan ID (UUID v4). |
| Field | `regionName` (`String!`) | The region of the cluster. |
{: caption="Fields for CreateKubernetesWorkloadMigrationPlanPayload" caption-side="bottom"}


### CreateSatelliteConnectorPayload
{: #createsatelliteconnectorpayload}

Output type for createSatelliteConnector.
{: shortdesc}

| Type | Name | Description |
| --- | --- | --- |
| Field | `satelliteConnector` (`SatelliteConnector`) | The new SatelliteConnector. |
{: caption="Fields for CreateSatelliteConnectorPayload" caption-side="bottom"}


### CreateVPCKubernetesClusterFromTemplatePayload
{: #createvpckubernetesclusterfromtemplatepayload}

| Type | Name | Description |
| --- | --- | --- |
| Field | `classicClusterID` (`String!`) | The classic cluster ID being migrated. |
| Field | `message` (`String!`) | Success or status message. |
| Field | `regionName` (`String!`) | The region where the cluster is being created. |
{: caption="Fields for CreateVPCKubernetesClusterFromTemplatePayload" caption-side="bottom"}


### CreateVPCKubernetesClusterTemplatePayload
{: #createvpckubernetesclustertemplatepayload}

Generate VPC meta data mutation response payload
{: shortdesc}

| Type | Name | Description |
| --- | --- | --- |
| Field | `classic` (`ClassicKubernetesClusterTemplate!`) | Classic cluster meta data |
| Field | `vpc` (`VPCKubernetesClusterTemplate!`) | VPC meta data |
{: caption="Fields for CreateVPCKubernetesClusterTemplatePayload" caption-side="bottom"}


### KeyValuePair
{: #keyvaluepair}

| Type | Name | Description |
| --- | --- | --- |
| Field | `key` (`String!`) |  |
| Field | `value` (`String!`) |  |
{: caption="Fields for KeyValuePair" caption-side="bottom"}


### KubernetesCluster
{: #kubernetescluster}

An IBM Cloud Kubernetes Service or IBM Cloud OpenShift Service cluster.
{: shortdesc}

| Type | Name | Description |
| --- | --- | --- |
| Implements | `Node` | |
| Field | `id` (`ID!`) | The cluster's unique identifier. |
| Field | `name` (`String`) | The cluster's name. |
| Field | `networkAttachments` (`NetworkAttachmentConnection`) | Network attachments for this cluster (if applicable).  \n **Arguments for `networkAttachments`**  \n * `after` (`String`) — Cursor to start fetching from. \n * `first` (`Int`) — Maximum number of items to return. |
| Field | `region` (`Region`) | The cluster's IBM Cloud catalog region. |
| Field | `vpcMigration` (`KubernetesClusterVPCMigration`) | VPC Migration |
{: caption="Fields for KubernetesCluster" caption-side="bottom"}


### KubernetesClusterAddOnTemplate
{: #kubernetesclusteraddontemplate}

Cluster Add-On
{: shortdesc}

| Type | Name | Description |
| --- | --- | --- |
| Field | `name` (`String!`) | Add-on name |
| Field | `version` (`String!`) | Add-on version |
{: caption="Fields for KubernetesClusterAddOnTemplate" caption-side="bottom"}


### KubernetesClusterKeyManagementTemplate
{: #kubernetesclusterkeymanagementtemplate}

Key management service for the cluster
{: shortdesc}

| Type | Name | Description |
| --- | --- | --- |
| Field | `actualInstances` (`[?]!`) | Actual instsance CRN |
| Field | `actualRootKeyIDs` (`[?]!`) | Actual root key ID |
| Field | `desiredInstance` (`String!`) | Desired instance CRN |
| Field | `desiredRootKeyID` (`String!`) | Desired root key ID |
{: caption="Fields for KubernetesClusterKeyManagementTemplate" caption-side="bottom"}


### KubernetesClusterVPCMigration
{: #kubernetesclustervpcmigration}

VPC Migration
{: shortdesc}

| Type | Name | Description |
| --- | --- | --- |
| Field | `allNamespaces` (`ClassicKubernetesNamespaceTemplateConnection!`) | List all namespaces on the classic cluster.  \n **Arguments for `allNamespaces`**  \n * `after` (`String`) — Return namespaces after this cursor. \n * `first` (`Int`) — Return the first N namespaces. \n * `last` (`Int`) — Return the last N namespaces. \n * `before` (`String`) — Return namespaces before this cursor. |
| Field | `classicClusterTemplate` (`ClassicKubernetesClusterTemplate!`) | Classic cluster meta data |
| Field | `status` (`ClassicKubernetesClusterVPCMigrationStatus`) | Cluster Migration Status |
| Field | `vpcClusterTemplate` (`VPCKubernetesClusterTemplate!`) | VPC meta data |
| Field | `workloadMigrationPlan` (`KubernetesClusterVPCMigrationPlan`) | Get a workload migration plan by ID.  \n **Arguments for `workloadMigrationPlan`**  \n * `id` (`ID!`) *(required)* |
| Field | `workloadMigrationPlans` (`KubernetesWorkloadMigrationPlanConnection!`) | Returns a paginated list of workload migration plan summaries for this cluster.  \n **Arguments for `workloadMigrationPlans`**  \n * `after` (`String`) — Return plans after this cursor. \n * `first` (`Int`) — Return the first N plans. \n * `last` (`Int`) — Return the last N plans. \n * `before` (`String`) — Return plans before this cursor. |
{: caption="Fields for KubernetesClusterVPCMigration" caption-side="bottom"}


### KubernetesClusterVPCMigrationPlan
{: #kubernetesclustervpcmigrationplan}

Response payload for migrationPlan query.
{: shortdesc}

| Type | Name | Description |
| --- | --- | --- |
| Field | `clusterID` (`String!`) | The classic cluster ID. |
| Field | `createdAt` (`DateTime!`) | RFC3339 timestamp when the migration plan was created. |
| Field | `errorMessage` (`String!`) | Error message if the migration plan failed. Empty string when there is no error. |
| Field | `message` (`String!`) | Human-readable label for the status code (e.g. "migration plan completed"). |
| Field | `migrationPlanID` (`String!`) | The migration plan UUID. |
| Field | `workloadPlanDetails` (`KubernetesWorkloadMigrationPlanDetails`) | Full migration plan details. Null if plan.json is not yet in COS. |
{: caption="Fields for KubernetesClusterVPCMigrationPlan" caption-side="bottom"}


### KubernetesNodePoolTemplate
{: #kubernetesnodepooltemplate}

A worker pool in a classic cluster.
{: shortdesc}

| Type | Name | Description |
| --- | --- | --- |
| Field | `classicStorageSizeGigabytes` (`Int`) | Size in GB of the classic secondary storage. |
| Field | `entitlement` (`String`) | OpenShift license source for this worker pool (e.g. "cloud_pak", "worker_plan_ocp"). Empty for IKS clusters. |
| Field | `flavorName` (`String!`) | The machine type. |
| Field | `id` (`ID!`) | The worker pool ID. |
| Field | `name` (`String!`) | The worker pool name. |
| Field | `nodeLabels` (`[KeyValuePair!]`) | Labels assigned to worker nodes in this pool |
| Field | `operatingSystemName` (`String!`) | Operating system name |
| Field | `secondaryStorageOption` (`String`) | Selected VPC secondary storage option profile name (e.g. "300gb.5iops-tier"). Empty if the classic flavor had no secondary storage. |
| Field | `secondaryStorageSizeGigabytes` (`Int`) | Size in GB of the selected VPC secondary storage option. Zero if the classic flavor had no secondary storage. |
| Field | `sizePerZone` (`Int!`) | Number of workers per zone. |
| Field | `zoneNames` (`[?]!`) | Zones where workers are deployed. |
| Field | `zoneToSubnetIDMap` (`[KeyValuePair!]`) | Subnet IDs mapped by zone for this worker pool. Empty until createCluster is called. |
{: caption="Fields for KubernetesNodePoolTemplate" caption-side="bottom"}


### KubernetesWorkloadMigrationPlan
{: #kubernetesworkloadmigrationplan}

A single workload migration plan summary.
{: shortdesc}

| Type | Name | Description |
| --- | --- | --- |
| Field | `createdAt` (`DateTime!`) | RFC3339 timestamp when the migration plan was created. |
| Field | `message` (`String!`) | Human-readable label for the status code (e.g. "migration plan completed"). |
| Field | `namespaceNames` (`[?]!`) | Namespaces included in this migration plan. |
| Field | `planID` (`String!`) | The migration plan ID (UUID v4). |
{: caption="Fields for KubernetesWorkloadMigrationPlan" caption-side="bottom"}


### KubernetesWorkloadMigrationPlanDetails
{: #kubernetesworkloadmigrationplandetails}

Full workload migration plan details from COS plan.json.
{: shortdesc}

| Type | Name | Description |
| --- | --- | --- |
| Field | `backupRecoveryInstanceID` (`String`) | BRS instance ID associated with this migration plan. Null if not yet set. |
| Field | `namespaces` (`[?]!`) | Per-namespace resource details (alphabetical order). |
| Field | `storage` (`[?]!`) | ReplatformStorage migration details. |
| Field | `vpcStorageClassNames` (`[?]!`) | VPC storage classes present on the target VPC cluster. |
{: caption="Fields for KubernetesWorkloadMigrationPlanDetails" caption-side="bottom"}


### Region
{: #region}

An IBM Cloud catalog region.
{: shortdesc}

| Type | Name | Description |
| --- | --- | --- |
| Implements | `Location` | |
| Implements | `Node` | |
| Field | `displayName` (`String`) | The translated name of this region. |
| Field | `id` (`ID!`) | The ID of this region. |
| Field | `name` (`String`) | The name of this region. |
{: caption="Fields for Region" caption-side="bottom"}


### ReinitializeKubernetesNodePayload
{: #reinitializekubernetesnodepayload}

Output type for reinitializeKubernetesNode.
{: shortdesc}

| Type | Name | Description |
| --- | --- | --- |
| Field | `node` (`KubernetesNode`) | The reinitializing Kubernetes node. |
{: caption="Fields for ReinitializeKubernetesNodePayload" caption-side="bottom"}


### RemoveSatelliteConnectorPayload
{: #removesatelliteconnectorpayload}

Output type for removeSatelliteConnector.
{: shortdesc}

| Type | Name | Description |
| --- | --- | --- |
| Field | `satelliteConnector` (`SatelliteConnector`) | The removed SatelliteConnector. |
{: caption="Fields for RemoveSatelliteConnectorPayload" caption-side="bottom"}


### RemoveVirtualNetworkInterfaceFromNodePayload
{: #removevirtualnetworkinterfacefromnodepayload}

Response payload for removing a VNI from a node.
{: shortdesc}

| Type | Name | Description |
| --- | --- | --- |
| Field | `cluster` (`KubernetesCluster!`) | The cluster the VNI was removed from. |
| Field | `node` (`NetworkAttachable!`) | The node the VNI was removed from. |
| Field | `virtualNetworkInterface` (`VirtualNetworkInterface!`) | The virtual network interface that was removed. |
{: caption="Fields for RemoveVirtualNetworkInterfaceFromNodePayload" caption-side="bottom"}


### ResourceGroup
{: #resourcegroup}

A ResourceGroup is a way for you to organize your account resources in customizable groupings so that you can quickly assign users access to multiple resources at a time.
{: shortdesc}

| Type | Name | Description |
| --- | --- | --- |
| Implements | `Node` | |
| Field | `externalID` (`String!`) | The resource group's IBM Cloud ID. |
| Field | `id` (`ID!`) | The resource group's Node ID. |
| Field | `name` (`String`) | The resource group's name. |
{: caption="Fields for ResourceGroup" caption-side="bottom"}


### SatelliteConnector
{: #satelliteconnector}

A Satellite Connector provides a secure connection between a specific remote location and IBM Cloud.
{: shortdesc}

| Type | Name | Description |
| --- | --- | --- |
| Implements | `Node` | |
| Field | `createdDate` (`DateTime`) | The date when this resource was created. |
| Field | `crn` (`CloudResourceName`) | The resource's IBM Cloud CRN. |
| Field | `id` (`ID!`) | The resource's unique identifier. |
| Field | `name` (`String!`) | The resource's name. |
| Field | `region` (`Region`) | The region the resource is managed from. |
| Field | `resourceGroup` (`ResourceGroup`) | The resource group containing this resource. |
| Field | `state` (`SatelliteConnectorState`) | The current state of this resource. |
{: caption="Fields for SatelliteConnector" caption-side="bottom"}


### SatelliteLocation
{: #satellitelocation}

A Satellite Location.
{: shortdesc}

| Type | Name | Description |
| --- | --- | --- |
| Implements | `Node` | |
| Field | `description` (`String`) | The Location description. |
| Field | `id` (`ID!`) | The resource's unique identifier. |
| Field | `name` (`String`) | The Location name. |
{: caption="Fields for SatelliteLocation" caption-side="bottom"}


### SecurityGroup
{: #securitygroup}

Represents a VPC security group.
{: shortdesc}

| Type | Name | Description |
| --- | --- | --- |
| Field | `externalID` (`String!`) | The VPC resource ID of this security group. |
{: caption="Fields for SecurityGroup" caption-side="bottom"}


### StartKubernetesWorkloadMigrationPayload
{: #startkubernetesworkloadmigrationpayload}

Response payload for startKubernetesWorkloadMigration mutation.
{: shortdesc}

| Type | Name | Description |
| --- | --- | --- |
| Field | `classicClusterID` (`String!`) | The classic cluster ID. |
| Field | `message` (`String!`) | Human-readable success message. |
| Field | `migrationPlanID` (`String!`) | The migration plan ID. |
| Field | `regionName` (`String!`) | The region. |
{: caption="Fields for StartKubernetesWorkloadMigrationPayload" caption-side="bottom"}


### Subnet
{: #subnet}

Represents a VPC subnet.
{: shortdesc}

| Type | Name | Description |
| --- | --- | --- |
| Field | `externalID` (`String!`) | The VPC resource ID of this subnet. |
{: caption="Fields for Subnet" caption-side="bottom"}


### UpdateSatelliteLocationPayload
{: #updatesatellitelocationpayload}

Output type for updateSatelliteLocation.
{: shortdesc}

| Type | Name | Description |
| --- | --- | --- |
| Field | `satelliteLocation` (`SatelliteLocation`) | The updated SatelliteLocation. |
{: caption="Fields for UpdateSatelliteLocationPayload" caption-side="bottom"}


### VPCBareMetalKubernetesNode
{: #vpcbaremetalkubernetesnode}

Represents a bare metal Kubernetes worker node in IBM Cloud VPC.
{: shortdesc}

| Type | Name | Description |
| --- | --- | --- |
| Implements | `KubernetesNode` | |
| Implements | `NetworkAttachable` | |
| Implements | `Node` | |
| Field | `id` (`ID!`) | Globally unique identifier for this worker node. |
| Field | `networkAttachments` (`NetworkAttachmentConnection`) | Network attachments for this bare metal node.  \n **Arguments for `networkAttachments`**  \n * `after` (`String`) — Cursor to start fetching from. \n * `first` (`Int`) — Maximum number of items to return. |
| Field | `region` (`Region`) |  |
{: caption="Fields for VPCBareMetalKubernetesNode" caption-side="bottom"}


### VPCKubernetesClusterTemplate
{: #vpckubernetesclustertemplate}

| Type | Name | Description |
| --- | --- | --- |
| Field | `addOns` (`[?]!`) | Cluster add-ons |
| Field | `allZoneNames` (`[?]!`) | Worker zones |
| Field | `controlPlaneVersion` (`String!`) | Cluster version |
| Field | `cosInstance` (`String!`) | COS instance CRN |
| Field | `defaultNodePoolEntitlement` (`String!`) | Default worker pool entitlement |
| Field | `disablePublicServiceEndpoint` (`Boolean!`) | Disable public service endpoint |
| Field | `keyManagementService` (`KubernetesClusterKeyManagementTemplate`) | Key management service |
| Field | `name` (`String!`) | Name |
| Field | `nodePools` (`[?]!`) | Node (previously worker) pools with per-WP subnet IDs. |
| Field | `offeringName` (`String!`) | Cluster type |
| Field | `podSubnetCIDR` (`String!`) | Pod subnet |
| Field | `regionName` (`String!`) | Region |
| Field | `resourceGroupID` (`String!`) | Resource group |
| Field | `serviceSubnetCIDR` (`String!`) | Service subnet |
| Field | `vpcID` (`String!`) | VPC ID |
{: caption="Fields for VPCKubernetesClusterTemplate" caption-side="bottom"}


### VPCMigrationCalicoNetworkPolicy
{: #vpcmigrationcaliconetworkpolicy}

Calico network policy migration details.
{: shortdesc}

| Type | Name | Description |
| --- | --- | --- |
| Field | `name` (`String!`) |  |
| Field | `notes` (`[?]!`) |  |
{: caption="Fields for VPCMigrationCalicoNetworkPolicy" caption-side="bottom"}


### VPCMigrationComponentAddOnStatus
{: #vpcmigrationcomponentaddonstatus}

Add-on migration operation status
{: shortdesc}

| Type | Name | Description |
| --- | --- | --- |
| Field | `additionalDetails` (`[KeyValuePair!]`) | Additional details of the operation |
| Field | `errorMessage` (`String`) | Operation error message |
| Field | `message` (`String!`) | Operation status descriptive message |
{: caption="Fields for VPCMigrationComponentAddOnStatus" caption-side="bottom"}


### VPCMigrationComponentClusterStatus
{: #vpcmigrationcomponentclusterstatus}

Cluster migration operation status
{: shortdesc}

| Type | Name | Description |
| --- | --- | --- |
| Field | `additionalDetails` (`[KeyValuePair!]`) | Additional details of the operation |
| Field | `errorMessage` (`String`) | Operation error message |
| Field | `message` (`String!`) | Operation status descriptive message |
{: caption="Fields for VPCMigrationComponentClusterStatus" caption-side="bottom"}


### VPCMigrationComponentGlobalResourcesStatus
{: #vpcmigrationcomponentglobalresourcesstatus}

Global resources migration operation status
{: shortdesc}

| Type | Name | Description |
| --- | --- | --- |
| Field | `additionalDetails` (`[KeyValuePair!]`) | Additional details of the operation |
| Field | `errorMessage` (`String`) | Operation error message |
| Field | `message` (`String!`) | Operation status descriptive message |
{: caption="Fields for VPCMigrationComponentGlobalResourcesStatus" caption-side="bottom"}


### VPCMigrationComponentPolicyStatus
{: #vpcmigrationcomponentpolicystatus}

Policy migration operation status
{: shortdesc}

| Type | Name | Description |
| --- | --- | --- |
| Field | `additionalDetails` (`[KeyValuePair!]`) | Additional details of the operation |
| Field | `errorMessage` (`String`) | Operation error message |
| Field | `message` (`String!`) | Operation status descriptive message |
{: caption="Fields for VPCMigrationComponentPolicyStatus" caption-side="bottom"}


### VPCMigrationExternalName
{: #vpcmigrationexternalname}

External name details.
{: shortdesc}

| Type | Name | Description |
| --- | --- | --- |
| Field | `name` (`String!`) |  |
| Field | `notes` (`[?]!`) |  |
{: caption="Fields for VPCMigrationExternalName" caption-side="bottom"}


### VPCMigrationHost
{: #vpcmigrationhost}

ReplatformHost details with classic-to-VPC hostname mappings.
{: shortdesc}

| Type | Name | Description |
| --- | --- | --- |
| Field | `hostMappings` (`[?]!`) |  |
| Field | `type` (`String!`) |  |
{: caption="Fields for VPCMigrationHost" caption-side="bottom"}


### VPCMigrationHostMapping
{: #vpcmigrationhostmapping}

Classic-to-VPC hostname mapping.
{: shortdesc}

| Type | Name | Description |
| --- | --- | --- |
| Field | `classic` (`String!`) |  |
| Field | `vpc` (`String!`) |  |
{: caption="Fields for VPCMigrationHostMapping" caption-side="bottom"}


### VPCMigrationIngress
{: #vpcmigrationingress}

Ingress object migration details.
{: shortdesc}

| Type | Name | Description |
| --- | --- | --- |
| Field | `hosts` (`[?]!`) |  |
| Field | `name` (`String!`) |  |
| Field | `notes` (`[?]!`) |  |
{: caption="Fields for VPCMigrationIngress" caption-side="bottom"}


### VPCMigrationKubernetesNetworkPolicy
{: #vpcmigrationkubernetesnetworkpolicy}

Kubernetes network policy migration details.
{: shortdesc}

| Type | Name | Description |
| --- | --- | --- |
| Field | `name` (`String!`) |  |
| Field | `notes` (`[?]!`) |  |
{: caption="Fields for VPCMigrationKubernetesNetworkPolicy" caption-side="bottom"}


### VPCMigrationLoadBalancer
{: #vpcmigrationloadbalancer}

Load balancer migration details.
{: shortdesc}

| Type | Name | Description |
| --- | --- | --- |
| Field | `loadBalancerTypeMappings` (`[?]!`) |  |
| Field | `name` (`String!`) |  |
| Field | `notes` (`[?]!`) |  |
{: caption="Fields for VPCMigrationLoadBalancer" caption-side="bottom"}


### VPCMigrationLoadBalancerTypeMapping
{: #vpcmigrationloadbalancertypemapping}

Load balancer type mapping (classic → VPC).
{: shortdesc}

| Type | Name | Description |
| --- | --- | --- |
| Field | `classic` (`String!`) |  |
| Field | `vpc` (`String!`) |  |
{: caption="Fields for VPCMigrationLoadBalancerTypeMapping" caption-side="bottom"}


### VPCMigrationNamespaceDetails
{: #vpcmigrationnamespacedetails}

Resource details for a single namespace.
{: shortdesc}

| Type | Name | Description |
| --- | --- | --- |
| Field | `migrationStatus` (`VPCMigrationNamespaceStatus`) | Per-namespace workload migration status. Null when no migration has been run yet. |
| Field | `name` (`String!`) | Namespace name. |
| Field | `networking` (`VPCMigrationNamespaceNetworking!`) | Namespace networking details. |
{: caption="Fields for VPCMigrationNamespaceDetails" caption-side="bottom"}


### VPCMigrationNamespaceNetworking
{: #vpcmigrationnamespacenetworking}

ReplatformNetworking resources for a namespace.
vpclbObjectPath and vpcnodeportObjectPath are backend-only fields on model.Networking
and are intentionally excluded from this type.
{: shortdesc}

| Type | Name | Description |
| --- | --- | --- |
| Field | `calicoNetworkPolicies` (`[?]!`) |  |
| Field | `externalNames` (`[?]!`) |  |
| Field | `ingresses` (`[?]!`) |  |
| Field | `kubernetesNetworkPolicies` (`[?]!`) |  |
| Field | `loadBalancers` (`[?]!`) |  |
| Field | `nodePorts` (`[?]!`) |  |
| Field | `routes` (`[?]!`) |  |
{: caption="Fields for VPCMigrationNamespaceNetworking" caption-side="bottom"}


### VPCMigrationNamespaceStatus
{: #vpcmigrationnamespacestatus}

Per-namespace workload migration status.
{: shortdesc}

| Type | Name | Description |
| --- | --- | --- |
| Field | `message` (`String!`) | Human-readable status message. |
{: caption="Fields for VPCMigrationNamespaceStatus" caption-side="bottom"}


### VPCMigrationNodePort
{: #vpcmigrationnodeport}

ReplatformNodePort service migration details.
{: shortdesc}

| Type | Name | Description |
| --- | --- | --- |
| Field | `name` (`String!`) |  |
| Field | `notes` (`[?]!`) |  |
{: caption="Fields for VPCMigrationNodePort" caption-side="bottom"}


### VPCMigrationNote
{: #vpcmigrationnote}

ReplatformNote on a migration resource.
{: shortdesc}

| Type | Name | Description |
| --- | --- | --- |
| Field | `description` (`String!`) |  |
| Field | `isUserActionRequired` (`Boolean!`) |  |
| Field | `key` (`String!`) | Machine-readable identifier for the note type. |
{: caption="Fields for VPCMigrationNote" caption-side="bottom"}


### VPCMigrationRoute
{: #vpcmigrationroute}

Route object migration details.
{: shortdesc}

| Type | Name | Description |
| --- | --- | --- |
| Field | `host` (`VPCMigrationHost!`) |  |
| Field | `name` (`String!`) |  |
| Field | `notes` (`[?]!`) |  |
{: caption="Fields for VPCMigrationRoute" caption-side="bottom"}


### VPCMigrationStorage
{: #vpcmigrationstorage}

ReplatformStorage migration details.
{: shortdesc}

| Type | Name | Description |
| --- | --- | --- |
| Field | `name` (`String!`) |  |
| Field | `notes` (`[?]!`) |  |
| Field | `storageClassNameMappings` (`[?]!`) |  |
{: caption="Fields for VPCMigrationStorage" caption-side="bottom"}


### VPCMigrationStorageClassNameMapping
{: #vpcmigrationstorageclassnamemapping}

ReplatformStorage class name mapping (classic → VPC).
{: shortdesc}

| Type | Name | Description |
| --- | --- | --- |
| Field | `classic` (`String!`) |  |
| Field | `vpc` (`String!`) |  |
{: caption="Fields for VPCMigrationStorageClassNameMapping" caption-side="bottom"}


## Interface types
{: #interface-types}

Interface types define common fields that are shared across multiple concrete object types.


### KubernetesNode
{: #kubernetesnode}

A Kubernetes Node runs your workload.
{: shortdesc}

| Type | Name | Description |
| --- | --- | --- |
| Implementation | `KubernetesNode` | |
| Implementation | `VPCBareMetalKubernetesNode` | |
| Field | `id` (`ID!`) | The resource's unique identifier. |
| Field | `region` (`Region`) |  |
{: caption="Fields for KubernetesNode" caption-side="bottom"}


### Location
{: #location}

An IBM Cloud catalog location.
{: shortdesc}

| Type | Name | Description |
| --- | --- | --- |
| Implementation | `Location` | |
| Implementation | `Region` | |
| Field | `displayName` (`String`) | Translated name of this location. |
| Field | `id` (`ID!`) | The ID of this location. |
| Field | `name` (`String`) | Name of this location. |
{: caption="Fields for Location" caption-side="bottom"}


### NetworkAttachable
{: #networkattachable}

Represents an entity that can have network interfaces attached to it.
{: shortdesc}

| Type | Name | Description |
| --- | --- | --- |
| Implementation | `NetworkAttachable` | |
| Field | `id` (`ID!`) | Globally unique identifier for this node. |
| Field | `networkAttachments` (`NetworkAttachmentConnection`) | Network attachments associated to this node.  \n **Arguments for `networkAttachments`**  \n * `after` (`String`) — Cursor to start fetching from. \n * `first` (`Int`) — Maximum number of items to return. |
{: caption="Fields for NetworkAttachable" caption-side="bottom"}


### NetworkAttachment
{: #networkattachment}

Represents a network interface attachment to a node.
{: shortdesc}

| Type | Name | Description |
| --- | --- | --- |
| Implementation | `BareMetalNetworkAttachmentByVLAN` | |
| Implementation | `NetworkAttachment` | |
| Field | `attachedTo` (`NetworkAttachable!`) | The node this network interface is attached to. |
| Field | `virtualNetworkInterface` (`VirtualNetworkInterface!`) | The virtual network interface that is attached. |
{: caption="Fields for NetworkAttachment" caption-side="bottom"}


### Node
{: #node}

Fetches an object given its ID.
{: shortdesc}

| Type | Name | Description |
| --- | --- | --- |
| Implementation | `KubernetesCluster` | |
| Implementation | `KubernetesNode` | |
| Implementation | `NetworkAttachable` | |
| Implementation | `Node` | |
| Implementation | `Region` | |
| Implementation | `ResourceGroup` | |
| Implementation | `SatelliteConnector` | |
| Implementation | `SatelliteLocation` | |
| Implementation | `VPCBareMetalKubernetesNode` | |
| Field | `id` (`ID!`) | The globally unique object ID. |
{: caption="Fields for Node" caption-side="bottom"}


### VirtualNetworkInterface
{: #virtualnetworkinterface}

Represents a virtual network interface in IBM Cloud VPC.
Can be attached to bare metal or virtual server instances.
{: shortdesc}

| Type | Name | Description |
| --- | --- | --- |
| Implementation | `BareMetalVirtualNetworkInterface` | |
| Implementation | `VirtualNetworkInterface` | |
| Field | `autoDelete` (`Boolean`) | Whether the VNI should be automatically deleted when detached. |
| Field | `externalID` (`String!`) | The VPC resource ID of this virtual network interface. |
| Field | `macAddress` (`MACAddress`) | MAC address assigned to this network interface. |
| Field | `name` (`String`) | Human-readable name of the VNI. |
| Field | `primaryIPAddress` (`IPv4Address`) | Primary IPv4 address assigned to this network interface. |
| Field | `securityGroups` (`SecurityGroupConnection`) | Security groups applied to this network interface.  \n **Arguments for `securityGroups`**  \n * `after` (`String`) — Cursor to start fetching from. \n * `first` (`Int`) — Maximum number of items to return. |
| Field | `subnet` (`Subnet!`) | The VPC subnet this network interface is connected to. |
{: caption="Fields for VirtualNetworkInterface" caption-side="bottom"}


## Input types
{: #input-types}

Input types are used as arguments to mutations. Fields marked *(required)* must be provided.


### AddVirtualNetworkInterfaceToBareMetalNodeInput
{: #addvirtualnetworkinterfacetobaremetalnodeinput}

Input for adding a VNI to a bare metal node.
{: shortdesc}

| Type | Name | Description |
| --- | --- | --- |
| Field | `autoDelete` (`Boolean`) | Whether to automatically delete the VNI from VPC when it is detached. Defaults to false if not specified. |
| Field | `cluster` (`ID`) | Cluster ID. Either cluster or node must be specified, but not both. If only cluster is provided, a node will be auto-selected and the attachment will float. |
| Field | `node` (`ID`) | Node ID. Either cluster or node must be specified, but not both. If specified, creates a non-floating attachment to this specific node. |
| Field | `virtualNetworkInterfaceID` (`String!`) *(required)* | The VPC resource ID of the virtual network interface to attach. |
| Field | `vlanID` (`Int!`) *(required)* | VLAN ID for the attachment (2-500). VLAN 1 is reserved for the primary network interface. |
{: caption="Input fields for AddVirtualNetworkInterfaceToBareMetalNodeInput" caption-side="bottom"}


### CreateKubernetesWorkloadMigrationPlanInput
{: #createkubernetesworkloadmigrationplaninput}

Input for creating a workload migration plan
{: shortdesc}

| Type | Name | Description |
| --- | --- | --- |
| Field | `cluster` (`ID!`) *(required)* | The classic cluster ID. |
| Field | `namespaceNames` (`[?]!`) *(required)* | List of namespaces to include in the migration plan (max 20). |
{: caption="Input fields for CreateKubernetesWorkloadMigrationPlanInput" caption-side="bottom"}


### CreateSatelliteConnectorInput
{: #createsatelliteconnectorinput}

Details needed to provision a Satellite Connector.
{: shortdesc}

| Type | Name | Description |
| --- | --- | --- |
| Field | `name` (`String!`) *(required)* | The resource's name. |
| Field | `regionName` (`String!`) *(required)* | The region name indicating where the new connector should be managed from. |
| Field | `resourceGroupID` (`String!`) *(required)* | The resource group ID to provision inside. |
{: caption="Input fields for CreateSatelliteConnectorInput" caption-side="bottom"}


### CreateVPCKubernetesClusterFromTemplateInput
{: #createvpckubernetesclusterfromtemplateinput}

| Type | Name | Description |
| --- | --- | --- |
| Field | `cluster` (`ID!`) *(required)* | The classic cluster ID to migrate from. |
| Field | `nodePoolOverrides` (`[KubernetesNodePoolVPCMigrationOverride!]`) | Worker pool overrides (flavor and/or subnet IDs per worker pool). |
| Field | `skipBackupRecoveryServiceNodePool` (`Boolean`) | Disable the BRS workerpool. When true, the BRS workerpool is removed from vpc.json before cluster creation.  \n Default: `false` |
| Field | `vpcClusterName` (`String`) | Optional override for the VPC cluster name. When provided, this name is used instead of the auto-generated `mig-<classic-cluster-name>` value from ReplatformGenerateVPCMetadata. Must start with a lowercase letter, contain only lowercase letters, digits, and hyphens, end with a lowercase letter or digit, and be at most 32 characters. |
| Field | `vpcID` (`String`) | The VPC ID to use for the new cluster. |
{: caption="Input fields for CreateVPCKubernetesClusterFromTemplateInput" caption-side="bottom"}


### CreateVPCKubernetesClusterTemplateInput
{: #createvpckubernetesclustertemplateinput}

Generate VPC meta data input
{: shortdesc}

| Type | Name | Description |
| --- | --- | --- |
| Field | `cluster` (`ID!`) *(required)* | The cluster ID. |
| Field | `cosInstance` (`String!`) *(required)* | The COS instance CRN for storing metadata. |
{: caption="Input fields for CreateVPCKubernetesClusterTemplateInput" caption-side="bottom"}


### KeyValuePairInput
{: #keyvaluepairinput}

| Type | Name | Description |
| --- | --- | --- |
| Field | `key` (`String!`) *(required)* |  |
| Field | `value` (`String!`) *(required)* |  |
{: caption="Input fields for KeyValuePairInput" caption-side="bottom"}


### KubernetesNodePoolVPCMigrationOverride
{: #kubernetesnodepoolvpcmigrationoverride}

| Type | Name | Description |
| --- | --- | --- |
| Field | `flavorName` (`String`) | VPC flavor to use. Optional — omit to keep the existing flavor. When provided must be non-empty. |
| Field | `name` (`String!`) *(required)* | Worker pool name. Required. |
| Field | `zoneToSubnetIDMap` (`[KeyValuePairInput!]`) | Subnet IDs mapped by zone for this worker pool. Optional. Required for every worker pool override when vpcID is provided at the top level. Type: Map[String, String] Key: zone name (e.g., "us-south-1") Value: subnet ID (e.g., "0717-subnet-abc123") Example: [{"key": "us-south-1", "value": "subnet-abc"}, {"key": "us-south-2", "value": "subnet-def"}] |
{: caption="Input fields for KubernetesNodePoolVPCMigrationOverride" caption-side="bottom"}


### ReinitializeKubernetesNodeInput
{: #reinitializekubernetesnodeinput}

Input type for reinitializeKubernetesNode.
{: shortdesc}

| Type | Name | Description |
| --- | --- | --- |
| Field | `bypassUnhealthyControlPlane` (`Boolean`) | Set to true to proceed with reinitialization, even when the cluster's control plane is unhealthy. |
| Field | `id` (`ID!`) *(required)* | Kubernetes node to reinitialize. |
{: caption="Input fields for ReinitializeKubernetesNodeInput" caption-side="bottom"}


### RemoveSatelliteConnectorInput
{: #removesatelliteconnectorinput}

Input type for removeSatelliteConnector.
{: shortdesc}

| Type | Name | Description |
| --- | --- | --- |
| Field | `id` (`ID!`) *(required)* | Satellite Connector ID to remove. |
{: caption="Input fields for RemoveSatelliteConnectorInput" caption-side="bottom"}


### RemoveVirtualNetworkInterfaceFromNodeInput
{: #removevirtualnetworkinterfacefromnodeinput}

Input for removing a VNI from a node.
{: shortdesc}

| Type | Name | Description |
| --- | --- | --- |
| Field | `cluster` (`ID`) | Cluster ID. Either cluster or node must be specified, but not both. |
| Field | `node` (`ID`) | Node ID. Either cluster or node must be specified, but not both. |
| Field | `virtualNetworkInterfaceID` (`String!`) *(required)* | The VPC resource ID of the virtual network interface to remove. |
{: caption="Input fields for RemoveVirtualNetworkInterfaceFromNodeInput" caption-side="bottom"}


### StartKubernetesWorkloadMigrationInput
{: #startkubernetesworkloadmigrationinput}

Input for the startKubernetesWorkloadMigration mutation.
{: shortdesc}

| Type | Name | Description |
| --- | --- | --- |
| Field | `backupRecoveryInstanceID` (`String!`) *(required)* | IBM Cloud BRS (Backup & Recovery Service) instance ID. |
| Field | `cluster` (`ID!`) *(required)* | Classic (source) Kubernetes cluster ID. |
| Field | `migrationPlanID` (`String!`) *(required)* | Migration plan UUID produced by createKubernetesWorkloadMigrationPlan. |
| Field | `storageClassClassicToVPCMap` (`[KeyValuePairInput!]`) | ReplatformStorage class mapping from classic storage class names to VPC storage class names. An empty map is allowed — written as {} in the workload metadata. Example: {"key": "ibmc-block-gold", "value": "ibmc-vpc-block-10iops-tier"} |
{: caption="Input fields for StartKubernetesWorkloadMigrationInput" caption-side="bottom"}


### UpdateSatelliteLocationInput
{: #updatesatellitelocationinput}

Input type for updateSatelliteLocation.
{: shortdesc}

| Type | Name | Description |
| --- | --- | --- |
| Field | `description` (`String`) |  |
| Field | `id` (`ID!`) *(required)* | Satellite Location ID to update. |
| Field | `name` (`String`) |  |
{: caption="Input fields for UpdateSatelliteLocationInput" caption-side="bottom"}


## Enum types
{: #enum-types}

Enum types define the set of allowed string values for a field.


### SatelliteConnectorState
{: #satelliteconnectorstate}

The administrative state of a Satellite Connector.

The values are expected to expand in the future. When processing, check for and log unknown values. Optionally halt processing and surface the error, or bypass the Satellite Connector on which the unexpected value was encountered.
{: shortdesc}

| Type | Name | Description |
| --- | --- | --- |
| Value | `CREATED` | The connector has completed provisioning and is ready to use. |
| Value | `CREATING` | The connector is provisioning and may not be ready to use. |
| Value | `DELETING` | The connector is deprovisioning and may be unavailable. |
| Value | `FAILED` | The connector's most recent operation has failed and it must be deleted to continue. |
{: caption="Values for SatelliteConnectorState" caption-side="bottom"}


## Scalar types
{: #scalar-types}

Scalar types are primitive leaf values in the GraphQL schema.


### CloudResourceName
{: #cloudresourcename}

A Cloud Resource Name (CRN) uniquely identifies IBM Cloud resources.
{: shortdesc}


### DateTime
{: #datetime}

A DateTime is an RFC3339 compliant combination of a date and time.
{: shortdesc}


### IPv4Address
{: #ipv4address}

IPv4 address in dotted-decimal notation (e.g., xxx.xxx.xxx.xxx).
{: shortdesc}


### MACAddress
{: #macaddress}

MAC address in colon-hexadecimal notation (e.g., 00:1A:2B:3C:4D:5E).
{: shortdesc}


## Internal queries
{: #internal-queries}

The following queries are for internal use only and are not supported for external callers. They are documented here for completeness.


### `globalSearchSatelliteConnectorAccounts`
{: #globalsearchsatelliteconnectoraccounts}

Globally searchable results for the IBM Global Search service. Internal use only.
{: shortdesc}

| Type | Name | Description |
| --- | --- | --- |
| Returns | `GlobalSearchSatelliteConnectorAccountsConnection` | |
| Argument | `after` (`String`) |  |
| Argument | `first` (`Int`) |  |
| Argument | `last` (`Int`) |  |
| Argument | `before` (`String`) |  |
| Argument | `regionName` (`String!`) *(required)* |  |
{: caption="Returns and arguments for globalSearchSatelliteConnectorAccounts" caption-side="bottom"}


#### Example request
{: #example-request-globalsearchsatelliteconnectoraccounts}

```sh
curl -X POST https://containers.cloud.ibm.com/graphql \
  -H "Authorization: Bearer $IAM_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
  "query": "query globalSearchSatelliteConnectorAccounts($after: String, $first: Int, $last: Int, $before: String, $regionName: String!) {\n  globalSearchSatelliteConnectorAccounts(after: $after, first: $first, last: $last, before: $before, regionName: $regionName) {\n    # ... select your fields here\n  }\n}",
  "variables": {
    "after": "example-value",
    "first": 0,
    "last": 0,
    "before": "example-value",
    "regionName": "example-value"
  }
}'
```


#### Example response
{: #example-response-globalsearchsatelliteconnectoraccounts}

```json
{
  "data": {
    "globalSearchSatelliteConnectorAccounts": {
      "edges": [
        {
          "cursor": "example-value",
          "node": {
            "externalID": "example-value"
          }
        }
      ],
      "pageInfo": {
        "endCursor": "example-value",
        "hasNextPage": true,
        "hasPreviousPage": true,
        "startCursor": "example-value"
      }
    }
  }
}
```
