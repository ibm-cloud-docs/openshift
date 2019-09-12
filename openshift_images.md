---

copyright:
  years: 2014, 2019
lastupdated: "2019-09-12"

keywords: openshift, roks, rhoks, rhos

subcollection: openshift

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:note: .note}
{:download: .download}
{:preview: .preview}

# Building images for your apps 
{: #openshift-images}

{{site.data.keyword.openshiftlong}} clusters include an internal registry to build, deploy, and manage container images locally. For a private registry to manage and control access to images across your enterprise, you can also set up your cluster to use {{site.data.keyword.registrylong}}.
{: shortdesc}

## Using the internal registry
{: #openshift_internal_registry}

OpenShift clusters are set up by default with an internal registry. When you delete the cluster, the internal registry and its images are also deleted. If you want to persist your images, consider using a private registry such as {{site.data.keyword.registrylong_notm}}, backing up your images to persistent storage such as {{site.data.keyword.objectstorageshort}}, or creating a separate, stand-alone OpenShift container registry (OCR) cluster. For more information, see the [OpenShift docs ![External link icon](../icons/launch-glyph.svg "External link icon")](https://docs.openshift.com/container-platform/3.11/install_config/registry/index.html#install-config-registry-overview).
{: shortdesc}

### Storing images in the internal registry
{: #storage_internal_registry}

By default, your OpenShift cluster's internal registry uses an [{{site.data.keyword.cloud_notm}} File Storage](/docs/openshift?topic=openshift-file_storage) volume to store the registry images. You can review the default size of the storage volume, or update the volume size.
{: shortdesc}

To view volume details including the storage class and size, you can describe the persistent volume claim. 

```
oc describe pvc registry-backing -n default
```
{: pre}

Example output:
```
Name:          registry-backing
Namespace:     default
StorageClass:  ibmc-file-bronze
Status:        Bound
Volume:        pvc-1c6bb7e9-b3f3-11e9-a5b4-020670ab62dc
Labels:        billingType=hourly
               region=us-east
               zone=wdc04
Annotations:   ibm.io/provisioning-status=complete
               kubectl.kubernetes.io/last-applied-configuration={"apiVersion":"v1","kind":"PersistentVolumeClaim","metadata":{"annotations":{},"labels":{"billingType":"hourly"},"name":"registry-backing","namespace":...
               pv.kubernetes.io/bind-completed=yes
               pv.kubernetes.io/bound-by-controller=yes
               volume.beta.kubernetes.io/storage-provisioner=ibm.io/ibmc-file
Finalizers:    [kubernetes.io/pvc-protection]
Capacity:      20Gi
Access Modes:  RWX
Events:        <none>
```
{: screen}

If your registry needs additional gigabytes of storage for your images, you can resize the file storage volume. For more information, see [Changing the size and IOPS of your existing storage device](/docs/openshift?topic=openshift-file_storage#file_change_storage_configuration). When you resize the volume in your IBM Cloud infrastructure account, the attached PVC description is not updated. Instead, you can log in to the `docker-registry` pod that uses the `registry-backing` PVC to verify that the volume is resized.
{: note}



<br />


## Using {{site.data.keyword.registrylong_notm}}
{: #openshift_iccr}

If you want to use images that are stored in your remote private {{site.data.keyword.registrylong_notm}} `icr.io` domain names, you must create image pull secrets for each global and regional registry. Then, add the image pull secrets to each project, and to a service account for each project or to each deployment.
{: shortdesc}

For more information, see the following topics in the {{site.data.keyword.containershort_notm}} docs.
* [Understanding how to authorize your cluster to pull images from a registry](/docs/containers?topic=containers-images#cluster_registry_auth).
* [Copying the `default-<region>-icr-io` secrets](/docs/containers?topic=containers-images#copy_imagePullSecret) from the `default` namespace to the namespace that you want to pull images from.
* [Creating your own image pull secret](/docs/containers?topic=containers-images#other_registry_accounts).
* [Adding the image pull secret](/docs/containers?topic=containers-images#use_imagePullSecret) to your deployment configuration or to the namespace service account.
