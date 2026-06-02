---

copyright:
  years: 2025, 2026
lastupdated: "2026-06-02"


keywords: key protect, hpcs, kp, migrate, encryption

subcollection: openshift

---

# Migrating storage components from HPCS to Key Protect
{: #migrate_hpcs_kp}

If your storage components use HPCS and you need to migrate them to use Key Protect instead, follow the information in this document. The exact steps you need to take depend on the type of component you are migrating. For general information about Key Protect, see [About Standard and Dedicated Key Protect](/docs/key-protect?topic=key-protect-about).
{: shortdesc}

## Before you begin
{: #before}

Before you begin, make sure to backup all of your apps and data using a backup tool such as Velero or OpenShift API for Data Protection.
    - [Velero](/docs/containers?topic=containers-data-portability&q=velero&tags=containers#export-velero)
    - [OpenShift API for Data Protection](https://www.redhat.com/en/blog/how-to-backup-and-restore-stateful-applications-on-openshift-using-oadp-and-odf){: external}


## Step 1. Get access to migration tools
{: #request}

Request access to migration tools to use during the process, which are used to detect HPCS key usage and later migrate certain components. You must request access by opening a [customer support ticket], so make sure to plan your timeline accordingly. After you open a customer support ticket, the migration tools are delivered in a zip file called `hpcs-2-kp-k8s.zip`, which contains several scripts for you to run during the migration process.

1. Create an [IBM Support ticket for IBM Cloud Kubernetes Service](/docs/containers?topic=containers-get-help#support-case) to request access to the tooling.
2. Download the `hpcs-2-kp-k8s.zip` file provided in the suppor ticket.
3. Verify the SHA-256 checksum of the downloaded binary matches the value that is provided in the support ticket. Compare the values directly; they must match exactly.

   Run the appropriate command for your operating system to get the SHA-256 checksum and compare with the value that is provided in the support ticket:

   **macOS:**
   ```sh
   shasum -a 256 <kur-binary>
   ```
   {: pre}

   Example:
   ```sh
   shasum -a 256 kur-darwin-arm64-1.0.0
   ```
   {: screen}

   **Linux:**
   ```sh
   sha256sum <kur-binary>
   ```
   {: pre}

   Example:
   ```sh
   sha256sum kur-linux-amd64-1.0.0
   ```
   {: screen}

   **Windows (Command Prompt):**
   ```cmd
   certutil -hashfile <kur-binary> SHA256
   ```
   {: pre}

   Example:
   ```cmd
   certutil -hashfile kur-windows-amd64-1.0.0.exe SHA256
   ```
   {: screen}

   **Windows (PowerShell):**
   ```powershell
   Get-FileHash <kur-binary> -Algorithm SHA256
   ```
   {: pre}

   Example:
   ```powershell
   Get-FileHash kur-windows-amd64-1.0.0.exe -Algorithm SHA256
   ```
   {: screen}


## Step 2. Identify key usage for migration
{: #encryption-hpcs-to-kp-migration-detect}

The tools downloaded in the previous step include a detection script (`hpcs-pvc-scan.sh`) that scans your account for Persistent Volume Claims (PVCs) that are encrypted with HPCS and must be migrated.

1. Run the script to detect HPCS usage.

   ```sh
   chmod +x hpcs-pvc-scan.sh
   ```
   {: pre}

  ```sh
   ./hpcs-pvc-scan.sh
   ```
   {: pre}

3. Review the output for PVCs that must be migrated. Note that the outputs for different components might include different values useful during the migration, such as a key CRN.

**Example output.** Note that this example does not include all possible components. Make sure to review your output carefully to understand which components involved and the full scope of the migration required.

```sh
╔══════════════════════════════════════════════════════════════════╗
║           PVCs Using HPCS Encryption Scan Report                 ║
╚══════════════════════════════════════════════════════════════════╝
Generated   : 2026-03-13T09:08:07Z

── List of COS PVCs ─────────────────────────────

+------+----------+---------------+-------------+------------------+
| S.No | PVC Name | PVC Namespace | Secret Name | Secret Namespace |
+------+----------+---------------+-------------+------------------+
|                           No PVC Found                           |
+------+----------+---------------+-------------+------------------+
╔══════════════════════════════════════════════════════════════════╗
║           PX PVCs Using HPCS Encryption Scan Report              ║
╚══════════════════════════════════════════════════════════════════╝
Generated   : 2026-03-13T09:08:09Z

── List of PX Encrypted PVCs ─────────────────────────────

+------+----------+---------------+-------------+------------------+
| S.No | PVC Name | PVC Namespace | Secret Name | Secret Namespace |
+------+----------+---------------+-------------+------------------+
| 1    | sample7  | portworx      | px-ibm      | portworx         |
| 2    | sample5  | default       | px-ibm      | portworx         |
+------+----------+---------------+-------------+------------------+

── List of PVCs from VPC Block/File CSI Driver ─────────────────────────────

+----------+-----------+------------------------+--------------+------------------------------------------------------------------------------------+
| PVC      | Namespace | PV                     | StorageClass | EncryptionKey                                                                      |
+----------+-----------+------------------------+--------------+------------------------------------------------------------------------------------+
| hpcs-pvc | default   | pvc-c39e4939-fba8-4a18 | hpcs-sc      | crn:v1:staging:public:hs-crypto:us-south:a/c42b8ad8507c90c:0ce92f39-69fd-4200-ba53 |
+----------+-----------+------------------------+--------------+------------------------------------------------------------------------------------+

```
{: screen}


## Step 3. Follow component migration steps
{: #migrate-script}

Different components require different steps for migration. Follow the links for the components that are listed in the output of your detection script. Note that some of these components have migration steps that use other scripts included in the `hpcs-2-kp-k8s.zip` file you downloaded earlier.

- [Openshift Data Foundation (ODF)](/docs/openshift?topic=openshift-migrate_hpcs_kp_odf)
- [Cloud Object Storage (COS)](/docs/openshift?topic=openshift-migrate_hpcs_kp_cos)
- [VPC Block Storage](/docs/openshift?topic=openshift-migrate_hpcs_kms_block)
- [Classic Block Storage](/docs/openshift?topic=openshift-migrate_hpcs_kms_classic_block)
- [Portworx](/docs/openshift?topic=openshift-migrate_hpcs_kp_px)
