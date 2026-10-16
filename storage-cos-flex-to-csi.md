---

copyright:
  years: 2026
lastupdated: "2026-10-15"

keywords: object storage, openshift, cos, FlexVolume, CSI, migrate, migration, cos-flex-to-csi, flex-to-csi, csi driver, object storage migration

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}

# Migrating {{site.data.keyword.cos_full_notm}} PVCs from FlexVolume to CSI
{: #storage-cos-flex-to-csi}

[Virtual Private Cloud]{: tag-vpc}

Use the `cos-flex-to-csi` migration tool to move your {{site.data.keyword.cos_full_notm}} persistent volume claims (PVCs) and secrets from the legacy FlexVolume driver to the modern Container Storage Interface (CSI) driver.
{: shortdesc}

The `cos-flex-to-csi` tool discovers your existing FlexVolume-based PVCs and related secrets, and creates equivalent CSI resources alongside them. Your original resources remain in place until you are ready to remove them, so you can validate the migration before decommissioning the FlexVolume-based resources.

## Why migrate to the CSI driver?
{: #cos-flex-to-csi-why}

The legacy FlexVolume driver is tentatively planned to be unsupported by the end of 2027. Plan to migrate your workloads to the CSI driver before support ends.
{: important}

Kubernetes has deprecated the FlexVolume specification across the industry in favor of the Container Storage Interface (CSI) standard. Migrating your storage resources to the {{site.data.keyword.cos_full_notm}} CSI driver provides the following benefits:

- **Managed add-on lifecycle:** The CSI driver is managed as a cluster add-on with automated patch updates and health management. The add-on installs and updates the `s3fs` or `rclone` mounter and the `cos-csi-mounter` service on your worker nodes, so you don't install or maintain these host components manually.
- **Standard CSI architecture:** The controller server and node server run as containerized pods and follow the standard CSI model. The node server forwards mount and unmount requests from the kubelet to the `cos-csi-mounter` systemd service on the worker node over a Unix socket.
- **Choice of mounters:** You can choose the `s3fs` or `rclone` mounter, with its own mount options, to match the access pattern and performance needs of each workload.

## Differences between FlexVolume and CSI
{: #cos-flex-to-csi-differences}

Review the key architectural and operational differences between the legacy FlexVolume driver and the modern CSI driver.

| Feature | FlexVolume driver (legacy) | CSI driver (modern) |
|---|---|---|
| Provisioner name | `ibm.io/ibmc-s3fs` | `cos.s3.csi.ibm.io` |
| Installation method | Helm chart | Managed cluster add-on (`ibm-object-csi-driver`) |
| Supported infrastructure | Classic, VPC and Satellite | VPC Gen 2 |
| Runtime model | Host-level scripts on worker nodes | Containerized controller and node pods (Deployment and DaemonSet), plus the `cos-csi-mounter` systemd service on each worker node that performs the mount |
| Upgrade management | Manual Helm release updates | Managed cluster add-on updates |
{: caption="Comparison between FlexVolume and CSI drivers" caption-side="bottom"}

## How the migration process works
{: #cos-flex-to-csi-how-it-works}

The `cos-flex-to-csi` tool provides a safe, non-destructive migration path:

1. **Discovery:** Scans your cluster to identify all FlexVolume PVCs and their associated secrets, and checks whether backing PVs have auto-delete bucket protection enabled.
2. **Dry run:** Previews the exact resource definitions and names that the tool generates before applying any changes to your cluster.
3. **Resource creation:** Creates a new CSI-compatible Secret and PVC (suffixed with `-csi-migrated`) in the same namespace as the original FlexVolume PVC. The original FlexVolume resources are not changed. Both resources point to the same underlying {{site.data.keyword.cos_short}} bucket without modifying bucket contents.
4. **Verification and cutover:** Your original FlexVolume PVC remains active until you verify that the new CSI PVC is bound, update your application deployments to reference the new PVC, and manually decommission the legacy resources.

## Before you begin
{: #cos-flex-to-csi-prereqs}

Before you install and run the migration tool, confirm that your environment meets the following requirements.

- Your cluster is a VPC Gen 2 cluster running {{site.data.keyword.containerlong_notm}} or {{site.data.keyword.openshiftlong_notm}}. Classic infrastructure clusters are not supported because the {{site.data.keyword.cos_full_notm}} CSI driver add-on is available only on VPC clusters.
- At least one worker node in your cluster runs Ubuntu or Red Hat CoreOS (RHCOS).
- The {{site.data.keyword.cos_full_notm}} CSI driver add-on is installed in your cluster. To install it, see [Installing the {{site.data.keyword.cos_full_notm}} cluster add-on](/docs/openshift?topic=openshift-storage-cos-install-addon).
- Your `KUBECONFIG` environment variable is set and you have `kubectl` (or `oc`) access to your cluster.
- The `cos-flex-to-csi` tool is run from a Linux (amd64 or arm64) or macOS (amd64 or arm64) machine with outbound internet access to GitHub. If your environment does not have internet access, use the `--no-upgrade` flag on the `migrate` command to skip the automatic self-upgrade check during migration.
- The identity used to run the tool has the [required RBAC permissions](#cos-flex-to-csi-permissions).

## Required permissions
{: #cos-flex-to-csi-permissions}

The `cos-flex-to-csi` tool uses your active `KUBECONFIG` credentials to read and create resources in your cluster. The identity must have the following RBAC permissions before you run the tool.

| Resource | Scope | Verbs required |
|---|---|---|
| `configmaps` | Namespaced (`kube-system` only) | `get` |
| `persistentvolumeclaims` | Namespaced (all user namespaces) | `get`, `list`, `create` |
| `persistentvolumes` | Cluster | `get`, `list` |
| `secrets` | Namespaced (all user namespaces) | `get`, `create` |
| `namespaces` | Cluster | `get` |
| `nodes` | Cluster | `list` |
| `storageclasses` | Cluster | `get`, `list` |
| `daemonsets` | Namespaced (`ibm-object-csi-operator`, `kube-system`) | `get` |
| `deployments` | Namespaced (`ibm-object-csi-operator` only) | `get` |
{: caption="RBAC permissions required by the cos-flex-to-csi migration tool" caption-side="bottom"}

## Installing the migration tool
{: #cos-flex-to-csi-install}

The `cos-flex-to-csi` binary is distributed as a standalone executable from the [ibmcloud-object-storage-plugin GitHub repository](https://github.com/IBM/ibmcloud-object-storage-plugin/releases){: external}. Download and install the latest release for your operating system and architecture.

The tool is available for the following platforms. Archive names follow the pattern `cos-flex-to-csi-v<version>-<os>-<arch>.tar.gz`.

| Platform | Archive file name |
|---|---|
| Linux amd64 | `cos-flex-to-csi-v<version>-linux-amd64.tar.gz` |
| Linux arm64 | `cos-flex-to-csi-v<version>-linux-arm64.tar.gz` |
| macOS amd64 | `cos-flex-to-csi-v<version>-darwin-amd64.tar.gz` |
| macOS arm64 | `cos-flex-to-csi-v<version>-darwin-arm64.tar.gz` |
{: caption="Supported platforms and archive file names" caption-side="bottom"}

The install script in the following steps detects your operating system and architecture automatically.

1. Save the following script to a file named `install-cos-flex-to-csi.sh`.

    ```sh
    #!/bin/bash
    HOST_UNAME="$(uname -s)"
    case "$HOST_UNAME" in
      Linux)  HOST_OS="linux"  ;;
      Darwin) HOST_OS="darwin" ;;
      *)      echo "Unsupported OS: $HOST_UNAME"; exit 1 ;;
    esac

    HOST_MACHINE="$(uname -m)"
    case "$HOST_MACHINE" in
      x86_64)          HOST_ARCH="amd64" ;;
      arm64|aarch64)   HOST_ARCH="arm64" ;;
      *)               echo "Unsupported architecture: $HOST_MACHINE"; exit 1 ;;
    esac

    GITHUB_REPO="IBM/ibmcloud-object-storage-plugin"
    COS_FLEX_TO_CSI_ARCHIVE="$(curl -fsSL \
      "https://api.github.com/repos/${GITHUB_REPO}/releases/latest" \
      | grep -o "cos-flex-to-csi-v[^\"[:space:]]*-${HOST_OS}-${HOST_ARCH}\.tar\.gz" \
      | grep -v '\.sha256$' \
      | head -n 1)"

    curl -fL -O "https://github.com/${GITHUB_REPO}/releases/latest/download/${COS_FLEX_TO_CSI_ARCHIVE}"
    tar -xzf "$COS_FLEX_TO_CSI_ARCHIVE"
    ```
    {: codeblock}

1. Make the script executable and run it to download and extract the latest release.

    ```sh
    chmod +x install-cos-flex-to-csi.sh && ./install-cos-flex-to-csi.sh
    ```
    {: pre}

1. Verify the installation to confirm the binary is ready to use.

    ```sh
    ./cos-flex-to-csi version
    ```
    {: pre}

    The output shows the current version of the tool, confirming the installation was successful.

## Discovering FlexVolume PVCs
{: #cos-flex-to-csi-discover}

Before migrating, scan your cluster to identify all FlexVolume-based PVCs and their associated secrets. The output shows the current migration status of each PVC so you know exactly what needs to be migrated.

1. Run the `discover` command against your target namespace or across all namespaces.

    - To scan a specific namespace, run the following command.

        ```sh
        ./cos-flex-to-csi discover -n NAMESPACE
        ```
        {: pre}

    - To scan all namespaces in the cluster, run the following command.

        ```sh
        ./cos-flex-to-csi discover --all-namespaces
        ```
        {: pre}

1. Review the discovery output table.

    The output lists each FlexVolume-based PVC, whether its backing PV has the `ibm.io/auto-delete-bucket` annotation enabled, its associated secret, migration status, and the names of the migrated CSI resources if migration has already been completed. PVC and secret names are shown in the `NAMESPACE/NAME` format.

    ```text
    5 COS FlexVolume PVC(s) found

    ┌────┬───────────────────┬────────────────────────────────┬──────────────────────┬────────────────┬───────────────────────────┬────────────────────────────────────┐
    │ #  │ COS FLEX PVC NAME │ HAS AUTO-DELETE-BUCKET ENABLED │ COS FLEX SECRET NAME │ MIGRATION DONE │ COS CSI PVC NAME          │ COS CSI SECRET NAME                │
    ├────┼───────────────────┼────────────────────────────────┼──────────────────────┼────────────────┼───────────────────────────┼────────────────────────────────────┤
    │ 1  │ default/pvc-1     │ NO                             │ default/secret-1     │ NO             │ -                         │ -                                  │
    │ 2  │ prod/pvc-2        │ NO                             │ prod/secret-2        │ YES            │ prod/pvc-2-csi-migrated   │ prod/secret-2-pvc-2-csi-migrated   │
    │ 3  │ staging/pvc-3     │ ⚠ YES                          │ staging/secret-3     │ NO             │ -                         │ -                                  │
    │ 4  │ dev/pvc-4         │ NO                             │ shared/secret-4      │ YES            │ dev/pvc-4-csi-migrated    │ dev/secret-4-pvc-4-csi-migrated    │
    │ 5  │ team-a/pvc-5      │ NO                             │ team-a/secret-5      │ ⚠ FAILED       │ team-a/pvc-5-csi-migrated │ team-a/secret-5-pvc-5-csi-migrated │
    └────┴───────────────────┴────────────────────────────────┴──────────────────────┴────────────────┴───────────────────────────┴────────────────────────────────────┘

    Summary: 2 pending, 1 failed, 2 migrated — 5 total PVCs
    ```
    {: screen}

    The FlexVolume driver allows a PVC and its secret to be in different namespaces. The CSI driver requires a PVC and its secret to be in the same namespace. For this reason, the tool creates the CSI secret in the same namespace as the PVC. In the previous example, the FlexVolume PVC `dev/pvc-4` uses the secret `shared/secret-4`, so the CSI secret is created as `dev/secret-4-pvc-4-csi-migrated`. The original secret in the `shared` namespace is not changed.

    The `MIGRATION DONE` column shows the migration status of each PVC.

    | Value | Meaning |
    |---|---|
    | `NO` | The CSI PVC does not exist yet. The PVC still needs to be migrated. |
    | `YES` | The CSI PVC exists and is in the `Bound` state. |
    | `⚠ FAILED` | The CSI PVC exists but is not in the `Bound` state, for example because the `migrate` command timed out while it waited for the PVC to bind. |
    {: caption="Values of the MIGRATION DONE column" caption-side="bottom"}

    If any migrations failed, `discover` prints a `Failed migration(s) detected: CSI PVC exists but is not Bound` message after the table. To resolve the failure, see [Resolving PVCs that fail to bind](#cos-flex-to-csi-failed-bind).

    The `HAS AUTO-DELETE-BUCKET ENABLED` column shows whether the `ibm.io/auto-delete-bucket: true` annotation is set on the backing PV of the FlexVolume PVC.

    | Value | Meaning |
    |---|---|
    | `NO` | The annotation is not set to `true`. The PVC can be migrated. |
    | `⚠ YES` | The annotation is set to `true`. Migration is blocked until you patch the annotation to `false`. |
    {: caption="Values of the HAS AUTO-DELETE-BUCKET ENABLED column" caption-side="bottom"}

    If any PVCs are blocked, `discover` prints a `⚠ MIGRATION BLOCKED — auto-delete-bucket: true detected on N PVC(s)` warning after the table. The warning includes a `kubectl patch` command for each affected backing PV that sets the annotation to `false`, for example:

    ```sh
    kubectl patch pv PV_NAME -p '{"metadata":{"annotations":{"ibm.io/auto-delete-bucket":"false"}}}'
    ```
    {: pre}

    After you apply the patches, run `discover` again to confirm, and then run `migrate`. For more information, see [Resolving blocked PVCs](#cos-flex-to-csi-auto-delete-bucket).

1. Identify the PVCs that require migration.

    The tool determines migration status at run time. It inspects the presence, the annotation (`app.kubernetes.io/created-by=cos-flex-to-csi-migration-tool`), and the phase of the expected CSI PVC in the cluster. A PVC shows `YES` in the `MIGRATION DONE` column only when all of these checks pass. A PVC shows `⚠ FAILED` when the CSI PVC exists but is not in the `Bound` state.

    Review the list and note which PVCs show `NO` or `⚠ FAILED` in the `MIGRATION DONE` column and whether any show `⚠ YES` in the `HAS AUTO-DELETE-BUCKET ENABLED` column before continuing.

## Previewing the migration with a dry run
{: #cos-flex-to-csi-dry-run}

Before applying changes to your cluster, use the `--dry-run` flag to preview exactly what resources the tool creates. A dry run does not modify any cluster resources.

1. Run the `migrate` command with the `--dry-run` flag. Replace NAMESPACE and PVC_NAME with your values.

    ```sh
    ./cos-flex-to-csi migrate -n NAMESPACE --pvc PVC_NAME --dry-run
    ```
    {: pre}

1. Review the output to verify that the generated resource names match your expectations before running the live migration. Pay particular attention to the naming convention described in [Understanding migrated resource names](#cos-flex-to-csi-naming).

## Migrating your PVCs
{: #cos-flex-to-csi-migrate}

After reviewing the dry-run output, run the `migrate` command for each PVC you want to migrate. The tool creates a new CSI secret and PVC alongside the existing FlexVolume resources without removing the originals.

At the start of every `migrate` run, the tool automatically checks the GitHub Releases API for a newer release and upgrades itself if one is available. If your environment does not have internet access to GitHub, include the `--no-upgrade` flag on the `migrate` command. For more information, see [Self-upgrade](#cos-flex-to-csi-upgrade).
{: note}

1. Run the `migrate` command to create the CSI resources.

    - Migrate a PVC named `my-pvc` in the `production` namespace.

        ```sh
        ./cos-flex-to-csi migrate -n production --pvc my-pvc
        ```
        {: pre}

    - Migrate a PVC in an air-gapped environment, skipping the self-upgrade check.

        ```sh
        ./cos-flex-to-csi migrate -n production --pvc my-pvc --no-upgrade
        ```
        {: pre}

1. Repeat this step for each PVC that shows `NO` in the `MIGRATION DONE` column from the discovery step. If a PVC is blocked due to an auto-delete bucket annotation, see [Resolving blocked PVCs](#cos-flex-to-csi-auto-delete-bucket).

    The `migrate` command waits up to 30 seconds for the new CSI PVC to reach the `Bound` state. If the PVC does not bind in that time, the command fails with a `CSI PVC did not reach Bound state within the timeout period` error, and `discover` shows `⚠ FAILED` for the PVC. For more information, see [Resolving PVCs that fail to bind](#cos-flex-to-csi-failed-bind).

## Verifying the migration and updating workloads
{: #cos-flex-to-csi-verify}

After migration, confirm that the new CSI PVC is bound before updating your workloads to use it.

1. Check that the migrated PVC is bound. The migration is successful when the `STATUS` column shows `Bound` for the new CSI PVC, which is named `ORIGINAL_PVC_NAME-csi-migrated`.

    ```sh
    oc get pvc -n NAMESPACE
    ```
    {: pre}

    Look for the `-csi-migrated` PVC in the output and confirm its `STATUS` is `Bound`. If the `STATUS` is not `Bound`, see [Resolving PVCs that fail to bind](#cos-flex-to-csi-failed-bind).

1. Run `discover` again to confirm that `MIGRATION DONE` now shows `YES` for the migrated PVC, and that the `COS CSI PVC NAME` and `COS CSI SECRET NAME` columns are populated.

    ```sh
    ./cos-flex-to-csi discover -n NAMESPACE
    ```
    {: pre}

1. Update your workload deployment YAML files to reference the new CSI PVC name (`ORIGINAL_PVC_NAME-csi-migrated`). For examples of deployment configurations, see [Deploying an app that uses {{site.data.keyword.cos_full_notm}}](/docs/openshift?topic=openshift-storage_cos_apps).

1. Apply the updated deployment to your cluster.

    ```sh
    oc apply -f deployment.yaml
    ```
    {: pre}

1. Verify that your application pods restart and mount the volume successfully.

1. Manually remove the original FlexVolume-based PVC and secret from your cluster when you are ready. Cleanup of the original resources is not automated in the current version of the tool. The original secret might be in a different namespace than the PVC and might be used by other PVCs. Check that no other PVC still uses the secret before you delete it.

## Understanding migrated resource names
{: #cos-flex-to-csi-naming}

All resources created by the migration tool follow a consistent naming pattern so that the original FlexVolume resources and the new CSI resources can coexist safely during transition.

| Original Flex PVC | Original Flex Secret | Migrated CSI PVC | Migrated CSI Secret |
|---|---|---|---|
| `my-pvc` | `my-secret` | `my-pvc-csi-migrated` | `my-secret-my-pvc-csi-migrated` |
{: caption="Naming convention for migrated resources" caption-side="bottom"}

The following naming rules are used by the tool.

- **PVC:** Each migrated PVC always gets the suffix `-csi-migrated`.
- **Secret:** The migrated secret name is built as `<original-secret>-<pvc-name>-csi-migrated`.
- **Namespace:** The migrated PVC and the migrated secret are always created in the same namespace as the original FlexVolume PVC, even when the original secret is in a different namespace. The CSI driver requires a PVC and its secret to be in the same namespace.

This secret naming rule ensures that every migrated PVC gets its own CSI secret, even when the original FlexVolume configuration reused a single secret across multiple PVCs.

### Single secret used by multiple PVCs
{: #cos-flex-to-csi-naming-shared-secret}

If multiple FlexVolume PVCs reference the same original secret, the tool creates one new CSI secret per PVC so that naming remains unique and traceable.

| Original Flex PVC | Original Flex Secret | Migrated CSI PVC | Migrated CSI Secret |
|---|---|---|---|
| `my-pvc-1` | `my-secret` | `my-pvc-1-csi-migrated` | `my-secret-my-pvc-1-csi-migrated` |
| `my-pvc-2` | `my-secret` | `my-pvc-2-csi-migrated` | `my-secret-my-pvc-2-csi-migrated` |
{: caption="Migration naming when one secret is shared across multiple PVCs" caption-side="bottom"}

This avoids name collisions and allows each migrated PVC to reference a dedicated CSI secret.

### Single secret used by single PVC
{: #cos-flex-to-csi-naming-dedicated-secret}

If each FlexVolume PVC references its own original secret, the tool creates one new CSI secret per PVC following the same naming pattern.

| Original Flex PVC | Original Flex Secret | Migrated CSI PVC | Migrated CSI Secret |
|---|---|---|---|
| `my-pvc-1` | `my-secret-1` | `my-pvc-1-csi-migrated` | `my-secret-1-my-pvc-1-csi-migrated` |
| `my-pvc-2` | `my-secret-2` | `my-pvc-2-csi-migrated` | `my-secret-2-my-pvc-2-csi-migrated` |
{: caption="Migration naming when each PVC has a dedicated secret" caption-side="bottom"}

Secret names are unique per migrated PVC, and PVC names are unique per original PVC. This naming pattern prevents collisions and allows the original and migrated resources to exist side by side until cleanup is complete. You can run the `discover` command at any time to see both original and migrated resources side by side.

## CLI reference
{: #cos-flex-to-csi-cli-reference}

The following table lists the top-level flag of the `cos-flex-to-csi` tool.

| Command or flag | Description |
|---|---|
| `./cos-flex-to-csi --upgrade` | Upgrades the migration tool binary to the latest release from GitHub without running a migration. This command is independent of the automatic upgrade check that runs with `migrate`. |
{: caption="cos-flex-to-csi top-level flags" caption-side="bottom"}

## Self-upgrade
{: #cos-flex-to-csi-upgrade}

The tool can upgrade itself to the latest release. The self-upgrade mechanism downloads the new binary from GitHub over HTTPS and automatically verifies its integrity against the SHA-256 checksum archive (`*.sha256`) that is distributed alongside each release. You do not need to verify the checksum manually.

The behavior depends on how you run the tool.

| Invocation | Upgrade behavior | How to skip |
|---|---|---|
| `./cos-flex-to-csi migrate ...` | Checks the GitHub Releases API for a newer binary at the start of every run and upgrades if one is available. | Include the `--no-upgrade` flag on the `migrate` command. |
| `./cos-flex-to-csi --upgrade` | Explicitly fetches and installs the latest release from GitHub. | Not applicable. Upgrading is the primary action of this command. |
{: caption="Self-upgrade behavior" caption-side="bottom"}

The `--no-upgrade` flag applies only to the `migrate` command. It has no effect on `./cos-flex-to-csi --upgrade`. In air-gapped environments, use `--no-upgrade` with `migrate`, and manually download a specific verified release when you need to upgrade.

## Troubleshooting
{: #cos-flex-to-csi-troubleshooting}

Review the following solutions for issues encountered when discovering or migrating resources with the `cos-flex-to-csi` tool.

### Resolving blocked PVCs
{: #cos-flex-to-csi-auto-delete-bucket}

The `migrate` command exits with an error and creates no resources when the backing PV of the FlexVolume PVC has the `ibm.io/auto-delete-bucket: true` annotation. This annotation instructs the FlexVolume driver to delete the {{site.data.keyword.cos_short}} bucket when the PVC is removed. If migration were allowed, the new CSI PVC would be bound to a bucket that might be destroyed when you clean up the FlexVolume resources, which causes permanent data loss.

When a PVC is blocked, the output is similar to the following example.

```text
❌ PV PV_NAME has annotation ibm.io/auto-delete-bucket: true

Migration cannot proceed: the bucket would be auto-deleted when the Flex PVC is removed.
To fix this, patch the annotation to false on the PV and then re-run:

  kubectl patch pv PV_NAME -p '{"metadata":{"annotations":{"ibm.io/auto-delete-bucket":"false"}}}'
```
{: screen}

The tool never patches this annotation automatically. To resolve a blocked PVC, complete the following steps.

1. Patch the annotation to `false` on the backing PV. Replace PV_NAME with the name of the PV.

    ```sh
    kubectl patch pv PV_NAME -p '{"metadata":{"annotations":{"ibm.io/auto-delete-bucket":"false"}}}'
    ```
    {: pre}

1. Run `./cos-flex-to-csi discover` again to confirm that `HAS AUTO-DELETE-BUCKET ENABLED` now shows `NO`.

1. Re-run the `migrate` command for the PVC.

### Resolving PVCs that fail to bind
{: #cos-flex-to-csi-failed-bind}

The `migrate` command creates the CSI secret and the CSI PVC, and then waits up to 30 seconds for the CSI PVC to reach the `Bound` state. If the PVC stays in the `Pending` state, the command fails and `discover` shows `⚠ FAILED` in the `MIGRATION DONE` column for the PVC. The tool does not remove the CSI resources that it created.

When a PVC fails to bind, the output is similar to the following example.

```text
Creating CSI PVC...
✅ CSI PVC created: PVC_NAME-csi-migrated
  ⏳ PVC status: Pending (waiting...)

❌ CSI PVC did not reach Bound state within the timeout period.

To investigate:
  kubectl get pvc PVC_NAME-csi-migrated -n NAMESPACE
  kubectl describe pvc PVC_NAME-csi-migrated -n NAMESPACE
```
{: screen}

To resolve a PVC that failed to bind, complete the following steps.

1. Review the events of the CSI PVC to find the cause of the failure. Replace PVC_NAME and NAMESPACE with the name of the original FlexVolume PVC and its namespace.

    ```sh
    kubectl describe pvc PVC_NAME-csi-migrated -n NAMESPACE
    ```
    {: pre}

1. Fix the root cause that is shown in the `Events` section of the output.

1. If you need to retry the migration, delete the CSI PVC and the CSI secret that the tool created for the failed migration. The CSI secret is in the same namespace as the PVC. Replace FLEX_SECRET_NAME with the name of the original FlexVolume secret.

    ```sh
    kubectl delete pvc PVC_NAME-csi-migrated -n NAMESPACE
    kubectl delete secret FLEX_SECRET_NAME-PVC_NAME-csi-migrated -n NAMESPACE
    ```
    {: pre}

    Delete only the resources with the `-csi-migrated` suffix. Do not delete the original FlexVolume PVC or secret.
    {: important}

1. Re-run the `migrate` command for the original FlexVolume PVC.

1. Run `./cos-flex-to-csi discover` again to confirm that `MIGRATION DONE` now shows `YES`.

## Limitations
{: #cos-flex-to-csi-limitations}

The following scenarios are not supported in the current version of the migration tool.

- **Classic infrastructure clusters** are not supported. The {{site.data.keyword.cos_full_notm}} CSI driver add-on is available only on VPC Gen 2 clusters, so migration is not possible on Classic clusters.
- **Cleanup of original FlexVolume resources** is not automated. You must manually remove the original PVCs and secrets after verifying the migration and updating your workloads. Because an original secret can be in a different namespace than the PVC and can be used by other PVCs, check that no other PVC still uses a secret before you delete it.
- **Unsupported node operating systems:** At least one worker node in the cluster must run Ubuntu or Red Hat CoreOS (RHCOS). Clusters with only RHEL nodes are not supported.
- **Air-gapped environments:** The automatic self-upgrade feature requires outbound internet access to GitHub. Use the `--no-upgrade` flag on the `migrate` command to skip the upgrade check in air-gapped environments. Do not run `./cos-flex-to-csi --upgrade` in air-gapped environments. Instead, manually download a specific verified release.
- **Backing PVs with `ibm.io/auto-delete-bucket: true`:** Migration is blocked for any FlexVolume PVC whose backing PV has the `ibm.io/auto-delete-bucket: true` annotation. You must manually patch the annotation to `false` on the PV before you can migrate. For more information, see [Resolving blocked PVCs](#cos-flex-to-csi-auto-delete-bucket).

If your cluster configuration is not listed as supported, do not proceed with migration until support is confirmed in a future release.

## Next steps
{: #cos-flex-to-csi-next-steps}

- After verifying that your migrated PVCs are bound, update your workloads to reference the new CSI PVCs.
- After updating your workloads, manually remove the original FlexVolume PVCs and secrets from your cluster. Before you delete a secret, check that no other PVC still uses it.
- Review [Deploying an app that uses {{site.data.keyword.cos_full_notm}}](/docs/openshift?topic=openshift-storage-cos-install-addon#cos-addon-app) to explore additional PVC configuration options available with the CSI driver.
- Review the [{{site.data.keyword.cos_full_notm}} add-on parameter reference](/docs/openshift?topic=openshift-storage-cos-install-addon) to customize your CSI driver configuration.

## Related links
{: #cos-flex-to-csi-related}

- [Installing the {{site.data.keyword.cos_full_notm}} cluster add-on](/docs/openshift?topic=openshift-storage-cos-install-addon)
- [Deploying an app that uses {{site.data.keyword.cos_full_notm}}](/docs/openshift?topic=openshift-storage-cos-install-addon#cos-addon-app)
- [ibmcloud-object-storage-plugin releases](https://github.com/IBM/ibmcloud-object-storage-plugin/releases){: external}
