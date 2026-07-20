---

copyright:
  years: 2026
lastupdated: "2026-07-20"

keywords: openshift, openshift data foundation, openshift container storage, disaster recovery, odf rdr, verify, regional disaster recovery

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}

# Verifying your OpenShift Data Foundation Regional Disaster Recovery configuration
{: #openshift_odf_rdr_verify}

[Virtual Private Cloud]{: tag-vpc}
[4.21 and later]{: tag-red}

After you set up OpenShift Data Foundation (ODF) Regional Disaster Recovery (RDR), verify that each component of the stack is healthy and properly configured. Work through each section on the appropriate cluster, hub or managed, as indicated.
{: shortdesc}

## Verifying the ACM add-on on the hub cluster
{: #odf-rdr-verify-acm}

[Hub cluster]{: tag-blue}

Complete the following steps on the **hub cluster**.

1. Verify that the ACM add-on is installed and in a `normal` state. Look for the `acm` add-on in the output and confirm the status shows `Addon Ready`.

    ```sh
    ibmcloud oc cluster addon ls --cluster <hub_cluster_name> | grep -i acm
    ```
    {: pre}

    Example output:
    ```sh
    acm   2.15.0   normal   Addon Ready. For more info: http://ibm.biz/addon-state (H1500)
    ```
    {: screen}

    If the ACM add-on is not listed, [install the ACM add-on](/docs/openshift?topic=openshift-acm&interface=cli).

1. Verify that the ACM add-on pods are running in the `kube-system` namespace. Look for the `acm-agent` and `ibm-acm-operator-controller-manager` pods and confirm that both show `Running` status.

    ```sh
    oc get pods -n kube-system | grep acm
    ```
    {: pre}

    Example output:
    ```sh
    acm-agent-6d9d49cbf6-tsmxd                           1/1   Running   118 (107m ago)   19d
    ibm-acm-operator-controller-manager-bc7b7f969-pr9lj   1/1   Running   3 (7d17h ago)    19d
    ```
    {: screen}

1. Verify that the ACM operator pods and MultiClusterHub pods are running in the `open-cluster-management` namespace.

    ```sh
    oc get pods -n open-cluster-management
    ```
    {: pre}

    Example output:
    ```sh
    multiclusterhub-operator-dcd787649-sqrcx     1/1   Running   0   14d
    console-chart-console-v2-7c8c6649cc-hmg6g    1/1   Running   0   15d
    submariner-addon-76986fdf45-v9kgm            1/1   Running   0   15d
    volsync-addon-controller-6575568dc6-6pjsb    1/1   Running   0   15d
    ```
    {: screen}

    If any pods are missing or not in `Running` status, see [Installing the ACM add-on](/docs/openshift?topic=openshift-acm&interface=cli).

## Verifying that managed clusters are imported and available
{: #odf-rdr-verify-managed-clusters}

[Hub cluster]{: tag-blue}

Complete the following step on the **hub cluster**.

Verify that all managed clusters are successfully imported and show `True` in both the `JOINED` and `AVAILABLE` columns.

```sh
oc get managedclusters
```
{: pre}

Example output:
```sh
NAME             HUB ACCEPTED   MANAGED CLUSTER URLS                                 JOINED   AVAILABLE   AGE
local-cluster    true           https://c100.au-syd.containers.cloud.ibm.com:30253   True     True        14d
managedcluster1  true           https://c100.au-syd.containers.cloud.ibm.com:31003   True     True        14d
managedcluster2  true           https://c100.au-syd.containers.cloud.ibm.com:31888   True     True        14d
```
{: screen}

If a managed cluster is missing or unavailable, [reimport the cluster](/docs/openshift?topic=openshift-acm#import).

## Verifying Submariner connectivity
{: #odf-rdr-verify-submariner}

[Hub cluster]{: tag-blue} [Managed cluster]{: tag-warm-gray}

Submariner provides network connectivity between your managed clusters. Complete the steps in each subsection on the cluster indicated.

### Verify the Submariner operator on the hub cluster
{: #odf-rdr-verify-submariner-hub}

[Hub cluster]{: tag-blue}

1. Verify that the Submariner operator pod is running on the **hub cluster**.

    ```sh
    oc get pods -n submariner-operator
    ```
    {: pre}

    Example output:
    ```sh
    NAME                                  READY   STATUS    RESTARTS      AGE
    submariner-operator-6bf8d56f74-7v44v  1/1     Running   3 (17h ago)   14d
    ```
    {: screen}

1. Verify that the Submariner add-on is registered for each managed cluster. Confirm that the `AVAILABLE` column shows `True` for each managed cluster.

    ```sh
    oc get managedclusteraddon -A | grep submariner
    ```
    {: pre}

    Example output:
    ```sh
    managedcluster1   submariner   True   False
    managedcluster2   submariner   True   False
    ```
    {: screen}

1. Verify that the Submariner broker exists.

    ```sh
    oc get broker -A
    ```
    {: pre}

    Example output:
    ```sh
    NAMESPACE                 NAME                AGE
    submariner-set1-broker    submariner-broker   12d
    ```
    {: screen}

### Verify Submariner on the managed clusters
{: #odf-rdr-verify-submariner-managed}

[Managed cluster]{: tag-warm-gray}

Run the following steps on **each managed cluster**.

1. Verify that the required Submariner pods are running. Confirm that `submariner-gateway`, `submariner-routeagent`, and `submariner-globalnet` pods are present and show `Running` status.

    ```sh
    oc get pods -n submariner-operator
    ```
    {: pre}

    Example output:
    ```sh
    NAME                                              READY   STATUS    RESTARTS      AGE
    submariner-addon-bc6bbf579-wjqhq                  1/1     Running   0             12d
    submariner-gateway-hxcbh                          1/1     Running   0             12d
    submariner-globalnet-jbmxw                        1/1     Running   3 (12d ago)   12d
    submariner-lighthouse-agent-858896855b-xghxn      1/1     Running   0             12d
    submariner-lighthouse-coredns-66d5579b66-52f6j    1/1     Running   0             12d
    submariner-lighthouse-coredns-66d5579b66-jhqkm    1/1     Running   0             12d
    submariner-metrics-proxy-65n4c                    2/2     Running   3 (12d ago)   12d
    submariner-operator-7c99f89cfb-rppth              1/1     Running   2 (17h ago)   12d
    submariner-routeagent-27p7v                       1/1     Running   0             12d
    submariner-routeagent-jjw66                       1/1     Running   0             12d
    submariner-routeagent-nt78s                       1/1     Running   0             12d
    ```
    {: screen}

1. Verify that the Submariner connection is healthy. In the output, check that `RouteAgentConnectionDegraded` has a `status` of `"False"`, which confirms that all route agent connections to remote endpoints are established and healthy.

    ```sh
    oc -n <managed_cluster_name> get managedclusteraddons submariner -o yaml
    ```
    {: pre}

    Example output:
    ```yaml
    status:
      - lastTransitionTime: "2026-03-18T03:36:24Z"
        message: All RouteAgent connections to remote endpoints are established and healthy.
        reason: ConnectionsEstablished
        status: "False"
        type: RouteAgentConnectionDegraded
    ```
    {: screen}

    If connectivity is degraded, reinstall Submariner by following [Step 4 of the ODF Regional Disaster Recovery setup](/docs/openshift?topic=openshift-openshift_odf_rdr_roks#submariner).

## Verifying ODF on the managed clusters
{: #odf-rdr-verify-odf}

[Managed cluster]{: tag-warm-gray}

Run the following steps on **each managed cluster**.

1. Verify that the ODF StorageCluster is ready and Ceph health is `HEALTH_OK`. In the output, confirm that the `PHASE` column shows `Ready` for the StorageCluster and the `HEALTH` column shows `HEALTH_OK` for the CephCluster.

    ```sh
    oc get storagecluster -n openshift-storage
    oc get cephcluster -n openshift-storage
    ```
    {: pre}

    Example output:
    ```sh
    NAME                 AGE   PHASE   EXTERNAL   CREATED AT             VERSION
    ocs-storagecluster   12d   Ready              2026-03-17T10:51:46Z   4.20.7

    NAME                              DATADIRHOSTPATH   MONCOUNT   AGE   PHASE   MESSAGE                       HEALTH      EXTERNAL   FSID
    ocs-storagecluster-cephcluster    /var/lib/rook     3          12d   Ready   Cluster created successfully  HEALTH_OK              5fb59e70-bd54-438f-9190-c09ddcf04c0c
    ```
    {: screen}

    If this is a fresh ODF installation and no applications have been deployed, consider reinstalling ODF by following the [ODF installation guide](/docs/openshift?topic=openshift-deploy-odf-vpc&interface=cli).

1. Verify that the required ServiceExports are present. Confirm that `ocs-provider-server` and the `rook-ceph-mon-*` and `rook-ceph-osd-*` entries are listed.

    ```sh
    oc get serviceexports -n openshift-storage
    ```
    {: pre}

    Example output:
    ```sh
    NAME                  AGE
    ocs-provider-server   12d
    rook-ceph-mon-d       12d
    rook-ceph-mon-e       12d
    rook-ceph-mon-f       12d
    rook-ceph-osd-0       12d
    rook-ceph-osd-1       12d
    rook-ceph-osd-2       12d
    ```
    {: screen}

    If the `ocs-provider-server` ServiceExport is missing, recreate it by following [Step 5 of the ODF Regional Disaster Recovery setup](/docs/openshift?topic=openshift-openshift_odf_rdr_roks#odf_install).

1. Verify that the multicluster network configuration is properly set on the StorageCluster. In the output, confirm that `multiClusterService.enabled` is `true` and that `clusterID` matches the name of the managed cluster. Also confirm that the `ocs.openshift.io/api-server-exported-address` annotation is present and correctly set.

    ```sh
    oc get storagecluster -n openshift-storage -o yaml
    ```
    {: pre}

    Look for the following values in the output:
    ```yaml
    network:
      multiClusterService:
        clusterID: <cluster-name>
        enabled: true
    ```
    {: pre}

    And the following annotation:
    ```yaml
    ocs.openshift.io/api-server-exported-address: <cluster-name>.ocs-provider-server.openshift-storage.svc.clusterset.local:50051
    ```
    {: pre}

## Verifying the ODF Multicluster Orchestrator on the hub cluster
{: #odf-rdr-verify-multicluster-orchestrator}

[Hub cluster]{: tag-blue}

Complete the following steps on the **hub cluster**.

1. Verify that the OpenShift GitOps operator pods are running. The ODF Multicluster Orchestrator requires GitOps to be installed first.

    ```sh
    oc get pods -n openshift-gitops
    ```
    {: pre}

    Example output:
    ```sh
    NAME                                                           READY   STATUS    RESTARTS   AGE
    cluster-6484df7d8f-fbk9b                                       1/1     Running   0          4d12h
    gitops-plugin-8646dcfd5d-kj5mf                                 1/1     Running   0          4d12h
    openshift-gitops-application-controller-0                      1/1     Running   0          4d12h
    openshift-gitops-applicationset-controller-664645457b-8n9gj    1/1     Running   0          4d12h
    openshift-gitops-dex-server-74ddb4bb94-trxk6                   1/1     Running   0          4d12h
    openshift-gitops-redis-68469975f8-mlkrq                        1/1     Running   0          14d
    openshift-gitops-repo-server-76567d7c46-j9fjq                  1/1     Running   0          4d12h
    openshift-gitops-server-6d74f8d998-f97zx                       1/1     Running   0          4d12h
    ```
    {: screen}

    If GitOps is not installed, see [Installing Red Hat OpenShift GitOps Operator in web console](https://docs.redhat.com/en/documentation/red_hat_openshift_gitops/1.20/html-single/installing_gitops/index#installing-gitops-operator-in-web-console_installing-openshift-gitops){: external}.

1. Verify that the ODF Multicluster Orchestrator operator pods are running in the `openshift-operators` namespace. Confirm that `odf-multicluster-console` and `odfmo-controller-manager` pods both show `Running` status.

    ```sh
    oc get pods -n openshift-operators | grep -i odf
    ```
    {: pre}

    Example output:
    ```sh
    odf-multicluster-console-cdd786658-2bdbz   1/1   Running   0             12d
    odfmo-controller-manager-8585c4bf9-mwhvf   1/1   Running   2 (16h ago)   12d
    ```
    {: screen}

1. Verify that the Ramen hub operator pod is running in the `submariner-operator` namespace.

    ```sh
    oc get pods -n submariner-operator
    ```
    {: pre}

    Example output:
    ```sh
    NAME                                  READY   STATUS    RESTARTS      AGE
    submariner-operator-6bf8d56f74-7v44v  1/1     Running   3 (17h ago)   14d
    ```
    {: screen}

1. Verify that the Ramen DR cluster operator pod is running on **each managed cluster** in the `openshift-dr-system` namespace.

    ```sh
    oc get pods -n openshift-dr-system | grep -i ramen
    ```
    {: pre}

    Example output:
    ```sh
    ramen-dr-cluster-operator-785d878dbc-lbrgz   2/2   Running   0   2d15h
    ```
    {: screen}

## Verifying the DR policy and MirrorPeer on the hub cluster
{: #odf-rdr-verify-drpolicy}

[Hub cluster]{: tag-blue}

Complete the following steps on the **hub cluster**.

1. Verify that the DRPolicy is validated. In the output, confirm that the `Validated` condition has a `status` of `"True"`.

    ```sh
    oc get drpolicy -A
    oc describe drpolicy <drpolicy_name>
    ```
    {: pre}

    Example output from `oc describe`:
    ```yaml
    status:
      conditions:
        - type: Validated
          status: "True"
    ```
    {: pre}

    If the DRPolicy is not validated, verify that NooBaa object buckets were created successfully on both managed clusters.

1. Verify that the MirrorPeer phase is `ExchangedSecret`. Describe the MirrorPeer resource and check the `Phase` field.

    ```sh
    oc get mirrorpeers -A
    oc describe mirrorpeer <mirrorpeer_name>
    ```
    {: pre}

    Example output from `oc describe`:
    ```yaml
    Status:
      Phase: ExchangedSecret
    Events: <none>
    ```
    {: pre}

    If the phase shows `ExchangingSecret`, verify Submariner connectivity by following [Verifying Submariner connectivity](#odf-rdr-verify-submariner).

## Verifying optional operators on the managed clusters
{: #odf-rdr-verify-optional-operators}

[Managed cluster]{: tag-warm-gray}

If you installed optional operators as part of your ODF RDR setup, verify that they are running on **each managed cluster**.

You are responsible for managing optional operators, including updating, monitoring, recovery, and reinstallation.
{: important}

1. Verify that the OpenShift GitOps operator pods are running. Confirm that the `openshift-gitops-application-controller`, `openshift-gitops-server`, and other GitOps pods show `Running` status.

    ```sh
    oc get pods -n openshift-gitops
    ```
    {: pre}

1. Verify that the OpenShift API for Data Protection (OADP) operator pods are running. Confirm that `openshift-adp-controller-manager` and `velero` pods both show `Running` status.

    ```sh
    oc get pods -n openshift-adp
    ```
    {: pre}

    Example output:
    ```sh
    NAME                                                  READY   STATUS    RESTARTS   AGE
    openshift-adp-controller-manager-7c8fc7f964-j2jnq    1/1     Running   1          12d
    velero-9cdf64b8b-9c2kk                               1/1     Running   1          12d
    ```
    {: screen}

    If an operator is missing, reinstall it by following the relevant installation guide.

## Collecting must-gather logs
{: #odf-rdr-must-gather}

[Hub cluster]{: tag-blue} [Managed cluster]{: tag-warm-gray}

If you cannot resolve an issue by working through the previous verification steps, collect must-gather logs from your hub and managed clusters and share them with IBM Support.

### Collect hub cluster logs
{: #odf-rdr-must-gather-hub}

[Hub cluster]{: tag-blue}

Run the following script on the **hub cluster** to collect diagnostic information.

```sh
#!/bin/bash
# Usage: ./hub-check.sh <cluster-name>
CLUSTER_NAME=$1
if [[ -z "$CLUSTER_NAME" ]]; then
  echo "Usage: $0 <cluster-name>"
  exit 1
fi

echo "===== Verify ACM ====="
ibmcloud oc cluster addon ls --cluster "$CLUSTER_NAME" | grep -i acm
oc get pods -n kube-system | grep acm
oc get pods -n open-cluster-management
oc get managedclusters

echo "===== Verify Submariner ====="
oc get pods -n submariner-operator
oc get managedclusteraddon -A | grep submariner
oc get managedclusteraddon -A -o yaml
oc get broker -A

echo "===== Verify Multicluster Operator ====="
oc get pods -n openshift-operators | grep -i odf
oc get drpolicy -A
oc get mirrorpeers -A

echo "===== Verify Additional Operators ====="
oc get pods -n openshift-gitops
oc get pods -n openshift-adp
```
{: pre}

### Collect managed cluster logs
{: #odf-rdr-must-gather-managed}

[Managed cluster]{: tag-warm-gray}

Run the following script on **each managed cluster** to collect diagnostic information.

```sh
#!/bin/bash
# Usage: ./managedCluster-check.sh

echo "===== Verify Submariner ====="
oc get pods -n submariner-operator
oc get submariner -A

echo "===== Verify DR Operator ====="
oc get pods -n openshift-dr-system | grep -i ramen

echo "===== Verify ODF ====="
oc get storagecluster -n openshift-storage
oc get cephcluster -n openshift-storage
oc get serviceexports -n openshift-storage
oc get storagecluster -n openshift-storage -o yaml

echo "===== Verify Additional Operators ====="
oc get pods -n openshift-gitops
oc get pods -n openshift-adp
```
{: pre}

For additional must-gather guidance, see the following resources:

- [Red Hat ACM must-gather](https://github.com/stolostron/must-gather){: external}
- [Red Hat ODF troubleshooting guide](https://docs.redhat.com/en/documentation/red_hat_openshift_data_foundation/4.21/html-single/troubleshooting_openshift_data_foundation/index){: external}
- [OpenShift gathering cluster data](https://docs.redhat.com/en/documentation/openshift_container_platform/4.21/html/support/gathering-cluster-data#about-must-gather_gathering-cluster-data){: external}

## Next steps
{: #odf-rdr-verify-next-steps}

- If all components are healthy, [test your disaster recovery configuration](/docs/openshift?topic=openshift-openshift_odf_rdr_roks#odf-rdr-test) by running a failover and relocate scenario.
- If you need further assistance, [contact IBM Support](/docs/openshift?topic=openshift-get-help) and include the must-gather logs you collected.
- Review the [ODF Regional Disaster Recovery setup guide](/docs/openshift?topic=openshift-openshift_odf_rdr_roks) to confirm all installation steps were completed correctly.

## Related links
{: #odf-rdr-verify-related-links}

- [Troubleshooting regional disaster recovery](https://docs.redhat.com/en/documentation/red_hat_openshift_data_foundation/4.21/html/configuring_openshift_data_foundation_disaster_recovery_for_openshift_workloads/troubleshooting_disaster_recovery#troubleshooting-regional-disaster-recovery_monitor-dr){: external}
- [Red Hat ODF troubleshooting guide](https://docs.redhat.com/en/documentation/red_hat_openshift_data_foundation/4.21/html-single/troubleshooting_openshift_data_foundation/index){: external}
- [Red Hat ACM must-gather](https://github.com/stolostron/must-gather){: external}
- [Installing the ACM add-on](/docs/openshift?topic=openshift-acm&interface=cli)
