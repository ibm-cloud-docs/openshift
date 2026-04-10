---

copyright: 
  years: 2014, 2026
lastupdated: "2026-04-10"


keywords: openshift, storage

subcollection: openshift

content-type: troubleshoot

---


{{site.data.keyword.attribute-definition-list}}





# Autoscaling fails after API key reset
{: #ts-storage-ca-apikey-reset}
{: support}

**Infrastructure provider**: VPC


After you reset your API key, autoscaling fails with an IAM permission error.
{: tsSymptoms}


Resetting your API key means the credentials that the cluster autoscaler add-on uses are no longer valid. After resetting your API key, you must reset the cluster autoscaler controller to use the latest API key for volume provisioning.
{: tsCauses}

After resetting your API key, you must re-create the cluster autoscaler controller pod. To re-create the controller pod, delete it by running the following commands.
{: tsResolve}

1. Get the autoscaler pod name.

    ```sh
    oc get pods -n kube-system | grep cluster-autoscaler
    ```
    {: pre}
    
1. Delete the autoscaler pod.

    ```sh
    oc delete pod -n kube-system cluster-autoscaler-pod
    ```
    {: pre}
