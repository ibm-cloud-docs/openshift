---

copyright: 
  years: 2014, 2022
lastupdated: "2022-04-12"

keywords: openshift, dedicated hosts, host pool, dedicated pool

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# VPC: Why can't I create worker nodes on dedicated hosts?
{: #ts-worker-dedicated}
{: support}

When you try to create worker nodes on dedicated hosts, you see an error message similar to one of the following.
{: tsSymptoms}

```sh
The dedicated hosts for the zone 'eu-de-2' are not ready.
```
{: screen}

```sh
Insufficient dedicated hosts available in zone 'us-south-3'.
```
{: screen}

```sh
Dedicated host has insufficient capacity
```
{: screen}

The possible causes for these issues include:
{: tsCauses}

- There are no dedicated hosts in the specified zone or pool.
- There are not enough dedicated hosts available.
- There are not enough resources available on the dedicated host.

Complete the following steps to resolve the issue.
{: tsResolve}

1. List your dedicated host pools and make a note of the pool ID.
    ```sh
    ibmcloud oc dedicated pool ls
    ```
    {: pre}
    
1. Lists the hosts in the pool and verify there are available hosts and that placement is enabled.

    ```sh
    ibmcloud oc dedicated host ls --pool POOL
    ```
    {: pre}

    * If there are no dedicated hosts in the zone, [create a new dedicated host in the zone](/docs/openshift?topic=openshift-dedicated-hosts#setup-dedicated-host-cli). After creating a host, [replace the worker node to reprovision](/docs/openshift?topic=openshift-kubernetes-service-cli#cli_worker_replace).

    * If there are available hosts in the zone, but placement is not enabled on the dedicated host you want to use, enable host placement. 
        ```sh
        ibmcloud oc dedicated host placement enable --host HOST --pool POOL 
        ```
        {: pre}

        After enabling host placement, wait to see if provisioning succeeds. If you still see provisioning errors, continue the steps to verify there are enough resources available. Or, [replace the worker node to reprovision](/docs/openshift?topic=openshift-kubernetes-service-cli#cli_worker_replace).
    
1. If there are available hosts, and placement is enabled, review the details of your dedicated host and verify there are enough resources available to create the worker node.
    ```sh
    ibmcloud oc dedicate host get --host HOST --pool POOL
    ```
    {: pre}
    
    You can also review your dedicated host resources in the [console](https://cloud.ibm.com/kubernetes/dedicated-hosts){: external}.
    {: tip}
    
    * If there are enough resources available, [replace the worker node that failed to reprovision](/docs/openshift?topic=openshift-kubernetes-service-cli#cli_worker_replace). Note that in some cases, it is not possible to reach 100% capacity.
    * If there are not enough resources on the dedciated host, reallocate your workloads to free up capacity on the host, or [create a new dedicated host in the zone](/docs/openshift?topic=openshift-dedicated-hosts#setup-dedicated-host-cli). 



