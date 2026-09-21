---
copyright:
  years: 2026
lastupdated: "2026-09-21"

keywords: containers, kubernetes, satellite, graphql, api, reference

subcollection: containers
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

Returns
:   `Node`

| Argument | Description |
| --- | --- |
| `id` (`ID!`) *(required)* | The globally unique node identifier. |
{: caption="Arguments for node" caption-side="bottom"}


#### Example request
{: #example-request-node}

```sh
curl -X POST https://containers.cloud.ibm.com/graphql \
  -H "Authorization: Bearer $IAM_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
  "query": "query node($id: ID!) {\n  node(id: $id) {\n    # \u2026 select your fields here\n  }\n}",
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

Returns
:   `SatelliteConnectorConnection`

| Argument | Description |
| --- | --- |
| `after` (`String`) | Return Satellite Connectors after this cursor. |
| `first` (`Int`) | Return the first N Satellite Connectors. |
| `last` (`Int`) | Return the last N Satellite Connectors. |
| `before` (`String`) | Return Satellite Connectors before this cursor. |
{: caption="Arguments for satelliteConnectors" caption-side="bottom"}


#### Example request
{: #example-request-satelliteconnectors}

```sh
curl -X POST https://containers.cloud.ibm.com/graphql \
  -H "Authorization: Bearer $IAM_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
  "query": "query satelliteConnectors($after: String, $first: Int, $last: Int, $before: String) {\n  satelliteConnectors(after: $after, first: $first, last: $last, before: $before) {\n    # \u2026 select your fields here\n  }\n}",
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

Returns
:   `AddVirtualNetworkInterfaceToBareMetalNodePayload`

| Argument | Description |
| --- | --- |
| `input` (`AddVirtualNetworkInterfaceToBareMetalNodeInput!`) *(required)* | Input parameters for adding the VNI to a bare metal node. |
{: caption="Arguments for addVirtualNetworkInterfaceToBareMetalNode" caption-side="bottom"}


#### Example request
{: #example-request-addvirtualnetworkinterfacetobaremetalnode}

```sh
curl -X POST https://containers.cloud.ibm.com/graphql \
  -H "Authorization: Bearer $IAM_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
  "query": "mutation addVirtualNetworkInterfaceToBareMetalNode($input: AddVirtualNetworkInterfaceToBareMetalNodeInput!) {\n  addVirtualNetworkInterfaceToBareMetalNode(input: $input) {\n    # \u2026 select your fields here\n  }\n}",
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


### `createSatelliteConnector`
{: #createsatelliteconnector}

Create a Satellite Connector.
{: shortdesc}

Returns
:   `CreateSatelliteConnectorPayload`

| Argument | Description |
| --- | --- |
| `input` (`CreateSatelliteConnectorInput`) |  |
{: caption="Arguments for createSatelliteConnector" caption-side="bottom"}


#### Example request
{: #example-request-createsatelliteconnector}

```sh
curl -X POST https://containers.cloud.ibm.com/graphql \
  -H "Authorization: Bearer $IAM_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
  "query": "mutation createSatelliteConnector($input: CreateSatelliteConnectorInput) {\n  createSatelliteConnector(input: $input) {\n    # \u2026 select your fields here\n  }\n}",
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


### `reinitializeKubernetesNode`
{: #reinitializekubernetesnode}

Reinitialize a Kubernetes node. Not supported on VPC virtual server instances today.
{: shortdesc}

Returns
:   `ReinitializeKubernetesNodePayload`

| Argument | Description |
| --- | --- |
| `input` (`ReinitializeKubernetesNodeInput`) |  |
{: caption="Arguments for reinitializeKubernetesNode" caption-side="bottom"}


#### Example request
{: #example-request-reinitializekubernetesnode}

```sh
curl -X POST https://containers.cloud.ibm.com/graphql \
  -H "Authorization: Bearer $IAM_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
  "query": "mutation reinitializeKubernetesNode($input: ReinitializeKubernetesNodeInput) {\n  reinitializeKubernetesNode(input: $input) {\n    # \u2026 select your fields here\n  }\n}",
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

Returns
:   `RemoveSatelliteConnectorPayload`

| Argument | Description |
| --- | --- |
| `input` (`RemoveSatelliteConnectorInput`) |  |
{: caption="Arguments for removeSatelliteConnector" caption-side="bottom"}


#### Example request
{: #example-request-removesatelliteconnector}

```sh
curl -X POST https://containers.cloud.ibm.com/graphql \
  -H "Authorization: Bearer $IAM_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
  "query": "mutation removeSatelliteConnector($input: RemoveSatelliteConnectorInput) {\n  removeSatelliteConnector(input: $input) {\n    # \u2026 select your fields here\n  }\n}",
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

Returns
:   `RemoveVirtualNetworkInterfaceFromNodePayload`

| Argument | Description |
| --- | --- |
| `input` (`RemoveVirtualNetworkInterfaceFromNodeInput!`) *(required)* | Input parameters for removing the VNI from a node. |
{: caption="Arguments for removeVirtualNetworkInterfaceFromNode" caption-side="bottom"}


#### Example request
{: #example-request-removevirtualnetworkinterfacefromnode}

```sh
curl -X POST https://containers.cloud.ibm.com/graphql \
  -H "Authorization: Bearer $IAM_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
  "query": "mutation removeVirtualNetworkInterfaceFromNode($input: RemoveVirtualNetworkInterfaceFromNodeInput!) {\n  removeVirtualNetworkInterfaceFromNode(input: $input) {\n    # \u2026 select your fields here\n  }\n}",
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
        }
      },
      "node": "<NetworkAttachable>",
      "virtualNetworkInterface": "<VirtualNetworkInterface>"
    }
  }
}
```


### `updateSatelliteLocation`
{: #updatesatellitelocation}

Update a Satellite Location.
{: shortdesc}

Returns
:   `UpdateSatelliteLocationPayload`

| Argument | Description |
| --- | --- |
| `input` (`UpdateSatelliteLocationInput`) |  |
{: caption="Arguments for updateSatelliteLocation" caption-side="bottom"}


#### Example request
{: #example-request-updatesatellitelocation}

```sh
curl -X POST https://containers.cloud.ibm.com/graphql \
  -H "Authorization: Bearer $IAM_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
  "query": "mutation updateSatelliteLocation($input: UpdateSatelliteLocationInput) {\n  updateSatelliteLocation(input: $input) {\n    # \u2026 select your fields here\n  }\n}",
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

| Field | Description |
| --- | --- |
| `externalID` (`String!`) | The account's IBM Cloud ID. |
{: caption="Fields for Account" caption-side="bottom"}


### AddVirtualNetworkInterfaceToBareMetalNodePayload
{: #addvirtualnetworkinterfacetobaremetalnodepayload}

Response payload for adding a VNI to a bare metal node.
{: shortdesc}

| Field | Description |
| --- | --- |
| `networkAttachment` (`NetworkAttachment!`) | The created network attachment with its properties. |
{: caption="Fields for AddVirtualNetworkInterfaceToBareMetalNodePayload" caption-side="bottom"}


### BareMetalNetworkAttachmentByVLAN
{: #baremetalnetworkattachmentbyvlan}

Network attachment for bare metal nodes using VLAN tagging.
{: shortdesc}

Implements
:   `NetworkAttachment`

| Field | Description |
| --- | --- |
| `attachedTo` (`NetworkAttachable!`) | The bare metal node this interface is attached to. |
| `canFloat` (`Boolean!`) | Whether this attachment can float between nodes in the cluster. |
| `virtualNetworkInterface` (`VirtualNetworkInterface!`) | The virtual network interface that is attached. |
| `vlanID` (`Int`) | VLAN ID used for this attachment (2-500). Null if not yet assigned. |
{: caption="Fields for BareMetalNetworkAttachmentByVLAN" caption-side="bottom"}


### BareMetalVirtualNetworkInterface
{: #baremetalvirtualnetworkinterface}

Virtual network interface attached to a bare metal server.
{: shortdesc}

Implements
:   `VirtualNetworkInterface`

| Field | Description |
| --- | --- |
| `autoDelete` (`Boolean`) | Whether the VNI should be automatically deleted when detached. |
| `externalID` (`String!`) | The VPC resource ID of this VNI. |
| `macAddress` (`MACAddress`) | MAC address assigned to this network interface. |
| `name` (`String`) | Human-readable name of the VNI. |
| `primaryIPAddress` (`IPv4Address`) | Primary IPv4 address assigned to this network interface. |
| `securityGroups` (`SecurityGroupConnection`) | Security groups applied to this network interface.  \n **Arguments for `securityGroups`**  \n * `after` (`String`) — Cursor to start fetching from. \n * `first` (`Int`) — Maximum number of items to return. |
| `subnet` (`Subnet!`) | The VPC subnet this network interface is connected to. |
{: caption="Fields for BareMetalVirtualNetworkInterface" caption-side="bottom"}


### CreateSatelliteConnectorPayload
{: #createsatelliteconnectorpayload}

Output type for createSatelliteConnector.
{: shortdesc}

| Field | Description |
| --- | --- |
| `satelliteConnector` (`SatelliteConnector`) | The new SatelliteConnector. |
{: caption="Fields for CreateSatelliteConnectorPayload" caption-side="bottom"}


### KubernetesCluster
{: #kubernetescluster}

An IBM Cloud Kubernetes Service or IBM Cloud OpenShift Service cluster.
{: shortdesc}

Implements
:   `Node`

| Field | Description |
| --- | --- |
| `id` (`ID!`) | The cluster's unique identifier. |
| `name` (`String`) | The cluster's name. |
| `networkAttachments` (`NetworkAttachmentConnection`) | Network attachments for this cluster (if applicable).  \n **Arguments for `networkAttachments`**  \n * `after` (`String`) — Cursor to start fetching from. \n * `first` (`Int`) — Maximum number of items to return. |
| `region` (`Region`) | The cluster's IBM Cloud catalog region. |
{: caption="Fields for KubernetesCluster" caption-side="bottom"}


### Region
{: #region}

An IBM Cloud catalog region.
{: shortdesc}

Implements
:   `Location`, `Node`

| Field | Description |
| --- | --- |
| `displayName` (`String`) | The translated name of this region. |
| `id` (`ID!`) | The ID of this region. |
| `name` (`String`) | The name of this region. |
{: caption="Fields for Region" caption-side="bottom"}


### ReinitializeKubernetesNodePayload
{: #reinitializekubernetesnodepayload}

Output type for reinitializeKubernetesNode.
{: shortdesc}

| Field | Description |
| --- | --- |
| `node` (`KubernetesNode`) | The reinitializing Kubernetes node. |
{: caption="Fields for ReinitializeKubernetesNodePayload" caption-side="bottom"}


### RemoveSatelliteConnectorPayload
{: #removesatelliteconnectorpayload}

Output type for removeSatelliteConnector.
{: shortdesc}

| Field | Description |
| --- | --- |
| `satelliteConnector` (`SatelliteConnector`) | The removed SatelliteConnector. |
{: caption="Fields for RemoveSatelliteConnectorPayload" caption-side="bottom"}


### RemoveVirtualNetworkInterfaceFromNodePayload
{: #removevirtualnetworkinterfacefromnodepayload}

Response payload for removing a VNI from a node.
{: shortdesc}

| Field | Description |
| --- | --- |
| `cluster` (`KubernetesCluster!`) | The cluster the VNI was removed from. |
| `node` (`NetworkAttachable!`) | The node the VNI was removed from. |
| `virtualNetworkInterface` (`VirtualNetworkInterface!`) | The virtual network interface that was removed. |
{: caption="Fields for RemoveVirtualNetworkInterfaceFromNodePayload" caption-side="bottom"}


### ResourceGroup
{: #resourcegroup}

A ResourceGroup is a way for you to organize your account resources in customizable groupings so that you can quickly assign users access to multiple resources at a time.
{: shortdesc}

Implements
:   `Node`

| Field | Description |
| --- | --- |
| `externalID` (`String!`) | The resource group's IBM Cloud ID. |
| `id` (`ID!`) | The resource group's Node ID. |
| `name` (`String`) | The resource group's name. |
{: caption="Fields for ResourceGroup" caption-side="bottom"}


### SatelliteConnector
{: #satelliteconnector}

A Satellite Connector provides a secure connection between a specific remote location and IBM Cloud.
{: shortdesc}

Implements
:   `Node`

| Field | Description |
| --- | --- |
| `createdDate` (`DateTime`) | The date when this resource was created. |
| `crn` (`CloudResourceName`) | The resource's IBM Cloud CRN. |
| `id` (`ID!`) | The resource's unique identifier. |
| `name` (`String!`) | The resource's name. |
| `region` (`Region`) | The region the resource is managed from. |
| `resourceGroup` (`ResourceGroup`) | The resource group containing this resource. |
| `state` (`SatelliteConnectorState`) | The current state of this resource. |
{: caption="Fields for SatelliteConnector" caption-side="bottom"}


### SatelliteLocation
{: #satellitelocation}

A Satellite Location.
{: shortdesc}

Implements
:   `Node`

| Field | Description |
| --- | --- |
| `description` (`String`) | The Location description. |
| `id` (`ID!`) | The resource's unique identifier. |
| `name` (`String`) | The Location name. |
{: caption="Fields for SatelliteLocation" caption-side="bottom"}


### SecurityGroup
{: #securitygroup}

Represents a VPC security group.
{: shortdesc}

| Field | Description |
| --- | --- |
| `externalID` (`String!`) | The VPC resource ID of this security group. |
{: caption="Fields for SecurityGroup" caption-side="bottom"}


### Subnet
{: #subnet}

Represents a VPC subnet.
{: shortdesc}

| Field | Description |
| --- | --- |
| `externalID` (`String!`) | The VPC resource ID of this subnet. |
{: caption="Fields for Subnet" caption-side="bottom"}


### UpdateSatelliteLocationPayload
{: #updatesatellitelocationpayload}

Output type for updateSatelliteLocation.
{: shortdesc}

| Field | Description |
| --- | --- |
| `satelliteLocation` (`SatelliteLocation`) | The updated SatelliteLocation. |
{: caption="Fields for UpdateSatelliteLocationPayload" caption-side="bottom"}


### VPCBareMetalKubernetesNode
{: #vpcbaremetalkubernetesnode}

Represents a bare metal Kubernetes worker node in IBM Cloud VPC.
{: shortdesc}

Implements
:   `KubernetesNode`, `NetworkAttachable`, `Node`

| Field | Description |
| --- | --- |
| `id` (`ID!`) | Globally unique identifier for this worker node. |
| `networkAttachments` (`NetworkAttachmentConnection`) | Network attachments for this bare metal node.  \n **Arguments for `networkAttachments`**  \n * `after` (`String`) — Cursor to start fetching from. \n * `first` (`Int`) — Maximum number of items to return. |
| `region` (`Region`) |  |
{: caption="Fields for VPCBareMetalKubernetesNode" caption-side="bottom"}


## Interface types
{: #interface-types}

Interface types define common fields that are shared across multiple concrete object types.


### KubernetesNode
{: #kubernetesnode}

A Kubernetes Node runs your workload.
{: shortdesc}

Implementations
:   `KubernetesNode`, `VPCBareMetalKubernetesNode`

| Field | Description |
| --- | --- |
| `id` (`ID!`) | The resource's unique identifier. |
| `region` (`Region`) |  |
{: caption="Fields for KubernetesNode" caption-side="bottom"}


### Location
{: #location}

An IBM Cloud catalog location.
{: shortdesc}

Implementations
:   `Location`, `Region`

| Field | Description |
| --- | --- |
| `displayName` (`String`) | Translated name of this location. |
| `id` (`ID!`) | The ID of this location. |
| `name` (`String`) | Name of this location. |
{: caption="Fields for Location" caption-side="bottom"}


### NetworkAttachable
{: #networkattachable}

Represents an entity that can have network interfaces attached to it.
{: shortdesc}

Implementations
:   `NetworkAttachable`

| Field | Description |
| --- | --- |
| `id` (`ID!`) | Globally unique identifier for this node. |
| `networkAttachments` (`NetworkAttachmentConnection`) | Network attachments associated to this node.  \n **Arguments for `networkAttachments`**  \n * `after` (`String`) — Cursor to start fetching from. \n * `first` (`Int`) — Maximum number of items to return. |
{: caption="Fields for NetworkAttachable" caption-side="bottom"}


### NetworkAttachment
{: #networkattachment}

Represents a network interface attachment to a node.
{: shortdesc}

Implementations
:   `BareMetalNetworkAttachmentByVLAN`, `NetworkAttachment`

| Field | Description |
| --- | --- |
| `attachedTo` (`NetworkAttachable!`) | The node this network interface is attached to. |
| `virtualNetworkInterface` (`VirtualNetworkInterface!`) | The virtual network interface that is attached. |
{: caption="Fields for NetworkAttachment" caption-side="bottom"}


### Node
{: #node}

Fetches an object given its ID.
{: shortdesc}

Implementations
:   `KubernetesCluster`, `KubernetesNode`, `NetworkAttachable`, `Node`, `Region`, `ResourceGroup`, `SatelliteConnector`, `SatelliteLocation`, `VPCBareMetalKubernetesNode`

| Field | Description |
| --- | --- |
| `id` (`ID!`) | The globally unique object ID. |
{: caption="Fields for Node" caption-side="bottom"}


### VirtualNetworkInterface
{: #virtualnetworkinterface}

Represents a virtual network interface in IBM Cloud VPC.
Can be attached to bare metal or virtual server instances.
{: shortdesc}

Implementations
:   `BareMetalVirtualNetworkInterface`, `VirtualNetworkInterface`

| Field | Description |
| --- | --- |
| `autoDelete` (`Boolean`) | Whether the VNI should be automatically deleted when detached. |
| `externalID` (`String!`) | The VPC resource ID of this virtual network interface. |
| `macAddress` (`MACAddress`) | MAC address assigned to this network interface. |
| `name` (`String`) | Human-readable name of the VNI. |
| `primaryIPAddress` (`IPv4Address`) | Primary IPv4 address assigned to this network interface. |
| `securityGroups` (`SecurityGroupConnection`) | Security groups applied to this network interface.  \n **Arguments for `securityGroups`**  \n * `after` (`String`) — Cursor to start fetching from. \n * `first` (`Int`) — Maximum number of items to return. |
| `subnet` (`Subnet!`) | The VPC subnet this network interface is connected to. |
{: caption="Fields for VirtualNetworkInterface" caption-side="bottom"}


## Input types
{: #input-types}

Input types are used as arguments to mutations. Fields marked *(required)* must be provided.


### AddVirtualNetworkInterfaceToBareMetalNodeInput
{: #addvirtualnetworkinterfacetobaremetalnodeinput}

Input for adding a VNI to a bare metal node.
{: shortdesc}

| Field | Description |
| --- | --- |
| `autoDelete` (`Boolean`) | Whether to automatically delete the VNI from VPC when it is detached. Defaults to false if not specified. |
| `cluster` (`ID`) | Cluster ID. Either cluster or node must be specified, but not both. If only cluster is provided, a node will be auto-selected and the attachment will float. |
| `node` (`ID`) | Node ID. Either cluster or node must be specified, but not both. If specified, creates a non-floating attachment to this specific node. |
| `virtualNetworkInterfaceID` (`String!`) *(required)* | The VPC resource ID of the virtual network interface to attach. |
| `vlanID` (`Int!`) *(required)* | VLAN ID for the attachment (2-500). VLAN 1 is reserved for the primary network interface. |
{: caption="Input fields for AddVirtualNetworkInterfaceToBareMetalNodeInput" caption-side="bottom"}


### CreateSatelliteConnectorInput
{: #createsatelliteconnectorinput}

Details needed to provision a Satellite Connector.
{: shortdesc}

| Field | Description |
| --- | --- |
| `name` (`String!`) *(required)* | The resource's name. |
| `regionName` (`String!`) *(required)* | The region name indicating where the new connector should be managed from. |
| `resourceGroupID` (`String!`) *(required)* | The resource group ID to provision inside. |
{: caption="Input fields for CreateSatelliteConnectorInput" caption-side="bottom"}


### ReinitializeKubernetesNodeInput
{: #reinitializekubernetesnodeinput}

Input type for reinitializeKubernetesNode.
{: shortdesc}

| Field | Description |
| --- | --- |
| `bypassUnhealthyControlPlane` (`Boolean`) | Set to true to proceed with reinitialization, even when the cluster's control plane is unhealthy. |
| `id` (`ID!`) *(required)* | Kubernetes node to reinitialize. |
{: caption="Input fields for ReinitializeKubernetesNodeInput" caption-side="bottom"}


### RemoveSatelliteConnectorInput
{: #removesatelliteconnectorinput}

Input type for removeSatelliteConnector.
{: shortdesc}

| Field | Description |
| --- | --- |
| `id` (`ID!`) *(required)* | Satellite Connector ID to remove. |
{: caption="Input fields for RemoveSatelliteConnectorInput" caption-side="bottom"}


### RemoveVirtualNetworkInterfaceFromNodeInput
{: #removevirtualnetworkinterfacefromnodeinput}

Input for removing a VNI from a node.
{: shortdesc}

| Field | Description |
| --- | --- |
| `cluster` (`ID`) | Cluster ID. Either cluster or node must be specified, but not both. |
| `node` (`ID`) | Node ID. Either cluster or node must be specified, but not both. |
| `virtualNetworkInterfaceID` (`String!`) *(required)* | The VPC resource ID of the virtual network interface to remove. |
{: caption="Input fields for RemoveVirtualNetworkInterfaceFromNodeInput" caption-side="bottom"}


### UpdateSatelliteLocationInput
{: #updatesatellitelocationinput}

Input type for updateSatelliteLocation.
{: shortdesc}

| Field | Description |
| --- | --- |
| `description` (`String`) |  |
| `id` (`ID!`) *(required)* | Satellite Location ID to update. |
| `name` (`String`) |  |
{: caption="Input fields for UpdateSatelliteLocationInput" caption-side="bottom"}


## Enum types
{: #enum-types}

Enum types define the set of allowed string values for a field.


### SatelliteConnectorState
{: #satelliteconnectorstate}

The administrative state of a Satellite Connector.

The values are expected to expand in the future. When processing, check for and log unknown values. Optionally halt processing and surface the error, or bypass the Satellite Connector on which the unexpected value was encountered.
{: shortdesc}

| Value | Description |
| --- | --- |
| `CREATED` | The connector has completed provisioning and is ready to use. |
| `CREATING` | The connector is provisioning and may not be ready to use. |
| `DELETING` | The connector is deprovisioning and may be unavailable. |
| `FAILED` | The connector's most recent operation has failed and it must be deleted to continue. |
{: caption="Values for SatelliteConnectorState" caption-side="bottom"}


## Scalar types
{: #scalar-types}

Scalar types are primitive leaf values in the GraphQL schema.


### CloudResourceName
{: #cloudresourcename}

A Cloud Resource Name (CRN) uniquely identifies IBM Cloud resources. A CRN is used to specify a resource in an unambiguous way that is guaranteed to be globally unique.
{: shortdesc}


### DateTime
{: #datetime}

A DateTime is an RFC3339 compliant combination of a date and time.
{: shortdesc}


### IPv4Address
{: #ipv4address}

IPv4 address in dotted-decimal notation (e.g., 192.168.1.1).
{: shortdesc}


### MACAddress
{: #macaddress}

MAC address in colon-hexadecimal notation (e.g., 00:1A:2B:3C:4D:5E).
{: shortdesc}
