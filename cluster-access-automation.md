---

copyright:
  years: 2014, 2026
lastupdated: "2026-08-13"

keywords: openshift, clusters, access, api key, service id, automation, ci/cd, pipeline

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}

# Accessing clusters from automation tools
{: #cluster-access-automation}

Use an {{site.data.keyword.cloud_notm}} IAM API key or service ID to log in to a cluster from automated pipelines, CI/CD tools, or scripts that run non-interactively.
{: shortdesc}

## Using an API key to log in
{: #access-api-key}

An IAM API key is the recommended approach for automation and CI/CD pipelines.

1. Create an API key and save the output — the key value cannot be retrieved again.
   ```sh
   ibmcloud iam api-key-create <name>
   ```
   {: pre}

1. Log in with the API key.
   ```sh
   ibmcloud login --apikey API_KEY
   ```
   {: pre}

1. Set the cluster context.
   ```sh
   ibmcloud oc cluster config -c CLUSTER_NAME_OR_ID
   ```
   {: pre}

1. Log in to the cluster.
   ```sh
   oc login -u apikey -p API_KEY [--server=PRIVATE_SERVICE_ENDPOINT]
   ```
   {: pre}

## Using a service ID to log in
{: #access-service-id}

Use a service ID when apps in other clusters or clouds need to access your cluster's services, or when you need credentials that are not tied to a specific user.

1. Create a service ID.
   ```sh
   ibmcloud iam service-id-create CLUSTER_NAME-id --description "Service ID for cluster CLUSTER_NAME"
   ```
   {: pre}

1. Assign an IAM policy to the service ID.
   ```sh
   ibmcloud iam service-policy-create SERVICE_ID --service-name containers-kubernetes --roles ROLE --service-instance CLUSTER_ID
   ```
   {: pre}

1. Create an API key for the service ID.
   ```sh
   ibmcloud iam service-api-key-create CLUSTER_NAME-key SERVICE_ID
   ```
   {: pre}

1. Use the API key to log in by following the steps in [Using an API key to log in](#access-api-key).

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
