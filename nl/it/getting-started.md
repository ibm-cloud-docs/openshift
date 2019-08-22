---

copyright:
  years: 2014, 2019
lastupdated: "2019-07-31"

keywords: openshift, containers, clusters, roks, rhoks, rhos

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

# Introduzione a Red Hat OpenShift on IBM Cloud
{: #getting-started}

Con Red Hat OpenShift on IBM Cloud, puoi creare cluster {{site.data.keyword.containerlong_notm}} con nodi di lavoro che vengono installati con il software di orchestrazione Red Hat OpenShift on IBM Cloud Container Platform  Ottieni tutti i [vantaggi del servizio {{site.data.keyword.containerlong_notm}}gestito](/docs/containers?topic=containers-responsibilities_iks) per l'ambiente della tua infrastruttura cluster, mentre utilizzi gli [strumenti e il catalogo OpenShift ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://docs.openshift.com/container-platform/3.11/welcome/index.html) eseguiti su Red Hat Enterprise Linux per le tue distribuzioni dell'applicazione.
{: shortdesc}

Per completare l'esercitazione introduttiva, utilizza un account {{site.data.keyword.cloud_notm}} Pagamento a consumo, in cui sei il proprietario o disponi di privilegi di Amministratore completi. Questa esercitazione introduttiva si concentra sulla configurazione di un cluster e un'applicazione di esempio rapidamente utilizzando la console {{site.data.keyword.cloud_notm}}. Per ulteriori informazioni su come utilizzare la CLI per creare il tuo cluster OpenShift e distribuire un'applicazione, consulta questa [esercitazione](/docs/openshift?topic=openshift-openshift_tutorial).

## Creazione di un cluster OpenShift
{: #openshift_gs_cluster}

Crea un cluster Red Hat OpenShift on IBM Cloud nella console {{site.data.keyword.containerlong_notm}}. I cluster OpenShift eseguono la versione 3.11, che include Kubernetes versione 1.11. Il sistema operativo è Red Hat Enterprise Linux 7.
{: shortdesc}

Vuoi saperne di più sulla personalizzazione della tua configurazione del cluster con la CLI? Consulta [Creazione di un cluster OpenShift](/docs/openshift?topic=openshift-openshift-create-cluster).
{: tip}

1.  Accedi al tuo [account {{site.data.keyword.cloud_notm}} ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://cloud.ibm.com/).
2.  Dal **catalogo**, fai clic su [**Red Hat OpenShift Cluster** ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")]](https://cloud.ibm.com/kubernetes/catalog/openshiftcluster), e fai quindi clic su **Create**.
3.  Scegli i dettagli di configurazione e il nome per il tuo cluster.
    *   Immetti un nome per il tuo cluster e seleziona il gruppo di risorse che vuoi assegnare al tuo cluster.
    *   Immetti le tag che vuoi aggiungere al tuo cluster. Le tag possono aiutarti a organizzare e trovare i tuoi cluster più facilmente nel tuo account {{site.data.keyword.cloud_notm}}.
    *   Per l'ubicazione (**Location**), imposta l'area geografica (**Geography**) e seleziona quindi una qualsiasi delle sei [ubicazioni ](/docs/openshift?topic=openshift-regions-and-zones) di area metropolitana (**Metro**) multizona in tutto il mondo da utilizzare per le tue zone di lavoro (**Worker zones**).
    *   Per **Default worker pool**, scegli un profilo disponibile per i tuoi nodi di lavoro. Red Hat OpenShift on IBM Cloud supporta solo OpenShift versione 3.11, che include Kubernetes versione 1.11. Il sistema operativo è Red Hat Enterprise Linux 7.
    *   Imposta un numero di nodi di lavoro da creare per ogni zona, ad esempio `3`.
4.  Per finire, fai clic su **Create cluster**.<p class="note">Il completamento del processo di creazione del tuo cluster potrebbe richiedere alcuni minuti. Una volta che lo stato del cluster diventa **Normal**, i componenti di rete e di bilanciamento del carico del cluster impiegano circa altri 10 minuti per distribuire e aggiornare il dominio cluster che utilizzi per la console web OpenShift e per altri instradamenti. </p>
5.  Verifica che la tua configurazione del cluster sia terminata prima di continuare al passo successivo controllando che il **dominio secondario Ingress** nella pagina dei dettagli del cluster segua un modello di `<cluster_name>.<region>.containers.appdomain.cloud`.

<br />


## Distribuzione di un'applicazione con il catalogo OpenShift
{: #openshift_gs_app}

Dalla console OpenShift, puoi distribuire una delle applicazioni di catalogo integrate.
{: shortdesc}

1.  Dalla pagina dei dettagli del cluster, fai clic su **OpenShift web console**.
2.  Nel riquadro **Getting Started**, fai clic su **Create Project**. Immetti un nome per il tuo progetto e fai clic su **Create**. Se già hai dei progetti esistenti, il tuo nome di riquadro cambia in **My Projects**.
3.  Fai clic sul tuo nome progetto e fai quindi clic su **Browse Catalog**.
4.  Fai clic su un'applicazione da distribuire. Ad esempio, dalla scheda **Language**, seleziona **JavaScript** e fai quindi clic su **Node.js**. Viene aperta la procedura guidata di Node.js.
    1.  Nella scheda *Information*, fai clic su **Next**.
    2.  Nella scheda *Configuration*, fai clic su **Try Sample Repository**.
    3.  Nella scheda *Results*, viene creata l'applicazione `nodejs-ex`. Fai clic su **Close**.
5.  Attendi qualche minuto che i pod vengano distribuiti. Per controllare lo stato dei pod, fai clic su **Applications > Pods**. Devi vedere un pod `nodejs-ex-build` in uno stato di **Completed** e un pod `nodejs-ex` in uno stato di **Running**.
6.  Quando sono disponibili entrambi i pod, fai clic su **Applications > Routes**.
7.  Fai clic sul nome host (**Hostname**) della tua applicazione `nodejs-ex`, Nel tuo browser viene aperta una nuova scheda con un messaggio simile al seguente.
    ```
    Welcome to your Node.js application on OpenShift
    ```
    {: screen}
8.  **Facoltativo**: per ripulire le risorse che hai creato, fai clic sul nome progetto nella barra dei menu e quindi su **View All Projects**. Fai clic sull'**icona More options > Delete project**.

<br />


## Operazioni successive
{: #openshift_gs_next}

Completa l'[esercitazione Red Hat OpenShift on IBM Cloud](/docs/openshift?topic=openshift-openshift_tutorial) per:
* Configura la tua CLI {{site.data.keyword.cloud_notm}} e OpenShift.
* Distribuisci un'applicazione che utilizza un servizio {{site.data.keyword.cloud_notm}}.

<br>
Per ulteriori informazioni sulla gestione delle tue applicazioni e dei tuoi servizi di instradamento, vedi la [Developer Guide di OpenShift ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")]](https://docs.openshift.com/container-platform/3.11/dev_guide/index.html).

<br />

