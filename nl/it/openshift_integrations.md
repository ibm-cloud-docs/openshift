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

# Miglioramento delle funzionalità del cluster con le integrazioni
{: #openshift_integrations}

Con {{site.data.keyword.openshiftlong}}, disponi di molti modi per migliorare le funzionalità dei tuoi cluster e delle tue applicazioni con contenuto di IBM e di terze parti quali l'intelligenza artificiale, la sicurezza, i database, la registrazione nei log, il monitoraggio e altro ancora. Scopri quali integrazioni sono disponibili e come integrare questi servizi con il tuo cluster.
{: shortdesc}

## Integrazioni disponibili
{: #openshift_available_integrations}

Accedi a ulteriori informazioni sulle seguenti integrazioni di {{site.data.keyword.cloud_notm}} e di terze parti per i cluster OpenShift.
{: shortdesc}

<dl>
  <dt>Servizi della piattaforma {{site.data.keyword.cloud_notm}}</dt>
  <dd>I servizi della piattaforma {{site.data.keyword.cloud_notm}} che supportano le chiavi del servizio possono essere integrati utilizzando il [bind del servizio](#oc_service_binding). Per trovare una panoramica dei servizi {{site.data.keyword.cloud_notm}}, vedi [Integrazioni popolari](/docs/containers?topic=containers-supported_integrations#popular_services).</dd>

  <dt>Servizi dell'infrastruttura classica {{site.data.keyword.cloud_notm}}</dt>
  <dd>Il tuo cluster OpenShift è basato sui servizi dell'infrastruttura classica {{site.data.keyword.cloud_notm}} pienamente integrati quali i Vrtual Server, i Bare Metal Server o le VLAN, Crei e lavori con queste istanze del servizio utilizzando l'API, la CLI o la console {{site.data.keyword.containerlong_notm}}.<br><br>
  Per proteggere la tua rete cluster o per connetterti a un data center in loco, puoi configurare una delle seguenti opzioni:
    <ul><li>[Servizio VPN IPSec strongSwan](/docs/containers?topic=containers-vpn#vpn-setup)</li>
    <li>[{{site.data.keyword.BluDirectLink}}](/docs/infrastructure/direct-link?topic=direct-link-get-started-with-ibm-cloud-direct-link)</li>
    <li>[VRA (Virtual Router Appliance)](/docs/containers?topic=containers-vpn#vyatta)</li>
    <li>[FSA (Fortigate Security Appliance)](/docs/services/vmwaresolutions/services?topic=vmware-solutions-fsa_considerations)</li></ul></dd>

  <dt>Archiviazione {{site.data.keyword.cloud_notm}}</dt>
  <dd>Le soluzioni di archiviazione persistente supportate, come {{site.data.keyword.cloud_notm}} File Storage, {{site.data.keyword.cloud_notm}} Block Storage o {{site.data.keyword.cos_full_notm}} sono integrate come driver flessibili di Kubernetes e possono essere configurate utilizzando i [grafici Helm](#oc_helm). La documentazione dell'archiviazione per ogni soluzione include istruzioni per l'installazione e la gestione dell'archiviazione. Per ulteriori informazioni sulla scelta di una soluzione di archiviazione persistente, vedi [Pianificazione di archiviazione persistente altamente disponibile](/docs/openshift?topic=containers-storage_planning).</dd>

  <dt>Cluster autoscaler</dt>
  <dd>Con il plugin `ibm-iks-cluster-autoscaler`, puoi ridimensionare automaticamente i pool di nodi di lavoro nel tuo cluster per aumentare o ridurre il numero di nodi di lavoro nel pool in base alle richieste di dimensionamento dei tuoi carichi di lavoro pianificati. Per ulteriori informazioni, vedi [Ridimensionamento dei cluster](/docs/containers?topic=containers-ca) nella documentazione di {{site.data.keyword.containerlong_notm}}.</dd>

  <dt>Istio per la rete di servizi</dt>
  <dd>A differenza dei cluster Kubernetes della community, <a href="https://www.ibm.com/cloud/info/istio" target="_blank">Istio <img src="../icons/launch-glyph.svg" alt="Icona link esterno"></a> non è disponibile come un componente aggiuntivo gestito per i cluster OpenShift. Utilizza invece il progetto Red Hat OpenShift Service Mesh. Per ulteriori informazioni, vedi [la documentazione sull'installazione di OpenShift ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://docs.openshift.com/container-platform/3.11/servicemesh-install/servicemesh-install.html).</dd>

  <dt>Knative per le applicazioni senza server</dt>
  <dd>A differenza dei cluster Kubernetes della community, <a href="https://github.com/knative/docs" target="_blank">Knative <img src="../icons/launch-glyph.svg" alt="Icona link esterno"></a> non è disponibile come un componente aggiuntivo gestito per i cluster OpenShift. Prova invece l'anteprima per gli sviluppatori Knative su OpenShift. Per ulteriori informazioni, vedi [la documentazione sull'installazione di OpenShift ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://github.com/openshift-knative/docs).</dd>

  <dt>Kubernetes Terminal</dt>
  <dd>Il [componente aggiuntivo Kubernetes Terminal](/docs/containers?topic=containers-cs_cli_install#cli_web) è disponibile solo per il cluster Kubernetes della community, non per i cluster OpenShift.</dd>

  <dt>{{site.data.keyword.la_full_notm}}</dt>
  <dd>Aggiungi funzionalità di gestione dei log al tuo cluster distribuendo LogDNA come servizio di terze parti ai tuoi nodi di lavoro per gestire i log dai contenitori di pod. Per ulteriori informazioni, vedi la seguente documentazione.<ul>
    <li>[Informazioni sulla collaborazione LogDNA](/docs/containers?topic=containers-service-partners#logdna-partner).</li>
    <li>[Configurazione di LogDNA in un cluster OpenShift](/docs/openshift?topic=openshift-openshift_health#openshift_logdna).</li>
    <li>[Esercitazione: Gestione dei log di cluster Kubernetes con {{site.data.keyword.loganalysisfull_notm}} con ](/docs/services/Log-Analysis-with-LogDNA/tutorials?topic=LogDNA-kube#kube).</li></ul></dd>

  <dt>Razee</dt>
  <dd>[Razee ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://razee.io/) è un progetto open source che automatizza e gestisce la distribuzione delle risorse Kubernetes tra cluster, ambienti e provider cloud e ti aiuta a visualizzare le informazioni sulla distribuzione per le tue risorse, consentendoti di monitorare il processo di rollout e trovare i problemi di distribuzione in modo più rapido. Per ulteriori informazioni su Razee e su come configurarlo nel tuo cluster per automatizzare il tuo processo di distribuzione, vedi la [documentazione di Razee ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://github.com/razee-io/Razee).</dd>

  <dt>{{site.data.keyword.mon_full_notm}}</dt>
  <dd>Ottieni visibilità operativa sulle prestazioni e sull'integrità delle tue applicazioni distribuendo Sysdig come servizio di terze parti ai tuoi nodi di lavoro per inoltrare le metriche a {{site.data.keyword.monitoringlong}}. Per ulteriori informazioni, vedi la seguente documentazione.<ul>
    <li>[Informazioni sulla collaborazione Sysdig](/docs/containers?topic=containers-service-partners#sydig-partner).</li>
    <li>[Configurazione di Sysdig in un cluster OpenShift](/docs/openshift?topic=openshift-openshift_health#openshift_sysdig).</li>
    <li>[Esercitazione: Analisi delle metriche per un'applicazione distribuita in un cluster Kubernetes](/docs/services/Monitoring-with-Sysdig/tutorials?topic=Sysdig-kubernetes_cluster#kubernetes_cluster).</li></ul></dd>

  <dt>Altre integrazioni di terze parti</dt>
  <dd>Puoi installare molte altre integrazioni nel tuo cluster OpenShift, ad esempio attraverso il catalogo OpenShift, gli operatori, i grafici Helm o le installazioni software open source fai-da-te. Assicurati che queste applicazioni siano compatibili con il tuo cluster OpenShift e la tua versione di Kubernetes. Ad esempio, potresti dover [aggiornare l'applicazione](/docs/openshift?topic=openshift-openshift_apps) perché l'installazione abbia esito positivo.</dd>

</dl>

<br />


## Aggiunta di integrazioni al tuo cluster OpenShift
{: #openshift_adding_services}

Puoi aggiungere servizi al tuo cluster Red Hat OpenShift on IBM Cloud in diversi modi, compresi i bind di servizio, i grafici Helm e gli operatori. Se voi installare applicazioni software open source, assicurati che tali applicazioni siano compatibili con il tuo cluster OpenShift e la tua versione Kubernetes. Ad esempio, potresti dover [aggiornare l'applicazione](/docs/openshift?topic=openshift-openshift_apps) perché l'installazione abbia esito positivo.
{: shortdesc}

### IBM Cloud Pak
{: #oc_cloud_paks}

Gli [IBM Cloud Pak&trade; ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://www.ibm.com/cloud/paks/) sono componenti software open source e middleware IBM inseriti nel contenitore che sono concessi su licenza per l'utilizzo in [IBM Passport Advantage](https://www.ibm.com/software/passportadvantage/) come parte della tua soluzione cloud ibrida. Gli IBM Cloud Pak vengono eseguiti esclusivamente sui cluster OpenShift, non sui cluster Kubernetes della community. Per utilizzare gli IBM Cloud Pak, devi configurare il tuo ambiente cluster nel seguente modo.
{: shortdesc}

1. Nel progetto a cui vuoi distribuire il Cloud Pack, assicurati di [configurare il segreto di pull dell'immagine per accedere alle immagini che sono archiviate in {{site.data.keyword.registrylong_notm}}](/docs/openshift?topic=openshift-openshift-images#openshift_iccr).
2. Importa il Cloud Pak da Passport Advantage al tuo registro. I metodi variano a seconda del Cloud Pak.
   * Per gli ambienti cloud pubblici, puoi utilizzare lo [strumento CLI `ibmcloud cr ppa-archive-load`](/docs/services/Registry?topic=registry-ts_index#ts_ppa_import).
   * Se hai dei servizi comuni ICP installati nel tuo cluster, puoi utilizzare lo [strumento CLI `cloudctl catalog load-archive`](https://www.ibm.com/support/knowledgecenter/en/SSBS6K_3.1.2/app_center/add_package_offline.html).
   * Alcuni Cloud Pak, come {{site.data.keyword.icp4dfull_notm}}, eseguono il push dell'immagine al repository per tuo conto come parte del loro processo di installazione.
3. Attieniti alle istruzioni specifiche per l'installazione di ciascun Cloud Pak, come ad esempio la configurazione dei valori di grafico Helm per lavorare entro i vincoli del contesto di sicurezza OpenShift.

### Bind del servizio {{site.data.keyword.cloud_notm}}
{: #oc_service_binding}

Per accedere ai servizi {{site.data.keyword.cloud_notm}} nel tuo account, puoi creare le credenziali del servizio e archiviare queste credenziali in un segreto di Kubernetes nel tuo cluster. Per ulteriori informazioni, vedi [Aggiunta di servizi attraverso il bind del servizio {{site.data.keyword.cloud_notm}}](/docs/containers?topic=containers-service-binding).

### Grafici Helm
{: #oc_helm}

[Helm ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://helm.sh) è un gestore pacchetti di Kubernetes che utilizza i grafici Helm per definire, installare e aggiornare applicazioni Kubernetes nel tuo cluster. I grafici Helm comprimono le specifiche per generare file YAML per le risorse Kubernetes che creano la tua applicazione. Poiché OpenShift imposta dei vincoli del contesto di sicurezza più rigidi rispetto a Kubernetes della community, potresti dover modificare la tua distribuzione Helm prima di installare il grafico. Per installare Helm, vedi la [documentazione di {{site.data.keyword.containershort_notm}}](/docs/containers?topic=containers-helm).
{: shortdesc}

### Operatori
{: #oc_operators}

Invece di Helm, puoi utilizzare gli [operatori ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://docs.openshift.com/container-platform/4.1/applications/operators/olm-what-operators-are.html) per assemblare, distribuire e aggiornare le tue applicazioni. Gli operatori sono disponibili solo per le versioni OpenShift 4.1. Nel frattempo, puoi provare l'[operatore {{site.data.keyword.cloud_notm}} sperimentale ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://github.ibm.com/seed/olm/blob/master/pocs/openshift-ibmcloud/README.md).
{: shortdesc}
