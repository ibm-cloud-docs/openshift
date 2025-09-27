---

copyright:
  years: 2024, 2025
lastupdated: "2025-09-27"


keywords: openshift, troubleshooting, upgrade, update, update status

subcollection: openshift
content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}


# Viewing cluster upgrade status
{: #upgrade-status}
{: support}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf}

For clusters that run version 4.16 or later, you can use the `oc adm upgrade status` command to check the update status of your cluster master during a master version update. This command provides details regarding the update status so you can determine if the update is proceeding normally or if intervention is required. If intervention is required, the command provides details of the issue as well as links to relevant documentation to help resolve the issue. For more information, see the {{site.data.keyword.redhat_openshift_notm}} documentation
{: shortdesc}

The `oc adm upgrade status` command is available as a technology preview from {{site.data.keyword.redhat_openshift_notm}}.
{: note}

## Getting cluster update details
{: #oc-adm-use}

1. Run the following command to set the `OC_ENABLE_CMD_UPGRADE_STATUS` environment variable to true.

    ```sh
    export OC_ENABLE_CMD_UPGRADE_STATUS=true
    ```
    {: pre}

2. Run the upgrade status command.

    ```sh
    oc adm upgrade status
    ```
    {: pre}

3. Review the output. If the output indicates any issues with the update, read the details and follow the provided links to relevant documentation to help resolve the issue. 

    Example output for a master update in progress.

    ```sh
    An update is in progress for 1m39s: Working towards 4.16.7: 473 of 673 done (70% complete), waiting on console, csi-snapshot-controller, image-registry, ingress, insights, kube-storage-version-migrator, marketplace, monitoring, node-tuning, openshift-samples, operator-lifecycle-manager, service-ca, storage

    = Control Plane =
    Assessment:      Progressing
    Completion:      0%
    Duration:        1m38.761469s
    Operator Status: 17 Total, 17 Available, 0 Progressing, 0 Degraded
    ```
    {: screen}


    Example output if no update is in progress. 

    ```sh
    The cluster version is not updating (Progressing=False).

    Reason: <none>
    Message: Cluster version is 4.16.7
    ```
    {: screen}
