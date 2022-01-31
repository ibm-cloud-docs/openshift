---

copyright:
  years: 2014, 2022
lastupdated: "2022-01-31"

keywords: openshift

subcollection: openshift
content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# VPC clusters: Why does the VPC load balancer for Ingress controller only route to one zone?
{: #router-mzr-error}
{: support}

**Supported infrastructure provider**:
* ![VPC infrastructure provider icon.](images/icon-vpc-2.svg) VPC


You create a multizone VPC cluster. However, when you run `ibmcloud is load-balancers` to find the VPC load balancer that exposes the Ingress controller, the VPC subnet for only one zone in your cluster is listed instead of the subnets for all zones in your cluster. In the output, look for the VPC load balancer **Name** that starts with `kube-crtmgr-<cluster_ID>`.
{: tsSymptoms}

```sh
ID                                          Name                                                         Family        Subnets               Is public   Provision status   Operating status   Resource group
r006-d044af9b-92bf-4047-8f77-a7b86efcb923   kube-bsaucubd07dhl66e4tgg-1f4f408ce6d2485499bcbdec0fa2d306   Application   mysubnet-us-south-3   true        active             online             default
```
{: screen}



When you create an {{site.data.keyword.openshiftshort}} cluster on VPC infrastructure in the CLI, the cluster is initially created with worker nodes in one zone only.
{: tsCauses} 

You then make the cluster multizone by manually adding zones to your worker pools with the `ibmcloud oc zone add vpc-gen2` command. Currently, when you add zones to your cluster, the Ingress controller is not updated with the VPC subnets for the new zones, and does not route requests to apps in the new zones.

Restart the Ingress controller so that a new VPC load balancer is created, which registers the Ingress controller behind a hostname and forwards traffic to the Ingress controller. Then, update your Ingress subdomain to use the new VPC load balancer hostname.
{: tsResolve}

1. Run the following command to find the VPC load balancer that exposes the Ingress controller. In the output, look for the VPC load balancer name that starts with `kube-crtmgr-<cluster_ID>`.
    ```sh
    ibmcloud is load-balancers
    ```
    {: pre}
    
    Example output
    
    ```sh
    ID                                          Name                                                         Family        Subnets               Is public   Provision status   Operating status   Resource group
    r006-d044af9b-92bf-4047-8f77-a7b86efcb923   kube-bsaucubd07dhl66e4tgg-1f4f408ce6d2485499bcbdec0fa2d306   Application   mysubnet-us-south-3   true        active             online             default
    ```
    {: screen}

2. Remove the `router-default` service and wait for it to be automatically re-created. 
    ```sh
    oc delete svc router-default -n openshift-ingress
    ```
    {: pre}
    
    After running the `delete svc` command to delete the service, you might need to remove the finalizers to fully remove the service. Run the following command to delete the finalizers on the service. `oc get svc-n openshift-ingress router-default -o=json | jq '.metadata.finalizers = null' | kubectl apply -f -`
    {: note}

3. Verify that the new VPC load balancer that exposes the Ingress controller has **Provision status** of `active` and an **Operating status** of `online`. Also, verify that the **Subnets** list now includes subnets for each zone of your cluster.
    ```sh
    ibmcloud is load-balancers
    ```
    {: pre}

    In the output, look for the VPC load balancer **Name** that starts with `kube-crtmgr-<cluster_ID>`.
    ```sh
    ID                                          Name                                                         Family        Subnets               Is public   Provision status   Operating status   Resource group
    r006-d044af9b-92bf-4047-8f77-a7b86efcb923   kube-bsaucubd07dhl66e4tgg-1f4f408ce6d2485499bcbdec0fa2d306   Application   mysubnet-us-south-1, mysubnet-us-south-2, mysubnet-us-south-3   true        active             online             default
    ```
    {: screen}

4. For the `router-default` service, copy the hostname that is assigned by the new VPC load balancer in the **EXTERNAL-IP** field.
    ```sh
    oc get svc -n openshift-ingress
    ```
    {: pre}

    Example output

    ```sh
    NAME                       TYPE           CLUSTER-IP      EXTERNAL-IP                            PORT(S)                      AGE
    router-default             LoadBalancer   172.21.47.119   1234abcd-us-south.lb.appdomain.cloud   80:32637/TCP,443:31719/TCP   2m
    router-internal-default    ClusterIP      172.21.51.30    <none>                                 80/TCP,443/TCP,1936/TCP      2m
    ```
    {: screen}

5. Get the Ingress subdomain for your cluster.
    ```sh
    ibmcloud oc cluster get -c <cluster_name_or_ID> | grep 'Ingress Subdomain'
    ```
    {: pre}

    Example output

    ```sh
    Ingress Subdomain:              mycluster-35366fb2d3d90fd50548180f69e7d12a-0000.us-south.containers.appdomain.cloud
    ```
    {: screen}

6. Update the Ingress subdomain DNS registration to use the new VPC load balancer hostname.
    ```sh
    ibmcloud oc nlb-dns replace --cluster <cluster_name_or_ID> --nlb-subdomain <Ingress_subdomain> --lb-host <vpc_lb_hostname>
    ```
    {: pre}

7. Verify that the ingress subdomain DNS registration is updated to include the new VPC load balancer hostname for your Ingress controller.
    ```sh
    ibmcloud oc nlb-dns ls -c <cluster_name_or_ID>
    ```
    {: pre}

    Example output

    ```sh
    Subdomain                                                                             Load Balancer Hostname                 SSL Cert Status   SSL Cert Secret Name                            Secret Namespace   
    mycluster-d84d4d2137685d8446c88eacf59b5038-0000.us-south.containers.appdomain.cloud   1234abcd-us-south.lb.appdomain.cloud   created           cluster-d84d4d2137685d8446c88eacf59b5038-0000   openshift-ingress
    ```
    {: screen}



