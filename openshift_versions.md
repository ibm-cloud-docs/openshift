---

copyright:
  years: 2014, 2020
lastupdated: "2020-04-20"

keywords: openshift, roks, rhoks, rhos, version, rhel, update, upgrade

subcollection: openshift

---

{:codeblock: .codeblock}
{:deprecated: .deprecated}
{:download: .download}
{:external: target="_blank" .external}
{:faq: data-hd-content-type='faq'}
{:gif: data-image-type='gif'}
{:help: data-hd-content-type='help'}
{:important: .important}
{:new_window: target="_blank"}
{:note: .note}
{:pre: .pre}
{:preview: .preview}
{:screen: .screen}
{:shortdesc: .shortdesc}
{:support: data-reuse='support'}
{:table: .aria-labeledby="caption"}
{:tip: .tip}
{:troubleshoot: data-hd-content-type='troubleshoot'}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:tsSymptoms: .tsSymptoms}


# Version information and update actions
{: #openshift_versions}

Review information about the supported OpenShift versions for {{site.data.keyword.openshiftlong}} clusters.
{: shortdesc}

For more information about the OpenShift  and Kubernetes project versions, review the following information.
* [OpenShift 4.3 release notes overview](https://docs.openshift.com/container-platform/4.3/release_notes/ocp-4-3-release-notes.html){: external}
* [OpenShift 3.11 release notes overview](https://docs.openshift.com/container-platform/3.11/release_notes/index.html){: external}
* [Kubernetes changelog](https://github.com/kubernetes/kubernetes/tree/master/CHANGELOG){: external}

## Update types
{: #openshift_update_types}

Your Red Hat OpenShift on IBM Cloud cluster has three types of updates: major, minor, and patch. As updates become available, you are notified when you view information about the cluster master or worker nodes, such as with the `ibmcloud oc cluster ls`, `cluster get`, `worker ls`, or `worker get` commands.
{:shortdesc}

|Update type|Examples of version labels|Updated by|Impact
|-----|-----|-----|-----|
|Major|3.x.x|You|Operation changes for clusters, including scripts or deployments.|
|Minor|x.11.x|You|Operation changes for clusters, including scripts or deployments.|
|Patch|x.x.104_1507|IBM and you|OpenShift patches, as well as other {{site.data.keyword.cloud_notm}} Provider component updates such as security and operating system patches. IBM updates masters automatically, but you apply patches to worker nodes. See more about patches in the following section.|
{: caption="Impacts of OpenShift updates" caption-side="top"}

<dl>
  <dt>**Major and minor updates (3.11)**</dt>
  <dd><p>First, [update your master node](/docs/openshift?topic=openshift-update#master) and then [update the worker nodes](/docs/openshift?topic=openshift-update#worker_node). Worker nodes cannot run an OpenShift major or minor version that is greater than the masters.</p><p class="note">If you use an `oc` or `kubectl` CLI version that does match at least the `major.minor` version of your clusters, you might experience unexpected results. Make sure to keep your cluster and [CLI versions](/docs/openshift?topic=openshift-openshift-cli#cli_oc) up-to-date.</p></dd>
  <dt>**Patch updates (x.x.104_1507)**</dt>
  <dd><p>Changes across patches are documented in the [Version changelog](/docs/openshift?topic=openshift-openshift_versions). Master patches are applied automatically, but you initiate worker node patches updates. Worker nodes can also run patch versions that are greater than the masters. As updates become available, you are notified when you view information about the master and worker nodes in the {{site.data.keyword.cloud_notm}} console or CLI, such as with the following commands: `ibmcloud oc cluster ls`, `cluster get`, `worker ls`, or `worker get`.</p>
  <p>Patches can be for worker nodes, masters, or both.</p>
  <ul><li>**Worker node patches**: Check monthly to see whether an update is available, and use the `ibmcloud oc worker update` [command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_update) or the `ibmcloud oc worker reload` [command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_reload) to apply these security and operating system patches. During an update or reload, your worker node machine is reimaged, and data is deleted if not [stored outside the worker node](/docs/openshift?topic=openshift-storage_planning#persistent_storage_overview).</li>
  <li>**Master patches**: Master patches are applied automatically over the course of several days, so a master patch version might show up as available before it is applied to your master. The update automation also skips clusters that are in an unhealthy state or have operations currently in progress. Occasionally, IBM might disable automatic updates for a specific master fix pack, as noted in the changelog, such as a patch that is only needed if a master is updated from one minor version to another. In any of these cases, you can choose to safely use the `ibmcloud oc cluster master update` [command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_cluster_update) yourself without waiting for the update automation to apply.</li></ul></dd>
</dl>

<br />


## OpenShift versions
{: #version_types}

Red Hat OpenShift on IBM Cloud supports the following versions of OpenShift. The worker node operating system is Red Hat Enterprise Linux 7.

* **Default**: 3.11, which includes Kubernetes 1.11
* **Latest**: 4.3, which includes Kubernetes 1.16

To check the Kubernetes server version of a cluster, log in to the cluster and run the following command.

```
oc version
```
{: pre}

Example output:
```
Client Version: v3.11.154
Kubernetes Version: v1.11.0+d4cacc0
```
{: screen}

## Release history
{: #openshift_release_history}

The following table records Red Hat OpenShift on IBM Cloud version release history. You can use this information for planning purposes, such as to estimate general time frames when a certain release might become unsupported. After the Red Hat OpenShift community releases a version update, the IBM team begins a process of hardening and testing the release for {{site.data.keyword.containerlong_notm}} environments. Availability and unsupported release dates depend on the results of these tests, community updates, security patches, and technology changes between versions. Plan to keep your cluster master and worker node version up-to-date.
{: shortdesc}

Red Hat OpenShift on IBM Cloud was first generally available with OpenShift version 3.11, which includes the Kubernetes project version 1.11. Dates that are marked with a dagger (`†`) are tentative and subject to change.
{: important}

<table summary="This table shows the release history for Red Hat OpenShift on IBM Cloud.">
<caption>Release history for Red Hat OpenShift on IBM Cloud.</caption>
<col width="20%" align="center">
<col width="20%">
<col width="30%">
<col width="30%">
<thead>
<tr>
<th>Supported?</th>
<th>OpenShift / Kubernetes version</th>
<th>Red Hat OpenShift on IBM Cloud<br>release date</th>
<th>Red Hat OpenShift on IBM Cloud<br>unsupported date</th>
</tr>
</thead>
<tbody>
<tr>
  <td><img src="images/icon_beta.png" align="left" width="28" style="width:28px;" alt="This version is supported as a beta."/></td>
  <td>4.3 / 1.16</td>
  <td>20 Apr 2020 at 10:58 UTC</td>
  <td>`†`</td>
</tr>
<tr>
  <td><img src="images/checkmark-filled.png" align="left" width="32" style="width:32px;" alt="This version is supported."/></td>
  <td>3.11 / 1.11</td>
  <td>1 Aug 2019 at 0:00 UTC</td>
  <td>`†`</td>
</tr>
</tbody>
</table>


<br />


## OpenShift 4.3
{: #ocp43}

<p><img src="images/logo_redhat.png" alt="Red Hat OpenShift icon" width="16" style="width:16px; border-style: none"/> <img src="images/certified_kubernetes_1x16.png" style="padding-right: 10px;" align="left" alt="This badge indicates Kubernetes version 1.16 certification for Red Hat OpenShift on IBM Cloud."/> Red Hat OpenShift on IBM Cloud is a Certified Kubernetes product for version 1.16 under the CNCF Kubernetes Software Conformance Certification program. _Kubernetes® is a registered trademark of The Linux Foundation in the United States and other countries, and is used pursuant to a license from The Linux Foundation._</p> 

With the release of OpenShift Container Platform 4.3, you get a new experience and capabilities for managing your cluster and its workloads. For more information, see the [OpenShift blog](https://blog.openshift.com/introducing-red-hat-openshift-4-3-to-enhance-kubernetes-security/){: external}.
{: shortdesc}

To create a 4.3 cluster, [try out the tutorial](/docs/openshift?topic=openshift-openshift_tutorial). You cannot update an existing version 3.11 cluster to a 4.3 cluster, but you can [migrate workloads to 4.3 clusters](#ocp-3-to-4-migration).

Review the following benefit highlights when you use version 4.3 clusters.
*   Ability to use your own [Operators](/docs/openshift?topic=openshift-operators) or operators that are provided by the OperatorHub to package and deploy services for your cluster.
*   New [OpenShift web console experience](/docs/openshift?topic=openshift-openshift_tutorial#openshift_oc_console) that reorganizes your cluster resources and workflows into two perspectives for the **Administrator** and **Developer**.
*   Update of the underlying Kubernetes API to 1.16 so that you can use new capabilities such as extensibility for core Kubernetes APIs, an updated `kubectl` experience, cluster lifecycle stability enhancements, support for projects such as `kustomize`, persistent local volumes, and custom resource and operator support.
*   [Ingress controllers are integrated into the Ingress Operator](/docs/openshift?topic=openshift-ingress-about-roks4) so that you can use routers to proxy app requests instead of application load balancers (ALBs).

For more information, check out the [comparison table between supported features of 3.11 and 4.3](/docs/openshift?topic=openshift-cs_ov#3.11_vs_4.3) or review the [service limitations](/docs/openshift?topic=openshift-openshift_limitations#ocp4_limitations).

<br />


## Migrating from version 3.11 to 4.3 clusters
{: #ocp-3-to-4-migration}

You cannot update your Red Hat OpenShift on IBM Cloud cluster from version 3.11 to 4.3. Instead, you can use the [OpenShift Migration Operator](https://github.com/fusor/mig-operator){: external} to migrate your workloads from a 3.11 source cluster to a 4.3 destination cluster.
{: shortdesc}

<p class="important">Keep in mind the following limitations to the migration operator.<ul><li>The OpenShift Migration Operator is a community tool that you choose to use, and is not supported by IBM or Red Hat.</li><li>You must [complete the prerequisites](#ocp3to4-migrate-prereqs) to prepare the resources in your {{site.data.keyword.cloud_notm}} account.</li><li>The instructions are intended for version 1.0.1 of the migration operator and for 3.11 source and 4.3 destination clusters. The instructions might not work with other versions.</li><li>The migration operator console does not work with Red Hat OpenShift on IBM Cloud. Instead, you can use the CLI to apply configuration files.</li><li>The migration operator is scoped to resources within a project or multiple projects. You cannot migrate resources that reside outside a project, such as cluster role bindings.</li><li>You cannot configure cross-origin resource sharing for 3.11 clusters.</li></ul></p>

**How does the migration operator work?**<br>
The migration operator is a set of custom resources that use [Velero](https://velero.io/){: external} and [Restic](https://restic.net/){: external} open source projects to back up your cluster resources in a project to an {{site.data.keyword.cos_full_notm}} service instance. Then, the operator restores the project resources on the destination cluster. For more information, see the [OpenShift tech topic](https://www.openshift.com/learn/topics/migration){: external} and a [conceptual overview of the architecture](https://github.com/fusor/mig-operator/blob/master/docs/usage/2.md).

For an architectural overview of the custom resource definitions that are applied in the clusters, see [CRD Architecture](https://github.com/fusor/mig-operator/blob/master/docs/usage/5.md#51-crd-architecture){: external}.

**Can I try out the migration with a sample app?**<br>
Yes, the open source documentation includes two examples of [MSSQL](https://github.com/fusor/mig-operator/blob/master/docs/usage/3.md){: external} and [Sock Shop](https://github.com/fusor/mig-operator/blob/master/docs/usage/4.md){: external} apps. Keep in mind that the migration operator console is not supported in Red Hat OpenShift on IBM Cloud, so you can use the CLI instead.

**If the console does not work, where are instructions to apply the configuration files myself?**<br>
After you complete the [prerequisites](#ocp3to4-migrate-prereqs), you can use the following [steps](#ocp3to4-migrate-source) as an example to configure your source and destination clusters for the migration. Remember that the instructions are intended for version 1.0.1 of the migration operator and for 3.11 source and 4.3 destination clusters. The instructions might not work with other versions, and are not updated in sync with the [open source community project docs](https://github.com/fusor/mig-operator/tree/master/docs/usage){: external}.

### Prerequisites
{: #ocp3to4-migrate-prereqs}

Before you migrate your workloads from an OpenShift version 3.11 cluster to a version 4.3 cluster, make sure that you have the following resources.
{: shortdesc}

1.  Identify your source Red Hat OpenShift on IBM Cloud version 3.11 cluster.
2.  [Create](/docs/openshift?topic=openshift-clusters) a destination Red Hat OpenShift on IBM Cloud version 4.3 cluster.
    
    For multizone clusters, both the source and destination clusters must be in the same zones. Also, to migrate persistent storage from the source cluster, both the source and destination clusters must be in the same zone.
    {: important}

3.  Prepare an [{{site.data.keyword.cos_full_notm}}](https://cloud.ibm.com/objectstorage/){: external} bucket for the migration backup and restore. 
    1.  Identify an existing or create an {{site.data.keyword.cos_short}} instance. When you create the instance, make sure to select **Include HMAC Credential**. For more information, see [Preparing your object storage service instance](/docs/openshift?topic=openshift-object_storage#create_cos_service).
    2.  [Create a bucket](/docs/cloud-object-storage-infrastructure?topic=cloud-object-storage-infrastructure-storing-and-retrieving-data#buckets) in your {{site.data.keyword.cos_short}} instance. Note the bucket's region **Location**, such as `us-south`.
    3.  Get your HMAC authentication credentials. From the {{site.data.keyword.cos_full_notm}} instance in the console, click **Service credentials** and find credentials that include a `cos_hmac_keys` object with `access_key_id` and `secret_access_key` values. If you do not have credentials with HMAC keys, click **New credential**. Create credentials that include HMAC credentials.
    4.  Get your {{site.data.keyword.cos_short}} instance endpoint for the same geography as your cluster is in. From the {{site.data.keyword.cos_full_notm}} instance in the console, click **Endpoints** and then select the location that you want to use. For example, `https://s3.us.cloud-object-storage.appdomain.cloud`.

### Step 1: Deploy the migration operator to the source cluster
{: #ocp3to4-migrate-source}

Deploy the migration operator to the source Red Hat OpenShift on IBM Cloud version 3.11 cluster.
{: shortdesc}

1.  For your version 3.11 cluster: [Access your OpenShift cluster](/docs/openshift?topic=openshift-access_cluster).
2.  Get the **Master URL** endpoint of the cluster. You use this endpoint later to set up the migration controller in the destination cluster.
    ```
    ibmcloud oc cluster get -c <cluster_name_or_ID>
    ```
    {: pre}

    Example output:
    ```
    Master URL: https://c100-e.<region>.containers.cloud.ibm.com:32xxx
    ```
    {: screen}
3.  Check that the app status that you want to migrate is **Running** before you migrate the app. If the status is not healthy, describe the pod for more information to troubleshoot the issue.
    ```
    oc get pods -n <project>
    ```
    {: pre}
4.  Deploy the migration operator to your source cluster. The configuration includes setting up an `openshift-migration` project; creating a custom resource definition for the migration operator; creating a service account, roles, and rolebindings for the resources; and creating the migration operator deployment.
    ```
    oc create -f https://raw.githubusercontent.com/fusor/mig-operator/master/deploy/non-olm/v1.0.1/operator.yml
    ```
    {: pre}
5.  Deploy the migration controller to your source cluster.
    1.  Get the migration controller configuration file from GitHub.
        ```
        curl https://raw.githubusercontent.com/fusor/mig-operator/master/deploy/non-olm/v1.0.1/controller-3.yml > migration-controller3.yaml
        ```
        {: pre}
    2.  Uncomment and replace the `mig_ui_cluster_api_endpoint` value with the cluster master URL that you previously retrieved.
    3.  Apply the configuration file to your cluster.
        ```
        oc apply -f migration-controller3.yaml
        ```
        {: pre}
6.  Verify that the migration operator, Restic, and Velero pods are in a **Running** status. The pods might take a few minutes to provision.
    ```
    oc get pods -n openshift-migration
    ```
    {: pre}
7.  Encode the service account token so that you can use it later in a secret in the destination cluster.
    ```
    oc sa get-token migration-operator -n openshift-migration | base64
    ```
    {: pre}

Now, you are ready to deploy the migration operator on the destination cluster.

### Step 2: Deploy the migration operator to the destination cluster
{: #ocp3to4-migrate-destination}

Deploy the migration operator to the destination Red Hat OpenShift on IBM Cloud version 4.3 cluster.
{: shortdesc}

1.  For your version 4.3 cluster: [Access your OpenShift cluster](/docs/openshift?topic=openshift-access_cluster).
2.  Deploy the migration operator to your destination cluster. The configuration includes setting up an `openshift-migration` project; creating a custom resource definition for the migration operator; creating a service account, roles, and rolebindings for the resources; and creating the migration operator deployment.
    ```
    oc create -f https://raw.githubusercontent.com/fusor/mig-operator/master/deploy/non-olm/v1.0.1/operator.yml
    ```
    {: pre}
3.  Deploy the migration controller to your destination cluster. You must deploy the controller to both clusters due to the limitation of the migration operator console not being supported in Red Hat OpenShift on IBM Cloud.
    1.  Get the migration controller configuration file from GitHub.
        ```
        curl https://raw.githubusercontent.com/fusor/mig-operator/master/deploy/non-olm/v1.0.1/controller-4.yml > migration-controller4.yaml
        ```
        {: pre}
    2.  Change the `migration_ui` value to `false` and save the file.
    3.  Apply the configuration file to your cluster.
        ```
        oc apply -f migration-controller4.yaml
        ```
        {: pre}
4.  Verify that the migration operator, Restic, and Velero pods are in a **Running** status. The pods might take a few minutes to provision.
    ```
    oc get pods -n openshift-migration
    ```
    {: pre}

### Step 3: Configure storage information in the destination cluster
{: #ocp3to4-storage-destination}

Both the version 3.11 source and 4.3 destination clusters have the migration operator installed. Now, you can set up the storage resources that are needed to backup and restore the data from the source cluster to the destination cluster.
{: shortdesc}

1.  Encode the {{site.data.keyword.cos_full_notm}} service credentials that you created in the [prerequisites](#ocp3to4-migrate-prereqs). Replace `<access_key_id>` and `<secret_access_key>` with your HMAC key values.

    Do not use `echo` when you base64 encode the values because `echo` injects an extra line character that causes the authentication to fail.
    {: tip}
    
    ```
    printf "<access_key_id>" | base64
    ```
    {: pre}

    ```
    printf "<secret_access_key>" | base64
    ```
    {: pre}
2.  Create a configuration file for a secret in your destination cluster that includes the encoded `<access_key_id>` and `<secret_access_key>` values.
    ```
    apiVersion: v1
    kind: Secret
    metadata:
      namespace: openshift-migration
      name: migstorage-creds
    type: Opaque
    data:
      aws-access-key-id: <encoded_access_key_id>
      aws-secret-access-key: <encoded_secret_access_key>
    ```
    {: codeblock}
3.  Create the secret.
    ```
    oc create -f migstorage-creds.yaml
    ```
    {: pre}
4.  Create a configuration file for a migration storage resource that has the information of your {{site.data.keyword.cos_full_notm}} configuration that you retrieved in the [prerequisites](#ocp3to4-migrate-prereqs).

    * **`<cos_bucket_name>`**: Replace with the name of your bucket in the {{site.data.keyword.cos_short}} instance, such as `migrate_bucket`.
    * **`<cos_endpoint>`** (twice): Replace with the public endpoint of your {{site.data.keyword.cos_short}} instance, such as `https://s3.us.cloud-object-storage.appdomain.cloud`.
    * **`<cos_bucket_region>`** (twice): Replace with the region of your {{site.data.keyword.cos_short}} instance that you can find in the endpoint, such as `us`.

    ```
    apiVersion: migration.openshift.io/v1alpha1
    kind: MigStorage
    metadata:
      labels:
        controller-tools.k8s.io: "1.0"
      name: migstorage-sample
      namespace: openshift-migration
    spec:
      backupStorageProvider: aws
      volumeSnapshotProvider: aws
      backupStorageConfig:
        awsBucketName: <cos_bucket_name>
        awsRegion: <cos_bucket_region>
        credsSecretRef:
          namespace: openshift-migration
          name: migstorage-creds
        awsPublicUrl: https://<cos_endpoint>
        awsS3Url: https://<cos_endpoint>
      volumeSnapshotConfig:
        awsRegion: <cos_bucket_region>
        credsSecretRef:
          namespace: openshift-migration
          name: migstorage-creds
    ```
    {: codeblock}
5.  Create the migration storage resource. 
    ```
    oc create -f migstorage-sample.yaml
    ```
    {: pre}
6.  Check that the migration controller successfully connected to your {{site.data.keyword.cos_short}} instance. In the `Status.Conditions` section, review the `Message`.
    ```
    oc -n openshift-migration describe migstorage migstorage-sample 
    ```
    {: pre}

    Example of a successful connection:
    ```
    Status:
      Conditions:
        Category:              Required
        Last Transition Time:  2020-01-20T18:49:07Z
        Message:               The storage is ready.
        Status:                True
        Type:                  Ready
    ```
    {: screen}

    Example of unsuccessful connection with a message to help you resolve the issue. For example, the following error is resolved by adding `https://` to the {{site.data.keyword.cos_short}} endpoint.
    ```
    Status:
      Conditions:
        Category:              Critical
        Last Transition Time:  2020-01-20T16:59:05Z
        Message:               The `backupStorageConfig` settings [PublicURL] not valid.
        Reason:                NotSupported
        Status:                True
        Type:                  InvalidBackupStorageSettings
    ```
    {: screen}

### Step 4: Configure the destination cluster with information about the source cluster
{: #ocp3to4-migrate-configure-destination}

To migrate workloads from the version 3.11 source cluster, the version 4.3 destination cluster must have credentials to the source cluster and additional information configured.
{: shortdesc}

1.  Create configuration file for a secret in your destination cluster that includes the encoded credentials to your source cluster that you retrieved in [Step 1](#ocp3to4-migrate-source).
    ```
    apiVersion: v1
    kind: Secret
    metadata:
      name: sa-token-remote
      namespace: openshift-migration
    type: Opaque
    data:
      saToken: <encoded_source_cluster_secret>
    ```
    {: codeblock}
2.  Create the secret.
    ```
    oc create -f sa-secret-source.yaml
    ```
    {: pre}
3.  Create a configuration file for a migration cluster resource that refers to the version 3.11 source cluster's master URL that you retrieved in [Step 1](#ocp3to4-migrate-source).
    ```
    apiVersion: migration.openshift.io/v1alpha1
    kind: MigCluster
    metadata:
      labels:
        controller-tools.k8s.io: "1.0"
      name: migcluster-remote
      namespace: openshift-migration
    spec:
      isHostCluster: false
      url: "<master_url_source_cluster>"
      serviceAccountSecretRef:
        name: sa-token-remote
        namespace: openshift-migration
    ```
    {: codeblock}
4.  Create the source migration cluster resource.
    ```
    oc create -f mig-cluster-source.yaml
    ```
    {: pre}  
5.  Check that the migration cluster resource in your version 4.3 destination cluster successfully connected to your source cluster. In the `Status.Conditions` section, review the `Message`.
    ```
    oc -n openshift-migration describe migcluster migcluster-remote
    ```
    {: pre}

    Example of a successful connection:
    ```
    Status:
      Conditions:
        Category:              Required
        Last Transition Time:  2020-01-20T18:49:07Z
        Message:               The cluster is ready.
        Status:                True
        Type:                  Ready
    ```
    {: screen}

6.  Create another migration cluster resource that identifies this version 4.3 destination cluster as the host cluster for the migration process.
    ```
    cat <<EOF | oc create -f -
    apiVersion: migration.openshift.io/v1alpha1
    kind: MigCluster
    metadata:
      labels:
        controller-tools.k8s.io: "1.0"
      name: migcluster-local
      namespace: openshift-migration
    spec:
      isHostCluster: true
    EOF
    ```
    {: codeblock}
7.  Create a configmap so that the migration process can move images from the source cluster's internal registry to the internal registry of the destination cluster.
    ```
    cat <<EOF | oc create -f -
    apiVersion: v1
    data:
      config.yaml: '{"imagePolicyConfig":{"internalRegistryHostname":"image-registry.openshift-image-registry.svc:5000"}}'
    kind: ConfigMap
    metadata:
      name: config
      namespace: openshift-apiserver
    EOF
    ```
    {: codeblock}

### Step 5: Run the migration
{: #ocp3to4-migrate-run}

To complete the migration process, create a sample plan to verify that what you want to migrate is included. Then, run the migration.
{: shortdesc}

1.  In your version 4.3 destination cluster, create a configuration file for a migration plan resource that identifies the previous migration cluster and storage resources that you created. Replace the `namespaces` values with all the projects that you want to migrate from the source to the destination cluster.
    ```
    apiVersion: migration.openshift.io/v1alpha1
    kind: MigPlan
    metadata:
      labels:
        controller-tools.k8s.io: "1.0"
      name: migplan-sample
      namespace: openshift-migration
    spec:

      srcMigClusterRef:
        name: migcluster-remote
        namespace: openshift-migration

      destMigClusterRef:
        name: migcluster-local
        namespace: openshift-migration

      migStorageRef:
        name: migstorage-sample
        namespace: openshift-migration

      namespaces:
      - <project_in_source_cluster>
      - <project_in_source_cluster>
    ```
    {: codeblock}
2.  Create the migration plan.
    ```
    oc create -f mig-plan.yaml
    ```
    {: pre}
3.  Verify that the resources that you want to migrate are included in the migration plan. Keep in mind that if you migrate persistent storage, your source and destination clusters must be in the zone. In the `Status.Conditions` section, review the `Message` fields.
    ```
    oc -n openshift-migration describe migplan migplan-sample
    ```
    {: pre}

    Example of a successful message.
    ```
    Message:               The migration plan is ready. 
    ```
    {: screen}

    Example of an unsuccessful message with troubleshooting information.
    ```
    Message:               Namespaces [migrate-hw] not found on the source cluster.
    ```
    {: screen}
4.  Create the migration that refers to the plan that you previously created.
    ```
    cat <<EOF | oc create -f -
    apiVersion: migration.openshift.io/v1alpha1
    kind: MigMigration
    metadata:
      labels:
        controller-tools.k8s.io: "1.0"
      name: migplan-sample
      namespace: openshift-migration
    spec:
      stage: false
      quiescePods: true
      keepAnnotations: true
      migPlanRef:
        name: migplan-sample
        namespace: openshift-migration
    EOF
    ```
    {: codeblock}

5.  Scale down pods on your version 3.11 source cluster because the migration cannot mount the backup pod storage while the app pods on your cluster run.

    Scaling down your app might cause downtime for your users. To prevent downtime, try creating a project that the migration plan does not include and deploy your app in that project.
    {: important}

    ```
    oc -n <deployment_config_name> scale --replicas=0 dc/<deployment_config_name>
    ```
    {: pre}

    ```
    oc -n <deployment_name> scale --replicas=0 dc/<deployment_name>
    ```
    {: pre}

6.  Check the status of your migration. The migration can take some time to complete.
    
    Check the status of all pods. If a pod is not in a **Running** status, describe the pod and check the `Events` section for errors.
    ```
    oc -n openshift-migration get pods
    ```
    {: pre}

    Check the logs of the pod to continue troubleshooting any errors.
    ```
    oc -n openshift-migration logs <migration-controller-pod>
    ```
    {: pre}

    In the `Status.Conditions` section, check the `Message` field for any `Errors`.
    ```
    oc -n openshift-migration describe migmigration <your-migration-name>
    ```
    {: pre}

    Do you see an error message similar to `Message: The migration has failed. See: Errors.`? Try [Debugging failed migrations](https://github.com/fusor/mig-operator/blob/master/docs/usage/5.md){: external}. For example, if you see a `Backup` error, check the Velero pod logs on the source cluster for more troubleshooting information.
    {: tip}

The migration is complete when the version 4.3 destination cluster includes the project and resources that you migrated.

