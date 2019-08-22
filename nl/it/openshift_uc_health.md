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

# Casi di utilizzo di assistenza sanitaria per {{site.data.keyword.cloud_notm}}
{: #cs_uc_health}

Questi casi di utilizzo evidenziano come i carichi di lavoro su {{site.data.keyword.openshiftlong}} traggono vantaggio dal cloud pubblico. Garantiscono un calcolo sicuro su bare metal isolato, la facile attivazione dei cluster per uno sviluppo più rapido, la migrazione da macchine virtuali e la condivisione dei dati nei database cloud.
{: shortdesc}


## Il fornitore di assistenza sanitaria migra i carichi di lavoro da VM inefficienti a contenitori operativi per i sistemi di reporting e gestione dei pazienti.
{: #uc_migrate}

Un responsabile IT per un fornitore di assistenza sanitaria dispone di sistemi aziendali di reporting e gestione dei pazienti installati in loco. Questi sistemi hanno lenti cicli di miglioramento, che portano a livelli di servizio stagnanti per i pazienti. 
{: shortdesc}

Perché {{site.data.keyword.cloud_notm}}: per migliorare il servizio dei pazienti, il fornitore ha cercato Red Hat OpenShift on IBM Cloud e {{site.data.keyword.contdelivery_full}} per ridurre la spesa IT e accelerare lo sviluppo, il tutto su una piattaforma sicura. I sistemi SaaS ad alto utilizzo del fornitore, che contenevano sia i sistemi di registrazione dei pazienti che le applicazioni di report aziendali, necessitavano di aggiornamenti frequenti.  Inoltre, gli sviluppatori del fornitore erano sopraffatti dall'occuparsi loro stessi dell'amministrazione dell'hardware, della rete e anche dello stack Kubernetes. Il fornitore voleva anche contrastare l'aumento del costo del lavoro e un budget in diminuzione.

Tecnologie chiave:
* [Cluster che si adattano a diverse esigenze di CPU, RAM e archiviazione](/docs/containers?topic=containers-planning_worker_nodes#planning_worker_nodes)
* [Adattamento orizzontale](/docs/containers?topic=containers-app#highly_available_apps)
* [Sicurezza e isolamento dei contenitori](/docs/containers?topic=containers-security#security) 
* [{{site.data.keyword.icp4dfull_notm}}](https://www.ibm.com/products/cloud-pak-for-data)
* [Strumenti nativi DevOps, incluse le toolchain aperte in {{site.data.keyword.contdelivery_full}}](https://www.ibm.com/cloud/garage/toolchains/)
* [SDK per Node.js](/docs/runtimes/nodejs?topic=Nodejs-nodejs_runtime#nodejs_runtime)
* [Funzionalità di accesso senza modificare il codice applicativo utilizzando {{site.data.keyword.appid_short_notm}}](/docs/services/appid?topic=appid-getting-started)

Hanno iniziato caricando i propri sistemi SaaS in un contenitore e inserendoli nel cloud. Da quel primo passo, sono passati dall'hardware sovradimensionato in un data center privato al calcolo personalizzabile che riduce le operazioni IT, la manutenzione e l'energia. Per ospitare le applicazioni SaaS, hanno progettato facilmente cluster Kubernetes per soddisfare le loro esigenze di CPU, RAM e archiviazione. Hanno utilizzato {{site.data.keyword.icp4dfull_notm}} per fornire gli strumenti di analisi familiari dal loro ambiente in loco. Un altro fattore per la riduzione dei costi del personale è che IBM gestisce Kubernetes, quindi il fornitore può concentrarsi sulla fornitura di un servizio clienti migliore. 

Lo sviluppo accelerato è una vittoria fondamentale per il responsabile IT. Con il passaggio al cloud pubblico, gli sviluppatori possono sperimentare facilmente con l'SDK Node.js, distribuendo le modifiche nei sistemi di sviluppo e test, ridimensionati su cluster separati. Queste distribuzioni sono state automatizzate con le toolchain aperte e {{site.data.keyword.contdelivery_full}}. Gli aggiornamenti al sistema SaaS non sono più rallentati da processi di build lenti e soggetti a errori. Gli sviluppatori possono fornire aggiornamenti incrementali ai loro utenti, tutti i giorni o anche più frequentemente.  Inoltre, la registrazione e il monitoraggio per i sistemi SaaS, in particolare l'interazione tra i report di front-end e back-end dei pazienti, si integrano rapidamente nel sistema. Gli sviluppatori non sprecano tempo a creare sistemi di registrazione complessi, solo per essere in grado di risolvere i problemi dei sistemi attivi.

La sicurezza prima di tutto: con bare metal per Red Hat OpenShift on IBM Cloud, i carichi di lavoro sensibili dei pazienti ora hanno un isolamento familiare ma all'interno della flessibilità del cloud pubblico. Da tale nucleo, Vulnerability Advisor fornisce la scansione:
* Scansione dei punti vulnerabili delle immagini
* Scansione delle politiche basata su ISO 27k
* Scansione dei contenitori attivi
* Scansione dei pacchetti per malware noti

Proteggere i dati dei pazienti fa sì che i pazienti siano più felici.

**Contesto: migrazione del carico di lavoro per il fornitore di assistenza sanitaria**

* Il debito tecnico, che è accompagnato da lunghi cicli di rilascio, ostacola i sistemi aziendali di reporting e gestione dei pazienti del fornitore.
* Le loro applicazioni personalizzate per back-office e front-office vengono consegnate in loco in immagini di macchine virtuali monolitiche.
* Hanno bisogno di rivedere i loro processi, metodi e strumenti ma non sanno bene da dove cominciare.
* Il loro debito tecnico è in crescita a causa dell'incapacità di rilasciare software di qualità per stare al passo con le richieste del mercato.
* La sicurezza è una preoccupazione primaria e questo problema si aggiunge alla difficoltà di consegna, che causa ancora più ritardi.
* I budget di spesa capitale sono sotto stretto controllo e l'IT ritiene di non disporre del budget o dello staff per creare scenari di test e preparazione necessari con i propri sistemi interni.

**Modello di soluzione**

Servizi I/O, archiviazione e calcolo su richiesta eseguiti nel cloud pubblico con accesso sicuro alle risorse aziendali in loco. Implementare un processo CI/CD e altre parti di IBM Garage Method per ridurre drasticamente i cicli di consegna.

**Passo 1: protezione della piattaforma di calcolo**
* Da tale nucleo, Vulnerability Advisor fornisce la scansione dei punti vulnerabili di immagini, politiche, contenitori e pacchetti per rilevare malware noti.
* Implementa in modo congruente l'autenticazione controllata dalle politiche ai tuoi servizi e alle tue API con una semplice annotazione Ingress. Con la sicurezza dichiarativa, puoi garantire l'autenticazione degli utenti e la convalida dei token utilizzando {{site.data.keyword.appid_short_notm}}.

**Passo 2: migrazione (Lift and shift)**
* Migra le immagini della macchina virtuale nelle immagini del contenitore eseguite in Red Hat OpenShift on IBM Cloud nel cloud pubblico.
* Distribuisci {{site.data.keyword.icp4dfull_notm}}, in modo che gli sviluppatori abbiano i loro strumenti di analisi familiari sul cloud.
* Fornisci procedure e dashboard DevOps standardizzati attraverso Kubernetes.
* Abilita il ridimensionamento su richiesta del calcolo per carichi di lavoro batch e di altro tipo di back-office che vengono eseguiti raramente.
* Utilizza {{site.data.keyword.SecureGatewayfull}} per mantenere connessioni sicure ai DBMS installati in loco.
* I costi capitali del data center privato/in loco sono notevolmente ridotti e sostituiti con un modello di calcolo a tempo che si adatta in base alla domanda di carico di lavoro.

**Passo 3: microservizi e Garage Method**
* Riprogetta le applicazioni in una serie di microservizi cooperativi. Questa serie viene eseguita all'interno di Red Hat OpenShift on IBM Cloud che si basa su aree funzionali dell'applicazione con i maggiori problemi di qualità.
* Utilizza {{site.data.keyword.cloudant}} con le chiavi fornite dal cliente per memorizzare i dati della cache nel cloud.
* Adotta le procedure di integrazione e fornitura continua (CI/CD) in modo che gli sviluppatori creino e rilascino un microservizio sulla propria pianificazione secondo necessità. {{site.data.keyword.contdelivery_full}} fornisce toolchain del flusso di lavoro per il processo CI/CD insieme alla creazione di immagini e alla scansione delle vulnerabilità delle immagini del contenitore.
* Adotta le procedure di sviluppo agili e iterative di IBM Garage Method per consentire frequenti rilasci di nuove funzioni, patch e correzioni senza tempi di inattività.

**Soluzione tecnica**
* Red Hat OpenShift on IBM Cloud 
* {{site.data.keyword.icp4dfull_notm}}
* {{site.data.keyword.cloudant}}
* {{site.data.keyword.SecureGatewayfull}}
* {{site.data.keyword.appid_short_notm}}

Per i carichi di lavoro più sensibili, i cluster possono essere ospitati in Red Hat OpenShift on IBM Cloud per Bare Metal.  Utilizzando la tecnologia dei contenitori standard del settore, le applicazioni possono essere inizialmente riospitate su Red Hat OpenShift on IBM Cloud in modo rapido senza importanti modifiche architetturali. Questa modifica offre il vantaggio immediato della scalabilità.

Possono replicare e ridimensionare le applicazioni, utilizzando regole definite e l'orchestratore automatizzato di Kubernetes. Red Hat OpenShift on IBM Cloud fornisce risorse di calcolo scalabili e i dashboard DevOps associati per creare, ridimensionare e rimuovere applicazioni e servizi su richiesta. Utilizzando gli oggetti di distribuzione e di runtime di Kubernetes, il fornitore può monitorare e gestire gli aggiornamenti alle applicazioni in modo affidabile.

{{site.data.keyword.SecureGatewayfull}} viene utilizzato per creare una pipeline sicura per database e documenti in loco per le applicazioni che vengono riospitate per l'esecuzione in Red Hat OpenShift on IBM Cloud 

{{site.data.keyword.cloudant}} è un moderno database NoSQL adatto a una serie di casi di utilizzo basati sui dati, dall'archiviazione e query di dati chiave-valore all'archiviazione e query di dati complessi orientati ai documenti. Per ridurre al minimo le query al sistema RDBMS di back-office, {{site.data.keyword.cloudant}} viene utilizzato per memorizzare nella cache i dati della sessione dell'utente tra le applicazioni. Queste scelte migliorano l'usabilità e le prestazioni dell'applicazione di front-end in tutte le applicazioni su Red Hat OpenShift on IBM Cloud.

Spostare i carichi di lavoro di calcolo in {{site.data.keyword.cloud_notm}} non è comunque sufficiente. Il fornitore deve anche passare attraverso una trasformazione di processi e metodi. Adottando le procedure di IBM Garage Method, il fornitore può implementare un processo di consegna agile e iterativo che supporta le moderne procedure di DevOps come CI/CD.

Gran parte dello stesso processo CI/CD è automatizzato con il servizio IBM Continuous Delivery nel cloud. Il fornitore può definire toolchain del flusso di lavoro per preparare le immagini del contenitore, verificare la presenza di vulnerabilità e distribuirle nel cluster Kubernetes.

**Risultati**
* Lo spostamento delle VM monolitiche esistenti nei contenitori ospitati nel cloud è stato il primo passo che ha consentito al fornitore di risparmiare sui costi di capitale e iniziare a conoscere le moderne procedure di DevOps. 
* Con il Cloud Pak distribuito, il fornitore ha scaricato il supporto stack completo dei suoi strumenti di analisi dei dati su IBM, compresa la gestione del ciclo di vita di tali strumenti. I suoi sviluppatori non hanno quindi più dovuto occuparsi delle attività operative, potendo concentrarsi sulle nuove funzioni e sugli aggiornamenti. 
* La riprogettazione delle applicazioni monolitiche chiave in una serie di microservizi dettagliati ha ridotto notevolmente i tempi di consegna di patch, correzioni di bug e nuove funzioni.
* In parallelo, il fornitore ha implementato semplici iterazioni a tempo fisso per ottenere la gestione del debito tecnico esistente.

## La ricerca no-profit ospita in modo sicuro dati sensibili mentre cresce la ricerca con i partner
{: #uc_research}

Un responsabile dello sviluppo per una ricerca no-profit sulle malattie ha ricercatori accademici e del settore che non possono condividere facilmente i dati di ricerca. Invece, il loro lavoro è isolato in poche aree nel mondo a causa delle normative regionali sulla conformità e dei database centralizzati.
{: shortdesc}

Perché {{site.data.keyword.cloud_notm}}: Red Hat OpenShift on IBM Cloud offre un calcolo sicuro in grado di ospitare l'elaborazione di dati sensibili e performanti su una piattaforma aperta. Questa piattaforma globale è ospitata nelle regioni vicine. Quindi è legato alle normative locali che ispirano la fiducia dei pazienti e dei ricercatori il fatto che i loro dati siano protetti localmente e facciano la differenza ottenendo migliori risultati sanitari.

Tecnologie chiave:
* [La pianificazione intelligente posiziona i carichi di lavoro dove necessario](/docs/containers?topic=containers-regions-and-zones#regions-and-zones)
* [{{site.data.keyword.cloudant}} per mantenere e sincronizzare i dati tra le applicazioni](/docs/services/Cloudant?topic=cloudant-getting-started#getting-started)
* [Scansione e isolamento delle vulnerabilità per i carichi di lavoro](/docs/services/Registry?topic=va-va_index#va_index)
* [Strumenti nativi DevOps, incluse le toolchain aperte in {{site.data.keyword.contdelivery_full}}](https://www.ibm.com/cloud/garage/toolchains/)
* [{{site.data.keyword.openwhisk}} per ripulire i dati e informare i ricercatori sulle modifiche alla struttura dei dati](/docs/openwhisk?topic=cloud-functions-pkg_cloudant#openwhisk_cloudant)

**Contesto: hosting e condivisione sicura dei dati sulle malattie per la ricerca no-profit**

* Diversi gruppi di ricercatori di varie istituzioni non hanno un modo unificato per condividere i dati, il che rallenta la collaborazione.
* La preoccupazione per la sicurezza si aggiunge alla difficoltà di collaborazione che causa una ricerca ancora meno condivisa.
* Sviluppatori e ricercatori sono sparsi in tutto il mondo e oltre i confini organizzativi, il che rende PaaS e SaaS l'opzione migliore per ogni gruppo di utenti.
* Le differenze regionali nelle normative sanitarie richiedono che alcuni dati e l'elaborazione dei dati restino all'interno di quella determinata regione.

**Soluzione**

La ricerca no-profit vuole aggregare i dati della ricerca sul cancro in tutto il mondo. Così creano una divisione dedicata alle soluzioni per i loro ricercatori:
* ACQUISIRE - Applicazioni per acquisire dati di ricerca. I ricercatori oggi utilizzano fogli di calcolo, documenti, prodotti commerciali e database proprietari o di produzione propria per registrare i risultati della ricerca. È improbabile che questa situazione cambi con il tentativo del no-profit di centralizzare l'analisi dei dati.
* ANONIMIZZARE - Applicazioni per rendere anonimi i dati. È necessario rimuovere la SPI per rispettare le normative sanitarie regionali.
* ANALIZZARE - Applicazioni per analizzare i dati. Lo schema di base è archiviare i dati in un formato normale e quindi interrogarli ed elaborarli utilizzando la tecnologia di AI e machine learning (ML), regressioni semplici e così via.

I ricercatori hanno bisogno di affiliarsi con un cluster regionale e le applicazioni devono acquisire, trasformare e rendere anonimi i dati:
1. Sincronizzazione dei dati resi anonimi tra i cluster regionali o spedizione a un archivio dati centralizzato
2. Elaborazione dei dati, utilizzando ML come PyTorch su nodi di lavoro bare metal che forniscono GPU

**ACQUISIRE** {{site.data.keyword.cloudant}} viene utilizzato in ogni cluster regionale che memorizza i documenti ricchi di dati dei ricercatori che possono essere interrogati ed elaborati secondo necessità. {{site.data.keyword.cloudant}} crittografa i dati inattivi e in transito, il che rispetta le leggi regionali sulla privacy dei dati.

{{site.data.keyword.openwhisk}} viene utilizzato per creare funzioni di elaborazione che acquisiscono i dati di ricerca e li memorizzano come documenti di dati strutturati in {{site.data.keyword.cloudant}}. {{site.data.keyword.SecureGatewayfull}} fornisce a {{site.data.keyword.openwhisk}} un modo semplice di accedere ai dati in loco in modo sicuro e protetto.

Le applicazioni web nei cluster regionali sono sviluppate in nodeJS per l'immissione manuale dei dati dei risultati, della definizione dello schema e dell'affiliazione delle organizzazioni di ricerca. IBM Key Protect aiuta a proteggere l'accesso ai dati di {{site.data.keyword.cloudant}} e IBM Vulnerability Advisor esegue la scansione di contenitori e immagini delle applicazioni per identificare gli exploit di sicurezza.

**ANONIMIZZARE** Ogni volta che un nuovo documento di dati viene memorizzato in {{site.data.keyword.cloudant}}, viene attivato un evento e una funzione cloud rende anonimi i dati e rimuove SPI dal documento di dati. Questi documenti di dati anonimi sono memorizzati separatamente dai dati "non elaborati" che vengono acquisiti e sono gli unici documenti che vengono condivisi tra le regioni per l'analisi.

**ANALIZZARE** I framework di machine learning richiedono un uso intensivo di calcolo e quindi l'organizzazione no-profit ha configurato un cluster di elaborazione globale di nodi di lavoro bare metal. A questo cluster di elaborazione globale è associato un database aggregato {{site.data.keyword.cloudant}} dei dati resi anonimi. Un lavoro cron attiva periodicamente una funzione cloud per distribuire i documenti di dati anonimi dai centri regionali all'istanza {{site.data.keyword.cloudant}} del cluster di elaborazione globale.

Il cluster di calcolo esegue il framework di ML PyTorch e le applicazioni di machine learning sono scritte in Python per analizzare i dati aggregati. Oltre alle applicazioni di ML, i ricercatori del gruppo collettivo sviluppano anche le proprie applicazioni che possono essere pubblicate ed eseguite sul cluster globale.

L'organizzazione no-profit fornisce anche applicazioni che vengono eseguite su nodi non bare metal del cluster globale. Le applicazioni visualizzano ed estraggono i dati aggregati e l'output dell'applicazione di ML. Queste applicazioni sono accessibili da un endpoint pubblico, che è protetto dal gateway API nel mondo. Quindi, i ricercatori e gli analisti di dati di tutto il mondo possono scaricare serie di dati ed eseguire le proprie analisi.

**Host di carichi di lavoro di ricerca su Red Hat OpenShift on IBM Cloud**

Gli sviluppatori hanno iniziato distribuendo le loro applicazioni SaaS per la condivisione delle ricerche in contenitori con Red Hat OpenShift on IBM Cloud. Hanno creato cluster per un ambiente di sviluppo che consentono agli sviluppatori di tutto il mondo di distribuire rapidamente e in modo collaborativo i miglioramenti alle applicazioni.

La sicurezza prima di tutto: il responsabile dello sviluppo ha scelto bare metal per ospitare i cluster di ricerca. Con bare metal per Red Hat OpenShift on IBM Cloud, i carichi di lavoro di ricerca sensibili ora hanno un isolamento familiare ma all'interno della flessibilità del cloud pubblico. Poiché questa organizzazione no-profit collabora anche con aziende farmaceutiche, la sicurezza delle applicazioni è fondamentale. La concorrenza è agguerrita e lo spionaggio aziendale è possibile. Da tale nucleo sicuro, Vulnerability Advisor fornisce la scansione:
* Scansione dei punti vulnerabili delle immagini
* Scansione delle politiche basata su ISO 27k
* Scansione dei contenitori attivi
* Scansione dei pacchetti per malware noti

Applicazioni di ricerca protette portano ad una maggiore partecipazione alla sperimentazione clinica.

Per ottenere la disponibilità globale, i sistemi di sviluppo, test e produzione vengono distribuiti in tutto il mondo in diversi data center. Per l'alta disponibilità (HA), usano una combinazione di cluster in più regioni geografiche e cluster multizona. Possono facilmente distribuire l'applicazione di ricerca ai cluster di Francoforte per conformarsi alla normativa europea locale. Distribuiscono l'applicazione anche nei cluster degli Stati Uniti per garantire la disponibilità e il ripristino in locale. Inoltre, diffondono il carico di lavoro di ricerca tra i cluster multizona di Francoforte per garantire che l'applicazione europea sia disponibile e bilanci anche il carico di lavoro in modo efficiente. Poiché i ricercatori caricano dati sensibili con l'applicazione per la condivisione delle ricerche, i cluster dell'applicazione sono ospitati in regioni in cui si applicano normative più severe.

Gli sviluppatori si concentrano sui problemi di dominio, utilizzando gli strumenti esistenti: anziché scrivere un codice ML univoco, la logica ML viene inserita nelle applicazioni, eseguendo il bind dei servizi {{site.data.keyword.cloud_notm}} ai cluster. Gli sviluppatori vengono inoltre liberati dalle attività di gestione dell'infrastruttura perché IBM si occupa di Kubernetes e degli aggiornamenti dell'infrastruttura, della sicurezza e altro ancora.

**Soluzione**

Kit starter Node, archiviazione e calcolo su richiesta eseguiti nel cloud pubblico con accesso sicuro ai dati di ricerca in tutto il mondo, secondo garanzia. Il calcolo nei cluster è a prova di manomissione e isolato su bare metal.

Soluzione tecnica:
* Red Hat OpenShift on IBM Cloud
* {{site.data.keyword.openwhisk}}
* {{site.data.keyword.cloudant}}
* {{site.data.keyword.SecureGatewayfull}}

**Passo 1: carica le applicazioni in un contenitore utilizzando i microservizi**
* Utilizza il kit starter Node.js di IBM per iniziare subito le attività di sviluppo.
* Struttura le applicazioni in una serie di microservizi cooperativi all'interno di Red Hat OpenShift on IBM Cloud in base alle aree funzionali dell'applicazione e delle sue dipendenze.
* Distribuisci le applicazioni di ricerca nei contenitori in Red Hat OpenShift on IBM Cloud.
* Fornisci dashboard DevOps standardizzati attraverso Kubernetes.
* Abilita il ridimensionamento su richiesta del calcolo per i carichi di lavoro batch e di altre ricerche che vengono eseguiti raramente.
* Utilizza {{site.data.keyword.SecureGatewayfull}} per mantenere connessioni sicure ai database installati in loco esistenti.

**Passo 2: utilizza il calcolo sicuro e performante**
* Le applicazioni di ML che richiedono un calcolo con prestazioni più elevate sono ospitate in Red Hat OpenShift on IBM Cloud su Bare Metal. Questo cluster ML è centralizzato, quindi ogni cluster regionale non ha le spese dei nodi di lavoro bare metal; anche le distribuzioni di Kubernetes sono più facili.
* Vulnerability Advisor fornisce la scansione dei punti vulnerabili di immagini, politiche, contenitori e pacchetti per rilevare malware noti.

**Passo 3: garantisci la disponibilità globale**
* Dopo che gli sviluppatori hanno creato e testato le applicazioni nei propri cluster di sviluppo e test, utilizzano le toolchain CI/CD di IBM per distribuire le applicazioni nei cluster in tutto il mondo.
* Gli strumenti HA integrati in Red Hat OpenShift on IBM Cloud bilanciano il carico di lavoro all'interno di ogni regione geografica, compresi la riparazione automatica e il bilanciamento del carico.
* Con le toolchain e gli strumenti di distribuzione Helm, le applicazioni vengono anche distribuite ai cluster in tutto il mondo, quindi i carichi di lavoro e i dati soddisfano le normative regionali.

**Passo 4: condivisione dei dati**
* {{site.data.keyword.cloudant}} è un moderno database NoSQL adatto a una serie di casi di utilizzo basati sui dati, dall'archiviazione e query di dati chiave-valore all'archiviazione e query di dati complessi orientati ai documenti.
* Per ridurre al minimo le query ai database regionali, {{site.data.keyword.cloudant}} viene utilizzato per memorizzare nella cache i dati della sessione dell'utente tra le applicazioni.
* Questa scelta migliora l'usabilità e le prestazioni dell'applicazione di front-end in tutte le applicazioni su Red Hat OpenShift on IBM Cloud.
* Mentre le applicazioni di lavoro in Red Hat OpenShift on IBM Cloud analizzano i dati in loco e memorizzano i risultati in {{site.data.keyword.cloudant}}, {{site.data.keyword.openwhisk}} reagisce alle modifiche e ripulisce automaticamente i dati sui feed dei dati in entrata.
* Allo stesso modo, è possibile attivare notifiche sui progressi della ricerca in una regione tramite caricamenti di dati in modo che tutti i ricercatori possano usufruire dei nuovi dati.

**Risultati**
* Con i kit starter, Red Hat OpenShift on IBM Cloud e gli strumenti CI/CD di IBM, gli sviluppatori globali lavorano tra le istituzioni e sviluppano collaborativamente le applicazioni di ricerca, con strumenti familiari e interoperabili.
* I microservizi riducono notevolmente i tempi di consegna di patch, correzioni di bug e nuove funzioni. Lo sviluppo iniziale è veloce e gli aggiornamenti sono frequenti.
* I ricercatori hanno accesso ai dati clinici e possono condividerli, rispettando al contempo le normative locali.
* I pazienti che partecipano alla ricerca sulle malattie hanno la certezza che i loro dati siano sicuri e facciano la differenza, quando sono condivisi con grandi team di ricerca.


