---

copyright: 
  years: 2023, 2023
lastupdated: "2023-02-10"

keywords: openshift, subnet, detach

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}


# I deleted a portable subnet and now my Classic cluster my Load Balancers are failing. How do I recover?
{: #ts-network-subnet-recover}
{: support}

[Classic]{: tag-classic}

You cluster is experiencing network errors.
{: tsSymptoms}

A portable subnet was deleted.
{: tsCauses}

Complete the following steps.
{: tsResolve}


1. For the cluster that is experiencing issues, run the following command and make a note of the cluster ID.
    ```sh
    ibmcloud oc cluster ls
    ```
    {: pre}


1. List the subnets your cluster is using. In the output, make a note of the subnets that your cluster is using.
    ```sh
    ibmcloud oc subnets --provider classic | grep CLUSTER-ID
    ```
    {: pre}


1. List the subnets in your account. Check whether any subnets that you found in step 1 are missing from the list of subnets in your account. This means your cluster is using a subnet that was deleted, which is causing your Load Balancer to fail.
    
    ```sh
    ibmcloud sl subnet list
    ```
    {: pre}
    
    ```sh
    ibmcloud sl subnet detail SUBNET-ID
    ```
    {: pre}


1. For each subnet that was deleted, re-create it. If you need public IP addresses for your ALBs or LoadBalancers, specify the public VLAN ID of your worker nodes; for private IPs specify the private VLAN ID of your worker nodes.
    ```sh
    ibmcloud oc cluster subnet create -c CLUSTER --size 8 --vlan VLAN-ID
    ```
    {: pre}




1. Find any LoadBalancers that use IP addresses in the deleted portable subnets, save them, and then delete them. Do not delete the LoadBalancers in the `openshift-ingress` namespace, as those are deleted later in these steps.
    1. Find your LoadBalancer details and make a note of the IP addresses they use.
        ```sh
        kubectl get svc -A -o wide | grep LoadBalancer
        ```
        {: pre}
    
    1. For each LoadBalancer not in the `openshift-ingress` namespace that uses a portable IP address, save the settings to a YAML file.
      ```sh
      kubectl get svc -o yaml -n LB-NAMESPACE LB-NAME > LB-NAMESPACE.LB-NAME.yaml
      ```
      {: pre}

    1. Delete the LoadBalancer.
        ```sh
        kubectl delete svc -n LB-NAMESPACE LB-NAME
        ```
        {: pre}

1. Complete the following steps quickly, because the portable subnet must be detached before the `openshift-ingress-operator` pod restarts and re-creates the LoadBalancers.

    1. Scale down the Ingress operator.
        ```sh
        kubectl scale deploy -n openshift-ingress-operator ingress-operator --replicas 0
        ```
        {: pre}

    1. Delete the LoadBalancers in the `openshift-ingress` namespace.
        ```sh
        kubectl delete svc -n openshift-ingress LB-NAME
        ```
        {: pre}

    1. Detach the portable subnets from your cluster.
        ```sh
        ibmcloud oc cluster subnet detach -c CLUSTER-ID --subnet-id SUBNET-ID
        ```
        {: pre}


1. Wait a few minutes for the detach command to finish, then check that they have been detached by reviewing the `ibm-cloud-provider-vlan-ip-config` ConfigMap that stores the subnets and IP addresses.
    ```sh
    kubectl get cm -n kube-system ibm-cloud-provider-vlan-ip-config -o yaml
    ```
    {: pre}

    It might take 5-10 minutes for the detach to complete. While you wait, you can ensure that the new portable subnets you created for this cluster also appear in the ConfigMap.
    {: note}
  
1. Check whether the LoadBalancers in the `openshift-ingress` namespace re-created, and if so, check whether the IP addresses used are from the new subnets. If they are from the old subnets, then delete them again by using the **`kubectl delete svc -n openshift-ingress LOADBALANCER_NAME`** command.

1. After the `openshift-ingress` LoadBalancers  re-create with IP addresses from the new subnets, add the new IP addresses to the DNS record.

    1. List the DNS entries.
        ```sh
        ibmcloud oc nlb-dns ls -c CLUSTER-ID
        ```
        {: pre}

    1. In the output, find the `openshift-ingress` entries, and add the new IP address(es) to them by using the following command.
        ```sh
        ibmcloud ks nlb-dns add -c CLUSTER-ID --ip NEW-LOADBALANCE-IP --nlb-host INGRESS-DOMAIN-NAME
        ```
        {: pre}
        
    1. Remove the old IPs.
        ```sh
        ibmcloud oc nlb-dns rm classic -c CLUSTER-ID --ip OLD-LOADBALANCER-IP --nlb-host INGRESS-DOMAIN-NAME
        ```
        {: pre}

1. Re-create any LoadBalancers not in the `openshift-ingress` namespace that you deleted in step 3 by by using the YAML file that you saved earlier.
    ```sh
    kubectl apply -f LB-NAMESPACE.LB-NAME.yaml
    ```
    {: pre} 


