---

copyright:
  years: 2014, 2026
lastupdated: "2026-06-26"


keywords: openshift

subcollection: openshift
content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}


# Why is the status of my OpenShift Data Foundation storage cluster stuck at `Failed to reconcile`?
{: #ts-ocs-roks-debug}
{: support}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf}

When you create your OpenShift Data Foundation storage cluster and run `oc describe storagecluster <storage-cluster-name>`, you see an error indicating that PVC names exceed the Kubernetes character limit.
{: shortdesc}



Device sets are groups of OSDs (Object Storage Daemons) that OpenShift Data Foundation uses to distribute data across your cluster. When you create a storage cluster, OpenShift Data Foundation automatically creates PVCs for these device sets.

When you run the describe command, you see an error similar to the following example.
{: tsSymptoms}

```sh
ceph-cluster-controller: failed to reconcile. failed to reconcile cluster "ocs-storagecluster-cephcluster": failed to configure local ceph cluster: failed to create cluster: failed to start ceph osds: 3 failures encountered while running osds in namespace openshift-storage: failed to create "provision" job for node "ocs-deviceset-ibmc-vpc-block-metro-retain-10iops-tier-0-datnv6k". Job.batch "rook-ceph-osd-prepare-aaa000aaa111a1a0e10ba1a11aa1a119" is invalid: [spec.template.spec.volumes[8].name: Invalid value: "ocs-deviceset-ibmc-vpc-block-metro-retain-10iops-tier-0-aaaaa1b-bridge": must be no more than 63 characters
```
{: screen}


Kubernetes PVC names must be fewer than 63 characters. If you have a multizone VPC cluster and create your OpenShift Data Foundation storage cluster by using a `retain` storage class like `ibmc-vpc-block-metro-retain-10iops-tier`, the corresponding device set PVCs are assigned names that exceed the 63 character limit.
{: tsCauses}

Create a custom storage class with a shorter name to ensure that the generated PVC names stay within the Kubernetes character limit.
{: tsResolve}

1. Get the YAML configuration of the storage class that you want to use in your ODF storage cluster and save it in a file on your local machine.
    ```sh
    oc get sc ibmc-vpc-block-metro-retain-10iops-tier -o yaml
    ```
    {: pre}

1. Edit the name of the storage class. Make sure that the name of your storage class is fewer than 30 characters to allow for the OpenShift Data Foundation storage cluster device set IDs to be under the 63 character Kubernetes limit. Create the storage class in your cluster.
    ```sh
    oc create -f <custom-storage-class.yaml>
    ```
    {: pre}

1. Clean up your [OpenShift Data Foundation deployment](/docs/openshift?topic=openshift-ocs-manage-deployment).

1. [Create an OpenShift Data Foundation deployment](/docs/openshift?topic=openshift-deploy-odf-vpc) that uses the storage class you created.
