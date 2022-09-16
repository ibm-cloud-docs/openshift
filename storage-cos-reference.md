---

copyright:
  years: 2014, 2022
lastupdated: "2022-09-16"

keywords: openshift

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}


# Storage class reference
{: #storage_cos_reference}

## Standard
{: #standard}


Name
:   `ibmc-s3fs-standard-cross-region`
:   `ibmc-s3fs-standard-perf-cross-region`
:   `ibmc-s3fs-standard-regional`
:   `ibmc-s3fs-standard-perf-regional`


Default resiliency endpoint
:   The resiliency endpoint is automatically set based on the location that your cluster is in. For more information, see [Regions and endpoints](/docs/cloud-object-storage/basics?topic=cloud-object-storage-endpoints#endpoints).

Chunk size
:   Storage classes without `perf`: 16 MB. Storage classes with `perf`: 52 MB


Kernel cache
:   Enabled

Billing
:   Monthly

Pricing
:   Review the [pricing documentation](https://cloud.ibm.com/objectstorage/create#pricing){: external}.


## Vault
{: #Vault}



Name
:   `ibmc-s3fs-vault-cross-region`
:   `ibmc-s3fs-vault-regional`

Default resiliency endpoint
:   The resiliency endpoint is automatically set based on the location that your cluster is in. For more information, see [Regions and endpoints](/docs/cloud-object-storage/basics?topic=cloud-object-storage-endpoints#endpoints).

Chunk size
:   16 MB

Kernel cache
:   Disabled

Billing
:   Monthly

Pricing
:   Review the [pricing documentation](https://cloud.ibm.com/objectstorage/create#pricing){: external}.

## Cold
{: #cold}


Name
:   `ibmc-s3fs-cold-cross-region`
:   `ibmc-s3fs-cold-perf-cross-region`
:   `ibmc-s3fs-cold-regional`
:   `ibmc-s3fs-cold-perf-regional`

Default resiliency endpoint
:   The resiliency endpoint is automatically set based on the location that your cluster is in. For more information, see [Regions and endpoints](/docs/cloud-object-storage/basics?topic=cloud-object-storage-endpoints#endpoints).

Chunk size
:   16 MB

Kernel cache
:   Disabled

Billing
:   Monthly

Pricing
:   Review the [pricing documentation](https://cloud.ibm.com/objectstorage/create#pricing){: external}.

## Flex
{: #flex}


Name
:   `ibmc-s3fs-flex-cross-region`
:   `ibmc-s3fs-flex-perf-cross-region`
:   `ibmc-s3fs-flex-regional`
:   `ibmc-s3fs-flex-perf-regional`

Default resiliency endpoint
:   The resiliency endpoint is automatically set based on the location that your cluster is in. For more information, see [Regions and endpoints](/docs/cloud-object-storage/basics?topic=cloud-object-storage-endpoints#endpoints).

Chunk size
:   Storage classes without `perf`: 16 MB
:   Storage classes with `perf`: 52 MB.

Kernel cache
:   Disabled

Billing
:   Monthly

Pricing
:  Review the [pricing documentation](https://cloud.ibm.com/objectstorage/create#pricing){: external}.


