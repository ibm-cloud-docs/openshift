---

copyright: 
  years: 2024, 2025
lastupdated: "2025-09-17"

keywords: openshift, {{site.data.keyword.openshiftlong_notm}}, secure by default, outbound traffic protection, 4.15

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}

# Managing outbound traffic protection in VPC clusters
{: #sbd-allow-outbound}

[Virtual Private Cloud]{: tag-vpc}
[4.15 and later]{: tag-red}

Review the following options for managing outbound traffic protection in {{site.data.keyword.openshiftlong_notm}} VPC clusters. You can allow all outbound access or selectively allow outbound traffic to the components that your apps need.

In many of the following scenarios, you have the option to add custom rules to your `kube-<clusterID>` security group as a way to allow outbound traffic to specific resources. Note that rules you add to the `kube-<clusterID>` security group are removed if you later run `ibmcloud oc security-group reset`. Resetting your security groups restores the default rules and removes any that you have added.
{: important}



## Disabling outbound traffic protection
{: #new-cluster-sbd}

[Virtual Private Cloud]{: tag-vpc}
[4.15 and later]{: tag-red}

Review the following options for disabling outbound traffic protections for new clusters.

You can toggle outbound traffic protection on and off by using the `outbound traffic protection enable` and `disable` commands. You might want to switch between the two configurations when you are moving away from allowing all outbound traffic.
{: tip}

### Option 1: Disabling outbound traffic protection when you create a cluster
{: #sbd-disable-1}

This option allows all outbound network connections.
{: note}

- In the console, select the **Allow outbound traffic** option.
- In the CLI, when you create a cluster by using the `cluster create vpc-gen2` [command](/docs/openshift?topic=openshift-kubernetes-service-cli#cli_cluster-create-vpc-gen2), specify the `--disable-outbound-traffic-protection` option.
- In Terraform, specify the `disable_outbound_traffic_protection = true` option.
- In the API, specify the `disableOutboundTrafficProtection=true` option.


### Option 2: Allowing outbound traffic through a custom security group
{: #sbd-disable-2}

Before creating your cluster, create a [custom security group](/docs/vpc?topic=vpc-using-security-groups) in your VPC that allows access to the external site or service that your cluster needs to access. Then, attach this security group to your cluster during cluster creation.

- In the console, specify your custom security group.
- In the CLI, when you create a cluster by using the `cluster create vpc-gen2` [command](/docs/openshift?topic=openshift-kubernetes-service-cli#cli_cluster-create-vpc-gen2), specify the `--cluster-security-group <security-group-ID>` option and include your custom security group ID.
- In Terraform, specify the `security_groups` [option](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/container_vpc_cluster#security_groups){: external} and include your custom group.

## Disabling outbound traffic protection for existing clusters
{: #existing-cluster-sbd}

[Virtual Private Cloud]{: tag-vpc}
[4.15 and later]{: tag-red}

Review your options for disabling outbound traffic protection after you've provisioned a cluster.

### Option 1: Disabling outbound traffic protection from the CLI
{: #sbd-disable-cli-option}

This option allows all external network connections.
{: note}

```sh
ibmcloud oc vpc outbound-traffic-protection disable --cluster CLUSTER
```
{: pre}

### Option 2: Adding a security group rule to the default cluster worker security group
{: #sbd-disable-custom-sg}

You can add a security group rule to the cluster worker security group (`kube-<clusterID>`) that allows access to the specific external site. Repeat this step for each site or subnet that your cluster needs to access. For more information, [Example scenarios for selectively allowing outbound traffic](#sbd-examples).

```sh
ibmcloud is sg-rulec kube-<clusterID> outbound all --remote <IP-address-or-subnet>
```
{: pre}

## Enabling outbound traffic protection for existing clusters
{: #sbd-enable-existing}

[Virtual Private Cloud]{: tag-vpc}
[4.15 and later]{: tag-red}

To enable outbound protection for your existing 4.15 clusters, run the following command. Note that enabling outbound traffic protection blocks all outbound traffic.

```sh
ibmcloud oc vpc outbound-traffic-protection enable --cluster CLUSTER
```
{: pre}

## Example scenarios for selectively allowing outbound traffic
{: #sbd-examples}

Review the following sections for instructions on how to allow outbound traffic to common resources and components such as external container registries like `quay.io`, the Red Hat Marketplace, and OperatorHub. Note that when you selectively allow outbound traffic by creating custom security group rules, your changes will get removed if you reset your security group to the default settings by running `ibmcloud oc security-group reset` command.

### Accessing images from external container registries like DockerHub or `quay.io`
{: #sbd-example-quay}

To access images from registries like DockerHub or `quay.io` or `registry.redhat.com`, choose from one of the following options.


* Disable outbound traffic protection.
    ```sh
    ibmcloud oc vpc outbound-traffic-protection disable --cluster CLUSTER
    ```
    {: pre}

* Mirror the images your app needs to `icr.io`. Pull, tag, and push those images to {{site.data.keyword.registrylong_notm}}. For more information, see [Pushing images to {{site.data.keyword.registrylong_notm}}](/docs/openshift?topic=openshift-images&interface=ui#push-images).




### Allowing outbound traffic to Red Hat Marketplace and OperatorHub
{: #sbd-example-oh}

The following steps enable all outbound traffic. If you don't want to enable this, you can [mirror the Red Hat Marketplace and OperatorHub images that your app needs](#sbd-example-quay) to to your own `icr.io`.

1. Disable outbound traffic protection.
    ```sh
    ibmcloud oc vpc outbound-traffic-protection disable --cluster CLUSTER
    ```
    {: pre}

1. Patch OperatorHub on your cluster to allow the pods to start.

    ```sh
    oc patch OperatorHub cluster --type json -p '[{"op": "remove", "path": "/spec/disableAllDefaultSources"}]'
    ```
    {: pre}

To revert these changes later and disable OperatorHub, complete the following steps.

1. Enable outbound traffic protection.

    ```sh
    ibmcloud oc vpc outbound-traffic-protection enable --cluster CLUSTER
    ```
    {: pre}

1. Patch OperatorHub on your cluster to disable the pods

    ```sh
    oc patch OperatorHub cluster --type json -p '[{"op": "add", "path": "/spec/disableAllDefaultSources", "value": true}]'
    ```
    {: pre}

### Allowing outbound traffic to Image Streams
{: #sbd-example-is}

To access image streams from your cluster, choose from the following options. 


* Mirror the images you need to the `icr.io` registry. For more information, see [Pushing images to {{site.data.keyword.registrylong_notm}}](/docs/openshift?topic=openshift-images&interface=ui#push-images).

* Disable outbound traffic protection.
    ```sh
    ibmcloud oc vpc outbound-traffic-protection disable --cluster CLUSTER
    ```
    {: pre}

* Add a security group rule to the `kube-<clusterID>` security group to the IP addresses of the image stream you want to use. Note that IP addresses for image streams might change.
    ```sh
    ibmcloud is sg-rulec kube-vpegw-<clusterID> inbound tcp --port-min PORT  --port-max PORT --remote IP-OR-CIDR
    ```
    {: pre}


### Allowing outbound traffic for remote health monitoring with Telemetry
{: #sbd-example-telemetry}

To allow remote health monitoring, you must disable outbound traffic protection by running the following command.

```sh
ibmcloud oc vpc outbound-traffic-protection disable --cluster CLUSTER
```
{: pre}



### Accessing 4.15 clusters and the web console over the VPE
{: #sbd-example-vpe}

You can configure Kubernetes to allow cluster access via the private vpe gateway. This option is available for both private-only and also public and private VPC clusters. Because access is via the private endpoint, the customer must set up a VPN from the client to their VPC to access the cluster.

Beginning with 4.15 clusters, an additional security group rule is needed for VPE access to work. The additional security group rule is needed for both private-only clusters and cluster with public and private endpoints.

1. List your VPN servers.
    ```sh
    ibmcloud is vpn-servers
    ```
    {: pre}

1. Get the details of your VPN server.
    ```sh
    ibmcloud is vpn-server SERVER
    ```
    {: pre}

1. Get the **Client IP pool** of your VPN server.
    ```sh
    ibmcloud is vpn-server | grep "Client IP pool"
    ```
    {: pre}

1. Get the details of your cluster and note the VPE port.

    ```sh
    ibmcloud ks cluster get --cluster <clusterID>
    ```
    {: pre}

1. Start your VPN on the client.

1. Access your cluster via VPE.
    ```sh
    ibmcloud ks cluster config --admin --cluster <clusterID> --endpoint vpe
    ```
    {: pre}

1. List pods. Note that this command fails because the client cannot access the cluster via the VPN through the VPE gateway.
    ```sh
    kubectl get pods -A
    ```
    {: pre}

1. Add a security group rule to the `kube-vpegw-<clusterID>` for your VPN. The remote in this case comes from the VPN’s client IP CIDR.

    ```sh
    ibmcloud is sg-rulec kube-vpegw-<clusterID> inbound tcp --port-min PORT  --port-max PORT --remote IP-OR-CIDR
    ```
    {: pre}

    Example command.

    ```sh
    ibmcloud is sg-rulec kube-vpegw-<clusterID> inbound tcp --port-min 30829  --port-max 30829 --remote 192.168.192.0/22
    ```
    {: pre}

1. List pods.
    ```sh
    kubectl get pods -A
    ```
    {: pre}


### Allowing outbound traffic for webhooks
{: #sbd-example-webhook}

If you are using webhooks that contact a URL or service external to the cluster, you must add security group rules that allow outbound traffic from your cluster workers to the URL or external service. Alternatively, you can disable outbound traffic protection completely.

Usually, admission webhooks that use cluster service references do not require any changes.

In the following example, an admission webhook that connects to a cluster service  does not usually require any changes because the master connects to the service via the Konnectivity connection, which is allowed by default. One exception would be if the pods implementing that cluster service need to connect to a URL or some external service. If so, then allow those pods to access the URL or external service, as shown in this example.

```yaml
apiVersion: admissionregistration.k8s.io/v1
kind: ValidatingWebhookConfiguration
metadata:
  name: my-cluster-service.webhook.io
webhooks:
- admissionReviewVersions:
  - v1
  clientConfig:
    caBundle: ABCDEFG...
    service:
      name: my-admission-webhook
      namespace: default
      path: /validate
      port: 443
...

```
{: codeblock}


However, if your admission webhooks use a URL, additional security group rules are required.

Example webhook that connects to a URL.

```yaml
apiVersion: admissionregistration.k8s.io/v1
kind: ValidatingWebhookConfiguration
metadata:
  name: my-url.webhook.io
webhooks:
- admissionReviewVersions:
  - v1
  clientConfig:
    caBundle: ABCDEFG...
    url: https://webhook.ibm.com:20001/validate
...
```
{: codeblock}


To allow access to the external URL or service for your webhook, you can choose one of the following options

* Disable outbound traffic protection by running the following command.

    ```sh
    ibmcloud oc vpc outbound-traffic-protection disable --cluster CLUSTER
    ```
    {: pre}

* Add outbound security group rules to the `kube-<clusterID>` security group to allow the cluster workers to connect to. In the previous example, the `webhook.ibm.com` service on port `20001` is used.

    1. Look up the IPs for the URL to access by using `dig`.

        ```sh
        dig +short URL
        ```
        {: pre}

        Example command.
        ```sh
        dig +short webhook.ibm.com
        ```
        {: pre}

        Example output
        ```sh
        1.2.3.4
        4.5.6.7
        ```
        {: screen}

    1. Create a rule for each IP address that is returned.

        ```sh
        ibmcloud is sg-rulec kube-<clusterID> outbound all --remote <IP-address-or-subnet>
        ```
        {: pre}

        Example commands.
        ```sh
        ibmcloud is sg-rulec kube-CLUSTERID outbound tcp --port-min 20001 --port-max 20001 --remote 1.2.3.4
        ibmcloud is sg-rulec kube-CLUSTERID outbound tcp --port-min 20001 --port-max 20001 --remote 4.5.6.7
        ```
        {: pre}


For more information, see [Dynamic Admission Control](https://kubernetes.io/docs/reference/access-authn-authz/extensible-admission-controllers/){: external}
{: tip}


### Allowing outbound traffic to a public service
{: #sbd-example-gh}

If the external service or services being called by your application have a small set of IPs/CIDRs used to host that service that do not change very often you can selectively allow outbound access to those IPs or CIDRs on your `kube-clusterID` security group.

The following example uses the github.com APIs at `api.github.com`.


1. Find the IPs programmatically by `curl`.

    ```sh
    curl -sS -H "Accept: application/vnd.github+json" https://api.github.com/meta | jq '.api'
    ```
    {: pre} 

1. Add each of the CIDRs you found in the previous step as the destination of an outbound security group rule on the `kube-clusterID` security group. Alternatively, you can create a custom security group that you add to your cluster workers at cluster create time.

    ```sh
    ibmcloud is sg-rulec kube-<clusterID> outbound all --remote <IP-address-or-subnet>
    ```
    {: pre}


For more information, see [About GitHub's IP addresses](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/about-githubs-ip-addresses).

### Considerations for hub and spoke VPCs with outbound traffic protection
{: #sbd-example-hubspoke}

In a hub and spoke model, only the hub VPC cluster is used for DNS resolution. The spoke clusters access DNS via the hub. Hub and spoke clusters are most often in different VPCs, which are connected via Transit Gateway.

In version 4.15 and later clusters, the hub and spoke model does not work without adjustments to the security groups for each. These adjustments allow traffic between the hub and spoke VPCs.

1. Update the clusters in the spoke VPC so they can access the hub VPC by adding rules to the `kube-<clusterID>` security group for each spoke cluster. Make sure to add an outbound rule to **each** VPC subnet CIDR the hub cluster workers are deployed in. For example, if a spoke is connecting to a single hub and that hub has workers in three zones, then three rules must be added to the spoke's `kube-<clusterID>` security group, one for each subnet.

    ```sh
    ibmcloud is sg-rulec kube-<spoke-clusterID> outbound all --remote <hub-subnet-CIDR>
    ```
    {: pre}

1. Update the hub clusters to allow traffic from the spokes by adding rules to the hub’s shared VPE Gateway security group (`kube-vpegw-vpcID`). Alternatively, if you use your own custom security groups for the shared VPE gateways, add rules to those custom security groups instead.

1. Run the following command to find the VPE gateways, then look at the details of the gateway to find its associated security group. Note the security group ID to add rules to it in the next step.

    ```sh
    ibmcloud is egs
    ```
    {: pre} 

1. Add an inbound rule from **each** VPC subnet that the spoke workers are deployed in. For example, if spokes are deployed to three different zones but to a single subnet in each of those zones, then three rules are added to the hub’s shared VPE Gateway security groups.
    ```sh
    ibmcloud is sg-rulec kube-vpegw-<hub-vpcID> inbound all --remote <spoke-subnet-CIDR>
    ```
    {: pre}


### Allowing temporary traffic to the cluster API server over the public network
{: #sbd-example-api-server-backup}

VPC cluster workers use the private network to communicate with the cluster master. Previously, for VPC clusters that had the public service endpoint enabled, if the private network was blocked or unavailable, then the cluster workers could fall back to using the public network to communicate with the cluster master.

In 4.15 and later clusters, falling back to the public network is not an option because public outbound traffic from the cluster workers is blocked. You might want to disable outbound traffic protection to allow this public network backup option, however, there is a better alternative. Instead, if there a temporary issue with the worker-to-master connection over the private network, then, at that time, you can add a temporary security group rule to the `kube-clusterID` security group to allow outbound traffic to the cluster master `apiserver` port. Later, when the problem is resolved, you can remove the temporary rule.

You can choose one of the following options to allow traffic over the public network if the private network is down.

* Add a security group rule to the `kube-clusterID` security group to allow traffic to the API server.
    1. Get your cluster details and note of the API server port.

        ```sh
        ic ks cluster get --cluster <clusterID>
        ```
        {: pre}

        Example output where the API server port is `30685`.

        ```sh
        Name:                           prestg-sbd-vpc-4.15
        ID:                             coekl4a107ovqfndhh60
        ...
        Public Service Endpoint URL:    https://c100-e.containers.pretest.cloud.ibm.com:30685
        Private Service Endpoint URL:   https://c100.private.containers.pretest.cloud.ibm.com:30685
        ...
        ```
        {: screen}

    1. Add an outbound security group rule from your `kube-<clusterID>` to `0.0.0.0/0` to allow all public network access.
        ```sh
        ibmcloud is sg-rulec kube-<clusterID> outbound tcp --port-min <API port> --port-max <API port> --remote 0.0.0.0/0
        ```
        {: pre}

        Example command with an API server port of `30685`.
        ```sh
        ibmcloud is sg-rulec kube-<clusterID> outbound tcp --port-min 30685 --port-max 30685 --remote 0.0.0.0/0
        ```
        {: pre}


* Disable outbound traffic protection.
    ```sh
    ibmcloud oc vpc outbound-traffic-protection disable --cluster CLUSTER
    ```
    {: pre}
