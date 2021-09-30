---

copyright: 
  years: 2014, 2021
lastupdated: "2021-09-30"

keywords: openshift, roks, rhoks, rhos

subcollection: openshift
content-type: troubleshoot

---




{{site.data.keyword.attribute-definition-list}}



# Checking the status of Ingress components
{: #ingress-status}

**Infrastructure provider**:
* <img src="images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Classic
* <img src="images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> VPC

## Getting the status and message
{: #check_status}

To check the overall health and status of your cluster's Ingress components:
{: shortdesc}

```sh
ibmcloud oc ingress status -c <cluster_name_or_ID>
```
{: pre}

The state of the Ingress components are reported in an **Ingress Status** and **Ingress Message**. Example output:
```
Ingress Status:   healthy
Message:          All Ingress components are healthy

Component                                        Status    Type
public-crdf253b6025d64944ab99ed63bb4567b6-alb1   healthy   alb
public-crdf253b6025d64944ab99ed63bb4567b6-alb2   healthy   alb
```
{: screen}

The **Ingress Status** and **Ingress Message** fields are also returned in the output of the `ibmcloud oc cluster get` command. The health of your Ingress components might impact the health of your cluster master. For example,  if your Ingress components are unhealthy, your cluster master might show a `warning` state. However, the health of your Ingress components does not cause your master health to become `critical`.
{: tip}


## Ingress statuses
{: #ingress_status}

The Ingress Status reflects the overall health of the Ingress components.
{: shortdesc}

|Ingress status|Description|
|--- |--- |
|`healthy` |The Ingress components are healthy. Check the **Ingress Message** field to verify that all operations for the Ingress components are complete.|
|`warning` |The Ingress components might not function properly due to errors. Check the **Ingress Message** field for more information and troubleshooting.|
{: caption="Ingress statuses"}
{: summary="Table rows read from left to right, with the Ingress status in column one and a description in column two."}

## Ingress messages
{: #ingress_message}

The Ingress Message provides details of what operation is in progress or information about any components that are unhealthy. Each status and message is described in the following tables.
{: shortdesc}

|Ingress message|Description|
|--- |--- |
|`ALB is disabled` |Version 3.11: Your public ALBs were manually disabled. For more information, see the [`ibmcloud oc ingress alb enable` CLI command reference](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_alb_configure).|
|`ALB is unhealthy or unreachable` |Version 3.11: One or more ALB IP addresses cannot be reached. For troubleshooting information, see [Ping the ALB subdomain and public IP addresses](/docs/containers?topic=containers-ingress-debug#ping).|
|`ALBs are not health checked in clusters created with no subnets` |Ingress health reporting is not supported for classic clusters that were created with the `--no-subnet` flag.|
|`ALBs cannot be created because no portable subnet is available` |Version 3.11: 1Each ALB is created with a portable public or private IP address from the public or private subnet on the VLANs that your classic cluster is connected to. If no portable IP address is available, the ALB is not created. You might need to add a new subnet to your cluster or order a new VLAN. For troubleshooting information, see [Classic clusters: Why does the ALB not deploy in a zone?](/docs/containers?topic=containers-cs_subnet_limit).|
|`All Ingress components are healthy` |The Ingress components are successfully deployed and are healthy.|
|`Creating Ingress ALBs` |Version 4: Your ALBs are currently deploying. Wait until your ALBs are fully deployed to review the health of your Ingress components. Note that ALB creation can take up to 15 minutes to complete. |
|`Creating TLS certificate for Ingress subdomain, which might take several minutes. Ensure you have the correct IAM permissions.` |The default Ingress subdomain for your cluster is created with a default TLS certificate, which is stored in the **Ingress Secret**. The certificate is currently being created and stored in the default {{site.data.keyword.cloudcerts_long_notm}} instance for your cluster.<p class="note">When the creation of the {{site.data.keyword.cloudcerts_short}} instance is triggered, the {{site.data.keyword.cloudcerts_short}} instance might take up to an hour to become visible in the {{site.data.keyword.cloud_notm}} console. If this message continues to be displayed, see [Why does no Ingress secret exist after cluster creation?](/docs/containers?topic=containers-ingress_secret).</p>|
|`Could not create a Certificate Manager instance. Ensure you have the correct IAM platform permissions.` | A default {{site.data.keyword.cloudcerts_long_notm}} instance for your cluster was not created to store the TLS certificate for the Ingress subdomain. The API key for the resource group and region that your cluster is in does not have the correct IAM permissions for {{site.data.keyword.cloudcerts_short}}. For troubleshooting steps, see [Why does no Ingress secret exist after cluster creation?](/docs/containers?topic=containers-ingress_secret).|
|`Could not upload certificates to Certificate Manager instance. Ensure you have the correct IAM service permissions.` |The TLS certificate for your cluster's default Ingress subdomain is created, but cannot be stored in the default {{site.data.keyword.cloudcerts_long_notm}} instance for your cluster. The API key for the resource group and region that your cluster is in does not have the correct IAM permissions for {{site.data.keyword.cloudcerts_short}}. For troubleshooting steps, see [Why does no Ingress secret exist after cluster creation?](/docs/containers?topic=containers-ingress_secret).|
|`Deploying router for Ingress controller` |Version 4: The router and router service that expose your Ingress controller are currently deploying to the cluster. If this message continues to be displayed, a router pod might be unable to deploy because only 1 worker node exists in the zone. Two worker nodes are required per zone so that the 2 replicas of the router can be deployed and updated correctly. For more information, see [Adding worker nodes to clusters](/docs/openshift?topic=openshift-add_workers). |
|`Ingress status is not supported for cluster type` |Ingress health reporting is currently not supported for {{site.data.keyword.openshiftshort}} clusters.|
|`Load balancer service for ALB or router is not ready` |Version 4: The router and router service that expose your Ingress controller did not correctly deploy to your cluster. For troubleshooting information, see [Version 4: Why doesn't the router for Ingress controller deploy in a zone?](/docs/openshift?topic=openshift-cs_subnet_limit_43).|
|`No workers found in this zone` | Router pods cannot deploy to a zone because no worker nodes match the pod affinity requirements. To ensure that you have the minimum required worker nodes per zone, see [Why do ALB pods not deploy to worker nodes?](/docs/containers?topic=containers-alb-pod-affinity).|
|`One or more ALBs are unhealthy` |Version 3.11: The external IP address for one or more of your ALBs was reported as unhealthy. For troubleshooting information, see [Ping the ALB subdomain and public IP addresses](/docs/containers?topic=containers-ingress-debug#ping).|
|`One or more routers are unhealthy` |Version 4: The external IP address for one or more routers was reported as unhealthy. For troubleshooting information, see [Check the health of the Ingress controller's router](/docs/openshift?topic=openshift-ingress-debug-roks4#errors-43), and if the issue is not addressed, continue to the next section to [Ping the Ingress subdomain and router public IP address](/docs/openshift?topic=openshift-ingress-debug-roks4#ping-43). |
|`Registering Ingress subdomain` |The default **Ingress Subdomain** for your cluster is currently being created. The Ingress subdomain and secret creation follows a process that might take more than 15 minutes to complete. For troubleshooting information, see [Why does no Ingress subdomain exist after cluster creation?](/docs/openshift?topic=openshift-ingress_subdomain).|
|`Router service is unhealthy or unreachable` |Version 4: The external IP address for one or more router services that expose Ingress controllers was reported as unhealthy or was unreachable, or one or more router services did not correctly deploy to your cluster. For troubleshooting information, see [Ping the Ingress subdomain and router public IP address](/docs/openshift?topic=openshift-ingress-debug-roks4#ping-43).|
|`The expiration dates reported by Ingress secrets are out of sync across namespaces.` | To resynchronize the expiration dates, [regenerate the secrets for your Ingress subdomain certificate](/docs/containers?topic=containers-sync_cert_dates).|
{: caption="Ingress messages"}
{: summary="Table rows read from left to right, with the Ingress message in column one and a description in column two."}




