---

copyright:
  years: 2014, 2021
lastupdated: "2021-09-10"

keywords: openshift, roks, rhoks, rhos

subcollection: openshift
content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}  

# Why does the cluster autoscaler add-on fail with the pod stuck in `Init` state?
{: #ca_ts_secret}

When you deploy the cluster autoscaler add-on, the `ibm-iks-cluster-autoscaler` pods are stuck in the `Init` state. When you run the `oc get pods | grep auto` command, you see output similar to the following:
{: tsSymptoms}

```
ibm-iks-cluster-autoscaler1-5656d89447-rrbgm     0/1     Init:0/1   0          5m2s
```
{: screen}


The cluster autoscaler add-on could not validate the secret that you configured. The Kubernetes secret that you used to deploy the cluster autoscaler add-on does not have the required permissions.
{: tsCauses}


To verify that the issue is a secret validation issue, get the logs from the `secret-validator` container in the `ibm-iks-cluster-autoscaler` pod.
{: tsResolve}

1. Get the name of the autoscaler pod in your cluster.
    ```sh
    oc get pods -A | grep auto
    ```
    {: pre}

    **Example output**
    ```sh
    kube-system                                             ibm-iks-cluster-autoscaler-6d7bc9b9df-9hgg2                       1/1     Running       0          34m
    ```
    {: screen}

2. Get the logs from the `secret-validator` container. If your secrets are invalid, the output message includes `Invalid secrets`.
    ```sh
    oc logs <autoscaler_pod_name> -c secret-validator -n kube-system
    ```
    {: pre}

    **Example output**
    ```sh
    ...
    "msg":"Invalid secrets"}
    ...
    {: screen}

3. After you verified that the issue is related to invalid secrets, verify that you have the `storage-secret-store` secret in your cluster.
    ```sh
    oc get secrets -A | grep storage-secret-store
    ```
    {: pre}

4. Update your `storage-secret-store` secret with the required IAM permissions by [resetting your credentials](/docs/containers?topic=containers-missing_permissions).


