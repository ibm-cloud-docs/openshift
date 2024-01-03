---

copyright:
  years: 2014, 2024
lastupdated: "2024-01-03"


keywords: openshift, cluster version, 

subcollection: openshift
content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}


# Why does OpenShift show the cluster version is down-level?
{: #ts-cluster-version-downlevel}
{: support}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [{{site.data.keyword.satelliteshort}}]{: tag-satellite}


You see one or more of the following for an extended period of time.
{: tsSymptoms}


- The OpenShift Web Console displays a banner stating that the cluster is updating and the **Cluster Settings** page shows the current version has a status of `Partial`.

- When you run `oc get clusterversion` command you see an earlier version.

    ```txt
    NAME      VERSION   AVAILABLE   PROGRESSING   SINCE   STATUS
    version   4.11.27   True        True          27h     Unable to apply 4.12.3: an unknown error has occurred: MultipleErrors
    ```
    {: screen}


- You see that a cluster master upgrade was cancelled with a status similar to the following.

    ```txt
    Version update cancelled. CAE012: Cannot complete cluster master operations because the current OpenShift clusterversion rollout is not complete. For more information, see the troubleshooting docs: 'https://ibm.biz/rhos_clusterversion_ts'
    ```
    {: screen}


A cluster master update to a new patch version or an upgrade to a new minor version has not completed.
{: tsCauses}

A cluster master update completes soon after updating the Cluster Version Operator. The Cluster Version Operator manages updates to various Cluster Operators, a process which continues after a cluster master update has completed. 

```sh
$ oc get clusterversion
NAME      VERSION   AVAILABLE   PROGRESSING   SINCE   STATUS
version   4.13.11   True        False         33h     Cluster version is 4.13.11

$ oc get co
NAME                                       VERSION   AVAILABLE   PROGRESSING   DEGRADED   SINCE   MESSAGE
console                                    4.13.11   True        False         False      2d3h    
csi-snapshot-controller                    4.13.11   True        False         False      2d4h    
dns                                        4.13.11   True        False         False      2d4h    
image-registry                             4.13.11   True        False         False      2d4h    
ingress                                    4.13.11   True        False         False      2d4h    
insights                                   4.13.11   True        False         False      2d4h    
kube-apiserver                             4.13.11   True        False         False      2d4h    
kube-controller-manager                    4.13.11   True        False         False      2d4h    
kube-scheduler                             4.13.11   True        False         False      2d4h    
kube-storage-version-migrator              4.13.11   True        False         False      2d4h    
marketplace                                4.13.11   True        False         False      2d4h    
monitoring                                 4.13.11   True        False         False      2d4h    
network                                    4.13.11   True        False         False      2d4h    
node-tuning                                4.13.11   True        False         False      32h     
openshift-apiserver                        4.13.11   True        False         False      2d4h    
openshift-controller-manager               4.13.11   True        False         False      2d4h    
openshift-samples                          4.13.11   True        False         False      33h     
operator-lifecycle-manager                 4.13.11   True        False         False      2d4h    
operator-lifecycle-manager-catalog         4.13.11   True        False         False      2d4h    
operator-lifecycle-manager-packageserver   4.13.11   True        False         False      2d4h    
service-ca                                 4.13.11   True        False         False      2d4h    
storage                                    4.13.11   True        False         False      2d4h    
```
{: screen}

If the cluster has just been upgraded, the cluster operators can take several minutes to upgrade. It is normal to see a status like the following with the number of completed steps increasing over time.

```sh
Working towards 4.13.11: 511 of 616 done (82% complete), waiting on network
```
{: screen}


If the cluster continues shows partial update for an extended period there is a problem in the cluster that is preventing the cluster operators from updating to the current version. This can be caused by many things, such as the following examples.

- Unhealthy cluster components such as worker nodes blocking the rollout of operator updates.
- Incorrect change to a cluster operator configuration.
- Conflicting changes to cluster configurations, such as RBAC changes that affect OpenShift components.



Begin by getting more detailed information about the cluster operator update progress and problems.
{: tsResolve}

1. Run the following commands to get more information.

    ```sh
    oc get clusterversion
    ```
    {: pre}
    
    ```sh
    oc get clusteroperators
    ```
    {: pre}
    
    ```sh
    oc describe clusteroperator NAME
    ```
    {: pre}

1. Review the **MESSAGE** column in the command output to identify which cluster operators are currently blocking progress and give an indication of the problem. The way in which OpenShift updates operators can result in unexpected dependencies; for example, some cluster operator updates might be waiting for other operators to complete the step they are running now.

1. Check the worker node status using the `oc get nodes` command. Sometimes nodes are not `Ready`, which can be due to a lack of resources on a node or a problem with `kube-proxy` or `kubelet`. This can cause issues during an update.

    - If you have recently changed the configuration of one of the incomplete operators, describe the operator for more details by running `oc describe clusteroperator NAME`.For example `oc describe cluster-operator image-registry` might show an error that helps identify the problem.

    - Continue checking the status and logs of the operator pods for further debugging of the issue. Sometimes the operators are degraded, but that does not mean the updates have failed or are not working.


1. If you are not able to identify or resolve the problems, or if the issue persists, contact support. Open a [support case](/docs/get-support?topic=get-support-using-avatar). In the case details, be sure to include any relevant log files, error messages, or command outputs.






