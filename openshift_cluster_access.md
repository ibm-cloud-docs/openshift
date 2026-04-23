---

copyright:
  years: 2014, 2026
lastupdated: "2026-04-23"


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

1. [Install the required CLI tools](/docs/openshift?topic=openshift-cli-install). For quick access to test features in your cluster, you can also use the [{{site.data.keyword.cloud-shell_notm}}](/docs/cloud-shell?topic=cloud-shell-shell-ui).
2. [Create your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-clusters).
3. If your network is protected by a company firewall, [allow access](/docs/openshift?topic=openshift-firewall#corporate) to the {{site.data.keyword.cloud_notm}} and {{site.data.keyword.openshiftlong_notm}} API endpoints and ports. For VPC clusters with only the private cloud service endpoint enabled, you can't test the connection to your cluster until you [configure a VPC VPN with the cloud service endpoint subnet](#vpc_private_se).
4. Check that your cluster is in a healthy state by running `ibmcloud oc cluster get -c <cluster_name_or_ID>`. If your cluster is not in a healthy state, review the [Debugging clusters](/docs/openshift?topic=openshift-debug_clusters) guide for help. For example, if your cluster is provisioned in an account that is protected by a firewall gateway appliance, you must [configure your firewall settings to allow outgoing traffic to the appropriate ports and IP addresses](/docs/openshift?topic=openshift-firewall).
5. Find your cluster's service endpoint.
    * **Classic or VPC clusters**: In the output of the cluster details from the previous step, check the **Public** or **Private Service Endpoint** URL of the cluster.
        *  Public Service Endpoint URL only: Continue with [Accessing clusters through the public cloud service endpoint](#access_public_se).
        *  Both service endpoint URLs: You can access your cluster either through the [public](#access_public_se) or the [private](#access_private_se) service endpoint.
    * **{{site.data.keyword.satellitelong_notm}} clusters**: Continue with [Accessing clusters on {{site.data.keyword.satelliteshort}}](#access_cluster_sat).
6. If any users in your account use multifactor authentication (MFA) like TOTP, make sure that you [enable it for all users at the account level](/docs/iam?topic=iam-enablemfa). To use MFA, it must be enabled at the account level to avoid authentication errors. 




## Accessing clusters through the public cloud service endpoint
{: #access_public_se}

For {{site.data.keyword.redhat_openshift_notm}} clusters with a public cloud service endpoint, you can log in to your cluster from the console or CLI.
{: shortdesc}

### Connecting to the cluster from the console
{: #access_oc_console}

You can quickly access your {{site.data.keyword.openshiftlong_notm}} cluster from the console.
{: shortdesc}

1. In the [console](https://cloud.ibm.com/containers/cluster-management/clusters){: external}, click the cluster that you want to access.
2. Click **{{site.data.keyword.redhat_openshift_notm}} web console**.
3. To continue working in the command line, click your profile name, such as `IAM#name@email.com`, and then click **Copy Login Command**. Depending on your cluster version, log in to your cluster from the command line as follows.
    *  **Version 4**: Click **Display Token**, copy the `oc login` command, and paste the command into your command line.

For security reasons, first log out of the {{site.data.keyword.cloud_notm}} console and then log out of the {{site.data.keyword.redhat_openshift_notm}} web console before you close your browser. You must complete both steps in the specified order to successfully log out of the {{site.data.keyword.redhat_openshift_notm}} web console.
{: note}   

What's next?
:   Try [Deploying apps through the console](/docs/openshift?topic=openshift-deploy_app&interface=ui#deploy_apps_ui).

### Connecting to the cluster from the CLI
{: #access_oc_cli}

Usually, you can use the {{site.data.keyword.redhat_openshift_notm}} web console to get the `oc login` token to access your cluster. If you can't or don't want to open the {{site.data.keyword.redhat_openshift_notm}} console, choose among the following options to log in to your {{site.data.keyword.openshiftlong_notm}} cluster by using the CLI.
{: shortdesc}

Choose from the following options.
*   **Log in as admin**:
    1. Make sure that you have the [**Administrator** platform access role for the cluster](/docs/openshift?topic=openshift-iam-platform-access-roles).
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



## Accessing clusters through the private cloud service endpoint
{: #access_private_se}

Allow authorized cluster users to access your [VPC](#vpc_private_se) or [classic](#access_private_se) cluster through the private cloud service endpoint.
{: shortdesc}

Want to set up a VPN to connect to your cluster from your local machine? Check out [Accessing private clusters by using the WireGuard VPN](/docs/openshift?topic=openshift-cluster-access-wireguard).
{: tip}

### Accessing VPC clusters through the private cloud service endpoint
{: #vpc_private_se}

All VPC clusters have a private service endpoint which authorized users can access. Since it is only available on the private network, users must access it in one of the following ways:
{: shortdesc}

1. For regions other than ca-mon, in-che, and in-mum, the private service endpoint for VPC clusters can be accessed from anywhere inside IBM Cloud, or from a client that is using a VPN (or similar) to connect in to IBM Cloud.

    You can connect via VPN into IBM Cloud using one of the following options:

    [client-to-site VPN](/docs/vpc?topic=vpc-vpn-client-to-site-overview)
    :   Most common option for cluster access, and fairly straightforward to set up. For configuration tips, see [Accessing VPC clusters through the Virtual Private Endpoint Gateway](#vpc_vpe).

    [site-to-site VPN](/docs/vpc?topic=vpc-vpn-onprem-example)
    :   This is more complex to set up but has additional features that might be useful.

    These clusters can be accessed via the private service endpoint URL for the cluster that looks like `c<XXX>.private.<REGION>.containers.cloud.ibm.com:XXXXX`. Use this command to get a kubeconfig file that uses this private endpoint:

    Then you can log into the cluster using one of several options shown below.  Once you have done so, you can verify that connection using something like `ibmcloud oc get nodes`

    * **Log in as admin**:
        1. Make sure that you have the [**Administrator** platform access role for the cluster](/docs/openshift?topic=openshift-iam-platform-access-roles).
        2. Download the kubeconfig for the administrator.
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




2. The private service endpoint for all VPC clusters, in all regions, can be accessed via that cluster's specific Virtual Private Endpoint (VPE) gateway. A VPE Gateway is only available from inside the VPC it was created in or via a VPN (or similar) into that specific VPC. There are two main options to connect to a cluster in this way:

    * A VPE Gateway for the cluster is automatically created in the VPC that the cluster was created in. So one option is to connect from a system inside that VPC, or from a system that has a VPN (or similar) connection into that VPC.
    * If you want to connect from a different VPC (maybe even a VPC in a different region or a different account) you can create a new VPE Gateway in that other VPC. Then from that other VPC (including if you are VPN'd into that other VPC), you can access the cluster master via that new VPE Gateway. The steps for how to do this are in the [Creating Additional Virtual Private Endpoint Gateways in Other VPCs and Accounts](#vpc_cluster_new_vpe_access) section below.
    * More information on this option, including how to get a kubeconfig file and tips on configuring a VPN, are in the [Accessing VPC clusters through the Virtual Private Endpoint Gateway](#vpc_vpe) section below.

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
        1. Make sure that you have the [**Administrator** platform access role for the cluster](/docs/openshift?topic=openshift-iam-platform-access-roles).
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




## Accessing {{site.data.keyword.redhat_openshift_notm}} clusters on {{site.data.keyword.satelliteshort}}
{: #access_cluster_sat}

After you [create a {{site.data.keyword.redhat_openshift_notm}} cluster in your {{site.data.keyword.satelliteshort}} location](/docs/openshift?topic=openshift-satellite-clusters), you can begin working with your cluster by accessing the cluster.
{: shortdesc}

When you access your cluster and run `oc get nodes` or `oc describe node <worker_node>` commands, you might see that the worker nodes are assigned `master,worker` roles. In OpenShift Container Platform clusters, operators use the master role as a `nodeSelector` so that OCP can deploy default components that are controlled by operators, such as the internal registry, in your cluster. The {{site.data.keyword.satelliteshort}} hosts that you assigned to your cluster function as worker nodes only, and no master node processes, such as the API server or Kubernetes scheduler, run on your worker nodes.
{: note}

### Accessing clusters through the cluster service URL
{: #access_cluster_sat_se}

Connect to your cluster through its service URL. This URL is one of your {{site.data.keyword.satelliteshort}} location subdomains and a node port, which is formatted such as `https://p1iuql40jam23qiuxt833-q9err0fiffbsar61e78vv6e7ds8ne1tx-ce00.us-east.satellite.appdomain.cloud:30710`.
{: shortdesc}

If your location hosts have private network connectivity only, or if you use Amazon Web Services, Google Cloud Platform, and Microsoft Azure hosts, you must be connected to your hosts' private network, such as through VPN access, to connect to your cluster and access the {{site.data.keyword.redhat_openshift_notm}} web console. Alternatively, if your hosts have public network connectivity, you can test access to your cluster by changing your cluster's and location's DNS records to [use your hosts' public IP addresses](#sat_public_access).
{: note}

You can quickly access your {{site.data.keyword.openshiftlong_notm}} cluster from the console.
1. In the [console](https://cloud.ibm.com/containers/cluster-management/clusters){: external}, click the cluster that you want to access.
2. Click **{{site.data.keyword.redhat_openshift_notm}} web console**.
3. Click your profile name, such as `IAM#name@email.com`, and then click **Copy Login Command**.
4. Click **Display Token**, and copy the `oc login` command.
5. Paste the command into your command line.

For security reasons, first log out of the {{site.data.keyword.cloud_notm}} console and then log out of the {{site.data.keyword.redhat_openshift_notm}} web console before you close your browser. You must complete both steps in the specified order to successfully log out of the {{site.data.keyword.redhat_openshift_notm}} web console.
{: note} 

If you can't or don't want to open the {{site.data.keyword.redhat_openshift_notm}} console, choose among the following options to log in to your {{site.data.keyword.openshiftlong_notm}} cluster by using the CLI.
*   **Log in as admin**:
    1. Make sure that you have the [**Administrator** IAM platform access role for the cluster](/docs/openshift?topic=openshift-iam-platform-access-roles).
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

To connect to your {{site.data.keyword.satelliteshort}} cluster by using the Link endpoint, for example `--endpoint link` in the CLI, you must follow the steps to set up a **Source** in your Location. This source allows access to your cluster APIs through the Link endpoint. For more information, see [Accessing your Red Hat OpenShift API Satellite link endpoints](/docs/satellite?topic=satellite-link-endpoint-secure).
{: note}

1. Make sure that you have the [**Administrator** IAM platform access role for the cluster](/docs/openshift?topic=openshift-iam-platform-access-roles).
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
    


## Accessing VPC clusters through the Virtual Private Endpoint Gateway
{: #vpc_vpe}

[Virtual Private Endpoint Gateway](/docs/vpc?topic=vpc-about-vpe) is created for VPC clusters automatically. The Kubernetes master is accessible through this Virtual Private Endpoint gateway if authorized cluster users are connected to the same VPC where the cluster is deployed, such as through a [{{site.data.keyword.vpc_short}} VPN](/docs/vpc?topic=vpc-vpn-overview). In this case, the `kubeconfig` is configured with the Virtual Private Endpoint (VPE) URL which is a private DNS name and can be resolved only by the {{site.data.keyword.vpc_short}} Private DNS service. The {{site.data.keyword.vpc_short}} Private DNS server addresses are `161.26.0.7` and `161.26.0.8`.
{: shortdesc}

For clusters that run version [4.13]{: tag-red}: If you enabled only the private cloud service endpoint during cluster creation, the virtual private endpoint of your VPC is used by default to access {{site.data.keyword.redhat_openshift_notm}} components such as the {{site.data.keyword.redhat_openshift_notm}} web console or OperatorHub. You must be connected to the private VPC network, such as through a VPN connection, to access these components or run `kubectl` commands on your cluster. Note that to access the console through the VPE, you must be able to access `cloud.ibm.com`, which requires public connectivity.
{: note}


1. Set up your {{site.data.keyword.vpc_short}} VPN and connect to your VPC through VPN.

    1. Configure a [client-to-site](/docs/vpc?topic=vpc-vpn-client-to-site-overview) or [site-to-site](/docs/vpc?topic=vpc-vpn-onprem-example) VPN to your VPC. For example, you might choose to set up a client-to-site connection with a VPN Client.
    2. For client-to-site VPN setups, you must specify the {{site.data.keyword.vpc_short}} Private DNS service addresses when you provision the VPN server as mentioned in the [considerations](/docs/vpc?topic=vpc-client-to-site-vpn-planning#existing-vpc-configuration-considerations). You must also create a VPN route after the VPN server is provisioned, with the destination `161.26.0.0/16` and action `translate`.
    3. For site-to-site VPN setups, you must follow the [Accessing service endpoints through VPN guide](/docs/vpc?topic=vpc-build-se-connectivity-using-vpn) and configure the {{site.data.keyword.vpc_short}} Private DNS service addresses.
    4. Verify that you are connected to the VPC through your {{site.data.keyword.vpc_short}} VPN connection.

2. To log in to your cluster, choose from the following options.
    * **Log in as admin**:
        1. Make sure that you have the [**Administrator** platform access role for the cluster](/docs/openshift?topic=openshift-iam-platform-access-roles).
        2. Set your command line context for the cluster and download the TLS certificates and permission files for the administrator.
            ```sh
            ibmcloud oc cluster config -c <cluster_name_or_ID> --admin --endpoint vpe
            ```
            {: pre}

    * **Log in with an API key**: See [Using an API key to log in to {{site.data.keyword.redhat_openshift_notm}}](/docs/openshift?topic=openshift-access_cluster#access_api_key).
    * **Log in with {{site.data.keyword.cloud_notm}} passcode**:
        1. Get the **VPE** address and the master **URL** in the output of the following command.
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
            oc login -u passcode -p <iam_passcode> --server=https://<VPE_URL>:<port_from_the_master_URL>
            ```
            {: pre}

            The login procedure will notify that certificate signed by an unknown authority as it is a self-signed certificate generated by IBM.

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

## Creating additional Virtual Private Endpoint gateways in other VPCs and accounts
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
    
    1. If you get an error "Could not find service", verify the Target CRN is correct. If correct, you need to create the authorization in the target account. See [Creating service authorization for cross-account VPE in the console](/docs/vpc?topic=vpc-ordering-cross-account-endpoint-gateway&interface=ui#cross-account-vpe-prerequisite-console).

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
        * Context Based Restriction (CBR) rules on the target cluster allow private traffic from the source VPC (add the three "Cloud Service Endpoint source addresses" from your source VPC to the private CBR rule)


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


## Accessing clusters from automation tools by using an API key
{: #access_automation}

{{site.data.keyword.openshiftlong_notm}} is integrated with {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM). With IAM, you can authenticate users and services by using their IAM identities and authorize actions with access roles and policies. When you authenticate as a user through the {{site.data.keyword.redhat_openshift_notm}} console, your IAM identity is used to generate a {{site.data.keyword.redhat_openshift_notm}} login token that you can use to log in to the command line. You can automate logging in to your cluster by creating an IAM API key or service ID to use for the `oc login` command.
{: shortdesc}

### Using an API key to log in to clusters
{: #access_api_key}

You can create an {{site.data.keyword.cloud_notm}} IAM API key and then use the API key to log in to a {{site.data.keyword.redhat_openshift_notm}} cluster. With API keys, you can use the credentials of one user or shared account to access a cluster, instead of logging in individually. You might also create an API key for a [service ID](#access_service_id). For more information, see [Understanding API keys](/docs/iam?topic=iam-manapikey).
{: shortdesc}

1. Create an {{site.data.keyword.cloud_notm}} API key.
    Save your API key in a secure location. You can't retrieve the API key again. If you want to export the output to a file on your local machine, include the `--file <path>/<file_name>` option.
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

    2. Download and add the `kubeconfig` configuration file for your cluster to your existing `kubeconfig` in `~/.kube/config` or the last file in the `KUBECONFIG` environment variable. **Note**: If you enabled the private cloud service endpoint and want to use it for the cluster context, include the `--endpoint private` option. To use the private cloud service endpoint to connect to your cluster, you must be in your {{site.data.keyword.cloud_notm}} private network or connected to the private network through a [VPC VPN connection](/docs/vpc?topic=vpc-vpn-onprem-example), or for classic infrastructure, a [classic VPN connection](/docs/iaas-vpn?topic=iaas-vpn-getting-started) or [{{site.data.keyword.dl_full_notm}}](/docs/dl?topic=dl-get-started-with-ibm-cloud-dl).
        ```sh
        ibmcloud oc cluster config -c <cluster_name_or_ID> [--endpoint private]
        ```
        {: pre}

3. Exchange your {{site.data.keyword.cloud_notm}} IAM API key credentials for a {{site.data.keyword.redhat_openshift_notm}} access token. You can log in from the CLI or API. For more information, see the [{{site.data.keyword.redhat_openshift_notm}} docs](https://docs.redhat.com/en/documentation/openshift_container_platform/4.20/html/authentication_and_authorization/configuring-internal-oauth){: external}.

    **Log in by using the `oc` CLI**:
    Log in to your cluster with the `oc login` command. The username (`-u`) is `apikey` and the password (`-p`) is your {{site.data.keyword.cloud_notm}} IAM API key value. To use the private cloud service endpoint, include the `--server=<private_service_endpoint>` option.
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

    2. Get the token endpoint of the {{site.data.keyword.redhat_openshift_notm}} `oauth` server.
        ```sh
        curl <master_URL>/.well-known/oauth-authorization-server | jq -r .token_endpoint
        ```
        {: pre}

        Example output
        ```sh
        <token_endpoint>/oauth/token
        ```
        : screen}
        
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

    5. Use your cluster master URL and the access token to access the {{site.data.keyword.redhat_openshift_notm}} API, such as to list all the pods in your cluster. For more information, see the [{{site.data.keyword.redhat_openshift_notm}} API documentation](https://docs.redhat.com/en/documentation/openshift_container_platform/4.20/html/api_overview/index){: external}.

        Example curl request:
        ```sh
        curl -H "Authorization: Bearer <access_token>" '<master_URL>/api/v1/pods'
        ```
        {: pre}

### Using a service ID to log in to clusters
{: #access_service_id}

You can create an {{site.data.keyword.cloud_notm}} IAM service ID, make an API key for the service ID, and then use the API key to log in to a {{site.data.keyword.redhat_openshift_notm}} cluster. You might use service IDs so that apps that are hosted in other clusters or clouds can access your cluster's services. Because service IDs are not tied to a specific user, your apps can authenticate if individual users leave your account. For more information, see [Creating and working with service IDs](/docs/iam?topic=iam-serviceids).
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
    | `--roles <service_access_role>` | Required. Enter the access role that you want the service ID to have to your {{site.data.keyword.redhat_openshift_notm}} cluster. [Platform access roles](/docs/openshift?topic=openshift-iam-platform-access-roles) permit cluster management activities such as creating worker nodes. [Service access roles](/docs/openshift?topic=openshift-iam-platform-access-roles) correspond to RBAC roles that permit {{site.data.keyword.redhat_openshift_notm}} management activities within the cluster, such as for Kubernetes resources like pods and namespaces. For multiple roles, include a comma-separated list. Possible values are `Administrator`, `Operator`, `Editor`, and `Viewer` (platform access roles); and `Reader`, `Writer`, and `Manager` (service access roles). |
    | `--service-instance <cluster_ID>` | To restrict the policy to a particular cluster, enter the cluster's ID. To get your cluster ID, run `ibmcloud oc clusters`. If you don't include the service instance, the access policy grants the service ID access to all your clusters, Kubernetes and {{site.data.keyword.redhat_openshift_notm}}. You can also scope the access policy to a region (`--region`) or resource group (`--resource-group-name`). |
    {: caption="Understanding this command's components" caption-side="bottom"}
    
3. Create an API key for the service ID. Name the API key similar to your service ID, and include the service ID that you previously created, `<cluster_name>-id`. Be sure to give the API key a description that helps you retrieve the key later. Save your API key in a secure location. You can't retrieve the API key again. If you want to export the output to a file on your local machine, include the `--file <path>/<file_name>` option.

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

    2. Download and add the `kubeconfig` configuration file for your cluster to your existing `kubeconfig` in `~/.kube/config` or the last file in the `KUBECONFIG` environment variable. **Note**: If you enabled the private cloud service endpoint and want to use it for the cluster context, include the `--endpoint private` option. To use the private cloud service endpoint to connect to your cluster, you must be in your {{site.data.keyword.cloud_notm}} private network or connected to the private network through a [VPC VPN connection](/docs/vpc?topic=vpc-vpn-onprem-example), or for classic infrastructure, a [classic VPN connection](/docs/iaas-vpn?topic=iaas-vpn-getting-started) or [{{site.data.keyword.dl_full_notm}}](/docs/dl?topic=dl-get-started-with-ibm-cloud-dl).
    
        ```sh
        ibmcloud oc cluster config -c <cluster_name_or_ID> [--endpoint private]
        ```
        {: pre}

5. [Use the service ID's API key to log in to your {{site.data.keyword.redhat_openshift_notm}} cluster](#access_api_key). The username (`-u`) is `apikey` and the password (`-p`) is your API key value. To use the private cloud service endpoint, include the `--server=<private_service_endpoint>` option.

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
