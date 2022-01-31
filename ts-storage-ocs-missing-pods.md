---

copyright:
  years: 2021, 2022
lastupdated: "2022-01-31"

keywords: openshift, storage

subcollection: openshift
content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}



# Why are no pods listed in the `openshift-storage` namespace?
{: #ts-ocs-no-pods}
{: support}


There are no pods listed when you run the `oc get pods -n openshift-storage` command. When you view the `ibm-ocs-operator-controller-manager` logs with the `oc logs <ibm-ocs-operator-controller-manager-a1a1a1a> -n kube-system` command, you see the following error message:
{: tsSymptoms}

```
Failed to get StorageCluster","error":"no matches for kind \"StorageCluster\" in version \"ocs.openshift.io/v1\
```
{: screen}


The catalog source for your ODF storage cluster is unhealthy.
{: tsCauses}

Remove all the catalog sources from your cluster.
{: tsResolve}

1. Remove all catalog sources from your cluster. A new catalog source and respective pods automatically generate.
    ```sh
    oc -n openshift-marketplace delete catsrc --all
    ```
    {: pre}

2. Wait a few minutes and verify that the pods regenerate. If the pods regenerate, the ODF installation proceeds. If the pods don't regenerate, [contact ODF support by raising a case in the {{site.data.keyword.redhat_notm}} customer portal](/docs/openshift?topic=openshift-ocs-error-unresolved).
    ```sh
    oc get pods,catsrc -n openshift-marketplace
    ```
    {: pre}







