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

# Configurazione di sottoreti e indirizzi IP per i cluster
{: #subnets}

Modifica il pool di indirizzi IP pubblici e privati portatili disponibili per i servizi NLB (network load balancer) aggiungendo sottoreti al tuo cluster {{site.data.keyword.openshiftlong}}.
{:shortdesc}

## Panoramica della rete in Red Hat OpenShift on IBM Cloud
{: #basics}

Comprendi i concetti di base della rete nei cluster Red Hat OpenShift on IBM Cloud. Red Hat OpenShift on IBM Cloud utilizza VLAN, sottoreti e indirizzi IP per fornire connettività di rete ai componenti cluster.
{: shortdesc}


### VLAN
{: #basics_vlans}

Quando crei un cluster, i nodi di lavoro del cluster vengono connessi automaticamente a una VLAN. Una VLAN configura un gruppo di nodi di lavoro e pod come se fossero collegati allo stesso cavo fisico e fornisce un canale per la connettività tra i nodi di lavoro e i pod.
{: shortdesc}

<dl>
<dt>VLAN per i cluster gratuiti</dt>
<dd>Per i cluster gratuiti, i nodi di lavoro del cluster sono connessi a una VLAN privata e a una VLAN pubblica di proprietà di IBM per impostazione predefinita. Poiché IBM controlla le VLAN, le sottoreti e gli indirizzi IP, non puoi creare dei cluster multizona o aggiungere sottoreti al tuo cluster e puoi solo utilizzare i servizi NodePort per esporre la tua applicazione.</dd>
<dt>VLAN per i cluster standard</dt>
<dd>Nei cluster standard, la prima volta che crei un cluster in una zona, viene automaticamente eseguito il provisioning di una VLAN pubblica e di una VLAN privata in tale zona per tuo conto nel tuo account dell'infrastruttura IBM Cloud. Per ogni cluster successivo che crei in tale zona, devi specificare la coppia di VLAN che vuoi usare nella zona. Puoi riutilizzare le stesse VLAN pubbliche e private create per te, poiché le VLAN possono essere condivise da più cluster.</br>
</br>Puoi collegare i tuoi nodi di lavoro a una VLAN pubblica e alla VLAN privata o solo alla VLAN privata. Se vuoi collegare i tuoi nodi di lavoro solo a una VLAN privata, puoi utilizzare l'ID di una VLAN privata esistente o [creare una VLAN privata](/docs/cli/reference/ibmcloud?topic=cloud-cli-manage-classic-vlans#sl_vlan_create) e utilizzare l'ID durante la creazione del cluster.</dd></dl>

Per visualizzare le VLAN di cui viene eseguito il provisioning in ciascuna zona per il tuo account, esegui `ibmcloud oc vlans --zone <zone>.` Per visualizzare le VLAN su cui viene eseguito il provisioning di un cluster, esegui `ibmcloud oc cluster-get --cluster <cluster_name_or_ID> --showResources` e cerca la sezione **Subnet VLANs**.

L'infrastruttura IBM Cloud gestisce le VLAN di cui viene eseguito automaticamente il provisioning quando crei il tuo primo cluster in una zona. Se lasci che una VLAN diventi inutilizzata, come ad esempio rimuovendo tutti i nodi di lavoro da essa, l'infrastruttura IBM Cloud la reclama. In seguito, se hai bisogno di una nuova VLAN, [contatta il supporto {{site.data.keyword.cloud_notm}}](/docs/infrastructure/vlans?topic=vlans-ordering-premium-vlans#ordering-premium-vlans).

**Posso modificare la mia decisione relativa alla VLAN in un secondo momento?**</br>
Puoi cambiare la tua configurazione della VLAN modificando i pool di nodi di lavoro nel tuo cluster. Per ulteriori informazioni, vedi [Modifica delle connessioni VLAN dei tuoi nodi di lavoro](/docs/containers?topic=containers-cs_network_cluster#change-vlans).

### Sottoreti e indirizzi IP
{: #basics_subnets}

In aggiunta ai nodi di lavoro e ai pod, sulle VLAN viene eseguito automaticamente anche il provisioning delle sottoreti. Le sottoreti forniscono la connettività di rete ai tuoi componenti del cluster assegnando loro degli indirizzi IP.
{: shortdesc}

Delle seguenti reti viene eseguito automaticamente il provisioning sulle VLAN pubbliche e private predefinite:

**Sottoreti VLAN pubbliche**
* La sottorete pubblica primaria determina gli indirizzi IP pubblici che vengono assegnati ai nodi di lavoro durante la creazione del cluster. Più cluster sulla stessa VLAN possono condividere una sottorete pubblica primaria.
* La sottorete pubblica portatile è associata solo a un singolo cluster e fornisce al cluster 8 indirizzi IP pubblici. 3 IP sono riservati per le funzioni dell'infrastruttura IBM Cloud. 1 IP viene utilizzato dall'ALB Ingress pubblico predefinito e 4 IP possono essere utilizzati per creare servizi NLB (network load balancer) pubblici o più ALB pubblici. Gli IP pubblici portatili sono indirizzi IP fissi e permanenti che possono essere utilizzati per accedere agli NLB o agli ALB su Internet. Se hai bisogno di più di 4 IP per gli NLB o gli ALB, vedi [Aggiunta di indirizzi IP portatili](/docs/containers?topic=containers-subnets#adding_ips).

**Sottoreti VLAN private**
* La sottorete privata primaria determina gli indirizzi IP privati che vengono assegnati ai nodi di lavoro durante la creazione del cluster. Più cluster sulla stessa VLAN possono condividere una sottorete privata primaria.
* La sottorete privata portatile è associata solo a un singolo cluster e fornisce al cluster 8 indirizzi IP privati. 3 IP sono riservati per le funzioni dell'infrastruttura IBM Cloud. 1 IP viene utilizzato dall'ALB Ingress privato predefinito e 4 IP possono essere utilizzati per creare servizi NLB (network load balancer) privati o più ALB privati. Gli IP privati portatili sono indirizzi IP fissi e permanenti che possono essere utilizzati per accedere agli NLB o agli ALB su una rete privata. Se hai bisogno di più di 4 IP per gli NLB o gli ALB privati, vedi [Aggiunta di indirizzi IP portatili](/docs/containers?topic=containers-subnets#adding_ips).

Per visualizzare tutte le sottoreti di cui viene eseguito il provisioning nel tuo account, esegui `ibmcloud oc subnets`. Per visualizzare le sottoreti pubbliche e private portatili associate a un singolo cluster, puoi eseguire `ibmcloud oc cluster-get --cluster <cluster_name_or_ID> --showResources` e cercare la sezione **Subnet VLANs**.

In {{site.data.keyword.containerlong_notm}}, le VLAN hanno un limite di 40 sottoreti. Se raggiungi questo limite, controlla prima se puoi [riutilizzare le sottoreti nella VLAN per creare nuovi cluster](/docs/containers?topic=containers-subnets#subnets_custom). Se hai bisogno di una nuova VLAN, ordinane una [contattando il supporto {{site.data.keyword.cloud_notm}}](/docs/infrastructure/vlans?topic=vlans-ordering-premium-vlans#ordering-premium-vlans). Quindi [crea un cluster](/docs/containers?topic=containers-cli-plugin-kubernetes-service-cli#cs_cluster_create) che utilizzi questa nuova VLAN.
{: note}

**L'indirizzo IP per i miei nodi di lavoro subisce variazioni?**</br>
Al tuo nodo di lavoro viene assegnato un indirizzo IP sulle VLAN pubbliche o private utilizzate dal tuo cluster. Una volta eseguito il provisioning del tuo nodo di lavoro, gli indirizzi IP restano immutati. Ad esempio, gli indirizzi IP del nodo di lavoro persistono attraverso le operazioni `reload`, `reboot` e `update`. Inoltre, l'indirizzo IP privato del nodo di lavoro viene utilizzato per l'identità di tale nodo nella maggior parte dei comandi `oc`. Se modifichi le VLAN utilizzate dal pool di nodi di lavoro, i nuovi nodi di lavoro di cui viene eseguito il provisioning in tale pool utilizzano le nuove VLAN per i propri indirizzi IP. Gli indirizzi IP
del nodo di lavoro esistente non cambiano, ma puoi scegliere di rimuovere i nodi di lavoro che utilizzano le vecchie VLAN.

### Segmentazione di rete
{: #basics_segmentation}

La segmentazione di rete descrive l'approccio di dividere una rete in più sottoreti. Le applicazioni eseguite in una sottorete non possono vedere o accedere alle applicazioni in un'altra sottorete. Per ulteriori informazioni sulle opzioni di segmentazione della rete e su come sono correlate alle VLAN, vedi [questo argomento sulla sicurezza del cluster](/docs/containers?topic=containers-security#network_segmentation).
{: shortdesc}

Tuttavia, in diverse situazioni, i componenti del tuo cluster devono essere autorizzati a comunicare su più VLAN private. Ad esempio, se vuoi creare un cluster multizona, hai più VLAN per un cluster o hai più sottoreti sulla stessa VLAN, i nodi di lavoro che si trovano su sottoreti diverse nella stessa VLAN o in VLAN diverse non possono comunicare automaticamente tra loro. Devi abilitare una VRF (Virtual Router Function) o lo spanning della VLAN per il tuo account dell'infrastruttura IBM Cloud.

**Cosa sono le VRF (Virtual Router Function) e lo spanning della VLAN?**</br>

<dl>
<dt>[VRF (Virtual Router Function)](/docs/infrastructure/direct-link?topic=direct-link-overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud#overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud)</dt>
<dd>Una VRF consente a tutte le VLAN e sottoreti nel tuo account dell'infrastruttura di comunicare tra loro. Inoltre, una VRF è necessaria per consentire ai tuoi nodi di lavoro e al master di comunicare sull'endpoint del servizio privato. Per abilitare VRF, [contatta il tuo rappresentante dell'account dell'infrastruttura IBM Cloud](/docs/infrastructure/direct-link?topic=direct-link-overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud#how-you-can-initiate-the-conversion). Per controllare se una VRF è già abilitata, utilizza il comando `ibmcloud account show`. Nota che VRF elimina l'opzione di spanning della VLAN per il tuo account, poiché tutte le VLAN sono in grado di comunicare a meno che non configuri un dispositivo gateway per gestire il traffico.</dd>
<dt>[Spanning della VLAN](/docs/infrastructure/vlans?topic=vlans-vlan-spanning#vlan-spanning)</dt>
<dd>Se non puoi o non vuoi abilitare VRF, abilita lo spanning della VLAN. Per eseguire questa azione, ti serve l'[autorizzazione dell'infrastruttura](/docs/containers?topic=containers-users#infra_access) **Rete > Gestisci il VLAN Spanning di rete** oppure puoi richiedere al proprietario dell'account di abilitarlo. Per controllare se lo spanning della VLAN è già abilitato, utilizza il [comando `ibmcloud oc vlan-spanning-get --region <region>`](/docs/containers?topic=containers-cli-plugin-kubernetes-service-cli#cs_vlan_spanning_get).
Nota che, se scegli di abilitare lo spanning della VLAN invece di una VRF, non puoi abilitare l'endpoint del servizio privato.</dd>
</dl>

**In che modo VRF o lo spanning della VLAN influiscono sulla segmentazione di rete?**</br>

Quando abiliti VRF o lo spanning della VLAN, qualsiasi sistema connesso a qualsiasi VLAN privata nello stesso account {{site.data.keyword.cloud_notm}} può comunicare con i nodi di lavoro. Puoi isolare il tuo cluster da altri sistemi sulla rete privata applicando delle [politiche di rete privata Calico](/docs/containers?topic=containers-network_policies#isolate_workers). {{site.data.keyword.containerlong_notm}} è inoltre compatibile con tutte le [offerte firewall dell'infrastruttura IBM Cloud ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://www.ibm.com/cloud-computing/bluemix/network-security). Puoi configurare un firewall, ad esempio una [VRA (Virtual Router Appliance)](/docs/infrastructure/virtual-router-appliance?topic=virtual-router-appliance-about-the-vra), con politiche di rete personalizzate per fornire una sicurezza di rete dedicata per il tuo cluster standard e per rilevare e risolvere intrusioni di rete.

<br />



## Utilizzo delle sottoreti esistenti per creare un cluster
{: #subnets_custom}

Quando crei un cluster standard, le sottoreti vengono create automaticamente per tuo conto. Tuttavia, invece di utilizzare le sottoreti di cui viene eseguito il provisioning automaticamente, puoi utilizzare le sottoreti portatili esistenti dal tuo account dell'infrastruttura IBM Cloud oppure riutilizzare le sottoreti da un cluster eliminato.
{:shortdesc}

Utilizza questa opzione per mantenere stabili gli indirizzi IP statici tra le rimozioni e le creazioni di cluster o per ordinare blocchi di indirizzi IP più grandi. Se invece vuoi ottenere più indirizzi IP pubblici o provati portatili per creare i servizi NLB (network load balancer) o ALB (application load balancer) Ingress, vedi [Aggiunta di indirizzi IP portatili](#adding_ips).

Tutte le sottoreti che erano precedentemente ordinate automaticamente durante la creazione del cluster vengono immediatamente eliminate dopo che elimini un cluster e non puoi riutilizzare le sottoreti per creare un nuovo cluster. Tuttavia, se [hai aggiunto manualmente le tue sottoreti al cluster ](#subnet_user_managed), le sottoreti non vengono eliminate quando elimini il cluster. Puoi riutilizzare le sottoreti per creare un nuovo cluster.
{: note}

Prima di iniziare:
- [Accedi al tuo account. Se applicabile, specifica il gruppo di risorse appropriato. Imposta il contesto per il tuo cluster.](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure)
- Per riutilizzare le sottoreti private gestite dall'utente da un cluster di cui non hai più bisogno, elimina il cluster non necessario.
   ```
   ibmcloud oc cluster-rm --cluster <cluster_name_or_ID>
   ```
   {: pre}

</br>Per creare un cluster utilizzando le sottoreti esistenti:

1. Ottieni l'ID della sottorete e l'ID della VLAN su cui si trova la sottorete.

    ```
    ibmcloud oc subnets
    ```
    {: pre}

    In questo output di esempio, l'ID sottorete è `1602829` e l'ID VLAN è `2234945`:
    ```
    Getting subnet list...
    OK
    ID        Network             Gateway          VLAN ID   Type      Bound Cluster
    1550165   10.xxx.xx.xxx/26    10.xxx.xx.xxx    2234947   private
    1602829   169.xx.xxx.xxx/28   169.xx.xxx.xxx   2234945   public
    ```
    {: screen}

2. [Crea un cluster nella CLI](/docs/containers?topic=containers-clusters#clusters_cli_steps) utilizzando l'ID VLAN che hai identificato. Includi l'indicatore `--no-subnet` per impedire la creazione automatica di una nuova sottorete IP pubblica portatile e di una nuova sottorete IP privata portatile.

    ```
    ibmcloud oc cluster-create --zone dal10 --machine-type b3c.4x16 --no-subnet --public-vlan 2234945 --private-vlan 2234947 --workers 3 --name my_cluster
    ```
    {: pre}
    Se non riesci a ricordare qual è la zona in cui si trova la VLAN per l'indicatore `--zone`, puoi controllare se la VLAN si trova in una specifica zona eseguendo `ibmcloud oc vlans --zone <zone>`.
    {: tip}

3.  Verifica che il cluster sia stato creato. Possono essere necessari fino a 15 minuti per l'ordine delle macchine del nodo di lavoro e per la configurazione e il provisioning del cluster nel tuo account.

    ```
    ibmcloud oc clusters
    ```
    {: pre}

    Quando il provisioning del tuo cluster è stato eseguito completamente, lo stato (**State**) cambia in `deployed`.

    ```
    Name         ID                                   State      Created          Workers    Zone      Version     Resource Group Name
    mycluster    aaf97a8843a29941b49a598f516da72101   deployed   20170201162433   3          dal10     1.13.8      Default
    ```
    {: screen}

4.  Controlla lo stato dei nodi di lavoro.

    ```
    ibmcloud oc workers --cluster <cluster_name_or_ID>
    ```
    {: pre}

    Prima di continuare al passo successivo, i nodi di lavoro devono essere pronti. Lo stato (**State**) cambia in `normal` e la condizione (**Status**) è `Ready`.

    ```
    ID                                                  Public IP        Private IP     Machine Type   State      Status   Zone     Version
    prod-dal10-pa8dfcc5223804439c87489886dbbc9c07-w1    169.xx.xxx.xxx   10.xxx.xx.xxx  free           normal     Ready    dal10      1.13.8
    ```
    {: screen}

5.  Aggiungi la sottorete al tuo cluster specificando l'ID sottorete. Quando rendi disponibile una sottorete a un cluster, per te viene creata una mappa di configurazione Kubernetes che include tutti gli indirizzi IP pubblici portatili che puoi utilizzare. Se non esiste alcun ALB Ingress nella zona dove si trova la VLAN della sottorete, vengono automaticamente utilizzati un indirizzo IP privato e uno pubblico portatili per creare gli ALB pubblico e privato per tale zona. Puoi utilizzare tutti gli altri indirizzi IP pubblici e privati portatili dalla sottorete per creare i servizi NLB per le tue applicazioni.
  * Per aggiungere una sottorete che esiste nel tuo account dell'infrastruttura IBM Cloud:
      ```
      ibmcloud oc cluster-subnet-add --cluster <cluster_name_or_id> --subnet-id <subnet_ID>
      ```
      {: pre}

      Comando di esempio:
      ```
      ibmcloud oc cluster-subnet-add --cluster mycluster --subnet-id 807861
      ```
      {: screen}

  * Per aggiungere una sottorete privata gestita dall'utente da una rete in loco:
      ```
      ibmcloud oc cluster-user-subnet-add --cluster <cluster_name> --subnet-cidr <subnet_CIDR> --private-vlan <private_VLAN>
      ```
      {: pre}

      Comando di esempio:

      ```
      ibmcloud oc cluster-user-subnet-add --cluster mycluster --subnet-cidr 10.xxx.xx.xxx/24 --private-vlan 2234947
      ```
      {: pre}

6. Verifica che la sottorete sia aggiunta al tuo cluster.

    ```
    ibmcloud oc cluster-get --showResources <cluster_name>
    ```
    {: pre}

7. **Importante**: per abilitare le comunicazioni tra i nodi di lavoro che si trovano su sottoreti differenti nella stessa VLAN, devi [abilitare l'instradamento tra le sottoreti sulla stessa VLAN](#subnet-routing).

<br />


## Gestione degli indirizzi IP portatili esistenti
{: #managing_ips}

Per impostazione predefinita, 4 indirizzi IP pubblici portatili e 4 privati portatili possono essere utilizzati per esporre le singole applicazioni alla rete pubblica o privata [creando un servizio NLB (network load balancer)](/docs/containers?topic=containers-loadbalancer). Per creare un servizio <staging create-alb> o ALB</staging create-alb>, devi avere almeno un indirizzo IP portatile del tipo corretto disponibile. Puoi visualizzare gli indirizzi IP portatili disponibili oppure liberare un indirizzo IP portatile utilizzato.
{: shortdesc}

### Visualizzazione degli indirizzi IP pubblici portatili disponibili
{: #review_ip}

Per elencare tutti gli indirizzi IP portatili nel tuo cluster, sia quelli usati che quelli disponibili, puoi eseguire questo comando:
{: shortdesc}

```
oc get cm ibm-cloud-provider-vlan-ip-config -n kube-system -o yaml
```
{: pre}

Per elencare solo gli indirizzi IP pubblici portatili disponibili per creare gli NLB pubblici o più ALB pubblici, puoi attenerti alla seguente procedura:

Prima di iniziare:
-  Assicurati di disporre del [ruolo del servizio {{site.data.keyword.cloud_notm}} IAM **Scrittore** o **Gestore**](/docs/containers?topic=containers-users#platform) per lo spazio dei nomi `default`.
- [Accedi al tuo account. Se applicabile, specifica il gruppo di risorse appropriato. Imposta il contesto per il tuo cluster.](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure)

Per elencare gli indirizzi IP pubblici portatili che sono disponibili:

1.  Crea un file di configurazione del servizio Kubernetes denominato `myservice.yaml` e definisci un servizio di tipo `LoadBalancer` con un indirizzo IP dell'NLB fittizio. Il seguente esempio utilizza l'indirizzo IP 1.1.1.1 come indirizzo IP dell'NLB. Sostituisci `<zone>` con la zona dove desideri controllare l'eventuale presenza di IP disponibili.

    ```
    apiVersion: v1
    kind: Service
    metadata:
      labels:
        run: myservice
      name: myservice
      namespace: default
      annotations:
        service.kubernetes.io/ibm-load-balancer-cloud-provider-zone: "<zone>"
    spec:
      ports:
      - port: 80
        protocol: TCP
        targetPort: 80
      selector:
        run: myservice
      sessionAffinity: None
      type: LoadBalancer
      loadBalancerIP: 1.1.1.1
    ```
    {: codeblock}

2.  Crea il servizio nel tuo cluster.

    ```
    oc apply -f myservice.yaml
    ```
    {: pre}

3.  Controlla il servizio.

    ```
    oc describe service myservice
    ```
    {: pre}

    La creazione di questo servizio non riesce perché il master Kubernetes non può trovare l'indirizzo IP dell'NLB specificato nella mappa di configurazione Kubernetes. Quando esegui questo comando, puoi visualizzare il messaggio di errore e un elenco di indirizzi IP pubblici disponibili per il cluster.

    ```
    Error on cloud load balancer a8bfa26552e8511e7bee4324285f6a4a for service default/myservice with UID 8bfa2655-2e85-11e7-bee4-324285f6a4af: Requested cloud provider IP 1.1.1.1 is not available. The following cloud provider IP addresses are available: <list_of_IP_addresses>
    ```
    {: screen}

<br />


### Liberazione degli indirizzi IP utilizzati
{: #free}

Puoi liberare un indirizzo IP portatile utilizzato eliminando il servizio NLB (network load balancer) o disabilitando l'ALB (application load balancer) Ingress che sta utilizzando tale indirizzo IP portatile.
{:shortdesc}

Prima di iniziare:
-  Assicurati di disporre del [ruolo del servizio {{site.data.keyword.cloud_notm}} IAM **Scrittore** o **Gestore**](/docs/containers?topic=containers-users#platform) per lo spazio dei nomi `default`.
- [Accedi al tuo account. Se applicabile, specifica il gruppo di risorse appropriato. Imposta il contesto per il tuo cluster.](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure)

Per eliminare un NLB o disabilitare un ALB:

1. Elenca i servizi disponibili nel tuo cluster.
    ```
    oc get services | grep LoadBalancer
    ```
    {: pre}

2. Rimuovi il servizio del programma di bilanciamento del carico o disabilita l'ALB che utilizza un indirizzo IP pubblico o privato.
  * Elimina un NLB:
    ```
    oc delete service <service_name>
    ```
    {: pre}
  * Disabilita un ALB:
    ```
    ibmcloud oc alb-configure --albID <ALB_ID> --disable
    ```
    {: pre}

<br />


## Aggiunta di indirizzi IP portatili
{: #adding_ips}

Per impostazione predefinita, 4 indirizzi IP pubblici portatili e 4 privati portatili possono essere utilizzati per esporre le singole applicazioni alla rete pubblica o privata [creando un servizio NLB (network load balancer)](/docs/containers?topic=containers-loadbalancer). Per creare più di 4 NLB pubblici e 4 privati, puoi ottenere ulteriori indirizzi IP portatili aggiungendo delle sottoreti di rete al cluster.
{: shortdesc}

Quando rendi disponibile una sottorete a un cluster, gli indirizzi IP di questa sottorete vengono utilizzati per scopi di rete del cluster. Per evitare conflitti di indirizzi IP, assicurati di utilizzare una sottorete con un solo cluster. Non utilizzare una sottorete per più cluster o per altri
scopi al di fuori di {{site.data.keyword.containerlong_notm}}
contemporaneamente.
{: important}

### Aggiunta di IP portatili ordinando più sottoreti
{: #request}

Puoi ottenere più indirizzi IP portatili per i servizi NLB creando una nuova sottorete in un account dell'infrastruttura IBM Cloud e rendendola disponibile al tuo cluster specificato.
{:shortdesc}

Gli indirizzi IP pubblici portatili vengono addebitati mensilmente. Se rimuovi gli indirizzi IP pubblici portatili dopo aver eseguito il provisioning della tua sottorete, devi comunque pagare l'addebito mensile anche se li hai utilizzati solo per un breve periodo di tempo.
{: note}

Prima di iniziare:
-  Assicurati di disporre del [ruolo della piattaforma {{site.data.keyword.cloud_notm}} IAM **Operatore** o **Amministratore**](/docs/containers?topic=containers-users#platform) per il cluster.
- [Accedi al tuo account. Se applicabile, specifica il gruppo di risorse appropriato. Imposta il contesto per il tuo cluster.](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure)

Per ordinare una sottorete:

1. Esegui il provisioning di una sottorete.

    ```
    ibmcloud oc cluster-subnet-create --cluster <cluster_name_or_id> --size <subnet_size> --vlan <VLAN_ID>
    ```
    {: pre}

    <table>
    <caption>Descrizione dei componenti di questo comando</caption>
    <thead>
    <th colspan=2><img src="images/idea.png" alt="Icona Idea"/> Descrizione dei componenti di questo comando</th>
    </thead>
    <tbody>
    <tr>
    <td><code><em>&lt;cluster_name_or_id&gt;</em></code></td>
    <td>Sostituisci <code>&lt;cluster_name_or_id&gt;</code> con il nome o l'ID del cluster.</td>
    </tr>
    <tr>
    <td><code><em>&lt;subnet_size&gt;</em></code></td>
    <td>Sostituisci <code>&lt;subnet_size&gt;</code> con il numero di indirizzi IP che vuoi creare nella sottorete portatile. I valori accettati sono 8, 16, 32 o 64. <p class="note"> Quando aggiungi gli indirizzi IP portatili per la tua sottorete, tre indirizzi IP vengono utilizzati per stabilire un collegamento di rete interno al cluster. Non puoi utilizzare questi tre indirizzi IP per i tuoi ALB (application load balancer) Ingress o per creare servizi NLB (network load balancer). Ad esempio, se richiedi otto indirizzi IP pubblici portatili, puoi utilizzarne cinque per esporre le tue applicazioni pubblicamente.</p> </td>
    </tr>
    <tr>
    <td><code><em>&lt;VLAN_ID&gt;</em></code></td>
    <td>Sostituisci <code>&lt;VLAN_ID&gt;</code> con l'ID della VLAN pubblica o privata su cui vuoi assegnare gli indirizzi IP pubblici o privati portatili. Devi selezionare una VLAN pubblica o privata a cui è connesso un nodo di lavoro esistente. Per riesaminare le VLAN pubbliche o private a cui sono connessi i tuoi nodi di lavoro, esegui <code>ibmcloud oc cluster-get --cluster &lt;cluster&gt; --showResources</code> e cerca la sezione <strong>Subnet VLANs</strong> nell'output. Il provisioning della sottorete viene eseguito nella stessa zona in cui si trova la VLAN.</td>
    </tr>
    </tbody></table>

2. Verifica che la sottorete sia stata creata e aggiunta correttamente al tuo cluster. Il CIDR della sottorete viene elencato nella sezione **Subnet VLANs**.

    ```
    ibmcloud oc cluster-get --cluster <cluster_name_or_ID> --showResources
    ```
    {: pre}

    Nell'output di esempio, è stata aggiunta una seconda sottorete alla VLAN pubblica `2234945`:
    ```
    Subnet VLANs
    VLAN ID   Subnet CIDR          Public   User-managed
    2234947   10.xxx.xx.xxx/29     false    false
    2234945   169.xx.xxx.xxx/29    true     false
    2234945   169.xx.xxx.xxx/29    true     false
    ```
    {: screen}

3. **Importante**: per abilitare le comunicazioni tra i nodi di lavoro che si trovano su sottoreti differenti nella stessa VLAN, devi [abilitare l'instradamento tra le sottoreti sulla stessa VLAN](#subnet-routing).

### Aggiunta di IP portatili aggiungendo sottoreti esistenti al tuo cluster
{: #add-existing}

Puoi ottenere più indirizzi IP portatili per i servizi NLB rendendo una sottorete esistente in un account dell'infrastruttura IBM disponibile al tuo cluster.
{:shortdesc}

Prima di iniziare:
-  Assicurati di disporre del [ruolo della piattaforma {{site.data.keyword.Bluemix_notm}} IAM **Operator** (operatore) o **Administrator** (amministratore)](/docs/containers?topic=containers-users#platform) per il cluster.
- [Accedi al tuo account. Se applicabile, specifica il gruppo di risorse appropriato. Imposta il contesto per il tuo cluster.](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure)

Per rendere una sottorete disponibile al tuo cluster:

1. Riesamina gli ID delle VLAN pubbliche o private su cui desideri allocare gli indirizzi IP pubblici o privati portatili. Devi selezionare una VLAN pubblica o privata a cui è connesso un nodo di lavoro esistente.
  ```
  ibmcloud oc cluster-get --cluster <cluster_name_or_id> --showResources
  ```
  {: pre}

  Nell'output, cerca i **VLAN ID** nella sezione **Subnet VLANs**. Output di esempio:
  ```
  Subnet VLANs
  VLAN ID   Subnet CIDR         Public   User-managed
  2234947   10.xxx.xx.xxx/29    false    false
  2234945   169.xx.xxx.xxx/29  true    false
  ```
  {: screen}

2. Ottieni l'ID della sottorete da utilizzare. Assicurati che la sottorete sia su uno degli ID VLAN che hai trovato nel passo precedente e che non sia già associata a un altro cluster.
  ```
  ibmcloud oc subnets
  ```
  {: pre}

  In questo output di esempio, l'ID sottorete è `1602829`, che si trova sul VLAN ID (ID VLAN) `2234945`:
  ```
  Getting subnet list...
    OK
    ID        Network             Gateway          VLAN ID   Type      Bound Cluster
    1550165   10.xxx.xx.xxx/26    10.xxx.xx.xxx    2234947   private
    1602829   169.xx.xxx.xxx/28   169.xx.xxx.xxx   2234945   public
  ```
  {: screen}

3. Rendi la sottorete disponibile per il tuo cluster.
  ```
  ibmcloud oc cluster-subnet-add --cluster <cluster_name_or_id> --subnet-id <subnet_ID>
  ```
  {: pre}

4. Verifica che la sottorete sia stata creata e aggiunta correttamente al tuo cluster. Il CIDR della sottorete viene elencato nella sezione **Subnet VLANs**.
  ```
  ibmcloud oc cluster-get --showResources <cluster_name_or_ID>
  ```
  {: pre}

  Nell'output di esempio, è stata aggiunta una seconda sottorete alla VLAN pubblica `2234945`:
  ```
  Subnet VLANs
    VLAN ID   Subnet CIDR          Public   User-managed
    2234947   10.xxx.xx.xxx/29     false    false
    2234945   169.xx.xxx.xxx/29    true     false
    2234945   169.xx.xxx.xxx/29    true     false
  ```
  {: screen}

5. **Importante**: per abilitare le comunicazioni tra i nodi di lavoro che si trovano su sottoreti differenti nella stessa VLAN, devi [abilitare l'instradamento tra le sottoreti sulla stessa VLAN](#subnet-routing).

<br />



### Aggiunta di IP privati portatili aggiungendo sottoreti gestite dall'utente alle VLAN private
{: #subnet_user_managed}

Puoi ottenere più IP privati portatili per i servizi NLB (network load balancer) rendendo una sottorete da una rete in loco disponibile al tuo cluster.
{:shortdesc}

Vuoi invece riutilizzare le sottoreti portatili esistenti nella tuo account dell'infrastruttura IBM Cloud? Vedi [Utilizzo delle sottoreti dell'infrastruttura IBM Cloud esistenti o personalizzate per creare un cluster](#subnets_custom).
{: tip}

Requisiti:
- Le sottoreti gestite dall'utente possono essere aggiunte solo a VLAN private.
- Il limite di lunghezza del prefisso della sottorete è da /24 a /30. Ad esempio, `169.xx.xxx.xxx/24` specifica 253 indirizzi IP privati utilizzabili, mentre `169.xx.xxx.xxx/30` specifica 1 indirizzo IP privato utilizzabile.
- Il primo indirizzo IP nella sottorete deve essere utilizzato come gateway della sottorete.

Prima di iniziare:
- Configura l'instradamento del traffico di rete in entrata e in uscita della sottorete esterna.
- Conferma di disporre di connettività VPN tra il gateway di rete del data center in loco e la VRA (Virtual Router Appliance) di rete privata o il servizio VPN strongSwan in esecuzione nel tuo cluster. In alternativa, assicurati di avere una connessione DirectLink configurata tra il tuo cluster e la rete data center in loco. Per ulteriori informazioni, vedi [Configurazione della connettività VPN](/docs/containers?topic=containers-vpn).
-  Assicurati di disporre del [ruolo della piattaforma {{site.data.keyword.cloud_notm}} IAM **Operatore** o **Amministratore**](/docs/containers?topic=containers-users#platform) per il cluster.
- [Accedi al tuo account. Se applicabile, specifica il gruppo di risorse appropriato. Imposta il contesto per il tuo cluster.](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure)


Per aggiungere una sottorete da una rete in loco:

1. Visualizza l'ID della VLAN privata del tuo cluster. Individua la sezione **Subnet VLANs**. Nel campo **User-managed**, identifica l'ID della VLAN con _false_.

    ```
    ibmcloud oc cluster-get --cluster <cluster_name> --showResources <cluster_name>
    ```
    {: pre}

    ```
    Subnet VLANs
  VLAN ID   Subnet CIDR         Public   User-managed
  2234947   10.xxx.xx.xxx/29    false    false
  2234945   169.xx.xxx.xxx/29  true    false
    ```
    {: screen}

2. Aggiungi la sottorete esterna alla tua VLAN privata. Gli indirizzi IP privati portatili vengono aggiunti alla mappa di configurazione del cluster.

    ```
    ibmcloud oc cluster-user-subnet-add --cluster <cluster_name> --subnet-cidr <subnet_CIDR> --private-vlan <private_VLAN>
    ```
    {: pre}

    Esempio:

    ```
    ibmcloud oc cluster-user-subnet-add --cluster mycluster --subnet-cidr 10.xxx.xx.xxx/24 --private-vlan 2234947
    ```
    {: pre}

3. Verifica che la sottorete fornita dall'utente sia stata aggiunta. Il campo **User-managed** è _true_.

    ```
    ibmcloud oc cluster-get --showResources <cluster_name>
    ```
    {: pre}

    In questo output di esempio, una seconda sottorete è stata aggiunta alla VLAN privata `2234947`:
    ```
    Subnet VLANs
    VLAN ID   Subnet CIDR       Public   User-managed
    2234947   10.xxx.xx.xxx/29  false    false
    2234945   169.xx.xxx.xxx/29 true     false
    2234947   10.xxx.xx.xxx/24  false    true
    ```
    {: screen}

4. [Abilita l'instradamento tra sottoreti sulla stessa VLAN](#subnet-routing).

5. Aggiungi un [servizio NLB (network load balancer) privato](/docs/containers?topic=containers-loadbalancer) oppure abilita un [ALB Ingress privato](/docs/containers?topic=containers-ingress#private_ingress) per accedere alla tua applicazione sulla rete privata. Per utilizzare un indirizzo IP privato dalla sottorete che hai aggiunto, devi specificare un indirizzo IP dal CIDR della sottorete. Diversamente, viene scelto a caso un indirizzo IP dalle sottoreti dell'infrastruttura IBM Cloud o dalle sottoreti fornite dall'utente sulla VLAN privata.

<br />


## Gestione dell'instradamento di sottorete
{: #subnet-routing}

Se hai più VLAN per un cluster, più sottoreti sulla stessa VLAN o un cluster multizona, devi abilitare una [VRF (Virtual Router Function)](/docs/infrastructure/direct-link?topic=direct-link-overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud#overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud) per il tuo account dell'infrastruttura IBM Cloud in modo che i tuoi nodi di lavoro possano comunicare tra loro sulla rete privata. Per abilitare VRF, [contatta il tuo rappresentante dell'account dell'infrastruttura IBM Cloud](/docs/infrastructure/direct-link?topic=direct-link-overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud#how-you-can-initiate-the-conversion). Per controllare se una VRF è già abilitata, utilizza il comando `ibmcloud account show`. Se non puoi o non vuoi abilitare VRF, abilita lo [spanning della VLAN](/docs/infrastructure/vlans?topic=vlans-vlan-spanning#vlan-spanning). Per eseguire questa azione, ti serve l'[autorizzazione dell'infrastruttura](/docs/containers?topic=containers-users#infra_access) **Rete > Gestisci il VLAN Spanning di rete** oppure puoi richiedere al proprietario dell'account di abilitarlo. Per controllare se lo spanning della VLAN è già abilitato, utilizza il [comando `ibmcloud oc vlan-spanning-get --region <region>`](/docs/containers?topic=containers-cli-plugin-kubernetes-service-cli#cs_vlan_spanning_get).

Esamina i seguenti scenari in cui è richiesto anche lo spanning della VLAN.

l'opzione di spanning della VLAN è disabilitata per i cluster creati in un account abilitato alla VRF. Quando la VRF è abilitata, tutte le VLAN nell'account possono automaticamente comunicare tra loro sulla rete privata. Per ulteriori informazioni, vedi [Pianificazione della configurazione di rete del tuo cluster: comunicazioni tra i nodi di lavoro](/docs/containers?topic=containers-plan_clusters#worker-worker).
{: note}

### Abilitazione dell'instradamento tra sottoreti primarie sulla stessa VLAN
{: #vlan-spanning}

Quando crei un cluster, viene eseguito il provisioning della sottorete pubblica e di quella privata primarie sulla VLAN pubbliche e private. La sottorete pubblica primaria termina in `/28` e fornisce 14 IP pubblici per i nodi di lavoro. La sottorete privata primaria termina in `/26` e fornisce gli IP privati per un massimo di 62 nodi di lavoro.
{:shortdesc}

Potresti superare i 14 IP pubblici e i 62 privati iniziali per i nodi di lavoro disponendo di un cluster di grandi dimensioni o di diversi cluster più piccoli nella stessa ubicazione sulla stessa VLAN. Quando una sottorete pubblica o privata raggiunge il limite di nodi di lavoro, viene ordinata un'altra sottorete primaria nella stessa VLAN.

Per garantire che i nodi di lavoro in queste sottoreti primarie sulla stessa VLAN possano comunicare, devi attivare lo spanning della VLAN. Per istruzioni, vedi [Abilita o disabilita lo spanning della VLAN](/docs/infrastructure/vlans?topic=vlans-vlan-spanning#vlan-spanning).

Per controllare se lo spanning della VLAN è già abilitato, utilizza il [comando `ibmcloud oc vlan-spanning-get --region <region>`](/docs/containers?topic=containers-cli-plugin-kubernetes-service-cli#cs_vlan_spanning_get).
{: tip}

### Gestione dell'instradamento di sottorete per i dispositivi gateway
{: #vra-routing}

Quando crei un cluster, vengono ordinate una sottorete pubblica e una privata portatili sulle VLAN a cui è connesso il cluster. Queste sottoreti forniscono indirizzi IP per i servizi NLB (network load balancer) e ALB (application load balancer) Ingress.
{: shortdesc}

Tuttavia, se hai un'applicazione router esistente, come ad esempio una [VRA (Virtual Router Appliance)](/docs/infrastructure/virtual-router-appliance?topic=virtual-router-appliance-about-the-vra#about-the-vra), le sottoreti portatili appena aggiunte dalle VLAN a cui è connesso il cluster non sono configurate sul router. Per utilizzare NLB o ALB Ingress, devi assicurarti che i dispositivi di rete possano eseguire l'instradamento tra sottoreti differenti sulla stessa VLAN [abilitando lo spanning della VLAN](/docs/infrastructure/vlans?topic=vlans-vlan-spanning#vlan-spanning).

Per controllare se lo spanning della VLAN è già abilitato, utilizza il [comando `ibmcloud oc vlan-spanning-get --region <region>`](/docs/containers?topic=containers-cli-plugin-kubernetes-service-cli#cs_vlan_spanning_get).
{: tip}

<br />


## Rimozione delle sottoreti da un cluster
{: #remove-subnets}

Se non hai più bisogno delle sottoreti, puoi rimuoverle dal tuo cluster. Le sottoreti possono essere scollegate da un cluster solo se nessuno degli indirizzi IP derivati dall'intervallo di detta sottorete è in uso nel tuo cluster.
{: shortdesc}

### Rimozione di una sottorete in un account dell'infrastruttura IBM Cloud da un cluster
{: #remove-sl-subnets}

Rimuovi una sottorete che si trova nel tuo account dell'infrastruttura IBM da un cluster. Dopo che hai rimosso la sottorete, non è più disponibile per il tuo cluster ma continua a esistere nel tuo account dell'infrastruttura IBM Cloud.
{: shortdesc}

<p class="note">Le sottoreti possono essere scollegate da un cluster solo se nessuno degli indirizzi IP derivati dall'intervallo di tale sottorete è in uso nel tuo cluster.</br></br>Gli indirizzi IP pubblici portatili vengono addebitati mensilmente. Se rimuovi la sottorete, dovrai comunque pagare l'addebito mensile per gli indirizzi IP, anche se li hai usati solo per un breve periodo di tempo.</p>

1. Trova il CIDR per la sottorete che desideri rimuovere.
  ```
  ibmcloud oc cluster-get --cluster <cluster_name> --showResources <cluster_name>
  ```
  {: pre}

  In questo output di esempio, il CIDR della sottorete da rimuovere è `169.1.1.1/29`.
  ```
  Subnet VLANs
  VLAN ID   Subnet CIDR          Public   User-managed
  2234947   10.xxx.xx.xxx/29     false    false
  2234945   169.xx.xxx.xxx/29    true     false
  2234945   169.1.1.1/29         true     false
  ```
  {: screen}

2. Utilizzando il CIDR che hai trovato nel passo precedente, ottieni l'ID della sottorete da rimuovere.
  ```
  ibmcloud oc subnets
  ```
  {: pre}

  In questo output di esempio, la sottorete con il CIDR `169.1.1.1/29` ha l'ID `1602829`.
  ```
  ID        Network             Gateway          VLAN ID   Type      Bound Cluster
  ...
  1602829   169.1.1.1/29        169.1.1.2        2234945   public    df253b6025d64944ab99ed63bb4567b6
  ```
  {: screen}

3. Scollega la sottorete dal tuo cluster. La sottorete rimane disponibile nel tuo account dell'infrastruttura IBM Cloud.
  ```
  ibmcloud oc cluster-subnet-detach --cluster <cluster_name_or_ID> --subnet-id <subnet_ID>
  ```
  {: pre}


4. Verifica che la sottorete non sia più associata al tuo cluster.
  ```
  ibmcloud oc cluster-get --showResources <cluster_name>
  ```
  {: pre}

  In questo output di esempio, viene rimossa la sottorete con il CIDR `169.1.1.1/29`.
  ```
  Subnet VLANs
  VLAN ID   Subnet CIDR         Public   User-managed
  2234947   10.xxx.xx.xxx/29    false    false
  2234945   169.xx.xxx.xxx/29  true    false
  ```
  {: screen}

### Rimozione di una sottorete in una rete in loco da un cluster
{: #remove-user-subnets}

Rimuovi una sottorete privata che si trova in una rete in loco da un cluster. Dopo che hai rimosso la sottorete, non è più disponibile per il tuo cluster ma continua a esistere nella tua rete in loco.
{: shortdesc}

1. Trova il CIDR e l'ID VLAN per la sottorete che desideri rimuovere.
  ```
  ibmcloud oc cluster-get --cluster <cluster_name> --showResources
  ```
  {: pre}

  In questo output di esempio, il CIDR della sottorete da rimuovere è `10.1.1.1/24` e l'ID VLAN è `2234947`.
  ```
  Subnet VLANs
  VLAN ID   Subnet CIDR       Public   User-managed
  2234947   10.xxx.xx.xxx/29  false    false
  2234945   169.xx.xxx.xxx/29 true     false
  2234947   10.1.1.1/24       false    true
  ```
  {: screen}

2. Utilizzando il CIDR e l'ID VLAN che hai trovato nel passo precedente, rimuovi la sottorete dal tuo cluster.
  ```
  ibmcloud oc cluster-user-subnet-rm --cluster <cluster_name_or_ID> --subnet-cidr <subnet_CIDR> --private-vlan <private_VLAN_ID>
  ```
  {: pre}

3. Verifica che la sottorete non sia più associata al tuo cluster.
  ```
  ibmcloud oc cluster-get --showResources <cluster_name>
  ```
  {: pre}

  In questo output di esempio, viene rimossa la sottorete con il CIDR `10.1.1.1/24`.
  ```
  Subnet VLANs
  VLAN ID   Subnet CIDR         Public   User-managed
  2234947   10.xxx.xx.xxx/29    false    false
  2234945   169.xx.xxx.xxx/29  true    false
  ```
  {: screen}


