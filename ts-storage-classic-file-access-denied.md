---

copyright: 
  years: 2025, 2026
lastupdated: "2026-01-06"


keywords: openshift, storage, file storage vpc, access, volume, access denied, mount

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Classic: Why am I denied server access when mounting a volume to a worker node?
{: #ts-storage-file-access-denied}

[Classic infrastructure]{: tag-classic-inf}


When you try to mount a file storage volume, you get an error stating that access is denied by the server. 
{: tsSymptoms}

Example error. 

```sh
MountVolume.SetUp failed for volume "pvc-XXXX" : mount failed: exit status 32 Mounting command: mount Mounting arguments: -t nfs fsf-region-fz.service.softlayer.com:/VOLUME/data01 /var/data/kubelet/pods/1a11b234-567c-89d0-1ef2-34g567abc89/volumes/kubernetes.io~nfs/pvc-XXXX Output: mount.nfs: access denied by server while mounting fsf-region-fz.service.softlayer.com:/VOLUME/data01
```
{: screen}

Your worker nodes might not have access to the your file storage.
{: tsCauses}

Follow the steps to ensure that your worker nodes have access. Note that these steps require classic infrastructure permissions. 
{: tsResolve}


## In the CLI
{: #cli}

1. Get the volume ID. 

    ```sh
    kubectl describe pv PVNAME -n NAMESPACE
    ```
    {: pre}

3. Get the ID of the worker node's subnet. 

    ```sh
    ibmcloud oc worker get --worker <worker_node_id> --cluster <cluster_id>
    ```
    {: pre}

    Example `Subnets` section in output.

    ```sh
    Subnets
    ID                                          IP Address                CIDR
    0101-0ef11da0-01c1-0011-1f7-01010db11e00    XXX.XX.XXX.10 (primary)   XXX.XX.XXX.10/24
    ```
    {: screen}


3. Run the command to authorize access. Specify the volume ID and worker subnet ID that you found in the previous steps.

    ```sh
    ibmcloud sl file access-authorize <volume_id> --subnet-id <worker_subnet_ID>
    ```
    {: pre}

## In the UI
{: #ui}

1. In the UI, navigate to your [Clusters](https://cloud.ibm.com/containers/cluster-management/clusters){: external} dashboard. Click on your cluster, then click **Worker nodes**.

2. Click on the relevant worker node to find the **Subnet** name. 

3. Navigate to the Classic Infrastructure [File Storage](https://cloud.ibm.com/cloud-storage/file){: external} dashboard and click on the volume you want to mount. 

4. Click **Actions** > **Authorize Host**.

5. Under **Select a host type**, select **Subnets**.

6. In the dropdown, select the subnet that applies to your worker node. 

7. Click **Save**.

