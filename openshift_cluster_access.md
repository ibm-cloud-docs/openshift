---

copyright:
  years: 2014, 2022
lastupdated: "2022-07-15"

keywords: openshift, clusters, access, endpoint

subcollection: openshift

---


{{site.data.keyword.attribute-definition-list}}



# Accessing {{site.data.keyword.redhat_openshift_notm}} clusters
{: #access_cluster}
{: help}
{: support}

After your {{site.data.keyword.openshiftlong}} cluster is created, you can begin working with your cluster by accessing the cluster.
{: shortdesc}

## Prerequisites
{: #prereqs}

1. [Install the required CLI tools](/docs/openshift?topic=openshift-openshift-cli), including the {{site.data.keyword.cloud_notm}} CLI, {{site.data.keyword.containershort_notm}} plug-in alias for {{site.data.keyword.redhat_openshift_notm}} (`ibmcloud oc`), and {{site.data.keyword.redhat_openshift_notm}} CLI (`oc`). For quick access to test features in your cluster, you can also use the [{{site.data.keyword.cloud-shell_notm}}](/docs/openshift?topic=openshift-openshift-cli#cloud-shell).
2. [Create your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-clusters).
3. If your network is protected by a company firewall, [allow access](/docs/openshift?topic=openshift-firewall#corporate) to the {{site.data.keyword.cloud_notm}} and {{site.data.keyword.openshiftlong_notm}} API endpoints and ports. For VPC clusters with only the private cloud service endpoint enabled, you can't test the connection to your cluster until you [configure a VPC VPN with the cloud service endpoint subnet](#vpc_private_se).
4. Check that your cluster is in a healthy state by running `ibmcloud oc cluster get -c <cluster_name_or_ID>`. If your cluster is not in a healthy state, review the [Debugging clusters](/docs/openshift?topic=openshift-debug_clusters) guide for help. For example, if your cluster is provisioned in an account that is protected by a firewall gateway appliance, you must [configure your firewall settings to allow outgoing traffic to the appropriate ports and IP addresses](/docs/openshift?topic=openshift-firewall).
5. Find your cluster's service endpoint.
    * **Classic or VPC clusters**: In the output of the cluster details from the previous step, check the **Public** or **Private Service Endpoint** URL of the cluster.
        *  Public Service Endpoint URL only: Continue with [Accessing clusters through the public cloud service endpoint](#access_public_se).
        *  Both service endpoint URLs: You can access your cluster either through the [public](#access_public_se) or the [private](#access_private_se) service endpoint.
    * **{{site.data.keyword.satellitelong_notm}} clusters**: Continue with [Accessing clusters on {{site.data.keyword.satelliteshort}}](#access_cluster_sat).
6. If any users in your account use multifactor authentication (MFA) like TOTP, make sure that you [enabale it for all users at the account level](/docs/account?topic=account-enablemfa). To use MFA, it must be enabled at the account level in order to avoid authentication errors. 




## Accessing clusters through the public cloud service endpoint
{: #access_public_se}

For {{site.data.keyword.redhat_openshift_notm}} clusters with a public cloud service endpoint, you can log in to your cluster from the console or CLI.
{: shortdesc}

### Connecting to the cluster from the console
{: #access_oc_console}

You can quickly access your {{site.data.keyword.openshiftlong_notm}} cluster from the console.
{: shortdesc}

1. In the [{{site.data.keyword.redhat_openshift_notm}} clusters console](https://cloud.ibm.com/kubernetes/clusters?platformType=openshift){: external}, click the cluster that you want to access.
2. Click **{{site.data.keyword.redhat_openshift_notm}} web console**.
3. To continue working in the command line, click your profile name, such as `IAM#name@email.com`, and then click **Copy Login Command**. Depending on your cluster version, log in to your cluster from the command line as follows.
    *  **Version 3.11**: Paste the copied `oc login` command into your command line.
    *  **Version 4**: Click **Display Token**, copy the `oc login` command, and paste the command into your command line.

For security reasons, first log out of the {{site.data.keyword.cloud_notm}} console and then log out of the {{site.data.keyword.redhat_openshift_notm}} web console before you close your browser. You must complete both steps in the specified order to successfully log out of the {{site.data.keyword.redhat_openshift_notm}} web console.
{: note}   

**What's next?** Try [Deploying apps through the console](/docs/openshift?topic=openshift-deploy_app#deploy_apps_ui).

### Connecting to the cluster from the CLI
{: #access_oc_cli}

Usually, you can use the {{site.data.keyword.redhat_openshift_notm}} web console to get the `oc login` token to access your cluster. If you can't or don't want to open the {{site.data.keyword.redhat_openshift_notm}} console, choose among the following options to log in to your {{site.data.keyword.openshiftlong_notm}} cluster by using the CLI.
{: shortdesc}

Choose from the following options.
*   **Log in as admin**:
    1. Make sure that you have the [**Administrator** platform access role for the cluster](/docs/openshift?topic=openshift-users#add_users).
    2. Set your command line context for the cluster and download the TLS certificates and permission files for the administrator.
        ```sh
        ibmcloud oc cluster config -c <cluster_name_or_ID> --admin
        ```
        {: pre}

*   **Log in with an API key**: See [Using an API key to log in to {{site.data.keyword.redhat_openshift_notm}}](/docs/openshift?topic=openshift-access_cluster#access_api_key).
*   **Log in with {{site.data.keyword.cloud_notm}} passcode**:
    1. Get the **Master URL** of your cluster in the output of the following command.
        ```sh
        ibmcloud oc cluster get -c <cluster_name_or_ID>
        ```
        {: pre}

    2. In your browser, open the following {{site.data.keyword.cloud_notm}} IAM passcode website.
        ```sh
        https://iam.cloud.ibm.com/identity/passcode
        ```
        {: codeblock}

    3. Log in with your IBMid and copy the passcode.
    4. Log in to your cluster with the passcode.
        ```sh
        oc login -u passcode -p <iam_passcode> --server=<master_URL>
        ```
        {: pre}

**What's next?** Try [Deploying apps through the CLI](/docs/openshift?topic=openshift-deploy_app#deploy_apps_cli).



## Accessing clusters through the private cloud service endpoint
{: #access_private_se}

Allow authorized cluster users to access your [VPC](#vpc_private_se) or [classic](#access_private_se) cluster through the private cloud service endpoint.
{: shortdesc}

Want to set up a VPN to connect to your cluster from your local machine? Check out [Accessing private clusters by using the WireGuard VPN](/docs/openshift?topic=openshift-access_cluster#access_vpn_openshift).
{: tip}

### Accessing VPC clusters through the private cloud service endpoint
{: #vpc_private_se}

The {{site.data.keyword.redhat_openshift_notm}} master is accessible through the private cloud service endpoint if authorized cluster users are in your {{site.data.keyword.cloud_notm}} private network or are connected to the private network, such as through a [VPC VPN connection](/docs/vpc?topic=vpc-vpn-onprem-example). However, communication with the Kubernetes master over the private cloud service endpoint must go through the `166.X.X.X` IP address range, which you must configure in your VPN gateway and connection setup.
{: shortdesc}

If you enabled only the private cloud service endpoint during cluster creation, the private cloud service endpoint is used by default to access {{site.data.keyword.redhat_openshift_notm}} components such as the {{site.data.keyword.redhat_openshift_notm}} web console or OperatorHub. You must be connected to the private VPC network, such as through a VPN connection, to access these components or run `kubectl` commands on your cluster.
{: note}

1. Set up your {{site.data.keyword.vpc_short}} VPN and connect to your private network through the VPN.
    1. [Configure a VPN gateway on your local machine](/docs/vpc?topic=vpc-vpn-onprem-example#configuring-onprem-gateway). For example, you might choose to set up StrongSwan on your machine.
    2. [Create a VPN gateway in your VPC, and create the connection between the VPC VPN gateway and your local VPN gateway](/docs/vpc?topic=vpc-vpn-create-gateway#vpn-create-ui). In the **New VPN connection for VPC** section, add the `166.8.0.0/14` subnet to the **Local subnets** field. If you have a multizone cluster, repeat this step to configure a VPC gateway on a subnet in each zone where you have worker nodes.
    3. Verify that you are connected to the private network through your {{site.data.keyword.vpc_short}} VPN connection.

2. To log in to your cluster, choose from the following options.
    * **Log in as admin**:
        1. Make sure that you have the [**Administrator** platform access role for the cluster](/docs/openshift?topic=openshift-users#add_users).
        2. Set your command line context for the cluster and download the TLS certificates and permission files for the administrator.
            ```sh
            ibmcloud oc cluster config -c <cluster_name_or_ID> --admin --endpoint private
            ```
            {: pre}

    * **Log in with an API key**: See [Using an API key to log in to {{site.data.keyword.redhat_openshift_notm}}](/docs/openshift?topic=openshift-access_cluster#access_api_key).
    * **Log in with {{site.data.keyword.cloud_notm}} passcode**:
        1. Get the **Private Service Endpoint URL** of your cluster in the output of the following command.
            ```sh
            ibmcloud oc cluster get -c <cluster_name_or_ID>
            ```
            {: pre}

        2. In your browser, open the following {{site.data.keyword.cloud_notm}} IAM passcode website.
            ```sh
            https://iam.cloud.ibm.com/identity/passcode
            ```
            {: codeblock}

        3. Log in with your IBMid and copy the passcode.
        4. Log in to your cluster with the passcode.
            ```sh
            oc login -u passcode -p <iam_passcode> --server=<private_service_endpoint_URL>
            ```
            {: pre}

3. Verify that the `oc` commands run properly with your cluster through the private cloud service endpoint by checking the version.
    ```sh
    oc version
    ```
    {: pre}

    Example output

    ```sh
    Client Version: 4.5.0-0.okd-2020-09-04-180756
    Server Version: 4.5.35
    Kubernetes Version: v1.18.3+cdb0358
    ```
    {: screen}

### Accessing classic clusters through the private cloud service endpoint
{: #classic_private_se}

The {{site.data.keyword.redhat_openshift_notm}} master is accessible through the private cloud service endpoint if authorized cluster users are in your {{site.data.keyword.cloud_notm}} private network or are connected to the private network such as through a [classic VPN connection](/docs/iaas-vpn?topic=iaas-vpn-getting-started) or [{{site.data.keyword.dl_full_notm}}](/docs/dl?topic=dl-get-started-with-ibm-cloud-dl). However, communication with the Kubernetes master over the private cloud service endpoint must go through the `166.X.X.X` IP address range, which is not routable from a classic VPN connection or through {{site.data.keyword.dl_full_notm}}. You can expose the private cloud service endpoint of the master for your cluster users by using a private network load balancer (NLB). The private NLB exposes the private cloud service endpoint of the master as an internal `10.X.X.X` IP address range that users can access with the VPN or {{site.data.keyword.dl_full_notm}} connection. If you enable only the private cloud service endpoint, you can use the {{site.data.keyword.redhat_openshift_notm}} web console to create the private NLB.
{: shortdesc}

1. Log in to your [{{site.data.keyword.redhat_openshift_notm}} cluster by using the public cloud service endpoint](#access_public_se).

2. Get the private cloud service endpoint URL and port for your cluster.
    ```sh
    ibmcloud oc cluster get -c <cluster_name_or_ID>
    ```
    {: pre}

    In this example output, the **Private Service Endpoint URL** is `https://c1.private.us-east.containers.cloud.ibm.com:31144`.
    ```sh
    NAME:                           setest
    ID:                             b8dcc56743394fd19c9f3db7b990e5e3
    State:                          normal
    Status:                         healthy cluster
    Created:                        2019-04-25T16:03:34+0000
    Location:                       wdc04
    Pod Subnet:                     172.30.0.0/16
    Service Subnet:                 172.21.0.0/16
    Master URL:                     https://c1-e.us-east.containers.cloud.ibm.com:31144
    Public Service Endpoint URL:    https://c1-e.us-east.containers.cloud.ibm.com:31144
    Private Service Endpoint URL:   https://c1.private.us-east.containers.cloud.ibm.com:31144
    Master Location:                Washington D.C.
    ...
    ```
    {: screen}

3. Create a YAML file that is named `oc-api-via-nlb.yaml`. This YAML creates a private `LoadBalancer` service and exposes the private cloud service endpoint through that NLB. Replace `<private_service_endpoint_port>` with the port you found in the previous step.
    ```yaml
    apiVersion: v1
    kind: Service
    metadata:
      name: oc-api-via-nlb
      annotations:
        service.kubernetes.io/ibm-load-balancer-cloud-provider-ip-type: private
      namespace: default
    spec:
      type: LoadBalancer
      ports:
      - protocol: TCP
        port: <private_service_endpoint_port>
        targetPort: <private_service_endpoint_port>
    ---
    kind: Endpoints
    apiVersion: v1
    metadata:
      name: oc-api-via-nlb
      namespace: default
    subsets:
      - addresses:
          - ip: 172.20.0.1
        ports:
          - port: 2040
    ```
    {: codeblock}

4. To create the private NLB and endpoint:
    1. Apply the configuration file that you previously created.
        ```sh
        oc apply -f oc-api-via-nlb.yaml
        ```
        {: pre}

    2. Verify that the `oc-api-via-nlb` NLB is created. In the output, note the `10.x.x.x` **EXTERNAL-IP** address. This IP address exposes the private cloud service endpoint for the cluster master on the port that you specified in your YAML file.
        ```sh
        oc get svc -o wide
        ```
        {: pre}

        In this example output, the IP address for the private cloud service endpoint of the master is `10.186.92.42`.
        ```sh
        NAME                     TYPE           CLUSTER-IP       EXTERNAL-IP      PORT(S)          AGE   SELECTOR
        oc-api-via-nlb           LoadBalancer   172.21.150.118   10.186.92.42     443:32235/TCP    10m   <none>
        ...
        ```
        {: screen}

5. On the client machines where you or your users run `oc` commands, add the NLB IP address and the private cloud service endpoint URL to the `/etc/hosts` file. Do not include any ports in the IP address and URL and don't include `https://` in the URL.
    * For macOS and Linux users:
        ```sh
        sudo nano /etc/hosts
        ```
        {: pre}

    * For Windows users:
        ```sh
        notepad C:\Windows\System32\drivers\etc\hosts
        ```
        {: pre}

        Depending on your local machine permissions, you might need to run Notepad as an administrator to edit the hosts file.
        {: tip}

        Example text to add:
        ```sh
        10.186.92.42      c1.private.us-east.containers.cloud.ibm.com
        ```
        {: codeblock}

6. Verify that you are connected to the private network through a [VPN](/docs/iaas-vpn?topic=iaas-vpn-getting-started) or [{{site.data.keyword.dl_full_notm}}](/docs/dl?topic=dl-get-started-with-ibm-cloud-dl) connection.

7. Log in to your cluster by choosing from one of the following options.
    * **Log in as admin**:
        1. Make sure that you have the [**Administrator** platform access role for the cluster](/docs/openshift?topic=openshift-users#add_users).
        2. Set your command line context for the cluster and download the TLS certificates and permission files for the administrator.
            ```sh
            ibmcloud oc cluster config -c <cluster_name_or_ID> --admin --endpoint private
            ```
            {: pre}

    * **Log in with an API key**: See [Using an API key to log in to {{site.data.keyword.redhat_openshift_notm}}](/docs/openshift?topic=openshift-access_cluster#access_api_key).
    * **Log in with {{site.data.keyword.cloud_notm}} passcode**:
        1. Get the **Private Service Endpoint URL** of your cluster in the output of the following command.
            ```sh
            ibmcloud oc cluster get -c <cluster_name_or_ID>
            ```
            {: pre}

        2. In your browser, open the following {{site.data.keyword.cloud_notm}} IAM passcode website.
            ```sh
            https://iam.cloud.ibm.com/identity/passcode
            ```
            {: codeblock}

        3. Log in with your IBMid and copy the passcode.
        4. Log in to your cluster with the passcode.
            ```sh
            oc login -u passcode -p <iam_passcode> --server=<private_service_endpoint_URL>
            ```
            {: pre}

8. Verify that the `oc` commands run properly with your cluster through the private cloud service endpoint by checking the version.
    ```sh
    oc version
    ```
    {: pre}

    Example output

    ```sh
    Client Version: 4.5.0-0.okd-2020-09-04-180756
    Server Version: 4.5.35
    Kubernetes Version: v1.18.3+cdb0358
    ```
    {: screen}

### Creating an allowlist for the private cloud service endpoint
{: #private-se-allowlist}

Control access to your private cloud service endpoint by creating a subnet allowlist.
{: shortdesc}

After you [grant users access to your cluster through {{site.data.keyword.cloud_notm}} IAM](/docs/openshift?topic=openshift-users#checking-perms), you can add a secondary layer of security by creating an allowlist for the private cloud service endpoint. Only authorized requests to your cluster master that originate from subnets in the allowlist are permitted through the cluster's private cloud service endpoint.

If you want to allow requests from a different VPC than the one your cluster is in, you must include the cloud service endpoint for that VPC in the allowlist.
{: note}

For example, to access your cluster's private cloud service endpoint, you must connect to your {{site.data.keyword.cloud_notm}} classic network or your VPC network through a VPN or {{site.data.keyword.dl_full_notm}}. You can add the subnet for the VPN or {{site.data.keyword.dl_short}} tunnel so that only authorized users in your organization can access the private cloud service endpoint from that subnet.

A private cloud service endpoint allowlist can also help prevent users from accessing your cluster after their authorization is revoked. When a user leaves your organization, you remove their {{site.data.keyword.cloud_notm}} IAM permissions that grant them access to the cluster. However, the user might have copied the API key that contains a functional ID's credentials, which contain the necessary IAM permissions for you cluster. That user can still use those credentials and the private cloud service endpoint address to access your cluster from a different subnet, such as from a different {{site.data.keyword.cloud_notm}} account. If you create an allowlist that includes only the subnets for your VPN tunnel in your organization's {{site.data.keyword.cloud_notm}} account, the user's attempted access from another {{site.data.keyword.cloud_notm}} account is denied.

Worker node subnets are automatically added to and removed from your allowlist so that worker nodes can always access the master through the private cloud service endpoint.

By default, private cloud service endpoint allowlists are limited to 20 subnets. If you need more than 20 subnets in your allowlist, you can [open a support ticket](/docs/containers?topic=containers-get-help#help-support) to increase the limit to 75. 
{: tip}

If the public cloud service endpoint is enabled for your cluster, authorized requests are still permitted through the public cloud service endpoint. Therefore, the private cloud service endpoint allowlist is most effective for controlling access to clusters that have only the private cloud service endpoint enabled.
{: note}

Before you begin:
* [Access your cluster through the private cloud service endpoint](#access_private_se).
* [Grant users access to your cluster through {{site.data.keyword.cloud_notm}} IAM](/docs/openshift?topic=openshift-users#checking-perms).

To create a private cloud service endpoint allowlist:

1. Get the subnets that you want to add to the allowlist. For example, you might get the subnet for the connection through your VPN or {{site.data.keyword.dl_short}} tunnel to your {{site.data.keyword.cloud_notm}} private network.

2. Enable the subnet allowlist feature for a cluster's private cloud service endpoint. Now, access to the cluster via the private cloud service endpoint is blocked for any requests that originate from a subnet that is not in the allowlist. Your worker nodes continue to run and have access to the master.
    ```sh
    ibmcloud oc cluster master private-service-endpoint allowlist enable --cluster <cluster_name_or_ID>
    ```
    {: pre}

3. Add subnets from which authorized users can access your private cloud service endpoint to the allowlist.
    ```sh
    ibmcloud oc cluster master private-service-endpoint allowlist add --cluster <cluster_name_or_ID> --subnet <subnet_CIDR> [--subnet <subnet_CIDR> ...]
    ```
    {: pre}

4. Verify that the subnets in your allowlist are correct. The allowlist includes subnets that you manually added and subnets that are automatically added and managed by IBM, such as worker node subnets.
    ```sh
    ibmcloud oc cluster master private-service-endpoint allowlist get --cluster <cluster_name_or_ID>
    ```
    {: pre}

Your authorized users can now continue with [Accessing {{site.data.keyword.redhat_openshift_notm}} clusters through the private cloud service endpoint](#access_private_se).




## Accessing {{site.data.keyword.redhat_openshift_notm}} clusters on {{site.data.keyword.satelliteshort}}
{: #access_cluster_sat}

After you [create a {{site.data.keyword.redhat_openshift_notm}} cluster in your {{site.data.keyword.satelliteshort}} location](/docs/openshift?topic=openshift-satellite-clusters), you can begin working with your cluster by accessing the cluster.
{: shortdesc}

Want to set up a VPN to connect to your cluster from your local machine? Check out [Accessing private clusters by using the WireGuard VPN](/docs/openshift?topic=openshift-access_cluster#access_vpn_openshift).
{: tip}

### Accessing clusters through the cluster service URL
{: #access_cluster_sat_se}

Connect to your cluster through its service URL. This URL is one of your {{site.data.keyword.satelliteshort}} location subdomains and a node port, which is formatted such as `https://p1iuql40jam23qiuxt833-q9err0fiffbsar61e78vv6e7ds8ne1tx-ce00.us-east.satellite.appdomain.cloud:30710`.
{: shortdesc}

If your location hosts have private network connectivity only, or if you use Amazon Web Services, Google Cloud Platform, and Microsoft Azure hosts, you must be connected to your hosts' private network, such as through VPN access, to connect to your cluster and access the {{site.data.keyword.redhat_openshift_notm}} web console. Alternatively, if your hosts have public network connectivity, you can test access to your cluster by changing your cluster's and location's DNS records to [use your hosts' public IP addresses](#sat_public_access).
{: note}

You can quickly access your {{site.data.keyword.openshiftlong_notm}} cluster from the console.
1. In the [{{site.data.keyword.redhat_openshift_notm}} clusters console](https://cloud.ibm.com/kubernetes/clusters?platformType=openshift){: external}, click the cluster that you want to access.
2. Click **{{site.data.keyword.redhat_openshift_notm}} web console**.
3. Click your profile name, such as `IAM#name@email.com`, and then click **Copy Login Command**.
4. Click **Display Token**, and copy the `oc login` command.
5. Paste the command into your command line.

For security reasons, first log out of the {{site.data.keyword.cloud_notm}} console and then log out of the {{site.data.keyword.redhat_openshift_notm}} web console before you close your browser. You must complete both steps in the specified order to successfully log out of the {{site.data.keyword.redhat_openshift_notm}} web console.
{: note} 

If you can't or don't want to open the {{site.data.keyword.redhat_openshift_notm}} console, choose among the following options to log in to your {{site.data.keyword.openshiftlong_notm}} cluster by using the CLI.
*   **Log in as admin**:
    1. Make sure that you have the [**Administrator** IAM platform access role for the cluster](/docs/openshift?topic=openshift-users#add_users).
    2. Set your command line context for the cluster and download the TLS certificates and permission files for the administrator. For more information, see the [CLI documentation](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_cluster_config).
        ```sh
        ibmcloud oc cluster config -c <cluster_name_or_ID> --admin
        ```
        {: pre}

*   **Log in with an API key**: See [Using an API key to log in to {{site.data.keyword.redhat_openshift_notm}}](/docs/openshift?topic=openshift-access_cluster#access_api_key).

### Accessing clusters from within the {{site.data.keyword.cloud_notm}} private network
{: #access_cluster_sat_link}

If you are connected to the {{site.data.keyword.cloud_notm}} private network, you can use the {{site.data.keyword.satelliteshort}} Link endpoint that is automatically generated for your cluster. This endpoint allows you to connect through the secured Link tunnel server to the cluster's master in your location control plane. The endpoint consists of the Link tunnel server hostname and a node port, which is formatted such as `c-02.<region>.link.satellite.cloud.ibm.com:<port>`.
{: shortdesc}

1. Make sure that you have the [**Administrator** IAM platform access role for the cluster](/docs/openshift?topic=openshift-users#add_users).
2. Set your command line context for the cluster by using the Link endpoint and download the TLS certificates and permission files for the administrator. For more information, see the [CLI documentation](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_cluster_config).
    ```sh
    ibmcloud oc cluster config -c <cluster_name_or_ID> --endpoint link --admin
    ```
    {: pre}

### Accessing clusters from the public network
{: #sat_public_access}

If your hosts have public network connectivity, and you want to access your cluster from your local machine without being connected to your hosts' private network, you can optionally update your cluster's subdomain and location's DNS record to use the public IP addresses of your hosts.
{: shortdesc}

For most location setups, the private IP addresses of your hosts are registered for the location's DNS record so that you can access your cluster only if you are connected to your cloud provider's private network. 

For example, if you use Amazon Web Services, Google Cloud Platform, or Microsoft Azure hosts, or if your hosts' default network interface is private, your location's DNS record is accessible only on the private network. 

To run `kubectl` or `oc` commands against your cluster or access the {{site.data.keyword.redhat_openshift_notm}} web console, you must be connected to your hosts' private network, such as through VPN access. However, if you want to access your cluster from the public network, such as to test access to your cluster from your local machine, you can change the DNS records for your location and cluster subdomains to use your hosts' public IPs instead.

Making your location and cluster subdomains available outside of your hosts' private network to your authorized cluster users is not recommended for production-level workloads.
{: important}

1. Review the location subdomains and check the **Records** for the private IP addresses of the hosts that are registered in the DNS for the subdomain.
    ```sh
    ibmcloud sat location dns ls --location <location_name_or_ID>
    ```
    {: pre}

1. Retrieve the matching public IP addresses of your hosts.
    ```sh
    ibmcloud sat host ls --location <location_name_or_ID>
    ```
    {: pre}

1. Update the location subdomain DNS record with the public IP addresses of each host in the control plane.
    ```sh
    ibmcloud sat location dns register --location <location_name_or_ID> --ip <host_IP> --ip <host_IP> --ip <host_IP>
    ```
    {: pre}

1. Verify that the public IP addresses are registered with your location DNS record.
    ```sh
    ibmcloud sat location dns ls --location <location_name_or_ID>
    ```
    {: pre}

1. Get the **Hostname** for your cluster in the format `<service_name>-<project>.<cluster_name>-<random_hash>-0000.upi.containers.appdomain.cloud` and note the private **IP(s)** that were automatically registered.
    ```sh
    ibmcloud oc nlb-dns ls --cluster <cluster_name_or_ID>
    ```
    {: pre}

1. Add the public IP addresses of the hosts that are assigned as worker nodes to this cluster to your cluster's subdomain. Repeat this command for each host's public IP address.
    ```sh
    ibmcloud oc nlb-dns add --ip <public_IP> --cluster <cluster_name_or_ID> --nlb-host <hostname>
    ```
    {: pre}

1. Remove the private IP addresses from your cluster's subdomain. Repeat this command for all private IP addresses that you retrieved earlier.
    ```sh
    ibmcloud oc nlb-dns rm classic --ip <private_IP> --cluster <cluster_name_or_ID> --nlb-host <hostname>
    ```
    {: pre}

1. Verify that the public IP addresses are registered with your cluster subdomain.
    ```sh
    ibmcloud oc nlb-dns ls --cluster <cluster_name_or_ID>
    ```
    {: pre}
    



## Accessing private clusters by using the WireGuard VPN
{: #access_vpn_openshift}

You can use the WireGuard VPN to securely connect to {{site.data.keyword.redhat_openshift_notm}} clusters with only a private network connection. Your cluster might run in a private network in {{site.data.keyword.cloud_notm}} or an {{site.data.keyword.satellitelong_notm}} location in another cloud provider or your on-premises data center.
{: shortdesc}

Before you begin, make sure that you have an {{site.data.keyword.redhat_openshift_notm}} cluster with a private-only network connection and that the cluster is assigned a private service endpoint.

1. Create a virtual server instance (VSI) that is connected to the same private network that your {{site.data.keyword.redhat_openshift_notm}} cluster runs in. This VSI serves as a jumpbox for your cluster. For example, if you have a private VPC cluster, make sure that you create the VSI in the same VPC. For more information about creating the VSI, consult your infrastructure provider's documentation. The VSI must meet the following specifications:
    - The VSI must have a minimum of 2 vCPUs, 8 GB memory, and 25 GB of disk space.
    - The VSI must run an operating system that is supported by WireGuard. For example, the steps in this topic were tested on an Ubuntu VSI.
    - You must create an SSH key that is stored on the VSI so that you can connect to your VSI via SSH.
    - You must assign a public IP address to your VSI so that your VSI is accessible over the public network.
    - Your VSI must allow at least the following network traffic. You can optionally open up more network traffic on your VSI if required for the apps that run on your cluster.
        - Inbound TCP traffic on port 22 for SSH connections
        - Inbound UDP traffic on port 51820 for the WireGuard server
        - All outbound traffic
2. Log in to your VSI by using the public IP address of the VSI.
    ```sh
    ssh -i <filepath_to_sshkey> root@<public_IP>
    ```
    {: pre}

3. Install the WireGuard server.

    The following steps are specific to VSIs that run Ubuntu. If you run a different Linux distribution, refer to the [WireGuard documentation](https://www.wireguard.com/install/){: external}.
    {: note}

    1. Update the Ubuntu operating system.
        ```sh
        apt update
        ```
        {: pre}
        
        ```sh
        apt upgrade
        ```
        {: pre}

    2. Check if your VSI requires a reboot to apply the updates.
        ```sh
        cat /var/run/reboot-required
        ```
        {: pre}

        Example output
        ```sh
        *** System restart required ***
        ```
        {: screen}

    3. If a reboot is required, reboot the VSI.
        ```sh
        reboot
        ```
        {: pre}

    4. Wait for the reboot to finish. Then, log in to your VSI again.
        ```sh
        ssh -i <filepath_to_sshkey> root@<public_IP>
        ```
        {: pre}

    5. Install the WireGuard server.
        ```sh
        apt install wireguard
        ```
        {: pre}

4. Create WireGuard server keys.
    1. On your VSI, create a new directory to store your keys.
        ```sh
        mkdir -p /etc/wireguard/keys
        ```
        {: pre}

    2. Create a private and a public WireGuard server key.
        ```sh
        wg genkey | tee /etc/wireguard/keys/server.key | wg pubkey | tee /etc/wireguard/keys/server.key.pub
        ```
        {: pre}

    3. Display the public and the private key that you created. 
        **Private key**:
        ```sh
        cat /etc/wireguard/keys/server.key
        ```
        {: pre}

        **Public key**:
        ```sh
        cat /etc/wireguard/keys/server.key.pub
        ```
        {: pre}

5. Retrieve the network interface that your VSI uses to route traffic.
    ```sh
    ip -o -4 route show to default | awk '{print $5}'
    ```
    {: pre}

    Example output

    ```sh
    ens3
    ```
    {: screen}

6. Create the WireGuard server configuration.
    1. Open the WireGuard server configuration. The configuration is initially empty.
        ```sh
        nano /etc/wireguard/wg0.conf
        ```
        {: pre}

    2. Add the following content to your configuration. In the `Interface` section, enter the private key from your WireGuard server that you created and change `<eth0>` to the network interface that you retrieved earlier. The IP address is a random address within the VPN tunnel that you assign to the WireGuard server.

        The server configuration does not yet include the WireGuard client configuration (`Peer`). You add the client configuration after you set up the WireGuard client on your local machine in a later step.
        {: note}

        ```sh
        [Interface]
        PrivateKey = <wireguard_server_private_key>
        Address = 172.16.0.1/24
        PostUp = iptables -A FORWARD -i wg0 -j ACCEPT; iptables -t nat -A POSTROUTING -o <eth0> -j MASQUERADE
        PostDown = iptables -D FORWARD -i wg0 -j ACCEPT; iptables -t nat -D POSTROUTING -o <eth0> -j MASQUERADE
        ListenPort = 51820
        ```
        {: codeblock}

    3. Save your changes and exit the nano editor.
    4. Change the permissions to your WireGuard configuration and server key file.
        ```sh
        chmod 600 /etc/wireguard/wg0.conf /etc/wireguard/keys/server.key
        ```
        {: pre}

7. Start the WireGuard server.
    1. Start the WireGuard server.
        ```sh
        wg-quick up wg0
        ```
        {: pre}

    2. Show the status of your WireGuard server connections. Note that your output only shows an interface section and no peer section as the WireGuard client is not successfully configured yet.
        ```sh
        wg show
        ```
        {: pre}

    3. Change the VSI system settings to automatically start the WireGuard server every time the VSI is booted.
        ```sh
        systemctl enable wg-quick@wg0
        ```
        {: pre}

8. Enable IPv4 forwarding on the WireGuard server.
    1. Open the VSI system and network settings.
        ```sh
        nano /etc/sysctl.conf
        ```
        {: pre}

    2. Remove the comment (`#`) from the `net.ipv4.ip_forward=1` line. Your configuration looks similar to the following:
        ```sh
        ...
        # Uncomment the next line to enable TCP/IP SYN cookies
        # See http://lwn.net/Articles/277146/
        # Note: This may impact IPv6 TCP sessions too
        #net.ipv4.tcp_syncookies=1

        # Uncomment the next line to enable packet forwarding for IPv4
        net.ipv4.ip_forward=1
        ...
        ```
        {: screen}
        
    3. Enable IPv4 forwarding on your VSI. 
        ```sh
        sysctl -p
        ```
        {: pre}

9. Retrieve the list of IP addresses that you need to allow in your WireGuard client configuration so that you can successfully connect to your private {{site.data.keyword.redhat_openshift_notm}} cluster.
    1. Get the details of your cluster and note the **Ingress Subdomain** and the **Private Service Endpoint URL**.
        ```sh
        ibmcloud ks cluster get --cluster <cluster_name_or_ID>
        ```
        {: pre}

    2. Retrieve the IP address that is assigned to the Ingress subdomain and your private service endpoint URL.
        ```sh
        nslookup <ingress_subdomain>
        ```
        {: pre}

        ```sh
        nslookup <private_service_endpoint_URL>
        ```
        {: pre}

        To successfully run an `nslookup` command on your private service endpoint URL, remove `https://` and the port from your URL. Alternatively, you can note all IP address CIDRs for the region that your cluster master is in as shown in step 3 of [Opening required ports in a private firewall](/docs/containers?topic=containers-firewall#firewall_private).
        {: tip}

    3. Get the IP address CIDR of all the VPC subnets, private VLANs, or on-prem networks that your cluster worker nodes are connected to. For example, if you created a VPC cluster in {{site.data.keyword.cloud_notm}}, you can get the subnet CIDR by getting the details for each worker node.  
        ```sh
        ibmcloud ks worker get --worker <worker_ID> --cluster <cluster_name_or_ID>
        ```
        {: pre}

10. Install, configure, and activate the WireGuard client.
    1. Follow the [instructions](https://www.wireguard.com/install/){: external} to install the WireGuard client on your local machine.
    2. Open the client.
    3. Click `+` to create an empty VPN tunnel. A WireGuard private and public key is automatically created for you and displayed in the client configuration.
    4. Enter a name for your client configuration.
    5. Add the following configuration after the `PrivateKey` that is displayed in the `Interface` section. The CIDR `192.168.3.217/32` is a random CIDR that you assign to the client to use within the VPN tunnel.

        Do not change the `PrivateKey` field, which can alter your WireGuard client private key and make the tunnel that you created unusable.
        {: important}

        In the `Peer` section, enter the following information:
        - `PublicKey`: The WireGuard server public key that you created earlier.
        - `AllowedIPs`: The IP address CIDRs of worker nodes, Ingress subdomain, the private service endpoint URL, and the WireGuard server that you retrieved earlier, separated by commas.
        - `Endpoint`: The public IP address of the jumpbox VSI.  

        ```sh
        Address = 192.168.3.217/32

        [Peer]
        PublicKey = <public_wireguard_server_key>
        AllowedIPs = <worker_CIDR>,<ingress_subdomain_CIDR>,<private_service_endpoint_URL_CIDR>,<wireguard_server_CIDR>
        Endpoint = <vsi_public_IP>:51820
        ```
        {: codeblock}

        Your final client configuration looks similar to the following:
        
        ```sh
        [Interface]
        PrivateKey = aAAA1a1AAAAAaaaaa1aaa1AAAa1AaAAaAaAAAaAaaAa=
        Address = 192.168.3.217/32

        [Peer]
        PublicKey = Aaaa1A1aaaaaaaaa1aaa1AAAa1AaAAAAAAAAAAaAaaAa=
        AllowedIPs = 166.9.58.104, 10.241.0.0/24, 172.16.0.1/24
        Endpoint = 167.63.170.188:51820
        ```
        {: codeblock}

    6. Save your configuration.
    7. Click **Activate** to start your WireGuard client. If the client is activated successfully, the status changes to **Active**.
    8. Copy the WireGuard client public key.

11. Finish the WireGuard server configuration.
    1. On your VSI, open the WireGuard server configuration again.
        ```sh
        nano /etc/wireguard/wg0.conf
        ```
        {: pre}

    2. Add the `Peer` section to your WireGuard server configuration to add the WireGuard client. Enter the WireGuard client public key in the `PublicKey` field and the IP address CIDR that you assigned to the client in the `AllowedIPs` field.  
        ```sh
        ...
        [Peer]
        PublicKey = <wireguard_client_public_key>
        AllowedIPs = 192.168.3.217/32
        ```
        {: codeblock}

        Your server configuration looks similar to the following:
        ```sh
        [Interface]
        PrivateKey = <wireguard_server_private_key>
        Address = 172.16.0.1/24
        PostUp = iptables -A FORWARD -i wg0 -j ACCEPT; iptables -t nat -A POSTROUTING -o ens3 -j MASQUERADE
        PostDown = iptables -D FORWARD -i wg0 -j ACCEPT; iptables -t nat -D POSTROUTING -o ens3 -j MASQUERADE
        ListenPort = 51820

        [Peer]
        PublicKey = <wireguard_client_public_key>
        AllowedIPs = 192.168.3.217/32
        ```
        {: codeblock}

    3. Stop the WireGuard server and start it again to apply your changes.
        ```sh
        wg-quick down wg0
        ```
        {: pre}

        ```sh
        wg-quick up wg0
        ```
        {: pre}

    4. Show the updated status of your WireGuard server connections. The interface and peer connections are displayed in your CLI output.
        ```sh
        wg show wg0
        ```
        {: pre}

        Example output
        ```sh
        interface: wg0
        public key: AA11aa1aa/aa1AaA1AaaaAAAaa1AAaaA1aAAAAaaAAA=
        private key: (hidden)
        listening port: 51820

        peer: a11aAaA+AaaaaaaaA1aAAaAA1/1AaAaAaaAA1AAA/aA=
        allowed ips: 192.168.3.217/32
        ```
        {: screen}

12. Check that you can connect to the private {{site.data.keyword.redhat_openshift_notm}} cluster from your local machine.
    1. From the [{{site.data.keyword.redhat_openshift_notm}} clusters console](https://cloud.ibm.com/kubernetes/clusters?platformType=openshift){: external}, select your private cluster that you want to connect to.  
    2. On the cluster overview page, go to the **Networking** section and copy the **Ingress subdomain**.
    3. Ping the Ingress subdomain to verify that you can connect to your private {{site.data.keyword.redhat_openshift_notm}} cluster.
    4. From the cluster overview page, open the {{site.data.keyword.redhat_openshift_notm}} web console. 

## Accessing clusters from automation tools by using an API key
{: #access_automation}

{{site.data.keyword.openshiftlong_notm}} is integrated with {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM). With IAM, you can authenticate users and services by using their IAM identities and authorize actions with access roles and policies. When you authenticate as a user through the {{site.data.keyword.redhat_openshift_notm}} console, your IAM identity is used to generate a {{site.data.keyword.redhat_openshift_notm}} login token that you can use to log in to the command line. You can automate logging in to your cluster by creating an IAM API key or service ID to use for the `oc login` command.
{: shortdesc}

### Using an API key to log in to clusters
{: #access_api_key}

You can create an {{site.data.keyword.cloud_notm}} IAM API key and then use the API key to log in to a {{site.data.keyword.redhat_openshift_notm}} cluster. With API keys, you can use the credentials of one user or shared account to access a cluster, instead of logging in individually. You might also create an API key for a [service ID](#access_service_id). For more information, see [Understanding API keys](/docs/account?topic=account-manapikey).
{: shortdesc}

1. Create an {{site.data.keyword.cloud_notm}} API key.
    Save your API key in a secure location. You can't retrieve the API key again. If you want to export the output to a file on your local machine, include the `--file <path>/<file_name>` flag.
    {: important}

    ```sh
    ibmcloud iam api-key-create <name>
    ```
    {: pre}

2. Configure your cluster to add the API key user to your cluster RBAC policies and to set your session context to your cluster server.
    1. Log in to {{site.data.keyword.cloud_notm}} with the API key credentials.
        ```sh
        ibmcloud login --apikey <API_key>
        ```
        {: pre}

    2. Download and add the `kubeconfig` configuration file for your cluster to your existing `kubeconfig` in `~/.kube/config` or the last file in the `KUBECONFIG` environment variable. **Note**: If you enabled the private cloud service endpoint and want to use it for the cluster context, include the `--endpoint private` flag. To use the private cloud service endpoint to connect to your cluster, you must be in your {{site.data.keyword.cloud_notm}} private network or connected to the private network through a [VPC VPN connection](/docs/vpc?topic=vpc-vpn-onprem-example), or for classic infrastructure, a [classic VPN connection](/docs/iaas-vpn?topic=iaas-vpn-getting-started) or [{{site.data.keyword.dl_full_notm}}](/docs/dl?topic=dl-get-started-with-ibm-cloud-dl).
        ```sh
        ibmcloud oc cluster config -c <cluster_name_or_ID> [--endpoint private]
        ```
        {: pre}

3. Exchange your {{site.data.keyword.cloud_notm}} IAM API key credentials for a {{site.data.keyword.redhat_openshift_notm}} access token. You can log in from the CLI or API. For more information, see the [{{site.data.keyword.redhat_openshift_notm}} docs](https://docs.openshift.com/container-platform/4.9/authentication/configuring-internal-oauth.html){: external}.

    **Log in by using the `oc` CLI**:
    Log in to your cluster with the `oc login` command. The username (`-u`) is `apikey` and the password (`-p`) is your {{site.data.keyword.cloud_notm}} IAM API key value. To use the private cloud service endpoint, include the `--server=<private_service_endpoint>` flag.
    ```sh
    oc login -u apikey -p <API_key> [--server=<private_service_endpoint>]
    ```
    {: pre}

    **Log in by running {{site.data.keyword.redhat_openshift_notm}} API requests directly against your cluster**:
    Log in to your cluster with the API such as via a curl request.

    1. Get the **Master URL** of your cluster.
        ```sh
        ibmcloud oc cluster get -c <cluster_name_or_ID>
        ```
        {: pre}

        Example output
        ```sh
        NAME:                           mycluster
        ID:                             1234567
        State:                          normal
        Created:                        2020-01-22T19:22:16+0000
        Location:                       dal10
        Master URL:                     https://c100-e.<region>.containers.cloud.ibm.com:<port>
        ...

        ```
        {: screen}

    2. ![Version 4 icon.](images/icon-version-43.png) **{{site.data.keyword.redhat_openshift_notm}} version 4 only**: Get the token endpoint of the {{site.data.keyword.redhat_openshift_notm}} `oauth` server.
        ```sh
        curl <master_URL>/.well-known/oauth-authorization-server | jq -r .token_endpoint
        ```
        {: pre}

        Example output
        ```sh
        <token_endpoint>/oauth/token
        ```
    3. Log in to the cluster with the endpoint that you previously retrieved. Replace `<URL>` with the `<token_endpoint>` of the `oauth` server.

        Example curl request:
        ```sh
        curl -u 'apikey:<API_key>' -H "X-CSRF-Token: a" '<URL>/oauth/authorize?client_id=openshift-challenging-client&response_type=token' -vvv
        ```
        {: pre}

    4. In the **Location** response, find the `access_token`, such as in the following example.
        ```sh
        < HTTP/1.1 302 Found
        < Cache-Control: no-cache, no-store, max-age=0, must-revalidate
        < Cache-Control: no-cache, no-store, max-age=0, must-revalidate
        < Expires: 0
        < Expires: Fri, 01 Jan 1990 00:00:00 GMT
        < Location: <token_endpoint>/oauth/token/implicit#access_token=<access_token>&expires_in=86400&scope=user%3Afull&token_type=Bearer
        ...
        ```
        {: screen}

    5. Use your cluster master URL and the access token to access the {{site.data.keyword.redhat_openshift_notm}} API, such as to list all the pods in your cluster. For more information, see the [{{site.data.keyword.redhat_openshift_notm}} API documentation](https://docs.openshift.com/container-platform/4.9/rest_api/index.html){: external}.

        Example curl request:
        ```sh
        curl -H "Authorization: Bearer <access_token>" '<master_URL>/api/v1/pods'
        ```
        {: pre}

### Using a service ID to log in to clusters
{: #access_service_id}

You can create an {{site.data.keyword.cloud_notm}} IAM service ID, make an API key for the service ID, and then use the API key to log in to a {{site.data.keyword.redhat_openshift_notm}} cluster. You might use service IDs so that apps that are hosted in other clusters or clouds can access your cluster's services. Because service IDs are not tied to a specific user, your apps can authenticate if individual users leave your account. For more information, see [Creating and working with service IDs](/docs/account?topic=account-serviceids).
{: shortdesc}

1. Create an {{site.data.keyword.cloud_notm}} IAM service ID for your cluster that is used for the IAM policies and API key credentials. Be sure to give the service ID a description that helps you retrieve the service ID later, such as including the cluster name.
    ```sh
    ibmcloud iam service-id-create <cluster_name>-id --description "Service ID for Red Hat OpenShift on IBM Cloud cluster <cluster_name>"
    ```
    {: pre}

    Example output

    ```sh
    NAME          <cluster_name>-id
    Description   Service ID for Red Hat OpenShift on IBM Cloud cluster <cluster_name>
    CRN           crn:v1:bluemix:public:iam-identity::a/1aa111aa1a11111aaa1a1111aa1aa111::serviceid:ServiceId-bbb2b2b2-2bb2-2222-b222-b2b2b2222b22
    Bound To      crn:v1:bluemix:public:::a/1aa111aa1a11111aaa1a1111aa1aa111:::
    Version       1-c3c333333333ccccc33333c33cc3cc33
    Locked        false
    UUID          ServiceId-bbb2b2b2-2bb2-2222-b222-b2b2b2222b22
    ```
    {: screen}

2. Create a custom {{site.data.keyword.cloud_notm}} IAM policy for your cluster service ID that grants access to {{site.data.keyword.openshiftlong_notm}}.

    ```sh
    ibmcloud iam service-policy-create <cluster_service_ID> --service-name containers-kubernetes --roles <service_access_role> --service-instance <cluster_ID>
    ```
    {: pre}
    
    | Parameter | Description |
    | -------------- | -------------- |
    | `<cluster_service_ID>` | Required. Enter the service ID that you previously created for your {{site.data.keyword.redhat_openshift_notm}} cluster. |
    | `--service-name containers-kubernetes` | Required. Enter `containers-kubernetes` so that the IAM policy is for {{site.data.keyword.openshiftlong_notm}} clusters. |
    | `--roles <service_access_role>` | Required. Enter the access role that you want the service ID to have to your {{site.data.keyword.redhat_openshift_notm}} cluster. [Platform access roles](/docs/openshift?topic=openshift-access_reference#iam_platform) permit cluster management activities such as creating worker nodes. [Service access roles](/docs/openshift?topic=openshift-access_reference#service) correspond to RBAC roles that permit {{site.data.keyword.redhat_openshift_notm}} management activities within the cluster, such as for Kubernetes resources like pods and namespaces. For multiple roles, include a comma-separated list. Possible values are `Administrator`, `Operator`, `Editor`, and `Viewer` (platform access roles); and `Reader`, `Writer`, and `Manager` (service access roles). |
    | `--service-instance <cluster_ID>` | To restrict the policy to a particular cluster, enter the cluster's ID. To get your cluster ID, run `ibmcloud oc clusters`. If you don't include the service instance, the access policy grants the service ID access to all your clusters, Kubernetes and {{site.data.keyword.redhat_openshift_notm}}. You can also scope the access policy to a region (`--region`) or resource group (`--resource-group-name`). |
    {: caption="Table 1. Understanding this command's components" caption-side="bottom"}
    
3. Create an API key for the service ID. Name the API key similar to your service ID, and include the service ID that you previously created, `<cluster_name>-id`. Be sure to give the API key a description that helps you retrieve the key later. Save your API key in a secure location. You can't retrieve the API key again. If you want to export the output to a file on your local machine, include the `--file <path>/<file_name>` flag.

    ```sh
    ibmcloud iam service-api-key-create <cluster_name>-key <service_ID> --description "API key for service ID <service_ID> in Red Hat OpenShift cluster <cluster_name>"
    ```
    {: pre}

    Example output

    ```sh
    Please preserve the API key! It can't be retrieved after it's created.

    Name          <cluster_name>-key
    Description   API key for service ID <service_ID> in Red Hat OpenShift cluster <cluster_name>
    Bound To      crn:v1:bluemix:public:iam-identity::a/1bb222bb2b33333ddd3d3333ee4ee444::serviceid:ServiceId-ff55555f-5fff-6666-g6g6-777777h7h7hh
    Created At    2019-02-01T19:06+0000
    API Key       i-8i88ii8jjjj9jjj99kkkkkkkkk_k9-llllll11mmm1
    Locked        false
    UUID          ApiKey-222nn2n2-o3o3-3o3o-4p44-oo444o44o4o4
    ```
    {: screen}

4. Configure your cluster to add the service ID user to your cluster RBAC policies and to set your session context to your cluster server.

    1. Log in to {{site.data.keyword.cloud_notm}} with the service ID's API key credentials.
        ```sh
        ibmcloud login --apikey <API_key>
        ```
        {: pre}

    2. Download and add the `kubeconfig` configuration file for your cluster to your existing `kubeconfig` in `~/.kube/config` or the last file in the `KUBECONFIG` environment variable. **Note**: If you enabled the private cloud service endpoint and want to use it for the cluster context, include the `--endpoint private` flag. To use the private cloud service endpoint to connect to your cluster, you must be in your {{site.data.keyword.cloud_notm}} private network or connected to the private network through a [VPC VPN connection](/docs/vpc?topic=vpc-vpn-onprem-example), or for classic infrastructure, a [classic VPN connection](/docs/iaas-vpn?topic=iaas-vpn-getting-started) or [{{site.data.keyword.dl_full_notm}}](/docs/dl?topic=dl-get-started-with-ibm-cloud-dl).
    
        ```sh
        ibmcloud oc cluster config -c <cluster_name_or_ID> [--endpoint private]
        ```
        {: pre}

5. [Use the service ID's API key to log in to your {{site.data.keyword.redhat_openshift_notm}} cluster](#access_api_key). The username (`-u`) is `apikey` and the password (`-p`) is your API key value. To use the private cloud service endpoint, include the `--server=<private_service_endpoint>` flag.

    ```sh
    oc login -u apikey -p <API_key> [--server=<private_service_endpoint>]
    ```
    {: pre}

6. Verify that the service ID can perform the actions that you authorized.

    Example: If you assigned a `Reader` service access role, the service ID can list pods in your {{site.data.keyword.redhat_openshift_notm}} project.
    ```sh
    oc get pods
    ```
    {: pre}

    Example: If you assigned a `Manager` service access role, the service ID can list the users in your {{site.data.keyword.redhat_openshift_notm}} cluster. The ID of your IAM service ID is in the **Identities** output. Other individual users might be identified by their email address and IBMid.
    
    ```sh
    oc get users
    ```
    {: pre}

    Example output

    ```sh
    NAME                           UID                                    FULL NAME   IDENTITIES
    IAM#                           dd44ddddd-d4dd-44d4-4d44-4d44d444d444              IAM:iam-ServiceId-bbb2b2b2-2bb2-2222-b222-b2b2b2222b22
    IAM#first.last@email.com       55555ee5-e555-55e5-e5e5-555555ee55ee               IAM:IBMid-666666FFF6
    ```
    {: screen}


## Accessing the cluster master via admission controllers and webhooks
{: #access_webhooks}

Admission controllers intercept authorized API requests from various Kubernetes resources before the requests reach the API server that runs in your {{site.data.keyword.openshiftlong_notm}} cluster master. Mutating admission webhooks might modify the request, and validating admission webhooks check the request. If either webhook rejects a request, the entire request fails. Advanced features, whether built-in or added on, often require admission controllers as a security precaution and to control what requests are sent to the API server. For more information, see [Using Admission Controllers](https://kubernetes.io/docs/reference/access-authn-authz/admission-controllers/){: external} and [Dynamic Admission Control](https://kubernetes.io/docs/reference/access-authn-authz/extensible-admission-controllers/){: external} in the Kubernetes documentation.

### Can I create my own admission controllers?
{: #access_webhooks_create_controllers}

Yes, see the [Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/extensible-admission-controllers/){: external} and [{{site.data.keyword.redhat_openshift_notm}}](https://docs.openshift.com/container-platform/4.9/architecture/admission-plug-ins.html){: external} documentation for more information. 

As noted in the Kubernetes documentation, you can use admission controllers for operations that are otherwise handled by the control plane. As such, take great caution when you configure a custom admission controller. You are responsible for any changes that happen in your cluster because of a custom admission controller.
{: important}

Keep in mind the following considerations when you configure a webhook.

- Create [replica pods](/docs/containers?topic=containers-app#replicaset) for the webhook so that if one pod goes down, the webhook can still process requests from your resources. Spread the replica pods across zones, if possible.
- Set appropriate CPU and memory [resource requests and limits](/docs/containers?topic=containers-app#resourcereq) for your webhook.
- Add [liveness and readiness probes](/docs/openshift?topic=openshift-openshift_apps#probe) to help make sure your webhook container is running and ready to serve requests.
- Set pod [anti-affinity scheduling rules](/docs/openshift?topic=openshift-openshift_apps#affinity) to prefer that your webhook pods run on different worker nodes and zones when possible. In clusters that run {{site.data.keyword.redhat_openshift_notm}} version 4.4 or later, you might use [pod topology](https://kubernetes.io/docs/concepts/workloads/pods/pod-topology-spread-constraints/){: external} instead. However, avoid [taints](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/){: external} or forced affinity that might restrict where the webhook pods can be scheduled.
- [Set pod priority](/docs/openshift?topic=openshift-pod_priority) to `system-cluster-critical` for the webhook pods so that other pods can't take resources from your webhook pods.
- Scope your webhook to the appropriate project. Avoid webhooks that process resources that run in system-critical projects that are set up in your cluster by default, such as `kube-system`, `ibm-system`, `ibm-operators`, `calico-system`, `tigera-operator` and `openshift-*` projects.
- Make sure that the worker nodes in your cluster are [the right size for running your webhook applications](/docs/openshift?topic=openshift-strategy#sizing). For example, if your pods request more CPU or memory than the worker node can provide, the pods are not scheduled.


### What other types of apps use admission controllers?
{: #access_webhooks-app-use-controllers}

Many cluster add-ons, plug-ins, and other third-party extensions use admission controllers. Some common ones include:
- [Portieris](/docs/openshift?topic=openshift-images#portieris-image-sec)


### I need help with a broken webhook. What can I do?
{: #access_webhooks-help}

See [Cluster can't update because of broken webhook](/docs/containers?topic=containers-webhooks_update).








