---

copyright:
  years: 2014, 2019
lastupdated: "2019-07-31"

keywords: oks, iro, openshift, red hat, red hat openshift, rhos, roks, rhoks

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

# Registrazione e monitoraggio
{: #openshift_health}



Per le metriche del cluster e la registrazione e il monitoraggio delle applicazioni, i cluster {{site.data.keyword.openshiftlong}} includono strumenti integrati per aiutarti a gestire l'integrità della tua singola istanza cluster. Puoi anche configurare gli strumenti {{site.data.keyword.cloud_notm}} per l'analisi multicluster o altri casi d'uso, quali i componenti aggiuntivi {{site.data.keyword.containerlong_notm}}: {{site.data.keyword.la_full_notm}} e {{site.data.keyword.mon_full_notm}}.
{: shortdesc}

## Utilizzo dello stack di registrazione e monitoraggio OpenShift integrato
{: #openshift_logmet}

Per impostazione predefinita, i cluster Red Hat OpenShift on IBM Cloud sono distribuiti con strumenti di registrazione e monitoraggio integrati che sono basati su progetti open source quali Prometheus, Elasticsearch, Fluentd e Kibana. Per ulteriori informazioni, vedi la seguente documentazione di OpenShift.
{: shortdesc}

* [Prometheus Cluster Monitoring ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://docs.openshift.com/container-platform/3.11/install_config/prometheus_cluster_monitoring.html).
* [Aggregating Container Logs ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://docs.openshift.com/container-platform/3.11/install_config/aggregate_logging.html).
* [Aggregate Logging Sizing Guidelines ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://docs.openshift.com/container-platform/3.11/install_config/aggregate_logging_sizing.html).
* [Enabling Cluster Metrics ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://docs.openshift.com/container-platform/3.11/install_config/cluster_metrics.html).

<br />


## Configurazione dei componenti aggiuntivi LogDNA e Sysdig per monitorare l'integrità del cluster
{: #openshift_logdna_sysdig}

Poiché OpenShift configura per impostazione predefinita dei [vincoli del contesto di sicurezza (o SCC, Security Context Constraint) ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://docs.openshift.com/container-platform/3.11/admin_guide/manage_scc.html) più rigidi rispetto al sistema Kubernetes della community, potresti notare che alcune applicazioni o alcuni componenti aggiuntivi del cluster che utilizzi sul Kubernetes della community non possono essere distribuiti su OpenShift nello stesso modo. In particolare, molte immagini devono essere eseguite come utente `root` o come contenitore privilegiato, cosa che viene impedita in OpenShift per impostazione predefinita. Puoi modificare gli SCC predefiniti creando account di sicurezza privilegiati e aggiornando il `securityContext` nella specifica del pod per utilizzare due popolari componenti aggiuntivi di {{site.data.keyword.containerlong_notm}}: {{site.data.keyword.la_full_notm}} e {{site.data.keyword.mon_full_notm}}.
{: shortdesc}

Prima di iniziare, accedi al tuo cluster come amministratore.
1.  Apri la tua console OpenShift all'indirizzo `https://<master_URL>/console`. Ad esempio, `https://c0.containers.cloud.ibm.com:23652/console`.
2.  Dalla barra dei menu della console web OpenShift, fai clic sul tuo profilo **IAM#user.name@email.com > Copy Login Command** e incolla nel tuo terminale il comando di accesso `oc` copiato per eseguire l'autenticazione tramite la CLI.

3.  Configura [{{site.data.keyword.la_short}}](#openshift_logdna) e [{{site.data.keyword.mon_short}}](#openshift_sysdig).

<br />


### Configurazione di LogDNA
{: #openshift_logdna}

Configura un progetto e un account di servizio privilegiato per {{site.data.keyword.la_full_notm}}. Quindi, crea un'istanza {{site.data.keyword.la_short}} nel tuo account {{site.data.keyword.cloud_notm}}. Per integrare la tua istanza {{site.data.keyword.la_short}} con il cluster OpenShift, devi modificare la serie di daemon che viene distribuita per utilizzare l'account di servizio privilegiato per l'esecuzione come root.
{: shortdesc}

1.  Configura il progetto e l'account di servizio privilegiato per LogDNA.
    1.  Come amministratore del cluster, crea un progetto `logdna`.
        ```
        oc adm new-project logdna
        ```
        {: pre}
    2.  Indica il progetto come destinazione in modo che le successive risorse che crei siano nello spazio dei nomi del progetto `logdna`.
        ```
        oc project logdna
        ```
        {: pre}
    3.  Crea un account di servizio per il progetto `logdna`.
        ```
        oc create serviceaccount logdna
        ```
        {: pre}
    4.  Aggiungi un vincolo del contesto di sicurezza privilegiato all'account di servizio per il progetto `logdna`.<p class="note">Se vuoi controllare quale autorizzazione viene fornita dalla politica SCC `privileged` all'account di servizio, esegui `oc describe scc privileged`. Per ulteriori informazioni sui SCC, vedi la [documentazione di OpenShift ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://docs.openshift.com/container-platform/3.11/admin_guide/manage_scc.html).</p>
        ```
        oc adm policy add-scc-to-user privileged -n logdna -z logdna
        ```
        {: pre}
2.  Crea la tua istanza {{site.data.keyword.la_full_notm}} nello stesso gruppo di risorse del tuo cluster. Seleziona un piano dei prezzi che determina il periodo di conservazione per i tuoi log, ad esempio `lite` che conserva i log per 0 giorni. Non è necessario che la regione corrisponda alla regione del tuo cluster. Per ulteriori informazioni, vedi [Provisioning di un'istanza](/docs/services/Log-Analysis-with-LogDNA/tutorials?topic=LogDNA-provision) e [Piani dei prezzi](/docs/services/Log-Analysis-with-LogDNA?topic=LogDNA-about#overview_pricing_plans).
    ```
    ibmcloud resource service-instance-create <service_instance_name> logdna (lite|7-days|14-days|30-days) <region> [-g <resource_group>]
    ```
    {: pre}

    Comando di esempio:
    ```
    ibmcloud resource service-instance-create logdna-openshift logdna lite us-south
    ```
    {: pre}

    Nell'output, prendi nota dell'**ID** dell'istanza del servizio, che è nel formato `crn:v1:bluemix:public:logdna:<region>:<ID_string>::`.
    ```
    Service instance <name> was created.

    Name:         <name>   
    ID:           crn:v1:bluemix:public:logdna:<region>:<ID_string>::   
    GUID:         <guid>   
    Location:     <region>   
    ...
    ```
    {: screen}    
3.  Ottieni la chiave di inserimento della tua istanza {{site.data.keyword.la_short}}. La chiave di inserimento LogDNA viene utilizzata per aprire un socket web sicuro al server di inserimento LogDNA e per autenticare l'agent di registrazione presso il servizio {{site.data.keyword.la_short}}.
    1.  Crea una chiave di servizio per la tua istanza LogDNA.
        ```
        ibmcloud resource service-key-create <key_name> Administrator --instance-id <logdna_instance_ID>
        ```
        {: pre}
    2.  Prendi nota della **ingestion_key** della tua chiave di servizio.
        ```
        ibmcloud resource service-key <key_name>
        ```
        {: pre}

        Output di esempio:
        ```
        Name:          <key_name>  
        ID:            crn:v1:bluemix:public:logdna:<region>:<ID_string>::    
        Created At:    Thu Jun  6 21:31:25 UTC 2019   
        State:         active   
        Credentials:                                   
                       apikey:                   <api_key_value>      
                       iam_apikey_description:   Auto-generated for key <ID>     
                       iam_apikey_name:          <key_name>       
                       iam_role_crn:             crn:v1:bluemix:public:iam::::role:Administrator      
                       iam_serviceid_crn:        crn:v1:bluemix:public:iam-identity::<ID_string>     
                       ingestion_key:            111a11aa1a1a11a1a11a1111aa1a1a11    
        ```
        {: screen}
4.  Crea un segreto Kubernetes per archiviare la chiave di inserimento LogDNA per la tua istanza del servizio.
    ```
     oc create secret generic logdna-agent-key --from-literal=logdna-agent-key=<logDNA_ingestion_key>
    ```
    {: pre}
5.  Crea una serie di daemon OpenShift per distribuire l'agent LogDNA su ogni nodo di lavoro del tuo cluster Kubernetes. L'agent LogDNA raccoglie i log con l'estensione `*.log` e i file senza estensione archiviati nella directory `/var/log` del tuo pod. Per impostazione predefinita, i log vengono raccolti da tutti gli spazi dei nomi, incluso `kube-system`, e vengono inoltrati automaticamente al servizio {{site.data.keyword.la_short}}.
    ```
    oc create -f https://raw.githubusercontent.com/logdna/logdna-agent/master/logdna-agent-ds-os.yml
    ```
    {: pre}
6.  Verifica che il pod `logdna-agent` su ogni nodo sia in uno stato **Running**.
    ```
    oc get pods
    ```
    {: pre}
7.  Dalla [console {{site.data.keyword.cloud_notm}} **Observability > Logging**](https://cloud.ibm.com/observe/logging), nella riga per la tua istanza {{site.data.keyword.la_short}}, fai clic su **View LogDNA**. Viene aperto il dashboard LogDNA. Dopo alcuni minuti, i log del tuo cluster vengono visualizzati e puoi analizzarli.

Per ulteriori informazioni su come utilizzare {{site.data.keyword.la_short}}, vedi la [documentazione sui passi successivi](/docs/services/Log-Analysis-with-LogDNA?topic=LogDNA-kube#kube_next_steps).

<br />


### Configurazione di Sysdig
{: #openshift_sysdig}

Crea un'istanza {{site.data.keyword.mon_full_notm}} nel tuo account {{site.data.keyword.cloud_notm}}. Per integrare la tua istanza {{site.data.keyword.mon_short}} con il cluster OpenShift, devi eseguire uno script che crea un progetto e un account di servizio privilegiato per l'agent Sysdig.
{: shortdesc}

1.  Crea la tua istanza {{site.data.keyword.mon_full_notm}} nello stesso gruppo di risorse del tuo cluster. Seleziona un piano dei prezzi che determina il periodo di conservazione per i tuoi log, ad esempio `lite`. Non è necessario che la regione corrisponda alla regione del tuo cluster. Per ulteriori informazioni, vedi [Provisioning di un'istanza](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-provision).
    ```
    ibmcloud resource service-instance-create <service_instance_name> sysdig-monitor (lite|graduated-tier) <region> [-g <resource_group>]
    ```
    {: pre}

    Comando di esempio:
    ```
    ibmcloud resource service-instance-create sysdig-openshift sysdig-monitor lite us-south
    ```
    {: pre}

    Nell'output, prendi nota dell'**ID** dell'istanza del servizio, che è nel formato `crn:v1:bluemix:public:logdna:<region>:<ID_string>::`.
    ```
    Service instance <name> was created.

    Name:         <name>   
    ID:           crn:v1:bluemix:public:sysdig-monitor:<region>:<ID_string>::   
    GUID:         <guid>   
    Location:     <region>   
    ...
    ```
    {: screen}    
2.  Ottieni la chiave di accesso della tua istanza {{site.data.keyword.mon_short}}. La chiave di accesso Sysdig viene utilizzata per aprire un socket web sicuro al server di inserimento Sysdig e per autenticare l'agent di monitoraggio presso il servizio {{site.data.keyword.mon_short}}.
    1.  Crea una chiave di servizio per la tua istanza Sysdig.
        ```
        ibmcloud resource service-key-create <key_name> Administrator --instance-id <sysdig_instance_ID>
        ```
        {: pre}
    2.  Prendi nota della **Chiave di accesso Sysdig** e dell'**Endpoint raccoglitore Sysdig** della tua chiave di servizio.
        ```
        ibmcloud resource service-key <key_name>
        ```
        {: pre}

        Output di esempio:
        ```
        Name:          <key_name>  
        ID:            crn:v1:bluemix:public:sysdig-monitor:<region>:<ID_string>::    
        Created At:    Thu Jun  6 21:31:25 UTC 2019   
        State:         active   
        Credentials:                                   
                       Sysdig Access Key:           11a1aa11-aa1a-1a1a-a111-11a11aa1aa11      
                       Sysdig Collector Endpoint:   ingest.<region>.monitoring.cloud.ibm.com      
                       Sysdig Customer Id:          11111      
                       Sysdig Endpoint:             https://<region>.monitoring.cloud.ibm.com  
                       apikey:                   <api_key_value>      
                       iam_apikey_description:   Auto-generated for key <ID>     
                       iam_apikey_name:          <key_name>       
                       iam_role_crn:             crn:v1:bluemix:public:iam::::role:Administrator      
                       iam_serviceid_crn:        crn:v1:bluemix:public:iam-identity::<ID_string>       
        ```
        {: screen}
3.  Esegui lo script per configurare un progetto `ibm-observe` con un account di servizio privilegiato e una serie di daemon Kubernetes per distribuire l'agent Sysdig su ogni nodo di lavoro del tuo cluster Kubernetes. L'agent Sysdig raccoglie metriche quali, ad esempio, l'utilizzo della CPU del nodo di lavoro, l'utilizzo della memoria del nodo di lavoro, il traffico HTTP da e verso i tuoi contenitori e i dati sui diversi componenti dell'infrastruttura.

    Nel seguente comando, sostituisci <code>&lt;sysdig_access_key&gt;</code> e <code>&lt;sysdig_collector_endpoint&gt;</code> con i valori dalla chiave di servizio che hai creato in precedenza. Per <code>&lt;tag&gt;</code>, puoi associare le tag con il tuo agent Sysdig, ad esempio `role:service,location:us-south` per aiutarti ad identificare l'ambiente da cui provengono le metriche.

    ```
    curl -sL https://ibm.biz/install-sysdig-k8s-agent | bash -s -- -a <sysdig_access_key> -c <sysdig_collector_endpoint> -t <tag> -ac 'sysdig_capture_enabled: false' --openshift
    ```
    {: pre}

    Output di esempio:
    ```
    * Detecting operating system
    * Downloading Sysdig cluster role yaml
    * Downloading Sysdig config map yaml
    * Downloading Sysdig daemonset v2 yaml
    * Creating project: ibm-observe
    * Creating sysdig-agent serviceaccount in project: ibm-observe
    * Creating sysdig-agent access policies
    * Creating sysdig-agent secret using the ACCESS_KEY provided
    * Retreiving the IKS Cluster ID and Cluster Name
    * Setting cluster name as <cluster_name>
    * Setting ibm.containers-kubernetes.cluster.id 1fbd0c2ab7dd4c9bb1f2c2f7b36f5c47
    * Updating agent configmap and applying to cluster
    * Setting tags
    * Setting collector endpoint
    * Adding additional configuration to dragent.yaml
    * Enabling Prometheus
    configmap/sysdig-agent created
    * Deploying the sysdig agent
    daemonset.extensions/sysdig-agent created
    ```
    {: screen}

4.  Verifica che i pod `sydig-agent` su ciascun nodo mostrino che i pod **1/1** sono pronti e che ogni pod abbia uno stato **Running**.
    ```
    oc get pods
    ```
    {: pre}

    Output di esempio:
    ```
    NAME                 READY     STATUS    RESTARTS   AGE
    sysdig-agent-qrbcq   1/1       Running   0          1m
    sysdig-agent-rhrgz   1/1       Running   0          1m
    ```
    {: screen}
5.  Dalla [console {{site.data.keyword.cloud_notm}} **Observability > Monitoring**](https://cloud.ibm.com/observe/logging), nella riga per la tua istanza {{site.data.keyword.mon_short}}, fai clic su **View Sysdig**. Viene aperto il dashboard Sysdig e puoi analizzare le metriche del tuo cluster.

Per ulteriori informazioni su come utilizzare {{site.data.keyword.mon_short}}, vedi la [documentazione sui passi successivi](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-kubernetes_cluster#kubernetes_cluster_next_steps).

<br />


### Facoltativo: ripulitura
{: #openshift_logdna_sysdig_cleanup}

Rimuovi le istanze {{site.data.keyword.la_short}} e {{site.data.keyword.mon_short}} dal tuo cluster e dall'account {{site.data.keyword.cloud_notm}}. Tieni presente che, a meno che non archivi i log e le metriche nell'[archiviazione persistente](/docs/services/Log-Analysis-with-LogDNA?topic=LogDNA-archiving), non puoi accedere a queste informazioni dopo aver eliminato le istanze dal tuo account.
{: shortdesc}

1.  Ripulisci le istanze {{site.data.keyword.la_short}} e {{site.data.keyword.mon_short}} nel tuo cluster rimuovendo i progetti che hai creato per loro. Quando elimini un progetto vengono rimosse anche le sue risorse, come gli account di servizio e le serie di daemon.
    ```
    oc delete project logdna
    ```
    {: pre}
    ```
    oc delete project ibm-observe
    ```
    {: pre}
2.  Rimuovi l'istanza dal tuo account {{site.data.keyword.cloud_notm}}.
    *   [Rimozione di un'istanza {{site.data.keyword.la_short}}](/docs/services/Log-Analysis-with-LogDNA?topic=LogDNA-remove).
    *   [Rimozione di un'istanza {{site.data.keyword.mon_short}}](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-remove).

<br />


## Configurazione degli strumenti di registrazione e monitoraggio {{site.data.keyword.cloud_notm}}
{: #openshift_other_logmet}

Per ulteriori informazioni su altri strumenti di registrazione e monitoraggio che puoi impostare, compresi i servizi {{site.data.keyword.cloud_notm}}, vedi i seguenti argomenti nella documentazione di {{site.data.keyword.containershort_notm}}.
{: shortdesc}

* [Scelta di una soluzione di registrazione](/docs/containers?topic=containers-health#logging_overview).
* [Scelta di una soluzione di monitoraggio](/docs/containers?topic=containers-health#view_metrics).
