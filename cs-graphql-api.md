---
copyright:
  years: 2026
lastupdated: "2026-09-22"

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

| Type | Name | Description |
| --- | --- | --- |
| Returns | `Node` | |
| Argument | `id` (`ID!`) *(required)* | The globally unique node identifier. |
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


### CreateSatelliteConnectorPayload
{: #createsatelliteconnectorpayload}

Output type for createSatelliteConnector.
{: shortdesc}

| Type | Name | Description |
| --- | --- | --- |
| Field | `satelliteConnector` (`SatelliteConnector`) | The new SatelliteConnector. |
{: caption="Fields for CreateSatelliteConnectorPayload" caption-side="bottom"}


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
{: caption="Fields for KubernetesCluster" caption-side="bottom"}


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
