---

copyright:
  years: 2014, 2021
lastupdated: "2021-10-04"

keywords: openshift, roks, rhoks, rhos

subcollection: openshift
content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

  

# Why is the status of my OpenShift Data Foundation storage cluster stuck at `Failed to reconcile`.
{: #ts-ocs-roks-debug}

**Infrastructure provider**:
* <img src="images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Classic
* <img src="images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> VPC

## ODF device set creation fails due to PVC names exceeding the Kubernetes character limit
{: #ocs-ts-sc-character-limit}


When you create your ODF storage cluster and you run `oc describe storagecluster <storage-cluster-name>`, you see an error similar to the following.
{: tsSymptoms}

```sh
ceph-cluster-controller: failed to reconcile. failed to reconcile cluster "ocs-storagecluster-cephcluster": failed to configure local ceph cluster: failed to create cluster: failed to start ceph osds: 3 failures encountered while running osds in namespace openshift-storage: failed to create "provision" job for node "ocs-deviceset-ibmc-vpc-block-metro-retain-10iops-tier-0-datnv6k". Job.batch "rook-ceph-osd-prepare-aaa000aaa111a1a0e10ba1a11aa1a119" is invalid: [spec.template.spec.volumes[8].name: Invalid value: "ocs-deviceset-ibmc-vpc-block-metro-retain-10iops-tier-0-aaaaa1b-bridge": must be no more than 63 characters
```
{: screen}


Kubernetes PVC names must be fewer than 63 characters.
{: tsCauses}


If you a have multizone VPC cluster and create your ODF storage cluster by using a `retain` class like the `ibmc-vpc-block-metro-retain-10iops-tier`, the corresponding ODF device set PVCs that are created by using this storage class are assigned names that exceed the 63 character limit.


Create a custom storage class that uses the same configuration as the pre-defined storage class that you want to use, but with a name that does not exceed 63 characters.
{: tsResolve}

1. Get the YAML configuration of the storage class that you want to use in your ODF storage cluster and save it in a file on your local machine.
    ```sh
    oc get sc ibmc-vpc-block-metro-retain-10iops-tier -o yaml
    ```
    {: pre}

1. Edit the name of the storage class. Make sure that the name of your custom storage class is fewer than 30 characters to allow for the ODF storage cluster device set IDs to be under the 63 character kubernetes limit. Create the storage class in your cluster.
    ```sh
    oc create -f <custom-storage-class.yaml>
    ```
    {: pre}

1. Clean up your [ODF deployment](/docs/openshift?topic=openshift-ocs-manage-deployment#ocs-rm-cleanup-resources).

1. Create an ODF deployment that uses the custom storage class you created.





