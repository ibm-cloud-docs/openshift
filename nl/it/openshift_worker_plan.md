---

copyright:
  years: 2014, 2019
lastupdated: "2019-07-31"

keywords: openshift, roks, rhoks, rhos, multi az, multi-az, szr, mzr

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

# Pianificazione della configurazione dei tuoi nodi di lavoro
{: #planning_worker_nodes}

Il tuo cluster {{site.data.keyword.openshiftlong}} è costituito da nodi di lavoro raggruppati in pool di nodi di lavoro ed è monitorato e gestito centralmente dal master Kubernetes. Gli amministratori del cluster decidono come configurare il cluster di nodi di lavoro per garantire che gli utenti dispongano di tutte le risorse per distribuire ed eseguire applicazioni nel cluster.
{:shortdesc}

Quando crei un cluster standard, nell'infrastruttura IBM Cloud vengono ordinati per tuo conto i nodi di lavoro delle stesse specifiche di memoria, CPU e spazio su disco (profilo) e vengono aggiunti al pool di nodi di lavoro predefinito nel tuo cluster. A ogni nodo di lavoro viene
assegnato un ID e nome dominio univoco che non deve essere modificato dopo la creazione del cluster. Puoi scegliere tra server virtuali o fisici (bare metal). A seconda del livello di isolamento hardware che scegli, i nodi di lavoro virtuali possono essere configurati come nodi condivisi o dedicati. Per aggiungere dei profili differenti al tuo cluster, [crea un altro pool di nodi di lavoro](/docs/containers?topic=containers-cli-plugin-kubernetes-service-cli#cs_worker_pool_create).

Kubernetes limita il numero massimo di nodi di lavoro che puoi avere in un cluster. Controlla [nodo di lavoro e quote pod ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://kubernetes.io/docs/setup/cluster-large/) per ulteriori informazioni.


Vuoi essere sicuro di avere sempre abbastanza nodi di lavoro per gestire il tuo carico di lavoro? Prova [il cluster autoscaler](/docs/containers?topic=containers-ca#ca).
{: tip}

<br />


## Hardware disponibile per i nodi di lavoro
{: #shared_dedicated_node}

Quando crei un cluster standard in {{site.data.keyword.cloud_notm}}, puoi scegliere se i tuoi pool di nodi di lavoro sono costituiti da nodi di lavoro che sono macchine fisiche (bare metal) o macchine virtuali che vengono eseguite su hardware fisico. Puoi anche selezionare il profilo di nodo di lavoro oppure una combinazione di memoria, CPU e altre specifiche macchina quali l'archiviazione disco.
{:shortdesc}

<img src="images/cs_clusters_hardware.png" width="700" alt="Opzioni hardware per i nodi di lavoro in un cluster standard" style="width:700px; border-style: none"/>

Se vuoi più di un profilo di nodo di lavoro, devi creare un pool di nodi di lavoro per ciascun profilo. Non puoi ridimensionare i nodi di lavoro esistenti per avere risorse diverse come CPU o memoria. Quando crei un cluster gratuito, viene eseguito automaticamente il provisioning del tuo nodo di lavoro come un nodo virtuale condiviso nell'account dell'infrastruttura IBM Cloud. Nei cluster standard, puoi scegliere il tipo di macchina più adatto al tuo carico di lavoro. Mentre pianifichi, considera le [riserve di risorse del nodo di lavoro](#resource_limit_node) sulla capacità totale di CPU e memoria.

Seleziona una delle seguenti opzioni per decidere quale tipo di pool di nodi di lavoro vuoi.
* [Macchine virtuali](#vm)
* [Macchine fisiche (bare metal)](#bm)
* [Macchine SDS (software-defined storage)](#sds)



## Macchine virtuali
{: #vm}

Con le VM, ottieni maggiore flessibilità, tempi di provisioning più veloci e ulteriori funzioni di scalabilità automatica rispetto ai bare metal, ad un prezzo più conveniente. Puoi utilizzare le VM per casi di utilizzo più generali, quali gli ambienti di sviluppo e test, di preparazione e di produzione, i microservizi e le applicazioni di business. Tuttavia, è un compromesso nelle prestazioni. Se hai bisogno di una potenza di calcolo ad elevate prestazioni per i carichi di lavoro con un utilizzo intensivo di RAM, dati o GPU, utilizza il [bare metal](#bm).
{: shortdesc}

**È meglio se utilizzo hardware condiviso o dedicato?**</br>
Quando crei un cluster virtuale standard, devi scegliere se desideri che l'hardware sottostante sia condiviso tra più clienti {{site.data.keyword.IBM_notm}} (più tenant) o che sia dedicato solo a te (tenant singolo).

* **In una configurazione di hardware condiviso a più tenant**: le risorse fisiche, quali CPU e memoria, sono condivise tra tutte le macchine virtuali distribuite allo stesso hardware fisico. Per assicurare che ogni macchina virtuale
possa essere eseguita indipendentemente, un monitoraggio della macchina virtuale, conosciuto anche come hypervisor,
divide le risorse fisiche in entità isolate e le alloca come risorse dedicate
a una macchina virtuale (isolamento hypervisor).
* **In una configurazione hardware dedicato a singolo tenant**: tutte le risorse fisiche sono dedicate soltanto a te. Puoi distribuire
più nodi di lavoro come macchine virtuali allo stesso host fisico. In modo analogo alla configurazione a più tenant, l'hypervisor assicura che ogni nodo di lavoro ottenga la propria quota di risorse fisiche disponibili.

I nodi condivisi sono generalmente più economici dei nodi dedicati perché i costi dell'hardware sottostante
sono condivisi tra più clienti. Tuttavia, quando decidi tra nodi condivisi e dedicati,
potresti voler verificare con il tuo dipartimento legale e discutere sul livello di conformità e isolamento dell'infrastruttura
che il tuo ambiente dell'applicazione necessita.

Alcuni profili sono disponibili per un solo tipo di configurazione di tenancy. Ad esempio, le VM `m3c` sono disponibili solo come configurazione di tenancy `shared`.
{: note}

**Quali sono le funzioni generali delle VM?**</br>
Le macchine virtuali utilizzano il disco locale anziché SAN (Storage Area Networking) per garantire l'affidabilità. I vantaggi dell'affidabilità includono una velocità di elaborazione più elevata durante la serializzazione dei byte sul disco locale e una riduzione del danneggiamento del file system dovuto a errori di rete. Ogni VM offre una velocità di rete di 1000 Mbps, 25 GB di archiviazione disco locale primaria per il file system del sistema operativo e 100 GB di archiviazione disco locale secondaria per dati quali il runtime del contenitore e il `kubelet`. L'archiviazione locale sul nodo di lavoro è solo per l'elaborazione a breve termine e i dischi primari e secondari vengono cancellati quando aggiorni o ricarichi il nodo di lavoro. Per le soluzioni di archiviazione persistente, vedi [Pianificazione di archiviazione persistente altamente disponibile](/docs/containers?topic=containers-storage_planning#storage_planning).

**Cosa succede se ho dei profili meno recenti?**</br>
se il tuo cluster ha tipi di nodo di lavoro `x1c` o Ubuntu 16 `x2c` meno recenti od obsoleti, puoi [aggiornare il tuo cluster ai nodi di lavoro `x3c`
di Ubuntu 18 ](/docs/containers?topic=containers-update#machine_type).

**Quali tipi di macchina virtuale sono disponibili?**</br>
I tipi di nodo di lavoro variano in base alla zona. La seguente tabella include la versione più recente di un tipo, ad esempio i tipi di nodi di lavoro Ubuntu 18 `x3c`, invece dei tipi di nodi di lavoro Ubuntu 16 precedenti, `x2c`. Per vedere i profili disponibili nella tua zona, esegui `ibmcloud oc flavors --zone <zone>`. Puoi anche riesaminare i profili [bare metal](#bm) o [SDS](#sds) disponibili.



{: #vm-table}
<table>
<caption>Profili virtuali disponibili in {{site.data.keyword.containerlong_notm}}.</caption>
<thead>
<th>Nome e caso di utilizzo</th>
<th>Core / Memoria</th>
<th>Disco primario / secondario</th>
<th>Velocità di rete</th>
</thead>
<tbody>
<tr>
<td><strong>Virtuale, u3c.2x4</strong>: utilizza questa VM di dimensione minima per il test rapido, le prove di concetto e altri carichi di lavoro leggeri.<p class="note">Disponibile solo per i cluster Kubernetes. Non disponibile per i cluster OpenShift.</p></td>
<td>2/4 GB</td>
<td>25/100 GB</td>
<td>1000 Mbps</td>
</tr>
<tr>
<td><strong>Virtuale, b3c.4x16</strong>: seleziona questa VM bilanciata per il test e lo sviluppo e altri carichi di lavoro leggeri.</td>
<td>4/16 GB</td>
<td>25/100 GB</td>
<td>1000 Mbps</td>
</tr>
<tr>
<td><strong>Virtuale, b3c.16x64</strong>: seleziona questa VM bilanciata per carichi di lavoro di dimensione media.</td></td>
<td>16/64 GB</td>
<td>25/100 GB</td>
<td>1000 Mbps</td>
</tr>
<tr>
<td><strong>Virtuale, b3c.32x128</strong>: seleziona questa VM bilanciata per carichi di lavoro medio-grandi, come un database e un sito Web dinamico con molti utenti simultanei.</td>
<td>32/128 GB</td>
<td>25/100 GB</td>
<td>1000 Mbps</td>
</tr>
<tr>
<td><strong>Virtuale, c3c.16x16</strong>: utilizza questo tipo quando vuoi un bilanciamento equilibrato delle risorse di elaborazione provenienti dal nodo di lavoro per carichi di lavoro leggeri.</td>
<td>16/16 GB</td>
<td>25/100 GB</td>
<td>1000 Mbps</td>
</tr><tr>
<td><strong>Virtuale, c3c.16x32</strong>: utilizza questo tipo quando vuoi un rapporto 1:2 tra le risorse di CPU e memoria del nodo di lavoro per carichi di lavoro leggeri o di medie dimensioni.</td>
<td>16/32 GB</td>
<td>25/100 GB</td>
<td>1000 Mbps</td>
</tr><tr>
<td><strong>Virtuale, c3c.32x32</strong>: utilizza questo tipo quando vuoi un bilanciamento equilibrato delle risorse di elaborazione provenienti dal nodo di lavoro per carichi di lavoro di medie dimensioni.</td>
<td>32/32 GB</td>
<td>25/100 GB</td>
<td>1000 Mbps</td>
</tr><tr>
<td><strong>Virtuale, c3c.32x64</strong>: utilizza questo tipo quando vuoi un rapporto 1:2 tra le risorse di CPU e memoria del nodo di lavoro per carichi di lavoro di medie dimensioni.</td>
<td>32/64 GB</td>
<td>25/100 GB</td>
<td>1000 Mbps</td>
</tr>
<tr>
<td><strong>Virtuale, m3c.8x64</strong>: utilizza questo tipo quando vuoi un rapporto 1:8 tra le risorse di CPU e memoria per carichi di lavoro leggeri o di medie dimensioni che richiedono più memoria, così come accade con i database {{site.data.keyword.Db2_on_Cloud_short}}. Disponibile solo a Dallas e come tenancy `--hardware shared`.</td>
<td>8/64 GB</td>
<td>25/100 GB</td>
<td>1000 Mbps</td>
</tr><tr>
<td><strong>Virtuale, m3c.16x128</strong>: utilizza questo tipo quando vuoi un rapporto 1:8 tra le risorse di CPU e memoria per carichi di lavoro di medie dimensioni che richiedono più memoria, così come accade con i database {{site.data.keyword.Db2_on_Cloud_short}}. Disponibile solo a Dallas e come tenancy `--hardware shared`.</td>
<td>16/128 GB</td>
<td>25/100 GB</td>
<td>1000 Mbps</td>
</tr><tr>
<td><strong>Virtuale, m3c.30x240</strong>: utilizza questo tipo quando vuoi un rapporto 1:8 tra le risorse di CPU e memoria per carichi di lavoro di dimensioni da medie a elevate che richiedono più memoria, così come accade con i database {{site.data.keyword.Db2_on_Cloud_short}}. Disponibile solo a Dallas e come tenancy `--hardware shared`.</td>
<td>30/240 GB</td>
<td>25/100 GB</td>
<td>1000 Mbps</td>
</tr>
<tr>
<td><strong>Virtuale, z1.2x4</strong>: utilizza questo tipo quando vuoi che venga creato un nodo di lavoro nei contenitori Hyper Protect sui sistemi IBM Z.</td>
<td>2/4 GB</td>
<td>25/100 GB</td>
<td>1000 Mbps</td>
</tr>
</tbody>
</table>

## Macchine fisiche (bare metal)
{: #bm}

Puoi eseguire il provisioning del tuo nodo di lavoro come server fisico a singolo tenant, indicato anche come bare metal.
{: shortdesc}

**In che modo il bare metal di differenzia dalle VM?**</br>
Bare metal ti dà accesso diretto alle risorse fisiche sulla macchina, come la memoria o la CPU. Questa configurazione elimina l'hypervisor della macchina virtuale che assegna risorse fisiche alle macchine virtuali eseguite sull'host. Invece, tutte le risorse di una macchina bare metal sono dedicate esclusivamente al nodo di lavoro, quindi non devi preoccuparti degli "elementi di disturbo" che condividono risorse o rallentano le prestazioni. I profili fisici hanno più archiviazione locale rispetto a quelli virtuali e alcuni dispongono di RAID per aumentare la disponibilità dei dati. L'archiviazione locale sul nodo di lavoro è solo per l'elaborazione a breve termine e i dischi primari e secondari vengono cancellati quando aggiorni o ricarichi il nodo di lavoro. Per le soluzioni di archiviazione persistente, vedi [Pianificazione di archiviazione persistente altamente disponibile](/docs/containers?topic=containers-storage_planning#storage_planning).

**Oltre ad avere specifiche migliori per le prestazioni, posso fare qualcosa con bare metal che non posso fare con le macchine virtuali?**</br>
Sì, con i nodi di lavoro bare metal puoi utilizzare {{site.data.keyword.datashield_full}}. {{site.data.keyword.datashield_short}} è integrato con la tecnologia di Intel® Software Guard Extensions (SGX) e Fortanix® in modo che il codice e i dati dei carichi di lavoro del tuo contenitore {{site.data.keyword.Bluemix_notm}} siano protetti durante l'utilizzo. I dati e il codice applicativo vengono eseguiti in enclavi con protezione avanzata della CPU. Le enclavi con protezione avanzata della CPU sono aree attendibili della memoria sul nodo di lavoro che proteggono aspetti critici dell'applicazione, aiutando a mantenere il codice e i dati riservati e invariati. Se tu o la tua azienda richiedete la sensibilità dei dati a causa di politiche interne, regolamentazioni governative o requisiti di conformità del settore, questa soluzione potrebbe aiutarvi a passare al cloud. Casi di utilizzo di esempio includono istituzioni finanziarie e sanitarie o paesi con politiche governative che richiedono soluzioni cloud in loco.

**Bare metal sembra essere un'opzione estremamente valida. Cosa mi impedisce di ordinarne uno immediatamente?**</br>
I server bare metal sono più costosi di quelli virtuali e sono più adatti per le applicazioni ad alte prestazioni che richiedono più risorse e controllo host.

I server bare metal vengono fatturati mensilmente. Se annulli un server bare metal prima della fine del mese, ti viene addebitato il costo fino alla fine di quel mese. Dopo aver ordinato o annullato un server bare metal, il processo viene completato manualmente nel tuo account dell'infrastruttura IBM Cloud. Pertanto, ci vuole più di un giorno lavorativo per completare questo processo.
{: important}

**Quali tipi di bare metal posso ordinare?**</br>
I tipi di nodo di lavoro variano in base alla zona. La seguente tabella include la versione più recente di un tipo, ad esempio i tipi di nodi di lavoro Ubuntu 18 `x3c`, invece dei tipi di nodi di lavoro Ubuntu 16 precedenti, `x2c`. Per vedere i profili disponibili nella tua zona, esegui `ibmcloud oc flavors --zone <zone>`. Puoi anche riesaminare i profili [VM](#vm) o [SDS](#sds) disponibili.

Le macchine bare metal sono ottimizzate per diversi casi d'uso quali i carichi di lavoro con un utilizzo intensivo di RAM, dati o GPU.

Scegli un profilo con la configurazione di archiviazione corretta per supportare il tuo carico di lavoro. Alcuni profili hanno una combinazione delle seguenti configurazioni di dischi e archiviazione. Ad esempio, alcuni profili possono avere un disco primario SATA con un disco secondario SSD raw.

* **SATA**: un dispositivo di archiviazione disco a rotazione magnetica che viene spesso utilizzato per il disco primario del nodo di lavoro che memorizza il file system del sistema operativo.
* **SSD**: un dispositivo di archiviazione SSD (solid-state drive) per i dati ad alte prestazioni.
* **Raw**: il dispositivo di archiviazione non è formattato e tutta la capacità è disponibile per l'utilizzo.
* **RAID**: un dispositivo di archiviazione con i dati distribuiti per la ridondanza e prestazioni che variano a seconda del livello RAID. Di conseguenza, la capacità del disco disponibile per l'utilizzo varia.

{: #bm-table}
<table>
<caption>Profili bare metal disponibili in {{site.data.keyword.containerlong_notm}}.</caption>
<thead>
<th>Nome e caso di utilizzo</th>
<th>Core / Memoria</th>
<th>Disco primario / secondario</th>
<th>Velocità di rete</th>
</thead>
<tbody>
<tr>
<td><strong>Bare metal con RAM intensiva, mr3c.28x512</strong>: massimizza la disponibilità della RAM dei tuoi nodi di lavoro.</td>
<td>28/512 GB</td>
<td>SATA da 2 TB/SSD da 960 GB</td>
<td>10000 Mbps</td>
</tr>
<tr>
<td><strong>Bare metal GPU, mg3c.16x128</strong>: scegli questo tipo per i carichi di lavoro matematicamente complessi, quale il calcolo ad alte prestazioni, il machine learning o le applicazioni 3D. Questo tipo ha una scheda fisica Tesla K80 con due GPU (graphics processing unit) per scheda per un totale di due GPU.</td>
<td>16/128 GB</td>
<td>SATA da 2 TB/SSD da 960 GB</td>
<td>10000 Mbps</td>
</tr>
<tr>
<td><strong>Bare metal GPU, mg3c.28x256</strong>: scegli questo tipo per i carichi di lavoro matematicamente complessi, quale il calcolo ad alte prestazioni, il machine learning o le applicazioni 3D. Questo tipo ha due schede fisiche Tesla K80 con due GPU per scheda per un totale di quattro GPU.</td>
<td>28/256 GB</td>
<td>SATA da 2 TB/SSD da 960 GB</td>
<td>10000 Mbps</td>
</tr>
<tr>
<td><strong>Bare metal con uso intensivo di dati, md3c.16x64.4x4tb</strong>: utilizza questo tipo per una quantità significativa di archiviazione su disco locale, incluso RAID, per aumentare la disponibilità dei dati, per carichi di lavoro quali file system distribuiti, database di grandi dimensioni e analisi dei big data.</td>
<td>16/64 GB</td>
<td>RAID1 da 2x2 TB/RAID10 SATA da 4x4 TB</td>
<td>10000 Mbps</td>
</tr>
<tr>
<td><strong>Bare metal con uso intensivo di dati, md3c.28x512.4x4tb</strong>: utilizza questo tipo per una quantità significativa di archiviazione su disco locale, incluso RAID, per aumentare la disponibilità dei dati, per carichi di lavoro quali file system distribuiti, database di grandi dimensioni e analisi dei big data.</td>
<td>28/512 GB</td>
<td>RAID1 da 2x2 TB/RAID10 SATA da 4x4 TB</td>
<td>10000 Mbps</td>
</tr>
<tr>
<td><strong>Bare metal bilanciato, mb3c.4x32</strong>: utilizzalo per i carichi di lavoro bilanciati che richiedono risorse di calcolo superiori a quelle offerte dalle macchine virtuali. Questo profilo può anche essere abilitato per Intel® Software Guard Extensions (SGX) in modo che tu possa utilizzare <a href="/docs/services/data-shield?topic=data-shield-getting-started#getting-started" target="_blank">{{site.data.keyword.datashield_short}} <img src="../icons/launch-glyph.svg" alt="Icona link esterno"></a> per crittografare la tua memoria di dati.</td>
<td>4/32 GB</td>
<td>SATA da 2 TB/SATA da 2 TB</td>
<td>10000 Mbps</td>
</tr>
<tr>
<td><strong>Bare metal bilanciato, mb3c.16x64</strong>: utilizzalo per i carichi di lavoro bilanciati che richiedono risorse di calcolo superiori a quelle offerte dalle macchine virtuali.</td>
<td>16/64 GB</td>
<td>SATA da 2 TB/SSD da 960 GB</td>
<td>10000 Mbps</td>
</tr>
<tr>
</tbody>
</table>

## Macchine SDS (software-defined storage)
{: #sds}

I profili SDS (software-defined storage) sono macchine fisiche fornite con dischi non formattati aggiuntivi per l'archiviazione locale fisica. A differenza del disco locale primario e secondario, questi dischi non formattati non vengono cancellati durante l'aggiornamento o il ricaricamento del nodo di lavoro. Poiché i dati hanno la stessa ubicazione del nodo di calcolo, le macchine SDS sono adatte per i carichi di lavoro ad alte prestazioni.
{: shortdesc}

**Quando utilizzo i tipi SDS?**</br>
Di norma utilizzi le macchine SDS nei seguenti casi:
*  Se utilizzi un componente aggiuntivo SDS come [Portworx](/docs/containers?topic=containers-portworx#portworx) nel cluster, usa una macchina SDS.
*  Se la tua applicazione è uno [StatefulSet ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://kubernetes.io/docs/concepts/workloads/controllers/statefulset/) che richiede l'archiviazione locale, puoi utilizzare le macchine SDS ed eseguire il provisioning di [volumi persistenti locali Kubernetes (beta)![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://kubernetes.io/blog/2018/04/13/local-persistent-volumes-beta/).
*  Se hai applicazioni personalizzate che richiedono ulteriore archiviazione locale non elaborata.

Per ulteriori soluzioni di archiviazione, vedi [Pianificazione di archiviazione persistente altamente disponibile](/docs/containers?topic=containers-storage_planning#storage_planning).

**Quali tipi di SDS posso ordinare?**</br>
I tipi di nodo di lavoro variano in base alla zona. La seguente tabella include la versione più recente di un tipo, ad esempio i tipi di nodi di lavoro Ubuntu 18 `x3c`, invece dei tipi di nodi di lavoro Ubuntu 16 precedenti, `x2c`. Per vedere i profili disponibili nella tua zona, esegui `ibmcloud oc flavors --zone <zone>`. Puoi anche riesaminare i profili [bare metal](#bm) o [VM](#vm) disponibili.

Scegli un profilo con la configurazione di archiviazione corretta per supportare il tuo carico di lavoro. Alcuni profili hanno una combinazione delle seguenti configurazioni di dischi e archiviazione. Ad esempio, alcuni profili possono avere un disco primario SATA con un disco secondario SSD raw.

* **SATA**: un dispositivo di archiviazione disco a rotazione magnetica che viene spesso utilizzato per il disco primario del nodo di lavoro che memorizza il file system del sistema operativo.
* **SSD**: un dispositivo di archiviazione SSD (solid-state drive) per i dati ad alte prestazioni.
* **Raw**: il dispositivo di archiviazione non è formattato e tutta la capacità è disponibile per l'utilizzo.
* **RAID**: un dispositivo di archiviazione con i dati distribuiti per la ridondanza e prestazioni che variano a seconda del livello RAID. Di conseguenza, la capacità del disco disponibile per l'utilizzo varia.

{: #sds-table}
<table>
<caption>Profili SDS disponibili in {{site.data.keyword.containerlong_notm}}.</caption>
<thead>
<th>Nome e caso di utilizzo</th>
<th>Core / Memoria</th>
<th>Disco primario / secondario</th>
<th>Dischi non formattati aggiuntivi</th>
<th>Velocità di rete</th>
</thead>
<tbody>
<tr>
<td><strong>Bare metal con SDS, ms3c.4x32.1.9tb.ssd</strong>: se hai bisogno di archiviazione locale supplementare per motivi di prestazioni, utilizza questo tipo dotato di notevole capacità di disco che supporta l'SDS (software-defined storage).</td>
<td>4/32 GB</td>
<td>SATA da 2 TB/SSD da 960 GB</td>
<td>TB raw da 1,9 TB (percorso dispositivo: `/dev/sdc`)</td>
<td>10000 Mbps</td>
</tr>
<tr>
<td><strong>Bare metal con SDS, ms3c.16x64.1.9tb.ssd</strong>: se hai bisogno di archiviazione locale supplementare per motivi di prestazioni, utilizza questo tipo dotato di notevole capacità di disco che supporta l'SDS (software-defined storage).</td>
<td>16/64 GB</td>
<td>SATA da 2 TB/SSD da 960 GB</td>
<td>TB raw da 1,9 TB (percorso dispositivo: `/dev/sdc`)</td>
<td>10000 Mbps</td>
</tr>
<tr>
<td><strong>Bare metal con SDS, ms3c.28x256.3.8tb.ssd</strong>: se hai bisogno di archiviazione locale supplementare per motivi di prestazioni, utilizza questo tipo dotato di notevole capacità di disco che supporta l'SDS (software-defined storage).</td>
<td>28/256 GB</td>
<td>SATA da 2 TB/SSD da 1,9 TB</td>
<td>TB raw da 3,8 TB (percorso dispositivo: `/dev/sdc`)</td>
<td>10000 Mbps</td>
</tr>
<tr>
<td><strong>Bare metal con SDS, ms3c.28x512.4x3.8tb.ssd</strong>: se hai bisogno di archiviazione locale supplementare per motivi di prestazioni, utilizza questo tipo dotato di notevole capacità di disco che supporta l'SDS (software-defined storage).</td>
<td>28/512 GB</td>
<td>SATA da 2 TB/SSD da 1,9 TB</td>
<td>4 dischi, SSD raw da 3,8 TB (percorsi dispositivo: `/dev/sdc`, `/dev/sdd`, `/dev/sde`, `/dev/sdf`)</td>
<td>10000 Mbps</td>
</tr>
</tbody>
</table>

## Riserve di risorse del nodo di lavoro
{: #resource_limit_node}

{{site.data.keyword.containerlong_notm}} imposta riserve di risorse di calcolo che limitano le risorse di calcolo disponibili su ciascun nodo di lavoro. Le risorse di memoria e CPU riservate non possono essere utilizzate dai pod sul nodo di lavoro e riducono le risorse assegnabili su ciascun nodo di lavoro. Quando distribuisci inizialmente i pod, se il nodo di lavoro non dispone di sufficienti risorse assegnabili, la distribuzione non riesce. Inoltre, se i pod superano il limite di risorse del nodo di lavoro, i pod vengono rimossi. In Kubernetes, questo limite è chiamato [soglia di rimozione rigida![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://kubernetes.io/docs/tasks/administer-cluster/out-of-resource/#hard-eviction-thresholds).
{:shortdesc}

Se sono disponibili meno CPU o memoria rispetto alle riserve del nodo di lavoro, Kubernetes inizia a rimuovere i pod per ripristinare risorse di calcolo sufficienti. I pod vengono ripianificati su un altro nodo di lavoro, laddove disponibile. Se i tuoi pod vengono rimossi frequentemente, aggiungi più nodi di lavoro al tuo cluster o imposta i [limiti di risorsa ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://kubernetes.io/docs/concepts/configuration/manage-compute-resources-container/#resource-requests-and-limits-of-pod-and-container) sui tuoi pod.

Le risorse che sono riservate sul tuo nodo di lavoro dipendono dalla quantità di CPU e memoria con cui viene fornito il tuo nodo di lavoro. {{site.data.keyword.containerlong_notm}} definisce i livelli di memoria e CPU come mostrato nelle seguenti tabelle. Se il tuo nodo di lavoro viene fornito con risorse di calcolo su più livelli, una percentuale delle tue risorse di CPU e memoria è riservata per ogni livello.

Per riesaminare quante risorse di calcolo sono attualmente utilizzate sul tuo nodo di lavoro, esegui [`oc top node` ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://kubernetes.io/docs/reference/kubectl/overview/#top).
{: tip}

| Livello di memoria | % o quantità riservata | Esempio di nodo di lavoro <code>b3c.4x16</code> (16 GB) | Esempio di nodo di lavoro <code>mg1c.28x256</code> (256 core)|
|:-----------------|:-----------------|:-----------------|:-----------------|
| Primi 4 GB (0 - 4 GB) | 25% di memoria | 1 GB | 1 GB|
| Prossimi 4 GB (5 - 8 GB) | 20% di memoria | 0,8 GB | 0,8 GB|
| Prossimi 8 GB (9 - 16 GB) | 10% di memoria | 0,8 GB | 0,8 GB|
| Prossimi 112 GB (17 - 128 GB) | 6% di memoria | N/D | 6,72 GB|
| GB restanti (129 GB e oltre) | 2% di memoria | N/D | 2,54 GB|
| Riserva aggiuntiva per [`kubelet` eviction ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://kubernetes.io/docs/tasks/administer-cluster/out-of-resource/) | 100 MB | 100 MB (quantità fissa) | 100 MB (quantità fissa)|
| **Totale riservato** | **(varia)** | **2,7 GB di 16 GB totali** | **11,96 GB di 256 GB totali**|
{: class="simple-tab-table"}
{: caption="Riserve di memoria del nodo di lavoro per livello" caption-side="top"}
{: #worker-memory-reserves}
{: tab-title="Worker node memory reserves by tier"}
{: tab-group="Worker Node"}

| Livello di CPU | % o quantità riservata | Esempio di nodo di lavoro <code>b3c.4x16</code> (quattro core) | Esempio di nodo di lavoro <code>mg1c.28x256</code> (28 core)|
|:-----------------|:-----------------|:-----------------|:-----------------|
| Primo core (Core 1) | 6% di core | 0,06 core | 0,06 core|
| Prossimi due core (core 2 - 3) | 1% di core | 0,02 core | 0,02 core|
| Prossimi due core (core 4 - 5) | 0.5% di core | 0,005 core | 0,01 core|
| Core rimanenti (Core 6+) | 0,25% di core | N/D | 0,0575 core|
| **Totale riservato** | **(varia)** | **0,085 core di un totale di quattro core** | **0,1475 core di 28 core totali**|
{: class="simple-tab-table"}
{: caption="Riserve di CPU del nodo di lavoro per livello" caption-side="top"}
{: #worker-cpu-reserves}
{: tab-title="Worker node CPU reserves by tier"}
{: tab-group="Worker Node"}



