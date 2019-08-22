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
 
# Rimozione dell'archiviazione persistente da un cluster
{: #cleanup}

Quando configuri l'archiviazione persistente nel tuo cluster, hai tre componenti principali: l'attestazione del volume persistente (o PVC, persistent volume claim) Kubernetes che richiede l'archiviazione, il volume persistente (o PV, persistent volume) montato in un pod e descritto nella PVC e l'istanza dell'infrastruttura IBM Cloud, come l'archiviazione blocchi o file NFS. A seconda di come hai eseguito la creazione della tua archiviazione, potresti dover eliminare tutti e tre separatamente.
{:shortdesc}

## Ripulitura dell'archiviazione persistente
{: #storage_remove}

Descrizione delle tue opzioni di eliminazione:

**Ho eliminato il mio cluster. Devo eliminare qualcos'altro per rimuovere l'archiviazione persistente?**</br>
Dipende. Quando elimini un cluster, la PVC e il PV vengono eliminati. Tuttavia, tu scegli se rimuovere l'istanza di archiviazione associata nell'infrastruttura IBM Cloud. Se scegli di non rimuoverla, l'istanza di archiviazione permane. Tuttavia, se hai eliminato il tuo cluster in uno stato non integro, l'archiviazione potrebbe permanere anche se hai scelto di rimuoverla. Attieniti alle istruzioni, in particolare il passo per [eliminare la tua istanza di archiviazione](#sl_delete_storage) nell'infrastruttura IBM Cloud.

**Posso eliminare la PVC per rimuovere tutta la mia archiviazione?**</br>
In alcuni casi. Se [crei l'archiviazione persistente in modo dinamico](/docs/containers?topic=containers-kube_concepts#dynamic_provisioning) e selezioni una classe di archiviazione senza `retain` nel suo nome, quando elimini la PVC vengono eliminati anche il PV e l'istanza di archiviazione dell'infrastruttura IBM Cloud.

In tutti gli altri casi, attieniti alle istruzioni per controllare lo stato della PVC, del PV e del dispositivo di archiviazione fisico ed eliminali separatamente, se necessario.

**Continuo a incorrere in addebiti per l'archiviazione dopo che l'ho eliminata?**</br>
Dipende da cosa elimini e dal tipo di fatturazione. Se elimini la PVC e il PV ma non l'istanza nel tuo account dell'infrastruttura IBM Cloud, tale istanza permane e incorri in addebiti per essa. Devi eliminare tutto, per evitare addebiti. Inoltre, quando specifichi il tipo di fatturazione (`billingType`) nella PVC, puoi scegliere `hourly` o `monthly`. Se hai scelto `monthly`, la tua istanza viene fatturata mensilmente. Quando elimini l'istanza, ti viene addebitato il resto del mese.

Quando annulli manualmente l'istanza di archiviazione persistente dalla console dell'infrastruttura IBM Cloud o dalla CLI `ibmcloud sl`, la fatturazione viene arrestata nel seguente modo: 
- **Archiviazione oraria**: la fatturazione viene arrestata immediatamente. Dopo che la tua archiviazione è stata annullata, potresti ancora vedere la tua istanza di archiviazione nella console per un massimo di 72 ore.  
- **Archiviazione mensile**: puoi scegliere tra l'**annullamento immediato** o l'**annullamento alla data di anniversario**. Se scegli un annullamento immediato, la tua archiviazione viene rimossa immediatamente e non puoi utilizzare più la tua archiviazione. Se scegli di annullare la tua archiviazione alla successiva data di anniversario, le tue istanze dell'archiviazione rimangono attive fino alla successiva data di anniversario e puoi continuare a utilizzarle fino a questa data. In entrambi i casi, la fatturazione viene arrestata per il successivo ciclo di fatturazione ma ti viene comunque addebitato in fattura il ciclo di fatturazione corrente fino alla sua fine. Dopo che la tua archiviazione è stata annullata, potresti ancora vedere la tua istanza di archiviazione nella console o nella CLI per un massimo di 72 ore.  

Se rimuovi l'archiviazione persistente con una politica di riacquisizione `Delete` di cui avevi eseguito dinamicamente il provisioning eliminando la PVC, l'archiviazione viene rimossa indipendentemente dal fatto che tu abbia scelto un tipo di fatturazione orario o mensile. Dopo che la tua archiviazione è stata rimossa, potresti ancora vedere la tua istanza di archiviazione nella console o nella CLI per un massimo di 72 ore. L'archiviazione persistente che utilizza una politica di riacquisizione `Retain` non viene rimossa e te ne viene comunque addebitato in fattura il suo utilizzo. 

<p class="important">Quando ripulisci l'archiviazione persistente, elimini tutti i dati in essa archiviati. Se hai bisogno di una copia dei dati, crea un backup per l'[archiviazione file](/docs/containers?topic=containers-file_storage#file_backup_restore) o l'[archiviazione blocchi](/docs/containers?topic=containers-block_storage#block_backup_restore).  </p>

**Ho eliminato la mia archiviazione. Perché posso ancora vedere le mie istanze?** </br>
Dopo che hai rimosso l'archiviazione persistente, ci possono volere 72 ore perché la rimozione venga elaborata completamente e perché l'archiviazione scompaia dalla CLI o dalla console dell'infrastruttura IBM Cloud. 

Prima di iniziare: [accedi al tuo account. Se applicabile, specifica il gruppo di risorse appropriato. Imposta il contesto per il tuo cluster.](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure)

Per ripulire i dati persistenti:

1.  Elenca le PVC nel tuo cluster e prendi nota del **`NAME`** della PVC, della **`STORAGECLASS`** e del nome del PV associato alla PVC e visualizzato come **`VOLUME`**.
    ```
    oc get pvc
    ```
    {: pre}

    Output di esempio:
    ```
    NAME                  STATUS    VOLUME                                     CAPACITY   ACCESSMODES   STORAGECLASS            AGE
    claim1-block-bronze   Bound     pvc-06886b77-102b-11e8-968a-f6612bb731fb   20Gi       RWO           ibmc-block-bronze       78d
    claim-file-bronze     Bound     pvc-457a2b96-fafc-11e7-8ff9-b6c8f770356c   4Gi        RWX           ibmc-file-bronze-retain 105d
    claim-file-silve      Bound     pvc-1efef0ba-0c48-11e8-968a-f6612bb731fb   24Gi       RWX           ibmc-file-silver        83d
    ```
    {: screen}

2. Esamina **`ReclaimPolicy`** e **`billingType`** per la classe di archiviazione.
   ```
   oc describe storageclass <storageclass_name>
   ```
   {: pre}

   Se la politica di riacquisizione indica `Delete`, il tuo PV e la tua archiviazione fisica vengono rimossi quando rimuovi la PVC. Se la politica di riacquisizione indica `Retain`, o se hai eseguito il provisioning della tua archiviazione senza una classe di archiviazione, il PV e l'archiviazione fisica non vengono rimossi quando rimuovi la PVC. Devi rimuovere la PVC, il PV e l'archiviazione fisica separatamente.

   Se la tua archiviazione viene addebitata mensilmente, ti viene comunque addebitato l'importo per l'intero mese, anche se rimuovi l'archiviazione prima della fine del ciclo di fatturazione.
   {: important}

3. Rimuovi gli eventuali pod che montano la PVC.
   1. Elenca i pod che montano la PVC.
      ```
      oc get pods --all-namespaces -o=jsonpath='{range .items[*]}{"\n"}{.metadata.name}{":\t"}{range .spec.volumes[*]}{.persistentVolumeClaim.claimName}{" "}{end}{end}' | grep "<pvc_name>"
      ```
      {: pre}

      Output di esempio:
      ```
      blockdepl-12345-prz7b:	claim1-block-bronze  
      ```
      {: screen}

      Se non viene restituito alcun pod nel tuo output della CLI, non hai alcun pod che utilizza la PVC.

   2. Rimuovi il pod che utilizza la PVC. Se il pod fa parte di una distribuzione, rimuovi la distribuzione.
      ```
      oc delete pod <pod_name>
      ```
      {: pre}

   3. Verifica che il pod venga rimosso.
      ```
      oc get pods
      ```
      {: pre}

4. Rimuovi la PVC.
   ```
   oc delete pvc <pvc_name>
   ```
   {: pre}

5. Esamina lo stato del tuo PV. Utilizza il nome del PV che hai richiamato in precedenza come **`VOLUME`**.
   ```
   oc get pv <pv_name>
   ```
   {: pre}

   Quando rimuovi la PVC, il PV ad essa associato viene rilasciato. A seconda di come hai eseguito il provisioning della tua archiviazione, il tuo PV passa a uno stato di `Deleting`, se il PV viene eliminato automaticamente, oppure a uno stato di `Released`, se devi eliminarlo manualmente. **Nota:**: per i PV eliminati automaticamente, lo stato potrebbe brevemente indicare `Released` prima che venga eliminato. Riesegui il comando dopo qualche minuto per appurare se il PV viene rimosso.

6. Se il tuo PV non viene eliminato, rimuovilo manualmente.
   ```
   oc delete pv <pv_name>
   ```
   {: pre}

7. Verifica che il PV venga rimosso.
   ```
   oc get pv
   ```
   {: pre}

8. {: #sl_delete_storage}Elenca l'istanza di archiviazione fisica a cui puntava il tuo PV e prendi nota del suo **`id`**.

   **Archiviazione file:**
   ```
   ibmcloud sl file volume-list --columns id  --columns notes | grep <pv_name>
   ```
   {: pre}
   **Archiviazione blocchi:**
   ```
   ibmcloud sl block volume-list --columns id --columns notes | grep <pv_name>
   ```
   {: pre}

   Se hai rimosso il tuo cluster e non puoi richiamare il nome del PV, sostituisci `grep <pv_name>` con `grep <cluster_id>` per elencare tutti i dispositivi di archiviazione associati al tuo cluster.
   {: tip}

   Output di esempio:
   ```
   id         notes
   12345678   {"plugin":"ibm-file-plugin-5b55b7b77b-55bb7","region":"us-south","cluster":"aa1a11a1a11b2b2bb22b22222c3c3333","type":"Endurance","ns":"default","pvc":"mypvc","pv":"pvc-d979977d-d79d-77d9-9d7d-d7d97ddd99d7","storageclass":"ibmc-file-gold"}
   ```
   {: screen}

   Descrizione delle informazioni del campo **Note**.
   *  **`"plugin":"ibm-file-plugin-5b55b7b77b-55bb7"`**: il plugin di archiviazione utilizzato dal cluster.
   *  **`"region":"us-south"`**: la regione in cui si trova il tuo cluster.
   *  **`"cluster":"aa1a11a1a11b2b2bb22b22222c3c3333"`**: l'ID cluster associato all'istanza di archiviazione.
   *  **`"type":"Endurance"`**: il tipo di archiviazione file o blocchi, `Endurance` o `Performance`.
   *  **`"ns":"default"`**: lo spazio dei nomi a cui viene distribuita l'istanza di archiviazione.
   *  **`"pvc":"mypvc"`**: il nome della PVC associata all'istanza di archiviazione.
   *  **`"pv":"pvc-d979977d-d79d-77d9-9d7d-d7d97ddd99d7"`**: il PV associato all'istanza di archiviazione
   *  **`"storageclass":"ibmc-file-gold"`**: il tipo di classe di archiviazione: bronze, silver, gold o personalizzata.

9. Rimuovi l'istanza di archiviazione fisica.

   **Archiviazione file:**
   ```
   ibmcloud sl file volume-cancel <filestorage_id>
   ```
   {: pre}

   **Archiviazione blocchi:**
   ```
   ibmcloud sl block volume-cancel <blockstorage_id>
   ```
   {: pre}

10. Verifica che l'istanza di archiviazione fisica venga rimossa. 
   
   Il completamento del processo di eliminazione potrebbe impiegare fino a 72 ore.
   {: important}

   **Archiviazione file:**
   ```
   ibmcloud sl file volume-list
   ```
   {: pre}
   **Archiviazione blocchi:**
   ```
   ibmcloud sl block volume-list
   ```
   {: pre}


