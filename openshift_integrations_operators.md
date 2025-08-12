---

copyright:
  years: 2014, 2025
lastupdated: "2025-08-12"


keywords: openshift, disconnect, airgap, olm, mirror

subcollection: openshift

---


{{site.data.keyword.attribute-definition-list}}


# Adding services by using Operators
{: #operators}

{{site.data.keyword.redhat_openshift_notm}} Operators provide additional functionality and extend the capabilities of a cluster. With operators, you can manage the lifecycle of the apps in your cluster, including third-party software and services that you integrate into your cluster from the [OperatorHub](https://operatorhub.io/){: external}. You can consistently install, update, and monitor system components by using operators or by making operators available to developers that work in specific projects or across projects.
{: shortdesc}

Operators are a convenient way to add services to your cluster from community, third-party, your own, or other providers. Keep in mind that you are responsible for managing additional charges; [understanding the operator's lifecycle](https://access.redhat.com/support/policy/updates/openshift_operators){: external}, support timeline, and how the services operate in your cluster at any point; and for ensuring that any operators you use are compatible with the cluster version. If you have issues with an operator, work with the appropriate provider to troubleshoot the issue.
{: note}


## Using Operators in clusters
{: #operators_4}

[Operators](https://docs.openshift.com/container-platform/4.18/operators/understanding/olm-what-operators-are.html){: external} are available in your cluster by default and can be used to package, deploy, and update your apps.
{: shortdesc}

Before you begin, [check the status](https://docs.openshift.com/container-platform/4.18/operators/admin/olm-status.html){: external} of any existing operators in your cluster. Resolve any issues before using operators to manage your apps. 

1. To use operators, follow the {{site.data.keyword.redhat_openshift_notm}} documentation.
    - [Adding Operators to a cluster](https://docs.openshift.com/container-platform/4.18/operators/admin/olm-adding-operators-to-cluster.html){: external}
    - [Deleting Operators from a cluster](https://docs.openshift.com/container-platform/4.18/operators/admin/olm-deleting-operators-from-cluster.html){: external}
    - [Creating applications from installed Operators](https://docs.openshift.com/container-platform/4.18/operators/user/olm-creating-apps-from-installed-operators.html){: external}
    - [Making your own custom Operator](https://github.com/operator-framework/community-operators/blob/master/docs/testing-operators.md#testing-operator-deployment-on-openshift){: external}.
        - For help creating custom Operators, see the [Operator SDK](https://docs.openshift.com/container-platform/4.18/operators/operator_sdk/osdk-about.html){: external} documentation, which includes a guide to build an operator that is based on a [Helm chart](https://docs.redhat.com/documentation/openshift_container_platform/4.7/html/operators/developing-operators){: external}.
        - To manage your custom Operator, see the [Operator Lifecycle Manager](https://docs.openshift.com/en/container-platform/4.18/operators/understanding/olm/olm-understanding-olm.html){: external} documentation.
2. Review any custom steps to install an operator in your cluster.
    - To set up an [OpenShift Container Platform Elasticsearch, Fluentd, and Kibana (EFK) stack](https://docs.redhat.com/documentation/openshift_container_platform/4.18/html/logging/index){: external}, see [installing the cluster logging operator](/docs/openshift?topic=openshift-health#oc_logging_operator).
3. If the operator uses a template with a build component that must pull an image from a private registry, the build might fail with an authentication error. To resolve this error, see [Build error due to image pull authentication](/docs/openshift?topic=openshift-ts-app-build-img-pull).

## Adding the IBM Operator Catalog source to OperatorHub
{: #operators_catalog}

You can add the IBM Operator Catalog as a source on OperatorHub by configuring a `CatalogSource`.

1. Create a YAML file specifying the catalog source. 
    ```yaml
    apiVersion: operators.coreos.com/v1alpha1
    kind: CatalogSource
    metadata:
      name: ibm-operator-catalog
      namespace: openshift-marketplace
    spec:
      displayName:  "IBM Operator Catalog"
      publisher: IBM
      sourceType: grpc
      image: icr.io/cpopen/ibm-operator-catalog:latest
      updateStrategy:
        registryPoll:
          interval: 45m
    ```
    {: codeblock}

2. Apply the file to the cluster.
    ```sh
    kubectl apply -f <file_name>
    ```
    {: pre}


## Disabling OperatorHub and mirroring catalog source images to `icr.io`
{: #mirror-operatorhub}

You can disable and mirror the OperatorHub catalog source images by following the [Operator Lifecycle Manager (OLM) on restricted networks documentation from Red Hat](https://docs.openshift.com/container-platform/4.18/operators/admin/olm-restricted-networks.html){: external}. 
{: shortdesc}

Mirroring OperatorHub is required to use operators with clusters that have private-only network configurations.
{: important}

To understand why you might disable and mirror the catalog, consider the following scenarios.
- **For private clusters:** The Red Hat-provided OperatorHub source images require access to the `registry.redhat.io` and `quay.io` registries. If your cluster runs on a restricted network, such as in a VPC without a public gateway or classic worker nodes on only a private VLAN, these images are not accessible
- You want to restrict the catalog content that is available to your cluster users in OperatorHub.

Before you begin

- Make sure that you have the **Manager** service role to the cluster in all namespaces in {{site.data.keyword.cloud_notm}} IAM.
- [Install the `opm` command-line interface](https://docs.openshift.com/container-platform/4.18/cli_reference/opm/cli-opm-ref.html){: external}, including its prerequisite tools such as `podman`.
- Have a Red Hat account with credentials to pull images from the `registry.redhat.io` and `quay.io` registries, or use the [default global pull secret](/docs/openshift?topic=openshift-registry#cluster_global_pull_secret).

To disable and mirror the OperatorHub source images:
1. Disable the catalog sources as described in [Disabling the default OperatorHub sources](https://docs.openshift.com/container-platform/4.18/operators/admin/olm-restricted-networks.html#olm-restricted-networks-operatorhub_olm-restricted-networks){: external}.
2. **Optional**: Prune the catalog index to a select list of packages as described in [Pruning an index image](https://docs.openshift.com/container-platform/4.18/operators/admin/olm-restricted-networks.html#olm-pruning-index-image_olm-restricted-networks){: external}. You might prune the catalog to control what images your cluster users can install and to reduce the size of the images in your registry.
3. Mirror the catalog to your compatible registry, such as {{site.data.keyword.registrylong_notm}}, as described in [Mirroring an Operator catalog](https://docs.openshift.com/container-platform/4.18/operators/admin/olm-restricted-networks.html#olm-mirror-catalog_olm-restricted-networks){: external}.


## Getting support for Operators
{: #operator_support}

You can open an {{site.data.keyword.cloud_notm}} [support ticket](/docs/openshift?topic=openshift-get-help) for issues about any operator installed from Operator Hub. If IBM support cannot resolve the issue or if the issue originates from outside of the IBM service, an issue is opened with {{site.data.keyword.redhat_openshift_notm}}.


## Operator FAQ
{: #operator_faq}

Which Operators in the OpenShift OperatorHub are available for use in the {{site.data.keyword.openshiftlong_notm}} service? 
:   By default, {{site.data.keyword.openshiftlong_notm}} includes the standard {{site.data.keyword.redhat_openshift_notm}} OperatorHub and its contents. For a list of Operators that are unsupported, see [Unsupported features and operators in {{site.data.keyword.openshiftlong_notm}}](/docs/openshift?topic=openshift-limitations#not-supported-features-table).

Is OpenShift Data Foundation available for Red Hat OpenShift on IBM Cloud?
:   Yes. However, ODF for IBM Cloud is available as a cluster add-on. There is no support for deploying the ODF operator via OperatorHub. For more information on the ODF add-on for storage, see [Understanding OpenShift Data Foundation](/docs/openshift?topic=openshift-ocs-storage-prep).

Are the IBM Cloud service level agreement terms impacted by the availability of OperatorHub items? 
:   No. All OpenShift OperatorHub installable items are outside of the control of IBM Cloud and therefore do not impact the IBM Cloud service level agreement terms. If you install an Operator from OperatorHub and it impacts the viability of your cluster, IBM is not responsible and you cannot make a claim against the service level agreement. See the service level agreement [terms](https://www.ibm.com/support/customer/csol/terms/?id=i126-9268&lc=en#detail-document){: external} for more information.

Who is responsible for the security of the operators that are available as a part of the OperatorHub? 
:   Responsibility for the security of an operator depends on the operator type. For information on operator types, see [About OperatorHub](https://docs.openshift.com/container-platform/4.14/operators/understanding/olm-understanding-operatorhub.html#olm-operatorhub-overview_olm-understanding-operatorhub){: external}. Security for `Red Hat`, `Certified`, and `Red Hat Marketplace` operators is maintained by {{site.data.keyword.redhat_openshift_notm}}. {{site.data.keyword.redhat_openshift_notm}} is not responsible for security for `Community` or `Custom` operators, which are maintained and supported outside of Red Hat. Note that you can filter out different operator types in OperatorHub, or you can set the spec section of your OperatorHub configuration file to exclude certain operators, such as in the example below. 
    ```yaml
    Spec:
      Sources:
        Disabled:  true
        Name:      community-operators
    ```
    {: codeblock}
