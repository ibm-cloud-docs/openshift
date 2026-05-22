---

copyright:
  years: 2026
lastupdated: "2026-05-22"

keywords: openshift, gpu, nvidia, rhel9, eus, repository, driver

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why does my NVIDIA GPU driver installation fail on RHEL 9 worker nodes?
{: #ts-gpu-driver-rhel9-eus}
{: troubleshoot}
{: support}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [{{site.data.keyword.satelliteshort}}]{: tag-satellite}

When you try to install NVIDIA GPU drivers on Red Hat Enterprise Linux 9 worker nodes, the installation fails with a repository error.
{: tsSymptoms}

You see an error message in the `nvidia-driver-daemonset-*` pod logs similar to the following:

```sh
Error: Unable to find a match: kernel-headers-VERSION kernel-devel-VERSION
```
{: screen}

For example:

```sh
Error: Unable to find a match: kernel-headers-5.14.0-570.112.1.el9_6.x86_64 kernel-devel-5.14.0-570.112.1.el9_6.x86_64
```
{: screen}

The NVIDIA GPU Operator does not enable all required Extended Update Support (EUS) repositories for RHEL 9 worker nodes. While EUS repositories are now enabled for RHEL 9 worker nodes in {{site.data.keyword.openshiftlong_notm}}, the NVIDIA driver installation requires additional repository configuration.
{: tsCauses}

Apply a ConfigMap to enable the required EUS repositories for the NVIDIA GPU driver installation.
{: tsResolve}

1. SSH to one of your RHEL 9 worker nodes to retrieve the required repository configuration values.

    ```sh
    oc debug node/<worker-node-name>
    ```
    {: pre}

2. Access the host file system.

    ```sh
    chroot /host
    ```
    {: pre}

3. View the Red Hat repository configuration to retrieve the required values.

    ```sh
    cat /etc/yum.repos.d/redhat.repo
    ```
    {: pre}

4. From the output, locate the `[rhel-9-for-x86_64-appstream-eus-rpms]` section and note the following values:
    - `baseurl` - The base URL for the repository
    - `sslclientkey` - The path to the SSL client key (contains a certificate serial number)
    - `sslclientcert` - The path to the SSL client certificate (contains the same certificate serial number)

    The certificate serial number appears in both the `sslclientkey` and `sslclientcert` paths. For example, if the paths are `/etc/pki/entitlement-host/1234567890123456789-key.pem` and `/etc/pki/entitlement-host/1234567890123456789.pem`, the certificate serial number is `1234567890123456789`.

5. Exit the debug session.

    ```sh
    exit
    exit
    ```
    {: pre}

6. Create a ConfigMap file named `nvidia-driver-repo-config.yaml` with the following content. Replace `NAMESPACE-GPU` with the namespace where the GPU driver is installed, `BASEURL` with the base URL you retrieved, and replace both instances of `CERT-SERIAL` with your certificate serial number.

    ```yaml
    apiVersion: v1
    kind: ConfigMap
    metadata:
      name: nvidia-driver-repo-config
      namespace: NAMESPACE-GPU
    data:
      rhel9.repo: |
        [ibm-rhel-9-for-x86_64-appstream-eus-rpms]
        name = Red Hat Enterprise Linux 9 for x86_64 - AppStream - Extended Update Support (RPMs)
        baseurl = BASEURL/pulp/repos/customer/Library/content/eus/rhel9/9.6/x86_64/appstream/os
        enabled = 1
        gpgcheck = 1
        gpgkey = file:///etc/pki/rpm-gpg/RPM-GPG-KEY-redhat-release
        sslverify = 1
        sslcacert = /etc/rhsm-host/ca/katello-server-ca.pem
        sslclientkey = /etc/pki/entitlement-host/CERT-SERIAL-key.pem
        sslclientcert = /etc/pki/entitlement-host/CERT-SERIAL.pem
        metadata_expire = 1
        enabled_metadata = 0
    ```
    {: codeblock}

7. Apply the ConfigMap to your cluster.

    ```sh
    oc apply -f nvidia-driver-repo-config.yaml
    ```
    {: pre}

8. Edit the cluster policy to add the ConfigMap to the `repoConfig` section.

    ```sh
    oc edit clusterpolicy
    ```
    {: pre}

9. Add the `configMapName` field to the `spec.repoConfig` section with the name of your ConfigMap.

    ```yaml
    spec:
      ...
      repoConfig:
        configMapName: nvidia-driver-repo-config
      ...
    ```
    {: codeblock}

10. Delete the NVIDIA driver daemonset pods to cycle them and apply the new configuration.

    ```sh
    oc delete po nvidia-driver-daemonset-*
    ```
    {: pre}

After the pods restart, the NVIDIA GPU Operator can access the required EUS repositories and successfully install the GPU drivers on your RHEL 9 worker nodes.
