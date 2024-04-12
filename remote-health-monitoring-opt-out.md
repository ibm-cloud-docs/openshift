---

copyright: 
  years: 2022, 2024
lastupdated: "2024-04-12"


keywords: openshift, kernel, rhcos, cpu pinning, huge pages, numa, core os

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}




# Understanding remote health monitoring
{: #remote-health-monitoring-opt-out}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [{{site.data.keyword.satelliteshort}}]{: tag-satellite}

{{site.data.keyword.openshiftlong_notm}} clusters are connected to [remote health monitoring](https://docs.openshift.com/container-platform/4.13/support/remote_health_monitoring/about-remote-health-monitoring.html) by default. This means clusters report health and usage data to Red Hat unless you opt out. With connected clusters, IBM Cloud is better positioned to support customers when there are issues specific to Red Hat which impact them. Additionally, remote health reporting gives Red Hat insights into how clusters are impacted by product upgrades. If you do not want to send cluster data to Red Hat, you must opt out.
{: shortdesc}

You can choose from the following options for remote health monitoring.

- Send cluster health and usage data is reported to Red Hat. This is the default behavior. No action needed.
- Do not send cluster health and usage data to Red Hat. Action required to opt out.


## Understanding the impacts of opting out
{: #remote-health-impacts}

Review the impacts of opting out.

- Support cases might take longer until resolution if the issue requires Red Hat involvement.
- Your subscription entitlement information must be manually entered via `console.redhat.com` without the benefit of automatic usage reporting.


## Opting out of remote health reporting
{: #remote-health-opt-out}

To opt out of remote health reporting, you must complete the following steps.

- Modify the global pull secret.
- Update your cluster to use the modified pull secret.

Before proceeding with the opt out steps, ensure that you have access to the cluster as a user with the `cluster-admin` role.

1. Download the global pull secret to your local file system by running the following command from the directory of your choice.

    ```sh
    oc extract secret/pull-secret -n openshift-config --to=.
    ```
    {: pre}

2. Edit the `.dockerconfigjson` file you downloaded in the previous step to remove the `cloud.openshift.com` entry.
    ```json
    "cloud.openshift.com":{"auth":"<hash>","email":"<email_address>"}
    ```
    {: pre}

3. Save the file.

4. From the same directory where you downloaded the pull secret, replace the pull secret in your cluster with the updated `.dockerconfigjson` on your local machine. In the following command, replace `<pull_secret_location>` with the path to your update `.dockerconfigjson` file.

    ```sh
    oc set data secret/pull-secret -n openshift-config --from-file=.dockerconfigjson=<pull_secret_location>
    ```
    {: pre}



