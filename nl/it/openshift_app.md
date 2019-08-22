---

copyright:
  years: 2014, 2019
lastupdated: "2019-07-31"

keywords: kubernetes, openshift, roks, rhoks, rhos

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

# Distribuzione di applicazioni nei cluster OpenShift
{: #openshift_apps}

Con i cluster {{site.data.keyword.openshiftlong}}, puoi distribuire le applicazioni da un file o un repository remoto come GitHub con un singolo comando. Inoltre, i tuoi cluster sono forniti con diversi servizi integrati che puoi utilizzare per gestire più agevolmente il tuo cluster.
{: shortdesc}

Per creare una nuova applicazione, utilizza il comando `oc new-app`. Per ulteriori informazioni, [prova l'esercitazione](/docs/openshift?topic=openshift-openshift_tutorial#openshift_deploy_app) e vedi la [documentazione di OpenShift ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://docs.openshift.com/container-platform/3.11/getting_started/developers_cli.html).

```
oc new-app --name <app_name> https://github.com/<path_to_app_repo> [--context-dir=<subdirectory>]
```
{: pre}

## Spostamento delle tue applicazioni a OpenShift
{: #openshift_move_apps}

Per impostazione predefinita, OpenShift configura impostazioni di sicurezza più rigide rispetto al Kubernetes della community  Se hai delle applicazioni che in precedenza venivano eseguite su Kubernetes della community, potresti doverle modificare in modo da poterle distribuire su OpenShift.
{: shortdesc}

Ad esempio, le applicazioni configurate per l'esecuzione come root potrebbero non riuscire, con i pod in uno stato `CrashLoopBackOff`. Per risolvere questo problema, puoi modificare i vincoli del contesto di sicurezza predefiniti o utilizzare un'immagine che non viene eseguita come root.

Per ulteriori informazioni, vedi la documentazione di OpenShift per la [Gestione di SCC (Security Context Constraint) ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://docs.openshift.com/container-platform/3.11/admin_guide/manage_scc.html).

Per migrare le applicazioni OpenShift da una versione precedente, ad esempio da 2.x a 3.x, vedi la [documentazione di OpenShift ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://docs.openshift.com/container-platform/3.11/dev_guide/migrating_applications/index.html).

<br />


## Accesso alla console web OpenShift
{: #openshift_console}

Puoi utilizzare la console OpenShift per gestire le tue applicazioni, distribuire applicazioni dal catalogo e accedere alla funzionalità integrata per un ausilio nella gestione del tuo cluster. La console OpenShift viene distribuita al tuo cluster per impostazione predefinita, invece del dashboard Kubernetes come nei cluster Kubernetes della community.
{: shortdesc}

Per una rapida panoramica di orientamento della console, vedi l'[esercitazione](/docs/openshift?topic=openshift-openshift_tutorial#openshift_oc_console).

Per ulteriori informazioni sulla console, vedi la [documentazione di OpenShift ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://docs.openshift.com/container-platform/3.11/getting_started/developers_console.html).

<br />


## Accesso ai servizi OpenShift integrati
{: #openshift_access_oc_services}

Red Hat OpenShift on IBM Cloud viene fornito con dei servizi integrati che puoi utilizzare per gestire il tuo cluster, come ad esempio la console OpenShift, Prometheus e Grafana. Puoi accedere a questi servizi usando l'host locale di un [instradamento ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://docs.openshift.com/container-platform/3.11/architecture/networking/routes.html). I nomi di dominio di instradamento predefiniti seguono un modello specifico per il cluster di `<service_name>-<namespace>.<cluster_name>-<random_ID>.<region>.containers.appdomain.cloud`.
{:shortdesc}

Puoi accedere agli instradamenti dei servizi OpenShift integrati dalla [console](#openshift_services_console) o dalla [CLI](#openshift_services_cli). Potresti voler utilizzare la console per spostarti tra le risorse Kubernetes in un unico progetto. Utilizzando la CLI, puoi elencare le risorse, come gli instradamenti, in più progetti.

### Accesso ai servizi OpenShift integrati dalla console
{: #openshift_services_console}
1.  Dalla console web OpenShift, nel menu a discesa nella barra dei menu di OpenShift Container Platform, fai clic su **Application Console**.
2.  Seleziona il progetto di **default**, quindi, nel riquadro di navigazione, fai clic su **Applications > Pods**.
3.  Verifica che i pod del **router** siano in uno stato **Running**. Il router funge da punto di ingresso per il traffico di rete esterno. Puoi utilizzare il router per esporre pubblicamente i servizi nel tuo cluster sull'indirizzo IP esterno del router utilizzando un instradamento. Il router rimane in ascolto sull'interfacci di rete host pubblica, a differenza dei tuoi pod dell'applicazione che rimangono in ascolto solo sugli IP privati. Il router esegue il proxy delle richieste esterne per i nomi host di instradamento che associ ai servizi. Le richieste vengono inviate agli IP dei pod dell'applicazione identificati dal servizio.
4.  Dal riquadro di navigazione del progetto di **default**, fai clic su **Applications > Deployments** e quindi sulla distribuzione **registry-console**. Il tuo cluster OpenShift viene fornito con un registro interno che puoi utilizzare per gestire le immagini locali per le tue distribuzioni. Per visualizzare le tue immagini, fai clic su **Applications > Routes** e apri l'URL del nome host (**Hostname**) della console del registro.
5.  Dal menu a discesa nella barra dei menu di OpenShift Container Platform, fai clic su **Cluster Console**.
6.  Dal riquadro di navigazione, espandi **Monitoring**.
7.  Fai clic sullo strumento di monitoraggio integrato a cui vuoi accedere, ad esempio **Dashboards**. L'instradamento Grafana si apre nel seguente formato: `https://grafana-openshift-monitoring.<cluster_name>-<random_ID>.<region>.containers.appdomain.cloud`.<p class="note">La prima volta che accedi al nome host potresti dover eseguire l'autenticazione, ad esempio facendo clic su **Log in with OpenShift** e autorizzando l'accesso alla tua identità IAM.</p>

### Accesso ai servizi OpenShift integrati dalla CLI
{: #openshift_services_cli}

1.  Dalla vista **Application Console** o **Service Console** nella console web OpenShift, fai clic sul tuo profilo **IAM#user.name@email.com > Copy Login Command** e incolla il comando di accesso nel tuo terminale per eseguire l'autenticazione.
    ```
    oc login https://c1-e.<region>.containers.cloud.ibm.com:<port> --token=<access_token>
    ```
    {: pre}
2.  Verifica che il tuo router sia stato distribuito. Il router funge da punto di ingresso per il traffico di rete esterno. Puoi utilizzare il router per esporre pubblicamente i servizi nel tuo cluster sull'indirizzo IP esterno del router utilizzando un instradamento. Il router rimane in ascolto sull'interfacci di rete host pubblica, a differenza dei tuoi pod dell'applicazione che rimangono in ascolto solo sugli IP privati. Il router esegue il proxy delle richieste esterne per i nomi host di instradamento che associ ai servizi. Le richieste vengono inviate agli IP dei pod dell'applicazione identificati dal servizio.
    ```
    oc get svc router -n default
    ```
    {: pre}

    Output di esempio:
    ```
    NAME      TYPE           CLUSTER-IP               EXTERNAL-IP     PORT(S)                      AGE
    router    LoadBalancer   172.21.xxx.xxx   169.xx.xxx.xxx   80:30399/TCP,443:32651/TCP                      5h
    ```
    {: screen}
2.  Ottieni il nome host **Host/Port** dell'instradamento del servizio a cui vuoi accedere. Ad esempio, potresti voler accedere al tuo dashboard Grafana per controllare le metriche relative all'utilizzo delle risorse del tuo cluster. I nomi di dominio di instradamento predefiniti seguono un modello specifico per il cluster di `<service_name>-<namespace>.<cluster_name>-<random_ID>.<region>.containers.appdomain.cloud`.
    ```
    oc get route --all-namespaces
    ```
    {: pre}

    Output di esempio:
    ```
    NAMESPACE                          NAME                HOST/PORT                                                                    PATH                  SERVICES            PORT               TERMINATION          WILDCARD
    default                            registry-console    registry-console-default.<cluster_name>-<random_ID>.<region>.containers.appdomain.cloud                              registry-console    registry-console   passthrough          None
    kube-service-catalog               apiserver           apiserver-kube-service-catalog.<cluster_name>-<random_ID>.<region>.containers.appdomain.cloud                        apiserver           secure             passthrough          None
    openshift-ansible-service-broker   asb-1338            asb-1338-openshift-ansible-service-broker.<cluster_name>-<random_ID>.<region>.containers.appdomain.cloud            asb                 1338               reencrypt            None
    openshift-console                  console             console.<cluster_name>-<random_ID>.<region>.containers.appdomain.cloud                                              console             https              reencrypt/Redirect   None
    openshift-monitoring               alertmanager-main   alertmanager-main-openshift-monitoring.<cluster_name>-<random_ID>.<region>.containers.appdomain.cloud                alertmanager-main   web                reencrypt            None
    openshift-monitoring               grafana             grafana-openshift-monitoring.<cluster_name>-<random_ID>.<region>.containers.appdomain.cloud                          grafana             https              reencrypt            None
    openshift-monitoring               prometheus-k8s      prometheus-k8s-openshift-monitoring.<cluster_name>-<random_ID>.<region>.containers.appdomain.cloud                   prometheus-k8s      web                reencrypt
    ```
    {: screen}
3.  Nel tuo browser web, apri l'instradamento a cui vuoi accedere, ad esempio: `https://grafana-openshift-monitoring.<cluster_name>-<random_ID>.<region>.containers.appdomain.cloud`. La prima volta che accedi al nome host potresti dover eseguire l'autenticazione, ad esempio facendo clic su **Log in with OpenShift** e autorizzando l'accesso alla tua identità IAM.

<br>
Ora sei nell'applicazione OpenShift integrata. Ad esempio, se sei in Grafana, potresti controllare l'utilizzo della CPU dello spazio dei nomi o altri grafici. Per accedere ad altri strumenti integrati, apri i loro nomi host di instradamento.
