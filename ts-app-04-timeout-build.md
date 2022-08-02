---

copyright:
  years: 2014, 2022
lastupdated: "2022-08-02"

keywords: openshift

subcollection: openshift
content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}


# Why does pushing to the internal registry time out?
{: #ts-app-timeout}
{: troubleshoot}
{: support}

**Infrastructure provider**:
* Classic
* VPC


You try to push an image to the [internal registry](/docs/openshift?topic=openshift-registry#openshift_internal_registry), but sporadically you see an error message similar to the following.
{: tsSymptoms}

```sh
received unexpected HTTP status: 504 Gateway Time-out
```
{: screen}

The default file storage device that provides the storage for the internal registry's images is initially set up with 2 IOPS and 20 GB of storage. When you push larger images, the device might time out because its IOPS is too low to support the image.
{: tsCauses}


[Change the size and IOPS of the existing file storage device](/docs/openshift?topic=openshift-file_storage#file_change_storage_configuration).
{: tsResolve}

When you resize the volume in your IBM Cloud infrastructure account, the attached PVC description is not updated. Instead, you can log in to the `openshift-image-registry` ({{site.data.keyword.redhat_openshift_notm}} 4) or `docker-registry` ({{site.data.keyword.redhat_openshift_notm}} 3.11) pod that uses the `registry-backing` PVC to verify that the volume is resized.
{: note}






