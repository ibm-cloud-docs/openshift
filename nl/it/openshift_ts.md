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
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}

# Risoluzione dei problemi dei cluster OpenShift
{: #openshift_troubleshoot}

Riesamina alcuni problemi noti o messaggi di errore comuni che potresti riscontrare quando utilizzi i cluster {{site.data.keyword.openshiftlong}}.
{: shortdesc}

Per il debug del cluster generale, vedi la documentazione di {{site.data.keyword.containerlong_notm}}:
* [Debug del tuo cluster](/docs/containers?topic=containers-cs_troubleshoot)
* [Cluster e nodi di lavoro](/docs/containers?topic=containers-cs_troubleshoot_clusters)
* [Archiviazione](/docs/containers?topic=containers-cs_troubleshoot_storage)
* [Registrazione e monitoraggio](/docs/containers?topic=containers-cs_troubleshoot_health)
* [Debug di Ingress](/docs/containers?topic=containers-cs_troubleshoot_debug_ingress)
* [Rete cluster](/docs/containers?topic=containers-cs_troubleshoot_network)

## Feedback e domande
{: #openshift_support}

I cluster Red Hat OpenShift on IBM Cloud generalmente disponibili sono coperti dal supporto IBM. Se hai dei cluster beta rimanenti, [crea i cluster OpenShift standard](/docs/openshift?topic=openshift-openshift-create-cluster) prima che i cluster beta scadano.
{: shortdesc}

Per qualsiasi domanda o feedback, pubblica il messaggio in Slack.
*   Se sei un utente esterno, pubblica nel canale [#openshift ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://ibm-container-service.slack.com/messages/CKCJLJCH4).
*   Se sei un dipendente IBM, utilizza il canale [#iks-openshift-users ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://ibm-argonauts.slack.com/messages/CJH0UPN2D).

Se non utilizzi un ID IBM per il tuo account {{site.data.keyword.cloud_notm}}, [richiedi un invito](https://bxcs-slack-invite.mybluemix.net/) a questo Slack.
{: tip}

## Autorizzazioni mancanti per creare i cluster
{: #rhoks_ts_cluster_permissions}

{: tsSymptoms}
Non disponi delle autorizzazioni per creare un cluster.

{: tsCauses}
Per creare un cluster OpenShift, devi disporre delle stesse autorizzazioni di cui hai bisogno per creare un cluster Kubernetes della community. Le autorizzazioni richieste includono le credenziali dell'infrastruttura per la regione e il gruppo di risorse e le autorizzazioni **Amministratore** di {{site.data.keyword.cloud_notm}} IAM (Identity and Access Management).

{: tsResolve}
Riesamina [Assegnazione dell'accesso al cluster](/docs/openshift?topic=openshift-users) per imparare come configurare le credenziali dell'infrastruttura per una regione e un gruppo di risorse e come assegnare agli utenti l'accesso tramite IAM.

<br />


## Non è stata trovata alcuna risorsa
{: #rhoks_ts_not_found}

{: tsSymptoms}
Quando stai eseguendo un comando `oc` come `oc get nodes` o `oc get secrets`, vedi un messaggio di errore simile al seguente:

```
No resources found.
```
{: screen}

{: tsCauses}
Il tuo token OpenShift è scaduto. I token OpenShift generati utilizzando le tue credenziali {{site.data.keyword.cloud_notm}} IAM scadono in 24 ore.

{: tsResolve}
[Riesegui l'autenticazione con il token OpenShift](/docs/openshift?topic=openshift-openshift-cli#openshift_cluster_login) copiando il comando `oc login` dalla console web o creando una chiave API.

<br />


## Errore del server OpenVPN dovuto all'indirizzo IP Ingress per NLB
{: #rhoks_ts_openvpn_subnet}

{: tsSymptoms}
Vedi il seguente messaggio di errore.
```
CAE003: Unable to determine the ingress IP address for the network load balancer.
```
{: screen}

{: tsCauses}
Non è stato possibile configurare il server OpenVPN perché non è stato possibile trovare l'indirizzo IP del router creato per l'NLB (network load balancer). Al router potrebbe non essere stato assegnato un indirizzo IP perché il tuo cluster non dispone di una sottorete con indirizzi IP portatili disponibili o la configurazione dell'NLB non era stata completata.

{: tsResolve}

**Verifica che il tuo cluster abbia delle sottoreti disponibili.**
1.  Controlla che il tuo cluster abbia un **CIDR sottorete** per le sottoreti pubblica e privata. Se configuri un cluster solo VLAN privata, potresti avere solo una sottorete privata.
    ```
    ibmcloud oc cluster-get --cluster <cluster_name_or_ID> --showResources
    ```
    {: pre}

    Output di esempio:
    ```
    Name:                   <cluster_name>   
    ...

    Subnet VLANs
    VLAN ID   Subnet CIDR        Public   User-managed   
    2345678   10.xxx.xx.xxx/29   false    false   
    2876543   169.xx.xxx.xxx/29  true     false
    ```
    {: screen}
2.  Se il cluster non ha una sottorete, [crea una sottorete per il cluster](/docs/containers?topic=containers-subnets#request) oppure [aggiungi una sottorete esistente dal tuo account al cluster](/docs/containers?topic=containers-subnets#add-existing).
3.  Se il cluster ha una sottorete, [controlla la presenza di indirizzi IP portatili disponibili](/docs/containers?topic=containers-subnets#review_ip) e, se necessario, [aggiungi ulteriori indirizzi IP portatili aggiungendo una sottorete](/docs/containers?topic=containers-subnets#adding_ips).
4.  Aggiorna il master per riavviare la configurazione di OpenVPN in modo che utilizzi la sottorete disponibile.
    ```
    ibmcloud oc cluster-refresh --cluster <cluster_name_or_ID>
    ```
    {: pre}

**Verifica che l'impostazione di NLB sia stata completata correttamente.**
1.  Controlla che i pod `ibm-cloud-provider-ip-*` per l'NLB siano in uno stato **Running**.
    ```
    oc get pods -n ibm-system | grep ibm-cloud-provider-ip
    ```
    {: pre}
2.  Se un pod non è in esecuzione, riesamina gli eventi (**Events**) nei dettagli del pod per risolvere ulteriormente il problema.
    ```
    oc describe pod -n kube-system <pod_name>
    ```
    {: pre}
3.  Dopo che hai risolto il problema del pod dell'NLB, aggiorna il master per riavviare la configurazione dell'NLB.
    ```
    ibmcloud oc cluster-refresh --cluster <cluster_name_or_ID>
    ```
    {: pre}

<br />


## Errore del server OpenVPN dovuto al DNS dell'NLB
{: #rhoks_ts_openvpn_dns}

{: tsSymptoms}
 Non è stato possibile creare un DNS (domain name service) per l'NLB (network load balancer) (`ibmcloud oc nlb-dns-create`) con il seguente messaggio di errore:<ul>
<li><code>This action requires the Editor role for the cluster in IBM Cloud Container Service. Contact the IBM Cloud account administrator and request the required Identity and Access user role. (A0008)</code></li>
<li><code>The specified cluster could not be found. (A0006)</code></li>
<li><code>The input parameters in the request body are either incomplete or in the wrong format. Be sure to include all required parameters in your request in JSON format. (E0011)</code></li></ul>

{: tsCauses}
Non è stato possibile configurare il server OpenVPN perché non è stato creato un DNS (domain name service) per l'NLB (network load balancer).

{: tsResolve}
1.  Controlla di disporre delle autorizzazioni corrette in {{site.data.keyword.cloud_notm}} IAM. In caso negativo, contatta il tuo amministratore dell'account perché [ti assegni il ruolo di accesso al servizio o alla piattaforma IAM appropriato](/docs/containers?topic=containers-users#platform).
    ```
    ibmcloud iam user-policies <my_user_name@example.com>
    ```
    {: pre}
2.  Per gli errori di cluster non trovato o di parametro di input non corretto, continua al passo successivo.
3.  Aggiorna il master in modo che l'operazione di creazione del DNS dell'NLB venga ritentata.
    ```
    ibmcloud oc cluster-refresh --cluster <cluster_name_or_ID>
    ```
    {: pre}

<br />


## Errore del server VPN dovuto alle credenziali dell'infrastruttura
{: #rhoks_ts_openvpn_login}

{: tsSymptoms}
Dopo che hai creato o aggiornato un cluster, lo stato master restituisce un messaggio di errore di configurazione del server VPN simile a quello riportato di seguito.
```
VPN server configuration update failed. IBM Cloud support has been notified and is working to resolve this issue.
```
{: screen}

{: tsCauses}
Le credenziali dell'infrastruttura associate al gruppo di risorse in cui viene creato il cluster mancano (come ad esempio il proprietario della chiave API non fa più parte dell'account) o mancano le autorizzazioni richieste.

{: tsResolve}
[Completa la guida alla risoluzione dei problemi](/docs/containers?topic=containers-cs_troubleshoot_clusters#cs_credentials) per controllare e aggiornare le credenziali dell'infrastruttura utilizzate per il gruppo di risorse.

<br />


## Progetti mancanti oppure i comandi `oc` e `kubectl` non riescono
{: #rhoks_ts_admin_config}

{: tsSymptoms}
Non vedi tutti i progetti a cui hai accesso. Quando provi a eseguire i comandi `oc` o `kubectl`, vedi un errore simile al seguente:
```
No resources found.
Error from server (Forbidden): <resource> is forbidden: User "IAM#user@email.com" cannot list <resources> at the cluster scope: no RBAC policy matched
```
{: screen}

{: tsCauses}
Devi scaricare i file di configurazione `admin` per il tuo cluster per eseguire i comandi che richiedono il ruolo cluster `cluster-admin`.

{: tsResolve}
Esegui `ibmcloud oc cluster-config --cluster <cluster_name_or_ID> --admin` e riprova.

<br />


## Pod nello stato `CrashLoopBackOff`
{: #rhoks_ts_pods_crashloop}

{: tsSymptoms}
I tuoi pod sono in uno stato `CrashLoopBackOff`.

{: tsCauses}
Quando provi a distribuire un'applicazione che funziona sulle piattaforme Kubernetes della community, potresti vedere questo stato oppure un messaggio di errore correlato perché, per impostazione predefinita, OpenShift configura delle impostazioni di sicurezza più rigide rispetto a Kubernetes della community.

{: tsResolve}
Assicurati di aver seguito la documentazione nell'[argomento Spostamento delle tue applicazioni a OpenShift](/docs/openshift?topic=openshift-openshift_apps#openshift_move_apps).

<br />


## Impossibile eseguire il push o il pull di immagini dalla macchina locale al registro Docker
{: #rhoks_ts_docker_local}

{: tsSymptoms}
Non puoi eseguire il push o il pull di immagini Docker dalla tua macchina locale al registro Docker integrato del cluster.

{: tsCauses}
Per impostazione predefinita, il registro Docker è disponibile internamente nel cluster. Puoi creare applicazioni da directory remote come GitHub o DockerHub utilizzando il comando `oc new-app`. In alternativa, puoi esporre il tuo registro Docker come con un instradamento o un programma di bilanciamento del carico in modo da poter eseguire il push e il pull di immagini dalla tua macchina locale.

{: tsResolve}
Crea un instradamento per il servizio `docker-registry` nel progetto `default`. Includi l'indicatore `--hostname` in modo da poter dare al registro un nome dominio più breve.

```
oc create route edge --service=docker-registry -n default --hostname <registry_domain_name>
```
{: pre}
