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

# Casi di utilizzo di trasporto per {{site.data.keyword.cloud_notm}}
{: #cs_uc_transport}

Questi casi di utilizzo evidenziano come i carichi di lavoro su {{site.data.keyword.openshiftlong}} possano
avvalersi delle toolchain per aggiornamenti rapidi delle applicazioni e le distribuzioni multiregione in tutto il mondo. Allo stesso tempo, questi carichi di lavoro possono connettersi a sistemi di back-end esistenti, utilizzare Watson AI per la personalizzazione e accedere ai dati IOT con {{site.data.keyword.messagehub_full}}.

{: shortdesc}

## La società di spedizione aumenta la disponibilità dei sistemi mondiali per l'ecosistema di business partner
{: #uc_shipping}

Un responsabile IT ha dei sistemi di pianificazione e instradamento delle spedizioni con cui i partner interagiscono. I partner richiedono informazioni aggiornate da questi sistemi che accedono ai dati dei dispositivi IoT. Tuttavia, questi sistemi non potevano essere ridimensionati in tutto il mondo con un'elevata disponibilità sufficiente. 
{: shortdesc}

Perché {{site.data.keyword.cloud_notm}}: Red Hat OpenShift on IBM Cloud ridimensiona le applicazioni inserite nel contenitore con 99,999 percento di disponibilità per soddisfare le crescenti richieste. Le distribuzioni di applicazioni si verificano 40 volte a giorno quando gli sviluppatori sperimentano facilmente, distribuendo rapidamente le modifiche ai sistemi di sviluppo e test. La piattaforma IoT facilita l'accesso ai dati IoT.

Tecnologie chiave:    
* [Più regioni per l'ecosistema di business partner](/docs/containers?topic=containers-regions-and-zones#regions-and-zones)
* [Adattamento orizzontale](/docs/containers?topic=containers-app#highly_available_apps)
* [Toolchain aperte in {{site.data.keyword.contdelivery_full}}](https://www.ibm.com/cloud/garage/toolchains/)
* [Servizi cloud per l'innovazione](https://www.ibm.com/cloud/products/#analytics)
* [{{site.data.keyword.messagehub_full}} per inserire dati di evento nelle applicazioni](/docs/services/EventStreams?topic=eventstreams-about#about)

**Contesto: la società di spedizione aumenta la disponibilità dei sistemi mondiali per l'ecosistema di business partner**

* Le differenze regionali per la logistica di spedizione hanno impedito stare al passo con il crescente numero di partner in più paesi. Un esempio sono le normative univoche e la logistica di transito, in cui la società deve mantenere registrazioni coerenti tra tutti i confini.
* I dati just-in-time hanno comportato la necessità di sistemi mondiali altamente disponibili per ridurre ritardi nelle operazioni di transito. Le tabelle orarie per i terminali di spedizione sono altamente controllate e in alcuni casi inflessibili. L'utilizzo del Web sta crescendo, quindi l'instabilità potrebbe causare un'esperienza utente insoddisfacente.
* Gli sviluppatori dovevano evolvere costantemente le applicazioni, ma gli strumenti tradizionali rallentavano la loro capacità di distribuire frequentemente aggiornamenti e funzioni.  

**Soluzione**

La società di spedizione ha bisogno di gestire in modo coerente tabelle orarie di consegna, inventari e documenti doganali. Quindi, può condividere con precisione la posizione delle spedizioni, i contenuti di spedizione e gli orari di consegna ai propri clienti. Sta cercando di sapere esattamente quando un bene (come un elettrodomestico, un capo abbigliamento o un prodotto) arriverà in modo che i suoi clienti di spedizione possano comunicare tali informazioni ai propri clienti.

La soluzione è composta da questi componenti principali:
1. Trasmissione di dati dai dispositivi IoT per ciascun container di spedizione: manifesti di carico e posizione
2. Documenti doganali condivisi digitalmente con i porti e i partner di transito applicabili, incluso il controllo degli accessi
3. Applicazioni per i clienti di spedizione che aggregano e comunicano le informazioni di arrivo per le merci spedite, comprese le API per i clienti di spedizione per riutilizzare i dati di spedizione nelle proprie applicazioni di vendita al dettaglio e business-to-business

Affinché la società di spedizione lavori con partner globali, i sistemi di traffico e pianificazione hanno richiesto modifiche locali per adattarsi alla lingua, alle normative e alla logistica portuale di ciascuna regione. Red Hat OpenShift on IBM Cloud offre una copertura globale in più regioni, tra cui Nord America, Europa, Asia e Australia, in modo che le applicazioni riflettano le esigenze dei suoi partner, in ogni paese.

I dispositivi IoT trasmettono i dati che {{site.data.keyword.messagehub_full}} distribuisce alle applicazioni portuali regionali e agli archivi dati dei manifesti di carico dei controlli doganali e container associati. {{site.data.keyword.messagehub_full}} è il punto di approdo per gli eventi IoT. Distribuisce gli eventi in base alla connettività gestita che la piattaforma Watson IoT offre a {{site.data.keyword.messagehub_full}}.

Una volta che gli eventi si trovano in {{site.data.keyword.messagehub_full}}, vengono mantenuti per l'uso immediato nelle applicazioni di transito portuale e per qualsiasi momento futuro. Le applicazioni che richiedono la latenza più bassa consumano direttamente in tempo reale dal flusso degli eventi ({{site.data.keyword.messagehub_full}}). Altre applicazioni future, come gli strumenti di analisi, possono scegliere di consumare in modalità batch dall'archivio eventi con {{site.data.keyword.cos_full}}.

Poiché i dati di spedizione sono condivisi con i clienti della società, gli sviluppatori assicurano che i clienti possano utilizzare le API per visualizzare i dati di spedizione nelle loro applicazioni. Esempi di tali applicazioni sono le applicazioni di tracciamento mobile o soluzioni di e-commerce web. Gli sviluppatori sono anche impegnati nella creazione e manutenzione delle applicazioni portuali regionali che raccolgono e diffondono i registri doganali e i manifesti di carico. In sintesi, devono concentrarsi sulla codifica anziché sulla gestione dell'infrastruttura. Pertanto, hanno scelto Red Hat OpenShift on IBM Cloud perché IBM semplifica la gestione dell'infrastruttura:
* Gestione di master Kubernetes, IaaS e componenti operativi, come Ingress e archiviazione
* Monitoraggio dell'integrità e del recupero dei nodi di lavoro
* Fornitura del calcolo globale, in modo che gli sviluppatori non siano responsabili dell'infrastruttura nelle diverse regioni in cui necessitano di carichi di lavoro e dati

Per ottenere la disponibilità globale, i sistemi di sviluppo, test e produzione sono stati distribuiti in tutto il mondo in diversi data center. Per l'alta disponibilità (HA), usano una combinazione di più cluster in diverse regioni geografiche e cluster multizona. Possono facilmente distribuire l'applicazione portuale per soddisfare le esigenze aziendali:
* Nei cluster di Francoforte per rispettare le normative europee locali
* Nei cluster degli Stati Uniti per garantire la disponibilità e il ripristino degli errori in locale

Inoltre, diffondono il carico di lavoro tra i cluster multizona di Francoforte per garantire che la versione europea dell'applicazione sia disponibile e che bilanci inoltre il carico di lavoro in modo efficiente. Poiché ogni regione carica dati univoci con l'applicazione portuale, i cluster dell'applicazione sono ospitati in regioni in cui la latenza è bassa.

Per gli sviluppatori, gran parte del processo di integrazione e fornitura continua (CI/CD) può essere automatizzato con {{site.data.keyword.contdelivery_full}}. La società può definire toolchain del flusso di lavoro per preparare le immagini del contenitore, verificare la presenza di vulnerabilità e distribuirle nel cluster Kubernetes.

**Modello di soluzione**

Gestione di eventi, archiviazione e calcolo su richiesta eseguiti nel cloud pubblico con accesso ai dati di spedizione in tutto il mondo, a seconda delle necessità

Soluzione tecnica:
* Red Hat OpenShift on IBM Cloud
* {{site.data.keyword.messagehub_full}}
* {{site.data.keyword.cos_full}}
* {{site.data.keyword.contdelivery_full}}

**Passo 1: carica le applicazioni in un contenitore utilizzando i microservizi**

* Integra le applicazioni in una serie di microservizi cooperativi in Red Hat OpenShift on IBM Cloud in base alle aree funzionali dell'applicazione e delle sue dipendenze.
* Distribuisci le applicazioni nei contenitori in Red Hat OpenShift on IBM Cloud.
* Fornisci dashboard DevOps standardizzati attraverso Kubernetes.
* Abilita il ridimensionamento su richiesta del calcolo per i carichi di lavoro batch e di altri inventari che vengono eseguiti raramente.
* Utilizza {{site.data.keyword.messagehub_full}} per gestire la trasmissione dei dati dai dispositivi IoT.

**Passo 2: garantisci la disponibilità globale**
* Gli strumenti HA integrati in Red Hat OpenShift on IBM Cloud bilanciano il carico di lavoro all'interno di ogni regione geografica, compresi la riparazione automatica e il bilanciamento del carico.
* Il bilanciamento del carico, i firewall e il DNS sono gestiti da IBM Cloud Internet Services.
* Utilizzando le toolchain e gli strumenti di distribuzione Helm, le applicazioni vengono anche distribuite ai cluster in tutto il mondo, quindi i carichi di lavoro e i dati soddisfano i requisiti regionali.

**Passo 3: condividi i dati**
* {{site.data.keyword.cos_full}} con {{site.data.keyword.messagehub_full}} fornisce l'archiviazione di dati cronologici e in tempo reale.
* Le API consentono ai clienti della società di spedizione di condividere i dati nelle loro applicazioni.

**Passo 4: consegna in modo continuo**
* {{site.data.keyword.contdelivery_full}} aiuta gli sviluppatori a fornire rapidamente una toolchain integrata, utilizzando template personalizzabili e condivisibili con gli strumenti di IBM, terze parti e open source. Automatizza i processi di build e di test, controllando la qualità con l'analisi.
* Dopo che gli sviluppatori hanno creato e testato le applicazioni nei propri cluster di sviluppo e test, utilizzano le toolchain CI/CD di IBM per distribuire le applicazioni nei cluster in tutto il mondo.
* Red Hat OpenShift on IBM Cloud fornisce un facile rollout e roll-back delle applicazioni; vengono distribuite applicazioni personalizzate per soddisfare i requisiti regionali attraverso l'instradamento e il bilanciamento del carico intelligenti di Istio.

**Risultati**

* Con Red Hat OpenShift on IBM Cloud e gli strumenti CI/CD di IBM, le versioni regionali delle applicazioni sono ospitate vicino ai dispositivi fisici da cui raccolgono i dati.
* I microservizi riducono notevolmente i tempi di consegna di patch, correzioni di bug e nuove funzioni. Lo sviluppo iniziale è veloce e gli aggiornamenti sono frequenti.
* I clienti di spedizione hanno accesso in tempo reale alle posizioni delle spedizioni, alle pianificazioni di consegna e persino ai registri portuali approvati.
* I partner di transito presso vari terminali di spedizione sono a conoscenza dei manifesti di carico e dei dettagli della spedizione, in modo che la logistica in loco sia migliorata, anziché ritardata.
* Separatamente da questo articolo, [Maersk e IBM hanno costituito una joint venture](https://www.ibm.com/press/us/en/pressrelease/53602.wss) per migliorare le catene di fornitura internazionali con Blockchain.

## La compagnia aerea fornisce un innovativo sito di indennità per le risorse umane (HR) in meno di 3 settimane
{: #uc_airline}

Un responsabile delle risorse umane (CHRO) ha bisogno di un nuovo sito di indennità per le risorse umane con un chatbot innovativo, ma gli strumenti e le piattaforme di sviluppo correnti implicano lunghi tempi di esecuzione per l'attivazione delle applicazioni. Questa situazione include lunghe attese per l'acquisto dell'hardware.
{: shortdesc}

Perché {{site.data.keyword.cloud_notm}}: Red Hat OpenShift on IBM Cloud fornisce una facile attivazione del calcolo. Quindi, gli sviluppatori possono sperimentare facilmente, distribuendo rapidamente le modifiche nei sistemi di sviluppo e test con toolchain aperte. I loro strumenti di sviluppo software tradizionali ottengono una marcia in più quando aggiungono IBM Watson Assistant. Il nuovo sito di indennità è stato creato in meno di 3 settimane.

Tecnologie chiave:    
* [Cluster che si adattano a diverse esigenze di CPU, RAM e archiviazione](/docs/containers?topic=containers-planning_worker_nodes#planning_worker_nodes)
* [Servizio chatbot con tecnologia Watson](https://developer.ibm.com/code/patterns/create-cognitive-banking-chatbot/)
* [Strumenti nativi DevOps, incluse le toolchain aperte in {{site.data.keyword.contdelivery_full}}](https://www.ibm.com/cloud/garage/toolchains/)
* [SDK per Node.js](/docs/runtimes/nodejs?topic=Nodejs-nodejs_runtime#nodejs_runtime)

**Contesto: creazione e distribuzione rapida di un innovativo sito di indennità HR in meno di 3 settimane**
* La crescita dei dipendenti e il cambiamento delle politiche HR hanno comportato la necessità di un nuovo sito per l'iscrizione annuale.
* Erano previste funzioni interattive, come un chatbot, per aiutare a comunicare le nuove politiche HR ai dipendenti esistenti.
* A causa della crescita del numero di dipendenti, il traffico del sito è in aumento, ma il budget dell'infrastruttura rimane invariato.
* Il team delle risorse umane ha dovuto affrontare la pressione di muoversi più velocemente: presentare rapidamente le funzioni del nuovo sito e pubblicare frequentemente le modifiche alle indennità dell'ultimo minuto.
* Il periodo di iscrizione dura due settimane e pertanto non sono tollerati tempi di inattività per la nuova applicazione.

**Soluzione**

La compagnia aerea vuole progettare una cultura aperta che metta le persone al primo posto. Il responsabile delle risorse umane è ben consapevole che l'attenzione a premiare e conservare le persone di talento influisce sulla redditività della compagnia aerea. Pertanto, l'introduzione annuale delle indennità è un aspetto chiave della promozione di una cultura incentrata sul dipendente.

Hanno bisogno di una soluzione che aiuti gli sviluppatori e i loro utenti:
* FRONT-END ALLE INDENNITÀ ESISTENTI: assicurazione, offerte educative, benessere e altro
* FUNZIONI SPECIFICHE DELLA REGIONE: ogni paese ha politiche HR univoche per cui il sito globale potrebbe sembrare simile ma mostra vantaggi specifici per regione
* STRUMENTI PER LO SVILUPPATORE che accelerano il rollout di funzioni e correzioni di bug
* CHATBOT per fornire conversazioni autentiche relative alle indennità e risolvere le richieste e le domande degli utenti in modo efficiente.

Soluzione tecnica:
* Red Hat OpenShift on IBM Cloud
* IBM Watson Assistant and Tone Analyzer
* {{site.data.keyword.contdelivery_full}}
* IBM Logging and Monitoring
* {{site.data.keyword.SecureGatewayfull}}
* {{site.data.keyword.appid_full_notm}}

Lo sviluppo accelerato è una vittoria fondamentale per il responsabile delle risorse umane. Il team ha iniziato caricando le applicazioni in un contenitore e inserendole nel cloud. Con l'uso di moderni contenitori, gli sviluppatori possono sperimentare facilmente con l'SDK Node.js SDK e distribuire le modifiche nei sistemi di sviluppo e test, che vengono ridimensionati su cluster separati. Queste distribuzioni sono state automatizzate con le toolchain aperte e {{site.data.keyword.contdelivery_full}}. Gli aggiornamenti al sito HR non languivano più in processi di build lenti e soggetti a errori. Gli sviluppatori possono fornire aggiornamenti incrementali al loro sito, tutti i giorni o anche più frequentemente.  Inoltre, la registrazione e il monitoraggio per il sito HR si integrano rapidamente, in particolare per il modo in cui il sito estrae dati personalizzati dai sistemi di indennità di back-end. Gli sviluppatori non sprecano tempo a creare sistemi di registrazione complessi, solo per essere in grado di risolvere i problemi dei sistemi attivi. Gli sviluppatori non hanno bisogno di diventare esperti di sicurezza cloud; possono facilmente implementare un'autenticazione controllata dalle politiche utilizzando {{site.data.keyword.appid_full_notm}}.

Con Red Hat OpenShift on IBM Cloud, sono passati dall'hardware sovradimensionato in un data center privato al calcolo personalizzabile che riduce le operazioni IT, la manutenzione e l'energia. Per ospitare il sito HR, sono riusciti a progettare facilmente cluster Kubernetes per soddisfare le loro esigenze di CPU, RAM e archiviazione. Un altro fattore per la riduzione dei costi del personale è che IBM gestisce Kubernetes, quindi gli sviluppatori possono concentrarsi sulla realizzazione di una migliore esperienza dei dipendenti per l'iscrizione alle indennità.

Red Hat OpenShift on IBM Cloud fornisce risorse di calcolo scalabili e i dashboard DevOps associati per creare, ridimensionare e rimuovere applicazioni e servizi su richiesta. Utilizzando la tecnologia dei contenitori standard del settore, le applicazioni possono essere rapidamente sviluppate e condivise in più ambienti di sviluppo, test e produzione. Questa configurazione offre il vantaggio immediato della scalabilità. Utilizzando la ricca serie di oggetti di distribuzione e di runtime di Kubernetes, il team delle risorse umane può monitorare e gestire gli aggiornamenti alle applicazioni in modo affidabile. Possono anche replicare e ridimensionare le applicazioni, utilizzando regole definite e l'orchestratore automatizzato di Kubernetes.

**Passo 1: contenitori, microservizi e Garage Method**
* Le applicazioni vengono create in una serie di microservizi cooperativi eseguiti in Red Hat OpenShift on IBM Cloud. L'architettura rappresenta le aree funzionali dell'applicazione con i maggiori problemi di qualità.
* Distribuisci le applicazioni nel contenitore in Red Hat OpenShift on IBM Cloud, scansionato continuamente con IBM Vulnerability Advisor.
* Fornisci dashboard DevOps standardizzati attraverso Kubernetes.
* Adotta le procedure di sviluppo agili e iterative essenziali all'interno di IBM Garage Method per consentire frequenti rilasci di nuove funzioni, patch e correzioni senza tempi di inattività.

**Passo 2: connessioni al back-end di indennità esistente**
* {{site.data.keyword.SecureGatewayfull}} viene utilizzato per creare un tunnel sicuro ai sistemi installati in loco che ospitano i sistemi di indennità.  
* La combinazione di dati in loco e Red Hat OpenShift on IBM Cloud consente l'accesso ai dati sensibili aderendo al contempo alle normative.
* Le conversazioni chatbot sono state inserite nelle politiche HR, consentendo al sito di indennità di riportare quali sono state le indennità più o meno popolari, compresi i miglioramenti mirati a iniziative con scarso rendimento.

**Passo 3: chatbot e personalizzazione**
* IBM Watson Assistant fornisce strumenti per strutturare rapidamente un chatbot in grado di fornire agli utenti le giuste informazioni sulle indennità.
* Watson Tone Analyzer assicura che i clienti siano soddisfatti con le conversazioni chatbot e richiedano l'intervento umano quando necessario.

**Passo 4: consegna in modo continuo in tutto il mondo**
* {{site.data.keyword.contdelivery_full}} aiuta gli sviluppatori a fornire rapidamente una toolchain integrata, utilizzando template personalizzabili e condivisibili con gli strumenti di IBM, terze parti e open source. Automatizza i processi di build e di test, controllando la qualità con l'analisi.
* Dopo che gli sviluppatori hanno creato e testato le applicazioni nei propri cluster di sviluppo e test, utilizzano le toolchain CI/CD di IBM per distribuire le applicazioni nei cluster di produzione in tutto il mondo.
* Red Hat OpenShift on IBM Cloud fornisce un facile rollout e roll-back delle applicazioni. Vengono distribuite applicazioni personalizzate per soddisfare i requisiti regionali attraverso l'instradamento e il bilanciamento del carico intelligenti di Istio.
* Gli strumenti HA integrati in Red Hat OpenShift on IBM Cloud bilanciano il carico di lavoro all'interno di ogni regione geografica, compresi la riparazione automatica e il bilanciamento del carico.

**Risultati**
* Con strumenti come il chatbot, il team delle risorse umane ha dimostrato alla propria forza lavoro che l'innovazione faceva parte della cultura aziendale e non era solo una parole in voga.
* L'autenticità con la personalizzazione nel sito ha affrontato le mutevoli aspettative della forza lavoro della compagnia aerea attuale.
* Gli aggiornamenti dell'ultimo minuto del sito HR, compresi quelli guidati dalle conversazioni chatbot dei dipendenti, sono stati pubblicati rapidamente perché gli sviluppatori hanno distribuito modifiche almeno 10 volte al giorno.
* Con la gestione dell'infrastruttura curata da IBM, il team di sviluppo è stato libero di consegnare il sito in sole 3 settimane.


