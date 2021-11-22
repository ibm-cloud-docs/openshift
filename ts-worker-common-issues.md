---

copyright: 
  years: 2014, 2021
lastupdated: "2021-11-22"

keywords: openshift

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}


# Common issues with worker nodes
{: #common_worker_nodes_issues}

Review common error messages and learn how to resolve them. Messages might begin with the prefix, `'<provider>' infrastructure exception:`, where `<provider>` identifies which infrastructure provider the worker node uses.
{: shortdesc}

**Infrastructure provider**:
* ![Classic infrastructure provider icon.](images/icon-classic-2.svg) Classic
* ![VPC infrastructure provider icon.](images/icon-vpc-2.svg) VPC

## Account prohibited from ordering
{: #order-prohibit}

**Message**:

```
Your account is currently prohibited from ordering 'Computing Instances'.
```
{: screen}

**Description and resolution**:

Your IBM Cloud infrastructure account might be restricted from ordering compute resources. Contact {{site.data.keyword.cloud_notm}} support by opening an [{{site.data.keyword.cloud_notm}} support case](/docs/containers?topic=containers-get-help).

## Could not place order
{: #order-not-placed}

**Message**:

```
Could not place order.

Could not place order. There are insufficient resources behind router 'router_name' to fulfill the request for the following guests: 'worker_id'.
```
{: screen}

**Description and resolution**:
The zone that you selected might not have enough infrastructure capacity to provision your worker nodes. Or, you might have exceeded a limit in your IBM Cloud infrastructure account. 

To resolve, try one of the following options:
* Infrastructure resource availability in zones can fluctuate often. Wait a few minutes and try again.
* For a single zone cluster, create the cluster in a different zone. For a multizone cluster, add a zone to the cluster.
* Specify a different pair of public and private VLANs for your worker nodes in your IBM Cloud infrastructure account. For worker nodes that are in a worker pool, you can use the `ibmcloud oc zone network-set` [command](<opens</li>
* Contact your IBM Cloud infrastructure account manager to verify that you don't exceed an account limit, such as a global quota.
* Open an [IBM Cloud infrastructure support case](/docs/containers?topic=containers-get-help).

## Could not obtain network VLAN
{: #no-network-vlan}

**Message**:

```
Could not obtain network VLAN with ID: <vlan-id>
```
{: screen}

**Description and resolution**:

Your worker node could not be provisioned because the selected VLAN ID could not be found for one of the following reasons:
* You might have specified the VLAN number instead of the VLAN ID. The VLAN number is 3 or 4 digits long, whereas the VLAN ID is 7 digits long. To retrieve the VLAN ID, run `ibmcloud oc vlan ls --zone <zone>`.
* The VLAN ID might not be associated with the IBM Cloud infrastructure account that you use. To list available VLAN IDs for your account, run `ibmcloud oc vlan ls --zone <zone>` . To change the IBM Cloud infrastructure account, see [`ibmcloud oc credential set`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_credentials_set).

## Location invalid
{: #location-invalid}

**Message**:

```
The location provided for this order is invalid
```
{: screen}

**Description and resolution**:

Your IBM Cloud infrastructure is not set up to order compute resources in the selected data center. Contact [{{site.data.keyword.cloud_notm}} support](/docs/containers?topic=containers-get-help) to verify that you account is set up correctly.

## Permissions error
{: #permissions-error}

**Message**:

```
The user does not have the necessary {{site.data.keyword.cloud_notm}} classic infrastructure permissions to add servers

'Item' must be ordered with permission.

The IBM Cloud infrastructure credentials could not be validated.

'<Provider>' infrastructure request not authorized
```
{: screen}

**Description and resolution**:

You might not have the required permissions to perform the action in your IBM Cloud infrastructure portfolio, or you are using the wrong infrastructure credentials. See [Setting up the API key to enable access to the infrastructure portfolio](/docs/containers?topic=containers-access-creds).

## Firewall error
{: #firewall-error}

**Message**:

```
Worker unable to talk to {{site.data.keyword.containerlong_notm}} servers. Please verify your firewall setup is allowing traffic from this worker.
```
{: screen}

**Description and resolution**:

If you have a firewall, [configure your firewall settings to allow outgoing traffic to the appropriate ports and IP addresses](/docs/openshift?topic=openshift-firewall#firewall_outbound).



## Hard reboot
{: #hard-reboot}

**Message**:

```
The worker did not respond to the soft reboot request. A hard reboot might be necessary.
```
{: screen}

**Description and resolution**:

Although you issued a reboot on your worker node, the worker node is unresponsive. You can rerun the [reboot command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_reboot) with the `--hard` flag to power off the worker node, or run the `worker reload` [command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_reload).

## Instance can't be found
{: #instance-not-found}

**Message**:

```
can't create IMS portal token, as no IMS account is linked to the selected BSS account

Provided user not found or active

User account is currently cancel_pending.

The worker node instance '<ID>' can't be found. Review '<provider>' infrastructure user permissions.

The worker node instance can't be found. Review '<provider>' infrastructure user permissions.

The worker node instance can't be identified. Review '<provider>' infrastructure user permissions.
```
{: screen}

**Description and resolution**:

The owner of the API key that is used to access the IBM Cloud infrastructure portfolio does not have the required permissions to perform the action, or might be pending deletion.

As the **user**, follow these steps:
1. If you have access to multiple accounts, make sure that you are logged in to the account where you want to work with {{site.data.keyword.openshiftlong_notm}}.
2. Run `ibmcloud oc api-key info --cluster <cluster_name_or_ID>` to view the current API key owner that is used to access the IBM Cloud infrastructure portfolio. </li>
3. Run `ibmcloud account list` to view the owner of the {{site.data.keyword.cloud_notm}} account that you currently use.
4. Contact the owner of the {{site.data.keyword.cloud_notm}} account and report that the API key owner has insufficient permissions in IBM Cloud infrastructure or might be pending to be deleted.

As the **account owner**, follow these steps:
1. Review the [required classic permissions in IBM Cloud infrastructure](/docs/openshift?topic=openshift-access-creds#infra_access) to perform the action that previously failed. For the VPC infrastructure provider, the API key owner must have the **Administrator** platform access role.
2. Fix the permissions of the API key owner or create a new API key by using the [`ibmcloud oc api-key reset --region <region>`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_api_key_reset) command.
3. If you or another account admin manually set IBM Cloud infrastructure credentials in your account, run [`ibmcloud oc credential unset --region <region>`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_credentials_unset) to remove the credentials from your account.




