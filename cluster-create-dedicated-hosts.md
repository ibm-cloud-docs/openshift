---

copyright: 
  years: 2022, 2024
lastupdated: "2024-06-12"


keywords: openshift, clusters, dedicated hosts

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}





# Creating clusters on dedicated hosts for VPC
{: #cluster-create-dedicated-hosts}

[Virtual Private Cloud]{: tag-vpc} 


Follow the steps to create a dedicated host in a dedicated host pool. Then, provision a cluster on your dedicated host infrastructure in the CLI. For steps to create a cluster on dedicated hosts in the console, review the information in [Creating VPC clusters](/docs/openshift?topic=openshift-cluster-create-vpc-gen2&interface=ui).
{: shortdesc}
 
1. List available dedicated host flavors. Note the flavor and flavor class that you want to use to create a dedicated host. 

    ```sh 
    ibmcloud oc flavors --provider vpc-gen2 --zone us-south-1
    ```
    {: pre}

    Example output.

    ```sh
    OK
    For more information about these flavors, see 'https://ibm.biz/flavors' 
    Name                   Cores   Memory   Network Speed  OS             Server Type   Storage   Secondary Storage   Flavor Class   Provider   
    bx2d.16x64             16      64GB     16Gbps         UBUNTU_20_64   virtual       100GB     600GB               bx2d           vpc-gen2   
    bx2d.32x128.600gb      32      128GB    16Gbps         UBUNTU_20_64   virtual       100GB     600GB               bx2d           vpc-gen2   
    bx2d.48x192.900gb      48      192GB    16Gbps         UBUNTU_20_64   virtual       100GB     900GB               bx2d           vpc-gen2
    ...    
    ```
    {: screen}

2. Create a dedicated host pool. Specify the flavor class and metro that you want to use.

    ```sh
    ibmcloud oc dedicated pool create --name my_host_pool --flavor-class bx2d --metro dal
    ```
    {: pre}

3. Verify that the dedicated host pool was created.

    ```sh
    ibmcloud oc dedicated pools      
    ```
    {: pre}

    Example output.

    ```sh
    ID                        Name                    Metro   Flavor Class   Hosts   State   
    dh_a1aaa1111aaa1aaa1a11   my_host_pool            dal     bx2d           0       created   
    ```
    {: screen}

4. Create the dedicated host. Specify the zone, dedicated host pool, and flavor. 

    ```sh
    ibmcloud oc dedicated host create --zone us-south --pool a1a1a1a1a --flavor bx2d.host.16x64
    ```
    {: pre}

5. Verify that the dedicated host was created. If the dedicated host is in the `create_pending` state, wait a few minutes for it to reach the `created` state. 

    ```sh
    ibmcloud oc dedicated host ls --pool a1a1a1a1a
    ```
    {: pre}

    Example output.

    ```sh
    ID                                                Zone         Flavor              State   
    aaaaa-aa-a1aaa1111aaa1aaa1a11-aaaaaaa1-a1aaaa1a   us-south     bx2d.host.16x64     created
    ```
    {: screen}

6. Gather the details required to create a cluster.

    1. List available subnets and note which one you want to use for the cluster. 

        ```sh
        ibmcloud is subnets 
        ```
        {: pre}

        Example output. 

        ```sh
        ID                                          Name        Status      Subnet CIDR       Addresses   ACL                        Public Gateway      VPC      Zone        Resource group   
        1111-a11aaaa1-1a11-1111-1a1a-aaaaa1111111   a1a1a1a1    available   xx.xxx.x.x/xx     xxx/xxx     xxxx-xxxx-xxxx-xxxx        pgw-a1a1a1a1a1a1a   my_vpc   us-east-1   default
        ```
        {: screen}

    1. List available VPCs and note which one you want to use to create the cluster.

        ```sh
        ibmcloud oc vpcs
        ```
        {: pre}

        Example output. 

        ```sh
        Name       ID                                          Provider   
        my_vpc     a111-11a111a1-11a1-1a11-11a1-a1a1111a11a1   vpc-gen2   
        ```
        {: screen}

    1. List available zones and note which one you want to create the cluster in.
    
        ```sh
        ibmcloud oc zones --provider vpc-gen2
        ```
        {: pre}

        Example output. 

        ```sh
        ID           Name         Metro             Flavors  
        us-east-1    us-east-1    Washington D.C.   -   
        us-east-2    us-east-2    Washington D.C.   -   
        us-east-3    us-east-3    Washington D.C.   -   
        us-south-1   us-south-1   Dallas            -   
        us-south-2   us-south-2   Dallas            -   
        us-south-3   us-south-3   Dallas            -   
        ```
        {: screen}


7. Create the cluster. Specify the dedicated host pool, the subnet, vpc and zone you previously noted, and the cluster flavor. Note that it may take several minutes for the cluster to fully provision.

    ```sh
    ibmcloud oc cluster create vpc-gen2  --name my_cluster --flavor bx2d.4x16 --dedicated-host-pool dh_a1aaa1111aaa1aaa1a11  --subnet-id 1111-a11aaaa1-1a11-1111-1a1a-aaaaa1111111 --vpc-id a111-11a111a1-11a1-1a11-11a1-a1a1111a11a1 --zone dal10 --workers 3
    ```
    {: pre}
    

8. Verify that the cluster is created.

    ```sh
    ibmcloud oc cluster ls
    ```
    {: pre}

    Example output.

    ```sh
    Name           ID                   State     Created      Workers   Location    Version                  Resource Group Name   Provider   
    my_cluster    a111a11a11aa1aa11a11  normal    1 hour ago   4         Dallas      1.29.5  default               vpc-gen2
    ```
    {: screen}
    
    
    
    
