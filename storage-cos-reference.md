---

copyright:
  years: 2014, 2024
lastupdated: "2024-01-03"


keywords: openshift

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}




# Storage class reference
{: #storage_cos_reference}

Review the storage class for {{site.data.keyword.cos_full_notm}}.
{: shortdesc}

To view more information about these classes, you can run the `get sc` command in your cluster.

```sh
oc get sc STORAGE-CLASS -o yaml
```
{: pre}

The resiliency endpoint is automatically set based on the location that your cluster is in. For more information, see [Endpoints and storage locations](/docs/cloud-object-storage?topic=cloud-object-storage-endpoints). For pricing information, see the [pricing documentation](https://cloud.ibm.com/objectstorage/create){: external}.
{: note}



| Feature | Description |
|-----|-----|
| Classes | `ibmc-s3fs-standard-cross-region`, `ibmc-s3fs-standard-perf-cross-region`, `ibmc-s3fs-standard-regional`, `ibmc-s3fs-standard-perf-regional` |
| `volumeBindingMode` | Immediate |
| `reclaimPolicy` | Delete |
| Chunk size | Storage classes without `perf`: 16 MB. Storage classes with `perf`: 52 MB |
| Kernel cache | Enabled |
| Billing type | Monthly |
{: caption="Standard classes." caption-side="bottom"}
{: #cos_sc1}
{: tab-title="Standard"}
{: tab-group="sc_ref"}
{: class="simple-tab-table"}
{: summary="The first column contains a feature of the storage class. The second column contains a brief description of the feature."}



| Feature | Description |
|-----|-----|
| Classes | `ibmc-s3fs-vault-cross-region`, `ibmc-s3fs-vault-regional` |
| Volume binding mode | Immediate |
| Reclaim policy | Delete |
| Chunk size | 16 MB |
| Kernel cache |  Disabled |
| Billing type | Monthly |
{: caption="Vault classes." caption-side="bottom"}
{: #cos_sc2}
{: tab-title="Valut"}
{: tab-group="sc_ref"}
{: class="simple-tab-table"}
{: summary="The first column contains a feature of the storage class. The second column contains a brief description of the feature."}


| Feature | Description |
|-----|-----|
| Classes | `ibmc-s3fs-cold-cross-region`, `ibmc-s3fs-cold-perf-cross-region`, `ibmc-s3fs-cold-regional`,  `ibmc-s3fs-cold-perf-regional` |
| `volumeBindingMode` | Immediate |
| `reclaimPolicy` | Delete |
| Chunk size | 16 MB |
| Kernel cache | Disabled |
| Billing type | Monthly |
{: caption="Cold classes." caption-side="bottom"}
{: #cos_sc3}
{: tab-title="Cold"}
{: tab-group="sc_ref"}
{: class="simple-tab-table"}
{: summary="The first column contains a feature of the storage class. The second column contains a brief description of the feature."}


| Feature | Description |
|-----|-----|
| Classes | `ibmc-s3fs-smart-cross-region`, `ibmc-s3fs-smart-perf-cross-region`, `ibmc-s3fs-smart-regional`, `ibmc-s3fs-smart-perf-regional` |
| `volumeBindingMode` | Immediate |
| `reclaimPolicy` | Delete |
| Chunk size | Storage classes without `perf`: 16 MB. Storage classes with `perf`: 52 MB |
| Kernel cache | Disabled |
| Billing type | Monthly |
{: caption="Smart classes." caption-side="bottom"}
{: #cos_sc4}
{: tab-title="Smart"}
{: tab-group="sc_ref"}
{: class="simple-tab-table"}
{: summary="The first column contains a feature of the storage class. The second column contains a brief description of the feature."}






