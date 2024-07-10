---

copyright: 
  years: 2024, 2024
lastupdated: "2024-07-10"


keywords: kubernetes, openshift, eit, 

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}



# Why do I see a `MetadataServiceNotEnabled` error for {{site.data.keyword.filestorage_vpc_short}}?
{: #ts-storage-vpc-file-eit-access}

[Virtual Private Cloud]{: tag-vpc}


Your app that uses encryption in-transit {{site.data.keyword.filestorage_vpc_short}} fails with a `MetadataServiceNotEnabled` error.
{: tsSymptoms}




You see an error message similar to the following.

```sh
Code: MetadataServiceNotEnabled, Description: Failed to mount target., BackendError: Response from mount-helper-container -> Exit Status Code: exit status 1 ,ResponseCode: 500, Action: Metadata service might not be enabled for worker node. Make sure to use IKS>=1.30 or OpenShift>=4.16 cluster.}
```
{: screen}

Encryption in-transit is not supported in clusters without public internet access. Cluster versions 4.15 and later are provisioned as Secure by Default. However, to use encryption in-transit, you must disable outbound traffic protection or add a security group rule that allows all outbound traffic.
{: tsCauses}

To resolve this, you must allow all outbound access to your cluster by using the following command.
{: tsResolve}

```sh
ibmcloud oc vpc outbound-traffic-protection disable --cluster CLUSTER [-f] [-q]
```
{: pre}




