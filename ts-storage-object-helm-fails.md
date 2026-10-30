---

copyright:
  years: 2014, 2026
lastupdated: "2026-10-30"


keywords: openshift, ibmc, helm

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}





# Why does installing the Object storage Helm plug-in fail?
{: #cos_helm_fails}
{: support}

Troubleshoot Helm installation failures for Cloud Object Storage.
{: shortdesc}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf}


When you install the {{site.data.keyword.cos_full_notm}} `ibmc` Helm plug-in, the installation fails with one of the following errors:
{: tsSymptoms}

```sh
Error: symlink /Users/iks-charts/ibm-object-storage-plugin/helm-ibmc /Users/ibm/.helm/plugins/helm-ibmc: file exists
```
{: screen}

```sh
Error: fork/exec /home/iksadmin/.helm/plugins/helm-ibmc/ibmc.sh: permission denied
```
{: screen}

When you run any `helm ibmc` command, such as `helm ibmc --update`, `helm ibmc install`, or `helm ibmc upgrade`, the command fails with the following error:

```sh
CURRENT HELM CLIENT VERSION IS "Client: v2.17.0+ga690bad".
ERROR: Helm v2 is not supported by ibmc v2.0.14 and later. Please upgrade to Helm v3 or higher. See https://helm.sh/docs/intro/install/ for installation instructions.
Error: plugin "ibmc" exited with error
```
{: screen}


When the `ibmc` Helm plug-in is installed, a symlink is created from the `~/.local/share/helm/plugins/helm-ibmc` directory for Linux systems or the `~/Library/helm/plugins/helm-ibmc` directory for Mac OS to the directory where the `ibmc` Helm plug-in is located on your local system, which is usually in `./ibmcloud-object-storage-plugin/helm-ibmc`.
{: tsCauses}

When you remove the `ibmc` Helm plug-in from your local system, or you move the `ibmc` Helm plug-in directory to a different location, the symlink is not removed.

If you see a `permission denied` error, you don't have the required `read`, `write`, and `execute` permission on the `ibmc.sh` bash file so that you can execute `ibmc` Helm plug-in commands.

If you see the `Helm v2 is not supported` error, your local Helm client is version 2. The `ibmc` Helm plug-in version 2.0.14 and later supports only Helm version 3 and later, and checks the Helm client version before every command. If you update the `ibmc` plug-in to version 2.0.14 or later while your Helm client is still version 2, the error occurs the next time that you run a `helm ibmc` command.


Review the following steps based on the error type.
{: tsResolve}

- For symlink errors:

    1. Remove the {{site.data.keyword.cos_full_notm}} Helm plug-in.

        Linux example
        ```sh
        rm -rf ~/.local/share/helm/plugins/helm-ibmc
        ```
        {: pre}

        Mac OS example
        ```sh
        rm -rf ~/Library/helm/plugins/helm-ibmc
        ```
        {: pre}

    2. Follow the [documentation](/docs/openshift?topic=openshift-storage_cos_install) to re-install the `ibmc` Helm plug-in and the {{site.data.keyword.cos_full_notm}} plug-in.

- For permission errors:

    1. Change the permissions for the `ibmc` plug-in.
        Linux example
        ```sh
        chmod 755 ~/.local/share/helm/plugins/helm-ibmc/ibmc.sh
        ```
        {: pre}

        Mac OS example
        ```sh
        chmod 755 ~/Library/helm/plugins/helm-ibmc/ibmc.sh
        ```
        {: pre}

    2. Try out the `ibm` Helm plug-in.
    
        ```sh
        helm ibmc --help
        ```
        {: pre}

- For `Helm v2 is not supported` errors:

    1. Check your Helm client version.

        ```sh
        helm version --template '{{.Version}}'
        ```
        {: pre}

    2. If the output starts with `v2`, or if the command fails with an error such as `Error: could not find tiller`, you are using Helm version 2. [Upgrade your Helm client to version 3 or later](/docs/openshift?topic=openshift-helm#install_v3). If you have existing Helm version 2 releases, see the [Helm v2 to v3 migration guide](https://helm.sh/docs/topics/v2_v3_migration/){: external}.

    3. Verify that the `ibmc` plug-in is at version 2.0.14 or later.

        ```sh
        helm plugin list
        ```
        {: pre}

    4. Try out the `ibmc` Helm plug-in.

        ```sh
        helm ibmc --help
        ```
        {: pre}

3. [Continue installing the {{site.data.keyword.cos_full_notm}} plug-in](/docs/openshift?topic=openshift-storage_cos_install).
