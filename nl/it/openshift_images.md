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
{:download: .download}
{:preview: .preview}

# Creazione di immagini per le tue applicazioni 
{: #openshift-images}

I cluster {{site.data.keyword.openshiftlong}} includono un registro interno per creare, distribuire e gestire immagini del contenitore localmente. Per un registro privato per gestire e controllare l'accesso alle immagini nell'ambito della tua azienda, puoi anche configurare il tuo cluster per utilizzare {{site.data.keyword.registrylong}}.
{: shortdesc}

## Utilizzo del registro interno
{: #openshift_internal_registry}

I cluster OpenShift sono configurati per impostazione predefinita con un registro interno. Per ulteriori informazioni, vedi la [documentazione di OpenShift ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://docs.openshift.com/container-platform/3.11/install_config/registry/index.html#install-config-registry-overview).
{: shortdesc}

## Utilizzo di {{site.data.keyword.registrylong_notm}}
{: #openshift_iccr}

Se vuoi utilizzare le immagini archiviate nei tuoi nomi di dominio `icr.io` {{site.data.keyword.registrylong_notm}} privati remoti, devi creare manualmente i segreti di pull dell'immagine per ogni registro globale e regionale. Aggiungi quindi i segreti di pull dell'immagine a ciascun progetto e a un account di servizio per ciascun progetto o a ciascuna distribuzione.
{: shortdesc}

Per ulteriori informazioni, vedi i seguenti argomenti nella documentazione di {{site.data.keyword.containershort_notm}}.
* [Descrizione di come autorizzare il tuo cluster ad eseguire il pull delle immagini da un registro](/docs/containers?topic=containers-images#cluster_registry_auth).
* [Copia dei segreti `default-<region>-icr-io`](/docs/containers?topic=containers-images#copy_imagePullSecret) dallo spazio dei nomi `default` allo spazio dei nomi da cui vuoi eseguire il pull di immagini.
* [Creazione del tuo segreto di pull dell'immagine](/docs/containers?topic=containers-images#other_registry_accounts).
* [Aggiunta del segreto di pull dell'immagine](/docs/containers?topic=containers-images#use_imagePullSecret) alla tua configurazione di distribuzione o all'account di servizio dello spazio dei nomi.
