---

copyright:
  years: 2014, 2019
lastupdated: "2019-07-31"

keywords: openshift, roks, rhoks, rhos, version, rhel

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

# Informazioni sulla versione e azioni di aggiornamento
{: #openshift_versions}

I cluster {{site.data.keyword.openshiftlong}} vengono eseguiti a OpenShift versione 3.11, che include il progetto Kubernetes versione 1.11. Il sistema operativo del nodo di lavoro è Red Hat Enterprise Linux 7.
{: shortdesc}

Per ulteriori informazioni sulle versioni di progetto OpenShift e Kubernetes, riesamina le seguenti informazioni.
* [Panoramica delle note sulla release di OpenShift ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://docs.openshift.com/container-platform/3.11/release_notes/index.html)
* [Changelog Kubernetes![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG.md)

## Tipi di aggiornamento
{: #openshift_update_types}

Il tuo cluster Red Hat OpenShift on IBM Cloud ha tre tipi di aggiornamento: principale, secondario e patch.
Quando gli aggiornamenti diventano disponibili, ricevi una notifica quando visualizzi le informazioni sui nodi di lavoro, come ad esempio nella console o nella CLI con i comandi `ibmcloud oc workers --cluster <cluster>` o `ibmcloud oc worker-get --cluster <cluster> --worker <worker>`.
{:shortdesc}

|Tipo di aggiornamento|Esempi di etichette di versione|Aggiornato da|Impatto
|-----|-----|-----|-----|
|Principale|3.x.x|Tu|Modifiche di funzionamento per i cluster, inclusi script o distribuzioni|
|Secondario|x.11.x|Tu|Modifiche di funzionamento per i cluster, inclusi script o distribuzioni|
|Patch|x.x.104_1507|IBM e tu|Patch OpenShift e altri aggiornamenti del componente {{site.data.keyword.cloud_notm}} Provider come patch di sicurezza e del sistema operativo. IBM aggiorna i master automaticamente, ma tu applichi le patch ai nodi di lavoro. Vedi ulteriori informazioni sulle patch nella seguente sezione.|
{: caption="Impatti degli aggiornamenti di OpenShift" caption-side="top"}

<dl>
  <dt>**Aggiornamenti principali e secondari (3.11)**</dt>
  <dd><p>Innanzitutto, [aggiorna il tuo nodo master](/docs/openshift?topic=containers-update#master) e quindi [aggiorna i nodi di lavoro](/docs/openshift?topic=containers-update#worker_node). I nodi di lavoro non possono eseguire una versione principale o secondaria di OpenShift che sia superiore ai master.</p><p class="note">Se utilizzi una versione della CLI `kubectl` che corrisponde almeno alla versione `major.minor` dei tuoi cluster, potresti riscontrare risultati imprevisti. Assicurati di mantenere aggiornate le tue [versioni della CLI](/docs/openshift?topic=openshift-openshift-cli#cli_oc) e dei cluster.</p></dd>
  <dt>**Aggiornamenti patch (x.x.104_1507)**</dt>
  <dd><p>Le patch master sono applicate automaticamente ma avvii tu gli aggiornamenti delle patch di nodi di lavoro. I nodi di lavoro possono anche eseguire versioni patch superiori ai master. Man mano che gli aggiornamenti diventano disponibili, ricevi una notifica quando visualizzi informazioni su nodi di lavoro e master nella console {{site.data.keyword.cloud_notm}} o nella CLI, ad esempio con i seguenti comandi: `ibmcloud oc clusters`, `cluster-get`, `workers` o `worker-get`.</p>
  <p>Le patch possono essere per i nodi di lavoro, per i master o per entrambi.</p>
  <ul><li>**Patch di nodi di lavoro**: controlla mensilmente se è disponibile un aggiornamento e utilizza il [comando](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_update) `ibmcloud oc worker-update` o il [comando](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_reload) `ibmcloud oc worker-reload` per applicare queste patch di sicurezza e sistema operativo. Durante un aggiornamento o un caricamento, viene ricreata l'immagine della macchina del nodo di lavoro e i dati vengono eliminati se non sono [archiviati all'esterno del nodo di lavoro](/docs/openshift?topic=containers-storage_planning#persistent_storage_overview).</li>
  <li>**Patch master**: le patch master vengono applicate automaticamente nel corso di diversi giorni, pertanto una versione della patch master potrebbe essere disponibile prima che venga applicata al tuo master. L'automazione degli aggiornamenti ignora anche i cluster che si trovano in uno stato non integro o che hanno operazioni attualmente in corso. Occasionalmente, IBM potrebbe disabilitare gli aggiornamenti automatici per uno specifico fix pack del master, come indicato nel changelog, ad esempio una patch che è necessaria solo se un master viene aggiornato da una versione secondaria a un'altra. In uno qualsiasi di questi casi, puoi scegliere di utilizzare tranquillamente il [comando](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_cluster_update) `ibmcloud oc cluster-update` tu stesso senza attendere l'applicazione dell'automazione degli aggiornamenti.</li></ul></dd>
</dl>

<br />


## Cronologia delle release
{: #openshift_release_history}

La seguente tabella registra la cronologia delle release di versione di Red Hat OpenShift on IBM Cloud. Puoi utilizzare queste informazioni per finalità di pianificazione, ad esempio per stimare i termini temporali generali di quando una specifica release potrebbe diventare non supportata. Dopo che la community Red Hat OpenShift ha rilasciato un aggiornamento della versione, il team di IBM inizia un processo di consolidamento e verifica della release per gli ambienti {{site.data.keyword.containerlong_notm}}. Le date di disponibilità e di cessazione del supporto della release dipendono dai risultati di questi test, dagli aggiornamenti della community, dalle patch di sicurezza e delle modifiche della tecnologia tra le versioni. Pianifica di tenere la versione del tuo master cluster e dei tuoi nodi di lavoro aggiornata.
{: shortdesc}

Red Hat OpenShift on IBM Cloud è stato per la prima volta disponibile generalmente con OpenShift versione 3.11, che include il progetto Kubernetes versione 1.11. Le date contrassegnate con un simbolo che sembra un pugnale (`†`) non sono definitive e sono soggette a variazioni.
{: important}

<table summary="Questa tabella mostra la cronologia delle release per Red Hat OpenShift on IBM Cloud.">
<caption>Cronologia delle release per Red Hat OpenShift on IBM Cloud.</caption>
<col width="20%" align="center">
<col width="20%">
<col width="30%">
<col width="30%">
<thead>
<tr>
<th>Supportata?</th>
<th>Versione OpenShift / Kubernetes</th>
<th>Red Hat OpenShift on IBM Cloud<br>data di rilascio</th>
<th>Red Hat OpenShift on IBM Cloud<br>data di cessazione del supporto</th>
</tr>
</thead>
<tbody>
<tr>
  <td><img src="images/checkmark-filled.png" align="left" width="32" style="width:32px;" alt="Questa versione è supportata."/></td>
  <td>3.11 / 1.11</td>
  <td>1°agosto 2019 alle ore 0:00 UTC</td>
  <td>`†`</td>
</tr>
</tbody>
</table>
