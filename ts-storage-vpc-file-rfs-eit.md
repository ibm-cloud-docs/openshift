---

copyright:
  years: 2026
lastupdated: "2026-08-13"


keywords: kubernetes, openshift, rfs, regional file storage, eit, encryption in transit, stunnel, troubleshooting

subcollection: openshift
content-type: troubleshoot


---

{{site.data.keyword.attribute-definition-list}}

# Troubleshooting Regional File Storage encryption in transit
{: #ts-storage-vpc-file-rfs-eit}

[Virtual Private Cloud]{: tag-vpc}

Use the following troubleshooting topics to resolve issues with Regional File Storage (RFS) encryption in transit (EIT).
{: shortdesc}

RFS EIT is available as a Beta feature and is recommended for experimental use only. Do not use this feature in production workloads.
{: beta}

## Why is my PVC stuck in Pending with `'rfs' profile is not accessible`?
{: #ts-rfs-eit-pvc-pending}

Your PVC remains in `Pending` state after creation, and you see an error similar to the following in the PVC events.
{: tsSymptoms}

```sh
'rfs' profile is not accessible
```
{: screen}

Your account might not be allowlisted for the `rfs` profile, or your cluster might not have the required IAM permissions for VPC file share operations.
{: tsCauses}

To resolve the issue:
{: tsResolve}

1. Check the PVC events to confirm the error.

    ```sh
    oc describe pvc <pvc-name>
    ```
    {: pre}

    Look for `'rfs' profile is not accessible` in the `Events` section. If this error is present, your account needs to be allowlisted for the `rfs` profile.

1. If the error is `'rfs' profile is not accessible`, [open a VPC support ticket](https://cloud.ibm.com/unifiedsupport/cases/add){: external} to request access. After your account is allowlisted, restart the CSI driver node pods.

    ```sh
    oc rollout restart daemonset ibm-vpc-file-csi-node -n kube-system
    ```
    {: pre}

1. If the PVC shows permission-related errors instead, verify that your cluster has the required [IAM permissions for VPC file share operations](/docs/vpc?topic=vpc-file-storage-vpc-about&interface=ui#fs-vpc-iam).

## Why does my pod fail to mount with `stunnel manager is not initialized`?
{: #ts-rfs-eit-stunnel-init}

Your pod shows a `FailedMount` event with an error similar to the following.
{: tsSymptoms}

```sh
stunnel manager is not initialized, this indicates a configuration error.
Restart the file csi node server pod from kube-system namespace where the
application is running and check if the issue is resolved.
```
{: screen}

The stunnel manager on the CSI node server pod on the affected worker node is not initialized, which indicates a configuration error on that node.
{: tsCauses}

To resolve the issue:
{: tsResolve}

1. Find the CSI node server pod that is running on the same node as your application pod. Note the node name where your pod is scheduled.

    ```sh
    oc get pod <app-pod-name> -o wide
    ```
    {: pre}

1. Get the CSI node server pod running on that node.

    ```sh
    oc get pods -n kube-system -l app=ibm-vpc-file-csi-node \
      --field-selector spec.nodeName=<node-name>
    ```
    {: pre}

1. Delete the CSI node server pod so that it restarts automatically.

    ```sh
    oc delete pod -n kube-system <csi-node-pod>
    ```
    {: pre}

1. Wait for the pod to restart and reach `Running` state, then retry your application pod.

    ```sh
    oc get pods -n kube-system -l app=ibm-vpc-file-csi-node
    ```
    {: pre}

    If the issue persists after the pod restarts, [open a support ticket](/docs/get-support) with the IBM Cloud Container Storage team.

## Why does my application with `hostNetwork: true` fail to bind a port?
{: #ts-rfs-eit-hostnetwork-port}

An application pod that uses `hostNetwork: true` fails at startup with the following error.
{: tsSymptoms}

```sh
Address already in use
```
{: screen}

RFS EIT binds one port per PVC mount in the range 11300–11599 on `127.0.0.1`. An application pod that uses `hostNetwork: true` and tries to bind to a port in this range conflicts with an existing RFS EIT PVC mount on the same node.
{: tsCauses}

To resolve the issue, choose one of the following options:
{: tsResolve}

- Scale down all applications that use RFS EIT file shares, then scale them back up. After scaling up, the application pods pick up different ports from the allocation range, and the conflict is resolved.
- Access the application through a Kubernetes `Service` resource instead of relying on host ports with `hostNetwork: true`. This avoids the port conflict entirely.

## Related topics
{: #ts-rfs-eit-related}

- [Regional File Storage encryption in transit (Beta)](/docs/openshift?topic=openshift-storage-file-vpc-eit#vpc-file-rfs-eit)
- [Why do I see an `UnresponsiveMountHelperContainerUtility` error?](/docs/openshift?topic=openshift-ts-storage-vpc-file-eit-unresponsive)
- [Why do I see a `MetadataServiceNotEnabled` error?](/docs/openshift?topic=openshift-ts-storage-vpc-file-eit-metadata)
