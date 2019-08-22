---

copyright:
  years: 2014, 2019
lastupdated: "2019-07-31"

keywords: openshift, roks, rhoks, rhos, clusters, worker nodes, worker pools, delete

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
{:gif: data-image-type='gif'}

# Aggiunta di nodi di lavoro e di zone ai cluster
{: #add_workers}

Per incrementare la disponibilità delle tue applicazioni, puoi aggiungere i nodi di lavoro a una zona esistente o a più zone esistenti nel tuo cluster. Per un supporto nella protezione delle tue applicazioni dai malfunzionamenti della zona, puoi aggiungere le zone al tuo cluster.
{:shortdesc}

Quando crei un cluster, viene eseguito il provisioning dei nodi di lavoro in un pool di nodi di lavoro. Dopo aver creato il cluster, puoi aggiungere altri nodi di lavoro a un pool ridimensionandolo o aggiungendo altro pool di nodi di lavoro. Per impostazione predefinita, il pool di nodi di lavoro esiste in un'unica zona. I cluster che hanno un pool di nodi di lavoro in un'unica zona sono denominati cluster a zona singola. Quando aggiungi altre zone al cluster, il pool di nodi di lavoro esiste tra le zone. I cluster che hanno un pool di nodi di lavoro distribuito tra più di una zona sono denominati cluster multizona.

Se hai un cluster multizona, mantieni bilanciate le sue risorse del nodo di lavoro. Assicurati che tutti i pool di nodi di lavoro vengano distribuiti tra le stesse zone e aggiungi o rimuovi i nodi di lavoro ridimensionando i pool invece di aggiungere singoli nodi.
{: tip}

Prima di iniziare, assicurati di disporre del [ruolo della piattaforma {{site.data.keyword.cloud_notm}} IAM **Operatore** o **Amministratore** ](/docs/containers?topic=containers-users#platform). Quindi, scegli una delle seguenti sezioni:
  * [Aggiungere nodi di lavoro ridimensionando un pool di nodi di lavoro esistente nel tuo cluster](#resize_pool)
  * [Aggiungere nodi di lavoro aggiungendo un pool di nodi di lavoro al tuo cluster](#add_pool)
  * [Aggiungere una zona al tuo cluster e replicare i nodi di lavoro nei tuoi pool di nodi di lavoro tra più zone](#add_zone)
  * [Obsoleto: Aggiungere un nodo di lavoro autonomo a un cluster](#standalone)

Dopo aver configurato il tuo pool di nodi di lavoro, puoi [configurare il cluster autoscaler](/docs/containers?topic=containers-ca#ca) per aggiungere o rimuovere automaticamente i nodi di lavoro dai pool di nodi di lavoro in base alle tue richieste di risorse del carico di lavoro.
{:tip}

## Aggiunta di nodi di lavoro ridimensionando un pool di nodi di lavoro esistente
{: #resize_pool}

Puoi aggiungere o ridurre il numero di nodi di lavoro nel tuo cluster ridimensionando un pool di nodi di lavoro esistente, indipendentemente dal fatto che il pool di nodi di lavoro si trovi in un'unica zona o sia distribuito tra più zone.
{: shortdesc}

Ad esempio, prendi in considerazione un cluster con un pool di nodi di lavoro che ha tre nodi di lavoro per ogni zona.
* Se il cluster è a zona singola ed esiste in `dal10`, il pool di nodi di lavoro ha tre nodi di lavoro in `dal10`. Il cluster ha un totale di tre nodi di lavoro.
* Se il cluster è multizona ed esiste in `dal10` e `dal12`, il pool di nodi di lavoro ha tre nodi di lavoro in `dal10` e tre nodo di lavoro in `dal12`. Il cluster ha un totale di sei nodi di lavoro.

Per i pool di nodi di lavoro bare metal, ricordati che la fatturazione è mensile. Il ridimensionamento aggiungendo o rimuovendo elementi influirà sui costi mensili.
{: tip}

Per ridimensionare il pool di nodi di lavoro, modifica il numero di nodi di lavoro che il pool di nodi di lavoro distribuisce in ciascuna zona:

1. Ottieni il nome del pool di nodi di lavoro che vuoi ridimensionare.
    ```
    ibmcloud oc worker-pools --cluster <cluster_name_or_ID>
    ```
    {: pre}

2. Ridimensiona il pool di nodi di lavoro indicando il numero di nodi di lavoro che vuoi distribuire in ciascuna zona. Il valore minimo è 1.
    ```
    ibmcloud oc worker-pool-resize --cluster <cluster_name_or_ID> --worker-pool <pool_name>  --size-per-zone <number_of_workers_per_zone>
    ```
    {: pre}

3. Verifica che il pool di nodi di lavoro sia stato ridimensionato.
    ```
    ibmcloud oc workers --cluster <cluster_name_or_ID> --worker-pool <pool_name>
    ```
    {: pre}

    Esempio di output per un pool di nodi di lavoro che si trova in due zone, `dal10` e `dal12`, e che è stato ridimensionato a due nodi di lavoro per zona:
    ```
    ID                                                 Public IP        Private IP      Machine Type      State    Status  Zone    Version
    kube-dal10-crb20b637238ea471f8d4a8b881aae4962-w7   169.xx.xxx.xxx   10.xxx.xx.xxx   b3c.4x16          normal   Ready   dal10   1.8.6_1504
    kube-dal10-crb20b637238ea471f8d4a8b881aae4962-w8   169.xx.xxx.xxx   10.xxx.xx.xxx   b3c.4x16          normal   Ready   dal10   1.8.6_1504
    kube-dal12-crb20b637238ea471f8d4a8b881aae4962-w9   169.xx.xxx.xxx   10.xxx.xx.xxx   b3c.4x16          normal   Ready   dal12   1.8.6_1504
    kube-dal12-crb20b637238ea471f8d4a8b881aae4962-w10  169.xx.xxx.xxx   10.xxx.xx.xxx   b3c.4x16          normal   Ready   dal12   1.8.6_1504
    ```
    {: screen}

## Aggiunta di nodi di lavoro creando un nuovo pool di nodi di lavoro
{: #add_pool}

Puoi aggiungere nodi di lavoro al tuo cluster creando un nuovo pool di nodi di lavoro.
{:shortdesc}

1. Richiama le **Worker Zones** del tuo cluster e scegli la zona a cui vuoi distribuire i nodi di lavoro nel tuo pool di nodi di lavoro. Se hai un cluster a zona singola, devi utilizzare la zona visualizzata nel campo **Worker Zones**. Per i cluster multizona, puoi scegliere una qualsiasi delle **Worker Zones** esistenti del tuo cluster o aggiungere una delle [località metropolitane multizona](/docs/containers?topic=containers-regions-and-zones#zones) per la regione in cui si trova il tuo cluster. Puoi elencare le zone disponibili eseguendo `ibmcloud oc zones`.
   ```
   ibmcloud oc cluster-get --cluster <cluster_name_or_ID>
   ```
   {: pre}

   Output di esempio:
   ```
   ...
   Worker Zones: dal10, dal12, dal13
   ```
   {: screen}

2. Per ciascuna zona elenca le VLAN pubbliche e private disponibili. Prendi nota della VLAN privata e di quella pubblica che vuoi utilizzare. Se non hai una VLAN privata o una pubblica, la VLAN viene creata automaticamente per te quando aggiungi una zona al tuo pool di nodi di lavoro.
   ```
   ibmcloud oc vlans --zone <zone>
   ```
   {: pre}

3.  Per ogni zona, riesamina i [profili disponibili per i nodi di lavoro](/docs/containers?topic=containers-planning_worker_nodes#planning_worker_nodes).

    ```
    ibmcloud oc flavors --zone <zone>
    ```
    {: pre}

4. Crea un pool di nodi di lavoro. Includi l'opzione `--labels` per etichettare automaticamente i nodi di lavoro che si trovano nel pool con l'etichetta `key=value`. Se esegui il provisioning di un pool di nodi di lavoro bare metal, specifica `--hardware dedicated`.
   ```
   ibmcloud oc worker-pool-create --name <pool_name> --cluster <cluster_name_or_ID> --machine-type <flavor> --size-per-zone <number_of_workers_per_zone> --hardware <dedicated_or_shared> --labels <key=value>
   ```
   {: pre}

5. Verifica che il pool di nodi di lavoro sia stato creato.
   ```
   ibmcloud oc worker-pools --cluster <cluster_name_or_ID>
   ```
   {: pre}

6. Per impostazione predefinita, l'aggiunta di un pool di nodi di lavoro crea un pool senza zone. Per distribuire i nodi di lavoro in una zona, devi aggiungere le zone precedentemente richiamate al pool di nodi di lavoro. Se vuoi estendere i tuoi nodi di lavoro su più zone, ripeti questo comando per ogni zona.
   ```
   ibmcloud oc zone-add --zone <zone> --cluster <cluster_name_or_ID> --worker-pools <pool_name> --private-vlan <private_VLAN_ID> --public-vlan <public_VLAN_ID>
   ```
   {: pre}

7. Verifica che sia stato eseguito il provisioning dei nodi di lavoro nella zona che hai aggiunto. I tuoi nodi di lavoro sono pronti quando lo stato cambia da **provision_pending** a **normal**.
   ```
   ibmcloud oc workers --cluster <cluster_name_or_ID> --worker-pool <pool_name>
   ```
   {: pre}

   Output di esempio:
   ```
   ID                                                 Public IP        Private IP      Machine Type      State    Status  Zone    Version
   kube-dal10-crb20b637238ea471f8d4a8b881aae4962-w7   169.xx.xxx.xxx   10.xxx.xx.xxx   b3c.4x16          provision_pending   Ready   dal10   1.8.6_1504
   kube-dal10-crb20b637238ea471f8d4a8b881aae4962-w8   169.xx.xxx.xxx   10.xxx.xx.xxx   b3c.4x16          provision_pending   Ready   dal10   1.8.6_1504
   ```
   {: screen}

## Aggiunta di nodi di lavoro aggiungendo una zona a un pool di nodi di lavoro
{: #add_zone}

Puoi estendere il tuo cluster tra più zone all'interno di una regione aggiungendo una zona al tuo pool di nodi di lavoro esistente.
{:shortdesc}

Quando aggiungi una zona a un pool di nodi di lavoro, viene eseguito il provisioning dei nodi di lavoro definiti nel tuo pool di nodi di lavoro nella nuova zona e vengono considerati per una pianificazione futura del carico di lavoro. {{site.data.keyword.containerlong_notm}} aggiunge automaticamente l'etichetta `failure-domain.beta.kubernetes.io/region` per la regione e l'etichetta `failure-domain.beta.kubernetes.io/zone` per la zona a ciascun nodo di lavoro. Il programma di pianificazione (scheduler) Kubernetes usa queste tabelle per estendere i pod tra le zone all'interno della stessa regione.

Se hai più pool di nodi di lavoro nel tuo cluster, aggiungi la zona a tutti i pool in modo che i nodi di lavoro vengano distribuiti in modo uniforme nel tuo cluster.

Prima di iniziare:
*  Per aggiungere una zona al tuo pool di nodi di lavoro, il tuo pool di nodi di lavoro deve trovarsi in una [zona che supporta il multizona](/docs/containers?topic=containers-regions-and-zones#zones). Se il tuo pool di nodi di lavoro non si trova in una zona che supporta il multizona, prendi in considerazione di [creare un nuovo pool di nodi di lavoro](#add_pool).
*  Se hai più VLAN per un cluster, più sottoreti sulla stessa VLAN o un cluster multizona, devi abilitare una [VRF (Virtual Router Function)](/docs/infrastructure/direct-link?topic=direct-link-overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud#overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud) per il tuo account dell'infrastruttura IBM Cloud in modo che i tuoi nodi di lavoro possano comunicare tra loro sulla rete privata. Per abilitare VRF, [contatta il tuo rappresentante dell'account dell'infrastruttura IBM Cloud](/docs/infrastructure/direct-link?topic=direct-link-overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud#how-you-can-initiate-the-conversion). Per controllare se una VRF è già abilitata, utilizza il comando `ibmcloud account show`. Se non puoi o non vuoi abilitare VRF, abilita lo [spanning della VLAN](/docs/infrastructure/vlans?topic=vlans-vlan-spanning#vlan-spanning). Per eseguire questa azione, ti serve l'[autorizzazione dell'infrastruttura](/docs/containers?topic=containers-users#infra_access) **Rete > Gestisci il VLAN Spanning di rete** oppure puoi richiedere al proprietario dell'account di abilitarlo. Per controllare se lo spanning della VLAN è già abilitato, utilizza il [comando `ibmcloud oc vlan-spanning-get --region <region>`](/docs/containers?topic=containers-cli-plugin-kubernetes-service-cli#cs_vlan_spanning_get).

Per aggiungere una zona con nodi di lavoro al tuo pool di nodi di lavoro:

1. Elenca le zone disponibili e seleziona quella che vuoi aggiungere al tuo pool di nodi di lavoro. La zona che hai scelto deve essere una zona che supporta il multizona.
   ```
   ibmcloud oc zones
   ```
   {: pre}

2. Elenca le VLAN disponibili in tale zona. Se non hai una VLAN privata o una pubblica, la VLAN viene creata automaticamente per te quando aggiungi una zona al tuo pool di nodi di lavoro.
   ```
   ibmcloud oc vlans --zone <zone>
   ```
   {: pre}

3. Elenca i pool di nodi di lavoro nel tuo cluster e prendi nota dei loro nomi.
   ```
   ibmcloud oc worker-pools --cluster <cluster_name_or_ID>
   ```
   {: pre}

4. Aggiungi la zona al tuo pool di nodi di lavoro. Se hai più pool di nodi di lavoro, aggiungi la zona a tutti i tuoi pool di nodi di lavoro in modo che il tuo cluster sia bilanciato in tutte le zone. Sostituisci `<pool1_id_or_name,pool2_id_or_name,...>` con i nomi di tutti i tuoi pool di nodi di lavoro in un elenco separato da virgole.

    È necessario che esistano una VLAN pubblica e una privata prima che tu possa aggiungere una zona a più pool di nodi di lavoro. Se non hai una VLAN privata e una pubblica in tale zona, aggiungi innanzitutto la zona a un pool di nodi di lavoro in modo che la VLAN privata e quella pubblica vengano create per te. Quindi, puoi aggiungere la zona agli altri pool di nodi di lavoro specificando la VLAN privata e quella pubblica create per te.
    {: note}

   Se vuoi utilizzare VLAN diverse per pool di nodi di lavoro differenti, ripeti questo comando per ciascuna VLAN e i suoi pool di nodi di lavoro corrispondenti. I nuovi nodi di lavoro vengono aggiunti alle VLAN che hai specificato, ma le VLAN per i nodi di lavoro esistenti non vengono modificate.
   {: tip}
   ```
   ibmcloud oc zone-add --zone <zone> --cluster <cluster_name_or_ID> --worker-pools <pool1_name,pool2_name,...> --private-vlan <private_VLAN_ID> --public-vlan <public_VLAN_ID>
   ```
   {: pre}

5. Verifica che la zona sia stata aggiunta al tuo cluster. Ricerca la zona aggiunta nel campo **Worker zones** dell'output. Tieni presente che il numero totale di nodi di lavoro nel campo **Workers** è aumentato in quanto è stato eseguito il provisioning dei nuovi nodi di lavoro nella zona aggiunta.
  ```
  ibmcloud oc cluster-get --cluster <cluster_name_or_ID>
  ```
  {: pre}

  Output di esempio:
  ```
  Name:                           mycluster
  ID:                             df253b6025d64944ab99ed63bb4567b6
  State:                          normal
  Created:                        2018-09-28T15:43:15+0000
  Location:                       dal10
  Master URL:                     https://c3.<region>.containers.cloud.ibm.com:30426
  Public Service Endpoint URL:    https://c3.<region>.containers.cloud.ibm.com:30426
  Private Service Endpoint URL:   https://c3-private.<region>.containers.cloud.ibm.com:31140
  Master Location:                Dallas
  Master Status:                  Ready (21 hours ago)
  Ingress Subdomain:              mycluster.us-south.containers.appdomain.cloud
  Ingress Secret:                 mycluster
  Workers:                        6
  Worker Zones:                   dal10, dal12
  Version:                        1.11.3_1524
  Owner:                          owner@email.com
  Resource Group ID:              a8a12accd63b437bbd6d58fb6a462ca7
  Resource Group Name:            Default
  ```
  {: screen}

## Obsoleto: Aggiunta di nodi di lavoro autonomi
{: #standalone}

Se hai un cluster che è stato creato prima dell'introduzione dei pool di nodi di lavoro, puoi usare i comandi obsoleti per aggiungere nodi di lavoro autonomi.
{: deprecated}

Se hai un cluster che è stato creato dopo l'introduzione dei pool di nodi di lavoro, non puoi aggiungere nodi di lavoro autonomi. Puoi invece [creare un pool di nodi di lavoro](#add_pool), [ridimensionare un pool di nodi di lavoro esistente](#resize_pool) o [aggiungere una zona a un pool di nodi di lavoro](#add_zone) per aggiungere i nodi di lavoro al tuo cluster.
{: note}

1. Elenca le zone disponibili e seleziona la zona a cui vuoi aggiungere i nodi di lavoro.
   ```
   ibmcloud oc zones
   ```
   {: pre}

2. Elenca le VLAN disponibili in tale zona e prendi nota del loro ID.
   ```
   ibmcloud oc vlans --zone <zone>
   ```
   {: pre}

3. Elenca i profili disponibili in tale zona.
   ```
   ibmcloud oc flavors --zone <zone>
   ```
   {: pre}

4. Aggiungi i nodi di lavoro autonomi al cluster. Per i profili bare metal, specifica `dedicated`.
   ```
   ibmcloud oc worker-add --cluster <cluster_name_or_ID> --workers <number_of_worker_nodes> --public-vlan <public_VLAN_ID> --private-vlan <private_VLAN_ID> --machine-type <flavor> --hardware <shared_or_dedicated>
   ```
   {: pre}

5. Verifica che i nodi di lavoro siano stati creati.
   ```
   ibmcloud oc workers --cluster <cluster_name_or_ID>
   ```
   {: pre}

<br />


## Aggiunta di etichette ai pool di nodi di lavoro esistenti
{: #worker_pool_labels}

Puoi assegnare un'etichetta a un pool di nodi di lavoro quando [crei il pool di nodi di lavoro](#add_pool) oppure in un secondo momento attenendoti alla seguente procedura. Dopo che un pool di nodi di lavoro è stato etichettato, tutti i nodi di lavoro esistenti e successivi prendono questa etichetta. Puoi utilizzare le etichette per distribuire specifici carichi di lavoro solo ai nodi di lavoro nel pool di nodi di lavoro, come ad esempio i [nodi edge per il traffico di rete del programma di bilanciamento del carico](/docs/containers?topic=containers-edge).
{: shortdesc}

Prima di iniziare: [accedi al tuo account. Se applicabile, specifica il gruppo di risorse appropriato. Imposta il contesto per il tuo cluster.](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure)

1.  Elenca i pool di nodi di lavoro nel tuo cluster.
    ```
    ibmcloud oc worker-pools --cluster <cluster_name_or_ID>
    ```
    {: pre}
2.  Per etichettare il pool di nodi di lavoro con un'etichetta `key=value`, utilizza la [API del pool di nodi di lavoro PATCH ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://containers.cloud.ibm.com/global/swagger-global-api/#/clusters/PatchWorkerPool). Formatta il corpo della richiesta come nel seguente esempio JSON.
    ```
    {
      "labels": {"key":"value"},
      "state": "labels"
    }
    ```
    {: codeblock}
3.  Verifica che il pool di nodi di lavoro e il nodo di lavoro abbiano l'etichetta `key=value` che hai assegnato.
    *   Per controllare i pool dei nodi di lavoro:
        ```
        ibmcloud oc worker-pool-get --cluster <cluster_name_or_ID> --worker-pool <worker_pool_name_or_ID>
        ```
        {: pre}
    *   Per controllare i nodi di lavoro:
        1.  Elenca i nodi di lavoro nel pool di nodi di lavoro e annota l'IP privato (**Private IP**).
            ```
            ibmcloud oc workers --cluster <cluster_name_or_ID> --worker-pool <worker_pool_name_or_ID>
            ```
            {: pre}
        2.  Esamina il campo delle etichette (**Labels**) dell'output.
            ```
            oc describe node <worker_node_private_IP>
            ```
            {: pre}

Dopo che hai etichettato il tuo pool di nodi di lavoro, puoi utilizzare l'[etichetta nelle tue distribuzioni dell'applicazione](/docs/containers?topic=containers-app#label) in modo che i tuoi carichi di lavoro vengano eseguiti solo su questi nodi di lavoro oppure le [contaminazioni ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://kubernetes.io/docs/concepts/configuration/taint-and-toleration/) per evitare che le distribuzioni vengano eseguite su questi nodi di lavoro.

<br />


## Autorecovery per i tuoi nodi di lavoro
{: #planning_autorecovery}

I componenti critici, come `containerd`, `kubelet`, `kube-proxy` e `calico`, devono funzionare correttamente per avere un nodo di lavoro Kubernetes integro. Con il passare del tempo questi componenti possono danneggiarsi e lasciare il tuo nodo di lavoro in uno stato non funzionale. I nodi di lavoro non funzionali riducono la capacità totale del cluster e possono causare tempi di inattività per la tua applicazione.
{:shortdesc}

Puoi [configurare i controlli dell'integrità per il nodo di lavoro e abilitare l'Autorecovery](/docs/containers?topic=containers-health#autorecovery). Se Autorecovery rileva un nodo di lavoro non integro in base ai controlli configurati, attiva un'azione correttiva come un ricaricamento del sistema operativo sul nodo di lavoro. Per ulteriori informazioni su come funziona Autorecovery, vedi il [blog Autorecovery ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://www.ibm.com/blogs/bluemix/2017/12/autorecovery-utilizes-consistent-hashing-high-availability/).



