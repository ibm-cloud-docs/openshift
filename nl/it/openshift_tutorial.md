---

copyright:
  years: 2014, 2019
lastupdated: "2019-07-31"

keywords: kubernetes, iks, oks, iro, openshift, red hat, red hat openshift, rhos, roks, rhoks

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
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}

# Esercitazione: Creazione di un cluster Red Hat OpenShift on IBM Cloud
{: #openshift_tutorial}

Con Red Hat OpenShift on IBM Cloud, puoi creare cluster {{site.data.keyword.containerlong_notm}} con nodi di lavoro che vengono installati con il software di orchestrazione Red Hat OpenShift on IBM Cloud Container Platform  Ottieni tutti i [vantaggi del servizio {{site.data.keyword.containerlong_notm}}gestito](/docs/containers?topic=containers-responsibilities_iks) per l'ambiente della tua infrastruttura cluster, mentre utilizzi gli [strumenti e il catalogo OpenShift ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://docs.openshift.com/container-platform/3.11/welcome/index.html) eseguiti su Red Hat Enterprise Linux per le tue distribuzioni dell'applicazione.
{: shortdesc}

I nodi di lavoro OpenShift sono disponibili solo per gli account a pagamento e i cluster standard. Red Hat OpenShift on IBM Cloud supporta solo OpenShift versione 3.11, che include Kubernetes versione 1.11. Il sistema operativo è Red Hat Enterprise Linux 7.
{: note}


## Obiettivi
{: #openshift_objectives}

Nelle lezioni dell'esercitazione, crei un cluster Red Hat OpenShift on IBM Cloud standard, apri la console OpenShift, accedi ai componenti OpenShift integrati, distribuisci un'applicazione che utilizza i servizi {{site.data.keyword.cloud_notm}} in un progetto OpenShift ed esponi l'applicazione su un instradamento OpenShift in modo che gli utenti esterni possano accedere al servizio.
{: shortdesc}

<img src="/images/roks_tutorial.png" width="600" alt="Diagramma dell'esercitazione OpenShift" style="width:600px; border-style: none"/>

## Tempo richiesto
{: #openshift_time}
45 minuti

## Destinatari
{: #openshift_audience}

Questa esercitazione è rivolta agli amministratori del cluster che vogliono imparare come creare un cluster Red Hat OpenShift on IBM Cloud per la prima volta.
{: shortdesc}

## Prerequisiti
{: #openshift_prereqs}

*   Assicurati di disporre delle seguenti politiche di accesso {{site.data.keyword.cloud_notm}} IAM.
    *   Il [ruolo della piattaforma **Amministratore**](/docs/containers?topic=containers-users#platform) per {{site.data.keyword.containerlong_notm}}
    *   Il [ruolo del servizio **Scrittore** o **Gestore**](/docs/containers?topic=containers-users#platform) per {{site.data.keyword.containerlong_notm}}
    *   Il [ruolo della piattaforma **Amministratore**](/docs/containers?topic=containers-users#platform) per {{site.data.keyword.registrylong_notm}}
*    Assicurati che la [chiave API](/docs/containers?topic=containers-users#api_key) per la regione e il gruppo di risorse {{site.data.keyword.cloud_notm}} sia configurata con le autorizzazioni dell'infrastruttura corrette, **Super utente**, o con i [ruoli minimi](/docs/containers?topic=containers-access_reference#infra) per creare un cluster.

<br />


## Lezione 1: Creazione di un cluster Red Hat OpenShift on IBM Cloud
{: #openshift_create_cluster}

Crea un cluster Red Hat OpenShift on IBM Cloud in {{site.data.keyword.containerlong_notm}}. Per informazioni su quali componenti vengono configurati quando crei un cluster, vedi l'[Architettura del servizio](/docs/openshift?topic=openshift-openshift-service-arch). OpenShift è disponibile solo per i cluster standard. Puoi trovare ulteriori informazioni sul prezzo dei cluster standard nelle [domande frequenti (FAQ)](/docs/openshift?topic=openshift-faqs#charges).
{:shortdesc}

1.  Installa gli strumenti di riga di comando.
    *   [Installa la CLI {{site.data.keyword.cloud_notm}} (`ibmcloud`), il plugin {{site.data.keyword.containershort_notm}} (`ibmcloud oc`) e il plugin {{site.data.keyword.registryshort_notm}} (`ibmcloud cr`)](/docs/containers?topic=containers-cs_cli_install#cs_cli_install_steps).
    *   [Installa le CLI OpenShift Origin (`oc`) e Kubernetes (`kubectl`)](/docs/containers?topic=containers-cs_cli_install#cli_oc).
2.  Accedi all'account che hai configurato per creare i cluster OpenShift. Indica come destinazione la regione **us-east** o quella **eu-gb** e il gruppo di risorse. Se hai un account federato, includi l'indicatore `--sso`.
    ```
    ibmcloud login -r (us-east|eu-gb) [-g default] [--sso]
    ```
    {: pre}
3.  Crea un cluster. Il seguente comando crea un cluster con tre nodi di lavoro che hanno quattro core e 16 GB di memoria a Washington, DC. Se hai delle VLAN esistenti che vuoi utilizzare, ottieni gli ID VLAN eseguendo `ibmcloud oc vlans --zone <zone>`.
    ```
    ibmcloud oc cluster-create --name my_openshift --location wdc04 --kube-version 3.11_openshift --machine-type b3c.4x16.encrypted  --workers 3 --public-vlan <public_VLAN_ID> --private-vlan <private_VLAN_ID>
    ```
    {: pre}
4.  Elenca i dettagli del tuo cluster. Esamina lo **Stato** del cluster, controlla il **Dominio secondario Ingress** e prendi nota dell'**URL master**.<p class="note">Il completamento del processo di creazione del tuo cluster potrebbe richiedere alcuni minuti. Una volta che lo stato del cluster diventa **Normal**, i componenti di rete e di bilanciamento del carico del cluster impiegano circa altri 10 minuti per distribuire e aggiornare il dominio cluster che utilizzi per la console web OpenShift e per altri instradamenti. Attendi che il cluster sia pronto prima di proseguire con il passo successivo controllando che il **Dominio secondario Ingress** segua un modello di `<cluster_name>.<region>.containers.appdomain.cloud`.</p>
    ```
    ibmcloud oc cluster-get --cluster <cluster_name_or_ID>
    ```
    {: pre}
5.  Scarica i file di configurazione per connetterti al tuo cluster.
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
6.  Nel tuo browser, passa all'indirizzo del tuo **URL master URL** e aggiungi `/console`. Ad esempio, `https://c0.containers.cloud.ibm.com:23652/console`.
7.  Dalla barra dei menu della console web OpenShift, fai clic sul tuo profilo **IAM#user.name@email.com > Copy Login Command**. Incolla nel tuo terminale il comando di login `oc` copiato per eseguire l'autenticazione tramite la CLI.<p class="tip">Salva l'URL master del tuo cluster per accedere successivamente alla console OpenShift. Nelle sessioni future, puoi saltare il passo `cluster-config` e copiare invece il comando di login dalla console.</p>
8.  Verifica che i comandi `oc` vengano eseguiti correttamente con il tuo cluster controllando la versione.

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

    Se non puoi eseguire operazioni che richiedono le autorizzazioni di Amministratore, come elencare tutti i nodi di lavoro o i pod in un cluster, scarica i certificati TLS e i file di autorizzazione per l'amministratore del cluster eseguendo il comando `ibmcloud oc cluster-config --cluster <cluster_name_or_ID> --admin`.
    {: tip}

<br />


## Lezione 2: Navigazione della console OpenShift
{: #openshift_oc_console}

Red Hat OpenShift on IBM Cloud viene fornito con dei servizi integrati che puoi utilizzare per gestire il tuo cluster, come ad esempio la console OpenShift.
{:shortdesc}

1.  Dalla console [{{site.data.keyword.containerlong_notm}} clusters ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://cloud.ibm.com/kubernetes/clusters?platformType=openshift), seleziona il tuo cluster OpenShift e fai quindi clic su **OpenShift web console**.
2.  Esplora le diverse aree della console OpenShift facendo clic sul menu a discesa nella barra dei menu **OpenShift Container Platform**.
    * **Service Catalog**: sfoglia il catalogo di servizi integrati che puoi distribuire su OpenShift. Ad esempio, se già hai un'applicazione `node.js` ospitata in GitHub, puoi fare clic sulla scheda **Languages** e distribuire un'applicazione **JavaScript**. Il riquadro **My Projects** fornisce una vista rapida di tutti i progetti a cui hai accesso e, facendo clic su un progetto, passi alla Application Console.
    * **Application Console**: per ogni spazio dei nomi di progetto a cui hai accesso, puoi gestire e visualizzare i log per le tue risorse OpenShift come ad esempio i pod, i servizi, gli instradamenti, le build, le immagini o le attestazioni di volumi persistenti. Puoi anche aggiungere servizi dal catalogo al progetto.
    * **Cluster Console**: per gli amministratori a livello di cluster in tutti i progetti nel cluster, puoi gestire progetti, account di servizio, ruoli RBAC, bind di ruolo e quote di risorse. Puoi anche visualizzare le viste combinate dello stato e degli eventi delle risorse all'interno del cluster.
3.  Per continuare a lavorare con il tuo cluster nel terminale, dalla Service Console o dalla Application Console, fai clic sul tuo profilo **IAM#user.name@email.com > Copy Login Command**. Incolla nel tuo terminale il comando di login `oc` copiato per eseguire l'autenticazione tramite la CLI.

<br />


## Lezione 3: Distribuzione di un'applicazione al tuo cluster OpenShift
{: #openshift_deploy_app}

Con Red Hat OpenShift on IBM Cloud, puoi creare una nuova applicazione ed esporre il tuo servizio dell'applicazione tramite un router OpenShift per consentirne l'utilizzo ad utenti esterni.
{: shortdesc}

Se hai fatto una pausa dall'ultima lezione e hai avviato un nuovo terminale, assicurati di accedere di nuovo al tuo cluster. Apri la tua console web OpenShift all'indirizzo `https://<master_URL>/console`. Ad esempio, `https://c0.containers.cloud.ibm.com:23652/console`. Quindi, dalla barra dei menu, fai clic sul tuo profilo **IAM#user.name@email.com > Copy Login Command** e incolla il comando di accesso `oc` copiato nel tuo terminale per eseguire l'autenticazione tramite la CLI.
{: tip}

1.  Crea un progetto per la tua applicazione Hello World. Un progetto è una versione OpenShift di uno spazio dei nomi Kubernetes con annotazioni aggiuntive.
    ```
    oc new-project hello-world
    ```
    {: pre}
2.  Crea l'applicazione di esempio [dal codice sorgente ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://github.com/IBM/container-service-getting-started-wt). Con il comando OpenShift `new-app`, puoi fare riferimento a una directory in un repository remoto che contiene il Dockerfile e il codice dell'applicazione per creare la tua immagine. Il comando crea l'immagine, la archivia nel registro Docker locale e crea le configurazioni di distribuzione dell'applicazione (`dc`) e i servizi (`svc`). Per ulteriori informazioni sulla creazione di nuove applicazioni, [consulta la documentazione OpenShift ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://docs.openshift.com/container-platform/3.11/dev_guide/application_lifecycle/new_app.html).
    ```
    oc new-app --name hello-world https://github.com/IBM/container-service-getting-started-wt --context-dir="Lab 1"
    ```
    {: pre}
3.  Verifica che i componenti dell'applicazione Hello World di esempio siano stato creati.
    1.  Elenca i servizi **hello-world** e prendi nota del nome servizio. La tua applicazione resta in ascolto del traffico su questi indirizzi IP interni del cluster a meno che non crei un instradamento per il servizio in modo che il router possa inoltrare le richieste di traffico esterno all'applicazione.
        ```
        oc get svc -n hello-world
        ```
        {: pre}

        Output di esempio:
        ```
        NAME          TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)    AGE
        hello-world   ClusterIP   172.21.xxx.xxx   <nones>       8080/TCP   31m
        ```
        {: screen}
    2.  Elenca i pod. I pod che hanno `build` nel nome sono lavori che sono stati **completati** come parte de processo di build della nuova applicazione. Assicura che lo stato del pod **hello-world** sia **Running**.
        ```
        oc get pods -n hello-world
        ```
        {: pre}

        Output di esempio:
        ```
        NAME                READY     STATUS             RESTARTS   AGE
        hello-world-9cv7d   1/1       Running            0          30m
        hello-world-build   0/1       Completed          0          31m
        ```
        {: screen}
4.  Configura un instradamento in modo che tu possa accedere pubblicamente al servizio hello world. Per impostazione predefinita, il nome host è in formato `<service_name>-<namespace>.<cluster_name>-<random_ID>.<region>.containers.appdomain.cloud`. Se vuoi personalizzare il nome host, includi l'indicatore `--hostname=<hostname>`.
    1.  Crea un instradamento per il servizio **hello-world**.
        ```
        oc create route edge --service=hello-world -n hello-world
        ```
        {: pre}
    2.  Ottieni l'indirizzo del nome host di instradamento dall'output **Host/Port**.
        ```
        oc get route -n hello-world
        ```
        {: pre}
        Output di esempio:
        ```
        NAME          HOST/PORT                         PATH                                        SERVICES      PORT       TERMINATION   WILDCARD
        hello-world   hello-world-hello.world.<cluster_name>-<random_ID>.<region>.containers.appdomain.cloud    hello-world   8080-tcp   edge/Allow    None
        ```
        {: screen}
5.  Accedi alla tua applicazione. Assicurati di accodare `https://` al tuo nome host di instradamento.
    ```
    curl https://hello-world-hello-world.<cluster_name>-<random_ID>.<region>.containers.appdomain.cloud
    ```
    {: pre}

    Output di esempio:
    ```
    Hello world da hello-world-9cv7d! La tua applicazione è attiva e in esecuzione in un cluster!
    ```
    {: screen}
6.  **Facoltativo** Per ripulire le risorse che hai creato in questa lezione, puoi utilizzare le etichette assegnate a ciascuna applicazione.
    1.  Elenca tutte le risorse per ogni applicazione nel progetto `hello-world`.
        ```
        oc get all -l app=hello-world -o name -n hello-world
        ```
        {: pre}
        Output di esempio:
        ```
        pod/hello-world-1-dh2ff
        replicationcontroller/hello-world-1
        service/hello-world
        deploymentconfig.apps.openshift.io/hello-world
        buildconfig.build.openshift.io/hello-world
        build.build.openshift.io/hello-world-1
        imagestream.image.openshift.io/hello-world
        imagestream.image.openshift.io/node
        route.route.openshift.io/hello-world
        ```
        {: screen}
    2.  Elimina tutte le risorse che hai creato.
        ```
        oc delete all -l app=hello-world -n hello-world
        ```
        {: pre}



<br />


## Operazioni successive
{: #openshift_next}

Per ulteriori informazioni su come lavorare con le tue applicazioni e i tuoi servizi di instradamento, vedi la [Guida per sviluppatori OpenShift](https://docs.openshift.com/container-platform/3.11/dev_guide/index.html).

Installa due diffusi componenti aggiuntivi {{site.data.keyword.containerlong_notm}}: [{{site.data.keyword.la_full_notm}}](/docs/openshift?topic=openshift-openshift_health#openshift_logdna) e [{{site.data.keyword.mon_full_notm}}](/docs/openshift?topic=openshift-openshift_health#openshift_sysdig).
