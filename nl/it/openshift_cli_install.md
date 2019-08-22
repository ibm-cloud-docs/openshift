---

copyright:
  years: 2014, 2019
lastupdated: "2019-07-31"

keywords: openshift, roks, rhoks, rhos, oc

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
{:download: .download}
{:preview: .preview}

# Installazione della CLI Red Hat OpenShift Container Platform 
{: #openshift-cli}

Puoi utilizzare l'alias del plugin della CLI {{site.data.keyword.containerlong}} per OpenShift (`ibmcloud oc`) per creare e gestire la tua infrastruttura del cluster OpenShift, ad esempio creando cluster e nodi di lavoro. Puoi quindi utilizzare la CLI OpenShift (`oc`) per gestire le risorse all'interno del tuo cluster OpenShift, come ad esempio progetti, pod e distribuzioni. 

## Installazione dei plugin e della CLI IBM Cloud
{: #cli_ibmcloud_oc}

Vedi l'argomento nella [documentazione di {{site.data.keyword.containerlong_notm}}](/docs/containers?topic=containers-cs_cli_install#cs_cli_install_steps) per installare le seguenti CLI.
{: shortdesc}

* CLI {{site.data.keyword.cloud_notm}} (`ibmcloud`)
* Plugin {{site.data.keyword.containershort_notm}} (alias `ibmcloud oc` per i cluster OpenShift)
* Plugin Container Registry (`ibmcloud cr`)

<br />


## Installazione della CLI OpenShift Origin (`oc`)
{: #cli_oc}

Per visualizzare una versione locale del dashboard OpenShift e per distribuire le applicazioni nei tuoi cluster Red Hat OpenShift on IBM Cloud, installa la CLI OpenShift Origin (`oc`). La CLI `oc` include una versione corrispondente della CLI Kubernetes (`kubectl`). Per ulteriori informazioni, vedi la [documentazione di OpenShift ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://docs.openshift.com/container-platform/3.11/cli_reference/get_started_cli.html).
{: shortdesc}

Stai utilizzando sia cluster OpenShift che Kubernetes della community? La CLI `oc` viene fornita con entrambi i file binari `oc` e `kubectl` ma i tuoi cluster differenti potrebbero eseguire versioni differenti di Kubernetes, come ad esempio 1.11 su OpenShift e 1.13.8 su Ubuntu. Assicurati di utilizzare il file binario `kubectl` che corrisponde alla versione Kubernetes `major.minor` del tuo cluster.
{: note}

1.  [Scarica la CLI OpenShift Origin ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://www.okd.io/download.html) per la tua versione OpenShift e il tuo sistema operativo locali. La versione OpenShift predefinita corrente è 3.11.

2.  Se utilizzi Mac OS o Linux, completa la seguente procedura per aggiungere i file binari alla tua variabile di sistema `PATH`. Se utilizzi Windows, installa la CLI `oc` nella stessa directory della CLI {{site.data.keyword.cloud_notm}}. Questa configurazione ti consente di ridurre le modifiche al percorso file quando esegui i comandi in un secondo momento.
    1.  Sposta i file eseguibili `oc` e `kubectl` nella directory `/usr/local/bin`.
        ```
        mv /<filepath>/oc /usr/local/bin/oc && mv /<filepath>/kubectl /usr/local/bin/kubectl
        ```
        {: pre}

    2.  Assicurati che `/usr/local/bin` sia elencato nella tua variabile di sistema `PATH`. La variabile `PATH` contiene tutte le directory in cui il tuo sistema operativo può trovare i file eseguibili. Le directory elencate nella variabile `PATH` servono a diversi scopi. `/usr/local/bin` viene utilizzata per memorizzare i file eseguibili per il software che non fa parte del sistema operativo e che viene installato manualmente dall'amministratore di sistema.
        ```
        echo $PATH
        ```
        {: pre}
        Output CLI di esempio:
        ```
        /usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin
        ```
        {: screen}
3.  Se hai dei cluster che eseguono versioni differenti di Kubernetes, come ad esempio un cluster OpenShift con la versione 1.11 e un cluster Kubernetes della community con la versione 1.15.1, scarica ciascun file binario di versione `kubectl` in una directory separata.
    1.  Elimina il file binario `kubectl` fornito con l'installazione di `oc` poiché questa versione di `kubectl` non funziona con i cluster Kubernetes della community.
        ```
        rm /usr/local/bin/kubectl
        ```
        {: pre}
    2.  [Scarica i file binari `kubectl` separati](/docs/containers?topic=containers-cs_cli_install#kubectl) che corrispondono alle versioni dei tuoi cluster OpenShift e Kubernetes della community.
    3.  **Facoltativo**: configura un alias nel tuo profilo del terminale locale per puntare a file binari separati che corrispondono alla versione di `kubectl` di cui ha bisogno il tuo cluster.
4.  **Facoltativo**: [abilita il completamento automatico per i comandi `kubectl` ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://kubernetes.io/docs/tasks/tools/install-kubectl/#enabling-shell-autocompletion). La procedura varia a seconda della shell che utilizzi. Puoi ripetere la procedura per abilitare il completamento automatico per i comandi `oc`. Ad esempio, in bash su Linux, invece di `kubectl completion bash >/etc/bash_completion.d/kubectl`, puoi eseguire `oc completion bash >/etc/bash_completion.d/oc_completion`.

Avvia quindi [Creazione di un cluster Red Hat OpenShift on IBM Cloud](/docs/openshift?topic=openshift-openshift_tutorial).

Per ulteriori informazioni sulla CLI OpenShift Origin, vedi la [documentazione dei comandi `oc`![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://docs.openshift.com/container-platform/3.11/cli_reference/basic_cli_operations.html).
{: note}


<br />


## Accesso a un cluster OpenShift dagli strumenti del terminale o dell'automazione
{: #openshift_cluster_login}

Red Hat OpenShift on IBM Cloud è integrato con {{site.data.keyword.cloud_notm}} IAM (Identity and Access Management). Con IAM, puoi autenticare gli utenti e i servizi utilizzando le loro identità IAM e autorizzare azioni con ruoli e politiche di accesso. Quando esegui l'autenticazione come utente tramite la console OpenShift, la tua identità IAM viene utilizzata per generare un token di accesso OpenShift che puoi utilizzare per accedere al terminale. Puoi automatizzare l'accesso al tuo cluster creando una chiave API IAM da utilizzare per il comando `oc login`.
{:shortdesc}

**Prima di iniziare**:
* [Installa la CLI `oc`](#cli_oc).
* [Crea un cluster OpenShift](/docs/openshift?topic=openshift-openshift-create-cluster).
* Controlla che il tuo cluster sia in uno stato integro eseguendo `ibmcloud oc cluster-get --cluster <cluster_name_or_ID>`. Se il tuo cluster non è in uno stato integro, riesamina la guida [Debug dei cluster](/docs/containers?topic=containers-cs_troubleshoot) per assistenza. Ad esempio, se il provisioning del tuo cluster viene eseguito in un account che è protetto da un dispositivo gateway firewall, devi [configurare le impostazioni del tuo firewall per consentire il traffico in uscita alle porte e agli indirizzi IP appropriati](/docs/openshift?topic=containers-firewall).

**Per accedere al tuo cluster come utente attraverso il terminale**:
1.  Nella console [{{site.data.keyword.containerlong_notm}} ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://cloud.ibm.com/kubernetes/clusters?platformType=openshift), fai clic sul cluster a cui vuoi accedere.
2.  Fai clic sulla scheda **Access** e attieniti alle istruzioni.

<br>
**Per automatizzare l'accesso al tuo cluster con una chiave API**:
1.  Crea una chiave API {{site.data.keyword.cloud_notm}}.<p class="important">Salva la tua chiave API in un'ubicazione sicura. Non puoi richiamare nuovamente la chiave API. Se vuoi esportare l'output in un file sulla tua macchina locale, includi l'indicatore `--file <path>/<file_name>`.</p>
    ```
    ibmcloud iam api-key-create <name>
    ```
    {: pre}
2.  Ottieni l'**URL master** del cluster a cui desideri accedere.
    ```
    ibmcloud oc cluster-get --cluster <cluster_name_or_ID>
    ```
    {: pre}
3.  Utilizza la chiave API e l'URL cluster per accedere al tuo cluster OpenShift. Il nome utente (`-u`) è `apikey`, la password (`-p`) è il tuo valore di chiave API e `--server` è l'URL del master cluster.
    ```
    oc login -u apikey -p <API_key> --server=<master_URL>
    ```
    {: pre}

    Puoi anche utilizzare una chiamata API per scambiare le tue credenziali {{site.data.keyword.cloud_notm}} IAM per un token OpenShift. Per ulteriori informazioni, vedi la [documentazione di OpenShift ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://docs.openshift.com/container-platform/3.11/architecture/additional_concepts/authentication.html#obtaining-oauth-tokens).

    Richiesta curl di esempio:
    ```
    curl -u 'apikey:<API_key>' -H "X-CSRF-Token: a" 'https://<master_URL>:<port>/oauth/authorize?client_id=openshift-challenging-client&response_type=token' -vvv
    ```
    {: pre}


