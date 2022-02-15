---

copyright: 
  years: 2014, 2022
lastupdated: "2022-02-15"

keywords: openshift

subcollection: openshift

content-type: troubleshoot

---


{{site.data.keyword.attribute-definition-list}}


# Why does installing the Object storage `ibmc` Helm plug-in fail?
{: #cos_helm_fails}
{: support}

**Infrastructure provider**:
* ![Classic infrastructure provider icon.](images/icon-classic-2.svg) Classic
* ![VPC infrastructure provider icon.](images/icon-vpc-2.svg) VPC


![Version 3.11 icon.](images/icon-version-311.png) This troubleshooting topic applies only to {{site.data.keyword.openshiftshort}} clusters that run version 3.11.
{: note}




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


When the `ibmc` Helm plug-in is installed, a symlink is created from the `~/.helm/plugins/helm-ibmc` directory for Linux systems or the `~/Library/helm/plugins/helm-ibmc` directory for Mac OS to the directory where the `ibmc` Helm plug-in is located on your local system, which is usually in `./ibmcloud-object-storage-plugin/helm-ibmc`.
{: tsCauses}

When you remove the `ibmc` Helm plug-in from your local system, or you move the `ibmc` Helm plug-in directory to a different location, the symlink is not removed.

If you see a `permission denied` error, you don't have the required `read`, `write`, and `execute` permission on the `ibmc.sh` bash file so that you can execute `ibmc` Helm plug-in commands.


Review the following steps based on the error type.
{: tsResolve}

**For symlink errors**:

1. Remove the {{site.data.keyword.cos_full_notm}} Helm plug-in.
    **Linux**
    ```
    rm -rf ~/.helm/plugins/helm-ibmc
    ```
    {: pre}

    **Mac OS**
    ```
    rm -rf ~/Library/helm/plugins/helm-ibmc for macOS
    ```
    {: pre}

2. Follow the [documentation](/docs/containers?topic=containers-storage_cos_install) to re-install the `ibmc` Helm plug-in and the {{site.data.keyword.cos_full_notm}} plug-in.

**For permission errors**:

1. Change the permissions for the `ibmc` plug-in.
    **Linux**
    ```
    chmod 755 ~/.helm/plugins/helm-ibmc/ibmc.sh
    ```
    {: pre}

    **Mac OS**
    ```
    chmod 755 ~/Library/helm/plugins/helm-ibmc/ibmc.sh
    ```

2. Try out the `ibm` Helm plug-in.
    ```sh
    helm ibmc --help
    ```
    {: pre}

3. [Continue installing the {{site.data.keyword.cos_full_notm}} plug-in](/docs/containers?topic=containers-storage_cos_install).






