---

copyright:
  years: 2023, 2023
lastupdated: "2023-03-23"

keywords: delete webhooks, webhooks, mutating, validating, troubleshooting webhooks

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}




# Deleting webhooks from a cluster
{: #ts-delete-webhooks}

Some troubleshooting and debugging steps might require you to temporarily remove certain webhooks from your cluster. Follow these steps to remove webhooks, then reapply them after you have resolved your issue.
{: shortdesc}


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

1. Identify any validating webhooks that are **not** included in the following list. 
    - `alertmanagerconfigs.openshift.io`
    - `managed-storage-validation-webhooks`
    - `multus.openshift.io` 
    - `performance-addon-operator`
    - `prometheusrules.openshift.io`
    - `snapshot.storage.k8s.io`

    Any validating wehbook that **is** included in this list should **not** be deleted in the following steps. 
    {: important}

1. For each validating webhook that is **not** included in the previous list, copy the component YAML file and delete the webhook.
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

   
        