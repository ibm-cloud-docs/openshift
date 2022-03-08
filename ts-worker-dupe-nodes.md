---

copyright: 
  years: 2014, 2022
lastupdated: "2022-03-08"

keywords: openshift

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}


# After a worker node updates or reloads, why do duplicate nodes and pods appear?
{: #cs_duplicate_nodes}
{: support}


**Infrastructure provider**:
* ![Classic infrastructure provider icon.](images/icon-classic-2.svg) Classic
* ![VPC infrastructure provider icon.](images/icon-vpc-2.svg) VPC


When you run `oc get nodes`, you see duplicate worker nodes with the status **`NotReady`**. The worker nodes with **`NotReady`** have public IP addresses, while the worker nodes with **`Ready`** have private IP addresses.
{: tsSymptoms}


Older clusters listed worker nodes by the cluster's public IP address. Now, worker nodes are listed by the cluster's private IP address. When you reload or update a node, the IP address is changed, but the reference to the public IP address remains.
{: tsCauses}


Service is not disrupted due to these duplicates, but you can remove the old worker node references from the API server.
{: tsResolve}

```sh
oc delete node <node_name1> <node_name2>
```
{: pre}






