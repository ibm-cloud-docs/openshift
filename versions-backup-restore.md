---

copyright: 
  years: 2014, 2022
lastupdated: "2022-02-21"

keywords: back up, restore, changelog, openshift

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}


# Back up and restore Helm chart 
{: #backup_restore_changelog}

View information for updates to the back up and restore Helm chart in your {{site.data.keyword.openshiftlong}} clusters.
{: shortdesc}

Refer to the following tables for a summary of changes for each version of the [back up and restore Helm chart](/docs/openshift?topic=openshift-utilities#ibmcloud-backup-restore).

| `ibmcloud-backup-restore` Helm chart version | Supported? | Cluster version support |
| -------------------- | -----------|--------------------------- |
| 2.0.5 | Yes | 4.3 - 4.6 |
{: caption="Back up and restore Helm chart versions" caption-side="top"}
{: summary="The rows are read from left to right. The first column is the back up and restore Helm chart version. The second column is the version's supported state. The third column is the cluster version of your cluster that the back up and restore Helm chart version is supported for."}


## Changelog for 1.0.5, released 17 December 2020
{: #0105_br_chart}

The following table shows the changes that are in version `1.0.5` of the `ibmcloud-backup-restore` Helm chart.
{: shortdesc}


- Image tags: `v100`  
- Supported cluster versions: 4.3 - 4.6  
- Images are now signed.  
- The `ibmcloud-backup-restore` Helm chart now pulls the universal base image (UBI) from the proxy image registry.  
- Resources that are deployed by the `ibmcloud-backup-restore` Helm chart are now linked with the corresponding source code and build URLs.  







