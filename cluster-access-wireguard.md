---

copyright: 
  years: 2022, 2022
lastupdated: "2022-12-01"

keywords: access, wireguard, private, ,openshift

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}





# Accessing private clusters by using the WireGuard VPN
{: #cluster-access-wireguard}


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

        To successfully run an `nslookup` command on your private service endpoint URL, remove `https://` and the port from your URL. Alternatively, you can note all IP address CIDRs for the region that your cluster master is in as shown in step 3 of [Opening required ports in a private firewall](/docs/openshift?topic=openshift-firewall#firewall_private).
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
