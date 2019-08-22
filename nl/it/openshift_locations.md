---

copyright:
  years: 2014, 2019
lastupdated: "2019-07-31"

keywords: openshift, roks, rhoks, rhos, mzr, szr, multizone, multi az

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


# Ubicazioni
{: #regions-and-zones}

Puoi distribuire i cluster {{site.data.keyword.openshiftlong}} in tutto il mondo. Quando crei un cluster, le sue risorse rimangono nell'ubicazione a cui distribuisci il cluster. Per lavorare con il tuo cluster, puoi accedere al servizio OpenShift tramite un endpoint API globale.
{:shortdesc}

![Ubicazioni di Red Hat OpenShift on IBM Cloud](images/locations-roks.png)

_Ubicazioni di Red Hat OpenShift on IBM Cloud_


## Ubicazioni di Red Hat OpenShift on IBM Cloud
{: #locations}

Le risorse {{site.data.keyword.cloud_notm}} sono organizzate in una gerarchia di ubicazioni geografiche. Red Hat OpenShift on IBM Cloud è disponibile in un sottoinsieme di queste ubicazioni, incluse tutte e sei le regioni con capacità multizona in tutto il mondo. Gli altri servizi {{site.data.keyword.cloud_notm}} potrebbero essere disponibili a livello globale o all'interno di un'ubicazione specifica.
{: shortdesc}

### Ubicazioni disponibili
{: #available-locations}

Per elencare le ubicazioni di Red Hat OpenShift on IBM Cloud disponibili, utilizza il comando `ibmcloud oc supported-locations`.
{: shortdesc}

La seguente immagine viene utilizzata come un esempio per spiegare il modo in cui sono organizzate le ubicazioni di Red Hat OpenShift on IBM Cloud.

![Organizzazione delle ubicazioni di Red Hat OpenShift on IBM Cloud](images/cs_regions_hierarchy.png)

<table summary="La tabella mostra l'organizzazione delle ubicazioni di Red Hat OpenShift on IBM Cloud. Le righe vanno lette da sinistra a destra, con il tipo di ubicazione nella colonna uno, un esempio del tipo nella colonna due e la descrizione nella colonna tre.">
<caption>Organizzazione delle ubicazioni di Red Hat OpenShift on IBM Cloud.</caption>
  <thead>
  <th>Tipo</th>
  <th>Esempio</th>
  <th>Descrizione</th>
  </thead>
  <tbody>
    <tr>
      <td>Area geografica</td>
      <td>Nord America (`na`)</td>
      <td>Un raggruppamento organizzativo basato sui continenti geografici.</td>
    </tr>
    <tr>
      <td>Paese</td>
      <td>Canada (`ca`)</td>
      <td>Il paese dell'ubicazione all'interno dell'area geografica.</td>
    </tr>
    <tr>
      <td>Area metropolitana</td>
      <td>Città del Messico (`mex-cty`), Dallas (`dal`)</td>
      <td>Il nome di una città in cui sono ubicati 1 o più data center (zone). Un'area metropolitana può essere una zona che supporta il multizona e avere data center che supportano il multizona, come Dallas, o può avere solo data center a zona singola, come Città del Messico. Se crei un cluster in un'area metropolitana che supporta il multizona, il master Kubernetes e i nodi di lavoro possono essere distribuiti tra le zone per garantire l'alta disponibilità.</td>
    </tr>
    <tr>
      <td>Data center (zona)</td>
      <td>Dallas 12 (`dal12`)</td>
      <td>Un'ubicazione fisica dell'infrastruttura di calcolo, di rete e di archiviazione e dei relativi sistemi di raffreddamento e alimentazione che ospitano servizi e applicazioni cloud. I cluster possono essere distribuiti tra i data center, o zone, in un'architettura multizona per l'alta disponibilità. Le zone sono isolate l'una dall'altra, il che garantisce che non ci sia alcun singolo punto di malfunzionamento condiviso.</td>
    </tr>
  </tbody>
  </table>

### Ubicazioni multizona in Red Hat OpenShift on IBM Cloud
{: #zones}

Le seguenti tabelle elencano le ubicazioni multizona disponibili in Red Hat OpenShift on IBM Cloud. Puoi scegliere di creare dei cluster con i nodi di lavoro in una zona dell'area metropolitana multizona o di diffondere i nodi di lavoro in tutte e tre le zone all'interno di ciascuna area metropolitana per proteggere le tue applicazioni da un malfunzionamento della zona. Sia che tu crei i nodi di lavoro in una singola zona o in diverse zone, le repliche del tuo master altamente disponibile vengono automaticamente distribuite tra le zone.
{: shortdesc}

Per determinare rapidamente se una zona ha una capacità multizona, puoi eseguire `ibmcloud oc supported-locations` e cercare il valore nella colonna `Multizone Metro`.
{: tip}

**Ubicazioni metropolitane multizona**

<table summary="La tabella mostra le ubicazioni di area metropolitana multizona disponibili in Red Hat OpenShift on IBM Cloud. Le righe vanno lette da sinistra a destra.  La colonna uno è l'area geografica in cui si trova l'ubicazione, la colonna due è il paese dell'ubicazione, la colonna tre è l'area metropolitana dell'ubicazione, la colonna quattro è il data center e la colonna cinque è la regione ora dichiarata obsoleta in cui un tempo era organizzata l'ubicazione.">
<caption>Ubicazioni di area metropolitana multizona disponibili in Red Hat OpenShift on IBM Cloud.</caption>
  <thead>
  <th>Area geografica</th>
  <th>Paese</th>
  <th>Area metropolitana</th>
  <th>Data center</th>
  <th>Regione obsoleta</th>
  </thead>
  <tbody>
    <tr>
      <td>Asia Pacifico</td>
      <td>Australia</td>
      <td>Sydney</td>
      <td>syd01, syd04, syd05</td>
      <td>Asia Pacifico Sud (`ap-south`, `au-syd`)</td>
    </tr>
    <tr>
      <td>Asia Pacifico</td>
      <td>Giappone</td>
      <td>Tokyo</td>
      <td>tok02, tok04, tok05</td>
      <td>Asia Pacifico Nord (`ap-north`, `jp-tok`)</td>
    </tr>
    <tr>
      <td>Europa</td>
      <td>Germania</td>
      <td>Francoforte</td>
      <td>fra02, fra04, fra05</td>
      <td>Europa Centrale (`eu-central`, `eu-de`)</td>
    </tr>
    <tr>
      <td>Europa</td>
      <td>Regno Unito</td>
      <td>Londra</td>
      <td>lon04, lon05, lon06</td>
      <td>Regno Unito Sud (`uk-south`, `eu-gb`)</td>
    </tr>
    <tr>
      <td>Nord America</td>
      <td>Stati Uniti</td>
      <td>Dallas</td>
      <td>dal10, dal12, dal13</td>
      <td>Stati Uniti Sud (`us-south`)</td>
    </tr>
    <tr>
      <td>Nord America</td>
      <td>Stati Uniti</td>
      <td>Washington, D.C.</td>
      <td>wdc04, wdc06, wdc07</td>
      <td>Stati Uniti Est (`us-east`)</td>
    </tr>
  </tbody>
  </table>

### Cluster multizona
{: #regions_multizone}

In un cluster multizona, le risorse del tuo cluster vengono distribuite tra più zone per una maggiore disponibilità.
{: shortdesc}

1.  I nodi di lavoro vengono distribuiti tra più zone nell'ubicazione metropolitana per fornire una maggiore disponibilità per il tuo cluster. Anche le repliche del master Kubernetes vengono distribuite tra le zone. Quando avvii azioni di orchestrazione del contenitore locale, come i comandi `oc`, le informazioni vengono scambiate tra i tuoi nodi di lavoro e master tramite l'endpoint globale.

2.  La modalità di distribuzione nelle zone nel tuo cluster multizona di altre risorse del cluster, quali l'archiviazione, la rete, il calcolo o le applicazioni in esecuzione nei pod, varia. Per ulteriori informazioni, consulta questi argomenti:
    *   Configurazione di [archiviazione file](/docs/openshift?topic=openshift-file_storage#add_file) e [archiviazione blocchi](/docs/openshift?topic=openshift-block_storage#add_block) nei cluster multizona o [scelta di una soluzione di archiviazione persistente multizona](/docs/openshift?topic=openshift-storage_planning#persistent_storage_overview).
    *   [Abilitazione dell'accesso pubblico o privato a un'applicazione utilizzando un servizio NLB (network load balancer) in un cluster multizona](/docs/containers?topic=containers-loadbalancer#multi_zone_config).
    *   [Gestione del traffico di rete utilizzando Ingress](/docs/containers?topic=containers-ingress-about).
    *   [Aumento della disponibilità della tua applicazione](/docs/containers?topic=containers-app#increase_availability).

3.  Quando avvii azioni di gestione del cluster, utilizzando ad esempio i [comandi `ibmcloud oc`](/docs/openshift?topic=openshift-kubernetes-service-cli), le informazioni di base sul cluster (come nome, ID, utente, comando) vengono instradate attraverso l'endpoint globale.

<br />


## Accesso all'endpoint globale
{: #endpoint}

Puoi organizzare le tue risorse tra i servizi {{site.data.keyword.cloud_notm}} utilizzando le ubicazioni {{site.data.keyword.cloud_notm}} (precedentemente chiamate regioni). Ad esempio, puoi creare un cluster Kubernetes utilizzando un'immagine Docker privata memorizzata nel tuo {{site.data.keyword.registryshort_notm}} della stessa ubicazione. Per accedere a queste risorse, puoi utilizzare gli endpoint globali e filtrare per ubicazione.
{:shortdesc}

### Accesso a {{site.data.keyword.cloud_notm}}
{: #login-ic}

Quando accedi alla riga di comando {{site.data.keyword.cloud_notm}} (`ibmcloud`), ti viene richiesto di selezionare una regione. Tuttavia, questa regione non influenza l'endpoint di plugin Red Hat OpenShift on IBM Cloud (`ibmcloud oc`), che utilizza ancora l'endpoint globale. Tieni presente che devi ancora specificare il gruppo di risorse in cui si trova il tuo cluster se non si trova nel gruppo di risorse predefinito.
{: shortdesc}

Per eseguire l'accesso all'endpoint API globale {{site.data.keyword.cloud_notm}} e specificare il gruppo di risorse in cui si trova il tuo cluster:
```
ibmcloud login -a https://cloud.ibm.com -g <nondefault_resource_group_name>
```
{: pre}

### Accesso a Red Hat OpenShift on IBM Cloud
{: #login-iks}

Quando esegui l'accesso a {{site.data.keyword.cloud_notm}}, puoi accedere a {{site.data.keyword.containershort_notm}}. Per aiutarti a iniziare, controlla le seguenti risorse per l'utilizzo della CLI e dell'API Red Hat OpenShift on IBM Cloud.
{: shortdesc}

**CLI di Red Hat OpenShift on IBM Cloud**:

[Configura la tua CLI per utilizzare il plugin `ibmcloud oc`](/docs/openshift?topic=openshift-openshift-cli). Per impostazione predefinita, sei collegato all'endpoint Red Hat OpenShift on IBM Cloud globale, `https://containers.cloud.ibm.com`.

Quando utilizzi la nuova funzionalità globale nella CLI Red Hat OpenShift on IBM Cloud, considera le seguenti modifiche rispetto alla funzionalità basata sulle regioni legacy.

* Elenco di risorse:
  * Quando elenchi le risorse, ad esempio con i comandi `ibmcloud oc clusters`, `ibmcloud oc subnets` o `ibmcloud oc zones`, vengono restituite le risorse presenti in tutte le ubicazioni. Per filtrare le risorse in base a un'ubicazione specifica, alcuni comandi includono un indicatore `--locations`. Ad esempio, se filtri i cluster per l'area metropolitana `wdc`, vengono restituiti i cluster multizona e i cluster a zona singola nei data center (zone) all'interno di quell'area metropolitana. Se filtri i cluster per il data center (zona) `wdc06`, vengono restituiti i cluster multizona che hanno un nodo di lavoro in quella zona e i cluster a zona singola in quella zona. Tieni presente che puoi passare un'ubicazione o un elenco di ubicazioni separate da virgole.
    Esempio di filtro per ubicazione:
    ```
    ibmcloud oc clusters --locations dal
    ```
    {: pre}
  * Altri comandi non restituiscono le risorse in tutte le ubicazioni. Per eseguire i comandi `credential-set/unset/get`, `api-key-reset` e `vlan-spanning-get`, devi specificare una regione in `--region`.

* Gestione delle risorse:
  * Quando utilizzi l'endpoint globale, puoi gestire le risorse per le quali disponi delle autorizzazioni di accesso in qualsiasi ubicazione, anche se imposti una regione eseguendo `ibmcloud oc region-set` e la risorsa che vuoi gestire si trova in un'altra regione.
  * Se hai dei cluster con lo stesso nome in regioni differenti, puoi utilizzare l'ID cluster quando esegui i comandi o impostare una regione con il comando `ibmcloud oc region-set` e utilizzare il nome cluster quando esegui i comandi.

* Funzionalità legacy:
  * Se devi elencare e gestire le risorse solo da una singola regione, puoi utilizzare il [comando ](/docs/containers?topic=containers-cli-plugin-kubernetes-service-cli#cs_init) `ibmcloud oc init` per specificare un endpoint regionale anziché l'endpoint globale.
    Esempio di indicazione dell'endpoint regionale Stati Uniti Sud:
    ```
    ibmcloud oc init --host https://us-south.containers.cloud.ibm.com
    ```
    {: pre}
  * Per utilizzare la funzionalità globale, puoi utilizzare nuovamente il comando `ibmcloud oc init` per specificare l'endpoint globale. Esempio per indicare nuovamente come destinazione l'endpoint globale:
    ```
    ibmcloud oc init --host https://containers.cloud.ibm.com
    ```
    {: pre}

</br></br>
**API Red Hat OpenShift on IBM Cloud**:
* [Inizia a utilizzare l'API](/docs/containers?topic=containers-cs_cli_install#cs_api).
* [Visualizza la documentazione sui comandi API](https://containers.cloud.ibm.com/global/swagger-global-api/).
* Genera un client dell'API da utilizzare nell'automazione utilizzando l'[API `swagger.json`](https://containers.cloud.ibm.com/global/swagger-global-api/swagger.json).

Per interagire con l'API Red Hat OpenShift on IBM Cloud globale, immetti il tipo di comando e accoda `global/v1/command` all'endpoint.

Esempio di API globale `GET /clusters`:
```
GET https://containers.cloud.ibm.com/global/v1/clusters
```
{: codeblock}

</br>

Se devi specificare una regione in una chiamata API, rimuovi il parametro `/global` dal percorso e passa il nome della regione nell'intestazione `X-Region`. Per elencare le regioni disponibili, esegui `ibmcloud oc regions`.

<br />

