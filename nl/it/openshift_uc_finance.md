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

# Casi di utilizzo dei servizi finanziari per {{site.data.keyword.cloud_notm}}
{: #cs_uc_finance}

Questi casi di utilizzo evidenziano come i carichi di lavoro su {{site.data.keyword.openshiftlong}} possano
sfruttare l'alta disponibilità, il calcolo ad alte
prestazione, la facile attivazione dei cluster per uno sviluppo più rapido e l'intelligenza artificiale di {{site.data.keyword.ibmwatson}}.
{: shortdesc}

## La società di prestiti riduce i costi e accelera la conformità normativa
{: #uc_mortgage}

Un VP per il Risk Management di una società di prestiti residenziali elabora 70 milioni di record al giorno, ma il sistema locale è lento e anche impreciso. Le spese IT sono aumentate vertiginosamente perché l'hardware è diventato rapidamente obsoleto e non è stato utilizzato pienamente. Nell'attesa del provisioning hardware, la conformità alle normative rallentava. 
{: shortdesc}

Perché {{site.data.keyword.cloud_notm}}: per migliorare l'analisi dei rischi, la società ha cercato i servizi Red Hat OpenShift on IBM Cloud e IBM Cloud Analytics per ridurre i costi, aumentare la disponibilità a livello mondiale e infine accelerare la conformità alle normative. Con Red Hat OpenShift on IBM Cloud in più regioni, le sue applicazioni di analisi possono essere inserite in un contenitore e distribuite in tutto il mondo, migliorando la disponibilità e rispondendo alle normative locali. Tali distribuzioni sono accelerate con strumenti familiari open source, già parte di Red Hat OpenShift on IBM Cloud.

Red Hat OpenShift on IBM Cloud e tecnologie chiave:
* [Adattamento orizzontale](/docs/containers?topic=containers-app#highly_available_apps)
* [Più regioni per l'alta disponibilità](/docs/containers?topic=containers-regions-and-zones#regions-and-zones)
* [Cluster che si adattano a diverse esigenze di CPU, RAM e archiviazione](/docs/containers?topic=containers-planning_worker_nodes#planning_worker_nodes)
* [Sicurezza e isolamento dei contenitori](/docs/containers?topic=containers-security#security)
* [{{site.data.keyword.cloudant}} per mantenere e sincronizzare i dati tra le applicazioni](/docs/services/Cloudant?topic=cloudant-getting-started#getting-started)
* [SDK per Node.js](/docs/runtimes/nodejs?topic=Nodejs-nodejs_runtime#nodejs_runtime)

**Soluzione**

Hanno iniziato caricando le applicazioni di analisi in un contenitore e inserendole nel cloud. In un attimo, i loro problemi hardware sono svaniti. Sono stati in grado di progettare facilmente cluster Kubernetes per soddisfare le loro esigenze di CPU, RAM, archiviazione e sicurezza ad alte prestazioni. E quando le loro applicazioni di analisi cambiano, possono aggiungere o ridurre le risorse di calcolo senza enormi investimenti in hardware. Con il ridimensionamento orizzontale di Red Hat OpenShift on IBM Cloud, le sue applicazioni si adattano al crescente numero di record, con report normativi più rapidi. Red Hat OpenShift on IBM Cloud fornisce risorse di calcolo elastiche in tutto il mondo che sono sicure e altamente performanti per il pieno utilizzo delle moderne risorse di elaborazione.

Ora queste applicazioni ricevono dati di volume elevato da un data warehouse su {{site.data.keyword.cloudant}}. L'archiviazione basata su cloud in {{site.data.keyword.cloudant}} garantisce una maggiore disponibilità rispetto a quando era bloccata in un sistema installato in loco. Poiché la disponibilità è essenziale, le applicazioni vengono distribuite su data center globali, anche per il DR e per la latenza.

Hanno anche accelerato la loro analisi dei rischi e la conformità. Le loro funzioni di analisi predittiva e di rischio, come i calcoli Monte Carlo, sono ora costantemente aggiornate attraverso distribuzioni agili iterative. L'orchestrazione dei contenitori viene gestita da un Kubernetes gestito in modo da ridurre anche i costi operativi. Infine, l'analisi del rischio per i prestiti è più sensibile ai rapidi cambiamenti del mercato.

**Contesto: conformità e modellazione finanziaria per i prestiti residenziali**

* L'aumento della necessità di una migliore gestione dei rischi finanziari determina un aumento della sorveglianza normativa. Le stesse necessità guidano la revisione associata nei processi di valutazione del rischio e la divulgazione di report regolamentari più dettagliati, integrati e abbondanti.
* Le griglie di calcolo ad alte prestazioni (HPC) sono i componenti chiave dell'infrastruttura per la modellazione finanziaria.

Il problema della società in questo momento è il ridimensionamento e il tempo di consegna.

Il loro ambiente attuale ha più di 7 anni, è installato in loco e ha una capacità di calcolo, archiviazione e I/O limitata.
Gli aggiornamenti del server sono costosi e richiedono molto tempo.
Gli aggiornamenti di software e applicazioni seguono un processo informale e non sono ripetibili.
La griglia HPC effettiva è difficile da programmare. L'API è troppo complessa per i nuovi sviluppatori che vengono contrattati e richiede conoscenze non documentate.
Inoltre, il completamento dei principali aggiornamenti delle applicazioni richiede da 6 a 9 mesi.

**Modello di soluzione: servizi I/O, archiviazione e calcolo su richiesta eseguiti nel cloud pubblico con accesso sicuro alle risorse aziendali in loco in base alle necessità**

* Archiviazione di documenti sicura e scalabile che supporta query di documenti strutturati e non strutturati
* Migrazione "lift and shift" di risorse e applicazioni aziendali esistenti quando è abilitata l'integrazione ad alcuni sistemi in loco che non verranno migrati
* Ridurre i tempi di distribuzione delle soluzioni e implementare i processi DevOps e di monitoraggio standard per risolvere i bug che influiscono sulla precisione dei report

**Soluzione dettagliata**

* Red Hat OpenShift on IBM Cloud
* {{site.data.keyword.cos_full_notm}}
* {{site.data.keyword.sqlquery_notm}} (Spark)
* {{site.data.keyword.cloudant}}
* {{site.data.keyword.SecureGateway}}

Red Hat OpenShift on IBM Cloud fornisce risorse di calcolo scalabili e i dashboard DevOps associati per creare, ridimensionare e rimuovere applicazioni e servizi su richiesta. Utilizzando i contenitori standard del settore, le applicazioni possono essere inizialmente riospitate su Red Hat OpenShift on IBM Cloud in modo rapido senza importanti modifiche architetturali.

Questa soluzione offre il vantaggio immediato della scalabilità. Utilizzando la ricca serie di oggetti di distribuzione e di runtime di Kubernetes, la società di prestiti controlla e gestisce gli aggiornamenti alle applicazioni in modo affidabile. Sono anche in grado di replicare e ridimensionare le applicazioni che utilizzano regole definite e l'orchestratore automatizzato di Kubernetes.

{{site.data.keyword.SecureGateway}} viene utilizzato per creare una pipeline sicura per database e documenti in loco per le applicazioni che vengono riospitate per l'esecuzione in Red Hat OpenShift on IBM Cloud 

{{site.data.keyword.cos_full_notm}} è utilizzato per l'archiviazione di tutti i documenti e dati non elaborati man mano che aumentano. Per le simulazioni Monte Carlo, viene implementata una pipeline del flusso di lavoro in cui i dati di simulazione si trovano in file strutturati memorizzati in {{site.data.keyword.cos_full_notm}}. Un trigger per avviare la simulazione ridimensiona i servizi di calcolo in Red Hat OpenShift on IBM Cloud per suddividere i dati dei file in N bucket di eventi per l'elaborazione della simulazione. Red Hat OpenShift on IBM Cloud ridimensiona automaticamente a N esecuzioni del servizio associato e scrive risultati intermedi in {{site.data.keyword.cos_full_notm}}. Questi risultati vengono elaborati da un'altra serie di servizi di calcolo di Red Hat OpenShift on IBM Cloud per produrre i risultati finali.

{{site.data.keyword.cloudant}} è un moderno database NoSQL utile per molti casi di utilizzo basati sui dati: dall'archiviazione e query di dati chiave-valore all'archiviazione e query di dati complessi orientati ai documenti. Per gestire la crescente serie di regole per i report normativi e di gestione, la società di prestiti utilizza {{site.data.keyword.cloudant}} per memorizzare i documenti associati ai dati normativi non elaborati che arrivano nell'azienda. I processi di calcolo su Red Hat OpenShift on IBM Cloud vengono attivati per compilare, elaborare e pubblicare i dati in vari formati di report. I risultati intermedi comuni tra i report sono memorizzati come documenti di {{site.data.keyword.cloudant}} in modo che sia possibile utilizzare i processi basati su template per produrre i report necessari.

**Risultati**

* Le simulazioni finanziarie complesse sono completate nel 25% del tempo rispetto a quanto era possibile in precedenza con i sistemi in loco esistenti.
* Il tempo di distribuzione è migliorato dai precedenti 6 - 9 mesi a una media di 1 - 3 settimane. Questo miglioramento si verifica perché Red Hat OpenShift on IBM Cloud consente un processo disciplinato e controllato per potenziare i contenitori di applicazioni e sostituirli con le versioni più recenti. I bug di report possono essere corretti rapidamente, risolvendo problemi, come la precisione.
* I costi di report normativi sono stati ridotti con una serie di servizi di archiviazione e di calcolo congruente e scalabile offerta da Red Hat OpenShift on IBM Cloud e {{site.data.keyword.cloudant}}.
* Nel tempo, le applicazioni originali inizialmente migrate nel cloud sono state ri-progettate in microservizi cooperativi che vengono eseguiti su Red Hat OpenShift on IBM Cloud. Questa azione ha ulteriormente accelerato lo sviluppo e il tempo di distribuzione e ha consentito ulteriori innovazioni grazie alla relativa facilità di sperimentazione. Hanno inoltre rilasciato applicazioni innovative con versioni più recenti dei microservizi per avvalersi delle condizioni di mercato e di business (ovvero, le applicazioni e i microservizi situazionali).


## La società di gestione dei pagamenti ottimizza la produttività degli sviluppatori, distribuendo ai loro partner strumenti abilitati all'intelligenza artificiale 4 volte più velocemente
{: #uc_payment_tech}

Un responsabile dello sviluppo ha sviluppatori che utilizzano gli strumenti applicativi installati in loco che rallentano la prototipazione nell'attesa di acquisti hardware.
{: shortdesc}

Perché {{site.data.keyword.cloud_notm}}: Red Hat OpenShift on IBM Cloud fornisce l'attivazione di risorse di calcolo utilizzando la tecnologia standard open source. Una volta che la società è passata a Red Hat OpenShift on IBM Cloud, gli sviluppatori hanno accesso agli strumenti compatibili DevOps, come i contenitori portatili e facilmente condivisibili.

Quindi, gli sviluppatori possono sperimentare facilmente, distribuendo rapidamente le modifiche nei sistemi di sviluppo e test con toolchain aperte. I loro strumenti di sviluppo di applicazioni acquisiscono un nuovo aspetto quando aggiungono servizi cloud di intelligenza artificiale alle applicazioni con un clic.

Tecnologie chiave:
* [Cluster che si adattano a diverse esigenze di CPU, RAM e archiviazione](/docs/containers?topic=containers-planning_worker_nodes#planning_worker_nodes)
* [Strumenti nativi DevOps, incluse le toolchain aperte in {{site.data.keyword.contdelivery_full}}](https://www.ibm.com/cloud/garage/toolchains/)
* [IBM Cloud Pak for Applications](https://www.ibm.com/cloud/cloud-pak-for-applications)
* [Prevenzione frodi con 'intelligenza artificiale {{site.data.keyword.watson}}](https://www.ibm.com/cloud/watson-studio)
* [Strumenti nativi DevOps, incluse le toolchain aperte in {{site.data.keyword.contdelivery_full}}](https://www.ibm.com/cloud/garage/toolchains/)
* [SDK per Node.js](/docs/runtimes/nodejs?topic=Nodejs-nodejs_runtime#nodejs_runtime)
* [Funzionalità di accesso senza modificare il codice applicativo utilizzando {{site.data.keyword.appid_short_notm}}](/docs/services/appid?topic=appid-getting-started)

**Contesto: ottimizzazione della produttività degli sviluppatori e distribuzione di strumenti di intelligenza artificiale ai partner 4 volte più velocemente**

* Le interruzioni dilagano nel settore dei pagamenti, con una crescita drammatica sia nel segmento cliente che business-to-business. Ma gli aggiornamenti degli strumenti di pagamento erano lenti.
* Sono necessarie funzioni cognitive per rilevare le transazioni fraudolente in modi nuovi e più veloci.
* Con il crescente numero di partner e delle loro transazioni, il traffico di strumenti aumenta, ma il budget di infrastruttura deve diminuire, massimizzando l'efficienza delle risorse.
* Il loro debito tecnico è in crescita, a causa dell'incapacità di rilasciare software di qualità per stare al passo con le richieste del mercato.
* I budget di spesa capitale sono sotto stretto controllo e l'IT ritiene di non disporre del budget o dello staff per creare scenari di test e preparazione con i propri sistemi interni.
* La sicurezza è sempre più una preoccupazione primaria e questa preoccupazione si aggiunge alla difficoltà di consegna causando ancora più ritardi.

**Soluzione**

Il responsabile dello sviluppo deve affrontare molte sfide nel settore dei pagamenti dinamici. Le normative, i comportamenti dei consumatori, le frodi, i concorrenti e le infrastrutture di mercato si stanno rapidamente evolvendo. Un rapido sviluppo è essenziale per far parte del futuro mondo dei pagamenti.

Il loro modello di business è quello di fornire strumenti di pagamento ai business partner, in modo che possano aiutare queste istituzioni finanziarie e altre organizzazioni a offrire esperienze di pagamento digitali altamente sicure.

Hanno bisogno di una soluzione che aiuti gli sviluppatori e i loro business partner:
* FRONT-END PER STRUMENTI DI PAGAMENTO: sistemi tariffari, tracciamento dei pagamenti che include conformità transfrontaliera, conformità normativa, dati biometrici, rimesse e altro
* FUNZIONI SPECIFICHE DELLA NORMATIVA: ogni paese ha normative univoche per cui la serie di strumenti complessiva potrebbe sembrare simile ma mostra vantaggi specifici per paese
* STRUMENTI PER LO SVILUPPATORE che accelerano il rollout di funzioni e correzioni di bug
* FRAUD DETECTION AS A SERVICE (FDaaS) utilizza l'intelligenza artificiale di {{site.data.keyword.watson}} per restare un passo avanti rispetto alle frequenti e crescenti azioni fraudolente

**Modello di soluzione**

Calcolo su richiesta, strumenti DevOps e intelligenza artificiale eseguiti nel cloud pubblico con accesso a sistemi di pagamento di back-end. Implementare un processo CI/CD per ridurre drasticamente i cicli di consegna.

Soluzione tecnica:
* Red Hat OpenShift on IBM Cloud
* IBM Cloud Pak for Applications
* {{site.data.keyword.contdelivery_full}}
* IBM Cloud Logging and Monitoring
* {{site.data.keyword.ibmwatson_notm}} for Financial Services
* {{site.data.keyword.appid_full_notm}}

Hanno iniziato caricando le VM di strumenti di pagamento in un contenitore e inserendole nel cloud. In un attimo, i loro problemi hardware sono svaniti. Sono stati in grado di progettare facilmente cluster Kubernetes per soddisfare le loro esigenze di CPU, RAM, archiviazione e sicurezza. E quando i loro strumenti di pagamento devono cambiare, possono aggiungere o ridurre le risorse calcolo senza costosi e lenti acquisti di hardware.

Con il ridimensionamento orizzontale di Red Hat OpenShift on IBM Cloud, le sue applicazioni si adattano al crescente numero di partner, con una conseguente crescita più rapida. Red Hat OpenShift on IBM Cloud fornisce risorse di calcolo elastiche in tutto il mondo che sono sicure per il pieno utilizzo delle moderne risorse di elaborazione.

Lo sviluppo accelerato è una vittoria fondamentale per il responsabile. Con l'uso di moderni contenitori, gli sviluppatori possono sperimentare facilmente nei linguaggi di loro scelta, distribuendo le modifiche nei sistemi di sviluppo e test, ridimensionati su cluster separati. Queste distribuzioni sono state automatizzate con le toolchain aperte e {{site.data.keyword.contdelivery_full}}. Gli aggiornamenti agli strumenti non languivano più in processi di build lenti e soggetti a errori. Gli sviluppatori possono fornire aggiornamenti incrementali ai loro strumenti, tutti i giorni o anche più frequentemente.

Inoltre, la registrazione e il monitoraggio per gli strumenti, in particolare dove è stato utilizzato {{site.data.keyword.watson}} AI, si integrano rapidamente nel sistema. Gli sviluppatori non sprecano a tempo a creare sistemi di registrazione complessi, solo per essere in grado di risolvere i problemi dei loro sistemi attivi. Un fattore chiave per la riduzione dei costi di personale è che IBM gestisce Kubernetes, quindi gli sviluppatori possono concentrarsi su strumenti di pagamento migliori.

La sicurezza prima di tutto: con bare metal per Red Hat OpenShift on IBM Cloud, gli strumenti di pagamento sensibili ora hanno un isolamento familiare ma all'interno della flessibilità del cloud pubblico. Le scansioni per vulnerabilità e malware vengono eseguite continuamente.

**Passo 1: migrazione al calcolo sicuro**
* Migra le immagini della macchina virtuale nelle immagini del contenitore eseguite in Red Hat OpenShift on IBM Cloud in {{site.data.keyword.Bluemix_notm}} pubblico.Distribuisci IBM Cloud Pak for Applications, in modo che gli sviluppatori abbiano i loro strumenti di sviluppo di applicazioni familiari sul cloud. 
* Da tale nucleo, Vulnerability Advisor fornisce la scansione dei punti vulnerabili di immagini, politiche, contenitori e pacchetti per rilevare malware noti.
* I costi capitali del data center privato/in loco sono notevolmente ridotti e sostituiti con un modello di calcolo a tempo che si adatta in base alla domanda di carico di lavoro.
* Implementa in modo congruente l'autenticazione controllata dalle politiche ai tuoi servizi e alle tue API con una semplice annotazione Ingress. Con la sicurezza dichiarativa, puoi garantire l'autenticazione degli utenti e la convalida dei token utilizzando {{site.data.keyword.appid_short_notm}}.

**Passo 2: operazioni e connessioni al back-end dei sistemi di pagamento esistenti**
* Utilizza IBM {{site.data.keyword.SecureGateway}} per mantenere connessioni sicure ai restanti sistemi di strumenti installati in loco.
* Fornisci procedure e dashboard DevOps standardizzati attraverso Kubernetes.
* Dopo che gli sviluppatori hanno creato e testato le applicazioni nei cluster di sviluppo e test, utilizzano le toolchain {{site.data.keyword.contdelivery_full}} per distribuire le applicazioni nei cluster di Red Hat OpenShift on IBM Cloud in tutto il mondo.
* Gli strumenti HA integrati in Red Hat OpenShift on IBM Cloud bilanciano il carico di lavoro all'interno di ogni regione geografica, compresi la riparazione automatica e il bilanciamento del carico.

**Passo 3: analisi e prevenzione delle frodi**
* Distribuisci IBM {{site.data.keyword.watson}} for Financial Services per prevenire e rilevare le frodi.
* Utilizzando le toolchain e gli strumenti di distribuzione Helm, le applicazioni vengono anche distribuite ai cluster di Red Hat OpenShift on IBM Cloud in tutto il mondo. Quindi, i carichi di lavoro e i dati rispondono alle normative regionali.

**Risultati**
* Lo spostamento delle VM monolitiche esistenti nei contenitori ospitati nel cloud è stato il primo passo che ha consentito al responsabile dello sviluppo di risparmiare sui costi di capitale e operativi.
* Con la gestione dell'infrastruttura curata da IBM, il team di sviluppo è stato libero di fornire aggiornamenti 10 volte al giorno.
* In parallelo, il fornitore ha implementato semplici iterazioni a tempo fisso per ottenere la gestione del debito tecnico esistente.
* Con il numero di transazioni che elaborano, possono ridimensionare le loro operazioni in modo esponenziale.
* Allo stesso tempo, la nuova analisi delle frodi con {{site.data.keyword.watson}} ha aumentato la velocità di individuazione e prevenzione, riducendo le frodi 4 volte di più rispetto alla media della regione.


