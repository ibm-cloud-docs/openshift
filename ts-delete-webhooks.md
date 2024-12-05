---

copyright:
  years: 2023, 2024
lastupdated: "2024-12-04"


keywords: delete webhooks, webhooks, mutating, validating, troubleshooting webhooks

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}




# Deleting webhooks from a cluster
{: #ts-delete-webhooks}

Some troubleshooting and debugging steps might require you to temporarily remove certain webhooks from your cluster. Follow these steps to remove webhooks, then reapply them after you have resolved your issue.
{: shortdesc}

## Checking webhooks that are rejecting requests
{: #webhook-reject}

1. Before you delete webhooks, run the following command to get a list of webhooks that are rejecting requests.

    ```sh
    kubectl get --raw /metrics | grep apiserver_admission_webhook_admission_duration_seconds
    ```
    {: pre}

1. Review the output for webhooks that have `rejected="true"` status.

1. Continue troubleshooting the webhooks that are rejecting requests.


## Deleting webhooks
{: #webhook-delete}

1. List the mutating webhooks in your cluster.

    ```sh
    oc get mutatingwebhookconfigurations
    ```
    {: pre}

1. For each mutating webhook, copy the component YAML file and delete the webhook.

    1. Run the command to copy the YAML file. Save the YAML file so you can reapply it later.

        ```sh
        oc get mutatingwebhookconfigurations <WEBHOOK-NAME> -o yaml > <WEBHOOK-NAME>.yml
        ```
        {: pre}

    1. Delete the mutating webhook. 

        ```sh
        oc delete mutatingwebhookconfigurations <WEBHOOK-NAME>
        ```
        {: pre}

1. List the validating webhooks in your cluster.

    ```sh
    oc get validatingwebhookconfigurations
    ```
    {: pre}

1. Identify any validating webhooks that aren't included in the following list.
    - `alertmanagerconfigs.openshift.io`
    - `managed-storage-validation-webhooks`
    - `multus.openshift.io` 
    - `performance-addon-operator`
    - `prometheusrules.openshift.io`
    - `snapshot.storage.k8s.io`

    Any validating webhook that's included in this list shouldn't be deleted in the following steps. 
    {: important}

1. For each validating webhook that isn't included in the previous list, copy the component YAML file and delete the webhook.
    1. Run the command to copy the YAML file. Save the YAML file so you can reapply it later.

        ```sh
        oc get validatingwebhookconfigurations <WEBHOOK-NAME> -o yaml > <WEBHOOK-NAME>.yml
        ```
        {: pre}

    1. Delete the validating webhook. 

        ```sh
        oc delete validatingwebhookconfigurations <WEBHOOK-NAME>
        ```
        {: pre}

1. When you are done troubleshooting your worker node issue, reapply the webhook YAML files.

    ```sh
    oc apply -f <webhook-yaml-file>
    ```
    {: pre}

   
        
