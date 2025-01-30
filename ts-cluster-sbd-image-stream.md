---

copyright:
  years: 2024, 2025
lastupdated: "2025-01-30"


keywords: openshift

subcollection: openshift
content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}




# Why don't image streams populate on a secure by default cluster?
{: #ts_cluster_sbd_image_stream}
{: support}

You completed the steps to [allow outbound traffic to image streams](/docs/openshift?topic=openshift-sbd-allow-outbound#sbd-example-is), but image streams do not populate on a secure by default cluster.
{: tsSymptoms}

In the console, when you navigate to the **Import from GIT** page and check the **Builder Image** section, you see a `Unable to detect the Builder Image` error.


Image streams are populated from a public registry. On a secure by default cluster, public access is blocked. If you disable traffic protection after the cluster is created, the image streams are not populated. The Cluster Samples Operator configuration management state is then errantly reported as `Removed`.
{: tsCauses}


Update the Cluster Samples Operator configuration management state to fix the issue.
{: tsResolve}

1. Run the following command:
    ```sh
    oc edit configs.samples.operator.openshift.io cluster
    ```
    {: pre}

1. Change the `Removed` value to `Managed`.

1. Repeat for each instance.

1. In the console, refresh the **Import from GIT** page.
