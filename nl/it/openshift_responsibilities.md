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


# Le tue responsabilità utilizzando Red Hat OpenShift on IBM Cloud
{: #responsibilities_openshift}

Informazioni sulle responsabilità, sui termini e sulle condizioni a cui attenerti quando utilizzi {{site.data.keyword.containerlong}} per eseguire il provisioning di cluster Red Hat OpenShift on IBM Cloud.
{:shortdesc}

## Responsabilità di gestione del cluster
{: #responsibilities}

IBM ti fornisce una piattaforma cloud enterprise per consentirti di distribuire le applicazioni insieme a servizi di sicurezza, {{site.data.keyword.cloud_notm}} DevOps, AI e dati. Puoi scegliere come configurare, integrare e utilizzare le tue applicazioni e i tuoi servizi nel cloud.
{:shortdesc}

<table summary="La tabella mostra le responsabilità di IBM e le tue. Le righe devono essere lette da sinistra a destra; le icone rappresentano ciascuna responsabilità nella colonna uno e la descrizione è contenuta nella colonna due.">
<caption>Responsabilità di IBM e tue</caption>
  <thead>
  <th colspan=2>Responsabilità in base al tipo</th>
  </thead>
  <tbody>
    <tr>
    <td align="center"><img src="images/icon_clouddownload.svg" alt="Icona di una nuvola con una freccia che punta verso il basso"/><br>Infrastruttura cloud</td>
    <td>
    **Responsabilità di IBM**:
    <ul><li>Distribuire un master dedicato altamente disponibile e pienamente gestito in un account protetto dell'infrastruttura di proprietà di IBM per ciascun cluster.</li>
    <li>Eseguire il provisioning dei nodi di lavoro nel tuo account dell'infrastruttura IBM Cloud.</li>
    <li>Configurare i componenti di gestione del cluster, come le VLAN e i programmi di bilanciamento del carico.</li>
    <li>Soddisfare le richieste di ulteriore infrastruttura, come ad esempio l'aggiunta e la rimozione di nodi di lavoro, la creazione di sottoreti predefinite e il provisioning di volumi di archiviazione in risposta alle attestazioni del volume persistente (o PVC, persistent volume claim).</li>
    <li>Integrare le risorse dell'infrastruttura ordinate in modo che funzionino automaticamente con l'architettura del tuo cluster e diventino disponibili per le tue applicazioni distribuite e i tuoi carichi di lavoro.</li></ul>
    <br><br>
    **Le tue responsabilità**:
    <ul><li>Utilizzare gli strumenti API, CLI e console forniti per regolare la capacità di [calcolo](/docs/containers?topic=containers-clusters#clusters) e [archiviazione](/docs/containers?topic=containers-storage_planning#storage_planning) e per regolare la [configurazione di rete](/docs/containers?topic=containers-cs_network_cluster#cs_network_cluster) per soddisfare le esigenze del tuo carico di lavoro.</li></ul><br><br>
    </td>
     </tr>
     <tr>
     <td align="center"><img src="images/icon_tools.svg" alt="Icona di una chiave inglese"/><br>Cluster gestito</td>
     <td>
     **Responsabilità di IBM**:
     <ul><li>Fornire una suite di strumenti per automatizzare la gestione dei cluster, come ad esempio [API ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://containers.cloud.ibm.com/global/swagger-global-api/), [plugin CLI](/docs/containers?topic=containers-cli-plugin-kubernetes-service-cli) e [console ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno") Red Hat OpenShift on IBM Cloud ](https://cloud.ibm.com/kubernetes/clusters).</li>
     <li>Applicare automaticamente aggiornamenti di sicurezza, versione e sistema operativo di patch master Kubernetes. Eseguire gli aggiornamenti principali e secondari a tua disposizione per poterli applicare.</li>
     <li>Aggiornare e ripristinare componenti Red Hat OpenShift on IBM Cloud e Kubernetes operativi all'interno del cluster, come ad esempio l'ALB (application load balancer) Ingress e il plugin di archiviazione file.</li>
     <li>Eseguire il backup e il ripristino dei dati in etcd, come ad esempio i tuoi file di configurazione del carico di lavoro Kubernetes</li>
     <li>Configurare una connessione OpenVPN tra il master e i nodi di lavoro quando viene creato il cluster.</li>
     <li>Monitorare e notificare l'integrità del master e dei tuoi nodi di lavoro nelle diverse interfacce.</li>
     <li>Fornire gli aggiornamenti di sicurezza, versione, sistema operativo di patch, principali e secondari del nodo di lavoro.</li>
     <li>Soddisfare le richieste di automazione per aggiornare e ripristinare i nodi di lavoro. Fornire l'[Autorecovery del nodo di lavoro](/docs/containers?topic=containers-health#autorecovery) facoltativo.</li>
     <li>Fornire gli strumenti, come ad esempio il [cluster autoscaler](/docs/containers?topic=containers-ca#ca), per estendere la tua infrastruttura cluster.</li>
     </ul>
     <br><br>
     **Le tue responsabilità**:
     <ul>
     <li>Utilizzare gli strumenti API, CLI o console per [applicare](/docs/containers?topic=containers-update#update) gli aggiornamenti master Kubernetes principali e secondari forniti e gli aggiornamenti di nodi di lavoro patch.</li>
     <li>Utilizzare gli strumenti API, CLI o console per [ripristinare](/docs/containers?topic=containers-cs_troubleshoot#cs_troubleshoot) le tue risorse dell'infrastruttura o impostare e configurare l'[Autorecovery di nodo di lavoro](/docs/containers?topic=containers-health#autorecovery) facoltativo.</li></ul>
     <br><br></td>
      </tr>
    <tr>
      <td align="center"><img src="images/icon_locked.svg" alt="Icona di blocco"/><br>Ambiente altamente sicuro</td>
      <td>
      **Responsabilità di IBM**:
      <ul>
      <li>Mantenere controlli commisurati ai [vari standard di conformità del settore](/docs/containers?topic=containers-faqs#standards), come ad esempio PCI DSS.</li>
      <li>Monitorare, isolare e ripristinare il master cluster.</li>
      <li>Fornire repliche ad alta disponibilità dei componenti server API master Kubernetes, etcd, programma di pianificazione e gestore controller per una protezione in caso di interruzioni del master.</li>
      <li>Applicare automaticamente gli aggiornamenti delle patch di sicurezza master e fornire gli aggiornamenti delle patch di sicurezza del nodo di lavoro.</li>
      <li>Abilitare specifiche impostazioni di sicurezza, come i dischi crittografati sui nodi di lavoro</li>
      <li>Disabilitare specifiche azioni non sicure per i nodi di lavoro, come ad esempio il non consentire agli utenti di eseguire SSH nell'host.</li>
      <li>Crittografare le comunicazioni tra il master e i nodi di lavoro con TLS.</li>
      <li>Fornire delle immagini Linux conformi a CIS per i sistemi operativi di nodo di lavoro.</li>
      <li>Monitorare in modo continuo le immagini di nodo di lavoro e master per rilevare problemi di vulnerabilità e conformità alla sicurezza.</li>
      <li>Eseguire il provisioning ai nodi di lavoro di due partizioni di dati crittografate a 256 bit SSD e AES.</li>
      <li>Fornire le opzioni per la connettività di rete del cluster, come ad esempio gli endpoint del servizio pubblico e privato.</li>
      <li>Fornire le opzioni per l'isolamento del calcolo, come ad esempio delle macchine virtuali dedicate o bare metal.</li>
      <li>Integrare RBAC (role-based access control) Kubernetes con {{site.data.keyword.Bluemix_notm}} IAM (Identity and Access Management).</li>
      </ul>
      <br><br>
      **Le tue responsabilità**:
      <ul>
      <li>Utilizzare gli strumenti API, CLI o console per applicare gli [aggiornamenti di patch di sicurezza](/docs/containers?topic=containers-changelog#changelog) forniti ai tuoi nodi di lavoro.</li>
      <li>Scegliere come configurare la tua [rete cluster](/docs/containers?topic=containers-plan_clusters) e configurare ulteriori [impostazioni di sicurezza](/docs/containers?topic=containers-security#security) per soddisfare le esigenze di sicurezza e di compatibilità del tuo carico di lavoro. Se applicabile, configura il tuo [firewall](/docs/containers?topic=containers-firewall#firewall).</li></ul>
      <br><br></td>
      </tr>

      <tr>
        <td align="center"><img src="images/icon_code.svg" alt="Icona di parentesi di codice"/><br>Orchestrazione delle applicazioni</td>
        <td>
        **Responsabilità di IBM**:
        <ul>
        <li>Eseguire il provisioning ai cluster dei componenti Kubernetes installati in modo da consentirti di accedere all'API Kubernetes.</li>
        <li>Fornire diversi componenti aggiuntivi gestiti per estendere le funzionalità della tua applicazione, come ad esempio [Istio](/docs/containers?topic=containers-istio#istio) e [Knative](/docs/containers?topic=containers-serverless-apps-knative). La manutenzione, per te, è semplificata poiché IBM fornisce l'installazione e gli aggiornamenti per i componenti aggiuntivi gestiti.</li>
        <li>Fornire l'integrazione cluster con tecnologie di partenariato di terze parti selezionate, come ad esempio {{site.data.keyword.la_short}}, {{site.data.keyword.mon_short}} e Portworx.</li>
        <li>Fornire l'automazione per abilitare l'associazione mediante bind dei servizi ad altri servizi {{site.data.keyword.cloud_notm}}.</li>
        <li>Creare dei cluster con i segreti di pull dell'immagine in modo che le tue distribuzioni nello spazio dei nomi Kubernetes `default` possano eseguire il pull di immagini da {{site.data.keyword.registrylong_notm}}.</li>
        <li>Fornire classi di archiviazione e plug-in per supportare i volumi persistenti per l'utilizzo con le tue applicazioni.</li>
        <li>Creare dei cluster con gli indirizzi IP di sottorete riservati da utilizzare per esporre le applicazioni esternamente.</li>
        <li>Supportare i programmi di bilanciamento del carico pubblici e privati Kubernetes nativi e gli instradamenti Ingress per esporre i servizi esternamente.</li>
        </ul>
        <br><br>
        **Le tue responsabilità**:
        <ul>
        <li>Utilizzare gli strumenti e le funzioni forniti per [configurare e distribuire](/docs/containers?topic=containers-app#app); [configurare le autorizzazioni](/docs/containers?topic=containers-users#users); [eseguire l'integrazione con altri servizi](/docs/containers?topic=containers-supported_integrations#supported_integrations); [servire esternamente](/docs/containers?topic=containers-cs_network_planning#cs_network_planning); [monitorare l'integrità](/docs/containers?topic=containers-health#health); [salvare, eseguire il backup e ripristinare i dati](/docs/containers?topic=containers-storage_planning#storage_planning) e gestire in altro modo i tuoi carichi di lavoro [altamente disponibili](/docs/containers?topic=containers-ha#ha) e resilienti.</li>
        </ul>
        </td>
        </tr>
  </tbody>
  </table>

<br />


## Uso improprio di Red Hat OpenShift on IBM Cloud
{: #terms}

I clienti non possono fare un uso improprio di Red Hat OpenShift on IBM Cloud.
{:shortdesc}

L'uso improprio include:

*   Qualsiasi attività illegale
*   La distribuzione o l'esecuzione di malware
*   Il danneggiamento di Red Hat OpenShift on IBM Cloud o l'interferenza con l'utilizzo da parte di altri utenti di Red Hat OpenShift on IBM Cloud
*   Il danneggiamento o l'interferenza con l'utilizzo di qualsiasi altro servizio o sistema
*   L'accesso non autorizzato a qualsiasi servizio o sistema
*   La modifica non autorizzata a qualsiasi servizio o sistema
*   La violazione dei diritti altrui

Per i termini generali di utilizzo, consulta [Termini dei
servizi cloud](/docs/overview/terms-of-use?topic=overview-terms#terms).


