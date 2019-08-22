---

copyright:
  years: 2014, 2019
lastupdated: "2019-07-31"

keywords: openshift, roks, rhoks, rhos

subcollection: openshift

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"} 
{:codeblock: .codeblock}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:download: .download}
{:preview: .preview}

# Limitazioni del servizio
{: #openshift_limitations}

Riesamina le seguenti limitazioni per {{site.data.keyword.openshiftlong}}. Per le limitazioni generali del prodotto, come le chiamate API o il numero di pod per ogni nodo di lavoro, vedi [Limitazioni del servizio {{site.data.keyword.containerlong_notm}}](/docs/containers?topic=containers-ibm-cloud-kubernetes-service-technology#tech_limits).
{: shortdesc}

## Cluster
{: #oc_limits_cluster}

*   Puoi creare solo i cluster standard e non i cluster gratuiti. Puoi invece creare un cluster Kubernetes gratuito e ridistribuire quindi nel tuo cluster OpenShift le applicazioni che provi nel cluster Kubernetes.
*   Le [ubicazioni](/docs/openshift?topic=openshift-regions-and-zones) sono disponibili in tutte e sei le aree metropolitane multizona nel mondo: Dallas, Francoforte, Londra, Sydney, Tokyo e Washington DC.
*   Non puoi creare un cluster con nodi di lavoro che eseguono più sistemi operativi, come OpenShift su Red Hat Enterprise Linux e Kubernetes della community su Ubuntu.

## Archiviazione
{: #oc_limits_storage}

Sono supportate le archiviazioni di file, blocchi e oggetti cloud di {{site.data.keyword.cloud_notm}}. L'archiviazione definita dal software (o SDS, software-defined storage) Portworx non è supportata.

A causa del modo in cui l'archiviazione file NFS {{site.data.keyword.cloud_notm}} configura le autorizzazioni utente di Linux, potresti riscontrare degli errori quando utilizzi l'archiviazione file. In tal caso, potresti dover configurare i [Vincoli del contesto di sicurezza OpenShift ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://docs.openshift.com/container-platform/3.11/admin_guide/manage_scc.html) o utilizzare un tipo di archiviazione diverso.

## Metriche 
{: #oc_limits_metrics}

L'Alert Manager [Prometheus integrato](/docs/openshift?topic=openshift-openshift_apps#openshift_access_oc_services) include due regole che vengono visualizzate come avvisi attivi in uno stato `FIRING`: `KubeControllerManagerDown` e `KubeSchedulerDown`. Questi componenti sono gestiti nel master cluster, quindi puoi ignorare questi avvisi.

Avviso di esempio:
```
alert: KubeControllerManagerDown
expr: absent(up{job="kube-controllers"}
  == 1)
for: 15m
labels:
  severity: critical
annotations:
  message: KubeControllerManager has disappeared from Prometheus target discovery.
```
{: screen}
