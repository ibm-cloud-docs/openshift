---

copyright:
  years: 2024, 2024
lastupdated: "2024-09-05"


keywords: openshift, troubleshooting, upgrade, oc adm, update, update status

subcollection: openshift
content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}


# Viewing cluster upgrade status with the `oc adm upgrade status` command
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

    Example output for a normal update status.

    ```sh
    = Control Plane =
    Assessment:      Progressing
    Target Version:  4.14.1 (from 4.14.0)
    Completion:      97%
    Duration:        54m
    Operator Status: 32 Healthy, 1 Unavailable

    Control Plane Nodes
    NAME                                        ASSESSMENT    PHASE      VERSION   EST    MESSAGE
    ip-10-0-53-40.us-east-2.compute.internal    Progressing   Draining   4.14.0    +10m
    ip-10-0-30-217.us-east-2.compute.internal   Outdated      Pending    4.14.0    ?
    ip-10-0-92-180.us-east-2.compute.internal   Outdated      Pending    4.14.0    ?

    = Worker Upgrade =

    = Worker Pool =
    Worker Pool:     worker
    Assessment:      Progressing
    Completion:      0%
    Worker Status:   3 Total, 2 Available, 1 Progressing, 3 Outdated, 1 Draining, 0 Excluded, 0 Degraded

    Worker Pool Nodes
    NAME                                        ASSESSMENT    PHASE      VERSION   EST    MESSAGE
    ip-10-0-4-159.us-east-2.compute.internal    Progressing   Draining   4.14.0    +10m
    ip-10-0-20-162.us-east-2.compute.internal   Outdated      Pending    4.14.0    ?
    ip-10-0-99-40.us-east-2.compute.internal    Outdated      Pending    4.14.0    ?

    = Worker Pool =
    Worker Pool:     infra
    Assessment:      Progressing
    Completion:      0%
    Worker Status:   1 Total, 0 Available, 1 Progressing, 1 Outdated, 1 Draining, 0 Excluded, 0 Degraded

    Worker Pool Node
    NAME                                             ASSESSMENT    PHASE      VERSION   EST    MESSAGE
    ip-10-0-4-159-infra.us-east-2.compute.internal   Progressing   Draining   4.14.0    +10m

    = Update Health =
    SINCE   LEVEL   IMPACT   MESSAGE
    14m4s   Info    None     Update is proceeding well
    ```
    {: screen}








