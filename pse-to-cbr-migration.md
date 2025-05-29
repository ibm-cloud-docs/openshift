---

copyright: 
  years: 2024, 2025
lastupdated: "2025-05-29"


keywords: kubernetes, private service endpoint, openshift, context based restrictions

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}

# Migrating from a private service endpoint allowlist to context based restrictions (CBR)
{: #pse-to-cbr-migration}

Private service endpoint allowlists are no longer supported and context based restrictions (CBR) should be used instead.  If your clusters currently have master private service endpoint allowlists enabled, you will not be able to modify the allowlist, all you can do is disable the allowlist.  Complete the following steps to migrate to using [context based restrictions](/docs/openshift?topic=openshift-cbr) (CBR).
{: shortdesc}

The following instructions cover protecting the private service endpoint of your cluster by using CBR rules. If your cluster has both a public and private service endpoint (PSE), you can also protect your cluster's public service endpoint with CBR.

Some advantages of CBR include:
- Target multiple clusters in an account at once and not have to set the list for each one.
- Allow access from specific VPCs, not just IPs or subnets.
- Set higher limits of up to 200 private and 500 public IPs or subnets, rather than a max total of 75 with PSE. 
- Create and manage CBR rules from the console, API, or CLI.
- Restrict public access via CBR. The private service endpoint allowlist only restricts private service endpoint traffic.

## Before you begin
{: #pse-cbr-before}

If you are already using CBR rules to protect your clusters, then these instructions might not fit your use case. Instead, use the CBR documentation to understand how to modify your existing CBR rules to include the private service endpoint allowlist subnets. For more information about CBR, see [Protecting cluster resources with context-based restrictions](/docs/openshift?topic=openshift-cbr&interface=ui) and the [example context-based restrictions scenarios](/docs/openshift?topic=openshift-cbr-tutorial).
{: note}

Before you start creating CBR zones and rules, verify that your private service endpoint allowlist is working as expected. After you set up CBR, you can re-run these tests to confirm the same behavior.

1 [Access your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-access_cluster).. Target the private service endpoint from a client system that uses a private IP that is in one of the custom subnets on your allowlist.

1. Run the following command to verify that allowed IPs can connect to the PSE.

    ```sh
    oc get nodes
    ```
    {: pre}


1 [Access your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-access_cluster).. Target the private service endpoint from an IP addressed that is all to verify you can connect.

1 [Access your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-access_cluster).. Target the private service endpoint from a client system that uses a private IP that is **not** allowed in your allowlist.

1. Re-run the previous command again to verify that IPs that aren't in the allowlist can't connect to the PSE.

Now that you've verified your allowlist is working as expected, you can continue with the migration.


## Step 1: Review the details of your allowlist
{: #pse-cbr-review}
{: step}

1. Get your PSE allowlist details.

    If a PSE allowlist is not enabled on your cluster, the command fails and the error indicates that this feature is disabled. In this case, your cluster requires no further action. 
    {: note}

    ```sh
    ibmcloud oc cluster master private-service-endpoint allowlist get -c CLUSTER
    ```
    {: pre}

    Example output

    ```sh
    Subnet             Type     Status
    10.138.53.64/26    System   Active
    10.30.50.0/24      Custom   Active
    10.249.94.103/32   Custom   Active
    OK
    laptop
    ```
    {: screen}

1. Review the output and make a note of the **Custom** subnets. These subnets are used later.
    - The **System** entries are migrated automatically and can be ignored. These entries make sure the cluster workers are allowed to connect to the cluster apiserver.
    - The **Custom** entries are the subnets that you have added that are allowed to connect to this cluster's private service endpoint. The subnets `10.30.50.0/24` and `10.249.94.103/32` in the example are added to a CBR network zone in the next step.


## Step 2: Creating a network zone
{: #pse-cbr-create}
{: cli}

Create a CBR network zone that contains the same subnets as your existing custom private service endpoint allowlist.

### Creating a network zone in the console
{: #pse-cbr-create-ui}
{: ui}

1. [Navigate to the CBR console](https://cloud.ibm.com/context-based-restrictions/zones){: external}.

1. Click **Create**.

1. Provide the details for your network zone.
    - **Name**: Give your network zone a name.
    - **Allowed IP addresses**: Enter the subnets you found in the earlier step.

1. Click **Next** to review the details of your network zone.

1. Click **Create** to finish creating your network zone.


### Creating a network zone by using the CLI
{: #pse-cbr-create-cli}
{: cli}

1. Create a network zone from the CLI by running a command similar to one of the following examples.

    The `cbr zone-create` command syntax.

    ```sh
    ibmcloud cbr zone-create [--name NAME] [--description DESCRIPTION] [--addresses ADDRESSES] [--excluded EXCLUDED] [--vpc VPC] [--service-ref SERVICE-REF] [--file FILE]
    ```
    {: pre}

    The `--addresses` parameter must be a comma separated list of subnets that you found in the step above in your private service endpoint allowlist.
    {: note}

    Example command to create a network zone for a single cluster.
    
    ```sh
    ibmcloud cbr zone-create --name private-subnets-for-cluster-XXXXXX --description "Private subnets that are allowed to access the apisever of cluster XXXXXX" --addresses 10.30.50.0/24,10.249.94.103/32
    ```
    {: pre}

    | Parameter | Description |
    | --- | --- |
    | `--name` |Give your network zone a name. |
    | `--description` | Provide an optional description of the zone. |
    | `--addresses` | Enter the subnets that you found in your master service endpoint allowlist in the previous step. |
    {: caption="CBR zone create example 1" caption-side="bottom"}

    Example command to create a network zone for all clusters in your account.

    ```sh
    ibmcloud cbr zone-create --name private-subnets-for-all-clusters --description "Private subnets that are allowed to access my clusters" --addresses 10.30.50.0/24,10.249.94.103/32
    ```
    {: pre}

    | Parameter | Description |
    | --- | --- |
    | `--name` | Give your network zone a name. |
    | `--description` | Provide an optional description of the zone. |
    | `--addresses` | Enter the subnets that you found in your master service endpoint allowlist in the previous step. |
    {: caption="CBR zone create example 1" caption-side="bottom"}

1. [Create a CBR rule](#pse-cbr-rule) to protect your cluster with CBR. This rule references your cluster, or all clusters in this account, and also references the network zone that you created.


## Step 3: Creating a CBR rule
{: #pse-cbr-rule}

Create a CBR rule that references the network zone that you created. You can create CBR rules in the console, CLI, or API.

### Creating a CBR rule in the console
{: #pse-cbr-rule-ui}

1. Navigate to your network zones in the [CBR console](https://cloud.ibm.com/context-based-restrictions/zones){: external}.

1. Click the **List of actions** on your and click **Edit**.

1. Add or remove subnets, VPCs, or services to your network zone to control which resources can access one or more of your clusters.

### Creating a CBR rule by using the CLI
{: #pse-cbr-rule-cli}


The following instructions describe how to use the CLI to create a network zone.

1. List your network zones and note the ID of the network zone that you created in the earlier step.
    ```sh
    ibmcloud cbr zones
    ```
    {: pre}

2. Create a CBR rule. You can create a rule to protect a single cluster or all clusters in your account.

    The `cbr rule-create` command syntax.

    ```sh
    ibmcloud cbr rule-create [--description DESCRIPTION] [--context-attributes CONTEXT-ATTRIBUTES] [--resource-attributes RESOURCE-ATTRIBUTES] [--region REGION] [--resource RESOURCE] [--resource-group-id RESOURCE-GROUP-ID] [--resource-type RESOURCE-TYPE] [--service-instance SERVICE-INSTANCE-GUID] [--service-name SERVICE-NAME] [--zone-id ZONE-ID] [--tags TAGS] [--enforcement-mode ENFORCEMENT-MODE] [--file FILE]
    ```
    {: pre}

    If your cluster has a public service endpoint, you must include the `--context-attributes endpointType=public` parameter so that traffic is allowed to the public service endpoint. If you don't include this option, all public traffic is blocked.
    {: note}

    Example command that uses the `CLUSTER-ID` of the cluster and the `NETWORK-ZONE-ID` of the network zone from the earlier step to create a CBR rule to protect only this cluster.
    ```sh
    ibmcloud cbr rule-create --api-types crn:v1:bluemix:public:containers-kubernetes::::api-type:cluster --description "Protect private endpoint for cluster CLUSTER" --service-name containers-kubernetes --service-instance CLUSTER-ID --context-attributes endpointType=private,networkZoneId=NETWORK-ZONE-ID --context-attributes endpointType=public
    ```
    {: pre}

    | Parameter | Description |
    | --- | --- |
    | `--api-types` | The `crn:v1:bluemix:public:containers-kubernetes::::api-type:cluster` value indicates the cluster control plane master APIs. For more information about the API types for {{site.data.keyword.openshiftlong_notm}}, see [Protecting specific APIs](/docs/openshift?topic=openshift-cbr&interface=ui#protect-api-types-cbr). |
    | `--description` | An optional description of the rule. |
    | `--service-name containers-kubernetes` | The `containers-kubernetes` value indicates {{site.data.keyword.openshiftlong_notm}} as the target service for the rule. |
    | `--service-instance CLUSTER-ID` | Specify the `CLUSTER-ID` of the cluster you want to protect. |
    | `--context-attributes endpointType=private,networkZoneId=NETWORK-ZONE-ID` | The option allows only resources in the `NETWORK-ZONE-ID` zone to access the cluster's private endpoint. |
    | `--context-attributes endpointType=public` | This option allows all resources to access the cluster's public endpoint. |
    | `networkZoneId` | Specify the `NETWORK-ZONE-ID` of the zone you created earlier. |
    {: caption="CBR rule create example 1" caption-side="bottom"}

    Example command that uses the `NETWORK-ZONE-ID` of the network zone from the earlier step to create a CBR rule that protects all clusters in this account.
    
    ```sh
    ibmcloud cbr rule-create --api-types crn:v1:bluemix:public:containers-kubernetes::::api-type:cluster --description "Protect private endpoint for all clusters" --service-name containers-kubernetes --context-attributes endpointType=private,networkZoneId=NETWORK-ZONE-ID --context-attributes endpointType=public
    ```
    {: pre}

    | Parameter | Description |
    | --- | --- |
    | `--api-types` | The `crn:v1:bluemix:public:containers-kubernetes::::api-type:cluster` value indicates the cluster control plane master APIs. For more information about the API types for {{site.data.keyword.openshiftlong_notm}}, see [Protecting specific APIs](/docs/openshift?topic=openshift-cbr&interface=ui#protect-api-types-cbr). |
    | `--description` | An optional description of the rule. |
    | `--service-name` | The `containers-kubernetes` value indicates {{site.data.keyword.openshiftlong_notm}} as the target service for the rule. |
    | `--context-attributes endpointType=private,networkZoneId=NETWORK-ZONE-ID` | The option allows only resources in the `NETWORK-ZONE-ID` zone to access the cluster's private endpoint. |
    |`--context-attributes endpointType=public` | This options allows all resources to access the cluster's public endpoint. |
    | `networkZoneId` | Specify the `NETWORK-ZONE-ID` of the zone you created earlier. |
    {: caption="CBR rule create example 2" caption-side="bottom"}

When creating a rule, if you see an error message that says `A rule with the same resource attributes already exists`, then you already have a CBR rule protecting your cluster. In this case, you must update your existing rule to add your network zone. For more information, see the [CBR rule-update](/docs/account?topic=account-cbr-plugin#cbr-cli-rule-update-command) documentation.
{: tip}

## Step 4: Disabling the private service endpoint allowlist
{: #pse-cbr-disable}

Now that your cluster's private service endpoint is protected by a CBR rule, you can disable your private service endpoint allowlist.

Run the following command.

```sh
ibmcloud oc cluster master private-service-endpoint allowlist disable -c CLUSTER
```
{: pre}


## Step 5: Testing the CBR rule
{: #pse-cbr-test}

Now that the CBR rule is protecting your cluster's private service endpoint, verify it is working as expected. Run the same tests that you [completed earlier](#pse-cbr-before).

1. {[target_ both]}. 

1. Run the following command against this cluster using a `kubeconfig` that targets the private service endpoint.

    ```sh
    oc get nodes
    ```
    {: pre}

1. Test this command from both a client system using a private IP that is in one of the subnets in the network zone you created (to verify it works), and then from a client system that uses a private IP that is **not** in any of the subnets in the network zone (to verify it fails and times out).

If you find that the behavior is not what you expect, check if there are other CBR rules for the `containers-kubernetes` service that might apply to your cluster, as these might be affecting cluster access as well.
{: tip}


## Step 6: Adding or removing subnets that can access the cluster
{: #pse-cbr-update}

Now that you are using a CBR rule to protect your cluster, you can modify the network zone to specify which subnets can access your cluster.

### Modifying your network zone from the console
{: #pse-zone-update-ui}
{: ui}

1. Navigate to your network zone in the [CBR console](https://cloud.ibm.com/context-based-restrictions/zones){: external}.

1. Select your zone, then click the **List of actions** and click **Edit**.

1. Add or remove subnets, VPCs, or services to your network zone to control which resources can access the chosen clusters.

### Modify your network zone from the CLI
{: #pse-zone-update-cli}
{: cli}

To add subnets that can access your cluster, you can use the `cbr zone-update` command.
```sh
ibmcloud cbr zone-update <NETWORK-ZONE-ID> --name <NETWORK-ZONE-NAME> --addresses <EXISTING-SUBNETS>,<NEW-SUBNETS>
```
{: pre}

Looking at the example for the network zone that was created earlier for all clusters in the account with the two subnets `10.30.50.0/24` and `10.249.94.103/32`. An example command to add a third subnet, `10.10.10.0/24`, would be as follows.

```sh
ibmcloud cbr zone-update <NETWORK-ZONE-ID> --name private-subnets-for-all-clusters --description "Private subnets that are allowed to access my clusters" --addresses 10.30.50.0/24,10.249.94.103/32,10.10.10.0/24
```
{: pre}

You must include all the existing entries in that network zone as well as the ones you want to add. The value you specify for `--addresses` replaces the current address or subnet list in that network zone.
{: note}

To remove subnets from the zone, you can use the same command and omit the subnets you want to remove from the `--addresses` value. In this case, only include the subnets you still want to allow to access your clusters.


## Removing context based restrictions from the private service endpoint
{: #pse-cbr-remove}

## Deleting a rule from the console
{: #pse-cbr-remove-ui}
{: ui}

1. Navigate to your rules in the [CBR console](https://cloud.ibm.com/context-based-restrictions/rules){: external}.

1. Select your rule, then click the **List of actions** and click **Remove**.

1. Add or remove subnets, VPCs, or services to your network zone to control which resources can access your chosen clusters.

## Deleting a rule from the CLI
{: #pse-cbr-remove-cli}
{: cli}

You can delete CBR rules with the `ibmcloud cbr rule-delete <RULE-ID>` or `ibmcloud cbr rule-update <RULE-ID>` command.

To remove CBR protection completely from a cluster or all clusters, you must either delete or disable all CBR rules that affect your cluster.

If you use `ibmcloud cbr rule-update` command to disable or enable an existing rule, you must specify all the attributes of the current rule in addition to the `--enforcement-mode disabled` parameter, otherwise the attributes you omit are removed from the rule.
{: important}


## Next steps
{: #pse-cbr-next}

For more information about CBR, see the following links.

- [Protecting cluster resources with context-based restrictions]/docs/openshift?topic=openshift-cbr&interface=ui).
- [Example context-based restrictions scenarios](/docs/openshift?topic=openshift-cbr-tutorial).
- [CBR CLI reference](/docs/account?topic=account-cbr-plugin).
