---
copyright:
  years: 2026
lastupdated: "2026-09-18"

keywords: containers, kubernetes, satellite, graphql, api, reference

subcollection: containers
---

{{site.data.keyword.attribute-definition-list}}

# IBM Cloud Kubernetes Service GraphQL API reference
{: #cs-graphql-api}

The {{site.data.keyword.containerlong_notm}} GraphQL API is available at `https://containers.cloud.ibm.com/graphql`. Use this API to manage Satellite Connectors, Kubernetes clusters, and bare metal worker nodes programmatically.
{: shortdesc}

This page is auto-generated from the live schema. All field and argument names are case-sensitive.


## Queries
{: #queries}

Queries retrieve data without modifying any resources. Send a `POST` request to `https://containers.cloud.ibm.com/graphql` with your query in the request body.


### `globalSearchSatelliteConnectorAccounts`
{: #globalsearchsatelliteconnectoraccounts}

Globally searchable results for the IBM Global Search service. Internal use only.
{: shortdesc}

**Returns:** `GlobalSearchSatelliteConnectorAccountsConnection`

**Arguments:**

- `after`: `String`
- `first`: `Int`
- `last`: `Int`
- `before`: `String`
- `regionName`: `String!` *(required)*


### `node`
{: #node}

Find a Node for the given ID. Use fragments to select additional fields.
{: shortdesc}

**Returns:** `Node`

**Arguments:**

- `id`: `ID!` *(required)*
  The globally unique node identifier.


### `satelliteConnectors`
{: #satelliteconnectors}

List the Satellite Connectors you have access to.
{: shortdesc}

**Returns:** `SatelliteConnectorConnection`

**Arguments:**

- `after`: `String`
  Return Satellite Connectors after this cursor.
- `first`: `Int`
  Return the first N Satellite Connectors.
- `last`: `Int`
  Return the last N Satellite Connectors.
- `before`: `String`
  Return Satellite Connectors before this cursor.


## Mutations
{: #mutations}

Mutations create, update, or delete resources. Each mutation requires an IAM bearer token in the `Authorization` header.


### `addVirtualNetworkInterfaceToBareMetalNode`
{: #addvirtualnetworkinterfacetobaremetalnode}

Adds a virtual network interface (VNI) to a bare metal Kubernetes worker node.
{: shortdesc}

**Returns:** `AddVirtualNetworkInterfaceToBareMetalNodePayload`

**Arguments:**

- `input`: `AddVirtualNetworkInterfaceToBareMetalNodeInput!` *(required)*
  Input parameters for adding the VNI to a bare metal node.


### `createSatelliteConnector`
{: #createsatelliteconnector}

Create a Satellite Connector.
{: shortdesc}

**Returns:** `CreateSatelliteConnectorPayload`

**Arguments:**

- `input`: `CreateSatelliteConnectorInput`


### `reinitializeKubernetesNode`
{: #reinitializekubernetesnode}

Reinitialize a Kubernetes node. Not supported on VPC virtual server instances today.
{: shortdesc}

**Returns:** `ReinitializeKubernetesNodePayload`

**Arguments:**

- `input`: `ReinitializeKubernetesNodeInput`


### `removeSatelliteConnector`
{: #removesatelliteconnector}

Remove a Satellite Connector.
{: shortdesc}

**Returns:** `RemoveSatelliteConnectorPayload`

**Arguments:**

- `input`: `RemoveSatelliteConnectorInput`


### `removeVirtualNetworkInterfaceFromNode`
{: #removevirtualnetworkinterfacefromnode}

Removes a virtual network interface from a Kubernetes worker node.
{: shortdesc}

**Returns:** `RemoveVirtualNetworkInterfaceFromNodePayload`

**Arguments:**

- `input`: `RemoveVirtualNetworkInterfaceFromNodeInput!` *(required)*
  Input parameters for removing the VNI from a node.


### `updateSatelliteLocation`
{: #updatesatellitelocation}

Update a Satellite Location.
{: shortdesc}

**Returns:** `UpdateSatelliteLocationPayload`

**Arguments:**

- `input`: `UpdateSatelliteLocationInput`


## Object types
{: #object-types}

Object types represent the concrete resources and response payloads returned by the API.


### Account
{: #account}

An IBM Cloud account.
{: shortdesc}

**Fields:**

`externalID`: `String!`
:   The account's IBM Cloud ID.


### AddVirtualNetworkInterfaceToBareMetalNodePayload
{: #addvirtualnetworkinterfacetobaremetalnodepayload}

Response payload for adding a VNI to a bare metal node.
{: shortdesc}

**Fields:**

`networkAttachment`: `NetworkAttachment!`
:   The created network attachment with its properties.


### BareMetalNetworkAttachmentByVLAN
{: #baremetalnetworkattachmentbyvlan}

Network attachment for bare metal nodes using VLAN tagging.
{: shortdesc}

**Implements:** `NetworkAttachment`

**Fields:**

`attachedTo`: `NetworkAttachable!`
:   The bare metal node this interface is attached to.

`canFloat`: `Boolean!`
:   Whether this attachment can float between nodes in the cluster.

`virtualNetworkInterface`: `VirtualNetworkInterface!`
:   The virtual network interface that is attached.

`vlanID`: `Int`
:   VLAN ID used for this attachment (2-500). Null if not yet assigned.


### BareMetalVirtualNetworkInterface
{: #baremetalvirtualnetworkinterface}

Virtual network interface attached to a bare metal server.
{: shortdesc}

**Implements:** `VirtualNetworkInterface`

**Fields:**

`autoDelete`: `Boolean`
:   Whether the VNI should be automatically deleted when detached.

`externalID`: `String!`
:   The VPC resource ID of this VNI.

`macAddress`: `MACAddress`
:   MAC address assigned to this network interface.

`name`: `String`
:   Human-readable name of the VNI.

`primaryIPAddress`: `IPv4Address`
:   Primary IPv4 address assigned to this network interface.

`securityGroups`: `SecurityGroupConnection`
:   Security groups applied to this network interface.
:   **Arguments:**
:   `after`: `String`
:       - Cursor to start fetching from.
:   `first`: `Int`
:       - Maximum number of items to return.

`subnet`: `Subnet!`
:   The VPC subnet this network interface is connected to.


### CreateSatelliteConnectorPayload
{: #createsatelliteconnectorpayload}

Output type for createSatelliteConnector.
{: shortdesc}

**Fields:**

`satelliteConnector`: `SatelliteConnector`
:   The new SatelliteConnector.


### KubernetesCluster
{: #kubernetescluster}

An IBM Cloud Kubernetes Service or IBM Cloud OpenShift Service cluster.
{: shortdesc}

**Implements:** `Node`

**Fields:**

`id`: `ID!`
:   The cluster's unique identifier.

`name`: `String`
:   The cluster's name.

`networkAttachments`: `NetworkAttachmentConnection`
:   Network attachments for this cluster (if applicable).
:   **Arguments:**
:   `after`: `String`
:       - Cursor to start fetching from.
:   `first`: `Int`
:       - Maximum number of items to return.

`region`: `Region`
:   The cluster's IBM Cloud catalog region.


### Region
{: #region}

An IBM Cloud catalog region.
{: shortdesc}

**Implements:** `Location`, `Node`

**Fields:**

`displayName`: `String`
:   The translated name of this region.

`id`: `ID!`
:   The ID of this region.

`name`: `String`
:   The name of this region.


### ReinitializeKubernetesNodePayload
{: #reinitializekubernetesnodepayload}

Output type for reinitializeKubernetesNode.
{: shortdesc}

**Fields:**

`node`: `KubernetesNode`
:   The reinitializing Kubernetes node.


### RemoveSatelliteConnectorPayload
{: #removesatelliteconnectorpayload}

Output type for removeSatelliteConnector.
{: shortdesc}

**Fields:**

`satelliteConnector`: `SatelliteConnector`
:   The removed SatelliteConnector.


### RemoveVirtualNetworkInterfaceFromNodePayload
{: #removevirtualnetworkinterfacefromnodepayload}

Response payload for removing a VNI from a node.
{: shortdesc}

**Fields:**

`cluster`: `KubernetesCluster!`
:   The cluster the VNI was removed from.

`node`: `NetworkAttachable!`
:   The node the VNI was removed from.

`virtualNetworkInterface`: `VirtualNetworkInterface!`
:   The virtual network interface that was removed.


### ResourceGroup
{: #resourcegroup}

A ResourceGroup is a way for you to organize your account resources in customizable groupings so that you can quickly assign users access to multiple resources at a time.
{: shortdesc}

**Implements:** `Node`

**Fields:**

`externalID`: `String!`
:   The resource group's IBM Cloud ID.

`id`: `ID!`
:   The resource group's Node ID.

`name`: `String`
:   The resource group's name.


### SatelliteConnector
{: #satelliteconnector}

A Satellite Connector provides a secure connection between a specific remote location and IBM Cloud.
{: shortdesc}

**Implements:** `Node`

**Fields:**

`createdDate`: `DateTime`
:   The date when this resource was created.

`crn`: `CloudResourceName`
:   The resource's IBM Cloud CRN.

`id`: `ID!`
:   The resource's unique identifier.

`name`: `String!`
:   The resource's name.

`region`: `Region`
:   The region the resource is managed from.

`resourceGroup`: `ResourceGroup`
:   The resource group containing this resource.

`state`: `SatelliteConnectorState`
:   The current state of this resource.


### SatelliteLocation
{: #satellitelocation}

A Satellite Location.
{: shortdesc}

**Implements:** `Node`

**Fields:**

`description`: `String`
:   The Location description.

`id`: `ID!`
:   The resource's unique identifier.

`name`: `String`
:   The Location name.


### SecurityGroup
{: #securitygroup}

Represents a VPC security group.
{: shortdesc}

**Fields:**

`externalID`: `String!`
:   The VPC resource ID of this security group.


### Subnet
{: #subnet}

Represents a VPC subnet.
{: shortdesc}

**Fields:**

`externalID`: `String!`
:   The VPC resource ID of this subnet.


### UpdateSatelliteLocationPayload
{: #updatesatellitelocationpayload}

Output type for updateSatelliteLocation.
{: shortdesc}

**Fields:**

`satelliteLocation`: `SatelliteLocation`
:   The updated SatelliteLocation.


### VPCBareMetalKubernetesNode
{: #vpcbaremetalkubernetesnode}

Represents a bare metal Kubernetes worker node in IBM Cloud VPC.
{: shortdesc}

**Implements:** `KubernetesNode`, `NetworkAttachable`, `Node`

**Fields:**

`id`: `ID!`
:   Globally unique identifier for this worker node.

`networkAttachments`: `NetworkAttachmentConnection`
:   Network attachments for this bare metal node.
:   **Arguments:**
:   `after`: `String`
:       - Cursor to start fetching from.
:   `first`: `Int`
:       - Maximum number of items to return.

`region`: `Region`


## Interface types
{: #interface-types}

Interface types define common fields that are shared across multiple concrete object types.


### KubernetesNode
{: #kubernetesnode}

A Kubernetes Node runs your workload.
{: shortdesc}

**Implementations:** `KubernetesNode`, `VPCBareMetalKubernetesNode`

**Fields:**

`id`: `ID!`
:   The resource's unique identifier.

`region`: `Region`


### Location
{: #location}

An IBM Cloud catalog location.
{: shortdesc}

**Implementations:** `Location`, `Region`

**Fields:**

`displayName`: `String`
:   Translated name of this location.

`id`: `ID!`
:   The ID of this location.

`name`: `String`
:   Name of this location.


### NetworkAttachable
{: #networkattachable}

Represents an entity that can have network interfaces attached to it.
{: shortdesc}

**Implementations:** `NetworkAttachable`

**Fields:**

`id`: `ID!`
:   Globally unique identifier for this node.

`networkAttachments`: `NetworkAttachmentConnection`
:   Network attachments associated to this node.
:   **Arguments:**
:   `after`: `String`
:       - Cursor to start fetching from.
:   `first`: `Int`
:       - Maximum number of items to return.


### NetworkAttachment
{: #networkattachment}

Represents a network interface attachment to a node.
{: shortdesc}

**Implementations:** `BareMetalNetworkAttachmentByVLAN`, `NetworkAttachment`

**Fields:**

`attachedTo`: `NetworkAttachable!`
:   The node this network interface is attached to.

`virtualNetworkInterface`: `VirtualNetworkInterface!`
:   The virtual network interface that is attached.


### Node
{: #node}

Fetches an object given its ID.
{: shortdesc}

**Implementations:** `KubernetesCluster`, `KubernetesNode`, `NetworkAttachable`, `Node`, `Region`, `ResourceGroup`, `SatelliteConnector`, `SatelliteLocation`, `VPCBareMetalKubernetesNode`

**Fields:**

`id`: `ID!`
:   The globally unique object ID.


### VirtualNetworkInterface
{: #virtualnetworkinterface}

Represents a virtual network interface in IBM Cloud VPC.
Can be attached to bare metal or virtual server instances.
{: shortdesc}

**Implementations:** `BareMetalVirtualNetworkInterface`, `VirtualNetworkInterface`

**Fields:**

`autoDelete`: `Boolean`
:   Whether the VNI should be automatically deleted when detached.

`externalID`: `String!`
:   The VPC resource ID of this virtual network interface.

`macAddress`: `MACAddress`
:   MAC address assigned to this network interface.

`name`: `String`
:   Human-readable name of the VNI.

`primaryIPAddress`: `IPv4Address`
:   Primary IPv4 address assigned to this network interface.

`securityGroups`: `SecurityGroupConnection`
:   Security groups applied to this network interface.
:   **Arguments:**
:   `after`: `String`
:       - Cursor to start fetching from.
:   `first`: `Int`
:       - Maximum number of items to return.

`subnet`: `Subnet!`
:   The VPC subnet this network interface is connected to.


## Input types
{: #input-types}

Input types are used as arguments to mutations. Fields marked *(required)* must be provided.


### AddVirtualNetworkInterfaceToBareMetalNodeInput
{: #addvirtualnetworkinterfacetobaremetalnodeinput}

Input for adding a VNI to a bare metal node.
{: shortdesc}

**Input fields:**

`autoDelete`: `Boolean`
:   Whether to automatically delete the VNI from VPC when it is detached.
Defaults to false if not specified.

`cluster`: `ID`
:   Cluster ID. Either cluster or node must be specified, but not both.
If only cluster is provided, a node will be auto-selected and the attachment will float.

`node`: `ID`
:   Node ID. Either cluster or node must be specified, but not both.
If specified, creates a non-floating attachment to this specific node.

`virtualNetworkInterfaceID`: `String!` *(required)*
:   The VPC resource ID of the virtual network interface to attach.

`vlanID`: `Int!` *(required)*
:   VLAN ID for the attachment (2-500).
VLAN 1 is reserved for the primary network interface.


### CreateSatelliteConnectorInput
{: #createsatelliteconnectorinput}

Details needed to provision a Satellite Connector.
{: shortdesc}

**Input fields:**

`name`: `String!` *(required)*
:   The resource's name.

`regionName`: `String!` *(required)*
:   The region name indicating where the new connector should be managed from.

`resourceGroupID`: `String!` *(required)*
:   The resource group ID to provision inside.


### ReinitializeKubernetesNodeInput
{: #reinitializekubernetesnodeinput}

Input type for reinitializeKubernetesNode.
{: shortdesc}

**Input fields:**

`bypassUnhealthyControlPlane`: `Boolean`
:   Set to true to proceed with reinitialization, even when the cluster's control plane is unhealthy.

`id`: `ID!` *(required)*
:   Kubernetes node to reinitialize.


### RemoveSatelliteConnectorInput
{: #removesatelliteconnectorinput}

Input type for removeSatelliteConnector.
{: shortdesc}

**Input fields:**

`id`: `ID!` *(required)*
:   Satellite Connector ID to remove.


### RemoveVirtualNetworkInterfaceFromNodeInput
{: #removevirtualnetworkinterfacefromnodeinput}

Input for removing a VNI from a node.
{: shortdesc}

**Input fields:**

`cluster`: `ID`
:   Cluster ID. Either cluster or node must be specified, but not both.

`node`: `ID`
:   Node ID. Either cluster or node must be specified, but not both.

`virtualNetworkInterfaceID`: `String!` *(required)*
:   The VPC resource ID of the virtual network interface to remove.


### UpdateSatelliteLocationInput
{: #updatesatellitelocationinput}

Input type for updateSatelliteLocation.
{: shortdesc}

**Input fields:**

`description`: `String`

`id`: `ID!` *(required)*
:   Satellite Location ID to update.

`name`: `String`


## Enum types
{: #enum-types}

Enum types define the set of allowed string values for a field.


### SatelliteConnectorState
{: #satelliteconnectorstate}

The administrative state of a Satellite Connector.

The values are expected to expand in the future. When processing, check for and log unknown values. Optionally halt processing and surface the error, or bypass the Satellite Connector on which the unexpected value was encountered.
{: shortdesc}

**Values:**

- `CREATED`
  The connector has completed provisioning and is ready to use.
- `CREATING`
  The connector is provisioning and may not be ready to use.
- `DELETING`
  The connector is deprovisioning and may be unavailable.
- `FAILED`
  The connector's most recent operation has failed and it must be deleted to continue.


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
