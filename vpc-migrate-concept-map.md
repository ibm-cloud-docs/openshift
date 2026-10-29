---

copyright:
  years: 2026, 2026
lastupdated: "2026-10-29"

keywords: openshift, classic, vpc, migrate, concept map, mapping, equivalent, comparison

subcollection: openshift

content-type: reference

---

{{site.data.keyword.attribute-definition-list}}

# Classic-to-VPC concept mapping
{: #vpc-migrate-concept-map}

[Classic infrastructure]{: tag-classic-inf}

Use this reference to find the VPC equivalent for Classic infrastructure concepts, resources, and CLI commands.
{: shortdesc}

## Networking
{: #vpc-migrate-concept-map-networking}

| Classic concept | VPC equivalent | Notes |
|-----------------|----------------|-------|
| VLAN | Subnet | VPC subnets are zone-scoped and bound to a VPC. |
| Public VLAN | Public gateway attached to a subnet | VPC worker nodes use a public gateway for outbound internet access. |
| Private VLAN | VPC subnet (private by default) | All VPC subnets are private unless a public gateway is attached. |
| Classic firewall (Vyatta/vSRX) | Security groups and network ACLs | Security groups are allow-only; network ACLs support allow and deny rules. SCTP is not supported. |
| Classic VPN | VPN for VPC | Must be set up before workload migration. See [Plan your VPC environment](/docs/openshift?topic=openshift-vpc-migrate-plan#vpc-migrate-plan-connectivity). |
| Direct Link 1.0 | Direct Link 2.0 | Must be provisioned separately before migration. |
| Service endpoint (private) | Virtual Private Endpoint (VPE) gateway | VPE gateways replace Classic private service endpoints for IBM Cloud services. |
| Portable IP | Floating IP or VPC load balancer IP | Floating IPs are zone-specific. |
{: caption="Classic-to-VPC networking concepts" caption-side="bottom"}

## Load balancers
{: #vpc-migrate-concept-map-lb}

| Classic concept | VPC equivalent | Notes |
|-----------------|----------------|-------|
| Classic NLB 1.0 | VPC Application Load Balancer (ALB) | Classic NLB 1.0 is an ALB in VPC. |
| Classic NLB 2.0 | VPC Network Load Balancer (NLB) | NLB 2.0 features map to VPC NLB with instance groups. |
| Classic ALB (Ingress) | VPC ALB (Ingress) | Ingress resources are migrated automatically. ALB annotations differ between Classic and VPC. |
| IBM-provided Ingress subdomain | IBM-provided VPC Ingress subdomain | A new subdomain is assigned to the VPC cluster. Update Ingress resources post-migration. |
{: caption="Classic-to-VPC load balancer concepts" caption-side="bottom"}

## Storage
{: #vpc-migrate-concept-map-storage}

| Classic concept | VPC equivalent | Notes |
|-----------------|----------------|-------|
| Classic Block Storage (Endurance/Performance) | VPC Block Storage | Provisioned as `ibmc-vpc-block-*` storage classes. PVC data is migrated via BRS. |
| Classic File Storage (NFS) | VPC File Storage | Provisioned as `ibmc-vpc-file-*` storage classes. PVC data is migrated via BRS. Classic File Storage for Classic is not supported on VPC. |
| Classic Object Storage (COS) | IBM Cloud Object Storage (same) | COS buckets are not cluster-specific; no migration required. Update any cluster-side credentials. |
| ODF on Classic | ODF on VPC | **Not migrated automatically.** Install ODF on the VPC cluster before you start workload migration. See [VPC: Installing ODF](/docs/openshift?topic=openshift-deploy-odf-vpc). |
| Portworx on Classic | Portworx on VPC | **Not migrated automatically.** Install Portworx on the VPC cluster before you start workload migration. See [Installing Portworx in your cluster](/docs/openshift?topic=openshift-storage_portworx_deploy). |
{: caption="Classic-to-VPC storage concepts" caption-side="bottom"}

### Storage class name mapping
{: #vpc-migrate-concept-map-storage-classes}

The migration service provides the Classic-to-VPC storage class name mapping. To review it, see the migration plan or the **Storage class mapping** step in the migration wizard.

## Regions and zones
{: #vpc-migrate-concept-map-regions}

The migration wizard creates the VPC cluster in the same region and multizone configuration as the Classic cluster. Zone placement for new VPC worker nodes is proposed based on your Classic cluster topology and can be adjusted during the Plan phase.
{: note}

In Classic infrastructure, data centers (such as `dal10`, `dal12`, and `dal13`) represent individual zones grouped into regions and metros (such as `us-south` / `us-dal`). In VPC, zones use standardized names within each multizone region (MZR), such as `us-south-1`, `us-south-2`, and `us-south-3`.

| Classic region / metro | Classic data centers (zones) | VPC region | VPC zones |
|------------------------|------------------------------|------------|-----------|
| `us-south` (`us-dal`) | `dal10`, `dal12`, `dal13` | `us-south` | `us-south-1`, `us-south-2`, `us-south-3` |
| `us-east` (`us-wdc`) | `wdc04`, `wdc06`, `wdc07` | `us-east` | `us-east-1`, `us-east-2`, `us-east-3` |
| `eu-de` (`de-fra`) | `fra02`, `fra04`, `fra05` | `eu-de` | `eu-de-1`, `eu-de-2`, `eu-de-3` |
| `eu-gb` (`uk-lon`) | `lon02`, `lon04`, `lon05`, `lon06` | `eu-gb` | `eu-gb-1`, `eu-gb-2`, `eu-gb-3` |
| `jp-tok` (`jp-tok`) | `tok02`, `tok04`, `tok05` | `jp-tok` | `jp-tok-1`, `jp-tok-2`, `jp-tok-3` |
| `jp-osa` (`jp-osa`) | `osa21`, `osa22`, `osa23` | `jp-osa` | `jp-osa-1`, `jp-osa-2`, `jp-osa-3` |
| `au-syd` (`au-syd`) | `syd01`, `syd04`, `syd05` | `au-syd` | `au-syd-1`, `au-syd-2`, `au-syd-3` |
| `in-che` (`in-che`) | [VERIFY: Classic data centers for Chennai] | `in-che` | `in-che-1`, `in-che-2`, `in-che-3` |
| `in-mum` (`in-mum`) | [VERIFY: Classic data centers for Mumbai] | `in-mum` | `in-mum-1`, `in-mum-2`, `in-mum-3` |
| `eu-es` (`eu-es`) | [VERIFY: Classic data centers for Madrid] | `eu-es` | `eu-es-1`, `eu-es-2`, `eu-es-3` |
{: caption="Classic-to-VPC region and zone mapping" caption-side="bottom"}

## Cluster infrastructure
{: #vpc-migrate-concept-map-cluster}

| Classic concept | VPC equivalent | Notes |
|-----------------|----------------|-------|
| Classic worker node (VSI or bare metal) | VPC worker node (VSI) | If a bare metal configuration is not available on VPC, it is mapped to the nearest suitable VSI flavor. |
| Worker node flavor (m3c, b3c) | VPC flavor (bx2, mx2, cx2) | Flavors are reassigned during the Plan phase. |
| Classic dedicated host | VPC dedicated host | Supported on VPC. |
| Classic worker pool | VPC worker pool | Worker pools are recreated with VPC-equivalent flavors. |
| Classic cluster VLAN spanning | VPC implicit routing | VPC subnets within a VPC route to each other automatically; no spanning required. |
| Classic cluster master endpoint | VPC cluster master endpoint | A new endpoint URL is assigned to the VPC cluster. |
{: caption="Classic-to-VPC cluster infrastructure concepts" caption-side="bottom"}

## IAM and access
{: #vpc-migrate-concept-map-iam}

| Classic concept | VPC equivalent | Notes |
|-----------------|----------------|-------|
| Classic infrastructure API key | VPC infrastructure API key | IAM credentials are not migrated. Verify IAM API key permissions before migration. |
| Classic service account | IAM-based service ID | No change; service IDs are not cluster-specific. |
| Classic image pull secret | VPC image pull secret | Secrets are migrated automatically during the Migrate step. |
{: caption="Classic-to-VPC IAM and access concepts" caption-side="bottom"}

## CLI commands
{: #vpc-migrate-concept-map-cli}

| Classic CLI command | VPC equivalent | Notes |
|---------------------|----------------|-------|
| `ibmcloud oc cluster-create --hardware dedicated` | `ibmcloud oc cluster create vpc-gen2` | VPC cluster creation uses the `vpc-gen2` subcommand. |
| `ibmcloud oc worker-add` | `ibmcloud oc worker-pool resize` | Workers are added by resizing a worker pool on VPC. |
| `ibmcloud oc vlan-spanning-get` | N/A | Not applicable on VPC; routing is implicit. |
| `ibmcloud oc nlb-dns-create` | `ibmcloud oc nlb-dns create` | Command structure is the same; NLB IPs differ. |
| `ibmcloud oc alb-autoupdate-enable` | `ibmcloud oc ingress alb autoupdate enable` | Ingress CLI commands use the `ingress` subgroup on VPC. |
{: caption="Classic-to-VPC CLI command mapping" caption-side="bottom"}
