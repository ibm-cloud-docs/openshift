---

copyright: 
  years: 2014, 2022
lastupdated: "2022-02-18"

keywords: openshift

subcollection: openshift

content-type: troubleshoot

---


{{site.data.keyword.attribute-definition-list}}


# Why are the file systems for worker nodes changed to read-only?
{: #readonly_nodes}
{: support}

**Infrastructure provider**: ![Classic infrastructure provider icon.](images/icon-classic-2.svg) Classic



You might see one of the following symptoms {: #stuck_creating_state}:
{: tsSymptoms}

- When you run `oc get pods -o wide`, you see that multiple pods that are running on the same worker node are stuck in the `ContainerCreating` state.
- When you run a `oc describe` command, you see the following error in the **Events** section: `MountVolume.SetUp failed for volume ... read-only file system`.

The file system on the worker node is read-only.
{: tsCauses}

Back up your data and reload your worker node.
{: tsResolve}

1. Back up any data that might be stored on the worker node or in your containers.
2. For a short-term fix to the existing worker node, reload the worker node.
    ```sh
    ibmcloud oc worker reload --cluster <cluster_name> --worker <worker_ID>
    ```
    {: pre}

For a long-term fix, [update the flavor of your worker pool](/docs/containers?topic=containers-update#machine_type).







