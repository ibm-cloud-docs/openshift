---

copyright: 
  years: 2014, 2023
lastupdated: "2023-06-26"

keywords: openshift, oc, installing oc, openshift cli, installing oc cli


subcollection: openshift

 


---


{{site.data.keyword.attribute-definition-list}}

# Installing the CLI
{: #cli-install}


You can use the following tools to manage your {{site.data.keyword.openshiftlong_notm}} clusters. In most cases, installing all the following tools is recommended.
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

To install the `container-service` or `ks` plugin, run the following command.

```sh
ibmcloud plugin install ks
```
{: pre}


## Install the {{site.data.keyword.redhat_openshift_notm}} CLI
{: #install-kubectl-cli}
{: step}

You can use the `oc` CLI to deploy and manage resources in your {{site.data.keyword.openshiftlong_notm}} cluster.




To install the CLI, see the [Getting started with the OpenShift CLI](https://docs.openshift.com/container-platform/4.11/cli_reference/openshift_cli/getting-started-cli.html){: external}.

- For a list of commands that are available to cluster administrators, see the [OpenShift CLI administrator command reference](https://docs.openshift.com/container-platform/4.11/cli_reference/openshift_cli/administrator-cli-commands.html){: external}.

- For a list of commands that are available to cluster developers, see the [OpenShift CLI developer command reference](https://docs.openshift.com/container-platform/4.11/cli_reference/openshift_cli/developer-cli-commands.html){: external}.






