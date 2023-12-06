---

copyright: 
  years: 2023, 2023
lastupdated: "2023-12-06"

keywords: portworx, openshift

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}


# Installing Autopilot for Portworx
{: #storage-portworx-autopilot}

Autopilot allows you to specify monitoring conditions in your cluster to react and apply changes when certain conditions occur without direct intervention.
{: shortdesc}

Before you can confiure autopilot: 

- [Install Portworx](/docs/openshift?topic=openshift-storage_portworx_deploy)

- Enable a Prometheus instance in your cluster

 - [Access your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-access_cluster).

 - Edit the `storageCluster` resource to enable prometheus.

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
    {: pre}

 - Verify that the Prometheus instance has been created.

    ```sh
    kubectl get service -n kube-system prometheus
    ```
    {: pre}

    ```sh
    NAME            TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)    AGE
    px-prometheus   ClusterIP   172.21.157.200   <none>        9090/TCP   19h
    ```
    {: screen}

    Note that `http://prometheus:9090` becomes the default Prometheus endppint that Portworx will use when you configure autopilot.
    {: note}

## Installing autopilot
{: #storage-portworx-install-ap}

1. Download and save the [Autopilot resources](https://install.portworx.com/?comp=autopilot){: external} as a `yaml` file and apply them to your cluster. 


    ```sh
    kuectl apply -f autopilot
    ```
    {: pre}

**Optional**: If you are installing Autopilot with the `PX-Security` using the Operator, you must modify the `StorageCluster` yaml. Add the following `PX_SHARED_SECRET` env var to the autopilot section:

    ```yaml
    env:
    - name: PX_SHARED_SECRET
    valueFrom:
    secretKeyRef:
    key: apps-secret
    name: px-system-secrets
    ```
    {: pre}

## Creating Rules
{: #storage-px-create-rules}

Now that you have installed autopilot in your cluster, refer to the [Portworx](https://docs.portworx.com/portworx-enterprise/operations/operate-kubernetes/autopilot/how-to-use/working-with-rules){: external} documentation on how to create custom rules and actions for your autopilot configuration.








