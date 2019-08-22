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
{:faq: data-hd-content-type='faq'}


# Domande frequenti (FAQ)
{: #faqs}

Riesamina le domande frequenti per l'utilizzo di {{site.data.keyword.openshiftlong}}.
{: shortdesc}

## Quali piattaforme del contenitore sono disponibili per il mio cluster?
{: #container_platforms}
{: faq}

Con {{site.data.keyword.containerlong_notm}}, puoi selezionare da due piattaforme di gestione del contenitore: la versione IBM di Kubernetes della community e Red Hat OpenShift on IBM Cloud. La piattaforma del contenitore selezionata viene installata sui nodi di lavoro e master del tuo cluster. Successivamente, puoi [aggiornare la versione](/docs/containers?topic=containers-update#update) ma non puoi eseguire il rollback a una versione precedente o passare a una piattaforma del contenitore differente. Se vuoi utilizzare più piattaforme del contenitore, crea un cluster separato per ognuna di esse.

Per ulteriori informazioni, vedi la sezione relativa al [confronto tra cluster Kubernetes della community e OpenShift](/docs/openshift?topic=openshift-why_openshift#openshift_kubernetes).

<dl>
  <dt>Kubernetes</dt>
    <dd>[Kubernetes ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://kubernetes.io/) è una piattaforma di orchestrazione dei contenitori open source di livello di produzione che puoi utilizzare per automatizzare, ridimensionare e gestire le tue applicazioni inserite nel contenitore che vengono eseguite su un sistema operativo Ubuntu. Con la [versione {{site.data.keyword.containerlong_notm}}](/docs/containers?topic=containers-cs_versions#cs_versions), ottieni l'accesso alle funzioni dell'API Kubernetes della community che sono considerate **beta** o superiori dalla community. Le funzioni Kubernetes **alpha**, che sono soggetti a modifiche, sono in genere non abilitate per impostazione predefinita. Con Kubernetes, puoi combinare diverse risorse come segreti, distribuzioni e servizi per creare e gestire in sicurezza applicazioni inserite nel contenitore altamente disponibili.<br><br>
    Per iniziare, [crea un cluster Kubernetes](/docs/containers?topic=containers-cs_cluster_tutorial#cs_cluster_tutorial).</dd>
  <dt>OpenShift</dt>
    <dd>Red Hat OpenShift on IBM Cloud è una piattaforma basata su Kubernetes che è progettata appositamente per accelerare i tuoi processi di fornitura di applicazioni inserite nel contenitore che vengono eseguite su un sistema operativo Red Hat Enterprise Linux 7. Puoi orchestrare e ridimensionare i tuoi carichi di lavoro OpenShift esistenti tra cloud in loco e non in loco per una soluzione ibrida portatile che funziona nello stesso modo in scenari multicloud. <br><br>
    Per iniziare, prova l'[esercitazione Red Hat OpenShift on IBM Cloud](/docs/openshift?topic=openshift-openshift_tutorial).</dd>
</dl>

## Posso creare un cluster OpenShift gratuito?
{: #openshift_free}
{: faq}

Puoi creare solo i cluster OpenShift standard. Se vuoi testare le funzionalità di Kubernetes, [crea un cluster Kubernetes gratuito](/docs/containers?topic=containers-clusters#clusters_free) e [distribuisci qualche applicazione](/docs/containers?topic=containers-app). Ridistribuisci quindi le applicazioni che provi nel cluster Kubernetes al tuo [cluster OpenShift](/docs/openshift?topic=openshift-openshift_tutorial#openshift_deploy_app).

## Posso convertire il mio cluster OpenShift beta in un cluster generalmente disponibile (GA, Generally Available)?
{: #openshift_beta_convert}
{: faq}

Puoi creare un cluster GA e quindi ridistribuire tutte le applicazioni da te utilizzate nei cluster beta prima che i cluster beta vengano rimossi. I cluster Beta saranno rimossi entro il 31 agosto 2019 alle ore 0:00 UTC (30 giorni dopo la disponibilità generale di Red Hat OpenShift on IBM Cloud). Per un esempio di ottenimento di tutti i file di configurazione da un progetto, vedi la [documentazione di OpenShift](https://docs.openshift.com/dedicated/admin_guide/assembly_backing-up-restoring-project-application.html).

## Quali versioni di Kubernetes supporta il servizio OpenShift?
{: #supported_kube_versions}
{: faq}

La versione di OpenShift supportata è 3.11, che include Kubernetes 1.11.

## Cosa mi viene addebitato quando utilizzo OpenShift?
{: #openshift_charges}
{: faq}

Per i cluster Red Hat OpenShift on IBM Cloud, ti vengono addebitati gli stessi componenti che nei cluster {{site.data.keyword.containerlong_notm}}. Per ulteriori informazioni, vedi [Cosa mi viene addebitato quando utilizzo {{site.data.keyword.containerlong_notm}}?](/docs/containers?topic=containers-faqs#charges)

Inoltre, i tuoi nodi di lavoro sono installati con il sistema operativo Red Hat Enterprise Linux, che aumenta il prezzo delle macchine del nodo di lavoro. Devi avere anche una licenza OpenShift, che prevede un costo mensile oltre al costo orario della VM o al costo mensile del bare metal. Occorre una licenza OpenShift ogni due core del profilo di nodo di lavoro. Se elimini il tuo nodo di lavoro prima della fine del mese, la tua licenza mensile è disponibile per gli altri nodi di lavoro del pool di nodi di lavoro.
