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

# Archiviazione dei dati su un classico IBM Cloud File Storage
{: #file_storage}

{{site.data.keyword.cloud_notm}} File Storage è un'archiviazione file basata su NFS persistente, rapida, collegata alla rete e flessibile che puoi aggiungere alle tue applicazioni utilizzando i volumi persistenti (PV, persistent volume) Kubernetes. Puoi scegliere tra i livelli di archiviazione predefiniti con dimensioni in GB e IOPS che soddisfano i requisiti dei tuoi carichi di lavoro. Per appurare se {{site.data.keyword.cloud_notm}} File Storage è l'opzione di archiviazione giusta per te, vedi [Scelta di una soluzione di archiviazione](/docs/containers?topic=containers-storage_planning#choose_storage_solution). Per le informazioni sui prezzi, vedi [Fatturazione](/docs/infrastructure/FileStorage?topic=FileStorage-about#billing).
{: shortdesc}

{{site.data.keyword.cloud_notm}} File Storage è disponibile solo per i cluster standard configurati con la connettività di rete pubblica. Se il tuo cluster non può accedere alla rete pubblica, come ad esempio un cluster privato dietro un firewall o un cluster con solo l'endpoint del servizio privato abilitato, puoi eseguire il provisioning di archiviazione file se il tuo cluster esegue Kubernetes versione 1.13.4_1513, 1.12.6_1544, 1.11.8_1550 o successive. Le istanze di archiviazione file NFS sono specifiche per una singola zona. Se hai un cluster multizona, prendi in considerazione le [opzioni di archiviazione persistente multizona](/docs/containers?topic=containers-storage_planning#persistent_storage_overview).
{: important}

## Decisioni relative alla configurazione dell'archiviazione file
{: #file_predefined_storageclass}

{{site.data.keyword.containerlong}} fornisce delle classi di archiviazione predefinite per l'archiviazione file che puoi utilizzare per eseguire il provisioning di archiviazione file con una specifica configurazione.
{: shortdesc}

Ogni classe di archiviazione specifica il tipo di archiviazione file di cui esegui il provisioning, compresi la dimensione disponibile, il file system IOPS e la politica di conservazione.  

Dopo aver eseguito il provisioning di uno specifico tipo di archiviazione utilizzando una classe di archiviazione, non puoi modificare il tipo o la politica di conservazione per il dispositivo di archiviazione. Tuttavia, puoi [modificare la dimensione e l'IOPS](#file_change_storage_configuration) se vuoi aumentare la capacità e le prestazioni della tua archiviazione. Per modificare il tipo e la politica di conservazione per la tua archiviazione, devi [creare una nuova istanza di archiviazione e copiare i dati](/docs/containers?topic=containers-kube_concepts#update_storageclass) dalla vecchia istanza di archiviazione a quella nuova.
{: important}

Prima di iniziare: [accedi al tuo account. Se applicabile, specifica il gruppo di risorse appropriato. Imposta il contesto per il tuo cluster.](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure)

Per stabilire una configurazione di archiviazione:

1. Elenca le classi di archiviazione disponibili in {{site.data.keyword.containerlong}}.
   ```
   oc get storageclasses | grep file
   ```
   {: pre}

   Output di esempio:
   ```
   $ oc get storageclasses
   NAME                         TYPE
   ibmc-file-bronze (default)   ibm.io/ibmc-file
   ibmc-file-custom             ibm.io/ibmc-file
   ibmc-file-gold               ibm.io/ibmc-file
   ibmc-file-retain-bronze      ibm.io/ibmc-file
   ibmc-file-retain-custom      ibm.io/ibmc-file
   ibmc-file-retain-gold        ibm.io/ibmc-file
   ibmc-file-retain-silver      ibm.io/ibmc-file
   ibmc-file-silver             ibm.io/ibmc-file
   ```
   {: screen}

2. Esamina la configurazione di una classe di archiviazione.
  ```
  oc describe storageclass <storageclass_name>
  ```
  {: pre}

   Per ulteriori informazioni su ciascuna classe di archiviazione, vedi la sezione di [riferimento delle classi di archiviazione](#file_storageclass_reference). Se non trovi quello che stai cercando, considera la possibilità di creare una tua classe di archiviazione personalizzata. Per iniziare, controlla gli [esempi di classe di archiviazione personalizzata](#file_custom_storageclass).
   {: tip}

3. Scegli il tipo di archiviazione file di cui desideri eseguire il provisioning.
   - **Classi di archiviazione bronze, silver e gold:** queste classi di archiviazione eseguono il provisioning di [archiviazione Endurance](/docs/infrastructure/FileStorage?topic=FileStorage-about#provisioning-with-endurance-tiers). L'archiviazione Endurance ti consente di scegliere la dimensione dell'archiviazione in gigabyte in livelli IOPS predefiniti.
   - **Classe di archiviazione personalizzata:** questa classe di archiviazione esegue il provisioning di [archiviazione Performance](/docs/infrastructure/FileStorage?topic=FileStorage-about#provisioning-with-performance). Con l'archiviazione Performance, hai più controllo sulla dimensione dell'archiviazione e sull'IOPS.

4. Scegli la dimensione e l'IOPS per la tua archiviazione file. La dimensione e il numero di IOPS definiscono il numero totale di IOPS (operazioni di input/ output al secondo) che funge da indicatore della rapidità della tua archiviazione. Più IOPS totale ha la tua archiviazione e più rapidamente elabora le operazioni di lettura e scrittura.
   - **Classi di archiviazione bronze, silver e gold:** queste classi di archiviazione vengono fornite con un numero fisso di IOPS per gigabyte e ne viene eseguito il provisioning su dischi rigidi SSD. Il numero totale di IOPS dipende dalla dimensione dell'archiviazione che scegli. Puoi selezionare qualsiasi numero intero di gigabyte all'interno dell'intervallo di dimensioni consentite, come ad esempio 20 Gi, 256 Gi o 11854 Gi. Per determinare il numero totale di IOPS, devi moltiplicare l'IOPS con la dimensione selezionata. Ad esempio, se selezioni una dimensione di archiviazione file di 1000Gi nella classe di archiviazione silver che viene fornita con 4 IOPS per GB, la tua archiviazione ha un totale di 4000 IOPS.
     <table>
         <caption>Tabella di intervalli di dimensioni della classe di archiviazione e IOPS per gigabyte</caption>
         <thead>
         <th>Classe di archiviazione</th>
         <th>IOPS per gigabyte</th>
         <th>Intervallo di dimensioni in gigabyte</th>
         </thead>
         <tbody>
         <tr>
         <td>Bronze</td>
         <td>2 IOPS/GB</td>
         <td>20-12000 Gi</td>
         </tr>
         <tr>
         <td>Silver</td>
         <td>4 IOPS/GB</td>
         <td>20-12000 Gi</td>
         </tr>
         <tr>
         <td>Gold</td>
         <td>10 IOPS/GB</td>
         <td>20-4000 Gi</td>
         </tr>
         </tbody></table>
   - **Classe di archiviazione personalizzata:** quando scegli questa classe di archiviazione, hai più controllo sulla dimensione e sull'IOPS che desideri. Per la dimensione, puoi selezionare qualsiasi numero intero di gigabyte all'interno dell'intervallo di dimensioni consentito. La dimensione da te scelta determina l'intervallo IOPS a tua disposizione. Puoi scegliere un IOPS che è un multiplo di 100 che è compreso nell'intervallo specificato. L'IOPS che scegli è statico e non ridimensiona l'archiviazione. Ad esempio, se scegli 40Gi con 100 IOPS, l'IOPS totale rimane 100. </br></br> Anche il rapporto IOPS-gigabyte determina il tipo di disco rigido di cui viene eseguito il provisioning per tuo conto. Ad esempio, se hai 500Gi a 100 IOPS, il tuo rapporto IOPS-gigabyte è 0,2. Il provisioning dell'archiviazione con un rapporto inferiore o uguale a 0,3 viene eseguito sui dischi rigidi SATA. Se il tuo rapporto è superiore a 0,3, il provisioning della tua archiviazione viene eseguito su dischi rigidi SSD.  
     <table>
         <caption>Tabella di intervalli di dimensioni della classe di archiviazione personalizzata e IOPS</caption>
         <thead>
         <th>Intervallo di dimensioni in gigabyte</th>
         <th>Intervallo di IOPS in multipli di 100</th>
         </thead>
         <tbody>
         <tr>
         <td>20-39 Gi</td>
         <td>100-1000 IOPS</td>
         </tr>
         <tr>
         <td>40-79 Gi</td>
         <td>100-2000 IOPS</td>
         </tr>
         <tr>
         <td>80-99 Gi</td>
         <td>100-4000 IOPS</td>
         </tr>
         <tr>
         <td>100-499 Gi</td>
         <td>100-6000 IOPS</td>
         </tr>
         <tr>
         <td>500-999 Gi</td>
         <td>100-10000 IOPS</td>
         </tr>
         <tr>
         <td>1000-1999 Gi</td>
         <td>100-20000 IOPS</td>
         </tr>
         <tr>
         <td>2000-2999 Gi</td>
         <td>200-40000 IOPS</td>
         </tr>
         <tr>
         <td>3000-3999 Gi</td>
         <td>200-48000 IOPS</td>
         </tr>
         <tr>
         <td>4000-7999 Gi</td>
         <td>300-48000 IOPS</td>
         </tr>
         <tr>
         <td>8000-9999 Gi</td>
         <td>500-48000 IOPS</td>
         </tr>
         <tr>
         <td>10000-12000 Gi</td>
         <td>1000-48000 IOPS</td>
         </tr>
         </tbody></table>

5. Scegli se vuoi mantenere i tuoi dati dopo l'eliminazione del cluster o dell'attestazione del volume persistente (o PVC, persistent volume claim).
   - Se vuoi conservare i tuoi dati, scegli una classe di archiviazione `retain`. Quando elimini la PVC, viene eliminata solo la PVC. Il PV, il dispositivo di archiviazione fisico nel tuo account dell'infrastruttura IBM Cloud e i tuoi dati permangono. Per reclamare l'archiviazione e utilizzarla nuovamente nel tuo cluster, devi rimuovere il PV e attenerti alla procedura per l'[utilizzo dell'archiviazione file esistente](#existing_file).
   - Se vuoi che il PV, i dati e il tuo dispositivo di archiviazione file fisico vengano eliminati quando elimini la PVC, scegli una classe di archiviazione senza `retain`.

6. Scegli se preferisci una fatturazione oraria o mensile. Per ulteriori informazioni, controlla la sezione relativa ai [prezzi ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://www.ibm.com/cloud/file-storage/pricing). Per impostazione predefinita, il provisioning di tutti i dispositivi di archiviazione file viene eseguito con un tipo di fatturazione oraria.
   Se scegli un tipo di fatturazione mensile, quando rimuovi l'archiviazione persistente pagherai comunque l'addebito mensile, anche se l'hai utilizzata solo per un breve periodo di tempo.
   {: note}

<br />



## Aggiunta di archiviazione file alle applicazioni
{: #add_file}

Crea un'attestazione del volume persistente (o PVC, persistent volume claim) per [eseguire dinamicamente il provisioning](/docs/containers?topic=containers-kube_concepts#dynamic_provisioning) di archiviazione file per il tuo cluster. Il provisioning dinamico crea automaticamente il volume persistente (o PV, persistent volume) corrispondente e ordina il dispositivo di archiviazione fisico nel tuo account dell'infrastruttura IBM Cloud.
{:shortdesc}

Prima di iniziare:
- Se hai un firewall, [consenti l'accesso in uscita](/docs/containers?topic=containers-firewall#pvc) per gli intervalli IP dell'infrastruttura IBM Cloud delle zone in cui si trovano i tuoi cluster, in modo da poter creare le PVC.
- [Decidi in merito alla classe di archiviazione predefinita](#file_predefined_storageclass) oppure crea una [classe di archiviazione personalizzata](#file_custom_storageclass).

Intendi esporre l'archiviazione file in una serie con stato? Vedi [Utilizzo dell'archiviazione file in una serie con stato](#file_statefulset) per ulteriori informazioni.
{: tip}

Per aggiungere l'archiviazione file:

1.  Crea un file di configurazione per definire la tua attestazione del volume persistente (o PVC, persistent volume claim) e salva la configurazione come un file `.yaml`.

    - **Esempio per le classi di archiviazione bronze, silver e gold**:
       il seguente file `.yaml` crea un'attestazione denominata `mypvc` della classe di archiviazione`"ibmc-file-silver"`, fatturata mensilmente (`"monthly"`), con una dimensione in gigabyte di `24Gi`.

       ```
       apiVersion: v1
       kind: PersistentVolumeClaim
       metadata:
         name: mypvc
         labels:
           billingType: "monthly"
           region: us-south
           zone: dal13
       spec:
         accessModes:
           - ReadWriteMany
         resources:
           requests:
             storage: 24Gi
         storageClassName: ibmc-file-silver
       ```
       {: codeblock}

    -  **Esempio per l'utilizzo della classe di archiviazione personalizzata**:
       il seguente file `.yaml` crea un'attestazione denominata `mypvc` della classe di archiviazione `ibmc-file-retain-custom`, fatturata su base oraria (`"hourly"`), con una dimensione in gigabyte di `45Gi` e un IOPS di `"300"`.

       ```
       apiVersion: v1
       kind: PersistentVolumeClaim
       metadata:
         name: mypvc
         labels:
           billingType: "hourly"
           region: us-south
           zone: dal13
       spec:
         accessModes:
           - ReadWriteMany
         resources:
           requests:
             storage: 45Gi
             iops: "300"
         storageClassName: ibmc-file-retain-custom
       ```
       {: codeblock}

       <table>
       <caption>Descrizione dei componenti del file YAML</caption>
       <thead>
       <th colspan=2><img src="images/idea.png" alt="Icona Idea"/> Descrizione dei componenti del file YAML</th>
       </thead>
       <tbody>
       <tr>
       <td><code>metadata.name</code></td>
       <td>Immetti il nome della PVC.</td>
       </tr>
       <tr>
         <td><code>metadata.labels.billingType</code></td>
          <td>Specifica la frequenza per la quale viene calcolata la fattura di archiviazione, "mensile" o "oraria". Se non specifichi un tipo di fatturazione, viene eseguito il provisioning dell'archiviazione con un tipo di fatturazione oraria. </td>
       </tr>
       <tr>
       <td><code>metadata.labels.region</code></td>
       <td>Facoltativo: specifica la regione in cui desideri eseguire il provisioning dell'archiviazione file. Per connetterti alla tua archiviazione, crea l'archiviazione nella stessa regione in cui si trova il tuo cluster. Se specifichi la regione, devi specificare anche una zona. Se non specifichi una regione, o se la regione specificata non viene trovata, l'archiviazione viene creata nella stessa regione del tuo cluster.
       </br></br>Per ottenere la regione per il tuo cluster, esegui `ibmcloud oc cluster-get --cluster <cluster_name_or_ID>` e cerca il prefisso della regione nell'**URL master**, come ad esempio `eu-de` in `https://c2.eu-de.containers.cloud.ibm.com:11111`.
       </br></br><strong>Suggerimento: </strong>invece di specificare la regione e la zona nella PVC, puoi anche specificare questi valori in una [classe di archiviazione personalizzata](#file_multizone_yaml). Quindi, utilizza la tua classe di archiviazione nella sezione <code>metadata.annotations.volume.beta.kubernetes.io/storage-class</code> della tua PVC. Se la regione e la zona sono specificate nella classe di archiviazione e nella PVC, i valori nella PVC hanno la precedenza. </td>
       </tr>
       <tr>
       <td><code>metadata.labels.zone</code></td>
       <td>Facoltativo: specifica la zona in cui desideri eseguire il provisioning dell'archiviazione file. Per utilizzare la tua archiviazione in un'applicazione, crea l'archiviazione nella stessa zona in cui si trova il tuo nodo di lavoro. Per visualizzare la zona del tuo nodo di lavoro, esegui <code>ibmcloud oc workers --cluster &lt;cluster_name_or_ID&gt;</code> e controlla la colonna <strong>Zone</strong> dell'output della CLI. Se specifichi la zona, devi specificare anche una regione. Se non specifichi una zona o se la zona specificata non viene trovata in un cluster multizona, la zona viene selezionata su una base round-robin. </br></br><strong>Suggerimento: </strong>invece di specificare la regione e la zona nella PVC, puoi anche specificare questi valori in una [classe di archiviazione personalizzata](#file_multizone_yaml). Quindi, utilizza la tua classe di archiviazione nella sezione <code>metadata.annotations.volume.beta.kubernetes.io/storage-class</code> della tua PVC. Se la regione e la zona sono specificate nella classe di archiviazione e nella PVC, i valori nella PVC hanno la precedenza.
</td>
       </tr>
       <tr>
       <td><code>spec.accessMode</code></td>
       <td>Specifica una delle seguenti opzioni: <ul><li><strong>ReadWriteMany: </strong>la PVC può essere montata con più pod. Tutti i pod possono leggere dal e scrivere nel volume. </li><li><strong>ReadOnlyMany: </strong>la PVC può essere montata con più pod. Tutti i pod hanno un accesso di sola lettura. <li><strong>ReadWriteOnce: </strong>la PVC può essere montata da un solo pod. Questo pod può leggere dal e scrivere nel volume. </li></ul></td>
       </tr>
       <tr>
       <td><code>spec.resources.requests.storage</code></td>
       <td>Immetti la dimensione dell'archiviazione file, in gigabyte (Gi). Una volta eseguito il provisioning dell'archiviazione, non puoi modificare la dimensione della tua archiviazione file. Assicurati di specificare una dimensione che corrisponda alla quantità di dati che desideri memorizzare.</td>
       </tr>
       <tr>
       <td><code>spec.resources.requests.iops</code></td>
       <td>Questa opzione è disponibile solo per le classi di archiviazione personalizzate (`ibmc-file-custom / ibmc-file-retain-custom`). Specifica l'IOPS totale per l'archiviazione, selezionando un multiplo di 100 nell'intervallo consentito. Se scegli un IOPS diverso da quello elencato, viene arrotondato per eccesso.</td>
       </tr>
       <tr>
       <td><code>spec.storageClassName</code></td>
       <td>Il nome della classe di archiviazione che vuoi utilizzare per eseguire il provisioning dell'archiviazione file. Puoi scegliere di utilizzare una delle [classi di archiviazione fornite da IBM](#file_storageclass_reference) o [creare una tua classe di archiviazione](#file_custom_storageclass). </br> Se non specifichi una classe di archiviazione, il PV viene creato con la classe di archiviazione predefinita <code>ibmc-file-bronze</code>. </br></br><strong>Suggerimento:</strong> se vuoi modificare la classe di archiviazione predefinita, esegui <code>oc patch storageclass &lt;storageclass&gt; -p '{"metadata": {"annotations":{"storageclass.kubernetes.io/is-default-class":"true"}}}'</code> e sostituisci <code>&lt;storageclass&gt;</code> con il nome della classe di archiviazione.</td>
       </tr>
       </tbody></table>

    Se vuoi utilizzare una classe di archiviazione personalizzata, crea la tua PVC con il nome della classe di archiviazione corrispondente, una dimensione e un IOPS validi.   
    {: tip}

2.  Crea la PVC.

    ```
    oc apply -f mypvc.yaml
    ```
    {: pre}

3.  Verifica che la tua PVC sia stata creata e associata al PV. Questo processo può richiedere qualche minuto.

    ```
    oc describe pvc mypvc
    ```
    {: pre}

    Output di esempio:

    ```
    Name: mypvc
    Namespace: default
    StorageClass: ""
    Status:		Bound
    Volume:		pvc-0d787071-3a67-11e7-aafc-eef80dd2dea2
    Labels:		<none>
    Capacity:	20Gi
    Access Modes:	RWX
    Events:
      FirstSeen	LastSeen	Count	From								SubObjectPath	Type		Reason			Message
      ---------	--------	-----	----								-------------	--------	------			-------
      3m		3m		1	{ibm.io/ibmc-file 31898035-3011-11e7-a6a4-7a08779efd33 }			Normal		Provisioning		External provisioner is provisioning volume for claim "default/my-persistent-volume-claim"
      3m		1m		10	{persistentvolume-controller }							Normal		ExternalProvisioning	cannot find provisioner "ibm.io/ibmc-file", expecting that a volume for the claim is provisioned either manually or via external software
      1m		1m		1	{ibm.io/ibmc-file 31898035-3011-11e7-a6a4-7a08779efd33 }			Normal		ProvisioningSucceeded	Successfully provisioned volume pvc-0d787071-3a67-11e7-aafc-eef80dd2dea2

    ```
    {: screen}

4.  {: #file_app_volume_mount}Per montare l'archiviazione nella tua distribuzione, crea un file `.yaml` di configurazione e specifica la PVC che esegue il bind del PV.

    Se hai un'applicazione che richiede che un utente non root scriva nell'archiviazione persistente oppure un'applicazione che richiede che il percorso di montaggio appartenga all'utente root, vedi [Aggiunta di accesso utente non root all'archiviazione file NFS](/docs/containers?topic=containers-cs_troubleshoot_storage#nonroot) o [Abilitazione dell'autorizzazione root per l'archiviazione file NFS](/docs/containers?topic=containers-cs_troubleshoot_storage#nonroot).
    {: tip}

    ```
    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: <deployment_name>
      labels:
        app: <deployment_label>
    spec:
      selector:
        matchLabels:
          app: <app_name>
      template:
        metadata:
          labels:
            app: <app_name>
        spec:
          containers:
          - image: <image_name>
            name: <container_name>
            volumeMounts:
            - name: <volume_name>
              mountPath: /<file_path>
          volumes:
          - name: <volume_name>
            persistentVolumeClaim:
              claimName: <pvc_name>
    ```
    {: codeblock}

    <table>
    <caption>Descrizione dei componenti del file YAML</caption>
    <thead>
    <th colspan=2><img src="images/idea.png" alt="Icona Idea"/> Descrizione dei componenti del file YAML</th>
    </thead>
    <tbody>
        <tr>
    <td><code>metadata.labels.app</code></td>
    <td>Un'etichetta per la distribuzione.</td>
      </tr>
      <tr>
        <td><code>spec.selector.matchLabels.app</code> <br/> <code>spec.template.metadata.labels.app</code></td>
        <td>Un'etichetta per la tua applicazione.</td>
      </tr>
    <tr>
    <td><code>template.metadata.labels.app</code></td>
    <td>Un'etichetta per la distribuzione.</td>
      </tr>
    <tr>
    <td><code>spec.containers.image</code></td>
    <td>Il nome dell'immagine che vuoi utilizzare. Per elencare le immagini disponibili nel tuo account {{site.data.keyword.registryshort_notm}}, esegui `ibmcloud cr image-list`.</td>
    </tr>
    <tr>
    <td><code>spec.containers.name</code></td>
    <td>Il nome del contenitore che vuoi distribuire al tuo cluster.</td>
    </tr>
    <tr>
    <td><code>spec.containers.volumeMounts.mountPath</code></td>
    <td>Il percorso assoluto della directory in cui viene montato il volume nel contenitore. I dati scritti nel percorso di montaggio vengono memorizzati nella directory <code>root</code> nella tua istanza di archiviazione file fisica. Se vuoi condividere un volume tra diverse applicazioni, puoi specificare i [percorsi secondari di volume ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://kubernetes.io/docs/concepts/storage/volumes/#using-subpath) per ciascuna delle tue applicazioni.  </td>
    </tr>
    <tr>
    <td><code>spec.containers.volumeMounts.name</code></td>
    <td>Il nome del volume per montare il tuo pod.</td>
    </tr>
    <tr>
    <td><code>volumes.name</code></td>
    <td>Il nome del volume per montare il tuo pod. Normalmente questo nome è lo stesso di <code>volumeMounts.name</code>.</td>
    </tr>
    <tr>
    <td><code>volumes.persistentVolumeClaim.claimName</code></td>
    <td>Il nome della PVC che esegue il bind del PV che vuoi utilizzare. </td>
    </tr>
    </tbody></table>

5.  Crea la distribuzione.
     ```
     oc apply -f <local_yaml_path>
     ```
     {: pre}

6.  Verifica che il PV venga montato correttamente.

     ```
     oc describe deployment <deployment_name>
     ```
     {: pre}

     Il punto di montaggio è nel campo **Montaggi volume** e il volume nel campo **Volumi**.

     ```
      Volume Mounts:
          /var/run/secrets/kubernetes.io/serviceaccount from default-token-tqp61 (ro)
          /volumemount from myvol (rw)
     ...
     Volumes:
      myvol:
        Type: PersistentVolumeClaim (a reference to a PersistentVolumeClaim in the same namespace)
        ClaimName: mypvc
        ReadOnly: false
     ```
     {: screen}

<br />


## Utilizzo dell'archiviazione file esistente nel tuo cluster
{: #existing_file}

Se hai un dispositivo di archiviazione fisico esistente che vuoi usare nel tuo cluster, puoi creare manualmente il PV e la PVC per [eseguire in modo statico il provisioning](/docs/containers?topic=containers-kube_concepts#static_provisioning) dell'archiviazione.
{: shortdesc}

Prima di iniziare:
- Assicurati di avere almeno un nodo di lavoro nella stessa zona della tua istanza di archiviazione file esistente.
- [Accedi al tuo account. Se applicabile, specifica il gruppo di risorse appropriato. Imposta il contesto per il tuo cluster.](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure)

### Passo 1: Preparazione della tua archiviazione esistente.
{: #existing-file-1}

Prima di poter iniziare a montare la tua archiviazione esistente in un'applicazione, devi richiamare tutte le informazioni necessarie per il tuo PV e preparare l'archiviazione in modo che sia accessibile nel tuo cluster.  
{: shortdesc}

**Per l'archiviazione di cui era stato eseguito il provisioning con una classe di archiviazione `retain`:** </br>
se hai eseguito il provisioning dell'archiviazione con una classe di archiviazione `retain` e rimuovi la PVC, il PV e il dispositivo di archiviazione fisico non vengono rimossi automaticamente. Per riutilizzare l'archiviazione nel tuo cluster, devi rimuovere prima il PV rimanente.

Per utilizzare l'archiviazione esistente in un cluster diverso da quello dove ne hai eseguito il provisioning, attieniti alla procedura per l'[archiviazione che era stata creata esternamente al cluster](#external_storage) per aggiungere l'archiviazione alla sottorete del tuo nodo di lavoro.
{: tip}

1. Elenca i PV esistenti.
   ```
   oc get pv
   ```
   {: pre}

   Cerca il PV che appartiene alla tua archiviazione persistente. Il PV è in uno stato `released`.

2. Ottieni i dettagli del PV.
   ```
   oc describe pv <pv_name>
   ```
   {: pre}

3. Prendi nota di `CapacityGb`, `storageClass`, `failure-domain.beta.kubernetes.io/region`, `failure-domain.beta.kubernetes.io/zone`, `server` e `path`.

4. Rimuovi il PV.
   ```
   oc delete pv <pv_name>
   ```
   {: pre}

5. Verifica che il PV venga rimosso.
   ```
   oc get pv
   ```
   {: pre}

</br>

**Per l'archiviazione persistente di cui era stato eseguito il provisioning fuori dal cluster:** </br>
se vuoi utilizzare l'archiviazione esistente di cui avevi eseguito il provisioning in precedenza ma che non hai mai usato nel tuo cluster in precedenza, devi renderla disponibile nella stessa sottorete dei tuoi nodi di lavoro.

1.  {: #external_storage}Dal [portale dell'infrastruttura IBM Cloud ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://cloud.ibm.com/classic?), fai clic su **Archiviazione**.
2.  Fai clic su **File Storage** e, dal menu **Azioni**, seleziona **Autorizza host**.
3.  Seleziona **Sottoreti**.
4.  Dall'elenco a discesa, seleziona la sottorete VLAN privata a cui è connesso il nodo di lavoro. Per trovare la sottorete del tuo nodo di lavoro, esegui `ibmcloud oc workers --cluster <cluster_name>` e confronta l'IP privato (`Private IP`) del tuo nodo di lavoro con la sottorete che hai trovato nell'elenco a discesa.
5.  Fai clic su **Invia**.
6.  Fai clic sul nome dell'archiviazione file.
7.  Prendi nota dei campi `Mount Point`, `size` e `Location`. Il campo `Mount Point` viene visualizzato come `<nfs_server>:<file_storage_path>`.

### Passo 2: Creazione di un volume persistente (o PV, persistent volume) e di un'attestazione del volume persistente (o PVC, persistent volume claim) corrispondente
{: #existing-file-2}

1.  Crea un file di configurazione dell'archiviazione per il tuo PV. Includi i valori che hai richiamato in precedenza.

    ```
    apiVersion: v1
    kind: PersistentVolume
    metadata:
     name: mypv
     labels:
        failure-domain.beta.kubernetes.io/region: <region>
        failure-domain.beta.kubernetes.io/zone: <zone>
    spec:
     capacity:
       storage: "<size>"
     accessModes:
       - ReadWriteMany
     nfs:
       server: "<nfs_server>"
       path: "<file_storage_path>"
    ```
    {: codeblock}

    <table>
    <caption>Descrizione dei componenti del file YAML</caption>
    <thead>
    <th colspan=2><img src="images/idea.png" alt="Icona Idea"/> Descrizione dei componenti del file YAML</th>
    </thead>
    <tbody>
    <tr>
    <td><code>name</code></td>
    <td>Immetti il nome dell'oggetto del PV da creare.</td>
    </tr>
    <tr>
    <td><code>metadata.labels</code></td>
    <td>Immetti la regione e la zona che hai richiamato in precedenza. Devi disporre di almeno un nodo di lavoro nella stessa regione e nella stessa zona della tua archiviazione persistente per montare l'archiviazione nel tuo cluster. Se un PV per la tua archiviazione già esiste, [aggiungi l'etichetta di zona e regione](/docs/containers?topic=containers-kube_concepts#storage_multizone) al tuo PV.
    </tr>
    <tr>
    <td><code>spec.capacity.storage</code></td>
    <td>Immetti la dimensione di archiviazione della condivisione file NFS esistente che hai richiamato in precedenza. La dimensione di archiviazione deve essere scritta in gigabyte, ad esempio, 20Gi (20 GB) o 1000Gi (1 TB) e deve corrispondere alla dimensione della condivisione file esistente.</td>
    </tr>
    <tr>
    <td><code>spec.accessMode</code></td>
    <td>Specifica una delle seguenti opzioni: <ul><li><strong>ReadWriteMany: </strong>la PVC può essere montata con più pod. Tutti i pod possono leggere dal e scrivere nel volume. </li><li><strong>ReadOnlyMany: </strong>la PVC può essere montata con più pod. Tutti i pod hanno un accesso di sola lettura. <li><strong>ReadWriteOnce: </strong>la PVC può essere montata da un solo pod. Questo pod può leggere dal e scrivere nel volume. </li></ul></td>
    </tr>
    <tr>
    <td><code>spec.nfs.server</code></td>
    <td>Immetti l'ID server della condivisione file NFS che hai richiamato in precedenza.</td>
    </tr>
    <tr>
    <td><code>path</code></td>
    <td>Immetti il percorso alla condivisione file NFS che hai richiamato in precedenza.</td>
    </tr>
    </tbody></table>

3.  Crea il PV nel tuo cluster.

    ```
    oc apply -f mypv.yaml
    ```
    {: pre}

4.  Verifica che il PV sia stato creato.

    ```
    oc get pv
    ```
    {: pre}

5.  Crea un altro file di configurazione per creare la tua PVC. Affinché la PVC corrisponda all'oggetto del PV creato in precedenza, devi scegliere lo stesso valore per `storage` e `accessMode`. Il campo `storage-class` deve essere vuoto. Se qualcuno di questi campi non corrisponde al PV, viene [dinamicamente eseguito il provisioning](/docs/containers?topic=containers-kube_concepts#dynamic_provisioning) di un nuovo PV e di una nuova istanza di archiviazione fisica.

    ```
    kind: PersistentVolumeClaim
    apiVersion: v1
    metadata:
     name: mypvc
    spec:
     accessModes:
       - ReadWriteMany
     resources:
       requests:
         storage: "<size>"
     storageClassName:
    ```
    {: codeblock}

6.  Crea la tua PVC.

    ```
    oc apply -f mypvc.yaml
    ```
    {: pre}

7.  Verifica che la tua PVC sia stata creata e associata al PV. Questo processo può richiedere qualche minuto.

    ```
    oc describe pvc mypvc
    ```
    {: pre}

    Output di esempio:

    ```
    Name: mypvc
    Namespace: default
    StorageClass: ""
    Status: Bound
    Volume: pvc-0d787071-3a67-11e7-aafc-eef80dd2dea2
    Labels: <none>
    Capacity: 20Gi
    Access Modes: RWX
    Events:
      FirstSeen LastSeen Count From        SubObjectPath Type Reason Message
      --------- -------- ----- ----        ------------- -------- ------ -------
      3m 3m 1 {ibm.io/ibmc-file 31898035-3011-11e7-a6a4-7a08779efd33 } Normal Provisioning External provisioner is provisioning volume for claim "default/my-persistent-volume-claim"
      3m 1m	 10 {persistentvolume-controller } Normal ExternalProvisioning cannot find provisioner "ibm.io/ibmc-file", expecting that a volume for the claim is provisioned either manually or via external software
      1m 1m 1 {ibm.io/ibmc-file 31898035-3011-11e7-a6a4-7a08779efd33 } Normal ProvisioningSucceeded	Successfully provisioned volume pvc-0d787071-3a67-11e7-aafc-eef80dd2dea2
    ```
    {: screen}


Hai creato correttamente un PV e lo hai collegato ad una PVC. Gli utenti del cluster possono ora [montare la PVC](#file_app_volume_mount) nelle proprie distribuzioni e iniziare a leggere e a scrivere sull'oggetto del PV.

<br />



## Utilizzo dell'archiviazione file in una serie con stato
{: #file_statefulset}

Se hai un'applicazione con stato, come ad esempio un database, puoi creare delle serie con stato che utilizzano l'archiviazione file per memorizzare i dati della tua applicazione. In alternativa, puoi utilizzare un DBaaS (database-as-a-service) {{site.data.keyword.cloud_notm}} e memorizzare i tuoi dati sul cloud.
{: shortdesc}

**Cosa devo sapere quando aggiungo l'archiviazione file a una serie con stato?** </br>
Per aggiungere l'archiviazione a una serie con stato, devi specificare la tua configurazione di archiviazione nella sezione `volumeClaimTemplates` del file YAML della serie con stato. La sezione `volumeClaimTemplates` è la base per la tua PVC e può includere la classe di archiviazione e la dimensione o l'IOPS della tua archiviazione file di cui desideri eseguire il provisioning. Tuttavia, se vuoi includere etichette in `volumeClaimTemplates`, Kubernetes non le include durante la creazione della PVC. Devi invece aggiungere le etichette direttamente alla tua serie con stato.

Non puoi distribuire due serie con stato contemporaneamente. Se tenti di creare una serie con stato prima ne venga completamente distribuita un'altra, la distribuzione della tua serie con stato potrebbe portare a risultati imprevisti.
{: important}

**Come posso creare la mia serie con stato in una zona specifica?** </br>
In un cluster multizona, puoi specificare la zona e la regione in cui vuoi creare la serie con stato nella sezione `spec.selector.matchLabels` e `spec.template.metadata.labels` del file YAML della serie con stato. In alternativa, puoi aggiungere queste etichette a una [classe di archiviazione personalizzata](/docs/containers?topic=containers-kube_concepts#customized_storageclass) e utilizzare questa classe di archiviazione nella sezione `volumeClaimTemplates` della tua serie con stato.

**Posso ritardare l'associazione di un PV al mio pod con stato finché il pod non è pronto?**<br>
Sì, puoi [creare una classe di archiviazione personalizzata](#file-topology) per la tua PVC che include il campo [`volumeBindingMode: WaitForFirstConsumer` ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://kubernetes.io/docs/concepts/storage/storage-classes/#volume-binding-mode).

**Quali opzioni ho per aggiungere l'archiviazione file a una serie con stato?** </br>
Se vuoi creare automaticamente la tua PVC quando crei la serie con stato, utilizza il [provisioning dinamico](#file_dynamic_statefulset). Puoi anche scegliere di eseguire il [pre-provisioning delle PVC o utilizzare PVC esistenti](#file_static_statefulset) con la tua serie con stato.  

### Provisioning dinamico: creazione della PVC quando crei una serie con stato
{: #file_dynamic_statefulset}

Utilizza questa opzione se vuoi creare automaticamente la PVC quando crei la serie con stato.
{: shortdesc}

Prima di iniziare: [accedi al tuo account. Se applicabile, specifica il gruppo di risorse appropriato. Imposta il contesto per il tuo cluster.](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure)

1. Verifica che tutte le serie con stato esistenti nel tuo cluster siano state completamente distribuite. Se una serie con stato è ancora in fase di distribuzione, non puoi iniziare a creare la tua serie con stato. Devi attendere che tutte le serie con stato nel tuo cluster vengano distribuite completamente per evitare risultati imprevisti.
   1. Elenca le serie con stato esistenti nel tuo cluster.
      ```
      oc get statefulset --all-namespaces
      ```
      {: pre}

      Output di esempio:
      ```
      NAME              DESIRED   CURRENT   AGE
      mystatefulset     3         3         6s
      ```
      {: screen}

   2. Visualizza la sezione **Pods Status** di ogni serie con stato per assicurarti che la distribuzione della serie con stato sia terminata.  
      ```
      oc describe statefulset <statefulset_name>
      ```
      {: pre}

      Output di esempio:
      ```
      Name:               nginx
      Namespace:          default
      CreationTimestamp:  Fri, 05 Oct 2018 13:22:41 -0400
      Selector:           app=nginx,billingType=hourly,region=us-south,zone=dal10
      Labels:             app=nginx
                          billingType=hourly
                          region=us-south
                          zone=dal10
      Annotations:        oc.kubernetes.io/last-applied-configuration={"apiVersion":"apps/v1","kind":"StatefulSet","metadata":{"annotations":{},"name":"nginx","namespace":"default"},"spec":{"podManagementPolicy":"Par...
      Replicas:           3 desired | 3 total
      Pods Status:        0 Running / 3 Waiting / 0 Succeeded / 0 Failed
      Pod Template:
        Labels:  app=nginx
                 billingType=hourly
                 region=us-south
                 zone=dal10
      ...
      ```
      {: screen}

      Una serie con stato è completamente distribuita quando il numero di repliche che trovi nella sezione **Replicas** dell'output della CLI è uguale al numero di pod in stato **Running** nella sezione **Pods Status**. Se una serie con stato non è ancora completamente distribuita, attendi fino al termine della distribuzione prima di procedere.

2. Crea un file di configurazione per la tua serie con stato e il servizio che utilizzi per esporre la serie con stato.

  - **Serie di stato di esempio che specifica una zona**

    Il seguente esempio mostra come distribuire NGINX come una serie con stato con 3 repliche. Per ogni replica, viene eseguito il provisioning di un dispositivo di archiviazione file da 20 gigabyte in base alle specifiche nella classe di archiviazione `ibmc-file-retain-bronze`. Il provisioning di tutti i dispositivi di archiviazione viene eseguito nella zona `dal10`. Poiché non è possibile accedere all'archiviazione file da altre zone, tutte le repliche della serie con stato sono distribuite anche sui nodi di lavoro che si trovano in `dal10`.

    ```
    apiVersion: v1
    kind: Service
    metadata:
     name: nginx
     labels:
       app: nginx
    spec:
     ports:
     - port: 80
       name: web
     clusterIP: None
     selector:
       app: nginx
    ---
    apiVersion: apps/v1
    kind: StatefulSet
    metadata:
     name: nginx
    spec:
     serviceName: "nginx"
     replicas: 3
     podManagementPolicy: Parallel
     selector:
       matchLabels:
         app: nginx
         billingType: "hourly"
         region: "us-south"
         zone: "dal10"
     template:
       metadata:
         labels:
           app: nginx
           billingType: "hourly"
           region: "us-south"
           zone: "dal10"
       spec:
         containers:
         - name: nginx
           image: k8s.gcr.io/nginx-slim:0.8
           ports:
           - containerPort: 80
             name: web
           volumeMounts:
           - name: myvol
             mountPath: /usr/share/nginx/html
     volumeClaimTemplates:
     - metadata:
         name: myvol
       spec:
         accessModes:
         - ReadWriteOnce
         resources:
           requests:
             storage: 20Gi
             iops: "300" #required only for performance storage
         storageClassName: ibmc-file-retain-bronze
    ```
    {: codeblock}

  - **Serie con stato di esempio con regola di anti-affinità e creazione di archiviazione file ritardata.**

    Il seguente esempio mostra come distribuire NGINX come una serie con stato con 3 repliche. La serie con stato non specifica la regione e la zona dove viene creata l'archiviazione file. La serie con stato utilizza invece una regola anti-affinità per garantire che i pod vengano distribuiti tra i nodi di lavoro e le zone. L'anti-affinità dei nodi di lavoro si ottiene definendo l'etichetta `app: nginx`. Questa etichetta indica al programma di pianificazione Kubernetes di non pianificare un pod su un nodo di lavoro se un pod con la stessa etichetta viene già eseguito su questo nodo di lavoro. L'etichetta `topologykey: failure-domain.beta.kubernetes.io/zone` limita ancora di più questa regola di anti-affinità e impedisce che il pod venga pianificato su un nodo di lavoro che si trova nella stessa zona di un nodo di lavoro che già esegue un pod con l'etichetta `app: nginx`. Per ogni pod di serie con stato, vengono create due PVC, come definito nella sezione `volumeClaimTemplates`, ma la creazione delle istanze di archiviazione file viene ritardata finché non viene pianificato un pod di serie con stato che utilizza l'archiviazione. Questa configurazione viene indicata come [pianificazione dei volumi che rileva la topologia](https://kubernetes.io/blog/2018/10/11/topology-aware-volume-provisioning-in-kubernetes/).

    ```
    apiVersion: storage.k8s.io/v1
    kind: StorageClass
    metadata:
      name: ibmc-file-bronze-delayed
    parameters:
      billingType: hourly
      classVersion: "2"
      iopsPerGB: "2"
      sizeRange: '[20-12000]Gi'
      type: Endurance
    provisioner: ibm.io/ibmc-file
    reclaimPolicy: Delete
    volumeBindingMode: WaitForFirstConsumer
    ---
    apiVersion: v1
    kind: Service
    metadata:
      name: nginx
      labels:
        app: nginx
    spec:
      ports:
      - port: 80
        name: web
      clusterIP: None
      selector:
        app: nginx
    ---
    apiVersion: apps/v1
    kind: StatefulSet
    metadata:
      name: web
    spec:
      serviceName: "nginx"
      replicas: 3
      podManagementPolicy: "Parallel"
      selector:
        matchLabels:
          app: nginx
      template:
        metadata:
          labels:
            app: nginx
        spec:
          affinity:
            podAntiAffinity:
              preferredDuringSchedulingIgnoredDuringExecution:
              - weight: 100
            podAffinityTerm:
              labelSelector:
                matchExpressions:
                    - key: app
                  operator: In
                  values:
                      - nginx
                  topologyKey: failure-domain.beta.kubernetes.io/zone
          containers:
          - name: nginx
            image: k8s.gcr.io/nginx-slim:0.8
            ports:
            - containerPort: 80
              name: web
            volumeMounts:
            - name: myvol1
              mountPath: /usr/share/nginx/html
            - name: myvol2
              mountPath: /tmp1
      volumeClaimTemplates:
      - metadata:
          name: myvol1
        spec:
          accessModes:
          - ReadWriteMany # access mode
          resources:
            requests:
              storage: 20Gi
          storageClassName: ibmc-file-bronze-delayed
      - metadata:
          name: myvol2
        spec:
          accessModes:
          - ReadWriteMany # access mode
          resources:
            requests:
              storage: 20Gi
          storageClassName: ibmc-file-bronze-delayed
    ```
    {: codeblock}

    <table>
    <caption>Descrizione dei componenti del file YAML della serie con stato</caption>
    <thead>
    <th colspan=2><img src="images/idea.png" alt="Icona Idea"/> Descrizione dei componenti del file YAML della serie con stato</th>
    </thead>
    <tbody>
    <tr>
    <td style="text-align:left"><code>metadata.name</code></td>
    <td style="text-align:left">Immetti un nome per la tua serie con stato. Il nome che immetti viene utilizzato per creare il nome della tua PVC nel formato: <code>&lt;volume_name&gt;-&lt;statefulset_name&gt;-&lt;replica_number&gt;</code>. </td>
    </tr>
    <tr>
    <td style="text-align:left"><code>spec.serviceName</code></td>
    <td style="text-align:left">Immetti il nome del servizio che vuoi utilizzare per esporre la tua serie con stato. </td>
    </tr>
    <tr>
    <td style="text-align:left"><code>spec.replicas</code></td>
    <td style="text-align:left">Immetti il numero di repliche per la tua serie con stato. </td>
    </tr>
    <tr>
    <td style="text-align:left"><code>spec.podManagementPolicy</code></td>
    <td style="text-align:left">Immetti la politica di gestione pod che vuoi utilizzare per la tua serie con stato. Scegli tra le seguenti opzioni: <ul><li><strong><code>OrderedReady</code></strong>: con questa opzione, le repliche della serie con stato vengono distribuite una dopo l'altra. Ad esempio, se hai distribuito 3 repliche, Kubernetes crea la PVC per la prima replica, attende che la PVC venga collegata, distribuisce la replica della serie con stato e monta la PVC sulla replica. Al termine della distribuzione, viene distribuita la seconda replica. Per ulteriori informazioni su questa opzione, vedi [`Gestione pod OrderedReady` ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://kubernetes.io/docs/concepts/workloads/controllers/statefulset/#orderedready-pod-management). </li><li><strong>Parallel: </strong>con questa opzione, la distribuzione di tutte le repliche della serie con stato viene avviata contemporaneamente. Se la tua applicazione supporta la distribuzione parallela di repliche, utilizza questa opzione per risparmiare tempo di distribuzione per le tue PVC e repliche della serie con stato. </li></ul></td>
    </tr>
    <tr>
    <td style="text-align:left"><code>spec.selector.matchLabels</code></td>
    <td style="text-align:left">Immetti tutte le etichette che vuoi includere nella serie con stato e nella PVC. Le etichette che includi nella sezione <code>volumeClaimTemplates</code> della tua serie con stato non vengono riconosciute da Kubernetes. Le etichette di esempio che potresti voler includere sono: <ul><li><code><strong>region</strong></code> e <code><strong>zone</strong></code>: se vuoi che tutte le tue repliche della serie con stato e PVC vengano create in una specifica zona, aggiungi entrambe le etichette. Puoi anche specificare la zona e la regione nella classe di archiviazione che utilizzi. Se non specifichi una zona e una regione e hai un cluster multizona, la zona in cui viene eseguito il provisioning della tua archiviazione è selezionata su una base round-robin per bilanciare equamente le richieste di volume tra tutte le zone.</li><li><code><strong>billingType</strong></code>: immetti il tipo di fatturazione che vuoi utilizzare per le tue PVC. Scegli tra <code>hourly</code> o <code>monthly</code>. Se non specifichi questa etichetta, tutte le PVC vengono create con un tipo di fatturazione oraria. </li></ul></td>
    </tr>
    <tr>
    <td style="text-align:left"><code>spec.template.metadata.labels</code></td>
    <td style="text-align:left">Immetti le stesse etichette che hai aggiunto alla sezione <code>spec.selector.matchLabels</code>. </td>
    </tr>
    <tr>
    <td style="text-align:left"><code>spec.template.spec.affinity</code></td>
    <td style="text-align:left">Specifica la tua regola di anti-affinità per garantire che i tuoi pod di serie con stato siano distribuiti tra i nodi di lavoro e le zone. L'esempio mostra una regola di anti-affinità in cui il pod di serie con stato preferisce non essere pianificato su un nodo di lavoro dove viene eseguito un pod che ha l'etichetta `app: nginx`. `topologykey: failure-domain.beta.kubernetes.io/zone` limita ancora di più questa regole di anti-affinità e impedisce al pod di essere pianificato su un nodo di lavoro se il nodo di lavoro si trova nella stessa zona di un pod che ha l'etichetta `app: nginx`. Utilizzando questa regola di anti-affinità, puoi ottenere l'anti-affinità tra i nodi di lavoro e le zone. </td>
    </tr>
    <tr>
    <td style="text-align:left"><code>spec.volumeClaimTemplates.metadata.name</code></td>
    <td style="text-align:left">Immetti un nome per il tuo volume. Utilizza lo stesso nome che hai definito nella sezione <code>spec.containers.volumeMount.name</code>. Il nome che immetti qui viene utilizzato per creare il nome della tua PVC nel formato: <code>&lt;volume_name&gt;-&lt;statefulset_name&gt;-&lt;replica_number&gt;</code>. </td>
    </tr>
    <tr>
    <td style="text-align:left"><code>spec.volumeClaimTemplates.spec.resources.</code></br><code>requests.storage</code></td>
    <td style="text-align:left">Immetti la dimensione dell'archiviazione file in gigabyte (Gi).</td>
    </tr>
    <tr>
    <td style="text-align:left"><code>spec.volumeClaimTemplates.spec.resources.</code></br><code>requests.iops</code></td>
    <td style="text-align:left">Se vuoi eseguire il provisioning dell'[archiviazione Performance](#file_predefined_storageclass), immetti il numero di IOPS. Se utilizzi una classe di archiviazione Endurance e specifichi un numero di IOPS, il numero di IOPS viene ignorato. Invece, viene utilizzato l'IOPS specificato nella tua classe di archiviazione.  </td>
    </tr>
    <tr>
    <td style="text-align:left"><code>spec.volumeClaimTemplates.</code></br><code>spec.storageClassName</code></td>
    <td style="text-align:left">Immetti la classe di archiviazione che vuoi utilizzare. Per elencare le classi di archiviazione esistenti, esegui <code>oc get storageclasses | grep file</code>. Se non specifichi alcuna classe di archiviazione, la PVC viene creata con la classe di archiviazione predefinita impostata nel tuo cluster. Assicurati che la classe di archiviazione predefinita utilizzi il provisioner <code>ibm.io/ibmc-file</code> in modo che la tua serie con stato venga fornita con l'archiviazione file.</td>
    </tr>
    </tbody></table>

4. Crea la tua serie con stato.
   ```
   oc apply -f statefulset.yaml
   ```
   {: pre}

5. Attendi che la serie con stato venga distribuita.
   ```
   oc describe statefulset <statefulset_name>
   ```
   {: pre}

   Per visualizzare lo stato corrente delle tue PVC, esegui `oc get pvc`. Il nome della tua PVC ha il formato `<volume_name>-<statefulset_name>-<replica_number>`.
   {: tip}

### Provisioning statico: utilizzo di una PVC esistente con la tua serie con stato
{: #file_static_statefulset}

Puoi eseguire il pre-provisioning delle tue PVC prima di creare la serie con stato oppure utilizzare PVC esistenti con la tua serie con stato.
{: shortdesc}

Quando [esegui dinamicamente il provisioning delle tue PVC quando crei la serie con stato](#file_dynamic_statefulset), il nome della PVC viene assegnato in base ai valori che hai usato nel file YAML della serie con stato. Affinché la serie con stato utilizzi le PVC esistenti, il nome delle tue PVC deve corrispondere al nome che viene automaticamente creato quando si utilizza il provisioning dinamico.

Prima di iniziare: [accedi al tuo account. Se applicabile, specifica il gruppo di risorse appropriato. Imposta il contesto per il tuo cluster.](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure)

1. Se desideri eseguire il pre-provisioning della tua PVC prima di creare la serie con stato, esegui i passi da 1 a 3 in [Aggiunta di archiviazione file alle applicazioni](#add_file) per creare una PVC per ogni replica della serie con stato. Assicurati di creare la tua PVC con un nome che rispetta il seguente formato:`<volume_name>-<statefulset_name>-<replica_number>`.
   - **`<volume_name>`**: utilizza il nome che vuoi specificare nella sezione `spec.volumeClaimTemplates.metadata.name` della tua serie con stato, ad esempio `nginxvol`.
   - **`<statefulset_name>`**: utilizza il nome che vuoi specificare nella sezione `metadata.name` della tua serie con stato, ad esempio `nginx_statefulset`.
   - **`<replica_number>`**: immetti il numero delle tue repliche a partire da 0.

   Ad esempio, se devi creare 3 repliche della serie con stato, crea 3 PVC con i seguenti nomi: `nginxvol-nginx_statefulset-0`, `nginxvol-nginx_statefulset-1` e `nginxvol-nginx_statefulset-2`.  

   Intendi creare una PVC e un PV per un'istanza di archiviazione file esistente? Crea la tua PVC e il tuo PV utilizzando il [provisioning statico](#existing_file).
   {: tip}

2. Attieniti alla procedura in [Provisioning dinamico: creazione della PVC quando crei una serie con stato](#file_dynamic_statefulset) per creare la tua serie con stato. Il nome della tua PVC rispetta il formato `<volume_name>-<statefulset_name>-<replica_number>`. Assicurati di utilizzare i seguenti valori dal tuo nome PVC nella specifica della serie con stato:
   - **`spec.volumeClaimTemplates.metadata.name`**: immetti il `<volume_name>` del tuo nome PVC.
   - **`metadata.name`**: immetti il `<statefulset_name>` del tuo nome PVC.
   - **`spec.replicas`**: immetti il numero di repliche che vuoi creare per la tua serie con stato. Il numero di repliche deve essere uguale al numero di PVC create in precedenza.

   Se le tue PVC si trovano in zone differenti, non includere un'etichetta di regione o zona nella tua serie con stato.
   {: note}

3. Verifica che le PVC siano utilizzate nei pod di replica della serie con stato.
   1. Elenca i pod nel tuo cluster. Identifica i pod che appartengono alla tua serie con stato.
      ```
      oc get pods
      ```
      {: pre}

   2. Verifica che la PVC esistente sia montata nella replica della serie con stato. Esamina il **`ClaimName`** nella sezione **`Volumes`** del tuo output della CLI.
      ```
      oc describe pod <pod_name>
      ```
      {: pre}

      Output di esempio:
      ```
      Name:           nginx-0
      Namespace:      default
      Node:           10.xxx.xx.xxx/10.xxx.xx.xxx
      Start Time:     Fri, 05 Oct 2018 13:24:59 -0400
      ...
      Volumes:
        myvol:
          Type:       PersistentVolumeClaim (a reference to a PersistentVolumeClaim in the same namespace)
          ClaimName:  myvol-nginx-0
     ...
      ```
      {: screen}

<br />


## Modifica della dimensione e dell'IOPS del tuo dispositivo di archiviazione esistente
{: #file_change_storage_configuration}

Se vuoi modificare la capacità o le prestazioni di archiviazione, puoi modificare il tuo volume esistente.
{: shortdesc}

Per domande sulla fatturazione e per trovare i passi su come utilizzare la console {{site.data.keyword.cloud_notm}} per modificare la tua archiviazione, vedi [Espansione della capacità di condivisione file](/docs/infrastructure/FileStorage?topic=FileStorage-expandCapacity#expandCapacity).
{: tip}

1. Elenca le PVC nel tuo cluster e prendi nota del nome del PV associato dalla colonna **VOLUME**.
   ```
   oc get pvc
   ```
   {: pre}

   Output di esempio:
   ```
   NAME             STATUS    VOLUME                                     CAPACITY   ACCESS MODES   STORAGECLASS        AGE
   myvol            Bound     pvc-01ac123a-123b-12c3-abcd-0a1234cb12d3   20Gi       RWX            ibmc-file-bronze    147d
   ```
   {: screen}

2. Richiama i valori **`StorageType`**, **`volumeId`** e **`server`** dell'archiviazione file fisica associata alla tua PVC elencando i dettagli del PV a cui è collegata la PVC. Sostituisci `<pv_name>` con il nome del PV che hai richiamato nel passo precedente. Il tipo di archiviazione, l'ID volume e il nome server sono mostrati nella sezione **`Labels`** del tuo output della CLI.
   ```
   oc describe pv <pv_name>
   ```
   {: pre}

   Output di esempio:
   ```
   Name:            pvc-4b62c704-5f77-11e8-8a75-b229c11ba64a
   Labels:          CapacityGb=20
                    Datacenter=dal10
                    Iops=2
                    StorageType=ENDURANCE
                    Username=IBM02SEV1543159_6
                    billingType=hourly
                    failure-domain.beta.kubernetes.io/region=us-south
                    failure-domain.beta.kubernetes.io/zone=dal10
                    path=IBM01SEV1234567_8ab12t
                    server=fsf-dal1001g-fz.adn.networklayer.com
                    volumeId=12345678
   ...
   ```
   {: screen}

3. Modifica la dimensione o l'IOPS del volume nel tuo account dell'infrastruttura IBM Cloud.

   Esempio per l'archiviazione Performance:
   ```
   ibmcloud sl file volume-modify <volume_ID> --new-size <size> --new-iops <iops>
   ```
   {: pre}

   Esempio per l'archiviazione Endurance:
   ```
   ibmcloud sl file volume-modify <volume_ID> --new-size <size> --new-tier <iops>
   ```
   {: pre}

   <table>
   <caption>Descrizione dei componenti del comando</caption>
   <thead>
   <th colspan=2><img src="images/idea.png" alt="Icona Idea"/> Descrizione dei componenti del file YAML</th>
   </thead>
   <tbody>
   <tr>
   <td><code>&lt;volume_ID&gt;</code></td>
   <td>Immetti l'ID del volume che hai richiamato in precedenza.</td>
   </tr>
   <tr>
   <td><code>&lt;new-size&gt;</code></td>
   <td>Immetti la nuova dimensione in gigabyte (Gi) per il tuo volume. Per le dimensioni valide, vedi [Decisioni relative alla configurazione dell'archiviazione file](#file_predefined_storageclass). La dimensione che immetti deve essere maggiore o uguale alla dimensione corrente del tuo volume. Se non specifichi una nuova dimensione, viene utilizzata la dimensione corrente del volume. </td>
   </tr>
   <tr>
   <td><code>&lt;new-iops&gt;</code></td>
   <td>Solo per l'archiviazione Performance. Immetti il nuovo numero di IOPS che desideri. Per l'IOPS valido, vedi [Decisioni relative alla configurazione dell'archiviazione file](#file_predefined_storageclass). Se non specifichi l'IOPS, viene utilizzato l'IOPS corrente. <p class="note">Se il rapporto IOPS/GB originale per il volume è inferiore a 0,3, il nuovo rapporto IOPS/GB deve essere inferiore a 0,3. Se il rapporto IOPS/GB originale per il volume è maggiore o uguale a 0,3, il nuovo rapporto IOPS/GB per il volume deve essere maggiore o uguale a 0,3.</p> </td>
   </tr>
   <tr>
   <td><code>&lt;new-tier&gt;</code></td>
   <td>Solo per l'archiviazione Endurance. Immetti il nuovo numero di IOPS per GB che desideri. Per l'IOPS valido, vedi [Decisioni relative alla configurazione dell'archiviazione file](#file_predefined_storageclass). Se non specifichi l'IOPS, viene utilizzato l'IOPS corrente. <p class="note">Se il rapporto IOPS/GB originale per il volume è inferiore a 0,25, il nuovo rapporto IOPS/GB deve essere inferiore a 0,25. Se il rapporto IOPS/GB originale per il volume è maggiore o uguale a 0,25, il nuovo rapporto IOPS/GB per il volume deve essere maggiore o uguale a 0,25.</p> </td>
   </tr>
   </tbody>
   </table>

   Output di esempio:
   ```
   Order 31020713 was placed successfully!.
   > Storage as a Service

   > 40 GBs

   > 2 IOPS per GB

   > 20 GB Storage Space (Snapshot Space)

   You may run 'ibmcloud sl file volume-list --order 12345667' to find this file volume after it is ready.
   ```
   {: screen}

4. Se hai modificato la dimensione del tuo volume e usi il volume nel pod, accedi al pod per verificare la nuova dimensione.
   1. Elenca tutti i pod che utilizzano la PVC.
      ```
      oc get pods --all-namespaces -o=jsonpath='{range .items[*]}{"\n"}{.metadata.name}{":\t"}{range .spec.volumes[*]}{.persistentVolumeClaim.claimName}{" "}{end}{end}' | grep "<pvc_name>"
      ```
      {: pre}

      I pod vengono restituiti nel formato: `<pod_name>: <pvc_name>`.
   2. Accedi al tuo pod.
      ```
      oc exec -it <pod_name> bash
      ```
      {: pre}

   3. Mostra le statistiche di utilizzo del disco e trova il percorso server per il tuo volume che hai richiamato in precedenza.
      ```
      df -h
      ```
      {: pre}

      Output di esempio:
      ```
      Filesystem                                                      Size  Used Avail Use% Mounted on
      overlay                                                          99G  4.8G   89G   6% /
      tmpfs                                                            64M     0   64M   0% /dev
      tmpfs                                                           7.9G     0  7.9G   0% /sys/fs/cgroup
      fsf-dal1001g-fz.adn.networklayer.com:/IBM01SEV1234567_6/data01   40G     0   40G   0% /myvol
      ```
      {: screen}


## Modifica della versione NFS predefinita
{: #nfs_version}

La versione dell'archiviazione file determina il protocollo che viene utilizzato per comunicare con il server dell'archiviazione file {{site.data.keyword.cloud_notm}}. Per impostazione predefinita, le istanze dell'archiviazione file sono configurate con NFS versione 4. Puoi modificare il PV esistente con una versione precedente di NFS se la tua applicazione richiede una versione specifica per funzionare correttamente.
{: shortdesc}

Per modificare la versione NFS predefinita, puoi creare una nuova classe di archiviazione per fornire l'archiviazione file in modo dinamico al tuo cluster oppure scegliere un PV esistente montato nel tuo pod.

Per applicare gli ultimi aggiornamenti di sicurezza e per prestazioni migliori, utilizza la versione NFS predefinita e non modificare NFS ad una versione precedente.
{: important}

**Per creare una classe di archiviazione personalizzata con una specifica versione NFS:**
1. Crea una [classe di archiviazione personalizzata](#nfs_version_class) con la versione NFS di cui desideri eseguire il provisioning.
2. Crea la classe di archiviazione nel tuo cluster.
   ```
   oc apply -f nfsversion_storageclass.yaml
   ```
   {: pre}

3. Verifica che la classe di archiviazione personalizzata sia stata creata.
   ```
   oc get storageclasses
   ```
   {: pre}

4. Esegui il provisioning dell'[archiviazione file](#add_file) con la tua classe di archiviazione personalizzata.

**Per modificare il tuo PV esistente in modo che utilizzi una versione NFS differente:**

1. Ottieni il PV dell'archiviazione file di cui vuoi modificare la versione NFS e prendi nota del nome del PV.
   ```
   oc get pv
   ```
   {: pre}

2. Aggiungi un'annotazione al tuo PV. Sostituisci `<version_number>` con la versione NFS che desideri utilizzare. Ad esempio per modificare la versione NFS con la 3.0, immetti **3**.  
   ```
   oc patch pv <pv_name> -p '{"metadata": {"annotations":{"volume.beta.kubernetes.io/mount-options":"vers=<version_number>"}}}'
   ```
   {: pre}

3. Elimina il pod che utilizza l'archiviazione file e ricrealo.
   1. Salva lo YAML del pod sulla tua macchina locale.
      ```
      kubect get pod <pod_name> -o yaml > <filepath/pod.yaml>
      ```
      {: pre}

   2. Elimina il pod.
      ```
      oc deleted pod <pod_name>
      ```
      {: pre}

   3. Ricrea il pod.
      ```
      oc apply -f pod.yaml
      ```
      {: pre}

4. Attendi che il pod venga distribuito.
   ```
   oc get pods
   ```
   {: pre}

   Il pod è completamente distribuito quando lo stato viene modificato con `In esecuzione`.

5. Accedi al tuo pod.
   ```
   oc exec -it <pod_name> sh
   ```
   {: pre}

6. Verifica che l'archiviazione file sia stata montata con la versione NFS da te specificata precedentemente.
   ```
   mount | grep "nfs" | awk -F" |," '{ print $5, $8 }'
   ```
   {: pre}

   Output di esempio:
   ```
   nfs vers=3.0
   ```
   {: screen}

<br />


## Backup e ripristino di dati
{: #file_backup_restore}

Il provisioning dell'archiviazione file viene eseguito nella stessa ubicazione dei nodi di lavoro nel tuo cluster. L'archiviazione viene ospitata sui server in cluster da IBM per offrire la disponibilità in caso di arresto di un server. Tuttavia, non viene eseguito il backup automatico dell'archiviazione file e potrebbe essere inaccessibile se si verifica un malfunzionamento dell'intera ubicazione. Per evitare che i tuoi dati vengano persi o danneggiati, puoi configurare dei backup periodici che puoi utilizzare per ripristinare i dati quando necessario.
{: shortdesc}

Esamina le seguenti opzioni di backup e ripristino per la tua archiviazione file:

<dl>
  <dt>Configura istantanee periodiche</dt>
  <dd><p>Puoi [configurare delle istantanee periodiche per la tua archiviazione file](/docs/infrastructure/FileStorage?topic=FileStorage-snapshots), che è un'immagine di sola lettura che acquisisce lo stato dell'istanza in un punto nel tempo. Per archiviare l'istantanea, devi richiedere lo spazio per l'istantanea nella tua archiviazione file. Le istantanee vengono archiviate nell'istanza di archiviazione esistente all'interno della stessa zona. Puoi ripristinare i dati da un'istantanea se un utente rimuove accidentalmente dati importanti dal volume.</br> <strong>Per creare un'istantanea per il tuo volume:</strong><ol><li>[Accedi al tuo account. Se applicabile, specifica il gruppo di risorse appropriato. Imposta il contesto per il tuo cluster.](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure)</li><li>Accedi alla CLI `ibmcloud sl`. <pre class="pre"><code>    ibmcloud sl init
    </code></pre></li><li>Elenca i PV esistenti nel tuo cluster. <pre class="pre"><code>oc get pv</code></pre></li><li>Ottieni i dettagli del PV per cui vuoi creare uno spazio per l'istantanea e prendi nota dell'ID volume, della dimensione e dell'IOPS. <pre class="pre"><code>oc describe pv &lt;pv_name&gt;</code></pre> L'ID volume, la dimensione e l'IOPS possono essere trovati nella sezione <strong>Etichette</strong> del tuo output della CLI. </li><li>Crea la dimensione dell'istantanea per il tuo volume esistente con i parametri che hai richiamato nel passo precedente. <pre class="pre"><code>ibmcloud sl file snapshot-order &lt;volume_ID&gt; --size &lt;size&gt; --tier &lt;iops&gt;</code></pre></li><li>Attendi che la dimensione dell'istantanea venga creata. <pre class="pre"><code>ibmcloud sl file volume-detail &lt;volume_ID&gt;</code></pre>La dimensione dell'istantanea viene fornita correttamente quando la <strong>Dimensione istantanea (GB)</strong> nel tuo output della CLI viene modificata da 0 con la dimensione che hai ordinato. </li><li>Crea l'istantanea per il tuo volume e prendi nota dell'ID dell'istantanea che ti viene creata. <pre class="pre"><code>ibmcloud sl file snapshot-create &lt;volume_ID&gt;</code></pre></li><li>Verifica che l'istantanea sia stata creata correttamente. <pre class="pre"><code>ibmcloud sl file snapshot-list &lt;volume_ID&gt;</code></pre></li></ol></br><strong>Per ripristinare i dati da un'istantanea in un volume esistente: </strong><pre class="pre"><code>ibmcloud sl file snapshot-restore &lt;volume_ID&gt; &lt;snapshot_ID&gt;</code></pre></p></dd>
  <dt>Replica le istantanee in un'altra zona</dt>
 <dd><p>Per proteggere i tuoi dati da un malfunzionamento dell'ubicazione, puoi [replicare le istantanee](/docs/infrastructure/FileStorage?topic=FileStorage-replication#replication) in un'istanza di archiviazione file configurata in un'altra zona. I dati possono essere replicati solo dall'archiviazione primaria a quella di backup. Non puoi montare un'istanza di archiviazione file replicata in un cluster. Quando la tua archiviazione primaria non funziona più, puoi impostare manualmente la tua archiviazione di backup replicata in modo che sia quella primaria. Quindi, puoi montarla nel tuo cluster. Una volta ripristinata la tua archiviazione primaria, puoi ripristinare i dati dall'archiviazione di backup.</p></dd>
 <dt>Duplica l'archiviazione</dt>
 <dd><p>Puoi [duplicare la tua istanza di archiviazione file](/docs/infrastructure/FileStorage?topic=FileStorage-duplicatevolume#duplicatevolume) nella stessa zona dell'istanza di archiviazione originale. Un duplicato contiene gli stessi dati dell'istanza di archiviazione originale nel momento in cui è stato creato il duplicato. A differenza delle repliche, puoi utilizzare il duplicato come un'istanza di archiviazione indipendente dall'originale. Per eseguire la duplicazione, per prima cosa [configura le istantanee per il volume](/docs/infrastructure/FileStorage?topic=FileStorage-snapshots).</p></dd>
  <dt>Esegui il backup dei dati in {{site.data.keyword.cos_full}}</dt>
  <dd><p>Puoi utilizzare l'[**immagine ibm-backup-restore**](/docs/services/RegistryImages/ibm-backup-restore?topic=RegistryImages-ibmbackup_restore_starter#ibmbackup_restore_starter) per avviare un pod di backup e ripristino nel tuo cluster. Questo pod contiene uno script per eseguire un backup una tantum o periodico per qualsiasi attestazione del volume persistente (PVC) nel tuo cluster. I dati vengono archiviati nella tua istanza {{site.data.keyword.cos_full}} che hai configurato in una zona.</p>
  <p>Per rendere i tuoi dati ancora più altamente disponibili e proteggere la tua applicazione da un errore di zona, configura una seconda istanza {{site.data.keyword.cos_full}} e replica i dati tra le varie zone. Se devi ripristinare i dati dalla tua istanza {{site.data.keyword.cos_full}}, utilizza lo script di ripristino fornito con l'immagine.</p></dd>
<dt>Copia i dati nei/dai pod e contenitori</dt>
<dd><p>Puoi utilizzare il comando `oc cp` [![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://kubernetes.io/docs/reference/kubectl/overview/#cp) per copiare i file e le directory in/da pod o specifici contenitori nel tuo cluster.</p>
<p>Prima di iniziare: [accedi al tuo account. Se applicabile, specifica il gruppo di risorse appropriato. Imposta il contesto per il tuo cluster.](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure) Se non specifichi un contenitore con <code>-c</code>, il comando utilizza il primo contenitore disponibile nel pod.</p>
<p>Puoi utilizzare il comando in diversi modi:</p>
<ul>
<li>Copia i dati dalla tua macchina locale a un pod nel tuo cluster: <pre class="pre"><code>oc cp <var>&lt;local_filepath&gt;/&lt;filename&gt;</var> <var>&lt;namespace&gt;/&lt;pod&gt;:&lt;pod_filepath&gt;</var></code></pre></li>
<li>Copia i dati da un pod nel tuo cluster alla tua macchina locale: <pre class="pre"><code>oc cp <var>&lt;namespace&gt;/&lt;pod&gt;:&lt;pod_filepath&gt;/&lt;filename&gt;</var> <var>&lt;local_filepath&gt;/&lt;filename&gt;</var></code></pre></li>
<li>Copia i dati dalla tua macchina locale a un contenitore specifico che viene eseguito in un pod nel tuo cluster: <pre class="pre"><code>oc cp <var>&lt;local_filepath&gt;/&lt;filename&gt;</var> <var>&lt;namespace&gt;/&lt;pod&gt;:&lt;pod_filepath&gt;</var> -c <var>&lt;container></var></code></pre></li>
</ul></dd>
  </dl>

<br />


## Riferimento delle classi di archiviazione
{: #file_storageclass_reference}

| Caratteristiche | Impostazione|
|:-----------------|:-----------------|
| Nome | <code>ibmc-file-bronze</code></br><code>ibmc-file-retain-bronze</code>|
| Tipo | [Archiviazione Endurance](/docs/infrastructure/FileStorage?topic=FileStorage-about#provisioning-with-endurance-tiers)|
| File system | NFS|
| IOPS per gigabyte | 2|
| Intervallo di dimensioni in gigabyte | 20-12000 Gi|
| Disco rigido | SSD|
| Fatturazione | Oraria|
| Prezzi | [Informazioni sui prezzi![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://www.ibm.com/cloud/file-storage/pricing)|
{: class="simple-tab-table"}
{: caption="Classe di archiviazione file: bronze" caption-side="top"}
{: #simpletabtable1}
{: tab-title="Bronze"}
{: tab-group="File storage class"}

| Caratteristiche | Impostazione|
|:-----------------|:-----------------|
| Nome | <code>ibmc-file-silver</code></br><code>ibmc-file-retain-silver</code>|
| Tipo | [Archiviazione Endurance](/docs/infrastructure/FileStorage?topic=FileStorage-about#provisioning-with-endurance-tiers)|
| File system | NFS|
| IOPS per gigabyte | 4|
| Intervallo di dimensioni in gigabyte | 20-12000 Gi|
| Disco rigido | SSD|
| Fatturazione | Oraria|
| Prezzi | [Informazioni sui prezzi![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://www.ibm.com/cloud/file-storage/pricing)|
{: class="simple-tab-table"}
{: caption="Classe di archiviazione file: silver" caption-side="top"}
{: #simpletabtable2}
{: tab-title="Silver"}
{: tab-group="File storage class"}

| Caratteristiche | Impostazione|
|:-----------------|:-----------------|
| Nome | <code>ibmc-file-gold</code></br><code>ibmc-file-retain-gold</code>|
| Tipo | [Archiviazione Endurance](/docs/infrastructure/FileStorage?topic=FileStorage-about#provisioning-with-endurance-tiers)|
| File system | NFS|
| IOPS per gigabyte | 10|
| Intervallo di dimensioni in gigabyte | 20-4000 Gi|
| Disco rigido | SSD|
| Fatturazione | Oraria|
| Prezzi | [Informazioni sui prezzi![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://www.ibm.com/cloud/file-storage/pricing)|
{: class="simple-tab-table"}
{: caption="Classe di archiviazione file: gold" caption-side="top"}
{: #simpletabtable3}
{: tab-title="Gold"}
{: tab-group="File storage class"}

| Caratteristiche | Impostazione|
|:-----------------|:-----------------|
| Nome | <code>ibmc-file-custom</code></br><code>ibmc-file-retain-custom</code>|
| Tipo | [Prestazioni](/docs/infrastructure/FileStorage?topic=FileStorage-about#provisioning-with-performance)|
| File system | NFS|
| IOPS e dimensione | <p><strong>Intervallo di dimensioni in gigabyte / intervallo di IOPS in multipli di 100</strong></p><ul><li>20-39 Gi / 100-1000 IOPS</li><li>40-79 Gi / 100-2000 IOPS</li><li>80-99 Gi / 100-4000 IOPS</li><li>100-499 Gi / 100-6000 IOPS</li><li>500-999 Gi / 100-10000 IOPS</li><li>1000-1999 Gi / 100-20000 IOPS</li><li>2000-2999 Gi / 200-40000 IOPS</li><li>3000-3999 Gi / 200-48000 IOPS</li><li>4000-7999 Gi / 300-48000 IOPS</li><li>8000-9999 Gi / 500-48000 IOPS</li><li>10000-12000 Gi / 1000-48000 IOPS</li></ul>|
| Disco rigido | Il rapporto IOPS-gigabyte determina il tipo di disco rigido di cui viene eseguito il provisioning. Per determinare il tuo rapporto IOPS/gigabyte, dividi l'IOPS per la dimensione della tua archiviazione. </br></br>Esempio: </br>hai scelto 500Gi di archiviazione con 100 IOPS. Il tuo rapporto è 0,2 (100 IOPS/500Gi). </br></br><strong>Panoramica dei tipi di disco rigido per rapporto:</strong><ul><li>Inferiore o uguale a 0,3: SATA</li><li>Maggiore di 0,3: SSD</li></ul>|
| Fatturazione | Oraria|
| Prezzi | [Informazioni sui prezzi![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://www.ibm.com/cloud/file-storage/pricing)|
{: class="simple-tab-table"}
{: caption="Classe di archiviazione file: custom" caption-side="top"}
{: #simpletabtable4}
{: tab-title="Custom"}
{: tab-group="File storage class"}

<br />


## Classi di archiviazione personalizzate di esempio
{: #file_custom_storageclass}

Puoi creare una classe di archiviazione personalizzata e utilizzare la classe di archiviazione nella tua PVC.
{: shortdesc}

{{site.data.keyword.containerlong_notm}} fornisce [classi di archiviazione predefinite](#file_storageclass_reference) per eseguire il provisioning dell'archiviazione file con un livello e una configurazione specifici. In alcuni casi, potresti voler eseguire il provisioning dell'archiviazione con una configurazione diversa che non è inclusa nelle classi di archiviazione predefinite. Puoi utilizzare gli esempi in questo argomento per trovare classi di archiviazione personalizzate di esempio.

Per creare la tua classe di archiviazione personalizzata, vedi [Personalizzazione di una classe di archiviazione](/docs/containers?topic=containers-kube_concepts#customized_storageclass). Quindi, [utilizza la classe di archiviazione personalizzata nella tua PVC](#add_file).

### Creazione di un'archiviazione che rileva la topologia
{: #file-topology}

Per utilizzare l'archiviazione file in un cluster multizona, il tuo pod deve essere pianificato nella stessa zona della tua istanza di archiviazione file in modo che tu possa leggere e scrivere sul volume. Prima che la pianificazione dei volumi che rileva la topologia fosse introdotta da Kubernetes, il provisioning dinamico della tua archiviazione creava automaticamente l'istanza di archiviazione file quando veniva creata una PVC. Quindi, quando creavi il tuo pod, il programma di pianificazione Kubernetes provava a distribuire il pod a un nodo di lavoro nello stesso data center della tua istanza di archiviazione file.
{: shortdesc}

La creazione dell'istanza di archiviazione file senza conoscere i vincoli del pod può portare a risultati indesiderati. Ad esempio, potrebbe non essere possibile pianificare il tuo pod sullo stesso nodo di lavoro della tua archiviazione perché il nodo di lavoro ha risorse insufficienti oppure perché il nodo di lavoro è contaminato e non consente la pianificazione del pod. Con la pianificazione dei volumi che rileva la topologia, l'istanza di archiviazione file viene ritardata finché non viene creato il primo pod che utilizza l'archiviazione.

La pianificazione dei volumi che rileva la topologia è supportata solo sui cluster che eseguono Kubernetes versione 1.12 o successive.
{: note}

I seguenti esempi mostrano come creare classi di archiviazione che ritardano la creazione dell'istanza di archiviazione file finché il primo pod che utilizza questa archiviazione non è pronto per essere pianificato. Per ritardare la creazione, devi includere l'opzione `volumeBindingMode: WaitForFirstConsumer`. Se non includi questa opzione, la `volumeBindingMode` viene impostata automaticamente su `Immediate` e l'istanza di archiviazione file viene creata quando crei la PVC.

- **Esempio per l'archiviazione file Endurance:**
  ```
  apiVersion: storage.k8s.io/v1
  kind: StorageClass
  metadata:
    name: ibmc-file-bronze-delayed
  parameters:
    billingType: hourly
    classVersion: "2"
    iopsPerGB: "2"
    sizeRange: '[20-12000]Gi'
    type: Endurance
  provisioner: ibm.io/ibmc-file
  reclaimPolicy: Delete
  volumeBindingMode: WaitForFirstConsumer
  ```
  {: codeblock}

- **Esempio per l'archiviazione file Performance:**
  ```
  apiVersion: storage.k8s.io/v1
  kind: StorageClass
  metadata:
   name: ibmc-file-performance-storageclass
   labels:
     kubernetes.io/cluster-service: "true"
  provisioner: ibm.io/ibmc-file
  parameters:
   billingType: "hourly"
   classVersion: "2"
   sizeIOPSRange: |-
     "[20-39]Gi:[100-1000]"
     "[40-79]Gi:[100-2000]"
     "[80-99]Gi:[100-4000]"
     "[100-499]Gi:[100-6000]"
     "[500-999]Gi:[100-10000]"
     "[1000-1999]Gi:[100-20000]"
     "[2000-2999]Gi:[200-40000]"
     "[3000-3999]Gi:[200-48000]"
     "[4000-7999]Gi:[300-48000]"
     "[8000-9999]Gi:[500-48000]"
     "[10000-12000]Gi:[1000-48000]"
   type: "Performance"
  reclaimPolicy: Delete
  volumeBindingMode: WaitForFirstConsumer
  ```
  {: codeblock}

### Specifica della zona per i cluster a multizona
{: #file_multizone_yaml}

Se vuoi creare la tua archiviazione file in una zona specifica, puoi specificare la zona e la regione in una classe di archiviazione personalizzata.
{: shortdesc}

Utilizza la classe di archiviazione personalizzata se desideri [eseguire il provisioning dell'archiviazione file in modo statico](#existing_file) in una zona specifica. In tutti gli altri casi, [specifica la zona direttamente nella tua PVC](#add_file).
{: note}

Quando crei la classe di archiviazione personalizzata, specifica la stessa regione e la stessa zona dove si trovano il tuo cluster e i tuoi nodi di lavoro. Per ottenere la regione del tuo cluster, esegui `ibmcloud oc cluster-get --cluster <cluster_name_or_ID>` e cerca il prefisso della regione nell'**URL master**, come ad esempio `eu-de` in `https://c2.eu-de.containers.cloud.ibm.com:11111`. Per ottenere la zona del tuo nodo di lavoro, esegui `ibmcloud oc workers --cluster <cluster_name_or_ID>`.

- **Esempio per l'archiviazione file Endurance:**
  ```
  apiVersion: storage.k8s.io/v1
  kind: StorageClass
  metadata:
    name: ibmc-file-silver-mycustom-storageclass
    labels:
      kubernetes.io/cluster-service: "true"
  provisioner: ibm.io/ibmc-file
  parameters:
    zone: "dal12"
    region: "us-south"
    type: "Endurance"
    iopsPerGB: "4"
    sizeRange: "[20-12000]Gi"
    reclaimPolicy: "Delete"
    classVersion: "2"
  reclaimPolicy: Delete
  volumeBindingMode: Immediate
  ```
  {: codeblock}

- **Esempio per l'archiviazione file Performance:**
  ```
  apiVersion: storage.k8s.io/v1
  kind: StorageClass
  metadata:
   name: ibmc-file-performance-storageclass
   labels:
     kubernetes.io/cluster-service: "true"
  provisioner: ibm.io/ibmc-file
  parameters:
   zone: "dal12"
   region: "us-south"
   billingType: "hourly"
   classVersion: "2"
   sizeIOPSRange: |-
     "[20-39]Gi:[100-1000]"
     "[40-79]Gi:[100-2000]"
     "[80-99]Gi:[100-4000]"
     "[100-499]Gi:[100-6000]"
     "[500-999]Gi:[100-10000]"
     "[1000-1999]Gi:[100-20000]"
     "[2000-2999]Gi:[200-40000]"
     "[3000-3999]Gi:[200-48000]"
     "[4000-7999]Gi:[300-48000]"
     "[8000-9999]Gi:[500-48000]"
     "[10000-12000]Gi:[1000-48000]"
   type: "Performance"
  reclaimPolicy: Delete
  volumeBindingMode: Immediate
  ```
  {: codeblock}

### Modifica della versione NFS predefinita
{: #nfs_version_class}

La seguente classe di archiviazione personalizzata ti consente di definire la versione NFS di cui desideri eseguire il provisioning. Ad esempio, per eseguire il provisioning di NFS versione 3.0, sostituisci `<nfs_version>` con **3.0**.
{: shortdesc}

- **Esempio per l'archiviazione file Endurance:**
  ```
  apiVersion: storage.k8s.io/v1
  kind: StorageClass
  metadata:
    name: ibmc-file-mount
    labels:
      kubernetes.io/cluster-service: "true"
  provisioner: ibm.io/ibmc-file
  parameters:
    type: "Endurance"
    iopsPerGB: "2"
    sizeRange: "[1-12000]Gi"
    reclaimPolicy: "Delete"
    classVersion: "2"
    mountOptions: nfsvers=<nfs_version>
  ```
  {: codeblock}

- **Esempio per l'archiviazione file Performance:**
  ```
  apiVersion: storage.k8s.io/v1
  kind: StorageClass
  metadata:
    name: ibmc-file-mount
    labels:
      kubernetes.io/cluster-service: "true"
  provisioner: ibm.io/ibmc-file
  parameters:
   type: "Performance"
   classVersion: "2"
   sizeIOPSRange: |-
     "[20-39]Gi:[100-1000]"
     "[40-79]Gi:[100-2000]"
     "[80-99]Gi:[100-4000]"
     "[100-499]Gi:[100-6000]"
     "[500-999]Gi:[100-10000]"
     "[1000-1999]Gi:[100-20000]"
     "[2000-2999]Gi:[200-40000]"
     "[3000-3999]Gi:[200-48000]"
     "[4000-7999]Gi:[300-48000]"
     "[8000-9999]Gi:[500-48000]"
     "[10000-12000]Gi:[1000-48000]"
   mountOptions: nfsvers=<nfs_version>
  ```
  {: codeblock}



