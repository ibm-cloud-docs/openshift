---

copyright:
  years: 2014, 2022
lastupdated: "2022-01-20"

keywords: openshift, openshift data foundation, openshift container storage, storage classes

subcollection: openshift

---


{{site.data.keyword.attribute-definition-list}}

# Storage class reference
{: #ocs-sc-ref}

Review the following ODF storage classes.
{: shortdesc}

The ODF storage classes all support dynamic provisioning and are multizone capable.
{: note}

| Feature | Description |
|-----|-----|
| Supported access | rwx |
| Volume mode | File |
| Performance | High |
| Consistency | Strong |
| Resiliency | High |
| Scalability | Multizone |
| Encryption | At rest |
{: caption="Ceph FS storage class details." caption-side="top"}
{: #ocs_sc1}
{: tab-title="ocs-storagecluster-cephfs"}
{: tab-group="sc_ref"}
{: class="simple-tab-table"}
{: summary="The first column contains a feature of the storage class. The second column contains a brief description of the feature."}

| Feature | Description |
|-----|-----|
| Supported access | rwo |
| Volume mode | Block |
| Performance | High |
| Consistency | Strong |
| Resiliency | High |
| Scalability | Multizone |
| Encryption | At rest |
{: caption="Ceph RBD storage class details." caption-side="top"}
{: #ocs_sc2}
{: tab-title="ocs-storagecluster-ceph-rbd"}
{: tab-group="sc_ref"}
{: class="simple-tab-table"}
{: summary="The first column contains a feature of the storage class. The second column contains a brief description of the feature."}

| Feature | Description |
|-----|-----|
| Supported access | rwx |
| Volume mode | s3fs (Cloud Object Storage s3fs plug-in) |
| Performance | High |
| Consistency | Eventual |
| Resiliency | High |
| Scalability | Multizone |
| Encryption | In transit and at rest |
{: caption="Ceph RGW storage class details." caption-side="top"}
{: #ocs_sc3}
{: tab-title="ocs-storagecluster-ceph-rgw"}
{: tab-group="sc_ref"}
{: class="simple-tab-table"}
{: summary="The first column contains a feature of the storage class. The second column contains a brief description of the feature."}















