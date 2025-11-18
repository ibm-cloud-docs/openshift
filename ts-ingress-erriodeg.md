---

copyright:
  years: 2022, 2025
lastupdated: "2025-11-18"


keywords: openshift, ingress, troubleshoot ingress, ingress operator, ingress cluster operator, ingress operator degraded, erriodeg

subcollection: openshift
content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}



# Why does the Ingress status show an `ERRIODEG` error?
{: #ts-ingress-erriodeg}
{: troubleshoot}
{: support}



[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [{{site.data.keyword.satelliteshort}}]{: tag-satellite}

You can use the `ibmcloud oc ingress status-report ignored-errors add` command to add an error to the ignored-errors list. Ignored errors still appear in the output of the `ibmcloud oc ingress status-report get` command, but are ignored when calculating the overall Ingress Status.
{: tip}

When you check the status of your cluster's Ingress components by running the `ibmcloud oc ingress status-report get` command, you see an error similar to the following.
{: tsSymptoms}

```sh
The Ingress Operator is in a degraded state (ERRIODEG).
```
{: screen}

The Ingress Operator checks the health of the Ingress Controllers and enters a degraded state when the checks fail.
{: tsCauses}


Get the details of the `ingress` ClusterOperator and complete the steps based on the error message.
{: tsResolve}


Check the status of the `ingress` ClusterOperator. If you see `False` in the `DEGRADED` column, wait 10 to 15 minutes to see if the Ingress Status warning disappears. If not, proceed with the troubleshooting steps based on the message in the `MESSAGE` column.
```sh
oc get clusteroperator ingress
```
{: pre}


## One or more status conditions indicate unavailable: `DeploymentAvailable=False`
{: #ts-ingress-erriodeg-da-false}

1. Ensure that your cluster has at least two workers. For more information, see [Adding worker nodes to Classic clusters](/docs/openshift?topic=openshift-add-workers-classic) or [Adding worker nodes to VPC clusters](/docs/openshift?topic=openshift-add-workers-vpc).
1. Ensure that your cluster workers are healthy, otherwise Ingress Controller pods cannot be scheduled. For more information, see [Worker node states](/docs/openshift?topic=openshift-worker-node-state-reference).

## One or more status conditions indicate unavailable: `LoadBalancerReady=False`
{: #ts-ingress-erriodeg-lbr-false}

1. **VPC only**: Ensure that you did not reach your LBaaS instance quota. For more information, see [Quotas and service limits](/docs/vpc?topic=vpc-quotas#alb-quotas) and the `ibmcloud is load-balancers` [command](/docs/vpc?topic=vpc-vpc-reference#lb-anchor).
1. Ensure that your cluster masters are healthy. For more information, see [Reviewing master health](/docs/openshift?topic=openshift-debug_master#review-master-health).
1. Refresh your cluster masters by running the `ibmcloud oc cluster master refresh` [command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_apiserver_refresh).

## One or more other status conditions indicate a degraded state: `CanaryChecksSucceeding=False`
{: #ts-ingress-erriodeg-ccs-false}

1. [Access your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-access_cluster).

1. Ensure that the correct LoadBalancer service address is registered for your Ingress subdomain.
    1. Run the `ibmcloud oc cluster get` [command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_cluster_get) to see your Ingress subdomain.
    1. Run the `ibmcloud oc nlb-dns get` [command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_nlb-dns-get) to see the registered addresses.
    1. Run the `oc get services -n openshift-ingress` command to get the actual load balancer addresses.
    1. Compare the registered and actual addresses and update the subdomain if it differs.
        **VPC**: Run the `ibmcloud oc nlb-dns replace` [command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_nlb-dns-replace) to replace the current address.
        **Classic**: Remove the currently registered addresses by running the `ibmcloud oc nlb-dns rm classic` [command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_nlb-dns-rm), then add the new addresses with the `ibmcloud oc nlb-dns add` [command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_nlb-dns-add).
        **Satellite**: The actual addresses depends on your configuration: if you expose your worker nodes with an external load balancer, register the load balancer addresses, otherwise register the IP addresses assigned to the `router-external-default` service in the `openshift-ingress` namespace (use the `oc get services -n openshift-ingress router-external-default -o yaml` command to retrieve the addresses). Remove the currently registered addresses by running the `ibmcloud oc nlb-dns rm classic` [command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_nlb-dns-rm), then add the new addresses with the `ibmcloud oc nlb-dns add` [command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_nlb-dns-add).

1. **VPC only**: canary health check traffic originates from one of the worker nodes of your cluster.
    - Health check traffic originates from one of the worker nodes of your cluster. In the case of clusters with public service endpoint, the traffic is directed to the public floating IP address of the VPC Load Balancer instance, therefore it is required to have a Public Gateway attached to all the worker subnets. In the case of clusters with only private service endpoints, the traffic is directed to the VPC subnet IP address of the VPC Load Balancer, therefore a Public Gateway is not required. For clusters with public service endpoint:
        1. Run the `ibmcloud is public-gateways` to see your public gateways.
        1. Run the `ibmcloud is subnets` to see your subnets.
        1. For every subnet run the `ibmcloud is subnet <subnet-id>` to check whenever it has a public gateway.
            1. If your subnet does not have a public gateway attached, you need to attach one. For more information, see [Creating public gateways](/docs/vpc?topic=vpc-create-public-gateways&interface=cli)
    - If your VPC Load Balancers are located on a subnet other than the worker nodes of your cluster, you must update the Security Group attached to the VPC Load Balancer subnet to allow incoming traffic from the worker subnets.
    - For more information, see [Creating a Red Hat OpenShift cluster in your Virtual Private Cloud](/docs/openshift?topic=openshift-vpc_rh_tutorial), [Configuring VPC subnets](/docs/openshift?topic=openshift-vpc-subnets#vpc_basics_pgw) and [Creating and managing VPC security groups](/docs/openshift?topic=openshift-vpc-security-group-manage).

1. Ensure that no firewall rules block the canary traffic.
    **VPC**: canary traffic originates from one of the worker nodes, flows through a VPC Public Gateway and arrives to the public side of the VPC Load Balancer instance. Configure your VPC Security Groups to allow this communication. For more information, see [Understanding secure by default cluster VPC networking](/docs/openshift?topic=openshift-vpc-security-group-reference) and [Creating and managing VPC security groups](/docs/openshift?topic=openshift-vpc-security-group-manage).
    **Classic**: canary traffic originates from the public IP address of one of the worker nodes and arrives to the public IP address of your classic load balancers. Configure your network policies to allow this communication. For more information, see [Controlling traffic with network policies on classic clusters](/docs/openshift?topic=openshift-network_policies).

## Next steps
{: #ts-ingress-erriodeg-next}

1. Wait 30 minutes, then run the `oc get clusteroperator ingress` command and check the `MESSAGE` column again.
1. If you see a different error message repeat the troubleshooting steps.
1. If the issue persists, contact support. Open a [support case](/docs/account?topic=account-using-avatar). In the case details, be sure to include any relevant log files, error messages, or command outputs.
