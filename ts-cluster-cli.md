---

copyright: 
  years: 2014, 2021
lastupdated: "2021-10-15"

keywords: openshift, roks, rhoks, rhos

subcollection: openshift
content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}


# Debugging common CLI issues with clusters
{: #ts_clis}
{: troubleshoot}
{: support}

Review the following common reasons for CLI connection issues or command failures.
{: shortdesc}

**Infrastructure provider**:
* ![Classic infrastructure provider icon.](images/icon-classic-2.svg) Classic
* ![VPC infrastructure provider icon.](images/icon-vpc-2.svg) VPC

## Firewall prevents running CLI commands
{: #ts_firewall_clis}


When you run `ibmcloud`, `kubectl`,`oc`,  or `calicoctl` commands from the CLI, they fail.
{: tsSymptoms}


You might have corporate network policies that prevent access from your local system to public endpoints via proxies or firewalls.
{: tsCauses}


[Allow TCP access for the CLI commands to work](/docs/openshift?topic=openshift-firewall#firewall_bx).
{: tsResolve}

This task requires the [**Administrator** {{site.data.keyword.cloud_notm}} IAM platform access role](/docs/openshift?topic=openshift-users#checking-perms) for the cluster.



## `kubectl` or `oc` commands do not work
{: #kubectl_fails}


When you run `kubectl` or `oc` commands against your cluster, your commands fail with an error message similar to the following.
{: tsSymptoms}

```
No resources found.
Error from server (NotAcceptable): unknown (get nodes)
```
{: screen}

```sh
invalid object doesn't have additional properties
```
{: screen}

```
error: No Auth Provider found for name "oidc"
```
{: screen}


You have a different version of `kubectl` than your cluster version.
{: tsCauses}

[Kubernetes does not support](https://kubernetes.io/releases/version-skew-policy/){: external} `kubectl` client versions that are 2 or more versions apart from the server version (n +/- 2). If you use a community Kubernetes cluster, you might also have the {{site.data.keyword.openshiftshort}} version of `kubectl`, which does not work with community Kubernetes clusters.

To check your client `kubectl` version against the cluster server version, run `oc version --short`.


[Install the version of `kubectl`](/docs/openshift?topic=openshift-openshift-cli#cli_oc) that matches the Kubernetes version of your cluster.
{: tsResolve}

If you have multiple clusters at different Kubernetes versions or different container platforms such as {{site.data.keyword.openshiftshort}}, download each `kubectl` version binary file to a separate directory. Then, you can set up an alias in your local command-line interface (CLI) profile to point to the `kubectl` binary file directory that matches the `kubectl` version of the cluster that you want to work with, or you might be able to use a tool such as `brew switch kubernetes-cli <major.minor>`.





## Time out when trying to connect to a pod
{: #roks_timeout}


You try to connect to a pod, such as logging in with `oc exec` or getting logs with `oc logs`. The pod is healthy, but you see an error message similar to the following.
{: tsSymptoms}

```
Error from server: Get https://<10.xxx.xx.xxx>:<port>/<address>: dial tcp <10.xxx.xx.xxx>:<port>: connect: connection timed out
```
{: screen}


The OpenVPN server is experiencing configuration issues that prevent accessing the pod from its internal address.
{: tsCauses}


Before you begin: [Access your {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-access_cluster).
{: tsResolve}

1. Check if a cluster and worker node updates are available by viewing your cluster and worker node details in the console or a `cluster ls` or `worker ls` command. If so, [update your cluster and worker nodes to the latest version](/docs/openshift?topic=openshift-update).
2. Restart the OpenVPN pod by deleting it. Another VPN pod is scheduled. When its **STATUS** is **Running**, try to connect the pod that you previously could not connect to.
    ```sh
    oc delete pod -n kube-system -l app=vpn
    ```
    {: pre}

## Missing projects or `oc` and `kubectl` commands fail
{: #rhoks_ts_admin_config}
{: troubleshoot}
{: support}

**Infrastructure provider**:
* ![Classic infrastructure provider icon.](images/icon-classic-2.svg) Classic
* ![VPC infrastructure provider icon.](images/icon-vpc-2.svg) VPC Generation 2 compute


You do not see all the projects that you have access to. When you try to run `oc` or `kubectl` commands, you see an error similar to the following.
{: tsSymptoms}

```
No resources found.
Error from server (Forbidden): <resource> is forbidden: User "IAM#user@email.com" cannot list <resources> at the cluster scope: no RBAC policy matched
```
{: screen}

You need to download the `admin` configuration files for your cluster in order to run commands that require the `cluster-admin` cluster role.
{: tsCauses}


Run `ibmcloud oc cluster config --cluster <cluster_name_or_ID> --admin` and try again.
{: tsResolve}






