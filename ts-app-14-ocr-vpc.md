---

copyright:
  years: 2014, 2021
lastupdated: "2021-11-10"

keywords: openshift

subcollection: openshift
content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why can't I push images to the internal registry from outside the VPC network?
{: #ts-app-ocr-vpc-push}
{: troubleshoot}

**Infrastructure provider and applicable versions**:
* ![VPC infrastructure provider icon.](images/icon-vpc-2.svg) VPC
* {{site.data.keyword.openshiftshort}} 4.4 or later


When you try to push container images to the internal {{site.data.keyword.openshiftshort}} container image registry, the push fails with a message similar to the following.
{: tsSymptoms} 

```
dial tcp 161.26.0.28:443: connect: network is unreachable
```
{: screen}


{{site.data.keyword.openshiftlong_notm}} clusters that run on the VPC infrastructure provider use {{site.data.keyword.cos_full_notm}} to store data from the cluster's internal container registry. By default, access to the {{site.data.keyword.cos_short}} endpoint is available only from inside a VPC instance. Therefore, when external process such as a local machine or CI/CD pipeline try to push container images to the internal registry from outside the VPC, the image push fails.
{: tsCauses}


Modify the custom resource of the internal image registry operator to proxy container image traffic through the internal registry pods to the direct {{site.data.keyword.cos_short}} endpoints.
{: tsResolve} 

Run the following command to patch the `configs.imageregistry.operator.openshift.io/cluster` resource to set the `disableRedirect` property to `true`. 

```sh
oc patch configs.imageregistry.operator.openshift.io/cluster --patch '{"spec":{"disableRedirect":true}}' --type=merge
```
{: pre}






