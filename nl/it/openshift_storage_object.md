---

copyright:
  years: 2014, 2019
lastupdated: "2019-07-31"

keywords: openshift, rhoks, roks, rhos

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

# Archiviazione dei dati su IBM Cloud Object Storage
{: #object_storage}

[{{site.data.keyword.cos_full_notm}}](/docs/services/cloud-object-storage?topic=cloud-object-storage-about-ibm-cloud-object-storage) è un'archiviazione persistente e altamente disponibile che puoi montare sulle applicazioni eseguite in un cluster Kubernetes utilizzando il plugin {{site.data.keyword.cos_full_notm}}. Il plugin è un plugin Kubernetes Flex-Volume che connette i bucket {{site.data.keyword.cos_short}} cloud ai pod nel tuo cluster. Le informazioni archiviate con {{site.data.keyword.cos_full_notm}} sono crittografate in transito e quando sono inattive, vengono diffuse tra più ubicazioni geografiche e vi si accede su HTTP utilizzando una API REST.
{: shortdesc}

Per stabilire una connessione a {{site.data.keyword.cos_full_notm}}, il tuo cluster richiede l'accesso alla rete pubblica per eseguire l'autenticazione presso {{site.data.keyword.cloud_notm}} Identity and Access Management. Se ha un cluster solo privato, puoi comunicare con l'endpoint del servizio privato di {{site.data.keyword.cos_full_notm}} se installi il plugin versione `1.0.3` o successive e configuri la tua istanza del servizio {{site.data.keyword.cos_full_notm}} per l'autenticazione HMAC. Se non desideri utilizzare l'autenticazione HMAC, devi aprire tutto il traffico di rete in uscita sulla porta 443 perché il plugin funzioni correttamente in un cluster privato.
{: important}

Con la versione 1.0.5, il plug-in {{site.data.keyword.cos_full_notm}} viene rinominato da `ibmcloud-object-storage-plugin` a `ibm-object-storage-plugin`. Per installare la nuova versione del plug-in, devi [disinstallare la vecchia installazione del grafico Helm](#remove_cos_plugin) e [reinstallare il grafico Helm con la nuova versione del plug-in {{site.data.keyword.cos_full_notm}}](#install_cos).
{: note}

Con la versione 1.0.8, il grafico Helm del plugin {{site.data.keyword.cos_full_notm}} è ora disponibile nel repository Helm `ibm-charts`. Assicurati di recuperare la versione più recente del grafico Helm da questo repository. Per aggiungere il repository, esegui `helm repo add ibm-charts https://icr.io/helm/ibm-charts`.
{: note}

## Creazione della tua istanza del servizio di archiviazione oggetti
{: #create_cos_service}

Prima di poter iniziare a utilizzare l'archiviazione oggetti nel tuo cluster, devi eseguire il provisioning di un'istanza del servizio {{site.data.keyword.cos_full_notm}} nel tuo account.
{: shortdesc}

Il plugin {{site.data.keyword.cos_full_notm}} è configurato per funzionare con qualsiasi endpoint API s3. Ad esempio, potresti voler utilizzare un server Cloud Object Storage locale, come ad esempio [Minio](https://cloud.ibm.com/kubernetes/solutions/helm-charts/ibm-charts/ibm-minio-objectstore), oppure stabilire una connessione a un endpoint API s3 che configuri a un provider cloud differente invece di utilizzare un'istanza del servizio {{site.data.keyword.cos_full_notm}}.

Attieniti alla seguente procedura per creare un'istanza del servizio {{site.data.keyword.cos_full_notm}}. Se intendi utilizzare un server Cloud Object Storage locale oppure un endpoint API s3 differente, fai riferimento alla documentazione del provider per configurare la tua istanza Cloud Object Storage.

1. Esegui una distribuzione dell'istanza del servizio {{site.data.keyword.cos_full_notm}}.
   1.  Apri la [pagina del catalogo {{site.data.keyword.cos_full_notm}}](https://cloud.ibm.com/catalog/services/cloud-object-storage).
   2.  Immetti un nome per la tua istanza del servizio, come `cos-backup`, e seleziona lo stesso gruppo di risorse in cui si trova il tuo cluster. Per visualizzare il gruppo di risorse del tuo cluster, esegui `ibmcloud oc cluster-get --cluster <cluster_name_or_ID>`.   
   3.  Esamina le [opzioni di piano ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://www.ibm.com/cloud-computing/bluemix/pricing-object-storage#s3api) per le informazioni sui prezzi e seleziona un piano.
   4.  Fai clic su **Crea**. Viene visualizzata la pagina dei dettagli del servizio.
2. {: #service_credentials}Richiama le credenziali del servizio {{site.data.keyword.cos_full_notm}}.
   1.  Nella navigazione nella pagina dei dettagli del servizio, fai clic su **Credenziali del servizio**.
   2.  Fai clic su **Nuova credenziale**. Viene visualizzata una finestra di dialogo.
   3.  Immetti un nome per le tue credenziali.
   4.  Dall'elenco a discesa **Ruolo**, seleziona `Writer` o `Manager`. Se selezioni `Reader`, non puoi utilizzare le credenziali per creare i bucket in {{site.data.keyword.cos_full_notm}} e scrivere dati in esso.
   5.  Facoltativo: in **Aggiungi parametri di configurazione inline (facoltativo)**, immetti `{"HMAC":true}` per creare credenziali HMAC aggiuntive per il servizio {{site.data.keyword.cos_full_notm}}. L'autenticazione HMAC aggiunge un ulteriore livello di sicurezza all'autenticazione OAuth2 prevenendo l'uso improprio di token OAuth2 scaduti o creati casualmente. **Importante**: se hai un cluster solo privato senza accesso pubblico, devi utilizzare l'autenticazione HMAC in modo da poter accedere al servizio {{site.data.keyword.cos_full_notm}} sulla rete privata.
   6.  Fai clic su **Aggiungi**. Le tue nuove credenziali sono elencate nella tabella **Credenziali del servizio**.
   7.  Fai clic su **Visualizza credenziali**.
   8.  Prendi nota dell'**apikey** per utilizzare i token OAuth2 per eseguire l'autenticazione presso il servizio {{site.data.keyword.cos_full_notm}}. Per l'autenticazione HMAC, nella sezione **cos_hmac_keys**, prendi nota di **access_key_id** e **secret_access_key**.
3. [Archivia le tue credenziali del servizio in un segreto Kubernetes all'interno del cluster](#create_cos_secret) per abilitare l'accesso alla tua istanza del servizio {{site.data.keyword.cos_full_notm}}.

## Creazione di un segreto per le credenziali del servizio di archiviazione oggetti
{: #create_cos_secret}

Per accedere alla tua istanza del servizio {{site.data.keyword.cos_full_notm}} per leggere e scrivere dati, devi archiviare in modo protetto le credenziali del servizio in un segreto Kubernetes. Il plugin {{site.data.keyword.cos_full_notm}} utilizza queste credenziali per ogni operazione di lettura o scrittura nel tuo bucket.
{: shortdesc}

Attieniti alla seguente procedura per creare un segreto Kubernetes per le credenziali di un'istanza del servizio {{site.data.keyword.cos_full_notm}}. Se intendi utilizzare un server Cloud Object Storage locale su un endpoint API s3 differente, crea un segreto Kubernetes con le credenziali appropriate.

Prima di iniziare: [accedi al tuo account. Se applicabile, specifica il gruppo di risorse appropriato. Imposta il contesto per il tuo cluster.](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure)

1. Richiama la **apikey**, oppure l'**access_key_id** e la **secret_access_key**, delle tue [credenziali del servizio {{site.data.keyword.cos_full_notm}}](#service_credentials).

2. Ottieni il **GUID** della tua istanza del servizio {{site.data.keyword.cos_full_notm}}.
   ```
   ibmcloud resource service-instance <service_name> | grep GUID
   ```
   {: pre}

3. Crea un segreto Kubernetes per archiviare le tue credenziali del servizio. Quando crei il tuo segreto, tutti i valori vengono automaticamente codificati in base64.

   **Esempio per l'utilizzo della chiave API:**
   ```
   oc create secret generic cos-write-access --type=ibm/ibmc-s3fs --from-literal=api-key=<api_key> --from-literal=service-instance-id=<service_instance_guid>
   ```
   {: pre}

   **Esempio per l'autenticazione HMAC:**
   ```
   oc create secret generic cos-write-access --type=ibm/ibmc-s3fs --from-literal=access-key=<access_key_ID> --from-literal=secret-key=<secret_access_key>
   ```
   {: pre}

   <table>
   <caption>Descrizione dei componenti del comando</caption>
   <thead>
   <th colspan=2><img src="images/idea.png" alt="Icona Idea"/> Descrizione dei componenti del comando</th>
   </thead>
   <tbody>
   <tr>
   <td><code>api-key</code></td>
   <td>Immetti la chiave API che hai richiamato dalle tue credenziali del servizio {{site.data.keyword.cos_full_notm}} precedentemente. Se vuoi utilizzare l'autenticazione HMAC, specifica invece <code>access-key</code> e <code>secret-key</code>.  </td>
   </tr>
   <tr>
   <td><code>access-key</code></td>
   <td>Immetti l'ID chiave di accesso che hai richiamato dalle tue credenziali del servizio {{site.data.keyword.cos_full_notm}} precedentemente. Se vuoi utilizzare l'autenticazione OAuth2, specifica invece <code>api-key</code>.  </td>
   </tr>
   <tr>
   <td><code>secret-key</code></td>
   <td>Immetti la chiave di accesso segreta che hai richiamato dalle tue credenziali del servizio {{site.data.keyword.cos_full_notm}} precedentemente. Se vuoi utilizzare l'autenticazione OAuth2, specifica invece <code>api-key</code>.</td>
   </tr>
   <tr>
   <td><code>service-instance-id</code></td>
   <td>Immetti il GUID della tua istanza del servizio {{site.data.keyword.cos_full_notm}} che hai richiamato precedentemente. </td>
   </tr>
   </tbody>
   </table>

4. Verifica che il segreto venga creato nel tuo spazio dei nomi.
   ```
   oc get secret
   ```
   {: pre}

5. [Installa il plugin {{site.data.keyword.cos_full_notm}}](#install_cos) o, se lo hai già installato, [decidi in merito alla configurazione ]( #configure_cos) per il tuo bucket {{site.data.keyword.cos_full_notm}}.

## Installazione del plugin IBM Cloud Object Storage
{: #install_cos}

Installa il plugin {{site.data.keyword.cos_full_notm}} con un grafico Helm per configurare le classi di archiviazione predefinite per {{site.data.keyword.cos_full_notm}}. Puoi utilizzare queste classi di archiviazione per creare una PVC per eseguire il provisioning di {{site.data.keyword.cos_full_notm}} per le tue applicazioni.
{: shortdesc}

Cerchi le istruzioni su come aggiornare o rimuovere il plugin {{site.data.keyword.cos_full_notm}}? Vedi [Aggiornamento del plugin](#update_cos_plugin) e [Rimozione del plugin](#remove_cos_plugin).
{: tip}

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

2.  Scegli se vuoi installare il plug-in {{site.data.keyword.cos_full_notm}} con o senza il server Helm, Tiller. Quindi, [attieniti alle istruzioni](/docs/containers?topic=containers-helm#public_helm_install) per installare il client Helm sulla tua macchina locale e, facoltativamente, Tiller con un account del servizio nel tuo cluster. **Nota**: se usi Windows, devi installare Tiller.

3. Se vuoi installare il plug-in con Tiller, verifica che Tiller sia installato con un account del servizio.
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

4. Aggiungi il repository {{site.data.keyword.cloud_notm}} Helm al tuo cluster.
   ```
   helm repo add ibm-charts https://icr.io/helm/ibm-charts
   ```
   {: pre}

4. Aggiorna il repository Helm per richiamare la versione più recente di tutti i grafici Helm in questo repository.
   ```
   helm repo update
   ```
   {: pre}

5. Scarica i grafici Helm e decomprimi i grafici nella directory corrente.
   ```
   helm fetch --untar ibm-charts/ibm-object-storage-plugin
   ```
   {: pre}

7. Se utilizzi una distribuzione Linux oppure OS X, installa il plug-in Helm {{site.data.keyword.cos_full_notm}} `ibmc`. Il plugin viene utilizzato per richiamare automaticamente l'ubicazione del tuo cluster e per impostare l'endpoint API per i tuoi bucket {{site.data.keyword.cos_full_notm}} nelle tue classi di archiviazione. Se utilizzi Windows come sistema operativo, vai al passo successivo.
   1. Installa il plugin Helm.
      ```
      helm plugin install ./ibm-object-storage-plugin/helm-ibmc
      ```
      {: pre}

      Output di esempio:
      ```
      Installed plugin: ibmc
      ```
      {: screen}

      Se vedi l'errore `Error: plugin already exists`, rimuovi il plug-in Helm `ibmc` eseguendo `rm -rf ~/.helm/plugins/helm-ibmc`.
      {: tip}

   2. Verifica che il plugin `ibmc` sia installato correttamente.
      ```
      helm ibmc --help
      ```
      {: pre}

      Output di esempio:
      ```
      Install or upgrade Helm charts in IBM K8S Service(IKS) and IBM Cloud Private(ICP)

      Available Commands:
         helm ibmc install [CHART][flags]                      Install a Helm chart
         helm ibmc upgrade [RELEASE][CHART] [flags]            Upgrade the release to a new version of the Helm chart
         helm ibmc template [CHART][flags] [--apply|--delete]  Install/uninstall a Helm chart without tiller

      Available Flags:
         -h, --help                    (Optional) This text.
         -u, --update                  (Optional) Update this plugin to the latest version

      Example Usage:
         With Tiller:
             Install:   helm ibmc install ibm-charts/ibm-object-storage-plugin --name ibm-object-storage-plugin
         Without Tiller:
             Install:   helm ibmc template ibm-charts/ibm-object-storage-plugin --apply
             Dry-run:   helm ibmc template ibm-charts/ibm-object-storage-plugin
             Uninstall: helm ibmc template ibm-charts/ibm-object-storage-plugin --delete

      Note:
         1. It is always recommended to install latest version of ibm-object-storage-plugin chart.
         2. It is always recommended to have 'oc' client up-to-date.
      ```
      {: screen}

      Se l'output mostra l'errore `Error: fork/exec /home/iksadmin/.helm/plugins/helm-ibmc/ibmc.sh: permission denied`, esegui `chmod 755 ~/.helm/plugins/helm-ibmc/ibmc.sh`. Esegui quindi nuovamente `helm ibmc --help`.
      {: tip}

8. Facoltativo: limita il plugin {{site.data.keyword.cos_full_notm}} per accedere solo ai segreti Kubernetes che detengono le tue credenziali del servizio {{site.data.keyword.cos_full_notm}}. Per impostazione predefinita, il plugin è autorizzato ad accedere a tutti i segreti Kubernetes nel tuo cluster.
   1. [Crea la tua istanza del servizio {{site.data.keyword.cos_full_notm}}](#create_cos_service).
   2. [Archivia le tue credenziali del servizio {{site.data.keyword.cos_full_notm}} in un segreto Kubernetes](#create_cos_secret).
   3. Passa alla directory `templates` ed elenca i file disponibili.  
      ```
      cd ibm-object-storage-plugin/templates && ls
      ```
      {: pre}

   4. Apri il file `provisioner-sa.yaml` e cerca la definizione di `ClusterRole` `ibmcloud-object-storage-secret-reader`.
   6. Aggiungi il nome del segreto che hai creato in precedenza all'elenco di segreti a cui il plug-in è autorizzato ad accedere nella sezione `resourceNames`.
      ```
      kind: ClusterRole
      apiVersion: rbac.authorization.k8s.io/v1beta1
      metadata:
        name: ibmcloud-object-storage-secret-reader
      rules:
      - apiGroups: [""]
        resources: ["secrets"]
        resourceNames: ["<secret_name1>","<secret_name2>"]
        verbs: ["get"]
      ```
      {: codeblock}
   7. Salva le modifiche.

9. Installa il plug-in {{site.data.keyword.cos_full_notm}}. Quando installi il plug-in, al tuo cluster vengono aggiunte le classi di archiviazione predefinite.

   - **Per OS X e Linux:**
     - Se hai tralasciato il passo precedente, installa senza una limitazione a specifici segreti Kubernetes.</br>
       **Senza Tiller**:
       ```
       helm ibmc template ibm-charts/ibm-object-storage-plugin --apply
       ```
       {: pre}

       **Con Tiller**:
       ```
       helm ibmc install ibm-charts/ibm-object-storage-plugin --name ibm-object-storage-plugin
       ```
       {: pre}

     - Se hai completato il passo precedente, installa con una limitazione a specifici segreti Kubernetes.</br>
       **Senza Tiller**:
       ```
       cd ../..
       helm ibmc template ./ibm-object-storage-plugin --apply
       ```
       {: pre}

       **Con Tiller**:
       ```
       cd ../..
       helm ibmc install ./ibm-object-storage-plugin --name ibm-object-storage-plugin
       ```
       {: pre}

   - **Per Windows:**
     1. Richiama la zona in cui è distribuito il tuo cluster e memorizzala in una variabile di ambiente.
        ```
        export DC_NAME=$(oc get cm cluster-info -n kube-system -o jsonpath='{.data.cluster-config\.json}' | grep datacenter | awk -F ': ' '{print $2}' | sed 's/\"//g' |sed 's/,//g')
        ```
        {: pre}

     2. Verifica che la variabile di ambiente sia impostata.
        ```
        printenv
        ```
        {: pre}

     3. Installa il grafico Helm.
        - Se hai tralasciato il passo precedente, installa senza una limitazione a specifici segreti Kubernetes.</br>
          ```
          helm install ibm-charts/ibm-object-storage-plugin --name ibm-object-storage-plugin
          ```
          {: pre}

        - Se hai completato il passo precedente, installa con una limitazione a specifici segreti Kubernetes.</br>
          ```
          cd ../..
          helm install ./ibm-object-storage-plugin --name ibm-object-storage-plugin
          ```
          {: pre}

   Output di esempio per l'installazione senza Tiller:
   ```
   Rendering the Helm chart templates...
   DC: dal10
   Chart: ibm-charts/ibm-object-storage-plugin
   wrote object-storage-templates/ibm-object-storage-plugin/templates/ibmc-s3fs-cold-cross-region.yaml
   wrote object-storage-templates/ibm-object-storage-plugin/templates/ibmc-s3fs-cold-regional.yaml
   wrote object-storage-templates/ibm-object-storage-plugin/templates/ibmc-s3fs-flex-cross-region.yaml
   wrote object-storage-templates/ibm-object-storage-plugin/templates/ibmc-s3fs-flex-perf-cross-region.yaml
   wrote object-storage-templates/ibm-object-storage-plugin/templates/ibmc-s3fs-flex-perf-regional.yaml
   wrote object-storage-templates/ibm-object-storage-plugin/templates/ibmc-s3fs-flex-regional.yaml
   wrote object-storage-templates/ibm-object-storage-plugin/templates/ibmc-s3fs-standard-cross-region.yaml
   wrote object-storage-templates/ibm-object-storage-plugin/templates/ibmc-s3fs-standard-perf-cross-region.yaml
   wrote object-storage-templates/ibm-object-storage-plugin/templates/ibmc-s3fs-standard-perf-regional.yaml
   wrote object-storage-templates/ibm-object-storage-plugin/templates/ibmc-s3fs-standard-regional.yaml
   wrote object-storage-templates/ibm-object-storage-plugin/templates/ibmc-s3fs-vault-cross-region.yaml
   wrote object-storage-templates/ibm-object-storage-plugin/templates/ibmc-s3fs-vault-regional.yaml
   wrote object-storage-templates/ibm-object-storage-plugin/templates/flex-driver-sa.yaml
   wrote object-storage-templates/ibm-object-storage-plugin/templates/provisioner-sa.yaml
   wrote object-storage-templates/ibm-object-storage-plugin/templates/flex-driver.yaml
   wrote object-storage-templates/ibm-object-storage-plugin/templates/tests/check-driver-install.yaml
   wrote object-storage-templates/ibm-object-storage-plugin/templates/provisioner.yaml
   Installing the Helm chart...
   serviceaccount/ibmcloud-object-storage-driver created
   daemonset.apps/ibmcloud-object-storage-driver created
   storageclass.storage.k8s.io/ibmc-s3fs-cold-cross-region created
   storageclass.storage.k8s.io/ibmc-s3fs-cold-regional created
   storageclass.storage.k8s.io/ibmc-s3fs-flex-cross-region created
   storageclass.storage.k8s.io/ibmc-s3fs-flex-perf-cross-region created
   storageclass.storage.k8s.io/ibmc-s3fs-flex-perf-regional created
   storageclass.storage.k8s.io/ibmc-s3fs-flex-regional created
   storageclass.storage.k8s.io/ibmc-s3fs-standard-cross-region created
   storageclass.storage.k8s.io/ibmc-s3fs-standard-perf-cross-region created
   storageclass.storage.k8s.io/ibmc-s3fs-standard-perf-regional created
   storageclass.storage.k8s.io/ibmc-s3fs-standard-regional created
   storageclass.storage.k8s.io/ibmc-s3fs-vault-cross-region created
   storageclass.storage.k8s.io/ibmc-s3fs-vault-regional created
   serviceaccount/ibmcloud-object-storage-plugin created
   clusterrole.rbac.authorization.k8s.io/ibmcloud-object-storage-plugin created
   clusterrole.rbac.authorization.k8s.io/ibmcloud-object-storage-secret-reader created
   clusterrolebinding.rbac.authorization.k8s.io/ibmcloud-object-storage-plugin created
   clusterrolebinding.rbac.authorization.k8s.io/ibmcloud-object-storage-secret-reader created
   deployment.apps/ibmcloud-object-storage-plugin created
   pod/ibmcloud-object-storage-driver-test created
   ```
   {: screen}

10. Verifica che il plugin sia installato correttamente.
    ```
    oc get pod -n default -o wide | grep object
    ```
    {: pre}

    Output di esempio:
    ```
    ibmcloud-object-storage-driver-9n8g8                              1/1       Running   0          2m
   ibmcloud-object-storage-plugin-7c774d484b-pcnnx                   1/1       Running   0          2m
    ```
    {: screen}

    L'installazione ha avuto esito positivo quando visualizzi un pod `ibmcloud-object-storage-plugin` e uno o più pod `ibmcloud-object-storage-driver`. Il numero di pod `ibmcloud-object-storage-driver` è uguale al numero di nodi di lavoro nel tuo cluster. Tutti i pod devono essere in uno stato `Running` perché il plugin funzioni correttamente. Se si verifica un malfunzionamento del pod, esegui `oc describe pod -n kube-system <pod_name>` per trovare la causa radice del malfunzionamento.

11. Verifica che le classi di archiviazione vengano create correttamente.
    ```
    oc get storageclass | grep s3
    ```
    {: pre}

    Output di esempio:
    ```
    ibmc-s3fs-cold-cross-region            ibm.io/ibmc-s3fs   8m
   ibmc-s3fs-cold-regional                ibm.io/ibmc-s3fs   8m
   ibmc-s3fs-flex-cross-region            ibm.io/ibmc-s3fs   8m
   ibmc-s3fs-flex-perf-cross-region       ibm.io/ibmc-s3fs   8m
   ibmc-s3fs-flex-perf-regional           ibm.io/ibmc-s3fs   8m
   ibmc-s3fs-flex-regional                ibm.io/ibmc-s3fs   8m
   ibmc-s3fs-standard-cross-region        ibm.io/ibmc-s3fs   8m
   ibmc-s3fs-standard-perf-cross-region   ibm.io/ibmc-s3fs   8m
   ibmc-s3fs-standard-perf-regional       ibm.io/ibmc-s3fs   8m
   ibmc-s3fs-standard-regional            ibm.io/ibmc-s3fs   8m
   ibmc-s3fs-vault-cross-region           ibm.io/ibmc-s3fs   8m
   ibmc-s3fs-vault-regional               ibm.io/ibmc-s3fs   8m
    ```
    {: screen}

12. Ripeti i passi per tutti i cluster dove vuoi accedere ai bucket {{site.data.keyword.cos_full_notm}}.

### Aggiornamento del plugin IBM Cloud Object Storage
{: #update_cos_plugin}

Puoi eseguire un upgrade del plugin {{site.data.keyword.cos_full_notm}} esistente alla versione più recente.
{: shortdesc}

1. Se hai precedentemente installato la versione 1.0.4 o antecedente del grafico Helm denominato `ibmcloud-object-storage-plugin`, rimuovi questa installazione Helm dal tuo cluster. Reinstalla quindi il grafico Helm.
   1. Controlla se la vecchia versione del grafico Helm {{site.data.keyword.cos_full_notm}} è installata nel tuo cluster.  
      ```
      helm ls | grep ibmcloud-object-storage-plugin
      ```
      {: pre}

      Output di esempio:
      ```
      ibmcloud-object-storage-plugin	1       	Mon Sep 18 15:31:40 2017	DEPLOYED	ibmcloud-object-storage-plugin-1.0.4	default
      ```
      {: screen}

   2. Se hai la versione 1.0.4 o antecedente del grafico Helm denominato `ibmcloud-object-storage-plugin`, rimuovi il grafico Helm dal tuo cluster. Se hai la versione 1.0.5 o versioni successive del grafico Helm denominato `ibm-object-storage-plugin`, continua con il passo 2.
      ```
      helm delete --purge ibmcloud-object-storage-plugin
      ```
      {: pre}

   3. Attieniti alla procedura in [Installazione del plug-in {{site.data.keyword.cos_full_notm}}](#install_cos) per installare la versione più recente del plug-in {{site.data.keyword.cos_full_notm}}.

2. Aggiorna il repository Helm di {{site.data.keyword.cloud_notm}} per richiamare la versione più recente di tutti i grafici Helm in questo repository.
   ```
   helm repo update
   ```
   {: pre}

3. Se utilizzi una distribuzione Linux oppure OS X, aggiorna il plug-in Helm {{site.data.keyword.cos_full_notm}} `ibmc` alla versione più recente.
   ```
   helm ibmc --update
   ```
   {: pre}

4. Scarica il grafico Helm {{site.data.keyword.cos_full_notm}} più recente sulla tua macchina locale ed estrai il pacchetto per esaminare il file `release.md` per trovare le informazioni sulla release più aggiornate.
   ```
   helm fetch --untar ibm-charts/ibm-object-storage-plugin
   ```
   {: pre}

5. Esegui l'upgrade del plug-in. </br>
   **Senza Tiller**:
   ```
   helm ibmc template ibm-charts/ibm-object-storage-plugin --update
   ```
   {: pre}

   **Con Tiller**:
   1. Trova il nome di installazione del tuo grafico Helm.
      ```
      helm ls | grep ibm-object-storage-plugin
      ```
      {: pre}

      Output di esempio:
      ```
      <helm_chart_name> 	1       	Mon Sep 18 15:31:40 2017	DEPLOYED	ibm-object-storage-plugin-1.0.5	default
      ```
      {: screen}

   2. Esegui l'upgrade del grafico Helm {{site.data.keyword.cos_full_notm}} alla versione più recente.
      ```   
      helm ibmc upgrade <helm_chart_name> ibm-charts/ibm-object-storage-plugin --force --recreate-pods -f
      ```
      {: pre}

6. Verifica che l'upgrade di `ibmcloud-object-storage-plugin` venga eseguito correttamente.  
   ```
   oc rollout status deployment/ibmcloud-object-storage-plugin -n kube-system
   ```
   {: pre}

   L'upgrade del plugin è riuscito quando vedi `deployment "ibmcloud-object-storage-plugin" successfully rolled out` nel tuo output della CLI.

7. Verifica che l'upgrade di `ibmcloud-object-storage-driver` venga eseguito correttamente.
   ```
   oc rollout status ds/ibmcloud-object-storage-driver -n kube-system
   ```
   {: pre}

   L'upgrade è riuscito quando vedi `daemon set "ibmcloud-object-storage-driver" successfully rolled out` nel tuo output della CLI.

8. Verifica che i pod {{site.data.keyword.cos_full_notm}} siano in uno stato `Running`.
   ```
   oc get pods -n kube-system -o wide | grep object-storage
   ```
   {: pre}


### Rimozione del plugin IBM Cloud Object Storage
{: #remove_cos_plugin}

Se non vuoi eseguire il provisioning di {{site.data.keyword.cos_full_notm}} e farne uso nel tuo cluster, puoi disinstallare il plug-in.
{: shortdesc}

La rimozione del plugin non rimuove PVC, PV o dati esistenti. Quando rimuovi il plugin, tutti i pod e le serie di daemon correlati vengono rimossi dal tuo cluster. Non puoi eseguire il provisioning di un nuovo {{site.data.keyword.cos_full_notm}} per il tuo cluster o utilizzare i PVC e i PV esistenti dopo che hai rimosso il plugin, a meno che tu non configuri l'applicazione per utilizzare l'API {{site.data.keyword.cos_full_notm}} direttamente.
{: important}

Prima di iniziare:

- [Indirizza la tua CLI al cluster](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure).
- Assicurati di non avere PVC o PV nel tuo cluster che utilizzano {{site.data.keyword.cos_full_notm}}. Per elencare tutti i pod che montano una specifica PVC, esegui `oc get pods --all-namespaces -o=jsonpath='{range .items[*]}{"\n"}{.metadata.name}{":\t"}{range .spec.volumes[*]}{.persistentVolumeClaim.claimName}{" "}{end}{end}' | grep "<pvc_name>"`.

Per rimuovere il plugin:

1. Rimuovi il plug-in dal tuo cluster: </br>
   **Con Tiller**:
   1. Trova il nome di installazione del tuo grafico Helm.
      ```
      helm ls | grep object-storage-plugin
      ```
      {: pre}

      Output di esempio:
      ```
      <helm_chart_name> 	1       	Mon Sep 18 15:31:40 2017	DEPLOYED	ibmcloud-object-storage-plugin-1.0.0	default
      ```
      {: screen}

   2. Elimina il plugin {{site.data.keyword.cos_full_notm}} rimuovendo il grafico Helm.
      ```
      helm delete --purge <helm_chart_name>
      ```
      {: pre}

   **Senza Tiller**:
   ```
   helm ibmc template ibm-charts/ibm-object-storage-plugin --delete
   ```
   {: pre}

2. Verifica che i pod {{site.data.keyword.cos_full_notm}} vengano rimossi.
   ```
   oc get pod -n kube-system | grep object-storage
   ```
   {: pre}

   La rimozione dei pod è riuscita se nel tuo output CLI non vengono visualizzati pod.

3. Verifica che le classi di archiviazione vengano rimosse.
   ```
   oc get storageclasses | grep s3
   ```
   {: pre}

   La rimozione delle classi di archiviazione è riuscita se nel tuo output CLI non vengono visualizzate classi di archiviazione.

4. Se utilizzi una distribuzione Linux oppure OS X, rimuovi il plugin Helm `ibmc`. Se utilizzi Windows, questo passo non è necessario.
   1. Rimuovi il plugin `ibmc`.
      ```
      rm -rf ~/.helm/plugins/helm-ibmc
      ```
      {: pre}

   2. Verifica che il plugin `ibmc` venga rimosso.
      ```
      helm plugin list
      ```
      {: pre}

      Output di esempio:
     ```
     NAME	VERSION	DESCRIPTION
     ```
     {: screen}

     Il plugin `ibmc` viene rimosso correttamente se il plugin `ibmc` non è elencato nel tuo output della CLI.


## Decisioni relative alla configurazione dell'archiviazione oggetti
{: #configure_cos}

{{site.data.keyword.containerlong_notm}} fornisce delle classi di archiviazione predefinite che puoi utilizzare per creare i bucket con una specifica configurazione.
{: shortdesc}

1. Elenca le classi di archiviazione disponibili in {{site.data.keyword.containerlong_notm}}.
   ```
   oc get storageclasses | grep s3
   ```
   {: pre}

   Output di esempio:
   ```
   ibmc-s3fs-cold-cross-region            ibm.io/ibmc-s3fs   8m
   ibmc-s3fs-cold-regional                ibm.io/ibmc-s3fs   8m
   ibmc-s3fs-flex-cross-region            ibm.io/ibmc-s3fs   8m
   ibmc-s3fs-flex-perf-cross-region       ibm.io/ibmc-s3fs   8m
   ibmc-s3fs-flex-perf-regional           ibm.io/ibmc-s3fs   8m
   ibmc-s3fs-flex-regional                ibm.io/ibmc-s3fs   8m
   ibmc-s3fs-standard-cross-region        ibm.io/ibmc-s3fs   8m
   ibmc-s3fs-standard-perf-cross-region   ibm.io/ibmc-s3fs   8m
   ibmc-s3fs-standard-perf-regional       ibm.io/ibmc-s3fs   8m
   ibmc-s3fs-standard-regional            ibm.io/ibmc-s3fs   8m
   ibmc-s3fs-vault-cross-region           ibm.io/ibmc-s3fs   8m
   ibmc-s3fs-vault-regional               ibm.io/ibmc-s3fs   8m
   ```
   {: screen}

2. Scegli una classe di archiviazione adatta ai tuoi requisiti di accesso ai dati. La classe di archiviazione determina i [prezzi ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://www.ibm.com/cloud-computing/bluemix/pricing-object-storage#s3api) per la capacità di archiviazione, le operazioni di lettura e scrittura e la larghezza di banda in uscita per un bucket. L'opzione corretta per te è basata sulla frequenza con cui i dati vengono letti e scritti nella tua istanza del servizio.
   - **Standard**: questa opzione è usata per i dati hot a cui si accede frequentemente. I casi d'uso comuni sono le applicazioni web o mobili.
   - **Vault**: questa opzione viene utilizzata per i carichi di lavoro o i dati cool a cui si accede poco di frequente, ad esempio una volta al mese o meno. I casi d'uso comuni sono gli archivi, la conservazione dei dati a breve termine, la conservazione di asset digitali, la sostituzione dei nastri e il ripristino d'emergenza.
   - **Cold**: questa opzione viene utilizzata per i dati cold a cui si accede raramente (ogni 90 giorni o meno) o i dati inattivi. I casi d'uso comuni sono gli archivi, i backup a lungo termine, i dati cronologici che conservi per la conformità oppure i carichi di lavoro e le applicazioni a cui si accede raramente.
   - **Flex**: questa opzione viene utilizzata per i carichi di lavoro e i dati che non seguono uno specifico modello di utilizzo o che sono troppo grandi per determinare o prevedere un modello di utilizzo. **Suggerimento:** controlla questo [blog ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://www.ibm.com/blogs/bluemix/2017/03/interconnect-2017-changing-rules-storage/) per capire come funziona la classe di archiviazione Flex rispetto ai livelli di archiviazione tradizionali.   

3. Decidi il livello di resilienza per i dati archiviati nel tuo bucket.
   - **Interregionale**: con questa opzione, i tuoi dati vengono archiviati tra tre regioni all'interno di una geolocalizzazione per la massima disponibilità. Se hai dei carichi di lavoro distribuiti tra le regioni, le richieste vengono instradate all'endpoint regionale più vicino. L'endpoint API per la geolocalizzazione viene impostato automaticamente dal plugin Helm `ibmc` che hai installato in precedenza in base all'ubicazione in cui si trova il tuo cluster. Ad esempio, se il tuo cluster si trova negli `Stati Uniti Sud`, le tue classi di archiviazione sono configurate per utilizzare l'endpoint API `US GEO` per i tuoi bucket. Per ulteriori informazioni, vedi [Regioni ed endpoint](/docs/services/cloud-object-storage/basics?topic=cloud-object-storage-endpoints#endpoints).  
   - **Regionale**: con questa opzione, i tuoi dati vengono replicati in più zone all'interno di una singola regione. Se hai dei carichi di lavoro che si trovano nella stessa regione, vedi una latenza più bassa e delle prestazioni migliori rispetto a una configurazione interregionale. L'endpoint regionale viene impostato automaticamente dal plugin Helm `ibm` che hai installato in precedenza in base all'ubicazione in cui si trova il tuo cluster. Ad esempio, se il tuo cluster si trova negli `Stati Uniti Sud`, le tue classi di archiviazione erano configurate per utilizzare `US South` come endpoint regionale per i tuoi bucket. Per ulteriori informazioni, vedi [Regioni ed endpoint](/docs/services/cloud-object-storage/basics?topic=cloud-object-storage-endpoints#endpoints).

4. Riesamina la configurazione del bucket {{site.data.keyword.cos_full_notm}} dettagliata per una classe di archiviazione.
   ```
   oc describe storageclass <storageclass_name>
   ```
   {: pre}

   Output di esempio:
   ```
   Name:                  ibmc-s3fs-standard-cross-region
   IsDefaultClass:        No
   Annotations:           <none>
   Provisioner:           ibm.io/ibmc-s3fs
   Parameters:            ibm.io/chunk-size-mb=16,ibm.io/curl-debug=false,ibm.io/debug-level=warn,ibm.io/iam-endpoint=https://iam.bluemix.net,ibm.io/kernel-cache=true,ibm.io/multireq-max=20,ibm.io/object-store-endpoint=https://s3-api.dal-us-geo.objectstorage.service.networklayer.com,ibm.io/object-store-storage-class=us-standard,ibm.io/parallel-count=2,ibm.io/s3fs-fuse-retry-count=5,ibm.io/stat-cache-size=100000,ibm.io/tls-cipher-suite=AESGCM
   AllowVolumeExpansion:  <unset>
   MountOptions:          <none>
   ReclaimPolicy:         Delete
   VolumeBindingMode:     Immediate
   Events:                <none>
   ```
   {: screen}

   <table>
   <caption>Descrizione dei dettagli delle classi di archiviazione</caption>
   <thead>
   <th colspan=2><img src="images/idea.png" alt="Icona Idea"/> Descrizione dei componenti del file YAML</th>
   </thead>
   <tbody>
   <tr>
   <td><code>ibm.io/chunk-size-mb</code></td>
   <td>La dimensione del blocco di dati letta da o scritta in {{site.data.keyword.cos_full_notm}}, espressa in megabyte. Le classi di archiviazione con <code>perf</code> nel loro nome sono configurate con 52 megabyte. Le classi di archiviazione senza <code>perf</code> nel loro nome utilizzano blocchi di 16 megabyte. Ad esempio, se vuoi leggere un file che è `1GB`, il plugin legge questo file in più blocchi da 16 o 52 megabyte. </td>
   </tr>
   <tr>
   <td><code>ibm.io/curl-debug</code></td>
   <td>Abilita la registrazione delle richieste inviate all'istanza del servizio {{site.data.keyword.cos_full_notm}}. Se abilitata, i log vengono inviati a `syslog` e puoi [inoltrare i log a un server di registrazione esterno](/docs/containers?topic=containers-health#logging). Per impostazione predefinita, tutte le classi di archiviazione sono impostate su <strong>false</strong> per disabilitare questa funzione di registrazione. </td>
   </tr>
   <tr>
   <td><code>ibm.io/debug-level</code></td>
   <td>Il livello di registrazione impostato dal plugin {{site.data.keyword.cos_full_notm}}. Tutte le classi di archiviazione sono configurate con il livello di registrazione <strong>WARN</strong>. </td>
   </tr>
   <tr>
   <td><code>ibm.io/iam-endpoint</code></td>
   <td>L'endpoint API per {{site.data.keyword.cloud_notm}} IAM (Identity and Access Management). </td>
   </tr>
   <tr>
   <td><code>ibm.io/kernel-cache</code></td>
   <td>Abilita o disabilita la cache del buffer del kernel per il punto di montaggio del volume. Se abilitata, i dati letti da {{site.data.keyword.cos_full_notm}} sono archiviati nella cache del kernel per garantire un accesso in lettura rapido ai tuoi dati. Se disabilitata, i dati non vengono memorizzati nella cache e sono sempre letti da {{site.data.keyword.cos_full_notm}}. La cache del kernel è abilitata per le classi di archiviazione <code>standard</code> e <code>flex</code> e disabilitata per le classi di archiviazione <code>cold</code> e <code>vault</code>. </td>
   </tr>
   <tr>
   <td><code>ibm.io/multireq-max</code></td>
   <td>Il numero massimo di richieste parallele che può essere inviato all'istanza del servizio {{site.data.keyword.cos_full_notm}} per elencare i file in una singola directory. Tutte le classi di archiviazione sono configurate con un massimo di 20 richieste parallele.  </td>
   </tr>
   <tr>
   <td><code>ibm.io/object-store-endpoint</code></td>
   <td>L'endpoint API da utilizzare per accedere al bucket nella tua istanza del servizio {{site.data.keyword.cos_full_notm}}. L'endpoint viene impostato automaticamente in base alla regione del tuo cluster. **Nota**: se vuoi accedere a un bucket esistente che si trova in una regione diversa rispetto a quella in cui si trova il tuo cluster, devi creare una [classe di archiviazione personalizzata](/docs/containers?topic=containers-kube_concepts#customized_storageclass) e utilizzare l'endpoint API per il tuo bucket.</td>
   </tr>
   <tr>
   <td><code>ibm.io/object-store-storage-class</code></td>
   <td>Il nome della classe di archiviazione. </td>
   </tr>
   <tr>
   <td><code>ibm.io/parallel-count</code></td>
   <td>Il numero massimo di richieste parallele che può essere inviato all'istanza del servizio {{site.data.keyword.cos_full_notm}} per una singola operazione di lettura o scrittura. Le classi di archiviazione con <code>perf</code> nel loro nome sono configurate con un massimo di 20 richieste parallele. Le classi di archiviazione senza <code>perf</code> sono configurate con due richieste parallele per impostazione predefinita.  </td>
   </tr>
   <tr>
   <td><code>ibm.io/s3fs-fuse-retry-count</code></td>
   <td>Il numero massimo di nuovi tentativi per un'operazione di lettura o scrittura prima che l'operazione venga considerata non riuscita. Tutte le classi di archiviazione sono configurate con un massimo di cinque nuovi tentativi.  </td>
   </tr>
   <tr>
   <td><code>ibm.io/stat-cache-size</code></td>
   <td>Il numero massimo di record conservato nella cache dei metadati {{site.data.keyword.cos_full_notm}}. Ogni record può richiedere fino a 0,5 kilobyte. Tutte le classi di archiviazione impostano il numero massimo di record a 100000 per impostazione predefinita. </td>
   </tr>
   <tr>
   <td><code>ibm.io/tls-cipher-suite</code></td>
   <td>La suite di cifratura TLS che deve essere utilizzata quando viene stabilita una connessione a {{site.data.keyword.cos_full_notm}} tramite l'endpoint HTTPS. Il valore per la suite di cifratura deve rispettare il [formato OpenSSL ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://www.openssl.org/docs/man1.0.2/apps/ciphers.html). Se i tuoi nodi di lavoro eseguono un sistema operativo Ubuntu, le tue classi di archiviazione sono configurate per utilizzare la suite di cifratura <strong><code>AESGCM</code></strong> per impostazione predefinita. Per i nodi di lavoro che eseguono un sistema operativo Red Hat, viene utilizzata per impostazione predefinita la suite di cifratura <strong><code>ecdhe_rsa_aes_128_gcm_sha_256</code></strong>.    </td>
   </tr>
   </tbody>
   </table>

   Per ulteriori informazioni su ciascuna classe di archiviazione, vedi la sezione di [riferimento delle classi di archiviazione](#cos_storageclass_reference). Se vuoi modificare qualche valore preimpostato, crea una tua [classe di archiviazione personalizzata](/docs/containers?topic=containers-kube_concepts#customized_storageclass).
   {: tip}

5. Decidi un nome per il tuo bucket. Il nome di un bucket deve essere univoco in {{site.data.keyword.cos_full_notm}}. Puoi anche scegliere di creare automaticamente un nome per il tuo bucket dal plugin {{site.data.keyword.cos_full_notm}}. Per organizzare i dati in un bucket, puoi creare delle sottodirectory.

   La classe di archiviazione che hai scelto in precedenza determina il prezzo per l'intero bucket. Non puoi definire delle classi di archiviazione differenti per le sottodirectory. Se vuoi archiviare i dati con requisiti di accesso differenti, considera la creazione di più bucket utilizzando più PVC.
   {: note}

6. Scegli se vuoi mantenere i tuoi dati e il bucket dopo l'eliminazione del cluster o dell'attestazione del volume persistente (o PVC, persistent volume claim). Quando elimini la PVC, il PV viene sempre eliminato. Puoi scegliere se vuoi anche eliminare automaticamente i dati e il bucket quando elimini la PVC. La tua istanza del servizio {{site.data.keyword.cos_full_notm}} è indipendente dalla politica di conservazione che selezioni per i tuoi dati e non viene mai rimossa quando elimini una PVC.

Ora che hai deciso in merito alla configurazione che desideri, sei pronto a [creare una PVC](#add_cos) per eseguire il provisioning di {{site.data.keyword.cos_full_notm}}.

## Aggiunta dell'archiviazione oggetti alle applicazioni
{: #add_cos}

Crea un'attestazione del volume persistente (o PVC, persistent volume claim) per eseguire il provisioning di {{site.data.keyword.cos_full_notm}} per il tuo cluster.
{: shortdesc}

A seconda delle impostazioni che scegli nella tua PVC, puoi eseguire il provisioning di {{site.data.keyword.cos_full_notm}} nei seguenti modi:
- [Provisioning dinamico](/docs/containers?topic=containers-kube_concepts#dynamic_provisioning): quando crei una PVC, il volume persistente (o PV, persistent volume) e il bucket nella tua istanza del servizio {{site.data.keyword.cos_full_notm}} vengono creati automaticamente.
- [Provisioning statico](/docs/containers?topic=containers-kube_concepts#static_provisioning): puoi fare riferimento a un bucket esistente nella tua istanza del servizio {{site.data.keyword.cos_full_notm}} nella tua PVC. Quando crei la PVC, il PV corrispondente viene automaticamente creato e collegato al tuo bucket esistente in {{site.data.keyword.cos_full_notm}}.

Prima di iniziare:
- [Crea e prepara la tua istanza del servizio {{site.data.keyword.cos_full_notm}}](#create_cos_service).
- [Crea un segreto per archiviare le tue credenziali del servizio {{site.data.keyword.cos_full_notm}}](#create_cos_secret).
- [Decidi in merito alla configurazione per il tuo {{site.data.keyword.cos_full_notm}}](#configure_cos).

Per aggiungere {{site.data.keyword.cos_full_notm}} al tuo cluster:

1. Crea un file di configurazione per definire la tua attestazione del volume persistente (o PVC, persistent volume claim).
   ```
   kind: PersistentVolumeClaim
   apiVersion: v1
   metadata:
     name: <pvc_name>
     namespace: <namespace>
     annotations:
       ibm.io/auto-create-bucket: "<true_or_false>"
       ibm.io/auto-delete-bucket: "<true_or_false>"
       ibm.io/bucket: "<bucket_name>"
       ibm.io/object-path: "<bucket_subdirectory>"
       ibm.io/secret-name: "<secret_name>"
       ibm.io/endpoint: "https://<s3fs_service_endpoint>"
   spec:
     accessModes:
       - ReadWriteOnce
     resources:
       requests:
         storage: 8Gi # Enter a fictitious value
     storageClassName: <storage_class>
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
   <td><code>metadata.namespace</code></td>
   <td>Immetti lo spazio dei nomi dove vuoi creare la PVC. La PVC deve essere creata nello stesso spazio dei nomi in cui hai creato il segreto Kubernetes per le tue credenziali del servizio {{site.data.keyword.cos_full_notm}} e dove vuoi eseguire il tuo pod. </td>
   </tr>
   <tr>
   <td><code>ibm.io/auto-create-bucket</code></td>
   <td>Scegli tra le seguenti opzioni: <ul><li><strong>true</strong>: quando crei la PVC, il PV e il bucket nella tua istanza del servizio {{site.data.keyword.cos_full_notm}} vengono creati automaticamente. Scegli questa opzione per creare un nuovo bucket nella tua istanza del servizio {{site.data.keyword.cos_full_notm}}. </li><li><strong>false</strong>: scegli questa opzione se vuoi accedere ai dati in un bucket esistente. Quando crei la PVC, il PV viene automaticamente creato e collegato al bucket che hai specificato in <code>ibm.io/bucket</code>.</td>
   </tr>
   <tr>
   <td><code>ibm.io/auto-delete-bucket</code></td>
   <td>Scegli tra le seguenti opzioni: <ul><li><strong>true</strong>: i tuoi dati, il bucket e il PV vengono automaticamente rimossi quando elimini la PVC. La tua istanza del servizio {{site.data.keyword.cos_full_notm}} rimane e non viene eliminata. Se scegli di impostare questa opzione su <strong>true</strong>, devi impostare <code>ibm.io/auto-create-bucket: true</code> e <code>ibm.io/bucket: ""</code> in modo che il tuo bucket venga creato automaticamente con un nome con il formato <code>tmp-s3fs-xxxx</code>. </li><li><strong>false</strong>: quando elimini la PVC, il PV viene eliminato automaticamente ma i tuoi dati e il bucket nella tua istanza del servizio {{site.data.keyword.cos_full_notm}} rimangono. Per accedere ai tuoi dati, devi creare un nuovo PVC con il nome del tuo bucket esistente. </li></ul>
   <tr>
   <td><code>ibm.io/bucket</code></td>
   <td>Scegli tra le seguenti opzioni: <ul><li>Se <code>ibm.io/auto-create-bucket</code> è impostata su <strong>true</strong>: immetti il nome del bucket che vuoi creare in {{site.data.keyword.cos_full_notm}}. Se, inoltre, <code>ibm.io/auto-delete-bucket</code> è impostata su <strong>true</strong>, devi lasciare questo campo vuoto per assegnare automaticamente un nome al tuo bucket con il formato <code>tmp-s3fs-xxxx</code>. Il nome deve essere univoco in {{site.data.keyword.cos_full_notm}}. </li><li>Se <code>ibm.io/auto-create-bucket</code> è impostata su <strong>false</strong>: immetti il nome del bucket esistente a cui vuoi accedere nel cluster. </li></ul> </td>
   </tr>
   <tr>
   <td><code>ibm.io/object-path</code></td>
   <td>Facoltativo; immetti il nome della sottodirectory esistente nel tuo bucket che vuoi montare. Utilizza questa opzione se vuoi montare solo una sottodirectory e non l'intero bucket. Per montare una sottodirectory, devi impostare <code>ibm.io/auto-create-bucket: "false"</code> e fornire il nome del bucket in <code>ibm.io/bucket</code>. </li></ul> </td>
   </tr>
   <tr>
   <td><code>ibm.io/secret-name</code></td>
   <td>Immetti il nome del segreto che contiene le credenziali {{site.data.keyword.cos_full_notm}} che hai creato in precedenza. </td>
   </tr>
   <tr>
  <td><code>ibm.io/endpoint</code></td>
  <td>Se hai creato la tua istanza del servizio {{site.data.keyword.cos_full_notm}} in un'ubicazione diversa dal tuo cluster, immetti l'endpoint del servizio privato o pubblico della tua istanza del servizio {{site.data.keyword.cos_full_notm}} che vuoi utilizzare. Per una panoramica degli endpoint del servizio disponibili, vedi [Ulteriori informazioni sull'endpoint](/docs/services/cloud-object-storage?topic=cloud-object-storage-advanced-endpoints). Per impostazione predefinita, il plug-in Helm <code>ibmc</code> richiama automaticamente la tua ubicazione del cluster e crea le classi di archiviazione utilizzando l'endpoint del servizio privato {{site.data.keyword.cos_full_notm}} che corrisponde alla tua ubicazione del cluster. Se il cluster si trova in una delle zone di città metropolitana, come ad esempio `dal10`, viene utilizzato l'endpoint del servizio privato {{site.data.keyword.cos_full_notm}} per la città metropolitana, in questo caso Dallas. Per verificare che l'endpoint del servizio nelle tue classi di archiviazione corrisponda all'endpoint del servizio della tua istanza del servizio, esegui `oc describe storageclass <storageclassname>`. Assicurati di immettere il tuo endpoint del servizio nel formato `https://<s3fs_private_service_endpoint>` per gli endpoint del servizio privati oppure `http://<s3fs_public_service_endpoint>` per gli endpoint del servizio pubblici. Se l'endpoint del servizio nella tua classe di archiviazione corrisponde all'endpoint del servizio della tua istanza del servizio {{site.data.keyword.cos_full_notm}}, non includere l'opzione <code>ibm.io/endpoint</code> nel file YAML della tua PVC. </td>
  </tr>
   <tr>
   <td><code>resources.requests.storage</code></td>
   <td>Una dimensione fittizia per il tuo bucket {{site.data.keyword.cos_full_notm}} in gigabyte. La dimensione è richiesta da Kubernetes, ma non è rispettata in {{site.data.keyword.cos_full_notm}}. Puoi immettere qualsiasi dimensione vuoi. Lo spazio effettivo che usi in {{site.data.keyword.cos_full_notm}} potrebbe essere diverso ed è fatturato in base alla [tabella dei prezzi ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://www.ibm.com/cloud-computing/bluemix/pricing-object-storage#s3api). </td>
   </tr>
   <tr>
   <td><code>spec.storageClassName</code></td>
   <td>Scegli tra le seguenti opzioni: <ul><li>Se <code>ibm.io/auto-create-bucket</code> è impostata su <strong>true</strong>: immetti la classe di archiviazione che vuoi utilizzare per il tuo nuovo bucket. </li><li>Se <code>ibm.io/auto-create-bucket</code> è impostato su <strong>false</strong>: immetti la classe di archiviazione che hai utilizzato per creare il tuo bucket esistente. </br></br>Se hai creato manualmente il bucket nella tua istanza del servizio {{site.data.keyword.cos_full_notm}} oppure non riesci a ricordare la classe di archiviazione che hai utilizzato, trova la tua istanza del servizio nel dashboard {{site.data.keyword.Bluemix}} e controlla <strong>Classe</strong> e <strong>Ubicazione</strong> del tuo bucket esistente. Usa quindi una [classe di archiviazione](#cos_storageclass_reference) appropriata. <p class="note">L'endpoint API {{site.data.keyword.cos_full_notm}} impostato nella tua classe di archiviazione è basato sulla regione in cui si trova il tuo cluster. Se vuoi accedere a un bucket che si trova in una regione diversa da quella in cui si trova il tuo cluster, devi creare una [classe di archiviazione personalizzata](/docs/containers?topic=containers-kube_concepts#customized_storageclass) e utilizzare l'endpoint API appropriato per il tuo bucket.</p></li></ul>  </td>
   </tr>
   </tbody>
   </table>

2. Crea la PVC.
   ```
   oc apply -f filepath/pvc.yaml
   ```
   {: pre}

3. Verifica che la tua PVC sia stata creata e associata al PV.
   ```
   oc get pvc
   ```
   {: pre}

   Output di esempio:
   ```
   NAME                  STATUS    VOLUME                                     CAPACITY   ACCESS MODES   STORAGECLASS                     AGE
   s3fs-test-pvc         Bound     pvc-b38b30f9-1234-11e8-ad2b-t910456jbe12   8Gi        RWO            ibmc-s3fs-standard-cross-region  1h
   ```
   {: screen}

4. Facoltativo: se intendi accedere ai tuoi dati con un utente non root o se hai aggiunto dei file a un bucket {{site.data.keyword.cos_full_notm}} esistente utilizzando direttamente la console o l'API, assicurati che ai [file sia assegnata l'autorizzazione corretta](/docs/containers?topic=containers-cs_troubleshoot_storage#cos_nonroot_access) in modo che la tua applicazione possa leggere e aggiornare correttamente i file secondo necessità.

4.  {: #cos_app_volume_mount}Per montare il PV nella tua distribuzione, crea un file `.yaml` di configurazione e specifica la PVC che esegue il bind del PV.

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
            securityContext:
              runAsUser: <non_root_user>
              fsGroup: <non_root_user> #only applicable for clusters that run Kubernetes version 1.13 or later
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
    <td><code>spec.containers.securityContext.runAsUser</code></td>
    <td>Facoltativo: per eseguire l'applicazione con un utente non root in un cluster che esegue Kubernetes versione 1.12 o antecedenti, specifica il [contesto di sicurezza ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://kubernetes.io/docs/tasks/configure-pod-container/security-context/) per il tuo pod definendo l'utente non root senza impostare al tempo stesso `fsGroup` nel tuo YAML di distribuzione. L'impostazione di `fsGroup` attiva il plugin {{site.data.keyword.cos_full_notm}} per aggiornare le autorizzazioni del gruppo per tutti i file in un bucket quando viene distribuito il pod. L'aggiornamento delle autorizzazioni è un'operazione di scrittura e influisce sulle prestazioni. A seconda del numero di file che hai, l'aggiornamento delle autorizzazioni potrebbe impedire al tuo pod di avviarsi e di passare a uno stato di <code>Running</code>. </br></br>Se hai un cluster che esegue Kubernetes versione 1.13 o successive e il plugin {{site.data.keyword.cloud_notm}} Object Storage versione 1.0.4 o successive, puoi modificare il proprietario del punto di montaggio s3fs. Per modificare il proprietario, specifica il contesto di sicurezza impostando `runAsUser` e `fsGroup` sullo stesso ID utente non root che desideri possieda il punto di montaggio s3fs. Se questi due valori non corrispondono, il punto di montaggio appartiene automaticamente all'utente `root`.  </td>
    </tr>
    <tr>
    <td><code>spec.containers.volumeMounts.mountPath</code></td>
    <td>Il percorso assoluto della directory in cui viene montato il volume nel contenitore. Se vuoi condividere un volume tra diverse applicazioni, puoi specificare i [percorsi secondari di volume ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://kubernetes.io/docs/concepts/storage/volumes/#using-subpath) per ciascuna delle tue applicazioni.</td>
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

7. Verifica che puoi scrivere dati nella tua istanza del servizio {{site.data.keyword.cos_full_notm}}.
   1. Accedi al pod che monta il tuo PV.
      ```
      oc exec <pod_name> -it bash
      ```
      {: pre}

   2. Vai al tuo percorso di montaggio del volume che hai definito nella distribuzione della tua applicazione.
   3. Crea un file di testo.
      ```
      echo "This is a test" > test.txt
      ```
      {: pre}

   4. Dal dashboard {{site.data.keyword.Bluemix}}, vai alla tua istanza del servizio {{site.data.keyword.cos_full_notm}}.
   5. Dal menu, seleziona **Bucket**.
   6. Apri il tuo bucket e verifica che puoi vedere il `test.txt` che hai creato.


## Utilizzo dell'archiviazione oggetti in una serie con stato
{: #cos_statefulset}

Se hai un'applicazione con stato, come ad esempio un database, puoi creare delle serie con stato che utilizzano {{site.data.keyword.cos_full_notm}} per memorizzare i dati della tua applicazione. In alternativa, puoi utilizzare un DBaaS (database-as-a-service) {{site.data.keyword.cloud_notm}}, come {{site.data.keyword.cloudant_short_notm}}, e memorizzare i tuoi dati sul cloud.
{: shortdesc}

Prima di iniziare:
- [Crea e prepara la tua istanza del servizio {{site.data.keyword.cos_full_notm}}](#create_cos_service).
- [Crea un segreto per archiviare le tue credenziali del servizio {{site.data.keyword.cos_full_notm}}](#create_cos_secret).
- [Decidi in merito alla configurazione per il tuo {{site.data.keyword.cos_full_notm}}](#configure_cos).

Per distribuire una serie con stato che utilizza l'archiviazione oggetti:

1. Crea un file di configurazione per la tua serie con stato e il servizio che utilizzi per esporre la serie con stato. I seguenti esempi mostrano come distribuire NGINX come una serie con stato con tre repliche, ciascuna delle quali con un bucket separato o condividendo lo stesso bucket.

   **Esempio per creare una serie con stato con tre repliche, dove ogni replica utilizza un bucket separato**:
   ```
   apiVersion: v1
   kind: Service
   metadata:
     name: nginx-v01
     namespace: default
     labels:
       app: nginx-v01 # must match spec.template.metadata.labels and spec.selector.matchLabels in stateful set YAML
   spec:
     ports:
     - port: 80
       name: web
     clusterIP: None
     selector:
       app: nginx-v01 # must match spec.template.metadata.labels and spec.selector.matchLabels in stateful set YAML
   ---
   apiVersion: apps/v1
   kind: StatefulSet
   metadata:
     name: web-v01
     namespace: default
   spec:
     selector:
       matchLabels:
         app: nginx-v01 # must match spec.template.metadata.labels in stateful set YAML and metadata.labels in service YAML
     serviceName: "nginx-v01"
     replicas: 3 
     template:
       metadata:
         labels:
           app: nginx-v01 # must match spec.selector.matchLabels in stateful set YAML and metadata.labels in service YAML
       spec:
         terminationGracePeriodSeconds: 10
         containers:
         - name: nginx
           image: k8s.gcr.io/nginx-slim:0.8
           ports:
           - containerPort: 80
             name: web
           volumeMounts:
           - name: mypvc
             mountPath: /usr/share/nginx/html
     volumeClaimTemplates:
     - metadata:
         name: mypvc
         annotations:
           ibm.io/auto-create-bucket: "true"
           ibm.io/auto-delete-bucket: "true"
           ibm.io/bucket: ""
           ibm.io/secret-name: mysecret 
           volume.beta.kubernetes.io/storage-class: ibmc-s3fs-standard-perf-cross-region 
           volume.beta.kubernetes.io/storage-provisioner: ibm.io/ibmc-s3fs
       spec:
         accessModes: [ "ReadWriteOnce" ]
         storageClassName: "ibmc-s3fs-standard-perf-cross-region"
         resources:
           requests:
             storage: 1Gi
   ```
   {: codeblock}

   **Esempio per creare una serie con stato con tre repliche che condividono lo stesso bucket `mybucket`**:
   ```
   apiVersion: v1
   kind: Service
   metadata:
     name: nginx-v01
     namespace: default
     labels:
       app: nginx-v01 # must match spec.template.metadata.labels and spec.selector.matchLabels in stateful set YAML
   spec:
     ports:
     - port: 80
       name: web
     clusterIP: None
     selector:
       app: nginx-v01 # must match spec.template.metadata.labels and spec.selector.matchLabels in stateful set YAML
   --- 
   apiVersion: apps/v1
   kind: StatefulSet
   metadata:
     name: web-v01
     namespace: default
   spec:
     selector:
       matchLabels:
         app: nginx-v01 # must match spec.template.metadata.labels in stateful set YAML and metadata.labels in service YAML
     serviceName: "nginx-v01"
     replicas: 3 
     template:
       metadata:
         labels:
           app: nginx-v01 # must match spec.selector.matchLabels in stateful set YAML and metadata.labels in service YAML
       spec:
         terminationGracePeriodSeconds: 10
         containers:
         - name: nginx
           image: k8s.gcr.io/nginx-slim:0.8
           ports:
           - containerPort: 80
             name: web
           volumeMounts:
           - name: mypvc
             mountPath: /usr/share/nginx/html
     volumeClaimTemplates:
     - metadata:
         name: mypvc
         annotations:
           ibm.io/auto-create-bucket: "false"
           ibm.io/auto-delete-bucket: "false"
           ibm.io/bucket: mybucket
           ibm.io/secret-name: mysecret
           volume.beta.kubernetes.io/storage-class: ibmc-s3fs-standard-perf-cross-region 
           volume.beta.kubernetes.io/storage-provisioner: ibm.io/ibmc-s3fs
       spec:
         accessModes: [ "ReadOnlyMany" ]
         storageClassName: "ibmc-s3fs-standard-perf-cross-region"
         resources:
           requests:
             storage: 1Gi
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
    <td style="text-align:left"><code>spec.selector.matchLabels</code></td>
    <td style="text-align:left">Immetti tutte le etichette che vuoi includere nella serie con stato e nella PVC. Le etichette che includi nella sezione <code>volumeClaimTemplates</code> della tua serie con stato non vengono riconosciute da Kubernetes. Devi invece definire queste etichette nella sezione <code>spec.selector.matchLabels</code> e <code>spec.template.metadata.labels</code> del file YAML della serie con stato. Per assicurarti che tutte le repliche della serie con stato vengano incluse nel bilanciamento del carico del tuo servizio, includi la stessa etichetta che hai usato nella sezione <code>spec.selector</code> del file YAML del servizio. </td>
    </tr>
    <tr>
    <td style="text-align:left"><code>spec.template.metadata.labels</code></td>
    <td style="text-align:left">Immetti le stesse etichette che hai aggiunto alla sezione <code>spec.selector.matchLabels</code> del tuo file YAML della serie con stato. </td>
    </tr>
    <tr>
    <td><code>spec.template.spec.</code></br><code>terminationGracePeriodSeconds</code></td>
    <td>Immetti il numero di secondi per consentire a <code>kubelet</code> di terminare correttamente il pod che esegue la replica della serie con stato. Per ulteriori informazioni, vedi [Delete Pods ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://kubernetes.io/docs/tasks/run-application/force-delete-stateful-set-pod/#delete-pods). </td>
    </tr>
    <tr>
    <td style="text-align:left"><code>spec.volumeClaimTemplates.</code></br><code>metadata.name</code></td>
    <td style="text-align:left">Immetti un nome per il tuo volume. Utilizza lo stesso nome che hai definito nella sezione <code>spec.containers.volumeMount.name</code>. Il nome che immetti qui viene utilizzato per creare il nome della tua PVC nel formato: <code>&lt;volume_name&gt;-&lt;statefulset_name&gt;-&lt;replica_number&gt;</code>. </td>
    </tr>
    <tr>
    <td><code>spec.volumeClaimTemplates.metadata</code></br><code>annotions.ibm.io/auto-create-bucket</code></td>
    <td>Scegli tra le seguenti opzioni: <ul><li><strong>true: </strong>scegli questa opzione per creare automaticamente un bucket per ogni replica della serie con stato. </li><li><strong>false: </strong>scegli questa opzione se vuoi condividere un bucket esistente tra le repliche della tua serie con stato. Assicurati di definire il nome del bucket nella sezione <code>spec.volumeClaimTemplates.metadata.annotions.ibm.io/bucket</code> del tuo file YAML della serie con stato.</li></ul></td>
    </tr>
    <tr>
    <td><code>spec.volumeClaimTemplates.metadata</code></br><code>annotions.ibm.io/auto-delete-bucket</code></td>
    <td>Scegli tra le seguenti opzioni: <ul><li><strong>true: </strong>i tuoi dati, il bucket e il PV vengono automaticamente rimossi quando elimini la PVC. La tua istanza del servizio {{site.data.keyword.cos_full_notm}} rimane e non viene eliminata. Se scegli di impostare questa opzione su true, devi impostare <code>ibm.io/auto-create-bucket: true</code> e <code>ibm.io/bucket: ""</code> in modo che il tuo bucket venga creato automaticamente con un nome con il formato <code>tmp-s3fs-xxxx</code>. </li><li><strong>false: </strong>quando elimini la PVC, il PV viene eliminato automaticamente ma i tuoi dati e il bucket nella tua istanza del servizio {{site.data.keyword.cos_full_notm}} rimangono. Per accedere ai tuoi dati, devi creare un nuovo PVC con il nome del tuo bucket esistente.</li></ul></td>
    </tr>
    <tr>
    <td><code>spec.volumeClaimTemplates.metadata</code></br><code>annotions.ibm.io/bucket</code></td>
    <td>Scegli tra le seguenti opzioni: <ul><li><strong>Se <code>ibm.io/auto-create-bucket</code> è impostato su true: </strong>immetti il nome del bucket che vuoi creare in {{site.data.keyword.cos_full_notm}}. Se anche <code>ibm.io/auto-delete-bucket</code> è impostato su <strong>true</strong>, devi lasciare questo campo vuoto per assegnare automaticamente un nome al tuo bucket con il formato tmp-s3fs-xxxx. Il nome deve essere univoco in {{site.data.keyword.cos_full_notm}}.</li><li><strong>Se <code>ibm.io/auto-create-bucket</code> è impostato su false: </strong>immetti il nome del bucket esistente a cui vuoi accedere nel cluster.</li></ul></td>
    </tr>
    <tr>
    <td><code>spec.volumeClaimTemplates.metadata</code></br><code>annotions.ibm.io/secret-name</code></td>
    <td>Immetti il nome del segreto che contiene le credenziali {{site.data.keyword.cos_full_notm}} che hai creato in precedenza.</td>
    </tr>
    <tr>
    <td style="text-align:left"><code>spec.volumeClaimTemplates.metadata.</code></br><code>annotations.volume.beta.</code></br><code>kubernetes.io/storage-class</code></td>
    <td style="text-align:left">Immetti la classe di archiviazione che vuoi utilizzare. Scegli tra le seguenti opzioni: <ul><li><strong>Se <code>ibm.io/auto-create-bucket</code> è impostato su true: </strong>immetti la classe di archiviazione che vuoi utilizzare per il tuo nuovo bucket.</li><li><strong>Se <code>ibm.io/auto-create-bucket</code> è impostato su false: </strong>immetti la classe di archiviazione che hai utilizzato per creare il tuo bucket esistente. </li></ul></br>  Per elencare le classi di archiviazione esistenti, esegui <code>oc get storageclasses | grep s3</code>. Se non specifichi alcuna classe di archiviazione, la PVC viene creata con la classe di archiviazione predefinita impostata nel tuo cluster. Assicurati che la classe di archiviazione predefinita utilizzi il provisioner <code>ibm.io/ibmc-s3fs</code> in modo che la tua serie con stato venga fornita con l'archiviazione oggetti.</td>
    </tr>
    <tr>
    <td style="text-align:left"><code>spec.volumeClaimTemplates.</code></br><code>spec.storageClassName</code></td>
    <td>Immetti la stessa classe di archiviazione che hai immesso nella sezione <code>spec.volumeClaimTemplates.metadata.annotations.volume.beta.kubernetes.io/storage-class</code> del tuo file YAML della serie con stato.  </td>
    </tr>
    <tr>
    <td style="text-align:left"><code>spec.volumeClaimTemplates.spec.</code></br><code>resource.requests.storage</code></td>
    <td>Immetti una dimensione fittizia per il tuo bucket {{site.data.keyword.cos_full_notm}} in gigabyte. La dimensione è richiesta da Kubernetes, ma non è rispettata in {{site.data.keyword.cos_full_notm}}. Puoi immettere qualsiasi dimensione vuoi. Lo spazio effettivo che usi in {{site.data.keyword.cos_full_notm}} potrebbe essere diverso ed è fatturato in base alla [tabella dei prezzi ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://www.ibm.com/cloud-computing/bluemix/pricing-object-storage#s3api).</td>
    </tr>
    </tbody></table>


## Backup e ripristino di dati
{: #cos_backup_restore}

{{site.data.keyword.cos_full_notm}} è configurato per fornire un'elevata durabilità per i tuoi dati per offrire loro una protezione da eventuali perdite. Puoi trovare la SLA nei [termini del servizio {{site.data.keyword.cos_full_notm}} ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://www-03.ibm.com/software/sla/sladb.nsf/sla/bm-7857-03).
{: shortdesc}

{{site.data.keyword.cos_full_notm}} non fornisce una cronologia delle versioni per i tuoi dati. Se devi mantenere e accedere a versioni meno recenti dei tuoi dati, devi configurare l'applicazione per gestire la cronologia dei dati o implementare delle soluzioni di backup alternative. Ad esempio, potresti voler archiviare i tuoi dati {{site.data.keyword.cos_full_notm}} nel tuo database in locale oppure utilizzare i nastri per archiviare i tuoi dati.
{: note}

## Riferimento delle classi di archiviazione
{: #cos_storageclass_reference}

### Standard
{: #standard}

<table>
<caption>Classe di archiviazione oggetti: standard</caption>
<thead>
<th>Caratteristiche</th>
<th>Impostazione</th>
</thead>
<tbody>
<tr>
<td>Nome</td>
<td><code>ibmc-s3fs-standard-cross-region</code></br><code>ibmc-s3fs-standard-perf-cross-region</code></br><code>ibmc-s3fs-standard-regional</code></br><code>ibmc-s3fs-standard-perf-regional</code></td>
</tr>
<tr>
<td>Endpoint di resilienza predefinito</td>
<td>L'endpoint di resilienza viene impostato automaticamente in base all'ubicazione in cui si trova il cluster. Per ulteriori informazioni, vedi [Regioni ed endpoint](/docs/services/cloud-object-storage/basics?topic=cloud-object-storage-endpoints#endpoints). </td>
</tr>
<tr>
<td>Dimensione blocco</td>
<td>Classe di archiviazione senza `perf`: 16 MB</br>Classe di archiviazione con `perf`: 52 MB</td>
</tr>
<tr>
<td>Cache kernel</td>
<td>Abilitata</td>
</tr>
<tr>
<td>Fatturazione</td>
<td>Mensile</td>
</tr>
<tr>
<td>Prezzi</td>
<td>[Prezzi ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://www.ibm.com/cloud-computing/bluemix/pricing-object-storage#s3api)</td>
</tr>
</tbody>
</table>

### Vault
{: #Vault}

<table>
<caption>Classe di archiviazione oggetti: vault</caption>
<thead>
<th>Caratteristiche</th>
<th>Impostazione</th>
</thead>
<tbody>
<tr>
<td>Nome</td>
<td><code>ibmc-s3fs-vault-cross-region</code></br><code>ibmc-s3fs-vault-regional</code></td>
</tr>
<tr>
<td>Endpoint di resilienza predefinito</td>
<td>L'endpoint di resilienza viene impostato automaticamente in base all'ubicazione in cui si trova il cluster. Per ulteriori informazioni, vedi [Regioni ed endpoint](/docs/services/cloud-object-storage/basics?topic=cloud-object-storage-endpoints#endpoints). </td>
</tr>
<tr>
<td>Dimensione blocco</td>
<td>16 MB</td>
</tr>
<tr>
<td>Cache kernel</td>
<td>Disabilitata</td>
</tr>
<tr>
<td>Fatturazione</td>
<td>Mensile</td>
</tr>
<tr>
<td>Prezzi</td>
<td>[Prezzi ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://www.ibm.com/cloud-computing/bluemix/pricing-object-storage#s3api)</td>
</tr>
</tbody>
</table>

### Cold
{: #cold}

<table>
<caption>Classe di archiviazione oggetti: cold</caption>
<thead>
<th>Caratteristiche</th>
<th>Impostazione</th>
</thead>
<tbody>
<tr>
<td>Nome</td>
<td><code>ibmc-s3fs-flex-cross-region</code></br><code>ibmc-s3fs-flex-perf-cross-region</code></br><code>ibmc-s3fs-flex-regional</code></br><code>ibmc-s3fs-flex-perf-regional</code></td>
</tr>
<tr>
<td>Endpoint di resilienza predefinito</td>
<td>L'endpoint di resilienza viene impostato automaticamente in base all'ubicazione in cui si trova il cluster. Per ulteriori informazioni, vedi [Regioni ed endpoint](/docs/services/cloud-object-storage/basics?topic=cloud-object-storage-endpoints#endpoints). </td>
</tr>
<tr>
<td>Dimensione blocco</td>
<td>16 MB</td>
</tr>
<tr>
<td>Cache kernel</td>
<td>Disabilitata</td>
</tr>
<tr>
<td>Fatturazione</td>
<td>Mensile</td>
</tr>
<tr>
<td>Prezzi</td>
<td>[Prezzi ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://www.ibm.com/cloud-computing/bluemix/pricing-object-storage#s3api)</td>
</tr>
</tbody>
</table>

### Flex
{: #flex}

<table>
<caption>Classe di archiviazione oggetti: flex</caption>
<thead>
<th>Caratteristiche</th>
<th>Impostazione</th>
</thead>
<tbody>
<tr>
<td>Nome</td>
<td><code>ibmc-s3fs-cold-cross-region</code></br><code>ibmc-s3fs-flex-perf-cross-region</code></br><code>ibmc-s3fs-cold-regional</code></br><code>ibmc-s3fs-flex-perf-regional</code></td>
</tr>
<tr>
<td>Endpoint di resilienza predefinito</td>
<td>L'endpoint di resilienza viene impostato automaticamente in base all'ubicazione in cui si trova il cluster. Per ulteriori informazioni, vedi [Regioni ed endpoint](/docs/services/cloud-object-storage/basics?topic=cloud-object-storage-endpoints#endpoints). </td>
</tr>
<tr>
<td>Dimensione blocco</td>
<td>Classe di archiviazione senza `perf`: 16 MB</br>Classe di archiviazione con `perf`: 52 MB</td>
</tr>
<tr>
<td>Cache kernel</td>
<td>Abilitata</td>
</tr>
<tr>
<td>Fatturazione</td>
<td>Mensile</td>
</tr>
<tr>
<td>Prezzi</td>
<td>[Prezzi ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://www.ibm.com/cloud-computing/bluemix/pricing-object-storage#s3api)</td>
</tr>
</tbody>
</table>


