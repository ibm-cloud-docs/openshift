---

copyright: 
  years: 2024, 2025
lastupdated: "2025-03-15"


keywords: openshift, {{site.data.keyword.openshiftlong_notm}}, kubernetes, certificate, rotate, ca rotate

subcollection: openshift


---


{{site.data.keyword.attribute-definition-list}}

# Rotating CA certificates in your cluster
{: #cert-rotate}

Revoke existing certificate authority (CA) certificates in your cluster and issue new CA certificates.
{: shortdesc}

By default, certificate authority (CA) certificates are administered to secure access to various components of your cluster, such as the master API server. As you use your cluster, you might want to revoke the certificates issued by the existing CA. For example, the administrators of your team might use a certificate signing request (CSR) to manually generate certificates that are signed by the cluster's CA for worker nodes in the cluster. If an administrator leaves your organization, you can ensure that they no longer have admin access to your cluster by creating a new CA and certificates for your cluster, and removing the old CA and certificates.

1. Create a CA for your cluster. Certificates that are signed by this new CA are issued for the cluster master components, and the API server is refreshed.

    ```sh
    ibmcloud oc cluster ca create -c CLUSTER
    ```
    {: pre}

2. Ensure that your cluster's master health is normal, the API server refresh is complete, and any master updates are complete. It might take several minutes for the master API server to refresh.

    ```sh
    ibmcloud oc cluster get --cluster CLUSTER
    ```
    {: pre}

3. Check the status of the CA creation. In the output, note the timestamp in the **Action Completed** field.
    ```sh
    ibmcloud oc cluster ca status -c CLUSTER
    ```
    {: pre}

    Example output

    ```sh
    Status:             CA certificate creation complete. Ensure that your worker nodes are reloaded before you start a CA certificate rotation.
    Action Started:     2020-08-30T16:17:56+0000
    Action Completed:   2020-08-30T16:21:13+0000
    ```
    {: screen}

4. Download the updated Kubernetes configuration data and certificates in your cluster's `kubeconfig` file.

    ```sh
    ibmcloud oc cluster config -c CLUSTER --admin --network
    ```
    {: pre}

5. Update any tooling that relies on the previous certificates.
    * If you use the certificate from your cluster's `kubeconfig` file in your own service such as Travis or Jenkins, or if you use `calicoctl` to manage Calico network policies, update your services and automation to use the new certificates.

6. Verify that the timestamps on your new certificates are later than the timestamp that you found in step 3. To check the date on your certificates, you can use a tool such as [KeyCDN](https://tools.keycdn.com/ssl){: external}.

7. [Reload your classic worker nodes](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_reload) or [replace your VPC worker nodes](/docs/openshift?topic=openshift-kubernetes-service-cli#cli_worker_replace) to pick up the certificates that are signed by the new CA.

8. Rotate the old certificates with the new certificates. The old CA certificates in your cluster are removed.
    ```sh
    ibmcloud oc cluster ca rotate -c CLUSTER
    ```
    {: pre}

9. Check the status of the CA certificate rotation.
    ```sh
    ibmcloud oc cluster ca status -c CLUSTER
    ```
    {: pre}

    Example output
    
    ```sh
    Status:             CA certificate rotation complete.
    Action Started:     2020-08-30T16:37:56+0000
    Action Completed:   2020-08-30T16:41:13+0000
    ```
    {: screen}
