---

copyright: 
  years: 2014, 2024
lastupdated: "2024-01-03"


keywords: portworx, openshift

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}


# Getting help and support
{: #storage_portworx_support}

Contact Portworx support by using one of the following methods.

- Sending an e-mail to `support@purestorage.com`.

- Calling `+1 (866) 244-7121` or `+1 (650) 729-4088` in the United States or one of the [International numbers](https://support.purestorage.com/Pure_Storage_Technical_Services/Technical_Services_Information/Contact_Us).

- Opening an issue in the [Portworx Service Portal](https://support.purestorage.com/Pure_Storage_Technical_Services/Technical_Services_Information/Contact_Us){: external}. If you don't have an account, see [Request access](https://purestorage.force.com/customers/CustomerAccessRequest){: external}.


## Gathering logs
{: #portworx_logs}

You can use the following script to collect log information from your Portworx cluster.
{: shortdesc}


The following script collects Portworx logs from your cluster and saves them on your local machine in the `/tmp/pxlogs` directory.

Before you begin: [Access your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-access_cluster).

1. Clone the `ibmcloud-storage-utilities` repo.
    ```sh
    git clone https://github.com/IBM/ibmcloud-storage-utilities.git
    ```
    {: pre}

2. Navigate to the `px_logcollector` directory.
    ```sh
    cd ibmcloud-storage-utilities/px_utils/px_logcollector/ 
    ```
    {: pre}

3. Run the `px_logcollect.sh` script. You can collect logs from all your worker nodes, or you can specify the `--workers` option and pass the private IP addresses of the worker nodes from where you want to collect logs. If you specify the `--workers` option, the log files are saved in the `/tmp/pxlogs/<worker_node_IP>` directory with the private IP address of each worker node as the folder name. To get the private IP addresses of your worker nodes, run the `oc get nodes` command.

    * **Collect the logs from all worker nodes in your cluster.**

        ```sh
        sudo ./px_logcollect.sh
        ```
        {: pre}

    * **Collect the logs from only certain worker nodes in your cluster.**
        ```sh
        sudo ./px_logcollect.sh --workers <worker-IP> <worker-IP> <worker-IP>
        ```
        {: pre}

4. Review the log files locally. If you can't resolve your issue by reviewing the logs, [open a support ticket](/docs/openshift?topic=openshift-get-help) and provide the log information that you collected.




