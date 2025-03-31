---

copyright:
  years: 2021, 2025
lastupdated: "2025-03-28"


keywords: openshift, storage

subcollection: openshift
content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}






# What if my OpenShift Data Foundation issue is still unresolved?
{: #ocs-error-unresolved}
{: support}

If your ODF issue is still unresolved or is not addressed in the troubleshooting steps, contact ODF support by raising a case in the {{site.data.keyword.redhat_notm}} customer portal.

1. [Access the Red Hat Customer Portal](https://access.redhat.com){: external} and sign in with your support credentials. 

2. Find the **Troubleshoot a product issue** section and select **Red Hat OpenShift Data Foundation**.

3. Select the version of your ODF instance.

4. Click **Continue**.

5. Use the {{site.data.keyword.redhat_notm}} `must-gather` tool to collect data about your cluster in a compressed file. For more information, see [Gathering data about your cluster](https://docs.redhat.com/documentation/openshift_container_platform/4.6/html/support/gathering-cluster-data#gathering-data-specific-features_gathering-cluster-data){: external}.
    ```sh
    oc adm must-gather --image=registry.redhat.io/ocs4/ocs-must-gather-rhel8:latest --dest-dir=ocs_mustgather
    ```
    {: pre}

6. Follow the prompts to describe the issue you have. Attach the file with the `must-gather` data you collected earlier.

7. Click **Open a case** to submit your issue. 
