---

copyright: 
  years: 2014, 2025
lastupdated: "2025-10-29"


keywords: openshift, oc, installing oc, openshift cli, installing oc cli


subcollection: openshift

 


---


{{site.data.keyword.attribute-definition-list}}

# Installing the CLI
{: #cli-install}


You can use the following tools to manage your {{site.data.keyword.openshiftlong_notm}} clusters. While you can install a subset of the tools, all the following tools are recommended.
{: shortdesc}


[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [{{site.data.keyword.satelliteshort}}]{: tag-satellite}


## Understanding the CLI tools
{: #cli-understand}

| CLI | Description |
| --- | --- |
| `ibmcloud` | You can use the `ibmcloud` CLI to login to your account, add users, manage your catalogs and more. |
| `ks` plug-in | After installing the `ibmcloud` CLI, you can use the `ks` plug-in to create and manage {{site.data.keyword.openshiftlong_notm}} clusters as well as {{site.data.keyword.satelliteshort}} hosts and Locations. |
| `oc` | You can use the `oc` CLI to manage resources within your clusters like pods, deployments, and more. |
{: caption="Table 1: CLI tools" caption-side="bottom"}


{{../cli/index.md#step1-install-idt}}

{{../cli/index.md#step2-verify-idt}}

{{../cli/index.md#step3-install-idt-manually}}

To install the `container-service` or `ks` plug-in, run the following command.

```sh
ibmcloud plugin install ks
```
{: pre}


## Install the {{site.data.keyword.redhat_openshift_notm}} CLI
{: #install-kubectl-cli}
{: step}

You can use the `oc` CLI to deploy and manage resources in your {{site.data.keyword.openshiftlong_notm}} cluster.




- If you already have a Red Hat account, install the OpenShift CLI. For more information, see the [Getting started with the OpenShift CLI](https://docs.openshift.com/container-platform/4.19/cli_reference/openshift_cli/getting-started-cli.html){: external}.

- If you don't have a Red Hat account, you can download the OpenShift CLI from the [console](https://cloud.ibm.com/containers/cluster-management/clusters){: external} after you create an OpenShift cluster.

- For more information about the OpenShift CLI, see the following links.
    - [OpenShift CLI administrator command reference](https://docs.redhat.com/en/documentation/openshift_container_platform/4.19/html/cli_tools/openshift-cli-oc#cli-administrator-commands){: external}.
    - [OpenShift CLI developer command reference](https://docs.redhat.com/en/documentation/openshift_container_platform/4.19/html/cli_tools/openshift-cli-oc#cli-developer-commands){: external}.

Red Hat OpenShift on IBM Cloud version 4.16 is now based on the RHEL 9.2 host operating system, which increases the [micro-architecture requirements](https://docs.openshift.com/container-platform/4.16/updating/preparing_for_updates/updating-cluster-prepare.html#rhel-micro-architecture-update-requirements){: external} to x86-64-v2. As a result, host machines for IBM Cloud {{site.data.keyword.satelliteshort}} must support x86-64-v2 architecture for any location that contains a version 4.16 cluster. See [Host system requirements](/docs/satellite?topic=satellite-host-reqs) for more information. In addition, client machines used to run `oc` client version 4.16 must also support x86-64-v2 architecture. Client machines that do not meet this micro-architecture requirement must use a RHEL 8 based `oc` version 4.16 client. Refer to the list of [available `oc` version 4.16 clients](https://mirror.openshift.com/pub/openshift-v4/clients/ocp/stable-4.16/){: external}.
{: important}
