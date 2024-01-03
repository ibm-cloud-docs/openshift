---

copyright: 
  years: 2023, 2024
lastupdated: "2024-01-03"


keywords: openshift, errsamo, loadbalancer service missing

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}



# Why does the Ingress status show an `ERRSAMO` error?
{: #ts-ingress-errsamo}
{: troubleshoot}
{: support}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf}

You can use the the `ibmcloud oc ingress status-report ignored-errors add` command to add an error to the ignored-errors list. Ignored errors still appear in the output of the `ibmcloud oc ingress status-report get` command, but are ignored when calculating the overall Ingress Status.
{: tip}


When you check the status of your cluster's Ingress components by running the `ibmcloud oc ingress status-report get` command, you see an error similar to the following example.
{: tsSymptoms}


```sh
The load balancer service address is missing (ERRSAMO).
```
{: screen}

The load balancer service that exposes your Ingress Controller doesn't have an address assigned.
{: tsCauses}

Complete the following steps to troubleshoot the issue.
{: tsResolve}

1. Ensure that your cluster masters and workers are healthy.
    - [Review master health](/docs/openshift?topic=openshift-debug_master#review-master-health)
    - [Review worker node states](/docs/openshift?topic=openshift-worker-node-state-reference).
1. List your load balancer services.
    
    ```sh
    oc get services -n openshift-ingress | grep LoadBalancer
    ```
    {: pre}

    
    
1. Identify services that do not have an address in the `EXTERNAL-IP` column.

1. Look for an event that references the following services.
    
    ```sh
    oc get events -n openshift-ingress| grep SERVICE
    ```
    {: pre}
    
    
    
1. Review contents of the `MESSAGE` column and complete the following steps based on your cluster type and error message.
    - If you see errors regarding your API key, you can try resetting the API key with the **`ibmcloud oc api-key reset`** [command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_api_key_reset).
    - **Classic**: If you see errors regarding your load balancer deployment, ensure your cluster has at least two healthy workers. For more information, see [Adding worker nodes and zones to clusters](/docs/openshift?topic=openshift-add-workers-classic).
    
    - **Classic**: If you see errors saying that no IPs are available, add new portable subnets to the cluster with the **`ibmcloud oc cluster subnet create`** [command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_cluster_subnet_create).
    - **VPC**: If you see permission issues, review your IAM permissions. For more information, see [Setting up an Application Load Balancer for VPC](/docs/openshift?topic=openshift-vpc-lbaas#setup_vpc_ks_vpc_lb).
    - **VPC**: Ensure that you did not reach your LBaaS instance quota. For more information, see [Quotas and service limits](/docs/vpc?topic=vpc-quotas#alb-quotas) and **`ibmcloud is load-balancers`** [command](/docs/vpc?topic=vpc-vpc-reference#lb-anchor).
    
1. Wait 10 to 15 minutes, then check if the load balancer got an address assigned. If not, check the events again.

1. If you see a different error, repeat the troubleshooting steps. If the issue persists, contact support. Open a [support case](/docs/get-support?topic=get-support-using-avatar). In the case details, be sure to include any relevant log files, error messages, or command outputs.



