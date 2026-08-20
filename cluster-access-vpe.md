---

copyright:
  years: 2014, 2026
lastupdated: "2026-08-20"

keywords: openshift, clusters, access, vpe, virtual private endpoint, vpc, cross-account

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}

# Accessing VPC clusters through the Virtual Private Endpoint gateway
{: #cluster-access-vpe}

A [Virtual Private Endpoint (VPE) gateway](/docs/vpc?topic=vpc-about-vpe) is created automatically for each VPC cluster. The cluster master is accessible through this endpoint if authorized users are connected to the same VPC network, such as through a [VPC VPN](/docs/vpc?topic=vpc-vpn-overview).
{: shortdesc}


For clusters that run version [4.13]{: tag-red}: If you enabled only the private cloud service endpoint during cluster creation, the VPE of your VPC is used by default to access {{site.data.keyword.redhat_openshift_notm}} components such as the web console or OperatorHub. You must be connected to the private VPC network to access these components.
{: note}


## Before you begin
{: #cluster-access-vpe-prereqs}

1. [Install the required CLI tools](/docs/openshift?topic=openshift-cli-install).
1. Configure a [client-to-site](/docs/vpc?topic=vpc-vpn-client-to-site-overview) or [site-to-site](/docs/vpc?topic=vpc-vpn-onprem-example) VPN to your VPC and connect.

## Accessing a VPC cluster through the VPE gateway
{: #cluster-access-vpe-steps}




1. Set the cluster context using the VPE endpoint.
   ```sh
   ibmcloud oc cluster config -c CLUSTER_NAME_OR_ID --endpoint vpe
   ```
   {: pre}

1. Log in to the cluster using one of the following methods.
   - **As admin**: `ibmcloud oc cluster config -c CLUSTER_NAME_OR_ID --admin --endpoint vpe`
   - **With an API key**: See [Accessing clusters from automation tools](/docs/openshift?topic=openshift-cluster-access-automation).
   - **With a passcode**: `oc login -u passcode -p <iam_passcode> --server=https://<VPE_URL>:<port>`

1. Verify access.
   ```sh
   oc version
   ```
   {: pre}


### Protecting clusters using context based restrictions
{: #protect-service-endpoints-with-cbr}

Private service endpoint allowlists are no longer supported.  Migrate from private service endpoint allowlists to context based restrictions as soon as possible. For specific migration steps, see [Migrating from a private service endpoint allowlist to context based restrictions (CBR)](/docs/openshift?topic=openshift-pse-to-cbr-migration).
{: unsupported}

Control access to your public and private service endpoints using context based restriction (CBR) rules.
{: shortdesc}

After you [grant users access to your cluster through {{site.data.keyword.cloud_notm}} IAM](/docs/openshift?topic=openshift-iam-platform-access-roles), you can add a secondary layer of security by creating CBR rules for your cluster's public and private service endpoint. Only authorized requests to your cluster master that originate from subnets in the CBR rules will be allowed.

If you want to allow requests from a different VPC than the one your cluster is in, you must include the cloud service endpoint IP address for that VPC in the CBR rules.
{: note}

For example, to access your cluster's private cloud service endpoint, you must connect to your {{site.data.keyword.cloud_notm}} classic network or your VPC network through a VPN or {{site.data.keyword.dl_full_notm}}. You can specify just the subnet for the VPN or {{site.data.keyword.dl_short}} tunnel to your CBR rules so that only authorized users in your organization can access the private cloud service endpoint from that subnet.

Public CBR rules (if your cluster has a public service endpoint) can also help prevent users from accessing your cluster after their authorization is revoked. When a user leaves your organization, you remove their {{site.data.keyword.cloud_notm}} IAM permissions that grant them access to the cluster. However, the user might have copied the admin `kubeconfig` file for a cluster, giving them access to that cluster. If you have a public CBR rule that only allows access to your cluster masters from known public subnets that your organization owns, then the user's attempted access from another public IP address will be blocked.

Worker node subnets are automatically added to and removed from the backend CBR implementation (but not the CBR rules/zones), so that worker nodes can always access the cluster master and users do not need to specifically add these to their own CBR rules.

To learn more about protecting your cluster with CBR rules, see [Protecting cluster resources with context-based restrictions](/docs/openshift?topic=openshift-cbr) and [Example context-based restrictions scenarios](/docs/openshift?topic=openshift-cbr-tutorial)

## Creating additional VPE gateways in other VPCs and accounts
{: #vpc_cluster_new_vpe_access}

In addition to the VPE gateway that is created for a cluster in its VPC, you can create additional VPE gateways for that cluster to allow access over the private network from other VPCs, regions, and accounts.

* Additional VPE gateways must be created by using the CLI or API. After creation, they can be managed in the web UI.

* For cross-account VPE gateways, you must first create an authorization in the target account. For more information, see [Creating service authorization for cross-account VPE in the console](/docs/vpc?topic=vpc-ordering-cross-account-endpoint-gateway&interface=ui#cross-account-vpe-prerequisite-console).

* No transit gateway or special routing is needed. The VPE gateway handles routing to the target cluster.

The following steps show you how to create a cross-account VPE gateway.

1. Get the necessary information from the target cluster.

    1. Set `ibmcloud target` to the target account, region, and resource group.
    
    1. Get the existing VPE gateway information.
    
        ```sh
        ibmcloud is endpoint-gateway iks-TARGET_CLUSTER_ID
        ```
        {: pre}
    
    1. Note the **Target CRN** (format: `crn:v1:bluemix:public:containers-kubernetes:REGION:a/TARGET_ACCOUNT:TARGET_CLUSTER_ID::`).
    
    1. Note the **Service Endpoints** host names.

2. Create the new VPE gateway in the source account.

    1. Set `ibmcloud target` to the source account, region, and resource group.
    
    1. Verify the VPC exists in this account.
    
        ```sh
        ibmcloud is vpcs
        ```
        {: pre}
    
    1. Create the VPE gateway.
    
        ```sh
        ibmcloud is endpoint-gateway-create --vpc SOURCE_VPC_NAME --target TARGET_CRN --name new-iks-TARGET_CLUSTER_ID --resource-group-name SOURCE_ACCOUNT_RESOURCE_GROUP
        ```
        {: pre}
        
        `SOURCE_VPC_NAME`
        :   The VPC name from the previous step.
        
        `TARGET_CRN`
        :   The CRN from the target cluster's VPE gateway.
        
        `--name`
        :   A name for your VPE gateway.
        
        `SOURCE_ACCOUNT_RESOURCE_GROUP`
        :   The resource group name in the source account.
    
    1. If you get an error `Could not find service`, verify the Target CRN is correct. If correct, you need to create the authorization in the target account. See [Creating service authorization for cross-account VPE in the console](/docs/vpc?topic=vpc-ordering-cross-account-endpoint-gateway&interface=ui#cross-account-vpe-prerequisite-console).

3. Add reserved IPs to your VPE gateway.

    You must add at least one reserved IP. Reserved IPs come from your source VPC subnets (one per zone maximum) and are added to the source VPC's private DNS entries.
    
    1. Create a reserved IP for each zone.
    
        ```sh
        ibmcloud is subnet-reserved-ip-create SOURCE_VPC_SUBNET_NAME --vpc SOURCE_VPC_NAME --name ANY_NAME_YOU_CHOOSE --auto-delete true --target VPE_GATEWAY_NAME
        ```
        {: pre}
    
    1. Optional: Add or modify security groups. By default, only the default security group for the source VPC is attached. For VPE gateways, security groups only protect ingress traffic. Ensure the security groups allow all necessary incoming traffic from clients.

4. Test the connection.

    1. From a VSI in the source VPC, use the same host name as the original VPE gateway. Find this in the **Service Endpoints** list or the **VPE Gateway** property from `ibmcloud ks cluster get -c CLUSTER_NAME`.
    
    1. Verify the connection works.
    
        ```sh
        curl -k https://CLUSTERID...:XXXXX/version
        ```
        {: pre}
    
    1. If the connection fails, check the following:
    
        * Security groups on the VSI and VPE gateway allow the necessary traffic
        * VPC ACL allows the traffic
        * Context Based Restriction (CBR) rules on the target cluster allow private traffic from the source VPC (add the three `Cloud Service Endpoint source addresses` from your source VPC to the private CBR rule)

### Example: Target account commands
{: #vpc_cluster_new_vpe_target_example}

The following example shows commands run in the target account to gather information about the cluster and its VPE gateway.

1. Verify you are targeting the correct account.

    ```sh
    ibmcloud target
    ```
    {: pre}

    Example output

    ```sh
    API endpoint:     https://cloud.ibm.com
    Region:           us-east
    User:             user2@example.com
    Account:          Target Account (9f8e7d6c5b4a321fedcba98765432222) <-> 2222222
    Resource group:   default
    ```
    {: screen}

1. List your clusters.

    ```sh
    ibmcloud ks clusters
    ```
    {: pre}

    Example output

    ```sh
    OK
    Name                     ID                     State    Created     Workers   Location        Version                  Resource Group Name   Provider
    vpe-cross-account-test   c8m5n3p2q4x6z1w7y077   normal   1 day ago   2         Washington DC   4.19.25_1572_openshift   default               vpc-gen2
    ```
    {: screen}

1. Get the VPE gateway details. Note the **Target CRN** and **Service Endpoints**.

    ```sh
    ibmcloud is endpoint-gateway iks-c8m5n3p2q4x6z1w7y077
    ```
    {: pre}

    Example output

    ```sh
    Getting endpoint gateway iks-c8m5n3p2q4x6z1w7y077 under account Target Account as user user2@example.com...
                                     
    ID                            r014-7a228b24-4bc4-416c-aede-7fda14e88d98   
    Name                          iks-c8m5n3p2q4x6z1w7y077
    CRN                           crn:v1:bluemix:public:is:us-east:a/9f8e7d6c5b4a321fedcba98765432222::endpoint-gateway:r014-7a228b24-4bc4-416c-aede-7fda14e88d98
    Target                        CRN      
                                  crn:v1:bluemix:public:containers-kubernetes:us-east:a/9f8e7d6c5b4a321fedcba98765432222:c8m5n3p2q4x6z1w7y077::
                                     
    DNS resolution binding mode   primary   
    Target Type                   provider_cloud_service   
    Target Remote                 ID                        Name   Resource type      
                                  No target remote found.      
                                     
    VPC                           ID                                          Name      
                                  r014-464b4e54-48a8-4f6c-b10a-68edc6fd2be4   new-vpcgen2-default-sec-grp-wdc      
                                     
    Private IPs                   ID                                          Name                                   Address       Subnet ID      
                                  0757-3bd457cb-af5a-4ab6-b9bb-6e78d3eaf752   iks-useast1-c8m5n3p2q4x6z1w7y077-2e8   172.22.0.11   0757-0c981aa5-cb47-41d9-ab29-edee98b416f8
                                     
    Service Endpoints             c8m5n3p2q4x6z1w7y077.vpe.private.us-east.containers.cloud.ibm.com
    Lifecycle State               stable   
    Health State                  ok   
    Security groups               ID                                          Name      
                                  r014-3873358e-3180-482b-927e-abcc300ecbf8   kube-vpegw-c8m5n3p2q4x6z1w7y077
                                     
    Created                       2026-04-03T12:14:59-05:00   
    Resource Group                default
    ```
    {: screen}

1. Optional: Get the cluster details to see the VPE gateway URL.

    ```sh
    ibmcloud ks cluster get -c c8m5n3p2q4x6z1w7y077
    ```
    {: pre}

    Example output

    ```sh
    Retrieving cluster c8m5n3p2q4x6z1w7y077...
    OK
                                    
    Name:                           vpe-cross-account-test
    ID:                             c8m5n3p2q4x6z1w7y077
    State:                          normal
    Status:                         All Workers Normal
    Created:                        2026-04-03 11:56:38 -0500 (1 day ago)
    Resource Group ID:              950cec30388441ce809ca0d18b5ca3bc
    Resource Group Name:            default
    Pod Subnet:                     172.17.0.0/18
    Service Subnet:                 172.21.0.0/16
    Workers:                        2
    Worker Zones:                   us-east-1
    Ingress Subdomain:              vpe-cross-account-test-354226545946e7ee0a2c700f061c1661-0000.us-east.containers.appdomain.cloud
    Ingress Secret:                 vpe-cross-account-test-354226545946e7ee0a2c700f061c1661-0000
    Ingress Status:                 healthy
    Ingress Message:                All Ingress components are healthy.
    Trusted Profile ID:             -
    Public Service Endpoint URL:    https://c111-e.us-east.containers.cloud.ibm.com:31100
    Private Service Endpoint URL:   https://c111.private.us-east.containers.cloud.ibm.com:31100
    Pull Secrets:                   enabled in the default namespace
    VPCs:                           r014-464b4e54-48a8-4f6c-b10a-68edc6fd2be4
    VPE Gateway:                    https://c8m5n3p2q4x6z1w7y077.vpe.private.us-east.containers.cloud.ibm.com:31100
    OAuth Server URL:               https://c111-e.us-east.containers.cloud.ibm.com:31264
    Konnectivity Server URL:        https://c8m5n3p2q4x6z1w7y077.vpe.private.us-east.containers.cloud.ibm.com:30996
    Secure By Default Networking:   enabled
    Outbound Traffic Protection:    enabled
    
    Master      
    Status:     Ready (1 day ago)
    State:      deployed
    Health:     normal
    Version:    4.19.25_1572_openshift
    Location:   Washington DC
    URL:        https://c111-e.us-east.containers.cloud.ibm.com:31100
    ```
    {: screen}

### Example: Source account commands
{: #vpc_cluster_new_vpe_source_example}

The following example shows commands run in the source account to create a VPE gateway that connects to the cluster in the target account.

1. Verify you are targeting the correct source account.

    ```sh
    ibmcloud target
    ```
    {: pre}

    Example output

    ```sh
    API endpoint:     https://cloud.ibm.com
    Region:           us-south
    User:             user1@example.com
    Account:          Source Account (a1b2c3d4e5f6789abcdef01234561111) <-> 1111111
    Resource group:   Default
    ```
    {: screen}

1. List your VPCs.

    ```sh
    ibmcloud is vpcs
    ```
    {: pre}

    Example output

    ```sh
    Listing vpcs in resource group Default and region us-south under account Source Account as user user1@example.com...
    ID                                          Name                      Status      Classic access   Default network ACL                             Default security group                           Resource group   Health state   DNS Hub   DNS Resolver Type   
    r006-6f450c4b-c808-40e7-9de6-c61c262a2ae9   dev-ansiblepr-vpc         available   false            vendor-paradox-ravioli-tank                     harmonica-hypnoses-tranquil-alkalize             Default          ok             false     system   
    r006-bd06a98a-1183-42d2-810d-1c564eeb5f39   fvt-vpc-sdnlb-server-40   available   false            sloppy-program-venue-subsiding                  prattle-pension-wilt-recycled                    Default          ok             false     system   
    r006-ecf65055-6868-4368-aa7c-48fc5ac29ff8   network-fvt-us-south      available   false            doorknob-baffle-quintet-poem                    spotted-sandpaper-auction-unluckily              Default          ok             false     system   
    r006-4ff93772-cee9-4d64-9d87-d8b1b781e201   network-fvt-vpc-gen2      available   false            stegosaur-reach-boxlike-alone-stranger-uncork   earplugs-preface-county-juicy-sensitize-babied   Default          ok             false     system
    ```
    {: screen}

1. Create the VPE gateway using the Target CRN from the target account.

    ```sh
    ibmcloud is endpoint-gateway-create --vpc network-fvt-us-south --target crn:v1:bluemix:public:containers-kubernetes:us-east:a/9f8e7d6c5b4a321fedcba98765432222:c8m5n3p2q4x6z1w7y077:: --name new-iks-c8m5n3p2q4x6z1w7y077 --resource-group-name Default
    ```
    {: pre}

    Example output

    ```sh
    Creating endpoint gateway new-iks-c8m5n3p2q4x6z1w7y077 in resource group Default under account Source Account as user user1@example.com...
                                     
    ID                            r006-2009f147-768a-4f6a-b8fa-75f20456cec2   
    Name                          new-iks-c8m5n3p2q4x6z1w7y077
    CRN                           crn:v1:bluemix:public:is:us-south:a/a1b2c3d4e5f6789abcdef01234561111::endpoint-gateway:r006-2009f147-768a-4f6a-b8fa-75f20456cec2
    Target                        CRN      
                                  crn:v1:bluemix:public:containers-kubernetes:us-east:a/9f8e7d6c5b4a321fedcba98765432222:c8m5n3p2q4x6z1w7y077::
                                     
    DNS resolution binding mode   primary   
    Target Type                   provider_cloud_service   
    Target Remote                 ID                        Name   Resource type      
                                  No target remote found.      
                                     
    VPC                           ID                                          Name      
                                  r006-ecf65055-6868-4368-aa7c-48fc5ac29ff8   network-fvt-us-south      
                                     
    Private IPs                   -   
    Service Endpoints             c8m5n3p2q4x6z1w7y077.vpe.private.us-east.containers.cloud.ibm.com
    Lifecycle State               pending   
    Health State                  ok   
    Security groups               ID                                          Name      
                                  r006-7ae081e2-743d-4046-b755-5ca9997ae077   spotted-sandpaper-auction-unluckily      
                                     
    Created                       2026-04-04T18:17:12-05:00   
    Resource Group                Default
    ```
    {: screen}

1. List the subnets to identify which to use for reserved IPs.

    ```sh
    ibmcloud is subnets --vpc network-fvt-us-south
    ```
    {: pre}

    Example output

    ```sh
    Listing subnets in resource group Default and region us-south under account Source Account as user user1@example.com...
    ID                                          Name                           Status      Subnet CIDR       Addresses   ACL                            Public Gateway                             VPC                    Zone         Resource group   
    0717-04288f84-4aef-4938-9fa7-5544a40ba258   network-fvt-us-south-1-priv    available   10.240.0.0/24     251/256     doorknob-baffle-quintet-poem   -                                          network-fvt-us-south   us-south-1   Default   
    0717-cdd4b20c-b48f-454b-b092-ad7aa14b39c8   network-fvt-us-south-1-pubgw   available   10.240.1.0/24     246/256     doorknob-baffle-quintet-poem   pgw-33eb53d0-74e4-11ee-a747-33927b3ab784   network-fvt-us-south   us-south-1   Default   
    0727-8813de08-fffa-45e3-ae67-2ba70703866e   network-fvt-us-south-2-priv    available   10.240.64.0/24    250/256     doorknob-baffle-quintet-poem   -                                          network-fvt-us-south   us-south-2   Default   
    0727-50b14707-c9f6-4f93-9f49-99de13c66161   network-fvt-us-south-2-pubgw   available   10.240.65.0/24    251/256     doorknob-baffle-quintet-poem   pgw-34fe4a70-74e4-11ee-a747-33927b3ab784   network-fvt-us-south   us-south-2   Default   
    0737-7a644374-f121-44c1-b216-5fd94c0362b2   network-fvt-us-south-3-priv    available   10.240.128.0/24   251/256     doorknob-baffle-quintet-poem   -                                          network-fvt-us-south   us-south-3   Default   
    0737-71a34942-304c-4419-9205-3714a3574962   network-fvt-us-south-3-pubgw   available   10.240.129.0/24   251/256     doorknob-baffle-quintet-poem   pgw-36088e80-74e4-11ee-a747-33927b3ab784   network-fvt-us-south   us-south-3   Default
    ```
    {: screen}

1. Create a reserved IP in the first zone and attach it to the VPE gateway.

    ```sh
    ibmcloud is subnet-reserved-ip-create network-fvt-us-south-1-pubgw --vpc network-fvt-us-south --name reserved-ip-for-us-south-1 --auto-delete true --target new-iks-c8m5n3p2q4x6z1w7y077
    ```
    {: pre}

    Example output

    ```sh
    Creating reserved IP in subnet network-fvt-us-south-1-pubgw under account Source Account as user user1@example.com...
                         
    ID                0717-685e1410-2fa1-4e7a-a4e5-27a097ec7a7a   
    Name              reserved-ip-for-us-south-1   
    Address           0.0.0.0   
    Auto delete       true   
    Owner             user   
    Created           2026-04-04T18:18:51-05:00   
    Lifecycle state   pending   
    Target            ID                                          Name                           Resource type      CRN      
                      r006-2009f147-768a-4f6a-b8fa-75f20456cec2   new-iks-c8m5n3p2q4x6z1w7y077   endpoint_gateway   crn:v1:bluemix:public:is:us-south:a/a1b2c3d4e5f6789abcdef01234561111::endpoint-gateway:r006-2009f147-768a-4f6a-b8fa-75f20456cec2
    ```
    {: screen}

1. Verify the reserved IP was added.

    ```sh
    ibmcloud is eg new-iks-c8m5n3p2q4x6z1w7y077
    ```
    {: pre}

    Example output

    ```sh
    Getting endpoint gateway new-iks-c8m5n3p2q4x6z1w7y077 under account Source Account as user user1@example.com...
                                     
    ID                            r006-2009f147-768a-4f6a-b8fa-75f20456cec2   
    Name                          new-iks-c8m5n3p2q4x6z1w7y077
    CRN                           crn:v1:bluemix:public:is:us-south:a/a1b2c3d4e5f6789abcdef01234561111::endpoint-gateway:r006-2009f147-768a-4f6a-b8fa-75f20456cec2
    Target                        CRN      
                                  crn:v1:bluemix:public:containers-kubernetes:us-east:a/9f8e7d6c5b4a321fedcba98765432222:c8m5n3p2q4x6z1w7y077::
                                     
    DNS resolution binding mode   primary   
    Target Type                   provider_cloud_service   
    Target Remote                 ID                        Name   Resource type      
                                  No target remote found.      
                                     
    VPC                           ID                                          Name      
                                  r006-ecf65055-6868-4368-aa7c-48fc5ac29ff8   network-fvt-us-south      
                                     
    Private IPs                   ID                                          Name                         Address      Subnet ID      
                                  0717-685e1410-2fa1-4e7a-a4e5-27a097ec7a7a   reserved-ip-for-us-south-1   10.240.1.5   0717-cdd4b20c-b48f-454b-b092-ad7aa14b39c8      
                                     
    Service Endpoints             c8m5n3p2q4x6z1w7y077.vpe.private.us-east.containers.cloud.ibm.com
    Lifecycle State               stable   
    Health State                  ok   
    Security groups               ID                                          Name      
                                  r006-7ae081e2-743d-4046-b755-5ca9997ae077   spotted-sandpaper-auction-unluckily      
                                     
    Created                       2026-04-04T18:17:12-05:00   
    Resource Group                Default
    ```
    {: screen}

1. Create a reserved IP in the second zone and attach it to the VPE gateway.

    ```sh
    ibmcloud is subnet-reserved-ip-create network-fvt-us-south-2-pubgw --vpc network-fvt-us-south --name reserved-ip-for-us-south-2 --auto-delete true --target new-iks-c8m5n3p2q4x6z1w7y077
    ```
    {: pre}

    Example output

    ```sh
    Creating reserved IP in subnet network-fvt-us-south-2-pubgw under account Source Account as user user1@example.com...
                         
    ID                0727-d315d943-c501-4f69-823d-bb82a2b13b29   
    Name              reserved-ip-for-us-south-2   
    Address           0.0.0.0   
    Auto delete       true   
    Owner             user   
    Created           2026-04-04T18:19:24-05:00   
    Lifecycle state   pending   
    Target            ID                                          Name                           Resource type      CRN      
                      r006-2009f147-768a-4f6a-b8fa-75f20456cec2   new-iks-c8m5n3p2q4x6z1w7y077   endpoint_gateway   crn:v1:bluemix:public:is:us-south:a/a1b2c3d4e5f6789abcdef01234561111::endpoint-gateway:r006-2009f147-768a-4f6a-b8fa-75f20456cec2
    ```
    {: screen}

1. Create a reserved IP in the third zone and attach it to the VPE gateway.

    ```sh
    ibmcloud is subnet-reserved-ip-create network-fvt-us-south-3-pubgw --vpc network-fvt-us-south --name reserved-ip-for-us-south-3 --auto-delete true --target new-iks-c8m5n3p2q4x6z1w7y077
    ```
    {: pre}

    Example output

    ```sh
    Creating reserved IP in subnet network-fvt-us-south-3-pubgw under account Source Account as user user1@example.com...
                         
    ID                0737-afbebd9f-02bd-4b9a-be90-5bacf9836041   
    Name              reserved-ip-for-us-south-3   
    Address           0.0.0.0   
    Auto delete       true   
    Owner             user   
    Created           2026-04-04T18:19:32-05:00   
    Lifecycle state   pending   
    Target            ID                                          Name                           Resource type      CRN      
                      r006-2009f147-768a-4f6a-b8fa-75f20456cec2   new-iks-c8m5n3p2q4x6z1w7y077   endpoint_gateway   crn:v1:bluemix:public:is:us-south:a/a1b2c3d4e5f6789abcdef01234561111::endpoint-gateway:r006-2009f147-768a-4f6a-b8fa-75f20456cec2
    ```
    {: screen}

1. Verify all reserved IPs were added.

    ```sh
    ibmcloud is eg new-iks-c8m5n3p2q4x6z1w7y077
    ```
    {: pre}

    Example output

    ```sh
    Getting endpoint gateway new-iks-c8m5n3p2q4x6z1w7y077 under account Source Account as user user1@example.com...
                                     
    ID                            r006-2009f147-768a-4f6a-b8fa-75f20456cec2   
    Name                          new-iks-c8m5n3p2q4x6z1w7y077
    CRN                           crn:v1:bluemix:public:is:us-south:a/a1b2c3d4e5f6789abcdef01234561111::endpoint-gateway:r006-2009f147-768a-4f6a-b8fa-75f20456cec2
    Target                        CRN      
                                  crn:v1:bluemix:public:containers-kubernetes:us-east:a/9f8e7d6c5b4a321fedcba98765432222:c8m5n3p2q4x6z1w7y077::
                                     
    DNS resolution binding mode   primary   
    Target Type                   provider_cloud_service   
    Target Remote                 ID                        Name   Resource type      
                                  No target remote found.      
                                     
    VPC                           ID                                          Name      
                                  r006-ecf65055-6868-4368-aa7c-48fc5ac29ff8   network-fvt-us-south      
                                     
    Private IPs                   ID                                          Name                         Address        Subnet ID      
                                  0737-afbebd9f-02bd-4b9a-be90-5bacf9836041   reserved-ip-for-us-south-3   10.240.129.5   0737-71a34942-304c-4419-9205-3714a3574962      
                                  0717-685e1410-2fa1-4e7a-a4e5-27a097ec7a7a   reserved-ip-for-us-south-1   10.240.1.5     0717-cdd4b20c-b48f-454b-b092-ad7aa14b39c8      
                                  0727-d315d943-c501-4f69-823d-bb82a2b13b29   reserved-ip-for-us-south-2   10.240.65.5    0727-50b14707-c9f6-4f93-9f49-99de13c66161      
                                     
    Service Endpoints             c8m5n3p2q4x6z1w7y077.vpe.private.us-east.containers.cloud.ibm.com
    Lifecycle State               stable   
    Health State                  ok   
    Security groups               ID                                          Name      
                                  r006-7ae081e2-743d-4046-b755-5ca9997ae077   spotted-sandpaper-auction-unluckily      
                                     
    Created                       2026-04-04T18:17:12-05:00   
    Resource Group                Default
    ```
    {: screen}

1. Test the connection from a VSI in the source VPC.

    ```sh
    curl -k https://c8m5n3p2q4x6z1w7y077.vpe.private.us-east.containers.cloud.ibm.com:31100/version
    ```
    {: pre}

    Example output

    ```sh
    {
      "major": "1",
      "minor": "32",
      "gitVersion": "v1.32.12",
      "gitCommit": "9b706b45b52a0c8bb05847295ee98ffccbabba32",
      "gitTreeState": "clean",
      "buildDate": "2026-02-19T13:30:47Z",
      "goVersion": "go1.23.10 (Red Hat 1.23.10-10.el9) X:strictfipsruntime",
      "compiler": "gc",
      "platform": "linux/amd64"
    }
    ```
    {: screen}

1. Verify the host name resolves to a reserved IP.

    ```sh
    dig +short c8m5n3p2q4x6z1w7y077.vpe.private.us-east.containers.cloud.ibm.com
    ```
    {: pre}

    Example output

    ```sh
    10.240.65.5
    ```
    {: screen}
