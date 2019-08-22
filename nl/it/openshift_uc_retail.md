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

# Casi di utilizzo di vendita al dettaglio per {{site.data.keyword.cloud_notm}}
{: #cs_uc_retail}

Questi casi di utilizzo evidenziano come i carichi di lavoro su {{site.data.keyword.openshiftlong}} possano
avvalersi delle analisi relative a conoscenze di mercato, distribuzioni multiregione in tutto il mondo e gestione degli inventari con {{site.data.keyword.messagehub_full}} e l'archiviazione oggetti.
{: shortdesc}

## Il rivenditore tradizionale condivide i dati, utilizzando le API con i business partner globali per promuovere le vendite omnicanale
{: #uc_data-share}

Un responsabile della linea di business deve aumentare i canali di vendita, ma il sistema di vendita al dettaglio è isolato in un data center in loco. La competizione ha business partner globali per la vendita incrociata e incrementale di permutazioni delle loro merci, attraverso siti fisici e online. 
{: shortdesc}

Perché {{site.data.keyword.cloud_notm}}: Red Hat OpenShift on IBM Cloud fornisce un ecosistema di cloud pubblico, in cui i contenitori consentono a nuovi business partner e altri soggetti esterni di co-sviluppare applicazioni e dati, tramite le API. Ora che il sistema di vendita al dettaglio è sul cloud pubblico, le API semplificano anche la condivisione dei dati e lanciano il nuovo sviluppo di applicazioni. Le distribuzioni di applicazioni aumentano quando gli sviluppatori sperimentano facilmente, distribuendo rapidamente le modifiche ai sistemi di sviluppo e test con le toolchain.

Red Hat OpenShift on IBM Cloud e tecnologie chiave:
* [Cluster che si adattano a diverse esigenze di CPU, RAM e archiviazione](/docs/containers?topic=containers-planning_worker_nodes#planning_worker_nodes)
* [{{site.data.keyword.cos_full}} per mantenere e sincronizzare i dati tra le applicazioni](/docs/tutorials?topic=solution-tutorials-pub-sub-object-storage#pub-sub-object-storage)
* [Strumenti nativi DevOps, incluse le toolchain aperte in {{site.data.keyword.contdelivery_full}}](https://www.ibm.com/cloud/garage/toolchains/)

**Contesto: il rivenditore condivide i dati, utilizzando le API con i business partner globali per promuovere le vendite omnicanale**

* Il rivenditore si trova di fronte a forti pressioni competitive. In primo luogo, deve mascherare la complessità del passaggio a nuovi prodotti e nuovi canali. Ad esempio, deve espandere la sofisticazione del prodotto. Allo stesso tempo, i clienti devono riuscire a passare tra i vari marchi con facilità.
* Questa capacità di passaggio tra i marchi significa che l'ecosistema di vendita al dettaglio richiede la connettività ai business partner. Quindi, il cloud può portare nuovo valore da business partner, clienti e altri soggetti esterni.
* Gli eventi utente lampo, come il Black Friday, mettono a dura prova i sistemi online esistenti, costringendo il rivenditore a sovraccaricare l'infrastruttura di calcolo.
* Gli sviluppatori del rivenditore dovevano evolvere costantemente le applicazioni, ma gli strumenti tradizionali rallentavano la loro capacità di distribuire frequentemente aggiornamenti e funzioni, specialmente in caso di collaborazione con team di business partner.  

**Soluzione**

È necessaria un'esperienza di acquisto più intelligente per aumentare la fidelizzazione dei clienti e il margine di profitto lordo. Il modello di vendita tradizionale del rivenditore risentiva della mancanza di inventario dei business partner per le vendite incrociate e incrementali. I suoi acquirenti sono alla ricerca di maggiore praticità, in modo che possano trovare rapidamente articoli correlati, come pantaloni e tappetini da yoga.

Il rivenditore deve inoltre fornire ai clienti contenuti utili, come informazioni sui prodotti, informazioni sui prodotti alternativi, recensioni e visibilità dell'inventario in tempo reale. E i clienti vogliono tutto questo sia quando sono online che in negozio attraverso dispositivi mobili personali e dipendenti del negozio dotati di dispositivi mobili.

La soluzione è composta da questi componenti principali:
* INVENTARIO: applicazione per l'ecosistema di business partner che aggrega e comunica l'inventario, in particolare le introduzioni di nuovi prodotti, che include API per i business partner da riutilizzare nelle proprie applicazioni di vendita al dettaglio e B2B
* VENDITE INCROCIATE E INCREMENTALI: applicazione che rende visibili le opportunità di vendita incrociata e incrementale con le API che possono essere utilizzate in varie applicazioni di e-commerce e mobili
* AMBIENTE DI SVILUPPO: i cluster Kubernetes per i sistemi di sviluppo, test e produzione aumentano la collaborazione e la condivisione dei dati tra il rivenditore e i suoi business partner

Affinché il rivenditore lavori con business partner globali, le API di inventario hanno richiesto modifiche per adattarsi alle preferenze della lingua e del mercato di ciascuna regione. Red Hat OpenShift on IBM Cloud offre copertura in più regioni, tra cui Nord America, Europa, Asia e Australia, in modo che le API riflettano le esigenze di ogni paese e garantiscano una bassa latenza per le chiamate API.

Un altro requisito è che i dati di inventario siano condivisibili con i clienti e i business partner della società. Con le API di inventario, gli sviluppatori possono fornire informazioni nelle applicazioni, ad esempio applicazioni di inventario per dispositivi mobili o soluzioni di e-commerce web. Gli sviluppatori sono anche impegnati nella creazione e manutenzione del sito di e-commerce principale. In sintesi, devono concentrarsi sulla codifica anziché sulla gestione dell'infrastruttura.

Pertanto, hanno scelto Red Hat OpenShift on IBM Cloud perché IBM semplifica la gestione dell'infrastruttura:
* Gestione di master Kubernetes, IaaS e componenti operativi, come Ingress e archiviazione
* Monitoraggio dell'integrità e del recupero dei nodi di lavoro
* Fornitura del calcolo globale, in modo che gli sviluppatori dispongano dell'infrastruttura hardware nelle regioni in cui necessitano di carichi di lavoro e dati

Inoltre, la registrazione e il monitoraggio per i microservizi API, in particolare il modo in cui estraggono i dati personalizzati dai sistemi di back-end, si integrano facilmente con Red Hat OpenShift on IBM Cloud. Gli sviluppatori non sprecano tempo a creare sistemi di registrazione complessi, solo per essere in grado di risolvere i problemi dei sistemi attivi.

{{site.data.keyword.messagehub_full}} funge da piattaforma di eventi just-in-time per trasmettere le informazioni in rapida evoluzione dai sistemi di inventario dei business partner a {{site.data.keyword.cos_full}}.

**Modello di soluzione**

Gestione di eventi, archiviazione e calcolo su richiesta eseguiti nel cloud pubblico con accesso agli inventari di vendita al dettaglio in tutto il mondo, a seconda delle necessità

Soluzione tecnica:
* Red Hat OpenShift on IBM Cloud
* {{site.data.keyword.messagehub_full}}
* {{site.data.keyword.cos_full}}
* {{site.data.keyword.contdelivery_full}}
* IBM Cloud Logging and Monitoring
* {{site.data.keyword.appid_short_notm}}

**Passo 1: carica le applicazioni in un contenitore utilizzando i microservizi**
* Struttura le applicazioni in una serie di microservizi cooperativi eseguiti all'interno di Red Hat OpenShift on IBM Cloud in base alle aree funzionali dell'applicazione e delle sue dipendenze.
* Distribuisci le applicazioni nelle immagini del contenitore eseguite in Red Hat OpenShift on IBM Cloud.
* Fornisci dashboard DevOps standardizzati attraverso Kubernetes.
* Abilita il ridimensionamento su richiesta del calcolo per i carichi di lavoro batch e di altri inventari che vengono eseguiti raramente.

**Passo 2: garantisci la disponibilità globale**
* Gli strumenti HA integrati in Red Hat OpenShift on IBM Cloud bilanciano il carico di lavoro all'interno di ogni regione geografica, compresi la riparazione automatica e il bilanciamento del carico.
* Il bilanciamento del carico, i firewall e il DNS sono gestiti da IBM Cloud Internet Services.
* Utilizzando le toolchain e gli strumenti di distribuzione Helm, le applicazioni vengono anche distribuite ai cluster in tutto il mondo, quindi i carichi di lavoro e i dati soddisfano i requisiti regionali, in particolare la personalizzazione.

**Passo 3: comprendi gli utenti**
* {{site.data.keyword.appid_short_notm}} fornisce funzionalità di accesso senza che occorra modificare il codice applicativo.
* Dopo che gli utenti hanno eseguito l'accesso, puoi utilizzare {{site.data.keyword.appid_short_notm}} per creare dei profili e personalizzare l'esperienza di un utente della tua applicazione.

**Passo 4: condividi i dati**
* {{site.data.keyword.cos_full}} con {{site.data.keyword.messagehub_full}} fornisce l'archiviazione di dati cronologici e in tempo reale, in modo che le offerte di vendita incrociata rappresentino l'inventario disponibile dei business partner.
* Le API consentono ai business partner del rivenditore di condividere i dati nelle loro applicazioni di e-commerce e B2B.

**Passo 5: consegna in modo continuo**
* Il debug delle API co-sviluppate diventa più semplice quando si aggiungono agli strumenti di IBM Cloud Logging and Monitoring, quelli basati su cloud accessibili ai vari sviluppatori.
* {{site.data.keyword.contdelivery_full}} aiuta gli sviluppatori a fornire rapidamente una toolchain integrata utilizzando template personalizzabili e condivisibili con gli strumenti di IBM, terze parti e open source. Automatizza i processi di build e di test, controllando la qualità con l'analisi.
* Dopo che gli sviluppatori hanno creato e testato le applicazioni nei propri cluster di sviluppo e test, utilizzano le toolchain di integrazione e fornitura continua (CI e CD) per distribuire le applicazioni nei cluster in tutto il mondo.
* Red Hat OpenShift on IBM Cloud fornisce un facile roll-out e roll-back delle applicazioni; le applicazioni personalizzate vengono distribuite nelle campagne di test attraverso l'instradamento e il bilanciamento del carico intelligenti di Istio.

**Risultati**
* I microservizi riducono notevolmente i tempi di consegna di patch, correzioni di bug e nuove funzioni. Lo sviluppo iniziale in tutto il mondo è veloce e gli aggiornamenti sono frequenti 40 volte a settimana.
* Il rivenditore e i suoi business partner hanno accesso immediato alla disponibilità di inventario e alle pianificazioni di consegna, utilizzando le API.
* Con Red Hat OpenShift on IBM Cloud e gli strumenti CI e CD di IBM, le versioni A-B delle applicazioni sono pronte per le campagne di test.
* Red Hat OpenShift on IBM Cloud fornisce calcoli scalabili, in modo che i carichi di lavoro delle API di inventario e vendite incrociate possano aumentare durante i periodi di volume elevato dell'anno, come le festività autunnali.

## Il negoziante tradizionale aumenta le vendite e il traffico dei clienti con le informazioni digitali
{: #uc_grocer}

Un direttore marketing ha bisogno di aumentare il traffico dei clienti del 20% nei negozi, rendendo i negozi una risorsa di differenziazione. Numerosi concorrenti di vendita al dettaglio e rivenditori online stanno rubando le vendite. Allo stesso tempo, il direttore marketing deve ridurre l'inventario senza diminuzioni di prezzo, perché mantenere l'inventario troppo a lungo blocca milioni di capitale.
{: shortdesc}

Perché {{site.data.keyword.cloud_notm}}: Red Hat OpenShift on IBM Cloud fornisce una facile attivazione di più calcolo, in cui gli sviluppatori aggiungono rapidamente servizi Cloud Analytics per informazioni approfondite sui comportamenti di vendita e l'adattabilità del mercato digitale.

Tecnologie chiave:    
* [Adattamento orizzontale per accelerare lo sviluppo](/docs/containers?topic=containers-app#highly_available_apps)
* [Cluster che si adattano a diverse esigenze di CPU, RAM e archiviazione](/docs/containers?topic=containers-planning_worker_nodes#planning_worker_nodes)
* [Informazioni approfondite sulle tendenze del mercato con Watson Discovery](https://www.ibm.com/watson/services/discovery/)
* [Strumenti nativi DevOps, incluse le toolchain aperte in {{site.data.keyword.contdelivery_full}}](https://www.ibm.com/cloud/garage/toolchains/)
* [Gestione dell'inventario con {{site.data.keyword.messagehub_full}}](/docs/services/EventStreams?topic=eventstreams-about#about)

**Contesto: il negoziante tradizionale aumenta le vendite e il traffico dei clienti con le informazioni digitali**

* Le competitive pressioni dai rivenditori online e dalle grandi catene di negozi hanno ostacolato i tradizionali modelli di vendita al dettaglio di alimentari. Le vendite sono in calo, evidenziato dal basso traffico di gente nei negozi fisici.
* Il loro programma di fidelizzazione ha bisogno di una spinta con una versione moderna dei coupon stampati al momento del pagamento. Quindi gli sviluppatori devono evolvere costantemente le applicazioni correlate, ma gli strumenti tradizionali rallentano la loro capacità di distribuire frequentemente aggiornamenti e funzioni.  
* Alcuni inventari di alto valore non si muovono come previsto, ma il movimento "culinario" sembra crescere nei principali mercati metropolitani.

**Soluzione**

Il negoziante ha bisogno di un'applicazione per aumentare la conversione e il traffico in negozio per generare nuove vendite e fidelizzare i clienti in una piattaforma di analisi cloud riutilizzabile. L'esperienza mirata nel negozio può essere un evento insieme a un fornitore di servizi o prodotti che attrae sia i vecchi che i nuovi clienti in base all'affinità con l'evento specifico. Il negozio e il business partner offrono quindi incentivi per partecipare all'evento e acquistare prodotti dal negozio o dal business partner.  

Dopo l'evento, i clienti vengono seguiti nell'acquisto dei prodotti necessari, in modo che in futuro possano ripetere da soli l'attività dimostrata. L'esperienza mirata al cliente viene misurata con la riscossione degli incentivi e le nuove registrazioni del cliente fidelizzato. La combinazione di un evento di marketing iper-personalizzato e uno strumento per tracciare gli acquisti in negozio può portare l'esperienza mirata fino all'acquisto del prodotto. Tutte queste azioni danno luogo a traffico e conversioni maggiori.

Come evento di esempio, uno chef locale viene invitato nel negozio per mostrare come preparare un pasto gourmet. Il negozio offre un incentivo per partecipare. Ad esempio forniscono un antipasto gratuito presso il ristorante dello chef e un ulteriore incentivo per acquistare gli ingredienti per il pasto dimostrato (ad esempio, $20 di sconto sul carrello da $150).

La soluzione è composta da questi componenti principali:
1. ANALISI DI INVENTARIO: gli eventi in negozio (ricette, elenchi di ingredienti e posizioni dei prodotti) sono personalizzati per commercializzare l'inventario a lenta rotazione.
2. APPLICAZIONE MOBILE FEDELTÀ: fornisce marketing mirato con coupon digitali, liste della spesa, inventario dei prodotti (prezzi, disponibilità) su una mappa del negozio e condivisione sociale.
3. ANALISI SOCIAL MEDIA: fornisce la personalizzazione rilevando le preferenze dei clienti in termini di tendenze: cucine, chef e ingredienti. L'analisi collega le tendenze regionali con l'attività di Twitter, Pinterest e Instagram di un utente.
4. STRUMENTI PER LO SVILUPPATORE: accelerano il rollout di funzioni e correzioni di bug.

I sistemi di inventario di back-end per l'inventario dei prodotti, il rifornimento dei negozi e la previsione dei prodotti hanno una grande quantità di informazioni, ma le moderne analisi possono sbloccare nuove informazioni su come muovere meglio i prodotti di fascia alta. Utilizzando una combinazione di {{site.data.keyword.cloudant}} e IBM Streaming Analytics, il direttore marketing può trovare gli ingredienti ottimali da abbinare agli eventi in negozio personalizzati.

{{site.data.keyword.messagehub_full}} funge da piattaforma di eventi just-in-time per trasmettere le informazioni in rapida evoluzione dai sistemi di inventario a IBM Streaming Analytics.

L'analisi dei social media con Watson Discovery (informazioni su personalità e linguaggio) alimenta anche le tendenze nell'analisi dell'inventario per migliorare la previsione dei prodotti.

L'applicazione mobile di fedeltà fornisce informazioni dettagliate sulla personalizzazione, in particolare quando i clienti utilizzano le funzioni di condivisione sociale, come la pubblicazione di ricette.

Oltre all'applicazione mobile, gli sviluppatori sono impegnati a creare e mantenere l'applicazione di fedeltà esistente legata ai coupon di pagamento tradizionali. In sintesi, devono concentrarsi sulla codifica anziché sulla gestione dell'infrastruttura. Pertanto, hanno scelto Red Hat OpenShift on IBM Cloud perché IBM semplifica la gestione dell'infrastruttura:
* Gestione di master Kubernetes, IaaS e componenti operativi, come Ingress e archiviazione
* Monitoraggio dell'integrità e del recupero dei nodi di lavoro
* Fornitura del calcolo globale, in modo che gli sviluppatori non siano responsabili della configurazione dell'infrastruttura nei data center

**Modello di soluzione**

Gestione di eventi, archiviazione e calcolo su richiesta eseguiti nel cloud pubblico con accesso ai sistemi ERP di back-end

Soluzione tecnica:
* Red Hat OpenShift on IBM Cloud
* {{site.data.keyword.messagehub_full}}
* {{site.data.keyword.cloudant}}
* IBM Streaming Analytics
* IBM Watson Discovery

**Passo 1: carica le applicazioni in un contenitore utilizzando i microservizi**

* Struttura applicazioni mobili e analisi di inventario nei microservizi e distribuiscile nei contenitori in Red Hat OpenShift on IBM Cloud.
* Fornisci dashboard DevOps standardizzati attraverso Kubernetes.
* Ridimensiona il calcolo su richiesta per i carichi di lavoro batch e di altri inventari che vengono eseguiti con minore frequenza.

**Passo 2: analizza l'inventario e le tendenze**
* {{site.data.keyword.messagehub_full}} funge da piattaforma di eventi just-in-time per trasmettere le informazioni in rapida evoluzione dai sistemi di inventario a IBM Streaming Analytics.
* L'analisi dei social media con Watson Discovery e i dati dei sistemi di inventario è integrata con IBM Streaming Analytics per fornire suggerimenti di merchandising e marketing.

**Passo 3: consegna le promozioni con l'applicazione mobile di fedeltà**
* Inizia subito a sviluppare l'applicazione mobile con IBM Mobile Starter Kit e altri servizi IBM Mobile, come ad esempio {{site.data.keyword.appid_full_notm}}.
* Le promozioni sotto forma di coupon e altre concessioni vengono inviate all'applicazione mobile degli utenti. Le promozioni sono state identificate utilizzando l'analisi di inventario e dei social, oltre ad altri sistemi di back-end.
* L'archiviazione di ricette di promozione su applicazione mobile e conversioni (coupon di pagamento riscattati) viene inviata ai sistemi ERP per ulteriori analisi.

**Risultati**
* Con Red Hat OpenShift on IBM Cloud, i microservizi riducono notevolmente i tempi di consegna di patch, correzioni di bug e nuove funzioni. Lo sviluppo iniziale è veloce e gli aggiornamenti sono frequenti.
* Il traffico e le vendite dei clienti sono aumentati nei negozi rendendo gli stessi negozi una risorsa di differenziazione.
* Allo stesso tempo, le nuove informazioni dall'analisi sociale e cognitiva migliorata hanno ridotto le spese operative di inventario.
* La condivisione sociale nell'applicazione mobile aiuta anche a identificare e vendere ai nuovi clienti.


