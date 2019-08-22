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

# Archiviazione dei dati su un classico IBM Cloud Block Storage
{: #block_storage}

{{site.data.keyword.cloud_notm}} Block Storage è un'archiviazione iSCSI ad alte prestazioni e persistente che puoi aggiungere alle tue applicazioni utilizzando i volumi persistenti (PV, persistent volume) Kubernetes. Puoi scegliere tra i livelli di archiviazione predefiniti con dimensioni in GB e IOPS che soddisfano i requisiti dei tuoi carichi di lavoro. Per appurare se {{site.data.keyword.cloud_notm}} Block Storage è l'opzione di archiviazione giusta per te, vedi [Scelta di una soluzione di archiviazione](/docs/containers?topic=containers-storage_planning#choose_storage_solution). Per ulteriori informazioni sui prezzi, vedi [Fatturazione](/docs/infrastructure/BlockStorage?topic=BlockStorage-About#billing).
{: shortdesc}

{{site.data.keyword.cloud_notm}} Block Storage è disponibile solo per i cluster standard. Se il tuo cluster non può accedere alla rete pubblica, ad esempio un cluster privato dietro un firewall o un cluster con solo l'endpoint del servizio privato abilitato, assicurati che hai installato il plugin {{site.data.keyword.cloud_notm}} Block Storage versione 1.3.0 o successive per stabilire una connessione alla tua istanza dell'archiviazione blocchi sulla rete privata. Le istanze di archiviazione blocchi sono specifiche per una singola zona. Se hai un cluster multizona, prendi in considerazione le [opzioni di archiviazione persistente multizona](/docs/containers?topic=containers-storage_planning#persistent_storage_overview).
{: important}

## Installazione del plugin {{site.data.keyword.cloud_notm}} Block Storage nel tuo cluster
{: #install_block}

Installa il plugin {{site.data.keyword.cloud_notm}} Block Storage con un grafico Helm per impostare le classi di archiviazione predefinite per l'archiviazione blocchi. Puoi utilizzare queste classi di archiviazione per creare una PVC per eseguire il provisioning dell'archiviazione blocchi per le tue applicazioni.
{: shortdesc}

Prima di iniziare: [accedi al tuo account. Se applicabile, specifica il gruppo di risorse appropriato. Imposta il contesto per il tuo cluster.](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure)

1. Assicurati che il tuo nodo di lavoro applichi la patch più recente per la tua versione secondaria.
   1. Elenca la versione patch corrente dei tuoi nodi di lavoro.
      ```
      ibmcloud oc workers --cluster <cluster_name_or_ID>
      ```
      {: pre}

      Output di esempio:
      ```
      OK
      ID                                                  Public IP        Private IP     Machine Type           State    Status   Zone    Version
      kube-dal10-crb1a23b456789ac1b20b2nc1e12b345ab-w26   169.xx.xxx.xxx    10.xxx.xx.xxx   b3c.4x16.encrypted     normal   Ready    dal10   1.13.8_1523*
      ```
      {: screen}

      Se il tuo nodo di lavoro non applica la versione patch più recente, viene visualizzato un asterisco (`*`) nella colonna **Versione** del tuo output della CLI.

   2. Esamina il [changelog di versione](/docs/containers?topic=containers-changelog#changelog) per trovare le modifiche incluse nella versione patch più recente.

   3. Applica la versione patch più recente ricaricando il tuo nodo di lavoro. Segui le istruzioni nel [comando ibmcloud oc worker-reload](/docs/containers?topic=containers-cli-plugin-kubernetes-service-cli#cs_worker_reload) per ripianificare correttamente qualsiasi pod in esecuzione sul tuo nodo di lavoro prima di ricaricare il tuo nodo di lavoro. Nota che durante il ricaricamento, la macchina del nodo di lavoro viene aggiornata con l'immagine più recente e i dati vengono eliminati se non sono [archiviati all'esterno del nodo di lavoro](/docs/containers?topic=containers-storage_planning#persistent_storage_overview).

1.  [Attieniti alle istruzioni](/docs/containers?topic=containers-helm#public_helm_install) per installare il client Helm sulla tua macchina locale e installare il server Helm (Tiller) con un account di servizio nel tuo cluster.

    L'installazione del server Helm Tiller richiede la connessione di rete pubblica al Google Container Registry pubblico. Se il tuo cluster non può accedere alla rete pubblica, come ad esempio un cluster privato dietro un firewall o un cluster con solo l'endpoint del servizio privato abilitato, puoi scegliere di [eseguire il pull dell'immagine Tiller sulla tua macchina locale ed eseguire il push dell'immagine nel tuo spazio dei nomi in {{site.data.keyword.registryshort_notm}}](/docs/containers?topic=containers-helm#private_local_tiller) oppure di [installare il grafico Helm senza utilizzare Tiller](/docs/containers?topic=containers-helm#private_install_without_tiller).
    {: note}

2.  Verifica che Tiller sia installato con un account di servizio.

    ```
    oc get serviceaccount -n kube-system tiller
    ```
    {: pre}

    Output di esempio:

    ```
    NAME                                 SECRETS   AGE
    tiller                               1         2m
    ```
    {: screen}

3. Aggiungi il repository di grafici Helm {{site.data.keyword.cloud_notm}} al cluster in cui vuoi utilizzare il plugin {{site.data.keyword.cloud_notm}} Block Storage.
   ```
   helm repo add iks-charts https://icr.io/helm/iks-charts
   ```
   {: pre}

4. Aggiorna il repository Helm per richiamare la versione più recente di tutti i grafici Helm in questo repository.
   ```
   helm repo update
   ```
   {: pre}

5. Installa il plugin {{site.data.keyword.cloud_notm}} Block Storage. Quando installi il plugin, al tuo cluster vengono aggiunte le classi di archiviazione blocchi predefinite.
   ```
   helm install iks-charts/ibmcloud-block-storage-plugin
   ```
   {: pre}

   Output di esempio:
   ```
   NAME:   bald-olm
   LAST DEPLOYED: Wed Apr 18 10:02:55 2018
   NAMESPACE: default
   STATUS: DEPLOYED

   RESOURCES:
   ==> v1beta1/DaemonSet
   NAME                           DESIRED  CURRENT  READY  UP-TO-DATE  AVAILABLE  NODE SELECTOR  AGE
   ibmcloud-block-storage-driver  0        0        0      0           0          <none>         0s

   ==> v1beta1/Deployment
   NAME                           DESIRED  CURRENT  UP-TO-DATE  AVAILABLE  AGE
   ibmcloud-block-storage-plugin  1        0        0           0          0s

   ==> v1/StorageClass
   NAME                      PROVISIONER        AGE
   ibmc-block-bronze         ibm.io/ibmc-block  0s
   ibmc-block-custom         ibm.io/ibmc-block  0s
   ibmc-block-gold           ibm.io/ibmc-block  0s
   ibmc-block-retain-bronze  ibm.io/ibmc-block  0s
   ibmc-block-retain-custom  ibm.io/ibmc-block  0s
   ibmc-block-retain-gold    ibm.io/ibmc-block  0s
   ibmc-block-retain-silver  ibm.io/ibmc-block  0s
   ibmc-block-silver         ibm.io/ibmc-block  0s

   ==> v1/ServiceAccount
   NAME                           SECRETS  AGE
   ibmcloud-block-storage-plugin  1        0s

   ==> v1beta1/ClusterRole
   NAME                           AGE
   ibmcloud-block-storage-plugin  0s

   ==> v1beta1/ClusterRoleBinding
   NAME                           AGE
   ibmcloud-block-storage-plugin  0s

   NOTES:
   Thank you for installing: ibmcloud-block-storage-plugin.   Your release is named: bald-olm
   ```
   {: screen}

6. Verifica che l'installazione sia stata eseguita correttamente.
   ```
   oc get pod -n kube-system | grep block
   ```
   {: pre}

   Output di esempio:
   ```
   ibmcloud-block-storage-driver-kh4mt                              1/1       Running   0          27d       10.118.98.19   10.118.98.19
   ibmcloud-block-storage-plugin-58c5f9dc86-pbl4t                   1/1       Running   0          14d       172.21.0.204   10.118.98.19
   ```
   {: screen}

   L'installazione ha avuto esito positivo quando visualizzi un pod `ibmcloud-block-storage-plugin` e uno o più pod `ibmcloud-block-storage-driver`. Il numero di pod `ibmcloud-block-storage-driver` è uguale al numero di nodi di lavoro nel tuo cluster. Tutti i pod devono essere in uno stato **In esecuzione**.

7. Verifica che le classi di archiviazione per l'archiviazione blocchi siano state aggiunte al tuo cluster.
   ```
   oc get storageclasses | grep block
   ```
   {: pre}

   Output di esempio:
   ```
   ibmc-block-bronze            ibm.io/ibmc-block
   ibmc-block-custom            ibm.io/ibmc-block
   ibmc-block-gold              ibm.io/ibmc-block
   ibmc-block-retain-bronze     ibm.io/ibmc-block
   ibmc-block-retain-custom     ibm.io/ibmc-block
   ibmc-block-retain-gold       ibm.io/ibmc-block
   ibmc-block-retain-silver     ibm.io/ibmc-block
   ibmc-block-silver            ibm.io/ibmc-block
   ```
   {: screen}

8. Ripeti questa procedura per ogni cluster in cui desideri eseguire il provisioning dell'archiviazione blocchi.

Ora puoi continuare a [creare una PVC](#add_block) per eseguire il provisioning dell'archiviazione blocchi per la tua applicazione.


### Aggiornamento del plugin {{site.data.keyword.cloud_notm}} Block Storage
Puoi eseguire l'upgrade del plugin {{site.data.keyword.cloud_notm}} Block Storage esistente alla versione più recente.
{: shortdesc}

Prima di iniziare: [accedi al tuo account. Se applicabile, specifica il gruppo di risorse appropriato. Imposta il contesto per il tuo cluster.](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure)

1. Aggiorna il repository Helm per richiamare la versione più recente di tutti i grafici helm in questo repository.
   ```
   helm repo update
   ```
   {: pre}

2. Facoltativo: scarica il grafico helm più recente sulla tua macchina locale. Estrai quindi il pacchetto ed esamina il file `release.md` per trovare le informazioni di release più aggiornate.
   ```
   helm fetch iks-charts/ibmcloud-block-storage-plugin
   ```
   {: pre}

3. Trova il nome del grafico Helm dell'archiviazione blocchi che hai installato nel tuo cluster.
   ```
   helm ls | grep ibmcloud-block-storage-plugin
   ```
   {: pre}

   Output di esempio:
   ```
   myhelmchart 	1       	Mon Sep 18 15:31:40 2017	DEPLOYED	ibmcloud-block-storage-plugin-0.1.0	default
   ```
   {: screen}

4. Aggiorna il plugin {{site.data.keyword.cloud_notm}} Block Storage alla versione più recente.
   ```
   helm upgrade --force --recreate-pods <helm_chart_name>  iks-charts/ibmcloud-block-storage-plugin
   ```
   {: pre}

5. Facoltativo; quando aggiorni il plugin, la classe di archiviazione `default` non è impostata. Se vuoi impostare la classe di archiviazione predefinita su una classe di archiviazione di tua scelta, esegui questo comando.
   ```
   oc patch storageclass <storageclass> -p '{"metadata": {"annotations":{"storageclass.kubernetes.io/is-default-class":"true"}}}'
   ```
   {: pre}


### Rimozione del plugin {{site.data.keyword.cloud_notm}} Block Storage
Se non vuoi eseguire il provisioning di {{site.data.keyword.cloud_notm}} Block Storage e farne uso nel tuo cluster, puoi disinstallare il grafico Helm.
{: shortdesc}

La rimozione del plugin non rimuove PVC, PV o dati esistenti. Quando rimuovi il plugin, tutti i pod e le serie di daemon correlati vengono rimossi dal tuo cluster. Non puoi eseguire il provisioning di una nuova archiviazione blocchi per il tuo cluster o utilizzare i PV e le PVC dell'archiviazione blocchi esistente una volta rimosso il plugin.
{: important}

Prima di iniziare:
- [Accedi al tuo account. Se applicabile, specifica il gruppo di risorse appropriato. Imposta il contesto per il tuo cluster.](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure)
- Assicurati di non avere PVC o PV nel tuo cluster che utilizzano l'archiviazione blocchi.

Per rimuovere il plugin:

1. Trova il nome del grafico Helm dell'archiviazione blocchi che hai installato nel tuo cluster.
   ```
   helm ls | grep ibmcloud-block-storage-plugin
   ```
   {: pre}

   Output di esempio:
   ```
   myhelmchart 	1       	Mon Sep 18 15:31:40 2017	DEPLOYED	ibmcloud-block-storage-plugin-0.1.0	default
   ```
   {: screen}

2. Elimina il plugin {{site.data.keyword.cloud_notm}} Block Storage.
   ```
   helm delete <helm_chart_name>
   ```
   {: pre}

3. Verifica che i pod dell'archiviazione blocchi siano stati rimossi.
   ```
   oc get pod -n kube-system | grep ibmcloud-block-storage-plugin
   ```
   {: pre}
   La rimozione dei pod è riuscita se nel tuo output CLI non vengono visualizzati pod.

4. Verifica che le classi di archiviazione blocchi vengano rimosse.
   ```
   oc get storageclasses | grep block
   ```
   {: pre}
   La rimozione delle classi di archiviazione è riuscita se nel tuo output CLI non vengono visualizzate classi di archiviazione.

<br />



## Decisioni relative alla configurazione dell'archiviazione blocchi
{: #block_predefined_storageclass}

{{site.data.keyword.containerlong}} fornisce delle classi di archiviazione predefinite per l'archiviazione blocchi che puoi utilizzare per eseguire il provisioning di archiviazione blocchi con una specifica configurazione.
{: shortdesc}

Ogni classe di archiviazione specifica il tipo di archiviazione blocchi di cui esegui il provisioning, compresi la dimensione disponibile, il file system IOPS e la politica di conservazione.  

Assicurati di scegliere attentamente la tua configurazione di archiviazione per disporre di sufficiente capacità per archiviare i tuoi dati. Dopo che hai eseguito il provisioning di uno specifico tipo di archiviazione utilizzando una classe di archiviazione, non puoi modificare la dimensione, il tipo, l'IOPS e la politica di conservazione per il dispositivo di archiviazione. Se hai bisogno di più archiviazione oppure di un'archiviazione con una configurazione differente, devi [creare una nuova istanza di archiviazione e copiare i dati](/docs/containers?topic=containers-kube_concepts#update_storageclass) dalla vecchia istanza di archiviazione a quella nuova.
{: important}

1. Elenca le classi di archiviazione disponibili in {{site.data.keyword.containerlong}}.
    ```
    oc get storageclasses | grep block
    ```
    {: pre}

    Output di esempio:
    ```
    $ oc get storageclasses
    NAME                         TYPE
    ibmc-block-custom            ibm.io/ibmc-block
    ibmc-block-bronze            ibm.io/ibmc-block
    ibmc-block-gold              ibm.io/ibmc-block
    ibmc-block-silver            ibm.io/ibmc-block
    ibmc-block-retain-bronze     ibm.io/ibmc-block
    ibmc-block-retain-silver     ibm.io/ibmc-block
    ibmc-block-retain-gold       ibm.io/ibmc-block
    ibmc-block-retain-custom     ibm.io/ibmc-block
    ```
    {: screen}

2. Esamina la configurazione di una classe di archiviazione.
   ```
   oc describe storageclass <storageclass_name>
   ```
   {: pre}

   Per ulteriori informazioni su ciascuna classe di archiviazione, vedi la sezione di [riferimento delle classi di archiviazione](#block_storageclass_reference). Se non trovi quello che stai cercando, considera la possibilità di creare una tua classe di archiviazione personalizzata. Per iniziare, controlla gli [esempi di classe di archiviazione personalizzata](#block_custom_storageclass).
   {: tip}

3. Scegli il tipo di archiviazione blocchi di cui desideri eseguire il provisioning.
   - **Classi di archiviazione bronze, silver e gold:** queste classi di archiviazione eseguono il provisioning di [archiviazione Endurance](/docs/infrastructure/BlockStorage?topic=BlockStorage-About#provendurance). Con l'archiviazione Endurance, puoi scegliere la dimensione dell'archiviazione in gigabyte a livelli IOPS predefiniti.
   - **Classe di archiviazione personalizzata:** questa classe di archiviazione esegue il provisioning di [archiviazione Performance](/docs/infrastructure/BlockStorage?topic=BlockStorage-About#provperformance). Con l'archiviazione Performance, hai più controllo sulla dimensione dell'archiviazione e sull'IOPS.

4. Scegli la dimensione e l'IOPS per la tua archiviazione blocchi. La dimensione e il numero di IOPS definiscono il numero totale di IOPS (operazioni di input/ output al secondo) che funge da indicatore della rapidità della tua archiviazione. Più IOPS totale ha la tua archiviazione e più rapidamente elabora le operazioni di lettura e scrittura.
   - **Classi di archiviazione bronze, silver e gold:** queste classi di archiviazione vengono fornite con un numero fisso di IOPS per gigabyte e ne viene eseguito il provisioning su dischi rigidi SSD. Il numero totale di IOPS dipende dalla dimensione dell'archiviazione che scegli. Puoi selezionare qualsiasi numero intero di gigabyte all'interno dell'intervallo di dimensioni consentite, come ad esempio 20 Gi, 256 Gi o 11854 Gi. Per determinare il numero totale di IOPS, devi moltiplicare l'IOPS con la dimensione selezionata. Ad esempio, se selezioni una dimensione di archiviazione blocchi di 1000Gi nella classe di archiviazione silver che viene fornita con 4 IOPS per GB, la tua archiviazione ha un totale di 4000 IOPS  
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
   - **Classe di archiviazione personalizzata:** quando scegli questa classe di archiviazione, hai più controllo sulla dimensione e sull'IOPS che desideri. Per la dimensione, puoi selezionare qualsiasi numero intero di gigabyte all'interno dell'intervallo di dimensioni consentito. La dimensione da te scelta determina l'intervallo IOPS a tua disposizione. Puoi scegliere un IOPS che è un multiplo di 100 che è compreso nell'intervallo specificato. L'IOPS che scegli è statico e non ridimensiona l'archiviazione. Ad esempio, se scegli 40Gi con 100 IOPS, l'IOPS totale rimane 100. </br></br>Anche il rapporto IOPS-gigabyte determina il tipo di disco rigido di cui viene eseguito il provisioning per tuo conto. Ad esempio, se hai 500Gi a 100 IOPS, il tuo rapporto IOPS-gigabyte è 0,2. Il provisioning dell'archiviazione con un rapporto inferiore o uguale a 0,3 viene eseguito sui dischi rigidi SATA. Se il tuo rapporto è superiore a 0,3, il provisioning della tua archiviazione viene eseguito su dischi rigidi SSD.
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
   - Se vuoi conservare i tuoi dati, scegli una classe di archiviazione `retain`. Quando elimini la PVC, viene eliminata solo la PVC. Il PV, il dispositivo di archiviazione fisico nel tuo account dell'infrastruttura IBM Cloud e i tuoi dati permangono. Per reclamare l'archiviazione e utilizzarla nuovamente nel tuo cluster, devi rimuovere il PV e attenerti alla procedura per l'[utilizzo dell'archiviazione blocchi esistente](#existing_block).
   - Se vuoi che il PV, i dati e il tuo dispositivo di archiviazione blocchi fisico vengano eliminati quando elimini la PVC, scegli una classe di archiviazione senza `retain`.

6. Scegli se preferisci una fatturazione oraria o mensile. Per ulteriori informazioni, controlla la sezione relativa ai [prezzi ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://www.ibm.com/cloud/block-storage/pricing). Per impostazione predefinita, il provisioning di tutti i dispositivi di archiviazione blocchi viene eseguito con un tipo di fatturazione oraria.

<br />



## Aggiunta di archiviazione blocchi alle applicazioni
{: #add_block}

Crea un'attestazione del volume persistente (o PVC, persistent volume claim) per [eseguire dinamicamente il provisioning](/docs/containers?topic=containers-kube_concepts#dynamic_provisioning) di archiviazione blocchi per il tuo cluster. Il provisioning dinamico crea automaticamente il volume persistente (o PV, persistent volume) corrispondente e ordina il dispositivo di archiviazione effettivo nel tuo account dell'infrastruttura IBM Cloud.
{:shortdesc}

L'archiviazione blocchi viene fornita con una modalità di accesso `ReadWriteOnce`. Puoi montarla su un solo pod in un nodo di lavoro nel cluster alla volta.
{: note}

Prima di iniziare:
- Se hai un firewall, [consenti l'accesso in uscita](/docs/containers?topic=containers-firewall#pvc) per gli intervalli IP dell'infrastruttura IBM Cloud delle zone in cui si trovano i tuoi cluster, in modo da poter creare le PVC.
- Installa il plug-in di archiviazione blocchi [{{site.data.keyword.cloud_notm}}](#install_block).
- [Decidi in merito alla classe di archiviazione predefinita](#block_predefined_storageclass) oppure crea una [classe di archiviazione personalizzata](#block_custom_storageclass).

Intendi esporre l'archiviazione blocchi in una serie con stato? Per ulteriori informazioni, vedi [Utilizzo dell'archiviazione blocchi in una serie con stato](#block_statefulset).
{: tip}

Per aggiungere l'archiviazione blocchi:

1.  Crea un file di configurazione per definire la tua attestazione del volume persistente (o PVC, persistent volume claim) e salva la configurazione come un file `.yaml`.

    -  **Esempio per le classi di archiviazione bronze, silver, gold**:
       Il seguente file `.yaml` crea un'attestazione denominata `mypvc` della classe di archiviazione `"ibmc-block-silver"`, con fatturazione oraria (`"hourly"`) e una dimensione in gigabyte di `24Gi`.

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
           - ReadWriteOnce
         resources:
           requests:
             storage: 24Gi
	     storageClassName: ibmc-block-silver
       ```
       {: codeblock}

    -  **Esempio per l'utilizzo della classe di archiviazione personalizzata**:
       il seguente file `.yaml` crea un'attestazione denominata `mypvc` della classe di archiviazione `ibmc-block-retain-custom`, fatturata su base oraria (`"hourly"`), con una dimensione in gigabyte di `45Gi` e un IOPS di `"300"`.

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
           - ReadWriteOnce
         resources:
           requests:
             storage: 45Gi
             iops: "300"
	     storageClassName: ibmc-block-retain-custom
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
         <td>Specifica la frequenza per la quale viene calcolata la fattura di archiviazione, "mensile" o "oraria". Il valore predefinito è "hourly".</td>
       </tr>
       <tr>
       <td><code>metadata.labels.region</code></td>
       <td>Specifica la regione in cui desideri eseguire il provisioning dell'archiviazione blocchi. Se specifichi la regione, devi specificare anche una zona. Se non specifichi una regione, o se la regione specificata non viene trovata, l'archiviazione viene creata nella stessa regione del tuo cluster. <p class="note">Questa opzione è supportata solo con il plugin IBM Cloud Block Storage versione 1.0.1 o superiore. Per le versioni del plugin meno recenti, se hai un cluster multizona, la zona in cui viene eseguito il provisioning della tua archiviazione è selezionata su una base round-robin per bilanciare equamente le richieste di volume tra tutte le zone. Per specificare la zona per la tua archiviazione, puoi creare prima una [classe di archiviazione personalizzata](#block_multizone_yaml). Crea quindi una PVC on la tua classe di archiviazione personalizzata.</p></td>
       </tr>
       <tr>
       <td><code>metadata.labels.zone</code></td>
	<td>Specifica la zona in cui desideri eseguire il provisioning dell'archiviazione blocchi. Se specifichi la zona, devi specificare anche una regione. Se non specifichi una zona o se la zona specificata non viene trovata in un cluster multizona, la zona viene selezionata su una base round-robin. <p class="note">Questa opzione è supportata solo con il plugin IBM Cloud Block Storage versione 1.0.1 o superiore. Per le versioni del plugin meno recenti, se hai un cluster multizona, la zona in cui viene eseguito il provisioning della tua archiviazione è selezionata su una base round-robin per bilanciare equamente le richieste di volume tra tutte le zone. Per specificare la zona per la tua archiviazione, puoi creare prima una [classe di archiviazione personalizzata](#block_multizone_yaml). Crea quindi una PVC on la tua classe di archiviazione personalizzata.</p></td>
	</tr>
        <tr>
        <td><code>spec.resources.requests.storage</code></td>
        <td>Immetti la dimensione dell'archiviazione blocchi, in gigabyte (Gi). Una volta eseguito il provisioning dell'archiviazione, non puoi modificare la dimensione della tua archiviazione blocchi. Assicurati di specificare una dimensione che corrisponda alla quantità di dati che desideri memorizzare. </td>
        </tr>
        <tr>
        <td><code>spec.resources.requests.iops</code></td>
        <td>Questa opzione è disponibile solo per le classi di archiviazione personalizzate (`ibmc-block-custom / ibmc-block-retain-custom`). Specifica l'IOPS totale per l'archiviazione, selezionando un multiplo di 100 nell'intervallo consentito. Se scegli un IOPS diverso da quello elencato, viene arrotondato per eccesso.</td>
        </tr>
	<tr>
	<td><code>spec.storageClassName</code></td>
	<td>Il nome della classe di archiviazione che vuoi utilizzare per eseguire il provisioning dell'archiviazione blocchi. Puoi scegliere di utilizzare una delle [classi di archiviazione fornite da IBM](#block_storageclass_reference) o [creare una tua classe di archiviazione](#block_custom_storageclass). </br> Se non specifichi una classe di archiviazione, il PV viene creato con la classe di archiviazione predefinita <code>ibmc-file-bronze</code><p>**Suggerimento:** se vuoi modificare la classe di archiviazione predefinita, esegui <code>oc patch storageclass &lt;storageclass&gt; -p '{"metadata": {"annotations":{"storageclass.kubernetes.io/is-default-class":"true"}}}'</code> e sostituisci <code>&lt;storageclass&gt;</code> con il nome della classe di archiviazione.</p></td>
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
    Access Modes:	RWO
    Events:
      FirstSeen	LastSeen	Count	From								SubObjectPath	Type		Reason			Message
      ---------	--------	-----	----								-------------	--------	------			-------
      3m 3m 1 {ibm.io/ibmc-block 31898035-3011-11e7-a6a4-7a08779efd33 } Normal Provisioning External provisioner is provisioning volume  for claim "default/my-persistent-volume-claim"
       3m 1m	 10 {persistentvolume-controller } Normal ExternalProvisioning cannot find provisioner "ibm.io/ibmc-block", expecting that  a volume for the claim is provisioned either manually or via external software
       1m 1m 1 {ibm.io/ibmc-block 31898035-3011-11e7-a6a4-7a08779efd33 } Normal ProvisioningSucceeded	Successfully provisioned volume  pvc-0d787071-3a67-11e7-aafc-eef80dd2dea2

    ```
    {: screen}

4.  {: #block_app_volume_mount}Per montare il PV nella tua distribuzione, crea un file `.yaml` di configurazione e specifica la PVC che esegue il bind del PV.

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
    <td>Il percorso assoluto della directory in cui viene montato il volume nel contenitore. I dati scritti nel percorso di montaggio vengono memorizzati nella directory root nella tua istanza di archiviazione blocchi fisica. Se vuoi condividere un volume tra diverse applicazioni, puoi specificare i [percorsi secondari di volume ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://kubernetes.io/docs/concepts/storage/volumes/#using-subpath) per ciascuna delle tue applicazioni. </td>
    </tr>
    <tr>
    <td><code>spec.containers.volumeMounts.name</code></td>
    <td>Il nome del volume per montare il tuo pod.</td>
    </tr>
    <tr>
    <td><code>volumes.name</code></td>
    <td>Il nome del volume per montare il tuo pod. Normalmente questo nome è lo stesso di <code>volumeMounts/name</code>.</td>
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




## Utilizzo dell'archiviazione blocchi esistente nel tuo cluster
{: #existing_block}

Se hai un dispositivo di archiviazione fisico esistente che vuoi usare nel tuo cluster, puoi creare manualmente il PV e la PVC per [eseguire in modo statico il provisioning](/docs/containers?topic=containers-kube_concepts#static_provisioning) dell'archiviazione.
{: shortdesc}

Prima di iniziare a montare la tua archiviazione esistente in un'applicazione, devi richiamare tutte le informazioni necessarie per il tuo PV.  

### Passo 1: Richiamo delle informazioni della tua archiviazione blocchi esistente
{: #existing-block-1}

1.  Recupera o genera una chiave API per il tuo account dell'infrastruttura IBM Cloud.
    1. Accedi al [portale dell'infrastruttura IBM Cloud ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://cloud.ibm.com/classic?).
    2. Seleziona **Account**, quindi **Utenti** e quindi **Elenco utenti**.
    3. Trova il tuo ID utente.
    4. Nella colonna **Chiave API**, fai clic su **Genera** per generare una chiave API oppure su **Visualizza** per visualizzare la tua chiave API esistente.
2.  Recupera il nome utente API per il tuo account dell'infrastruttura IBM Cloud.
    1. Dal menu **Elenco utenti**, seleziona il tuo ID utente.
    2. Nella sezione **Informazioni di accesso API**, trova il tuo **Nome utente API**.
3.  Accedi al plugin della CLI dell'infrastruttura IBM Cloud.
    ```
    ibmcloud sl init
    ```
    {: pre}

4.  Scegli di eseguire l'autenticazione utilizzando il nome utente e la chiave API per il tuo account dell'infrastruttura IBM Cloud.
5.  Immetti il nome utente e la chiave API che hai recuperato nei passi precedenti.
6.  Elenca i dispositivi di archiviazione blocchi disponibili.
    ```
    ibmcloud sl block volume-list
    ```
    {: pre}

    Output di esempio:
    ```
    id         username            datacenter   storage_type              capacity_gb   bytes_used   ip_addr         lunId   active_transactions
    38642141   IBM02SEL1543159-1   dal10        endurance_block_storage   20            -            169.xx.xxx.xxx   170     0
    ```
    {: screen}

7.  Prendi nota di `id`, `ip_addr`, `capacity_gb`, `datacenter` e `lunId` del dispositivo di archiviazione blocchi che vuoi montare nel tuo cluster. **Nota:** per montare l'archiviazione esistente in un cluster, devi disporre di un nodo di lavoro nella stessa zona della tua archiviazione. Per verificare la zona del tuo nodo di lavoro, esegui `ibmcloud oc workers --cluster <cluster_name_or_ID>`.

### Passo 2: Creazione di un volume persistente (o PV, persistent volume) e di un'attestazione del volume persistente (o PVC, persistent volume claim) corrispondente
{: #existing-block-2}

1.  Facoltativo: se hai dell'archiviazione di cui hai eseguito il provisioning con una classe di archiviazione `retain`, quando rimuovi la PVC, il PV e il dispositivo di archiviazione fisico non vengono rimossi. Per riutilizzare l'archiviazione nel tuo cluster, devi prima rimuovere il PV.
    1. Elenca i PV esistenti.
       ```
       oc get pv
       ```
       {: pre}

       Cerca il PV che appartiene alla tua archiviazione persistente. Il PV è in uno stato `released`.

    2. Rimuovi il PV.
       ```
       oc delete pv <pv_name>
       ```
       {: pre}

    3. Verifica che il PV venga rimosso.
       ```
       oc get pv
       ```
       {: pre}

2.  Crea un file di configurazione per il tuo PV. Includi `id`, `ip_addr`, `capacity_gb`, `datacenter` e `lunIdID` dell'archiviazione blocchi che hai richiamato in precedenza.

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
        storage: "<storage_size>"
      accessModes:
        - ReadWriteOnce
      flexVolume:
        driver: "ibm/ibmc-block"
        fsType: "<fs_type>"
        options:
          "Lun": "<lun_ID>"
          "TargetPortal": "<IP_address>"
          "VolumeID": "<volume_ID>"
          "volumeName": "<volume_name>"
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
    <td>Immetti il nome del PV che desideri creare.</td>
    </tr>
    <tr>
    <td><code>metadata.labels</code></td>
    <td>Immetti la regione e la zona che hai richiamato in precedenza. Devi disporre di almeno un nodo di lavoro nella stessa regione e nella stessa zona della tua archiviazione persistente per montare l'archiviazione nel tuo cluster. Se un PV per la tua archiviazione già esiste, [aggiungi l'etichetta di zona e regione](/docs/containers?topic=containers-kube_concepts#storage_multizone) al tuo PV.
    </tr>
    <tr>
    <td><code>spec.flexVolume.fsType</code></td>
    <td>Immetti il tipo di file system configurato per la tua archiviazione blocchi esistente. Scegli tra <code>ext4</code> o <code>xfs</code>. Se non specifichi questa opzione, viene utilizzato il valore predefinito del PV <code>ext4</code>. Quando viene definito il `fsType` non corretto, la creazione del PV ha esito positivo ma il montaggio del PV in un pod ha esito negativo. </td></tr>	    
    <tr>
    <td><code>spec.capacity.storage</code></td>
    <td>Immetti la dimensione di archiviazione dell'archiviazione blocchi esistente che hai recuperato nel passo precedente come <code>capacity-gb</code>. La dimensione di archiviazione deve essere scritta in gigabyte, ad esempio, 20Gi (20 GB) o 1000Gi (1 TB).</td>
    </tr>
    <tr>
    <td><code>flexVolume.options.Lun</code></td>
    <td>Immetti l'ID lun per la tua archiviazione blocchi che hai richiamato precedentemente come <code>lunId</code>.</td>
    </tr>
    <tr>
    <td><code>flexVolume.options.TargetPortal</code></td>
    <td>Immetti l'indirizzo IP dell'archiviazione blocchi che hai richiamato in precedenza come <code>ip_addr</code>. </td>
    </tr>
    <tr>
	    <td><code>flexVolume.options.VolumeId</code></td>
	    <td>Immetti l'ID della tua archiviazione blocchi che hai richiamato in precedenza come <code>id</code>.</td>
	    </tr>
	    <tr>
		    <td><code>flexVolume.options.volumeName</code></td>
		    <td>Immetti un nome per il tuo volume.</td>
	    </tr>
    </tbody></table>

3.  Crea il PV nel tuo cluster.
    ```
    oc apply -f mypv.yaml
    ```
    {: pre}

4. Verifica che il PV sia stato creato.
    ```
    oc get pv
    ```
    {: pre}

5. Crea un altro file di configurazione per creare la tua PVC. Affinché la PVC corrisponda all'oggetto del PV creato in precedenza, devi scegliere lo stesso valore per `storage` e `accessMode`. Il campo `storage-class` deve essere vuoto. Se uno di questi campi non corrisponde al PV, verrà creato automaticamente un nuovo PV.

     ```
     kind: PersistentVolumeClaim
     apiVersion: v1
     metadata:
      name: mypvc
     spec:
      accessModes:
        - ReadWriteOnce
      resources:
        requests:
          storage: "<storage_size>"
      storageClassName:
     ```
     {: codeblock}

6.  Crea la tua PVC.
     ```
     oc apply -f mypvc.yaml
     ```
     {: pre}

7.  Verifica che la tua PVC sia stata creata e collegata al PV che hai creato in precedenza. Questo processo può richiedere qualche minuto.
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
     Access Modes: RWO
     Events:
       FirstSeen LastSeen Count From        SubObjectPath Type Reason Message
       --------- -------- ----- ----        ------------- -------- ------ -------
       3m 3m 1 {ibm.io/ibmc-block 31898035-3011-11e7-a6a4-7a08779efd33 } Normal Provisioning External provisioner is provisioning volume  for claim "default/my-persistent-volume-claim"
       3m 1m	 10 {persistentvolume-controller } Normal ExternalProvisioning cannot find provisioner "ibm.io/ibmc-block", expecting that  a volume for the claim is provisioned either manually or via external software
       1m 1m 1 {ibm.io/ibmc-block 31898035-3011-11e7-a6a4-7a08779efd33 } Normal ProvisioningSucceeded	Successfully provisioned volume  pvc-0d787071-3a67-11e7-aafc-eef80dd2dea2
     ```
     {: screen}

Hai creato correttamente un PV e lo hai collegato ad una PVC. Gli utenti del cluster possono ora [montare la PVC](#block_app_volume_mount) nelle proprie distribuzioni e iniziare a leggere e a scrivere nel PV.

<br />



## Utilizzo dell'archiviazione blocchi in una serie con stato
{: #block_statefulset}

Se hai un'applicazione con stato, come ad esempio un database, puoi creare delle serie con stato che utilizzano l'archiviazione blocchi per memorizzare i dati della tua applicazione. In alternativa, puoi utilizzare un DBaaS (database-as-a-service) {{site.data.keyword.cloud_notm}} e memorizzare i tuoi dati sul cloud.
{: shortdesc}

**Cosa devo sapere quando aggiungo l'archiviazione blocchi a una serie con stato?** </br>
Per aggiungere l'archiviazione a una serie con stato, devi specificare la tua configurazione di archiviazione nella sezione `volumeClaimTemplates` del file YAML della serie con stato. La sezione `volumeClaimTemplates` è la base per la tua PVC e può includere la classe di archiviazione e la dimensione o l'IOPS della tua archiviazione blocchi di cui desideri eseguire il provisioning. Tuttavia, se vuoi includere etichette in `volumeClaimTemplates`, Kubernetes non le include durante la creazione della PVC. Devi invece aggiungere le etichette direttamente alla tua serie con stato.

Non puoi distribuire due serie con stato contemporaneamente. Se tenti di creare una serie con stato prima ne venga completamente distribuita un'altra, la distribuzione della tua serie con stato potrebbe portare a risultati imprevisti.
{: important}

**Come posso creare la mia serie con stato in una zona specifica?** </br>
In un cluster multizona, puoi specificare la zona e la regione in cui vuoi creare la serie con stato nella sezione `spec.selector.matchLabels` e `spec.template.metadata.labels` del file YAML della serie con stato. In alternativa, puoi aggiungere queste etichette a una [classe di archiviazione personalizzata](/docs/containers?topic=containers-kube_concepts#customized_storageclass) e utilizzare questa classe di archiviazione nella sezione `volumeClaimTemplates` della tua serie con stato.

**Posso ritardare l'associazione di un PV al mio pod con stato finché il pod non è pronto?**<br>
Sì, puoi [creare una classe di archiviazione personalizzata](#topology_yaml) per la tua PVC che include il campo [`volumeBindingMode: WaitForFirstConsumer` ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://kubernetes.io/docs/concepts/storage/storage-classes/#volume-binding-mode).

**Quali opzioni ho per aggiungere l'archiviazione blocchi a una serie con stato?** </br>
Se vuoi creare automaticamente la tua PVC quando crei la serie con stato, utilizza il [provisioning dinamico](#block_dynamic_statefulset). Puoi anche scegliere di eseguire il [pre-provisioning delle PVC o utilizzare PVC esistenti](#block_static_statefulset) con la tua serie con stato.  

### Provisioning dinamico: creazione della PVC quando crei una serie con stato
{: #block_dynamic_statefulset}

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

     Il seguente esempio mostra come distribuire NGINX come una serie con stato con tre repliche. Per ogni replica, viene eseguito il provisioning di un dispositivo di archiviazione blocchi di 20 gigabyte basato sulle specifiche che sono definite nella classe di archiviazione `ibmc-block-retain-bronze`. Il provisioning di tutti i dispositivi di archiviazione viene eseguito nella zona `dal10`. Poiché non è possibile accedere all'archiviazione blocchi da altre zone, tutte le repliche della serie con stato sono distribuite anche sui nodi di lavoro che si trovano in `dal10`.

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
	      storageClassName: ibmc-block-retain-bronze
     ```
     {: codeblock}

   - **Serie con stato di esempio con regola di anti-affinità e creazione di archiviazione blocchi ritardata.**

     Il seguente esempio mostra come distribuire NGINX come una serie con stato con tre repliche. La serie con stato non specifica la regione e la zona dove viene creata l'archiviazione blocchi. La serie con stato utilizza invece una regola anti-affinità per garantire che i pod vengano distribuiti tra i nodi di lavoro e le zone. Definendo `topologykey: failure-domain.beta.kubernetes.io/zone`, il programma di pianificazione Kubernetes non può pianificare un pod su un nodo di lavoro se il nodo di lavoro si trova nella stessa zona di un pod che ha l'etichetta `app: nginx`. Per ogni pod di serie con stato, vengono create due PVC, come definito nella sezione `volumeClaimTemplates`, ma la creazione delle istanze di archiviazione blocchi viene ritardata finché non viene pianificato un pod di serie con stato che utilizza l'archiviazione. Questa configurazione viene indicata come [pianificazione dei volumi che rileva la topologia](https://kubernetes.io/blog/2018/10/11/topology-aware-volume-provisioning-in-kubernetes/).

     ```
     apiVersion: storage.k8s.io/v1
     kind: StorageClass
     metadata:
       name: ibmc-block-bronze-delayed
     parameters:
       billingType: hourly
       classVersion: "2"
       fsType: ext4
       iopsPerGB: "2"
       sizeRange: '[20-12000]Gi'
       type: Endurance
     provisioner: ibm.io/ibmc-block
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
           - ReadWriteOnce # access mode
           resources:
             requests:
               storage: 20Gi
	       storageClassName: ibmc-block-bronze-delayed
       - metadata:
           name: myvol2
         spec:
           accessModes:
           - ReadWriteOnce # access mode
           resources:
             requests:
               storage: 20Gi
	       storageClassName: ibmc-block-bronze-delayed
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
     <td style="text-align:left">Immetti la politica di gestione pod che vuoi utilizzare per la tua serie con stato. Scegli tra le seguenti opzioni: <ul><li><strong>`OrderedReady`: </strong>con questa opzione, le repliche della serie con stato vengono distribuite una dopo l'altra. Ad esempio, se hai distribuito tre repliche, Kubernetes crea la PVC per la prima replica, attende che la PVC venga collegata, distribuisce la replica della serie con stato e monta la PVC sulla replica. Al termine della distribuzione, viene distribuita la seconda replica. Per ulteriori informazioni su questa opzione, vedi [`Gestione pod OrderedReady` ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://kubernetes.io/docs/concepts/workloads/controllers/statefulset/#orderedready-pod-management). </li><li><strong>Parallel: </strong>con questa opzione, la distribuzione di tutte le repliche della serie con stato viene avviata contemporaneamente. Se la tua applicazione supporta la distribuzione parallela di repliche, utilizza questa opzione per risparmiare tempo di distribuzione per le tue PVC e repliche della serie con stato. </li></ul></td>
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
     <td style="text-align:left">Immetti la dimensione dell'archiviazione blocchi in gigabyte (Gi).</td>
     </tr>
     <tr>
     <td style="text-align:left"><code>spec.volumeClaimTemplates.spec.resources.</code></br><code>requests.iops</code></td>
     <td style="text-align:left">Se vuoi eseguire il provisioning dell'[archiviazione Performance](#block_predefined_storageclass), immetti il numero di IOPS. Se utilizzi una classe di archiviazione Endurance e specifichi un numero di IOPS, il numero di IOPS viene ignorato. Invece, viene utilizzato l'IOPS specificato nella tua classe di archiviazione.  </td>
     </tr>
     <tr>
     <td style="text-align:left"><code>spec.volumeClaimTemplates.</code></br><code>spec.storageClassName</code></td>
     <td style="text-align:left">Immetti la classe di archiviazione che vuoi utilizzare. Per elencare le classi di archiviazione esistenti, esegui <code>oc get storageclasses | grep block</code>. Se non specifichi alcuna classe di archiviazione, la PVC viene creata con la classe di archiviazione predefinita impostata nel tuo cluster. Assicurati che la classe di archiviazione predefinita utilizzi il provisioner <code>ibm.io/ibmc-block</code> in modo che la tua serie con stato venga fornita con l'archiviazione blocchi.</td>
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

### Provisioning statico: utilizzo di PVC esistenti con una serie con stato
{: #block_static_statefulset}

Puoi eseguire il pre-provisioning delle tue PVC prima di creare la serie con stato oppure utilizzare PVC esistenti con la tua serie con stato.
{: shortdesc}

Quando [esegui dinamicamente il provisioning delle tue PVC quando crei la serie con stato](#block_dynamic_statefulset), il nome della PVC viene assegnato in base ai valori che hai usato nel file YAML della serie con stato. Affinché la serie con stato utilizzi le PVC esistenti, il nome delle tue PVC deve corrispondere al nome che viene automaticamente creato quando si utilizza il provisioning dinamico.

Prima di iniziare: [accedi al tuo account. Se applicabile, specifica il gruppo di risorse appropriato. Imposta il contesto per il tuo cluster.](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure)

1. Se vuoi eseguire i pre-provisioning della PVC per la tua serie con stato prima di creare la serie con stato, attieniti ai passi da 1 a 3 in [Aggiunta di archiviazione blocchi alle applicazioni](#add_block) per creare una PVC per ogni replica di serie con stato. Assicurati di creare la tua PVC con un nome che rispetta il seguente formato:`<volume_name>-<statefulset_name>-<replica_number>`.
   - **`<volume_name>`**: utilizza il nome che vuoi specificare nella sezione `spec.volumeClaimTemplates.metadata.name` della tua serie con stato, ad esempio `nginxvol`.
   - **`<statefulset_name>`**: utilizza il nome che vuoi specificare nella sezione `metadata.name` della tua serie con stato, ad esempio `nginx_statefulset`.
   - **`<replica_number>`**: immetti il numero della tua replica, iniziando con 0.

   Ad esempio, se devi creare tre repliche della serie con stato, crea tre PVC con i seguenti nomi: `nginxvol-nginx_statefulset-0`, `nginxvol-nginx_statefulset-1` e `nginxvol-nginx_statefulset-2`.  

   Intendi creare una PVC e un PV per un dispositivo di archiviazione esistente? Crea la tua PVC e il tuo PV utilizzando il [provisioning statico](#existing_block).

2. Attieniti alla procedura in [Provisioning dinamico: creazione della PVC quando crei una serie con stato](#block_dynamic_statefulset) per creare la tua serie con stato. Il nome della tua PVC rispetta il formato `<volume_name>-<statefulset_name>-<replica_number>`. Assicurati di utilizzare i seguenti valori dal tuo nome PVC nella specifica della serie con stato:
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
{: #block_change_storage_configuration}

Se vuoi modificare la capacità o le prestazioni di archiviazione, puoi modificare il tuo volume esistente.
{: shortdesc}

Per domande sulla fatturazione e per trovare i passi su come utilizzare la console {{site.data.keyword.cloud_notm}} per modificare la tua archiviazione, vedi [Espansione della capacità di Block Storage](/docs/infrastructure/BlockStorage?topic=BlockStorage-expandingcapacity#expandingcapacity) e [Regolazione di IOPS](/docs/infrastructure/BlockStorage?topic=BlockStorage-adjustingIOPS). Gli aggiornamenti che esegui dalla console non sono riflessi nel volume persistente (PV, persistent volume). Per aggiungere queste informazioni al PV, esegui `oc patch pv <pv_name>` e aggiorna manualmente la dimensione e IOPS nelle sezioni **Etichette** e **Annotazione** del tuo PV.
{: tip}

1. Elenca le PVC nel tuo cluster e prendi nota del nome del PV associato dalla colonna **VOLUME**.
   ```
   oc get pvc
   ```
   {: pre}

   Output di esempio:
   ```
   NAME             STATUS    VOLUME                                     CAPACITY   ACCESS MODES   STORAGECLASS        AGE
   myvol            Bound     pvc-01ac123a-123b-12c3-abcd-0a1234cb12d3   20Gi       RWO            ibmc-block-bronze    147d
   ```
   {: screen}

2. Se vuoi modificare l'IOPS e la dimensione per la tua archiviazione blocchi, modifica l'IOPS prima nella sezione `metadata.labels.IOPS` del tuo PV. Puoi passare a un valore IOPS inferiore o superiore. Assicurati di immettere un IOPS che sia supportato per il tipo di archiviazione di cui disponi. Ad esempio, se hai un'archiviazione blocchi Endurance con 4 IOPS, puoi modificare l'IOPS in 2 o 10. Per più valori IOPS supportati, vedi [Decisioni relative alla tua configurazione dell'archiviazione blocchi](/docs/containers?topic=containers-block_storage#block_predefined_storageclass).
   ```
   oc edit pv <pv_name>
   ```
   {: pre}

   Per modificare l'IOPS dalla CLI, devi anche modificare la dimensione della tua archiviazione blocchi. Se vuoi modificare solo l'IOPS, ma non la dimensione, devi [richiedere la modifica dell'IOPS dalla console](/docs/infrastructure/BlockStorage?topic=BlockStorage-adjustingIOPS).
   {: note}

3. Modifica la PVC e aggiungi la nuova dimensione nella sezione `spec.resources.requests.storage` della tua PVC. Puoi passare a una dimensione maggiore solo fino alla capacità massima impostata dalla tua classe di archiviazione. Non puoi ridurre la dimensione della tua archiviazione esistente. Per vedere le dimensioni disponibili per la tua archiviazione, vedi [Decisioni relative alla configurazione dell'archiviazione blocchi](/docs/containers?topic=containers-block_storage#block_predefined_storageclass).
   ```
   oc edit pvc <pvc_name>
   ```
   {: pre}

4. Verifica che l'espansione del volume sia richiesta. L'espansione del volume è richiesta correttamente quando vedi un messaggio `FileSystemResizePending` nella sezione **Conditions** del tuo output della CLI. 
   ```
   oc describe pvc <pvc_name>
   ```
   {: pre}

   Output di esempio:
   ```
   ...
   Conditions:
   Type                      Status  LastProbeTime                     LastTransitionTime                Reason  Message
   ----                      ------  -----------------                 ------------------                ------  -------
   FileSystemResizePending   True    Mon, 01 Jan 0001 00:00:00 +0000   Thu, 25 Apr 2019 15:52:49 -0400           Waiting for user to (re-)start a pod to finish file system resize of volume on node.
   ```
   {: screen}

5. Elenca tutti i pod che montano la PVC. Se la tua PVC è montata da un pod, l'espansione del volume viene elaborata automaticamente. Se la tua PVC non è montata da un pod, devi montare la PVC in un pod in modo che l'espansione del volume possa essere elaborata. 
   ```
   oc get pods --all-namespaces -o=jsonpath='{range .items[*]}{"\n"}{.metadata.name}{":\t"}{range .spec.volumes[*]}{.persistentVolumeClaim.claimName}{" "}{end}{end}' | grep "<pvc_name>"
   ```
   {: pre}

   I pod montati vengono restituiti nel formato: `<pod_name>: <pvc_name>`.

6. Se la tua PVC non è montata da un pod, [crea un pod o una distribuzione e monta la PVC](/docs/containers?topic=containers-block_storage#add_block). Se la tua PVC è montata da un pod, continua con il passo successivo.  

7. Monitorare lo stato dell'espansione del volume. L'espansione del volume è completa quando vedi il messaggio `"message":"Success"` nel tuo output della CLI.
   ```
   oc get pv <pv_name> -o go-template=$'{{index .metadata.annotations "ibm.io/volume-expansion-status"}}\n'
   ```
   {: pre}

   Output di esempio:
   ```
   {"size":50,"iops":500,"orderid":38832711,"start":"2019-04-30T17:00:37Z","end":"2019-04-30T17:05:27Z","status":"complete","message":"Success"}
   ```
   {: screen}

8. Verifica che la dimensione e l'IOPS siano modificati nella sezione **Etichette** del tuo output della CLI.
   ```
   oc describe pv <pv_name>
   ```
   {: pre}

   Output di esempio:
   ```
   ...
   Labels:       CapacityGb=50
                 Datacenter=dal10
                 IOPS=500
   ```
   {: screen}


## Backup e ripristino di dati
{: #block_backup_restore}

Il provisioning dell'archiviazione blocchi viene eseguito nella stessa ubicazione dei nodi di lavoro nel tuo cluster. L'archiviazione viene ospitata sui server in cluster da IBM per offrire la disponibilità in caso di arresto di un server. Tuttavia, non viene eseguito il backup automatico dell'archiviazione blocchi e potrebbe essere inaccessibile se si verifica un malfunzionamento dell'intera ubicazione. Per evitare che i tuoi dati vengano persi o danneggiati, puoi configurare dei backup periodici che puoi utilizzare per ripristinare i dati quando necessario.
{: shortdesc}

Esamina le seguenti opzioni di backup e ripristino per la tua archiviazione blocchi:

<dl>
  <dt>Configura istantanee periodiche</dt>
  <dd><p>Puoi [configurare delle istantanee periodiche per la tua archiviazione blocchi](/docs/infrastructure/BlockStorage?topic=BlockStorage-snapshots#snapshots), che è un'immagine di sola lettura che acquisisce lo stato dell'istanza in un punto nel tempo. Per archiviare l'istantanea, devi richiedere lo spazio per l'istantanea nella tua archiviazione blocchi. Le istantanee vengono archiviate nell'istanza di archiviazione esistente all'interno della stessa zona. Puoi ripristinare i dati da un'istantanea se un utente rimuove accidentalmente dati importanti dal volume.</br></br> <strong>Per creare un'istantanea per il tuo volume:</strong><ol><li>[Accedi al tuo account. Se applicabile, specifica il gruppo di risorse appropriato. Imposta il contesto per il tuo cluster.](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure)</li><li>Accedi alla CLI `ibmcloud sl`. <pre class="pre"><code>    ibmcloud sl init
    </code></pre></li><li>Elenca i PV esistenti nel tuo cluster. <pre class="pre"><code>oc get pv</code></pre></li><li>Ottieni i dettagli del PV per cui vuoi creare uno spazio per l'istantanea e prendi nota dell'ID volume, della dimensione e dell'IOPS. <pre class="pre"><code>oc describe pv &lt;pv_name&gt;</code></pre> La dimensione e l'IOPS vengono visualizzati nella sezione <strong>Etichette</strong> del tuo output della CLI. Per trovare l'ID volume, controlla l'annotazione <code>ibm.io/network-storage-id</code> del tuo output della CLI. </li><li>Crea la dimensione dell'istantanea per il tuo volume esistente con i parametri che hai richiamato nel passo precedente. <pre class="pre"><code>ibmcloud sl block snapshot-order &lt;volume_ID&gt; --size &lt;size&gt; --tier &lt;iops&gt;</code></pre></li><li>Attendi che la dimensione dell'istantanea venga creata. <pre class="pre"><code>ibmcloud sl block volume-detail &lt;volume_ID&gt;</code></pre>La dimensione dell'istantanea viene fornita correttamente quando la <strong>Dimensione istantanea (GB)</strong> nel tuo output della CLI viene modificata da 0 con la dimensione che hai ordinato. </li><li>Crea l'istantanea per il tuo volume e prendi nota dell'ID dell'istantanea che ti viene creata. <pre class="pre"><code>ibmcloud sl block snapshot-create &lt;volume_ID&gt;</code></pre></li><li>Verifica che l'istantanea sia stata creata correttamente. <pre class="pre"><code>ibmcloud sl block snapshot-list &lt;volume_ID&gt;</code></pre></li></ol></br><strong>Per ripristinare i dati da un'istantanea in un volume esistente: </strong><pre class="pre"><code>ibmcloud sl block snapshot-restore &lt;volume_ID&gt; &lt;snapshot_ID&gt;</code></pre></p></dd>
  <dt>Replica le istantanee in un'altra zona</dt>
 <dd><p>Per proteggere i tuoi dati da un malfunzionamento dell'ubicazione, puoi [replicare le istantanee](/docs/infrastructure/BlockStorage?topic=BlockStorage-replication#replication) in un'istanza di archiviazione blocchi configurata in un'altra zona. I dati possono essere replicati solo dall'archiviazione primaria a quella di backup. Non puoi montare un'istanza di archiviazione blocchi replicata in un cluster. Quando la tua archiviazione primaria non funziona più, puoi impostare manualmente la tua archiviazione di backup replicata in modo che sia quella primaria. Quindi, puoi montarla nel tuo cluster. Una volta ripristinata la tua archiviazione primaria, puoi ripristinare i dati dall'archiviazione di backup.</p></dd>
 <dt>Duplica l'archiviazione</dt>
 <dd><p>Puoi [duplicare la tua istanza di archiviazione blocchi](/docs/infrastructure/BlockStorage?topic=BlockStorage-duplicatevolume#duplicatevolume) nella stessa zona dell'istanza di archiviazione originale. Un duplicato contiene gli stessi dati dell'istanza di archiviazione originale nel momento in cui è stato creato il duplicato. A differenza delle repliche, puoi utilizzare il duplicato come un'istanza di archiviazione indipendente dall'originale. Per eseguire la duplicazione, configura innanzitutto le istantanee per il volume.</p></dd>
  <dt>Esegui il backup dei dati in {{site.data.keyword.cos_full}}</dt>
  <dd><p>Puoi utilizzare l'[**immagine ibm-backup-restore**](/docs/services/RegistryImages/ibm-backup-restore?topic=RegistryImages-ibmbackup_restore_starter#ibmbackup_restore_starter) per avviare un pod di backup e ripristino nel tuo cluster. Questo pod contiene uno script per eseguire un backup una tantum o periodico per qualsiasi attestazione del volume persistente (PVC) nel tuo cluster. I dati vengono archiviati nella tua istanza {{site.data.keyword.cos_full}} che hai configurato in una zona.</p><p class="note">L'archiviazione blocchi viene montata con una modalità di accesso RWO. Questo accesso consente di montare un solo pod nell'archiviazione blocchi alla volta. Per eseguire il backup dei tuoi dati, devi smontare il pod dell'applicazione dall'archiviazione, montarlo nel tuo pod di backup, eseguire il backup dei dati e rimontare l'archiviazione nel tuo pod dell'applicazione. </p>
Per rendere i tuoi dati ancora più altamente disponibili e proteggere la tua applicazione da un errore di zona, configura una seconda istanza {{site.data.keyword.cos_short}} e replica i dati tra le varie zone. Se devi ripristinare i dati dalla tua istanza {{site.data.keyword.cos_short}}, utilizza lo script di ripristino fornito con l'immagine.</dd>
<dt>Copia i dati nei/dai pod e contenitori</dt>
<dd><p>Puoi utilizzare il comando `oc cp` [![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://kubernetes.io/docs/reference/kubectl/overview/#cp) per copiare i file e le directory in/da pod o specifici contenitori nel tuo cluster.</p>
<p>Prima di iniziare: [accedi al tuo account. Se applicabile, specifica il gruppo di risorse appropriato. Imposta il contesto per il tuo cluster.](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure) Se non specifichi un contenitore con <code>-c</code>, il comando utilizza il primo contenitore disponibile nel pod.</p>
<p>Puoi utilizzare il comando in diversi modi:</p>
<ul>
<li>Copia i dati dalla tua macchina locale a un pod nel tuo cluster: <pre class="pre"><code>oc cp <var>&lt;local_filepath&gt;/&lt;filename&gt;</var> <var>&lt;namespace&gt;/&lt;pod&gt;:&lt;pod_filepath&gt;</var></code></pre></li>
<li>Copia i dati da un pod nel tuo cluster alla tua macchina locale: <pre class="pre"><code>oc cp <var>&lt;namespace&gt;/&lt;pod&gt;:&lt;pod_filepath&gt;/&lt;filename&gt;</var> <var>&lt;local_filepath&gt;/&lt;filename&gt;</var></code></pre></li>
<li>Copia i dati dalla tua macchina locale a un contenitore specifico che viene eseguito in un pod nel tuo cluster: <pre class="pre"><code>oc cp <var>&lt;local_filepath&gt;/&lt;filename&gt;</var> <var>&lt;namespace&gt;/&lt;pod&gt;:&lt;pod_filepath&gt;</var> -c <var>&lt;container&gt;</var></code></pre></li>
</ul></dd>
  </dl>

<br />


## Riferimento delle classi di archiviazione
{: #block_storageclass_reference}

### Bronze
{: #block_bronze}

<table>
<caption>Classe di archiviazione blocchi: bronze</caption>
<thead>
<th>Caratteristiche</th>
<th>Impostazione</th>
</thead>
<tbody>
<tr>
<td>Nome</td>
<td><code>ibmc-block-bronze</code></br><code>ibmc-block-retain-bronze</code></td>
</tr>
<tr>
<td>Tipo</td>
<td>[Archiviazione Endurance](/docs/infrastructure/BlockStorage?topic=BlockStorage-About#provendurance)</td>
</tr>
<tr>
<td>File system</td>
<td>ext4</td>
</tr>
<tr>
<td>IOPS per gigabyte</td>
<td>2</td>
</tr>
<tr>
<td>Intervallo di dimensioni in gigabyte</td>
<td>20-12000 Gi</td>
</tr>
<tr>
<td>Disco rigido</td>
<td>SSD</td>
</tr>
<tr>
<td>Fatturazione</td>
<td>Il tipo di fatturazione predefinito dipende dalla versione del tuo plugin {{site.data.keyword.cloud_notm}} Block Storage: <ul><li> Versione 1.0.1 e successive: Ogni ora</li><li>Versione 1.0.0 e precedente: Mensile</li></ul></td>
</tr>
<tr>
<td>Prezzi</td>
<td>[Informazioni sui prezzi![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://www.ibm.com/cloud/block-storage/pricing)</td>
</tr>
</tbody>
</table>


### Silver
{: #block_silver}

<table>
<caption>Classe di archiviazione blocchi: silver</caption>
<thead>
<th>Caratteristiche</th>
<th>Impostazione</th>
</thead>
<tbody>
<tr>
<td>Nome</td>
<td><code>ibmc-block-silver</code></br><code>ibmc-block-retain-silver</code></td>
</tr>
<tr>
<td>Tipo</td>
<td>[Archiviazione Endurance](/docs/infrastructure/BlockStorage?topic=BlockStorage-About#provendurance)</td>
</tr>
<tr>
<td>File system</td>
<td>ext4</td>
</tr>
<tr>
<td>IOPS per gigabyte</td>
<td>4</td>
</tr>
<tr>
<td>Intervallo di dimensioni in gigabyte</td>
<td>20-12000 Gi</td>
</tr>
<tr>
<td>Disco rigido</td>
<td>SSD</td>
</tr>
<tr>
<td>Fatturazione</td>
<td>Il tipo di fatturazione predefinito dipende dalla versione del tuo plugin {{site.data.keyword.cloud_notm}} Block Storage: <ul><li> Versione 1.0.1 e successive: Ogni ora</li><li>Versione 1.0.0 e precedente: Mensile</li></ul></td>
</tr>
<tr>
<td>Prezzi</td>
<td>[Informazioni sui prezzi![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://www.ibm.com/cloud/block-storage/pricing)</td>
</tr>
</tbody>
</table>

### Gold
{: #block_gold}

<table>
<caption>Classe di archiviazione blocchi: gold</caption>
<thead>
<th>Caratteristiche</th>
<th>Impostazione</th>
</thead>
<tbody>
<tr>
<td>Nome</td>
<td><code>ibmc-block-gold</code></br><code>ibmc-block-retain-gold</code></td>
</tr>
<tr>
<td>Tipo</td>
<td>[Archiviazione Endurance](/docs/infrastructure/BlockStorage?topic=BlockStorage-About#provendurance)</td>
</tr>
<tr>
<td>File system</td>
<td>ext4</td>
</tr>
<tr>
<td>IOPS per gigabyte</td>
<td>10</td>
</tr>
<tr>
<td>Intervallo di dimensioni in gigabyte</td>
<td>20-4000 Gi</td>
</tr>
<tr>
<td>Disco rigido</td>
<td>SSD</td>
</tr>
<tr>
<td>Fatturazione</td>
<td>Il tipo di fatturazione predefinito dipende dalla versione del tuo plugin {{site.data.keyword.cloud_notm}} Block Storage: <ul><li> Versione 1.0.1 e successive: Ogni ora</li><li>Versione 1.0.0 e precedente: Mensile</li></ul></td>
</tr>
<tr>
<td>Prezzi</td>
<td>[Informazioni sui prezzi![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://www.ibm.com/cloud/block-storage/pricing)</td>
</tr>
</tbody>
</table>

### Personalizzata
{: #block_custom}

<table>
<caption>Classe di archiviazione blocchi: custom</caption>
<thead>
<th>Caratteristiche</th>
<th>Impostazione</th>
</thead>
<tbody>
<tr>
<td>Nome</td>
<td><code>ibmc-block-custom</code></br><code>ibmc-block-retain-custom</code></td>
</tr>
<tr>
<td>Tipo</td>
<td>[Prestazioni](/docs/infrastructure/BlockStorage?topic=BlockStorage-About#provperformance)</td>
</tr>
<tr>
<td>File system</td>
<td>ext4</td>
</tr>
<tr>
<td>IOPS e dimensione</td>
<td><strong>Intervallo di dimensioni in gigabyte / intervallo di IOPS in multipli di 100</strong><ul><li>20-39 Gi / 100-1000 IOPS</li><li>40-79 Gi / 100-2000 IOPS</li><li>80-99 Gi / 100-4000 IOPS</li><li>100-499 Gi / 100-6000 IOPS</li><li>500-999 Gi / 100-10000 IOPS</li><li>1000-1999 Gi / 100-20000 IOPS</li><li>2000-2999 Gi / 200-40000 IOPS</li><li>3000-3999 Gi / 200-48000 IOPS</li><li>4000-7999 Gi / 300-48000 IOPS</li><li>8000-9999 Gi / 500-48000 IOPS</li><li>10000-12000 Gi / 1000-48000 IOPS</li></ul></td>
</tr>
<tr>
<td>Disco rigido</td>
<td>Il rapporto IOPS-gigabyte determina il tipo di disco rigido di cui viene eseguito il provisioning. Per determinare il tuo rapporto IOPS/gigabyte, dividi l'IOPS per la dimensione della tua archiviazione. </br></br>Esempio: </br>hai scelto 500Gi di archiviazione con 100 IOPS. Il tuo rapporto è 0,2 (100 IOPS/500Gi). </br></br><strong>Panoramica dei tipi di disco rigido per rapporto:</strong><ul><li>Inferiore o uguale a 0,3: SATA</li><li>Maggiore di 0,3: SSD</li></ul></td>
</tr>
<tr>
<td>Fatturazione</td>
<td>Il tipo di fatturazione predefinito dipende dalla versione del tuo plugin {{site.data.keyword.cloud_notm}} Block Storage: <ul><li> Versione 1.0.1 e successive: Ogni ora</li><li>Versione 1.0.0 e precedente: Mensile</li></ul></td>
</tr>
<tr>
<td>Prezzi</td>
<td>[Informazioni sui prezzi![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://www.ibm.com/cloud/block-storage/pricing)</td>
</tr>
</tbody>
</table>

<br />


## Classi di archiviazione personalizzate di esempio
{: #block_custom_storageclass}

Puoi creare una classe di archiviazione personalizzata e utilizzare la classe di archiviazione nella tua PVC.
{: shortdesc}

{{site.data.keyword.containerlong_notm}} fornisce [classi di archiviazione predefinite](#block_storageclass_reference) per eseguire il provisioning dell'archiviazione blocchi con un livello e una configurazione specifici. In alcuni casi, potresti voler eseguire il provisioning dell'archiviazione con una configurazione diversa che non è inclusa nelle classi di archiviazione predefinite. Puoi utilizzare gli esempi in questo argomento per trovare classi di archiviazione personalizzate di esempio.

Per creare la tua classe di archiviazione personalizzata, vedi [Personalizzazione di una classe di archiviazione](/docs/containers?topic=containers-kube_concepts#customized_storageclass). Quindi, [utilizza la classe di archiviazione personalizzata nella tua PVC](#add_block).

### Creazione di un'archiviazione che rileva la topologia
{: #topology_yaml}

Per utilizzare l'archiviazione blocchi in un cluster multizona, il tuo pod deve essere pianificato nella stessa zona della tua istanza di archiviazione blocchi in modo che tu possa leggere e scrivere sul volume. Prima che la pianificazione dei volumi che rileva la topologia fosse introdotta da Kubernetes, il provisioning dinamico della tua archiviazione creava automaticamente l'istanza di archiviazione blocchi quando veniva creata una PVC. Quindi, quando creavi il tuo pod, il programma di pianificazione Kubernetes provava a distribuire il pod allo stesso data center della tua istanza di archiviazione blocchi.
{: shortdesc}

La creazione dell'istanza di archiviazione blocchi senza conoscere i vincoli del pod può portare a risultati indesiderati. Ad esempio, potrebbe non essere possibile pianificare il tuo pod sullo stesso nodo di lavoro della tua archiviazione perché il nodo di lavoro ha risorse insufficienti oppure perché il nodo di lavoro è contaminato e non consente la pianificazione del pod. Con la pianificazione dei volumi che rileva la topologia, l'istanza di archiviazione blocchi viene ritardata finché non viene creato il primo pod che utilizza l'archiviazione.

La pianificazione dei volumi che rileva la topologia è supportata solo sui cluster che eseguono Kubernetes versione 1.12 o successive. Per utilizzare questa funzione, assicurati di aver installato il plugin {{site.data.keyword.cloud_notm}} Block Storage versione 1.2.0 o successive.
{: note}

I seguenti esempi mostrano come creare classi di archiviazione che ritardano la creazione dell'istanza di archiviazione blocchi finché il primo pod che utilizza questa archiviazione non è pronto per essere pianificato. Per ritardare la creazione, devi includere l'opzione `volumeBindingMode: WaitForFirstConsumer`. Se non includi questa opzione, la `volumeBindingMode` viene impostata automaticamente su `Immediate` e l'istanza di archiviazione blocchi viene creata quando crei la PVC.

- **Esempio per l'archiviazione blocchi Endurance:**
  ```
  apiVersion: storage.k8s.io/v1
  kind: StorageClass
  metadata:
    name: ibmc-block-bronze-delayed
  parameters:
    billingType: hourly
    classVersion: "2"
    fsType: ext4
    iopsPerGB: "2"
    sizeRange: '[20-12000]Gi'
    type: Endurance
  provisioner: ibm.io/ibmc-block
  reclaimPolicy: Delete
  volumeBindingMode: WaitForFirstConsumer
  ```
  {: codeblock}

- **Esempio per l'archiviazione blocchi Performance:**
  ```
  apiVersion: storage.k8s.io/v1
  kind: StorageClass
  metadata:
   name: ibmc-block-performance-storageclass
   labels:
     kubernetes.io/cluster-service: "true"
  provisioner: ibm.io/ibmc-block
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

### Specifica della zona e della regione
{: #block_multizone_yaml}

Se vuoi creare la tua archiviazione blocchi in una zona specifica, puoi specificare la zona e la regione in una classe di archiviazione personalizzata.
{: shortdesc}

Utilizza la classe di archiviazione personalizzata se usi il plugin {{site.data.keyword.cloud_notm}} Block Storage versione 1.0.0 o se vuoi eseguire [il provisioning dell'archiviazione blocchi in modo statico](#existing_block) in una zona specifica. In tutti gli altri casi, [specifica la zona direttamente nella tua PVC](#add_block).
{: note}

Il seguente file `.yaml` personalizza una classe di archiviazione basata sulla classe di archiviazione di non conservazione `ibm-block-silver`: il `type` è `"Endurance"`, l'`iopsPerGB` è `4`, il `sizeRange` è `"[20-12000]Gi"` e la `reclaimPolicy` è impostata su `"Delete"`. La zona viene specificata come `dal12`. Per utilizzare una classe di archiviazione differente come tua base, vedi il [riferimento delle classi di archiviazione](#block_storageclass_reference).

Crea la classe di archiviazione nelle stessa regione e nella stessa zona dei tuoi cluster e dei tuoi nodi di lavoro. Per ottenere la regione del tuo cluster, esegui `ibmcloud oc cluster-get --cluster <cluster_name_or_ID>` e cerca il prefisso della regione nell'**URL master**, come ad esempio `eu-de` in `https://c2.eu-de.containers.cloud.ibm.com:11111`. Per ottenere la zona del tuo nodo di lavoro, esegui `ibmcloud oc workers --cluster <cluster_name_or_ID>`.

- **Esempio per l'archiviazione blocchi Endurance:**
  ```
  apiVersion: storage.k8s.io/v1
  kind: StorageClass
  metadata:
    name: ibmc-block-silver-mycustom-storageclass
    labels:
      kubernetes.io/cluster-service: "true"
  provisioner: ibm.io/ibmc-block
  parameters:
    zone: "dal12"
    region: "us-south"
    type: "Endurance"
    iopsPerGB: "4"
    sizeRange: "[20-12000]Gi"
  reclaimPolicy: "Delete"
  ```
  {: codeblock}

- **Esempio per l'archiviazione blocchi Performance:**
  ```
  apiVersion: storage.k8s.io/v1
  kind: StorageClass
  metadata:
    name: ibmc-block-performance-storageclass
    labels:
      kubernetes.io/cluster-service: "true"
  provisioner: ibm.io/ibmc-block
  parameters:
    zone: "dal12"
    region: "us-south"
    type: "Performance"
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
  reclaimPolicy: "Delete"
  ```
  {: codeblock}

### Montaggio dell'archiviazione blocchi con un file system `XFS`
{: #xfs}

I seguenti esempi creano una classe di archiviazione che esegue il provisioning dell'archiviazione blocchi con un file system `XFS`.
{: shortdesc}

- **Esempio per l'archiviazione blocchi Endurance:**
  ```
  apiVersion: storage.k8s.io/v1
  kind: StorageClass
  metadata:
    name: ibmc-block-custom-xfs
    labels:
      addonmanager.kubernetes.io/mode: Reconcile
  provisioner: ibm.io/ibmc-block
  parameters:
    type: "Endurance"
    iopsPerGB: "4"
    sizeRange: "[20-12000]Gi"
    fsType: "xfs"
  reclaimPolicy: "Delete"
  ```

- **Esempio per l'archiviazione blocchi Performance:**
  ```
  apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: ibmc-block-custom-xfs
  labels:
    addonmanager.kubernetes.io/mode: Reconcile
provisioner: ibm.io/ibmc-block
parameters:
  type: "Performance"
  sizeIOPSRange: |-
    [20-39]Gi:[100-1000]
    [40-79]Gi:[100-2000]
    [80-99]Gi:[100-4000]
    [100-499]Gi:[100-6000]
    [500-999]Gi:[100-10000]
    [1000-1999]Gi:[100-20000]
    [2000-2999]Gi:[200-40000]
    [3000-3999]Gi:[200-48000]
    [4000-7999]Gi:[300-48000]
    [8000-9999]Gi:[500-48000]
    [10000-12000]Gi:[1000-48000]
    fsType: "xfs"
     reclaimPolicy: "Delete"
     classVersion: "2"
  ```
  {: codeblock}

<br />



