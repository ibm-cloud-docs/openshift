---

copyright: 
  years: 2023, 2024
lastupdated: "2024-07-18"


keywords: portworx, <containers>containers</containers><openshift>openshift</openshift>, autopilot

subcollection: <containers>containers</containers><openshift>openshift</openshift>


---

{{site.data.keyword.attribute-definition-list}}


# Installing Autopilot for Portworx
{: #storage-portworx-autopilot}

Autopilot allows you to specify monitoring conditions in your cluster to react and apply changes when certain conditions occur without direct intervention. For more information about Autopilot, see the [Portworx documentation](https://docs.portworx.com/portworx-enterprise/operations/operate-kubernetes/autopilot){: external}
{: shortdesc}

## Prerequisites
{: #autopilot-prereqs}


1. [Install Portworx](/docs/<containers>containers</containers><openshift>openshift</openshift>?topic=<containers>containers</containers><openshift>openshift</openshift>-storage_portworx_deploy).

1. <containers>[Log in to your account. If applicable, target the appropriate resource group. Set the context for your cluster.](/docs/containers?topic=containers-access_cluster)</containers><openshift>[Access your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-access_cluster).</openshift>

1. Autopilot requires a running Prometheus instance in your cluster. To set up Prometheus, see [Monitor your Portworx cluster](https://docs.portworx.com/portworx-enterprise/operations/operate-kubernetes/monitoring){: external}.

1. Make sure Prometheus is enabled, or edit your `storageCluster` resource and enable it by setting `enabled: true`.

    ```sh
    kubectl get service -n kube-system prometheus
    ```
    {: pre}

    ```sh
    monitoring:
    prometheus:
        alertManager:
        enabled: true
        enabled: true
        exportMetrics: true
        resources: {}
    telemetry: {}
    ```
    {: screen}

1. Verify that the Prometheus instance has been created.

    ```sh
    kubectl get service -n kube-system prometheus
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
    kubectl apply -f autopilot.yaml
    ```
    {: pre}

## Creating Rules
{: #storage-px-create-rules}

Now that you have installed autopilot in your cluster, refer to the [Portworx documentation](https://docs.portworx.com/portworx-enterprise/operations/operate-kubernetes/autopilot/how-to-use/working-with-rules){: external} on how to create custom rules and actions for your autopilot configuration.








