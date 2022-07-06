---

copyright: 
  years: 2014, 2022
lastupdated: "2022-07-06"

keywords: openshift, storage

subcollection: openshift

content-type: troubleshoot

---


{{site.data.keyword.attribute-definition-list}}



# Autoscaling fails after API key reset
{: #ts-storage-ca-apikey-reset}
{: support}

**Infrastructure provider**:
![VPC](../icons/vpc.svg "VPC") VPC


After you reset your API key, autoscaling fails with an IAM permission error.
{: tsSymptoms}


Resetting your API key means the credentials the cluster autoscaler add-on uses is no longer valid. After resetting your API key, you must reset the cluster autoscaler controller to use the latest API key for volume provisioning.
{: tsCauses}


After resetting your API key, you must re-create the cluster autoscaler controller pod. To re-create the controller pod, delete it by running the following command:
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







