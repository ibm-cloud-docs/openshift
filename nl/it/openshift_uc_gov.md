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

# Casi di utilizzo di governo per {{site.data.keyword.cloud_notm}}
{: #cs_uc_gov}

Questi casi di utilizzo evidenziano come i carichi di lavoro su {{site.data.keyword.openshiftlong}} traggono vantaggio dal cloud pubblico. Questi carichi di lavoro sono isolati in regioni globali per la sovranità dei dati, utilizzano il servizio di machine learning Watson invece di nuovo codice netto e si connettono ai database installati in loco.
{: shortdesc}

## Il governo regionale migliora la collaborazione e la velocità con gli sviluppatori della comunità che combinano i dati pubblici e privati
{: #uc_data_mashup}

Un responsabile dei programmi OGD (Open-Government Data) deve condividere i dati pubblici con la comunità e il settore privato, ma i dati sono bloccati in un sistema monolitico installato in loco. 
{: shortdesc}

Perché {{site.data.keyword.cloud_notm}}: con Red Hat OpenShift on IBM Cloud, il responsabile fornisce il valore trasformativo dei dati pubblici e privati combinati. Allo stesso modo, il servizio fornisce la piattaforma cloud pubblica per il refactoring e l'esposizione di microservizi da applicazioni monolitiche in loco. Inoltre, il cloud pubblico consente al governo e alle associazioni pubbliche di utilizzare servizi cloud esterni e strumenti open source adatti alla collaborazione.

Tecnologie chiave:    
* [Cluster che si adattano a diverse esigenze di CPU, RAM e archiviazione](/docs/containers?topic=containers-planning_worker_nodes#planning_worker_nodes)
* [Strumenti nativi DevOps, incluse le toolchain aperte in {{site.data.keyword.contdelivery_full}}](https://www.ibm.com/cloud/garage/toolchains/)
* [Fornisci l'accesso ai dati pubblici con {{site.data.keyword.cos_full_notm}}](/docs/services/cloud-object-storage?topic=cloud-object-storage-about-ibm-cloud-object-storage)
* [Servizi IBM Cloud Analytics plug-and-play](https://www.ibm.com/cloud/analytics)

**Contesto: il governo migliora la collaborazione e la velocità con gli sviluppatori della comunità che combinano i dati pubblici e privati**
* Un modello di “open government” è il futuro, ma questa agenzia governativa regionale non può fare un salto in avanti con i propri sistemi in loco.
* Vogliono sostenere l'innovazione e promuovere il co-sviluppo tra settore privato, cittadini e agenzie pubbliche.
* Diversi gruppi di sviluppatori delle organizzazioni di governo e private non dispongono di una piattaforma open source unificata in cui possano condividere facilmente API e dati.
* I dati del governo sono bloccati in sistemi in loco senza un facile accesso pubblico.

**Soluzione**

Una trasformazione open-government deve essere costruita su una base che offra prestazioni, resilienza, continuità delle operazioni aziendali e sicurezza. Man mano che l'innovazione e il co-sviluppo vanno avanti, le agenzie e i cittadini dipendono da software, servizi e società di infrastrutture per la “protezione e prestazione di servizi”.

Per abbattere la burocrazia e trasformare la relazione del governo con i suoi elettori, si sono rivolti a standard aperti per costruire una piattaforma per la co-creazione:

* OPEN DATA – archiviazione di dati in cui cittadini, agenzie governative e aziende accedono, condividono e migliorano i dati liberamente
* OPEN API – una piattaforma di sviluppo in cui le API sono offerte e riutilizzate da tutti i partner della comunità
* OPEN INNOVATION – una serie di servizi cloud che consentono agli sviluppatori di regolare l'innovazione anziché codificarla manualmente

Per iniziare, il governo utilizza {{site.data.keyword.cos_full_notm}} per memorizzare i suoi dati pubblici nel cloud. Questa archiviazione è riutilizzabile, condivisibile da chiunque e soggetta solo all'attribuzione e alla condivisione in ugual modo. I dati sensibili possono essere ripuliti prima di essere trasferiti nel cloud. Oltre a ciò, vengono configurati controlli di accesso in modo che il cloud limiti la nuova archiviazione di dati, in cui la comunità può dimostrare i POC di dati liberi esistenti migliorati.

Il passo successivo del governo per le collaborazioni tra pubblico e privato è stato quello di stabilire un'economia delle API ospitata in {{site.data.keyword.apiconnect_long}}. Lì, gli sviluppatori di comunità e impresa rendono i dati facilmente accessibili in forma di API. I loro obiettivi sono di disporre di API REST pubblicamente disponibili, per consentire l'interoperabilità e accelerare l'integrazione delle applicazioni. Utilizzano IBM {{site.data.keyword.SecureGateway}} per riconnettersi alle origini dati private in loco.

Infine, le applicazioni basate su tali API condivise sono ospitate in Red Hat OpenShift on IBM Cloud, dove è facile attivare i cluster. Quindi, gli sviluppatori della comunità, del settore privato e del governo possono co-creare facilmente le applicazioni. In sintesi, gli sviluppatori devono concentrarsi sulla codifica anziché sulla gestione dell'infrastruttura. Pertanto, hanno scelto Red Hat OpenShift on IBM Cloud perché IBM semplifica la gestione dell'infrastruttura:
* Gestione di master Kubernetes, IaaS e componenti operativi, come Ingress e archiviazione
* Monitoraggio dell'integrità e del recupero dei nodi di lavoro
* Fornitura del calcolo globale, in modo che gli sviluppatori non debbano sostenere l'infrastruttura nelle regioni di tutto il mondo in cui necessitano di carichi di lavoro e dati

Spostare i carichi di lavoro di calcolo in {{site.data.keyword.cloud_notm}} non è comunque sufficiente. Il governo deve anche passare attraverso una trasformazione di processi e metodi. Adottando le procedure di IBM Garage Method, il fornitore può implementare un processo di consegna agile e iterativo che supporta le moderne procedure di DevOps come CI/CD (Continuous Integration and Delivery).

Gran parte dello stesso processo CI/CD è automatizzato con {{site.data.keyword.contdelivery_full}} nel cloud. Il fornitore può definire toolchain del flusso di lavoro per preparare le immagini del contenitore, verificare la presenza di vulnerabilità e distribuirle nel cluster Kubernetes.

**Modello di soluzione**

Strumenti API, archiviazione e calcolo su richiesta eseguiti nel cloud pubblico con accesso sicuro da e verso origini dati in loco.

Soluzione tecnica:
* Red Hat OpenShift on IBM Cloud
* {{site.data.keyword.cos_full_notm}} e {{site.data.keyword.cloudant}}
* {{site.data.keyword.apiconnect_long}}
* IBM {{site.data.keyword.SecureGateway}}
* {{site.data.keyword.contdelivery_full}}

**Passo 1: memorizza i dati nel cloud**
* {{site.data.keyword.cos_full_notm}} fornisce l'archiviazione di dati cronologici, accessibile a tutti sul cloud pubblico.
* Utilizza {{site.data.keyword.cloudant}} con le chiavi fornite dallo sviluppatore per memorizzare i dati della cache nel cloud.
* Utilizza IBM {{site.data.keyword.SecureGateway}} per mantenere connessioni sicure ai database installati in loco esistenti.

**Passo 2: fornisci l'accesso ai dati con le API**
* Utilizza {{site.data.keyword.apiconnect_long}} per la piattaforma di economia delle API. Le API consentono ai settori pubblico e privato di combinare i dati nelle loro applicazioni.
* Crea cluster per applicazioni pubbliche-private, guidate dalle API.
* Struttura le applicazioni in una serie di microservizi cooperativi eseguiti all'interno di Red Hat OpenShift on IBM Cloud, che si basa sulle aree funzionali delle applicazioni e delle loro dipendenze.
* Distribuisci le applicazioni nei contenitori eseguiti in Red Hat OpenShift on IBM Cloud. Gli strumenti HA integrati in Red Hat OpenShift on IBM Cloud bilanciano i carichi di lavoro, compresi la riparazione automatica e il bilanciamento del carico.
* Fornisci dashboard DevOps standardizzati attraverso Kubernetes, strumenti open source noti a tutti i tipi di sviluppatori.

**Passo 3: innovazione con IBM Garage e i servizi cloud**
* Adotta le procedure di sviluppo agili e iterative di IBM Garage Method per consentire frequenti rilasci di funzioni, patch e correzioni senza tempi di inattività.
* Sia che gli sviluppatori siano nel settore pubblico o privato, {{site.data.keyword.contdelivery_full}} li aiuta a fornire rapidamente una toolchain integrata, utilizzando template personalizzabili e condivisibili.
* Dopo che gli sviluppatori hanno creato e testato le applicazioni nei propri cluster di sviluppo e test, utilizzano le toolchain {{site.data.keyword.contdelivery_full}} per distribuire le applicazioni nei cluster di produzione.
* Con gli strumenti Watson di intelligenza artificiale, apprendimento automatico e apprendimento approfondito disponibili nel catalogo {{site.data.keyword.cloud_notm}}, gli sviluppatori si concentrano sui problemi di dominio. Invece del codice ML univoco personalizzato, la logica ML viene inserita nelle applicazioni con i bind dei servizi.

**Risultati**
* Le generalmente lente collaborazioni tra pubblico e privato adesso attivano le applicazioni rapidamente, in settimane invece che in mesi. Queste collaborazioni di sviluppo offrono ora funzioni e correzioni di bug fino a 10 volte a settimana.
* Lo sviluppo è accelerato quando tutti i partecipanti utilizzano strumenti open source ben noti, come Kubernetes. Le lunghe curve di apprendimento non rappresentano più un blocco.
* Ai cittadini e al settore privato viene fornita la trasparenza delle attività, delle informazioni e dei piani. Inoltre, i cittadini sono integrati nei processi, nei servizi e nel supporto del governo.
* Le collaborazioni tra pubblico e privato consentono di portare a termine compiti di enorme entità, come il rilevamento dei virus Zika, la distribuzione intelligente dell'elettricità, l'analisi delle statistiche sulla criminalità e l'istruzione universitaria per le nuove professionalità (new collar).

## Il grande porto pubblico protegge lo scambio di dati portuali e manifesti di spedizione che collegano organizzazioni pubbliche e private
{: #uc_port}

I responsabili IT per una società di spedizione privata e il porto gestito dal governo devono connettersi, fornire visibilità e scambiare in modo sicuro le informazioni sui porti. Ma non esisteva un sistema unificato per collegare le informazioni sui porti pubbliche e i manifesti di carico privati.
{: shortdesc}

Perché {{site.data.keyword.cloud_notm}}: Red Hat OpenShift on IBM Cloud consente agli enti governativi e alle partecipazioni del settore pubblico di utilizzare servizi cloud esterni e strumenti open source adatti alla collaborazione. I contenitori hanno fornito una piattaforma condivisibile in cui sia la società portuale che quella di spedizione avevano la garanzia che le informazioni condivise fossero ospitate su una piattaforma sicura. E tale piattaforma si ridimensiona quando si passa da piccoli sistemi di sviluppo e test a grandi sistemi di produzione. Le toolchain aperte hanno accelerato ulteriormente lo sviluppo mediante l'automazione di build, test e distribuzioni.

Tecnologie chiave:    
* [Cluster che si adattano a diverse esigenze di CPU, RAM e archiviazione](/docs/containers?topic=containers-planning_worker_nodes#planning_worker_nodes)
* [Sicurezza e isolamento dei contenitori](/docs/containers?topic=containers-security#security)
* [Strumenti nativi DevOps, incluse le toolchain aperte in {{site.data.keyword.contdelivery_full}}](https://www.ibm.com/cloud/garage/toolchains/)
* [SDK per Node.js](/docs/runtimes/nodejs?topic=Nodejs-nodejs_runtime#nodejs_runtime)

**Contesto: il porto protegge lo scambio di dati portuali e manifesti di carico che collegano organizzazioni pubbliche e private.**

* Diversi gruppi di sviluppatori delle società di governo e di spedizione non dispongono di una piattaforma unificata in cui possano collaborare, il che rallenta le distribuzioni di aggiornamenti e funzioni.
* Gli sviluppatori sono sparsi in tutto il mondo e oltre i confini organizzativi, il che rende l'open-source e PaaS l'opzione migliore.
* La sicurezza è una preoccupazione primaria e questa preoccupazione aumenta la difficoltà di collaborazione che influisce sulle funzioni e sugli aggiornamenti del software, specialmente dopo che le applicazioni passano in produzione.
* I dati just-in-time hanno comportato la necessità di sistemi mondiali altamente disponibili per ridurre ritardi nelle operazioni di transito. Le tabelle orarie per i terminali di spedizione sono altamente controllate e in alcuni casi inflessibili. L'utilizzo del Web sta crescendo, quindi l'instabilità potrebbe causare un'esperienza utente insoddisfacente.

**Soluzione**

Il porto e la società di spedizione collaborano allo sviluppo di un sistema di scambio unificato per inviare elettronicamente informazioni relative alla conformità per lo sdoganamento di merci e navi una sola volta, piuttosto che a più agenzie. Le applicazioni doganali e di manifesti di carico possono condividere rapidamente i contenuti di una particolare spedizione e garantire che tutti documenti siano trasferiti ed elaborati elettronicamente dalle agenzie per il porto.

Quindi creano una collaborazione dedicata alle soluzioni per il sistema commerciale:
* DICHIARAZIONI - Applicazione per raccogliere manifesti di carico ed elaborare digitalmente documenti doganali tipici e per contrassegnare gli articoli non a norma per indagini e controlli
* TARIFFE – Applicazione per calcolare le tariffe, inviare elettronicamente le spese allo spedizioniere e ricevere pagamenti digitali
* NORMATIVE – Applicazione flessibile e configurabile che introduce nelle precedenti due applicazioni politiche e normative in continua evoluzione che influiscono sulle importazioni, sulle esportazioni e sull'elaborazione delle tariffe

Gli sviluppatori hanno iniziato distribuendo le loro applicazioni in contenitori con Red Hat OpenShift on IBM Cloud. Hanno creato cluster per un ambiente di sviluppo condiviso che consentono agli sviluppatori di tutto il mondo di distribuire rapidamente e in modo collaborativo i miglioramenti alle applicazioni. I contenitori consentono a ciascun team di sviluppo di utilizzare la lingua di loro scelta.

La sicurezza prima di tutto: i responsabili IT hanno scelto i cluster bare metal. Con bare metal per Red Hat OpenShift on IBM Cloud, i carichi di lavoro doganali sensibili ora hanno un isolamento familiare ma all'interno della flessibilità del cloud pubblico. 

Poiché la società di spedizione vuole anche lavorare con altri porti, la sicurezza delle applicazioni è fondamentale. I manifesti di carico e le informazioni doganali sono altamente confidenziali. Da tale nucleo sicuro, Vulnerability Advisor fornisce le seguenti scansioni:
* Scansioni dei punti vulnerabili delle immagini
* Scansioni delle politiche basate su ISO 27k
* Scansioni dei contenitori attivi
* Scansioni dei pacchetti per malware noti

Allo stesso tempo, {{site.data.keyword.iamlong}} aiuta a controllare chi ha accesso alle risorse e a quale livello.

Gli sviluppatori si concentrano sui problemi di dominio, utilizzando gli strumenti esistenti: invece di scrivere un codice di registrazione e monitoraggio univoco, lo inseriscono nelle applicazioni, eseguendo il bind dei servizi {{site.data.keyword.cloud_notm}} nei cluster. Gli sviluppatori vengono inoltre liberati dalle attività di gestione dell'infrastruttura perché IBM si occupa di Kubernetes e degli aggiornamenti dell'infrastruttura, della sicurezza e altro ancora.

**Modello di soluzione**

Kit starter Node, archiviazione e calcolo su richiesta eseguiti nel cloud pubblico con accesso sicuro ai dati di spedizione in tutto il mondo, a seconda delle necessità. Il calcolo nei cluster è a prova di manomissione e isolato su bare metal.  

Soluzione tecnica:
* Red Hat OpenShift on IBM Cloud
* {{site.data.keyword.openwhisk}}
* {{site.data.keyword.cloudant}}
* IBM {{site.data.keyword.SecureGateway}}

**Passo 1: carica le applicazioni in un contenitore utilizzando i microservizi**
* Utilizza il kit starter Node.js di IBM per iniziare subito le attività di sviluppo.
* Struttura le applicazioni in una serie di microservizi cooperativi eseguiti all'interno di Red Hat OpenShift on IBM Cloud in base alle aree funzionali dell'applicazione e delle sue dipendenze.
* Distribuisci le applicazioni di spedizione e manifesti di carico nel contenitore eseguito in Red Hat OpenShift on IBM Cloud.
* Fornisci dashboard DevOps standardizzati attraverso Kubernetes.
* Utilizza IBM {{site.data.keyword.SecureGateway}} per mantenere connessioni sicure ai database installati in loco esistenti.

**Passo 2: garantisci la disponibilità globale**
* Dopo che gli sviluppatori distribuiscono le applicazioni nei propri cluster di sviluppo e test, utilizzano le toolchain {{site.data.keyword.contdelivery_full}} ed Helm per distribuire applicazioni specifiche per paese nei cluster di tutto il mondo.
* I carichi di lavoro e i dati possono quindi soddisfare le normative regionali.
* Gli strumenti HA integrati in Red Hat OpenShift on IBM Cloud bilanciano il carico di lavoro all'interno di ogni regione geografica, compresi la riparazione automatica e il bilanciamento del carico.

**Passo 3: condivisione dei dati**
* {{site.data.keyword.cloudant}} è un moderno database NoSQL adatto a una serie di casi di utilizzo basati sui dati, dall'archiviazione e query di dati chiave-valore all'archiviazione e query di dati complessi orientati ai documenti.
* Per ridurre al minimo le query ai database regionali, {{site.data.keyword.cloudant}} viene utilizzato per memorizzare nella cache i dati della sessione dell'utente tra le applicazioni.
* Questa configurazione migliora l'usabilità e le prestazioni dell'applicazione di front-end in tutte le applicazioni su {{site.data.keyword.containershort}}.
* Mentre le applicazioni di lavoro in Red Hat OpenShift on IBM Cloud analizzano i dati in loco e memorizzano i risultati in {{site.data.keyword.cloudant}}, {{site.data.keyword.openwhisk}} reagisce alle modifiche e ripulisce automaticamente i dati sui feed dei dati in entrata.
* Allo stesso modo, è possibile attivare notifiche sulle spedizioni in una regione tramite caricamenti di dati in modo che tutti i consumatori futuri possano accedere ai nuovi dati.

**Risultati**
* Con i kit starter IBM, Red Hat OpenShift on IBM Cloud e gli strumenti {{site.data.keyword.contdelivery_full}}, gli sviluppatori globali collaborano nelle organizzazioni e negli enti governativi. Sviluppano collaborativamente applicazioni doganali, con strumenti familiari e interoperabili.
* I microservizi riducono notevolmente i tempi di consegna di patch, correzioni di bug e nuove funzioni. Lo sviluppo iniziale è veloce e gli aggiornamenti sono frequenti, fino a 10 volte a settimana.
* I clienti di spedizione e i funzionari governativi hanno accesso ai dati dei manifesti di carico e possono condividere i dati doganali, rispettando al contempo le normative locali.
* La società di spedizione beneficia di una migliore gestione logistica nella catena di fornitura: costi ridotti e tempi di sdoganamento più rapidi.
* Il 99% sono dichiarazioni digitali e il 90% delle importazioni viene elaborato senza l'intervento umano.


