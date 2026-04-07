---

copyright: 
  years: 2023, 2026
lastupdated: "2026-04-07"


keywords: portworx, openshift, autopilot

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}


# Installing Autopilot for Portworx
{: #storage-portworx-autopilot}

Autopilot lets you define monitoring conditions in your cluster and automatically apply changes when those conditions occur. For more information about Autopilot, see the [Portworx documentation](https://docs.portworx.com/portworx-enterprise/operations/scale-portworx-cluster/autopilot){: external}.
{: shortdesc}

## Prerequisites
{: #autopilot-prereqs}


1. [Install Portworx](/docs/openshift?topic=openshift-storage_portworx_deploy).

1. [Access your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-access_cluster).

1. Autopilot requires a running Prometheus instance in your cluster. To set up Prometheus, see [Monitor your Portworx cluster](https://docs.portworx.com/portworx-enterprise/operations/observability){: external}.

1. Make sure that Prometheus is enabled. If it is not enabled, edit your `storageCluster` resource and set `enabled: true` in the Prometheus configuration.

    Verify that the Prometheus service exists:
    ```sh
    oc get service -n kube-system prometheus
    ```
    {: pre}

    Example Prometheus configuration:
    ```yaml
    monitoring:
      prometheus:
        alertManager:
          enabled: true
        enabled: true
        exportMetrics: true
        resources: {}
      telemetry: {}
    ```
    {: codeblock}

1. Verify that the Prometheus instance has been created.

    ```sh
    oc get service -n kube-system prometheus
    ```
    {: pre}

    ```sh
    NAME            TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)    AGE
    px-prometheus   ClusterIP   172.21.157.200   <none>        9090/TCP   19h
    ```
    {: screen}

    Note that `http://prometheus:9090` is the default Prometheus endpoint when Autopilot is enabled.
    {: note}

## Installing Autopilot
{: #storage-portworx-install-ap}

1. Download and save the [Autopilot resources](https://install.portworx.com/?comp=autopilot){: external} to a file called `autopilot.yaml`.

1. **Optional**: If you are installing Autopilot with `PX-Security`, you must modify the `storageCluster` to add the `PX_SHARED_SECRET` environment variable to the autopilot section.

    ```yaml
    env:
    - name: PX_SHARED_SECRET
    valueFrom:
    secretKeyRef:
    key: apps-secret
    name: px-system-secrets
    ```
    {: pre}

1. Deploy Autopilot to your cluster. 

    ```sh
    oc apply -f autopilot.yaml
    ```
    {: pre}

## Creating Rules
{: #storage-px-create-rules}

Now that you have installed Autopilot in your cluster, see the [Portworx documentation](https://docs.portworx.com/portworx-enterprise/operations/scale-portworx-cluster/autopilot/how-to-use/working-with-rules){: external} to create custom rules and actions for your Autopilot configuration.
