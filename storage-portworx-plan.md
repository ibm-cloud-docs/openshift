---

copyright: 
  years: 2014, 2025
lastupdated: "2025-05-15"


keywords: portworx, kubernetes, openshift

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}



# Planning your Portworx setup
{: #storage_portworx_plan}

Before you create your cluster and install Portworx, review the following planning steps.
{: shortdesc}

- Decide where you want to store the Portworx metadata. You can use KVDB or an external Database instance. For more information, see [Understanding the key-value store](/docs/openshift?topic=openshift-storage_portworx_kv_store). To learn more about what the key value does, see the [Portworx documentation](https://docs.portworx.com/portworx-enterprise/operations/kvdb-for-portworx/internal-kvdb){: external}.
- Decide whether you want encryption. You can use {{site.data.keyword.hscrypto}} or {{site.data.keyword.keymanagementservicelong_notm}}. For more information, see [Understanding encryption for Portworx](/docs/openshift?topic=openshift-storage_portworx_encryption).
- Decide whether you want to use journal devices. Journal devices allow Portworx to write logs directly to a local disk on your worker node.
- **VPC or Satellite clusters only** - Decide whether you want to use cloud drives. Cloud drives allow you to dynamically provision the Portworx volumes. If you don’t want to use cloud drives, you must manually attach volumes to worker nodes.
- Review the [Limitations](#portworx_limitations).


## Limitations
{: #portworx_limitations}

Review the following Portworx limitations.

| Limitation | Description |
| --- | --- |
| Private-only clusters in Montreal | The default installation method for Portworx Enterprise and Portworx Backup is not yet supported for private-only clusters in the Montreal region. Contact Portworx Support if you need to install Portworx Enterprise or Portworx Backup or in a private-only cluster in Montreal. For more information, see [Portworx Support](/docs/openshift?topic=openshift-storage_portworx_about#portworx-billing-support). | 
| **Classic clusters** Pod restart required when adding worker nodes. | Because Portworx runs as a DaemonSet in your cluster, existing worker nodes are automatically inspected for raw block storage and added to the Portworx data layer when you deploy Portworx. If you add or update worker nodes to your cluster and add raw block storage to those workers, restart the Portworx pods on the new or updated worker nodes so that your storage volumes are detected by the DaemonSet. |
| **VPC clusters** Storage volume reattachment required when updating worker nodes. | When you update a worker node in a VPC cluster, the worker node is removed from your cluster and replaced with a new worker node. If Portworx volumes are attached to the worker node that is replaced, you must attach the volumes to the new worker node. You can attach storage volumes with the [API](/docs/openshift?topic=openshift-utilities#vpc_api_attach) or the [CLI](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_storage_att_cr). Note this limitation does not apply to Portworx deployments that are using cloud drives. |
| The Portworx experimental `InitializerConfiguration` feature is not supported. | {{site.data.keyword.openshiftlong_notm}} does not support the [Portworx experimental `InitializerConfiguration` admission controller](https://github.com/libopenstorage/stork#initializer-experimental){: external}. |
| Private clusters | To install Portworx in a cluster that doesn't have VRF or access to private cloud service endpoints (CSEs), you must create a rule in the default security group to allow inbound and outbound traffic for the following IP addresses: `166.9.24.81`, `166.9.22.100`, and `166.9.20.178`. For more information, see [Updating the default security group](/docs/vpc?topic=vpc-updating-the-default-security-group#updating-the-default-security-group). |
| Portworx Backup | Portworx backup is not supported for {{site.data.keyword.satelliteshort}} clusters. |
{: caption="Portworx limitations"}

## Overview of the Portworx lifecycle
{: #portowrx_lifecycle}

1. Create a [multizone cluster](/docs/openshift?topic=openshift-clusters).
    1. Infrastructure provider: For Satellite clusters, make sure to add block storage volumes to your hosts before attaching them to your location. If you use classic infrastructure, you must choose a bare metal flavor for the worker nodes. For classic clusters, virtual machines have only 1000 Mbps of networking speed, which is not sufficient to run production workloads with Portworx. Instead, provision Portworx on bare metal machines for the best performance.
    2. Worker node flavor: Choose an SDS or bare metal flavor. If you want to use virtual machines, use a worker node with 8 vCPU and 8 GB memory or more.
    3. Minimum number of workers: Two worker nodes per zone across three zones, for a minimum total of six worker nodes.
1. **VPC and non-SDS classic worker nodes only**: [Create raw, unformatted, and unmounted block storage](/docs/openshift?topic=openshift-utilities#manual_block).
1. For production workloads, create an [external Databases for etcd](/docs/openshift?topic=openshift-storage_portworx_kv_store) instance for your Portworx metadata key-value store.
1. **Optional** [Set up encryption](/docs/openshift?topic=openshift-storage_portworx_encryption).
1. [Install Portworx](/docs/openshift?topic=openshift-storage_portworx_deploy).
1. Maintain the lifecycle of your Portworx deployment in your cluster.
    1. When you update worker nodes in [VPC](/docs/openshift?topic=openshift-storage_portworx_update#portworx_vpc_up) clusters, you must take additional steps to re-attach your Portworx volumes. You can attach your storage volumes by using the API or CLI.
        * [Attaching {{site.data.keyword.block_storage_is_short}} volumes with the CLI](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_storage_att_cr).
        * [Attaching {{site.data.keyword.block_storage_is_short}} volumes with the API](/docs/openshift?topic=openshift-utilities#vpc_api_attach).
    2. To remove a Portworx volume, storage node, or the entire Portworx cluster, see [Portworx cleanup](/docs/openshift?topic=openshift-storage_portworx_removing).


## Creating a secret to store the KMS credentials
{: #px_create_km_secret}

**Before you begin:** [Set up encryption](/docs/openshift?topic=openshift-storage_portworx_encryption)

1. Encode the credentials that you retrieved in the previous section to base64 and note all the base64 encoded values. Repeat this command for each parameter to retrieve the base64 encoded value.
    ```sh
    echo -n "<value>" | base64
    ```
    {: pre}

2. Create a project in your cluster called `portworx`.
    ```sh
    oc create ns portworx
    ```
    {: pre}

3. Create a Kubernetes secret named `px-ibm` in the `portworx` project of your cluster to store your {{site.data.keyword.keymanagementservicelong_notm}} information.
    1. Create a configuration file for your Kubernetes secret with the following content.
        ```yaml
        apiVersion: v1
        kind: Secret
        metadata:
          name: px-ibm
          namespace: portworx
        type: Opaque
        data:
          IBM_SERVICE_API_KEY: <base64_apikey>
          IBM_INSTANCE_ID: <base64_guid>
          IBM_CUSTOMER_ROOT_KEY: <base64_rootkey>
          IBM_BASE_URL: <base64_endpoint>
        ```
        {: codeblock}

        `metadata.name`
        :   Enter `px-ibm` as the name for your Kubernetes secret. If you use a different name, Portworx does not recognize the secret during installation.
        
        `data.IBM_SERVICE_API_KEY`
        :   Enter the base64 encoded {{site.data.keyword.keymanagementservicelong_notm}} or {{site.data.keyword.hscrypto}} API key that you retrieved earlier.
        
        `data.IBM_INSTANCE_ID`
        :   Enter the base64 encoded service instance GUID that you retrieved earlier.
        
        `data.IBM_CUSTOMER_ROOT_KEY`
        :   Enter the base64 encoded root key that you retrieved earlier.
        
        `data.IBM_BASE_URL`
        :   {{site.data.keyword.keymanagementservicelong_notm}}: Enter the base64 encoded API endpoint of your service instance.
        :   {{site.data.keyword.hscrypto}}: Enter the base64 encoded Key Management public endpoint.

    2. Create the secret in the `portworx` project of your cluster.
        ```sh
        oc apply -f secret.yaml
        ```
        {: pre}

    3. Verify that the secret is created successfully.
        ```sh
        oc get secrets -n portworx
        ```
        {: pre}

4. If you set up encryption before your installed Portworx, you can now [install Portworx in your cluster](/docs/openshift?topic=openshift-storage_portworx_deploy). To add encryption to your cluster after you installed Portworx, update the Portworx DaemonSet to add `"-secret_type"` and `"ibm-kp"` as additional options to the Portworx container definition.
    1. Update the Portworx DaemonSet.
        ```sh
        oc edit daemonset portworx -n kube-system
        ```
        {: pre}

        Example updated DaemonSet
        ```sh
        containers:
        - args:
        - -c
        - testclusterid
        - -s
        - /dev/sdb
        - -x
        - kubernetes
        - -secret_type
        - ibm-kp
        name: portworx
        ```
        {: codeblock}

        After you edit the DaemonSet, the Portworx pods are restarted and automatically update the `config.json` file on the worker node to reflect that change.

    2. List the Portworx pods in your `kube-system` project.
        ```sh
        oc get pods -n kube-system | grep portworx
        ```
        {: pre}

    3. Log in to one of your Portworx pods.
        ```sh
        oc exec -it <pod_name> -it -n kube-system
        ```
        {: pre}

    4. Navigate in to the `pwx` directory.
        ```sh
        cd etc/pwx
        ```
        {: pre}

    5. Review the `config.json` file to verify that `"secret_type": "ibm-kp"` is added to the **secret** section of your CLI output.
        ```sh
        cat config.json
        ```
        {: pre}

        Example output
        ```sh
        {
        "alertingurl": "",
        "clusterid": "px-kp-test",
        "dataiface": "",
        "kvdb": [
          "etcd:https://portal-ssl748-34.bmix-dal-yp-12a2312v5-123a-44ac-b8f7-5d8ce1d123456.123456789.composedb.com:56963",
          "etcd:https://portal-ssl735-35.bmix-dal-yp-12a2312v5-123a-44ac-b8f7-5d8ce1d123456.12345678.composedb.com:56963"
        ],
        "mgtiface": "",
        "password": "ABCDEFGHIJK",
        "scheduler": "kubernetes",
        "secret": {
            "cluster_secret_key": "",
            "secret_type": "ibm-kp"
        },
        "storage": {
            "devices": [
          "/dev/sdc1"
            ],
            "journal_dev": "",
            "max_storage_nodes_per_zone": 0,
            "system_metadata_dev": ""
        },
        "username": "root",
        "version": "1.0"
        }
        ```
        {: screen}

    6. Exit the pod.

Check out how to [encrypt the secrets in your cluster](/docs/openshift?topic=openshift-encryption), including the secret where you stored your {{site.data.keyword.keymanagementserviceshort}} CRK for your Portworx storage cluster.
{: tip}
