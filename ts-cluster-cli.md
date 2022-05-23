---

copyright: 
  years: 2014, 2022
lastupdated: "2022-05-23"

keywords: openshift

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
* ![Classic](../icons/classic.svg "Classic") Classic
* ![VPC](../icons/vpc.svg "VPC") VPC

## Firewall prevents running CLI commands
{: #ts_firewall_clis}


When you run `ibmcloud`, `kubectl`,`oc`,  or `calicoctl` commands from the CLI, they fail.
{: tsSymptoms}


You might have corporate network policies that prevent access from your local system to public endpoints via proxies or firewalls.
{: tsCauses}


[Allow TCP access for the CLI commands to work](/docs/openshift?topic=openshift-firewall#firewall_bx).
{: tsResolve}

This task requires the [**Administrator** {{site.data.keyword.cloud_notm}} IAM platform access role](/docs/openshift?topic=openshift-users#checking-perms) for the cluster.



## `kubectl` or `oc` commands don't work
{: #kubectl_fails}


When you run `kubectl` or `oc` commands against your cluster, your commands fail with an error message similar to the following.
{: tsSymptoms}

```sh
No resources found.
Error from server (NotAcceptable): unknown (get nodes)
```
{: screen}

```sh
invalid object doesn't have additional properties
```
{: screen}

```sh
error: No Auth Provider found for name "oidc"
```
{: screen}


You have a different version of `kubectl` than your cluster version.
{: tsCauses}

[Kubernetes does not support](https://kubernetes.io/releases/version-skew-policy/){: external} `kubectl` client versions that are 2 or more versions apart from the server version (n +/- 2). If you use a community Kubernetes cluster, you might also have the {{site.data.keyword.redhat_openshift_notm}} version of `kubectl`, which does not work with community Kubernetes clusters.

To check your client `kubectl` version against the cluster server version, run `oc version --short`.


[Install the version of `kubectl`](/docs/openshift?topic=openshift-openshift-cli#cli_oc) that matches the Kubernetes version of your cluster.
{: tsResolve}

If you have multiple clusters at different Kubernetes versions or different container platforms such as {{site.data.keyword.redhat_openshift_notm}}, download each `kubectl` version binary file to a separate directory. Then, you can set up an alias in your local command-line interface (CLI) profile to point to the `kubectl` binary file directory that matches the `kubectl` version of the cluster that you want to work with, or you might be able to use a tool such as `brew switch kubernetes-cli <major.minor>`.





## Time out when trying to connect to a pod
{: #roks_timeout}


You try to connect to a pod, such as logging in with `oc exec` or getting logs with `oc logs`. The pod is healthy, but you see an error message similar to the following.
{: tsSymptoms}

```sh
Error from server: Get https://<10.xxx.xx.xxx>:<port>/<address>: dial tcp <10.xxx.xx.xxx>:<port>: connect: connection timed out
```
{: screen}


The OpenVPN server is experiencing configuration issues that prevent accessing the pod from its internal address.
{: tsCauses}


Before you begin: [Access your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-access_cluster).
{: tsResolve}

1. Check if a cluster and worker node updates are available by viewing your cluster and worker node details in the console or a `cluster ls` or `worker ls` command. If so, [update your cluster and worker nodes to the latest version](/docs/openshift?topic=openshift-update).
2. Restart the OpenVPN pod by deleting it. Another VPN pod is scheduled. When its **STATUS** is **Running**, try to connect the pod that you previously could not connect to.
    ```sh
    oc delete pod -n kube-system -l app=vpn
    ```
    {: pre}
    
## 500 error when trying to log in to an {{site.data.keyword.redhat_openshift_notm}} cluster via `oc login`
{: #500_error_oc_login}


When you try to log in to an {{site.data.keyword.redhat_openshift_notm}} cluster via `oc login` for the first time and you see an error message similar to the following.
{: tsSymptoms}

```txt
$ oc login SERVER -u apikey -p <APIKEY>
The server uses a certificate signed by an unknown authority.
You can bypass the certificate check, but any data you send to the server could be intercepted by others.
Use insecure connections? (y/n): y

Error from server (InternalError): Internal error occurred: unexpected response: 500
```
{: screen}


Some recent changes to the IAM user role have not yet been synchronized to the {{site.data.keyword.redhat_openshift_notm}} cluster.
{: tsCauses}


Synchronize the IAM user information to the {{site.data.keyword.redhat_openshift_notm}} cluster. After the initial user synchronization is performed, further RBAC synchronization should occur automatically.
{: tsResolve}

Before you begin: 

[Access your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-access_cluster).

To synchronize the IAM information for the user, you have 2 options:
- Log in to your cluster from the {{site.data.keyword.redhat_openshift_notm}} [{{site.data.keyword.redhat_openshift_notm}} clusters console](https://cloud.ibm.com/kubernetes/clusters?platformType=openshift){: external}.
- Set your command line context for the cluster by running the  `ibmcloud oc cluster config --cluster CLUSTER` command.

If you use an API key for a functional ID or another user, make sure to log in as the correct user.
{: note}

After the impacted user completes the IAM synchronization, the cluster administrator can verify the user exists in the cluster by listing users with the `oc get users` command.
{: tip}

## Missing projects or `oc` and `kubectl` commands fail
{: #rhoks_ts_admin_config}
{: troubleshoot}
{: support}

**Infrastructure provider**:
* ![Classic](../icons/classic.svg "Classic") Classic
* ![VPC](../icons/vpc.svg "VPC") VPC Generation 2 compute


You don't see all the projects that you have access to. When you try to run `oc` or `kubectl` commands, you see an error similar to the following.
{: tsSymptoms}

```txt
No resources found.
Error from server (Forbidden): <resource> is forbidden: User "IAM#user@email.com" can't list <resources> at the cluster scope: no RBAC policy matched
```
{: screen}

You need to download the `admin` configuration files for your cluster in order to run commands that require the `cluster-admin` cluster role.
{: tsCauses}


Run `ibmcloud oc cluster config --cluster <cluster_name_or_ID> --admin` and try again.
{: tsResolve}


