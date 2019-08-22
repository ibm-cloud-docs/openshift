---

copyright:
  years: 2014, 2019
lastupdated: "2019-07-31"

keywords: openshift, roks, rhoks, rhos, clusters

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

# Creazione di cluster OpenShift
{: #openshift-create-cluster}

Crea un cluster {{site.data.keyword.openshiftlong}} in {{site.data.keyword.containerlong_notm}}.
{: shortdesc}

## Prerequisiti
{: #openshift_cluster_prereqs}

Per creare i cluster OpenShift, completa la seguente procedura prerequisita.

1.  [Prepara il tuo account a creare i cluster](/docs/containers?topic=containers-clusters#cluster_prepare). Questo passo include la creazione di un account fatturabile, la configurazione di una chiave API con le autorizzazioni dell'infrastruttura, assicurandoti di disporre dell'accesso di Amministratore in {{site.data.keyword.cloud_notm}} IAM, la pianificazione dei gruppi di risorse e la configurazione della rete di account.
2.  [Preparati a creare i cluster](/docs/containers?topic=containers-clusters#prepare_cluster_level). Questo passo include il pianificare la configurazione del cluster, lo stimare i costi e il consentire il traffico di rete attraverso un firewall. <p class="note">I cluster OpenShift sono disponibili [solo come cluster standard, non gratuito](/docs/openshift?topic=openshift-faqs#openshift_free).</p>
3.   [Installa le CLI {{site.data.keyword.cloud_notm}} e OpenShift](/docs/openshift?topic=openshift-openshift-cli).

<br />


## Creazione di un cluster con la console
{: #openshift_create_cluster_console}

Crea un cluster OpenShift standard nella console {{site.data.keyword.containerlong_notm}}.
{: shortdesc}

Prima di iniziare, [completa i prerequisiti](#openshift_cluster_prereqs).

1.  Crea un cluster.
    1.  Accedi al tuo [account {{site.data.keyword.cloud_notm}} ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://cloud.ibm.com/).
    2.  Dal menu a tre linee ![icona di menu a tre linee](../icons/icon_hamburger.svg "icona di menu a tre linee"), seleziona **OpenShift** e fai clic su **Create cluster**.
    3.  Scegli i dettagli di configurazione e il nome per il tuo cluster.
    *   Compila i tuoi nome cluster, gruppo di risorse e tag.
    *   Per l'ubicazione (**Location**), imposta l'area geografica (**Geography**) e seleziona quindi una qualsiasi delle sei [ubicazioni ](/docs/openshift?topic=openshift-regions-and-zones) di area metropolitana (**Metro**) multizona in tutto il mondo da utilizzare per le tue zone di lavoro (**Worker zones**).
    *   Per **Default worker pool**, scegli un profilo disponibile per i tuoi nodi di lavoro. Red Hat OpenShift on IBM Cloud supporta solo OpenShift versione 3.11, che include Kubernetes versione 1.11. Il sistema operativo è Red Hat Enterprise Linux 7.
    1.  Per finire, fai clic su **Create cluster**.<p class="note">Il completamento del processo di creazione del tuo cluster potrebbe richiedere alcuni minuti. Una volta che lo stato del cluster diventa **Normal**, i componenti di rete e di bilanciamento del carico del cluster impiegano circa altri 10 minuti per distribuire e aggiornare il dominio cluster che utilizzi per la console web OpenShift e per altri instradamenti. Attendi che il cluster sia pronto prima di proseguire con il passo successivo controllando che il **dominio secondario Ingress** segua un modello di `<cluster_name>.<region>.containers.appdomain.cloud`.<br><br>Se il tuo cluster non raggiunge uno stato di **deployed**, consulta la guida [Debug dei cluster](/docs/containers?topic=containers-cs_troubleshoot) per assistenza. Ad esempio, se il provisioning del tuo cluster viene eseguito in un account che è protetto da un dispositivo gateway firewall, devi [configurare le impostazioni del tuo firewall per consentire il traffico in uscita alle porte e agli indirizzi IP appropriati](/docs/openshift?topic=containers-firewall).</p>
2.  Dalla pagina dei dettagli del cluster, fai clic su **OpenShift web console**. Per ulteriori informazioni sull'utilizzo della console OpenShift, vedi la [documentazione di OpenShift ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://docs.openshift.com/container-platform/3.11/getting_started/developers_console.html).
3.  Per continuare a lavorare nel terminale, dal menu della console web OpenShift, fai clic sul tuo profilo **IAM#user.name@email.com > Copy Login Command**. Incolla nel tuo terminale il comando di login `oc` copiato per eseguire l'autenticazione tramite la CLI.

<br />


## Creazione di un cluster con la CLI
{: #openshift_create_cluster_cli}

Crea un cluster OpenShift standard utilizzando la CLI {{site.data.keyword.cloud_notm}}.
{: shortdesc}

Prima di iniziare, [completa i prerequisiti](#openshift_cluster_prereqs).

1.  Accedi all'account che hai configurato per creare i cluster OpenShift. Indica come destinazione la regione **us-east** o quella **eu-gb** e il gruppo di risorse. Se hai un account federato, includi l'indicatore `--sso`.
    ```
    ibmcloud login -r (us-east|eu-gb) [-g default] [--sso]
    ```
    {: pre}
2.  Crea un cluster.
    ```
    ibmcloud oc cluster-create --name <name> --location <zone> --kube-version <openshift_version> --machine-type <worker_node_flavor> --workers <number_of_worker_nodes_per_zone> --public-vlan <public_VLAN_ID> --private-vlan <private_VLAN_ID>
    ```
    {: pre}

    Comando di esempio per creare un cluster con tre nodi di lavoro che hanno quattro core e 16 GB di memoria a Washington, DC:

    ```
    ibmcloud oc cluster-create --name my_openshift --location wdc04 --kube-version 3.11_openshift --machine-type b3c.4x16.encrypted  --workers 3 --public-vlan <public_VLAN_ID> --private-vlan <private_VLAN_ID>
    ```
    {: pre}

    <table summary="La prima riga nella tabella si estende su entrambe le colonne. Le restanti righe devono essere lette da sinistra a destra, con i componenti del comando nella colonna uno e la descrizione corrispondente nella colonna due.">
    <caption>Componenti di cluster-create</caption>
    <thead>
    <th colspan=2><img src="images/idea.png" alt="Icona Idea"/> Descrizione dei componenti di questo comando</th>
    </thead>
    <tbody>
    <tr>
    <td><code>cluster-create</code></td>
    <td>Il comando per creare un cluster dell'infrastruttura classica nel tuo account {{site.data.keyword.cloud_notm}}.</td>
    </tr>
    <tr>
    <td><code>--name <em>&lt;name&gt;</em></code></td>
    <td>Immetti un nome per il tuo cluster. Il nome deve iniziare con una lettera, può contenere lettere, numeri e trattini (-) e non può contenere più di 35 caratteri. Utilizza un nome che sia univoco tra tutte le regioni {{site.data.keyword.cloud_notm}}.</td>
    </tr>
    <tr>
    <td><code>--location <em>&lt;zone&gt;</em></code></td>
    <td>Specifica la zona in cui vuoi creare il cluster. Per un elenco di zone supportate, vedi [Ubicazioni multizona](/docs/openshift?topic=openshift-regions-and-zones#zones).</p></td>
    </tr>
    <tr>
      <td><code>--kube-version <em>&lt;openshift_version&gt;</em></code></td>
      <td>Devi scegliere una versione OpenShift supportata. Le versioni OpenShift includono una versione di Kubernetes che differisce dalle versioni Kubernetes disponibili sui cluster Ubuntu Kubernetes della community. Per elencare le versioni OpenShift disponibili, esegui `ibmcloud oc versions`. Per creare un cluster con la versione patch più recente, puoi specificare solo la versione principale e secondaria, ad esempio ` 3.11_openshift`.<br><br>Red Hat OpenShift on IBM Cloud supporta solo OpenShift versione 3.11, che include Kubernetes versione 1.11. Il sistema operativo è Red Hat Enterprise Linux 7.</td>
    </tr>
    <tr>
    <td><code>--machine-type <em>&lt;worker_node_flavor&gt;</em></code></td>
    <td>Scegli un tipo di macchina, o un profilo, per i tuoi nodi di lavoro. Puoi distribuire i tuoi nodi di lavoro come macchine virtuali su hardware condiviso o dedicato o come macchine fisiche su bare metal. I tipi di macchine fisiche e virtuali disponibili variano in base alla zona in cui distribuisci il cluster. Per elencare i profili disponibili, esegui `ibmcloud oc flavors --zone <zone>`.</td>
    </tr>
    <tr>
    <td><code>--workers <em>&lt;number_of_worker_nodes_per_zone&gt;</em></code></td>
    <td>Il numero di nodi di lavoro da includere nel cluster. Potresti voler specificare almeno tre nodi di lavoro in modo che il tuo cluster disponga di risorse sufficienti per eseguire i componenti predefiniti e per l'alta disponibilità. Se non viene specificata l'opzione <code>--workers</code>, viene creato un nodo di lavoro.</td>
    </tr>
    <tr>
    <td><code>--public-vlan <em>&lt;public_vlan_id&gt;</em></code></td>
    <td>Se hai già una VLAN pubblica configurata nel tuo account dell'infrastruttura IBM Cloud per quella zona, immetti l'ID della VLAN pubblica. Per controllare le VLAN disponibili, esegui `ibmcloud oc vlans --zone <zone>`. <br><br>Se non hai una VLAN pubblica nel tuo account, non specificare questa opzione. {{site.data.keyword.containerlong_notm}} crea automaticamente una VLAN pubblica per tuo conto.</td>
    </tr>
    <tr>
    <td><code>--private-vlan <em>&lt;private_vlan_id&gt;</em></code></td>
    <td>Se hai già una VLAN privata configurata nel tuo account dell'infrastruttura IBM Cloud per quella zona, immetti l'ID della VLAN privata. Per controllare le VLAN disponibili, esegui `ibmcloud oc vlans --zone <zone>`. <br><br>Se non hai una VLAN privata nel tuo account, non specificare questa opzione. {{site.data.keyword.containerlong_notm}} crea automaticamente una VLAN privata per te.</td>
    </tr>
    </tbody></table>
3.  Elenca i dettagli del tuo cluster. Esamina lo **Stato** del cluster, controlla il **Dominio secondario Ingress** e prendi nota dell'**URL master**.<p class="note">Il completamento del processo di creazione del tuo cluster potrebbe richiedere alcuni minuti. Una volta che lo stato del cluster diventa **Normal**, i componenti di rete e di bilanciamento del carico del cluster impiegano circa altri 10 minuti per distribuire e aggiornare il dominio cluster che utilizzi per la console web OpenShift e per altri instradamenti. Attendi che il cluster sia pronto prima di proseguire con il passo successivo controllando che il **Dominio secondario Ingress** segua un modello di `<cluster_name>.<region>.containers.appdomain.cloud`.<br><br>Il tuo cluster non è in uno stato **deployed**? controlla la guida [Debug dei cluster](/docs/containers?topic=containers-cs_troubleshoot) per un aiuto. Ad esempio, se il provisioning del tuo cluster viene eseguito in un account che è protetto da un dispositivo gateway firewall, devi [configurare le impostazioni del tuo firewall per consentire il traffico in uscita alle porte e agli indirizzi IP appropriati](/docs/openshift?topic=containers-firewall).</p>

    ```
    ibmcloud oc cluster-get --cluster <cluster_name_or_ID>
    ```
    {: pre}

4.  Scarica i file di configurazione per connetterti al tuo cluster.
    ```
    ibmcloud oc cluster-config --cluster <cluster_name_or_ID>
    ```
    {: pre}

    Al termine del download dei file di configurazione, viene visualizzato un comando che puoi copiare e incollare per impostare il percorso del file di configurazione Kubernetes locale come variabile di ambiente.

    Esempio per OS X:

    ```
    export KUBECONFIG=/Users/<user_name>/.bluemix/plugins/kubernetes-service/clusters/<cluster_name>/kube-config-<datacenter>-<cluster_name>.yml
    ```
    {: screen}
5.  Nel tuo browser, passa all'indirizzo del tuo **URL master URL** e aggiungi `/console`. Ad esempio, `https://c0.containers.cloud.ibm.com:23652/console`.
6.  Dalla barra dei menu della console web OpenShift, fai clic sul tuo profilo **IAM#user.name@email.com > Copy Login Command**. Incolla nel tuo terminale il comando di login `oc` copiato per eseguire l'autenticazione tramite la CLI.<p class="tip">Salva l'URL master del tuo cluster per accedere successivamente alla console OpenShift. Nelle sessioni future, puoi saltare il passo `cluster-config` e copiare invece il comando di login dalla console.</p>
7.  Verifica che i comandi `oc` vengano eseguiti correttamente con il tuo cluster controllando la versione.

    ```
    oc version
    ```
    {: pre}

    Output di esempio:

    ```
    oc v3.11.0+0cbc58b
    kubernetes v1.11.0+d4cacc0
    features: Basic-Auth

    Server https://c0.containers.cloud.ibm.com:23652
    openshift v3.11.98
    kubernetes v1.11.0+d4cacc0
    ```
    {: screen}

<br />


## Passi successivi
{: #next_steps}

Quando il cluster è attivo e in esecuzione, puoi controllare le seguenti attività:
- Se hai creato il cluster in una zona con supporto multizona, [estendi i nodi di lavoro aggiungendo una zona al tuo cluster](/docs/openshift?topic=containers-add_workers).
- [Distribuisci un'applicazione nel tuo cluster](/docs/containers?topic=openshift-openshift_apps).
- [Esponi le tue applicazioni con gli instradamenti](/docs/openshift?topic=openshift-openshift_routes).
