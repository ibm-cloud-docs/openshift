---

copyright:
  years: 2026, 2026
lastupdated: "2026-11-05"


keywords: openshift, {{site.data.keyword.openshiftlong_notm}}, update cluster components, Fluentd, Ingress ALB, managed add-ons, update add-ons

subcollection: openshift

content-type: howto

---

{{site.data.keyword.attribute-definition-list}}


# Updating cluster components and managed add-ons
{: #update-components}

Your {{site.data.keyword.openshiftlong_notm}} cluster comes with components, such as Ingress, that are installed automatically when you provision the cluster. By default, these components are updated automatically by IBM. However, you can disable automatic updates for some components and manually update them separately from the master and worker nodes.
{: shortdesc}

## Understanding cluster components
{: #components}

What default components can I update separately from the cluster?
:   You can optionally disable automatic updates for the following components:
    * [Fluentd for logging](#logging-up)
    * [Ingress application load balancer (ALB)](#alb)

Are there components that I can't update separately from the cluster?
:   Yes. Your cluster is deployed with the following managed components and associated resources that can't be changed, except to scale pods or edit configmaps for certain performance benefits. If you try to change one of these deployment components, their original settings are restored on a regular interval when they are updated with the cluster master. However, note that resources that you create that are associated with these components, such as Calico network policies that you create to be implemented by the Calico deployment components, are not updated.

    * `calico` components
    * `coredns` components
    * `ibm-cloud-provider-ip`
    * `ibm-file-plugin`
    * `ibm-keepalived-watcher`
    * `ibm-master-proxy`
    * `ibm-storage-watcher`
    * 
    * `metrics-server`
    * `olm-operator` and `catalog` components
    * `vpn`

Can I install other plug-ins or add-ons than the default components?
:   Yes. {{site.data.keyword.openshiftlong_notm}} provides other plug-ins and add-ons that you can choose from to add capabilities to your cluster. For example, you might want to enable IBM-managed add-ons in your cluster. You must update these add-ons separately by following the steps to [update managed add-ons](/docs/openshift?topic=openshift-managed-addons#updating-managed-add-ons).

## Managing automatic updates for Fluentd
{: #logging-up}

When you create a logging configuration for a source in your cluster to forward to an external server, a Fluentd component is created in your cluster. To change your logging or filter configurations, the Fluentd component must be at the latest version. By default, automatic updates to the component are enabled.
{: shortdesc}

To run the following commands, you must have the [**Administrator** {{site.data.keyword.cloud_notm}} IAM platform access role](/docs/openshift?topic=openshift-iam-platform-access-roles) for the cluster.

You can manage automatic updates of the Fluentd component in the following ways.

* Check whether automatic updates are enabled by running the `ibmcloud oc logging autoupdate get --cluster CLUSTER` [command](/docs/openshift?topic=openshift-kubernetes-service-cli#logging-autoupdate-get-cli).
* Disable automatic updates by running the `ibmcloud oc logging autoupdate disable` [command](/docs/openshift?topic=openshift-kubernetes-service-cli#logging-autoupdate-disable-cli).
* If automatic updates are disabled, but you need to change your configuration, you have two options:
    * Turn on automatic updates for your Fluentd pods.
        ```sh
        ibmcloud oc logging autoupdate enable --cluster CLUSTER
        ```
        {: pre}

    * Force a one-time update when you use a logging command that includes the `--force-update` option. Your pods update to the latest version of the Fluentd component, but Fluentd does not update automatically going forward.
        Example command

        ```sh
        ibmcloud oc logging config update --cluster CLUSTER --id LOG-CONFIG-ID --type LOG-TYPE --force-update
        ```
        {: pre}

## Managing automatic updates for Ingress ALBs
{: #alb}

Control when the Ingress application load balancer (ALB) component is updated. For information about keeping ALBs up-to-date, see [Managing the Ingress ALB lifecycle](/docs/openshift?topic=openshift-ingress-about-roks4).
{: shortdesc}

## Updating managed add-ons
{: #addons-update}

Managed {{site.data.keyword.openshiftlong_notm}} cluster add-ons are an easy way to enhance your cluster with open-source capabilities. The version of the open-source tool that you add to your cluster is tested by IBM and approved for use in {{site.data.keyword.openshiftlong_notm}}. To update managed add-ons that you enabled in your cluster to the latest versions, see [Updating managed add-ons](/docs/openshift?topic=openshift-managed-addons#updating-managed-add-ons).

## Next steps
{: #update-components-next}

Return to [Updating clusters, worker nodes, and cluster components](/docs/openshift?topic=openshift-update) to confirm that you completed each part of the update.

## Related links
{: #update-components-related}

* [Updating managed add-ons](/docs/openshift?topic=openshift-managed-addons#updating-managed-add-ons)
* [Your responsibilities with using {{site.data.keyword.openshiftlong_notm}}](/docs/openshift?topic=openshift-responsibilities_iks)
