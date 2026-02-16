---

copyright: 
  years: 2026, 2026
lastupdated: "2026-02-16"


keywords: kubernetes, openshift, ca cert, certificate authority, rotate

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}



# Why can't I create or renew my CA cert?
{: #ts-cert-failed}
{: troubleshoot}
{: support}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf}

When you run the `cluster ca create` command, you see an error message similar to the following.
{: tsSymptoms}

```sh
ibmcloud ks cluster ca create -c CLUSTER
```
{: pre}

```txt
FAILED
You must reload/update/replace all workers and download new certificates locally in order to revoke old CA Cert. (E1955)
```
{: screen}


This error can occur when you try starting a new rotation process without completing a prior one. After a rotation is started, all steps must be completed before another rotation can be initiated. 
{: tsCauses}


To complete the rotation process, you must reload or replace your worker nodes.
{: tsResolve}

1. Reload or replace your worker nodes by following the steps for your cluster type.
    

    * [Reload your classic worker nodes](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_reload).
    * [Replace your VPC worker nodes](/docs/openshift?topic=openshift-kubernetes-service-cli#cli_worker_replace).

1. Update any tooling or webhooks that rely on the previous certificates. For example, you might need to update one or more of the following.
    - If you use the certificate from your cluster's `kubeconfig` file in your own service, such as Jenkins.
    - If you use `calicoctl` to manage Calico network policies, update your services and automation to use the new certificates.
    - If you forward audit logs to {{site.data.keyword.logs_full_notm}}, update the certificates for your [master audit webhook](/docs/openshift?topic=openshift-health-audit).
    - If you forward audit logs over the private network, update the certificates for your [master audit webhook](/docs/openshift?topic=openshift-health-audit#audit-api-server-priv).

1. Run the `ca rotate` command to complete the certificate rotation.

    ```sh
    ibmcloud ks cluster ca rotate -c CLUSTER
    ```
    {: pre}

1. If the issue persists, contact support. Open a [support case](/docs/account?topic=account-using-avatar). In the case details, be sure to include any relevant log files, error messages, or command outputs.



